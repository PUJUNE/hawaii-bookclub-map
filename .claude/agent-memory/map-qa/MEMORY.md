# map-qa 메모리

## 실행 방법
- 빌드 없는 정적 단일 파일. `python3 -m http.server 8000` 후 `http://localhost:8000/index.html`
  (또는 file:// 직접 로드도 동작 — 외부 의존성은 unpkg의 Leaflet 1.9.4 CSS/JS와 CARTO 타일뿐).
- 원격(Claude Code on the web) 환경에서는 Playwright에 `executablePath: '/opt/pw-browsers/chromium'` 사용.
- 원격 환경 주의: 헤드리스 브라우저는 프록시 때문에 unpkg(403)와 CARTO 타일(ERR_TUNNEL_CONNECTION_FAILED)을
  못 받는다. 검증 시 `npm i leaflet`으로 받은 로컬 leaflet.js/css로 CDN URL을 치환한 사본(test.html)을 쓰고,
  타일 로드 실패 에러는 환경 문제이므로 무시한다 (2026-07-20 확인).
- 배포본: https://pujune.github.io/hawaii-bookclub-map/ (GitHub Pages, main 반영 후 확인).

## 체크리스트
1. 콘솔 에러 0건.
2. 지도 노드 수 == ll 있는 항목 수 == subtitle의 '지도 표시 N곳'.
3. 사이드바 목록 항목 수 == M.length == subtitle의 '모임 N회'.
4. 모바일 토글 버튼의 개수(#ltCount) == M.length (과거 하드코딩 미갱신 버그 있었음).
5. 경로 화살표/곡선 수 == (지도 표시 수 − 1), '이동 경로' 체크박스로 켜고 꺼짐.
6. 노드 클릭 → 팝업에 회차·책·저자·날짜·장소, CAND 있는 회차는 '아쉬웠던 다른 후보작' 표시.
7. 목록 클릭 → flyTo 후 팝업 자동 오픈, 해당 항목 active 하이라이트.
8. 장소 없는 회차(pl:null)는 목록에서 흐리게(off), 클릭 불가.
9. '수도권 보기'/'전체 보기' 전환 — 전체 보기에서 광주(19회차) 포함.
10. 모바일(폭 ≤760px): 지도가 위, 접이식 목록 시트가 아래. 목록에서 선택 시 시트가 접히며 지도 노출. 노드 32px.
11. 연도별 노드 색: 22 파랑, 23 초록, 24 옐로(글자 어두움), 25 진초록, 26 보라. legend와 일치.

## 알려진 이력
- 2026-07-20: 모바일 목록 버튼 '(39)' 하드코딩 미갱신 버그 발견 → #ltCount로 동적 계산화.
- GitHub Pages deploy가 일시 실패한 적 있음(재시도 커밋으로 해결) — 배포 안 보이면 Actions 재실행 먼저.
