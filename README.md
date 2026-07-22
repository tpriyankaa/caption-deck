<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Caption Deck</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;1,600&family=DM+Sans:wght@400;500;600&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root {
  --cream: #f5efe6;
  --cream-dark: #ede0cf;
  --brown-light: #c4a882;
  --brown: #8b6343;
  --brown-dark: #5c3d1e;
  --rust: #b85c38;
  --rust-light: #d4734a;
  --sage: #7a8c6e;
  --sage-light: #a3b899;
  --ink: #2c1810;
  --ink-soft: #6b4c35;
}
* { box-sizing: border-box; margin: 0; padding: 0; }
body {
  min-height: 100vh;
  background: var(--cream);
  background-image:
    radial-gradient(ellipse at top left, rgba(196,168,130,0.3) 0%, transparent 50%),
    radial-gradient(ellipse at bottom right, rgba(184,92,56,0.15) 0%, transparent 50%);
  font-family: "DM Sans", system-ui, sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 52px 20px 40px;
  color: var(--ink);
}
/* ---------- Header ---------- */
.site-header {
  text-align: center;
  max-width: 560px;
  margin-bottom: 40px;
}
.eyebrow {
  display: inline-block;
  font-family: "DM Mono", monospace;
  font-size: 11px;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--ink-soft);
  background: var(--cream-dark);
  border: 1px solid var(--brown-light);
  border-radius: 999px;
  padding: 5px 14px;
  margin-bottom: 16px;
}
h1 {
  font-family: "Playfair Display", serif;
  font-weight: 700;
  font-size: clamp(2.8rem, 7vw, 4rem);
  margin-bottom: 10px;
  letter-spacing: -0.02em;
  color: var(--brown-dark);
  line-height: 1.1;
}
.subhead {
  color: var(--ink-soft);
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.6;
}
/* ---------- Divider ---------- */
.divider {
  width: 60px;
  height: 2px;
  background: linear-gradient(90deg, var(--rust), var(--brown-light));
  border-radius: 999px;
  margin: 18px auto 0;
}
/* ---------- Category chips ---------- */
.category-row {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 8px;
  max-width: 580px;
  margin-bottom: 44px;
}
.chip {
  font-family: "DM Mono", monospace;
  font-size: 12px;
  letter-spacing: 0.04em;
  border: 1.5px solid var(--brown-light);
  background: transparent;
  color: var(--brown);
  padding: 7px 16px;
  border-radius: 999px;
  cursor: pointer;
  transition: all 0.2s ease;
}
.chip:hover {
  background: var(--cream-dark);
  border-color: var(--brown);
  color: var(--brown-dark);
  transform: translateY(-1px);
}
.chip.active {
  background: var(--brown-dark);
  color: var(--cream);
  border-color: var(--brown-dark);
  box-shadow: 0 4px 12px rgba(92,61,30,0.25);
}
/* ---------- Card stack ---------- */
.card-stack {
  position: relative;
  width: min(92vw, 440px);
  margin-bottom: 32px;
}
.ghost-card {
  position: absolute;
  inset: 0;
  background: var(--cream-dark);
  border: 1.5px solid var(--brown-light);
  border-radius: 16px;
}
.ghost-card--back  { transform: rotate(4deg);  opacity: 0.6; }
.ghost-card--mid   { transform: rotate(-3deg); opacity: 0.8; }
.card {
  position: relative;
  background: var(--cream);
  border: 1.5px solid var(--brown-light);
  border-radius: 16px;
  box-shadow:
    0 2px 0 var(--brown-light),
    0 8px 32px -8px rgba(92,61,30,0.2),
    0 24px 48px -16px rgba(92,61,30,0.15);
  padding: 38px 30px 24px;
  min-height: 280px;
  display: flex;
  flex-direction: column;
}
.card.flip { animation: flip-in 0.45s cubic-bezier(0.23,1,0.32,1); }
@keyframes flip-in {
  0%   { transform: rotateX(80deg) scale(0.95); opacity: 0; }
  100% { transform: rotateX(0deg)  scale(1);    opacity: 1; }
}
.card-tab {
  position: absolute;
  top: -15px; left: 28px;
  background: linear-gradient(135deg, var(--rust), var(--rust-light));
  color: var(--cream);
  font-family: "DM Mono", monospace;
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  padding: 6px 14px;
  border-radius: 6px;
  transform: rotate(-1.5deg);
  box-shadow: 0 4px 8px rgba(184,92,56,0.3);
}
.card-label {
  font-family: "DM Mono", monospace;
  font-size: 11px;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--brown-light);
  margin-bottom: 14px;
}
.card-caption {
  font-family: "Playfair Display", serif;
  font-style: italic;
  font-weight: 600;
  font-size: 1.4rem;
  line-height: 1.5;
  margin-bottom: 24px;
  flex-grow: 1;
  color: var(--brown-dark);
}
.card-hashtags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-bottom: 20px;
}
.hashtag {
  font-family: "DM Mono", monospace;
  font-size: 11px;
  letter-spacing: 0.03em;
  color: var(--sage);
  background: rgba(122,140,110,0.1);
  border: 1px solid rgba(122,140,110,0.3);
  padding: 4px 10px;
  border-radius: 6px;
}
.card-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-top: 1px solid var(--cream-dark);
  padding-top: 16px;
}
.card-index {
  font-family: "DM Mono", monospace;
  font-size: 11px;
  color: var(--brown-light);
  letter-spacing: 0.05em;
}
.copy-btn {
  font-family: "DM Sans", sans-serif;
  font-size: 13px;
  font-weight: 600;
  background: var(--cream-dark);
  color: var(--brown-dark);
  border: 1.5px solid var(--brown-light);
  border-radius: 8px;
  padding: 8px 16px;
  cursor: pointer;
  transition: all 0.2s ease;
  letter-spacing: 0.02em;
}
.copy-btn:hover {
  background: var(--brown-dark);
  color: var(--cream);
  border-color: var(--brown-dark);
}
.copy-btn:active { transform: scale(0.97); }
/* ---------- Pull button ---------- */
.pull-btn {
  font-family: "DM Sans", sans-serif;
  font-weight: 600;
  font-size: 15px;
  background: linear-gradient(135deg, var(--rust), var(--rust-light));
  color: var(--cream);
  border: none;
  padding: 15px 32px;
  border-radius: 999px;
  cursor: pointer;
  box-shadow:
    0 2px 0 rgba(92,61,30,0.3),
    0 8px 24px -8px rgba(184,92,56,0.5);
  transition: all 0.2s ease;
  letter-spacing: 0.02em;
}
.pull-btn:hover {
  transform: translateY(-2px);
  box-shadow:
    0 4px 0 rgba(92,61,30,0.2),
    0 12px 28px -8px rgba(184,92,56,0.6);
}
.pull-btn:active { transform: translateY(0); }
/* ---------- Toast ---------- */
.toast {
  margin-top: 16px;
  min-height: 20px;
  font-family: "DM Mono", monospace;
  font-size: 12px;
  color: var(--sage);
  letter-spacing: 0.04em;
  opacity: 0;
  transition: opacity 0.25s ease;
}
.toast.show { opacity: 1; }
/* ---------- Footer ---------- */
.site-footer {
  margin-top: 52px;
  text-align: center;
  font-size: 13px;
  color: var(--brown-light);
  max-width: 440px;
  line-height: 1.6;
}
.site-footer code {
  font-family: "DM Mono", monospace;
  background: var(--cream-dark);
  color: var(--brown);
  padding: 2px 7px;
  border-radius: 4px;
  font-size: 12px;
}
/* ---------- Focus ---------- */
.chip:focus-visible,
.copy-btn:focus-visible,
.pull-btn:focus-visible {
  outline: 2px solid var(--rust);
  outline-offset: 3px;
}
/* ---------- Mobile ---------- */
@media (max-width: 480px) {
  .card { padding: 30px 20px 18px; }
  .card-caption { font-size: 1.2rem; }
  h1 { font-size: 2.4rem; }
}
</style>
</head>
<body>

