<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>无敌鲨鱼大王 - 游戏世界</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        :root {
            --primary: #00f3ff;
            --secondary: #ff00ea;
            --dark: #0a0a1a;
            --darker: #050510;
            --light: #f0f8ff;
            --accent: #ff6b00;
        }

        body {
            background: linear-gradient(135deg, var(--darker), var(--dark));
            color: var(--light);
            overflow-x: hidden;
            line-height: 1.6;
        }

        /* 粒子背景效果 */
        #particles-js {
            position: fixed;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            z-index: -1;
        }

        /* 导航栏样式 */
        header {
            position: fixed;
            top: 0;
            width: 100%;
            z-index: 1000;
            background: rgba(10, 10, 26, 0.85);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid rgba(0, 243, 255, 0.3);
            padding: 15px 5%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.3s ease;
        }

        header.scrolled {
            padding: 10px 5%;
            background: rgba(10, 10, 26, 0.95);
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 1.8rem;
            font-weight: bold;
            color: var(--primary);
            text-shadow: 0 0 10px rgba(0, 243, 255, 0.7);
        }

        .logo i {
            color: var(--secondary);
        }

        nav ul {
            display: flex;
            list-style: none;
            gap: 30px;
        }

        nav a {
            color: var(--light);
            text-decoration: none;
            font-size: 1.1rem;
            font-weight: 500;
            padding: 8px 15px;
            border-radius: 5px;
            transition: all 0.3s ease;
            position: relative;
        }

        nav a:hover {
            color: var(--primary);
        }

        nav a::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--primary);
            transition: width 0.3s ease;
        }

        nav a:hover::after {
            width: 100%;
        }

        .mobile-menu-btn {
            display: none;
            background: transparent;
            border: none;
            color: var(--primary);
            font-size: 1.8rem;
            cursor: pointer;
        }

        /* 主内容区域 */
        main {
            margin-top: 80px;
        }

        section {
            min-height: 100vh;
            padding: 100px 10%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            position: relative;
        }

        .section-title {
            font-size: 3rem;
            margin-bottom: 50px;
            position: relative;
            display: inline-block;
        }

        .section-title::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 0;
            width: 100px;
            height: 4px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            border-radius: 2px;
        }

        /* 英雄区域样式 */
        .hero {
            text-align: center;
            background: linear-gradient(rgba(5, 5, 16, 0.9), rgba(5, 5, 16, 0.7)), url('https://images.unsplash.com/photo-1550745165-9bc0b252726f?ixlib=rb-4.0.3&auto=format&fit=crop&w=1950&q=80') no-repeat center center/cover;
            position: relative;
            overflow: hidden;
        }

        .hero-content {
            max-width: 900px;
            margin: 0 auto;
            position: relative;
            z-index: 10;
        }

        .hero h1 {
            font-size: 5rem;
            margin-bottom: 20px;
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            line-height: 1.1;
        }

        .hero h2 {
            font-size: 2.5rem;
            margin-bottom: 30px;
            color: var(--light);
            font-weight: 300;
        }

        .hero p {
            font-size: 1.4rem;
            margin-bottom: 40px;
            max-width: 700px;
            margin-left: auto;
            margin-right: auto;
        }

        .tagline {
            display: inline-block;
            padding: 8px 25px;
            background: rgba(0, 243, 255, 0.1);
            border: 1px solid var(--primary);
            border-radius: 30px;
            margin-bottom: 40px;
            font-size: 1.2rem;
            color: var(--primary);
            backdrop-filter: blur(5px);
        }

        .cta-button {
            display: inline-block;
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            border: none;
            padding: 15px 40px;
            font-size: 1.2rem;
            color: white;
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-decoration: none;
            margin-top: 20px;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(0, 243, 255, 0.4);
        }

        .cta-button:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 20px rgba(0, 243, 255, 0.6);
        }

        /* 关于我区域 */
        .about {
            background: var(--dark);
        }

        .about-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 50px;
            align-items: center;
        }

        .about-text h3 {
            font-size: 2.2rem;
            margin-bottom: 25px;
            color: var(--primary);
        }

        .about-text p {
            font-size: 1.2rem;
            margin-bottom: 20px;
            text-align: justify;
        }

        .game-list {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 30px;
        }

        .game-tag {
            padding: 8px 20px;
            background: rgba(255, 0, 234, 0.1);
            border: 1px solid var(--secondary);
            border-radius: 30px;
            font-size: 1.1rem;
            transition: all 0.3s ease;
        }

        .game-tag:hover {
            background: rgba(255, 0, 234, 0.3);
            transform: translateY(-3px);
        }

        .about-image {
            position: relative;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
            border: 2px solid var(--primary);
        }

        .about-image img {
            width: 100%;
            display: block;
            transition: transform 0.5s ease;
        }

        .about-image:hover img {
            transform: scale(1.05);
        }

        /* 游戏展示区域 */
        .games {
            background: linear-gradient(rgba(5, 5, 16, 0.9), rgba(5, 5, 16, 0.9)), url('https://images.unsplash.com/photo-1552820728-8b83bb6b773f?ixlib=rb-4.0.3&auto=format&fit=crop&w=1950&q=80') no-repeat center center/cover;
        }

        .games-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 40px;
        }

        .game-card {
            background: rgba(20, 20, 40, 0.7);
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            transition: all 0.4s ease;
            border: 1px solid rgba(0, 243, 255, 0.3);
            position: relative;
        }

        .game-card:hover {
            transform: translateY(-15px);
            box-shadow: 0 20px 40px rgba(0, 243, 255, 0.3);
            border-color: var(--primary);
        }

        .game-image {
            height: 250px;
            overflow: hidden;
        }

        .game-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s ease;
        }

        .game-card:hover .game-image img {
            transform: scale(1.1);
        }

        .game-content {
            padding: 25px;
        }

        .game-content h3 {
            font-size: 1.8rem;
            margin-bottom: 15px;
            color: var(--primary);
        }

        .game-content p {
            margin-bottom: 20px;
            color: #ccc;
        }

        .game-stats {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }

        .stat {
            text-align: center;
        }

        .stat-value {
            font-size: 1.8rem;
            font-weight: bold;
            color: var(--secondary);
        }

        .stat-label {
            font-size: 0.9rem;
            color: #aaa;
        }

        /* 游戏装备区域 */
        .setup {
            background: var(--dark);
        }

        .setup-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 50px;
            align-items: center;
        }

        .setup-image {
            position: relative;
        }

        .setup-image img {
            width: 100%;
            border-radius: 10px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
            border: 2px solid var(--secondary);
        }

        .setup-items {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 40px;
        }

        .setup-item {
            background: rgba(30, 30, 50, 0.5);
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            transition: all 0.3s ease;
            border: 1px solid rgba(0, 243, 255, 0.2);
        }

        .setup-item:hover {
            transform: translateY(-5px);
            background: rgba(40, 40, 60, 0.7);
            border-color: var(--primary);
        }

        .setup-item i {
            font-size: 2.5rem;
            color: var(--primary);
            margin-bottom: 15px;
        }

        /* 联系区域 */
        .contact {
            background: linear-gradient(rgba(5, 5, 16, 0.9), rgba(5, 5, 16, 0.9)), url('https://images.unsplash.com/photo-1511882150382-421056c89033?ixlib=rb-4.0.3&auto=format&fit=crop&w=1950&q=80') no-repeat center center/cover;
            text-align: center;
        }

        .contact-form {
            max-width: 600px;
            margin: 0 auto;
            background: rgba(20, 20, 40, 0.7);
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            border: 1px solid var(--primary);
        }

        .form-group {
            margin-bottom: 25px;
            text-align: left;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-size: 1.1rem;
            color: var(--primary);
        }

        .form-group input,
        .form-group textarea {
            width: 100%;
            padding: 12px 15px;
            border-radius: 8px;
            border: 1px solid rgba(0, 243, 255, 0.3);
            background: rgba(10, 10, 26, 0.5);
            color: var(--light);
            font-size: 1rem;
        }

        .form-group textarea {
            min-height: 150px;
            resize: vertical;
        }

        .social-links {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-top: 50px;
            flex-wrap: wrap;
        }

        .social-link {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(0, 243, 255, 0.1);
            border: 2px solid var(--primary);
            color: var(--primary);
            font-size: 2rem;
            transition: all 0.3s ease;
            text-decoration: none;
        }

        .social-link:hover {
            background: var(--primary);
            color: var(--dark);
            transform: translateY(-10px) scale(1.1);
            box-shadow: 0 0 20px var(--primary);
        }

        /* 页脚 */
        footer {
            background: var(--darker);
            text-align: center;
            padding: 30px;
            border-top: 1px solid rgba(0, 243, 255, 0.3);
        }

        .footer-logo {
            font-size: 2rem;
            color: var(--primary);
            margin-bottom: 20px;
            font-weight: bold;
        }

        .copyright {
            color: #aaa;
            font-size: 1.1rem;
        }

        .back-to-top {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 50px;
            height: 50px;
            background: var(--primary);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--dark);
            font-size: 1.5rem;
            cursor: pointer;
            box-shadow: 0 0 15px rgba(0, 243, 255, 0.5);
            transition: all 0.3s ease;
            opacity: 0;
            visibility: hidden;
            z-index: 999;
        }

        .back-to-top.show {
            opacity: 1;
            visibility: visible;
        }

        .back-to-top:hover {
            transform: translateY(-5px);
            box-shadow: 0 0 20px rgba(0, 243, 255, 0.8);
        }

        /* 响应式设计 */
        @media (max-width: 992px) {
            .about-content, .setup-content {
                grid-template-columns: 1fr;
            }
            
            .hero h1 {
                font-size: 3.5rem;
            }
            
            .hero h2 {
                font-size: 2rem;
            }
        }

        @media (max-width: 768px) {
            nav ul {
                display: none;
                position: absolute;
                top: 100%;
                left: 0;
                width: 100%;
                background: rgba(10, 10, 26, 0.95);
                flex-direction: column;
                padding: 20px 0;
                gap: 10px;
            }
            
            nav ul.show {
                display: flex;
            }
            
            nav a {
                display: block;
                padding: 12px 5%;
            }
            
            .mobile-menu-btn {
                display: block;
            }
            
            .section-title {
                font-size: 2.5rem;
            }
            
            .hero h1 {
                font-size: 2.8rem;
            }
            
            .hero h2 {
                font-size: 1.8rem;
            }
            
            .social-link {
                width: 70px;
                height: 70px;
                font-size: 1.8rem;
            }
        }

        @media (max-width: 576px) {
            section {
                padding: 100px 5%;
            }
            
            .hero h1 {
                font-size: 2.3rem;
            }
            
            .hero p {
                font-size: 1.1rem;
            }
        }

        /* 动画效果 */
        @keyframes float {
            0%, 100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-20px);
            }
        }

        .floating {
            animation: float 6s ease-in-out infinite;
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
        
        .fade-in {
            animation: fadeInUp 1s ease forwards;
        }
        
        /* 鲨鱼主题装饰 */
        .shark-decoration {
            position: absolute;
            z-index: 1;
            opacity: 0.1;
        }
        
        .shark-1 {
            top: 10%;
            left: 5%;
            width: 150px;
            height: 150px;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><path d="M50,10 Q70,30 90,50 Q70,70 50,90 Q30,70 10,50 Q30,30 50,10 Z" fill="none" stroke="%2300f3ff" stroke-width="2"/></svg>') no-repeat center;
            animation: float 8s ease-in-out infinite;
        }
        
        .shark-2 {
            bottom: 20%;
            right: 7%;
            width: 100px;
            height: 100px;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><path d="M10,50 Q30,30 50,10 Q70,30 90,50 Q70,70 50,90 Q30,70 10,50 Z" fill="none" stroke="%23ff00ea" stroke-width="2"/></svg>') no-repeat center;
            animation: float 7s ease-in-out infinite reverse;
        }
    </style>
</head>
<body>
    <!-- 粒子背景 -->
    <div id="particles-js"></div>
    
    <!-- 鲨鱼装饰元素 -->
    <div class="shark-decoration shark-1"></div>
    <div class="shark-decoration shark-2"></div>
    
    <!-- 导航栏 -->
    <header id="header">
        <div class="logo">
            <i class="fas fa-gamepad"></i>
            <span>无敌鲨鱼大王</span>
        </div>
        <nav>
            <ul id="nav-menu">
                <li><a href="#hero">首页</a></li>
                <li><a href="#about">关于我</a></li>
                <li><a href="#games">游戏世界</a></li>
                <li><a href="#setup">游戏装备</a></li>
                <li><a href="#contact">联系我</a></li>
            </ul>
            <button class="mobile-menu-btn" id="mobile-menu">
                <i class="fas fa-bars"></i>
            </button>
        </nav>
    </header>
    
    <main>
        <!-- 英雄区域 -->
        <section id="hero" class="hero">
            <div class="hero-content">
                <div class="tagline fade-in">专业玩家 & 游戏爱好者</div>
                <h1 class="fade-in">无敌鲨鱼大王</h1>
                <h2 class="fade-in">探索游戏世界的深度与魅力</h2>
                <p class="fade-in">欢迎来到我的游戏领域！在这里，我将分享我对3A游戏的热爱，特别是《GTA5》、《荒野大镖客》和《黑神话：悟空》的深度体验和游戏技巧。</p>
                <div class="fade-in" style="margin-top: 40px;">
                    <a href="#games" class="cta-button">探索我的游戏世界</a>
                </div>
            </div>
        </section>
        
        <!-- 关于我区域 -->
        <section id="about" class="about">
            <h2 class="section-title">关于我</h2>
            <div class="about-content">
                <div class="about-text">
                    <h3>我是无敌鲨鱼大王</h3>
                    <p>一个狂热的3A游戏玩家，沉浸在虚拟世界的冒险中。对我来说，游戏不仅是娱乐，更是一种艺术形式和叙事媒介。</p>
                    <p>从侠盗猎车手的自由都市到西部荒野的壮丽景观，再到中国神话的奇幻世界，我在这些精心打造的游戏宇宙中寻找灵感与挑战。</p>
                    <p>我热衷于探索游戏中的每一个细节，完成每一个任务，解锁每一个成就。对我来说，游戏是逃避现实、体验不同人生的绝佳方式。</p>
                    
                    <div class="game-list">
                        <div class="game-tag">GTA5</div>
                        <div class="game-tag">荒野大镖客2</div>
                        <div class="game-tag">黑神话：悟空</div>
                        <div class="game-tag">赛博朋克2077</div>
                        <div class="game-tag">艾尔登法环</div>
                        <div class="game-tag">战神</div>
                    </div>
                </div>
                <div class="about-image floating">
                    <img src="https://images.unsplash.com/photo-1593305841991-05c297ba4575?ixlib=rb-4.0.3&auto=format&fit=crop&w=1950&q=80" alt="游戏设置">
                </div>
            </div>
        </section>
        
        <!-- 游戏展示区域 - 已更新图片 -->
        <section id="games" class="games">
            <h2 class="section-title">我的游戏世界</h2>
            <div class="games-container">
                <!-- GTA5 卡片 -->
                <div class="game-card fade-in">
                    <div class="game-image">
                        <img src="https://images.unsplash.com/photo-1534945773093-1119ae0f3d0b?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1920&q=80" alt="GTA5">
                    </div>
                    <div class="game-content">
                        <h3>侠盗猎车手 V</h3>
                        <p>在洛圣都的霓虹灯下，我体验了犯罪世界的方方面面。从街头飙车到精心策划的银行抢劫，这个游戏提供了无与伦比的自由度和细节。</p>
                        <p>完成度: 100% | 游戏时长: 500+小时</p>
                        <div class="game-stats">
                            <div class="stat">
                                <div class="stat-value">98%</div>
                                <div class="stat-label">完成度</div>
                            </div>
                            <div class="stat">
                                <div class="stat-value">A+</div>
                                <div class="stat-label">评级</div>
                            </div>
                            <div class="stat">
                                <div class="stat-value">500+</div>
                                <div class="stat-label">小时</div>
                            </div>
                        </div>
                    </div>
                </div>
                
                <!-- 荒野大镖客 卡片 -->
                <div class="game-card fade-in">
                    <div class="game-image">
                        <img src="https://images.unsplash.com/photo-1580234811497-9df7fd2f357e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1920&q=80" alt="荒野大镖客2">
                    </div>
                    <div class="game-content">
                        <h3>荒野大镖客：救赎2</h3>
                        <p>作为亚瑟·摩根，我在美国西部的荒野中寻找救赎。这款游戏的细节令人惊叹，从马匹的毛发到营地的动态，都展现了游戏制作的巅峰。</p>
                        <p>完成度: 95% | 游戏时长: 300+小时</p>
                        <div class="game-stats">
                            <div class="stat">
                                <div class="stat-value">95%</div>
                                <div class="stat-label">完成度</div>
                            </div>
                            <div class="stat">
                                <div class="stat-value">S</div>
                                <div class="stat-label">评级</div>
                            </div>
                            <div class="stat">
                                <div class="stat-value">300+</div>
                                <div class="stat-label">小时</div>
                            </div>
                        </div>
                    </div>
                </div>
                
                <!-- 黑神话悟空 卡片 -->
                <div class="game-card fade-in">
                    <div class="game-image">
                        <img src="https://images.unsplash.com/photo-1635863138275-d9b33299680a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1920&q=80" alt="黑神话：悟空">
                    </div>
                    <div class="game-content">
                        <h3>黑神话：悟空</h3>
                        <p>沉浸在中国神话的奇幻世界中，扮演齐天大圣孙悟空。这款游戏将中国传统文化与顶尖游戏设计完美结合，战斗系统深度十足，视觉效果震撼。</p>
                        <p>完成度: 正在攻略 | 游戏时长: 80+小时</p>
                        <div class="game-stats">
                            <div class="stat">
                                <div class="stat-value">65%</div>
                                <div class="stat-label">进度</div>
                            </div>
                            <div class="stat">
                                <div class="stat-value">A</div>
                                <div class="stat-label">评级</div>
                            </div>
                            <div class="stat">
                                <div class="stat-value">80+</div>
                                <div class="stat-label">小时</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        
        <!-- 游戏装备区域 - 主机配置更新为雷神猎刃s5060 i9 -->
        <section id="setup" class="setup">
            <h2 class="section-title">我的游戏装备</h2>
            <div class="setup-content">
                <div class="setup-image floating">
                    <img src="https://images.unsplash.com/photo-1593118247619-e2d6f056869e?ixlib=rb-4.0.3&auto=format&fit=crop&w=1950&q=80" alt="游戏装备">
                </div>
                <div class="setup-text">
                    <h3>极致游戏体验</h3>
                    <p>为了充分享受这些视觉盛宴般的游戏，我配置了顶级的游戏装备，确保每一帧画面都完美呈现，每一次操作都精准响应。</p>
                    
                    <div class="setup-items">
                        <div class="setup-item fade-in">
                            <i class="fas fa-desktop"></i>
                            <h4>游戏主机</h4>
                            <p>雷神猎刃s5060 i9</p>
                        </div>
                        <div class="setup-item fade-in">
                            <i class="fas fa-headphones"></i>
                            <h4>耳机</h4>
                            <p>SteelSeries Arctis Pro</p>
                        </div>
                        <div class="setup-item fade-in">
                            <i class="fas fa-keyboard"></i>
                            <h4>键盘</h4>
                            <p>Razer Huntsman V2</p>
                        </div>
                        <div class="setup-item fade-in">
                            <i class="fas fa-mouse"></i>
                            <h4>鼠标</h4>
                            <p>Logitech G Pro X Superlight</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        
        <!-- 联系区域 -->
        <section id="contact" class="contact">
            <h2 class="section-title">联系我</h2>
            <p style="font-size: 1.4rem; max-width: 700px; margin: 0 auto 50px;">
                如果你也是3A游戏爱好者，或者对我的游戏经历感兴趣，欢迎联系我！我们可以交流游戏心得，组队完成任务，或者一起探索新的游戏世界。
            </p>
            
            <div class="contact-form">
                <div class="form-group">
                    <label for="name">姓名</label>
                    <input type="text" id="name" placeholder="请输入您的姓名">
                </div>
                <div class="form-group">
                    <label for="email">邮箱</label>
                    <input type="email" id="email" placeholder="请输入您的邮箱">
                </div>
                <div class="form-group">
                    <label for="message">留言</label>
                    <textarea id="message" placeholder="请告诉我您想交流的游戏内容..."></textarea>
                </div>
                <button class="cta-button" style="width: 100%;">发送消息</button>
            </div>
            
            <div class="social-links">
                <a href="#" class="social-link">
                    <i class="fab fa-steam"></i>
                </a>
                <a href="#" class="social-link">
                    <i class="fab fa-discord"></i>
                </a>
                <a href="#" class="social-link">
                    <i class="fab fa-twitch"></i>
                </a>
                <a href="#" class="social-link">
                    <i class="fab fa-youtube"></i>
                </a>
                <a href="#" class="social-link">
                    <i class="fab fa-twitter"></i>
                </a>
            </div>
        </section>
    </main>
    
    <!-- 页脚 -->
    <footer>
        <div class="footer-logo">无敌鲨鱼大王</div>
        <div class="copyright">© 2023 无敌鲨鱼大王的游戏世界 | 版权所有</div>
    </footer>
    
    <!-- 返回顶部按钮 -->
    <div class="back-to-top" id="backToTop">
        <i class="fas fa-arrow-up"></i>
    </div>
    
    <!-- 粒子效果脚本 -->
    <script src="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js"></script>
    <script>
        // 初始化粒子背景
        particlesJS("particles-js", {
            particles: {
                number: { value: 80, density: { enable: true, value_area: 800 } },
                color: { value: "#00f3ff" },
                shape: { type: "circle" },
                opacity: { value: 0.5, random: true },
                size: { value: 3, random: true },
                line_linked: {
                    enable: true,
                    distance: 150,
                    color: "#00f3ff",
                    opacity: 0.3,
                    width: 1
                },
                move: {
                    enable: true,
                    speed: 2,
                    direction: "none",
                    random: true,
                    straight: false,
                    out_mode: "out",
                    bounce: false
                }
            },
            interactivity: {
                detect_on: "canvas",
                events: {
                    onhover: { enable: true, mode: "grab" },
                    onclick: { enable: true, mode: "push" },
                    resize: true
                }
            }
        });
        
        // 滚动效果
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault();
                document.querySelector(this.getAttribute('href')).scrollIntoView({
                    behavior: 'smooth'
                });
                
                // 关闭移动端菜单
                document.getElementById('nav-menu').classList.remove('show');
            });
        });
        
        // 返回顶部按钮
        const backToTopBtn = document.getElementById('backToTop');
        
        window.addEventListener('scroll', () => {
            if (window.pageYOffset > 300) {
                backToTopBtn.classList.add('show');
            } else {
                backToTopBtn.classList.remove('show');
            }
        });
        
        backToTopBtn.addEventListener('click', () => {
            window.scrollTo({
                top: 0,
                behavior: 'smooth'
            });
        });
        
        // 移动端菜单
        const mobileMenuBtn = document.getElementById('mobile-menu');
        const navMenu = document.getElementById('nav-menu');
        
        mobileMenuBtn.addEventListener('click', () => {
            navMenu.classList.toggle('show');
        });
        
        // 滚动时改变导航栏样式
        const header = document.getElementById('header');
        
        window.addEventListener('scroll', () => {
            if (window.pageYOffset > 50) {
                header.classList.add('scrolled');
            } else {
                header.classList.remove('scrolled');
            }
        });
        
        // 滚动动画
        const fadeElements = document.querySelectorAll('.fade-in');
        
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.opacity = 1;
                    entry.target.style.transform = 'translateY(0)';
                }
            });
        }, {
            threshold: 0.1
        });
        
        fadeElements.forEach(element => {
            element.style.opacity = 0;
            element.style.transform = 'translateY(30px)';
            element.style.transition = 'opacity 0.8s ease, transform 0.8s ease';
            observer.observe(element);
        });
        
        // 添加鲨鱼主题动态效果
        document.addEventListener('mousemove', (e) => {
            const shark1 = document.querySelector('.shark-1');
            const shark2 = document.querySelector('.shark-2');
            
            const x = e.clientX / window.innerWidth;
            const y = e.clientY / window.innerHeight;
            
            shark1.style.transform = `translate(${x * 10 - 5}px, ${y * 10 - 5}px)`;
            shark2.style.transform = `translate(${-(x * 10 - 5)}px, ${-(y * 10 - 5)}px)`;
        });
    </script>
</body>
</html>
