<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>V-ULTIMA TIER 12 VIP - BOSS LÊ ĐỨC BAN</title>
    <style>
        :root { --r: #f00; --n: #0f0; --cyan: #00ffff; --purple: #bc13fe; --glow: #9d00ff; }
        * { box-sizing: border-box; font-family: 'Courier New', monospace; margin: 0; padding: 0; outline: none; -webkit-tap-highlight-color: transparent; }
        body { background: #000; color: #fff; overflow: hidden; height: 100vh; width: 100vw; }
        #matrix-canvas { position: fixed; inset: 0; z-index: 1; opacity: 0.5; pointer-events: none; }
        .system-container { position: relative; z-index: 10; width: 100%; height: 100%; display: flex; justify-content: center; align-items: center; pointer-events: none; }
        .hub { pointer-events: auto; background: rgba(10, 0, 25, 0.92); border: 4px solid var(--purple); border-radius: 45px; padding: 30px; text-align: center; box-shadow: 0 0 60px var(--glow); width: 95%; max-width: 440px; position: relative; backdrop-filter: blur(5px); }
        .layer { display: none; width: 100%; flex-direction: column; align-items: center; }
        .title-neon { color: #ffeb3b; font-size: 20px; font-weight: 900; margin-bottom: 25px; text-transform: uppercase; letter-spacing: 2px; }
        .inp-boss { width: 100%; padding: 18px; background: rgba(0,0,0,0.8); border: 3px solid #333; border-radius: 20px; color: #fff; font-size: 16px; text-align: center; margin-bottom: 15px; box-shadow: inset 0 0 10px #000; }
        .btn-confirm { background: var(--purple); color: #fff; border: none; border-radius: 25px; padding: 18px; width: 100%; font-weight: 900; font-size: 18px; cursor: pointer; text-transform: uppercase; box-shadow: 0 0 25px var(--glow); }
        #login-error { color: var(--r); font-weight: 900; font-size: 13px; margin-top: 15px; display: none; }
        #res-display { font-size: 85px; font-weight: 950; margin: 5px 0 0 0; text-shadow: 0 0 40px var(--purple); }
        #md5-display { font-size: 10px; color: var(--cyan); margin-bottom: 15px; word-break: break-all; opacity: 0.8; }
        .history-grid { display: grid; grid-template-columns: repeat(5, 1fr); gap: 8px; margin-top: 20px; }
        .h-box { background: rgba(255,255,255,0.05); border: 1.5px solid var(--purple); border-radius: 8px; padding: 8px; font-size: 12px; font-weight: bold; }
        .admin-box { background: #fff; color: #000; border-radius: 10px; padding: 15px; width: 100%; overflow: hidden; margin-top: 10px; box-shadow: 0 0 20px #fff; }
        .admin-header { display: flex; justify-content: space-between; align-items: center; color: var(--purple); font-weight: 900; font-size: 12px; margin-bottom: 10px; border-bottom: 2px dashed #000; padding-bottom: 5px; }
        .create-user-section { border: 1.5px dashed #000; padding: 10px; margin-bottom: 10px; display: flex; gap: 5px; }
        .create-user-section input { border: 1px solid #000; padding: 5px; font-size: 11px; width: 35%; color: #000; }
        .btn-create { background: #008000; color: #fff; border: none; padding: 5px 10px; border-radius: 5px; font-weight: 900; cursor: pointer; }
        table { width: 100%; border-collapse: collapse; font-size: 9px; font-weight: 900; }
        th, td { border: 1px solid #000; padding: 6px; text-align: center; }
        .status-on { color: #008000; }
        .status-off { color: #ff0000; }
        .btn-kick-admin { background: #ff0000; color: #fff; border: none; padding: 5px; border-radius: 4px; width: 100%; cursor: pointer; }
        .footer-marquee { position: fixed; bottom: 0; width: 100%; background: #000; border-top: 2px solid var(--r); padding: 6px 0; z-index: 1000; }
        .marquee-txt { display: inline-block; white-space: nowrap; color: var(--r); font-weight: 900; font-size: 13px; animation: scroll 15s linear infinite; text-transform: uppercase; }
        @keyframes scroll { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
        .nav-admin { display: flex; justify-content: space-around; margin-bottom: 15px; }
        .nav-admin span { cursor: pointer; padding: 5px 15px; border-radius: 15px; background: #222; font-size: 11px; border: 1px solid var(--purple); }
        .nav-admin .active { background: var(--purple); box-shadow: 0 0 10px var(--purple); }
        .edit-link { cursor: pointer !important; color: blue !important; text-decoration: underline !important; font-weight: 900; }
        #expired-overlay { display: none; position: absolute; inset: 0; background: rgba(0,0,0,0.95); z-index: 100; border-radius: 45px; justify-content: center; align-items: center; flex-direction: column; padding: 20px; }
        #countdown-box { color: #ffeb3b; font-size: 14px; font-weight: bold; margin-top: 5px; text-shadow: 0 0 10px rgba(255, 235, 59, 0.5); }
    </style>
</head>
<body onload="initSystem()">
    <canvas id="matrix-canvas"></canvas>
    <div class="system-container">
        <div id="scr-login" class="layer" style="display: flex;">
            <div class="hub">
                <div class="title-neon">V-ULTIMA OMNIPOTENCE</div>
                <input type="text" id="login-u" class="inp-boss" placeholder="NHẬP TÊN CHIẾN BINH...">
                <input type="password" id="login-p" class="inp-boss" placeholder="MẬT MÃ TRUY CẬP...">
                <button class="btn-confirm" onclick="processLogin()">XÁC THỰC HỆ THỐNG</button>
                <div id="login-error">TRUY CẬP BỊ TỪ CHỐI - SAI MẬT MÃ</div>
            </div>
        </div>

        <div id="scr-main" class="layer">
            <div class="hub" id="main-hub">
                <div id="expired-overlay">
                    <h2 style="color:red; font-weight:900;">HẾT THỜI GIAN CHIẾN ĐẤU</h2>
                    <p style="margin-top:15px; font-size:14px;">LIÊN HỆ BOSS LÊ ĐỨC BAN ĐỂ GIA HẠN</p>
                    <button class="btn-confirm" onclick="logout()" style="margin-top:20px;">QUAY LẠI</button>
                </div>
                <div class="nav-admin">
                    <span id="tab1" class="active" onclick="toggleView(1)">PHÂN TÍCH MD5</span>
                    <span id="tab2" onclick="toggleView(2)">QUẢN TRỊ TỐI CAO</span>
                </div>
                
                <div id="view-tool">
                    <div id="boss-title" style="color:#ffeb3b; font-weight:900; font-size: 14px;">CHIẾN BINH: <span id="user-name-display">...</span> [TIER 12]</div>
                    <div id="countdown-box">THỜI GIAN: ĐANG ĐỒNG BỘ...</div>
                    <div id="res-display">READY</div>
                    <div id="md5-display">CHỜ MÃ CHIẾN TRƯỜNG</div>
                    <input type="text" id="md5-inp" class="inp-boss" placeholder="DÁN MÃ MD5 TẠI ĐÂY" maxlength="32" oninput="validateMD5(this)">
                    <button class="btn-confirm" id="btn-analyst" onclick="handleTool()">PHÂN TÍCH & BẺ CẦU</button>
                    <div id="hand-progress" style="margin-top:10px; color:var(--cyan); font-weight:bold; font-size: 12px;">TIẾN TRÌNH: 0/10 TAY</div>
                    <div class="history-grid" id="history-list">
                        <div class="h-box">-</div><div class="h-box">-</div><div class="h-box">-</div><div class="h-box">-</div><div class="h-box">-</div>
                    </div>
                </div>

                <div id="view-admin" style="display: none;">
                    <div class="admin-box">
                        <div class="admin-header">
                            <span>BẢNG ĐIỀU KHIỂN BOSS BAN</span>
                            <button onclick="logout()" style="background:red; color:#fff; border:none; padding:2px 8px; border-radius:4px; font-weight:900;">LOGOUT</button>
                        </div>
                        <div class="create-user-section">
                            <input type="text" id="new-user" placeholder="User">
                            <input type="text" id="new-pass" placeholder="Pass">
                            <button class="btn-create" onclick="addNewUser()">TẠO</button>
                        </div>
                        <table id="user-table">
                            <thead>
                                <tr>
                                    <th>STT</th><th>USER</th><th>PASS</th><th>GIỜ</th><th>STATUS</th><th>TOOL</th>
                                </tr>
                            </thead>
                            <tbody id="user-list-body"></tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="footer-marquee">
        <div class="marquee-txt">V-ULTIMA OMNIPOTENCE: TRẠNG THÁI SẴN SÀNG CHIẾN ĐẤU... GHOST MODE ACTIVE... ĐANG ĐÁNH SẬP NHÀ CÁI... ĐƯA BOSS LEE DUC BAN LÊN ĐỈNH CAO...</div>
    </div>

    <script>
        let currentBoss = "";
        let toolHistory = [];
        let lastMd5 = "";
        let timerInterval = null;
        let lastSyncTime = Date.now();
        
        // KHỞI TẠO HỆ THỐNG VỚI 3 TÀI KHOẢN MẶC ĐỊNH
        const defaultUsers = [
            {id: 1, u: 'admin', p: '230078', role: 'boss', status: 'offline', expiry: '999999'},
            {id: 2026, u: '2026', p: '2026', role: 'user', status: 'offline', expiry: '24'},
            {id: 777, u: 'anhban', p: '123', role: 'user', status: 'offline', expiry: '24'}
        ];

        let userDatabase = JSON.parse(localStorage.getItem('vData')) || defaultUsers;

        // KIỂM TRA VÀ BẢO VỆ TÀI KHOẢN MẶC ĐỊNH KHÔNG BỊ MẤT
        function syncDefaults() {
            defaultUsers.forEach(def => {
                if (!userDatabase.find(x => x.u === def.u)) {
                    userDatabase.push(def);
                }
            });
            saveData();
        }
        syncDefaults();

        function validateMD5(input) {
            input.value = input.value.replace(/[^0-9a-fA-F]/g, '').toLowerCase();
        }

        function startGlobalTimer() {
            if (timerInterval) clearInterval(timerInterval);
            lastSyncTime = Date.now();
            timerInterval = setInterval(() => {
                let user = userDatabase.find(x => x.u === currentBoss);
                if (user && user.role !== 'boss') {
                    let now = Date.now();
                    let deltaTime = (now - lastSyncTime) / 1000;
                    lastSyncTime = now;
                    let hours = parseFloat(user.expiry);
                    if (hours > 0) {
                        hours -= (deltaTime / 3600);
                        user.expiry = hours.toFixed(6);
                        saveData();
                        updateCountdownUI(hours);
                    } else {
                        user.expiry = "0";
                        saveData();
                        checkExpiry();
                        clearInterval(timerInterval);
                    }
                } else if (user && user.role === 'boss') {
                    document.getElementById('countdown-box').innerText = "THỜI GIAN: VĨNH VIỄN";
                }
            }, 1000);
        }

        function updateCountdownUI(hours) {
            const totalSeconds = Math.max(0, Math.floor(hours * 3600));
            const h = Math.floor(totalSeconds / 3600);
            const m = Math.floor((totalSeconds % 3600) / 60);
            const s = totalSeconds % 60;
            document.getElementById('countdown-box').innerText = `THỜI GIAN CÒN LẠI: ${h.toString().padStart(2,'0')}:${m.toString().padStart(2,'0')}:${s.toString().padStart(2,'0')}`;
        }

        function checkExpiry() {
            let user = userDatabase.find(x => x.u === currentBoss);
            if (!user) return;
            if (user.role !== 'boss' && parseFloat(user.expiry) <= 0) {
                document.getElementById('expired-overlay').style.display = 'flex';
                document.getElementById('btn-analyst').disabled = true;
                document.getElementById('md5-inp').disabled = true;
            }
        }

        function processLogin() {
            const u = document.getElementById('login-u').value.trim().toLowerCase();
            const p = document.getElementById('login-p').value.trim();
            const err = document.getElementById('login-error');
            const found = userDatabase.find(x => x.u === u && x.p === p);
            if(found) {
                currentBoss = found.u; 
                found.status = 'online'; 
                saveData();
                err.style.display = 'none'; 
                document.getElementById('scr-login').style.display = 'none';
                document.getElementById('scr-main').style.display = 'flex';
                document.getElementById('user-name-display').innerText = u.toUpperCase();
                if(found.role !== 'boss') document.getElementById('tab2').style.display = 'none';
                renderAdminTable();
                checkExpiry();
                startGlobalTimer();
            } else { 
                err.style.display = 'block'; 
            }
        }

        function toggleView(n) {
            document.getElementById('view-tool').style.display = n === 1 ? 'block' : 'none';
            document.getElementById('view-admin').style.display = n === 2 ? 'block' : 'none';
            document.getElementById('tab1').className = n === 1 ? 'active' : '';
            document.getElementById('tab2').className = n === 2 ? 'active' : '';
            if (n === 2) renderAdminTable();
        }

        function handleTool() {
            let inp = document.getElementById('md5-inp'); 
            let code = inp.value.trim();
            if(code.length !== 32) { alert("MÃ MD5 PHẢI ĐỦ 32 KÝ TỰ HEX!"); return; }
            if(code === lastMd5) { alert("MÃ NÀY ĐÃ ĐƯỢC PHÂN TÍCH!"); return; }
            
            lastMd5 = code;
            let sum = 0; 
            for(let char of code) { let n = parseInt(char, 16); if(!isNaN(n)) sum += n; }
            let res = (sum % 2 === 0) ? "TÀI" : "XỈU";
            
            const display = document.getElementById('res-display'); 
            display.innerText = res;
            display.style.color = res === "TÀI" ? "var(--r)" : "var(--cyan)";
            document.getElementById('md5-display').innerText = `MÃ MD5: ${code}`;
            
            toolHistory.unshift(res); 
            if(toolHistory.length > 5) toolHistory.pop();
            const boxes = document.querySelectorAll('.h-box');
            boxes.forEach((box, i) => { if(toolHistory[i]) box.innerText = toolHistory[i]; });
            document.getElementById('hand-progress').innerText = `TIẾN TRÌNH: ${toolHistory.length}/10 TAY`;
            
            inp.value = "";
        }

        function addNewUser() {
            const nu = document.getElementById('new-user').value.trim().toLowerCase();
            const np = document.getElementById('new-pass').value.trim();
            if(!nu || !np) return;
            // Ngăn chặn tạo trùng với các TK mặc định
            if(defaultUsers.find(x => x.u === nu)) { alert("USER NÀY ĐÃ TỒN TẠI TRONG HỆ THỐNG MẶC ĐỊNH!"); return; }
            userDatabase.push({ id: Date.now(), u: nu, p: np, role: 'user', status: 'offline', expiry: "24" });
            saveData(); renderAdminTable();
            document.getElementById('new-user').value = ""; document.getElementById('new-pass').value = "";
        }

        function editPass(id) {
            let idx = userDatabase.findIndex(x => x.id === id);
            if(userDatabase[idx].role === 'boss') return;
            let newP = prompt("MẬT KHẨU MỚI:", userDatabase[idx].p);
            if(newP) { userDatabase[idx].p = newP; saveData(); renderAdminTable(); }
        }

        function editHours(id) {
            let idx = userDatabase.findIndex(x => x.id === id);
            if(userDatabase[idx].role === 'boss') return;
            let newH = prompt("SỐ GIỜ SỬ DỤNG MỚI:", userDatabase[idx].expiry);
            if(newH) { userDatabase[idx].expiry = parseFloat(newH).toFixed(6); saveData(); renderAdminTable(); }
        }

        function kickUser(id) {
            // Chế độ bảo vệ: Không cho xóa các TK mặc định
            const userToKick = userDatabase.find(x => x.id === id);
            if(defaultUsers.find(x => x.u === userToKick.u)) {
                alert("TÀI KHOẢN MẶC ĐỊNH KHÔNG THỂ XÓA!");
                return;
            }
            if(confirm("XÓA CHIẾN BINH NÀY?")) {
                userDatabase = userDatabase.filter(x => x.id !== id);
                saveData(); renderAdminTable();
            }
        }
        
        function renderAdminTable() {
            const body = document.getElementById('user-list-body'); body.innerHTML = "";
            userDatabase.forEach((u, index) => {
                const isBoss = u.role === 'boss';
                const isDefault = defaultUsers.some(d => d.u === u.u && d.u !== 'admin');
                const dispExpiry = isBoss ? 'VĨNH VIỄN' : parseFloat(u.expiry).toFixed(2);
                const row = `<tr>
                    <td>${index + 1}</td>
                    <td>${u.u} ${isDefault ? '<span style="color:blue">[DEF]</span>' : ''}</td>
                    <td><span class="${isBoss?'':'edit-link'}" onclick="editPass(${u.id})">${u.p}</span></td>
                    <td><span class="${isBoss?'':'edit-link'}" onclick="editHours(${u.id})">${dispExpiry}</span></td>
                    <td class="${u.status === 'online' ? 'status-on' : 'status-off'}">• ${u.status.toUpperCase()}</td>
                    <td>${isBoss ? '<b style="color:green">BOSS</b>' : `<button class="btn-kick-admin" onclick="kickUser(${u.id})">KÍCH</button>`}</td>
                </tr>`;
                body.innerHTML += row;
            });
        }

        function saveData() { localStorage.setItem('vData', JSON.stringify(userDatabase)); }
        
        function logout() { 
            let user = userDatabase.find(x => x.u === currentBoss);
            if(user) user.status = 'offline';
            saveData();
            location.reload(); 
        }

        function initSystem() {
            const c = document.getElementById('matrix-canvas'); const ctx = c.getContext('2d');
            c.width = window.innerWidth; c.height = window.innerHeight;
            const fontSize = 20; const columns = Math.floor(c.width / fontSize);
            const chars = "VULTIMA10101".split(""); const drops = Array(columns).fill(1);
            setInterval(() => {
                ctx.fillStyle = "rgba(0, 0, 0, 0.15)"; ctx.fillRect(0, 0, c.width, c.height);
                ctx.fillStyle = "#bc13fe"; ctx.font = "bold " + fontSize + "px Courier New";
                for(let i = 0; i < drops.length; i++) {
                    const text = chars[Math.floor(Math.random() * chars.length)];
                    ctx.fillText(text, i * fontSize, drops[i] * fontSize);
                    if(drops[i] * fontSize > c.height && Math.random() > 0.975) drops[i] = 0;
                    drops[i]++;
                }
            }, 35);
        }
    </script>
</body>
</html>
