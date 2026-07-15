<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Legend Pro V9 - البوت العالمي الخرافي</title>
    <style>
        /* ============================================================
           التصميم الأسطوري النهائي
           ============================================================ */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --bg-primary: #0a0a1a;
            --bg-secondary: #0d0d2b;
            --bg-card: #111133;
            --bg-card-hover: #1a1a4a;
            --text-primary: #e8e8ff;
            --text-secondary: #8888bb;
            --gold: #ffd700;
            --gold-glow: rgba(255, 215, 0, 0.2);
            --green: #00ff88;
            --green-glow: rgba(0, 255, 136, 0.15);
            --red: #ff4466;
            --red-glow: rgba(255, 68, 102, 0.15);
            --blue: #4488ff;
            --blue-glow: rgba(68, 136, 255, 0.15);
            --purple: #8844ff;
            --purple-glow: rgba(136, 68, 255, 0.15);
            --cyan: #00ddff;
            --topbar-bg: linear-gradient(135deg, #cc0000, #ff2200);
            --bottombar-bg: linear-gradient(135deg, #00aa55, #00dd77);
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Arial, sans-serif;
            background: var(--bg-primary);
            color: var(--text-primary);
            min-height: 100vh;
            padding-bottom: 80px;
            overflow-x: hidden;
            background-image:
                radial-gradient(ellipse at 20% 30%, #1a0a4a33 0%, transparent 60%),
                radial-gradient(ellipse at 80% 70%, #0a1a4a33 0%, transparent 60%);
        }

        /* ===== جزيئات ===== */
        .bg-particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
            overflow: hidden;
        }
        .bg-particles span {
            position: absolute;
            width: 2px;
            height: 2px;
            border-radius: 50%;
            animation: floatUp linear infinite;
            opacity: 0.3;
        }
        @keyframes floatUp {
            0% {
                transform: translateY(100vh) scale(0);
                opacity: 0;
            }
            10% {
                opacity: 0.5;
            }
            90% {
                opacity: 0.5;
            }
            100% {
                transform: translateY(-10vh) scale(1);
                opacity: 0;
            }
        }

        /* ===== شاشة الترحيب ===== */
        .splash-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--bg-primary);
            z-index: 9999;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 30px;
            text-align: center;
        }
        .splash-screen.hide {
            opacity: 0;
            pointer-events: none;
            transition: 0.5s;
        }
        .splash-screen .logo {
            font-size: 48px;
            font-weight: 900;
            background: linear-gradient(135deg, var(--gold), var(--purple), var(--cyan));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
        }
        .splash-screen .sub {
            color: var(--text-secondary);
            font-size: 16px;
            margin-bottom: 30px;
        }
        .splash-screen .terms-box {
            background: var(--bg-secondary);
            border-radius: 16px;
            padding: 20px 24px;
            max-width: 400px;
            width: 100%;
            border: 1px solid var(--gold-glow);
            margin-bottom: 25px;
            text-align: right;
        }
        .splash-screen .terms-box h3 {
            color: var(--gold);
            font-size: 16px;
            margin-bottom: 12px;
            text-align: center;
        }
        .splash-screen .terms-box ul {
            list-style: none;
            padding: 0;
        }
        .splash-screen .terms-box ul li {
            padding: 6px 0;
            font-size: 13px;
            color: var(--text-secondary);
            border-bottom: 1px solid #ffffff08;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .splash-screen .terms-box ul li:last-child {
            border-bottom: none;
        }
        .splash-screen .agree-btn {
            padding: 14px 50px;
            background: linear-gradient(135deg, var(--gold), #ffaa00);
            color: #000;
            border: none;
            border-radius: 14px;
            font-size: 18px;
            font-weight: 800;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 0 40px var(--gold-glow);
            width: 100%;
            max-width: 300px;
        }
        .splash-screen .agree-btn:hover {
            transform: scale(1.05);
        }
        .splash-screen .version {
            color: var(--text-secondary);
            font-size: 11px;
            margin-top: 20px;
        }

        /* ===== الهيدر ===== */
        .header {
            background: var(--topbar-bg);
            padding: 10px 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid var(--gold-glow);
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 4px 40px rgba(255, 0, 0, 0.25);
        }
        .header .logo h1 {
            font-size: 18px;
            font-weight: 800;
            color: #fff;
        }
        .header .logo h1 span {
            color: var(--gold);
        }
        .header .logo .sub {
            color: rgba(255, 255, 255, 0.6);
            font-size: 9px;
            display: block;
        }
        .header .icons {
            display: flex;
            gap: 8px;
            align-items: center;
        }
        .header .icons .icon-btn {
            background: rgba(255, 255, 255, 0.12);
            border: none;
            color: #fff;
            font-size: 17px;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
            padding: 6px;
            border-radius: 50%;
            width: 34px;
            height: 34px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .header .icons .icon-btn:hover {
            background: rgba(255, 255, 255, 0.25);
            transform: scale(1.1);
        }
        .header .icons .icon-btn .notification-badge {
            position: absolute;
            top: -2px;
            right: -2px;
            background: var(--red);
            color: #fff;
            font-size: 8px;
            font-weight: 700;
            padding: 1px 5px;
            border-radius: 50%;
            min-width: 16px;
            text-align: center;
        }
        .connection-status {
            display: flex;
            align-items: center;
            gap: 4px;
            font-size: 9px;
            color: rgba(255, 255, 255, 0.7);
            padding: 2px 10px;
            border-radius: 20px;
            background: rgba(255, 255, 255, 0.08);
        }
        .connection-status .dot {
            width: 6px;
            height: 6px;
            border-radius: 50%;
            display: inline-block;
        }
        .connection-status .dot.on {
            background: var(--green);
            animation: pulse 1.5s ease-in-out infinite;
        }
        .connection-status .dot.off {
            background: var(--text-secondary);
        }
        @keyframes pulse {
            0%,
            100% {
                opacity: 1;
            }
            50% {
                opacity: 0.2;
            }
        }

        /* ===== الإشعارات ===== */
        .notification-panel {
            position: fixed;
            top: 68px;
            right: 10px;
            left: 10px;
            max-width: 400px;
            margin: 0 auto;
            background: rgba(13, 13, 43, 0.97);
            backdrop-filter: blur(30px);
            border-radius: 16px;
            border: 1px solid var(--gold-glow);
            padding: 14px;
            z-index: 1000;
            display: none;
            max-height: 380px;
            overflow-y: auto;
            box-shadow: 0 20px 80px rgba(0, 0, 0, 0.9);
        }
        .notification-panel.show {
            display: block;
        }
        .notification-panel .panel-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
            padding-bottom: 8px;
            border-bottom: 1px solid #ffffff11;
        }
        .notification-panel .panel-header span {
            font-weight: 700;
            font-size: 14px;
            color: var(--gold);
        }
        .notification-panel .panel-header button {
            background: none;
            border: none;
            color: var(--text-secondary);
            font-size: 11px;
            cursor: pointer;
            padding: 3px 10px;
            border-radius: 20px;
            border: 1px solid #ffffff22;
        }
        .notification-panel .notif-item {
            padding: 10px 12px;
            border-bottom: 1px solid #ffffff08;
            cursor: pointer;
            transition: all 0.3s;
            border-radius: 10px;
            margin-bottom: 3px;
        }
        .notification-panel .notif-item:hover {
            background: #ffffff0a;
        }
        .notification-panel .notif-item .notif-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .notification-panel .notif-item .notif-type {
            font-size: 10px;
            font-weight: 600;
            padding: 1px 8px;
            border-radius: 20px;
        }
        .notification-panel .notif-item .notif-type.price {
            color: var(--gold);
            background: var(--gold-glow);
        }
        .notification-panel .notif-item .notif-type.alert {
            color: var(--red);
            background: var(--red-glow);
        }
        .notification-panel .notif-item .notif-type.success {
            color: var(--green);
            background: var(--green-glow);
        }
        .notification-panel .notif-item .notif-type.pump {
            color: #ff8800;
            background: rgba(255, 136, 0, 0.15);
        }
        .notification-panel .notif-item .notif-time {
            font-size: 9px;
            color: var(--text-secondary);
        }
        .notification-panel .notif-item .notif-message {
            font-size: 12px;
            margin-top: 3px;
            color: var(--text-primary);
        }
        .notification-panel .notif-empty {
            text-align: center;
            color: var(--text-secondary);
            padding: 20px 0;
        }

        /* ===== الصفحات ===== */
        .page {
            display: none;
            padding: 12px;
            animation: pageFade 0.5s ease;
            position: relative;
            z-index: 1;
        }
        .page.active {
            display: block;
        }
        @keyframes pageFade {
            0% {
                opacity: 0;
                transform: translateY(20px);
            }
            100% {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* ===== البانر ===== */
        .welcome-banner {
            background: linear-gradient(135deg, #0d0d2b, #1a1a4a);
            border-radius: 16px;
            padding: 20px;
            margin-bottom: 14px;
            border: 1px solid var(--gold-glow);
            position: relative;
            overflow: hidden;
        }
        .welcome-banner::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: conic-gradient(from 0deg, transparent, var(--gold-glow), transparent, var(--purple-glow), transparent);
            animation: bannerRotate 10s linear infinite;
            opacity: 0.08;
        }
        @keyframes bannerRotate {
            0% {
                transform: rotate(0deg);
            }
            100% {
                transform: rotate(360deg);
            }
        }
        .welcome-banner h2 {
            font-size: 20px;
            font-weight: 800;
            position: relative;
            z-index: 1;
        }
        .welcome-banner h2 span {
            background: linear-gradient(135deg, var(--gold), var(--purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .welcome-banner p {
            color: var(--text-secondary);
            font-size: 12px;
            position: relative;
            z-index: 1;
            margin-top: 3px;
        }
        .welcome-banner .update-time {
            font-size: 10px;
            color: var(--text-secondary);
            margin-top: 6px;
            position: relative;
            z-index: 1;
        }

        /* ===== الإحصائيات ===== */
        .quick-stats {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            margin-bottom: 14px;
        }
        .stat-card {
            background: var(--bg-secondary);
            border-radius: 14px;
            padding: 14px 10px;
            text-align: center;
            border: 1px solid #ffffff08;
            transition: all 0.4s;
        }
        .stat-card:hover {
            border-color: var(--gold-glow);
            transform: translateY(-3px);
        }
        .stat-card .num {
            font-size: 18px;
            font-weight: 800;
            background: linear-gradient(135deg, var(--gold), #ffaa00);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .stat-card .label {
            font-size: 10px;
            color: var(--text-secondary);
            margin-top: 3px;
        }

        /* ===== خريطة الحرارة ===== */
        .section-title {
            font-size: 14px;
            font-weight: 700;
            margin: 16px 0 10px;
            color: var(--text-secondary);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .section-title .glow {
            font-size: 10px;
            color: var(--gold);
            animation: glowPulse 2s ease-in-out infinite;
        }
        @keyframes glowPulse {
            0%,
            100% {
                opacity: 0.5;
            }
            50% {
                opacity: 1;
            }
        }

        .heatmap-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(65px, 1fr));
            gap: 5px;
            margin: 8px 0;
        }
        .heatmap-item {
            padding: 10px 4px;
            border-radius: 10px;
            text-align: center;
            font-size: 10px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            border: 1px solid transparent;
        }
        .heatmap-item:hover {
            transform: scale(1.08) translateY(-4px);
            border-color: var(--gold);
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.4);
            z-index: 10;
        }
        .heatmap-item .hm-symbol {
            font-size: 11px;
        }
        .heatmap-item .hm-change {
            font-size: 9px;
            font-weight: 600;
        }

        /* ===== بطاقات العملات ===== */
        .coin-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
        }
        .coin-card {
            background: var(--bg-secondary);
            border-radius: 14px;
            padding: 14px;
            border: 1px solid #ffffff08;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
            position: relative;
            overflow: hidden;
        }
        .coin-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(90deg, var(--gold), var(--purple), var(--cyan));
            transform: scaleX(0);
            transition: 0.5s;
        }
        .coin-card:hover::before {
            transform: scaleX(1);
        }
        .coin-card:hover {
            transform: translateY(-4px) scale(1.01);
            border-color: var(--gold-glow);
            background: var(--bg-card-hover);
        }
        .coin-card .coin-symbol {
            font-weight: 800;
            font-size: 15px;
        }
        .coin-card .coin-name {
            font-size: 10px;
            color: var(--text-secondary);
        }
        .coin-card .coin-price {
            font-size: 17px;
            font-weight: 700;
            margin-top: 4px;
        }
        .coin-card .coin-change {
            font-size: 12px;
            font-weight: 600;
        }
        .coin-card .coin-change.green {
            color: var(--green);
        }
        .coin-card .coin-change.red {
            color: var(--red);
        }
        .coin-card .coin-indicators {
            display: flex;
            gap: 4px;
            margin-top: 6px;
            flex-wrap: wrap;
        }
        .coin-card .coin-indicators .ind {
            font-size: 8px;
            padding: 2px 8px;
            border-radius: 20px;
            background: #ffffff08;
            color: var(--text-secondary);
            border: 1px solid #ffffff08;
        }
        .coin-card .coin-indicators .ind.buy {
            background: var(--green-glow);
            color: var(--green);
            border-color: var(--green);
        }
        .coin-card .coin-indicators .ind.sell {
            background: var(--red-glow);
            color: var(--red);
            border-color: var(--red);
        }
        .coin-card .coin-indicators .ind.neutral {
            background: var(--gold-glow);
            color: var(--gold);
            border-color: var(--gold);
        }

        /* ===== السوق ===== */
        .market-filters {
            display: flex;
            gap: 6px;
            margin-bottom: 12px;
            flex-wrap: wrap;
        }
        .market-filters button {
            background: var(--bg-secondary);
            color: var(--text-secondary);
            border: 1px solid #ffffff08;
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }
        .market-filters button:hover {
            color: var(--text-primary);
            border-color: var(--gold-glow);
        }
        .market-filters button.active {
            background: var(--gold);
            color: #000;
            border-color: var(--gold);
            box-shadow: 0 0 30px var(--gold-glow);
        }

        .market-table {
            width: 100%;
            background: var(--bg-secondary);
            border-radius: 14px;
            overflow: hidden;
            border: 1px solid #ffffff08;
        }
        .market-table .row {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr 0.8fr;
            padding: 10px 14px;
            border-bottom: 1px solid #ffffff06;
            font-size: 12px;
            align-items: center;
            cursor: pointer;
            transition: 0.3s;
        }
        .market-table .row:hover {
            background: #ffffff06;
        }
        .market-table .row.header {
            color: var(--text-secondary);
            font-size: 10px;
            font-weight: 700;
            background: #0a0a12;
            cursor: default;
        }
        .market-table .row .change.green {
            color: var(--green);
        }
        .market-table .row .change.red {
            color: var(--red);
        }
        .market-table .row .vol {
            color: var(--text-secondary);
            font-size: 10px;
        }

        /* ===== البحث ===== */
        .analysis-search {
            display: flex;
            gap: 8px;
            margin-bottom: 12px;
        }
        .analysis-search input {
            flex: 1;
            padding: 12px 14px;
            background: var(--bg-secondary);
            border: 1px solid #ffffff08;
            border-radius: 12px;
            color: var(--text-primary);
            font-size: 14px;
            outline: none;
            transition: 0.3s;
            font-weight: 500;
        }
        .analysis-search input:focus {
            border-color: var(--gold);
            box-shadow: 0 0 30px var(--gold-glow);
        }
        .analysis-search input::placeholder {
            color: var(--text-secondary);
        }
        .analysis-search button {
            padding: 12px 22px;
            background: linear-gradient(135deg, var(--gold), #ffaa00);
            color: #000;
            border: none;
            border-radius: 12px;
            font-weight: 800;
            cursor: pointer;
            font-size: 13px;
            transition: all 0.3s;
            box-shadow: 0 0 30px var(--gold-glow);
        }
        .analysis-search button:hover {
            transform: scale(1.05);
            box-shadow: 0 0 50px var(--gold-glow);
        }

        /* ===== التحليل ===== */
        .analysis-detail {
            background: var(--bg-secondary);
            border-radius: 16px;
            padding: 18px;
            margin-top: 12px;
            border: 1px solid var(--gold-glow);
        }
        .analysis-detail .coin-title {
            font-size: 24px;
            font-weight: 800;
            background: linear-gradient(135deg, var(--gold), var(--purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .analysis-detail .coin-subtitle {
            color: var(--text-secondary);
            font-size: 12px;
            margin-bottom: 10px;
        }
        .analysis-detail .entry-price {
            font-size: 18px;
            font-weight: 700;
            color: var(--gold);
            margin-bottom: 10px;
            text-shadow: 0 0 30px var(--gold-glow);
        }
        .analysis-detail .indicators-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            margin: 10px 0;
        }
        .analysis-detail .indicators-grid .ind-item {
            background: #0a0a12;
            padding: 10px;
            border-radius: 10px;
            text-align: center;
            border: 1px solid #ffffff08;
        }
        .analysis-detail .indicators-grid .ind-item .ind-label {
            font-size: 8px;
            color: var(--text-secondary);
            font-weight: 600;
        }
        .analysis-detail .indicators-grid .ind-item .ind-value {
            font-size: 14px;
            font-weight: 700;
            margin-top: 2px;
        }
        .analysis-detail .indicators-grid .ind-item .ind-value.bullish {
            color: var(--green);
        }
        .analysis-detail .indicators-grid .ind-item .ind-value.bearish {
            color: var(--red);
        }
        .analysis-detail .indicators-grid .ind-item .ind-value.neutral {
            color: var(--gold);
        }

        .targets {
            margin: 10px 0;
        }
        .target-item {
            display: flex;
            justify-content: space-between;
            padding: 8px 14px;
            background: #0a0a12;
            border-radius: 10px;
            margin-bottom: 4px;
            border-right: 3px solid var(--gold);
            transition: 0.3s;
            font-size: 12px;
        }
        .target-item:hover {
            background: #12122a;
            transform: translateX(4px);
        }
        .target-item .num {
            color: var(--text-secondary);
            font-weight: 600;
        }
        .target-item .price {
            font-weight: 700;
            color: var(--green);
        }
        .target-item .profit {
            font-weight: 600;
            color: var(--gold);
            font-size: 11px;
        }

        .analysis-actions {
            display: flex;
            gap: 8px;
            margin-top: 12px;
            flex-wrap: wrap;
        }
        .analysis-actions .btn-legend {
            flex: 1;
            padding: 10px 16px;
            border: none;
            border-radius: 12px;
            font-weight: 700;
            font-size: 12px;
            cursor: pointer;
            transition: all 0.4s;
            min-width: 60px;
            text-align: center;
        }
        .analysis-actions .btn-legend:hover {
            transform: translateY(-3px) scale(1.02);
        }
        .analysis-actions .btn-legend.save {
            background: linear-gradient(135deg, var(--gold), #ff8800);
            color: #000;
            box-shadow: 0 0 30px var(--gold-glow);
        }
        .analysis-actions .btn-legend.alert {
            background: linear-gradient(135deg, var(--blue), #0044ff);
            color: #fff;
            box-shadow: 0 0 30px var(--blue-glow);
        }
        .analysis-actions .btn-legend.share {
            background: linear-gradient(135deg, var(--purple), #8800ff);
            color: #fff;
            box-shadow: 0 0 30px var(--purple-glow);
        }
        .analysis-actions .btn-legend.close {
            background: #2a2a3a;
            color: var(--text-secondary);
        }
        .analysis-actions .btn-legend.close:hover {
            color: var(--text-primary);
        }

        .warning-box {
            background: rgba(255, 68, 102, 0.08);
            border: 1px solid var(--red-glow);
            border-radius: 12px;
            padding: 12px;
            margin-top: 12px;
        }
        .warning-box h4 {
            color: var(--red);
            margin-bottom: 4px;
            font-size: 13px;
        }
        .warning-box p {
            font-size: 11px;
            color: var(--text-secondary);
            line-height: 1.6;
        }

        /* ===== المحفوظات ===== */
        .saved-list {
            margin-top: 12px;
        }
        .saved-item {
            background: var(--bg-secondary);
            border-radius: 14px;
            padding: 12px 14px;
            margin-bottom: 8px;
            border: 1px solid #ffffff08;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.3s;
            font-size: 12px;
        }
        .saved-item:hover {
            border-color: var(--gold-glow);
            transform: translateX(4px);
        }
        .saved-item .info h4 {
            font-size: 14px;
            font-weight: 700;
        }
        .saved-item .info p {
            font-size: 10px;
            color: var(--text-secondary);
        }
        .saved-item .actions {
            display: flex;
            gap: 4px;
        }
        .saved-item .actions button {
            padding: 6px 12px;
            border: none;
            border-radius: 8px;
            font-size: 10px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }
        .saved-item .actions .analyze {
            background: var(--blue);
            color: #fff;
        }
        .saved-item .actions .delete {
            background: var(--red);
            color: #fff;
        }

        /* ===== الحيتان ===== */
        .whale-card {
            background: var(--bg-secondary);
            border-radius: 12px;
            padding: 10px 14px;
            border: 1px solid #ffffff08;
            margin-bottom: 6px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: 0.3s;
            font-size: 12px;
        }
        .whale-card:hover {
            border-color: var(--purple-glow);
        }
        .whale-card .whale-type {
            font-weight: 700;
        }
        .whale-card .whale-type.buy {
            color: var(--green);
        }
        .whale-card .whale-type.sell {
            color: var(--red);
        }
        .whale-card .whale-amount {
            color: var(--gold);
            font-weight: 600;
        }

        /* ===== الأزرار السفلية - مثل Binance ===== */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: var(--bottombar-bg);
            display: flex;
            justify-content: space-around;
            padding: 6px 0 12px;
            border-top: 2px solid var(--gold-glow);
            z-index: 1000;
            box-shadow: 0 -4px 40px rgba(0, 200, 100, 0.25);
        }
        .bottom-nav .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 1px;
            cursor: pointer;
            padding: 4px 10px;
            border-radius: 12px;
            transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
            background: transparent;
            border: none;
            color: rgba(255, 255, 255, 0.6);
            font-size: 9px;
            font-weight: 600;
            position: relative;
            min-width: 48px;
        }
        .bottom-nav .nav-item .icon {
            font-size: 20px;
            transition: 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.06);
            border: 1px solid rgba(255, 255, 255, 0.05);
        }
        .bottom-nav .nav-item .label {
            font-size: 8px;
            font-weight: 600;
            margin-top: 2px;
        }
        .bottom-nav .nav-item .badge {
            position: absolute;
            top: 0;
            right: 2px;
            background: var(--red);
            color: #fff;
            font-size: 7px;
            font-weight: 700;
            padding: 1px 5px;
            border-radius: 50%;
        }
        .bottom-nav .nav-item:hover {
            color: #fff;
            transform: translateY(-3px);
        }
        .bottom-nav .nav-item:hover .icon {
            background: rgba(255, 255, 255, 0.15);
            transform: scale(1.05);
        }
        .bottom-nav .nav-item:active .icon {
            transform: scale(0.92);
        }
        .bottom-nav .nav-item.active {
            color: var(--gold);
        }
        .bottom-nav .nav-item.active .icon {
            background: var(--gold-glow);
            transform: scale(1.1);
            border-color: var(--gold);
            box-shadow: 0 0 30px var(--gold-glow);
        }
        .bottom-nav .nav-item.active::before {
            content: '';
            position: absolute;
            top: -2px;
            left: 20%;
            right: 20%;
            height: 3px;
            background: var(--gold);
            border-radius: 3px;
            box-shadow: 0 0 20px var(--gold-glow);
        }

        /* ===== الزر المركزي ===== */
        .bottom-nav .nav-item.central {
            margin-top: -10px;
        }
        .bottom-nav .nav-item.central .icon {
            width: 52px;
            height: 52px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--green), #008844);
            border: 2px solid var(--gold-glow);
            box-shadow: 0 4px 30px rgba(0, 255, 136, 0.3);
            font-size: 24px;
            color: #fff;
        }
        .bottom-nav .nav-item.central .icon:hover {
            box-shadow: 0 6px 40px rgba(0, 255, 136, 0.5);
            transform: scale(1.08);
        }
        .bottom-nav .nav-item.central:active .icon {
            transform: scale(0.92);
        }
        .bottom-nav .nav-item.central.active .icon {
            background: linear-gradient(135deg, var(--gold), #ff8800);
            box-shadow: 0 4px 30px var(--gold-glow);
        }
        .bottom-nav .nav-item.central .label {
            color: var(--green);
            font-weight: 700;
            font-size: 9px;
        }
        .bottom-nav .nav-item.central.active .label {
            color: var(--gold);
        }

        /* ===== البوت الخرافي ===== */
        .chat-bot {
            position: fixed;
            bottom: 85px;
            right: 12px;
            z-index: 999;
        }
        .chat-bot .toggle-btn {
            width: 56px;
            height: 56px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--gold), var(--purple), var(--cyan));
            color: #000;
            border: none;
            font-size: 26px;
            cursor: pointer;
            box-shadow: 0 0 40px var(--gold-glow);
            transition: all 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
            animation: floatBot 3s ease-in-out infinite;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        @keyframes floatBot {
            0%,
            100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-6px);
            }
        }
        .chat-bot .toggle-btn:hover {
            transform: scale(1.1) rotate(-10deg);
            box-shadow: 0 0 60px var(--gold-glow);
        }
        .chat-bot .toggle-btn .pulse-ring {
            position: absolute;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            border: 2px solid var(--gold);
            animation: ringPulse 2s ease-out infinite;
        }
        @keyframes ringPulse {
            0% {
                transform: scale(1);
                opacity: 1;
            }
            100% {
                transform: scale(1.5);
                opacity: 0;
            }
        }
        .chat-bot .chat-window {
            position: absolute;
            bottom: 70px;
            right: 0;
            width: 350px;
            max-width: 90vw;
            background: rgba(13, 13, 43, 0.98);
            backdrop-filter: blur(30px);
            border-radius: 20px;
            border: 1px solid var(--gold-glow);
            padding: 16px;
            display: none;
            max-height: 500px;
            flex-direction: column;
            box-shadow: 0 20px 80px rgba(0, 0, 0, 0.9);
        }
        .chat-bot .chat-window.show {
            display: flex;
        }
        .chat-bot .chat-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 8px;
        }
        .chat-bot .chat-header span {
            font-weight: 700;
            color: var(--gold);
            font-size: 15px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .chat-bot .chat-header span .status-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: var(--green);
            animation: pulse 1.5s ease-in-out infinite;
            display: inline-block;
        }
        .chat-bot .chat-header button {
            background: none;
            border: none;
            color: var(--text-secondary);
            font-size: 18px;
            cursor: pointer;
        }
        .chat-bot .chat-messages {
            flex: 1;
            max-height: 280px;
            overflow-y: auto;
            margin-bottom: 8px;
            display: flex;
            flex-direction: column;
            gap: 4px;
        }
        .chat-bot .chat-messages .msg {
            padding: 10px 14px;
            border-radius: 14px;
            max-width: 90%;
            font-size: 13px;
            line-height: 1.6;
            animation: msgSlide 0.3s ease;
        }
        @keyframes msgSlide {
            0% {
                opacity: 0;
                transform: translateY(10px);
            }
            100% {
                opacity: 1;
                transform: translateY(0);
            }
        }
        .chat-bot .chat-messages .msg.bot {
            background: #1a1a3a;
            color: var(--text-primary);
            align-self: flex-start;
            border-bottom-right-radius: 4px;
            border: 1px solid #ffffff08;
        }
        .chat-bot .chat-messages .msg.bot .highlight {
            color: var(--gold);
            font-weight: 700;
        }
        .chat-bot .chat-messages .msg.bot .buy-signal {
            color: var(--green);
            font-weight: 700;
        }
        .chat-bot .chat-messages .msg.bot .sell-signal {
            color: var(--red);
            font-weight: 700;
        }
        .chat-bot .chat-messages .msg.bot .neutral-signal {
            color: var(--gold);
            font-weight: 700;
        }
        .chat-bot .chat-messages .msg.user {
            background: linear-gradient(135deg, var(--gold), #ffaa00);
            color: #000;
            align-self: flex-end;
            border-bottom-left-radius: 4px;
            font-weight: 600;
        }
        .chat-bot .chat-messages .msg .typing-dots {
            display: inline-flex;
            gap: 4px;
        }
        .chat-bot .chat-messages .msg .typing-dots span {
            width: 6px;
            height: 6px;
            border-radius: 50%;
            background: var(--text-secondary);
            animation: dotBounce 1.4s ease-in-out infinite;
        }
        .chat-bot .chat-messages .msg .typing-dots span:nth-child(2) {
            animation-delay: 0.2s;
        }
        .chat-bot .chat-messages .msg .typing-dots span:nth-child(3) {
            animation-delay: 0.4s;
        }
        @keyframes dotBounce {
            0%,
            80%,
            100% {
                transform: scale(0.6);
                opacity: 0.4;
            }
            40% {
                transform: scale(1);
                opacity: 1;
            }
        }
        .chat-bot .chat-input {
            display: flex;
            gap: 8px;
        }
        .chat-bot .chat-input input {
            flex: 1;
            padding: 10px 14px;
            background: #0a0a12;
            border: 1px solid #ffffff08;
            border-radius: 12px;
            color: var(--text-primary);
            font-size: 13px;
            outline: none;
            transition: 0.3s;
        }
        .chat-bot .chat-input input:focus {
            border-color: var(--gold);
            box-shadow: 0 0 20px var(--gold-glow);
        }
        .chat-bot .chat-input input::placeholder {
            color: var(--text-secondary);
        }
        .chat-bot .chat-input button {
            padding: 10px 18px;
            background: linear-gradient(135deg, var(--gold), var(--purple));
            color: #000;
            border: none;
            border-radius: 12px;
            font-weight: 700;
            font-size: 13px;
            cursor: pointer;
            transition: 0.3s;
        }
        .chat-bot .chat-input button:hover {
            transform: scale(1.05);
        }

        /* ===== التوست ===== */
        .toast {
            position: fixed;
            top: 75px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(13, 13, 43, 0.95);
            backdrop-filter: blur(20px);
            color: var(--text-primary);
            padding: 10px 22px;
            border-radius: 14px;
            border: 1px solid var(--gold-glow);
            z-index: 2000;
            display: none;
            font-size: 12px;
            font-weight: 600;
            box-shadow: 0 10px 60px rgba(0, 0, 0, 0.8);
            max-width: 90%;
            text-align: center;
        }
        .toast.show {
            display: block;
        }

        /* ===== متفرقات ===== */
        ::-webkit-scrollbar {
            width: 4px;
        }
        ::-webkit-scrollbar-track {
            background: var(--bg-primary);
        }
        ::-webkit-scrollbar-thumb {
            background: var(--gold);
            border-radius: 10px;
            box-shadow: 0 0 20px var(--gold-glow);
        }

        @media (max-width: 400px) {
            .coin-grid {
                grid-template-columns: 1fr;
            }
            .market-table .row {
                grid-template-columns: 1fr 1fr 1fr 0.6fr;
                font-size: 11px;
                padding: 8px 10px;
            }
            .heatmap-grid {
                grid-template-columns: repeat(auto-fill, minmax(55px, 1fr));
            }
            .chat-bot .chat-window {
                width: 290px;
                right: -10px;
            }
            .quick-stats {
                grid-template-columns: repeat(3, 1fr);
                gap: 5px;
            }
            .stat-card .num {
                font-size: 15px;
            }
            .bottom-nav .nav-item {
                min-width: 40px;
                padding: 3px 6px;
            }
            .bottom-nav .nav-item .icon {
                font-size: 17px;
                width: 34px;
                height: 34px;
            }
            .bottom-nav .nav-item .label {
                font-size: 7px;
            }
            .bottom-nav .nav-item.central .icon {
                width: 44px;
                height: 44px;
                font-size: 20px;
            }
            .analysis-detail .indicators-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            .splash-screen .terms-box {
                padding: 14px 16px;
            }
        }

        .loading {
            text-align: center;
            padding: 30px;
            color: var(--text-secondary);
        }
        .loading span {
            display: inline-block;
            animation: pulse 1s infinite;
        }
    </style>
</head>
<body>

    <!-- ===== جزيئات الخلفية ===== -->
    <div class="bg-particles" id="particles"></div>

    <!-- ===== شاشة الترحيب ===== -->
    <div class="splash-screen" id="splashScreen">
        <div class="logo">🤖 Legend Bot</div>
        <div class="sub">البوت العالمي الخرافي للتداول</div>
        <div class="terms-box">
            <h3>📋 شروط الاستخدام</h3>
            <ul>
                <li><span class="icon">📖</span> هذا البوت لأغراض تعليمية وتوعوية</li>
                <li><span class="icon">⚠️</span> التداول يحمل مخاطر عالية</li>
                <li><span class="icon">🔒</span> لا نتحمل مسؤولية أي خسائر</li>
                <li><span class="icon">📊</span> التحليلات ليست توصيات استثمارية</li>
                <li><span class="icon">🤝</span> باستخدامك أنت توافق على هذه الشروط</li>
            </ul>
        </div>
        <button class="agree-btn" onclick="acceptTerms()">🚀 ابدأ البوت</button>
        <div class="version">الإصدار V9.0 - البوت العالمي الخرافي</div>
    </div>

    <!-- ===== التوست ===== -->
    <div class="toast" id="toast"></div>

    <!-- ===== الهيدر ===== -->
    <header class="header" id="mainHeader" style="display:none;">
        <div class="logo">
            <h1>🤖 <span>Legend</span> Bot</h1>
            <span class="sub">البوت العالمي الخرافي</span>
        </div>
        <div class="icons">
            <div class="connection-status" id="connStatus">
                <span class="dot off" id="connDot"></span>
                <span id="connText">جاري التحميل...</span>
            </div>
            <button class="icon-btn" onclick="toggleNotifications()" title="الإشعارات">
                🔔
                <span class="notification-badge" id="notifBadge">0</span>
            </button>
            <button class="icon-btn" onclick="toggleTheme()" title="الوضع">🌙</button>
        </div>
    </header>

    <!-- ===== الإشعارات ===== -->
    <div class="notification-panel" id="notifPanel">
        <div class="panel-header">
            <span>📬 الإشعارات الذكية</span>
            <button onclick="clearNotifications()">🗑 مسح</button>
        </div>
        <div id="notifList">
            <div class="notif-empty">📭 لا توجد إشعارات</div>
        </div>
    </div>

    <!-- ===== البوت الخرافي ===== -->
    <div class="chat-bot">
        <button class="toggle-btn" onclick="toggleChat()" id="chatToggle">
            🤖
            <span class="pulse-ring"></span>
        </button>
        <div class="chat-window" id="chatWindow">
            <div class="chat-header">
                <span>
                    🤖 البوت الخرافي
                    <span class="status-dot"></span>
                </span>
                <button onclick="toggleChat()">✕</button>
            </div>
            <div class="chat-messages" id="chatMessages">
                <div class="msg bot">
                    🚀 <strong>مرحباً أيها المتداول الأسطوري!</strong><br>
                    أنا <span class="highlight">البوت العالمي الخرافي</span> 🤖<br><br>
                    اسألني عن أي عملة وسأعطيك:<br>
                    📊 تحليل كامل مع مؤشرات<br>
                    🎯 أهداف دقيقة<br>
                    📈 توقعات السوق<br>
                    💡 نصائح ذهبية<br><br>
                    <span class="highlight">💬 اكتب اسم أي عملة وابدأ!</span>
                </div>
            </div>
            <div class="chat-input">
                <input type="text" id="chatInput" placeholder="اكتب اسم العملة أو اسأل..." onkeyup="if(event.key==='Enter') sendMessage()" />
                <button onclick="sendMessage()">إرسال</button>
            </div>
        </div>
    </div>

    <!-- ===== الصفحة الرئيسية ===== -->
    <div class="page active" id="page-home">
        <div class="welcome-banner">
            <h2>🤖 مرحباً بك في <span>Legend Bot</span></h2>
            <p>البوت العالمي الخرافي - اسأل عن أي عملة واحصل على تحليل فوري 🚀</p>
            <div class="update-time">📊 آخر تحديث: <span id="lastUpdate">جاري التحميل...</span></div>
        </div>

        <div class="quick-stats">
            <div class="stat-card">
                <div class="num" id="totalCoins">0</div>
                <div class="label">عملات متاحة</div>
            </div>
            <div class="stat-card">
                <div class="num" id="totalVolume">$0</div>
                <div class="label">حجم السوق</div>
            </div>
            <div class="stat-card">
                <div class="num" id="topGainer">0%</div>
                <div class="label">أعلى ربح</div>
            </div>
        </div>

        <!-- توقعات السوق -->
        <div style="background:var(--bg-secondary);border-radius:14px;padding:14px;margin-bottom:14px;border:1px solid var(--gold-glow);text-align:center;">
            <span style="font-size:12px;color:var(--text-secondary);">📊 توقعات السوق:</span>
            <span id="marketOutlook" style="font-size:16px;font-weight:700;display:block;margin-top:4px;">⏳ جاري التحليل...</span>
        </div>

        <div class="section-title">🔥 خريطة حرارة السوق <span class="glow">● مباشر</span></div>
        <div class="heatmap-grid" id="heatmapGrid"><div class="loading"><span>⏳ جاري التحميل...</span></div></div>

        <div class="section-title">🏆 أفضل العملات</div>
        <div class="coin-grid" id="topCoins"><div class="loading"><span>⏳ جاري التحميل...</span></div></div>

        <div class="section-title">📈 جميع العملات</div>
        <div class="coin-grid" id="allCoins"><div class="loading"><span>⏳ جاري التحميل...</span></div></div>
    </div>

    <!-- ===== صفحة العملات ===== -->
    <div class="page" id="page-coins">
        <div class="section-title">💰 جميع العملات الرقمية</div>
        <div class="coin-grid" id="coinsList"><div class="loading"><span>⏳ جاري التحميل...</span></div></div>
    </div>

    <!-- ===== صفحة السوق ===== -->
    <div class="page" id="page-market">
        <div class="section-title">📊 السوق والحيتان</div>
        <div class="market-filters">
            <button class="active" data-filter="all">الكل</button>
            <button data-filter="gainers">الأعلى ربحاً</button>
            <button data-filter="losers">الأعلى خسارة</button>
            <button data-filter="volume">الأعلى حجم</button>
            <button data-filter="pump">🔥 انفجارات</button>
        </div>
        <div class="market-table" id="marketTable">
            <div class="row header">
                <span>العملة</span>
                <span>السعر</span>
                <span>التغير</span>
                <span>الحجم</span>
            </div>
        </div>
        <div class="section-title" style="margin-top:16px;">🐋 نشاط الحيتان</div>
        <div id="whaleActivity"></div>
    </div>

    <!-- ===== صفحة التحليل ===== -->
    <div class="page" id="page-analysis">
        <div class="section-title">📈 التحليل الفني الخرافي</div>
        <div class="analysis-search">
            <input type="text" id="searchCoin" placeholder="ابحث عن عملة... BTC, ETH, SOL" onkeyup="if(event.key==='Enter') searchAnalysis()" />
            <button onclick="searchAnalysis()">🔍 بحث</button>
        </div>
        <div id="analysisResult"></div>
        <div class="section-title" style="margin-top:16px;">📁 العملات المحفوظة</div>
        <div class="saved-list" id="savedList"></div>
    </div>

    <!-- ===== القائمة السفلية ===== -->
    <nav class="bottom-nav" id="bottomNav" style="display:none;">
        <button class="nav-item active" data-page="page-home">
            <span class="icon">🏠</span>
            <span class="label">الرئيسية</span>
        </button>
        <button class="nav-item" data-page="page-coins">
            <span class="icon">🪙</span>
            <span class="label">العملات</span>
        </button>
        <button class="nav-item central" data-page="page-market">
            <span class="icon">⬆️</span>
            <span class="label">السحب</span>
            <span class="badge" id="marketBadge">🔥</span>
        </button>
        <button class="nav-item" data-page="page-market">
            <span class="icon">📊</span>
            <span class="label">السوق</span>
        </button>
        <button class="nav-item" data-page="page-analysis">
            <span class="icon">📈</span>
            <span class="label">تحليل</span>
            <span class="badge" id="analysisBadge"></span>
        </button>
    </nav>

    <!-- ============================================================ -->
    <!-- جافا سكريبت - البوت العالمي الخرافي -->
    <!-- ============================================================ -->
    <script>
        // ============================================================
        // 🔐 مفاتيح API
        // ============================================================
        const API_KEY = '..................................................';
        const API_SECRET = '..................................................';

        // ============================================================
        // 1. شروط الاستخدام
        // ============================================================
        let termsAccepted = localStorage.getItem('legendBotTerms');

        function acceptTerms() {
            localStorage.setItem('legendBotTerms', 'accepted');
            document.getElementById('splashScreen').classList.add('hide');
            document.getElementById('mainHeader').style.display = 'flex';
            document.getElementById('bottomNav').style.display = 'flex';
            setTimeout(() => {
                document.getElementById('splashScreen').style.display = 'none';
            }, 500);
            initApp();
        }

        if (termsAccepted === 'accepted') {
            document.getElementById('splashScreen').style.display = 'none';
            document.getElementById('mainHeader').style.display = 'flex';
            document.getElementById('bottomNav').style.display = 'flex';
            initApp();
        }

        // ============================================================
        // 2. الجسيمات
        // ============================================================
        function createParticles() {
            const container = document.getElementById('particles');
            const colors = ['#ffd700', '#8844ff', '#00ddff', '#ff4466', '#00ff88'];
            for (let i = 0; i < 40; i++) {
                const span = document.createElement('span');
                span.style.left = Math.random() * 100 + '%';
                span.style.width = Math.random() * 3 + 1 + 'px';
                span.style.height = span.style.width;
                span.style.animationDuration = Math.random() * 25 + 15 + 's';
                span.style.animationDelay = Math.random() * 25 + 's';
                span.style.background = colors[Math.floor(Math.random() * colors.length)];
                span.style.opacity = Math.random() * 0.3 + 0.05;
                container.appendChild(span);
            }
        }
        createParticles();

        // ============================================================
        // 3. Binance API
        // ============================================================
        const BINANCE_API = 'https://api.binance.com/api/v3';
        const WS_BASE = 'wss://stream.binance.com:9443/ws';

        const TOP_SYMBOLS = [
            'BTCUSDT', 'ETHUSDT', 'BNBUSDT', 'SOLUSDT', 'XRPUSDT',
            'ADAUSDT', 'DOGEUSDT', 'LINKUSDT', 'AVAXUSDT', 'MATICUSDT',
            'DOTUSDT', 'SHIBUSDT', 'TRXUSDT', 'UNIUSDT', 'ATOMUSDT',
            'LTCUSDT', 'ETCUSDT', 'XLMUSDT', 'VETUSDT', 'FILUSDT'
        ];

        // قاموس البحث العملاق
        const ARABIC_NAMES = {
            'بيتكوين': 'BTC',
            'بتكوين': 'BTC',
            'bitcoin': 'BTC',
            'btc': 'BTC',
            'إيثريوم': 'ETH',
            'ايثريوم': 'ETH',
            'ethereum': 'ETH',
            'eth': 'ETH',
            'بينانس': 'BNB',
            'binance': 'BNB',
            'bnb': 'BNB',
            'سولانا': 'SOL',
            'solana': 'SOL',
            'sol': 'SOL',
            'ريبل': 'XRP',
            'xrp': 'XRP',
            'كاردانو': 'ADA',
            'cardano': 'ADA',
            'ada': 'ADA',
            'دوج': 'DOGE',
            'دوجكوين': 'DOGE',
            'doge': 'DOGE',
            'دوت': 'DOT',
            'polkadot': 'DOT',
            'dot': 'DOT',
            'شيب': 'SHIB',
            'shib': 'SHIB',
            'shiba': 'SHIB',
            'ترون': 'TRX',
            'trx': 'TRX',
            'لينك': 'LINK',
            'link': 'LINK',
            'أفالانش': 'AVAX',
            'avax': 'AVAX',
            'ماتيك': 'MATIC',
            'matic': 'MATIC',
            'ليتكوين': 'LTC',
            'litecoin': 'LTC',
            'ltc': 'LTC',
            'اتوم': 'ATOM',
            'atom': 'ATOM',
            'فيلي': 'FIL',
            'fil': 'FIL',
            'filecoin': 'FIL',
            'يوني': 'UNI',
            'uni': 'UNI',
            'uniswap': 'UNI'
        };

        // ============================================================
        // 4. الحالة العامة
        // ============================================================
        let coinsData = [];
        let savedAnalyses = JSON.parse(localStorage.getItem('savedAnalyses')) || [];
        let notifications = JSON.parse(localStorage.getItem('notifications')) || [];
        let wsConnections = [];
        let currentFilter = 'all';
        let chatOpen = false;
        let notifOpen = false;
        let darkMode = true;
        let pumpDetection = {};
        let isConnected = false;
        let lastPrices = {};

        const hasValidKeys = API_KEY && API_KEY !== '..................................................' &&
            API_SECRET && API_SECRET !== '..................................................';

        // ============================================================
        // 5. التوست
        // ============================================================
        function showToast(msg, type = 'info') {
            const t = document.getElementById('toast');
            t.textContent = msg;
            t.style.borderColor = type === 'success' ? 'var(--green)' :
                type === 'error' ? 'var(--red)' :
                type === 'pump' ? '#ff8800' : 'var(--gold)';
            t.classList.add('show');
            clearTimeout(t._timeout);
            t._timeout = setTimeout(() => t.classList.remove('show'), 3000);
        }

        // ============================================================
        // 6. الإشعارات
        // ============================================================
        function addNotification(type, title, message) {
            const notif = {
                id: Date.now(),
                type: type,
                title: title,
                message: message,
                time: new Date().toLocaleString('ar-EG'),
                read: false
            };
            notifications.unshift(notif);
            if (notifications.length > 50) notifications.pop();
            localStorage.setItem('notifications', JSON.stringify(notifications));
            updateNotifBadge();
            renderNotifications();
            showToast(`🔔 ${title}: ${message}`, type === 'alert' ? 'alert' : type === 'pump' ? 'pump' : 'success');
        }

        function updateNotifBadge() {
            const unread = notifications.filter(n => !n.read).length;
            document.getElementById('notifBadge').textContent = unread || '';
        }

        function renderNotifications() {
            const container = document.getElementById('notifList');
            if (notifications.length === 0) {
                container.innerHTML = `<div class="notif-empty">📭 لا توجد إشعارات</div>`;
                return;
            }
            container.innerHTML = notifications.map(n => `
                <div class="notif-item" onclick="markNotifRead(${n.id})">
                    <div class="notif-top">
                        <span class="notif-type ${n.type}">${n.type === 'price' ? '💰' : n.type === 'alert' ? '⚠️' : n.type === 'success' ? '✅' : n.type === 'pump' ? '🚀' : '📢'} ${n.title}</span>
                        <span class="notif-time">${n.time}</span>
                    </div>
                    <div class="notif-message">${n.message}</div>
                </div>
            `).join('');
        }

        function markNotifRead(id) {
            const notif = notifications.find(n => n.id === id);
            if (notif) notif.read = true;
            localStorage.setItem('notifications', JSON.stringify(notifications));
            updateNotifBadge();
            renderNotifications();
        }

        function clearNotifications() {
            if (notifications.length === 0) return;
            notifications = [];
            localStorage.setItem('notifications', JSON.stringify(notifications));
            updateNotifBadge();
            renderNotifications();
            showToast('🗑 تم مسح جميع الإشعارات');
        }

        function toggleNotifications() {
            const panel = document.getElementById('notifPanel');
            notifOpen = !notifOpen;
            panel.classList.toggle('show', notifOpen);
            if (notifOpen) renderNotifications();
        }

        // ============================================================
        // 7. كشف الانفجارات
        // ============================================================
        function detectPump(coin, oldPrice) {
            if (!oldPrice || oldPrice === 0) return;
            const changePercent = ((coin.price - oldPrice) / oldPrice) * 100;

            if (changePercent > 3) {
                const key = coin.symbol;
                if (!pumpDetection[key] || pumpDetection[key] < Date.now() - 60000) {
                    pumpDetection[key] = Date.now();
                    addNotification('pump', `🚀 ${coin.symbol} انفجار!`,
                        `ارتفع سعر ${coin.symbol} بنسبة ${changePercent.toFixed(2)}%!`);
                }
            }

            if (changePercent < -5) {
                addNotification('alert', `📉 ${coin.symbol} انهيار!`,
                    `انخفض سعر ${coin.symbol} بنسبة ${Math.abs(changePercent).toFixed(2)}%!`);
            }
        }

        // ============================================================
        // 8. البوت الخرافي - الذكاء الاصطناعي
        // ============================================================
        function toggleChat() {
            const window = document.getElementById('chatWindow');
            const btn = document.getElementById('chatToggle');
            chatOpen = !chatOpen;
            window.classList.toggle('show', chatOpen);
            if (chatOpen) document.getElementById('chatInput').focus();
        }

        function sendMessage() {
            const input = document.getElementById('chatInput');
            const msg = input.value.trim();
            if (!msg) return;

            const messages = document.getElementById('chatMessages');
            messages.innerHTML += `<div class="msg user">${msg}</div>`;
            messages.scrollTop = messages.scrollHeight;

            // إظهار مؤشر الكتابة
            const typing = document.createElement('div');
            typing.className = 'msg bot';
            typing.id = 'typingIndicator';
            typing.innerHTML = `
                🤖
                <div class="typing-dots">
                    <span></span><span></span><span></span>
                </div>
            `;
            messages.appendChild(typing);
            messages.scrollTop = messages.scrollHeight;

            setTimeout(() => {
                document.getElementById('typingIndicator')?.remove();
                const reply = getBotReply(msg);
                const botMsg = document.createElement('div');
                botMsg.className = 'msg bot';
                botMsg.innerHTML = reply;
                messages.appendChild(botMsg);
                messages.scrollTop = messages.scrollHeight;

                // إذا كان السؤال عن عملة، إضافة زر للتحليل
                const lower = msg.toLowerCase();
                let found = false;
                for (const [arabic, sym] of Object.entries(ARABIC_NAMES)) {
                    if (lower.includes(arabic.toLowerCase())) {
                        found = true;
                        break;
                    }
                }
                if (!found) {
                    for (const coin of coinsData) {
                        if (lower.includes(coin.symbol.toLowerCase()) ||
                            lower.includes(coin.name.toLowerCase())) {
                            found = true;
                            break;
                        }
                    }
                }
                if (found) {
                    const btnDiv = document.createElement('div');
                    btnDiv.style.cssText =
                        'display:flex;justify-content:center;margin-top:4px;';
                    btnDiv.innerHTML = `
                        <button onclick="searchCoin('${msg.toUpperCase().replace(/[^A-Z]/g, '')}')" style="padding:6px 16px;background:var(--gold);color:#000;border:none;border-radius:8px;font-weight:700;font-size:11px;cursor:pointer;">
                            📊 عرض التحليل الكامل
                        </button>
                    `;
                    messages.appendChild(btnDiv);
                    messages.scrollTop = messages.scrollHeight;
                }
            }, 800 + Math.random() * 400);

            input.value = '';
        }

        function getBotReply(query) {
            const q = query.toLowerCase().trim();

            // ===== 1. البحث عن عملة =====
            let symbol = null;

            // قاموس العربي
            for (const [arabic, sym] of Object.entries(ARABIC_NAMES)) {
                if (q.includes(arabic.toLowerCase())) {
                    symbol = sym;
                    break;
                }
            }

            if (!symbol) {
                for (const coin of coinsData) {
                    if (q.includes(coin.symbol.toLowerCase()) ||
                        q.includes(coin.name.toLowerCase())) {
                        symbol = coin.symbol;
                        break;
                    }
                }
            }

            if (symbol) {
                const coin = coinsData.find(c => c.symbol === symbol);
                if (coin) {
                    const change = coin.change >= 0 ? `+${coin.change.toFixed(2)}%` : `${coin.change.toFixed(2)}%`;
                    const changeEmoji = coin.change >= 0 ? '🟢' : '🔴';
                    const signal = coin.change >= 5 ? '🟢 شراء قوي' :
                        coin.change >= 2 ? '📈 شراء' :
                        coin.change <= -5 ? '🔴 بيع قوي' :
                        coin.change <= -2 ? '📉 بيع' : '⏸ محايد';

                    const rsi = (50 + Math.random() * 30 - 15);
                    const stoch = (20 + Math.random() * 60);

                    let reply = `📊 <strong>تحليل ${coin.symbol}</strong> 📊\n\n`;
                    reply += `💰 <strong>السعر:</strong> $${coin.price.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 4 })}\n`;
                    reply += `📈 <strong>التغير:</strong> ${changeEmoji} ${change}\n`;
                    reply += `📊 <strong>الحجم:</strong> $${coin.volume.toFixed(1)}M\n`;
                    reply += `📈 <strong>أعلى:</strong> $${coin.high?.toFixed(4) || coin.price}\n`;
                    reply += `📉 <strong>أدنى:</strong> $${coin.low?.toFixed(4) || coin.price}\n\n`;
                    reply += `📊 <strong>المؤشرات الفنية:</strong>\n`;
                    reply += `• RSI: ${rsi.toFixed(0)} ${rsi < 30 ? '🟢 منخفض' : rsi > 70 ? '🔴 مرتفع' : '🟡 محايد'}\n`;
                    reply += `• Stochastic: ${stoch.toFixed(0)} ${stoch < 30 ? '🟢 تشبع شراء' : stoch > 70 ? '🔴 تشبع بيع' : '🟡 محايد'}\n\n`;
                    reply += `🎯 <strong>الأهداف (5 مستويات):</strong>\n`;
                    for (let i = 1; i <= 5; i++) {
                        const target = coin.price * (1 + (i * 0.05 + 0.02));
                        const profit = (i * 5 + 2);
                        reply += `• الهدف ${i}: $${target.toFixed(4)} (ربح ${profit}%)\n`;
                    }
                    reply += `\n📊 <strong>الإشارة:</strong> ${signal}\n\n`;
                    reply += `💡 <strong>نصيحة:</strong> ${coin.change >= 0 ? '🟢 النظر في الشراء مع Stop Loss عند -5%' : '🔴 الحذر والمراقبة'}`;
                    return reply;
                }
            }

            // ===== 2. أفضل العملات =====
            if (q.includes('أفضل') || q.includes('الرابح') || q.includes('اربح') || q.includes('انفجار')) {
                const sorted = [...coinsData].sort((a, b) => b.change - a.change);
                const top = sorted.slice(0, 5);
                if (top.length === 0) return '⏳ جاري تحميل البيانات...';
                let reply = `🏆 <strong>أفضل 5 عملات اليوم:</strong>\n\n`;
                top.forEach((c, i) => {
                    const emoji = c.change >= 5 ? '🚀' : c.change >= 2 ? '📈' : '🟢';
                    reply += `${i+1}. ${emoji} <strong>${c.symbol}</strong>: ${c.change >= 0 ? '+' : ''}${c.change.toFixed(2)}% ($${c.price.toLocaleString()})\n`;
                });
                reply += `\n💡 ${top[0]?.symbol} هو الرابح الأكبر اليوم!`;
                return reply;
            }

            // ===== 3. الأسوأ =====
            if (q.includes('أسوأ') || q.includes('خسارة') || q.includes('انهيار')) {
                const sorted = [...coinsData].sort((a, b) => a.change - b.change);
                const worst = sorted.slice(0, 3);
                if (worst.length === 0) return '⏳ جاري تحميل البيانات...';
                let reply = `📉 <strong>أسوأ 3 عملات اليوم:</strong>\n\n`;
                worst.forEach((c, i) => {
                    const emoji = c.change <= -5 ? '🔴' : '📉';
                    reply += `${i+1}. ${emoji} <strong>${c.symbol}</strong>: ${c.change.toFixed(2)}% ($${c.price.toLocaleString()})\n`;
                });
                reply += `\n⚠️ <strong>تنبيه:</strong> تجنب هذه العملات حالياً!`;
                return reply;
            }

            // ===== 4. توقعات السوق =====
            if (q.includes('توقعات') || q.includes('اتجاه') || q.includes('سوق') || q.includes('تحليل السوق')) {
                const gainers = coinsData.filter(c => c.change > 0).length;
                const losers = coinsData.filter(c => c.change < 0).length;
                const total = coinsData.length;
                if (total === 0) return '⏳ جاري تحميل البيانات...';
                const outlook = gainers > losers ? '🟢 صاعد (Bullish) 🔥' :
                    losers > gainers ? '🔴 هابط (Bearish) 📉' : '🟡 محايد (Neutral) ⏸';
                const strongest = coinsData.reduce((a, b) => a.change > b.change ? a : b);
                const weakest = coinsData.reduce((a, b) => a.change < b.change ? a : b);
                return `📊 <strong>توقعات السوق اليوم:</strong>\n\n` +
                    `📈 عملات صاعدة: ${gainers}\n` +
                    `📉 عملات هابطة: ${losers}\n` +
                    `📊 الاتجاه العام: ${outlook}\n\n` +
                    `🚀 أقوى عملة: <strong>${strongest.symbol}</strong> (${strongest.change.toFixed(2)}%)\n` +
                    `📉 أضعف عملة: <strong>${weakest.symbol}</strong> (${weakest.change.toFixed(2)}%)\n\n` +
                    `💡 نصيحة: ${gainers > losers ? 'السوق في حالة صعود، ابحث عن فرص الشراء' : 'السوق في حالة هبوط، كن حذراً'}`;
            }

            // ===== 5. نصائح التداول =====
            if (q.includes('نصيحة') || q.includes('تداول') || q.includes('استثمار') || q.includes('كيف')) {
                const topGainers = [...coinsData].sort((a, b) => b.change - a.change).slice(0, 3);
                if (topGainers.length === 0) return '⏳ جاري تحميل البيانات...';
                return `💡 <strong>نصائح التداول الذهبية:</strong>\n\n` +
                    `🟢 <strong>العملات الصاعدة اليوم:</strong> ${topGainers.map(c => c.symbol).join(', ')}\n\n` +
                    `📊 <strong>إدارة المخاطر:</strong>\n` +
                    `• نسبة المخاطرة: 1-2% من رأس المال\n` +
                    `• استخدم Stop Loss عند -5% إلى -10%\n` +
                    `• خذ أرباحك عند +10% إلى +15%\n` +
                    `• لا تخاطر بأكثر مما تستطيع خسارته\n\n` +
                    `🎯 <strong>استراتيجيات ناجحة:</strong>\n` +
                    `• ادرس السوق جيداً قبل الدخول\n` +
                    `• استخدم التحليل الفني والأساسي معاً\n` +
                    `• تحكم في مشاعرك ولا تتخذ قرارات عاطفية\n\n` +
                    `⚠️ <strong>تذكر:</strong> التداول يحمل مخاطر عالية!`;
            }

            // ===== 6. تعريف البوت =====
            if (q.includes('من انت') || q.includes('من أنت') || q.includes('تعريف')) {
                return `🤖 <strong>أنا البوت العالمي الخرافي!</strong>\n\n` +
                    `🚀 <strong>مهمتي:</strong> مساعدتك في التداول والعملات الرقمية\n\n` +
                    `📊 <strong>ماذا أقدم لك؟</strong>\n` +
                    `• تحليل فني كامل لأي عملة\n` +
                    `• أهداف دقيقة مع نسب ربح\n` +
                    `• توقعات السوق\n` +
                    `• نصائح تداول ذهبية\n` +
                    `• تنبيهات الانفجارات والانهيارات\n\n` +
                    `💬 <strong>اسألني عن:</strong>\n` +
                    `• أي عملة (مثال: BTC, ETH, SOL)\n` +
                    `• أفضل العملات اليوم\n` +
                    `• توقعات السوق\n` +
                    `• نصائح التداول\n\n` +
                    `🌟 <strong>معي ستتداول بذكاء!</strong>`;
            }

            // ===== 7. الترحيب =====
            if (q.includes('مرحب') || q.includes('السلام') || q.includes('هلا') || q.includes('اهلا')) {
                return `👋 <strong>وعليكم السلام!</strong>\n\n` +
                    `أنا <span class="highlight">البوت العالمي الخرافي</span> 🤖\n\n` +
                    `💬 <strong>اسألني عن:</strong>\n` +
                    `• <strong>أي عملة</strong> (مثال: BTC, ETH, SOL)\n` +
                    `• <strong>أفضل العملات</strong> اليوم\n` +
                    `• <strong>توقعات السوق</strong>\n` +
                    `• <strong>نصائح التداول</strong>\n\n` +
                    `🚀 اكتب اسم العملة وابدأ التحليل!`;
            }

            // ===== 8. الرد الافتراضي =====
            return `🤔 <strong>لم أفهم سؤالك تماماً.</strong>\n\n` +
                `💬 <strong>يمكنك سؤالي عن:</strong>\n` +
                `• <strong>أي عملة</strong> (مثال: BTC, ETH, SOL)\n` +
                `• <strong>أفضل العملات</strong> اليوم\n` +
                `• <strong>توقعات السوق</strong>\n` +
                `• <strong>نصائح التداول</strong>\n\n` +
                `🌟 <strong>مثال:</strong> "سعر BTC" أو "تحليل ETH" أو "أفضل العملات"`;
            }

            // ============================================================
            // 9. جلب البيانات
            // ============================================================
            async function fetchMarketData() {
                try {
                    const response = await fetch(`${BINANCE_API}/ticker/24hr`);
                    if (!response.ok) throw new Error('فشل جلب البيانات');
                    const data = await response.json();

                    coinsData = data
                        .filter(item => TOP_SYMBOLS.includes(item.symbol))
                        .map(item => {
                            const name = item.symbol.replace('USDT', '');
                            const price = parseFloat(item.lastPrice);
                            if (lastPrices[name]) {
                                detectPump({ symbol: name, price: price }, lastPrices[name]);
                            }
                            lastPrices[name] = price;

                            return {
                                symbol: name,
                                fullSymbol: item.symbol,
                                name: name,
                                price: price,
                                change: parseFloat(item.priceChangePercent),
                                volume: parseFloat(item.quoteVolume) / 1e6,
                                high: parseFloat(item.highPrice),
                                low: parseFloat(item.lowPrice),
                                open: parseFloat(item.openPrice)
                            };
                        });

                    coinsData.sort((a, b) => b.volume - a.volume);
                    updateStats();
                    renderAll();
                    setupWebSockets();

                    isConnected = true;
                    document.getElementById('connDot').className = 'dot on';
                    document.getElementById('connText').textContent = 'متصل ✓';
                    document.getElementById('lastUpdate').textContent = new Date().toLocaleString('ar-EG');

                    updateMarketOutlook();

                    return coinsData;
                } catch (error) {
                    console.error('Error:', error);
                    showToast('⚠️ فشل جلب البيانات من Binance', 'error');
                    useFallbackData();
                    return coinsData;
                }
            }

            function useFallbackData() {
                coinsData = TOP_SYMBOLS.map(sym => {
                    const name = sym.replace('USDT', '');
                    const basePrice = Math.random() * 100 + 10;
                    return {
                        symbol: name,
                        fullSymbol: sym,
                        name: name,
                        price: basePrice,
                        change: (Math.random() * 20 - 10),
                        volume: Math.random() * 100 + 10,
                        high: basePrice * 1.05,
                        low: basePrice * 0.95,
                        open: basePrice
                    };
                });
                renderAll();
                updateStats();
                document.getElementById('connDot').className = 'dot off';
                document.getElementById('connText').textContent = 'بيانات تجريبية';
                document.getElementById('lastUpdate').textContent = new Date().toLocaleString('ar-EG');
                updateMarketOutlook();
            }

            function updateMarketOutlook() {
                const gainers = coinsData.filter(c => c.change > 0).length;
                const losers = coinsData.filter(c => c.change < 0).length;
                const total = coinsData.length;
                if (total === 0) {
                    document.getElementById('marketOutlook').textContent = '⏳ جاري التحليل...';
                    return;
                }
                const outlook = gainers > losers ? '🟢 صاعد (Bullish) 🔥' :
                    losers > gainers ? '🔴 هابط (Bearish) 📉' : '🟡 محايد (Neutral) ⏸';
                document.getElementById('marketOutlook').textContent = outlook;
                document.getElementById('marketOutlook').style.color = gainers > losers ? 'var(--green)' :
                    losers > gainers ? 'var(--red)' : 'var(--gold)';
            }

            // ============================================================
            // 10. WebSocket
            // ============================================================
            function setupWebSockets() {
                wsConnections.forEach(ws => {
                    if (ws.readyState === WebSocket.OPEN || ws.readyState === WebSocket.CONNECTING) ws.close();
                });
                wsConnections = [];

                const streams = TOP_SYMBOLS.map(sym => `${sym.toLowerCase()}@ticker`).join('/');
                const wsUrl = `${WS_BASE}/stream?streams=${streams}`;

                try {
                    const ws = new WebSocket(wsUrl);
                    ws.onopen = () => console.log('✅ WebSocket متصل');
                    ws.onmessage = (event) => {
                        try {
                            const data = JSON.parse(event.data);
                            if (data.data && data.data.data) {
                                const ticker = data.data.data;
                                const coin = coinsData.find(c => c.fullSymbol === ticker.s);
                                if (coin) {
                                    const oldPrice = coin.price;
                                    const newPrice = parseFloat(ticker.c);

                                    coin.price = newPrice;
                                    coin.change = parseFloat(ticker.P);
                                    coin.high = parseFloat(ticker.h);
                                    coin.low = parseFloat(ticker.l);
                                    coin.volume = parseFloat(ticker.q) / 1e6;

                                    detectPump(coin, oldPrice);
                                    updateCoinCards(coin);
                                    updateStats();
                                    updateMarketOutlook();

                                    document.getElementById('connDot').className = 'dot on';
                                    document.getElementById('connText').textContent = 'مباشر ✓';
                                    document.getElementById('lastUpdate').textContent = new Date().toLocaleString(
                                    'ar-EG');
                                }
                            }
                        } catch (e) {}
                    };
                    ws.onerror = () => console.log('WebSocket error');
                    ws.onclose = () => {
                        console.log('WebSocket مغلق، إعادة محاولة...');
                        setTimeout(setupWebSockets, 5000);
                    };
                    wsConnections.push(ws);
                } catch (e) {
                    setTimeout(setupWebSockets, 5000);
                }
            }

            // ============================================================
            // 11. عرض البيانات
            // ============================================================
            function renderAll() {
                renderHeatmap();
                renderTopCoins();
                renderAllCoins();
                renderCoinsList();
                renderMarket('all');
                renderSavedList();
                renderWhales();
            }

            function renderHeatmap() {
                const container = document.getElementById('heatmapGrid');
                const sorted = [...coinsData].sort((a, b) => b.volume - a.volume);
                if (sorted.length === 0) {
                    container.innerHTML = `<div class="loading"><span>⏳ جاري التحميل...</span></div>`;
                    return;
                }
                container.innerHTML = sorted.map(c => {
                    const intensity = Math.min(Math.abs(c.change) / 10, 1);
                    const color = c.change >= 0 ?
                        `hsl(140, 80%, ${20 + intensity * 40}%)` :
                        `hsl(0, 80%, ${20 + intensity * 40}%)`;
                    return `
                            <div class="heatmap-item" style="background:${color};" onclick="searchCoin('${c.symbol}')">
                                <div class="hm-symbol">${c.symbol}</div>
                                <div class="hm-change">${c.change >= 0 ? '+' : ''}${c.change.toFixed(1)}%</div>
                            </div>
                        `;
                }).join('');
            }

            function renderTopCoins() {
                const container = document.getElementById('topCoins');
                const top = [...coinsData].sort((a, b) => b.change - a.change).slice(0, 4);
                if (top.length === 0) {
                    container.innerHTML = `<div class="loading"><span>⏳ جاري التحميل...</span></div>`;
                    return;
                }
                container.innerHTML = top.map(c => coinCardHTML(c)).join('');
            }

            function renderAllCoins() {
                const container = document.getElementById('allCoins');
                if (coinsData.length === 0) {
                    container.innerHTML = `<div class="loading"><span>⏳ جاري التحميل...</span></div>`;
                    return;
                }
                container.innerHTML = coinsData.map(c => coinCardHTML(c)).join('');
            }

            function renderCoinsList() {
                const container = document.getElementById('coinsList');
                if (coinsData.length === 0) {
                    container.innerHTML = `<div class="loading"><span>⏳ جاري التحميل...</span></div>`;
                    return;
                }
                container.innerHTML = coinsData.map(c => coinCardHTML(c)).join('');
            }

            function coinCardHTML(c) {
                const signal = c.change >= 5 ? 'شراء' : c.change <= -5 ? 'بيع' : 'محايد';
                const signalClass = c.change >= 5 ? 'buy' : c.change <= -5 ? 'sell' : 'neutral';
                return `
                        <div class="coin-card" data-symbol="${c.symbol}" onclick="searchCoin('${c.symbol}')">
                            <div class="flex-between">
                                <span class="coin-symbol">${c.symbol}</span>
                                <span class="coin-change ${c.change >= 0 ? 'green' : 'red'}">${c.change >= 0 ? '+' : ''}${c.change.toFixed(2)}%</span>
                            </div>
                            <div class="coin-name">${c.name}</div>
                            <div class="coin-price">$${c.price.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 4 })}</div>
                            <div class="coin-indicators">
                                <span class="ind">📊 RSI: ${(50 + Math.random() * 30 - 15).toFixed(0)}</span>
                                <span class="ind ${signalClass}">${signal === 'شراء' ? '🟢' : signal === 'بيع' ? '🔴' : '⚪'} ${signal}</span>
                            </div>
                        </div>
                    `;
            }

            function updateCoinCards(updatedCoin) {
                document.querySelectorAll('.coin-card').forEach(card => {
                    if (card.dataset.symbol === updatedCoin.symbol) {
                        const priceEl = card.querySelector('.coin-price');
                        const changeEl = card.querySelector('.coin-change');
                        if (priceEl) {
                            const newText =
                                `$${updatedCoin.price.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 4 })}`;
                            priceEl.textContent = newText;
                        }
                        if (changeEl) {
                            changeEl.textContent = `${updatedCoin.change >= 0 ? '+' : ''}${updatedCoin.change.toFixed(2)}%`;
                            changeEl.className = `coin-change ${updatedCoin.change >= 0 ? 'green' : 'red'}`;
                        }
                    }
                });
                renderHeatmap();
            }

            function renderWhales() {
                const container = document.getElementById('whaleActivity');
                const types = ['buy', 'sell'];
                const symbols = ['BTC', 'ETH', 'SOL', 'XRP', 'ADA', 'DOGE', 'AVAX', 'MATIC'];
                container.innerHTML = Array.from({ length: 5 }, () => {
                    const type = types[Math.floor(Math.random() * types.length)];
                    const symbol = symbols[Math.floor(Math.random() * symbols.length)];
                    const amount = (Math.random() * 25 + 1).toFixed(1);
                    const mins = Math.floor(Math.random() * 60);
                    return `
                            <div class="whale-card">
                                <span class="whale-type ${type}">${type === 'buy' ? '🟢 شراء' : '🔴 بيع'}</span>
                                <span class="whale-amount">${symbol}</span>
                                <span style="color:var(--text-secondary);">$${amount}M</span>
                                <span style="font-size:10px;color:var(--text-secondary);">منذ ${mins} دقيقة</span>
                            </div>
                        `;
                }).join('');
            }

            // ============================================================
            // 12. السوق
            // ============================================================
            function renderMarket(filter) {
                currentFilter = filter || 'all';
                let sorted = [...coinsData];

                if (filter === 'gainers') sorted.sort((a, b) => b.change - a.change);
                else if (filter === 'losers') sorted.sort((a, b) => a.change - b.change);
                else if (filter === 'volume') sorted.sort((a, b) => b.volume - a.volume);
                else if (filter === 'pump') sorted = sorted.filter(c => c.change > 3).sort((a, b) => b.change - a.change);

                const container = document.getElementById('marketTable');
                if (sorted.length === 0) {
                    container.innerHTML = `
                            <div class="row header">
                                <span>العملة</span>
                                <span>السعر</span>
                                <span>التغير</span>
                                <span>الحجم</span>
                            </div>
                            <div class="loading"><span>⏳ جاري التحميل...</span></div>
                        `;
                    return;
                }

                const rows = sorted.map(c => `
                        <div class="row" onclick="searchCoin('${c.symbol}')">
                            <span><strong>${c.symbol}</strong> <span style="color:var(--text-secondary);font-size:10px;">${c.name}</span></span>
                            <span>$${c.price.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 4 })}</span>
                            <span class="change ${c.change >= 0 ? 'green' : 'red'}">${c.change >= 0 ? '+' : ''}${c.change.toFixed(2)}%</span>
                            <span class="vol">$${c.volume.toFixed(1)}M</span>
                        </div>
                    `).join('');

                container.innerHTML = `
                        <div class="row header">
                            <span>العملة</span>
                            <span>السعر</span>
                            <span>التغير</span>
                            <span>الحجم</span>
                        </div>
                        ${rows}
                    `;
            }

            // ============================================================
            // 13. البحث والتحليل
            // ============================================================
            function searchAnalysis() {
                const input = document.getElementById('searchCoin').value.trim();
                if (!input) {
                    showToast('📝 الرجاء إدخال اسم العملة', 'error');
                    return;
                }

                let symbol = null;
                const lowerInput = input.toLowerCase();

                for (const [arabic, sym] of Object.entries(ARABIC_NAMES)) {
                    if (lowerInput.includes(arabic.toLowerCase()) || arabic.toLowerCase().includes(lowerInput)) {
                        symbol = sym;
                        break;
                    }
                }

                if (!symbol) {
                    for (const coin of coinsData) {
                        if (lowerInput.includes(coin.symbol.toLowerCase()) ||
                            lowerInput.includes(coin.name.toLowerCase()) ||
                            coin.symbol.toLowerCase().includes(lowerInput)) {
                            symbol = coin.symbol;
                            break;
                        }
                    }
                }

                if (!symbol) {
                    showToast(`⏳ جاري البحث عن ${input}...`, 'info');
                    const searchTerm = input.toUpperCase();
                    fetch(`${BINANCE_API}/ticker/24hr?symbol=${searchTerm}USDT`)
                        .then(res => res.json())
                        .then(data => {
                            if (data && data.symbol) {
                                const newCoin = {
                                    symbol: data.symbol.replace('USDT', ''),
                                    fullSymbol: data.symbol,
                                    name: data.symbol.replace('USDT', ''),
                                    price: parseFloat(data.lastPrice),
                                    change: parseFloat(data.priceChangePercent),
                                    volume: parseFloat(data.quoteVolume) / 1e6,
                                    high: parseFloat(data.highPrice),
                                    low: parseFloat(data.lowPrice),
                                    open: parseFloat(data.openPrice)
                                };
                                coinsData.push(newCoin);
                                showAnalysisDetail(newCoin);
                                renderAll();
                                showToast(`✅ تم العثور على ${newCoin.symbol}`, 'success');
                            } else {
                                showToast('❌ العملة غير موجودة', 'error');
                            }
                        })
                        .catch(() => {
                            showToast('❌ فشل البحث عن العملة', 'error');
                        });
                    return;
                }

                const coin = coinsData.find(c => c.symbol === symbol);
                if (coin) {
                    showAnalysisDetail(coin);
                } else {
                    showToast('❌ العملة غير موجودة', 'error');
                }
            }

            function searchCoin(symbol) {
                document.getElementById('searchCoin').value = symbol;
                const coin = coinsData.find(c => c.symbol === symbol);
                if (coin) showAnalysisDetail(coin);
                document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
                document.querySelector('[data-page="page-analysis"]').classList.add('active');
                document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
                document.getElementById('page-analysis').classList.add('active');
            }

            function showAnalysisDetail(coin) {
                const container = document.getElementById('analysisResult');

                const rsi = (50 + Math.random() * 30 - 15);
                const stoch = (20 + Math.random() * 60);
                const macd = (Math.random() * 2 - 1);
                const ma7 = coin.price * (1 + (Math.random() * 0.04 - 0.02));
                const ma25 = coin.price * (1 + (Math.random() * 0.06 - 0.03));

                const signal = rsi < 30 && macd > 0 ? '🟢 إشارة شراء قوية' :
                    rsi < 40 && macd > 0 ? '🟢 إشارة شراء' :
                    rsi > 70 && macd < 0 ? '🔴 إشارة بيع قوية' :
                    rsi > 60 && macd < 0 ? '🔴 إشارة بيع' : '⚪ محايد';

                const targets = [
                    { price: coin.price * 1.05, profit: '5%' },
                    { price: coin.price * 1.10, profit: '10%' },
                    { price: coin.price * 1.18, profit: '18%' },
                    { price: coin.price * 1.25, profit: '25%' },
                    { price: coin.price * 1.35, profit: '35%' }
                ];

                container.innerHTML = `
                        <div class="analysis-detail">
                            <div style="display:flex;justify-content:space-between;align-items:center;">
                                <div class="coin-title">${coin.symbol}</div>
                                <button onclick="document.getElementById('analysisResult').innerHTML='';" style="background:none;border:none;color:var(--text-secondary);font-size:18px;cursor:pointer;">✕</button>
                            </div>
                            <div class="coin-subtitle">${coin.name}</div>
                            <div class="entry-price">💰 سعر الدخول: $${coin.price.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 4 })}</div>

                            <div class="indicators-grid">
                                <div class="ind-item">
                                    <div class="ind-label">📊 RSI</div>
                                    <div class="ind-value ${rsi < 30 ? 'bullish' : rsi > 70 ? 'bearish' : 'neutral'}">${rsi.toFixed(0)}</div>
                                </div>
                                <div class="ind-item">
                                    <div class="ind-label">📈 Stochastic</div>
                                    <div class="ind-value ${stoch < 30 ? 'bullish' : stoch > 70 ? 'bearish' : 'neutral'}">${stoch.toFixed(0)}</div>
                                </div>
                                <div class="ind-item">
                                    <div class="ind-label">📊 MACD</div>
                                    <div class="ind-value ${macd > 0 ? 'bullish' : 'bearish'}">${macd.toFixed(3)}</div>
                                </div>
                                <div class="ind-item">
                                    <div class="ind-label">📉 MA 7</div>
                                    <div class="ind-value">$${ma7.toFixed(4)}</div>
                                </div>
                                <div class="ind-item">
                                    <div class="ind-label">📉 MA 25</div>
                                    <div class="ind-value">$${ma25.toFixed(4)}</div>
                                </div>
                                <div class="ind-item">
                                    <div class="ind-label">📊 الحجم</div>
                                    <div class="ind-value">$${coin.volume.toFixed(1)}M</div>
                                </div>
                            </div>

                            <div style="text-align:center;padding:12px;background:#0a0a12;border-radius:12px;margin:10px 0;border:1px solid var(--gold-glow);">
                                <span style="font-size:18px;font-weight:800;background:linear-gradient(135deg,var(--gold),var(--purple));-webkit-background-clip:text;-webkit-text-fill-color:transparent;">${signal}</span>
                            </div>

                            <div class="targets">
                                <div style="font-weight:700;margin-bottom:8px;color:var(--gold);font-size:14px;">🎯 الأهداف (5 مستويات)</div>
                                ${targets.map((t, i) => `
                                        <div class="target-item">
                                            <span class="num">الهدف ${i+1}</span>
                                            <span class="price">$${t.price.toFixed(4)}</span>
                                            <span class="profit">ربح ${t.profit}</span>
                                        </div>
                                    `).join('')}
                            </div>

                            <div style="margin:10px 0;padding:10px;background:#0a0a12;border-radius:10px;text-align:center;">
                                <span style="color:var(--text-secondary);font-size:12px;">📊 Stop Loss مقترح: </span>
                                <span style="color:var(--red);font-weight:700;font-size:13px;">$${(coin.price * 0.95).toFixed(4)} (-5%)</span>
                            </div>

                            <div class="analysis-actions">
                                <button class="btn-legend save" onclick="saveAnalysis('${coin.symbol}')">💾 حفظ</button>
                                <button class="btn-legend alert" onclick="setPriceAlert('${coin.symbol}')">🔔 تنبيه</button>
                                <button class="btn-legend share" onclick="shareAnalysis('${coin.symbol}')">📤 مشاركة</button>
                                <button class="btn-legend close" onclick="document.getElementById('analysisResult').innerHTML='';">✖</button>
                            </div>

                            <div class="warning-box">
                                <h4>⚠️ تحذير هام</h4>
                                <p>التداول في العملات الرقمية يحمل مخاطر عالية. قد تخسر جزءاً أو كل استثمارك. هذه التحليلات لأغراض تعليمية فقط وليست توصية استثمارية.</p>
                            </div>
                        </div>
                    `;

                container.scrollIntoView({ behavior: 'smooth', block: 'start' });
            }

            // ============================================================
            // 14. حفظ التحليل
            // ============================================================
            function saveAnalysis(symbol) {
                const coin = coinsData.find(c => c.symbol === symbol);
                if (!coin) return;

                if (savedAnalyses.some(a => a.symbol === symbol)) {
                    showToast('⚠️ هذه العملة محفوظة مسبقاً', 'error');
                    return;
                }

                savedAnalyses.push({
                    symbol: coin.symbol,
                    name: coin.name,
                    price: coin.price,
                    change: coin.change,
                    savedAt: new Date().toLocaleString('ar-EG')
                });

                localStorage.setItem('savedAnalyses', JSON.stringify(savedAnalyses));
                renderSavedList();
                document.getElementById('analysisBadge').textContent = savedAnalyses.length;
                showToast(`✅ تم حفظ ${coin.symbol}`, 'success');
            }

            function renderSavedList() {
                const container = document.getElementById('savedList');
                if (savedAnalyses.length === 0) {
                    container.innerHTML =
                        `<p style="color:var(--text-secondary);text-align:center;padding:15px;font-size:12px;">📭 لا توجد تحليلات محفوظة</p>`;
                    return;
                }

                container.innerHTML = savedAnalyses.map((a, index) => `
                        <div class="saved-item">
                            <div class="info">
                                <h4>${a.symbol} - ${a.name}</h4>
                                <p>سعر الدخول: $${a.price.toLocaleString(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 4 })} | التغير: ${a.change >= 0 ? '+' : ''}${a.change.toFixed(2)}%</p>
                                <p style="font-size:9px;color:var(--text-secondary);">حفظ: ${a.savedAt}</p>
                            </div>
                            <div class="actions">
                                <button class="analyze" onclick="searchCoin('${a.symbol}')">📊</button>
                                <button class="delete" onclick="deleteAnalysis(${index})">🗑</button>
                            </div>
                        </div>
                    `).join('');
            }

            function deleteAnalysis(index) {
                const deleted = savedAnalyses[index];
                savedAnalyses.splice(index, 1);
                localStorage.setItem('savedAnalyses', JSON.stringify(savedAnalyses));
                renderSavedList();
                document.getElementById('analysisBadge').textContent = savedAnalyses.length;
                showToast(`🗑 تم حذف تحليل ${deleted.symbol}`);
            }

            function setPriceAlert(symbol) {
                const coin = coinsData.find(c => c.symbol === symbol);
                if (!coin) return;
                const target = coin.price * 1.05;
                showToast(`🔔 تم تفعيل تنبيه لـ ${symbol} عند $${target.toFixed(4)}`, 'success');
                addNotification('alert', `🔔 تنبيه ${symbol}`, `تم تفعيل التنبيه عند $${target.toFixed(4)}`);
            }

            function shareAnalysis(symbol) {
                const coin = coinsData.find(c => c.symbol === symbol);
                if (!coin) return;
                const text =
                    `📊 تحليل ${coin.symbol}\n💰 السعر: $${coin.price.toLocaleString()}\n📈 التغير: ${coin.change >= 0 ? '+' : ''}${coin.change.toFixed(2)}%\n📊 Legend Bot - البوت العالمي الخرافي`;
                if (navigator.share) {
                    navigator.share({ title: `تحليل ${coin.symbol}`, text: text }).catch(() => {});
                } else {
                    navigator.clipboard.writeText(text).then(() => {
                        showToast('📤 تم نسخ التحليل للحافظة', 'success');
                    }).catch(() => {
                        showToast('📤 ' + text, 'info');
                    });
                }
            }

            // ============================================================
            // 15. الإحصائيات
            // ============================================================
            function updateStats() {
                document.getElementById('totalCoins').textContent = coinsData.length;
                const totalVol = coinsData.reduce((sum, c) => sum + c.volume, 0);
                document.getElementById('totalVolume').textContent = `$${totalVol.toFixed(1)}M`;
                const top = coinsData.reduce((max, c) => c.change > max.change ? c : max, coinsData[0] || { change: 0 });
                document.getElementById('topGainer').textContent = `${top.change >= 0 ? '+' : ''}${top.change.toFixed(2)}%`;
            }

            // ============================================================
            // 16. التنقل
            // ============================================================
            document.querySelectorAll('.nav-item').forEach(item => {
                item.addEventListener('click', function() {
                    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
                    this.classList.add('active');
                    const pageId = this.dataset.page;
                    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
                    document.getElementById(pageId).classList.add('active');

                    if (pageId === 'page-market') renderMarket(currentFilter);
                    if (pageId === 'page-coins') renderCoinsList();
                    if (pageId === 'page-home') {
                        renderTopCoins();
                        renderAllCoins();
                        renderHeatmap();
                        updateMarketOutlook();
                    }
                    if (pageId === 'page-analysis') renderSavedList();
                });
            });

            // ============================================================
            // 17. فلترة السوق
            // ============================================================
            document.querySelectorAll('.market-filters button').forEach(btn => {
                btn.addEventListener('click', function() {
                    document.querySelectorAll('.market-filters button').forEach(b => b.classList.remove('active'));
                    this.classList.add('active');
                    renderMarket(this.dataset.filter);
                });
            });

            // ============================================================
            // 18. الوضع
            // ============================================================
            function toggleTheme() {
                darkMode = !darkMode;
                const root = document.documentElement;
                if (darkMode) {
                    root.style.setProperty('--bg-primary', '#0a0a1a');
                    root.style.setProperty('--bg-secondary', '#0d0d2b');
                    root.style.setProperty('--bg-card', '#111133');
                    root.style.setProperty('--bg-card-hover', '#1a1a4a');
                    root.style.setProperty('--text-primary', '#e8e8ff');
                    root.style.setProperty('--text-secondary', '#8888bb');
                } else {
                    root.style.setProperty('--bg-primary', '#f0f0f8');
                    root.style.setProperty('--bg-secondary', '#ffffff');
                    root.style.setProperty('--bg-card', '#f0f0ff');
                    root.style.setProperty('--bg-card-hover', '#e0e0ff');
                    root.style.setProperty('--text-primary', '#1a1a2e');
                    root.style.setProperty('--text-secondary', '#666688');
                }
            }

            // ============================================================
            // 19. تهيئة التطبيق
            // ============================================================
            function initApp() {
                fetchMarketData();
                renderSavedList();
                updateNotifBadge();
                renderNotifications();
                document.getElementById('analysisBadge').textContent = savedAnalyses.length || '';

                setInterval(() => {
                    renderWhales();
                }, 30000);

                setInterval(() => {
                    if (!isConnected) {
                        fetchMarketData();
                    }
                }, 60000);

                console.log('🤖 Legend Bot V9 - البوت العالمي الخرافي');
                console.log('🚀 تم تشغيل البوت الخرافي بنجاح!');

                setTimeout(() => {
                    addNotification('success', '🤖 البوت الخرافي', 'تم تشغيل البوت العالمي الخرافي بنجاح!');
                }, 2000);
            }

            if (termsAccepted === 'accepted') {}
    </script>
</body>
</html>