<header class="site-header">
  <span class="eyebrow">✦ pick a vibe, pull a card ✦</span>
  <h1>Caption Deck</h1>
  <p class="subhead">A little box of captions for whatever you're posting.</p>
  <div class="divider"></div>
</header>

<main>
  <div class="category-row" id="categoryRow"></div>

  <div class="card-stack">
    <div class="ghost-card ghost-card--back"></div>
    <div class="ghost-card ghost-card--mid"></div>
    <section class="card" id="card">
      <div class="card-tab" id="cardTab">general</div>
      <p class="card-label">today's caption</p>
      <p class="card-caption" id="captionText">Press "Pull a card" to get your first caption.</p>
      <div class="card-hashtags" id="hashtagRow"></div>
      <div class="card-footer">
        <span class="card-index" id="cardIndex">card —</span>
        <button class="copy-btn" id="copyBtn" type="button">Copy ✦</button>
      </div>
    </section>
  </div>

  <button class="pull-btn" id="pullBtn" type="button">Pull a card →</button>
  <p class="toast" id="toast"></p>
</main>

<footer class="site-footer">
  <p>A beginner-friendly project. Add your own captions inside <code>CAPTION_DATA</code>.</p>
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
    hashtags: ["#wanderlust", "#passportstamps", "#newplace", "#roadtrip"],
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
    hashtags: ["#foodie", "#homecooked", "#eatwell", "#kitchenwin"],
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
    hashtags: ["#justme", "#nofilter", "#selfcare", "#ootd"],
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
    hashtags: ["#keepgoing", "#growth", "#mindset", "#progress"],
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

const categoryRow = document.getElementById("categoryRow");
const card        = document.getElementById("card");
const cardTab     = document.getElementById("cardTab");
const captionText = document.getElementById("captionText");
const hashtagRow  = document.getElementById("hashtagRow");
const cardIndex   = document.getElementById("cardIndex");
const pullBtn     = document.getElementById("pullBtn");
const copyBtn     = document.getElementById("copyBtn");
const toast       = document.getElementById("toast");

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
    showToast("✦ copied to clipboard");
  } catch {
    showToast("select the text and copy manually.");
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
</html>

## 🛠️ Built With

![HTML](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)

---

## 👩‍💻 Author

Made with ❤️ by **Priyanka** — [@tpriyankaa](https://github.com/tpriyankaa)
