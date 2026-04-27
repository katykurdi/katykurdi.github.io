<!DOCTYPE html>
<html lang="ku" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>کات بەسەربردن - گەمە و کۆمیدی</title>
<script src="https://cdn.tailwindcss.com"></script>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Rabar+021&display=swap');
  
  * {
    font-family: 'Rabar 021', 'Tahoma', sans-serif;
  }
  
  body {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
    min-height: 100vh;
    overflow-x: hidden;
  }
  
  .glass {
    background: rgba(255, 255, 255, 0.15);
    backdrop-filter: blur(15px);
    -webkit-backdrop-filter: blur(15px);
    border: 1px solid rgba(255, 255, 255, 0.25);
  }
  
  .card-hover {
    transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  }
  
  .card-hover:hover {
    transform: translateY(-10px) scale(1.03);
    box-shadow: 0 25px 50px rgba(0,0,0,0.3);
  }
  
  @keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-20px); }
  }
  
  .floating {
    animation: float 4s ease-in-out infinite;
  }
  
  @keyframes wiggle {
    0%, 100% { transform: rotate(-3deg); }
    50% { transform: rotate(3deg); }
  }
  
  .wiggle {
    animation: wiggle 2s ease-in-out infinite;
  }
  
  @keyframes shake {
    0%, 100% { transform: translateX(0); }
    25% { transform: translateX(-10px); }
    75% { transform: translateX(10px); }
  }
  
  .shake {
    animation: shake 0.5s;
  }
  
  .gradient-text {
    background: linear-gradient(45deg, #fbbf24, #f59e0b, #ef4444, #ec4899);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  
  .btn-fun {
    background: linear-gradient(45deg, #f43f5e, #fb7185);
    transition: all 0.3s;
    box-shadow: 0 4px 15px rgba(244, 63, 94, 0.4);
  }
  
  .btn-fun:hover {
    transform: translateY(-3px);
    box-shadow: 0 8px 25px rgba(244, 63, 94, 0.6);
  }
  
  .emoji-bg {
    position: absolute;
    font-size: 3rem;
    opacity: 0.15;
    animation: float 6s ease-in-out infinite;
  }
  
  .modal {
    display: none;
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: rgba(0,0,0,0.7);
    z-index: 100;
    justify-content: center;
    align-items: center;
    padding: 20px;
  }
  
  .modal.active {
    display: flex;
  }
  
  .modal-content {
    background: linear-gradient(135deg, #fff 0%, #f3e8ff 100%);
    border-radius: 25px;
    padding: 30px;
    max-width: 600px;
    width: 100%;
    max-height: 90vh;
    overflow-y: auto;
    animation: popIn 0.4s ease-out;
  }
  
  @keyframes popIn {
    from { transform: scale(0.5); opacity: 0; }
    to { transform: scale(1); opacity: 1; }
  }
  
  .rps-btn {
    font-size: 4rem;
    transition: all 0.3s;
  }
  
  .rps-btn:hover {
    transform: scale(1.2) rotate(10deg);
  }
  
  .memory-card {
    aspect-ratio: 1;
    cursor: pointer;
    perspective: 1000px;
  }
  
  .memory-card-inner {
    position: relative;
    width: 100%;
    height: 100%;
    transition: transform 0.6s;
    transform-style: preserve-3d;
  }
  
  .memory-card.flipped .memory-card-inner {
    transform: rotateY(180deg);
  }
  
  .memory-front, .memory-back {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    border-radius: 15px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2.5rem;
  }
  
  .memory-front {
    background: linear-gradient(135deg, #667eea, #764ba2);
    color: white;
  }
  
  .memory-back {
    background: linear-gradient(135deg, #fbbf24, #f59e0b);
    transform: rotateY(180deg);
  }
  
  .memory-card.matched .memory-back {
    background: linear-gradient(135deg, #10b981, #059669);
  }
  
  ::-webkit-scrollbar {
    width: 10px;
  }
  ::-webkit-scrollbar-track {
    background: rgba(255,255,255,0.1);
  }
  ::-webkit-scrollbar-thumb {
    background: linear-gradient(180deg, #f43f5e, #ec4899);
    border-radius: 10px;
  }
</style>
</head>
<body>

<!-- Background Emojis -->
<div class="emoji-bg" style="top: 10%; left: 5%;">😂</div>
<div class="emoji-bg" style="top: 20%; right: 10%; animation-delay: 1s;">🎮</div>
<div class="emoji-bg" style="top: 50%; left: 8%; animation-delay: 2s;">🤣</div>
<div class="emoji-bg" style="top: 70%; right: 5%; animation-delay: 3s;">🎯</div>
<div class="emoji-bg" style="top: 85%; left: 15%; animation-delay: 1.5s;">🎲</div>

<!-- Header -->
<header class="glass sticky top-0 z-50 py-4 px-6 mb-8">
  <nav class="max-w-7xl mx-auto flex items-center justify-between flex-wrap gap-4">
    <div class="flex items-center gap-3">
      <span class="text-4xl wiggle">🎉</span>
      <h1 class="text-2xl md:text-3xl font-bold text-white">کات بەسەربردن</h1>
    </div>
    <div class="flex gap-4 text-white text-sm md:text-base">
      <a href="#games" class="hover:text-yellow-300 transition">گەمەکان</a>
      <a href="#jokes" class="hover:text-yellow-300 transition">گاڵتە</a>
      <a href="#quiz" class="hover:text-yellow-300 transition">پرسیار</a>
      <a href="#facts" class="hover:text-yellow-300 transition">زانیاری</a>
    </div>
  </nav>
</header>

<!-- Hero Section -->
<section class="text-center px-6 py-12 max-w-5xl mx-auto">
  <h2 class="text-5xl md:text-7xl font-extrabold mb-6 floating">
    <span class="gradient-text">کاتت بە خۆشی</span><br>
    <span class="text-white">بەسەر ببە! 🎊</span>
  </h2>
  <p class="text-xl text-white/90 mb-8 max-w-2xl mx-auto">
    کۆمەڵێک گەمە و گاڵتە و پرسیاری سەرسوڕهێنەر، تەنها بۆ ئەوەی کاتت بە خۆشترین شێوە بەسەر ببەیت 😄
  </p>
  <button onclick="document.getElementById('games').scrollIntoView({behavior:'smooth'})" class="btn-fun text-white px-8 py-4 rounded-full font-bold text-lg">
    دەست پێبکە 🚀
  </button>
</section>

<!-- Games Section -->
<section id="games" class="max-w-7xl mx-auto px-6 py-12">
  <h3 class="text-4xl font-bold text-white text-center mb-10">🎮 گەمەکان</h3>
  <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
    
    <div class="glass rounded-3xl p-6 card-hover cursor-pointer text-center" onclick="openModal('rpsModal')">
      <div class="text-6xl mb-4">✊✋✌️</div>
      <h4 class="text-2xl font-bold text-white mb-2">بەرد، کاغەز، مەقەست</h4>
      <p class="text-white/80">لە دژی کۆمپیوتەر یاری بکە!</p>
    </div>
    
    <div class="glass rounded-3xl p-6 card-hover cursor-pointer text-center" onclick="openModal('memoryModal'); initMemory()">
      <div class="text-6xl mb-4">🧠</div>
      <h4 class="text-2xl font-bold text-white mb-2">یاری بیرەوەری</h4>
      <p class="text-white/80">جووتە کارتەکان بدۆزەرەوە</p>
    </div>
    
    <div class="glass rounded-3xl p-6 card-hover cursor-pointer text-center" onclick="openModal('clickerModal')">
      <div class="text-6xl mb-4">👆</div>
      <h4 class="text-2xl font-bold text-white mb-2">کلیکەری خێرا</h4>
      <p class="text-white/80">لە ١٠ چرکەدا چەند کلیک دەکەیت؟</p>
    </div>
    
    <div class="glass rounded-3xl p-6 card-hover cursor-pointer text-center" onclick="openModal('guessModal'); resetGuess()">
      <div class="text-6xl mb-4">🔢</div>
      <h4 class="text-2xl font-bold text-white mb-2">ژمارەکە بدۆزەرەوە</h4>
      <p class="text-white/80">ژمارەیەک لە نێوان ١-١٠٠</p>
    </div>
    
    <div class="glass rounded-3xl p-6 card-hover cursor-pointer text-center" onclick="openModal('diceModal')">
      <div class="text-6xl mb-4">🎲</div>
      <h4 class="text-2xl font-bold text-white mb-2">گۆلەی بەخت</h4>
      <p class="text-white/80">گۆلە بهاوێژە و بەختت تاقی بکەرەوە</p>
    </div>
    
    <div class="glass rounded-3xl p-6 card-hover cursor-pointer text-center" onclick="openModal('reactionModal')">
      <div class="text-6xl mb-4">⚡</div>
      <h4 class="text-2xl font-bold text-white mb-2">خێرایی کاردانەوە</h4>
      <p class="text-white/80">چەند خێرایت؟</p>
    </div>
    
  </div>
</section>

<!-- Jokes Section -->
<section id="jokes" class="max-w-5xl mx-auto px-6 py-12">
  <h3 class="text-4xl font-bold text-white text-center mb-10">😂 گاڵتەی کۆمیدی</h3>
  <div class="glass rounded-3xl p-8 text-center">
    <div id="jokeText" class="text-2xl md:text-3xl text-white font-bold mb-6 min-h-[100px] flex items-center justify-center">
      دوگمەکە کلیک بکە بۆ گاڵتەیەک! 🎭
    </div>
    <button onclick="newJoke()" class="btn-fun text-white px-8 py-3 rounded-full font-bold">
      گاڵتەی نوێ 🎪
    </button>
  </div>
</section>

<!-- Quiz Section -->
<section id="quiz" class="max-w-5xl mx-auto px-6 py-12">
  <h3 class="text-4xl font-bold text-white text-center mb-10">🤔 پرسیاری سەیر و سەمەرە</h3>
  <div class="glass rounded-3xl p-8">
    <div id="quizQuestion" class="text-2xl text-white font-bold mb-6 text-center"></div>
    <div id="quizOptions" class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6"></div>
    <div id="quizResult" class="text-center text-xl font-bold"></div>
    <div class="text-center mt-6">
      <button onclick="newQuiz()" class="btn-fun text-white px-8 py-3 rounded-full font-bold">
        پرسیاری نوێ 🎯
      </button>
    </div>
  </div>
</section>

<!-- Fun Facts -->
<section id="facts" class="max-w-5xl mx-auto px-6 py-12">
  <h3 class="text-4xl font-bold text-white text-center mb-10">💡 زانیاری سەرسوڕهێنەر</h3>
  <div class="glass rounded-3xl p-8 text-center">
    <div id="factText" class="text-xl md:text-2xl text-white mb-6 min-h-[100px] flex items-center justify-center">
      دوگمەکە کلیک بکە بۆ زانیارییەک!
    </div>
    <button onclick="newFact()" class="btn-fun text-white px-8 py-3 rounded-full font-bold">
      زانیاری نوێ ✨
    </button>
  </div>
</section>

<!-- Footer -->
<footer class="text-center text-white/80 py-8 px-6">
  <p class="text-lg">دروستکراوە بە ❤️ بۆ کاتبەسەربردنی خۆش</p>
  <p class="text-sm mt-2">© 2024 کات بەسەربردن</p>
</footer>

<!-- RPS Modal -->
<div id="rpsModal" class="modal">
  <div class="modal-content text-center">
    <h3 class="text-3xl font-bold mb-4 gradient-text">بەرد، کاغەز، مەقەست</h3>
    <div class="flex justify-around my-6 text-6xl">
      <div>
        <div>تۆ: <span id="playerChoice">❓</span></div>
      </div>
      <div>
        <div>کۆمپیوتەر: <span id="computerChoice">❓</span></div>
      </div>
    </div>
    <div id="rpsResult" class="text-2xl font-bold mb-4 min-h-[40px]"></div>
    <div class="flex justify-center gap-4 mb-4">
      <button class="rps-btn" onclick="playRPS('✊')">✊</button>
      <button class="rps-btn" onclick="playRPS('✋')">✋</button>
      <button class="rps-btn" onclick="playRPS('✌️')">✌️</button>
    </div>
    <p class="text-lg">بردنەوە: <span id="rpsScore">0</span> - <span id="rpsLoss">0</span></p>
    <button onclick="closeModal('rpsModal')" class="btn-fun text-white px-6 py-2 rounded-full mt-4">داخستن</button>
  </div>
</div>

<!-- Memory Modal -->
<div id="memoryModal" class="modal">
  <div class="modal-content text-center">
    <h3 class="text-3xl font-bold mb-4 gradient-text">یاری بیرەوەری</h3>
    <p class="mb-4">هەوڵەکان: <span id="memoryMoves">0</span></p>
    <div id="memoryGrid" class="grid grid-cols-4 gap-2 mb-4"></div>
    <button onclick="initMemory()" class="btn-fun text-white px-6 py-2 rounded-full ml-2">دەستپێکردنەوە</button>
    <button onclick="closeModal('memoryModal')" class="btn-fun text-white px-6 py-2 rounded-full">داخستن</button>
  </div>
</div>

<!-- Clicker Modal -->
<div id="clickerModal" class="modal">
  <div class="modal-content text-center">
    <h3 class="text-3xl font-bold mb-4 gradient-text">کلیکەری خێرا</h3>
    <p class="text-xl mb-2">کات: <span id="clickerTime">10</span> چرکە</p>
    <p class="text-2xl font-bold mb-4">کلیک: <span id="clickerCount">0</span></p>
    <button id="clickerBtn" onclick="doClick()" class="btn-fun text-white px-12 py-8 rounded-full font-bold text-2xl mb-4">
      کلیک بکە! 👆
    </button>
    <div>
      <button onclick="startClicker()" class="btn-fun text-white px-6 py-2 rounded-full ml-2">دەستپێکردن</button>
      <button onclick="closeModal('clickerModal')" class="btn-fun text-white px-6 py-2 rounded-full">داخستن</button>
    </div>
  </div>
</div>

<!-- Guess Modal -->
<div id="guessModal" class="modal">
  <div class="modal-content text-center">
    <h3 class="text-3xl font-bold mb-4 gradient-text">ژمارەکە بدۆزەرەوە</h3>
    <p class="mb-4">ژمارەیەک لە نێوان ١ و ١٠٠ بنوسە</p>
    <input type="number" id="guessInput" min="1" max="100" class="border-2 border-purple-400 rounded-xl px-4 py-2 text-xl text-center mb-4 w-32">
    <br>
    <button onclick="checkGuess()" class="btn-fun text-white px-6 py-2 rounded-full mb-4">پشکنین</button>
    <div id="guessResult" class="text-xl font-bold min-h-[40px] mb-2"></div>
    <p>هەوڵەکان: <span id="guessAttempts">0</span></p>
    <button onclick="closeModal('guessModal')" class="btn-fun text-white px-6 py-2 rounded-full mt-4">داخستن</button>
  </div>
</div>

<!-- Dice Modal -->
<div id="diceModal" class="modal">
  <div class="modal-content text-center">
    <h3 class="text-3xl font-bold mb-4 gradient-text">گۆلەی بەخت</h3>
    <div id="diceDisplay" class="text-9xl my-6">🎲</div>
    <p id="diceResult" class="text-2xl font-bold mb-4"></p>
    <button onclick="rollDice()" class="btn-fun text-white px-6 py-2 rounded-full ml-2">گۆلە بهاوێژە</button>
    <button onclick="closeModal('diceModal')" class="btn-fun text-white px-6 py-2 rounded-full">داخستن</button>
  </div>
</div>

<!-- Reaction Modal -->
<div id="reactionModal" class="modal">
  <div class="modal-content text-center">
    <h3 class="text-3xl font-bold mb-4 gradient-text">خێرایی کاردانەوە</h3>
    <div id="reactionBox" onclick="handleReaction()" class="rounded-2xl p-12 mb-4 cursor-pointer text-2xl font-bold text-white" style="background: linear-gradient(135deg, #6b7280, #4b5563);">
      کلیک بکە بۆ دەستپێکردن
    </div>
    <p id="reactionResult" class="text-xl font-bold"></p>
    <button onclick="closeModal('reactionModal')" class="btn-fun text-white px-6 py-2 rounded-full mt-4">داخستن</button>
  </div>
</div>

<script>
// Modal functions
function openModal(id) {
  document.getElementById(id).classList.add('active');
}
function closeModal(id) {
  document.getElementById(id).classList.remove('active');
}

// Jokes
const jokes = [
  "بۆچی کۆمپیوتەر چووە لای پزیشک؟ چونکە ڤایرۆسی هەبوو! 🦠",
  "مامۆستا: ئەگەر سێ سێو هەبێت و دووانم خوارد، چەندم ماوە؟ قوتابی: دوو سێو، چونکە سێیەمیان نەخواردووە! 🍎",
  "بۆچی ماسی نوقم نابێت؟ چونکە لە ئاودا فێری مەلەوانی بووە لە منداڵییەوە! 🐟",
  "کێ خۆشترینە؟ ئەوەی کە کاتژمێرەکەی خۆی نەفرۆشتووە بۆ کڕینی نان! 😂",
  "بۆچی مریشک ڕێگاکەی بڕی؟ چونکە لای دیکە کافیشاپ هەبوو! 🐔☕",
  "کوڕەکە: باوکە، من ناتوانم خوێندن. باوکی: کوڕم، تۆ مامۆستای! 📚",
  "ئەو کەسەی هەموو ڕۆژێک خۆشی دەوێت، تەنها لە ئاوێنە دەیبینێت! 🪞",
  "بۆچی تەلەفۆن چووە بۆ خوێندنگە؟ بۆ ئەوەی شارژی زانیاری بکات! 📱",
  "هاوڕێم گوتی: من ٣ زمان دەزانم. گوتم: بەڵام تۆ تەنها بە کوردی قسە دەکەیت! گوتی: بەڵێ، بەڵام بێدەنگیم بە سێ زمان دەزانم! 🤐",
  "ئەگەر باران دەباری، ئەوە دارودرەخت دەستیان نەشۆردووە، بەڵکو ئاسمان دڵی پێیان سووتاوە! 🌧️",
  "پزیشک: تۆ ٢٠ کیلۆ زیاد بوویت! نەخۆش: نا دکتۆر، جلەکانم چووکڵە بوون! 👕",
  "بۆچی ڕیاضی غەمگینە؟ چونکە کێشەی زۆری هەیە! ➗"
];

function newJoke() {
  const joke = jokes[Math.floor(Math.random() * jokes.length)];
  const el = document.getElementById('jokeText');
  el.style.opacity = '0';
  setTimeout(() => {
    el.textContent = joke;
    el.style.opacity = '1';
    el.style.transition = 'opacity 0.5s';
  }, 200);
}

// Facts
const facts = [
  "🐙 ئەختەپوس سێ دڵی هەیە و خوێنەکەی شینە!",
  "🍯 هەنگوین هەرگیز خراپ نابێت، تەنانەت دوای ٣٠٠٠ ساڵیش!",
  "🦒 زرافە لە ٢٤ کاتژمێردا تەنها ٣٠ خولەک دەنووێ!",
  "🧠 مێشکی مرۆڤ ٢٠٪ ی وزەی لەش بەکاردێنێت!",
  "🌙 هەنگاوەکانی سەر مانگ تا ١٠٠ ملیۆن ساڵی تر دەمێننەوە!",
  "🐌 خرنە دەتوانێت تا ٣ ساڵ بنوێت!",
  "🦈 نەهەنگ پێش درەختەکان لەسەر زەویدا بوون!",
  "❤️ دڵت ڕۆژانە نزیکەی ١٠٠،٠٠٠ جار لێدەدات!",
  "🍌 مۆز لە ڕووی زانستییەوە بەری دارە، نەک میوە!",
  "🐝 هەنگ دەتوانێت ڕووخسار بناسێتەوە!",
  "🌍 زەوی ڕۆژانە ٢٥،٠٠٠ کیلۆمەتر دەسوڕێتەوە!",
  "🦎 مارمێلکەکان دەتوانن کلکی خۆیان بفڕێنن و دووبارە بێتەوە!"
];

function newFact() {
  const fact = facts[Math.floor(Math.random() * facts.length)];
  const el = document.getElementById('factText');
  el.style.opacity = '0';
  setTimeout(() => {
    el.textContent = fact;
    el.style.opacity = '1';
    el.style.transition = 'opacity 0.5s';
  }, 200);
}

// Quiz
const quizzes = [
  {q: "گەورەترین دەریا لە جیهاندا کامەیە؟", o: ["دەریای ڕۆژهەڵات", "ئۆقیانوسی هێمن", "دەریای سپی", "دەریای ڕەش"], a: 1},
  {q: "چەند ڕۆژ لە ساڵێکی پڕداهاتدا هەیە؟", o: ["365", "366", "364", "367"], a: 1},
  {q: "کام پلانێت گەورەترینە؟", o: ["زەوی", "مەریخ", "موشتەری", "زوهرە"], a: 2},
  {q: "نووسەری شاکاری 'مەم و زین' کێیە؟", o: ["نالی", "ئەحمەدی خانی", "گۆران", "هەژار"], a: 1},
  {q: "چەند ئێسک لە لەشی مرۆڤی گەورەدا هەیە؟", o: ["206", "300", "150", "250"], a: 0},
  {q: "نزیکترین ئەستێرە بۆ زەوی کامەیە؟", o: ["مانگ", "خۆر", "زوهرە", "موشتەری"], a: 1},
  {q: "زمانی فەرمی وڵاتی برازیل چییە؟", o: ["ئیسپانی", "پۆرتوگالی", "ئینگلیزی", "فەڕەنسی"], a: 1},
];

let currentQuiz = -1;
function newQuiz() {
  let idx;
  do { idx = Math.floor(Math.random() * quizzes.length); } while (idx === currentQuiz);
  currentQuiz = idx;
  const q = quizzes[idx];
  document.getElementById('quizQuestion').textContent = q.q;
  document.getElementById('quizResult').textContent = '';
  const optDiv = document.getElementById('quizOptions');
  optDiv.innerHTML = '';
  q.o.forEach((opt, i) => {
    const btn = document.createElement('button');
    btn.className = 'btn-fun text-white px-4 py-3 rounded-2xl font-bold';
    btn.textContent = opt;
    btn.onclick = () => checkQuiz(i, q.a, btn);
    optDiv.appendChild(btn);
  });
}

function checkQuiz(selected, correct, btn) {
  const result = document.getElementById('quizResult');
  if (selected === correct) {
    result.textContent = '✅ زۆر باشە! وەڵامەکەت دروستە';
    result.style.color = '#10b981';
    btn.style.background = 'linear-gradient(45deg, #10b981, #059669)';
  } else {
    result.textContent = '❌ بەداخەوە هەڵە بوو';
    result.style.color = '#ef4444';
    btn.style.background = 'linear-gradient(45deg, #ef4444, #dc2626)';
  }
}

newQuiz();

// RPS Game
let rpsScore = 0, rpsLoss = 0;
function playRPS(player) {
  const choices = ['✊', '✋', '✌️'];
  const computer = choices[Math.floor(Math.random() * 3)];
  document.getElementById('playerChoice').textContent = player;
  document.getElementById('computerChoice').textContent = computer;
  
  let result;
  if (player === computer) {
    result = '🤝 یەکسانە!';
  } else if (
    (player === '✊' && computer === '✌️') ||
    (player === '✋' && computer === '✊') ||
    (player === '✌️' && computer === '✋')
  ) {
    result = '🎉 تۆ بردتەوە!';
    rpsScore++;
  } else {
    result = '😢 تۆ دۆڕایت!';
    rpsLoss++;
  }
  document.getElementById('rpsResult').textContent = result;
  document.getElementById('rpsScore').textContent = rpsScore;
  document.getElementById('rpsLoss').textContent = rpsLoss;
}

// Memory Game
let memoryFlipped = [], memoryMatched = 0, memoryMoves = 0, memoryLock = false;
function initMemory() {
  const emojis = ['🎮', '🎲', '🎯', '🎨', '🎭', '🎪', '🎸', '🎺'];
  const cards = [...emojis, ...emojis].sort(() => Math.random() - 0.5);
  const grid = document.getElementById('memoryGrid');
  grid.innerHTML = '';
  memoryFlipped = [];
  memoryMatched = 0;
  memoryMoves = 0;
  memoryLock = false;
  document.getElementById('memoryMoves').textContent = '0';
  
  cards.forEach((emoji, i) => {
    const card = document.createElement('div');
    card.className = 'memory-card';
    card.dataset.emoji = emoji;
    card.innerHTML = `<div class="memory-card-inner">
      <div class="memory-front">?</div>
      <div class="memory-back">${emoji}</div>
    </div>`;
    card.onclick = () => flipMemory(card);
    grid.appendChild(card);
  });
}

function flipMemory(card) {
  if (memoryLock || card.classList.contains('flipped') || card.classList.contains('matched')) return;
  card.classList.add('flipped');
  memoryFlipped.push(card);
  
  if (memoryFlipped.length === 2) {
    memoryMoves++;
    document.getElementById('memoryMoves').textContent = memoryMoves;
    memoryLock = true;
    
    if (memoryFlipped[0].dataset.emoji === memoryFlipped[1].dataset.emoji) {
      setTimeout(() => {
        memoryFlipped.forEach(c => c.classList.add('matched'));
        memoryFlipped = [];
        memoryLock = false;
        memoryMatched++;
        if (memoryMatched === 8) {
          setTimeout(() => alert(`🎉 سەرکەوتوو بوویت! بە ${memoryMoves} هەوڵدان`), 300);
        }
      }, 500);
    } else {
      setTimeout(() => {
        memoryFlipped.forEach(c => c.classList.remove('flipped'));
        memoryFlipped = [];
        memoryLock = false;
      }, 1000);
    }
  }
}

// Clicker
let clickerCount = 0, clickerTime = 10, clickerInterval = null, clickerActive = false;
function startClicker() {
  clickerCount = 0;
  clickerTime = 10;
  clickerActive = true;
  document.getElementById('clickerCount').textContent = '0';
  document.getElementById('clickerTime').textContent = '10';
  if (clickerInterval) clearInterval(clickerInterval);
  clickerInterval = setInterval(() => {
    clickerTime--;
    document.getElementById('clickerTime').textContent = clickerTime;
    if (clickerTime <= 0) {
      clearInterval(clickerInterval);
      clickerActive = false;
      alert(`🎉 ${clickerCount} کلیکت کرد لە ١٠ چرکەدا!`);
    }
  }, 1000);
}
function doClick() {
  if (!clickerActive) return;
  clickerCount++;
  document.getElementById('clickerCount').textContent = clickerCount;
}

// Guess
let guessNumber = 0, guessAttempts = 0;
function resetGuess() {
  guessNumber = Math.floor(Math.random() * 100) + 1;
  guessAttempts = 0;
  document.getElementById('guessAttempts').textContent = '0';
  document.getElementById('guessResult').textContent = '';
  document.getElementById('guessInput').value = '';
}
function checkGuess() {
  const val = parseInt(document.getElementById('guessInput').value);
  if (isNaN(val)) return;
  guessAttempts++;
  document.getElementById('guessAttempts').textContent = guessAttempts;
  const result = document.getElementById('guessResult');
  if (val === guessNumber) {
    result.textContent = `🎉 سەرکەوتوو بوویت! بە ${guessAttempts} هەوڵدان`;
    result.style.color = '#10b981';
    setTimeout(resetGuess, 2000);
  } else if (val < guessNumber) {
    result.textContent = '⬆️ زیاتر!';
    result.style.color = '#3b82f6';
  } else {
    result.textContent = '⬇️ کەمتر!';
    result.style.color = '#ef4444';
  }
}

// Dice
function rollDice() {
  const display = document.getElementById('diceDisplay');
  const dice = ['⚀', '⚁', '⚂', '⚃', '⚄', '⚅'];
  let i = 0;
  const interval = setInterval(() => {
    display.textContent = dice[Math.floor(Math.random() * 6)];
    i++;
    if (i > 10) {
      clearInterval(interval);
      const final = Math.floor(Math.random() * 6) + 1;
      display.textContent = dice[final - 1];
      document.getElementById('diceResult').textContent = `ژمارە: ${final}`;
    }
  }, 100);
}

// Reaction
let reactionStart = 0, reactionTimeout = null, reactionState = 'idle';
function handleReaction() {
  const box = document.getElementById('reactionBox');
  const result = document.getElementById('reactionResult');
  
  if (reactionState === 'idle' || reactionState === 'done') {
    reactionState = 'waiting';
    box.style.background = 'linear-gradient(135deg, #ef4444, #dc2626)';
    box.textContent = 'چاوەڕێ بە... 🔴';
    result.textContent = '';
    const delay = Math.random() * 4000 + 1000;
    reactionTimeout = setTimeout(() => {
      reactionState = 'ready';
      box.style.background = 'linear-gradient(135deg, #10b981, #059669)';
      box.textContent = 'ئێستا کلیک بکە! 🟢';
      reactionStart = Date.now();
    }, delay);
  } else if (reactionState === 'waiting') {
    clearTimeout(reactionTimeout);
    reactionState = 'done';
    box.style.background = 'linear-gradient(135deg, #6b7280, #4b5563)';
    box.textContent = 'زۆر زوو بوو! دیسان هەوڵ بدە';
  } else if (reactionState === 'ready') {
    const time = Date.now() - reactionStart;
    reactionState = 'done';
    box.style.background = 'linear-gradient(135deg, #6b7280, #4b5563)';
    box.textContent = 'دیسان کلیک بکە';
    result.textContent = `⚡ خێراییت: ${time} میلی چرکە`;
    result.style.color = time < 300 ? '#10b981' : time < 500 ? '#f59e0b' : '#ef4444';
  }
}
</script>

</body>
</html>
