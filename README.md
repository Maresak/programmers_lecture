## <프로그래머스 강의 중 "실습으로 배우는 데이터 사이언스">
- 강의 링크 : https://programmers.co.kr/learn/courses/21
- 강의는 Mac 환경이므로 윈도우 환경과 소폭 다른게 있는 부분이 있다.
- 주피터 랩과 노트북 전환은 url에서 /lab 또는 /tree 를 이용

## <구글 Colaboratory를 이용하여 tensorflow 실행>
- 실습링크, 단축키 : https://colab.research.google.com/notebooks/mlcc/hello_world.ipynb
- 구글의 머신러닝 단기집중과정에서 온라인 머신러닝 학습시스템 : https://developers.google.com/machine-learning/crash-course/
- 구글 머신러닝 단기집중과정 실습(Colaboratory 사용) : https://developers.google.com/machine-learning/crash-course/exercises

---
### 2019.03.14 현재 안 되는 부분
1. 09_nltk_tutorial 에서 worker를 잘 인식하지 못하는 지 분산하여 training이 되지 않는다
2. 12_tf-idf_k-fold 에서 XGBoost 부분을 해결해야 한다. 아마 윈도우 환경에서 설치가 제대로 되지 않은걸로 추정 (해결)
    http://quantfactory.blogspot.com/2017/04/xgboost.html 참고하며 해결 중
    - Git Bash를 열어 XGBoost를 저장할 경로에 다음 명령어를 입력
        - git clone --recursive https://github.com/dmlc/xgboost
        - cd xgboost
        - git submodule init
        - git submodule update
    - 복사한 XGBoost를 빌드하려면 64bit 윈도우에서는 MinGW-W64가 필요하다
        - architecture에서 x86_64로 변경 후 설치
        - Windows 환경에서 Linux 환경을 구축하여 개발을 진행해야 할 경우 Linux의 GCC Compiler를 사용할 수 있게 하는게 MinGW
        - 설치 후 시스템 환경변수에 path 설정 (C:\Program Files\mingw-w64\x86_64-7.3.0-posix-seh-rt_v5-rev0\mingw64\bin 로 저장했음)
        - Git Bash를 새로 열어 which mingw32-make 를 했을 때 위의 경로 돌려주면 완료
        - 또는 cmd 창에서 gcc --version으로 gcc 명령 인식되는지 확인
    - XGBoost 설치한 경로로 가서 Git Bash에 다음과 같이 입력해 준다
        - 편의를 위해 alias make='mingw32-make' 를 입력
        - cd dmlc-core
        - make -j4
        - cd ../rabit
        - make lib/librabit_empty.a -j4
        - cd ..
        - cp make/mingw64.mk config.mk
        - make -j4
    - 아나콘다 프롬프트 등에서 XGBoost를 설치한다
        - cd xgboost\ptyhon-package
        - ptyhon setup.py install
    - import xgboost as xgb 까지 확인
    
    ### parameters에서 booster항목에서 gblinear를 gbtree로 변경하니 0과 1 모두 출력