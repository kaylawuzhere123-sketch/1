<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>STEP 1 Daily Tracker - Bubblegum Pink Edition</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Google Fonts: Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
    </style>
</head>
<body class="bg-[#fff1f6] text-slate-800 min-h-screen pb-16">

    <!-- Top Header & Countdown -->
    <header class="bg-white/80 backdrop-blur-md border-b border-pink-100 sticky top-0 z-30 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 py-4 flex flex-col md:flex-row justify-between items-center gap-4">
            <div class="flex items-center space-x-3">
                <div class="w-10 h-10 rounded-2xl bg-gradient-to-tr from-pink-500 to-rose-400 flex items-center justify-center text-white font-bold text-xl shadow-md shadow-pink-200">
                    💕
                </div>
                <div>
                    <h1 class="text-xl font-bold bg-gradient-to-r from-pink-600 to-rose-500 bg-clip-text text-transparent">USMLE STEP 1 Daily Tracker</h1>
                    <p class="text-xs text-rose-400 font-medium">Bubblegum Pink Edition • Stay Consistent & Crush It</p>
                </div>
            </div>

            <!-- Live Exam Countdown -->
            <div class="flex items-center gap-3 bg-pink-50/80 border border-pink-200/60 px-4 py-2 rounded-2xl">
                <span class="text-sm font-semibold text-pink-600">🎯 Exam Countdown:</span>
                <div id="countdown-timer" class="text-sm font-bold text-rose-700">Loading...</div>
            </div>

            <!-- Global Actions -->
            <div class="flex items-center gap-2">
                <button onclick="exportData()" class="px-3 py-2 text-xs font-semibold bg-pink-100 text-pink-700 rounded-xl hover:bg-pink-200 transition">Backup JSON</button>
                <label class="px-3 py-2 text-xs font-semibold bg-rose-500 text-white rounded-xl hover:bg-rose-600 transition cursor-pointer shadow-sm shadow-rose-200">
                    Restore <input type="file" id="importFile" onchange="importData(event)" class="hidden">
                </label>
            </div>
        </div>
    </header>

    <main class="max-w-7xl mx-auto px-4 mt-8 space-y-8">

        <!-- Motivational & Streak Banner -->
        <div class="bg-gradient-to-r from-pink-500 via-rose-500 to-pink-600 rounded-3xl p-6 text-white shadow-xl shadow-pink-200 flex flex-col md:flex-row justify-between items-center gap-6 relative overflow-hidden">
            <div class="absolute -right-10 -bottom-10 w-48 h-48 bg-white/10 rounded-full blur-2xl pointer-events-none"></div>
            <div>
                <span id="date-display" class="text-xs font-bold uppercase tracking-widest bg-white/20 px-3 py-1 rounded-full text-pink-100">Today</span>
                <h2 id="motivational-quote" class="text-xl md:text-2xl font-bold mt-2">"Small daily improvements over time lead to stunning results."</h2>
            </div>
            <div class="flex items-center gap-4 bg-white/10 backdrop-blur-md px-5 py-3 rounded-2xl border border-white/20">
                <div class="text-center">
                    <div class="text-3xl font-extrabold" id="current-streak">0</div>
                    <div class="text-xs uppercase tracking-wider text-pink-100 font-medium">Day Streak 🔥</div>
                </div>
                <div class="w-px h-10 bg-white/20"></div>
                <div class="text-center">
                    <div class="text-3xl font-extrabold" id="best-streak">0</div>
                    <div class="text-xs uppercase tracking-wider text-pink-100 font-medium">Best Streak 🏆</div>
                </div>
            </div>
        </div>

        <!-- Date Navigator & Calendar Header -->
        <div class="bg-white rounded-3xl p-5 border border-pink-100 shadow-sm flex flex-col sm:flex-row justify-between items-center gap-4">
            <div class="flex items-center gap-3">
                <button onclick="changeDate(-1)" class="w-10 h-10 rounded-xl bg-pink-50 text-pink-600 font-bold hover:bg-pink-100 transition flex items-center justify-center">&larr;</button>
                <input type="date" id="selected-date-input" onchange="onDateInputChange(this.value)" class="bg-pink-50/50 border border-pink-200 font-bold text-pink-700 px-4 py-2 rounded-xl focus:outline-none focus:ring-2 focus:ring-pink-400">
                <button onclick="changeDate(1)" class="w-10 h-10 rounded-xl bg-pink-50 text-pink-600 font-bold hover:bg-pink-100 transition flex items-center justify-center">&rarr;</button>
            </div>
            <button onclick="setToday()" class="px-4 py-2 bg-pink-500 text-white font-semibold text-sm rounded-xl hover:bg-pink-600 transition shadow-md shadow-pink-200">Jump to Today</button>
        </div>

        <!-- Two Column Layout: Core Tasks & Features -->
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            
            <!-- Column 1 & 2: Core Task Tracker -->
            <div class="lg:col-span-2 space-y-6">
                
                <!-- Task Card 1: STEP Videos -->
                <div class="bg-white rounded-3xl p-6 border border-pink-100 shadow-sm transition hover:shadow-md">
                    <div class="flex items-center justify-between mb-4">
                        <div class="flex items-center gap-3">
                            <input type="checkbox" id="task-video" onchange="saveData()" class="w-6 h-6 accent-pink-500 rounded-lg cursor-pointer">
                            <label for="task-video" class="font-bold text-lg text-slate-700 cursor-pointer">🎥 Watch STEP Videos</label>
                        </div>
                        <div class="flex items-center gap-2">
                            <span class="text-xs font-semibold text-pink-500 uppercase">Count:</span>
                            <input type="number" id="video-count" min="0" value="0" oninput="saveData()" class="w-20 bg-pink-50 border border-pink-200 rounded-xl px-3 py-1 font-bold text-pink-700 text-center">
                        </div>
                    </div>
                    <input type="text" id="video-notes" placeholder="Enter video topics, Sketchy/Pathoma modules..." oninput="saveData()" class="w-full bg-pink-50/40 border border-pink-200/60 rounded-2xl px-4 py-3 text-sm focus:outline-none focus:ring-2 focus:ring-pink-400">
                </div>

                <!-- Task Card 2: UWorld Questions -->
                <div class="bg-white rounded-3xl p-6 border border-pink-100 shadow-sm transition hover:shadow-md">
                    <div class="flex items-center justify-between mb-4">
                        <div class="flex items-center gap-3">
                            <input type="checkbox" id="task-uworld" onchange="saveData()" class="w-6 h-6 accent-pink-500 rounded-lg cursor-pointer">
                            <label for="task-uworld" class="font-bold text-lg text-slate-700 cursor-pointer">📝 Do UWorld Blocks</label>
                        </div>
                        <div class="flex items-center gap-4">
                            <div class="flex items-center gap-2">
                                <span class="text-xs font-semibold text-pink-500 uppercase">Blocks:</span>
                                <input type="number" id="uworld-blocks" min="0" value="0" oninput="saveData()" class="w-16 bg-pink-50 border border-pink-200 rounded-xl px-2 py-1 font-bold text-pink-700 text-center">
                            </div>
                            <div class="flex items-center gap-2">
                                <span class="text-xs font-semibold text-pink-500 uppercase">Total Qs:</span>
                                <input type="number" id="uworld-qs" min="0" value="0" oninput="saveData()" class="w-16 bg-pink-50 border border-pink-200 rounded-xl px-2 py-1 font-bold text-pink-700 text-center">
                            </div>
                        </div>
                    </div>
                    <input type="text" id="uworld-notes" placeholder="Enter block percentages or main subjects..." oninput="saveData()" class="w-full bg-pink-50/40 border border-pink-200/60 rounded-2xl px-4 py-3 text-sm focus:outline-none focus:ring-2 focus:ring-pink-400">
                </div>

                <!-- Task Card 3: Anki Reviews -->
                <div class="bg-white rounded-3xl p-6 border border-pink-100 shadow-sm transition hover:shadow-md">
                    <div class="flex items-center justify-between mb-4">
                        <div class="flex items-center gap-3">
                            <input type="checkbox" id="task-anki" onchange="saveData()" class="w-6 h-6 accent-pink-500 rounded-lg cursor-pointer">
                            <label for="task-anki" class="font-bold text-lg text-slate-700 cursor-pointer">🧠 Finish Anki Reviews</label>
                        </div>
                        <div class="flex items-center gap-2">
                            <span class="text-xs font-semibold text-pink-500 uppercase">Cards:</span>
                            <input type="number" id="anki-cards" min="0" value="0" oninput="saveData()" class="w-24 bg-pink-50 border border-pink-200 rounded-xl px-3 py-1 font-bold text-pink-700 text-center">
                        </div>
                    </div>
                    
                    <!-- Backlog warning meter -->
                    <div class="flex items-center justify-between bg-pink-50/60 p-3 rounded-2xl border border-pink-200/60">
                        <span class="text-xs font-bold text-pink-700">⚠️ Due Card Backlog (Unreviewed):</span>
                        <input type="number" id="anki-backlog" min="0" value="0" oninput="saveData()" class="w-20 bg-white border border-pink-300 rounded-xl px-2 py-1 font-bold text-rose-600 text-center shadow-xs">
                    </div>
                    <div id="backlog-warning" class="text-xs text-rose-500 font-semibold mt-2 hidden">🚨 High Backlog Alert! Clear your due cards before adding new ones!</div>
                </div>

                <!-- Analytics Graphs Section -->
                <div class="bg-white rounded-3xl p-6 border border-pink-100 shadow-sm">
                    <div class="flex justify-between items-center mb-6">
                        <h3 class="font-bold text-lg text-slate-700">📊 Quantitative Study Volume Trends</h3>
                        <div class="flex gap-2">
                            <button onclick="updateChartRange(7)" id="btn-range-7" class="px-3 py-1 text-xs font-bold bg-pink-500 text-white rounded-xl shadow-xs">Last 7 Days</button>
                            <button onclick="updateChartRange(30)" id="btn-range-30" class="px-3 py-1 text-xs font-bold bg-pink-100 text-pink-700 rounded-xl">Last 30 Days</button>
                        </div>
                    </div>
                    <div class="relative h-64 w-full">
                        <canvas id="volumeChart"></canvas>
                    </div>
                </div>

                <!-- NBME Practice Score Trend Tracker -->
                <div class="bg-white rounded-3xl p-6 border border-pink-100 shadow-sm">
                    <h3 class="font-bold text-lg text-slate-700 mb-4">📈 NBME & Practice Score Trend Tracker</h3>
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-4">
                        <div>
                            <label class="block text-xs font-bold text-pink-600 uppercase mb-1">Exam Name / Form</label>
                            <input type="text" id="nbme-name" placeholder="e.g. NBME 30 or Free 120" class="w-full bg-pink-50/50 border border-pink-200 rounded-xl px-3 py-2 text-sm font-medium focus:outline-none focus:ring-2 focus:ring-pink-400">
                        </div>
                        <div>
                            <label class="block text-xs font-bold text-pink-600 uppercase mb-1">Score / Percentage</label>
                            <input type="number" id="nbme-score" placeholder="e.g. 235 or 78%" class="w-full bg-pink-50/50 border border-pink-200 rounded-xl px-3 py-2 text-sm font-medium focus:outline-none focus:ring-2 focus:ring-pink-400">
                        </div>
                        <div class="flex items-end">
                            <button onclick="addNbmeScore()" class="w-full py-2 bg-pink-500 hover:bg-pink-600 text-white font-bold text-sm rounded-xl transition shadow-md shadow-pink-200">Log Score</button>
                        </div>
                    </div>
                    <div class="relative h-48 w-full mt-4">
                        <canvas id="nbmeChart"></canvas>
                    </div>
                </div>

            </div>

            <!-- Column 3: Tools, Mystery Reward, High-Yield Diagnosis & UWorld Incorrects -->
            <div class="space-y-6">

                <!-- Mystery Reward Generator Box -->
                <div class="bg-gradient-to-br from-pink-500 to-rose-500 rounded-3xl p-6 text-white shadow-xl shadow-pink-200 text-center relative overflow-hidden">
                    <div class="absolute -right-6 -top-6 w-32 h-32 bg-white/10 rounded-full blur-xl pointer-events-none"></div>
                    <h3 class="text-lg font-bold mb-1">🎁 Study Reward Mystery Box</h3>
                    <p class="text-xs text-pink-100 mb-4">Earned based on how well you complete today's core tasks!</p>
                    <div id="reward-display" class="bg-white/20 backdrop-blur-md border border-white/30 rounded-2xl p-4 mb-4 font-semibold text-sm min-h-[60px] flex items-center justify-center">
                        Complete your tasks to unlock your study reward!
                    </div>
                    <button onclick="spinReward()" class="w-full py-3 bg-white text-pink-600 hover:bg-pink-50 font-bold rounded-2xl shadow-md transition">✨ Open Reward Box</button>
                </div>

                <!-- High-Yield STEP Diagnosis of the Day -->
                <div class="bg-white rounded-3xl p-6 border border-pink-100 shadow-sm">
                    <div class="flex justify-between items-center mb-3">
                        <span class="text-xs font-bold uppercase tracking-wider bg-pink-100 text-pink-700 px-3 py-1 rounded-full">High-Yield Board Case</span>
                        <label class="flex items-center gap-1.5 text-xs font-bold text-slate-500 cursor-pointer">
                            <input type="checkbox" id="diagnosis-mastered" onchange="saveData()" class="w-4 h-4 accent-pink-500 rounded"> Mastered
                        </label>
                    </div>
                    <h3 id="hy-title" class="font-bold text-lg text-rose-700 mb-2">Diagnosis Name</h3>
                    <div class="space-y-2 text-xs text-slate-600">
                        <p><strong class="text-slate-700">Specialty:</strong> <span id="hy-specialty">-</span></p>
                        <p><strong class="text-slate-700">Buzzwords:</strong> <span id="hy-buzzwords">-</span></p>
                        <p><strong class="text-slate-700">Presentation:</strong> <span id="hy-presentation">-</span></p>
                        <p><strong class="text-slate-700">Pathology/Mechanism:</strong> <span id="hy-mechanism">-</span></p>
                    </div>
                </div>

                <!-- Pomodoro Timer -->
                <div class="bg-white rounded-3xl p-6 border border-pink-100 shadow-sm text-center">
                    <h3 class="font-bold text-lg text-slate-700 mb-1">⏱️ Focus Pomodoro</h3>
                    <p class="text-xs text-slate-400 mb-4">Stay locked in for UWorld or Anki</p>
                    <div id="pomo-display" class="text-4xl font-black text-pink-600 mb-4 tracking-wider">25:00</div>
                    <div class="flex justify-center gap-2">
                        <button onclick="startPomo()" id="pomo-start-btn" class="px-4 py-2 bg-pink-500 hover:bg-pink-600 text-white font-bold text-sm rounded-xl shadow-md shadow-pink-200 transition">Start</button>
                        <button onclick="resetPomo()" class="px-4 py-2 bg-pink-100 hover:bg-pink-200 text-pink-700 font-bold text-sm rounded-xl transition">Reset</button>
                    </div>
                </div>

                <!-- UWorld Incorrects & Concept Tagging Filter -->
                <div class="bg-white rounded-3xl p-6 border border-pink-100 shadow-sm">
                    <h3 class="font-bold text-lg text-slate-700 mb-3">🏷️ UWorld Incorrects Logger</h3>
                    <div class="space-y-3 mb-4">
                        <input type="text" id="inc-concept" placeholder="Concept / Missed Topic..." class="w-full bg-pink-50/50 border border-pink-200 rounded-xl px-3 py-2 text-sm focus:outline-none focus:ring-2 focus:ring-pink-400">
                        <div class="grid grid-cols-2 gap-2">
                            <select id="inc-system" class="bg-pink-50/50 border border-pink-200 rounded-xl px-3 py-2 text-xs font-semibold text-slate-700 focus:outline-none">
                                <option value="Cardiology">Cardiology</option>
                                <option value="Neurology">Neurology</option>
                                <option value="Renal">Renal</option>
                                <option value="GI">GI / Nutrition</option>
                                <option value="Pulmonology">Pulmonology</option>
                                <option value="Endocrine">Endocrine</option>
                                <option value="Hematology">Hematology</option>
                                <option value="Infectious Disease">Infectious Disease</option>
                            </select>
                            <select id="inc-error" class="bg-pink-50/50 border border-pink-200 rounded-xl px-3 py-2 text-xs font-semibold text-slate-700 focus:outline-none">
                                <option value="Knowledge Gap">Knowledge Gap</option>
                                <option value="Misread Stem">Misread Stem</option>
                                <option value="Reasoning Error">Reasoning Error</option>
                            </select>
                        </div>
                        <button onclick="addIncorrect()" class="w-full py-2 bg-pink-500 hover:bg-pink-600 text-white font-bold text-xs rounded-xl transition shadow-md shadow-pink-200">+ Log Incorrect Concept</button>
                    </div>
                    <div id="incorrects-list" class="space-y-2 max-h-48 overflow-y-auto pr-1">
                        <!-- Populated dynamically -->
                    </div>
                </div>

            </div>

        </div>

    </main>

    <script>
        // Target Exam Date (e.g., June 15, 2026)
        const EXAM_DATE = new Date('2026-06-15T08:00:00').getTime();

        function updateCountdown() {
            const now = new Date().getTime();
            const distance = EXAM_DATE - now;
            if (distance < 0) {
                document.getElementById('countdown-timer').innerText = "Exam Day is Here! 🎉";
                return;
            }
            const days = Math.floor(distance / (1000 * 60 * 60 * 24));
            const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
            document.getElementById('countdown-timer').innerText = `${days}d ${hours}h ${minutes}m`;
        }
        setInterval(updateCountdown, 1000);
        updateCountdown();

        // High-Yield Diagnosis Curated Bank
        const HY_DIAGNOSES = [
            { specialty: "Genetics / Metabolism", title: "Acute Intermittent Porphyria", buzzwords: "Port-wine urine, abdominal pain, psychiatric symptoms, ALA synthase up-regulation", presentation: "Acute abdominal pain, neurologic symptoms triggered by fasting, alcohol, or CYP450 inducers (barbiturates).", mechanism: "Porphobilinogen (PBG) deaminase deficiency leading to neurotoxic ALA and PBG accumulation." },
            { specialty: "Renal / Autoimmune", title: "Goodpasture Syndrome", buzzwords: "Linear IgG deposition, anti-GBM antibodies, glomerulonephritis + hemoptysis", presentation: "Young adult male with acute kidney injury (hematuria) and pulmonary hemorrhage.", mechanism: "Autoantibodies against the alpha-3 chain of type IV collagen in glomerular and alveolar basement membranes." },
            { specialty: "Cardiology / Embryology", title: "Tetralogy of Fallot", buzzwords: "Boot-shaped heart, early cyanosis, tet spells, squatting for relief", presentation: "Infant with cyanosis during crying or feeding who instinctively squats to increase SVR.", mechanism: "Unequal septation of the infundibulum due to anterior-superior displacement of the infundibular septum." },
            { specialty: "Hematology / Oncology", title: "Li-Fraumeni Syndrome", buzzwords: "TP53 mutation, multiple primary cancers at young age (SBLA syndrome)", presentation: "Patient with family history of breast cancer, sarcomas, brain tumors, and leukemia before age 45.", mechanism: "Germline mutation in the TP53 tumor suppressor gene leading to impaired apoptosis and cell cycle arrest." },
            { specialty: "Gastroenterology", title: "Wilson Disease", buzzwords: "Kayser-Fleischer rings, low ceruloplasmin, basal ganglia degeneration, ATP7B mutation", presentation: "Young patient presenting with psychiatric disturbances, dysarthria, and movement disorders.", mechanism: "Autosomal recessive defect in hepatocyte copper-transporting ATPase (ATP7B), preventing biliary copper excretion." }
        ];

        function getDailyDiagnosis() {
            const dayOfYear = Math.floor((new Date() - new Date(new Date().getFullYear(), 0, 0)) / (1000 * 60 * 60 * 24));
            return HY_DIAGNOSES[dayOfYear % HY_DIAGNOSES.length];
        }

        function loadDiagnosis() {
            const diag = getDailyDiagnosis();
            document.getElementById('hy-title').innerText = diag.title;
            document.getElementById('hy-specialty').innerText = diag.specialty;
            document.getElementById('hy-buzzwords').innerText = diag.buzzwords;
            document.getElementById('hy-presentation').innerText = diag.presentation;
            document.getElementById('hy-mechanism').innerText = diag.mechanism;
        }

        // Date & LocalStorage Management
        let currentDateKey = formatDateKey(new Date());

        function formatDateKey(date) {
            const year = date.getFullYear();
            const month = String(date.getMonth() + 1).padStart(2, '0');
            const day = String(date.getDate()).padStart(2, '0');
            return `${year}-${month}-${day}`;
        }

        function setToday() {
            currentDateKey = formatDateKey(new Date());
            document.getElementById('selected-date-input').value = currentDateKey;
            loadDayData();
        }

        function changeDate(days) {
            const d = new Date(currentDateKey);
            d.setDate(d.getDate() + days);
            currentDateKey = formatDateKey(d);
            document.getElementById('selected-date-input').value = currentDateKey;
            loadDayData();
        }

        function onDateInputChange(val) {
            if (val) {
                currentDateKey = val;
                loadDayData();
            }
        }

        function getAllData() {
            const data = localStorage.getItem('usmle_tracker_data');
            return data ? JSON.parse(data) : {};
        }

        function saveAllData(allData) {
            localStorage.setItem('usmle_tracker_data', JSON.stringify(allData));
            calculateStreaks();
            updateCharts();
        }

        function loadDayData() {
            document.getElementById('selected-date-input').value = currentDateKey;
            document.getElementById('date-display').innerText = new Date(currentDateKey + 'T00:00:00').toLocaleDateString('en-US', { weekday: 'short', month: 'short', day: 'numeric', year: 'numeric' });

            const allData = getAllData();
            const dayData = allData[currentDateKey] || {
                video: false, videoCount: 0, videoNotes: '',
                uworld: false, uworldBlocks: 0, uworldQs: 0, uworldNotes: '',
                anki: false, ankiCards: 0, ankiBacklog: 0,
                diagnosisMastered: false
            };

            document.getElementById('task-video').checked = dayData.video;
            document.getElementById('video-count').value = dayData.videoCount || 0;
            document.getElementById('video-notes').value = dayData.videoNotes || '';

            document.getElementById('task-uworld').checked = dayData.uworld;
            document.getElementById('uworld-blocks').value = dayData.uworldBlocks || 0;
            document.getElementById('uworld-qs').value = dayData.uworldQs || 0;
            document.getElementById('uworld-notes').value = dayData.uworldNotes || '';

            document.getElementById('task-anki').checked = dayData.anki;
            document.getElementById('anki-cards').value = dayData.ankiCards || 0;
            const backlog = dayData.ankiBacklog || 0;
            document.getElementById('anki-backlog').value = backlog;

            document.getElementById('diagnosis-mastered').checked = dayData.diagnosisMastered || false;

            const warningEl = document.getElementById('backlog-warning');
            if (backlog > 200) {
                warningEl.classList.remove('hidden');
            } else {
                warningEl.classList.add('hidden');
            }
        }

        function saveData() {
            const allData = getAllData();
            allData[currentDateKey] = {
                video: document.getElementById('task-video').checked,
                videoCount: parseInt(document.getElementById('video-count').value) || 0,
                videoNotes: document.getElementById('video-notes').value,
                uworld: document.getElementById('task-uworld').checked,
                uworldBlocks: parseFloat(document.getElementById('uworld-blocks').value) || 0,
                uworldQs: parseInt(document.getElementById('uworld-qs').value) || 0,
                uworldNotes: document.getElementById('uworld-notes').value,
                anki: document.getElementById('task-anki').checked,
                ankiCards: parseInt(document.getElementById('anki-cards').value) || 0,
                ankiBacklog: parseInt(document.getElementById('anki-backlog').value) || 0,
                diagnosisMastered: document.getElementById('diagnosis-mastered').checked
            };

            const backlog = allData[currentDateKey].ankiBacklog;
            const warningEl = document.getElementById('backlog-warning');
            if (backlog > 200) {
                warningEl.classList.remove('hidden');
            } else {
                warningEl.classList.add('hidden');
            }

            saveAllData(allData);
        }

        // Streak Engine
        function calculateStreaks() {
            const allData = getAllData();
            let currentStreak = 0;
            let bestStreak = 0;
            let tempStreak = 0;

            let checkDate = new Date();
            let checkKey = formatDateKey(checkDate);

            // Calculate current streak backward from today
            for (let i = 0; i < 365; i++) {
                const day = allData[checkKey];
                if (day && day.video && day.uworld && day.anki) {
                    currentStreak++;
                } else if (i > 0) { // allow today to be incomplete without breaking streak immediately if early in day
                    break;
                }
                checkDate.setDate(checkDate.getDate() - 1);
                checkKey = formatDateKey(checkDate);
            }

            // Simple max streak estimation across logged keys
            Object.keys(allData).sort().forEach(k => {
                const day = allData[k];
                if (day && day.video && day.uworld && day.anki) {
                    tempStreak++;
                    if (tempStreak > bestStreak) bestStreak = tempStreak;
                } else {
                    tempStreak = 0;
                }
            });

            if (currentStreak > bestStreak) bestStreak = currentStreak;

            document.getElementById('current-streak').innerText = currentStreak;
            document.getElementById('best-streak').innerText = bestStreak;
        }

        // Mystery Reward Generator
        function spinReward() {
            const allData = getAllData();
            const day = allData[currentDateKey];
            const rewardDisplay = document.getElementById('reward-display');

            if (!day || (!day.video && !day.uworld && !day.anki)) {
                rewardDisplay.innerText = "🔒 Complete at least one study task today to unlock your mystery reward!";
                return;
            }

            let score = 0;
            if (day.video) score++;
            if (day.uworld) score++;
            if (day.anki) score++;
            if (day.uworldQs >= 40) score++;

            const rewardsLow = [
                "☕ 10-Minute Coffee Break with your favorite playlist!",
                "🍫 A sweet treat or dark chocolate square!",
                "🌳 A refreshing 15-minute outside walk without guilt!"
            ];
            const rewardsHigh = [
                "🎉 30-Minute Episode of your favorite show tonight!",
                "🍕 Delicious Barbecue takeout from Smoke Daddy!",
                "🛍️ A guilt-free online shopping session or extra rest evening!"
            ];

            const pool = score >= 3 ? rewardsHigh : rewardsLow;
            const chosen = pool[Math.floor(Math.random() * pool.length)];
            rewardDisplay.innerText = chosen;
        }

        // UWorld Incorrects LocalStorage & Rendering
        function getIncorrects() {
            const inc = localStorage.getItem('usmle_incorrects');
            return inc ? JSON.parse(inc) : [];
        }

        function addIncorrect() {
            const concept = document.getElementById('inc-concept').value.trim();
            const system = document.getElementById('inc-system').value;
            const error = document.getElementById('inc-error').value;

            if (!concept) return;

            const list = getIncorrects();
            list.unshift({ id: Date.now(), concept, system, error });
            localStorage.setItem('usmle_incorrects', JSON.stringify(list));
            document.getElementById('inc-concept').value = '';
            renderIncorrects();
        }

        function deleteIncorrect(id) {
            let list = getIncorrects();
            list = list.filter(item => item.id !== id);
            localStorage.setItem('usmle_incorrects', JSON.stringify(list));
            renderIncorrects();
        }

        function renderIncorrects() {
            const list = getIncorrects();
            const container = document.getElementById('incorrects-list');
            container.innerHTML = '';

            if (list.length === 0) {
                container.innerHTML = `<p class="text-xs text-slate-400 text-center py-4">No incorrects logged yet. Keep pushing!</p>`;
                return;
            }

            list.forEach(item => {
                const div = document.createElement('div');
                div.className = "flex items-center justify-between bg-pink-50/50 border border-pink-200/60 p-2.5 rounded-xl text-xs";
                div.innerHTML = `
                    <div>
                        <span class="font-bold text-slate-700">${item.concept}</span>
                        <div class="text-[10px] text-pink-600 font-semibold mt-0.5">${item.system} • <span class="text-rose-500">${item.error}</span></div>
                    </div>
                    <button onclick="deleteIncorrect(${item.id})" class="text-rose-400 hover:text-rose-600 font-bold px-2">&times;</button>
                `;
                container.appendChild(div);
            });
        }

        // NBME Score Loggers & Chart
        let nbmeChartInstance = null;
        function getNbmeScores() {
            const s = localStorage.getItem('usmle_nbmes');
            return s ? JSON.parse(s) : [];
        }

        function addNbmeScore() {
            const name = document.getElementById('nbme-name').value.trim();
            const score = parseFloat(document.getElementById('nbme-score').value);
            if (!name || isNaN(score)) return;

            const scores = getNbmeScores();
            scores.push({ name, score, date: new Date().toLocaleDateString() });
            localStorage.setItem('usmle_nbmes', JSON.stringify(scores));
            document.getElementById('nbme-name').value = '';
            document.getElementById('nbme-score').value = '';
            renderNbmeChart();
        }

        function renderNbmeChart() {
            const scores = getNbmeScores();
            const ctx = document.getElementById('nbmeChart').getContext('2d');
            if (nbmeChartInstance) nbmeChartInstance.destroy();

            nbmeChartInstance = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: scores.map(s => s.name),
                    datasets: [{
                        label: 'Exam Score / %',
                        data: scores.map(s => s.score),
                        borderColor: '#ec4899',
                        backgroundColor: 'rgba(236, 72, 153, 0.1)',
                        borderWidth: 3,
                        tension: 0.3,
                        fill: true,
                        pointBackgroundColor: '#f43f5e'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: {
                        y: { grid: { color: '#fce7f3' } },
                        x: { grid: { display: false } }
                    }
                }
            });
        }

        // Volume Analytics Chart (Videos, Anki, UWorld)
        let volumeChartInstance = null;
        let currentChartDays = 7;

        function updateChartRange(days) {
            currentChartDays = days;
            document.getElementById('btn-range-7').className = days === 7 ? "px-3 py-1 text-xs font-bold bg-pink-500 text-white rounded-xl shadow-xs" : "px-3 py-1 text-xs font-bold bg-pink-100 text-pink-700 rounded-xl";
            document.getElementById('btn-range-30').className = days === 30 ? "px-3 py-1 text-xs font-bold bg-pink-500 text-white rounded-xl shadow-xs" : "px-3 py-1 text-xs font-bold bg-pink-100 text-pink-700 rounded-xl";
            updateCharts();
        }

        function updateCharts() {
            const allData = getAllData();
            const labels = [];
            const videoData = [];
            const ankiData = [];
            const uworldData = [];

            for (let i = currentChartDays - 1; i >= 0; i--) {
                const d = new Date();
                d.setDate(d.getDate() - i);
                const key = formatDateKey(d);
                labels.push(d.toLocaleDateString('en-US', { month: 'short', day: 'numeric' }));
                
                const day = allData[key] || {};
                videoData.push(day.videoCount || 0);
                ankiData.push(day.ankiCards || 0);
                uworldData.push(day.uworldQs || 0);
            }

            const ctx = document.getElementById('volumeChart').getContext('2d');
            if (volumeChartInstance) volumeChartInstance.destroy();

            volumeChartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: labels,
                    datasets: [
                        { label: 'STEP Videos', data: videoData, backgroundColor: '#f43f5e', borderRadius: 6 },
                        { label: 'Anki Cards', data: ankiData, backgroundColor: '#ec4899', borderRadius: 6 },
                        { label: 'UWorld Qs', data: uworldData, backgroundColor: '#fbcfe8', borderRadius: 6 }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { position: 'top' } },
                    scales: {
                        y: { grid: { color: '#fce7f3' }, beginAtZero: true },
                        x: { grid: { display: false } }
                    }
                }
            });
        }

        // Pomodoro Timer Logic
        let pomoTime = 25 * 60;
        let pomoInterval = null;
        let pomoRunning = false;

        function startPomo() {
            if (pomoRunning) {
                clearInterval(pomoInterval);
                pomoRunning = false;
                document.getElementById('pomo-start-btn').innerText = "Start";
                return;
            }
            pomoRunning = true;
            document.getElementById('pomo-start-btn').innerText = "Pause";
            pomoInterval = setInterval(() => {
                if (pomoTime > 0) {
                    pomoTime--;
                    const m = Math.floor(pomoTime / 60);
                    const s = pomoTime % 60;
                    document.getElementById('pomo-display').innerText = `${String(m).padStart(2, '0')}:${String(s).padStart(2, '0')}`;
                } else {
                    clearInterval(pomoInterval);
                    pomoRunning = false;
                    alert("Pomodoro complete! Take a well-deserved break!");
                    resetPomo();
                }
            }, 1000);
        }

        function resetPomo() {
            clearInterval(pomoInterval);
            pomoRunning = false;
            pomoTime = 25 * 60;
            document.getElementById('pomo-display').innerText = "25:00";
            document.getElementById('pomo-start-btn').innerText = "Start";
        }

        // Export & Import Backup JSON
        function exportData() {
            const allData = {
                tracker: getAllData(),
                incorrects: getIncorrects(),
                nbmes: getNbmeScores()
            };
            const blob = new Blob([JSON.stringify(allData, null, 2)], { type: 'json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `usmle_tracker_backup_${currentDateKey}.json`;
            a.click();
        }

        function importData(event) {
            const file = event.target.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const parsed = JSON.parse(e.target.result);
                    if (parsed.tracker) localStorage.setItem('usmle_tracker_data', JSON.stringify(parsed.tracker));
                    if (parsed.incorrects) localStorage.setItem('usmle_incorrects', JSON.stringify(parsed.incorrects));
                    if (parsed.nbmes) localStorage.setItem('usmle_nbmes', JSON.stringify(parsed.nbmes));
                    loadDayData();
                    renderIncorrects();
                    renderNbmeChart();
                    calculateStreaks();
                    alert("Data restored successfully!");
                } catch (err) {
                    alert("Invalid backup file format.");
                }
            };
            reader.readAsText(file);
        }

        // Initial Load
        window.onload = function() {
            setToday();
            loadDiagnosis();
            renderIncorrects();
            renderNbmeChart();
            calculateStreaks();
            updateCharts();
        };
    </script>
</body>
</html>
