<!DOCTYPE html>
<html lang="zh-HK">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>開支申請流程圖</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+HK:wght@400;500;700;900&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Noto Sans HK', sans-serif;
            background: #f8f9fa;
            overflow-x: hidden;
        }
        
        .grain {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
            opacity: 0.03;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E");
        }

        .alert-banner {
            background: linear-gradient(90deg, #ff416c 0%, #ff4b2b 100%);
            background-size: 200% 200%;
            animation: gradientShift 5s ease infinite;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .flow-step {
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .flow-step:hover {
            transform: translateY(-4px) scale(1.01);
            box-shadow: 0 20px 40px -10px rgba(0,0,0,0.15);
        }

        .condition-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            position: relative;
            overflow: hidden;
        }

        .condition-card::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.2) 1px, transparent 1px);
            background-size: 4px 4px;
            opacity: 0.3;
            animation: grain 8s steps(10) infinite;
        }

        @keyframes grain {
            0%, 100% { transform: translate(0, 0); }
            10% { transform: translate(-5%, -10%); }
            20% { transform: translate(-15%, 5%); }
            30% { transform: translate(7%, -25%); }
            40% { transform: translate(-5%, 25%); }
            50% { transform: translate(-15%, 10%); }
            60% { transform: translate(15%, 0%); }
            70% { transform: translate(0%, 15%); }
            80% { transform: translate(3%, 35%); }
            90% { transform: translate(-10%, 10%); }
        }

        .step-number {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            box-shadow: 0 4px 15px rgba(245, 87, 108, 0.4);
        }

        .amount-badge {
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-5px); }
        }

        .glass-panel {
            background: rgba(255, 255, 255, 0.7);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.3);
        }

        .hover-reveal {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-out;
        }

        .flow-step:hover .hover-reveal {
            max-height: 200px;
        }

        .path-highlight {
            position: relative;
        }

        .path-highlight::after {
            content: '';
            position: absolute;
            left: 0;
            bottom: 0;
            width: 0;
            height: 3px;
            background: #f5576c;
            transition: width 0.3s ease;
        }

        .flow-step:hover .path-highlight::after {
            width: 100%;
        }

        .calendar-icon {
            animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: .7; }
        }

        @media print {
            .no-print { display: none; }
            .print-break { page-break-inside: avoid; }
            .alert-banner { background: #dc2626 !important; -webkit-print-color-adjust: exact; }
        }
    </style>
</head>
<body class="min-h-screen text-slate-800">

    <!-- Grain Texture Overlay -->
    <div class="grain"></div>

    <!-- Alert Banner: Important Dates -->
    <div class="alert-banner text-white py-4 px-6 relative z-20 shadow-lg no-print">
        <div class="max-w-6xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4">
            <div class="flex items-center gap-3">
                <div class="calendar-icon bg-white/20 p-2 rounded-lg backdrop-blur-sm">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"/>
                    </svg>
                </div>
                <div class="font-bold text-lg">
                    重要截止時間：每月 <span class="text-2xl mx-1">10日</span> 及 <span class="text-2xl mx-1">25日</span> （含零用現金申請）
                </div>
            </div>
            <div class="flex items-center gap-2 text-sm bg-black/20 px-4 py-2 rounded-full backdrop-blur-sm">
                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"/>
                </svg>
                <span>遇假期將提前辦理</span>
            </div>
        </div>
    </div>

    <!-- Header -->
    <header class="relative z-10 bg-slate-900 text-white py-12 px-6 overflow-hidden border-b border-slate-800">
        <div class="absolute inset-0 opacity-20">
            <div class="absolute top-0 left-0 w-96 h-96 bg-purple-500 rounded-full blur-3xl -translate-x-1/2 -translate-y-1/2"></div>
            <div class="absolute bottom-0 right-0 w-96 h-96 bg-pink-500 rounded-full blur-3xl translate-x-1/2 translate-y-1/2"></div>
        </div>
        <div class="max-w-6xl mx-auto relative z-10">
            <div class="flex items-center gap-3 mb-4">
                <div class="w-12 h-1 bg-gradient-to-r from-pink-500 to-purple-500"></div>
                <span class="text-sm uppercase tracking-widest text-slate-400">Standard Operating Procedure</span>
            </div>
            <h1 class="text-5xl md:text-7xl font-black mb-4 bg-clip-text text-transparent bg-gradient-to-r from-white via-purple-200 to-pink-200">
                開支申請流程圖
            </h1>
            <p class="text-slate-400 text-lg max-w-2xl">
                規範化採購流程，確保財務審批合規高效
            </p>
        </div>
    </header>

    <main class="relative z-10 max-w-6xl mx-auto p-6 space-y-12">

        <!-- Stage 1: Preparation -->
        <section class="print-break">
            <div class="flex items-center gap-4 mb-8">
                <div class="step-number w-16 h-16 rounded-2xl flex items-center justify-center text-3xl font-bold text-white">
                    1
                </div>
                <div>
                    <h2 class="text-3xl font-bold text-slate-900">購置前準備</h2>
                    <p class="text-slate-500">依據金額門檻採取不同審批路徑</p>
                </div>
            </div>

            <div class="grid md:grid-cols-3 gap-6">
                <!-- Under $300 -->
                <div class="flow-step group bg-white rounded-3xl p-6 shadow-lg border border-slate-100 cursor-pointer transform transition-all">
                    <div class="flex justify-between items-start mb-4">
                        <span class="amount-badge inline-block px-4 py-2 bg-emerald-100 text-emerald-800 rounded-full text-sm font-bold border-2 border-emerald-200">
                            &lt; $300
                        </span>
                        <svg class="w-6 h-6 text-emerald-500 opacity-0 group-hover:opacity-100 transition-opacity" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/>
                        </svg>
                    </div>
                    <h3 class="text-xl font-bold mb-3 text-slate-800">簡易採購</h3>
                    <div class="space-y-3">
                        <div class="flex items-start gap-2">
                            <div class="w-2 h-2 rounded-full bg-emerald-500 mt-2 flex-shrink-0"></div>
                            <p class="text-slate-600">向<strong>阿清</strong>索取「物資購置表」</p>
                        </div>
                        <div class="hover-reveal">
                            <div class="pt-4 mt-4 border-t border-slate-100 text-sm text-slate-500">
                                <p>✓ 無需額外審批</p>
                                <p class="mt-1">✓ 適用於日常小額文具、雜項</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- $300-$2000 -->
                <div class="flow-step group bg-white rounded-3xl p-6 shadow-lg border border-slate-100 cursor-pointer transform transition-all">
                    <div class="flex justify-between items-start mb-4">
                        <span class="amount-badge inline-block px-4 py-2 bg-amber-100 text-amber-800 rounded-full text-sm font-bold border-2 border-amber-200">
                            &gt; $300
                        </span>
                        <svg class="w-6 h-6 text-amber-500 opacity-0 group-hover:opacity-100 transition-opacity" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/>
                        </svg>
                    </div>
                    <h3 class="text-xl font-bold mb-3 text-slate-800">標準審批</h3>
                    <div class="space-y-3">
                        <div class="flex items-start gap-2">
                            <div class="w-2 h-2 rounded-full bg-amber-500 mt-2 flex-shrink-0"></div>
                            <p class="text-slate-600">向<strong>阿清</strong>索取「物資購置表」</p>
                        </div>
                        <div class="flex items-start gap-2">
                            <div class="w-2 h-2 rounded-full bg-amber-500 mt-2 flex-shrink-0"></div>
                            <p class="text-slate-600">需向<strong>主任</strong>申請並獲得簽名</p>
                        </div>
                        <div class="hover-reveal">
                            <div class="pt-4 mt-4 border-t border-slate-100 text-sm text-slate-500">
                                <p>⚠ 必須提前獲得書面批准</p>
                                <p class="mt-1">⚠ 事後補簽無效</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Over $2000 -->
                <div class="flow-step group bg-white rounded-3xl p-6 shadow-lg border-2 border-purple-200 cursor-pointer transform transition-all relative overflow-hidden">
                    <div class="absolute top-0 right-0 w-32 h-32 bg-purple-100 rounded-full blur-3xl -translate-y-1/2 translate-x-1/2 opacity-50"></div>
                    <div class="flex justify-between items-start mb-4 relative z-10">
                        <span class="amount-badge inline-block px-4 py-2 bg-purple-100 text-purple-800 rounded-full text-sm font-bold border-2 border-purple-300">
                            &gt; $2000
                        </span>
                        <svg class="w-6 h-6 text-purple-500 opacity-0 group-hover:opacity-100 transition-opacity" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/>
                        </svg>
                    </div>
                    <h3 class="text-xl font-bold mb-3 text-slate-800 relative z-10">嚴格採購</h3>
                    <div class="space-y-3 relative z-10">
                        <div class="flex items-start gap-2">
                            <div class="w-2 h-2 rounded-full bg-purple-500 mt-2 flex-shrink-0"></div>
                            <p class="text-slate-600">向<strong>阿清</strong>索取「物資購置表」</p>
                        </div>
                        <div class="flex items-start gap-2">
                            <div class="w-2 h-2 rounded-full bg-purple-600 mt-2 flex-shrink-0"></div>
                            <p class="text-slate-600">提供<strong>三間公司報價</strong></p>
                        </div>
                        <div class="flex items-start gap-2">
                            <div class="w-2 h-2 rounded-full bg-purple-700 mt-2 flex-shrink-0"></div>
                            <p class="text-slate-600">主任挑選其一並<strong>寫明原因</strong></p>
                        </div>
                        <div class="hover-reveal">
                            <div class="pt-4 mt-4 border-t border-slate-100 text-sm text-slate-500 bg-purple-50 p-3 rounded-lg">
                                <p>📋 需附報價單正本或電郵截圖</p>
                                <p class="mt-1">✍ 選擇理由必須具體（非僅寫「價格最低」）</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Arrow Down -->
            <div class="flex justify-center my-8">
                <svg class="w-8 h-16 text-slate-300 animate-bounce" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3"/>
                </svg>
            </div>
        </section>

        <!-- Stage 2: Purchase & Payment -->
        <section class="print-break">
            <div class="flex items-center gap-4 mb-8">
                <div class="step-number w-16 h-16 rounded-2xl flex items-center justify-center text-3xl font-bold text-white" style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);">
                    2
                </div>
                <div>
                    <h2 class="text-3xl font-bold text-slate-900">購買與支付</h2>
                    <p class="text-slate-500">根據付款方式決定文件要求</p>
                </div>
            </div>

            <div class="grid md:grid-cols-2 gap-8">
                <!-- Personal Payment -->
                <div class="flow-step bg-gradient-to-br from-slate-50 to-slate-100 rounded-3xl p-8 border border-slate-200 relative overflow-hidden">
                    <div class="absolute top-0 right-0 p-4 opacity-10">
                        <svg class="w-24 h-24" fill="currentColor" viewBox="0 0 24 24"><path d="M20 4H4c-1.11 0-1.99.89-1.99 2L2 18c0 1.11.89 2 2 2h16c1.11 0 2-.89 2-2V6c0-1.11-.89-2-2-2zm0 14H4v-6h16v6zm0-10H4V6h16v2z"/></svg>
                    </div>
                    <div class="relative z-10">
                        <div class="inline-flex items-center gap-2 px-4 py-2 bg-white rounded-full shadow-sm mb-4 border border-slate-200">
                            <span class="w-2 h-2 rounded-full bg-green-500"></span>
                            <span class="font-bold text-slate-700">個人支付</span>
                        </div>
                        <p class="text-slate-600 mb-4">員工自行買入，事後憑單據報銷</p>
                        
                        <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-200 space-y-3">
                            <h4 class="font-bold text-slate-800 flex items-center gap-2">
                                <svg class="w-5 h-5 text-blue-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/>
                                </svg>
                                必需文件
                            </h4>
                            <ul class="space-y-2 text-sm text-slate-600">
                                <li class="flex items-center gap-2 path-highlight">
                                    <span class="w-6 h-6 rounded-full bg-blue-100 text-blue-600 flex items-center justify-center text-xs font-bold">1</span>
                                    付款截圖（電子支付記錄）
                                </li>
                                <li class="flex items-center gap-2 path-highlight">
                                    <span class="w-6 h-6 rounded-full bg-blue-100 text-blue-600 flex items-center justify-center text-xs font-bold">2</span>
                                    收據（Receipt）
                                </li>
                                <li class="flex items-center gap-2 path-highlight">
                                    <span class="w-6 h-6 rounded-full bg-blue-100 text-blue-600 flex items-center justify-center text-xs font-bold">3</span>
                                    發票（Invoice）
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>

                <!-- Non-Personal Payment -->
                <div class="flow-step bg-gradient-to-br from-indigo-50 to-purple-50 rounded-3xl p-8 border border-indigo-200 relative overflow-hidden">
                    <div class="absolute top-0 right-0 p-4 opacity-10">
                        <svg class="w-24 h-24" fill="currentColor" viewBox="0 0 24 24"><path d="M14 2H6c-1.1 0-1.99.9-1.99 2L4 20c0 1.1.89 2 1.99 2H18c1.1 0 2-.9 2-2V8l-6-6zm2 16H8v-2h8v2zm0-4H8v-2h8v2zm-3-5V3.5L18.5 9H13z"/></svg>
                    </div>
                    <div class="relative z-10">
                        <div class="inline-flex items-center gap-2 px-4 py-2 bg-white rounded-full shadow-sm mb-4 border border-indigo-200">
                            <span class="w-2 h-2 rounded-full bg-indigo-500"></span>
                            <span class="font-bold text-slate-700">非個人支付</span>
                        </div>
                        <p class="text-sm text-indigo-600 mb-2 font-medium">適用於：大額電器、維修等</p>
                        
                        <div class="bg-white rounded-2xl p-6 shadow-sm border border-indigo-100 space-y-3">
                            <h4 class="font-bold text-slate-800 flex items-center gap-2">
                                <svg class="w-5 h-5 text-indigo-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z"/>
                                </svg>
                                支票申請要求
                            </h4>
                            <div class="p-4 bg-indigo-50 rounded-xl border-l-4 border-indigo-500">
                                <p class="text-indigo-900 font-bold mb-1">發票抬頭必須為：</p>
                                <p class="text-indigo-700 text-lg font-mono">[公司名稱]</p>
                            </div>
                            <p class="text-sm text-slate-500 mt-2">使用支票支付，無需員工墊支</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Arrow Down -->
            <div class="flex justify-center my-8">
                <svg class="w-8 h-16 text-slate-300 animate-bounce" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3"/>
                </svg>
            </div>
        </section>

        <!-- Stage 3: Settlement -->
        <section class="print-break">
            <div class="flex items-center gap-4 mb-8">
                <div class="step-number w-16 h-16 rounded-2xl flex items-center justify-center text-3xl font-bold text-white" style="background: linear-gradient(135deg, #fa709a 0%, #fee140 100%);">
                    3
                </div>
                <div>
                    <h2 class="text-3xl font-bold text-slate-900">領取與結算</h2>
                    <p class="text-slate-500">財務處理與最終交收</p>
                </div>
            </div>

            <div class="glass-panel rounded-3xl p-8 shadow-2xl relative overflow-hidden">
                <div class="absolute inset-0 bg-gradient-to-br from-pink-50 to-yellow-50 opacity-50"></div>
                
                <div class="relative z-10 grid md:grid-cols-2 gap-8">
                    <!-- Left: Check Process -->
                    <div class="space-y-6">
                        <div class="flow-step bg-white rounded-2xl p-6 shadow-md border border-pink-100">
                            <div class="flex items-center gap-3 mb-4">
                                <div class="w-12 h-12 rounded-full bg-pink-100 flex items-center justify-center">
                                    <svg class="w-6 h-6 text-pink-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/>
                                    </svg>
                                </div>
                                <h3 class="text-lg font-bold text-slate-800">1. 支票發放</h3>
                            </div>
                            <ul class="space-y-2 text-sm text-slate-600 ml-2">
                                <li class="flex items-start gap-2">
                                    <span class="text-pink-500 mt-1">→</span>
                                    <span>阿清收到發票後申請支票</span>
                                </li>
                                <li class="flex items-start gap-2">
                                    <span class="text-pink-500 mt-1">→</span>
                                    <span>成功後通知領取</span>
                                </li>
                            </ul>
                        </div>

                        <div class="flow-step bg-white rounded-2xl p-6 shadow-md border border-yellow-200">
                            <div class="flex items-center gap-3 mb-4">
                                <div class="w-12 h-12 rounded-full bg-yellow-100 flex items-center justify-center">
                                    <svg class="w-6 h-6 text-yellow-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7h12m0 0l-4-4m4 4l-4 4m0 6H4m0 0l4 4m-4-4l4-4"/>
                                    </svg>
                                </div>
                                <h3 class="text-lg font-bold text-slate-800">2. 交收程序</h3>
                            </div>
                            <div class="bg-yellow-50 rounded-xl p-4 border-l-4 border-yellow-500">
                                <p class="text-sm text-slate-700 font-bold mb-2">商家領取支票時需同時提交：</p>
                                <div class="flex gap-4 text-sm">
                                    <span class="px-3 py-1 bg-white rounded-lg border border-yellow-300">發票</span>
                                    <span class="px-3 py-1 bg-white rounded-lg border border-yellow-300">支票正本</span>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Right: Summary -->
                    <div class="bg-slate-900 text-white rounded-2xl p-8 shadow-xl">
                        <h3 class="text-2xl font-bold mb-6 flex items-center gap-2">
                            <svg class="w-6 h-6 text-yellow-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"/>
                            </svg>
                            關鍵檢查點
                        </h3>
                        <ul class="space-y-4">
                            <li class="flex items-start gap-3">
                                <span class="w-6 h-6 rounded-full bg-green-500 text-xs flex items-center justify-center flex-shrink-0 mt-0.5">✓</span>
                                <span class="text-slate-300"><strong class="text-white">個人支付</strong>的員工：是否齊全三張單據？</span>
                            </li>
                            <li class="flex items-start gap-3">
                                <span class="w-6 h-6 rounded-full bg-green-500 text-xs flex items-center justify-center flex-shrink-0 mt-0.5">✓</span>
                                <span class="text-slate-300"><strong class="text-white">支票支付</strong>的發票：抬頭是否正確？</span>
                            </li>
                            <li class="flex items-start gap-3">
                                <span class="w-6 h-6 rounded-full bg-green-500 text-xs flex items-center justify-center flex-shrink-0 mt-0.5">✓</span>
                                <span class="text-slate-300"><strong class="text-white">大額採購</strong>：是否有三份報價及主任選擇理由？</span>
                            </li>
                        </ul>
                        
                        <div class="mt-8 pt-6 border-t border-slate-700">
                            <p class="text-sm text-slate-400 italic">
                                "所有文件應在採購後5個工作日內提交阿清處理"
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Important Dates & Notes Section -->
        <section class="print-break mt-12">
            <div class="bg-gradient-to-br from-rose-50 to-orange-50 rounded-3xl p-8 border-2 border-rose-200 shadow-xl relative overflow-hidden">
                <div class="absolute top-0 right-0 w-64 h-64 bg-rose-200 rounded-full blur-3xl opacity-20 -translate-y-1/2 translate-x-1/2"></div>
                
                <div class="relative z-10">
                    <div class="flex items-center gap-3 mb-6">
                        <div class="bg-gradient-to-br from-rose-500 to-orange-500 p-3 rounded-2xl shadow-lg">
                            <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
                            </svg>
                        </div>
                        <h2 class="text-3xl font-bold text-slate-900">重要日期與注意事項</h2>
                    </div>

                    <div class="grid md:grid-cols-2 gap-8">
                        <!-- Deadline Info -->
                        <div class="bg-white rounded-2xl p-6 shadow-lg border border-rose-100">
                            <div class="flex items-center gap-2 mb-4 text-rose-600 font-bold text-lg">
                                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"/>
                                </svg>
                                申請截止時間
                            </div>
                            <div class="space-y-4">
                                <div class="flex items-center gap-4 p-4 bg-rose-50 rounded-xl border-l-4 border-rose-500">
                                    <div class="text-3xl font-black text-rose-600">10</div>
                                    <div class="text-slate-700">每月10日<br><span class="text-sm text-slate-500">適用於所有開支申請及零用現金</span></div>
                                </div>
                                <div class="flex items-center gap-4 p-4 bg-orange-50 rounded-xl border-l-4 border-orange-500">
                                    <div class="text-3xl font-black text-orange-600">25</div>
                                    <div class="text-slate-700">每月25日<br><span class="text-sm text-slate-500">適用於所有開支申請及零用現金</span></div>
                                </div>
                            </div>
                        </div>

                        <!-- Special Notes -->
                        <div class="space-y-4">
                            <div class="bg-white rounded-2xl p-6 shadow-lg border border-amber-200 flex items-start gap-4">
                                <div class="bg-amber-100 p-2 rounded-lg flex-shrink-0">
                                    <svg class="w-6 h-6 text-amber-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"/>
                                    </svg>
                                </div>
                                <div>
                                    <h4 class="font-bold text-slate-900 mb-1">假期調整</h4>
                                    <p class="text-slate-600 text-sm">如遇假期將<span class="font-bold text-amber-700">提前</span>辦理，請留意辦公室公告</p>
                                </div>
                            </div>

                            <div class="bg-white rounded-2xl p-6 shadow-lg border border-blue-200 flex items-start gap-4">
                                <div class="bg-blue-100 p-2 rounded-lg flex-shrink-0">
                                    <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
                                    </svg>
                                </div>
                                <div>
                                    <h4 class="font-bold text-slate-900 mb-1">支票通知</h4>
                                    <p class="text-slate-600 text-sm">支票開出後，<strong>阿清會另行通知</strong>領取時間，請勿自行前往財務部查詢</p>
                                </div>
                            </div>

                            <div class="bg-slate-800 text-white rounded-2xl p-6 shadow-lg">
                                <div class="flex items-center gap-2 mb-2 text-yellow-400 font-bold">
                                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
                                    </svg>
                                    溫馨提示
                                </div>
                                <p class="text-slate-300 text-sm">建議在截止日前 <strong>2-3 個工作天</strong>提交申請，預留時間處理文件補充或修改</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Quick Reference Card -->
        <section class="print-break mt-8 mb-24">
            <div class="bg-gradient-to-r from-slate-800 to-slate-900 rounded-3xl p-8 text-white shadow-2xl">
                <h3 class="text-2xl font-bold mb-6 text-center">快速參考：金額門檻對照表</h3>
                <div class="grid md:grid-cols-3 gap-6 text-center">
                    <div class="p-4 rounded-2xl bg-white/10 backdrop-blur border border-white/20">
                        <div class="text-3xl font-bold text-emerald-400 mb-2">&lt; $300</div>
                        <div class="text-sm text-slate-300">僅需購置表</div>
                    </div>
                    <div class="p-4 rounded-2xl bg-white/10 backdrop-blur border border-white/20">
                        <div class="text-3xl font-bold text-amber-400 mb-2">$300 - $2,000</div>
                        <div class="text-sm text-slate-300">購置表 + 主任簽名</div>
                    </div>
                    <div class="p-4 rounded-2xl bg-white/10 backdrop-blur border border-white/20">
                        <div class="text-3xl font-bold text-pink-400 mb-2">&gt; $2,000</div>
                        <div class="text-sm text-slate-300">購置表 + 三份報價 + 書面理由</div>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- Print Button -->
    <div class="fixed bottom-8 right-8 no-print">
        <button onclick="window.print()" class="bg-slate-900 text-white px-6 py-3 rounded-full shadow-2xl hover:bg-slate-800 transition-all flex items-center gap-2 group">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 17h2a2 2 0 002-2v-4a2 2 0 00-2-2H5a2 2 0 00-2 2v4a2 2 0 002 2h2m2 4h6a2 2 0 002-2v-4a2 2 0 00-2-2H9a2 2 0 00-2 2v4a2 2 0 002 2zm8-12V5a2 2 0 00-2-2H9a2 2 0 00-2 2v4h10z"/>
            </svg>
            列印流程圖
            <span class="hidden group-hover:inline text-xs opacity-75">(Ctrl+P)</span>
        </button>
    </div>

    <script>
        // Add smooth scroll behavior
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                document.querySelector(this.getAttribute('href')).scrollIntoView({
                    behavior: 'smooth'
                });
            });
        });

        // Add intersection observer for scroll animations
        const observerOptions = {
            threshold: 0.1,
            rootMargin: '0px 0px -50px 0px'
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.opacity = '1';
                    entry.target.style.transform = 'translateY(0)';
                }
            });
        }, observerOptions);

        document.querySelectorAll('.flow-step').forEach((el, index) => {
            el.style.opacity = '0';
            el.style.transform = 'translateY(20px)';
            el.style.transition = `all 0.6s cubic-bezier(0.4, 0, 0.2, 1) ${index * 0.1}s`;
            observer.observe(el);
        });
    </script>
</body>
</html>
