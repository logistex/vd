# 장고에서 지도 출력
Hakim, [Displaying a map in a Django Webapp](https://medium.com/@h4k1m0u/displaying-a-map-in-a-django-webapp-1-3-creating-a-gis-database-with-postgresql-and-postgis-e596d3c2310)

## 1. PostgreSQL 및 PostGIS 설치하여 GIS DB 생성

### 1.1 PostgreSQL 및 PostGIS 설치
- [PostgreSQL 공식 웹사이트](https://www.postgresql.org/download/windows/)
[EntrepriseDB’s website](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)에서 다운로드
- 설치 과정에서 디폴트 로케일은 korean으로 선택
- 설치 마지막 단계에서 Stack Builder를 통한 추가 도구 설치 여부를 물어보면, 체크하여 PostGIS 설치 진행
![](https://miro.medium.com/max/569/0*uipJ9lvFQH9f_xDt.png)
![](https://miro.medium.com/max/628/0*VUrNO6TOXYdEXnWt.png)
- PostGIS 설치 과정에서 `Create a spatial database` 선택하고,
user는 기본값 'postgres' 그대로, 비번 입력하고, DB Name은 'my-database'로 진행
![](https://miro.medium.com/max/515/0*DN7jYJ5gxHwhKNUc.png)
- 추가적인 질문에 모두 'yes' 응답
- 시스템 환경 변수 PATH에 'C:\Program Files\PostgreSQL\10\bin' 추가 등록
![](https://miro.medium.com/max/430/0*U5iibRC5Q7H1-h75.png)

### 1.2 사용자 생성 및 GIS DB 소유권 등록
- cmd 명령 프롬프트 실행하여 작업
```SHELL {.line-numbers}
# PostgreSQL에 사용자 'postgres'로 로그인
psql -U postgres
# 비밀번호 입력하면, 프롬프트 나타남

# 계정 생성 개별 사용자 아이디 및 비번 등록
CREATE USER <my-user> WITH PASSWORD ‘<my-password>’;

# GIS DB 'my-database'의 소유권을 개별 사용자에게 등록
ALTER DATABASE 'my-database' OWNER TO <my-user>;

# DB 목록 조회
\list+
# 계정 목록 조회
\du+
```

### 1.3 마무리
- PostgreSQL(DB 엔진) 및 PostGIS(GIS 도구) 설치 완료
- GIS DB('my-database') 생성 완료
- GIS DB 사용을 위한 개별 사용자 및 소유권 등록 완료
- GeoDjango로 GIS 웹 앱 개발 과정을 공부할 예정

## 2. GeoDjango로 GIS 웹 앱 개발
- 세계 도시의 지도 좌표를 테이블에 등록
- 세계 도시를 장고 웹 앱 지도에 표시

### 2.1 장고 프로젝트 생성

1. 가상환경 `vnv_geo` 준비
```SHELL {.line-numbers}
# 콘다 가상환경 정보 확인
$ conda info --envs

# 콘다 가상환경 생성 (장고는 2.x 버전으로 설치)
$ conda create --channel conda-forge --name vnv_geo python django=2.2 psycopg2 qgis=3.4

# 콘다 가상환경 활성화
$ conda activate vnv_geo

# 가상환경에 설치된 패키지 확인
$ conda list
# python=3.7.6 django=2.2.8 psycopg2=2.8.4 qgis=3.4.14 gdal=2.4.2

## 가상환경 스펙 저장 및 생성
#$ conda env export --name vnv_geo > vnv_geo_spec.yml
#$ conda env create --name vnv_geo --file vnv_geo_spec.yml
#
#$ conda list --name vnv_geo --explicit > vnv_geo_spec.txt
#$ conda create --name vnv_geo --file vnv_geo_spec.txt
```

2. 파이참 프로젝트 `c:\geo`생성
- 파이참에서 열려 있는 프로젝트를 닫기
- Create New Project 클릭하기
- 가상환경을 'vnv_vd'로 지정한 'C:\geo' 프로젝트 생성
    - New Project 창의 Pure Python 메뉴에서
    - Location에 'C:\geo' 입력하고
    - Project Interpreter 클릭하여,
      Existing interpreter 선택하고, ... 단추 클릭하여,
      Add Python Interpreter 창에서 Conda Environment 클릭하고,
      Interpreter 항목의 ... 단추 클릭하여,
      'C:\Anaconda3\envs\vnv_geo\python.exe' 선택하고,
      Make available to all project 체크하고,
      OK 단추 클릭한 후,
      Existing interpreter 항목의 Interpreter 리스트 단추를 확장하면 보이는
      'Python 3.8 (vnv_vd)' 항목을 선택하고
    - Create 단추 클릭하여 프로젝트 생성 완료

3. 장고 프로젝트 `world` 생성 및 설정
- 파이참에서 생성된 프로젝트 폴더가 열리면,
  터미널 창을 열어서 프롬프트가 '(vnv_geo) C:\geo>'임을 확인하고 작업
```SHELL {.line-numbers}
(vnv_geo) C:\geo>conda list                          # 설치된 패키지 버전 확인
(vnv_geo) C:\geo>django-admin startproject world .   # 장고 프로젝트 생성
```
- DB 설정 수정
```PYTHON {.line-numbers}
# world/settings.py

DATABASES = {
    'default': {
        'ENGINE': 'django.contrib.gis.db.backends.postgis',
        'NAME': 'my-database',
        'USER': '<database-user>',
        'PASSWORD': '',
        'HOST': 'localhost',
        'PORT': '',
    }
}
```


## 참고 자료
참고 자료는 [../map_ref.md](../map_ref.md)을 참조
