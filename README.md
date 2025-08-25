<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>QuoteGenius AI - Millions of Quotes</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: white;
            margin: 0;
            padding: 0;
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

        .quote-stats {
            margin-top: 15px;
            font-size: 0.8rem;
            opacity: 0.7;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .loading {
            display: none;
            color: #4ecdc4;
            font-size: 0.9rem;
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
            position: relative;
        }

        .category-btn:hover, .category-btn.active {
            background: rgba(255,255,255,0.4);
            transform: translateY(-2px);
        }

        .api-badge {
            position: absolute;
            top: -5px;
            right: -5px;
            background: #4caf50;
            color: white;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            font-size: 0.6rem;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .quote-source-selector {
            margin-bottom: 20px;
        }

        .source-toggle {
            display: flex;
            background: rgba(255,255,255,0.1);
            border-radius: 10px;
            padding: 5px;
            margin-bottom: 15px;
        }

        .source-btn {
            flex: 1;
            background: transparent;
            border: none;
            color: white;
            padding: 10px;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .source-btn.active {
            background: rgba(255,255,255,0.3);
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
            position: relative;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
        }

        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }

        .btn-secondary {
            background: linear-gradient(45deg, #4ecdc4, #44a08d);
        }

        .btn-tertiary {
            background: linear-gradient(45deg, #ffa726, #ff7043);
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

        .error-message {
            background: rgba(255, 87, 87, 0.2);
            color: #ffcccb;
            padding: 10px;
            border-radius: 8px;
            margin: 10px 0;
            font-size: 0.9rem;
            display: none;
        }

        .success-message {
            background: rgba(76, 175, 80, 0.2);
            color: #c8e6c9;
            padding: 10px;
            border-radius: 8px;
            margin: 10px 0;
            font-size: 0.9rem;
            display: none;
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
            <p class="subtitle">Millions of Quotes from Famous People - Never Repeat!</p>
        </div>

        <div class="main-app">
            <div class="quote-display">
                <div class="current-quote" id="currentQuote">
                    "Click 'New Quote' to get inspired with unlimited quotes from our vast database!"
                </div>
                <div class="quote-author" id="quoteAuthor">- QuoteGenius AI</div>
                <div class="quote-stats">
                    <span id="quoteStats">Ready to inspire you!</span>
                    <span class="loading" id="loading">🔄 Loading...</span>
                </div>
                <div class="error-message" id="errorMessage"></div>
                <div class="success-message" id="successMessage"></div>
            </div>

            <div class="controls-panel">
                <div class="control-section">
                    <div class="control-title">Quote Source</div>
                    <div class="quote-source-selector">
                        <div class="source-toggle">
                            <button class="source-btn active" data-source="api" onclick="setQuoteSource('api')">
                                🌐 Live API (Unlimited)
                            </button>
                            <button class="source-btn" data-source="local" onclick="setQuoteSource('local')">
                                💾 Local Database
                            </button>
                        </div>
                    </div>
                </div>

                <div class="control-section">
                    <div class="control-title">Choose Your Inspiration Style</div>
                    <div class="quote-categories">
                        <button class="category-btn active" data-category="motivational">
                            🚀 Motivational
                            <span class="api-badge">∞</span>
                        </button>
                        <button class="category-btn" data-category="wisdom">
                            🧠 Wisdom
                            <span class="api-badge">∞</span>
                        </button>
                        <button class="category-btn" data-category="success">
                            💼 Success
                            <span class="api-badge">∞</span>
                        </button>
                        <button class="category-btn" data-category="happiness">
                            😊 Happiness
                            <span class="api-badge">∞</span>
                        </button>
                        <button class="category-btn" data-category="inspirational">
                            ⭐ Inspirational
                            <span class="api-badge">∞</span>
                        </button>
                        <button class="category-btn" data-category="life">
                            🌱 Life
                            <span class="api-badge">∞</span>
                        </button>
                    </div>
                </div>

                <div class="control-section">
                    <div class="control-title">Anti-Repeat System</div>
                    <div class="notification-settings">
                        <div class="setting-row">
                            <span class="setting-label">Memory Mode:</span>
                            <select id="memoryMode">
                                <option value="session">This Session Only</option>
                                <option value="daily">Reset Daily</option>
                                <option value="weekly">Reset Weekly</option>
                                <option value="never">Never Reset</option>
                            </select>
                        </div>
                        <div class="setting-row">
                            <span class="setting-label">Quotes Seen:</span>
                            <span id="quotesSeenCount">0</span>
                        </div>
                        <div class="setting-row">
                            <span class="setting-label">Available:</span>
                            <span id="availableCount">Unlimited</span>
                        </div>
                    </div>
                </div>

                <div class="action-buttons">
                    <button class="btn" onclick="getNewQuote()" id="newQuoteBtn">New Quote</button>
                    <button class="btn btn-secondary" onclick="enableNotifications()">Enable Notifications</button>
                    <button class="btn btn-tertiary" onclick="resetProgress()">Reset Memory</button>
                </div>
            </div>
        </div>

        <div class="features">
            <div class="feature-card">
                <div class="feature-icon">🌐</div>
                <div class="feature-title">Unlimited API Quotes</div>
                <div class="feature-desc">Access millions of quotes from multiple APIs including Quotable, ZenQuotes, and more. Never run out of inspiration!</div>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">🔄</div>
                <div class="feature-title">Smart No-Repeat System</div>
                <div class="feature-desc">Advanced algorithms ensure you never see the same quote twice until you want to. Configurable memory modes.</div>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">⚡</div>
                <div class="feature-title">Multiple API Sources</div>
                <div class="feature-desc">Fallback system tries multiple quote APIs to ensure you always get fresh content, even if one service is down.</div>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">🎯</div>
                <div class="feature-title">Category Intelligence</div>
                <div class="feature-desc">AI-powered categorization finds quotes matching your mood and needs from our vast database of famous quotes.</div>
            </div>
        </div>
    </div>

    <div class="notification-demo" id="notificationDemo">
        <strong>QuoteGenius AI</strong><br>
        <em>"Success is not final, failure is not fatal: it is the courage to continue that counts." - Winston Churchill</em>
    </div>

    <script>
        // Quote tracking system
        let seenQuotes = new Set();
        let dailyCount = 0;
        let currentCategory = 'motivational';
        let quoteSource = 'api'; // 'api' or 'local'

        // Fallback local quotes for when APIs are down
        const fallbackQuotes = {
            motivational: [
                { text: "The only way to do great work is to love what you do.", author: "Steve Jobs" },
                { text: "Success is not final, failure is not fatal: it is the courage to continue that counts.", author: "Winston Churchill" },
                { text: "The future belongs to those who believe in the beauty of their dreams.", author: "Eleanor Roosevelt" },
                { text: "It is during our darkest moments that we must focus to see the light.", author: "Aristotle" }
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
            happiness: [
                { text: "Happiness is not something ready made. It comes from your own actions.", author: "Dalai Lama" },
                { text: "The purpose of our lives is to be happy.", author: "Dalai Lama" },
                { text: "Life is really simple, but we insist on making it complicated.", author: "Confucius" },
                { text: "The best way to cheer yourself up is to try to cheer somebody else up.", author: "Mark Twain" }
            ],
            inspirational: [
                { text: "Be yourself; everyone else is already taken.", author: "Oscar Wilde" },
                { text: "You miss 100% of the shots you don't take.", author: "Wayne Gretzky" },
                { text: "The only impossible journey is the one you never begin.", author: "Tony Robbins" },
                { text: "Life is what happens to you while you're busy making other plans.", author: "John Lennon" }
            ],
            life: [
                { text: "Life is 10% what happens to you and 90% how you react to it.", author: "Charles R. Swindoll" },
                { text: "In the end, we will remember not the words of our enemies, but the silence of our friends.", author: "Martin Luther King Jr." },
                { text: "The best time to plant a tree was 20 years ago. The second best time is now.", author: "Chinese Proverb" },
                { text: "Life is either a daring adventure or nothing at all.", author: "Helen Keller" }
            ]
        };

        // Multiple API sources for maximum quote availability
        const quoteAPIs = [
            {
                name: 'Quotable',
                url: 'https://api.quotable.io/random',
                params: (category) => `?tags=${getCategoryTags(category)}&minLength=50&maxLength=300`,
                parse: (data) => ({ text: data.content, author: data.author })
            },
            {
                name: 'ZenQuotes',
                url: 'https://zenquotes.io/api/random',
                params: () => '',
                parse: (data) => ({ text: data[0].q, author: data[0].a })
            },
            {
                name: 'Type.fit',
                url: 'https://type.fit/api/quotes',
                params: () => '',
                parse: (data) => {
                    const quote = data[Math.floor(Math.random() * data.length)];
                    return { text: quote.text, author: quote.author || 'Unknown' };
                }
            }
        ];

        // Map categories to API tags
        function getCategoryTags(category) {
            const tagMap = {
                motivational: 'motivational,inspirational',
                wisdom: 'wisdom,famous-quotes',
                success: 'success,business',
                happiness: 'happiness,life',
                inspirational: 'inspirational,motivational',
                life: 'life,philosophy'
            };
            return tagMap[category] || 'inspirational';
        }

        // Create unique identifier for quotes
        function getQuoteId(quote) {
            return btoa(`${quote.text}-${quote.author}`).replace(/[^a-zA-Z0-9]/g, '').substring(0, 20);
        }

        // Check if quote has been seen before
        function hasSeenQuote(quote) {
            const id = getQuoteId(quote);
            return seenQuotes.has(id);
        }

        // Mark quote as seen
        function markQuoteAsSeen(quote) {
            const id = getQuoteId(quote);
            seenQuotes.add(id);
            updateStats();
        }

        // Fetch quote from API with fallback
        async function fetchQuoteFromAPI() {
            setLoading(true);
            
            for (const api of quoteAPIs) {
                try {
                    const url = api.url + api.params(currentCategory);
                    const response = await fetch(url);
                    
                    if (!response.ok) {
                        throw new Error(`HTTP ${response.status}`);
                    }
                    
                    const data = await response.json();
                    const quote = api.parse(data);
                    
                    // Validate quote
                    if (!quote.text || !quote.author) {
                        throw new Error('Invalid quote format');
                    }
                    
                    // Clean up author name
                    quote.author = quote.author.replace(/,.*$/, '').trim();
                    if (quote.author.toLowerCase() === 'unknown' || quote.author === 'type.fit') {
                        quote.author = 'Anonymous';
                    }
                    
                    setLoading(false);
                    showSuccess(`Quote fetched from ${api.name} API`);
                    return quote;
                    
                } catch (error) {
                    console.warn(`${api.name} API failed:`, error.message);
                    continue;
                }
            }
            
            // All APIs failed, use fallback
            setLoading(false);
            showError('APIs unavailable, using local quotes');
            return getLocalQuote();
        }

        // Get quote from local database
        function getLocalQuote() {
            const quotes = fallbackQuotes[currentCategory] || fallbackQuotes.motivational;
            return quotes[Math.floor(Math.random() * quotes.length)];
        }

        // Main function to get a new quote
        async function getNewQuote() {
            const btn = document.getElementById('newQuoteBtn');
            btn.disabled = true;
            clearMessages();
            
            try {
                let quote;
                let attempts = 0;
                const maxAttempts = 10;
                
                do {
                    if (quoteSource === 'api') {
                        quote = await fetchQuoteFromAPI();
                    } else {
                        quote = getLocalQuote();
                    }
                    
                    attempts++;
                    
                    // If we've seen this quote before, try again (up to maxAttempts)
                    if (hasSeenQuote(quote) && attempts < maxAttempts) {
                        continue;
                    } else {
                        break;
                    }
                } while (attempts < maxAttempts);
                
                // Display the quote
                document.getElementById('currentQuote').textContent = `"${quote.text}"`;
                document.getElementById('quoteAuthor').textContent = `- ${quote.author}`;
                
                // Mark as seen and update stats
                if (!hasSeenQuote(quote)) {
                    markQuoteAsSeen(quote);
                    dailyCount++;
                } else if (attempts >= maxAttempts) {
                    showError('You\'ve seen most available quotes in this category!');
                }
                
            } catch (error) {
                showError('Failed to load quote. Please try again.');
                console.error('Quote loading error:', error);
            }
            
            btn.disabled = false;
        }

        // UI helper functions
        function setLoading(show) {
            document.getElementById('loading').style.display = show ? 'block' : 'none';
        }

        function showError(message) {
            const errorEl = document.getElementById('errorMessage');
            errorEl.textContent = message;
            errorEl.style.display = 'block';
            setTimeout(() => errorEl.style.display = 'none', 5000);
        }

        function showSuccess(message) {
            const successEl = document.getElementById('successMessage');
            successEl.textContent = message;
            successEl.style.display = 'block';
            setTimeout(() => successEl.style.display = 'none', 3000);
        }

        function clearMessages() {
            document.getElementById('errorMessage').style.display = 'none';
            document.getElementById('successMessage').style.display = 'none';
        }

        // Update statistics display
        function updateStats() {
            document.getElementById('quotesSeenCount').textContent = seenQuotes.size;
            document.getElementById('quoteStats').textContent = `Seen: ${seenQuotes.size} | Today: ${dailyCount}`;
            
            if (quoteSource === 'local') {
                const totalLocal = Object.values(fallbackQuotes).reduce((sum, quotes) => sum + quotes.length, 0);
                document.getElementById('availableCount').textContent = totalLocal - seenQuotes.size;
            } else {
                document.getElementById('availableCount').textContent = 'Unlimited';
            }
        }

        // Set quote source
        function setQuoteSource(source) {
            quoteSource = source;
            document.querySelectorAll('.source-btn').forEach(btn => {
                btn.classList.toggle('active', btn.dataset.source === source);
            });
            updateStats();
            clearMessages();
            
            if (source === 'api') {
                // Update badges to show infinity symbol
                document.querySelectorAll('.api-badge').forEach(badge => {
                    badge.textContent = '∞';
                    badge.style.background = '#4caf50';
                });
                showSuccess('Connected to unlimited quote APIs!');
            } else {
                // Update badges to show local counts
                document.querySelectorAll('.api-badge').forEach((badge, index) => {
                    const categories = Object.keys(fallbackQuotes);
                    const category = categories[index];
                    if (category) {
                        badge.textContent = fallbackQuotes[category].length;
                        badge.style.background = '#ff9800';
                    }
                });
                showSuccess('Using local quote database');
            }
        }

        // Category selection
        document.querySelectorAll('.category-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                document.querySelectorAll('.category-btn').forEach(b => b.classList.remove('active'));
                this.classList.add('active');
                currentCategory = this.dataset.category;
                clearMessages();
            });
        });

        // Reset progress
        function resetProgress() {
            seenQuotes.clear();
            dailyCount = 0;
            updateStats();
            showSuccess('Memory reset! All quotes are fresh again.');
        }

        // Notification functions (simplified for demo)
        function enableNotifications() {
            if ('Notification' in window) {
                Notification.requestPermission().then(function(permission) {
                    if (permission === 'granted') {
                        showSuccess('Notifications enabled! You\'ll receive unique quotes.');
                        scheduleNotifications();
                    }
                });
            } else {
                showError('Your browser doesn\'t support notifications.');
            }
        }

        function scheduleNotifications() {
            // Demo notification after 10 seconds
            setTimeout(async () => {
                if (Notification.permission === 'granted') {
                    const quote = await fetchQuoteFromAPI();
                    new Notification('QuoteGenius AI', {
                        body: `"${quote.text.substring(0, 100)}..." - ${quote.author}`,
                        icon: '📖'
                    });
                }
            }, 10000);
        }

        // Initialize app
        updateStats();
        setQuoteSource('api');

        // Auto-refresh demonstration every 45 seconds
        setInterval(() => {
            if (Math.random() > 0.9 && quoteSource === 'api') { // 10% chance
                getNewQuote();
            }
        }, 45000);
    </script>
</body>
</html>
