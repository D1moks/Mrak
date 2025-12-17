
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
                        <p>Путь от Демона к Шико через накопление Кровавых Монет. Узнай как повысить свой ранг в братстве.</p>
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
// Реалистичные снежинки без кнопок
(function() {
    'use strict';
    
    // Проверяем, что мы в зимний период (декабрь-февраль)
    const now = new Date();
    const month = now.getMonth() + 1; // 1-12
    const isWinter = month === 12 || month === 1 || month === 2;
    if (!isWinter) return;
    
    // Конфигурация
    const config = {
        // Количество и распределение
        count: 85,
        density: 1.2, // Плотность (влияет на распределение)
        
        // Физика снежинок
        gravity: 0.1,       // Гравитация
        mass: 0.05,         // Масса для инерции
        airResistance: 0.95, // Сопротивление воздуха
        
        // Размеры
        size: {
            min: 1.5,
            max: 6,
            distribution: 2.5 // Коэффициент распределения (чем больше, тем больше маленьких)
        },
        
        // Ветер и турбулентность
        wind: {
            base: 0.15,
            variance: 0.25,
            gusts: {
                enabled: true,
                frequency: 0.003, // Частота порывов
                strength: 1.8     // Сила порывов
            },
            turbulence: 0.12      // Турбулентность
        },
        
        // Вращение и колебания
        rotation: {
            enabled: true,
            speed: { min: -0.8, max: 0.8 },
            wobble: 0.15 // Дрожание
        },
        
        // Внешний вид
        appearance: {
            blur: true,
            blurAmount: { min: 0.1, max: 0.4 },
            glow: true,
            glowIntensity: { min: 0.3, max: 0.7 },
            opacity: { min: 0.4, max: 0.92 },
            colorVariation: 0.1 // Вариация цвета (0-1)
        },
        
        // Формы снежинок
        shapes: [
            'circle',      // Простые круглые
            'soft',        // Мягкие размытые
            'crystal',     // Кристаллические
            'fluffy'       // Пушистые
        ],
        
        // z-index
        zIndex: 9998,
        
        // Производительность
        fpsLimit: 60,
        lazyLoad: true,    // Постепенная загрузка
        lazyLoadDelay: 100 // Задержка между созданием
    };
    
    let snowflakes = [];
    let animationId = null;
    let lastTime = 0;
    let windGust = 0;
    let windGustPhase = 0;
    let isAnimating = true;
    
    // Создание стилей
    const style = document.createElement('style');
    style.textContent = `
        .realistic-snowflake {
            position: fixed;
            pointer-events: none;
            z-index: ${config.zIndex};
            opacity: 0;
            transform-origin: center;
            will-change: transform, opacity;
            transition: opacity 2s cubic-bezier(0.4, 0, 0.2, 1);
            background: white;
        }
        
        .realistic-snowflake.visible {
            opacity: var(--opacity);
        }
        
        /* Формы снежинок */
        .realistic-snowflake.circle {
            border-radius: 50%;
        }
        
        .realistic-snowflake.soft {
            border-radius: 50%;
            filter: blur(var(--blur)) brightness(1.1);
            background: radial-gradient(
                ellipse at center,
                rgba(255, 255, 255, 0.9) 0%,
                rgba(255, 255, 255, 0.6) 40%,
                rgba(255, 255, 255, 0.2) 70%,
                transparent 100%
            );
        }
        
        .realistic-snowflake.crystal {
            border-radius: 50%;
            background: 
                radial-gradient(circle at 30% 30%, 
                    rgba(255, 255, 255, 0.95) 0%,
                    rgba(230, 240, 255, 0.8) 30%,
                    rgba(210, 225, 245, 0.6) 60%,
                    transparent 100%
                ),
                linear-gradient(45deg, 
                    transparent 45%,
                    rgba(255, 255, 255, 0.3) 50%,
                    transparent 55%
                ),
                linear-gradient(-45deg, 
                    transparent 45%,
                    rgba(255, 255, 255, 0.3) 50%,
                    transparent 55%
                );
            background-blend-mode: overlay;
        }
        
        .realistic-snowflake.fluffy {
            border-radius: 50%;
            filter: blur(var(--blur));
            background: 
                radial-gradient(circle at 20% 20%, 
                    rgba(255, 255, 255, 0.95) 0%,
                    rgba(240, 248, 255, 0.7) 25%,
                    rgba(230, 240, 250, 0.4) 50%,
                    transparent 70%
                ),
                radial-gradient(circle at 80% 80%, 
                    rgba(255, 255, 255, 0.8) 0%,
                    rgba(240, 248, 255, 0.5) 25%,
                    transparent 50%
                );
        }
        
        /* Эффект свечения */
        .realistic-snowflake.glow {
            filter: drop-shadow(0 0 1px rgba(255, 255, 255, 0.4)) var(--blur-effect);
            box-shadow: 0 0 var(--glow-size) rgba(255, 255, 255, var(--glow-intensity));
        }
        
        /* Анимации */
        @keyframes gentle-sparkle {
            0%, 100% { opacity: var(--opacity); }
            50% { opacity: calc(var(--opacity) * 1.2); }
        }
        
        .realistic-snowflake.sparkle {
            animation: gentle-sparkle 4s infinite ease-in-out;
            animation-delay: var(--sparkle-delay);
        }
        
        /* Эффект накопления на нижней границе */
        .snow-accumulation {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            height: 0;
            background: linear-gradient(to top, 
                rgba(255, 255, 255, 0.1) 0%,
                rgba(255, 255, 255, 0.05) 50%,
                transparent 100%
            );
            z-index: ${config.zIndex - 1};
            pointer-events: none;
            transition: height 10s ease;
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
    
    function randomGaussian(mean, std) {
        let u = 0, v = 0;
        while(u === 0) u = Math.random();
        while(v === 0) v = Math.random();
        return Math.sqrt(-2.0 * Math.log(u)) * Math.cos(2.0 * Math.PI * v) * std + mean;
    }
    
    function getSnowflakeSize() {
        // Распределение размеров по степенному закону (больше маленьких)
        const u = Math.random();
        return config.size.min + (config.size.max - config.size.min) * 
               Math.pow(u, config.size.distribution);
    }
    
    function getWind() {
        let wind = config.wind.base + random(-config.wind.variance, config.wind.variance);
        
        // Порывы ветра
        if (config.wind.gusts.enabled) {
            windGustPhase += config.wind.gusts.frequency;
            const gust = Math.sin(windGustPhase * 2 * Math.PI) * 
                        config.wind.gusts.strength * 
                        Math.random();
            
            // Случайные сильные порывы
            if (Math.random() < 0.001) {
                windGust = random(-config.wind.gusts.strength * 2, config.wind.gusts.strength * 2);
            }
            
            wind += gust + windGust;
            windGust *= 0.95; // Затухание порыва
        }
        
        return wind;
    }
    
    // Создание снежинок
    function createSnowflakes() {
        // Создаем эффект накопления снега
        const accumulation = document.createElement('div');
        accumulation.className = 'snow-accumulation';
        document.body.appendChild(accumulation);
        
        // Постепенное создание снежинок
        let created = 0;
        
        function createBatch() {
            const batchSize = Math.min(15, config.count - created);
            
            for (let i = 0; i < batchSize; i++) {
                createSnowflake();
                created++;
            }
            
            if (created < config.count) {
                setTimeout(createBatch, config.lazyLoadDelay);
            }
        }
        
        createBatch();
    }
    
    function createSnowflake() {
        const snowflake = document.createElement('div');
        
        // Выбор формы
        const shape = config.shapes[randomInt(0, config.shapes.length)];
        snowflake.className = `realistic-snowflake ${shape}`;
        
        // Размер
        const size = getSnowflakeSize();
        
        // Цвет и прозрачность
        const opacity = random(config.appearance.opacity.min, config.appearance.opacity.max);
        let color = 'rgba(255, 255, 255, 1)';
        
        if (config.appearance.colorVariation > 0) {
            const variation = random(-config.appearance.colorVariation, config.appearance.colorVariation);
            color = `rgba(${255 + variation * 50}, ${255 + variation * 30}, ${255 + variation * 10}, 1)`;
        }
        
        // Эффекты
        const blur = config.appearance.blur ? 
            random(config.appearance.blurAmount.min, config.appearance.blurAmount.max) : 0;
        
        const glow = config.appearance.glow ? 
            random(config.appearance.glowIntensity.min, config.appearance.glowIntensity.max) : 0;
        
        // Позиция (более реалистичное распределение)
        const x = random(-50, window.innerWidth + 50);
        const y = random(-200, -50);
        
        // Устанавливаем стили
        snowflake.style.cssText = `
            width: ${size}px;
            height: ${size}px;
            left: ${x}px;
            top: ${y}px;
            --opacity: ${opacity};
            --blur: ${blur}px;
            --blur-effect: ${config.appearance.blur ? `blur(${blur}px)` : 'none'};
            --glow-intensity: ${glow};
            --glow-size: ${size * 0.8}px;
            --sparkle-delay: ${random(0, 4)}s;
            background-color: ${color};
        `;
        
        // Эффекты
        if (config.appearance.glow) snowflake.classList.add('glow');
        if (Math.random() > 0.7) snowflake.classList.add('sparkle');
        
        document.body.appendChild(snowflake);
        
        // Физические свойства
        const velocity = {
            x: random(-0.5, 0.5),
            y: random(0.2, 0.5)
        };
        
        const acceleration = {
            x: 0,
            y: config.gravity
        };
        
        // Данные снежинки
        snowflakes.push({
            element: snowflake,
            x: x,
            y: y,
            size: size,
            mass: config.mass * (size / config.size.max),
            velocity: velocity,
            acceleration: acceleration,
            rotation: random(0, 360),
            rotationSpeed: config.rotation.enabled ? 
                random(config.rotation.speed.min, config.rotation.speed.max) : 0,
            wobble: random(0, Math.PI * 2),
            wobbleSpeed: random(0.02, 0.08),
            shape: shape,
            opacity: opacity,
            terminalVelocity: random(0.8, 1.5), // Максимальная скорость падения
            turbulence: random(0, Math.PI * 2)
        });
        
        // Плавное появление
        setTimeout(() => {
            snowflake.classList.add('visible');
        }, random(0, 1000));
    }
    
    // Физический движок
    function updatePhysics(deltaTime) {
        const wind = getWind();
        const timeFactor = deltaTime / 16.67; // Нормализация к 60 FPS
        
        snowflakes.forEach((flake, index) => {
            // Применяем гравитацию
            flake.acceleration.y = config.gravity;
            
            // Применяем ветер с учетом массы
            flake.acceleration.x = (wind / flake.mass) * timeFactor;
            
            // Турбулентность
            if (config.wind.turbulence > 0) {
                flake.turbulence += 0.05;
                flake.acceleration.x += Math.sin(flake.turbulence) * config.wind.turbulence * timeFactor;
            }
            
            // Колебания
            flake.wobble += flake.wobbleSpeed * timeFactor;
            flake.acceleration.x += Math.sin(flake.wobble) * config.rotation.wobble * timeFactor;
            
            // Обновляем скорость с учетом сопротивления воздуха
            flake.velocity.x = (flake.velocity.x + flake.acceleration.x) * config.airResistance;
            flake.velocity.y = (flake.velocity.y + flake.acceleration.y) * config.airResistance;
            
            // Ограничиваем максимальную скорость
            flake.velocity.y = Math.min(flake.velocity.y, flake.terminalVelocity);
            
            // Обновляем позицию
            flake.x += flake.velocity.x * timeFactor;
            flake.y += flake.velocity.y * timeFactor;
            
            // Обновляем вращение
            flake.rotation += flake.rotationSpeed * timeFactor;
            
            // Проверка границ
            if (flake.y > window.innerHeight + 20) {
                resetSnowflake(flake);
            }
            
            if (flake.x > window.innerWidth + 50) {
                flake.x = -50;
            } else if (flake.x < -50) {
                flake.x = window.innerWidth + 50;
            }
            
            // Обновляем элемент
            flake.element.style.transform = 
                `translate(${flake.x}px, ${flake.y}px) rotate(${flake.rotation}deg)`;
            
            // Легкое изменение прозрачности в зависимости от скорости
            const speedFactor = Math.abs(flake.velocity.y) / flake.terminalVelocity;
            flake.element.style.opacity = Math.min(flake.opacity, speedFactor * 1.5);
        });
    }
    
    function resetSnowflake(flake) {
        // Сохраняем часть горизонтальной скорости для реалистичности
        const horizontalMomentum = flake.velocity.x * 0.3;
        
        flake.y = random(-200, -50);
        flake.x = random(-50, window.innerWidth + 50);
        
        // Сброс физики
        flake.velocity = {
            x: horizontalMomentum + random(-0.3, 0.3),
            y: random(0.1, 0.4)
        };
        
        flake.acceleration = {
            x: 0,
            y: config.gravity
        };
        
        flake.rotation = random(0, 360);
        flake.rotationSpeed = config.rotation.enabled ? 
            random(config.rotation.speed.min, config.rotation.speed.max) : 0;
        
        flake.terminalVelocity = random(0.8, 1.5);
        
        // Плавное появление
        flake.element.classList.remove('visible');
        setTimeout(() => {
            flake.element.classList.add('visible');
        }, 100);
    }
    
    // Основной цикл анимации
    function animate(currentTime) {
        if (!isAnimating) return;
        
        // Ограничение FPS
        if (!lastTime) lastTime = currentTime;
        const deltaTime = currentTime - lastTime;
        
        if (deltaTime > 1000 / config.fpsLimit) {
            updatePhysics(deltaTime);
            lastTime = currentTime;
        }
        
        animationId = requestAnimationFrame(animate);
    }
    
    // Обработка изменения размера окна
    function handleResize() {
        // Плавное обновление позиций снежинок
        snowflakes.forEach(flake => {
            if (flake.x > window.innerWidth) {
                flake.x = window.innerWidth - 10;
            }
            if (flake.x < -10) {
                flake.x = window.innerWidth + 10;
            }
        });
        
        // Обновляем эффект накопления снега
        const accumulation = document.querySelector('.snow-accumulation');
        if (accumulation) {
            // Динамическая высота в зависимости от количества снежинок внизу
            const flakesAtBottom = snowflakes.filter(f => 
                f.y > window.innerHeight - 50
            ).length;
            
            const accumulationHeight = Math.min(30, flakesAtBottom * 0.3);
            accumulation.style.height = `${accumulationHeight}px`;
        }
    }
    
    // Автоматическая пауза при неактивной вкладке
    function handleVisibilityChange() {
        if (document.hidden) {
            isAnimating = false;
            if (animationId) {
                cancelAnimationFrame(animationId);
                animationId = null;
            }
        } else {
            isAnimating = true;
            lastTime = performance.now();
            animationId = requestAnimationFrame(animate);
        }
    }
    
    // Инициализация
    function init() {
        // Добавляем легкий зимний фон
        const winterOverlay = document.createElement('div');
        winterOverlay.style.cssText = `
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            pointer-events: none;
            z-index: ${config.zIndex - 2};
            background: linear-gradient(
                to bottom,
                rgba(135, 206, 235, 0.02) 0%,
                rgba(176, 224, 230, 0.01) 100%
            );
            mix-blend-mode: overlay;
        `;
        document.body.appendChild(winterOverlay);
        
        // Создаем снежинки
        createSnowflakes();
        
        // Запускаем анимацию
        lastTime = performance.now();
        animationId = requestAnimationFrame(animate);
        
        // Настройка событий
        window.addEventListener('resize', handleResize);
        document.addEventListener('visibilitychange', handleVisibilityChange);
        
        // Автоматическая адаптация производительности
        let frameCount = 0;
        let lastFpsCheck = performance.now();
        
        function monitorPerformance() {
            frameCount++;
            const now = performance.now();
            
            if (now - lastFpsCheck > 1000) {
                const fps = Math.round((frameCount * 1000) / (now - lastFpsCheck));
                
                // Автоматическое снижение количества снежинок при низком FPS
                if (fps < 30 && snowflakes.length > 30) {
                    // Плавно удаляем часть снежинок
                    const toRemove = Math.floor(snowflakes.length * 0.1);
                    for (let i = 0; i < toRemove; i++) {
                        const flake = snowflakes.pop();
                        if (flake && flake.element.parentNode) {
                            flake.element.style.opacity = '0';
                            setTimeout(() => {
                                if (flake.element.parentNode) {
                                    flake.element.parentNode.removeChild(flake.element);
                                }
                            }, 1000);
                        }
                    }
                }
                
                frameCount = 0;
                lastFpsCheck = now;
            }
            
            requestAnimationFrame(monitorPerformance);
        }
        
        monitorPerformance();
    }
    
    // Запуск
    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', init);
    } else {
        init();
    }
})();
</script>

<!-- Минимальный CSS для улучшения вида -->
<style>
    /* Легкие эффекты для улучшения восприятия снега */
    body::before {
        content: '';
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        pointer-events: none;
        background: 
            radial-gradient(
                circle at 20% 80%,
                rgba(255, 255, 255, 0.03) 0%,
                transparent 50%
            ),
            radial-gradient(
                circle at 80% 20%,
                rgba(255, 255, 255, 0.02) 0%,
                transparent 50%
            );
        z-index: 9997;
        animation: gentle-drift 60s infinite linear;
    }
    
    @keyframes gentle-drift {
        0% { transform: translate(0, 0); }
        25% { transform: translate(-1%, 1%); }
        50% { transform: translate(-1%, -1%); }
        75% { transform: translate(1%, -1%); }
        100% { transform: translate(0, 0); }
    }
    
    /* Эффект холодного стекла для контента */
    .content, article, main, .container {
        position: relative;
    }
    
    .content::after, article::after, main::after, .container::after {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: linear-gradient(
            to bottom,
            rgba(255, 255, 255, 0.01) 0%,
            rgba(240, 248, 255, 0.005) 100%
        );
        pointer-events: none;
        z-index: 1;
        mix-blend-mode: overlay;
    }
    
    /* Улучшение контраста для текста на фоне снега */
    h1, h2, h3, h4, h5, h6, p, li {
        text-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
    }
</style>
    
</body>
</html>

