<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
  <title>تطبيق كريستيانو رونالدو</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Tajawal', sans-serif;
    }

    body {
      background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d);
      color: white;
      min-height: 100vh;
      padding: 0;
      overflow-x: hidden;
    }

    .app-container {
      max-width: 500px;
      margin: 0 auto;
      background: rgba(10, 10, 20, 0.92);
      border-radius: 24px;
      box-shadow: 0 10px 40px rgba(0,0,0,0.5);
      overflow: hidden;
      position: relative;
      height: 100vh;
      display: flex;
      flex-direction: column;
    }

    .header {
      background: rgba(0,0,0,0.6);
      padding: 20px;
      text-align: center;
      position: relative;
    }

    .header h1 {
      font-size: 24px;
      font-weight: 800;
      text-shadow: 0 2px 4px rgba(0,0,0,0.5);
    }

    .tab-bar {
      display: flex;
      background: #111;
      justify-content: space-around;
      padding: 12px 0;
      position: sticky;
      bottom: 0;
      z-index: 10;
      box-shadow: 0 -2px 10px rgba(0,0,0,0.3);
    }

    .tab {
      background: transparent;
      color: white;
      border: none;
      font-size: 16px;
      font-weight: bold;
      padding: 8px 16px;
      border-radius: 12px;
      cursor: pointer;
      transition: all 0.3s;
    }

    .tab.active {
      background: #d32f2f;
      transform: scale(1.05);
    }

    .screen {
      padding: 20px;
      flex: 1;
      overflow-y: auto;
      display: none;
      animation: fadeIn 0.5s ease;
    }

    .screen.active {
      display: block;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* معرض الصور */
    .gallery {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 14px;
    }

    .gallery img {
      width: 100%;
      height: 160px;
      object-fit: cover;
      border-radius: 16px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.4);
      transition: transform 0.3s, box-shadow 0.3s;
    }

    .gallery img:hover {
      transform: scale(1.03);
      box-shadow: 0 6px 16px rgba(211, 47, 47, 0.6);
    }

    /* الألغاز */
    .quiz-controls {
      text-align: center;
      margin: 20px 0;
    }

    .question-card {
      background: rgba(30,30,40,0.8);
      padding: 20px;
      border-radius: 18px;
      margin-bottom: 20px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.3);
    }

    .question-text {
      font-size: 18px;
      margin-bottom: 16px;
      line-height: 1.5;
    }

    .option-btn {
      display: block;
      width: 100%;
      padding: 14px;
      margin: 8px 0;
      background: #2c2c3a;
      color: white;
      border: none;
      border-radius: 12px;
      text-align: right;
      font-size: 16px;
      cursor: pointer;
      transition: background 0.2s;
    }

    .option-btn:hover {
      background: #3a3a4a;
    }

    .option-btn.selected {
      background: #d32f2f;
      border-left: 4px solid white;
    }

    .final-score {
      text-align: center;
      font-size: 28px;
      font-weight: bold;
      margin-top: 30px;
      color: #4caf50;
    }

    /* زر بدء التطبيق */
    .start-screen {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 100%;
      text-align: center;
      padding: 20px;
    }

    .start-screen h2 {
      font-size: 28px;
      margin-bottom: 30px;
      text-shadow: 0 2px 4px rgba(0,0,0,0.5);
    }

    .start-btn {
      background: linear-gradient(to right, #d32f2f, #b71c1c);
      color: white;
      border: none;
      padding: 16px 40px;
      font-size: 20px;
      font-weight: bold;
      border-radius: 50px;
      cursor: pointer;
      box-shadow: 0 6px 15px rgba(183, 28, 28, 0.5);
      transition: transform 0.2s, box-shadow 0.2s;
    }

    .start-btn:hover {
      transform: translateY(-3px);
      box-shadow: 0 8px 20px rgba(183, 28, 28, 0.7);
    }

    /* إضافة خط عربي جميل */
    @import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700;800&display=swap');
  </style>
</head>
<body>

<div class="app-container">
  <!-- شاشة البداية -->
  <div class="screen active" id="start-screen">
    <div class="start-screen">
      <h2>مرحباً بك في عالم<br>كريستيانو رونالدو!</h2>
      <button class="start-btn" onclick="startApp()">ابدأ التطبيق</button>
    </div>
  </div>

  <!-- شاشة المعرض -->
  <div class="screen" id="gallery-screen">
    <div class="header">
      <h1>معرض الصور</h1>
    </div>
    <div class="gallery">
      <img src="https://upload.wikimedia.org/wikipedia/commons/8/8c/Cristiano_Ronaldo_2018.jpg" alt="2018">
      <img src="https://upload.wikimedia.org/wikipedia/commons/6/69/Cristiano_Ronaldo_Manchester_United_2021.jpg" alt="ManUtd 2021">
      <img src="https://upload.wikimedia.org/wikipedia/commons/3/3c/Cristiano_Ronaldo_2017-2018.jpg" alt="Real Madrid">
      <img src="https://upload.wikimedia.org/wikipedia/commons/7/74/Cristiano_Ronaldo_Al_Nassr_FC.jpg" alt="Al Nassr">
      <img src="https://upload.wikimedia.org/wikipedia/commons/1/15/Cristiano_Ronaldo_2008.jpg" alt="2008">
      <img src="https://upload.wikimedia.org/wikipedia/commons/5/57/Cristiano_Ronaldo_Juventus_2018-12-02.jpg" alt="Juventus">
      <img src="https://upload.wikimedia.org/wikipedia/commons/e/e9/Cristiano_Ronaldo_vs_Spain_2018.jpg" alt="World Cup 2018">
      <img src="https://upload.wikimedia.org/wikipedia/commons/5/53/Cristiano_Ronaldo_2022_FIFA_World_Cup.jpg" alt="World Cup 2022">
    </div>
  </div>

  <!-- شاشة الألغاز -->
  <div class="screen" id="quiz-screen">
    <div class="header">
      <h1>اختبار كريستيانو رونالدو</h1>
    </div>
    <div id="quiz-content"></div>
  </div>

  <!-- شريط التنقل السفلي -->
  <div class="tab-bar">
    <button class="tab" onclick="switchScreen('gallery')">الصور</button>
    <button class="tab" onclick="switchScreen('quiz')">الألغاز</button>
  </div>
</div>

<script>
  // --- بدء التطبيق ---
  function startApp() {
    document.getElementById('start-screen').classList.remove('active');
    document.getElementById('gallery-screen').classList.add('active');
    document.querySelectorAll('.tab')[0].classList.add('active');
  }

  // --- التنقل بين الشاشات ---
  let currentScreen = 'gallery';
  document.querySelectorAll('.tab')[0].classList.add('active');

  function switchScreen(screen) {
    // إزالة النشط من الجميع
    document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));

    // إظهار الشاشة المطلوبة
    if (screen === 'gallery') {
      document.getElementById('gallery-screen').classList.add('active');
      document.querySelectorAll('.tab')[0].classList.add('active');
      currentScreen = 'gallery';
    } else if (screen === 'quiz') {
      document.getElementById('quiz-screen').classList.add('active');
      document.querySelectorAll('.tab')[1].classList.add('active');
      loadQuiz();
      currentScreen = 'quiz';
    }
  }

  // --- أسئلة الألغاز (20 مثال — يمكنك توسيعها لـ100) ---
  const quizQuestions = [
    { q: "في أي سنة وُلد كريستيانو رونالدو؟", a: ["1984", "1985", "1986", "1987"], correct: "1985" },
    { q: "من أي دولة ينحدر كريستيانو رونالدو؟", a: ["إسبانيا", "البرتغال", "فرنسا", "إيطاليا"], correct: "البرتغال" },
    { q: "ما اسم والدته؟", a: ["ماريا دولوريس", "إيزابيل", "أليسيا", "كريستينا"], correct: "ماريا دولوريس" },
    { q: "كم عدد أبنائه؟", a: ["3", "4", "5", "6"], correct: "5" },
    { q: "في أي نادٍ فاز بأول دوري أبطال؟", a: ["ريال مدريد", "يوفنتوس", "مانشستر يونايتد", "برشلونة"], correct: "مانشستر يونايتد" },
    { q: "كم مرة فاز بجائزة الحذاء الذهبي؟", a: ["2", "3", "4", "5"], correct: "4" },
    { q: "ما هو رقم قميصه الشهير؟", a: ["7", "9", "10", "11"], correct: "7" },
    { q: "أين وُلد؟", a: ["لشبونة", "مدريد", "فونشال", "بورتو"], correct: "فونشال" },
    { q: "كم هدف سجّل في دوري أبطال أوروبا (حتى 2025)؟", a: ["120+", "130+", "140+", "150+"], correct: "140+" },
    { q: "ما أول لقب كبير فاز به؟", a: ["الدوري البرتغالي", "كأس البرتغال", "كأس الاتحاد الإنجليزي", "دوري أبطال أوروبا"], correct: "كأس البرتغال" },
    // أضف 90 سؤالًا آخر بنفس التنسيق!
  ];

  let userAnswers = {};

  function loadQuiz() {
    const content = document.getElementById('quiz-content');
    content.innerHTML = quizQuestions.map((q, i) => `
      <div class="question-card">
        <div class="question-text">${i + 1}. ${q.q}</div>
        ${q.a.map(opt => `
          <button class="option-btn" onclick="selectAnswer(${i}, '${opt}')">${opt}</button>
        `).join('')}
      </div>
    `).join('') + `
      <div class="quiz-controls">
        <button class="start-btn" onclick="submitQuiz()">إرسال الإجابات</button>
      </div>
      <div id="quiz-result"></div>
    `;
    // إعادة تعيين الإجابات
    userAnswers = {};
  }

  function selectAnswer(index, answer) {
    userAnswers[index] = answer;
    // تحديث واجهة الزر المحدد
    document.querySelectorAll('.question-card')[index].querySelectorAll('.option-btn').forEach(btn => {
      btn.classList.remove('selected');
    });
    event.target.classList.add('selected');
  }

  function submitQuiz() {
    let score = 0;
    quizQuestions.forEach((q, i) => {
      if (userAnswers[i] === q.correct) score++;
    });
    const percent = Math.round((score / quizQuestions.length) * 100);
    let msg = `أحسنت! 🏆<br>إجابتك الصحيحة: <b>${score}/${quizQuestions.length}</b><br>`;
    if (percent >= 90) msg += "أنت خبير CR7 حقيقي!";
    else if (percent >= 70) msg += "ممتاز! أنت من محبيه الحقيقيين.";
    else if (percent >= 50) msg += "جيد، لكن يمكنك التعلم أكثر!";
    else msg += "حاول مرة أخرى واقرأ عن أسطورتك!";

    document.getElementById('quiz-result').innerHTML = `<div class="final-score">${msg}</div>`;
  }
</script>

</body>
</html>
