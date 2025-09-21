<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Code × Ninja 10 — Digital Dojo</title>
  <meta name="description" content="An ultra-minimalist cinematic landing page for Code × Ninja 10 — glassmorphism, ambient gradients, parallax, animated SVGs, lo-fi audio, and a hidden terminal." />
  <meta name="robots" content="noindex" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&family=Space+Grotesk:wght@400;600;700&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg-1: 8 10 16; /* dark */
      --accent-1: 112 76 255; /* violet */
      --accent-2: 0 210 255; /* cyan */
      --glass: rgba(255,255,255,0.05);
      --muted: rgba(255,255,255,0.65);
      --gap: 32px;
      --radius: 18px;
      --card-w: 1080px;
      --fw-sans: 'Inter', system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
      --fw-display: 'Space Grotesk', var(--fw-sans);
      color-scheme: dark;
    }

    /* Reset */
    *{box-sizing:border-box}
    html,body{height:100%}
    body{margin:0; font-family:var(--fw-sans); background-color:rgb(var(--bg-1)); color:#fff; -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;}

    /* cinematic ambient background */
    .bg{
      position:fixed; inset:0; z-index:-2; pointer-events:none; overflow:hidden;
      background:
        radial-gradient(800px 400px at 10% 20%, rgba(var(--accent-2),0.06), transparent),
        radial-gradient(600px 300px at 90% 80%, rgba(var(--accent-1),0.05), transparent),
        linear-gradient(180deg, rgba(2,4,8,1) 0%, rgba(6,6,10,1) 100%);
    }
    .grain{
      position:fixed; inset:0; z-index:-1; opacity:0.03; background-image:url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="120" height="120"><filter id="g"><feTurbulence baseFrequency="0.9" numOctaves="1" stitchTiles="stitch"/></filter><rect width="100%" height="100%" filter="url(%23g)"/></svg>'); mix-blend-mode:overlay;
    }

    /* layout container */
    .stage{min-height:100vh; display:flex; flex-direction:column; align-items:center; justify-content:center; padding:clamp(20px,4vw,64px); gap:var(--gap);}

    /* card */
    .card{
      width:min(100%, var(--card-w)); display:flex; gap:28px; align-items:center; padding:clamp(28px,4vw,56px); border-radius:calc(var(--radius) + 6px);
      background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); border:1px solid rgba(255,255,255,0.04); backdrop-filter: blur(14px) saturate(140%);
      box-shadow: 0 30px 80px rgba(2,6,23,0.6), inset 0 1px 0 rgba(255,255,255,0.02);
      transition: transform 500ms cubic-bezier(.2,.9,.25,1), box-shadow 300ms ease;
    }
    .card:hover{ transform: translateY(-8px); }

    .brand{flex:0 0 140px; display:flex; align-items:center; justify-content:center}
    .brand svg{width:110px;height:110px}

    .meta{flex:1; display:flex; flex-direction:column; gap:12px}
    .eyebrow{font-weight:600; color:var(--muted); font-size:13px; letter-spacing:0.12em; text-transform:uppercase}
    .headline{font-family:var(--fw-display); font-weight:800; font-size:clamp(28px,4.5vw,56px); line-height:0.92; margin:0}
    .sub{color:rgba(255,255,255,0.72); font-size:16px; max-width:66ch}

    .meta .tags{display:flex; gap:10px; margin-top:6px}
    .tag{padding:8px 12px; border-radius:999px; font-weight:700; font-size:13px; background:linear-gradient(90deg, rgba(var(--accent-1),0.12), rgba(var(--accent-2),0.06)); border:1px solid rgba(255,255,255,0.03)}

    .actions{display:flex; align-items:center; gap:12px}
    .btn-primary{background:linear-gradient(90deg, rgba(var(--accent-1),1), rgba(var(--accent-2),1)); color:#fff; padding:12px 18px; border-radius:12px; font-weight:800; font-size:14px; border:0; cursor:pointer; box-shadow:0 12px 36px rgba(8,6,20,0.6);}
    .btn-ghost{padding:10px 14px; border-radius:10px; border:1px solid rgba(255,255,255,0.06); background:transparent; color:var(--muted); font-weight:700; cursor:pointer}

    /* hero */
    .hero{width:min(100%,var(--card-w)); display:grid; grid-template-columns:1fr 360px; gap:36px; align-items:center; margin-top:8px}
    .hero h1{font-family:var(--fw-display); font-size:clamp(40px,8vw,112px); margin:0; line-height:0.92; font-weight:900}
    .hero p{margin:12px 0 0 0; font-size:18px; color:rgba(255,255,255,0.8); max-width:68ch}

    .aside{display:flex; flex-direction:column; gap:18px; align-items:flex-end}

    /* animated sigil */
    .sigil{width:100%; display:flex; align-items:center; justify-content:center}
    .sigil svg{width:100%; height:auto; max-width:360px}

    /* glass info panel */
    .glass-panel{width:100%; padding:18px 20px; border-radius:14px; background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); border:1px solid rgba(255,255,255,0.04); backdrop-filter: blur(8px); display:flex; gap:16px; align-items:center}
    .glass-panel .meta-left{flex:1}
    .glass-panel .meta-right{display:flex; gap:10px; align-items:center}

    /* terminal Easter egg */
    .terminal{
      position:fixed; right:28px; bottom:28px; width:min(760px,90vw); max-height:72vh; background:linear-gradient(180deg,#050509, #071018); color:#9bffd0; border-radius:12px; padding:18px; box-shadow:0 18px 80px rgba(0,0,0,0.7); display:none; z-index:9999; border:1px solid rgba(255,255,255,0.03); font-family:ui-monospace, SFMono-Regular, Menlo, Monaco, monospace;}
    .term-head{display:flex; gap:10px; align-items:center; margin-bottom:10px}
    .term-dot{width:12px;height:12px;border-radius:50%}
    .dot-red{background:#ff6159}
    .dot-yellow{background:#ffbe2e}
    .dot-green{background:#32d74b}
    .term-content{white-space:pre-wrap; font-size:13px; line-height:1.5; max-height:52vh; overflow:auto}
    .term-input{outline:none; border:0; background:transparent; color:inherit; width:100%; font-family:inherit}

    /* preloader */
    .preloader{position:fixed; inset:0; display:flex; align-items:center; justify-content:center; z-index:99999; background:linear-gradient(180deg, #000000, rgba(0,0,0,0.6));}
    .preloader .lo{width:84px;height:84px; border-radius:20px; display:grid; place-items:center; border:1px solid rgba(255,255,255,0.04); backdrop-filter:blur(8px);}

    /* responsive */
    @media (max-width:1024px){ .hero{grid-template-columns:1fr 280px} .card{padding:20px} }
    @media (max-width:800px){ .hero{grid-template-columns:1fr; } .aside{align-items:center} .card{flex-direction:column; align-items:flex-start;} .brand{flex:0 0 auto} }

    /* accessibility focus */
    :focus{outline:2px solid rgba(255,255,255,0.06); outline-offset:3px}

    /* reduced motion */
    @media (prefers-reduced-motion:reduce){ *{animation:none!important; transition:none!important} }
  </style>
</head>
<body>
  <div class="bg" aria-hidden="true"></div>
  <div class="grain" aria-hidden="true"></div>

  <!-- preloader -->
  <div class="preloader" id="preloader" aria-hidden="true">
    <div class="lo">
      <!-- subtle animated logo -->
      <svg width="64" height="64" viewBox="0 0 120 120" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <rect x="6" y="6" width="108" height="108" rx="20" fill="rgba(255,255,255,0.02)" />
        <path d="M20 80C40 64 64 40 96 44" stroke="rgba(112,76,255,0.9)" stroke-width="6" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </div>
  </div>

  <main class="stage" id="stage">
    <div class="card" role="region" aria-labelledby="main-title">
      <div class="brand" aria-hidden="true">
        <!-- refined animated ninja glyph -->
        <svg viewBox="0 0 160 160" xmlns="http://www.w3.org/2000/svg">
          <defs>
            <linearGradient id="gradA" x1="0" x2="1"><stop offset="0" stop-color="#704CFF"/><stop offset="1" stop-color="#00D2FF"/></linearGradient>
            <filter id="glow"><feGaussianBlur stdDeviation="4" result="b"/><feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
          </defs>
          <rect x="8" y="8" width="144" height="144" rx="26" fill="rgba(255,255,255,0.02)"/>
          <g transform="translate(18,18) scale(0.8)" filter="url(#glow)">
            <path id="ninja" d="M30 52c6-2 22-20 36-20 4 0 8 2 12 6 0 0-10 10-14 18-6 12-24 26-44 22 0 0 10-12 10-26z" stroke="url(#gradA)" stroke-width="6" stroke-linecap="round" stroke-linejoin="round" fill="none"/>
            <circle cx="84" cy="32" r="6" fill="url(#gradA)"/>
          </g>
          <animate xlink:href="#ninja" attributeName="opacity" values="0.2;1;0.2" dur="3.6s" repeatCount="indefinite"/>
        </svg>
      </div>

      <div class="meta">
        <div style="display:flex; align-items:flex-start; gap:18px; width:100%">
          <div style="flex:1">
            <div class="eyebrow">Code × Ninja</div>
            <h2 id="main-title" class="headline">10 — The Digital Dojo</h2>
            <p class="sub">A cinematic, invite-only gathering for elite coders. Expect theater-grade talks, live code kata, and curated deep practice — crafted like a keynote, executed like a ritual.</p>
            <div class="tags" aria-hidden="true">
              <span class="tag">Private • Invite-only</span>
              <span class="tag">Oct 18–20, 2025</span>
              <span class="tag">Tokyo • Virtual</span>
            </div>
          </div>

          <div class="actions" aria-hidden="false">
            <button class="btn-primary" id="rsvpBtn">Request Invite</button>
            <button class="btn-ghost" id="trailerBtn" aria-haspopup="dialog">Play Trailer</button>
          </div>
        </div>

        <div style="margin-top:12px">
          <div class="glass-panel" role="group" aria-label="event highlights">
            <div class="meta-left">
              <div style="font-weight:700">Precision • Power • Discipline</div>
              <div style="font-size:13px; color:var(--muted); margin-top:6px">Curated sessions, small cohorts, live code duels, and a final deploy ceremony.</div>
            </div>
            <div class="meta-right">
              <div style="font-size:12px; color:var(--muted)">Ambience</div>
              <div id="audioToggle" role="button" tabindex="0" aria-pressed="false" style="cursor:pointer; padding:8px 10px; border-radius:10px; background:rgba(255,255,255,0.02); border:1px solid rgba(255,255,255,0.03); font-weight:700">Lo‑Fi</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <section class="hero" aria-labelledby="hero-head">
      <div>
        <h1 id="hero-head">The code is your kata. The editor is your sword.</h1>
        <p>Three days. Ten sessions. One mission: refine craft through focused practice, high-velocity demos, and controlled chaos. Expect precision tech talks, live coding duels, and a ceremony of deploys.</p>

        <div style="display:flex; gap:12px; margin-top:18px">
          <button class="btn-primary">Apply for Invite</button>
          <button class="btn-ghost" id="learnBtn">Program & Schedule</button>
        </div>
      </div>

      <aside class="aside">
        <div class="sigil" aria-hidden="true">
          <!-- intricate animated SVG sigil with parallax layers -->
          <svg viewBox="0 0 600 360" preserveAspectRatio="xMidYMid meet">
            <defs>
              <linearGradient id="G" x1="0" x2="1"><stop offset="0" stop-color="#704CFF"/><stop offset="1" stop-color="#00D2FF"/></linearGradient>
              <filter id="f1"><feGaussianBlur stdDeviation="8" result="b"/><feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
            </defs>

            <g id="bgWaves" filter="url(#f1)" opacity="0.14">
              <path d="M0 200 C120 80 240 80 360 200 C480 320 600 320 720 200" transform="translate(-60,-40) scale(0.8)" stroke="url(#G)" stroke-width="18" stroke-linecap="round" fill="none"></path>
            </g>

            <g id="center">
              <circle cx="300" cy="180" r="56" stroke="url(#G)" stroke-width="5" fill="rgba(255,255,255,0.01)"/>
              <path d="M300 132 L330 180 L300 228 L270 180 Z" fill="url(#G)" opacity="0.98">
                <animateTransform attributeName="transform" attributeType="XML" type="rotate" from="0 300 180" to="360 300 180" dur="12s" repeatCount="indefinite"/>
              </path>
            </g>

            <g id="pulse">
              <circle cx="300" cy="180" r="60" stroke="rgba(255,255,255,0.06)" stroke-width="1">
                <animate attributeName="r" values="48;86;48" dur="4.8s" repeatCount="indefinite"/>
                <animate attributeName="opacity" values="0.6;0.02;0.6" dur="4.8s" repeatCount="indefinite"/>
              </circle>
            </g>
          </svg>
        </div>

        <div style="width:100%; display:flex; gap:8px; justify-content:flex-end">
          <div class="tag">Limited seating</div>
        </div>
      </aside>
    </section>

    <!-- trailer modal (aria) -->
    <div id="trailerModal" role="dialog" aria-modal="true" aria-hidden="true" style="position:fixed; inset:0; display:none; align-items:center; justify-content:center; z-index:9998; backdrop-filter: blur(6px);">
      <div style="width:min(1100px,96vw); background:linear-gradient(180deg,#071018,#021018); border-radius:14px; padding:18px; border:1px solid rgba(255,255,255,0.03); box-shadow:0 30px 90px rgba(0,0,0,0.7)">
        <div style="display:flex; justify-content:space-between; align-items:center; gap:12px; margin-bottom:10px">
          <strong style="font-family:var(--fw-display); font-weight:800">Code × Ninja 10 — Trailer</strong>
          <button id="closeTrailer" class="btn-ghost">Close</button>
        </div>
        <div style="position:relative; padding-top:56.25%">
          <iframe id="trailerFrame" src="about:blank" style="position:absolute; inset:0; width:100%; height:100%; border:0; border-radius:8px" title="trailer"></iframe>
        </div>
      </div>
    </div>

    <!-- hidden audio element -->
    <audio id="lofi" loop preload="metadata">
      <source src="./lofi-sample.mp3" type="audio/mpeg">
    </audio>

    <!-- terminal Easter egg -->
    <div class="terminal" id="terminal" role="dialog" aria-hidden="true">
      <div class="term-head"><div class="term-dot dot-red"></div><div class="term-dot dot-yellow"></div><div class="term-dot dot-green"></div><strong style="margin-left:6px">dojo@codex:~</strong></div>
      <div class="term-content" id="termContent">Welcome to the secret Code × Ninja console. Type <code>help</code> to begin.
> </div>
      <div style="margin-top:12px"><input id="termInput" class="term-input" autocomplete="off" spellcheck="false" aria-label="terminal input" /></div>
    </div>

    <footer style="width:100%; text-align:center; padding-top:28px; color:rgba(255,255,255,0.06); font-size:13px">&copy; Code × Ninja — digital dojo</footer>
  </main>

  <script>
    (function(){
      // Preloader
      const pre = document.getElementById('preloader');
      window.addEventListener('load', ()=>{
        setTimeout(()=>{ pre.style.opacity=0; pre.style.pointerEvents='none'; pre.remove(); }, 420);
      });

      // Parallax subtle on scroll and mouse
      const stage = document.getElementById('stage');
      let mouseX=0, mouseY=0;
      window.addEventListener('mousemove', (e)=>{ mouseX = (e.clientX - window.innerWidth/2)/window.innerWidth; mouseY = (e.clientY - window.innerHeight/2)/window.innerHeight; document.documentElement.style.setProperty('--mx', mouseX); document.documentElement.style.setProperty('--my', mouseY); });

      // Buttons
      document.getElementById('rsvpBtn').addEventListener('click', ()=>{ const b=document.getElementById('rsvpBtn'); b.textContent='Requested'; b.disabled=true; b.style.opacity=0.98; });

      // Trailer modal
      const trailerBtn = document.getElementById('trailerBtn');
      const trailerModal = document.getElementById('trailerModal');
      const trailerFrame = document.getElementById('trailerFrame');
      const closeTrailer = document.getElementById('closeTrailer');
      trailerBtn.addEventListener('click', ()=>{ trailerModal.style.display='flex'; trailerModal.setAttribute('aria-hidden','false'); trailerFrame.src = 'https://www.youtube.com/embed/ScMzIvxBSi4?autoplay=1&controls=0'; });
      closeTrailer.addEventListener('click', ()=>{ trailerModal.style.display='none'; trailerModal.setAttribute('aria-hidden','true'); trailerFrame.src='about:blank'; });

      // audio toggle with fallback WebAudio
      const audioToggle = document.getElementById('audioToggle');
      const audioEl = document.getElementById('lofi');
      let playing=false; let wa=null;
      async function startWebAudio(){
        const ctx = new (window.AudioContext || window.webkitAudioContext)();
        const buffer = ctx.createBuffer(1, ctx.sampleRate*3, ctx.sampleRate);
        const data = buffer.getChannelData(0); for(let i=0;i<data.length;i++) data[i] = (Math.random()*2-1)*0.002;
        const src = ctx.createBufferSource(); src.buffer=buffer; src.loop=true;
        const bp = ctx.createBiquadFilter(); bp.type='lowpass'; bp.frequency.value = 1400;
        const gain = ctx.createGain(); gain.gain.value = 0.12;
        src.connect(bp); bp.connect(gain); gain.connect(ctx.destination); src.start(); wa={ctx,src,gain};
      }
      async function toggleAudio(){
        if(playing){ if(audioEl && !audioEl.paused) audioEl.pause(); if(wa){ wa.src.stop(); wa.ctx.close(); wa=null; } audioToggle.setAttribute('aria-pressed','false'); playing=false; return; }
        // try native
        if(audioEl && audioEl.querySelector('source').src){ try{ await audioEl.play(); playing=true; audioToggle.setAttribute('aria-pressed','true'); }catch(e){ await startWebAudio(); playing=true; audioToggle.setAttribute('aria-pressed','true'); } } else { await startWebAudio(); playing=true; audioToggle.setAttribute('aria-pressed','true'); }
      }
      audioToggle.addEventListener('click', toggleAudio);
      audioToggle.addEventListener('keydown', (e)=>{ if(e.key==='Enter' || e.key===' ') { e.preventDefault(); toggleAudio(); } });

      // Terminal Easter egg (Backtick ` or Ctrl+Shift+N), with commands
      const terminal = document.getElementById('terminal'); const termInput = document.getElementById('termInput'); const termContent = document.getElementById('termContent'); let termOpen=false;
      function openTerm(){ terminal.style.display='block'; terminal.setAttribute('aria-hidden','false'); termInput.focus(); termOpen=true; }
      function closeTerm(){ terminal.style.display='none'; terminal.setAttribute('aria-hidden','true'); termOpen=false; }
      window.addEventListener('keydown', (e)=>{
        if(e.key==='`' && !e.ctrlKey && !e.metaKey){ e.preventDefault(); termOpen?closeTerm():openTerm(); }
        if(e.ctrlKey && e.shiftKey && e.key.toLowerCase()==='n'){ e.preventDefault(); termOpen?closeTerm():openTerm(); }
        if(e.key==='Escape' && termOpen) closeTerm();
      });

      termInput.addEventListener('keydown',(e)=>{
        if(e.key==='Enter'){ const v=termInput.value.trim(); if(!v){ termContent.textContent += '
> '; termInput.value=''; return;} termContent.textContent += '
$ '+v+'
'; handleCmd(v.toLowerCase()); termInput.value=''; termContent.scrollTop = termContent.scrollHeight; }
      });
      function handleCmd(cmd){ if(cmd==='help'){ termContent.textContent += 'help — show this list
status — dojo status
kata — random kata
whoami — your ninja rank
clear — clear console
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
'; }
      }

      // keyboard shortcut: press K to focus RSVP (for power users)
      window.addEventListener('keydown', (e)=>{ if(e.key.toLowerCase()==='k' && !e.metaKey && !e.ctrlKey && !e.altKey){ document.getElementById('rsvpBtn').focus(); } });

      // small motion: subtle parallax tied to mouse position for hero elements
      const hero = document.querySelector('.hero');
      function rafLoop(){ requestAnimationFrame(rafLoop); const x = (mouseX||0)*12; const y=(mouseY||0)*8; hero.style.transform = `translate3d(${x}px, ${y}px, 0)`; }
      rafLoop();

      // Accessibility: ensure focus-visible like outlines if keyboard used
      window.addEventListener('keydown', (e)=>{ if(e.key==='Tab') document.body.classList.add('user-is-tabbing'); });

      // tiny analytics safe stub: log interaction counts to console for dev
      window.addEventListener('click', (e)=>{ if(e.target.closest('.btn-primary')) console.log('interaction: primary-click'); });

    })();
  </script>
</body>
</html>
