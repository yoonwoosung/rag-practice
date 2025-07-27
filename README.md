# Retrieval-Augmented Generation (RAG) 실습 프로젝트

LangChain과 OpenAI GPT-4-turbo를 활용하여 RAG(Retrieval-Augmented Generation)의 개념과 구조를 실습하였습니다.  
PromptTemplate 정의부터 모델 호출, 문서 요약 및 응답 평가까지 전체 흐름을 직접 구현하며,  
검색 기반 응답 생성 구조를 학습했습니다.

---

##  실습 구성

---

###  1. LLM 모델 호출 (`model.invoke`)

OpenAI GPT-4-turbo 모델을 호출하여 간단한 질의에 대한 응답 결과를 확인했습니다.


---

###  2. PromptTemplate 정의 및 적용

프롬프트 템플릿을 구성하여 반복적인 질의 형식을 자동화하고, 동적 입력값을 기반으로 다양한 문장을 생성했습니다.

####  (1) 템플릿 구조 정의

PromptTemplate은 질문 양식을 자동으로 만드는 기능입니다.  
예를 들어 어떤 언어로 어떤 작업을 할지 틀을 만들어두고, 여기에 문장만 바꾸면 됩니다.

```python
from langchain.prompts import PromptTemplate

template = """당신은 {language} 전문가입니다. 다음 문장에 대해 {task} 해주세요:
"{sentence}"
"""

prompt = PromptTemplate(
    input_variables=["language", "task", "sentence"],
    template=template,
)
🧪 (2) 실제 문장에 템플릿 적용
TextLoader를 통해 sample.txt 파일에서 문장을 불러오고,
각 문장마다 PromptTemplate을 적용해 GPT가 이해할 수 있는 구조로 만듭니다.

python
복사
편집
from langchain_community.document_loaders import TextLoader

loader = TextLoader("data/sample.txt")
docs = loader.load()

for doc in docs:
    print(prompt.format(
        language="한국어",
        task="문법 오류를 설명",
        sentence=doc.page_content
    ))
    print("=" * 80)
📷 템플릿 적용 결과

 3. LLM API 호출 결과
PromptTemplate을 통해 구성한 문장을 실제 GPT 모델에 전달하고 응답을 받았습니다.
이 과정은 model.invoke(...)로 수행됩니다.



 4. 요약 응답 및 문서 평가
GPT가 문서를 요약하거나 평가하는 과정을 테스트했습니다.
문서에 대한 감정 분석, 핵심 내용 요약 등도 수행할 수 있습니다.


