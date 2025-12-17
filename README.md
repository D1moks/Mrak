
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Отряд  - Хэллоуи</title>
    <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🎄</text></svg>">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --black: #000000;
            --dark: #0a0a0a;
            --gray: #1a1a1a;
            --light-gray: #2a2a2a;
            --white: #ffffff;
            --light: #f0f0f0;
            --accent: #6a0dad;
            --gold: #9370db;
            --success: #00ff00;
            --blood-red: #4b0082;
            --dark-purple: #191970;
            --deep-blue: #000080;
            --halloween-orange: #18ff8c;
            --halloween-purple: #8a2be2;
            --pumpkin: #ff8c00;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        /* Кастомный скроллбар */
        ::-webkit-scrollbar {
            width: 8px;
        }

        ::-webkit-scrollbar-track {
            background: rgba(10, 10, 10, 0.8);
        }

        ::-webkit-scrollbar-thumb {
            background: linear-gradient(45deg, #4b0082, #6a0dad);
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: linear-gradient(45deg, #6a0dad, #9370db);
        }

        /* WebGL Canvas */
        #webgl-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            display: block;
        }

        /* ФОН С ВАШИМ ИЗОБРАЖЕНИЕМ */
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: url('3db32463-2150-4c18-b1d1-7b64cf57a1d0.png') no-repeat center center fixed;
            background-size: cover;
            color: var(--white);
            min-height: 100vh;
            line-height: 1.6;
            position: relative;
            overflow-x: hidden;
        }

        /* Затемнение фона для лучшей читаемости */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            z-index: -1;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 1;
        }

        /* НОВАЯ НАВИГАЦИЯ - Боковая панель */
        .dark-sidebar {
            position: fixed;
            left: 0;
            top: 0;
            width: 80px;
            height: 100vh;
            background: rgba(10, 10, 10, 0.95);
            backdrop-filter: blur(20px);
            border-right: 1px solid rgba(106, 13, 173, 0.3);
            z-index: 1000;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px 0;
        }

        .dark-sidebar:hover {
            width: 250px;
            box-shadow: 10px 0 30px rgba(106, 13, 173, 0.3);
        }

        .sidebar-logo {
            width: 50px;
            height: 50px;
            background: linear-gradient(45deg, #4b0082, #6a0dad);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5em;
            margin-bottom: 40px;
            border: 2px solid rgba(147, 112, 219, 0.5);
            position: relative;
            overflow: hidden;
            transition: all 0.3s ease;
        }

        .sidebar-logo::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.2) 0%, rgba(255,255,255,0) 70%);
            transform: rotate(30deg);
            animation: shine 6s infinite linear;
        }

        .sidebar-nav {
            display: flex;
            flex-direction: column;
            gap: 15px;
            width: 100%;
            padding: 0 15px;
        }

        .nav-item {
            display: flex;
            align-items: center;
            gap: 15px;
            padding: 15px;
            border-radius: 12px;
            color: var(--light);
            text-decoration: none;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            white-space: nowrap;
            border: 1px solid transparent;
            cursor: pointer;
        }

        .nav-item::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(147, 112, 219, 0.2), transparent);
            transition: left 0.6s ease;
        }

        .nav-item:hover::before {
            left: 100%;
        }

        .nav-item:hover {
            background: rgba(106, 13, 173, 0.2);
            border-color: rgba(147, 112, 219, 0.4);
            transform: translateX(5px);
        }

        .nav-item.active {
            background: rgba(106, 13, 173, 0.3);
            border-color: rgba(147, 112, 219, 0.6);
            box-shadow: 0 5px 15px rgba(106, 13, 173, 0.3);
        }

        .nav-icon {
            width: 24px;
            height: 24px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2em;
            transition: all 0.3s ease;
        }

        .nav-text {
            opacity: 0;
            transform: translateX(-10px);
            transition: all 0.3s ease;
            font-weight: 500;
        }

        .dark-sidebar:hover .nav-text {
            opacity: 1;
            transform: translateX(0);
        }

        /* Главный контент с отступом под боковую панель */
        .main-content {
            margin-left: 80px;
            transition: margin-left 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            min-height: 100vh;
        }

        .dark-sidebar:hover ~ .main-content {
            margin-left: 250px;
        }

        /* Секции */
        .section {
            display: none;
            animation: fadeInUp 0.8s ease-out;
        }
        
        .section.active {
            display: block;
        }
        
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes shine {
            0% { transform: translateX(-100%) translateY(-100%) rotate(30deg); }
            100% { transform: translateX(100%) translateY(100%) rotate(30deg); }
        }

        /* Герой секция */
        .hero {
            text-align: center;
            padding: 100px 0 80px;
            position: relative;
        }
        
        .hero h1 {
            font-size: 4em;
            margin-bottom: 20px;
            background: linear-gradient(45deg, #9370db, #6a0dad, #4b0082);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 0 30px rgba(106, 13, 173, 0.3);
            position: relative;
            display: inline-block;
        }
        
        .hero h1::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 0;
            width: 100%;
            height: 3px;
            background: linear-gradient(90deg, transparent, #9370db, transparent);
            border-radius: 50%;
        }
        
        .hero p {
            font-size: 1.3em;
            color: var(--light);
            max-width: 700px;
            margin: 0 auto 40px;
            position: relative;
            padding: 20px;
            border-radius: 10px;
            background: rgba(106, 13, 173, 0.05);
            border: 1px solid rgba(106, 13, 173, 0.1);
        }

        /* Символ Мрака */
        .symbol-section {
            text-align: center;
            padding: 60px 0;
            margin: 40px 0;
        }
        
        .symbol-container {
            background: rgba(106, 13, 173, 0.1);
            border-radius: 20px;
            padding: 50px;
            backdrop-filter: blur(15px);
            border: 1px solid rgba(106, 13, 173, 0.3);
            max-width: 600px;
            margin: 0 auto;
            position: relative;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            transition: all 0.4s ease;
        }
        
        .symbol-container:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(75, 0, 130, 0.4);
        }
        
        .symbol-container::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(147, 112, 219, 0.1), transparent);
            transition: left 0.7s ease;
        }
        
        .symbol-container:hover::before {
            left: 100%;
        }
        
        .symbol-icon {
            font-size: 5em;
            margin-bottom: 20px;
            background: linear-gradient(45deg, #4b0082, #6a0dad, #000080);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: symbolPulse 4s infinite;
            filter: drop-shadow(0 0 10px rgba(106, 13, 173, 0.5));
        }
        
        @keyframes symbolPulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }
        
        .symbol-title {
            font-size: 2em;
            margin-bottom: 15px;
            background: linear-gradient(45deg, #9370db, #6a0dad);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .symbol-description {
            color: var(--light);
            line-height: 1.7;
            font-size: 1.1em;
        }

        /* Сетка функций */
        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 30px;
            margin: 80px 0;
        }
        
        .feature-card {
            background: rgba(106, 13, 173, 0.1);
            border-radius: 20px;
            padding: 40px 30px;
            backdrop-filter: blur(15px);
            border: 1px solid rgba(106, 13, 173, 0.3);
            transition: all 0.4s ease;
            text-align: center;
            position: relative;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        .feature-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(147, 112, 219, 0.1), transparent);
            transition: left 0.7s ease;
        }
        
        .feature-card:hover::before {
            left: 100%;
        }
        
        .feature-card:hover {
            transform: translateY(-15px);
            background: rgba(106, 13, 173, 0.15);
            border-color: rgba(147, 112, 219, 0.5);
            box-shadow: 0 20px 40px rgba(75, 0, 130, 0.4);
        }
        
        .feature-icon {
            width: 80px;
            height: 80px;
            background: linear-gradient(45deg, #4b0082, #6a0dad, #000080);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 25px;
            font-size: 2em;
            animation: pulse 3s infinite;
            border: 2px solid #9370db;
            position: relative;
            overflow: hidden;
        }
        
        .feature-icon::after {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.3) 0%, rgba(255,255,255,0) 70%);
            transform: rotate(30deg);
            animation: shine 5s infinite linear;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); box-shadow: 0 0 0 0 rgba(147, 112, 219, 0.3); }
            70% { transform: scale(1.05); box-shadow: 0 0 0 10px rgba(147, 112, 219, 0); }
            100% { transform: scale(1); box-shadow: 0 0 0 0 rgba(147, 112, 219, 0); }
        }
        
        .feature-card h3 {
            font-size: 1.8em;
            margin-bottom: 15px;
            background: linear-gradient(45deg, #9370db, #6a0dad);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .feature-card p {
            color: var(--light);
            margin-bottom: 25px;
            line-height: 1.7;
        }
        
        .feature-button {
            display: inline-block;
            padding: 12px 30px;
            background: rgba(106, 13, 173, 0.2);
            color: var(--white);
            text-decoration: none;
            border-radius: 25px;
            border: 1px solid rgba(147, 112, 219, 0.5);
            font-weight: 600;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
            cursor: pointer;
        }
        
        .feature-button::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(147, 112, 219, 0.2), transparent);
            transition: left 0.5s ease;
        }
        
        .feature-button:hover::before {
            left: 100%;
        }
        
        .feature-button:hover {
            background: rgba(106, 13, 173, 0.3);
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(75, 0, 130, 0.3);
        }
        
        /* Заголовки секций */
        .section-title {
            font-size: 2.5em;
            margin-bottom: 50px;
            text-align: center;
            background: linear-gradient(45deg, #9370db, #6a0dad);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            position: relative;
            display: inline-block;
            left: 50%;
            transform: translateX(-50%);
        }
        
        .section-title::after {
            content: '';
            position: absolute;
            bottom: -15px;
            left: 0;
            width: 100%;
            height: 3px;
            background: linear-gradient(90deg, transparent, #9370db, transparent);
            border-radius: 50%;
        }
        
        /* Сетка команды */
        .members-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin: 40px 0;
        }
        
        .member-card {
            background: rgba(106, 13, 173, 0.1);
            border-radius: 20px;
            padding: 30px 25px;
            backdrop-filter: blur(15px);
            border: 1px solid rgba(106, 13, 173, 0.3);
            transition: all 0.4s ease;
            text-align: center;
            position: relative;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        .member-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(147, 112, 219, 0.1), transparent);
            transition: left 0.7s ease;
        }
        
        .member-card:hover::before {
            left: 100%;
        }
        
        .member-card:hover {
            transform: translateY(-10px);
            background: rgba(106, 13, 173, 0.15);
            border-color: rgba(147, 112, 219, 0.5);
            box-shadow: 0 20px 40px rgba(75, 0, 130, 0.4);
        }
        
        .member-avatar {
            width: 80px;
            height: 80px;
            background: linear-gradient(45deg, #4b0082, #6a0dad, #000080);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 20px;
            font-size: 2em;
            border: 2px solid #9370db;
            animation: pulse 3s infinite;
            position: relative;
            overflow: hidden;
        }
        
        .member-avatar::after {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.3) 0%, rgba(255,255,255,0) 70%);
            transform: rotate(30deg);
            animation: shine 5s infinite linear;
        }
        
        .member-rank {
            color: #9370db;
            font-weight: 600;
            margin-bottom: 8px;
            font-size: 1.1em;
        }
        
        .member-name {
            font-size: 1.4em;
            margin-bottom: 10px;
            background: linear-gradient(45deg, #9370db, #6a0dad);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .member-role {
            color: var(--light);
            font-size: 0.95em;
            line-height: 1.4;
        }
        
        .member-card.vacant {
            background: rgba(106, 13, 173, 0.05);
            border: 2px dashed rgba(147, 112, 219, 0.3);
        }
        
        .member-card.vacant .member-avatar {
            background: linear-gradient(45deg, #191970, #4b0082);
            border-color: rgba(147, 112, 219, 0.2);
        }
        
        .member-card.vacant .member-name {
            color: var(--accent);
            -webkit-text-fill-color: var(--accent);
            background: none;
        }

        /* Правила */
        .rules-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 30px;
            margin: 60px 0;
        }
        
        .rule-card {
            background: rgba(106, 13, 173, 0.1);
            border-radius: 20px;
            padding: 35px 30px;
            backdrop-filter: blur(15px);
            border: 1px solid rgba(106, 13, 173, 0.3);
            transition: all 0.4s ease;
            position: relative;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        .rule-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(147, 112, 219, 0.1), transparent);
            transition: left 0.7s ease;
        }
        
        .rule-card:hover::before {
            left: 100%;
        }
        
        .rule-card:hover {
            transform: translateY(-10px);
            background: rgba(106, 13, 173, 0.15);
            border-color: rgba(147, 112, 219, 0.5);
            box-shadow: 0 20px 40px rgba(75, 0, 130, 0.4);
        }
        
        .rule-icon {
            width: 70px;
            height: 70px;
            background: linear-gradient(45deg, #4b0082, #6a0dad, #000080);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 20px;
            font-size: 1.8em;
            animation: pulse 3s infinite;
            border: 2px solid #9370db;
            position: relative;
            overflow: hidden;
        }
        
        .rule-icon::after {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.3) 0%, rgba(255,255,255,0) 70%);
            transform: rotate(30deg);
            animation: shine 5s infinite linear;
        }
        
        .rule-title {
            font-size: 1.6em;
            margin-bottom: 20px;
            background: linear-gradient(45deg, #9370db, #6a0dad);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .rule-list {
            list-style: none;
            color: var(--light);
        }
        
        .rule-list li {
            margin-bottom: 12px;
            padding-left: 25px;
            position: relative;
            line-height: 1.5;
        }
        
        .rule-list li:before {
            content: '•';
            position: absolute;
            left: 10px;
            color: #9370db;
            font-weight: bold;
        }

        /* Футер */
        .footer {
            text-align: center;
            margin-top: 80px;
            padding-top: 40px;
            border-top: 1px solid rgba(106, 13, 173, 0.3);
            color: var(--light);
            position: relative;
        }
        
        .footer::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 1px;
            background: linear-gradient(90deg, transparent, #9370db, transparent);
        }

        /* Server Info */
        .server-info {
            background: rgba(75, 0, 130, 0.3);
            padding: 12px 20px;
            border-radius: 10px;
            border: 1px solid rgba(106, 13, 173, 0.4);
            display: inline-flex;
            align-items: center;
            gap: 10px;
            font-family: monospace;
            font-size: 1.1em;
            margin-top: 20px;
            color: #e0e0e0;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .server-info:hover {
            background: rgba(75, 0, 130, 0.5);
            border-color: rgba(147, 112, 219, 0.6);
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(106, 13, 173, 0.4);
        }

        .server-info.copied {
            background: rgba(0, 128, 0, 0.3);
            border-color: rgba(0, 255, 0, 0.4);
        }

        .server-info.copied::after {
            content: '✓ Скопировано!';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 128, 0, 0.7);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            animation: fadeOut 2s ease-in-out forwards;
        }

        @keyframes fadeOut {
            0% { opacity: 1; }
            70% { opacity: 1; }
            100% { opacity: 0; }
        }

        /* Категории команды */
        .team-category {
            margin-bottom: 60px;
        }
        
        .category-title {
            font-size: 2.2em;
            margin-bottom: 40px;
            text-align: center;
            background: linear-gradient(45deg, #9370db, #6a0dad);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            position: relative;
        }
        
        .category-title::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 100px;
            height: 2px;
            background: linear-gradient(90deg, transparent, #9370db, transparent);
        }

        .page-header {
            text-align: center;
            margin-bottom: 60px;
        }

        .page-header h1 {
            font-size: 3em;
            margin-bottom: 20px;
            background: linear-gradient(45deg, #9370db, #6a0dad);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            position: relative;
            display: inline-block;
        }

        .page-header h1::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 0;
            width: 100%;
            height: 3px;
            background: linear-gradient(90deg, transparent, #9370db, transparent);
            border-radius: 50%;
        }

        /* Стили для системы материи */
        .matter-system {
            text-align: left;
        }

        .matter-category {
            margin-bottom: 25px;
        }

        .matter-category h4 {
            color: #9370db;
            margin-bottom: 15px;
            font-size: 1.2em;
            border-bottom: 1px solid rgba(147, 112, 219, 0.3);
            padding-bottom: 5px;
        }

        .matter-category ul {
            list-style: none;
            color: var(--light);
        }

        .matter-category li {
            margin-bottom: 8px;
            padding: 5px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .matter-amount {
            color: #9370db;
            font-weight: bold;
            float: right;
        }

        /* Стили для системы повышения */
        .progression-system {
            width: 100%;
        }

        .rank-card {
            background: rgba(106, 13, 173, 0.1);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 15px;
            border: 1px solid rgba(106, 13, 173, 0.3);
            transition: all 0.3s ease;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: relative;
            overflow: hidden;
        }

        .rank-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(147, 112, 219, 0.1), transparent);
            transition: left 0.7s ease;
        }

        .rank-card:hover::before {
            left: 100%;
        }

        .rank-card:hover {
            background: rgba(106, 13, 173, 0.15);
            border-color: rgba(147, 112, 219, 0.5);
            transform: translateX(5px);
        }

        .rank-info {
            flex: 1;
        }

        .rank-name {
            font-size: 1.3em;
            font-weight: bold;
            background: linear-gradient(45deg, #9370db, #6a0dad);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 5px;
        }

        .rank-requirements {
            color: var(--light);
            font-size: 0.9em;
        }

        .rank-matter {
            background: rgba(147, 112, 219, 0.2);
            padding: 8px 15px;
            border-radius: 20px;
            font-weight: bold;
            color: #9370db;
            border: 1px solid rgba(147, 112, 219, 0.3);
        }

        .progression-note {
            background: rgba(106, 13, 173, 0.1);
            border-radius: 15px;
            padding: 20px;
            margin-top: 30px;
            border: 1px solid rgba(106, 13, 173, 0.3);
            text-align: center;
            color: var(--light);
            position: relative;
            overflow: hidden;
        }

        .progression-note::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(147, 112, 219, 0.1), transparent);
            transition: left 0.7s ease;
        }

        .progression-note:hover::before {
            left: 100%;
        }

        .progression-note h4 {
            color: #9370db;
            margin-bottom: 10px;
        }

        /* Хэллоуинские украшения */
        .halloween-decoration {
            position: fixed;
            z-index: -1;
            pointer-events: none;
        }
        
        /* Улучшенные тыквы */
        .pumpkin {
            position: fixed;
            width: 60px;
            height: 50px;
            background-color: var(--pumpkin);
            border-radius: 50% 50% 40% 40%;
            z-index: -1;
            animation: pumpkinFloat 20s infinite alternate ease-in-out;
            box-shadow: 0 0 15px rgba(255, 140, 0, 0.5);
            filter: brightness(1);
            transition: filter 0.5s ease;
        }
        
        .pumpkin::before, .pumpkin::after {
            content: '';
            position: absolute;
            width: 15px;
            height: 15px;
            background-color: #000;
            border-radius: 50%;
            top: 15px;
            animation: pumpkinEyes 5s infinite alternate;
        }
        
        .pumpkin::before {
            left: 12px;
        }
        
        .pumpkin::after {
            right: 12px;
        }
        
        .pumpkin-stem {
            position: absolute;
            width: 10px;
            height: 15px;
            background-color: #228B22;
            top: -10px;
            left: 50%;
            transform: translateX(-50%);
            border-radius: 5px 5px 0 0;
        }
        
        .pumpkin-mouth {
            position: absolute;
            width: 30px;
            height: 15px;
            border-bottom: 5px solid #000;
            border-radius: 0 0 50% 50%;
            bottom: 10px;
            left: 50%;
            transform: translateX(-50%);
            animation: pumpkinMouth 8s infinite alternate;
        }
        
        .pumpkin-glow {
            position: absolute;
            width: 100%;
            height: 100%;
            border-radius: inherit;
            box-shadow: 0 0 20px 5px rgba(255, 140, 0, 0.7);
            opacity: 0;
            animation: pumpkinGlow 4s infinite alternate;
        }
        <link href="https://cdn.jsdelivr.net/gh/Alaev-Co/snowflakes/dist/snow.min.css" rel="stylesheet">
        <script src="https://cdn.jsdelivr.net/gh/Alaev-Co/snowflakes/dist/Snow.min.js"></script>
           <script>
	         new Snow ();
             </script>
        
        /* Улучшенные призраки */
        .ghost {
            position: fixed;
            width: 50px;
            height: 65px;
            background-color: rgba(255, 255, 255, 0.8);
            border-radius: 50% 50% 0 0;
            animation: ghostFloat 25s infinite alternate ease-in-out;
            filter: drop-shadow(0 0 8px rgba(255, 255, 255, 0.5));
            z-index: -1;
            opacity: 0.8;
        }
        
        .ghost::before, .ghost::after {
            content: '';
            position: absolute;
            width: 15px;
            height: 20px;
            background-color: rgba(255, 255, 255, 0.8);
            border-radius: 50%;
            top: 30px;
            animation: ghostArms 3s infinite alternate;
        }
        
        .ghost::before {
            left: 5px;
            transform: rotate(-20deg);
        }
        
        .ghost::after {
            right: 5px;
            transform: rotate(20deg);
        }
        
        .ghost-eyes {
            position: absolute;
            width: 8px;
            height: 8px;
            background-color: #000;
            border-radius: 50%;
            top: 20px;
            animation: ghostEyes 4s infinite alternate;
        }
        
        .ghost-eyes.left {
            left: 15px;
        }
        
        .ghost-eyes.right {
            right: 15px;
        }
        
        .ghost-bottom {
            position: absolute;
            width: 100%;
            height: 15px;
            bottom: 0;
            display: flex;
            justify-content: space-around;
            animation: ghostBottom 2s infinite alternate;
        }
        
        .ghost-bottom-wave {
            width: 15px;
            height: 15px;
            border-radius: 50%;
            background-color: rgba(255, 255, 255, 0.8);
        }
        
        /* Паутина */
        .cobweb {
            position: fixed;
            width: 80px;
            height: 80px;
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            z-index: -1;
            animation: cobwebPulse 15s infinite alternate ease-in-out;
        }
        
        .cobweb::before, .cobweb::after {
            content: '';
            position: absolute;
            width: 80px;
            height: 80px;
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            top: 0;
            left: 0;
        }
        
        .cobweb::before {
            transform: rotate(45deg);
        }
        
        .cobweb::after {
            transform: rotate(22.5deg);
        }
        
        .cobweb-center {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: rgba(255, 255, 255, 0.5);
            border-radius: 50%;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            animation: cobwebCenter 3s infinite alternate;
        }
        
        /* Летучие мыши */
        .bat {
            position: fixed;
            width: 40px;
            height: 30px;
            animation: batFly 18s infinite linear;
            z-index: -1;
        }
        
        .bat-body {
            position: absolute;
            width: 15px;
            height: 15px;
            background-color: #000;
            border-radius: 50%;
            top: 7px;
            left: 12px;
        }
        
        .bat-wing {
            position: absolute;
            width: 25px;
            height: 15px;
            background-color: #000;
            border-radius: 50% 50% 0 0;
            top: 0;
            animation: batWing 1s infinite alternate;
        }
        
        .bat-wing.left {
            left: -5px;
            transform: rotate(-30deg);
        }
        
        .bat-wing.right {
            right: -5px;
            transform: rotate(30deg);
        }
        
        .bat-ear {
            position: absolute;
            width: 8px;
            height: 8px;
            background-color: #000;
            border-radius: 50%;
            top: 2px;
        }
        
        .bat-ear.left {
            left: 8px;
        }
        
        .bat-ear.right {
            right: 8px;
        }
        /*
    snow
    */
    (function ($) {
      $.fn.snowFlurry = function (options) {
    var s = $.extend({
      maxSize: 5,
      numberOfFlakes: 25,
      minSpeed: 10,
      maxSpeed: 15,
      color: '#fff',
      timeout: 0
    }, options);
    var windowWidth = $(window).innerWidth(),
      WidthArray = [],
      DelayArray = [],
      animateArray = [],
      flakeSize = [],
      snowInterval;
    if (s.maxSize <= 10) {
      for (var i = 1; i < s.maxSize; i++) {
        flakeSize.push(i);
      }
    } else {
      for (var i = 1; i < 10; i++) {
        flakeSize.push(i);
      }
    }
    for (var i = 0; i < windowWidth - 20; i++) {
      WidthArray.push(i);
    }
    for (var i = 0; i < s.numberOfFlakes; i++) {
      $('<div class="sf-snow-flake"></div>').appendTo('body');
    }
    for (var i = 0; i < 10; i++) {
      DelayArray.push(i);
    }
    for (var i = s.minSpeed; i < s.maxSpeed; i++) {
      animateArray.push(i);
    }
    function getRandomFlakeSize() {
      var item = flakeSize[Math.floor(Math.random() * flakeSize.length)];
      return item;
    }
    function getRandomPosition() {
      var item = WidthArray[Math.floor(Math.random() * WidthArray.length)];
      return item;
    }
    function getRandomDelay() {
      var item = DelayArray[Math.floor(Math.random() * DelayArray.length)];
      return item * 1000;
    }
    function getRandomAnimation() {
      var item = animateArray[Math.floor(Math.random() * animateArray.length)];
      return item * 1000;
    }
    $('.sf-snow-flake').each(function () {
      var elem = $(this);
      elem.attr('data-speed', getRandomAnimation());
      elem.attr('data-delay', getRandomDelay());
      var elemSpeed = elem.attr('data-speed'),
        elemDelay = elem.attr('data-delay');
      var flakeSize = getRandomFlakeSize();
      elem.css({
        'width': flakeSize,
        'height': flakeSize,
        'border-radius': flakeSize / 2,
        'background-color': s.color,
        'box-shadow': '0 0 2px 1px' + s.color
      })
      function activateAnim() {
        setTimeout(function () {
          elem.css('left', getRandomPosition());
          elem.addClass('sf-snow-anim');
          elem.css('transition', 'top ' + elemSpeed / 1000 + 's linear');
          setTimeout(function () {
            elem.css('transition', '');
            elem.removeClass('sf-snow-anim');
          }, elemSpeed);
        }, elemDelay);
      }
      if (device.mobile() || device.tablet() || Modernizr.touch || $('html').hasClass('no-csstransitions')) { } else if (device.desktop()) {
        activateAnim();
        snowInterval = setInterval(function () {
          activateAnim();
        }, +elemDelay + +elemSpeed);
      }
      if (s.timeout != 0) {
        setTimeout(function () {
          clearInterval(snowInterval);
          $('.sf-snow-flake').fadeOut(1500, function () {
            $(this).remove();
          })
        }, s.timeout * 1000);
      }
    });
      };
    }(jQuery));
    jQuery(document).ready(function ($) {
      $(document).snowFlurry({
    maxSize: 10,
    numberOfFlakes: 100,
    minSpeed: 10,
    maxSpeed: 20,
    color: '#fff',
    timeout: 0
      });
    });
        /* Улучшенные анимации для хэллоуинских элементов */
        @keyframes pumpkinFloat {
            0% { transform: translate(0, 0) rotate(0deg) scale(1); }
            25% { transform: translate(20px, 15px) rotate(5deg) scale(1.05); }
            50% { transform: translate(10px, 25px) rotate(-5deg) scale(0.95); }
            75% { transform: translate(15px, 10px) rotate(3deg) scale(1.02); }
            100% { transform: translate(5px, 20px) rotate(-3deg) scale(1); }
        }
        
        @keyframes pumpkinEyes {
            0%, 70% { opacity: 1; }
            75%, 100% { opacity: 0.3; }
        }
        
        @keyframes pumpkinMouth {
            0%, 80% { height: 15px; }
            85%, 100% { height: 20px; }
        }
        
        @keyframes pumpkinGlow {
            0%, 70% { opacity: 0; }
            75%, 100% { opacity: 0.7; }
        }
        
        @keyframes ghostFloat {
            0% { 
                transform: translate(0, 0) scale(1);
                opacity: 0.7;
            }
            25% { 
                transform: translate(15px, 10px) scale(1.05);
                opacity: 0.9;
            }
            50% { 
                transform: translate(30px, 20px) scale(1.1);
                opacity: 0.8;
            }
            75% { 
                transform: translate(20px, 30px) scale(0.95);
                opacity: 0.6;
            }
            100% { 
                transform: translate(10px, 15px) scale(0.9);
                opacity: 0.5;
            }
        }
        
        @keyframes ghostArms {
            0% { transform: rotate(-20deg); }
            100% { transform: rotate(-30deg); }
        }
        
        @keyframes ghostEyes {
            0%, 80% { background-color: #000; }
            85%, 100% { background-color: #ff0000; }
        }
        
        @keyframes ghostBottom {
            0% { transform: translateY(0); }
            100% { transform: translateY(3px); }
        }
        
        @keyframes cobwebPulse {
            0% { transform: scale(1) rotate(0deg); opacity: 0.3; }
            50% { transform: scale(1.1) rotate(180deg); opacity: 0.6; }
            100% { transform: scale(1) rotate(360deg); opacity: 0.3; }
        }
        
        @keyframes cobwebCenter {
            0% { transform: translate(-50%, -50%) scale(1); }
            100% { transform: translate(-50%, -50%) scale(1.2); }
        }
        
        @keyframes batFly {
            0% { transform: translate(0, 0) rotate(0deg); }
            25% { transform: translate(100px, 50px) rotate(90deg); }
            50% { transform: translate(200px, 0) rotate(180deg); }
            75% { transform: translate(100px, -50px) rotate(270deg); }
            100% { transform: translate(0, 0) rotate(360deg); }
        }
        
        @keyframes batWing {
            0% { height: 15px; }
            100% { height: 20px; }
        }
        
        /* Хэллоуинские акценты в навигации */
        .halloween-nav-item {
            position: relative;
        }
        
        .halloween-nav-item::after {
            content: '🎄';
            position: absolute;
            right: 10px;
            font-size: 0.8em;
            opacity: 0;
            transition: opacity 0.3s ease;
            animation: pumpkinJump 2s infinite;
        }
        
        .halloween-nav-item:hover::after {
            opacity: 1;
        }
        
        @keyframes pumpkinJump {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-5px); }
        }
        
        /* Хэллоуинский баннер */
        .halloween-banner {
            position: relative;
            text-align: center;
            margin: 20px 0 40px;
            padding: 15px;
            background: linear-gradient(90deg, transparent, rgba(60, 179, 113, 0.2), transparent);
            border-top: 1px solid rgba(60, 179, 113, 0.3);
            border-bottom: 1px solid rgba(60, 179, 113, 0.3);
            overflow: hidden;
            animation: bannerGlow 3s infinite alternate;
        }
        
        .halloween-banner h2 {
            color: var(--halloween-orange);
            font-size: 1.8em;
            margin-bottom: 10px;
            text-shadow: 0 0 10px rgba(255, 117, 24, 0.5);
            animation: textPulse 2s infinite alternate;
        }
        
        .halloween-banner p {
            color: var(--light);
            font-size: 1.1em;
        }
        
        .halloween-banner::before, .halloween-banner::after {
            content: '🎄';
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            font-size: 1.5em;
            animation: pumpkinSpin 4s infinite linear;
        }
        
        .halloween-banner::before {
            left: 20px;
        }
        
        .halloween-banner::after {
            right: 20px;
        }
        
        @keyframes bannerGlow {
            0% { box-shadow: 0 0 5px rgba(255, 117, 24, 0.3); }
            100% { box-shadow: 0 0 20px rgba(255, 117, 24, 0.7); }
        }
        
        @keyframes textPulse {
            0% { transform: scale(1); }
            100% { transform: scale(1.05); }
        }
        
        @keyframes pumpkinSpin {
            0% { transform: translateY(-50%) rotate(0deg); }
            100% { transform: translateY(-50%) rotate(360deg); }
        }
        
        /* Хэллоуинские акценты в карточках */
        .halloween-card {
            position: relative;
            overflow: hidden;
        }
        
        .halloween-card::before {
            content: '';
            position: absolute;
            top: -10px;
            right: -10px;
            width: 30px;
            height: 30px;
            background-color: var(--halloween-orange);
            border-radius: 50%;
            opacity: 0.3;
            z-index: 1;
            animation: cardPumpkin 4s infinite alternate;
        }
        
        @keyframes cardPumpkin {
            0% { transform: scale(1); }
            100% { transform: scale(1.2); }
        }
        
        /* Хэллоуинские кнопки */
        .halloween-button {
            background: linear-gradient(45deg, var(--halloween-orange), var(--pumpkin)) !important;
            border-color: var(--halloween-orange) !important;
            color: #000 !important;
            font-weight: bold;
            animation: buttonPulse 3s infinite alternate;
        }
        
        .halloween-button:hover {
            background: linear-gradient(45deg, var(--pumpkin), var(--halloween-orange)) !important;
            box-shadow: 0 5px 15px rgba(255, 117, 24, 0.4) !important;
            animation: none;
        }
        
        @keyframes buttonPulse {
            0% { box-shadow: 0 0 5px rgba(255, 117, 24, 0.5); }
            100% { box-shadow: 0 0 15px rgba(255, 117, 24, 0.8); }
        }
        
        /* Адаптивность */
        @media (max-width: 768px) {
            .dark-sidebar {
                width: 60px;
            }
            
            .dark-sidebar:hover {
                width: 200px;
            }
            
            .main-content {
                margin-left: 60px;
            }
            
            .dark-sidebar:hover ~ .main-content {
                margin-left: 200px;
            }
            
            .hero h1 {
                font-size: 2.5em;
            }
            
            .features-grid {
                grid-template-columns: 1fr;
            }
            
            .rules-grid {
                grid-template-columns: 1fr;
            }
            
            .members-grid {
                grid-template-columns: 1fr;
            }
            
            .feature-card {
                padding: 30px 20px;
            }
            
            .feature-icon {
                width: 70px;
                height: 70px;
                font-size: 1.8em;
            }
            
            .symbol-container {
                padding: 30px 20px;
            }
            
            .symbol-icon {
                font-size: 3em;
            }
            
            .section-title {
                font-size: 2em;
            }
            
            .pumpkin, .ghost, .cobweb, .bat {
                transform: scale(0.7);
            }
            
            .halloween-banner h2 {
                font-size: 1.5em;
            }
            
            .halloween-banner::before, .halloween-banner::after {
                font-size: 1.2em;
            }
        }
        
        @media (max-width: 480px) {
            .dark-sidebar {
                width: 50px;
            }
            
            .dark-sidebar:hover {
                width: 180px;
            }
            
            .main-content {
                margin-left: 50px;
            }
            
            .hero {
                padding: 60px 0 40px;
            }
            
            .hero h1 {
                font-size: 2em;
            }
            
            .member-card {
                padding: 25px 20px;
            }
            
            .symbol-container {
                padding: 25px 15px;
            }
            
            .pumpkin, .ghost, .cobweb, .bat {
                transform: scale(0.5);
            }
            
            .halloween-banner h2 {
                font-size: 1.2em;
            }
            
            .halloween-banner p {
                font-size: 0.9em;
            }
            
            .halloween-banner::before, .halloween-banner::after {
                font-size: 1em;
            }
        }
    </style>
