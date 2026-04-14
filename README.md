<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
  <title>Safe Harbor | Recovery Space</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: #f4f1ea;
      font-family: system-ui, 'Segoe UI', 'Roboto', 'Helvetica Neue', sans-serif;
      line-height: 1.5;
      color: #1e2a2e;
      padding: 2rem 1rem;
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
    }

    /* header */
    .header {
      text-align: center;
      margin-bottom: 3rem;
    }

    .shield {
      font-size: 3rem;
      margin-bottom: 0.5rem;
    }

    h1 {
      font-size: 2.2rem;
      letter-spacing: -0.01em;
      background: linear-gradient(135deg, #2c5f2d, #5f8b6f);
      background-clip: text;
      -webkit-background-clip: text;
      color: transparent;
      margin-bottom: 0.5rem;
    }

    .tagline {
      font-size: 1.2rem;
      color: #4a5b55;
      max-width: 600px;
      margin: 0 auto;
      font-weight: 400;
    }

    .privacy-note {
      background: #e6e3d8;
      display: inline-block;
      padding: 0.3rem 1rem;
      border-radius: 40px;
      font-size: 0.8rem;
      margin-top: 1rem;
      color: #2c4b3e;
    }

    /* cards grid */
    .help-grid {
      display: flex;
      flex-wrap: wrap;
      gap: 1.8rem;
      justify-content: center;
      margin-bottom: 3rem;
    }

    .card {
      background: white;
      border-radius: 2rem;
      padding: 1.5rem;
      flex: 1;
      min-width: 220px;
      max-width: 260px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.05);
      transition: all 0.2s ease;
      cursor: pointer;
      border: 1px solid #e2dfd3;
      text-align: center;
    }

    .card:hover {
      transform: translateY(-5px);
      box-shadow: 0 18px 30px rgba(0, 0, 0, 0.1);
      border-color: #b7c9b1;
    }

    .card-emoji {
      font-size: 2.5rem;
      margin-bottom: 0.75rem;
    }

    .card h3 {
      font-size: 1.5rem;
      margin-bottom: 0.5rem;
      color: #2c5f2d;
    }

    .card p {
      color: #3d4f48;
      font-size: 0.9rem;
    }

    /* dynamic help section */
    .help-panel {
      background: white;
      border-radius: 2rem;
      padding: 2rem;
      margin-bottom: 2rem;
      box-shadow: 0 8px 24px rgba(0, 0, 0, 0.05);
      border: 1px solid #e5e0d2;
    }

    .help-title {
      font-size: 1.6rem;
      font-weight: 600;
      margin-bottom: 0.5rem;
      color: #2c3e2b;
      display: flex;
      align-items: center;
      gap: 10px;
      flex-wrap: wrap;
    }

    .help-content {
      font-size: 1.05rem;
      color: #2e3f3a;
      margin: 1rem 0;
      padding: 1rem 0;
      border-top: 1px solid #ede8db;
      border-bottom: 1px solid #ede8db;
    }

    .resource-btn {
      background: #2c5f2d;
      color: white;
      border: none;
      padding: 0.6rem 1.5rem;
      border-radius: 40px;
      font-size: 0.9rem;
      font-weight: 500;
      cursor: pointer;
      transition: 0.2s;
      margin-top: 0.5rem;
      display: inline-block;
    }

    .resource-btn:hover {
      background: #1f4520;
      transform: scale(0.97);
    }

    /* coping & breathing */
    .tools-section {
      display: flex;
      flex-wrap: wrap;
      gap: 1.5rem;
      margin-bottom: 2rem;
    }

    .tool-card {
      background: #ffffffdb;
      backdrop-filter: blur(2px);
      background: white;
      flex: 1;
      min-width: 240px;
      border-radius: 1.5rem;
      padding: 1.5rem;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.03);
      border: 1px solid #e2ddcf;
    }

    .tool-card h3 {
      font-size: 1.4rem;
      margin-bottom: 1rem;
      color: #2f5e3a;
    }

    .tip-text {
      font-size: 1.1rem;
      background: #f9f7f0;
      padding: 1rem;
      border-radius: 1rem;
      margin: 0.5rem 0;
      font-style: italic;
    }

    button {
      background: #97b791;
      border: none;
      padding: 0.6rem 1.2rem;
      border-radius: 3rem;
      font-weight: 500;
      cursor: pointer;
      transition: 0.2s;
      color: #1e2a1c;
      font-size: 0.9rem;
    }

    button:hover {
      background: #7f9e78;
    }

    .breathing-circle {
      width: 80px;
      height: 80px;
      background: #cbdcc2;
      border-radius: 50%;
      margin: 1rem auto;
      transition: transform 4s ease;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: bold;
      color: #2b4727;
      cursor: pointer;
    }

    .breathing-circle.animate {
      transform: scale(1.5);
      background: #9bbf8f;
    }

    .crisis {
      background: #fef4e8;
      border-left: 6px solid #c47a44;
      padding: 1rem 1.5rem;
      border-radius: 1.5rem;
      margin-top: 2rem;
    }

    footer {
      margin-top: 3rem;
      text-align: center;
      font-size: 0.8rem;
      color: #6f7c74;
      border-top: 1px solid #ded9cc;
      padding-top: 2rem;
    }

    @media (max-width: 700px) {
      body {
        padding: 1rem;
      }
      .help-title {
        font-size: 1.3rem;
      }
    }
  </style>
