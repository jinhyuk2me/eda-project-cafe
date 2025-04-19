<p align="center">
  <img src="https://github.com/jinhyuk2me/eda-project-cafespot/blob/main/img/banner.png?raw=true" width="100%">
</p>

---

# 스타벅스 vs 이디야: 입지 전략 비교 분석  
> **Store Location Analysis Project: Starbucks vs Ediya in Seoul**

---

## 🗂️ 프로젝트 개요

서울시 내 대표 프랜차이즈 카페인 **스타벅스**와 **이디야**의 매장 위치 데이터를 수집하여,  
**공간적 근접성**, **상권 중복도**, **입점 전략의 차이**를 정량적으로 비교 분석한 프로젝트입니다.  
실제 주소 기반 크롤링, 좌표 변환, DB 저장, 거리 계산, 상관관계 분석, 지도 시각화까지 일련의 분석 파이프라인을 구현했습니다.

---

## ⚙️ 기술 스택

| 분류 | 기술 | 배지 |
|------|------|------|
| **개발환경** | Ubuntu (Linux)<br>VS Code<br>Jupyter Notebook | ![Linux](https://img.shields.io/badge/linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)<br>![VS Code](https://img.shields.io/badge/VSCode-007ACC?style=for-the-badge&logo=visual-studio-code&logoColor=white)<br>![Jupyter](https://img.shields.io/badge/jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white) |
| **언어** | Python 3 | ![Python](https://img.shields.io/badge/python-3776AB?style=for-the-badge&logo=python&logoColor=white) |
| **데이터 수집** | BeautifulSoup<br>Selenium<br>Naver API<br>Google Maps API | ![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup-FFDB4D?style=for-the-badge&logo=python&logoColor=black)<br>![Selenium](https://img.shields.io/badge/selenium-43B02A?style=for-the-badge&logo=selenium&logoColor=white)<br>![Google Maps](https://img.shields.io/badge/Google_Maps_API-4285F4?style=for-the-badge&logo=googlemaps&logoColor=white)<br>![Naver API](https://img.shields.io/badge/Naver_API-03C75A?style=for-the-badge&logo=naver&logoColor=white) |
| **데이터 분석** | Pandas<br>Numpy | ![Pandas](https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)<br>![Numpy](https://img.shields.io/badge/numpy-013243?style=for-the-badge&logo=numpy&logoColor=white) |
| **시각화** | Matplotlib<br>Folium | ![Matplotlib](https://img.shields.io/badge/matplotlib-11557C?style=for-the-badge&logo=matplotlib&logoColor=white)<br>![Folium](https://img.shields.io/badge/folium-77B829?style=for-the-badge&logo=leaflet&logoColor=white) |
| **DB** | MySQL | ![MySQL](https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white) |
| **형상 관리** | Git / GitHub | ![Git](https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white) ![GitHub](https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white) |

---

## 🧩 전체 분석 흐름

본 프로젝트는 매장 간 입지 관계를 파악하기 위해 **두 가지 상이한 방식**의 분석을 병행하였습니다.  
각 방식은 다른 데이터 기준과 알고리즘을 바탕으로 서로 보완적인 인사이트를 제공합니다.

---

### 🛣️ [1] 거리 기반 근접성 분석

> **위경도 좌표 기반으로 두 매장 간 실제 거리**를 계산하여, 이디야 매장이 스타벅스 반경 내 얼마나 분포하는지 계량적으로 분석

1. **매장 주소 크롤링**
   - 스타벅스: 홈페이지에서 도로명 주소 수집
   - 이디야: 지번 주소 제공 → 도로명 주소로 정제 필요

2. **좌표 변환**
   - Google Maps API 기반 위경도 추출
   - Naver API, Selenium 등 보조 수단을 활용해 주소 품질 보완

3. **거리 계산**
   - `Haversine 공식`으로 두 좌표 간 거리 계산
   - `KDTree` 알고리즘을 활용해 이디야 ↔ 스타벅스 간 **최근접 매장 거리** 추출

4. **시각화 및 해석**
   - `folium`을 활용한 매장 위치 지도 시각화
   - `matplotlib` 기반 거리 분포 히스토그램 생성
   - 100m / 300m / 500m 이내 매장 비율 계량화

---

### 🏙️ [2] 도로명 주소 기반 상권 중복 분석

> **동일 도로명 기준으로 스타벅스와 이디야 매장 수를 집계**하여, 두 브랜드가 동일 상권을 얼마나 공유하는지 파악

1. **주소 정제 및 전처리**
   - `AddressManager` 클래스에서 지번 주소를 도로명 주소로 변환
   - 서울시 도로명만 필터링 (`isSeoul`, `isDoro` 등)

2. **도로 단위 매장 수 집계**
   - 각 도로별 스타벅스/이디야 매장 수 카운트
   - 동일 도로상 브랜드 간 입지 밀도 비교

3. **상관관계 분석**
   - `Pandas`를 활용해 도로 기준 매장 수 테이블 생성
   - Pearson 상관계수 계산 → **ρ ≈ 0.6937**

4. **시각화 및 해석**
   - 상관분석 결과 테이블 및 scatter plot 생성
   - 도로 단위 상권 중복도를 수치 기반으로 판단

---

## 📑 주요 분석 결과 요약

| 항목 | 결과 |
|------|------|
| **100m 이내 근접 비율** | 약 12~15% |
| **300m 이내** | 약 42~47% |
| **500m 이내** | 약 63~68% |
| **도로명 기반 매장 수 상관관계** | **0.6937** |
| **전략 해석** | 같은 생활권에서 일정 거리 두고 **공존**하는 전략 추정됨 |

> ❗ 두 브랜드는 서로 다른 지역을 피하기보다는, **같은 상권 내 일정 거리 유지 전략**을 통해 공존하며 시장을 나누는 경향을 보임.

---

## 📊 분석 및 시각화

### 📍 Figure A. 스타벅스 & 이디야 매장 위치 지도
![Figure A](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/store%20map%20folium.png?raw=true)

### 📊 Figure B. 이디야 매장의 최근접 스타벅스 거리 분포
**[물리적 거리 계산: Haversine]**
- 100m 이내에 있는 이디야 매장 비율: 15.32%
- 300m 이내에 있는 이디야 매장 비율: 47.94%
- 500m 이내에 있는 이디야 매장 비율: 68.37%
**[물리적 거리 계산: KDTree]**
- 100m 이내에 있는 이디야 매장 개수: 65 / 509 (12.77%)
- 300m 이내에 있는 이디야 매장 개수: 218 / 509 (42.83%)
- 500m 이내에 있는 이디야 매장 개수: 323 / 509 (63.46%)

### 📈 Figure C. 도로명 기준 매장 수 상관관계 분석
![Figure C](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/correlation%20by%20region.png?raw=true)

---

## 🙋‍♂️ 기여자

| 이름 | GitHub |
|------|--------|
| 장진혁 (Jinhyuk Jang) | [@jinhyuk2me](https://github.com/jinhyuk2me) |

---

## 📎 참고 및 출처

- [스타벅스 매장 찾기](https://www.starbucks.co.kr/store/store_map.do)
- [이디야 매장 찾기](https://smartediya.com/store)
- Google Maps Geocoding API
- Naver Local Search API
