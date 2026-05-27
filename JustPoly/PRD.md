# 발표용 HTML 제작 계획

## Summary

`text.md` 내용을 기준으로 루트에 `presentation.html`을 만든다. 결과물은 슬라이드형 발표 자료이며, GLB 표시에는 가장 간편한 `<model-viewer>` CDN 방식을 사용한다.

## Key Changes

- `presentation.html` 단일 파일로 구현한다.
- 별도 빌드 도구 없이 브라우저에서 열 수 있게 구성한다.
- 발표용 슬라이드 UI를 만든다:
  - 좌우/상하 키보드 이동
  - 이전/다음 버튼
  - 현재 슬라이드 번호 표시
  - 발표 화면에 맞는 큰 제목, 짧은 문장, 표 중심 레이아웃
- 디자인은 차분한 기술 발표 스타일로 구성한다:
  - 과한 이모지 사용 없음
  - 한국어 본문 가독성 우선
  - 긴 문단은 발표용 bullet로 압축
  - 표는 넓은 화면에서도 읽기 좋게 정리

## GLB Viewer Plan

- `todo:` 위치는 `<model-viewer>`로 대체한다.
- CDN:
  - `https://unpkg.com/@google/model-viewer/dist/model-viewer.min.js`
- 케이스별 결과물 슬라이드:
  - `data/case1/`
  - `data/case2/`
  - `data/case3/`
  - 각 섹션에는 `tank.glb`, `building.glb`, `hotel.glb`, `tofu.glb` 중 대표 모델을 탭/버튼으로 바꿔 볼 수 있게 한다.
- 종합 비교 슬라이드:
  - 원본, 케이스1, 케이스2, 케이스3를 4분할 grid로 동시에 표시한다.
  - 비교 대상 모델은 버튼으로 `tank`, `building`, `hotel`, `tofu` 전환 가능하게 한다.
- `<model-viewer>` 기본 옵션:
  - `camera-controls`
  - `auto-rotate`
  - `shadow-intensity="0.8"`
  - `environment-image="neutral"`
  - `exposure="1"`
  - 모델 로딩 실패 시 짧은 fallback 문구 표시

## Test Plan

- 브라우저에서 `presentation.html`을 열어 슬라이드 이동이 정상 동작하는지 확인한다.
- `data/resource/*.glb`, `data/case1/*.glb`, `data/case2/*.glb`, `data/case3/*.glb`가 정상 로딩되는지 확인한다.
- 종합 비교 슬라이드에서 모델 전환 버튼이 네 개 viewer 모두의 경로를 함께 바꾸는지 확인한다.
- 작은 화면에서도 텍스트와 viewer가 겹치지 않는지 확인한다.

## Assumptions

- 인터넷 연결이 가능한 발표 환경으로 가정하고 CDN `model-viewer`를 사용한다.
- 오프라인 발표가 필요하면 이후 CDN 파일을 로컬 vendor로 내려받는 방식으로 바꾼다.
- 원본 Markdown 내용은 의미를 유지하되, 발표용으로 문장을 압축하고 슬라이드 단위로 재구성한다.
