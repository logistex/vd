# 장고에서 Mapbox 지도 출력
[How to Add Maps to Django Web App Projects with Mapbox](https://www.fullstackpython.com/blog/maps-django-web-applications-projects-mapbox.html)

```SHELL {.line-numbers}
# 콘다 가상환경 준비 ...
conda info --envs
# conda remove --name vnv_mb --all
conda create --name vnv_mb django
# (python=3.8.1 django=3.0.3)
conda activate vnv_mb

# 파이참 프로젝트 `c:\mapbox` 생성 ...

# 장고 프로젝트 `djmaps` 생성
django-admin startproject djmaps .

# 장고 앱 `maps` 생성
python manage.py startapp maps
```

```PYTHON  {.line-numbers}
# djmaps/settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'maps',                       # !!!
]
```

```PYTHON  {.line-numbers}
# djmaps/djmaps/urls.py
from django.conf.urls import include
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('', include('maps.urls')),
    path('admin/', admin.site.urls),
]
```

```PYTHON  {.line-numbers}
# maps/urls.py
from django.conf.urls import url
from . import views

urlpatterns = [
    url(r'', views.default_map, name="default"),
]
```

```PYTHON  {.line-numbers}
# maps/views.py
from django.shortcuts import render

def default_map(request):
    return render(request, 'default.html', {})
```

```HTML  {.line-numbers}
<!--maps/templates/default.html-->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Interactive maps for Django web apps</title>
</head>
<body>
    <h1>Map time!</h1>
</body>
</html>
```

runserver
![](https://www.fullstackpython.com/img/180519-django-maps/map-time.png)

## Mapbox를 활용하여 지도 추가

- [mapbox.com](https://www.mapbox.com/) 홈페이지로 이동
![](https://www.fullstackpython.com/img/180519-django-maps/mapbox-homepage.jpg)
- "Get Started for free" 클릭
![](https://www.fullstackpython.com/img/180519-django-maps/sign-up.jpg)
- 회원 가입 또는 로그인
![](https://www.fullstackpython.com/img/180519-django-maps/add-mapbox.png)
- "JS Web" 클릭
![](https://www.fullstackpython.com/img/180519-django-maps/method-installation.png)
- "Use the Mapbox CDN"을 선택
- 다음 두 화면에서 코드를 복사해서 `maps/templates/default.html` 파일에 붙여넣기
```HTML  {.line-numbers}
<!--maps/templates/default.html-->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Interactive maps for Django web apps</title>
    <!--첫 화면의 두 줄을 복사하여 이곳에 붙여넣기-->
</head>
<body>
    <h1>Map time!</h1>
    <!--둘째 화면의 코드를 복사하여 이곳에 붙여넣기-->
</body>
</html>
```
- 뷰 수정
```PYTHON  {.line-numbers}
# maps/views.py
from django.shortcuts import render

def default_map(request):
    # TODO: move this token to Django settings from an environment variable
    # found in the Mapbox account settings and getting started instructions
    # https://www.mapbox.com/account/ 에서 "Access tokens" 섹션에 나오는 "Default public token" 값을 복사하여 아래 코드의 `pk.my_mapbox_access_token` 부분에 붙여넣는다.
    mapbox_access_token = 'pk.my_mapbox_access_token'
    return render(request, 'default.html',
                  { 'mapbox_access_token': mapbox_access_token })
```
- runserver 수행 후 지도 확인
- `default.html`에서 div#map의 width를 100%로 수정 후, 브라우저 갱신
- 지도 위에서 마우스 휠 스크롤하여 확대/축소
- 지도 위를 클릭하고 드래그하여 위치 조정

## 지도 설정
- `default.html`에서 style 수정 및 center, zoom 추가
```HTML  {.line-numbers}
    style: 'mapbox://styles/mapbox/streets-v10',
    center: [127.049121, 37.558658], <!--[경도, 위도]-->
    zoom: 16			     <!--기본값 0보다 확대-->
```
- `style: 'mapbox://styles/mapbox/streets-v9'` 시도
- 상세한 지도 설정 변수는 [Mapbox GL JS API documentation](https://www.mapbox.com/mapbox-gl-js/api/) 참고
- `default.html`에서 `mapbox://styles/mapbox/satellite-streets-v10`로 수정하여 위성 사진 보기
- `default.html`에서 `bearing: 90` 추가하여 지도 회전하기
```HTML  {.line-numbers}
    style: 'mapbox://styles/mapbox/satellite-streets-v10',
    center: [127.049121, 37.558658],
    zoom: 16,
    bearing: 90
```

## 정리 및 과제
- 인터액티브 자바스크립트-기반 지도를 장고 웹 앱에 추가하였음
- 지도 스타일 조정
- Mapbox가 제공하는 추가적 API 공부에 도전
  - Directions(네비게이션 기능)
  - Map Matching(위치 추적하여 지도 매칭)
  - Geocoding(주소로 좌표 찾기)
- 분석형 지도에 도전
  - 위치 지정 마커 표시하기
  - scatter map
  ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FVIvuv%2Fbtqzy5OkahV%2FKpkQfzykYUB7pp4z6gncck%2Fimg.png)
  - choropleth map (단계 구분 지도)
  ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FdQlAGZ%2FbtqzyhVZPwK%2FYCVKaALqk0Zese565yZb1k%2Fimg.png)
  - heat map
  ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FbDzM3D%2FbtqzyXXkEPD%2FHixH928kerKkDEoRopiIFK%2Fimg.jpg)

## 참고 자료
장고 지도 표시에 관한 참고 자료는 [여기](../map_ref.md) 참조
