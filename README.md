<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>GIAI O CHU</title>
    <link rel="preconnect" href="https://fonts.gstatic.com" />
    <link href="https://fonts.googleapis.com/css2?family=Luckiest+Guy&family=Poppins:wght@400;700&display=swap" rel="stylesheet" />
    <style>
        body {
            font-family: 'Poppins', Arial, sans-serif;
            min-height: 100vh;
            margin: 0;
            padding: 0;
            position: relative;
            background: linear-gradient(120deg, #30cfd0 0%, #330867 100%);
            background-size: 300% 300%;
            animation: bgGradientMove 18s ease-in-out infinite;
            overflow-x: hidden;
            color: #fff;
        }
        @keyframes bgGradientMove {
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
        #particles-js {
            position: fixed;
            width: 100vw;
            height: 100vh;
            left: 0;
            top: 0;
            right: 0;
            bottom: 0;
            z-index: 0;
        }
        .confetti {
            pointer-events: none;
            position: fixed;
            left: 0;
            top: 0;
            width: 100vw;
            height: 100vh;
            z-index: 99;
        }
        .container {
            margin: 40px auto 40px auto;
            background: rgba(20, 65, 75, 0.85);
            border-radius: 32px;
            backdrop-filter: blur(24px);
            box-shadow: 0 20px 80px rgba(27, 81, 89, 0.6), 0 0 64px rgba(27, 81, 89, 0.4) inset;
            border: 2.5px solid rgba(255, 255, 255, 0.15);
            max-width: 740px;
            padding: 38px 34px 45px 34px;
            position: relative;
            z-index: 10;
            color: #eefafb;
        }
        h1 {
    font-family: 'Luckiest Guy', cursive;
    text-align: center;
    font-size: 54px;
    letter-spacing: 2px;
    margin-bottom: 22px;
    color: white;
    background: none !important;
    -webkit-background-clip: unset !important;
    -webkit-text-fill-color: unset !important;
    text-shadow: none !important;
    animation: none !important;
    filter: none !important;
    opacity: 1 !important;
}



        .grid-wrapper {
            perspective: 800px;
        }
        .grid {
            display: inline-block;
            background: rgba(0, 48, 55, 0.7);
            padding: 10px;
            border-radius: 14px;
            box-shadow: 0 10px 40px rgba(16, 64, 75, 0.7), 0 0 40px rgba(48, 207, 208, 0.3) inset;
            margin-bottom: 6px;
            transform-style: preserve-3d;
            transition: 0.4s cubic-bezier(0.66, -0.55, 0.27, 1.45) transform;
        }
        .grid:hover {
            transform: rotateX(2deg) rotateY(-2deg) scale(1.05);
        }
        .row {
            display: flex;
            line-height: 0;
            position: relative;
        }
        .cell {
            width: 46px;
            height: 46px;
            border: 2.5px solid rgba(48, 207, 208, 0.4);
            background: linear-gradient(135deg, #2193b0, #6dd5ed);
            border-radius: 8px;
            margin: 1px;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
            box-sizing: border-box;
            box-shadow: 0 3px 12px #41b3c477;
            transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }
        .cell input {
            font-family: inherit;
            width: 100%;
            height: 100%;
            border: none;
            border-radius: 8px;
            text-align: center;
            font-size: 22px;
            font-weight: 700;
            text-transform: uppercase;
            color: #e0f7f9;
            background: transparent;
            outline: none;
            transition: all 0.32s;
            z-index: 1;
        }
        .cell input:focus {
            background: linear-gradient(135deg, #00c6ffee, #0072ffcc);
            color: #bbdefb;
            font-weight: 800;
            transform: scale(1.16);
            box-shadow: 0 0 40px #00b0ffdd, 0 0 60px #0072ffbb inset;
            z-index: 10;
        }
        .cell input:disabled {
            background: #04404eaa;
            color: #658f99;
            cursor: not-allowed;
        }
        .cell input.correct {
            background: linear-gradient(135deg, #7de2e8, #0dadad);
            color: #fff;
            font-weight: 900;
            animation: popCorrect 0.5s ease;
            box-shadow: 0 0 20px #0eadabbb;
        }
        @keyframes popCorrect {
            0% {
                transform: scale(0.8);
            }
            55% {
                transform: scale(1.3);
            }
            100% {
                transform: scale(1);
            }
        }
        .cell.empty {
            background: transparent;
            border: none;
        }
        .confirm-btn {
            position: absolute;
            right: -78px;
            top: 50%;
            transform: translateY(-50%);
            padding: 12px 22px;
            background: linear-gradient(110deg, #33ccff, #00c6ff);
            color: white;
            border: none;
            border-radius: 23px;
            cursor: pointer;
            font-size: 15px;
            font-weight: 700;
            box-shadow: 0 6px 21px #00c6ff44;
            display: none;
            transition: 0.33s;
            letter-spacing: 1px;
        }
        .confirm-btn.show {
            display: block;
            animation: bounceIn 0.43s;
        }
        @keyframes bounceIn {
            0% {
                opacity: 0;
                right: -120px;
                transform: translateY(-50%) scale(0.45);
            }
            78% {
                transform: translateY(-50%) scale(1.12);
            }
            100% {
                opacity: 1;
                right: -78px;
                transform: translateY(-50%) scale(1);
            }
        }
        .clue-buttons {
            margin-top: 24px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }
        .clue-section {
            background: rgba(48, 207, 208, 0.15);
            backdrop-filter: blur(8px);
            padding: 23px;
            border-radius: 18px;
            box-shadow: 0 7px 22px #12aabc88;
        }
        .clue-section h3 {
            color: #00bcd4;
            font-size: 23px;
            font-weight: 700;
            margin-bottom: 8px;
            text-shadow: 0 2px 13px #00bcd455;
        }
        .clue-btn {
            display: inline-block;
            padding: 12px 18px;
            margin: 7px 4px 0 0;
            background: linear-gradient(90deg, #43e97b 0%, #38f9d7 100%);
            border: none;
            border-radius: 21px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            box-shadow: 0 4px 9px #43e97baa;
            transition: 0.28s;
            color: #032b31;
        }
        .clue-btn.active {
            background: linear-gradient(90deg, #20b2aa, #00e0d7);
            color: white;
            transform: scale(1.09);
            box-shadow: 0 6px 20px #00b8ab99;
        }
        .clue-btn.completed {
            background: linear-gradient(90deg, #33ccff, #0099ff);
            color: white;
            animation: pulse 1.5s infinite ease-in-out;
        }
        @keyframes pulse {
            0%,
            60%,
            100% {
                box-shadow: 0 6px 22px #00b8abba;
            }
            25% {
                box-shadow: 0 8px 35px #32aaffcc;
            }
        }
        button.check-all {
            margin-top: 28px;
            padding: 16px 44px;
            background: linear-gradient(110deg, #33ccff, #00c6ff);
            color: white;
            border: none;
            border-radius: 30px;
            font-size: 22px;
            cursor: pointer;
            font-weight: 700;
            box-shadow: 0 10px 30px #00c6ff77;
            letter-spacing: 1px;
            transition: 0.31s;
        }
        button.check-all:hover {
            background: linear-gradient(110deg, #00c6ff, #33ccff);
            transform: scale(1.09);
            box-shadow: 0 15px 40px #00c6ffaa;
        }
        button.check-all:active {
            transform: scale(1.05);
        }
        .modal {
            display: none;
            position: fixed;
            z-index: 987;
            left: 0;
            top: 0;
            width: 100vw;
            height: 100vh;
            background: rgba(14, 71, 77, 0.9);
            backdrop-filter: blur(25px);
        }
        .modal-content {
            background: linear-gradient(110deg, #39b0ac, #2cb4ca 77%);
            margin: 12% auto;
            padding: 42px;
            border-radius: 30px;
            max-width: 550px;
            width: 92%;
            text-align: center;
            box-shadow: 0 23px 90px #2cb4ca88;
            position: relative;
            animation: modalZoomIn 0.4s cubic-bezier(0.7, -0.43, 0.3, 1.45);
        }
        @keyframes modalZoomIn {
            from {
                transform: scale(0.6);
            }
            to {
                transform: scale(1);
            }
        }
        .modal-content h2 {
            color: #e0ffee;
            font-size: 36px;
            font-weight: 700;
            margin-bottom: 14px;
            letter-spacing: 1px;
            text-shadow: 0 4px 14px #00c6ff70;
        }
        .modal-content p {
            color: #def5fb;
            font-size: 26px;
        }
        .close {
            color: #bef8f9;
            position: absolute;
            top: 20px;
            right: 34px;
            font-size: 37px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.2s;
        }
        .close:hover {
            color: #00ffff;
            transform: scale(1.18) rotate(90deg);
        }
        .success-modal {
            display: none;
            position: fixed;
            z-index: 999;
            left: 0;
            top: 0;
            width: 100vw;
            height: 100vh;
            background: rgba(14, 71, 77, 0.95);
            backdrop-filter: blur(20px);
        }
        .success-content {
            background: linear-gradient(135deg, #30cfd0, #2cb4ca, #39b0ac);
            padding: 54px 12px;
            border-radius: 34px;
            max-width: 420px;
            margin: 13% auto;
            text-align: center;
            color: #e0ffee;
            animation: successZoom 0.46s cubic-bezier(0.68, -0.45, 0.34, 1.44);
            box-shadow: 0 24px 100px #30cfd0cc;
        }
        @keyframes successZoom {
            from {
                transform: scale(0.4) rotate(-25deg);
                opacity: 0;
            }
            70% {
                transform: scale(1.22) rotate(13deg);
            }
            to {
                transform: scale(1) rotate(0);
                opacity: 1;
            }
        }
        .success-content h2 {
            font-size: 79px;
            animation: celebrate 1.3s infinite;
        }
        @keyframes celebrate {
            0%,
            100% {
                transform: scale(1) rotate(0deg);
            }
            40% {
                transform: scale(1.18) rotate(-13deg);
            }
            60% {
                transform: scale(0.97) rotate(10deg);
            }
        }
        .success-content p {
            font-size: 29px;
            margin: 0;
            font-weight: 600;
            text-shadow: 0 2px 7px #30cfdb99;
        }
    </style>
</head>
<body>
    <div id="particles-js"></div>
    <canvas class="confetti"></canvas>

    <div class="container">
        <h1>GHEP O CHU</h1>
        <div class="grid-wrapper">
            <div class="grid" id="crossword"></div>
        </div>
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
        <button class="check-all" onclick="checkAllAnswers()">✨ KIỂM TRA </button>
    </div>

    <div id="clueModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal()">&times;</span>
            <h2 id="modalTitle">Câu hỏi</h2>
            <p id="modalText"></p>
        </div>
    </div>

    <div id="successModal" class="success-modal">
        <div class="success-content">
            <h2>🎉</h2>
            <p>CHÚC MỪNG <br>CHÍNH XÁC!</p>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js"></script>
    <script>
        particlesJS('particles-js', {
            particles: {
                number: { value: 90, density: { enable: true, value_area: 900 } },
                color: { value: '#30cfd0' },
                shape: { type: 'circle' },
                opacity: { value: 0.57, random: true },
                size: { value: 4, random: true },
                line_linked: { enable: true, distance: 150, color: '#30cfd0', opacity: 0.5, width: 2 },
                move: { enable: true, speed: 2.7, direction: 'none', random: true, out_mode: 'out' }
            },
            interactivity: {
                detect_on: 'canvas',
                events: { onhover: { enable: true, mode: 'grab' }, onclick: { enable: true, mode: 'push' } },
                modes: { grab: { distance: 210, line_linked: { opacity: 0.85 } }, push: { particles_nb: 4 } }
            }
        });

        // Confetti effect simplified (reuse previous definition)
        const confettiCanvas = document.querySelector('.confetti');
        const ctx = confettiCanvas.getContext('2d');
        let conf = [];
        let w = window.innerWidth, h = window.innerHeight;
        confettiCanvas.width = w; confettiCanvas.height = h;
        function randomConfetti() {
            for(let i=0;i<130;i++) {
                conf.push({
                    x:Math.random()*w,
                    y:Math.random()*-h,
                    r:6+Math.random()*6,
                    d:Math.random()*Math.PI*2,
                    s:2+Math.random()*3,
                    c:["#30cfd0","#2c87aa","#06b5aa","#69d2c0","#77c9d4"][Math.floor(Math.random()*5)]
                });
            }
        }
        function drawConfetti() {
            ctx.clearRect(0,0,w,h);
            for(let i=0;i<conf.length;i++){
                ctx.beginPath();
                ctx.arc(conf[i].x, conf[i].y, conf[i].r, 0, Math.PI*2, false);
                ctx.fillStyle = conf[i].c;
                ctx.fill();
                conf[i].y += conf[i].s;
                conf[i].x += Math.sin(conf[i].d)*2;
                if(conf[i].y > h) conf[i].y = Math.random()*-80;
                if(conf[i].x > w) conf[i].x = 0;
            }
        }
        function launchConfetti() {
            conf = [];
            randomConfetti();
            confettiCanvas.style.display = 'block';
            let t = 0;
            const intervalId = setInterval(() => {
                drawConfetti();
                t++;
                if(t > 80){ clearInterval(intervalId); confettiCanvas.style.display='none'; }
            },40);
        }
        window.addEventListener('resize', () => {
            w = window.innerWidth; h=window.innerHeight;
            confettiCanvas.width=w; confettiCanvas.height=h;
        });


        const grid = [
            [0,0,0,1,1,1,1,1,0,0,0,0,0,0],
            [0,0,1,1,1,1,1,1,0,0,0,0,0,0],
            [0,0,0,0,0,1,1,1,1,1,1,1,0,0],
            [0,0,0,0,0,0,1,1,1,1,1,1,1,1],
            [0,0,0,1,1,1,1,1,1,1,1,1,0,0],
            [0,1,1,1,1,1,1,0,0,0,0,0,0,0],
            [0,1,1,1,1,1,1,0,0,0,0,0,0,0]
        ];
        const clues = {
            across: {
                1:{text:'Thủ đô của Việt Nam',row:0,col:3,answer:'HANOI',length:5},
                2:{text:'Con vật có vòi dài',row:1,col:2,answer:'ELEPHANT',length:6},
                3:{text:'Hành tinh chúng ta đang sống',row:2,col:5,answer:'EARTH',length:7},
                4:{text:'Đại dương lớn nhất thế giới',row:3,col:6,answer:'PACIFIC',length:8},
                5:{text:'Màu của bầu trời',row:4,col:3,answer:'BLUE',length:9},
                6:{text:'Thủ đô của Nhật Bản',row:5,col:1,answer:'TOKYO',length:6},
                7:{text:'Người dạy học',row:6,col:1,answer:'TEACHER',length:6}
            },
            down:{
                1:{text:'Câu hỏi cột dọc',row:0,col:6,answer:'VERTICAL',length:7}
            }
        };

        let currentSelectedRow=null,currentSelectedDirection=null,currentSelectedNum=null,completedClues=new Set();

        function openModal(direction,num) {
            const modal=document.getElementById('clueModal');
            document.getElementById('modalTitle').textContent = (direction==='across'?'🡢 Ngang ':'🡣 Dọc ') + num;
            document.getElementById('modalText').textContent = clues[direction][num].text;
            modal.style.display='block';
        }
        function closeModal() {document.getElementById('clueModal').style.display='none';}
        window.onclick=function(event){
            if(event.target===document.getElementById('clueModal'))closeModal();
        };
        function showSuccessModal(){
            document.getElementById('successModal').style.display='block';
            setTimeout(()=>{document.getElementById('successModal').style.display='none';},2000);
            launchConfetti();
        }

        function createGrid(){
            const crossword=document.getElementById('crossword');
            crossword.innerHTML = '';
            grid.forEach((row,rowIndex)=>{
                const rowDiv=document.createElement('div');rowDiv.className='row';rowDiv.dataset.row=rowIndex;
                row.forEach((cell,colIndex)=>{
                    const cellDiv=document.createElement('div');cellDiv.className='cell';
                    if(cell===0){cellDiv.classList.add('empty');}
                    else{
                        const input=document.createElement('input');
                        input.maxLength=1;input.dataset.row=rowIndex;input.dataset.col=colIndex;input.disabled=true;
                        input.addEventListener('keydown',e=>handleKeyDown(e,rowIndex,colIndex));
                        input.addEventListener('input',e=>{
                            e.target.value = e.target.value.toUpperCase();
                            e.target.classList.add('typing');
                            setTimeout(()=>e.target.classList.remove('typing'),350);
                            if(e.target.value) checkRowComplete();
                        });
                        cellDiv.appendChild(input);
                    }
                    rowDiv.appendChild(cellDiv);
                });
                const confirmBtn=document.createElement('button');
                confirmBtn.className='confirm-btn';
                confirmBtn.textContent = '✓ Xác nhận';
                confirmBtn.dataset.row=rowIndex;
                confirmBtn.onclick = ()=> confirmAnswer(rowIndex);
                rowDiv.appendChild(confirmBtn);
                crossword.appendChild(rowDiv);
            });
            createClueButtons();
        }
        function checkRowComplete() {
            if(currentSelectedDirection !== 'across' || currentSelectedNum === null) return;
            const clue = clues.across[currentSelectedNum];
            const inputs = getRowInputs(clue.row, clue.col, clue.length);
            const allFilled = inputs.every(input => input.value !== '');
            const confirmBtn = document.querySelector(`.confirm-btn[data-row="${clue.row}"]`);
            if(allFilled) confirmBtn.classList.add('show');
            else confirmBtn.classList.remove('show');
        }
        function getRowInputs(row,startCol,length){
            const inputs = [];
            document.querySelectorAll('.cell input').forEach(input=>{
                const r = parseInt(input.dataset.row), c = parseInt(input.dataset.col);
                if(r===row && c>=startCol && c<startCol+length) inputs.push(input);
            });
            return inputs.sort((a,b) => parseInt(a.dataset.col)-parseInt(b.dataset.col));
        }
        function confirmAnswer(row){
            if(currentSelectedNum===null || currentSelectedDirection!=='across') return;
            const clue=clues.across[currentSelectedNum];
            if(clue.row !== row) return;
            const inputs=getRowInputs(clue.row, clue.col, clue.length);
            const userAnswer = inputs.map(i=>i.value).join('');
            if(userAnswer === clue.answer){
                inputs.forEach(i => { i.classList.add('correct'); i.disabled=true; });
                document.querySelector(`.confirm-btn[data-row="${row}"]`).classList.remove('show');
                completedClues.add(`across-${currentSelectedNum}`);
                updateClueButtonStatus(currentSelectedDirection,currentSelectedNum);
                showSuccessModal();
                currentSelectedRow=null; currentSelectedDirection=null; currentSelectedNum=null;
            }else{
                alert('❌ Sai rồi! Hãy thử lại nhé!');
            }
        }
        function updateClueButtonStatus(direction,num){
            document.querySelectorAll('.clue-btn').forEach(btn=>{
                if(btn.dataset.direction === direction && btn.dataset.num == num){
                    btn.classList.add('completed');
                    btn.style.pointerEvents = 'none';
                }
            });
        }
        function handleKeyDown(e,row,col){
            const key=e.key;
            if(key === 'Backspace' && e.target.value === ''){e.preventDefault();moveToPrevious(row,col);}
            else if(key==='ArrowRight'){e.preventDefault();moveRight(row,col);}
            else if(key==='ArrowLeft'){e.preventDefault();moveLeft(row,col);}
            else if(key==='ArrowDown'){e.preventDefault();moveDown(row,col);}
            else if(key==='ArrowUp'){e.preventDefault();moveUp(row,col);}
        }
        function moveRight(row,col){
            const inputs = Array.from(document.querySelectorAll('.cell input:not(:disabled)'));
            for(let input of inputs){
                if(parseInt(input.dataset.row)===row && parseInt(input.dataset.col) > col){input.focus();return;}
            }
        }
        function moveLeft(row,col){
            const inputs=Array.from(document.querySelectorAll('.cell input:not(:disabled)')).reverse();
            for(let input of inputs){
                if(parseInt(input.dataset.row)===row && parseInt(input.dataset.col)<col){input.focus();return;}
            }
        }
        function moveDown(row,col){
            const inputs=Array.from(document.querySelectorAll('.cell input:not(:disabled)'));
            for(let input of inputs){
                if(parseInt(input.dataset.col)===col && parseInt(input.dataset.row)>row){input.focus();return;}
            }
        }
        function moveUp(row,col){
            const inputs=Array.from(document.querySelectorAll('.cell input:not(:disabled)')).reverse();
            for(let input of inputs){
                if(parseInt(input.dataset.col)===col && parseInt(input.dataset.row)<row){input.focus();return;}
            }
        }
        function moveToPrevious(row,col){
            const cells=Array.from(document.querySelectorAll('.cell input:not(:disabled)')).reverse();
            let currentFound=false;
            for(let cell of cells){
                if(currentFound){cell.focus();cell.value='';return;}
                if(parseInt(cell.dataset.row)===row && parseInt(cell.dataset.col)===col) currentFound=true;
            }
        }
        function createClueButtons(){
            const acrossDiv=document.getElementById('acrossButtons');
            const downDiv=document.getElementById('downButtons');
            acrossDiv.innerHTML='';downDiv.innerHTML='';
            Object.keys(clues.across).forEach(num=>{
                const btn=document.createElement('button');
                btn.className='clue-btn';
                btn.textContent='Hàng '+num;
                btn.dataset.direction='across';
                btn.dataset.num=num;
                btn.addEventListener('click',e => selectClue('across',num,e.currentTarget));
                acrossDiv.appendChild(btn);
            });
            const btn=document.createElement('button');
            btn.className='clue-btn';
            btn.textContent='Cột dọc';
            btn.dataset.direction='down';
            btn.dataset.num=1;
            btn.addEventListener('click',e => selectClue('down',1,e.currentTarget));
            downDiv.appendChild(btn);
        }
        function selectClue(direction,num,clickedButton){
            if(completedClues.has(`${direction}-${num}`)) return;
            document.querySelectorAll('.clue-btn').forEach(btn => btn.classList.remove('active'));
            if(clickedButton) clickedButton.classList.add('active');
            openModal(direction,num);
            const clue=clues[direction][num];
            currentSelectedRow=clue.row;
            currentSelectedDirection=direction;
            currentSelectedNum=num;
            lockAllInputs();
            unlockSelectedInputs(direction,clue);
            document.querySelectorAll('.confirm-btn').forEach(btn => btn.classList.remove('show'));
            const inputs=document.querySelectorAll('.cell input');
            for(let input of inputs){
                if(parseInt(input.dataset.row)===clue.row && parseInt(input.dataset.col)===clue.col){
                    input.focus();
                    break;
                }
            }
        }
        function lockAllInputs(){
            document.querySelectorAll('.cell input').forEach(input=>{
                if(!input.classList.contains('correct')) input.disabled=true;
            });
        }
        function unlockSelectedInputs(direction,clue){
            document.querySelectorAll('.cell input').forEach(input=>{
                const r=parseInt(input.dataset.row), c=parseInt(input.dataset.col);
                if(direction==='across'){
                    if(r===clue.row && c>=clue.col && c<clue.col+clue.length) {
                        if(!input.classList.contains('correct')) input.disabled=false;
                    }
                } else {
                    if(c===clue.col && r>=clue.row && r<=6) {
                        if(!input.classList.contains('correct')) input.disabled=false;
                    }
                }
            });
        }
        function checkAllAnswers(){
            const inputs=document.querySelectorAll('.cell input');
            let allFilled=true;
            inputs.forEach(input=>{
                if(input.value==='' && !input.classList.contains('correct')) allFilled=false;
            });
            if(allFilled) alert('🎉 Chúc mừng! Bạn hoàn thành crossword puzzle!');
            else alert('📝 Hoàn thành tất cả các câu hỏi nha!');
        }
        createGrid();
    </script>
</body>
</html>
