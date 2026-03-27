---
title: 线程池
date: 2024-05-28 09:41:10
tags:
---

# 什么是线程池

线程池是一种基于池化资源管理的方法，用于高效地管理线程的创建和销毁，从而提升系统性能。在系统启动时，线程池会创建固定空闲线程。当程序提交任务给线程池工作队列中，线程池便分配一个空闲线程来执行该任务。任务完成后，线程不会被销毁，而是返回线程池，进入等待状态，以便执行后续的任务。尽管一个线程一次只能执行一个任务，线程池能够同时处理多个任务的提交。

## 核心功能

- 工作队列

  需要执行的任务队列，存储程序向线程池提交的任务，等待状态

- 工作线程

  系统线程池中的线程数量，负责将工作队列中等待状态的任务取出来执行

- 线程池管理器

  负责管理和线程池的状态，包括创建和销毁

# 为什么使用线程池

当业务需求导致系统频繁地启动和关闭线程时，这种操作不仅成本高，还会大量消耗系统资源，并增加线程过度切换的风险，可能导致系统资源崩溃。在这种情况下，使用线程池是一个很好的解决方案。线程池通过重用一组现有线程，减少了线程创建和销毁的频率，从而有效降低了资源消耗和提高了系统稳定性。

总结：

- 提高响应速度
- 降低资源利用率
- 提高线程的管理能力

# 线程池的作用是什么

线程池的作用减少资源消耗对任务进行优先级和调度等，可以实现负载均衡根据任务需求和复杂性调整线程数量。此外，线程池支持即时执行任务，有效减少处理请求的延迟，增强应用程序的可伸缩性，允许根据实际负载动态调整线程池大小以优化资源使用。线程池还增强了错误恢复和容错能力，通过内置策略处理执行中的错误，保证了程序的整体稳定性和可靠性。

# 使用`Executors`案例

## `Executors.newFixedThreadPool(int nThreads)`

这是一个固定的工作线程池,当系统启动的时候创建固定大小的线程池。如：可以将一个大文件分割成多个部分，同时由不同的线程进行处理

- 当你向线程池提交一个任务时，线程池会尝试使用空闲的线程去执行这个任务，如果所有线程都在忙，新的任务会被放入队列中等待执行，一旦有线程变为空闲状态，它会从队列中取出下一个任务并执行。

  ```
     public static void main(String[] args) {
          // 在系统是创建三个固定空闲的线程池，从而当任务执行是直接使用线程池中的线程
          ExecutorService fixedThreadPool = Executors.newFixedThreadPool(3);
          for (int i = 0; i < 10; i++) {
              fixedThreadPool.execute(new Runnable() {
                  @Override
                  public void run() {
                      // 打印正在执行的缓存的线程信息
                      System.out.println(Thread.currentThread().getName());
                      try {
                          Thread.sleep(2000);
                      }catch (InterruptedException e){
                          e.printStackTrace();
                      }
                  }
              });
          }
      }
  ```

  执行结果

  ```
  pool-1-thread-1
  pool-1-thread-3
  pool-1-thread-2
  pool-1-thread-3
  pool-1-thread-1
  pool-1-thread-2
  pool-1-thread-2
  pool-1-thread-3
  pool-1-thread-1
  pool-1-thread-3
  ```

## `Executors.newCachedThreadPool()`

​		这是一个可缓存的线程池，执行时先查看线程池中是否有以前建立好的线程，如果有直接使用线程池中的线程，如果没有则创建一个新线程添加到先吃池中，一般使用在大量短任务中

- 当执行任务还没有结束，则创建新线程，但任务执行结束，选择线程池工作队列中的某个线程执行当前任务

  ```
    private static void test() {
          // 创建一个可以缓存的线程池
          ExecutorService cachedThreadPool = Executors.newCachedThreadPool();
          for (int i = 0; i < 10; i++) {
              try {
                  Thread.sleep(1000);
              }catch (InterruptedException e){
                  e.printStackTrace();
              }
              cachedThreadPool.execute(new Runnable() {
                  @Override
                  public void run() {
                      // 打印正在执行的缓存的线程信息
                      System.out.println(Thread.currentThread().getName());
                      try {
                          Thread.sleep(1000);
                      }catch (InterruptedException e){
                          e.printStackTrace();
                      }
                  }
              });
          }
      }
  ```

  执行结果

  ```
  pool-1-thread-1
  pool-1-thread-2
  pool-1-thread-2
  pool-1-thread-1
  pool-1-thread-2
  pool-1-thread-1
  pool-1-thread-2
  pool-1-thread-1
  pool-1-thread-1
  pool-1-thread-2
  ```

  

