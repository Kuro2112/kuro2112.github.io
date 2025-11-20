<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crossword Puzzle</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
            background-size: 400% 400%;
            animation: gradientShift 15s ease infinite;
            padding: 20px;
        }
        
        @keyframes gradientShift {
            0% {
                background-position: 0% 50%;
            }
            50% {
                background-position: 100% 50%;
            }
            100% {
                background-position: 0% 50%;
            }
        }
        
        .container {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.2);
        }
        
        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 20px;
        }
        
        .grid {
            display: inline-block;
            background: #333;
        }
        
        .row {
            display: flex;
            line-height: 0;
        }
        
        .cell {
            width: 40px;
            height: 40px;
            border: 1px solid #666;
            background: white;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            font-weight: bold;
            text-transform: uppercase;
            position: relative;
            vertical-align: top;
            box-sizing: border-box;
        }
        
        .cell input {
            width: 100%;
            height: 100%;
            border: none;
            text-align: center;
            font-size: 18px;
            font-weight: bold;
            text-transform: uppercase;
            background: transparent;
        }
        
        .cell input:focus {
            outline: 2px solid #667eea;
            background: #f0f4ff;
        }
        
        .cell.black {
            background: #333;
        }
        
        .cell.empty {
            background: transparent;
            border: none;
        }
        
        .clue-display {
            margin-top: 20px;
            padding: 15px;
            background: #f0f4ff;
            border-radius: 8px;
            min-height: 60px;
            border: 2px solid #667eea;
        }
        
        .clue-display h4 {
            margin: 0 0 10px 0;
            color: #667eea;
        }
        
        .clue-display p {
            margin: 0;
            color: #333;
            font-size: 16px;
        }
        
        .clue-display.empty {
            display: flex;
            align-items: center;
            justify-content: center;
            color: #999;
            font-style: italic;
        }
        
        .clue-buttons {
            margin-top: 20px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }
        
        .clue-section {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        .clue-section h3 {
            color: #667eea;
            margin: 0 0 15px 0;
            font-size: 18px;
        }
        
        .clue-btn {
            display: inline-block;
            padding: 8px 14px;
            margin: 4px;
            background: #f8f9ff;
            border: 2px solid #e0e7ff;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 14px;
            color: #333;
        }
        
        .clue-btn:hover {
            background: #e0e7ff;
            border-color: #667eea;
            transform: translateX(3px);
        }
        
        .clue-btn.active {
            background: #667eea;
            color: white;
            border-color: #667eea;
        }
        
        .clues {
            margin-top: 30px;
            display: none;
        }
        
        .clue-section ul {
            list-style: none;
            padding: 0;
        }
        
        .clue-section li {
            margin-bottom: 8px;
            color: #555;
        }
        
        button {
            margin-top: 20px;
            padding: 12px 30px;
            background: #667eea;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            display: block;
            margin-left: auto;
            margin-right: auto;
        }
        
        button:hover {
            background: #5568d3;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🧩 Crossword Puzzle</h1>
        
        <div class="grid" id="crossword"></div>
        
        <!-- Khu bấm chọn Hàng/Cột bên ngoài -->
        <div class="clue-buttons">
            <div class="clue-section">
                <h3>🡢 Hàng ngang</h3>
                <div id="acrossButtons"></div>
            </div>
            <div class="clue-section">
                <h3>🡣 Cột dọc</h3>
                <div id="downButtons"></div>
            </div>
        </div>
        
        <div class="clue-display" id="clueDisplay">
            <p>👆 Click vào Hàng / Cột bên trên hoặc một ô trong bảng để xem câu hỏi</p>
        </div>
        
        <button onclick="checkAnswers()">Kiểm tra đáp án</button>
    </div>

    <script>
        // Grid structure based on the image (1 = white cell, 0 = empty)
        const grid = [
            [0, 0, 0, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0],
            [0, 0, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 0, 0],
            [0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1],
            [0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0],
            [0, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0],
            [0, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0]
        ];

        // Clues with positions
        const clues = {
            'across': {
                1: { text: 'Thủ đô của Việt Nam', row: 0, col: 3 },
                2: { text: 'Con vật có vòi dài', row: 1, col: 2 },
                3: { text: 'Hành tinh chúng ta đang sống', row: 2, col: 5 },
                4: { text: 'Đại dương lớn nhất thế giới', row: 3, col: 6 },
                5: { text: 'Màu của bầu trời', row: 4, col: 3 },
                6: { text: 'Thủ đô của Nhật Bản', row: 5, col: 1 },
                7: { text: 'Người dạy học', row: 6, col: 1 }
            },
            'down': {
                1: { text: 'Câu hỏi cột dọc', row: 0, col: 6 }
            }
        };

        function createGrid() {
            const crossword = document.getElementById('crossword');
            
            grid.forEach((row, rowIndex) => {
                const rowDiv = document.createElement('div');
                rowDiv.className = 'row';
                
                row.forEach((cell, colIndex) => {
                    const cellDiv = document.createElement('div');
                    cellDiv.className = 'cell';
                    
                    if (cell === 0) {
                        cellDiv.classList.add('empty');
                    } else {
                        const input = document.createElement('input');
                        input.maxLength = 1;
                        input.dataset.row = rowIndex;
                        input.dataset.col = colIndex;
                        
                        input.addEventListener('input', (e) => {
                            e.target.value = e.target.value.toUpperCase();
                            moveToNext(rowIndex, colIndex);
                        });
                        
                        input.addEventListener('focus', () => {
                            showClue(rowIndex, colIndex);
                        });
                        
                        cellDiv.appendChild(input);
                    }
                    
                    rowDiv.appendChild(cellDiv);
                });
                
                crossword.appendChild(rowDiv);
            });
            
            createClueButtons();
        }
        
        // Tạo nút Hàng 1, Hàng 2... và Cột dọc
        function createClueButtons() {
            const acrossDiv = document.getElementById('acrossButtons');
            const downDiv = document.getElementById('downButtons');

            // HÀNG NGANG: Hàng 1, Hàng 2, ...
            const acrossKeys = Object.keys(clues.across);
            acrossKeys.forEach(num => {
                const btn = document.createElement('button');
                btn.className = 'clue-btn';
                btn.textContent = 'Hàng ' + num;
                btn.addEventListener('click', (e) => {
                    selectClue('across', num, e.currentTarget);
                });
                acrossDiv.appendChild(btn);
            });

            // HÀNG DỌC - CHỈ 1 CÂU
            const btn = document.createElement('button');
            btn.className = 'clue-btn';
            btn.textContent = 'Cột dọc';
            btn.addEventListener('click', (e) => {
                selectClue('down', 1, e.currentTarget);
            });
            downDiv.appendChild(btn);
        }
        
        function selectClue(direction, num, clickedButton) {
            // Bỏ active trên tất cả nút
            document.querySelectorAll('.clue-btn').forEach(btn => btn.classList.remove('active'));

            // Thêm active cho nút vừa bấm
            if (clickedButton) {
                clickedButton.classList.add('active');
            }

            const clue = clues[direction][num];
            const clueDisplay = document.getElementById('clueDisplay');
            const directionSymbol = direction === 'across' ? '🡢' : '🡣';
            const directionText = direction === 'across' ? 'Ngang' : 'Dọc';
            
            clueDisplay.innerHTML = `<h4>${directionSymbol} ${directionText} ${num}</h4><p>${clue.text}</p>`;
            
            // Focus vào ô đầu tiên của từ đó
            const inputs = document.querySelectorAll('.cell input');
            for (let input of inputs) {
                if (parseInt(input.dataset.row) === clue.row && 
                    parseInt(input.dataset.col) === clue.col) {
                    input.focus();
                    break;
                }
            }
        }

        function showClue(row, col) {
            const clueDisplay = document.getElementById('clueDisplay');
            let foundClue = false;
            
            // Check for across clue
            for (let num in clues.across) {
                const clue = clues.across[num];
                if (clue.row === row && col >= clue.col && col < clue.col + 10) {
                    clueDisplay.innerHTML = `<h4>🡢 Ngang ${num}</h4><p>${clue.text}</p>`;
                    
                    // Highlight nút tương ứng
                    document.querySelectorAll('.clue-btn').forEach(btn => btn.classList.remove('active'));
                    const btns = document.querySelectorAll('#acrossButtons .clue-btn');
                    const index = Object.keys(clues.across).indexOf(num);
                    if (btns[index]) btns[index].classList.add('active');
                    
                    foundClue = true;
                    break;
                }
            }
            
            // Check for down clue - CHỈ CÓ 1 CỘT DỌC TẠI COL = 6
            if (!foundClue) {
                const clue = clues.down[1];
                if (col === clue.col && row >= clue.row && row <= 6) {
                    clueDisplay.innerHTML = `<h4>🡣 Dọc 1</h4><p>${clue.text}</p>`;
                    
                    // Highlight nút cột dọc
                    document.querySelectorAll('.clue-btn').forEach(btn => btn.classList.remove('active'));
                    const downBtn = document.querySelector('#downButtons .clue-btn');
                    if (downBtn) downBtn.classList.add('active');
                    
                    foundClue = true;
                }
            }
            
            if (!foundClue) {
                clueDisplay.innerHTML = '<p>👆 Click vào Hàng / Cột bên trên hoặc một ô để xem câu hỏi</p>';
                document.querySelectorAll('.clue-btn').forEach(btn => btn.classList.remove('active'));
            }
        }

        function moveToNext(row, col) {
            const cells = document.querySelectorAll('.cell input');
            let currentFound = false;
            
            for (let cell of cells) {
                if (currentFound && cell.value === '') {
                    cell.focus();
                    return;
                }
                if (parseInt(cell.dataset.row) === row && parseInt(cell.dataset.col) === col) {
                    currentFound = true;
                }
            }
        }

        function checkAnswers() {
            const inputs = document.querySelectorAll('.cell input');
            let allFilled = true;
            
            inputs.forEach(input => {
                if (input.value === '') {
                    allFilled = false;
                }
            });
            
            if (allFilled) {
                alert('🎉 Chúc mừng! Bạn đã hoàn thành crossword puzzle!');
            } else {
                alert('📝 Hãy điền đầy đủ tất cả các ô trước khi kiểm tra!');
            }
        }

        createGrid();
    </script>
</body>
</html>
