<p align="center">
  <img src="https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/banner.png?raw=true" width="100%">
</p>

---
# 스타벅스 vs 이디야: 서울시 매장 입지 비교 분석
> **Location Strategy Comparison: Starbucks vs Ediya**

---

## 🗂️ 프로젝트 개요

서울시 내 대표 커피 프랜차이즈인 **스타벅스**와 **이디야**의 매장 위치 데이터를 수집하여, **공간적 근접성**, **상권 중복도**, **거리 기반 전략** 등을 비교 분석한 프로젝트입니다.  
**Selenium** 기반 크롤링과 **Google Maps API**를 활용하여 좌표를 추출하고, **MySQL** 기반 저장 및 **folium** 시각화를 수행했습니다.

---

## ⚙️ 기술 스택

| 분류 | 기술 | 배지 |
|------|------|------|
| **개발환경** | Ubuntu (Linux)<br>VS Code<br>Jupyter Notebook | ![Linux](https://img.shields.io/badge/linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)<br>![VS Code](https://img.shields.io/badge/VSCode-007ACC?style=for-the-badge&logo=visual-studio-code&logoColor=white)<br>![Jupyter](https://img.shields.io/badge/jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white) |
| **언어** | Python 3 | ![Python](https://img.shields.io/badge/python-3776AB?style=for-the-badge&logo=python&logoColor=white) |
| **데이터 수집** | BeautifulSoup<br>Selenium<br>Naver API<br>Google Maps API | ![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup-FFDB4D?style=for-the-badge&logo=python&logoColor=black)<br>![Selenium](https://img.shields.io/badge/selenium-43B02A?style=for-the-badge&logo=selenium&logoColor=white)<br>![Google Maps](https://img.shields.io/badge/Google_Maps_API-4285F4?style=for-the-badge&logo=googlemaps&logoColor=white)<br>![Naver API](https://img.shields.io/badge/Naver_API-03C75A?style=for-the-badge&logo=naver&logoColor=white) |
| **데이터 분석** | Pandas<br>Numpy<br>Scipy<br>sklearn | ![Pandas](https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)<br>![Numpy](https://img.shields.io/badge/numpy-013243?style=for-the-badge&logo=numpy&logoColor=white) |
| **시각화** | Matplotlib<br>Folium | ![Matplotlib](https://img.shields.io/badge/matplotlib-11557C?style=for-the-badge&logo=matplotlib&logoColor=white)<br>![Folium](https://img.shields.io/badge/folium-77B829?style=for-the-badge&logo=leaflet&logoColor=white) |
| **DB** | MySQL | ![MySQL](https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white) |
| **형상 관리** | Git / GitHub | ![Git](https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white) ![GitHub](https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white) |

---

## 📥 데이터 수집 및 처리 흐름

| 단계 | 설명 |
|------|------|
| **1. 주소 수집** | 스타벅스/이디야 각각의 공식 웹사이트에서 매장 주소 크롤링 |
| **2. 좌표 변환** | Google Maps API를 사용하여 위경도 추출, 필요시 Naver API 및 Selenium 보완 |
| **3. DB 저장** | MySQL + 커스텀 `StoreDBManager` 클래스 활용, 중복 방지 로직 포함 |
| **4. 거리 계산** | `haversine` 공식 기반 거리 계산 + `KDTree`를 통한 최근접 거리 탐색 |
| **5. 시각화** | folium 기반 지도 시각화, 거리 히스토그램 및 분포 시각화 포함 |

---

## 🔎 분석 항목

### 📌 거리 기반 분석
- **이디야 ↔ 스타벅스 간 최근접 거리** 측정
- 100m / 300m / 500m 이내 비율 도출

### 📌 공간 중복도 분석
- 같은 행정구/도로 단위의 매장 수 비교
- Pearson 상관계수로 입지 중복 정도 파악

### 📌 시각화
- folium 지도 기반 **매장 위치 시각화**
- matplotlib 기반 거리 히스토그램

---

## 📑 주요 결과 요약

| 항목 | 인사이트 |
|------|----------|
| **이디야 500m 이내 스타벅스 존재율** | 약 **65%** |
| **300m 이내 근접 매장 비율** | 약 **42~47%** |
| **100m 이내 초근접 비율** | 약 **12~15%** |
| **공간 상관관계** | 도로 단위 기준 매장 수 상관계수 **≈ 0.69** |
| **전략 해석** | 두 브랜드는 **적정 거리 두고 상권 공존 전략** 유지하는 경향 |

---

## 📊 시각화 예시 (Figures A–C)

### 📍 Figure A. 서울시 내 스타벅스 & 이디야 매장 위치 (folium)
![Figure A](img/store_map_folium.png)

---

### 📊 Figure B. 이디야 매장과 가장 가까운 스타벅스 거리 분포
![Figure B](img/ediya_nearest_starbucks_hist.png)

---

### 📈 Figure C. 행정동 단위 매장 수 상관관계
![Figure C](img/correlation_by_region.png)

---

## 🙋‍♂️ 기여자

| 이름 | GitHub |
|------|--------|
| 장진혁 (Jinhyuk Jang) | [@jinhyuk2me](https://github.com/jinhyuk2me) |

---

## 📌 참고 및 주의 사항

- 본 분석은 **물리적 거리와 행정구 단위 통계**를 기반으로 수행되었습니다.
- **유동 인구, 상권 특성, 매장 규모 등** 외부 변수는 미포함이므로, **해석 시 참고 수준**으로 활용 부탁드립니다.
