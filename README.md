# quiz-ifba-estudo

import { useState } from "react"; import { Card, CardContent } from "@/components/ui/card"; import { Button } from "@/components/ui/button";

// Questões de exemplo (você pode trocar pelo conteúdo real do IFBA 2026) const questions = { portugues: [ { q: "Qual é o sujeito da frase: 'Os alunos estudam bastante'?", a: "Os alunos" }, { q: "Encontre o verbo da frase: 'A menina correu rápido'.", a: "correu" }, // ... até 10 questões ], matematica: [ { q: "Qual é o resultado de 7 x 8?", a: "56" }, { q: "A raiz quadrada de 144 é?", a: "12" }, // ... até 10 questões ], humanas: [ { q: "Quem foi o primeiro presidente do Brasil?", a: "Deodoro da Fonseca" }, { q: "Qual é a capital da França?", a: "Paris" }, // ... até 10 questões ], natureza: [ { q: "Qual é o símbolo químico da água?", a: "H2O" }, { q: "Qual planeta é conhecido como planeta vermelho?", a: "Marte" }, // ... até 10 questões ], redacao: [ { q: "O que é uma tese em um texto dissertativo?", a: "É a ideia principal defendida" }, { q: "Quantos parágrafos em média tem uma redação do Enem?", a: "4 a 5" }, // ... até 10 questões ], };

function Quiz({ subject, goToEstudos }) { const [step, setStep] = useState(0); const [answers, setAnswers] = useState([]); const [finished, setFinished] = useState(false);

const qs = questions[subject];

function handleAnswer(ans) { setAnswers([...answers, ans]); if (step + 1 < qs.length) { setStep(step + 1); } else { setFinished(true); } }

function restartQuiz() { setStep(0); setAnswers([]); setFinished(false); }

return ( <Card className="p-4"> <CardContent> {!finished ? ( <div> <h2 className="text-xl font-bold mb-2">{qs[step].q}</h2> <Button onClick={() => handleAnswer(prompt("Digite sua resposta:"))}> Responder </Button> </div> ) : ( <div> <h2 className="text-xl font-bold mb-4">Gabarito</h2> {qs.map((q, i) => ( <p key={i}> <strong>{q.q}</strong><br /> Sua resposta: {answers[i]} <br /> Correto: {q.a} </p> ))} <div className="flex gap-2 mt-4"> <Button onClick={goToEstudos}>Estudar</Button> <Button onClick={restartQuiz}>Fazer outro quiz</Button> </div> </div> )} </CardContent> </Card> ); }

export default function App() { const [tab, setTab] = useState("estudos");

return ( <div className="p-6"> <nav className="flex gap-4 mb-6"> <Button onClick={() => setTab("estudos")}>Estudos</Button> <Button onClick={() => setTab("portugues")}>Quiz Português</Button> <Button onClick={() => setTab("matematica")}>Quiz Matemática</Button> <Button onClick={() => setTab("humanas")}>Quiz Ciências Humanas</Button> <Button onClick={() => setTab("natureza")}>Quiz Ciências da Natureza</Button> <Button onClick={() => setTab("redacao")}>Quiz Redação</Button> </nav>

{tab === "estudos" && (
    <Card className="p-4">
      <CardContent>
        <h1 className="text-2xl font-bold mb-4">Conteúdos de Estudos - IFBA 2026</h1>
        <p>
          Aqui você encontra os conteúdos detalhados de Português, Matemática,
          Ciências Humanas, Ciências da Natureza e Redação.
        </p>
        <ul className="list-disc ml-6 mt-2">
          <li>Português: interpretação de texto, gramática, literatura...</li>
          <li>Matemática: álgebra, geometria, porcentagem...</li>
          <li>Ciências Humanas: história do Brasil, geografia, filosofia...</li>
          <li>Ciências da Natureza: física, química, biologia...</li>
          <li>Redação: tese, argumentos, coesão, conclusão...</li>
        </ul>
      </CardContent>
    </Card>
  )}

  {tab !== "estudos" && tab !== "" && (
    <Quiz subject={tab} goToEstudos={() => setTab("estudos")} />
  )}
</div>

); }

