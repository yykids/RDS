## Database > RDS for MySQL > 콘솔 사용 가이드

## 간단히 시작하기

![[그림 1] 초기 화면](http://static.toastoven.net/prod_rds/gs_001.png)
<center>[그림 1] 초기 화면</center>

* 가장 먼저 해야 할 일은 DB 인스턴스를 생성하는 일입니다.
* <b>[그림 1]</b> 의 좌측 상단 생성 버튼을 누르시면 <b>[그림 2]</b> 와 같이 페이지 하단에 생성 레이어가 표시됩니다.

![[그림 2] DB 인스턴스 - 상세 설정 화면](http://static.toastoven.net/prod_rds/gs_002.png)
<center>[그림 2] DB 인스턴스 - 상세 설정 화면</center>

* 설정 레이어에 표시된 필수 항목을 모두 입력하신 후, 레이어 우측 상단의 다음 버튼을 눌러주세요.
    * DB Instance : DB 인스턴스 이름을 입력합니다.
    * 설명 : DB 인스턴스의 설명을 입력합니다.
    * DB Engine : 생성 하시고자 하시는 Database Engine 버전을 선택합니다.
        * 현재는 5.6.33 버전만 지원합니다.
    * DB Port : Database 의 Port 번호를 입력합니다.
        * 10000 ~ 12000 사이로 설정할 수 있습니다.
    * DB ID : Database 생성 시 만들어질 관리자 계정 아이디를 입력합니다.
    * DB Password : Database 생성 시 만들어질 관리자 계정 비밀번호를 입력합니다.
    * 네트워크 : DB 인스턴스와 네트워크 통신을 하시길 원하시는 Compute & Network 상품의 subnet 을 선택합니다.
    * Floating IP : 토스트클라우드 외부 네트워크와 연결을 원하실 경우 Floating IP 를 사용으로 설정합니다.
    * Flavor : DB 인스턴스의 사양을 선택합니다.
    * Storage : DB 인스턴스 볼륨의 크기를 입력합니다.
        * 20 GB ~ 600 GB 크기로 생성 할 수 있습니다.
    * Availabillity Zone : DB 인스턴스가 생성 될 Zone 을 선택합니다.

![[그림 3] DB 인스턴스 - 백업 & Access 제어 화면](http://static.toastoven.net/prod_rds/gs_003.png)
<center>[그림 3] DB 인스턴스 - 백업 & Access 제어 화면</center>

* 자동 백업 및 접근 제어 설정을 한 후, 다음 버튼을 누릅니다.
* 자동 백업을 하려면 백업 보관 기간을 1일 이상 선택합니다.
    * 없음으로 선택 시, 자동으로 백업을 하지 않습니다.
    * 자동 백업은 백업 시작 시각 부터 Duration 사이 중 임의의 시점에 시작됩니다.
    * Duration 은 백업이 시작되는 시각을 의미합니다.
        * Duration 안에 백업이 종료되는 것을 의미 하지 않습니다.
* 사용자 접근 제어에 DB 인스턴스에 접근 가능한 사용자를 CIDR 형식으로 입력합니다.
    * 사용자 접근 제어에 등록되지 않은 IP 는 접속이 불가능합니다.

![[그림 4] DB 인스턴스 - DB Configuration](http://static.toastoven.net/prod_rds/gs_004.png)
<center>[그림 4] DB 인스턴스 - DB Configuration</center>

* 변경 하고자 하는 설정 값을 변경 후, 생성 버튼을 누릅니다.

![[그림 5] DB 인스턴스 - 생성 확인](http://static.toastoven.net/prod_rds/gs_005.png)
<center>[그림 5] DB 인스턴스 - 생성 확인</center>

* 최종적으로 확인 버튼을 누르면, DB 인스턴스가 생성됩니다.
* 생성되기 까지 수분에서 수십분이 소요 됩니다.

![[그림 6] DB 인스턴스 - 목록 조회 (생성 중)](http://static.toastoven.net/prod_rds/gs_006.png)
<center>[그림 6] DB 인스턴스 - 목록 조회 (생성 중)</center>
![[그림 7] DB 인스턴스 - 목록 조회 (생성 완료)](http://static.toastoven.net/prod_rds/gs_007.png)
<center>[그림 7] DB 인스턴스 - 목록 조회 (생성 완료)</center>

* DB 인스턴스의 생성이 완료 되면 <b>[그림 7]</b> 처럼 상태가 정상으로 변하게 됩니다.

### DB 인스턴스 접속

![[그림 8] DB 인스턴스 - 상세 보기](http://static.toastoven.net/prod_rds/gs_008.png)
<center>[그림 8] DB 인스턴스 - 상세 보기</center>

* 생성된 DB 인스턴스를 선택하면 상세 설정을 확인 할 수 있습니다.
* Floating IP 가 연결되지 않은 DB 인스턴스는 외부에서 접근이 불가능합니다.
* 외부에서 접속을 테스트하기 위해 우측 상단의 변경 버튼을 누릅니다.

![[그림 9] DB 인스턴스 - Floating IP 변경](http://static.toastoven.net/prod_rds/gs_009.png)
<center>[그림 9] DB 인스턴스 - Floating IP 변경</center>

* Floating IP 항목을 사용함으로 수정합니다.
* 확인 버튼을 눌러 수정 사항을 반영합니다.

![[그림 10] MySQL Workbench 접속](http://static.toastoven.net/prod_rds/gs_010.png)
<center>[그림 10] MySQL Workbench 접속</center>

## DB 인스턴스

### Flavor

* TOAST Cloud Compute & Network 상품에서 제공하는 모든 사양으로 DB 인스턴스를 생성 할 수 있습니다.

### 백업

* RDS 에서는 데이터 볼륨 크기와 동일한 크기의 백업 볼륨을 기본 제공합니다.
* 백업 볼륨의 크기가 가득차면, 오래된 백업 부터 순차적으로 Object Storage 로 업로드 됩니다.
* Object Storage 에 저장된 백업은 용량에 따라 별도 과금됩니다.
* 별도의 과금을 원하지 않으면, 백업 주기를 적절하게 조절해야 합니다.
* 백업이 실행되는 동안에는 백업으로 인한 성능 저하가 발생 할 수 있습니다.
* 서비스에 영향을 주지 않기 위해서, 서비스의 부하가 적은 시간에 백업을 하는 것이 유리합니다.
* TOAST Cloud RDS 는 시점 복원을 지원합니다.
    * bin log 사이즈와 보관 주기가 너무 짧은 경우 원하는 시점으로 복원이 어려울 수 있습니다.
* 복원 중인 DB 인스턴스를 백업 할 수 없습니다.

#### 자동 백업

* DB 인스턴스의 백업 주기를 1일 이상으로 설정 시, 자동 백업이 활성화 됩니다.
    * 백업 주기를 1일 이상에서 없음으로 변경하는 즉시 모든 자동 백업은 서버에서 그 즉시 삭제됩니다.
    * 삭제된 백업은 복원 할 수 없습니다.
* 설정된 백업 주기 만큼 백업 파일을 유지합니다.
* 자동 백업은 백업 시작 시각 부터 Duration 사이 중 임의의 시점에 시작됩니다.
* Duration 은 백업이 시작되는 시각을 의미합니다.
    * Duration 안에 백업을 완료하는 의미가 아닙니다.
    * Duration 안에 백업을 완료하지 못하더라도 백업은 종료되지 않습니다.

#### 수동 백업

* 자동 백업 이외에 언제든지 수동으로 백업을 할 수 있습니다.
* 수동 백업은 모두 Object Storage 에 저장되며, 명시적으로 삭제 하지 않는한 지워지지 않습니다.

### 복원

* 보관된 백업을 이용하여 원하는 시점으로 DB 인스턴스를 복원 할 수 있습니다.
* 복원 시, 원본 DB 인스턴스를 변경하지 않고 새로운 DB 인스턴스를 생성합니다.
* 백업의 저장 위치가 Object Storage 에 있을 경우, 시간이 더 소요됩니다.
* 백업 중인 DB 인스턴스를 이용해서 복원을 할 수 없습니다.
> [참고] 복원이 진행되는 동안 bin log file의 사이즈만큼의 Object Storage 사용량이 발생할 수 있습니다.

### 복제

* 읽기 성능을 높이기 위해서 MySQL 이 지원하는 Read Only Slave 를 만들 수 있습니다.
* Read Only Slave 를 만들기 위해서 원본 DB 인스턴스를 선택한 후 추가기능 > 복제본 생성을 누릅니다.

![[그림 1] 복제 - 생성](http://static.toastoven.net/prod_rds/rp_001.png)
<center>[그림 1] 복제 - 생성</center>

* 복제본 생성을 위한 설정을 입력한 후, 복제 버튼을 누르면 복제본이 생성됩니다.
* 원본 DB 인스턴스와 동일한 사양 혹은 더 높은 사양으로 만드는 것을 권장하며, 낮은 사양으로 생성 시 복제 지연이 발생 할 수 있습니다.
* 복재본 생성시, 원본 DB 인스턴스의 I/O 성능이 평소보다 낮아 질 수 있습니다.
* 원본 DB 인스턴스의 크기에 비례하여 복제본 생성 시간이 늘어 날 수 있습니다.
> [참고] 복제가 진행되는 동안 bin log file의 사이즈만큼의 Object Storage 사용량이 발생할 수 있습니다.

#### 제약 사항

* 하나의 원본 인스턴스는 최대 5개의 복재 본을 만들 수 있습니다.
* 복제본의 복제본을 만들 수 없습니다.

### 승격

* 복제 관계를 끊고 Read Only Slave 에서 Master 로 변경하는 것을 승격이라 부릅니다.
* 승격된 복제본은 더이상 원본 DB 인스턴스의 수정사항을 자동으로 반영하지 않습니다.
* 승격된 복제본은 독립된 DB 인스턴스로서 동작하게 됩니다.
* 승격 하려는 복제본과 원본 DB 인스턴스 사이에 복제 지연이 있는 경우, 해당 지연이 없어 질 때까지, 승격되지 않습니다.

## Networks

* Network 상품의 사용자 VPC를 RDS상품에 연결하여, RDS의 DB 인스턴스가 사용자의 VPC를 사용하는 인스턴스와 통신할 수 있습니다.
* Networks 탭을 누르면 연결된 사용자의 VPC 리스트를 볼 수 있습니다.

![[그림 1] 네트워크 화면](http://static.toastoven.net/prod_rds/nw_001.png)
<center>[그림 1] 네트워크 화면</center>

* 우선 Network 상품을 통해 연결하고자 하는 사용자의 VPC와 서브넷을 생성하고하고 해당 원하는 VPC에 원하는 서브넷을 생성합니다.
* Network 상품이 Enable 되어있지 않으면 연결 가능한 VPC 항목이 표시되지 않습니다.

![[그림 2] 네트워크 화면](http://static.toastoven.net/prod_rds/nw_002-1.png)
<center>[그림 2] VPC의 Management 탭 화면</center>
![[그림 3] 네트워크 화면](http://static.toastoven.net/prod_rds/nw_002-2.png)
<center>[그림 3] VPC의 Subnets 탭 화면</center>

> [참고] Network 상품의 VPC와 서브넷을 생성하여도, 해당 VPC를 사용하는 Instance가 없을 경우에는 연결 가능한 VPC 목록에서 생성한 VPC가 나타나지 않습니다.
> [참고] 서브넷을 생성하지 않고 VPC만 생성할 경우 연결을 할 수 없습니다.

* 연결하기를 원하는 네트워크를 선택하고 설명을 기입한 후 확인을 누릅니다.

![[그림 4] 네트워크 화면](http://static.toastoven.net/prod_rds/nw_003-1.png)
![[그림 5] 네트워크 화면](http://static.toastoven.net/prod_rds/nw_003-2.png)
<center>[그림 4] VPC 연결 생성 화면</center>

![[그림 6] 네트워크 화면](http://static.toastoven.net/prod_rds/nw_004.png)
<center>[그림 5] VPC 연결 완료 화면</center>

* 원하는 VPC 연결을 선택한 후 삭제할 수 있습니다.

![[그림 7] 네트워크 화면](http://static.toastoven.net/prod_rds/nw_005.png)
<center>[그림 6] VPC 연결 삭제 화면</center>

## Monitoring

* RDS 는 DB 운영 및 사용에 필요한 모니터링 항목을 주기적으로 수집하고, 차트로 보여줍니다.
* 특정 DB 인스턴스의 모니터링 항목이 보고 싶을 경우, DB 인스턴스 목록에서 특정 DB 인스턴스를 선택 한 후, Monitoring 탭을 선택합니다.

![[그림 1] 모니터링 - 특정 DB 인스턴스](http://static.toastoven.net/prod_rds/mt_001.png)
<center>[그림 1] 모니터링 - 특정 DB 인스턴스</center>

* 전체 DB 인스턴스의 모니터링 항목이 보고 싶은 경우에는, Monitoring 탭으로 들어가신 후 보고자 하는 DB 인스턴스를 선택 후 추가 버튼을 누릅니다.
* 차트 범위, 간격, 종류 및 항목을 변경 시, 변경 사항이 추가된 모든 DB 인스턴스에 영향을 줍니다.

![[그림 2] 모니터링 - 여러 DB 인스턴스](http://static.toastoven.net/prod_rds/mt_002.png)
<center>[그림 2] 모니터링 - 여러 DB 인스턴스</center>

* 차트의 범위를 쉽게 조정 할 수 있게 유틸성 버튼을 제공합니다.
* 1시간, 6시간 등의 버튼을 누를 때마다, 현재 시각을 기준으로 자동으로 from ~ to 를 계산하여 갱신합니다.

![[그림 3] 모니터링 - 차트 범위 조정 버튼](http://static.toastoven.net/prod_rds/mt_003.png)
<center>[그림 3] 모니터링 - 차트 범위 조정 버튼</center>

* 차트 범위에 따라 선택 할 수 있는 차트 간격이 달라집니다.
    * 2시간 이내 : 1분, 10분
    * 12시간 이내 : 10분, 1시간
    * 4일 이내 : 1시간, 6시간
    * 2주 이내 : 6시간, 하루
    * 그외 : 하루
* 차트 종류는 최대값과 평균값을 지원합니다.

![[그림 4] 모니터링 - 차트 간격](http://static.toastoven.net/prod_rds/mt_004.png)
<center>[그림 4] 모니터링 - 차트 간격</center>

> [참고] RDS DB 인스턴스별 모니터링 데이터는 사용자 DB 인스턴스의 'rds_maintenance'라는 database에 임시 저장 및 삭제됩니다. 따라서 생성한 뒤 아무 동작도 하지 않은 인스턴스임에도 몇몇 모니터링 항목들이 규칙적으로 움직이는 그래프 형태를 가질 수 있습니다. 
> [참고] 만약 rds_maintenance database의 데이터를 조작할 경우, 정확하지 않은 모니터링 데이터가 수집될 수 있습니다.

### 항목

* RDS 에서 지원하는 모니터링 항목은 다음과 같습니다.

![[그림 5] 모니터링 - 차트 항목](http://static.toastoven.net/prod_rds/mt_005.png)
<center>[그림 5] 모니터링 - 차트 항목</center>

### 로그 파일

* DB 인스턴스에 접속하지 않고 편하게 로그파일을 보거나 다운로드 받을 수 있습니다.
* DB 인스턴스를 선택한 후, Event & Log 탭을 누르면 error.log, slow_query.log, general.log 파일을 볼 수 있습니다.

![[그림 6] 이벤트 &amp; 로그](http://static.toastoven.net/prod_rds/mt_006.png)
<center>[그림 6] 이벤트 &amp; 로그</center>

* 단 반드시 DB Configuration 에서 해당 로그를 남기도록 설정을 해야 합니다.
* 보기 버튼을 누르면 팝업이 열리며, 로그 파일을 볼 수 있습니다.
* 로그 길이에 입력 된 라인수 만큼 볼 수 있으며, 50 ~ 1000 라인까지 볼 수 있습니다.

![[그림 7] 이벤트 &amp; 로그 - error.log 파일 로그](http://static.toastoven.net/prod_rds/mt_007.png)
<center>[그림 7] 이벤트 &amp; 로그 - error.log 파일 로그</center>

* 로그 파일 전체를 보고 싶다면, 다운로드 버튼을 눌러 직접 파일을 다운로드 받아야 합니다.

![[그림 8] 이벤트 &amp; 로그 - error.log 파일 가져오기](http://static.toastoven.net/prod_rds/mt_008-1.png)
![[그림 8] 이벤트 &amp; 로그 - error.log 파일 가져오기](http://static.toastoven.net/prod_rds/mt_008-2.png)
<center>[그림 8] 이벤트 &amp; 로그 - error.log 파일 가져오기</center>

* 다운로드 버튼을 누르면 <b>[그림 8]</b> 처럼 팝업이 나타납니다.
* 가져오기 버튼을 누른후 잠시 기다리시면, <b>[그림 9]</b> 처럼 다운로드 가능한 상태가 됩니다.
* 로그 파일은 임시 Object Storage 에 업로드 되어 최대 5분 동안 다운로드 할 수 있도록 유지됩니다.
> [참고] Object Storage에 업로드 되고 삭제되는 5분간 Object Storage 사용 요금이 청구될 수 있습니다.

![[그림 9] 이벤트 &amp; 로그 -  error.log 파일 다운로드](http://static.toastoven.net/prod_rds/mt_009.png)
<center>[그림 9] 이벤트 &amp; 로그 -  error.log 파일 다운로드</center>

## Event

* RDS 는 DB 인스턴스에서 발생한 의미 있는 이벤트를 자동으로 남깁니다.
* 특정 DB 인스턴스에서 발생한 이벤트를 보고 싶으면, DB 인스턴스를 선택한 후, 상세 설정 레이어의 Event & Log 탭에서 확인 할 수 있습니다.
* 내가 가진 모든 DB 인스턴스에서 발생한 이벤트를 한꺼번에 보려면, Events 탭으로 이동하여 조회 할 수 있습니다.

![[그림 1] 이벤트 &amp; 로그 -  목록 조회](http://static.toastoven.net/prod_rds/ev_001.png)
<center>[그림 1] 이벤트 &amp; 로그 -  목록 조회</center>

* 이벤트 타입은 어떤 리소스에서 발생한 이벤트인지를 지칭합니다.
    * INSTANCE : DB 인스턴스와 관련된 이벤트 입니다.
    * BACKUP : 백업과 관련된 이벤트 입니다.
* Identifier 는 이벤트가 발생한 리소스를 지칭합니다.
    * 이벤트 타입이 INSTANCE 일 경우 DB 인스턴스 이름이 표시됩니다.
    * 이벤트 타입이 BACKUP일 경우 백업 ID가 표시됩니다.

	
## Notification

* RDS 는 원하는 리소스에서 발생하는 특정 이벤트에 대한 Notification을 수신그룹에 전달할 수 있습니다.
* 원하는 Notification을 설정하기 위하여 Notification 탭을 선택한 후, 생성 버튼을 클릭합니다.

![[그림 1] Notification 리스트 - 생성](http://static.toastoven.net/prod_rds/nt_001.png)
<center>[그림 1] Notification - 생성</center>

* 원하는 Notification의 이름을 입력하고, 알림 설정을 통해 설정하고자하는 이벤트와 리소스를 선택합니다.
* 수신그룹 항목에서 원하는 수신그룹을 체크박스를 통하여 선택하거나 혹은 생성버튼을 통하여 수신그룹을 새롭게 지정합니다.
* 생성 버튼을 클릭하여 Notificaion 생성을 완료합니다.

> [참고] 수신그룹에서 원하는 대상에 체크박스를 선택하지 않으면 메일이나 SNS가 전달되지 않습니다.
