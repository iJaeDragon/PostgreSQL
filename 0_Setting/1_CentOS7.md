# CentOS7

### PostgreSQL repository 설치 및 활성화

```
  # sudo yum -y install https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```

### PostgreSQL repository 활성화 확인

```
  # sudo yum repolist
  Loaded plugins: fastestmirror
  Loading mirror speeds from cached hostfile
   * base: mirror.kakao.com
   * epel: d2lzkl7pfhq30w.cloudfront.net
   * extras: mirror.kakao.com
   * updates: mirror.kakao.com
  repo id                           repo name                               status
  base/7/x86_64                     CentOS-7 - Base                         10,072
  epel/x86_64                       Extra Packages for Enterprise Linux 7 - 13,791
  extras/7/x86_64                   CentOS-7 - Extras                          526
  mysql-connectors-community/x86_64 MySQL Connectors Community                 258
  mysql-tools-community/x86_64      MySQL Tools Community                      108
  mysql80-community/x86_64          MySQL 8.0 Community Server                 503
  pgdg-common/7/x86_64              PostgreSQL common RPMs for RHEL / CentO    545
  pgdg12/7/x86_64                   PostgreSQL 12 for RHEL / CentOS 7 - x86  1,377
  pgdg13/7/x86_64                   PostgreSQL 13 for RHEL / CentOS 7 - x86  1,140
  pgdg14/7/x86_64                   PostgreSQL 14 for RHEL / CentOS 7 - x86    900
  pgdg15/7/x86_64                   PostgreSQL 15 for RHEL / CentOS 7 - x86    613
  updates/7/x86_64                  CentOS-7 - Updates                       6,173
  repolist: 36,006
```

### PostgreSQL 설치

```
  # sudo yum -y install postgresql13 postgresql13-server
```

<details>
<summary>접기/펼치기</summary>

## 에러가 나는경우

```
  # date
```

date 커맨드로 현재 시간을 확인하고 실제 시간과 차이가 많이 난다면 현재 시간으로 조정

```
  # timedatectl set-ntp no
  # timedatectl set-time "2024-09-15 11:16:52"
  # timedatectl set-ntp yes
```
</details>

### PostgreSQL 초기화

```
  # sudo /usr/pgsql-13/bin/postgresql-13-setup initdb
```

### PostgreSQL 서비스 시작

```
  # sudo systemctl start postgresql-13
```

### PostgreSQL 서비스 상태 확인

```
  # sudo systemctl status postgresql-13
  ● postgresql-13.service - PostgreSQL 13 database server
     Loaded: loaded (/usr/lib/systemd/system/postgresql-13.service; disabled; vendor preset: disabled)
     Active: active (running) since 일 2024-09-15 11:28:38 KST; 9min ago
       Docs: https://www.postgresql.org/docs/13/static/
    Process: 21148 ExecStartPre=/usr/pgsql-13/bin/postgresql-13-check-db-dir ${PGDATA} (code=exited, status=0/SUCCESS)
   Main PID: 21154 (postmaster)
     CGroup: /system.slice/postgresql-13.service
             ├─21154 /usr/pgsql-13/bin/postmaster -D /var/lib/pgsql/13/data/
             ├─21156 postgres: logger
             ├─21158 postgres: checkpointer
             ├─21159 postgres: background writer
             ├─21160 postgres: walwriter
             ├─21161 postgres: autovacuum launcher
             ├─21162 postgres: stats collector
             └─21163 postgres: logical replication launcher
  
   9월 15 11:28:37 localhost.localdomain systemd[1]: Starting PostgreSQL 13 da...
   9월 15 11:28:37 localhost.localdomain postmaster[21154]: 2024-09-15 11:28:3….
   9월 15 11:28:37 localhost.localdomain postmaster[21154]: 2024-09-15 11:28:3….
   9월 15 11:28:38 localhost.localdomain systemd[1]: Started PostgreSQL 13 dat...
  Hint: Some lines were ellipsized, use -l to show in full.
```

### 재부팅 시 PostgreSQL 서비스가 시작되록 서비스 활성화

```
  sudo systemctl enable postgresql-13
  Created symlink from /etc/systemd/system/multi-user.target.wants/postgresql-13.service to /usr/lib/systemd/system/postgresql-13.service.

```

### PostgreSQL Admin Password 설정

```
  # sudo su - postgres
  # psql -c "alter user postgres with password '원하는비밀번호'"
  ALTER ROLE
```

### 외부 접속을 허용이 필요할 경우 postgresql.conf, pg_hba.conf 파일을 수정해야 한다.

```
  # sudo sudo vi /var/lib/pgsql/13/data/postgresql.conf
  listen_addresses = '*'
```

```
  # sudo sudo vi /var/lib/pgsql/13/data/pg_hba.conf
    
  # 모든 IP 허용
  host  all all 0.0.0.0/0  md5
  
  # 특정 IP 대역 허용 (192.168.0.1 ~ 192.168.0.255)
  host  all  all 192.168.0.0/24
  
  # 특정 IP 만 허용
  host  all  all 192.168.0.100/32
```

### PostgreSQL 설정 변경 시 재시작을 해줘야 한다.

```
  # systemctl restart postgresql-13
```
