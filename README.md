# Random-Quotes-website
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>منصة الاقتباسات الملهمة - مشروع حوسبة سحابية</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        :root {
            --primary-color: #667eea;
            --secondary-color: #764ba2;
            --accent-color: #4CAF50;
            --text-color: #2c3e50;
            --bg-color: #ffffff;
            --card-bg: #f8f9fa;
            --shadow: 0 20px 40px rgba(0,0,0,0.1);
            --transition: all 0.3s ease;
        }
        
        .dark-mode {
            --primary-color: #8a6de9;
            --secondary-color: #9a76d4;
            --accent-color: #66bb6a;
            --text-color: #ecf0f1;
            --bg-color: #1a1a2e;
            --card-bg: #16213e;
            --shadow: 0 20px 40px rgba(0,0,0,0.3);
        }
        
        body {
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            line-height: 1.6;
            transition: var(--transition);
            position: relative;
            overflow-x: hidden;
        }
        
        /* تأثيرات الخلفية المتحركة */
        .bg-animation {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0.1;
        }
        
        .floating-shape {
            position: absolute;
            background: rgba(255,255,255,0.1);
            border-radius: 50%;
            animation: float 20s infinite linear;
        }
        
        .shape-1 { width: 100px; height: 100px; top: 10%; left: 10%; animation-delay: 0s; }
        .shape-2 { width: 150px; height: 150px; top: 60%; left: 80%; animation-delay: -5s; }
        .shape-3 { width: 80px; height: 80px; top: 80%; left: 20%; animation-delay: -10s; }
        .shape-4 { width: 120px; height: 120px; top: 30%; left: 70%; animation-delay: -15s; }
        
        @keyframes float {
            0%, 100% { transform: translate(0, 0) rotate(0deg); }
            25% { transform: translate(100px, 50px) rotate(90deg); }
            50% { transform: translate(50px, 100px) rotate(180deg); }
            75% { transform: translate(-50px, 50px) rotate(270deg); }
        }
        
        .container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 25px;
            padding: 40px;
            box-shadow: var(--shadow);
            text-align: center;
            max-width: 850px;
            width: 100%;
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255,255,255,0.2);
            transition: var(--transition);
            position: relative;
            overflow: hidden;
        }
        
        .dark-mode .container {
            background: rgba(26, 26, 46, 0.95);
            border: 1px solid rgba(255,255,255,0.1);
        }
        
        /* تأثير دخول الحاوية */
        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(50px) scale(0.9);
            }
            to {
                opacity: 1;
                transform: translateY(0) scale(1);
            }
        }
        
        .container {
            animation: slideIn 0.8s ease-out;
        }
        
        .header {
            margin-bottom: 40px;
            padding-bottom: 25px;
            border-bottom: 2px solid rgba(0,0,0,0.1);
            position: relative;
        }
        
        .dark-mode .header {
            border-bottom-color: rgba(255,255,255,0.1);
        }
        
        .header::after {
            content: '';
            position: absolute;
            bottom: -2px;
            left: 50%;
            transform: translateX(-50%);
            width: 100px;
            height: 3px;
            background: linear-gradient(90deg, var(--primary-color), var(--accent-color));
            border-radius: 2px;
        }
        
        .header h1 {
            color: var(--text-color);
            font-size: 2.8rem;
            margin-bottom: 15px;
            background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
            position: relative;
        }
        
        .header h1::before {
            content: '📚';
            position: absolute;
            left: -50px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 2rem;
            animation: bounce 2s infinite;
        }
        
        @keyframes bounce {
            0%, 100% { transform: translateY(-50%) scale(1); }
            50% { transform: translateY(-50%) scale(1.1); }
        }
        
        .header p {
            color: var(--text-color);
            font-size: 1.2rem;
            opacity: 0.8;
        }
        
        .stats {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin: 30px 0;
            flex-wrap: wrap;
        }
        
        .stat-item {
            background: var(--card-bg);
            padding: 20px;
            border-radius: 15px;
            min-width: 140px;
            transition: var(--transition);
            border: 1px solid rgba(0,0,0,0.05);
            position: relative;
            overflow: hidden;
        }
        
        .dark-mode .stat-item {
            border-color: rgba(255,255,255,0.05);
        }
        
        .stat-item::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 3px;
            background: linear-gradient(90deg, var(--primary-color), var(--accent-color));
        }
        
        .stat-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.15);
        }
        
        .stat-number {
            font-size: 2rem;
            font-weight: bold;
            color: var(--accent-color);
            display: block;
            margin-bottom: 5px;
        }
        
        .stat-label {
            font-size: 0.9rem;
            color: var(--text-color);
            opacity: 0.8;
        }
        
        .quote-box {
            background: linear-gradient(135deg, var(--card-bg), var(--card-bg));
            border-radius: 20px;
            padding: 50px 40px;
            margin: 40px 0;
            border-left: 5px solid var(--accent-color);
            position: relative;
            transition: var(--transition);
            box-shadow: 0 10px 30px rgba(0,0,0,0.08);
        }
        
        .dark-mode .quote-box {
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        
        .quote-box::before {
            content: '"';
            position: absolute;
            top: 20px;
            right: 30px;
            font-size: 6rem;
            color: var(--accent-color);
            opacity: 0.2;
            font-family: serif;
        }
        
        .quote-box:hover {
            transform: translateY(-8px);
            box-shadow: 0 15px 35px rgba(0,0,0,0.15);
        }
        
        .quote-text {
            font-size: 1.9rem;
            line-height: 1.8;
            color: var(--text-color);
            margin-bottom: 25px;
            font-weight: 600;
            position: relative;
            z-index: 1;
            transition: var(--transition);
        }
        
        .quote-author {
            font-size: 1.4rem;
            color: var(--text-color);
            font-style: italic;
            margin-bottom: 20px;
            opacity: 0.9;
            position: relative;
            padding-right: 30px;
        }
        
        .quote-author::before {
            content: '—';
            position: absolute;
            right: 0;
            color: var(--accent-color);
        }
        
        .quote-category {
            display: inline-block;
            background: linear-gradient(135deg, var(--accent-color), var(--primary-color));
            color: white;
            padding: 10px 25px;
            border-radius: 25px;
            font-size: 0.95rem;
            font-weight: 500;
            box-shadow: 0 4px 15px rgba(76, 175, 80, 0.3);
            transition: var(--transition);
        }
        
        .quote-category:hover {
            transform: scale(1.05);
            box-shadow: 0 6px 20px rgba(76, 175, 80, 0.4);
        }
        
        .buttons {
            margin: 40px 0;
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
        }
        
        .btn {
            background: linear-gradient(135deg, var(--accent-color), var(--primary-color));
            color: white;
            border: none;
            padding: 18px 35px;
            font-size: 1.1rem;
            border-radius: 35px;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 12px;
            box-shadow: 0 6px 20px rgba(76, 175, 80, 0.3);
            position: relative;
            overflow: hidden;
        }
        
        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
            transition: 0.5s;
        }
        
        .btn:hover::before {
            left: 100%;
        }
        
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(76, 175, 80, 0.4);
        }
        
        .btn:active {
            transform: translateY(-1px);
        }
        
        .btn-secondary {
            background: linear-gradient(135deg, #6c757d, #5a6268);
            box-shadow: 0 6px 20px rgba(108, 117, 125, 0.3);
        }
        
        .btn-secondary:hover {
            box-shadow: 0 8px 25px rgba(108, 117, 125, 0.4);
        }
        
        .btn-info {
            background: linear-gradient(135deg, #17a2b8, #138496);
            box-shadow: 0 6px 20px rgba(23, 162, 184, 0.3);
        }
        
        .btn-info:hover {
            box-shadow: 0 8px 25px rgba(23, 162, 184, 0.4);
        }
        
        .btn-dark {
            background: linear-gradient(135deg, #343a40, #23272b);
            box-shadow: 0 6px 20px rgba(52, 58, 64, 0.3);
        }
        
        .btn-dark:hover {
            box-shadow: 0 8px 25px rgba(52, 58, 64, 0.4);
        }
        
        .theme-toggle {
            position: absolute;
            top: 20px;
            left: 20px;
            background: var(--card-bg);
            border: none;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.3rem;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            transition: var(--transition);
            z-index: 100;
        }
        
        .theme-toggle:hover {
            transform: rotate(30deg);
        }
        
        .footer {
            margin-top: 50px;
            padding-top: 30px;
            border-top: 2px solid rgba(0,0,0,0.1);
            color: var(--text-color);
        }
        
        .dark-mode .footer {
            border-top-color: rgba(255,255,255,0.1);
        }
        
        .cloud-badge {
            display: inline-block;
            background: linear-gradient(135deg, #2196F3, #1976D2);
            color: white;
            padding: 12px 25px;
            border-radius: 25px;
            font-size: 1rem;
            font-weight: 500;
            margin-top: 20px;
            box-shadow: 0 4px 15px rgba(33, 150, 243, 0.3);
            transition: var(--transition);
        }
        
        .cloud-badge:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(33, 150, 243, 0.4);
        }
        
        /* تأثيرات النص المتحركة */
        @keyframes textGlow {
            0%, 100% { text-shadow: 0 0 5px rgba(76, 175, 80, 0.5); }
            50% { text-shadow: 0 0 20px rgba(76, 175, 80, 0.8), 0 0 30px rgba(76, 175, 80, 0.6); }
        }
        
        .glowing-text {
            animation: textGlow 2s ease-in-out infinite;
        }
        
        /* شريط التقدم المتحرك */
        .progress-bar {
            width: 100%;
            height: 4px;
            background: rgba(0,0,0,0.1);
            border-radius: 2px;
            margin: 20px 0;
            overflow: hidden;
        }
        
        .dark-mode .progress-bar {
            background: rgba(255,255,255,0.1);
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--primary-color), var(--accent-color));
            border-radius: 2px;
            width: 0%;
            transition: width 30s linear;
        }
        
        /* تأثيرات للشاشات الصغيرة */
        @media (max-width: 768px) {
            .container {
                padding: 30px 20px;
                margin: 10px;
            }
            
            .header h1 {
                font-size: 2.2rem;
            }
            
            .header h1::before {
                position: static;
                display: block;
                margin-bottom: 10px;
                transform: none;
            }
            
            .quote-text {
                font-size: 1.5rem;
            }
            
            .buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .btn {
                width: 100%;
                max-width: 300px;
                justify-content: center;
            }
            
            .stats {
                gap: 15px;
            }
            
            .stat-item {
                min-width: 120px;
                padding: 15px;
            }
        }
        
        /* تأثيرات خاصة للوضع الليلي */
        .dark-mode .btn {
            box-shadow: 0 6px 20px rgba(0,0,0,0.3);
        }
        
        /* تأثير اهتزاز عند التحديث */
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }
        
        .shake {
            animation: shake 0.5s ease-in-out;
        }
    </style>
