# walentynkiMyszeczka-33
<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<title>Walentynki 💖</title>

<style>
body {
    margin: 0;
    font-family: 'Segoe UI', sans-serif;
    background: linear-gradient(135deg, #ff758c, #ff7eb3);
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    overflow: hidden;
}

.card {
    background: rgba(255,255,255,0.15);
    padding: 40px;
    border-radius: 20px;
    max-width: 520px;
    text-align: center;
    backdrop-filter: blur(10px);
    box-shadow: 0 20px 40px rgba(0,0,0,0.2);
    z-index: 2;
}

h1 { font-size: 2.5em; }
h2 { font-weight: normal; }

.countdown {
    font-size: 1.3em;
    margin: 20px 0;
}

.buttons button {
    margin: 10px;
    padding: 15px 35px;
    font-size: 1.1em;
    border: none;
    border-radius: 30px;
    cursor: pointer;
    background: white;
    color: #ff4d6d;
}

.heart {
    position: absolute;
    font-size: 20px;
    animation: floatUp 3s linear forwards;
}

@keyframes floatUp {
    from {
        transform: translateY(0) scale(1);
        opacity: 1;
    }
    to {
        transform: translateY(-700px) scale(1.5);
        opacity: 0;
    }
}

.success {
    font-size: 1.6em;
    margin-top: 20px;
}
</style>
</head>

<body>

<div class="card">
    <h1>Klaudio 💕</h1>
    <h2>Czy zostaniesz moją Walentynką?</h2>

    <div class="countdown" id="countdown"></div>

    <div class="buttons">
        <button onclick="yes()">TAK 💖</button>
        <button onclick="no()">NIE 🙈</button>
    </div>

    <div class="success" id="success"></div>
</div>

<div id="player" style="display:none;"></div>

<script>
// ====== DATA RANDKI ======
const date = new Date("2026-02-14 18:00:00");
// ========================

// Odliczanie
setInterval(() => {
    const now = new Date();
    const diff = date - now;

    if (diff <= 0) {
        countdown.innerHTML = "To już dziś! ❤️";
        return;
    }

    const d = Math.floor(diff / (1000*60*60*24));
    const h = Math.floor((diff / (1000*60*60)) % 24);
    const m = Math.floor((diff / (1000*60)) % 60);
    const s = Math.floor((diff / 1000) % 60);

    countdown.innerHTML = `Do naszej randki zostało:<br>
    ${d} dni ${h}h ${m}m ${s}s 💕`;
}, 1000);

// Serduszka
function hearts() {
    for (let i = 0; i < 120; i++) {
        const h = document.createElement("div");
        h.className = "heart";
        h.innerHTML = "❤️";
        h.style.left = Math.random() * window.innerWidth + "px";
        h.style.bottom = "-20px";
        h.style.fontSize = (Math.random()*25 + 15) + "px";
        document.body.appendChild(h);

        setTimeout(() => h.remove(), 3000);
    }
}

// Kliknięcie NIE
function no() {
    alert("Nie przyjmuję tej odpowiedzi 😌💘");
}

// YouTube API
let player;
let volume = 5;
let musicStarted = false;

function onYouTubeIframeAPIReady() {
    player = new YT.Player('player', {
        videoId: 'QDXXN987bJg',
        playerVars: { controls: 0 }
    });
}

// Kliknięcie TAK
function yes() {
    hearts();
    success.innerHTML = "Wiedziałem! ❤️<br>Nie mogę się doczekać naszej randki 😘";

    if (!musicStarted) {
        musicStarted = true;
        player.playVideo();
        player.setVolume(volume);

        const fade = setInterval(() => {
            if (volume < 40) {
                volume += 2;
                player.setVolume(volume);
            } else {
                clearInterval(fade);
            }
        }, 300);
    }
}

// Załaduj API
const tag = document.createElement('script');
tag.src = "https://www.youtube.com/iframe_api";
document.body.appendChild(tag);
</script>

</body>
</html>
