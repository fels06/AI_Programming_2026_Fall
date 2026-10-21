데이터셋별 모델 노트북 7개

01 Iris: 4-12-8-3, softmax, Dropout 0
02 Pima: 8-16-8-1, sigmoid, Dropout 0.1
03 Wine: 12-30-12-8-1, sigmoid, Dropout 0
04 Ames: 전처리 후 D-64-32-1, 로그 가격, Dropout 0.1
05 ETTh1: 96시간 입력, 128-64-24, seasonal residual 기본
06 IRB2400 FK: 6-128-128-64-6
07 IRB2400 IK: 6-128-128-64-6, sin/cos 및 현재 관절각 조건 입력 옵션

실행
1. Colab에 ipynb를 업로드하고 '모두 실행'합니다.
   로봇 데이터는 30만 행이므로 GPU 런타임을 권장합니다.
2. 로컬은 Python 3.11/3.12 환경에서 아래를 먼저 실행합니다.
   python -m pip install -r requirements.txt
   노트북을 여는 Jupyter 커널도 이 환경을 선택합니다.
3. 각 CSV를 Google Drive의 MyDrive/Colab Notebooks/data/ 폴더에 넣습니다.
   데이터 셀에서 Drive를 마운트하고 FILE_PATH를 확인합니다.
   다른 폴더나 로컬에서 실행하면 FILE_PATH를 실제 CSV 경로로 수정합니다.
   파일이 없으면 경로와 파일명을 포함한 FileNotFoundError가 발생합니다.
4. 빠른 동작 확인은 설정 셀의 QUICK_RUN=True로 변경합니다.
   이 모드는 2 epoch이며, 시계열 window·로봇 샘플도 줄입니다.
   정식 학습은 QUICK_RUN=False입니다.
5. 각 노트북은 다른 노트북이나 별도 Python 파일 없이 실행됩니다.
   artifact는 artifacts/<데이터셋>/ 아래 생성됩니다.

결과물
model.keras, preprocessing.joblib, metrics.json, config.json,
history.csv, test_predictions.csv, 학습 곡선 및 예측 시각화.
마지막 셀은 저장한 모델·전처리를 다시 불러와 예측 일치를 확인합니다.
ETTh1 모델 파일은 anchor 더하기까지 포함하므로 predict가 최종 예측을 반환합니다.

분할·평가
- 분류·Ames: train/validation/test=60/20/20.
- FK·IK: 64/16/20. 실제 새 궤적의 성능과 같다고 단정하지 않습니다.
- ETTh1: 시간순 70/15/15, target이 경계를 넘는 window는 제외합니다.
- 전처리 통계는 train에서만 학습하고 test에는 transform만 적용합니다.
- 이진 분류 임계값은 validation F1으로 선택합니다(설정에서 끌 수 있음).
- 모델 설정 비교는 validation으로 하고, test로 설정을 고르지 않습니다.
- 출력이 없는 노트북입니다. 전체 학습으로 성능을 직접 확인할 수 있습니다.
- 제공 모델은 비교 시작점이며 최고 성능을 보장하는 모델은 아닙니다.

데이터·원문
https://github.com/dearyonghoon/course-ai-programming-2026/tree/83c0f113a74b737f1790f3db9f41b34885fd57b2/data
https://github.com/dearyonghoon/course-ai-programming-2026/tree/83c0f113a74b737f1790f3db9f41b34885fd57b2/labs

L03 스타일 개정판
- 학습 목표 / 실습 방법 / 번호가 붙은 단계별 설명을 추가했습니다.
- 확인할 내용 / 체크포인트 / 직접 해보기 / 정리로 학습 흐름을 구성했습니다.
- 데이터 shape, 입력·정답 역할, 전처리 fit/transform, 주요 함수 인자를 한국어로 주석 처리했습니다.
- 모델 층을 직접 나열하고 모델 정의, compile, fit, 학습 곡선, 평가를 별도 셀로 나눴습니다.
- 기존 데이터, 분할 비율, 모델 유닛 수, 전처리와 선택 옵션은 유지했습니다.
- 시계열 잔차 예측과 IK의 sin/cos·현재 관절각 조건 입력도 유지했습니다.
- 출력은 비워 두었습니다. 저장된 전체 학습 성능은 없으며 위에서부터 직접 실행합니다.
- 데이터는 Google Drive 마운트 → FILE_PATH 지정 → 파일 존재 확인 → CSV 읽기 순서로 가져옵니다.
- CSV를 자동 다운로드하지 않습니다. 각 파일은 사용자가 Drive 또는 로컬에 준비합니다.
참고: https://github.com/dearyonghoon/course-ai-programming-2026/blob/83c0f113a74b737f1790f3db9f41b34885fd57b2/labs/L03_Linear_Regression.ipynb

개정판 실행 검증
- Python 3.12 격리 환경에서 기본 노트북 7개를 QUICK_RUN으로 모두 실행했습니다.
- ETTh1의 direct, last_residual과 IK의 sin/cos, 현재 관절각 조건 옵션도 확인했습니다.
- 총 11개 경로에서 2 epoch 학습·평가·저장·재로딩 예측 일치를 확인했습니다.
- 정식 전체 학습의 성능을 측정한 결과는 아닙니다.
- 실제 검증에 사용한 핵심 패키지 버전은 requirements-tested.txt에 있습니다.

Drive 경로 로딩 개정판 검증
- 7개 CSV 모두 로컬 FILE_PATH 지정 후 데이터 읽기를 확인했습니다.
- 파일이 없을 때 FileNotFoundError와 경로 수정 안내를 확인했습니다.
- Drive mount 호출은 가짜 모듈로 검증했으며 실제 Drive 인증은 Colab에서 실행합니다.
- 데이터 읽기 이후의 분할·전처리·모델·평가 코드는 이전 개정판과 같습니다.
