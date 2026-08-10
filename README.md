<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Color Floyds — Hand Made Acrylic Paintings</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,500;0,9..144,600;0,9..144,700;1,9..144,500&family=Space+Grotesk:wght@400;500;600;700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<!-- EmailJS SDK -->
<script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
<style>
  :root{
    --ink:#15141a;
    --ink-soft:#242230;
    --canvas:#faf6ef;
    --canvas-dim:#f0e9db;
    --red:#e2472b;
    --blue:#2c5aa3;
    --yellow:#eeb50a;
    --green:#4f8f5b;
    --line: rgba(21,20,26,0.12);
    --shadow: 0 18px 40px -18px rgba(21,20,26,0.35);
    --radius: 18px;
  }
  *{box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  body{
    margin:0;
    background:var(--canvas);
    color:var(--ink);
    font-family:'Space Grotesk', sans-serif;
    -webkit-font-smoothing:antialiased;
  }
  h1,h2,h3{
    font-family:'Fraunces', serif;
    margin:0;
    letter-spacing:-0.01em;
  }
  img{max-width:100%; display:block;}
  a{color:inherit;}
  .price{font-family:'Space Mono', monospace;}

  /* ---------- brushstroke underline signature ---------- */
  .brush-underline{
    position:relative;
    display:inline-block;
  }
  .brush-underline svg{
    position:absolute;
    left:-4%;
    bottom:-0.28em;
    width:108%;
    height:0.5em;
    z-index:-1;
  }

  /* ---------- top bar ---------- */
  .topbar{
    position:sticky; top:0; z-index:40;
    display:flex; align-items:center; justify-content:space-between;
    padding:18px 6vw;
    background:rgba(250,246,239,0.86);
    backdrop-filter:blur(10px);
    border-bottom:1px solid var(--line);
  }
  .brand{
    display:flex; align-items:center; gap:10px;
    font-family:'Fraunces', serif;
    font-weight:700;
    font-size:1.35rem;
  }
  .brand .dot{
    width:14px; height:14px; border-radius:40% 60% 55% 45%/50% 45% 55% 50%;
    background:conic-gradient(from 90deg, var(--red), var(--yellow), var(--blue), var(--green), var(--red));
    box-shadow: 0 2px 6px rgba(0,0,0,0.25);
  }
  .brand small{
    display:block;
    font-family:'Space Grotesk', sans-serif;
    font-weight:400;
    font-size:0.62rem;
    letter-spacing:0.14em;
    text-transform:uppercase;
    color:var(--ink-soft);
    opacity:0.65;
  }
  .top-actions{display:flex; align-items:center; gap:14px;}
  .icon-btn{
    position:relative;
    width:44px; height:44px;
    border-radius:50%;
    border:1px solid var(--line);
    background:var(--canvas);
    display:flex; align-items:center; justify-content:center;
    cursor:pointer;
    transition:transform .15s ease, box-shadow .15s ease;
  }
  .icon-btn:hover{ transform:translateY(-2px); box-shadow:var(--shadow); }
  .badge{
    position:absolute; top:-6px; right:-6px;
    min-width:20px; height:20px; padding:0 4px;
    border-radius:50%;
    background:var(--red); color:#fff;
    font-size:0.7rem; font-weight:700;
    display:flex; align-items:center; justify-content:center;
    font-family:'Space Grotesk', sans-serif;
  }

  /* ---------- hero ---------- */
  .hero{
    position:relative;
    min-height:88vh;
    display:flex; align-items:center;
    overflow:hidden;
    padding:0 6vw;
    /* NOTE: swap this gradient for background-image:url('YOUR-HERO-IMAGE-URL') once you have the correct direct image link.
       The ibb.co link supplied resolved to an unrelated stock photo, so a painterly gradient placeholder is used instead. */
    background:
      radial-gradient(circle at 82% 20%, rgba(226,71,43,0.55), transparent 45%),
      radial-gradient(circle at 68% 70%, rgba(44,90,163,0.5), transparent 50%),
      radial-gradient(circle at 95% 55%, rgba(238,181,10,0.45), transparent 45%),
      linear-gradient(160deg, var(--ink) 0%, #1d1b26 55%, #201a2b 100%);
  }
  .hero::after{
    content:"";
    position:absolute; inset:0;
    background-image:
      radial-gradient(rgba(255,255,255,0.05) 1px, transparent 1px);
    background-size:22px 22px;
    opacity:0.5;
    pointer-events:none;
  }
  .hero-inner{
    position:relative; z-index:2;
    max-width:640px;
    padding:64px 0;
  }
  .eyebrow{
    display:inline-flex; align-items:center; gap:8px;
    font-size:0.72rem; letter-spacing:0.18em; text-transform:uppercase;
    color:#f4ead9; opacity:0.8; margin-bottom:20px;
  }
  .eyebrow::before{
    content:""; width:26px; height:2px; background:var(--yellow);
  }
  .hero h1{
    color:var(--canvas);
    font-size:clamp(2.6rem, 6vw, 4.6rem);
    line-height:1.02;
    font-weight:600;
  }
  .hero h1 em{
    font-style:italic;
    font-weight:500;
    background:linear-gradient(100deg, var(--yellow), var(--red) 60%, var(--blue));
    -webkit-background-clip:text;
    background-clip:text;
    color:transparent;
  }
  .hero p{
    color:#e8e1d2;
    font-size:1.05rem;
    max-width:460px;
    margin:22px 0 34px;
    line-height:1.6;
    opacity:0.85;
  }
  .btn{
    appearance:none; border:none; cursor:pointer;
    font-family:'Space Grotesk', sans-serif;
    font-weight:600;
    font-size:0.95rem;
    border-radius:999px;
    padding:16px 30px;
    display:inline-flex; align-items:center; gap:10px;
    transition:transform .18s ease, box-shadow .18s ease, background .18s ease;
  }
  .btn-primary{
    background:var(--canvas);
    color:var(--ink);
  }
  .btn-primary:hover{ transform:translateY(-3px); box-shadow:0 14px 30px -10px rgba(0,0,0,0.5); }
  .btn-primary svg{ transition:transform .18s ease; }
  .btn-primary:hover svg{ transform:translateX(3px); }

  /* ---------- section shell ---------- */
  section{ padding:96px 6vw; }
  .section-head{
    display:flex; align-items:flex-end; justify-content:space-between;
    gap:24px; margin-bottom:44px; flex-wrap:wrap;
  }
  .section-eyebrow{
    font-size:0.72rem; letter-spacing:0.18em; text-transform:uppercase;
    color:var(--red); font-weight:700; margin-bottom:10px; display:block;
  }
  .section-head h2{ font-size:clamp(1.8rem, 3.4vw, 2.6rem); font-weight:600; }
  .section-head p{ max-width:360px; color:var(--ink-soft); opacity:0.75; line-height:1.6; margin:0;}

  /* ---------- carousel ---------- */
  .carousel-wrap{ position:relative; }
  .carousel{
    display:flex; gap:22px;
    overflow-x:auto;
    scroll-snap-type:x mandatory;
    padding:10px 4px 26px;
    scrollbar-width:thin;
    scrollbar-color: var(--ink) transparent;
  }
  .carousel::-webkit-scrollbar{ height:6px; }
  .carousel::-webkit-scrollbar-thumb{ background:var(--line); border-radius:10px; }

  .card{
    scroll-snap-align:start;
    flex:0 0 clamp(230px, 68vw, 300px);
    background:#fff;
    border-radius:var(--radius);
    overflow:hidden;
    border:1px solid var(--line);
    box-shadow:0 10px 24px -18px rgba(21,20,26,0.4);
    display:flex; flex-direction:column;
    transition:transform .2s ease, box-shadow .2s ease;
  }
  .card:hover{ transform:translateY(-6px); box-shadow:var(--shadow); }
  .card-media{
    aspect-ratio:1/1;
    background:var(--canvas-dim);
    overflow:hidden;
  }
  .card-media img{ width:100%; height:100%; object-fit:cover; }
  .card-body{ padding:18px 18px 20px; display:flex; flex-direction:column; gap:6px; flex:1;}
  .card-body h3{ font-size:1.08rem; font-weight:600; }
  .card-tag{ font-size:0.78rem; color:var(--ink-soft); opacity:0.6; }
  .card-foot{
    margin-top:auto;
    display:flex; align-items:center; justify-content:space-between;
    padding-top:14px;
  }
  .card-foot .price{ font-size:1.02rem; font-weight:700; }
  .add-btn{
    border:1px solid var(--ink);
    background:transparent;
    color:var(--ink);
    border-radius:999px;
    padding:9px 16px;
    font-size:0.82rem; font-weight:600;
    cursor:pointer;
    font-family:'Space Grotesk', sans-serif;
    transition:all .18s ease;
  }
  .add-btn:hover{ background:var(--ink); color:#fff; }
  .add-btn.added{ background:var(--green); border-color:var(--green); color:#fff; }

  .carousel-nav{
    display:flex; gap:10px; justify-content:flex-end; margin-top:8px;
  }
  .nav-btn{
    width:42px; height:42px; border-radius:50%;
    border:1px solid var(--line); background:#fff; cursor:pointer;
    display:flex; align-items:center; justify-content:center;
    transition:background .15s ease;
  }
  .nav-btn:hover{ background:var(--canvas-dim); }

  /* ---------- about strip ---------- */
  .about{
    background:var(--ink);
    color:var(--canvas);
    border-radius:28px;
    margin:0 6vw 96px;
    padding:64px 7vw;
    display:grid; grid-template-columns:1.1fr 1fr; gap:48px;
    align-items:center;
  }
  .about h2{ color:var(--canvas); font-size:clamp(1.8rem,3vw,2.4rem); font-weight:600;}
  .about p{ color:#cfc9ba; line-height:1.7; margin-top:16px; }
  .swatches{ display:flex; flex-wrap:wrap; gap:14px; }
  .swatch{
    width:74px; height:74px; border-radius:40% 60% 55% 45%/50% 45% 55% 50%;
  }

  /* ---------- footer ---------- */
  footer{
    padding:56px 6vw 40px;
    border-top:1px solid var(--line);
    display:flex; flex-wrap:wrap; gap:24px; align-items:center; justify-content:space-between;
  }
  footer .f-brand{ font-family:'Fraunces', serif; font-weight:700; font-size:1.2rem; }
  footer .f-links{ display:flex; gap:22px; font-size:0.9rem; opacity:0.75; flex-wrap:wrap;}
  footer .f-links a{ text-decoration:none; }
  footer .f-links a:hover{ text-decoration:underline; }

  /* ---------- floating buttons ---------- */
  .floating-col{
    position:fixed; right:22px; bottom:22px; z-index:60;
    display:flex; flex-direction:column; gap:14px; align-items:flex-end;
  }
  .fab{
    width:58px; height:58px; border-radius:50%;
    display:flex; align-items:center; justify-content:center;
    cursor:pointer; box-shadow:var(--shadow);
    border:none;
    transition:transform .18s ease;
  }
  .fab:hover{ transform:translateY(-3px) scale(1.04); }
  .fab-whatsapp{ background:#25D366; }
  .fab-cart{ background:var(--ink); position:relative; }
  .fab-cart .badge{ top:-4px; right:-4px; background:var(--red); }

  /* ---------- cart drawer ---------- */
  .overlay{
    position:fixed; inset:0; background:rgba(21,20,26,0.5);
    opacity:0; pointer-events:none; transition:opacity .25s ease;
    z-index:70;
  }
  .overlay.open{ opacity:1; pointer-events:auto; }

  .drawer{
    position:fixed; top:0; right:0; height:100%;
    width:min(420px, 92vw);
    background:var(--canvas);
    z-index:80;
    transform:translateX(100%);
    transition:transform .3s cubic-bezier(.4,0,.2,1);
    display:flex; flex-direction:column;
    box-shadow:-20px 0 50px rgba(0,0,0,0.25);
  }
  .drawer.open{ transform:translateX(0); }
  .drawer-head{
    display:flex; align-items:center; justify-content:space-between;
    padding:22px 24px; border-bottom:1px solid var(--line);
  }
  .drawer-head h3{ font-size:1.3rem; font-weight:600;}
  .close-btn{
    width:36px; height:36px; border-radius:50%; border:1px solid var(--line);
    background:transparent; cursor:pointer; display:flex; align-items:center; justify-content:center;
  }
  .drawer-body{ flex:1; overflow-y:auto; padding:16px 24px; }
  .empty-state{
    text-align:center; padding:60px 10px; color:var(--ink-soft); opacity:0.6;
  }
  .cart-item{
    display:flex; gap:14px; padding:16px 0; border-bottom:1px solid var(--line);
  }
  .cart-item img{ width:64px; height:64px; border-radius:12px; object-fit:cover; flex-shrink:0;}
  .ci-info{ flex:1; display:flex; flex-direction:column; gap:4px;}
  .ci-info .name{ font-weight:600; font-size:0.95rem;}
  .ci-row{ display:flex; align-items:center; justify-content:space-between; margin-top:auto;}
  .qty-control{ display:flex; align-items:center; gap:10px; }
  .qty-control button{
    width:26px; height:26px; border-radius:50%; border:1px solid var(--line);
    background:#fff; cursor:pointer; font-weight:700; line-height:1;
  }
  .remove-link{
    background:none; border:none; color:var(--red); font-size:0.78rem; cursor:pointer;
    text-decoration:underline; padding:0; font-family:'Space Grotesk', sans-serif;
  }

  .drawer-foot{
    padding:20px 24px 26px; border-top:1px solid var(--line);
    background:var(--canvas);
  }
  .total-row{ display:flex; justify-content:space-between; font-weight:700; font-size:1.1rem; margin-bottom:16px;}
  .field{ margin-bottom:12px; }
  .field label{ font-size:0.78rem; font-weight:600; display:block; margin-bottom:6px; opacity:0.75;}
  .field input{
    width:100%; padding:12px 14px; border-radius:10px; border:1px solid var(--line);
    font-family:'Space Grotesk', sans-serif; font-size:0.92rem; background:#fff;
  }
  .field input:focus, .field input:focus-visible{ outline:2px solid var(--blue); outline-offset:1px; }
  .send-btn{
    width:100%; margin-top:6px;
    background:var(--red); color:#fff; border:none;
    padding:15px; border-radius:12px; font-weight:700; font-size:0.95rem;
    cursor:pointer; font-family:'Space Grotesk', sans-serif;
    display:flex; align-items:center; justify-content:center; gap:8px;
    transition:background .18s ease;
  }
  .send-btn:hover{ background:#c8371f; }
  .send-btn:disabled{ opacity:0.6; cursor:not-allowed; }
  .status-msg{ margin-top:10px; font-size:0.85rem; text-align:center; }
  .status-msg.ok{ color:var(--green); }
  .status-msg.err{ color:var(--red); }

  :focus-visible{ outline:2px solid var(--blue); outline-offset:2px; }

  @media (max-width:820px){
    .about{ grid-template-columns:1fr; padding:44px 8vw; margin:0 5vw 64px; }
    section{ padding:72px 6vw; }
  }
  @media (prefers-reduced-motion: reduce){
    *{ transition:none !important; scroll-behavior:auto !important; }
  }
</style>
</head>
<body>

<!-- ================= TOP BAR ================= -->
<header class="topbar">
  <div class="brand">
    <span class="dot"></span>
    <span>Color Floyds<br><small>Hand Made Acrylic Paintings</small></span>
  </div>
  <div class="top-actions">
    <button class="icon-btn" id="cartIconTop" aria-label="Open cart">
      <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"/></svg>
      <span class="badge" id="cartCountTop" style="display:none;">0</span>
    </button>
  </div>
</header>

<!-- ================= HERO ================= -->
<section class="hero" style="padding-top:0; padding-bottom:0;">
  <div class="hero-inner">
    <span class="eyebrow">Small batch · Studio made</span>
    <h1>Paintings made<br>by <em>hand</em>, not by<br>machines.</h1>
    <p>Color Floyds is a one-person studio pouring, layering and dragging acrylic paint into originals you won't find anywhere else. Every canvas is one of a kind.</p>
    <button class="btn btn-primary" id="shopNowBtn">
      Shop now
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4"><path d="M5 12h14M13 6l6 6-6 6"/></svg>
    </button>
  </div>
</section>

<!-- ================= PRODUCTS ================= -->
<section id="products">
  <div class="section-head">
    <div>
      <span class="section-eyebrow">The Collection</span>
      <h2 class="brush-underline">Original canvases<svg viewBox="0 0 300 20" preserveAspectRatio="none"><path d="M2 14 C60 4, 120 18, 180 8 S 280 4 298 12" stroke="#eeb50a" stroke-width="7" fill="none" stroke-linecap="round"/></svg></h2>
    </div>
    <p>Scroll through the current pieces. Each one is a single original — once it's sold, it's gone.</p>
  </div>

  <div class="carousel-wrap">
    <div class="carousel" id="carousel"></div>
    <div class="carousel-nav">
      <button class="nav-btn" id="prevBtn" aria-label="Previous">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4"><path d="M15 18l-6-6 6-6"/></svg>
      </button>
      <button class="nav-btn" id="nextBtn" aria-label="Next">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4"><path d="M9 18l6-6-6-6"/></svg>
      </button>
    </div>
  </div>
</section>

<!-- ================= ABOUT ================= -->
<section style="padding-top:0;">
  <div class="about">
    <div>
      <h2 class="brush-underline">Every colour<br>tells on itself<svg viewBox="0 0 260 20" preserveAspectRatio="none"><path d="M2 14 C60 4, 120 18, 180 8 S 250 4 258 12" stroke="#e2472b" stroke-width="7" fill="none" stroke-linecap="round"/></svg></h2>
      <p>No prints, no reproductions — what you see is the exact canvas that ships. Message on WhatsApp for custom sizes, colour ways or commissions.</p>
    </div>
    <div class="swatches" aria-hidden="true">
      <div class="swatch" style="background:var(--red);"></div>
      <div class="swatch" style="background:var(--yellow);"></div>
      <div class="swatch" style="background:var(--blue);"></div>
      <div class="swatch" style="background:var(--green);"></div>
      <div class="swatch" style="background:linear-gradient(135deg,var(--red),var(--yellow));"></div>
      <div class="swatch" style="background:linear-gradient(135deg,var(--blue),var(--green));"></div>
    </div>
  </div>
</section>

<!-- ================= FOOTER ================= -->
<footer>
  <div class="f-brand">Color Floyds</div>
  <div class="f-links">
    <a href="mailto:color.floyds@gmail.com">color.floyds@gmail.com</a>
    <a href="https://wa.me/8217813941" target="_blank" rel="noopener">WhatsApp</a>
  </div>
  <div style="font-size:0.8rem; opacity:0.5;">© <span id="year"></span> Color Floyds. All paintings original.</div>
</footer>

<!-- ================= FLOATING BUTTONS ================= -->
<div class="floating-col">
  <a class="fab fab-whatsapp" href="https://wa.me/8217813941" target="_blank" rel="noopener" aria-label="Chat on WhatsApp">
    <svg width="28" height="28" viewBox="0 0 32 32" fill="#fff"><path d="M16.02 3C9.4 3 4 8.4 4 15.02c0 2.5.72 4.83 1.98 6.8L4 29l7.36-1.93a11.9 11.9 0 0 0 4.66.95h.01c6.62 0 12.02-5.4 12.02-12.02C28.05 8.4 22.65 3 16.02 3zm0 21.8h-.01a9.8 9.8 0 0 1-4.99-1.37l-.36-.21-4.37 1.15 1.17-4.26-.23-.37a9.75 9.75 0 0 1-1.5-5.22c0-5.4 4.4-9.79 9.8-9.79 2.62 0 5.08 1.02 6.93 2.87a9.73 9.73 0 0 1 2.87 6.93c0 5.4-4.4 9.79-9.31 9.27zm5.36-7.34c-.29-.15-1.73-.85-2-.95-.27-.1-.46-.15-.66.15-.2.29-.76.95-.93 1.14-.17.2-.34.22-.63.07-.29-.15-1.23-.45-2.34-1.44-.87-.77-1.45-1.73-1.62-2.02-.17-.29-.02-.45.13-.6.13-.13.29-.34.44-.51.15-.17.2-.29.29-.49.1-.2.05-.37-.02-.51-.07-.15-.66-1.6-.91-2.19-.24-.58-.48-.5-.66-.51-.17-.01-.37-.01-.56-.01-.2 0-.51.07-.78.37-.27.29-1.02 1-1.02 2.44s1.05 2.83 1.19 3.03c.15.2 2.06 3.14 4.99 4.4.7.3 1.24.48 1.67.61.7.22 1.34.19 1.84.12.56-.08 1.73-.71 1.97-1.39.24-.68.24-1.27.17-1.39-.07-.12-.26-.2-.55-.35z"/></svg>
  </a>
  <button class="fab fab-cart" id="cartFab" aria-label="Open cart">
    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="1.8"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"/></svg>
    <span class="badge" id="cartCountFab" style="display:none;">0</span>
  </button>
</div>

<!-- ================= CART DRAWER ================= -->
<div class="overlay" id="overlay"></div>
<aside class="drawer" id="drawer" aria-label="Shopping cart">
  <div class="drawer-head">
    <h3>Your cart</h3>
    <button class="close-btn" id="closeDrawer" aria-label="Close cart">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2"><path d="M18 6 6 18M6 6l12 12"/></svg>
    </button>
  </div>
  <div class="drawer-body" id="drawerBody">
    <div class="empty-state" id="emptyState">
      <p>Your cart is empty.<br>Add a painting to get started.</p>
    </div>
  </div>
  <div class="drawer-foot" id="drawerFoot" style="display:none;">
    <div class="total-row"><span>Total</span><span class="price" id="totalPrice">₹0</span></div>
    <div class="field">
      <label for="custName">Your name</label>
      <input type="text" id="custName" placeholder="Full name" required>
    </div>
    <div class="field">
      <label for="custPhone">Phone number</label>
      <input type="tel" id="custPhone" placeholder="e.g. 9876543210" required>
    </div>
    <button class="send-btn" id="sendOrderBtn">
      Send order
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2"><path d="M22 2 11 13M22 2l-7 20-4-9-9-4 20-7z"/></svg>
    </button>
    <div class="status-msg" id="statusMsg"></div>
  </div>
</aside>

<script>
/* =========================================================
   1) PRODUCT DATA
   Add more products by copying an object into this array.
   ========================================================= */
const PRODUCTS = [
  {
    id: 'p1',
    name: 'Untitled Bloom I',
    price: 2499,
    img: 'https://i.ibb.co/FLpbqw8C/1.png'
  },
  {
    id: 'p2',
    name: 'Untitled Bloom II',
    price: 2799,
    img: 'https://i.ibb.co/C56gxg6k/2.png'
  }
];

/* =========================================================
   2) EMAILJS CONFIG — replace with your own EmailJS values.
   Sign up free at https://www.emailjs.com/
   - Create an Email Service  -> get SERVICE_ID
   - Create an Email Template -> get TEMPLATE_ID
      Template should use variables: {{customer_name}}, {{customer_phone}}, {{order_items}}, {{order_total}}, {{to_email}}
   - Get your Public Key from Account > API Keys
   ========================================================= */
const EMAILJS_PUBLIC_KEY  = 'YOUR_PUBLIC_KEY';
const EMAILJS_SERVICE_ID  = 'YOUR_SERVICE_ID';
const EMAILJS_TEMPLATE_ID = 'YOUR_TEMPLATE_ID';
const OWNER_EMAIL = 'color.floyds@gmail.com';

if (window.emailjs && EMAILJS_PUBLIC_KEY !== 'YOUR_PUBLIC_KEY') {
  emailjs.init({ publicKey: EMAILJS_PUBLIC_KEY });
}

/* =========================================================
   3) CART STATE
   ========================================================= */
let cart = []; // { id, name, price, img, qty }

function formatPrice(n){ return '₹' + n.toLocaleString('en-IN'); }

function addToCart(id){
  const product = PRODUCTS.find(p => p.id === id);
  if(!product) return;
  const existing = cart.find(i => i.id === id);
  if(existing){ existing.qty += 1; }
  else { cart.push({ ...product, qty: 1 }); }
  renderCart();
  flashAdded(id);
}

function changeQty(id, delta){
  const item = cart.find(i => i.id === id);
  if(!item) return;
  item.qty += delta;
  if(item.qty <= 0){ cart = cart.filter(i => i.id !== id); }
  renderCart();
}

function removeItem(id){
  cart = cart.filter(i => i.id !== id);
  renderCart();
}

function cartCount(){ return cart.reduce((sum, i) => sum + i.qty, 0); }
function cartTotal(){ return cart.reduce((sum, i) => sum + i.qty * i.price, 0); }

function flashAdded(id){
  const btn = document.querySelector(`.add-btn[data-id="${id}"]`);
  if(!btn) return;
  const original = btn.textContent;
  btn.textContent = 'Added ✓';
  btn.classList.add('added');
  setTimeout(() => { btn.textContent = original; btn.classList.remove('added'); }, 1100);
}

function renderCart(){
  const count = cartCount();
  [ 'cartCountTop', 'cartCountFab' ].forEach(id => {
    const el = document.getElementById(id);
    el.textContent = count;
    el.style.display = count > 0 ? 'flex' : 'none';
  });

  const body = document.getElementById('drawerBody');
  const foot = document.getElementById('drawerFoot');
  const empty = document.getElementById('emptyState');

  if(cart.length === 0){
    body.innerHTML = '';
    body.appendChild(empty);
    foot.style.display = 'none';
    return;
  }

  foot.style.display = 'block';
  body.innerHTML = cart.map(item => `
    <div class="cart-item">
      <img src="${item.img}" alt="${item.name}">
      <div class="ci-info">
        <span class="name">${item.name}</span>
        <span class="price">${formatPrice(item.price)}</span>
        <div class="ci-row">
          <div class="qty-control">
            <button aria-label="Decrease quantity" onclick="changeQty('${item.id}', -1)">−</button>
            <span>${item.qty}</span>
            <button aria-label="Increase quantity" onclick="changeQty('${item.id}', 1)">+</button>
          </div>
          <button class="remove-link" onclick="removeItem('${item.id}')">Remove</button>
        </div>
      </div>
    </div>
  `).join('');

  document.getElementById('totalPrice').textContent = formatPrice(cartTotal());
}

/* =========================================================
   4) RENDER PRODUCT CAROUSEL
   ========================================================= */
function renderProducts(){
  const carousel = document.getElementById('carousel');
  carousel.innerHTML = PRODUCTS.map(p => `
    <article class="card">
      <div class="card-media"><img src="${p.img}" alt="${p.name}" loading="lazy"></div>
      <div class="card-body">
        <h3>${p.name}</h3>
        <span class="card-tag">Acrylic on canvas</span>
        <div class="card-foot">
          <span class="price">${formatPrice(p.price)}</span>
          <button class="add-btn" data-id="${p.id}" onclick="addToCart('${p.id}')">Add to cart</button>
        </div>
      </div>
    </article>
  `).join('');
}
renderProducts();
renderCart();
document.getElementById('year').textContent = new Date().getFullYear();

/* =========================================================
   5) CAROUSEL AUTO-SLIDE + ARROWS
   ========================================================= */
const carouselEl = document.getElementById('carousel');
let autoTimer;

function startAutoSlide(){
  stopAutoSlide();
  autoTimer = setInterval(() => {
    const cardWidth = carouselEl.querySelector('.card')?.offsetWidth || 280;
    const atEnd = carouselEl.scrollLeft + carouselEl.clientWidth >= carouselEl.scrollWidth - 10;
    carouselEl.scrollBy({ left: atEnd ? -carouselEl.scrollWidth : cardWidth + 22, behavior: 'smooth' });
  }, 3200);
}
function stopAutoSlide(){ clearInterval(autoTimer); }

carouselEl.addEventListener('mouseenter', stopAutoSlide);
carouselEl.addEventListener('mouseleave', startAutoSlide);
carouselEl.addEventListener('touchstart', stopAutoSlide, { passive:true });
startAutoSlide();

document.getElementById('prevBtn').addEventListener('click', () => {
  const cardWidth = carouselEl.querySelector('.card')?.offsetWidth || 280;
  carouselEl.scrollBy({ left: -(cardWidth + 22), behavior: 'smooth' });
});
document.getElementById('nextBtn').addEventListener('click', () => {
  const cardWidth = carouselEl.querySelector('.card')?.offsetWidth || 280;
  carouselEl.scrollBy({ left: cardWidth + 22, behavior: 'smooth' });
});

/* =========================================================
   6) SHOP NOW SCROLL
   ========================================================= */
document.getElementById('shopNowBtn').addEventListener('click', () => {
  document.getElementById('products').scrollIntoView({ behavior:'smooth' });
});

/* =========================================================
   7) DRAWER OPEN / CLOSE
   ========================================================= */
const drawer = document.getElementById('drawer');
const overlay = document.getElementById('overlay');

function openDrawer(){
  drawer.classList.add('open');
  overlay.classList.add('open');
}
function closeDrawer(){
  drawer.classList.remove('open');
  overlay.classList.remove('open');
}

document.getElementById('cartIconTop').addEventListener('click', openDrawer);
document.getElementById('cartFab').addEventListener('click', openDrawer);
document.getElementById('closeDrawer').addEventListener('click', closeDrawer);
overlay.addEventListener('click', closeDrawer);
document.addEventListener('keydown', e => { if(e.key === 'Escape') closeDrawer(); });

/* =========================================================
   8) SEND ORDER VIA EMAILJS
   ========================================================= */
document.getElementById('sendOrderBtn').addEventListener('click', () => {
  const nameEl = document.getElementById('custName');
  const phoneEl = document.getElementById('custPhone');
  const statusEl = document.getElementById('statusMsg');
  const btn = document.getElementById('sendOrderBtn');

  const name = nameEl.value.trim();
  const phone = phoneEl.value.trim();

  statusEl.textContent = '';
  statusEl.className = 'status-msg';

  if(cart.length === 0){
    statusEl.textContent = 'Your cart is empty.';
    statusEl.classList.add('err');
    return;
  }
  if(!name){
    statusEl.textContent = 'Please enter your name.';
    statusEl.classList.add('err');
    nameEl.focus();
    return;
  }
  if(!phone || phone.replace(/\D/g,'').length < 8){
    statusEl.textContent = 'Please enter a valid phone number.';
    statusEl.classList.add('err');
    phoneEl.focus();
    return;
  }

  const itemsList = cart.map(i => `${i.name}  x${i.qty}  —  ${formatPrice(i.price * i.qty)}`).join('\n');
  const templateParams = {
    customer_name: name,
    customer_phone: phone,
    order_items: itemsList,
    order_total: formatPrice(cartTotal()),
    to_email: OWNER_EMAIL
  };

  if(!window.emailjs || EMAILJS_PUBLIC_KEY === 'YOUR_PUBLIC_KEY'){
    statusEl.textContent = 'EmailJS is not configured yet — see comments in the code.';
    statusEl.classList.add('err');
    console.log('Order payload (EmailJS not configured):', templateParams);
    return;
  }

  btn.disabled = true;
  btn.textContent = 'Sending…';

  emailjs.send(EMAILJS_SERVICE_ID, EMAILJS_TEMPLATE_ID, templateParams)
    .then(() => {
      statusEl.textContent = 'Order sent! We will contact you shortly.';
      statusEl.classList.add('ok');
      cart = [];
      renderCart();
      nameEl.value = '';
      phoneEl.value = '';
      setTimeout(closeDrawer, 1800);
    })
    .catch(err => {
      console.error(err);
      statusEl.textContent = 'Something went wrong sending the order. Please try WhatsApp instead.';
      statusEl.classList.add('err');
    })
    .finally(() => {
      btn.disabled = false;
      btn.innerHTML = 'Send order <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2"><path d="M22 2 11 13M22 2l-7 20-4-9-9-4 20-7z"/></svg>';
    });
});
</script>
</body>
</html>