</head>
<body>
<div class="container">
  <div class="header">
    <div class="shield">🛡️🌿</div>
    <h1>Safe Harbor</h1>
    <div class="tagline">no shame · no judgment · just support</div>
    <div class="privacy-note">🔒 completely anonymous · your browser, your space</div>
  </div>

  <!-- addiction categories -->
  <div class="help-grid">
    <div class="card" data-addiction="alcohol">
      <div class="card-emoji">🍷➡️💧</div>
      <h3>Alcohol</h3>
      <p>tools to cut back & find community</p>
    </div>
    <div class="card" data-addiction="substances">
      <div class="card-emoji">💊⚡</div>
      <h3>Drugs</h3>
      <p>recovery pathways & harm reduction</p>
    </div>
    <div class="card" data-addiction="gaming">
      <div class="card-emoji">🎮🕹️</div>
      <h3>Gaming</h3>
      <p>balance & real-life joy again</p>
    </div>
    <div class="card" data-addiction="internet">
      <div class="card-emoji">📱💻</div>
      <h3>Internet/Phone</h3>
      <p>digital boundaries & mindful usage</p>
    </div>
    <div class="card" data-addiction="shopping">
      <div class="card-emoji">🛍️💳</div>
      <h3>Shopping</h3>
      <p>spending less, feeling more</p>
    </div>
  </div>

  <!-- dynamic help output -->
  <div class="help-panel" id="helpPanel">
    <div class="help-title">
      <span>🤝</span> <span id="selectedAddiction">Choose an addiction above</span>
    </div>
    <div class="help-content" id="helpContent">
      Click any card — we'll show you first steps, coping strategies, and resources.
    </div>
    <button id="moreResourcesBtn" style="background:#e2dfd3; color:#2c4b3e;">📘 Show local / online resources</button>
    <div id="extraResources" style="margin-top: 1rem; font-size: 0.9rem;"></div>
  </div>

  <!-- tools: daily tip + breathing -->
  <div class="tools-section">
    <div class="tool-card">
      <h3>🌱 daily grounding tip</h3>
      <div class="tip-text" id="dailyTip">Loading a gentle reminder...</div>
      <button id="newTipBtn">🔄 new tip</button>
    </div>
    <div class="tool-card">
      <h3>🧘 4-second breathing buddy</h3>
      <div class="breathing-circle" id="breathCircle">breathe</div>
      <p style="margin-top: 0.5rem; font-size:0.85rem;">click the circle → inhale while it grows, exhale as it shrinks (4 sec in, 4 out)</p>
    </div>
  </div>

  <!-- crisis support -->
  <div class="crisis">
    <strong>🆘 if you're in crisis right now</strong><br>
    You matter. Please call or text a helpline (24/7, confidential):<br>
    🇺🇸 SAMHSA: 1-800-662-4357  |  Crisis Text Line: text HOME to 741741<br>
    🌍 International: <a href="https://findahelpline.com" target="_blank" style="color:#c47a44;">findahelpline.com</a><br>
    <span style="font-size:0.8rem;">💙 You are not alone. There is no shame in asking for help.</span>
  </div>
  <footer>
    Safe Harbor – a judgment-free zone. Every step counts, no matter how small.
  </footer>
</div>

