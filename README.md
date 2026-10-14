# 수퍼유자 상품 이미지 저장소

**수퍼유자**(super.yuja.dev)는 Appier Korea가 마케팅 자동화·고객 데이터·챗봇을 시연하려고 만든 **데모 쇼핑몰**입니다.
이 저장소에는 그 데모의 **AI로 생성한 가상 상품 사진**이 있습니다. **실제 상점이 아니며**, 사진 속 상품·브랜드·모델은 실존하지 않습니다.

- 사진 파일 안에는 AI 생성 표시가 기계가 읽을 수 있는 형태로 들어 있습니다
  (XMP의 IPTC `DigitalSourceType = trainedAlgorithmicMedia`). 파일은 원본 그대로 올리며 다시 압축하지 않습니다.
- 사람이 보는 표시("✦ AI 생성")는 사진을 보여 주는 화면(데모 사이트, 아래 갤러리)이 사진 위에 붙입니다.

## 주소 형식

```
https://bhson-appier.github.io/super-yuja-storage/<버티컬>/<상품ID>/<그룹>/<종류>-<순번>-<sha8>.jpg
```

| 부분 | 뜻 |
|---|---|
| 버티컬 | 상품 부문(예: `fashion`) |
| 상품ID | 데모 상품 ID(예: `FA-OU-0001`) |
| 그룹 | 사진이 속한 색상 코드(예: `camel`), 없으면 `_` |
| 종류 | `main`(상품 사진) · `model`(착용 사진) |
| 순번 | 같은 그룹·종류 안의 차례(1부터) |
| sha8 | 파일 내용의 SHA-256 앞 8자리 |

- **파일은 제자리에서 바뀌지 않습니다.** 사진이 바뀌면 내용이 달라져 새 이름이 생깁니다. 그래서 오래 캐시해도 됩니다.
- 대체된 옛 파일은 14일 동안 남겨 두었다가 지웁니다(`_state.json`).
- 기획전 그림은 `promo/<기획전ID>/<역할>-<순번>-<sha8>.jpg`(역할 `intro` 소개 사진 · `slide` 정사각 배너 · `banner` 가로 배너), 목록은 `promo/index.json`.
- 사진마다 같은 이름에 `-w640.webp`·`-w960.webp`를 붙인 **크기별 WebP 사본**이 있습니다(원본보다 넓은 사본은 만들지 않음, 메타데이터 포함). 데모 사이트는 이 사본을 브라우저가 바로 받습니다.
- 버티컬마다 `<버티컬>/index.json`에 상품별 대표 사진(`default_main`)·대표 착용 사진(`default_model`)과 모든 사진이 있습니다.
  `placeholder: true`는 사진이 승인되기 전까지 쓰는 **임시 그림**(AI 생성 아님)입니다.
- 갤러리: https://bhson-appier.github.io/super-yuja-storage/

이 저장소는 스크립트(`scripts/storage/sync_image_storage.py`, 데모 저장소)가 만듭니다. 직접 고치지 마세요.
