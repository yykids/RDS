## Database > RDS for MySQL > 控制台使用指南

## 开始

若欲使用RDS for MysQL，应先创建DB实例。可利用如下方法创建DB实例。

* 在**Console > Database > RDS for MySQL**的**DB Instance **标签中单击左上端的**+创建**按钮，如下图所示，在页面下端出现输入界面。

![rds_01_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_01_20190723_zh.png)

* **具体设置**界面中显示的必需项目全部输入完成后，单击界面右上端的**下一步**按钮。
    * DB Instance:输入DB实例名。
    * 说明：输入DB实例的说明。
    * DB Engine:选择要创建的数据库引擎版本。
    * DB Port:输入数据库端口号。可在10000~12000之间进行设置。
    * DB User ID:创建数据库时，输入要创建的管理员账号ID。
    * DB Password:创建数据库时，输入要创建的管理员账号密码。
    * VPC Subnet:选择要创建的DB实例与要进行private network通信的Compute & Network服务的子网。
    * Floating IP:若欲与TOAST云外部网络连接，设置为使用Floating IP。
    * Flavor:选择DB实例的类型。
    * Storage类型：指定DB实例卷的类型。
        * 可选择HDD及SSD。
    * Storage:输入DB实例卷的大小。
        * 可创建为20GB~2,000GB的大小。
    * Availabillity Zone:选择要创建DB实例的区域。
    * 高可用性：创建DB实例时，在与Master不同的Availability Zone创建Candidate Master。
    * DB文件加密：加密用户数据文件及备份文件。
    * 默认警报：可登记DB实例事件中与提前定义事件相关的警报。
        * 使用默认警报时，应选择接收组。

> [参考] 若所选Compute & Network服务的VPC子网未与互联网网关连接，则无法使用浮动IP。
> [参考] VPC子网一经选择无法更改。
> [参考] Candidate Master实例必须创建于与Master不同的Availability Zone，不显示在列表中。
> [参考] 实例列表按照各实例的创建顺序排列，Candidate Master在Master的高可用性选项使用时创建，因此进行故障处理后实例的顺序可能发生更改。
> [参考] 若使用DB文件加密功能，性能会有所减少。
> [参考] 使用默认警报时，自动登记相应实例的警报，名称设置为”{实例名}-default”。登记的警报可更改及删除，应用的实例也可更改。


在**备份&Access控制**界面中指定备份信息。

![rds_02_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_02_20190723_zh.png)

* 设置自动备份及访问控制后，单击**下一步**按钮。
* 备份保存期限：若欲进行自动备份，请选择1天以上。
    若选择**无**，则不进行自动备份。
* 备份开始时间：自动备份从备份开始时间至Duration之间任意的时间开始。
    Duration指开始备份的时间。不意味着在Duration中备份结束。
* 用户访问控制：以CIDR格式输入可访问DB实例的用户。
    未注册于用户访问控制中的IP无法连接。

可在DB Configuration界面中更改设置值。

![rds_03_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_03_20190723_zh.png)

* 更改所需设置值后，单击**创建**按钮。
* 最后单击**确认**按钮，创建DB实例。
* 创建需要几到几十分钟的时间。

### 连接DB实例

选择创建的DB实例，可确认详细设置。
在实例[具体设置]的[访问信息]中可以确认可访问的域信息。
Floating IP未设置为“使用”的DB实例无法从外部访问。

1.为测试从外部连接，单击右上方的**更改**按钮。
2.将浮动IP项目修改为**使用**。
3.单击**确定**按钮，反映修改项。

![rds_04_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_04_20190723_zh.png)

设置后浮动IP生成，可确认是否能从外部连接。

![rds_05_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_05_20190723_zh.png)

以下为MySQL Workbench连接示例。

![rds_06_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_06_20190723_zh.png)

#### 限制事项

* 在用户Compute商品的实例无法访问dns服务器的网络环境下，相应实例无法通过域访问RDS实例。

## DB实例

### 高可用性

