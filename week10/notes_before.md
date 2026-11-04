# notes_before.md — week9/tools.py 정리

## 파일 개요

`week9/tools.py`는 영화진흥위원회(KOBIS) 오픈 API로 **일별 박스오피스 정보**를 가져오는 도구 모음입니다.

- 외부 라이브러리: `requests` (HTTP 요청)
- API 키: `secret.py`의 `API_KEY`에서 불러옴
- 요청 주소(`BASE_URL`): KOBIS 일별 박스오피스 조회 API (`searchDailyBoxOfficeList.json`)

## 함수 목록

현재 함수는 **1개**입니다.

### `get_boxoffice_rank_1(date)`

그 날짜의 박스오피스 **1위 영화 제목**을 알려줍니다.

| 항목 | 내용 |
|------|------|
| 받는 것 | `date` (문자열) — 8자리 날짜. 예: `"20260824"` |
| 돌려주는 것 | (문자열) 1위 영화 제목. 예: `"오디세이"` |

**동작 순서**

1. `key`(API 키)와 `targetDt`(날짜)를 파라미터로 만든다.
2. `requests.get`으로 API에 요청한다 (타임아웃 10초).
3. 응답을 JSON으로 바꾼다.
4. `boxOfficeResult` → `dailyBoxOfficeList`에서 영화 목록을 꺼낸다.
5. 목록의 첫 번째 영화(`movies[0]`)의 제목(`movieNm`)을 돌려준다.

## 참고할 점

- 에러 처리가 없습니다. 날짜 형식이 틀리거나, API 키가 잘못됐거나, 네트워크 오류가 나면 예외(`KeyError`, `IndexError`, `requests` 예외 등)가 그대로 발생합니다.
- 1위 영화의 제목만 돌려주고, 관객 수 등 다른 정보는 사용하지 않습니다.
