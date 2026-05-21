<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>LeafCy AI | Leafia AI - Dual Mode</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
            font-family: 'Inter', system-ui, -apple-system, sans-serif;
            height: 100vh;
            overflow: hidden;
            display: flex;
            flex-direction: column;
        }
        .switch-bar {
            background: #0f0f1a;
            padding: 8px 20px;
            display: flex;
            justify-content: flex-end;
            align-items: center;
            gap: 12px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
            flex-shrink: 0;
        }
        .switch-btn {
            background: linear-gradient(135deg, #2ecc71, #27ae60);
            border: none;
            padding: 8px 20px;
            border-radius: 40px;
            color: white;
            font-weight: 600;
            font-size: 0.85rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            transition: all 0.2s ease;
            font-family: inherit;
        }
        .switch-btn:hover {
            transform: scale(1.02);
            opacity: 0.9;
        }
        .current-mode {
            background: rgba(255,255,255,0.1);
            padding: 4px 12px;
            border-radius: 30px;
            font-size: 0.7rem;
            color: #aaa;
        }
        .iframe-container {
            flex: 1;
            width: 100%;
            position: relative;
            background: #fff;
        }
        iframe {
            width: 100%;
            height: 100%;
            border: none;
            display: block;
        }
        @media (max-width: 600px) {
            .switch-bar { padding: 6px 12px; }
            .switch-btn { padding: 6px 14px; font-size: 0.75rem; }
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,400;14..32,500;14..32,600;14..32,700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
</head>
<body>
<div class="switch-bar">
    <div class="current-mode" id="currentModeBadge"><i class="fas fa-leaf"></i> Mode: LeafCy</div>
    <button class="switch-btn" id="switchBtn"><i class="fas fa-exchange-alt"></i> Switch To Leafia [FREE]</button>
</div>
<div class="iframe-container">
    <iframe id="mainFrame" src="LeafCy.html" title="AI Assistant"></iframe>
</div>

<script>
    const iframe = document.getElementById('mainFrame');
    const switchBtn = document.getElementById('switchBtn');
    const currentModeBadge = document.getElementById('currentModeBadge');
    
    let currentMode = 'leafcy';
    
    // Listen for messages from iframe (when Leafia clicks "Balik Ke LeafCy")
    window.addEventListener('message', function(event) {
        if (event.data === 'switchToWebsite1') {
            if (currentMode === 'leafia') {
                iframe.src = 'LeafCy.html';
                currentMode = 'leafcy';
                currentModeBadge.innerHTML = '<i class="fas fa-leaf"></i> Mode: LeafCy';
                switchBtn.innerHTML = '<i class="fas fa-exchange-alt"></i> Switch To Leafia [FREE]';
                switchBtn.style.background = 'linear-gradient(135deg, #2ecc71, #27ae60)';
            }
        }
    });
    
    switchBtn.addEventListener('click', function() {
        if (currentMode === 'leafcy') {
            iframe.src = 'my1.html';
            currentMode = 'leafia';
            currentModeBadge.innerHTML = '<i class="fas fa-feather-alt"></i> Mode: Leafia';
            switchBtn.innerHTML = '<i class="fas fa-exchange-alt"></i> Balik Ke LeafCy [LIMITED]';
            switchBtn.style.background = 'linear-gradient(135deg, #f06292, #4fc3f7)';
        } else {
            iframe.src = 'LeafCy.html';
            currentMode = 'leafcy';
            currentModeBadge.innerHTML = '<i class="fas fa-leaf"></i> Mode: LeafCy';
            switchBtn.innerHTML = '<i class="fas fa-exchange-alt"></i> Switch To Leafia [FREE]';
            switchBtn.style.background = 'linear-gradient(135deg, #2ecc71, #27ae60)';
        }
    });
</script>
</body>
</html>
