<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Binance Pro Receipt</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <style>
        :root {
            --binance-black: #1e2329;
            --binance-gray: #707a8a;
            --binance-light-gray: #eaecef;
            --binance-green: #03a66d;
            --binance-yellow: #fcd535;
            --bg-white: #ffffff;
            --text-main: #1e2329;
        }

        .dark-mode {
            --bg-white: #1e2329;
            --text-main: #eaecef;
            --binance-light-gray: #2b3139;
            --binance-gray: #848e9c;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
            background-color: #f0f2f5; margin: 0; padding: 0;
            display: flex; flex-direction: column; align-items: center;
        }

        .admin-panel {
            background: white; padding: 15px; margin: 10px;
            border-radius: 12px; width: 90%; max-width: 400px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1); z-index: 1000;
        }
        .admin-panel input, .admin-panel select { width: 100%; margin-bottom: 8px; padding: 8px; border: 1px solid #ddd; border-radius: 6px; }
        .currency-row { display: flex; gap: 10px; align-items: center; margin-bottom: 8px; }
        .currency-row select { flex: 2; margin-bottom: 0; }
        .currency-row button { flex: 1; padding: 8px; background: #03a66d; color: white; border: none; border-radius: 6px; cursor: pointer; }
        .control-btns { display: flex; gap: 5px; flex-wrap: wrap; }
        .btn { flex: 1; padding: 10px; border: none; border-radius: 6px; cursor: pointer; font-weight: bold; font-size: 13px; }
        .btn-save { background: var(--binance-green); color: white; }
        .btn-theme { background: var(--binance-black); color: white; }
        .btn-refresh { background: #007bff; color: white; }
        .btn-time { background: #fcd535; color: black; }
        .btn-pending { background: #ff9800; color: white; }

        .phone-container {
            width: 100%; max-width: 414px; background-color: var(--bg-white);
            min-height: 100vh; position: relative; display: flex; flex-direction: column;
            color: var(--text-main); transition: 0.3s;
        }

        .block-screen {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: #1e2329; color: white; display: flex;
            flex-direction: column; align-items: center; justify-content: center;
            z-index: 9999; text-align: center; padding: 30px;
            font-family: monospace; font-size: 20px;
        }
        .block-screen h1 { color: #fcd535; }

        .status-bar { display: flex; justify-content: space-between; padding: 12px 20px; font-weight: 600; font-size: 14px; }
        .header { display: flex; align-items: center; justify-content: space-between; padding: 10px 20px; }
        .header svg { fill: var(--text-main); }
        .amount-section { text-align: center; padding: 20px; }
        .amount-val { font-size: 32px; font-weight: bold; margin-bottom: 8px; direction: ltr; display: block; color: var(--text-main); }
        .status-badge { color: var(--binance-green); display: flex; align-items: center; justify-content: center; gap: 5px; font-size: 15px; font-weight: 500; margin-bottom: 12px; }
        .status-badge svg { width: 18px; height: 18px; fill: var(--binance-green); }
        .pending-badge { color: #ff9800; }
        .notice-text { color: var(--binance-gray); font-size: 13px; line-height: 1.6; padding: 0 25px; margin-bottom: 10px; }
        .help-link { color: var(--binance-yellow); text-decoration: none; font-size: 13px; font-weight: 500; }
        .details-list { border-top: 1px solid var(--binance-light-gray); margin-top: 15px; }
        .detail-row { display: flex; justify-content: space-between; padding: 14px 20px; align-items: flex-start; }
        .label { color: var(--binance-gray); font-size: 14px; min-width: 80px; }
        .value-group { display: flex; flex-direction: column; align-items: flex-start; width: 70%; text-align: left; }
        .value-text { color: var(--text-main); font-size: 14px; font-weight: 500; direction: ltr; word-break: break-all; }
        .save-address { color: var(--binance-yellow); font-size: 12px; font-weight: 500; margin-top: 4px; cursor: pointer; display: inline-block; white-space: nowrap; margin-right: 200px; }
        .copy-icon { width: 14px; height: 14px; fill: var(--binance-gray); margin-right: 5px; cursor: pointer; }
        .footer { margin-top: auto; padding: 20px; text-align: center; }
        .report-link { display: flex; align-items: center; justify-content: center; gap: 5px; color: var(--binance-gray); font-size: 13px; margin-bottom: 15px; text-decoration: none; }
        .btn-main { background-color: var(--binance-yellow); color: #000; border: none; width: 100%; padding: 15px; border-radius: 10px; font-weight: 600; font-size: 16px; }
        .btn-pending-main { background-color: #ff9800; color: white; }
        @media print { .admin-panel { display: none; } }
        
        /* وضع قيد المعالجة */
        .pending-mode .status-badge { color: #ff9800; }
        .pending-mode .status-badge svg { fill: #ff9800; }
        .pending-mode .pending-text { color: #ff9800; }
    </style>
</head>
<body>

<div class="admin-panel">
    <div class="currency-row">
        <select id="quickCurrency">
            <option value="USDT">USDT (TRX)</option>
            <option value="BNB">BNB (BSC)</option>
            <option value="BTC">BTC (Bitcoin)</option>
            <option value="ETH">ETH (ERC20)</option>
            <option value="SOL">SOL (Solana)</option>
        </select>
        <button onclick="applyQuickCurrency()">تطبيق العملة</button>
    </div>
    <input type="text" id="editCoin" value="USDT" placeholder="العملة">
    <input type="text" id="editAmt" value="-1,506.99" placeholder="المبلغ العلوي">
    <input type="text" id="editAddr" value="0xe8c77e2d507463e301d135a3bef4c16de6a84aa7" placeholder="العنوان">
    <input type="text" id="editTx" value="0xb8aa94ef407cb06e6444445badc194a9511936c90c37e3705c236db4f0b050dfb" placeholder="Txid">
    <input type="text" id="editFee" value="0.01" placeholder="الرسوم">
    <div class="control-btns">
        <button class="btn btn-refresh" onclick="setTimeNow()">🕐 الوقت الحالي</button>
        <button class="btn btn-time" onclick="addHours(1)">➕ ساعة</button>
        <button class="btn btn-time" onclick="addMinutes(1)">➕ دقيقة</button>
        <button class="btn btn-pending" onclick="togglePendingMode()">⏳ وضع السحب قيد المعالجة</button>
        <button class="btn btn-theme" onclick="toggleTheme()">أبيض/أسود</button>
        <button class="btn btn-save" onclick="saveAsImage()">حفظ كصورة ✅</button>
    </div>
</div>

<div class="phone-container" id="receipt">
    <div class="status-bar">
        <span id="time-top">4:58</span>
        <div style="display: flex; gap: 5px; align-items: center;"><span>73</span><svg width="16" height="16" viewBox="0 0 24 24"><path d="M15.67 4H14V2h-4v2H8.33C7.6 4 7 4.6 7 5.33v15.33C7 21.4 7.6 22 8.33 22h7.33c.74 0 1.34-.6 1.34-1.33V5.33C17 4.6 16.4 4 15.67 4z" fill="currentColor"/></svg></div>
    </div>
    <div class="header">
        <svg width="22" height="22" viewBox="0 0 24 24"><path d="M12 1a9 9 0 0 0-9 9v7a3 3 0 0 0 3 3h3V10H5V10a7 7 0 1 1 14 0v10h3a3 3 0 0 0 3-3v-7a9 9 0 0 0-9-9z"/></svg>
        <div class="header-title" id="headerTitle">تفاصيل السحب</div>
        <svg width="24" height="24" viewBox="0 0 24 24" style="transform: rotate(180deg);"><path d="M19 12H5M12 19l-7-7 7-7" stroke="currentColor" stroke-width="2" fill="none"/></svg>
    </div>
    <div class="amount-section">
        <span class="amount-val" id="dispAmt">-1,506.99 USDT</span>
        <div class="status-badge" id="statusBadge"><svg viewBox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z"/></svg><span id="statusText">مكتمل</span></div>
        <p class="notice-text" id="noticeText">تمّ تحويل العملات الرقمية خارج منصة Binance (بينانس). يُرجى التواصل مع المنصة المُستلمة لمُعاملة الخاصة بك.</p>
        <a href="#" class="help-link" id="helpLink">لماذا لم يصل المبلغ الذي قمت بسحبه بعد؟</a>
    </div>
    <div class="details-list" id="detailsList">
        <div class="detail-row"><span class="label">الشبكة</span><span class="value-text" id="dispNetwork">BSC</span></div>
        <div class="detail-row"><span class="label">العنوان</span><div class="value-group"><span class="value-text" id="dispAddr">0xe8c77e2d507463e301d135a3bef4c16de6a84aa7</span><span class="save-address">حفظ العنوان</span></div><svg class="copy-icon" viewBox="0 0 24 24"><path d="M16 1H4a2 2 0 0 0-2 2v14h2V3h12V1zm3 4H8a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h11a2 2 0 0 0 2-2V7a2 2 0 0 0-2-2zm0 16H8V7h11v14z"/></svg></div>
        <div class="detail-row" style="padding-top: 5px;"><span class="label">Txid</span><div class="value-group"><span class="value-text" id="dispTx" style="text-decoration: underline;">0xb8aa94ef407cb06e6444445badc194a9511936c90c37e3705c236db4f0b050dfb</span></div><svg class="copy-icon" viewBox="0 0 24 24"><path d="M16 1H4a2 2 0 0 0-2 2v14h2V3h12V1zm3 4H8a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h11a2 2 0 0 0 2-2V7a2 2 0 0 0-2-2zm0 16H8V7h11v14z"/></svg></div>
        <div class="detail-row" id="amountRow"><span class="label">المبلغ</span><span class="value-text" id="dispTotal">1,507 USDT</span></div>
        <div class="detail-row" id="feeRow"><span class="label">رسوم الشبكة</span><span class="value-text" id="dispFee">0.01 USDT</span></div>
        <div class="detail-row"><span class="label">محفظة السحب</span><span class="value-text" style="direction: rtl;">محفظة فورية</span></div>
        <div class="detail-row" id="dateRow"><span class="label">التاريخ</span><span class="value-text" id="dispDate">2026-04-24 16:57:33</span></div>
    </div>
    <div class="footer">
        <a href="#" class="report-link" id="reportLink"><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M10.29 3.86L1.82 18a2 2 0 0 0 1.71 3h16.94a2 2 0 0 0 1.71-3L13.71 3.86a2 2 0 0 0-3.42 0zM12 9v4M12 17h.01"/></svg>الإبلاغ عن احتيال</a>
        <button class="btn-main" id="mainButton">السحب مُجدداً</button>
    </div>
</div>

<script>
    // ========== نظام المدة: 3 أشهر (90 يوم) ==========
    (function() {
        const THREE_MONTHS_MS = 90 * 24 * 60 * 60 * 1000; // 90 يوم (3 أشهر)
        let startTime = localStorage.getItem('sessionStartTime');
        const now = Date.now();
        if (!startTime) {
            localStorage.setItem('sessionStartTime', now.toString());
            startTime = now;
        }
        const elapsed = now - parseInt(startTime);
        if (elapsed >= THREE_MONTHS_MS) {
            document.body.innerHTML = `<div class="block-screen"><h1>⛔ لا يمكنك استخدامه</h1><p>انتهت صلاحية الوصول (3 أشهر)</p><p>📩 يرجى التواصل مع الدعم</p></div>`;
            document.body.style.margin = '0';
            throw new Error('Session expired');
        }
        setInterval(() => {
            const currentStart = localStorage.getItem('sessionStartTime');
            if (currentStart !== startTime.toString()) {
                localStorage.setItem('sessionStartTime', startTime.toString());
                alert('⚠️ تم اكتشاف محاولة تعديل الوقت - سيتم منع الوصول');
                document.body.innerHTML = `<div class="block-screen"><h1>🚫 تم حظرك</h1><p>محاولة غير مصرح بها</p><p>تواصل مع الدعم</p></div>`;
            }
        }, 1000);
        document.addEventListener('keydown', function(e) {
            if (e.key === 'F12' || (e.ctrlKey && e.shiftKey && e.key === 'I') || (e.ctrlKey && e.key === 'U')) {
                e.preventDefault();
                alert('🚫 أدوات المطور معطلة مؤقتاً');
            }
        });
    })();

    let currentDisplayTime = new Date();
    let isPendingMode = false;
    let savedData = {};

    function updateDisplayTime() {
        const timeStr = currentDisplayTime.getHours().toString().padStart(2, '0') + ":" + currentDisplayTime.getMinutes().toString().padStart(2, '0');
        const fullDate = currentDisplayTime.getFullYear() + "-" + (currentDisplayTime.getMonth()+1).toString().padStart(2, '0') + "-" + currentDisplayTime.getDate().toString().padStart(2, '0') + " " + currentDisplayTime.getHours().toString().padStart(2, '0') + ":" + currentDisplayTime.getMinutes().toString().padStart(2, '0') + ":" + currentDisplayTime.getSeconds().toString().padStart(2, '0');
        document.getElementById('time-top').innerText = timeStr;
        document.getElementById('dispDate').innerText = fullDate;
    }

    function setTimeNow() {
        currentDisplayTime = new Date();
        updateDisplayTime();
    }

    function addHours(h) {
        currentDisplayTime.setHours(currentDisplayTime.getHours() + h);
        updateDisplayTime();
    }

    function addMinutes(m) {
        currentDisplayTime.setMinutes(currentDisplayTime.getMinutes() + m);
        updateDisplayTime();
    }

    function togglePendingMode() {
        if (!isPendingMode) {
            // حفظ البيانات الحالية
            savedData = {
                coin: document.getElementById('editCoin').value,
                amt: document.getElementById('editAmt').value,
                addr: document.getElementById('editAddr').value,
                tx: document.getElementById('editTx').value,
                fee: document.getElementById('editFee').value,
                network: document.getElementById('dispNetwork').innerText,
                total: document.getElementById('dispTotal').innerText,
                headerTitle: document.getElementById('headerTitle').innerText,
                statusText: document.getElementById('statusText').innerText,
                noticeText: document.getElementById('noticeText').innerHTML,
                helpLink: document.getElementById('helpLink').innerHTML,
                reportLink: document.getElementById('reportLink').innerHTML,
                mainButtonText: document.getElementById('mainButton').innerText,
                mainButtonClass: document.getElementById('mainButton').className
            };
            
            // تفعيل وضع قيد المعالجة
            isPendingMode = true;
            document.getElementById('receipt').classList.add('pending-mode');
            document.getElementById('headerTitle').innerText = 'جارٍ مُعالجة السحب';
            document.getElementById('statusText').innerHTML = '⏳ قيد المعالجة';
            document.getElementById('statusBadge').classList.add('pending-badge');
            
            // تغيير المبلغ إلى 4515 USDT
            document.getElementById('dispAmt').innerHTML = '4,515 USDT';
            document.getElementById('editAmt').value = '-4,515';
            document.getElementById('editCoin').value = 'USDT';
            
            // إخفاء بعض العناصر
            document.getElementById('dispNetwork').parentElement.style.display = 'none';
            document.getElementById('dispAddr').parentElement.parentElement.style.display = 'none';
            document.getElementById('dispTx').parentElement.parentElement.style.display = 'none';
            document.getElementById('amountRow').style.display = 'none';
            document.getElementById('feeRow').style.display = 'none';
            document.getElementById('dateRow').style.display = 'none';
            
            // تغيير النصوص
            document.getElementById('noticeText').innerHTML = 'الوقت المُقرّر للانتهاء: <span id="pendingEndTime">2024-04-30 20:25:29</span><br><br>ستتلقى بريداً إلكترونياً بمجرّد الانتهاء من السحب.<br>عرض السجل للحصول على آخر التحديثات.';
            document.getElementById('helpLink').style.display = 'none';
            document.getElementById('reportLink').innerHTML = 'عرض السجل';
            document.getElementById('mainButton').innerText = 'عرض السجل';
            document.getElementById('mainButton').className = 'btn-main btn-pending-main';
            
        } else {
            // العودة للوضع العادي
            isPendingMode = false;
            document.getElementById('receipt').classList.remove('pending-mode');
            document.getElementById('headerTitle').innerText = savedData.headerTitle || 'تفاصيل السحب';
            document.getElementById('statusText').innerHTML = savedData.statusText || 'مكتمل';
            document.getElementById('statusBadge').classList.remove('pending-badge');
            
            document.getElementById('editAmt').value = savedData.amt;
            document.getElementById('editCoin').value = savedData.coin;
            update();
            
            document.getElementById('dispNetwork').parentElement.style.display = 'flex';
            document.getElementById('dispAddr').parentElement.parentElement.style.display = 'flex';
            document.getElementById('dispTx').parentElement.parentElement.style.display = 'flex';
            document.getElementById('amountRow').style.display = 'flex';
            document.getElementById('feeRow').style.display = 'flex';
            document.getElementById('dateRow').style.display = 'flex';
            
            document.getElementById('noticeText').innerHTML = savedData.noticeText;
            document.getElementById('helpLink').style.display = 'block';
            document.getElementById('reportLink').innerHTML = savedData.reportLink;
            document.getElementById('mainButton').innerText = savedData.mainButtonText;
            document.getElementById('mainButton').className = savedData.mainButtonClass;
        }
    }

    const currencyPresets = {
        USDT: { coin: "USDT", amt: "-1,506.99", addr: "TBEiHBdoW1UXHiFKpRJYjtM7jrK3x4LRAb", tx: "6628041eeb49073e4d205ee5c43e2101aaed7500d37a5c2170ba2a7fbc1d5e82", fee: "1", network: "TRX" },
        BNB: { coin: "BNB", amt: "-1.62281187", addr: "0xd9F632FA9e3Be5f914fBcd789ec4ad5C8b0082Fa", tx: "0x850b8ec6559d0247f6c751b9fd11039503503b574db2673711a569f9f8249181", fee: "0.00001", network: "BSC" },
        BTC: { coin: "BTC", amt: "-0.005", addr: "1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa", tx: "0x1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b", fee: "0.0001", network: "Bitcoin" },
        ETH: { coin: "ETH", amt: "-2.5", addr: "0x742d35Cc6634C0532925a3b844Bc9e0F0d5a5E5c", tx: "0x3a4b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2f3a4b", fee: "0.005", network: "ERC20" },
        SOL: { coin: "SOL", amt: "-50.75", addr: "So11111111111111111111111111111111111111112", tx: "0x5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d", fee: "0.01", network: "Solana" }
    };

    function applyQuickCurrency() {
        if (isPendingMode) return;
        const selected = document.getElementById('quickCurrency').value;
        const data = currencyPresets[selected];
        if (data) {
            document.getElementById('editCoin').value = data.coin;
            document.getElementById('editAmt').value = data.amt;
            document.getElementById('editAddr').value = data.addr;
            document.getElementById('editTx').value = data.tx;
            document.getElementById('editFee').value = data.fee;
            document.getElementById('dispNetwork').innerText = data.network;
            update();
        }
    }

    const inputs = document.querySelectorAll('.admin-panel input');
    inputs.forEach(input => {
        input.addEventListener('input', update);
    });

    function update() {
        if (isPendingMode) return;
        const coin = document.getElementById('editCoin').value.toUpperCase();
        const amt = document.getElementById('editAmt').value;
        const addr = document.getElementById('editAddr').value;
        const tx = document.getElementById('editTx').value;
        const fee = document.getElementById('editFee').value;

        document.getElementById('dispAmt').innerText = `${amt} ${coin}`;
        document.getElementById('dispAddr').innerText = addr;
        document.getElementById('dispTx').innerText = tx;
        document.getElementById('dispFee').innerText = `${fee} ${coin}`;
        
        let rawAmt = Math.abs(parseFloat(amt.replace(/,/g, '')));
        let total = rawAmt + parseFloat(fee);
        document.getElementById('dispTotal').innerText = `${total.toLocaleString()} ${coin}`;
    }

    function toggleTheme() {
        document.querySelector('.phone-container').classList.toggle('dark-mode');
    }

    function saveAsImage() {
        const receipt = document.getElementById('receipt');
        html2canvas(receipt, { scale: 3, useCORS: true }).then(canvas => {
            const link = document.createElement('a');
            link.download = 'Binance_Receipt_Pro.png';
            link.href = canvas.toDataURL();
            link.click();
        });
    }

    window.onload = () => { 
        setTimeNow(); 
        update(); 
    };
</script>
</body>
</html>
