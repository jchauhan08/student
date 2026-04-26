---
layout: post
author: Jaynee Chauhan 
permalink: /matching
---
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Memory Match — APCSP CPT</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800&family=Syne+Mono&display=swap" rel="stylesheet"/>
<style>
  /* ── CSS Variables ── */
  :root {
    --bg:       #0b0c10;
    --surface:  #13141a;
    --card-bg:  #1c1e28;
    --card-face:#1c1e28;
    --accent:   #00f5c4;
    --accent2:  #ff4d6d;
    --gold:     #ffd166;
    --text:     #e8eaf0;
    --muted:    #5a5f72;
    --radius:   14px;
    --shadow:   0 8px 32px rgba(0,0,0,0.5);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Syne', sans-serif;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 28px 16px 48px;
    background-image:
      radial-gradient(ellipse 60% 40% at 70% 10%, rgba(0,245,196,0.07) 0%, transparent 70%),
      radial-gradient(ellipse 50% 35% at 20% 90%, rgba(255,77,109,0.06) 0%, transparent 70%);
  }

  /* ── Header ── */
  header {
    text-align: center;
    margin-bottom: 28px;
  }
  header h1 {
    font-size: clamp(1.8rem, 5vw, 3rem);
    font-weight: 800;
    letter-spacing: -1px;
    line-height: 1;
  }
  header h1 span { color: var(--accent); }
  header p {
    font-family: 'Syne Mono', monospace;
    font-size: 0.75rem;
    color: var(--muted);
    margin-top: 6px;
    letter-spacing: 2px;
    text-transform: uppercase;
  }

  /* ── Stats Bar ── */
  .stats {
    display: flex;
    gap: 20px;
    margin-bottom: 24px;
    flex-wrap: wrap;
    justify-content: center;
  }
  .stat-box {
    background: var(--surface);
    border: 1px solid rgba(255,255,255,0.06);
    border-radius: var(--radius);
    padding: 10px 22px;
    text-align: center;
    min-width: 90px;
  }
  .stat-label {
    font-family: 'Syne Mono', monospace;
    font-size: 0.6rem;
    color: var(--muted);
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 3px;
  }
  .stat-value {
    font-size: 1.5rem;
    font-weight: 700;
    color: var(--accent);
  }
  #timer-val { color: var(--gold); }
  #streak-val { color: var(--accent2); }

  /* ── Difficulty Selector ── */
  .controls {
    display: flex;
    gap: 10px;
    margin-bottom: 28px;
    flex-wrap: wrap;
    justify-content: center;
  }
  .ctrl-btn {
    font-family: 'Syne', sans-serif;
    font-size: 0.8rem;
    font-weight: 700;
    letter-spacing: 1px;
    text-transform: uppercase;
    padding: 8px 20px;
    border-radius: 999px;
    border: 1.5px solid var(--muted);
    background: transparent;
    color: var(--muted);
    cursor: pointer;
    transition: all 0.2s;
  }
  .ctrl-btn:hover, .ctrl-btn.active {
    border-color: var(--accent);
    color: var(--accent);
    background: rgba(0,245,196,0.07);
  }
  #restart-btn {
    border-color: var(--accent2);
    color: var(--accent2);
  }
  #restart-btn:hover {
    background: rgba(255,77,109,0.1);
  }

  /* ── Game Board ── */
  #board {
    display: grid;
    gap: 14px;
    width: 100%;
    max-width: 680px;
    justify-items: center;
  }

  /* ── Card ── */
  .card {
    width: 100%;
    aspect-ratio: 1;
    perspective: 900px;
    cursor: pointer;
  }
  .card-inner {
    width: 100%; height: 100%;
    position: relative;
    transform-style: preserve-3d;
    transition: transform 0.45s cubic-bezier(0.4, 0, 0.2, 1);
    border-radius: var(--radius);
  }
  .card.flipped .card-inner  { transform: rotateY(180deg); }
  .card.matched .card-inner  { transform: rotateY(180deg); }

  .card-front, .card-back {
    position: absolute; inset: 0;
    border-radius: var(--radius);
    backface-visibility: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: clamp(1.4rem, 4vw, 2.2rem);
    border: 1.5px solid rgba(255,255,255,0.07);
  }
  /* Back = hidden face */
  .card-back {
    background: var(--card-bg);
    color: var(--muted);
    font-size: clamp(1rem, 3vw, 1.6rem);
  }
  .card-back::after {
    content: '?';
    font-weight: 800;
    font-family: 'Syne', sans-serif;
    color: var(--muted);
    font-size: clamp(1.2rem, 4vw, 2rem);
  }
  /* Front = emoji face */
  .card-front {
    background: var(--card-face);
    transform: rotateY(180deg);
    border-color: rgba(255,255,255,0.12);
    box-shadow: var(--shadow);
  }
  .card.matched .card-front {
    border-color: var(--accent);
    box-shadow: 0 0 18px rgba(0,245,196,0.35);
    background: #111a18;
  }
  .card.wrong .card-front {
    border-color: var(--accent2);
    box-shadow: 0 0 14px rgba(255,77,109,0.35);
  }
  .card:hover:not(.flipped):not(.matched) .card-back {
    border-color: rgba(0,245,196,0.3);
    background: #202230;
  }

  /* ── Win Overlay ── */
  #win-overlay {
    display: none;
    position: fixed; inset: 0;
    background: rgba(11,12,16,0.92);
    backdrop-filter: blur(8px);
    z-index: 100;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    gap: 18px;
    text-align: center;
    padding: 24px;
  }
  #win-overlay.show { display: flex; animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity:0; transform:scale(0.95); } to { opacity:1; transform:scale(1); } }
  #win-overlay h2 { font-size: clamp(2rem, 8vw, 4rem); font-weight: 800; color: var(--accent); }
  #win-overlay p  { color: var(--text); font-size: 1.1rem; line-height: 1.7; }
  #win-overlay .score-summary {
    background: var(--surface);
    border: 1px solid rgba(0,245,196,0.2);
    border-radius: var(--radius);
    padding: 18px 36px;
    font-family: 'Syne Mono', monospace;
    font-size: 0.9rem;
    color: var(--accent);
    line-height: 2;
  }
  #play-again {
    background: var(--accent);
    color: #000;
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 1rem;
    letter-spacing: 1px;
    padding: 14px 40px;
    border-radius: 999px;
    border: none;
    cursor: pointer;
    transition: transform 0.15s, box-shadow 0.15s;
    margin-top: 8px;
  }
  #play-again:hover { transform: scale(1.04); box-shadow: 0 0 24px rgba(0,245,196,0.4); }

  /* ── CPT Info Panel ── */
  .cpt-panel {
    margin-top: 40px;
    max-width: 680px;
    width: 100%;
    background: var(--surface);
    border: 1px solid rgba(255,255,255,0.06);
    border-radius: var(--radius);
    padding: 24px 28px;
  }
  .cpt-panel h3 {
    font-size: 0.7rem;
    letter-spacing: 3px;
    text-transform: uppercase;
    font-family: 'Syne Mono', monospace;
    color: var(--muted);
    margin-bottom: 16px;
  }
  .cpt-row {
    display: flex;
    gap: 12px;
    margin-bottom: 10px;
    align-items: flex-start;
    font-size: 0.875rem;
    line-height: 1.6;
  }
  .cpt-tag {
    flex-shrink: 0;
    background: rgba(0,245,196,0.12);
    color: var(--accent);
    font-family: 'Syne Mono', monospace;
    font-size: 0.65rem;
    padding: 2px 8px;
    border-radius: 4px;
    margin-top: 2px;
    letter-spacing: 1px;
  }
  .cpt-row span { color: var(--text); }
  .cpt-row span b { color: var(--gold); }
