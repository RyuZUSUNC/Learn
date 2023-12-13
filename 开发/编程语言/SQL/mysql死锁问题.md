>环境: MySQL 5.7.25 引擎 InnoDB

```log
2019-10-23 13:07:17.144 ERROR nested exception is org.springframework.dao.DeadlockLoserDataAccessException: 
### Error updating database.  Cause: com.mysql.cj.jdbc.exceptions.MySQLTransactionRollbackException: Deadlock found when trying to get lock; try restarting transaction
### The error may involve com.x.x.mapper.XMapper.update-Inline
### The error occurred while setting parameters
### SQL: UPDATE tb_a SET start_time = ?, end_time = ? WHERE  id = ?
### Cause: com.mysql.cj.jdbc.exceptions.MySQLTransactionRollbackException: Deadlock found when trying to get lock; try restarting transaction
com.mysql.cj.jdbc.exceptions.MySQLTransactionRollbackException: Deadlock found when trying to get lock; try restarting transaction
```

## 什么是死锁？

当多个进程访问同一`数据库`时，其中每个进程拥有的`锁`都是其他进程所需的，由此造成每个进程都无法继续下去。 简单的说，进程A等待进程B释放他的资源，B又等待A释放他的资源，这样就互相等待就形成`死锁`。

## 查看数据库基本信息

查看数据库版本：select version();

事务隔离级别查询方法：select @@tx_isolation

通过命令show engines查看一下InnoDB的特点

InnoDB支持事务，行级锁及外键。

我们平时遇到的就是多个事务之间行级锁导致的。

## 分析

业务日志中的记录太过简单，只知道哪个方法的事务发生了死锁，没有多余的信息，所以我们要到数据库中寻找更多的有用信息，通过命令 show engine Innodb status 查看:

```log
------------------------
LATEST DETECTED DEADLOCK
------------------------
2023-01-16 20:55:41 0x7f341eb5f700
# 事务1
*** (1) TRANSACTION:
TRANSACTION 231803370, ACTIVE 0 sec starting index read
mysql tables in use 2, locked 2
LOCK WAIT 1661 lock struct(s), heap size 155856, 48200 row lock(s)
MySQL thread id 1030488, OS thread handle 139861822699264, query id 84548252 10.200.200.204 root Sending data
DELETE FROM monitoring_snapshot
        WHERE monitoring_id = 820 and id not in
      (SELECT * FROM (SELECT id FROM monitoring_snapshot WHERE monitoring_id = 820 order by id desc limit 10) AS temp )
# 等待b表的X锁
*** (1) WAITING FOR THIS LOCK TO BE GRANTED:
RECORD LOCKS space id 232 page no 6694 n bits 80 index PRIMARY of table `sh_nids_service`.`monitoring_snapshot` trx id 231803370 lock mode S waiting
# 事务2
*** (2) TRANSACTION:
TRANSACTION 231803392, ACTIVE 0 sec inserting
mysql tables in use 1, locked 1
4 lock struct(s), heap size 1136, 2 row lock(s), undo log entries 1
MySQL thread id 1032399, OS thread handle 139861830268672, query id 84548280 10.200.200.204 root update
insert into monitoring_snapshot(user_id,response_time,result,node_id,snapshot,packet_loss_rate,monitoring_id,node_ip,node_name,create_time,type,ping_times,receive_times)
        VALUES
          
            (null,'157','1',
             '0232d759d64525edf79559aaacbe8f69','Cache-Control: private<br>Content-Type: text/html; charset=gb2312<br>Vary: Accept-Encoding<br>Server: Microsoft-IIS/7.5<br>X-AspNet-Version: 2.0.50727<br>Set-Cookie: ASP.NET_SessionId=0t5e5nqbmvcnvpvtzmzfp5fg; path=/; HttpOnly<br>X-Powered-By: ASP.NET<br>Date: Mon, 16 Jan 2023 12:55:40 GMT<br>','200',
             835,'118.24.147.50','TX_Cloud',
             '2023-01-16 20:55:41.04','1','0',
             null)
         , 
            (null,'151','1',
             '319e69d2fd7dfc42ece42ea53b9b3fe0','Cache-Control: private<br>Content-Type: text/html; charset=gb2312<br>Vary: Accept-Encoding<br>Server: Microsoft-IIS/7.5<br>X-AspNet-Version: 
# 持有b表的X锁
*** (2) HOLDS THE LOCK(S):
RECORD LOCKS space id 232 page no 6694 n bits 80 index PRIMARY of table `sh_nids_service`.`monitoring_snapshot` trx id 231803392 lock_mode X locks rec but not gap
# 等待a表的X锁
*** (2) WAITING FOR THIS LOCK TO BE GRANTED:
RECORD LOCKS space id 232 page no 6694 n bits 80 index PRIMARY of table `sh_nids_service`.`monitoring_snapshot` trx id 231803392 lock_mode X insert intention waiting
# 回滚事务2
*** WE ROLL BACK TRANSACTION (2)
```

## 总结排查步骤

1. 通过业务系统日志快速定位到发生死锁的代码块
2. 查看InnoDB的死锁日志，找出各个事务对应的代码块
3. 通过死锁日志和业务代码推测画出死锁的事务发生场景

## 降低发生死锁的概率
1. 避免大事务，可以拆分成多个小事务，因为大事务耗时长，与其他事务发生的概率就大。
2. 多个事务操作相同的一些资源，尽量保持顺序一致。
3. 更新语句尽量只更新必要的字段，内容相同的字段不要更新。

## 记录完整的死锁日志

show engine innodb status 时，显示的信息不全。

这是mysql客户端的一个bug：BUG#19825，交互式客户端限制了输出信息最大为 `64KB`，因此更多的信息无法显示。

但我们可以通过开启锁监控来查看完整的日志，方式如下：

```bash
# 建议排查问题后关闭，15秒输出一次，会导致日志越来越大
-- 开启标准监控 开ON/关OFF
set GLOBAL innodb_status_output=ON;

-- 开启锁监控  开ON/关OFF
set GLOBAL innodb_status_output_locks=ON;
```

也可以通过一个专门用于记录死锁日志的参数：

```bash
set GLOBAL innodb_print_all_deadlocks=ON;
```

内容一般输出到 mysql error log 里，查看日志位置：select @@log_error

