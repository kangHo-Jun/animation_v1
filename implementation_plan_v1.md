# 대장간 인덱스 페이지 애니메이션 교체 계획 (v1)

이 계획은 '대장간' 브랜드의 정체성을 살려 **미니멀하고 프리미엄한 다크 모드** 디자인을 적용합니다. 기존 4개의 버튼을 2개로 압축하고, 더 역동적인 `WAVES` 애니메이션 효과를 사용합니다.

## 디자인 컨셉
- **브랜드명**: '대장간' (기존 창원목재에서 변경)
- **포인트 컬러**: **Amber/Gold (#FFAB40)** - 타오르는 불꽃과 프리미엄 금속의 느낌
- **애니메이션**: **Vanta.js WAVES** - 부드럽고 세련된 파동 효과로 '깔끔함' 극대화
- **레이아웃**: 2개의 가로형 와이드 버튼으로 시각적 안정감과 가독성 확보

## Proposed Changes

### [MODIFY] index.html (스마트 에디터)

#### 1단계: 기존 코드 삭제
`index.html` 파일의 **4행**에 있는 아래 코드를 삭제합니다.
```html
<!--@import(/smart-banner/shop1/smart-banner-admin-RES00001.html)-->
```

#### 2단계: 신규 v1 코드 삽입
삭제한 위치에 아래의 프리미엄 코드를 삽입합니다.

```html
<!-- 대장간 프리미엄 애니메이션 v1 시작 -->
<style>
    @import url('https://fonts.googleapis.com/css2?family=Outfit:wght@400;700;900&display=swap');

    .forge-hero {
        position: relative;
        width: 100%;
        min-height: 550px;
        display: flex;
        align-items: center;
        justify-content: center;
        background-color: #050505;
        overflow: hidden;
        font-family: 'Outfit', 'Noto Sans KR', sans-serif;
    }
    #vanta-waves {
        position: absolute;
        top: 0; left: 0;
        width: 100% !important; height: 100% !important;
        z-index: 0;
    }
    .forge-container {
        position: relative;
        z-index: 10;
        width: 90%;
        max-width: 1100px;
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
        color: #fff;
        pointer-events: none;
    }
    .forge-container > * { pointer-events: auto; }

    .forge-label {
        font-size: 0.9rem;
        letter-spacing: 0.3em;
        color: #FFAB40;
        font-weight: 700;
        margin-bottom: 20px;
        text-transform: uppercase;
        opacity: 0;
        animation: fadeInUp 0.8s forwards 0.2s;
    }
    .forge-title {
        font-size: clamp(3rem, 10vw, 5.5rem);
        font-weight: 900;
        margin: 0 0 15px 0;
        line-height: 1;
        letter-spacing: -0.02em;
        opacity: 0;
        animation: fadeInUp 0.8s forwards 0.4s;
    }
    .forge-desc {
        font-size: 1.1rem;
        font-weight: 400;
        opacity: 0;
        margin-bottom: 50px;
        letter-spacing: 0.05em;
        color: rgba(255, 255, 255, 0.7);
        animation: fadeInUp 0.8s forwards 0.6s;
    }

    .forge-buttons {
        display: flex;
        gap: 20px;
        width: 100%;
        max-width: 600px;
        opacity: 0;
        animation: fadeInUp 0.8s forwards 0.8s;
    }
    .forge-btn {
        flex: 1;
        padding: 22px;
        background: rgba(255, 255, 255, 0.03);
        border: 1px solid rgba(255, 255, 255, 0.1);
        backdrop-filter: blur(15px);
        border-radius: 12px;
        color: #fff;
        text-decoration: none;
        font-weight: 700;
        font-size: 1.1rem;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 12px;
        transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
    }
    .forge-btn i { font-size: 1.2rem; color: #FFAB40; transition: transform 0.3s; }
    .forge-btn:hover {
        background: rgba(255, 255, 255, 0.08);
        border-color: #FFAB40;
        transform: translateY(-5px);
        box-shadow: 0 15px 30px rgba(0,0,0,0.3);
    }
    .forge-btn:hover i { transform: scale(1.2); }

    @keyframes fadeInUp {
        from { opacity: 0; transform: translateY(30px); }
        to { opacity: 1; transform: translateY(0); }
    }

    @media (max-width: 768px) {
        .forge-buttons { flex-direction: column; gap: 12px; }
        .forge-hero { min-height: 600px; }
        .forge-title { font-size: 3rem; }
    }
</style>

<section class="forge-hero">
    <div id="vanta-waves"></div>
    <div class="forge-container">
        <span class="forge-label">Premium Tools & Craft</span>
        <h1 class="forge-title">대장간</h1>
        <p class="forge-desc">장인의 정신으로 빚어낸 완벽한 결과물</p>
        
        <div class="forge-buttons">
            <a href="/product/list.html" class="forge-btn">
                <i class="fas fa-th-large"></i>
                <span>전체상품</span>
            </a>
            <a href="/board/free/list.html" class="forge-btn">
                <i class="fas fa-file-invoice-dollar"></i>
                <span>최신 단가표</span>
            </a>
        </div>
    </div>
</section>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r134/three.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vanta@latest/dist/vanta.waves.min.js"></script>
<script>
    function startForgeVanta() {
        if (typeof VANTA !== 'undefined') {
            VANTA.WAVES({
                el: "#vanta-waves",
                mouseControls: true, touchControls: true, gyroControls: false,
                minHeight: 200.00, minWidth: 200.00, scale: 1.00, scaleMobile: 1.00,
                color: 0x080808, shininess: 35.00, waveHeight: 20.00, waveSpeed: 0.80, zoom: 0.95
            });
        }
    }
    if (document.readyState === 'complete') { startForgeVanta(); }
    else { window.addEventListener('load', startForgeVanta); }
</script>
<!-- 대장간 프리미엄 애니메이션 v1 끝 -->
```

## Verification Plan
1. **브랜드명 확인**: 타이틀이 '대장간'으로 정확히 출력되는지 확인.
2. **버튼 개수 및 가독성**: 버튼이 2개이며 와이드형으로 깔끔하게 배치되는지 확인.
3. **애니메이션 품질**: Vanta WAVES 배경이 부드럽게 구동되는지 확인.
4. **모바일 최적화**: 모바일 환경에서 텍스트와 버튼이 적절한 크기로 재배치되는지 확인.
