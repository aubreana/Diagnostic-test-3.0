<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Travel English Quest - Diagnostic Test v2.0</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;500;600;700&family=Nunito:wght@400;500;600;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg: #FEF9F3;
      --fg: #1A3A3A;
      --muted: #6B8A8A;
      --accent: #FF6B35;
      --accent-light: #FF8C5A;
      --card: #FFFFFF;
      --border: #E8DDD4;
      --primary: #0D7377;
      --primary-light: #14919B;
      --success: #2ECC71;
      --error: #E74C3C;
      --warning: #F39C12;
      --purple: #9B59B6;
    }

    * { box-sizing: border-box; }

    body {
      font-family: 'Nunito', sans-serif;
      background: var(--bg);
      color: var(--fg);
      min-height: 100vh;
      overflow-x: hidden;
    }

    h1, h2, h3, .display-font { font-family: 'Fredoka', sans-serif; }

    .bg-pattern {
      position: fixed;
      inset: 0;
      z-index: -1;
      background: 
        radial-gradient(ellipse at 20% 20%, rgba(13, 115, 119, 0.08) 0%, transparent 50%),
        radial-gradient(ellipse at 80% 80%, rgba(255, 107, 53, 0.08) 0%, transparent 50%),
        radial-gradient(ellipse at 50% 50%, rgba(20, 145, 155, 0.05) 0%, transparent 70%);
    }

    .floating-shapes {
      position: fixed;
      inset: 0;
      z-index: -1;
      pointer-events: none;
      overflow: hidden;
    }

    .shape {
      position: absolute;
      border-radius: 50%;
      opacity: 0.12;
      animation: float 20s ease-in-out infinite;
    }

    .shape:nth-child(1) { width: 300px; height: 300px; background: var(--primary); top: -100px; right: -100px; }
    .shape:nth-child(2) { width: 200px; height: 200px; background: var(--accent); bottom: 10%; left: -50px; animation-delay: -5s; }
    .shape:nth-child(3) { width: 150px; height: 150px; background: var(--primary-light); top: 40%; right: 5%; animation-delay: -10s; }

    @keyframes float {
      0%, 100% { transform: translate(0, 0) rotate(0deg); }
      25% { transform: translate(20px, -20px) rotate(5deg); }
      50% { transform: translate(-10px, 20px) rotate(-5deg); }
      75% { transform: translate(15px, 10px) rotate(3deg); }
    }

    .screen { display: none; animation: fadeSlideIn 0.5s ease-out; }
    .screen.active { display: block; }

    @keyframes fadeSlideIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .btn-primary {
      background: linear-gradient(135deg, var(--primary) 0%, var(--primary-light) 100%);
      color: white;
      padding: 14px 32px;
      border-radius: 50px;
      font-weight: 600;
      font-size: 1.1rem;
      border: none;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 4px 15px rgba(13, 115, 119, 0.3);
    }

    .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 6px 25px rgba(13, 115, 119, 0.4); }
    .btn-primary:active { transform: translateY(0); }
    .btn-primary:disabled { opacity: 0.5; cursor: not-allowed; transform: none; }

    .btn-secondary {
      background: var(--card);
      color: var(--primary);
      padding: 12px 28px;
      border-radius: 50px;
      font-weight: 600;
      border: 2px solid var(--primary);
      cursor: pointer;
      transition: all 0.3s ease;
    }

    .btn-secondary:hover { background: var(--primary); color: white; }

    .option-btn {
      width: 100%;
      text-align: left;
      padding: 16px 20px;
      border-radius: 16px;
      background: var(--card);
      border: 2px solid var(--border);
      cursor: pointer;
      transition: all 0.25s ease;
      font-size: 1rem;
      line-height: 1.5;
    }

    .option-btn:hover:not(.selected):not(.disabled) {
      border-color: var(--primary);
      background: rgba(13, 115, 119, 0.05);
      transform: translateX(5px);
    }

    .option-btn.selected { border-color: var(--primary); background: rgba(13, 115, 119, 0.1); }
    .option-btn.correct { border-color: var(--success); background: rgba(46, 204, 113, 0.15); }
    .option-btn.wrong { border-color: var(--error); background: rgba(231, 76, 60, 0.15); }
    .option-btn.disabled { cursor: default; opacity: 0.7; }

    .progress-track { height: 8px; background: var(--border); border-radius: 10px; overflow: hidden; }
    .progress-fill { height: 100%; background: linear-gradient(90deg, var(--primary) 0%, var(--accent) 100%); border-radius: 10px; transition: width 0.5s ease; }

    .question-card {
      background: var(--card);
      border-radius: 24px;
      padding: 28px;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.06);
      border: 1px solid var(--border);
    }

    .level-badge {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      padding: 6px 14px;
      border-radius: 50px;
      font-size: 0.85rem;
      font-weight: 600;
    }

    .level-easy { background: rgba(46, 204, 113, 0.15); color: #27AE60; }
    .level-medium { background: rgba(243, 156, 18, 0.15); color: #D68910; }
    .level-hard { background: rgba(155, 89, 182, 0.15); color: #8E44AD; }

    .result-card {
      background: var(--card);
      border-radius: 24px;
      padding: 32px;
      box-shadow: 0 8px 30px rgba(0, 0, 0, 0.08);
    }

    .score-circle {
      width: 160px;
      height: 160px;
      border-radius: 50%;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      margin: 0 auto 24px;
      position: relative;
    }

    .score-circle::before {
      content: '';
      position: absolute;
      inset: 4px;
      border-radius: 50%;
      background: var(--card);
    }

    .score-circle .score-content { position: relative; z-index: 1; text-align: center; }

    .score-excellent { background: conic-gradient(var(--success) 0deg, var(--success) var(--deg), #E8E8E8 var(--deg)); }
    .score-good { background: conic-gradient(var(--primary) 0deg, var(--primary) var(--deg), #E8E8E8 var(--deg)); }
    .score-fair { background: conic-gradient(var(--warning) 0deg, var(--warning) var(--deg), #E8E8E8 var(--deg)); }
    .score-basic { background: conic-gradient(var(--error) 0deg, var(--error) var(--deg), #E8E8E8 var(--deg)); }

    .explanation-card {
      background: rgba(13, 115, 119, 0.05);
      border-radius: 12px;
      padding: 16px;
      margin-top: 12px;
      border-left: 4px solid var(--primary);
    }

    .stagger-item {
      opacity: 0;
      transform: translateY(15px);
      animation: staggerIn 0.4s ease forwards;
    }

    @keyframes staggerIn { to { opacity: 1; transform: translateY(0); } }

    .confetti {
      position: fixed;
      width: 10px;
      height: 10px;
      background: var(--accent);
      animation: confetti-fall 3s ease-out forwards;
      z-index: 1000;
      pointer-events: none;
    }

    @keyframes confetti-fall {
      0% { transform: translateY(-100vh) rotate(0deg); opacity: 1; }
      100% { transform: translateY(100vh) rotate(720deg); opacity: 0; }
    }

    .plane-icon { animation: fly 3s ease-in-out infinite; }

    @keyframes fly {
      0%, 100% { transform: translate(0, 0) rotate(-5deg); }
      50% { transform: translate(10px, -10px) rotate(5deg); }
    }

    .input-field {
      width: 100%;
      padding: 14px 20px;
      border-radius: 12px;
      border: 2px solid var(--border);
      font-size: 1rem;
      font-family: inherit;
      transition: all 0.3s ease;
      background: var(--card);
    }

    .input-field:focus {
      outline: none;
      border-color: var(--primary);
      box-shadow: 0 0 0 4px rgba(13, 115, 119, 0.1);
    }

    .review-item {
      background: var(--card);
      border-radius: 16px;
      padding: 20px;
      margin-bottom: 16px;
      border: 1px solid var(--border);
    }

    .review-item.wrong-answer { border-color: var(--error); background: rgba(231, 76, 60, 0.03); }
    .review-item.correct-answer { border-color: var(--success); background: rgba(46, 204, 113, 0.03); }

    .topic-tag {
      display: inline-block;
      padding: 4px 10px;
      border-radius: 6px;
      font-size: 0.75rem;
      font-weight: 600;
      background: rgba(13, 115, 119, 0.1);
      color: var(--primary);
    }

    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
      }
    }

    @media (max-width: 640px) {
      .question-card { padding: 20px; border-radius: 20px; }
      .option-btn { padding: 14px 16px; font-size: 0.95rem; }
      .result-card { padding: 24px; }
      .score-circle { width: 140px; height: 140px; }
    }
  </style>
</head>
<body>
  <div class="bg-pattern"></div>
  <div class="floating-shapes">
    <div class="shape"></div>
    <div class="shape"></div>
    <div class="shape"></div>
  </div>

  <!-- WELCOME SCREEN -->
  <div id="welcome-screen" class="screen active">
    <div class="min-h-screen flex items-center justify-center px-4 py-8">
      <div class="max-w-lg w-full text-center">
        <div class="mb-8">
          <svg class="plane-icon w-24 h-24 mx-auto" style="color: var(--primary);" viewBox="0 0 100 100" fill="none">
            <circle cx="50" cy="50" r="45" fill="currentColor" opacity="0.1"/>
            <path d="M50 20L30 45H45L50 80L55 45H70L50 20Z" fill="currentColor"/>
            <path d="M35 55L25 60L35 65V55Z" fill="currentColor" opacity="0.7"/>
            <path d="M65 55L75 60L65 65V55Z" fill="currentColor" opacity="0.7"/>
          </svg>
        </div>

        <h1 class="display-font text-4xl md:text-5xl font-bold mb-4" style="color: var(--fg);">
          Travel English Quest
        </h1>
        <p class="text-lg mb-2" style="color: var(--muted);">Diagnostic Test for Young Travelers</p>
        <p class="text-base mb-8" style="color: var(--muted);">Grade 4-6 | 30 Random Questions | 10 HOTS</p>

        <div class="grid grid-cols-4 gap-3 mb-8">
          <div class="bg-white rounded-xl p-4 shadow-sm border" style="border-color: var(--border);">
            <div class="text-2xl font-bold display-font" style="color: var(--primary);">50</div>
            <div class="text-xs" style="color: var(--muted);">Bank Soal</div>
          </div>
          <div class="bg-white rounded-xl p-4 shadow-sm border" style="border-color: var(--border);">
            <div class="text-2xl font-bold display-font" style="color: var(--accent);">30</div>
            <div class="text-xs" style="color: var(--muted);">Soal Tes</div>
          </div>
          <div class="bg-white rounded-xl p-4 shadow-sm border" style="border-color: var(--border);">
            <div class="text-2xl font-bold display-font" style="color: var(--purple);">10</div>
            <div class="text-xs" style="color: var(--muted);">HOTS</div>
          </div>
          <div class="bg-white rounded-xl p-4 shadow-sm border" style="border-color: var(--border);">
            <div class="text-2xl font-bold display-font" style="color: var(--success);">45</div>
            <div class="text-xs" style="color: var(--muted);">Menit</div>
          </div>
        </div>

        <div class="mb-6">
          <input type="text" id="student-name" class="input-field" placeholder="Write your name..." maxlength="30">
        </div>

        <button id="start-btn" class="btn-primary w-full max-w-xs">Start Test</button>

        <div class="mt-8 p-4 bg-white rounded-xl border" style="border-color: var(--border);">
          <p class="text-sm font-semibold mb-2" style="color: var(--fg);">Fitur Baru:</p>
          <div class="flex flex-wrap gap-2 justify-center">
            <span class="topic-tag">Acak Soal</span>
            <span class="topic-tag">Acak Pilihan</span>
            <span class="topic-tag">10 HOTS</span>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- QUIZ SCREEN -->
  <div id="quiz-screen" class="screen">
    <div class="min-h-screen px-4 py-6">
      <div class="max-w-2xl mx-auto">
        <div class="mb-6">
          <div class="flex items-center justify-between mb-3">
            <span id="student-display" class="font-semibold" style="color: var(--muted);"></span>
            <span id="timer-display" class="font-semibold display-font" style="color: var(--accent);">45:00</span>
          </div>
          <div class="progress-track">
            <div id="progress-bar" class="progress-fill" style="width: 0%"></div>
          </div>
          <div class="flex justify-between mt-2 text-sm" style="color: var(--muted);">
            <span id="question-counter">Question 1 of 30</span>
            <span id="level-display"></span>
          </div>
        </div>

        <div class="question-card">
          <div class="flex items-center gap-2 mb-4">
            <div id="level-badge" class="level-badge"></div>
            <span id="topic-tag" class="topic-tag"></span>
          </div>
          <h2 id="question-text" class="text-lg md:text-xl font-semibold mb-6 leading-relaxed"></h2>
          <div id="options-container" class="space-y-3"></div>
        </div>

        <div class="flex justify-between mt-6">
          <button id="prev-btn" class="btn-secondary opacity-50" disabled>Previous</button>
          <button id="next-btn" class="btn-primary" disabled>Next</button>
        </div>
      </div>
    </div>
  </div>

  <!-- RESULT SCREEN -->
  <div id="result-screen" class="screen">
    <div class="min-h-screen px-4 py-8">
      <div class="max-w-2xl mx-auto">
        <div class="result-card text-center mb-6">
          <h2 class="display-font text-3xl font-bold mb-2">Test Result</h2>
          <p id="result-name" class="text-lg mb-6" style="color: var(--muted);"></p>
          
          <div id="score-circle" class="score-circle mb-6">
            <div class="score-content">
              <div id="score-number" class="display-font text-4xl font-bold" style="color: var(--fg);"></div>
              <div class="text-sm" style="color: var(--muted);">out of 30</div>
            </div>
          </div>

          <div id="level-result" class="mb-6"></div>

          <div class="grid grid-cols-3 gap-4 mb-6">
            <div class="bg-green-50 rounded-xl p-4">
              <div id="correct-count" class="text-2xl font-bold display-font text-green-600">0</div>
              <div class="text-sm text-green-700">Correct</div>
            </div>
            <div class="bg-red-50 rounded-xl p-4">
              <div id="wrong-count" class="text-2xl font-bold display-font text-red-600">0</div>
              <div class="text-sm text-red-700">Wrong</div>
            </div>
            <div class="bg-blue-50 rounded-xl p-4">
              <div id="time-taken" class="text-2xl font-bold display-font text-blue-600">--:--</div>
              <div class="text-sm text-blue-700">Time</div>
            </div>
          </div>

          <div id="stats-breakdown" class="mb-6 p-4 bg-gray-50 rounded-xl text-left">
            <p class="font-semibold mb-2">Breakdown by Level:</p>
            <div id="level-stats" class="text-sm space-y-1"></div>
          </div>

          <button id="review-btn" class="btn-secondary">See Explanations</button>
        </div>

        <div id="review-section" class="hidden">
          <h3 class="display-font text-2xl font-bold mb-4">Explanations</h3>
          <div id="review-container"></div>
          <div class="text-center mt-8">
            <button id="restart-btn" class="btn-primary">Try Again</button>
          </div>
        </div>
      </div>
    </div>
  </div>

  <script>
    // ==================== QUESTION BANK (50 Questions) ====================
    const questionBank = [
      // ===== INTRODUCTION (1-7) =====
      { id: 1, topic: 'Introduction', level: 'easy', question: 'Hello! My name is Budi. What is _____ name?', options: ['your', 'you', 'yours', 'you are'], correct: 0, explanation: 'We use "your" to ask about the other person\'s name.' },
      { id: 2, topic: 'Introduction', level: 'easy', question: 'A: How old are you?\nB: I _____ ten years old.', options: ['am', 'is', 'are', 'have'], correct: 0, explanation: 'We use "am" with "I" for age.' },
      { id: 3, topic: 'Introduction', level: 'easy', question: 'Where are you from?\nThe correct answer is...', options: ['I am from Indonesia.', 'I like Indonesia.', 'I go to Indonesia.', 'I have Indonesia.'], correct: 0, explanation: 'We use "I am from..." to tell where we live or come from.' },
      { id: 4, topic: 'Introduction', level: 'easy', question: 'A: Nice to meet you!\nB: _____', options: ['Nice to meet you, too!', 'Thank you!', 'Goodbye!', 'I am fine.'], correct: 0, explanation: 'When someone says "Nice to meet you," we answer "Nice to meet you, too."' },
      { id: 5, topic: 'Introduction', level: 'medium', question: 'What is your hobby?\nChoose the correct answer.', options: ['I like swimming.', 'I am swimming.', 'I can swimming.', 'I go swimming.'], correct: 0, explanation: 'We use "I like + verb-ing" to talk about hobbies.' },
      { id: 6, topic: 'Introduction', level: 'medium', question: 'A: How are you?\nB: _____', options: ['I am fine, thank you.', 'I am from Jakarta.', 'I am ten years old.', 'I like playing.'], correct: 0, explanation: '"How are you?" asks about your feeling or condition.' },
      { id: 7, topic: 'Introduction', level: 'hard', question: 'Your new friend says: "I\'m from Malaysia."\nWhat is the best response?', options: ['Oh, that\'s interesting! I\'ve never been there.', 'I am fine.', 'My name is Budi.', 'Where is Malaysia?'], correct: 0, explanation: 'We show interest when someone tells us where they are from.' },

      // ===== TOILETS & BASIC NEEDS (8-13) =====
      { id: 8, topic: 'Basic Needs', level: 'easy', question: 'You need to go to the toilet. You ask:', options: ['Excuse me, where is the toilet?', 'Where toilet?', 'I want toilet.', 'Toilet is where?'], correct: 0, explanation: 'We say "Excuse me, where is the toilet?" to ask politely.' },
      { id: 9, topic: 'Basic Needs', level: 'easy', question: 'I am thirsty. I want to drink _____.', options: ['water', 'bread', 'rice', 'chicken'], correct: 0, explanation: 'We drink water when we are thirsty.' },
      { id: 10, topic: 'Basic Needs', level: 'medium', question: 'You feel sick. You say:', options: ['I have a headache.', 'I am a headache.', 'I like headache.', 'I get headache.'], correct: 0, explanation: 'We say "I have a..." to tell about sickness or pain.' },
      { id: 11, topic: 'Basic Needs', level: 'medium', question: 'You cannot open your suitcase. You ask for help:\n"_____ help me, please?"', options: ['Can you', 'You can', 'Are you', 'Do you'], correct: 0, explanation: 'We use "Can you help me?" to ask for help politely.' },
      { id: 12, topic: 'Basic Needs', level: 'hard', question: 'You are lost in a big mall. You need to find your parents.\nWhat should you do?', options: ['Find a security guard and ask for help.', 'Run around the mall.', 'Go outside.', 'Cry loudly.'], correct: 0, explanation: 'A security guard can help you find your parents safely.' },
      { id: 13, topic: 'Basic Needs', level: 'hard', question: 'You see a sign: "First Aid". What does it mean?', options: ['A place for medical help.', 'A place to buy food.', 'A place to play.', 'A place to sleep.'], correct: 0, explanation: '"First Aid" is a place for medical help or emergency treatment.' },

      // ===== AT THE RESTAURANT (14-20) =====
      { id: 14, topic: 'Restaurant', level: 'medium', question: 'The waiter asks: "What would you like to eat?"\nYou answer:', options: ['I would like fried rice, please.', 'I want eating fried rice.', 'Give me fried rice.', 'Fried rice for me.'], correct: 0, explanation: 'We use "I would like..." to order food politely.' },
      { id: 15, topic: 'Restaurant', level: 'medium', question: 'You want to see the menu. You say:', options: ['Can I see the menu, please?', 'Where is the menu?', 'I want menu.', 'Give menu.'], correct: 0, explanation: 'We ask "Can I see the menu, please?" politely.' },
      { id: 16, topic: 'Restaurant', level: 'medium', question: 'You finish eating. You want to pay. You say:', options: ['Can I have the bill, please?', 'I want to pay now.', 'How much is this?', 'I am finished.'], correct: 0, explanation: 'We ask for "the bill" when we want to pay at a restaurant.' },
      { id: 17, topic: 'Restaurant', level: 'medium', question: 'The waiter asks: "Would you like some juice?"\nYou want it. You answer:', options: ['Yes, please.', 'Yes, I like.', 'Yes, I want.', 'Yes, I do.'], correct: 0, explanation: 'We say "Yes, please" to accept an offer politely.' },
      { id: 18, topic: 'Restaurant', level: 'hard', question: 'Your food is too salty. You want to tell the waiter.\nWhat should you say?', options: ['Excuse me, this food is too salty.', 'This is bad!', 'I don\'t want this.', 'Give me new food.'], correct: 0, explanation: 'We say the problem politely starting with "Excuse me..."' },
      { id: 19, topic: 'Restaurant', level: 'hard', question: 'You have an allergy to peanuts. What should you ask the waiter?', options: ['Does this food contain peanuts?', 'Is this food good?', 'Do you have peanuts?', 'I don\'t like peanuts.'], correct: 0, explanation: '"Contain" means the food has peanuts inside as ingredient.' },
      { id: 20, topic: 'Restaurant', level: 'hard', question: 'The waiter asks: "How would you like your egg?"\nWhat does he mean?', options: ['How do you want your egg cooked?', 'How many eggs do you want?', 'What color is your egg?', 'Where is your egg?'], correct: 0, explanation: 'The waiter asks if you want your egg fried, boiled, or scrambled.' },

      // ===== AT THE HOTEL (21-27) =====
      { id: 21, topic: 'Hotel', level: 'medium', question: 'You arrive at the hotel. You say:\n"I have a _____ for tonight."', options: ['reservation', 'ticket', 'pass', 'card'], correct: 0, explanation: 'A "reservation" is when you book a room before you arrive.' },
      { id: 22, topic: 'Hotel', level: 'easy', question: 'The receptionist gives you the key. She says:\n"Here is your room _____. The number is 305."', options: ['key', 'door', 'card', 'ticket'], correct: 0, explanation: 'A "room key" opens your hotel room door.' },
      { id: 23, topic: 'Hotel', level: 'hard', question: 'Your room is not clean. You call the receptionist and say:\n"My room is not clean. Can you _____ it, please?"', options: ['clean', 'fix', 'change', 'do'], correct: 0, explanation: 'We ask the hotel staff to "clean" a dirty room.' },
      { id: 24, topic: 'Hotel', level: 'medium', question: 'You need extra towels. You call the receptionist:\n"I need more _____ in my room."', options: ['towels', 'soaps', 'waters', 'beds'], correct: 0, explanation: 'A "towel" is used to dry your body after a shower.' },
      { id: 25, topic: 'Hotel', level: 'hard', question: 'You want to sleep but the next room is very noisy.\nWhat should you do?', options: ['Call the reception to complain.', 'Go to the next room.', 'Sleep anyway.', 'Make more noise.'], correct: 0, explanation: 'The hotel reception can help solve noise problems.' },
      { id: 26, topic: 'Hotel', level: 'hard', question: 'You see a sign on the hotel door: "Do Not Disturb".\nWhat does it mean?', options: ['Please do not enter or knock.', 'Please clean the room.', 'The room is empty.', 'Welcome to the room.'], correct: 0, explanation: '"Do Not Disturb" means the person inside does not want to be bothered.' },
      { id: 27, topic: 'Hotel', level: 'medium', question: 'You want to leave your luggage before check-in time.\nYou ask: "Can I _____ my luggage here?"', options: ['leave', 'put', 'take', 'bring'], correct: 0, explanation: '"Leave" means to let something stay there while you go somewhere else.' },

      // ===== PRICES & SHOPPING (28-35) =====
      { id: 28, topic: 'Shopping', level: 'medium', question: 'You want to know the price. You ask:', options: ['How much is this?', 'How many is this?', 'What is the price?', 'How is the price?'], correct: 0, explanation: 'We ask "How much is this?" to know the price.' },
      { id: 29, topic: 'Shopping', level: 'medium', question: 'You want to buy a T-shirt. You ask the shopkeeper:\n"Can I _____ this on?"', options: ['try', 'wear', 'put', 'take'], correct: 0, explanation: 'We say "try on" when we want to wear clothes to check the size.' },
      { id: 30, topic: 'Shopping', level: 'hard', question: 'The shirt is too expensive. You say:\n"Do you have a _____ price?"', options: ['lower', 'small', 'less', 'little'], correct: 0, explanation: '"Lower price" means a cheaper price or a discount.' },
      { id: 31, topic: 'Shopping', level: 'medium', question: 'In Singapore, you see "$5". What does "$" mean?', options: ['Singapore Dollar', 'Indonesian Rupiah', 'US Dollar', 'Malaysian Ringgit'], correct: 0, explanation: 'The "$" sign in Singapore means Singapore Dollar (SGD).' },
      { id: 32, topic: 'Shopping', level: 'medium', question: 'You pay for your food. The cashier asks:\n"Cash or _____?"', options: ['card', 'coin', 'money', 'bill'], correct: 0, explanation: 'We can pay with "cash" (money) or "card" (debit/credit card).' },
      { id: 33, topic: 'Shopping', level: 'hard', question: 'The shop has a sale. You see a sign "50% OFF".\nWhat does it mean?', options: ['The price is half of the original.', 'The price is 50 dollars.', 'You pay 50% more.', 'Only 50 items left.'], correct: 0, explanation: '"50% OFF" means the price is reduced by half.' },
      { id: 34, topic: 'Shopping', level: 'hard', question: 'You bought a shirt but it is too small. You want to return it.\nYou need the _____.', options: ['receipt', 'menu', 'ticket', 'card'], correct: 0, explanation: 'A "receipt" is the paper proof of your purchase. You need it to return items.' },
      { id: 35, topic: 'Shopping', level: 'hard', question: 'The shopkeeper says: "This is non-refundable."\nWhat does it mean?', options: ['You cannot return this item.', 'This item is free.', 'This item is expensive.', 'You can exchange this item.'], correct: 0, explanation: '"Non-refundable" means you cannot get your money back.' },

      // ===== DIRECTIONS (36-42) =====
      { id: 36, topic: 'Directions', level: 'easy', question: 'You are lost. You ask:\n"Excuse me, _____ is the MRT station?"', options: ['where', 'what', 'when', 'who'], correct: 0, explanation: 'We use "where" to ask about a place or location.' },
      { id: 37, topic: 'Directions', level: 'medium', question: 'Someone gives you directions:\n"Go _____ and turn left."', options: ['straight', 'right', 'back', 'down'], correct: 0, explanation: '"Go straight" means go forward, do not turn.' },
      { id: 38, topic: 'Directions', level: 'medium', question: 'You see a sign: "NO ENTRY". What does it mean?', options: ['You cannot go in.', 'You can go in.', 'Please go in.', 'The door is open.'], correct: 0, explanation: '"No entry" means you are not allowed to enter.' },
      { id: 39, topic: 'Directions', level: 'hard', question: 'The shop is _____ the hotel and the bank.', options: ['between', 'next', 'near', 'behind'], correct: 0, explanation: '"Between" is used when a place has two places on each side.' },
      { id: 40, topic: 'Directions', level: 'medium', question: 'A: Is the museum far from here?\nB: No, it\'s _____. You can walk.', options: ['near', 'far', 'long', 'big'], correct: 0, explanation: 'When we can walk to a place, it means the place is "near".' },
      { id: 41, topic: 'Directions', level: 'hard', question: 'You see a sign: "Pedestrians Only".\nWho can use this road?', options: ['People walking only.', 'Cars only.', 'Bicycles only.', 'Motorcycles only.'], correct: 0, explanation: '"Pedestrians" are people who walk. Cars and bikes cannot enter.' },
      { id: 42, topic: 'Directions', level: 'hard', question: 'You are looking for a restaurant. Someone says:\n"It\'s across from the hospital."\nWhere is the restaurant?', options: ['Opposite the hospital.', 'Inside the hospital.', 'Next to the hospital.', 'Behind the hospital.'], correct: 0, explanation: '"Across from" means on the opposite side of the street.' },

      // ===== TRAVEL VOCABULARY (43-50) =====
      { id: 43, topic: 'Travel', level: 'medium', question: 'At the airport, you show your _____ to the officer.', options: ['passport', 'ticket', 'money', 'bag'], correct: 0, explanation: 'A "passport" is a document for traveling to other countries.' },
      { id: 44, topic: 'Travel', level: 'hard', question: 'You are at the airport. You hear:\n"Flight GA 123 is now _____ at Gate 5."', options: ['boarding', 'leaving', 'going', 'flying'], correct: 0, explanation: '"Boarding" means passengers can get on the plane now.' },
      { id: 45, topic: 'Travel', level: 'medium', question: 'You have a lot of luggage. You put it on a _____.', options: ['trolley', 'bus', 'car', 'train'], correct: 0, explanation: 'A "trolley" or "cart" helps us carry heavy bags at the airport.' },
      { id: 46, topic: 'Travel', level: 'medium', question: 'You want to go to Sentosa Island. You buy a _____.', options: ['ticket', 'pass', 'card', 'letter'], correct: 0, explanation: 'A "ticket" is what you buy to enter a place or use transport.' },
      { id: 47, topic: 'Travel', level: 'hard', question: 'The flight attendant says: "Please fasten your seatbelt."\nWhat should you do?', options: ['Connect the seatbelt around your waist.', 'Open the seatbelt.', 'Stand up.', 'Turn off your phone.'], correct: 0, explanation: '"Fasten" means to connect or close the seatbelt.' },
      { id: 48, topic: 'Travel', level: 'hard', question: 'You see "BOARDING PASS" on your document.\nWhat is it for?', options: ['To get on the plane.', 'To buy food.', 'To open your suitcase.', 'To pay for taxi.'], correct: 0, explanation: 'A "boarding pass" shows your seat number and allows you to enter the plane.' },
      { id: 49, topic: 'Travel', level: 'hard', question: 'At immigration, the officer asks: "What is the purpose of your visit?"\nWhat does he want to know?', options: ['Why you are visiting.', 'Where you are from.', 'How long you will stay.', 'Where you will stay.'], correct: 0, explanation: '"Purpose of visit" means the reason for your trip (holiday, study, work).' },
      { id: 50, topic: 'Travel', level: 'hard', question: 'Your flight is delayed. What does "delayed" mean?', options: ['The flight will leave later than scheduled.', 'The flight is cancelled.', 'The flight is on time.', 'The flight arrived early.'], correct: 0, explanation: '"Delayed" means the flight will not leave at the original time.' }
    ];

    // ==================== STATE VARIABLES ====================
    let currentQuestion = 0;
    let answers = [];
    let studentName = '';
    let startTime = null;
    let timerInterval = null;
    let timeRemaining = 45 * 60;
    let selectedQuestions = [];

    // ==================== DOM ELEMENTS ====================
    let elements = {};

    // ==================== UTILITY FUNCTIONS ====================
    function shuffleArray(array) {
      const arr = [...array];
      for (let i = arr.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [arr[i], arr[j]] = [arr[j], arr[i]];
      }
      return arr;
    }

    function formatTime(seconds) {
      const mins = Math.floor(seconds / 60);
      const secs = seconds % 60;
      return `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
    }

    function getLevelText(level) {
      const levels = {
        easy: { text: 'Easy', class: 'level-easy', icon: '●' },
        medium: { text: 'Medium', class: 'level-medium', icon: '●●' },
        hard: { text: 'HOTS', class: 'level-hard', icon: '★' }
      };
      return levels[level] || levels.easy;
    }

    function showScreen(screenId) {
      document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
      document.getElementById(screenId).classList.add('active');
    }

    // ==================== QUESTION SELECTION ====================
    function selectAndShuffleQuestions() {
      // Separate by level
      const hardQuestions = questionBank.filter(q => q.level === 'hard');
      const otherQuestions = questionBank.filter(q => q.level !== 'hard');

      // Shuffle both pools
      const shuffledHard = shuffleArray(hardQuestions);
      const shuffledOthers = shuffleArray(otherQuestions);

      // Select 10 hard and 20 others
      const selectedHard = shuffledHard.slice(0, 10);
      const selectedOthers = shuffledOthers.slice(0, 20);

      // Combine and shuffle all
      let combined = [...selectedHard, ...selectedOthers];
      combined = shuffleArray(combined);

      // Shuffle options for each question
      combined = combined.map(q => {
        const optionsWithIndex = q.options.map((opt, idx) => ({
          text: opt,
          originalIndex: idx
        }));
        const shuffledOptions = shuffleArray(optionsWithIndex);
        
        return {
          ...q,
          options: shuffledOptions.map(o => o.text),
          correct: shuffledOptions.findIndex(o => o.originalIndex === q.correct)
        };
      });

      return combined;
    }

    // ==================== TIMER ====================
    function startTimer() {
      startTime = Date.now();
      timerInterval = setInterval(() => {
        timeRemaining--;
        if (elements.timerDisplay) {
          elements.timerDisplay.textContent = formatTime(timeRemaining);
        }
        if (timeRemaining <= 0) {
          clearInterval(timerInterval);
          showResults();
        }
        if (timeRemaining === 300 && elements.timerDisplay) {
          elements.timerDisplay.style.color = 'var(--error)';
        }
      }, 1000);
    }

    function stopTimer() {
      if (timerInterval) clearInterval(timerInterval);
    }

    // ==================== RENDER ====================
    function renderQuestion() {
      const q = selectedQuestions[currentQuestion];
      const levelInfo = getLevelText(q.level);

      // Progress
      const progress = ((currentQuestion + 1) / selectedQuestions.length) * 100;
      if (elements.progressBar) elements.progressBar.style.width = `${progress}%`;
      if (elements.questionCounter) elements.questionCounter.textContent = `Question ${currentQuestion + 1} of ${selectedQuestions.length}`;

      // Level badge
      if (elements.levelBadge) {
        elements.levelBadge.className = `level-badge ${levelInfo.class}`;
        elements.levelBadge.innerHTML = `<span>${levelInfo.icon}</span> ${levelInfo.text}`;
      }

      // Topic tag
      if (elements.topicTag) {
        elements.topicTag.textContent = q.topic;
      }

      // Question text
      if (elements.questionText) {
        elements.questionText.innerHTML = q.question.replace(/\n/g, '<br>');
      }

      // Options
      if (elements.optionsContainer) {
        elements.optionsContainer.innerHTML = '';
        const labels = ['A', 'B', 'C', 'D'];

        q.options.forEach((option, index) => {
          const btn = document.createElement('button');
          btn.className = 'option-btn stagger-item';
          btn.style.animationDelay = `${index * 0.08}s`;
          btn.innerHTML = `<span class="font-semibold mr-2" style="color: var(--primary);">${labels[index]}.</span> ${option}`;
          btn.dataset.index = index;

          if (answers[currentQuestion] !== null) {
            btn.classList.add('disabled');
            if (answers[currentQuestion] === index) btn.classList.add('selected');
          }

          btn.addEventListener('click', () => selectOption(index));
          elements.optionsContainer.appendChild(btn);
        });
      }

      // Navigation
      if (elements.prevBtn) {
        elements.prevBtn.disabled = currentQuestion === 0;
        elements.prevBtn.style.opacity = currentQuestion === 0 ? '0.5' : '1';
      }

      updateNextButton();
    }

    function selectOption(index) {
      answers[currentQuestion] = index;
      document.querySelectorAll('.option-btn').forEach((btn, i) => {
        btn.classList.remove('selected');
        if (i === index) btn.classList.add('selected');
      });
      updateNextButton();
    }

    function updateNextButton() {
      const isLastQuestion = currentQuestion === selectedQuestions.length - 1;
      if (elements.nextBtn) {
        elements.nextBtn.textContent = isLastQuestion ? 'Finish' : 'Next';
        elements.nextBtn.disabled = answers[currentQuestion] === null;
        elements.nextBtn.style.opacity = answers[currentQuestion] === null ? '0.5' : '1';
      }
    }

    // ==================== RESULTS ====================
    function showResults() {
      stopTimer();

      let correct = 0;
      const levelStats = { easy: { correct: 0, total: 0 }, medium: { correct: 0, total: 0 }, hard: { correct: 0, total: 0 } };

      selectedQuestions.forEach((q, i) => {
        levelStats[q.level].total++;
        if (answers[i] === q.correct) {
          correct++;
          levelStats[q.level].correct++;
        }
      });

      const wrong = selectedQuestions.length - correct;
      const percentage = (correct / selectedQuestions.length) * 100;
      const deg = Math.max(0, Math.min(360, (percentage / 100) * 360));
      const timeUsed = (45 * 60) - timeRemaining;

      // Update result elements
      if (elements.resultName) elements.resultName.textContent = `Name: ${studentName}`;
      if (elements.scoreNumber) elements.scoreNumber.textContent = correct;
      if (elements.correctCount) elements.correctCount.textContent = correct;
      if (elements.wrongCount) elements.wrongCount.textContent = wrong;
      if (elements.timeTaken) elements.timeTaken.textContent = formatTime(timeUsed);

      // Score circle
      if (elements.scoreCircle) {
        elements.scoreCircle.style.setProperty('--deg', `${deg}deg`);
        elements.scoreCircle.className = 'score-circle';
        if (percentage >= 83) elements.scoreCircle.classList.add('score-excellent');
        else if (percentage >= 60) elements.scoreCircle.classList.add('score-good');
        else if (percentage >= 33) elements.scoreCircle.classList.add('score-fair');
        else elements.scoreCircle.classList.add('score-basic');
      }

      // Level result
      let levelInfo, recommendation;
      if (correct >= 25) {
        levelInfo = { text: 'Advanced', color: 'var(--success)', bg: 'rgba(46, 204, 113, 0.1)' };
        recommendation = 'Excellent! You are ready for the immersion program.';
      } else if (correct >= 18) {
        levelInfo = { text: 'Intermediate', color: 'var(--primary)', bg: 'rgba(13, 115, 119, 0.1)' };
        recommendation = 'Good job! Review the topics you missed.';
      } else if (correct >= 10) {
        levelInfo = { text: 'Basic', color: 'var(--warning)', bg: 'rgba(243, 156, 18, 0.1)' };
        recommendation = 'You need more practice before the trip.';
      } else {
        levelInfo = { text: 'Beginner', color: 'var(--error)', bg: 'rgba(231, 76, 60, 0.1)' };
        recommendation = 'Please study more English before joining.';
      }

      if (elements.levelResult) {
        elements.levelResult.innerHTML = `
          <div class="inline-block px-6 py-3 rounded-full mb-4" style="background: ${levelInfo.bg};">
            <span class="display-font text-xl font-bold" style="color: ${levelInfo.color};">${levelInfo.text}</span>
          </div>
          <p class="text-base" style="color: var(--muted);">${recommendation}</p>
        `;
      }

      // Level stats breakdown
      if (elements.levelStats) {
        elements.levelStats.innerHTML = `
          <p>Easy: ${levelStats.easy.correct}/${levelStats.easy.total} correct</p>
          <p>Medium: ${levelStats.medium.correct}/${levelStats.medium.total} correct</p>
          <p>HOTS (Hard): ${levelStats.hard.correct}/${levelStats.hard.total} correct</p>
        `;
      }

      showScreen('result-screen');

      if (correct >= 18) createConfetti();
    }

    function createConfetti() {
      const colors = ['#FF6B35', '#0D7377', '#2ECC71', '#F39C12', '#14919B', '#9B59B6'];
      for (let i = 0; i < 60; i++) {
        setTimeout(() => {
          const confetti = document.createElement('div');
          confetti.className = 'confetti';
          confetti.style.left = Math.random() * 100 + 'vw';
          confetti.style.background = colors[Math.floor(Math.random() * colors.length)];
          confetti.style.animationDuration = (2 + Math.random() * 2) + 's';
          document.body.appendChild(confetti);
          setTimeout(() => confetti.remove(), 4000);
        }, i * 30);
      }
    }

    // ==================== REVIEW ====================
    function showReview() {
      if (elements.reviewSection) elements.reviewSection.classList.remove('hidden');
      if (elements.reviewContainer) elements.reviewContainer.innerHTML = '';

      const labels = ['A', 'B', 'C', 'D'];

      selectedQuestions.forEach((q, i) => {
        const isCorrect = answers[i] === q.correct;
        const card = document.createElement('div');
        card.className = `review-item ${isCorrect ? 'correct-answer' : 'wrong-answer'}`;

        const levelInfo = getLevelText(q.level);

        let optionsHtml = q.options.map((opt, j) => {
          let classes = 'p-2 rounded-lg mb-2 text-sm';
          if (j === q.correct) classes += ' bg-green-100 text-green-800 font-semibold';
          else if (j === answers[i] && !isCorrect) classes += ' bg-red-100 text-red-800';
          else classes += ' bg-gray-50';
          return `<div class="${classes}">${labels[j]}. ${opt}${j === q.correct ? ' (Correct)' : ''}${j === answers[i] && !isCorrect ? ' (Your answer)' : ''}</div>`;
        }).join('');

        card.innerHTML = `
          <div class="flex items-center gap-2 mb-3 flex-wrap">
            <span class="font-bold display-font" style="color: var(--fg);">Q${i + 1}</span>
            <span class="level-badge ${levelInfo.class} text-xs">${levelInfo.text}</span>
            <span class="topic-tag">${q.topic}</span>
            <span class="ml-auto ${isCorrect ? 'text-green-600' : 'text-red-600'} font-semibold">
              ${isCorrect ? 'Correct' : 'Wrong'}
            </span>
          </div>
          <p class="mb-3 font-medium">${q.question.replace(/\n/g, '<br>')}</p>
          <div class="mb-3">${optionsHtml}</div>
          <div class="explanation-card">
            <p class="text-sm font-semibold mb-1" style="color: var(--primary);">Explanation:</p>
            <p class="text-sm" style="color: var(--muted);">${q.explanation}</p>
          </div>
        `;

        if (elements.reviewContainer) elements.reviewContainer.appendChild(card);
      });

      if (elements.reviewSection) elements.reviewSection.scrollIntoView({ behavior: 'smooth' });
    }

    // ==================== RESTART ====================
    function restart() {
      currentQuestion = 0;
      answers = [];
      timeRemaining = 45 * 60;
      startTime = null;
      selectedQuestions = selectAndShuffleQuestions();

      if (elements.studentNameInput) elements.studentNameInput.value = '';
      if (elements.reviewSection) elements.reviewSection.classList.add('hidden');
      if (elements.reviewContainer) elements.reviewContainer.innerHTML = '';
      if (elements.timerDisplay) elements.timerDisplay.style.color = 'var(--accent)';

      showScreen('welcome-screen');
    }

    // ==================== INITIALIZATION ====================
    function initDOMReferences() {
      elements = {
        welcomeScreen: document.getElementById('welcome-screen'),
        quizScreen: document.getElementById('quiz-screen'),
        resultScreen: document.getElementById('result-screen'),
        startBtn: document.getElementById('start-btn'),
        prevBtn: document.getElementById('prev-btn'),
        nextBtn: document.getElementById('next-btn'),
        reviewBtn: document.getElementById('review-btn'),
        restartBtn: document.getElementById('restart-btn'),
        studentNameInput: document.getElementById('student-name'),
        studentDisplay: document.getElementById('student-display'),
        timerDisplay: document.getElementById('timer-display'),
        progressBar: document.getElementById('progress-bar'),
        questionCounter: document.getElementById('question-counter'),
        levelDisplay: document.getElementById('level-display'),
        questionText: document.getElementById('question-text'),
        optionsContainer: document.getElementById('options-container'),
        levelBadge: document.getElementById('level-badge'),
        topicTag: document.getElementById('topic-tag'),
        scoreCircle: document.getElementById('score-circle'),
        scoreNumber: document.getElementById('score-number'),
        resultName: document.getElementById('result-name'),
        levelResult: document.getElementById('level-result'),
        correctCount: document.getElementById('correct-count'),
        wrongCount: document.getElementById('wrong-count'),
        timeTaken: document.getElementById('time-taken'),
        reviewSection: document.getElementById('review-section'),
        reviewContainer: document.getElementById('review-container'),
        levelStats: document.getElementById('level-stats')
      };
    }

    function initEventListeners() {
      if (elements.startBtn) {
        elements.startBtn.addEventListener('click', () => {
          studentName = (elements.studentNameInput && elements.studentNameInput.value.trim()) || 'Student';
          if (elements.studentDisplay) elements.studentDisplay.textContent = studentName;
          selectedQuestions = selectAndShuffleQuestions();
          startTimer();
          renderQuestion();
          showScreen('quiz-screen');
        });
      }

      if (elements.prevBtn) {
        elements.prevBtn.addEventListener('click', () => {
          if (currentQuestion > 0) {
            currentQuestion--;
            renderQuestion();
          }
        });
      }

      if (elements.nextBtn) {
        elements.nextBtn.addEventListener('click', () => {
          if (currentQuestion < selectedQuestions.length - 1) {
            currentQuestion++;
            renderQuestion();
          } else {
            const unanswered = answers.filter(a => a === null).length;
            if (unanswered > 0) {
              if (confirm(`You have ${unanswered} unanswered questions. Are you sure you want to finish?`)) {
                showResults();
              }
            } else {
              showResults();
            }
          }
        });
      }

      if (elements.reviewBtn) elements.reviewBtn.addEventListener('click', showReview);
      if (elements.restartBtn) elements.restartBtn.addEventListener('click', restart);

      if (elements.studentNameInput) {
        elements.studentNameInput.addEventListener('keypress', (e) => {
          if (e.key === 'Enter' && elements.startBtn) elements.startBtn.click();
        });
      }
    }

    // Initialize on DOM load
    document.addEventListener('DOMContentLoaded', () => {
      initDOMReferences();
      initEventListeners();
      selectedQuestions = selectAndShuffleQuestions();
    });
  </script>
</body>
</html>
