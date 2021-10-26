su - oracle

lsnrctl status



<br>

env|grep LANG

env|grep NLS_LANG



<br>

sqlplus / as sysdba

##查看归档

```oracle
select * from dual;

archive log list;

show parameter recovery
```



<br>

##生产环境部分参数

```oracle
show parameter process;

alter profile default limit password_life_time unlimited;
```



<br>

##创建表空间及用户

```oracle
select file_name,tablespace_name from dba_data_files;

create tablespace portal_service datafile '/u01/app/oracle/oradata/xydb/portal01.dbf' size 1G autoextend on next 1G maxsize 31G ;

alter tablespace portal_service add datafile '/u01/app/oracle/oradata/xydb/portal02.dbf' size 1G autoextend on next 1G maxsize 31G ;

create user portal_service identified by Oraps485Cle default tablespace portal_service;
grant dba to portal_service;
```



<br>

##字符集

```
select userenv('language') from dual;
```

