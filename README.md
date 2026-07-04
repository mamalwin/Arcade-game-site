<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Arcade Game</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Vazirmatn:wght@400;700;900&display=swap" rel="stylesheet">
<style>
:root{
  --bg-0:#0a0d14;
  --bg-1:#10141f;
  --bg-2:#161b29;
  --panel:#131826;
  --line:#232a3d;
  --neon:#00f0c8;
  --neon-2:#ff3d81;
  --neon-3:#ffd23f;
  --text-0:#eef1f8;
  --text-1:#9aa4bd;
  --text-2:#5c6584;
  --radius:14px;
  --font-display:'Orbitron', 'Vazirmatn', sans-serif;
  --font-body:'Vazirmatn', 'Segoe UI', sans-serif;
  --font-mono:'JetBrains Mono', monospace;
}
@font-face{
  font-family:'Orbitron';
  src:local('Orbitron');
}
*{box-sizing:border-box;}
html,body{margin:0;padding:0;}
html{scroll-behavior:smooth;}
body{
  background:
    radial-gradient(1200px 800px at 15% -10%, rgba(0,240,200,0.10), transparent 60%),
    radial-gradient(1000px 700px at 100% 10%, rgba(255,61,129,0.09), transparent 55%),
    radial-gradient(900px 700px at 50% 110%, rgba(125,95,255,0.08), transparent 60%),
    var(--bg-0);
  background-size:200% 200%, 200% 200%, 200% 200%, 100% 100%;
  animation:bgdrift 22s ease-in-out infinite;
  color:var(--text-0);
  font-family:var(--font-body);
  min-height:100vh;
  overflow-x:hidden;
}
@keyframes bgdrift{
  0%{background-position:0% 0%, 100% 0%, 50% 100%, 0 0;}
  50%{background-position:30% 20%, 70% 30%, 60% 80%, 0 0;}
  100%{background-position:0% 0%, 100% 0%, 50% 100%, 0 0;}
}
@media(prefers-reduced-motion:reduce){
  *{animation-duration:0.01ms !important; animation-iteration-count:1 !important; transition-duration:0.01ms !important;}
  html{scroll-behavior:auto;}
}
::selection{background:var(--neon);color:#04110d;}
::-webkit-scrollbar{width:10px;}
::-webkit-scrollbar-track{background:var(--bg-0);}
::-webkit-scrollbar-thumb{background:var(--line);border-radius:10px;}

/* scanline atmosphere */
.scanlines{
  position:fixed;inset:0;pointer-events:none;z-index:9999;
  background:repeating-linear-gradient(
    to bottom,
    rgba(255,255,255,0.015) 0px,
    rgba(255,255,255,0.015) 1px,
    transparent 1px,
    transparent 3px
  );
  mix-blend-mode:overlay;
  opacity:.5;
}
.noise-vignette{
  position:fixed;inset:0;pointer-events:none;z-index:9998;
  box-shadow:inset 0 0 220px rgba(0,0,0,0.65);
}

header.top{
  position:sticky;top:0;z-index:100;
  backdrop-filter:blur(14px);
  background:rgba(10,13,20,0.72);
  border-bottom:1px solid var(--line);
  padding:18px 6vw;
  display:flex;align-items:center;justify-content:space-between;
  gap:16px;
}
.brand{
  display:flex;align-items:center;gap:12px;
  font-family:var(--font-display);
  letter-spacing:2px;
  font-size:1.25rem;
  cursor:pointer;
}
.brand .dot{
  width:12px;height:12px;border-radius:3px;
  background:var(--neon);
  box-shadow:0 0 12px var(--neon), 0 0 28px var(--neon);
  animation:pulse 2.4s ease-in-out infinite;
}
@keyframes pulse{
  0%,100%{opacity:1; transform:scale(1);}
  50%{opacity:.55; transform:scale(.82);}
}
.brand b{color:var(--neon);}
nav.top-nav{
  display:flex;gap:22px;
  font-size:.92rem;
  color:var(--text-1);
}
nav.top-nav span{cursor:pointer;transition:color .2s;}
nav.top-nav span:hover{color:var(--text-0);}
.score-pill{
  font-family:var(--font-mono);
  font-size:.82rem;
  color:var(--neon-3);
  border:1px solid var(--line);
  padding:6px 14px;
  border-radius:100px;
  background:var(--bg-1);
  white-space:nowrap;
}

/* HERO */
.hero{
  padding:88px 6vw 60px;
  position:relative;
  display:grid;
  grid-template-columns:1.15fr .85fr;
  gap:40px;
  align-items:center;
}
@media(max-width:900px){.hero{grid-template-columns:1fr;padding:56px 6vw 40px;}}
.eyebrow{
  font-family:var(--font-mono);
  color:var(--neon);
  font-size:.8rem;
  letter-spacing:3px;
  text-transform:uppercase;
  display:flex;align-items:center;gap:10px;
  margin-bottom:18px;
}
.eyebrow::before{
  content:'';
  width:26px;height:1px;
  background:var(--neon);
}
h1.hero-title{
  font-family:var(--font-display);
  font-size:clamp(2.4rem, 5.4vw, 4.2rem);
  line-height:1.08;
  margin:0 0 20px;
  letter-spacing:1px;
}
h1.hero-title .glow{
  color:var(--neon);
  text-shadow:0 0 18px rgba(0,240,200,0.55), 0 0 46px rgba(0,240,200,0.25);
}
.hero p.lead{
  color:var(--text-1);
  font-size:1.08rem;
  line-height:1.9;
  max-width:52ch;
  margin-bottom:32px;
}
.hero-cta{display:flex;gap:14px;flex-wrap:wrap;}
.btn{
  position:relative;
  font-family:var(--font-body);
  font-weight:700;
  font-size:.95rem;
  padding:14px 28px;
  border-radius:10px;
  border:1px solid transparent;
  cursor:pointer;
  overflow:hidden;
  transition:transform .18s ease, box-shadow .18s ease, background .18s ease;
}
.btn:active{transform:scale(.96);}
.btn:focus-visible{outline:2px solid var(--neon); outline-offset:3px;}
.btn::after{
  content:'';
  position:absolute; inset:0;
  background:radial-gradient(circle at var(--mx,50%) var(--my,50%), rgba(255,255,255,.35), transparent 60%);
  opacity:0; transition:opacity .3s ease;
  pointer-events:none;
}
.btn:hover::after{opacity:1;}
.btn-primary{
  background:var(--neon);
  color:#04120e;
  box-shadow:0 0 0 rgba(0,240,200,0);
}
.btn-primary:hover{
  box-shadow:0 8px 34px rgba(0,240,200,.4);
  transform:translateY(-2px);
}
.btn-ghost{
  background:transparent;
  color:var(--text-0);
  border-color:var(--line);
}
.btn-ghost:hover{border-color:var(--neon);color:var(--neon); transform:translateY(-2px);}
button:focus-visible, .tile:focus-visible, .card:focus-visible{outline:2px solid var(--neon); outline-offset:2px;}

.hero-stage{
  position:relative;
  aspect-ratio:1/1;
  max-width:420px;
  margin-inline-start:auto;
}
.cab{
  position:absolute;
  border-radius:16px;
  border:1px solid var(--line);
  background:linear-gradient(160deg, var(--bg-2), var(--bg-1));
  box-shadow:0 30px 60px -20px rgba(0,0,0,.7);
  display:flex;align-items:center;justify-content:center;
  font-family:var(--font-display);
  overflow:hidden;
}
.cab::after{
  content:'';
  position:absolute;inset:0;
  background:linear-gradient(120deg, transparent 40%, rgba(255,255,255,.04) 50%, transparent 60%);
  animation:sheen 6s ease-in-out infinite;
}
@keyframes sheen{0%,100%{transform:translateX(-100%);}50%{transform:translateX(100%);}}
.cab1{width:62%;height:62%;top:0;left:0;color:var(--neon);font-size:2.6rem;box-shadow:0 0 40px -10px rgba(0,240,200,.35), 0 30px 60px -20px rgba(0,0,0,.7);animation:float1 5s ease-in-out infinite;}
.cab2{width:46%;height:46%;bottom:6%;right:0;color:var(--neon-2);font-size:1.8rem;box-shadow:0 0 40px -10px rgba(255,61,129,.35);animation:float2 6s ease-in-out infinite;}
.cab3{width:34%;height:34%;bottom:0;left:8%;color:var(--neon-3);font-size:1.3rem;box-shadow:0 0 40px -10px rgba(255,210,63,.35);animation:float3 4.5s ease-in-out infinite;}
@keyframes float1{0%,100%{transform:translateY(0);}50%{transform:translateY(-10px);}}
@keyframes float2{0%,100%{transform:translateY(0);}50%{transform:translateY(12px);}}
@keyframes float3{0%,100%{transform:translateY(0);}50%{transform:translateY(-8px);}}

/* SECTION HEADERS */
.section{padding:20px 6vw 70px;}
.section-head{
  display:flex;align-items:flex-end;justify-content:space-between;
  margin-bottom:30px;flex-wrap:wrap;gap:12px;
}
.section-head h2{
  font-family:var(--font-display);
  font-size:1.7rem;
  margin:0;
  letter-spacing:.5px;
}
.section-head h2 .idx{
  font-family:var(--font-mono);
  color:var(--neon);
  font-size:1rem;
  margin-inline-end:10px;
}
.section-head p{color:var(--text-2);font-size:.9rem;margin:0;}

.filter-bar{
  display:flex;gap:10px;flex-wrap:wrap;margin-bottom:26px;
}
.filter-chip{
  font-family:var(--font-mono);
  font-size:.78rem;
  padding:8px 16px;
  border-radius:100px;
  border:1px solid var(--line);
  background:var(--panel);
  color:var(--text-1);
  cursor:pointer;
  transition:all .2s ease;
  white-space:nowrap;
}
.filter-chip:hover{border-color:var(--neon); color:var(--text-0);}
.filter-chip.active{
  background:var(--neon);
  color:#04120e;
  border-color:var(--neon);
  box-shadow:0 4px 18px rgba(0,240,200,.3);
  font-weight:700;
}
.search-box{
  display:flex;align-items:center;gap:10px;
  background:var(--panel);
  border:1px solid var(--line);
  border-radius:10px;
  padding:10px 16px;
  margin-bottom:22px;
  max-width:340px;
  transition:border-color .2s;
}
.search-box:focus-within{border-color:var(--neon);}
.search-box input{
  background:transparent;border:none;outline:none;
  color:var(--text-0); font-family:var(--font-body); font-size:.9rem; width:100%;
}
.search-box input::placeholder{color:var(--text-2);}
.no-results{
  color:var(--text-2); text-align:center; padding:50px 0; font-family:var(--font-mono); font-size:.9rem;
}

/* GRID OF GAMES */
.grid{
  display:grid;
  grid-template-columns:repeat(auto-fill, minmax(260px,1fr));
  gap:22px;
}
.card{
  position:relative;
  background:var(--panel);
  border:1px solid var(--line);
  border-radius:var(--radius);
  padding:0;
  overflow:hidden;
  cursor:pointer;
  opacity:0;
  transform:translateY(18px);
  animation:cardIn .6s cubic-bezier(.2,.8,.3,1) forwards;
  animation-delay:calc(var(--i, 0) * 45ms);
  transition:transform .3s cubic-bezier(.2,.8,.3,1), border-color .3s ease, box-shadow .3s ease;
}
@keyframes cardIn{
  to{opacity:1; transform:translateY(0);}
}
.card::before{
  content:'';
  position:absolute; inset:-1px;
  border-radius:inherit;
  padding:1px;
  background:linear-gradient(120deg, transparent, var(--accent, var(--neon)), transparent);
  background-size:250% 250%;
  -webkit-mask:linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite:xor; mask-composite:exclude;
  opacity:0; transition:opacity .3s ease;
  pointer-events:none;
}
.card:hover{
  transform:translateY(-8px) scale(1.015);
  border-color:transparent;
  box-shadow:0 24px 48px -18px rgba(0,0,0,.65), 0 0 30px -8px var(--accent, var(--neon));
}
.card:hover::before{
  opacity:1;
  animation:borderSweep 2.2s linear infinite;
}
@keyframes borderSweep{
  0%{background-position:0% 0%;}
  100%{background-position:250% 250%;}
}
.card:hover .card-art{transform:scale(1.06);}
.card:hover .card-art span.emoji{transform:scale(1.15) rotate(-4deg);}
.card-art{
  height:150px;
  display:flex;align-items:center;justify-content:center;
  font-size:3rem;
  position:relative;
  background:
    radial-gradient(circle at 30% 20%, rgba(255,255,255,.06), transparent 60%),
    linear-gradient(150deg, var(--bg-2), var(--bg-1));
  border-bottom:1px solid var(--line);
  transition:transform .35s cubic-bezier(.2,.8,.3,1);
}
.card-art::before{
  content:'';
  position:absolute;inset:0;
  background:repeating-linear-gradient(45deg, rgba(255,255,255,.02) 0 2px, transparent 2px 10px);
}
.card-art span.emoji{
  display:inline-block;
  transition:transform .35s cubic-bezier(.34,1.56,.64,1);
  filter:drop-shadow(0 0 14px var(--accent, var(--neon)));
}
.play-hint{
  font-size:.78rem;color:var(--text-2);
  display:flex;align-items:center;gap:6px;
  transition:color .2s, transform .2s;
}
.card:hover .play-hint{color:var(--accent, var(--neon)); transform:translateX(-3px);}
.card-body{padding:18px 18px 20px;}
.card-body h3{
  font-family:var(--font-display);
  font-size:1rem;
  margin:0 0 6px;
  letter-spacing:.5px;
}
.card-body p{
  color:var(--text-2);
  font-size:.85rem;
  line-height:1.7;
  margin:0 0 14px;
  min-height:44px;
}
.tag-row{display:flex;gap:8px;flex-wrap:wrap;align-items:center;justify-content:space-between;}
.tag{
  font-family:var(--font-mono);
  font-size:.68rem;
  color:var(--accent, var(--neon));
  border:1px solid var(--line);
  padding:4px 10px;
  border-radius:100px;
}
/* FOOTER */
footer{
  padding:40px 6vw 60px;
  border-top:1px solid var(--line);
  color:var(--text-2);
  font-size:.85rem;
  display:flex;justify-content:space-between;flex-wrap:wrap;gap:14px;
}
footer .brand{font-size:1rem;}

/* GAME VIEW */
.game-view{
  display:none;
  padding:26px 6vw 70px;
  min-height:70vh;
}
.game-view.active{display:block;}
.hub-view.hidden{display:none;}
.game-topbar{
  display:flex;align-items:center;justify-content:space-between;
  margin-bottom:22px;flex-wrap:wrap;gap:12px;
}
.back-btn{
  font-family:var(--font-mono);
  font-size:.85rem;
  color:var(--text-1);
  background:var(--panel);
  border:1px solid var(--line);
  border-radius:10px;
  padding:10px 18px;
  cursor:pointer;
  transition:.2s;
}
.back-btn:hover{color:var(--neon);border-color:var(--neon);}
.game-title{
  font-family:var(--font-display);
  font-size:1.4rem;
  display:flex;align-items:center;gap:12px;
}
.game-stage{
  background:var(--panel);
  border:1px solid var(--line);
  border-radius:var(--radius);
  padding:26px;
  display:flex;flex-direction:column;align-items:center;gap:18px;
}
.hud{
  display:flex;gap:24px;flex-wrap:wrap;justify-content:center;
  font-family:var(--font-mono);font-size:.9rem;color:var(--text-1);
}
.hud b{color:var(--neon-3);}
canvas{
  background:#04060a;
  border-radius:10px;
  border:1px solid var(--line);
  max-width:100%;
  touch-action:none;
}
.controls-hint{
  color:var(--text-2);font-size:.8rem;text-align:center;max-width:60ch;
}
.overlay-msg{
  font-family:var(--font-display);
  color:var(--neon);
  font-size:1.1rem;
  text-align:center;
}
.mini-btn{
  font-family:var(--font-body);font-weight:700;font-size:.85rem;
  padding:9px 20px;border-radius:8px;border:1px solid var(--line);
  background:var(--bg-1);color:var(--text-0);cursor:pointer;transition:.2s;
}
.mini-btn:hover{border-color:var(--neon);color:var(--neon);}

/* board grids reused by memory/2048/ttt */
.board-grid{display:grid;gap:8px;}
.tile{
  display:flex;align-items:center;justify-content:center;
  border-radius:8px;font-family:var(--font-display);
  user-select:none;cursor:pointer;transition:transform .12s, background .2s;
}
.tile:active{transform:scale(.95);}

@media(max-width:600px){
  header.top{padding:14px 5vw;}
  nav.top-nav{display:none;}
  .hero{padding:48px 5vw 30px;}
}
</style>
</head>
<body>

<div class="scanlines"></div>
<div class="noise-vignette"></div>

<header class="top">
  <div class="brand" onclick="showHub()"><span class="dot"></span>Arcade Game</div>
  <nav class="top-nav">
    <span onclick="scrollToGrid()">بازی‌ها</span>
    <span onclick="showHub()">خانه</span>
  </nav>
</header>

<main id="hubView" class="hub-view">
  <section class="hero">
    <div>
      <h1 class="hero-title">وارد <span class="glow">آرکید</span> شو<br>و رکورد بشکن</h1>
      <p class="lead">مجموعه‌ای از بازی‌های کلاسیک و مدرن، مستقیم توی مرورگرت. بدون نصب، بدون تبلیغ، فقط بازی. یکی رو انتخاب کن و شروع کن.</p>
      <div class="hero-cta">
        <button class="btn btn-primary" onclick="scrollToGrid()">شروع بازی</button>
      </div>
    </div>
    <div class="hero-stage">
      <div class="cab cab1">🐍</div>
      <div class="cab cab2">🧱</div>
      <div class="cab cab3">🃏</div>
    </div>
  </section>

  <section class="section" id="gridSection">
    <div class="section-head">
      <h2><span class="idx">01</span>همه بازی‌ها</h2>
      <p id="gameCountLabel">۴۰ بازی — روی هر کارت کلیک کن تا شروع بشه</p>
    </div>
    <div class="search-box">
      <span>🔍</span>
      <input type="text" id="searchInput" placeholder="جستجوی بازی...">
    </div>
    <div class="filter-bar" id="filterBar"></div>
    <div class="grid" id="gamesGrid"></div>
    <div class="no-results" id="noResults" style="display:none;">بازی‌ای با این مشخصات پیدا نشد 🔎</div>
  </section>

  <footer>
    <div class="brand">Arcade Game</div>
    <div>ساخته‌شده با ❤  توسط Mampy Team</div>
  </footer>
</main>

<!-- ================= GAME VIEWS ================= -->
<div id="views"></div>

<script>
/* ============ GAME METADATA ============ */
const GAMES = [
  {id:'snake', title:'مار', icon:'🐍', accent:'#00f0c8', desc:'مار رو هدایت کن، غذا بخور، رشد کن، به خودت برخورد نکن.', tag:'کلاسیک'},
  {id:'g2048', title:'۲۰۴۸', icon:'🔢', accent:'#ffd23f', desc:'کاشی‌ها رو ترکیب کن تا به عدد ۲۰۴۸ برسی.', tag:'پازل'},
  {id:'memory', title:'حافظه', icon:'🃏', accent:'#ff3d81', desc:'جفت کارت‌های یکسان رو با کمترین حرکت پیدا کن.', tag:'حافظه'},
  {id:'ttt', title:'دوز', icon:'❌', accent:'#7d5fff', desc:'با هوش مصنوعی یا دوستت دوز بازی کن.', tag:'استراتژی'},
  {id:'breakout', title:'آجرشکن', icon:'🧱', accent:'#00f0c8', desc:'توپ رو با راکت بگیر و همه آجرها رو بشکن.', tag:'آرکید'},
  {id:'flappy', title:'پرنده پرنده', icon:'🐤', accent:'#ffd23f', desc:'از بین لوله‌ها عبور کن و امتیاز جمع کن.', tag:'آرکید'},
  {id:'tetris', title:'تتریس', icon:'🧩', accent:'#ff3d81', desc:'قطعات رو بچین و ردیف‌های کامل بساز.', tag:'کلاسیک'},
  {id:'whack', title:'موش‌کوب', icon:'🔨', accent:'#7d5fff', desc:'قبل از فرار موش‌ها روی سرشون بزن.', tag:'واکنش'},
  {id:'rps', title:'سنگ کاغذ قیچی', icon:'✊', accent:'#00f0c8', desc:'در برابر کامپیوتر شانست رو امتحان کن.', tag:'سریع'},
  {id:'reaction', title:'تست واکنش', icon:'⚡', accent:'#ffd23f', desc:'سرعت واکنشت رو به میلی‌ثانیه اندازه بگیر.', tag:'واکنش'},
  {id:'pong', title:'پونگ', icon:'🏓', accent:'#00f0c8', desc:'راکت رو کنترل کن و توپ رو از دست حریف کامپیوتری رد نکن.', tag:'آرکید'},
  {id:'minesweeper', title:'مین‌یاب', icon:'💣', accent:'#ff3d81', desc:'خانه‌های امن رو باز کن و مین‌ها رو حدس بزن.', tag:'پازل'},
  {id:'simon', title:'سایمون', icon:'🎵', accent:'#7d5fff', desc:'توالی رنگ‌ها رو به خاطر بسپار و تکرار کن.', tag:'حافظه'},
  {id:'connect4', title:'چهار در ردیف', icon:'🔴', accent:'#ffd23f', desc:'چهار مهره هم‌رنگ رو قبل از حریف در یک ردیف بچین.', tag:'استراتژی'},
  {id:'wordguess', title:'حدس کلمه', icon:'🔤', accent:'#00f0c8', desc:'کلمه مخفی رو با حروف پیشنهادی حدس بزن.', tag:'کلمات'},
  {id:'math', title:'چالش ریاضی', icon:'➗', accent:'#ff3d81', desc:'قبل از تموم شدن زمان به سوالات ریاضی جواب بده.', tag:'آموزشی'},
  {id:'colormatch', title:'تطبیق رنگ', icon:'🎨', accent:'#7d5fff', desc:'رنگ متن و معنی کلمه رو تشخیص بده، سریع و درست.', tag:'واکنش'},
  {id:'dino', title:'دایناسور پرشی', icon:'🦖', accent:'#ffd23f', desc:'از موانع بپر و تا جایی که می‌تونی دوام بیار.', tag:'آرکید'},
  {id:'asteroids', title:'سیارک‌ها', icon:'☄️', accent:'#00f0c8', desc:'سفینه رو بچرخون، شلیک کن، سیارک‌ها رو نابود کن.', tag:'آرکید'},
  {id:'lightsout', title:'چراغ‌ها خاموش', icon:'💡', accent:'#ff3d81', desc:'با کمترین کلیک همه چراغ‌ها رو خاموش کن.', tag:'پازل'},
  {id:'wordle', title:'حدس پنج‌حرفی', icon:'🟩', accent:'#7d5fff', desc:'کلمه پنج‌حرفی رو در ۶ حدس پیدا کن.', tag:'کلمات'},
  {id:'sudoku', title:'سودوکو مینی', icon:'🔢', accent:'#ffd23f', desc:'جدول ۴×۴ رو با اعداد ۱ تا ۴ کامل کن.', tag:'پازل'},
  {id:'typing', title:'تست تایپ', icon:'⌨️', accent:'#00f0c8', desc:'متن رو تا جایی که می‌تونی سریع و درست تایپ کن.', tag:'مهارت'},
  {id:'jump', title:'پرش مکعب', icon:'🟦', accent:'#ff3d81', desc:'مکعب رو در زمان درست بپران تا به موانع نخوره.', tag:'آرکید'},
  {id:'match3', title:'سه‌تایی', icon:'🍬', accent:'#7d5fff', desc:'سه شکل هم‌رنگ رو در یک ردیف بچین تا امتیاز بگیری.', tag:'پازل'},
  {id:'towerstack', title:'برج‌سازی', icon:'🏗️', accent:'#ffd23f', desc:'بلوک‌های متحرک رو دقیق روی هم بچین و برج بساز.', tag:'مهارت'},
  {id:'maze', title:'هزارتو', icon:'🌀', accent:'#00f0c8', desc:'راه خروج از هزارتو رو پیدا کن.', tag:'پازل'},
  {id:'slidepuzzle', title:'پازل کشویی', icon:'🧩', accent:'#ff3d81', desc:'کاشی‌ها رو بلغزون تا تصویر رو کامل کنی.', tag:'پازل'},
  {id:'catchgame', title:'گرفتن میوه', icon:'🍎', accent:'#7d5fff', desc:'سبد رو حرکت بده و میوه‌های در حال سقوط رو بگیر.', tag:'واکنش'},
  {id:'guessnumber', title:'حدس عدد', icon:'🎯', accent:'#ffd23f', desc:'عدد مخفی بین ۱ تا ۱۰۰ رو با کمترین حدس پیدا کن.', tag:'کلاسیک'},
  {id:'blackjack', title:'بلک‌جک', icon:'🂡', accent:'#00f0c8', desc:'به ۲۱ نزدیک شو بدون رد شدن، در برابر خانه بازی کن.', tag:'کارتی'},
  {id:'hangman', title:'دار مریزی', icon:'🎪', accent:'#ff3d81', desc:'حروف کلمه مخفی رو حدس بزن قبل از تموم شدن جون‌ها.', tag:'کلمات'},
  {id:'spaceshooter', title:'جنگ فضایی', icon:'🚀', accent:'#7d5fff', desc:'سفینه دشمن رو قبل از رسیدنش به تو منهدم کن.', tag:'آرکید'},
  {id:'bubbleshoot', title:'حباب‌ترکون', icon:'🫧', accent:'#ffd23f', desc:'حباب‌های هم‌رنگ رو نشونه بگیر و بترکون.', tag:'آرکید'},
  {id:'pixelpaint', title:'نقاشی پیکسلی', icon:'🖌️', accent:'#00f0c8', desc:'روی بوم پیکسلی نقاشی بکش و خلاقیتت رو نشون بده.', tag:'خلاقانه'},
  {id:'quiz', title:'مسابقه اطلاعات عمومی', icon:'❓', accent:'#ff3d81', desc:'به سوالات عمومی جواب بده و امتیاز جمع کن.', tag:'آموزشی'},
  {id:'stackcolor', title:'برج رنگی', icon:'🎨', accent:'#7d5fff', desc:'رنگ درست رو در زمان درست انتخاب کن و برج بساز.', tag:'واکنش'},
  {id:'chess', title:'شطرنج تمرینی', icon:'♟️', accent:'#ffd23f', desc:'مهره‌ها رو حرکت بده و با قوانین شطرنج آشنا شو.', tag:'استراتژی'},
  {id:'runner', title:'دونده بی‌پایان', icon:'🏃', accent:'#00f0c8', desc:'از موانع در حال حرکت فرار کن و رکورد بزن.', tag:'آرکید'},
  {id:'cardmatch', title:'جنگ اعداد', icon:'🔢', accent:'#ff3d81', desc:'کارت بزرگ‌تر رو انتخاب کن و از حریف ببر.', tag:'کارتی'},
];

const CATEGORIES = ['همه', ...Array.from(new Set(GAMES.map(g=>g.tag)))];
let activeFilter='همه', searchTerm='';

let playCount = 0;
function bumpPlays(){ playCount++; document.getElementById('totalPlays').textContent = 'بازی‌های امروز: '+playCount.toLocaleString('fa-IR'); }

const gridEl = document.getElementById('gamesGrid');
const filterBar = document.getElementById('filterBar');
const noResultsEl = document.getElementById('noResults');
const countLabel = document.getElementById('gameCountLabel');

CATEGORIES.forEach(cat=>{
  const chip = document.createElement('button');
  chip.className='filter-chip'+(cat===activeFilter?' active':'');
  chip.textContent=cat;
  chip.onclick=()=>{ activeFilter=cat; renderGrid(); document.querySelectorAll('.filter-chip').forEach(c=>c.classList.toggle('active', c.textContent===cat)); };
  filterBar.appendChild(chip);
});

document.getElementById('searchInput').addEventListener('input', e=>{
  searchTerm = e.target.value.trim();
  renderGrid();
});

function renderGrid(){
  const filtered = GAMES.filter(g=>{
    const matchCat = activeFilter==='همه' || g.tag===activeFilter;
    const matchSearch = !searchTerm || g.title.includes(searchTerm) || g.desc.includes(searchTerm);
    return matchCat && matchSearch;
  });
  gridEl.innerHTML='';
  countLabel.textContent = `${filtered.length.toLocaleString('fa-IR')} بازی — روی هر کارت کلیک کن تا شروع بشه`;
  noResultsEl.style.display = filtered.length? 'none':'block';
  filtered.forEach((g,i)=>{
    const card = document.createElement('div');
    card.className='card';
    card.style.setProperty('--accent', g.accent);
    card.style.setProperty('--i', i);
    card.tabIndex=0;
    card.setAttribute('role','button');
    card.onclick=()=>openGame(g.id);
    card.onkeydown=(e)=>{ if(e.key==='Enter'||e.key===' '){ e.preventDefault(); openGame(g.id);} };
    card.innerHTML=`
      <div class="card-art"><span class="emoji">${g.icon}</span></div>
      <div class="card-body">
        <h3>${g.title}</h3>
        <p>${g.desc}</p>
        <div class="tag-row">
          <span class="tag">${g.tag}</span>
          <span class="play-hint">شروع ▶</span>
        </div>
      </div>`;
    gridEl.appendChild(card);
  });
}
renderGrid();

function scrollToGrid(){ document.getElementById('gridSection').scrollIntoView({behavior:'smooth'}); }

function showHub(){
  document.getElementById('hubView').classList.remove('hidden');
  document.querySelectorAll('.game-view').forEach(v=>v.classList.remove('active'));
  cleanupCurrentGame();
  window.scrollTo({top:0,behavior:'smooth'});
}

let currentCleanup = null;
function cleanupCurrentGame(){ if(currentCleanup){ try{currentCleanup();}catch(e){} currentCleanup=null; } }

function openGame(id){
  document.getElementById('hubView').classList.add('hidden');
  document.querySelectorAll('.game-view').forEach(v=>v.classList.remove('active'));
  let view = document.getElementById('view-'+id);
  if(!view){
    view = document.createElement('div');
    view.id='view-'+id;
    view.className='game-view';
    document.getElementById('views').appendChild(view);
    builders[id](view);
  }
  view.classList.add('active');
  window.scrollTo({top:0,behavior:'smooth'});
  bumpPlays();
}

function gameTopbar(title, icon){
  return `<div class="game-topbar">
    <button class="back-btn" onclick="showHub()">← بازگشت به آرکید</button>
    <div class="game-title">${icon} ${title}</div>
    <div style="width:140px"></div>
  </div>`;
}

const builders = {};

/* ============ 1. SNAKE ============ */
builders.snake = function(view){
  view.innerHTML = gameTopbar('مار','🐍') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="snakeScore">0</b></span><span>بهترین: <b id="snakeBest">0</b></span></div>
      <canvas id="snakeCanvas" width="400" height="400"></canvas>
      <div class="controls-hint">با کلیدهای جهت‌دار یا W A S D حرکت کن. روی موبایل، صفحه رو سوایپ کن.</div>
      <button class="mini-btn" id="snakeRestart">شروع دوباره</button>
    </div>`;
  const canvas = view.querySelector('#snakeCanvas');
  const ctx = canvas.getContext('2d');
  const size = 20, cells = 20;
  let snake, dir, food, score, best = +(localStorage.getItem('snakeBest')||0), alive, loopId;
  view.querySelector('#snakeBest').textContent = best;

  function reset(){
    snake=[{x:10,y:10},{x:9,y:10},{x:8,y:10}];
    dir={x:1,y:0}; score=0; alive=true;
    placeFood();
    view.querySelector('#snakeScore').textContent = score;
    if(loopId) clearInterval(loopId);
    loopId = setInterval(tick, 100);
  }
  function placeFood(){
    food = {x:Math.floor(Math.random()*cells), y:Math.floor(Math.random()*cells)};
    if(snake.some(s=>s.x===food.x&&s.y===food.y)) placeFood();
  }
  function tick(){
    if(!alive) return;
    const head = {x:snake[0].x+dir.x, y:snake[0].y+dir.y};
    if(head.x<0||head.y<0||head.x>=cells||head.y>=cells||snake.some(s=>s.x===head.x&&s.y===head.y)){
      alive=false; clearInterval(loopId);
      if(score>best){ best=score; localStorage.setItem('snakeBest',best); view.querySelector('#snakeBest').textContent=best; }
      draw(true); return;
    }
    snake.unshift(head);
    if(head.x===food.x && head.y===food.y){ score++; view.querySelector('#snakeScore').textContent=score; placeFood(); }
    else snake.pop();
    draw(false);
  }
  function draw(gameOver){
    ctx.fillStyle='#04060a'; ctx.fillRect(0,0,canvas.width,canvas.height);
    ctx.fillStyle='#ff3d81'; ctx.fillRect(food.x*size+2, food.y*size+2, size-4, size-4);
    snake.forEach((s,i)=>{
      ctx.fillStyle = i===0? '#00f0c8':'rgba(0,240,200,0.65)';
      ctx.fillRect(s.x*size+1, s.y*size+1, size-2, size-2);
    });
    if(gameOver){
      ctx.fillStyle='rgba(0,0,0,0.6)'; ctx.fillRect(0,0,canvas.width,canvas.height);
      ctx.fillStyle='#00f0c8'; ctx.font='bold 24px Orbitron, sans-serif'; ctx.textAlign='center';
      ctx.fillText('باختی! دوباره امتحان کن', canvas.width/2, canvas.height/2);
    }
  }
  function keyHandler(e){
    const k=e.key.toLowerCase();
    if((k==='arrowup'||k==='w')&&dir.y===0) dir={x:0,y:-1};
    else if((k==='arrowdown'||k==='s')&&dir.y===0) dir={x:0,y:1};
    else if((k==='arrowleft'||k==='a')&&dir.x===0) dir={x:-1,y:0};
    else if((k==='arrowright'||k==='d')&&dir.x===0) dir={x:1,y:0};
  }
  document.addEventListener('keydown', keyHandler);
  let touchStart=null;
  canvas.addEventListener('touchstart', e=>{touchStart={x:e.touches[0].clientX,y:e.touches[0].clientY};});
  canvas.addEventListener('touchend', e=>{
    if(!touchStart) return;
    const dx=e.changedTouches[0].clientX-touchStart.x, dy=e.changedTouches[0].clientY-touchStart.y;
    if(Math.abs(dx)>Math.abs(dy)){ if(dx>20&&dir.x===0)dir={x:1,y:0}; else if(dx<-20&&dir.x===0)dir={x:-1,y:0}; }
    else { if(dy>20&&dir.y===0)dir={x:0,y:1}; else if(dy<-20&&dir.y===0)dir={x:0,y:-1}; }
  });
  view.querySelector('#snakeRestart').onclick = reset;
  reset();
  currentCleanup = ()=>{ clearInterval(loopId); document.removeEventListener('keydown', keyHandler); };
  view._cleanup = ()=>{ clearInterval(loopId); document.removeEventListener('keydown', keyHandler); };
};

/* ============ 2. 2048 ============ */
builders.g2048 = function(view){
  view.innerHTML = gameTopbar('۲۰۴۸','🔢') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="t2048Score">0</b></span><span>بهترین: <b id="t2048Best">0</b></span></div>
      <div class="board-grid" id="t2048Grid" style="grid-template-columns:repeat(4,70px);grid-template-rows:repeat(4,70px);background:#0d1119;padding:8px;border-radius:10px;"></div>
      <div class="controls-hint">با کلیدهای جهت‌دار حرکت کن. روی موبایل سوایپ کن.</div>
      <button class="mini-btn" id="t2048Restart">شروع دوباره</button>
    </div>`;
  const gridEl = view.querySelector('#t2048Grid');
  let grid, score, best = +(localStorage.getItem('t2048Best')||0);
  view.querySelector('#t2048Best').textContent = best;
  const colors = {2:'#1f2537',4:'#232a44',8:'#2e3a6b',16:'#3a4b8a',32:'#4b5fb0',64:'#5f74d6',128:'#ffd23f',256:'#ffbf3f',512:'#ff9f3f',1024:'#ff7d3f',2048:'#ff3d81'};

  function reset(){
    grid = Array.from({length:4},()=>Array(4).fill(0));
    score=0;
    addTile(); addTile();
    render();
  }
  function addTile(){
    const empty=[];
    for(let r=0;r<4;r++)for(let c=0;c<4;c++) if(grid[r][c]===0) empty.push([r,c]);
    if(!empty.length) return;
    const [r,c] = empty[Math.floor(Math.random()*empty.length)];
    grid[r][c] = Math.random()<0.9?2:4;
  }
  function render(){
    gridEl.innerHTML='';
    for(let r=0;r<4;r++)for(let c=0;c<4;c++){
      const v = grid[r][c];
      const d=document.createElement('div');
      d.className='tile';
      d.style.background = v? (colors[v]||'#ff3d81') : '#161b29';
      d.style.color = v>=128? '#0a0d14':'#eef1f8';
      d.style.fontSize = v>512? '1.1rem':'1.4rem';
      d.textContent = v||'';
      gridEl.appendChild(d);
    }
    view.querySelector('#t2048Score').textContent = score;
    if(score>best){ best=score; localStorage.setItem('t2048Best',best); view.querySelector('#t2048Best').textContent=best; }
  }
  function slide(row){
    let arr = row.filter(x=>x);
    for(let i=0;i<arr.length-1;i++){
      if(arr[i]===arr[i+1]){ arr[i]*=2; score+=arr[i]; arr.splice(i+1,1); }
    }
    while(arr.length<4) arr.push(0);
    return arr;
  }
  function move(dir){
    let moved=false;
    const before = JSON.stringify(grid);
    if(dir==='left'){ grid = grid.map(r=>slide(r)); }
    if(dir==='right'){ grid = grid.map(r=>slide(r.slice().reverse()).reverse()); }
    if(dir==='up'){
      for(let c=0;c<4;c++){ let col=[grid[0][c],grid[1][c],grid[2][c],grid[3][c]]; col=slide(col); for(let r=0;r<4;r++) grid[r][c]=col[r]; }
    }
    if(dir==='down'){
      for(let c=0;c<4;c++){ let col=[grid[3][c],grid[2][c],grid[1][c],grid[0][c]]; col=slide(col); for(let r=0;r<4;r++) grid[3-r][c]=col[r]; }
    }
    moved = before !== JSON.stringify(grid);
    if(moved){ addTile(); render(); }
  }
  function keyHandler(e){
    const map={ArrowLeft:'left',ArrowRight:'right',ArrowUp:'up',ArrowDown:'down'};
    if(map[e.key]){ e.preventDefault(); move(map[e.key]); }
  }
  document.addEventListener('keydown', keyHandler);
  let ts=null;
  gridEl.addEventListener('touchstart', e=>{ts={x:e.touches[0].clientX,y:e.touches[0].clientY};});
  gridEl.addEventListener('touchend', e=>{
    if(!ts) return;
    const dx=e.changedTouches[0].clientX-ts.x, dy=e.changedTouches[0].clientY-ts.y;
    if(Math.abs(dx)>Math.abs(dy)) move(dx>20?'right':dx<-20?'left':'');
    else move(dy>20?'down':dy<-20?'up':'');
  });
  view.querySelector('#t2048Restart').onclick = reset;
  reset();
  currentCleanup = ()=>document.removeEventListener('keydown', keyHandler);
  view._cleanup = currentCleanup;
};

/* ============ 3. MEMORY ============ */
builders.memory = function(view){
  view.innerHTML = gameTopbar('حافظه','🃏') + `
    <div class="game-stage">
      <div class="hud"><span>حرکت‌ها: <b id="memMoves">0</b></span><span>جفت‌ها: <b id="memPairs">0</b>/8</span></div>
      <div class="board-grid" id="memGrid" style="grid-template-columns:repeat(4,80px);"></div>
      <button class="mini-btn" id="memRestart">شروع دوباره</button>
    </div>`;
  const icons = ['🍎','🍋','🍇','🍓','🍒','🥝','🍑','🍍'];
  const gridEl = view.querySelector('#memGrid');
  let cards, flipped, matched, moves;
  function reset(){
    cards = [...icons,...icons].sort(()=>Math.random()-0.5);
    flipped=[]; matched=[]; moves=0;
    view.querySelector('#memMoves').textContent=0;
    view.querySelector('#memPairs').textContent=0;
    render();
  }
  function render(){
    gridEl.innerHTML='';
    cards.forEach((icon,i)=>{
      const d=document.createElement('div');
      d.className='tile';
      d.style.width='80px'; d.style.height='80px'; d.style.fontSize='2rem';
      const shown = flipped.includes(i)||matched.includes(i);
      d.style.background = matched.includes(i)? 'rgba(0,240,200,0.18)' : '#161b29';
      d.style.border = matched.includes(i)? '1px solid #00f0c8':'1px solid #232a3d';
      d.textContent = shown? icon : '❔';
      d.onclick = ()=>flip(i);
      gridEl.appendChild(d);
    });
  }
  function flip(i){
    if(flipped.length===2 || flipped.includes(i) || matched.includes(i)) return;
    flipped.push(i); render();
    if(flipped.length===2){
      moves++; view.querySelector('#memMoves').textContent=moves;
      const [a,b]=flipped;
      if(cards[a]===cards[b]){
        matched.push(a,b);
        view.querySelector('#memPairs').textContent = matched.length/2;
        flipped=[]; render();
      } else {
        setTimeout(()=>{ flipped=[]; render(); }, 700);
      }
    }
  }
  view.querySelector('#memRestart').onclick = reset;
  reset();
  currentCleanup=null;
};

/* ============ 4. TIC TAC TOE ============ */
builders.ttt = function(view){
  view.innerHTML = gameTopbar('دوز','❌') + `
    <div class="game-stage">
      <div class="hud" id="tttStatus">نوبت شما (X)</div>
      <div class="board-grid" id="tttGrid" style="grid-template-columns:repeat(3,90px);"></div>
      <button class="mini-btn" id="tttRestart">شروع دوباره</button>
    </div>`;
  const gridEl = view.querySelector('#tttGrid');
  const statusEl = view.querySelector('#tttStatus');
  let board, gameOver;
  const WIN=[[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
  function reset(){ board=Array(9).fill(''); gameOver=false; statusEl.textContent='نوبت شما (X)'; render(); }
  function render(){
    gridEl.innerHTML='';
    board.forEach((v,i)=>{
      const d=document.createElement('div');
      d.className='tile';
      d.style.width='90px'; d.style.height='90px'; d.style.fontSize='2.2rem';
      d.style.background='#161b29'; d.style.border='1px solid #232a3d';
      d.style.color = v==='X'? '#00f0c8':'#ff3d81';
      d.textContent=v;
      d.onclick=()=>playerMove(i);
      gridEl.appendChild(d);
    });
  }
  function checkWin(b, mark){ return WIN.some(line=>line.every(i=>b[i]===mark)); }
  function playerMove(i){
    if(gameOver || board[i]) return;
    board[i]='X'; render();
    if(checkWin(board,'X')){ statusEl.textContent='بردی! 🎉'; gameOver=true; return; }
    if(board.every(c=>c)){ statusEl.textContent='مساوی شد'; gameOver=true; return; }
    statusEl.textContent='نوبت کامپیوتر...';
    setTimeout(computerMove, 400);
  }
  function computerMove(){
    if(gameOver) return;
    // try win, then block, then center, then random
    const empties = board.map((v,i)=>v?null:i).filter(i=>i!==null);
    let move = findBest('O') ?? findBest('X') ?? (board[4]===''?4:null) ?? empties[Math.floor(Math.random()*empties.length)];
    board[move]='O'; render();
    if(checkWin(board,'O')){ statusEl.textContent='باختی! دوباره تلاش کن'; gameOver=true; return; }
    if(board.every(c=>c)){ statusEl.textContent='مساوی شد'; gameOver=true; return; }
    statusEl.textContent='نوبت شما (X)';
  }
  function findBest(mark){
    for(const line of WIN){
      const vals = line.map(i=>board[i]);
      if(vals.filter(v=>v===mark).length===2 && vals.includes('')){
        return line[vals.indexOf('')];
      }
    }
    return null;
  }
  view.querySelector('#tttRestart').onclick = reset;
  reset();
  currentCleanup=null;
};

/* ============ 5. BREAKOUT ============ */
builders.breakout = function(view){
  view.innerHTML = gameTopbar('آجرشکن','🧱') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="brkScore">0</b></span><span>جان: <b id="brkLives">3</b></span></div>
      <canvas id="brkCanvas" width="420" height="360"></canvas>
      <div class="controls-hint">با موس یا کلیدهای جهت چپ/راست راکت رو حرکت بده.</div>
      <button class="mini-btn" id="brkRestart">شروع دوباره</button>
    </div>`;
  const canvas = view.querySelector('#brkCanvas');
  const ctx = canvas.getContext('2d');
  let paddleX, ball, rows=4, cols=8, bricks, score, lives, animId, running;
  const brickW=44, brickH=16, gap=6, offsetTop=30, offsetLeft=15;
  const colors=['#00f0c8','#ffd23f','#ff3d81','#7d5fff'];

  function reset(){
    paddleX = canvas.width/2-40;
    ball = {x:canvas.width/2, y:canvas.height-40, dx:3, dy:-3, r:6};
    bricks = [];
    for(let r=0;r<rows;r++){ bricks[r]=[]; for(let c=0;c<cols;c++) bricks[r][c]={x:0,y:0,alive:true}; }
    score=0; lives=3; running=true;
    view.querySelector('#brkScore').textContent=score;
    view.querySelector('#brkLives').textContent=lives;
    if(animId) cancelAnimationFrame(animId);
    loop();
  }
  function drawBricks(){
    for(let r=0;r<rows;r++)for(let c=0;c<cols;c++){
      const b=bricks[r][c]; if(!b.alive) continue;
      const x=offsetLeft+c*(brickW+gap), y=offsetTop+r*(brickH+gap);
      b.x=x; b.y=y;
      ctx.fillStyle=colors[r%colors.length]; ctx.fillRect(x,y,brickW,brickH);
    }
  }
  function collide(){
    for(let r=0;r<rows;r++)for(let c=0;c<cols;c++){
      const b=bricks[r][c]; if(!b.alive) continue;
      if(ball.x>b.x && ball.x<b.x+brickW && ball.y-ball.r<b.y+brickH && ball.y+ball.r>b.y){
        ball.dy*=-1; b.alive=false; score+=10; view.querySelector('#brkScore').textContent=score;
      }
    }
  }
  function loop(){
    if(!running) return;
    ctx.fillStyle='#04060a'; ctx.fillRect(0,0,canvas.width,canvas.height);
    drawBricks();
    ctx.beginPath(); ctx.arc(ball.x,ball.y,ball.r,0,Math.PI*2); ctx.fillStyle='#eef1f8'; ctx.fill();
    ctx.fillStyle='#00f0c8'; ctx.fillRect(paddleX, canvas.height-14, 80, 10);

    ball.x+=ball.dx; ball.y+=ball.dy;
    if(ball.x<ball.r||ball.x>canvas.width-ball.r) ball.dx*=-1;
    if(ball.y<ball.r) ball.dy*=-1;
    if(ball.y> canvas.height-24 && ball.y<canvas.height-14 && ball.x>paddleX && ball.x<paddleX+80) ball.dy*=-1;
    if(ball.y>canvas.height){
      lives--; view.querySelector('#brkLives').textContent=lives;
      if(lives<=0){ running=false; msg('باختی! دوباره امتحان کن'); return; }
      ball={x:canvas.width/2,y:canvas.height-40,dx:3,dy:-3,r:6};
    }
    collide();
    if(bricks.flat().every(b=>!b.alive)){ running=false; msg('بردی! همه آجرها شکست 🎉'); return; }
    animId = requestAnimationFrame(loop);
  }
  function msg(text){
    ctx.fillStyle='rgba(0,0,0,0.6)'; ctx.fillRect(0,0,canvas.width,canvas.height);
    ctx.fillStyle='#00f0c8'; ctx.font='bold 20px Orbitron, sans-serif'; ctx.textAlign='center';
    ctx.fillText(text, canvas.width/2, canvas.height/2);
  }
  function mouseHandler(e){
    const rect = canvas.getBoundingClientRect();
    const x = (e.clientX - rect.left) * (canvas.width/rect.width);
    paddleX = Math.min(Math.max(x-40,0), canvas.width-80);
  }
  function keyHandler(e){
    if(e.key==='ArrowLeft') paddleX=Math.max(paddleX-25,0);
    if(e.key==='ArrowRight') paddleX=Math.min(paddleX+25,canvas.width-80);
  }
  canvas.addEventListener('mousemove', mouseHandler);
  document.addEventListener('keydown', keyHandler);
  view.querySelector('#brkRestart').onclick = reset;
  reset();
  currentCleanup = ()=>{ running=false; cancelAnimationFrame(animId); document.removeEventListener('keydown', keyHandler); };
  view._cleanup = currentCleanup;
};

/* ============ 6. FLAPPY ============ */
builders.flappy = function(view){
  view.innerHTML = gameTopbar('پرنده پرنده','🐤') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="flpScore">0</b></span><span>بهترین: <b id="flpBest">0</b></span></div>
      <canvas id="flpCanvas" width="360" height="420"></canvas>
      <div class="controls-hint">کلیک کن یا کلید Space رو بزن تا پرنده بالا بپره.</div>
      <button class="mini-btn" id="flpRestart">شروع دوباره</button>
    </div>`;
  const canvas = view.querySelector('#flpCanvas');
  const ctx = canvas.getContext('2d');
  let bird, pipes, score, best=+(localStorage.getItem('flpBest')||0), running, animId, frame;
  view.querySelector('#flpBest').textContent=best;

  function reset(){
    bird={x:70,y:200,vy:0};
    pipes=[{x:400, gap:150, top:100}];
    score=0; running=true; frame=0;
    view.querySelector('#flpScore').textContent=score;
    if(animId) cancelAnimationFrame(animId);
    loop();
  }
  function flap(){ if(running) bird.vy=-6.5; else reset(); }
  function loop(){
    if(!running) return;
    frame++;
    ctx.fillStyle='#04060a'; ctx.fillRect(0,0,canvas.width,canvas.height);
    bird.vy+=0.35; bird.y+=bird.vy;
    ctx.fillStyle='#ffd23f'; ctx.beginPath(); ctx.arc(bird.x,bird.y,12,0,Math.PI*2); ctx.fill();

    if(frame%90===0){
      const top = 50+Math.random()*180;
      pipes.push({x:canvas.width, gap:140, top});
    }
    pipes.forEach(p=>p.x-=2.6);
    pipes = pipes.filter(p=>p.x>-40);
    ctx.fillStyle='#00f0c8';
    pipes.forEach(p=>{
      ctx.fillRect(p.x,0,30,p.top);
      ctx.fillRect(p.x,p.top+p.gap,30,canvas.height-p.top-p.gap);
      if(!p.passed && p.x+30<bird.x){ p.passed=true; score++; view.querySelector('#flpScore').textContent=score; }
      if(bird.x+12>p.x && bird.x-12<p.x+30 && (bird.y-12<p.top || bird.y+12>p.top+p.gap)) gameOver();
    });
    if(bird.y>canvas.height||bird.y<0) gameOver();
    if(running) animId = requestAnimationFrame(loop);
  }
  function gameOver(){
    running=false;
    if(score>best){ best=score; localStorage.setItem('flpBest',best); view.querySelector('#flpBest').textContent=best; }
    ctx.fillStyle='rgba(0,0,0,0.6)'; ctx.fillRect(0,0,canvas.width,canvas.height);
    ctx.fillStyle='#00f0c8'; ctx.font='bold 20px Orbitron, sans-serif'; ctx.textAlign='center';
    ctx.fillText('باختی! کلیک کن برای شروع دوباره', canvas.width/2, canvas.height/2);
  }
  function keyHandler(e){ if(e.code==='Space'){ e.preventDefault(); flap(); } }
  canvas.addEventListener('click', flap);
  document.addEventListener('keydown', keyHandler);
  view.querySelector('#flpRestart').onclick = reset;
  reset();
  currentCleanup = ()=>{ running=false; cancelAnimationFrame(animId); document.removeEventListener('keydown', keyHandler); };
  view._cleanup = currentCleanup;
};

/* ============ 7. TETRIS (lite) ============ */
builders.tetris = function(view){
  view.innerHTML = gameTopbar('تتریس','🧩') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="tetScore">0</b></span></div>
      <canvas id="tetCanvas" width="240" height="440"></canvas>
      <div class="controls-hint">جهت چپ/راست: حرکت — جهت بالا: چرخش — جهت پایین: سقوط سریع</div>
      <button class="mini-btn" id="tetRestart">شروع دوباره</button>
    </div>`;
  const canvas = view.querySelector('#tetCanvas');
  const ctx = canvas.getContext('2d');
  const cols=8, rows=16, size=30;
  const SHAPES = [
    [[1,1,1,1]], //I
    [[1,1],[1,1]], //O
    [[0,1,0],[1,1,1]], //T
    [[1,0,0],[1,1,1]], //J
    [[0,0,1],[1,1,1]], //L
    [[1,1,0],[0,1,1]], //S
    [[0,1,1],[1,1,0]], //Z
  ];
  const COLORS = ['#00f0c8','#ffd23f','#7d5fff','#3f7dff','#ff9f3f','#3fff8f','#ff3d81'];
  let board, cur, score, dropTimer, running;

  function newPiece(){
    const idx = Math.floor(Math.random()*SHAPES.length);
    return {shape:SHAPES[idx].map(r=>r.slice()), color:COLORS[idx], x:Math.floor(cols/2)-1, y:0};
  }
  function reset(){
    board = Array.from({length:rows},()=>Array(cols).fill(0));
    cur = newPiece(); score=0; running=true;
    view.querySelector('#tetScore').textContent=score;
    if(dropTimer) clearInterval(dropTimer);
    dropTimer = setInterval(drop, 600);
    draw();
  }
  function collides(shape,ox,oy){
    for(let y=0;y<shape.length;y++)for(let x=0;x<shape[y].length;x++){
      if(!shape[y][x]) continue;
      const nx=ox+x, ny=oy+y;
      if(nx<0||nx>=cols||ny>=rows) return true;
      if(ny>=0 && board[ny][nx]) return true;
    }
    return false;
  }
  function merge(){
    cur.shape.forEach((row,y)=>row.forEach((v,x)=>{ if(v && cur.y+y>=0) board[cur.y+y][cur.x+x]=cur.color; }));
  }
  function clearLines(){
    let cleared=0;
    board = board.filter(row=>{
      if(row.every(c=>c)){ cleared++; return false; }
      return true;
    });
    while(board.length<rows) board.unshift(Array(cols).fill(0));
    if(cleared){ score += cleared*100; view.querySelector('#tetScore').textContent=score; }
  }
  function drop(){
    if(!running) return;
    if(!collides(cur.shape, cur.x, cur.y+1)) cur.y++;
    else {
      merge(); clearLines();
      cur = newPiece();
      if(collides(cur.shape, cur.x, cur.y)){ running=false; clearInterval(dropTimer); draw(true); return; }
    }
    draw();
  }
  function rotate(){
    const s = cur.shape;
    const rotated = s[0].map((_,i)=>s.map(row=>row[i]).reverse());
    if(!collides(rotated, cur.x, cur.y)) cur.shape = rotated;
    draw();
  }
  function draw(gameOver){
    ctx.fillStyle='#04060a'; ctx.fillRect(0,0,canvas.width,canvas.height);
    for(let y=0;y<rows;y++)for(let x=0;x<cols;x++){
      if(board[y][x]){ ctx.fillStyle=board[y][x]; ctx.fillRect(x*size+1,y*size+1,size-2,size-2); }
    }
    ctx.fillStyle=cur.color;
    cur.shape.forEach((row,y)=>row.forEach((v,x)=>{
      if(v) ctx.fillRect((cur.x+x)*size+1,(cur.y+y)*size+1,size-2,size-2);
    }));
    if(gameOver){
      ctx.fillStyle='rgba(0,0,0,0.6)'; ctx.fillRect(0,0,canvas.width,canvas.height);
      ctx.fillStyle='#00f0c8'; ctx.font='bold 18px Orbitron, sans-serif'; ctx.textAlign='center';
      ctx.fillText('بازی تمام شد', canvas.width/2, canvas.height/2);
    }
  }
  function keyHandler(e){
    if(!running) return;
    if(e.key==='ArrowLeft' && !collides(cur.shape,cur.x-1,cur.y)){ cur.x--; draw(); }
    if(e.key==='ArrowRight' && !collides(cur.shape,cur.x+1,cur.y)){ cur.x++; draw(); }
    if(e.key==='ArrowDown') drop();
    if(e.key==='ArrowUp') rotate();
  }
  document.addEventListener('keydown', keyHandler);
  view.querySelector('#tetRestart').onclick = reset;
  reset();
  currentCleanup = ()=>{ running=false; clearInterval(dropTimer); document.removeEventListener('keydown', keyHandler); };
  view._cleanup = currentCleanup;
};

/* ============ 8. WHACK-A-MOLE ============ */
builders.whack = function(view){
  view.innerHTML = gameTopbar('موش‌کوب','🔨') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="wkScore">0</b></span><span>زمان: <b id="wkTime">30</b></span></div>
      <div class="board-grid" id="wkGrid" style="grid-template-columns:repeat(3,90px);grid-template-rows:repeat(3,90px);"></div>
      <button class="mini-btn" id="wkRestart">شروع دوباره</button>
    </div>`;
  const gridEl = view.querySelector('#wkGrid');
  let holes, score, time, moleTimer, countdownTimer, activeHole;
  function reset(){
    score=0; time=30; activeHole=-1;
    view.querySelector('#wkScore').textContent=score;
    view.querySelector('#wkTime').textContent=time;
    render();
    if(moleTimer) clearInterval(moleTimer);
    if(countdownTimer) clearInterval(countdownTimer);
    moleTimer = setInterval(popMole, 800);
    countdownTimer = setInterval(()=>{
      time--; view.querySelector('#wkTime').textContent=time;
      if(time<=0){ clearInterval(moleTimer); clearInterval(countdownTimer); activeHole=-1; render(true); }
    }, 1000);
  }
  function popMole(){ activeHole = Math.floor(Math.random()*9); render(); }
  function render(over){
    gridEl.innerHTML='';
    for(let i=0;i<9;i++){
      const d=document.createElement('div');
      d.className='tile';
      d.style.width='90px'; d.style.height='90px'; d.style.fontSize='2.4rem';
      d.style.background='#161b29'; d.style.border='1px solid #232a3d';
      d.textContent = i===activeHole? '🐹':'';
      d.onclick = ()=>{ if(i===activeHole && time>0){ score++; view.querySelector('#wkScore').textContent=score; activeHole=-1; render(); } };
      gridEl.appendChild(d);
    }
    if(over){
      const msg=document.createElement('div');
      msg.style.gridColumn='1/-1'; msg.style.textAlign='center'; msg.style.color='#00f0c8'; msg.style.fontFamily='Orbitron, sans-serif';
      msg.textContent = `زمان تمام شد! امتیاز نهایی: ${score}`;
      gridEl.appendChild(msg);
    }
  }
  view.querySelector('#wkRestart').onclick = reset;
  reset();
  currentCleanup = ()=>{ clearInterval(moleTimer); clearInterval(countdownTimer); };
  view._cleanup = currentCleanup;
};

/* ============ 9. ROCK PAPER SCISSORS ============ */
builders.rps = function(view){
  view.innerHTML = gameTopbar('سنگ کاغذ قیچی','✊') + `
    <div class="game-stage">
      <div class="hud"><span>برد: <b id="rpsWin">0</b></span><span>باخت: <b id="rpsLose">0</b></span><span>مساوی: <b id="rpsDraw">0</b></span></div>
      <div class="overlay-msg" id="rpsResult">یکی رو انتخاب کن</div>
      <div style="display:flex;gap:16px;">
        <button class="mini-btn" data-c="rock" style="font-size:1.8rem;padding:16px 22px;">✊</button>
        <button class="mini-btn" data-c="paper" style="font-size:1.8rem;padding:16px 22px;">✋</button>
        <button class="mini-btn" data-c="scissors" style="font-size:1.8rem;padding:16px 22px;">✌️</button>
      </div>
    </div>`;
  const emap={rock:'✊',paper:'✋',scissors:'✌️'};
  let win=0,lose=0,draw=0;
  view.querySelectorAll('[data-c]').forEach(btn=>{
    btn.onclick=()=>{
      const player = btn.dataset.c;
      const options=['rock','paper','scissors'];
      const comp = options[Math.floor(Math.random()*3)];
      let result;
      if(player===comp) { result='مساوی شد 🤝'; draw++; }
      else if((player==='rock'&&comp==='scissors')||(player==='paper'&&comp==='rock')||(player==='scissors'&&comp==='paper')){ result='بردی! 🎉'; win++; }
      else { result='باختی 😅'; lose++; }
      view.querySelector('#rpsResult').textContent = `تو: ${emap[player]}  کامپیوتر: ${emap[comp]}  —  ${result}`;
      view.querySelector('#rpsWin').textContent=win;
      view.querySelector('#rpsLose').textContent=lose;
      view.querySelector('#rpsDraw').textContent=draw;
    };
  });
  currentCleanup=null;
};

/* ============ 10. REACTION TEST ============ */
builders.reaction = function(view){
  view.innerHTML = gameTopbar('تست واکنش','⚡') + `
    <div class="game-stage">
      <div class="hud"><span>بهترین زمان: <b id="rtBest">--</b> ms</span></div>
      <div id="rtBox" style="width:100%;max-width:420px;height:260px;border-radius:12px;display:flex;align-items:center;justify-content:center;font-family:'Orbitron',sans-serif;font-size:1.3rem;cursor:pointer;background:#161b29;border:1px solid #232a3d;transition:background .15s;">برای شروع کلیک کن</div>
    </div>`;
  const box = view.querySelector('#rtBox');
  let state='idle', startTime, timeoutId, best=+(localStorage.getItem('rtBest')||0);
  if(best) view.querySelector('#rtBest').textContent = best;
  function toIdle(){
    state='idle'; box.style.background='#161b29'; box.textContent='برای شروع کلیک کن';
  }
  box.onclick = ()=>{
    if(state==='idle'){
      state='waiting'; box.style.background='#2a1420'; box.textContent='صبر کن... رنگ سبز رو ببین';
      const delay = 1200+Math.random()*2500;
      timeoutId = setTimeout(()=>{
        state='ready'; box.style.background='rgba(0,240,200,0.25)'; box.textContent='همین الان کلیک کن!';
        startTime = performance.now();
      }, delay);
    } else if(state==='waiting'){
      clearTimeout(timeoutId);
      box.style.background='#161b29'; box.textContent='زودتر از موعد کلیک کردی! دوباره امتحان کن';
      state='idle';
    } else if(state==='ready'){
      const rt = Math.round(performance.now()-startTime);
      if(!best || rt<best){ best=rt; localStorage.setItem('rtBest',best); view.querySelector('#rtBest').textContent=best; }
      box.style.background='#161b29';
      box.textContent = `زمان واکنش: ${rt} ms — دوباره امتحان کن`;
      state='idle';
    }
  };
  currentCleanup = ()=>clearTimeout(timeoutId);
  view._cleanup = currentCleanup;
};

/* ============ 11. PONG ============ */
builders.pong = function(view){
  view.innerHTML = gameTopbar('پونگ','🏓') + `
    <div class="game-stage">
      <div class="hud"><span>تو: <b id="pongYou">0</b></span><span>کامپیوتر: <b id="pongCpu">0</b></span></div>
      <canvas id="pongCanvas" width="420" height="300"></canvas>
      <div class="controls-hint">با موس یا کلیدهای جهت بالا/پایین راکت رو حرکت بده.</div>
      <button class="mini-btn" id="pongRestart">شروع دوباره</button>
    </div>`;
  const canvas = view.querySelector('#pongCanvas');
  const ctx = canvas.getContext('2d');
  let you, cpu, ball, scoreYou, scoreCpu, running, animId;
  function reset(){
    you={y:120,h:60}; cpu={y:120,h:60};
    ball={x:210,y:150,dx:4,dy:3,r:7};
    scoreYou=0; scoreCpu=0; running=true;
    view.querySelector('#pongYou').textContent=0;
    view.querySelector('#pongCpu').textContent=0;
    if(animId) cancelAnimationFrame(animId);
    loop();
  }
  function loop(){
    if(!running) return;
    ctx.fillStyle='#04060a'; ctx.fillRect(0,0,canvas.width,canvas.height);
    ctx.strokeStyle='#232a3d'; ctx.setLineDash([6,6]); ctx.beginPath(); ctx.moveTo(210,0); ctx.lineTo(210,300); ctx.stroke(); ctx.setLineDash([]);
    cpu.y += (ball.y-(cpu.y+cpu.h/2))*0.06;
    cpu.y = Math.max(0,Math.min(canvas.height-cpu.h, cpu.y));
    ball.x+=ball.dx; ball.y+=ball.dy;
    if(ball.y<ball.r||ball.y>canvas.height-ball.r) ball.dy*=-1;
    if(ball.x<18 && ball.y>you.y && ball.y<you.y+you.h) ball.dx=Math.abs(ball.dx);
    if(ball.x>canvas.width-18 && ball.y>cpu.y && ball.y<cpu.y+cpu.h) ball.dx=-Math.abs(ball.dx);
    if(ball.x<0){ scoreCpu++; view.querySelector('#pongCpu').textContent=scoreCpu; ball={x:210,y:150,dx:4,dy:3,r:7}; }
    if(ball.x>canvas.width){ scoreYou++; view.querySelector('#pongYou').textContent=scoreYou; ball={x:210,y:150,dx:-4,dy:3,r:7}; }
    ctx.fillStyle='#00f0c8'; ctx.fillRect(8, you.y, 10, you.h);
    ctx.fillStyle='#ff3d81'; ctx.fillRect(canvas.width-18, cpu.y, 10, cpu.h);
    ctx.fillStyle='#eef1f8'; ctx.beginPath(); ctx.arc(ball.x,ball.y,ball.r,0,Math.PI*2); ctx.fill();
    animId=requestAnimationFrame(loop);
  }
  function mouseHandler(e){
    const rect=canvas.getBoundingClientRect();
    const y=(e.clientY-rect.top)*(canvas.height/rect.height);
    you.y = Math.max(0,Math.min(canvas.height-you.h, y-you.h/2));
  }
  function keyHandler(e){
    if(e.key==='ArrowUp') you.y=Math.max(0,you.y-25);
    if(e.key==='ArrowDown') you.y=Math.min(canvas.height-you.h,you.y+25);
  }
  canvas.addEventListener('mousemove', mouseHandler);
  document.addEventListener('keydown', keyHandler);
  view.querySelector('#pongRestart').onclick=reset;
  reset();
  currentCleanup=()=>{ running=false; cancelAnimationFrame(animId); document.removeEventListener('keydown', keyHandler); };
  view._cleanup=currentCleanup;
};

/* ============ 12. MINESWEEPER ============ */
builders.minesweeper = function(view){
  view.innerHTML = gameTopbar('مین‌یاب','💣') + `
    <div class="game-stage">
      <div class="hud"><span>مین‌ها: <b id="msMines">10</b></span><span id="msStatus">در حال بازی</span></div>
      <div class="board-grid" id="msGrid" style="grid-template-columns:repeat(9,32px);gap:3px;"></div>
      <div class="controls-hint">کلیک چپ: باز کردن — کلیک راست: علامت‌گذاری مین</div>
      <button class="mini-btn" id="msRestart">شروع دوباره</button>
    </div>`;
  const gridEl = view.querySelector('#msGrid');
  const size=9, mineCount=10;
  let board, revealed, flagged, gameOver;
  function reset(){
    board=Array.from({length:size},()=>Array(size).fill(0));
    revealed=Array.from({length:size},()=>Array(size).fill(false));
    flagged=Array.from({length:size},()=>Array(size).fill(false));
    gameOver=false;
    let placed=0;
    while(placed<mineCount){
      const r=Math.floor(Math.random()*size), c=Math.floor(Math.random()*size);
      if(board[r][c]!==-1){ board[r][c]=-1; placed++; }
    }
    for(let r=0;r<size;r++)for(let c=0;c<size;c++){
      if(board[r][c]===-1) continue;
      let count=0;
      for(let dr=-1;dr<=1;dr++)for(let dc=-1;dc<=1;dc++){
        const nr=r+dr,nc=c+dc;
        if(nr>=0&&nr<size&&nc>=0&&nc<size&&board[nr][nc]===-1) count++;
      }
      board[r][c]=count;
    }
    view.querySelector('#msStatus').textContent='در حال بازی';
    view.querySelector('#msMines').textContent=mineCount;
    render();
  }
  function reveal(r,c){
    if(r<0||r>=size||c<0||c>=size||revealed[r][c]||flagged[r][c]) return;
    revealed[r][c]=true;
    if(board[r][c]===0){
      for(let dr=-1;dr<=1;dr++)for(let dc=-1;dc<=1;dc++) reveal(r+dr,c+dc);
    }
  }
  function render(){
    gridEl.innerHTML='';
    for(let r=0;r<size;r++)for(let c=0;c<size;c++){
      const d=document.createElement('div');
      d.className='tile';
      d.style.width='32px'; d.style.height='32px'; d.style.fontSize='.9rem';
      if(revealed[r][c]){
        d.style.background = board[r][c]===-1? '#ff3d81':'#161b29';
        d.style.border='1px solid #232a3d';
        d.textContent = board[r][c]===-1? '💣' : (board[r][c]||'');
        const numColors=['','#00f0c8','#ffd23f','#ff3d81','#7d5fff','#3f7dff','#ff9f3f','#3fff8f','#eef1f8'];
        d.style.color = numColors[board[r][c]]||'#eef1f8';
      } else {
        d.style.background='#1b2233'; d.style.border='1px solid #2a3350';
        d.textContent = flagged[r][c]? '🚩':'';
      }
      d.onclick=()=>{
        if(gameOver||flagged[r][c]) return;
        if(board[r][c]===-1){
          gameOver=true;
          for(let rr=0;rr<size;rr++)for(let cc=0;cc<size;cc++) if(board[rr][cc]===-1) revealed[rr][cc]=true;
          view.querySelector('#msStatus').textContent='باختی! 💥';
          render(); return;
        }
        reveal(r,c);
        checkWin();
        render();
      };
      d.oncontextmenu=(e)=>{
        e.preventDefault();
        if(gameOver||revealed[r][c]) return;
        flagged[r][c]=!flagged[r][c];
        render();
      };
      gridEl.appendChild(d);
    }
  }
  function checkWin(){
    let safeLeft=0;
    for(let r=0;r<size;r++)for(let c=0;c<size;c++) if(board[r][c]!==-1 && !revealed[r][c]) safeLeft++;
    if(safeLeft===0){ gameOver=true; view.querySelector('#msStatus').textContent='بردی! 🎉'; }
  }
  view.querySelector('#msRestart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 13. SIMON ============ */
builders.simon = function(view){
  view.innerHTML = gameTopbar('سایمون','🎵') + `
    <div class="game-stage">
      <div class="hud"><span>دور: <b id="simRound">0</b></span><span>بهترین: <b id="simBest">0</b></span></div>
      <div style="display:grid;grid-template-columns:repeat(2,110px);grid-template-rows:repeat(2,110px);gap:10px;">
        <div class="simon-pad" data-c="0" style="background:#00f0c8;border-radius:14px;cursor:pointer;transition:filter .15s, transform .1s;"></div>
        <div class="simon-pad" data-c="1" style="background:#ff3d81;border-radius:14px;cursor:pointer;transition:filter .15s, transform .1s;"></div>
        <div class="simon-pad" data-c="2" style="background:#ffd23f;border-radius:14px;cursor:pointer;transition:filter .15s, transform .1s;"></div>
        <div class="simon-pad" data-c="3" style="background:#7d5fff;border-radius:14px;cursor:pointer;transition:filter .15s, transform .1s;"></div>
      </div>
      <div class="overlay-msg" id="simMsg">برای شروع کلیک کن</div>
      <button class="mini-btn" id="simRestart">شروع دوباره</button>
    </div>`;
  const pads = view.querySelectorAll('.simon-pad');
  let seq, playerIdx, round, best=+(localStorage.getItem('simBest')||0), accepting;
  view.querySelector('#simBest').textContent=best;
  function reset(){
    seq=[]; round=0; accepting=false;
    view.querySelector('#simRound').textContent=0;
    view.querySelector('#simMsg').textContent='برای شروع کلیک کن';
    nextRound();
  }
  function nextRound(){
    seq.push(Math.floor(Math.random()*4));
    round++; playerIdx=0; accepting=false;
    view.querySelector('#simRound').textContent=round;
    view.querySelector('#simMsg').textContent='به دنباله نگاه کن...';
    playSeq();
  }
  function flash(i){
    return new Promise(res=>{
      pads[i].style.filter='brightness(2)'; pads[i].style.transform='scale(0.95)';
      setTimeout(()=>{ pads[i].style.filter=''; pads[i].style.transform=''; res(); }, 320);
    });
  }
  async function playSeq(){
    await new Promise(r=>setTimeout(r,400));
    for(const i of seq){ await flash(i); await new Promise(r=>setTimeout(r,180)); }
    accepting=true;
    view.querySelector('#simMsg').textContent='نوبت توئه!';
  }
  pads.forEach(pad=>{
    pad.onclick=async ()=>{
      if(!accepting) return;
      const i=+pad.dataset.c;
      await flash(i);
      if(i===seq[playerIdx]){
        playerIdx++;
        if(playerIdx===seq.length){
          accepting=false;
          if(round>best){ best=round; localStorage.setItem('simBest',best); view.querySelector('#simBest').textContent=best; }
          setTimeout(nextRound, 600);
        }
      } else {
        accepting=false;
        view.querySelector('#simMsg').textContent=`باختی! دور ${round} — دوباره امتحان کن`;
      }
    };
  });
  view.querySelector('#simRestart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 14. CONNECT FOUR ============ */
builders.connect4 = function(view){
  view.innerHTML = gameTopbar('چهار در ردیف','🔴') + `
    <div class="game-stage">
      <div class="hud" id="c4Status">نوبت شما 🔴</div>
      <div class="board-grid" id="c4Grid" style="grid-template-columns:repeat(7,48px);gap:5px;background:#0d1119;padding:10px;border-radius:10px;"></div>
      <button class="mini-btn" id="c4Restart">شروع دوباره</button>
    </div>`;
  const gridEl = view.querySelector('#c4Grid');
  const rows=6, cols=7;
  let board, gameOver;
  function reset(){
    board=Array.from({length:rows},()=>Array(cols).fill(0));
    gameOver=false;
    view.querySelector('#c4Status').textContent='نوبت شما 🔴';
    render();
  }
  function render(){
    gridEl.innerHTML='';
    for(let r=0;r<rows;r++)for(let c=0;c<cols;c++){
      const d=document.createElement('div');
      d.style.width='48px'; d.style.height='48px'; d.style.borderRadius='50%';
      d.style.background = board[r][c]===1?'#ff3d81':board[r][c]===2?'#ffd23f':'#161b29';
      d.style.cursor='pointer';
      d.onclick=()=>dropDisc(c);
      gridEl.appendChild(d);
    }
  }
  function dropDisc(c){
    if(gameOver) return;
    for(let r=rows-1;r>=0;r--){
      if(board[r][c]===0){
        board[r][c]=1; render();
        if(checkWin(1)){ view.querySelector('#c4Status').textContent='بردی! 🎉'; gameOver=true; return; }
        if(board.flat().every(v=>v)){ view.querySelector('#c4Status').textContent='مساوی'; gameOver=true; return; }
        view.querySelector('#c4Status').textContent='نوبت کامپیوتر...';
        setTimeout(cpuMove, 450);
        return;
      }
    }
  }
  function cpuMove(){
    if(gameOver) return;
    const options=[];
    for(let c=0;c<cols;c++) if(board[0][c]===0) options.push(c);
    const c = options[Math.floor(Math.random()*options.length)];
    for(let r=rows-1;r>=0;r--){
      if(board[r][c]===0){
        board[r][c]=2; render();
        if(checkWin(2)){ view.querySelector('#c4Status').textContent='باختی! 😅'; gameOver=true; return; }
        if(board.flat().every(v=>v)){ view.querySelector('#c4Status').textContent='مساوی'; gameOver=true; return; }
        view.querySelector('#c4Status').textContent='نوبت شما 🔴';
        return;
      }
    }
  }
  function checkWin(p){
    for(let r=0;r<rows;r++)for(let c=0;c<cols;c++){
      if(c+3<cols && [0,1,2,3].every(i=>board[r][c+i]===p)) return true;
      if(r+3<rows && [0,1,2,3].every(i=>board[r+i][c]===p)) return true;
      if(r+3<rows&&c+3<cols && [0,1,2,3].every(i=>board[r+i][c+i]===p)) return true;
      if(r-3>=0&&c+3<cols && [0,1,2,3].every(i=>board[r-i][c+i]===p)) return true;
    }
    return false;
  }
  view.querySelector('#c4Restart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 15. WORD GUESS ============ */
builders.wordguess = function(view){
  view.innerHTML = gameTopbar('حدس کلمه','🔤') + `
    <div class="game-stage">
      <div class="hud"><span>جون: <b id="wgLives">6</b></span></div>
      <div class="overlay-msg" id="wgWord" style="letter-spacing:6px;font-size:1.6rem;"></div>
      <div id="wgLetters" style="display:flex;flex-wrap:wrap;gap:8px;max-width:480px;justify-content:center;"></div>
      <div class="controls-hint" id="wgHint"></div>
      <button class="mini-btn" id="wgRestart">شروع دوباره</button>
    </div>`;
  const words = [
    {w:'ایران', hint:'نام یک کشور'},
    {w:'رایانه', hint:'دستگاه محاسباتی'},
    {w:'کتابخانه', hint:'محل نگهداری کتاب‌ها'},
    {w:'دریا', hint:'حجم بزرگ آب شور'},
    {w:'ستاره', hint:'جسم نورانی در آسمان شب'},
  ];
  let target, guessed, lives;
  function reset(){
    const pick = words[Math.floor(Math.random()*words.length)];
    target = pick.w; guessed=[]; lives=6;
    view.querySelector('#wgHint').textContent = 'راهنمایی: '+pick.hint;
    view.querySelector('#wgLives').textContent=lives;
    renderWord(); renderLetters();
  }
  function renderWord(){
    view.querySelector('#wgWord').textContent = target.split('').map(ch=>guessed.includes(ch)?ch:'_').join(' ');
  }
  function renderLetters(){
    const letters = 'اآبپتثجچحخدذرزژسشصضطظعغفقکگلمنوهی';
    const box = view.querySelector('#wgLetters');
    box.innerHTML='';
    letters.split('').forEach(ch=>{
      const btn=document.createElement('button');
      btn.className='mini-btn'; btn.textContent=ch; btn.style.width='40px'; btn.style.padding='8px 0';
      if(guessed.includes(ch)){ btn.disabled=true; btn.style.opacity=.35; }
      btn.onclick=()=>{
        guessed.push(ch);
        if(!target.includes(ch)){
          lives--; view.querySelector('#wgLives').textContent=lives;
          if(lives<=0){ view.querySelector('#wgWord').textContent = 'باختی! کلمه: '+target; box.innerHTML=''; return; }
        }
        renderWord(); renderLetters();
        if(target.split('').every(c=>guessed.includes(c))){
          view.querySelector('#wgWord').textContent = target+' — بردی! 🎉';
          box.innerHTML='';
        }
      };
      box.appendChild(btn);
    });
  }
  view.querySelector('#wgRestart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 16. MATH CHALLENGE ============ */
builders.math = function(view){
  view.innerHTML = gameTopbar('چالش ریاضی','➗') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="mathScore">0</b></span><span>زمان: <b id="mathTime">30</b></span></div>
      <div class="overlay-msg" id="mathQ" style="font-size:2rem;"></div>
      <input id="mathInput" type="number" style="width:160px;padding:12px;border-radius:8px;border:1px solid #232a3d;background:#0d1119;color:#eef1f8;font-size:1.2rem;text-align:center;">
      <button class="mini-btn" id="mathSubmit">ثبت جواب</button>
      <button class="mini-btn" id="mathRestart">شروع دوباره</button>
    </div>`;
  let score, time, answer, timer;
  function newQ(){
    const a=Math.floor(Math.random()*20)+1, b=Math.floor(Math.random()*20)+1;
    const ops=['+','-','×']; const op=ops[Math.floor(Math.random()*3)];
    answer = op==='+'? a+b : op==='-'? a-b : a*b;
    view.querySelector('#mathQ').textContent = `${a} ${op} ${b} = ?`;
    view.querySelector('#mathInput').value='';
    view.querySelector('#mathInput').focus();
  }
  function reset(){
    score=0; time=30;
    view.querySelector('#mathScore').textContent=0;
    view.querySelector('#mathTime').textContent=time;
    newQ();
    if(timer) clearInterval(timer);
    timer=setInterval(()=>{
      time--; view.querySelector('#mathTime').textContent=time;
      if(time<=0){ clearInterval(timer); view.querySelector('#mathQ').textContent=`زمان تمام شد! امتیاز: ${score}`; view.querySelector('#mathInput').disabled=true; }
    },1000);
  }
  function submit(){
    if(time<=0) return;
    if(+view.querySelector('#mathInput').value === answer){ score++; view.querySelector('#mathScore').textContent=score; }
    newQ();
  }
  view.querySelector('#mathSubmit').onclick=submit;
  view.querySelector('#mathInput').addEventListener('keydown', e=>{ if(e.key==='Enter') submit(); });
  view.querySelector('#mathRestart').onclick=reset;
  reset();
  currentCleanup=()=>clearInterval(timer);
  view._cleanup=currentCleanup;
};

/* ============ 17. COLOR MATCH (Stroop) ============ */
builders.colormatch = function(view){
  view.innerHTML = gameTopbar('تطبیق رنگ','🎨') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="cmScore">0</b></span><span>زمان: <b id="cmTime">20</b></span></div>
      <div id="cmWord" style="font-family:'Orbitron',sans-serif;font-size:2.4rem;font-weight:bold;"></div>
      <div class="controls-hint">آیا رنگ نوشته با معنی کلمه یکی است؟</div>
      <div style="display:flex;gap:14px;">
        <button class="mini-btn" id="cmYes" style="padding:14px 26px;">✅ بله</button>
        <button class="mini-btn" id="cmNo" style="padding:14px 26px;">❌ خیر</button>
      </div>
      <button class="mini-btn" id="cmRestart">شروع دوباره</button>
    </div>`;
  const colorNames = [{n:'قرمز',c:'#ff3d81'},{n:'زرد',c:'#ffd23f'},{n:'سبز',c:'#00f0c8'},{n:'بنفش',c:'#7d5fff'}];
  let score, time, timer, isMatch;
  function newRound(){
    const wordObj = colorNames[Math.floor(Math.random()*4)];
    const match = Math.random()<0.5;
    let colorObj = wordObj;
    if(!match){ do{ colorObj = colorNames[Math.floor(Math.random()*4)]; } while(colorObj.n===wordObj.n); }
    isMatch = match;
    const w = view.querySelector('#cmWord');
    w.textContent = wordObj.n;
    w.style.color = colorObj.c;
  }
  function reset(){
    score=0; time=20;
    view.querySelector('#cmScore').textContent=0;
    view.querySelector('#cmTime').textContent=time;
    newRound();
    if(timer) clearInterval(timer);
    timer=setInterval(()=>{
      time--; view.querySelector('#cmTime').textContent=time;
      if(time<=0){ clearInterval(timer); view.querySelector('#cmWord').textContent='تمام شد!'; view.querySelector('#cmWord').style.color='#00f0c8'; }
    },1000);
  }
  function answer(userSaysMatch){
    if(time<=0) return;
    if(userSaysMatch===isMatch){ score++; view.querySelector('#cmScore').textContent=score; }
    newRound();
  }
  view.querySelector('#cmYes').onclick=()=>answer(true);
  view.querySelector('#cmNo').onclick=()=>answer(false);
  view.querySelector('#cmRestart').onclick=reset;
  reset();
  currentCleanup=()=>clearInterval(timer);
  view._cleanup=currentCleanup;
};

/* ============ 18. DINO RUNNER ============ */
builders.dino = function(view){
  view.innerHTML = gameTopbar('دایناسور پرشی','🦖') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="dinoScore">0</b></span><span>بهترین: <b id="dinoBest">0</b></span></div>
      <canvas id="dinoCanvas" width="420" height="180"></canvas>
      <div class="controls-hint">کلید Space یا کلیک برای پریدن.</div>
      <button class="mini-btn" id="dinoRestart">شروع دوباره</button>
    </div>`;
  const canvas=view.querySelector('#dinoCanvas'); const ctx=canvas.getContext('2d');
  let dino, obstacles, score, best=+(localStorage.getItem('dinoBest')||0), running, animId, speed, frame;
  view.querySelector('#dinoBest').textContent=best;
  function reset(){
    dino={y:130,vy:0,h:30,jumping:false};
    obstacles=[]; score=0; speed=5; frame=0; running=true;
    view.querySelector('#dinoScore').textContent=0;
    if(animId) cancelAnimationFrame(animId);
    loop();
  }
  function jump(){ if(!dino.jumping && running){ dino.vy=-9; dino.jumping=true; } else if(!running) reset(); }
  function loop(){
    if(!running) return;
    frame++;
    ctx.fillStyle='#04060a'; ctx.fillRect(0,0,canvas.width,canvas.height);
    ctx.strokeStyle='#232a3d'; ctx.beginPath(); ctx.moveTo(0,160); ctx.lineTo(420,160); ctx.stroke();
    dino.vy+=0.5; dino.y+=dino.vy;
    if(dino.y>130){ dino.y=130; dino.vy=0; dino.jumping=false; }
    ctx.fillStyle='#00f0c8'; ctx.fillRect(40,dino.y,26,30);
    if(frame%Math.max(50-Math.floor(speed),25)===0) obstacles.push({x:420,w:14,h:28+Math.random()*14});
    obstacles.forEach(o=>o.x-=speed);
    obstacles = obstacles.filter(o=>o.x>-20);
    ctx.fillStyle='#ff3d81';
    obstacles.forEach(o=>{
      ctx.fillRect(o.x,160-o.h,o.w,o.h);
      if(40+26>o.x && 40<o.x+o.w && dino.y+30>160-o.h) gameOver();
    });
    score++; speed=5+score/500;
    view.querySelector('#dinoScore').textContent=Math.floor(score/5);
    if(running) animId=requestAnimationFrame(loop);
  }
  function gameOver(){
    running=false;
    const s=Math.floor(score/5);
    if(s>best){ best=s; localStorage.setItem('dinoBest',best); view.querySelector('#dinoBest').textContent=best; }
    ctx.fillStyle='rgba(0,0,0,.6)'; ctx.fillRect(0,0,canvas.width,canvas.height);
    ctx.fillStyle='#00f0c8'; ctx.font='bold 18px Orbitron, sans-serif'; ctx.textAlign='center';
    ctx.fillText('باختی! کلیک کن برای شروع دوباره', 210, 90);
  }
  function keyHandler(e){ if(e.code==='Space'){ e.preventDefault(); jump(); } }
  canvas.addEventListener('click', jump);
  document.addEventListener('keydown', keyHandler);
  view.querySelector('#dinoRestart').onclick=reset;
  reset();
  currentCleanup=()=>{ running=false; cancelAnimationFrame(animId); document.removeEventListener('keydown', keyHandler); };
  view._cleanup=currentCleanup;
};

/* ============ 19. ASTEROIDS ============ */
builders.asteroids = function(view){
  view.innerHTML = gameTopbar('سیارک‌ها','☄️') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="astScore">0</b></span></div>
      <canvas id="astCanvas" width="420" height="380"></canvas>
      <div class="controls-hint">چپ/راست: چرخش — بالا: حرکت — Space: شلیک</div>
      <button class="mini-btn" id="astRestart">شروع دوباره</button>
    </div>`;
  const canvas=view.querySelector('#astCanvas'); const ctx=canvas.getContext('2d');
  let ship, bullets, rocks, score, keys, running, animId;
  function reset(){
    ship={x:210,y:190,angle:0,vx:0,vy:0};
    bullets=[]; rocks=[]; score=0; keys={}; running=true;
    for(let i=0;i<5;i++) rocks.push(spawnRock());
    view.querySelector('#astScore').textContent=0;
    if(animId) cancelAnimationFrame(animId);
    loop();
  }
  function spawnRock(){
    return {x:Math.random()*420, y:Math.random()*380, vx:(Math.random()-0.5)*2, vy:(Math.random()-0.5)*2, r:20+Math.random()*10};
  }
  function loop(){
    if(!running) return;
    ctx.fillStyle='#04060a'; ctx.fillRect(0,0,canvas.width,canvas.height);
    if(keys['ArrowLeft']) ship.angle-=0.08;
    if(keys['ArrowRight']) ship.angle+=0.08;
    if(keys['ArrowUp']){ ship.vx+=Math.sin(ship.angle)*0.12; ship.vy-=Math.cos(ship.angle)*0.12; }
    ship.x+=ship.vx; ship.y+=ship.vy; ship.vx*=0.99; ship.vy*=0.99;
    ship.x=(ship.x+420)%420; ship.y=(ship.y+380)%380;
    ctx.save(); ctx.translate(ship.x,ship.y); ctx.rotate(ship.angle);
    ctx.strokeStyle='#00f0c8'; ctx.beginPath(); ctx.moveTo(0,-12); ctx.lineTo(8,10); ctx.lineTo(-8,10); ctx.closePath(); ctx.stroke();
    ctx.restore();
    bullets.forEach(b=>{ b.x+=b.vx; b.y+=b.vy; });
    bullets = bullets.filter(b=>b.life-- >0);
    ctx.fillStyle='#ffd23f';
    bullets.forEach(b=>ctx.fillRect(b.x-1,b.y-1,3,3));
    rocks.forEach(r=>{
      r.x+=r.vx; r.y+=r.vy;
      r.x=(r.x+420)%420; r.y=(r.y+380)%380;
      ctx.strokeStyle='#ff3d81'; ctx.beginPath(); ctx.arc(r.x,r.y,r.r,0,Math.PI*2); ctx.stroke();
    });
    for(let i=rocks.length-1;i>=0;i--){
      for(let j=bullets.length-1;j>=0;j--){
        const dx=rocks[i].x-bullets[j].x, dy=rocks[i].y-bullets[j].y;
        if(Math.hypot(dx,dy)<rocks[i].r){
          rocks.splice(i,1); bullets.splice(j,1); score+=10;
          view.querySelector('#astScore').textContent=score;
          rocks.push(spawnRock());
          break;
        }
      }
    }
    rocks.forEach(r=>{
      if(Math.hypot(ship.x-r.x, ship.y-r.y)<r.r+8) gameOver();
    });
    if(running) animId=requestAnimationFrame(loop);
  }
  function shoot(){
    bullets.push({x:ship.x+Math.sin(ship.angle)*12, y:ship.y-Math.cos(ship.angle)*12, vx:Math.sin(ship.angle)*6, vy:-Math.cos(ship.angle)*6, life:60});
  }
  function gameOver(){
    running=false;
    ctx.fillStyle='rgba(0,0,0,.6)'; ctx.fillRect(0,0,canvas.width,canvas.height);
    ctx.fillStyle='#00f0c8'; ctx.font='bold 18px Orbitron, sans-serif'; ctx.textAlign='center';
    ctx.fillText(`برخورد کردی! امتیاز: ${score}`, 210, 190);
  }
  function keyDown(e){ keys[e.key]=true; if(e.code==='Space'){ e.preventDefault(); if(running) shoot(); } }
  function keyUp(e){ keys[e.key]=false; }
  document.addEventListener('keydown', keyDown);
  document.addEventListener('keyup', keyUp);
  view.querySelector('#astRestart').onclick=reset;
  reset();
  currentCleanup=()=>{ running=false; cancelAnimationFrame(animId); document.removeEventListener('keydown', keyDown); document.removeEventListener('keyup', keyUp); };
  view._cleanup=currentCleanup;
};

/* ============ 20. LIGHTS OUT ============ */
builders.lightsout = function(view){
  view.innerHTML = gameTopbar('چراغ‌ها خاموش','💡') + `
    <div class="game-stage">
      <div class="hud"><span>حرکت‌ها: <b id="loMoves">0</b></span></div>
      <div class="board-grid" id="loGrid" style="grid-template-columns:repeat(5,60px);gap:6px;"></div>
      <button class="mini-btn" id="loRestart">شروع دوباره</button>
    </div>`;
  const gridEl = view.querySelector('#loGrid');
  const size=5;
  let board, moves;
  function reset(){
    board=Array.from({length:size},()=>Array(size).fill(false));
    for(let i=0;i<15;i++) toggle(Math.floor(Math.random()*size), Math.floor(Math.random()*size), false);
    moves=0;
    view.querySelector('#loMoves').textContent=0;
    render();
  }
  function toggle(r,c, count=true){
    [[0,0],[1,0],[-1,0],[0,1],[0,-1]].forEach(([dr,dc])=>{
      const nr=r+dr, nc=c+dc;
      if(nr>=0&&nr<size&&nc>=0&&nc<size) board[nr][nc]=!board[nr][nc];
    });
    if(count){ moves++; view.querySelector('#loMoves').textContent=moves; }
  }
  function render(){
    gridEl.innerHTML='';
    for(let r=0;r<size;r++)for(let c=0;c<size;c++){
      const d=document.createElement('div');
      d.className='tile';
      d.style.width='60px'; d.style.height='60px';
      d.style.background = board[r][c]? '#ffd23f':'#161b29';
      d.style.border='1px solid #232a3d';
      d.style.boxShadow = board[r][c]? '0 0 18px rgba(255,210,63,.6)':'none';
      d.onclick=()=>{ toggle(r,c); render(); if(board.flat().every(v=>!v)) setTimeout(()=>alert('بردی! 🎉 حرکت‌ها: '+moves),100); };
      gridEl.appendChild(d);
    }
  }
  view.querySelector('#loRestart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 21. WORDLE ============ */
builders.wordle = function(view){
  view.innerHTML = gameTopbar('حدس پنج‌حرفی','🟩') + `
    <div class="game-stage">
      <div class="hud">حدس بزن (انگلیسی، ۵ حرف)</div>
      <div class="board-grid" id="wdGrid" style="grid-template-columns:repeat(5,50px);gap:6px;"></div>
      <input id="wdInput" maxlength="5" style="width:160px;padding:10px;text-align:center;text-transform:uppercase;border-radius:8px;border:1px solid #232a3d;background:#0d1119;color:#eef1f8;font-size:1.1rem;">
      <button class="mini-btn" id="wdSubmit">حدس بزن</button>
      <div class="controls-hint" id="wdMsg"></div>
      <button class="mini-btn" id="wdRestart">شروع دوباره</button>
    </div>`;
  const words=['APPLE','BRAVE','CHESS','DANCE','EAGLE','FLAME','GRAPE','HOUSE','LIGHT','MUSIC'];
  let target, attempts, maxAttempts=6, rows;
  function reset(){
    target = words[Math.floor(Math.random()*words.length)];
    attempts=0; rows=[];
    view.querySelector('#wdMsg').textContent='';
    view.querySelector('#wdInput').disabled=false;
    render();
  }
  function render(){
    const gridEl=view.querySelector('#wdGrid');
    gridEl.innerHTML='';
    for(let r=0;r<maxAttempts;r++){
      for(let c=0;c<5;c++){
        const d=document.createElement('div');
        d.className='tile'; d.style.width='50px'; d.style.height='50px'; d.style.fontSize='1.3rem';
        d.style.border='1px solid #232a3d';
        if(rows[r]){
          d.textContent=rows[r].letters[c];
          d.style.background = rows[r].colors[c]==='g'?'#00f0c8':rows[r].colors[c]==='y'?'#ffd23f':'#161b29';
          d.style.color = rows[r].colors[c]==='none'?'#eef1f8':'#04120e';
        } else d.style.background='#161b29';
        gridEl.appendChild(d);
      }
    }
  }
  function submit(){
    const input = view.querySelector('#wdInput').value.toUpperCase();
    if(input.length!==5 || attempts>=maxAttempts) return;
    const colors = input.split('').map((ch,i)=> ch===target[i]? 'g' : target.includes(ch)? 'y':'none');
    rows.push({letters:input.split(''), colors});
    attempts++;
    view.querySelector('#wdInput').value='';
    render();
    if(input===target){ view.querySelector('#wdMsg').textContent='بردی! 🎉'; view.querySelector('#wdInput').disabled=true; }
    else if(attempts>=maxAttempts){ view.querySelector('#wdMsg').textContent='باختی! کلمه: '+target; view.querySelector('#wdInput').disabled=true; }
  }
  view.querySelector('#wdSubmit').onclick=submit;
  view.querySelector('#wdInput').addEventListener('keydown', e=>{ if(e.key==='Enter') submit(); });
  view.querySelector('#wdRestart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 22. MINI SUDOKU 4x4 ============ */
builders.sudoku = function(view){
  view.innerHTML = gameTopbar('سودوکو مینی','🔢') + `
    <div class="game-stage">
      <div class="hud" id="sdStatus">جدول رو با اعداد ۱ تا ۴ کامل کن</div>
      <div class="board-grid" id="sdGrid" style="grid-template-columns:repeat(4,64px);gap:4px;"></div>
      <button class="mini-btn" id="sdCheck">بررسی جواب</button>
      <button class="mini-btn" id="sdRestart">شروع دوباره</button>
    </div>`;
  const solution=[[1,2,3,4],[3,4,1,2],[2,1,4,3],[4,3,2,1]];
  let puzzle, fixed;
  function reset(){
    puzzle = solution.map(row=>row.slice());
    fixed = Array.from({length:4},()=>Array(4).fill(false));
    let removed=0;
    while(removed<8){
      const r=Math.floor(Math.random()*4), c=Math.floor(Math.random()*4);
      if(puzzle[r][c]!==0){ puzzle[r][c]=0; removed++; }
    }
    for(let r=0;r<4;r++)for(let c=0;c<4;c++) fixed[r][c] = puzzle[r][c]!==0;
    view.querySelector('#sdStatus').textContent='جدول رو با اعداد ۱ تا ۴ کامل کن';
    render();
  }
  function render(){
    const gridEl=view.querySelector('#sdGrid');
    gridEl.innerHTML='';
    for(let r=0;r<4;r++)for(let c=0;c<4;c++){
      const inp=document.createElement('input');
      inp.maxLength=1;
      inp.style.cssText='width:64px;height:64px;text-align:center;font-size:1.4rem;border-radius:8px;border:1px solid #232a3d;background:#161b29;color:#00f0c8;font-family:Orbitron,sans-serif;';
      if(fixed[r][c]){ inp.value=puzzle[r][c]; inp.disabled=true; inp.style.color='#9aa4bd'; inp.style.background='#0d1119'; }
      else {
        inp.value = puzzle[r][c]||'';
        inp.addEventListener('input', ()=>{
          const v = inp.value.replace(/[^1-4]/g,'');
          inp.value=v;
          puzzle[r][c] = v? +v : 0;
        });
      }
      gridEl.appendChild(inp);
    }
  }
  function check(){
    const ok = JSON.stringify(puzzle)===JSON.stringify(solution);
    view.querySelector('#sdStatus').textContent = ok? 'درسته! بردی 🎉' : 'هنوز اشتباهه، دوباره امتحان کن';
  }
  view.querySelector('#sdCheck').onclick=check;
  view.querySelector('#sdRestart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 23. TYPING TEST ============ */
builders.typing = function(view){
  view.innerHTML = gameTopbar('تست تایپ','⌨️') + `
    <div class="game-stage">
      <div class="hud"><span>WPM: <b id="tpWpm">0</b></span><span>خطا: <b id="tpErr">0</b></span></div>
      <div class="overlay-msg" id="tpTarget" style="font-family:'JetBrains Mono',monospace;font-size:1.1rem;line-height:2;max-width:520px;color:#9aa4bd;"></div>
      <textarea id="tpInput" rows="3" style="width:100%;max-width:520px;padding:12px;border-radius:8px;border:1px solid #232a3d;background:#0d1119;color:#eef1f8;font-family:'JetBrains Mono',monospace;font-size:1rem;" placeholder="اینجا شروع کن به تایپ..."></textarea>
      <button class="mini-btn" id="tpRestart">شروع دوباره</button>
    </div>`;
  const texts = [
    'برنامه نویسی هنر حل کردن مسئله با منطق و خلاقیت است',
    'هر روز یک قدم کوچک بردار تا به هدف بزرگ برسی',
    'موفقیت نتیجه تلاش مداوم و یادگیری از شکست هاست',
  ];
  let target, startTime, errors;
  function reset(){
    target = texts[Math.floor(Math.random()*texts.length)];
    errors=0; startTime=null;
    view.querySelector('#tpTarget').textContent=target;
    view.querySelector('#tpInput').value='';
    view.querySelector('#tpInput').disabled=false;
    view.querySelector('#tpWpm').textContent=0;
    view.querySelector('#tpErr').textContent=0;
  }
  function onInput(){
    const val = view.querySelector('#tpInput').value;
    if(!startTime) startTime=Date.now();
    errors=0;
    for(let i=0;i<val.length;i++) if(val[i]!==target[i]) errors++;
    view.querySelector('#tpErr').textContent=errors;
    if(val===target){
      const minutes = (Date.now()-startTime)/60000;
      const wpm = Math.round((target.split(' ').length)/Math.max(minutes,0.01));
      view.querySelector('#tpWpm').textContent=wpm;
      view.querySelector('#tpInput').disabled=true;
    }
  }
  view.querySelector('#tpInput').addEventListener('input', onInput);
  view.querySelector('#tpRestart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 24. CUBE JUMP ============ */
builders.jump = function(view){
  view.innerHTML = gameTopbar('پرش مکعب','🟦') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="jpScore">0</b></span><span>بهترین: <b id="jpBest">0</b></span></div>
      <canvas id="jpCanvas" width="420" height="200"></canvas>
      <div class="controls-hint">Space یا کلیک برای پریدن، از موانع بالا و پایین فرار کن.</div>
      <button class="mini-btn" id="jpRestart">شروع دوباره</button>
    </div>`;
  const canvas=view.querySelector('#jpCanvas'); const ctx=canvas.getContext('2d');
  let cube, obstacles, score, best=+(localStorage.getItem('jpBest')||0), running, animId, frame, speed;
  view.querySelector('#jpBest').textContent=best;
  function reset(){
    cube={y:100,vy:0}; obstacles=[]; score=0; frame=0; speed=4; running=true;
    view.querySelector('#jpScore').textContent=0;
    if(animId) cancelAnimationFrame(animId);
    loop();
  }
  function jump(){ if(running){ cube.vy=-7; } else reset(); }
  function loop(){
    if(!running) return;
    frame++;
    ctx.fillStyle='#04060a'; ctx.fillRect(0,0,canvas.width,canvas.height);
    cube.vy+=0.4; cube.y+=cube.vy;
    cube.y=Math.max(10,Math.min(190,cube.y));
    ctx.fillStyle='#00f0c8'; ctx.fillRect(50,cube.y-10,20,20);
    if(frame%70===0) obstacles.push({x:420, gapY:40+Math.random()*100, gapH:70});
    obstacles.forEach(o=>o.x-=speed);
    obstacles=obstacles.filter(o=>o.x>-20);
    ctx.fillStyle='#ff3d81';
    obstacles.forEach(o=>{
      ctx.fillRect(o.x,0,16,o.gapY);
      ctx.fillRect(o.x,o.gapY+o.gapH,16,200-o.gapY-o.gapH);
      if(!o.passed && o.x+16<50){ o.passed=true; score++; view.querySelector('#jpScore').textContent=score; speed=4+score/20; }
      if(60>o.x && 50<o.x+16 && (cube.y-10<o.gapY || cube.y+10>o.gapY+o.gapH)) gameOver();
    });
    if(running) animId=requestAnimationFrame(loop);
  }
  function gameOver(){
    running=false;
    if(score>best){ best=score; localStorage.setItem('jpBest',best); view.querySelector('#jpBest').textContent=best; }
    ctx.fillStyle='rgba(0,0,0,.6)'; ctx.fillRect(0,0,canvas.width,canvas.height);
    ctx.fillStyle='#00f0c8'; ctx.font='bold 18px Orbitron, sans-serif'; ctx.textAlign='center';
    ctx.fillText('باختی! کلیک کن برای شروع دوباره', 210, 100);
  }
  function keyHandler(e){ if(e.code==='Space'){ e.preventDefault(); jump(); } }
  canvas.addEventListener('click', jump);
  document.addEventListener('keydown', keyHandler);
  view.querySelector('#jpRestart').onclick=reset;
  reset();
  currentCleanup=()=>{ running=false; cancelAnimationFrame(animId); document.removeEventListener('keydown', keyHandler); };
  view._cleanup=currentCleanup;
};

/* ============ 25. MATCH 3 ============ */
builders.match3 = function(view){
  view.innerHTML = gameTopbar('سه‌تایی','🍬') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="m3Score">0</b></span></div>
      <div class="board-grid" id="m3Grid" style="grid-template-columns:repeat(6,52px);gap:4px;"></div>
      <div class="controls-hint">دو خانه مجاور رو به ترتیب کلیک کن تا جاشون عوض بشه</div>
      <button class="mini-btn" id="m3Restart">شروع دوباره</button>
    </div>`;
  const size=6; const icons=['🍎','🍋','🍇','🍓','🍒'];
  let grid, score, selected;
  function reset(){
    grid = Array.from({length:size},()=>Array.from({length:size},()=>icons[Math.floor(Math.random()*icons.length)]));
    score=0; selected=null;
    view.querySelector('#m3Score').textContent=0;
    resolveMatches(false);
    render();
  }
  function render(){
    const gridEl=view.querySelector('#m3Grid');
    gridEl.innerHTML='';
    for(let r=0;r<size;r++)for(let c=0;c<size;c++){
      const d=document.createElement('div');
      d.className='tile';
      d.style.width='52px'; d.style.height='52px'; d.style.fontSize='1.6rem';
      d.style.background = selected&&selected[0]===r&&selected[1]===c? '#232a3d':'#161b29';
      d.style.border='1px solid #232a3d';
      d.textContent=grid[r][c];
      d.onclick=()=>handleClick(r,c);
      gridEl.appendChild(d);
    }
  }
  function handleClick(r,c){
    if(!selected){ selected=[r,c]; render(); return; }
    const [sr,sc]=selected;
    const adjacent = Math.abs(sr-r)+Math.abs(sc-c)===1;
    if(adjacent){
      [grid[sr][sc], grid[r][c]] = [grid[r][c], grid[sr][sc]];
      selected=null;
      if(!resolveMatches(true)){
        [grid[sr][sc], grid[r][c]] = [grid[r][c], grid[sr][sc]];
      }
      render();
    } else { selected=[r,c]; render(); }
  }
  function findMatches(){
    const toClear=new Set();
    for(let r=0;r<size;r++)for(let c=0;c<size-2;c++){
      if(grid[r][c] && grid[r][c]===grid[r][c+1] && grid[r][c]===grid[r][c+2]){
        toClear.add(r+','+c); toClear.add(r+','+(c+1)); toClear.add(r+','+(c+2));
      }
    }
    for(let c=0;c<size;c++)for(let r=0;r<size-2;r++){
      if(grid[r][c] && grid[r][c]===grid[r+1][c] && grid[r][c]===grid[r+2][c]){
        toClear.add(r+','+c); toClear.add((r+1)+','+c); toClear.add((r+2)+','+c);
      }
    }
    return toClear;
  }
  function resolveMatches(countScore){
    let any=false;
    let matches = findMatches();
    while(matches.size){
      any=true;
      matches.forEach(key=>{
        const [r,c]=key.split(',').map(Number);
        grid[r][c]=null;
      });
      if(countScore){ score+=matches.size*10; view.querySelector('#m3Score').textContent=score; }
      for(let c=0;c<size;c++){
        let col=[];
        for(let r=0;r<size;r++) if(grid[r][c]) col.push(grid[r][c]);
        while(col.length<size) col.unshift(icons[Math.floor(Math.random()*icons.length)]);
        for(let r=0;r<size;r++) grid[r][c]=col[r];
      }
      matches = findMatches();
    }
    return any;
  }
  view.querySelector('#m3Restart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 26. TOWER STACK ============ */
builders.towerstack = function(view){
  view.innerHTML = gameTopbar('برج‌سازی','🏗️') + `
    <div class="game-stage">
      <div class="hud"><span>ارتفاع: <b id="tsScore">0</b></span></div>
      <canvas id="tsCanvas" width="300" height="420"></canvas>
      <div class="controls-hint">کلیک یا Space برای گذاشتن بلوک در لحظه درست.</div>
      <button class="mini-btn" id="tsRestart">شروع دوباره</button>
    </div>`;
  const canvas=view.querySelector('#tsCanvas'); const ctx=canvas.getContext('2d');
  let stack, moving, score, running, animId, dir;
  const colors=['#00f0c8','#ffd23f','#ff3d81','#7d5fff','#3f7dff'];
  function reset(){
    stack=[{x:100,w:100,y:400}];
    moving={x:0,w:100,y:370,dir:1};
    score=0; running=true; dir=1;
    view.querySelector('#tsScore').textContent=0;
    if(animId) cancelAnimationFrame(animId);
    loop();
  }
  function loop(){
    if(!running) return;
    ctx.fillStyle='#04060a'; ctx.fillRect(0,0,canvas.width,canvas.height);
    moving.x += 3*moving.dir;
    if(moving.x<=0 || moving.x+moving.w>=300) moving.dir*=-1;
    stack.forEach((s,i)=> { ctx.fillStyle=colors[i%colors.length]; ctx.fillRect(s.x,s.y,s.w,20); });
    ctx.fillStyle=colors[stack.length%colors.length];
    ctx.fillRect(moving.x, moving.y, moving.w, 20);
    animId=requestAnimationFrame(loop);
  }
  function place(){
    if(!running) return;
    const top = stack[stack.length-1];
    const overlapStart = Math.max(top.x, moving.x);
    const overlapEnd = Math.min(top.x+top.w, moving.x+moving.w);
    const overlap = overlapEnd-overlapStart;
    if(overlap<=6){ gameOver(); return; }
    const newBlock = {x:overlapStart, w:overlap, y:top.y-20};
    stack.push(newBlock);
    score++; view.querySelector('#tsScore').textContent=score;
    moving = {x:0, w:overlap, y:newBlock.y-20, dir: Math.random()<0.5?1:-1};
    if(newBlock.y<60){
      stack.forEach(s=>s.y+=20);
      moving.y+=20;
    }
  }
  function gameOver(){
    running=false; cancelAnimationFrame(animId);
    ctx.fillStyle='rgba(0,0,0,.6)'; ctx.fillRect(0,0,300,420);
    ctx.fillStyle='#00f0c8'; ctx.font='bold 18px Orbitron, sans-serif'; ctx.textAlign='center';
    ctx.fillText(`بازی تمام شد! ارتفاع: ${score}`, 150, 210);
  }
  function keyHandler(e){ if(e.code==='Space'){ e.preventDefault(); place(); } }
  canvas.addEventListener('click', ()=> running? place() : reset());
  document.addEventListener('keydown', keyHandler);
  view.querySelector('#tsRestart').onclick=reset;
  reset();
  currentCleanup=()=>{ running=false; cancelAnimationFrame(animId); document.removeEventListener('keydown', keyHandler); };
  view._cleanup=currentCleanup;
};

/* ============ 27. MAZE ============ */
builders.maze = function(view){
  view.innerHTML = gameTopbar('هزارتو','🌀') + `
    <div class="game-stage">
      <div class="hud" id="mzStatus">با کلیدهای جهت‌دار به خروجی برس</div>
      <canvas id="mzCanvas" width="330" height="330"></canvas>
      <button class="mini-btn" id="mzRestart">هزارتوی جدید</button>
    </div>`;
  const canvas=view.querySelector('#mzCanvas'); const ctx=canvas.getContext('2d');
  const size=11, cell=30;
  let grid, player, exit, won;
  function genMaze(){
    const g = Array.from({length:size},()=>Array(size).fill(1));
    function carve(x,y){
      g[y][x]=0;
      const dirs=[[0,-2],[0,2],[-2,0],[2,0]].sort(()=>Math.random()-0.5);
      for(const [dx,dy] of dirs){
        const nx=x+dx, ny=y+dy;
        if(nx>0&&nx<size-1&&ny>0&&ny<size-1&&g[ny][nx]===1){
          g[y+dy/2][x+dx/2]=0;
          carve(nx,ny);
        }
      }
    }
    carve(1,1);
    return g;
  }
  function reset(){
    grid = genMaze();
    player={x:1,y:1}; exit={x:size-2,y:size-2}; grid[exit.y][exit.x]=0; won=false;
    view.querySelector('#mzStatus').textContent='با کلیدهای جهت‌دار به خروجی برس';
    render();
  }
  function render(){
    ctx.fillStyle='#04060a'; ctx.fillRect(0,0,330,330);
    for(let y=0;y<size;y++)for(let x=0;x<size;x++){
      if(grid[y][x]===1){ ctx.fillStyle='#232a3d'; ctx.fillRect(x*cell,y*cell,cell,cell); }
    }
    ctx.fillStyle='#ffd23f'; ctx.fillRect(exit.x*cell+4,exit.y*cell+4,cell-8,cell-8);
    ctx.fillStyle='#00f0c8'; ctx.fillRect(player.x*cell+4,player.y*cell+4,cell-8,cell-8);
  }
  function keyHandler(e){
    if(won) return;
    let {x,y}=player;
    if(e.key==='ArrowUp') y--; else if(e.key==='ArrowDown') y++;
    else if(e.key==='ArrowLeft') x--; else if(e.key==='ArrowRight') x++;
    else return;
    e.preventDefault();
    if(x>=0&&x<size&&y>=0&&y<size&&grid[y][x]===0){
      player={x,y};
      if(x===exit.x&&y===exit.y){ won=true; view.querySelector('#mzStatus').textContent='بردی! 🎉 هزارتوی جدید بساز'; }
      render();
    }
  }
  document.addEventListener('keydown', keyHandler);
  view.querySelector('#mzRestart').onclick=reset;
  reset();
  currentCleanup=()=>document.removeEventListener('keydown', keyHandler);
  view._cleanup=currentCleanup;
};

/* ============ 28. SLIDING PUZZLE ============ */
builders.slidepuzzle = function(view){
  view.innerHTML = gameTopbar('پازل کشویی','🧩') + `
    <div class="game-stage">
      <div class="hud"><span>حرکت‌ها: <b id="spMoves">0</b></span></div>
      <div class="board-grid" id="spGrid" style="grid-template-columns:repeat(4,72px);gap:5px;"></div>
      <button class="mini-btn" id="spRestart">هم‌زدن دوباره</button>
    </div>`;
  const size=4;
  let tiles, moves;
  function reset(){
    tiles = Array.from({length:size*size-1},(_,i)=>i+1); tiles.push(0);
    for(let i=0;i<200;i++){
      const blank = tiles.indexOf(0);
      const neighbors = getNeighbors(blank);
      const swap = neighbors[Math.floor(Math.random()*neighbors.length)];
      [tiles[blank], tiles[swap]] = [tiles[swap], tiles[blank]];
    }
    moves=0;
    view.querySelector('#spMoves').textContent=0;
    render();
  }
  function getNeighbors(i){
    const r=Math.floor(i/size), c=i%size;
    const res=[];
    if(r>0) res.push(i-size); if(r<size-1) res.push(i+size);
    if(c>0) res.push(i-1); if(c<size-1) res.push(i+1);
    return res;
  }
  function render(){
    const gridEl=view.querySelector('#spGrid');
    gridEl.innerHTML='';
    tiles.forEach((v,i)=>{
      const d=document.createElement('div');
      d.className='tile';
      d.style.width='72px'; d.style.height='72px'; d.style.fontSize='1.3rem';
      d.style.background = v===0? 'transparent':'#161b29';
      d.style.border = v===0? 'none':'1px solid #00f0c8';
      d.style.color='#00f0c8';
      d.textContent = v||'';
      d.onclick=()=>{
        const blank = tiles.indexOf(0);
        if(getNeighbors(i).includes(blank)){
          [tiles[i],tiles[blank]]=[tiles[blank],tiles[i]];
          moves++; view.querySelector('#spMoves').textContent=moves;
          render();
          if(tiles.slice(0,-1).every((v,idx)=>v===idx+1)) setTimeout(()=>alert('بردی! 🎉 حرکت‌ها: '+moves),100);
        }
      };
      gridEl.appendChild(d);
    });
  }
  view.querySelector('#spRestart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 29. CATCH FRUIT ============ */
builders.catchgame = function(view){
  view.innerHTML = gameTopbar('گرفتن میوه','🍎') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="ctScore">0</b></span><span>جان: <b id="ctLives">3</b></span></div>
      <canvas id="ctCanvas" width="360" height="360"></canvas>
      <div class="controls-hint">با موس یا کلیدهای چپ/راست سبد رو حرکت بده.</div>
      <button class="mini-btn" id="ctRestart">شروع دوباره</button>
    </div>`;
  const canvas=view.querySelector('#ctCanvas'); const ctx=canvas.getContext('2d');
  let basketX, items, score, lives, running, animId, frame;
  const emojis=['🍎','🍋','🍇','🍓','🍒'];
  function reset(){
    basketX=150; items=[]; score=0; lives=3; frame=0; running=true;
    view.querySelector('#ctScore').textContent=0;
    view.querySelector('#ctLives').textContent=3;
    if(animId) cancelAnimationFrame(animId);
    loop();
  }
  function loop(){
    if(!running) return;
    frame++;
    ctx.fillStyle='#04060a'; ctx.fillRect(0,0,360,360);
    if(frame%45===0) items.push({x:Math.random()*330+15, y:-10, e:emojis[Math.floor(Math.random()*emojis.length)], vy:2+Math.random()*1.5});
    ctx.font='28px sans-serif';
    items.forEach(it=>{ it.y+=it.vy; ctx.fillText(it.e, it.x, it.y); });
    items = items.filter(it=>{
      if(it.y>330 && it.y<360 && it.x>basketX-5 && it.x<basketX+65){ score++; view.querySelector('#ctScore').textContent=score; return false; }
      if(it.y>360){ lives--; view.querySelector('#ctLives').textContent=lives; if(lives<=0) gameOver(); return false; }
      return true;
    });
    ctx.fillStyle='#00f0c8'; ctx.fillRect(basketX,340,60,14);
    if(running) animId=requestAnimationFrame(loop);
  }
  function gameOver(){
    running=false;
    ctx.fillStyle='rgba(0,0,0,.6)'; ctx.fillRect(0,0,360,360);
    ctx.fillStyle='#00f0c8'; ctx.font='bold 18px Orbitron, sans-serif'; ctx.textAlign='center';
    ctx.fillText(`باختی! امتیاز: ${score}`, 180, 180);
  }
  function mouseHandler(e){
    const rect=canvas.getBoundingClientRect();
    basketX = Math.max(0, Math.min(300, (e.clientX-rect.left)*(360/rect.width) - 30));
  }
  function keyHandler(e){
    if(e.key==='ArrowLeft') basketX=Math.max(0,basketX-20);
    if(e.key==='ArrowRight') basketX=Math.min(300,basketX+20);
  }
  canvas.addEventListener('mousemove', mouseHandler);
  document.addEventListener('keydown', keyHandler);
  view.querySelector('#ctRestart').onclick=reset;
  reset();
  currentCleanup=()=>{ running=false; cancelAnimationFrame(animId); document.removeEventListener('keydown', keyHandler); };
  view._cleanup=currentCleanup;
};

/* ============ 30. GUESS THE NUMBER ============ */
builders.guessnumber = function(view){
  view.innerHTML = gameTopbar('حدس عدد','🎯') + `
    <div class="game-stage">
      <div class="hud"><span>تلاش‌ها: <b id="gnTries">0</b></span></div>
      <div class="overlay-msg" id="gnMsg">عددی بین ۱ تا ۱۰۰ رو حدس بزن</div>
      <input id="gnInput" type="number" min="1" max="100" style="width:160px;padding:12px;border-radius:8px;border:1px solid #232a3d;background:#0d1119;color:#eef1f8;font-size:1.2rem;text-align:center;">
      <button class="mini-btn" id="gnSubmit">حدس بزن</button>
      <button class="mini-btn" id="gnRestart">شروع دوباره</button>
    </div>`;
  let target, tries;
  function reset(){
    target = Math.floor(Math.random()*100)+1; tries=0;
    view.querySelector('#gnMsg').textContent='عددی بین ۱ تا ۱۰۰ رو حدس بزن';
    view.querySelector('#gnTries').textContent=0;
    view.querySelector('#gnInput').disabled=false;
    view.querySelector('#gnInput').value='';
  }
  function submit(){
    const val = +view.querySelector('#gnInput').value;
    if(!val) return;
    tries++; view.querySelector('#gnTries').textContent=tries;
    if(val===target){ view.querySelector('#gnMsg').textContent=`درسته! 🎉 در ${tries} تلاش`; view.querySelector('#gnInput').disabled=true; }
    else if(val<target) view.querySelector('#gnMsg').textContent='بزرگ‌تر بگو ⬆️';
    else view.querySelector('#gnMsg').textContent='کوچیک‌تر بگو ⬇️';
    view.querySelector('#gnInput').value='';
    view.querySelector('#gnInput').focus();
  }
  view.querySelector('#gnSubmit').onclick=submit;
  view.querySelector('#gnInput').addEventListener('keydown', e=>{ if(e.key==='Enter') submit(); });
  view.querySelector('#gnRestart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 31. BLACKJACK ============ */
builders.blackjack = function(view){
  view.innerHTML = gameTopbar('بلک‌جک','🂡') + `
    <div class="game-stage">
      <div class="hud"><span>تو: <b id="bjYou">0</b></span><span>خانه: <b id="bjHouse">?</b></span></div>
      <div id="bjYourCards" style="font-size:1.8rem;"></div>
      <div id="bjHouseCards" style="font-size:1.8rem;"></div>
      <div class="overlay-msg" id="bjMsg"></div>
      <div style="display:flex;gap:12px;">
        <button class="mini-btn" id="bjHit">🂠 کارت بگیر</button>
        <button class="mini-btn" id="bjStand">✋ بایست</button>
      </div>
      <button class="mini-btn" id="bjRestart">دست جدید</button>
    </div>`;
  const suits=['♠','♥','♦','♣'];
  let deck, yourHand, houseHand, done;
  function newDeck(){
    const d=[];
    for(const s of suits) for(let v=1;v<=13;v++) d.push({v,s});
    return d.sort(()=>Math.random()-0.5);
  }
  function val(card){ return card.v>10?10:card.v===1?11:card.v; }
  function handValue(hand){
    let sum=hand.reduce((a,c)=>a+val(c),0);
    let aces=hand.filter(c=>c.v===1).length;
    while(sum>21 && aces>0){ sum-=10; aces--; }
    return sum;
  }
  function cardStr(c){ const names={1:'A',11:'J',12:'Q',13:'K'}; return (names[c.v]||c.v)+c.s; }
  function reset(){
    deck=newDeck(); yourHand=[deck.pop(),deck.pop()]; houseHand=[deck.pop(),deck.pop()]; done=false;
    view.querySelector('#bjMsg').textContent='';
    view.querySelector('#bjHit').disabled=false; view.querySelector('#bjStand').disabled=false;
    render();
  }
  function render(hideHouse=true){
    view.querySelector('#bjYourCards').textContent = yourHand.map(cardStr).join(' ');
    view.querySelector('#bjYou').textContent = handValue(yourHand);
    if(hideHouse && !done){
      view.querySelector('#bjHouseCards').textContent = cardStr(houseHand[0])+' 🂠';
      view.querySelector('#bjHouse').textContent='?';
    } else {
      view.querySelector('#bjHouseCards').textContent = houseHand.map(cardStr).join(' ');
      view.querySelector('#bjHouse').textContent = handValue(houseHand);
    }
  }
  function hit(){
    if(done) return;
    yourHand.push(deck.pop());
    if(handValue(yourHand)>21) endGame('باختی! بیش از ۲۱ شدی 💥');
    render();
  }
  function stand(){
    if(done) return;
    while(handValue(houseHand)<17) houseHand.push(deck.pop());
    const y=handValue(yourHand), h=handValue(houseHand);
    if(h>21 || y>h) endGame('بردی! 🎉');
    else if(y===h) endGame('مساوی شد 🤝');
    else endGame('باختی 😅');
  }
  function endGame(msg){
    done=true;
    view.querySelector('#bjMsg').textContent=msg;
    view.querySelector('#bjHit').disabled=true; view.querySelector('#bjStand').disabled=true;
    render(false);
  }
  view.querySelector('#bjHit').onclick=hit;
  view.querySelector('#bjStand').onclick=stand;
  view.querySelector('#bjRestart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 32. HANGMAN ============ */
builders.hangman = function(view){
  view.innerHTML = gameTopbar('دار مریزی','🎪') + `
    <div class="game-stage">
      <div class="hud"><span>جون: <b id="hmLives">6</b></span></div>
      <div id="hmDrawing" style="font-size:3rem;"></div>
      <div class="overlay-msg" id="hmWord" style="letter-spacing:8px;"></div>
      <div id="hmLetters" style="display:flex;flex-wrap:wrap;gap:6px;max-width:480px;justify-content:center;"></div>
      <button class="mini-btn" id="hmRestart">شروع دوباره</button>
    </div>`;
  const stages=['🙂','😐','😟','😧','😰','😵','💀'];
  const words=['موز','خورشید','باران','کوهستان','دوچرخه','گیتار'];
  let target, guessed, lives;
  function reset(){
    target = words[Math.floor(Math.random()*words.length)];
    guessed=[]; lives=6;
    view.querySelector('#hmLives').textContent=lives;
    view.querySelector('#hmDrawing').textContent=stages[0];
    renderWord(); renderLetters();
  }
  function renderWord(){
    view.querySelector('#hmWord').textContent = target.split('').map(ch=>guessed.includes(ch)?ch:'_').join(' ');
  }
  function renderLetters(){
    const letters='اآبپتثجچحخدذرزژسشصضطظعغفقکگلمنوهی';
    const box = view.querySelector('#hmLetters');
    box.innerHTML='';
    letters.split('').forEach(ch=>{
      const btn=document.createElement('button');
      btn.className='mini-btn'; btn.textContent=ch; btn.style.width='38px'; btn.style.padding='7px 0';
      if(guessed.includes(ch)){ btn.disabled=true; btn.style.opacity=.35; }
      btn.onclick=()=>{
        guessed.push(ch);
        if(!target.includes(ch)){
          lives--; view.querySelector('#hmLives').textContent=lives;
          view.querySelector('#hmDrawing').textContent = stages[6-lives] || stages[6];
          if(lives<=0){ view.querySelector('#hmWord').textContent='باختی! کلمه: '+target; box.innerHTML=''; return; }
        }
        renderWord(); renderLetters();
        if(target.split('').every(c=>guessed.includes(c))){
          view.querySelector('#hmWord').textContent = target+' — بردی! 🎉';
          box.innerHTML='';
        }
      };
      box.appendChild(btn);
    });
  }
  view.querySelector('#hmRestart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 33. SPACE SHOOTER ============ */
builders.spaceshooter = function(view){
  view.innerHTML = gameTopbar('جنگ فضایی','🚀') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="ssScore">0</b></span><span>جان: <b id="ssLives">3</b></span></div>
      <canvas id="ssCanvas" width="360" height="420"></canvas>
      <div class="controls-hint">چپ/راست: حرکت — Space: شلیک</div>
      <button class="mini-btn" id="ssRestart">شروع دوباره</button>
    </div>`;
  const canvas=view.querySelector('#ssCanvas'); const ctx=canvas.getContext('2d');
  let shipX, bullets, enemies, score, lives, running, animId, frame, keys;
  function reset(){
    shipX=170; bullets=[]; enemies=[]; score=0; lives=3; frame=0; running=true; keys={};
    view.querySelector('#ssScore').textContent=0;
    view.querySelector('#ssLives').textContent=3;
    if(animId) cancelAnimationFrame(animId);
    loop();
  }
  function loop(){
    if(!running) return;
    frame++;
    ctx.fillStyle='#04060a'; ctx.fillRect(0,0,360,420);
    if(keys['ArrowLeft']) shipX=Math.max(0,shipX-4);
    if(keys['ArrowRight']) shipX=Math.min(340,shipX+4);
    ctx.fillStyle='#00f0c8'; ctx.fillRect(shipX,390,20,20);
    bullets.forEach(b=>b.y-=6); bullets=bullets.filter(b=>b.y>-10);
    ctx.fillStyle='#ffd23f'; bullets.forEach(b=>ctx.fillRect(b.x-2,b.y-6,4,10));
    if(frame%45===0) enemies.push({x:Math.random()*330, y:-20});
    enemies.forEach(en=>en.y+=1.6);
    ctx.fillStyle='#ff3d81'; enemies.forEach(en=>ctx.fillRect(en.x,en.y,22,18));
    for(let i=enemies.length-1;i>=0;i--){
      for(let j=bullets.length-1;j>=0;j--){
        if(bullets[j].x>enemies[i].x && bullets[j].x<enemies[i].x+22 && bullets[j].y>enemies[i].y && bullets[j].y<enemies[i].y+18){
          enemies.splice(i,1); bullets.splice(j,1); score+=10; view.querySelector('#ssScore').textContent=score;
          break;
        }
      }
    }
    enemies = enemies.filter(en=>{
      if(en.y>420) return false;
      if(en.y>385 && en.x<shipX+20 && en.x+22>shipX){ lives--; view.querySelector('#ssLives').textContent=lives; if(lives<=0) gameOver(); return false; }
      return true;
    });
    if(running) animId=requestAnimationFrame(loop);
  }
  function shoot(){ bullets.push({x:shipX+10, y:388}); }
  function gameOver(){
    running=false;
    ctx.fillStyle='rgba(0,0,0,.6)'; ctx.fillRect(0,0,360,420);
    ctx.fillStyle='#00f0c8'; ctx.font='bold 18px Orbitron, sans-serif'; ctx.textAlign='center';
    ctx.fillText(`باختی! امتیاز: ${score}`, 180, 210);
  }
  function keyDown(e){ keys[e.key]=true; if(e.code==='Space'){ e.preventDefault(); if(running) shoot(); } }
  function keyUp(e){ keys[e.key]=false; }
  document.addEventListener('keydown', keyDown);
  document.addEventListener('keyup', keyUp);
  view.querySelector('#ssRestart').onclick=reset;
  reset();
  currentCleanup=()=>{ running=false; cancelAnimationFrame(animId); document.removeEventListener('keydown', keyDown); document.removeEventListener('keyup', keyUp); };
  view._cleanup=currentCleanup;
};

/* ============ 34. BUBBLE SHOOT ============ */
builders.bubbleshoot = function(view){
  view.innerHTML = gameTopbar('حباب‌ترکون','🫧') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="bsScore">0</b></span></div>
      <canvas id="bsCanvas" width="360" height="420"></canvas>
      <div class="controls-hint">روی حباب‌ها کلیک کن تا بترکن، قبل از رسیدن به پایین.</div>
      <button class="mini-btn" id="bsRestart">شروع دوباره</button>
    </div>`;
  const canvas=view.querySelector('#bsCanvas'); const ctx=canvas.getContext('2d');
  let bubbles, score, running, animId, frame;
  const colors=['#00f0c8','#ff3d81','#ffd23f','#7d5fff'];
  function reset(){
    bubbles=[]; score=0; frame=0; running=true;
    view.querySelector('#bsScore').textContent=0;
    if(animId) cancelAnimationFrame(animId);
    loop();
  }
  function loop(){
    if(!running) return;
    frame++;
    ctx.fillStyle='#04060a'; ctx.fillRect(0,0,360,420);
    if(frame%50===0) bubbles.push({x:20+Math.random()*320, y:-15, r:16, c:colors[Math.floor(Math.random()*colors.length)], vy:1+Math.random()});
    bubbles.forEach(b=>b.y+=b.vy);
    bubbles.forEach(b=>{ ctx.beginPath(); ctx.arc(b.x,b.y,b.r,0,Math.PI*2); ctx.fillStyle=b.c; ctx.globalAlpha=.85; ctx.fill(); ctx.globalAlpha=1; });
    const before=bubbles.length;
    bubbles = bubbles.filter(b=>b.y<430);
    if(bubbles.length<before && running){
      // a bubble escaped, minor penalty visual only
    }
    if(running) animId=requestAnimationFrame(loop);
  }
  function clickHandler(e){
    const rect=canvas.getBoundingClientRect();
    const x=(e.clientX-rect.left)*(360/rect.width), y=(e.clientY-rect.top)*(420/rect.height);
    for(let i=bubbles.length-1;i>=0;i--){
      const b=bubbles[i];
      if(Math.hypot(b.x-x,b.y-y)<b.r){ bubbles.splice(i,1); score++; view.querySelector('#bsScore').textContent=score; break; }
    }
  }
  canvas.addEventListener('click', clickHandler);
  view.querySelector('#bsRestart').onclick=reset;
  reset();
  currentCleanup=()=>{ running=false; cancelAnimationFrame(animId); };
  view._cleanup=currentCleanup;
};

/* ============ 35. PIXEL PAINT ============ */
builders.pixelpaint = function(view){
  view.innerHTML = gameTopbar('نقاشی پیکسلی','🖌️') + `
    <div class="game-stage">
      <div class="hud">روی خانه‌ها کلیک یا بکش تا رنگ بزنی</div>
      <div id="ppPalette" style="display:flex;gap:8px;"></div>
      <div class="board-grid" id="ppGrid" style="grid-template-columns:repeat(16,20px);gap:1px;"></div>
      <button class="mini-btn" id="ppClear">پاک کردن</button>
    </div>`;
  const size=16;
  const palette=['#00f0c8','#ff3d81','#ffd23f','#7d5fff','#eef1f8','#04060a'];
  let currentColor=palette[0];
  const cellsColor=Array.from({length:size*size},()=>'#161b29');
  function renderPalette(){
    const box=view.querySelector('#ppPalette');
    box.innerHTML='';
    palette.forEach(c=>{
      const sw=document.createElement('div');
      sw.style.cssText=`width:28px;height:28px;border-radius:6px;background:${c};cursor:pointer;border:2px solid ${c===currentColor?'#fff':'transparent'};`;
      sw.onclick=()=>{ currentColor=c; renderPalette(); };
      box.appendChild(sw);
    });
  }
  function renderGrid(){
    const gridEl=view.querySelector('#ppGrid');
    gridEl.innerHTML='';
    let painting=false;
    for(let i=0;i<size*size;i++){
      const d=document.createElement('div');
      d.style.cssText=`width:20px;height:20px;background:${cellsColor[i]};cursor:pointer;`;
      d.onmousedown=()=>{ painting=true; cellsColor[i]=currentColor; d.style.background=currentColor; };
      d.onmouseenter=()=>{ if(painting){ cellsColor[i]=currentColor; d.style.background=currentColor; } };
      gridEl.appendChild(d);
    }
    document.addEventListener('mouseup', ()=>painting=false);
  }
  view.querySelector('#ppClear').onclick=()=>{ for(let i=0;i<cellsColor.length;i++) cellsColor[i]='#161b29'; renderGrid(); };
  renderPalette(); renderGrid();
  currentCleanup=null;
};

/* ============ 36. QUIZ ============ */
builders.quiz = function(view){
  view.innerHTML = gameTopbar('مسابقه اطلاعات عمومی','❓') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="qzScore">0</b></span><span>سوال: <b id="qzNum">1</b>/8</span></div>
      <div class="overlay-msg" id="qzQ" style="font-size:1.1rem;max-width:500px;"></div>
      <div id="qzOptions" style="display:flex;flex-direction:column;gap:10px;width:100%;max-width:420px;"></div>
      <button class="mini-btn" id="qzRestart" style="display:none;">شروع دوباره</button>
    </div>`;
  const questions=[
    {q:'پایتخت فرانسه کدام است؟', o:['برلین','پاریس','رم','مادرید'], a:1},
    {q:'بزرگ‌ترین اقیانوس جهان کدام است؟', o:['اطلس','هند','آرام','منجمد'], a:2},
    {q:'کدام سیاره به مریخ معروف است؟', o:['زهره','مریخ','مشتری','زحل'], a:1},
    {q:'نماد شیمیایی طلا چیست؟', o:['Ag','Fe','Au','Pb'], a:2},
    {q:'بلندترین کوه جهان کدام است؟', o:['اورست','دماوند','آلپ','کیلیمانجارو'], a:0},
    {q:'موتور جستجوی گوگل در چه سالی تاسیس شد؟', o:['۱۹۹۸','۲۰۰۰','۱۹۹۵','۲۰۰۴'], a:0},
    {q:'کدام گاز برای تنفس انسان ضروری است؟', o:['نیتروژن','هیدروژن','اکسیژن','کربن'], a:2},
    {q:'واحد پول ژاپن چیست؟', o:['وون','ین','یوان','روپیه'], a:1},
  ];
  let idx, score;
  function reset(){
    idx=0; score=0;
    view.querySelector('#qzScore').textContent=0;
    view.querySelector('#qzRestart').style.display='none';
    showQ();
  }
  function showQ(){
    if(idx>=questions.length){
      view.querySelector('#qzQ').textContent=`تمام شد! امتیاز نهایی: ${score}/${questions.length}`;
      view.querySelector('#qzOptions').innerHTML='';
      view.querySelector('#qzRestart').style.display='inline-block';
      return;
    }
    view.querySelector('#qzNum').textContent=idx+1;
    const cur=questions[idx];
    view.querySelector('#qzQ').textContent=cur.q;
    const box=view.querySelector('#qzOptions');
    box.innerHTML='';
    cur.o.forEach((opt,i)=>{
      const btn=document.createElement('button');
      btn.className='mini-btn'; btn.textContent=opt; btn.style.padding='12px';
      btn.onclick=()=>{
        if(i===cur.a){ score++; view.querySelector('#qzScore').textContent=score; btn.style.borderColor='#00f0c8'; }
        else btn.style.borderColor='#ff3d81';
        Array.from(box.children).forEach(b=>b.disabled=true);
        setTimeout(()=>{ idx++; showQ(); }, 600);
      };
      box.appendChild(btn);
    });
  }
  view.querySelector('#qzRestart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 37. STACK COLOR (reaction) ============ */
builders.stackcolor = function(view){
  view.innerHTML = gameTopbar('برج رنگی','🎨') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="scScore">0</b></span></div>
      <div class="overlay-msg">رنگ هدف: <span id="scTarget" style="font-weight:bold;"></span></div>
      <div id="scOptions" style="display:flex;gap:14px;"></div>
      <button class="mini-btn" id="scRestart">شروع دوباره</button>
    </div>`;
  const colorDefs=[{n:'فیروزه‌ای',c:'#00f0c8'},{n:'صورتی',c:'#ff3d81'},{n:'زرد',c:'#ffd23f'},{n:'بنفش',c:'#7d5fff'}];
  let score, targetIdx;
  function reset(){
    score=0; view.querySelector('#scScore').textContent=0;
    newRound();
  }
  function newRound(){
    targetIdx = Math.floor(Math.random()*colorDefs.length);
    view.querySelector('#scTarget').textContent = colorDefs[targetIdx].n;
    view.querySelector('#scTarget').style.color = colorDefs[targetIdx].c;
    const box=view.querySelector('#scOptions');
    box.innerHTML='';
    const shuffled = colorDefs.map((c,i)=>({...c,i})).sort(()=>Math.random()-0.5);
    shuffled.forEach(c=>{
      const sw=document.createElement('div');
      sw.style.cssText=`width:60px;height:60px;border-radius:12px;background:${c.c};cursor:pointer;`;
      sw.onclick=()=>{
        if(c.i===targetIdx){ score++; view.querySelector('#scScore').textContent=score; newRound(); }
        else { sw.style.outline='3px solid #ff3d81'; setTimeout(newRound,400); }
      };
      box.appendChild(sw);
    });
  }
  view.querySelector('#scRestart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 38. CHESS (practice, no check detection) ============ */
builders.chess = function(view){
  view.innerHTML = gameTopbar('شطرنج تمرینی','♟️') + `
    <div class="game-stage">
      <div class="hud" id="chStatus">نوبت سفید</div>
      <div class="board-grid" id="chGrid" style="grid-template-columns:repeat(8,44px);gap:0;"></div>
      <div class="controls-hint">حرکت آزاد بدون بررسی کیش — برای تمرین چیدمان و حرکت مهره‌ها</div>
      <button class="mini-btn" id="chRestart">شروع دوباره</button>
    </div>`;
  const pieces={
    'r':'♜','n':'♞','b':'♝','q':'♛','k':'♚','p':'♟',
    'R':'♖','N':'♘','B':'♗','Q':'♕','K':'♔','P':'♙'
  };
  let board, turn, selected;
  function reset(){
    board=[
      ['r','n','b','q','k','b','n','r'],
      ['p','p','p','p','p','p','p','p'],
      ['','','','','','','',''],
      ['','','','','','','',''],
      ['','','','','','','',''],
      ['','','','','','','',''],
      ['P','P','P','P','P','P','P','P'],
      ['R','N','B','Q','K','B','N','R'],
    ];
    turn='w'; selected=null;
    view.querySelector('#chStatus').textContent='نوبت سفید';
    render();
  }
  function isWhite(p){ return p===p.toUpperCase() && p!==''; }
  function render(){
    const gridEl=view.querySelector('#chGrid');
    gridEl.innerHTML='';
    for(let r=0;r<8;r++)for(let c=0;c<8;c++){
      const d=document.createElement('div');
      const dark=(r+c)%2===1;
      d.style.cssText=`width:44px;height:44px;display:flex;align-items:center;justify-content:center;font-size:1.7rem;cursor:pointer;background:${dark?'#232a3d':'#161b29'};`;
      if(selected&&selected[0]===r&&selected[1]===c) d.style.background='#00f0c855';
      d.textContent = pieces[board[r][c]]||'';
      d.onclick=()=>handleClick(r,c);
      gridEl.appendChild(d);
    }
  }
  function handleClick(r,c){
    const piece=board[r][c];
    if(selected){
      const [sr,sc]=selected;
      if(sr===r&&sc===c){ selected=null; render(); return; }
      board[r][c]=board[sr][sc]; board[sr][sc]='';
      selected=null;
      turn = turn==='w'?'b':'w';
      view.querySelector('#chStatus').textContent = turn==='w'?'نوبت سفید':'نوبت سیاه';
      render();
    } else if(piece && ((turn==='w'&&isWhite(piece)) || (turn==='b'&&!isWhite(piece)))){
      selected=[r,c]; render();
    }
  }
  view.querySelector('#chRestart').onclick=reset;
  reset();
  currentCleanup=null;
};

/* ============ 39. ENDLESS RUNNER ============ */
builders.runner = function(view){
  view.innerHTML = gameTopbar('دونده بی‌پایان','🏃') + `
    <div class="game-stage">
      <div class="hud"><span>امتیاز: <b id="rnScore">0</b></span><span>بهترین: <b id="rnBest">0</b></span></div>
      <canvas id="rnCanvas" width="420" height="200"></canvas>
      <div class="controls-hint">Space یا کلیک برای پرش، پرش دوم برای دبل جامپ.</div>
      <button class="mini-btn" id="rnRestart">شروع دوباره</button>
    </div>`;
  const canvas=view.querySelector('#rnCanvas'); const ctx=canvas.getContext('2d');
  let player, obstacles, score, best=+(localStorage.getItem('rnBest')||0), running, animId, frame, speed, jumpsLeft;
  view.querySelector('#rnBest').textContent=best;
  function reset(){
    player={y:140,vy:0}; obstacles=[]; score=0; speed=5; frame=0; running=true; jumpsLeft=2;
    view.querySelector('#rnScore').textContent=0;
    if(animId) cancelAnimationFrame(animId);
    loop();
  }
  function jump(){
    if(!running){ reset(); return; }
    if(jumpsLeft>0){ player.vy=-8.5; jumpsLeft--; }
  }
  function loop(){
    if(!running) return;
    frame++;
    ctx.fillStyle='#04060a'; ctx.fillRect(0,0,420,200);
    ctx.strokeStyle='#232a3d'; ctx.beginPath(); ctx.moveTo(0,170); ctx.lineTo(420,170); ctx.stroke();
    player.vy+=0.5; player.y+=player.vy;
    if(player.y>140){ player.y=140; player.vy=0; jumpsLeft=2; }
    ctx.fillStyle='#00f0c8'; ctx.fillRect(50,player.y,24,30);
    if(frame%60===0) obstacles.push({x:420, w:16, h:20+Math.random()*30, y: Math.random()<0.5? 150 : 40});
    obstacles.forEach(o=>o.x-=speed);
    obstacles=obstacles.filter(o=>o.x>-20);
    ctx.fillStyle='#ff3d81';
    obstacles.forEach(o=>{
      const oy = o.y===150? 170-o.h : 0;
      ctx.fillRect(o.x,oy,o.w,o.h);
      if(!o.passed && o.x+o.w<50){ o.passed=true; score++; view.querySelector('#rnScore').textContent=score; speed=5+score/30; }
      if(50+24>o.x && 50<o.x+o.w && player.y<oy+o.h && player.y+30>oy) gameOver();
    });
    if(running) animId=requestAnimationFrame(loop);
  }
  function gameOver(){
    running=false;
    if(score>best){ best=score; localStorage.setItem('rnBest',best); view.querySelector('#rnBest').textContent=best; }
    ctx.fillStyle='rgba(0,0,0,.6)'; ctx.fillRect(0,0,420,200);
    ctx.fillStyle='#00f0c8'; ctx.font='bold 18px Orbitron, sans-serif'; ctx.textAlign='center';
    ctx.fillText('باختی! کلیک کن برای شروع دوباره', 210, 100);
  }
  function keyHandler(e){ if(e.code==='Space'){ e.preventDefault(); jump(); } }
  canvas.addEventListener('click', jump);
  document.addEventListener('keydown', keyHandler);
  view.querySelector('#rnRestart').onclick=reset;
  reset();
  currentCleanup=()=>{ running=false; cancelAnimationFrame(animId); document.removeEventListener('keydown', keyHandler); };
  view._cleanup=currentCleanup;
};

/* ============ 40. NUMBER WAR (cards) ============ */
builders.cardmatch = function(view){
  view.innerHTML = gameTopbar('جنگ اعداد','🔢') + `
    <div class="game-stage">
      <div class="hud"><span>تو: <b id="nwYou">0</b></span><span>حریف: <b id="nwCpu">0</b></span><span>دور: <b id="nwRound">0</b>/10</span></div>
      <div style="display:flex;gap:30px;align-items:center;">
        <div style="text-align:center;"><div style="font-size:.8rem;color:#9aa4bd;">کارت تو</div><div id="nwYourCard" style="font-size:2.4rem;">🂠</div></div>
        <div style="font-family:Orbitron,sans-serif;color:#9aa4bd;">VS</div>
        <div style="text-align:center;"><div style="font-size:.8rem;color:#9aa4bd;">کارت حریف</div><div id="nwCpuCard" style="font-size:2.4rem;">🂠</div></div>
      </div>
      <div class="overlay-msg" id="nwMsg">کارت بکش تا شروع بشه</div>
      <button class="mini-btn" id="nwDraw">کارت بکش</button>
      <button class="mini-btn" id="nwRestart">شروع دوباره</button>
    </div>`;
  const suits=['♠','♥','♦','♣'];
  let you, cpu, round;
  function reset(){
    you=0; cpu=0; round=0;
    view.querySelector('#nwYou').textContent=0;
    view.querySelector('#nwCpu').textContent=0;
    view.querySelector('#nwRound').textContent=0;
    view.querySelector('#nwMsg').textContent='کارت بکش تا شروع بشه';
    view.querySelector('#nwYourCard').textContent='🂠';
    view.querySelector('#nwCpuCard').textContent='🂠';
    view.querySelector('#nwDraw').disabled=false;
  }
  function draw(){
    if(round>=10) return;
    round++;
    const yv=Math.floor(Math.random()*13)+1, cv=Math.floor(Math.random()*13)+1;
    const names={1:'A',11:'J',12:'Q',13:'K'};
    view.querySelector('#nwYourCard').textContent=(names[yv]||yv)+suits[Math.floor(Math.random()*4)];
    view.querySelector('#nwCpuCard').textContent=(names[cv]||cv)+suits[Math.floor(Math.random()*4)];
    view.querySelector('#nwRound').textContent=round;
    if(yv>cv){ you++; view.querySelector('#nwMsg').textContent='بردی این دور رو! 🎉'; }
    else if(yv<cv){ cpu++; view.querySelector('#nwMsg').textContent='باختی این دور 😅'; }
    else view.querySelector('#nwMsg').textContent='مساوی شد 🤝';
    view.querySelector('#nwYou').textContent=you;
    view.querySelector('#nwCpu').textContent=cpu;
    if(round>=10){
      view.querySelector('#nwDraw').disabled=true;
      view.querySelector('#nwMsg').textContent = you>cpu? `بازی تمام شد — بردی! نهایی ${you}-${cpu}` : you<cpu? `بازی تمام شد — باختی! نهایی ${you}-${cpu}` : 'بازی تمام شد — مساوی!';
    }
  }
  view.querySelector('#nwDraw').onclick=draw;
  view.querySelector('#nwRestart').onclick=reset;
  reset();
  currentCleanup=null;
};
</script>
</body>
</html>
