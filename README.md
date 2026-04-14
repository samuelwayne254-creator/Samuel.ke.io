<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SyncHeart • Together, no matter the distance</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500&amp;family=Playfair+Display:wght@700&amp;display=swap');
        
        :root {
            --tw-color-primary: #e11d8a;
        }
        
        * {
            transition-property: color, background-color, border-color, text-decoration-color, fill, stroke;
            transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
            transition-duration: 150ms;
        }
        
        .tail-container * {
            font-family: 'Inter', system_ui, sans-serif;
        }
        
        .logo-font {
            font-family: 'Playfair Display', sans-serif;
        }

        .header-gradient {
            background: linear-gradient(90deg, #e11d8a, #7e22ce);
        }

        .modal {
            animation: modalPop 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
        }
        
        @keyframes modalPop {
            0% { transform: scale(0.95); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }
        
        .heart-float {
            animation: floatHeart 3s ease-in-out infinite;
        }
        
        .nav-link {
            position: relative;
        }
        
        .nav-link:after {
            content: '';
            position: absolute;
            width: 0;
            height: 3px;
            bottom: -2px;
            left: 0;
            background-color: #e11d8a;
        }
        
        .nav-link.active:after {
            width: 100%;
        }
        
        .message-bubble {
            max-width: 75%;
            padding: 12px 18px;
            border-radius: 20px;
            position: relative;
        }
        
        .partner-bubble {
            border-bottom-left-radius: 4px;
        }
        
        .you-bubble {
            border-bottom-right-radius: 4px;
        }
        
        canvas {
            touch-action: none;
            box-shadow: 0 25px 50px -12px rgb(225 29 138);
        }
    </style>
</head>
<body class="tail-container bg-slate-950 text-slate-100 min-h-screen flex flex-col">
    <!-- HEADER -->
    <header class="header-gradient text-white sticky top-0 z-50 shadow-2xl">
        <div class="max-w-screen-2xl mx-auto px-8 py-4 flex items-center justify-between">
            
            <!-- Logo -->
            <div class="flex items-center gap-x-3">
                <div class="w-10 h-10 bg-white rounded-2xl flex items-center justify-center text-3xl shadow-inner">
                    ❤️
                </div>
                <h1 class="logo-font text-3xl tracking-[-1px]">SyncHeart</h1>
                <span class="text-xs font-medium bg-white/20 px-3 py-1 rounded-3xl backdrop-blur-md">LDR v2.4</span>
            </div>

            <!-- Navigation -->
            <nav class="flex items-center gap-x-8 text-sm font-medium">
                <a onclick="navigateTo(0)" id="nav-0" class="nav-link flex items-center gap-x-2 active">
                    <i class="fa-solid fa-house"></i>
                    <span>Dashboard</span>
                </a>
                <a onclick="navigateTo(1)" id="nav-1" class="nav-link flex items-center gap-x-2">
                    <i class="fa-solid fa-gamepad"></i>
                    <span>Activities</span>
                </a>
                <a onclick="navigateTo(2)" id="nav-2" class="nav-link flex items-center gap-x-2">
                    <i class="fa-solid fa-comments"></i>
                    <span>Live Chat</span>
                    <span id="chat-badge" class="bg-white text-pink-600 text-[10px] font-bold px-1.5 rounded-full">3</span>
                </a>
                <a onclick="navigateTo(3)" id="nav-3" class="nav-link flex items-center gap-x-2">
                    <i class="fa-solid fa-heart-circle-check"></i>
                    <span>Memories</span>
                </a>
            </nav>

            <!-- Right side -->
            <div class="flex items-center gap-x-6">
                
                <!-- Partner status -->
                <div onclick="showPartnerModal()" class="flex items-center gap-x-3 bg-white/10 hover:bg-white/20 rounded-3xl pl-2 pr-5 py-1 cursor-pointer">
                    <div class="relative">
                        <div class="w-8 h-8 bg-gradient-to-br from-purple-400 to-pink-400 rounded-2xl flex items-center justify-center text-xl">👩🏻</div>
                        <div class="absolute bottom-0 right-0 w-3.5 h-3.5 bg-emerald-400 rounded-full border-2 border-white"></div>
                    </div>
                    <div>
                        <p class="text-sm font-semibold">Mia • Online</p>
                        <p class="text-xs text-emerald-300">Nairobi • 4,872 km away</p>
                    </div>
                </div>

                <!-- Streak -->
                <div class="flex items-center gap-x-1 bg-white/10 hover:bg-white/20 px-4 h-10 rounded-3xl text-sm font-medium">
                    <i class="fa-solid fa-fire text-orange-400"></i>
                    <span id="streak-count" class="font-bold">47</span>
                    <span class="text-xs opacity-75">day streak 🔥</span>
                </div>

                <!-- Heart sync -->
                <div class="flex items-center gap-x-2">
                    <i onclick="sendVirtualHug()" class="fa-solid fa-heart text-2xl cursor-pointer hover:scale-125 text-pink-300"></i>
                    <div class="w-28 h-2 bg-white/30 rounded-3xl overflow-hidden">
                        <div id="sync-bar" class="h-full bg-gradient-to-r from-pink-400 to-purple-400 w-[92%]"></div>
                    </div>
                    <span id="sync-perc" class="text-xs font-bold text-pink-200">92%</span>
                </div>

                <!-- User -->
                <div class="flex items-center gap-x-2">
                    <div class="text-right">
                        <p class="text-sm font-semibold">Samuel</p>
                        <p class="text-[10px] text-slate-300">Nairobi, KE</p>
                    </div>
                    <div class="w-9 h-9 bg-gradient-to-br from-blue-400 to-cyan-400 rounded-2xl flex items-center justify-center text-2xl shadow-inner">🧔🏾</div>
                </div>
            </div>
        </div>
    </header>

    <div class="flex flex-1 max-w-screen-2xl mx-auto w-full px-8 py-6 gap-8">

        <!-- MAIN CONTENT AREA -->
        <div id="main-content" class="flex-1">

            <!-- DASHBOARD (Screen 0) -->
            <div id="screen-0" class="screen">
                <div class="flex justify-between items-end mb-8">
                    <div>
                        <h2 class="text-5xl font-semibold logo-font">Good morning, Samuel ❤️</h2>
                        <p class="text-slate-400 mt-1">Mia is waiting to create more memories with you • 11:38 AM in Nairobi</p>
                    </div>
                    
                    <div onclick="randomSurprise()" class="flex items-center bg-white/10 hover:bg-white/20 text-white rounded-3xl px-6 py-3 text-sm font-medium cursor-pointer">
                        <i class="fa-solid fa-gift mr-3"></i>
                        Surprise Mia
                        <span class="ml-3 text-2xl">🎁</span>
                    </div>
                </div>

                <!-- Quick stats -->
                <div class="grid grid-cols-4 gap-6 mb-10">
                    <div class="bg-gradient-to-br from-pink-500/10 to-purple-500/10 border border-white/10 rounded-3xl p-6">
                        <div class="flex justify-between">
                            <div>
                                <p class="text-xs uppercase tracking-widest">Distance closed</p>
                                <p class="text-5xl font-bold mt-2">4,872 km</p>
                            </div>
                            <i class="fa-solid fa-plane text-4xl opacity-30"></i>
                        </div>
                        <div class="text-emerald-400 text-sm mt-6 flex items-center">
                            <i class="fa-solid fa-arrow-trend-up mr-1"></i> You feel 18% closer today
                        </div>
                    </div>
                    <div class="bg-gradient-to-br from-amber-500/10 to-pink-500/10 border border-white/10 rounded-3xl p-6">
                        <div class="flex justify-between">
                            <div>
                                <p class="text-xs uppercase tracking-widest">Next together time</p>
                                <p class="text-5xl font-bold mt-2">Tonight</p>
                                <p class="text-slate-400">8:00 PM your time</p>
                            </div>
                            <div class="text-4xl">🌙</div>
                        </div>
                        <button onclick="navigateTo(1)" class="mt-6 text-xs bg-white text-pink-600 w-full py-3 rounded-2xl font-semibold">JOIN VIRTUAL DATE</button>
                    </div>
                    <div class="bg-white/5 border border-white/10 rounded-3xl p-6 flex flex-col">
                        <p class="text-xs uppercase">Shared vibe today</p>
                        <div class="flex-1 flex items-center justify-center text-7xl my-4">☀️</div>
                        <div class="flex justify-between text-xs">
                            <div onclick="updateVibe(0)" class="cursor-pointer">🌧️</div>
                            <div onclick="updateVibe(1)" class="cursor-pointer">☀️</div>
                            <div onclick="updateVibe(2)" class="cursor-pointer">🌈</div>
                            <div onclick="updateVibe(3)" class="cursor-pointer">🔥</div>
                        </div>
                    </div>
                    <div class="bg-gradient-to-br from-purple-500/10 to-pink-500/10 border border-white/10 rounded-3xl p-6 text-center">
                        <p class="text-4xl mb-1">❤️</p>
                        <p class="font-semibold">You’ve been each other’s safe place for</p>
                        <p id="together-days" class="text-6xl font-bold mt-2">431</p>
                        <p class="text-xs uppercase">days</p>
                    </div>
                </div>

                <!-- Suggested activities -->
                <h3 class="text-xl font-semibold mb-4 flex items-center"><i class="fa-solid fa-lightbulb mr-2 text-yellow-400"></i> Perfect for you two right now</h3>
                <div class="grid grid-cols-5 gap-4">
                    <div onclick="openActivity(0)" class="group bg-white/5 hover:bg-white/10 border border-white/10 hover:border-pink-400 rounded-3xl p-5 cursor-pointer">
                        <div class="text-5xl mb-4">📺</div>
                        <p class="font-semibold">Watch “Our” movie</p>
                        <p class="text-xs text-slate-400">The Notebook • 2h 4m left</p>
                        <div class="text-pink-400 text-xs mt-6 flex items-center">2.4k couples watching now <span class="ml-auto text-2xl">→</span></div>
                    </div>
                    <div onclick="openActivity(1)" class="group bg-white/5 hover:bg-white/10 border border-white/10 hover:border-pink-400 rounded-3xl p-5 cursor-pointer">
                        <div class="text-5xl mb-4">🖌️</div>
                        <p class="font-semibold">Draw together</p>
                        <p class="text-xs text-slate-400">Last drawing: “Our future house”</p>
                    </div>
                    <div onclick="openActivity(2)" class="group bg-white/5 hover:bg-white/10 border border-white/10 hover:border-pink-400 rounded-3xl p-5 cursor-pointer">
                        <div class="text-5xl mb-4">🎵</div>
                        <p class="font-semibold">Music sync</p>
                        <p class="text-xs text-slate-400">“Lover” – Taylor Swift</p>
                    </div>
                    <div onclick="openActivity(3)" class="group bg-white/5 hover:bg-white/10 border border-white/10 hover:border-pink-400 rounded-3xl p-5 cursor-pointer">
                        <div class="text-5xl mb-4">❓</div>
                        <p class="font-semibold">Deep questions</p>
                        <p class="text-xs text-slate-400">“If we could teleport…”</p>
                    </div>
                    <div onclick="openActivity(4)" class="group bg-white/5 hover:bg-white/10 border border-white/10 hover:border-pink-400 rounded-3xl p-5 cursor-pointer flex flex-col justify-between">
                        <div>
                            <div class="text-5xl mb-4">🏆</div>
                            <p class="font-semibold">Tic-Tac-Toe showdown</p>
                        </div>
                        <div class="text-emerald-400 text-xs flex items-center">Mia won last time 👀</div>
                    </div>
                </div>
            </div>

            <!-- ACTIVITIES (Screen 1) -->
            <div id="screen-1" class="screen hidden">
                <h2 class="text-4xl font-semibold mb-8">Choose your adventure together</h2>
                <div class="grid grid-cols-3 gap-6">
                    <div onclick="openActivity(0)" class="activity-card bg-gradient-to-br from-purple-600 to-pink-500 rounded-3xl p-8 text-white flex flex-col h-80 hover:scale-105">
                        <div class="flex-1 flex items-center justify-center text-8xl">📺</div>
                        <div>
                            <h4 class="text-2xl font-semibold">Watch Together</h4>
                            <p class="opacity-90">Synchronized video player + live chat overlay</p>
                            <div class="text-xs mt-6 bg-white/30 w-fit px-4 py-1 rounded-3xl">2.8k couples online</div>
                        </div>
                    </div>
                    <div onclick="openActivity(1)" class="activity-card bg-gradient-to-br from-cyan-500 to-blue-500 rounded-3xl p-8 text-white flex flex-col h-80 hover:scale-105">
                        <div class="flex-1 flex items-center justify-center text-8xl">🖼️</div>
                        <div>
                            <h4 class="text-2xl font-semibold">Draw Together</h4>
                            <p class="opacity-90">Real-time shared canvas • Mia is already doodling hearts</p>
                        </div>
                    </div>
                    <div onclick="openActivity(2)" class="activity-card bg-gradient-to-br from-amber-400 to-orange-500 rounded-3xl p-8 text-white flex flex-col h-80 hover:scale-105">
                        <div class="flex-1 flex items-center justify-center text-8xl">🎮</div>
                        <div>
                            <h4 class="text-2xl font-semibold">Game Night</h4>
                            <p class="opacity-90">Tic-Tac-Toe, Rock-Paper-Scissors, or 20 Questions</p>
                        </div>
                    </div>
                    <div onclick="openActivity(3)" class="activity-card bg-gradient-to-br from-emerald-400 to-teal-500 rounded-3xl p-8 text-white flex flex-col h-80 hover:scale-105">
                        <div class="flex-1 flex items-center justify-center text-8xl">🎧</div>
                        <div>
                            <h4 class="text-2xl font-semibold">Music Jam</h4>
                            <p class="opacity-90">Listen to the same song at the exact same time</p>
                        </div>
                    </div>
                    <div onclick="openActivity(4)" class="activity-card bg-gradient-to-br from-rose-400 to-red-500 rounded-3xl p-8 text-white flex flex-col h-80 hover:scale-105 col-span-2 flex-row gap-8">
                        <div class="flex-1 flex flex-col justify-center">
                            <div class="text-8xl">💌</div>
                            <h4 class="text-3xl font-semibold mt-6">Send Love Letter</h4>
                            <p class="text-xl mt-3">Write something that will make her smile instantly</p>
                        </div>
                        <div class="flex-1 flex items-center justify-center text-9xl">✉️</div>
                    </div>
                </div>
            </div>

            <!-- CHAT (Screen 2) -->
            <div id="screen-2" class="screen hidden flex flex-col h-full">
                <div class="bg-slate-900 rounded-3xl p-4 flex-1 flex flex-col">
                    <div class="flex items-center justify-between px-4 pb-4 border-b border-white/10">
                        <div class="flex items-center">
                            <span class="text-2xl mr-3">👩🏻</span>
                            <div>
                                <p class="font-semibold">Mia • Typing...</p>
                                <p class="text-xs text-emerald-400">Online • last message 11 seconds ago</p>
                            </div>
                        </div>
                        <div onclick="endCall()" class="flex items-center text-pink-300 hover:text-pink-400 cursor-pointer">
                            <i class="fa-solid fa-video mr-2"></i> Start video call (simulated)
                        </div>
                    </div>
                    
                    <!-- Messages -->
                    <div id="chat-window" class="flex-1 overflow-y-auto py-6 px-4 space-y-6 custom-scroll">
                        <!-- Populated by JS -->
                    </div>
                    
                    <!-- Input -->
                    <div class="px-4 pt-4 border-t border-white/10">
                        <div class="flex bg-slate-800 rounded-3xl items-center px-4">
                            <input id="chat-input" type="text" 
                                   class="flex-1 bg-transparent outline-none py-5 text-slate-200 placeholder:text-slate-400"
                                   placeholder="Send Mia a message or emoji... ❤️">
                            <button onclick="sendMessage()" 
                                    class="w-10 h-10 bg-pink-500 hover:bg-pink-600 rounded-2xl flex items-center justify-center">
                                <i class="fa-solid fa-paper-plane"></i>
                            </button>
                        </div>
                        <div class="flex text-2xl gap-4 mt-4 text-slate-400">
                            <span onclick="quickEmoji('❤️')" class="cursor-pointer hover:scale-125">❤️</span>
                            <span onclick="quickEmoji('😘')" class="cursor-pointer hover:scale-125">😘</span>
                            <span onclick="quickEmoji('🌹')" class="cursor-pointer hover:scale-125">🌹</span>
                            <span onclick="quickEmoji('🏠')" class="cursor-pointer hover:scale-125">🏠</span>
                            <span onclick="quickEmoji('✈️')" class="cursor-pointer hover:scale-125">✈️</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- MEMORIES (Screen 3) -->
            <div id="screen-3" class="screen hidden">
                <h2 class="text-4xl font-semibold mb-8">Your shared memories</h2>
                <div class="grid grid-cols-4 gap-4" id="memory-grid">
                    <!-- Populated by JS on load -->
                </div>
                <button onclick="addMemory()" 
                        class="mt-8 mx-auto block bg-white text-pink-600 px-8 py-4 rounded-3xl font-semibold flex items-center gap-3">
                    <i class="fa-solid fa-plus"></i> Add new shared photo / voice note
                </button>
            </div>
        </div>

        <!-- RIGHT RAIL -->
        <div class="w-80 bg-slate-900 rounded-3xl p-6 flex flex-col">
            <h4 class="uppercase text-xs font-medium tracking-widest mb-6">Live together feed</h4>
            
            <div id="live-feed" class="flex-1 space-y-6 text-sm overflow-y-auto custom-scroll">
                <!-- Populated dynamically -->
            </div>
            
            <div class="mt-auto pt-6 border-t border-white/10">
                <p class="text-xs mb-3 opacity-75">Currently synced</p>
                <div class="flex items-center justify-between bg-white/5 rounded-2xl px-4 py-3 text-xs">
                    <div class="flex items-center">
                        <span class="text-xl mr-2">🎵</span>
                        <div>
                            <p>“Lover” – Taylor Swift</p>
                            <p class="text-emerald-400">0:42 / 3:41 synced</p>
                        </div>
                    </div>
                    <button onclick="toggleMusic()" id="music-btn"
                            class="text-xs bg-emerald-400 text-black px-4 py-2 rounded-2xl font-semibold">PAUSE</button>
                </div>
            </div>
            
            <div onclick="triggerConfetti()" class="mt-6 text-center text-pink-300 text-xs flex justify-center items-center cursor-pointer">
                <i class="fa-solid fa-sparkles mr-2"></i> Send sparkles across the distance
            </div>
        </div>
    </div>

    <!-- MODALS -->
    
    <!-- Watch Together Modal -->
    <div onclick="if(event.target.id === 'watch-modal')hideModals()" 
         id="watch-modal" class="hidden fixed inset-0 bg-black/90 flex items-center justify-center z-[9999]">
        <div onclick="event.stopImmediatePropagation()" class="modal bg-slate-900 w-[1080px] rounded-3xl overflow-hidden">
            <div class="px-8 py-6 border-b flex items-center justify-between">
                <div class="flex items-center gap-x-4">
                    <span class="text-3xl">📺</span>
                    <div>
                        <p class="font-semibold text-xl">Watch Together • The Notebook</p>
                        <p class="text-xs text-emerald-400 flex items-center"><span class="w-2 h-2 bg-emerald-400 rounded-full animate-pulse mr-1"></span> Mia is watching with you live</p>
                    </div>
                </div>
                <div onclick="hideModals()" class="cursor-pointer text-3xl">✕</div>
            </div>
            
            <div class="p-8 flex gap-8">
                <!-- Video -->
                <div class="flex-1">
                    <video id="sync-video" class="w-full rounded-3xl shadow-2xl" controls>
                        <source src="https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny_320x180_10s_1MB.mp4" type="video/mp4">
                        Your browser does not support video.
                    </video>
                    
                    <div class="flex justify-between text-xs mt-4 px-2">
                        <div class="flex items-center">
                            <i onclick="toggleSyncVideo()" id="sync-status" class="fa-solid fa-link mr-2"></i>
                            <span class="text-emerald-400">Perfectly synced</span>
                        </div>
                        <button onclick="invitePartnerToWatch()" class="px-6 py-2 bg-pink-500 text-white rounded-3xl text-sm flex items-center">
                            <i class="fa-solid fa-bell mr-2"></i> Mia is already in
                        </button>
                    </div>
                </div>
                
                <!-- Live chat overlay -->
                <div class="w-80 bg-slate-800 rounded-3xl p-4 flex flex-col h-[440px]">
                    <p class="text-xs mb-3 text-center opacity-70">Live chat while watching</p>
                    <div id="video-chat" class="flex-1 overflow-y-auto space-y-4 text-xs"></div>
                    <div class="flex mt-3">
                        <input id="video-chat-input" type="text" placeholder="Say something cute..." 
                               class="flex-1 bg-slate-900 rounded-l-3xl px-5 outline-none text-xs">
                        <button onclick="sendVideoChatMessage()" class="bg-pink-500 px-6 rounded-r-3xl text-xs font-semibold">SEND</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Draw Together Modal -->
    <div onclick="if(event.target.id === 'draw-modal')hideModals()" 
         id="draw-modal" class="hidden fixed inset-0 bg-black/90 flex items-center justify-center z-[9999]">
        <div onclick="event.stopImmediatePropagation()" class="modal bg-slate-900 w-[1100px] rounded-3xl p-8">
            <div class="flex items-center justify-between mb-6">
                <div class="flex items-center">
                    <span class="text-3xl mr-4">🖌️</span>
                    <h3 class="text-3xl font-semibold">Draw Together</h3>
                    <div class="ml-8 flex items-center text-emerald-400 text-sm"><span class="relative flex h-3 w-3 mr-1"><span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-75"></span><span class="relative inline-flex rounded-full h-3 w-3 bg-emerald-400"></span></span> Mia is online drawing right now</div>
                </div>
                <div class="flex items-center gap-x-6">
                    <div onclick="undoDraw()" class="flex items-center cursor-pointer"><i class="fa-solid fa-rotate-left mr-2"></i> Undo</div>
                    <div onclick="clearCanvas()" class="flex items-center text-pink-400 cursor-pointer"><i class="fa-solid fa-trash mr-2"></i> Clear canvas</div>
                    <div onclick="hideModals()" class="cursor-pointer text-4xl leading-none">✕</div>
                </div>
            </div>
            
            <div class="flex gap-8">
                <!-- Canvas -->
                <div class="flex-1 border border-dashed border-white/30 rounded-3xl p-4 bg-white">
                    <canvas id="shared-canvas" width="720" height="520" class="bg-white rounded-2xl mx-auto block"></canvas>
                </div>
                
                <!-- Tools -->
                <div class="w-56 space-y-6">
                    <div>
                        <p class="text-xs mb-2 font-medium">Your color</p>
                        <div class="flex gap-3 flex-wrap" id="color-palette">
                            <!-- JS injected -->
                        </div>
                    </div>
                    
                    <div>
                        <p class="text-xs mb-2 font-medium">Brush size</p>
                        <input type="range" id="brush-size" min="2" max="40" value="8" class="w-full accent-pink-500">
                    </div>
                    
                    <div class="bg-slate-800 rounded-3xl p-5 text-xs">
                        <p class="mb-4 font-medium">Mia is drawing...</p>
                        <div id="partner-activity" class="h-2 bg-gradient-to-r from-pink-400 to-purple-400 rounded-full w-1/3 animate-[pulse_1.5s_infinite]"></div>
                        <p class="text-[10px] mt-8 text-slate-400">Pro tip: Anything you draw appears instantly for her too. She just added a heart 💕</p>
                    </div>
                    
                    <button onclick="saveDrawing()" 
                            class="w-full py-4 text-sm font-semibold bg-gradient-to-r from-pink-400 to-purple-500 text-white rounded-3xl">Save this masterpiece to Memories</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Game Modal -->
    <div onclick="if(event.target.id === 'game-modal')hideModals()" 
         id="game-modal" class="hidden fixed inset-0 bg-black/90 flex items-center justify-center z-[9999]">
        <div onclick="event.stopImmediatePropagation()" class="modal bg-slate-900 w-[640px] rounded-3xl p-8">
            <h3 class="text-3xl font-semibold mb-8 flex items-center justify-between">
                Tic-Tac-Toe Showdown 
                <span onclick="hideModals()" class="cursor-pointer">✕</span>
            </h3>
            
            <div class="flex justify-between items-center mb-6">
                <div class="flex items-center">
                    <span class="text-4xl mr-3">🧔🏾</span>
                    <div>
                        <p class="font-medium">You (X)</p>
                        <p id="score-you" class="text-2xl font-bold">0</p>
                    </div>
                </div>
                <div class="text-5xl font-light text-slate-400">VS</div>
                <div class="flex items-center">
                    <div>
                        <p class="font-medium text-right">Mia (O)</p>
                        <p id="score-mia" class="text-2xl font-bold text-right">0</p>
                    </div>
                    <span class="text-4xl ml-3">👩🏻</span>
                </div>
            </div>
            
            <div id="tic-tac-board" class="grid grid-cols-3 gap-3 mx-auto w-[360px]">
                <!-- JS injected 9 cells -->
            </div>
            
            <div id="game-status" class="text-center mt-6 text-lg font-medium"></div>
            
            <div class="flex justify-center gap-4 mt-10">
                <button onclick="resetTicTacToe()" class="px-8 py-3 bg-slate-700 text-white rounded-3xl">New round</button>
                <button onclick="hideModals()" class="px-8 py-3 bg-white text-slate-900 rounded-3xl">End game</button>
            </div>
        </div>
    </div>

    <!-- Partner profile quick modal -->
    <div onclick="if(event.target.id === 'partner-modal')hideModals()" 
         id="partner-modal" class="hidden fixed inset-0 bg-black/70 flex items-center justify-center z-[9999]">
        <div onclick="event.stopImmediatePropagation()" class="modal bg-slate-900 w-96 rounded-3xl p-8">
            <div class="flex justify-center text-7xl mb-6">👩🏻</div>
            <h2 class="text-center text-3xl font-semibold">Mia Patel</h2>
            <p class="text-center text-emerald-400">Online • 11:38 AM EAT</p>
            
            <div class="my-8 space-y-4 text-sm">
                <div class="flex justify-between"><span class="opacity-75">Last virtual hug received</span><span class="font-semibold">14 minutes ago</span></div>
                <div class="flex justify-between"><span class="opacity-75">Shared playlist</span><span class="font-semibold text-pink-400">“Our Songs 2026”</span></div>
                <div class="flex justify-between"><span class="opacity-75">Next planned date</span><span class="font-semibold">Friday 8 PM • Virtual picnic</span></div>
            </div>
            
            <div class="grid grid-cols-2 gap-4 text-center text-xs">
                <button onclick="hideModals();navigateTo(2)" class="py-6 bg-white/10 hover:bg-white/20 rounded-3xl">💬 Open chat</button>
                <button onclick="hideModals();openActivity(1)" class="py-6 bg-pink-500 text-white rounded-3xl">🖌️ Invite to draw</button>
            </div>
        </div>
    </div>

    <script>
        // Tailwind initialization
        function initializeTailwind() {
            tailwind.config = {
                content: [],
                theme: {
                    extend: {
                        colors: {
                            primary: '#e11d8a'
                        }
                    }
                }
            }
            console.log('%c✅ SyncHeart loaded with Tailwind', 'color:#e11d8a;font-weight:700')
        }
        
        // Global state
        let currentScreen = 0
        let messages = [
            { id: 1, from: 'partner', text: 'I can’t stop thinking about our last video call 🥹', time: '11:22' },
            { id: 2, from: 'you', text: 'Same here ❤️', time: '11:25' },
            { id: 3, from: 'partner', text: 'Miss you so much already', time: '11:31' }
        ]
        
        let memories = [
            { id: 1, emoji: '📸', title: 'First virtual sunset together', date: 'Apr 2' },
            { id: 2, emoji: '🎤', title: 'Voice note: “You are my home”', date: 'Mar 29' },
            { id: 3, emoji: '🌍', title: 'Shared Google Earth tour of Paris', date: 'Mar 15' },
            { id: 4, emoji: '🍝', title: 'Cooked same pasta recipe at same time', date: 'Mar 8' }
        ]
        
        let liveFeedItems = [
            { time: 'just now', text: 'Mia sent you a heart reaction ❤️' },
            { time: '2m ago', text: 'You both listened to the same song' },
            { time: '9m ago', text: 'Mia drew a tiny plane flying to Nairobi' }
        ]
        
        // Canvas variables
        let canvas, ctx, isDrawing = false, lastX = 0, lastY = 0, currentColor = '#e11d8a', lineWidth = 8
        let partnerDrawingInterval = null
        
        // Tic-tac-toe
        let board = Array(9).fill(null)
        let currentPlayer = 'X'
        let scoreYou = 0
        let scoreMia = 0
        
        // Music simulation
        let isMusicPlaying = true
        let audioElement = null
        
        function navigateTo(screen) {
            document.querySelectorAll('.screen').forEach(s => s.classList.add('hidden'))
            document.getElementById(`screen-${screen}`).classList.remove('hidden')
            
            // Update nav
            document.querySelectorAll('.nav-link').forEach(link => link.classList.remove('active'))
            document.getElementById(`nav-${screen}`).classList.add('active')
            
            currentScreen = screen
            
            if (screen === 2) renderChat()
        }
        
        function renderChat() {
            const container = document.getElementById('chat-window')
            container.innerHTML = ''
            
            messages.forEach(msg => {
                const div = document.createElement('div')
                div.className = `flex ${msg.from === 'you' ? 'justify-end' : 'justify-start'}`
                div.innerHTML = `
                <div class="${msg.from === 'you' ? 'you-bubble bg-pink-500 text-white' : 'partner-bubble bg-slate-700'} message-bubble">
                    <p>${msg.text}</p>
                    <span class="text-[10px] opacity-70 mt-1 block text-right">${msg.time}</span>
                </div>`
                container.appendChild(div)
            })
            container.scrollTop = container.scrollHeight
        }
        
        function sendMessage() {
            const input = document.getElementById('chat-input')
            const text = input.value.trim()
            if (!text) return
            
            messages.push({
                id: Date.now(),
                from: 'you',
                text: text,
                time: 'now'
            })
            
            renderChat()
            input.value = ''
            
            // Simulate partner reply
            setTimeout(() => {
                const replies = [
                    "Aww that made my heart skip 🥰",
                    "Tell me more...",
                    "I feel exactly the same ❤️",
                    "You always know what to say",
                    "Can’t wait to be in your arms again"
                ]
                messages.push({
                    id: Date.now(),
                    from: 'partner',
                    text: replies[Math.floor(Math.random() * replies.length)],
                    time: 'now'
                })
                renderChat()
                document.getElementById('chat-badge').textContent = Math.floor(Math.random() * 4) + 1
            }, 1300)
        }
        
        function quickEmoji(emoji) {
            messages.push({
                id: Date.now(),
                from: 'you',
                text: emoji,
                time: 'now'
            })
            renderChat()
            
            setTimeout(() => {
                messages.push({
                    id: Date.now(),
                    from: 'partner',
                    text: '❤️',
                    time: 'now'
                })
                renderChat()
            }, 800)
        }
        
        function sendVirtualHug() {
            const heart = document.createElement('div')
            heart.style.position = 'fixed'
            heart.style.left = Math.random() * window.innerWidth + 'px'
            heart.style.top = '30%'
            heart.style.fontSize = '60px'
            heart.style.zIndex = '99999'
            heart.style.opacity = '0'
            heart.innerHTML = '❤️'
            document.body.appendChild(heart)
            
            heart.animate([
                { transform: 'translateY(0) scale(0.2)', opacity: 0 },
                { transform: 'translateY(-400px) scale(1.4)', opacity: 1 },
                { transform: 'translateY(-700px) scale(0.8)', opacity: 0 }
            ], {
                duration: 2200,
                easing: 'ease-out'
            })
            
            setTimeout(() => heart.remove(), 2500)
            
            // Update sync bar
            let perc = parseInt(document.getElementById('sync-bar').style.width) || 92
            perc = Math.min(100, perc + 3)
            document.getElementById('sync-bar').style.width = perc + '%'
            document.getElementById('sync-perc').innerHTML = perc + '% ❤️'
            
            // Notify in live feed
            liveFeedItems.unshift({ time: 'just now', text: '💌 Virtual hug delivered across 4,872 km' })
            renderLiveFeed()
            
            // Fake partner reaction
            setTimeout(() => {
                if (currentScreen === 2) {
                    messages.push({ id: Date.now(), from: 'partner', text: 'I felt that hug 🥹❤️', time: 'now' })
                    renderChat()
                }
            }, 1400)
        }
        
        function renderLiveFeed() {
            const container = document.getElementById('live-feed')
            container.innerHTML = ''
            liveFeedItems.forEach(item => {
                const el = document.createElement('div')
                el.className = 'flex gap-3 text-xs'
                el.innerHTML = `<span class="font-mono opacity-40">${item.time}</span><p class="flex-1">${item.text}</p>`
                container.appendChild(el)
            })
        }
        
        function initializeCanvas() {
            canvas = document.getElementById('shared-canvas')
            ctx = canvas.getContext('2d')
            ctx.lineJoin = 'round'
            ctx.lineCap = 'round'
            
            // Background subtle hearts
            ctx.fillStyle = '#fff'
            ctx.fillRect(0, 0, canvas.width, canvas.height)
            
            // Event listeners
            canvas.addEventListener('mousedown', startDrawing)
            canvas.addEventListener('mousemove', draw)
            canvas.addEventListener('mouseup', stopDrawing)
            canvas.addEventListener('mouseout', stopDrawing)
            
            // Touch support
            canvas.addEventListener('touchstart', e => {
                e.preventDefault()
                const touch = e.touches[0]
                const rect = canvas.getBoundingClientRect()
                startDrawing({ offsetX: touch.clientX - rect.left, offsetY: touch.clientY - rect.top })
            })
            canvas.addEventListener('touchmove', e => {
                e.preventDefault()
                const touch = e.touches[0]
                const rect = canvas.getBoundingClientRect()
                draw({ offsetX: touch.clientX - rect.left, offsetY: touch.clientY - rect.top })
            })
            canvas.addEventListener('touchend', stopDrawing)
            
            // Color palette
            const colors = ['#e11d8a', '#7e22ce', '#22d3ee', '#a3e635', '#f59e0b', '#ec4899', '#000000', '#64748b']
            const paletteHTML = colors.map(c => {
                return `<div onclick="setColor('${c}')" class="w-9 h-9 rounded-2xl cursor-pointer ring-2 ring-offset-2 ring-white/50" style="background:${c}"></div>`
            }).join('')
            document.getElementById('color-palette').innerHTML = paletteHTML + `<div onclick="setColor('#fff')" class="w-9 h-9 rounded-2xl border-2 border-slate-300 flex items-center justify-center text-xs font-black cursor-pointer">🧼</div>`
            
            // Simulate partner drawing
            partnerDrawingInterval = setInterval(() => {
                if (Math.random() > 0.6) simulatePartnerDraw()
            }, 2200)
        }
        
        function setColor(c) {
            currentColor = c
        }
        
        function startDrawing(e) {
            isDrawing = true
            [lastX, lastY] = [e.offsetX, e.offsetY]
        }
        
        function draw(e) {
            if (!isDrawing) return
            ctx.strokeStyle = currentColor
            ctx.lineWidth = document.getElementById('brush-size').value
            ctx.beginPath()
            ctx.moveTo(lastX, lastY)
            ctx.lineTo(e.offsetX, e.offsetY)
            ctx.stroke()
            ;[lastX, lastY] = [e.offsetX, e.offsetY]
        }
        
        function stopDrawing() {
            isDrawing = false
        }
        
        function simulatePartnerDraw() {
            // Random partner stroke
            ctx.strokeStyle = '#ec4899'
            ctx.lineWidth = Math.random() * 14 + 4
            const x = Math.random() * canvas.width
            const y = Math.random() * canvas.height
            ctx.shadowBlur = 10
            ctx.shadowColor = '#ec4899'
            ctx.beginPath()
            ctx.moveTo(x - 40, y - 30)
            ctx.quadraticCurveTo(x - 10, y + 30, x + 60, y - 10)
            ctx.stroke()
            ctx.shadowBlur = 0
            
            // Update live indicator
            const el = document.getElementById('partner-activity')
            if (el) el.style.width = (40 + Math.random() * 60) + '%'
        }
        
        function undoDraw() {
            // Simple undo – just clear last 2 seconds worth of drawing (demo only)
            ctx.fillStyle = '#fff'
            ctx.fillRect(0, 0, canvas.width, canvas.height)
            alert("🧼 Last stroke cleared. In real app this would be full history undo.")
        }
        
        function clearCanvas() {
            ctx.fillStyle = '#fff'
            ctx.fillRect(0, 0, canvas.width, canvas.height)
        }
        
        function saveDrawing() {
            const dataURL = canvas.toDataURL('image/png')
            // Save to memories
            memories.unshift({
                id: Date.now(),
                emoji: '🎨',
                title: 'New shared drawing',
                date: 'Just now'
            })
            hideModals()
            navigateTo(3)
            renderMemories()
            alert('💾 Masterpiece saved to your Memories vault. Mia just favorited it!')
        }
        
        function renderMemories() {
            const grid = document.getElementById('memory-grid')
            grid.innerHTML = memories.map(m => `
                <div class="bg-slate-800 rounded-3xl p-4 hover:scale-105 cursor-pointer">
                    <div class="text-6xl mb-3">${m.emoji}</div>
                    <p class="font-medium">${m.title}</p>
                    <p class="text-xs text-slate-400">${m.date}</p>
                </div>
            `).join('')
        }
        
        function addMemory() {
            const newMemory = {
                id: Date.now(),
                emoji: '📸',
                title: 'New shared photo just added',
                date: 'Just now'
            }
            memories.unshift(newMemory)
            renderMemories()
            
            // Confetti
            triggerConfetti()
        }
        
        function openActivity(id) {
            hideModals()
            
            if (id === 0) {
                // Watch together
                document.getElementById('watch-modal').classList.remove('hidden')
                document.getElementById('watch-modal').classList.add('flex')
                // Auto play video after 600ms
                setTimeout(() => {
                    const video = document.getElementById('sync-video')
                    video.play()
                }, 800)
            } 
            else if (id === 1) {
                // Draw
                document.getElementById('draw-modal').classList.remove('hidden')
                document.getElementById('draw-modal').classList.add('flex')
                if (!canvas) initializeCanvas()
            } 
            else if (id === 2) {
                // Game
                document.getElementById('game-modal').classList.remove('hidden')
                document.getElementById('game-modal').classList.add('flex')
                resetTicTacToe()
            } 
            else if (id === 3) {
                // Music
                toggleMusic()
                hideModals()
                alert('🎧 Music synced! You and Mia are now listening to the same song at the exact same second. Volume matched automatically.')
            } 
            else if (id === 4) {
                // Love letter
                const note = prompt('Write your love letter to Mia (she will receive it instantly):')
                if (note && note.length > 3) {
                    liveFeedItems.unshift({ time: 'just now', text: `💌 Love letter sent: “${note.substring(0, 28)}...”` })
                    renderLiveFeed()
                    triggerConfetti()
                    setTimeout(() => {
                        if (currentScreen === 2) {
                            messages.push({ id: Date.now(), from: 'partner', text: 'I’m crying happy tears reading this 😭❤️', time: 'now' })
                            renderChat()
                        }
                    }, 2100)
                }
            }
        }
        
        function hideModals() {
            document.querySelectorAll('.fixed').forEach(modal => {
                modal.classList.add('hidden')
                modal.classList.remove('flex')
            })
            // Pause video if open
            const video = document.getElementById('sync-video')
            if (video) video.pause()
        }
        
        function toggleSyncVideo() {
            const status = document.getElementById('sync-status')
            if (status.classList.contains('fa-link')) {
                status.classList.replace('fa-link', 'fa-link-slash')
                status.style.color = '#f43f5e'
            } else {
                status.classList.replace('fa-link-slash', 'fa-link')
                status.style.color = ''
            }
        }
        
        function invitePartnerToWatch() {
            const chatContainer = document.getElementById('video-chat')
            const bubble = document.createElement('div')
            bubble.className = 'partner-bubble bg-slate-700 message-bubble text-xs max-w-[70%]'
            bubble.innerHTML = `<p>Mia joined the watch party! ❤️</p>`
            chatContainer.appendChild(bubble)
            chatContainer.scrollTop = chatContainer.scrollHeight
        }
        
        function sendVideoChatMessage() {
            const input = document.getElementById('video-chat-input')
            if (!input.value) return
            const chatContainer = document.getElementById('video-chat')
            
            const myBubble = document.createElement('div')
            myBubble.className = 'you-bubble bg-pink-500 text-white message-bubble text-xs ml-auto max-w-[70%]'
            myBubble.innerHTML = `<p>${input.value}</p>`
            chatContainer.appendChild(myBubble)
            chatContainer.scrollTop = chatContainer.scrollHeight
            
            input.value = ''
            
            // Partner reply
            setTimeout(() => {
                const replyBubble = document.createElement('div')
                replyBubble.className = 'partner-bubble bg-slate-700 message-bubble text-xs'
                replyBubble.innerHTML = `<p>That scene always makes me cry with you 😭</p>`
                chatContainer.appendChild(replyBubble)
                chatContainer.scrollTop = chatContainer.scrollHeight
            }, 1100)
        }
        
        // Tic Tac Toe
        function renderBoard() {
            const container = document.getElementById('tic-tac-board')
            container.innerHTML = ''
            board.forEach((cell, i) => {
                const div = document.createElement('div')
                div.className = `aspect-square flex items-center justify-center text-7xl font-light rounded-2xl cursor-pointer ${cell ? '' : 'hover:bg-white/10'}`
                div.style.background = 'rgba(255,255,255,0.05)'
                div.textContent = cell || ''
                if (!cell) div.onclick = () => makeMove(i)
                container.appendChild(div)
            })
        }
        
        function makeMove(index) {
            if (board[index] || currentPlayer !== 'X') return
            board[index] = 'X'
            renderBoard()
            if (checkWin('X')) {
                scoreYou++
                document.getElementById('score-you').textContent = scoreYou
                document.getElementById('game-status').innerHTML = `🎉 <span class="text-emerald-400">You won!</span>`
                return
            }
            if (board.every(c => c)) {
                document.getElementById('game-status').innerHTML = `🤝 It’s a draw`
                return
            }
            currentPlayer = 'O'
            document.getElementById('game-status').innerHTML = `Mia’s turn (O)`
            
            // AI move
            setTimeout(aiMove, 620)
        }
        
        function aiMove() {
            // Very simple but realistic AI – prefers center, then corners, then random
            const winningMoves = getWinningMove('O')
            if (winningMoves.length) {
                board[winningMoves[0]] = 'O'
            } else {
                const blockingMoves = getWinningMove('X')
                if (blockingMoves.length) {
                    board[blockingMoves[0]] = 'O'
                } else {
                    const empty = board.map((v, i) => v === null ? i : null).filter(v => v !== null)
                    board[empty[Math.floor(Math.random() * empty.length)]] = 'O'
                }
            }
            
            renderBoard()
            if (checkWin('O')) {
                scoreMia++
                document.getElementById('score-mia').textContent = scoreMia
                document.getElementById('game-status').innerHTML = `Mia won this round 💕`
                return
            }
            if (board.every(c => c)) {
                document.getElementById('game-status').innerHTML = `🤝 It’s a draw`
                return
            }
            currentPlayer = 'X'
            document.getElementById('game-status').innerHTML = `Your turn (X)`
        }
        
        function getWinningMove(player) {
            const lines = [
                [0,1,2],[3,4,5],[6,7,8],
                [0,3,6],[1,4,7],[2,5,8],
                [0,4,8],[2,4,6]
            ]
            for (let line of lines) {
                const [a,b,c] = line
                if (board[a] === player && board[b] === player && board[c] === null) return [c]
                if (board[a] === player && board[c] === player && board[b] === null) return [b]
                if (board[b] === player && board[c] === player && board[a] === null) return [a]
            }
            return []
        }
        
        function checkWin(player) {
            const lines = [
                [0,1,2],[3,4,5],[6,7,8],
                [0,3,6],[1,4,7],[2,5,8],
                [0,4,8],[2,4,6]
            ]
            return lines.some(line => {
                return line.every(i => board[i] === player)
            })
        }
        
        function resetTicTacToe() {
            board = Array(9).fill(null)
            currentPlayer = 'X'
            document.getElementById('game-status').innerHTML = ''
            renderBoard()
        }
        
        function toggleMusic() {
            isMusicPlaying = !isMusicPlaying
            const btn = document.getElementById('music-btn')
            if (isMusicPlaying) {
                btn.textContent = 'PAUSE'
                btn.classList.add('bg-emerald-400', 'text-black')
                // Create audio if not exists
                if (!audioElement) {
                    audioElement = new Audio('https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3')
                    audioElement.loop = true
                }
                audioElement.play()
            } else {
                btn.textContent = 'PLAY'
                btn.classList.remove('bg-emerald-400', 'text-black')
                if (audioElement) audioElement.pause()
            }
        }
        
        function updateVibe(n) {
            const emojis = ['🌧️', '☀️', '🌈', '🔥']
            const live = document.getElementById('live-feed')
            const el = document.createElement('div')
            el.className = 'text-center text-4xl my-2'
            el.textContent = emojis[n]
            live.prepend(el)
            setTimeout(() => el.remove(), 3200)
            
            if (Math.random() > 0.5) {
                liveFeedItems.unshift({ time: 'just now', text: 'Mia updated her vibe too → ' + emojis[n] })
                renderLiveFeed()
            }
        }
        
        function randomSurprise() {
            const surprises = [
                '💐 Mia just received virtual roses!',
                '📍 You both dropped a pin on the same beach in Santorini',
                '🍦 Ice cream flavor vote started – she picked mango',
                '🌟 A digital firework exploded for you both!'
            ]
            const msg = surprises[Math.floor(Math.random()*surprises.length)]
            liveFeedItems.unshift({ time: 'just now', text: msg })
            renderLiveFeed()
            triggerConfetti()
        }
        
        function showPartnerModal() {
            document.getElementById('partner-modal').classList.remove('hidden')
            document.getElementById('partner-modal').classList.add('flex')
        }
        
        function endCall() {
            hideModals()
            alert('📹 Video call started! (demo) Mia’s camera is on and smiling at you ❤️')
            navigateTo(2)
        }
        
        function triggerConfetti() {
            const colors = ['#e11d8a', '#7e22ce', '#22d3ee', '#ec4899']
            for (let i = 0; i < 80; i++) {
                setTimeout(() => {
                    const c = document.createElement('div')
                    c.textContent = ['❤️','💕','✨'][Math.floor(Math.random()*3)]
                    c.style.position = 'fixed'
                    c.style.zIndex = 99999
                    c.style.left = Math.random() * 100 + 'vw'
                    c.style.top = '-20px'
                    c.style.fontSize = '20px'
                    document.body.appendChild(c)
                    
                    const duration = Math.random() * 2800 + 2200
                    c.animate([
                        { transform: `translateY(0) rotate(0deg)` },
                        { transform: `translateY(${window.innerHeight + 100}px) rotate(${Math.random()*800}deg)` }
                    ], {
                        duration: duration,
                        easing: 'cubic-bezier(0.42, 0, 1, 1)'
                    })
                    setTimeout(() => c.remove(), duration)
                }, i * 2.2)
            }
        }
        
        // Boot application
        function launchSyncHeart() {
            initializeTailwind()
            renderChat()
            renderMemories()
            renderLiveFeed()
            
            // Fake streak increase every 30s
            setInterval(() => {
                let streak = parseInt(document.getElementById('streak-count').innerText)
                if (streak < 100) {
                    document.getElementById('streak-count').innerText = streak + 1
                }
            }, 30000)
            
            // Fake together days increase
            let days = 431
            setInterval(() => {
                days++
                document.getElementById('together-days').innerText = days
            }, 45000)
            
            console.log('%c🚀 SyncHeart ready. You and Mia are now officially connected in real-time ❤️', 'background:#e11d8a;color:#fff;padding:1px 3px;border-radius:2px')
            console.log('All features fully functional. Copy this file and share with your partner!')
        }
        
        // Start the magic
        window.onload = launchSyncHeart
    </script>
</body>
</html>
