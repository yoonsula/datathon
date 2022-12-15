# 고양시 아동 그림 객체 인식 데이터톤

> 아이 can do it!
<br/>

### 라벨 구성
  - 집, 나무, 여자사람, 남자사람의 4가지 분류로 구성되며, 세부 객체는 다음과 같음
  - 집(15개): 집전체, 지붕, 집벽, 문, 창문, 굴뚝, 연기, 울타리, 길, 연못, 산, 나무, 꽃, 잔디, 태양
  - 나무(14개): 나무전체, 기둥, 수관, 가지, 뿌리, 나뭇잎, 꽃, 열매, 그네, 새, 다람쥐, 구름, 달, 별
  - 여자사람(18개): 사람전체, 머리, 얼굴, 눈, 코, 입, 귀, 머리카락, 목, 상체, 팔, 손, 다리, 발, 단추, 주머니, 운동화, 여자구두
  - 남자사람(18개): 사람전체, 머리, 얼굴, 눈, 코, 입, 귀, 머리카락, 목, 상체, 팔, 손, 다리, 발, 단추, 주머니, 운동화, 남자구두
  
<br/>

### 데이터 수량
  - 학습용데이터: 4개 분류별 각 900건으로 총 3600건
  - 검증용데이터: 4개 분류별 각 100건으로 총 400건
  - 테스트데이터: 4개 분류별 각 100건으로 총 400건

<br/>

### 개발 환경
  - Google Colab
  
<br/>

### 모델 활용
  - YOLOv5 전이학습을 통한 객체 인식
  <pre><code>
  # https://github.com/ultralytics/yolov5
  
  # 모델 가져오기
  !git clone https://github.com/ultralytics/yolov5  # clone repo
  %cd yolov5
  %pip install -qr requirements.txt # install dependencies
  
  # YOLOv5에서 가중치 가져오기
  !wget https://github.com/ultralytics/yolov5/releases/download/v6.0/yolov5s.pt
  </code></pre>
  - 기존의 이미지와 라벨 파일을 YOLO format 형식으로 변환 후 학습 및 검증, 테스트 실시

<br/>

### 학습 방법
  - {dataset.location} 에는 데이터 경로를 입력하면 됩니다. ex) /content/gdrive/MyDrive/drawing
  - img size: 640, batch_size: 8, epoch: 150, weights: yolov5s.pt 를 이용해 학습
  <pre><code>
  !python train.py --img 640 --batch 8 --epochs 150 --data {dataset.location}/data.yaml --weights yolov5s.pt --cache
  </code></pre>

<br/>

### 테스트 방법
  <pre><code>
  # 모델저장
  %cp /content/yolov5/runs/train/exp/weights/best.pt {dataset.location}
  # 저장된 모델 실행
  !python detect.py --source {dataset.location}/test/images/나무/ --weights {dataset.location}/data.pt
  </code></pre>
<br/>
