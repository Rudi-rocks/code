<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Code × Ninja 10</title>
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@600;800&family=Inter:wght@400;700&display=swap" rel="stylesheet">
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      font-family: 'Inter', sans-serif;
      background: linear-gradient(135deg, #0f0f0f, #1a1a1a);
      background-attachment: fixed;
      overflow-x: hidden;
    }
    .glass {
      backdrop-filter: blur(14px);
      background: rgba(255, 255, 255, 0.04);
      border: 1px solid rgba(255, 255, 255, 0.08);
      box-shadow: 0 0 30px rgba(0, 255, 255, 0.1);
    }
    .glow {
      text-shadow: 0 0 10px #00ffff, 0 0 30px #00ffff;
    }
    .katana {
      animation: slash 1.2s ease-in-out forwards;
      transform-origin: center;
    }
    @keyframes slash {
      0% { transform: scale(0) rotate(0deg); opacity: 0; }
      50% { transform: scale(1.2) rotate(30deg); opacity: 1; }
      100% { transform: scale(1) rotate(45deg); opacity: 1; }
    }
    .terminal {
      display: none;
      position: fixed;
      bottom: 20px;
      left: 20px;
      background: #111;
      color: #0f0;
      padding: 20px;
      font-family: monospace;
      border: 2px solid #0f0;
      z-index: 50;
      white-space: pre-line;
    }
    .qr-glow:hover {
      filter: drop-shadow(0 0 10px #00ffff);
      transform: scale(1.05);
    }
    .parallax {
      background-image: url('https://images.unsplash.com/photo-1607083206173-3e4f1e7e3f2a?ixlib=rb-4.0.3&auto=format&fit=crop&w=1920&q=80');
      background-size: cover;
      background-position: center;
      background-attachment: fixed;
    }
  </style>
</head>
<body class="text-white parallax relative">

  <!-- Background Audio -->
  <audio id="bg-audio" loop>
    <source src="https://files.catbox.moe/9gk3xj.mp3" type="audio/mpeg">
  </audio>

  <!-- Audio Toggle -->
  <button onclick="toggleAudio()" class="absolute top-6 right-6 bg-cyan-700 hover:bg-cyan-800 px-4 py-2 rounded-full text-sm font-bold shadow-lg z-10">
    🔊 Toggle Beats
  </button>

  <!-- Hero Section -->
  <section class="flex flex-col items-center justify-center min-h-screen px-6 text-center relative z-10">
    <h1 class="text-6xl font-bold text-cyan-400 glow mb-4 tracking-wide font-orbitron">Code × Ninja 10</h1>
    <p class="text-xl text-gray-300 max-w-xl mb-6 italic">Precision. Power. Discipline. The ultimate coding dojo experience.</p>

    <!-- Katana SVG Animation -->
    <svg class="katana w-16 h-16 text-cyan-400 mb-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
      <path d="M3 3l18 18M21 3L3 21" />
    </svg>

    <!-- Glass Card -->
    <div class="glass p-6 rounded-xl shadow-xl max-w-md">
      <h2 class="text-2xl font-semibold text-cyan-300 mb-4">🗓️ Event Details</h2>
      <ul class="text-left space-y-2 text-gray-200">
        <li><strong>Date:</strong> October 10, 2025</li>
        <li><strong>Time:</strong> 6 PM – 9 PM</li>
        <li><strong>Venue:</strong> SRM IST – Paari G Block</li>
        <li><strong>Theme:</strong> Code. Combat. Clarity.</li>
      </ul>
    </div>

    <!-- CTA Button -->
    <a href="#" class="mt-10 px-8 py-3 bg-cyan-600 hover:bg-cyan-700 rounded-full text-white font-bold transition transform hover:scale-105 shadow-lg">Enter the Dojo</a>

    <!-- QR Code -->
    <img src="https://api.qrserver.com/v1/create-qr-code/?size=120x120&data=https://rudi-rocks.github.io/code-x-ninja-10" alt="QR Code" class="mt-8 opacity-80 transition qr-glow" />

    <!-- Terminal Easter Egg -->
    <div id="terminal" class="terminal">
      <p id="typed-text"></p>
    </div>
  </section>

  <!-- Scripts -->
  <script>
    const audio = document.getElementById('bg-audio');
    function toggleAudio() {
      audio.muted = !audio.muted;
    }

    document.addEventListener('keydown', function(e) {
      if (e.ctrlKey && e.key === 'k') {
        const terminal = document.getElementById('terminal');
        const typedText = document.getElementById('typed-text');
        terminal.style.display = terminal.style.display === 'none' ? 'block' : 'none';
        if (terminal.style.display === 'block') {
          typedText.innerText = '';
          const message = "Welcome, Ninja.\nYour mind is sharp.\nYour code is sharper.\n– Rudi";
          let i = 0;
          const type = () => {
            if (i < message.length) {
              typedText.innerText += message[i];
              i++;
              setTimeout(type, 50);
            }
          };
          type();
        }
      }
    });
  </script>
</body>
</html>
