## Database > RDS for MySQL > API 가이드

| 리전 | 엔드포인트 |
|---|---|
| 한국(판교) 리전 | https://api-gw.cloud.toast.com/rds-for-mysql-kr1 |
| 한국(평촌) 리전 | https://api-gw.cloud.toast.com/rds-for-mysql-kr2 |
| 일본 리전 | https://api-gw.cloud.toast.com/rds-for-mysql-jp1 |

## Monitoring

### Metric 조회

```
GET /rds/api/v1.0/appkeys/{appkey}/monitoring/metrics
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| appkey | URL | String | O | 상품 Appkey 또는 프로젝트 통합 Appkey |

#### 응답

```json
{
"metrics" : [
{
"metricName" : "CPU_USAGE",
"unit" : "percent"
},
{
"metricName" : "NETWORK_SENT",
"unit" : "bps"
}
]
}
```

### 모니터링 데이터 조회

```
GET /rds/api/v1.0/appkeys/{appkey}/monitoring/metric-statistics
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 | 제약 사항 |
|---|---|---|---|---|
| appkey | URL | String | O | 상품 Appkey 또는 프로젝트 통합 Appkey | |
| instanceId | Query | Array(String) | O | DB 인스턴스 아이디 | Min:1, Max: 20 |
| metricName | Query | Enum | O | 통계 항목(Metric) 이름 | |
| period | Query | Enum | O | 조회 주기 | |
| statisticsType | Query | Enum | O | 통계 타입 | |
| from | Query | Datetime | O | 조회 시작일시 | |
| to | Query | Datetime | O | 조회 종료일시 | |

#### 응답

```json
{
"metricStatistics" : [
{
"instanceId" : "72b5f839-9faf-4243-9410-27072656caa3",
"metrics" : [
{
"metricName" : "CPU_USAGE",
"unit" : "percent",
"dataList" : [
{
"datetime" : "2020-08-06T13:30:00.000+0900",
"value" : 10
},
{
"datetime" : "2020-08-06T13:31:00.000+0900",
"value" : 15
}
]
}
]
}
]
}
```