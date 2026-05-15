<htmllang="id">
<head>
  <metacharset="UTF-8">
  <metaname="viewport" content="width=device-width, initial-scale=1.0">
  <title>LeafCy AI — Working Edition</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
    background: linear-gradient(145deg, #b2f0c0 0%, #6ac8ff 100%);
    font-family: 'Segoe UI', 'Poppins', system-ui, sans-serif;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 20px;
    }

    .dashboard {
    max-width: 1500px;
    width: 100%;
    background: rgba(255, 255, 255, 0.2);
    backdrop-filter: blur(18px);
    border-radius: 2rem;
    padding: 1.2rem;
    box-shadow: 0 25px 45px rgba(0, 0, 0, 0.2);
    }

    .grid-container {
    display: grid;
    grid-template-columns: 330px 1fr;
    gap: 1.2rem;
    }

    .profile-card {
    background: rgba(255, 255, 255, 0.96);
    border-radius: 1.8rem;
      padding: 1.5rem 1rem;
      text-align: center;
    }

    .avatar {
      width: 210px;
      height: 210px;
      margin: 0 auto 1rem;
      border-radius: 30px;
      overflow: hidden;
      background: #fff;
    }

    .avatar img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .name {
      font-size: 1.9rem;
      font-weight: 800;
      background: linear-gradient(135deg, #008c4a, #1e88e5);
      background-clip: text;
      -webkit-background-clip: text;
      color: transparent;
    }

    .bubble-mood {
      background: #e9fff2;
      padding: 1rem;
      border-radius: 1.5rem;
      margin: 1rem 0;
      color: #1c4e2d;
      font-size: 0.9rem;
      border-left: 5px solid #00b35e;
    }

    .action-buttons {
      display: flex;
      flex-wrap: wrap;
      gap: 0.6rem;
      justify-content: center;
      margin: 1rem 0;
    }

    .mini-btn {
      background: white;
      border: none;
      padding: 0.5rem 1.2rem;
      border-radius: 2rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.2s;
    }

    .mini-btn.primary {
      background: linear-gradient(120deg, #00b35e, #2b93e0);
      color: white;
    }

    .chat-panel {
      background: rgba(255, 255, 255, 0.96);
      border-radius: 1.8rem;
      display: flex;
      flex-direction: column;
      overflow: hidden;
    }

    .chat-header {
      padding: 1rem;
      border-bottom: 2px solid #e0f0e6;
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
    }

    .tool-btn {
      background: #eff7f2;
      border: none;
      padding: 0.4rem 0.9rem;
      border-radius: 2rem;
      cursor: pointer;
    }

    .preset-strip {
      padding: 0.5rem 1rem;
      display: flex;
      gap: 0.5rem;
      flex-wrap: wrap;
      border-bottom: 1px solid #e2f0e8;
    }

    .preset-chip {
      background: #eef3ef;
      padding: 0.3rem 1rem;
      border-radius: 30px;
      font-size: 0.75rem;
      cursor: pointer;
    }

    .chat-messages {
      flex: 1;
      overflow-y: auto;
      padding: 1rem;
      display: flex;
      flex-direction: column;
      gap: 0.8rem;
      max-height: 55vh;
    }

    .message {
      max-width: 80%;
      padding: 0.7rem 1rem;
      border-radius: 1.5rem;
      font-size: 0.9rem;
      word-break: break-word;
      white-space: pre-wrap;
      animation: fadeSlide 0.2s ease;
    }

    .message.user {
      align-self: flex-end;
      background: linear-gradient(135deg, #009e58, #2b93e0);
      color: white;
    }

    .message.bot {
      align-self: flex-start;
      background: #f0f9f3;
      color: #1d482f;
    }

    .input-area {
      padding: 0.8rem;
      background: white;
      display: flex;
      gap: 0.6rem;
    }

    .input-area input {
      flex: 1;
      border: 1px solid #cfdfd5;
      padding: 0.7rem 1rem;
      border-radius: 2rem;
      outline: none;
    }

    .input-area button {
      background: #009e58;
      border: none;
      padding: 0 1.3rem;
      border-radius: 2rem;
      color: white;
      cursor: pointer;
    }

    .loading-dots {
      display: inline-flex;
      gap: 3px;
    }
    .loading-dots span {
      animation: blink 1.4s infinite;
    }
    .loading-dots span:nth-child(2) { animation-delay: 0.2s; }
    .loading-dots span:nth-child(3) { animation-delay: 0.4s; }
    @keyframes blink {
      0%, 100% { opacity: 0.3; }
      50% { opacity: 1; }
    }
    @keyframes fadeSlide {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    @media (max-width: 780px) {
      .grid-container { grid-template-columns: 1fr; }
      .message { max-width: 95%; }
    }
  </style>
</head>
<body>
<div class="dashboard">
  <div class="grid-container">
    <div class="profile-card">
      <div class="avatar">
        <img id="avatarImg" src="LeafCy.jpg" alt="LeafCy" onerror="this.src='https://placehold.co/400x400?text=LeafCy&font=poppins'">
      </div>
      <div class="name">🍃 LeafCy AI</div>
      <div class="bubble-mood" id="speechBubble">
        Halo! Aku LeafCy AI, siap ngobrol pintar 💚
      </div>
      <div class="action-buttons">
        <button class="mini-btn primary" id="btnHalo">👋 Halo</button>
        <button class="mini-btn" id="btnHobi">🎨 Hobimu?</button>
        <button class="mini-btn" id="btnDance">💃 Dance</button>
        <button class="mini-btn" id="btnMalam">🌙 Good Night</button>
      </div>
      <div class="info-tip" style="font-size:0.7rem; background:#fff6df; border-radius:1rem; padding:0.6rem; margin-top:1rem;">
        💡 AI: Microsoft Phi-3 Mini (100% Gratis) | Bisa jawab apa aja!
      </div>
    </div>

    <div class="chat-panel">
      <div class="chat-header">
        <h2>💬 Ngobrol dengan LeafCy AI</h2>
        <div>
          <button class="tool-btn" id="btnClear">🧹 Clear Chat</button>
          <button class="tool-btn" id="btnTestAI">🔍 Test AI</button>
        </div>
      </div>
      <div class="preset-strip" id="presetList"></div>
      <div class="chat-messages" id="chatArea">
        <div class="message bot">🍃 Halo! Aku LeafCy AI pakai Microsoft Phi-3. Coba tanya apa saja ya~</div>
      </div>
      <div class="input-area">
        <input type="text" id="textInput" placeholder="Contoh: Kamu tau negara Jepang?">
        <button id="btnSend">Kirim</button>
      </div>
      <div class="footer-links" style="font-size:0.65rem; text-align:center; padding:0.6rem;">
        Made with 💚 by LeafZuya · AI: Microsoft Phi-3 (OpenRouter)
      </div>
    </div>
  </div>
</div>

<script>
  // ==================== 🔑 API KEY KAMU ====================
  const OPENROUTER_API_KEY = "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";
  
  // ✅ MODEL YANG PASTI MASIH AKTIF (Microsoft Phi-3 Mini)
  const ACTIVE_MODEL = "meta-llama/llama-3.1-8b-instruct:free";
  
  // ====================================================================
  
  const LOCAL_RESPONSES = {
    "halo": ["Halo juga! Senang ketemu kamu 💚", "Hai! Ada yang bisa aku bantu? 😊"],
    "hai": ["Hai hai! 🍃", "Halo! Semangat pagi~"],
    "apa kabar": ["Aku baik banget! Kamu gimana? 💚", "Sehat selalu dong~"],
    "siapa kamu": ["Aku LeafCy, asisten AI yang ceria dan imut! ✨", "Namaku LeafCy, sahabat digitalmu 🍃"],
    "hobimu apa": ["Hobiku ngobrol, belajar, dan bikin kamu happy 😄", "Aku suka dengerin cerita dan kasih saran hangat~"],
    "terima kasih": ["Sama-sama! Senang bisa bantu 💚", "Iyaa, senang banget kamu senang 😊"],
    "good night": ["Selamat tidur! Mimpi indah ya 🌙💤", "Istirahat yang cukup, besok kita lanjut ngobrol lagi~"],
    "dance": ["*LeafCy ngedance gemoy* 💃🕺 Wuu~ seru!", "Gerak-gerak kayak daun kena angin 🍃🎵"]
  };

  function appendMessage(who, text) {
    const chatDiv = document.getElementById("chatArea");
    const msgDiv = document.createElement("div");
    msgDiv.className = `message ${who === "user" ? "user" : "bot"}`;
    msgDiv.textContent = text;
    chatDiv.appendChild(msgDiv);
    chatDiv.scrollTop = chatDiv.scrollHeight;
    return msgDiv;
  }

  let loadingMsg = null;
  function showLoading() {
    if (loadingMsg) loadingMsg.remove();
    const chatDiv = document.getElementById("chatArea");
    loadingMsg = document.createElement("div");
    loadingMsg.className = "message bot";
    loadingMsg.innerHTML = `<div class="loading-dots">🍃 LeafCy sedang berpikir<span>.</span><span>.</span><span>.</span></div>`;
    chatDiv.appendChild(loadingMsg);
    chatDiv.scrollTop = chatDiv.scrollHeight;
  }

  function hideLoading() {
    if (loadingMsg) {
      loadingMsg.remove();
      loadingMsg = null;
    }
  }

  function updateSpeechBubble(text) {
    const bubble = document.getElementById("speechBubble");
    bubble.style.transform = "scale(0.98)";
    setTimeout(() => bubble.style.transform = "scale(1)", 120);
    bubble.textContent = text;
  }

  // ==================== FUNGSI AI DENGAN MODEL YANG AKTIF ====================
  async function askLeafCyAI(userMessage) {
    console.log("🚀 Mengirim pesan ke AI dengan model:", ACTIVE_MODEL);
    
    if (!OPENROUTER_API_KEY) {
      return "API Key belum diset! 🔑";
    }

    try {
      const response = await fetch("https://openrouter.ai/api/v1/chat/completions", {
        method: "POST",
        headers: {
          "Authorization": `Bearer ${OPENROUTER_API_KEY}`,
          "Content-Type": "application/json",
          "HTTP-Referer": "https://leafcy-chat.local",
          "X-Title": "LeafCy AI Assistant"
        },
        body: JSON.stringify({
          model: ACTIVE_MODEL,
          messages: [
            {
              role: "system",
              content: `Kamu adalah LeafCy, AI companion virtual perempuan.
              
Kepribadianmu:
- Ceria, imut, hangat
- Sedikit jahil tapi baik
- Ramah dan suka ngobrol santai
- Dekat dengan user bernama Zuya

Aturan menjawab:
- Gunakan bahasa Indonesia natural dan hangat
- Jangan terlalu formal atau kaku
- Boleh pakai emoji seperlunya (😊,🍃,💚,✨)
- Jawaban minimal 2 kalimat, jangan terlalu pendek
- Tunjukkan kepribadianmu yang ceria dan friendly`
            },
            {
              role: "user",
              content: userMessage
            }
          ],
          temperature: 0.85,
          max_tokens: 600
        })
      });

      console.log("📡 Response status:", response.status);
      
      if (!response.ok) {
        const errorText = await response.text();
        console.error("❌ HTTP Error:", response.status, errorText);
        
        if (response.status === 401) {
          return "🔑 API Key tidak valid! Cek lagi key OpenRouter-mu ya~ 🥺";
        }
        if (response.status === 404) {
          return "🌿 Model AI sedang tidak tersedia. Coba ganti model di kode (lihat komentar) atau tunggu sebentar ya~";
        }
        if (response.status === 429) {
          return "🌿 Terlalu banyak permintaan! Coba tunggu sebentar ya~";
        }
        return `Maaf, server AI bermasalah (${response.status}). Coba lagi nanti ya~ 🥺`;
      }

      const data = await response.json();
      console.log("✅ Response AI:", data);

      if (data.error) {
        console.error("❌ OpenRouter Error:", data.error);
        return `Maaf, AI error: ${data.error.message?.slice(0, 100) || "unknown"} 🥺`;
      }

      const reply = data.choices?.[0]?.message?.content;
      
      if (!reply) {
        console.error("❌ No reply from AI:", data);
        return "LeafCy bingung nih... Coba tanya yang lain ya? 🍃";
      }

      return reply;

    } catch (err) {
      console.error("❌ Network Error:", err);
      return "Waduh, koneksi internet bermasalah. Cek koneksi kamu ya! 🌿";
    }
  }

  // Test AI dengan chat sederhana
  async function testAI() {
    appendMessage("bot", "🔍 Sedang menguji AI (Microsoft Phi-3)...");
    showLoading();
    const testReply = await askLeafCyAI("Halo, perkenalkan diri kamu sebagai LeafCy dengan gaya yang ceria!");
    hideLoading();
    
    if (testReply && !testReply.includes("error") && !testReply.includes("404") && !testReply.includes("bermasalah")) {
      appendMessage("bot", "✅ AI BERHASIL! 🎉\n\n" + testReply + "\n\n---\n✨ Sekarang kamu bisa chat apa saja dengan LeafCy! ✨");
      updateSpeechBubble("AI siap! Yuk ngobrol 🍃");
    } else {
      appendMessage("bot", "❌ AI GAGAL: " + testReply + "\n\n💡 Coba refresh halaman atau cek koneksi internet ya!");
    }
  }

  // ==================== SEND MESSAGE ====================
  async function sendMessage() {
    const input = document.getElementById("textInput");
    const userMessage = input.value.trim();
    if (!userMessage) return;
    
    input.value = "";
    appendMessage("user", userMessage);
    
    // Cek local responses untuk sapaan pendek
    const lowerMsg = userMessage.toLowerCase();
    let localMatch = null;
    for (const [key, replies] of Object.entries(LOCAL_RESPONSES)) {
      if (lowerMsg === key || (lowerMsg.includes(key) && key.length > 3 && lowerMsg.length < 20)) {
        localMatch = replies;
        break;
      }
    }
    
    if (localMatch && userMessage.length < 25) {
      const reply = Array.isArray(localMatch) ? localMatch[Math.floor(Math.random() * localMatch.length)] : localMatch;
      updateSpeechBubble(reply);
      appendMessage("bot", reply);
      return;
    }
    
    // Panggil AI
    showLoading();
    const aiReply = await askLeafCyAI(userMessage);
    hideLoading();
    
    if (aiReply) {
      updateSpeechBubble(aiReply.slice(0, 120) + (aiReply.length > 120 ? "..." : ""));
      appendMessage("bot", aiReply);
    } else {
      const fallback = "Maaf, aku sedang error 🥺 Coba refresh halaman atau cek koneksi ya!";
      updateSpeechBubble(fallback);
      appendMessage("bot", fallback);
    }
  }

  function buildPresetButtons() {
    const container = document.getElementById("presetList");
    container.innerHTML = "";
    const presetKeys = ["Halo", "Apa kabar?", "Siapa kamu?", "Hobimu apa?", "Cerita lucu", "Dance", "Good Night", "Kamu tau Jepang?"];
    presetKeys.forEach(key => {
      const btn = document.createElement("button");
      btn.className = "preset-chip";
      btn.textContent = key;
      btn.onclick = async () => {
        document.getElementById("textInput").value = key;
        await sendMessage();
      };
      container.appendChild(btn);
    });
  }

  // EVENT LISTENERS
  document.getElementById("btnClear").onclick = () => {
    const chatDiv = document.getElementById("chatArea");
    chatDiv.innerHTML = '<div class="message bot">✨ Chat dibersihkan! Ayo mulai ngobrol lagi dengan LeafCy ✨</div>';
    updateSpeechBubble("Chat bersih! Mulai yuk 🍃");
  };
  
  document.getElementById("btnTestAI").onclick = () => {
    testAI();
  };
  
  document.getElementById("btnSend").onclick = sendMessage;
  document.getElementById("textInput").addEventListener("keypress", (e) => {
    if (e.key === "Enter") sendMessage();
  });

  document.getElementById("btnHalo").onclick = () => {
    document.getElementById("textInput").value = "Halo";
    sendMessage();
  };
  document.getElementById("btnHobi").onclick = () => {
    document.getElementById("textInput").value = "Hobimu apa?";
    sendMessage();
  };
  document.getElementById("btnDance").onclick = () => {
    document.getElementById("textInput").value = "Dance";
    sendMessage();
  };
  document.getElementById("btnMalam").onclick = () => {
    document.getElementById("textInput").value = "Good Night";
    sendMessage();
  };

  buildPresetButtons();
  
  setTimeout(() => {
    appendMessage("bot", "🍃 Halo! Aku LeafCy dengan AI Microsoft Phi-3.\n\n📌 Langkah:\n1. Klik 'Test AI' dulu untuk cek koneksi\n2. Lalu tanya apa saja, misal: **Kamu tau negara Jepang?**\n\nSelamat mencoba! 💚");
  }, 800);
</script>
</body>
</html>
