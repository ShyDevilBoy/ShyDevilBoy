<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GitHub个人主页</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary: #6e40c9;
            --secondary: #5e35b1;
            --accent: #ff4081;
            --dark: #121212;
            --light: #f5f5f7;
            --gradient: linear-gradient(135deg, var(--primary), var(--accent));
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--dark);
            color: var(--light);
            line-height: 1.6;
            overflow-x: hidden;
            position: relative;
        }
        
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle at 15% 50%, rgba(110, 64, 201, 0.1), transparent 40%), 
                        radial-gradient(circle at 85% 30%, rgba(255, 64, 129, 0.1), transparent 40%);
            z-index: -1;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        /* Header & Navigation */
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 0;
            position: sticky;
            top: 0;
            background-color: rgba(18, 18, 18, 0.9);
            z-index: 100;
            backdrop-filter: blur(10px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .logo {
            font-size: 28px;
            font-weight: 700;
            background: var(--gradient);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            display: flex;
            align-items: center;
        }
        
        .logo i {
            margin-right: 10px;
            font-size: 32px;
        }
        
        nav ul {
            display: flex;
            list-style: none;
            gap: 30px;
        }
        
        nav a {
            text-decoration: none;
            color: var(--light);
            font-weight: 500;
            position: relative;
            transition: color 0.3s;
        }
        
        nav a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--gradient);
            transition: width 0.3s;
        }
        
        nav a:hover {
            color: var(--accent);
        }
        
        nav a:hover::after {
            width: 100%;
        }
        
        /* Hero Section */
        .hero {
            min-height: 90vh;
            display: flex;
            align-items: center;
            position: relative;
            overflow: hidden;
            padding: 60px 0;
        }
        
        .hero-content {
            position: relative;
            z-index: 2;
            max-width: 650px;
        }
        
        .hero h1 {
            font-size: 4.5rem;
            margin-bottom: 20px;
            line-height: 1.1;
        }
        
        .gradient-text {
            background: var(--gradient);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            position: relative;
        }
        
        .typed-text {
            display: inline-block;
        }
        
        .blinking-cursor {
            display: inline-block;
            width: 3px;
            margin-left: 5px;
            background: var(--accent);
            height: 60px;
            animation: blink 1s infinite;
        }
        
        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0; }
        }
        
        .hero p {
            font-size: 1.4rem;
            color: rgba(255, 255, 255, 0.8);
            margin-bottom: 30px;
        }
        
        .cta-button {
            display: inline-block;
            background: var(--gradient);
            color: white;
            padding: 15px 40px;
            border-radius: 50px;
            text-decoration: none;
            font-weight: 600;
            font-size: 1.2rem;
            transition: transform 0.3s, box-shadow 0.3s;
            border: none;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            z-index: 1;
        }
        
        .cta-button::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(45deg, var(--primary), var(--accent), var(--primary));
            background-size: 300% 100%;
            z-index: -1;
            transition: background-position 0.5s;
        }
        
        .cta-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(255, 64, 129, 0.3);
        }
        
        .cta-button:hover::before {
            background-position: 100% 0;
        }
        
        .social-icons {
            display: flex;
            gap: 20px;
            margin-top: 30px;
        }
        
        .social-icons a {
            display: inline-flex;
            justify-content: center;
            align-items: center;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background-color: rgba(255, 255, 255, 0.1);
            color: var(--light);
            font-size: 1.4rem;
            transition: transform 0.3s, background-color 0.3s;
        }
        
        .social-icons a:hover {
            background: var(--gradient);
            transform: translateY(-5px);
        }
        
        /* Skills Section */
        .skills {
            padding: 100px 0;
            position: relative;
        }
        
        .section-title {
            text-align: center;
            font-size: 2.5rem;
            margin-bottom: 70px;
            position: relative;
        }
        
        .section-title::after {
            content: '';
            position: absolute;
            bottom: -15px;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 4px;
            background: var(--gradient);
            border-radius: 2px;
        }
        
        .skills-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 30px;
        }
        
        .skill-card {
            background: rgba(25, 25, 35, 0.6);
            border-radius: 20px;
            padding: 30px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: transform 0.3s, box-shadow 0.3s;
            position: relative;
            overflow: hidden;
        }
        
        .skill-card::before {
            content: '';
            position: absolute;
            top: -2px;
            left: -2px;
            right: -2px;
            bottom: -2px;
            background: var(--gradient);
            z-index: -1;
            border-radius: 22px;
        }
        
        .skill-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        }
        
        .skill-card h3 {
            font-size: 1.5rem;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
        }
        
        .skill-card h3 i {
            margin-right: 15px;
            color: var(--accent);
        }
        
        .skill-category {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 20px;
        }
        
        .skill-tag {
            background: rgba(110, 64, 201, 0.2);
            color: var(--light);
            padding: 8px 20px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 500;
        }
        
        /* Stats Section */
        .stats {
            padding: 100px 0;
            position: relative;
        }
        
        .stats-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
            margin-top: 50px;
        }
        
        .stat-card {
            background: rgba(25, 25, 35, 0.6);
            border-radius: 15px;
            padding: 30px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            text-align: center;
            transition: transform 0.3s;
        }
        
        .stat-card:hover {
            transform: translateY(-10px);
        }
        
        .stat-card i {
            font-size: 3rem;
            margin-bottom: 20px;
            background: var(--gradient);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        
        .stat-number {
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 10px;
            background: var(--gradient);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        
        .stat-text {
            font-size: 1.2rem;
            color: rgba(255, 255, 255, 0.8);
        }
        
        /* Projects Section */
        .projects {
            padding: 100px 0;
            position: relative;
        }
        
        .projects-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
            gap: 30px;
        }
        
        .project-card {
            background: rgba(25, 25, 35, 0.6);
            border-radius: 15px;
            overflow: hidden;
            transition: transform 0.3s, box-shadow 0.3s;
            position: relative;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .project-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        }
        
        .project-image {
            height: 200px;
            width: 100%;
            background: linear-gradient(45deg, var(--primary), var(--accent));
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 4rem;
            color: white;
        }
        
        .project-content {
            padding: 25px;
        }
        
        .project-title {
            font-size: 1.5rem;
            margin-bottom: 15px;
        }
        
        .project-description {
            color: rgba(255, 255, 255, 0.8);
            margin-bottom: 20px;
        }
        
        .project-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .project-tag {
            background: rgba(255, 64, 129, 0.1);
            color: var(--accent);
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.8rem;
        }
        
        .project-links {
            display: flex;
            gap: 15px;
        }
        
        .project-link {
            display: flex;
            align-items: center;
            color: var(--light);
            text-decoration: none;
            font-size: 0.9rem;
        }
        
        .project-link i {
            margin-right: 8px;
            transition: transform 0.3s;
        }
        
        .project-link:hover i {
            transform: translateX(5px);
        }
        
        /* Contact Section */
        .contact {
            padding: 100px 0;
            position: relative;
            text-align: center;
        }
        
        .contact-form {
            max-width: 600px;
            margin: 50px auto 0;
            display: grid;
            gap: 20px;
        }
        
        .form-group {
            position: relative;
        }
        
        .form-group input,
        .form-group textarea {
            width: 100%;
            padding: 18px 20px;
            background: rgba(25, 25, 35, 0.6);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            color: var(--light);
            font-size: 1rem;
            backdrop-filter: blur(10px);
        }
        
        .form-group textarea {
            height: 150px;
            resize: vertical;
        }
        
        .form-group input:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: var(--primary);
        }
        
        .form-group label {
            position: absolute;
            left: 20px;
            top: 18px;
            color: rgba(255, 255, 255, 0.7);
            transition: all 0.3s;
            pointer-events: none;
        }
        
        .form-group input:focus + label,
        .form-group textarea:focus + label,
        .form-group input:not(:placeholder-shown) + label,
        .form-group textarea:not(:placeholder-shown) + label {
            top: -12px;
            left: 15px;
            background: var(--dark);
            padding: 0 5px;
            font-size: 0.9rem;
            color: var(--accent);
        }
        
        .submit-btn {
            background: var(--gradient);
            color: white;
            border: none;
            padding: 16px;
            font-size: 1.1rem;
            font-weight: 600;
            border-radius: 10px;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            margin-top: 10px;
        }
        
        .submit-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(255, 64, 129, 0.3);
        }
        
        /* Footer */
        footer {
            padding: 40px 0;
            text-align: center;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            color: rgba(255, 255, 255, 0.6);
        }
        
        /* Animations */
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
            100% { transform: translateY(0px); }
        }
        
        .floating {
            animation: float 6s ease-in-out infinite;
        }
        
        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(255, 64, 129, 0.6); }
            70% { box-shadow: 0 0 0 20px rgba(255, 64, 129, 0); }
            100% { box-shadow: 0 0 0 0 rgba(255, 64, 129, 0); }
        }
        
        .pulse {
            position: relative;
            animation: pulse 2s infinite;
            border-radius: 50%;
        }
        
        /* Responsive */
        @media (max-width: 992px) {
            .hero h1 {
                font-size: 3.5rem;
            }
            
            .section-title {
                font-size: 2rem;
            }
        }
        
        @media (max-width: 768px) {
            header {
                flex-direction: column;
                gap: 20px;
            }
            
            nav ul {
                gap: 20px;
            }
            
            .hero {
                text-align: center;
            }
            
            .hero-content {
                margin: 0 auto;
            }
            
            .social-icons {
                justify-content: center;
            }
            
            .hero h1 {
                font-size: 2.8rem;
            }
            
            .projects-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <div class="container">
            <div class="logo">
                <i class="fab fa-github"></i>
                GitHub Profile
            </div>
            <nav>
                <ul>
                    <li><a href="#home">Home</a></li>
                    <li><a href="#skills">Skills</a></li>
                    <li><a href="#stats">Stats</a></li>
                    <li><a href="#projects">Projects</a></li>
                    <li><a href="#contact">Contact</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <!-- Hero Section -->
    <section id="home" class="hero">
        <div class="container">
            <div class="hero-content">
                <h1>Hello, I'm <span class="gradient-text">John Doe</span></h1>
                <h1>A <span class="gradient-text typed-text">Full-Stack Developer</span><span class="blinking-cursor"></span></h1>
                <p>Passionate about creating elegant, innovative solutions to complex problems. Open-source enthusiast and cloud computing advocate.</p>
                <a href="#projects" class="cta-button pulse">View My Work</a>
                <div class="social-icons">
                    <a href="#" title="GitHub"><i class="fab fa-github"></i></a>
                    <a href="#" title="LinkedIn"><i class="fab fa-linkedin-in"></i></a>
                    <a href="#" title="Twitter"><i class="fab fa-twitter"></i></a>
                    <a href="#" title="Stack Overflow"><i class="fab fa-stack-overflow"></i></a>
                </div>
            </div>
        </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="skills">
        <div class="container">
            <h2 class="section-title">My Skills</h2>
            <div class="skills-container">
                <div class="skill-card floating">
                    <h3><i class="fas fa-laptop-code"></i> Frontend Development</h3>
                    <div class="skill-category">
                        <div class="skill-tag">React</div>
                        <div class="skill-tag">Vue.js</div>
                        <div class="skill-tag">JavaScript</div>
                        <div class="skill-tag">TypeScript</div>
                        <div class="skill-tag">Tailwind CSS</div>
                        <div class="skill-tag">SASS</div>
                        <div class="skill-tag">HTML5</div>
                        <div class="skill-tag">CSS3</div>
                    </div>
                </div>
                
                <div class="skill-card floating">
                    <h3><i class="fas fa-server"></i> Backend Development</h3>
                    <div class="skill-category">
                        <div class="skill-tag">Node.js</div>
                        <div class="skill-tag">Express</div>
                        <div class="skill-tag">Python</div>
                        <div class="skill-tag">Django</div>
                        <div class="skill-tag">REST API</div>
                        <div class="skill-tag">GraphQL</div>
                        <div class="skill-tag">MongoDB</div>
                        <div class="skill-tag">PostgreSQL</div>
                    </div>
                </div>
                
                <div class="skill-card floating">
                    <h3><i class="fas fa-cloud"></i> DevOps & Cloud</h3>
                    <div class="skill-category">
                        <div class="skill-tag">AWS</div>
                        <div class="skill-tag">Docker</div>
                        <div class="skill-tag">Kubernetes</div>
                        <div class="skill-tag">Terraform</div>
                        <div class="skill-tag">CI/CD</div>
                        <div class="skill-tag">Jenkins</div>
                        <div class="skill-tag">Linux</div>
                        <div class="skill-tag">Bash</div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Stats Section -->
    <section id="stats" class="stats">
        <div class="container">
            <h2 class="section-title">GitHub Statistics</h2>
            <div class="stats-container">
                <div class="stat-card">
                    <i class="fas fa-code-branch"></i>
                    <div class="stat-number" id="repos">47</div>
                    <div class="stat-text">Repositories</div>
                </div>
                
                <div class="stat-card">
                    <i class="fas fa-star"></i>
                    <div class="stat-number" id="stars">256</div>
                    <div class="stat-text">Stars</div>
                </div>
                
                <div class="stat-card">
                    <i class="fas fa-code"></i>
                    <div class="stat-number" id="commits">1,287</div>
                    <div class="stat-text">Commits</div>
                </div>
                
                <div class="stat-card">
                    <i class="fas fa-users"></i>
                    <div class="stat-number" id="contributions">84</div>
                    <div class="stat-text">Contributions</div>
                </div>
            </div>
            <div style="margin-top: 60px; height: 300px;">
                <canvas id="languageChart"></canvas>
            </div>
        </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="projects">
        <div class="container">
            <h2 class="section-title">Featured Projects</h2>
            <div class="projects-grid">
                <div class="project-card">
                    <div class="project-image">
                        <i class="fas fa-music"></i>
                    </div>
                    <div class="project-content">
                        <h3 class="project-title">Music Streaming Platform</h3>
                        <p class="project-description">A full-featured music streaming service with personalized playlists, recommendations, and social features.</p>
                        <div class="project-tags">
                            <div class="project-tag">React</div>
                            <div class="project-tag">Node.js</div>
                            <div class="project-tag">MongoDB</div>
                            <div class="project-tag">Web Audio API</div>
                        </div>
                        <div class="project-links">
                            <a href="#" class="project-link"><i class="fab fa-github"></i> Source Code</a>
                            <a href="#" class="project-link"><i class="fas fa-external-link-alt"></i> Live Demo</a>
                        </div>
                    </div>
                </div>
                
                <div class="project-card">
                    <div class="project-image">
                        <i class="fas fa-robot"></i>
                    </div>
                    <div class="project-content">
                        <h3 class="project-title">AI Task Manager</h3>
                        <p class="project-description">Intelligent task management system with automated prioritization, scheduling, and progress tracking.</p>
                        <div class="project-tags">
                            <div class="project-tag">Python</div>
                            <div class="project-tag">TensorFlow</div>
                            <div class="project-tag">Vue.js</div>
                            <div class="project-tag">Firebase</div>
                        </div>
                        <div class="project-links">
                            <a href="#" class="project-link"><i class="fab fa-github"></i> Source Code</a>
                            <a href="#" class="project-link"><i class="fas fa-external-link-alt"></i> Live Demo</a>
                        </div>
                    </div>
                </div>
                
                <div class="project-card">
                    <div class="project-image">
                        <i class="fas fa-wallet"></i>
                    </div>
                    <div class="project-content">
                        <h3 class="project-title">Crypto Portfolio Tracker</h3>
                        <p class="project-description">Real-time cryptocurrency portfolio tracker with market analytics and price alerts.</p>
                        <div class="project-tags">
                            <div class="project-tag">React</div>
                            <div class="project-tag">Redux</div>
                            <div class="project-tag">Express</div>
                            <div class="project-tag">WebSockets</div>
                        </div>
                        <div class="project-links">
                            <a href="#" class="project-link"><i class="fab fa-github"></i> Source Code</a>
                            <a href="#" class="project-link"><i class="fas fa-external-link-alt"></i> Live Demo</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="contact">
        <div class="container">
            <h2 class="section-title">Get In Touch</h2>
            <form class="contact-form">
                <div class="form-group">
                    <input type="text" id="name" placeholder=" ">
                    <label for="name">Your Name</label>
                </div>
                <div class="form-group">
                    <input type="email" id="email" placeholder=" ">
                    <label for="email">Your Email</label>
                </div>
                <div class="form-group">
                    <input type="text" id="subject" placeholder=" ">
                    <label for="subject">Subject</label>
                </div>
                <div class="form-group">
                    <textarea id="message" placeholder=" "></textarea>
                    <label for="message">Message</label>
                </div>
                <button type="submit" class="submit-btn">Send Message <i class="fas fa-paper-plane"></i></button>
            </form>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <div class="container">
            <p>&copy; 2023 GitHub Portfolio. All rights reserved.</p>
            <p>Made with <i class="fas fa-heart" style="color: var(--accent);"></i> for developers</p>
        </div>
    </footer>

    <script>
        // Animated typing effect
        document.addEventListener('DOMContentLoaded', function() {
            const typingText = document.querySelector('.typed-text');
            const texts = ['Full-Stack Developer', 'Open Source Contributor', 'Cloud Architect', 'Tech Enthusiast'];
            let textIndex = 0;
            let charIndex = 0;
            let isDeleting = false;
            let typingSpeed = 100;
            const cursor = document.querySelector('.blinking-cursor');
            
            function typeEffect() {
                const currentText = texts[textIndex];
                
                if (!isDeleting && charIndex < currentText.length) {
                    typingText.textContent += currentText.charAt(charIndex);
                    charIndex++;
                    setTimeout(typeEffect, typingSpeed);
                } else if (isDeleting && charIndex > 0) {
                    typingText.textContent = currentText.substring(0, charIndex - 1);
                    charIndex--;
                    setTimeout(typeEffect, typingSpeed / 2);
                } else {
                    isDeleting = !isDeleting;
                    if (!isDeleting) textIndex = (textIndex + 1) % texts.length;
                    setTimeout(typeEffect, typingSpeed * 2);
                }
            }
            
            setTimeout(typeEffect, 1000);
            
            // Count-up animation for stats
            const countUpOptions = {
                duration: 2000,
                useEasing: true
            };
            
            const reposElement = document.getElementById('repos');
            const starsElement = document.getElementById('stars');
            const commitsElement = document.getElementById('commits');
            const contributionsElement = document.getElementById('contributions');
            
            function animateValue(id, start, end, duration) {
                const element = document.getElementById(id);
                let startTimestamp = null;
                const step = (timestamp) => {
                    if (!startTimestamp) startTimestamp = timestamp;
                    const progress = Math.min((timestamp - startTimestamp) / duration, 1);
                    const value = Math.floor(progress * (end - start) + start);
                    element.textContent = value;
                    if (progress < 1) {
                        window.requestAnimationFrame(step);
                    }
                };
                window.requestAnimationFrame(step);
            }
            
            // Initialize values with animation
            setTimeout(() => {
                animateValue('repos', 0, 47, 1500);
                animateValue('stars', 0, 256, 1500);
                animateValue('commits', 0, 1287, 1500);
                animateValue('contributions', 0, 84, 1500);
            }, 500);
            
            // Language chart using Chart.js
            const ctx = document.getElementById('languageChart').getContext('2d');
            const languageChart = new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['JavaScript', 'Python', 'TypeScript', 'HTML/CSS', 'Java', 'C++'],
                    datasets: [{
                        data: [35, 25, 20, 10, 5, 5],
                        backgroundColor: [
                            '#f1e05a',
                            '#3572a5',
                            '#3178c6',
                            '#e34c26',
                            '#b07219',
                            '#f34b7d'
                        ],
                        borderWidth: 0,
                        hoverOffset: 20
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'right',
                            labels: {
                                color: '#f5f5f7',
                                font: {
                                    size: 14
                                }
                            }
                        },
                        title: {
                            display: true,
                            text: 'GitHub Language Distribution',
                            color: '#f5f5f7',
                            font: {
                                size: 18
                            }
                        }
                    }
                }
            });
        });
    </script>
</body>
</html>
