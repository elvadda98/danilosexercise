<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: English Expressions Part 5</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #ff9a9e 0%, #fad0c4 100%);
            min-height: 100vh;
            padding: 20px;
            color: #333;
        }

        .container {
            max-width: 1000px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><circle cx="20" cy="20" r="2" fill="rgba(255,255,255,0.1)"/><circle cx="80" cy="30" r="1.5" fill="rgba(255,255,255,0.1)"/><circle cx="40" cy="70" r="1" fill="rgba(255,255,255,0.1)"/><circle cx="90" cy="80" r="2.5" fill="rgba(255,255,255,0.1)"/></svg>');
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255, 154, 158, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #ff9a9e;
            box-shadow: 0 4px 15px rgba(255, 154, 158, 0.2);
        }

        .word-bank h3 {
            color: #ff9a9e;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(255, 154, 158, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(255, 154, 158, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #ff9a9e;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #ff9a9e;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #ff9a9e;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(255, 154, 158, 0.2);
        }

        .option.selected {
            background: #ff9a9e;
            color: white;
            border-color: #ff9a9e;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #ff9a9e;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #ff9a9e;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(255, 154, 158, 0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #ff9a9e;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(255, 154, 158, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255, 154, 158, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(255, 154, 158, 0.3);
            z-index: 1000;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/39</div>
    
    <div class="container">
        <div class="header">
            <h1>📚 English Expressions Game: Part 5</h1>
            <p>Test your knowledge of these useful English expressions!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Meanings</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section active">
            <div class="word-bank">
                <h3>📝 Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">reason</span>
                    <span class="word-option">working method</span>
                    <span class="word-option">concerns</span>
                    <span class="word-option">earnings</span>
                    <span class="word-option">few</span>
                    <span class="word-option">allow</span>
                    <span class="word-option">acquired</span>
                    <span class="word-option">appreciate</span>
                    <span class="word-option">role</span>
                    <span class="word-option">commute</span>
                    <span class="word-option">square</span>
                    <span class="word-option">usually</span>
                    <span class="word-option">especially</span>
                </div>
            </div>

            <div class="question">
                <h3>Question 1:</h3>
                <p>I really <input type="text" class="fill-blank" data-answer="appreciate" placeholder="answer"> your help with this difficult task.</p>
                <div class="feedback" id="feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2:</h3>
                <p>My daily <input type="text" class="fill-blank" data-answer="commute" placeholder="answer"> to work takes about 30 minutes each way.</p>
                <div class="feedback" id="feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3:</h3>
                <p>Very <input type="text" class="fill-blank" data-answer="few" placeholder="answer"> people understand the complexity of this issue.</p>
                <div class="feedback" id="feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4:</h3>
                <p>I <input type="text" class="fill-blank" data-answer="usually" placeholder="answer"> have coffee first thing in the morning.</p>
                <div class="feedback" id="feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5:</h3>
                <p>His monthly <input type="text" class="fill-blank" data-answer="earnings" placeholder="answer"> have increased since he got promoted.</p>
                <div class="feedback" id="feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6:</h3>
                <p>She has <input type="text" class="fill-blank" data-answer="acquired" placeholder="answer"> valuable skills through years of experience.</p>
                <div class="feedback" id="feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7:</h3>
                <p>My main <input type="text" class="fill-blank" data-answer="concerns" placeholder="answer"> about the project are the timeline and budget.</p>
                <div class="feedback" id="feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8:</h3>
                <p>There's no <input type="text" class="fill-blank" data-answer="reason" placeholder="answer"> to be upset; everything is fine.</p>
                <div class="feedback" id="feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 9:</h3>
                <p>Please <input type="text" class="fill-blank" data-answer="allow" placeholder="answer"> me to explain the situation before you make a decision.</p>
                <div class="feedback" id="feedback-9" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 10:</h3>
                <p>Her efficient <input type="text" class="fill-blank" data-answer="working method" placeholder="answer"> helps her complete tasks quickly.</p>
                <div class="feedback" id="feedback-10" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 11:</h3>
                <p>I love all fruits, <input type="text" class="fill-blank" data-answer="especially" placeholder="answer"> mangoes and strawberries.</p>
                <div class="feedback" id="feedback-11" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 12:</h3>
                <p>His <input type="text" class="fill-blank" data-answer="role" placeholder="answer"> in the company is to manage the marketing department.</p>
                <div class="feedback" id="feedback-12" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 13:</h3>
                <p>The town <input type="text" class="fill-blank" data-answer="square" placeholder="answer"> is where people gather for festivals and events.</p>
                <div class="feedback" id="feedback-13" style="display: none;"></div>
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #ff9a9e;">Match the expressions with their meanings</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Words</h4>
                    <div class="match-item" data-word="reason" onclick="selectMatch(this)">reason</div>
                    <div class="match-item" data-word="working method" onclick="selectMatch(this)">working method</div>
                    <div class="match-item" data-word="concerns" onclick="selectMatch(this)">concerns</div>
                    <div class="match-item" data-word="earnings" onclick="selectMatch(this)">earnings</div>
                    <div class="match-item" data-word="few" onclick="selectMatch(this)">few</div>
                    <div class="match-item" data-word="allow" onclick="selectMatch(this)">allow</div>
                    <div class="match-item" data-word="acquired" onclick="selectMatch(this)">acquired</div>
                    <div class="match-item" data-word="appreciate" onclick="selectMatch(this)">appreciate</div>
                    <div class="match-item" data-word="role" onclick="selectMatch(this)">role</div>
                    <div class="match-item" data-word="commute" onclick="selectMatch(this)">commute</div>
                    <div class="match-item" data-word="square" onclick="selectMatch(this)">square</div>
                    <div class="match-item" data-word="usually" onclick="selectMatch(this)">usually</div>
                    <div class="match-item" data-word="especially" onclick="selectMatch(this)">especially</div>
                </div>
                <div class="match-column">
                    <h4>Meanings</h4>
                    <div class="match-item" data-meaning="few" onclick="selectMatch(this)">A small number of; not many</div>
                    <div class="match-item" data-meaning="acquired" onclick="selectMatch(this)">Gained through one's efforts or actions</div>
                    <div class="match-item" data-meaning="role" onclick="selectMatch(this)">A function or position that someone has in a situation</div>
                    <div class="match-item" data-meaning="working method" onclick="selectMatch(this)">A systematic way of approaching tasks and problems</div>
                    <div class="match-item" data-meaning="reason" onclick="selectMatch(this)">A cause, explanation, or justification for an action or event</div>
                    <div class="match-item" data-meaning="commute" onclick="selectMatch(this)">To travel some distance between one's home and place of work regularly</div>
                    <div class="match-item" data-meaning="square" onclick="selectMatch(this)">An open area in a town or city, often used for public gatherings</div>
                    <div class="match-item" data-meaning="allow" onclick="selectMatch(this)">To give permission for something; to permit</div>
                    <div class="match-item" data-meaning="appreciate" onclick="selectMatch(this)">To recognize the value or significance of; to be grateful for</div>
                    <div class="match-item" data-meaning="usually" onclick="selectMatch(this)">Under normal conditions; generally</div>
                    <div class="match-item" data-meaning="especially" onclick="selectMatch(this)">To a great extent; particularly; notably more than other things</div>
                    <div class="match-item" data-meaning="earnings" onclick="selectMatch(this)">Money obtained in return for labor or services</div>
                    <div class="match-item" data-meaning="concerns" onclick="selectMatch(this)">Worries or anxieties about something</div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "reason" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A season of the year</div>
                    <div class="option" onclick="selectOption(this, true)">A cause, explanation, or justification for something</div>
                    <div class="option" onclick="selectOption(this, false)">A type of measurement</div>
                    <div class="option" onclick="selectOption(this, false)">A mathematical calculation</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: "Working method" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A job that involves physical labor</div>
                    <div class="option" onclick="selectOption(this, true)">A systematic way of approaching tasks and problems</div>
                    <div class="option" onclick="selectOption(this, false)">A method for finding employment</div>
                    <div class="option" onclick="selectOption(this, false)">A technique for working with tools</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: "Concerns" refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Business organizations</div>
                    <div class="option" onclick="selectOption(this, true)">Worries or anxieties about something</div>
                    <div class="option" onclick="selectOption(this, false)">Musical performances</div>
                    <div class="option" onclick="selectOption(this, false)">Important meetings</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: "Earnings" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Things learned through experience</div>
                    <div class="option" onclick="selectOption(this, true)">Money obtained in return for labor or services</div>
                    <div class="option" onclick="selectOption(this, false)">Parts of the body used for hearing</div>
                    <div class="option" onclick="selectOption(this, false)">Agricultural products</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: "Few" refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A large number</div>
                    <div class="option" onclick="selectOption(this, true)">A small number; not many</div>
                    <div class="option" onclick="selectOption(this, false)">Exactly three</div>
                    <div class="option" onclick="selectOption(this, false)">An unlimited amount</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: "Allow" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To disagree with something</div>
                    <div class="option" onclick="selectOption(this, true)">To give permission for something; to permit</div>
                    <div class="option" onclick="selectOption(this, false)">To lower in value</div>
                    <div class="option" onclick="selectOption(this, false)">To speak loudly</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7: "Acquired" refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Naturally possessed from birth</div>
                    <div class="option" onclick="selectOption(this, true)">Gained through one's efforts or actions</div>
                    <div class="option" onclick="selectOption(this, false)">Lost or misplaced</div>
                    <div class="option" onclick="selectOption(this, false)">Given away freely</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8: "Appreciate" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To decrease in value</div>
                    <div class="option" onclick="selectOption(this, true)">To recognize the value of; to be grateful for</div>
                    <div class="option" onclick="selectOption(this, false)">To criticize harshly</div>
                    <div class="option" onclick="selectOption(this, false)">To estimate roughly</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 9: "Role" refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of bread</div>
                    <div class="option" onclick="selectOption(this, true)">A function or position that someone has</div>
                    <div class="option" onclick="selectOption(this, false)">A list of names</div>
                    <div class="option" onclick="selectOption(this, false)">A part of a machine</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 10: "Commute" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To reduce a judicial sentence</div>
                    <div class="option" onclick="selectOption(this, true)">To travel regularly between home and workplace</div>
                    <div class="option" onclick="selectOption(this, false)">To change electrical current</div>
                    <div class="option" onclick="selectOption(this, false)">To communicate effectively</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 11: "Square" refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A circular shape</div>
                    <div class="option" onclick="selectOption(this, true)">An open area in a town or city for public gatherings</div>
                    <div class="option" onclick="selectOption(this, false)">A unit of measurement for distance</div>
                    <div class="option" onclick="selectOption(this, false)">A type of dance</div>
                </div>
                <div class="feedback" id="mc-feedback-11" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 12: "Usually" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Rarely or infrequently</div>
                    <div class="option" onclick="selectOption(this, true)">Under normal conditions; generally</div>
                    <div class="option" onclick="selectOption(this, false)">In a useful manner</div>
                    <div class="option" onclick="selectOption(this, false)">Specifically or particularly</div>
                </div>
                <div class="feedback" id="mc-feedback-12" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 13: "Especially" refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">In a special manner</div>
                    <div class="option" onclick="selectOption(this, true)">To a great extent; particularly; notably more than other things</div>
                    <div class="option" onclick="selectOption(this, false)">In a speculative way</div>
                    <div class="option" onclick="selectOption(this, false)">For a special occasion</div>
                </div>
                <div class="feedback" id="mc-feedback-13" style="display: none;"></div>
            </div>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === 13) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            updateScore();
        }

        function updateScore() {
            // Calculate score for fill-in-the-blank
            let fillScore = 0;
            document.querySelectorAll('.fill-blank.correct').forEach(blank => {
                if (!blank.classList.contains('counted')) {
                    fillScore++;
                    blank.classList.add('counted');
                }
            });
            
            // Calculate score for matching (each pair is 1 point)
            const matchScore = matchedPairs.length;
            
            // Calculate score for multiple choice (each correct is 1 point)
            let mcScore = 0;
            document.querySelectorAll('.option.correct.selected').forEach(opt => {
                mcScore++;
            });
            
            // Total score
            score = fillScore + matchScore + mcScore;
            document.getElementById('score').textContent = score;
        }
    </script>
</body>
</html>
