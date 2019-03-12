---
title: "에어플로우 구버전에서 DAG 삭제하는 법(mysql 사용 시)"
last_modified_at: 2019-03-10T00:00:00
category: record
tag: 
    - PYTHON
    - airflow 
    - mysql
---

에어플로우 버전 1.10부터 모든 관련 테이블에서 DAG 정보를 삭제하는 커맨드가 추가되었다. CLI와 REST API로 사용 가능하고, 웹 UI에도 삭제 버튼이 생겼다. [참조](https://stackoverflow.com/questions/40651783/airflow-how-to-delete-a-dag)  

하지만 그 이하 버전을 사용 중이라면 직접 DB에서 관련 정보를 삭제하는 수 밖에 없다. 아래 코드는 DB를 mysql로 사용했을 때 DB에 접속해서 DAG를 삭제하는 방법이다. 
```
set @dag_id = 'BAD_DAG';  # 삭제할 DAG 이름

delete from airflow.xcom where dag_id = @dag_id;
delete from airflow.task_fail where dag_id = @dag_id;
delete from airflow.task_instance where dag_id = @dag_id;
delete from airflow.sla_miss where dag_id = @dag_id;
delete from airflow.log where dag_id = @dag_id;
delete from airflow.job where dag_id = @dag_id;
delete from airflow.dag_run where dag_id = @dag_id;
delete from airflow.dag_stats where dag_id = @dag_id;
delete from airflow.dag where dag_id = @dag_id;
```
외래키 제약 때문에 위의 순서대로 지워줘야 하더라.
