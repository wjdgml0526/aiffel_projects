🔑 **PRT(Peer Review Template)**  
리뷰어:  김나경 
코더:  이정희

- [x]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요? (완성도)**
    - 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
    - 문제를 해결하는 완성된 코드란 프로젝트 루브릭 3개 중 2개, 
    퀘스트 문제 요구조건 등을 지칭
        - 해당 조건을 만족하는 부분의 코드 및 결과물을 캡쳐하여 사진으로 첨부
          1. 번역기 모델 학습에 필요한 텍스트 데이터 전처리가 잘 이루어졌다.
             ```
             def preprocess_sentence(sentence, s_token=False, e_token=False):
                sentence = sentence.lower().strip()
            
                sentence = re.sub(r"([?.,!])", r" \1 ", sentence)
                sentence = re.sub(r'\bthe\b', '', sentence)
                sentence = re.sub(r'[" "]+', " ", sentence)
                sentence = re.sub(r"[^ㄱ-ㅣ가-힣a-zA-Z?.!]+", " ", sentence)
            
                sentence = sentence.strip()
            
                if s_token:
                    sentence = '<start> ' + sentence
            
                if e_token:
                    sentence += ' <end>'
                
                return sentence
             ```
             ```
             # Sentencepiece를 활용하여 학습한 tokenizer를 생성합니다.
             def generate_tokenizer(corpus,
                                    vocab_size = 20000,
                                    lang="ko",
                                    pad_id=0,
                                    bos_id=1,
                                    eos_id=2,
                                    unk_id=3):
                
                model_prefix = f'{lang}_tokenizer'
                spm.SentencePieceTrainer.train(
                    input = corpus,
                    model_prefix = model_prefix,
                    vocab_size = vocab_size,
                    pad_id = pad_id,
                    bos_id = bos_id,
                    eos_id = eos_id,
                    unk_id = unk_id,
                    user_defined_symbols = ['<PAD>', '<BOS>', '<EOS>', '<UNK>']
                )
            
                tokenizer = spm.SentencePieceProcessor()
                tokenizer.Load(f'{model_prefix}.model')
            
                return tokenizer
              ```
          2. Transformer 번역기 모델이 정상적으로 구동된다.
             ![image](https://github.com/wjdgml0526/aiffel_projects/assets/111371565/c5172315-fea5-494e-a3ab-2e089822f0aa)
             - 학습이 잘 진행된다

          3. 테스트 결과 의미가 통하는 수준의 번역문이 생성되었다.
             ![image](https://github.com/wjdgml0526/aiffel_projects/assets/111371565/e0ee07fa-9d72-40e1-9152-9fa5238afdf0)
            - 정확한 문장은 아니지만 핵심단어를 잘 포함하고 있다

- [x]  **2. 프로젝트에서 핵심적인 부분에 대한 설명이 주석(닥스트링) 및 마크다운 형태로 잘 기록되어있나요? (설명)**
    - [ ]  모델 선정 이유
    - [해당 없음]  Metrics 선정 이유
    - [x]  Loss 선정 이유
          ![image](https://github.com/wjdgml0526/aiffel_projects/assets/111371565/87d06d91-b50f-4bf7-a8f9-a723a1afa421)
        ![image](https://github.com/wjdgml0526/aiffel_projects/assets/111371565/ed30bb30-6e0e-459a-8768-ace66d222901)
    - 각 단계 별로 설명이 잘 되어 있다



- [x]  **3. 체크리스트에 해당하는 항목들을 모두 수행하였나요? (문제 해결)**
    - [x]  데이터를 분할하여 프로젝트를 진행했나요? (train, validation, test 데이터로 구분)
          ![image](https://github.com/wjdgml0526/aiffel_projects/assets/111371565/927965f0-85af-463c-ac25-eeb6041e76b7)
            - 인코더와 디코더 입력을 잘 구분하여 정의함

    - []  하이퍼파라미터를 변경해가며 여러 시도를 했나요? (learning rate, dropout rate, unit, batch size, epoch 등)
    - [x]  각 실험을 시각화하여 비교하였나요?
                    ![image](https://github.com/wjdgml0526/aiffel_projects/assets/111371565/e8e5e1ce-9173-44d6-ba11-b85c5e759166)
            - 폰트에 문제가 있지만 그래프 자체는 잘 출력됨
           
    - [x]  모든 실험 결과가 기록되었나요?
          ![image](https://github.com/wjdgml0526/aiffel_projects/assets/111371565/1ad7d152-e449-4bf6-aa52-d5bb50af9cc8)
            - epoch 별로 sample을 확인함


- [ ]  **4. 프로젝트에 대한 회고가 상세히 기록 되어 있나요? (회고, 정리)**
    - [ ]  배운 점
    - [ ]  아쉬운 점
    - [ ]  느낀 점
    - [ ]  어려웠던 점
