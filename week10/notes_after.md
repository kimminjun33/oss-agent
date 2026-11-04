작성: Claude Code / 확인: (김민준)

# week9/tools.py 함수 정리

## 개요
- 영화진흥위원회(KOBIS) 오픈 API로 일별 박스오피스 정보를 가져오는 도구 모음임
- `requests` 로 HTTP 요청을 보내고, API 키는 `secret.py` 의 `API_KEY` 에서 가져옴

## 모듈 수준 상수
- `BASE_URL`: KOBIS 일별 박스오피스 조회 엔드포인트 주소임 (`searchDailyBoxOfficeList.json`)

## 함수 목록
- 함수는 `get_boxoffice_rank_1` 하나뿐임

### `get_boxoffice_rank_1(date)`
- 역할: 지정한 날짜의 박스오피스 1위 영화 제목을 돌려줌
- 입력: `date` (문자열) — 8자리 날짜, 예: `"20260824"`
- 출력: (문자열) 1위 영화 제목, 예: `"오디세이"`
- 동작 순서
  1. `key`, `targetDt` 를 파라미터로 묶어 `BASE_URL` 에 GET 요청을 보냄 (타임아웃 10초)
  2. 응답을 JSON 으로 파싱함
  3. `boxOfficeResult.dailyBoxOfficeList` 목록을 꺼냄
  4. 첫 번째 항목의 `movieNm` 값을 반환함

## 눈에 띄는 점
- 함수가 하나뿐이라 1위 외의 순위는 가져올 수 없음
- HTTP 상태 코드 확인이나 예외 처리가 없어, API 오류나 빈 목록이면 `KeyError`, `IndexError` 등이 그대로 발생함
- 날짜 형식 검증이 없음
- `secret.py` 가 같은 폴더에 있어야 import 가 됨
