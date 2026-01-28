<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Raspadinhas do Açaí</title>

  <style>
    body {
      font-family: Arial, sans-serif;
      background: #4b1b6d;
      color: #fff;
      text-align: center;
      padding-top: 40px;
    }

    .container {
      position: relative;
      width: 300px;
      height: 150px;
      margin: 20px auto;
      border-radius: 10px;
      overflow: hidden;
    }

    .premio {
      position: absolute;
      width: 100%;
      height: 100%;
      background: #fff;
      color: #4b1b6d;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 18px;
      font-weight: bold;
      text-align: center;
      padding: 10px;
    }

    canvas {
      position: absolute;
      top: 0;
      left: 0;
      cursor: pointer;
    }

    button {
      margin-top: 15px;
      padding: 12px 20px;
      background: #25D366;
      border: none;
      border-radius: 8px;
      color: #fff;
      font-size: 16px;
      cursor: pointer;
      display: none;
    }
  </style>
</head>
<body>

  <h1>🍧 Raspadinhas do Açaí</h1>
  <p>Raspe e envie seu prêmio pelo WhatsApp</p>

  <div class="container">
    <div class="premio" id="premio"></div>
    <canvas id="raspadinha" width="300" height="150"></canvas>
  </div>

  <button id="btnWhatsapp">📲 Enviar no WhatsApp</button>

  <script>
    const premios = [
      "🎉 10% OFF no Açaí",
      "🥄 Açaí grátis",
      "😋 Topping extra grátis",
      "💔 Não foi dessa vez",
      "🎁 Compre 1 leve 2"
    ];

    const premioSorteado = premios[Math.floor(Math.random() * premios.length)];
    document.getElementById("premio").innerText = premioSorteado;

    const canvas = document.getElementById("raspadinha");
    const ctx = canvas.getContext("2d");

    ctx.fillStyle = "#B0B0B0";
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    ctx.globalCompositeOperation = "destination-out";

    let raspando = false;
    let revelado = false;

    function raspar(x, y) {
      ctx.beginPath();
      ctx.arc(x, y, 18, 0, Math.PI * 2);
      ctx.fill();
    }

    function mostrarBotao() {
      if (!revelado) {
        revelado = true;
        document.getElementById("btnWhatsapp").style.display = "inline-block";
      }
    }

    canvas.addEventListener("mousedown", () => raspando = true);
    canvas.addEventListener("mouseup", () => raspando = false);
    canvas.addEventListener("mousemove", (e) => {
      if (!raspando) return;
      const r = canvas.getBoundingClientRect();
      raspar(e.clientX - r.left, e.clientY - r.top);
      mostrarBotao();
    });

    canvas.addEventListener("touchmove", (e) => {
      e.preventDefault();
      const r = canvas.getBoundingClientRect();
      const t = e.touches[0];
      raspar(t.clientX - r.left, t.clientY - r.top);
      mostrarBotao();
    });

    document.getElementById("btnWhatsapp").onclick = () => {
      const numeroLoja = "5599999999999"; // ALTERE PARA O WHATSAPP DA LOJA
      const msg = `🍧 Raspadinha do Açaí!\nMeu prêmio foi: *${premioSorteado}* 🎉\nPosso resgatar?`;
      window.open(`https://wa.me/${numeroLoja}?text=${encodeURIComponent(msg)}`);
    };
  </script>

</body>
</html>