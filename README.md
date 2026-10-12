```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Convite Fundo do Mar Encantado</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;500;600;700&family=Quicksand:wght@500;600;700&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Quicksand', sans-serif;
            background: linear-gradient(180deg, #e0f2fe 0%, #bae6fd 40%, #7dd3fc 75%, #38bdf8 100%);
            min-height: 100vh;
            overflow-x: hidden;
            user-select: none;
        }

        .font-fredoka {
            font-family: 'Fredoka', cursive;
        }

        /* Glassmorphism Card Style */
        .glass-card {
            background: rgba(255, 255, 255, 0.82);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 3px solid rgba(255, 255, 255, 0.9);
            box-shadow: 0 20px 50px rgba(14, 116, 144, 0.25);
        }

        /* Float Animations for Sea Creatures */
        @keyframes floatSlow {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-16px) rotate(4deg); }
        }
        @keyframes floatMedium {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(18px) rotate(-5deg); }
        }
        @keyframes floatFast {
            0%, 100% { transform: translateY(0px) scale(1) rotate(0deg); }
            50% { transform: translateY(-22px) scale(1.04) rotate(3deg); }
        }
        @keyframes swimHorizontal {
            0% { transform: translateX(-10px) translateY(0); }
            50% { transform: translateX(12px) translateY(-8px); }
            100% { transform: translateX(-10px) translateY(0); }
        }
        @keyframes wiggling {
            0%, 100% { transform: rotate(-6deg); }
            50% { transform: rotate(6deg); }
        }

        .anim-float-1 { animation: floatSlow 5s ease-in-out infinite; }
        .anim-float-2 { animation: floatMedium 6s ease-in-out infinite 1s; }
        .anim-float-3 { animation: floatFast 4.5s ease-in-out infinite 0.5s; }
        .anim-swim { animation: swimHorizontal 7s ease-in-out infinite; }
        .anim-wiggle { animation: wiggling 2.5s ease-in-out infinite; }

        /* Bubble Particle Canvas Layer */
        #bubbleCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        /* Pulsing Glow for Interactive Elements */
        @keyframes pulseGlow {
            0%, 100% { box-shadow: 0 0 15px rgba(56, 189, 248, 0.4); }
            50% { box-shadow: 0 0 30px rgba(56, 189, 248, 0.8); }
        }
        .pulse-glow {
            animation: pulseGlow 2.5s infinite;
        }

        /* Coral decoration styling */
        .coral-shadow {
            filter: drop-shadow(0px 8px 12px rgba(14, 116, 144, 0.2));
        }

        /* Custom Scrollbar for Modal */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #e0f2fe;
            border-radius: 10px;
        }
        ::-webkit-scrollbar-thumb {
            background: #38bdf8;
            border-radius: 10px;
        }
    </style>
</head>
<body class="relative flex flex-col justify-between min-h-screen text-slate-700 pb-12">

    <!-- Canvas background for rising bubble particles -->
    <canvas id="bubbleCanvas"></canvas>

    <!-- Top Music Toggle Button -->
    <header class="relative z-30 w-full p-4 flex justify-between items-center max-w-4xl mx-auto">
        <div class="flex items-center gap-2 bg-white/70 backdrop-blur-md px-3 py-1.5 rounded-full border border-white/80 shadow-sm">
            <span class="text-xl">🌊</span>
            <span class="text-xs font-bold text-sky-800 uppercase tracking-wider">Fundo do Mar</span>
        </div>

        <button id="audioToggleBtn" onclick="toggleAudio()" class="flex items-center gap-2 bg-white/80 hover:bg-white backdrop-blur-md px-4 py-2 rounded-full border border-sky-200 shadow-md transition-all transform hover:scale-105 active:scale-95 text-sky-700 font-semibold text-xs sm:text-sm">
            <span id="audioIcon">🎵</span>
            <span id="audioText">Música de Fundo</span>
        </button>
    </header>

    <!-- FLOATING ANIMATED CREATURES matching the watercolor image 1000336215.jpg -->
    <div class="fixed inset-0 pointer-events-none z-10 overflow-hidden">
        
        <!-- 1. Caranguejo Laranja com Bochechinhas (Topo Esquerdo) -->
        <div class="absolute top-12 left-2 sm:left-12 w-20 sm:w-28 anim-float-1 pointer-events-auto cursor-pointer hover:scale-110 transition-transform" onclick="popBubble(this)" title="Clique em mim!">
            <svg viewBox="0 0 200 180" class="w-full h-full filter drop-shadow-md">
                <!-- Body -->
                <ellipse cx="100" cy="100" rx="48" ry="36" fill="#FF8A65"/>
                <!-- Watercolor shading effect -->
                <ellipse cx="95" cy="95" rx="42" ry="30" fill="#FF7043" opacity="0.6"/>
                <!-- Eyes -->
                <line x1="80" y1="70" x2="72" y2="50" stroke="#FF7043" stroke-width="6" stroke-linecap="round"/>
                <line x1="120" y1="70" x2="128" y2="50" stroke="#FF7043" stroke-width="6" stroke-linecap="round"/>
                <circle cx="72" cy="48" r="9" fill="#FFFFFF"/>
                <circle cx="72" cy="48" r="4" fill="#374151"/>
                <circle cx="128" cy="48" r="9" fill="#FFFFFF"/>
                <circle cx="128" cy="48" r="4" fill="#374151"/>
                <!-- Claws -->
                <path d="M55 90 Q30 70 35 45 Q55 55 50 80 Z" fill="#FF7043"/>
                <path d="M145 90 Q170 70 165 45 Q145 55 150 80 Z" fill="#FF7043"/>
                <!-- Cheeks & Smile -->
                <circle cx="75" cy="105" r="7" fill="#FF5252" opacity="0.4"/>
                <circle cx="125" cy="105" r="7" fill="#FF5252" opacity="0.4"/>
                <path d="M90 108 Q100 118 110 108" stroke="#8D6E63" stroke-width="3" stroke-linecap="round" fill="none"/>
                <!-- Legs -->
                <path d="M60 120 Q45 135 40 150 M65 125 Q55 145 53 160" stroke="#FF7043" stroke-width="5" stroke-linecap="round"/>
                <path d="M140 120 Q155 135 160 150 M135 125 Q145 145 147 160" stroke="#FF7043" stroke-width="5" stroke-linecap="round"/>
            </svg>
        </div>

        <!-- 2. Tartaruga Aconchegante (Topo Direito) -->
        <div class="absolute top-16 right-3 sm:right-16 w-24 sm:w-32 anim-float-2 pointer-events-auto cursor-pointer hover:scale-110 transition-transform" onclick="popBubble(this)" title="Tartaruguinha!">
            <svg viewBox="0 0 220 160" class="w-full h-full filter drop-shadow-md">
                <!-- Flippers -->
                <ellipse cx="60" cy="110" rx="22" ry="10" fill="#A7F3D0" transform="rotate(-20 60 110)"/>
                <ellipse cx="150" cy="110" rx="22" ry="10" fill="#A7F3D0" transform="rotate(20 150 110)"/>
                <!-- Head sleeping -->
                <ellipse cx="50" cy="80" rx="20" ry="16" fill="#C6F6D5"/>
                <!-- Closed Eye -->
                <path d="M42 82 Q48 88 54 82" stroke="#2F855A" stroke-width="2.5" fill="none" stroke-linecap="round"/>
                <circle cx="58" cy="84" r="4" fill="#F472B6" opacity="0.4"/>
                <!-- Shell watercolor texture -->
                <ellipse cx="110" cy="75" rx="50" ry="38" fill="#86EFAC"/>
                <ellipse cx="110" cy="75" rx="42" ry="32" fill="#4ADE80" opacity="0.7"/>
                <!-- Hexagon pattern on shell -->
                <polygon points="110,50 125,60 125,78 110,88 95,78 95,60" stroke="#15803D" stroke-width="2" fill="none" opacity="0.5"/>
            </svg>
        </div>

        <!-- 3. Polvo Roxo Fofo (Meio Esquerdo) -->
        <div class="absolute top-1/3 left-1 sm:left-8 w-20 sm:w-28 anim-float-3 pointer-events-auto cursor-pointer hover:scale-110 transition-transform" onclick="popBubble(this)">
            <svg viewBox="0 0 200 200" class="w-full h-full filter drop-shadow-md">
                <!-- Tentacles -->
                <path d="M60 130 C40 160 30 180 50 185 C65 185 70 160 80 140" fill="#C084FC"/>
                <path d="M80 140 C70 170 80 190 95 188 C110 185 100 160 100 140" fill="#A855F7"/>
                <path d="M100 140 C110 170 120 190 135 185 C150 180 130 150 120 140" fill="#C084FC"/>
                <path d="M120 140 C140 160 160 175 170 160 C175 145 150 135 140 130" fill="#A855F7"/>
                <!-- Head -->
                <circle cx="100" cy="90" r="48" fill="#E9D5FF"/>
                <circle cx="95" cy="85" r="42" fill="#C084FC" opacity="0.8"/>
                <!-- Eyes & Face -->
                <circle cx="82" cy="88" r="5" fill="#1E293B"/>
                <circle cx="118" cy="88" r="5" fill="#1E293B"/>
                <circle cx="84" cy="86" r="2" fill="#FFFFFF"/>
                <circle cx="120" cy="86" r="2" fill="#FFFFFF"/>
                <circle cx="72" cy="98" r="6" fill="#F472B6" opacity="0.5"/>
                <circle cx="128" cy="98" r="6" fill="#F472B6" opacity="0.5"/>
                <path d="M93 100 Q100 108 107 100" stroke="#4C1D95" stroke-width="2.5" fill="none" stroke-linecap="round"/>
            </svg>
        </div>

        <!-- 4. Baleia Azul Sorridente (Meio Direito) -->
        <div class="absolute top-1/3 right-1 sm:right-6 w-28 sm:w-40 anim-swim pointer-events-auto cursor-pointer hover:scale-110 transition-transform" onclick="popBubble(this)">
            <svg viewBox="0 0 240 180" class="w-full h-full filter drop-shadow-md">
                <!-- Water Spout -->
                <path d="M150 50 Q140 30 120 25 M150 50 Q155 25 170 20 M150 50 Q165 30 180 35" stroke="#BAE6FD" stroke-width="4" stroke-linecap="round" fill="none"/>
                <!-- Main Whale Body -->
                <path d="M30 110 C20 60 100 45 170 65 C210 75 230 110 190 130 C130 155 60 145 30 110 Z" fill="#93C5FD"/>
                <!-- Belly -->
                <path d="M50 115 C70 135 120 145 170 130 C150 115 100 110 50 115 Z" fill="#E0F2FE"/>
                <!-- Tail -->
                <path d="M30 110 C15 95 0 90 5 110 C10 125 25 120 30 110 Z" fill="#60A5FA"/>
                <!-- Eye & Cheek -->
                <circle cx="160" cy="85" r="4" fill="#1E293B"/>
                <circle cx="162" cy="83" r="1.5" fill="#FFFFFF"/>
                <circle cx="175" cy="95" r="6" fill="#F472B6" opacity="0.4"/>
                <path d="M150 100 Q160 108 170 100" stroke="#1E3A8A" stroke-width="2" fill="none" stroke-linecap="round"/>
            </svg>
        </div>

        <!-- 5. Cavalo Marinho Pastel (Inferior Esquerdo) -->
        <div class="absolute bottom-20 left-2 sm:left-10 w-16 sm:w-24 anim-float-2 pointer-events-auto cursor-pointer hover:scale-110 transition-transform" onclick="popBubble(this)">
            <svg viewBox="0 0 140 200" class="w-full h-full filter drop-shadow-md">
                <!-- Head & Snout -->
                <path d="M70 30 C90 30 100 50 85 65 C75 75 70 90 75 110 C80 130 95 145 85 165 C75 180 55 175 60 155 C65 140 55 130 50 110 C45 90 50 30 70 30 Z" fill="#FFEDD5"/>
                <path d="M70 30 C85 30 95 45 80 60" fill="#FED7AA"/>
                <!-- Snout extension -->
                <path d="M85 50 L105 52 C110 53 110 60 104 62 L82 60 Z" fill="#FED7AA"/>
                <!-- Eye -->
                <circle cx="75" cy="45" r="4" fill="#1E293B"/>
                <circle cx="76" cy="44" r="1.5" fill="#FFFFFF"/>
                <circle cx="82" cy="52" r="4" fill="#F472B6" opacity="0.5"/>
                <!-- Back Fin -->
                <path d="M45 90 Q30 100 45 115 Z" fill="#FDE68A"/>
            </svg>
        </div>

        <!-- 6. Peixe Amarelo Dorminhoco (Inferior Direito) -->
        <div class="absolute bottom-24 right-4 sm:right-12 w-20 sm:w-28 anim-float-1 pointer-events-auto cursor-pointer hover:scale-110 transition-transform" onclick="popBubble(this)">
            <svg viewBox="0 0 200 160" class="w-full h-full filter drop-shadow-md">
                <!-- Tail -->
                <path d="M150 80 L185 50 C190 70 190 90 185 110 Z" fill="#93C5FD"/>
                <!-- Body -->
                <ellipse cx="100" cy="80" rx="60" ry="45" fill="#FEF08A"/>
                <ellipse cx="90" cy="80" rx="50" ry="38" fill="#FDE047" opacity="0.7"/>
                <!-- Blue Stripes -->
                <path d="M80 38 Q85 80 80 122 M110 38 Q115 80 110 122" stroke="#60A5FA" stroke-width="6" opacity="0.6" stroke-linecap="round" fill="none"/>
                <!-- Sleeping Eye -->
                <path d="M55 75 Q62 82 70 75" stroke="#1E293B" stroke-width="3" fill="none" stroke-linecap="round"/>
                <circle cx="72" cy="85" r="5" fill="#F472B6" opacity="0.5"/>
            </svg>
        </div>
    </div>

    <!-- MAIN INVITATION CARD CONTAINER -->
    <main class="relative z-20 w-full max-w-xl mx-auto px-4 my-auto">
        <div class="glass-card rounded-3xl p-6 sm:p-10 text-center relative overflow-hidden my-4">
            
            <!-- Floating Decorative Stars inside Card -->
            <div class="absolute top-4 left-6 w-10 h-10 anim-wiggle">
                <!-- Estrela do Mar Amarela -->
                <svg viewBox="0 0 100 100">
                    <polygon points="50,5 64,36 98,36 70,57 81,91 50,70 19,91 30,57 2,36 36,36" fill="#FDE047" stroke="#FACC15" stroke-width="3"/>
                    <circle cx="42" cy="45" r="3" fill="#1E293B"/>
                    <circle cx="58" cy="45" r="3" fill="#1E293B"/>
                    <path d="M46 56 Q50 60 54 56" stroke="#1E293B" stroke-width="2" fill="none"/>
                </svg>
            </div>

            <div class="absolute top-4 right-6 w-10 h-10 anim-wiggle" style="animation-delay: 1s;">
                <!-- Peixe Baiacu Azul -->
                <svg viewBox="0 0 100 100">
                    <circle cx="50" cy="50" r="32" fill="#93C5FD"/>
                    <circle cx="38" cy="45" r="4" fill="#1E293B"/>
                    <circle cx="62" cy="45" r="4" fill="#1E293B"/>
                    <path d="M45 60 Q50 65 55 60" stroke="#1E293B" stroke-width="2" fill="none"/>
                    <path d="M15 50 L5 40 M15 50 L5 60 M85 50 L95 40 M85 50 L95 60" stroke="#60A5FA" stroke-width="3"/>
                </svg>
            </div>

            <!-- Card Header Tag -->
            <div class="inline-block bg-sky-100 text-sky-700 px-4 py-1.5 rounded-full text-xs sm:text-sm font-bold uppercase tracking-widest mb-4 shadow-sm">
                🌊 Convite de Aniversário 🐚
            </div>

            <!-- Title -->
            <h1 class="font-fredoka text-3xl sm:text-5xl text-sky-900 leading-tight mb-2">
                Fundo do Mar do <br>
                <span class="text-sky-500 text-4xl sm:text-6xl drop-shadow-sm" id="childName">Gabriel</span>
            </h1>

            <p class="text-slate-600 font-semibold text-base sm:text-lg mb-6">
                Mergulhe com a gente para comemorar os meus <br>
                <span class="text-amber-500 font-bold font-fredoka text-xl sm:text-2xl" id="childAge">2 Aninhos! 🐠</span>
            </p>

            <!-- Event Details Grid -->
            <div class="bg-white/90 rounded-2xl p-5 sm:p-6 shadow-inner space-y-4 border border-sky-100 mb-6 text-left sm:text-center">
                
                <div class="flex sm:justify-center items-center gap-4">
                    <div class="w-10 h-10 rounded-full bg-sky-100 flex items-center justify-center text-xl shrink-0">
                        📅
                    </div>
                    <div>
                        <p class="text-xs uppercase font-bold text-sky-400">Data Especial</p>
                        <p class="font-bold text-slate-800 text-sm sm:text-base" id="eventDate">Sábado, 21 de Novembro de 2026</p>
                    </div>
                </div>

                <hr class="border-sky-100">

                <div class="flex sm:justify-center items-center gap-4">
                    <div class="w-10 h-10 rounded-full bg-sky-100 flex items-center justify-center text-xl shrink-0">
                        ⏰
                    </div>
                    <div>
                        <p class="text-xs uppercase font-bold text-sky-400">Horário</p>
                        <p class="font-bold text-slate-800 text-sm sm:text-base" id="eventTime">Às 16:00 Horas</p>
                    </div>
                </div>

                <hr class="border-sky-100">

                <div class="flex sm:justify-center items-center gap-4">
                    <div class="w-10 h-10 rounded-full bg-sky-100 flex items-center justify-center text-xl shrink-0">
                        📍
                    </div>
                    <div>
                        <p class="text-xs uppercase font-bold text-sky-400">Local da Aventura</p>
                        <p class="font-bold text-slate-800 text-sm sm:text-base" id="eventLocation">Buffet Oceano Mágico</p>
                        <p class="text-xs text-slate-500" id="eventAddress">Av. Beira Mar, 1000 - Boa Viagem</p>
                    </div>
                </div>
            </div>

            <!-- Action Buttons -->
            <div class="flex flex-col sm:flex-row gap-3">
                <button onclick="openModal()" class="flex-1 py-3.5 px-6 bg-gradient-to-r from-sky-400 to-blue-500 hover:from-sky-500 hover:to-blue-600 text-white font-bold rounded-2xl shadow-lg transition-all transform hover:-translate-y-0.5 active:translate-y-0 pulse-glow flex items-center justify-center gap-2 text-base">
                    <span>💌</span> Confirmar Presença (RSVP)
                </button>
                
                <button onclick="openMap()" class="py-3.5 px-5 bg-white hover:bg-sky-50 text-sky-700 font-bold rounded-2xl border-2 border-sky-200 shadow-md transition-all flex items-center justify-center gap-2 text-sm">
                    <span>🗺️</span> Ver Mapa
                </button>
            </div>

            <p class="text-xs text-slate-400 mt-6">
                Clique nos bichinhos para brincar com eles! 🫧
            </p>

        </div>
    </main>

    <!-- Bottom Watercolor Corals Decorative Illustration -->
    <footer class="relative w-full z-10 pointer-events-none mt-auto">
        <div class="w-full flex justify-between items-end px-2 sm:px-12 -mb-2">
            <!-- Left Coral Cluster -->
            <svg class="w-28 sm:w-48 h-auto coral-shadow" viewBox="0 0 200 150">
                <path d="M20 150 C10 100 40 70 30 40 C25 25 40 20 45 35 C55 70 45 110 50 150 Z" fill="#F472B6"/>
                <path d="M50 150 C40 110 70 80 65 50 C60 35 75 30 80 45 C90 80 75 120 80 150 Z" fill="#FB7185"/>
                <path d="M80 150 C75 120 110 100 115 70 C120 55 130 60 125 75 C115 105 105 130 110 150 Z" fill="#38BDF8"/>
                <!-- Sea anemone dot details -->
                <circle cx="30" cy="40" r="4" fill="#FCE7F3"/>
                <circle cx="65" cy="50" r="4" fill="#FCE7F3"/>
                <circle cx="115" cy="70" r="4" fill="#E0F2FE"/>
            </svg>

            <!-- Right Coral Cluster -->
            <svg class="w-28 sm:w-48 h-auto coral-shadow" viewBox="0 0 200 150">
                <path d="M180 150 C190 100 160 70 170 40 C175 25 160 20 155 35 C145 70 155 110 150 150 Z" fill="#FBBF24"/>
                <path d="M150 150 C160 110 130 80 135 50 C140 35 125 30 120 45 C110 80 125 120 120 150# index.html
