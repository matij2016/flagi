<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mistrz Geografii (Pełna Wersja)</title>
    <style>
        body { 
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
            text-align: center; 
            background-color: #f4f6f7; 
            color: #2c3e50; 
            margin: 0; 
            padding: 0; 
        }
        
        .screen { 
            max-width: 600px; 
            margin: 30px auto; 
            background: #ffffff; 
            padding: 30px; 
            border-radius: 15px; 
            box-shadow: 0 10px 25px rgba(0,0,0,0.1); 
            border: 1px solid #ddd;
        }

        h1 { margin-top: 0; color: #d35400; }
        h2 { color: #333; }
        
        img { 
            border: 2px solid #bdc3c7; 
            max-height: 200px; 
            max-width: 100%; 
            margin-bottom: 20px; 
            border-radius: 10px; 
            background: #fafafa; 
            padding: 10px; 
        }
        
        /* PRZYCISKI */
        .menu-btn { 
            display: block; width: 100%; margin: 15px 0; padding: 15px; 
            font-size: 18px; font-weight: bold; background: #27ae60; 
            border: none; border-radius: 8px; color: white; cursor: pointer; 
            transition: 0.3s; box-shadow: 0 5px 0 #1e8449;
        }
        .menu-btn:hover { background: #2ecc71; transform: translateY(-2px); }
        .menu-btn:active { transform: translateY(2px); box-shadow: none; }

        .btn-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
        .game-btn { 
            padding: 15px; font-size: 14px; cursor: pointer; /* Zmniejszyłem lekko czcionkę dla długich nazw */
            background: #2980b9; color: white; border: none; border-radius: 5px; 
            word-wrap: break-word;
        }
        .game-btn:hover { background: #3498db; }

        input[type="text"] { 
            width: 70%; padding: 15px; font-size: 18px; 
            border-radius: 5px; border: 2px solid #bdc3c7; margin-bottom: 10px; text-align: center; 
            background: #fff; color: black;
        }
        .submit-btn { 
            padding: 15px 30px; background: #e67e22; color: white; 
            border: none; border-radius: 5px; font-size: 18px; cursor: pointer; 
        }

        /* TABELA RANKINGOWA */
        #leaderboard { 
            margin-top: 20px; 
            background: #ecf0f1; 
            padding: 15px; 
            border-radius: 10px; 
            color: black;
        }
        table { width: 100%; border-collapse: collapse; margin-top: 10px; }
        th, td { padding: 10px; border-bottom: 1px solid #bdc3c7; }
        th { color: #d35400; }
        
        tr:nth-child(1) td { color: #f39c12; font-weight: bold; } /* Złoto */
        tr:nth-child(2) td { color: #7f8c8d; font-weight: bold; } /* Srebro */
        tr:nth-child(3) td { color: #a0522d; font-weight: bold; } /* Brąz */
        tr:nth-child(4) td { color: #000000; font-weight: bold; } /* Czarny */
        tr:nth-child(5) td { color: #000000; font-weight: bold; } /* Czarny */

        #stats { 
            font-size: 22px; margin-bottom: 20px; background: #ecf0f1; 
            padding: 10px; border-radius: 5px; color: #2c3e50;
        }

        #bonus-section { 
            display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; 
            background: rgba(0,0,0,0.9); z-index: 100; 
            justify-content: center; align-items: center; flex-direction: column; 
            color: white; 
        }
        .cards-container { display: flex; gap: 20px; margin-top: 20px; }
        .card { 
            width: 100px; height: 150px; 
            background: linear-gradient(45deg, #f39c12, #d35400); 
            display: flex; justify-content: center; align-items: center; 
            font-size: 40px; font-weight: bold; cursor: pointer; 
            border: 4px solid white; border-radius: 15px; color: white;
        }

        .back-btn { background: #c0392b; box-shadow: 0 5px 0 #922b21; }
        .back-btn:hover { background: #e74c3c; }
    </style>
</head>
<body>

<div id="lobby" class="screen">
    <h1>🌍 Mistrz Geografii 🌍</h1>
    <p>Wybierz tryb gry:</p>
    <button class="menu-btn" onclick="startGame(1)">🚩 Wariant 1: Flaga (Wybór)</button>
    <button class="menu-btn" onclick="startGame(2)">🗺️ Wariant 2: Kształt (Wybór)</button>
    <button class="menu-btn" onclick="startGame(3)">⌨️ Wariant 3: Flaga (Wpisywanie)</button>

    <div id="leaderboard">
        <h3>🏆 TOP 5 GRACZY</h3>
        <table id="score-table">
            <thead>
                <tr>
                    <th>Miejsce</th>
                    <th>Gracz</th>
                    <th>Punkty</th>
                </tr>
            </thead>
            <tbody id="score-list"></tbody>
        </table>
        <br>
        <button onclick="resetScores()" style="margin-top:10px; font-size:12px; background:none; border:1px solid #7f8c8d; color:#7f8c8d; cursor:pointer; padding: 5px;">Zresetuj wyniki</button>
    </div>
</div>

<div id="game-container" class="screen" style="display: none;">
    <div id="stats">
        ❤️ Życia: <span id="lives">3</span> | ⭐ Punkty: <span id="score">0</span>
    </div>
    <h2 id="question-text">Co to za kraj?</h2>
    <img id="game-img" src="" alt="Zagadka">

    <div id="answers-grid" class="btn-grid">
        <button class="game-btn" onclick="checkAnswer(0)">A</button>
        <button class="game-btn" onclick="checkAnswer(1)">B</button>
        <button class="game-btn" onclick="checkAnswer(2)">C</button>
        <button class="game-btn" onclick="checkAnswer(3)">D</button>
    </div>
    
    <div id="input-area" style="display:none;">
        <input type="text" id="type-answer" placeholder="Wpisz nazwę kraju..." onkeydown="if(event.key === 'Enter') checkTypeAnswer()">
        <br>
        <button class="submit-btn" onclick="checkTypeAnswer()">SPRAWDŹ</button>
    </div>

    <button class="menu-btn back-btn" onclick="goToLobby()">🏠 Wyjdź do Menu</button>
</div>

<div id="game-over-screen" class="screen" style="display: none;">
    <h1 style="color: #c0392b">KONIEC GRY!</h1>
    <h2>Twój wynik: <span id="final-score" style="color: #d35400; font-size: 40px;">0</span></h2>
    
    <div id="save-score-area">
        <p>Wpisz swoje imię, aby zapisać wynik:</p>
        <input type="text" id="player-name" placeholder="Twoje imię" maxlength="15">
        <br><br>
        <button class="menu-btn" onclick="saveScore()">💾 Zapisz Wynik</button>
    </div>
    
    <button class="menu-btn back-btn" onclick="goToLobby()">❌ Wróć bez zapisywania</button>
</div>

<div id="bonus-section">
    <h2 style="color:#2ecc71; font-size: 30px;">DOBRA ODPOWIEDŹ!</h2>
    <p>Wybierz kartę bonusową:</p>
    <div class="cards-container">
        <div class="card" onclick="pickCard(this)">?</div>
        <div class="card" onclick="pickCard(this)">?</div>
        <div class="card" onclick="pickCard(this)">?</div>
    </div>
</div>

<script>
    // OGROMNA LISTA KRAJÓW (Kody ISO-2)
    const countries = [
        {code: 'af', name: 'Afganistan'}, {code: 'al', name: 'Albania'}, {code: 'dz', name: 'Algieria'},
        {code: 'ad', name: 'Andora'}, {code: 'ao', name: 'Angola'}, {code: 'ag', name: 'Antigua i Barbuda'},
        {code: 'sa', name: 'Arabia Saudyjska'}, {code: 'ar', name: 'Argentyna'}, {code: 'am', name: 'Armenia'},
        {code: 'au', name: 'Australia'}, {code: 'at', name: 'Austria'}, {code: 'az', name: 'Azerbejdżan'},
        {code: 'bs', name: 'Bahamy'}, {code: 'bh', name: 'Bahrajn'}, {code: 'bd', name: 'Bangladesz'},
        {code: 'bb', name: 'Barbados'}, {code: 'be', name: 'Belgia'}, {code: 'bz', name: 'Belize'},
        {code: 'bj', name: 'Benin'}, {code: 'bt', name: 'Bhutan'}, {code: 'by', name: 'Białoruś'},
        {code: 'bo', name: 'Boliwia'}, {code: 'ba', name: 'Bośnia i Hercegowina'}, {code: 'bw', name: 'Botswana'},
        {code: 'br', name: 'Brazylia'}, {code: 'bn', name: 'Brunei'}, {code: 'bg', name: 'Bułgaria'},
        {code: 'bf', name: 'Burkina Faso'}, {code: 'bi', name: 'Burundi'}, {code: 'cl', name: 'Chile'},
        {code: 'cn', name: 'Chiny'}, {code: 'hr', name: 'Chorwacja'}, {code: 'cy', name: 'Cypr'},
        {code: 'td', name: 'Czad'}, {code: 'cz', name: 'Czechy'}, {code: 'dk', name: 'Dania'},
        {code: 'cd', name: 'Demokratyczna Republika Konga'}, {code: 'dm', name: 'Dominika'},
        {code: 'do', name: 'Dominikana'}, {code: 'dj', name: 'Dżibuti'}, {code: 'eg', name: 'Egipt'},
        {code: 'ec', name: 'Ekwador'}, {code: 'er', name: 'Erytrea'}, {code: 'ee', name: 'Estonia'},
        {code: 'et', name: 'Etiopia'}, {code: 'fj', name: 'Fidżi'}, {code: 'ph', name: 'Filipiny'},
        {code: 'fi', name: 'Finlandia'}, {code: 'fr', name: 'Francja'}, {code: 'ga', name: 'Gabon'},
        {code: 'gm', name: 'Gambia'}, {code: 'gh', name: 'Ghana'}, {code: 'gr', name: 'Grecja'},
        {code: 'gd', name: 'Grenada'}, {code: 'ge', name: 'Gruzja'}, {code: 'gy', name: 'Gujana'},
        {code: 'gt', name: 'Gwatemala'}, {code: 'gn', name: 'Gwinea'}, {code: 'gw', name: 'Gwinea Bissau'},
        {code: 'ht', name: 'Haiti'}, {code: 'es', name: 'Hiszpania'}, {code: 'nl', name: 'Holandia'},
        {code: 'hn', name: 'Honduras'}, {code: 'in', name: 'Indie'}, {code: 'id', name: 'Indonezja'},
        {code: 'iq', name: 'Irak'}, {code: 'ir', name: 'Iran'}, {code: 'ie', name: 'Irlandia'},
        {code: 'is', name: 'Islandia'}, {code: 'il', name: 'Izrael'}, {code: 'jm', name: 'Jamajka'},
        {code: 'jp', name: 'Japonia'}, {code: 'ye', name: 'Jemen'}, {code: 'jo', name: 'Jordania'},
        {code: 'kh', name: 'Kambodża'}, {code: 'cm', name: 'Kamerun'}, {code: 'ca', name: 'Kanada'},
        {code: 'qa', name: 'Katar'}, {code: 'kz', name: 'Kazachstan'}, {code: 'ke', name: 'Kenia'},
        {code: 'kg', name: 'Kirgistan'}, {code: 'ki', name: 'Kiribati'}, {code: 'co', name: 'Kolumbia'},
        {code: 'km', name: 'Komory'}, {code: 'cg', name: 'Kongo'}, {code: 'kr', name: 'Korea Południowa'},
        {code: 'kp', name: 'Korea Północna'}, {code: 'cr', name: 'Kostaryka'}, {code: 'cu', name: 'Kuba'},
        {code: 'kw', name: 'Kuwejt'}, {code: 'la', name: 'Laos'}, {code: 'ls', name: 'Lesotho'},
        {code: 'lb', name: 'Liban'}, {code: 'lr', name: 'Liberia'}, {code: 'ly', name: 'Libia'},
        {code: 'li', name: 'Liechtenstein'}, {code: 'lt', name: 'Litwa'}, {code: 'lu', name: 'Luksemburg'},
        {code: 'lv', name: 'Łotwa'}, {code: 'mk', name: 'Macedonia Północna'}, {code: 'mg', name: 'Madagaskar'},
        {code: 'mw', name: 'Malawi'}, {code: 'mv', name: 'Malediwy'}, {code: 'my', name: 'Malezja'},
        {code: 'ml', name: 'Mali'}, {code: 'mt', name: 'Malta'}, {code: 'ma', name: 'Maroko'},
        {code: 'mr', name: 'Mauretania'}, {code: 'mu', name: 'Mauritius'}, {code: 'mx', name: 'Meksyk'},
        {code: 'fm', name: 'Mikronezja'}, {code: 'mm', name: 'Mjanma'}, {code: 'md', name: 'Mołdawia'},
        {code: 'mc', name: 'Monako'}, {code: 'mn', name: 'Mongolia'}, {code: 'mz', name: 'Mozambik'},
        {code: 'na', name: 'Namibia'}, {code: 'nr', name: 'Nauru'}, {code: 'np', name: 'Nepal'},
        {code: 'de', name: 'Niemcy'}, {code: 'ne', name: 'Niger'}, {code: 'ng', name: 'Nigeria'},
        {code: 'ni', name: 'Nikaragua'}, {code: 'no', name: 'Norwegia'}, {code: 'nz', name: 'Nowa Zelandia'},
        {code: 'om', name: 'Oman'}, {code: 'pk', name: 'Pakistan'}, {code: 'pw', name: 'Palau'},
        {code: 'pa', name: 'Panama'}, {code: 'pg', name: 'Papua-Nowa Gwinea'}, {code: 'py', name: 'Paragwaj'},
        {code: 'pe', name: 'Peru'}, {code: 'pl', name: 'Polska'}, {code: 'pt', name: 'Portugalia'},
        {code: 'za', name: 'RPA'}, {code: 'cf', name: 'Republika Środkowoafrykańska'},
        {code: 'cv', name: 'Republika Zielonego Przylądka'}, {code: 'ru', name: 'Rosja'}, {code: 'ro', name: 'Rumunia'},
        {code: 'rw', name: 'Rwanda'}, {code: 'kn', name: 'Saint Kitts i Nevis'}, {code: 'lc', name: 'Saint Lucia'},
        {code: 'vc', name: 'Saint Vincent i Grenadyny'}, {code: 'sv', name: 'Salwador'}, {code: 'ws', name: 'Samoa'},
        {code: 'sm', name: 'San Marino'}, {code: 'sn', name: 'Senegal'}, {code: 'rs', name: 'Serbia'},
        {code: 'sc', name: 'Seszele'}, {code: 'sl', name: 'Sierra Leone'}, {code: 'sg', name: 'Singapur'},
        {code: 'sk', name: 'Słowacja'}, {code: 'si', name: 'Słowenia'}, {code: 'so', name: 'Somalia'},
        {code: 'lk', name: 'Sri Lanka'}, {code: 'us', name: 'Stany Zjednoczone'}, {code: 'sz', name: 'Suazi'},
        {code: 'sd', name: 'Sudan'}, {code: 'ss', name: 'Sudan Południowy'}, {code: 'sr', name: 'Surinam'},
        {code: 'sy', name: 'Syria'}, {code: 'ch', name: 'Szwajcaria'}, {code: 'se', name: 'Szwecja'},
        {code: 'tj', name: 'Tadżykistan'}, {code: 'th', name: 'Tajlandia'}, {code: 'tz', name: 'Tanzania'},
        {code: 'tl', name: 'Timor Wschodni'}, {code: 'tg', name: 'Togo'}, {code: 'to', name: 'Tonga'},
        {code: 'tt', name: 'Trynidad i Tobago'}, {code: 'tn', name: 'Tunezja'}, {code: 'tr', name: 'Turcja'},
        {code: 'tm', name: 'Turkmenistan'}, {code: 'tv', name: 'Tuvalu'}, {code: 'ug', name: 'Uganda'},
        {code: 'ua', name: 'Ukraina'}, {code: 'uy', name: 'Urugwaj'}, {code: 'uz', name: 'Uzbekistan'},
        {code: 'vu', name: 'Vanuatu'}, {code: 'va', name: 'Watykan'}, {code: 've', name: 'Wenezuela'},
        {code: 'hu', name: 'Węgry'}, {code: 'gb', name: 'Wielka Brytania'}, {code: 'vn', name: 'Wietnam'},
        {code: 'it', name: 'Włochy'}, {code: 'ci', name: 'Wybrzeże Kości Słoniowej'},
        {code: 'mh', name: 'Wyspy Marshalla'}, {code: 'sb', name: 'Wyspy Salomona'},
        {code: 'st', name: 'Wyspy Świętego Tomasza i Książęca'}, {code: 'zm', name: 'Zambia'},
        {code: 'zw', name: 'Zimbabwe'}, {code: 'ae', name: 'Zjednoczone Emiraty Arabskie'}
    ];

    let currentMode = 1;
    let currentCountry;
    let score = 0;
    let lives = 3;

    window.onload = function() {
        initFakeScores();
        updateLeaderboardDisplay();
        goToLobby();
    };

    function initFakeScores() {
        if (!localStorage.getItem('geoGameScores')) {
            const bots = [
                { name: "MistrzBot", score: 150 },
                { name: "Podróżnik", score: 80 },
                { name: "Turysta", score: 30 }
            ];
            localStorage.setItem('geoGameScores', JSON.stringify(bots));
        }
    }

    function resetScores() {
        localStorage.removeItem('geoGameScores');
        initFakeScores();
        updateLeaderboardDisplay();
    }

    function startGame(mode) {
        currentMode = mode;
        score = 0;
        lives = 3;
        document.getElementById('score').innerText = score;
        document.getElementById('lives').innerText = lives;

        document.getElementById('lobby').style.display = 'none';
        document.getElementById('game-over-screen').style.display = 'none';
        document.getElementById('game-container').style.display = 'block';

        if (mode === 1 || mode === 2) {
            document.getElementById('answers-grid').style.display = 'grid';
            document.getElementById('input-area').style.display = 'none';
        } else {
            document.getElementById('answers-grid').style.display = 'none';
            document.getElementById('input-area').style.display = 'block';
        }
        nextRound();
    }

    function goToLobby() {
        document.getElementById('game-container').style.display = 'none';
        document.getElementById('game-over-screen').style.display = 'none';
        document.getElementById('bonus-section').style.display = 'none';
        document.getElementById('lobby').style.display = 'block';
        updateLeaderboardDisplay();
    }

    function endGame() {
        document.getElementById('game-container').style.display = 'none';
        document.getElementById('game-over-screen').style.display = 'block';
        document.getElementById('final-score').innerText = score;
        document.getElementById('player-name').value = '';
    }

    function saveScore() {
        const name = document.getElementById('player-name').value.trim();
        if (name === "") { alert("Wpisz imię!"); return; }

        let highScores = JSON.parse(localStorage.getItem('geoGameScores')) || [];
        highScores.push({ name: name, score: score });
        highScores.sort((a, b) => b.score - a.score);
        highScores = highScores.slice(0, 5); 
        
        localStorage.setItem('geoGameScores', JSON.stringify(highScores));
        goToLobby();
    }

    function updateLeaderboardDisplay() {
        const listElement = document.getElementById('score-list');
        const highScores = JSON.parse(localStorage.getItem('geoGameScores')) || [];

        listElement.innerHTML = ""; 
        highScores.forEach((entry, index) => {
            let row = `<tr><td>#${index + 1}</td><td>${entry.name}</td><td>${entry.score}</td></tr>`;
            listElement.innerHTML += row;
        });
    }

    function nextRound() {
        currentCountry = countries[Math.floor(Math.random() * countries.length)];
        document.getElementById('type-answer').value = '';
        const imgElement = document.getElementById('game-img');
        
        if (currentMode === 2) {
            imgElement.src = `https://raw.githubusercontent.com/djaiss/mapsicon/master/all/${currentCountry.code}/256.png`;
            document.getElementById('question-text').innerText = "Jaki kraj ma taki kształt?";
        } else {
            imgElement.src = `https://flagcdn.com/w320/${currentCountry.code}.png`;
            document.getElementById('question-text').innerText = "Czyja to flaga?";
        }

        if (currentMode === 1 || currentMode === 2) {
            let options = [currentCountry];
            while (options.length < 4) {
                let randomC = countries[Math.floor(Math.random() * countries.length)];
                if (!options.includes(randomC)) options.push(randomC);
            }
            options.sort(() => Math.random() - 0.5);

            const buttons = document.querySelectorAll('#answers-grid button');
            for (let i = 0; i < 4; i++) {
                buttons[i].innerText = options[i].name;
                buttons[i].onclick = function() { checkAnswer(options[i]); };
            }
        }
    }

    function checkAnswer(selectedCountry) {
        if (selectedCountry.code === currentCountry.code) showBonusCards();
        else loseLife();
    }

    function checkTypeAnswer() {
        let text = document.getElementById('type-answer').value.trim();
        if (text.toLowerCase() === currentCountry.name.toLowerCase()) showBonusCards();
        else loseLife();
    }

    function loseLife() {
        lives--;
        document.getElementById('lives').innerText = lives;
        if (lives <= 0) endGame();
        else {
            alert(`❌ Źle! To: ${currentCountry.name}`);
            nextRound();
        }
    }

    function showBonusCards() {
        document.getElementById('bonus-section').style.display = 'flex';
        const cards = document.querySelectorAll('.card');
        cards.forEach(card => {
            card.innerText = "?";
            card.style.background = "linear-gradient(45deg, #f39c12, #d35400)";
            card.style.pointerEvents = "auto";
        });
    }

    function pickCard(cardElement) {
        const points = Math.floor(Math.random() * 10) + 1;
        cardElement.innerText = "+" + points;
        cardElement.style.background = "#27ae60"; 
        score += points;
        document.getElementById('score').innerText = score;
        document.querySelectorAll('.card').forEach(c => c.style.pointerEvents = "none");
        setTimeout(() => {
            document.getElementById('bonus-section').style.display = 'none';
            nextRound();
        }, 1500);
    }
</script>

</body>
</html>
