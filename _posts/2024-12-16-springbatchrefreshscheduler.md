---
title: Spring - Spring batch와 스케줄러를 구현해 refresh 토큰을 제거 구현 
date: 2024-12-16 21:40:00 + 09:00
categories: [Backend, Spring]
tags: [web, backend, spring, schduler, batch]
---

오늘은 DB에 저장된 refresh token들을 주기적으로 삭제해야하는데<br> 
이를 해결하기 위해서 Spring batch와 스케줄러를 사용하였다.

우선 코드를 보기전 Spring batch를 간략하게 소개하겠다.

## ❓ **Spring batch란?**
대용량의 데이터를 효율적으로 처리하고 관리할 수 있도록 설계된 Spring 기반의 처리 프레임워크이다.

스프링의 특징들은 아래와 같다.

1. 대규모 데이터 처리
- 대용량의 데이터를 읽고 처리한 뒤 다른 저장소에 쓰는 작업을 안정적이고 효율적으로 처리 가능
2. 재사용 가능한 구조 
- 배치 작업의 구성 요소를 모듈화해서 재사용 가능
3. 병렬 처리 및 스케줄링
- 멀티스레드와 파티셔닝을 통한 병렬 처리 지원
4. 트랜잭션 관리
- 데이터 처리 중 트랜잭션을 관리하여 실패시 롤백 및 데이터 정합성 유지가 수월함
5. 로깅 및 모니터링
- 배치 작업 상태와 실행 기록을 데이터베이스나 로그에 기록
- 작업 실패, 성공, 소유 시간 등을 메타 테이블에 자동으로 저장

이러한 특징들을 가지고 있기에 로그인 할때마다 발급되는 refresh token에 만료기간 검증 및 제거에 효율적이라고 판단했다.

Spring batch에 대해서 자세하게 다루면 이번 글이 끝이 안날 것 같으니 간단한 개념만 알아보자.

## 📤 **Spring batch 기본 개념**

### **Job**
- Spring batch의 작업 실행 단위

### **Job Parameter**
- JobInstance를 구분하는데 사용

### **Job Instance**
- Job의 실행 단위

### **Job Execution**
- Job Instance에 실행 정보를 담고있는 객체

### **Job Repository**
- Job과 Step의 실행 상태와 메타데이터를 관리하는 핵심 컴포넌트

### **JobLauncher**
- Job을 실행시키는 역할 

### **PlatformTransactionManager**
- 트랜잭션 관리를 추상화한 인터페이스

### **Step**
- Job을 구성하는 작업의 논리적 단위

### **Step Instance**
- Step의 실행 단위

### **Step Execution**
- Step Instane의 실행 정보를 담고있는 객체

## 🚀 **스케줄러 구현**

RefreshRemomveScheduler.java
```java
package com.example.oqp.scheduler;

import org.springframework.batch.core.Job;
import org.springframework.batch.core.JobParametersBuilder;
import org.springframework.batch.core.JobParametersInvalidException;
import org.springframework.batch.core.launch.JobLauncher;
import org.springframework.batch.core.repository.JobExecutionAlreadyRunningException;
import org.springframework.batch.core.repository.JobInstanceAlreadyCompleteException;
import org.springframework.batch.core.repository.JobRestartException;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.scheduling.annotation.EnableScheduling;
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Component;

@Component
@EnableScheduling
public class RefreshRemoveScheduler {
    private final Job refreshRemove;
    private final Job refreshUseYn;
    private final JobLauncher jobLauncher;

    public RefreshRemoveScheduler(@Qualifier("refreshTokenStatusRemoveJob") Job refreshRemove, @Qualifier("refreshTokenUseYnJob") Job refreshUseYn, JobLauncher jobLauncher) {
        this.refreshRemove = refreshRemove;
        this.refreshUseYn = refreshUseYn;
        this.jobLauncher = jobLauncher;
    }

    @Scheduled(cron = "0 0 */12 * * *")
    public synchronized void removeRefresh() throws JobInstanceAlreadyCompleteException, JobExecutionAlreadyRunningException, JobParametersInvalidException, JobRestartException {
        jobLauncher.run(refreshRemove, new JobParametersBuilder()
                .addLong("time", System.currentTimeMillis())
                .toJobParameters()
        );
    }

    @Scheduled(cron = "0 0 * * * *")
    public synchronized void useYn() throws JobExecutionAlreadyRunningException, JobRestartException, JobInstanceAlreadyCompleteException, JobParametersInvalidException {
        jobLauncher.run(refreshUseYn, new JobParametersBuilder()
                .addLong("time", System.currentTimeMillis())
                .toJobParameters()
        );
    }
}
```
이런식으로 스케줄러가 Job을 실행시키도록 구현하였다.<br>
여기서 마저 설명을 하겠다.

