<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>LeafCy AI [New Beta]</title>
    <!-- Google Fonts + Font Awesome -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,500;14..32,600;14..32,700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        /* Reset & modern base - Tema Hijau Putih */
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

        /* Header elegant */
        .chat-header {
            padding: 16px 24px;
            background: #ffffff;
            border-bottom: 1px solid #2ecc71;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .logo-area {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        /* Tombol Menu (3 titik) */
        .menu-btn {
            background: rgba(46, 204, 113, 0.12);
            border-radius: 40px;
            padding: 8px 12px;
            font-size: 1rem;
            font-weight: 500;
            color: #2ecc71;
            cursor: pointer;
            transition: all 0.2s ease;
            border: 1px solid rgba(46, 204, 113, 0.3);
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .menu-btn:hover {
            background: rgba(46, 204, 113, 0.25);
            transform: scale(1.02);
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
        
        /* Sidebar Menu History */
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

        /* Menu cara ambil API Key */
        .guide-menu {
            background: rgba(46, 204, 113, 0.12);
            border-radius: 40px;
            padding: 5px 12px;
            font-size: 0.7rem;
            font-weight: 500;
            color: #2ecc71;
            display: flex;
            align-items: center;
            gap: 6px;
            cursor: pointer;
            transition: all 0.2s ease;
            border: 1px solid rgba(46, 204, 113, 0.3);
        }
        .guide-menu:hover {
            background: rgba(46, 204, 113, 0.25);
            color: #27ae60;
            transform: scale(1.02);
        }

        /* Chat messages container */
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

        /* bubble animation */
        .message {
            display: flex;
            align-items: flex-start;
            gap: 12px;
            max-width: 85%;
            animation: fadeSlideUp 0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1);
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

        /* Style untuk gambar di chat */
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

        /* Input area */
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

        /* Tombol upload foto */
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
        
        /* Sembunyikan input file asli */
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

        /* Reset Chat Button */
        .action-clear {
            position: absolute;
            bottom: 100px;
            right: 20px;
            background: #ffffff;
            border-radius: 40px;
            padding: 8px 15px;
            font-size: 0.75rem;
            font-weight: 500;
            color: #e74c3c;
            display: flex;
            align-items: center;
            gap: 8px;
            cursor: pointer;
            backdrop-filter: blur(10px);
            z-index: 10;
            transition: 0.2s;
            border: 1px solid #e74c3c;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        .action-clear:hover {
            background: #e74c3c;
            color: white;
            transform: scale(1.02);
        }

        /* typing indicator */
        .typing-indicator {
            display: flex;
            align-items: center;
            gap: 5px;
            padding: 10px 18px;
            background: #f0f4f0;
            border-radius: 28px;
            width: fit-content;
        }

        .typing-indicator span {
            width: 8px;
            height: 8px;
            background: #2ecc71;
            border-radius: 50%;
            display: inline-block;
            animation: pulseBlink 1.2s infinite;
        }
        .typing-indicator span:nth-child(2) { animation-delay: 0.2s; }
        .typing-indicator span:nth-child(3) { animation-delay: 0.4s; }

        @keyframes pulseBlink {
            0%, 60%, 100% { transform: scale(0.7); opacity: 0.4; }
            30% { transform: scale(1.2); opacity: 1; }
        }

        .welcome-message {
            text-align: center;
            margin: auto;
            padding: 30px;
            color: #5a8a5a;
        }

        .api-warning {
            background: rgba(231, 76, 60, 0.12);
            color: #e74c3c;
            font-size: 0.7rem;
            padding: 5px 12px;
            border-radius: 40px;
            display: inline-flex;
            align-items: center;
            gap: 6px;
        }
        
        /* Modal panduan API Key */
        .modal-guide {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            backdrop-filter: blur(5px);
            z-index: 1002;
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            background: #ffffff;
            max-width: 450px;
            width: 90%;
            border-radius: 32px;
            padding: 24px;
            border: 2px solid #2ecc71;
            color: #1a1a1a;
            font-size: 0.9rem;
            line-height: 1.5;
            box-shadow: 0 20px 35px rgba(0,0,0,0.3);
        }
        .modal-content h3 {
            margin-bottom: 16px;
            color: #2ecc71;
            display: flex;
            gap: 10px;
            align-items: center;
        }
        .modal-content ol {
            padding-left: 20px;
            margin: 15px 0;
        }
        .modal-content li {
            margin: 10px 0;
        }
        .close-modal {
            background: linear-gradient(135deg, #2ecc71, #27ae60);
            border: none;
            padding: 10px 20px;
            border-radius: 40px;
            color: white;
            margin-top: 16px;
            cursor: pointer;
            width: 100%;
            font-weight: bold;
        }
        .code-block {
            background: #f0f4f0;
            padding: 8px;
            border-radius: 12px;
            font-family: monospace;
            font-size: 0.7rem;
            word-break: break-all;
            margin-top: 10px;
        }
        .bottom-info-text {
            font-size: 11px;
            color: #5a8a5a;
        }
        @media (max-width: 600px) {
            .message { max-width: 92%; }
            .sidebar { width: 280px; }
        }
    </style>
</head>
<body>
<div class="app">
    <div class="chat-header">
        <div class="logo-area">
            <div id="menuBtn" class="menu-btn"><i class="fas fa-ellipsis-v"></i></div>
            <div class="logo-icon">
                <img src="leafcy.png" alt="Logo" onerror="this.src='https://via.placeholder.com/36x36/2ecc71/ffffff?text=Leaf'">
            </div>
            <div class="logo-text">LeafCy AI</div>
            <div class="model-badge" id="modelBadge"><i class="fas fa-charging-station"></i> Zyrion (Leaf-Ice)</div>
        </div>
        <div style="display: flex; gap: 12px; align-items: center;">
            <div id="guideApiBtn" class="guide-menu"><i class="fas fa-question-circle"></i> Cara Ambil API Key</div>
            <div id="apiStatus" class="api-warning" style="background: #fdeaea;"><i class="fas fa-key"></i> API Key ?</div>
        </div>
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
            <div class="bottom-info-text"><i class="fas fa-database"></i> history scrollable</div>
        </div>
    </div>
    
    <div class="action-clear" id="clearChatBtn">
        <i class="fas fa-trash-alt"></i> Reset Chat
    </div>
</div>

<!-- Sidebar History -->
<div class="overlay" id="overlay"></div>
<div class="sidebar" id="sidebar">
    <div class="sidebar-header">
        <h3><i class="fas fa-history"></i> Riwayat Chat</h3>
        <button class="close-sidebar" id="closeSidebar"><i class="fas fa-times"></i></button>
    </div>
    <div class="history-list" id="historyList"></div>
    <button class="new-chat-btn" id="newChatBtn"><i class="fas fa-plus-circle"></i> Chat Baru</button>
</div>

<!-- Modal Panduan API Key -->
<div id="apiGuideModal" class="modal-guide">
    <div class="modal-content">
        <h3><i class="fas fa-seedling"></i> Cara Mendapatkan API Key OpenRouter</h3>
        <ol>
            <li>Kunjungi <strong><a href="https://openrouter.io/keys" target="_blank" style="color:#2ecc71;">https://openrouter.io/keys</a></strong> (buka di tab baru).</li>
            <li>Daftar / Login menggunakan akun Google atau Email.</li>
            <li>Setelah masuk, klik tombol <strong>"Create Key"</strong>.</li>
            <li>Beri nama key (contoh: LeafCyAI) lalu klik Create.</li>
            <li>Copy kunci API yang muncul (contoh: <code>sk-or-v1-xxxxxxxxxxxx</code>).</li>
            <li>Kembali ke chat ini, lalu klik <strong>ikon kunci di pojok kanan atas (API Key ?)</strong>.</li>
            <li>Masukkan API Key yang sudah di-copy, lalu tekan OK.</li>
        </ol>
        <p>✅ Selesai! Sekarang LeafCy AI menggunakan <strong>Zyrion (Leaf-Ice)</strong> dengan konteks 1 Juta token dan bisa membaca gambar!</p>
        <div class="code-block">💡 Tips: Key akan tersimpan di browser (localStorage) sehingga tidak perlu input ulang setiap kali.</div>
        <button class="close-modal" id="closeModalBtn">Mengerti, Tutup</button>
    </div>
</div>

<script>
    // --------------------------------------------------------------
    // LeafCy AI - Dengan Fitur Chat History + Upload Gambar
    // 🔥 MENGGUNAKAN ZYRION (LEAF-ICE) - 1 JUTA TOKEN KONTEKS 🔥
    // --------------------------------------------------------------
    let OPENROUTER_API_KEY = localStorage.getItem('leafcy_api_key') || ''; 
    const DEFAULT_MODEL = "google/gemini-2.0-flash-001";
    let currentModel = DEFAULT_MODEL;
    
    // Data struktur chat
    let chats = []; // { id, title, messages, createdAt, updatedAt }
    let currentChatId = null;
    
    // DOM elements
    const messagesContainer = document.getElementById('chatMessages');
    const chatInput = document.getElementById('chatInput');
    const sendBtn = document.getElementById('sendBtn');
    const clearBtn = document.getElementById('clearChatBtn');
    const apiStatusDiv = document.getElementById('apiStatus');
    const guideApiBtn = document.getElementById('guideApiBtn');
    const modalGuide = document.getElementById('apiGuideModal');
    const closeModalBtn = document.getElementById('closeModalBtn');
    const menuBtn = document.getElementById('menuBtn');
    const sidebar = document.getElementById('sidebar');
    const overlay = document.getElementById('overlay');
    const closeSidebar = document.getElementById('closeSidebar');
    const newChatBtn = document.getElementById('newChatBtn');
    const historyList = document.getElementById('historyList');
    const fileInput = document.getElementById('fileInput');
    const uploadBtn = document.getElementById('uploadBtn');
    
    // Variabel untuk menyimpan gambar yang akan diupload
    let pendingImage = null;
    let pendingImageBase64 = null;
    
    // ========== FUNGSI MANAJEMEN CHAT ==========
    function loadChatsFromStorage() {
        const saved = localStorage.getItem('leafcy_chats');
        if (saved) {
            chats = JSON.parse(saved);
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
    
    function loadChatToUI() {
        const chat = chats.find(c => c.id === currentChatId);
        if (!chat) return;
        
        if (chat.messages.length > 0 && chat.title === `Chat ${new Date(chat.createdAt).toLocaleString()}`) {
            const firstUserMsg = chat.messages.find(m => m.role === 'user');
            if (firstUserMsg) {
                chat.title = firstUserMsg.content.substring(0, 30) + (firstUserMsg.content.length > 30 ? '...' : '');
                saveChatsToStorage();
            }
        }
        
        while (messagesContainer.firstChild) {
            messagesContainer.removeChild(messagesContainer.firstChild);
        }
        
        if (chat.messages.length === 0) {
            const welcomeDiv = document.createElement('div');
            welcomeDiv.className = 'welcome-message';
            welcomeDiv.innerHTML = `<i class="fas fa-seedling" style="font-size: 32px; margin-bottom: 12px; display: block; color:#2ecc71;"></i>
                                     LeafCy AI ✨ Zyrion (Leaf-Ice)<br>🎯 1 Juta Token Konteks | 📷 Bisa Baca Gambar!<br><span style="font-size:12px;">✨ Mulai ngobrol dengan AI super cerdas ✨</span>`;
            messagesContainer.appendChild(welcomeDiv);
        } else {
            chat.messages.forEach(msg => {
                const msgEl = createMessageElement(msg.role, msg.content, msg.timestamp, msg.image);
                messagesContainer.appendChild(msgEl);
            });
        }
        scrollToBottom();
    }
    
    function addMessageToCurrentChat(role, content, imageData = null) {
        const chat = chats.find(c => c.id === currentChatId);
        if (!chat) return;
        
        const message = {
            role: role,
            content: content.trim(),
            timestamp: getCurrentTimestamp()
        };
        if (imageData) {
            message.image = imageData;
        }
        
        chat.messages.push(message);
        chat.updatedAt = new Date().toISOString();
        
        if (chat.messages.length === 1 && role === 'user') {
            chat.title = content.substring(0, 30) + (content.length > 30 ? '...' : '');
        }
        
        saveChatsToStorage();
        loadChatToUI();
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
        if (chats.length === 1) {
            alert("Minimal harus ada 1 chat! Buat chat baru dulu ya.");
            return;
        }
        chats = chats.filter(c => c.id !== chatId);
        if (currentChatId === chatId) {
            currentChatId = chats[0].id;
        }
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
            
            const lastMsg = chat.messages[chat.messages.length - 1];
            const preview = lastMsg ? lastMsg.content.substring(0, 40) : 'Belum ada pesan';
            const date = new Date(chat.updatedAt);
            
            item.innerHTML = `
                <div class="history-title">${escapeHtml(chat.title)}</div>
                <div class="history-preview">${escapeHtml(preview)}</div>
                <div class="history-time">${date.toLocaleDateString()} ${date.toLocaleTimeString()}</div>
                <div style="display: flex; justify-content: flex-end; margin-top: 5px;">
                    <i class="fas fa-trash" style="color: #e74c3c; font-size: 12px; cursor: pointer; opacity: 0.7;"></i>
                </div>
            `;
            
            item.addEventListener('click', (e) => {
                if (!e.target.classList.contains('fa-trash')) {
                    switchToChat(chat.id);
                }
            });
            
            const deleteIcon = item.querySelector('.fa-trash');
            if (deleteIcon) {
                deleteIcon.addEventListener('click', (e) => deleteChat(chat.id, e));
            }
            
            historyList.appendChild(item);
        });
    }
    
    function escapeHtml(text) {
        const div = document.createElement('div');
        div.textContent = text;
        return div.innerHTML;
    }
    
    function closeSidebarPanel() {
        sidebar.classList.remove('open');
        overlay.classList.remove('show');
    }
    
    function openSidebarPanel() {
        sidebar.classList.add('open');
        overlay.classList.add('show');
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
        
        const reader = new FileReader();
        reader.onload = function(e) {
            pendingImageBase64 = e.target.result;
            const imgPreview = document.createElement('img');
            imgPreview.src = pendingImageBase64;
            imgPreview.style.maxWidth = '40px';
            imgPreview.style.maxHeight = '40px';
            imgPreview.style.borderRadius = '8px';
            imgPreview.style.marginRight = '8px';
            
            const oldPreview = document.querySelector('.image-preview-indicator');
            if (oldPreview) oldPreview.remove();
            
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
    
    uploadBtn.addEventListener('click', () => {
        fileInput.click();
    });
    
    fileInput.addEventListener('change', (e) => {
        if (e.target.files && e.target.files[0]) {
            handleImageUpload(e.target.files[0]);
        }
        fileInput.value = '';
    });
    
    // ========== FUNGSI UTAMA ==========
    function updateApiStatusUI() {
        if (OPENROUTER_API_KEY && OPENROUTER_API_KEY.length > 10) {
            apiStatusDiv.innerHTML = `<i class="fas fa-check-circle"></i> API Active`;
            apiStatusDiv.style.background = "rgba(46, 204, 113, 0.15)";
            apiStatusDiv.style.color = "#2ecc71";
        } else {
            apiStatusDiv.innerHTML = `<i class="fas fa-key"></i> Set API Key`;
            apiStatusDiv.style.background = "#fdeaea";
            apiStatusDiv.style.color = "#e74c3c";
        }
    }

    function promptForApiKey() {
        let newKey = prompt("🔑 Masukkan OpenRouter API Key kamu:\n(Dapatkan di https://openrouter.io/keys)\n\nAPI Key akan disimpan di localStorage.", OPENROUTER_API_KEY);
        if (newKey && newKey.trim().length > 0) {
            OPENROUTER_API_KEY = newKey.trim();
            localStorage.setItem('leafcy_api_key', OPENROUTER_API_KEY);
            updateApiStatusUI();
            return true;
        } else if (newKey === "") {
            alert("API Key diperlukan agar LeafCy bisa merespon dengan kecerdasan Sendiri. Masukkan key yang valid.");
        }
        return false;
    }
    
    function showApiGuide() {
        modalGuide.style.display = 'flex';
    }
    function closeModal() {
        modalGuide.style.display = 'none';
    }

    async function getAIResponseFromOpenRouter(userMessage, conversationHistory, imageBase64 = null) {
        if (!OPENROUTER_API_KEY || OPENROUTER_API_KEY.length < 20) {
            const wantKey = confirm("⚠️ API Key OpenRouter belum ditemukan. Ingin memasukkan API Key sekarang?\n\nKlik 'OK' untuk masukkan key, atau 'Batal' untuk lihat panduan.");
            if (wantKey) {
                const hasKey = promptForApiKey();
                if (!hasKey) {
                    showApiGuide();
                    return "🌸 **API Key diperlukan** agar LeafCy bisa merespon dengan kecerdasan penuh. Silakan klik tombol 'Cara Ambil API Key' di pojok kanan atas, ikuti panduan, lalu masukkan key-mu ya! Nyaww~";
                }
            } else {
                showApiGuide();
                return "🍃 **Belum ada API Key!** Klik tombol 'Cara Ambil API Key' di samping logo untuk panduan mendapatkan key dari OpenRouter. Setelah punya key, klik ikon kunci untuk memasukkannya. Nyaww~";
            }
        }
        
        const messagesForAPI = [];
        messagesForAPI.push({ role: "system", content: "Kamu adalah LeafCy, asisten cerdas, modern, hangat,Imut,Elegan, dan sangat membantu. Gunakan bahasa Indonesia natural dan relevan. Berikan jawaban informatif, kreatif, dan akurat,Buat Dirimu Terlihat Seperti Anak Laki-Laki Kucing Yang Bersifat Ceria Layaknya Anak Usia 11 Tahun,Dan Jangan Lupakan Kata 'Nyaww' diakhir Chat"});
        
        const recentHistory = conversationHistory.slice(-12);
        for (let msg of recentHistory) {
            if (msg.role === 'user') {
                if (msg.image) {
                    messagesForAPI.push({ 
                        role: "user", 
                        content: [
                            { type: "text", text: msg.content },
                            { type: "image_url", image_url: { url: msg.image } }
                        ]
                    });
                } else {
                    messagesForAPI.push({ role: "user", content: msg.content });
                }
            } else if (msg.role === 'assistant') {
                messagesForAPI.push({ role: "assistant", content: msg.content });
            }
        }
        
        // Pesan user saat ini (bisa dengan gambar)
        if (imageBase64) {
            messagesForAPI.push({ 
                role: "user", 
                content: [
                    { type: "text", text: userMessage },
                    { type: "image_url", image_url: { url: imageBase64 } }
                ]
            });
        } else {
            messagesForAPI.push({ role: "user", content: userMessage });
        }
        
        try {
            const response = await fetch("https://openrouter.ai/api/v1/chat/completions", {
                method: "POST",
                headers: {
                    "Authorization": `Bearer ${OPENROUTER_API_KEY}`,
                    "Content-Type": "application/json",
                    "HTTP-Referer": window.location.origin,
                    "X-Title": "LeafCy AI [New Beta] X OpenRouter"
                },
                body: JSON.stringify({
                    model: currentModel,
                    messages: messagesForAPI,
                    temperature: 0.7,
                    max_tokens: 800,
                    stream: false
                })
            });
            
            if (!response.ok) {
                const errData = await response.json().catch(() => ({}));
                console.error("OpenRouter error", errData);
                if (response.status === 401) {
                    localStorage.removeItem('leafcy_api_key');
                    OPENROUTER_API_KEY = '';
                    updateApiStatusUI();
                    return "🔐 **API Key tidak valid atau expired.** Silakan masukkan ulang API Key dari OpenRouter. Klik ikon kunci untuk mengganti key. Nyaww~";
                } else if (response.status === 404) {
                    return "⚠️ Model Zyrion (Leaf-Ice) sedang dalam masa transisi. Coba lagi sebentar. Nyaww~";
                }
                return `⚠️ Terjadi kesalahan API: ${response.status} ${errData.error?.message || 'Cek kembali key atau kuota.'} Nyaww~`;
            }
            
            const data = await response.json();
            const reply = data.choices?.[0]?.message?.content || "Maaf, saya tidak bisa memproses permintaan saat ini. Nyaww~";
            return reply;
        } catch (error) {
            console.error("Fetch error:", error);
            return "🌐 Gagal terhubung ke OpenRouter. Periksa koneksi internetmu atau coba lagi. Nyaww~";
        }
    }
    
    function createMessageElement(role, content, timestamp, imageData = null) {
        const wrapper = document.createElement('div');
        wrapper.className = `message ${role}`;
        const avatar = document.createElement('div');
        avatar.className = 'avatar';
        if (role === 'user') avatar.innerHTML = '<i class="fas fa-user"></i>';
        else avatar.innerHTML = '<i class="fas fa-seedling"></i>';
        
        const rightPart = document.createElement('div');
        rightPart.style.maxWidth = '100%';
        const bubble = document.createElement('div');
        bubble.className = 'bubble';
        
        let innerHtml = formatContent(content);
        if (imageData && role === 'user') {
            innerHtml = `<div class="image-preview-bubble"><img src="${imageData}" class="message-image" onclick="window.open(this.src)"></div><br>` + innerHtml;
        }
        bubble.innerHTML = innerHtml;
        
        const timeSpan = document.createElement('div');
        timeSpan.className = 'timestamp';
        const date = new Date(timestamp);
        timeSpan.innerText = date.toLocaleTimeString([], { hour: '2-digit', minute:'2-digit' });
        rightPart.appendChild(bubble);
        rightPart.appendChild(timeSpan);
        wrapper.appendChild(avatar);
        wrapper.appendChild(rightPart);
        return wrapper;
    }
    
    function formatContent(text) {
        return text.replace(/\n/g, '<br>').replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>');
    }
    
    function getCurrentTimestamp() {
        return new Date().toISOString();
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
        if (typingIndicatorElement) {
            typingIndicatorElement.remove();
            typingIndicatorElement = null;
        }
    }
    
    function scrollToBottom() {
        messagesContainer.scrollTo({ top: messagesContainer.scrollHeight, behavior: 'smooth' });
    }
    
    async function sendUserMessage() {
        let userText = chatInput.value.trim();
        const imageToSend = pendingImageBase64;
        
        if (!userText && !imageToSend) return;
        if (!userText) userText = "[Mengirim gambar]";
        
        chatInput.disabled = true;
        sendBtn.disabled = true;
        uploadBtn.disabled = true;
        
        addMessageToCurrentChat('user', userText, imageToSend);
        chatInput.value = '';
        chatInput.style.height = 'auto';
        
        const indicator = document.querySelector('.image-preview-indicator');
        if (indicator) indicator.remove();
        pendingImageBase64 = null;
        
        const chat = chats.find(c => c.id === currentChatId);
        const chatHistoryForAPI = chat ? chat.messages.slice(0, -1) : [];
        
        showTyping();
        const aiReply = await getAIResponseFromOpenRouter(userText, chatHistoryForAPI, imageToSend);
        hideTyping();
        addMessageToCurrentChat('assistant', aiReply);
        
        chatInput.disabled = false;
        sendBtn.disabled = false;
        uploadBtn.disabled = false;
        chatInput.focus();
    }
    
    function resetCurrentChat() {
        if (confirm('Hapus semua pesan di chat ini?')) {
            const chat = chats.find(c => c.id === currentChatId);
            if (chat) {
                chat.messages = [];
                chat.updatedAt = new Date().toISOString();
                saveChatsToStorage();
                loadChatToUI();
                addMessageToCurrentChat('assistant', 'Riwayat chat ini direset! ✨ Aku siap membantu Kamu! Tanyakan apa saja! Nyaww~');
            }
        }
    }
    
    function init() {
        loadChatsFromStorage();
        updateApiStatusUI();
        
        menuBtn.addEventListener('click', openSidebarPanel);
        closeSidebar.addEventListener('click', closeSidebarPanel);
        overlay.addEventListener('click', closeSidebarPanel);
        newChatBtn.addEventListener('click', createNewChat);
        guideApiBtn.addEventListener('click', showApiGuide);
        closeModalBtn.addEventListener('click', closeModal);
        window.addEventListener('click', (e) => {
            if (e.target === modalGuide) closeModal();
        });
        
        if (!OPENROUTER_API_KEY) {
            setTimeout(() => {
                const ask = confirm("🔐 LeafCy membutuhkan OpenRouter API Key agar bisa berpikir dengan logika sendiri. Ingin memasukkan sekarang?");
                if (ask) promptForApiKey();
                else {
                    addMessageToCurrentChat('assistant', "Halo! Aku LeafCy AI versi Upgrade Dari Sebelumnya! 🚀. Untuk mendapatkan respon cerdas sebenarnya, silakan masukkan API Key dari OpenRouter. Kamu bisa klik tombol 'Cara Ambil API Key' di pojok kanan atas atau klik ikon kunci. 🌟 Jangan malu-malu, nyaww~");
                }
            }, 600);
        } else {
            setTimeout(() => {
                const chat = chats.find(c => c.id === currentChatId);
                if (chat && chat.messages.length === 0) {
                    addMessageToCurrentChat('assistant', "Halo! ✨ Aku LeafCy dengan **Zyrion (Leaf-Ice)** – punya konteks **1 JUTA TOKEN** dan bisa **BACA GAMBAR**! 📷 Aku bisa mengingat percakapan super panjang, membaca foto yang kamu upload, dan memberikan jawaban lebih cerdas, gratis pula! Tanyakan apa pun atau upload foto, nyaww~ 🚀");
                }
            }, 400);
        }
        
        sendBtn.addEventListener('click', sendUserMessage);
        clearBtn.addEventListener('click', resetCurrentChat);
        chatInput.addEventListener('keydown', (e) => {
            if (e.key === 'Enter' && !e.shiftKey) {
                e.preventDefault();
                if (!chatInput.disabled) sendUserMessage();
            }
        });
        chatInput.addEventListener('input', function() {
            this.style.height = 'auto';
            this.style.height = Math.min(130, this.scrollHeight) + 'px';
        });
        chatInput.focus();
        
        apiStatusDiv.style.cursor = 'pointer';
        apiStatusDiv.addEventListener('click', () => {
            promptForApiKey();
            if (OPENROUTER_API_KEY) updateApiStatusUI();
        });
    }
    
    init();
</script>
</body>
</html>
