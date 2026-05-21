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

        /* ===== TOP BAR ===== */
        .switch-bar{
            width:100%;
            display:flex;
            align-items:center;
            justify-content:space-between;
            gap:12px;

            padding:
                calc(env(safe-area-inset-top) + 10px)
                14px
                10px
                14px;

            background:rgba(10,10,20,0.92);
            backdrop-filter:blur(12px);

            border-bottom:1px solid rgba(255,255,255,0.08);

            position:sticky;
            top:0;
            z-index:999;
            flex-shrink:0;
        }

        .current-mode{
            display:flex;
            align-items:center;
            gap:8px;

            background:rgba(255,255,255,0.08);

            color:#f1f5f9;

            padding:10px 16px;
            border-radius:18px;

            font-size:0.95rem;
            font-weight:600;

            min-height:52px;
            flex:1;
        }

        .switch-btn{
            border:none;
            outline:none;

            min-height:52px;

            padding:12px 18px;

            border-radius:18px;

            background:linear-gradient(135deg,#2ecc71,#27ae60);

            color:white;
            font-size:0.9rem;
            font-weight:700;

            display:flex;
            align-items:center;
            justify-content:center;
            gap:10px;

            cursor:pointer;

            transition:0.2s ease;

            flex:1.2;

            box-shadow:
                0 4px 15px rgba(46,204,113,0.25);
        }

        .switch-btn:active{
            transform:scale(0.97);
        }

        /* ===== IFRAME ===== */
        .iframe-container{
            flex:1;
            width:100%;
            height:100%;
            overflow:hidden;
            position:relative;
        }

        iframe{
            width:100%;
            height:100%;
            border:none;
            display:block;
            background:white;
        }

        /* ===== MOBILE FIX ===== */
        @media (max-width:700px){

            .switch-bar{
                flex-direction:column;
                align-items:stretch;
                gap:10px;
            }

            .current-mode,
            .switch-btn{
                width:100%;
            }

            .current-mode{
                justify-content:center;
                text-align:center;
                font-size:1rem;
            }

            .switch-btn{
                font-size:1rem;
                padding:14px 16px;
            }
        }

        /* ===== EXTRA SMALL PHONE ===== */
        @media (max-width:420px){

            .current-mode{
                font-size:0.92rem;
                padding:12px;
            }

            .switch-btn{
                font-size:0.92rem;
            }
        }
    </style>
</head>

<body>

    <!-- TOP CONTROL -->
    <div class="switch-bar">

        <div class="current-mode" id="currentModeBadge">
            <i class="fas fa-leaf"></i>
            <span>Mode: LeafCy</span>
        </div>

        <button class="switch-btn" id="switchBtn">
            <i class="fas fa-exchange-alt"></i>
            <span>Switch To Leafia [FREE]</span>
        </button>

    </div>

    <!-- MAIN SCREEN -->
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

        // ===== LISTEN FROM IFRAME =====
        window.addEventListener('message', function(event){

            if(event.data === 'switchToWebsite1'){

                if(currentMode === 'leafia'){

                    iframe.src = 'LeafCy.html';

                    currentMode = 'leafcy';

                    currentModeBadge.innerHTML = `
                        <i class="fas fa-leaf"></i>
                        <span>Mode: LeafCy</span>
                    `;

                    switchBtn.innerHTML = `
                        <i class="fas fa-exchange-alt"></i>
                        <span>Switch To Leafia [FREE]</span>
                    `;

                    switchBtn.style.background =
                        'linear-gradient(135deg,#2ecc71,#27ae60)';
                }
            }
        });

        // ===== SWITCH BUTTON =====
        switchBtn.addEventListener('click', function(){

            if(currentMode === 'leafcy'){

                iframe.src = 'my1.html';

                currentMode = 'leafia';

                currentModeBadge.innerHTML = `
                    <i class="fas fa-feather-alt"></i>
                    <span>Mode: Leafia</span>
                `;

                switchBtn.innerHTML = `
                    <i class="fas fa-exchange-alt"></i>
                    <span>Balik Ke LeafCy [LIMITED]</span>
                `;

                switchBtn.style.background =
                    'linear-gradient(135deg,#f06292,#4fc3f7)';

            } else {

                iframe.src = 'LeafCy.html';

                currentMode = 'leafcy';

                currentModeBadge.innerHTML = `
                    <i class="fas fa-leaf"></i>
                    <span>Mode: LeafCy</span>
                `;

                switchBtn.innerHTML = `
                    <i class="fas fa-exchange-alt"></i>
                    <span>Switch To Leafia [FREE]</span>
                `;

                switchBtn.style.background =
                    'linear-gradient(135deg,#2ecc71,#27ae60)';
            }
        });
    </script>

</body>
</html>
