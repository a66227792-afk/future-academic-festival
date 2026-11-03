# 도로 위험요소 자동 신고 시스템

미래인재대학 학술제 · 4NOVA 팀 · 덕성여자대학교

도로 사진에서 균열과 포트홀을 인식해 민원문을 생성하는 신고 지원 시스템이다. 시스템에 쓰이는 비전언어모델(VLM)의 유형·심각도 판정 신뢰성을 300장의 테스트셋으로 평가하고(HyperCLOVA X, Gemini), YOLOv8-seg로 예측한 파손 면적 비율에 따라 일반·보통·긴급 3단계 처리 우선순위를 산출한다. 서비스에는 HyperCLOVA X(HCX-005)를 연동하였고, Streamlit 웹 프로토타입으로 구현하였다.

## 폴더 구조

| 폴더 | 내용 |
|---|---|
| `app/` | Streamlit 프로토타입(`app.py`) |
| `vlm_eval/` | VLM 예비 비교(30장)와 확대 평가(300장), 평가 함수 |
| `area/` | 라벨 기반 파손 면적 비율 계산, 분포 그래프 |
| `yolo/` | YOLOv8-seg 학습·검증 노트북, 학습 결과 곡선 |
| `results/` | VLM 평가 결과, 채점 기록, 최종 표·그래프 |
| `data_info/` | 학습/검증 분할 기록(`sampling.json`) |
| `docs/` | 논문, 발표 자료 |

## 실행 방법

```bash
pip install -r requirements.txt
streamlit run app/app.py
```

- 앱의 위치 검출은 학습한 YOLO 가중치(`best.pt`)가 필요하다. 가중치 파일은 용량 때문에 저장소에 포함하지 않았으며, `app/app.py`의 `MODEL_PATH`에 경로를 지정한다.
- HyperCLOVA X(CLOVA Studio) API 키는 앱 화면에서 입력한다. 키가 없으면 가짜 데이터로 동작한다.

## 데이터

AI Hub의 「지자체 도로 정비 AI 데이터(CASE1 도로)」(TL01 라벨)를 사용하였다. 이용 약관상 재배포가 불가하여 원본 이미지와 라벨은 저장소에 포함하지 않았다. AI Hub(https://aihub.or.kr)에서 직접 내려받아 사용한다.

## 환경변수 (평가 노트북 실행 시)

키 값은 저장소에 올리지 않는다. 아래 이름으로 환경변수에 설정하고 노트북에서 `os.environ`으로 읽는다.

| 이름 | 용도 |
|---|---|
| `CLOVA_API_KEY` | HyperCLOVA X(CLOVA Studio) |
| `GEMINI_API_KEY` | Gemini |
| `OPENROUTER_API_KEY` | GPT-4o, Qwen, Claude (예비 비교) |

## 팀

조민서, 김주혜, 신윤수, 권민지
