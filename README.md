<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>3rd Quarter Exam: Trends, Networks, and Critical Thinking</title>
<style>
  body {
    font-family: Arial, sans-serif;
    max-width: 900px;
    margin: auto;
    padding: 20px;
  }
  h1 { text-align: center; }
  .question { margin-bottom: 18px; }
  button {
    padding: 12px 25px;
    font-size: 16px;
    cursor: pointer;
  }
  input[type=radio] { margin-right: 8px; }
  #score { font-weight: bold; margin-top: 20px; }
</style>
</head>
<body>

<h1>3rd Quarter Examination</h1>
<h2>Trends, Networks, and Critical Thinking in the 21st Century</h2>

<label><strong>Student Name:</strong></label><br>
<input type="text" id="studentName" required><br><br>

<div id="questions"></div>

<button onclick="submitExam()">Submit Exam</button>

<p id="score"></p>

<script>
// Questions array: [Question, [Options], correctIndex]
const questions = [
["What is a trend?", ["A pattern of behavior demonstrated by a big number of people within a particular period.","A short-lived idea or temporary event.","Something that is very popular for a short time.","A product that has little, if any, utility but is characterized by a quick rise in sales and popularity followed by a quick decline in sales and popularity."],0],
["What is strategy-planning in any field?", ["The art of developing or carrying out a plan to achieve a goal","The process of conducting research on the business environment","The capacity for thinking conceptually and imaginatively","The process of breaking down a complex problem into parts"],0],
["What is a fad?", ["Something that is very popular for a short time.","A pattern of behavior demonstrated by a big number of people within a particular period.","A short-lived idea or temporary event.","A product that has little, if any, utility but is characterized by a quick rise in sales and popularity followed by a quick decline in sales and popularity."],0],
["It evolves and changes as it continues to grow. What term best describes the statement above?", ["Craze","Phenomenon","Viral","Trend"],3],
["Who said: “Intuition becomes increasingly valuable in the new information society precisely because there is no so much data”?", ["Henry Reed","John Naisbitt","Albert Einstein","Alexis Carrel"],1],
["Which of the following is NOT a type of globalization?", ["Economic Globalization","Social Globalization","Political Globalization","Regional Globalization"],3],
["How does a trend differ from a fad?", ["A trend has a definite beginning and a definite end, while a fad continues to evolve and change.","A trend is a short-lived idea or temporary event, while a fad has a longer staying power.","A trend is not confined to particular segments in society, while a fad is.","A trend is not rooted in people's cultural traditions, beliefs, and values, while a fad is."],2],
["Which of the following is an example of a trend in sports?", ["Hula hoop","Fidget spinner","Wearable devices that monitor training performance","Candy Crush App"],2],
["Which characteristic of a trend is not applicable to a fad?", ["Duration of time","Cultural basis","Transitory increase and decrease","Confined to particular segments in society"],1],
["Which stage of the process of identifying a trend involves the participation of entrepreneurial and business firms to develop and innovate ideas?", ["Fringe stage","Mainstream stage","Trendy stage","None of the above"],0],
["Which of the following is not an element of a trend?", ["Duration of time","Cultural basis","Acceptability","Triviality"],3],
["What is the center of influence in social networks?", ["The person who can give favors and make things happen.","The person with the most followers.","The person who is most well-known in the community."],0],
["Which of the following characteristics is true of a fad?", ["Fad is accepted by many industries and people.","Fad has a longer staying power and enjoys a longer period of popularity.","Fad is not created but just revived from a style that existed all along in the lives of some subgroup.","Fad is not confined to particular segments in society."],3],
["Which of the following is an example of a fad?", ["Stem cell treatment","Online ticketing","Pokémon Go","Home solar electric system"],2],
["What is the definition of parts in relation to the whole?", ["The subdivisions into which something is or is regarded as divided and which together constitute the completeness of the components.","The subdivisions that are separated and do not constitute the completeness of the components.","The subdivisions that constitute the completeness of the components but are not regarded as a whole.","The subdivisions that are not separated but constitute the completeness of the components."],0],
["What is the impact of deforestation on climate change?", ["Deforestation reduces the amount of carbon dioxide in the atmosphere","Deforestation releases carbon dioxide into the atmosphere","Deforestation has no impact on climate change","None of the above"],1],
["The following are definitions of cause, EXCEPT:", ["Something that brings effect or result","Reason for an action or condition","Bring forth or give rise to","Something produced"],3],
["Which stage of the process of identifying a trend involves the participation of 'conservative consumers' joining the trend, and corporations and company brands exploiting the growing demand for the idea?", ["Fringe stage","Trendy stage","Mainstream stage","None of the above"],2],
["What is the cultural basis of a trend?", ["The trend is confined to particular segments in society.","The trend has longer staying power and enjoys a longer period of popularity.","The trend is rooted on the people’s cultural traditions, beliefs, and values.","The trend shows transitory increase or decrease of a particular idea, event, or phenomenon."],2],
["When is it appropriate to use strategic analysis?", ["When conducting research on the business environment within which an organization operates","When determining the best path to take when planning to make changes in an organization","When identifying key goals","When creating a personal SWOT analysis"],1],
["What is the impact of individual actions on mitigating climate change?", ["Individual actions have no impact on mitigating climate change","Individual actions can have a significant impact on mitigating climate change","Individual actions are only important for reducing waste, not mitigating climate change","None of the above"],1],
["What is the purpose of action planning?", ["To identify the direction of the department","To answer the question of what success would look like","To identify key goals","To clarify the ways in which daily work will help move the goals forward"],3],
["What is the purpose of reflecting on the outcomes?", ["To identify the direction of the department","To answer the question of what success would look like","To clarify the ways in which daily work will help move the goals forward","To evaluate the effectiveness of the implemented solution and learn"],3],
["Do you think intuitive thinking is more valuable than logical thinking? Why or why not?", ["Yes, because it allows us to make quick decisions without needing to rely on past experiences or knowledge.","No, because logical thinking is more reliable and objective.","It depends on the situation and context in which each type of thinking is used."],2],
["Come up with a scenario where intuitive thinking can be used to solve a problem that cannot be solved by logical thinking alone.", ["A doctor trying to diagnose a patient's illness when their symptoms do not match any known medical conditions.","A motorcycle mechanic diagnose the defect using users manual.","Engineer who follow step by step process in building a house.","None of the above"],0],
["Develop a plan to reduce your carbon footprint by 50%. Which of the following is not appropriate?", ["Reducing meat consumption and adopting a more plant-based diet","Using reusable bags, containers, and utensils instead of single-use plastic","Supporting companies and products with sustainable practices and policies.","Switching from energy-efficient light bulbs and appliances to more energy consuming appliances."],3]
];

