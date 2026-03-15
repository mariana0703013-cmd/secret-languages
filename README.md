<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>M.N.B Secret Languages</title>
    <style>
        :root {
            --bg: #0f172a;
            --card: #1e293b;
            --accent: #38bdf8;
            --text: #f8fafc;
        }
        body { font-family: 'Segoe UI', Arial, sans-serif; margin: 0; background: var(--bg); color: var(--text); line-height: 1.6; }
        header { background: #020617; text-align: center; padding: 40px 20px; border-bottom: 2px solid var(--accent); }
        header h1 { color: var(--accent); margin: 0; font-size: 2.5rem; }
        nav { background: var(--card); padding: 10px; position: sticky; top: 0; display: flex; justify-content: center; gap: 15px; flex-wrap: wrap; z-index: 100; }
        nav a { color: var(--text); text-decoration: none; font-weight: bold; font-size: 0.9rem; padding: 5px 10px; border-radius: 4px; transition: 0.3s; }
        nav a:hover { background: var(--accent); color: #020617; }
        section { padding: 30px 20px; max-width: 800px; margin: 0 auto; }
        .card { background: var(--card); padding: 20px; margin: 20px 0; border-radius: 12px; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1); }
        input, button { width: 100%; padding: 12px; margin: 8px 0; border-radius: 8px; border: 1px solid #334155; box-sizing: border-box; }
        input { background: #0f172a; color: white; }
        button { background: var(--accent); color: #020617; cursor: pointer; font-weight: bold; border: none; transition: transform 0.1s; }
        button:active { transform: scale(0.98); }
        .result-box { background: #334155; padding: 15px; border-radius: 6px; min-height: 20px; word-break: break-all; margin-top: 10px; color: var(--accent); font-family: monospace; }
        footer { background: #020617; text-align: center; padding: 30px; font-size: 0.8rem; opacity: 0.7; }
    </style>
</head>
<body>

<header>
    <h1>M.N.B Secret</h1>
    <p>Code. Translate. Communicate.</p>
</header>

<nav>
    <a href="#home">Home</a>
    <a href="#languages">Languages</a>
    <a href="#secret">Tools</a>
    <a href="#game">Game</a>
</nav>

<section id="home">
    <h2>Welcome</h2>
    <p>Explore world languages, generate encrypted ciphers, and test your linguistic knowledge.</p>
</section>

<section id="languages">
    <h2>Search Languages</h2>
    <input type="text" id="search" placeholder="Type a language (e.g. Arabic, Yoruba)...">
    <div id="languageList" style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 15px;"></div>
</section>

<section id="secret">
    <h2>Secret Tools</h2>
    <div class="card">
        <h3>Leet (L33T) Translator</h3>
        <input id="leetInput" placeholder="Enter text to convert...">
        <button onclick="translateLeet()">Convert to Leet</button>
        <div class="result-box" id="leetResult"></div>
    </div>

    <div class="card">
        <h3>Caesar Cipher</h3>
        <input id="cipherInput" placeholder="Message to encrypt...">
        <input id="shift" type="number" value="3" placeholder="Shift (1-25)">
        <button onclick="runCipher()">Encrypt Message</button>
        <div class="result-box" id="cipherResult"></div>
    </div>
</section>

<section id="game">
    <div class="card" style="text-align: center; border: 2px solid var(--accent);">
        <h2>Trivia Challenge</h2>
        <p id="question">Which language has the most native speakers?</p>
        <button onclick="checkAnswer('Spanish')">Spanish</button>
        <button onclick="checkAnswer('French')">French</button>
        <button onclick="checkAnswer('Chinese')">Chinese</button>
        <p id="gameResult" style="font-weight: bold; margin-top: 15px;"></p>
    </div>
</section>

<footer>
    <p>© 2026 M.N.B Secret Languages | Created for Mobile</p>
</footer>

<script>
    const languages = ["English", "Spanish", "French", "German", "Italian", "Yoruba", "Hausa", "Igbo", "Chinese", "Japanese", "Arabic", "Russian", "Portuguese", "Hindi"];
    
    function displayLanguages(arr) {
        const list = document.getElementById("languageList");
        list.innerHTML = arr.map(l => `<div style="background:#334155; padding:10px; border-radius:5px; text-align:center;">${l}</div>`).join('');
    }

    displayLanguages(languages);

    document.getElementById("search").addEventListener("input", (e) => {
        const filtered = languages.filter(l => l.toLowerCase().includes(e.target.value.toLowerCase()));
        displayLanguages(filtered);
    });

    function translateLeet() {
        const map = {'a':'4', 'e':'3', 'i':'1', 'o':'0', 's':'5', 't':'7', 'b':'8'};
        let text = document.getElementById("leetInput").value.toLowerCase();
        let result = text.split('').map(char => map[char] || char).join('');
        document.getElementById("leetResult").innerText = result || "Result will appear here...";
    }

    function runCipher() {
        let str = document.getElementById("cipherInput").value;
        let amount = parseInt(document.getElementById("shift").value);
        
        let output = str.split('').map(char => {
            if (char.match(/[a-z]/i)) {
                let code = char.charCodeAt();
                let base = (code >= 65 && code <= 90) ? 65 : 97;
                return String.fromCharCode(((code - base + amount) % 26) + base);
            }
            return char;
        }).join('');
        
        document.getElementById("cipherResult").innerText = output || "Encrypted text will appear here...";
    }

    function checkAnswer(choice) {
        const res = document.getElementById("gameResult");
        if(choice === "Chinese") {
            res.innerText = "✅ Correct! Mandarin Chinese has over 900 million native speakers.";
            res.style.color = "#4ade80";
        } else {
            res.innerText = "❌ Not quite. Try again!";
            res.style.color = "#f87171";
        }
    }
</script>
</body>
</html>
