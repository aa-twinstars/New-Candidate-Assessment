# New-Candidate-Assessment
This online assessment form is designed to evaluate candidates’ skills in typing (English and Arabic), Excel, and administrative/data entry experience before an interview.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Candidate Online Assessment</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<style>
  body {
    margin: 0;
    font-family: 'Poppins', sans-serif;
    color: #fff;
    background: linear-gradient(135deg, #1E12AA, #BE1982, #F5781E);
    min-height: 100vh;
    padding: 0;
  }
  h1, h2, h3 { text-align: center; }
  section {
    background: rgba(0,0,0,0.5);
    padding: 20px;
    margin: 20px auto;
    border-radius: 12px;
    max-width: 800px;
  }
  textarea, input[type="text"] {
    width: 100%; padding: 8px; margin-top: 5px;
    border-radius: 5px; border: none;
  }
  textarea[disabled] { background: #ddd; color: #555; }
  button {
    display: block; margin: 10px auto; padding: 10px 20px;
    border: none; border-radius: 8px; font-size: 16px;
    cursor: pointer; background: #fff; color: #333;
  }
  button:hover { opacity: 0.85; }
  .hidden { display: none; }
  .result { background: rgba(255,255,255,0.2); padding: 10px; margin-top: 10px; border-radius: 8px; }
  #certificate {
    border: 3px solid #fff;
    padding: 20px; margin: 20px auto;
    max-width: 600px; text-align: center;
    background: rgba(255,255,255,0.1);
  }
</style>
</head>
<body>

<!-- Intro Page -->
<div id="introPage">
  <h1>Candidate Online Assessment</h1>
  <section>
    <h3>Welcome!</h3>
    <p>Please enter your name to begin. This test includes:</p>
    <ul>
      <li>Typing Test (English & Arabic)</li>
      <li>Excel Knowledge</li>
      <li>Admin/Data Entry Experience</li>
    </ul>
    <p>Total time will be tracked automatically.</p>
    <label>Candidate Name:</label>
    <input type="text" id="candidateName">
    <button onclick="startAssessment()">Start Assessment</button>
  </section>
</div>

<!-- Assessment Page -->
<div id="assessmentPage" class="hidden">
  <h1>Assessment in Progress</h1>
  <p style="text-align:center;">Total Duration: <span id="timer">0s</span></p>

  <!-- Typing English -->
  <section>
    <h2>Typing Test (English)</h2>
    <p><b>"The quick brown fox jumps over the lazy dog."</b></p>
    <button onclick="enableTyping('eng1')">Start Typing</button>
    <textarea id="eng1" disabled></textarea>
    <button onclick="finishTyping('eng1')" class="hidden" id="finEng1">Finish</button>
    <div class="result" id="resultEng1"></div>

    <p><b>"Effective communication is key to success."</b></p>
    <button onclick="enableTyping('eng2')">Start Typing</button>
    <textarea id="eng2" disabled></textarea>
    <button onclick="finishTyping('eng2')" class="hidden" id="finEng2">Finish</button>
    <div class="result" id="resultEng2"></div>
  </section>

  <!-- Typing Arabic -->
  <section>
    <h2>Typing Test (Arabic)</h2>
    <p><b>السرعة والدقة في الكتابة أمران مهمان في العمل الإداري اليوم.</b></p>
    <button onclick="enableTyping('arb1')">Start Typing</button>
    <textarea id="arb1" disabled></textarea>
    <button onclick="finishTyping('arb1')" class="hidden" id="finArb1">Finish</button>
    <div class="result" id="resultArb1"></div>

    <p><b>تنظيم الوقت والاهتمام بالتفاصيل يساعدان على إنجاز المهام بشكل أفضل.</b></p>
    <button onclick="enableTyping('arb2')">Start Typing</button>
    <textarea id="arb2" disabled></textarea>
    <button onclick="finishTyping('arb2')" class="hidden" id="finArb2">Finish</button>
    <div class="result" id="resultArb2"></div>
  </section>

  <!-- Excel -->
  <section>
    <h2>Excel Questions</h2>
    <label>1. What is the shortcut key to copy a cell in Excel?</label><input type="text" id="q1">
    <label>2. How do you sum values in a range of cells A1 to A10?</label><input type="text" id="q2">
    <label>3. Which function is used to find the average of numbers in a range B1 to B5?</label><input type="text" id="q3">
    <label>4. In Excel, what is the symbol used to start a formula?</label><input type="text" id="q4">
    <label>5. If cell A1 has 10 and B1 has 5, what formula will multiply these two values?</label><input type="text" id="q5">
    <label>6. What is the function of VLOOKUP in Excel?</label><input type="text" id="q6">
    <label>7. Write a simple VLOOKUP formula to find the price of “Apple” in a table with products in column A and prices in column B.</label><input type="text" id="q7">
    <label>8. Which feature allows you to arrange data in ascending or descending order?</label><input type="text" id="q8">
    <label>9. What is a Pivot Table used for in Excel?</label><input type="text" id="q9">
    <label>10. How do you create a Pivot Table in Excel?</label><input type="text" id="q10">
  </section>

  <!-- Admin -->
  <section>
    <h2>Admin/Data Entry Experience</h2>
    <label>1. Describe your previous experience</label><textarea id="adm1"></textarea>
    <label>2. How do you ensure accuracy?</label><textarea id="adm2"></textarea>
    <label>3. Data management software?</label><textarea id="adm3"></textarea>
    <label>4. How do you prioritize tasks?</label><textarea id="adm4"></textarea>
    <label>5. Example of correcting error</label><textarea id="adm5"></textarea>
  </section>

  <button onclick="submitAll()">Submit All</button>
</div>

<!-- Final Page -->
<div id="finalPage" class="hidden">
  <h1>Assessment Completed</h1>
  <div id="summary"></div>
  <div id="certificate" class="hidden">
    <h2>Certificate of Achievement</h2>
    <p>This is to certify that <span id="certName"></span> has successfully completed the assessment with excellent performance.</p>
  </div>
  <button onclick="downloadPDF()">Download Submission (PDF)</button>
</div>

<script>
let timerInterval, startTime, candidate;
let typingStart={}, typingEnd={}, typingResults={};

const excelAnswers = {
  q1: "Ctrl + C", q2: "=SUM(A1:A10)", q3: "=AVERAGE(B1:B5)", q4: "=",
  q5: "=A1*B1", q6: "To look up a value in a table and return a corresponding value from another column.",
  q7: '=VLOOKUP("Apple", A:B, 2, FALSE)', q8: "Sort",
  q9: "To summarize, analyze, and present large sets of data easily.",
  q10: "Select your data → Go to Insert → PivotTable → Choose location → Click OK"
};

function startAssessment() {
  candidate = document.getElementById("candidateName").value;
  if(!candidate){ alert("Please enter your name."); return;}
  document.getElementById("introPage").classList.add("hidden");
  document.getElementById("assessmentPage").classList.remove("hidden");
  startTime = Date.now();
  timerInterval = setInterval(updateTimer, 1000);
}

function updateTimer(){
  let elapsed = Math.floor((Date.now()-startTime)/1000);
  document.getElementById("timer").innerText = elapsed + "s";
}

function enableTyping(id){
  let textarea = document.getElementById(id);
  textarea.disabled=false;
  textarea.focus();
  document.getElementById("fin"+id.charAt(0).toUpperCase()+id.slice(1)).classList.remove("hidden");
  typingStart[id]=Date.now();
}

function finishTyping(id){
  let textarea=document.getElementById(id);
  textarea.disabled=true;
  document.getElementById("fin"+id.charAt(0).toUpperCase()+id.slice(1)).classList.add("hidden");
  typingEnd[id]=Date.now();
  let timeSec = ((typingEnd[id]-typingStart[id])/1000).toFixed(1);
  let text = textarea.value.trim();
  let words = text.split(/\s+/).length;
  let wpm = ((words/timeSec)*60).toFixed(2);

  const paragraphs={
    eng1:"The quick brown fox jumps over the lazy dog.",
    eng2:"Effective communication is key to success.",
    arb1:"السرعة والدقة في الكتابة أمران مهمان في العمل الإداري اليوم.",
    arb2:"تنظيم الوقت والاهتمام بالتفاصيل يساعدان على إنجاز المهام بشكل أفضل."
  };
  let original = paragraphs[id].split(/\s+/);
  let typedWords = text.split(/\s+/);
  let correct=0;
  for(let i=0;i<Math.min(original.length,typedWords.length);i++) if(original[i]===typedWords[i]) correct++;
  let accuracy = ((correct/original.length)*100).toFixed(2);

  typingResults[id]={time:timeSec,wpm,accuracy,text};
  document.getElementById("result"+id.charAt(0).toUpperCase()+id.slice(1)).innerText=
    `Time: ${timeSec}s, WPM: ${wpm}, Accuracy: ${accuracy}%`;
}

function submitAll(){
  clearInterval(timerInterval);
  let duration = Math.floor((Date.now()-startTime)/1000);

  // Excel score
  let score=0;
  for(let key in excelAnswers){
    let val=document.getElementById(key).value.trim();
    if(val.toUpperCase()===excelAnswers[key].toUpperCase()) score++;
  }
  let percent = (score/10)*100;
  let recommendation = percent>=80 ? "Strong candidate, suitable for data/admin role." : "Needs improvement in Excel and typing accuracy.";

  document.getElementById("assessmentPage").classList.add("hidden");
  document.getElementById("finalPage").classList.remove("hidden");

  let summaryHTML=`<section>
    <h2>Results for ${candidate}</h2>
    <p>Total Time: ${duration}s</p>
    <p>Excel Score: ${score}/10 (${percent}%)</p>
    <p>Recommendation: ${recommendation}</p>
  </section>`;
  document.getElementById("summary").innerHTML=summaryHTML;

  if(percent>=80){
    document.getElementById("certificate").classList.remove("hidden");
    document.getElementById("certName").innerText=candidate;
  }
}

function downloadPDF(){
  const { jsPDF } = window.jspdf;
  let doc = new jsPDF();
  let y=20;
  doc.setFont("helvetica","bold");
  doc.setFontSize(18);
  doc.setTextColor(30,18,170);
  doc.text("Candidate Online Assessment Results",10,y); y+=10;
  doc.setFont("helvetica","normal"); doc.setFontSize(12); doc.setTextColor(0,0,0);
  doc.text("Candidate: "+candidate,10,y); y+=10;

  // Typing Results
  const typingQ=[["Typing English 1","The quick brown fox jumps over the lazy dog.","eng1"],
                 ["Typing English 2","Effective communication is key to success.","eng2"],
                 ["Typing Arabic 1","السرعة والدقة في الكتابة أمران مهمان في العمل الإداري اليوم.","arb1"],
                 ["Typing Arabic 2","تنظيم الوقت والاهتمام بالتفاصيل يساعدان على إنجاز المهام بشكل أفضل.","arb2"]];
  typingQ.forEach(([title, question, id])=>{
    if(y>270){doc.addPage();y=20;}
    doc.setFont("helvetica","bold"); doc.text(title+":",10,y); y+=6;
    doc.setFont("helvetica","normal"); doc.text("Question: "+question,12,y); y+=6;
    let res=typingResults[id];
    let answerText=res?`Answer: ${res.text} | Time: ${res.time}s | WPM: ${res.wpm} | Accuracy: ${res.accuracy}%`:"Answer: (No Answer)";
    let lines=doc.splitTextToSize(answerText,170);
    lines.forEach(line=>{if(y>270){doc.addPage();y=20;} doc.text(line,12,y); y+=6;});
    y+=4;
  });

  // Excel Questions
  const excelQnA=[
    ["1. What is the shortcut key to copy a cell in Excel?",document.getElementById("q1").value],
    ["2. How do you sum values in a range of cells A1 to A10?",document.getElementById("q2").value],
    ["3. Which function is used to find the average of numbers in a range B1 to B5?",document.getElementById("q3").value],
    ["4. In Excel, what is the symbol used to start a formula?",document.getElementById("q4").value],
    ["5. If cell A1 has 10 and B1 has 5, what formula will multiply these two values?",document.getElementById("q5").value],
    ["6. What is the function of VLOOKUP in Excel?",document.getElementById("q6").value],
    ["7. Write a simple VLOOKUP formula to find the price of “Apple” in a table with products in column A and prices in column B.",document.getElementById("q7").value],
    ["8. Which feature allows you to arrange data in ascending or descending order?",document.getElementById("q8").value],
    ["9. What is a Pivot Table used for in Excel?",document.getElementById("q9").value],
    ["10. How do you create a Pivot Table in Excel?",document.getElementById("q10").value]
  ];
  if(y>270){doc.addPage(); y=20;}
  doc.setFont("helvetica","bold"); doc.text("Excel Questions & Answers:",10,y); y+=6;
  doc.setFont("helvetica","normal");
  excelQnA.forEach(([q,a])=>{
    if(y>270){doc.addPage(); y=20;}
    let lines=doc.splitTextToSize("Q: "+q,170);
    lines.forEach(line=>{if(y>270){doc.addPage(); y=20;} doc.text(line,12,y); y+=6;});
    lines=doc.splitTextToSize("A: "+(a||"(No Answer)"),170);
    lines.forEach(line=>{if(y>270){doc.addPage(); y=20;} doc.text(line,14,y); y+=6;});
    y+=4;
  });

  // Admin Questions
  const adminQnA=[
    ["1. Describe your previous experience", document.getElementById("adm1").value],
    ["2. How do you ensure accuracy?", document.getElementById("adm2").value],
    ["3. Data management software?", document.getElementById("adm3").value],
    ["4. How do you prioritize tasks?", document.getElementById("adm4").value],
    ["5. Example of correcting error", document.getElementById("adm5").value]
  ];
  if(y>270){doc.addPage();y=20;}
  doc.setFont("helvetica","bold"); doc.text("Admin Questions & Answers:",10,y); y+=6;
  doc.setFont("helvetica","normal");
  adminQnA.forEach(([q,a])=>{
    if(y>270){doc.addPage();y=20;}
    let lines=doc.splitTextToSize("Q: "+q,170);
    lines.forEach(line=>{if(y>270){doc.addPage();y=20;} doc.text(line,12,y); y+=6;});
    lines=doc.splitTextToSize("A: "+(a||"(No Answer)"),170);
    lines.forEach(line=>{if(y>270){doc.addPage();y=20;} doc.text(line,14,y); y+=6;});
    y+=4;
  });

  // Summary
  if(y>270){doc.addPage(); y=20;}
  doc.setFont("helvetica","bold"); doc.text("Summary & Recommendation:",10,y); y+=6;
  let summaryText=document.getElementById("summary").innerText;
  let lines=doc.splitTextToSize(summaryText,170);
  lines.forEach(line=>{if(y>270){doc.addPage();y=20;} doc.text(line,12,y); y+=6;});

  // Certificate if applicable
  if(!document.getElementById("certificate").classList.contains("hidden")){
    doc.addPage();
    doc.setFontSize(20); doc.setFont("helvetica","bold"); doc.setTextColor(190,25,130);
    doc.text("Certificate of Achievement",50,60);
    doc.setFontSize(14); doc.setFont("helvetica","normal"); doc.setTextColor(0,0,0);
    doc.text("This is to certify that " + candidate,40,90);
    doc.text("has successfully completed the assessment",40,110);
    doc.text("with excellent performance.",40,130);
  }

  doc.save(candidate+"_Assessment.pdf");
}
</script>
</body>
</html>
