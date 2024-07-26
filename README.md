<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>德州撲克遊戲</title>
    <style>
        /* 在這裡添加您的CSS樣式 */
        body {
            font-family: Arial, sans-serif;
            text-align: center;
        }
        #game-table {
            width: 800px;
            height: 600px;
            margin: 0 auto;
            background-color: green;
            position: relative;
        }
        .player {
            width: 100px;
            height: 100px;
            position: absolute;
            background-color: #f0f0f0;
            border-radius: 50%;
        }
        #community-cards {
            width: 300px;
            height: 100px;
            background-color: #ddd;
            margin: 20px auto;
        }
    </style>
</head>
<body>
    <h1>德州撲克遊戲</h1>
    <div id="setup">
        <label for="num-players">玩家數量 (2-10): </label>
        <input type="number" id="num-players" min="2" max="10" value="2">
        <label for="starting-chips">起始籌碼: </label>
        <input type="number" id="starting-chips" min="100" value="1000">
        <button onclick="startGame()">開始遊戲</button>
    </div>
    <div id="game-table">
        <!-- 玩家位置將在這裡動態生成 -->
        <div id="community-cards"></div>
    </div>
    <div id="controls" style="display: none;">
        <button onclick="call()">跟注</button>
        <button onclick="raise()">加注</button>
        <button onclick="fold()">棄牌</button>
    </div>

    <script>
        let players = [];
        let currentPlayer = 0;
        let timer;

        function startGame() {
            const numPlayers = document.getElementById('num-players').value;
            const startingChips = document.getElementById('starting-chips').value;
            
            // 清空之前的玩家
            players = [];
            document.getElementById('game-table').innerHTML = '<div id="community-cards"></div>';

            // 生成玩家
            for (let i = 0; i < numPlayers; i++) {
                players.push({
                    id: i,
                    chips: parseInt(startingChips),
                    hand: []
                });
                addPlayerToTable(i);
            }

            document.getElementById('controls').style.display = 'block';
            dealCards();
            startRound();
        }

        function addPlayerToTable(playerId) {
            const gameTable = document.getElementById('game-table');
            const playerElem = document.createElement('div');
            playerElem.className = 'player';
            playerElem.id = `player-${playerId}`;
            playerElem.style.left = `${Math.random() * 700}px`;
            playerElem.style.top = `${Math.random() * 500}px`;
            playerElem.textContent = `玩家 ${playerId + 1}`;
            gameTable.appendChild(playerElem);
        }

        function dealCards() {
            // 這裡應該實現發牌邏輯
            console.log('發牌');
        }

        function startRound() {
            currentPlayer = 0;
            startTurn();
        }

        function startTurn() {
            console.log(`玩家 ${currentPlayer + 1} 的回合`);
            timer = setTimeout(() => {
                // 時間到，自動棄牌
                fold();
            }, 60000); // 60秒
        }

        function endTurn() {
            clearTimeout(timer);
            currentPlayer = (currentPlayer + 1) % players.length;
            startTurn();
        }

        function call() {
            console.log(`玩家 ${currentPlayer + 1} 跟注`);
            endTurn();
        }

        function raise() {
            console.log(`玩家 ${currentPlayer + 1} 加注`);
            endTurn();
        }

        function fold() {
            console.log(`玩家 ${currentPlayer + 1} 棄牌`);
            endTurn();
        }

        // 這裡應該添加更多遊戲邏輯，如計算勝者、處理籌碼等
    </script>
</body>
</html>
