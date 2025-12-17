
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Отряд МРАК - Новый Год</title>
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
            background: url('https://i.postimg.cc/NFjD2CJW/3db32463-2150-4c18-b1d1-7b64cf57a1d0.png') no-repeat center center fixed;
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
            text-shadow: 0 0 10px rgba(60, 179, 113, 0.5);
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
            0% { box-shadow: 0 0 5px rgba(60, 179, 113, 0.3); }
            100% { box-shadow: 0 0 20px rgba(60, 179, 113, 0.7); }
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
            box-shadow: 0 5px 15px rgba(60, 179, 113, 0.4) !important;
            animation: none;
        }
        
        @keyframes buttonPulse {
            0% { box-shadow: 0 0 5px rgba(60, 179, 113, 0.5); }
            100% { box-shadow: 0 0 15px rgba(60, 179, 113, 0.8); }
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
                <div class="nav-text">Лор Мрака</div>
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
                    <h1>ОТРЯДА МРАК</h1>
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
                        <h3>Лор Жнецов Мрака</h3>
                        <p>Узнай лор и ключевую информацию о отраде Мрака.</p>
                        <div class="feature-button halloween-button" onclick="showSection('symbol')">
                            Узнать лор
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
                        <p>Путь от Демона к Шико через накопление Кровавых Монет. Узнай как повысить свой ранг в братстве.</p>
                        <div class="feature-button halloween-button" onclick="showSection('progression')">
                            Узнать о повышении
                        </div>
                    </div>
                </div>
            </div>

            <!-- Лор Мрака -->
            <div id="symbol" class="section">
                <div class="page-header">
                    <h1>Демонический отряд «Мрак» (暗闇)</h1>
                    <p style="color: var(--light); max-width: 600px; margin: 0 auto; font-size: 1.2em;">
                        Информация и ключевые моменты нашего братсва
                    </p>
                </div>

                <div class="symbol-section">
                    <div class="symbol-container">
                        <div class="symbol-icon">
                            <i class="fas fa-ankh"></i>
                        </div>
                        <h2 class="symbol-title">ЛОР ЖНЕЦОВ МРАКА(暗闇)</h2>
                        <div class="symbol-description">
                            <p>«Тайный отряд, что служил великому Сёгуну, мы выполняли работу во тьме, наши жертвы даже не замечали нас. Однако смерть Сёгуна - сделала нас ронинами. Мы годами скитались под покровом ночи, выполняя всю грязную работу, что нам поручали.                             Наше стремление получить больше могущества и власти, нарастало с каждый днем. 
                            Но одна ночь изменила нашу жизнь навсегда. Нам было дано задание, от неизвестного. Нужно было устранить некую девушку, в городе Асакуса. После прибытия на месте, мы ужаснулись. К сожалению мы не смогли справиться с заданием, ведь эта                                    девушка оказалась сильнее нашего отряда. После бойни, нам поступило предложение: “Станьте моими тенями, служите во мраке, а я дарую вам силу”. После чего перед нами предстала уже не дама, а мужчина и назвался он Мудзан  Кибуцуджи. А дальше                              все как в тумане, он даровал нам кровь. Тьма, безграничная бездна мрака, поглотила нас, наши мечи, что сияли, что отражали свет луны, покрылись мраком и поглощали любой намек на свет. Так мы стали отрядом Мрака, что служит великому Мудзану                              Кибуцуджи.
                            Наш отряд более не являлся безымянным отрядом ронинов. Нам даровали силу и название, теперь мы: “Отряд мрака - тайное братство, где тьма становится силой, а молчание - оружием. ”</p>
                            <p style="margin-top: 15px;">Ключевые детали лора </p>
                            <ul style="text-align: left; margin-top: 15px; color: var(--light);">
                                <li><strong>Происхождение:</strong>Отряд самураев, что по стечению обстоятельств, стал ронинами.</li>
                                <li><strong>Философия:</strong>Главным оружием отряда является тьма, они скрываются в ней, она является как их защитником, так и их оружием. Все суждения посвящены мраку. Истинная сила таиться в мраке.</li>
                                <li><strong>Тактика:</strong>Они использую силу мрака в свою пользу, они выполняют поставленные задачи, быстро и чисто, без лишних колебаний.</li>
                                <li><strong>Цель:</strong>Сбор крови сильнейших истребителей для ритуала пробуждения древнего духа мрака, который поглотит солнце. Веря, что абсолютная тьма, поможет демонам в борьбе с истребителями.</li>
                                <li><strong>Слабость:</strong>Любой демон мрака нуждается в постоянном наличии, свежей крови истребителя, в ином случае жнец теряет силу. Если жнец выпьет слишком много крови, он начнет терять контроль над собой.</li>
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
                                <div class="member-name">Амайя Кумагаи</div>
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
                                <div class="member-name">Goro Agave</div>
                                <div class="member-role">Командир отряда (CMD)<br></div>
                            </div>
                            
                            <div class="member-card halloween-card">
                                <div class="member-avatar"><i class="fas fa-star"></i></div>
                                <div class="member-rank">Старший Жнец Мрака</div>
                                <div class="member-name">Shisui Agave</div>
                                <div class="member-role">Заместитель командира (D.CMD)<br></div>
                            </div>
                        </div>
                    </div>

                    <!-- Инструкторы -->
                    <div class="team-category">
                        <h2 class="category-title">Инструкторы Мрака</h2>
                        <div class="members-grid">
                             <div class="member-card halloween-card vacant">
                                <div class="member-avatar"><i class="fas fa-user-plus"></i></div>
                                <div class="member-rank">Инструктор Мрака</div>
                                <div class="member-name">[Вакантно]</div>
                                <div class="member-role">Инструктор<br></div>
                            </div>
                            
                             <div class="member-card halloween-card vacant">
                                <div class="member-avatar"><i class="fas fa-user-plus"></i></div>
                                <div class="member-rank">Инструктор Мрака</div>
                                <div class="member-name">[Вакантно]</div>
                                <div class="member-role">Инструктор<br></div>
                            </div>
                            
                             <div class="member-card halloween-card vacant">
                                <div class="member-avatar"><i class="fas fa-user-plus"></i></div>
                                <div class="member-rank">Инструктор Мрака</div>
                                <div class="member-name">[Вакантно]</div>
                                <div class="member-role">Инструктор<br></div>
                            </div>
                        </div>
                    </div>

                    <!-- Боевой состав -->
                    <div class="team-category">
                        <h2 class="category-title">Жнецы Мрака</h2>
                        <div class="members-grid">
                            <div class="member-card halloween-card vacant">
                                <div class="member-avatar"><i class="fas fa-user-plus"></i></div>
                                <div class="member-rank">Жнец Мрака</div>
                                <div class="member-name">[Вакантно]</div>
                                <div class="member-role">Боец<br></div>
                            </div>
                            
                            <div class="member-card halloween-card vacant">
                                <div class="member-avatar"><i class="fas fa-user-plus"></i></div>
                                <div class="member-rank">Жнец Мрака</div>
                                <div class="member-name">[Вакантно]</div>
                                <div class="member-role">Боец<br></div>
                            </div>
                            
                            <div class="member-card halloween-card vacant">
                                <div class="member-avatar"><i class="fas fa-user-plus"></i></div>
                                <div class="member-rank">Жнец Мрака</div>
                                <div class="member-name">[Вакантно]</div>
                                <div class="member-role">Боец<br></div>
                            </div>
                            
                            <div class="member-card halloween-card vacant">
                                <div class="member-avatar"><i class="fas fa-user-plus"></i></div>
                                <div class="member-rank">Жнец Мрака</div>
                                <div class="member-name">[Вакантно]</div>
                                <div class="member-role">Боец<br></div>
                            </div>
                            
                            <div class="member-card halloween-card vacant">
                                <div class="member-avatar"><i class="fas fa-user-plus"></i></div>
                                <div class="member-rank">Жнец Мрака</div>
                                <div class="member-name">[Вакантно]</div>
                                <div class="member-role">Боец<br></div>
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
                        Путь от Демона к Цукумону через накопление Кровавых Монет 
                    </p>
                </div>

                <div class="features-grid">
                    <!-- Система получения Кровавых Монет -->
                    <div class="feature-card halloween-card">
                        <div class="feature-icon">
                            <i class="fas fa-coins"></i>
                        </div>
                        <h3>Получение Кровавых Монет</h3>
                        <div class="matter-system">
                            <div class="matter-category">
                                <h4>Боевые действия</h4>
                                <ul>
                                    <li>Убийство 1 истребителя ➤ <span class="matter-amount">1 Кровавая Монета</span></li>
                                    <li>Убийство 1 столпа ➤ <span class="matter-amount">2 Кровавые Монеты</span></li>
                                    <li>Продолжительный захват точки ➤ <span class="matter-amount">3 Кровавых Монет</span></li>
                                    <li>Захват обычной точеки ➤ <span class="matter-amount">1 Кровавые Монеты</span></li>
                                    <li>Участие в ГРП ➤ <span class="matter-amount">5 Кровавых Монет</span></li>
                                </ul>
                            </div>
                            
                            <div class="matter-category">
                                <h4>Задания</h4>
                                <ul>
                                    <li>Инструктора Мрака ➤ <span class="matter-amount">2-5 Кровавые Монеты</span></li>
                                    <li>Старшего Жнеца ➤ <span class="matter-amount">5-7 Кровавых Монет</span></li>
                                    <li>Мрачной Жницы ➤ <span class="matter-amount">10 Кровавых Монет</span></li>
                                    <li>Низшей луны ➤ <span class="matter-amount">5 Кровавых Монет</span></li>
                                    <li>Высшей луны ➤ <span class="matter-amount">7 Кровавых Монет</span></li>
                                </ul>
                            </div>
                            
                            <div class="matter-category">
                                <h4>Тренировки и мероприятия</h4>
                                <ul>
                                    <li>Проведение тренировки ➤ <span class="matter-amount">3 Кровавые Монеты</span></li>
                                    <li>Участие в тренировке ➤ <span class="matter-amount">2 Кровавые Монеты</span></li>
                                    <li>Участие в мероприятии ➤ <span class="matter-amount">4 Кровавые Монеты</span></li>
                                </ul>
                            </div>
                            
                            <div class="matter-category">
                                <h4>Почтения</h4>
                                <ul>
                                    <li>1 степень ➤ <span class="matter-amount">5+ Кровавых Монет</span></li>
                                    <li>2 степень ➤ <span class="matter-amount">10+ Кровавых Монет</span></li>
                                    <li>3 степень ➤ <span class="matter-amount">15+ Кровавых Монет</span></li>
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
                                    <div class="rank-requirements">КД: 2 день</div>
                                </div>
                                <div class="rank-matter">5 Кровавых Монет</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Demon ➤ Keykon</div>
                                    <div class="rank-requirements">КД: 2 день</div>
                                </div>
                                <div class="rank-matter">10 Кровавых Монет</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Keykon ➤ Hofuma</div>
                                    <div class="rank-requirements">КД: 3 дня</div>
                                </div>
                                <div class="rank-matter">15 Кровавых Монет</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Hofuma ➤ Chisuma</div>
                                    <div class="rank-requirements">КД: 3 дня</div>
                                </div>
                                <div class="rank-matter">20 Кровавых Монет</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Chisuma ➤ Chikuma</div>
                                    <div class="rank-requirements">КД: 3 дня</div>
                                </div>
                                <div class="rank-matter">25 Кровавых Монет</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Chikuma ➤ Asakuma</div>
                                    <div class="rank-requirements">КД: 3 дня</div>
                                </div>
                                <div class="rank-matter">30 Кровавых Монет</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Asakuma ➤ Hobura</div>
                                    <div class="rank-requirements">КД: 4 дня</div>
                                </div>
                                <div class="rank-matter">35 Кровавых Монет</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Hobura ➤ Shateigashira</div>
                                    <div class="rank-requirements">КД: 4 дня</div>
                                </div>
                                <div class="rank-matter">40 Кровавых Монет</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Shateigashira ➤ Wakagashira</div>
                                    <div class="rank-requirements">КД: 4 дня</div>
                                </div>
                                <div class="rank-matter">45 Кровавых Монет</div>
                            </div>
                            
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Wakagashira ➤ Tsukumon</div>
                                    <div class="rank-requirements">КД: 4 дня</div>
                                </div>
                                <div class="rank-matter">50 Кровавых Монет</div>
                            </div>
                            <div class="rank-card">
                                <div class="rank-info">
                                    <div class="rank-name">Tsukumon ➤ Shiko</div>
                                    <div class="rank-requirements">КД: 4 дня</div>
                                </div>
                                <div class="rank-matter">55 Кровавых Монет + Одобрение Мудзана</div>
                            </div>  
                            
                        </div>
                        
                        <div class="progression-note">
                            <h4>Важная информация</h4>
                            <p>Учет Кровавых Монет ведется самостоятельно. В отчет о повышении прикладывайте скриншоты ваших действий.</p>
                            <p style="margin-top: 10px; font-size: 0.9em;">Кровавые Монеты можно выкупить за Йены у Старших Жнецов Мрака+</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="footer">
            <p>© 2025 Отряд Мрак | s5.yufu.su:27017</p>
            <p style="margin-top: 10px; font-size: 0.9em;">Мрак • Сила • Тайна • 🎄 Новый год 🎄</p>
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
<script>
(function() {
    'use strict';
    
    // Конфигурация
    const config = {
        count: 1000,                // Количество снежинок
        speed: 1.5,               // Скорость падения
        sizeMin: 2,               // Минимальный размер
        sizeMax: 8,               // Максимальный размер
        wind: 0.3,                // Сила ветра
        color: '#ffffff',         // Цвет снежинок
        opacityMin: 0.3,          // Минимальная прозрачность
        opacityMax: 0.9,          // Максимальная прозрачность
        zIndex: 9999              // z-index для снежинок
    };
    
    let snowflakes = [];
    let animationId = null;
    
    // Создание стилей для снежинок
    const style = document.createElement('style');
    style.textContent = `
        .snowflake-js {
            position: fixed;
            background-color: ${config.color};
            border-radius: 50%;
            pointer-events: none;
            box-shadow: 0 0 5px rgba(255, 255, 255, 0.5);
            z-index: ${config.zIndex};
            opacity: 0;
            transition: opacity 0.5s ease;
        }
        .snowflake-js.visible {
            opacity: var(--opacity);
        }
        .snowflake-controls {
            position: fixed;
            bottom: 10px;
            right: 10px;
            z-index: ${config.zIndex + 1};
            background: rgba(0, 0, 0, 0.7);
            color: white;
            padding: 8px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-family: Arial, sans-serif;
            display: flex;
            align-items: center;
            gap: 8px;
            backdrop-filter: blur(5px);
        }
        .snowflake-toggle {
            background: #4CAF50;
            border: none;
            color: white;
            padding: 4px 10px;
            border-radius: 15px;
            cursor: pointer;
            font-size: 11px;
            transition: background 0.3s;
        }
        .snowflake-toggle:hover {
            background: #45a049;
        }
        .snowflake-toggle.paused {
            background: #f44336;
        }
    `;
    document.head.appendChild(style);
    
    // Создание снежинок
    function createSnowflakes() {
        for (let i = 0; i < config.count; i++) {
            createSnowflake();
        }
    }
    
    // Создание одной снежинки
    function createSnowflake() {
        const snowflake = document.createElement('div');
        snowflake.className = 'snowflake-js';
        
        const size = random(config.sizeMin, config.sizeMax);
        const opacity = random(config.opacityMin, config.opacityMax);
        
        snowflake.style.width = `${size}px`;
        snowflake.style.height = `${size}px`;
        snowflake.style.setProperty('--opacity', opacity);
        snowflake.style.left = `${random(0, window.innerWidth)}px`;
        snowflake.style.top = `${random(-100, -10)}px`;
        
        document.body.appendChild(snowflake);
        
        // Делаем снежинку видимой после добавления в DOM
        setTimeout(() => snowflake.classList.add('visible'), 10);
        
        snowflakes.push({
            element: snowflake,
            x: parseFloat(snowflake.style.left),
            y: parseFloat(snowflake.style.top),
            speed: random(config.speed * 0.7, config.speed * 1.3),
            wind: random(-config.wind, config.wind),
            swing: random(0, Math.PI * 2),
            swingSpeed: random(0.01, 0.03),
            size: size
        });
    }
    
    // Анимация
    function animate() {
        snowflakes.forEach(snowflake => {
            snowflake.y += snowflake.speed;
            snowflake.x += snowflake.wind;
            
            // Добавляем легкие колебания
            snowflake.swing += snowflake.swingSpeed;
            snowflake.x += Math.sin(snowflake.swing) * 0.3;
            
            // Проверка границ
            if (snowflake.y > window.innerHeight) {
                resetSnowflake(snowflake);
            }
            
            if (snowflake.x > window.innerWidth + 20) {
                snowflake.x = -20;
            } else if (snowflake.x < -20) {
                snowflake.x = window.innerWidth + 20;
            }
            
            // Обновление позиции
            snowflake.element.style.transform = `translate3d(${snowflake.x}px, ${snowflake.y}px, 0)`;
        });
        
        animationId = requestAnimationFrame(animate);
    }
    
    // Сброс снежинки
    function resetSnowflake(snowflake) {
        snowflake.y = random(-100, -10);
        snowflake.x = random(0, window.innerWidth);
        snowflake.speed = random(config.speed * 0.7, config.speed * 1.3);
        snowflake.wind = random(-config.wind, config.wind);
    }
    
    // Вспомогательная функция для случайных чисел
    function random(min, max) {
        return Math.random() * (max - min) + min;
    }
    
    // Обработка изменения размера окна
    function handleResize() {
        snowflakes.forEach(snowflake => {
            if (snowflake.x > window.innerWidth) {
                snowflake.x = window.innerWidth - 10;
            }
        });
    }
    
    // Создание элементов управления
    function createControls() {
        const controls = document.createElement('div');
        controls.className = 'snowflake-controls';
        
        const toggleBtn = document.createElement('button');
        toggleBtn.className = 'snowflake-toggle';
        toggleBtn.textContent = '❄️ Снег';
        toggleBtn.title = 'Включить/выключить снег';
        
        const countSpan = document.createElement('span');
        countSpan.textContent = `${config.count}❄️`;
        
        controls.appendChild(toggleBtn);
        controls.appendChild(countSpan);
        document.body.appendChild(controls);
        
        // Обработчик клика
        toggleBtn.addEventListener('click', function() {
            if (animationId) {
                cancelAnimationFrame(animationId);
                animationId = null;
                this.classList.add('paused');
                this.textContent = '⛄ Снег';
            } else {
                animate();
                this.classList.remove('paused');
                this.textContent = '❄️ Снег';
            }
        });
    }
    
    // Инициализация
    function init() {
        createSnowflakes();
        createControls();
        animate();
        
        window.addEventListener('resize', handleResize);
        window.addEventListener('beforeunload', () => {
            if (animationId) cancelAnimationFrame(animationId);
        });
    }
    
    // Запуск при полной загрузке страницы
    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', init);
    } else {
        init();
    }
    
})();
</script>

