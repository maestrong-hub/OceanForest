# 바다숲 복원 (Ocean Forest) — PWA

바다 숲 복원 활동을 기록·공유하는 PWA(설치형 웹앱)입니다. GitHub Pages로 배포한 뒤 PWABuilder로 안드로이드/iOS 앱 패키지를 만들 수 있습니다.

## 폴더 구성
```
index.html          앱 본체 (단일 파일)
manifest.json       PWA 매니페스트
sw.js               서비스 워커 (오프라인 캐시)
privacy_policy.html 개인정보처리방침 (스토어 등록용)
icon-*.png          앱 아이콘 (120~1024)
feature_graphic.png Play 스토어 피처 그래픽 (1024x500)
favicon.png         브라우저 탭 아이콘
.nojekyll           GitHub Pages Jekyll 처리 방지
```

## 1) GitHub에 올리기
1. GitHub에서 새 저장소 생성 (예: `oceanforest`)
2. 이 폴더(`oceanforest-pwa`)의 **내용물 전체**를 저장소 루트에 올립니다.
   ```bash
   git init
   git add .
   git commit -m "바다숲 복원 PWA"
   git branch -M main
   git remote add origin https://github.com/<사용자명>/oceanforest.git
   git push -u origin main
   ```

## 2) GitHub Pages 켜기
1. 저장소 → **Settings → Pages**
2. **Source**: `Deploy from a branch`
3. **Branch**: `main` / `/ (root)` → Save
4. 1~2분 뒤 `https://<사용자명>.github.io/oceanforest/` 주소가 생성됩니다.

## 3) PWA 동작 확인
- 위 주소를 모바일 크롬에서 열면 "홈 화면에 추가" 배너가 뜹니다.
- 데스크톱 크롬: 주소창 오른쪽 설치(⊕) 아이콘.
- 크롬 DevTools → **Application → Manifest / Service Workers**에서 정상 등록 확인.

## 4) 앱으로 패키징 (스토어 업로드)
[PWABuilder](https://www.pwabuilder.com) 사용:
1. 배포된 Pages 주소 입력 → 스캔
2. **Android (TWA)** 패키지 다운로드 → Play Console 업로드
   - `.aab` 서명 후 업로드. TWA 도메인 인증을 위해 `assetlinks.json` 설정 필요.
3. **iOS** 패키지 다운로드 → Xcode로 빌드 → App Store Connect 업로드

> 참고: 매니페스트의 `start_url`/`scope`는 상대경로(`./`)라 저장소 이름이 바뀌어도 동작합니다.
> 앱 내용을 수정하면 `sw.js`의 `CACHE` 버전(`oceanforest-v1` → `v2`)을 올려야 사용자에게 갱신이 반영됩니다.
