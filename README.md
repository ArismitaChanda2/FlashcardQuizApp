# FlashcardQuizApp
//For the basic structure
index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
<div class="app">
    <h1>Quiz To Try!</h1>
    <div class="quiz">
       <h2 id="question">Are You Ready? </h2>
       <div id="answer-buttons">
          <button class="btn">Option A</button>
          <button class="btn">Option B</button>
          <button class="btn">Option C</button>
          <button class="btn">Option D</button>
       </div>
        <button id="next-btn">Next</button>     
    </div>
</div>
<script src="script.js"></script>
</body>
</html
  
//For styling the layout
style.css
* {
    margin: 0;
    padding: 0;
    font-family: Arial, Helvetica, sans-serif;
    box-sizing: border-box;
}
  body{
      background:  #250116;
  }
  .app{
  background:#b5efff  ;
  width: 90%;
  max-width: 600px;
  margin: 100px auto 0;
  border-radius: 10px;
  padding: 30px;
  
  }
  
  .app h1{
      font-size: 25px;
      color:rgb(143, 28, 53);
      font-weight: 600;
      border-bottom: 1px solid #333;
      padding-bottom: 30px;
      text-align: center;
  }
  .quiz{
      padding: 20px 0;
  
  }
  
  .quiz h2{
      font-size: 18px;
      color:black;
      font-weight: 600;
  }
  
.btn{
      background: #fff;
      color:rgb(75, 4, 4);
      font-weight:500 ;
      width:100%;
      border: 1px solid #222;
      padding: 10px;
      margin: 10px 0;
      text-align: left;
      border-radius: 4px;
      cursor: pointer;
      transition:all 0.5s;
  
  }
  .btn:hover:not([disabled]){
      background: #222;
      color:#baf0ff ;
  }
  .btn:disabled{
    cursor:  no-drop;;
  }
  
  #next-btn {
      background: #001e4d;
      color: rgb(233, 234, 250);
      font-weight:500 ;
      width:150px;
      border: 0;
      padding: 10px;
      margin: 20px auto 0;
      border-radius: 4px;
      cursor: pointer;
      display: none;
  }


  .correct{
     background: #9aeabc;
  }

  .incorrect{
    background: #ff9393;
  }

//For implementing the logic
script.js
const questions= 
[
    {
    question:"What does BCC stand for in an email?",
    answers:[
        {text: "Bold Carbon Copy",correct: false},
        {text: "Blind Carbon Copy",correct: true},
      
        {text: "Bold Computer Copy",correct: false},
      
        {text: "Blind Carbon Copies",correct: false},
      
        ]
   },
   {
     question:"What is the name of the company that was acquired by Oracle on Jan 27,2010?",
    answers:[
        {text: "Sun Microsystems",correct: true},
        {text: "Moon Microsystems",correct:false},
        {text: "Sun Macrosystems",correct: false},
      
        {text: "Moon Macrosystems",correct: false},
      

         ]

    },
    {

        question:"What is the name of the widely used programming lagguage developed by Microsoft?",
         answers:[
        {text: "Visual Studio",correct: false},
        {text: "Microsoft Studio",correct: false},
      
        {text: "Microsoft",correct: false},
      
        {text: "Visual Basic",correct: true},
      
            ]



    },
    {

   question:"How much is a byte equal to?",
    answers:[
        {text: "8 bits",correct: true},
        {text: "32 bits",correct: false},
        {text: "16 bits",correct: false},
        {text: "64 bits",correct: false},
      
           ]

    },
    {
    question:"Who invented Compact Disc?",
     answers:[
        {text: "James T. Russell",correct: true},
        {text: "Fujio Masuoka",correct: false},
        {text: "Thomas Edison",correct: false},
        {text:"Martin Cooper",correct: false},
        ]

    },
    {
        question:"What do you call a person who uses the internet to explore and communicate?",
        answers:[
        {text: "Citizen",correct: false},
        {text: "Resident",correct: false},
        {text: "Cybernaut",correct: true},
        {text: "None of these",correct: false},

                ]



    },
   {
     question:"V-RAM is used for access of the following?",
     answers:[
        {text: "Video & Graphics",correct: true},
        {text: "Text and Images",correct: false},
        {text: "programs",correct: false},
        {text: "only Videos",correct: false},
        ]
    },
   {
      question:"BSNL,Reliance,Shaw Cable,AOL,Tata Indicom all can be kept in which one of the following groups?",
      answers:[
        {text: "ISDN",correct: false},
        {text: "IRC",correct: false},
        {text: "ISP",correct: true},
        {text: "Icons",correct: false},
       ]

    },
    {
    question:"Which of the following is a quickly accessible location which is available to the CPU of the computer?",
    answers:[
        {text: "Memory",correct: false},
        {text: "BIOS",correct: false},
        {text: "Processor Register",correct:true},
        {text: "Graphic Card",correct: false},

        ]
    },

    {

    question:"Which of the following was the first commercial transistor computer?",
     answers:[
        {text: "EDSAC",correct:false},
        {text: "Metrovick950",correct: true},
        {text: "SIRAC",correct: false},
        {text: "Zuse Z4",correct: false},

        ]
    }
];

const questionElement = document.getElementById("question");
const answerButtons = document.getElementById("answer-buttons");
const nextButton = document.getElementById("next-btn");

let currentQuestionIndex= 0;
let score = 0;

function startQuiz(){
currentQuestionIndex = 0;
score= 0;
nextButton.innerHTML = "Next";
showQuestion();
}

function showQuestion(){
    resetState();
let currentQuestion = questions[currentQuestionIndex];
let questionNo = currentQuestionIndex + 1;
questionElement.innerHTML = questionNo + "."+ currentQuestion.question;

currentQuestion.answers.forEach(answer => {
    const button = document.createElement("button");
    button.innerHTML = answer.text;
    button.classList.add("btn");
    answerButtons.appendChild(button);
    if(answer.correct){
       button.dataset.correct = answer.correct;

    }
    button.addEventListener("click", selectAnswer);
    
});
}

function resetState(){
    nextButton.style.display = "none";
    while(answerButtons.firstChild){
      answerButtons.removeChild(answerButtons.firstChild);
    }
}



function selectAnswer(e){
    const selectedBtn = e.target;
    const isCorrect = selectedBtn.dataset.correct == "true";
    if(isCorrect){
         selectedBtn.classList.add("correct");
         score++;

    }else{
          selectedBtn.classList.add("incorrect");

    }
    Array.from(answerButtons.children).forEach(button => 
        {
          if(button.dataset.correct ==="true"){
             button.classList.add("correct");
        }
        button.disabled = true;
        
    });
    nextButton.style.display = "block";


}

function showScore(){

    resetState();
    questionElement.innerHTML = `Your Scored ${score} out of ${questions.length}! `;
    nextButton.innerHTML = "Play Again!";
    nextButton.style.display  = "block";
}



function handleNextButton(){

    currentQuestionIndex++;
    if(currentQuestionIndex < questions.length){
        showQuestion();
    }else{
        showScore();
    }
}



nextButton.addEventListener("click", ()=>{
     if(currentQuestionIndex < questions.length){
        handleNextButton();
     }else{

     startQuiz();
    }   

});

startQuiz();








