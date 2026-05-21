<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover, user-scalable=no" />
    <title>LeafCy AI | Leafia AI - Dual Mode</title>

    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">

    <style>
        *{
            margin:0;
            padding:0;
            box-sizing:border-box;
        }

        html,body{
            width:100%;
            height:100%;
            overflow:hidden;
            font-family:'Inter',system-ui,sans-serif;
            background:#111827;
        }

        body{
            display:flex;
            flex-direction:column;

            background:
                radial-gradient(circle at top left, #1f3b73 0%, transparent 35%),
                linear-gradient(135deg, #0f172a 0%, #16213e 100%);
        }

        /* ===== MINI TOP BAR ===== */
        .switch-bar{
            position:fixed;
            top:10px;
            left:10px;
            right:10px;

            z-index:9999;

            display:flex;
            justify-content:space-between;
            align-items:center;

            pointer-events:none;
        }

        /* ===== MODE BADGE ===== */
        .current-mode{
            pointer-events:auto;

            display:flex;
            align-items:center;
            gap:6px;

            background:rgba(15,15,25,0.78);
            backdrop-filter:blur(10px);

            color:white;

            padding:8px 12px;

            border-radius:999px;

            font-size:0.78rem;
            font-weight:600;

            border:1px solid rgba(255,255,255,0.08);

            box-shadow:
                0 4px 14px rgba(0,0,0,0.22);
        }

        /* ===== SWITCH BUTTON ===== */
        .switch-btn{
            pointer-events:auto;

            border:none;
            outline:none;

            background:
                linear-gradient(135deg,#2ecc71,#27ae60);

            color:white;

            padding:9px 14px;

            border-radius:999px;

            font-size:0.78rem;
            font-weight:700;

            display:flex;
            align-items:center;
            gap:7px;

            cursor:pointer;

            transition:0.18s ease;

            box-shadow:
                0 4px 14px rgba(46,204,113,0.28);
        }

        .switch-btn:active{
            transform:scale(0.95);
        }

        /* ===== IFRAME ===== */
        .iframe-container{
            width:100%;
            height:100vh;
            overflow:hidden;
        }

        iframe{
            width:100%;
            height:100%;
            border:none;
            display:block;
            background:white;
        }

        /* ===== MOBILE ===== */
        @media (max-width:480px){

            .switch-bar{
                top:8px;
                left:8px;
                right:8px;
            }

            .current-mode{
                font-size:0.72rem;
                padding:7px 10px;
            }

            .switch-btn{
                font-size:0.72rem;
                padding:8px 11px;
            }
        }
    </style>
</head>

<body>

    <!-- MINI FLOAT TOP -->
    <div class="switch-bar">

        <div class="current-mode" id="currentModeBadge">
            <i class="fas fa-leaf"></i>
            <span>LeafCy</span>
        </div>

        <button class="switch-btn" id="switchBtn">
            <i class="fas fa-exchange-alt"></i>
            <span>Leafia</span>
        </button>

    </div>

    <!-- FULLSCREEN APP -->
    <div class="iframe-container">
        <iframe
            id="mainFrame"
            src="LeafCy.html"
            title="AI Assistant">
        </iframe>
    </div>

    <script>
        const iframe = document.getElementById('mainFrame');
        const switchBtn = document.getElementById('switchBtn');
        const currentModeBadge = document.getElementById('currentModeBadge');

        let currentMode = 'leafcy';

        // ===== MESSAGE FROM IFRAME =====
        window.addEventListener('message', function(event){

            if(event.data === 'switchToWebsite1'){

                if(currentMode === 'leafia'){

                    iframe.src = 'LeafCy.html';

                    currentMode = 'leafcy';

                    currentModeBadge.innerHTML = `
                        <i class="fas fa-leaf"></i>
                        <span>LeafCy</span>
                    `;

                    switchBtn.innerHTML = `
                        <i class="fas fa-exchange-alt"></i>
                        <span>Leafia</span>
                    `;

                    switchBtn.style.background =
                        'linear-gradient(135deg,#2ecc71,#27ae60)';
                }
            }
        });

        // ===== SWITCH MODE =====
        switchBtn.addEventListener('click', function(){

            if(currentMode === 'leafcy'){

                iframe.src = 'my1.html';

                currentMode = 'leafia';

                currentModeBadge.innerHTML = `
                    <i class="fas fa-feather-alt"></i>
                    <span>Leafia</span>
                `;

                switchBtn.innerHTML = `
                    <i class="fas fa-exchange-alt"></i>
                    <span>LeafCy</span>
                `;

                switchBtn.style.background =
                    'linear-gradient(135deg,#f06292,#4fc3f7)';

            } else {

                iframe.src = 'LeafCy.html';

                currentMode = 'leafcy';

                currentModeBadge.innerHTML = `
                    <i class="fas fa-leaf"></i>
                    <span>LeafCy</span>
                `;

                switchBtn.innerHTML = `
                    <i class="fas fa-exchange-alt"></i>
                    <span>Leafia</span>
                `;

                switchBtn.style.background =
                    'linear-gradient(135deg,#2ecc71,#27ae60)';
            }
        });
    </script>

</body>
</html>