</head>
<body>
    <!-- تأثيرات الخلفية المتحركة -->
    <div class="bg-animation">
        <div class="floating-shape shape-1"></div>
        <div class="floating-shape shape-2"></div>
        <div class="floating-shape shape-3"></div>
        <div class="floating-shape shape-4"></div>
    </div>
    
    <div class="container">
        <!-- زر تبديل الوضع الليلي -->
        <button class="theme-toggle" onclick="toggleDarkMode()" title="تبديل الوضع الليلي">
            🌙
        </button>
        
        <div class="header">
            <h1>منصة الاقتباسات الملهمة</h1>
            <p>اكتشف كنوز الحكمة والإلهام من مختلف الثقافات والحضارات</p>
        </div>
        
        <div class="stats">
            <div class="stat-item">
                <span class="stat-number" id="totalQuotes">50</span>
                <div class="stat-label">اقتباس متاح</div>
            </div>
            <div class="stat-item">
                <span class="stat-number" id="categories">8</span>
                <div class="stat-label">فئة متنوعة</div>
            </div>
            <div class="stat-item">
                <span class="stat-number" id="authors">25</span>
                <div class="stat-label">مفكر وكاتب</div>
            </div>
        </div>
        
        <!-- شريط التقدم -->
        <div class="progress-bar">
            <div class="progress-fill" id="progressFill"></div>
        </div>
        
        <div class="quote-box" id="quoteBox">
            <div class="quote-text" id="quoteText">"الحياة رحلة، استمتع بها ولا تستعجل النهاية"</div>
            <div class="quote-author" id="quoteAuthor">- مصطفى محمود</div>
            <div class="quote-category" id="quoteCategory">حكمة</div>
        </div>
        
        <div class="buttons">
            <button class="btn" onclick="getRandomQuote()">
                🔄 اقتباس جديد
            </button>
            <button class="btn btn-secondary" onclick="showAllQuotes()">
                📖 جميع الاقتباسات
            </button>
            <button class="btn btn-info" onclick="shareQuote()">
                📤 مشاركة الاقتباس
            </button>
            <button class="btn btn-dark" onclick="speakQuote()">
                🔊 استماع للاقتباس
            </button>
        </div>
        
        <div class="footer">
            <p>تم تطوير هذا المشروع كجزء من مادة الحوسبة السحابية</p>
            <p>يعرض مجموعة مختارة من أروع الاقتباسات العربية والعالمية</p>
            <div class="cloud-badge glowing-text">☁️ مستضاف سحابياً على GitHub Pages - نموذج للحوسبة السحابية</div>
        </div>
    </div>

    <script>
        // قاعدة البيانات الشاملة للاقتباسات
        const quotes = [
            // حكمة
            {text: "الحكمة هي أن تعرف ما الذي تعرفه، وما الذي لا تعرفه", author: "سقراط", category: "حكمة"},
            {text: "كن أنت التغيير الذي تريد أن تراه في العالم", author: "غاندي", category: "حكمة"},
            {text: "الحياة بسيطة، لكننا نصر على تعقيدها", author: "كونفوشيوس", category: "حكمة"},
            {text: "أعظم المجازفات ألا نخاطر بشيء", author: "مجهول", category: "حكمة"},
            {text: "ليس المهم طول الحياة، بل عمقها", author: "إمرسون", category: "حكمة"},
            {text: "من لا يعرف التاريخ يظل طفلاً إلى الأبد", author: "شيشرون", category: "حكمة"},
            {text: "الحكمة أعظم من القوة", author: "مثل عربي", category: "حكمة"},
            {text: "الصمت حكمة وقليل فاعله", author: "مثل عربي", category: "حكمة"},

            // نجاح
            {text: "النجاح رحلة وليس وجهة", author: "مجهول", category: "نجاح"},
            {text: "الفشل ليس نهاية الطريق، بل محطة تعلم", author: "مجهول", category: "نجاح"},
            {text: "لا تنتظر الظروف المثالية، اصنعها", author: "مجهول", category: "نجاح"},
            {text: "التميز ليس بمهارة، بل بعادة", author: "أرسطو", category: "نجاح"},
            {text: "المستقبل لمن يتعلم مهارات اليوم", author: "مالكوم إكس", category: "نجاح"},
            {text: "النجاح يحققه الذين يواصلون المحاولة", author: "مجهول", category: "نجاح"},
            {text: "ابدأ من حيث أنت، واستخدم ما لديك", author: "آرثر آش", category: "نجاح"},

            // تحفيز
            {text: "لا تؤجل عمل اليوم إلى الغد", author: "مثل عربي", category: "تحفيز"},
            {text: "الأمل هو الحلم في حالة اليقظة", author: "أرسطو", category: "تحفيز"},
            {text: "التحديات هي ما تجعل الحياة مثيرة للاهتمام", author: "جوشوا مارين", category: "تحفيز"},
            {text: "أنت أقوى مما تظن", author: "مجهول", category: "تحفيز"},
            {text: "لا يوجد مصعد للنجاح، يجب أن تستخدم السلالم", author: "مجهول", category: "تحفيز"},
            {text: "الحلم لا يتحقق بالتمني، بل بالإرادة والعمل", author: "مجهول", category: "تحفيز"},

            // فلسفة
            {text: "أنا أفكر، إذن أنا موجود", author: "ديكارت", category: "فلسفة"},
            {text: "الحياة ما هي إلا معانقة للمجهول", author: "مجهول", category: "فلسفة"},
            {text: "الحرية هي أن تعيش كما تختار", author: "أفلاطون", category: "فلسفة"},
            {text: "الجمال في عين الناظر", author: "مثل إنجليزي", category: "فلسفة"},
            {text: "الحقيقة موجودة، والباطل مصنوع", author: "مجهول", category: "فلسفة"},

            // علم
            {text: "الفضول هو شعلة العقل", author: "ويليام آرثر وارد", category: "علم"},
            {text: "العلم هو نور العقل", author: "مجهول", category: "علم"},
            {text: "كل اكتشاف يفتح أبواباً جديدة", author: "ماري كوري", category: "علم"},
            {text: "التعليم هو أقوى سلاح يمكنك استخدامه لتغيير العالم", author: "نيلسون مانديلا", category: "علم"},
            {text: "العقل مثل المظلة، يعمل فقط عندما يكون مفتوحاً", author: "مجهول", category: "علم"},

            // إبداع
            {text: "الإبداع يولد من رحم المعاناة", author: "مجهول", category: "إبداع"},
            {text: "الفن هو كذبة تجعلنا ندرك الحقيقة", author: "بابلو بيكاسو", category: "إبداع"},
            {text: "الخيال أهم من المعرفة", author: "ألبرت أينشتاين", category: "إبداع"},
            {text: "لا توجد قواعد في الفن، فقط النتائج", author: "مجهول", category: "إبداع"},

            // علاقات
            {text: "الصداقة نبع الحياة", author: "مثل عربي", category: "علاقات"},
            {text: "الحب لا ينظر بالعين بل بالقلب", author: "شكسبير", category: "علاقات"},
            {text: "الأسرة ليست شيء مهم، بل كل شيء", author: "مايكل جيه فوكس", category: "علاقات"},
            {text: "الابتسامة تذيب الجليد", author: "مثل عربي", category: "علاقات"},

            // تطوير ذات
            {text: "تعلم من الأمس، عش اليوم، تمنى الغد", author: "أينشتاين", category: "تطوير ذات"},
            {text: "التغيير يبدأ من الداخل", author: "مجهول", category: "تطوير ذات"},
            {text: "القراءة غذاء العقل", author: "مثل عربي", category: "تطوير ذات"},
            {text: "الوقت كالسيف إن لم تقطعه قطعك", author: "مثل عربي", category: "تطوير ذات"},
            {text: "الرحلة الألف ميل تبدأ بخطوة", author: "مثل صيني", category: "تطوير ذات"},
            {text: "لا تيأس، فعادة ما يكون آخر مفتاح في مجموعة المفاتيح هو الذي سيفتح الباب", author: "مجهول", category: "تطوير ذات"},
            {text: "النجاح هو مجموع الجهود الصغيرة المتكررة يوماً بعد يوم", author: "روبرت كولير", category: "تطوير ذات"},

            // إضافية
            {text: "الصبر مفتاح الفرج", author: "مثل عربي", category: "حكمة"},
            {text: "العقل السليم في الجسم السليم", author: "مثل لاتيني", category: "صحة"},
            {text: "الاقتصاد فضيلة وضرورة", author: "مثل عربي", category: "اقتصاد"},
            {text: "السفر يوسع الآفاق", author: "مثل عالمي", category: "سفر"}
        ];

        // إحصائيات الموقع
        function updateStats() {
            document.getElementById('totalQuotes').textContent = quotes.length;
            
            const categories = [...new Set(quotes.map(quote => quote.category))];
            document.getElementById('categories').textContent = categories.length;
            
            const authors = [...new Set(quotes.map(quote => quote.author))];
            document.getElementById('authors').textContent = authors.length;
        }

        // تأثيرات عند تغيير الاقتباس
        function animateQuoteChange() {
            const quoteBox = document.getElementById('quoteBox');
            quoteBox.style.transform = 'scale(0.95)';
            quoteBox.style.opacity = '0.7';
            
            setTimeout(() => {
                quoteBox.style.transform = 'scale(1)';
                quoteBox.style.opacity = '1';
                quoteBox.classList.add('shake');
                
                setTimeout(() => {
                    quoteBox.classList.remove('shake');
                }, 500);
            }, 200);
        }

        // عرض اقتباس عشوائي
        function getRandomQuote() {
            animateQuoteChange();
            
            setTimeout(() => {
                const randomIndex = Math.floor(Math.random() * quotes.length);
                const quote = quotes[randomIndex];
                
                document.getElementById('quoteText').textContent = `"${quote.text}"`;
                document.getElementById('quoteAuthor').textContent = `- ${quote.author}`;
                document.getElementById('quoteCategory').textContent = quote.category;
                
                // إعادة تعيين شريط التقدم
                resetProgressBar();
            }, 300);
        }

        // عرض جميع الاقتباسات
        function showAllQuotes() {
            let allQuotes = "📚 جميع الاقتباسات المتاحة:\n\n";
            
            // تجميع الاقتباسات حسب الفئة
            const quotesByCategory = {};
            quotes.forEach(quote => {
                if (!quotesByCategory[quote.category]) {
                    quotesByCategory[quote.category] = [];
                }
                quotesByCategory[quote.category].push(quote);
            });
            
            // عرض الاقتباسات مصنفة
            Object.keys(quotesByCategory).forEach(category => {
                allQuotes += `\n🌈 ${category}:\n`;
                quotesByCategory[category].forEach((quote, index) => {
                    allQuotes += `${index + 1}. "${quote.text}"\n   - ${quote.author}\n\n`;
                });
            });
            
            alert(allQuotes);
        }

        // مشاركة الاقتباس
        function shareQuote() {
            const quoteText = document.getElementById('quoteText').textContent;
            const quoteAuthor = document.getElementById('quoteAuthor').textContent;
            const quoteCategory = document.getElementById('quoteCategory').textContent;
            
            const shareText = `${quoteText}\n${quoteAuthor}\n📂 ${quoteCategory}\n\nشارك من: منصة الاقتباسات الملهمة`;
            
            if (navigator.share) {
                navigator.share({
                    title: 'اقتباس ملهم',
                    text: shareText
                });
            } else {
                // نسخ للناسخة إذا لم يكن المشاركة متاحة
                navigator.clipboard.writeText(shareText).then(() => {
                    alert('✅ تم نسخ الاقتباس! يمكنك مشاركته الآن');
                });
            }
        }

        // استماع للاقتباس (Text-to-Speech)
        function speakQuote() {
            const quoteText = document.getElementById('quoteText').textContent;
            const quoteAuthor = document.getElementById('quoteAuthor').textContent;
            
            const speech = new SpeechSynthesisUtterance();
            speech.text = `${quoteText} ${quoteAuthor}`;
            speech.lang = 'ar-SA';
            speech.rate = 0.9;
            speech.pitch = 1;
            
            window.speechSynthesis.speak(speech);
        }

        // تبديل الوضع الليلي
        function toggleDarkMode() {
            document.body.classList.toggle('dark-mode');
            const themeToggle = document.querySelector('.theme-toggle');
            
            if (document.body.classList.contains('dark-mode')) {
                themeToggle.innerHTML = '☀️';
                themeToggle.title = 'الوضع النهاري';
                localStorage.setItem('darkMode', 'enabled');
            } else {
                themeToggle.innerHTML = '🌙';
                themeToggle.title = 'الوضع الليلي';
                localStorage.setItem('darkMode', 'disabled');
            }
        }

        // شريط التقدم التلقائي
        function resetProgressBar() {
            const progressFill = document.getElementById('progressFill');
            progressFill.style.transition = 'none';
            progressFill.style.width = '0%';
            
            setTimeout(() => {
                progressFill.style.transition = 'width 30s linear';
                progressFill.style.width = '100%';
            }, 100);
        }

        // التحقق من الوضع المخزن
        function checkDarkModePreference() {
            if (localStorage.getItem('darkMode') === 'enabled') {
                document.body.classList.add('dark-mode');
                document.querySelector('.theme-toggle').innerHTML = '☀️';
                document.querySelector('.theme-toggle').title = 'الوضع النهاري';
            }
        }

        // تهيئة الموقع
        window.onload = function() {
            getRandomQuote();
            updateStats();
            resetProgressBar();
            checkDarkModePreference();
            
            // تغيير الاقتباس تلقائياً كل 30 ثانية
            setInterval(getRandomQuote, 30000);
            
            // إضافة تأثيرات عشوائية للأشكال العائمة
            const shapes = document.querySelectorAll('.floating-shape');
            shapes.forEach(shape => {
                const randomDelay = Math.random() * 20;
                shape.style.animationDelay = `-${randomDelay}s`;
            });
        };

        // تأثيرات إضافية عند التمرير
        window.addEventListener('scroll', function() {
            const scrolled = window.pageYOffset;
            const rate = scrolled * -0.5;
            
            document.querySelector('.bg-animation').style.transform = `translateY(${rate}px)`;
        });
    </script>
</body>
</html>
