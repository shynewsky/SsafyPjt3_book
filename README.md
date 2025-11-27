# ThRead – 메인 페이지

AI 기반 도서 분석·창작 지원 서비스 **ThRead**의 메인 화면입니다. Bootstrap 5.3과 커스텀 CSS 토큰으로 반응형 UI를 구성했습니다.

## 사용 기술 & 실행
- **Bootstrap 5.3.3 (CDN)** 사용
- **CSS 디자인 토큰**: `--brand-red`, `--section-gap`
- 실행 방법: 저장소를 내려받고 `06-main.html`을 브라우저로 열면 동작합니다(CDN 연결 필요).

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
```

---

## 핵심 기능 (설명 + 짤막한 핵심 코드)

### 1) 네비게이션 (히어로 위 절대 배치)
**구현 방법**: 헤더를 `position:absolute`로 히어로 상단에 겹치고, 412px 이상에서는 메뉴를 항상 펼칩니다. 로그아웃은 모달 트리거로 구현합니다.
```html
<header class="nav-section">
  <nav class="navbar">
    <div class="container">
      <a class="navbar-brand nav-subtitle" href="#">
        <span class="th">Th</span><span class="read">Read</span>
      </a>
      <button class="navbar-toggler" data-bs-toggle="collapse" data-bs-target="#navbarNav">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav nav-menu ms-auto">
          <li class="nav-item"><a class="nav-link" href="#">쓰레드</a></li>
          <li class="nav-item"><a class="nav-link" href="#">도서 검색</a></li>
          <li class="nav-item"><a class="nav-link" href="#">마이 페이지</a></li>
          <li class="nav-item nav-link" role="button" data-bs-toggle="modal" data-bs-target="#logoutModal">로그아웃</li>
        </ul>
      </div>
    </div>
  </nav>
</header>
```
```css
.nav-section{position:absolute;inset:0 auto auto 0;width:100%;z-index:1000}
@media (min-width:412px){
  .navbar .navbar-collapse{display:flex!important;flex-basis:auto}
  .navbar .navbar-nav{flex-direction:row}
  .navbar .navbar-toggler{display:none}
}
```

### 2) 히어로 섹션 (풀블리드 이미지 + 어두운 오버레이)
**구현 방법**: 배경 이미지를 `object-fit:cover`로 전 화면 채우고, 오버레이로 대비를 확보합니다. 콘텐츠는 z-index로 위에 위치.
```html
<section class="hero-section">
  <img src="assets/nav/hero_image.jpg" class="hero-img" alt="Hero">
  <div class="hero-overlay"></div>
  <div class="hero-content">
    <h1 class="hero-title">AI 기반 도서 분석 및<br class="d-412-deactivate"> 창작 지원 통합 솔루션 서비스</h1>
    <div class="hero-subtitle"><span class="th">Th</span><span class="read">Read</span></div>
  </div>
</section>
```
```css
.hero-section{min-height:80vh;position:relative;display:flex;align-items:center;justify-content:center;color:#fff}
.hero-img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;z-index:1}
.hero-overlay{position:absolute;inset:0;background:rgba(0,0,0,.5);z-index:2}
.hero-content{position:relative;z-index:3}
```

### 3) 베스트셀러 캐러셀 (자동 슬라이드 + 커스텀 Next 버튼)
**구현 방법**: Bootstrap Carousel에 자동 전환/순환 속성을 부여하고, Next 버튼을 원형·반투명 스타일로 커스텀합니다.
```html
<div id="bestsellerCarousel" class="carousel slide"
     data-bs-ride="carousel" data-bs-interval="2500" data-bs-pause="false" data-bs-wrap="true">
  <div class="carousel-inner">
    <div class="carousel-item active">…책 4개…</div>
    <div class="carousel-item">…책 4개…</div>
    <div class="carousel-item">…책 4개…</div>
  </div>
  <button class="carousel-control-next" type="button" data-bs-target="#bestsellerCarousel" data-bs-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span>
  </button>
</div>
```
```css
.bestseller .carousel-control-next{
  right:20px;top:50%;transform:translateY(-50%);
  width:56px;height:56px;display:flex;align-items:center;justify-content:center;opacity:1
}
.bestseller .carousel-control-next .carousel-control-next-icon{
  width:56px;height:56px;border-radius:50%;
  background-color:rgba(254,74,81,.35);background-size:40% 40%;box-shadow:0 2px 8px rgba(0,0,0,.15)
}
```

### 4) AI 추천 (7:5 레이아웃, 모바일 스택)
**구현 방법**: `row` 내부에서 좌측 `col-lg-7`(이미지), 우측 `col-lg-5`(텍스트) 비율. 576px 이하에서 세로 스택.
```html
<section class="section-block">
  <div class="ai-recommendation">
    <div class="row align-items-center ai-gap">
      <div class="col-12 col-lg-7">
        <div class="ai-books d-flex">
          <img src="assets/ai_recommendation/img1.jpeg" class="ai-bk">
          <img src="assets/ai_recommendation/img2.jpeg" class="ai-bk ai-bk-lg">
          <img src="assets/ai_recommendation/img3.jpeg" class="ai-bk">
        </div>
      </div>
      <div class="col-12 col-lg-5 text-center text-lg-start">
        <h3 class="section-title">AI 추천</h3>
        <p class="text-muted">사용자 <span class="ai-emph">활동 데이터 기반</span> 추천</p>
      </div>
    </div>
  </div>
