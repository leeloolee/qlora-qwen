# QLoRA + Qwen-VL

이 레포지토리는 Vision-Language Large language model에 대하여 "QLoRA: Efficient Finetuning of Quantized LLMs"를 지원하는 프로젝트로, 양자화된 대규모 언어 모델(LLMs)의 효율적인 파인 튜닝을 가능하게 합니다.
이 프로젝트는 서울대학교 병원의 바루다 프로젝트에서 개발되었으며, bitsandbytes를 사용한 양자화와 Hugging Face의 PEFT 및 transformers 라이브러리와 통합되어 있습니다.

## 개요
QLoRA는 65B 파라미터 모델을 단일 48GB GPU에서 파인 튜닝할 수 있을 정도로 메모리 사용량을 충분히 줄이는 효율적인 방법을 제시합니다. 이는 전체 16비트 파인 튜닝 작업 성능을 유지하면서 4비트 양자화된 사전 훈련된 언어 모델을 통해 그라디언트를 역전파합니다. 

### QLoRA
QLoRA는 성능을 희생하지 않고 메모리를 절약하기 위해 여러 혁신을 도입했습니다:

- 4비트 NormalFloat (NF4), 정규 분포 가중치에 이론적으로 최적인 새로운 데이터 유형
- 평균 메모리 사용량을 줄이기 위한 더블 양자화
- 메모리 스파이크를 관리하기 위한 페이지드 옵티마이저

### Qwen-VL
Qwen 모델은 텍스트와 이미지 모두를 인식하고 이해하기 위해 설계된 대규모 비전-언어 모델입니다. 
이 모델은 이미지 캡셔닝, 질문 응답, 시각적 위치 찾기, 그리고 유연한 상호작용과 같은 작업에서 뛰어난 성능을 보인다고 합니다. 

 zero-shot captioning, 시각적 또는 문서 기반의 시각적 질문 응답, 그리고 그라운딩을 포함한 다양한 작업을 다룹니다.

- **강력한 성능**: 여러 평가 벤치마크(제로샷 캡셔닝, VQA, DocVQA, 그라운딩 포함)에서 동일 수준의 모델 규모로 기존의 오픈 소스 대규모 비전-언어 모델(LVLM)을 크게 능가합니다.
- **다국어 LVLM 텍스트 인식 및 그라운딩 지원**: Qwen-VL은 자연스럽게 영어와 중국어, 그리고 다국어 대화를 지원합니다. 또한 이미지 내에서 중국어와 영어의 이중 언어 텍스트와 인스턴스를 끝까지 인식하고 그라운딩합니다.
- **다중 이미지 중첩 대화**: 이 기능은 여러 이미지의 입력과 비교를 허용하며, 이미지와 관련된 질문을 지정하고 다중 이미지 스토리텔링에 참여할 수 있습니다.
- **세밀한 인식과 이해**: 다른 오픈 소스 LVLM이 현재 사용하는 224×224 해상도에 비해, 448×448 해상도는 세밀한 텍스트 인식, 문서 QA, 그리고 바운딩 박스 탐지를 촉진합니다.

