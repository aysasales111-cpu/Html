#html <!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chemistry Advanced Mock Test</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f4f6f9;
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
        }
        .quiz-container {
            max-width: 650px;
            width: 100%;
            background: #fff;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.08);
        }
        h1 {
            text-align: center;
            color: #1a73e8;
            font-size: 24px;
            margin-top: 0;
            border-bottom: 2px solid #e8f0fe;
            padding-bottom: 15px;
        }
        /* Login Screen */
        .start-screen {
            text-align: center;
            padding: 20px 10px;
        }
        .input-group {
            margin-bottom: 15px;
            text-align: left;
            max-width: 80%;
            margin-left: auto;
            margin-right: auto;
        }
        .input-group label {
            display: block;
            font-weight: bold;
            margin-bottom: 5px;
            color: #3c4043;
        }
        .input-field {
            width: 100%;
            padding: 12px;
            border: 2px solid #dadce0;
            border-radius: 6px;
            font-size: 16px;
            outline: none;
            box-sizing: border-box;
        }
        .input-field:focus {
            border-color: #1a73e8;
        }
        .error-message {
            color: #d93025;
            font-weight: bold;
            margin-top: 10px;
            display: none;
        }
        .btn {
            background-color: #1a73e8;
            color: white;
            border: none;
            padding: 12px 30px;
            font-size: 16px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: bold;
            transition: background 0.2s;
            margin-top: 15px;
        }
        .btn:hover {
            background-color: #1557b0;
        }
        /* Header Info */
        .exam-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #e8f0fe;
            padding: 12px 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            font-weight: bold;
            font-size: 16px;
            color: #1c3d5a;
            position: sticky;
            top: 10px;
            z-index: 100;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }
        .timer-box {
            color: #d93025;
            background: #fce8e6;
            padding: 5px 10px;
            border-radius: 4px;
            border: 1px solid #fad2cf;
        }
        /* Questions */
        .question-card {
            margin-bottom: 25px;
            padding-bottom: 20px;
            border-bottom: 1px dashed #dadce0;
        }
        .question-text {
            font-size: 17px;
            font-weight: bold;
            color: #202124;
            margin-bottom: 12px;
            line-height: 1.5;
        }
        .options-container {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .option-label {
            background-color: #f8f9fa;
            border: 1px solid #dadce0;
            border-radius: 6px;
            padding: 12px;
            font-size: 15px;
            cursor: pointer;
            display: flex;
            align-items: center;
            transition: background 0.2s;
        }
        .option-label:hover {
            background-color: #f1f3f4;
        }
        .option-label input {
            margin-right: 12px;
            transform: scale(1.2);
        }
        /* Result Screen */
        .result-box {
            text-align: center;
            padding: 20px;
            background: #e6f4ea;
            border-radius: 8px;
            color: #137333;
            margin-bottom: 25px;
        }
        .explanation-box {
            margin-top: 10px;
            padding: 12px;
            background-color: #f1f3f4;
            border-left: 4px solid #5f6368;
            border-radius: 4px;
            font-size: 14px;
            color: #3c4043;
            line-height: 1.5;
        }
        .correct-ans {
            background-color: #d4edda !important;
            border-color: #c3e6cb !important;
            color: #155724;
        }
        .wrong-ans {
            background-color: #f8d7da !important;
            border-color: #f5c6cb !important;
            color: #721c24;
        }
        #sending-status {
            font-weight: bold;
            color: #1a73e8;
            margin-top: 10px;
            display: none;
        }
    </style>
</head>
<body>

