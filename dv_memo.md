# 데이터 시각화(data visualization)

## 수업 자료 [다운로드](https://github.com/logistex/vd)
- 링크에 접속하여 `Clone or download` 단추 클릭하고, `download ZIP` 클릭
- 다운로드된 `dv-master.zip` 파일을 압축해제하고, 작업 폴더로 이동

## [아나콘다 설치](./anaconda.md)

## 가상환경 활용 (아무 폴더에서나)
```
$ cd \somewhere\to\work              # 작업 폴더로 이동
$ conda create -n vnv_dv python=3.8  # vnv_dv 가상환경 생성

$ conda activate vnv_dv              # 가상환경 활성화
$ python --versions                  # 파이썬 버전 확인
...                                  # 작업 수행
# conda Deactivate                   # 가상환경 비활성화
```

## Jupyter Notebook (쥬피터 랩 사용을 권고)
```
$ jupyter notebook
```

## Jupyter Lab
- 쥬피터 노트북보다 개선된 신품
- 작동법
```
# 작업 폴더에서,
$ conda activate vnv_dv             # 일단 가상환경 활성화
$ conda install jupyterlab          # 가상환경 내부에서 설치
$ jupyter lab                       # 가상환경 내부에서 실행
```
- 본 강의 노트 `dv_memo.md`를 열어보기
- `/DataScience/source_code/01. 인구대비 CCTV 설치량 분석.ipynb` 열어보기