- 当执行当前任务是上一个任务已经完成，会复用执行上一个任务的线程

  ```
  
      private static void test1() {
          // 创建一个可以缓存的线程池
          ExecutorService cachedThreadPool = Executors.newCachedThreadPool();
          for (int i = 0; i < 10; i++) {
              try {
                  Thread.sleep(1000);
              }catch (InterruptedException e){
                  e.printStackTrace();
              }
              cachedThreadPool.execute(new Runnable() {
                  @Override
                  public void run() {
                      // 如果当前执行的任务时间短，则继续使用当前线程不需要重写创建或从线程池中获取
                      // 打印正在执行的缓存的线程信息
                      System.out.println(Thread.currentThread().getName());
  
                  }
              });
          }
      }
  ```

  执行结果

  ```
  pool-1-thread-1
  pool-1-thread-1
  pool-1-thread-1
  pool-1-thread-1
  pool-1-thread-1
  pool-1-thread-1
  pool-1-thread-1
  pool-1-thread-1
  pool-1-thread-1
  pool-1-thread-1
  ```

  

## `Executors.newSingleThreadExecutor()`

​		是一个单线程化的线程池，它只会用唯一的工作线程执行任务，保证所有任务都是按顺序执行。如：文件操作、数据库事务处理

- 将所有任务提交到线程池工作队列中，首先只有一个任务在执行工作，其它任务在等待上一个任务执行完才可以执行

  ```
  public class NewSingleThreadExecutor {
      public static void main(String[] args) {
          ExecutorService singleThreadExecutor = Executors.newSingleThreadExecutor();
          // 这里会直接执行完循环，提交10个任务给线程执行，但是只有一个线程工作
          for (int i = 0; i < 10; i++) {
              final int index = i;
              singleThreadExecutor.execute(new Runnable() {
                  @Override
                  public void run() {
                      try {
                          System.out.println(Thread.currentThread().getName()+"index："+index);
                          Thread.sleep(5000);
                      } catch (InterruptedException e) {
                          throw new RuntimeException(e);
                      }
                  }
              });
          }
      }
  }
  ```

  执行结果

  ```
  pool-1-thread-1index：0
  pool-1-thread-1index：1
  pool-1-thread-1index：2
  pool-1-thread-1index：3
  pool-1-thread-1index：4
  pool-1-thread-1index：5
  pool-1-thread-1index：6
  pool-1-thread-1index：7
  pool-1-thread-1index：8
  pool-1-thread-1index：9
  ```

## `Executors.newScheduledThreadPool(int corePoolSize)`

​       是一个具有固定数量核心线程的计划任务线程池，这种线程池主要用于执行那些需要在指定时间延迟之后运行，或者需要周期性执行的任务。比如：每天或每小时执行数据备份、生成报告

- `scheduleAtFixedRate(Runnable command, long initialDelay,long period,TimeUnit unit)`有四个参数

  - command：这是你要执行的任务
  - `initialDelay`:这个任务开始之前延迟到什么时候开始执行
  - period：这个是开始之后这个任务多长时间执行一次
  - unit：时间单位，这里是秒

  ```
  public class NewScheduledThreadPool {
      public static void main(String[] args) {
          // 系统启动是创建三个空闲的线程
          ScheduledExecutorService scheduledExecutorService = Executors.newScheduledThreadPool(3);
          scheduledExecutorService.scheduleAtFixedRate(new Runnable() {
              @Override
              public void run() {
                  System.out.println("延迟2秒后每4秒执行一次");
              }
          },2,4, TimeUnit.SECONDS);
      }
  }
  ```

  执行结果

  ```
  延迟2秒后每4秒执行一次
  延迟2秒后每4秒执行一次
  延迟2秒后每4秒执行一次
  延迟2秒后每4秒执行一次
  延迟2秒后每4秒执行一次
  延迟2秒后每4秒执行一次
  ```

  