우선 스케줄러를 사용하려면 위 코드에서 보이듯이
```java
@EnableScheduling
```
이 어노테이션을 꼭 사용해야한다.

이제 코드를 하나씩 뜯어보겠다.

빈을 주입시키는건 Spring을 공부했다면 이미 다 알고있을테니 넘어가고 바로 스케줄러로 넘어가보자.

```java
@Scheduled(cron = "0 0 */12 * * *")
    public synchronized void removeRefresh() throws JobInstanceAlreadyCompleteException, JobExecutionAlreadyRunningException, JobParametersInvalidException, JobRestartException {
        jobLauncher.run(refreshRemove, new JobParametersBuilder()
                .addLong("time", System.currentTimeMillis())
                .toJobParameters()
        );
    }
```
``@Scheduled`` 어노테이션을 사용해서 스케줄러를 구현하는데 ``cron`` 이라는 속성이 보인다.

``cron``은 작업의 실행 주기를 지정하는 속성이다.<br>
``removeRefresh`` 스케줄러의 동작 주기는 12시간 마다 돌도록 설정해둔것이다.

``cron`` 의 표현식은 아주 간닪다.

```java
cron = "0 0 */12 * * *"
       초 분 시간 일 월 요일
```
이런식으로 구성이 된다.

저 표현식을 해석하자면 
0 초 0 분 */12 시간 * 일 * 월 * 요일로
매일 요일상관 없이 매월 12시간마다 돌라는 표현식이다.

```java
jobLauncher.run(refreshRemove, new JobParametersBuilder()
                .addLong("time", System.currentTimeMillis())
                .toJobParameters()
        );
```
위에서 설명했듯이 JobLauncher는 Job을 실행시키는 역할을 한다. 

또한 인자로 JobParameters를 넘기는데 위에서 설명했듯이 JobParameter는 JobInstance를 구별하는 용도로 사용된다.

바로 batch 코드를 확인해보자.

```java
package com.example.oqp.scheduler.job;

import com.example.oqp.db.entity.JwtRefresh;
import jakarta.persistence.EntityManager;
import jakarta.persistence.EntityManagerFactory;
import jakarta.persistence.PersistenceContext;
import lombok.RequiredArgsConstructor;
import lombok.extern.slf4j.Slf4j;
import org.springframework.batch.core.Job;
import org.springframework.batch.core.Step;
import org.springframework.batch.core.configuration.annotation.EnableBatchProcessing;
import org.springframework.batch.core.configuration.annotation.StepScope;
import org.springframework.batch.core.job.builder.JobBuilder;
import org.springframework.batch.core.repository.JobRepository;
import org.springframework.batch.core.step.builder.StepBuilder;
import org.springframework.batch.item.Chunk;
import org.springframework.batch.item.ItemProcessor;
import org.springframework.batch.item.database.JpaItemWriter;
import org.springframework.batch.item.database.JpaPagingItemReader;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.task.TaskExecutor;
import org.springframework.scheduling.concurrent.ThreadPoolTaskExecutor;
import org.springframework.transaction.PlatformTransactionManager;

@Slf4j
@Configuration
@RequiredArgsConstructor
@EnableBatchProcessing
public class RefreshRemoveJob {

    private final JobRepository jobRepository;
    private final PlatformTransactionManager transactionManager;
    private final EntityManagerFactory entityManagerFactory;

    @Bean("refreshTokenStatusRemoveJob")
    public Job refreshRemoveJob(@Qualifier("deleteRefreshStep") Step deleteRefreshStep) {
        return new JobBuilder("refreshRemoveJob", jobRepository)
                .start(deleteRefreshStep)
                .build();
    }

    @Bean("deleteRefreshStep")
    public Step deleteRefreshStep(@Qualifier("refreshItemReader") JpaPagingItemReader<JwtRefresh> refreshItemReader){
        return new StepBuilder("refreshRemoveStep", jobRepository)
                .<JwtRefresh, JwtRefresh>chunk(100, transactionManager)
                .reader(refreshItemReader)
                .processor(refreshChangeNProcessor())
                .writer(refreshUpdateWriter())
                .taskExecutor(taskExecutor())
                .build();
    }

    @StepScope
    @Bean("refreshItemReader")
    public JpaPagingItemReader<JwtRefresh> refreshRead(){
        JpaPagingItemReader<JwtRefresh> reader = new JpaPagingItemReader<>();
        reader.setPageSize(100);
        reader.setQueryString("select f from JwtRefresh f where f.useYn = 'N'");
        reader.setEntityManagerFactory(entityManagerFactory);
        return reader;
    }

    @StepScope
    @Bean
    public ItemProcessor<JwtRefresh, JwtRefresh> refreshChangeNProcessor(){
        return new ItemProcessor<JwtRefresh, JwtRefresh>() {

            @Override
            public JwtRefresh process(JwtRefresh item) throws Exception {
                log.info("item : {}", item.toString());

                return item;
            }
        };
    }

    @StepScope
    @Bean
    public JpaItemWriter<JwtRefresh> refreshUpdateWriter() {
        JpaItemWriter<JwtRefresh> writer = new JpaItemWriter<>(){
            @Override
            protected void doWrite(EntityManager entityManager, Chunk<? extends JwtRefresh> items) {
                for (JwtRefresh jwtRefresh : items) {
                    log.info("Deleting item: {}", jwtRefresh);

                    if (!entityManager.contains(jwtRefresh)) {
                        jwtRefresh = entityManager.merge(jwtRefresh);
                    }
                    entityManager.remove(jwtRefresh);
                }
            }
        };
        writer.setEntityManagerFactory(entityManagerFactory);

        return writer;
    }

    public TaskExecutor taskExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(5);
        executor.setMaxPoolSize(5);
        executor.setThreadNamePrefix("refreshRemoveJob-");
        executor.initialize();
        return executor;
    }
}
```
코드가 좀 길긴하지만 천천히 뜯어보자.