<script>
// Прорисованные векторные снежинки
(function() {
    'use strict';
    
    // Настройки
    const config = {
        // Количество и плотность
        count: 45,
        density: 1.0,
        
        // Размеры
        size: {
            min: 15,
            max: 45,
            scale: 0.8 // Коэффициент масштабирования (0.5-1.5)
        },
        
        // Движение
        speed: {
            base: 0.8,
            variance: 0.6
        },
        wind: {
            base: 0.15,
            variance: 0.2,
            changeRate: 0.001
        },
        
        // Вращение
        rotation: {
            enabled: true,
            speed: { min: -0.3, max: 0.3 },
            wobble: 0.08
        },
        
        // Внешний вид
        opacity: { min: 0.3, max: 0.85 },
        strokeWidth: { min: 0.8, max: 1.5 },
        color: {
            base: '#ffffff',
            variants: [
                'rgba(255, 255, 255, 1)',
                'rgba(240, 248, 255, 1)', // AliceBlue
                'rgba(230, 240, 255, 1)', // Очень светлый голубой
                'rgba(255, 250, 240, 1)'  // FloralWhite
            ]
        },
        
        // Сложность узоров
        complexity: { min: 4, max: 8 }, // Количество лучей
        detail: { min: 1, max: 3 }, // Уровень детализации
        
        // Эффекты
        glow: true,
        sparkle: true,
        twinkle: true,
        
        // Производительность
        fpsLimit: 60,
        lazyLoad: true,
        
        // z-index
        zIndex: 9998
    };
    
    let snowflakes = [];
    let animationId = null;
    let lastTime = 0;
    let windDirection = 0;
    
    // Создание стилей
    const style = document.createElement('style');
    style.textContent = `
        .art-snowflake {
            position: fixed;
            pointer-events: none;
            z-index: ${config.zIndex};
            opacity: 0;
            transform-origin: center;
            will-change: transform, opacity;
            transition: opacity 2s ease-out;
            filter: drop-shadow(0 0 1px rgba(255, 255, 255, 0.3));
        }
        
        .art-snowflake svg {
            width: 100%;
            height: 100%;
            filter: var(--filter);
        }
        
        .art-snowflake.visible {
            opacity: var(--opacity);
        }
        
        /* Эффекты свечения */
        .art-snowflake.glow svg {
            filter: drop-shadow(0 0 2px rgba(255, 255, 255, 0.4));
        }
        
        /* Мерцание */
        .art-snowflake.sparkle {
            animation: gentle-sparkle 4s infinite ease-in-out;
        }
        
        /* Переливчатость */
        .art-snowflake.twinkle {
            animation: subtle-twinkle 6s infinite alternate;
        }
        
        /* Анимации */
        @keyframes gentle-sparkle {
            0%, 100% { opacity: var(--opacity); }
            50% { opacity: calc(var(--opacity) * 1.3); }
        }
        
        @keyframes subtle-twinkle {
            0% { filter: drop-shadow(0 0 1px rgba(255, 255, 255, 0.3)) brightness(0.95); }
            100% { filter: drop-shadow(0 0 3px rgba(255, 255, 255, 0.5)) brightness(1.05); }
        }
        
        /* Эффект кристалла */
        .art-snowflake.crystal {
            filter: drop-shadow(0 0 2px rgba(255, 255, 255, 0.5));
        }
        
        /* Фоновый градиент для зимней атмосферы */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: 
                radial-gradient(
                    ellipse at 20% 20%,
                    rgba(135, 206, 235, 0.03) 0%,
                    transparent 50%
                ),
                radial-gradient(
                    ellipse at 80% 80%,
                    rgba(176, 224, 230, 0.02) 0%,
                    transparent 50%
                );
            pointer-events: none;
            z-index: ${config.zIndex - 10};
            mix-blend-mode: overlay;
        }
    `;
    
    document.head.appendChild(style);
    
    // Вспомогательные функции
    function random(min, max) {
        return Math.random() * (max - min) + min;
    }
    
    function randomInt(min, max) {
        return Math.floor(random(min, max));
    }
    
    function randomChoice(array) {
        return array[randomInt(0, array.length)];
    }
    
    // Генерация SVG снежинки
    function generateSnowflakeSVG(size, complexity, detailLevel, color, strokeWidth) {
        const center = size / 2;
        const radius = size / 2 * 0.9;
        const rays = complexity;
        const angleStep = (2 * Math.PI) / rays;
        
        let pathData = '';
        
        // Основные лучи
        for (let i = 0; i < rays; i++) {
            const angle = i * angleStep;
            const endX = center + Math.cos(angle) * radius;
            const endY = center + Math.sin(angle) * radius;
            
            // Основной луч
            pathData += `M ${center} ${center} L ${endX} ${endY} `;
            
            // Боковые ветви на основном луче
            for (let branch = 1; branch <= detailLevel; branch++) {
                const branchPos = 0.3 + (branch / (detailLevel + 1)) * 0.5;
                const branchX = center + Math.cos(angle) * radius * branchPos;
                const branchY = center + Math.sin(angle) * radius * branchPos;
                const branchLength = radius * 0.15 * (1 - branch * 0.2);
                
                // Правая ветвь
                const branchAngle1 = angle + Math.PI / 6;
                const branchEndX1 = branchX + Math.cos(branchAngle1) * branchLength;
                const branchEndY1 = branchY + Math.sin(branchAngle1) * branchLength;
                pathData += `M ${branchX} ${branchY} L ${branchEndX1} ${branchEndY1} `;
                
                // Левая ветвь
                const branchAngle2 = angle - Math.PI / 6;
                const branchEndX2 = branchX + Math.cos(branchAngle2) * branchLength;
                const branchEndY2 = branchY + Math.sin(branchAngle2) * branchLength;
                pathData += `M ${branchX} ${branchY} L ${branchEndX2} ${branchEndY2} `;
                
                // Дополнительные маленькие веточки для большего уровня детализации
                if (detailLevel >= 2 && branch === 1) {
                    const smallBranchLength = branchLength * 0.6;
                    
                    const smallAngle1 = angle + Math.PI / 4;
                    const smallEndX1 = branchX + Math.cos(smallAngle1) * smallBranchLength;
                    const smallEndY1 = branchY + Math.sin(smallAngle1) * smallBranchLength;
                    pathData += `M ${branchX} ${branchY} L ${smallEndX1} ${smallEndY1} `;
                    
                    const smallAngle2 = angle - Math.PI / 4;
                    const smallEndX2 = branchX + Math.cos(smallAngle2) * smallBranchLength;
                    const smallEndY2 = branchY + Math.sin(smallAngle2) * smallBranchLength;
                    pathData += `M ${branchX} ${branchY} L ${smallEndX2} ${smallEndY2} `;
                }
            }
            
            // Внутренние украшения на кончике луча
            if (detailLevel >= 2) {
                const tipX = endX;
                const tipY = endY;
                const decorationSize = radius * 0.08;
                
                // Кружок на кончике
                pathData += `M ${tipX} ${tipY} m -${decorationSize}, 0 a ${decorationSize},${decorationSize} 0 1,0 ${decorationSize*2},0 a ${decorationSize},${decorationSize} 0 1,0 -${decorationSize*2},0 `;
                
                // Маленькие ответвления перед кончиком
                const preTipPos = 0.85;
                const preTipX = center + Math.cos(angle) * radius * preTipPos;
                const preTipY = center + Math.sin(angle) * radius * preTipPos;
                const smallTipLength = radius * 0.07;
                
                const smallAngle1 = angle + Math.PI / 3;
                const smallTipX1 = preTipX + Math.cos(smallAngle1) * smallTipLength;
                const smallTipY1 = preTipY + Math.sin(smallAngle1) * smallTipLength;
                pathData += `M ${preTipX} ${preTipY} L ${smallTipX1} ${smallTipY1} `;
                
                const smallAngle2 = angle - Math.PI / 3;
                const smallTipX2 = preTipX + Math.cos(smallAngle2) * smallTipLength;
                const smallTipY2 = preTipY + Math.sin(smallAngle2) * smallTipLength;
                pathData += `M ${preTipX} ${preTipY} L ${smallTipX2} ${smallTipY2} `;
            }
        }
        
        // Внутренний шестиугольник/круг
        const innerShapeRadius = radius * 0.2;
        if (detailLevel >= 2) {
            // Шестиугольник
            for (let i = 0; i < 6; i++) {
                const angle = i * (Math.PI / 3);
                const x1 = center + Math.cos(angle) * innerShapeRadius;
                const y1 = center + Math.sin(angle) * innerShapeRadius;
                const x2 = center + Math.cos(angle + Math.PI / 3) * innerShapeRadius;
                const y2 = center + Math.sin(angle + Math.PI / 3) * innerShapeRadius;
                pathData += `M ${x1} ${y1} L ${x2} ${y2} `;
            }
        } else {
            // Простой круг
            pathData += `M ${center} ${center} m -${innerShapeRadius}, 0 a ${innerShapeRadius},${innerShapeRadius} 0 1,0 ${innerShapeRadius*2},0 a ${innerShapeRadius},${innerShapeRadius} 0 1,0 -${innerShapeRadius*2},0 `;
        }
        
        // Точки на пересечениях
        if (detailLevel >= 3) {
            const dotRadius = radius * 0.03;
            for (let i = 0; i < rays; i++) {
                const angle = i * angleStep;
                for (let dotPos = 0.4; dotPos <= 0.7; dotPos += 0.15) {
                    const dotX = center + Math.cos(angle) * radius * dotPos;
                    const dotY = center + Math.sin(angle) * radius * dotPos;
                    pathData += `M ${dotX} ${dotY} m -${dotRadius}, 0 a ${dotRadius},${dotRadius} 0 1,0 ${dotRadius*2},0 a ${dotRadius},${dotRadius} 0 1,0 -${dotRadius*2},0 `;
                }
            }
        }
        
        return `
            <svg viewBox="0 0 ${size} ${size}" xmlns="http://www.w3.org/2000/svg">
                <path d="${pathData}" 
                      stroke="${color}" 
                      stroke-width="${strokeWidth}" 
                      stroke-linecap="round" 
                      stroke-linejoin="round" 
                      fill="none"
                      stroke-opacity="0.9"/>
            </svg>
        `;
    }
    
    // Создание снежинок
    function createSnowflakes() {
        let created = 0;
        
        function createBatch() {
            const batchSize = Math.min(8, config.count - created);
            
            for (let i = 0; i < batchSize; i++) {
                createSnowflake();
                created++;
            }
            
            if (created < config.count) {
                setTimeout(createBatch, 200);
            }
        }
        
        createBatch();
    }
    
    function createSnowflake() {
        const snowflake = document.createElement('div');
        snowflake.className = 'art-snowflake';
        
        // Параметры снежинки
        const size = random(config.size.min, config.size.max) * config.size.scale;
        const opacity = random(config.opacity.min, config.opacity.max);
        const color = randomChoice(config.color.variants);
        const strokeWidth = random(config.strokeWidth.min, config.strokeWidth.max);
        const complexity = randomInt(config.complexity.min, config.complexity.max);
        const detailLevel = randomInt(config.detail.min, config.detail.max);
        
        // Генерация уникальной снежинки
        const svgHTML = generateSnowflakeSVG(size, complexity, detailLevel, color, strokeWidth);
        
        // Устанавливаем стили
        snowflake.style.cssText = `
            width: ${size}px;
            height: ${size}px;
            left: ${random(-50, window.innerWidth + 50)}px;
            top: ${random(-100, -20)}px;
            --opacity: ${opacity};
        `;
        
        snowflake.innerHTML = svgHTML;
        
        // Добавляем эффекты
        if (config.glow) snowflake.classList.add('glow');
        if (config.sparkle) snowflake.classList.add('sparkle');
        if (config.twinkle && Math.random() > 0.5) snowflake.classList.add('twinkle');
        if (detailLevel >= 2) snowflake.classList.add('crystal');
        
        document.body.appendChild(snowflake);
        
        // Физические параметры
        const velocity = {
            x: random(-0.3, 0.3),
            y: random(0.3, 0.8)
        };
        
        // Данные снежинки
        snowflakes.push({
            element: snowflake,
            x: parseFloat(snowflake.style.left),
            y: parseFloat(snowflake.style.top),
            size: size,
            velocity: velocity,
            rotation: random(0, 360),
            rotationSpeed: config.rotation.enabled ? 
                random(config.rotation.speed.min, config.rotation.speed.max) : 0,
            wobble: random(0, Math.PI * 2),
            wobbleSpeed: random(0.02, 0.06),
            opacity: opacity,
            complexity: complexity,
            windResistance: random(0.8, 1.2) // Сопротивление ветру
        });
        
        // Плавное появление
        setTimeout(() => {
            snowflake.classList.add('visible');
        }, random(0, 800));
    }
    
    // Анимация
    function animate(currentTime) {
        if (!lastTime) lastTime = currentTime;
        const deltaTime = Math.min(currentTime - lastTime, 100);
        
        // Плавное изменение ветра
        windDirection += random(-config.wind.changeRate, config.wind.changeRate);
        const currentWind = Math.sin(windDirection) * config.wind.base + 
                           random(-config.wind.variance, config.wind.variance);
        
        // Обновление каждой снежинки
        snowflakes.forEach((flake) => {
            // Применяем гравитацию с небольшим ускорением
            flake.velocity.y = Math.min(flake.velocity.y + 0.001, 1.2);
            
            // Применяем ветер с учетом сопротивления
            flake.velocity.x = (flake.velocity.x + currentWind / flake.windResistance) * 0.99;
            
            // Колебания
            flake.wobble += flake.wobbleSpeed;
            flake.velocity.x += Math.sin(flake.wobble) * config.rotation.wobble;
            
            // Обновление позиции
            flake.x += flake.velocity.x * (deltaTime / 16);
            flake.y += flake.velocity.y * (deltaTime / 16);
            
            // Вращение
            flake.rotation += flake.rotationSpeed;
            
            // Проверка границ
            if (flake.y > window.innerHeight + 50) {
                resetSnowflake(flake);
            }
            
            if (flake.x > window.innerWidth + 60) {
                flake.x = -60;
            } else if (flake.x < -60) {
                flake.x = window.innerWidth + 60;
            }
            
            // Обновление отображения
            flake.element.style.transform = 
                `translate(${flake.x}px, ${flake.y}px) rotate(${flake.rotation}deg)`;
            
            // Легкое изменение прозрачности при движении
            const speed = Math.sqrt(flake.velocity.x * flake.velocity.x + 
                                  flake.velocity.y * flake.velocity.y);
            const opacityVariation = Math.sin(currentTime / 1000 + flake.x * 0.01) * 0.1;
            flake.element.style.opacity = Math.min(1, 
                flake.opacity * (0.9 + speed * 0.1 + opacityVariation));
        });
        
        lastTime = currentTime;
        animationId = requestAnimationFrame(animate);
    }
    
    function resetSnowflake(flake) {
        flake.y = random(-100, -30);
        flake.x = random(-50, window.innerWidth + 50);
        
        // Сохраняем часть горизонтальной скорости для непрерывности
        flake.velocity.x *= 0.5;
        flake.velocity.y = random(0.3, 0.8);
        
        // Случайное изменение скорости вращения
        flake.rotationSpeed = random(config.rotation.speed.min, config.rotation.speed.max);
        
        // Плавное появление
        flake.element.classList.remove('visible');
        setTimeout(() => {
            flake.element.classList.add('visible');
        }, 300);
    }
    
    // Обработка изменения размера окна
    function handleResize() {
        snowflakes.forEach(flake => {
            if (flake.x > window.innerWidth) {
                flake.x = window.innerWidth - 20;
            }
            if (flake.x < -20) {
                flake.x = window.innerWidth + 20;
            }
        });
    }
    
    // Автоматическая пауза при скрытии вкладки
    function handleVisibilityChange() {
        if (document.hidden) {
            // Плавное уменьшение прозрачности
            snowflakes.forEach(flake => {
                flake.element.style.transition = 'opacity 1s ease';
                flake.element.style.opacity = '0.2';
            });
            
            if (animationId) {
                cancelAnimationFrame(animationId);
                animationId = null;
            }
        } else {
            // Плавное восстановление
            snowflakes.forEach(flake => {
                flake.element.style.opacity = '';
                setTimeout(() => {
                    flake.element.style.transition = '';
                }, 1000);
            });
            
            lastTime = performance.now();
            animationId = requestAnimationFrame(animate);
        }
    }
    
    // Создание фоновых эффектов
    function createBackgroundEffects() {
        // Эффект легкой дымки
        const haze = document.createElement('div');
        haze.style.cssText = `
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: 
                radial-gradient(
                    circle at 20% 30%,
                    rgba(255, 255, 255, 0.02) 0%,
                    transparent 40%
                ),
                radial-gradient(
                    circle at 80% 70%,
                    rgba(230, 240, 255, 0.015) 0%,
                    transparent 40%
                );
            pointer-events: none;
            z-index: ${config.zIndex - 5};
            mix-blend-mode: screen;
            animation: gentle-drift 40s infinite linear;
        `;
        
        const hazeStyle = document.createElement('style');
        hazeStyle.textContent = `
            @keyframes gentle-drift {
                0% { transform: translate(0, 0) scale(1); }
                33% { transform: translate(1%, 1%) scale(1.01); }
                66% { transform: translate(-1%, -1%) scale(0.99); }
                100% { transform: translate(0, 0) scale(1); }
            }
        `;
        
        document.head.appendChild(hazeStyle);
        document.body.appendChild(haze);
    }
    
    // Инициализация
    function init() {
        // Только в зимние месяцы
        const month = new Date().getMonth() + 1;
        if (month !== 12 && month !== 1 && month !== 2) return;
        
        createBackgroundEffects();
        createSnowflakes();
        
        lastTime = performance.now();
        animationId = requestAnimationFrame(animate);
        
        // Настройка событий
        window.addEventListener('resize', handleResize);
        document.addEventListener('visibilitychange', handleVisibilityChange);
        
        // Периодическое обновление для разнообразия
        setInterval(() => {
            if (snowflakes.length < config.count * 0.9 && Math.random() > 0.7) {
                createSnowflake();
            }
        }, 5000);
    }
    
    // Запуск
    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', init);
    } else {
        init();
    }
})();
</script>

