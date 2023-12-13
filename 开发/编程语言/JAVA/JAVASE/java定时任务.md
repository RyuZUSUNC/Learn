# ScheduledExecutorService
ScheduledExecutorService 将定时任务与线程池功能结合使用：当任务到达执行时间，将任务交于线程池，由线程池分配线程去执行任务。
其中有两个方法容易混淆：`scheduleAtFixedRate` `scheduleWithFixedDelay`

`ScheduleAtFixedRate`: 两次任务之间的间隔时间，取决于每次任务执行的时间长短；

`ScheduleWithFixedDelay`: 不受任务执行时间长短影响，固定这次任务执行结束后隔x秒执行下一次。

```java
public ScheduledFuture<?> scheduleAtFixedRate(Runnable command,
                                                  long initialDelay,
                                                  long period,
                                                  TimeUnit unit);

```
假如每个任务执行花费 `time` 时间，如果 `time >= period`，则这次任务执行结束后 立刻执行下一次任务。

如果 `time < period` , 则这次任务执行结束后 ，隔 `period - time` 后执行下一次任务。

