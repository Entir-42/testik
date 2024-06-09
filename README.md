<!DOCTYPE html>
<html>
<head>
<title>Matrix Efekt</title>
<style>
body {
    background-color: black;
    overflow: hidden;
    margin: 0;
}

.matrix {
    font-family: monospace;
    font-size: 20px;
    color: #00FF00;
    white-space: pre;
    width: 100%;
    height: 100vh;
    display: flex;
    flex-direction: column;
}

.matrix-row {
    display: flex;
}

.fade-out {
    animation: fadeOut 0.5s forwards; /* Animácia miznutia */
}

@keyframes fadeOut {
    to { opacity: 0; }
}
</style>
</head>
<body>
<div class="matrix"></div>
<script>
const matrix = document.querySelector('.matrix');
const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,:;!?-_"()[]{}@+#$&|^~`\\ \n€$£¥↑↓←→◯';
const maxChangesPerTick = 1000; // Maximálny počet zmien za jeden interval
const minFadeOutDuration = 500; // Minimálna hodnota trvania miznutia
const maxFadeOutDuration = 1000; // Maximálna hodnota trvania miznutia

function createMatrixRow() {
    const row = document.createElement('div');
    row.classList.add('matrix-row');
    for (let i = 0; i < Math.floor(window.innerWidth / 20); i++) {
        const span = document.createElement('span');
        span.textContent = characters.charAt(Math.floor(Math.random() * characters.length));
        row.appendChild(span);
    }
    return row;// ... (rovnaké ako predtým)
}

function fillMatrix() {
    while (matrix.scrollHeight <= window.innerHeight) {
        matrix.appendChild(createMatrixRow());
    }// ... (rovnaké ako predtým)
}

function rain() {
    let changes = 0;
    const rows = matrix.querySelectorAll('.matrix-row');
    rows.forEach(row => {
        const spans = row.querySelectorAll('span');
        spans.forEach(span => {
            if (changes < maxChangesPerTick && Math.random() < 0.05) {
                span.classList.add('fade-out');
                const fadeOutDuration = Math.floor(Math.random() * (maxFadeOutDuration - minFadeOutDuration + 1)) + minFadeOutDuration; // Generovanie náhodnej hodnoty
                setTimeout(() => {
                    span.textContent = characters.charAt(Math.floor(Math.random() * characters.length));
                    span.classList.remove('fade-out');
                }, fadeOutDuration);
                changes++;
            }
        });
    });
}

fillMatrix();
setInterval(rain, 200); // Upravte interval pre frekvenciu zmien
</script>
</body>
</html>