<div class="quiz-container">
    <h1>রসায়ন অ্যাডভান্সড মক টেস্ট</h1>

    <div id="start-screen" class="start-screen">
        <h3>পরীক্ষার্থী লগইন পোর্টাল</h3>
        
        <div class="input-group">
            <label for="student-name-input">পরীক্ষার্থীর নাম (Student Name):</label>
            <input type="text" id="student-name-input" class="input-field" placeholder="আপনার নাম লিখুন..." autocomplete="off">
        </div>

        <div class="input-group">
            <label for="student-id-input">ইউনিক ইউজার আইডি (User ID):</label>
            <input type="text" id="student-id-input" class="input-field" placeholder="ইউজার আইডি দিন..." autocomplete="off">
        </div>

        <div class="input-group">
            <label for="student-pass-input">পরীক্ষার পাসওয়ার্ড (Password):</label>
            <input type="password" id="student-pass-input" class="input-field" placeholder="গোপন পাসওয়ার্ড দিন...">
        </div>

        <div id="login-error" class="error-message">❌ ভুল আইডি অথবা পাসওয়ার্ড! আবার চেষ্টা করুন।</div>
        
        <button class="btn" onclick="validateAndStart()">লগইন ও পরীক্ষা শুরু</button>
    </div>

    <div id="exam-screen" style="display: none;">
        <div class="exam-header">
            <div>আইডি: <span id="display-student-id" style="color: #5f6368;"></span> | নাম: <span id="display-student-name" style="color: #1a73e8;"></span></div>
            <div class="timer-box">সময় বাকি: <span id="timer">10:00</span></div>
        </div>

        <form id="quiz-form">
            <div class="question-card">
                <p class="question-text">১. পাইরোফসফরিক অ্যাসিডে (H<sub>4</sub>P<sub>2</sub>O<sub>7</sub>) ফসফরাসের জারণ অবস্থা কত?</p>
                <div class="options-container">
                    <label class="option-label"><input type="radio" name="q1" value="A">ক) +3</label>
                    <label class="option-label"><input type="radio" name="q1" value="B">খ) +4</label>
                    <label class="option-label"><input type="radio" name="q1" value="C">গ) +5</label>
                    <label class="option-label"><input type="radio" name="q1" value="D">ঘ) +6</label>
                </div>
                <div class="explanation-box" id="exp-q1" style="display:none;">
                    <strong>সঠি উত্তর: গ) +5</strong><br>
                    <strong>ব্যাখ্যা:</strong> H<sub>4</sub>P<sub>2</sub>O<sub>7</sub> অণুতে জারণ সংখ্যার হিসাব করলে দাঁড়ায়: 4(+1) + 2x + 7(-2) = 0। এটি সমাধান করলে হয়, 4 + 2x - 14 = 0 বা 2x = 10, সুতরাং x = +5।
                </div>
            </div>

            <div class="question-card">
                <p class="question-text">২. C<sub>4</sub>H<sub>9</sub>Br আণবিক সংকেতবিশিষ্ট যৌগের দ্বি-বন্ধন তুল্যাঙ্ক (DBE) কত?</p>
                <div class="options-container">
                    <label class="option-label"><input type="radio" name="q2" value="A">ক) 0</label>
                    <label class="option-label"><input type="radio" name="q2" value="B">খ) 1</label>
                    <label class="option-label"><input type="radio" name="q2" value="C">গ) 2</label>
                    <label class="option-label"><input type="radio" name="q2" value="D">ঘ) 3</label>
                </div>
                <div class="explanation-box" id="exp-q2" style="display:none;">
                    <strong>সঠিক উত্তর: ক) 0</strong><br>
                    <strong>ব্যাখ্যা:</strong> সমীকরণ অনুযায়ী, C<sub>4</sub>H<sub>9</sub>Br এর দ্বি-বন্ধন তুল্যাঙ্ক (DBE) = [4(4-2)+9(1-2)+1(1-2)]/2 + 1। এর মান হিসাব করলে 0 হয়, যা নির্দেশ করে এটি একটি সম্পৃক্ত মুক্ত শৃঙ্খল যৌগ (অ্যালকিল হ্যালাইড)।
                </div>
            </div>

            <div class="question-card">
                <p class="question-text">৩. ICl<sub>4</sub><sup>-</sup> আয়নে কেন্দ্রীয় আয়োডিন পরমাণুর চারদিকে কতগুলি নিঃসঙ্গ ইলেকট্রন-জোড় (Lone pair) রয়েছে?</p>
                <div class="options-container">
                    <label class="option-label"><input type="radio" name="q3" value="A">ক) 0</label>
                    <label class="option-label"><input type="radio" name="q3" value="B">খ) 1</label>
                    <label class="option-label"><input type="radio" name="q3" value="C">গ) 2</label>
                    <label class="option-label"><input type="radio" name="q3" value="D">ঘ) 3</label>
                </div>
                <div class="explanation-box" id="exp-q3" style="display:none;">
                    <strong>সঠিক উত্তর: গ) 2</strong><br>
                    <strong>ব্যাখ্যা:</strong> I-পরমাণুর যোজ্যতা কক্ষে 7টি ইলেকট্রন, 4টি Cl পরমাণু দ্বারা প্রদত্ত 4টি ইলেকট্রন এবং নেগেটিভ চার্জের জন্য 1টি ইলেকট্রন থাকে। মোট ইলেকট্রন সংখ্যা = 12, তাই ইলেকট্রন-জোড়ের সংখ্যা = 12/2 = 6। এর মধ্যে 4টি বন্ধন-জোড় এবং 2টি নিঃসঙ্গ ইলেকট্রন-জোড় বর্তমান, ফলে এটি সামতলিক বর্গাকার গঠন লাভ করে।
                </div>
            </div>

            <div class="question-card">
                <p class="question-text">৪. C<sub>5</sub>H<sub>12</sub> (পেন্টেন)-এর ব্রোমিনেশনের ফলে মোট কয়টি মনোব্রোমিনেটেড যৌগ (স্টিরিওআইসোমার বাদে) পাওয়া যাবে?</p>
                <div class="options-container">
                    <label class="option-label"><input type="radio" name="q4" value="A">ক) 3</label>
                    <label class="option-label"><input type="radio" name="q4" value="B">খ) 4</label>
                    <label class="option-label"><input type="radio" name="q4" value="C">গ) 5</label>
                    <label class="option-label"><input type="radio" name="q4" value="D">ঘ) 8</label>
                </div>
                <div class="explanation-box" id="exp-q4" style="display:none;">
                    <strong>সঠিক উত্তর: ঘ) 8</strong><br>
                    <strong>ব্যাখ্যা:</strong> C<sub>5</sub>H<sub>12</sub> সংকেতবিশিষ্ট তিনটি সমাবয়বী অ্যালকেনের ক্ষেত্রে, n-পেন্টেন থেকে 3টি, 2-মিথাইলবিউটেন থেকে 4টি এবং 2,2-ডাইমিথাইলপ্রোপেন থেকে 1টি মনোব্রোমিনেটেড যৌগ পাওয়া যায়। অতএব, মনোব্রোমিনেটেড যৌগের মোট সংখ্যা = 3 + 4 + 1 = 8।
                </div>
            </div>

            <div class="question-card">
                <p class="question-text">৫. P<sub>4</sub>(g) → 2P<sub>2</sub>(g) বিক্রিয়াটিতে এনথ্যালপির পরিবর্তন (ΔH) কত? (P-P এবং P≡P বন্ধন-বিয়োজন এনথ্যালপি যথাক্রমে 209 এবং 490 kJ·mol<sup>-1</sup>)</p>
                <div class="options-container">
                    <label class="option-label"><input type="radio" name="q5" value="A">ক) +274 kJ·mol<sup>-1</sup></label>
                    <label class="option-label"><input type="radio" name="q5" value="B">খ) -274 kJ·mol<sup>-1</sup></label>
                    <label class="option-label"><input type="radio" name="q5" value="C">গ) +1254 kJ·mol<sup>-1</sup></label>
                    <label class="option-label"><input type="radio" name="q5" value="D">ঘ) -980 kJ·mol<sup>-1</sup></label>
                </div>
                <div class="explanation-box" id="exp-q5" style="display:none;">
                    <strong>সঠিক উত্তর: ক) +274 kJ·mol<sup>-1</sup></strong><br>
                    <strong>ব্যাখ্যা:</strong> 1টি P<sub>4</sub> অণুতে 6টি P-P বন্ধন এবং 2টি P<sub>2</sub> অণুতে 2টি P≡P বন্ধন আছে। সুতরাং, P<sub>4</sub> থেকে 2P<sub>2</sub> তে রূপান্তরিত হতে এনথ্যালপির পরিবর্তন (ΔH) = 6 × 209 - 2 × 490 = 1254 - 980 = +274 kJ·mol<sup>-1</sup>।
                </div>
            </div>

            <div class="question-card">
                <p class="question-text">৬. XeO<sub>3</sub>F<sub>2</sub> অণুতে কেন্দ্রীয় Xe পরমাণুর সংকরায়ণ অবস্থা ও নিঃসঙ্গ ইলেকট্রন-জোড়ের সংখ্যা কত?</p>
                <div class="options-container">
                    <label class="option-label"><input type="radio" name="q6" value="A">ক) sp<sup>3</sup>d<sup>2</sup>, 1</label>
                    <label class="option-label"><input type="radio" name="q6" value="B">খ) sp<sup>3</sup>d, 0</label>
                    <label class="option-label"><input type="radio" name="q6" value="C">গ) sp<sup>3</sup>d, 1</label>
                    <label class="option-label"><input type="radio" name="q6" value="D">ঘ) sp<sup>3</sup>d<sup>2</sup>, 0</label>
                </div>
                <div class="explanation-box" id="exp-q6" style="display:none;">
                    <strong>সঠিক উত্তর: খ) sp<sup>3</sup>d, 0</strong><br>
                    <strong>ব্যাখ্যা:</strong> XeO<sub>3</sub>F<sub>2</sub> এর ক্ষেত্রে H = 1/2 [8+2] = 5, অর্থাৎ সংকরায়ণ sp<sup>3</sup>d। নিঃসঙ্গ ইলেকট্রন-জোড়ের সংখ্যা = 5 - 2 - 3 = 0, যার ফলে অণুটির আকৃতি ত্রিকোণীয় দ্বি-পিরামিডীয় হয়।
                </div>
            </div>

            <div class="question-card">
                <p class="question-text">৭. ClO<sub>3</sub><sup>-</sup> আয়নের গঠন নির্ণয়ের জন্য H এর মান (ইলেকট্রন-জোড় সংখ্যা) কত?</p>
                <div class="options-container">
                    <label class="option-label"><input type="radio" name="q7" value="A">ক) 3</label>
                    <label class="option-label"><input type="radio" name="q7" value="B">খ) 4</label>
                    <label class="option-label"><input type="radio" name="q7" value="C">গ) 5</label>
                    <label class="option-label"><input type="radio" name="q7" value="D">ঘ) 6</label>
                </div>
                <div class="explanation-box" id="exp-q7" style="display:none;">
                    <strong>সঠিক উত্তর: খ) 4</strong><br>
                    <strong>ব্যাখ্যা:</strong> VSEPR সূত্রানুযায়ী, H = 1/2 [V+X-C+A] = 1/2 [7+0-0+1] = 4। সুতরাং ইলেকট্রন-জোড়ের সংখ্যা 4 হওয়ায় গঠন চতুস্তলকীয় হবে (যাতে 1টি নিঃসঙ্গ-জোড় ও 3টি বন্ধন-জোড় থাকে)।
                </div>
            </div>

            <div class="question-card">
                <p class="question-text">৮. P<sub>4</sub>O<sub>10</sub> অণুতে P-O-P সেতুবন্ধনের সংখ্যা এবং P=O বন্ধনের সংখ্যা যথাক্রমে কত?</p>
                <div class="options-container">
                    <label class="option-label"><input type="radio" name="q8" value="A">ক) 4 এবং 6</label>
                    <label class="option-label"><input type="radio" name="q8" value="B">খ) 6 এবং 4</label>
                    <label class="option-label"><input type="radio" name="q8" value="C">গ) 5 এবং 5</label>
                    <label class="option-label"><input type="radio" name="q8" value="D">ঘ) 3 এবং 4</label>
                </div>
                <div class="explanation-box" id="exp-q8" style="display:none;">
                    <strong>সঠিক উত্তর: খ) 6 এবং 4</strong><br>
                    <strong>ব্যাখ্যা:</strong> P<sub>4</sub>O<sub>10</sub> অণুর গঠনে 6টি P-O-P সেতুবন্ধন এবং 4টি P=O বন্ধন বর্তমান থাকে।
                </div>
            </div>

            <div class="question-card">
                <p class="question-text">৯. H<sub>3</sub>PO<sub>3</sub>-এর ডিসপ্রোপরসনেশন বিক্রিয়ায় ফসফরাসের জারণ সংখ্যা +3 থেকে পরিবর্তিত হয়ে কী কী হয়?</p>
                <div class="options-container">
                    <label class="option-label"><input type="radio" name="q9" value="A">ক) +1 এবং +5</label>
                    <label class="option-label"><input type="radio" name="q9" value="B">খ) -3 এবং +5</label>
                    <label class="option-label"><input type="radio" name="q9" value="C">গ) 0 এবং +5</label>
                    <label class="option-label"><input type="radio" name="q9" value="D">ঘ) -3 এবং +4</label>
                </div>
                <div class="explanation-box" id="exp-q9" style="display:none;">
                    <strong>সঠিক উত্তর: খ) -3 এবং +5</strong><br>
                    <strong>ব্যাখ্যা:</strong> বিক্রিয়াটি হল: 4H<sub>3</sub>PO<sub>3</sub> → PH<sub>3</sub> + 3H<sub>3</sub>PO<sub>4</sub>। এই ডিসপ্রোপরসনেশন বিক্রিয়ায় P-এর জারণ সংখ্যা +3 থেকে হ্রাস পেয়ে PH<sub>3</sub> তে -3 এবং বৃদ্ধি পেয়ে H<sub>3</sub>PO<sub>4</sub> তে +5 হয়।
                </div>
            </div>

            <div class="question-card">
                <p class="question-text">১০. অ্যালকেনের মুক্ত-মূলক হ্যালোজেনেশন বিক্রিয়ায় ব্রোমিন (Br<sub>2</sub>) দ্বারা 3°, 2° এবং 1° হাইড্রোজেনের প্রতিস্থাপনের তুলনামূলক হার কত?</p>
                <div class="options-container">
                    <label class="option-label"><input type="radio" name="q10" value="A">ক) 5 : 3.8 : 1</label>
                    <label class="option-label"><input type="radio" name="q10" value="B">খ) 1600 : 82 : 1</label>
                    <label class="option-label"><input type="radio" name="q10" value="C">গ) 1 : 2 : 3</label>
                    <label class="option-label"><input type="radio" name="q10" value="D">ঘ) 1 : 82 : 1600</label>
                </div>
                <div class="explanation-box" id="exp-q10" style="display:none;">
                    <strong>সঠিক উত্তর: খ) 1600 : 82 : 1</strong><br>
                    <strong>ব্যাখ্যা:</strong> ব্রোমিনের সিলেক্টিভিটি (selectivity) ক্লোরিন অপেক্ষা অনেক বেশি। ব্রোমিনের ক্ষেত্রে 3°, 2° এবং 1° H-এর প্রতিস্থাপনের তুলনামূলক হার 1600:82:1, যেখানে ক্লোরিনের ক্ষেত্রে এই হার মাত্র 5:3.8:1।
                </div>
            </div>

            <div style="text-align: center; margin-top: 20px;">
                <button type="button" id="submit-btn" class="btn" style="background-color: #34a853;" onclick="submitExam()">খাতা জমা দিন (Submit)</button>
                <div id="sending-status">⏳ শিক্ষকের কাছে রেজাল্ট পাঠানো হচ্ছে... দয়া করে অপেক্ষা করুন।</div>
            </div>
        </form>

        <div id="result-screen" style="display: none; margin-top: 30px;">
            <div class="result-box">
                <h2>পরীক্ষার ফলাফল</h2>
                <p style="font-size: 16px;">আইডি: <span id="res-id" style="font-weight: bold;"></span> | পরীক্ষার্থী: <span id="res-name" style="font-weight: bold;"></span></p>
                <p style="font-size: 22px; font-weight: bold;">মোট স্কোর: <span id="score">0</span> / ১০</p>
            </div>
            <h3 style="color: #3c4043; border-bottom: 2px solid #ccc; padding-bottom: 5px;">উত্তরপত্র পর্যালোচনা (Answer Sheet)</h3>
        </div>
    </div>
