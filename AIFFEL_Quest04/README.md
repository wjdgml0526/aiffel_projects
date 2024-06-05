🔑 **PRT(Peer Review Template)**

- [X]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요? (완성도)**
    - 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
    - 문제를 해결하는 완성된 코드란 프로젝트 루브릭 3개 중 2개, 
    퀘스트 문제 요구조건 등을 지칭
        - 해당 조건을 만족하는 부분의 코드 및 결과물을 캡쳐하여 사진으로 첨부
          1. 사진 제작
              1) 인물 사진
             ![image](https://github.com/4rldur0/aiffel_projects/assets/111371565/e20ee112-ed04-404f-82a2-837d431fcc9c)
              2) 동물 사진
             ![image](https://github.com/4rldur0/aiffel_projects/assets/111371565/d7064f7e-16c3-4721-8d25-4faf94399600)
              3) 크로마키
             ![image](https://github.com/4rldur0/aiffel_projects/assets/111371565/51c81c1d-9e57-46b9-991c-3da39f0d8f50)
          2. 문제점
             ![image](https://github.com/4rldur0/aiffel_projects/assets/111371565/f9795e3a-2285-4149-bdda-755fb6b27293)
          3. 솔루션
             ![image](https://github.com/4rldur0/aiffel_projects/assets/111371565/105f9a17-faeb-43d3-add0-5ac9a7f9b508)
             > 꽃다발을 잡고있는 손이 블러처리되는 문제를 해결하기 위한 방안으로 깊이 추정 알고리즘을 말해주셨는데, 손 자체가 꽃다발 사이에 있고 꽃다발과 사람의 깊이 차이가 크지 않기 때문에 알고리즘이 잘 작동할 지 궁금합니다! 이에 대해서 알게 되시면 나중에 꼭 알려주세요:) 


        


- [X]  **2. 프로젝트에서 핵심적인 부분에 대한 설명이 주석(닥스트링) 및 마크다운 형태로 잘 기록되어있나요? (설명)**
    - [ ]  모델 선정 이유
          > DeepLab에 대한 설명이 있었으면 좋았을 것 같습니다!
    - [해당 없음]  Metrics 선정 이유
    - [헤당 없음]  Loss 선정 이유

- [X]  **3. 체크리스트에 해당하는 항목들을 모두 수행하였나요? (문제 해결)**
    - [해당 없음]  데이터를 분할하여 프로젝트를 진행했나요? (train, validation, test 데이터로 구분)
    - [해당 없음]  하이퍼파라미터를 변경해가며 여러 시도를 했나요? (learning rate, dropout rate, unit, batch size, epoch 등)
    - [X]  각 실험을 시각화하여 비교하였나요?
    - [X]  모든 실험 결과가 기록되었나요?
          > 세그멘테이션을 적용하고 블러된 배경과 합성하는 부분이 함수로 처리되어 있어 한번에 모든 이미지를 다양한 조건으로 처리할 수 있다는 점이 좋다고 생각합니다다
  ```
    def portrait_mode(model, img_path, target_obj, blur_ksize = (13, 13)):
    # 이미지 불러오기
    img_orig = cv2.imread(img_path)
    
    # 불러온 이미지 분할, 분할 출력 배열 생성
    segvalues, output = model.segmentAsPascalvoc(img_path) # segmentAsPascalvoc()함 수 를 호출 하여 입력된 이미지를 분할, 분할 출력의 배열을 가져옴, 분할 은 pacalvoc 데이터로 학습된 모델을 이용
    
    # object 추출
    LABEL_NAMES = [
    'background', 'aeroplane', 'bicycle', 'bird', 'boat', 'bottle', 'bus',
    'car', 'cat', 'chair', 'cow', 'diningtable', 'dog', 'horse', 'motorbike',
    'person', 'pottedplant', 'sheep', 'sofa', 'train', 'tv'
    ]
    try:
        obj_idx = LABEL_NAMES.index(target_obj)
    except ValueError:
        return LABEL_NAMES
    
    # 아래 코드를 이해하지 않아도 좋습니다
    # PixelLib에서 그대로 가져온 코드입니다
    # 주목해야 할 것은 생상 코드 결과물이예요!

    #컬러맵 만들기 
    colormap = np.zeros((256, 3), dtype = int)
    ind = np.arange(256, dtype=int)

    for shift in reversed(range(8)):
        for channel in range(3):
            colormap[:, channel] |= ((ind >> channel) & 1) << shift
        ind >>= 3
    # 색상순서 변경 - colormap의 배열은 RGB 순이며 output의 배열은 BGR 순서로 채널 배치가 되어 있어서
    seg_color = (colormap[obj_idx][2], colormap[obj_idx][1], colormap[obj_idx][0])
    
    # seg_color로만 이루어진 마스크
    # output의 픽셀 별로 색상이 seg_color와 같다면 1(True), 다르다면 0(False)이 됩니다
    # seg_color 값이 person을 값이 므로 사람이 있는 위치를 제외하고는 gray로 출력
    # cmap 값을 변경하면 다른 색상으로 확인이 가능함
    seg_map = np.all(output==seg_color, axis=-1)
    
    # True과 False인 값을 각각 255과 0으로 바꿔줍니다
    img_mask = seg_map.astype(np.uint8) * 255
    
    # 배경 흐리게 하기
    # (13,13)은 blurring kernel size를 뜻합니다
    # 다양하게 바꿔보세요
    img_orig_blur = cv2.blur(img_orig, blur_ksize)
    
    # 세그멘테이션 마스크를 이용해서 배경만 추출
    # cv2.cvtColor(입력 이미지, 색상 변환 코드): 입력 이미지의 색상 채널을 변경
    # cv2.COLOR_BGR2RGB: 원본이 BGR 순서로 픽셀을 읽다보니
    # 이미지 색상 채널을 변경해야함 (BGR 형식을 RGB 형식으로 변경) 
    img_mask_color = cv2.cvtColor(img_mask, cv2.COLOR_GRAY2BGR)

    # cv2.bitwise_not(): 이미지가 반전됩니다. 배경이 0 사람이 255 였으나
    # 연산을 하고 나면 배경은 255 사람은 0입니다.
    img_bg_mask = cv2.bitwise_not(img_mask_color)

    # cv2.bitwise_and()을 사용하면 배경만 있는 영상을 얻을 수 있습니다.
    # 0과 어떤 수를 bitwise_and 연산을 해도 0이 되기 때문에 
    # 사람이 0인 경우에는 사람이 있던 모든 픽셀이 0이 됩니다. 결국 사람이 사라지고 배경만 남아요!
    img_bg_blur = cv2.bitwise_and(img_orig_blur, img_bg_mask)
    
    # np.where(조건, 참일때, 거짓일때)
    # 세그멘테이션 마스크가 255인 부분만 원본 이미지 값을 가지고 오고 
    # 아닌 영역은 블러된 이미지 값을 사용합니다.
    img_concat = np.where(img_mask_color==255, img_orig, img_bg_blur)
    
    return img_concat
  ```

- [X]  **4. 프로젝트에 대한 회고가 상세히 기록 되어 있나요? (회고, 정리)**
    - [X]  배운 점
    - [X]  아쉬운 점
    - [X]  느낀 점
    - [X]  어려웠던 점
          ![image](https://github.com/4rldur0/aiffel_projects/assets/111371565/f1fb27b2-f136-448c-8ff8-6ce918a30d06)

--- 
[리뷰어 느낀 점]  
같은 동작을 하지만 구현이 조금씩 다르게 되어있어 배우는 점이 있었습니다. **그리고 강아지가 귀여워요**
