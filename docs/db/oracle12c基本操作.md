su - oracle

sqlplus / as sysdba

show pdbs;

##创建PDB

create pluggable database urpdb admin user urpdb identified by J38xmmAqbc12ed roles=(dba);
alter pluggable database urpdb open;
alter session set container=urpdb;

create tablespace urpdb datafile '+DATA' size 1G autoextend on next 1G maxsize 31G extent management local segment space management auto;
alter tablespace urpdb add datafile '+DATA' size 1G autoextend on next 1G maxsize 31G;
alter tablespace urpdb add datafile '+DATA' size 1G autoextend on next 1G maxsize 31G;
alter tablespace urpdb add datafile '+DATA' size 1G autoextend on next 1G maxsize 31G;
alter tablespace urpdb add datafile '+DATA' size 1G autoextend on next 1G maxsize 31G;

create user urpuser identified by J3nmmAAb6EYn default tablespace urpdb account unlock;

grant dba to urpuser;
grant select any table to urpuser;

sqlplus urpuser/J3nmmAAb6EYn@10.8.14.15:1521/s_urpdb

[oracle@jcpt-rac1 ~]$ srvctl add service -d xydb -s s_urpdb -r xydb1,xydb2 -P basic -e select -m basic -z 180 -w 5 -pdb urpdb
[oracle@jcpt-rac1 ~]$ srvctl status service -d xydb -s s_urpdb
Service s_urpdb is not running.
[oracle@jcpt-rac1 ~]$ srvctl start service -d xydb -s s_urpdb
[oracle@jcpt-rac1 ~]$ srvctl status service -d xydb -s s_urpdb
Service s_urpdb is running on instance(s) xydb1,xydb2
[oracle@jcpt-rac1 ~]$ lsnrctl status 
