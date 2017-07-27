## Upcoming Products > RDS > Getting Started

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
    * Floating IP : 토스트클라우드 외부 네트워크와 연결을 원하실 경우 Floating IP 를 선택합니다.
        * 생성하신 Floating IP 가 없으시면 바로 생성이 가능합니다.
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

* DB 인스턴스의 생성이 완료 되면 [그림 7] 처럼 상태가 정상으로 변하게 됩니다.

![[그림 8] DB 인스턴스 - 상세 보기](http://static.toastoven.net/prod_rds/gs_008.png)
<center>[그림 8] DB 인스턴스 - 상세 보기</center>

* 생성된 DB 인스턴스를 선택하면 상세 설정을 확인 할 수 있습니다.
* Floating IP 가 연결되지 않은 DB 인스턴스는 외부에서 접근이 불가능합니다.
* 외부에서 접속을 테스트하기 위해 우측 상단의 변경 버튼을 누릅니다.

![[그림 9] DB 인스턴스 - Floating IP 생성 팝업](http://static.toastoven.net/prod_rds/gs_009.png)
<center>[그림 9] DB 인스턴스 - Floating IP 생성 팝업</center>
![[그림 10] DB 인스턴스 - Floating IP 생성 후](http://static.toastoven.net/prod_rds/gs_010.png)
<center>[그림 10] DB 인스턴스 - Floating IP 생성 후</center>

* 생성 버튼을 눌러 신규 Floating IP 를 생성합니다.
* 확인 버튼을 눌러 수정 사항을 반영합니다.

![[그림 11] MySQL Workbench 접속](http://static.toastoven.net/prod_rds/gs_011.png)
<center>[그림 11] MySQL Workbench 접속</center>