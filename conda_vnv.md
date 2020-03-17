# 콘다 가상환경 작업

- `venv`(파이썬 가상환경 관리자)로 가상환경을 만들 때는 가상환경을 저장할 폴더를 지정했었음
  `% python3 -m venv /path/to/new/environment`
- Conda 가상환경은 일반적으로 저장 폴더를 지정하지 않고 생성하며,
  실제 저장되는 위치는 아나콘다 설치 폴더 하위의 `envs` 폴더에 생성됨
- `venv`에서는 가상환경을 삭제하는 별도 명령이 없고, 비활성화된 상태에서 해당 폴더를 삭제
- Conda 가상환경은 가상환경을 삭제하는 명령이 별도로 존재함, 비활성화 된 상태에서
  `% conda remove my_venv`

```SHELL {.line-numbers}
# 가상환경 정보 확인
% conda info --envs

# 가상환경 생성 (아무 폴더에서나)
% conda create --name conda-env python
% conda create -n conda-env python=3.7 numpy

# 폴더를 지정하여 가상환경 생성
% conda create --prefix c:/vnv/python38 python=3.8

# 가상환경 활성화
% conda activate conda-env
(conda-env) %

# 가상환경 비활성화
% conda deactivate

# 가상환경 삭제
% conda env remove -n conda-env

# 가상환경에 설치된 패키지 확인
$ conda list

# txt 파일로 가상환경 스펙 저장 및 생성
$ conda list --name conda-env --explicit > conda-env.txt
$ conda create --name conda-env --file conda-env.txt
```
- 참고 자료
  - [Managing environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-with-commands)
  - [The Definitive Guide to Conda Environments](https://towardsdatascience.com/a-guide-to-conda-environments-bc6180fc533) 참조
