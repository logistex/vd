# ﻿[anaconda 설치](https://wonderbout.tistory.com/22)

### 설치 파일 다운로드
- https://www.anaconda.com/download/
- Windows, Python 3.7 version, 64-Bit Graphical Installer
### 설치 파일 실행
- `다운로드\Anaconda3-2019.10-Windows-x86_64.exe` 실행
- 대부분 'I Agree' 또는 'Next' 단추 클릭
- Install for 'Just Me' (recommended)
- Destination Folder 'C:\Anaconda3'
- 'Add Anaconda to my PATH environment variable' (기본값대로 체크 해제)
- 'Register Anaconda as my default Python 3.7' (기본값대로 체크)
- 'Install Microsoft VSCode' skip
- Finish
### 설치 사항 확인
- 윈도우 시작 메뉴에 'Anaconda3 (64-bit)' 폴더 및 메뉴 항목 확인
- 윈도우 시작 메뉴에서 'Anaconda Powershell Prompt (Anaconda3)' 실행
```
(base) PS C:\Users\logis> python --version
Python 3.7.4
```
### Getting started with Anaconda
- Anaconda Navigator (Anaconda3) 실행 (오래 걸려요 ...)
- Spyder 3.3.6
    - heollo.py 파일을 작성하고 런 실행
    - Spyder 종료
- Jupyter Notebook
    - 'C:\Users\logis\' 폴더가 브라우즈 됨
    - Document 폴더로 진입
    - `New > Python 3` 버튼으로 새 노트북 생성
    - In 셀에서 `print('Hello Notebook!')` 입력 후, `CTRL+Enter` 입력하여 실행
    - 노트북 이름을 'Hello'로 변경
    - 저장된 'Hello.ipynb' 파일 확인
    - 노트북 종료
- Anaconda Prompt 활용하여 파이썬 프로그램 작성
    - 시작 메뉴에서 'Anaconda Prompt' 또는 'Anaconda Powershell Prompt' 실행
    - 'Anaconda Prompt' 또는 'Anaconda Powershell Prompt' 종료
```
(base) C:\Users\logis>python
Python 3.7.4 (default, Aug  9 2019, 18:34:13) [MSC v.1915 64 bit (AMD64)] :: Anaconda, Inc. on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> print('Hello Anaconda!')
Hello Anaconda!
>>> exit()
(base) C:\Users\logis>
```
- 'Anaconda Prompt' 또는 'Anaconda Powershell Prompt'에서
    - `spyder` 입력하고 엔터 쳐서 스파이더 실행
    - `jupyter notebook` 입력하고 엔터 쳐서 쥬피터 노트북 실행
    - `jupyter lab` 입력하고 엔터 엔터 쳐서 쥬피터 랩 실행
