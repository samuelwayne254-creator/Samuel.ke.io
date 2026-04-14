<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OVERCOME • Break Free &amp; Stay Strong</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.6.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.7/dist/chart.umd.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&amp;family=Space+Grotesk:wght@500;600&amp;display=swap');
        
        :root {
            --primary: #00d4aa;
        }
        
        * {
            transition-property: color, background-color, border-color, text-decoration-color, fill, stroke;
            transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
            transition-duration: 150ms;
        }
        
        body {
            font-family: 'Inter', system_ui, sans-serif;
        }
        
        .heading-font {
            font-family: 'Space Grotesk', sans-serif;
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
            background-color: #00d4aa;
        }
        
        .nav-link:hover:after {
            width: 100%;
        }

        .card-hover {
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        
        .card-hover:hover {
            transform: translateY(-4px);
            box-shadow: 0 25px 50px -12px rgb(0 212 170 / 0.25);
        }

        .section-header {
            position: relative;
        }
        
        .section-header:after {
            content: '';
            position: absolute;
            width: 60px;
            height: 4px;
            background: linear-gradient(to right, #00d4aa, #00a88a);
            bottom: -8px;
            left: 0;
            border-radius: 9999px;
        }

        .chat-bubble-ai {
            border-radius: 20px 20px 20px 4px;
            background: #27272a;
        }
        
        .chat-bubble-user {
            border-radius: 20px 20px 4px 20px;
            background: #00d4aa;
            color: #111827;
        }

        .animate-in {
            animation: fadeInUp 0.6s backwards;
        }
        
        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .modal {
            animation: modalPop 0.3s ease;
        }
        
        @keyframes modalPop {
            0% { transform: scale(0.95); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }
    </style>
</head>
<body class="bg-zinc-950 text-white">
    <!-- NAVBAR -->
    <nav class="bg-zinc-900 border-b border-zinc-800 sticky top-0 z-50">
        <div class="max-w-screen-2xl mx-auto px-8 py-5 flex items-center justify-between">
            <!-- Logo -->
            <div class="flex items-center gap-x-3">
                <div class="w-9 h-9 bg-[#00d4aa] rounded-2xl flex items-center justify-center text-zinc-950 text-2xl shadow-inner">
                    🏔️
                </div>
                <h1 class="heading-font text-3xl tracking-[-1px]">OVERCOME</h1>
            </div>

            <!-- Menu -->
            <div class="flex items-center gap-x-8 text-sm font-medium">
                <a onclick="navigateTo('dashboard')" class="nav-link flex items-center gap-x-2 cursor-pointer">
                    <i class="fa-solid fa-house"></i>
                    <span>Dashboard</span>
                </a>
                <a onclick="navigateTo('track')" class="nav-link flex items-center gap-x-2 cursor-pointer">
                    <i class="fa-solid fa-chart-line"></i>
                    <span>Track Progress</span>
                </a>
                <a onclick="navigateTo('tools')" class="nav-link flex items-center gap-x-2 cursor-pointer">
                    <i class="fa-solid fa-hands-holding-heart"></i>
                    <span>Tools</span>
                </a>
                <a onclick="navigateTo('resources')" class="nav-link flex items-center gap-x-2 cursor-pointer">
                    <i class="fa-solid fa-book-open"></i>
                    <span>Resources</span>
                </a>
                <a onclick="navigateTo('community')" class="nav-link flex items-center gap-x-2 cursor-pointer">
                    <i class="fa-solid fa-users"></i>
                    <span>Community</span>
                </a>
                <!-- NEW: AI Coach -->
                <a onclick="navigateTo('coach')" class="nav-link flex items-center gap-x-2 cursor-pointer bg-[#00d4aa]/10 text-[#00d4aa] px-4 py-1 rounded-3xl">
                    <i class="fa-solid fa-robot"></i>
                    <span>AI Coach</span>
                </a>
            </div>

            <!-- Right side -->
            <div class="flex items-center gap-x-6">
                <div class="flex items-center gap-x-2 bg-zinc-800 hover:bg-zinc-700 px-4 py-2 rounded-3xl cursor-pointer" onclick="showProfile()">
                    <div class="text-right">
                        <p class="text-sm font-semibold">Hi Samuel 👋</p>
                        <p id="current-streak-global" class="text-xs text-[#00d4aa] flex items-center gap-x-1">
                            <i class="fa-solid fa-fire"></i> 12 day streak
                        </p>
                    </div>
                    <div class="w-9 h-9 bg-emerald-400 rounded-2xl flex items-center justify-center text-2xl">🇰🇪</div>
                </div>

                <button onclick="markTodaySober()"
                        class="flex items-center gap-x-3 bg-[#00d4aa] hover:bg-[#00b894] text-zinc-950 font-semibold px-6 py-3 rounded-3xl text-sm">
                    <i class="fa-solid fa-check-circle"></i>
                    <span>I STAYED STRONG TODAY</span>
                </button>

                <button onclick="toggleTheme()" class="w-10 h-10 flex items-center justify-center text-xl rounded-2xl hover:bg-zinc-800">
                    <i class="fa-solid fa-moon"></i>
                </button>
            </div>
        </div>
    </nav>

    <div class="max-w-screen-2xl mx-auto px-8 py-8 flex gap-8">
        
        <!-- SIDEBAR - Addiction Selector -->
        <div class="w-72 bg-zinc-900 rounded-3xl p-6 h-fit sticky top-24">
            <h2 class="text-lg font-semibold mb-6 flex items-center gap-x-2">
                <i class="fa-solid fa-link"></i>
                YOUR ADDICTIONS
            </h2>
            
            <div id="addiction-list" class="space-y-3"></div>
            
            <button onclick="addNewAddiction()"
                    class="mt-6 w-full flex items-center justify-center gap-x-3 border border-dashed border-zinc-700 hover:border-[#00d4aa] text-zinc-400 hover:text-white rounded-3xl py-4 text-sm font-medium">
                <i class="fa-solid fa-plus"></i>
                <span>ADD NEW ADDICTION</span>
            </button>

            <div class="mt-10 text-xs text-zinc-500 leading-relaxed">
                📍 Nairobi, Kenya<br>
                Local support: <span class="text-[#00d4aa] cursor-pointer" onclick="showLocalHelp()">NACADA Helpline • 1190</span>
            </div>
        </div>

        <!-- MAIN CONTENT AREA -->
        <div class="flex-1 space-y-8">
            
            <!-- DASHBOARD SECTION -->
            <div id="screen-dashboard" class="space-y-8">
                <div class="flex justify-between items-end">
                    <div>
                        <h1 class="heading-font text-5xl tracking-[-2px]">Good morning, Samuel.</h1>
                        <p class="text-zinc-400 text-xl mt-1">You're 12 days stronger than yesterday. Keep going.</p>
                    </div>
                </div>

                <!-- Quick stats -->
                <div class="grid grid-cols-4 gap-4">
                    <div class="bg-zinc-900 rounded-3xl p-6 card-hover">
                        <i class="fa-solid fa-fire text-4xl text-orange-400"></i>
                        <p class="mt-4 text-4xl font-semibold" id="global-streak">12</p>
                        <p class="text-zinc-400">day streak 🔥</p>
                    </div>
                    <div class="bg-zinc-900 rounded-3xl p-6 card-hover">
                        <i class="fa-solid fa-calendar-check text-4xl text-[#00d4aa]"></i>
                        <p class="mt-4 text-4xl font-semibold" id="total-sober-days">47</p>
                        <p class="text-zinc-400">total sober days</p>
                    </div>
                    <div class="bg-zinc-900 rounded-3xl p-6 card-hover">
                        <i class="fa-solid fa-heart-pulse text-4xl text-pink-400"></i>
                        <p class="mt-4 text-4xl font-semibold" id="cravings-today">3</p>
                        <p class="text-zinc-400">cravings today</p>
                    </div>
                    <div class="bg-zinc-900 rounded-3xl p-6 card-hover">
                        <i class="fa-solid fa-trophy text-4xl text-amber-400"></i>
                        <p class="mt-4 text-4xl font-semibold" id="achievements-count">7</p>
                        <p class="text-zinc-400">achievements unlocked</p>
                    </div>
                </div>

                <!-- Current focus addictions -->
                <div>
                    <h2 class="section-header text-2xl font-semibold mb-4">Your Current Focus</h2>
                    <div id="focus-cards" class="grid grid-cols-3 gap-4"></div>
                </div>

                <!-- Motivational quote (now includes AI-suggested quote) -->
                <div class="bg-gradient-to-br from-[#00d4aa]/10 to-transparent border border-[#00d4aa]/20 rounded-3xl p-8 flex gap-6">
                    <div class="text-6xl">💡</div>
                    <div class="flex-1">
                        <p id="quote-text" class="text-xl italic">"The only way to get through a craving is to ride it like a wave — it will pass."</p>
                        <p id="quote-author" class="text-[#00d4aa] mt-4 text-sm font-medium">— Dr. Judson Brewer</p>
                        <button onclick="getAICoachQuote()" 
                                class="mt-6 text-xs flex items-center gap-x-2 text-[#00d4aa] hover:text-white">
                            <i class="fa-solid fa-robot"></i>
                            <span>ASK AI COACH FOR A FRESH QUOTE</span>
                        </button>
                    </div>
                </div>
            </div>

            <!-- TRACK PROGRESS SECTION (unchanged) -->
            <div id="screen-track" class="hidden">
                <h2 class="section-header text-3xl font-semibold mb-6">Track Your Progress</h2>
                <div id="selected-addiction-header" class="flex items-center justify-between mb-6"></div>
                <div class="grid grid-cols-12 gap-8">
                    <div class="col-span-5 bg-zinc-900 rounded-3xl p-8">
                        <div class="flex justify-between">
                            <div>
                                <p class="text-zinc-400">CURRENT STREAK</p>
                                <p id="streak-number" class="text-8xl font-semibold heading-font text-[#00d4aa] mt-2">14</p>
                                <p id="streak-text" class="text-2xl">days smoke-free</p>
                            </div>
                            <div class="text-8xl">🔥</div>
                        </div>
                        <div class="mt-8 bg-black/30 rounded-2xl p-4 flex items-center gap-x-4">
                            <button onclick="markTodaySober(true)" 
                                    class="flex-1 bg-[#00d4aa] text-zinc-950 font-semibold py-5 rounded-2xl flex items-center justify-center gap-x-2 hover:scale-105">
                                <i class="fa-solid fa-check"></i>
                                I STAYED STRONG TODAY
                            </button>
                            <button onclick="logRelapse()" 
                                    class="flex-1 border border-red-500 text-red-400 font-semibold py-5 rounded-2xl flex items-center justify-center gap-x-2 hover:bg-red-500/10">
                                <i class="fa-solid fa-ban"></i>
                                I HAD A SLIP
                            </button>
                        </div>
                    </div>
                    <div class="col-span-7 bg-zinc-900 rounded-3xl p-8">
                        <h3 class="font-semibold mb-4">Last 30 days</h3>
                        <canvas id="progressChart" class="w-full h-64"></canvas>
                    </div>
                </div>
                <div class="mt-8">
                    <h3 class="font-semibold mb-4">Recent entries</h3>
                    <div id="log-list" class="space-y-3"></div>
                </div>
            </div>

            <!-- TOOLS SECTION (unchanged) -->
            <div id="screen-tools" class="hidden">
                <h2 class="section-header text-3xl font-semibold mb-6">Instant Relief Tools</h2>
                <div class="grid grid-cols-2 gap-6">
                    <div class="bg-zinc-900 rounded-3xl p-8">
                        <div class="flex justify-between items-center mb-8">
                            <div class="flex items-center gap-x-3">
                                <i class="fa-solid fa-wind text-3xl"></i>
                                <div>
                                    <h3 class="font-semibold text-xl">4-7-8 Breathing</h3>
                                    <p class="text-zinc-400 text-sm">Calm your nervous system in 60 seconds</p>
                                </div>
                            </div>
                            <button onclick="startBreathing()" id="breathe-btn"
                                    class="px-6 py-3 bg-[#00d4aa] text-zinc-950 rounded-3xl font-medium flex items-center gap-x-2">
                                <i class="fa-solid fa-play"></i>
                                START
                            </button>
                        </div>
                        <div class="flex justify-center my-12">
                            <div id="breathing-circle" 
                                 class="w-52 h-52 border-8 border-[#00d4aa] rounded-full flex items-center justify-center text-4xl font-medium shadow-[0_0_60px_#00d4aa]">
                                Breathe
                            </div>
                        </div>
                        <div class="text-center text-sm text-zinc-400" id="breathing-status">Inhale for 4 • Hold for 7 • Exhale for 8</div>
                    </div>

                    <div class="bg-zinc-900 rounded-3xl p-8 flex flex-col">
                        <h3 class="font-semibold text-xl mb-2">Craving Surfing</h3>
                        <p class="text-zinc-400">Ride the urge. It peaks in 10–15 minutes and then fades.</p>
                        <div class="flex-1 flex flex-col justify-center items-center">
                            <div id="craving-timer" class="text-7xl font-mono font-semibold mb-6 text-[#00d4aa]">15:00</div>
                            <button onclick="startCravingTimer()" 
                                    class="px-10 py-4 bg-white/10 hover:bg-white/20 text-white font-semibold rounded-3xl flex items-center gap-x-3">
                                <i class="fa-solid fa-hourglass-start"></i>
                                START 15-MINUTE TIMER
                            </button>
                        </div>
                        <textarea id="craving-note" rows="2"
                                  class="w-full bg-black/30 border border-transparent focus:border-[#00d4aa] rounded-3xl p-4 text-sm placeholder:text-zinc-500"
                                  placeholder="What triggered this craving?"></textarea>
                    </div>

                    <div onclick="playDistraction()" class="col-span-2 bg-zinc-900 rounded-3xl p-8 flex items-center gap-8 cursor-pointer hover:bg-gradient-to-r hover:from-[#00d4aa]/10">
                        <div class="flex-1">
                            <span class="px-4 py-1 bg-amber-300 text-zinc-950 text-xs font-bold rounded-3xl">INSTANT WIN</span>
                            <h3 class="text-4xl font-semibold mt-4 leading-none">5-minute brain game</h3>
                            <p class="text-zinc-400 mt-3">Click as many green orbs as you can before they disappear.</p>
                        </div>
                        <div id="game-preview" class="w-40 h-40 bg-black/70 rounded-3xl flex items-center justify-center text-6xl">🎯</div>
                    </div>
                </div>
            </div>

            <!-- RESOURCES SECTION (unchanged) -->
            <div id="screen-resources" class="hidden">
                <h2 class="section-header text-3xl font-semibold mb-6">Evidence-Based Resources</h2>
                <div class="grid grid-cols-3 gap-6">
                    <a href="https://www.who.int/health-topics/substance-use" target="_blank" class="bg-zinc-900 hover:bg-zinc-800 rounded-3xl p-6 card-hover">
                        <i class="fa-solid fa-globe text-4xl mb-6 text-[#00d4aa]"></i>
                        <h4 class="font-semibold">WHO Substance Use Guide</h4>
                        <p class="text-zinc-400 mt-2 text-sm">Global facts, myths, and recovery science.</p>
                    </a>
                    <a href="https://www.smartrecovery.org/" target="_blank" class="bg-zinc-900 hover:bg-zinc-800 rounded-3xl p-6 card-hover">
                        <i class="fa-solid fa-brain text-4xl mb-6 text-[#00d4aa]"></i>
                        <h4 class="font-semibold">SMART Recovery (Free)</h4>
                        <p class="text-zinc-400 mt-2 text-sm">Self-management tools used by millions.</p>
                    </a>
                    <a href="#" onclick="showKenyaResources()" class="bg-zinc-900 hover:bg-zinc-800 rounded-3xl p-6 card-hover">
                        <i class="fa-solid fa-flag text-4xl mb-6 text-[#00d4aa]"></i>
                        <h4 class="font-semibold">Kenya Local Support</h4>
                        <p class="text-zinc-400 mt-2 text-sm">NACADA • Mathari Hospital • Free counseling lines</p>
                    </a>
                </div>
                <div class="mt-8 p-6 bg-zinc-900 rounded-3xl border border-amber-400/30">
                    <h3 class="text-amber-400 flex items-center gap-x-2"><i class="fa-solid fa-book"></i> Daily Tip</h3>
                    <p id="daily-tip" class="mt-4 text-lg">Replace one bad habit with a 5-minute walk every time a craving hits.</p>
                </div>
            </div>

            <!-- COMMUNITY SECTION (unchanged) -->
            <div id="screen-community" class="hidden">
                <h2 class="section-header text-3xl font-semibold mb-6">You're not alone. Real stories from real people.</h2>
                <div id="community-posts" class="space-y-6"></div>
                <div class="mt-8 bg-zinc-900 rounded-3xl p-6 flex gap-4">
                    <input id="post-input" type="text" placeholder="Share your win or ask for support..." 
                           class="flex-1 bg-black/30 rounded-3xl px-6 py-4 focus:outline-none">
                    <button onclick="postToCommunity()" 
                            class="px-10 bg-[#00d4aa] text-zinc-950 font-semibold rounded-3xl">POST</button>
                </div>
            </div>

            <!-- NEW: AI COACH SECTION -->
            <div id="screen-coach" class="hidden">
                <div class="flex items-center justify-between mb-6">
                    <div>
                        <h2 class="section-header text-3xl font-semibold">AI Coach</h2>
                        <p class="text-zinc-400">Your 24/7 recovery companion • Trained on evidence-based techniques</p>
                    </div>
                    <div class="flex items-center gap-x-3 text-sm bg-zinc-900 px-5 py-3 rounded-3xl">
                        <div class="w-3 h-3 bg-[#00d4aa] rounded-full animate-pulse"></div>
                        Always here for you, Samuel
                    </div>
                </div>

                <!-- Chat Container -->
                <div class="bg-zinc-900 rounded-3xl p-6 h-[560px] flex flex-col">
                    <div id="chat-messages" class="flex-1 overflow-y-auto space-y-6 pr-4 scrollbar-thin scrollbar-thumb-zinc-700">
                        <!-- Messages populated by JS -->
                    </div>

                    <!-- Quick prompts -->
                    <div class="flex flex-wrap gap-2 mt-4 mb-4">
                        <button onclick="quickPrompt('craving')" 
                                class="text-xs bg-zinc-800 hover:bg-[#00d4aa] hover:text-zinc-950 px-5 py-2 rounded-3xl">I'm having a strong craving right now</button>
                        <button onclick="quickPrompt('motivation')" 
                                class="text-xs bg-zinc-800 hover:bg-[#00d4aa] hover:text-zinc-950 px-5 py-2 rounded-3xl">I need some motivation</button>
                        <button onclick="quickPrompt('progress')" 
                                class="text-xs bg-zinc-800 hover:bg-[#00d4aa] hover:text-zinc-950 px-5 py-2 rounded-3xl">Reflect on my progress</button>
                        <button onclick="quickPrompt('relapse')" 
                                class="text-xs bg-zinc-800 hover:bg-[#00d4aa] hover:text-zinc-950 px-5 py-2 rounded-3xl">I slipped today — help me get back</button>
                        <button onclick="quickPrompt('goal')" 
                                class="text-xs bg-zinc-800 hover:bg-[#00d4aa] hover:text-zinc-950 px-5 py-2 rounded-3xl">Help me set a new goal</button>
                    </div>

                    <!-- Input -->
                    <div class="flex gap-3">
                        <input id="chat-input" 
                               type="text"
                               placeholder="Type your message to the AI Coach..."
                               class="flex-1 bg-zinc-800 text-white rounded-3xl px-6 py-4 focus:outline-none focus:border-[#00d4aa] border border-transparent"
                               onkeypress="if(event.key === 'Enter') sendMessageToAI()">
                        <button onclick="sendMessageToAI()" 
                                class="w-12 h-12 bg-[#00d4aa] text-zinc-950 rounded-3xl flex items-center justify-center text-2xl hover:scale-110">
                            <i class="fa-solid fa-paper-plane"></i>
                        </button>
                    </div>
                </div>

                <div class="text-center text-xs text-zinc-500 mt-4 flex items-center justify-center gap-x-4">
                    <span>💡 Powered by real recovery science</span>
                    <span class="text-[#00d4aa]">•</span>
                    <span>Responses are simulated but feel real — always combine with real support</span>
                </div>
            </div>
        </div>
    </div>

    <!-- Existing modals (relapse & profile) remain unchanged -->
    <div onclick="if(event.target.id === 'relapse-modal')hideModals()" 
         id="relapse-modal"
         class="hidden fixed inset-0 bg-black/70 z-[100] flex items-center justify-center">
        <div class="modal bg-zinc-900 rounded-3xl max-w-md w-full mx-4 p-8">
            <h2 class="text-2xl font-semibold">You had a slip. That's okay.</h2>
            <p class="text-zinc-400 mt-2">Every recovery journey has bumps. What matters is getting back up.</p>
            <textarea id="relapse-reason" rows="3" class="mt-8 w-full bg-zinc-800 rounded-3xl p-5" placeholder="What happened? Be honest — this helps you grow."></textarea>
            <div class="flex gap-4 mt-8">
                <button onclick="hideModals()" class="flex-1 py-5 border border-zinc-700 rounded-3xl font-medium">CANCEL</button>
                <button onclick="confirmRelapse()" class="flex-1 py-5 bg-red-500 text-white rounded-3xl font-medium">LOG THIS &amp; RESET STREAK</button>
            </div>
            <p class="text-center text-xs text-zinc-500 mt-6">You are still worthy of recovery.</p>
        </div>
    </div>

    <div onclick="if(event.target.id === 'profile-modal')hideModals()" 
         id="profile-modal"
         class="hidden fixed inset-0 bg-black/70 z-[100] flex items-center justify-center">
        <div class="modal bg-zinc-900 rounded-3xl max-w-lg w-full mx-4 p-8">
            <div class="flex justify-between">
                <h2 class="text-2xl font-semibold">Your Recovery Profile</h2>
                <i onclick="hideModals()" class="fa-solid fa-xmark text-2xl cursor-pointer"></i>
            </div>
            <div class="mt-8 space-y-8">
                <div>
                    <label class="text-xs uppercase tracking-widest">Your name</label>
                    <input id="profile-name" value="Samuel" class="w-full mt-2 bg-zinc-800 rounded-3xl px-6 py-5 text-xl">
                </div>
                <div class="grid grid-cols-2 gap-6">
                    <div>
                        <label class="text-xs uppercase tracking-widest">Joined recovery</label>
                        <p class="mt-2 text-3xl font-semibold">March 1, 2026</p>
                    </div>
                    <div>
                        <label class="text-xs uppercase tracking-widest">Total days clean</label>
                        <p id="profile-total-days" class="mt-2 text-3xl font-semibold">47</p>
                    </div>
                </div>
                <button onclick="saveProfile()" class="w-full py-6 bg-[#00d4aa] text-zinc-950 rounded-3xl font-semibold text-lg">SAVE CHANGES</button>
            </div>
        </div>
    </div>

    <script>
        // Tailwind script initialization
        function initializeTailwind() {
            return { config(userConfig = {}) { return { configUser: userConfig, theme: { extend: { colors: { primary: '#00d4aa' } } } } }, theme: { extend: {} } }
        }

        // Global data store
        let userData = {
            name: "Samuel",
            globalStreak: 12,
            totalSoberDays: 47,
            cravingsToday: 3,
            achievements: 7,
            addictions: {
                smoking: { name: "Smoking", icon: "🚬", streak: 14, color: "#00d4aa", logs: [{ date: "2026-04-13", type: "sober", note: "Felt strong today" }, { date: "2026-04-12", type: "sober", note: "" }], lastReset: "2026-03-31" },
                social: { name: "Social Media", icon: "📱", streak: 9, color: "#00a88a", logs: [{ date: "2026-04-13", type: "sober", note: "Used app blocker" }], lastReset: "2026-04-04" },
                gaming: { name: "Gaming", icon: "🎮", streak: 5, color: "#00d4aa", logs: [], lastReset: "2026-04-09" }
            },
            chatHistory: [] // NEW: AI Coach chat history
        }

        let currentAddictionKey = "smoking"
        let chartInstance = null

        // Expanded quotes (more motivational + Kenya-friendly)
        let quotes = [
            { text: "The only way to get through a craving is to ride it like a wave — it will pass.", author: "Dr. Judson Brewer" },
            { text: "You don't have to be great to start, but you have to start to be great.", author: "Zig Ziglar" },
            { text: "Every time you choose recovery, you vote for the person you want to become.", author: "Anonymous" },
            { text: "Cravings are temporary. Your freedom is permanent.", author: "OVERCOME community" },
            { text: "Pole pole ndio mwendo. Small consistent steps win the race.", author: "Kenyan proverb" },
            { text: "Your future self is watching you right now. Make them proud.", author: "AI Coach" },
            { text: "One day at a time. In Nairobi, one matatu ride at a time.", author: "Local recovery warrior" }
        ]

        // AI Coach responses (functional keyword matching)
        const aiResponses = {
            greeting: [
                "Hey Samuel! 👋 How’s your day going in Nairobi? I’m here to support your recovery journey.",
                "Good to see you, Samuel. What’s on your mind today?"
            ],
            craving: [
                "Cravings are normal — they usually peak in 10-15 minutes. Try the 4-7-8 breathing tool right now. You’ve beaten this before. You’ve got this.",
                "Breathe with me: Inhale 4… hold 7… exhale 8. The urge is a wave — it will pass. Want me to walk you through a grounding exercise?"
            ],
            motivation: [
                "Samuel, you’ve already built a 12-day streak. That’s real strength. Remember why you started — your future self in Nairobi is thanking you right now.",
                "You are not your addiction. You are the man who shows up every single day. I’m proud of you."
            ],
            progress: [
                "Looking at your data: 47 total sober days and a 14-day streak on smoking. That’s incredible growth. What’s one thing you’re most proud of this week?",
                "Your brain is literally rewiring itself. Science shows that after 30 days the dopamine pathways start to heal. You’re doing the work."
            ],
            relapse: [
                "A slip is not a failure — it’s data. You’re still in recovery. What triggered it? Let’s make a plan so tomorrow is stronger. You are still worthy.",
                "Every champion has fallen. The difference is they get back up. I’m here with you. Let’s log it and reset with compassion."
            ],
            goal: [
                "Great question! How about this goal for the next 7 days: Stay strong on your top addiction and journal one win every night. Want me to help you make it even more specific?",
                "Let’s set a SMART goal together. What’s one small, achievable thing you want to focus on this week?"
            ]
        }

        let chatHistory = []

        // Render addiction list (unchanged)
        function renderAddictionList() {
            const container = document.getElementById('addiction-list')
            container.innerHTML = ''
            Object.keys(userData.addictions).forEach(key => {
                const addiction = userData.addictions[key]
                const isActive = key === currentAddictionKey
                const div = document.createElement('div')
                div.className = `flex items-center gap-x-4 px-5 py-5 rounded-3xl cursor-pointer ${isActive ? 'bg-[#00d4aa] text-zinc-950' : 'hover:bg-zinc-800'}`
                div.innerHTML = `
                    <span class="text-3xl">${addiction.icon}</span>
                    <div class="flex-1">
                        <p class="font-semibold">${addiction.name}</p>
                        <p class="text-xs flex items-center gap-x-1 ${isActive ? 'text-zinc-900' : 'text-zinc-400'}">
                            <i class="fa-solid fa-fire"></i> ${addiction.streak} day streak
                        </p>
                    </div>
                    ${isActive ? `<i class="fa-solid fa-circle-check"></i>` : ''}
                `
                div.onclick = () => {
                    currentAddictionKey = key
                    renderAddictionList()
                    if (!document.getElementById('screen-track').classList.contains('hidden')) showTrackerForCurrent()
                }
                container.appendChild(div)
            })
        }

        // Render focus cards (unchanged)
        function renderFocusCards() {
            const container = document.getElementById('focus-cards')
            container.innerHTML = ''
            Object.keys(userData.addictions).forEach(key => {
                const add = userData.addictions[key]
                const card = document.createElement('div')
                card.className = `bg-zinc-900 rounded-3xl p-6 card-hover cursor-pointer`
                card.innerHTML = `
                    <div class="text-5xl mb-4">${add.icon}</div>
                    <h4 class="font-semibold">${add.name}</h4>
                    <div class="mt-6 flex justify-between items-end">
                        <div>
                            <span class="text-4xl font-semibold">${add.streak}</span>
                            <span class="text-xs uppercase ml-1">days</span>
                        </div>
                        <div class="text-[#00d4aa] text-sm flex items-center"><i class="fa-solid fa-fire mr-1"></i> ON FIRE</div>
                    </div>
                `
                card.onclick = () => { currentAddictionKey = key; navigateTo('track') }
                container.appendChild(card)
            })
        }

        // Show tracker (unchanged)
        function showTrackerForCurrent() {
            const addiction = userData.addictions[currentAddictionKey]
            document.getElementById('selected-addiction-header').innerHTML = `
                <div class="flex items-center gap-x-4">
                    <span class="text-5xl">${addiction.icon}</span>
                    <div>
                        <h2 class="text-4xl heading-font">${addiction.name} Tracker</h2>
                        <p class="text-zinc-400">You're doing better than you think.</p>
                    </div>
                </div>
                <button onclick="navigateTo('dashboard')" class="flex items-center gap-x-2 text-zinc-400">← Back to dashboard</button>
            `
            document.getElementById('streak-number').textContent = addiction.streak
            document.getElementById('streak-text').innerHTML = `${addiction.name.toLowerCase()}-free`
            
            const logContainer = document.getElementById('log-list')
            logContainer.innerHTML = ''
            if (addiction.logs.length === 0) {
                logContainer.innerHTML = `<div class="bg-black/30 rounded-3xl p-8 text-center text-zinc-400">No entries yet. Start logging your wins!</div>`
                return
            }
            addiction.logs.forEach(log => {
                const el = document.createElement('div')
                el.className = 'flex justify-between items-center bg-black/30 px-6 py-4 rounded-3xl'
                el.innerHTML = `
                    <div class="flex items-center gap-x-4">
                        <span class="text-2xl">${log.type === 'sober' ? '✅' : '⚠️'}</span>
                        <div>
                            <p class="font-medium">${log.date}</p>
                            <p class="text-sm text-zinc-400">${log.note || 'No note'}</p>
                        </div>
                    </div>
                    <span class="text-xs bg-zinc-800 px-4 py-1 rounded-3xl">${log.type}</span>
                `
                logContainer.appendChild(el)
            })
            renderProgressChart(addiction)
        }

        function renderProgressChart(addiction) {
            const ctx = document.getElementById('progressChart')
            if (chartInstance) chartInstance.destroy()
            const labels = [], data = []
            const today = new Date('2026-04-14')
            for (let i = 29; i >= 0; i--) {
                const d = new Date(today)
                d.setDate(d.getDate() - i)
                labels.push(d.getDate() + '/' + (d.getMonth() + 1))
                data.push(Math.random() > 0.2 ? 1 : 0)
            }
            chartInstance = new Chart(ctx, {
                type: 'line',
                data: { labels: labels, datasets: [{ label: 'Sober days', data: data, borderColor: '#00d4aa', backgroundColor: 'rgba(0, 212, 170, 0.15)', borderWidth: 3, tension: 0.3, pointRadius: 0, pointHoverRadius: 6 }] },
                options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false } }, scales: { y: { display: false }, x: { grid: { color: '#27272a' }, ticks: { color: '#a1a1aa', font: { size: 11 } } } } }
            })
        }

        // Mark sober (unchanged)
        function markTodaySober(fromTracker = false) {
            const addiction = userData.addictions[currentAddictionKey]
            const today = '2026-04-14'
            addiction.logs.unshift({ date: today, type: 'sober', note: 'Marked strong today' })
            addiction.streak++
            userData.globalStreak++
            userData.totalSoberDays++
            renderAddictionList()
            renderFocusCards()
            document.getElementById('current-streak-global').innerHTML = `<i class="fa-solid fa-fire"></i> ${userData.globalStreak} day streak`
            document.getElementById('global-streak').textContent = userData.globalStreak
            launchConfetti()
            showToast(`🎉 +1 day for ${addiction.name}!`)
            if (fromTracker || !document.getElementById('screen-track').classList.contains('hidden')) showTrackerForCurrent()
            saveToLocalStorage()
        }

        function logRelapse() { document.getElementById('relapse-modal').classList.remove('hidden'); document.getElementById('relapse-modal').classList.add('flex') }
        function confirmRelapse() {
            const note = document.getElementById('relapse-reason').value || 'No note provided'
            const addiction = userData.addictions[currentAddictionKey]
            addiction.logs.unshift({ date: '2026-04-14', type: 'relapse', note: note })
            addiction.streak = 0
            hideModals()
            showTrackerForCurrent()
            renderAddictionList()
            renderFocusCards()
            showToast('📝 Relapse logged. Tomorrow is a new day.', true)
            saveToLocalStorage()
        }
        function hideModals() {
            document.querySelectorAll('.fixed').forEach(m => { m.classList.add('hidden'); m.classList.remove('flex') })
            document.getElementById('relapse-reason').value = ''
        }

        // Breathing, craving timer, distraction, confetti, toast, community (unchanged) — keeping them short for space
        let breathingInterval = null
        function startBreathing() {
            const btn = document.getElementById('breathe-btn')
            const circle = document.getElementById('breathing-circle')
            const status = document.getElementById('breathing-status')
            if (breathingInterval) { clearInterval(breathingInterval); btn.innerHTML = `<i class="fa-solid fa-play"></i> START`; circle.style.animation = ''; circle.innerHTML = 'Breathe'; status.textContent = 'Inhale for 4 • Hold for 7 • Exhale for 8'; return }
            btn.innerHTML = `<i class="fa-solid fa-stop"></i> STOP`
            let phase = 0, seconds = 4
            circle.style.animation = 'spin 8s linear infinite'
            breathingInterval = setInterval(() => {
                seconds--
                if (phase === 0) { circle.innerHTML = `Inhale<br><span class="text-7xl">${seconds}</span>`; status.textContent = 'Inhale...'; if (seconds <= 0) { phase = 1; seconds = 7 } }
                else if (phase === 1) { circle.innerHTML = `Hold<br><span class="text-7xl">${seconds}</span>`; status.textContent = 'Hold...'; if (seconds <= 0) { phase = 2; seconds = 8 } }
                else { circle.innerHTML = `Exhale<br><span class="text-7xl">${seconds}</span>`; status.textContent = 'Exhale...'; if (seconds <= 0) { phase = 0; seconds = 4 } }
            }, 1000)
        }

        let cravingTimerInterval = null
        function startCravingTimer() {
            let timeLeft = 900
            const display = document.getElementById('craving-timer')
            if (cravingTimerInterval) clearInterval(cravingTimerInterval)
            display.textContent = '15:00'
            cravingTimerInterval = setInterval(() => {
                timeLeft--
                const min = Math.floor(timeLeft / 60)
                const sec = timeLeft % 60
                display.textContent = `${min}:${sec < 10 ? '0' : ''}${sec}`
                if (timeLeft <= 0) {
                    clearInterval(cravingTimerInterval)
                    display.innerHTML = `🎉<br><span class="text-4xl">You made it!</span>`
                    showToast('Craving passed! You are stronger than the urge.')
                }
            }, 1000)
        }

        function playDistraction() {
            const preview = document.getElementById('game-preview')
            preview.innerHTML = `<div class="relative w-40 h-40" id="orb-game"><div onclick="this.style.display='none';score++" class="absolute w-8 h-8 bg-[#00d4aa] rounded-full shadow-[0_0_30px_#00d4aa] top-4 left-6 cursor-pointer"></div><div onclick="this.style.display='none';score++" class="absolute w-8 h-8 bg-[#00d4aa] rounded-full shadow-[0_0_30px_#00d4aa] top-20 right-8 cursor-pointer"></div><div onclick="this.style.display='none';score++" class="absolute w-8 h-8 bg-[#00d4aa] rounded-full shadow-[0_0_30px_#00d4aa] bottom-8 left-12 cursor-pointer"></div><div class="absolute bottom-4 left-1/2 -translate-x-1/2 text-xs font-bold text-white">CLICK THE GREEN ORBS FAST!</div></div>`
            let score = 0
            setTimeout(() => {
                const game = document.getElementById('orb-game')
                if (game) {
                    game.innerHTML += `<div class="mt-6 text-center text-2xl">Score: <span class="text-[#00d4aa]">${score}</span>/3</div>`
                    showToast(`Great job! You distracted the craving for ${score * 20} seconds.`)
                }
            }, 4000)
        }

        function launchConfetti() {
            const colors = ['#00d4aa', '#00a88a', '#ffffff']
            for (let i = 0; i < 80; i++) {
                const confetti = document.createElement('div')
                confetti.style.position = 'fixed'; confetti.style.zIndex = '99999'; confetti.style.left = Math.random() * 100 + 'vw'; confetti.style.top = '-20px'; confetti.style.fontSize = '20px'; confetti.style.transform = `rotate(${Math.random() * 360}deg)`; confetti.textContent = ['🔥','🎉','🪄','💪'][Math.floor(Math.random()*4)]
                document.body.appendChild(confetti)
                const duration = Math.random() * 3000 + 2000
                confetti.animate([{ transform: `translateY(0) rotate(0deg)` }, { transform: `translateY(${window.innerHeight + 100}px) rotate(${Math.random()*800}deg)` }], { duration: duration, easing: 'cubic-bezier(0.25, 0.1, 0.25, 1)' })
                setTimeout(() => confetti.remove(), duration)
            }
        }

        function showToast(message, isRed = false) {
            const toast = document.createElement('div')
            toast.style.cssText = `position:fixed; bottom:30px; left:50%; transform:translateX(-50%); background:${isRed ? '#f43f5e' : '#00d4aa'}; color:${isRed ? '#fff' : '#111'}; padding:18px 28px; border-radius:9999px; box-shadow:0 25px 50px -12px rgb(0 0 0 / 0.4); font-weight:600; z-index:999999; display:flex; align-items:center; gap:10px;`
            toast.innerHTML = `${message} <i onclick="this.parentElement.remove()" class="fa-solid fa-xmark ml-4"></i>`
            document.body.appendChild(toast)
            setTimeout(() => toast.remove(), 3200)
        }

        // Community functions (unchanged)
        let communityPosts = [{ user: "Aisha M.", location: "Nairobi", text: "Day 28 alcohol-free. My sleep is finally normal again.", likes: 24, emoji: "🍺" }, { user: "Kevin O.", location: "Mombasa", text: "Just hit 60 days off social media.", likes: 18, emoji: "📱" }]
        function renderCommunity() {
            const container = document.getElementById('community-posts')
            container.innerHTML = ''
            communityPosts.forEach(post => {
                const el = document.createElement('div')
                el.className = 'bg-zinc-900 rounded-3xl p-6 flex gap-4'
                el.innerHTML = `<div class="text-5xl flex-shrink-0">${post.emoji}</div><div class="flex-1"><div class="flex justify-between"><div><span class="font-semibold">${post.user}</span><span class="text-zinc-500 text-sm ml-2">${post.location}</span></div><div class="flex items-center text-amber-400"><i class="fa-solid fa-heart mr-1"></i> ${post.likes}</div></div><p class="mt-3 text-zinc-200">${post.text}</p></div>`
                container.appendChild(el)
            })
        }
        function postToCommunity() {
            const input = document.getElementById('post-input')
            if (!input.value.trim()) return
            communityPosts.unshift({ user: "Samuel", location: "Nairobi", text: input.value, likes: 0, emoji: "🏆" })
            input.value = ''
            renderCommunity()
            showToast('Posted to the community!')
        }

        // NEW: AI COACH FUNCTIONS
        function renderChat() {
            const container = document.getElementById('chat-messages')
            container.innerHTML = ''
            chatHistory.forEach(msg => {
                const bubble = document.createElement('div')
                bubble.className = `flex ${msg.isAI ? 'justify-start' : 'justify-end'}`
                bubble.innerHTML = `
                    ${msg.isAI ? `
                    <div class="max-w-[75%] flex gap-3">
                        <div class="w-8 h-8 bg-[#00d4aa]/20 text-[#00d4aa] rounded-2xl flex items-center justify-center text-xl flex-shrink-0">🧠</div>
                        <div class="chat-bubble-ai px-5 py-4 text-sm">${msg.text}</div>
                    </div>` : `
                    <div class="chat-bubble-user px-5 py-4 text-sm max-w-[75%]">${msg.text}</div>`}
                `
                container.appendChild(bubble)
            })
            container.scrollTop = container.scrollHeight
        }

        function addAIMessage(text) {
            chatHistory.push({ isAI: true, text: text })
            renderChat()
            saveToLocalStorage()
        }

        function getAIResponse(userMessage) {
            const lower = userMessage.toLowerCase()
            if (lower.includes('craving') || lower.includes('urge')) return aiResponses.craving[Math.floor(Math.random() * aiResponses.craving.length)]
            if (lower.includes('motivation') || lower.includes('encourage')) return aiResponses.motivation[Math.floor(Math.random() * aiResponses.motivation.length)]
            if (lower.includes('progress') || lower.includes('how am i doing')) return aiResponses.progress[Math.floor(Math.random() * aiResponses.progress.length)]
            if (lower.includes('slip') || lower.includes('relapse') || lower.includes('fell')) return aiResponses.relapse[Math.floor(Math.random() * aiResponses.relapse.length)]
            if (lower.includes('goal') || lower.includes('target')) return aiResponses.goal[Math.floor(Math.random() * aiResponses.goal.length)]
            // Default responses
            return [
                "Thank you for sharing, Samuel. That takes courage. How can I support you most right now?",
                "You’re not alone in this. What’s one small step we can take together today?",
                "I hear you. Let’s focus on what you can control right now — your next choice."
            ][Math.floor(Math.random() * 3)]
        }

        function sendMessageToAI() {
            const input = document.getElementById('chat-input')
            const message = input.value.trim()
            if (!message) return
            chatHistory.push({ isAI: false, text: message })
            renderChat()
            input.value = ''
            // Simulate thinking
            setTimeout(() => {
                const reply = getAIResponse(message)
                addAIMessage(reply)
            }, 800)
        }

        function quickPrompt(type) {
            let message = ''
            if (type === 'craving') message = "I'm having a strong craving right now"
            else if (type === 'motivation') message = "I need some motivation"
            else if (type === 'progress') message = "Reflect on my progress"
            else if (type === 'relapse') message = "I slipped today — help me get back"
            else if (type === 'goal') message = "Help me set a new goal"
            
            chatHistory.push({ isAI: false, text: message })
            renderChat()
            setTimeout(() => {
                const reply = getAIResponse(message)
                addAIMessage(reply)
            }, 600)
        }

        // NEW: Get a fresh AI-suggested quote
        function getAICoachQuote() {
            const randomQuote = quotes[Math.floor(Math.random() * quotes.length)]
            document.getElementById('quote-text').textContent = `"${randomQuote.text}"`
            document.getElementById('quote-author').innerHTML = `— ${randomQuote.author} <span class="text-xs ml-2 text-[#00d4aa]">(AI Coach pick)</span>`
            showToast("💡 Fresh quote from your AI Coach!")
        }

        // Navigation
        function navigateTo(screen) {
            document.querySelectorAll('[id^="screen-"]').forEach(s => s.classList.add('hidden'))
            const target = document.getElementById('screen-' + screen)
            if (target) target.classList.remove('hidden')
            
            if (screen === 'track') showTrackerForCurrent()
            if (screen === 'community') renderCommunity()
            if (screen === 'coach') {
                // Initialize chat on first visit
                if (chatHistory.length === 0) {
                    chatHistory = userData.chatHistory.length > 0 ? userData.chatHistory : [
                        { isAI: true, text: "Hi Samuel! 👋 I’m your AI Coach. I’m here to help you stay strong, manage cravings, celebrate wins, and keep you moving forward. What’s on your mind today?" }
                    ]
                    userData.chatHistory = chatHistory
                }
                renderChat()
            }
        }

        // Profile, add addiction, local help, save (unchanged)
        function showProfile() {
            document.getElementById('profile-name').value = userData.name
            document.getElementById('profile-total-days').textContent = userData.totalSoberDays
            document.getElementById('profile-modal').classList.remove('hidden')
            document.getElementById('profile-modal').classList.add('flex')
        }
        function saveProfile() {
            userData.name = document.getElementById('profile-name').value
            hideModals()
            showToast('Profile updated. You got this, ' + userData.name + '!')
        }
        function addNewAddiction() {
            const name = prompt('What addiction do you want to overcome?', 'Porn')
            if (!name) return
            const key = name.toLowerCase().replace(/\s/g, '')
            userData.addictions[key] = { name: name, icon: ['📵','🍔','🍺','💰','🃏'][Math.floor(Math.random()*5)], streak: 0, color: '#00d4aa', logs: [], lastReset: '2026-04-14' }
            renderAddictionList()
            showToast(`✅ ${name} added. Let's beat it together!`)
        }
        function showKenyaResources() {
            alert('✅ NACADA Helpline: 1190\n✅ Mathari National Hospital: 0722 123 456\n✅ Kenya Psychiatric Association support groups available in Nairobi.\n\nYou can also visit https://nacada.go.ke for free resources.')
        }
        function showLocalHelp() { showKenyaResources() }
        function toggleTheme() { showToast('🌗 Theme switched (demo)') }

        // Storage
        function saveToLocalStorage() {
            userData.chatHistory = chatHistory
            localStorage.setItem('overcomeUserData', JSON.stringify(userData))
        }
        function loadFromLocalStorage() {
            const saved = localStorage.getItem('overcomeUserData')
            if (saved) {
                const parsed = JSON.parse(saved)
                userData = parsed
                chatHistory = parsed.chatHistory || []
            }
        }

        // Initialize everything
        function initializeApp() {
            loadFromLocalStorage()
            initializeTailwind()
            renderAddictionList()
            renderFocusCards()
            document.getElementById('current-streak-global').innerHTML = `<i class="fa-solid fa-fire"></i> ${userData.globalStreak} day streak`
            document.getElementById('global-streak').textContent = userData.globalStreak
            document.getElementById('total-sober-days').textContent = userData.totalSoberDays
            document.getElementById('cravings-today').textContent = userData.cravingsToday

            // Random quote on dashboard
            const randomQuote = quotes[Math.floor(Math.random() * quotes.length)]
            document.getElementById('quote-text').textContent = `"${randomQuote.text}"`
            document.getElementById('quote-author').innerHTML = `— ${randomQuote.author}`

            const tips = ["Hydrate. A dehydrated brain craves dopamine more intensely.", "Movement is medicine. A 10-minute walk can cut cravings by 40%.", "Tell one trusted person your goal today — accountability works."]
            document.getElementById('daily-tip').textContent = tips[Math.floor(Math.random()*tips.length)]

            console.log('%c🚀 OVERCOME + AI Coach fully loaded and ready for Samuel!', 'color:#00d4aa; font-family:Space Grotesk; font-size:13px')
        }

        window.onload = initializeApp
    </script>
</body>
</html>
