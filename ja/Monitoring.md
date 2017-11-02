## Upcoming Products > RDS > Monitoring

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
* 로그 파일은 임시 Object Storage 에 업로드 되어 최대 5분 동안 유지됩니다.

![[그림 9] 이벤트 &amp; 로그 -  error.log 파일 다운로드](http://static.toastoven.net/prod_rds/mt_009.png)
<center>[그림 9] 이벤트 &amp; 로그 -  error.log 파일 다운로드</center>

### 이벤트 로그

* RDS 는 DB 인스턴스에서 발생한 의미 있는 이벤트를 자동으로 남깁니다.
* 특정 DB 인스턴스에서 발생한 이벤트를 보고 싶으면, DB 인스턴스를 선택한 후, 상세 설정 레이어의 Event & Log 탭에서 확인 할 수 있습니다.
* 내가 가진 모든 DB 인스턴스에서 발생한 이벤트를 한꺼번에 보려면, Events 탭으로 이동하여 조회 할 수 있습니다.

![[그림 10] 이벤트 &amp; 로그 -  목록 조회](http://static.toastoven.net/prod_rds/mt_010.png)
<center>[그림 10] 이벤트 &amp; 로그 -  목록 조회</center>

* 이벤트 타입은 어떤 리소스에서 발생한 이벤트인지를 지칭합니다.
    * FLOATING_IP : Floating IP 와 관련된 이벤트 입니다.
    * INSTANCE : DB 인스턴스와 관련된 이벤트 입니다.
    * BACKUP : 백업과 관련된 이벤트 입니다.
* Identifier 는 이벤트가 발생한 리소스를 지칭합니다.
    * 이벤트 타입이 FLOATING_IP 일 경우 IP 주소가 표시됩니다.
    * 이벤트 타입이 INSTANCE 일 경우 DB 인스턴스 이름이 표시됩니다.
    * 이벤트 타입이 BACKUP일 경우 백업 ID가 표시됩니다.

### 알람

* 추후 출시
