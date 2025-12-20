<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mistrz Geografii + Ranking</title>
    <style>
        body { 
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
            text-align: center; 
            background-color: #2c3e50; 
            color: white; 
            margin: 0; 
            padding: 0; 
        }
        
        /* GŁÓWNE PUDEŁKA */
        .screen { 
            max-width: 600px; 
            margin: 30px auto; 
            background: #34495e; 
            padding: 30px; 
            border-radius: 15px; 
            box-shadow: 0 10px 25px rgba(0,0,0,0.5); 
        }

        h1 { margin-top: 0; color: #f1c40f; }
        h2 { color: #ecf0f1; }
        
        /* OBRAZEK */
        img { 
            border: 5px solid #ecf0f1; 
            max-height: 200px; 
            max-width: 100%; 
            margin-bottom: 20px; 
            border-radius: 10px; 
            background: white; 
            padding: 10px; 
        }
        
        /* PRZYCISKI MENU */
        .menu-btn { 
            display: block; 
            width: 100%; 
            margin: 15px 0; 
            padding: 15px; 
            font-size: 18px; 
            font-weight: bold; 
            background: #27ae60; 
            border: none; 
            border-radius: 8px; 
            color: white; 
            cursor: pointer; 
            transition: 0.3s; 
            box-shadow: 0 5px 0 #1e8449;
        }
        .menu-btn:hover { background: #2ecc71; transform: translateY(-2px); }
        .menu-btn:active { transform: translateY(2px); box-shadow: none; }

        /* PRZYCISKI GRY */
        .btn-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
        .game-btn { 
            padding: 15px; 
            font-size: 16px; 
            cursor: pointer; 
            background: #2980b9; 
            color: white; 
            border: none; 
            border-radius: 5px; 
        }
        .game-btn:hover { background: #3498db; }

        /* INPUT */
        input[type="text"] { 
            width: 70%; padding: 15px; font-size: 18px; 
            border-radius: 5px; border: none; margin-bottom: 10px; 
            text-align: center; 
        }
        .submit-btn { 
            padding: 15px 30px; background: #e67e22; color: white; 
            border: none; border-radius: 5px; font-size: 18px; cursor: pointer; 
        }

        /* TABELA RANKINGOWA */
        #leaderboard {
            margin-top: 20px;
            background: rgba(0,0,0,0.2);
            padding: 15px;
            border-radius: 10px;
        }
        table { width: 100%; border-collapse: collapse; margin-top: 10px; }
        th, td { padding: 10px; border-bottom: 1px solid rgba(255,255,255,0.1); }
        th { color: #f39c12; }
        tr:first-child td { font-weight: bold; color: #f1c40f; } /* Złoty dla 1 miejsca */

        /* KARTY BONUSOWE */
        #bonus-section { 
            display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; 
            background: rgba(0,0,0,0.95); z-index: 100; 
            justify-content: center; align-items: center; flex-direction: column; 
        }
        .cards-container { display: flex; gap: 20px; margin-top: 20px; }
        .card { 
            width: 100px; height: 150px; 
            background: linear-gradient(45deg, #f39c12, #d35400); 
            display: flex; justify-content: center; align-items: center; 
            font-size: 40px; font-weight: bold; cursor: pointer; 
            border: 4px solid white; border-radius: 15px; 
        }

        .back-btn { background: #c0392b; box-shadow: 0 5px 0 #922b21; }
        .back-btn:hover { background: #e74c3c; }
    </style>
</head>
<body>

<!-- LOBBY (MENU GŁÓWNE) -->
<div id="lobby" class="screen">
    <h1>🌍 Mistrz Geografii 🌍</h1>
    <p>Wybierz tryb gry:</p>
    <button class="menu-btn" onclick="startGame(1)">🚩 Wariant 1: Flaga (Wybór)</button>
    <button class="menu-btn" onclick="startGame(2)">🗺️ Wariant 2: Kształt (Wybór)</button>
    <button class="menu-btn" onclick="startGame(3)">⌨️ Wariant 3: Flaga (Wpisywanie)</button>

    <!-- TABELA WYNIKÓW -->
    <div id="leaderboard">
        <h3>🏆 Najlepsi Gracze (Top 5)</h3>
        <table id="score-table">
            <thead>
                <tr>
                    <th>Miejsce</th>
                    <th>Gracz</th>
                    <th>Punkty</th>
                </tr>
            </thead>
            <tbody id="score-list">
                <!-- Tu JavaScript wstawi wyniki -->
                <tr><td colspan="3">Brak wyników. Zagraj pierwszy!</td></tr>
            </tbody>
        </table>
    </div>
</div>

<!-- EKRAN GRY -->
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

<!-- EKRAN KONIEC GRY (Nowość) -->
<div id="game-over-screen" class="screen" style="display: none;">
    <h1 style="color: #e74c3c">KONIEC GRY!</h1>
    <h2>Twój wynik: <span id="final-score" style="color: #f1c40f; font-size: 40px;">0</span></h2>
    
    <div id="save-score-area">
        <p>Wpisz swoje imię, aby zapisać wynik:</p>
        <input type="text" id="player-name" placeholder="Twoje imię" maxlength="15">
        <br><br>
        <button class="menu-btn" onclick="saveScore()">💾 Zapisz Wynik</button>
    </div>
    
    <button class="menu-btn back-btn" onclick="goToLobby()">❌ Wróć bez zapisywania</button>
</div>

<!-- KARTY BONUSOWE -->
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
    // BAZA KRAJÓW
    const countries = [
        { code: 'pl', name: 'Polska' }, { code: 'de', name: 'Niemcy' },
        { code: 'fr', name: 'Francja' }, { code: 'es', name: 'Hiszpania' },
        { code: 'it', name: 'Włochy' }, { code: 'us', name: 'USA' },
        { code: 'gb', name: 'Wielka Brytania' }, { code: 'jp', name: 'Japonia' },
        { code: 'br', name: 'Brazylia' }, { code: 'ca', name: 'Kanada' },
        { code: 'cn', name: 'Chiny' }, { code: 'ru', name: 'Rosja' },
        { code: 'au', name: 'Australia' }, { code: 'in', name: 'Indie' },
        { code: 'mx', name: 'Meksyk' }, { code: 'ar', name: 'Argentyna' },
        { code: 'eg', name: 'Egipt' }, { code: 'pt', name: 'Portugalia' },
        { code: 'se', name: 'Szwecja' }, { code: 'no', name: 'Norwegia' },
        { code: 'fi', name: 'Finlandia' }, { code: 'gr', name: 'Grecja' },
        { code: 'tr', name: 'Turcja' }, { code: 'ua', name: 'Ukraina' }
    ];

    let currentMode = 1;
    let currentCountry;
    let score = 0;
    let lives = 3;

    // --- ŁADOWANIE RANKINGU NA START ---
    window.onload = function() {
        updateLeaderboardDisplay();
        goToLobby();
    };

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
        updateLeaderboardDisplay(); // Odśwież tabelę
    }

    // --- OBSŁUGA KOŃCA GRY i RANKINGU ---

    function endGame() {
        // Pokaż ekran końca gry zamiast alertu
        document.getElementById('game-container').style.display = 'none';
        document.getElementById('game-over-screen').style.display = 'block';
        document.getElementById('final-score').innerText = score;
        document.getElementById('player-name').value = ''; // Wyczyść pole imienia
    }

    function saveScore() {
        const name = document.getElementById('player-name').value.trim();
        if (name === "") {
            alert("Wpisz jakieś imię!");
            return;
        }

        // Pobierz stare wyniki z pamięci przeglądarki
        let highScores = JSON.parse(localStorage.getItem('geoGameScores')) || [];
        
        // Dodaj nowy wynik
        highScores.push({ name: name, score: score });
        
        // Posortuj (od największego do najmniejszego)
        highScores.sort((a, b) => b.score - a.score);
        
        // Zachowaj tylko Top 5
        highScores = highScores.slice(0, 5);
        
        // Zapisz z powrotem do pamięci
        localStorage.setItem('geoGameScores', JSON.stringify(highScores));

        // Wróć do lobby
        goToLobby();
    }

    function updateLeaderboardDisplay() {
        const listElement = document.getElementById('score-list');
        const highScores = JSON.parse(localStorage.getItem('geoGameScores')) || [];

        listElement.innerHTML = ""; // Czyścimy tabelę

        if (highScores.length === 0) {
            listElement.innerHTML = "<tr><td colspan='3'>Brak wyników. Zagraj!</td></tr>";
            return;
        }

        highScores.forEach((entry, index) => {
            let row = `<tr>
                <td>#${index + 1}</td>
                <td>${entry.name}</td>
                <td>${entry.score}</td>
            </tr>`;
            listElement.innerHTML += row;
        });
    }

    // --- LOGIKA GRY ---

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
        if (selectedCountry.code === currentCountry.code) {
            showBonusCards();
        } else {
            loseLife();
        }
    }

    function checkTypeAnswer() {
        let text = document.getElementById('type-answer').value.trim();
        if (text.toLowerCase() === currentCountry.name.toLowerCase()) {
            showBonusCards();
        } else {
            loseLife();
        }
    }

    function loseLife() {
        lives--;
        document.getElementById('lives').innerText = lives;
        if (lives <= 0) {
            endGame(); // Zamiast alertu, idziemy do ekranu końcowego
        } else {
            alert(`❌ Źle! To: ${currentCountry.name}`);
            nextRound();
        }
    }

    // --- BONUSY ---

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