우선 Job은 Spring batch 작업에 실행 단위라고 하였다.

이런 Job은 하나 이상의 Step으로 구성된다.

우선 가장 위 코드부터 설명하겠다.<br>

```java
@Bean("refreshTokenStatusRemoveJob")
    public Job refreshRemoveJob(@Qualifier("deleteRefreshStep") Step deleteRefreshStep) {
        return new JobBuilder("refreshRemoveJob", jobRepository)
                .start(deleteRefreshStep)
                .build();
    }
```
``JobBuilder``를 사용해서 Job을 생성는 코드이다.<br>

``.start``를 사용하여 실행할 Step을 지정한다.

```java
 @Bean("deleteRefreshStep")
    public Step deleteRefreshStep(@Qualifier("refreshItemReader") JpaPagingItemReader<JwtRefresh> refreshItemReader){
        return new StepBuilder("refreshRemoveStep", jobRepository)
                .<JwtRefresh, JwtRefresh>chunk(100, transactionManager)
                .reader(refreshItemReader)
                .processor(refreshChangeNProcessor())
                .writer(refreshUpdateWriter())
                .taskExecutor(taskExecutor())
                .build();
    }
```
위 코드는 StepBuilder를 사용하여 Step을 생성하는 코드이다.

하나씩 뜯어보자면

```java
.<JwtRefresh, JwtRefresh>chunk(100, transactionManager)
```
이 부분은 Chunk 기반 처리를 설정하는 코드이다.<br>

> Chunk기반?<br>
> 데이터를 일정 크기로 나누어 읽고 처리하는 방식을 말한다.

``<JwtRefresh, JwtRefresh>`` 입력타입과 출력타입을 나타내는 것인데
ItemReader로 읽어드릴 데이터 타입, ItemWriter에서 처리할 데이터 타입을 명시한다.

```java
chunk(100, transactionManager)
```

한번의 100개의 데이터를 읽고 처리한다는 뜻이다.

``transactionManager``는 트랜잭션 매니저로 지정하여 100개의 데이터 처리가 완료되면 트랜잭션이 커밋된다.

```java
.reader(refreshItemReader)
.processor(refreshChangeNProcessor())
.writer(refreshUpdateWriter())
.taskExecutor(taskExecutor())
.build();
```
각각 ItemReader, ItemProcessor, ItemWriter, taskExecutor를 지정하는 코드이다.

ItemReader, ItemProcessor, ItemWriter를 간략하게 설명하겠다
- ItemReader: 데이터를 읽는 역할
- ItemProcessor: 읽어온 데이터를 변환하는 역할(없어도 됨)
- ItemWriter: ItemProcessor로 변환 혹은 ItemReader로 읽어온 데이터를 처리하는 역할

이제 자세한 코드를 알아보자.

```java
@StepScope
@Bean("refreshItemReader")
  public JpaPagingItemReader<JwtRefresh> refreshRead(){
        JpaPagingItemReader<JwtRefresh> reader = new JpaPagingItemReader<>();
        reader.setPageSize(100);
        reader.setQueryString("select f from JwtRefresh f where f.useYn = 'N'");
        reader.setEntityManagerFactory(entityManagerFactory);
        return reader;
    }
```