* 在不同Availability Zone创建Candidate Master，发生故障时可进行故障处理。
* 重启高可用性实例时，选择[利用故障处理重启]选项，可置换Master与Candidate Master。
* 对于使用高可用性的实例，更改部分选项时访问信息不变，但Master与Candidate Master实例可能互换。 
* 发生故障，对高可用性实例执行故障处理时，更改的新Master实例不继承原有Master实例的备份。

#### 限制事项

* 高可用性实例保障最少1次的故障处理。发生故障进行故障处理时，Candidate Master实例更改为不使用高可用性功能的一般Master。
* 更改后的新Master实例继承原Master实例访问所使用的域名。
* 并且可以重新指定高可用性选项使用。
* 执行故障处理的原Master实例的访问信息更改，转换为“中断”状态。
* 执行故障处理的原Master实例可利用实例重启功能尝试重新驱动，但由于故障导致的数据损坏等原因，有可能无法重新驱动或无法正常运行。
* Read Only Slave实例不提供高可用性功能。
* 重启使用高可用性功能的实例或更改选项期间，该实例无法进行Read Only Slave操作。
* 高可用性功能基于域，因此若为用户Compute商品的实例无法访问dns服务器的网络环境，则相应实例无法通过域访问RDS实例，发生故障处理时，无法正常访问。

### 实例类型

* 可利用TOAST Compute & Network服务提供的所有类型来创建DB实例。

### 备份


* 在RDS中执行所有备份后，创建的备份上传至自主Object Storage保管。
* 仅限自动备份，免费提供相当于原始实例数据卷大小的备份容量。
* 若不希望产生额外的费用，应调节备份周期。
* 备份执行期间，性能有可能降低。
* 若不希望影响服务，最好在服务负载较低的时间备份。
* TOAST RDS支持时间点还原。
    若二进制日志（binary log）大小和存储周期过短，则可能难以还原至所需时间点。
* 正在还原的DB实例无法备份。

#### 自动备份

* 若DB实例的备份周期设置为1天以上，则启动自动备份。
    * 若将备份周期从1天以上更改为无，则所有自动备份立即从服务器上删除。
    * 删除的备份无法还原。
* 按照设置的备份周期保留备份文件。
* 自动备份从备份开始时间至Duration之间任意的时间开始。
* Duration指开始备份的时间。不意味着在Duration中完成备份。
    即使在Duration中无法完成备份，备份也不会结束。
* 自动备份在删除所有原始实例时一同删除。

#### 手动备份

* 除自动备份外，可随时进行手动备份。
* 手动备份在明确指示不删除的情况下不会被删除。

### 还原

* 利用保存的备份可将DB实例还原到需要的时间点。
* 还原时，不更改原始DB实例，创建新的DB实例。
* 若备份存储在Object Storage中，则需要更多时间。
* 不可使用正在备份的DB实例来进行还原。

>[参考] 还原进行过程中，Object Storage使用量可能达到与Binary Log文件相同的大小。
>[参考] 无二进制日志文件时，无法恢复时间。

### 复制

* 若欲提高读取性能，可以创建支持MySQL的Read Only Slave。
* 若欲创建Read Only Slave，选择原始DB实例后单击**附加功能>创建副本**。

![rds_07_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_07_20190723_zh.png)

* 输入创建副本所需的设置，单击**复制**按钮，创建副本。
* 建议创建为与原始DB实例相同的类型或更高的类型，创建为较低的类型时，有可能发生复制延迟。
* 创建副本时，原始DB实例的I/O性能可能比平时有所降低。
* 根据原始DB实例的大小，创建副本的时间可能有所延长。

>[参考] 复制进行过程中，Object Storage使用量可能达到与二进制日志文件相同的大小。
>[参考] 复制完成后，Read Only Slave的规则添加至Master实例的访问规则(access rule)项目。 

#### 限制事项

* 一个原始实例最多可以创建5个副本。
* 副本无法创建副本。

### 升级

* 断开复制关系并从Read Only Slave更改为Master，称为升级。
* 升级的副本无法再自动反映DB实例的修改事项。
* 升级的副本作为独立的DB实例运行。
* 若欲升级的副本与原始DB实例之间存在复制延迟，则该延迟消失前不会升级。

