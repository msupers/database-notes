# sql语句总结

## PG查询某列字段重复的行

```sql
select jenkins_job_name  from e_ci_configure where flag <> 'd' and jenkins_job_name in (select jenkins_job_name from e_ci_configure where flag <> 'd' group by jenkins_job_name having count (jenkins_job_name) >1 )
```