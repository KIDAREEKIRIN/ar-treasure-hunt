# WebAR 데모 모음 (테이블탑 / 탐험 / 이미지 타깃)

스마트폰·태블릿 브라우저에서 **링크만으로 실행되는** 무료 WebAR 데모 3종입니다.
모두 [A-Frame](https://aframe.io/) + [AR.js](https://ar-js-org.github.io/AR.js-Docs/) 로 만들었고 추가 설치/빌드가 없습니다.

| 데모 | 파일 | 기술 | 핵심 |
|------|------|------|------|
| A. 테이블탑 보드게임 | `demo-a-tabletop.html` | AR.js 마커(Hiro) | 마커를 **바닥 앵커**로, 그 위에 보드판 + 주사위/말 |
| B. 방 탐험 보물찾기 | `demo-b-exploration.html` | 카메라 + 자이로(look-controls) | 그 자리에서 360° 둘러보며 숨은 보물 수집 |
| C. 이미지 타깃 등장 | `demo-c-image-target.html` | AR.js 마커(Kanji) | 특정 그림을 비추면 콘텐츠가 팝업 |

> 참고: 무료 WebAR에서 **A와 C는 같은 "마커/이미지 인식" 기술**이고 인터랙션 성격만 다릅니다.
> **B만 자이로 기반**으로 기술 갈래가 다릅니다. 마커 없이 바닥을 자동 인식하는 진짜 공간 추적은
> 유료 SDK(8th Wall 등) 단계에서 붙입니다 — 이 데모들은 그 전에 **게임플레이를 무료로 검증**하는 용도입니다.

---

## ⚠️ 가장 중요한 제약: 카메라는 HTTPS에서만 열립니다

`file://`로 HTML을 더블클릭하면 카메라 권한이 막혀 **작동하지 않습니다.**
아래 방법 중 하나로 HTTPS(또는 localhost) 환경에서 여세요.

### 방법 1) 같은 PC에서 빠른 테스트 (localhost)
```bash
cd webar-demos
python3 -m http.server 8000
# 같은 PC 브라우저에서 http://localhost:8000 접속 (localhost는 HTTPS 예외로 카메라 허용됨)
```
단, **아이패드/탭 같은 다른 기기**에서 테스트하려면 localhost로는 안 되고 HTTPS가 필요합니다 → 방법 2·3.

### 방법 2) ngrok으로 즉석 HTTPS 터널 (기기 테스트 추천)
```bash
cd webar-demos
python3 -m http.server 8000
# 새 터미널에서:
ngrok http 8000
# 출력된 https://xxxx.ngrok-free.app 주소를 아이패드/폰 브라우저로 열기
```

### 방법 3) 무료 호스팅에 올리기 (배포/공유용)
- **GitHub Pages**: 이 폴더를 레포에 push → Settings → Pages 활성화
- **Netlify / Vercel**: 폴더를 드래그&드롭하면 즉시 HTTPS URL 발급
- 발급된 URL을 QR로 만들어 공유하면 "설치 없이 링크 실행" 완성

---

## 🎯 마커 이미지 (A·C 데모용 — 인쇄하거나 다른 화면에 띄워 비추세요)

- **Hiro 마커** (데모 A): https://raw.githack.com/AR-js-org/AR.js/master/data/images/hiro.png
- **Kanji 마커** (데모 C): https://raw.githack.com/AR-js-org/AR.js/master/data/images/kanji.png

마커를 종이에 인쇄하거나 **다른 모니터/폰 화면에 띄운 뒤**, 데모를 실행한 기기 카메라로 비추면 됩니다.
데모 B는 마커가 필요 없습니다(자이로만 사용).

---

## 📱 기기별 참고

- **iPad Air M3 / iPhone (iOS Safari)**: 데모 B의 자이로는 iOS에서 **권한 팝업 허용**이 필요합니다(A-Frame이 자동으로 버튼 표시).
- **갤럭시탭 S6 / Android Chrome**: 셋 다 동작. 2019년 기기라 무거운 콘텐츠는 프레임이 떨어질 수 있어 가볍게 유지하세요.
- 카메라가 후면으로 안 잡히면 데모 B의 `facingMode` 설정을 확인하세요(현재 후면 우선).

---

## 🔜 다음 단계 (production)

1. 이 데모들로 **게임 재미 검증** (무료, 지금 단계)
2. 마커 없이 바닥 자동 인식이 필요해지면 → **8th Wall**로 트래킹 레이어만 교체 (Three.js 게임 로직은 재사용)
3. 앱스토어 배포까지 가려면 → Unity + AR Foundation 재구성 검토

## 라이브러리 버전
- A-Frame `1.5.0`
- AR.js `3.4.5`