<!-- Дополнительные стили для красоты -->
<style>
    /* Улучшение контраста текста */
    body {
        position: relative;
    }
    
    /* Эффект легкого свечения вокруг текста */
    h1, h2, h3, h4, h5, h6 {
        position: relative;
        z-index: ${config?.zIndex + 1 || 10000};
    }
    
    /* Эффект кристаллизации для изображений */
    img {
        transition: filter 0.5s ease;
    }
    
    img:hover {
        filter: brightness(1.05) contrast(1.02);
    }
    
    /* Легкий эффект мороза для контента */
    .content-wrapper, main, article {
        position: relative;
    }
    
    .content-wrapper::after, main::after, article::after {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: 
            linear-gradient(
                45deg,
                transparent 48%,
                rgba(255, 255, 255, 0.01) 50%,
                transparent 52%
            ),
            linear-gradient(
                -45deg,
                transparent 48%,
                rgba(255, 255, 255, 0.01) 50%,
                transparent 52%
            );
        background-size: 20px 20px;
        pointer-events: none;
        z-index: 1;
        opacity: 0.1;
        mix-blend-mode: overlay;
    }
    
    /* Эффект для ссылок */
    a {
        position: relative;
        transition: all 0.3s ease;
    }
    
    a:hover {
        text-shadow: 0 0 8px rgba(135, 206, 235, 0.3);
    }
    
    /* Эффект для кнопок */
    button:not([class*="snow"]) {
        position: relative;
        overflow: hidden;
    }
    
    button:not([class*="snow"])::after {
        content: '❄';
        position: absolute;
        right: 8px;
        top: 50%;
        transform: translateY(-50%);
        font-size: 12px;
        opacity: 0;
        transition: opacity 0.3s ease;
    }
    
    button:not([class*="snow"]):hover::after {
        opacity: 0.5;
    }
</style>
    
</body>
</html>

