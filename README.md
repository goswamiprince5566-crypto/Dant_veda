<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>Dant-Veda Official Store</title>
    <style>
        /* SMOOTH SCROLLING */
        html { scroll-behavior: smooth; }

        /* DESIGN STYLES */
        body { margin: 0; padding: 0; font-family: 'Segoe UI', sans-serif; background-color: #f4f9f4; color: #333; padding-bottom: 60px; overflow-x: hidden; }
        
        /* --- 1. STARTING INTRO --- */
        #splash-screen {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: #0b4d2e; z-index: 9999;
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            transition: opacity 0.8s ease-out;
        }
        .splash-logo { font-size: 50px; color: white; font-weight: bold; animation: popIn 1s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
        .splash-tagline { color: #a3d9a5; margin-top: 10px; font-size: 16px; letter-spacing: 2px; animation: fadeIn 2s ease; }
        .loading-bar-container { width: 200px; height: 5px; background: rgba(255,255,255,0.2); margin-top: 30px; border-radius: 5px; overflow: hidden; }
        .loading-bar-fill { height: 100%; background: #ff9800; width: 0%; animation: fillBar 2.5s linear forwards; }
        @keyframes popIn { 0% { transform: scale(0); opacity: 0; } 100% { transform: scale(1); opacity: 1; } }
        @keyframes fadeIn { 0% { opacity: 0; } 100% { opacity: 1; } }
        @keyframes fillBar { 0% { width: 0%; } 100% { width: 100%; } }

        /* --- 2. SCROLL PROGRESS BAR --- */
        .progress-container { width: 100%; height: 5px; background: #ccc; position: fixed; top: 0; z-index: 2000; }
        .progress-bar { height: 5px; background: #ff416c; width: 0%; transition: width 0.1s; }

        /* --- 3. NEWS TICKER --- */
        .news-ticker { background: #222; color: #fff; padding: 8px; white-space: nowrap; overflow: hidden; font-size: 13px; letter-spacing: 1px; margin-top: 5px; }
        .news-content { display: inline-block; padding-left: 100%; animation: scrollText 15s linear infinite; }
        @keyframes scrollText { 0% { transform: translateX(0); } 100% { transform: translateX(-100%); } }

        /* --- 4. BACK TO TOP BUTTON --- */
        #myBtn { display: none; position: fixed; bottom: 80px; right: 20px; z-index: 99; font-size: 18px; border: none; outline: none; background-color: #0b4d2e; color: white; cursor: pointer; padding: 12px; border-radius: 6px; }
        #myBtn:hover { background-color: #555; }

        /* --- 5. SEARCH BAR STYLES (NEW) --- */
        .search-container { margin-top: 15px; display: flex; justify-content: center; gap: 5px; }
        .search-input { padding: 10px; width: 250px; border-radius: 20px; border: 1px solid #ccc; outline: none; font-size: 14px; box-shadow: inset 2px 2px 5px rgba(0,0,0,0.1); }
        .search-btn { background: orange; border: none; padding: 8px 15px; border-radius: 20px; cursor: pointer; font-weight: bold; color: white; }

        /* QUIZ */
        .quiz-box { background: white; padding: 20px; border-radius: 10px; max-width: 400px; margin: 20px auto; border: 2px solid #0b4d2e; box-shadow: 0 5px 15px rgba(0,0,0,0.1); }
        .quiz-question { font-weight: bold; font-size: 18px; margin-bottom: 15px; color: #333; }
        .quiz-btn { padding: 10px 20px; border: none; border-radius: 5px; cursor: pointer; font-weight: bold; margin: 5px; transition: 0.3s; }
        .btn-yes { background: #4caf50; color: white; }
        .btn-no { background: #f44336; color: white; }
        .quiz-result { margin-top: 10px; font-weight: bold; font-size: 14px; min-height: 20px; }

        /* HEADER & HERO */
        .header { background-color: #0b4d2e; color: white; padding: 15px; text-align: center; position: sticky; top: 5px; z-index: 1000; box-shadow: 0 4px 6px rgba(0,0,0,0.1); }
        .nav { background: #333; overflow: hidden; display: flex; justify-content: center; margin-top: 10px; border-radius: 5px; }
        .nav a { color: white; padding: 10px 15px; text-decoration: none; display: block; font-size: 14px; }
        
        .section { padding: 40px 20px; border-bottom: 1px solid #ddd; text-align: center; }
        
        #home { background-color: #e8f5e9; position: relative; }
        .hero-box { width: 90%; height: 250px; background-color: #cccccc; margin: 20px auto; border: 2px dashed #000; position: relative; display: flex; align-items: center; justify-content: center; }
        
        .stamp-box { position: absolute; top: -10px; right: -10px; background: #d32f2f; color: white; padding: 10px 20px; font-weight: bold; font-size: 14px; border-radius: 50px; border: 2px solid white; transform: rotate(20deg); animation: stampIn 0.8s ease; }
        @keyframes stampIn { 0% { transform: rotate(20deg) scale(3); opacity: 0; } 80% { transform: rotate(20deg) scale(0.9); opacity: 1; } 100% { transform: rotate(20deg) scale(1); opacity: 1; } }

        /* SHOP, TABLE, MISSION */
        #shop { background: #fcfcfc; }
        .product-list { display: flex; flex-wrap: wrap; justify-content: center; gap: 15px; margin-top: 20px; }
        .card { background: white; border: 1px solid #ddd; width: 45%; padding: 10px; border-radius: 8px; position: relative; box-shadow: 0 2px 5px rgba(0,0,0,0.1); transition: transform 0.3s; }
        .card:hover { transform: translateY(-5px); border: 1px solid #0b4d2e; }
        .prod-badge { position: absolute; top: 5px; left: 5px; background: #0b4d2e; color: white; font-size: 10px; padding: 3px 8px; border-radius: 5px; font-weight: bold; z-index: 5; }
        .prod-img-box { width: 100%; height: 80px; background: #ddd; margin-bottom: 10px; border: 1px dashed #666; display: flex; align-items: center; justify-content: center; }
        .order-btn { background: #25D366; color: white; padding: 10px; text-decoration: none; border-radius: 4px; display: block; margin-top: 5px; cursor: pointer; border: none; width: 100%; font-weight: bold; }

        #compare { background: white; }
        .comp-table { width: 100%; max-width: 500px; margin: 20px auto; border-collapse: collapse; box-shadow: 0 4px 10px rgba(0,0,0,0.1); }
        .comp-table th, .comp-table td { border: 1px solid #ddd; padding: 12px; text-align: center; }
        .comp-table th { background-color: #0b4d2e; color: white; }
        .check { color: green; font-weight: bold; font-size: 18px; }
        .cross { color: red; font-weight: bold; font-size: 18px; }

        #mission { background: #dff0d8; }
        #donate { background: #fff3e0; }
        .donate-container { background: white; border: 2px dashed #0b4d2e; padding: 20px; border-radius: 15px; width: 90%; max-width: 300px; margin: 0 auto; box-shadow: 0 5px 15px rgba(0,0,0,0.1); }
        .pay-btn { background: orange; color: white; padding: 12px; text-decoration: none; border-radius: 5px; font-weight: bold; display: block; margin-top: 15px; text-align: center; }

        .social-box { width: 90%; height: 180px; background-color: #a3d9a5; margin: 20px auto; border: 2px dashed #0b4d2e; display: flex; align-items: center; justify-content: center; overflow: hidden; }

        #contact { background: #333; color: white; }
        input, textarea { width: 90%; padding: 10px; margin: 5px 0; border-radius: 5px; border: none; }
        .submit-btn { background: orange; color: white; padding: 10px; border: none; border-radius: 5px; cursor: pointer; width: 100%; font-weight: bold; }
        .footer { background: black; color: white; text-align: center; padding: 10px; font-size: 12px; margin-bottom: 50px;}
        .btn { background: #0b4d2e; color: white; padding: 8px; text-decoration: none; border-radius: 4px; display: block; margin-top: 5px; cursor: pointer; border: none; width: 100%; font-size: 14px; }

        .offer-bar { position: fixed; bottom: 0; left: 0; width: 100%; background: linear-gradient(45deg, #ff416c, #ff4b2b); color: white; text-align: center; padding: 12px; font-weight: bold; font-size: 16px; cursor: pointer; animation: slideUp 0.4s ease forwards; z-index: 1000; }
        @keyframes slideUp { from { bottom: -60px; } to { bottom: 0; } }

        .confetti { position: fixed; top: -10px; width: 10px; height: 10px; z-index: 9999; animation: fall linear forwards; border-radius: 2px; }
        @keyframes fall { to { transform: translateY(100vh) rotate(720deg); } }

    </style>
</head>
<body>

    <div id="splash-screen">
        <div class="splash-logo">🌿 DANT-VEDA</div>
        <div class="splash-tagline">NATURE'S BEST CARE</div>
        <div class="loading-bar-container">
            <div class="loading-bar-fill"></div>
        </div>
    </div>

    <div class="progress-container">
        <div class="progress-bar" id="myBar"></div>
    </div>

    <button onclick="topFunction()" id="myBtn" title="Go to top">⬆</button>

    <div class="news-ticker">
        <div class="news-content">
            📢 Welcome to Dant-Veda! 🌿 India's #1 Herbal Toothpaste. 🚚 Free Shipping on orders above Rs. 100! 📞 Call us: 1800-111-222
        </div>
    </div>

    <div class="header">
        <h1>🌿 DANT-VEDA</h1>
        
        <div class="search-container">
            <input type="text" id="searchInput" class="search-input" onkeyup="searchProducts()" placeholder="🔍 Search product (e.g. Mini)...">
        </div>

        <div class="nav">
            <a href="#home">Home</a>
            <a href="#shop">Shop</a>
            <a href="#quiz">Quiz</a>
            <a href="#contact">Contact</a>
        </div>
    </div>

    <div id="home" class="section">
        <h2 style="color: #0b4d2e; font-size: 24px;">INDIA'S #1 <span style="background:orange; color:white; padding:0 5px;">CHEMICAL FREE</span> TOOTHPASTE</h2>
        <p style="font-weight: bold;">🚫 No Chemicals. Only Nature. 🌱</p>
        
        <div class="hero-box">
            <div class="stamp-box">100%<br>SAFE</div>
            <img src="imagee7.png" style="width: 287px; height: 249px; object-fit: cover;" alt="Hero Image"> 
        </div>
        
        <br>
        <button class="btn" style="background:orange; width: 70%; margin: 0 auto; font-weight:bold;" onclick="window.location.href='#shop'">BUY NOW (100% HERBAL) 👇</button>
    </div>

    <div id="shop" class="section">
        <h2 style="color:#0b4d2e;">🔥 BEST SELLERS</h2>
        <div class="product-list">
            <div class="card">
                <div class="prod-badge">🚫 0% Chemical</div>
                <div class="prod-img-box"><img src="imagee1.png" style="width: 100%; height: 100%; object-fit: contain;" alt="Mini Pack"></div>
                <h4>Mini Pack</h4>
                <p><b>Rs. 30</b></p>
                <button class="order-btn" onclick="magicButton('Mini Pack', 30)">ORDER NOW 💬</button>
            </div>
            <div class="card" style="border: 2px solid orange;">
                <div class="prod-badge">🌿 Pure Herbal</div>
                <div class="prod-img-box"><img src="imagee2.png" style="width: 100%; height: 100%; object-fit: contain;" alt="Std Pack"></div>
                <h4>Std. Pack</h4>
                <p><b>Rs. 55</b></p>
                <button class="order-btn" onclick="magicButton('Standard Pack', 55)">ORDER NOW 💬</button>
            </div>
            <div class="card">
                <div class="prod-badge">✅ Kid Safe</div>
                <div class="prod-img-box"><img src="imagee4.png" style="width: 100%; height: 100%; object-fit: contain;" alt="Family Pack"></div>
                <h4>Family Pack</h4>
                <p><b>Rs. 100</b></p>
                <button class="order-btn" onclick="magicButton('Family Pack', 100)">ORDER NOW 💬</button>
            </div>
        </div>
        <p id="no-result" style="display:none; color:red; margin-top:20px;">No Product Found!</p>
    </div>

    <div id="quiz" class="section" style="background: #e8f5e9;">
        <h2 style="color: #0b4d2e;">🧠 DANT-GYAAN (QUIZ)</h2>
        <p>Answer to win Magic!</p>
        
        <div class="quiz-box">
            <div class="quiz-question">Q: Does Dant-Veda contain harmful chemicals?</div>
            <button class="quiz-btn btn-yes" onclick="checkAnswer('yes')">YES</button>
            <button class="quiz-btn btn-no" onclick="checkAnswer('no')">NO</button>
            <div id="quiz-result" class="quiz-result"></div>
        </div>
    </div>

    <div id="compare" class="section">
        <h2 style="color: #0b4d2e;">🆚 WHY CHOOSE US?</h2>
        <table class="comp-table">
            <tr>
                <th>Feature</th>
                <th style="background:#0b4d2e;">Dant-Veda 🌿</th>
                <th style="background:#555;">Others 🧪</th>
            </tr>
            <tr>
                <td><b>Chemicals</b></td>
                <td><span class="check">0%</span></td>
                <td><span class="cross">High</span></td>
            </tr>
            <tr>
                <td><b>Safe for Kids</b></td>
                <td><span class="check">✔ Yes</span></td>
                <td><span class="cross">✘ No</span></td>
            </tr>
        </table>
    </div>

    <div id="mission" class="section">
        <h2>🙏 MISSION MUSKURATA BHARAT</h2>
        <div class="social-box">
             <img src="imagee.png" style="width: 359px; height: 200px; object-fit: cover;" alt="Camp Photo">
        </div>
        <p>We donate Re. 1 from every pack.</p>
        <button class="btn" style="width: 220px; margin: 0 auto; background: orange;" onclick="window.location.href='#donate'">VOLUNTEER & DONATE 👇</button>
    </div>

    <div id="donate" class="section">
        <h2 style="color: #0b4d2e;">🤝 SUPPORT US</h2>
        <div class="donate-container">
            <h3 style="color: #0b4d2e; margin-top: 0;">SCAN & PAY</h3>
            <div style="border: 1px solid #ddd; padding: 5px; display: inline-block; border-radius: 10px; background: white;">
                <img src="imagee5.png" alt="Payment QR Code" style="width: 200px; height: auto; border-radius: 5px; display: block;">
            </div>
            <br>
            <div style="background: #f4f4f4; padding: 10px; border-radius: 5px; font-weight: bold; color: #333; border: 1px solid #ccc; margin-top: 10px;">
                UPI: 9717489130@upi
            </div>
            <p style="font-size: 12px; color: #666; margin-top: 5px;">Name: <b>Prince Giri</b></p>
            <a href="upi://pay?pa=9717489130@upi&pn=Prince%20Giri&cu=INR" class="pay-btn" onclick="startConfetti()">PAY NOW ⚡</a>
        </div>
    </div>

    <div id="contact" class="section">
        <h2>📞 CONSUMER SUPPORT</h2>
        <p>Have a query? Write to us.</p>
        <form onsubmit="alert('Message Sent Successfully!'); return false;">
            <input type="text" placeholder="Your Name" required>
            <input type="email" placeholder="Your Email" required>
            <textarea rows="4" placeholder="Your Message / Complaint"></textarea>
            <button type="submit" class="submit-btn">SEND MESSAGE</button>
        </form>
        <br>
        <p>Helpline: 1800-111-222</p>
    </div>

    <div class="footer">
        <p>© 2025 Dant-Veda Pvt Ltd | New Delhi</p>
    </div>

    <div class="offer-bar" onclick="window.location.href='#shop'">
        ⚡ Flash Sale! Free Delivery on orders above ₹100 | Order Now 👉
    </div>

    <script>
        // SPLASH SCREEN
        window.onload = function() {
            setTimeout(function() {
                var splash = document.getElementById('splash-screen');
                if (splash) {
                    splash.style.opacity = '0';
                    setTimeout(function() { splash.style.display = 'none'; }, 800);
                }
            }, 2500);
        };

        // SCROLL BAR & BACK TO TOP
        var mybutton = document.getElementById("myBtn");
        window.onscroll = function() {
            var winScroll = document.body.scrollTop || document.documentElement.scrollTop;
            var height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
            var scrolled = (height > 0) ? (winScroll / height) * 100 : 0;
            var bar = document.getElementById("myBar");
            if (bar) bar.style.width = scrolled + "%";
            
            if (document.body.scrollTop > 300 || document.documentElement.scrollTop > 300) {
                if (mybutton) mybutton.style.display = "block";
            } else {
                if (mybutton) mybutton.style.display = "none";
            }
        };

        function topFunction() {
            document.body.scrollTop = 0;
            document.documentElement.scrollTop = 0;
        }

        // QUIZ LOGIC
        function checkAnswer(answer) {
            var result = document.getElementById('quiz-result');
            if(!result) return;
            if(answer === 'no') {
                result.innerHTML = "✅ CORRECT! It is 100% Herbal.";
                result.style.color = "green";
                startConfetti();
            } else {
                result.innerHTML = "❌ WRONG! We don't use chemicals.";
                result.style.color = "red";
                if (navigator.vibrate) { navigator.vibrate(200); }
            }
        }

        // MAGIC BUTTON
        function magicButton(productName, price) {
            if (navigator.vibrate) { navigator.vibrate(100); }
            startConfetti();
            setTimeout(() => {
                var phoneNumber = "919717489130"; 
                var text = "Hello Prince, I want to order " + productName + " (Rs. " + price + "). Please confirm delivery details.";
                window.open("https://wa.me/" + phoneNumber + "?text=" + encodeURIComponent(text), "_blank");
            }, 800);
        }

        // SEARCH FUNCTION (LIVE FILTERING)
        function searchProducts() {
            var input = document.getElementById("searchInput");
            if(!input) return;
            var filter = input.value.toUpperCase();
            var cards = document.getElementsByClassName("card");
            var found = false;
            
            if(filter.length > 0) {
                var shop = document.getElementById('shop');
                if(shop) shop.scrollIntoView({behavior: 'smooth'});
            }

            for (var i = 0; i < cards.length; i++) {
                var h4 = cards[i].getElementsByTagName("h4")[0];
                if (h4) {
                    var txtValue = h4.textContent || h4.innerText;
                    if (txtValue.toUpperCase().indexOf(filter) > -1) {
                        cards[i].style.display = "";
                        found = true;
                    } else {
                        cards[i].style.display = "none";
                    }
                }
            }

            var noResult = document.getElementById("no-result");
            if (!found) {
                if(noResult) noResult.style.display = "block";
            } else {
                if(noResult) noResult.style.display = "none";
            }
        }

        // CONFETTI
        function startConfetti() {
            var colors = ['#f44336', '#e91e63', '#9c27b0', '#673ab7', '#3f51b5', '#2196f3', '#03a9f4', '#00bcd4', '#009688', '#4caf50', '#8bc34a', '#cddc39', '#ffeb3b', '#ffc107', '#ff9800', '#ff5722'];
            for(let i=0; i<40; i++) {
                let confetti = document.createElement('div');
                confetti.classList.add('confetti');
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.top = (-20 - Math.random()*40) + 'px';
                confetti.style.width = (6 + Math.random()*8) + 'px';
                confetti.style.height = (6 + Math.random()*8) + 'px';
                confetti.style.opacity = (0.7 + Math.random()*0.3);
                confetti.st
