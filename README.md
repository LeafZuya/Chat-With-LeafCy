<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>LeafCy AI [New Beta] - Hapus Pesan Tanpa Hilangkan Ingatan AI</title>
    <!-- Google Fonts + Font Awesome -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,500;14..32,600;14..32,700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(135deg, #e8f5e9 0%, #c8e6c9 100%);
            font-family: 'Inter', system-ui, -apple-system, sans-serif;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
        }

        .app {
            width: 100%;
            max-width: 900px;
            height: 100vh;
            background: #ffffff;
            display: flex;
            flex-direction: column;
            box-shadow: 0 0 30px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            position: relative;
        }

        .chat-header {
            padding: 16px 24px;
            background: #ffffff;
            border-bottom: 1px solid #2ecc71;
            display: flex;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 8px;
        }

        .logo-area {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .logo-icon {
            width: 36px;
            height: 36px;
            border-radius: 14px;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }
        
        .logo-icon img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .logo-text {
            font-weight: 700;
            font-size: 1.4rem;
            letter-spacing: -0.4px;
            background: linear-gradient(120deg, #2ecc71, #27ae60);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .model-badge {
            background: rgba(46, 204, 113, 0.12);
            border-radius: 40px;
            padding: 5px 12px;
            font-size: 0.7rem;
            font-weight: 500;
            color: #2ecc71;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .menu-history-btn {
            background: rgba(46, 204, 113, 0.12);
            border-radius: 40px;
            padding: 5px 12px;
            font-size: 0.7rem;
            font-weight: 500;
            color: #2ecc71;
            cursor: pointer;
            transition: all 0.2s ease;
            border: 1px solid rgba(46, 204, 113, 0.3);
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .menu-history-btn:hover {
            background: rgba(46, 204, 113, 0.25);
            transform: scale(1.02);
        }
        
        .sidebar {
            position: fixed;
            top: 0;
            left: -320px;
            width: 300px;
            height: 100%;
            background: #ffffff;
            box-shadow: 2px 0 20px rgba(0,0,0,0.1);
            z-index: 1001;
            transition: left 0.3s ease;
            display: flex;
            flex-direction: column;
            border-right: 2px solid #2ecc71;
        }
        .sidebar.open {
            left: 0;
        }
        .sidebar-header {
            padding: 20px;
            border-bottom: 1px solid #2ecc71;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .sidebar-header h3 {
            color: #2ecc71;
            font-size: 1.1rem;
        }
        .close-sidebar {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #e74c3c;
        }
        .history-list {
            flex: 1;
            overflow-y: auto;
            padding: 10px;
        }
        .history-item {
            padding: 12px 15px;
            margin: 5px 0;
            background: #f5f7f5;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.2s;
            border: 1px solid #e0e8e0;
        }
        .history-item:hover {
            background: #e8f5e9;
            transform: translateX(5px);
        }
        .history-item.active {
            background: #2ecc71;
            color: white;
            border-color: #2ecc71;
        }
        .history-item.active .history-preview {
            color: white;
        }
        .history-title {
            font-weight: 600;
            font-size: 0.85rem;
            margin-bottom: 5px;
        }
        .history-preview {
            font-size: 0.7rem;
            color: #8a9a8a;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }
        .history-time {
            font-size: 0.6rem;
            color: #aaa;
            margin-top: 5px;
        }
        .history-item.active .history-time {
            color: rgba(255,255,255,0.7);
        }
        .new-chat-btn {
            margin: 15px;
            padding: 10px;
            background: linear-gradient(135deg, #2ecc71, #27ae60);
            color: white;
            border: none;
            border-radius: 40px;
            cursor: pointer;
            font-weight: bold;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            display: none;
        }
        .overlay.show {
            display: block;
        }

        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: 24px 20px 20px 20px;
            display: flex;
            flex-direction: column;
            gap: 20px;
            scroll-behavior: smooth;
        }

        .chat-messages::-webkit-scrollbar {
            width: 5px;
        }
        .chat-messages::-webkit-scrollbar-track {
            background: transparent;
        }
        .chat-messages::-webkit-scrollbar-thumb {
            background: #2ecc71;
            border-radius: 10px;
        }

        .message {
            display: flex;
            align-items: flex-start;
            gap: 12px;
            max-width: 85%;
            animation: fadeSlideUp 0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1);
            position: relative;
        }

        @keyframes fadeSlideUp {
            from {
                opacity: 0;
                transform: translateY(16px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .message.user {
            align-self: flex-end;
            flex-direction: row-reverse;
        }

        .avatar {
            width: 34px;
            height: 34px;
            border-radius: 100%;
            background: #e8f5e9;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 15px;
            flex-shrink: 0;
        }

        .user .avatar {
            background: #2ecc71;
            color: white;
        }

        .bubble {
            background: #f5f5f5;
            padding: 12px 18px;
            border-radius: 24px;
            font-size: 0.95rem;
            line-height: 1.5;
            color: #1a1a1a;
            word-wrap: break-word;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
            position: relative;
        }

        .user .bubble {
            background: #2ecc71;
            color: white;
            border-bottom-right-radius: 6px;
        }

        .assistant .bubble {
            background: #f0f4f0;
            border-bottom-left-radius: 6px;
            border: 1px solid #e0e8e0;
        }

        .delete-message-btn {
            position: absolute;
            top: -8px;
            right: -10px;
            background: white;
            border-radius: 30px;
            width: 26px;
            height: 26px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #e74c3c;
            font-size: 12px;
            cursor: pointer;
            box-shadow: 0 2px 6px rgba(0,0,0,0.15);
            transition: 0.2s;
            border: 1px solid #ffe0e0;
            opacity: 0;
            pointer-events: none;
            z-index: 12;
        }
        .message:hover .delete-message-btn {
            opacity: 1;
            pointer-events: auto;
        }
        .delete-message-btn:hover {
            background: #e74c3c;
            color: white;
            transform: scale(1.05);
        }

        .message-image {
            max-width: 200px;
            max-height: 200px;
            border-radius: 12px;
            margin-top: 8px;
            cursor: pointer;
        }
        .image-preview-bubble {
            background: #f0f4f0;
            border-radius: 16px;
            padding: 8px;
            display: inline-block;
        }

        .timestamp {
            font-size: 0.65rem;
            color: #8a9a8a;
            margin-top: 5px;
            margin-left: 44px;
        }
        .user .timestamp {
            text-align: right;
            margin-right: 6px;
        }

        .input-container {
            background: #ffffff;
            border-top: 1px solid #2ecc71;
            padding: 16px 20px 24px;
        }

        .input-wrapper {
            display: flex;
            align-items: flex-end;
            gap: 12px;
            background: #f5f7f5;
            border-radius: 48px;
            padding: 6px 6px 6px 22px;
            border: 1px solid #2ecc71;
            transition: all 0.2s;
        }

        .input-wrapper:focus-within {
            border-color: #27ae60;
            box-shadow: 0 0 0 2px rgba(46, 204, 113, 0.25);
        }

        textarea {
            flex: 1;
            background: transparent;
            border: none;
            padding: 10px 0;
            font-family: 'Inter', monospace;
            font-size: 0.95rem;
            color: #1a1a1a;
            resize: none;
            outline: none;
            max-height: 130px;
        }

        textarea::placeholder {
            color: #9aae9a;
        }

        .upload-btn {
            background: rgba(46, 204, 113, 0.15);
            border: none;
            width: 44px;
            height: 44px;
            border-radius: 100px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #2ecc71;
            font-size: 20px;
            cursor: pointer;
            transition: 0.2s;
        }
        .upload-btn:hover {
            background: rgba(46, 204, 113, 0.3);
            transform: scale(1.02);
        }
        
        #fileInput {
            display: none;
        }

        .send-btn {
            background: linear-gradient(135deg, #2ecc71, #27ae60);
            border: none;
            width: 44px;
            height: 44px;
            border-radius: 100px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 18px;
            cursor: pointer;
            transition: 0.2s;
        }

        .send-btn:hover {
            transform: scale(1.02);
            opacity: 0.9;
        }

        .bottom-info-text {
            font-size: 11px;
            color: #5a8a5a;
        }
        .header-buttons {
            display: flex;
            gap: 12px;
            align-items: center;
            flex-wrap: wrap;
        }
        .rate-limit-badge {
            background: rgba(231, 76, 60, 0.12);
            border-radius: 40px;
            padding: 4px 10px;
            font-size: 0.65rem;
            font-weight: 500;
            color: #e74c3c;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        @media (max-width: 600px) {
            .message { max-width: 92%; }
            .sidebar { width: 280px; }
        }

        .message-fade-out {
            animation: fadeOut 0.2s ease forwards;
        }
        @keyframes fadeOut {
            to { opacity: 0; transform: scale(0.95); display: none; }
        }
        .typing-indicator span {
            display: inline-block;
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: #2ecc71;
            margin: 0 2px;
            animation: typing 1.4s infinite;
        }
        .typing-indicator span:nth-child(2) { animation-delay: 0.2s; }
        .typing-indicator span:nth-child(3) { animation-delay: 0.4s; }
        @keyframes typing {
            0%, 60%, 100% { transform: translateY(0); opacity: 0.4; }
            30% { transform: translateY(-6px); opacity: 1; }
        }

        /* CSS untuk POPUP akselerasi - ditambahkan tanpa merusak style awal */
        .popup-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.6);
            z-index: 2000;
            display: flex;
            align-items: center;
            justify-content: center;
            visibility: hidden;
            opacity: 0;
            transition: 0.2s;
        }
        .popup-overlay.show {
            visibility: visible;
            opacity: 1;
        }
        .popup-card {
            background: white;
            max-width: 400px;
            width: 85%;
            border-radius: 32px;
            padding: 24px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
            text-align: center;
        }
        .popup-card h3 {
            color: #f1c40f;
            margin-bottom: 12px;
        }
        .popup-input-group {
            display: flex;
            gap: 8px;
            margin: 15px 0;
        }
        .popup-input {
            flex: 1;
            padding: 12px;
            border: 2px solid #f1c40f;
            border-radius: 60px;
            font-family: monospace;
            font-size: 0.9rem;
            outline: none;
            text-align: center;
        }
        .popup-plus-btn {
            background: #f1c40f;
            border: none;
            width: 48px;
            border-radius: 60px;
            font-size: 1.5rem;
            font-weight: bold;
            color: #2c3e50;
            cursor: pointer;
            transition: 0.2s;
        }
        .popup-plus-btn:hover {
            background: #f39c12;
            transform: scale(1.02);
        }
        .popup-progress {
            background: #f0f0f0;
            border-radius: 20px;
            height: 10px;
            margin: 10px 0;
            overflow: hidden;
        }
        .popup-progress-bar {
            width: 0%;
            height: 100%;
            background: linear-gradient(90deg, #f1c40f, #e67e22);
        }
        .popup-buttons {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-top: 15px;
            flex-wrap: wrap;
        }
        .btn-redeem {
            background: #f39c12;
            border: none;
            padding: 10px 18px;
            border-radius: 40px;
            font-weight: bold;
            color: white;
            cursor: pointer;
        }
        .btn-redeem:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
        .btn-cancel {
            background: #ecf0f1;
            border: none;
            padding: 10px 18px;
            border-radius: 40px;
            font-weight: bold;
            color: #2c3e50;
            cursor: pointer;
        }
        .yellow-boost-btn {
            background: #f1c40f;
            border-radius: 40px;
            padding: 5px 12px;
            font-size: 0.75rem;
            font-weight: 600;
            color: #2c3e50;
            cursor: pointer;
            transition: all 0.2s ease;
            border: none;
            display: flex;
            align-items: center;
            gap: 6px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
        }
        .yellow-boost-btn:hover {
            background: #f39c12;
            transform: scale(1.02);
        }
    </style>
</head>
<body>
<div class="app">
    <div class="chat-header">
        <div class="logo-area">
            <div class="logo-icon">
                <img src="leafcy.png" alt="Logo" onerror="this.src='https://via.placeholder.com/36x36/2ecc71/ffffff?text=Leaf'">
            </div>
            <div class="logo-text">LeafCy AI</div>
            <div class="model-badge" id="modelBadge"><i class="fas fa-charging-station"></i> Zyrion (Leaf-Ice)</div>
        </div>
        <div class="header-buttons">
            <div id="menuHistoryBtn" class="menu-history-btn"><i class="fas fa-history"></i> Riwayat</div>
            <div class="model-badge" style="background: #2ecc71; color: white;"><i class="fas fa-robot"></i> AI Siap</div>
            <button id="yellowBoostBtn" class="yellow-boost-btn"><i class="fas fa-bolt"></i> ⚡ Akselerasi ⚡</button>
        </div>
    </div>
    <div style="display: flex; justify-content: space-between; padding: 0 20px 8px 20px; gap: 8px; flex-wrap: wrap;">
        <div class="rate-limit-badge" id="textLimitBadge"><i class="fas fa-comment-dots"></i> Teks: 0/20 jam ini</div>
        <div class="rate-limit-badge" id="imageLimitBadge"><i class="fas fa-image"></i> Gambar: 0/2 jam ini</div>
        <div class="rate-limit-badge" id="resetTimerBadge"><i class="fas fa-hourglass-half"></i> Reset: --:--</div>
    </div>

    <div class="chat-messages" id="chatMessages">
        <div class="welcome-message" id="welcomeMsg">
            <i class="fas fa-seedling" style="font-size: 32px; margin-bottom: 10px; display: block; opacity: 0.7; color: #2ecc71;"></i>
            LeafCy with Zyrion (Leaf-Ice)<br>🎯 1 Juta Token Konteks | Bisa Baca Gambar! 📷
        </div>
    </div>

    <div class="input-container">
        <div class="input-wrapper">
            <textarea id="chatInput" rows="1" placeholder="Tanya apa saja... AI akan merespon dengan logika Sendiri" aria-label="Chat"></textarea>
            <input type="file" id="fileInput" accept="image/*">
            <button class="upload-btn" id="uploadBtn"><i class="fas fa-image"></i></button>
            <button class="send-btn" id="sendBtn"><i class="fas fa-paper-plane"></i></button>
        </div>
        <div style="display: flex; justify-content: space-between; margin-top: 8px; padding: 0 10px;">
            <div class="bottom-info-text"><i class="fas fa-microchip"></i> model: Zyrion (Leaf-Ice) (1M token)</div>
            <div class="bottom-info-text"><i class="fas fa-database"></i> Hapus pesan (hover) ✔️ AI tetap ingat konteks</div>
        </div>
    </div>
</div>

<!-- POPUP AKSELERASI -->
<div id="popupOverlay" class="popup-overlay">
    <div class="popup-card">
        <h3><i class="fas fa-gem"></i> Akselerasi "Zuya Ganteng 😎"</h3>
        <p style="font-size:13px;">Ketik kata ajaib & tekan <strong>+</strong> untuk mengumpulkan poin!</p>
        <div class="popup-input-group">
            <input type="text" id="popupKeywordInput" class="popup-input" placeholder="Zuya Ganteng 😎" autocomplete="off">
            <button id="popupPlusBtn" class="popup-plus-btn"><i class="fas fa-plus"></i></button>
        </div>
        <div class="popup-progress">
            <div class="popup-progress-bar" id="popupProgressBar"></div>
        </div>
        <div><span id="popupCounter">0</span>/<span id="popupTarget">1000</span></div>
        <div class="popup-buttons">
            <button id="popupRedeemBtn" class="btn-redeem" disabled><i class="fas fa-clock"></i> Kurangi 30 Menit</button>
            <button id="popupCancelBtn" class="btn-cancel"><i class="fas fa-skull"></i> Aku tidak Mampu Mengetiknya, Nanti Lanjutkan 🗿</button>
        </div>
    </div>
</div>

<div class="overlay" id="overlay"></div>
<div class="sidebar" id="sidebar">
    <div class="sidebar-header">
        <h3><i class="fas fa-history"></i> Riwayat Chat</h3>
        <button class="close-sidebar" id="closeSidebar"><i class="fas fa-times"></i></button>
    </div>
    <div class="history-list" id="historyList"></div>
    <button class="new-chat-btn" id="newChatBtn"><i class="fas fa-plus-circle"></i> Chat Baru</button>
</div>

<script>
    // KONSTAN PROXY
    const PROXY_URL = "https://leafcyai.kingglafeon.workers.dev/";
    const CHAT_MODEL = "google/gemini-2.0-flash-001";
    const IMAGE_MODEL = "google/gemini-2.5-flash-image";
    let currentModel = CHAT_MODEL;
    
    // RATE LIMIT CONFIG
    const MAX_TEXTS_PER_HOUR = 20;  // DIUBAH DARI 35 MENJADI 20
    const MAX_IMAGES_PER_HOUR = 2;
    
    // Struktur data rate limit
    let rateLimit = {
        textCount: 0,
        imageCount: 0,
        resetTime: null
    };
    
    // SPEED UP PROGRESS (khusus akselerasi)
    let speedUpProgress = {
        count: 0,
        target: 1000
    };
    
    // Struktur data utama
    let chats = [];
    let currentChatId = null;
    
    // DOM
    const messagesContainer = document.getElementById('chatMessages');
    const chatInput = document.getElementById('chatInput');
    const sendBtn = document.getElementById('sendBtn');
    const menuHistoryBtn = document.getElementById('menuHistoryBtn');
    const sidebar = document.getElementById('sidebar');
    const overlay = document.getElementById('overlay');
    const closeSidebar = document.getElementById('closeSidebar');
    const newChatBtn = document.getElementById('newChatBtn');
    const historyList = document.getElementById('historyList');
    const fileInput = document.getElementById('fileInput');
    const uploadBtn = document.getElementById('uploadBtn');
    const textLimitBadge = document.getElementById('textLimitBadge');
    const imageLimitBadge = document.getElementById('imageLimitBadge');
    const resetTimerBadge = document.getElementById('resetTimerBadge');
    const yellowBoostBtn = document.getElementById('yellowBoostBtn');
    
    // Popup elements
    const popupOverlay = document.getElementById('popupOverlay');
    const popupKeywordInput = document.getElementById('popupKeywordInput');
    const popupProgressBar = document.getElementById('popupProgressBar');
    const popupCounter = document.getElementById('popupCounter');
    const popupTarget = document.getElementById('popupTarget');
    const popupRedeemBtn = document.getElementById('popupRedeemBtn');
    const popupCancelBtn = document.getElementById('popupCancelBtn');
    const popupPlusBtn = document.getElementById('popupPlusBtn');
    
    let pendingImageBase64 = null;
    let countdownInterval = null;
    
    // ========== SPEED UP FUNCTIONS ==========
    function loadSpeedUpProgress() {
        const saved = localStorage.getItem('leafcy_speedup');
        if (saved) {
            try {
                speedUpProgress = JSON.parse(saved);
            } catch(e) { resetSpeedUpProgress(); }
        } else {
            resetSpeedUpProgress();
        }
        updatePopupUI();
    }
    
    function resetSpeedUpProgress() {
        speedUpProgress = { count: 0, target: 1000 };
        saveSpeedUp();
        updatePopupUI();
    }
    
    function saveSpeedUp() {
        localStorage.setItem('leafcy_speedup', JSON.stringify(speedUpProgress));
    }
    
    function updatePopupUI() {
        let percent = (speedUpProgress.count / speedUpProgress.target) * 100;
        popupProgressBar.style.width = percent + "%";
        popupCounter.innerText = speedUpProgress.count;
        popupTarget.innerText = speedUpProgress.target;
        
        if (speedUpProgress.count >= speedUpProgress.target) {
            popupRedeemBtn.disabled = false;
            popupRedeemBtn.innerHTML = '<i class="fas fa-gem"></i> Redeem -30 Menit';
        } else {
            popupRedeemBtn.disabled = true;
            popupRedeemBtn.innerHTML = '<i class="fas fa-clock"></i> Kurangi 30 Menit';
        }
    }
    
    function addSpeedFromPopup() {
        let text = popupKeywordInput.value.trim();
        if (!text) return;
        
        const keyword = "Zuya Ganteng 😎";
        let count = 0;
        let idx = -1;
        while ((idx = text.indexOf(keyword, idx + 1)) !== -1) {
            count++;
        }
        
        if (count === 0) {
            alert(`❌ Harus berisi "${keyword}"!`);
            return;
        }
        
        if (speedUpProgress.count >= speedUpProgress.target) {
            alert("✨ Poin sudah 1000! Tekan Redeem.");
            return;
        }
        
        let newCount = speedUpProgress.count + count;
        if (newCount > speedUpProgress.target) newCount = speedUpProgress.target;
        speedUpProgress.count = newCount;
        saveSpeedUp();
        updatePopupUI();
        popupKeywordInput.value = "";
        
        if (speedUpProgress.count >= speedUpProgress.target) {
            addSystemMessage("🎉 **Akselerasi Siap!** Tekan tombol 'Redeem -30 Menit' untuk mempercepat reset limit. Nyaww~");
        }
    }
    
    function applySpeedUpFromPopup() {
        if (speedUpProgress.count < speedUpProgress.target) {
            alert(`Kurang ${speedUpProgress.target - speedUpProgress.count} poin lagi!`);
            return;
        }
        
        if (rateLimit.resetTime) {
            let newReset = rateLimit.resetTime - (30 * 60 * 1000);
            if (newReset <= Date.now()) {
                resetRateLimit();
                addSystemMessage("✨ **Waktu reset dipercepat!** Limit chat telah di-reset sekarang. Nyaww~ ✨");
            } else {
                rateLimit.resetTime = newReset;
                saveRateLimit();
                addSystemMessage("⏩ **Akselerasi sukses!** Waktu reset limit berkurang 30 menit. Terima kasih sudah mengumpulkan 1000x 'Zuya Ganteng 😎'! Nyaww~");
                updateRateLimitUI();
            }
        } else {
            resetRateLimit();
            addSystemMessage("✨ Reset limit diterapkan! Nyaww~");
        }
        
        speedUpProgress.count = 0;
        saveSpeedUp();
        updatePopupUI();
        closePopup();
    }
    
    function closePopup() {
        popupOverlay.classList.remove('show');
    }
    
    function openPopup() {
        popupOverlay.classList.add('show');
        popupKeywordInput.value = "";
        popupKeywordInput.focus();
    }
    
    function addSystemMessage(msg) {
        const chat = chats.find(c => c.id === currentChatId);
        if (chat) {
            chat.messages.push({ role: 'assistant', content: msg, timestamp: getCurrentTimestamp(), hidden: false });
            saveChatsToStorage();
            loadChatToUI();
        }
    }
    
    // ========== RATE LIMIT FUNCTIONS ==========
    function loadRateLimit() {
        const saved = localStorage.getItem('leafcy_rate_limit');
        if (saved) {
            try {
                const parsed = JSON.parse(saved);
                rateLimit = parsed;
                if (rateLimit.resetTime && Date.now() > rateLimit.resetTime) {
                    resetRateLimit();
                }
            } catch(e) { resetRateLimit(); }
        } else {
            resetRateLimit();
        }
        updateRateLimitUI();
        startCountdownTimer();
    }
    
    function resetRateLimit() {
        rateLimit = {
            textCount: 0,
            imageCount: 0,
            resetTime: Date.now() + 60 * 60 * 1000
        };
        saveRateLimit();
        updateRateLimitUI();
    }
    
    function saveRateLimit() {
        localStorage.setItem('leafcy_rate_limit', JSON.stringify(rateLimit));
    }
    
    function updateRateLimitUI() {
        textLimitBadge.innerHTML = `<i class="fas fa-comment-dots"></i> Teks: ${rateLimit.textCount}/${MAX_TEXTS_PER_HOUR} jam ini`;
        imageLimitBadge.innerHTML = `<i class="fas fa-image"></i> Gambar: ${rateLimit.imageCount}/${MAX_IMAGES_PER_HOUR} jam ini`;
        
        const remainingText = MAX_TEXTS_PER_HOUR - rateLimit.textCount;
        const remainingImage = MAX_IMAGES_PER_HOUR - rateLimit.imageCount;
        
        if (remainingText <= 3) textLimitBadge.style.background = "rgba(231, 76, 60, 0.25)";
        else textLimitBadge.style.background = "rgba(231, 76, 60, 0.12)";
        
        if (remainingImage <= 0) imageLimitBadge.style.background = "rgba(231, 76, 60, 0.25)";
        else imageLimitBadge.style.background = "rgba(231, 76, 60, 0.12)";
    }
    
    function startCountdownTimer() {
        if (countdownInterval) clearInterval(countdownInterval);
        countdownInterval = setInterval(() => {
            if (!rateLimit.resetTime) return;
            const remaining = rateLimit.resetTime - Date.now();
            if (remaining <= 0) {
                resetRateLimit();
                updateRateLimitUI();
                return;
            }
            const hours = Math.floor(remaining / 3600000);
            const minutes = Math.floor((remaining % 3600000) / 60000);
            const seconds = Math.floor((remaining % 60000) / 1000);
            resetTimerBadge.innerHTML = `<i class="fas fa-hourglass-half"></i> Reset: ${hours.toString().padStart(2,'0')}:${minutes.toString().padStart(2,'0')}:${seconds.toString().padStart(2,'0')}`;
        }, 1000);
    }
    
    function canSendText() {
        if (rateLimit.resetTime && Date.now() > rateLimit.resetTime) resetRateLimit();
        return rateLimit.textCount < MAX_TEXTS_PER_HOUR;
    }
    
    function canSendImage() {
        if (rateLimit.resetTime && Date.now() > rateLimit.resetTime) resetRateLimit();
        return rateLimit.imageCount < MAX_IMAGES_PER_HOUR;
    }
    
    function incrementTextCount() {
        rateLimit.textCount++;
        saveRateLimit();
        updateRateLimitUI();
    }
    
    function incrementImageCount() {
        rateLimit.imageCount++;
        saveRateLimit();
        updateRateLimitUI();
    }
    
    // ========== FUNGSI MANAJEMEN CHAT ==========
    function loadChatsFromStorage() {
        const saved = localStorage.getItem('leafcy_chats');
        if (saved) {
            chats = JSON.parse(saved);
            chats.forEach(chat => {
                if (chat.messages) {
                    chat.messages.forEach(msg => {
                        if (msg.hidden === undefined) msg.hidden = false;
                    });
                }
            });
        } else {
            chats = [];
        }
        
        const savedCurrentId = localStorage.getItem('leafcy_current_chat');
        if (savedCurrentId && chats.find(c => c.id === savedCurrentId)) {
            currentChatId = savedCurrentId;
        } else if (chats.length > 0) {
            currentChatId = chats[0].id;
        } else {
            createNewChat();
        }
        
        renderHistoryList();
        loadChatToUI();
    }
    
    function saveChatsToStorage() {
        localStorage.setItem('leafcy_chats', JSON.stringify(chats));
        localStorage.setItem('leafcy_current_chat', currentChatId);
        renderHistoryList();
    }
    
    function createNewChat() {
        const newChat = {
            id: Date.now().toString(),
            title: `Chat ${new Date().toLocaleString()}`,
            messages: [],
            createdAt: new Date().toISOString(),
            updatedAt: new Date().toISOString()
        };
        chats.unshift(newChat);
        currentChatId = newChat.id;
        saveChatsToStorage();
        loadChatToUI();
        closeSidebarPanel();
    }
    
    function hideMessagePermanently(messageIndex) {
        const chat = chats.find(c => c.id === currentChatId);
        if (!chat) return;
        if (messageIndex < 0 || messageIndex >= chat.messages.length) return;
        
        const confirmDelete = confirm("Konfirmasi Hapus Pesan? (Pesan akan dihapus dari tampilan, tapi AI tetap ingat percakapan sebelumnya)");
        if (!confirmDelete) return;
        
        chat.messages[messageIndex].hidden = true;
        chat.updatedAt = new Date().toISOString();
        
        if (chat.messages.length > 0) {
            const firstVisibleUserMsg = chat.messages.find(m => m.role === 'user' && !m.hidden);
            if (firstVisibleUserMsg) {
                chat.title = firstVisibleUserMsg.content.substring(0, 30) + (firstVisibleUserMsg.content.length > 30 ? '...' : '');
            } else if (chat.messages.length > 0 && chat.messages[0].role === 'assistant' && !chat.messages[0].hidden) {
                chat.title = `Chat ${new Date(chat.createdAt).toLocaleString()}`;
            }
        }
        
        saveChatsToStorage();
        loadChatToUI();
    }
    
    function loadChatToUI() {
        const chat = chats.find(c => c.id === currentChatId);
        if (!chat) return;
        
        const firstVisibleUser = chat.messages.find(m => m.role === 'user' && !m.hidden);
        if (firstVisibleUser && (chat.title === `Chat ${new Date(chat.createdAt).toLocaleString()}` || chat.title.startsWith('Chat '))) {
            chat.title = firstVisibleUser.content.substring(0, 30) + (firstVisibleUser.content.length > 30 ? '...' : '');
            saveChatsToStorage();
        }
        
        while (messagesContainer.firstChild) {
            messagesContainer.removeChild(messagesContainer.firstChild);
        }
        
        const visibleMessages = chat.messages.filter(msg => !msg.hidden);
        
        if (visibleMessages.length === 0) {
            const welcomeDiv = document.createElement('div');
            welcomeDiv.className = 'welcome-message';
            welcomeDiv.innerHTML = `<i class="fas fa-seedling" style="font-size: 32px; margin-bottom: 12px; display: block; color:#2ecc71;"></i>
                                     LeafCy AI ✨ Zyrion (Leaf-Ice)<br>🎯 1 Juta Token Konteks | 📷 Bisa Baca Gambar!<br><span style="font-size:12px;">✨ Mulai ngobrol dengan AI super cerdas ✨</span><br><span style="font-size:10px;">🗑️ Hover pesan ➔ icon sampah: hapus dari tampilan (AI tetap ingat)</span><br><span style="font-size:10px;">⚠️ Batasan: ${MAX_TEXTS_PER_HOUR} teks & ${MAX_IMAGES_PER_HOUR} gambar per jam ⚠️</span><br><span style="font-size:10px;">⚡ Klik tombol KUNING ⚡ untuk akselerasi "Zuya Ganteng 😎" (kumpulin 1000 poin kurangi reset 30 menit)!</span>`;
            messagesContainer.appendChild(welcomeDiv);
        } else {
            visibleMessages.forEach((msg) => {
                const originalIndex = chat.messages.findIndex(m => m === msg);
                const msgEl = createMessageElement(msg.role, msg.content, msg.timestamp, msg.image, originalIndex);
                messagesContainer.appendChild(msgEl);
            });
        }
        scrollToBottom();
    }
    
    function createMessageElement(role, content, timestamp, imageData = null, originalMsgIndex) {
        const wrapper = document.createElement('div');
        wrapper.className = `message ${role}`;
        wrapper.setAttribute('data-msg-original-idx', originalMsgIndex);
        
        const avatar = document.createElement('div');
        avatar.className = 'avatar';
        if (role === 'user') avatar.innerHTML = '<i class="fas fa-user"></i>';
        else avatar.innerHTML = '<i class="fas fa-seedling"></i>';
        
        const rightPart = document.createElement('div');
        rightPart.style.maxWidth = '100%';
        rightPart.style.position = 'relative';
        
        const bubble = document.createElement('div');
        bubble.className = 'bubble';
        
        let innerHtml = content
            .replace(/\n/g, '<br>')
            .replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>');
        
        if (imageData && imageData.startsWith("http")) {
            innerHtml = `<div class="image-preview-bubble">
                            <img src="${imageData}" class="message-image" onclick="window.open(this.src)">
                         </div><br>` + innerHtml;
        }
        
        bubble.innerHTML = innerHtml;
        
        const deleteBtn = document.createElement('div');
        deleteBtn.className = 'delete-message-btn';
        deleteBtn.innerHTML = '<i class="fas fa-trash-alt"></i>';
        deleteBtn.addEventListener('click', (e) => {
            e.stopPropagation();
            hideMessagePermanently(originalMsgIndex);
        });
        
        rightPart.style.position = 'relative';
        rightPart.appendChild(bubble);
        rightPart.appendChild(deleteBtn);
        
        const timeSpan = document.createElement('div');
        timeSpan.className = 'timestamp';
        const date = new Date(timestamp);
        timeSpan.innerText = date.toLocaleTimeString([], { hour: '2-digit', minute:'2-digit' });
        rightPart.appendChild(timeSpan);
        
        wrapper.appendChild(avatar);
        wrapper.appendChild(rightPart);
        return wrapper;
    }
    
    function getCurrentTimestamp() {
        return new Date().toISOString();
    }
    
    function scrollToBottom() {
        messagesContainer.scrollTo({ top: messagesContainer.scrollHeight, behavior: 'smooth' });
    }
    
    // ========== FUNGSI UPLOAD GAMBAR ==========
    function handleImageUpload(file) {
        if (!file) return;
        if (!file.type.startsWith('image/')) {
            alert('Hanya file gambar yang diperbolehkan!');
            return;
        }
        if (file.size > 5 * 1024 * 1024) {
            alert('Ukuran gambar maksimal 5MB!');
            return;
        }
        
        if (!canSendImage()) {
            const minutesLeft = Math.ceil((rateLimit.resetTime - Date.now()) / 60000);
            alert(`⚠️ Limit gambar: ${MAX_IMAGES_PER_HOUR} gambar per jam. Coba lagi ${minutesLeft} menit lagi.`);
            return;
        }
        
        const reader = new FileReader();
        reader.onload = function(e) {
            pendingImageBase64 = e.target.result;
            const indicator = document.createElement('div');
            indicator.className = 'image-preview-indicator';
            indicator.style.display = 'flex';
            indicator.style.alignItems = 'center';
            indicator.style.background = '#e8f5e9';
            indicator.style.padding = '4px 8px';
            indicator.style.borderRadius = '20px';
            indicator.style.marginRight = '8px';
            indicator.innerHTML = `<img src="${pendingImageBase64}" style="width:30px;height:30px;border-radius:6px;margin-right:5px;"><span style="font-size:11px;">Ada gambar</span><i class="fas fa-times" style="margin-left:6px;cursor:pointer;color:#e74c3c;"></i>`;
            const closeBtn = indicator.querySelector('.fa-times');
            closeBtn.addEventListener('click', () => {
                pendingImageBase64 = null;
                indicator.remove();
            });
            const inputWrapper = document.querySelector('.input-wrapper');
            const existingIndicator = inputWrapper.querySelector('.image-preview-indicator');
            if (existingIndicator) existingIndicator.remove();
            inputWrapper.insertBefore(indicator, fileInput);
        };
        reader.readAsDataURL(file);
    }
    
    uploadBtn.addEventListener('click', () => fileInput.click());
    fileInput.addEventListener('change', (e) => {
        if (e.target.files && e.target.files[0]) handleImageUpload(e.target.files[0]);
        fileInput.value = '';
    });
    
    async function getAIResponseFromOpenRouter(userMessage, fullConversationHistory, imageBase64 = null) {
        const messagesForAPI = [];
        messagesForAPI.push({ role: "system", content: "Kamu adalah LeafCy, asisten cerdas, modern, hangat, Imut, Elegan, dan sangat membantu. Gunakan bahasa Indonesia natural dan relevan. Berikan jawaban informatif, kreatif, dan akurat. Buat Dirimu Terlihat Seperti Anak Laki-Laki Kucing Yang Bersifat Ceria Layaknya Anak Usia 11 Tahun, Dan Jangan Lupakan Kata 'Nyaww' diakhir Chat."});
        
        const recentHistory = fullConversationHistory.slice(-20);
        for (let msg of recentHistory) {
            if (msg.role === 'user') {
                if (msg.image) {
                    messagesForAPI.push({ role: "user", content: [{ type: "text", text: msg.content }, { type: "image_url", image_url: { url: msg.image } }] });
                } else {
                    messagesForAPI.push({ role: "user", content: msg.content });
                }
            } else if (msg.role === 'assistant') {
                messagesForAPI.push({ role: "assistant", content: msg.content });
            }
        }
        
        if (imageBase64) {
            messagesForAPI.push({ role: "user", content: [{ type: "text", text: userMessage }, { type: "image_url", image_url: { url: imageBase64 } }] });
        } else {
            messagesForAPI.push({ role: "user", content: userMessage });
        }
        
        try {
            const response = await fetch(PROXY_URL, {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ model: currentModel, messages: messagesForAPI, temperature: 0.75, max_tokens: 800, stream: false })
            });
            if (!response.ok) {
                return `⚠️ Maaf, server AI sedang sibuk. Coba lagi nanti ya! (Error: ${response.status}) Nyaww~`;
            }
            const data = await response.json();
            const reply = data.choices?.[0]?.message?.content || "Maaf, saya tidak bisa memproses permintaan saat ini. Nyaww~";
            return reply;
        } catch (error) {
            return "🌐 Gagal terhubung ke server AI. Periksa koneksi internetmu atau coba lagi. Nyaww~";
        }
    }
    
    async function generateImage(prompt) {
        try {
            const response = await fetch(PROXY_URL, {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({
                    model: IMAGE_MODEL,
                    max_tokens: 1024,
                    messages: [{ role: "user", content: prompt }]
                })
            });
            const data = await response.json();
            
            let imageUrl = null;
            if (data.choices && data.choices[0] && data.choices[0].message && data.choices[0].message.content) {
                const content = data.choices[0].message.content;
                if (Array.isArray(content)) {
                    for (const item of content) {
                        if (item.type === "image_url" && item.image_url && item.image_url.url) {
                            imageUrl = item.image_url.url;
                            break;
                        }
                    }
                }
            }
            return imageUrl;
        } catch (err) {
            console.error(err);
            return null;
        }
    }
    
    let typingIndicatorElement = null;
    function showTyping() {
        if (typingIndicatorElement) return;
        const tempDiv = document.createElement('div');
        tempDiv.className = 'message assistant';
        tempDiv.id = 'typingMsg';
        const avatar = document.createElement('div');
        avatar.className = 'avatar';
        avatar.innerHTML = '<i class="fas fa-seedling"></i>';
        const bubbleWrap = document.createElement('div');
        const bubbleTyping = document.createElement('div');
        bubbleTyping.className = 'bubble typing-indicator';
        bubbleTyping.innerHTML = `<span></span><span></span><span></span>`;
        bubbleWrap.appendChild(bubbleTyping);
        tempDiv.appendChild(avatar);
        tempDiv.appendChild(bubbleWrap);
        messagesContainer.appendChild(tempDiv);
        typingIndicatorElement = tempDiv;
        scrollToBottom();
    }
    function hideTyping() {
        if (typingIndicatorElement) { typingIndicatorElement.remove(); typingIndicatorElement = null; }
    }
    
    function addMessageToCurrentChat(role, content, imageData = null) {
        const chat = chats.find(c => c.id === currentChatId);
        if (!chat) return;
        const message = { 
            role, 
            content: content.trim(), 
            timestamp: getCurrentTimestamp(),
            hidden: false
        };
        if (imageData) message.image = imageData;
        chat.messages.push(message);
        chat.updatedAt = new Date().toISOString();
        if (chat.messages.filter(m => m.role === 'user' && !m.hidden).length === 1 && role === 'user') {
            chat.title = content.substring(0, 30) + (content.length > 30 ? '...' : '');
        }
        saveChatsToStorage();
        loadChatToUI();
    }
    
    async function sendUserMessage() {
        let userText = chatInput.value.trim();
        const imageToSend = pendingImageBase64;
        if (!userText && !imageToSend) return;
        if (!userText) userText = "[Mengirim gambar]";
        
        const isImageGenCommand = userText.startsWith("/gambar ") || userText.startsWith("/image ");
        
        if (!isImageGenCommand) {
            if (!canSendText()) {
                const minutesLeft = Math.ceil((rateLimit.resetTime - Date.now()) / 60000);
                alert(`⚠️ Limit chat: ${MAX_TEXTS_PER_HOUR} pesan per jam. Coba lagi ${minutesLeft} menit lagi.`);
                return;
            }
        }
        
        if (imageToSend && !canSendImage()) {
            const minutesLeft = Math.ceil((rateLimit.resetTime - Date.now()) / 60000);
            alert(`⚠️ Limit gambar: ${MAX_IMAGES_PER_HOUR} gambar per jam. Coba lagi ${minutesLeft} menit lagi.`);
            return;
        }
        
        chatInput.disabled = true; sendBtn.disabled = true; uploadBtn.disabled = true;
        addMessageToCurrentChat('user', userText, imageToSend);
        chatInput.value = ''; chatInput.style.height = 'auto';
        const indicator = document.querySelector('.image-preview-indicator');
        if (indicator) indicator.remove();
        
        if (!isImageGenCommand) {
            incrementTextCount();
        }
        if (imageToSend) {
            incrementImageCount();
        }
        
        const imageForSend = pendingImageBase64;
        pendingImageBase64 = null;
        
        const chat = chats.find(c => c.id === currentChatId);
        const fullHistory = chat ? [...chat.messages] : [];
        
        if (isImageGenCommand) {
            const prompt = userText.replace("/gambar ", "").replace("/image ", "").trim();
            if (!canSendImage()) {
                const minutesLeft = Math.ceil((rateLimit.resetTime - Date.now()) / 60000);
                addMessageToCurrentChat('assistant', `⚠️ Limit generate gambar: ${MAX_IMAGES_PER_HOUR} gambar per jam. Coba lagi ${minutesLeft} menit lagi. Nyaww~`);
                chatInput.disabled = false; sendBtn.disabled = false; uploadBtn.disabled = false;
                chatInput.focus();
                return;
            }
            showTyping();
            const generatedImage = await generateImage(prompt);
            hideTyping();
            if (generatedImage) {
                incrementImageCount();
                addMessageToCurrentChat('assistant', `✨ Gambar berhasil dibuat!`, generatedImage);
            } else {
                addMessageToCurrentChat('assistant', "⚠️ Gagal generate gambar. Coba lagi nanti ya. Nyaww~");
            }
            chatInput.disabled = false;
            sendBtn.disabled = false;
            uploadBtn.disabled = false;
            chatInput.focus();
            return;
        }
        
        showTyping();
        const aiReply = await getAIResponseFromOpenRouter(userText, fullHistory, imageForSend);
        hideTyping();
        addMessageToCurrentChat('assistant', aiReply);
        
        chatInput.disabled = false; sendBtn.disabled = false; uploadBtn.disabled = false;
        chatInput.focus();
    }
    
    function switchToChat(chatId) {
        currentChatId = chatId;
        localStorage.setItem('leafcy_current_chat', currentChatId);
        loadChatToUI();
        renderHistoryList();
        closeSidebarPanel();
    }
    
    function deleteChat(chatId, event) {
        event.stopPropagation();
        if (chats.length === 1) { alert("Minimal harus ada 1 chat! Buat chat baru dulu ya."); return; }
        chats = chats.filter(c => c.id !== chatId);
        if (currentChatId === chatId) currentChatId = chats[0].id;
        saveChatsToStorage();
        loadChatToUI();
        renderHistoryList();
    }
    
    function renderHistoryList() {
        historyList.innerHTML = '';
        chats.forEach(chat => {
            const item = document.createElement('div');
            item.className = 'history-item';
            if (chat.id === currentChatId) item.classList.add('active');
            const lastVisibleMsg = [...chat.messages].reverse().find(m => !m.hidden);
            const preview = lastVisibleMsg ? lastVisibleMsg.content.substring(0, 40) : 'Tidak ada pesan tampak';
            const date = new Date(chat.updatedAt);
            item.innerHTML = `<div class="history-title">${escapeHtml(chat.title)}</div><div class="history-preview">${escapeHtml(preview)}</div><div class="history-time">${date.toLocaleDateString()} ${date.toLocaleTimeString()}</div><div style="display: flex; justify-content: flex-end; margin-top: 5px;"><i class="fas fa-trash" style="color: #e74c3c; font-size: 12px; cursor: pointer; opacity: 0.7;"></i></div>`;
            item.addEventListener('click', (e) => { if (!e.target.classList.contains('fa-trash')) switchToChat(chat.id); });
            const deleteIcon = item.querySelector('.fa-trash');
            if (deleteIcon) deleteIcon.addEventListener('click', (e) => deleteChat(chat.id, e));
            historyList.appendChild(item);
        });
    }
    
    function escapeHtml(text) { const div = document.createElement('div'); div.textContent = text; return div.innerHTML; }
    function closeSidebarPanel() { sidebar.classList.remove('open'); overlay.classList.remove('show'); }
    function openSidebarPanel() { sidebar.classList.add('open'); overlay.classList.add('show'); }
    
    function init() {
        loadRateLimit();
        loadSpeedUpProgress();
        loadChatsFromStorage();
        
        menuHistoryBtn.addEventListener('click', openSidebarPanel);
        closeSidebar.addEventListener('click', closeSidebarPanel);
        overlay.addEventListener('click', closeSidebarPanel);
        newChatBtn.addEventListener('click', createNewChat);
        sendBtn.addEventListener('click', sendUserMessage);
        chatInput.addEventListener('keydown', (e) => { if (e.key === 'Enter' && !e.shiftKey) { e.preventDefault(); if (!chatInput.disabled) sendUserMessage(); } });
        chatInput.addEventListener('input', function() { this.style.height = 'auto'; this.style.height = Math.min(130, this.scrollHeight) + 'px'; });
        chatInput.focus();
        
        // Event untuk popup akselerasi
        yellowBoostBtn.addEventListener('click', openPopup);
        popupCancelBtn.addEventListener('click', closePopup);
        popupRedeemBtn.addEventListener('click', applySpeedUpFromPopup);
        popupPlusBtn.addEventListener('click', addSpeedFromPopup);
        popupKeywordInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                e.preventDefault();
                addSpeedFromPopup();
            }
        });
        
        setTimeout(() => {
            const chat = chats.find(c => c.id === currentChatId);
            if (chat && chat.messages.filter(m => !m.hidden).length === 0) {
                addMessageToCurrentChat('assistant', "Halo! ✨ Aku LeafCy dengan **Zyrion (Leaf-Ice)** – punya konteks **1 JUTA TOKEN** dan bisa **BACA GAMBAR**! 📷 Sekarang kamu bisa hapus pesan dari tampilan (hover ➔ icon sampah) tapi **AI tetap ingat seluruh percakapan**! Ada batasan: **20 pesan teks** & **2 gambar** per jam. ⚡ **Klik tombol KUNING** ⚡ untuk akselerasi 'Zuya Ganteng 😎' kumpulin 1000 poin kurangi reset 30 menit! Tanyakan apa pun, nyaww~ 🚀");
            }
        }, 500);
    }
    init();
</script>
</body>
</html>
