## Database > RDS for MySQL > 콘솔 사용 가이드 > Networks

## Networks

* Compute & Network 상품의 사용자 network를 RDS상품에 연결하여, RDS의 DB 인스턴스가 사용자의 인스턴스와 통신할 수 있습니다.
* Networks 탭을 누르면 연결된 네트워크 리스트를 볼 수 있습니다.

![[그림 1] 네트워크 화면](http://static.toastoven.net/prod_rds/nw_001.png)
<center>[그림 1] 네트워크 화면</center>

* 우선 Compute & Network 상품을 통해 연결하고자 하는 사용자 network와 subnet을 등록하고 해당 network와 subnet을 router에 등록하여야합니다.
* Compute & Network 상품이 Enable 되어있지 않으면 연결 가능한 네트워크 항목이 표시되지 않습니다.

![[그림 2] 네트워크 화면](http://static.toastoven.net/prod_rds/nw_002-1.png)
![[그림 3] 네트워크 화면](http://static.toastoven.net/prod_rds/nw_002-2.png)
<center>[그림 2] Compute & Network 상품의 network, router 화면</center>

* 연결하기를 원하는 네트워크를 선택하고 설명을 기입한 후 확인을 누릅니다.

![[그림 4] 네트워크 화면](http://static.toastoven.net/prod_rds/nw_003-1.png)
![[그림 5] 네트워크 화면](http://static.toastoven.net/prod_rds/nw_003-2.png)
<center>[그림 3] network 연결 생성 화면</center>

![[그림 6] 네트워크 화면](http://static.toastoven.net/prod_rds/nw_004.png)
<center>[그림 4] network 연결 완료 화면</center>

* 원하는 네트워크 연결을 선택한 후 삭제할 수 있습니다.

![[그림 7] 네트워크 화면](http://static.toastoven.net/prod_rds/nw_005.png)
<center>[그림 5] network 연결 삭제 화면</center>