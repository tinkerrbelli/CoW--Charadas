# Collapse of Worlds-Charadas
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Alice in Wonderland - Charadas</title>

  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600;700&family=Poppins:wght@300;400;500;600&display=swap" rel="stylesheet">

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      min-height: 100vh;
      overflow-x: hidden;
      background:
        radial-gradient(circle at top, rgba(255,120,0,0.2), transparent 35%),
        radial-gradient(circle at bottom, rgba(120,0,255,0.2), transparent 40%),
        linear-gradient(180deg, #14001f, #070010, #000000);
      font-family: 'Poppins', sans-serif;
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 30px;
      position: relative;
    }

    .particles {
      position: fixed;
      width: 100%;
      height: 100%;
      top: 0;
      left: 0;
      overflow: hidden;
      pointer-events: none;
      z-index: 0;
    }

    .particle {
      position: absolute;
      width: 6px;
      height: 6px;
      border-radius: 50%;
      background: rgba(255,255,255,0.6);
      animation: float 15s linear infinite;
    }

    @keyframes float {
      from {
        transform: translateY(100vh) scale(0);
        opacity: 0;
      }
      20% {
        opacity: 1;
      }
      to {
        transform: translateY(-120vh) scale(1.2);
        opacity: 0;
      }
    }

    .container {
      width: 100%;
      max-width: 900px;
      background: rgba(10, 5, 25, 0.78);
      border: 2px solid rgba(255,255,255,0.12);
      border-radius: 30px;
      backdrop-filter: blur(12px);
      padding: 40px;
      position: relative;
      z-index: 2;
      box-shadow:
        0 0 40px rgba(170, 0, 255, 0.35),
        0 0 80px rgba(255, 115, 0, 0.15);
      animation: appear 1s ease;
    }

    @keyframes appear {
      from {
        opacity: 0;
        transform: translateY(30px) scale(0.95);
      }
      to {
        opacity: 1;
        transform: translateY(0px) scale(1);
      }
    }

    h1 {
      text-align: center;
      font-family: 'Cinzel', serif;
      font-size: clamp(2rem, 5vw, 4rem);
      margin-bottom: 10px;
      color: #ffd4a3;
      text-shadow:
        0 0 15px rgba(255, 145, 0, 0.8),
        0 0 35px rgba(255, 0, 128, 0.5);
    }

    .subtitle {
      text-align: center;
      margin-bottom: 35px;
      color: #d6c5ff;
      font-size: 1rem;
      opacity: 0.9;
    }

    .card {
      background: rgba(255,255,255,0.05);
      border: 1px solid rgba(255,255,255,0.08);
      border-radius: 24px;
      padding: 35px;
      min-height: 280px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      position: relative;
      overflow: hidden;
    }

    .card::before {
      content: "";
      position: absolute;
      width: 200px;
      height: 200px;
      background: radial-gradient(circle, rgba(255,120,0,0.25), transparent 70%);
      top: -80px;
      right: -80px;
      border-radius: 50%;
    }

    .difficulty {
      display: inline-block;
      padding: 8px 14px;
      border-radius: 999px;
      font-size: 0.9rem;
      font-weight: 600;
      margin-bottom: 25px;
      width: fit-content;
      letter-spacing: 1px;
      text-transform: uppercase;
    }

    .facil {
      background: rgba(0,255,120,0.18);
      border: 1px solid rgba(0,255,120,0.4);
      color: #82ffbf;
    }

    .medio {
      background: rgba(255,208,0,0.18);
      border: 1px solid rgba(255,208,0,0.4);
      color: #ffe17d;
    }

    .dificil {
      background: rgba(255,70,70,0.18);
      border: 1px solid rgba(255,70,70,0.4);
      color: #ff9898;
    }

    .charada {
      font-size: clamp(1.3rem, 3vw, 2rem);
      line-height: 1.7;
      margin-bottom: 30px;
      animation: fadeIn 0.6s ease;
      text-shadow: 0 0 10px rgba(255,255,255,0.1);
    }

    @keyframes fadeIn {
      from {
        opacity: 0;
        transform: translateY(15px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .resposta {
      opacity: 0;
      max-height: 0;
      overflow: hidden;
      transition: all 0.5s ease;
      color: #ffc98b;
      font-size: 1.1rem;
      border-left: 3px solid rgba(255,166,0,0.5);
      padding-left: 15px;
    }

    .resposta.show {
      opacity: 1;
      max-height: 200px;
      margin-top: 10px;
    }

    .buttons {
      margin-top: 35px;
      display: flex;
      gap: 20px;
      flex-wrap: wrap;
      justify-content: center;
    }

    button {
      border: none;
      padding: 15px 28px;
      border-radius: 18px;
      font-size: 1rem;
      font-weight: 600;
      cursor: pointer;
      transition: 0.3s ease;
      font-family: 'Poppins', sans-serif;
    }

    .next-btn {
      background: linear-gradient(135deg, #ff7300, #ff00b3);
      color: white;
      box-shadow: 0 0 25px rgba(255,0,140,0.4);
    }

    .answer-btn {
      background: rgba(255,255,255,0.08);
      color: white;
      border: 1px solid rgba(255,255,255,0.1);
    }

    button:hover {
      transform: translateY(-3px) scale(1.03);
    }

    .counter {
      text-align: center;
      margin-top: 28px;
      color: #cdbfff;
      opacity: 0.8;
    }

    .quote {
      text-align: center;
      margin-top: 30px;
      font-style: italic;
      color: rgba(255,255,255,0.5);
    }

    @media (max-width: 700px) {
      .container {
        padding: 25px;
      }

      .card {
        padding: 25px;
      }

      .buttons {
        flex-direction: column;
      }

      button {
        width: 100%;
      }
    }
  </style>
</head>
<body>

  <div class="particles" id="particles"></div>

  <div class="container">

    <h1>Alice in Wonderland</h1>

    <p class="subtitle">
      “Às vezes eu acredito em até seis coisas impossíveis antes do café da manhã.”
    </p>

    <div class="card">

      <div id="difficulty" class="difficulty facil">
        Fácil
      </div>

      <div id="charada" class="charada">
        Clique no botão abaixo para entrar na toca do coelho.
      </div>

      <div id="resposta" class="resposta"></div>

      <div class="buttons">
        <button class="next-btn" onclick="novaCharada()">
          Próxima Charada
        </button>

        <button class="answer-btn" onclick="mostrarResposta()">
          Mostrar Resposta
        </button>
      </div>

      <div id="counter" class="counter">
        0 / 150 charadas
      </div>

    </div>

    <div class="quote">
      “We're all mad here.”
    </div>

  </div>

  <script>

    const baseCharadas = [
      {
        dificuldade: 'Fácil',
        pergunta: 'Quanto mais seca, mais molhada fica. O que é?',
        resposta: 'A toalha.'
      },
      {
        dificuldade: 'Médio',
        pergunta: 'O que sobe mas nunca desce?',
        resposta: 'A idade.'
      },
      {
        dificuldade: 'Difícil',
        pergunta: 'Sou invisível, mas posso preencher uma sala inteira. O que sou?',
        resposta: 'A escuridão.'
      },
      {
        dificuldade: 'Fácil',
        pergunta: 'O que tem dentes mas não morde?',
        resposta: 'O pente.'
      },
      {
        dificuldade: 'Médio',
        pergunta: 'O que corre mas nunca anda?',
        resposta: 'A água.'
      },
      {
        dificuldade: 'Difícil',
        pergunta: 'Quanto mais você tira de mim, maior eu fico. O que sou?',
        resposta: 'Um buraco.'
      },
      {
        dificuldade: 'Fácil',
        pergunta: 'Qual é a coisa que cai em pé e corre deitada?',
        resposta: 'A chuva.'
      },
      {
        dificuldade: 'Médio',
        pergunta: 'O que pode viajar o mundo inteiro sem sair do lugar?',
        resposta: 'O selo.'
      },
      {
        dificuldade: 'Difícil',
        pergunta: 'Sou leve como uma pena, mas ninguém consegue me segurar por muito tempo. O que sou?',
        resposta: 'A respiração.'
      },
      {
        dificuldade: 'Fácil',
        pergunta: 'O que fica cheio durante o dia e vazio à noite?',
        resposta: 'O sapato.'
      },
      {
        dificuldade: 'Médio',
        pergunta: 'O que quanto mais cresce, menos se vê?',
        resposta: 'A escuridão.'
      },
      {
        dificuldade: 'Difícil',
        pergunta: 'Tenho cidades, mas não casas. Tenho rios, mas não água. O que sou?',
        resposta: 'Um mapa.'
      },
      {
        dificuldade: 'Fácil',
        pergunta: 'Qual mão é melhor para mexer açúcar no café?',
        resposta: 'Nenhuma. Melhor usar uma colher.'
      },
      {
        dificuldade: 'Médio',
        pergunta: 'O que quanto mais se usa, mais afiado fica?',
        resposta: 'O cérebro.'
      },
      {
        dificuldade: 'Difícil',
        pergunta: 'O que existe uma vez em um minuto, duas em um momento e nunca em cem anos?',
        resposta: 'A letra M.'
      }
    ];

    const charadas = [];

    while(charadas.length < 150){
      const copia = [...baseCharadas]
        .sort(() => Math.random() - 0.5);

      charadas.push(...copia);
    }

    charadas.length = 150;

    let atual = -1;

    function novaCharada(){

      atual++;

      if(atual >= charadas.length){
        atual = 0;
      }

      const item = charadas[atual];

      const pergunta = document.getElementById('charada');
      const resposta = document.getElementById('resposta');
      const dificuldade = document.getElementById('difficulty');
      const counter = document.getElementById('counter');

      pergunta.style.opacity = 0;

      setTimeout(() => {

        pergunta.innerText = item.pergunta;
        resposta.innerText = item.resposta;

        resposta.classList.remove('show');

        dificuldade.innerText = item.dificuldade;

        dificuldade.className = 'difficulty';

        if(item.dificuldade === 'Fácil'){
          dificuldade.classList.add('facil');
        }

        if(item.dificuldade === 'Médio'){
          dificuldade.classList.add('medio');
        }

        if(item.dificuldade === 'Difícil'){
          dificuldade.classList.add('dificil');
        }

        pergunta.style.opacity = 1;

        counter.innerText = `${atual + 1} / 150 charadas`;

      }, 250);

    }

    function mostrarResposta(){
      document.getElementById('resposta')
      .classList.toggle('show');
    }

    const particlesContainer = document.getElementById('particles');

    for(let i = 0; i < 45; i++){
      const particle = document.createElement('div');
      particle.classList.add('particle');

      particle.style.left = Math.random() * 100 + 'vw';
      particle.style.animationDuration =
      (Math.random() * 10 + 10) + 's';

      particle.style.animationDelay =
      Math.random() * 5 + 's';

      particle.style.opacity = Math.random();

      particlesContainer.appendChild(particle);
    }

  </script>

</body>
</html>
