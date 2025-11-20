<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🧩 Crossword Puzzle - Interactive Challenge</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700;800&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Poppins', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            background: #0f0c29;
            background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
            padding: 20px;
            position: relative;
            overflow-x: hidden;
        }
        
        /* ANIMATED BACKGROUND SHAPES */
        .bg-shapes {
            position: fixed;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            z-index: 0;
            overflow: hidden;
        }
        
        .shape {
            position: absolute;
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0.05));
            backdrop-filter: blur(10px);
            border-radius: 50%;
            animation: float 20s infinite ease-in-out;
        }
        
        .shape:nth-child(1) {
            width: 300px;
            height: 300px;
            top: 10%;
            left: 10%;
            animation-delay: 0s;
        }
        
        .shape:nth-child(2) {
            width: 200px;
            height: 200px;
            top: 60%;
            right: 10%;
            animation-delay: 2s;
        }
        
        .shape:nth-child(3) {
            width: 150px;
            height: 150px;
            bottom: 10%;
            left: 20%;
            animation-delay: 4s;
        }
        
        @keyframes float {
            0%, 100% {
                transform: translate(0, 0) rotate(0deg);
            }
            33% {
                transform: translate(30px, -50px) rotate(120deg);
            }
            66% {
                transform: translate(-20px, 20px) rotate(240deg);
            }
        }
        
        /* GLASSMORPHISM CONTAINER */
        .container {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px) saturate(180%);
            -webkit-backdrop-filter: blur(20px) saturate(180%);
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 25px 80px rgba(0, 0, 0, 0.4),
                        0 0 60px rgba(102, 126, 234, 0.3) inset;
            position: relative;
            z-index: 1;
            border: 2px solid rgba(255, 255, 255, 0.2);
            animation: slideInUp 0.8s ease-out;
        }
        
        @keyframes slideInUp {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        /* NEON TITLE */
        h1 {
            text-align: center;
            font-size: 48px;
            font-weight: 800;
            margin-bottom: 30px;
            color: #fff;
            text-shadow: 0 0 10px #667eea,
                         0 0 20px #667eea,
                         0 0 30px #667eea,
                         0 0 40px #667eea;
            letter-spacing: 2px;
            animation: neonPulse 2s ease-in-out infinite alternate;
        }
        
        @keyframes neonPulse {
            from {
                text-shadow: 0 0 10px #667eea,
                             0 0 20px #667eea,
                             0 0 30px #667eea;
            }
            to {
                text-shadow: 0 0 15px #667eea,
                             0 0 30px #667eea,
                             0 0 50px #667eea,
                             0 0 70px #764ba2;
            }
        }
        
        /* 3D GRID EFFECT */
        .grid-wrapper {
            perspective: 1000px;
            display: inline-block;
        }
        
        .grid {
            display: inline-block;
            background: rgba(42, 42, 42, 0.8);
            backdrop-filter: blur(10px);
            padding: 8px;
            border-radius: 15px;
            box-shadow: 0 15px 50px rgba(0, 0, 0, 0.5),
                        0 0 40px rgba(102, 126, 234, 0.2) inset;
            transform-style: preserve-3d;
            transition: transform 0.3s ease;
        }
        
        .grid:hover {
            transform: rotateX(2deg) rotateY(2deg);
        }
        
        .row {
            display: flex;
            line-height: 0;
            position: relative;
        }
        
        /* FUTURISTIC CELLS */
        .cell {
            width: 50px;
            height: 50px;
            border: 2px solid rgba(102, 126, 234, 0.3);
            background: rgba(255, 255, 255, 0.95);
            display: inline-flex;
            align-items: center;
            justify-content: center;
            font-size: 22px;
            font-weight: 700;
            text-transform: uppercase;
            position: relative;
            box-sizing: border-box;
            transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            overflow: hidden;
        }
        
        .cell::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(102, 126, 234, 0.3), transparent);
            transform: rotate(45deg);
            transition: all 0.5s;
        }
        
        .cell:hover::before {
            animation: shine 0.8s ease;
        }
        
        @keyframes shine {
            0% {
                top: -50%;
                left: -50%;
            }
            100% {
                top: 150%;
                left: 150%;
            }
        }
        
        .cell input {
            width: 100%;
            height: 100%;
            border: none;
            text-align: center;
            font-size: 22px;
            font-weight: 700;
            text-transform: uppercase;
            background: transparent;
            color: #1a1a2e;
            z-index: 1;
            transition: all 0.3s ease;
        }
        
        .cell input:focus {
            outline: none;
            background: linear-gradient(135deg, rgba(102, 126, 234, 0.2), rgba(118, 75, 162, 0.2));
            transform: scale(1.15);
            box-shadow: 0 0 30px rgba(102, 126, 234, 0.8),
                        0 0 60px rgba(102, 126, 234, 0.4) inset;
            z-index: 10;
            color: #fff;
            font-weight: 800;
        }
        
        .cell input:disabled {
            background: rgba(200, 200, 200, 0.3);
            cursor: not-allowed;
            color: #666;
        }
        
        .cell input.correct {
            background: linear-gradient(135deg, #4ade80, #22c55e, #16a34a) !important;
            color: white;
            animation: correctExplosion 0.6s ease;
            box-shadow: 0 0 20px #4ade80;
        }
        
        @keyframes correctExplosion {
            0% {
                transform: scale(0.8);
                box-shadow: 0 0 0 rgba(74, 222, 128, 0);
            }
            50% {
                transform: scale(1.3);
                box-shadow: 0 0 40px rgba(74, 222, 128, 1);
            }
            100% {
                transform: scale(1);
                box-shadow: 0 0 20px rgba(74, 222, 128, 0.8);
            }
        }
        
        .cell input.typing {
            animation: typeFlash 0.3s ease;
        }
        
        @keyframes typeFlash {
            0%, 100% {
                box-shadow: 0 0 0 rgba(102, 126, 234, 0);
            }
            50% {
                box-shadow: 0 0 30px rgba(102, 126, 234, 1),
                            0 0 60px rgba(118, 75, 162, 0.5);
            }
        }
        
        .cell.empty {
            background: transparent;
            border: none;
        }
        
        /* FUTURISTIC CONFIRM BUTTON */
        .confirm-btn {
            position: absolute;
            right: -100px;
            top: 50%;
            transform: translateY(-50%);
            padding: 12px 22px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 30px;
            cursor: pointer;
            font-size: 15px;
            font-weight: 700;
            display: none;
            transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            box-shadow: 0 8px 25px rgba(102, 126, 234, 0.5);
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        
        .confirm-btn:hover {
            transform: translateY(-50%) scale(1.1);
            box-shadow: 0 12px 40px rgba(102, 126, 234, 0.8);
            background: linear-gradient(135deg, #764ba2, #667eea);
        }
        
        .confirm-btn.show {
            display: block;
            animation: bounceIn 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }
        
        @keyframes bounceIn {
            0% {
                opacity: 0;
                right: -150px;
                transform: translateY(-50%) scale(0.3);
            }
            50% {
                transform: translateY(-50%) scale(1.1);
            }
            100% {
                opacity: 1;
                right: -100px;
                transform: translateY(-50%) scale(1);
            }
        }
        
        /* MODAL STYLES */
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background: rgba(15, 12, 41, 0.95);
            animation: fadeIn 0.3s;
            backdrop-filter: blur(10px);
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .modal-content {
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.15), rgba(255, 255, 255, 0.05));
            backdrop-filter: blur(30px) saturate(200%);
            margin: 12% auto;
            padding: 45px;
            border-radius: 30px;
            width: 85%;
            max-width: 600px;
            box-shadow: 0 25px 100px rgba(0, 0, 0, 0.6),
                        0 0 80px rgba(102, 126, 234, 0.3) inset;
            animation: modalZoomIn 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            border: 3px solid rgba(255, 255, 255, 0.2);
            position: relative;
            overflow: hidden;
        }
        
        .modal-content::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
            animation: shimmer 3s infinite;
        }
        
        @keyframes shimmer {
            to {
                left: 100%;
            }
        }
        
        @keyframes modalZoomIn {
            from {
                transform: scale(0.5) rotateX(30deg);
                opacity: 0;
            }
            to {
                transform: scale(1) rotateX(0);
                opacity: 1;
            }
        }
        
        .modal-content h2 {
            color: #fff;
            margin: 0 0 25px 0;
            font-size: 36px;
            font-weight: 800;
            text-shadow: 0 0 20px rgba(102, 126, 234, 0.8);
            z-index: 1;
            position: relative;
        }
        
        .modal-content p {
            color: rgba(255, 255, 255, 0.95);
            font-size: 22px;
            line-height: 1.7;
            z-index: 1;
            position: relative;
        }
        
        .close {
            color: rgba(255, 255, 255, 0.7);
            float: right;
            font-size: 40px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            z-index: 2;
            position: relative;
        }
        
        .close:hover {
            color: #fff;
            transform: rotate(90deg) scale(1.2);
            text-shadow: 0 0 20px #667eea;
        }
        
        /* SUCCESS MODAL */
        .success-modal {
            display: none;
            position: fixed;
            z-index: 2000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background: rgba(15, 12, 41, 0.95);
            backdrop-filter: blur(15px);
        }
        
        .success-content {
            background: linear-gradient(135deg, #667eea, #764ba2, #f093fb);
            background-size: 200% 200%;
            animation: gradientMove 3s ease infinite, successZoom 0.7s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            margin: 15% auto;
            padding: 60px;
            border-radius: 40px;
            width: 85%;
            max-width: 500px;
            text-align: center;
            color: white;
            box-shadow: 0 30px 120px rgba(102, 126, 234, 0.8);
            border: 3px solid rgba(255, 255, 255, 0.4);
        }
        
        @keyframes gradientMove {
            0%, 100% {
                background-position: 0% 50%;
            }
            50% {
                background-position: 100% 50%;
            }
        }
        
        @keyframes successZoom {
            0% {
                transform: scale(0) rotate(-180deg);
                opacity: 0;
            }
            70% {
                transform: scale(1.2) rotate(10deg);
            }
            100% {
                transform: scale(1) rotate(0);
                opacity: 1;
            }
        }
        
        .success-content h2 {
            font-size: 90px;
            margin: 0 0 25px 0;
            animation: celebrate 1s ease infinite;
            filter: drop-shadow(0 0 20px rgba(255, 255, 255, 0.8));
        }
        
        @keyframes celebrate {
            0%, 100% {
                transform: scale(1) rotate(-10deg);
            }
            50% {
                transform: scale(1.2) rotate(10deg);
            }
        }
        
        .success-content p {
            font-size: 32px;
            margin: 0;
            font-weight: 700;
            text-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
        }
        
        /* CLUE BUTTONS */
        .clue-buttons {
            margin-top: 30px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
        }
        
        .clue-section {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(15px);
            padding: 25px;
            border-radius: 20px;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3),
                        0 0 40px rgba(102, 126, 234, 0.2) inset;
            border: 2px solid rgba(255, 255, 255, 0.2);
            transition: all 0.3s ease;
        }
        
        .clue-section:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 35px rgba(0, 0, 0, 0.4),
                        0 0 60px rgba(102, 126, 234, 0.3) inset;
        }
        
        .clue-section h3 {
            color: #fff;
            margin: 0 0 20px 0;
            font-size: 22px;
            font-weight: 700;
            text-shadow: 0 0 10px rgba(102, 126, 234, 0.8);
        }
        
        .clue-btn {
            display: inline-block;
            padding: 12px 20px;
            margin: 6px;
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            font-size: 16px;
            color: #fff;
            font-weight: 600;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .clue-btn:hover {
            background: linear-gradient(135deg, #667eea, #764ba2);
            border-color: rgba(255, 255, 255, 0.5);
            transform: translateY(-4px);
            box-shadow: 0 8px 25px rgba(102, 126, 234, 0.6);
        }
        
        .clue-btn.active {
            background: linear-gradient(135deg, #667eea, #764ba2);
            border-color: #fff;
            box-shadow: 0 8px 30px rgba(102, 126, 234, 0.7),
                        0 0 40px rgba(255, 255, 255, 0.3) inset;
            transform: scale(1.05);
        }
        
        .clue-btn.completed {
            background: linear-gradient(135deg, #4ade80, #22c55e);
            border-color: #fff;
            box-shadow: 0 8px 30px rgba(74, 222, 128, 0.7);
            animation: pulse 2s ease infinite;
        }
        
        @keyframes pulse {
            0%, 100% {
                box-shadow: 0 8px 30px rgba(74, 222, 128, 0.7);
            }
            50% {
                box-shadow: 0 8px 40px rgba(74, 222, 128, 1);
            }
        }
        
        button.check-all {
            margin-top: 30px;
            padding: 18px 45px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: 3px solid rgba(255, 255, 255, 0.4);
            border-radius: 40px;
            font-size: 20px;
            cursor: pointer;
            display: block;
            margin-left: auto;
            margin-right: auto;
            font-weight: 700;
            transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            box-shadow: 0 8px 30px rgba(102, 126, 234, 0.6);
            text-transform: uppercase;
            letter-spacing: 2px;
        }
        
        button.check-all:hover {
            transform: translateY(-5px) scale(1.05);
            box-shadow: 0 15px 50px rgba(102, 126, 234, 0.9);
            background: linear-gradient(135deg, #764ba2, #667eea);
        }
        
        button.check-all:active {
            transform: translateY(-2px) scale(1.02);
        }
    </style>
</head>
<body>
    <!-- ANIMATED BACKGROUND SHAPES -->
    <div class="bg-shapes">
        <div class="shape"></div>
        <div class="shape"></div>
        <div class="shape"></div>
    </div>
    
    <!-- PARTICLES BACKGROUND -->
    <div id="particles-js"></div>
    
    <div class="container">
        <h1>🧩 CROSSWORD PUZZLE</h1>
        
        <div class="grid-wrapper">
            <div class="grid" id="crossword"></div>
        </div>
        
        <div class="clue-buttons">
            <div class="clue-section">
                <h3>🡢 HÀNG NGANG</h3>
                <div id="acrossButtons"></div>
            </div>
            <div class="clue-section">
                <h3>🡣 CỘT DỌC</h3>
                <div id="downButtons"></div>
            </div>
        </div>
        
        <button class="check-all" onclick="checkAllAnswers()">✨ KIỂM TRA TẤT CẢ</button>
    </div>

    <!-- MODAL POPUP -->
    <div id="clueModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal()">&times;</span>
            <h2 id="modalTitle">CÂU HỎI</h2>
            <p id="modalText">Nội dung câu hỏi sẽ hiển thị ở đây</p>
        </div>
    </div>

    <!-- SUCCESS MODAL -->
    <div id="successModal" class="success-modal">
        <div class="success-content">
            <h2>🎉</h2>
            <p>CHÚC MỪNG!<br>CHÍNH XÁC!</p>
        </div>
    </div>

    <!-- PARTICLES.JS -->
    <script src="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js"></script>
    <script>
        // PARTICLES CONFIGURATION
        particlesJS('particles-js', {
            particles: {
                number: { value: 100, density: { enable: true, value_area: 800 } },
                color: { value: '#667eea' },
                shape: { type: 'circle' },
                opacity: { value: 0.6, random: true },
                size: { value: 4, random: true },
                line_linked: { enable: true, distance: 150, color: '#667eea', opacity: 0.5, width: 2 },
                move: { enable: true, speed: 2.5, direction: 'none', random: true, out_mode: 'out' }
            },
            interactivity: {
                detect_on: 'canvas',
                events: {
                    onhover: { enable: true, mode: 'grab' },
                    onclick: { enable: true, mode: 'push' }
                },
                modes: {
                    grab: { distance: 200, line_linked: { opacity: 0.8 } },
                    push: { particles_nb: 4 }
                }
            }
        });

        const grid = [
            [0, 0, 0, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0],
            [0, 0, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0],
            [0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 0, 0],
            [0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1],
            [0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0],
            [0, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0],
            [0, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0]
        ];

        const clues = {
            'across': {
                1: { text: 'Thủ đô của Việt Nam', row: 0, col: 3, answer: 'HANOI', length: 5 },
                2: { text: 'Con vật có vòi dài', row: 1, col: 2, answer: 'ELEPHANT', length: 6 },
                3: { text: 'Hành tinh chúng ta đang sống', row: 2, col: 5, answer: 'EARTH', length: 7 },
                4: { text: 'Đại dương lớn nhất thế giới', row: 3, col: 6, answer: 'PACIFIC', length: 8 },
                5: { text: 'Màu của bầu trời', row: 4, col: 3, answer: 'BLUE', length: 9 },
                6: { text: 'Thủ đô của Nhật Bản', row: 5, col: 1, answer: 'TOKYO', length: 6 },
                7: { text: 'Người dạy học', row: 6, col: 1, answer: 'TEACHER', length: 6 }
            },
            'down': {
                1: { text: 'Câu hỏi cột dọc', row: 0, col: 6, answer: 'VERTICAL', length: 7 }
            }
        };

        let currentSelectedRow = null;
        let currentSelectedDirection = null;
        let currentSelectedNum = null;
        let completedClues = new Set();

        function openModal(direction, num) {
            const modal = document.getElementById('clueModal');
            const modalTitle = document.getElementById('modalTitle');
            const modalText = document.getElementById('modalText');
            
            const clue = clues[direction][num];
            const directionSymbol = direction === 'across' ? '🡢' : '🡣';
            const directionText = direction === 'across' ? 'NGANG' : 'DỌC';
            
            modalTitle.textContent = `${directionSymbol} ${directionText} ${num}`;
            modalText.textContent = clue.text;
            modal.style.display = 'block';
        }

        function closeModal() {
            document.getElementById('clueModal').style.display = 'none';
        }

        function showSuccessModal() {
            const modal = document.getElementById('successModal');
            modal.style.display = 'block';
            setTimeout(() => {
                modal.style.display = 'none';
            }, 2500);
        }

        window.onclick = function(event) {
            const modal = document.getElementById('clueModal');
            if (event.target === modal) closeModal();
        }

        function createGrid() {
            const crossword = document.getElementById('crossword');
            
            grid.forEach((row, rowIndex) => {
                const rowDiv = document.createElement('div');
                rowDiv.className = 'row';
                rowDiv.dataset.row = rowIndex;
                
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
                        input.disabled = true;
                        
                        input.addEventListener('keydown', (e) => handleKeyDown(e, rowIndex, colIndex));
                        
                        input.addEventListener('input', (e) => {
                            e.target.value = e.target.value.toUpperCase();
                            e.target.classList.add('typing');
                            setTimeout(() => e.target.classList.remove('typing'), 300);
                            if (e.target.value) checkRowComplete();
                        });
                        
                        cellDiv.appendChild(input);
                    }
                    
                    rowDiv.appendChild(cellDiv);
                });
                
                const confirmBtn = document.createElement('button');
                confirmBtn.className = 'confirm-btn';
                confirmBtn.innerHTML = '✓ XÁC NHẬN';
                confirmBtn.dataset.row = rowIndex;
                confirmBtn.onclick = () => confirmAnswer(rowIndex);
                rowDiv.appendChild(confirmBtn);
                
                crossword.appendChild(rowDiv);
            });
            
            createClueButtons();
        }
        
        function checkRowComplete() {
            if (currentSelectedDirection !== 'across' || currentSelectedNum === null) return;
            
            const clue = clues.across[currentSelectedNum];
            const inputs = getRowInputs(clue.row, clue.col, clue.length);
            const allFilled = inputs.every(input => input.value !== '');
            const confirmBtn = document.querySelector(`.confirm-btn[data-row="${clue.row}"]`);
            
            if (allFilled) confirmBtn.classList.add('show');
            else confirmBtn.classList.remove('show');
        }
        
        function getRowInputs(row, startCol, length) {
            const inputs = [];
            document.querySelectorAll('.cell input').forEach(input => {
                const inputRow = parseInt(input.dataset.row);
                const inputCol = parseInt(input.dataset.col);
                if (inputRow === row && inputCol >= startCol && inputCol < startCol + length) {
                    inputs.push(input);
                }
            });
            return inputs.sort((a, b) => parseInt(a.dataset.col) - parseInt(b.dataset.col));
        }
        
        function confirmAnswer(row) {
            if (currentSelectedNum === null || currentSelectedDirection !== 'across') return;
            
            const clue = clues.across[currentSelectedNum];
            if (clue.row !== row) return;
            
            const inputs = getRowInputs(clue.row, clue.col, clue.length);
            const userAnswer = inputs.map(input => input.value).join('');
            
            if (userAnswer === clue.answer) {
                inputs.forEach(input => {
                    input.classList.add('correct');
                    input.disabled = true;
                });
                
                document.querySelector(`.confirm-btn[data-row="${row}"]`).classList.remove('show');
                completedClues.add(`across-${currentSelectedNum}`);
                updateClueButtonStatus(currentSelectedDirection, currentSelectedNum);
                showSuccessModal();
                
                currentSelectedRow = null;
                currentSelectedDirection = null;
                currentSelectedNum = null;
            } else {
                alert('❌ Câu trả lời chưa chính xác. Hãy thử lại!');
            }
        }
        
        function updateClueButtonStatus(direction, num) {
            document.querySelectorAll('.clue-btn').forEach(btn => {
                if (btn.dataset.direction === direction && btn.dataset.num == num) {
                    btn.classList.add('completed');
                    btn.style.pointerEvents = 'none';
                }
            });
        }
        
        function handleKeyDown(e, row, col) {
            const key = e.key;
            
            if (key === 'Backspace' && e.target.value === '') {
                e.preventDefault();
                moveToPrevious(row, col);
            } else if (key === 'ArrowRight') {
                e.preventDefault();
                moveRight(row, col);
            } else if (key === 'ArrowLeft') {
                e.preventDefault();
                moveLeft(row, col);
            } else if (key === 'ArrowDown') {
                e.preventDefault();
                moveDown(row, col);
            } else if (key === 'ArrowUp') {
                e.preventDefault();
                moveUp(row, col);
            }
        }

        function moveRight(row, col) {
            const inputs = Array.from(document.querySelectorAll('.cell input:not(:disabled)'));
            for (let input of inputs) {
                if (parseInt(input.dataset.row) === row && parseInt(input.dataset.col) > col) {
                    input.focus();
                    return;
                }
            }
        }

        function moveLeft(row, col) {
            const inputs = Array.from(document.querySelectorAll('.cell input:not(:disabled)')).reverse();
            for (let input of inputs) {
                if (parseInt(input.dataset.row) === row && parseInt(input.dataset.col) < col) {
                    input.focus();
                    return;
                }
            }
        }

        function moveDown(row, col) {
            const inputs = Array.from(document.querySelectorAll('.cell input:not(:disabled)'));
            for (let input of inputs) {
                if (parseInt(input.dataset.col) === col && parseInt(input.dataset.row) > row) {
                    input.focus();
                    return;
                }
            }
        }

        function moveUp(row, col) {
            const inputs = Array.from(document.querySelectorAll('.cell input:not(:disabled)')).reverse();
            for (let input of inputs) {
                if (parseInt(input.dataset.col) === col && parseInt(input.dataset.row) < row) {
                    input.focus();
                    return;
                }
            }
        }

        function moveToPrevious(row, col) {
            const cells = Array.from(document.querySelectorAll('.cell input:not(:disabled)')).reverse();
            let currentFound = false;
            
            for (let cell of cells) {
                if (currentFound) {
                    cell.focus();
                    cell.value = '';
                    return;
                }
                if (parseInt(cell.dataset.row) === row && parseInt(cell.dataset.col) === col) {
                    currentFound = true;
                }
            }
        }
        
        function createClueButtons() {
            const acrossDiv = document.getElementById('acrossButtons');
            const downDiv = document.getElementById('downButtons');

            Object.keys(clues.across).forEach(num => {
                const btn = document.createElement('button');
                btn.className = 'clue-btn';
                btn.textContent = 'Hàng ' + num;
                btn.dataset.direction = 'across';
                btn.dataset.num = num;
                btn.addEventListener('click', (e) => selectClue('across', num, e.currentTarget));
                acrossDiv.appendChild(btn);
            });

            const btn = document.createElement('button');
            btn.className = 'clue-btn';
            btn.textContent = 'Cột dọc';
            btn.dataset.direction = 'down';
            btn.dataset.num = 1;
            btn.addEventListener('click', (e) => selectClue('down', 1, e.currentTarget));
            downDiv.appendChild(btn);
        }
        
        function selectClue(direction, num, clickedButton) {
            if (completedClues.has(`${direction}-${num}`)) return;
            
            document.querySelectorAll('.clue-btn').forEach(btn => btn.classList.remove('active'));
            if (clickedButton) clickedButton.classList.add('active');

            openModal(direction, num);
            
            const clue = clues[direction][num];
            currentSelectedRow = clue.row;
            currentSelectedDirection = direction;
            currentSelectedNum = num;
            
            lockAllInputs();
            unlockSelectedInputs(direction, clue);
            
            document.querySelectorAll('.confirm-btn').forEach(btn => btn.classList.remove('show'));
            
            const inputs = document.querySelectorAll('.cell input');
            for (let input of inputs) {
                if (parseInt(input.dataset.row) === clue.row && parseInt(input.dataset.col) === clue.col) {
                    input.focus();
                    break;
                }
            }
        }
        
        function lockAllInputs() {
            document.querySelectorAll('.cell input').forEach(input => {
                if (!input.classList.contains('correct')) input.disabled = true;
            });
        }
        
        function unlockSelectedInputs(direction, clue) {
            document.querySelectorAll('.cell input').forEach(input => {
                const row = parseInt(input.dataset.row);
                const col = parseInt(input.dataset.col);
                
                if (direction === 'across') {
                    if (row === clue.row && col >= clue.col && col < clue.col + clue.length) {
                        if (!input.classList.contains('correct')) input.disabled = false;
                    }
                } else {
                    if (col === clue.col && row >= clue.row && row <= 6) {
                        if (!input.classList.contains('correct')) input.disabled = false;
                    }
                }
            });
        }

        function checkAllAnswers() {
            const inputs = document.querySelectorAll('.cell input');
            let allFilled = true;
            
            inputs.forEach(input => {
                if (input.value === '' && !input.classList.contains('correct')) allFilled = false;
            });
            
            if (allFilled) {
                alert('🎉 Chúc mừng! Bạn đã hoàn thành crossword puzzle!');
            } else {
                alert('📝 Hãy hoàn thành tất cả các câu hỏi!');
            }
        }

        createGrid();
    </script>
</body>
</html>
