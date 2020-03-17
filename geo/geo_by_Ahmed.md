# 위치-기반 웹 앱 작성 (Django 및 GeoDjango 활용)
- 190000, vl, Ahmed Bouchefra, [Make a Location-Based Web App With Django and GeoDjango](https://realpython.com/location-based-app-with-geodjango-tutorial/)
  GeoDjango, PostgreSQL and PostGIS
  his [code](https://github.com/realpython/materials/tree/master/nearbyshops)

## 1. 목표
- 지정한 위치에 근접한 상점 이름과 거리를 보여주는 장면
  - 한양여대 주변 상점
  - 서울시청 주변 상점
![](https://files.realpython.com/media/Screenshot_from_2018-11-28_21-13-19.35e78f378050.png)
- 관리자 화면에서 지도에 기반하여 상점을 등록하는 장면
![](https://files.realpython.com/media/Screenshot_from_2018-11-28_21-12-25.2e7a3ff3f939.png)
- [OpenStreetMap](http://www.openstreetmap.org/)에서 [overpass turbo](https://overpass-turbo.eu/)라는 웹-기반 지리 데이터 검색 도구를 써서 획득한 Miami 지역 상점 데이터
  - 우리 실습에선 'shop in Seoul'로 적용
  - 이렇게 획득한 JSON 데이터를 장고 DB에 적재
![](https://files.realpython.com/media/Screenshot_from_2018-10-19_02-34-34.dce4b6e8d898.png)
- 'shop in Miami'로 지리 데이터 검색하는 장면
![](https://files.realpython.com/media/Screenshot_from_2018-11-09_22-55-41.7a5b7e60974c.png)
- `download/copy as raw OSM data` 링크를 통하여 JSON 파일로 다운로드하는 장면
![](https://files.realpython.com/media/Screenshot_from_2018-10-19_02-25-43.ac6770d6a956.png)

## 2. 준비
### 2.1 OSGeo4W 설치
- OSGeo4W 소개
  - GAL/OGR, QuantumGIS(qgis) 등 여러 GIS 프로그램을 묶은 패키지
  - 지도 관련 작업에 매우 자주 사용되는 패키지
  - [홈 페이지](https://trac.osgeo.org/osgeo4w/)에서
      운영체제에 맞는 버전(32bit/64bit)을 다운 받아 실행하면
      필요한 파일을 인터넷을 통해서 설치하는 방식 (상당히 오래 걸림...)
  - [한글 설치 안내](https://gisngps.tistory.com/2)
  - 아래 설치 방법 중 단계 4에서 <b>`3.12-1`</b> 버전을 선택하도록, 주의가 필요함
- 설치 방법
  0. 아래 과정에서 특별한 언급이 없으면 그냥 `다음`으로 진행
  1. 첫 화면에서 `Advanced Install` 선택
  2. `Choose Installation Type` 창에서 `Install from Internet` 선택
  3. `Choose download Site(s)` 창에서 첫 항목 선택
  4. `Select Packages` 창에서
     `Package` 열 값이 `qgis-full: QGIS Full Desktop (meta Packages for express install)`인 행을 찾고,
     해당 행의 `New` 열에 보이는 작은 아이콘을 반복적으로 눌러서
     <b>`3.12-1`</b> 값이 나오도록 하고 `다음`으로 진행
  5. 모든 `Agreement of Restrictive Package` 창에서 체크 선택하고 `다음`으로 진행
- 설치 결과 확인
  - 바탕화면에 `OSGeo4W` 폴더가 생성되고, 그 안에 `OSGeo4W Shell` 아이콘이 생성됨
  - `OSGeo4W Shell` 실행하면, 커맨드 창이 열리고, `o-help` 입력하면 도움말이 출력됨
  - `OSGeo4W Shell`에서 `gdalinfo --help-general` 및 `gdalinfo --version` 등의 명령 실행
  - 우리 실습에서는 gdal300.dll 파일의 위치를 장고에게 알려줘야 함
    ```PYTHON {.line-numbers}
    # nearbyshops/settings.py
    # ...
    GDAL_LIBRARY_PATH = r'C:\OSGeo4W64\bin\gdal300'
    ```
  - 다양한 Desktop 앱이 설치됨
    ![](../OSGeo4W.png)
    - `QGIS Desktop` 활용에 관해서는 아래를 참고
      - [QGIS 예제와 팁](http://www.qgistutorials.com/ko/)
      - [QTiles로 베이스 맵 만들기](http://www.qgistutorials.com/ko/docs/creating_basemaps_with_qtiles.html)
      - [Web Mapping with QGIS2Web](http://www.qgistutorials.com/ko/docs/web_mapping_with_qgis2web.html)
    - `Qt Designer` 활용에 관해서는 [초보자를 위한 Python GUI 프로그래밍 - PyQt5](https://wikidocs.net/book/2944) 참고

### 2.2 PostgreSQL 설치 및 설정
- 원저에서는 Docker 도구에 PostgreSQL을 설치하지만,
- 본 실습에서는 Desktop에 직접 PostgreSQL을 설치하여 진행함
- PostgreSQL을 활용한 지리 정보 검색 예제는 [여기 한글 자료](https://www.joinc.co.kr/w/man/12/spatial)를 참고

<b>2.2.1 설치</b>
- [PostgreSQL 공식 웹사이트](https://www.postgresql.org/download/windows/)
[EntrepriseDB’s website](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)에서 다운로드
- 설치 과정에서 디폴트 로케일은 korean으로 선택
- 설치 마지막 단계에서 `Stack Builder 4.1.0` 창에서
  추가 도구 설치 여부를 물어보면,
  `PostGIS Bundle for PostgreSQL 10` 체크하여 PostGIS 설치 진행
![](https://miro.medium.com/max/569/0*uipJ9lvFQH9f_xDt.png)
![](https://miro.medium.com/max/628/0*VUrNO6TOXYdEXnWt.png)
- PostGIS 설치 과정에서 `Create a spatial database` 선택하고,
  user는 기본값 'postgres' 그대로,
  비번 입력하고,
  DB Name은 'my-database'로 진행
![](https://miro.medium.com/max/515/0*DN7jYJ5gxHwhKNUc.png)
- 추가적인 질문에 모두 'yes' 응답
- 시스템 환경 변수 PATH에 'C:\Program Files\PostgreSQL\10\bin' 추가 등록
![](https://miro.medium.com/max/430/0*U5iibRC5Q7H1-h75.png)

<b>2.2.2 설정</b>
- cmd 명령 프롬프트 실행하여 작업
```SHELL {.line-numbers}
# PostgreSQL에 사용자 'postgres'로 로그인
$ psql -U postgres
# 비밀번호 입력하면, 프롬프트 나타남

# 아래 작업은 불필요함(?)
# # 계정 생성 개별 사용자 아이디 및 비번 등록
# CREATE USER <my-user> WITH PASSWORD ‘<my-password>’;
#
# # GIS DB 'my-database'의 소유권을 개별 사용자에게 등록
# ALTER DATABASE 'my-database' OWNER TO <my-user>;

# DB 목록 조회
\list+
# 계정 목록 조회
\du+
```
### 2.3 가상환경 준비
```SHELL {.line-numbers}
# 설치할 패키지 지정하여 가상환경 생성
$ conda create --name vnv_geo python geos psycopg2 django

# 설치된 패키지 목록을 파일로 저장
$ conda list --name vnv_geo --explicit > vnv_geo.txt

# 설치된 패키지 목록이 저장된 파일로 가상환경 생성
$ conda create --name vnv_geo --file vnv_geo.txt
```
설치된 패키지 목록이 저장된 파일은 [여기](../vnv_geo.txt)에서 다운로드 가능함

### 2.4 파이참 프로젝트 생성
- `c:\geo` 위치에 `geo`라는 파이참 프로젝트를 생성
- 가상환경을 vnv_geo로 지정

## 3. 장고 프로젝트 생성
- vnv_geo 가상환경이 활성화된 파이참 터미널에서 장고 프로젝트 생성
```SHELL {.line-numbers}
(vnv_geo) C:\geo>django-admin.py startproject nearbyshops .
```
- DB 설정
```PYTHON {.line-numbers}
# nearbyshops/settings.py
# ...
DATABASES = {
    'default': {
        'ENGINE': 'django.contrib.gis.db.backends.postgis',
        'NAME': 'my-database',
        'USER': 'postgres',
        'PASSWORD': '<비번>',
        'HOST': 'localhost',
        'PORT': '5432'
    }
}
```
- GeoDjango 앱 등록
```PYTHON {.line-numbers}
# nearbyshops/settings.py
# ...
INSTALLED_APPS = [
    # ...
    'django.contrib.gis',
]
```

## 4. 장고 앱 생성
### 4.1 앱 생성
```SHELL {.line-numbers}
(vnv_geo) C:\geo>python manage.py startapp shops
```
### 4.2 앱 등록
```PYTHON {.line-numbers}
# nearbyshops/settings.py
# ...
INSTALLED_APPS = [
    # ...
    'shops',
]
```
### 4.3 모델 정의
- [PointField](https://docs.djangoproject.com/en/3.0/ref/contrib/gis/model-api/#pointfield)
  - GeoDjango에서 사용하는 기하학적 필드
  - ()위도, 경도) 좌표를 표현하는 [GEOS Point](https://docs.djangoproject.com/en/3.0/ref/contrib/gis/geos/#django.contrib.gis.geos.Point) 객체를 저장
- `from django.contrib.gis.db import models`
  - `django.contrib.gis.db`로부터 `models`를 임포트 하고 있음에 주목
  - 일반적으로는 `django.db`로부터 `models`를 임포트 함
```PYTHON {.line-numbers}
# shops/models.py
from django.contrib.gis.db import models

class Shop(models.Model):                     # 상점
    name = models.CharField(max_length=100)     # 이름
    location = models.PointField()              # 위치(위도, 경도)
    address = models.CharField(max_length=100)  # 주소
    city = models.CharField(max_length=50)      # 시 (소재지)
```
### 4.4 DB 테이블 생성
DB 생성에 관한 좋은 문서로서, [Django Migrations: A Primer](https://realpython.com/django-migrations-a-primer/) 참고
```SHELL {.line-numbers}
(vnv_geo) C:\geo>python manage.py makemigrations
(vnv_geo) C:\geo>python manage.py migrate
```
### 4.5 수퍼 유저 생성
```SHELL {.line-numbers}
(vnv_geo) C:\geo>python manage.py createsuperuser
```
### 4.6 어드민 기능에 모델 등록
- [장고 어드민 애플리케이션](https://docs.djangoproject.com/en/3.0/ref/contrib/admin/)은 데이터 관리를 위한 CRUD 인터페이스를 제공함
- GeoDjango가 장고 어드민 애플리케이션을 확장하여 지리 필드 작업을 지원함
- `Shop` 모델을 어드민 페이지에서 관리하려면, 우선 등록이 필요함
  ```PYTHON {.line-numbers}
  # shops/admin.py
  from django.contrib.gis.admin import OSMGeoAdmin
  from django.contrib import admin
  from .models import Shop

  @admin.register(Shop)
  class ShopAdmin(OSMGeoAdmin):
      list_display = ('name', 'location')
  ```
- [@admin.register](https://docs.djangoproject.com/en/3.0/ref/contrib/admin/#the-register-decorator) 장식자를 통하여 `Shop` 모델을 어드민 앱에 등록
  - 우리가 배웠던 어드민 등록 [방식](https://docs.djangoproject.com/ko/3.0/intro/tutorial07/)과 다름
  - Model Admin 등록법에 관해 잘 정리한 [초보몽키의 기사](https://wayhome25.github.io/django/2017/03/22/django-ep8-django-admin/)를 강추
  - 장식자로 장식된 클래스 `ShopAdmin`은 어드민 인터페이스에서 `Shop` 모델을 대표함
  - 어드민 인터페이스에서 출력할 특정 필드를 `list_display` 튜플로 지정하는 등의 맞춤화가 가능함
  - 장식자에 대한 심화 학습은 영문 자료 [Primer on Python Decorators](https://realpython.com/primer-on-python-decorators/)를 추천
- `from django.contrib.gis.admin import OSMGeoAdmin`
  - `Shop` 모델에 GeoDjango 필드가 포함되어 있으므로,
    특별히 `OSMGeoAdmin`를 임포트해야 하는데,
    이는 `django.contrib.gis.admin` 팩키지로부터 가져올 수 있음
  - `OSMGeoAdmin` 대신에 `GeoModelAdmin`를 사용할 수도 있음
  - `OSMGeoAdmin`은 `GeoModelAdmin`을 상속받은 파생 클래스임
    - OSM은 Open Street Map을 의미하며,
    영국의 비영리 기구인 OSM 재단이 운영하고 있으며,
    오픈 소스 방식의 참여형 무료 지도 서비스를 제공함
    - [Open Street Map](https://www.openstreetmap.org/)에서 우리 대학 검색해보면,
    구글 지도보다 좋은 듯 ...
  - 어드민에서 지리 필드를 출력할 때
    - `OSMGeoAdmin`은 [Open Street Map](https://www.openstreetmap.org/) 레이어를 사용
    - `GeoModelAdmin`은 [Vector Map Level 0](https://earth-info.nga.mil/publications/vmap0.html)를 사용
    - `OSMGeoAdmin`이 `GeoModelAdmin`보다 더욱 상세한 정보를 제공
### 4.7 장고 서버 가동
```SHELL {.line-numbers}
(vnv_geo) C:\geo>python manage.py runserver
```
- localhost:8000/admin 접속
![](https://files.realpython.com/media/Screenshot_from_2018-11-28_21-22-03.34e252c9266a.png)
- `Add shop` 화면
  - `Location` 지리 필드가 인터액티브 지도로 출력됨
  - 지도 확대/축소 가능
![](https://files.realpython.com/media/Screenshot_from_2018-11-28_21-12-25.2e7a3ff3f939.png)

### 4.8 서울 상점 데이터 획득
- 수동 등록이 아니라 데이터 마이그레이션 작업을 통한 자동 등록
- 데이터 마이그레이션에 관한 영문 자료 [Data Migrations](https://realpython.com/data-migrations/) 추천
- [OpenStreetMap](http://www.openstreetmap.org/)의 [overpass turbo](https://overpass-turbo.eu/)를 활용하여 현실 데이터를 획득
  - overpass turbo는 OpenStreetMap에 대한 웹 기반 데이터 검색 도구
  - [Overpass API](https://wiki.openstreetmap.org/wiki/Overpass_API) 쿼리를 써서 OSM 지도의 특정 요소만 검색하고, 지도 상에서 확인/검토 가능함
  - 통합 마법사 [Wizard](http://wiki.openstreetmap.org/wiki/Overpass_turbo/Wizard)를 활용하여 쿼리 생성을 쉽게 수행 가능함
- 우리 실습에서는 [overpass turbo](https://overpass-turbo.eu/)에서 `Wizard` 버튼을 활용
  - `Query Wizard` 창에 'shop in Seoul' 입력하고, `build and run query` 단추 클릭하고, 생성된 쿼리 문장 감상
  ![](https://files.realpython.com/media/Screenshot_from_2018-11-09_22-55-41.7a5b7e60974c.png)
  - `Export` 단추 클릭하여 보이는 `Export` 창에서,
  `download/copy as raw OSM data` 링크로 'export.json' 파일 다운로드 받은 후,
  (프로젝트 루트 폴더에) 'geo/data.json' 파일로 저장
  ![](https://files.realpython.com/media/Screenshot_from_2018-10-19_02-25-43.ac6770d6a956.png)
  - `Export` 창에서 `Map` 메뉴를 열어 `as interactive Map` 링크 클릭하여 서울 또는 우리 학교 근방의 상점 위치를 확인
  - 파이참에서 'geo/data.json' 파일을 열어 감상
    - `elements`라는 사전형 데이터의 리스트
    - 내부에 `lat`(위도), `lon`(경도) 및 `tags`(name & shop) 키에 주목
  ![](https://files.realpython.com/media/Screenshot_from_2018-10-19_02-34-34.dce4b6e8d898.png)
- Overpass 쿼리에 대한 사용법은 영문 [위키](https://wiki.openstreetmap.org/wiki/Overpass_API/Overpass_QL)
- 'overpass 쿼리'로 구글링한 결과는 별로(?)이지만,
  [오픈스트리트맵의 검색과 내려받기 (QGIS3) — QGIS Tutorials](http://www.qgistutorials.com/ko/docs/3/downloading_osm_data.html) 기사는 참고할 만함

### 4.9 서울 상점 데이터를 DB로 적재

```PYTHON {.line-numbers}
```
```PYTHON {.line-numbers}
```
```PYTHON {.line-numbers}
```
```PYTHON {.line-numbers}
```
```PYTHON {.line-numbers}
```
  -


## 4. 결론


GDAL_LIBRARY_PATH = r'C:\OSGeo4W64\bin\gdal300'