</style>
</head>
<body>

<header>
  <h1>Memory <span>Match</span></h1>
  <p>APCSP Create Performance Task</p>
</header>

<!-- Stats -->
<div class="stats">
  <div class="stat-box"><div class="stat-label">Moves</div><div class="stat-value" id="moves-val">0</div></div>
  <div class="stat-box"><div class="stat-label">Matches</div><div class="stat-value" id="matches-val">0</div></div>
  <div class="stat-box"><div class="stat-label">Time</div><div class="stat-value" id="timer-val">0s</div></div>
  <div class="stat-box"><div class="stat-label">Streak</div><div class="stat-value" id="streak-val">0</div></div>
</div>

<!-- Controls -->
<div class="controls">
  <button class="ctrl-btn active" data-pairs="6">Easy (4×3)</button>
  <button class="ctrl-btn" data-pairs="8">Medium (4×4)</button>
  <button class="ctrl-btn" data-pairs="10">Hard (5×4)</button>
  <button class="ctrl-btn" id="restart-btn">↺ Restart</button>
</div>

<!-- Game Board -->
<div id="board"></div>

<!-- Win Overlay -->
<div id="win-overlay">
  <h2>🎉 You Win!</h2>
  <p>All pairs matched. Here's your score:</p>
  <div class="score-summary" id="win-summary"></div>
  <button id="play-again">Play Again</button>