</div>

<script>
    // ⚠️ এই নিচের লিংকের জায়গায় আপনার নিজের Google Web App URLটি বসাবেন
    const GOOGLE_SCRIPT_URL = "YOUR_GOOGLE_WEB_APP_URL_HERE";

    // আপনার দেওয়া নির্দিষ্ট ৩টি জোড়া User ID এবং Password ম্যাপিং
    const credentials = {
        "Samir7890": "999999S",
        "Aksha5678": "888888A",
        "Ritu1234": "333333R"
    };

    // সঠিক উত্তরের চাবিকাঠি
    const correctAnswers = {
        q1: "C", q2: "A", q3: "C", q4: "D", q5: "A",
        q6: "B", q7: "B", q8: "B", q9: "B", q10: "B"
    };

    let totalTime = 600; // ১০ মিনিট
    let timerInterval;

    // পাসওয়ার্ড ভ্যালিডেশন এবং পরীক্ষা শুরুর ফাংশন
    function validateAndStart() {
        const nameInput = document.getElementById('student-name-input').value.trim();
        const idInput = document.getElementById('student-id-input').value.trim();
        const passInput = document.getElementById('student-pass-input').value.trim();
        const errorDiv = document.getElementById('login-error');

        if (nameInput === "" || idInput === "" || passInput === "") {
            errorDiv.innerText = "⚠️ দয়া করে নাম, আইডি এবং পাসওয়ার্ড সবকটি পূরণ করুন!";
            errorDiv.style.display = 'block';
            return;
        }

        // 🔒 পরীক্ষা একবারে বেশি দেওয়া বন্ধ করার সিকিউরিটি চেক
        if (localStorage.getItem("locked_" + idInput) === "true") {
            errorDiv.innerText = "❌ এই ইউজার আইডি দিয়ে ইতিমধ্যেই পরীক্ষা দেওয়া হয়ে গেছে! আপনি আর লগইন করতে পারবেন না।";
            errorDiv.style.display = 'block';
            return;
        }

        // ইউজার আইডি এবং পাসওয়ার্ড ম্যাচিং চেক
        if (credentials[idInput] && credentials[idInput] === passInput) {
            errorDiv.style.display = 'none';
            document.getElementById('start-screen').style.display = 'none';
            document.getElementById('exam-screen').style.display = 'block';
            
            document.getElementById('display-student-name').innerText = nameInput;
            document.getElementById('display-student-id').innerText = idInput;

            timerInterval = setInterval(updateTimer, 1000);
        } else {
            errorDiv.innerText = "❌ ভুল ইউজার আইডি অথবা পাসওয়ার্ড! সঠিক তথ্য দিয়ে আবার চেষ্টা করুন।";
            errorDiv.style.display = 'block';
        }
    }

    // টাইমার ফাংশন
    function updateTimer() {
        let minutes = Math.floor(totalTime / 60);
        let seconds = totalTime % 60;

        seconds = seconds < 10 ? '0' + seconds : seconds;
        minutes = minutes < 10 ? '0' + minutes : minutes;

        document.getElementById('timer').innerText = minutes + ":" + seconds;

        if (totalTime <= 0) {
            clearInterval(timerInterval);
            alert("সময় শেষ! উত্তরপত্রটি স্বয়ংক্রিয়ভাবে জমা নেওয়া হলো।");
            submitExam();
        }
        totalTime--;
    }

    // সাবমিট এবং গুগল শিটে ডেটা পাঠানোর ফাংশন
    function submitExam() {
        clearInterval(timerInterval);
        document.getElementById('submit-btn').style.display = 'none';
        document.getElementById('sending-status').style.display = 'block';
        document.getElementById('timer').innerText = "00:00 (জমা দেওয়া হয়েছে)";

        const form = document.getElementById('quiz-form');
        let score = 0;

        const studentName = document.getElementById('student-name-input').value;
        const studentId = document.getElementById('student-id-input').value;

        // 🔒 সাবমিট হওয়ার সাথে সাথেই এই নির্দিষ্ট আইডিটিকে চিরতরে লক করে দেওয়া হলো
        localStorage.setItem("locked_" + studentId, "true");

        for (let qNum in correctAnswers) {
            const selectedOpt = form.elements[qNum].value;
            const correctOpt = correctAnswers[qNum];
            
            const questionCard = form.elements[qNum][0].closest('.question-card');
            const labels = questionCard.getElementsByClassName('option-label');

            for(let i=0; i<4; i++) {
                form.elements[qNum][i].disabled = true;
                if(form.elements[qNum][i].value === correctOpt) {
                    labels[i].classList.add('correct-ans');
                }
                if(selectedOpt === form.elements[qNum][i].value && selectedOpt !== correctOpt) {
                    labels[i].classList.add('wrong-ans');
                }
            }

            if (selectedOpt === correctOpt) {
                score++;
            }
            document.getElementById('exp-' + qNum).style.display = 'block';
        }

        // রেজাল্ট ডিসপ্লে
        document.getElementById('res-name').innerText = studentName;
        document.getElementById('res-id').innerText = studentId;
        document.getElementById('score').innerText = score;
        document.getElementById('result-screen').style.display = 'block';

        window.scrollTo({top: 0, behavior: 'smooth'});

        // গুগল শিটে ডেটা সাবমিট করার এপিআই কোড
        if (GOOGLE_SCRIPT_URL !== "YOUR_GOOGLE_WEB_APP_URL_HERE") {
            const formData = new FormData();
            formData.append("studentId", studentId);
            formData.append("studentName", studentName);
            formData.append("score", score);

            fetch(GOOGLE_SCRIPT_URL, {
                method: "POST",
                body: formData
            })
            .then(response => {
                document.getElementById('sending-status').innerText = "✅ রেজাল্ট সফলভাবে শিক্ষকের ডেটাবেসে জমা হয়েছে!";
                document.getElementById('sending-status').style.color = "green";
            })
            .catch(error => {
                document.getElementById('sending-status').innerText = "⚠️ নেটওয়ার্ক সমস্যার কারণে শিটে সেভ হতে পারেনি, তবে স্ক্রিনে দেখতে পাচ্ছেন।";
                document.getElementById('sending-status').style.color = "orange";
            });
        } else {
            document.getElementById('sending-status').innerText = "💡 গুগল স্ক্রিপ্ট লিঙ্ক সেট করা হয়নি, তাই লাইভ সেভ হলো না।";
            document.getElementById('sending-status').style.color = "orange";
        }
    }
</script>

</body>
</html>
