# Samuel.ke.io
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>For Shanil ❤️</title>

<style>
body {
    margin: 0;
    font-family: 'Segoe UI', sans-serif;
    background: #fff0f5;
    color: #333;
    text-align: center;
}

header {
    background: linear-gradient(135deg, #ff758c, #ffb199);
    color: white;
    padding: 70px 20px;
}

h1 {
    font-size: 2.8em;
}

.btn {
    display: inline-block;
    margin-top: 20px;
    padding: 12px 25px;
    background: white;
    color: #ff4d6d;
    border-radius: 25px;
    text-decoration: none;
    font-weight: bold;
}

section {
    padding: 50px 20px;
}

.card-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 20px;
}

.card {
    background: white;
    padding: 20px;
    width: 260px;
    border-radius: 15px;
    box-shadow: 0 5px 15px rgba(0,0,0,0.1);
}

.timer {
    font-size: 2em;
    color: #ff4d6d;
    margin-top: 15px;
}

footer {
    background: #ffc2d1;
    padding: 20px;
}
</style>
</head>

<body>

<header>
    <h1>Shanil ❤️</h1>
    <p>No matter the distance, you’re always close to my heart.</p>
    <a href="#activities" class="btn">Our Moments</a>
</header>

<section>
    <h2>💌 A Message For You</h2>
    <p>
        Shanil, every day apart just makes me appreciate you more.
        Distance may keep us physically apart, but nothing can break what we have.
        I miss you, I think about you, and I can't wait for the day I see you again ❤️
    </p>
</section>

<section id="activities">
    <h2>🎮 Fun Things We Can Do Together</h2>
    <div class="card-container">
        <div class="card">
            <h3>🎬 Movie Nights</h3>
            <p>Pick a movie, press play at the same time, and text while watching.</p>
        </div>
        <div class="card">
            <h3>🎧 Music Dates</h3>
            <p>Create a playlist together and listen at the same time.</p>
        </div>
        <div class="card">
            <h3>❓ Question Game</h3>
            <p>Ask each other random or deep questions every night.</p>
        </div>
        <div class="card">
            <h3>🍝 Virtual Dinner</h3>
            <p>Cook the same meal and eat together on video call.</p>
        </div>
        <div class="card">
            <h3>📱 Game Night</h3>
            <p>Play mobile games together and compete or team up.</p>
        </div>
        <div class="card">
            <h3>💖 Memory Sharing</h3>
            <p>Send each other photos and talk about your favorite memories.</p>
        </div>
    </div>
</section>

<section>
    <h2>🕒 Countdown Until I See You</h2>
    <input type="date" id="dateInput">
    <div class="timer" id="countdown"></div>
</section>

<footer>
    <p>Made with love, just for you Shanil ❤️</p>
</footer>

<script>
const dateInput = document.getElementById("dateInput");
const countdown = document.getElementById("countdown");

dateInput.addEventListener("change", () => {
    const target = new Date(dateInput.value).getTime();

    const timer = setInterval(() => {
        const now = new Date().getTime();
        const diff = target - now;

        if (diff <= 0) {
            countdown.innerHTML = "Finally together ❤️";
            clearInterval(timer);
            return;
        }

        const days = Math.floor(diff / (1000 * 60 * 60 * 24));
        countdown.innerHTML = days + " days left 💕";
    }, 1000);
});
</script>
<section id="interactive">
    <h2>🎮 Let’s Do Something Together</h2>

    <div class="card-container">

        <!-- RANDOM QUESTION -->
        <div class="card">
            <h3>❓ Question Game</h3>
            <p id="question">Click below to get a question</p>
            <button onclick="newQuestion()">New Question</button>
        </div>

        <!-- SPIN THE DATE -->
        <div class="card">
            <h3>🎡 Pick Our Activity</h3>
            <p id="activity">Click to decide what we do</p>
            <button onclick="spinActivity()">Spin</button>
        </div>

        <!-- LOVE NOTES -->
        <div class="card">
            <h3>💌 Love Notes</h3>
            <input id="noteInput" placeholder="Write something sweet..." />
            <button onclick="saveNote()">Send</button>
            <p id="savedNote"></p>
        </div>

    </div>
</section>
</body>
</html>
