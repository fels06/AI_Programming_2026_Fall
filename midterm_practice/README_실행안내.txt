중간고사 대비 코딩 연습 · 문제별 셀 분리

01_Midterm_Questions.ipynb: 공통 준비 + 문제 14개, 문제마다 설명 1셀/코드 1셀
02_Midterm_Solutions_Executed.ipynb: 같은 문제의 정답과 직접 실행한 출력/그래프
requirements.txt: 필요한 Python 패키지

사용: Colab에서 노트북을 열고 공통 준비부터 실행하세요.
CSV를 Google Drive의 MyDrive/Colab Notebooks/data/에 넣으세요.
로컬에서는 문제 1, 6, 8, 10, 12, 13의 FILE_PATH를 실제 경로로 바꿉니다.
필요 파일: iris3.csv, pima-indians-diabetes3.csv, ames_train.csv, ETTh1.csv, datasetIRB2400.csv
데이터 출처: 기존 dataset_model_notebooks에서 사용하는 동일한 CSV입니다.
Wine은 제외했고 새 데이터셋은 추가하지 않았습니다.

문제 목록
1. Iris 파일 읽기와 층화 60/20/20 분할
2. MinMax 0~1 정규화, 정수/one-hot 라벨
3. 훈련 샘플 앞 10개의 2x5 시각화
4. AdamW weight decay, Dropout, EarlyStopping
5. 학습 곡선, 정확도, 혼동행렬
6. Pima 0값 처리, 중앙값 대체, 표준화
7. Pima 이진 분류와 정확도/F1
8. Ames 수치/범주 전처리와 로그 가격
9. Ames 회귀와 가격 역변환 MAE
10. ETTh1 시간순 분할과 24→1 window
11. ETTh1 MLP와 Last Value 비교
12. IRB2400 FK 입력/출력 표준화와 출력별 MAE
13. IRB2400 IK 관절각 예측과 circular MAE
14. Iris 모델/전처리 저장과 재로딩

각 문제의 선행 문제를 확인하고 위에서부터 푸세요.
Iris는 이미지가 아니라 4개 특성의 막대그래프로 시각화합니다.
훈련에만 전처리 fit, 검증으로 조기 종료, 테스트는 최종 평가에 사용합니다.
정답은 로컬 CPU에서 QUICK_RUN=True, 2 epoch로 실제 실행했습니다.
큰 분할은 훈련 최대 1024개, 검증/테스트 최대 256개를 사용했습니다.
저장된 숫자는 동작 확인이며 충분히 학습한 성능을 의미하지 않습니다.
전체 학습은 QUICK_RUN=False로 바꿔 다시 실행하세요(최대 60 epoch).
실행 점검에서만 FILE_PATH를 같은 CSV의 로컬 캐시로 바꿨습니다.
Colab Drive 인증은 사용자가 Colab에서 실행합니다.