우선 ``@StepScope`` 는 Step이 실행될때마다 해당 빈이 초기화되도록 설정하는 어노테이션이다.

ItemReader, ItemWriter에도 종류가 아주 많지만 나는 ``JpaPagingItemReader``를 사용하였다.

``JpaPagingItemReader``를 사용한 이유는 데이터를 읽어올때 페이징을 적용시켜서 한번에 읽는 데이터의 수를 제한할 수 있기 때문이다.

또한 로그인할때마다 발급되는 jwt 토큰 특성상 DB에 쌓이는 refresh token의 수는 아주 많을 것이기 때문에 멀티 스레드 방식을 선택하였는데 

``JpaPagingItemReader``는 스레드가 독립적으로 데이터를 읽도록 설계되어있기 떄문에 데이터 처리시 충돌을 방지해준다는 이점을 가지고 있어서 선택하였다.

이제 코드를 한줄씩 뜯어보겠다.

```java
reader.setPageSize(100);
```
위 코드는 한번에 읽어올 데이터들을 설정하는데 보통 Chunk 사이즈와 동일하게 잡는다.

```java
reader.setQueryString("select f from JwtRefresh f where f.useYn = 'N'");
```
위 코드는 JPQL을 사용하여 데이터 조회 쿼리를 작성한 것이다.

```java
reader.setEntityManagerFactory(entityManagerFactory);
```
JpaPagingItemReader에 EntityManagerFactory를 설정하는 부분이다.

이런식으로 조회된 데이터들은 ``processor`` 로 넘어간다.

```java
@StepScope
    @Bean
    public ItemProcessor<JwtRefresh, JwtRefresh> refreshChangeNProcessor(){
        return new ItemProcessor<JwtRefresh, JwtRefresh>() {

            @Override
            public JwtRefresh process(JwtRefresh item) throws Exception {
                log.info("item : {}", item.toString());

                return item;
            }
        };
    }
```
JpaPagingItemReader에서 조회되어 넘어온 데이터들을 변환할때 ItemProcessor를 사용하지만 

현재 로직에서는 변환이 필요 없기 때문에 어떤 값들이 넘어오는지 확인해보기 위해서 로그만 설정해두었다.

이렇게 ``processor``를 거친 데이터들은 ``writer``로 넘어간다

```java
@StepScope
    @Bean
    public JpaItemWriter<JwtRefresh> refreshUpdateWriter() {
        JpaItemWriter<JwtRefresh> writer = new JpaItemWriter<>(){
            @Override
            protected void doWrite(EntityManager entityManager, Chunk<? extends JwtRefresh> items) {
                for (JwtRefresh jwtRefresh : items) {
                    log.info("Deleting item: {}", jwtRefresh);

                    if (!entityManager.contains(jwtRefresh)) {
                        jwtRefresh = entityManager.merge(jwtRefresh);
                    }
                    entityManager.remove(jwtRefresh);
                }
            }
        };
        writer.setEntityManagerFactory(entityManagerFactory);

        return writer;
    }
```
``processor``에서 넘어온 데이터를 ``entityManager``를 사용하여 제거 처리를 한 후 반환한다.

```java
public TaskExecutor taskExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(5);
        executor.setMaxPoolSize(5);
        executor.setThreadNamePrefix("refreshRemoveJob-");
        executor.initialize();
        return executor;
    }
```
``TaskExecutor`` 는 스레드를 설정하는데 사용하는데 위 코드는 멀티 스레드를 설정하는 코드이다.

스케줄러 코드를 다시 확인해보면

```java
@Scheduled(cron = "0 0 */12 * * *")
    public synchronized void removeRefresh() throws JobInstanceAlreadyCompleteException, JobExecutionAlreadyRunningException, JobParametersInvalidException, JobRestartException {
        jobLauncher.run(refreshRemove, new JobParametersBuilder()
                .addLong("time", System.currentTimeMillis())
                .toJobParameters()
        );
    }

    @Scheduled(cron = "0 0 * * * *")
    public synchronized void useYn() throws JobExecutionAlreadyRunningException, JobRestartException, JobInstanceAlreadyCompleteException, JobParametersInvalidException {
        jobLauncher.run(refreshUseYn, new JobParametersBuilder()
                .addLong("time", System.currentTimeMillis())
                .toJobParameters()
        );
    }
```
만료 기간을 주기적으로 확인하는 스케줄러 또한 구현되있지만..<br>
글이 너무 길어지기 때문에 이건 다음 글에서 다루도록 하겠다.