</div>

<!-- CPT Info Panel -->
<div class="cpt-panel">
  <h3>CPT Rubric Requirements — Satisfied by this program</h3>
  <div class="cpt-row"><span class="cpt-tag">LIST</span><span><b>cardDeck[]</b> — a list of card objects. Each object stores the emoji, index, matched state, and flipped state. The list manages all card data and is iterated to render and evaluate the board.</span></div>
  <div class="cpt-row"><span class="cpt-tag">PROCEDURE</span><span><b>flipCard(index)</b> — a defined function with a parameter (<b>index</b>) that selects which card to flip. The parameter directly affects which element of the list is updated and what output occurs.</span></div>
  <div class="cpt-row"><span class="cpt-tag">ALGORITHM</span><span>Contains <b>sequencing</b> (flip → store → compare), <b>selection</b> (if 2 cards flipped: check match or mismatch), and <b>iteration</b> (loop over cardDeck to check win condition).</span></div>
  <div class="cpt-row"><span class="cpt-tag">INPUT</span><span>User clicks a card → triggers <b>flipCard(index)</b> with the card's position as input.</span></div>
  <div class="cpt-row"><span class="cpt-tag">OUTPUT</span><span>Board renders card state; stats update (moves, matches, streak, timer); win screen displays final score on completion.</span></div>
</div>

