# Sign new v2.1 API 명세
- 변경서 다중 SQL 그룹 지원을 위해서 작성된 API 명세서 입니다.
- 기존 SIGN v2.1 API의 문서 부분이 수정되었습니다.

# 문서 작성
## 승인 요청
작성 완료된 DB 데이터 변경 요청서를 생성 합니다.
### URL
* /api/sign/doc/dataModify/ask
* POST
* application/json;charset=UTF-8
### Request
|항목|값(예시)|타입|설명|
|---|---|---|---|
|selectBeforeDataCountFlag|false|boolean|변경 전 데이터 조회 여부<br/>true : 조회<br/>false : 조회 안함|
|docTitle|\[변경\] DB데이터변경|String|문서 제목|
|describe|DB데이터변경사유|String|사유|
|aprvLimit|2021/05/05|String|결재 기한|
|dataModifyTargetId|34|int|변경 대상 ID|
|orgUid|u01|String|기안자 ID|
|groundsDocId|근거-001|String|근거 문서 번호|
|apvLineApprover||Array|결재자 목록|
|approverOrgUid|m01|String|결재자 ID|
|approveOrder|1|int|결재 순서|
|approvePowerType|0|int|결재 권한 종류<br/>0 : 결재<br/>1 : DB데이터변경실행|
|sqlGroup||Array|SQL 그룹 리스트|
|sqlGroupName|사용자 데이터 변경|String|SQL 그룹 이름|
|modifySqlType|1|int|변경 SQL종류<br/>1 : 기본SQL<br/>2 : PL/SQL|
|modifySql|update emp_sign set empno=1002 where empno=1001|String|변경 SQL|
|beforeSql|select * from emp_sign where empno=1001|String|변경 전 검증SQL|
|afterSql|select * from emp_sign where empno=1002|String|변경 후 검증SQL|


```json
{
    "selectBeforeDataCountFlag": false,
    "docTitle": "[변경] DB데이터변경",
    "describe": "DB데이터변경사유",
    "aprvLimit": "2024/11/05",
    "dataModifyTargetId": "2",
    "orgUid": "test",
    "groundsDocId": "",
    "apvLineApprover": [
        {
            "approveOrder": 1,
            "approvePowerType": 0,
            "approverOrgUid": "test"
        },
        {
            "approveOrder": 2,
            "approvePowerType": 1,
            "approverOrgUid": "test"
        }
    ],
    "sqlGroup":[
		    {
				    "sqlGroupName": "SQL 그룹 1",
				    "modifySqlType": 1,
				    "modifySql": "update emp_sign set empno=1002 where empno=1001",
				    "beforeSql": "select * from emp_sign where empno=1001",
				    "afterSql": "select * from emp_sign where empno=1002"
		    },
		    {
				    "sqlGroupName": "SQL 그룹 2",
				    "modifySqlType": 1,
				    "modifySql": "update emp_sign set empno=1003 where empno=1004",
				    "beforeSql": "select * from emp_sign where empno=1003",
				    "afterSql": "select * from emp_sign where empno=1004"
		    }
    ]
}
```
### Response
|항목|값(예시)|타입|설명|
|---|---|---|---|
|code|200|int|결과 코드|
|data||Map|결과 데이터|
|docId|2021000005|String|결재 문서 번호|
|message||String|결과 메시지|

[성공]
```json
{
    "code": 200,
    "data": {
        "docId": "2021000005"
    },
    "message": ""
}
```

[실패]
```json
{
    "code": 500,
    "message": "",
    "data": {}
}
```
