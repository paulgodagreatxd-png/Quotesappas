# Quotesappas
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>QuoteGenius AI - Your Personal Inspiration Assistant</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: white;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
            padding: 40px 0;
        }

        .app-title {
            font-size: 3.5rem;
            font-weight: bold;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
            background: linear-gradient(45deg, #fff, #f0f8ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .subtitle {
            font-size: 1.3rem;
            opacity: 0.9;
            margin-bottom: 30px;
        }

        .main-app {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 40px;
        }

        .quote-display {
            background: rgba(255,255,255,0.15);
            padding: 40px;
            border-radius: 20px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,255,255,0.2);
            text-align: center;
            min-height: 300px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .current-quote {
            font-size: 1.4rem;
            line-height: 1.6;
            margin-bottom: 20px;
            font-style: italic;
        }

        .quote-author {
            font-size: 1rem;
            opacity: 0.8;
            margin-top: 15px;
        }

        .controls-panel {
            background: rgba(255,255,255,0.15);
            padding: 30px;
            border-radius: 20px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,255,255,0.2);
        }

        .control-section {
            margin-bottom: 30px;
        }

        .control-title {
            font-size: 1.2rem;
            font-weight: bold;
            margin-bottom: 15px;
            color: #fff;
        }

        .quote-categories {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 20px;
        }

        .category-btn {
            background: rgba(255,255,255,0.2);
            border: none;
            padding: 12px 16px;
            border-radius: 10px;
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 0.9rem;
        }

        .category-btn:hover, .category-btn.active {
            background: rgba(255,255,255,0.4);
            transform: translateY(-2px);
        }

        .notification-settings {
            background: rgba(255,255,255,0.1);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
        }

        .setting-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .setting-label {
            font-size: 0.9rem;
        }

        select, input {
            background: rgba(255,255,255,0.2);
            border: 1px solid rgba(255,255,255,0.3);
            border-radius: 8px;
            padding: 8px 12px;
            color: white;
            font-size: 0.9rem;
        }

        select option {
            background: #764ba2;
            color: white;
        }

        .action-buttons {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-top: 20px;
        }

        .btn {
            background: linear-gradient(45deg, #ff6b6b, #ee5a52);
            border: none;
            padding: 15px 25px;
            border-radius: 12px;
            color: white;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1rem;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
        }

        .btn-secondary {
            background: linear-gradient(45deg, #4ecdc4, #44a08d);
        }

        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-top: 40px;
        }

        .feature-card {
            background: rgba(255,255,255,0.1);
            padding: 25px;
            border-radius: 15px;
            text-align: center;
            border: 1px solid rgba(255,255,255,0.2);
        }

        .feature-icon {
            font-size: 3rem;
            margin-bottom: 15px;
        }

        .feature-title {
            font-size: 1.3rem;
            font-weight: bold;
            margin-bottom: 10px;
        }

        .feature-desc {
            font-size: 0.9rem;
            opacity: 0.8;
            line-height: 1.5;
        }

        .notification-demo {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(0,0,0,0.9);
            color: white;
            padding: 20px;
            border-radius: 15px;
            max-width: 350px;
            opacity: 0;
            transform: translateX(400px);
            transition: all 0.5s ease;
            border-left: 4px solid #4ecdc4;
        }

        .notification-demo.show {
            opacity: 1;
            transform: translateX(0);
        }

        @media (max-width: 768px) {
            .main-app {
                grid-template-columns: 1fr;
            }
            
            .app-title {
                font-size: 2.5rem;
            }
            
            .quote-categories {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1 class="app-title">QuoteGenius AI</h1>
            <p class="subtitle">Your Personal AI-Powered Inspiration Assistant</p>
        </div>

        <div class="main-app">
            <div class="quote-display">
                <div class="current-quote" id="currentQuote">
                    "The only way to do great work is to love what you do. If you haven't found it yet, keep looking. Don't settle."
                </div>
                <div class="quote-author" id="quoteAuthor">- Steve Jobs</div>
            </div>

            <div class="controls-panel">
                <div class="control-section">
                    <div class="control-title">Choose Your Inspiration Style</div>
                    <div class="quote-categories">
                        <button class="category-btn active" data-category="motivational">🚀 Motivational</button>
                        <button class="category-btn" data-category="funny">😂 Funny</button>
                        <button class="category-btn" data-category="wisdom">🧠 Wisdom</button>
                        <button class="category-btn" data-category="success">💼 Success</button>
                        <button class="category-btn" data-category="love">❤️ Love & Life</button>
                        <button class="category-btn" data-category="creative">🎨 Creative</button>
                    </div>
                </div>

                <div class="control-section">
                    <div class="control-title">Notification Settings</div>
                    <div class="notification-settings">
                        <div class="setting-row">
                            <span class="setting-label">Frequency:</span>
                            <select id="frequency">
                                <option value="hourly">Every Hour</option>
                                <option value="daily" selected>Daily</option>
                                <option value="weekly">Weekly</option>
                                <option value="custom">Custom</option>
                            </select>
                        </div>
                        <div class="setting-row">
                            <span class="setting-label">Best Time:</span>
                            <input type="time" id="bestTime" value="08:00">
                        </div>
                        <div class="setting-row">
                            <span class="setting-label">Mood Matching:</span>
                            <select id="moodMatching">
                                <option value="auto">Auto-Detect</option>
                                <option value="happy">Always Uplifting</option>
                                <option value="calm">Peaceful & Calm</option>
                                <option value="energetic">High Energy</option>
                            </select>
                        </div>
                    </div>
                </div>

                <div class="action-buttons">
                    <button class="btn" onclick="getNewQuote()">New Quote</button>
                    <button class="btn btn-secondary" onclick="enableNotifications()">Enable Notifications</button>
                </div>
            </div>
        </div>

        <div class="features">
            <div class="feature-card">
                <div class="feature-icon">🤖</div>
                <div class="feature-title">AI-Powered Selection</div>
                <div class="feature-desc">Advanced AI analyzes your preferences, mood, and time of day to deliver perfectly timed inspiration</div>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">📱</div>
                <div class="feature-title">Smart Notifications</div>
                <div class="feature-desc">Receive quotes when you need them most - during breaks, stressful moments, or your optimal motivation times</div>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">🎯</div>
                <div class="feature-title">Personalized Content</div>
                <div class="feature-desc">Choose from motivational, funny, wisdom, success, love, or creative quotes. AI learns your favorites over time</div>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">📊</div>
                <div class="feature-title">Mood Analytics</div>
                <div class="feature-desc">Track your inspiration patterns and see how different quote types affect your daily motivation levels</div>
            </div>
        </div>
    </div>

    <div class="notification-demo" id="notificationDemo">
        <strong>QuoteGenius AI</strong><br>
        <em>"Success is not final, failure is not fatal: it is the courage to continue that counts." - Winston Churchill</em>
    </div>

    <script>
        const quotes = {
            motivational: [
                { text: "The only way to do great work is to love what you do. If you haven't found it yet, keep looking. Don't settle.", author: "Steve Jobs" },
                { text: "Success is not final, failure is not fatal: it is the courage to continue that counts.", author: "Winston Churchill" },
                { text: "The future belongs to those who believe in the beauty of their dreams.", author: "Eleanor Roosevelt" },
                { text: "It is during our darkest moments that we must focus to see the light.", author: "Aristotle" }
            ],
            funny: [
                { text: "I haven't failed. I've just found 10,000 ways that won't work.", author: "Thomas Edison" },
                { text: "The trouble with having an open mind, of course, is that people will insist on coming along and trying to put things in it.", author: "Terry Pratchett" },
                { text: "I'm not superstitious, but I am a little stitious.", author: "Michael Scott" },
                { text: "Behind every great man is a woman rolling her eyes.", author: "Jim Carrey" }
            ],
            wisdom: [
                { text: "The only true wisdom is in knowing you know nothing.", author: "Socrates" },
                { text: "In the middle of difficulty lies opportunity.", author: "Albert Einstein" },
                { text: "The journey of a thousand miles begins with one step.", author: "Lao Tzu" },
                { text: "Yesterday is history, tomorrow is a mystery, today is a gift.", author: "Eleanor Roosevelt" }
            ],
            success: [
                { text: "Success is walking from failure to failure with no loss of enthusiasm.", author: "Winston Churchill" },
                { text: "The way to get started is to quit talking and begin doing.", author: "Walt Disney" },
                { text: "Don't be afraid to give up the good to go for the great.", author: "John D. Rockefeller" },
                { text: "Innovation distinguishes between a leader and a follower.", author: "Steve Jobs" }
            ],
            love: [
                { text: "Life is what happens to you while you're busy making other plans.", author: "John Lennon" },
                { text: "The best time to plant a tree was 20 years ago. The second best time is now.", author: "Chinese Proverb" },
                { text: "Be yourself; everyone else is already taken.", author: "Oscar Wilde" },
                { text: "Life is really simple, but we insist on making it complicated.", author: "Confucius" }
            ],
            creative: [
                { text: "Creativity is intelligence having fun.", author: "Albert Einstein" },
                { text: "The secret to creativity is knowing how to hide your sources.", author: "Pablo Picasso" },
                { text: "You can't use up creativity. The more you use, the more you have.", author: "Maya Angelou" },
                { text: "Imagination is more important than knowledge.", author: "Albert Einstein" }
            ]
        };

        let currentCategory = 'motivational';

        // Category selection
        document.querySelectorAll('.category-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                document.querySelectorAll('.category-btn').forEach(b => b.classList.remove('active'));
                this.classList.add('active');
                currentCategory = this.dataset.category;
                getNewQuote();
            });
        });

        function getNewQuote() {
            const categoryQuotes = quotes[currentCategory];
            const randomQuote = categoryQuotes[Math.floor(Math.random() * categoryQuotes.length)];
            
            document.getElementById('currentQuote').textContent = `"${randomQuote.text}"`;
            document.getElementById('quoteAuthor').textContent = `- ${randomQuote.author}`;
        }

        function enableNotifications() {
            if ('Notification' in window) {
                Notification.requestPermission().then(function(permission) {
                    if (permission === 'granted') {
                        showNotificationDemo();
                        alert('Notifications enabled! You\'ll receive inspiring quotes based on your settings.');
                        // In a real app, this would set up scheduled notifications
                        scheduleNotifications();
                    }
                });
            } else {
                alert('Your browser doesn\'t support notifications, but the app will still work great!');
            }
        }

        function showNotificationDemo() {
            const demo = document.getElementById('notificationDemo');
            demo.classList.add('show');
            setTimeout(() => {
                demo.classList.remove('show');
            }, 4000);
        }

        function scheduleNotifications() {
            // Simulate AI-powered notification scheduling
            const frequency = document.getElementById('frequency').value;
            const time = document.getElementById('bestTime').value;
            const mood = document.getElementById('moodMatching').value;
            
            console.log(`AI will send ${currentCategory} quotes ${frequency} at ${time} with ${mood} mood matching`);
            
            // In a real app, this would use service workers for background notifications
            setTimeout(() => {
                if (Notification.permission === 'granted') {
                    const randomQuote = quotes[currentCategory][Math.floor(Math.random() * quotes[currentCategory].length)];
                    new Notification('QuoteGenius AI', {
                        body: `"${randomQuote.text}" - ${randomQuote.author}`,
                        icon: '📖'
                    });
                }
            }, 10000); // Demo notification after 10 seconds
        }

        // Auto-generate a new quote every 15 seconds for demo
        setInterval(() => {
            if (Math.random() > 0.7) { // 30% chance every 15 seconds
                getNewQuote();
            }
        }, 15000);
    </script>
</body>
</html>


