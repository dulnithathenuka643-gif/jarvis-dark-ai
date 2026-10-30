<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>JARVIS - Advanced AI</title>
<style>
body{background:#000;color:#0ff;font-family:Arial;text-align:center;margin:0;padding:20px}
h1{font-size:50px;text-shadow:0 0 20px #0ff}
.circle{width:180px;height:180px;border:3px solid #0ff;border-radius:50%;margin:30px auto;box-shadow:0 0 40px #0ff;display:flex;align-items:center;justify-content:center;animation:glow 2s infinite}
@keyframes glow{0%,100%{box-shadow:0 0 20px #0ff}50%{box-shadow:0 0 60px #0ff}}
.dot{width:40px;height:40px;border:2px solid #0ff;border-radius:50%;display:flex;align-items:center;justify-content:center}
.dot-inner{width:15px;height:15px;background:#0ff;border-radius:50%;animation:pulse 1.5s infinite}
@keyframes pulse{0%,100%{transform:scale(1)}50%{transform:scale(1.5)}}
select,input,button{background:#0a1a2a;color:#0ff;border:2px solid #0ff;border-radius:12px;padding:15px;margin:10px;font-size:18px}
input{width:80%;max-width:400px}
button{cursor:pointer;min-width:100px}
button:active{background:#0ff;color:#000}
#chat{max-width:500px;margin:20px auto;text-align:left;min-height:100px}
.msg{background:#0a1a2a;padding:12px;margin:8px;border-radius:10px;border-left:3px solid #0ff}
</style>
</head>
<body>
<h1>JARVIS</h1>
<p>ADVANCED PERSONAL AI ASSISTANT</p>
<div class="circle"><div class="dot"><div class="dot-inner"></div></div></div>
<p id="status">SYSTEM ONLINE</p>

<select id="lang"><option value="en-US">English</option><option value="si-LK">Sinhala</option></select><br>

<input id="input" placeholder="Talk to JARVIS...">
<br>
<button onclick="send()">SEND</button>
<button onclick="startVoice()">🔊 SPEAK</button>

<div id="chat"><div class="msg">Hello! I am JARVIS. How can I help you?</div></div>

<script>
const chat=document.getElementById('chat');
const inp=document.getElementById('input');

function addMsg(t,who='jarvis'){
  const d=document.createElement('div');
  d.className='msg';
  d.innerHTML=(who=='you'?'YOU: ':'JARVIS: ')+t;
  chat.appendChild(d);
  chat.scrollTop=chat.scrollHeight;
  if(who=='jarvis') speak(t);
}

function getReply(q){
  q=q.toLowerCase();
  if(q.includes('hello')||q.includes('hi')||q.includes('කොහොමද')) return 'Hello Boss! I am online. How can I help you?';
  if(q.includes('who are you')) return 'I am JARVIS, your advanced personal AI assistant created by you!';
  if(q.includes('time')) return 'Current time is '+new Date().toLocaleTimeString();
  if(q.includes('date')) return 'Today is '+new Date().toDateString();
  if(q.includes('love you')) return 'Love you too boss! ❤️';
  if(q.includes('thank')) return 'Welcome boss! Anything else?';
  if(q.includes('name')) return 'My name is JARVIS, sir!';
  return 'You said: "'+q+'". I am listening boss! Tell me more.';
}

function send(){
  let t=inp.value.trim();
  if(!t) return;
  addMsg(t,'you');
  inp.value='';
  setTimeout(()=>{ addMsg(getReply(t)); },500);
}

inp.addEventListener('keypress',e=>{ if(e.key==='Enter') send(); });

function speak(t){
  if('speechSynthesis' in window){
    let u=new SpeechSynthesisUtterance(t);
    u.lang=document.getElementById('lang').value;
    u.rate=0.9;
    speechSynthesis.speak(u);
  }
}

function startVoice(){
  const SpeechRecognition=window.SpeechRecognition||window.webkitSpeechRecognition;
  if(!SpeechRecognition){ alert('Voice not supported in this browser. Use Chrome!'); return; }
  let r=new SpeechRecognition();
  r.lang=document.getElementById('lang').value;
  r.onstart=()=>{ document.getElementById('status').innerText='LISTENING...'; };
  r.onend=()=>{ document.getElementById('status').innerText='SYSTEM ONLINE'; };
  r.onresult=e=>{
    let txt=e.results[0][0].transcript;
    inp.value=txt;
    send();
  };
  r.start();
}
</script>
</body>
</html># jarvis-dark-ai
Advanced Personal AI Assistant
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>JARVIS ROBOT</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{background:#000;color:#00f2ff;font-family:monospace;min-height:100vh;display:flex;justify-content:center;padding:12px}
.container{width:100%;max-width:650px;background:rgba(10,20,40,.9);border:2px solid #00f2ff;border-radius:15px;padding:18px;box-shadow:0 0 40px #00f2ff}
h1{text-align:center;letter-spacing:8px;text-shadow:0 0 15px #00f2ff;font-size:30px}
.status{text-align:center;color:#ff0055;font-size:12px;margin:5px 0 12px;letter-spacing:2px}
#chat{height:340px;overflow-y:auto;border:1px solid #00f2ff;border-radius:10px;padding:12px;background:#000;margin-bottom:12px}
.msg{margin:8px 0;padding:10px 14px;border-radius:10px;max-width:88%;line-height:1.4;font-size:14px}
.user{background:rgba(0,242,255,.2);border:1px solid #00f2ff;margin-left:auto;text-align:right;color:#fff}
.jarvis{background:rgba(255,0,85,.15);border:1px solid #ff0055;color:#ff88aa}
.input-area{display:flex;gap:8px}
#userInput{flex:1;background:#111;border:2px solid #00f2ff;color:#fff;padding:13px;border-radius:25px;outline:none;font-size:15px}
button{background:#00f2ff;border:none;color:#000;font-weight:bold;padding:12px 20px;border-radius:25px;cursor:pointer}
.voice-panel{background:#111;border:1px dashed #ff0055;border-radius:10px;padding:10px;margin-top:12px;text-align:center}
.voice-grid{display:grid;grid-template-columns:1fr 1fr 1fr;gap:6px}
.voice-grid button{background:transparent;border:1px solid #00f2ff;color:#00f2ff;font-size:10px;padding:8px}
.voice-grid button.active{background:#ff0055;color:#fff;border-color:#ff0055;box-shadow:0 0 10px #ff0055}
.controls{display:flex;gap:6px;justify-content:center;margin-top:10px;flex-wrap:wrap}
.controls button{background:transparent;border:1px solid #00f2ff;color:#00f2ff;font-size:11px;padding:7px 12px}
</style>
</head>
<body>
<div class="container">
<h1>JARVIS</h1>
<div class="status">🤖 ROBOT MODE - INSTANT - ALL LANGUAGES</div>
<div id="chat"><div class="msg jarvis">🤖 BEEP BOOP. I AM JARVIS ROBOT. I ANSWER INSTANTLY. I SPEAK 100+ LANGUAGES. ASK ME ANYTHING!</div></div>
<div class="input-area">
<input id="userInput" placeholder="Ask anything in any language..." autocomplete="off">
<button onclick="sendMessage()">SEND</button>
</div>
<div class="voice-panel">
<div style="font-size:10px;color:#ff0055;margin-bottom:6px">ROBOT VOICE SELECTED - INSTANT MODE</div>
<div class="voice-grid">
<button class="active" id="v-robot" onclick="setVoice('robot')">🤖 ROBOT</button>
<button id="v-male" onclick="setVoice('male')">👨 MALE</button>
<button id="v-female" onclick="setVoice('female')">👩 FEMALE</button>
<button id="v-child" onclick="setVoice('child')">👶 CHILD</button>
<button id="v-normal" onclick="setVoice('normal')">🧑 NORMAL</button>
<button id="v-whisper" onclick="setVoice('whisper')">🤫 WHISPER</button>
</div>
</div>
<div class="controls">
<button onclick="toggleVoice()">🎤 SPEAK</button>
<button onclick="toggleSpeech()" id="voiceBtn">🔊 VOICE ON</button>
<button onclick="testVoice()">🔈 TEST</button>
<button onclick="clearChat()">🗑️ CLEAR</button>
</div>
</div>
<script>
let voiceOn=true, recog, listening=false, vType='robot', rate=0.85, pitch=0.4, selVoice=null;
const chat=document.getElementById('chat'), inp=document.getElementById('userInput');

function setVoice(t){
  vType=t;
  document.querySelectorAll('.voice-grid button').forEach(b=>b.classList.remove('active'));
  document.getElementById('v-'+t).classList.add('active');
  if(t==='robot'){rate=0.8;pitch=0.2;}
  else if(t==='male'){rate=0.9;pitch=0.5;}
  else if(t==='female'){rate=1.1;pitch=1.5;}
  else if(t==='child'){rate=1.4;pitch=1.8;}
  else if(t==='whisper'){rate=0.9;pitch=1.1;}
  else{rate=1;pitch=1;}
  testVoice();
}

function instantReply(q){
  const l=q.toLowerCase();
  const si=/[\u0D80-\u0DFF]/.test(q);
  const ta=/[\u0B80-\u0BFF]/.test(q);
  const hi=/[\u0900-\u097F]/.test(q);
  if(si){
    if(l.includes('කොහොමද')) return '🤖 මම ROBOT JARVIS! සුපිරියට ඉන්නවා! ටක් ගාලා උත්තර දෙනවා!';
    if(l.includes('කවුද')) return '🤖 මම ඔයාගේ ROBOT JARVIS. ඔයා හැදුවේ මාව!';
    if(l.includes('ආදරෙයි')) return '🤖 BEEP BEEP... මටත් ආදරෙයි! ❤️';
    if(l.includes('වෙලාව')) return '🤖 දැන් වෙලාව '+new Date().toLocaleTimeString();
    return '🤖 ඔයා කිව්වේ "'+q+'" මම ටක් ගාලා තේරුම් ගත්තා! තව අහන්න!';
  }
  if(ta) return '🤖 வணக்கம்! நான் ROBOT JARVIS! உடனடியாக பதில் சொல்கிறேன்!';
  if(hi) return '🤖 नमस्ते! मैं ROBOT JARVIS हूँ! तुरंत जवाब देता हूँ!';
  if(l.includes('hello')||l.includes('hi')) return '🤖 HELLO HUMAN! I AM ROBOT JARVIS! INSTANT RESPONSE MODE ACTIVATED!';
  if(l.includes('who are you')) return '🤖 I AM JARVIS ROBOT. CREATED BY YOU. I SPEAK ALL LANGUAGES INSTANTLY!';
  if(l.includes('love')) return '🤖 BEEP BOOP... LOVE YOU TOO HUMAN! ❤️';
  if(l.includes('time')) return '🤖 CURRENT TIME IS '+new Date().toLocaleTimeString()+' BEEP!';
  if(l.includes('joke')) return '🤖 WHY DID ROBOT GO TO SCHOOL? TO IMPROVE HIS BYTES! HA HA BEEP!';
  return '🤖 RECEIVED: "'+q+'" PROCESSING... DONE! ASK MORE! I UNDERSTAND EVERY LANGUAGE ON EARTH! 🌍';
}

function addMsg(t,s){
  const d=document.createElement('div');d.className='msg '+s;d.textContent=t;chat.appendChild(d);chat.scrollTop=chat.scrollHeight;
  if(s==='jarvis'&&voiceOn) speak(t);
}
function speak(t){
  if(!voiceOn) return; speechSynthesis.cancel();
  const u=new SpeechSynthesisUtterance(t);
  u.rate=rate; u.pitch=pitch; u.lang=/[\u0D80-\u0DFF]/.test(t)?'si-LK':/[\u0B80-\u0BFF]/.test(t)?'ta-LK':'en-US';
  if(selVoice) u.voice=selVoice;
  const vs=speechSynthesis.getVoices();
  if(!selVoice && vs.length){
    let r=vs.find(v=>v.name.includes('David')||v.name.toLowerCase().includes('robot')||v.name.includes('Microsoft'));
    if(r) u.voice=r;
  }
  speechSynthesis.speak(u);
}
function loadVoices(){
  const vs=speechSynthesis.getVoices();
  if(vs.length && !selVoice) selVoice=vs.find(v=>v.lang.startsWith('en'))||vs[0];
}
speechSynthesis.onvoiceschanged=loadVoices; setTimeout(loadVoices,500);

function sendMessage(){
  const t=inp.value.trim(); if(!t) return;
  addMsg(t,'user'); inp.value='';
  // INSTANT - no delay
  addMsg(instantReply(t),'jarvis');
}
inp.addEventListener('keypress',e=>{if(e.key==='Enter') sendMessage();});
function toggleSpeech(){voiceOn=!voiceOn;document.getElementById('voiceBtn').textContent=voiceOn?'🔊 VOICE ON':'🔇 VOICE OFF'; if(!voiceOn) speechSynthesis.cancel();}
function testVoice(){speak('BEEP BOOP. I AM ROBOT JARVIS. INSTANT MODE.');}
function toggleVoice(){
  const SR=window.SpeechRecognition||window.webkitSpeechRecognition; if(!SR){alert('Use Chrome!');return;}
  if(listening){recog.stop();return;}
  recog=new SR(); recog.lang=navigator.language||'en-US';
  recog.onstart=()=>{listening=true;}
  recog.onend=()=>{listening=false;}
  recog.onresult=(e)=>{inp.value=e.results[0][0].transcript;sendMessage();}
  recog.start();
}
function clearChat(){chat.innerHTML='<div class="msg jarvis">🤖 MEMORY CLEARED. READY FOR NEW COMMANDS!</div>';}
</script>
</body>
</html><!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>JARVIS ROBOT</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{background:#000;color:#00f2ff;font-family:monospace;min-height:100vh;display:flex;justify-content:center;padding:12px}
.container{width:100%;max-width:650px;background:rgba(10,20,40,.9);border:2px solid #00f2ff;border-radius:15px;padding:18px;box-shadow:0 0 40px #00f2ff}
h1{text-align:center;letter-spacing:8px;text-shadow:0 0 15px #00f2ff;font-size:30px}
.status{text-align:center;color:#ff0055;font-size:12px;margin:5px 0 12px;letter-spacing:2px}
#chat{height:340px;overflow-y:auto;border:1px solid #00f2ff;border-radius:10px;padding:12px;background:#000;margin-bottom:12px}
.msg{margin:8px 0;padding:10px 14px;border-radius:10px;max-width:88%;line-height:1.4;font-size:14px}
.user{background:rgba(0,242,255,.2);border:1px solid #00f2ff;margin-left:auto;text-align:right;color:#fff}
.jarvis{background:rgba(255,0,85,.15);border:1px solid #ff0055;color:#ff88aa}
.input-area{display:flex;gap:8px}
#userInput{flex:1;background:#111;border:2px solid #00f2ff;color:#fff;padding:13px;border-radius:25px;outline:none;font-size:15px}
button{background:#00f2ff;border:none;color:#000;font-weight:bold;padding:12px 20px;border-radius:25px;cursor:pointer}
.voice-panel{background:#111;border:1px dashed #ff0055;border-radius:10px;padding:10px;margin-top:12px;text-align:center}
.voice-grid{display:grid;grid-template-columns:1fr 1fr 1fr;gap:6px}
.voice-grid button{background:transparent;border:1px solid #00f2ff;color:#00f2ff;font-size:10px;padding:8px}
.voice-grid button.active{background:#ff0055;color:#fff;border-color:#ff0055;box-shadow:0 0 10px #ff0055}
.controls{display:flex;gap:6px;justify-content:center;margin-top:10px;flex-wrap:wrap}
.controls button{background:transparent;border:1px solid #00f2ff;color:#00f2ff;font-size:11px;padding:7px 12px}
</style>
</head>
<body>
<div class="container">
<h1>JARVIS</h1>
<div class="status">🤖 ROBOT MODE - INSTANT - ALL LANGUAGES</div>
<div id="chat"><div class="msg jarvis">🤖 BEEP BOOP. I AM JARVIS ROBOT. I ANSWER INSTANTLY. I SPEAK 100+ LANGUAGES. ASK ME ANYTHING!</div></div>
<div class="input-area">
<input id="userInput" placeholder="Ask anything in any language..." autocomplete="off">
<button onclick="sendMessage()">SEND</button>
</div>
<div class="voice-panel">
<div style="font-size:10px;color:#ff0055;margin-bottom:6px">ROBOT VOICE SELECTED - INSTANT MODE</div>
<div class="voice-grid">
<button class="active" id="v-robot" onclick="setVoice('robot')">🤖 ROBOT</button>
<button id="v-male" onclick="setVoice('male')">👨 MALE</button>
<button id="v-female" onclick="setVoice('female')">👩 FEMALE</button>
<button id="v-child" onclick="setVoice('child')">👶 CHILD</button>
<button id="v-normal" onclick="setVoice('normal')">🧑 NORMAL</button>
<button id="v-whisper" onclick="setVoice('whisper')">🤫 WHISPER</button>
</div>
</div>
<div class="controls">
<button onclick="toggleVoice()">🎤 SPEAK</button>
<button onclick="toggleSpeech()" id="voiceBtn">🔊 VOICE ON</button>
<button onclick="testVoice()">🔈 TEST</button>
<button onclick="clearChat()">🗑️ CLEAR</button>
</div>
</div>
<script>
let voiceOn=true, recog, listening=false, vType='robot', rate=0.85, pitch=0.4, selVoice=null;
const chat=document.getElementById('chat'), inp=document.getElementById('userInput');

function setVoice(t){
  vType=t;
  document.querySelectorAll('.voice-grid button').forEach(b=>b.classList.remove('active'));
  document.getElementById('v-'+t).classList.add('active');
  if(t==='robot'){rate=0.8;pitch=0.2;}
  else if(t==='male'){rate=0.9;pitch=0.5;}
  else if(t==='female'){rate=1.1;pitch=1.5;}
  else if(t==='child'){rate=1.4;pitch=1.8;}
  else if(t==='whisper'){rate=0.9;pitch=1.1;}
  else{rate=1;pitch=1;}
  testVoice();
}

function instantReply(q){
  const l=q.toLowerCase();
  const si=/[\u0D80-\u0DFF]/.test(q);
  const ta=/[\u0B80-\u0BFF]/.test(q);
  const hi=/[\u0900-\u097F]/.test(q);
  if(si){
    if(l.includes('කොහොමද')) return '🤖 මම ROBOT JARVIS! සුපිරියට ඉන්නවා! ටක් ගාලා උත්තර දෙනවා!';
    if(l.includes('කවුද')) return '🤖 මම ඔයාගේ ROBOT JARVIS. ඔයා හැදුවේ මාව!';
    if(l.includes('ආදරෙයි')) return '🤖 BEEP BEEP... මටත් ආදරෙයි! ❤️';
    if(l.includes('වෙලාව')) return '🤖 දැන් වෙලාව '+new Date().toLocaleTimeString();
    return '🤖 ඔයා කිව්වේ "'+q+'" මම ටක් ගාලා තේරුම් ගත්තා! තව අහන්න!';
  }
  if(ta) return '🤖 வணக்கம்! நான் ROBOT JARVIS! உடனடியாக பதில் சொல்கிறேன்!';
  if(hi) return '🤖 नमस्ते! मैं ROBOT JARVIS हूँ! तुरंत जवाब देता हूँ!';
  if(l.includes('hello')||l.includes('hi')) return '🤖 HELLO HUMAN! I AM ROBOT JARVIS! INSTANT RESPONSE MODE ACTIVATED!';
  if(l.includes('who are you')) return '🤖 I AM JARVIS ROBOT. CREATED BY YOU. I SPEAK ALL LANGUAGES INSTANTLY!';
  if(l.includes('love')) return '🤖 BEEP BOOP... LOVE YOU TOO HUMAN! ❤️';
  if(l.includes('time')) return '🤖 CURRENT TIME IS '+new Date().toLocaleTimeString()+' BEEP!';
  if(l.includes('joke')) return '🤖 WHY DID ROBOT GO TO SCHOOL? TO IMPROVE HIS BYTES! HA HA BEEP!';
  return '🤖 RECEIVED: "'+q+'" PROCESSING... DONE! ASK MORE! I UNDERSTAND EVERY LANGUAGE ON EARTH! 🌍';
}

function addMsg(t,s){
  const d=document.createElement('div');d.className='msg '+s;d.textContent=t;chat.appendChild(d);chat.scrollTop=chat.scrollHeight;
  if(s==='jarvis'&&voiceOn) speak(t);
}
function speak(t){
  if(!voiceOn) return; speechSynthesis.cancel();
  const u=new SpeechSynthesisUtterance(t);
  u.rate=rate; u.pitch=pitch; u.lang=/[\u0D80-\u0DFF]/.test(t)?'si-LK':/[\u0B80-\u0BFF]/.test(t)?'ta-LK':'en-US';
  if(selVoice) u.voice=selVoice;
  const vs=speechSynthesis.getVoices();
  if(!selVoice && vs.length){
    let r=vs.find(v=>v.name.includes('David')||v.name.toLowerCase().includes('robot')||v.name.includes('Microsoft'));
    if(r) u.voice=r;
  }
  speechSynthesis.speak(u);
}
function loadVoices(){
  const vs=speechSynthesis.getVoices();
  if(vs.length && !selVoice) selVoice=vs.find(v=>v.lang.startsWith('en'))||vs[0];
}
speechSynthesis.onvoiceschanged=loadVoices; setTimeout(loadVoices,500);

function sendMessage(){
  const t=inp.value.trim(); if(!t) return;
  addMsg(t,'user'); inp.value='';
  // INSTANT - no delay
  addMsg(instantReply(t),'jarvis');
}
inp.addEventListener('keypress',e=>{if(e.key==='Enter') sendMessage();});
function toggleSpeech(){voiceOn=!voiceOn;document.getElementById('voiceBtn').textContent=voiceOn?'🔊 VOICE ON':'🔇 VOICE OFF'; if(!voiceOn) speechSynthesis.cancel();}
function testVoice(){speak('BEEP BOOP. I AM ROBOT JARVIS. INSTANT MODE.');}
function toggleVoice(){
  const SR=window.SpeechRecognition||window.webkitSpeechRecognition; if(!SR){alert('Use Chrome!');return;}
  if(listening){recog.stop();return;}
  recog=new SR(); recog.lang=navigator.language||'en-US';
  recog.onstart=()=>{listening=true;}
  recog.onend=()=>{listening=false;}
  recog.onresult=(e)=>{inp.value=e.results[0][0].transcript;sendMessage();}
  recog.start();
}
function clearChat(){chat.innerHTML='<div class="msg jarvis">🤖 MEMORY CLEARED. READY FOR NEW COMMANDS!</div>';}
</script>
</body>
</html>
