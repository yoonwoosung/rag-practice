#  Retrieval-Augmented Generation (RAG) 실습 프로젝트

LangChain과 OpenAI GPT-4-turbo를 활용하여 RAG의 핵심 개념과 실습을 진행했습니다.  
PromptTemplate 작성부터 LLM 호출, 문서 요약 및 분석까지 전 과정을 실습하며,  
LLM을 기반으로 검색 + 생성 구조를 구현하는 전체 흐름을 체득했습니다.

---

## 📌 실습 구성

### 1️⃣ LLM 모델 호출 (`model.invoke`)
OpenAI GPT-4-turbo 모델을 호출하여 간단한 질문에 응답하는 기본 테스트입니다.

![invoke test](./images/01_invoke_test_result.png)

---

### 2️⃣ PromptTemplate 정의 및 적용

LangChain의 `PromptTemplate`을 정의하고, `TextLoader`로 불러온 문장을 기반으로 템플릿을 적용하여 동적 프롬프트를 생성했습니다.

```python
from langchain.prompts import PromptTemplate

template = """당신은 {language} 전문가입니다. 다음 문장에 대해 {task} 해주세요:
"{sentence}"
"""

prompt = PromptTemplate(
    input_variables=["language", "task", "sentence"],
    template=template,
)