### 아나콘다 업데이트
- 'Anaconda Powershell Prompt'에서
```
# 아나콘다 버전 확인
(base) PS C:\Users\logis> conda --version
conda 4.8.2
# 아나콘다 자체를 업데이트
(base) PS C:\Users\logis> conda update conda
# 아나콘다 파이썬 패키지 전체를 업데이트
(base) PS C:\Users\logis> conda update --all  # 경우에 따라 두 번 실행
```
- Conda
  - 패키지 관리 시스템
  - 환경 관리 시스템
  - pip(패키지 관리자) 및 venv(환경 관리자) 두 기능을 통합한 개념
  - [venv, virtualenv, conda, pyenv](https://wikidocs.net/16402)
  - [Pipenv vs virtualenv vs conda environment](https://medium.com/@krishnaregmi/pipenv-vs-virtualenv-vs-conda-environment-3dde3f6869ed)
  - [pyenv, conda, virtualenv, pip, autoenv](http://egloos.zum.com/mcchae/v/11271948)
  - [Environment management with Conda](https://angus.readthedocs.io/en/2019/conda_tutorial.html)
  - [The Definitive Guide to Conda Environments](https://towardsdatascience.com/a-guide-to-conda-environments-bc6180fc533)
  - [Conda vs. pip vs. virtualenv commands](https://conda.io/projects/conda/en/latest/commands.html#conda-vs-pip-vs-virtualenv-commands)
- Conda 가상환경 활용
  - `venv`(파이썬 가상환경 관리자)로 가상환경을 만들 때는 가상환경을 저장할 폴더를 지정했었음
    `% python3 -m venv /path/to/new/environment`
  - Conda 가상환경은 저장 폴더를 지정하지 않고 생성하며, 실제 저장되는 위치는
    아나콘다 설치 폴더 하위의 `envs` 폴더에 생성됨
  - `venv`에서는 가상환경을 삭제하는 명령이 없고, 비활성화된 상태에서 폴더를 삭제하면 됨
  - Conda 가상환경은 가상환경을 삭제하는 명령이 별도로 존재함, 비활성화 된 상태에서
    `% conda remove my_venv`
```
# 가상환경 생성 (아무 폴더에서나)
% conda create --name conda-env python
% conda create -n conda-env python=3.7
% conda create -n conda-env numpy requests
% conda create -n conda-env python=3.7 numpy=1.16.1 requests=2.19.1
# 폴더를 지정하여 가상환경 생성
% conda create --prefix c:/vnv/python38 python=3.8

# 가상환경 활성화
% conda activate conda-env
(conda-env) %

# 가상환경 비활성화
% conda deactivate

# 가상환경 삭제
% conda remove conda-env --all

# 기타 더 상세한 정보는 [The Definitive Guide to Conda Environments] 참조
```
- conda 홈 디렉토리를 작업 폴더로 변경
  - 시작 메뉴에서 `Anaconda Powershell Prompt` 항목을 우 클릭 후,
    `자세히` > `파일 위치 열기` 선택
  - 이렇게 하면
    `C:\Users\logis\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Anaconda3 (64-bit)` 폴더가 탐색기에서 열리는데
  - 여기서 `Anaconda Powershell Prompt` 항목을 우 클릭하여 `속성` 선택하고
  - `시작 위치` 항목의 값 '%HOMEPATH%'를 'c:\myFolder' 형식으로 수정하고 적용 및 확인

```
# 가상환경 생성 (위치 지정)
(base) PS C:\elite> conda create --prefix c:/vnv/python38 python=3.8

# 가상환경 정보 확인
(base) PS C:\elite> conda info --envs
# conda environments:
#
                      *  C:\Anaconda3
base                     C:\anaconda3
                         c:\vnv\python38

# 현재의 파이썬 버전은 3.7
(base) PS C:\elite> python --version
Python 3.7.6

# 가상환경 활성화
(base) PS C:\elite> conda activate c:\vnv\python38

# 가상 환경의 파이썬 버전은 3.8
(c:\vnv\python38) PS C:\elite> python --version
Python 3.8.1

# 가상환경 비활성화
(c:\vnv\python38) PS C:\elite> conda deactivate

# 가상환경 제거
(base) PS C:\elite> conda remove c:\vnv\python38
# 간혹 conda remove 명령에서 오류가 발생할 경우에는 그냥 폴더 강제 삭제
(base) PS C:\elite> rm -r c:\vnv\python38  # -r 옵션

# 가상환경 정보 확인
(base) PS C:\elite> conda info --envs
# conda environments:
#
                      *  C:\Anaconda3
base                     C:\anaconda3
```




  <table class="colwidths-given docutils align-default">
  <colgroup>
  <col style="width: 10%" />
  <col style="width: 30%" />
  <col style="width: 30%" />
  <col style="width: 30%" />
  </colgroup>
  <thead>
  <tr class="row-odd"><th class="head"><p>Task</p></th>
  <th class="head"><p>Conda package and environment manager command</p></th>
  <th class="head"><p>Pip package manager command</p></th>
  <th class="head"><p>Virtualenv environment manager command</p></th>
  </tr>
  </thead>
  <tbody>
  <tr class="row-even"><td><p>Install a package</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">install</span> <span class="pre">$PACKAGE_NAME</span></code></p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">pip</span> <span class="pre">install</span> <span class="pre">$PACKAGE_NAME</span></code></p></td>
  <td><p>X</p></td>
  </tr>
  <tr class="row-odd"><td><p>Update a package</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">update</span> <span class="pre">--name</span> <span class="pre">$ENVIRONMENT_NAME</span> <span class="pre">$PACKAGE_NAME</span></code></p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">pip</span> <span class="pre">install</span> <span class="pre">--upgrade</span> <span class="pre">$PACKAGE_NAME</span></code></p></td>
  <td><p>X</p></td>
  </tr>
  <tr class="row-even"><td><p>Update package manager</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">update</span> <span class="pre">conda</span></code></p></td>
  <td><p>Linux/macOS: <code class="docutils literal notranslate"><span class="pre">pip</span> <span class="pre">install</span> <span class="pre">-U</span> <span class="pre">pip</span></code> Win: <code class="docutils literal notranslate"><span class="pre">python</span> <span class="pre">-m</span> <span class="pre">pip</span> <span class="pre">install</span> <span class="pre">-U</span> <span class="pre">pip</span></code></p></td>
  <td><p>X</p></td>
  </tr>
  <tr class="row-odd"><td><p>Uninstall a package</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">remove</span> <span class="pre">--name</span> <span class="pre">$ENVIRONMENT_NAME</span> <span class="pre">$PACKAGE_NAME</span></code></p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">pip</span> <span class="pre">uninstall</span> <span class="pre">$PACKAGE_NAME</span></code></p></td>
  <td><p>X</p></td>
  </tr>
  <tr class="row-even"><td><p>Create an environment</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">create</span> <span class="pre">--name</span> <span class="pre">$ENVIRONMENT_NAME</span> <span class="pre">python</span></code></p></td>
  <td><p>X</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">cd</span> <span class="pre">$ENV_BASE_DIR;</span> <span class="pre">virtualenv</span> <span class="pre">$ENVIRONMENT_NAME</span></code></p></td>
  </tr>
  <tr class="row-odd"><td><p>Activate an environment</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">activate</span> <span class="pre">$ENVIRONMENT_NAME</span></code>*</p></td>
  <td><p>X</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">source</span> <span class="pre">$ENV_BASE_DIR/$ENVIRONMENT_NAME/bin/activate</span></code></p></td>
  </tr>
  <tr class="row-even"><td><p>Deactivate an environment</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">deactivate</span></code></p></td>
  <td><p>X</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">deactivate</span></code></p></td>
  </tr>
  <tr class="row-odd"><td><p>Search available packages</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">search</span> <span class="pre">$SEARCH_TERM</span></code></p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">pip</span> <span class="pre">search</span> <span class="pre">$SEARCH_TERM</span></code></p></td>
  <td><p>X</p></td>
  </tr>
  <tr class="row-even"><td><p>Install package from specific source</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">install</span> <span class="pre">--channel</span> <span class="pre">$URL</span> <span class="pre">$PACKAGE_NAME</span></code></p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">pip</span> <span class="pre">install</span> <span class="pre">--index-url</span> <span class="pre">$URL</span> <span class="pre">$PACKAGE_NAME</span></code></p></td>
  <td><p>X</p></td>
  </tr>
  <tr class="row-odd"><td><p>List installed packages</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">list</span> <span class="pre">--name</span> <span class="pre">$ENVIRONMENT_NAME</span></code></p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">pip</span> <span class="pre">list</span></code></p></td>
  <td><p>X</p></td>
  </tr>
  <tr class="row-even"><td><p>Create requirements file</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">list</span> <span class="pre">--export</span></code></p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">pip</span> <span class="pre">freeze</span></code></p></td>
  <td><p>X</p></td>
  </tr>
  <tr class="row-odd"><td><p>List all environments</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">info</span> <span class="pre">--envs</span></code></p></td>
  <td><p>X</p></td>
  <td><p>Install virtualenv wrapper, then <code class="docutils literal notranslate"><span class="pre">lsvirtualenv</span></code></p></td>
  </tr>
  <tr class="row-even"><td><p>Install other package manager</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">install</span> <span class="pre">pip</span></code></p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">pip</span> <span class="pre">install</span> <span class="pre">conda</span></code></p></td>
  <td><p>X</p></td>
  </tr>
  <tr class="row-odd"><td><p>Install Python</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">install</span> <span class="pre">python=x.x</span></code></p></td>
  <td><p>X</p></td>
  <td><p>X</p></td>
  </tr>
  <tr class="row-even"><td><p>Update Python</p></td>
  <td><p><code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">update</span> <span class="pre">python</span></code>*</p></td>
  <td><p>X</p></td>
  <td><p>X</p></td>
  </tr>
  </tbody>
  </table>
  <p>* <code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">activate</span></code> only works on conda 4.6 and later versions.
  For conda versions prior to 4.6, type:</p>
  <blockquote>
  <div><ul class="simple">
  <li><p>Windows: <code class="docutils literal notranslate"><span class="pre">activate</span></code></p></li>
  <li><p>Linux and macOS: <code class="docutils literal notranslate"><span class="pre">source</span> <span class="pre">activate</span></code></p></li>
  </ul>
  </div></blockquote>
  <p>* <code class="docutils literal notranslate"><span class="pre">conda</span> <span class="pre">update</span> <span class="pre">python</span></code> updates to the most recent in the series,
  so any Python 2.x would update to the latest 2.x and any Python 3.x
  to the latest 3.x.</p>
