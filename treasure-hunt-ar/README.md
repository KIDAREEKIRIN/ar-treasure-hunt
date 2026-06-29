# 💎 보물 탐험 AR — 월드 트래킹 버전 (8th Wall / Niantic 엔진)

자이로 버전(`../treasure-hunt/`)을 **마커 없는 실제 바닥 트래킹(SLAM)**으로 업그레이드한 버전입니다.
바닥을 탭하면 그 주변에 보물이 흩어지고, **실제로 걸어가서** 탭해 수집합니다.

## 동작
1. 페이지를 열면 8th Wall 엔진이 카메라+SLAM을 시작(권한 허용 필요).
2. 바닥을 비추고 **탭** → 주변에 보물 6개 + 지뢰 2개가 실제 공간에 배치됨.
3. 보물을 향해 **걸어가서 탭**하면 획득(+점수·콤보·파티클·사운드). 화살표가 가장 가까운 보물을 안내.
4. 🟥 지뢰를 탭하면 시간·점수 감점. 제한시간 안에 다 모으면 클리어.

## 기술 구성 (빌드 불필요, 정적 self-host)
- `vendor/8frame-1.5.0.min.js` — 8th Wall의 A-Frame 포크. `xrweb`(월드 트래킹) 컴포넌트 포함. (예제 repo의 LFS에서 받아 벤더링)
- `@8thwall/engine-binary` (CDN) — 무료 배포 엔진 바이너리(SLAM), `data-preload-chunks="slam"`.
- `@8thwall/xrextras`, `@8thwall/landing-page` (CDN) — 로딩/권한/에러 UI.
- 게임 로직은 `index.html` 안에 인라인(`ar-treasure-game` 컴포넌트). 자이로 버전의 점수·콤보·종류별 모델·지뢰·레이더·파티클·사운드를 이식.

> webpack/LFS 없이 **순수 정적 파일**이라 GitHub Pages 등 어디서든 호스팅됩니다.

## 라이선스 / 출처 (중요)
- 엔진 바이너리는 **Niantic Spatial XR Engine License**(무료, limited-use). © Niantic Spatial, Inc.
  전문: https://github.com/8thwall/engine/blob/main/LICENSE
- 핵심 제약: **(1) 유료 판매되고 (2) 가치가 전적/상당 부분 이 엔진에서 나오는** 제품엔 사용 불가.
  → 무료 배포이거나 AR이 더 큰 제품의 한 기능이면 OK. 역공학·바이너리 변형 금지. `xr.js`의 Niantic 저작권 고지 유지.
- 8frame/예제 코드는 MIT (8th Wall, Inc.).

## 튜닝 포인트 (`index.html` 상단 CONFIG)
- 스케일: `modelUnits`(모델 크기), `fieldRMin/Max`(보물 분포 반경), `yMin/Max`(높이), `colliderR`(조준 반경)
  — 8frame 예제 스케일(약 6단위 ≈ 1m) 기준. **실기기에서 체감 보고 조정 권장.**
- 게임: `treasureCount`·`mineCount`·`timeSec`·`comboWindowMs`·`fakePenaltySec`, 종류는 `TYPES`.

## 아직 이식 안 한 것 (기기 검증 후 추가 예정)
- 웨이브 재배치, 시간 보너스 아이템, 난이도 선택, 최고기록(localStorage) — 자이로 버전에 이미 구현돼 있어 이식만 하면 됨.

## ⚠️ 검증 상태
- self-host 파이프라인·컴포넌트 로드·게임 로직은 헤드리스 프리뷰로 확인 완료(콘솔 에러 0).
- **실제 카메라 영상·SLAM 바닥 인식·걷기 트래킹·스케일 체감은 실기기 확인 필요.**
