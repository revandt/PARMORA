<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="theme-color" content="#0d2e24">
    <title>Palmora — Deteksi Dini & Siaga Warga Dwi-Musim</title>

    <!-- Tailwind CSS & Lucide Icons -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>

    <!-- Tipografi Modern -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">

    <style>
        * {
            box-sizing: border-box;
            font-family: 'Plus Jakarta Sans', system-ui, -apple-system, sans-serif;
        }

        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }

        @keyframes doorOpenLeft {
            0% { transform: translateX(0); }
            100% { transform: translateX(-105%); }
        }
        @keyframes doorOpenRight {
            0% { transform: translateX(0); }
            100% { transform: translateX(105%); }
        }
        @keyframes badgeZoomFade {
            0% { opacity: 1; transform: scale(1); }
            60% { opacity: 1; transform: scale(1.08); }
            100% { opacity: 0; transform: scale(0.85); }
        }
        .door-left-run {
            animation: doorOpenLeft 0.85s cubic-bezier(0.77, 0, 0.175, 1) 0.25s forwards;
        }
        .door-right-run {
            animation: doorOpenRight 0.85s cubic-bezier(0.77, 0, 0.175, 1) 0.25s forwards;
        }
        .door-badge-run {
            animation: badgeZoomFade 0.55s ease-out 0.1s forwards;
        }

        @keyframes tabPopIn {
            0% { opacity: 0; transform: translateY(12px) scale(0.98); }
            100% { opacity: 1; transform: translateY(0) scale(1); }
        }
        @keyframes slideFromRight {
            0% { opacity: 0; transform: translateX(36px) scale(0.98); }
            100% { opacity: 1; transform: translateX(0) scale(1); }
        }
        @keyframes slideFromLeft {
            0% { opacity: 0; transform: translateX(-36px) scale(0.98); }
            100% { opacity: 1; transform: translateX(0) scale(1); }
        }
        .animate-tab {
            animation: tabPopIn 0.34s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }
        .animate-slide-right {
            animation: slideFromRight 0.35s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }
        .animate-slide-left {
            animation: slideFromLeft 0.35s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }

        @keyframes floatSlow {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-6px) rotate(2deg); }
        }
        .animate-float {
            animation: floatSlow 3.3s ease-in-out infinite;
        }

        @keyframes diagonalSweep {
            0% { transform: translateX(-140%) skewX(-24deg); }
            100% { transform: translateX(250%) skewX(-24deg); }
        }
        .shimmer-card::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 45%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transform: translateX(-140%) skewX(-24deg);
            animation: diagonalSweep 4.6s ease-in-out infinite;
            pointer-events: none;
        }

        @keyframes shootSkyward {
            0% { opacity: 1; transform: translate(0, 0) scale(1); }
            100% { opacity: 0; transform: translate(var(--dx, 0px), -145px) scale(0.25); }
        }
        .sky-spark {
            position: fixed;
            width: 8px;
            height: 8px;
            border-radius: 9999px;
            pointer-events: none;
            z-index: 9999;
            animation: shootSkyward 0.85s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }

        @keyframes sonarPulse {
            0% { transform: scale(0.95); opacity: 0.85; }
            100% { transform: scale(2.3); opacity: 0; }
        }
        .animate-sonar {
            animation: sonarPulse 1.8s cubic-bezier(0, 0, 0.2, 1) infinite;
        }

        @keyframes waveMove {
            0%, 100% { transform: translateX(0); }
            50% { transform: translateX(-8%); }
        }
        .animate-wave {
            animation: waveMove 5s ease-in-out infinite;
        }

        @keyframes eqBounce {
            0%, 100% { height: 4px; }
            50% { height: 14px; }
        }
        .eq-1 { animation: eqBounce 0.55s ease-in-out infinite; }
        .eq-2 { animation: eqBounce 0.55s ease-in-out 0.15s infinite; }
        .eq-3 { animation: eqBounce 0.55s ease-in-out 0.3s infinite; }

        @keyframes redAlertPulse {
            0%, 100% { opacity: 0.35; }
            50% { opacity: 0.95; }
        }
        @keyframes urgentCardShake {
            0%, 100% { transform: translateX(0); }
            20% { transform: translateX(-2px); }
            40% { transform: translateX(2px); }
            60% { transform: translateX(-1.5px); }
            80% { transform: translateX(1.5px); }
        }
        .alarm-vignette-active {
            animation: redAlertPulse 0.9s ease-in-out infinite;
        }
        .alarm-card-urgent {
            animation: urgentCardShake 0.45s ease-in-out infinite;
            box-shadow: 0 0 28px rgba(220, 38, 38, 0.65) !important;
        }
        @keyframes flowStreamDash {
            to { stroke-dashoffset: -24; }
        }
        .water-jet-anim {
            stroke-dasharray: 8 6;
            animation: flowStreamDash 0.65s linear infinite;
        }

        .ripple-btn {
            position: relative;
            overflow: hidden;
            transition: transform 0.16s cubic-bezier(0.2, 0.8, 0.2, 1), box-shadow 0.2s ease, background-color 0.2s ease;
        }
        .ripple-btn:active {
            transform: scale(0.96);
        }
        .ripple-circle {
            position: absolute;
            border-radius: 50%;
            transform: scale(0);
            animation: rippleEffect 0.55s linear;
            background-color: rgba(255, 255, 255, 0.35);
            pointer-events: none;
        }
        @keyframes rippleEffect {
            to {
                transform: scale(4);
                opacity: 0;
            }
        }

        input[type="range"].kanal-slider {
            -webkit-appearance: none;
            appearance: none;
            height: 10px;
            border-radius: 999px;
            background: #cbd5e1;
            outline: none;
        }
        input[type="range"].kanal-slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 24px;
            height: 24px;
            border-radius: 50%;
            background: #0f766e;
            border: 3px solid #ffffff;
            box-shadow: 0 2px 8px rgba(15, 118, 110, 0.45);
            cursor: pointer;
            transition: transform 0.15s ease;
        }
        input[type="range"].kanal-slider::-webkit-slider-thumb:hover {
            transform: scale(1.12);
        }
    </style>