<script>
  // ══════════════════════════════════════════════════════
  //  APCSP CPT — Memory Match
  //  All CPT requirements are clearly labeled in comments
  // ══════════════════════════════════════════════════════

  // ── LIST: cardDeck stores all card objects ──
  // This list manages the complexity of the program.
  // Each element is an object with emoji, matched, and flipped state.
  let cardDeck = [];   // <-- THE LIST

  // ── Other state variables ──
  let flippedIndices = [];  // tracks the (up to) 2 currently flipped cards
  let moves    = 0;
  let matches  = 0;
  let streak   = 0;
  let totalPairs = 6;
  let timerInterval = null;
  let seconds  = 0;
  let locked   = false;  // prevents clicking while evaluating a pair

  // Emoji pool
  const EMOJI_POOL = [
    '🐉','🦄','🌋','🪐','🦋','🎯','🧩','🪄',
    '🎸','🦊','🌊','🔮','🍄','🎭','🚀','⚡',
    '🌈','🐙','🦁','🎲'
  ];

  // ── shuffleArray: Fisher-Yates shuffle algorithm ──
  function shuffleArray(arr) {
    for (let i = arr.length - 1; i > 0; i--) {      // ITERATION
      const j = Math.floor(Math.random() * (i + 1));
      [arr[i], arr[j]] = [arr[j], arr[i]];
    }
    return arr;
  }

  // ── initGame: sets up cardDeck (the list) ──
  function initGame() {
    clearInterval(timerInterval);
    seconds = 0; moves = 0; matches = 0; streak = 0;
    flippedIndices = []; locked = false;
    updateStats();

    // Build the list: pick emojis, duplicate for pairs, shuffle
    const chosen = shuffleArray([...EMOJI_POOL]).slice(0, totalPairs);
    const pairs  = shuffleArray([...chosen, ...chosen]);

    // ITERATION: populate cardDeck list with card objects
    cardDeck = [];
    for (let i = 0; i < pairs.length; i++) {
      cardDeck.push({ emoji: pairs[i], matched: false, flipped: false, id: i });
    }

    renderBoard();
    startTimer();
    document.getElementById('win-overlay').classList.remove('show');
  }

  // ── renderBoard: uses the list to create the UI ──
  function renderBoard() {
    const board = document.getElementById('board');
    board.innerHTML = '';

    // Set grid columns based on difficulty
    const cols = totalPairs === 10 ? 5 : 4;
    board.style.gridTemplateColumns = `repeat(${cols}, 1fr)`;

    // ITERATION over cardDeck list to render each card
    for (let i = 0; i < cardDeck.length; i++) {
      const card = cardDeck[i];
      const el   = document.createElement('div');
      el.className = 'card' + (card.matched ? ' matched' : '') + (card.flipped ? ' flipped' : '');
      el.innerHTML = `
        <div class="card-inner">
          <div class="card-back"></div>
          <div class="card-front">${card.emoji}</div>
        </div>`;
      // INPUT: user click passes index to flipCard
      el.addEventListener('click', () => flipCard(i));
      board.appendChild(el);
    }
  }

  // ══════════════════════════════════════════════════════
  //  PROCEDURE: flipCard(index)
  //  Parameter: index — which card in the list to flip
  //  The parameter directly affects program behavior:
  //    - selects which cardDeck element to update
  //    - determines which card is compared for a match
  // ══════════════════════════════════════════════════════
  function flipCard(index) {
    // SELECTION: guard conditions
    if (locked) return;
    if (cardDeck[index].matched) return;
    if (cardDeck[index].flipped) return;
    if (flippedIndices.length === 2) return;

    // SEQUENCING step 1: flip the card in the list
    cardDeck[index].flipped = true;
    flippedIndices.push(index);
    renderBoard();

    // SEQUENCING step 2: if 2 cards are flipped, evaluate
    if (flippedIndices.length === 2) {
      moves++;
      updateStats();
      locked = true;

      const [a, b] = flippedIndices;

      // SELECTION: check if the two cards are a match
      if (cardDeck[a].emoji === cardDeck[b].emoji) {
        // ── Match! ──
        cardDeck[a].matched = true;
        cardDeck[b].matched = true;
        matches++;
        streak++;
        flippedIndices = [];
        locked = false;
        renderBoard();
        updateStats();
        checkWin();   // ITERATION inside checkWin
      } else {
        // ── No match: flip back after delay ──
        streak = 0;
        updateStats();
        setTimeout(() => {
          cardDeck[a].flipped = false;
          cardDeck[b].flipped = false;
          flippedIndices = [];
          locked = false;
          renderBoard();
        }, 900);
      }
    }
  }

  // ── checkWin: ITERATION over list to see if all matched ──
  function checkWin() {
    let allMatched = true;
    for (let i = 0; i < cardDeck.length; i++) {   // ITERATION
      if (!cardDeck[i].matched) { allMatched = false; break; } // SELECTION
    }
    if (allMatched) {
      clearInterval(timerInterval);
      // OUTPUT: display win screen with final stats
      document.getElementById('win-summary').innerHTML =
        `Moves: ${moves}<br>Time: ${seconds}s<br>Pairs: ${totalPairs}<br>Score: ${calcScore()}`;
      document.getElementById('win-overlay').classList.add('show');
    }
  }

  // ── calcScore: simple scoring formula ──
  function calcScore() {
    const base   = totalPairs * 100;
    const timePenalty  = seconds * 2;
    const movePenalty  = Math.max(0, moves - totalPairs) * 5;
    return Math.max(0, base - timePenalty - movePenalty);
  }

  // ── Timer ──
  function startTimer() {
    timerInterval = setInterval(() => {
      seconds++;
      document.getElementById('timer-val').textContent = seconds + 's';
    }, 1000);
  }

  // ── updateStats: OUTPUT to the UI ──
  function updateStats() {
    document.getElementById('moves-val').textContent   = moves;
    document.getElementById('matches-val').textContent = matches;
    document.getElementById('streak-val').textContent  = streak;
  }

  // ── Controls ──
  document.querySelectorAll('[data-pairs]').forEach(btn => {
    btn.addEventListener('click', () => {
      document.querySelectorAll('[data-pairs]').forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
      totalPairs = parseInt(btn.dataset.pairs);
      initGame();
    });
  });
  document.getElementById('restart-btn').addEventListener('click', initGame);
  document.getElementById('play-again').addEventListener('click', initGame);

  // ── Start ──
  initGame();
</script>
</body>
</html>