# 스타벅스 vs 이디야: 매장 입지 비교 분석 프로젝트

> **📅 프로젝트 기간: 2025.03.15 (1Day Project)**

## 📌 개요
본 프로젝트는 서울시 내 커피 프랜차이즈 브랜드 **스타벅스**와 **이디야**의 매장 정보를 웹 크롤링을 통해 수집한 뒤, 위치 정보를 분석하여 두 브랜드 간의 입지 전략을 비교하는 분석 프로젝트입니다.

## 🎯 분석 목적
- 두 브랜드 매장의 위치 중복 여부 및 공간적 근접성 분석
- 상권 공유 수준 및 거리 기반 전략 차이 파악
- 데이터 수집 → 저장 → 거리 계산 → 시각화 → 상관관계 분석까지 일련의 파이프라인 구현

## 🛠️ 기술 스택

| 분류 | 기술 | 배지 |
|------|------|------|
| **개발환경** | Ubuntu (Linux)<br>VS Code<br>Jupyter Notebook | ![Linux](https://img.shields.io/badge/linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)<br>![VS Code](https://img.shields.io/badge/VSCode-007ACC?style=for-the-badge&logo=visual-studio-code&logoColor=white)<br>![Jupyter](https://img.shields.io/badge/jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white) |
| **언어** | Python | ![Python](https://img.shields.io/badge/python-3776AB?style=for-the-badge&logo=python&logoColor=white) |
| **데이터 수집** | BeautifulSoup<br>urllib<br>Google Maps API<br>Naver API<br>Selenium | ![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup-FFDB4D?style=for-the-badge&logo=python&logoColor=black)<br>![urllib](https://img.shields.io/badge/urllib-4B8BBE?style=for-the-badge&logo=python&logoColor=white)<br>![Google Maps](https://img.shields.io/badge/Google_Maps_API-4285F4?style=for-the-badge&logo=googlemaps&logoColor=white)<br>![Naver API](https://img.shields.io/badge/Naver_API-03C75A?style=for-the-badge&logo=naver&logoColor=white)<br>![Selenium](https://img.shields.io/badge/selenium-43B02A?style=for-the-badge&logo=selenium&logoColor=white) |
| **데이터 분석** | Pandas<br>Matplotlib<br>Seaborn<br>Numpy | ![Pandas](https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)<br>![Matplotlib](https://img.shields.io/badge/matplotlib-11557C?style=for-the-badge&logo=matplotlib&logoColor=white)<br>![Seaborn](https://img.shields.io/badge/seaborn-4B8BBE?style=for-the-badge&logo=python&logoColor=white)<br>![Numpy](https://img.shields.io/badge/numpy-013243?style=for-the-badge&logo=numpy&logoColor=white) |
| **시각화** | Folium | ![Folium](https://img.shields.io/badge/folium-77B829?style=for-the-badge&logo=leaflet&logoColor=white) |
| **DB** | MySQL | ![MySQL](https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white) |
| **형상 관리** | Git / GitHub | ![Git](https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white) ![GitHub](https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white) |



## 🗂️ 데이터 수집 및 처리 흐름
1. **매장 주소 크롤링**:
   - 스타벅스: 공식 홈페이지에서 도로명 주소 수집
   - 이디야: 홈페이지에서 지번 주소 수집 → 도로명 주소로 변환 필요

2. **주소 → 좌표 변환**:
   - Google Maps API 사용 (좌표 변환)
   - 이디야 주소의 경우 도로명 보완을 위해 Naver API 및 Selenium까지 활용

3. **MySQL 저장 및 불러오기**:
   - 커스텀 `StoreDBManager` 클래스 활용
   - 중복 방지를 위해 `store name`을 PK로 설정

4. **거리 계산 및 분석**:
   - `Haversine 공식` + `KDTree` 기반 최근접 거리 계산
   - 이디야 매장이 스타벅스 반경 내에 얼마나 위치하는지 계량 분석

5. **시각화**:
   - `folium`을 통한 지도 기반 시각화
   - 거리 분포 히스토그램, 상관계수 등 시각적 해석 포함

## 📊 분석 결과 요약

- 이디야 매장 중 약 **65%** 가 **500m 이내에 스타벅스 매장** 존재
- **300m 이내**에는 **약 42~47%** 의 이디야 매장이 위치
- **100m 이내**로 매우 근접한 매장은 **약 12~15%** 수준
- 이는 **극단적인 근접보다는 일정 거리 유지** 전략을 의미함
- 도로명 주소 단위 기준 매장 수 **상관계수 ≈ 0.69** → 두 브랜드는 같은 도로권·상권을 많이 공유함
- 따라서 **서로 다른 지역을 공략하는 전략보다는, 생활권 내 일정 거리 두고 공존**하는 전략으로 해석됨

> ❗ 단, 이 분석은 물리적 거리와 주소 기반 통계에 의존하고 있어, 유동 인구, 입지 상권 등 추가 변수에 대한 고려는 후속 분석이 필요함


## 발표자료

![슬라이드 1](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0001.jpg?raw=true)  
![슬라이드 2](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0002.jpg?raw=true)  
![슬라이드 3](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0003.jpg?raw=true)  
![슬라이드 4](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0004.jpg?raw=true)  
![슬라이드 5](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0005.jpg?raw=true)  
![슬라이드 6](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0006.jpg?raw=true)  
![슬라이드 7](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0007.jpg?raw=true)  
![슬라이드 8](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0008.jpg?raw=true)  
![슬라이드 9](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0009.jpg?raw=true)  
![슬라이드 10](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0010.jpg?raw=true)  
![슬라이드 11](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0011.jpg?raw=true)  
![슬라이드 12](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0012.jpg?raw=true)  
![슬라이드 13](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0013.jpg?raw=true)  
![슬라이드 14](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0014.jpg?raw=true)  
![슬라이드 15](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0015.jpg?raw=true)  
![슬라이드 16](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0016.jpg?raw=true)  
![슬라이드 17](https://github.com/jinhyuk2me/eda-project-cafe/blob/main/img/스타벅스%20vs.%20이디야_%20데이터로%20보는%20거리와%20분포_page-0017.jpg?raw=true)  