</head>
<body>
    <!-- WebGL Canvas -->
    <canvas id="webgl-canvas"></canvas>
    
    <!-- УЛУЧШЕННЫЕ ХЭЛЛОУИНСКИЕ ЭЛЕМЕНТЫ -->
    <div class="halloween-decoration">
        <!-- Тыквы -->
        <div class="pumpkin" style="top: 10%; left: 5%;">
            <div class="pumpkin-stem"></div>
            <div class="pumpkin-mouth"></div>
            <div class="pumpkin-glow"></div>
        </div>
        
        <div class="pumpkin" style="top: 15%; right: 8%; animation-delay: 3s;">
            <div class="pumpkin-stem"></div>
            <div class="pumpkin-mouth"></div>
            <div class="pumpkin-glow"></div>
        </div>
        
        <div class="pumpkin" style="bottom: 20%; left: 10%; animation-delay: 6s;">
            <div class="pumpkin-stem"></div>
            <div class="pumpkin-mouth"></div>
            <div class="pumpkin-glow"></div>
        </div>
        
        <!-- Призраки -->
        <div class="ghost" style="top: 20%; right: 15%; animation-delay: 2s;">
            <div class="ghost-eyes left"></div>
            <div class="ghost-eyes right"></div>
            <div class="ghost-bottom">
                <div class="ghost-bottom-wave"></div>
                <div class="ghost-bottom-wave"></div>
                <div class="ghost-bottom-wave"></div>
            </div>
        </div>
        
        <div class="ghost" style="bottom: 30%; left: 20%; animation-delay: 5s;">
            <div class="ghost-eyes left"></div>
            <div class="ghost-eyes right"></div>
            <div class="ghost-bottom">
                <div class="ghost-bottom-wave"></div>
                <div class="ghost-bottom-wave"></div>
                <div class="ghost-bottom-wave"></div>
            </div>
        </div>
        
        <!-- Паутина -->
        <div class="cobweb" style="top: 5%; right: 5%;">
            <div class="cobweb-center"></div>
        </div>
        <div class="cobweb" style="bottom: 10%; left: 5%; animation-delay: 7s;">
            <div class="cobweb-center"></div>
        </div>
        
        <!-- Летучие мыши -->
        <div class="bat" style="top: 15%; left: 20%; animation-delay: 0s;">
            <div class="bat-body"></div>
            <div class="bat-wing left"></div>
            <div class="bat-wing right"></div>
            <div class="bat-ear left"></div>
            <div class="bat-ear right"></div>
        </div>
        
        <div class="bat" style="top: 25%; right: 25%; animation-delay: 4s;">
            <div class="bat-body"></div>
            <div class="bat-wing left"></div>
            <div class="bat-wing right"></div>
            <div class="bat-ear left"></div>
            <div class="bat-ear right"></div>
        </div>
        
        <div class="bat" style="bottom: 15%; left: 30%; animation-delay: 8s;">
            <div class="bat-body"></div>
            <div class="bat-wing left"></div>
            <div class="bat-wing right"></div>
            <div class="bat-ear left"></div>
            <div class="bat-ear right"></div>
        </div>
    </div>
    
    <!-- НОВАЯ БОКОВАЯ ПАНЕЛЬ НАВИГАЦИИ -->
    <nav class="dark-sidebar">
        <div class="sidebar-logo">
            <i class="fas fa-moon"></i>
        </div>
        
        <div class="sidebar-nav">
            <div class="nav-item halloween-nav-item active" onclick="showSection('main')">
                <div class="nav-icon">
                    <i class="fas fa-home"></i>
                </div>
                <div class="nav-text">Главная</div>
            </div>
            
            <div class="nav-item halloween-nav-item" onclick="showSection('symbol')">
                <div class="nav-icon">
                    <i class="fas fa-ankh"></i>
                </div>
                <div class="nav-text">Символ Мрака</div>
            </div>
            
            <div class="nav-item halloween-nav-item" onclick="showSection('rules')">
                <div class="nav-icon">
                    <i class="fas fa-scroll"></i>
                </div>
                <div class="nav-text">Устав Братства</div>
            </div>
            
            <div class="nav-item halloween-nav-item" onclick="showSection('team')">
                <div class="nav-icon">
                    <i class="fas fa-users"></i>
                </div>
                <div class="nav-text">Состав Отряда</div>
            </div>
            
            <div class="nav-item halloween-nav-item" onclick="showSection('progression')">
                <div class="nav-icon">
                    <i class="fas fa-chart-line"></i>
                </div>
                <div class="nav-text">Система Повышения</div>
            </div>
        </div>
    </nav>

    <!-- Основной контент -->
    <div class="main-content">
        <div class="container">
            <!-- Главная страница -->
            <div id="main" class="section active">
                <!-- новогодний БАННЕР -->
                <div class="halloween-banner">
                    <h2>🎄 Новогодний Вайб в отряде Мрак 🎄</h2>
                    <p>Счастливого нового года, всего вам мрачного</p>
                </div>
                
                <section class="hero">
                    <h1>ОТРЯД МРАК</h1>
                    <p>Тайное братство, где тьма становится силой, а молчание - оружием.</p>
                    
                    <div class="server-info" id="server-ip" onclick="copyServerIP()">
                        <i class="fas fa-server"></i>
                        <span>s5.yufu.su:27017</span>
                    </div>
                </section>

                <div class="features-grid">
                    <div class="feature-card halloween-card">
                        <div class="feature-icon">
                            <i class="fas fa-ankh"></i>
                        </div>
                        <h3>Символ Мрака</h3>
                        <p>Узнай о древнем символе, что объединяет всех членов нашего братства. Тайный знак, несущий силу и защиту.</p>
                        <div class="feature-button halloween-button" onclick="showSection('symbol')">
                            Узнать о символе
                        </div>
                    </div>
                    
                    <div class="feature-card halloween-card">
                        <div class="feature-icon">
                            <i class="fas fa-book"></i>
                        </div>
                        <h3>Устав Братства</h3>
                        <p>Законы тьмы, которые оберегают наше братство. Дисциплина и порядок - основа силы Мрака.</p>
                        <div class="feature-button halloween-button" onclick="showSection('rules')">
                            Изучить устав
                        </div>
                    </div>
                    
                    <div class="feature-card halloween-card">
                        <div class="feature-icon">
                            <i class="fas fa-users"></i>
                        </div>
                        <h3>Иерархия Тени</h3>
                        <p>От Жнеца Мрака до Мрачной Жницы - каждый находит свое место в нашей иерархии, основанной на силе и преданности.</p>
                        <div class="feature-button halloween-button" onclick="showSection('team')">
                            Узнать состав
                        </div>
                    </div>

                    <div class="feature-card halloween-card">
                        <div class="feature-icon">
                            <i class="fas fa-chart-line"></i>
                        </div>
                        <h3>Система Повышения</h3>
                        <p>Путь от Демона к Цукумону через накопление материи. Узнай как повысить свой ранг в братстве.</p>
                        <div class="feature-button halloween-button" onclick="showSection('progression')">
                            Узнать о повышении
                        </div>
                    </div>
                </div>
            </div>

            <!-- Символ Мрака -->
            <div id="symbol" class="section">
                <div class="page-header">
                    <h1>СИМВОЛ МРАКА</h1>
                    <p style="color: var(--light); max-width: 600px; margin: 0 auto; font-size: 1.2em;">
                        Древний знак, объединяющий братство тьмы
                    </p>
                </div>

                <div class="symbol-section">
                    <div class="symbol-container">
                        <div class="symbol-icon">
                            <i class="fas fa-ankh"></i>
                        </div>
                        <h2 class="symbol-title">АНКХ ТЬМЫ</h2>
                        <div class="symbol-description">
                            <p>Наш символ - древний Анкх, переплетенный с лунным серпом. Он олицетворяет вечную жизнь во тьме, мудрость ночи и силу, что проистекает из глубин мироздания.</p>
                            <p style="margin-top: 15px;">Анкх Тьмы объединяет три начала: </p>
                            <ul style="text-align: left; margin-top: 15px; color: var(--light);">
                                <li><strong>Верхняя петля</strong> - вечность и бесконечность мрака</li>
                                <li><strong>Перекладина</strong> - равновесие между светом и тьмой</li>
                                <li><strong>Вертикальная ось</strong> - связь между мирами</li>
                            </ul>
                            <p style="margin-top: 20px; font-style: italic;">"В темноте мы обретаем силу, в молчании - мудрость, в единстве - бессмертие"</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Устав -->
            <div id="rules" class="section">
                <div class="page-header">
                    <h1>УСТАВ ОТРЯДА МРАК</h1>
                    <p style="color: var(--light); max-width: 600px; margin: 0 auto; font-size: 1.2em;">
                        Законы тьмы, которые оберегают наше братство
                    </p>
                </div>

                <!-- Правила -->
                <div class="rules-grid">
                    <!-- Обязанности -->
                    <div class="rule-card halloween-card">
                        <div class="rule-icon"><i class="fas fa-shield-alt"></i></div>
                        <h3 class="rule-title">Кодекс Чести</h3>
                        <ul class="rule-list">
                            <li>Храни тайны братства Мрака</li>
                            <li>Защищай собратьев по тени</li>
                            <li>Уважай иерархию и старших</li>
                            <li>Совершенствуй свои навыки</li>
                            <li>Будь предан идеалам Мрака</li>
                        </ul>
                    </div>
                    
                    <!-- Запреты -->
                    <div class="rule-card halloween-card">
                        <div class="rule-icon"><i class="fas fa-ban"></i></div>
                        <h3 class="rule-title">Запреты Тьмы</h3>
                        <ul class="rule-list">
                            <li>Не раскрывай секреты отряда</li>
                            <li>Не предавай доверие собратьев</li>
                            <li>Не действуй вопреки приказам</li>
                            <li>Не проявляй слабость перед чужими</li>
                            <li>Не нарушай законы иерархии</li>
                        </ul>
                    </div>
                    
                    <!-- Ценности -->
                    <div class="rule-card halloween-card">
                        <div class="rule-icon"><i class="fas fa-gem"></i></div>
                        <h3 class="rule-title">Ценности Братства</h3>
                        <ul class="rule-list">
                            <li>Сила через единство</li>
                            <li>Мудрость через молчание</li>
                            <li>Власть через знание</li>
                            <li>Защита через тень</li>
                            <li>Бессмертие через legacy</li>
                        </ul>
                    </div>
                </div>
            </div>

            <!-- Состав -->
            <div id="team" class="section">
                <div class="page-header">
                    <h1>СОСТАВ ОТРЯДА МРАК</h1>
                    <p style="color: var(--light); max-width: 600px; margin: 0 auto; font-size: 1.2em;">
                        Иерархия теней, где каждый нашел свое место
                    </p>
                </div>

                <!-- Структура команды -->
                <div class="team-structure">
                    <!-- Владелец -->
                    <div class="team-category">
                        <h2 class="category-title">Владелец Отряда</h2>
                        <div class="members-grid">
                            <div class="member-card halloween-card">
                                <div class="member-avatar"><i class="fas fa-crown"></i></div>
                                <div class="member-rank">Мрачная Жница Мрака</div>
                                <div class="member-name">Токи Юри</div>
                                <div class="member-role">Владелец отряда<br>Верховная правительница</div>
                            </div>
                        </div>
                    </div>

                    <!-- Командный состав -->
                    <div class="team-category">
                        <h2 class="category-title">Командный Состав</h2>
                        <div class="members-grid">
                            <div class="member-card halloween-card">
                                <div class="member-avatar"><i class="fas fa-star"></i></div>
                                <div class="member-rank">Старший Жнец Мрака</div>
                                <div class="member-name">Tanuki Doto</div>
                                <div class="member-role">Командир отряда (CMD)<br>Тактическое руководство</div>
                            </div>
                            
                            <div class="member-card halloween-card">
                                <div class="member-avatar"><i class="fas fa-star"></i></div>
                                <div class="member-rank">Старший Жнец Мрака</div>
                                <div class="member-name">Yuika Miorine</div>
                                <div class="member-role">Заместитель командира (D.CMD)<br>Оперативное управление</div>
                            </div>
                        </div>
                    </div>

                    <!-- Инструкторы -->
                    <div class="team-category">
                        <h2 class="category-title">Инструкторы Мрака</h2>
                        <div class="members-grid">
                            <div class="member-card halloween-card">
                                <div class="member-avatar"><i class="fas fa-user-graduate"></i></div>
                                <div class="member-rank">Инструктор Мрака</div>
                                <div class="member-name">Ашина Кайдо</div>
                                <div class="member-role">Главный инструктор<br>Обучение новичков</div>
                            </div>
                            
                            <div class="member-card halloween-card">
                                <div class="member-avatar"><i class="fas fa-user-graduate"></i></div>
                                <div class="member-rank">Инструктор Мрака</div>
                                <div class="member-name">Сабуро Гусато</div>
                                <div class="member-role">Инструктор<br>Боевая подготовка</div>
                            </div>
                            
                            <div class="member-card halloween-card">
                                <div class="member-avatar"><i class="fas fa-user-graduate"></i></div>
                                <div class="member-rank">Инструктор Мрака</div>
                                <div class="member-name">Каге Мидзуно</div>
                                <div class="member-role">Инструктор<br>Стратегия и тактика</div>
                            </div>
                        </div>
                    </div>

                    <!-- Боевой состав -->
                    <div class="team-category">
                        <h2 class="category-title">Жнецы Мрака</h2>
                        <div class="members-grid">
                            <div class="member-card halloween-card">
                                <div class="member-avatar"><i class="fas fa-moon"></i></div>
                                <div class="member-rank">Жнец Мрака</div>
                                <div class="member-name">Отава Кунзе</div>
                                <div class="member-role">Боец<br>Исполнитель приказов</div>
                            </div>
                            
                            <div class="member-card halloween-card">
                                <div class="member-avatar"><i class="fas fa-moon"></i></div>
                                <div class="member-rank">Жнец Мрака</div>
                                <div class="member-name">Сугихаре Макиро</div>
                                <div class="member-role">Боец<br>Суматоха</div>
                            </div>
                            
                            <div class="member-card halloween-card">
                                <div class="member-avatar"><i class="fas fa-moon"></i></div>
                                <div class="member-rank">Жнец Мрака</div>
                                <div class="member-name">Рётто Гусато</div>
                                <div class="member-role">Боец<br>Чертилкин</div>
                            </div>
                            
                            <div class="member-card halloween-card vacant">
                                <div class="member-avatar"><i class="fas fa-user-plus"></i></div>
                                <div class="member-rank">Жнец Мрака</div>
                                <div class="member-name">[Вакантно]</div>
                                <div class="member-role">Боец<br>Чернило</div>
                            </div>
                            
                            <div class="member-card halloween-card vacant">
                                <div class="member-avatar"><i class="fas fa-user-plus"></i></div>
                                <div class="member-rank">Жнец Мрака</div>
                                <div class="member-name">[Вакантно]</div>
                                <div class="member-role">Боец<br>Шпакля</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Система повышения -->
            <div id="progression" class="section">
                <div class="page-header">
                    <h1>СИСТЕМА ПОВЫШЕНИЯ</h1>
                    <p style="color: var(--light); max-width: 600px; margin: 0 auto; font-size: 1.2em;">
                        Путь от Демона к Цукумону через накопление материи
                    </p>
                </div>

                <div class="features-grid">
                    <!-- Система получения материи -->
                    <div class="feature-card halloween-card">
                        <div class="feature-icon">
                            <i class="fas fa-coins"></i>
                        </div>
                        <h3>Получение Материи</h3>
                        <div class="matter-system">
                            <div class="matter-category">
                                <h4>Боевые действия</h4>
                                <ul>
                                    <li>Убийство 1 истребителя ➤ <span class="matter-amount">1 материя</span></li>
                                    <li>Убийство 1 столпа ➤ <span class="matter-amount">2 материи</span></li>
                                    <li>Захват важной точки ➤ <span class="matter-amount">5 материй</span></li>
                                    <li>Захват 2 точек ➤ <span class="matter-amount">2 материи</span></li>
                                    <li>Участие в ГРП ➤ <span class="matter-amount">5 материй</span></li>
                                </ul>
                            </div>
                            
                            <div class="matter-category">
                                <h4>Задания</h4>
                                <ul>
                                    <li>Инструктора Мрака ➤ <span class="matter-amount">2-5 материй</span></li>
                                    <li>Старшего Жнеца ➤ <span class="matter-amount">5-7 материй</span></li>
                                    <li>Мрачной Жницы ➤ <span class="matter-amount">10 материй</span></li>
                                    <li>Низшей луны ➤ <span class="matter-amount">5 материй</span></li>
                                    <li>Высшей луны ➤ <span class="matter-amount">7 материй</span></li>
                                </ul>
                            </div>
                            
                            <div class="matter-category">
                                <h4>Тренировки и мероприятия</h4>
                                <ul>
                                    <li>Проведение тренировки ➤ <span class="matter-amount">3 материи</span></li>
                                    <li>Участие в тренировке ➤ <span class="matter-amount">2 материи</span></li>
                                    <li>Участие в мероприятии ➤ <span class="matter-amount">4 материи</span></li>
                                </ul>
                            </div>
                            
                            <div class="matter-category">
                                <h4>Почтения</h4>
                                <ul>
                                    <li>1 степень ➤ <span class="matter-amount">5+ материй</span></li>
                                    <li>2 степень ➤ <span class="matter-amount">10+ материй</span></li>
                                    <li>3 степень ➤ <span class="matter-amount">15+ материй</span></li>
                                </ul>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Система повышения -->
                    <div class="feature-card halloween-card">
                        <div class="feature-icon">
                            <i class="fas fa-chart-line"></i>
                        </div>
                        <h3>Путь Повышения</h3>
                        <div class="progression-system">
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Otokuma ➤ Demon</div>
                                    <div class="rank-requirements">КД: 1 день</div>
                                </div>
                                <div class="rank-matter">5 материй</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Demon ➤ Keykon</div>
                                    <div class="rank-requirements">КД: 1 день</div>
                                </div>
                                <div class="rank-matter">10 материй</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Keykon ➤ Hofuma</div>
                                    <div class="rank-requirements">КД: 2 дня</div>
                                </div>
                                <div class="rank-matter">15 материй</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Hofuma ➤ Chisuma</div>
                                    <div class="rank-requirements">КД: 2 дня</div>
                                </div>
                                <div class="rank-matter">20 материй</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Chisuma ➤ Chikuma</div>
                                    <div class="rank-requirements">КД: 2 дня</div>
                                </div>
                                <div class="rank-matter">25 материй</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Chikuma ➤ Asakuma</div>
                                    <div class="rank-requirements">КД: 2 дня</div>
                                </div>
                                <div class="rank-matter">30 материй</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Asakuma ➤ Hobura</div>
                                    <div class="rank-requirements">КД: 3 дня</div>
                                </div>
                                <div class="rank-matter">35 материй</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Hobura ➤ Shateigashira</div>
                                    <div class="rank-requirements">КД: 3 дня</div>
                                </div>
                                <div class="rank-matter">40 материй</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Shateigashira ➤ Wakagashira</div>
                                    <div class="rank-requirements">КД: 3 дня</div>
                                </div>
                                <div class="rank-matter">45 материй</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Wakagashira ➤ Tsukumon</div>
                                    <div class="rank-requirements">КД: 3 дня</div>
                                </div>
                                <div class="rank-matter">50 материй</div>
                            </div>
                        </div>
                        
                        <div class="progression-note">
                            <h4>Важная информация</h4>
                            <p>Учет материи ведется самостоятельно. В отчет о повышении прикладывайте скриншоты ваших действий.</p>
                            <p style="margin-top: 10px; font-size: 0.9em;">Материю можно выкупить за Йены у Старших Жнецов Мрака+</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="footer">
            <p>© 2025 Отряд Мрак | s5.yufu.su:27017</p>
            <p style="margin-top: 10px; font-size: 0.9em;">Тень • Сила • Тайна • 🎄 Хэллоуин 🎄</p>
        </div>
    </div>

    <script>
        function showSection(sectionId) {
            // Скрываем все секции
            document.querySelectorAll('.section').forEach(section => {
                section.style.display = 'none';
            });
            
            // Показываем выбранную секцию
            const targetSection = document.getElementById(sectionId);
            if (targetSection) {
                targetSection.style.display = 'block';
                targetSection.classList.add('active');
                
                // Плавная прокрутка к верху
                window.scrollTo({ top: 0, behavior: 'smooth' });
            }
            
            // Обновляем активную ссылку в навигации
            document.querySelectorAll('.nav-item').forEach(link => {
                link.classList.remove('active');
            });
            
            // Находим соответствующую ссылку и делаем ее активной
            const activeLink = document.querySelector(`.nav-item[onclick="showSection('${sectionId}')"]`);
            if (activeLink) {
                activeLink.classList.add('active');
            }
        }

        // Функция копирования IP-адреса сервера
        function copyServerIP() {
            const serverIP = 's5.yufu.su:27017';
            const serverElement = document.getElementById('server-ip');
            
            // Используем современный API для копирования в буфер обмена
            navigator.clipboard.writeText(serverIP).then(() => {
                // Показываем визуальное подтверждение
                serverElement.classList.add('copied');
                
                // Возвращаем исходный вид через 2 секунды
                setTimeout(() => {
                    serverElement.classList.remove('copied');
                }, 2000);
                
                // Дополнительное подтверждение в консоли
                console.log('IP-адрес сервера скопирован: ' + serverIP);
            }).catch(err => {
                // Fallback для старых браузеров
                console.error('Ошибка при копировании: ', err);
                
                // Альтернативный метод копирования
                const textArea = document.createElement('textarea');
                textArea.value = serverIP;
                document.body.appendChild(textArea);
                textArea.select();
                document.execCommand('copy');
                document.body.removeChild(textArea);
                
                // Показываем визуальное подтверждение даже при fallback
                serverElement.classList.add('copied');
                setTimeout(() => {
                    serverElement.classList.remove('copied');
                }, 2000);
            });
        }

        // Инициализация при загрузке
        document.addEventListener('DOMContentLoaded', function() {
            // Показываем главную страницу по умолчанию
            showSection('main');
            
            // Анимация появления элементов при скролле
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.style.opacity = '1';
                        entry.target.style.transform = 'translateY(0)';
                    }
                });
            }, { threshold: 0.1 });

            // Наблюдаем за всеми анимируемыми элементами
            document.querySelectorAll('.feature-card, .member-card, .rule-card, .symbol-container, .rank-card').forEach(el => {
                el.style.opacity = '0';
                el.style.transform = 'translateY(30px)';
                el.style.transition = 'opacity 0.6s ease, transform 0.6s ease';
                observer.observe(el);
            });
        });

        // WebGL Background Script
        class WebGLBackground {
            constructor() {
                this.canvas = document.getElementById('webgl-canvas');
                this.gl = this.canvas.getContext('webgl');
                this.particles = [];
                this.mouse = { x: 0, y: 0 };
                this.time = 0;
                
                if (!this.gl) {
                    console.error('WebGL not supported');
                    return;
                }
                
                this.init();
                this.animate();
                
                document.addEventListener('mousemove', (e) => {
                    this.mouse.x = (e.clientX / window.innerWidth) * 2 - 1;
                    this.mouse.y = -(e.clientY / window.innerHeight) * 2 + 1;
                });
            }

            init() {
                this.resize();
                window.addEventListener('resize', () => this.resize());
                this.createShaders();
                this.createBuffers();
                this.createParticles();
            }

            resize() {
                this.canvas.width = window.innerWidth;
                this.canvas.height = window.innerHeight;
                this.gl.viewport(0, 0, this.canvas.width, this.canvas.height);
            }

            createShaders() {
                const vsSource = `
                    attribute vec2 aPosition;
                    attribute float aSize;
                    attribute vec3 aColor;
                    attribute float aAlpha;
                    
                    uniform float uTime;
                    uniform vec2 uMouse;
                    uniform vec2 uResolution;
                    
                    varying vec3 vColor;
                    varying float vAlpha;
                    
                    void main() {
                        float moveX = sin(uTime * 0.5 + aPosition.x) * 0.1;
                        float moveY = cos(uTime * 0.3 + aPosition.y) * 0.1;
                        
                        float mouseDist = distance(aPosition, uMouse);
                        float mouseInfluence = 0.2 * (1.0 - smoothstep(0.0, 0.5, mouseDist));
                        
                        vec2 position = aPosition + vec2(moveX, moveY) + uMouse * mouseInfluence;
                        
                        vec2 normalized = position / uResolution * 2.0 - 1.0;
                        gl_Position = vec4(normalized.x, normalized.y, 0.0, 1.0);
                        
                        float pulse = sin(uTime * 2.0 + aPosition.x + aPosition.y) * 0.2 + 0.8;
                        gl_PointSize = aSize * pulse;
                        
                        vColor = aColor;
                        vAlpha = aAlpha;
                    }
                `;

                const fsSource = `
                    precision mediump float;
                    
                    varying vec3 vColor;
                    varying float vAlpha;
                    
                    void main() {
                        float dist = length(gl_PointCoord - vec2(0.5));
                        if (dist > 0.5) {
                            discard;
                        }
                        
                        float alpha = vAlpha * (1.0 - smoothstep(0.3, 0.5, dist));
                        
                        gl_FragColor = vec4(vColor, alpha);
                    }
                `;

                const vertexShader = this.compileShader(this.gl.VERTEX_SHADER, vsSource);
                const fragmentShader = this.compileShader(this.gl.FRAGMENT_SHADER, fsSource);
                
                this.program = this.gl.createProgram();
                this.gl.attachShader(this.program, vertexShader);
                this.gl.attachShader(this.program, fragmentShader);
                this.gl.linkProgram(this.program);
                
                if (!this.gl.getProgramParameter(this.program, this.gl.LINK_STATUS)) {
                    console.error('Unable to initialize the shader program: ' + this.gl.getProgramInfoLog(this.program));
                }
                
                this.gl.useProgram(this.program);
                
                this.aPosition = this.gl.getAttribLocation(this.program, 'aPosition');
                this.aSize = this.gl.getAttribLocation(this.program, 'aSize');
                this.aColor = this.gl.getAttribLocation(this.program, 'aColor');
                this.aAlpha = this.gl.getAttribLocation(this.program, 'aAlpha');
                
                this.uTime = this.gl.getUniformLocation(this.program, 'uTime');
                this.uMouse = this.gl.getUniformLocation(this.program, 'uMouse');
                this.uResolution = this.gl.getUniformLocation(this.program, 'uResolution');
            }

            compileShader(type, source) {
                const shader = this.gl.createShader(type);
                this.gl.shaderSource(shader, source);
                this.gl.compileShader(shader);
                
                if (!this.gl.getShaderParameter(shader, this.gl.COMPILE_STATUS)) {
                    console.error('An error occurred compiling the shaders: ' + this.gl.getShaderInfoLog(shader));
                    this.gl.deleteShader(shader);
                    return null;
                }
                
                return shader;
            }

            createBuffers() {
                this.positionBuffer = this.gl.createBuffer();
                this.sizeBuffer = this.gl.createBuffer();
                this.colorBuffer = this.gl.createBuffer();
                this.alphaBuffer = this.gl.createBuffer();
            }

            createParticles() {
                const particleCount = 400;
                
                for (let i = 0; i < particleCount; i++) {
                    this.particles.push({
                        x: Math.random() * this.canvas.width,
                        y: Math.random() * this.canvas.height,
                        size: Math.random() * 2 + 1,
                        color: [
                            Math.random() * 0.3 + 0.3,
                            Math.random() * 0.2 + 0.2,
                            Math.random() * 0.4 + 0.4
                        ],
                        alpha: Math.random() * 0.2 + 0.1,
                        speedX: (Math.random() - 0.5) * 0.3,
                        speedY: (Math.random() - 0.5) * 0.3
                    });
                }
            }

            updateParticles() {
                this.particles.forEach(particle => {
                    particle.x += particle.speedX;
                    particle.y += particle.speedY;
                    
                    if (particle.x < 0) particle.x = this.canvas.width;
                    if (particle.x > this.canvas.width) particle.x = 0;
                    if (particle.y < 0) particle.y = this.canvas.height;
                    if (particle.y > this.canvas.height) particle.y = 0;
                });
            }

            render() {
                this.gl.clearColor(0.0, 0.0, 0.0, 0.0);
                this.gl.clear(this.gl.COLOR_BUFFER_BIT);
                
                this.gl.uniform1f(this.uTime, this.time);
                this.gl.uniform2f(this.uMouse, this.mouse.x, this.mouse.y);
                this.gl.uniform2f(this.uResolution, this.canvas.width, this.canvas.height);
                
                const positions = [];
                const sizes = [];
                const colors = [];
                const alphas = [];
                
                this.particles.forEach(particle => {
                    positions.push(particle.x, particle.y);
                    sizes.push(particle.size);
                    colors.push(...particle.color);
                    alphas.push(particle.alpha);
                });
                
                this.gl.bindBuffer(this.gl.ARRAY_BUFFER, this.positionBuffer);
                this.gl.bufferData(this.gl.ARRAY_BUFFER, new Float32Array(positions), this.gl.STATIC_DRAW);
                this.gl.enableVertexAttribArray(this.aPosition);
                this.gl.vertexAttribPointer(this.aPosition, 2, this.gl.FLOAT, false, 0, 0);
                
                this.gl.bindBuffer(this.gl.ARRAY_BUFFER, this.sizeBuffer);
                this.gl.bufferData(this.gl.ARRAY_BUFFER, new Float32Array(sizes), this.gl.STATIC_DRAW);
                this.gl.enableVertexAttribArray(this.aSize);
                this.gl.vertexAttribPointer(this.aSize, 1, this.gl.FLOAT, false, 0, 0);
                
                this.gl.bindBuffer(this.gl.ARRAY_BUFFER, this.colorBuffer);
                this.gl.bufferData(this.gl.ARRAY_BUFFER, new Float32Array(colors), this.gl.STATIC_DRAW);
                this.gl.enableVertexAttribArray(this.aColor);
                this.gl.vertexAttribPointer(this.aColor, 3, this.gl.FLOAT, false, 0, 0);
                
                this.gl.bindBuffer(this.gl.ARRAY_BUFFER, this.alphaBuffer);
                this.gl.bufferData(this.gl.ARRAY_BUFFER, new Float32Array(alphas), this.gl.STATIC_DRAW);
                this.gl.enableVertexAttribArray(this.aAlpha);
                this.gl.vertexAttribPointer(this.aAlpha, 1, this.gl.FLOAT, false, 0, 0);
                
                this.gl.drawArrays(this.gl.POINTS, 0, this.particles.length);
            }

            animate() {
                this.time += 0.01;
                this.updateParticles();
                this.render();
                requestAnimationFrame(() => this.animate());
            }
        }

        window.addEventListener('load', () => {
            new WebGLBackground();
        });
    </script>
</body>
</html>
