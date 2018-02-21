## Database > RDS for MySQL > Developer Guide

## Migration

* RDS는 mysqldump를 이용하여 TOAST Cloud RDS 의 외부로 데이터로 내보나거나 외부로부터 가져올 수 있습니다.
* mysqldump 유틸리티는 mysql을 설치했을 때 기본으로 제공됩니다.

### mysqldump를 이용하여 내보내기

* TOAST Cloud RDS의 인스턴스를 준비하여 사용합니다.
* 내보낼 데이터를 저장하게 될 외부 인스턴스, 혹은 로컬 클라이언트가 설치된 컴퓨터의 용량이 충분히 확보되어있는지 확인합니다.
* TOAST Cloud의 외부로 데이터를 내보내야할 경우, Floating IP를 생성하여 데이터를 내보낼 RDS 인스턴스에 연결합니다.
* 아래의 mysqldump 명령어를 통하여 외부로 데이터를 내보냅니다.

####  파일로 내보낼 경우.
```
mysqldump -h{rds_insance_floating_ip} -u{db_id} -p{db_password} --port={db_port} --single-transaction --routines --events --triggers --databases {database_name1, database_name2, ...} > {local_path_and_file_name}
```

#### TOAST Cloud RDS 외부의 mysql db로 내보낼 경우.
```
mysqldump -h{rds_insance_floating_ip} -u{db_id} -p{db_password} --port={db_port} --single-transaction --routines --events --triggers --databases {database_name1, database_name2, ...} | mysql -h{external_db_host} -u{external_db_id} -p{external_db_password} --port={external_db_port}
```

### mysqldump를 이용하여 가져오기

* 데이터를 가져올 TOAST Cloud RDS 외부의 db를 준비합니다.
* 가져올 TOAST Cloud RDS 인스턴스의 용량이 충분한지 확인합니다.
* Floating IP를 생성하여 TOAST Cloud RDS 인스턴스에 연결합니다.
* 아래의 mysqldump 명령어를 통하여 외부로부터 데이터를 가져옵니다.

```
mysqldump -h{external_db_host} -u{external_db_id} -p{external_db_password} --port={external_db_port} --single-transaction --routines --events --triggers --databases {database_name1, database_name2, ...} | mysql -h{rds_insance_floating_ip} -u{db_id} -p{db_password} --port={db_port} 
```

### 복제를 이용하여 내보내기

* 복제를 이용하여 TOAST Cloud RDS의 데이터를 외부의 DB로 내보낼 수 있습니다.
* 외부의 db 버전은 TOAST Cloud RDS의 버전과 같거나 그보다 최신 버전이어야합니다.
* 데이터를 내보낼 TOAST Cloud RDS Master 혹은 Read Only Slave 인스턴스를 준비합니다.
* Floating IP를 생성하여 데이터를 내보낼 TOAST Cloud RDS 인스턴스들에 연결합니다.
* 아래의 명령어를 통해 TOAST Cloud RDS 인스턴스로부터 데이터를 파일로 내보냅니다.
* Master RDS 인스턴스로부터 내보낼 경우.

```
mysqldump -h{rds_master_insance_floating_ip} -u{db_id} -p{db_password} --port={db_port} --single-transaction --master-data=2 --routines --events --triggers --databases {database_name1, database_name2, ...} > {local_path_and_file_name}
```

* Read Only Slave RDS 인스턴스로부터 내보낼 경우.

```
mysqldump -h{rds_read_only_slave_insance_floating_ip} -u{db_id} -p{db_password} --port={db_port} --single-transaction --dump-slave=2 --routines --events --triggers --databases {database_name1, database_name2, ...} > {local_path_and_file_name}
```

* 백업된 파일을 열어 주석에 쓰여진 MASTER_LOG_FILE 및 MASTER_LOG_POS를 따로 기록합니다.
* TOAST Cloud RDS 인스턴스로부터 데이터를 백업받을 외부 로컬 클라이언트 혹은 db가 설치된 컴퓨터의 용량이 충분한지 확인합니다.
* 외부 DB에 my.cnf (winodws의 경우 my.ini) 파일에 아래와 같은 옵션을 추가합니다.
* server-id의 경우 TOAST Cloud RDS 인스턴스의 DB Configuration 항목의 server-id와 다른 값으로 입력합니다.

```
...
[mysqld]
...
server-id={server_id}
replicate-ignore-db=rds_maintenance
...
```

* 외부 DB를 재시작합니다.
* 백업된 파일을 아래의 명령어를 통해 외부의 DB에 입력합니다.

```
mysql -h{external_db_host} -u{exteranl_db_id} -p{external_db_password} --port={exteranl_db_port} < {local_path_and_file_name}
```

* TOAST Cloud RDS 인스턴스에서 복제에 사용할 계정을 생성합니다.
* 새롭게 복제를 설정하기에 앞서 혹시 존재할 수도 있는 기존 복제 정보를 초기화하기 위하여 아래의 쿼리를 실행합니다. 이 때, RESET SLAVE를 실행할 경우 기존 복제 정보가 초기화됩니다.

```
STOP SLAVE;

RESET SLAVE;
```

* 복제에 사용할 계정 정보와 아까 따로 기록해 두었던 MASTER_LOG_FILE과 MSATER_LOG_POS를 이용하여 외부 DB에 아래와 같이 쿼리를 실행합니다.

```
CHANGE MASTER TO master_host = '{rds_master_instance_floating_ip}', master_user='{user_id_for_replication}', master_password='{password_forreplication_user}', master_port ={rds_master_instance_port}, master_log_file ='{MASTER_LOG_FILE}', master_log_pos = {MASTER_LOG_POS};

START SLAVE;
```

* 외부 db에서 TOAST Cloud RDS 인스턴스의 원본 데이터를 따라잡은 후, 외부 db에 STOP SLAVE 명령을 이용하여 복제를 종료합니다.
