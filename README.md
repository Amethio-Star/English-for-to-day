<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Advanced Smart Quiz</title>
<style>
body { font-family: Arial, sans-serif; margin:0; padding:20px; background:#eef2f7; }
.container { max-width:800px; margin:auto; background:white; padding:25px; border-radius:15px; box-shadow:0 0 20px rgba(0,0,0,0.15); }
h1{text-align:center; margin-bottom:20px;}
.question { background:#f9f9f9; padding:15px; margin-bottom:20px; border-radius:10px;}
input[type=text], input[type=radio]{width:95%; padding:10px; margin-top:5px; border-radius:6px; border:1px solid #ccc;}
button{padding:10px 20px; margin-top:15px; border:none; border-radius:8px; background:#4CAF50; color:white; font-size:16px; cursor:pointer;}
button:hover{opacity:0.9;}
#result{font-weight:bold; margin-top:20px; font-size:18px;}
.correct{color:green; font-weight:bold;}
.incorrect{color:red; font-weight:bold;}
</style>
</head>
<body>
<div class="container">
<h1>Advanced Smart Quiz</h1>
<div id="quizArea"></div>
<div id="fillArea"></div>
<div id="writingArea"></div>
<p id="result"></p>
</div>
<script>
const questions = [
  {number:1,question:"Choose the word with a different way of pronunciation in the underlined part.",options:["A. crazy","B. bracelet","C. characteristic","D. operation"],answer:"C. characteristic"},
  {number:2,question:"Choose the word with a different way of pronunciation in the underlined part.",options:["A. honesty","B. conflict","C. property","D. provision"],answer:"D. provision"},
  {number:3,question:"Choose the word with a different stress pattern.",options:["A. virus","B. freedom","C. fitness","D. disease"],answer:"D. disease"},
  {number:4,question:"Choose the word with a different stress pattern.",options:["A. volunteer","B. teenager","C. character","D. gallery"],answer:"A. volunteer"}
];

const fillQuestions = [
  {number:1,question:"John’s parents are very strict, so he ____________ use his smartphone after 9 PM.",answer:"mustn’t"},
  {number:2,question:"She’s thinking of moving out of her apartment ____________ the current rent is too high.",answer:"because"},
  {number:3,question:"Although Kim moved here 2 years ago, she still hasn’t explored all of her ____________.",answer:"neighbourhood"},
  {number:4,question:"His view is very old-fashioned because he was brought __________ in a traditional family.",answer:"up"},
  {number:5,question:"Matt has been doing ____________ exercises as he wants to become stronger.",answer:"strength"}
];

const writingQuestions = [
  {number:1,question:"The mayor (improve) ____________ significantly the city’s infrastructure since she was elected.",answer:"has improved"},
  {number:2,question:"My mother (think) ____________ of limiting my brother’s screen time as his exam is approaching.",answer:"is thinking"},
  {number:3,question:"Although teenagers don’t have to give up (use) __________ social media, they shouldn’t spend too much time on it.",answer:"using"},
  {number:4,question:"Because it rained heavily all yesterday morning, the environment worker (not have to) __________ water the neighbourhood’s garden.",answer:"didn’t have to"},
  {number:5,question:"Mike (have) ____________ difficulty keeping food down now because of food poisoning.",answer:"is having"}
];

function renderMCQ(){
  const area = document.getElementById('quizArea');
  area.innerHTML='<h2>Phonetics & Stress Questions</h2>';
  questions.forEach(q=>{
    let html='<div class="question"><p>'+q.number+'. '+q.question+'</p>';
    q.options.forEach(opt=>{html+='<label><input type="radio" name="q'+q.number+'" value="'+opt+'"> '+opt+'</label><br>';});
    html+='</div>';
    area.innerHTML+=html;
  });
  area.innerHTML+='<button onclick="checkMCQ()">Submit</button>';
}

function checkMCQ(){
  let score=0;
  questions.forEach(q=>{
    const selected=document.querySelector('input[name=q'+q.number+']:checked');
    const qDiv = document.querySelector('input[name=q'+q.number+']').closest('.question');
    qDiv.querySelectorAll('label').forEach(lbl=>{
      lbl.classList.remove('correct','incorrect');
      if(lbl.innerText === q.answer) lbl.classList.add('correct');
      else if(lbl.querySelector('input').checked) lbl.classList.add('incorrect');
    });
    if(selected && selected.value===q.answer) score++;
  });
  document.getElementById('result').innerHTML='Score: '+score+'/'+questions.length;
}

function renderFill(){
  const area = document.getElementById('fillArea');
  area.innerHTML='<h2>Grammar & Vocabulary</h2>';
  fillQuestions.forEach(f=>{
    area.innerHTML+='<div class="question"><p>'+f.number+'. '+f.question+'</p><input type="text" id="f'+f.number+'"></div>';
  });
  area.innerHTML+='<button onclick="checkFill()">Submit</button>';
}

function checkFill(){
  let score=0;
  fillQuestions.forEach(f=>{
    const input = document.getElementById('f'+f.number);
    const val=input.value.trim().toLowerCase();
    const parentDiv=input.closest('.question');
    parentDiv.classList.remove('correct','incorrect');
    if(val===f.answer.toLowerCase()){ score++; parentDiv.classList.add('correct'); }
    else parentDiv.classList.add('incorrect');
  });
  document.getElementById('result').innerHTML+=' | Score: '+score+'/'+fillQuestions.length;
}

function renderWriting(){
  const area = document.getElementById('writingArea');
  area.innerHTML='<h2>Verb Forms / Writing</h2>';
  writingQuestions.forEach(w=>{
    area.innerHTML+='<div class="question"><p>'+w.number+'. '+w.question+'</p><input type="text" id="w'+w.number+'"></div>';
  });
  area.innerHTML+='<button onclick="checkWriting()">Submit</button>';
}

function checkWriting(){
  let score=0;
  writingQuestions.forEach(w=>{
    const input = document.getElementById('w'+w.number);
    const val=input.value.trim().toLowerCase();
    const parentDiv=input.closest('.question');
    parentDiv.classList.remove('correct','incorrect');
    if(val===w.answer.toLowerCase()){ score++; parentDiv.classList.add('correct'); }
    else parentDiv.classList.add('incorrect');
  });
  document.getElementById('result').innerHTML+=' | Score: '+score+'/'+writingQuestions.length;
}

renderMCQ();
renderFill();
renderWriting();
</script>
</body>
</html>

