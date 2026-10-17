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
            display: flex
