# 보물 모델 넣는 곳

보물 종류마다 다른 .glb 를 씁니다. 아래 이름으로 저장하면 게임에 자동 적용됩니다.

| 파일명 | 종류 | 점수 |
|--------|------|------|
| `models/common.glb` | 🟡 일반 | 1 |
| `models/rare.glb`   | 🔵 희귀 | 3 |
| `models/epic.glb`   | 🟣 전설 | 5 |

- 각 파일은 코드의 `TYPES[].models` 첫 항목입니다.
- 어떤 크기의 모델이든 게임이 **자동으로 크기·중심을 보정**하므로 스케일 조정 불필요.
- 파일이 없거나 로드 실패 시 → 종류별 네트워크 샘플 → 색 도형 순으로 자동 폴백.
- 희귀·전설은 모델 위에 파랑/보라 **발광(glow)**과 오라 링이 더해집니다.
- ⚠️ 로컬 .glb는 `file://` 로는 안 되고, 로컬 서버(`python3 -m http.server`)나 호스팅으로 서빙해야 로드됩니다.

## 무료 .glb 모델 출처

| 출처 | 특징 | 라이선스 |
|------|------|----------|
| https://poly.pizza | 구 Google Poly. "gem" 검색 → glb 바로 다운로드 | 대부분 CC0 / CC-BY |
| https://quaternius.com | 게임용 로우폴리 팩, 통째로 무료 | **CC0** |
| https://kenney.nl/assets?q=3d | 깔끔한 게임 에셋 | **CC0** |
| https://sketchfab.com | 방대함. "Downloadable" + 라이선스 필터 필수 | 모델마다 다름 |
| https://github.com/KhronosGroup/glTF-Sample-Assets | 파이프라인 테스트용 | 다양 |

> 추천: 상업적 사용이면 출처표기가 필요 없는 **CC0**(Quaternius·Kenney·Poly Pizza의 CC0)이 안전합니다.
> CC-BY 모델을 쓰면 크레딧에 제작자 표기를 잊지 마세요.

## 모델이 .gltf(+ .bin + 텍스처)로 쪼개져 있다면
한 파일 .glb 로 합치는 게 편합니다:
- 웹: https://gltf.report 또는 https://glb-packer.glitch.me
- CLI: `npm i -g @gltf-transform/cli` 후 `gltf-transform copy in.gltf out.glb`

## 종류·점수·발광 바꾸기
`index.html` 상단의 `TYPES` 에서 종류별 `models`(URL 목록)·`points`·`weight`(등장비율)·`glow`·`aura`·`sizeMul` 을 조절하세요.
