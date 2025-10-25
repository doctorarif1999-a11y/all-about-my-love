<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>For My Love 💖</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      height: 100vh;
      width: 100vw;
      background: url("https://iili.io/KkLPDtn.jpg") no-repeat center center fixed;
      background-size: cover;
      position: relative;
      font-family: 'Poppins', sans-serif;
    }

    /* BUTTERFLIES */
    .butterfly {
      position: fixed;
      width: 60px;
      height: 60px;
      background-size: contain;
      background-repeat: no-repeat;
      animation: flap 0.35s ease-in-out infinite alternate;
      opacity: 0.75;
      will-change: transform;
      pointer-events: none;
      filter: drop-shadow(0 0 8px rgba(255, 255, 255, 0.4));
    }

    @keyframes flap {
      0% { transform: rotate(-15deg) scale(0.9); }
      100% { transform: rotate(15deg) scale(1.25); }
    }

    /* FLOWER RING */
    .flower-ring {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 320px;
      height: 320px;
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 2;
    }

    .flower {
      position: absolute;
      width: 80px;
      height: 80px;
      background-size: contain;
      background-repeat: no-repeat;
      cursor: pointer;
      transition: all 1s ease;
      z-index: 3;
    }

    /* TEXT STYLE — white with black outline and golden glow */
    .flower-message {
      position: fixed;
      top: 75%;
      left: 50%;
      transform: translateX(-50%);
      font-size: 1.6em; /* ⬅ Increased size */
      font-weight: 500;
      color: #fff;
      text-align: center;
      white-space: pre-line;
      opacity: 0;
      transition: opacity 0.8s;
      z-index: 4;
      text-shadow:
        0 0 10px rgba(255, 215, 0, 0.6),
        0 0 20px rgba(255, 215, 0, 0.4),
        2px 2px 4px #000,
        -2px -2px 4px #000;
    }
  </style>
