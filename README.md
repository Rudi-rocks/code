
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
  <title>Code × Ninja 10 — The Digital Dojo</title>
  <meta name="description" content="Code × Ninja 10 — invite-only cinematic summit for elite engineers. Glassmorphism, parallax, SVG sigil, lo‑fi ambience, secret terminal, schedule, speakers, RSVP and more." />
  <meta name="theme-color" content="#05060a" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&family=Space+Grotesk:wght@400;600;700&display=swap" rel="stylesheet">

  <style>
    /* ==========================
       Design tokens & variables
       ========================== */
    :root{
      --bg-1: 6 8 12; /* base dark */
      --accent-1: 112 76 255; /* violet */
      --accent-2: 0 210 255; /* cyan */
      --glass: rgba(255,255,255,0.04);
      --muted: rgba(255,255,255,0.64);
      --radius: 16px;
      --gap: 28px;
      --container: 1200px;
      --fw-sans: 'Inter', system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
      --fw-display: 'Space Grotesk', var(--fw-sans);
      --ease: cubic-bezier(.2,.9,.25,1);
    }

    /* Reset & global */
    *{box-sizing:border-box}
    html,body{height:100%}
    body{margin:0; min-height:100vh; font-family:var(--fw-sans); color:#fff; background:linear-gradient(180deg,#04050a,#06070b); -webkit-font-smoothing:antialiased}
    a{color:inherit; text-decoration:none}

    /* Background atmospherics */
    .bg-wrap{position:fixed; inset:0; z-index:-4; overflow:hidden}
    .bg-gradient{position:absolute; inset:-20% -40%; background:radial-gradient(800px 400px at 12% 22%, rgba(var(--accent-2),0.08), transparent), radial-gradient(800px 360px at 92% 78%, rgba(var(--accent-1),0.06), transparent); mix-blend-mode:screen}
    .bg-grid{position:absolute; inset:0; background-image:linear-gradient(transparent 0 1px, rgba(255,255,255,0.01) 1px), linear-gradient(90deg, transparent 0 1px, rgba(255,255,255,0.01) 1px); background-size: 160px 160px; opacity:0.03}
    .bg-noise{position:absolute; inset:0; opacity:0.025; background-image:url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="200" height="200"><filter id="t"><feTurbulence baseFrequency="0.9" numOctaves="1" stitchTiles="stitch"/></filter><rect width="100%" height="100%" filter="url(%23t)"/></svg>'); mix-blend-mode:overlay}

    /* layout */
    .container{max-width:var(--container); margin:0 auto; padding:clamp(20px,4vw,64px); display:flex; flex-direction:column; gap:var(--gap)}

    /* Navigation */
    header.nav{display:flex; align-items:center; justify-content:space-between; gap:12px}
    .nav-left{display:flex; gap:12px; align-items:center}
    .logo{display:flex; gap:12px; align-items:center}
    .logo b{font-family:var(--fw-display); font-weight:800; letter-spacing:-0.02em}
    .nav-links{display:flex; gap:12px; align-items:center}
    .nav-links a{padding:8px 10px; border-radius:10px; font-weight:700; color:var(--muted)}
    .nav-cta{display:flex; gap:8px; align-items:center}

    /* Hero Card */
    .card{
      display:flex; gap:28px; align-items:center; padding: clamp(22px,3.6vw,44px); border-radius:calc(var(--radius) + 6px);
      background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); border:1px solid rgba(255,255,255,0.04); backdrop-filter: blur(12px) saturate(130%);
      box-shadow: 0 30px 80px rgba(2,6,23,0.6);
      transition: transform 420ms var(--ease), box-shadow 300ms var(--ease);
    }
    .card:hover{transform:translateY(-10px)}

    .brand{flex:0 0 140px; display:flex; align-items:center; justify-content:center}
    .hero-meta{flex:1}
    .eyebrow{font-weight:700; color:var(--muted); font-size:12px; letter-spacing:0.14em; text-transform:uppercase}
    .title{font-family:var(--fw-display); font-weight:900; font-size:clamp(26px,4.6vw,54px); margin:6px 0 0}
    .lead{color:rgba(255,255,255,0.78); font-size:16px; margin-top:10px; max-width:66ch}

    .meta-actions{display:flex; gap:12px; align-items:center; margin-top:14px}
    .btn{padding:12px 16px; border-radius:12px; font-weight:800; cursor:pointer; border:0}
    .btn-primary{background:linear-gradient(90deg,#704CFF,#00D2FF); color:#fff; box-shadow:0 12px 36px rgba(8,6,20,0.6)}
    .btn-muted{background:transparent; border:1px solid rgba(255,255,255,0.05); color:var(--muted)}

    /* Hero right column */
    .right-col{width:380px; display:flex; flex-direction:column; gap:14px; align-items:center}
    .sigil-wrap{width:100%; display:flex; align-items:center; justify-content:center}

    /* schedule / speakers / CTA */
    .section{padding:48px 0; display:flex; gap:20px; align-items:flex-start}
    .grid-2{display:grid; grid-template-columns:1fr 420px; gap:28px; align-items:start}

    .panel{background:linear-gradient(180deg, rgba(255,255,255,0.015), rgba(255,255,255,0.01)); border-radius:12px; border:1px solid rgba(255,255,255,0.03); padding:18px}
    .schedule .item{display:flex; gap:12px; align-items:flex-start; padding:12px 0; border-bottom:1px solid rgba(255,255,255,0.02)}
    .schedule .time{font-weight:800; min-width:78px}
    .speaker{display:flex; gap:12px; align-items:center}
    .avatar{width:56px; height:56px; border-radius:12px; background:linear-gradient(90deg,#704CFF,#00D2FF); display:grid; place-items:center; font-weight:800}

    /* FAQ */
    .faq .q{padding:12px 0; border-bottom:1px solid rgba(255,255,255,0.02)}

    /* Footer */
    footer{padding:24px 0; color:rgba(255,255,255,0.06); text-align:center}

    /* terminal Easter egg */
    .terminal{position:fixed; right:28px; bottom:28px; width:min(820px,92vw); max-height:72vh; background:linear-gradient(180deg,#041018,#07141a); color:#a3ffd6; border-radius:12px; padding:18px; box-shadow:0 18px 90px rgba(0,0,0,0.7); display:none; z-index:9999; font-family:ui-monospace, SFMono-Regular, Menlo, Monaco, monospace}
    .term-head{display:flex; gap:10px; align-items:center; margin-bottom:10px}
    .term-dot{width:12px;height:12px;border-radius:50%}
    .dot-red{background:#ff6159}
    .dot-yellow{background:#ffbe2e}
    .dot-green{background:#32d74b}
    .term-content{white-space:pre-wrap; font-size:13px; line-height:1.5; max-height:54vh; overflow:auto}
    .term-input{outline:none; border:0; background:transparent; color:inherit; width:100%; font-family:inherit}

    /* responsive adjustments */
    @media (max-width:1100px){ .grid-2{grid-template-columns:1fr 360px} .right-col{width:340px} }
    @media (max-width:820px){ .card{flex-direction:column; align-items:flex-start} .right-col{width:100%} .grid-2{grid-template-columns:1fr} }

    /* reduced motion */
    @media (prefers-reduced-motion:reduce){ *{animation:none!important; transition:none!important} }
  </style>
</head>
<body>
  <!-- Background layers -->
  <div class="bg-wrap" aria-hidden="true">
    <div class="bg-gradient"></div>
    <div class="bg-grid"></div>
    <div class="bg-noise"></div>
  </div>

  <div class="container" id="container">
    <!-- NAV -->
    <header class="nav" role="banner">
      <div class="nav-left">
        <div class="logo" aria-hidden="true">
          <svg width="40" height="40" viewBox="0 0 120 120" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
            <rect x="6" y="6" width="108" height="108" rx="20" fill="rgba(255,255,255,0.02)"/>
            <path d="M24 80C44 64 68 40 100 44" stroke="#704CFF" stroke-width="6" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <b>Code × Ninja</b>
        </div>
        <nav class="nav-links" role="navigation" aria-label="primary">
          <a href="#program">Program</a>
          <a href="#speakers">Speakers</a>
          <a href="#faq">FAQ</a>
        </nav>
      </div>

      <div class="nav-cta">
        <button class="btn btn-muted" id="toggleAudio">Lo‑Fi</button>
        <button class="btn btn-primary" id="applyBtn">Request Invite</button>
      </div>
    </header>

    <!-- HERO CARD -->
    <section class="card" role="region" aria-labelledby="hero-title">
      <div class="brand" aria-hidden="true">
        <!-- Large glyph / animated -->
        <svg viewBox="0 0 160 160" width="120" height="120" xmlns="http://www.w3.org/2000/svg">
          <defs>
            <linearGradient id="gA" x1="0" x2="1"><stop offset="0" stop-color="#704CFF"/><stop offset="1" stop-color="#00D2FF"/></linearGradient>
            <filter id="glo"><feGaussianBlur stdDeviation="4" result="b"/><feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
          </defs>
          <rect x="8" y="8" width="144" height="144" rx="26" fill="rgba(255,255,255,0.02)"/>
          <g transform="translate(18,18) scale(0.8)" filter="url(#glo)">
            <path id="n" d="M30 52c6-2 22-20 36-20 4 0 8 2 12 6 0 0-10 10-14 18-6 12-24 26-44 22 0 0 10-12 10-26z" stroke="url(#gA)" stroke-width="6" stroke-linecap="round" stroke-linejoin="round" fill="none"/>
            <circle cx="84" cy="32" r="6" fill="url(#gA)"/>
          </g>
          <animate xlink:href="#n" attributeName="opacity" values="0.2;1;0.2" dur="3.6s" repeatCount="indefinite"/>
        </svg>
      </div>

      <div class="hero-meta">
        <div class="eyebrow">Invite-only summit</div>
        <h1 id="hero-title" class="title">Code × Ninja 10 — The Digital Dojo</h1>
        <p class="lead">A cinematic, ultra-minimalist gathering for elite engineers. Precision-focused sessions, live katas, curated cohorts, and a final deploy ceremony. Crafted like an Apple keynote; executed like a ritual.</p>

        <div class="meta-actions">
          <div style="display:flex; gap:10px; align-items:center;">
            <span class="tag" style="padding:8px 12px; border-radius:999px; background:linear-gradient(90deg, rgba(112,76,255,0.12), rgba(0,210,255,0.06)); font-weight:800">Oct 18–20, 2025</span>
            <span class="tag" style="padding:8px 12px; border-radius:999px; font-weight:800">Tokyo • Virtual</span>
          </div>
          <div style="margin-left:auto; display:flex; gap:10px">
            <button class="btn btn-primary" id="applyMain">Apply for Invite</button>
            <button class="btn btn-muted" id="programBtn">View Program</button>
          </div>
        </div>
      </div>

      <div class="right-col" aria-hidden="true">
        <div class="sigil-wrap">
          <!-- Animated sigil: rotating blades + pulse -->
          <svg viewBox="0 0 600 360" preserveAspectRatio="xMidYMid meet" width="100%">
            <defs>
              <linearGradient id="G1" x1="0" x2="1"><stop offset="0" stop-color="#704CFF"/><stop offset="1" stop-color="#00D2FF"/></linearGradient>
              <filter id="blur8"><feGaussianBlur stdDeviation="8" result="b"/></filter>
            </defs>
            <g filter="url(#blur8)" opacity="0.12">
              <path d="M0 220 C120 100 240 100 360 220 C480 340 600 340 720 220" transform="translate(-60,-40) scale(0.8)" stroke="url(#G1)" stroke-width="24" stroke-linecap="round" fill="none"></path>
            </g>
            <g transform="translate(300,180)">
              <circle r="64" fill="rgba(255,255,255,0.01)" stroke="url(#G1)" stroke-width="4"></circle>
              <g id="blade">
                <path d="M0 -46 L26 -8 L-26 -8 Z" fill="url(#G1)"></path>
                <path d="M0 46 L26 8 L-26 8 Z" fill="url(#G1)" opacity="0.9"></path>
              </g>
              <use href="#blade" transform="rotate(45)"/>
              <use href="#blade" transform="rotate(90)"/>
              <use href="#blade" transform="rotate(135)"/>
              <animateTransform attributeName="transform" attributeType="XML" type="rotate" from="0 300 180" to="360 300 180" dur="14s" repeatCount="indefinite"/>
            </g>
            <circle cx="300" cy="180" r="72" stroke="rgba(255,255,255,0.06)" stroke-width="1">
              <animate attributeName="r" values="56;96;56" dur="4.6s" repeatCount="indefinite"/>
              <animate attributeName="opacity" values="0.6;0.02;0.6" dur="4.6s" repeatCount="indefinite"/>
            </circle>
          </svg>
        </div>

        <div style="width:100%; display:flex; gap:8px; justify-content:flex-end">
          <div class="tag">Limited seating</div>
        </div>
      </div>
    </section>

    <!-- PROGRAM + SPEAKERS -->
    <section id="program" class="section">
      <div class="grid-2">
        <div>
          <h3 style="font-family:var(--fw-display); font-weight:800; font-size:20px; margin:0 0 12px">Program</h3>
          <div class="panel schedule" aria-labelledby="program">
            <!-- Day 1 -->
            <div style="font-weight:800; margin-bottom:8px">Day 1 — Opening & Katas</div>
            <div class="item"><div class="time">09:00</div><div><div style="font-weight:800">Opening Keynote — Precision</div><div style="color:var(--muted); font-size:13px">Ceremony-level keynote: craft as ritual.</div></div></div>
            <div class="item"><div class="time">10:30</div><div><div style="font-weight:800">Live Kata — One-line TDD</div><div style="color:var(--muted); font-size:13px">Rapid tests, fierce focus.</div></div></div>
            <div class="item"><div class="time">13:00</div><div><div style="font-weight:800">Silent Debugging</div><div style="color:var(--muted); font-size:13px">Troubleshoot in enforced quiet.</div></div></div>
            <!-- Day 2 -->
            <div style="font-weight:800; margin:14px 0 8px">Day 2 — Duels & Deep Practice</div>
            <div class="item"><div class="time">09:00</div><div><div style="font-weight:800">Pair Kata — Live Duels</div><div style="color:var(--muted); font-size:13px">Head-to-head on curated challenges.</div></div></div>
            <div class="item"><div class="time">15:00</div><div><div style="font-weight:800">Workshop — Critical Refactor</div><div style="color:var(--muted); font-size:13px">Focused refactor under time pressure.</div></div></div>
            <!-- Day 3 -->
            <div style="font-weight:800; margin:14px 0 8px">Day 3 — Deploy & Closing</div>
            <div class="item"><div class="time">11:00</div><div><div style="font-weight:800">Deploy Ceremony</div><div style="color:var(--muted); font-size:13px">Final collective deploys & ritual close.</div></div></div>
          </div>
        </div>

        <aside id="speakers" class="panel">
          <h4 style="margin:0 0 12px; font-weight:800">Speakers & Masters</h4>
          <div style="display:flex; flex-direction:column; gap:12px">
            <div class="speaker"><div class="avatar">AK</div><div><div style="font-weight:800">Akira Tan</div><div style="font-size:13px; color:var(--muted)">Systems wizard, latency whisperer</div></div></div>
            <div class="speaker"><div class="avatar">ML</div><div><div style="font-weight:800">Maya Li</div><div style="font-size:13px; color:var(--muted)">Design systems, motion & optics</div></div></div>
            <div class="speaker"><div class="avatar">RJ</div><div><div style="font-weight:800">R. Joshi</div><div style="font-size:13px; color:var(--muted)">Security kata, safe-by-default</div></div></div>
          </div>
        </aside>
      </div>
    </section>

    <!-- CTA / Email form (progressive enhancement) -->
    <section class="section" style="align-items:center; justify-content:center; text-align:center">
      <div style="max-width:780px; width:100%">
        <div class="panel" style="display:flex; flex-direction:column; gap:12px; align-items:center">
          <div style="font-weight:800; font-size:18px">Apply for an Invite</div>
          <p style="color:var(--muted); margin:0 0 8px">Applications are reviewed by hand. We prioritize craft, learning intent, and community contribution.</p>
          <form id="applyForm" style="display:flex; gap:10px; width:100%; max-width:720px;">
            <input id="name" name="name" placeholder="Your full name" required style="flex:2; padding:12px 14px; border-radius:10px; border:1px solid rgba(255,255,255,0.04); background:transparent; color:inherit" />
            <input id="email" name="email" type="email" placeholder="Email" required style="flex:2; padding:12px 14px; border-radius:10px; border:1px solid rgba(255,255,255,0.04); background:transparent; color:inherit" />
            <button class="btn btn-primary" type="submit" style="flex:1">Apply</button>
          </form>
          <div id="applyMsg" style="font-size:13px; color:var(--muted); margin-top:6px"></div>
        </div>
      </div>
    </section>

    <!-- FAQ -->
    <section id="faq" class="section">
      <div style="width:100%">
        <h3 style="font-weight:800; margin:0 0 12px">FAQ</h3>
        <div class="panel faq">
          <div class="q"><div style="font-weight:800">Is this in-person?</div><div style="color:var(--muted)">Yes — Tokyo hosts a physical cohort; the main event is hybrid. Remote seats are limited.</div></div>
          <div class="q"><div style="font-weight:800">How do I get an invite?</div><div style="color:var(--muted)">Apply above. Invitations are manual and prioritized by craft and fit.</div></div>
          <div class="q"><div style="font-weight:800">Can I speak?</div><div style="color:var(--muted)">Speaker slots are curated. Submit a concise pitch with the application.</div></div>
        </div>
      </div>
    </section>

    <footer>
      <div style="display:flex; gap:10px; justify-content:center; align-items:center; flex-wrap:wrap">
        <div style="color:rgba(255,255,255,0.06)">&copy; Code × Ninja</div>
        <div style="color:rgba(255,255,255,0.06)">—</div>
        <div style="color:rgba(255,255,255,0.06)">Designed for precision</div>
      </div>
    </footer>
  </div>

  <!-- Hidden elements: audio, terminal -->
  <audio id="lofi" loop preload="metadata"><source src="./lofi-sample.mp3" type="audio/mpeg"></audio>
  <div class="terminal" id="terminal" role="dialog" aria-hidden="true">
    <div class="term-head"><div class="term-dot dot-red"></div><div class="term-dot dot-yellow"></div><div class="term-dot dot-green"></div><strong style="margin-left:6px">dojo@codex:~</strong></div>
    <div class="term-content" id="termContent">Welcome to Code × Ninja hidden console. Type <code>help</code> to begin.
> </div>
    <div style="margin-top:12px"><input id="termInput" class="term-input" autocomplete="off" spellcheck="false" aria-label="terminal input" /></div>
  </div>

  <script>
    /* =====================
       Progressive behaviors
       =====================*/
    (function(){
      // Simple feature detection
      const hasAudio = !!document.createElement('audio').canPlayType;

      // Pre-cache some small images (data URIs) if needed — omitted here for brevity

      // Trailer modal stub (opens YouTube in iframe when available)
      document.getElementById('programBtn').addEventListener('click', ()=>{ document.getElementById('program').scrollIntoView({behavior:'smooth'}); });
      document.getElementById('applyBtn').addEventListener('click', ()=>{ document.getElementById('applyForm').scrollIntoView({behavior:'smooth'}); });

      // Form submission (fake, client-side) — demonstrates validation and UX
      const form = document.getElementById('applyForm');
      const msg = document.getElementById('applyMsg');
      form.addEventListener('submit', (e)=>{
        e.preventDefault(); const name = form.name.value.trim(); const email = form.email.value.trim();
        if(!name || !email){ msg.textContent='Please complete the form.'; return; }
        // Simulated network call
        msg.style.color='var(--muted)'; msg.textContent='Submitting…'; setTimeout(()=>{ msg.textContent='Application received. We review invites manually — expect reply within 7–10 days.'; form.reset(); }, 1200);
      });

      // Audio toggle with WebAudio fallback
      const btnAudio = document.getElementById('toggleAudio'); const audioEl = document.getElementById('lofi'); let playing=false; let wa=null;
      async function startWebAudio(){ const ctx = new (window.AudioContext||window.webkitAudioContext)(); const buffer = ctx.createBuffer(1, ctx.sampleRate*3, ctx.sampleRate); const data = buffer.getChannelData(0); for(let i=0;i<data.length;i++) data[i]=(Math.random()*2-1)*0.002; const src=ctx.createBufferSource(); src.buffer=buffer; src.loop=true; const biquad=ctx.createBiquadFilter(); biquad.type='lowpass'; biquad.frequency.value=1400; const gain=ctx.createGain(); gain.gain.value=0.12; src.connect(biquad); biquad.connect(gain); gain.connect(ctx.destination); src.start(); wa={ctx,src,gain}; }
      async function toggleAudio(){ if(playing){ if(audioEl&&!audioEl.paused) audioEl.pause(); if(wa){ wa.src.stop(); wa.ctx.close(); wa=null; } btnAudio.textContent='Lo‑Fi'; playing=false; btnAudio.setAttribute('aria-pressed','false'); return; } if(audioEl && audioEl.querySelector('source').src){ try{ await audioEl.play(); playing=true; btnAudio.textContent='Pause'; btnAudio.setAttribute('aria-pressed','true'); }catch(e){ await startWebAudio(); playing=true; btnAudio.textContent='Pause'; btnAudio.setAttribute('aria-pressed','true'); } } else { await startWebAudio(); playing=true; btnAudio.textContent='Pause'; btnAudio.setAttribute('aria-pressed','true'); } }
      btnAudio.addEventListener('click', toggleAudio);

      // Terminal Easter egg — open with backtick (`) or Ctrl+Shift+N
      const terminal = document.getElementById('terminal'); const termInput = document.getElementById('termInput'); const termContent = document.getElementById('termContent'); let open=false;
      function openTerm(){ terminal.style.display='block'; terminal.setAttribute('aria-hidden','false'); termInput.focus(); open=true; }
      function closeTerm(){ terminal.style.display='none'; terminal.setAttribute('aria-hidden','true'); open=false; }
      window.addEventListener('keydown', (e)=>{ if(e.key==='`' && !e.ctrlKey && !e.metaKey){ e.preventDefault(); open?closeTerm():openTerm(); } if(e.ctrlKey && e.shiftKey && e.key.toLowerCase()==='n'){ e.preventDefault(); open?closeTerm():openTerm(); } if(e.key==='Escape' && open) closeTerm(); });
      termInput.addEventListener('keydown', (e)=>{ if(e.key==='Enter'){ const v=termInput.value.trim(); if(!v){ termContent.textContent += '
> '; termInput.value=''; return; } termContent.textContent += '
$ '+v+'
'; handleCmd(v.toLowerCase()); termInput.value=''; termContent.scrollTop = termContent.scrollHeight; } });
      function handleCmd(cmd){ if(cmd==='help'){ termContent.textContent += 'help — show this list
status — dojo status
kata — random kata
whoami — ninja rank
clear — clear
exit — close terminal
'; }
        else if(cmd==='status'){ termContent.textContent += 'dojo: active
cohorts: 6/6
mission: refine craft
'; }
        else if(cmd==='kata'){ const kata=['Refactor Sprint — 30m','Silent Debugging — 20m','One-line TDD — 25m','Merge Ritual — 15m']; termContent.textContent += kata[Math.floor(Math.random()*kata.length)]+'
'; }
        else if(cmd==='whoami'){ termContent.textContent += 'ninja@anon — rank: black-belt (provisional)
'; }
        else if(cmd==='clear'){ termContent.textContent = '> '; }
        else if(cmd==='exit'){ closeTerm(); }
        else { termContent.textContent += 'command not found: '+cmd+'
'; } }

      // Keyboard shortcut: press K to focus apply button
      window.addEventListener('keydown', (e)=>{ if(e.key.toLowerCase()==='k' && !e.metaKey && !e.ctrlKey && !e.altKey){ document.getElementById('applyBtn').focus(); } });

      // Subtle parallax on mouse for sigil and hero
      let mx=0,my=0; window.addEventListener('mousemove', (e)=>{ mx=(e.clientX - window.innerWidth/2)/window.innerWidth; my=(e.clientY - window.innerHeight/2)/window.innerHeight; const hero=document.querySelector('.card'); if(hero){ hero.style.transform = `translate3d(${mx*12}px, ${my*8}px, 0)`; } const sig=document.querySelector('.sigil-wrap'); if(sig){ sig.style.transform = `translate3d(${mx*18}px, ${my*10}px, 0)`; } });

      // Minimal focus ring for keyboard users
      window.addEventListener('keydown',(e)=>{ if(e.key==='Tab') document.body.classList.add('user-tab'); });

      // tiny dev analytics (console only)
      document.addEventListener('click',(e)=>{ if(e.target.closest('.btn-primary')) console.log('interaction:primary'); });

    })();
  </script>

  <!-- Notes for deployers (developer docs embedded) -->
  <!--
    Deployment notes / tips (keep these in the source):
    - Replace ./lofi-sample.mp3 with a licensed ambient audio. Keep loop short (2–5 min) and fade on start.
    - Use a CDN for Google Fonts or self-host for privacy-sensitive builds.
    - Replace avatars and speaker data with real content and optimize SVGs for production.
    - Consider adding a small Service Worker for offline assets and fast re-visit animations.
    - For accessibility: ensure color contrast and keyboard focus on interactive elements. Provide transcripts for talk videos.

    Files to include alongside this HTML for production:
    - /assets/lofi-sample.mp3 (or use streaming link)
    - small poster image for social cards
    - optionally a manifest.json + icons for PWA
  -->
</body>
</html>
<footer>
  <div style="display:flex; gap:10px; justify-content:center; align-items:center; flex-wrap:wrap">
    <div style="color:rgba(255,255,255,0.06)">&copy; Code × Ninja</div>
    <div style="color:rgba(255,255,255,0.06)">—</div>
    <div style="color:rgba(255,255,255,0.06)">Designed for precision</div>
  </div>
  <div style="margin-top:8px; font-size:13px; color:rgba(255,255,255,0.3); text-align:center;">
    Rudra Pratap Singh • Reg No: RA2511003011539 • SRM Institute of Science and Technology
  </div>
</footer>
