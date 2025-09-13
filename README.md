    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Muneeb Telecom | Premium Electronics</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.min.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore-compat.js"></script>
    <style>
        :root {
            --dark-bg: #0a0a1a;
            --dark-card: #12122a;
            --primary: #ff6b35;
            --accent: #ff9e35;
            --neon-orange: #ff6b35;
            --neon-yellow: #ff9e35;
            --text: #ffffff;
            --text-muted: #a0a0c0;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: var(--dark-bg);
            color: var(--text);
            overflow-x: hidden;
            line-height: 1.6;
        }

        .container {
            width: 100%;
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Header Styles */
        header {
            padding: 20px 0;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            background: rgba(10, 10, 26, 0.8);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid rgba(255, 155, 53, 0.2);
        }

        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo-container {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo-img {
            height: 50px;
            width: auto;
            border-radius: 10px;
        }

        .logo-text {
            font-size: 28px;
            font-weight: 700;
            background: linear-gradient(45deg, var(--neon-yellow), var(--neon-orange));
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 10px rgba(255, 155, 53, 0.5);
        }

        nav ul {
            display: flex;
            list-style: none;
            gap: 30px;
        }

        nav a {
            color: var(--text);
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s, text-shadow 0.3s;
            position: relative;
        }

        nav a:hover {
            color: var(--neon-yellow);
            text-shadow: 0 0 10px rgba(255, 155, 53, 0.7);
        }

        nav a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: linear-gradient(90deg, var(--neon-yellow), var(--neon-orange));
            transition: width 0.3s;
        }

        nav a:hover::after {
            width: 100%;
        }

        .mobile-menu-btn {
            display: none;
            background: none;
            border: none;
            color: var(--text);
            font-size: 24px;
            cursor: pointer;
        }

        /* Hero Section */
        .hero {
            height: 100vh;
            display: flex;
            align-items: center;
            padding-top: 80px;
            position: relative;
            overflow: hidden;
        }

        .hero-content {
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 40px;
        }

        .hero-text {
            flex: 1;
            max-width: 500px;
        }

        .hero-text h1 {
            font-size: 3.5rem;
            margin-bottom: 20px;
            background: linear-gradient(45deg, var(--neon-yellow), var(--neon-orange));
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
            line-height: 1.2;
        }

        .hero-text p {
            font-size: 1.2rem;
            color: var(--text-muted);
            margin-bottom: 30px;
        }

        .btn {
            display: inline-block;
            padding: 12px 30px;
            background: linear-gradient(45deg, var(--neon-yellow), var(--neon-orange));
            color: white;
            border: none;
            border-radius: 30px;
            font-weight: 600;
            text-decoration: none;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            box-shadow: 0 0 20px rgba(255, 155, 53, 0.5);
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 0 30px rgba(255, 155, 53, 0.7);
        }

        .hero-3d {
            flex: 1;
            height: 400px;
            position: relative;
        }

        #phone-container {
            width: 100%;
            height: 100%;
            border-radius: 20px;
            overflow: hidden;
        }

        /* Featured Products */
        .section-title {
            text-align: center;
            margin-bottom: 60px;
            font-size: 2.5rem;
            background: linear-gradient(45deg, var(--neon-yellow), var(--neon-orange));
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .section-title::after {
            content: '';
            display: block;
            width: 100px;
            height: 4px;
            background: linear-gradient(90deg, var(--neon-yellow), var(--neon-orange));
            margin: 10px auto;
            border-radius: 2px;
        }

        .products {
            padding: 100px 0;
        }

        .product-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
        }

        .product-card {
            background: var(--dark-card);
            border-radius: 15px;
            overflow: hidden;
            transition: transform 0.3s, box-shadow 0.3s;
            position: relative;
            border: 1px solid rgba(255, 155, 53, 0.1);
        }

        .product-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 10px 30px rgba(255, 155, 53, 0.2);
        }

        .product-img {
            height: 200px;
            background: linear-gradient(135deg, #1a1a3a, #0a0a1a);
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }

        .product-img::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255, 155, 53, 0.1), transparent);
            transform: rotate(45deg);
            animation: shine 3s infinite linear;
        }

        @keyframes shine {
            0% { transform: translateX(-100%) rotate(45deg); }
            100% { transform: translateX(100%) rotate(45deg); }
        }

        .product-info {
            padding: 20px;
        }

        .product-info h3 {
            font-size: 1.3rem;
            margin-bottom: 10px;
        }

        .product-info p {
            color: var(--text-muted);
            margin-bottom: 15px;
        }

        .price {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--neon-orange);
            margin-bottom: 15px;
        }

        /* Categories */
        .categories {
            padding: 100px 0;
            background: linear-gradient(to bottom, rgba(10, 10, 26, 0.9), rgba(10, 10, 26, 0.7)), url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100"><rect fill="%2312122a" width="100" height="100"/><path d="M0 50L100 50M50 0L50 100" stroke="%23333" stroke-width="1"/></svg>');
            background-size: cover;
        }

        .category-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
        }

        .category-card {
            background: var(--dark-card);
            border-radius: 15px;
            padding: 30px;
            text-align: center;
            transition: transform 0.3s, box-shadow 0.3s;
            border: 1px solid rgba(255, 155, 53, 0.1);
        }

        .category-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(255, 155, 53, 0.2);
        }

        .category-icon {
            font-size: 3rem;
            margin-bottom: 20px;
            color: var(--neon-orange);
        }

        .category-card h3 {
            font-size: 1.5rem;
            margin-bottom: 15px;
        }

        /* About Us */
        .about {
            padding: 100px 0;
        }

        .about-content {
            display: flex;
            align-items: center;
            gap: 50px;
        }

        .about-text {
            flex: 1;
        }

        .about-text h2 {
            font-size: 2.5rem;
            margin-bottom: 20px;
            background: linear-gradient(45deg, var(--neon-yellow), var(--neon-orange));
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .about-text p {
            font-size: 1.1rem;
            color: var(--text-muted);
            margin-bottom: 20px;
        }

        .about-stats {
            flex: 1;
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
        }

        .stat-box {
            background: var(--dark-card);
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            border: 1px solid rgba(255, 155, 53, 0.1);
        }

        .stat-number {
            font-size: 2.5rem;
            font-weight: 700;
            color: var(--neon-orange);
            margin-bottom: 10px;
        }

        /* Contact */
        .contact {
            padding: 100px 0;
            background: linear-gradient(to bottom, rgba(10, 10, 26, 0.9), rgba(10, 10, 26, 0.7)), url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100"><rect fill="%2312122a" width="100" height="100"/><path d="M0 50L100 50M50 0L50 100" stroke="%23333" stroke-width="1"/></svg>');
            background-size: cover;
        }

        .contact-content {
            display: flex;
            gap: 50px;
        }

        .contact-info {
            flex: 1;
        }

        .contact-info h2 {
            font-size: 2.5rem;
            margin-bottom: 20px;
            background: linear-gradient(45deg, var(--neon-yellow), var(--neon-orange));
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .contact-info p {
            font-size: 1.1rem;
            color: var(--text-muted);
            margin-bottom: 30px;
        }

        .contact-details {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .contact-detail {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .contact-icon {
            width: 50px;
            height: 50px;
            background: linear-gradient(45deg, var(--neon-yellow), var(--neon-orange));
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
        }

        .contact-form {
            flex: 1;
            background: var(--dark-card);
            padding: 30px;
            border-radius: 15px;
            border: 1px solid rgba(255, 155, 53, 0.1);
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
        }

        .form-group input,
        .form-group textarea {
            width: 100%;
            padding: 12px 15px;
            background: rgba(10, 10, 26, 0.5);
            border: 1px solid rgba(255, 155, 53, 0.2);
            border-radius: 8px;
            color: var(--text);
            font-size: 1rem;
        }

        .form-group input:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: var(--neon-orange);
            box-shadow: 0 0 10px rgba(255, 155, 53, 0.3);
        }

        /* Footer */
        footer {
            background: var(--dark-card);
            padding: 50px 0 20px;
            border-top: 1px solid rgba(255, 155, 53, 0.1);
        }

        .footer-content {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 40px;
            margin-bottom: 40px;
        }

        .footer-logo {
            font-size: 2rem;
            font-weight: 700;
            margin-bottom: 20px;
            background: linear-gradient(45deg, var(--neon-yellow), var(--neon-orange));
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .footer-links h3 {
            font-size: 1.3rem;
            margin-bottom: 20px;
            color: var(--neon-orange);
        }

        .footer-links ul {
            list-style: none;
        }

        .footer-links li {
            margin-bottom: 10px;
        }

        .footer-links a {
            color: var(--text-muted);
            text-decoration: none;
            transition: color 0.3s;
        }

        .footer-links a:hover {
            color: var(--neon-orange);
        }

        .social-links {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }

        .social-links a {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--dark-bg);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text);
            text-decoration: none;
            transition: all 0.3s;
            border: 1px solid rgba(255, 155, 53, 0.2);
        }

        .social-links a:hover {
            background: linear-gradient(45deg, var(--neon-yellow), var(--neon-orange));
            color: white;
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(255, 155, 53, 0.3);
        }

        .copyright {
            text-align: center;
            padding-top: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            color: var(--text-muted);
        }

        /* Floating CTA */
        .floating-cta {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: linear-gradient(45deg, var(--neon-yellow), var(--neon-orange));
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            text-decoration: none;
            font-size: 1.5rem;
            box-shadow: 0 5px 20px rgba(255, 155, 53, 0.5);
            z-index: 1000;
            animation: pulse 2s infinite;
            transition: transform 0.3s;
        }

        .floating-cta:hover {
            transform: scale(1.1);
        }

        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(255, 155, 53, 0.7); }
            70% { box-shadow: 0 0 0 15px rgba(255, 155, 53, 0); }
            100% { box-shadow: 0 0 0 0 rgba(255, 155, 53, 0); }
        }

        /* Responsive Styles */
        @media (max-width: 992px) {
            .hero-content {
                flex-direction: column;
                text-align: center;
            }
            
            .hero-text {
                max-width: 100%;
            }
            
            .about-content, .contact-content {
                flex-direction: column;
            }
            
            nav ul {
                gap: 15px;
            }
        }

        @media (max-width: 768px) {
            .mobile-menu-btn {
                display: block;
            }
            
            nav ul {
                position: fixed;
                top: 80px;
                left: -100%;
                width: 100%;
                height: calc(100vh - 80px);
                background: var(--dark-bg);
                flex-direction: column;
                align-items: center;
                justify-content: center;
                gap: 40px;
                transition: left 0.3s;
            }
            
            nav ul.active {
                left: 0;
            }
            
            .hero-text h1 {
                font-size: 2.5rem;
            }
            
            .section-title {
                font-size: 2rem;
            }
            
            .logo-text {
                font-size: 22px;
            }
            
            .logo-img {
                height: 40px;
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <div class="container header-content">
            <div class="logo-container">
                <img src="https://i.postimg.cc/WzZHhfQ6/IMG-20250913-094205.jpg" alt="Muneeb Telecom Logo" class="logo-img">
                <div class="logo-text">Muneeb Telecom</div>
            </div>
            <button class="mobile-menu-btn">
                <i class="fas fa-bars"></i>
            </button>
            <nav>
                <ul>
                    <li><a href="#home">Home</a></li>
                    <li><a href="#products">Products</a></li>
                    <li><a href="#categories">Categories</a></li>
                    <li><a href="#about">About Us</a></li>
                    <li><a href="#contact">Contact</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero" id="home">
        <div class="container hero-content">
            <div class="hero-text">
                <h1>Experience The Future of Mobile Technology</h1>
                <p>Discover the latest smartphones, tablets, and smart devices with cutting-edge technology and premium design.</p>
                <a href="#products" class="btn">Explore Products</a>
            </div>
            <div class="hero-3d">
                <div id="phone-container"></div>
            </div>
        </div>
    </section>

    <!-- Featured Products -->
    <section class="products" id="products">
        <div class="container">
            <h2 class="section-title">Featured Products</h2>
            <div class="product-grid">
                <div class="product-card">
                    <div class="product-img">
                        <i class="fas fa-mobile-alt" style="font-size: 80px; color: var(--neon-orange);"></i>
                    </div>
                    <div class="product-info">
                        <h3>Quantum X Pro</h3>
                        <p>The latest flagship with revolutionary camera technology.</p>
                        <div class="price">$999</div>
                        <a href="#" class="btn">View Details</a>
                    </div>
                </div>
                <div class="product-card">
                    <div class="product-img">
                        <i class="fas fa-tablet-alt" style="font-size: 80px; color: var(--neon-orange);"></i>
                    </div>
                    <div class="product-info">
                        <h3>Nexus Tab Ultra</h3>
                        <p>Powerful tablet for work and entertainment.</p>
                        <div class="price">$799</div>
                        <a href="#" class="btn">View Details</a>
                    </div>
                </div>
                <div class="product-card">
                    <div class="product-img">
                        <i class="fas fa-headphones" style="font-size: 80px; color: var(--neon-orange);"></i>
                    </div>
                    <div class="product-info">
                        <h3>SoundBlast Pro</h3>
                        <p>Wireless headphones with immersive sound quality.</p>
                        <div class="price">$249</div>
                        <a href="#" class="btn">View Details</a>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Categories -->
    <section class="categories" id="categories">
        <div class="container">
            <h2 class="section-title">Product Categories</h2>
            <div class="category-grid">
                <div class="category-card">
                    <div class="category-icon">
                        <i class="fas fa-mobile-alt"></i>
                    </div>
                    <h3>Smartphones</h3>
                    <p>Latest models from top brands with cutting-edge technology.</p>
                </div>
                <div class="category-card">
                    <div class="category-icon">
                        <i class="fas fa-tablet-alt"></i>
                    </div>
                    <h3>Tablets</h3>
                    <p>Powerful tablets for work, creativity, and entertainment.</p>
                </div>
                <div class="category-card">
                    <div class="category-icon">
                        <i class="fas fa-clock"></i>
                    </div>
                    <h3>Smart Watches</h3>
                    <p>Stay connected with advanced wearable technology.</p>
                </div>
                <div class="category-card">
                    <div class="category-icon">
                        <i class="fas fa-headphones"></i>
                    </div>
                    <h3>Accessories</h3>
                    <p>Premium accessories to enhance your experience.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- About Us -->
    <section class="about" id="about">
        <div class="container">
            <h2 class="section-title">About Us</h2>
            <div class="about-content">
                <div class="about-text">
                    <h2>We Bring You The Future</h2>
                    <p>Muneeb Telecom has been at the forefront of mobile technology for over a decade. We pride ourselves on offering the latest devices with exceptional customer service.</p>
                    <p>Our team of experts is always ready to help you find the perfect device that suits your needs and lifestyle.</p>
                    <a href="#contact" class="btn">Get In Touch</a>
                </div>
                <div class="about-stats">
                    <div class="stat-box">
                        <div class="stat-number">10+</div>
                        <div class="stat-text">Years Experience</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-number">5000+</div>
                        <div class="stat-text">Happy Customers</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-number">50+</div>
                        <div class="stat-text">Brands Available</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-number">24/7</div>
                        <div class="stat-text">Customer Support</div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Contact -->
    <section class="contact" id="contact">
        <div class="container">
            <h2 class="section-title">Contact Us</h2>
            <div class="contact-content">
                <div class="contact-info">
                    <h2>Get In Touch</h2>
                    <p>Have questions about our products or services? Reach out to our team for assistance.</p>
                    <div class="contact-details">
                        <div class="contact-detail">
                            <div class="contact-icon">
                                <i class="fas fa-map-marker-alt"></i>
                            </div>
                            <div>
                                <h3>Location</h3>
                                <p>123 Tech Street, Digital City</p>
                            </div>
                        </div>
                        <div class="contact-detail">
                            <div class="contact-icon">
                                <i class="fas fa-phone"></i>
                            </div>
                            <div>
                                <h3>Phone</h3>
                                <p>+1 (555) 123-4567</p>
                            </div>
                        </div>
                        <div class="contact-detail">
                            <div class="contact-icon">
                                <i class="fas fa-envelope"></i>
                            </div>
                            <div>
                                <h3>Email</h3>
                                <p>info@muneebtelecom.com</p>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="contact-form">
                    <h3>Send us a Message</h3>
                    <form id="contactForm">
                        <div class="form-group">
                            <label for="name">Name</label>
                            <input type="text" id="name" required>
                        </div>
                        <div class="form-group">
                            <label for="email">Email</label>
                            <input type="email" id="email" required>
                        </div>
                        <div class="form-group">
                            <label for="message">Message</label>
                            <textarea id="message" rows="5" required></textarea>
                        </div>
                        <button type="submit" class="btn">Send Message</button>
                    </form>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <div class="container">
            <div class="footer-content">
                <div class="footer-about">
                    <div class="footer-logo">Muneeb Telecom</div>
                    <p>Providing the latest technology with exceptional service since 2010.</p>
                    <div class="social-links">
                        <a href="https://www.tiktok.com/@muneebtelecom?_t=ZN-8zgTtO2KphW&_r=1" target="_blank"><i class="fab fa-tiktok"></i></a>
                        <a href="https://www.instagram.com/muneeb_telecome14?igsh=bmZmbmswN3lkaGQy" target="_blank"><i class="fab fa-instagram"></i></a>
                        <a href="https://www.olx.com.pk/en/profile/f7e31bc0-0ecc-44ca-89eb-a137baac48aa" target="_blank"><i class="fas fa-store"></i></a>
                    </div>
                </div>
                <div class="footer-links">
                    <h3>Quick Links</h3>
                    <ul>
                        <li><a href="#home">Home</a></li>
                        <li><a href="#products">Products</a></li>
                        <li><a href="#categories">Categories</a></li>
                        <li><a href="#about">About Us</a></li>
                        <li><a href="#contact">Contact</a></li>
                    </ul>
                </div>
                <div class="footer-links">
                    <h3>Products</h3>
                    <ul>
                        <li><a href="#">Smartphones</a></li>
                        <li><a href="#">Tablets</a></li>
                        <li><a href="#">Smart Watches</a></li>
                        <li><a href="#">Accessories</a></li>
                        <li><a href="#">New Arrivals</a></li>
                    </ul>
                </div>
                <div class="footer-links">
                    <h3>Support</h3>
                    <ul>
                        <li><a href="#">FAQ</a></li>
                        <li><a href="#">Shipping</a></li>
                        <li><a href="#">Returns</a></li>
                        <li><a href="#">Warranty</a></li>
                        <li><a href="#">Privacy Policy</a></li>
                    </ul>
                </div>
            </div>
            <div class="copyright">
                <p>&copy; 2023 Muneeb Telecom. All Rights Reserved.</p>
            </div>
        </div>
    </footer>

    <!-- Floating CTA -->
    <a href="#contact" class="floating-cta">
        <i class="fas fa-phone"></i>
    </a>

    <script>
        // Mobile Menu Toggle
        const menuBtn = document.querySelector('.mobile-menu-btn');
        const navMenu = document.querySelector('nav ul');
        
        menuBtn.addEventListener('click', () => {
            navMenu.classList.toggle('active');
            menuBtn.innerHTML = navMenu.classList.contains('active') ? 
                '<i class="fas fa-times"></i>' : '<i class="fas fa-bars"></i>';
        });

        // Close menu when clicking on a link
        document.querySelectorAll('nav a').forEach(link => {
            link.addEventListener('click', () => {
                navMenu.classList.remove('active');
                menuBtn.innerHTML = '<i class="fas fa-bars"></i>';
            });
        });

        // Three.js 3D Phone Animation
        let scene, camera, renderer, phone;
        
        function init() {
            // Create scene
            scene = new THREE.Scene();
            
            // Create camera
            camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            camera.position.z = 5;
            
            // Create renderer
            renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
            renderer.setSize(document.getElementById('phone-container').offsetWidth, 
                             document.getElementById('phone-container').offsetHeight);
            document.getElementById('phone-container').appendChild(renderer.domElement);
            
            // Create phone model (simplified with basic geometry)
            const geometry = new THREE.BoxGeometry(2, 4, 0.2);
            const material = new THREE.MeshPhongMaterial({ 
                color: 0xff6b35,
                shininess: 100,
                specular: 0xff9e35
            });
            phone = new THREE.Mesh(geometry, material);
            scene.add(phone);
            
            // Add lights
            const ambientLight = new THREE.AmbientLight(0x404040);
            scene.add(ambientLight);
            
            const directionalLight = new THREE.DirectionalLight(0xff9e35, 1);
            directionalLight.position.set(5, 5, 5);
            scene.add(directionalLight);
            
            const pointLight = new THREE.PointLight(0xff6b35, 1, 100);
            pointLight.position.set(-5, -5, 5);
            scene.add(pointLight);
            
            // Animation
            function animate() {
                requestAnimationFrame(animate);
                
                phone.rotation.x += 0.005;
                phone.rotation.y += 0.01;
                
                renderer.render(scene, camera);
            }
            
            animate();
            
            // Handle window resize
            window.addEventListener('resize', () => {
                camera.aspect = document.getElementById('phone-container').offsetWidth / 
                                document.getElementById('phone-container').offsetHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(document.getElementById('phone-container').offsetWidth, 
                                document.getElementById('phone-container').offsetHeight);
            });
        }
        
        // Initialize 3D scene when page is loaded
        window.onload = init;

        // Firebase Configuration
        const firebaseConfig = {
            apiKey: "YOUR_API_KEY",
            authDomain: "muneeb-telecom.firebaseapp.com",
            projectId: "muneeb-telecom",
            storageBucket: "muneeb-telecom.appspot.com",
            messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
            appId: "YOUR_APP_ID"
        };

        // Initialize Firebase
        firebase.initializeApp(firebaseConfig);
        const db = firebase.firestore();

        // Handle contact form submission
        document.getElementById('contactForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const name = document.getElementById('name').value;
            const email = document.getElementById('email').value;
            const message = document.getElementById('message').value;
            
            // Save to Firestore
            db.collection('contacts').add({
                name: name,
                email: email,
                message: message,
                timestamp: firebase.firestore.FieldValue.serverTimestamp()
            })
            .then(() => {
                alert('Message sent successfully!');
                document.getElementById('contactForm').reset();
            })
            .catch((error) => {
                console.error('Error adding document: ', error);
                alert('Error sending message. Please try again.');
            });
        });
    </script>