</head>
<body>
  <div class="flower-ring" id="flowerRing"></div>
  <div class="flower-message" id="flowerMessage"></div>

  <script>
    /* BUTTERFLIES */
    const numButterflies = 25;
    const butterflyImages = [
      "https://pngimg.com/uploads/butterfly/butterfly_PNG1058.png",
      "https://pngimg.com/uploads/butterfly/butterfly_PNG1060.png",
      "https://pngimg.com/uploads/butterfly/butterfly_PNG1048.png"
    ];

    function randomRange(min, max) {
      return Math.random() * (max - min) + min;
    }

    for (let i = 0; i < numButterflies; i++) {
      const butterfly = document.createElement('div');
      butterfly.classList.add('butterfly');
      butterfly.style.backgroundImage = `url('${butterflyImages[Math.floor(Math.random() * butterflyImages.length)]}')`;
      butterfly.style.left = randomRange(0, window.innerWidth) + 'px';
      butterfly.style.top = randomRange(0, window.innerHeight) + 'px';
      butterfly.style.width = randomRange(50, 80) + 'px';
      butterfly.style.animationDuration = (0.25 + Math.random() * 0.25) + 's';
      butterfly.style.opacity = randomRange(0.55, 0.8);
      document.body.appendChild(butterfly);
      smoothFly(butterfly);
    }

    function smoothFly(el) {
      let x = parseFloat(el.style.left);
      let y = parseFloat(el.style.top);
      let dx = randomRange(-1, 1);
      let dy = randomRange(-1, 1);
      const speed = randomRange(0.3, 0.8);

      function move() {
        x += dx * speed;
        y += dy * speed;

        if (x < -100 || x > window.innerWidth + 100) dx *= -1;
        if (y < -100 || y > window.innerHeight + 100) dy *= -1;

        dx += randomRange(-0.02, 0.02);
        dy += randomRange(-0.02, 0.02);
        const length = Math.sqrt(dx * dx + dy * dy);
        dx /= length;
        dy /= length;

        el.style.left = x + 'px';
        el.style.top = y + 'px';
        el.style.transform = `rotate(${Math.sin(Date.now() / 400) * 15}deg) scale(${1 + Math.sin(Date.now() / 500) * 0.1})`;

        requestAnimationFrame(move);
      }
      move();
    }

    /* FLOWERS */
    const flowers = [
      "https://i.ibb.co/YTQgWrd7/2025102509143047.png",
      "https://i.ibb.co/twqtPm1P/2025102509141665.png",
      "https://i.ibb.co/7dQmdQBt/2025102509140223.png",
      "https://i.ibb.co/1YQ4CVCJ/2025102509134208.png",
      "https://i.ibb.co/20CPLTkQ/2025102509131496.png",
      "https://i.ibb.co/Y4rpFs3x/2025102509125895.png",
      "https://i.ibb.co/C52wfsGX/2025102509124346.png",
      "https://i.ibb.co/k6JVfPGw/2025102509121996.png"
    ];

    const messages = [
      "تم سا صرف تم ہی کو دیکھا",
      "Moon or the stars?\n      - Her Eyes",
      "تیری آنکھوں کے سوا دنیا میں رکھا کیا ہے",
      "It's the eyes.\nIt was all in her Eyes.",
      "تیری صورت سے ہے عالم میں بہاروں کو ثبات\n    تیری آنکھوں کے سوا دنیا میں رکھا گیا",
      "The voice of your eyes!\nIt's deeper than all roses",
      "ایسی الجھی نظر تم سے ہٹتی نہیں",
      "What beauty can there be \nto mention after your eyes"
    ];

    const ring = document.getElementById("flowerRing");
    const msg = document.getElementById("flowerMessage");
    let activeFlower = null;

    const radius = 130;
    const positions = [];

    flowers.forEach((img, i) => {
      const flower = document.createElement("div");
      flower.className = "flower";
      flower.style.backgroundImage = `url(${img})`;
      const angle = (i / flowers.length) * 2 * Math.PI;
      const x = Math.cos(angle) * radius;
      const y = Math.sin(angle) * radius;
      flower.style.left = `calc(50% + ${x}px - 40px)`;
      flower.style.top = `calc(50% + ${y}px - 40px)`;
      positions.push({ x, y });

      flower.addEventListener("click", (e) => {
        e.stopPropagation();
        if (activeFlower === flower) {
          resetFlowers();
          return;
        }
        document.querySelectorAll(".flower").forEach(f => {
          f.style.opacity = 0.4;
          f.style.transform = "";
        });
        flower.style.left = "50%";
        flower.style.top = "50%";
        flower.style.transform = "translate(-50%, -50%) scale(1.6)";
        flower.style.opacity = 1;
        msg.textContent = messages[i];
        msg.style.opacity = 1;
        activeFlower = flower;
      });

      ring.appendChild(flower);
    });

    document.body.addEventListener("click", () => {
      resetFlowers();
    });

    function resetFlowers() {
      document.querySelectorAll(".flower").forEach((f, i) => {
        const { x, y } = positions[i];
        f.style.left = `calc(50% + ${x}px - 40px)`;
        f.style.top = `calc(50% + ${y}px - 40px)`;
        f.style.transform = "";
        f.style.opacity = 1;
      });
      msg.style.opacity = 0;
      activeFlower = null;
    }
  </script>
</body>
</html>![15652](https://github.com/user-attachments/assets/d0210ecb-17cd-461c-aec5-a905db851abb)
<img width="625" height="624" alt="18654" src="https://github.com/user-attachments/assets/81e00934-c892-47bb-8954-80dd13ca1849" />
<img width="626" height="615" alt="18655" src="https://github.com/user-attachments/assets/7c3c1d94-e029-4af9-ac50-c1a3ca8676ff" />
<img width="735" height="698" alt="18656" src="https://github.com/user-attachments/assets/5cb39781-ef6f-4908-855b-c9bbad66ddac" />
<img width="563" height="577" alt="18657" src="https://github.com/user-attachments/assets/c0b4aabc-1f26-49e5-833a-d27c11530604" />
<img width="734" height="708" alt="18658" src="https://github.com/user-attachments/assets/496441f9-27f4-4509-8fb3-bf99ecd3bb46" />
<img width="622" height="640" alt="18659" src="https://github.com/user-attachments/assets/2b13695d-708f-4308-9b45-301841371606" />
<img width="725" height="735" alt="18660" src="https://github.com/user-attachments/assets/7176292b-96e3-4734-9b0d-c991340beaef" />
<img width="717" height="720" alt="18661" src="https://github.com/user-attachments/assets/d0d3ee3b-52f4-40fb-aff2-665c0e9f02f8" />
