<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Bir Sorum Var... 😄</title>
<style>
    body {
        font-family: 'Comic Sans MS', cursive, sans-serif;
        text-align: center;
        background: #fff0f5;
        padding: 50px;
        overflow-x: hidden;
    }
    #container {
        margin-top: 80px;
    }
    #text {
        font-size: 26px;
        margin-bottom: 40px;
        transition: 0.3s;
    }
    button {
        font-size: 22px;
        padding: 15px 28px;
        margin: 10px;
        border-radius: 12px;
        border: none;
        cursor: pointer;
        transition: 0.3s, transform 0.3s;
        position: relative;
    }
    #yesBtn {
        background-color: #ff69b4;
        color: white;
    }
    #noBtn {
        background-color: #ccc;
    }
    .confetti {
        position: fixed;
        width: 10px;
        height: 10px;
        background-color: red;
        top: 0;
        left: 50%;
        pointer-events: none;
        opacity: 0.7;
        animation: fall 3s linear forwards;
    }
    @keyframes fall {
        0% { transform: translateY(0) rotate(0deg); }
        100% { transform: translateY(100vh) rotate(360deg); opacity: 0; }
    }
</style>
</head>

<body>

<h1>Bir Sorum Var Sana... 😏</h1>

<div id="container">
    <div id="text">Seninle konuşmak her zaman günümü aydınlatıyor 🌸</div>
    <button id="nextBtn">İlerle</button>
</div>

<audio id="noSound" src="https://www.soundjay.com/button/sounds/button-16.mp3"></audio>

<script>
let step = 0;
const text = document.getElementById("text");
const container = document.getElementById("container");
const nextBtn = document.getElementById("nextBtn");
const noSound = document.getElementById("noSound");

const compliments = [
    "Senin gülüşün her şeyi güzelleştiriyor 😍",
    "Seninle sohbet etmek her zaman keyifli 💖",
    "Senin enerjin yanında olunca insan mutlu oluyor ✨"
];

const questions = [
    "Gerçekten merak ettiğim bir şey var 😄",
    "Cevabın beni heyecanlandıracak! 😜",
    "Biliyor musun, seninle geçirdiğim her an, günümü güzelleştiriyor. Acaba bir şans verir misin, birlikte daha çok güzel an biriktirelim mi? 💖"
];

// İltaftlar ve sorular
nextBtn.addEventListener("click", () => {
    step++;
    if (step < compliments.length) {
        text.textContent = compliments[step];
    } else if (step < compliments.length + questions.length - 1) {
        // İlerle butonu ile diğer sorular
        const qStep = step - compliments.length;
        text.textContent = questions[qStep];
    } else if (step === compliments.length + questions.length - 1) {
        // Son soru: çıkma teklifi
        text.textContent = questions[questions.length - 1];
        nextBtn.style.display = "none";

        // Evet ve Hayır butonları ekle
        const yesBtn = document.createElement("button");
        yesBtn.id = "yesBtn";
        yesBtn.textContent = "Evet";
        container.appendChild(yesBtn);

        const noBtn = document.createElement("button");
        noBtn.id = "noBtn";
        noBtn.textContent = "Hayır";
        container.appendChild(noBtn);

        // Hayır butonu kaçıyor ve ses çıkarıyor
        noBtn.addEventListener("mouseenter", () => {
            const x = Math.random() * (window.innerWidth - noBtn.offsetWidth);
            const y = Math.random() * (window.innerHeight - noBtn.offsetHeight - 100);
            noBtn.style.position = "absolute";
            noBtn.style.left = x + "px";
            noBtn.style.top = y + "px";
            noSound.play();
        });

        // Evet butonuna basınca final ve konfeti
        yesBtn.addEventListener("click", () => {
            text.textContent = "Seni ömrümün sonuna kadar SEVECEĞİM 🎉💞";
            yesBtn.style.display = "none";
            noBtn.style.display = "none";
            startConfetti();
        });

        function startConfetti() {
            const colors = ['#ff0a54','#ff477e','#ff85a1','#fbb1b1','#f9bec7','#f7cad0'];
            for(let i=0;i<150;i++){
                const confetti = document.createElement('div');
                confetti.classList.add('confetti');
                confetti.style.backgroundColor = colors[Math.floor(Math.random()*colors.length)];
                confetti.style.left = Math.random() * window.innerWidth + "px";
                confetti.style.animationDuration = (2 + Math.random()*2) + "s";
                confetti.style.width = confetti.style.height = (5 + Math.random()*10) + "px";
                document.body.appendChild(confetti);
                setTimeout(() => confetti.remove(), 4000);
            }
        }
    }
});

// Başlangıç iltifat
text.textContent = compliments[0];
</script>

</body>
</html>
