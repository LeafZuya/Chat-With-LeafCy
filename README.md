<html lang="id">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>LeafCy Chat — LeafZuya</title>
<style>
  :root{
    --green1:#00c16b;
    --green2:#00994d;
    --blue1:#27a2ff;
    --bg-grad-a: #00e69a;
    --bg-grad-b: #39a7ff;
    --card: rgba(255,255,255,0.92);
    --accent: linear-gradient(135deg,var(--green1),var(--blue1));
  }
  *{box-sizing:border-box}
  html,body{height:100%; margin:0; font-family: "Poppins", "Segoe UI", Arial, sans-serif; background: linear-gradient(135deg,var(--bg-grad-a),var(--bg-grad-b));}
  .wrap{
    min-height:100vh;
    display:flex;
    align-items:center;
    justify-content:center;
    padding:28px;
  }

  .panel{
    width:960px;
    max-width:96%;
    background: linear-gradient(180deg, rgba(255,255,255,0.12), rgba(255,255,255,0.06));
    border-radius:18px;
    box-shadow: 0 18px 60px rgba(0,0,0,0.25);
    padding:18px;
    display:grid;
    grid-template-columns: 360px 1fr;
    gap:18px;
    align-items:start;
    position:relative;
    overflow:visible;
  }

  .left {
    background: var(--card);
    border-radius:14px;
    padding:14px;
    text-align:center;
    position:relative;
    min-height:440px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.12);
  }

  .avatar-wrap{
    width:260px; height:260px; margin:12px auto 8px;
    border-radius:14px; overflow:hidden; display:flex; align-items:center; justify-content:center;
    background: linear-gradient(180deg,#ffffff,#f0fbff);
    box-shadow: 0 10px 20px rgba(0,0,0,0.08);
    position:relative;
  }
  .avatar-wrap img{ width:100%; height:100%; object-fit:cover; display:block; }

  .name {
    font-weight:800; color:#0a3; font-size:20px; margin-top:8px;
  }
  .subtitle { color:#467; font-size:13px; margin-top:4px; opacity:0.9; }

  .bubble {
    position:absolute;
    top:18px;
    right:-12px;
    width:280px;
    max-width:42%;
    background: linear-gradient(180deg,#fff,#f5fff9);
    border-radius:12px;
    padding:12px 14px;
    box-shadow: 0 8px 22px rgba(0,0,0,0.12);
    font-size:15px;
    color:#0a3;
    z-index:20;
    transition: transform .18s ease;
  }
  .bubble.small { width:220px; font-size:14px; }
  .bubble:after{
    content:"";
    position:absolute;
    left: -10px; top:16px;
    border: 8px solid transparent;
    border-right-color: #fff;
    filter: drop-shadow(0 2px 2px rgba(0,0,0,0.06));
  }

  .right {
    background: var(--card);
    border-radius:14px;
    padding:14px;
    min-height:440px;
    box-shadow: inset 0 2px 12px rgba(0,0,0,0.03);
  }

  .title {
    font-size:18px; font-weight:800; color: #065; display:flex; align-items:center; gap:10px;
  }
  .controls { margin-top:12px; display:flex; gap:8px; flex-wrap:wrap; align-items:center; }

  .btn {
    background: white; border:1px solid rgba(0,0,0,0.06);
    padding:10px 14px; border-radius:12px; cursor:pointer; font-weight:700;
    box-shadow: 0 6px 14px rgba(0,0,0,0.06);
  }
  .btn.primary {
    background: var(--accent); color:white; border:none;
    box-shadow: 0 10px 20px rgba(0,0,0,0.18); transform: translateY(0);
  }
  .btn:active { transform: translateY(1px) }

  .preset-list { margin-top:14px; display:flex; gap:8px; flex-wrap:wrap; }
  .preset {
    background: linear-gradient(180deg,#fff,#f4fbff);
    border-radius:10px; padding:8px 10px; cursor:pointer; border:1px solid rgba(0,0,0,0.05);
    font-weight:700; box-shadow: 0 6px 12px rgba(0,0,0,0.06);
  }

  .chat {
    margin-top:14px; max-height: 230px; overflow:auto; padding-right:6px;
    display:flex; flex-direction:column; gap:10px;
  }
  .msg {
    max-width:70%; padding:10px 12px; border-radius:12px; font-size:15px;
    box-shadow: 0 8px 18px rgba(0,0,0,0.06);
  }
  .msg.user { align-self:flex-end; background: linear-gradient(180deg,#e9f7ff,#e0f0ff); color:#024; border:1px solid rgba(0,0,0,0.04); }
  .msg.leafcy { align-self:flex-start; background: linear-gradient(180deg,#fffefc,#f7fff6); color:#063; border:1px solid rgba(0,0,0,0.04); }

  .input-row { display:flex; gap:8px; margin-top:12px; align-items:center; }
  .input-row input[type="text"]{ flex:1; padding:10px;border-radius:10px;border:1px solid #ddd; font-size:15px; }
  .small-muted { font-size:12px; color:#577; margin-top:8px; }
  .foot { margin-top:12px; font-size:12px; color:#064; opacity:0.9; text-align:center; }

  @media(max-width:900px){
    .panel { grid-template-columns: 1fr; }
    .bubble { position:relative; right:auto; left:auto; margin:6px auto 0; }
  }
</style>
</head>
<body>
  <div class="wrap">
    <div class="panel" role="application" aria-labelledby="leafcyTitle">
      <div class="left">
        <div class="bubble" id="speechBubble">Klik tombol di kanan untuk mulai ngobrol dengan LeafCy!</div>

        <div class="avatar-wrap">
          <img id="avatarImg" src="leafcy.gif" alt="LeafCy avatar (GIF)">
        </div>

        <div class="name">LeafCy</div>
        <div class="subtitle">Virtual friend — Have Fun!</div>

        <div style="margin-top:14px; display:flex; gap:8px; justify-content:center;">
          <button class="btn primary" id="btnWave">Say Hello</button>
          <button class="btn" id="btnCalm">Calm Voice</button>
        </div>

        <div style="margin-top:12px; display:flex; gap:8px; justify-content:center;">
          <button class="btn" id="btnDance">Dance</button>
          <button class="btn" id="btnSleep">Good Night</button>
        </div>

        <div class="small-muted">You can replace <b>leafcy.gif</b> with your own GIF file in the same repo.</div>
      </div>

      <div class="right">
        <div class="title" id="leafcyTitle">Interaksi Ringan — LeafCy</div>

        <div class="controls">
          <button class="btn primary" id="btnStart">Start</button>
          <button class="btn" id="btnClear">Clear Chat</button>
          <button class="btn" id="btnAdd">Add Custom Reply</button>
        </div>

        <div class="preset-list" id="presetList"></div>

        <div class="chat" id="chatArea"></div>

        <div class="input-row">
          <input id="textIn" type="text" placeholder="Ketik pesan (atau tekan salah satu tombol preset)..." />
          <button class="btn primary" id="btnSend">Send</button>
        </div>

        <div class="small-muted">Tip: tombol preset memberikan jawaban cepat; kamu juga bisa menambah jawaban sendiri.</div>
        <div class="foot">Made with 💚 — LeafZuya</div>
      </div>
    </div>
  </div>

<script>
const speechBubble = document.getElementById("speechBubble");
const chatArea = document.getElementById("chatArea");
const presetList = document.getElementById("presetList");
const textIn = document.getElementById("textIn");
const avatarImg = document.getElementById("avatarImg");

const RESPONSES = {
  "Halo": ["Halo juga! Aku LeafCy 😎, gimana kabarnya?", "Hai! Senang ketemu kamu lagi!"],
  "Siapa kamu?": ["Aku LeafCy — asisten dan teman virtualmu! 🍃", "Namaku LeafCy, si pembuat suasana fun dan hijau~"],
  "Cerita lucu": ["Kemarin aku ngoding sambil minum jus daun... kode-nya malah hijau semua 😆", "Kenapa programmer suka daun? Karena suka yang *refresh*! 😂"],
  "Apa hobimu?": ["Ngoding, mendesain hal hijau, dan main game seru! 💻🎮", "Mendengarkan musik sambil ngedit website kamu 🍀"],
  "Dance": ["*LeafCy bergoyang cool* 💃", "Wuu~ let's dance in green rhythm! 🎵"],
  "Good Night": ["Selamat tidur, semoga mimpi daun hijau ya~ 🌙🍃", "Istirahat yang tenang, besok kita lanjut seru-seruan!"],
  "Praise": ["Kamu keren banget! 💚", "Wah, aura semangatmu nular banget! Keep it up!"]
};

function buildPresetButtons(){
  presetList.innerHTML = "";
  Object.keys(RESPONSES).forEach(key=>{
    const b = document.createElement("button");
    b.className = "preset";
    b.textContent = key;
    b.onclick = ()=> handleUserMessage(key);
    presetList.appendChild(b);
  });
}
buildPresetButtons();

function appendMessage(who, text){
  const d = document.createElement("div");
  d.className = "msg " + (who==="user" ? "user" : "leafcy");
  d.textContent = text;
  chatArea.appendChild(d);
  chatArea.scrollTop = chatArea.scrollHeight;
}

function chooseReply(arr){
  if (!arr) return "Hmm...";
  return arr[Math.floor(Math.random()*arr.length)];
}

function leafcyReply(replyText){
  speechBubble.style.transform = "scale(0.98)";
  setTimeout(()=> speechBubble.style.transform = "scale(1)", 140);
  const prev = speechBubble.textContent;
  speechBubble.textContent = "Menulis...";
  setTimeout(()=>{
    speechBubble.textContent = replyText;
    appendMessage("leafcy", replyText);
  }, 550 + Math.random()*600);
}

function handleUserMessage(text){
  if (!text) return;
  appendMessage("user", text);
  const key = Object.keys(RESPONSES).find(k => k.toLowerCase() === text.toLowerCase());
  if (key){
    leafcyReply(chooseReply(RESPONSES[key]));
    return;
  }

  const ltext = text.toLowerCase();
  if (/(hai|halo|hallo|hi|hey|yo)\b/.test(ltext)){
    leafcyReply(chooseReply(RESPONSES["Halo"]));
    return;
  }
  if (/(siapa|namamu|kamu siapa)/i.test(ltext)){
    leafcyReply(chooseReply(RESPONSES["Siapa kamu?"]));
    return;
  }
  if (/hob|hobi|game|main/i.test(ltext)){
    leafcyReply(chooseReply(RESPONSES["Apa hobimu?"]));
    return;
  }
  if (/cerit|lucu|joke|humor/i.test(ltext)){
    leafcyReply(chooseReply(RESPONSES["Cerita lucu"]));
    return;
  }

  const fallback = [
    "Menarik banget! Bisa dijelasin lagi? 🤔",
    "Hmm... Aku masih belajar soal itu 🍀",
    "Itu hal baru buatku, tapi seru juga ya!"
  ];
  leafcyReply(chooseReply(fallback));
}

document.getElementById("btnWave").addEventListener("click", ()=> handleUserMessage("Halo"));
document.getElementById("btnCalm").addEventListener("click", ()=> handleUserMessage("Apa hobimu?"));
document.getElementById("btnDance").addEventListener("click", ()=> handleUserMessage("Dance"));
document.getElementById("btnSleep").addEventListener("click", ()=> handleUserMessage("Good Night"));

document.getElementById("btnStart").addEventListener("click", ()=>{
  speechBubble.textContent = "Hai! Aku LeafCy — siap ngobrol santai hari ini? 🌿";
  appendMessage("leafcy", speechBubble.textContent);
});
document.getElementById("btnClear").addEventListener("click", ()=>{
  chatArea.innerHTML = "";
  speechBubble.textContent = "Obrolan dibersihkan. Klik Start untuk mulai lagi!";
});
document.getElementById("btnAdd").addEventListener("click", ()=>{
  const phrase = prompt("Masukkan kalimat/preset yang ingin ditambah (contoh: 'Kabar'):");
  if (!phrase) return;
  const reply = prompt("Masukkan balasan LeafCy untuk preset itu:");
  if (!reply) return;
  RESPONSES[phrase] = [reply];
  buildPresetButtons();
  alert("Preset baru berhasil ditambahkan!");
});

document.getElementById("btnSend").addEventListener("click", ()=>{
  const v = textIn.value.trim();
  if (!v) return;
  textIn.value = "";
  handleUserMessage(v);
});
textIn.addEventListener("keydown", (e)=>{
  if (e.key === "Enter"){
    e.preventDefault();
    document.getElementById("btnSend").click();
  }
});

avatarImg.addEventListener("click", ()=>{
  speechBubble.textContent = "Hehe, jangan pencet terus dong~ 😆";
  appendMessage("leafcy","Hehe, jangan pencet terus dong~ 😆");
});

setTimeout(()=> {
  speechBubble.textContent = "Halo! Klik 'Start' atau ketik sesuatu untuk mulai ngobrol denganku 🌿";
}, 350);

textIn.focus();
</script>
</body>
</html>
