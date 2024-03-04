# Divorce-lawyers-LLM
이혼전문 변호사 LLM 입니다!

- Tesla V100 32GB 한 대를 사용해서 튜닝하였습니다.
- SOLAR 10.7B에 PEFT LORA를 붙이고, 4bit 양자화를 통해서 학습시켰습니다. 
- 학습 코드는 이 repo를 참고 하였습니다. https://github.com/nlpai-lab/KULLM

- Inference는 24GB 한 대 만으로도 가능합니다!
- LORA MODEL CARD : https://huggingface.co/DoHwan9672/SOLAR10.7B-Divorce-Lawyers-LLM-PEFT

- 데이터셋은 "찾기쉬운 생활법령 정보 ‘이혼' 키워드 | 백문백답, 판례, 솔로몬의 재판 카테고리", "다정 법률 상담소 | 이혼 분쟁 - FAQ", 네이버 지식인 크롤링을 통하여 구축하였습니다. 
- 데이터셋은 학습 및 연구 목적으로만 사용하였습니다. https://huggingface.co/datasets/DoHwan9672/divorce_QA_korean

### create conda env

```
conda env create -f llm.yaml
conda activate llm
```

### Run Fastapi backend


```
cd Divorce-lawyers-LLM
uvicorn main:app --reload
```

### Run Streamlit Frontend

```
streamlit run app.py
```

### Access Streamlit app
http://localhost:8501 

### Example
![Initial](https://github.com/rlaehghks5/Divorce-lawyers-LLM/assets/121927513/8ed7f75f-c507-48c8-a6dc-45fb873ba90b.png)



### 기존 모델과 비교

| **질문** | 이혼소송을 하려고 하는데. 사실 남편과 다른 부분은 크게 이견이 없는데 이혼소송 재산분할만 이견이 심합니다. 재산이 거의다 남편 명의인데 남편은 결혼할 때 본인이 가지고 온 재산에다 본인이 돈을 거의 벌었으 므로 재산분할할게 거의 없다는 입장인거 같습니다. 이혼소송 재산분할 다툼에서 어떻게 해야할까요? 자세히 알려주세요. |
| **SOLAR 10.7B (origin)** | 안녕하세요. 법률 자문 을 제공 할 수는 없지만, 이혼소송 재산 분할 문제 에 대해 더 많 이 알아볼 수 있는 몇 가지 자원 을 안내해 드릴 수 있습니다 있습니다. 먼저, 당신의 주(state)의 이혼법과 재산 분할 법(혹 은 공동체 법)을 조사해보세요. 이러한 법은 주마다 다를 수 있습니다. 또한 당신의 상황에 적합한 변호사를 찾아보는 것도 고려 해볼 수 있습니다. 이혼소송 은 복잡할 수 있으며, 변호사의 도움을 받 는 것이 유 리 할 수 있습니다. 마지막으 로, 당신의 지역 에 있는 법률 원조 사무소 를 확인해 보세요. 그들은 무료 나 저렴 한 비용으 로 법률 지원 을 제공할 수 있습니다. |
| **SOLAR 10.7B (fine-tuning)** | 이혼소송 재산분할 다툼에 대응하는 방법에 대해 질문하셨습니다. **우선 결혼 할 때 남편의 재산이 있었다면 그 재산은 혼인 중 누구에게 속하는지를 알 수 없으므로 재산 분할의 대상이 될 수 있습니다.** 또한 재산 분할은 혼인 중 부부가 공동으 로 일정한 형태의 노력을 하여 재산을 형성한 경우 재산을 분할할 수 있는 제도이므로 **재산 분할은 꼭 부부중 누가 어떤 재산을 형성하였는지 명확하게 밝 혀야 하는것이 아니라 부부가 공동으 로 노력하여 재산을 형성한 정도에 따라 재산 분할의 범위가 달라질 수 있습니다.** **예를 들어 부부가 재산을 형성하는데 있어 남편이 100% 노력을 하였고 아내가 0% 노력을 하였다고 하더라도 아내가 집안의 주부로 노력하여 가정을 꾸려왔다면 재산 분할 비율에 큰 변동이 있을 수 있습니다.** 재산 분할은 그 분할의 비율에 대해서 다툼이 많은 경우이지만 재산 분할 비율이 결정 된 이후 재산 분 할 비율이 너무 불공평하다고 여겨지면 재산 비율 분할 비율을 조정할 수 있는 방법이 있으니 이혼소송 재산 분할 다 툼에 대응하는 방법에 대해 더 자세히 알고 싶다면 전문가와 상담하는 것이 좋습니다. |


