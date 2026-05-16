# LL 웹사이트 수정 가이드

이 가이드는 LL (Lonely Legacy) 웹사이트의 index.html 파일을 직접 수정할 때 필요한 정보를 제공합니다.

## 파일 위치
- `index.html`: 메인 웹페이지 파일
- 모든 HTML, CSS, JavaScript가 단일 파일에 통합되어 있습니다.

## 크롬하츠 스타일 미니멀 메뉴 시스템

### 메뉴 버튼 (LL 엠블럼)
**위치**: HTML `<div class="header-left">` 내부 (약 426번째 줄)
```html
<div class="menu-btn" id="menuBtn">
    <img src="assets/ll-emblem.png" alt="LL Menu">
</div>
```
- LL 브랜드 엠블럼 PNG 이미지를 사용합니다.
- 이미지 경로: `assets/ll-emblem.png`
- 크기: 50px x 100px (50px~100px 내외 권장)
- z-index: 9999로 설정되어 항상 최상단에 표시됩니다.
- 호버 시 투명도 0.6, 확대 1.05배 효과가 적용됩니다.

### 미니멀 메뉴 텍스트 컨테이너
**위치**: CSS `.menu-text-container` 클래스 (약 152번째 줄)
```css
.menu-text-container {
    position: fixed;
    top: 280px;
    left: 50px;
    z-index: 9998;
    display: flex;
    flex-direction: column;
    gap: 25px;
    opacity: 0;
    visibility: hidden;
    transition: opacity 0.4s ease, visibility 0.4s ease;
}
```
- **박스 배경 없음**: 베이지 배경 위에 텍스트만 투명하게 노출
- **위치**: 버튼 직하단 (top: 280px, left: 50px) - 엠블럼과 간격 2배
- **z-index**: 9998 (메뉴 버튼 바로 아래)
- **애니메이션**: 페이드인/페이드아웃 (0.4초)
- **메뉴 순서**: SHOP → ARCHIVE → EDITORIAL

### 메뉴 텍스트 아이템
**위치**: CSS `.menu-text-item` 클래스 (약 172번째 줄)
```css
.menu-text-item {
    font-family: 'Times New Roman', Georgia, serif;
    font-size: 16px;
    font-weight: bold;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: #1a1a1a;
    cursor: pointer;
    transition: opacity 0.3s ease, letter-spacing 0.3s ease;
}
```
- **폰트**: 세리프 (Times New Roman)
- **스타일**: 대문자, 굵은 글씨
- **자간**: 4px (호버 시 6px로 확장)
- **호버 효과**: 투명도 0.6, 자간 확장

### 메뉴 토글 기능
**위치**: JavaScript (약 485번째 줄)
```javascript
function toggleMenu() {
    isMenuOpen = !isMenuOpen;
    if (isMenuOpen) {
        menuTextContainer.classList.add('active');
    } else {
        menuTextContainer.classList.remove('active');
    }
}
```
- LL 엠블럼 버튼 클릭 시 메뉴 텍스트 페이드인/페이드아웃
- 서브 페이지가 열려있으면 메인으로 돌아감
- 메뉴 텍스트 클릭 시 해당 서브 페이지로 전환

### 섹션 스위칭 기능
**위치**: JavaScript (약 511번째 줄)
```javascript
function switchToPage(pageName) {
    scrollContainer.classList.add('hidden');
    document.querySelectorAll('.sub-page').forEach(page => {
        page.classList.remove('active');
    });
    const targetPage = document.getElementById(pageName + 'Page');
    if (targetPage) {
        targetPage.classList.add('active');
        subPageContainer.classList.add('active');
    }
}
```
- 메인 비주얼 페이드아웃, 서브 페이지 페이드인
- 페이지 전환 시 메뉴 자동 닫힘
- 서브 페이지에서 스크롤 가능

### 메인 페이지 고정 뷰
**위치**: CSS `.scroll-container` 클래스 (약 202번째 줄)
```css
.scroll-container {
    width: 100%;
    height: 100vh;
    overflow: hidden;
}
```
- **스크롤 잠금**: 메인 홈 화면은 스크롤 없이 완전한 고정 뷰
- **높이**: 100vh
- **오버플로우**: hidden

### 서브 페이지 스크롤 허용
**위치**: CSS `.sub-page-container` 클래스 (약 212번째 줄)
```css
.sub-page-container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    overflow-y: auto;
}
```
- **스크롤 허용**: 서브 페이지에서만 스크롤 가능
- **오버플로우**: overflow-y: auto
- **전환**: 페이드인/페이드아웃 (0.5초)

### Shop 페이지 제품 그리드
**위치**: CSS `.product-grid` 클래스 (약 316번째 줄)
```css
.product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 40px;
    margin-top: 50px;
}
```
- **레이아웃**: 그리드 형태 (반응형)
- **최소 너비**: 300px
- **간격**: 40px

### Shop 페이지 업로드 폼
**위치**: CSS `.upload-section` 클래스 (약 367번째 줄)
```css
.upload-section {
    margin-top: 80px;
    padding: 40px;
    background: rgba(245, 240, 232, 0.5);
    border: 1px solid rgba(0, 0, 0, 0.1);
}
```
- **위치**: 제품 그리드 하단
- **배경**: 반투명 베이지
- **기능**: 제품 이름, 가격, 설명, 이미지 URL 입력 폼

## 이미지 수정 방법

