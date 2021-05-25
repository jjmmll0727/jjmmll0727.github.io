---
title: "capstone design - trained model"
excerpt: "various model"
categories: "project"
---

<div style = "font-size: 28px; line-height: 25px;">
<center><strong>trained model</strong></center><br><br>
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
스마트 기기를 사용하면서 사람들은 웹툰이나 소설 등을 볼 떄 스크롤이나 터치 등 단순 반복 행위들을 하게 된다.<br>
이러한 반복 행위들을 손가락이 아닌 얼굴 표정으로 대체 할 수 있다면, 손을 사용하지 못하는 환경에서도 자유롭게 웹툰이나 소설 등을 볼 수 있겠다 라는 관점에 의하여 졸업 프로젝트를 시작하게 되었다.<br>
안드로이드 스튜디오 안에 딥러닝 학습 모델을 집어넣고, real-time background camera를 통해 사용자의 얼굴을 학습 모델의 input 값으로 넣어준다면 나오는 결과 값을 나오게 한다. 예를 들어, " 웃는 얼굴이 포착되었습니다, 눈을 깜빡였습니다 " <br>
이와 같은 결과값을 통해 안드로이드에서 터치 이벤트를 발생시키거나, 스크롤 이벤트를 발생시키는 서비스이다.<br><br>
</div>

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<strong>초기단계</strong><br><br>
dlib이라는 소프트웨어를 통해 얼굴의 임의의 68개의 점을 잡고, 눈의 위치, 입의 위치에 해당하는 점들의 번호를 통해 눈과 입의 이미지를 추출해낸다.<br>
추출한 이미지들을 사전에 학습된 모델들을 통해 해당 이미지가 우리가 원하는 이미지인지 판별하는 작업까지 완료를 했었다.<br>
</div>

```python
## dilb software
detector = dlib.get_frontal_face_detector()
predictor = dlib.shape_predictor('shape_predictor_68_face_landmarks.dat')

for face in faces:
    
    shapes = predictor(gray, face)
    shapes = face_utils.shape_to_np(shapes)

    eye_img_l, eye_rect_l = crop_eye(gray, eye_points=shapes[36:42])
    eye_img_r, eye_rect_r = crop_eye(gray, eye_points=shapes[42:48])

    eye_img_l = cv2.resize(eye_img_l, dsize=IMG_SIZE)
    eye_img_r = cv2.resize(eye_img_r, dsize=IMG_SIZE)
    eye_img_r = cv2.flip(eye_img_r, flipCode=1)

    #cv2.imshow('l', eye_img_l)
    #cv2.imshow('r', eye_img_r)

    eye_input_l = eye_img_l.copy().reshape((1, IMG_SIZE[1], IMG_SIZE[0], 1)).astype(np.float32) / 255.
    eye_input_r = eye_img_r.copy().reshape((1, IMG_SIZE[1], IMG_SIZE[0], 1)).astype(np.float32) / 255.

    pred_l = model.predict(eye_input_l)
    pred_r = model.predict(eye_input_r)
```

<div style = "font-size: 15px; line-height: 25px; text-align: left">
<strong>용량 문제</strong><br><br>
dlib을 사용하니 정확도는 높아졌지만, 용량이 너무 크다고 판단되었다. <br>
교수님과의 피드백을 통해 더 가벼운 모델을 사용하는 것을 권장 받고, 다른 network를 찾아보기로 하였다. <br>
dlib이라는 소프트웨어를 사용하는 것이 너무 무거워서 눈 등의 이미지를 추출하는 다른 모델이 필요했다. <br>
opencv 알고리즘 중에 haar cascade를 이용했다. <br>
haar cascade는 머신러닝 기반의 object detection algorithm이다. <br>
사전에 정해진 물체(ex. 눈)를 인식하는데 아주 효율적인 알고리즘으로서, 깃허브에서 다운이 가능하다.<br>
<a href = "https://github.com/opencv/opencv/tree/master/data/haarcascades">haar cascade github</a><br>
</div>

```python
face_cascade = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')
eye_cascade = cv2.CascadeClassifier('haarcascade_eye.xml')

faces = face_cascade.detectMultiScale(
        image,
        scaleFactor=1.1,
        minNeighbors=5,
        minSize=(1, 1),
        flags=cv2.CASCADE_SCALE_IMAGE
        )
```
<div style = "font-size: 15px; line-height: 25px; text-align: left">
위와 같이 알고리즘을 가져와서 이미지에서 얼굴 및 눈 이미지를 추출할 수 있다. <br>
추출한 이미지를 학습모델에 넣어 우리가 원하는 눈의 이미지가 맞는지 파악하기 위해 xception 모델을 사용하였다. <br>

<p style = "font-size: 15px;"><a href = "https://docs.opencv.org/4.1.0/d7/d8b/tutorial_py_face_detection.html">출처</a></p>