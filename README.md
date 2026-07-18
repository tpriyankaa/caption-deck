<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Caption Deck</title>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,wght@0,600;0,700;1,600&family=Inter:wght@400;500;600&family=IBM+Plex+Mono:wght@500&display=swap" rel="stylesheet">
<style>
:root {
  --paper: #fbf7ef;
  --paper-dim: #f1ead9;
  --ink: #1c1b19;
  --ink-soft: #5b564c;
  --yellow: #f2c230;
  --pink: #e8527a;
  --teal: #2e8b7e;
  --font-display: "Fraunces", serif;
  --font-body: "Inter", system-ui, sans-serif;
  --font-mono: "IBM Plex Mono", monospace;
}
* { box-sizing: border-box; margin: 0; padding: 0; }
body {
  min-height: 100vh;
  background: #fbf7ef;
  background-image: radial-gradient(circle at 1px 1px, rgba(28,27,25,0.06) 1px, transparent 0);
  background-size: 22px 22px;
  font-family: "Inter", system-ui, sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 48px 20px 32px;
  color: #1c1b19;
}
.site-header {
  text-align: center;
  max-width: 520px;
  margin-bottom: 36px;
}
.eyebrow {
  display: inline-block;
  font-family: "IBM Plex Mono", monospace;
  font-size: 12px;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: #5b564c;
  background: #f1ead9;
  border: 1px solid rgba(28,27,25,0.12);
  border-radius: 999px;
  padding: 4px 12px;
  margin-bottom: 14px;
}
h1 {
  font-family: "Fraunces", serif;
  font-weight: 700;
  font-size: clamp(2.4rem, 6vw, 3.4rem);
  margin-bottom: 8px;
  letter-spacing: -0.01em;
}
.subhead { color: #5b564c; font-size: 1rem; }
.category-row {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 8px;
  max-width: 560px;
  margin-bottom: 40px;
}
.chip {
  font-family: "IBM Plex Mono", monospace;
  font-size: 13px;
  border: 1px solid rgba(28,27,25,0.18);
  background: #fbf7ef;
  color: #1c1b19;
  padding: 7px 14px;
  border-radius: 999px;
  cursor: pointer;
  transition: transform 0.15s ease, background 0.15s ease;
}
.chip:hover { transform: translateY(-1px); }
.chip.active { background: #1c1b19; color: #fbf7ef; border-color: #1c1b19; }
.card-stack {
  position: relative;
  width: min(92vw, 420px);
  margin-bottom: 28px;
}
.ghost-card {
  position: absolute;
  inset: 0;
  background: #f1ead9;
  border: 1px solid rgba(28,27,25,0.1);
  border-radius: 10px;
}
.ghost-card--back  { transform: rotate(4deg); }
.ghost-card--mid   { transform: rotate(-3deg); }
.card {
  position: relative;
  background: #fbf7ef;
  border: 1px solid rgba(28,27,25,0.16);
  border-radius: 10px;
  box-shadow: 0 14px 30px -18px rgba(28,27,25,0.45);
  padding: 34px 26px 20px;
  min-height: 260px;
  display: flex;
  flex-direction: column;
}
.card.flip { animation: flip-in 0.4s ease; }
@keyframes flip-in {
  0%   { transform: rotateX(90deg); opacity: 0; }
  100% { transform: rotateX(0deg);  opacity: 1; }
}
.card-tab {
  position: absolute;
  top: -14px; left: 24px;
  background: #f2c230;
  color: #1c1b19;
  font-family: "IBM Plex Mono", monospace;
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  padding: 5px 12px;
  border-radius: 5px;
  transform: rotate(-2deg);
  box-shadow: 0 3px 0 rgba(28,27,25,0.12);
}
.card-caption {
  font-family: "Fraunces", serif;
  font-style: italic;
  font-weight: 600;
  font-size: 1.35rem;
  line-height: 1.4;
  margin: 12px 0 20px;
  flex-grow: 1;
}
.card-hashtags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-bottom: 18px;
}
.hashtag {
  font-family: "IBM Plex Mono", monospace;
  font-size: 12px;
  color: #2e8b7e;
  background: rgba(46,139,126,0.1);
  border: 1px solid rgba(46,139,126,0.25);
  padding: 3px 9px;
  border-radius: 6px;
}
.card-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-top: 1px dashed rgba(28,27,25,0.2);
  padding-top: 14px;
}
.card-index {
  font-family: "IBM Plex Mono", monospace;
  font-size: 12px;
  color: #5b564c;
}
.copy-btn {
  font-family: "IBM Plex Mono", monospace;
  font-size: 13px;
  background: #1c1b19;
  color: #fbf7ef;
  border: none;
  border-radius: 6px;
  padding: 8px 14px;
  cursor: pointer;
  transition: background 0.15s ease, transform 0.15s ease;
}
.copy-btn:hover  { background: #e8527a; }
.copy-btn:active { transform: scale(0.96); }
.pull-btn {
  font-family: "Inter", system-ui, sans-serif;
  font-weight: 600;
  font-size: 15px;
  background: #e8527a;
  color: #fbf7ef;
  border: none;
  padding: 13px 26px;
  border-radius: 999px;
  cursor: pointer;
  box-shadow: 0 10px 20px -10px rgba(232,82,122,0.6);
  transition: transform 0.15s ease, box-shadow 0.15s ease;
}
.pull-btn:hover  { transform: translateY(-2px); box-shadow: 0 14px 24px -10px rgba(232,82,122,0.7); }
.pull-btn:active { transform: translateY(0); }
.toast {
  margin-top: 14px;
  min-height: 18px;
  font-family: "IBM Plex Mono", monospace;
  font-size: 12px;
  color: #2e8b7e;
  opacity: 0;
  transition: opacity 0.25s ease;
}
.toast.show { opacity: 1; }
.site-footer {
  margin-top: 44px;
  text-align: center;
  font-size: 13px;
  color: #5b564c;
  max-width: 420px;
}
.site-footer code {
  font-family: "IBM Plex Mono", monospace;
  background: #f1ead9;
  padding: 2px 6px;
  border-radius: 4px;
}
@media (max-width: 480px) {
  .card { padding: 28px 18px 16px; }
  .card-caption { font-size: 1.15rem; }
}
</style>
</head>
<body>

<header class="site-header">
  <span class="eyebrow">pick a vibe, pull a card</span>
  <h1>Caption Deck</h1>
  <p class="subhead">A little box of captions for whatever you're posting.</p>
</header>

<main>
  <div class="category-row" id="categoryRow"></div>

  <div class="card-stack">
    <div class="ghost-card ghost-card--back"></div>
    <div class="ghost-card ghost-card--mid"></div>
    <section class="card" id="card">
      <div class="card-tab" id="cardTab">general</div>
      <p class="card-caption" id="captionText">Press "Pull a card" to get your first caption.</p>
      <div class="card-hashtags" id="hashtagRow"></div>
      <div class="card-footer">
        <span class="card-index" id="cardIndex">card —</span>
        <button class="copy-btn" id="copyBtn" type="button">Copy</button>
      </div>
    </section>
  </div>

  <button class="pull-btn" id="pullBtn" type="button">Pull a card →</button>
  <p class="toast" id="toast"></p>
</main>

<footer class="site-footer">
  <p>Beginner-friendly project. Add your own captions inside <code>CAPTION_DATA</code> in the script.</p>
</footer>

<script>
const CAPTION_DATA = {
  general: {
    label: "General",
    hashtags: ["#goodvibes", "#todayswin", "#justpost", "#momentmade"],
    captions: [
      "Not perfect, just posted.",
      "This is your sign to hit share.",
      "Small moment, main character energy.",
      "Living for the little things.",
      "Filed under: worth remembering.",
    ],
  },
  travel: {
    label: "Travel",
    hashtags: ["#wanderlust", "#passportstamps", "#newplace", "#roadtrip", "#exploremore"],
    captions: [
      "Left my routine at the gate.",
      "Somewhere new, same old me — slightly sunburnt.",
      "Collecting places, not things.",
      "Map says one thing, my feet say another.",
      "Currently allergic to my own timezone.",
    ],
  },
  food: {
    label: "Food",
    hashtags: ["#foodie", "#homecooked", "#eatwell", "#tastetest", "#kitchenwin"],
    captions: [
      "Ate this before it could get cold. No regrets.",
      "Recipe: follow instructions, then improvise wildly.",
      "10/10, would eat again immediately.",
      "Cooking is just chemistry you get to eat.",
      "This plate is doing a lot of emotional labor today.",
    ],
  },
  selfie: {
    label: "Selfie",
    hashtags: ["#justme", "#nofilter", "#selfcare", "#feelinggood", "#ootd"],
    captions: [
      "New angle, same chaos.",
      "Confidence: rented, not owned. Wearing it anyway.",
      "Proof I left the house today.",
      "Lighting was good so I had to.",
      "One (1) picture that doesn't look weird. Posting immediately.",
    ],
  },
  motivational: {
    label: "Motivational",
    hashtags: ["#keepgoing", "#growth", "#mindset", "#showup", "#progress"],
    captions: [
      "Small steps still count as moving.",
      "Doing it scared beats not doing it at all.",
      "Progress, not perfection — framed and hung on the wall.",
      "The version of you a year ago would be proud.",
      "Bet on yourself. The odds are better than you think.",
    ],
  },
  funny: {
    label: "Funny",
    hashtags: ["#lol", "#relatable", "#send", "#itwasajoke"],
    captions: [
      "Personality: 90% snacks, 10% overthinking.",
      "I peaked at this exact moment.",
      "Running on caffeine and spite today.",
      "This post has no plot, just vibes.",
      "Emotionally I am a golden retriever that saw a squirrel.",
    ],
  },
  pets: {
    label: "Pets",
    hashtags: ["#petsofinstagram", "#goodboy", "#catsofinstagram", "#furbaby"],
    captions: [
      "My tiny roommate pays rent in chaos and love.",
      "Officially owned by this creature now.",
      "Zero productivity, infinite cuteness.",
      "Best decision I never regret making.",
      "This one's the real main character of the house.",
    ],
  },
  fitness: {
    label: "Fitness",
    hashtags: ["#fitnessjourney", "#trainhard", "#nodaysoff", "#pr"],
    captions: [
      "Showed up when the couch made a better offer.",
      "New personal record, old amount of soreness.",
      "One more rep than yesterday. That's the whole plan.",
      "Sweat now, brag later.",
      "Consistency over intensity, every single time.",
    ],
  },
};

let currentCategory = "general";
let lastIndex = -1;

const categoryRow  = document.getElementById("categoryRow");
const card         = document.getElementById("card");
const cardTab      = document.getElementById("cardTab");
const captionText  = document.getElementById("captionText");
const hashtagRow   = document.getElementById("hashtagRow");
const cardIndex    = document.getElementById("cardIndex");
const pullBtn      = document.getElementById("pullBtn");
const copyBtn      = document.getElementById("copyBtn");
const toast        = document.getElementById("toast");

function renderChips() {
  Object.keys(CAPTION_DATA).forEach(key => {
    const btn = document.createElement("button");
    btn.type = "button";
    btn.className = "chip" + (key === currentCategory ? " active" : "");
    btn.textContent = CAPTION_DATA[key].label;
    btn.dataset.category = key;
    btn.addEventListener("click", () => {
      currentCategory = key;
      lastIndex = -1;
      document.querySelectorAll(".chip").forEach(c =>
        c.classList.toggle("active", c.dataset.category === key)
      );
      pullCard();
    });
    categoryRow.appendChild(btn);
  });
}

function pullCard() {
  const data = CAPTION_DATA[currentCategory];
  let i;
  do { i = Math.floor(Math.random() * data.captions.length); }
  while (i === lastIndex && data.captions.length > 1);
  lastIndex = i;

  cardTab.textContent = data.label.toLowerCase();
  captionText.textContent = data.captions[i];
  cardIndex.textContent = `card ${i + 1} of ${data.captions.length}`;

  hashtagRow.innerHTML = "";
  [...data.hashtags].sort(() => Math.random() - 0.5).slice(0, 3).forEach(tag => {
    const s = document.createElement("span");
    s.className = "hashtag";
    s.textContent = tag;
    hashtagRow.appendChild(s);
  });

  card.classList.remove("flip");
  void card.offsetWidth;
  card.classList.add("flip");
  hideToast();
}

async function copyCard() {
  const tags = Array.from(hashtagRow.children).map(e => e.textContent).join(" ");
  try {
    await navigator.clipboard.writeText(captionText.textContent + "\n\n" + tags);
    showToast("Copied to clipboard ✓");
  } catch {
    showToast("Select the text and copy manually.");
  }
}

function showToast(msg) {
  toast.textContent = msg;
  toast.classList.add("show");
  clearTimeout(showToast._t);
  showToast._t = setTimeout(hideToast, 2200);
}
function hideToast() { toast.classList.remove("show"); }

pullBtn.addEventListener("click", pullCard);
copyBtn.addEventListener("click", copyCard);
renderChips();
</script>
</body>
</html># caption-deck
