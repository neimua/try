```html
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>TOKYO EXPRESS // 兩天一夜東京快閃網頁手冊</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=SF+Pro+Display:wght@400;500;600;700&family=Noto+Sans+TC:wght@400;500;700;900&display=swap');
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, "SF Pro Display", "Noto Sans TC", sans-serif;
            background: #0f172a; /* 深色背景，讓中間的模擬手機視窗更顯眼 */
            overflow-x: hidden;
        }

        /* 自訂滾動條 */
        ::-webkit-scrollbar {
            width: 4px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(241, 245, 249, 0.1);
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(148, 163, 184, 0.3);
            border-radius: 10px;
        }

        /* 解決 iOS 彈性滾動與底欄遮擋問題 */
        .safe-bottom {
            padding-bottom: calc(env(safe-area-inset-bottom) + 80px);
        }
    </style>
</head>
<body class="flex items-center justify-center min-h-screen md:py-6">

    <!-- 主體容器 (在電腦端模擬成手機，在手機端滿版) -->
    <div class="w-full max-w-md bg-slate-50 min-h-screen md:min-h-[850px] md:max-h-[900px] md:rounded-[40px] md:shadow-[0_25px_60px_-15px_rgba(0,0,0,0.5)] md:border-[10px] md:border-slate-800 flex flex-col justify-between relative overflow-hidden">
        
        <!-- 頂部時間與雙時區顯示 -->
        <header class="bg-gradient-to-r from-slate-900 via-indigo-950 to-slate-900 text-white pt-6 pb-5 px-5 rounded-b-[32px] shadow-lg sticky top-0 z-40">
            <div class="flex justify-between items-center mb-3">
                <div class="flex items-center gap-1.5">
                    <span class="text-xs tracking-widest text-indigo-400 font-bold uppercase">Tokyo Express</span>
                    <span class="bg-pink-500/20 text-pink-400 text-[10px] px-2 py-0.5 rounded-full font-bold">⚡ 2D1N</span>
                </div>
                <div class="flex gap-2 text-[10px] text-slate-300 bg-black/20 px-2.5 py-1 rounded-full backdrop-blur-md">
                    <span id="clock-tpe">TPE 11:50</span>
                    <span class="text-slate-500">|</span>
                    <span id="clock-tyo" class="text-amber-400 font-bold">TYO 12:50</span>
                </div>
            </div>
            
            <div class="flex justify-between items-end">
                <div>
                    <h1 class="text-2xl font-black tracking-tight bg-gradient-to-r from-white to-slate-200 bg-clip-text text-transparent">東京甜蜜快閃</h1>
                    <p class="text-[11px] text-slate-400 mt-0.5">與先生的新宿、豪德寺、鐵塔快閃之旅</p>
                </div>
                <div class="text-right">
                    <div id="general-progress-badge" class="bg-indigo-500/10 border border-indigo-400/20 px-3 py-1 rounded-xl text-xs font-bold text-indigo-300">
                        準備度 0%
                    </div>
                </div>
            </div>
        </header>

        <!-- 主體滑動內容區域 -->
        <main class="flex-grow overflow-y-auto px-4 py-4 safe-bottom">
            
            <!-- ==================== TAB 1: CHECKLIST ==================== -->
            <section id="sec-checklist" class="tab-section space-y-4">
                <div class="bg-white rounded-3xl p-5 shadow-sm border border-slate-100">
                    <div class="flex justify-between items-center mb-4">
                        <div class="flex items-center gap-2">
                            <span class="text-lg">🧳</span>
                            <h2 class="text-base font-bold text-slate-800">出發前最終檢查</h2>
                        </div>
                        <button onclick="resetChecklist()" class="text-xs text-slate-400 hover:text-red-500 transition-colors">重置所有</button>
                    </div>

                    <!-- 進度條 -->
                    <div class="space-y-1 mb-4">
                        <div class="flex justify-between text-xs font-semibold text-slate-500">
                            <span>必備清單完成進度</span>
                            <span id="chk-progress-txt">0/6</span>
                        </div>
                        <div class="w-full bg-slate-100 h-2.5 rounded-full overflow-hidden">
                            <div id="chk-progress-bar" class="h-full bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 rounded-full transition-all duration-300" style="width: 0%"></div>
                        </div>
                    </div>

                    <!-- 列表容器 -->
                    <div id="checklist-container" class="space-y-2.5">
                        <!-- JS Dynamic Content -->
                    </div>

                    <!-- 新增自訂事項 -->
                    <div class="mt-4 pt-4 border-t border-dashed border-slate-100 flex gap-2">
                        <input type="text" id="add-item-input" placeholder="新增其他必帶物品..." class="flex-grow text-xs px-3.5 py-2.5 bg-slate-50 rounded-xl border border-slate-200 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                        <button onclick="addChecklistItem()" class="bg-indigo-600 hover:bg-indigo-700 text-white text-xs font-bold px-4 rounded-xl transition-all">新增</button>
                    </div>
                </div>

                <!-- 飯店資訊快捷卡 -->
                <div class="bg-white rounded-3xl p-5 shadow-sm border border-slate-100 space-y-3">
                    <div class="flex items-center gap-2">
                        <span class="text-lg">🏨</span>
                        <h3 class="text-sm font-bold text-slate-800">落腳飯店資訊</h3>
                    </div>
                    <div class="bg-slate-50 p-3.5 rounded-2xl border border-slate-100 space-y-2">
                        <div>
                            <p class="text-[10px] text-slate-400 font-bold uppercase">飯店名稱</p>
                            <p class="text-xs font-bold text-slate-800 flex items-center justify-between">
                                <span>Dormy Inn PREMIUM 東京小傳馬町</span>
                                <button onclick="copyToClipboard('Dormy Inn PREMIUM Kanda-Kodenmacho')" class="text-[10px] text-indigo-600 font-semibold bg-indigo-50 px-2 py-0.5 rounded-md hover:bg-indigo-100">複製英文</button>
                            </p>
                            <p class="text-[11px] text-slate-500 mt-0.5">ドーミーインPREMIUM東京小伝馬町</p>
                        </div>
                        <div class="border-t border-slate-200/60 my-2 pt-2">
                            <p class="text-[10px] text-slate-400 font-bold uppercase">地址 / 電話</p>
                            <p class="text-xs text-slate-700 leading-normal flex items-start justify-between gap-1 mt-0.5">
                                <span class="flex-grow">東京都中央区日本橋小伝馬町2-3</span>
                                <button onclick="copyToClipboard('東京都中央区日本橋小伝馬町2-3')" class="text-[10px] text-indigo-600 font-semibold bg-indigo-50 px-2 py-0.5 rounded-md shrink-0 hover:bg-indigo-100">複製地址</button>
                            </p>
                            <p class="text-xs text-slate-700 mt-1">📞 03-5614-5489</p>
                        </div>
                    </div>
                </div>
            </section>

            <!-- ==================== TAB 2: DAY 1 ==================== -->
            <section id="sec-day1" class="tab-section hidden space-y-4">
                <div class="bg-slate-900 text-white rounded-3xl p-5 shadow-md flex justify-between items-center">
                    <div>
                        <span class="text-xs text-indigo-300 font-bold uppercase tracking-wider">Day 1 Focus</span>
                        <h3 class="text-lg font-bold">新宿東口爆買 & 溫泉拉麵夜</h3>
                    </div>
                    <div class="text-right">
                        <span class="bg-amber-400/20 text-amber-400 text-xs font-bold px-2.5 py-1 rounded-full">人形町一車直達</span>
                    </div>
                </div>

                <!-- 時間軸列表 -->
                <div id="day1-timeline" class="space-y-4 relative before:absolute before:left-5 before:top-4 before:bottom-4 before:w-0.5 before:bg-slate-200">
                    <!-- JS Dynamic Content -->
                </div>
            </section>

            <!-- ==================== TAB 3: DAY 2 ==================== -->
            <section id="sec-day2" class="tab-section hidden space-y-4">
                <div class="bg-slate-900 text-white rounded-3xl p-5 shadow-md flex justify-between items-center">
                    <div>
                        <span class="text-xs text-pink-300 font-bold uppercase tracking-wider">Day 2 Focus</span>
                        <h3 class="text-lg font-bold">豪德寺還願、鐵塔與下午茶</h3>
                    </div>
                    <div class="text-right">
                        <span class="bg-emerald-400/20 text-emerald-400 text-xs font-bold px-2.5 py-1 rounded-full">星宇20:40起飛</span>
                    </div>
                </div>

                <!-- 時間軸列表 -->
                <div id="day2-timeline" class="space-y-4 relative before:absolute before:left-5 before:top-4 before:bottom-4 before:w-0.5 before:bg-slate-200">
                    <!-- JS Dynamic Content -->
                </div>
            </section>

            <!-- ==================== TAB 4: TOOLS ==================== -->
            <section id="sec-tools" class="tab-section hidden space-y-4">
                
                <!-- 購物試算器 -->
                <div class="bg-white rounded-3xl p-5 shadow-sm border border-slate-100 space-y-4">
                    <div class="flex items-center gap-2">
                        <span class="text-lg">🧮</span>
                        <h3 class="text-sm font-bold text-slate-800">日幣購物免稅折扣計算</h3>
                    </div>
                    
                    <div class="space-y-3">
                        <div>
                            <label class="text-[11px] text-slate-400 font-bold block mb-1">輸入日幣含稅價 (JPY)</label>
                            <div class="relative">
                                <span class="absolute left-3 top-1/2 -translate-y-1/2 text-slate-400 font-bold text-sm">¥</span>
                                <input type="number" id="tax-input" placeholder="例如：55000" oninput="runTaxCalc()" class="w-full pl-7 pr-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-500 font-bold text-slate-800 text-sm">
                            </div>
                        </div>

                        <div class="grid grid-cols-2 gap-2">
                            <div class="bg-slate-50 p-3 rounded-xl border border-slate-100">
                                <span class="text-[10px] text-slate-400 block">標準退稅後 (10%)</span>
                                <span id="res-taxfree" class="text-base font-black text-slate-800">¥ 0</span>
                            </div>
                            <div class="bg-indigo-50 p-3 rounded-xl border border-indigo-100">
                                <span class="text-[10px] text-indigo-500 block">Bic Camera (退稅+7%)</span>
                                <span id="res-bic" class="text-base font-black text-indigo-600">¥ 0</span>
                            </div>
                        </div>
                        <p class="text-[10px] text-slate-400 leading-normal">
                            * 退稅門檻為當天同一店家單筆滿 ¥5,000 (不含稅)。Bic Camera 折扣券需出示護照與優惠券畫面。
                        </p>
                    </div>
                </div>

                <!-- 隨行筆記型號備忘錄 -->
                <div class="bg-white rounded-3xl p-5 shadow-sm border border-slate-100 space-y-3">
                    <div class="flex items-center justify-between">
                        <div class="flex items-center gap-2">
                            <span class="text-lg">📝</span>
                            <h3 class="text-sm font-bold text-slate-800">購物備忘錄 (免找型號/鞋號)</h3>
                        </div>
                        <span class="text-[10px] text-slate-400 bg-slate-100 px-2 py-0.5 rounded-full">自動儲存</span>
                    </div>
                    <textarea id="shopping-memo" rows="4" placeholder="在這裡寫下您跟先生想買的：&#10;- On 鞋碼: 男生 US10 / 女生 US6&#10;- Panasonic 美容儀型號: EH-XR10&#10;- 唐吉訶德必帶面膜..." class="w-full p-3 bg-slate-50 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-700 leading-relaxed"></textarea>
                </div>

                <!-- 日語溝通急救卡 -->
                <div class="bg-white rounded-3xl p-5 shadow-sm border border-slate-100 space-y-3">
                    <div class="flex items-center gap-2">
                        <span class="text-lg">🗣️</span>
                        <h3 class="text-sm font-bold text-slate-800">路途日語溝通圖卡</h3>
                    </div>
                    <p class="text-xs text-slate-500 mb-2">遇到困難時，直接點擊下方按鈕出示全螢幕給日本人看！</p>
                    
                    <div class="grid grid-cols-2 gap-2">
                        <button onclick="showRescueCard('搭計程車去機場', '成田空港までタクシーをお願いします。', '請幫我叫一台到成田機場的計程車。')" class="p-3 bg-slate-50 border border-slate-100 rounded-2xl text-left hover:bg-slate-100 transition-all">
                            <p class="text-xs font-bold text-slate-800">🚕 叫車去機場</p>
                            <p class="text-[10px] text-slate-400 mt-1 truncate">成田空港まで...</p>
                        </button>
                        <button onclick="showRescueCard('向飯店要冰塊', '氷（こおり）をいただけますか？', '可以給我一些冰塊嗎？')" class="p-3 bg-slate-50 border border-slate-100 rounded-2xl text-left hover:bg-slate-100 transition-all">
                            <p class="text-xs font-bold text-slate-800">🧊 索取冰塊</p>
                            <p class="text-[10px] text-slate-400 mt-1 truncate">氷をいただけますか...</p>
                        </button>
                        <button onclick="showRescueCard('結帳要免稅', '免税（めんぜい）でお願いします。', '請幫我辦理免稅。')" class="p-3 bg-slate-50 border border-slate-100 rounded-2xl text-left hover:bg-slate-100 transition-all">
                            <p class="text-xs font-bold text-slate-800">🛍️ 辦理免稅</p>
                            <p class="text-[10px] text-slate-400 mt-1 truncate">免税でお願いします...</p>
                        </button>
                        <button onclick="showRescueCard('請飯店協助叫計程車', 'タクシーを一台呼んでいただけますか？', '可以幫我叫一輛計程車嗎？')" class="p-3 bg-slate-50 border border-slate-100 rounded-2xl text-left hover:bg-slate-100 transition-all">
                            <p class="text-xs font-bold text-slate-800">🏨 飯店叫計程車</p>
                            <p class="text-[10px] text-slate-400 mt-1 truncate">タクシーを一台...</p>
                        </button>
                    </div>
                </div>

                <!-- 突發航班與備案資訊 -->
                <div class="bg-rose-50 border border-rose-100 rounded-3xl p-5 space-y-3">
                    <div class="flex items-center gap-2 text-rose-800">
                        <span class="text-lg">⚠️</span>
                        <h3 class="text-sm font-bold">回程應變與備用計畫</h3>
                    </div>
                    <div class="space-y-2 text-xs text-rose-700 leading-relaxed">
                        <div class="bg-white/80 p-3 rounded-2xl">
                            <p class="font-bold text-slate-800">🌀 航班追蹤與確認</p>
                            <p class="text-[11px] text-slate-500 mt-0.5">第二天下午 16:00 起，請務必開啟星宇 App 查詢航班資訊是否異動。</p>
                            <a href="https://www.starlux-airlines.com/" target="_blank" class="inline-block mt-2 bg-rose-600 text-white text-[10px] font-bold px-3 py-1.5 rounded-lg">開啟星宇官網</a>
                        </div>
                        <div class="bg-white/80 p-3 rounded-2xl">
                            <p class="font-bold text-slate-800">🚇 若前往機場的鐵路延誤</p>
                            <p class="text-[11px] text-slate-500 mt-0.5 mb-2">可前往 TCAT (東京城市航空總站，步行約 12 分鐘) 改搭利木津巴士直達機場。</p>
                            <a href="https://www.limousinebus.co.jp/" target="_blank" class="inline-block bg-slate-800 text-white text-[10px] font-bold px-3 py-1.5 rounded-lg">利木津時刻表</a>
                        </div>
                    </div>
                </div>
            </section>
        </main>

        <!-- 底部 Native Style 導覽列 -->
        <nav class="absolute bottom-0 left-0 right-0 bg-white/95 border-t border-slate-200/80 px-4 py-2 flex justify-between items-center z-40 backdrop-blur-md shadow-[0_-5px_20px_rgba(0,0,0,0.05)] rounded-t-3xl">
            <button onclick="changeTab('checklist')" id="tab-checklist" class="nav-item flex-grow flex flex-col items-center gap-1 py-1.5 text-indigo-600 font-bold transition-all">
                <span class="text-xl">🧳</span>
                <span class="text-[10px]">準備清單</span>
            </button>
            <button onclick="changeTab('day1')" id="tab-day1" class="nav-item flex-grow flex flex-col items-center gap-1 py-1.5 text-slate-400 hover:text-slate-600 transition-all">
                <span class="text-xl">⚡</span>
                <span class="text-[10px]">第一天</span>
            </button>
            <button onclick="changeTab('day2')" id="tab-day2" class="nav-item flex-grow flex flex-col items-center gap-1 py-1.5 text-slate-400 hover:text-slate-600 transition-all">
                <span class="text-xl">🐈</span>
                <span class="text-[10px]">第二天</span>
            </button>
            <button onclick="changeTab('tools')" id="tab-tools" class="nav-item flex-grow flex flex-col items-center gap-1 py-1.5 text-slate-400 hover:text-slate-600 transition-all">
                <span class="text-xl">⚙️</span>
                <span class="text-[10px]">急救工具</span>
            </button>
        </nav>

        <!-- 全螢幕日語急救卡彈出層 -->
        <div id="rescue-modal" class="fixed inset-0 bg-slate-950/90 z-50 flex items-center justify-center p-6 opacity-0 pointer-events-none transition-all duration-300">
            <div class="bg-white w-full max-w-sm rounded-[32px] p-6 shadow-2xl relative space-y-6">
                <button onclick="closeRescueCard()" class="absolute top-4 right-4 text-slate-400 hover:text-slate-600 p-2 text-xl font-bold">✕</button>
                <div class="text-center space-y-2 border-b border-slate-100 pb-4">
                    <span id="rescue-emoji" class="text-4xl block">🚕</span>
                    <h4 id="rescue-title" class="text-base font-black text-slate-800">搭計程車去機場</h4>
                </div>
                <div class="space-y-4">
                    <div class="bg-indigo-50/50 p-5 rounded-2xl border border-indigo-100 text-center">
                        <p class="text-xs text-indigo-500 font-bold uppercase tracking-wider mb-2">請向對方出示此行日語：</p>
                        <p id="rescue-japanese" class="text-xl font-black text-slate-900 leading-normal select-all">成田空港までタクシーをお願いします。</p>
                    </div>
                    <div class="text-center">
                        <p class="text-xs text-slate-400">中文原意：</p>
                        <p id="rescue-chinese" class="text-xs font-semibold text-slate-600 mt-1">請幫我叫一台到成田機場的計程車。</p>
                    </div>
                </div>
                <div class="text-center">
                    <button onclick="closeRescueCard()" class="w-full bg-slate-900 hover:bg-slate-800 text-white text-sm font-bold py-3.5 rounded-2xl transition-all">關閉畫面</button>
                </div>
            </div>
        </div>

        <!-- Toast 訊息提示 -->
        <div id="toast" class="fixed bottom-24 left-1/2 -translate-x-1/2 bg-slate-900/95 text-white text-xs font-semibold px-4 py-3 rounded-full shadow-2xl flex items-center gap-2 border border-slate-800 transform translate-y-10 opacity-0 pointer-events-none transition-all duration-300 z-50">
            <span id="toast-icon">✨</span>
            <span id="toast-text">已複製到剪貼簿！</span>
        </div>

    </div>

    <script>
        // --- 核心資料 ---
        const initialChecklist = [
            { id: 1, text: "護照（確認效期 6 個月以上）", required: true, checked: false },
            { id: 2, text: "實體卡：玉山星宇航空世界卡 (機場優先報到靈魂必備)", required: true, checked: false },
            { id: 3, text: "手機與充電設備 (網卡確認、行動電源、充電線)", required: true, checked: false },
            { id: 4, text: "日幣現金 & 數位西瓜卡 (Suica) 加值完成", required: true, checked: false },
            { id: 5, text: "空大行李箱 (準備裝 On/Hoka 鞋、美容儀、戰利品)", required: true, checked: false },
            { id: 6, text: "隨身折疊傘 (預防週日局部小陣雨)", required: true, checked: false }
        ];

        const day1Events = [
            { id: '1-1', time: "14:00 - 15:30", title: "抵達成田機場", desc: "辦理入境、領取行李。準備前往電車月台。" },
            { id: '1-2', time: "15:30 - 16:45", title: "機場 ➔ 飯店交通", desc: "搭乘 Access Express 一車直達「人形町站」，步行 8 分鐘至 Dormy Inn PREMIUM 東京小傳馬町。", link: "https://www.google.com/maps/dir/Narita+Airport+Station/Dormy+Inn+PREMIUM+Tokyo+Kodenmacho" },
            { id: '1-3', time: "16:45 - 17:10", title: "飯店 Check-in", desc: "房間放行李、稍作休息。準備前進新宿東口。" },
            { id: '1-4', time: "17:10 - 17:35", title: "飯店 ➔ 新宿交通", desc: "步行 4 分鐘至「馬喰橫山站」搭乘都營新宿線直達「新宿站」東口。" },
            { id: '1-5', time: "17:35 - 18:30", title: "第一站：Alpen TOKYO", desc: "直衝 1 樓入手 On 與 Hoka 潮流球鞋，記得憑護照享免稅結帳！", address: "東京都新宿区新宿３丁目２３−７" },
            { id: '1-6', time: "18:30 - 19:30", title: "第二站：Bic Camera 新宿東口店", desc: "直奔美容家電區，入手 Panasonic 美容儀，結帳出示 10%+7% 免稅折扣券。", address: "東京都新宿区新宿３丁目２９−１" },
            { id: '1-7', time: "19:30 - 21:00", title: "晚餐時間：解鎖新宿東口", desc: "悠閒享用高畫質燒肉或精緻日本料理。" },
            { id: '1-8', time: "21:00 - 21:50", title: "第三站：唐吉訶德 新宿東口本店", desc: "高效率掃貨藥妝、面膜與日本限定伴手禮、零食。", address: "東京都新宿区歌舞伎町１丁目１６−５" },
            { id: '1-9', time: "21:50 - 22:15", title: "計程車舒適回飯店", desc: "21:50 準時在路邊攔計程車提戰利品回飯店最省力。" },
            { id: '1-10', time: "22:15 - 23:00", title: "多美迎：免費夜鳴醬油拉麵", desc: "戰利品放房間後，直接下 2 樓餐廳享用熱騰騰的現煮拉麵。" },
            { id: '1-11', time: "23:00 之後", title: "頂樓天然溫泉「傳馬之湯」", desc: "享受溫泉洗去疲憊，泡完到門口拿免費冰棒，再散步去買超商宵夜。" }
        ];

        const day2Events = [
            { id: '2-1', time: "08:00 - 08:45", title: "清晨交通（飯店 ➔ 豪德寺）", desc: "「小傳馬町站」搭日比谷線 ➔ 「日比谷站」地下轉千代田線直通小田急線 ➔ 直達「豪德寺站」。" },
            { id: '2-2', time: "08:45 - 10:15", title: "第一站：豪德寺還願", desc: "在最安靜的清晨跟招福貓誠心還願，恭請新的招福貓與御守。", address: "東京都世田谷区豪徳寺２丁目２４−７" },
            { id: '2-3', time: "10:15 - 10:45", title: "回程交通（豪德寺 ➔ 日比谷）", desc: "原路搭車返回「日比谷站」。" },
            { id: '2-4', time: "10:45 - 13:00", title: "第二站：東京中城日比谷 & 午餐", desc: "逛日式質感選物店、享用美味午餐。一定要上 6 樓空中花園俯瞰！", address: "東京都千代田区有楽町１丁目１−２" },
            { id: '2-5', time: "13:00 - 13:10", title: "神速交通（日比谷 ➔ 芝公園）", desc: "搭乘都營三田線坐 2 站，在「御成門站」下車，步行 2 分鐘。" },
            { id: '2-6', time: "13:10 - 14:10", title: "第三站：芝公園 4 號地", desc: "足足 1 小時在草地散步，拍出背後有巨大橘紅東京鐵塔的經典同框照！", link: "https://www.google.com/maps/place/Shiba+Park+No.4+Area" },
            { id: '2-7', time: "14:10 - 15:45", title: "第四站：銀座 ＆ HARBS 下午茶", desc: "搭計程車至 HARBS 有樂町LUMINE店 或 銀座三越店，品嚐招牌水果千層蛋糕。" },
            { id: '2-8', time: "15:45 - 16:00", title: "交通回小傳馬町", desc: "「銀座站」搭日比谷線直達「小傳馬町站」回飯店。" },
            { id: '2-9', time: "16:00 - 16:30", title: "飯店房間大打包", desc: "把戰利品妥善裝箱。點開星宇 App 確認航班狀態，優雅辦理退房。" },
            { id: '2-10', time: "16:30 - 16:45", title: "前往人形町站", desc: "拖行李步行約 8 分鐘至淺草線月台。" },
            { id: '2-11', time: "16:50 - 18:05", title: "機場交通（人形町 ➔ 成田）", desc: "搭乘 16:50 左右班次 Access Express，一車直達二航廈。" },
            { id: '2-12', time: "18:10 之後", title: "成田機場：星宇航空回台", desc: "直奔星宇航空櫃檯，亮出實體玉山星宇世界卡免排隊快速辦理託運，20:40 航班帥氣回台！" }
        ];

        // --- 狀態管理 ---
        let state = {
            checklist: JSON.parse(localStorage.getItem('tokyo_express_chk')) || initialChecklist,
            day1Done: JSON.parse(localStorage.getItem('tokyo_express_d1')) || {},
            day2Done: JSON.parse(localStorage.getItem('tokyo_express_d2')) || {},
            memo: localStorage.getItem('tokyo_express_memo') || ''
        };

        // --- 初始化時鐘 ---
        function updateClocks() {
            const now = new Date();
            
            // 台北時間 (UTC+8)
            const optionsTpe = { timeZone: 'Asia/Taipei', hour: '2-digit', minute: '2-digit', hour12: false };
            const tpeTime = now.toLocaleTimeString('zh-TW', optionsTpe);
            document.getElementById('clock-tpe').innerText = `TPE ${tpeTime}`;
            
            // 東京時間 (UTC+9)
            const optionsTyo = { timeZone: 'Asia/Tokyo', hour: '2-digit', minute: '2-digit', hour12: false };
            const tyoTime = now.toLocaleTimeString('zh-TW', optionsTyo);
            document.getElementById('clock-tyo').innerText = `TYO ${tyoTime}`;
        }
        setInterval(updateClocks, 1000);
        updateClocks();

        // --- 導覽切換 (Tab Switch) ---
        function changeTab(targetTab) {
            document.querySelectorAll('.tab-section').forEach(section => {
                section.classList.add('hidden');
            });
            document.getElementById(`sec-${targetTab}`).classList.remove('hidden');

            // 調整底部按鈕樣式
            document.querySelectorAll('.nav-item').forEach(btn => {
                btn.classList.remove('text-indigo-600', 'font-bold');
                btn.classList.add('text-slate-400');
            });
            const activeBtn = document.getElementById(`tab-${targetTab}`);
            activeBtn.classList.remove('text-slate-400');
            activeBtn.classList.add('text-indigo-600', 'font-bold');

            // 滾動回到頂部
            document.querySelector('main').scrollTop = 0;
        }

        // --- 檢查清單渲染 ---
        function renderChecklist() {
            const container = document.getElementById('checklist-container');
            container.innerHTML = '';

            state.checklist.forEach((item, index) => {
                const checked = item.checked ? 'checked' : '';
                const textStyle = item.checked ? 'line-through text-slate-400' : 'text-slate-700';
                const cardStyle = item.checked ? 'bg-slate-50 border-slate-200/60' : 'bg-white border-slate-100 shadow-sm';
                
                const itemDiv = document.createElement('div');
                itemDiv.className = `flex items-center justify-between p-3.5 rounded-2xl border transition-all ${cardStyle}`;
                
                itemDiv.innerHTML = `
                    <label class="flex items-center gap-3 flex-grow cursor-pointer">
                        <input type="checkbox" ${checked} onchange="toggleCheckItem(${index})" class="w-5 h-5 rounded-lg border-slate-300 text-indigo-600 focus:ring-indigo-500">
                        <span class="text-xs font-semibold ${textStyle}">${item.text}</span>
                    </label>
                    ${!item.required ? `
                        <button onclick="deleteCheckItem(${index})" class="text-slate-300 hover:text-red-500 p-1 text-xs ml-2">✕</button>
                    ` : ''}
                `;
                container.appendChild(itemDiv);
            });

            saveAndCalcProgress();
        }

        function toggleCheckItem(index) {
            state.checklist[index].checked = !state.checklist[index].checked;
            renderChecklist();
        }

        function addChecklistItem() {
            const input = document.getElementById('add-item-input');
            const text = input.value.trim();
            if (!text) return;

            state.checklist.push({
                id: Date.now(),
                text: text,
                required: false,
                checked: false
            });
            input.value = '';
            renderChecklist();
            triggerToast('✨ 新增成功');
        }

        function deleteCheckItem(index) {
            state.checklist.splice(index, 1);
            renderChecklist();
        }

        function resetChecklist() {
            state.checklist = initialChecklist.map(item => ({ ...item, checked: false }));
            renderChecklist();
            triggerToast('🔄 清單已全部重置');
        }

        // --- 進度計算與儲存 ---
        function saveAndCalcProgress() {
            localStorage.setItem('tokyo_express_chk', JSON.stringify(state.checklist));
            localStorage.setItem('tokyo_express_d1', JSON.stringify(state.day1Done));
            localStorage.setItem('tokyo_express_d2', JSON.stringify(state.day2Done));

            // 計算檢查清單進度
            const total = state.checklist.length;
            const checked = state.checklist.filter(item => item.checked).length;
            const percentage = total > 0 ? Math.round((checked / total) * 100) : 0;

            document.getElementById('chk-progress-txt').innerText = `${checked}/${total}`;
            document.getElementById('chk-progress-bar').style.width = `${percentage}%`;
            document.getElementById('general-progress-badge').innerText = `準備度 ${percentage}%`;
        }

        // --- 時間軸渲染 ---
        function renderTimelines() {
            // DAY 1
            const d1Container = document.getElementById('day1-timeline');
            d1Container.innerHTML = '';
            day1Events.forEach(evt => {
                const isChecked = state.day1Done[evt.id] || false;
                d1Container.appendChild(createTimelineNode(evt, 1, isChecked));
            });

            // DAY 2
            const d2Container = document.getElementById('day2-timeline');
            d2Container.innerHTML = '';
            day2Events.forEach(evt => {
                const isChecked = state.day2Done[evt.id] || false;
                d2Container.appendChild(createTimelineNode(evt, 2, isChecked));
            });
        }

        function createTimelineNode(evt, dayNum, isChecked) {
            const div = document.createElement('div');
            div.className = `flex gap-3 relative transition-opacity duration-300 ${isChecked ? 'opacity-55' : ''}`;
            
            div.innerHTML = `
                <!-- 時間連線球 -->
                <div class="relative z-10 flex flex-col items-center shrink-0">
                    <button onclick="toggleEvent('${evt.id}', ${dayNum})" class="w-10 h-10 rounded-2xl shadow-sm border border-slate-200/80 flex items-center justify-center text-sm transition-all bg-white font-bold text-slate-700 hover:scale-105 active:scale-95">
                        ${isChecked ? '✓' : '⏰'}
                    </button>
                    <div class="w-0.5 bg-slate-200 flex-grow my-2"></div>
                </div>

                <!-- 卡片本體 -->
                <div class="flex-grow bg-white p-4 rounded-3xl border border-slate-100 shadow-sm space-y-2">
                    <div class="flex justify-between items-center">
                        <span class="text-[10px] font-black text-indigo-600 bg-indigo-50 px-2.5 py-0.5 rounded-lg">${evt.time}</span>
                        ${evt.address ? `
                            <button onclick="copyToClipboard('${evt.address}')" class="text-[10px] text-slate-400 hover:text-indigo-600 font-medium">複製地址</button>
                        ` : ''}
                    </div>
                    <div>
                        <h4 class="font-bold text-slate-800 text-sm ${isChecked ? 'line-through text-slate-400' : ''}">${evt.title}</h4>
                        <p class="text-xs text-slate-500 mt-1 leading-relaxed">${evt.desc}</p>
                    </div>
                    ${evt.address ? `
                        <div class="bg-slate-50 p-2 rounded-xl text-[10px] text-slate-400 flex items-center justify-between">
                            <span class="truncate pr-2">📍 ${evt.address}</span>
                            <a href="https://www.google.com/maps/search/?api=1&query=${encodeURIComponent(evt.title + ' ' + evt.address)}" target="_blank" class="text-indigo-600 font-bold hover:underline shrink-0">地圖 ➔</a>
                        </div>
                    ` : ''}
                    ${evt.link && !evt.address ? `
                        <div class="text-right">
                            <a href="${evt.link}" target="_blank" class="text-[10px] font-bold text-indigo-600 bg-indigo-50 px-2 py-1 rounded-lg">查看交通地圖 ➔</a>
                        </div>
                    ` : ''}
                </div>
            `;
            return div;
        }

        function toggleEvent(id, dayNum) {
            if (dayNum === 1) {
                state.day1Done[id] = !state.day1Done[id];
            } else {
                state.day2Done[id] = !state.day2Done[id];
            }
            saveAndCalcProgress();
            renderTimelines();
            triggerToast('✓ 已更新進度狀態');
        }

        // --- 免稅計算邏輯 ---
        function runTaxCalc() {
            const inputVal = parseFloat(document.getElementById('tax-input').value);
            if (isNaN(inputVal) || inputVal <= 0) {
                document.getElementById('res-taxfree').innerText = "¥ 0";
                document.getElementById('res-bic').innerText = "¥ 0";
                return;
            }

            // 一般免稅 (除以 1.1)
            const taxFree = Math.round(inputVal / 1.1);
            // Bic Camera 優惠 (免稅後額外折 7%)
            const bicPrice = Math.round(taxFree * 0.93);

            document.getElementById('res-taxfree').innerText = `¥ ${taxFree.toLocaleString()}`;
            document.getElementById('res-bic').innerText = `¥ ${bicPrice.toLocaleString()}`;
        }

        // --- 隨手筆記本備忘錄監聽 ---
        const memoArea = document.getElementById('shopping-memo');
        memoArea.value = state.memo;
        memoArea.addEventListener('input', (e) => {
            state.memo = e.target.value;
            localStorage.setItem('tokyo_express_memo', state.memo);
        });

        // --- 全螢幕急救卡 Modal 邏輯 ---
        function showRescueCard(title, japanese, chinese) {
            document.getElementById('rescue-title').innerText = title;
            document.getElementById('rescue-japanese').innerText = japanese;
            document.getElementById('rescue-chinese').innerText = chinese;
            
            const modal = document.getElementById('rescue-modal');
            modal.classList.remove('opacity-0', 'pointer-events-none');
            modal.firstElementChild.classList.remove('scale-95');
        }

        function closeRescueCard() {
            const modal = document.getElementById('rescue-modal');
            modal.classList.add('opacity-0', 'pointer-events-none');
            modal.firstElementChild.classList.add('scale-95');
        }

        // --- Toast 顯示機制 ---
        function triggerToast(text, icon = "✨") {
            const toast = document.getElementById('toast');
            document.getElementById('toast-icon').innerText = icon;
            document.getElementById('toast-text').innerText = text;
            
            toast.classList.remove('translate-y-10', 'opacity-0', 'pointer-events-none');
            setTimeout(() => {
                toast.classList.add('translate-y-10', 'opacity-0', 'pointer-events-none');
            }, 1800);
        }

        // --- 剪貼簿複製機制 (使用 textarea 相容法) ---
        function copyToClipboard(text) {
            const textArea = document.createElement("textarea");
            textArea.value = text;
            document.body.appendChild(textArea);
            textArea.select();
            try {
                document.execCommand('copy');
                triggerToast('已複製到剪貼簿！', '📋');
            } catch (err) {
                console.error('複製失敗:', err);
            }
            document.body.removeChild(textArea);
        }

        // --- 起始載入 ---
        renderChecklist();
        renderTimelines();
    </script>
</body>
</html>

```