### 确保容量

*  删除DB实例的资源，可确保磁盘容量。

#### 删除二进制日志

![rds_08_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_08_20190723_zh.png)

* 删除二进制日志文件，确保磁盘空间。

>[注意] 所选对象二进制日志文件与之前创建的二进制文件全部删除。
>[注意] 删除二进制日志文件时，根据删除的二进制日志文件，也可能无法恢复至特定时间。 
>[注意] 二进制日志文件全部删除时，无法使用时间恢复。

### 扩展存储

![rds_09_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_09_20190723_zh.png)

* 扩展DB实例的存储大小。
* 若存在Read Only Slave，则一同扩展为与Master相同的存储大小。
* 对象DB实例重启。

### DB文件加密

* 加密存储用户数据的数据库文件及备份文件。

> [参考] 实时执行加密，因此DB实例的性能会有所减少。

#### 限制事项

* 从不使用DB文件加密功能的实例恢复或复制时，无法打开DB文件加密功能。
* 从使用DB文件加密功能的实例恢复或复制时，无法关闭DB文件加密功能。

## 监控

* RDS定期收集DB运营及使用所需的监控项目，并以图表显示。
* 若欲查看特定DB实例的监控项目，在**DB Instance**列表中选择特定DB实例后，选择**Monitoring**标签。

![rds_10_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_10_20190723_zh.png)

* 若欲查看整体DB实例的监控项目，在**Monitoring**标签中选择所需DB实例后，单击**添加**按钮。
* 若更改图表范围、间距、种类及项目，更改的事项影响添加的所有DB实例。

![rds_11_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_11_20190723_zh.png)

* 可以使用能够轻松调整图表范围的按钮。
* 每按一次1小时、6小时等按钮，以当前时间为准自动计算from~to并更新。
<br/>
* 根据图表范围，可选图表的间距有所不同。
    * 2小时以内：1分钟、10分钟
    * 12小时以内：10分钟、1小时
    * 4天以内：1小时、6小时
    * 2周以内：6小时、一天
    * 其他：一天
* 图表类型支持最大值和平均值。

>[参考] 各RDS DB实例的监控数据临时保存在用户DB实例的名为“rds_maintenance”的数据库中，然后删除。因此，即使创建后未进行任何操作的实例，也会显示几个监控项目规则移动的图表状态。 
>[参考] 若操作rds_maintenance database的数据，可能会收集到错误的监控数据。

### 监控项目

* RDS支持的监控项目如下。

![rds_12_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_12_20190723_zh.png)

### 日志文件

* 无需访问DB实例，即可轻松查看或下载日志文件。
* 选择**DB Instance**后单击**Events & Log**标签，可查看error.log, slow_query.log, general.log文件。

![rds_13_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_13_20190723_zh.png)

* 但，应在**DB Configuration**中设置为保留该日志。
* 单击**查看**按钮，可在新窗口中确认日志文件。
* 可按照在日志长度中输入的行数查看，可从最后查看1MB大小的日志。

![rds_14_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_14_20190723_zh.png)

* 若欲查看整个日志文件，应单击**下载**按钮，直接下载日志文件。

![rds_15_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_15_20190723_zh.png)

* 单击**下载**按钮，可打开新窗口。
* 单击**加载**按钮后稍待片刻，**下载**按钮激活，可进行下载。
* 日志文件临时上传到Object Storage，最长保留5分钟以供下载。
>[参考] 可能收取上传到Object Storage至删除的5分钟内的Object Storage使用费用。


## 事件

* RDS自动保留DB实例中发生的有意义的事件。
* 若欲查看特定DB实例中发生的事件，选择DB实例后，可在**具体设置**界面的**Event & Log**标签中确认。
* 若欲一次性查看DB实例中发生的事件，可跳转至**Event**标签确认。

![rds_16_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_16_20190723_zh.png)

* **类型**指的是在何种资源中发生的事件。
    * INSTANCE:与DB实例相关的事件。
    * BACKUP:与备份相关的事件。
