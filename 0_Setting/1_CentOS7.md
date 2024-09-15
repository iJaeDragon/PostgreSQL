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
  sudo yum -y install postgresql13 postgresql13-server
```

<details>
<summary>접기/펼치기</summary>

## 에러가 나는경우

```
  date
```

date 커맨드로 현재 시간을 확인하고 실제 시간과 차이가 많이 난다면 현재 시간으로 조정

```
  timedatectl set-time "2024-09-15 11:16:52"
```
</details>

### PostgreSQL 초기화
