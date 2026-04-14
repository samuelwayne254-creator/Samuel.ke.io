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

        .progress-circle {
            animation: spin 1s linear infinite;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .animate-in {
            animation: fadeInUp 0.6s backwards;
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
            </div>

            <!-- Right side -->
            <div class="flex items-center gap-x-6">
                <!-- Personalized greeting -->
                <div class="flex items-center gap-x-2 bg-zinc-800 hover:bg-zinc-700 px-4 py-2 rounded-3xl cursor-pointer" onclick="showProfile()">
                    <div class="text-right">
                        <p class="text-sm font-semibold">Hi Samuel 👋</p>
                        <p id="current-streak-global" class="text-xs text-[#00d4aa] flex items-center gap-x-1">
                            <i class="fa-solid fa-fire"></i> 12 day streak
                        </p>
                    </div>
                    <div class="w-9 h-9 bg-emerald-400 rounded-2xl flex items-center justify-center text-2xl">🇰🇪</div>
                </div>

                <!-- Quick action -->
                <button onclick="markTodaySober()"
                        class="flex items-center gap-x-3 bg-[#00d4aa] hover:bg-[#00b894] text-zinc-950 font-semibold px-6 py-3 rounded-3xl text-sm">
                    <i class="fa-solid fa-check-circle"></i>
                    <span>I STAYED STRONG TODAY</span>
                </button>

                <!-- Settings -->
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
            
            <!-- Add new addiction -->
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
                    <div class="text-right">
                        <div class="inline-flex items-center gap-x-2 bg-zinc-800 rounded-3xl px-5 py-2 text-sm">
                            <div class="w-3 h-3 bg-[#00d4aa] rounded-full animate-pulse"></div>
                            You're in recovery mode
                        </div>
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

                <!-- Motivational quote -->
                <div class="bg-gradient-to-br from-[#00d4aa]/10 to-transparent border border-[#00d4aa]/20 rounded-3xl p-8 flex gap-6">
                    <div class="text-6xl">💡</div>
                    <div>
                        <p id="quote-text" class="text-xl italic">"The only way to get through a craving is to ride it like a wave — it will pass."</p>
                        <p id="quote-author" class="text-[#00d4aa] mt-4 text-sm font-medium">— Dr. Judson Brewer, neuroscientist</p>
                    </div>
                </div>
            </div>

            <!-- TRACK PROGRESS SECTION -->
            <div id="screen-track" class="hidden">
                <h2 class="section-header text-3xl font-semibold mb-6">Track Your Progress</h2>
                
                <div id="selected-addiction-header" class="flex items-center justify-between mb-6"></div>
                
                <div class="grid grid-cols-12 gap-8">
                    <!-- Streak card -->
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

                    <!-- Progress chart -->
                    <div class="col-span-7 bg-zinc-900 rounded-3xl p-8">
                        <h3 class="font-semibold mb-4">Last 30 days</h3>
                        <canvas id="progressChart" class="w-full h-64"></canvas>
                    </div>
                </div>

                <!-- Recent logs -->
                <div class="mt-8">
                    <h3 class="font-semibold mb-4">Recent entries</h3>
                    <div id="log-list" class="space-y-3"></div>
                </div>
            </div>

            <!-- TOOLS SECTION -->
            <div id="screen-tools" class="hidden">
                <h2 class="section-header text-3xl font-semibold mb-6">Instant Relief Tools</h2>
                
                <div class="grid grid-cols-2 gap-6">
                    <!-- Breathing -->
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

                    <!-- Craving timer -->
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
                            <p class="text-xs text-zinc-500 mt-8 text-center max-w-xs">Remember: “This too shall pass.” Write what you're feeling below if you want.</p>
                        </div>
                        
                        <textarea id="craving-note" rows="2"
                                  class="w-full bg-black/30 border border-transparent focus:border-[#00d4aa] rounded-3xl p-4 text-sm placeholder:text-zinc-500"
                                  placeholder="What triggered this craving?"></textarea>
                    </div>

                    <!-- Quick distractions -->
                    <div onclick="playDistraction()" class="col-span-2 bg-zinc-900 rounded-3xl p-8 flex items-center gap-8 cursor-pointer hover:bg-gradient-to-r hover:from-[#00d4aa]/10">
                        <div class="flex-1">
                            <span class="px-4 py-1 bg-amber-300 text-zinc-950 text-xs font-bold rounded-3xl">INSTANT WIN</span>
                            <h3 class="text-4xl font-semibold mt-4 leading-none">5-minute brain game</h3>
                            <p class="text-zinc-400 mt-3">Click as many green orbs as you can before they disappear. Distract the urge.</p>
                        </div>
                        <div id="game-preview" class="w-40 h-40 bg-black/70 rounded-3xl flex items-center justify-center text-6xl">🎯</div>
                    </div>
                </div>
            </div>

            <!-- RESOURCES SECTION -->
            <div id="screen-resources" class="hidden">
                <h2 class="section-header text-3xl font-semibold mb-6">Evidence-Based Resources</h2>
                <div class="grid grid-cols-3 gap-6">
                    <a href="https://www.who.int/health-topics/substance-use" target="_blank" 
                       class="bg-zinc-900 hover:bg-zinc-800 rounded-3xl p-6 card-hover">
                        <i class="fa-solid fa-globe text-4xl mb-6 text-[#00d4aa]"></i>
                        <h4 class="font-semibold">WHO Substance Use Guide</h4>
                        <p class="text-zinc-400 mt-2 text-sm">Global facts, myths, and recovery science.</p>
                    </a>
                    <a href="https://www.smartrecovery.org/" target="_blank" 
                       class="bg-zinc-900 hover:bg-zinc-800 rounded-3xl p-6 card-hover">
                        <i class="fa-solid fa-brain text-4xl mb-6 text-[#00d4aa]"></i>
                        <h4 class="font-semibold">SMART Recovery (Free)</h4>
                        <p class="text-zinc-400 mt-2 text-sm">Self-management tools used by millions.</p>
                    </a>
                    <a href="#" onclick="showKenyaResources()" 
                       class="bg-zinc-900 hover:bg-zinc-800 rounded-3xl p-6 card-hover">
                        <i class="fa-solid fa-flag text-4xl mb-6 text-[#00d4aa]"></i>
                        <h4 class="font-semibold">Kenya Local Support</h4>
                        <p class="text-zinc-400 mt-2 text-sm">NACADA • Mathari Hospital • Free counseling lines</p>
                    </a>
                </div>
                
                <div class="mt-8 p-6 bg-zinc-900 rounded-3xl border border-amber-400/30">
                    <h3 class="text-amber-400 flex items-center gap-x-2"><i class="fa-solid fa-book"></i> Daily Tip</h3>
                    <p id="daily-tip" class="mt-4 text-lg">Replace one bad habit with a 5-minute walk every time a craving hits. Science shows it rewires your brain in 21 days.</p>
                </div>
            </div>

            <!-- COMMUNITY SECTION -->
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
        </div>
    </div>

    <!-- RELAPSE MODAL -->
    <div onclick="if(event.target.id === 'relapse-modal')hideModals()" 
         id="relapse-modal"
         class="hidden fixed inset-0 bg-black/70 z-[100] flex items-center justify-center">
        <div class="modal bg-zinc-900 rounded-3xl max-w-md w-full mx-4 p-8">
            <h2 class="text-2xl font-semibold">You had a slip. That's okay.</h2>
            <p class="text-zinc-400 mt-2">Every recovery journey has bumps. What matters is getting back up.</p>
            
            <textarea id="relapse-reason" rows="3" class="mt-8 w-full bg-zinc-800 rounded-3xl p-5" placeholder="What happened? Be honest — this helps you grow."></textarea>
            
            <div class="flex gap-4 mt-8">
                <button onclick="hideModals()" 
                        class="flex-1 py-5 border border-zinc-700 rounded-3xl font-medium">CANCEL</button>
                <button onclick="confirmRelapse()" 
                        class="flex-1 py-5 bg-red-500 text-white rounded-3xl font-medium">LOG THIS &amp; RESET STREAK</button>
            </div>
            
            <p class="text-center text-xs text-zinc-500 mt-6">You are still worthy of recovery.</p>
        </div>
    </div>

    <!-- Profile modal -->
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
                    <input id="profile-name" value="Samuel" 
                           class="w-full mt-2 bg-zinc-800 rounded-3xl px-6 py-5 text-xl">
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
                
                <button onclick="saveProfile()" 
                        class="w-full py-6 bg-[#00d4aa] text-zinc-950 rounded-3xl font-semibold text-lg">SAVE CHANGES</button>
            </div>
        </div>
    </div>

    <script>
        // Tailwind script initialization
        function initializeTailwind() {
            return {
                config(userConfig = {}) {
                    return {
                        configUser: userConfig,
                        theme: {
                            extend: {
                                colors: {
                                    primary: '#00d4aa'
                                }
                            }
                        }
                    }
                },
                theme: {
                    extend: {}
                }
            }
        }
        
        // Global data store (persisted in localStorage)
        let userData = {
            name: "Samuel",
            globalStreak: 12,
            totalSoberDays: 47,
            cravingsToday: 3,
            achievements: 7,
            addictions: {
                smoking: {
                    name: "Smoking",
                    icon: "🚬",
                    streak: 14,
                    color: "#00d4aa",
                    logs: [
                        { date: "2026-04-13", type: "sober", note: "Felt strong today" },
                        { date: "2026-04-12", type: "sober", note: "" },
                        { date: "2026-04-11", type: "sober", note: "Walked instead of smoking" }
                    ],
                    lastReset: "2026-03-31"
                },
                social: {
                    name: "Social Media",
                    icon: "📱",
                    streak: 9,
                    color: "#00a88a",
                    logs: [
                        { date: "2026-04-13", type: "sober", note: "Used app blocker" },
                        { date: "2026-04-12", type: "sober", note: "" }
                    ],
                    lastReset: "2026-04-04"
                },
                gaming: {
                    name: "Gaming",
                    icon: "🎮",
                    streak: 5,
                    color: "#00d4aa",
                    logs: [],
                    lastReset: "2026-04-09"
                }
            }
        }
        
        let currentAddictionKey = "smoking"
        let chartInstance = null
        
        // Fake quotes
        const quotes = [
            { text: "The only way to get through a craving is to ride it like a wave — it will pass.", author: "Dr. Judson Brewer" },
            { text: "You don't have to be great to start, but you have to start to be great.", author: "Zig Ziglar" },
            { text: "Every time you choose recovery, you vote for the person you want to become.", author: "Anonymous" },
            { text: "Cravings are temporary. Your freedom is permanent.", author: "OVERCOME community" }
        ]
        
        // Fake community posts
        let communityPosts = [
            {
                user: "Aisha M.",
                location: "Nairobi",
                text: "Day 28 alcohol-free. My sleep is finally normal again. Proud of myself today.",
                likes: 24,
                emoji: "🍺"
            },
            {
                user: "Kevin O.",
                location: "Mombasa",
                text: "Just hit 60 days off social media. My mind feels so clear.",
                likes: 18,
                emoji: "📱"
            }
        ]
        
        // Render addiction sidebar
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
                    showTrackerForCurrent()
                }
                container.appendChild(div)
            })
        }
        
        // Render focus cards on dashboard
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
                        <div class="text-[#00d4aa] text-sm flex items-center">
                            <i class="fa-solid fa-fire mr-1"></i> ON FIRE
                        </div>
                    </div>
                `
                card.onclick = () => {
                    currentAddictionKey = key
                    navigateTo('track')
                }
                container.appendChild(card)
            })
        }
        
        // Show tracker screen for current addiction
        function showTrackerForCurrent() {
            const addiction = userData.addictions[currentAddictionKey]
            
            // Header
            document.getElementById('selected-addiction-header').innerHTML = `
                <div class="flex items-center gap-x-4">
                    <span class="text-5xl">${addiction.icon}</span>
                    <div>
                        <h2 class="text-4xl heading-font">${addiction.name} Tracker</h2>
                        <p class="text-zinc-400">You're doing better than you think.</p>
                    </div>
                </div>
                <button onclick="navigateTo('dashboard')" class="flex items-center gap-x-2 text-zinc-400">
                    ← Back to dashboard
                </button>
            `
            // Streak
            document.getElementById('streak-number').textContent = addiction.streak
            document.getElementById('streak-text').innerHTML = `${addiction.name.toLowerCase()}-free`
            
            // Logs
            const logContainer = document.getElementById('log-list')
            logContainer.innerHTML = ''
            
            if (addiction.logs.length === 0) {
                logContainer.innerHTML = `<div class="bg-black/30 rounded-3xl p-8 text-center text-zinc-400">No entries yet. Start logging your wins!</div>`
                return
            }
            
            addiction.logs.forEach((log, i) => {
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
            
            // Chart
            renderProgressChart(addiction)
        }
        
        function renderProgressChart(addiction) {
            const ctx = document.getElementById('progressChart')
            
            if (chartInstance) chartInstance.destroy()
            
            // Fake 30-day data
            const labels = []
            const data = []
            const today = new Date('2026-04-14')
            
            for (let i = 29; i >= 0; i--) {
                const d = new Date(today)
                d.setDate(d.getDate() - i)
                labels.push(d.getDate() + '/' + (d.getMonth() + 1))
                // Random but realistic
                data.push(Math.random() > 0.2 ? 1 : 0)
            }
            
            chartInstance = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Sober days',
                        data: data,
                        borderColor: '#00d4aa',
                        backgroundColor: 'rgba(0, 212, 170, 0.15)',
                        borderWidth: 3,
                        tension: 0.3,
                        pointRadius: 0,
                        pointHoverRadius: 6
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: {
                        y: { display: false },
                        x: { grid: { color: '#27272a' }, ticks: { color: '#a1a1aa', font: { size: 11 } } }
                    }
                }
            })
        }
        
        // Mark today as sober
        function markTodaySober(fromTracker = false) {
            const addiction = userData.addictions[currentAddictionKey]
            
            // Add to logs
            const today = '2026-04-14'
            addiction.logs.unshift({
                date: today,
                type: 'sober',
                note: 'Marked strong today'
            })
            
            // Increase streak
            addiction.streak++
            userData.globalStreak++
            userData.totalSoberDays++
            
            // Update UI
            renderAddictionList()
            renderFocusCards()
            document.getElementById('global-streak-global').innerHTML = `<i class="fa-solid fa-fire"></i> ${userData.globalStreak} day streak`
            document.getElementById('global-streak').textContent = userData.globalStreak
            
            // Confetti
            launchConfetti()
            
            // Show toast
            showToast(`🎉 +1 day for ${addiction.name}!`)
            
            // If inside tracker, refresh it
            if (fromTracker || document.getElementById('screen-track').classList.contains('hidden') === false) {
                showTrackerForCurrent()
            }
            
            // Save to localStorage
            saveToLocalStorage()
        }
        
        // Log relapse
        function logRelapse() {
            document.getElementById('relapse-modal').classList.remove('hidden')
            document.getElementById('relapse-modal').classList.add('flex')
        }
        
        function confirmRelapse() {
            const note = document.getElementById('relapse-reason').value || 'No note provided'
            const addiction = userData.addictions[currentAddictionKey]
            
            addiction.logs.unshift({
                date: '2026-04-14',
                type: 'relapse',
                note: note
            })
            
            // Reset streak
            addiction.streak = 0
            
            hideModals()
            showTrackerForCurrent()
            renderAddictionList()
            renderFocusCards()
            
            showToast('📝 Relapse logged. Tomorrow is a new day.', true)
            saveToLocalStorage()
        }
        
        function hideModals() {
            document.querySelectorAll('.fixed').forEach(m => {
                m.classList.add('hidden')
                m.classList.remove('flex')
            })
            document.getElementById('relapse-reason').value = ''
        }
        
        // Breathing exercise
        let breathingInterval = null
        
        function startBreathing() {
            const btn = document.getElementById('breathe-btn')
            const circle = document.getElementById('breathing-circle')
            const status = document.getElementById('breathing-status')
            
            if (breathingInterval) {
                clearInterval(breathingInterval)
                btn.innerHTML = `<i class="fa-solid fa-play"></i> START`
                circle.style.animation = ''
                circle.innerHTML = 'Breathe'
                status.textContent = 'Inhale for 4 • Hold for 7 • Exhale for 8'
                return
            }
            
            btn.innerHTML = `<i class="fa-solid fa-stop"></i> STOP`
            
            let phase = 0 // 0=inhale, 1=hold, 2=exhale
            let seconds = 4
            
            circle.style.animation = 'spin 8s linear infinite'
            
            breathingInterval = setInterval(() => {
                seconds--
                
                if (phase === 0) {
                    circle.innerHTML = `Inhale<br><span class="text-7xl">${seconds}</span>`
                    status.textContent = 'Inhale...'
                    if (seconds <= 0) { phase = 1; seconds = 7 }
                } 
                else if (phase === 1) {
                    circle.innerHTML = `Hold<br><span class="text-7xl">${seconds}</span>`
                    status.textContent = 'Hold...'
                    if (seconds <= 0) { phase = 2; seconds = 8 }
                } 
                else {
                    circle.innerHTML = `Exhale<br><span class="text-7xl">${seconds}</span>`
                    status.textContent = 'Exhale...'
                    if (seconds <= 0) { phase = 0; seconds = 4 }
                }
            }, 1000)
        }
        
        // Craving timer
        let cravingTimerInterval = null
        
        function startCravingTimer() {
            let timeLeft = 900 // 15 minutes in seconds
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
                    
                    // Save the note if any
                    const note = document.getElementById('craving-note').value
                    if (note) {
                        userData.cravingsToday++
                        document.getElementById('cravings-today').textContent = userData.cravingsToday
                    }
                }
            }, 1000)
        }
        
        // Simple distraction game
        function playDistraction() {
            const preview = document.getElementById('game-preview')
            preview.innerHTML = `
                <div class="relative w-40 h-40" id="orb-game">
                    <div onclick="this.style.display='none';score++" class="absolute w-8 h-8 bg-[#00d4aa] rounded-full shadow-[0_0_30px_#00d4aa] top-4 left-6 cursor-pointer"></div>
                    <div onclick="this.style.display='none';score++" class="absolute w-8 h-8 bg-[#00d4aa] rounded-full shadow-[0_0_30px_#00d4aa] top-20 right-8 cursor-pointer"></div>
                    <div onclick="this.style.display='none';score++" class="absolute w-8 h-8 bg-[#00d4aa] rounded-full shadow-[0_0_30px_#00d4aa] bottom-8 left-12 cursor-pointer"></div>
                    <div class="absolute bottom-4 left-1/2 -translate-x-1/2 text-xs font-bold text-white">CLICK THE GREEN ORBS FAST!</div>
                </div>
            `
            let score = 0
            let clicks = 0
            
            setTimeout(() => {
                const game = document.getElementById('orb-game')
                if (game) {
                    game.innerHTML += `<div class="mt-6 text-center text-2xl">Score: <span class="text-[#00d4aa]">${score}</span>/3</div>`
                    showToast(`Great job! You distracted the craving for ${score * 20} seconds.`)
                    setTimeout(() => {
                        renderFocusCards() // refresh preview
                    }, 1800)
                }
            }, 4000)
        }
        
        // Launch confetti
        function launchConfetti() {
            const colors = ['#00d4aa', '#00a88a', '#ffffff']
            for (let i = 0; i < 80; i++) {
                const confetti = document.createElement('div')
                confetti.style.position = 'fixed'
                confetti.style.zIndex = '99999'
                confetti.style.left = Math.random() * 100 + 'vw'
                confetti.style.top = '-20px'
                confetti.style.fontSize = '20px'
                confetti.style.transform = `rotate(${Math.random() * 360}deg)`
                confetti.textContent = ['🔥','🎉','🪄','💪'][Math.floor(Math.random()*4)]
                document.body.appendChild(confetti)
                
                const duration = Math.random() * 3000 + 2000
                confetti.animate([
                    { transform: `translateY(0) rotate(0deg)` },
                    { transform: `translateY(${window.innerHeight + 100}px) rotate(${Math.random()*800}deg)` }
                ], {
                    duration: duration,
                    easing: 'cubic-bezier(0.25, 0.1, 0.25, 1)'
                })
                
                setTimeout(() => confetti.remove(), duration)
            }
        }
        
        function showToast(message, isRed = false) {
            const toast = document.createElement('div')
            toast.style.cssText = `position:fixed; bottom:30px; left:50%; transform:translateX(-50%); background:${isRed ? '#f43f5e' : '#00d4aa'}; color:${isRed ? '#fff' : '#111'}; padding:18px 28px; border-radius:9999px; box-shadow:0 25px 50px -12px rgb(0 0 0 / 0.4); font-weight:600; z-index:999999; display:flex; align-items:center; gap:10px;`
            toast.innerHTML = `${message} <i onclick="this.parentElement.remove()" class="fa-solid fa-xmark ml-4"></i>`
            document.body.appendChild(toast)
            
            setTimeout(() => {
                if (toast) toast.remove()
            }, 3200)
        }
        
        // Community
        function renderCommunity() {
            const container = document.getElementById('community-posts')
            container.innerHTML = ''
            
            communityPosts.forEach(post => {
                const el = document.createElement('div')
                el.className = 'bg-zinc-900 rounded-3xl p-6 flex gap-4'
                el.innerHTML = `
                    <div class="text-5xl flex-shrink-0">${post.emoji}</div>
                    <div class="flex-1">
                        <div class="flex justify-between">
                            <div>
                                <span class="font-semibold">${post.user}</span>
                                <span class="text-zinc-500 text-sm ml-2">${post.location}</span>
                            </div>
                            <div class="flex items-center text-amber-400">
                                <i class="fa-solid fa-heart mr-1"></i> ${post.likes}
                            </div>
                        </div>
                        <p class="mt-3 text-zinc-200">${post.text}</p>
                    </div>
                `
                container.appendChild(el)
            })
        }
        
        function postToCommunity() {
            const input = document.getElementById('post-input')
            if (!input.value.trim()) return
            
            communityPosts.unshift({
                user: "Samuel",
                location: "Nairobi",
                text: input.value,
                likes: 0,
                emoji: "🏆"
            })
            
            input.value = ''
            renderCommunity()
            showToast('Posted to the community! Others will see your win.')
        }
        
        // Kenya resources modal
        function showKenyaResources() {
            alert('✅ NACADA Helpline: 1190\n✅ Mathari National Hospital: 0722 123 456\n✅ Kenya Psychiatric Association support groups available in Nairobi.\n\nYou can also visit https://nacada.go.ke for free resources.')
        }
        
        function showLocalHelp() {
            showKenyaResources()
        }
        
        // Add new addiction
        function addNewAddiction() {
            const name = prompt('What addiction do you want to overcome?', 'Porn')
            if (!name) return
            
            const key = name.toLowerCase().replace(/\s/g, '')
            
            userData.addictions[key] = {
                name: name,
                icon: ['📵','🍔','🍺','💰','🃏'][Math.floor(Math.random()*5)],
                streak: 0,
                color: '#00d4aa',
                logs: [],
                lastReset: '2026-04-14'
            }
            
            renderAddictionList()
            showToast(`✅ ${name} added. Let's beat it together!`)
        }
        
        // Profile
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
        
        // Theme toggle (for fun)
        function toggleTheme() {
            if (document.documentElement.classList.contains('dark')) {
                document.documentElement.classList.remove('dark')
            } else {
                document.documentElement.classList.add('dark')
            }
            showToast('🌗 Theme switched (demo)')
        }
        
        // Navigation
        function navigateTo(screen) {
            document.querySelectorAll('[id^="screen-"]').forEach(s => s.classList.add('hidden'))
            document.getElementById('screen-' + screen).classList.remove('hidden')
            
            if (screen === 'track') {
                showTrackerForCurrent()
            }
            if (screen === 'community') {
                renderCommunity()
            }
        }
        
        // Save / load from localStorage
        function saveToLocalStorage() {
            localStorage.setItem('overcomeUserData', JSON.stringify(userData))
        }
        
        function loadFromLocalStorage() {
            const saved = localStorage.getItem('overcomeUserData')
            if (saved) {
                userData = JSON.parse(saved)
            }
        }
        
        // Initialize everything
        function initializeApp() {
            loadFromLocalStorage()
            initializeTailwind()
            
            // Render everything
            renderAddictionList()
            renderFocusCards()
            
            // Set global streak
            document.getElementById('global-streak-global').innerHTML = `<i class="fa-solid fa-fire"></i> ${userData.globalStreak} day streak`
            document.getElementById('global-streak').textContent = userData.globalStreak
            document.getElementById('total-sober-days').textContent = userData.totalSoberDays
            document.getElementById('cravings-today').textContent = userData.cravingsToday
            
            // Random daily quote
            const randomQuote = quotes[Math.floor(Math.random() * quotes.length)]
            document.getElementById('quote-text').textContent = `"${randomQuote.text}"`
            document.getElementById('quote-author').innerHTML = `— ${randomQuote.author}`
            
            // Daily tip
            const tips = [
                "Hydrate. A dehydrated brain craves dopamine more intensely.",
                "Movement is medicine. A 10-minute walk can cut cravings by 40%.",
                "Tell one trusted person your goal today — accountability works."
            ]
            document.getElementById('daily-tip').textContent = tips[Math.floor(Math.random()*tips.length)]
            
            console.log('%c🚀 OVERCOME web app fully loaded and ready to help Samuel crush his goals!', 'color:#00d4aa; font-family:Space Grotesk; font-size:13px')
        }
        
        // Boot the app
        window.onload = initializeApp
    </script>
</body>
</html>






      