### 1. 백그라운드 이미지
**위치**: CSS `.background-image` 클래스 (약 45번째 줄)
```css
.background-image {
    background-image: url('web_source/shop_background.jpg');
    opacity: 0.15;
}
```
- 베이지/화이트 톤의 추상적인 질감 이미지 URL로 교체하세요.
- `opacity` 값으로 배경 이미지의 투명도를 조절할 수 있습니다 (0.0 ~ 1.0).

### 2. LL 로고 이미지
**위치**: HTML `<div class="logo-container">` 내부 (약 215번째 줄)
```html
<a href="#" class="logo-placeholder">
    <!-- <img src="LOGO_IMAGE_URL_HERE" alt="LL Logo"> -->
    L O N E L Y &nbsp;&nbsp; L E G A C Y
</a>
```
- 주석 처리된 `<img>` 태그의 주석을 제거하고 `src`에 로고 이미지 URL을 넣으세요.
- 텍스트 플레이스홀더는 삭제하거나 주석 처리하세요.

### 3. 실버 메탈 오브젝트 이미지 (메인 섹션)
**위치**: HTML `<section class="section section-1">` 내부 (약 245번째 줄)
```html
<img src="https://images.unsplash.com/photo-1611591437281-460bfbe1220a?w=800&q=80" 
     alt="Silver Object" 
     class="silver-object" 
     id="silverObject">
```
- `src`에 실버/메탈 오브젝트의 고화질 이미지 URL을 넣으세요.

### 4. 실버 메탈 오브젝트 시퀀스 이미지 배열
**위치**: JavaScript `objectImages` 배열 (약 330번째 줄)
```javascript
const objectImages = [
    'https://images.unsplash.com/photo-1611591437281-460bfbe1220a?w=800&q=80',
    'https://images.unsplash.com/photo-1611186871348-b1ce696e52c9?w=800&q=80',
    'https://images.unsplash.com/photo-1605146769289-440113cc3d00?w=800&q=80',
    'https://images.unsplash.com/photo-1616401784845-180882ba9ba8?w=800&q=80',
    'https://images.unsplash.com/photo-1579546929518-9e396f3cc809?w=800&q=80'
];
```
- 스크롤 시 순차적으로 표시될 이미지 URL들을 배열로 넣으세요.
- 이미지 개수는 자유롭게 추가/삭제할 수 있습니다.

## 인스타그램 링크 수정
**위치**: HTML `<footer>` 내부 (약 265번째 줄)
```html
<a href="https://www.instagram.com/lonelylegacyxx/" target="_blank" class="instagram-link">
```
- `href` 속성에 인스타그램 계정 URL을 수정하세요.

## 색상 수정
**위치**: CSS 상단 (약 30-35번째 줄)
```css
body {
    background-color: #F5F0E8;
    color: #1a1a1a;
}
```
- `background-color`: 배경 색상 (현재 베이지 톤)
- `color`: 텍스트 색상 (현재 다크 그레이)

## 폰트 수정
**위치**: CSS `body` 선택자 (약 30번째 줄)
```css
body {
    font-family: 'Times New Roman', Georgia, serif;
}
```
- 원하는 세리프 폰트로 변경하세요.

## 섹션 내용 수정
### 섹션 2: SOUND & VISUAL ARCHIVE
**위치**: HTML `<section class="section section-2">` 내부 (약 253번째 줄)
- 제목과 설명 텍스트를 자유롭게 수정하세요.

### 섹션 3: PRODUCT LAB
**위치**: HTML `<section class="section section-3">` 내부 (약 261번째 줄)
- 제목과 설명 텍스트를 자유롭게 수정하세요.

## 메뉴 항목 수정
**위치**: HTML `<div class="menu-items">` 내부 (약 227번째 줄)
```html
<div class="menu-items">
    <a href="#" class="menu-item">ARCHIVE</a>
    <a href="#" class="menu-item">EDITORIAL</a>
    <a href="#" class="menu-item">SHOP</a>
</div>
```
- 메뉴 항목의 텍스트와 링크를 수정하세요.

## 로컬 서버 실행 방법
### 방법 1: Python (권장)
```bash
cd "c:/Users/windows10/Desktop/LL true shop"
python -m http.server 8000
```
- 브라우저에서 `http://localhost:8000` 접속

### 방법 2: Node.js (http-server)
```bash
cd "c:/Users/windows10/Desktop/LL true shop"
npx http-server -p 8000
```
- 브라우저에서 `http://localhost:8000` 접속

### 방법 3: VS Code Live Server
- VS Code의 "Live Server" 확장프로그램 설치
- index.html 파일 우클릭 → "Open with Live Server"

## 주요 기능 설명

### 1. 마그네틱 스크롤
- CSS Scroll Snap으로 구현
- 스크롤 시 각 섹션에 자석처럼 걸리는 효과

### 2. 메뉴 오버레이
- 왼쪽 상단 "MENU +" 클릭 시 슬라이딩 메뉴 표시
- "CLOSE" 또는 메뉴 항목 클릭 시 닫힘

### 3. 실버 오브젝트 시퀀스
- 첫 번째 섹션에서 스크롤 시 이미지 순차 변경
- 호버 시 확대 효과

### 4. 로고 드래그 앤 드롭
- 중앙 상단 로고를 드래그하여 바탕화면/폴더에 드롭
- 웹사이트 URL 바로가기 파일 생성

### 5. 반응형 디자인
- 모바일/태블릿/데스크톱 대응
- 화면 크기에 따라 자동 조절

## 주의사항
- 이미지 URL은 반드시 유효한 외부 링크여야 합니다.
- 로컬 이미지를 사용하려면 상대 경로를 사용하세요 (예: `./images/logo.png`)
- JavaScript 수정 시 주석을 참고하여 기능이 깨지지 않도록 주의하세요.
