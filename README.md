<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SyncHeart • Samuel & Mia</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=Playfair+Display:wght@700&display=swap');
        
        :root { --pink: #e11d8a; }
        
        * { transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1); }
        
        .logo-font { font-family: 'Playfair Display', sans-serif; }
        .header-gradient { background: linear-gradient(90deg, #e11d8a, #7e22ce); }
        
        .modal { animation: modalPop 0.4s cubic-bezier(0.34, 1.56, 0.64, 1); }
        @keyframes modalPop {
            from { transform: scale(0.9) translateY(40px); opacity: 0; }
            to { transform: scale(1) translateY(0); opacity: 1; }
        }
        
        .slide { transition: opacity 900ms ease-in-out; }
        .heart-float { animation: heartRise 2.8s ease-out forwards; }
        
        @keyframes heartRise {
            0% { transform: translateY(0) scale(0.5); opacity: 1; }
            100% { transform: translateY(-320px) scale(1.6); opacity: 0; }
        }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 min-h-screen flex flex-col">

    <!-- HEADER -->
    <header class="header-gradient text-white sticky top-0 z-50 shadow-2xl">
        <div class="max-w-screen-2xl mx-auto px-8 py-4 flex items-center justify-between">
            <div class="flex items-center gap-x-3">
                <div class="w-11 h-11 bg-white rounded-2xl flex items-center justify-center text-3xl shadow-inner">❤️</div>
                <h1 class="logo-font text-3xl tracking-tight">SyncHeart</h1>
                <span class="text-xs bg-white/20 px-3 py-1 rounded-full">Samuel & Mia</span>
            </div>

            <nav class="flex items-center gap-x-9 text-sm font-medium">
                <a onclick="navigateTo(0)" id="nav-0" class="nav-link flex items-center gap-x-2 active"><i class="fa-solid fa-house"></i> Home</a>
                <a onclick="navigateTo(1)" id="nav-1" class="nav-link flex items-center gap-x-2"><i class="fa-solid fa-gamepad"></i> Games</a>
                <a onclick="navigateTo(2)" id="nav-2" class="nav-link flex items-center gap-x-2"><i class="fa-solid fa-comments"></i> Chat</a>
                <a onclick="navigateTo(3)" id="nav-3" class="nav-link flex items-center gap-x-2"><i class="fa-solid fa-images"></i> Slide Pic</a>
                <a onclick="navigateTo(4)" id="nav-4" class="nav-link flex items-center gap-x-2"><i class="fa-solid fa-heart-circle-check"></i> Memories</a>
            </nav>

            <div class="flex items-center gap-x-5">
                <button onclick="openSyncControlModal()" class="flex items-center gap-2 bg-white/10 hover:bg-white/20 px-6 py-3 rounded-3xl text-sm">
                    <i class="fa-solid fa-sync"></i> Sync
                </button>
                <div onclick="sendVirtualHug()" class="text-3xl cursor-pointer hover:scale-125">❤️</div>
                <div class="flex items-center gap-3 bg-white/10 px-4 py-2 rounded-3xl">
                    <div class="w-8 h-8 bg-gradient-to-br from-pink-400 to-purple-400 rounded-2xl flex items-center justify-center text-xl">👩🏻</div>
                    <div>
                        <p class="text-sm font-semibold">Mia</p>
                        <p class="text-[10px] text-emerald-300">Online • Nairobi</p>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <div class="flex flex-1 max-w-screen-2xl mx-auto w-full px-8 py-8 gap-8">

        <!-- MAIN AREA -->
        <div id="main-content" class="flex-1">

            <!-- HOME (Screen 0) -->
            <div id="screen-0" class="screen">
                <h1 class="text-6xl font-bold logo-font mb-2">Hey Samuel ❤️</h1>
                <p class="text-2xl text-slate-400">Mia is thinking about you right now</p>
                
                <div class="grid grid-cols-3 gap-6 mt-12">
                    <div onclick="navigateTo(3)" class="bg-gradient-to-br from-pink-500/10 to-rose-500/10 border border-pink-400/30 rounded-3xl p-8 cursor-pointer hover:scale-105">
                        <div class="text-6xl mb-6">📸</div>
                        <h3 class="text-2xl font-semibold">Slide Pic for Mia</h3>
                        <p class="text-slate-400 mt-3">Private romantic photos only she can see</p>
                    </div>
                    <div onclick="navigateTo(1)" class="bg-gradient-to-br from-violet-500/10 to-purple-500/10 border border-violet-400/30 rounded-3xl p-8 cursor-pointer hover:scale-105">
                        <div class="text-6xl mb-6">🎮</div>
                        <h3 class="text-2xl font-semibold">Play Games Together</h3>
                        <p class="text-slate-400 mt-3">New games added just for you two</p>
                    </div>
                    <div onclick="sendVirtualHug()" class="bg-gradient-to-br from-rose-400/10 to-pink-500/10 border border-rose-400/30 rounded-3xl p-8 cursor-pointer hover:scale-105 flex flex-col justify-between">
                        <div>
                            <div class="text-6xl mb-6">🤗</div>
                            <h3 class="text-2xl font-semibold">Send Her a Hug</h3>
                        </div>
                        <p class="text-emerald-400 text-sm">She felt the last one 💕</p>
                    </div>
                </div>
            </div>

            <!-- GAMES SCREEN (Screen 1) - Now with more games -->
            <div id="screen-1" class="screen hidden">
                <h2 class="text-4xl font-semibold mb-2">Games for Samuel & Mia</h2>
                <p class="text-slate-400 mb-10">Play together in real-time • Everything syncs instantly</p>
                
                <div class="grid grid-cols-4 gap-6">
                    <!-- Tic Tac Toe -->
                    <div onclick="startGame(0)" class="game-card bg-gradient-to-br from-amber-400 to-orange-500 text-white rounded-3xl p-8 h-80 flex flex-col hover:scale-105 cursor-pointer">
                        <div class="text-7xl mb-auto">⭕❌</div>
                        <div>
                            <h4 class="text-2xl font-semibold">Tic-Tac-Toe</h4>
                            <p class="opacity-90 text-sm mt-1">Classic showdown • Last winner: Mia</p>
                        </div>
                    </div>

                    <!-- Memory Match -->
                    <div onclick="startGame(1)" class="game-card bg-gradient-to-br from-cyan-400 to-blue-500 text-white rounded-3xl p-8 h-80 flex flex-col hover:scale-105 cursor-pointer">
                        <div class="text-7xl mb-auto">🧠</div>
                        <div>
                            <h4 class="text-2xl font-semibold">Memory Match</h4>
                            <p class="opacity-90 text-sm mt-1">Match our shared memories</p>
                        </div>
                    </div>

                    <!-- Would You Rather -->
                    <div onclick="startGame(2)" class="game-card bg-gradient-to-br from-purple-400 to-pink-500 text-white rounded-3xl p-8 h-80 flex flex-col hover:scale-105 cursor-pointer">
                        <div class="text-7xl mb-auto">🤔</div>
                        <div>
                            <h4 class="text-2xl font-semibold">Would You Rather</h4>
                            <p class="opacity-90 text-sm mt-1">Fun & deep questions</p>
                        </div>
                    </div>

                    <!-- Truth or Dare -->
                    <div onclick="startGame(3)" class="game-card bg-gradient-to-br from-rose-400 to-red-500 text-white rounded-3xl p-8 h-80 flex flex-col hover:scale-105 cursor-pointer">
                        <div class="text-7xl mb-auto">🔥</div>
                        <div>
                            <h4 class="text-2xl font-semibold">Truth or Dare</h4>
                            <p class="opacity-90 text-sm mt-1">Get closer tonight</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- CHAT SCREEN (Screen 2) -->
            <div id="screen-2" class="screen hidden flex flex-col h-full">
                <!-- Chat UI from previous version - kept functional -->
                <div class="bg-slate-900 rounded-3xl flex-1 flex flex-col">
                    <div class="p-6 border-b border-white/10 flex items-center justify-between">
                        <div class="flex items-center gap-4">
                            <div class="text-3xl">👩🏻</div>
                            <div>
                                <p class="font-semibold">Mia Patel</p>
                                <p class="text-emerald-400 text-sm">Online • Typing...</p>
                            </div>
                        </div>
                    </div>
                    <div id="chat-window" class="flex-1 p-6 overflow-y-auto space-y-6"></div>
                    <div class="p-6 border-t border-white/10">
                        <div class="flex bg-slate-800 rounded-3xl">
                            <input id="chat-input" type="text" placeholder="Message Mia..." 
                                   class="flex-1 bg-transparent px-6 py-5 outline-none">
                            <button onclick="sendMessage()" class="px-8 text-pink-400"><i class="fa-solid fa-paper-plane"></i></button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- SLIDE PIC SCREEN (Screen 3) - Personalized for Mia -->
            <div id="screen-3" class="screen hidden flex flex-col h-full">
                <div class="flex justify-between mb-8">
                    <div>
                        <h2 class="text-5xl font-semibold logo-font">Slide Pic for Mia ❤️</h2>
                        <p class="text-slate-400">Private photos only she sees</p>
                    </div>
                    <button onclick="addNewSlidePic()" 
                            class="bg-white text-pink-600 px-8 py-4 rounded-3xl font-semibold flex items-center gap-3">
                        <i class="fa-solid fa-plus"></i> Add Photo for Mia
                    </button>
                </div>

                <div class="flex-1 slide-container bg-slate-900 rounded-3xl relative overflow-hidden shadow-2xl" style="height: 580px;">
                    <div id="slides-wrapper" class="relative w-full h-full"></div>
                    
                    <button onclick="prevSlide()" class="absolute left-8 top-1/2 -translate-y-1/2 bg-black/50 hover:bg-black/70 w-12 h-12 rounded-2xl flex items-center justify-center text-4xl">‹</button>
                    <button onclick="nextSlide()" class="absolute right-8 top-1/2 -translate-y-1/2 bg-black/50 hover:bg-black/70 w-12 h-12 rounded-2xl flex items-center justify-center text-4xl">›</button>
                    
                    <button onclick="likeCurrentSlide()" 
                            class="absolute bottom-8 right-8 bg-white text-pink-600 w-16 h-16 rounded-3xl text-4xl shadow-2xl hover:scale-110">❤️</button>
                </div>
                
                <div class="mt-6 flex justify-between items-center">
                    <p id="slide-caption" class="text-xl font-medium"></p>
                    <p id="slide-counter" class="text-slate-400"></p>
                </div>
            </div>

            <!-- MEMORIES (Screen 4) -->
            <div id="screen-4" class="screen hidden">
                <h2 class="text-4xl font-semibold mb-8">Samuel & Mia Memories</h2>
                <div id="memory-grid" class="grid grid-cols-4 gap-6"></div>
            </div>
        </div>

        <!-- RIGHT PANEL -->
        <div class="w-80 bg-slate-900 rounded-3xl p-6">
            <p class="uppercase text-xs tracking-widest mb-4">Right now with Mia</p>
            <div class="space-y-6">
                <div onclick="navigateTo(1)" class="cursor-pointer bg-white/5 p-5 rounded-3xl hover:bg-white/10">
                    <p class="text-emerald-400 text-xs">GAME INVITE</p>
                    <p class="font-medium">Mia wants to play Would You Rather</p>
                </div>
            </div>
        </div>
    </div>

    <!-- GAMES MODALS -->
    <div id="game-modal" class="hidden fixed inset-0 bg-black/90 flex items-center justify-center z-[9999]">
        <div onclick="event.stopImmediatePropagation()" class="modal bg-slate-900 w-[720px] rounded-3xl p-8">
            <div class="flex justify-between mb-6">
                <h3 id="game-title" class="text-3xl font-semibold"></h3>
                <button onclick="closeGameModal()" class="text-3xl">✕</button>
            </div>
            <div id="game-content" class="min-h-[420px]"></div>
        </div>
    </div>

    <!-- Slide Pic Add Modal -->
    <div id="add-photo-modal" class="hidden fixed inset-0 bg-black/90 flex items-center justify-center z-[99999]">
        <div onclick="event.stopImmediatePropagation()" class="modal bg-slate-900 w-96 rounded-3xl p-8">
            <h3 class="text-xl font-semibold mb-6">Add a photo for Mia</h3>
            <input type="file" id="photo-upload" accept="image/*" class="hidden" onchange="previewAndAddPhoto(event)">
            <button onclick="document.getElementById('photo-upload').click()" 
                    class="w-full py-12 border-2 border-dashed border-slate-600 rounded-3xl text-pink-400 hover:border-pink-400">
                Upload Photo
            </button>
            <div class="mt-8">
                <input id="photo-caption-input" placeholder="Sweet caption for Mia..." class="w-full bg-slate-800 rounded-2xl px-5 py-4">
            </div>
            <button onclick="addPhotoToSlides()" 
                    class="mt-6 w-full bg-pink-500 py-4 rounded-3xl font-semibold">Add to Slide Pic</button>
        </div>
    </div>

    <script>
        // ===================== PERSONALIZED DATA =====================
        const coupleName = "Samuel & Mia";

        // Slide Pics - Dedicated to Mia
        let slidePics = [
            { url: "https://picsum.photos/id/1011/1200/800", caption: "Your smile lights up my whole day", date: "Apr 10" },
            { url: "https://picsum.photos/id/1005/1200/800", caption: "Missing your laugh already", date: "Apr 8" },
            { url: "https://picsum.photos/id/201/1200/800", caption: "Our virtual sunset date", date: "Apr 5" },
        ];
        let currentSlideIndex = 0;
        let autoSlide = null;

        // Games
        let currentGame = 0;

        // Chat simulation
        let messages = [
            { from: "mia", text: "I can't stop smiling after our call last night 🥰", time: "11:12" },
            { from: "you", text: "Same here ❤️", time: "11:15" }
        ];

        // ===================== NAVIGATION =====================
        function navigateTo(n) {
            document.querySelectorAll('.screen').forEach(s => s.classList.add('hidden'));
            document.getElementById(`screen-${n}`).classList.remove('hidden');

            document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
            document.getElementById(`nav-${n}`).classList.add('active');

            if (n === 3) renderSlides();
        }

        // ===================== SLIDE PIC =====================
        function renderSlides() {
            const wrapper = document.getElementById('slides-wrapper');
            wrapper.innerHTML = '';
            
            slidePics.forEach((pic, i) => {
                const div = document.createElement('div');
                div.className = `slide absolute inset-0 bg-cover bg-center ${i === currentSlideIndex ? 'opacity-100' : 'opacity-0'}`;
                div.style.backgroundImage = `url(${pic.url})`;
                wrapper.appendChild(div);
            });

            document.getElementById('slide-caption').textContent = slidePics[currentSlideIndex].caption;
            document.getElementById('slide-counter').textContent = `${currentSlideIndex + 1}/${slidePics.length}`;
        }

        function nextSlide() {
            currentSlideIndex = (currentSlideIndex + 1) % slidePics.length;
            renderSlides();
        }

        function prevSlide() {
            currentSlideIndex = (currentSlideIndex - 1 + slidePics.length) % slidePics.length;
            renderSlides();
        }

        function likeCurrentSlide() {
            for (let i = 0; i < 12; i++) {
                setTimeout(() => {
                    const heart = document.createElement('div');
                    heart.textContent = '❤️';
                    heart.className = 'heart-float text-5xl absolute';
                    heart.style.left = Math.random() * 80 + 10 + '%';
                    heart.style.bottom = '30%';
                    document.getElementById('slides-wrapper').appendChild(heart);
                    setTimeout(() => heart.remove(), 3000);
                }, i * 70);
            }
        }

        function addNewSlidePic() {
            document.getElementById('add-photo-modal').classList.remove('hidden');
            document.getElementById('add-photo-modal').classList.add('flex');
        }

        function previewAndAddPhoto(e) {
            // Demo - in real app you would upload
            const caption = document.getElementById('photo-caption-input').value || "Beautiful moment for you";
            slidePics.unshift({
                url: "https://picsum.photos/id/" + Math.floor(Math.random()*400) + "/1200/800",
                caption: caption,
                date: "Just now"
            });
            hideAddPhotoModal();
            currentSlideIndex = 0;
            renderSlides();
        }

        function hideAddPhotoModal() {
            document.getElementById('add-photo-modal').classList.add('hidden');
            document.getElementById('add-photo-modal').classList.remove('flex');
        }

        function addPhotoToSlides() {
            previewAndAddPhoto();
        }

        // ===================== GAMES =====================
        function startGame(gameId) {
            currentGame = gameId;
            document.getElementById('game-modal').classList.remove('hidden');
            document.getElementById('game-modal').classList.add('flex');

            const title = document.getElementById('game-title');
            const content = document.getElementById('game-content');

            if (gameId === 0) {
                title.textContent = "Tic-Tac-Toe • Samuel vs Mia";
                content.innerHTML = `
                    <div class="grid grid-cols-3 gap-3 max-w-xs mx-auto mt-10" id="ttt-board"></div>
                    <p class="text-center mt-8 text-emerald-400" id="ttt-status">Your turn (X)</p>
                `;
                initTicTacToe();
            } 
            else if (gameId === 1) {
                title.textContent = "Memory Match • Our Memories";
                content.innerHTML = `<p class="text-center text-2xl mt-20">Memory Match Game Coming Soon<br><span class="text-pink-400">Samuel & Mia Edition</span></p>`;
            } 
            else if (gameId === 2) {
                title.textContent = "Would You Rather";
                content.innerHTML = `
                    <div class="space-y-8 mt-12">
                        <div onclick="answerWYR(0)" class="bg-slate-800 hover:bg-pink-500/20 p-6 rounded-3xl cursor-pointer">Live in Nairobi forever with me or travel the world together?</div>
                        <div onclick="answerWYR(1)" class="bg-slate-800 hover:bg-pink-500/20 p-6 rounded-3xl cursor-pointer">Never argue again or never be apart again?</div>
                    </div>
                `;
            } 
            else if (gameId === 3) {
                title.textContent = "Truth or Dare • Samuel & Mia";
                content.innerHTML = `
                    <div class="flex gap-6 justify-center mt-20">
                        <button onclick="chooseTruth()" class="px-12 py-6 bg-purple-600 rounded-3xl text-xl">Truth</button>
                        <button onclick="chooseDare()" class="px-12 py-6 bg-rose-600 rounded-3xl text-xl">Dare</button>
                    </div>
                `;
            }
        }

        function closeGameModal() {
            document.getElementById('game-modal').classList.add('hidden');
            document.getElementById('game-modal').classList.remove('flex');
        }

        // Simple Tic-Tac-Toe
        let tttBoard = Array(9).fill(null);
        let tttPlayer = 'X';

        function initTicTacToe() {
            tttBoard = Array(9).fill(null);
            const boardEl = document.getElementById('ttt-board');
            boardEl.innerHTML = '';
            for (let i = 0; i < 9; i++) {
                const cell = document.createElement('div');
                cell.className = 'aspect-square bg-slate-800 rounded-2xl flex items-center justify-center text-6xl cursor-pointer';
                cell.onclick = () => tttMove(i);
                boardEl.appendChild(cell);
            }
        }

        function tttMove(i) {
            if (tttBoard[i]) return;
            tttBoard[i] = tttPlayer;
            document.querySelectorAll('#ttt-board > div')[i].textContent = tttPlayer;
            
            if (checkTTTWin(tttPlayer)) {
                document.getElementById('ttt-status').innerHTML = `🎉 Samuel wins!`;
                return;
            }
            tttPlayer = 'O';
            document.getElementById('ttt-status').innerHTML = `Mia's turn (O)`;
            
            // Simulate Mia move
            setTimeout(() => {
                const empty = tttBoard.map((v,i) => v===null ? i : null).filter(v=>v!==null);
                if (empty.length) {
                    const move = empty[Math.floor(Math.random()*empty.length)];
                    tttBoard[move] = 'O';
                    document.querySelectorAll('#ttt-board > div')[move].textContent = 'O';
                    if (checkTTTWin('O')) document.getElementById('ttt-status').innerHTML = `Mia wins this round 💕`;
                }
            }, 800);
        }

        function checkTTTWin(p) {
            const wins = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
            return wins.some(combo => combo.every(i => tttBoard[i] === p));
        }

        function answerWYR(choice) {
            const responses = ["Mia says: Same! ❤️", "Mia chose the other option and is blushing"];
            alert(responses[choice]);
        }

        function chooseTruth() {
            alert("Truth: What is one thing you love most about Samuel?");
        }

        function chooseDare() {
            alert("Dare: Send Samuel a voice note saying how much you miss him right now 💕");
        }

        // ===================== OTHER FEATURES =====================
        function sendVirtualHug() {
            for (let i = 0; i < 15; i++) {
                setTimeout(() => {
                    const h = document.createElement('div');
                    h.textContent = '❤️';
                    h.style.position = 'fixed';
                    h.style.left = Math.random() * 100 + 'vw';
                    h.style.top = '60%';
                    h.style.fontSize = '50px';
                    document.body.appendChild(h);
                    h.animate([{transform:'translateY(0)'},{transform:'translateY(-600px)'}], {duration:1800, easing:'ease-out'});
                    setTimeout(() => h.remove(), 2000);
                }, i*50);
            }
        }

        function sendMessage() {
            const input = document.getElementById('chat-input');
            if (!input.value) return;
            // Add message logic here (same as previous versions)
            input.value = '';
        }

        function openSyncControlModal() {
            alert("Sync Controls opened\n\nVideo & Music sync perfectly between Samuel and Mia");
        }

        // Initialize
        function initApp() {
            navigateTo(0);
            console.log('%c❤️ SyncHeart for Samuel & Mia is ready', 'color:#e11d8a;font-size:16px');
        }

        window.onload = initApp;
    </script>
</body>
</html>
