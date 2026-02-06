# 1. 👥팀 소개
🚗 **motor-chata**

팀을 소개하는 짤막한 말..


<table>
  <tr align="center">
    <td><img src="https://github.com/jjhhyy0926/motor-chata/blob/main/assets/minha.png?raw=true" width="120px"><br><b>김민하</b></td>
    <td><img src="https://github.com/jjhhyy0926/motor-chata/blob/main/assets/jaehyun.png?raw=true" width="120px"><br><b>배재현</b></td>
    <td><img src="https://github.com/jjhhyy0926/motor-chata/blob/main/assets/jihye.png?raw=true" width="120px"><br><b>윤지혜</b></td>
    <td><img src="https://github.com/jjhhyy0926/motor-chata/blob/main/assets/yhjeon.png?raw=true" width="120px"><br><b>전윤하</b></td>
    <td><img src="https://github.com/motor-chata/motor-chata/blob/main/assets/ekthf.png?raw=true" width="120px"><br><b>정다솔</b></td>
    <td><img src="https://github.com/motor-chata/motor-chata/blob/main/assets/wlkstj.png?raw=true" width="120px"><br><b>홍진서</b></td>
  </tr>

  <tr align="center">
    <td><b>GitHub 총괄 관리/ERD 작성/Figma UI 디자인/ERD 작성/로직 설계 </b></td>
    <td><b>발표/대본 작성/ERD 작성 </b></td>
    <td><b>노션 정리/ERD 작성 보조/웹 크롤링/데이터 전처리/DB적재 </b></td>
    <td><b>일정 관리/ERD 작성/Streamlit 구현/DB 스키마 모델링(코드 변환)</b></td>
    <td><b>회의록 보조/ERD 작성/DB 구축/웹 크롤링/DB 적재</b></td>
    <td><b>회의록 작성/ERD 작성/PPT 작성/대본 작성/</b></td>
  </tr></table>

---
# 2. 프로젝트 기간
2026-02-04 ~ 2026-02-06

---
# 3. 프로젝트 개요
## 프로젝트명
### 🚗mota-chata : ㄹㅇㄹ
## 프로젝트 소개
중고차 거래 비중이 높은 차량을 중심으로 공식 리콜 데이터를 기반한 결함 내용과 시정 방법을 한눈에 제공해 소비자의 구매·조치 판단을 돕는 것이 목적입니다.
## 기대효과
- **리콜 정보 접근성 향상**
분산된 리콜 데이터를 한 화면에서 제공함으로써, 차량 결함 정보 탐색에 필요한 시간과 비용을 크게 줄일 수 있다.
- **안전 위험 사전 예방 효과**
차량별 반복되는 결함 패턴과 위험 요소를 명확히 확인할 수 있어, 운행 중 발생할 수 있는 안전사고 가능성을 줄이는 데 기여한다.
- **차량 유지관리 수준 향상**
시정 방법 및 문의처 정보를 제공하여 운전자가 필요한 점검이나 조치를 즉시 확인하고 대응할 수 있도록 지원한다.
- **제조사·모델 간 품질 비교 용이**
브랜드별·차종별 리콜 패턴을 비교해 차량 품질 수준을 직관적으로 확인할 수 있어, 장기적 차량 선택 기준 수립에 도움을 준다.
- **사용자 경험 개선(UX 향상)**
검색·필터·요약지표(KPI) 등 직관적인 UI를 통해 리콜 정보 활용성을 높이며, 이용자가 결함 정보를 쉽게 이해할 수 있도록 한다.
- **정책 및 제조사 개선 인사이트 제공**
축적된 리콜 데이터를 분석하면 특정 제조사나 모델의 반복 결함을 파악할 수 있어, 제도 개선이나 서비스 품질 향상을 위한 자료로 활용될 수 있다.
## 대상 사용자
중고차 구매자와 차량 보유 운전자가 리콜 이력과 시정 방법을 쉽게 확인하고,
초보 운전자 및 자동차 정보 콘텐츠 제작자까지 활용할 수 있는 서비스입니다.

---
# 4. 프로젝트 설계
## 프로젝트 구조
## ERD
## Table Specification
### 1) tbl_manufacturer — 제조사 정보
- 제조사 기본 정보를 관리
- PK: maker_id

| Column | Type | Description |
|--------|------|-------------|
| maker_id | INT | PK |
| maker_name | VARCHAR(30) | 제조사 이름 |
| maker_detail | VARCHAR(50) | 제조사 상세명 |
| region_at | VARCHAR(10) | 제조사 지역 |

---

### 2) tbl_model — 모델 정보
- 모델명과 생산기간 관리
- PK: model_id, FK: maker_id

| Column | Type | Description |
|--------|------|-------------|
| model_id | INT | PK |
| maker_id | INT | FK → tbl_manufacturer.maker_id |
| model_name | VARCHAR(255) | 모델명 |
| start_date | DATETIME | 생산 시작 시점 |
| end_date | DATETIME | 생산 종료 시점 |

---

### 3) tbl_recall — 리콜 정보
- 리콜 사례를 저장하는 핵심 테이블
- PK: recall_id, FK: model_id

| Column | Type | Description |
|--------|------|-------------|
| recall_id | INT | PK |
| model_id | INT | FK → tbl_model.model_id |
| recall_title | VARCHAR(255) | 리콜 제목 |
| recall_type | VARCHAR(50) | 리콜 유형 |
| fix_method | TEXT | 시정 방법 |
| defect_desc | TEXT | 결함 설명 |
| recall_center | VARCHAR(255) | 시정센터/문의처 |
| recall_quantity | INT | 대상 수량 |
| recall_date | VARCHAR(30) | 리콜 공표일 |
| device_type | VARCHAR(50) | 장치 분류 |
---
# 5. 트러블 슈팅

---
# 6. 기술 스택

### 🛠 Development Environment
- PyCharm
- GitHub

### 📡 Data Collection
- Requests
- Selenium
- BeautifulSoup4
- JSON Parsing

### 🗄 Database
- MySQL
- ERDCloud (ERD 설계)
- CSV Import

### 🌐 Web Application
- Streamlit

### 🎨 UI / Documentation
- Figma
- Notion


---
# 7. 데이터 출처
- 자동차리콜센터 (국토교통부 · 한국교통안전공단 제공)
- https://www.car.go.kr/ri/main.do
본 프로젝트의 리콜 정보, 결함 내용, 시정 방법 데이터는 자동차리콜센터의 공개 데이터를 기반으로 크롤링하여 수집했습니다.

---
# 한줄 회고