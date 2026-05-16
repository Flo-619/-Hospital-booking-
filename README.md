<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <meta name="description" content="Botswana Hospital Queue - Free Queue System + Extra Payment Section (Priority, Express, Donation, Premium)">
    <meta name="theme-color" content="#0a2f44">
    <title>Botswana Hospital Queue | Free + Premium Payments | Priority Queue</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        :root {
            --primary: #0d9488;
            --primary-dark: #0f766e;
            --primary-glow: #5eead4;
            --bg-dark: #0a0f1f;
            --card-glass: rgba(18, 25, 45, 0.85);
            --text-light: #f1f5f9;
            --text-muted: #cbd5e1;
            --accent-gold: #fbbf24;
            --error: #ef4444;
            --success: #10b981;
            --warning: #f59e0b;
            --premium-gold: #ffd700;
        }
        body {
            font-family: 'Inter', system-ui, sans-serif;
            background: radial-gradient(ellipse at 30% 40%, #0f172a, #030712);
            min-height: 100vh;
            padding: 20px 18px 48px;
            color: var(--text-light);
            transition: all 0.2s ease;
        }
        body.font-light { font-weight: 300; }
        body.font-regular { font-weight: 400; }
        body.font-bold { font-weight: 700; }
        .app-container { max-width: 1400px; margin: 0 auto; position: relative; z-index: 2; }
        *:focus { outline: 3px solid var(--accent-gold); outline-offset: 3px; }
        .glass-header {
            background: rgba(15, 23, 42, 0.7);
            backdrop-filter: blur(16px);
            border-radius: 2rem;
            padding: 1.4rem 2rem;
            margin-bottom: 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 1rem;
            border: 1px solid rgba(94, 234, 212, 0.25);
        }
        .brand h1 { font-size: 1.7rem; background: linear-gradient(135deg, #fff, var(--primary-glow)); -webkit-background-clip: text; background-clip: text; color: transparent; }
        .toolbar { display: flex; gap: 10px; flex-wrap: wrap; }
        .pill-btn {
            background: rgba(255,255,255,0.05);
            border: 1px solid rgba(94,234,212,0.3);
            padding: 8px 20px;
            border-radius: 40px;
            font-size: 0.8rem;
            font-weight: 500;
            cursor: pointer;
            color: var(--text-light);
            transition: 0.2s;
        }
        .pill-btn.active { background: var(--primary); border-color: var(--primary-glow); box-shadow: 0 0 10px var(--primary-glow); }
        .pill-btn:hover:not(.active) { background: rgba(13,148,136,0.3); }
        .neo-card {
            background: var(--card-glass);
            backdrop-filter: blur(16px);
            border-radius: 2rem;
            border: 1px solid rgba(94, 234, 212, 0.2);
            overflow: hidden;
            transition: transform 0.2s;
        }
        .neo-card:hover { transform: translateY(-3px); }
        .card-header { padding: 1.2rem 1.8rem; border-bottom: 1px solid rgba(94,234,212,0.2); background: rgba(0,0,0,0.2); }
        .card-header h2 { font-size: 1.3rem; display: flex; align-items: center; gap: 8px; color: var(--primary-glow); flex-wrap: wrap; }
        .card-body { padding: 1.5rem; }
        .input-field { margin-bottom: 1.2rem; }
        .input-field label { display: block; font-size: 0.75rem; font-weight: 600; margin-bottom: 6px; color: var(--text-muted); }
        .input-field input, .input-field select, .input-field textarea {
            width: 100%;
            padding: 12px 16px;
            background: rgba(0,0,0,0.6);
            border: 1px solid rgba(94,234,212,0.35);
            border-radius: 1.25rem;
            color: var(--text-light);
            font-size: 0.95rem;
        }
        .input-field input:focus, .input-field select:focus { outline: none; border-color: var(--primary); box-shadow: 0 0 0 2px rgba(13,148,136,0.3); }
        button {
            width: 100%;
            padding: 12px;
            border-radius: 2rem;
            font-weight: 700;
            border: none;
            cursor: pointer;
            background: linear-gradient(105deg, var(--primary-dark), var(--primary));
            color: white;
            transition: 0.2s;
        }
        button:hover:not(:disabled) { transform: scale(0.98); box-shadow: 0 0 12px var(--primary-glow); }
        .grid-4col {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 1.8rem;
            margin-bottom: 2rem;
        }
        @media (max-width: 1200px) { .grid-4col { grid-template-columns: repeat(2, 1fr); } }
        @media (max-width: 700px) { .grid-4col { grid-template-columns: 1fr; } .glass-header { flex-direction: column; } .key-btn { width: 40px; height: 40px; } }
        .key-btn { background: #1e293b; border: 1px solid var(--primary-glow); width: 48px; height: 48px; border-radius: 14px; cursor: pointer; color: white; font-weight: bold; transition: 0.1s; }
        .key-btn:hover, .key-btn:focus { background: var(--primary); transform: scale(1.02); }
        .keyboard-row { display: flex; justify-content: center; gap: 6px; margin-bottom: 8px; flex-wrap: wrap; }
        .key-btn.special { width: auto; padding: 0 16px; }
        .feedback-toast { margin-top: 1rem; padding: 12px; border-radius: 1rem; display: none; background: rgba(0,0,0,0.8); border-left: 4px solid var(--primary); animation: fadeIn 0.3s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(-5px); } to { opacity: 1; transform: translateY(0); } }
        .queue-table { width: 100%; border-collapse: collapse; }
        .queue-table th, .queue-table td { padding: 12px 8px; text-align: left; border-bottom: 1px solid rgba(94,234,212,0.2); }
        .queue-table th { color: var(--primary-glow); font-weight: 700; }
        .currently-serving { background: linear-gradient(135deg, var(--primary-dark), var(--primary)); border-radius: 1.5rem; padding: 1.2rem; text-align: center; margin-bottom: 1.5rem; font-weight: bold; font-size: 1.1rem; }
        .call-btn { background: var(--accent-gold); color: #0f172a; margin-top: 1rem; }
        .serve-btn { background: var(--success); padding: 6px 12px; border-radius: 2rem; font-size: 0.75rem; width: auto; }
        .free-badge { background: var(--success); color: white; border-radius: 30px; padding: 4px 12px; font-size: 0.7rem; font-weight: bold; display: inline-block; margin-left: 8px; }
        
        /* Payment Section Styles */
        .tier-selector { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 1rem; }
        .tier-btn {
            background: #334155;
            padding: 8px 12px;
            border-radius: 2rem;
            font-size: 0.75rem;
            font-weight: 600;
            cursor: pointer;
            border: none;
            color: white;
            transition: all 0.2s;
        }
        .tier-btn.active-tier { background: linear-gradient(105deg, var(--primary-dark), var(--primary)); box-shadow: 0 0 8px var(--primary-glow); }
        .tier-btn:hover { transform: translateY(-2px); background: var(--primary-dark); }
        .payment-method-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 8px; margin: 1rem 0; }
        .payment-method-btn {
            background: rgba(255,255,255,0.08);
            border: 1px solid rgba(94,234,212,0.3);
            border-radius: 1rem;
            padding: 10px;
            cursor: pointer;
            text-align: center;
            transition: all 0.2s;
            font-size: 0.8rem;
        }
        .payment-method-btn:hover, .payment-method-btn.selected { background: rgba(13,148,136,0.4); border-color: var(--primary-glow); transform: translateY(-2px); }
        .donation-amounts { display: flex; gap: 8px; flex-wrap: wrap; margin: 10px 0; }
        .donation-amount { background: #334155; padding: 6px 12px; border-radius: 2rem; font-size: 0.75rem; cursor: pointer; transition: 0.2s; }
        .donation-amount:hover, .donation-amount.active { background: var(--primary); }
        .recent-payments { max-height: 200px; overflow-y: auto; margin-top: 1rem; font-size: 0.7rem; }
        .payment-item { background: rgba(0,0,0,0.3); border-radius: 0.75rem; padding: 8px; margin-bottom: 6px; border-left: 3px solid var(--primary); }
        .priority-badge { background: var(--accent-gold); color: #0f172a; border-radius: 20px; padding: 2px 8px; font-size: 0.6rem; font-weight: bold; margin-left: 8px; }
        .premium-star { color: var(--premium-gold); font-size: 0.9rem; margin-left: 5px; }
        .modal-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.95); backdrop-filter: blur(12px); z-index: 1000;
            display: flex; align-items: center; justify-content: center; padding: 20px;
        }
        .modal-card { max-width: 450px; width: 100%; background: #0f172a; border-radius: 2rem; border: 2px solid var(--primary-glow); padding: 2rem; }
    </style>
</head>
<body>
<div class="app-container" id="appContainer">
    <div class="glass-header">
        <div class="brand"><h1 id="mainTitle">🇧🇼 Botswana Hospital Queue · Free + Premium</h1><p id="taglineText">Free queue • Priority upgrades • Donations • Bilingual</p></div>
        <div class="toolbar">
            <button class="pill-btn" id="fontUp">🔍 A+</button><button class="pill-btn" id="fontDown">🔍 A-</button>
            <button class="pill-btn" id="contrastBtn">🌓 Contrast</button>
            <button class="pill-btn" id="langEn"><span>🇬🇧 English</span></button>
            <button class="pill-btn" id="langTs"><span>🇧🇼 Setswana</span></button>
        </div>
    </div>
    <div class="emergency-banner" style="background:rgba(239,68,68,0.12); border-left:5px solid #ef4444; border-radius:1.5rem; padding:1rem; margin-bottom:1.5rem;"><span>🚨</span> <span id="emergencyMsg">Emergency: 997 (Ambulance) / 998 (Police)</span></div>
    
    <!-- Font Controls -->
    <div class="neo-card" style="margin-bottom: 1.8rem;">
        <div class="card-header"><h2>🎨 <span id="fontControlTitle">Font & Typography Controls</span></h2></div>
        <div class="card-body">
            <div style="display:flex; flex-wrap:wrap; gap:20px; justify-content:space-between;">
                <div style="flex:1; min-width:150px;"><label id="fontFamilyLabel">📄 Font Family</label><select id="fontFamilySelect"><option value="'Inter', system-ui">Inter</option><option value="'Open Dyslexic', sans-serif">Open Dyslexic</option><option value="Tahoma">Tahoma</option></select></div>
                <div style="flex:1; min-width:150px;"><label id="fontWeightLabel">⚖️ Font Weight</label><div class="font-control-group"><button id="weightLight" class="pill-btn">Light</button><button id="weightRegular" class="pill-btn">Regular</button><button id="weightBold" class="pill-btn">Bold</button></div></div>
                <div style="flex:1; min-width:180px;"><label id="lineSpacingLabel">📏 Line Spacing</label><input type="range" id="lineHeightSlider" min="1" max="2" step="0.05" value="1.4"><span id="lineHeightValue">1.4</span></div>
                <div style="flex:1; min-width:180px;"><label id="letterSpacingLabel">🔤 Letter Spacing</label><input type="range" id="letterSpacingSlider" min="0" max="3" step="0.1" value="0"><span id="letterSpacingValue">0px</span></div>
            </div>
        </div>
    </div>

    <!-- 4-COLUMN GRID: Booking + Symptom + Keyboard + PAYMENT SECTION -->
    <div class="grid-4col">
        <!-- Card 1: Free Booking -->
        <div class="neo-card">
            <div class="card-header"><h2>📋 <span id="bookingTitle">Queue Registration</span> <span class="free-badge">✓ FREE</span></h2></div>
            <div class="card-body">
                <div class="input-field"><label id="nameLabel">Full Name *</label><input type="text" id="fullName" placeholder="e.g. Amantle Raditladi"></div>
                <div class="input-field"><label id="omangLabel">Omang (National ID) *</label><input type="text" id="omangId" placeholder="e.g. 10123456789"></div>
                <div class="input-field"><label id="hospitalLabel">Select Hospital *</label><select id="hospitalSelect"><option value="">-- Choose Hospital --</option><option>Princess Marina Hospital</option><option>Nyangabgwe Referral Hospital</option><option>Molepolole DHMT</option><option>Mochudi Hospital</option></select></div>
                <div class="input-field"><label id="reasonLabel">Reason for Visit *</label><input type="text" id="visitReason" placeholder="e.g. fever, chest pain"></div>
                <button id="bookBtn">✨ <span id="bookText">Join Queue (Free)</span></button>
                <div id="bookingToast" class="feedback-toast"></div>
            </div>
        </div>
        
        <!-- Card 2: Symptom Checker -->
        <div class="neo-card">
            <div class="card-header"><h2>🩺 <span id="symptomTitle">Symptom Checker & AI Referral</span></h2></div>
            <div class="card-body">
                <div class="input-field"><label id="symptomsLabel">Describe your symptoms</label>
                <textarea id="symptomInput" rows="4" placeholder="Example: severe headache, chest tightness..."></textarea></div>
                <button id="getAIBtn">🧠 <span id="aiBtnText">Get AI Recommendation</span></button>
                <div id="aiToast" class="feedback-toast"></div>
            </div>
        </div>
        
        <!-- Card 3: On-Screen Keyboard -->
        <div class="neo-card">
            <div class="card-header"><h2>⌨️ <span id="keyboardTitle">On-Screen Keyboard</span></h2></div>
            <div class="card-body">
                <button id="toggleKeyboardBtn" class="keyboard-toggle">🎹 <span id="toggleKeyboardText">Show Keyboard</span></button>
                <div id="onscreenKeyboard" style="display:none;"><div class="onscreen-keyboard" id="dynamicKbContainer"></div></div>
            </div>
        </div>
        
        <!-- Card 4: EXTRA PAYMENT SECTION -->
        <div class="neo-card">
            <div class="card-header"><h2>💰 <span id="paymentSectionTitle">Premium Upgrades & Donations</span> <span id="premiumUserBadge" style="display:none;" class="premium-star">⭐ Premium Member</span></h2></div>
            <div class="card-body">
                <!-- Pricing Tiers -->
                <div class="tier-selector" id="pricingTiers">
                    <button class="tier-btn active-tier" data-tier="priority" data-price="15">🚀 Priority Jump (BWP 15)</button>
                    <button class="tier-btn" data-tier="express" data-price="10">⚡ Express (BWP 10)</button>
                    <button class="tier-btn" data-tier="donation" data-price="custom">❤️ Donation (Custom)</button>
                    <button class="tier-btn" data-tier="premium" data-price="25">⭐ Premium (BWP 25/30d)</button>
                </div>
                
                <!-- Donation Custom Amount (hidden by default) -->
                <div id="donationSection" style="display:none;">
                    <div class="donation-amounts" id="donationAmounts">
                        <span class="donation-amount" data-amount="5">BWP 5</span>
                        <span class="donation-amount" data-amount="10">BWP 10</span>
                        <span class="donation-amount" data-amount="20">BWP 20</span>
                        <span class="donation-amount" data-amount="50">BWP 50</span>
                        <span class="donation-amount" data-amount="100">BWP 100</span>
                    </div>
                    <input type="number" id="customDonation" placeholder="Or enter custom amount (BWP)" min="1" style="width:100%; margin-top:8px;">
                </div>
                
                <!-- Payment Methods -->
                <div class="payment-method-grid" id="paymentMethodsGrid">
                    <div class="payment-method-btn" data-method="orange">📱 Orange Money</div>
                    <div class="payment-method-btn" data-method="mascom">📱 Mascom MyZaka</div>
                    <div class="payment-method-btn" data-method="btc">📱 BTC SmartMoney</div>
                    <div class="payment-method-btn" data-method="card">💳 Credit/Debit Card</div>
                    <div class="payment-method-btn" data-method="cash">💵 Cash on Arrival</div>
                </div>
                
                <button id="processPaymentBtn">💸 Complete Payment</button>
                
                <!-- Recent Payments -->
                <div style="margin-top: 1rem;">
                    <div style="display:flex; justify-content:space-between; align-items:center;">
                        <span style="font-size:0.75rem; font-weight:bold;">📜 Recent Payments</span>
                        <button id="viewAllPaymentsBtn" style="width:auto; padding:4px 12px; font-size:0.7rem; background:#334155;">View All</button>
                    </div>
                    <div id="recentPaymentsList" class="recent-payments">
                        <div style="text-align:center; color:var(--text-muted); padding:10px;">No payments yet</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Active Patient Queue Board -->
    <div class="neo-card">
        <div class="card-header"><h2>📊 <span id="queueBoardTitle">Active Patient Queue</span> <span id="queueCounter"></span></h2></div>
        <div class="card-body">
            <div id="currentlyServing" class="currently-serving">🩺 <span id="servingText">Currently Serving</span>: <strong id="servingPatient">—</strong></div>
            <div style="overflow-x: auto;">
                <table class="queue-table" id="queueTable">
                    <thead><tr><th>#</th><th id="thPatient">Patient</th><th id="thWait">Est. Wait</th><th id="thStatus">Status</th><th id="thAction">Action</th></tr></thead>
                    <tbody id="queueTableBody"></tbody>
                </table>
            </div>
            <button id="callNextBtn" class="call-btn">🔔 <span id="callNextText">Call Next Patient (Admin)</span></button>
            <div id="adminPinPanel" style="display:none; margin-top:10px;">
                <input type="password" id="adminPin" placeholder="Enter PIN 1234" style="width:70%; padding:10px; border-radius:2rem;">
                <button id="verifyPinBtn" style="width:28%;">Verify</button>
            </div>
            <div id="offlineStatus" style="font-size:0.7rem; text-align:center; margin-top:14px;">📡 Offline-capable | Free + Premium Payments | Priority Queue Upgrades</div>
        </div>
    </div>
    <footer id="footerText">⚕️ Botswana Health | Free Queue + Priority Upgrades | Donations Support Hospital</footer>
</div>

<script>
    // ======================== COMPLETE BILINGUAL TRANSLATIONS ========================
    const translations = {
        en: {
            mainTitle: "🇧🇼 Botswana Hospital Queue · Free + Premium",
            tagline: "Free queue • Priority upgrades • Donations • Bilingual",
            emergencyMsg: "Emergency: 997 (Ambulance) / 998 (Police)",
            fontControlTitle: "Font & Typography Controls",
            fontFamilyLabel: "Font Family", fontWeightLabel: "Font Weight",
            lineSpacingLabel: "Line Spacing", letterSpacingLabel: "Letter Spacing",
            bookingTitle: "Queue Registration", symptomTitle: "Symptom Checker", aiBtnText: "Get AI Recommendation",
            keyboardTitle: "On-Screen Keyboard", toggleKeyboardText: "Show Keyboard", hideKeyboardText: "Hide Keyboard",
            queueBoardTitle: "Active Patient Queue", servingText: "Currently Serving",
            thPatient: "Patient", thWait: "Est. Wait", thStatus: "Status", thAction: "Action",
            callNextText: "Call Next Patient (Admin)", emptyQueue: "✨ No active queue",
            waiting: "Waiting", inProgress: "In Progress", served: "Served", serveBtn: "Serve",
            nameLabel: "Full Name *", omangLabel: "Omang (ID) *", hospitalLabel: "Select Hospital *", reasonLabel: "Reason *",
            bookText: "Join Queue (Free)", fillFields: "Please fill all fields", omangInvalid: "Invalid Omang",
            paymentSectionTitle: "Premium Upgrades & Donations",
            prioritySuccess: "✅ Priority Jump purchased! You've been moved to position 2.",
            expressSuccess: "✅ Express Service purchased! Your estimated wait time reduced.",
            donationSuccess: "❤️ Thank you for your donation of BWP {amount}!",
            premiumSuccess: "⭐ Premium Membership activated for 30 days!",
            paymentConfirm: "Payment of BWP {amount} via {method} completed successfully.",
            priorityBadge: "Priority", premiumBadge: "Premium"
        },
        ts: {
            mainTitle: "🇧🇼 Sepatela sa Botswana · Mahala + Tefelo",
            tagline: "Mela ya mahala • Tefelo ya pele • Meputso • Dipuo tse pedi",
            emergencyMsg: "Tshoganetso: 997/998",
            fontControlTitle: "Taolo ya Ditlhaka", fontFamilyLabel: "Leloko la Tlhaka", fontWeightLabel: "Botebo",
            lineSpacingLabel: "Sebaka", letterSpacingLabel: "Sebaka sa Ditlhaka",
            bookingTitle: "Kwala Mo Meleng", symptomTitle: "Tlhathollo ya Matshwao", aiBtnText: "Kaelo ya AI",
            keyboardTitle: "Khiboto", toggleKeyboardText: "Bontsha", hideKeyboardText: "Tlhama",
            queueBoardTitle: "Ba Emeletseng", servingText: "Ba Alafiwang",
            thPatient: "Mokudi", thWait: "Nako", thStatus: "Maemo", thAction: "Tiragatso",
            callNextText: "Bitsa Mokudi (Admin)", emptyQueue: "✨ Ga go na ba e emetseng",
            waiting: "Ba emetse", inProgress: "Ba alafiwa", served: "Ba alafitswe", serveBtn: "Alafa",
            nameLabel: "Leina *", omangLabel: "Omang *", hospitalLabel: "Tlhopa Sepatela *", reasonLabel: "Lebaka *",
            bookText: "Tsena Mo Meleng", fillFields: "Tsweetswee tlatsa", omangInvalid: "Omang e sa siamang",
            paymentSectionTitle: "Tefelo ya Pele le Meputso",
            prioritySuccess: "✅ O fudusetswe mo maemong a 2 ka BWP 15!",
            expressSuccess: "⚡ Nako ya go emela e fokoditswe!",
            donationSuccess: "❤️ Re leboga mpuso wa BWP {amount}!",
            premiumSuccess: "⭐ Premium e bereka malatsi a 30!",
            paymentConfirm: "Tefelo ya BWP {amount} ka {method} e atlegile.",
            priorityBadge: "Pele", premiumBadge: "Premium"
        }
    };
    
    let currentLang = "en";
    let queueDB = [];
    let currentlyServingIndex = 0;
    let autoRefreshInterval;
    let activeInputElement = null;
    let selectedTier = "priority";
    let selectedMethod = null;
    let customDonationAmount = 0;
    let premiumExpiry = null;
    
    // Payment storage
    let paymentReceipts = [];
    
    function loadData() {
        try {
            const storedQueue = localStorage.getItem("bw_queue_free_v3");
            if(storedQueue) queueDB = JSON.parse(storedQueue);
            const storedServing = localStorage.getItem("bw_serving_free_v3");
            if(storedServing !== null) currentlyServingIndex = parseInt(storedServing);
            const storedPayments = localStorage.getItem("bw_payment_receipts_v3");
            if(storedPayments) paymentReceipts = JSON.parse(storedPayments);
            const storedPremium = localStorage.getItem("bw_premium_expiry_v3");
            if(storedPremium && Date.now() < parseInt(storedPremium)) premiumExpiry = parseInt(storedPremium);
        } catch(e) { console.error("Load error:", e); }
        updateQueueStatuses();
        renderQueueBoard();
        renderRecentPayments();
        updatePremiumBadge();
    }
    
    function saveAll() {
        localStorage.setItem("bw_queue_free_v3", JSON.stringify(queueDB));
        localStorage.setItem("bw_serving_free_v3", currentlyServingIndex);
        localStorage.setItem("bw_payment_receipts_v3", JSON.stringify(paymentReceipts));
        if(premiumExpiry) localStorage.setItem("bw_premium_expiry_v3", premiumExpiry);
        localStorage.setItem("bw_language_free_v3", currentLang);
    }
    
    function updateQueueStatuses() {
        queueDB.forEach((p, idx) => { 
            p.position = idx + 1; 
            if(idx < currentlyServingIndex) p.status = "served"; 
            else if(idx === currentlyServingIndex) p.status = "in_progress"; 
            else p.status = "waiting"; 
        });
        saveAll();
    }
    
    function getPartialName(fullName) { 
        if(!fullName) return "?"; 
        let parts = fullName.trim().split(/\s+/); 
        if(parts.length >= 2) return parts[0] + " " + parts[1].charAt(0) + "."; 
        return parts[0].substring(0, 8);
    }
    
    function escapeHtml(str) { if(!str) return ''; return str.replace(/[&<>]/g, m => ({'&':'&amp;','<':'&lt;','>':'&gt;'})[m]); }
    
    function renderQueueBoard() {
        const t = translations[currentLang];
        const tbody = document.getElementById("queueTableBody");
        const servingSpan = document.getElementById("servingPatient");
        if(!queueDB.length) { 
            tbody.innerHTML = `<tr><td colspan="5" style="text-align:center; padding:40px;">${t.emptyQueue}</td></tr>`; 
            servingSpan.innerText = "—";
            return; 
        }
        let html = "";
        queueDB.forEach((p, idx) => {
            let statusText = p.status === "waiting" ? t.waiting : (p.status === "in_progress" ? t.inProgress : t.served);
            let waitMinutes = 0;
            if(p.status === "waiting") { 
                let positionsAhead = idx - currentlyServingIndex; 
                waitMinutes = positionsAhead * 15; 
                if(p.priority) waitMinutes = Math.floor(waitMinutes / 2);
            }
            let waitDisplay = p.status === "waiting" ? `${waitMinutes} min` : (p.status === "in_progress" ? "Now" : "✓");
            let badges = "";
            if(p.priority) badges += `<span class="priority-badge">🚀 Priority</span>`;
            if(p.premium) badges += `<span class="premium-star">⭐ Premium</span>`;
            let serveButton = p.status !== "served" ? `<button class="serve-btn" data-id="${p.id}" onclick="servePatient('${p.id}')">✅ ${t.serveBtn}</button>` : "<span>✓ Done</span>";
            html += `<tr><td>${idx+1}</td><td>${escapeHtml(getPartialName(p.name))} ${badges}</td><td>${waitDisplay}</td><td>${statusText}</td><td>${serveButton}</td></tr>`;
        });
        tbody.innerHTML = html;
        if(currentlyServingIndex < queueDB.length && queueDB[currentlyServingIndex]) 
            servingSpan.innerText = `${getPartialName(queueDB[currentlyServingIndex].name)} (Position ${currentlyServingIndex+1})`;
        else servingSpan.innerText = "—";
        document.getElementById("queueCounter").innerHTML = queueDB.length ? `${queueDB.length} ${t.waiting}` : "";
    }
    
    window.servePatient = function(id) {
        const patient = queueDB.find(p => p.id === id);
        if(patient && patient.status !== "served") {
            patient.status = "served";
            updateQueueStatuses();
            renderQueueBoard();
            showToast("bookingToast", translations[currentLang].serveConfirm || "Patient served", "#10b981");
        }
    };
    
    function callNextPatient() { 
        if(queueDB.length && currentlyServingIndex < queueDB.length - 1) { 
            currentlyServingIndex++;
            updateQueueStatuses(); 
            renderQueueBoard(); 
            showToast("bookingToast", `📢 Next patient called - Position ${currentlyServingIndex+1}`, "#fbbf24");
        } else if(queueDB.length && currentlyServingIndex === queueDB.length-1) 
            showToast("bookingToast", "No more patients in queue", "#ef4444"); 
        else 
            showToast("bookingToast", "Queue is empty", "#ef4444"); 
    }
    
    function handleBooking() {
        const name = document.getElementById("fullName").value.trim();
        const omang = document.getElementById("omangId").value.trim();
        const hospital = document.getElementById("hospitalSelect").value;
        const reason = document.getElementById("visitReason").value.trim();
        const t = translations[currentLang];
        if(!name || !omang || !hospital || !reason) { alert(t.fillFields); return; }
        if(omang.length < 5 || !/^[A-Za-z0-9]+$/.test(omang)) { alert(t.omangInvalid); return; }
        
        const newPatient = { 
            id: Date.now() + "-" + Math.random().toString(36).substr(2, 8), 
            name, omang, hospital, reason, 
            status: "waiting", timestamp: Date.now(),
            priority: false, premium: premiumExpiry && Date.now() < premiumExpiry
        };
        queueDB.push(newPatient);
        updateQueueStatuses();
        renderQueueBoard();
        showToast("bookingToast", `✅ ${name} added to queue (Position ${queueDB.length})`, "#14b8a6");
        document.getElementById("fullName").value = "";
        document.getElementById("omangId").value = "";
        document.getElementById("visitReason").value = "";
        document.getElementById("hospitalSelect").value = "";
    }
    
    // ======================== PAYMENT SYSTEM ========================
    function generateTransactionId() {
        const date = new Date();
        const yyyymmdd = date.getFullYear() + String(date.getMonth()+1).padStart(2,'0') + String(date.getDate()).padStart(2,'0');
        const random = Math.random().toString(36).substr(2, 4).toUpperCase();
        return `BWP-${yyyymmdd}-${random}`;
    }
    
    function processPayment() {
        if(!selectedMethod) { alert("Please select a payment method"); return; }
        const t = translations[currentLang];
        let amount = 0;
        let tierName = "";
        
        if(selectedTier === "priority") { amount = 15; tierName = "Priority Queue Jump"; }
        else if(selectedTier === "express") { amount = 10; tierName = "Express Service"; }
        else if(selectedTier === "donation") { 
            amount = customDonationAmount || parseInt(document.getElementById("customDonation")?.value) || 10;
            tierName = "Donation";
        }
        else if(selectedTier === "premium") { amount = 25; tierName = "Premium Membership (30 days)"; }
        
        const transactionId = generateTransactionId();
        const receipt = {
            id: transactionId,
            date: new Date().toISOString(),
            tier: selectedTier,
            amount: amount,
            method: selectedMethod,
            description: tierName
        };
        paymentReceipts.unshift(receipt);
        saveAll();
        renderRecentPayments();
        
        // Apply payment effects
        const currentPatientName = document.getElementById("fullName").value.trim();
        if(selectedTier === "priority" && currentPatientName) {
            // Find the current patient being booked and move them to position 2
            const existingPatient = queueDB.find(p => p.name === currentPatientName && p.status === "waiting");
            if(existingPatient) {
                existingPatient.priority = true;
                // Reorder queue: move this patient to index 1 (position 2)
                const currentIndex = queueDB.findIndex(p => p.id === existingPatient.id);
                if(currentIndex > 1 && currentlyServingIndex < currentIndex) {
                    queueDB.splice(currentIndex, 1);
                    queueDB.splice(1, 0, existingPatient);
                    updateQueueStatuses();
                }
            }
        } else if(selectedTier === "premium") {
            premiumExpiry = Date.now() + 30 * 24 * 60 * 60 * 1000;
            saveAll();
            updatePremiumBadge();
        } else if(selectedTier === "express" && currentPatientName) {
            const existingPatient = queueDB.find(p => p.name === currentPatientName);
            if(existingPatient) existingPatient.priority = true;
        }
        
        renderQueueBoard();
        
        // Show confirmation modal
        const modal = document.createElement("div"); modal.className = "modal-overlay";
        modal.innerHTML = `<div class="modal-card"><h2 style="color:var(--primary-glow);">✅ Payment Confirmed</h2>
            <p><strong>Amount:</strong> BWP ${amount}</p><p><strong>Method:</strong> ${selectedMethod}</p>
            <p><strong>Transaction ID:</strong> ${transactionId}</p><p><strong>Service:</strong> ${tierName}</p>
            <button id="closeModalBtn" style="margin-top:1rem;">Close</button></div>`;
        document.body.appendChild(modal);
        document.getElementById("closeModalBtn").onclick = () => modal.remove();
        
        let successMsg = "";
        if(selectedTier === "priority") successMsg = t.prioritySuccess;
        else if(selectedTier === "express") successMsg = t.expressSuccess;
        else if(selectedTier === "donation") successMsg = t.donationSuccess.replace("{amount}", amount);
        else if(selectedTier === "premium") successMsg = t.premiumSuccess;
        showToast("bookingToast", successMsg || t.paymentConfirm.replace("{amount}", amount).replace("{method}", selectedMethod), "#10b981");
    }
    
    function renderRecentPayments() {
        const container = document.getElementById("recentPaymentsList");
        if(!paymentReceipts.length) { container.innerHTML = '<div style="text-align:center; color:var(--text-muted); padding:10px;">No payments yet</div>'; return; }
        let html = "";
        paymentReceipts.slice(0, 5).forEach(p => {
            html += `<div class="payment-item"><strong>${p.date.slice(0,10)}</strong> | BWP ${p.amount} | ${p.method}<br><small>${p.description}</small><br><span style="font-size:0.6rem;">ID: ${p.id.slice(-12)}</span></div>`;
        });
        container.innerHTML = html;
    }
    
    function viewAllPayments() {
        if(!paymentReceipts.length) { alert("No payment history"); return; }
        let historyHtml = "<div class='modal-overlay'><div class='modal-card'><h3>📜 Complete Payment History</h3><div style='max-height:400px; overflow-y:auto;'>";
        paymentReceipts.forEach(p => {
            historyHtml += `<div style="border-bottom:1px solid #333; padding:8px;"><strong>${new Date(p.date).toLocaleString()}</strong><br>Amount: BWP ${p.amount} | Method: ${p.method}<br>Service: ${p.description}<br><span style="font-size:0.65rem;">TXN: ${p.id}</span></div>`;
        });
        historyHtml += `</div><button id="closeHistoryBtn" style="margin-top:1rem;">Close</button></div></div>`;
        const div = document.createElement("div"); div.innerHTML = historyHtml; document.body.appendChild(div);
        document.getElementById("closeHistoryBtn").onclick = () => div.remove();
    }
    
    function updatePremiumBadge() {
        const badge = document.getElementById("premiumUserBadge");
        if(premiumExpiry && Date.now() < premiumExpiry) {
            if(badge) badge.style.display = "inline-block";
        } else if(badge) badge.style.display = "none";
    }
    
    // AI Symptom Checker
    function handleAI() {
        const symptoms = document.getElementById("symptomInput").value.trim();
        const t = translations[currentLang];
        if(!symptoms) { alert("Please describe symptoms"); return; }
        document.getElementById("aiToast").innerHTML = `<strong>🧠 AI Recommendation</strong><br><br>Based on your symptoms, please visit the nearest clinic for consultation. If emergency, call 997.`;
        document.getElementById("aiToast").style.display = "block";
        setTimeout(() => document.getElementById("aiToast").style.display = "none", 6000);
    }
    
    // Event Setup
    function setupEventListeners() {
        document.getElementById("bookBtn").onclick = handleBooking;
        document.getElementById("getAIBtn").onclick = handleAI;
        document.getElementById("callNextBtn").onclick = () => document.getElementById("adminPinPanel").style.display = "block";
        document.getElementById("verifyPinBtn").onclick = () => { 
            if(document.getElementById("adminPin").value === "1234") { callNextPatient(); document.getElementById("adminPinPanel").style.display = "none"; document.getElementById("adminPin").value = ""; } 
            else alert("Wrong PIN"); 
        };
        document.getElementById("processPaymentBtn").onclick = processPayment;
        document.getElementById("viewAllPaymentsBtn").onclick = viewAllPayments;
        
        // Tier selection
        document.querySelectorAll(".tier-btn").forEach(btn => {
            btn.onclick = () => {
                document.querySelectorAll(".tier-btn").forEach(b => b.classList.remove("active-tier"));
                btn.classList.add("active-tier");
                selectedTier = btn.getAttribute("data-tier");
                document.getElementById("donationSection").style.display = selectedTier === "donation" ? "block" : "none";
            };
        });
        
        // Payment method selection
        document.querySelectorAll(".payment-method-btn").forEach(btn => {
            btn.onclick = () => {
                document.querySelectorAll(".payment-method-btn").forEach(b => b.classList.remove("selected"));
                btn.classList.add("selected");
                selectedMethod = btn.getAttribute("data-method");
            };
        });
        
        // Donation amounts
        document.querySelectorAll(".donation-amount").forEach(amt => {
            amt.onclick = () => {
                document.querySelectorAll(".donation-amount").forEach(a => a.classList.remove("active"));
                amt.classList.add("active");
                customDonationAmount = parseInt(amt.getAttribute("data-amount"));
                if(document.getElementById("customDonation")) document.getElementById("customDonation").value = customDonationAmount;
            };
        });
        if(document.getElementById("customDonation")) {
            document.getElementById("customDonation").oninput = (e) => customDonationAmount = parseInt(e.target.value) || 0;
        }
    }
    
    // Font & Accessibility
    function loadFontPreferences() {
        let ff = localStorage.getItem("font_family_free"); if(ff) document.body.style.fontFamily = ff;
        let fw = localStorage.getItem("font_weight_free"); if(fw) { document.body.classList.remove("font-light","font-regular","font-bold"); document.body.classList.add(fw); }
        let lh = localStorage.getItem("line_height_free"); if(lh) { document.getElementById("lineHeightSlider").value = lh; document.getElementById("appContainer").style.lineHeight = lh; }
        let ls = localStorage.getItem("letter_spacing_free"); if(ls) { document.getElementById("letterSpacingSlider").value = ls; document.getElementById("appContainer").style.letterSpacing = ls+"px"; }
        document.getElementById("fontFamilySelect").onchange = (e) => { document.body.style.fontFamily = e.target.value; localStorage.setItem("font_family_free", e.target.value); };
        document.getElementById("weightLight").onclick = () => setWeight("font-light");
        document.getElementById("weightRegular").onclick = () => setWeight("font-regular");
        document.getElementById("weightBold").onclick = () => setWeight("font-bold");
        document.getElementById("lineHeightSlider").oninput = (e) => { document.getElementById("appContainer").style.lineHeight = e.target.value; localStorage.setItem("line_height_free", e.target.value); document.getElementById("lineHeightValue").innerText = e.target.value; };
        document.getElementById("letterSpacingSlider").oninput = (e) => { document.getElementById("appContainer").style.letterSpacing = e.target.value+"px"; localStorage.setItem("letter_spacing_free", e.target.value); document.getElementById("letterSpacingValue").innerText = e.target.value+"px"; };
    }
    function setWeight(className) { document.body.classList.remove("font-light","font-regular","font-bold"); document.body.classList.add(className); localStorage.setItem("font_weight_free", className); }
    document.getElementById("fontUp").onclick = () => { let cur = parseFloat(getComputedStyle(document.body).fontSize); document.body.style.fontSize = Math.min(cur*1.1, 28)+"px"; };
    document.getElementById("fontDown").onclick = () => { let cur = parseFloat(getComputedStyle(document.body).fontSize); document.body.style.fontSize = Math.max(cur*0.9, 12)+"px"; };
    let contrast=false; document.getElementById("contrastBtn").onclick=()=>{ document.body.style.background = contrast ? "" : "#000"; document.body.style.color = contrast ? "" : "#ffffe0"; contrast=!contrast; };
    
    // Keyboard
    function buildKeyboard() {
        const container = document.getElementById("dynamicKbContainer"); if(!container) return;
        container.innerHTML = "";
        const rows = [["1","2","3","4","5","6","7","8","9","0"],["q","w","e","r","t","y","u","i","o","p"],["a","s","d","f","g","h","j","k","l"],["z","x","c","v","b","n","m"],["space","backspace","clear"],["tab","enter"]];
        rows.forEach(row => { 
            let rowDiv = document.createElement("div"); rowDiv.className = "keyboard-row"; 
            row.forEach(k => { 
                let btn = document.createElement("button"); btn.className = "key-btn"; 
                btn.innerText = {space:"␣ Space", backspace:"⌫", clear:"🗑", tab:"↹", enter:"⏎"}[k] || k; 
                btn.onclick = () => { if(!activeInputElement) activeInputElement = document.getElementById("fullName"); 
                    if(k === "backspace") activeInputElement.value = activeInputElement.value.slice(0,-1); 
                    else if(k === "space") activeInputElement.value += " "; 
                    else if(k === "clear") activeInputElement.value = ""; 
                    else if(k === "tab") { let ids = ["fullName","omangId","visitReason"]; let idx = ids.findIndex(id => document.getElementById(id) === activeInputElement); activeInputElement = document.getElementById(ids[(idx+1)%ids.length]); if(activeInputElement) activeInputElement.focus(); } 
                    else activeInputElement.value += k; 
                    activeInputElement.dispatchEvent(new Event('input')); 
                }; rowDiv.appendChild(btn); 
            }); container.appendChild(rowDiv); 
        });
    }
    document.querySelectorAll("#fullName, #omangId, #visitReason, #symptomInput").forEach(el => { el.addEventListener("focus", () => activeInputElement = el); });
    document.getElementById("toggleKeyboardBtn").onclick = () => { let kb = document.getElementById("onscreenKeyboard"); kb.style.display = kb.style.display === "none" ? "block" : "none"; if(kb.style.display === "block" && !document.getElementById("dynamicKbContainer").children.length) buildKeyboard(); };
    
    // Language switching
    function updateAllText() { 
        const t = translations[currentLang]; 
        for(let key in t) { let el = document.getElementById(key); if(el && typeof t[key] === 'string') el.innerText = t[key]; }
        document.getElementById("bookingTitle").innerHTML = t.bookingTitle + ' <span class="free-badge">✓ FREE</span>';
        renderQueueBoard(); 
    }
    document.getElementById("langEn").onclick = () => { currentLang = "en"; updateAllText(); saveAll(); };
    document.getElementById("langTs").onclick = () => { currentLang = "ts"; updateAllText(); saveAll(); };
    
    function showToast(id, msg, col) { 
        let el = document.getElementById(id); 
        if(el) { el.innerText = msg; el.style.display = "block"; el.style.borderLeftColor = col; setTimeout(() => el.style.display = "none", 4000); } 
    }
    
    setInterval(() => { renderQueueBoard(); if(premiumExpiry && Date.now() > premiumExpiry) { premiumExpiry = null; updatePremiumBadge(); saveAll(); } }, 10000);
    
    function init() { 
        let savedLang = localStorage.getItem("bw_language_free_v3"); 
        if(savedLang === "ts") currentLang = "ts"; 
        loadData(); loadFontPreferences(); updateAllText(); buildKeyboard(); setupEventListeners();
        selectedMethod = null; selectedTier = "priority";
    }
    init();
</script>
</body>
</html>
