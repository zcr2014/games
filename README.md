
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>😈 恶作剧</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        html, body {
            width: 100%;
            height: 100%;
            overflow: hidden;
            cursor: none;
        }
        body {
            background: linear-gradient(135deg, #0a0a15 0%, #1a1a2e 50%, #0f3460 100%);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            user-select: none;
        }
        .blocker {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1000;
            pointer-events: all;
        }
        .blocker::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at center, transparent 120px, rgba(0, 0, 0, 0.95) 120px);
        }
        .blocker-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: #e94560;
            font-size: 24px;
            text-align: center;
            pointer-events: none;
            text-shadow: 0 0 20px rgba(233, 69, 96, 0.8);
        }
        .container {
            text-align: center;
            z-index: 10;
            position: relative;
        }
        h1 {
            color: #e94560;
            font-size: 48px;
            margin-bottom: 20px;
            text-shadow: 0 0 30px rgba(233, 69, 96, 0.8);
            animation: pulse 2s infinite;
        }
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }
        .message {
            color: #ffffff;
            font-size: 24px;
            margin-bottom: 40px;
            line-height: 1.6;
        }
        .mic-btn {
            width: 200px;
            height: 200px;
            border-radius: 50%;
            border: none;
            background: linear-gradient(145deg, #e94560, #c73e54);
            cursor: pointer !important;
            display: flex;
            justify-content: center;
            align-items: center;
            box-shadow: 0 0 50px rgba(233, 69, 96, 0.6), 
                        inset 0 -5px 20px rgba(0,0,0,0.3),
                        inset 0 5px 20px rgba(255,255,255,0.2);
            transition: transform 0.3s, box-shadow 0.3s;
            position: relative;
            margin: 0 auto 30px;
            z-index: 1001;
        }
        .mic-btn:hover {
            transform: scale(1.1);
            box-shadow: 0 0 80px rgba(233, 69, 96, 0.8), 
                        inset 0 -5px 20px rgba(0,0,0,0.3),
                        inset 0 5px 20px rgba(255,255,255,0.2);
        }
        .mic-btn.listening {
            animation: listening 1s infinite;
            background: linear-gradient(145deg, #4ecdc4, #3db8b0);
        }
        @keyframes listening {
            0%, 100% { box-shadow: 0 0 50px rgba(78, 205, 196, 0.6); }
            50% { box-shadow: 0 0 100px rgba(78, 205, 196, 1); }
        }
        .mic-icon {
            font-size: 80px;
            color: #ffffff;
        }
        .status {
            color: #a8e6cf;
            font-size: 20px;
            min-height: 30px;
        }
        .hint {
            color: #a8a8a8;
            font-size: 16px;
            margin-top: 20px;
        }
        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }
        .particle {
            position: absolute;
            width: 10px;
            height: 10px;
            background: rgba(233, 69, 96, 0.5);
            border-radius: 50%;
            animation: float 3s infinite ease-in-out;
        }
        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(0deg); opacity: 0.5; }
            50% { transform: translateY(-20px) rotate(180deg); opacity: 1; }
        }
        .success-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 2000;
            flex-direction: column;
        }
        .success-overlay.show {
            display: flex;
            animation: fadeIn 0.5s;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        .success-text {
            color: #4ecdc4;
            font-size: 60px;
            margin-bottom: 30px;
            text-shadow: 0 0 30px rgba(78, 205, 196, 0.8);
        }
        .exit-btn {
            background: linear-gradient(145deg, #4ecdc4, #3db8b0);
            color: #1a1a2e;
            border: none;
            padding: 20px 60px;
            font-size: 24px;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.3s;
        }
        .exit-btn:hover {
            transform: scale(1.1);
        }
        .warning-banner {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            background: linear-gradient(90deg, #e94560, #c73e54);
            color: white;
            padding: 15px;
            text-align: center;
            font-size: 18px;
            z-index: 500;
            box-shadow: 0 5px 20px rgba(0,0,0,0.5);
        }
        .skull {
            position: fixed;
            font-size: 100px;
            opacity: 0.1;
            z-index: 2;
            pointer-events: none;
        }
        .fullscreen-btn {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: rgba(233, 69, 96, 0.8);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 10px;
            cursor: pointer;
            z-index: 600;
            font-size: 16px;
            display: none;
        }
        .custom-cursor {
            position: fixed;
            width: 20px;
            height: 20px;
            background: #e94560;
            border-radius: 50%;
            pointer-events: none;
            z-index: 9999;
            transform: translate(-50%, -50%);
            box-shadow: 0 0 20px #e94560;
            transition: transform 0.1s, background 0.2s, box-shadow 0.2s;
        }
        .custom-cursor.on-btn {
            background: #4ecdc4;
            box-shadow: 0 0 30px #4ecdc4;
            transform: translate(-50%, -50%) scale(1.5);
        }
        .start-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 3000;
            cursor: pointer;
        }
        .start-content {
            text-align: center;
            animation: pulse 2s infinite;
        }
        .start-icon {
            font-size: 150px;
            margin-bottom: 30px;
        }
        .start-content h2 {
            color: #e94560;
            font-size: 48px;
            margin-bottom: 20px;
            text-shadow: 0 0 30px rgba(233, 69, 96, 0.8);
        }
        .start-content p {
            color: #a8e6cf;
            font-size: 24px;
        }
        .escape-warning {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle, #ff0000 0%, #8b0000 50%, #000000 100%);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 10000;
            flex-direction: column;
            animation: flash 0.1s infinite;
            cursor: pointer;
        }
        .escape-warning.show {
            display: flex;
        }
        @keyframes flash {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.8; }
        }
        .escape-warning .emoji {
            font-size: 200px;
            animation: shake-hard 0.1s infinite;
        }
        @keyframes shake-hard {
            0%, 100% { transform: translateX(0) rotate(0deg); }
            25% { transform: translateX(-20px) rotate(-5deg); }
            75% { transform: translateX(20px) rotate(5deg); }
        }
        .escape-warning .text {
            color: #ffffff;
            font-size: 80px;
            font-weight: bold;
            text-shadow: 0 0 50px #ff0000, 0 0 100px #ff0000;
            margin-top: 30px;
            animation: pulse-text 0.2s infinite;
        }
        @keyframes pulse-text {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }
        .escape-warning .subtext {
            color: #ffff00;
            font-size: 36px;
            margin-top: 20px;
        }
        .type-section {
            margin-top: 30px;
            text-align: center;
        }
        .type-input {
            width: 300px;
            padding: 15px 20px;
            font-size: 20px;
            border: 3px solid #e94560;
            border-radius: 10px;
            background: rgba(45, 45, 68, 0.8);
            color: #ffffff;
            outline: none;
            text-align: center;
            z-index: 1001;
            position: relative;
        }
        .type-input::placeholder {
            color: #a8a8a8;
        }
        .type-input:focus {
            border-color: #4ecdc4;
            box-shadow: 0 0 20px rgba(78, 205, 196, 0.5);
        }
        .type-label {
            color: #a8e6cf;
            font-size: 16px;
            margin-bottom: 10px;
        }
        .type-hint {
            color: #a8a8a8;
            font-size: 14px;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="warning-banner">
        ⚠️ 此页面已被锁定！只有说"爸爸"才能离开！所有快捷键已禁用！⚠️
    </div>

    <div class="custom-cursor" id="cursor"></div>
    
    <div class="particles" id="particles"></div>
    
    <div class="skull" style="top: 10%; left: 10%;">💀</div>
    <div class="skull" style="top: 20%; right: 15%;">😈</div>
    <div class="skull" style="bottom: 15%; left: 20%;">👻</div>
    <div class="skull" style="bottom: 25%; right: 10%;">🎃</div>
    
    <div class="container">
        <h1>😈 你被困住了！</h1>
        <p class="message">
            想要离开？没那么容易！<br>
            点击按钮说<span style="color: #e94560; font-weight: bold;">"爸爸"</span>，或者在下面打字！
        </p>
        <button class="mic-btn" id="micBtn" onclick="startListening()">
            <span class="mic-icon">🎤</span>
        </button>
        <p class="status" id="status">点击按钮开始说话</p>
        <p class="hint">💡 提示：请确保浏览器有麦克风权限</p>
        
        <div class="type-section">
            <p class="type-label">或者在这里打字：</p>
            <input type="text" class="type-input" id="typeInput" placeholder="输入'爸爸'然后回车" autocomplete="off">
            <p class="type-hint">按回车确认</p>
        </div>
    </div>

    <div class="blocker" id="blocker">
        <div class="blocker-text" id="blockerText">
            🚫 鼠标被锁定！<br>
            只能点击麦克风按钮！
        </div>
    </div>

    <button class="fullscreen-btn" id="fullscreenBtn" onclick="goFullscreen()">📺 点击进入全屏模式（更难退出）</button>

    <div class="start-overlay" id="startOverlay">
        <div class="start-content">
            <div class="start-icon">😈</div>
            <h2>准备好了吗？</h2>
            <p>点击任意位置开始...</p>
        </div>
    </div>

    <div class="escape-warning" id="escapeWarning">
        <div class="emoji">😡</div>
        <div class="text">别想逃！</div>
        <div class="subtext">👆 点击这里继续！</div>
    </div>

    <div class="success-overlay" id="successOverlay">
        <div class="success-text">🎉 好孩子！</div>
        <p style="color: #ffffff; font-size: 24px; margin-bottom: 30px;">你终于叫了！可以走了~</p>
        <button class="exit-btn" onclick="exitPage()">🚪 离开</button>
    </div>

    <script>
        let isListening = false;
        let recognition = null;
        let success = false;
        let fullscreenActive = false;

        const cursor = document.getElementById('cursor');
        const micBtn = document.getElementById('micBtn');
        const blocker = document.getElementById('blocker');
        const blockerText = document.getElementById('blockerText');
        const startOverlay = document.getElementById('startOverlay');

        function createParticles() {
            const container = document.getElementById('particles');
            for (let i = 0; i < 50; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                particle.style.left = Math.random() * 100 + '%';
                particle.style.top = Math.random() * 100 + '%';
                particle.style.animationDelay = Math.random() * 3 + 's';
                particle.style.width = (Math.random() * 10 + 5) + 'px';
                particle.style.height = particle.style.width;
                container.appendChild(particle);
            }
        }
        createParticles();

        startOverlay.addEventListener('click', function() {
            startOverlay.style.display = 'none';
            goFullscreen();
        });

        document.addEventListener('mousemove', function(e) {
            cursor.style.left = e.clientX + 'px';
            cursor.style.top = e.clientY + 'px';

            const micRect = micBtn.getBoundingClientRect();
            const micCenterX = micRect.left + micRect.width / 2;
            const micCenterY = micRect.top + micRect.height / 2;
            const micDistance = Math.sqrt(Math.pow(e.clientX - micCenterX, 2) + Math.pow(e.clientY - micCenterY, 2));

            const typeInput = document.getElementById('typeInput');
            const inputRect = typeInput.getBoundingClientRect();
            const isOverInput = e.clientX >= inputRect.left && e.clientX <= inputRect.right &&
                               e.clientY >= inputRect.top && e.clientY <= inputRect.bottom;

            if (micDistance < 120 || isOverInput) {
                cursor.classList.add('on-btn');
                blocker.style.display = 'none';
            } else {
                cursor.classList.remove('on-btn');
                if (!success) {
                    blocker.style.display = 'block';
                }
            }
        });

        blocker.addEventListener('click', function(e) {
            e.preventDefault();
            e.stopPropagation();
            
            const messages = [
                '🚫 别挣扎了！',
                '😈 逃不掉的！',
                '💀 快叫爸爸！',
                '👻 你被困住了！',
                '🎃 放弃抵抗吧！'
            ];
            blockerText.innerHTML = messages[Math.floor(Math.random() * messages.length)] + '<br>只能点击麦克风按钮！';
            
            blocker.style.animation = 'none';
            blocker.offsetHeight;
            blocker.style.animation = 'shake 0.3s';
        });

        document.head.insertAdjacentHTML('beforeend', `
            <style>
                @keyframes shake {
                    0%, 100% { transform: translateX(0); }
                    25% { transform: translateX(-10px); }
                    75% { transform: translateX(10px); }
                }
            </style>
        `);

        function goFullscreen() {
            if (success) return;
            
            const elem = document.documentElement;
            let promise;
            
            if (elem.requestFullscreen) {
                promise = elem.requestFullscreen();
            } else if (elem.webkitRequestFullscreen) {
                promise = elem.webkitRequestFullscreen();
            } else if (elem.mozRequestFullScreen) {
                promise = elem.mozRequestFullScreen();
            } else if (elem.msRequestFullscreen) {
                promise = elem.msRequestFullscreen();
            }
            
            fullscreenActive = true;
            document.getElementById('fullscreenBtn').style.display = 'none';
            
            return promise;
        }

        let escapeWarningShown = false;
        let fullscreenCheckEnabled = true;

        function forceFullscreen() {
            if (success) return;
            if (!fullscreenCheckEnabled) return;
            
            const isFullscreen = document.fullscreenElement || 
                                document.webkitFullscreenElement || 
                                document.mozFullScreenElement || 
                                document.msFullscreenElement;
            
            if (!isFullscreen && fullscreenActive) {
                if (!escapeWarningShown) {
                    showEscapeWarning();
                }
            }
        }

        function showEscapeWarning() {
            escapeWarningShown = true;
            fullscreenCheckEnabled = false;
            
            const warning = document.getElementById('escapeWarning');
            warning.classList.add('show');
            playAlarmSound();
            
            const clickHandler = function() {
                warning.classList.remove('show');
                escapeWarningShown = false;
                fullscreenCheckEnabled = true;
                warning.removeEventListener('click', clickHandler);
                goFullscreen();
            };
            
            warning.addEventListener('click', clickHandler);
            
            warning.querySelector('.subtext').textContent = '点击这里或说"爸爸"才能离开！';
        }

        function playAlarmSound() {
            try {
                const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                
                const oscillator1 = audioContext.createOscillator();
                const oscillator2 = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                
                oscillator1.connect(gainNode);
                oscillator2.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                oscillator1.frequency.value = 800;
                oscillator2.frequency.value = 600;
                oscillator1.type = 'square';
                oscillator2.type = 'sawtooth';
                
                gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.3);
                
                oscillator1.start(audioContext.currentTime);
                oscillator2.start(audioContext.currentTime);
                oscillator1.stop(audioContext.currentTime + 0.3);
                oscillator2.stop(audioContext.currentTime + 0.3);
            } catch (e) {
                console.log('Audio not supported');
            }
        }

        function startListening() {
            if (isListening) return;

            if (!('webkitSpeechRecognition' in window) && !('SpeechRecognition' in window)) {
                document.getElementById('status').textContent = '❌ 你的浏览器不支持语音识别，请使用Chrome或Edge';
                return;
            }

            const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
            recognition = new SpeechRecognition();
            recognition.lang = 'zh-CN';
            recognition.continuous = true;
            recognition.interimResults = true;
            recognition.maxAlternatives = 5;

            isListening = true;
            const status = document.getElementById('status');
            
            micBtn.classList.add('listening');
            status.textContent = '🎧 正在听...请大声说"爸爸"';

            let lastTranscript = '';
            let attempts = 0;

            recognition.onresult = function(event) {
                let finalTranscript = '';
                let interimTranscript = '';

                for (let i = event.resultIndex; i < event.results.length; i++) {
                    const transcript = event.results[i][0].transcript;
                    if (event.results[i].isFinal) {
                        finalTranscript += transcript;
                    } else {
                        interimTranscript += transcript;
                    }
                }

                const currentTranscript = finalTranscript || interimTranscript;
                
                if (currentTranscript && currentTranscript !== lastTranscript) {
                    lastTranscript = currentTranscript;
                    status.textContent = '你说: "' + currentTranscript + '"';
                    
                    const keywords = [
                        '爸爸', '粑粑', 'baba', 'father', 'dad', 
                        '爹', '爹地', 'papa', 'pa', '爸',
                        '把把', '霸霸', '八八', 'ba ba'
                    ];
                    
                    const lowerTranscript = currentTranscript.toLowerCase();
                    let matched = false;
                    
                    for (const keyword of keywords) {
                        if (lowerTranscript.includes(keyword.toLowerCase())) {
                            matched = true;
                            break;
                        }
                    }
                    
                    if (!matched) {
                        for (let i = 0; i < currentTranscript.length - 1; i++) {
                            if (currentTranscript[i] === '爸' && currentTranscript[i + 1] === '爸') {
                                matched = true;
                                break;
                            }
                        }
                    }
                    
                    if (matched) {
                        recognition.stop();
                        onSuccess();
                    } else {
                        attempts++;
                        if (attempts >= 3) {
                            status.textContent = '❌ 不对！要说"爸爸"！再试一次！';
                            attempts = 0;
                        }
                    }
                }
            };

            recognition.onerror = function(event) {
                if (event.error === 'no-speech') {
                    status.textContent = '🎤 没检测到声音，请大声说！';
                } else if (event.error === 'audio-capture') {
                    status.textContent = '❌ 请允许麦克风权限！';
                } else if (event.error === 'not-allowed') {
                    status.textContent = '❌ 麦克风被禁止！请在浏览器设置中允许！';
                } else {
                    status.textContent = '❌ 错误: ' + event.error + ' - 请重试';
                }
                micBtn.classList.remove('listening');
                isListening = false;
            };

            recognition.onend = function() {
                if (isListening && !success) {
                    micBtn.classList.remove('listening');
                    isListening = false;
                    document.getElementById('status').textContent = '没听清？点击按钮再试一次~';
                }
            };

            try {
                recognition.start();
            } catch (e) {
                status.textContent = '❌ 启动失败，请重试';
                isListening = false;
                micBtn.classList.remove('listening');
            }
        }

        function onSuccess() {
            success = true;
            isListening = false;
            micBtn.classList.remove('listening');
            document.getElementById('status').textContent = '✅ 正确！';
            blocker.style.display = 'none';
            document.getElementById('fullscreenBtn').style.display = 'none';
            
            if (document.exitFullscreen) {
                document.exitFullscreen();
            } else if (document.webkitExitFullscreen) {
                document.webkitExitFullscreen();
            } else if (document.msExitFullscreen) {
                document.msExitFullscreen();
            }
            
            setTimeout(() => {
                document.getElementById('successOverlay').classList.add('show');
            }, 500);
        }

        function exitPage() {
            window.onbeforeunload = null;
            window.close();
            
            setTimeout(() => {
                document.body.innerHTML = '<div style="display:flex;justify-content:center;align-items:center;height:100vh;background:#1a1a2e;color:#4ecdc4;font-size:24px;text-align:center;flex-direction:column;">✅ 你可以关闭这个标签页了<br><br><button onclick="window.close()" style="background:#4ecdc4;color:#1a1a2e;border:none;padding:15px 40px;font-size:20px;border-radius:10px;cursor:pointer;">关闭页面</button></div>';
            }, 100);
        }

        function checkTypeInput() {
            const input = document.getElementById('typeInput');
            const value = input.value.trim().toLowerCase();
            
            const keywords = [
                '爸爸', '粑粑', 'baba', 'father', 'dad', 
                '爹', '爹地', 'papa', 'pa', '爸',
                '把把', '霸霸', '八八', 'ba ba',
                'daddy', 'papi', 'baba'
            ];
            
            for (const keyword of keywords) {
                if (value.includes(keyword.toLowerCase())) {
                    onSuccess();
                    return true;
                }
            }
            
            return false;
        }

        document.getElementById('typeInput').addEventListener('keydown', function(e) {
            if (e.key === 'Enter') {
                e.preventDefault();
                e.stopPropagation();
                
                if (!checkTypeInput()) {
                    this.value = '';
                    this.style.borderColor = '#e94560';
                    this.placeholder = '❌ 不对！再试一次！';
                    
                    setTimeout(() => {
                        this.style.borderColor = '#e94560';
                        this.placeholder = "输入'爸爸'然后回车";
                    }, 1000);
                }
            }
        });

        document.getElementById('typeInput').addEventListener('focus', function() {
            this.style.borderColor = '#4ecdc4';
        });

        document.getElementById('typeInput').addEventListener('blur', function() {
            this.style.borderColor = '#e94560';
        });

        window.onbeforeunload = function(e) {
            if (!success) {
                e.preventDefault();
                e.returnValue = '😈 你必须说"爸爸"才能离开！';
                return '😈 你必须说"爸爸"才能离开！';
            }
        };

        document.addEventListener('contextmenu', e => e.preventDefault());

        document.addEventListener('keydown', function(e) {
            if (success) return;
            
            const typeInput = document.getElementById('typeInput');
            const isTyping = document.activeElement === typeInput;
            
            if (isTyping) {
                if (e.key === 'Escape') {
                    e.preventDefault();
                    typeInput.blur();
                    return false;
                }
                return;
            }
            
            e.preventDefault();
            e.stopPropagation();
            
            if (e.key === 'Escape' || e.keyCode === 27) {
                e.preventDefault();
                e.stopPropagation();
                return false;
            }
            if (e.key === 'F4' && e.altKey) return false;
            if (e.key === 'w' && e.ctrlKey) return false;
            if (e.key === 'F11') return false;
            if (e.key === 'F12') return false;
            if (e.key === 'Tab') return false;
            if (e.key === 'u' && e.ctrlKey) return false;
            if (e.key === 's' && e.ctrlKey) return false;
            if (e.key === 'p' && e.ctrlKey) return false;
            if (e.key === 'h' && e.ctrlKey) return false;
            if (e.key === 'j' && e.ctrlKey) return false;
            if (e.key === 'k' && e.ctrlKey) return false;
            if (e.key === 'l' && e.ctrlKey) return false;
            if (e.key === 'r' && e.ctrlKey) return false;
            if (e.key === 'd' && e.ctrlKey) return false;
            if (e.key === 'g' && e.ctrlKey) return false;
            if (e.key === 'i' && e.ctrlKey && e.shiftKey) return false;
            
            return false;
        });

        document.addEventListener('keyup', function(e) {
            if (e.key === 'Escape' || e.keyCode === 27) {
                e.preventDefault();
                e.stopPropagation();
                return false;
            }
        });

        document.addEventListener('keypress', function(e) {
            if (e.key === 'Escape' || e.keyCode === 27) {
                e.preventDefault();
                e.stopPropagation();
                return false;
            }
        });

        window.addEventListener('keydown', function(e) {
            if (e.key === 'Escape' || e.keyCode === 27) {
                e.preventDefault();
                e.stopPropagation();
                return false;
            }
        });

        function initFullscreenLock() {
            document.addEventListener('fullscreenchange', forceFullscreen);
            document.addEventListener('webkitfullscreenchange', forceFullscreen);
            document.addEventListener('mozfullscreenchange', forceFullscreen);
            document.addEventListener('MSFullscreenChange', forceFullscreen);
            
            setInterval(forceFullscreen, 50);
            
            function aggressiveFullscreenCheck() {
                if (!success && fullscreenActive) {
                    forceFullscreen();
                    requestAnimationFrame(aggressiveFullscreenCheck);
                }
            }
            requestAnimationFrame(aggressiveFullscreenCheck);
        }
        initFullscreenLock();

        setInterval(() => {
            if (!success && !document.hidden) {
                const warnings = [
                    '⚠️ 此页面已被锁定！只有说"爸爸"才能离开！',
                    '😈 别想逃跑！快叫爸爸！',
                    '💀 你逃不掉的！',
                    '👻 我们在看着你...'
                ];
                document.querySelector('.warning-banner').textContent = warnings[Math.floor(Math.random() * warnings.length)];
            }
        }, 3000);
    </script>
</body>
</html>
