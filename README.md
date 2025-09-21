<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Code × Ninja 10 — Digital Dojo</title>
  <meta name="description" content="An ultra-minimalist cinematic landing page for Code × Ninja 10 — glassmorphism, ambient gradients, parallax, and a secret terminal." />
  <style>
    :root{
      --bg-1: 12 14 23; /* dark navy */
      --accent-1: 112 76 255; /* violet */
      --accent-2: 0 210 255; /* cyan */
      --glass: rgba(255,255,255,0.06);
      --glass-2: rgba(255,255,255,0.04);
      --gap: 28px;
      --radius: 16px;
      --card-w: 860px;
      color-scheme: dark;
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    }

    /* Reset */
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      min-height:100vh;
      background:radial-gradient(1200px 600px at 10% 20%, rgba(var(--accent-2),0.06), transparent),
                 linear-gradient(180deg, rgba(var(--bg-1),1) 0%, #05060a 100%);
      color:rgba(255,255,255,0.95);
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      overflow-x:hidden;
      --motion: 1s cubic-bezier(.2,.9,.25,1);
    }

    /* grid container */
    .wrap{
      min-height:100vh;
      display:grid;
      grid-template-rows:1fr auto;
      align-items:center;
      justify-items:center;
      padding: clamp(24px,4vw,64px);
      gap:var(--gap);
      position:relative;
      isolation:isolate;
    }

    /* parallax layers (interactive on mousemove) */
    .parallax-layer{
      position:absolute; inset:0; pointer-events:none; transform-style:preserve-3d;
    }
    .layer{
      position:absolute; will-change:transform; transition:transform 400ms linear;
    }
    .layer.shape{ filter:blur(28px) saturate(120%); opacity:0.25 }
    .layer.topo{ mix-blend-mode:screen; opacity:0.08 }

    /* Main glass card */
    .card{
      width: min(100%, var(--card-w));
      max-width:100%;
      padding: clamp(28px,4vw,48px);
      border-radius: calc(var(--radius) + 6px);
      background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      backdrop-filter: blur(10px) saturate(140%);
      box-shadow: 0 10px 40px rgba(2,6,23,0.6), inset 0 1px 0 rgba(255,255,255,0.02);
      border: 1px solid rgba(255,255,255,0.04);
      display:flex; gap:24px; align-items:center;
      transform:translateY(0); transition:transform var(--motion);
    }

    .brand{
      min-width:120px; display:flex; align-items:center; justify-content:center; flex-shrink:0;
    }

    .title{
      font-weight:700; letter-spacing:-0.02em; font-size:clamp(28px,4.4vw,44px);
      margin:0 0 8px 0; line-height:1;
    }
    .subtitle{
      color:rgba(255,255,255,0.7); margin:0; font-size:clamp(12px,1.6vw,15px); font-weight:500;
    }

    .info{display:flex; gap:18px; align-items:center; margin-top:14px}
    .pill{padding:8px 12px; border-radius:999px; font-weight:600; font-size:13px; letter-spacing:0.02em; background:linear-gradient(90deg, rgba(var(--accent-1),0.12), rgba(var(--accent-2),0.06)); border:1px solid rgba(255,255,255,0.03)}

    .cta{margin-left:auto; display:flex; gap:12px; align-items:center}
    .btn{
      padding:12px 16px; border-radius:12px; font-weight:700; font-size:14px; cursor:pointer; border:0;
      background:linear-gradient(90deg, rgba(var(--accent-1),0.95), rgba(var(--accent-2),0.9));
      box-shadow: 0 6px 20px rgba(14,12,30,0.6);
      color:white; letter-spacing:0.02em; transform:translateY(0); transition:transform 160ms ease, box-shadow 160ms ease;
    }
    .btn:active{transform:translateY(1px); box-shadow:0 3px 8px rgba(14,12,30,0.5)}

    /* left panel — features */
    .left{
      display:flex; flex-direction:column; gap:6px; flex:1;
    }
    .right{
      width:220px; display:flex; flex-direction:column; gap:10px; align-items:flex-end;
    }

    /* hero large heading */
    .hero{
      text-align:left; width:min(100%,var(--card-w)); padding: calc(clamp(28px,4vw,48px) * 0.2) 0;
      display:grid; grid-template-columns:1fr auto; gap:32px; align-items:center;
    }
    .hero h1{font-size:clamp(40px,6.8vw,96px); margin:0; line-height:0.92; font-weight:800; letter-spacing:-0.02em}
    .hero p{margin:12px 0 0 0; color:rgba(255,255,255,0.72); max-width:60ch; font-size:18px}

    /* animated svg container */
    .svg-wrap{display:flex; align-items:center; justify-content:center; width:420px; height:140px}
    svg{display:block; max-width:100%; height:auto}

    /* footer / controls */
    .controls{display:flex; gap:12px; align-items:center}
    .audio-toggle{display:flex; gap:8px; align-items:center; padding:8px 12px; border-radius:9px; background:var(--glass); border:1px solid rgba(255,255,255,0.03)}

    /* terminal Easter egg */
    .terminal{
      position:fixed; right:36px; bottom:36px; width:min(720px,90vw); max-height:70vh; background:rgba(6,6,10,0.92);
      border-radius:10px; padding:18px; box-shadow:0 12px 40px rgba(0,0,0,0.7); color:#8cffc7; font-family:ui-monospace, SFMono-Regular, Menlo, Monaco, monospace; display:none; z-index:9999; overflow:auto; border:1px solid rgba(255,255,255,0.03)
    }
    .terminal header{display:flex; gap:10px; align-items:center; margin-bottom:10px}
    .term-dot{width:12px;height:12px;border-radius:50%}
    .dot-red{background:#ff6159}
    .dot-yellow{background:#ffbe2e}
    .dot-green{background:#32d74b}
    .terminal .content{white-space:pre-wrap; font-size:13px; line-height:1.45}
    .term-input{outline:none; border:0; background:transparent; color:inherit; width:100%;}

    /* responsive */
    @media (max-width:900px){
      .card{flex-direction:column; padding:20px}
      .right{width:100%; align-items:flex-start}
      .svg-wrap{width:180px;height:72px}
      .hero h1{font-size:clamp(28px,10vw,48px)}
    }

    /* motion preference */
    @media (prefers-reduced-motion:reduce){
      :root{--motion:0s}
      .parallax-layer, .layer{transition:none}
    }

    /* micro interactions */
    .card:hover{transform:translateY(-6px)}

    /* utility */
    .muted{color:rgba(255,255,255,0.6)}
  </style>
</head>
<body>
  <div class="wrap" id="wrap">

    <!-- Parallax decorative layers -->
    <div class="parallax-layer" id="parallax">
      <div class="layer shape" data-speed="0.03" style="left:-10%; top:5%; width:40vw; height:40vh; background:linear-gradient(120deg, rgba(var(--accent-1),0.25), rgba(var(--accent-2),0.18)); border-radius:28%"></div>
      <div class="layer shape" data-speed="0.06" style="right:-12%; bottom:5%; width:30vw; height:30vh; background:linear-gradient(120deg, rgba(var(--accent-2),0.22), rgba(var(--accent-1),0.18)); border-radius:36%"></div>
      <div class="layer topo" data-speed="0.01" style="left:0; right:0; top:20%; height:240px; background-image:radial-gradient(circle at 20% 30%, rgba(255,255,255,0.02), transparent);"></div>
    </div>

    <!-- Main card -->
    <main class="card" role="main" aria-labelledby="main-title">
      <div class="left">
        <div class="brand" aria-hidden="true">
          <!-- animated minimalist ninja glyph -->
          <svg width="120" height="120" viewBox="0 0 120 120" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
            <defs>
              <linearGradient id="g1" x1="0" x2="1">
                <stop offset="0" stop-color="rgba(112,76,255,1)"/>
                <stop offset="1" stop-color="rgba(0,210,255,1)"/>
              </linearGradient>
            </defs>
            <rect x="6" y="6" width="108" height="108" rx="20" fill="rgba(255,255,255,0.02)" />
            <g transform="translate(18,18) scale(0.7)">
              <path id="stroke" d="M30 52c6-2 22-20 36-20 4 0 8 2 12 6 0 0-10 10-14 18-6 12-24 26-44 22 0 0 10-12 10-26z" stroke="url(#g1)" stroke-width="5" stroke-linecap="round" stroke-linejoin="round" fill="none"></path>
              <circle cx="84" cy="32" r="6" fill="url(#g1)"></circle>
            </g>
            <animate xlink:href="#stroke" attributeName="stroke-dashoffset" from="200" to="0" dur="2.4s" begin="0s" fill="freeze" />
          </svg>
        </div>

        <div>
          <h2 id="main-title" class="title">Code × Ninja <span class="muted">10</span></h2>
          <p class="subtitle">A digital dojo — precision, power, discipline. An invite-only event for elite engineers, designers, and black-belt hackers.</p>

          <div class="info">
            <span class="pill">Private • Invite-only</span>
            <span class="pill">October 18, 2025</span>
            <span class="pill">Tokyo • Virtual</span>
          </div>
        </div>
      </div>

      <div class="right">
        <div class="svg-wrap" aria-hidden="true">
          <!-- animated waveform / sigil -->
          <svg viewBox="0 0 600 160" preserveAspectRatio="xMidYMid meet">
            <defs>
              <linearGradient id="lg" x1="0" x2="1">
                <stop offset="0" stop-color="rgba(112,76,255,1)"/>
                <stop offset="1" stop-color="rgba(0,210,255,1)"/>
              </linearGradient>
            </defs>
            <path id="sig" d="M10 120 C110 20 210 20 310 120 C410 220 510 220 590 120" stroke="url(#lg)" stroke-width="6" fill="none" stroke-linecap="round">
              <animate attributeName="stroke-dasharray" values="0,600;600,0;0,600" dur="6s" repeatCount="indefinite" />
            </path>
            <g id="pulses">
              <circle cx="310" cy="120" r="22" fill="rgba(0,0,0,0)" stroke="rgba(255,255,255,0.06)" stroke-width="1">
                <animate attributeName="r" values="6;28;6" dur="4s" repeatCount="indefinite"/>
                <animate attributeName="opacity" values="0.6;0.02;0.6" dur="4s" repeatCount="indefinite"/>
              </circle>
            </g>
          </svg>
        </div>

        <div class="controls">
          <div class="audio-toggle" id="audioToggle" role="button" tabindex="0" aria-pressed="false" title="Toggle lo-fi ambience (replace audio source as desired)">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true"><path d="M4 12h3v6H4zM9 7h3v11H9zM14 4h3v14h-3z" fill="rgba(255,255,255,0.9)"/></svg>
            <span style="font-weight:700; font-size:13px">Lo‑Fi Ambience</span>
          </div>

          <button class="btn" id="rsvp">Request Invite</button>
        </div>
      </div>
    </main>

    <!-- Hero statement under card -->
    <section class="hero" aria-labelledby="hero-head">
      <div>
        <h1 id="hero-head">The code is your kata. The editor is your sword.</h1>
        <p>Three days. Ten sessions. One mission: refine craft through focused practice, high-velocity demos, and controlled chaos. Expect precision tech talks, live coding duels, and a ceremony of deploys.</p>
      </div>
      <div style="text-align:right;">
        <div class="pill muted" style="display:inline-block">Limited seating</div>
      </div>
    </section>

    <!-- hidden audio element (user should replace src with a real file or allow the toggle to use WebAudio fallback) -->
    <audio id="lofi" loop preload="none">
      <source src="./lofi-sample.mp3" type="audio/mpeg">
      <!-- If no file, JS will use a subtle WebAudio ambient synth fallback. -->
    </audio>

    <!-- Terminal Easter egg overlay -->
    <div class="terminal" id="terminal" role="dialog" aria-hidden="true">
      <header>
        <div class="term-dot dot-red"></div>
        <div class="term-dot dot-yellow"></div>
        <div class="term-dot dot-green"></div>
        <strong style="margin-left:8px">dojo@codex:~</strong>
      </header>
      <div class="content" id="termContent">Welcome to the Code × Ninja hidden console. Type <code>help</code> for commands.

> </div>
      <div style="margin-top:12px">
        <input id="termInput" class="term-input" autocomplete="off" spellcheck="false" aria-label="terminal input" />
      </div>
    </div>

    <!-- subtle credits (visually minimal) -->
    <footer style="position:relative; text-align:center; width:100%; padding-top:28px; color:rgba(255,255,255,0.06); font-size:13px">&copy; Code × Ninja — digital dojo</footer>
  </div>

  <script>
    // Respect reduced motion
    const prefersReduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

    // Parallax: mousemove -> transform layers
    (function(){
      const wrap = document.getElementById('parallax');
      const layers = Array.from(wrap.querySelectorAll('.layer'));
      function onMove(e){
        const cx = window.innerWidth/2; const cy = window.innerHeight/2;
        const x = (e.clientX - cx)/cx; const y = (e.clientY - cy)/cy;
        layers.forEach(l=>{
          const s = parseFloat(l.dataset.speed) || 0.02;
          const tx = x * 12 * s * -1; const ty = y * 12 * s * -1;
          l.style.transform = `translate3d(${tx}px, ${ty}px, 0)`;
        });
      }
      if(!prefersReduced){ window.addEventListener('mousemove', onMove); }
    })();

    // Audio toggle: if file exists use audio element, otherwise WebAudio ambient synth
    (function(){
      const el = document.getElementById('audioToggle');
      const audio = document.getElementById('lofi');
      let ctx, osc, gain;
      let playing=false;

      function startWebAudio(){
        ctx = new (window.AudioContext || window.webkitAudioContext)();
        const noise = ctx.createBufferSource();
        // create short noise buffer
        const bufferSize = ctx.sampleRate * 2;
        const buffer = ctx.createBuffer(1, bufferSize, ctx.sampleRate);
        const data = buffer.getChannelData(0);
        for(let i=0;i<bufferSize;i++) data[i] = (Math.random()*2-1) * 0.003; // ultra low
        noise.buffer = buffer; noise.loop = true;
        gain = ctx.createGain(); gain.gain.value = 0.15;
        const biquad = ctx.createBiquadFilter(); biquad.type = 'lowpass'; biquad.frequency.value = 1200;
        noise.connect(biquad); biquad.connect(gain); gain.connect(ctx.destination);
        noise.start();
        // store to stop later
        audio._wa = { ctx, noise, gain };
      }

      async function toggle(){
        if(playing){
          // stop
          if(audio && !audio.paused){ audio.pause(); }
          if(audio._wa){ audio._wa.noise.stop(); audio._wa.ctx.close(); audio._wa = null; }
          playing=false; el.setAttribute('aria-pressed','false'); el.style.opacity=1; return;
        }
        // try native audio first
        if(audio && audio.querySelector('source').src){
          try{
            await audio.play(); playing=true; el.setAttribute('aria-pressed','true');
          }catch(e){
            // fallback to WebAudio
            startWebAudio(); playing=true; el.setAttribute('aria-pressed','true');
          }
        } else {
          startWebAudio(); playing=true; el.setAttribute('aria-pressed','true');
        }
      }

      el.addEventListener('click', toggle);
      el.addEventListener('keydown', (e)=>{ if(e.key==='Enter' || e.key===' ') { e.preventDefault(); toggle(); } });
    })();

    // RSVP / small micro interaction
    document.getElementById('rsvp').addEventListener('click', ()=>{
      const btn = document.getElementById('rsvp');
      btn.textContent = 'Requested'; btn.disabled=true; btn.style.opacity=0.95;
    });

    // Hidden terminal: open with backtick (`) or Ctrl+Shift+N
    (function(){
      const terminal = document.getElementById('terminal');
      const termInput = document.getElementById('termInput');
      const termContent = document.getElementById('termContent');
      let open = false;

      function showTerminal(){ terminal.style.display='block'; terminal.setAttribute('aria-hidden','false'); open=true; termInput.focus(); }
      function hideTerminal(){ terminal.style.display='none'; terminal.setAttribute('aria-hidden','true'); open=false; }

      window.addEventListener('keydown', (e)=>{
        if(e.key === '`' && !e.metaKey && !e.ctrlKey){
          if(open) hideTerminal(); else showTerminal(); e.preventDefault();
        }
        if(e.ctrlKey && e.shiftKey && e.key.toLowerCase()==='n'){
          e.preventDefault(); if(open) hideTerminal(); else showTerminal();
        }
        if(e.key==='Escape' && open){ hideTerminal(); }
      });

      // simple command handler
      termInput.addEventListener('keydown', (e)=>{
        if(e.key==='Enter'){
          const v = termInput.value.trim();
          if(!v){ termContent.textContent += '\n> '; termInput.value=''; return; }
          termContent.textContent += '\n$ ' + v + '\n';
          handleCmd(v.toLowerCase());
          termInput.value='';
          termContent.scrollTop = termContent.scrollHeight;
        }
      });

      function handleCmd(cmd){
        if(cmd === 'help'){
          termContent.textContent += 'commands:\n help — show this list\n status — dojo status\n kata — show a random kata\n clear — clear the console\n exit — close terminal\n';
        } else if(cmd === 'status'){
          termContent.textContent += 'dojo: active\ncapacity: restricted\nmission: refine craft\n';
        } else if(cmd === 'kata'){
          const kata = ['Refactor sprint: 30m', 'Pair kata: 45m', 'Silent debugging: 20m', 'One-line TDD: 25m'];
          termContent.textContent += kata[Math.floor(Math.random()*kata.length)] + '\n';
        } else if(cmd === 'clear'){
          termContent.textContent = '> ';
        } else if(cmd === 'exit'){
          hideTerminal();
        } else {
          termContent.textContent += 'command not found: ' + cmd + '\n';
        }
      }
    })();

    // tiny accessibility: focus outlines
    document.addEventListener('keydown', (e)=>{ if(e.key==='Tab') document.body.classList.add('show-focus'); });
  </script>
</body>
</html>