## git 작업
### 0) git [설치 안내서](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%84%A4%EC%B9%98)
- [GitHub Desktop 웹사이트](http://desktop.github.com/)
- [GitHub Desktop 설치 및 다운로드](https://gocoder.tistory.com/1549)

### 1) 최초 준비 (git 대상 로컬 폴더에서 `Git Bash here`)
- 초기화
```bash {.line-numbers}
$ git init
$ git config --global user.name "Your Name"
$ git config --global user.email you@example.com
```

- .gitignore 파일 작성
```
.git
.ipynb_checkpoints
```

- 로컬 add/commit
```
$ git status
$ git add --all .
$ git commit -m "first commit"
```

- GitHub.com 저장소 준비
  - 계정 생성
  - new repository "VisualizeData" 생성

- 리모트 add 및 push
```
$ git remote add origin https://github.com/<your-github-username>/VisualizeData.git
$ git push -u origin master
```

### 2) 2차 이후 배포 (push)
```
$ git status
$ git add --all .
$ git status
$ git commit -m "Changed the HTML for the site."
$ git push
```

## 도서 자료
- 파이썬 데이터 분석 계열
  - 모두의 데이터 과학 with 파이썬 http://m.yes24.com/Goods/Detail/43633333
  - 모두의 데이터 분석 with 파이썬 http://m.yes24.com/Goods/Detail/72227684
  - <b>파이썬으로 데이터 주무르기</b> 독특한 예제를 통해 배우는 데이터 분석 입문 http://www.yes24.com/Product/Goods/57670268
- R 데이터 분석 계열
  - Do it! 쉽게 배우는 R 데이터 분석 http://www.yes24.com/Product/Goods/43868089
  - IT CookBook, R로 배우는 데이터 과학 http://www.hanbit.co.kr/store/books/look.php?p_code=B2093037271
  - 제대로 알고 쓰는 R 통계분석 http://www.hanbit.co.kr/store/books/look.php?p_code=B7014039221
- 인포그래픽 계열
  - <b>Visualize This 비주얼라이즈 디스</b> [빅데이터 시대의 데이터 시각화+인포그래픽 기법] http://acornpub.co.kr/book/visualize-this
  - <b>월스트리트저널 인포그래픽 가이드</b> http://www.yes24.com/Product/Goods/12292773
  - 좋아 보이는 것들의 비밀, 인포그래픽 정보로 소통하는 비주얼 스토리텔링 http://www.yes24.com/Product/goods/23452983

## 강좌 자료
- 빅데이터 분석 결과 시각화 e-koreatech https://e-koreatech.step.or.kr/page/lms/?m1=course&m2=course_detail&course_id=100039
- 뉴스젤리 http://newsjel.ly/
- 유용한 '데이터 시각화' 정보 사이트 모음 https://www.bloter.net/archives/369220

## 장고 데이터 시각화
- Django Packages in charts https://djangopackages.org/grids/g/charts/
- 장고에서 차트그리기 https://dowtech.tistory.com/3
- Django Dashboard - Learn by Coding https://dev.to/sm0ke/django-dashboard-learn-by-coding-437l
- Adding charts to Django admin - https://findwork.dev/blog/adding-charts-to-django-admin/
- The Best Python Data Visualization Libraries - FusionBrew - The FusionCharts Blog - https://www.fusioncharts.com/blog/best-python-data-visualization-libraries/
- Integrating Bokeh visualisations into Django Projects. - By - https://hackernoon.com/integrating-bokeh-visualisations-into-django-projects-a1c01a16b67a
- Beautiful Visual Charts in Django - Better Programming - Medium - https://medium.com/better-programming/prettify-python-django-with-beautiful-visual-charts-836fe6646305
- How To Create Charts In Django - https://www.fusioncharts.com/blog/creating-charts-in-django/
- Django and R on Heroku | R-bloggers - https://www.r-bloggers.com/django-and-r-on-heroku/
- Django and R: Using Open Source Database and Statistical Tools for Efficient Scientific Data Evaluation and Analysis | Request PDF - https://www.researchgate.net/publication/266114045_Django_and_R_Using_Open_Source_Database_and_Statistical_Tools_for_Efficient_Scientific_Data_Evaluation_and_Analysis
- How do you use R in Python to return an R graph through Django? - Stack Overflow - https://stackoverflow.com/questions/32697469/how-do-you-use-r-in-python-to-return-an-r-graph-through-django
-
## 파이썬 데이터 시각화
- The 25 Best Data Visualizations of 2019 | Visual Learning Center by Visme - https://visme.co/blog/best-data-visualizations/
- The Python Graph Gallery – Visualizing data – with Python - https://python-graph-gallery.com/
- The Data Visualisation Catalogue - https://datavizcatalogue.com/
- Data Viz Project | Collection of data visualizations to get inspired and finding the right type. - https://datavizproject.com/
- Data visualization - Material Design - https://material.io/design/communication/data-visualization.html#behavior

- Python에서 데이터 시각화하는 다양한 방법 · 어쩐지 오늘은 - https://zzsza.github.io/development/2018/08/24/data-visualization-in-python/
- 9 Data Visualization Tools That You Cannot Miss in 2019 - https://towardsdatascience.com/9-data-visualization-tools-that-you-cannot-miss-in-2019-3ff23222a927
- Introduction to Data Visualization in Python - Towards Data Science - https://towardsdatascience.com/introduction-to-data-visualization-in-python-89a54c97fbed
- 10 Useful Python Data Visualization Libraries for Any Discipline - https://mode.com/blog/python-data-visualization-libraries/
- Top 5 Python Libraries For Data Visualization - https://analyticsindiamag.com/top-5-python-libraries-for-data-visualization/
- Interactive Data Visualization in Python With Bokeh – Real Python - https://realpython.com/python-data-visualization-bokeh/
- Data Visualization with Python | Coursera - https://ko.coursera.org/learn/python-for-data-visualization
- 유용한 '데이터 시각화' 정보 사이트 모음 | Bloter.net - http://www.bloter.net/archives/369220

- [Handbook_of_Data_Visualization.pdf](./Handbook_of_Data_Visualization.pdf)

## 쥬피터 노트북
- jupyterhub https://github.com/jupyterhub/jupyterhub
- jupyterhub Getting Started https://github.com/jupyterhub/jupyterhub
- [191113 Tutorial Jupyter Notebook: The Definitive Guide (article) - DataCamp](https://www.datacamp.com/community/tutorials/tutorial-jupyter-notebook)
- [170511 IPython Or Jupyter? (article) - DataCamp](https://www.datacamp.com/community/blog/ipython-jupyter)
- https://colab.research.google.com/notebooks/intro.ipynb

## 영상 자료
- Hans Rosling: The best stats ever seen https://www.ted.com/talks/hans_rosling_the_best_stats_you_ve_ever_seen#t-291883
- David McCandless: The beauty of data visualization - TED Talks https://www.ted.com/talks/david_mccandless_the_beauty_of_data_visualization
- Aaron Koblin: Visualizing ourselves … https://www.ted.com/talks/aaron_koblin_visualizing_ourselves_with_crowd_sourced_data
- 5 Great TED Talks about DataViz https://coolinfographics.com/blog/2016/10/10/5-great-ted-talks-about-dataviz.html

## 신종 코로나
- 신종 코로나바이러스, 현황 "한 눈에 쉽게" 확인하는 법 http://www.biotimes.co.kr/news/articleView.html?idxno=2426
- 존스 홉킨스 시스템 과학/공학 센터 https://gisanddata.maps.arcgis.com/apps/opsdashboard/index.html#/bda7594740fd40299423467b48e9ecf6
- 이동훈(27) 경희대 https://coronamap.site
- 홍준수(21) 호주 멜버른 대락교 https://coronamap.live
- 신종 코로나 바이러스 맵 http://corona.paullab.synology.me

## [Markdown for Jupyter notebooks cheatsheet](https://www.ibm.com/support/knowledgecenter/SSHGWL_1.2.3/analyze-data/markd-jupyter.html)
- atom에서는 안되고, 쥬피터 노트북에서만 작동함
- Blue boxes (alert-info)
  <div class="alert alert-block alert-info">
    <b>Tip:</b> Use blue boxes (alert-info) for tips and notes.
    If it’s a note, you don’t have to include the word “Note”.
  </div>

- Yellow boxes (alert-warning)
  <div class="alert alert-block alert-warning">
    <b>Example:</b> Use yellow boxes for examples that are not
    inside code cells, or use for mathematical formulas if needed.
  </div>

- Green boxes (alert-success)
  <div class="alert alert-block alert-success">
    <b>Up to you:</b> Use green boxes sparingly, and only for some specific
    purpose that the other boxes can't cover. For example, if you have a lot
    of related content to link to, maybe you decide to use green boxes for
    related links from each section of a notebook.
  </div>

- Red boxes (alert-danger)
  <div class="alert alert-block alert-danger">
    <b>Just don't:</b> In general, avoid the red boxes. These should only be
    used for actions that might cause data loss or another major issue.
  </div>


## 서울시 인구 대비 CCTV 대수 분석
#### 1) 쥬피터 랩에서 노트북 내용 1차 실행
- 아나콘다 파워쉘 프롬프트 실행
- 가상환경 활성화
```
$ conda info --envs             # 가상환경 정보 확인
$ conda activate vnv_dv         # 활성화

# 필요한 모듈 설치
$ conda install pandas
$ conda install numpy
$ conda install matplotlib
# $ conda install xlrd

# 쥬피터 랩 기동
$ jupyter lab
```
- 쥬피터 랩에서
  `DataScience/source_code/01. 인구대비 CCTV 설치량 분석.ipynb` 노트북 파일을 선택하여 열고, 메뉴 `Run > Run All Cells` 실행
- 엑셀 파일 읽기 오류
  - 프롬프트 창에서 작동 중인 쥬피터 랩을 `CTRL+C` 입력하여 중지
  - 'xlrd' 설치 후, 다시 랩 시작
```
$ conda install xlrd
$ jupyter lab
```
#### 2) 쥬피터 랩에서 노트북 내용 2차 실행
- 쥬피터 랩에서
  `DataScience/source_code/01. 인구대비 CCTV 설치량 분석.ipynb` 노트북 파일을 선택하여 열고, 메뉴 `Run > Run All Cells` 실행하면,
  잘 실행됨
- 노트북 끝으로 이동해서 비디오 시청

#### 3) 가상환경 다루기 연습
- 가상환경에 설치된 내역을 파일로 저장하고 활용
```
# 현재 vnv_dv 활성화된 상태라고 가정하고
$ conda list                              # 설치된 패키지 내역 확인
$ conda env export > requirements.yml     # 내용 확인 (!!! utf8로 변경 !!!)
$ conda remove xlrd                       # 특정 패키지 삭제
$ conda list                              # 삭제된 패키지 내역 확인
$ conda deactivate                        # 비활성화

# 현재 열려 있는 프롬프트 창을 닫았다가 다시 열고
$ conda env list                          # 가상환경 목록 확인
$ conda remove -n vnv_dv --all            # 가상환경 삭제
$ conda env list                          # 삭제된 상황 확인
$ conda env create -f ./requirements.yml  # 가상환경 재설치 (!!! utf8로 변경 !!!)
$ conda env list                          # 재설치된 가상환경 확인
```
- 다시 가상환경 활성화하고, 랩 기동 후,
- 노트북 처음으로 이동해서 수업 시작