<script>
  // Addiction-specific help data
  const helpData = {
    alcohol: {
      title: "🍃 Alcohol support",
      content: "You're not alone. Many people change their drinking habits. Start with one alcohol-free day, track drinks, or join an online support group like SMART Recovery or AA meetings (many are virtual).",
      extra: "🔹 Try the 'I Am Sober' app · 🔹 Talk to a doctor about naltrexone · 🔹 r/stopdrinking (supportive subreddit)"
    },
    substances: {
      title: "💚 Substance use recovery",
      content: "Recovery isn't linear — every moment you choose health is a win. Look into harm reduction, therapy, or peer support (NA, Dharma Recovery).",
      extra: "🔹 Never use alone · 🔹 Fentanyl test strips save lives · 🔹 SAMHSA helpline 1-800-662-4357 · 🔹 Neverquit podcast"
    },
    gaming: {
      title: "🎮 Healthy gaming balance",
      content: "Gaming addiction is real, and so is recovery. Set screen timers, find offline hobbies, and connect with others who understand (Game Quitters community).",
      extra: "🔹 Use console parental controls · 🔹 90-day 'game detox' challenge · 🔹 Cam Adair's Game Quitters forum"
    },
    internet: {
      title: "📵 Digital wellness",
      content: "Mindless scrolling happens to all of us. Try phone-free hours, grayscale mode, or app blockers like Freedom / Opal. Small breaks rewire your brain.",
      extra: "🔹 No phone in bedroom · 🔹 30-min morning without screen · 🔹 r/nosurf community"
    },
    shopping: {
      title: "💸 Spending & shopping awareness",
      content: "Impulse buying often masks emotions. Pause before buying, wait 24h, unlink one-click payments, and find free comforts (nature, music, tea).",
      extra: "🔹 Debtors Anonymous meetings · 🔹 'Do I need it?' challenge · 🔹 Unsubscribe from sale emails"
    }
  };

  let currentAddiction = null;

  function updateHelpPanel(addictionKey) {
    const data = helpData[addictionKey];
    if (!data) return;
    currentAddiction = addictionKey;
    document.getElementById('selectedAddiction').innerHTML = data.title;
    document.getElementById('helpContent').innerHTML = data.content;
    document.getElementById('extraResources').innerHTML = '';
  }

  // attach click events to cards
  const cards = document.querySelectorAll('.card');
  cards.forEach(card => {
    card.addEventListener('click', () => {
      const addiction = card.getAttribute('data-addiction');
      if (addiction) updateHelpPanel(addiction);
    });
  });

  // more resources button
  const moreBtn = document.getElementById('moreResourcesBtn');
  const extraDiv = document.getElementById('extraResources');
  moreBtn.addEventListener('click', () => {
    if (!currentAddiction) {
      extraDiv.innerHTML = '👆 Please select an addiction first to see relevant resources.';
      return;
    }
    const extraText = helpData[currentAddiction]?.extra || "Check online support groups or local harm reduction centers.";
    extraDiv.innerHTML = `<div style="background:#f3f0e6; padding:0.8rem; border-radius:1rem;">${extraText}</div>`;
  });

  // Daily coping tips array (JS-powered)
  const tips = [
    "You've survived 100% of your worst days. This one will pass too.",
    "Urges usually last 15-20 minutes. Try a 5-minute walk or cold water on your face.",
    "Shame grows in silence. Speaking to someone — even online — cuts its power.",
    "Progress isn't perfection. One sober hour is a victory.",
    "You are more than your addiction. Name three things you like about yourself right now.",
    "Deep breath in... hold... out. Do it again. Notice the shift.",
    "Your brain can heal. Neuroplasticity means new habits create new pathways."
  ];

  const tipElement = document.getElementById('dailyTip');
  function showRandomTip() {
    const randomIndex = Math.floor(Math.random() * tips.length);
    tipElement.textContent = tips[randomIndex];
  }
  showRandomTip();
  document.getElementById('newTipBtn').addEventListener('click', showRandomTip);

  // breathing circle animation
  const breathCircle = document.getElementById('breathCircle');
  let breathing = false;
  breathCircle.addEventListener('click', () => {
    if (breathing) return;
    breathing = true;
    breathCircle.classList.add('animate');
    breathCircle.textContent = 'inhale...';
    setTimeout(() => {
      breathCircle.classList.remove('animate');
      breathCircle.textContent = 'exhale...';
      setTimeout(() => {
        breathCircle.textContent = 'breathe';
        breathing = false;
      }, 4000);
    }, 4000);
  });

  // optional: default selection on load (alcohol support to feel less empty)
  updateHelpPanel('alcohol');
</script>
</body>
</html>
