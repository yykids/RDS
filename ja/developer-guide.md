## Database > RDS for MySQL > 開発者ガイド

## マイグレーション

mysqldumpを利用してTOAST RDSの外部にデータでエクスポートしたり、外部からデータをインポートすることができます。mysqldumpユーティリティはmysqlをインストールした時、デフォルトで提供されます。

### mysqldumpを利用してエクスポート

* TOAST RDSのインスタンスを準備します。
* エクスポートするデータを保存する外部インスタンス、またはローカルクライアントがインストールされたコンピュータの容量が十分にあるか確認します。
* TOASTの外部にデータをエクスポートする必要がある時、Floating IPを作成してデータをエクスポートするRDSインスタンスに接続します。

下記のmysqldumpコマンドを使用して外部にデータをエクスポートします。

#### ファイルでエクスポートする場合
```
mysqldump -h{rds_insance_floating_ip} -u{db_id} -p{db_password} --port={db_port} --single-transaction --routines --events --triggers --databases {database_name1, database_name2, ...} > {local_path_and_file_name}
```

#### TOAST RDS外部のmysql dbにエクスポートする場合
```
mysqldump -h{rds_insance_floating_ip} -u{db_id} -p{db_password} --port={db_port} --single-transaction --routines --events --triggers --databases {database_name1, database_name2, ...} | mysql -h{external_db_host} -u{external_db_id} -p{external_db_password} --port={external_db_port}
```

### mysqldumpを利用してインポート

* データをインポートするTOAST RDS外部のDBを準備します。
* インポートするTOAST RDSインスタンスの容量が十分にあるか確認します。
* Floating IPを作成してTOAST RDSインスタンスに接続します。
* 下記のmysqldumpコマンドを使用して外部からデータをインポートします。

```
mysqldump -h{external_db_host} -u{external_db_id} -p{external_db_password} --port={external_db_port} --single-transaction --routines --events --triggers --databases {database_name1, database_name2, ...} | mysql -h{rds_insance_floating_ip} -u{db_id} -p{db_password} --port={db_port} 
```

### コピーを利用してエクスポート

* コピーを利用してTOAST RDSのデータを外部DBにエクスポートできます。
* 外部DBバージョンはTOAST RDSのバージョンと同じか、それより新しいバージョンでなければいけません。
* データをエクスポートするTOAST RDS MasterまたはRead Only Slaveインスタンスを準備します。
* Floating IPを作成して、データをエクスポートするTOAST RDSインスタンスに接続します。
* 下記のコマンドを使用してTOAST RDSインスタンスからデータをファイルでエクスポートします。

#### Master RDSインスタンスからエクスポートする場合

```
mysqldump -h{rds_master_insance_floating_ip} -u{db_id} -p{db_password} --port={db_port} --single-transaction --master-data=2 --routines --events --triggers --databases {database_name1, database_name2, ...} > {local_path_and_file_name}
```

#### Read Only Slave RDSインスタンスからエクスポートする場合

```
mysqldump -h{rds_read_only_slave_insance_floating_ip} -u{db_id} -p{db_password} --port={db_port} --single-transaction --dump-slave=2 --routines --events --triggers --databases {database_name1, database_name2, ...} > {local_path_and_file_name}
```

* バックアップされたファイルを開き、コメントに書かれたMASTER_LOG_FILEおよびMASTER_LOG_POSを別途記録します。
* TOAST RDSインスタンスからデータをバックアップする外部ローカルクライアント、またはDBがインストールされたコンピュータの容量が十分にあるか確認します。
* 外部DBのmy.cnf (Winodwsの場合my.ini)ファイルに下記のようなオプションを追加します。
* server-idの場合、TOAST RDSインスタンスのDB Configuration項目のserver-idと異なる値を入力します。

```
...
[mysqld]
...
server-id={server_id}
replicate-ignore-db=rds_maintenance
...
```

* 外部DBを再起動します。
* バックアップされたファイルを下記のコマンドを使用して外部DBに入力します。

```
mysql -h{external_db_host} -u{exteranl_db_id} -p{external_db_password} --port={exteranl_db_port} < {local_path_and_file_name}
```

* TOAST RDSインスタンスでコピーに使用するアカウントを作成します。
* 新規コピーを設定する前に、もしかするとあるかもしれない既存コピー情報を初期化するには、下記のクエリーを実行します。この時、RESET SLAVEを実行すると既存コピー情報が初期化されます。

```
STOP SLAVE;

RESET SLAVE;
```

* コピーに使用するアカウント情報と、別途記録しておいたMASTER_LOG_FILEとMASTER_LOG_POSを利用して、外部DBに下記のようにクエリーを実行します。

```
CHANGE MASTER TO master_host = '{rds_master_instance_floating_ip}', master_user='{user_id_for_replication}', master_password='{password_forreplication_user}', master_port ={rds_master_instance_port}, master_log_file ='{MASTER_LOG_FILE}', master_log_pos = {MASTER_LOG_POS};

START SLAVE;
```

* 外部DBでTOAST RDSインスタンスの原本データのコピーが完了した後、外部DBにSTOP SLAVEコマンドを利用してコピーを終了します。