</section>
```
```css
.ai-recommendation{width:80%;margin-inline:auto}
.ai-books{gap:24px;justify-content:center}
@media (max-width:575.98px){.ai-books{flex-direction:column;align-items:center;gap:16px}}
```

### 5) 장르별 도서 (4열 그리드 → 412px 이하 1열)
**구현 방법**: Bootstrap `row` + `col-3`로 4열 배치, 412px 이하에서 1열로 강제. 장르 라벨은 `position:absolute`로 배치.
```html
<section class="genre-books container">
  <h3 class="section-title">장르별 도서 목록</h3>
  <div class="genre-list row">
    <div class="genre-item col-3"><img src="assets/genre/travel.jpg"><span class="sctext">여행</span></div>
    <!-- …다른 장르 항목들… -->
  </div>
</section>
```
```css
.genre-list{display:flex;flex-wrap:wrap;justify-content:flex-start}
.genre-item{position:relative;margin:20px 0}
.sctext{position:absolute;left:20px;bottom:10px;color:#fff}
@media (max-width:411.98px){.genre-list .genre-item{flex:0 0 100%!important;max-width:100%!important}}
```

### 6) 지금 이 쓰레드 (카드 3열, 고정 높이 이미지)
**구현 방법**: Bootstrap Card로 이미지/제목/요약/저자+도서명을 구성하고, 이미지 높이를 고정하여 균일한 카드 높이를 유지합니다.
```html
<section class="thread container text-center">
  <div class="card-list row g-4">
    <div class="card-item col-4">
      <div class="card h-100">
        <img src="assets/threads/img1.jpg" class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">상실의 아픔을 넘어 빛으로</h5>
          <p class="card-text">…요약…</p>
        </div>
        <p class="md-auto card-author">최민정 | <span>다시 피어나는 꽃처럼</span></p>
      </div>
    </div>
    <!-- …동일 패턴 반복… -->
  </div>
</section>
```
```css
.card img{width:100%;height:150px;object-fit:cover;object-position:center}
.card-title{font-size:14px;font-weight:bold}
.card-text{font-size:12px}
.card-author{font-size:12px;color:gray}
.card-author span{color:#fe4a51}
@media (max-width:411.98px){.card-list .card-item{flex:0 0 100%!important;max-width:100%!important}}
```

### 7) 페이지네이션 (테두리 제거·투명 배경·활성 색상)
**구현 방법**: `.border-0 .bg-transparent`로 외곽선/배경 제거, 활성 페이지 링크는 `text-danger`(브랜드 톤)로 강조.
```html
<nav aria-label="Page">
  <ul class="pagination justify-content-center">
    <li class="page-item"><a class="page-link border-0 bg-transparent text-danger" href="#">1</a></li>
    <li class="page-item"><a class="page-link border-0 bg-transparent text-body-secondary" href="#">2</a></li>
    <li class="page-item"><a class="page-link border-0 bg-transparent text-body-secondary" href="#">3</a></li>
  </ul>
</nav>
```

### 8) 로그아웃 모달 (중앙 정렬 + 브랜드 버튼)
**구현 방법**: Bootstrap Modal을 사용해 확인 UI를 제공하고, `.btn-brand`로 브랜드 색상을 적용합니다.
```html
<div class="modal fade" id="logoutModal" tabindex="-1">
  <div class="modal-dialog modal-dialog-centered">
    <div class="modal-content border-0 rounded-3">
      <button class="btn-close ms-auto me-2 mt-2" data-bs-dismiss="modal"></button>
      <div class="modal-body text-center pt-5"><p class="fs-3 m-0">정말 로그아웃 하시겠습니까?</p></div>
      <div class="modal-footer justify-content-center gap-2 border-0 py-5">
        <button type="button" class="btn btn-outline-secondary px-4" data-bs-dismiss="modal">취소</button>
        <button type="button" class="btn btn-brand px-4" id="btnLogout">로그아웃</button>
      </div>
    </div>
  </div>
</div>
```
```css
.btn-brand{background:#fe4a51;border-color:#fe4a51;color:#fff}
.btn-brand:hover{background:#e8434a;border-color:#e8434a}
```

### 9) 푸터
**구현 방법**: 어두운 배경/연한 텍스트, 중앙 정렬된 컨테이너로 간결하게 마무리합니다.
```html
<footer class="site-footer">
  <div class="container text-center">© 2025 ThRead</div>
</footer>
```
```css
.site-footer{background:#1f2226;color:#cbd1d8;padding:24px 0;font-size:.9rem}
```

---

## 반응형 & 접근성 포인트
- **412px 이상**: 햄버거 숨김·항상 펼침(`@media(min-width:412px)`), 특정 줄바꿈 요소 비활성화(`.d-412-deactivate`).
- **576px 이하**: AI 추천 이미지 열 배치 → 세로 스택.
- **브랜드 토큰** `--brand-red`로 버튼/텍스트 강조 일관성 유지.

## 자산(Assets) 구조
```
assets/
 ├─ nav/hero_image.jpg
 ├─ bestsellers/img1.jpeg … img12.jpeg
 ├─ ai_recommendation/img1.jpeg … img3.jpeg
 ├─ genre/*.jpg
 └─ threads/*.jpg
```
