📌 프로젝트 개요

Spark Bulk Data Load (SBDL)은 대량의 데이터를 Spark 기반으로 처리하고 Kafka로 전송하는 데이터 처리 파이프라인입니다. 이 프로젝트는 다양한 환경(Local, QA, Production)에서 실행될 수 있도록 설계되었으며, 데이터 로드, 변환, 조인, 전송 등의 기능을 포함합니다.

📂 폴더 및 파일 구조

SBDL/
│-- conf/                  # 환경 설정 파일
│   │-- sbdl.conf          # 애플리케이션 설정 파일
│   │-- spark.conf         # Spark 설정 파일
│-- lib/                   # 핵심 라이브러리 코드
│   │-- ConfigLoader.py    # 설정 파일 로드 및 처리
│   │-- DataLoader.py      # 데이터 로딩 관련 기능
│   │-- DataGen.py         # 샘플 데이터 생성 스크립트
│   │-- Transformations.py # 데이터 변환 및 조인 로직
│   │-- Utils.py           # Spark 세션 설정 유틸리티
│   │-- logger.py          # Log4j 기반 로깅 유틸리티
│-- test_data/             # 테스트 데이터를 저장하는 폴더
│-- Jenkinsfile            # CI/CD 설정 파일
│-- log4j.properties       # 로깅 설정 파일
│-- main.py                # 프로젝트 메인 실행 파일
│-- Pipfile                # Python 패키지 종속성 관리 파일
│-- Pipfile.lock           # 패키지 버전 고정 파일
│-- sbdl_submit.sh         # Spark Submit 실행 스크립트
│-- test_nutter_sbdl.py    # Nutter 기반 테스트 코드
│-- test_pytest_sbdl.py    # Pytest 기반 테스트 코드
│-- .gitignore             # Git에서 제외할 파일 목록

🚀 설치 및 실행 방법

1️⃣ 환경 설정

먼저 pipenv를 이용하여 필요한 의존성을 설치합니다.

pipenv install

2️⃣ Spark 환경에서 실행

spark-submit --master local[2] main.py local 2022-08-02

또는 클러스터 환경에서 실행하려면:

bash sbdl_submit.sh

⚙️ 환경 설정

conf/sbdl.conf

enable.hive: Hive 사용 여부 (true / false)

hive.database: Hive 데이터베이스 이름

kafka.topic: Kafka로 전송할 토픽명

kafka.bootstrap.servers: Kafka 서버 정보

conf/spark.conf

spark.executor.instances: 실행할 Executor 개수

spark.executor.memory: Executor 메모리 할당량

🛠 주요 파일 설명

🔹 main.py

프로젝트의 메인 실행 파일로, 다음 단계를 수행합니다:

환경 변수 및 설정 로드

Spark 세션 생성

계정, 관계, 주소 데이터 로드 및 변환

Kafka에 데이터 전송

🔹 lib/ConfigLoader.py

설정 파일(sbdl.conf, spark.conf)을 로드하고 환경별 설정을 적용하는 기능을 담당합니다.

🔹 lib/DataLoader.py

CSV 또는 Hive 테이블에서 데이터를 로드하는 역할

read_accounts(), read_parties(), read_address() 함수 제공

🔹 lib/Transformations.py

데이터 변환, 조인 및 가공 로직 구현

get_contract(), get_relations(), apply_header() 등의 함수 포함

🔹 lib/Utils.py

get_spark_session(): 환경에 맞는 Spark 세션을 생성

🔹 lib/logger.py

Log4j 기반의 로깅 설정을 포함하여 로그 관리

🔹 test_pytest_sbdl.py

Pytest 기반 단위 테스트 파일

DataLoader, Transformations 등의 기능 테스트 수행

🔹 test_nutter_sbdl.py

Databricks Nutter 기반 테스트 스크립트

📜 로깅 및 디버깅

log4j.properties

Spark 로그 레벨을 설정 (INFO, WARN, ERROR 등)

Kafka 관련 디버깅 로그 설정 포함

🧪 테스트 수행 방법

pytest test_pytest_sbdl.py

또는 Nutter 테스트 실행:

python test_nutter_sbdl.py

🚀 배포 및 CI/CD

Jenkinsfile

CI/CD 파이프라인을 정의하며, Spark 애플리케이션을 빌드하고 배포하는 과정 포함

sbdl_submit.sh

spark-submit 명령어를 사용하여 클러스터에서 실행하는 스크립트

