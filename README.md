<!DOCTYPE html>
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
