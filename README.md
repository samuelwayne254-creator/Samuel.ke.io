<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>You Are Not Alone</title>

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #f4f8fb;
    color: #333;
}

header {
    background: linear-gradient(135deg, #6a9fb5, #b8d8e3);
    color: white;
    text-align: center;
    padding: 60px 20px;
}

section {
    padding: 40px 20px;
    text-align: center;
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

button {
    padding: 10px 20px;
    border: none;
    background: #6a9fb5;
    color: white;
    border-radius: 20px;
    cursor: pointer;
}

textarea {
    width: 80%;
    height: 80px;
    margin-top: 10px;
}

.quote {
    font-style: italic;
    margin-top: 10px;
}

footer {
    background: #dbeef3;
    padding: 20px;
}
</style>
</head>

<body>

<header>
    <h1>You Are Not Alone 💙</h1>
    <p>Small steps. Real progress. One day at a time.</p>
</header>

<section>
    <h2>🌱 Daily Support Tools</h2>

    <div class="card-container">

        <!-- MOTIVATION -->
        <div class="card">
            <h3>💬 Motivation</h3>
            <p id="quote">Click to get encouragement</p>
            <button onclick="newQuote()">Inspire Me</button>
        </div>

        <!-- DISTRACTION -->
        <div class="card">
            <h3>🧠 Healthy Distraction</h3>
            <p id="activity">Click for something to do</p>
            <button onclick="newActivity()">Help Me</button>
        </div>

        <!-- JOURNAL -->
        <div class="card">
            <h3>📝 Journal</h3>
            <textarea id="journal" placeholder="Write how you feel..."></textarea>
            <button onclick="saveJournal()">Save</button>
        </div>

    </div>
</section>

<section>
    <h2>⏳ Stay Strong</h2>
    <p>You’ve made it this far. That means something.</p>
    <div id="timer" style="font-size: 2em;"></div>
</section>

<section>
    <h2>🚨 Need Immediate Help?</h2>
    <p>If you're struggling right now, please reach out to someone you trust or a local support line.</p>
    <p>You deserve support. You don’t have to go through this alone.</p>
</section>

<footer>
    <p>Recovery is not perfect—but it is possible 💙</p>
</footer>

<script>

// MOTIVATION
const quotes = [
"You’ve survived 100% of your hardest days.",
"This feeling will pass.",
"You are stronger than the urge.",
"Progress, not perfection.",
"One step at a time is enough.",
"You are not your addiction."
];

function newQuote() {
    const random = quotes[Math.floor(Math.random() * quotes.length)];
    document.getElementById("quote").innerText = random;
}

// ACTIVITIES
const activities = [
"Go for a short walk 🚶",
"Drink a glass of water 💧",
"Call a friend 📞",
"Listen to calming music 🎧",
"Take deep breaths for 1 minute 🧘",
"Write down your thoughts 📝"
];

function newActivity() {
    const random = activities[Math.floor(Math.random() * activities.length)];
    document.getElementById("activity").innerText = random;
}

// JOURNAL
function saveJournal() {
    const text = document.getElementById("journal").value;
    localStorage.setItem("journalEntry", text);
    alert("Saved. You're doing great 💙");
}

// LOAD JOURNAL
window.onload = () => {
    const saved = localStorage.getItem("journalEntry");
    if (saved) {
        document.getElementById("journal").value = saved;
    }
};

// SIMPLE TIMER (session)
let seconds = 0;
setInterval(() => {
    seconds++;
    document.getElementById("timer").innerText =
        Math.floor(seconds / 60) + " min " + (seconds % 60) + " sec";
}, 1000);

</script>

</body>
</html>





