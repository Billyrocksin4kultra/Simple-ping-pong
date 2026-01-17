<!DOCTYPE html>    
<html>    
<head>    
    <title>Ping Pong</title>    
    <style>    
        canvas { border: 1px solid black; background: #000; display: block; margin: auto; }    
        body { background: #f0f0f0; text-align: center; }    
    </style>    
</head>    
<body>    
    <canvas id="game" width="400" height="200"></canvas>    
    <script>    
        const canvas = document.getElementById('game');    
        const ctx = canvas.getContext('2d');    
    
        let ballX = 200, ballY = 100;    
        let ballSpeedX = 5, ballSpeedY = 3;    
        let paddleHeight = 60, paddleWidth = 10;    
        let leftPaddleY = 70, rightPaddleY = 70;    
    
        function draw() {    
            // Clear    
            ctx.fillStyle = 'black'; ctx.fillRect(0, 0, 400, 200);    
    
            // Net    
            ctx.setLineDash([5, 10]); ctx.strokeStyle = 'white';    
            ctx.beginPath(); ctx.moveTo(200, 0); ctx.lineTo(200, 200); ctx.stroke();    
    
            // Paddles    
            ctx.fillStyle = 'white';    
            ctx.fillRect(10, leftPaddleY, paddleWidth, paddleHeight);    
            ctx.fillRect(380, rightPaddleY, paddleWidth, paddleHeight);    
    
            // Ball    
            ctx.beginPath(); ctx.arc(ballX, ballY, 8, 0, Math.PI*2); ctx.fill();    
        }    
    
        function update() {    
            ballX += ballSpeedX; ballY += ballSpeedY;    
    
            // Wall bounce    
            if (ballY <= 0 || ballY >= 190) ballSpeedY = -ballSpeedY;    
    
            // Paddle bounce    
            if (ballX <= 20 && ballY >= leftPaddleY && ballY <= leftPaddleY + paddleHeight)    
                ballSpeedX = -ballSpeedX;    
            if (ballX >= 360 && ballY >= rightPaddleY && ballY <= rightPaddleY + paddleHeight)    
                ballSpeedX = -ballSpeedX;    
        }    
    
        function gameLoop() {    
            update(); draw(); requestAnimationFrame(gameLoop);    
        }    
    
        // Controls    
        document.addEventListener('keydown', e => {    
            if (e.key === 'ArrowUp') rightPaddleY = Math.max(0, rightPaddleY - 15);    
            if (e.key === 'ArrowDown') rightPaddleY = Math.min(140, rightPaddleY + 15);    
            if (e.key === 'w') leftPaddleY = Math.max(0, leftPaddleY - 15);    
            if (e.key === 's') leftPaddleY = Math.min(140, leftPaddleY + 15);    
        });    
    
        gameLoop();    
    </script>    
</body>    
</html>    