// Generate questions dynamically
const container = document.getElementById("questions");
questions.forEach((q,i)=>{
  let div=document.createElement("div");
  div.className="question";
  div.innerHTML=`<p>${i+1}. ${q[0]}</p>`;
  q[1].forEach((opt,idx)=>{
    div.innerHTML+=`
      <input type="radio" name="q${i}" value="${idx===q[2]?1:0}"> ${opt}<br>`;
  });
  container.appendChild(div);
});

// Submit Exam: score only after all answered
function submitExam(){
  const name = document.getElementById("studentName").value.trim();
  if(!name){
    alert("Please enter your name.");
    return;
  }
  
  let answered = 0, score = 0;
  questions.forEach((q,i)=>{
    const sel = document.querySelector(`input[name=q${i}]:checked`);
    if(sel) { answered++; score += Number(sel.value); }
  });
  
  if(answered < questions.length){
    alert("Please answer all questions before submitting.");
    return;
  }
  
  document.getElementById("score").innerHTML = `${name}, your score is <strong>${score}/${questions.length}</strong>`;
}

// Anti-cheating: warn if leaving page
window.onblur = function(){ alert("Warning: Switching tabs or leaving the exam page is not allowed!"); };

// Disable right-click and text selection
document.addEventListener('contextmenu', e => e.preventDefault());
document.addEventListener('selectstart', e => e.preventDefault());

</script>

</body>
</html>
