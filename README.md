<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mistrz Geografii (Jasny + Czarny Ranking)</title>
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
            padding: 15px; font-size: 16px; cursor: pointer; 
            background: #2980b9; color: white; border: none; border-radius: 5px; 
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

        /* --- STYL TABELI RANKINGOWEJ --- */
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
        
        /* KOLORY DLA MIEJSC 1, 2, 3 (Podium) */
        tr:nth-child(1) td { color: #f39c12; font-weight: bold; } /* Złoto */
        tr:nth-child(2) td { color: #7f8c8d; font-weight: bold; } /* Srebro */
        tr:nth-child(3) td { color: #a0522d; font-weight: bold; } /* Brąz */

        /* KOLORY DLA MIEJSC 4 i 5 (Reszta) - TU ZMIANA NA CZARNY */
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
            background: linear-gradient(45deg, #f39c12, 
