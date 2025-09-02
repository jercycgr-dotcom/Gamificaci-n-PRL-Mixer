<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Detecta el Riesgo - Departamento PRL Mixer & Pack</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(to bottom, #1E90FF, #87CEFA);
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
    }

    .container {
      max-width: 800px;
      margin: 30px auto;
      background: rgba(255, 255, 255, 0.95);
      padding: 25px;
      border-radius: 15px;
      box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
      text-align: center;
    }

    h1 {
      color: #333;
    }

    .question {
      font-size: 20px;
      margin-top: 20px;
    }

    .emoji {
      font-size: 80px;
      display: block;
      margin: 15px auto;
      animation: float 3s ease-in-out infinite;
    }

    @keyframes float {
      0%, 100% { transform: translateY(0px); }
      50% { transform: translateY(-10px); }
    }

    .options {
      display: flex;
      flex-direction: column;
      margin-top: 20px;
    }

    button {
      padding: 14px;
      margin: 8px 0;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      cursor: pointer;
      transition: all 0.3s ease;
    }

    button:hover {
      transform: scale(1.05);
    }

    .correct {
      background-color: #4CAF50;
      color: #fff;
    }

    .partial {
      background-color: #FF9800;
      color: #fff;
    }

    .incorrect {
      background-color: #f44336;
      color: #fff;
    }

    .feedback {
      margin-top: 20px;
      font-weight: bold;
      font-size: 18px;
      opacity: 0;
      transition: opacity 0.5s, transform 0.5s;
    }

    .feedback.show {
      opacity: 1;
      transform: scale(1.1);
    }

    .score {
      text-align: center;
      font-size: 24px;
      color: #333;
      margin-top: 20px;
    }

    .ranking {
      margin-top: 15px;
      font-size: 18px;
      color: #333;
    }

    .progress-bar {
      height: 20px;
      background: #ccc;
      border-radius: 10px;
      overflow: hidden;
      margin-top: 15px;
    }

    .progress {
      height: 100%;
      width: 0%;
      background: #4CAF50;
      transition: width 0.5s;
    }

    /* Revisión de respuestas con texto en negro */
    .review-box {
      border-left: 8px solid #ccc;
      background: #f9f9f9;
      padding: 10px 15px;
      margin: 10px 0;
      border-radius: 8px;
      text-align: left;
      color: #000; /* Texto en negro */
    }

    .review-box.correct { border-color: #4CAF50; }
    .review-box.partial { border-color: #FF9800; }
    .review-box.incorrect { border-color: #f44336; }
  </style>
</head>
<body>
  <div class="container">
    <h1>Simulador de Seguridad: Detecta el Riesgo</h1>
    <div class="progress-bar">
      <div class="progress" id="progress"></div>
    </div>
    <div id="quiz"></div>
  </div>

  <script>
    const questions = [
      {
        q: "Escenario 1: Estás usando las escaleras de acceso a Mixer & Pack.",
        emoji: "🏬🪜",
        options: [
          { text: "Bajar/subir rápido sin usar pasamanos", type: "incorrect", feedback: "Bajar sin sujetarte es peligroso." },
          { text: "Sujetarte del pasamanos", type: "correct", feedback: "¡Bien! Sujetarte previene caídas." },
          { text: "Saltar el escalón", type: "partial", feedback: "Saltar aumenta el riesgo de caída." }
        ]
      },
      {
        q: "Escenario 2: Vas a mover un palet pesado. ¿Qué harías?",
        emoji: "📦",
        options: [
          { text: "Pedir ayuda", type: "correct", feedback: "¡Bien! Usar ayuda protege tu espalda." },
          { text: "Levantar el palet solo", type: "incorrect", feedback: "Nunca levantes cargas pesadas solo." },
          { text: "Inclinarse para levantar el palet solo", type: "partial", feedback: "Podrías lastimarte la espalda." }
        ]
      },
      {
        q: "Escenario 3: Vas a manipular una máquina en funcionamiento. ¿Qué debes hacer?",
        emoji: "⚙️",
        options: [
          { text: "Seguir el procedimiento establecido", type: "correct", feedback: "¡Bien! Seguir procedimientos evita accidentes." },
          { text: "Ignorar el procedimiento, la experiencia es mejor", type: "incorrect", feedback: "Ignorar procedimientos es muy peligroso." },
          { text: "Si ya sabes como hacerlo no hay que seguir el procedimiento", type: "partial", feedback: "Puedes sufrir un atrapamiento." }
        ]
      },
      {
        q: "Escenario 4: Estoy trabajando en una máquina y quito la seguridad de máquina. ¿Qué debo hacer?",
        emoji: "🔒",
        options: [
          { text: "Nunca quitar las seguridades", type: "correct", feedback: "¡Bien! Nunca se deben quitar." },
          { text: "Quitarlas si la operación es rápida", type: "partial", feedback: "Aun así aumenta riesgo." },
          { text: "Quitarlas y trabajar con cuidado", type: "incorrect", feedback: "Muy peligroso." }
        ]
      },
      {
        q: "Escenario 5: Estoy en el lavadero y voy a limpiar un tanque metálico con agua caliente. ¿Qué debo hacer?",
        emoji: "💧🔥",
        options: [
          { text: "Usar EPIs adecuados para trabajos con altas temperaturas", type: "correct", feedback: "¡Bien! Previene quemaduras." },
          { text: "La tarea es rápida y pierdo tiempo si me pongo los EPIs", type: "incorrect", feedback: "Riesgo de quemadura." },
          { text: "Únicamente uso guantes de protección", type: "partial", feedback: "No garantiza protección total, pueden hacer salpicaduras en el rostro." }
        ]
      },
      {
        q: "Escenario 6: Te encuentras caminando en zona de riesgo, hay poco espacio y mucho material acumulado. ¿Qué debo hacer?",
        emoji: "🪑📏",
        options: [
          { text: "Mantener la distancia del material", type: "correct", feedback: "¡Bien! Evita golpes." },
          { text: "Ese tipo de material no produce accidentes, es algo rutinario", type: "incorrect", feedback: "Provoca accidentes." },
          { text: "Mover material/muebles sin comunicar a nadie", type: "partial", feedback: "Riesgo de accidente." }
        ]
      },
      {
        q: "Escenario 7: Te encuentras trabajando en una línea y al intentar tomar un frasco sobrepasas el área de trabajo/cintas transportadoras. ¿Qué debiste haber hecho?",
        emoji: "📦↗️",
        options: [
          { text: "Nunca sobrepasar las cintas transportadoras", type: "correct", feedback: "¡Bien! Evita lesiones." },
          { text: "Estirarse para tomar el frasco, la acción es rápida y nunca sucede nada", type: "incorrect", feedback: "Riesgo de tirones y atrapamiento" },
          { text: "Nuestras cintas transportadoras no producen atrapamientos", type: "partial", feedback: "Todas las cintas transportadoras pueden provocar atrapamientos." }
        ]
      },
      {
        q: "Escenario 8: Estamos en el área de envasado y nos encontramos con palets y cajas en el pasillo. ¿Qué debemos hacer?",
        emoji: "📦",
        options: [
          { text: "Mantener despejado el área de tránsito", type: "correct", feedback: "¡Bien! Previene caídas." },
          { text: "Saltar entre palets", type: "incorrect", feedback: "Peligro, has tenido un accidente." },
          { text: "Pasar de largo y no comunicar a nadie", type: "partial", feedback: "La acumulación de material en los pasillos aumenta el riesgo de caída." }
        ]
      },
      {
        q: "Escenario 9: Estoy paletizando y comienzo a sentir molestias en la espalda. ¿Qué debo hacer?",
        emoji: "💪📦",
        options: [
          { text: "Usar la técnica correcta de levantamiento", type: "correct", feedback: "¡Bien! Evita lesiones lumbares." },
          { text: "Continuar el trabajo sin comunicar a nadie de la molestia", type: "incorrect", feedback: "Peligro, provoca dolor y puede agravar la lesión." },
          { text: "No usar ayudas mecánicas como traspalet elevadores, demora demasiado", type: "partial", feedback: "Estás a punto de tener una lesión." }
        ]
      },
      {
        q: "Escenario 10: Estás en el laboratorio, manipulando alcohol y fragancias. ¿Qué debo hacer?",
        emoji: "⚗️👀",
        options: [
          { text: "Colocarme las gafas cuando hay riesgo de proyección de líquidos", type: "correct", feedback: "¡Bien! Protege tus ojos." },
          { text: "No usar las gafas, estoy manipulando poco líquido", type: "incorrect", feedback: "Peligro, riesgo de salpicadura y lesiones en los ojos." },
          { text: "Si lo hago con mucho cuidado no necesito usar las gafas", type: "partial", feedback: "No es suficiente." }
        ]
      }
    ];

    let current = 0;
    let score = 0;
    let ranking = [];
    let userAnswers = [];

    function showQuestion() {
      const quizDiv = document.getElementById('quiz');
      quizDiv.innerHTML = "";
      if (current < questions.length) {
        const q = questions[current];
        const qDiv = document.createElement('div');
        qDiv.className = 'question';
        qDiv.innerHTML = `<h2>${q.q}</h2><div class="emoji">${q.emoji}</div>`;
        const optionsDiv = document.createElement('div');
        optionsDiv.className = 'options';
        q.options.forEach(opt => {
          const btn = document.createElement('button');
          btn.textContent = opt.text;
          btn.onclick = () => handleAnswer(opt, btn);
          optionsDiv.appendChild(btn);
        });
        qDiv.appendChild(optionsDiv);
        quizDiv.appendChild(qDiv);
        updateProgress();
      } else {
        showScore();
      }
    }

    function handleAnswer(selectedOption, selectedBtn) {
      const { type, feedback } = selectedOption;

      if (type === 'correct') score += 10;
      else if (type === 'partial') score += 5;

      userAnswers.push({
        question: questions[current].q,
        emoji: questions[current].emoji,
        selected: selectedOption.text,
        type: selectedOption.type,
        feedback: selectedOption.feedback
      });

      const buttons = selectedBtn.parentNode.querySelectorAll('button');
      buttons.forEach(b => {
        b.disabled = true;
        const option = questions[current].options.find(opt => opt.text === b.textContent);
        if (option) b.classList.add(option.type);
      });

      selectedBtn.style.opacity = '1';

      const feedbackDiv = document.createElement('div');
      feedbackDiv.className = 'feedback show';
      feedbackDiv.textContent = feedback;
      selectedBtn.parentNode.appendChild(feedbackDiv);

      setTimeout(nextQuestion, 2000);
    }

    function nextQuestion() {
      current++;
      showQuestion();
    }

    function showScore() {
      const quizDiv = document.getElementById('quiz');
      ranking.push(score);
      ranking.sort((a, b) => b - a);

      let reviewHTML = `<div style="margin-top:30px;"><h3>Revisión de respuestas con errores</h3>`;
      userAnswers.forEach(ans => {
        if (ans.type !== 'correct') {
          reviewHTML += `
            <div class="review-box ${ans.type}">
              <div><strong>${ans.emoji} ${ans.question}</strong></div>
              <div><strong>Tu respuesta:</strong> <span class="${ans.type}">${ans.selected}</span></div>
              <div><strong>Feedback:</strong> ${ans.feedback}</div>
            </div>`;
        }
      });
      reviewHTML += `</div>`;

      quizDiv.innerHTML = `
        <div class="score">¡Has completado el simulador!<br>Tu puntuación: ${score} / ${questions.length * 10}</div>
        <div class="ranking">Top puntuaciones: ${ranking.slice(0, 5).join(" - ")}</div>
        <div style="margin-top:15px;">Revisa los escenarios donde obtuviste menos puntos y refuerza las medidas de seguridad. ¡La prevención salva vidas!</div>
        ${reviewHTML}
      `;
    }

    function updateProgress() {
      document.getElementById('progress').style.width = ((current / questions.length) * 100) + '%';
    }

    showQuestion();
  </script>
</body>
</html>
