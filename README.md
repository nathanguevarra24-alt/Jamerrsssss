# Jamerrsssss
# Jamerrsssss
<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>James Nathanael M. Guevarra | Cosmic Portfolio & Lab Observatory</title>
  <meta name="description" content="Astronomy-themed personal portfolio and custom laboratory showcase of James Nathanael M. Guevarra." />

  <!-- Google Fonts: Space Grotesk, Inter, and JetBrains Mono -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500;600&family=Space+Grotesk:wght@500;600;700&display=swap" rel="stylesheet">

  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            sans: ['Inter', 'sans-serif'],
            display: ['Space Grotesk', 'sans-serif'],
            mono: ['JetBrains Mono', 'monospace'],
          },
          colors: {
            void: '#03050c',
            nebula: '#0a0f24',
            stardust: '#141c3a',
            pulsar: '#38bdf8',
            supernova: '#c084fc',
            solar: '#fbbf24',
          },
          animation: {
            'spin-slow': 'spin 28s linear infinite',
            'spin-reverse-slower': 'spin-reverse 42s linear infinite',
            'float': 'float 6s ease-in-out infinite',
            'pulse-glow': 'pulseGlow 4s ease-in-out infinite',
          },
          keyframes: {
            'spin-reverse': {
              '0%': { transform: 'rotate(360deg)' },
              '100%': { transform: 'rotate(0deg)' },
            },
            float: {
              '0%, 100%': { transform: 'translateY(0px)' },
              '50%': { transform: 'translateY(-14px)' },
            },
            pulseGlow: {
              '0%, 100%': { opacity: '0.55', transform: 'scale(1)' },
              '50%': { opacity: '0.9', transform: 'scale(1.05)' },
            }
          }
        }
      }
    };
  </script>

  <style>
    /* Custom Cosmic Scrollbar & Glassmorphism Utilities */
    body {
      background-color: #03050c;
      color: #e2e8f0;
      overflow-x: hidden;
    }

    ::-webkit-scrollbar {
      width: 8px;
    }
    ::-webkit-scrollbar-track {
      background: #03050c;
    }
    ::-webkit-scrollbar-thumb {
      background: linear-gradient(180deg, #38bdf8, #a855f7);
      border-radius: 9999px;
    }

    /* Glassmorphic Card Styling with Nebula Border Hover */
    .cosmic-card {
      background: rgba(13, 19, 43, 0.62);
      backdrop-filter: blur(14px);
      -webkit-backdrop-filter: blur(14px);
      border: 1px solid rgba(148, 163, 184, 0.14);
      transition: transform 0.35s cubic-bezier(0.22, 1, 0.36, 1),
                  border-color 0.35s ease,
                  box-shadow 0.35s ease;
    }

    .cosmic-card:hover {
      border-color: rgba(56, 189, 248, 0.45);
      box-shadow: 0 18px 40px -15px rgba(56, 189, 248, 0.22),
                  0 0 25px -5px rgba(192, 132, 252, 0.18);
    }

    /* Edit Mode Highlighting */
    .edit-mode-active [contenteditable="true"] {
      outline: 1px dashed rgba(251, 191, 36, 0.75);
      background: rgba(251, 191, 36, 0.06);
      border-radius: 0.375rem;
      padding: 2px 6px;
      cursor: text;
      transition: all 0.2s ease;
    }
    .edit-mode-active [contenteditable="true"]:focus {
      outline: 2px solid #fbbf24;
      background: rgba(251, 191, 36, 0.12);
    }

    /* Scroll Reveal Utility */
    .reveal {
      opacity: 0;
      transform: translateY(24px);
      transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1),
                  transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }

    /* Audio Equalizer Bars */
    @keyframes eqBar {
      0%, 100% { height: 4px; }
      50% { height: 16px; }
    }
    .eq-playing .eq-bar-1 { animation: eqBar 0.8s ease-in-out infinite; }
    .eq-playing .eq-bar-2 { animation: eqBar 0.55s ease-in-out infinite 0.15s; }
    .eq-playing .eq-bar-3 { animation: eqBar 0.95s ease-in-out infinite 0.3s; }
    .eq-playing .eq-bar-4 { animation: eqBar 0.65s ease-in-out infinite 0.1s; }
  </style>
