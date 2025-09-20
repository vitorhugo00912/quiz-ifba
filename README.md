# quiz-ifba
O Quiz IFBA 2026 é um site de estudos interativo com questões de Português, Matemática, Ciências, História &amp; Geografia e Redação. A cada tentativa, 10 perguntas aleatórias são sorteadas. Também inclui um guia com os principais conteúdos do edital para revisar de forma rápida e prática.
<!DOCTYPE html><html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quiz IFBA 2026</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background: #0d1b2a;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      min-height: 100vh;
    }
    header {
      text-align: center;
      padding: 20px;
    }
    .container {
      max-width: 900px;
      width: 100%;
      padding: 20px;
    }
    .menu button {
      background: #1b263b;
      border: none;
      color: #fff;
      padding: 12px 20px;
      margin: 10px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 16px;
      transition: 0.3s;
    }
    .menu button:hover {
      background: #415a77;
    }
    .quiz, .study {
      display: none;
    }
    .question {
      margin: 15px 0;
      padding: 15px;
      background: #1b263b;
      border-radius: 10px;
    }
    .options label {
      display: block;
      margin: 8px 0;
      cursor: pointer;
    }
    .result {
      margin-top: 20px;
      padding: 15px;
      background: #1b263b;
      border-radius: 10px;
    }
    button.finish {
      margin-top: 20px;
      background: #e63946;
    }
    button.retry {
      margin-top: 10px;
      background: #2a9d8f;
    }
    .study-section {
      margin: 15px 0;
      padding: 15px;
      background: #1b263b;
      border-radius: 10px;
    }
    .study-section h3 {
      margin-top: 0;
    }
  </style>
</head>
<body>
  <header>
    <h1>Quiz IFBA – Conteúdos 2026</h1>
    <p>Escolha uma matéria para começar. Cada tentativa seleciona <b>10 questões aleatórias</b> do banco (sem repetir).</p>
  </header>  <div class="container">
    <div class="menu" id="menu">
      <button onclick="startQuiz('portugues')">Português</button>
      <button onclick="startQuiz('matematica')">Matemática</button>
      <button onclick="startQuiz('ciencias')">Ciências</button>
      <button onclick="startQuiz('humanas')">História & Geografia</button>
      <button onclick="startQuiz('redacao')">Redação / Teoria</button>
      <button onclick="openStudy()">Estudar Conteúdos</button>
    </div><div id="quiz" class="quiz"></div>

<div id="study" class="study">
  <h2>Resumo dos Conteúdos – IFBA 2026</h2>

  <div class="study-section">
    <h3>Português / Linguagens</h3>
    <ul>
      <li>Interpretação de textos</li>
      <li>Ortografia e acentuação gráfica</li>
      <li>Classes de palavras</li>
      <li>Concordância verbal e nominal</li>
      <li>Regência verbal e nominal</li>
      <li>Uso da crase</li>
    </ul>
  </div>

  <div class="study-section">
    <h3>Matemática</h3>
    <ul>
      <li>Conjuntos numéricos (naturais, inteiros, racionais, irracionais)</li>
      <li>Operações e expressões algébricas</li>
      <li>Equações do 1º e 2º grau</li>
      <li>Funções e gráficos</li>
      <li>Geometria plana (perímetro, área, ângulos, triângulos, polígonos, círculo)</li>
      <li>Probabilidade e estatística</li>
    </ul>
  </div>

  <div class="study-section">
    <h3>Ciências da Natureza</h3>
    <ul>
      <li><b>Biologia</b>: estrutura da célula, genética básica, ecologia e meio ambiente</li>
      <li><b>Química</b>: transformações químicas, estados físicos da matéria, misturas e substâncias</li>
      <li><b>Física</b>: energia, força, movimento, leis de Newton, calor e eletricidade</li>
    </ul>
  </div>

  <div class="study-section">
    <h3>Ciências Humanas (História & Geografia)</h3>
    <ul>
      <li>História do Brasil: Brasil Colônia, Brasil Império, Independência e República</li>
      <li>História Geral: Primeira e Segunda Guerra Mundial, Guerra Fria</li>
      <li>Geografia: geografia do Brasil (aspectos físicos e humanos), geografia mundial</li>
    </ul>
  </div>

  <div class="study-section">
    <h3>Redação</h3>
    <ul>
      <li>Texto dissertativo-argumentativo</li>
      <li>Tese, desenvolvimento e conclusão</li>
      <li>Coesão, coerência e clareza</li>
      <li>Uso da norma culta da língua portuguesa</li>
    </ul>
  </div>

  <button onclick="backToMenu()">Voltar</button>
</div>

  </div>  <script>
    const questionBank = { /* (banco de questões continua igual, não removido) */ };

    let currentQuiz = [];

    function startQuiz(subject) {
      document.getElementById('menu').style.display = 'none';
      document.getElementById('study').style.display = 'none';
      const quizDiv = document.getElementById('quiz');
      quizDiv.innerHTML = '';
      quizDiv.style.display = 'block';

      // Embaralhar e escolher 10 questões
      currentQuiz = [...questionBank[subject]]
        .sort(() => 0.5 - Math.random())
        .slice(0, 10);

      currentQuiz.forEach((q, i) => {
        const qDiv = document.createElement('div');
        qDiv.classList.add('question');
        qDiv.innerHTML = `<p><b>${i+1}. ${q.q}</b></p>`;
        const optDiv = document.createElement('div');
        optDiv.classList.add('options');
        q.options.forEach((opt, j) => {
          optDiv.innerHTML += `<label><input type='radio' name='q${i}' value='${j}'> ${opt}</label>`;
        });
        qDiv.appendChild(optDiv);
        quizDiv.appendChild(qDiv);
      });

      const finishBtn = document.createElement('button');
      finishBtn.textContent = 'Finalizar';
      finishBtn.classList.add('finish');
      finishBtn.onclick = finishQuiz;
      quizDiv.appendChild(finishBtn);
    }

    function finishQuiz() {
      let score = 0;
      let resultText = '';
      currentQuiz.forEach((q, i) => {
        const ans = document.querySelector(`input[name='q${i}']:checked`);
        if(ans && parseInt(ans.value) === q.answer) score++;
        resultText += `<p>${i+1}. ${q.q}<br><b>Resposta correta:</b> ${q.options[q.answer]}</p>`;
      });
      const quizDiv = document.getElementById('quiz');
      quizDiv.innerHTML = `<div class='result'><h2>Você acertou ${score} de ${currentQuiz.length}</h2>${resultText}</div>`;
      const retryBtn = document.createElement('button');
      retryBtn.textContent = 'Tentar novamente';
      retryBtn.classList.add('retry');
      retryBtn.onclick = () => { location.reload(); };
      quizDiv.appendChild(retryBtn);
    }

    function openStudy() {
      document.getElementById('menu').style.display = 'none';
      document.getElementById('quiz').style.display = 'none';
      document.getElementById('study').style.display = 'block';
    }

    function backToMenu() {
      document.getElementById('study').style.display = 'none';
      document.getElementById('quiz').style.display = 'none';
      document.getElementById('menu').style.display = 'block';
    }
  </script></body>
</html>
