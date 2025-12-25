
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>NICO</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body {
  font-family: Arial;
  background: #0f172a;
  color: white;
  text-align: center;
  padding: 20px;
}
button {
  padding: 15px 25px;
  font-size: 18px;
  margin-top: 20px;
  border: none;
  border-radius: 10px;
  background: #22c55e;
  color: black;
}
#log {
  margin-top: 20px;
  font-size: 16px;
}
</style>
</head>

<body>

<h1>🤖 نيكو</h1>
<p>مساعد ذكي يتكلم العربية</p>

<button onclick="startNico()">🎤 تحدث مع نيكو</button>

<div id="log"></div>

<script>
const log = document.getElementById("log");

function speak(text){
  const msg = new SpeechSynthesisUtterance(text);
  msg.lang = "ar-SA";
  speechSynthesis.speak(msg);
}

function startNico(){
  speak("مرحبًا، أنا نيكو. تحدث معي الآن");
  
  const rec = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
  rec.lang = "ar-SA";
  rec.start();

  rec.onresult = (e) => {
    const text = e.results[0][0].transcript;
    log.innerHTML = "🧑 أنت: " + text;
    reply(text);
  }
}

function reply(text){
  let answer = "لم أفهم سؤالك";
  if(text.includes("اسمك")) answer = "اسمي نيكو";
  if(text.includes("كيفك")) answer = "أنا بخير، شكرًا لسؤالك";
  if(text.includes("السلام")) answer = "وعليكم السلام ورحمة الله";

  log.innerHTML += "<br>🤖 نيكو: " + answer;
  speak(answer);
}
</script>

</body>
</html>