</head>
<body class="antialiased selection:bg-sky-400/30 selection:text-sky-200">

  <!-- Interactive Deep Space Canvas Background -->
  <canvas id="cosmos-canvas" class="fixed inset-0 w-full h-full pointer-events-none z-0"></canvas>

  <!-- Ambient Nebula Radial Glows -->
  <div class="fixed inset-0 pointer-events-none z-0 overflow-hidden">
    <div class="absolute -top-36 -left-36 w-[32rem] h-[32rem] rounded-full bg-purple-700/15 blur-[130px] animate-pulse-glow"></div>
    <div class="absolute top-1/3 -right-32 w-[30rem] h-[30rem] rounded-full bg-sky-600/15 blur-[130px] animate-pulse-glow" style="animation-delay: 2s;"></div>
    <div class="absolute bottom-0 left-1/3 w-[28rem] h-[28rem] rounded-full bg-indigo-700/15 blur-[140px]"></div>
  </div>

  <!-- Toast Notification Banner (Replaces alert/confirm) -->
  <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>

  <!-- Glassmorphic Sticky Header / Navigation -->
  <header class="fixed top-0 inset-x-0 z-40 border-b border-slate-800/70 bg-[#03050c]/75 backdrop-blur-xl">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between gap-4">
      <!-- Brand / Callsign -->
      <a href="#hero" class="flex items-center gap-3 group">
        <div class="relative w-9 h-9 rounded-xl bg-gradient-to-br from-sky-400/20 to-purple-500/20 border border-sky-400/40 flex items-center justify-center shadow-inner group-hover:scale-105 transition-transform">
          <span class="w-2.5 h-2.5 rounded-full bg-sky-400 shadow-[0_0_12px_#38bdf8]"></span>
          <span class="absolute inset-1 rounded-lg border border-purple-400/40 animate-spin-slow"></span>
        </div>
        <div class="flex flex-col">
          <span class="font-display font-bold text-sm sm:text-base tracking-wide text-slate-100 group-hover:text-sky-300 transition-colors">
            J.N.M. GUEVARRA
          </span>
          <span class="font-mono text-[10px] tracking-widest uppercase text-sky-400/80">
            Observatory // Portfolio
          </span>
        </div>
      </a>

      <!-- Desktop Nav Links -->
      <nav class="hidden md:flex items-center gap-7 text-sm font-medium text-slate-300">
        <a href="#about" class="hover:text-sky-400 transition-colors">Mission Log</a>
        <a href="#lab-tasks" class="hover:text-sky-400 transition-colors flex items-center gap-1.5">
          <span>Lab Tasks</span>
          <span class="px-1.5 py-0.5 text-[10px] font-mono rounded-full bg-purple-500/20 text-purple-300 border border-purple-400/30">Custom</span>
        </a>
        <a href="#telemetry" class="hover:text-sky-400 transition-colors">Telemetry</a>
        <a href="#contact" class="hover:text-sky-400 transition-colors">Comms</a>
      </nav>

      <!-- Ambient Space Music Synth Control & Mobile Menu Button -->
      <div class="flex items-center gap-2 sm:gap-3">
        <!-- Web Audio API Ambient Synth Controller -->
        <div class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-slate-900/90 border border-slate-700/70 shadow-lg">
          <button id="audio-toggle-btn" type="button" aria-label="Toggle Cosmic Ambient Audio"
            class="flex items-center gap-2 text-xs font-mono text-sky-300 hover:text-white transition-colors focus:outline-none">
            <span id="audio-icon-play" class="flex items-center justify-center w-5 h-5 rounded-full bg-sky-500/20 text-sky-400">
              <svg class="w-3 h-3 fill-current" viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg>
            </span>
            <span id="audio-icon-pause" class="hidden items-center justify-center w-5 h-5 rounded-full bg-purple-500/25 text-purple-300">
              <svg class="w-3 h-3 fill-current" viewBox="0 0 24 24"><path d="M6 19h4V5H6v14zm8-14v14h4V5h-4z"/></svg>
            </span>
            <span class="hidden sm:inline" id="audio-status-text">Cosmic Audio</span>
          </button>

          <!-- Animated Equalizer -->
          <div id="audio-eq" class="flex items-end gap-0.5 h-4 w-4 px-0.5">
            <span class="eq-bar-1 w-0.5 h-1 bg-sky-400 rounded-full"></span>
            <span class="eq-bar-2 w-0.5 h-2 bg-purple-400 rounded-full"></span>
            <span class="eq-bar-3 w-0.5 h-1.5 bg-amber-300 rounded-full"></span>
            <span class="eq-bar-4 w-0.5 h-1 bg-sky-400 rounded-full"></span>
          </div>

          <!-- Volume Slider -->
          <input id="audio-volume" type="range" min="0" max="1" step="0.05" value="0.35" aria-label="Ambient Volume"
            class="hidden lg:block w-16 h-1 bg-slate-700 rounded-lg appearance-none cursor-pointer accent-sky-400" />
        </div>

        <!-- Mobile Menu Toggle -->
        <button id="mobile-menu-btn" type="button" aria-label="Toggle Menu"
          class="md:hidden p-2 rounded-xl border border-slate-700/80 bg-slate-900/80 text-slate-300 hover:text-sky-400">
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"/>
          </svg>
        </button>
      </div>
    </div>

    <!-- Mobile Dropdown Navigation -->
    <div id="mobile-menu" class="hidden md:hidden border-t border-slate-800/80 bg-[#050816]/95 backdrop-blur-xl px-4 py-4 space-y-2">
      <a href="#about" class="block px-3 py-2 rounded-lg text-sm font-medium text-slate-300 hover:bg-slate-800/70 hover:text-sky-400">Mission Log</a>
      <a href="#lab-tasks" class="block px-3 py-2 rounded-lg text-sm font-medium text-slate-300 hover:bg-slate-800/70 hover:text-sky-400">Custom Lab Tasks</a>
      <a href="#telemetry" class="block px-3 py-2 rounded-lg text-sm font-medium text-slate-300 hover:bg-slate-800/70 hover:text-sky-400">Telemetry & Skills</a>
      <a href="#contact" class="block px-3 py-2 rounded-lg text-sm font-medium text-slate-300 hover:bg-slate-800/70 hover:text-sky-400">Comms Channel</a>
    </div>
  </header>

  <!-- Main Content -->
  <main class="relative z-10 pt-24 pb-20">

    <!-- HERO SECTION -->
    <section id="hero" class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pt-8 pb-20 lg:py-24">
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
        <!-- Hero Text -->
        <div class="lg:col-span-7 space-y-6 text-center lg:text-left">
          <div class="inline-flex items-center gap-2.5 px-3.5 py-1.5 rounded-full bg-sky-500/10 border border-sky-400/30 text-sky-300 text-xs font-mono tracking-wider uppercase">
            <span class="w-2 h-2 rounded-full bg-amber-400 animate-ping"></span>
            <span>Deep Space Computing &amp; Laboratory Archive</span>
          </div>

          <h1 class="font-display text-4xl sm:text-5xl lg:text-6xl font-bold tracking-tight text-white leading-[1.12]">
            James Nathanael
            <span class="block mt-1 bg-gradient-to-r from-sky-400 via-purple-400 to-amber-300 bg-clip-text text-transparent">
              M. Guevarra
            </span>
          </h1>

          <p id="hero-bio-editable" class="text-base sm:text-lg text-slate-300/90 max-w-2xl mx-auto lg:mx-0 leading-relaxed">
            Exploring the cosmos through code, computational modeling, and custom laboratory experiments. Welcome to my interactive orbital observatory—housing software prototypes, telemetry experiments, and celestial simulations.
          </p>

          <div class="flex flex-wrap items-center justify-center lg:justify-start gap-4 pt-2">
            <a href="#lab-tasks"
              class="px-6 py-3.5 rounded-xl font-semibold text-sm text-slate-950 bg-gradient-to-r from-sky-400 via-cyan-300 to-purple-400 hover:brightness-110 shadow-[0_0_25px_rgba(56,189,248,0.45)] transition-all transform hover:-translate-y-0.5">
              Explore Lab Tasks
            </a>
            <a href="#contact"
              class="px-6 py-3.5 rounded-xl font-semibold text-sm text-slate-200 bg-slate-900/75 border border-slate-700 hover:border-purple-400/60 hover:text-white transition-all transform hover:-translate-y-0.5">
              Establish Comms
            </a>
          </div>

          <!-- Quick Telemetry Coordinates -->
          <div class="pt-4 grid grid-cols-3 gap-4 max-w-md mx-auto lg:mx-0 border-t border-slate-800/80 font-mono text-xs">
            <div>
              <span class="block text-slate-500">SECTOR</span>
              <span class="text-sky-300">SOL-III // EARTH</span>
            </div>
            <div>
              <span class="block text-slate-500">STATUS</span>
              <span class="text-emerald-400">● ONLINE</span>
            </div>
            <div>
              <span class="block text-slate-500">ARCHIVE</span>
              <span class="text-purple-300">GITHUB PAGES</span>
            </div>
          </div>
        </div>

        <!-- Hero Visual: Custom Animated Planetary Orrery SVG -->
        <div class="lg:col-span-5 flex justify-center">
          <div class="relative w-72 h-72 sm:w-96 sm:h-96 flex items-center justify-center animate-float">
            <!-- Outer Nebula Halo -->
            <div class="absolute inset-4 rounded-full bg-gradient-to-tr from-sky-500/20 via-purple-500/20 to-amber-400/20 blur-2xl"></div>

            <!-- Interactive SVG Orrery -->
            <svg viewBox="0 0 400 400" class="w-full h-full drop-shadow-[0_0_30px_rgba(56,189,248,0.28)]">
              <defs>
                <radialGradient id="planetCore" cx="35%" cy="35%" r="65%">
                  <stop offset="0%" stop-color="#7dd3fc" />
                  <stop offset="45%" stop-color="#3b82f6" />
                  <stop offset="85%" stop-color="#311042" />
                  <stop offset="100%" stop-color="#090d1f" />
                </radialGradient>
                <linearGradient id="ringGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                  <stop offset="0%" stop-color="#38bdf8" stop-opacity="0.85" />
                  <stop offset="50%" stop-color="#c084fc" stop-opacity="0.55" />
                  <stop offset="100%" stop-color="#fbbf24" stop-opacity="0.85" />
                </linearGradient>
              </defs>

              <!-- Outer Dashed Orbital Path -->
              <circle cx="200" cy="200" r="178" fill="none" stroke="rgba(148,163,184,0.22)" stroke-width="1" stroke-dasharray="4 6" class="origin-center animate-spin-slow" />
              <!-- Middle Orbital Ring -->
              <circle cx="200" cy="200" r="134" fill="none" stroke="rgba(56,189,248,0.3)" stroke-width="1.2" class="origin-center animate-spin-reverse-slower" />

              <!-- Orbiting Satellite 1 -->
              <g class="origin-center animate-spin-slow">
                <circle cx="200" cy="22" r="6" fill="#fbbf24" />
                <circle cx="200" cy="22" r="12" fill="none" stroke="#fbbf24" stroke-opacity="0.4" stroke-width="1" />
              </g>

              <!-- Orbiting Satellite 2 -->
              <g class="origin-center animate-spin-reverse-slower">
                <circle cx="334" cy="200" r="5" fill="#c084fc" />
              </g>

              <!-- Tilted Planetary Ring (Back Arc) -->
              <ellipse cx="200" cy="200" rx="145" ry="42" transform="rotate(-22 200 200)" fill="none" stroke="url(#ringGrad)" stroke-width="6" stroke-opacity="0.45" />

              <!-- Central Exoplanet Sphere -->
              <circle cx="200" cy="200" r="68" fill="url(#planetCore)" />
              <!-- Atmospheric Rim Light -->
              <circle cx="200" cy="200" r="68" fill="none" stroke="#7dd3fc" stroke-width="1.5" stroke-opacity="0.6" />

              <!-- Tilted Planetary Ring (Front Foreground Arc) -->
              <path d="M 66 254 A 145 42 -22 0 0 334 146" fill="none" stroke="url(#ringGrad)" stroke-width="7" stroke-linecap="round" />

              <!-- Star Glints -->
              <path d="M85 85 L88 93 L96 96 L88 99 L85 107 L82 99 L74 96 L82 93 Z" fill="#fef08a" opacity="0.85" />
              <path d="M320 305 L322 311 L328 313 L322 315 L320 321 L318 315 L312 313 L318 311 Z" fill="#7dd3fc" opacity="0.85" />
            </svg>
          </div>
        </div>
      </div>
    </section>

    <!-- ABOUT / MISSION LOG SECTION -->
    <section id="about" class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16 reveal">
      <div class="cosmic-card rounded-3xl p-6 sm:p-10 relative overflow-hidden">
        <div class="flex flex-col lg:flex-row gap-8 lg:items-center justify-between">
          <div class="space-y-4 max-w-3xl">
            <div class="inline-flex items-center gap-2 text-xs font-mono uppercase tracking-widest text-purple-300">
              <span>// 01. MISSION LOG</span>
            </div>
            <h2 class="font-display text-2xl sm:text-3xl font-bold text-white">
              Charting Curiosity Across Code &amp; Cosmos
            </h2>
            <p class="text-slate-300 leading-relaxed text-sm sm:text-base">
              I am <strong class="text-sky-300 font-semibold">James Nathanael M. Guevarra</strong>—passionate about bridging structured laboratory experimentation with modern software development. Just as astronomers map distant nebulae through patient observation and precision instruments, I build clean, resilient projects and document every discovery in my lab logs below.
            </p>
          </div>

          <!-- Highlight Metrics -->
          <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-1 gap-3 min-w-[230px]">
            <div class="p-4 rounded-2xl bg-slate-950/70 border border-slate-800/90">
              <div id="stat-lab-count" class="font-display text-2xl font-bold text-sky-400">04</div>
              <div class="text-xs font-mono text-slate-400 uppercase mt-0.5">Active Lab Tasks</div>
            </div>
            <div class="p-4 rounded-2xl bg-slate-950/70 border border-slate-800/90">
              <div class="font-display text-2xl font-bold text-purple-400">100%</div>
              <div class="text-xs font-mono text-slate-400 uppercase mt-0.5">Static &amp; GitHub Ready</div>
            </div>
            <div class="p-4 rounded-2xl bg-slate-950/70 border border-slate-800/90 col-span-2 sm:col-span-1">
              <div class="font-display text-2xl font-bold text-amber-300">∞</div>
              <div class="text-xs font-mono text-slate-400 uppercase mt-0.5">Curiosity Index</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CUSTOM EDITABLE LAB TASKS SECTION -->
    <section id="lab-tasks" class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16 reveal">
      <!-- Section Header & Interactive Editor Toolbar -->
      <div class="flex flex-col lg:flex-row lg:items-end justify-between gap-6 mb-10">
        <div class="space-y-2">
          <div class="inline-flex items-center gap-2 text-xs font-mono uppercase tracking-widest text-sky-400">
            <span>// 02. LABORATORY OBSERVATORY</span>
          </div>
          <h2 class="font-display text-3xl sm:text-4xl font-bold text-white">
            Custom Lab Tasks &amp; Experiments
          </h2>
          <p class="text-sm sm:text-base text-slate-400 max-w-2xl">
            Placeholder cards ready for your custom coursework, scripts, and experiments. Toggle <span class="text-amber-300 font-medium">Edit Mode</span> to click and customize any card text, tags, or links directly in your browser.
          </p>
        </div>

        <!-- Toolbar Controls -->
        <div class="flex flex-wrap items-center gap-2.5">
          <button id="toggle-edit-btn" type="button"
            class="inline-flex items-center gap-2 px-4 py-2.5 rounded-xl text-xs sm:text-sm font-semibold bg-amber-400/15 text-amber-300 border border-amber-400/40 hover:bg-amber-400/25 transition-all">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"/>
            </svg>
            <span id="edit-btn-label">Enable Edit Mode</span>
          </button>

          <button id="add-lab-btn" type="button"
            class="inline-flex items-center gap-1.5 px-4 py-2.5 rounded-xl text-xs sm:text-sm font-semibold bg-sky-500/15 text-sky-300 border border-sky-400/40 hover:bg-sky-500/25 transition-all">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/>
            </svg>
            <span>Add Lab Card</span>
          </button>

          <button id="export-html-btn" type="button" title="Download updated index.html for GitHub Pages"
            class="inline-flex items-center gap-1.5 px-4 py-2.5 rounded-xl text-xs sm:text-sm font-semibold bg-purple-500/15 text-purple-300 border border-purple-400/40 hover:bg-purple-500/25 transition-all">
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"/>
            </svg>
            <span>Export HTML</span>
          </button>

          <button id="reset-labs-btn" type="button" title="Restore default placeholder lab cards"
            class="inline-flex items-center gap-1.5 px-3 py-2.5 rounded-xl text-xs font-mono text-slate-400 bg-slate-900/80 border border-slate-700/80 hover:text-rose-300 hover:border-rose-400/40 transition-all">
            <span>Reset</span>
          </button>
        </div>
      </div>

      <!-- Edit Mode Helper Banner -->
      <div id="edit-mode-banner" class="hidden mb-6 px-4 py-3 rounded-2xl bg-amber-400/10 border border-amber-400/35 flex flex-col sm:flex-row sm:items-center justify-between gap-2 text-xs sm:text-sm text-amber-200">
        <div class="flex items-center gap-2">
          <span class="w-2 h-2 rounded-full bg-amber-400 animate-ping"></span>
          <span><strong>Edit Mode Active:</strong> Click any card code, title, description, tags, or URLs to edit inline. Changes save automatically in your browser.</span>
        </div>
        <span class="font-mono text-[11px] text-amber-300/80">Tip: Use "Export HTML" to save a permanent file for GitHub!</span>
      </div>

      <!-- Lab Cards Grid Container -->
      <div id="lab-cards-grid" class="grid grid-cols-1 md:grid-cols-2 gap-6 lg:gap-8">
        <!-- Cards rendered dynamically via JS with default astronomy/computing placeholders -->
      </div>
    </section>

    <!-- TELEMETRY & SKILLS CONSTELLATION SECTION -->
    <section id="telemetry" class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16 reveal">
      <div class="space-y-2 mb-10">
        <div class="inline-flex items-center gap-2 text-xs font-mono uppercase tracking-widest text-purple-300">
          <span>// 03. INSTRUMENTATION &amp; TELEMETRY</span>
        </div>
        <h2 class="font-display text-3xl sm:text-4xl font-bold text-white">
          Technical Constellation
        </h2>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        <!-- Skill Cluster 1 -->
        <div class="cosmic-card rounded-2xl p-6 space-y-4">
          <div class="w-11 h-11 rounded-xl bg-sky-500/15 border border-sky-400/30 flex items-center justify-center text-sky-400">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.8" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"/>
            </svg>
          </div>
          <h3 class="font-display text-lg font-bold text-white">Web &amp; Frontend</h3>
          <div class="flex flex-wrap gap-2 text-xs font-mono">
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-sky-300">HTML5 / Canvas</span>
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-sky-300">Tailwind CSS</span>
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-sky-300">JavaScript ES6+</span>
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-sky-300">Web Audio API</span>
          </div>
        </div>

        <!-- Skill Cluster 2 -->
        <div class="cosmic-card rounded-2xl p-6 space-y-4">
          <div class="w-11 h-11 rounded-xl bg-purple-500/15 border border-purple-400/30 flex items-center justify-center text-purple-400">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.8" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
            </svg>
          </div>
          <h3 class="font-display text-lg font-bold text-white">Computation &amp; Labs</h3>
          <div class="flex flex-wrap gap-2 text-xs font-mono">
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-purple-300">Python</span>
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-purple-300">Data Visualization</span>
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-purple-300">Algorithms</span>
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-purple-300">Simulation</span>
          </div>
        </div>

        <!-- Skill Cluster 3 -->
        <div class="cosmic-card rounded-2xl p-6 space-y-4">
          <div class="w-11 h-11 rounded-xl bg-amber-500/15 border border-amber-400/30 flex items-center justify-center text-amber-300">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.8" d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z"/>
            </svg>
          </div>
          <h3 class="font-display text-lg font-bold text-white">Astronomy Focus</h3>
          <div class="flex flex-wrap gap-2 text-xs font-mono">
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-amber-200">Orbital Mechanics</span>
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-amber-200">Telemetry Logs</span>
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-amber-200">Astrophotography</span>
          </div>
        </div>

        <!-- Skill Cluster 4 -->
        <div class="cosmic-card rounded-2xl p-6 space-y-4">
          <div class="w-11 h-11 rounded-xl bg-emerald-500/15 border border-emerald-400/30 flex items-center justify-center text-emerald-400">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.8" d="M8 9l3 3-3 3m5 0h3M5 20h14a2 2 0 002-2V6a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"/>
            </svg>
          </div>
          <h3 class="font-display text-lg font-bold text-white">Workflow &amp; DevOps</h3>
          <div class="flex flex-wrap gap-2 text-xs font-mono">
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-emerald-300">Git &amp; GitHub</span>
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-emerald-300">GitHub Pages</span>
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-emerald-300">Linux CLI</span>
            <span class="px-2.5 py-1 rounded-lg bg-slate-900/90 border border-slate-700/80 text-emerald-300">Documentation</span>
          </div>
        </div>
      </div>
    </section>

    <!-- CONTACT / COMMS SECTION -->
    <section id="contact" class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16 reveal">
      <div class="cosmic-card rounded-3xl p-6 sm:p-10 lg:p-12">
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-10">
          <!-- Contact Info -->
          <div class="lg:col-span-5 space-y-6">
            <div class="inline-flex items-center gap-2 text-xs font-mono uppercase tracking-widest text-sky-400">
              <span>// 04. SUBSPACE COMMS</span>
            </div>
            <h2 class="font-display text-3xl font-bold text-white">
              Transmit a Signal
            </h2>
            <p class="text-sm sm:text-base text-slate-300 leading-relaxed">
              Interested in collaborating on lab experiments, software projects, or astronomical simulations? Reach out through any of the channels below.
            </p>

            <div class="space-y-3 pt-2 font-mono text-xs sm:text-sm">
              <div class="flex items-center justify-between p-3.5 rounded-xl bg-slate-950/75 border border-slate-800">
                <span class="text-slate-400">EMAIL</span>
                <button type="button" onclick="copyText('james.guevarra@example.com')" class="text-sky-300 hover:text-white flex items-center gap-1.5">
                  <span>james.guevarra@example.com</span>
                  <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"/></svg>
                </button>
              </div>
              <a href="https://github.com" target="_blank" rel="noopener noreferrer"
                class="flex items-center justify-between p-3.5 rounded-xl bg-slate-950/75 border border-slate-800 hover:border-purple-400/50 transition-colors">
                <span class="text-slate-400">GITHUB</span>
                <span class="text-purple-300">@james-guevarra ↗</span>
              </a>
              <a href="https://linkedin.com" target="_blank" rel="noopener noreferrer"
                class="flex items-center justify-between p-3.5 rounded-xl bg-slate-950/75 border border-slate-800 hover:border-sky-400/50 transition-colors">
                <span class="text-slate-400">LINKEDIN</span>
                <span class="text-amber-300">James Nathanael M. Guevarra ↗</span>
              </a>
            </div>
          </div>

          <!-- Interactive Signal Form -->
          <form id="comms-form" class="lg:col-span-7 space-y-4">
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
              <div>
                <label for="sender-name" class="block text-xs font-mono uppercase text-slate-400 mb-1.5">Sender Callsign / Name</label>
                <input id="sender-name" type="text" required placeholder="e.g., Carl Sagan"
                  class="w-full px-4 py-3 rounded-xl bg-slate-950/80 border border-slate-800 text-slate-200 placeholder-slate-600 focus:outline-none focus:border-sky-400 transition-colors text-sm" />
              </div>
              <div>
                <label for="sender-email" class="block text-xs font-mono uppercase text-slate-400 mb-1.5">Return Frequency / Email</label>
                <input id="sender-email" type="email" required placeholder="observer@cosmos.org"
                  class="w-full px-4 py-3 rounded-xl bg-slate-950/80 border border-slate-800 text-slate-200 placeholder-slate-600 focus:outline-none focus:border-sky-400 transition-colors text-sm" />
              </div>
            </div>

            <div>
              <label for="sender-message" class="block text-xs font-mono uppercase text-slate-400 mb-1.5">Transmission Payload</label>
              <textarea id="sender-message" rows="4" required placeholder="Write your message, feedback, or lab collaboration inquiry..."
                class="w-full px-4 py-3 rounded-xl bg-slate-950/80 border border-slate-800 text-slate-200 placeholder-slate-600 focus:outline-none focus:border-purple-400 transition-colors text-sm"></textarea>
            </div>

            <button type="submit"
              class="w-full sm:w-auto px-7 py-3.5 rounded-xl font-semibold text-sm text-slate-950 bg-gradient-to-r from-sky-400 to-purple-400 hover:brightness-110 shadow-[0_0_20px_rgba(56,189,248,0.35)] transition-all">
              Send Transmission
            </button>
          </form>
        </div>
      </div>
    </section>
  </main>

  <!-- Footer -->
  <footer class="relative z-10 border-t border-slate-800/80 bg-[#03050c]/85 backdrop-blur-md py-8">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col sm:flex-row items-center justify-between gap-4 text-xs font-mono text-slate-400">
      <div>
        &copy; <span id="current-year"></span> <span class="text-slate-200">James Nathanael M. Guevarra</span>. All rights reserved.
      </div>
      <div class="flex items-center gap-2 text-slate-500">
        <span>Built for GitHub Pages</span>
        <span>•</span>
        <span class="text-sky-400/80">Per Aspera Ad Astra</span>
      </div>
    </div>
  </footer>

  <!-- Interactive JavaScript Engine -->
  <script>
    // =========================================================================
    // 1. TOAST NOTIFICATION & CLIPBOARD UTILITIES (No alert() / confirm())
    // =========================================================================
    function showToast(message, type = 'info') {
      const container = document.getElementById('toast-container');
      const toast = document.createElement('div');
      const colors = {
        info: 'border-sky-400/50 bg-slate-900/95 text-sky-200',
        success: 'border-emerald-400/50 bg-slate-900/95 text-emerald-200',
        warning: 'border-amber-400/50 bg-slate-900/95 text-amber-200'
      };

      toast.className = `pointer-events-auto px-4 py-3 rounded-xl border backdrop-blur-xl shadow-2xl text-xs sm:text-sm font-medium flex items-center gap-2.5 transform translate-y-2 opacity-0 transition-all duration-300 ${colors[type] || colors.info}`;
      toast.innerHTML = `
        <span class="w-2 h-2 rounded-full ${type === 'success' ? 'bg-emerald-400' : type === 'warning' ? 'bg-amber-400' : 'bg-sky-400'}"></span>
        <span>${message}</span>
      `;
      container.appendChild(toast);

      requestAnimationFrame(() => {
        toast.classList.remove('translate-y-2', 'opacity-0');
      });

      setTimeout(() => {
        toast.classList.add('translate-y-2', 'opacity-0');
        setTimeout(() => toast.remove(), 300);
      }, 3400);
    }

    function copyText(text) {
      const tempInput = document.createElement('textarea');
      tempInput.value = text;
      document.body.appendChild(tempInput);
      tempInput.select();
      document.execCommand('copy');
      document.body.removeChild(tempInput);
      showToast(`Copied "${text}" to clipboard`, 'success');
    }

    // =========================================================================
    // 2. INTERACTIVE DEEP SPACE STARFIELD CANVAS (Twinkling Stars & Shooting Stars)
    // =========================================================================
    (function initCosmosCanvas() {
      const canvas = document.getElementById('cosmos-canvas');
      const ctx = canvas.getContext('2d');
      let width = 0;
      let height = 0;
      let stars = [];
      let shootingStars = [];
      let mouse = { x: 0, y: 0, targetX: 0, targetY: 0 };

      function resizeCanvas() {
        width = canvas.width = window.innerWidth;
        height = canvas.height = window.innerHeight;
        createStars();
      }

      function createStars() {
        const starCount = Math.min(Math.floor((width * height) / 6500), 260);
        const palette = ['#ffffff', '#bae6fd', '#e9d5ff', '#fef08a', '#7dd3fc'];
        stars = Array.from({ length: starCount }, () => ({
          x: Math.random() * width,
          y: Math.random() * height,
          radius: Math.random() * 1.6 + 0.35,
          alpha: Math.random() * 0.8 + 0.2,
          twinkleSpeed: (Math.random() * 0.02 + 0.005) * (Math.random() < 0.5 ? 1 : -1),
          depth: Math.random() * 0.6 + 0.15,
          color: palette[Math.floor(Math.random() * palette.length)]
        }));
      }

      function spawnShootingStar() {
        if (shootingStars.length > 2) return;
        shootingStars.push({
          x: Math.random() * width * 0.85,
          y: Math.random() * height * 0.4,
          len: Math.random() * 95 + 55,
          speed: Math.random() * 9 + 7,
          angle: Math.PI / 4 + (Math.random() * 0.2 - 0.1),
          life: 1.0
        });
      }

      window.addEventListener('mousemove', (e) => {
        mouse.targetX = (e.clientX - width / 2) * 0.03;
        mouse.targetY = (e.clientY - height / 2) * 0.03;
      }, { passive: true });

      window.addEventListener('resize', resizeCanvas);

      function render() {
        ctx.clearRect(0, 0, width, height);

        // Smooth mouse parallax interpolation
        mouse.x += (mouse.targetX - mouse.x) * 0.05;
        mouse.y += (mouse.targetY - mouse.y) * 0.05;

        // Draw stars
        for (const s of stars) {
          s.alpha += s.twinkleSpeed;
          if (s.alpha > 1 || s.alpha < 0.18) s.twinkleSpeed *= -1;

          const drawX = (s.x - mouse.x * s.depth + width) % width;
          const drawY = (s.y - mouse.y * s.depth + height) % height;

          ctx.beginPath();
          ctx.arc(drawX, drawY, s.radius, 0, Math.PI * 2);
          ctx.fillStyle = s.color;
          ctx.globalAlpha = Math.max(0.1, Math.min(1, s.alpha));
          ctx.fill();
        }

        // Occasional shooting star
        if (Math.random() < 0.006) spawnShootingStar();

        for (let i = shootingStars.length - 1; i >= 0; i--) {
          const st = shootingStars[i];
          st.x += Math.cos(st.angle) * st.speed;
          st.y += Math.sin(st.angle) * st.speed;
          st.life -= 0.018;

          if (st.life <= 0) {
            shootingStars.splice(i, 1);
            continue;
          }

          const tailX = st.x - Math.cos(st.angle) * st.len;
          const tailY = st.y - Math.sin(st.angle) * st.len;
          const grad = ctx.createLinearGradient(st.x, st.y, tailX, tailY);
          grad.addColorStop(0, `rgba(255, 255, 255, ${st.life})`);
          grad.addColorStop(0.4, `rgba(56, 189, 248, ${st.life * 0.6})`);
          grad.addColorStop(1, 'rgba(56, 189, 248, 0)');

          ctx.globalAlpha = 1;
          ctx.strokeStyle = grad;
          ctx.lineWidth = 1.8;
          ctx.beginPath();
          ctx.moveTo(st.x, st.y);
          ctx.lineTo(tailX, tailY);
          ctx.stroke();
        }

        ctx.globalAlpha = 1;
        requestAnimationFrame(render);
      }

      window.addEventListener('load', () => {
        resizeCanvas();
        render();
      });
    })();

    // =========================================================================
    // 3. WEB AUDIO API COSMIC AMBIENT SYNTHESIZER (Zero External Audio Files)
    // =========================================================================
    (function initSpaceAudioSynth() {
      const toggleBtn = document.getElementById('audio-toggle-btn');
      const iconPlay = document.getElementById('audio-icon-play');
      const iconPause = document.getElementById('audio-icon-pause');
      const statusText = document.getElementById('audio-status-text');
      const eqEl = document.getElementById('audio-eq');
      const volumeSlider = document.getElementById('audio-volume');

      let audioCtx = null;
      let masterGain = null;
      let isPlaying = false;
      let shimmerInterval = null;

      function setupSynth() {
        const AudioContext = window.AudioContext || window.webkitAudioContext;
        audioCtx = new AudioContext();

        masterGain = audioCtx.createGain();
        masterGain.gain.setValueAtTime(0.001, audioCtx.currentTime);

        // Warm Lowpass Filter for Deep Nebula Drone
        const filter = audioCtx.createBiquadFilter();
        filter.type = 'lowpass';
        filter.frequency.setValueAtTime(420, audioCtx.currentTime);
        filter.Q.setValueAtTime(2.5, audioCtx.currentTime);

        // Slow LFO modulating filter cutoff for cosmic breathing effect
        const lfo = audioCtx.createOscillator();
        const lfoGain = audioCtx.createGain();
        lfo.frequency.setValueAtTime(0.09, audioCtx.currentTime);
        lfoGain.gain.setValueAtTime(160, audioCtx.currentTime);
        lfo.connect(lfoGain);
        lfoGain.connect(filter.frequency);
        lfo.start();

        // Ethereal Harmonic Chord Pad (D minor 9 / cosmic fifths)
        const freqs = [73.42, 110.0, 146.83, 220.0, 329.63];
        freqs.forEach((freq, idx) => {
          const osc = audioCtx.createOscillator();
          const oscGain = audioCtx.createGain();
          osc.type = idx % 2 === 0 ? 'sine' : 'triangle';
          osc.frequency.setValueAtTime(freq, audioCtx.currentTime);
          osc.detune.setValueAtTime((idx - 2) * 4, audioCtx.currentTime);

          oscGain.gain.setValueAtTime(0.14 / freqs.length, audioCtx.currentTime);
          osc.connect(oscGain);
          oscGain.connect(filter);
          osc.start();
        });

        filter.connect(masterGain);
        masterGain.connect(audioCtx.destination);

        // Occasional gentle starlight bell chime
        const chimeNotes = [440, 523.25, 587.33, 659.25, 783.99, 880];
        shimmerInterval = setInterval(() => {
          if (!isPlaying || !audioCtx) return;
          const now = audioCtx.currentTime;
          const chimeOsc = audioCtx.createOscillator();
          const chimeGain = audioCtx.createGain();
          const note = chimeNotes[Math.floor(Math.random() * chimeNotes.length)];

          chimeOsc.type = 'sine';
          chimeOsc.frequency.setValueAtTime(note, now);

          chimeGain.gain.setValueAtTime(0.0001, now);
          chimeGain.gain.exponentialRampToValueAtTime(0.025, now + 0.6);
          chimeGain.gain.exponentialRampToValueAtTime(0.0001, now + 4.2);

          chimeOsc.connect(chimeGain);
          chimeGain.connect(masterGain);
          chimeOsc.start(now);
          chimeOsc.stop(now + 4.4);
        }, 4800);
      }

      toggleBtn.addEventListener('click', () => {
        if (!audioCtx) setupSynth();
        if (audioCtx.state === 'suspended') audioCtx.resume();

        isPlaying = !isPlaying;
        const targetVol = parseFloat(volumeSlider.value) || 0.35;
        const now = audioCtx.currentTime;

        if (isPlaying) {
          masterGain.gain.cancelScheduledValues(now);
          masterGain.gain.setTargetAtTime(targetVol, now, 0.8);
          iconPlay.classList.add('hidden');
          iconPause.classList.remove('hidden');
          iconPause.classList.add('flex');
          statusText.textContent = 'Ambient On';
          eqEl.classList.add('eq-playing');
          showToast('Deep-space ambient synthesizer activated', 'info');
        } else {
          masterGain.gain.cancelScheduledValues(now);
          masterGain.gain.setTargetAtTime(0.0001, now, 0.4);
          iconPause.classList.add('hidden');
          iconPause.classList.remove('flex');
          iconPlay.classList.remove('hidden');
          statusText.textContent = 'Cosmic Audio';
          eqEl.classList.remove('eq-playing');
        }
      });

      volumeSlider.addEventListener('input', (e) => {
        if (masterGain && isPlaying) {
          masterGain.gain.setTargetAtTime(parseFloat(e.target.value), audioCtx.currentTime, 0.1);
        }
      });
    })();

    // =========================================================================
    // 4. CUSTOM EDITABLE LAB TASK CARDS (LocalStorage + Add/Delete + Export HTML)
    // =========================================================================
    const STORAGE_KEY = 'jnmg_galaxy_portfolio_labs_v1';

    const DEFAULT_LAB_TASKS = [
      {
        id: 'lab-01',
        code: 'LAB-01 // PLACEHOLDER',
        status: 'Completed',
        date: '2026-Q1',
        title: 'Orbital Mechanics & Keplerian Trajectory Simulator',
        description: 'Placeholder description: Interactive computational lab modeling planetary orbits, eccentricity, and gravitational slingshot maneuvers using numerical integration.',
        tags: ['Python', 'Physics', 'Simulation', 'Placeholder'],
        repoUrl: 'https://github.com',
        demoUrl: '#lab-tasks'
      },
      {
        id: 'lab-02',
        code: 'LAB-02 // PLACEHOLDER',
        status: 'In Progress',
        date: '2026-Q2',
        title: 'Stellar Spectral Classification & Light Curve Analyzer',
        description: 'Placeholder description: Processing simulated photometric light curves and absorption spectra to classify star types and detect exoplanet transit dips.',
        tags: ['Data Analysis', 'Spectroscopy', 'Algorithms', 'Placeholder'],
        repoUrl: 'https://github.com',
        demoUrl: '#lab-tasks'
      },
      {
        id: 'lab-03',
        code: 'LAB-03 // PLACEHOLDER',
        status: 'Completed',
        date: '2026-Q3',
        title: 'Deep-Sky Telemetry & Sensor Data Logger',
        description: 'Placeholder description: Custom software pipeline built to parse, clean, and visualize real-time environmental and telescope mount telemetry streams.',
        tags: ['JavaScript', 'Telemetry', 'Dashboard', 'Placeholder'],
        repoUrl: 'https://github.com',
        demoUrl: '#lab-tasks'
      },
      {
        id: 'lab-04',
        code: 'LAB-04 // PLACEHOLDER',
        status: 'Prototype',
        date: '2026-Q4',
        title: 'Custom Lab Experiment Module [Your Title Here]',
        description: 'Placeholder description: Click "Enable Edit Mode" above to customize this card with your own laboratory task objectives, tools used, and repository links.',
        tags: ['Custom Lab', 'GitHub Pages', 'Edit Me'],
        repoUrl: 'https://github.com',
        demoUrl: '#lab-tasks'
      }
    ];

    let labTasks = [];
    let isEditMode = false;

    function loadLabTasks() {
      try {
        const saved = localStorage.getItem(STORAGE_KEY);
        if (saved) {
          const parsed = JSON.parse(saved);
          if (Array.isArray(parsed) && parsed.length > 0) {
            labTasks = parsed;
            return;
          }
        }
      } catch (err) {
        console.warn('Could not read saved labs from localStorage:', err);
      }
      labTasks = JSON.parse(JSON.stringify(DEFAULT_LAB_TASKS));
    }

    function saveLabTasks() {
      try {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(labTasks));
      } catch (err) {
        console.warn('Could not save labs to localStorage:', err);
      }
      updateLabStats();
    }

    function updateLabStats() {
      const statEl = document.getElementById('stat-lab-count');
      if (statEl) {
        statEl.textContent = String(labTasks.length).padStart(2, '0');
      }
    }

    function getStatusBadgeClasses(status) {
      const normalized = (status || '').toLowerCase();
      if (normalized.includes('complete')) {
        return 'bg-emerald-500/15 text-emerald-300 border-emerald-400/30';
      }
      if (normalized.includes('progress')) {
        return 'bg-sky-500/15 text-sky-300 border-sky-400/30';
      }
      return 'bg-amber-500/15 text-amber-300 border-amber-400/30';
    }

    function renderLabCards() {
      const grid = document.getElementById('lab-cards-grid');
      grid.innerHTML = '';

      if (isEditMode) {
        grid.classList.add('edit-mode-active');
      } else {
        grid.classList.remove('edit-mode-active');
      }

      labTasks.forEach((task, index) => {
        const card = document.createElement('article');
        card.className = 'cosmic-card rounded-3xl p-6 sm:p-7 flex flex-col justify-between gap-6 relative group';
        card.dataset.index = index;

        const tagsHtml = task.tags
          .map(tag => `<span class="px-2.5 py-1 rounded-lg bg-slate-950/80 border border-slate-800 text-xs font-mono text-sky-300/90">${escapeHtml(tag)}</span>`)
          .join('');

        card.innerHTML = `
          <div class="space-y-4">
            <!-- Top Row: Lab Code + Status + Delete (in Edit Mode) -->
            <div class="flex items-center justify-between gap-3 flex-wrap">
              <span contenteditable="${isEditMode}" data-field="code"
                class="font-mono text-xs tracking-wider uppercase text-purple-300 font-semibold">
                ${escapeHtml(task.code)}
              </span>

              <div class="flex items-center gap-2">
                <span contenteditable="${isEditMode}" data-field="date"
                  class="font-mono text-xs text-slate-400">
                  ${escapeHtml(task.date)}
                </span>
                <span contenteditable="${isEditMode}" data-field="status"
                  class="px-2.5 py-0.5 rounded-full text-[11px] font-mono border ${getStatusBadgeClasses(task.status)}">
                  ${escapeHtml(task.status)}
                </span>
                ${isEditMode ? `
                  <button type="button" data-delete-index="${index}" title="Remove Lab Card"
                    class="p-1.5 rounded-lg bg-rose-500/15 text-rose-300 border border-rose-400/40 hover:bg-rose-500/30 transition-colors">
                    <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
                    </svg>
                  </button>
                ` : ''}
              </div>
            </div>

            <!-- Lab Title -->
            <h3 contenteditable="${isEditMode}" data-field="title"
              class="font-display text-xl sm:text-2xl font-bold text-white group-hover:text-sky-300 transition-colors">
              ${escapeHtml(task.title)}
            </h3>

            <!-- Lab Description -->
            <p contenteditable="${isEditMode}" data-field="description"
              class="text-sm text-slate-300/90 leading-relaxed">
              ${escapeHtml(task.description)}
            </p>

            <!-- Tags (Comma-separated when editing) -->
            <div>
              ${isEditMode ? `
                <label class="block text-[10px] font-mono uppercase text-amber-300/80 mb-1">Tags (comma-separated):</label>
                <div contenteditable="true" data-field="tags" class="text-xs font-mono text-sky-300">
                  ${escapeHtml(task.tags.join(', '))}
                </div>
              ` : `
                <div class="flex flex-wrap gap-2">${tagsHtml}</div>
              `}
            </div>
          </div>

          <!-- Footer Links -->
          <div class="pt-4 border-t border-slate-800/80 flex flex-col gap-2">
            ${isEditMode ? `
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-2 text-xs font-mono">
                <div>
                  <span class="text-[10px] text-amber-300/80 block">GitHub Repo URL:</span>
                  <div contenteditable="true" data-field="repoUrl" class="text-slate-300 truncate">${escapeHtml(task.repoUrl)}</div>
                </div>
                <div>
                  <span class="text-[10px] text-amber-300/80 block">Live Demo / Report URL:</span>
                  <div contenteditable="true" data-field="demoUrl" class="text-slate-300 truncate">${escapeHtml(task.demoUrl)}</div>
                </div>
              </div>
            ` : `
              <div class="flex items-center justify-between gap-4 text-xs font-mono">
                <a href="${escapeAttr(task.repoUrl)}" target="_blank" rel="noopener noreferrer"
                  class="inline-flex items-center gap-1.5 text-slate-300 hover:text-sky-400 transition-colors">
                  <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24"><path fill-rule="evenodd" d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.53 1.032 1.53 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z" clip-rule="evenodd"/></svg>
                  <span>Source / Repo</span>
                </a>
                <a href="${escapeAttr(task.demoUrl)}" target="${task.demoUrl.startsWith('#') ? '_self' : '_blank'}" rel="noopener noreferrer"
                  class="inline-flex items-center gap-1 text-purple-300 hover:text-amber-300 transition-colors">
                  <span>Inspect Lab</span>
                  <span>↗</span>
                </a>
              </div>
            `}
          </div>
        `;

        // Attach inline edit listeners
        card.querySelectorAll('[contenteditable="true"]').forEach(el => {
          el.addEventListener('blur', () => {
            const field = el.dataset.field;
            const rawVal = el.textContent.trim();
            if (field === 'tags') {
              labTasks[index].tags = rawVal.split(',').map(t => t.trim()).filter(Boolean);
            } else {
              labTasks[index][field] = rawVal;
            }
            saveLabTasks();
          });
        });

        // Attach delete button listener in Edit Mode
        const delBtn = card.querySelector('[data-delete-index]');
        if (delBtn) {
          delBtn.addEventListener('click', () => {
            const removedTitle = labTasks[index].title;
            labTasks.splice(index, 1);
            saveLabTasks();
            renderLabCards();
            showToast(`Removed "${removedTitle}"`, 'warning');
          });
        }

        // Subtle 3D Tilt Hover Effect (Disabled while actively editing text)
        card.addEventListener('mousemove', (e) => {
          if (isEditMode) {
            card.style.transform = '';
            return;
          }
          const rect = card.getBoundingClientRect();
          const x = (e.clientX - rect.left) / rect.width - 0.5;
          const y = (e.clientY - rect.top) / rect.height - 0.5;
          card.style.transform = `perspective(900px) rotateX(${(-y * 5).toFixed(2)}deg) rotateY(${(x * 5).toFixed(2)}deg) translateY(-4px)`;
        });

        card.addEventListener('mouseleave', () => {
          card.style.transform = '';
        });

        grid.appendChild(card);
      });

      updateLabStats();
    }

    function escapeHtml(str) {
      return String(str || '')
        .replace(/&/g, '&amp;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;')
        .replace(/"/g, '&quot;');
    }

    function escapeAttr(str) {
      const val = String(str || '').trim();
      if (/^javascript:/i.test(val)) return '#';
      return escapeHtml(val || '#');
    }

    // Toolbar Event Listeners
    document.getElementById('toggle-edit-btn').addEventListener('click', () => {
      isEditMode = !isEditMode;
      const label = document.getElementById('edit-btn-label');
      const banner = document.getElementById('edit-mode-banner');
      const heroBio = document.getElementById('hero-bio-editable');

      if (isEditMode) {
        label.textContent = 'Done Editing';
        banner.classList.remove('hidden');
        heroBio.setAttribute('contenteditable', 'true');
        heroBio.classList.add('outline', 'outline-1', 'outline-dashed', 'outline-amber-400/70', 'rounded-lg', 'p-2');
        showToast('Edit Mode enabled — click any card field to customize', 'warning');
      } else {
        label.textContent = 'Enable Edit Mode';
        banner.classList.add('hidden');
        heroBio.removeAttribute('contenteditable');
        heroBio.classList.remove('outline', 'outline-1', 'outline-dashed', 'outline-amber-400/70', 'rounded-lg', 'p-2');
        saveLabTasks();
        showToast('Changes saved locally!', 'success');
      }
      renderLabCards();
    });

    document.getElementById('add-lab-btn').addEventListener('click', () => {
      const nextNum = String(labTasks.length + 1).padStart(2, '0');
      labTasks.push({
        id: `lab-${Date.now()}`,
        code: `LAB-${nextNum} // CUSTOM`,
        status: 'In Progress',
        date: '2026',
        title: `Custom Lab Task #${nextNum} [Editable Placeholder]`,
        description: 'Placeholder description: Outline your hypothesis, methodology, tools, and results for this laboratory task.',
        tags: ['Custom', 'Lab Task', 'Placeholder'],
        repoUrl: 'https://github.com',
        demoUrl: '#lab-tasks'
      });
      saveLabTasks();
      if (!isEditMode) {
        document.getElementById('toggle-edit-btn').click();
      } else {
        renderLabCards();
      }
      showToast(`Added Lab-${nextNum} card`, 'success');
    });

    document.getElementById('reset-labs-btn').addEventListener('click', () => {
      labTasks = JSON.parse(JSON.stringify(DEFAULT_LAB_TASKS));
      saveLabTasks();
      renderLabCards();
      showToast('Restored default placeholder lab cards', 'info');
    });

    // Export standalone HTML snapshot with updated lab cards baked in
    document.getElementById('export-html-btn').addEventListener('click', () => {
      if (isEditMode) {
        document.getElementById('toggle-edit-btn').click();
      }
      let docHtml = '<!DOCTYPE html>\n' + document.documentElement.outerHTML;
      // Replace DEFAULT_LAB_TASKS array in exported source so GitHub Pages loads customized cards by default
      const serialized = JSON.stringify(labTasks, null, 2);
      docHtml = docHtml.replace(
        /const DEFAULT_LAB_TASKS = \[[\s\S]*?\];/,
        `const DEFAULT_LAB_TASKS = ${serialized};`
      );

      const blob = new Blob([docHtml], { type: 'text/html;charset=utf-8' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = 'index.html';
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      URL.revokeObjectURL(url);
      showToast('Exported updated index.html ready for GitHub Pages!', 'success');
    });

    // =========================================================================
    // 5. NAVIGATION, SCROLL REVEAL & CONTACT FORM HANDLERS
    // =========================================================================
    document.getElementById('current-year').textContent = new Date().getFullYear();

    // Mobile Menu Toggle
    const mobileMenuBtn = document.getElementById('mobile-menu-btn');
    const mobileMenu = document.getElementById('mobile-menu');
    mobileMenuBtn.addEventListener('click', () => {
      mobileMenu.classList.toggle('hidden');
    });
    mobileMenu.querySelectorAll('a').forEach(link => {
      link.addEventListener('click', () => mobileMenu.classList.add('hidden'));
    });

    // Scroll Reveal IntersectionObserver
    const revealObserver = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible');
        }
      });
    }, { threshold: 0.12 });

    document.querySelectorAll('.reveal').forEach(el => revealObserver.observe(el));

    // Comms Form Submission
    document.getElementById('comms-form').addEventListener('submit', (e) => {
      e.preventDefault();
      const sender = document.getElementById('sender-name').value.trim();
      showToast(`Signal received from ${sender || 'Observer'}! Thank you for reaching out.`, 'success');
      e.target.reset();
    });

    // Initialize Lab Cards on Load
    loadLabTasks();
    renderLabCards();
  </script>
</body>
</html>