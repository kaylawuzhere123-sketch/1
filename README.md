<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>USMLE STEP 1 Daily Tracker - Bubblegum Pink Edition</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #fff0f5;
            --card-bg: #ffffff;
            --primary: #ff1493;
            --primary-light: #ff69b4;
            --primary-lighter: #ffe4e1;
            --accent: #ffb6c1;
            --text-main: #4a2e35;
            --text-muted: #8c6771;
            --border: #ffc0cb;
            --shadow: rgba(255, 105, 180, 0.12);
            --radius: 20px;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Plus Jakarta Sans', sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            min-height: 100vh;
            padding: 24px;
            display: flex;
            justify-content: center;
        }

        .container {
            width: 100%;
            max-width: 900px;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        /* Header */
        header {
            background: var(--card-bg);
            border: 2px solid var(--border);
            border-radius: var(--radius);
            padding: 24px;
            box-shadow: 0 8px 30px var(--shadow);
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .header-top {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            flex-wrap: wrap;
            gap: 16px;
        }

        .title-area h1 {
            font-size: 26px;
            font-weight: 800;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .title-area p {
            font-size: 13px;
            color: var(--text-muted);
            margin-top: 4px;
            font-weight: 600;
        }

        .header-actions {
            display: flex;
            align-items: center;
            gap: 10px;
            flex-wrap: wrap;
        }

        /* Countdown Badge & Config */
        .countdown-card {
            background: var(--primary-lighter);
            border: 1px solid var(--border);
            border-radius: 14px;
            padding: 10px 16px;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .countdown-info {
            display: flex;
            flex-direction: column;
        }

        .countdown-label {
            font-size: 11px;
            font-weight: 700;
            color: var(--primary);
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .countdown-value {
            font-size: 14px;
            font-weight: 800;
            color: var(--text-main);
        }

        .date-input-wrapper {
            display: flex;
            align-items: center;
            gap: 6px;
            font-size: 12px;
            font-weight: 600;
            color: var(--text-muted);
        }

        .date-input-wrapper input[type="date"] {
            padding: 4px 8px;
            border-radius: 8px;
            border: 1px solid var(--border);
            background: white;
            font-size: 12px;
            color: var(--text-main);
            outline: none;
        }

        .btn {
            background: var(--primary);
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 12px;
            font-weight: 700;
            font-size: 13px;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 4px 12px rgba(255, 20, 147, 0.2);
        }

        .btn:hover {
            background: #e01082;
            transform: translateY(-1px);
        }

        .btn-secondary {
            background: white;
            color: var(--primary);
            border: 2px solid var(--primary-light);
        }

        .btn-secondary:hover {
            background: var(--primary-lighter);
        }

        /* Motivational Banner */
        .banner {
            background: linear-gradient(135deg, var(--primary) 0%, var(--primary-light) 100%);
            border-radius: var(--radius);
            padding: 24px;
            color: white;
            box-shadow: 0 8px 25px var(--shadow);
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: relative;
            overflow: hidden;
        }

        .banner-content {
            max-width: 60%;
        }

        .date-badge {
            background: rgba(255, 255, 255, 0.25);
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            display: inline-block;
            margin-bottom: 8px;
            backdrop-filter: blur(4px);
        }

        .banner h2 {
            font-size: 18px;
            font-weight: 700;
            line-height: 1.4;
        }

        .streaks-box {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(6px);
            border: 1px solid rgba(255, 255, 255, 0.3);
            border-radius: 16px;
            padding: 12px 20px;
            display: flex;
            gap: 20px;
            text-align: center;
        }

        .streak-item .number {
            font-size: 20px;
            font-weight: 800;
        }

        .streak-item .label {
            font-size: 10px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            font-weight: 700;
            opacity: 0.9;
        }

        /* Date Navigation */
        .date-nav {
            background: var(--card-bg);
            border: 2px solid var(--border);
            border-radius: var(--radius);
            padding: 16px 20px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            box-shadow: 0 4px 15px var(--shadow);
        }

        .date-nav-controls {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .icon-btn {
            background: var(--primary-lighter);
            border: 1px solid var(--border);
            color: var(--primary);
            width: 36px;
            height: 36px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            cursor: pointer;
            transition: 0.2s;
        }

        .icon-btn:hover {
            background: var(--primary);
            color: white;
        }

        .date-display-box {
            display: flex;
            align-items: center;
            gap: 8px;
            background: white;
            border: 1px solid var(--border);
            padding: 6px 12px;
            border-radius: 12px;
            font-weight: 700;
            font-size: 14px;
            color: var(--text-main);
        }

        .date-display-box input[type="date"] {
            border: none;
            outline: none;
            font-weight: 700;
            font-size: 14px;
            color: var(--text-main);
            background: transparent;
            cursor: pointer;
        }

        /* Main Grid */
        .main-grid {
            display: grid;
            grid-template-columns: 1fr 340px;
            gap: 20px;
        }

        @media(max-width: 768px) {
            .main-grid {
                grid-template-columns: 1fr;
            }
            .banner {
                flex-direction: column;
                gap: 16px;
                align-items: flex-start;
            }
            .banner-content {
                max-width: 100%;
            }
            .streaks-box {
                width: 100%;
                justify-content: space-around;
            }
        }

        .tasks-column {
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        /* Task Card */
        .task-card {
            background: var(--card-bg);
            border: 2px solid var(--border);
            border-radius: var(--radius);
            padding: 20px;
            box-shadow: 0 4px 15px var(--shadow);
            display: flex;
            flex-direction: column;
            gap: 14px;
            transition: all 0.2s;
        }

        .task-card.completed {
            border-color: #ff69b4;
            background: #fff9fb;
        }

        .task-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .task-title-group {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .task-checkbox {
            width: 22px;
            height: 22px;
            accent-color: var(--primary);
            cursor: pointer;
            border-radius: 6px;
        }

        .task-title {
            font-size: 16px;
            font-weight: 700;
            color: var(--text-main);
        }

        .task-counter-badge {
            background: var(--primary-lighter);
            color: var(--primary);
            padding: 4px 10px;
            border-radius: 10px;
            font-size: 12px;
            font-weight: 800;
            border: 1px solid var(--border);
            min-width: 45px;
            text-align: center;
        }

        .task-input {
            width: 100%;
            padding: 10px 14px;
            border: 1px solid var(--border);
            border-radius: 12px;
            font-size: 13px;
            outline: none;
            background: #fff;
            color: var(--text-main);
            transition: border-color 0.2s;
        }

        .task-input:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(255, 20, 147, 0.1);
        }

        .sub-inputs-row {
            display: flex;
            gap: 10px;
        }

        .sub-input-group {
            flex: 1;
            display: flex;
            flex-direction: column;
            gap: 4px;
        }

        .sub-input-group label {
            font-size: 11px;
            font-weight: 700;
            color: var(--text-muted);
        }

        /* Right Column (Reward & Widgets) */
        .sidebar-column {
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .reward-card {
            background: linear-gradient(145deg, #ffffff 0%, #fff0f5 100%);
            border: 2px dashed var(--primary-light);
            border-radius: var(--radius);
            padding: 24px;
            text-align: center;
            box-shadow: 0 4px 15px var(--shadow);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 14px;
        }

        .reward-card h3 {
            font-size: 16px;
            font-weight: 800;
            color: var(--primary);
        }

        .reward-card p {
            font-size: 12px;
            color: var(--text-muted);
            line-height: 1.4;
        }

        .reward-box-display {
            background: white;
            border: 1px solid var(--border);
            border-radius: 14px;
            padding: 14px;
            width: 100%;
            font-size: 13px;
            font-weight: 700;
            color: var(--text-main);
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.02);
        }

        /* Collapsible sections or extra widgets */
        .widget-card {
            background: var(--card-bg);
            border: 2px solid var(--border);
            border-radius: var(--radius);
            padding: 18px;
            box-shadow: 0 4px 15px var(--shadow);
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .widget-title {
            font-size: 14px;
            font-weight: 800;
            color: var(--primary);
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .analytics-container {
            position: relative;
            height: 180px;
            width: 100%;
        }

        /* Modal Overlay */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(74, 46, 53, 0.4);
            backdrop-filter: blur(4px);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.2s ease;
        }

        .modal-overlay.active {
            opacity: 1;
            pointer-events: auto;
        }

        .modal {
            background: white;
            border-radius: var(--radius);
            border: 2px solid var(--border);
            width: 90%;
            max-width: 450px;
            padding: 24px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.15);
            display: flex;
            flex-direction: column;
            gap: 16px;
            transform: translateY(20px);
            transition: transform 0.2s ease;
        }

        .modal-overlay.active .modal {
            transform: translateY(0);
        }

        .modal h3 {
            color: var(--primary);
            font-size: 18px;
            font-weight: 800;
        }

        .modal textarea {
            width: 100%;
            height: 100px;
            padding: 12px;
            border-radius: 12px;
            border: 1px solid var(--border);
            font-size: 13px;
            outline: none;
            resize: vertical;
        }

        .modal-actions {
            display: flex;
            justify-content: flex-end;
            gap: 10px;
        }
    </style>
</head>
<body>

    <div class="container">
        <!-- Header -->
        <header>
            <div class="header-top">
                <div class="title-area">
                    <h1>🌸 USMLE STEP 1 Daily Tracker</h1>
                    <p>Bubblegum Pink Edition • Stay Consistent & Crush It</p>
                </div>
                <div class="header-actions">
                    <div class="countdown-card">
                        <span style="font-size: 18px;">🎯</span>
                        <div class="countdown-info">
                            <span class="countdown-label">Exam Countdown</span>
                            <span class="countdown-value" id="countdown-text">Loading...</span>
                        </div>
                    </div>
                    <button class="btn btn-secondary" onclick="exportJSON()">Backup JSON</button>
                    <button class="btn" style="background:#ff6b81;" onclick="triggerRestore()">Restore</button>
                    <input type="file" id="restore-file" style="display:none" onchange="importJSON(event)">
                </div>
            </div>
            
            <!-- STEP Date Setting Bar -->
            <div style="display: flex; align-items: center; justify-content: space-between; border-top: 1px solid var(--border); padding-top: 12px; flex-wrap: wrap; gap: 10px;">
                <div class="date-input-wrapper">
                    <span>📅 Target STEP Exam Date:</span>
                    <input type="date" id="step-date-input" onchange="updateStepDate(this.value)">
                </div>
                <div style="font-size: 12px; color: var(--text-muted); font-weight: 600;" id="date-status-msg">
                    Set your exam date to keep your countdown accurate!
                </div>
            </div>
        </header>

        <!-- Motivational Banner -->
        <div class="banner">
            <div class="banner-content">
                <span class="date-badge" id="banner-date-label">SAT, OCT 17, 2026</span>
                <h2 id="daily-quote">"Small daily improvements over time lead to stunning results."</h2>
            </div>
            <div class="streaks-box">
                <div class="streak-item">
                    <div class="number" id="current-streak">1</div>
                    <div class="label">Day Streak 🔥</div>
                </div>
                <div class="streak-item">
                    <div class="number" id="best-streak">1</div>
                    <div class="label">Best Streak 🏆</div>
                </div>
            </div>
        </div>

        <!-- Date Navigation Bar -->
        <div class="date-nav">
            <div class="date-nav-controls">
                <button class="icon-btn" onclick="changeDate(-1)">❮</button>
                <div class="date-display-box">
                    <span>📅</span>
                    <input type="date" id="picker-date" onchange="select