* **Identifier**指发生事件的资源。
    * 若事件类型为INSTANCE，则显示DB实例名。
    * 若事件类型为BACKUP，则显示备份ID。

## Notification

RDS可将在所需资源中发生的特定事件警报传达给接收组。

1.若欲设置所需警报，在**Notification**标签中单击**创建**按钮。
2.输入需要的警报名，在**警报设置**中选择要设置的时间和资源。
   设置后单击**添加**按钮。
3.若欲创建接收警报的接收组，单击**创建**按钮。
4.[接收对象] 弹出窗口后，输入接收组名称。在项目成员中单击要接收警报信息的成员，选定为接收对象项目成员。
5.在接收对象窗口中单击**创建**按钮。
6.警报设置完成后，单击**创建**按钮。 

![rds_17_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_17_20190723_zh.png)

若满足设置的条件，可通过接收对象中输入的邮箱地址和电话接收警报。

![rds_18_20190723](https://static.toastoven.net/prod_rds/19.07.23/rds_18_20190723_zh.png)

>[参考] 若在接收组中不勾选所需对象的复选框，则不发送邮件或SMS。

## 부록1. 하이퍼바이저 점검을 위한 DB 인스턴스 마이그레이션 가이드

TOAST는 주기적으로 DB 인스턴스의 하이퍼바이저 소프트웨어를 업데이트하여 보안과 안정성을 향상시키고 있습니다.
점검 대상 하이퍼바이저에서 구동 중인 DB 인스턴스는 마이그레이션을 통해 점검이 완료된 하이퍼바이저로 이동해야 합니다.

DB 인스턴스 마이그레이션은 TOAST 콘솔에서 시작할 수 있습니다.
DB 구성에 따라 특정 DB 인스턴스를 선택하여 마이그레이션 시, 연관된 DB 인스턴스(예를 들면 Slave 인스턴스)도 점검 대상이면 같이 마이그레이션을 진행합니다.
아래 가이드에 따라 콘솔에 있는 마이그레이션 기능을 이용하시기 바랍니다.
점검 대상으로 지정된 DB 인스턴스가 있는 프로젝트로 이동합니다.

### 1. 점검 대상 DB 인스턴스를 확인 합니다.

이름 옆에 마이그레이션 버튼이 있는 DB 인스턴스가 점검 대상 인스턴스입니다.

![rds_planed_migration_0](https://static.toastoven.net/prod_rds/planned_migration_alarm/image0_zh.png)

마이그레이션 버튼 위에 마우스 커서를 올리면 자세한 점검 일정을 확인할 수 있습니다.

![rds_planed_migration_1](https://static.toastoven.net/prod_rds/planned_migration_alarm/image1_zh.png)

### 2. 점검 대상 DB 인스턴스에 접속 중인 응용 프로그램을 종료해야 합니다.

DB에 연결된 서비스에 영향을 주지 않도록 적절한 조치를 취하시길 바랍니다.
서비스에 영향을 줄 수밖에 없을 때는 TOAST 고객 센터로 연락해 주시면 적합한 조치를 안내해 드리겠습니다.

### 3. 점검 대상 DB 인스턴스를 선택하고 마이그레이션 버튼을 클릭한 후 DB 인스턴스 마이그레이션 확인을 묻는 창이 나타나면 확인 버튼을 클릭합니다.

![rds_planed_migration_2](https://static.toastoven.net/prod_rds/planned_migration_alarm/image2_zh.png)

### 4. DB 인스턴스 마이그레이션이 끝날 때까지 대기합니다.

DB 인스턴스 상태가 변경되지 않는다면 '새로 고침'을 해보시기 바랍니다.

![rds_planed_migration_3](https://static.toastoven.net/prod_rds/planned_migration_alarm/image3_zh.png)

DB 인스턴스가 마이그레이션되는 동안에는 아무런 조작을 할 수 없습니다.
DB 인스턴스 마이그레이션이 정상적으로 완료되지 않으면 자동으로 관리자에게 보고되며, TOAST에서 별도로 연락을 드립니다.