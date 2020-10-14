# sql语句总结

## PG查询某列字段重复的行

为什么总结这个? <br> 在工作中,有个功能是从数据库里select数据, 原本某个字段`jenkins_job_name`是不能重复的,但是由于种种原因,`select`数据发现`jenkins_job_name`这个字段取出来了多行.<br> 因此要查出来还有没有别的重复的`脏数据`,用到了如下的sql

```sql
select jenkins_job_name  from e_ci_configure where flag <> 'd' and jenkins_job_name in (select jenkins_job_name from e_ci_configure where flag <> 'd' group by jenkins_job_name having count (jenkins_job_name) >1 )
```