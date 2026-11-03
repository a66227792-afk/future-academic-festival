# 도로 위험요소 자동 신고 시스템

미래인재대학 학술제 · 4NOVA 팀 (덕성여자대학교)

도로 사진에서 균열과 포트홀을 인식하고, 파손 면적에 따라 처리 우선순위를 정해 민원문을 만들어 주는 신고 지원 시스템이다. 비전언어모델(HyperCLOVA X, Gemini)의 판정 신뢰성을 300장의 사진으로 평가하였고, 평가 결과에 따라 서비스에는 HyperCLOVA X를 연결하였다. 파손 위치와 면적은 YOLOv8-seg로 구하며, 면적 비율이 2% 미만이면 일반, 5% 미만이면 보통, 그 이상이면 긴급으로 나눈다. 전체는 Streamlit 웹 앱으로 구현하였다.

## 폴더

- `app/` : Streamlit 웹 앱
- `vlm_eval/` : VLM 평가 코드
- `area/` : 파손 면적 비율 계산
- `yolo/` : YOLOv8-seg 학습과 검증
- `results/` : 평가 결과와 최종 표·그래프
- `data_info/` : 학습·검증 분할 기록
- `docs/` : 논문과 발표 자료

## 실행

```bash
pip install -r requirements.txt
streamlit run app/app.py
```

위치 검출에는 학습한 가중치 파일(`best.pt`)이 필요하다. 용량 때문에 저장소에는 넣지 않았고, `app/app.py`의 `MODEL_PATH`에 경로를 지정하면 된다. HyperCLOVA X API 키는 앱 화면에서 입력하며, 키가 없으면 가짜 데이터로 동작한다.

## 데이터

AI Hub의 지자체 도로 정비 AI 데이터(CASE1 도로)를 사용하였다. 재배포가 허용되지 않아 원본 사진과 라벨은 포함하지 않았으며, [AI Hub](https://aihub.or.kr)에서 내려받아야 한다.

## 환경변수

평가 노트북을 실행하려면 아래 키를 환경변수로 설정한다. 키 값은 저장소에 올리지 않았다.

`CLOVA_API_KEY`, `GEMINI_API_KEY`, `OPENROUTER_API_KEY`

## 팀

조민서, 김주혜, 신윤수, 권민지
