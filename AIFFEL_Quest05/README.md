🔑 **PRT(Peer Review Template)**

- 리뷰어 박장현, 코더 이정희

- [X]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요? (완성도)**
    - 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
    - 문제를 해결하는 완성된 코드란 프로젝트 루브릭 3개 중 2개, 
    퀘스트 문제 요구조건 등을 지칭
        - 해당 조건을 만족하는 부분의 코드 및 결과물을 캡쳐하여 사진으로 첨부
    - **1. 다양한 방법으로 Text Classification 태스크를 성공적으로 구현하였다.**  -> 성공
      ![스크린샷 2024-06-12 오후 5 20 36](https://github.com/wjdgml0526/aiffel_projects/assets/37362505/d5ebc360-34cd-4a2f-9601-ecaf1092d107)  
      ![스크린샷 2024-06-12 오후 5 20 51](https://github.com/wjdgml0526/aiffel_projects/assets/37362505/09bc4576-8fda-4879-84b2-10ca22c91b80)  
      ![스크린샷 2024-06-12 오후 5 21 03](https://github.com/wjdgml0526/aiffel_projects/assets/37362505/8ae0225e-dc53-4f75-bd52-9e2210d9e19d)  
    - **2. gensim을 활용하여 자체학습된 혹은 사전학습된 임베딩 레이어를 분석하였다.** -> 성공
      ![스크린샷 2024-06-12 오후 5 22 24](https://github.com/wjdgml0526/aiffel_projects/assets/37362505/843f78ed-c6cd-4e96-9116-ed8b0a646218)
    - **3. 한국어 Word2vec을 활용하여 가시적인 성능향상을 달성했다.**  -> 미흡
      ![스크린샷 2024-06-12 오후 5 22 49](https://github.com/wjdgml0526/aiffel_projects/assets/37362505/927bb0b7-5c4d-46a1-8c4d-e530eb83bf50)
        - word_vectors를 word_vectors.wv로 바꿔주시면 정상적으로 작동합니다.
        - word_vector_dim도 사전학습된 임베딩의 차원에 맞게 수정해주세요.
      
- [X]  **2. 프로젝트에서 핵심적인 부분에 대한 설명이 주석(닥스트링) 및 마크다운 형태로 잘 기록되어있나요? (설명)**
    - [X]  모델 선정 이유
    - [X]  Metrics 선정 이유
    - [X]  Loss 선정 이유
    - 노드에서 배운 Model, Metrics, Loss 사용
      
- [X]  **3. 체크리스트에 해당하는 항목들을 모두 수행하였나요? (문제 해결)**
    - [X]  데이터를 분할하여 프로젝트를 진행했나요? (train, validation, test 데이터로 구분)
       ![스크린샷 2024-06-12 오후 5 28 38](https://github.com/wjdgml0526/aiffel_projects/assets/37362505/99ade4c2-5ea5-4a9e-a199-9145ecb60596)
    - [ ]  하이퍼파라미터를 변경해가며 여러 시도를 했나요? (learning rate, dropout rate, unit, batch size, epoch 등)
       시간이 부족해서 하이퍼파라미터를 변경하는 실험까지는 진행하지 못한 것으로 보이네요.
    - [X]  각 실험을 시각화하여 비교하였나요?
       ![스크린샷 2024-06-12 오후 5 27 10](https://github.com/wjdgml0526/aiffel_projects/assets/37362505/f5c8e468-7ddd-4ad5-85d3-ba01b894ad7e)  
    - [X]  모든 실험 결과가 기록되었나요?

- [X]  **4. 프로젝트에 대한 회고가 상세히 기록 되어 있나요? (회고, 정리)**
    - [X]  배운 점
    - [X]  아쉬운 점
    - [X]  느낀 점
    - [X]  어려웠던 점