</head>
<body class="bg-[#ebf1ed] text-slate-800 antialiased min-h-screen flex flex-col selection:bg-emerald-200 selection:text-emerald-950">

    <!-- OVERLAY KILATAN MERAH DARURAT -->
    <div id="alarm-red-vignette" class="fixed inset-0 pointer-events-none z-50 hidden border-[6px] border-red-600/90 shadow-[inset_0_0_95px_rgba(220,38,38,0.55)] alarm-vignette-active" aria-hidden="true"></div>

    <!-- ANIMASI PINTU MASUK APLIKASI -->
    <div id="app-entry-doors" class="fixed inset-0 z-[100] pointer-events-none flex overflow-hidden" aria-hidden="true">
        <div id="door-left" class="w-1/2 h-full bg-[#0d2e24] border-r border-emerald-500/30 flex items-center justify-end pr-4 shadow-2xl door-left-run">
            <div class="w-12 h-24 rounded-l-full bg-emerald-500/15 border border-emerald-400/30"></div>
        </div>
        <div id="door-right" class="w-1/2 h-full bg-[#0d2e24] border-l border-emerald-500/30 flex items-center justify-start pl-4 shadow-2xl door-right-run">
            <div class="w-12 h-24 rounded-r-full bg-emerald-500/15 border border-emerald-400/30"></div>
        </div>
        <div id="door-badge" class="absolute inset-0 flex flex-col items-center justify-center text-white door-badge-run">
            <div class="w-16 h-16 rounded-3xl bg-gradient-to-br from-emerald-400 to-teal-500 text-slate-950 flex items-center justify-center shadow-xl mb-2">
                <i data-lucide="sprout" class="w-8 h-8 stroke-[2.5]"></i>
            </div>
            <span class="font-extrabold text-xl tracking-tight">Palmora</span>
        </div>
    </div>

    <!-- HEADER UTAMA -->
    <header class="bg-[#0d2e24] text-white sticky top-0 z-40 shadow-md border-b border-emerald-900/60">
        <div class="max-w-[1380px] mx-auto px-4 py-3 flex flex-wrap items-center justify-between gap-3">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-2xl bg-gradient-to-br from-emerald-400 to-teal-500 text-slate-950 flex items-center justify-center shadow-sm">
                    <i data-lucide="sprout" class="w-5 h-5 stroke-[2.5]"></i>
                </div>
                <div>
                    <div class="flex items-center gap-2">
                        <h1 class="font-extrabold text-lg tracking-tight leading-none">Palmora</h1>
                        <span class="text-[10px] font-extrabold uppercase tracking-wider px-2 py-0.5 rounded-full bg-emerald-500/20 text-emerald-300 border border-emerald-400/30">
                            Siaga Dwi-Musim
                        </span>
                    </div>
                    <p class="text-[11px] text-emerald-200/80 mt-0.5">Kabupaten Kapuas • Provinsi Kalimantan Tengah</p>
                </div>
            </div>

            <div class="flex flex-wrap items-center justify-center gap-2">
                <div class="bg-emerald-950/80 p-1 rounded-2xl border border-emerald-800/80 flex items-center gap-1" role="group" aria-label="Pilih kondisi cuaca">
                    <button type="button" onclick="setScenario('rainy')" data-season-btn="rainy"
                        class="ripple-btn px-3 py-1.5 rounded-xl text-xs font-bold flex items-center gap-1.5 transition-all">
                        <i data-lucide="cloud-rain" class="w-3.5 h-3.5"></i>
                        <span>Hujan</span>
                    </button>
                    <button type="button" onclick="setScenario('dry')" data-season-btn="dry"
                        class="ripple-btn px-3 py-1.5 rounded-xl text-xs font-bold flex items-center gap-1.5 transition-all">
                        <i data-lucide="flame" class="w-3.5 h-3.5"></i>
                        <span>Kemarau</span>
                    </button>
                    <button type="button" onclick="setScenario('normal')" data-season-btn="normal"
                        class="ripple-btn px-3 py-1.5 rounded-xl text-xs font-bold flex items-center gap-1.5 transition-all">
                        <i data-lucide="shield-check" class="w-3.5 h-3.5"></i>
                        <span>Aman</span>
                    </button>
                </div>

                <button type="button" id="btn-alarm" onclick="toggleAlarm(event)"
                    class="ripple-btn bg-amber-400 hover:bg-amber-300 text-slate-950 text-xs font-extrabold px-3.5 py-2 rounded-xl flex items-center gap-2 shadow-xs">
                    <i data-lucide="bell-ring" class="w-4 h-4"></i>
                    <span id="alarm-btn-text">Uji Alarm</span>
                    <span id="alarm-eq" class="hidden items-end gap-0.5 h-3.5">
                        <span class="w-0.5 bg-white rounded-full eq-1"></span>
                        <span class="w-0.5 bg-white rounded-full eq-2"></span>
                        <span class="w-0.5 bg-white rounded-full eq-3"></span>
                    </span>
                </button>

                <button type="button" onclick="replayDoorIntro()" title="Putar ulang animasi masuk"
                    class="ripple-btn bg-white/10 hover:bg-white/20 text-emerald-100 text-xs font-bold p-2 rounded-xl flex items-center justify-center">
                    <i data-lucide="door-open" class="w-4 h-4"></i>
                </button>

                <div class="hidden lg:flex bg-emerald-950/80 p-1 rounded-2xl border border-emerald-800/80 items-center gap-1">
                    <button type="button" onclick="setLayout('split')" data-layout-btn="split"
                        class="ripple-btn px-2.5 py-1.5 rounded-xl text-[11px] font-bold">Semua</button>
                    <button type="button" onclick="setLayout('mobile')" data-layout-btn="mobile"
                        class="ripple-btn px-2.5 py-1.5 rounded-xl text-[11px] font-bold">HP</button>
                    <button type="button" onclick="setLayout('pc')" data-layout-btn="pc"
                        class="ripple-btn px-2.5 py-1.5 rounded-xl text-[11px] font-bold">PC</button>
                </div>
            </div>
        </div>
    </header>

    <!-- KONTEN UTAMA -->
    <main class="flex-1 max-w-[1380px] w-full mx-auto px-4 py-6">
        <div id="workspace-grid" class="grid grid-cols-1 lg:grid-cols-12 gap-7 items-start justify-items-center">

            <!-- KOLOM KIRI: MOBILE WARGA -->
            <section id="panel-mobile" class="w-full lg:col-span-5 xl:col-span-4 flex flex-col items-center">
                <div class="mb-3 text-center">
                    <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-white border border-slate-200 text-xs font-bold text-slate-600 shadow-2xs">
                        <i data-lucide="smartphone" class="w-3.5 h-3.5 text-emerald-700"></i>
                        Aplikasi Warga (Mobile)
                    </span>
                </div>

                <div id="mobile-phone-frame" class="w-full max-w-[392px] bg-slate-900 rounded-[2.7rem] p-3 shadow-2xl border-[3px] border-slate-800 relative transition-all duration-300">
                    <div class="bg-[#f5f8f6] rounded-[2.1rem] overflow-hidden flex flex-col h-[750px] relative">

                        <div class="bg-white px-5 pt-2.5 pb-1.5 flex items-center justify-between text-[11px] font-bold text-slate-700">
                            <span>09:42 WIB</span>
                            <div class="w-20 h-4 bg-slate-900 rounded-full"></div>
                            <div class="flex items-center gap-1.5 text-slate-600">
                                <i data-lucide="signal" class="w-3.5 h-3.5"></i>
                                <i data-lucide="battery-full" class="w-4 h-4 text-emerald-600"></i>
                            </div>
                        </div>

                        <div class="bg-white px-4 py-2.5 border-b border-slate-100 flex items-center justify-between">
                            <div class="flex items-center gap-2">
                                <div class="w-8 h-8 rounded-xl bg-emerald-700 text-white flex items-center justify-center">
                                    <i data-lucide="sprout" class="w-4 h-4"></i>
                                </div>
                                <div>
                                    <p class="text-xs font-extrabold text-slate-900 leading-none">Palmora Warga</p>
                                    <p class="text-[10px] text-slate-500 mt-0.5 flex items-center gap-1">
                                        <i data-lucide="map-pin" class="w-2.5 h-2.5 text-emerald-600"></i>
                                        Kabupaten Kapuas • Kalteng
                                    </p>
                                </div>
                            </div>
                            <span id="mob-live-chip" class="px-2.5 py-1 rounded-full text-[10px] font-extrabold bg-emerald-100 text-emerald-800">
                                LIVE
                            </span>
                        </div>

                        <div id="mobile-scroll-body" class="flex-1 overflow-y-auto no-scrollbar p-3.5 space-y-3.5">

                            <!-- TAB BERANDA -->
                            <div id="mob-tab-home" class="space-y-3.5 animate-tab">
                                <article id="mob-alert-card" class="shimmer-card rounded-3xl p-4 bg-gradient-to-br from-blue-600 to-blue-700 text-white shadow-md transition-all duration-300 relative overflow-hidden text-center">
                                    <canvas id="mob-weather-canvas" class="absolute inset-0 w-full h-full pointer-events-none z-0"></canvas>

                                    <div class="relative z-10 inline-flex items-center gap-2 bg-black/25 backdrop-blur-xs px-3 py-1 rounded-full text-[10px] font-extrabold uppercase tracking-wider mb-2">
                                        <span class="relative flex h-2 w-2">
                                            <span class="animate-sonar absolute inline-flex h-full w-full rounded-full bg-white"></span>
                                            <span class="relative inline-flex rounded-full h-2 w-2 bg-white"></span>
                                        </span>
                                        <span id="mob-alert-badge">PERINGATAN DINI BANJIR</span>
                                    </div>

                                    <div class="relative z-10 flex flex-col items-center justify-center">
                                        <div class="animate-float w-11 h-11 rounded-2xl bg-white/20 backdrop-blur-xs border border-white/25 flex items-center justify-center mb-1.5 shadow-xs">
                                            <i id="mob-weather-icon" data-lucide="cloud-rain" class="w-6 h-6 text-white"></i>
                                        </div>
                                        <h2 id="mob-alert-title" class="text-base font-extrabold leading-snug">
                                            Luapan di Hulu — Rumah Masih Aman
                                        </h2>
                                        <div class="mt-1.5 inline-flex items-center gap-1.5 bg-white/15 px-2.5 py-0.5 rounded-full text-[10px] font-bold text-white/95">
                                            <i data-lucide="wind" class="w-3 h-3"></i>
                                            <span id="mob-wind-live">Angin Tenggara • 18 km/j</span>
                                        </div>
                                    </div>

                                    <div class="grid grid-cols-2 gap-2 mt-3 relative z-10">
                                        <div class="bg-white/15 backdrop-blur-xs rounded-2xl p-2.5">
                                            <p class="text-[10px] uppercase tracking-wider text-white/80 font-semibold">Estimasi Tiba</p>
                                            <p id="mob-alert-eta" class="text-sm font-extrabold mt-0.5">± 2 Jam 15 Mnt</p>
                                        </div>
                                        <div class="bg-white/15 backdrop-blur-xs rounded-2xl p-2.5">
                                            <p class="text-[10px] uppercase tracking-wider text-white/80 font-semibold">Titik Bahaya</p>
                                            <p id="mob-alert-dist" class="text-sm font-extrabold mt-0.5">1,4 km Hulu</p>
                                        </div>
                                    </div>

                                    <button type="button" onclick="switchMobTab('evakuasi')"
                                        class="ripple-btn mt-3 w-full bg-white text-slate-900 hover:bg-slate-50 font-extrabold text-xs py-2.5 px-4 rounded-2xl shadow-xs flex items-center justify-center gap-2 relative z-10">
                                        <i data-lucide="compass" class="w-4 h-4 text-emerald-700"></i>
                                        <span>Lihat Arah Mengungsi</span>
                                    </button>

                                    <svg class="animate-wave absolute -bottom-2 left-0 w-[120%] h-6 text-white/15 pointer-events-none z-0" viewBox="0 0 1200 120" preserveAspectRatio="none">
                                        <path d="M0,40 C300,100 900,-20 1200,40 L1200,120 L0,120 Z" fill="currentColor"></path>
                                    </svg>
                                </article>

                                <div class="bg-white rounded-3xl p-3 border border-slate-200/80 shadow-2xs grid grid-cols-4 gap-2 text-center">
                                    <button type="button" onclick="switchMobTab('evakuasi')" class="ripple-btn flex flex-col items-center gap-1.5 p-1.5 rounded-2xl hover:bg-slate-50">
                                        <div class="w-10 h-10 rounded-2xl bg-emerald-100 text-emerald-700 flex items-center justify-center">
                                            <i data-lucide="navigation" class="w-5 h-5"></i>
                                        </div>
                                        <span class="text-[11px] font-bold text-slate-700">Posko</span>
                                    </button>
                                    <button type="button" onclick="switchMobTab('pantau')" class="ripple-btn flex flex-col items-center gap-1.5 p-1.5 rounded-2xl hover:bg-slate-50">
                                        <div class="w-10 h-10 rounded-2xl bg-sky-100 text-sky-700 flex items-center justify-center">
                                            <i data-lucide="waves" class="w-5 h-5"></i>
                                        </div>
                                        <span class="text-[11px] font-bold text-slate-700">Kanal</span>
                                    </button>
                                    <button type="button" onclick="switchMobTab('panduan')" class="ripple-btn flex flex-col items-center gap-1.5 p-1.5 rounded-2xl hover:bg-slate-50">
                                        <div class="w-10 h-10 rounded-2xl bg-amber-100 text-amber-700 flex items-center justify-center">
                                            <i data-lucide="book-open-check" class="w-5 h-5"></i>
                                        </div>
                                        <span class="text-[11px] font-bold text-slate-700">Panduan</span>
                                    </button>
                                    <button type="button" onclick="toggleAlarm(event)" class="ripple-btn flex flex-col items-center gap-1.5 p-1.5 rounded-2xl hover:bg-slate-50">
                                        <div class="w-10 h-10 rounded-2xl bg-rose-100 text-rose-700 flex items-center justify-center">
                                            <i data-lucide="volume-2" class="w-5 h-5"></i>
                                        </div>
                                        <span class="text-[11px] font-bold text-slate-700">Sirine</span>
                                    </button>
                                </div>

                                <div id="mob-sensor-cards" class="grid grid-cols-2 gap-2.5 text-center"></div>

                                <article class="bg-white border border-emerald-200 rounded-3xl p-3.5 shadow-2xs text-center">
                                    <div class="inline-flex items-center gap-1.5 px-2.5 py-0.5 rounded-full bg-emerald-50 text-emerald-800 text-[10px] font-extrabold mb-1.5">
                                        <i data-lucide="users" class="w-3 h-3"></i>
                                        <span>Info Warga Kab. Kapuas</span>
                                    </div>
                                    <p id="mob-nudge-msg" class="text-xs font-semibold text-slate-700 leading-relaxed mb-3">
                                        86% warga Kabupaten Kapuas sudah mengamankan dokumen &amp; memantau sekat kanal.
                                    </p>
                                    <button type="button" id="btn-citizen-ready" onclick="confirmCitizenReady(event)"
                                        class="ripple-btn w-full bg-emerald-700 hover:bg-emerald-800 text-white text-xs font-extrabold py-2.5 px-4 rounded-2xl flex items-center justify-center gap-1.5 shadow-2xs">
                                        <i data-lucide="check-circle-2" class="w-4 h-4"></i>
                                        <span id="btn-citizen-ready-text">Konfirmasi Saya Siaga</span>
                                    </button>
                                </article>
                            </div>

                            <!-- TAB EVAKUASI -->
                            <div id="mob-tab-evakuasi" class="space-y-3 hidden">
                                <div class="bg-white rounded-3xl p-4 border border-slate-200/80 text-center shadow-2xs">
                                    <span class="inline-block px-2.5 py-0.5 rounded-full bg-emerald-100 text-emerald-800 text-[10px] font-extrabold mb-1">
                                        TITIK KUMPUL TERDEKAT
                                    </span>
                                    <h3 class="text-sm font-extrabold text-slate-900">Arah Evakuasi Warga</h3>
                                    <p class="text-[11px] text-slate-500 mt-0.5">Pilih posko di dataran lebih tinggi</p>
                                </div>

                                <div class="space-y-2.5">
                                    <article class="bg-white border border-emerald-200 rounded-3xl p-3.5 shadow-2xs text-center">
                                        <div class="flex items-center justify-center gap-2 mb-1">
                                            <span class="w-7 h-7 rounded-xl bg-emerald-100 text-emerald-700 flex items-center justify-center">
                                                <i data-lucide="home" class="w-4 h-4"></i>
                                            </span>
                                            <h4 class="text-xs font-extrabold text-slate-900">Posko 1 — Posko Induk Kab. Kapuas</h4>
                                        </div>
                                        <p class="text-[11px] text-slate-600">850 m arah Selatan • Dataran Tinggi (+2,4 m)</p>
                                        <div class="mt-2 inline-flex items-center gap-2 bg-emerald-50 text-emerald-800 px-3 py-1 rounded-full text-[10px] font-bold">
                                            <span>Jalur Poros Kapuas Aman</span>
                                            <span>•</span>
                                            <span>Kapasitas 250 Orang</span>
                                        </div>
                                    </article>

                                    <article class="bg-white border border-sky-200 rounded-3xl p-3.5 shadow-2xs text-center">
                                        <div class="flex items-center justify-center gap-2 mb-1">
                                            <span class="w-7 h-7 rounded-xl bg-sky-100 text-sky-700 flex items-center justify-center">
                                                <i data-lucide="heart-pulse" class="w-4 h-4"></i>
                                            </span>
                                            <h4 class="text-xs font-extrabold text-slate-900">Posko 2 — RSUD / Puskesmas Kab. Kapuas</h4>
                                        </div>
                                        <p class="text-[11px] text-slate-600">1,2 km arah Timur • Ruang Bersih Udara &amp; Medis</p>
                                        <div class="mt-2 inline-flex items-center gap-2 bg-sky-50 text-sky-800 px-3 py-1 rounded-full text-[10px] font-bold">
                                            <span>Prioritas Balita &amp; Lansia</span>
                                            <span>•</span>
                                            <span>Oksigen &amp; Masker</span>
                                        </div>
                                    </article>
                                </div>

                                <div class="bg-white rounded-3xl p-3.5 border border-slate-200/80 shadow-2xs">
                                    <p class="text-xs font-extrabold text-slate-900 text-center mb-2.5">Tas Siaga Keluarga</p>
                                    <div id="evac-checklist" class="space-y-2 text-xs"></div>
                                </div>
                            </div>

                            <!-- TAB PANTAU -->
                            <div id="mob-tab-pantau" class="space-y-3 hidden">
                                <div class="bg-white rounded-3xl p-3.5 border border-slate-200/80 shadow-2xs text-center">
                                    <div class="flex items-center justify-center gap-1.5">
                                        <span class="w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
                                        <p class="text-[10px] font-extrabold uppercase tracking-wider text-emerald-700">Sekat Kanal Gambut IoT</p>
                                    </div>
                                    <h3 id="mob-gate-title" class="text-sm font-extrabold text-slate-900 mt-0.5">Bukaan 85% (Pelepasan Air)</h3>

                                    <div id="mob-canal-scene" class="mt-2.5 mx-auto w-full rounded-2xl overflow-hidden border border-slate-200 shadow-inner bg-sky-50"></div>

                                    <p class="text-[10px] text-slate-500 mt-2 font-medium">Aktuator otomatis dikendalikan dari Posko Kab. Kapuas</p>
                                </div>

                                <div id="mob-zone-list" class="space-y-2"></div>
                            </div>

                            <!-- TAB PANDUAN -->
                            <div id="mob-tab-panduan" class="space-y-2.5 hidden">
                                <div class="bg-white rounded-3xl p-3.5 border border-slate-200/80 text-center shadow-2xs">
                                    <h3 class="text-sm font-extrabold text-slate-900">Langkah Cepat Warga</h3>
                                    <p class="text-[11px] text-slate-500">Ringkasan tindakan saat cuaca berubah</p>
                                </div>

                                <div class="bg-blue-50 border border-blue-200 rounded-3xl p-3.5 text-center">
                                    <div class="w-8 h-8 rounded-xl bg-blue-600 text-white flex items-center justify-center mx-auto mb-1.5">
                                        <i data-lucide="cloud-rain" class="w-4 h-4"></i>
                                    </div>
                                    <h4 class="text-xs font-extrabold text-blue-950">Saat Hujan Deras</h4>
                                    <p class="text-[11px] text-blue-900/80 mt-1 leading-relaxed">
                                        Cek parit sekitar rumah, simpan surat berharga di tempat tinggi, dan ikuti jadwal buka kanal posko.
                                    </p>
                                </div>

                                <div class="bg-amber-50 border border-amber-200 rounded-3xl p-3.5 text-center">
                                    <div class="w-8 h-8 rounded-xl bg-amber-600 text-white flex items-center justify-center mx-auto mb-1.5">
                                        <i data-lucide="flame" class="w-4 h-4"></i>
                                    </div>
                                    <h4 class="text-xs font-extrabold text-amber-950">Saat Kemarau Kering</h4>
                                    <p class="text-[11px] text-amber-900/80 mt-1 leading-relaxed">
                                        Jaga pintu sekat kanal tetap tertutup agar lahan basah, dilarang membakar semak, dan siapkan masker N95.
                                    </p>
                                </div>

                                <div class="bg-emerald-50 border border-emerald-200 rounded-3xl p-3.5 text-center">
                                    <div class="w-8 h-8 rounded-xl bg-emerald-700 text-white flex items-center justify-center mx-auto mb-1.5">
                                        <i data-lucide="heart-handshake" class="w-4 h-4"></i>
                                    </div>
                                    <h4 class="text-xs font-extrabold text-emerald-950">Saling Jaga Tetangga</h4>
                                    <p class="text-[11px] text-emerald-900/80 mt-1 leading-relaxed">
                                        Kabari warga lansia atau keluarga dengan balita saat status alarm berubah menjadi Waspada.
                                    </p>
                                </div>
                            </div>

                        </div>

                        <nav class="mobile-nav bg-white border-t border-slate-200/80 px-2 py-2 grid grid-cols-4 gap-1" aria-label="Menu aplikasi warga">
                            <button type="button" onclick="switchMobTab('home')" data-mobnav="home"
                                class="ripple-btn flex flex-col items-center justify-center py-1.5 rounded-2xl text-emerald-800 bg-emerald-100/80 font-extrabold text-[11px]">
                                <i data-lucide="home" class="w-4 h-4 mb-0.5"></i>
                                <span>Beranda</span>
                            </button>
                            <button type="button" onclick="switchMobTab('evakuasi')" data-mobnav="evakuasi"
                                class="ripple-btn flex flex-col items-center justify-center py-1.5 rounded-2xl text-slate-500 hover:bg-slate-100 font-semibold text-[11px]">
                                <i data-lucide="compass" class="w-4 h-4 mb-0.5"></i>
                                <span>Evakuasi</span>
                            </button>
                            <button type="button" onclick="switchMobTab('pantau')" data-mobnav="pantau"
                                class="ripple-btn flex flex-col items-center justify-center py-1.5 rounded-2xl text-slate-500 hover:bg-slate-100 font-semibold text-[11px]">
                                <i data-lucide="activity" class="w-4 h-4 mb-0.5"></i>
                                <span>Pantau</span>
                            </button>
                            <button type="button" onclick="switchMobTab('panduan')" data-mobnav="panduan"
                                class="ripple-btn flex flex-col items-center justify-center py-1.5 rounded-2xl text-slate-500 hover:bg-slate-100 font-semibold text-[11px]">
                                <i data-lucide="book-open" class="w-4 h-4 mb-0.5"></i>
                                <span>Panduan</span>
                            </button>
                        </nav>
                    </div>
                </div>
            </section>

            <!-- KOLOM KANAN: DASHBOARD POSKO PC -->
            <section id="panel-pc" class="w-full lg:col-span-7 xl:col-span-8 space-y-4">
                <div class="text-center lg:text-left flex flex-wrap items-center justify-center lg:justify-between gap-2">
                    <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full bg-white border border-slate-200 text-xs font-bold text-slate-600 shadow-2xs">
                        <i data-lucide="monitor" class="w-3.5 h-3.5 text-emerald-700"></i>
                        Dashboard Posko &amp; Pengelola (PC)
                    </span>
                    <span class="text-xs font-semibold text-slate-500">Sinkronisasi Otomatis dengan Aplikasi Warga</span>
                </div>

                <div class="shimmer-card relative overflow-hidden bg-gradient-to-r from-[#0d2e24] via-[#154839] to-[#1d604d] text-white rounded-3xl p-6 shadow-sm text-center sm:text-left flex flex-col sm:flex-row items-center justify-between gap-4">
                    <canvas id="pc-weather-canvas" class="absolute inset-0 w-full h-full pointer-events-none z-0"></canvas>
                    <div class="relative z-10">
                        <span class="inline-block text-[10px] font-extrabold uppercase tracking-wider bg-white/15 px-3 py-1 rounded-full text-emerald-200 mb-2">
                            Posko Siaga • Kabupaten Kapuas, Kalimantan Tengah
                        </span>
                        <h2 class="text-xl sm:text-2xl font-extrabold tracking-tight">
                            Kendali Sekat Kanal &amp; Kesiapsiagaan Warga
                        </h2>
                    </div>
                    <div class="relative z-10 flex items-center gap-3 bg-black/25 backdrop-blur-xs border border-white/15 rounded-2xl px-4 py-3 text-xs shrink-0">
                        <div class="text-center px-2 border-r border-white/15">
                            <p class="text-[10px] text-emerald-200">Gateway</p>
                            <p class="font-extrabold text-emerald-300">Online</p>
                        </div>
                        <div class="text-center px-2 border-r border-white/15">
                            <p class="text-[10px] text-emerald-200">Sensor</p>
                            <p class="font-extrabold">3 / 3 Aktif</p>
                        </div>
                        <div class="text-center px-2">
                            <p class="text-[10px] text-emerald-200">Posko</p>
                            <p class="font-extrabold">Siap 24 Jam</p>
                        </div>
                    </div>
                </div>

                <div id="pc-kpi-grid" class="grid grid-cols-2 sm:grid-cols-4 gap-3 text-center"></div>

                <div class="bg-white p-1.5 rounded-2xl border border-slate-200/80 shadow-2xs flex flex-wrap items-center justify-center gap-1.5">
                    <button type="button" onclick="switchPcTab('kontrol')" data-pcnav="kontrol"
                        class="ripple-btn flex-1 min-w-[130px] py-2 px-4 rounded-xl text-xs font-extrabold bg-emerald-800 text-white flex items-center justify-center gap-1.5">
                        <i data-lucide="sliders" class="w-4 h-4"></i>
                        <span>Kendali &amp; Siaga</span>
                    </button>
                    <button type="button" onclick="switchPcTab('database')" data-pcnav="database"
                        class="ripple-btn flex-1 min-w-[130px] py-2 px-4 rounded-xl text-xs font-bold text-slate-600 hover:bg-slate-100 flex items-center justify-center gap-1.5">
                        <i data-lucide="database" class="w-4 h-4"></i>
                        <span>Data Sensor</span>
                    </button>
                    <button type="button" onclick="switchPcTab('edukasi')" data-pcnav="edukasi"
                        class="ripple-btn flex-1 min-w-[130px] py-2 px-4 rounded-xl text-xs font-bold text-slate-600 hover:bg-slate-100 flex items-center justify-center gap-1.5">
                        <i data-lucide="users" class="w-4 h-4"></i>
                        <span>Edukasi &amp; Nudge</span>
                    </button>
                </div>

                <!-- PC TAB KONTROL -->
                <div id="pc-tab-kontrol" class="grid grid-cols-1 md:grid-cols-2 gap-4 animate-tab">
                    <article class="bg-white rounded-3xl p-5 border border-slate-200/80 shadow-2xs flex flex-col justify-between text-center">
                        <div>
                            <span class="inline-block px-2.5 py-0.5 rounded-full bg-teal-50 text-teal-800 text-[10px] font-extrabold uppercase tracking-wider">
                                Otomasi Tata Air
                            </span>
                            <h3 class="text-base font-extrabold text-slate-900 mt-1">Pintu Sekat Kanal Utama</h3>
                            <p id="pc-gate-desc" class="text-xs text-slate-500 mt-0.5">Mode Pelepasan Air Terukur <span id="pc-gate-badge" class="font-extrabold text-teal-700">(85%)</span></p>

                            <div id="pc-canal-scene" class="my-3.5 mx-auto w-full rounded-2xl overflow-hidden border border-slate-200 shadow-inner bg-sky-50"></div>

                            <div class="px-2">
                                <input type="range" id="pc-gate-slider" min="0" max="100" value="85" oninput="updateGate(this.value)" class="kanal-slider w-full">
                                <div class="flex justify-between text-[10px] font-bold text-slate-400 mt-1">
                                    <span>0% (Tutup Penuh)</span>
                                    <span>50%</span>
                                    <span>100% (Buka Penuh)</span>
                                </div>
                            </div>
                        </div>

                        <div class="grid grid-cols-3 gap-2 mt-4">
                            <button type="button" onclick="updateGate(15, event)"
                                class="ripple-btn py-2 px-2 rounded-xl bg-amber-50 hover:bg-amber-100 text-amber-900 border border-amber-200 text-[11px] font-extrabold">
                                Tahan Air (15%)
                            </button>
                            <button type="button" onclick="updateGate(50, event)"
                                class="ripple-btn py-2 px-2 rounded-xl bg-emerald-50 hover:bg-emerald-100 text-emerald-900 border border-emerald-200 text-[11px] font-extrabold">
                                Seimbang (50%)
                            </button>
                            <button type="button" onclick="updateGate(85, event)"
                                class="ripple-btn py-2 px-2 rounded-xl bg-blue-50 hover:bg-blue-100 text-blue-900 border border-blue-200 text-[11px] font-extrabold">
                                Lepas Air (85%)
                            </button>
                        </div>
                    </article>

                    <article class="bg-white rounded-3xl p-5 border border-slate-200/80 shadow-2xs flex flex-col justify-between text-center">
                        <div>
                            <span class="inline-block px-2.5 py-0.5 rounded-full bg-emerald-50 text-emerald-800 text-[10px] font-extrabold uppercase tracking-wider">
                                Psikologi Lingkungan • Nudge
                            </span>
                            <h3 class="text-base font-extrabold text-slate-900 mt-1">Kesiapsiagaan Warga</h3>
                            <p class="text-xs text-slate-500 mt-0.5">Partisipasi warga merespons peringatan dini</p>

                            <div class="my-4 bg-emerald-50/80 border border-emerald-200 rounded-2xl p-4">
                                <p id="pc-readiness-val" class="text-3xl font-extrabold text-emerald-800">86%</p>
                                <p class="text-xs font-bold text-emerald-900 mt-0.5">Keluarga Kab. Kapuas Sudah Siaga</p>
                                <div class="w-full h-2.5 bg-emerald-200/70 rounded-full overflow-hidden mt-2.5">
                                    <div id="pc-readiness-bar" class="h-full bg-emerald-600 rounded-full transition-all duration-500" style="width: 86%;"></div>
                                </div>
                            </div>

                            <div class="bg-slate-50 border border-slate-200/80 rounded-2xl p-3 text-xs text-slate-700 font-medium leading-relaxed">
                                "<span id="pc-nudge-preview">86% warga Kabupaten Kapuas sudah mengamankan dokumen &amp; memantau sekat kanal.</span>"
                            </div>
                        </div>

                        <button type="button" onclick="broadcastNudge(event)"
                            class="ripple-btn mt-4 w-full bg-emerald-700 hover:bg-emerald-800 text-white text-xs font-extrabold py-3 px-4 rounded-2xl flex items-center justify-center gap-2 shadow-xs">
                            <i data-lucide="send" class="w-4 h-4"></i>
                            <span>Kirim Pengingat ke HP Warga</span>
                        </button>
                    </article>
                </div>

                <!-- PC TAB DATABASE -->
                <div id="pc-tab-database" class="bg-white rounded-3xl p-5 border border-slate-200/80 shadow-2xs hidden">
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 mb-4">
                        <div class="text-center sm:text-left">
                            <span class="inline-block px-2.5 py-0.5 rounded-full bg-emerald-50 text-emerald-800 text-[10px] font-extrabold uppercase tracking-wider mb-1">
                                Arsip Telemetri • Kabupaten Kapuas
                            </span>
                            <h3 class="text-base font-extrabold text-slate-900">Riwayat Rekaman Sensor Lapangan</h3>
                            <p class="text-xs text-slate-500">Log otomatis 3 stasiun pemantauan (Hulu Sawit, Sekat Kanal, &amp; Pemukiman)</p>
                        </div>
                        <div class="flex flex-wrap items-center justify-center sm:justify-end gap-2">
                            <select id="pc-node-filter" onchange="renderLogs()"
                                class="bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-xs font-bold text-slate-700">
                                <option value="all">Semua Titik</option>
                                <option value="NODE-01">NODE-01 (Hulu Sawit)</option>
                                <option value="NODE-02">NODE-02 (Sekat Kanal)</option>
                                <option value="NODE-03">NODE-03 (Pemukiman)</option>
                            </select>
                            <select id="pc-log-filter" onchange="renderLogs()"
                                class="bg-slate-50 border border-slate-200 rounded-xl px-3 py-2 text-xs font-bold text-slate-700">
                                <option value="all">Semua Status</option>
                                <option value="Waspada">Waspada</option>
                                <option value="Pantau">Pantau</option>
                                <option value="Aman">Aman</option>
                            </select>
                            <button type="button" onclick="simulateNewReading(event)"
                                class="ripple-btn bg-emerald-700 hover:bg-emerald-800 text-white text-xs font-extrabold px-3.5 py-2 rounded-xl flex items-center gap-1.5 shadow-2xs">
                                <i data-lucide="refresh-cw" class="w-3.5 h-3.5"></i>
                                <span>Ambil Data Baru</span>
                            </button>
                        </div>
                    </div>

                    <div id="pc-log-summary" class="grid grid-cols-3 gap-2.5 mb-3.5 text-center"></div>

                    <div class="overflow-x-auto rounded-2xl border border-slate-200/90">
                        <table class="w-full border-collapse text-xs">
                            <thead>
                                <tr class="bg-slate-50 text-slate-600 font-extrabold uppercase text-[10px] tracking-wider border-b border-slate-200">
                                    <th class="py-3 px-3.5 text-left">Waktu (WIB)</th>
                                    <th class="py-3 px-3.5 text-left">Stasiun / Lokasi Kapuas</th>
                                    <th class="py-3 px-3.5 text-center">Muka Air</th>
                                    <th class="py-3 px-3.5 text-center">Kelembapan</th>
                                    <th class="py-3 px-3.5 text-center">Udara / VOC</th>
                                    <th class="py-3 px-3.5 text-center">Status</th>
                                </tr>
                            </thead>
                            <tbody id="pc-log-tbody" class="divide-y divide-slate-100 font-semibold text-slate-700"></tbody>
                        </table>
                    </div>
                </div>

                <!-- PC TAB EDUKASI -->
                <div id="pc-tab-edukasi" class="grid grid-cols-1 md:grid-cols-3 gap-3.5 hidden text-center">
                    <article class="bg-white rounded-3xl p-5 border border-slate-200/80 shadow-2xs">
                        <div class="w-10 h-10 rounded-2xl bg-blue-100 text-blue-700 flex items-center justify-center mx-auto mb-2.5">
                            <i data-lucide="eye" class="w-5 h-5"></i>
                        </div>
                        <h4 class="text-sm font-extrabold text-slate-900">Persepsi Risiko Nyata</h4>
                        <p class="text-xs text-slate-600 mt-1.5 leading-relaxed">
                            Menampilkan jarak bahaya dan estimasi waktu tiba agar warga bersiap sebelum air atau asap mencapai rumah.
                        </p>
                    </article>

                    <article class="bg-white rounded-3xl p-5 border border-slate-200/80 shadow-2xs">
                        <div class="w-10 h-10 rounded-2xl bg-emerald-100 text-emerald-700 flex items-center justify-center mx-auto mb-2.5">
                            <i data-lucide="users" class="w-5 h-5"></i>
                        </div>
                        <h4 class="text-sm font-extrabold text-slate-900">Bukti Sosial Warga</h4>
                        <p class="text-xs text-slate-600 mt-1.5 leading-relaxed">
                            Pesan berbasis kebersamaan tetangga mendorong warga ikut menjaga sekat kanal tanpa paksaan.
                        </p>
                    </article>

                    <article class="bg-white rounded-3xl p-5 border border-slate-200/80 shadow-2xs">
                        <div class="w-10 h-10 rounded-2xl bg-amber-100 text-amber-700 flex items-center justify-center mx-auto mb-2.5">
                            <i data-lucide="shield-check" class="w-5 h-5"></i>
                        </div>
                        <h4 class="text-sm font-extrabold text-slate-900">Aksi Cepat Tanpa Panik</h4>
                        <p class="text-xs text-slate-600 mt-1.5 leading-relaxed">
                            Panduan langkah sederhana mempermudah evakuasi kelompok rentan menuju posko terdekat.
                        </p>
                    </article>
                </div>

            </section>
        </div>
    </main>

    <!-- TOAST NOTIFIKASI -->
    <div id="toast-box" class="fixed bottom-5 left-1/2 -translate-x-1/2 z-50 pointer-events-none opacity-0 translate-y-4 transition-all duration-300">
        <div class="bg-slate-900 text-white px-4 py-2.5 rounded-2xl shadow-xl border border-slate-700 flex items-center gap-2 text-xs font-bold">
            <i data-lucide="check-circle-2" class="w-4 h-4 text-emerald-400"></i>
            <span id="toast-text">Notifikasi terkirim</span>
        </div>
    </div>

    <script>
        const state = {
            season: 'rainy',
            gatePct: 85,
            readinessPct: 86,
            citizenConfirmed: false,
            mobTab: 'home',
            pcTab: 'kontrol',
            layout: 'split',
            alarmActive: false,
            alarmTimer: null,
            audioCtx: null,
            timeOffsetMin: 0,
            toastTimer: null
        };

        const tabOrder = ['home', 'evakuasi', 'pantau', 'panduan'];

        const scenarioData = {
            rainy: {
                badge: 'PERINGATAN DINI BANJIR',
                cardGradient: 'from-blue-600 to-blue-700',
                weatherIcon: 'cloud-rain',
                windLive: 'Angin Tenggara • 18 km/j',
                title: 'Luapan di Hulu — Rumah Masih Aman',
                eta: '± 2 Jam 15 Mnt',
                dist: '1,4 km Hulu',
                defaultGate: 85,
                defaultReadiness: 86,
                gateDesc: 'Mode Pelepasan Air Terukur',
                nudge: '86% warga Kabupaten Kapuas sudah mengamankan dokumen &amp; memantau sekat kanal.',
                metrics: [
                    { label: 'Muka Air Hulu', val: '+0,32 m', icon: 'waves', color: 'text-blue-600 bg-blue-50' },
                    { label: 'Curah Hujan', val: '68 mm', icon: 'cloud-rain', color: 'text-sky-600 bg-sky-50' },
                    { label: 'Kualitas Udara', val: 'Baik (12)', icon: 'wind', color: 'text-emerald-600 bg-emerald-50' },
                    { label: 'Jarak Aman', val: '1,4 km', icon: 'shield', color: 'text-teal-600 bg-teal-50' }
                ],
                zones: [
                    { name: 'Hulu Perkebunan Sawit Kapuas', dist: '1,4 km', water: '+0,32 m', status: 'Waspada', badge: 'bg-blue-100 text-blue-800' },
                    { name: 'Sekat Kanal Utama Kapuas', dist: '600 m', water: '+0,12 m', status: 'Pantau', badge: 'bg-amber-100 text-amber-800' },
                    { name: 'Pemukiman Warga Kapuas', dist: '0 km', water: '−0,15 m', status: 'Aman', badge: 'bg-emerald-100 text-emerald-800' }
                ],
                logs: [
                    { time: '09:45 WIB', code: 'NODE-01', loc: 'Hulu Perkebunan Sawit Kapuas', water: '+0,34 m', soil: '95%', air: '11 µg/m³ PM₂.₅', status: 'Waspada' },
                    { time: '09:40 WIB', code: 'NODE-02', loc: 'Sekat Kanal Utama Kapuas', water: '+0,14 m', soil: '89%', air: '13 µg/m³ PM₂.₅', status: 'Pantau' },
                    { time: '09:35 WIB', code: 'NODE-03', loc: 'Zona Pemukiman Warga Kapuas', water: '−0,14 m', soil: '75%', air: '10 µg/m³ PM₂.₅', status: 'Aman' },
                    { time: '09:15 WIB', code: 'NODE-01', loc: 'Hulu Perkebunan Sawit Kapuas', water: '+0,28 m', soil: '92%', air: '12 µg/m³ PM₂.₅', status: 'Waspada' },
                    { time: '09:00 WIB', code: 'NODE-02', loc: 'Sekat Kanal Utama Kapuas', water: '+0,09 m', soil: '85%', air: '14 µg/m³ PM₂.₅', status: 'Pantau' },
                    { time: '08:45 WIB', code: 'NODE-03', loc: 'Zona Pemukiman Warga Kapuas', water: '−0,18 m', soil: '71%', air: '11 µg/m³ PM₂.₅', status: 'Aman' }
                ]
            },
            dry: {
                badge: 'PERINGATAN KARHUTLA & ASAP',
                cardGradient: 'from-amber-600 to-orange-700',
                weatherIcon: 'flame',
                windLive: 'Angin Kering • 22 km/j',
                title: 'Hulu Mengering — Siaga Asap ke Pemukiman',
                eta: '± 3 Jam 00 Mnt',
                dist: '1,4 km Hulu',
                defaultGate: 15,
                defaultReadiness: 82,
                gateDesc: 'Mode Penahanan Air Gambut',
                nudge: '82% petani Kab. Kapuas telah menutup pintu sekat kanal agar lahan tetap basah.',
                metrics: [
                    { label: 'Muka Air Hulu', val: '−0,48 m', icon: 'droplets', color: 'text-amber-600 bg-amber-50' },
                    { label: 'Suhu Lahan', val: '35,4 °C', icon: 'thermometer', color: 'text-orange-600 bg-orange-50' },
                    { label: 'VOC Tanaman', val: '78 ppm', icon: 'sprout', color: 'text-rose-600 bg-rose-50' },
                    { label: 'Udara Kapuas', val: 'Sedang (42)', icon: 'wind', color: 'text-teal-600 bg-teal-50' }
                ],
                zones: [
                    { name: 'Hulu Perkebunan Sawit Kapuas', dist: '1,4 km', water: '−0,48 m', status: 'Waspada', badge: 'bg-amber-100 text-amber-800' },
                    { name: 'Sekat Kanal Utama Kapuas', dist: '600 m', water: '−0,36 m', status: 'Pantau', badge: 'bg-orange-100 text-orange-800' },
                    { name: 'Pemukiman Warga Kapuas', dist: '0 km', water: '−0,24 m', status: 'Aman', badge: 'bg-emerald-100 text-emerald-800' }
                ],
                logs: [
                    { time: '09:45 WIB', code: 'NODE-01', loc: 'Hulu Perkebunan Sawit Kapuas', water: '−0,48 m', soil: '28%', air: '78 ppm VOC', status: 'Waspada' },
                    { time: '09:40 WIB', code: 'NODE-02', loc: 'Sekat Kanal Utama Kapuas', water: '−0,36 m', soil: '35%', air: '45 ppm VOC', status: 'Pantau' },
                    { time: '09:35 WIB', code: 'NODE-03', loc: 'Zona Pemukiman Warga Kapuas', water: '−0,24 m', soil: '54%', air: '24 µg/m³ PM₂.₅', status: 'Aman' },
                    { time: '09:15 WIB', code: 'NODE-01', loc: 'Hulu Perkebunan Sawit Kapuas', water: '−0,45 m', soil: '30%', air: '71 ppm VOC', status: 'Waspada' },
                    { time: '09:00 WIB', code: 'NODE-02', loc: 'Sekat Kanal Utama Kapuas', water: '−0,33 m', soil: '38%', air: '39 ppm VOC', status: 'Pantau' },
                    { time: '08:45 WIB', code: 'NODE-03', loc: 'Zona Pemukiman Warga Kapuas', water: '−0,22 m', soil: '56%', air: '21 µg/m³ PM₂.₅', status: 'Aman' }
                ]
            },
            normal: {
                badge: 'KONDISI AMAN • TERKENDALI',
                cardGradient: 'from-emerald-600 to-teal-700',
                weatherIcon: 'sun',
                windLive: 'Angin Sepoi • 9 km/j',
                title: 'Air Kanal &amp; Udara Kapuas Normal',
                eta: 'Tidak Ada Ancaman',
                dist: 'Zona Aman',
                defaultGate: 50,
                defaultReadiness: 91,
                gateDesc: 'Mode Tata Air Seimbang',
                nudge: '91% warga &amp; kelompok tani Kab. Kapuas aktif menjaga sekat kanal tetap berfungsi baik.',
                metrics: [
                    { label: 'Muka Air Hulu', val: '−0,15 m', icon: 'waves', color: 'text-emerald-600 bg-emerald-50' },
                    { label: 'Kelembapan', val: '68%', icon: 'droplets', color: 'text-teal-600 bg-teal-50' },
                    { label: 'Udara Kapuas', val: 'Sehat (16)', icon: 'wind', color: 'text-sky-600 bg-sky-50' },
                    { label: 'Status Posko', val: 'Normal', icon: 'shield-check', color: 'text-emerald-600 bg-emerald-50' }
                ],
                zones: [
                    { name: 'Hulu Perkebunan Sawit Kapuas', dist: '1,4 km', water: '−0,15 m', status: 'Aman', badge: 'bg-emerald-100 text-emerald-800' },
                    { name: 'Sekat Kanal Utama Kapuas', dist: '600 m', water: '−0,18 m', status: 'Aman', badge: 'bg-emerald-100 text-emerald-800' },
                    { name: 'Pemukiman Warga Kapuas', dist: '0 km', water: '−0,20 m', status: 'Aman', badge: 'bg-emerald-100 text-emerald-800' }
                ],
                logs: [
                    { time: '09:45 WIB', code: 'NODE-01', loc: 'Hulu Perkebunan Sawit Kapuas', water: '−0,15 m', soil: '68%', air: '18 ppm VOC', status: 'Aman' },
                    { time: '09:40 WIB', code: 'NODE-02', loc: 'Sekat Kanal Utama Kapuas', water: '−0,18 m', soil: '65%', air: '16 µg/m³ PM₂.₅', status: 'Aman' },
                    { time: '09:35 WIB', code: 'NODE-03', loc: 'Zona Pemukiman Warga Kapuas', water: '−0,20 m', soil: '62%', air: '15 µg/m³ PM₂.₅', status: 'Aman' },
                    { time: '09:15 WIB', code: 'NODE-01', loc: 'Hulu Perkebunan Sawit Kapuas', water: '−0,16 m', soil: '67%', air: '19 ppm VOC', status: 'Aman' },
                    { time: '09:00 WIB', code: 'NODE-02', loc: 'Sekat Kanal Utama Kapuas', water: '−0,19 m', soil: '64%', air: '15 µg/m³ PM₂.₅', status: 'Aman' },
                    { time: '08:45 WIB', code: 'NODE-03', loc: 'Zona Pemukiman Warga Kapuas', water: '−0,21 m', soil: '61%', air: '14 µg/m³ PM₂.₅', status: 'Aman' }
                ]
            }
        };

        const checklistItems = [
            { id: 'chk1', text: 'KTP, KK, &amp; Surat Tanah dalam map kedap air', done: true },
            { id: 'chk2', text: 'Masker N95 / medis untuk balita &amp; lansia', done: true },
            { id: 'chk3', text: 'Obat pribadi, senter, &amp; powerbank terisi penuh', done: false },
            { id: 'chk4', text: 'Air minum &amp; makanan siap santap untuk 2 hari', done: false }
        ];

        function setScenario(season) {
            state.season = season;
            const d = scenarioData[season];
            state.gatePct = d.defaultGate;
            state.readinessPct = d.defaultReadiness;
            state.citizenConfirmed = false;

            document.querySelectorAll('[data-season-btn]').forEach(btn => {
                const active = btn.dataset.seasonBtn === season;
                btn.className = active
                    ? 'ripple-btn px-3 py-1.5 rounded-xl text-xs font-extrabold flex items-center gap-1.5 bg-white text-slate-900 shadow-xs'
                    : 'ripple-btn px-3 py-1.5 rounded-xl text-xs font-bold flex items-center gap-1.5 text-emerald-200 hover:text-white';
            });

            const readyBtn = document.getElementById('btn-citizen-ready');
            if (readyBtn) {
                readyBtn.className = 'ripple-btn w-full bg-emerald-700 hover:bg-emerald-800 text-white text-xs font-extrabold py-2.5 px-4 rounded-2xl flex items-center justify-center gap-1.5 shadow-2xs';
                document.getElementById('btn-citizen-ready-text').textContent = 'Konfirmasi Saya Siaga';
            }

            renderAll();
        }

        function renderAll() {
            const d = scenarioData[state.season];

            const alertCard = document.getElementById('mob-alert-card');
            if (alertCard) {
                if (state.alarmActive) {
                    alertCard.className = 'shimmer-card alarm-card-urgent rounded-3xl p-4 bg-gradient-to-br from-red-600 via-rose-700 to-red-800 text-white shadow-xl transition-all duration-300 relative overflow-hidden text-center';
                    document.getElementById('mob-alert-badge').textContent = 'DARURAT • SIRINE BMKG AKTIF';
                } else {
                    alertCard.className = `shimmer-card rounded-3xl p-4 bg-gradient-to-br ${d.cardGradient} text-white shadow-md transition-all duration-300 relative overflow-hidden text-center`;
                    document.getElementById('mob-alert-badge').textContent = d.badge;
                }
            }

            document.getElementById('mob-alert-title').innerHTML = d.title;
            document.getElementById('mob-alert-eta').textContent = d.eta;
            document.getElementById('mob-alert-dist').textContent = d.dist;
            document.getElementById('mob-wind-live').textContent = d.windLive;

            const wIcon = document.getElementById('mob-weather-icon');
            if (wIcon) wIcon.setAttribute('data-lucide', state.alarmActive ? 'siren' : d.weatherIcon);

            document.getElementById('mob-nudge-msg').innerHTML = d.nudge;
            document.getElementById('pc-nudge-preview').innerHTML = d.nudge;
            document.getElementById('pc-readiness-val').textContent = `${state.readinessPct}%`;
            document.getElementById('pc-readiness-bar').style.width = `${state.readinessPct}%`;

            document.getElementById('mob-sensor-cards').innerHTML = d.metrics.map((m, idx) => `
                <div class="bg-white border border-slate-200/80 rounded-3xl p-3 shadow-2xs flex flex-col items-center justify-center transition-transform duration-200 hover:-translate-y-0.5">
                    <span class="animate-float w-7 h-7 rounded-xl ${m.color} flex items-center justify-center mb-1" style="animation-delay: ${idx * 0.25}s">
                        <i data-lucide="${m.icon}" class="w-4 h-4"></i>
                    </span>
                    <p class="text-base font-extrabold text-slate-900">${m.val}</p>
                    <p class="text-[10px] font-bold text-slate-500">${m.label}</p>
                </div>
            `).join('');

            document.getElementById('pc-kpi-grid').innerHTML = d.metrics.map((m, idx) => `
                <article class="bg-white border border-slate-200/90 rounded-3xl p-4 shadow-2xs flex flex-col items-center justify-center transition-transform duration-200 hover:-translate-y-0.5">
                    <div class="animate-float w-9 h-9 rounded-2xl ${m.color} flex items-center justify-center mb-1.5" style="animation-delay: ${idx * 0.25}s">
                        <i data-lucide="${m.icon}" class="w-5 h-5"></i>
                    </div>
                    <p class="text-2xl font-extrabold text-slate-900">${m.val}</p>
                    <p class="text-xs font-bold text-slate-500 mt-0.5">${m.label}</p>
                </article>
            `).join('');

            document.getElementById('mob-zone-list').innerHTML = d.zones.map(z => `
                <div class="bg-white border border-slate-200/80 rounded-2xl p-3 flex items-center justify-between shadow-2xs">
                    <div>
                        <p class="text-xs font-extrabold text-slate-900">${z.name}</p>
                        <p class="text-[10px] text-slate-500 font-semibold">Jarak ${z.dist} • Air ${z.water}</p>
                    </div>
                    <span class="px-2.5 py-1 rounded-full text-[10px] font-extrabold ${z.badge}">${z.status}</span>
                </div>
            `).join('');

            syncGateVisuals();
            renderChecklist();
            renderLogs();
            refreshIcons();
        }

        function refreshIcons() {
            try {
                if (window.lucide && typeof window.lucide.createIcons === 'function') {
                    window.lucide.createIcons();
                }
            } catch (e) {}
        }

        function updateGate(val, ev) {
            if (ev) launchSkyParticles(ev.clientX, ev.clientY, '#38bdf8');
            state.gatePct = Number(val);
            syncGateVisuals();
        }

        function syncGateVisuals() {
            const pct = state.gatePct;
            const modeLabel = pct <= 25
                ? 'Mode Penahanan Air Gambut'
                : pct >= 70
                    ? 'Mode Pelepasan Air Terukur'
                    : 'Mode Tata Air Seimbang';

            const slider = document.getElementById('pc-gate-slider');
            if (slider) slider.value = pct;

            const pcDesc = document.getElementById('pc-gate-desc');
            if (pcDesc) {
                pcDesc.innerHTML = `${modeLabel} <span id="pc-gate-badge" class="font-extrabold text-teal-700">(${pct}%)</span>`;
            }

            const mobTitle = document.getElementById('mob-gate-title');
            if (mobTitle) {
                const shortMode = pct <= 25 ? 'Penahanan Air' : pct >= 70 ? 'Pelepasan Air' : 'Seimbang';
                mobTitle.textContent = `Bukaan ${pct}% (${shortMode})`;
            }

            const pcScene = document.getElementById('pc-canal-scene');
            if (pcScene) {
                pcScene.innerHTML = buildCanalGateSVG(pct, state.season, 'pc');
            }

            const mobScene = document.getElementById('mob-canal-scene');
            if (mobScene) {
                mobScene.innerHTML = buildCanalGateSVG(pct, state.season, 'mob');
            }
        }

        function buildCanalGateSVG(pct, season, uid) {
            const openRatio = pct / 100;
            const gateY = 66 - openRatio * 34;
            const stemTopY = gateY - 26;

            const upstreamY = season === 'rainy'
                ? (74 + openRatio * 10)
                : season === 'dry'
                    ? (102 - (1 - openRatio) * 14)
                    : 88;
            const downstreamY = Math.min(114, Math.max(upstreamY + 4, 114 - openRatio * 24));

            const beaconColor = season === 'dry' ? '#f59e0b' : season === 'rainy' ? '#ef4444' : '#10b981';
            const skyTop = season === 'dry' ? '#fef3c7' : season === 'rainy' ? '#dbeafe' : '#e0f2fe';
            const skyBottom = season === 'dry' ? '#fde68a' : season === 'rainy' ? '#eff6ff' : '#f0fdf4';
            const waterTop = season === 'dry' ? '#0284c7' : '#0ea5e9';
            const waterBot = season === 'dry' ? '#0c4a6e' : '#0369a1';

            return `
                <svg viewBox="0 0 360 156" class="w-full h-auto block select-none" role="img" aria-label="Ilustrasi penampang pintu sekat kanal bukaan ${pct} persen">
                    <defs>
                        <linearGradient id="sky-${uid}" x1="0" y1="0" x2="0" y2="1">
                            <stop offset="0%" stop-color="${skyTop}"/>
                            <stop offset="100%" stop-color="${skyBottom}"/>
                        </linearGradient>
                        <linearGradient id="water-${uid}" x1="0" y1="0" x2="0" y2="1">
                            <stop offset="0%" stop-color="${waterTop}" stop-opacity="0.88"/>
                            <stop offset="100%" stop-color="${waterBot}" stop-opacity="0.96"/>
                        </linearGradient>
                        <linearGradient id="peat-${uid}" x1="0" y1="0" x2="0" y2="1">
                            <stop offset="0%" stop-color="#5c3a21"/>
                            <stop offset="100%" stop-color="#3b2313"/>
                        </linearGradient>
                        <linearGradient id="steel-${uid}" x1="0" y1="0" x2="1" y2="0">
                            <stop offset="0%" stop-color="#334155"/>
                            <stop offset="50%" stop-color="#64748b"/>
                            <stop offset="100%" stop-color="#1e293b"/>
                        </linearGradient>
                    </defs>

                    <rect x="0" y="0" width="360" height="156" fill="url(#sky-${uid})"/>
                    <g opacity="0.28" fill="#14532d">
                        <path d="M26,72 Q22,52 10,48 Q22,47 28,55 Q34,46 46,48 Q35,53 31,72 Z"/>
                        <path d="M332,72 Q328,50 315,46 Q328,45 334,54 Q341,44 353,46 Q341,52 337,72 Z"/>
                        <circle cx="58" cy="64" r="11"/>
                        <circle cx="302" cy="64" r="10"/>
                    </g>

                    <path d="M0,72 L76,72 L86,126 L0,126 Z" fill="url(#peat-${uid})"/>
                    <path d="M284,72 L360,72 L360,126 L274,126 Z" fill="url(#peat-${uid})"/>
                    <rect x="0" y="69" width="77" height="4" rx="2" fill="#15803d"/>
                    <rect x="283" y="69" width="77" height="4" rx="2" fill="#15803d"/>

                    <rect x="0" y="124" width="360" height="32" fill="#475569"/>
                    <rect x="74" y="120" width="212" height="8" fill="#94a3b8"/>

                    <path d="M0,${upstreamY} L172,${upstreamY} L172,120 L84,120 L76,72 L0,72 Z" fill="url(#water-${uid})"/>
                    <line x1="0" y1="${upstreamY}" x2="172" y2="${upstreamY}" stroke="#bae6fd" stroke-width="2"/>

                    <path d="M188,${downstreamY} L360,${downstreamY} L360,120 L276,120 L284,72 L360,72 L360,${downstreamY} Z" fill="url(#water-${uid})"/>
                    <rect x="188" y="${downstreamY}" width="172" height="${120 - downstreamY}" fill="url(#water-${uid})"/>
                    <line x1="188" y1="${downstreamY}" x2="360" y2="${downstreamY}" stroke="#bae6fd" stroke-width="2"/>

                    ${pct > 5 ? `
                        <path d="M168,116 Q180,113 196,115 T232,116" fill="none" stroke="#e0f2fe" stroke-width="2.5" class="water-jet-anim"/>
                        <path d="M172,111 Q186,108 202,111 T226,112" fill="none" stroke="#ffffff" stroke-width="1.6" opacity="0.8" class="water-jet-anim"/>
                        <circle cx="198" cy="113" r="2.2" fill="#ffffff" opacity="0.75"/>
                        <circle cx="212" cy="116" r="1.8" fill="#e0f2fe" opacity="0.7"/>
                    ` : ''}

                    <rect x="163" y="34" width="10" height="86" rx="2" fill="#cbd5e1" stroke="#64748b" stroke-width="1.2"/>
                    <rect x="187" y="34" width="10" height="86" rx="2" fill="#cbd5e1" stroke="#64748b" stroke-width="1.2"/>

                    <rect x="155" y="64" width="7" height="54" fill="#ffffff" stroke="#334155" stroke-width="0.8"/>
                    <rect x="155" y="64" width="7" height="10" fill="#dc2626"/>
                    <rect x="155" y="84" width="7" height="10" fill="#0284c7"/>
                    <rect x="155" y="104" width="7" height="10" fill="#0284c7"/>
                    <text x="151" y="71" text-anchor="end" font-size="6.5" font-weight="800" fill="#991b1b">+0.3m</text>
                    <text x="151" y="92" text-anchor="end" font-size="6.5" font-weight="700" fill="#1e293b">0.0m</text>
                    <text x="151" y="112" text-anchor="end" font-size="6.5" font-weight="800" fill="#92400e">-0.4m</text>

                    <rect x="148" y="26" width="64" height="9" rx="3" fill="#1e293b"/>
                    <rect x="166" y="8" width="28" height="18" rx="4" fill="#0f172a" stroke="#475569" stroke-width="1.2"/>
                    <polygon points="164,8 196,8 192,3 168,3" fill="#0284c7"/>
                    <circle cx="180" cy="14" r="3.2" fill="${beaconColor}"/>
                    <text x="180" y="23" text-anchor="middle" font-size="5.5" font-weight="800" fill="#e2e8f0">IoT GATE</text>

                    <line x1="180" y1="${stemTopY}" x2="180" y2="${gateY}" stroke="#94a3b8" stroke-width="4" stroke-dasharray="2 1.5"/>

                    <g transform="translate(0, ${gateY - 66})">
                        <rect x="168" y="66" width="24" height="54" rx="1.5" fill="url(#steel-${uid})" stroke="#0f172a" stroke-width="1.2"/>
                        <line x1="169" y1="76" x2="191" y2="76" stroke="#94a3b8" stroke-width="1.5"/>
                        <line x1="169" y1="88" x2="191" y2="88" stroke="#94a3b8" stroke-width="1.5"/>
                        <line x1="169" y1="100" x2="191" y2="100" stroke="#94a3b8" stroke-width="1.5"/>
                        <line x1="169" y1="112" x2="191" y2="112" stroke="#94a3b8" stroke-width="1.5"/>
                        <rect x="168" y="118" width="24" height="2.5" fill="#f59e0b"/>
                    </g>

                    <rect x="10" y="132" width="76" height="17" rx="8.5" fill="#0f172a" opacity="0.82"/>
                    <text x="48" y="143" text-anchor="middle" font-size="8" font-weight="800" fill="#e2e8f0">HULU (SAWIT)</text>

                    <rect x="134" y="131" width="92" height="19" rx="9.5" fill="#0f766e"/>
                    <text x="180" y="143.5" text-anchor="middle" font-size="8.5" font-weight="800" fill="#ffffff">BUKAAN ${pct}%</text>

                    <rect x="274" y="132" width="76" height="17" rx="8.5" fill="#0f172a" opacity="0.82"/>
                    <text x="312" y="143" text-anchor="middle" font-size="8" font-weight="800" fill="#e2e8f0">HILIR (WARGA)</text>
                </svg>
            `;
        }

        function renderChecklist() {
            const container = document.getElementById('evac-checklist');
            if (!container) return;
            container.innerHTML = checklistItems.map(item => `
                <button type="button" onclick="toggleChecklist('${item.id}')"
                    class="w-full text-left flex items-center gap-2.5 p-2 rounded-2xl border transition-all ${item.done ? 'bg-emerald-50/80 border-emerald-200 text-emerald-950' : 'bg-slate-50 border-slate-200/80 text-slate-700 hover:bg-slate-100'}">
                    <span class="w-5 h-5 rounded-lg flex items-center justify-center shrink-0 ${item.done ? 'bg-emerald-600 text-white' : 'bg-white border border-slate-300'}">
                        ${item.done ? '<i data-lucide="check" class="w-3.5 h-3.5 stroke-[3]"></i>' : ''}
                    </span>
                    <span class="font-semibold text-[11px] leading-snug ${item.done ? 'line-through opacity-75' : ''}">${item.text}</span>
                </button>
            `).join('');
            refreshIcons();
        }

        function toggleChecklist(id) {
            const item = checklistItems.find(x => x.id === id);
            if (item) {
                item.done = !item.done;
                renderChecklist();
            }
        }

        function confirmCitizenReady(ev) {
            if (ev) launchSkyParticles(ev.clientX, ev.clientY, '#10b981');
            if (!state.citizenConfirmed) {
                state.citizenConfirmed = true;
                state.readinessPct = Math.min(99, state.readinessPct + 2);
            }
            const readyBtn = document.getElementById('btn-citizen-ready');
            if (readyBtn) {
                readyBtn.className = 'ripple-btn w-full bg-slate-900 text-emerald-300 text-xs font-extrabold py-2.5 px-4 rounded-2xl flex items-center justify-center gap-1.5';
                document.getElementById('btn-citizen-ready-text').textContent = 'Tercatat Siaga ✓';
            }

            renderAll();
            showToast('Terima kasih! Kesiapsiagaan Anda tercatat di Posko Kab. Kapuas');
        }

        function broadcastNudge(ev) {
            if (ev) launchSkyParticles(ev.clientX, ev.clientY, '#34d399');
            showToast('Notifikasi peringatan & panduan terkirim ke warga Kab. Kapuas');
        }

        function renderLogs() {
            const tbody = document.getElementById('pc-log-tbody');
            const filterEl = document.getElementById('pc-log-filter');
            const nodeFilterEl = document.getElementById('pc-node-filter');
            const summaryEl = document.getElementById('pc-log-summary');
            if (!tbody || !filterEl) return;

            const allLogs = scenarioData[state.season].logs;
            const statusFilter = filterEl.value;
            const nodeFilter = nodeFilterEl ? nodeFilterEl.value : 'all';

            if (summaryEl) {
                const countWaspada = allLogs.filter(r => r.status === 'Waspada').length;
                const countPantau = allLogs.filter(r => r.status === 'Pantau').length;
                const countAman = allLogs.filter(r => r.status === 'Aman').length;
                summaryEl.innerHTML = `
                    <div class="bg-slate-50 border border-slate-200/80 rounded-2xl py-2 px-3">
                        <p class="text-[10px] font-bold text-slate-500">Total Sampel</p>
                        <p class="text-sm font-extrabold text-slate-900">${allLogs.length} Rekaman</p>
                    </div>
                    <div class="bg-amber-50/70 border border-amber-200/80 rounded-2xl py-2 px-3">
                        <p class="text-[10px] font-bold text-amber-800">Waspada / Pantau</p>
                        <p class="text-sm font-extrabold text-amber-900">${countWaspada + countPantau} Titik</p>
                    </div>
                    <div class="bg-emerald-50/70 border border-emerald-200/80 rounded-2xl py-2 px-3">
                        <p class="text-[10px] font-bold text-emerald-800">Kondisi Aman</p>
                        <p class="text-sm font-extrabold text-emerald-900">${countAman} Titik</p>
                    </div>
                `;
            }

            const rows = allLogs.filter(r =>
                (statusFilter === 'all' || r.status === statusFilter) &&
                (nodeFilter === 'all' || r.code === nodeFilter)
            );

            if (rows.length === 0) {
                tbody.innerHTML = `<tr><td colspan="6" class="py-7 text-center text-slate-400 font-semibold">Tidak ada rekaman yang sesuai dengan filter pilihan</td></tr>`;
                return;
            }

            tbody.innerHTML = rows.map((r, idx) => {
                const badgeCls = r.status === 'Waspada'
                    ? 'bg-rose-100 text-rose-800 border border-rose-200'
                    : r.status === 'Pantau'
                        ? 'bg-amber-100 text-amber-800 border border-amber-200'
                        : 'bg-emerald-100 text-emerald-800 border border-emerald-200';
                const nodeBadge = r.code === 'NODE-01'
                    ? 'bg-sky-100 text-sky-800'
                    : r.code === 'NODE-02'
                        ? 'bg-teal-100 text-teal-800'
                        : 'bg-slate-200 text-slate-800';
                return `
                    <tr class="hover:bg-slate-50/90 transition-colors ${idx === 0 ? 'bg-emerald-50/30' : ''}">
                        <td class="py-3 px-3.5 text-left whitespace-nowrap">
                            <span class="font-bold text-slate-700">${r.time}</span>
                            ${idx === 0 ? '<span class="ml-1.5 px-1.5 py-0.5 rounded-md bg-emerald-100 text-emerald-800 text-[9px] font-extrabold">BARU</span>' : ''}
                        </td>
                        <td class="py-3 px-3.5 text-left">
                            <div class="flex items-center gap-2">
                                <span class="px-2 py-0.5 rounded-md text-[10px] font-extrabold shrink-0 ${nodeBadge}">${r.code}</span>
                                <span class="font-bold text-slate-900">${r.loc}</span>
                            </div>
                        </td>
                        <td class="py-3 px-3.5 text-center font-extrabold text-sky-700 whitespace-nowrap">${r.water}</td>
                        <td class="py-3 px-3.5 text-center font-bold text-slate-700 whitespace-nowrap">${r.soil}</td>
                        <td class="py-3 px-3.5 text-center font-semibold text-slate-600 whitespace-nowrap">${r.air}</td>
                        <td class="py-3 px-3.5 text-center whitespace-nowrap">
                            <span class="inline-block px-2.5 py-0.5 rounded-full text-[10px] font-extrabold ${badgeCls}">${r.status}</span>
                        </td>
                    </tr>
                `;
            }).join('');
        }

        function simulateNewReading(ev) {
            if (ev) launchSkyParticles(ev.clientX, ev.clientY, '#10b981');
            state.timeOffsetMin += 5;
            const totalMin = 45 + state.timeOffsetMin;
            const hh = String(9 + Math.floor(totalMin / 60)).padStart(2, '0');
            const mm = String(totalMin % 60).padStart(2, '0');
            const timeStr = `${hh}:${mm} WIB`;

            const d = scenarioData[state.season];
            const jitter = ((Math.random() - 0.5) * 0.04).toFixed(2);
            const newWater = state.season === 'rainy'
                ? `+${(0.34 + Number(jitter)).toFixed(2).replace('.', ',')} m`
                : state.season === 'dry'
                    ? `−${(0.48 + Number(jitter)).toFixed(2).replace('.', ',')} m`
                    : `−${(0.15 + Number(jitter)).toFixed(2).replace('.', ',')} m`;

            d.logs.unshift({
                time: timeStr,
                code: 'NODE-01',
                loc: 'Hulu Perkebunan Sawit Kapuas',
                water: newWater,
                soil: state.season === 'rainy' ? '95%' : state.season === 'dry' ? '27%' : '69%',
                air: state.season === 'rainy' ? '11 µg/m³ PM₂.₅' : state.season === 'dry' ? '80 ppm VOC' : '17 ppm VOC',
                status: state.season === 'normal' ? 'Aman' : 'Waspada'
            });
            if (d.logs.length > 10) d.logs.pop();

            renderLogs();
            showToast(`Rekaman baru NODE-01 Kapuas tersimpan (${timeStr})`);
        }

        function switchMobTab(tab, dir) {
            const prevIdx = tabOrder.indexOf(state.mobTab);
            const nextIdx = tabOrder.indexOf(tab);
            const slideDir = dir || (nextIdx >= prevIdx ? 'right' : 'left');

            state.mobTab = tab;
            tabOrder.forEach(t => {
                const el = document.getElementById(`mob-tab-${t}`);
                if (!el) return;
                if (t === tab) {
                    el.classList.remove('hidden', 'animate-tab', 'animate-slide-right', 'animate-slide-left');
                    void el.offsetWidth;
                    el.classList.add(slideDir === 'right' ? 'animate-slide-right' : 'animate-slide-left');
                } else {
                    el.classList.add('hidden');
                }
            });

            document.querySelectorAll('[data-mobnav]').forEach(btn => {
                const active = btn.dataset.mobnav === tab;
                btn.className = active
                    ? 'ripple-btn flex flex-col items-center justify-center py-1.5 rounded-2xl text-emerald-800 bg-emerald-100/80 font-extrabold text-[11px]'
                    : 'ripple-btn flex flex-col items-center justify-center py-1.5 rounded-2xl text-slate-500 hover:bg-slate-100 font-semibold text-[11px]';
            });

            if (tab === 'pantau') syncGateVisuals();
            refreshIcons();
        }

        function switchPcTab(tab) {
            state.pcTab = tab;
            ['kontrol', 'database', 'edukasi'].forEach(t => {
                const el = document.getElementById(`pc-tab-${t}`);
                if (!el) return;
                if (t === tab) {
                    el.classList.remove('hidden');
                    el.classList.add('animate-tab');
                } else {
                    el.classList.add('hidden');
                }
            });

            document.querySelectorAll('[data-pcnav]').forEach(btn => {
                const active = btn.dataset.pcnav === tab;
                btn.className = active
                    ? 'ripple-btn flex-1 min-w-[130px] py-2 px-4 rounded-xl text-xs font-extrabold bg-emerald-800 text-white flex items-center justify-center gap-1.5'
                    : 'ripple-btn flex-1 min-w-[130px] py-2 px-4 rounded-xl text-xs font-bold text-slate-600 hover:bg-slate-100 flex items-center justify-center gap-1.5';
            });
            refreshIcons();
        }

        function setLayout(mode) {
            state.layout = mode;
            const mobPanel = document.getElementById('panel-mobile');
            const pcPanel = document.getElementById('panel-pc');

            document.querySelectorAll('[data-layout-btn]').forEach(btn => {
                const active = btn.dataset.layoutBtn === mode;
                btn.className = active
                    ? 'ripple-btn px-2.5 py-1.5 rounded-xl text-[11px] font-extrabold bg-white text-slate-900'
                    : 'ripple-btn px-2.5 py-1.5 rounded-xl text-[11px] font-bold text-emerald-200 hover:text-white';
            });

            if (mode === 'split') {
                mobPanel.classList.remove('hidden', 'lg:col-span-12');
                mobPanel.classList.add('lg:col-span-5', 'xl:col-span-4');
                pcPanel.classList.remove('hidden', 'lg:col-span-12');
                pcPanel.classList.add('lg:col-span-7', 'xl:col-span-8');
            } else if (mode === 'mobile') {
                mobPanel.classList.remove('hidden', 'lg:col-span-5', 'xl:col-span-4');
                mobPanel.classList.add('lg:col-span-12');
                pcPanel.classList.add('hidden');
            } else {
                pcPanel.classList.remove('hidden', 'lg:col-span-7', 'xl:col-span-8');
                pcPanel.classList.add('lg:col-span-12');
                mobPanel.classList.add('hidden');
            }
        }

        function playSirenCycle() {
            try {
                const AudioCtx = window.AudioContext || window.webkitAudioContext;
                if (!AudioCtx) return;
                if (!state.audioCtx) state.audioCtx = new AudioCtx();
                if (state.audioCtx.state === 'suspended') state.audioCtx.resume();

                const ctx = state.audioCtx;
                const now = ctx.currentTime;

                const osc = ctx.createOscillator();
                const gain = ctx.createGain();
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(520, now);
                osc.frequency.linearRampToValueAtTime(980, now + 0.55);
                osc.frequency.linearRampToValueAtTime(560, now + 1.1);

                gain.gain.setValueAtTime(0.001, now);
                gain.gain.exponentialRampToValueAtTime(0.14, now + 0.08);
                gain.gain.exponentialRampToValueAtTime(0.001, now + 1.15);

                osc.connect(gain);
                gain.connect(ctx.destination);
                osc.start(now);
                osc.stop(now + 1.18);

                [1.22, 1.38].forEach(offset => {
                    const beep = ctx.createOscillator();
                    const bGain = ctx.createGain();
                    beep.type = 'square';
                    beep.frequency.setValueAtTime(1150, now + offset);
                    bGain.gain.setValueAtTime(0.08, now + offset);
                    bGain.gain.exponentialRampToValueAtTime(0.001, now + offset + 0.1);
                    beep.connect(bGain);
                    bGain.connect(ctx.destination);
                    beep.start(now + offset);
                    beep.stop(now + offset + 0.11);
                });
            } catch (e) {}
        }

        function toggleAlarm(ev) {
            if (ev) launchSkyParticles(ev.clientX, ev.clientY, '#ef4444');
            state.alarmActive = !state.alarmActive;

            const btn = document.getElementById('btn-alarm');
            const btnText = document.getElementById('alarm-btn-text');
            const eq = document.getElementById('alarm-eq');
            const vignette = document.getElementById('alarm-red-vignette');

            if (state.alarmActive) {
                btn.className = 'ripple-btn bg-red-600 hover:bg-red-700 text-white text-xs font-extrabold px-3.5 py-2 rounded-xl flex items-center gap-2 shadow-md';
                btnText.textContent = 'Matikan Alarm';
                eq.classList.remove('hidden');
                eq.classList.add('flex');
                vignette.classList.remove('hidden');

                playSirenCycle();
                state.alarmTimer = setInterval(playSirenCycle, 1650);
                showToast('SIRINE PERINGATAN DINI BMKG AKTIF!');
            } else {
                btn.className = 'ripple-btn bg-amber-400 hover:bg-amber-300 text-slate-950 text-xs font-extrabold px-3.5 py-2 rounded-xl flex items-center gap-2 shadow-xs';
                btnText.textContent = 'Uji Alarm';
                eq.classList.add('hidden');
                eq.classList.remove('flex');
                vignette.classList.add('hidden');

                if (state.alarmTimer) {
                    clearInterval(state.alarmTimer);
                    state.alarmTimer = null;
                }
                showToast('Sirine peringatan dini dimatikan');
            }

            renderAll();
        }

        function replayDoorIntro() {
            const gate = document.getElementById('app-entry-doors');
            const left = document.getElementById('door-left');
            const right = document.getElementById('door-right');
            const badge = document.getElementById('door-badge');
            if (!gate || !left || !right || !badge) return;

            gate.classList.remove('hidden');
            left.classList.remove('door-left-run');
            right.classList.remove('door-right-run');
            badge.classList.remove('door-badge-run');

            void gate.offsetWidth;
            left.classList.add('door-left-run');
            right.classList.add('door-right-run');
            badge.classList.add('door-badge-run');

            setTimeout(() => gate.classList.add('hidden'), 1200);
        }

        function launchSkyParticles(x, y, color = '#34d399') {
            if (!x && !y) return;
            for (let i = 0; i < 8; i++) {
                const spark = document.createElement('span');
                spark.className = 'sky-spark';
                spark.style.left = `${x}px`;
                spark.style.top = `${y}px`;
                spark.style.backgroundColor = color;
                spark.style.setProperty('--dx', `${(Math.random() - 0.5) * 90}px`);
                document.body.appendChild(spark);
                setTimeout(() => spark.remove(), 880);
            }
        }

        function showToast(msg) {
            const box = document.getElementById('toast-box');
            const txt = document.getElementById('toast-text');
            if (!box || !txt) return;
            txt.textContent = msg;
            box.classList.remove('opacity-0', 'translate-y-4');
            if (state.toastTimer) clearTimeout(state.toastTimer);
            state.toastTimer = setTimeout(() => {
                box.classList.add('opacity-0', 'translate-y-4');
            }, 2600);
        }

        function initWeatherCanvas(canvasId) {
            const canvas = document.getElementById(canvasId);
            if (!canvas) return;
            const ctx = canvas.getContext('2d');
            const particles = Array.from({ length: 28 }, () => ({
                x: Math.random() * 400,
                y: Math.random() * 200,
                speed: 1.2 + Math.random() * 2.4,
                size: 1.5 + Math.random() * 2.2,
                drift: (Math.random() - 0.5) * 1.2
            }));

            function resize() {
                const rect = canvas.getBoundingClientRect();
                if (rect.width > 0 && rect.height > 0) {
                    canvas.width = rect.width;
                    canvas.height = rect.height;
                }
            }
            resize();
            window.addEventListener('resize', resize);

            function draw() {
                if (canvas.width === 0 || canvas.height === 0) resize();
                ctx.clearRect(0, 0, canvas.width, canvas.height);

                particles.forEach(p => {
                    if (state.season === 'rainy') {
                        ctx.strokeStyle = 'rgba(255, 255, 255, 0.32)';
                        ctx.lineWidth = 1.3;
                        ctx.beginPath();
                        ctx.moveTo(p.x, p.y);
                        ctx.lineTo(p.x - 5, p.y + 13);
                        ctx.stroke();

                        p.x -= p.speed * 0.6;
                        p.y += p.speed * 2.2;
                        if (p.y > canvas.height) { p.y = -15; p.x = Math.random() * (canvas.width + 40); }
                        if (p.x < -10) p.x = canvas.width + 10;
                    } else if (state.season === 'dry') {
                        ctx.fillStyle = 'rgba(254, 240, 138, 0.42)';
                        ctx.beginPath();
                        ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
                        ctx.fill();

                        p.y -= p.speed * 0.85;
                        p.x += Math.sin(p.y * 0.04) * 0.7;
                        if (p.y < -10) { p.y = canvas.height + 10; p.x = Math.random() * canvas.width; }
                    } else {
                        ctx.fillStyle = 'rgba(255, 255, 255, 0.24)';
                        ctx.beginPath();
                        ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
                        ctx.fill();

                        p.x += p.speed * 0.45;
                        p.y += Math.sin(p.x * 0.03) * 0.35;
                        if (p.x > canvas.width + 10) { p.x = -10; p.y = Math.random() * canvas.height; }
                    }
                });

                requestAnimationFrame(draw);
            }
            requestAnimationFrame(draw);
        }

        function initInteractions() {
            document.addEventListener('click', e => {
                const btn = e.target.closest('.ripple-btn');
                if (!btn) return;
                const rect = btn.getBoundingClientRect();
                const circle = document.createElement('span');
                const diameter = Math.max(rect.width, rect.height);
                circle.style.width = circle.style.height = `${diameter}px`;
                circle.style.left = `${e.clientX - rect.left - diameter / 2}px`;
                circle.style.top = `${e.clientY - rect.top - diameter / 2}px`;
                circle.className = 'ripple-circle';
                btn.appendChild(circle);
                setTimeout(() => circle.remove(), 580);
            });

            const scrollBody = document.getElementById('mobile-scroll-body');
            let touchStartX = 0;
            if (scrollBody) {
                scrollBody.addEventListener('touchstart', e => {
                    touchStartX = e.changedTouches[0].screenX;
                }, { passive: true });

                scrollBody.addEventListener('touchend', e => {
                    const diffX = e.changedTouches[0].screenX - touchStartX;
                    if (Math.abs(diffX) < 55) return;
                    const idx = tabOrder.indexOf(state.mobTab);
                    if (diffX < 0 && idx < tabOrder.length - 1) {
                        switchMobTab(tabOrder[idx + 1], 'right');
                    } else if (diffX > 0 && idx > 0) {
                        switchMobTab(tabOrder[idx - 1], 'left');
                    }
                }, { passive: true });
            }
        }

        window.addEventListener('DOMContentLoaded', () => {
            setTimeout(() => {
                const gate = document.getElementById('app-entry-doors');
                if (gate) gate.classList.add('hidden');
            }, 1200);

            setLayout('split');
            setScenario('rainy');
            initWeatherCanvas('mob-weather-canvas');
            initWeatherCanvas('pc-weather-canvas');
            initInteractions();
            refreshIcons();
        });
    </script>
</body>
</html>
