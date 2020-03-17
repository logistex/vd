# [한국 지도 시각화하기 및 gps 표시 (D3.js v5를 이용하여)](https://dev-shin.tistory.com/m/entry/한국-지도-시각화하기-및-gps-표시-D3js-v5를-이용하여)

- 준비
```SHELL {.line-numbers}
# 콘다 가상환경 준비 ...
conda info --envs
conda activate vnv_dj
# (python=3.7.1 django=2.1.3)

# 파이참 프로젝트 `c:\d3map` 생성 ...

# 장고 프로젝트 `d3` 생성
django-admin startproject d3 .

# 장고 앱 `d3_korean_map` 생성
python manage.py startapp d3_korean_map
```

- 우리나라 지도 경계선 [JSON 데이터 파일](https://raw.githubusercontent.com/southkorea/southkorea-maps/master/kostat/2018/json/skorea-provinces-2018-topo-simple.json)을 `BASE_DIR` 폴더에 다운받기

- 접속 경로 정의
```PYTHON  {.line-numbers}
# d3/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('map/', include('d3_korea_map.urls'))
]
```

```PYTHON  {.line-numbers}
# d3_korean_map/urls.py
# from django.contrib import admin
from django.urls import path, include
# from d3_korea_map.map import show_korea_map
from . import views

urlpatterns = [
    path('', views.show_korea_map, name='KoreaMap'),
]
```

- 뷰 정의
```PYTHON  {.line-numbers}
# d3_korean_map/views.py
from django.http import HttpResponse
from django.template import loader


def show_korea_map(request):
    def get():
        template = loader.get_template('map/main.html')
        return HttpResponse(template.render())

    if request.method == 'GET':
        return get()
    else:
        return HttpResponse(status=405)
```

```PYTHON  {.line-numbers}
# d3_korea_map/map.py

```

```PYTHON  {.line-numbers}
# d3_korea_map/map.py

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
