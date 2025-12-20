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

    <button class="menu-btn back-btn" <!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Mistrz Geografii</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; text-align: center; background-color: #2c3e50; color: white; margin: 0; padding: 0; }
        
        /* Styl dla Lobby i Kontenera Gry */
        .screen { max-width: 600px; margin: 50px auto; background: #34495e; padding: 30px; border-radius: 15px; box-shadow: 0 10px 25px rgba(0,0,0,0.5); }
        .hidden { display: none !important; }

        h1 { margin-top: 0; color: #f1c40f; }
        
        /* Obrazek (Flaga lub Mapa) */
        img { border: 5px solid #ecf0f1; max-height: 200px; max-width: 100%; margin-bottom: 20px; border-radius: 10px; background: white; padding: 10px; }
        
        /* Przyciski w menu i grze */
        .btn-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
        .menu-btn { display: block; width: 100%; margin: 10px 0; padding: 20px; font-size: 18px; font-weight: bold; background: #27ae60; border: none; border-radius: 8px; color: white; cursor: pointer; transition: 0.3s; }
        .menu-btn:hover { background: #2ecc71; transform: scale(1.02); }

        .game-btn { padding: 15px; font-size: 16px; cursor: pointer; background: #2980b9; color: white; border: none; border-radius: 5px; transition: 0.2s; }
        .game-btn:hover { background: #3498db; }

        /* Input dla wariantu 3 */
        input[type="text"] { width: 70%; padding: 15px; font-size: 18px; border-radius: 5px; border: none; margin-bottom: 10px; text-align: center; }
        .submit-btn { padding: 15px 30px; background: #e67e22; color: white; border: none; border-radius: 5px; font-size: 18px; cursor: pointer; }

        /* Sekcja kart bonusowych */
        #bonus-section { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.9); z-index: 100; justify-content: center; align-items: center; flex-direction: column; }
        .cards-container { display: flex; gap: 20px; margin-top: 20px; }
        .card { width: 120px; height: 180px; background: linear-gradient(45deg, #f39c12, #d35400); display: flex; justify-content: center; align-items: center; font-size: 40px; font-weight: bold; cursor: pointer; border: 4px solid white; border-radius: 15px; box-shadow: 0 0 20px rgba(255, 165, 0, 0.6); transition: 0.3s; }
        .card:hover { transform: translateY(-10px); }

        #stats { font-size: 22px; margin-bottom: 20px; background: rgba(0,0,0,0.2); padding: 10px; border-radius: 5px; }
        
        .back-btn { margin-top: 20px; background: #c0392b; width: auto; display: inline-block; padding: 10px 20px; }
    </style>
</head>
<body>

<!-- LOBBY (MENU GŁÓWNE) -->
<div id="lobby" class="screen">
    <h1>🌍 Mistrz Geografii 🌍</h1>
    <p>Wybierz tryb gry:</p>
    <button class="menu-btn" onclick="startGame(1)">Wariant 1: Zgadnij Flagę (Przyciski)</button>
    <button class="menu-btn" onclick="startGame(2)">Wariant 2: Zgadnij Kształt (Przyciski)</button>
    <button class="menu-btn" onclick="startGame(3)">Wariant 3: Zgadnij Flagę (Wpisywanie)</button>
</div>

<!-- EKRAN GRY -->
<div id="game-container" class="screen hidden">
    <div id="stats">
        ❤️ Życia: <span id="lives">3</span> | ⭐ Punkty: <span id="score">0</span>
    </div>

    <h2 id="question-text">Co to za kraj?</h2>
    
    <!-- Obrazek (Flaga lub Kształt) -->
    <img id="game-img" src="" alt="Zagadka">

    <!-- Kontener na przyciski (Wariant 1 i 2) -->
    <div id="answers-grid" class="btn-grid hidden">
        <button class="game-btn" onclick="checkAnswer(0)">A</button>
        <button class="game-btn" onclick="checkAnswer(1)">B</button>
        <button class="game-btn" onclick="checkAnswer(2)">C</button>
        <button class="game-btn" onclick="checkAnswer(3)">D</button>
    </div>
    
    <!-- Kontener na wpisywanie (Wariant 3) -->
    <div id="input-area" class="hidden">
        <input type="text" id="type-answer" placeholder="Wpisz nazwę kraju..." onkeydown="if(event.key === 'Enter') checkTypeAnswer()">
        <br>
        <button class="submit-btn" onclick="checkTypeAnswer()">SPRAWDŹ</button>
    </div>

    <button class="menu-btn back-btn" onclick="goToLobby()">Wróć do menu</button>
</div>

<!-- EKRAN KART BONUSOWYCH -->
<div id="bonus-section">
    <h2 style="color:#2ecc71; font-size: 30px;">DOBRA ODPOWIEDŹ!</h2>
    <p>Wybierz kartę, aby odkryć punkty:</p>
    <div class="cards-container">
        <div class="card" onclick="pickCard(this)">?</div>
        <div class="card" onclick="pickCard(this)">?</div>
        <div class="card" onclick="pickCard(this)">?</div>
    </div>
</div>

<script>
    // BAZA DANYCH KRAJÓW (Kod ISO + Nazwa)
    const countries = [
        { code: 'pl', name: 'Polska' }, { code: 'de', name: 'Niemcy' },
        { code: 'fr', name: 'Francja' }, { code: 'es', name: 'Hiszpania' },
        { code: 'it', name: 'Włochy' }, { code: 'us', name: 'USA' },
        { code: 'gb', name: 'Wielka Brytania' }, { code: 'jp', name: 'Japonia' },
        { code: 'br', name: 'Brazylia' }, { code: 'ca', name: 'Kanada' },
        { code: 'cn', name: 'Chiny' }, { code: 'ru', name: 'Rosja' },
        { code: 'au', name: 'Australia' }, { code: 'in', name: 'Indie' },
        { code: 'mx', name: 'Meksyk' }, { code: 'ar', name: 'Argentyna' },
        { code: 'eg', name: 'Egipt' }, { code: 'za', name: 'RPA' },
        { code: 'kr', name: 'Korea Południowa' }, { code: 'tr', name: 'Turcja' },
        { code: 'ua', name: 'Ukraina' }, { code: 'gr', name: 'Grecja' },
        { code: 'pt', name: 'Portugalia' }, { code: 'se', name: 'Szwecja' },
        { code: 'no', name: 'Norwegia' }, { code: 'fi', name: 'Finlandia' },
        { code: 'dk', name: 'Dania' }, { code: 'nl', name: 'Holandia' },
        { code: 'be', name: 'Belgia' }, { code: 'ch', name: 'Szwajcaria' },
        { code: 'at', name: 'Austria' }, { code: 'cz', name: 'Czechy' },
        { code: 'sk', name: 'Słowacja' }, { code: 'hu', name: 'Węgry' },
        { code: 'ro', name: 'Rumunia' }, { code: 'bg', name: 'Bułgaria' },
        { code: 'hr', name: 'Chorwacja' }, { code: 'ie', name: 'Irlandia' },
        { code: 'th', name: 'Tajlandia' }, { code: 'vn', name: 'Wietnam' }
    ];

    let currentMode = 1;
    let currentCountry;
    let score = 0;
    let lives = 3;
    let correctAnswerIndex;

    // --- FUNKCJE MENU ---

    function startGame(mode) {
        currentMode = mode;
        score = 0;
        lives = 3;
        document.getElementById('score').innerText = score;
        document.getElementById('lives').innerText = lives;

        // Przełącz ekrany
        document.getElementById('lobby').classList.add('hidden');
        document.getElementById('game-container').classList.remove('hidden');

        // Ustaw widok w zależności od trybu
        if (mode === 1 || mode === 2) {
            document.getElementById('answers-grid').classList.remove('hidden');
            document.getElementById('input-area').classList.add('hidden');
        } else {
            document.getElementById('answers-grid').classList.add('hidden');
            document.getElementById('input-area').classList.remove('hidden');
        }

        nextRound();
    }

    function goToLobby() {
        document.getElementById('lobby').classList.remove('hidden');
        document.getElementById('game-container').classList.add('hidden');
    }

    // --- LOGIKA GRY ---

    function nextRound() {
        if (lives <= 0) {
            alert("❌ KONIEC GRY! Twój wynik: " + score);
            goToLobby();
            return;
        }

        // Wylosuj kraj
        currentCountry = countries[Math.floor(Math.random() * countries.length)];
        
        // Wyczyść input
        document.getElementById('type-answer').value = '';

        // Ustaw obrazek w zależności od wariantu
        const imgElement = document.getElementById('game-img');
        
        if (currentMode === 2) {
            // Wariant 2: Mapa (korzystamy z github raw dla kształtów)
            // Uwaga: Niektóre kody w tej bazie mogą się różnić, ale dla większości zadziała
            imgElement.src = `https://raw.githubusercontent.com/djaiss/mapsicon/master/all/${currentCountry.code}/256.png`;
            document.getElementById('question-text').innerText = "Jaki kraj ma taki kształt?";
        } else {
            // Wariant 1 i 3: Flaga
            imgElement.src = `https://flagcdn.com/w320/${currentCountry.code}.png`;
            document.getElementById('question-text').innerText = "Do kogo należy ta flaga?";
        }

        // Jeśli to wariant 1 lub 2, przygotuj przyciski
        if (currentMode === 1 || currentMode === 2) {
            let options = [currentCountry];
            while (options.length < 4) {
                let randomC = countries[Math.floor(Math.random() * countries.length)];
                if (!options.includes(randomC)) {
                    options.push(randomC);
                }
            }
            options.sort(() => Math.random() - 0.5);

            const buttons = document.querySelectorAll('#answers-grid button');
            for (let i = 0; i < 4; i++) {
                buttons[i].innerText = options[i].name;
                // Musimy zresetować onclick, żeby zamknąć starą funkcję w pętli (closure fix)
                buttons[i].onclick = () => checkAnswer(options[i]);
            }
        }
    }

    // Sprawdzanie przycisków (Wariant 1 i 2)
    function checkAnswer(selectedCountry) {
        if (selectedCountry.code === currentCountry.code) {
            showBonusCards();
        } else {
            loseLife();
        }
    }

    // Sprawdzanie wpisywania (Wariant 3)
    function checkTypeAnswer() {
        let text = document.getElementById('type-answer').value.trim();
        // Porównanie bez wielkości liter
        if (text.toLowerCase() === currentCountry.name.toLowerCase()) {
            showBonusCards();
        } else {
            loseLife();
        }
    }

    function loseLife() {
        lives--;
        document.getElementById('lives').innerText = lives;
        alert(`❌ Źle! Poprawna odpowiedź to: ${currentCountry.name}`);
        nextRound();
    }

    // --- KARTY BONUSOWE ---

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
        // Losuj punkty 1-10
        const points = Math.floor(Math.random() * 10) + 1;
        
        cardElement.innerText = "+" + points;
        cardElement.style.background = "#27ae60"; // Zielony
        
        score += points;
        document.getElementById('score').innerText = score;

        // Zablokuj inne karty
        const cards = document.querySelectorAll('.card');
        cards.forEach(c => c.style.pointerEvents = "none");

        // Po chwili następna runda
        setTimeout(() => {
            document.getElementById('bonus-section').style.display = 'none';
            nextRound();
        }, 1500);
    }

</script>

</body>
</html><!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Mistrz Geografii</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; text-align: center; background-color: #2c3e50; color: white; margin: 0; padding: 0; }
        
        /* Styl dla Lobby i Kontenera Gry */
        .screen { max-width: 600px; margin: 50px auto; background: #34495e; padding: 30px; border-radius: 15px; box-shadow: 0 10px 25px rgba(0,0,0,0.5); }
        .hidden { display: none !important; }

        h1 { margin-top: 0; color: #f1c40f; }
        
        /* Obrazek (Flaga lub Mapa) */
        img { border: 5px solid #ecf0f1; max-height: 200px; max-width: 100%; margin-bottom: 20px; border-radius: 10px; background: white; padding: 10px; }
        
        /* Przyciski w menu i grze */
        .btn-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
        .menu-btn { display: block; width: 100%; margin: 10px 0; padding: 20px; font-size: 18px; font-weight: bold; background: #27ae60; border: none; border-radius: 8px; color: white; cursor: pointer; transition: 0.3s; }
        .menu-btn:hover { background: #2ecc71; transform: scale(1.02); }

        .game-btn { padding: 15px; font-size: 16px; cursor: pointer; background: #2980b9; color: white; border: none; border-radius: 5px; transition: 0.2s; }
        .game-btn:hover { background: #3498db; }

        /* Input dla wariantu 3 */
        input[type="text"] { width: 70%; padding: 15px; font-size: 18px; border-radius: 5px; border: none; margin-bottom: 10px; text-align: center; }
        .submit-btn { padding: 15px 30px; background: #e67e22; color: white; border: none; border-radius: 5px; font-size: 18px; cursor: pointer; }

        /* Sekcja kart bonusowych */
        #bonus-section { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.9); z-index: 100; justify-content: center; align-items: center; flex-direction: column; }
        .cards-container { display: flex; gap: 20px; margin-top: 20px; }
        .card { width: 120px; height: 180px; background: linear-gradient(45deg, #f39c12, #d35400); display: flex; justify-content: center; align-items: center; font-size: 40px; font-weight: bold; cursor: pointer; border: 4px solid white; border-radius: 15px; box-shadow: 0 0 20px rgba(255, 165, 0, 0.6); transition: 0.3s; }
        .card:hover { transform: translateY(-10px); }

        #stats { font-size: 22px; margin-bottom: 20px; background: rgba(0,0,0,0.2); padding: 10px; border-radius: 5px; }
        
        .back-btn { margin-top: 20px; background: #c0392b; width: auto; display: inline-block; padding: 10px 20px; }
    </style>
</head>
<body>

<!-- LOBBY (MENU GŁÓWNE) -->
<div id="lobby" class="screen">
    <h1>🌍 Mistrz Geografii 🌍</h1>
    <p>Wybierz tryb gry:</p>
    <button class="menu-btn" onclick="startGame(1)">Wariant 1: Zgadnij Flagę (Przyciski)</button>
    <button class="menu-btn" onclick="startGame(2)">Wariant 2: Zgadnij Kształt (Przyciski)</button>
    <button class="menu-btn" onclick="startGame(3)">Wariant 3: Zgadnij Flagę (Wpisywanie)</button>
</div>

<!-- EKRAN GRY -->
<div id="game-container" class="screen hidden">
    <div id="stats">
        ❤️ Życia: <span id="lives">3</span> | ⭐ Punkty: <span id="score">0</span>
    </div>

    <h2 id="question-text">Co to za kraj?</h2>
    
    <!-- Obrazek (Flaga lub Kształt) -->
    <img id="game-img" src="" alt="Zagadka">

    <!-- Kontener na przyciski (Wariant 1 i 2) -->
    <div id="answers-grid" class="btn-grid hidden">
        <button class="game-btn" onclick="checkAnswer(0)">A</button>
        <button class="game-btn" onclick="checkAnswer(1)">B</button>
        <button class="game-btn" onclick="checkAnswer(2)">C</button>
        <button class="game-btn" onclick="checkAnswer(3)">D</button>
    </div>
    
    <!-- Kontener na wpisywanie (Wariant 3) -->
    <div id="input-area" class="hidden">
        <input type="text" id="type-answer" placeholder="Wpisz nazwę kraju..." onkeydown="if(event.key === 'Enter') checkTypeAnswer()">
        <br>
        <button class="submit-btn" onclick="checkTypeAnswer()">SPRAWDŹ</button>
    </div>

    <button class="menu-btn back-btn" onclick="goToLobby()">Wróć do menu</button>
</div>

<!-- EKRAN KART BONUSOWYCH -->
<div id="bonus-section">
    <h2 style="color:#2ecc71; font-size: 30px;">DOBRA ODPOWIEDŹ!</h2>
    <p>Wybierz kartę, aby odkryć punkty:</p>
    <div class="cards-container">
        <div class="card" onclick="pickCard(this)">?</div>
        <div class="card" onclick="pickCard(this)">?</div>
        <div class="card" onclick="pickCard(this)">?</div>
    </div>
</div>

<script>
    // BAZA DANYCH KRAJÓW (Kod ISO + Nazwa)
    const countries = [
        { code: 'pl', name: 'Polska' }, { code: 'de', name: 'Niemcy' },
        { code: 'fr', name: 'Francja' }, { code: 'es', name: 'Hiszpania' },
        { code: 'it', name: 'Włochy' }, { code: 'us', name: 'USA' },
        { code: 'gb', name: 'Wielka Brytania' }, { code: 'jp', name: 'Japonia' },
        { code: 'br', name: 'Brazylia' }, { code: 'ca', name: 'Kanada' },
        { code: 'cn', name: 'Chiny' }, { code: 'ru', name: 'Rosja' },
        { code: 'au', name: 'Australia' }, { code: 'in', name: 'Indie' },
        { code: 'mx', name: 'Meksyk' }, { code: 'ar', name: 'Argentyna' },
        { code: 'eg', name: 'Egipt' }, { code: 'za', name: 'RPA' },
        { code: 'kr', name: 'Korea Południowa' }, { code: 'tr', name: 'Turcja' },
        { code: 'ua', name: 'Ukraina' }, { code: 'gr', name: 'Grecja' },
        { code: 'pt', name: 'Portugalia' }, { code: 'se', name: 'Szwecja' },
        { code: 'no', name: 'Norwegia' }, { code: 'fi', name: 'Finlandia' },
        { code: 'dk', name: 'Dania' }, { code: 'nl', name: 'Holandia' },
        { code: 'be', name: 'Belgia' }, { code: 'ch', name: 'Szwajcaria' },
        { code: 'at', name: 'Austria' }, { code: 'cz', name: 'Czechy' },
        { code: 'sk', name: 'Słowacja' }, { code: 'hu', name: 'Węgry' },
        { code: 'ro', name: 'Rumunia' }, { code: 'bg', name: 'Bułgaria' },
        { code: 'hr', name: 'Chorwacja' }, { code: 'ie', name: 'Irlandia' },
        { code: 'th', name: 'Tajlandia' }, { code: 'vn', name: 'Wietnam' }
    ];

    let currentMode = 1;
    let currentCountry;
    let score = 0;
    let lives = 3;
    let correctAnswerIndex;

    // --- FUNKCJE MENU ---

    function startGame(mode) {
        currentMode = mode;
        score = 0;
        lives = 3;
        document.getElementById('score').innerText = score;
        document.getElementById('lives').innerText = lives;

        // Przełącz ekrany
        document.getElementById('lobby').classList.add('hidden');
        document.getElementById('game-container').classList.remove('hidden');

        // Ustaw widok w zależności od trybu
        if (mode === 1 || mode === 2) {
            document.getElementById('answers-grid').classList.remove('hidden');
            document.getElementById('input-area').classList.add('hidden');
        } else {
            document.getElementById('answers-grid').classList.add('hidden');
            document.getElementById('input-area').classList.remove('hidden');
        }

        nextRound();
    }

    function goToLobby() {
        document.getElementById('lobby').classList.remove('hidden');
        document.getElementById('game-container').classList.add('hidden');
    }

    // --- LOGIKA GRY ---

    function nextRound() {
        if (lives <= 0) {
            alert("❌ KONIEC GRY! Twój wynik: " + score);
            goToLobby();
            return;
        }

        // Wylosuj kraj
        currentCountry = countries[Math.floor(Math.random() * countries.length)];
        
        // Wyczyść input
        document.getElementById('type-answer').value = '';

        // Ustaw obrazek w zależności od wariantu
        const imgElement = document.getElementById('game-img');
        
        if (currentMode === 2) {
            // Wariant 2: Mapa (korzystamy z github raw dla kształtów)
            // Uwaga: Niektóre kody w tej bazie mogą się różnić, ale dla większości zadziała
            imgElement.src = `https://raw.githubusercontent.com/djaiss/mapsicon/master/all/${currentCountry.code}/256.png`;
            document.getElementById('question-text').innerText = "Jaki kraj ma taki kształt?";
        } else {
            // Wariant 1 i 3: Flaga
            imgElement.src = `https://flagcdn.com/w320/${currentCountry.code}.png`;
            document.getElementById('question-text').innerText = "Do kogo należy ta flaga?";
        }

        // Jeśli to wariant 1 lub 2, przygotuj przyciski
        if (currentMode === 1 || currentMode === 2) {
            let options = [currentCountry];
            while (options.length < 4) {
                let randomC = countries[Math.floor(Math.random() * countries.length)];
                if (!options.includes(randomC)) {
                    options.push(randomC);
                }
            }
            options.sort(() => Math.random() - 0.5);

            const buttons = document.querySelectorAll('#answers-grid button');
            for (let i = 0; i < 4; i++) {
                buttons[i].innerText = options[i].name;
                // Musimy zresetować onclick, żeby zamknąć starą funkcję w pętli (closure fix)
                buttons[i].onclick = () => checkAnswer(options[i]);
            }
        }
    }

    // Sprawdzanie przycisków (Wariant 1 i 2)
    function checkAnswer(selectedCountry) {
        if (selectedCountry.code === currentCountry.code) {
            showBonusCards();
        } else {
            loseLife();
        }
    }

    // Sprawdzanie wpisywania (Wariant 3)
    function checkTypeAnswer() {
        let text = document.getElementById('type-answer').value.trim();
        // Porównanie bez wielkości liter
        if (text.toLowerCase() === currentCountry.name.toLowerCase()) {
            showBonusCards();
        } else {
            loseLife();
        }
    }

    function loseLife() {
        lives--;
        document.getElementById('lives').innerText = lives;
        alert(`❌ Źle! Poprawna odpowiedź to: ${currentCountry.name}`);
        nextRound();
    }

    // --- KARTY BONUSOWE ---

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
        // Losuj punkty 1-10
        const points = Math.floor(Math.random() * 10) + 1;
        
        cardElement.innerText = "+" + points;
        cardElement.style.background = "#27ae60"; // Zielony
        
        score += points;
        document.getElementById('score').innerText = score;

        // Zablokuj inne karty
        const cards = document.querySelectorAll('.card');
        cards.forEach(c => c.style.pointerEvents = "none");

        // Po chwili następna runda
        setTimeout(() => {
            document.getElementById('bonus-section').style.display = 'none';
            nextRound();
        }, 1500);
    }

</script>

</body>
</html><!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Mistrz Geografii</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; text-align: center; background-color: #2c3e50; color: white; margin: 0; padding: 0; }
        
        /* Styl dla Lobby i Kontenera Gry */
        .screen { max-width: 600px; margin: 50px auto; background: #34495e; padding: 30px; border-radius: 15px; box-shadow: 0 10px 25px rgba(0,0,0,0.5); }
        .hidden { display: none !important; }

        h1 { margin-top: 0; color: #f1c40f; }
        
        /* Obrazek (Flaga lub Mapa) */
        img { border: 5px solid #ecf0f1; max-height: 200px; max-width: 100%; margin-bottom: 20px; border-radius: 10px; background: white; padding: 10px; }
        
        /* Przyciski w menu i grze */
        .btn-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
        .menu-btn { display: block; width: 100%; margin: 10px 0; padding: 20px; font-size: 18px; font-weight: bold; background: #27ae60; border: none; border-radius: 8px; color: white; cursor: pointer; transition: 0.3s; }
        .menu-btn:hover { background: #2ecc71; transform: scale(1.02); }

        .game-btn { padding: 15px; font-size: 16px; cursor: pointer; background: #2980b9; color: white; border: none; border-radius: 5px; transition: 0.2s; }
        .game-btn:hover { background: #3498db; }

        /* Input dla wariantu 3 */
        input[type="text"] { width: 70%; padding: 15px; font-size: 18px; border-radius: 5px; border: none; margin-bottom: 10px; text-align: center; }
        .submit-btn { padding: 15px 30px; background: #e67e22; color: white; border: none; border-radius: 5px; font-size: 18px; cursor: pointer; }

        /* Sekcja kart bonusowych */
        #bonus-section { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.9); z-index: 100; justify-content: center; align-items: center; flex-direction: column; }
        .cards-container { display: flex; gap: 20px; margin-top: 20px; }
        .card { width: 120px; height: 180px; background: linear-gradient(45deg, #f39c12, #d35400); display: flex; justify-content: center; align-items: center; font-size: 40px; font-weight: bold; cursor: pointer; border: 4px solid white; border-radius: 15px; box-shadow: 0 0 20px rgba(255, 165, 0, 0.6); transition: 0.3s; }
        .card:hover { transform: translateY(-10px); }

        #stats { font-size: 22px; margin-bottom: 20px; background: rgba(0,0,0,0.2); padding: 10px; border-radius: 5px; }
        
        .back-btn { margin-top: 20px; background: #c0392b; width: auto; display: # flagi-2
html<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Gra o Krajach</title>
    <style>
        body { font-family: sans-serif; text-align: center; background-color: #f0f0f0; }
        #game-container { max-width: 600px; margin: 0 auto; background: white; padding: 20px; border-radius: 10px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
        img { border: 1px solid #ccc; max-height: 200px; margin-bottom: 20px; }
        .btn-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
        button { padding: 15px; font-size: 16px; cursor: pointer; background: #007bff; color: white; border: none; border-radius: 5px; }
        button:hover { background: #0056b3; }
        
        /* Styl dla sekcji z kartami bonusowymi */
        #bonus-section { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.8); justify-content: center; align-items: center; flex-direction: column; }
        .cards-container { display: flex; gap: 20px; }
        .card { width: 100px; height: 150px; background: orange; display: flex; justify-content: center; align-items: center; font-size: 24px; font-weight: bold; cursor: pointer; border: 3px solid white; border-radius: 10px; }
        
        #stats { font-size: 20px; margin-bottom: 10px; }
        .hidden { display: none; }
    </style>
</head>
<body>

<div id="game-container">
    <h1>Zgadnij Flagę</h1>
    
    <div id="stats">
        Życia: <span id="lives">3</span> | Punkty: <span id="score">0</span>
    </div>

    <!-- Obrazek flagi -->
    <img id="flag-img" src="" alt="Flaga">

    <!-- Przyciski odpowiedzi -->
    <div id="answers" class="btn-grid">
        <button onclick="checkAnswer(0)">Opcja A</button>
        <button onclick="checkAnswer(1)">Opcja B</button>
        <button onclick="checkAnswer(2)">Opcja C</button>
        <button onclick="checkAnswer(3)">Opcja D</button>
    </div>
    
    <!-- Wariant 3: Input (na razie ukryty) -->
    <div id="input-area" class="hidden">
        <input type="text" id="type-answer" placeholder="Wpisz nazwę kraju...">
        <button onclick="checkTypeAnswer()">Zatwierdź</button>
    </div>
</div>

<!-- Ekran wyboru kart -->
<div id="bonus-section">
    <h2 style="color:white">Dobra odpowiedź! Wybierz kartę bonusową:</h2>
    <div class="cards-container">
        <div class="card" onclick="pickCard(this)">?</div>
        <div class="card" onclick="pickCard(this)">?</div>
        <div class="card" onclick="pickCard(this)">?</div>
    </div>
</div>

<script>
    // Baza danych krajów (kod do flagi, nazwa)
    const countries = [
        { code: 'pl', name: 'Polska' },
        { code: 'de', name: 'Niemcy' },
        { code: 'fr', name: 'Francja' },
        { code: 'es', name: 'Hiszpania' },
        { code: 'it', name: 'Włochy' },
        { code: 'us', name: 'USA' },
        { code: 'gb', name: 'Wielka Brytania' },
        { code: 'jp', name: 'Japonia' },
        { code: 'br', name: 'Brazylia' },
        { code: 'ca', name: 'Kanada' }
    ];

    let currentCountry;
    let score = 0;
    let lives = 3;
    let correctAnswerIndex;

    // Funkcja startująca rundę
    function nextRound() {
        if (lives <= 0) {
            alert("Koniec gry! Twój wynik: " + score);
            location.reload(); // Restart gry
            return;
        }

        // 1. Wylosuj poprawny kraj
        currentCountry = countries[Math.floor(Math.random() * countries.length)];
        
        // 2. Ustaw flagę (Wariant 1)
        document.getElementById('flag-img').src = `https://flagcdn.com/w320/${currentCountry.code}.png`;

        // 3. Przygotuj odpowiedzi (1 poprawna, 3 losowe inne)
        let options = [currentCountry];
        while (options.length < 4) {
            let randomC = countries[Math.floor(Math.random() * countries.length)];
            if (!options.includes(randomC)) {
                options.push(randomC);
            }
        }

        // Pomieszaj odpowiedzi
        options.sort(() => Math.random() - 0.5);

        // Wyświetl przyciski
        const buttons = document.querySelectorAll('#answers button');
        for (let i = 0; i < 4; i++) {
            buttons[i].innerText = options[i].name;
            if (options[i].name === currentCountry.name) {
                correctAnswerIndex = i;
            }
        }
    }

    // Sprawdzanie odpowiedzi (Wariant 1 i 2)
    function checkAnswer(index) {
        if (index === correctAnswerIndex) {
            // Pokaż karty bonusowe
            showBonusCards();
        } else {
            // Zła odpowiedź
            lives--;
            document.getElementById('lives').innerText = lives;
            alert(`Źle! To była: ${currentCountry.name}. Tracisz życie.`);
            nextRound();
        }
    }

    // Obsługa kart bonusowych
    function showBonusCards() {
        document.getElementById('bonus-section').style.display = 'flex';
        // Reset kart (zakryj je z powrotem)
        const cards = document.querySelectorAll('.card');
        cards.forEach(card => {
            card.innerText = "?";
            card.style.background = "orange";
            card.style.pointerEvents = "auto"; // odblokuj klikanie
        });
    }

    function pickCard(cardElement) {
        // Losuj punkty od 1 do 10
        const points = Math.floor(Math.random() * 10) + 1;
        
        // Pokaż punkty na karcie
        cardElement.innerText = points;
        cardElement.style.background = "lightgreen";
        
        // Dodaj do wyniku
        score += points;
        document.getElementById('score').innerText = score;

        // Zablokuj inne karty (żeby nie klikać dwa razy)
        const cards = document.querySelectorAll('.card');
        cards.forEach(c => c.style.pointerEvents = "none");

        // Poczekaj chwilę i idź do następnej rundy
        setTimeout(() => {
            document.getElementById('bonus-section').style.display = 'none';
            nextRound();
        }, 1500);
    }

    // Start gry
    nextRound();
</script>

</body>
</html>
