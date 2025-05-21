
<html lang="en">
<head meta http-equiv="Content-Security-Policy" content="default-src 'self' newsapi.org;">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NewsHub - Modern News Blog</title>
    <meta name="description" content="Stay updated with the latest news and articles">
    <style>
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --background-color: #f5f6fa;
            --text-color: #2c3e50;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--background-color);
            color: var(--text-color);
            line-height: 1.6;
        }

        header {
            background-color: var(--primary-color);
            color: white;
            padding: 1rem;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 1rem;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: bold;
            color: white;
            text-decoration: none;
        }

        .search-container {
            flex: 1;
            max-width: 400px;
            min-width: 200px;
        }

        #searchInput {
            width: 100%;
            padding: 0.5rem 1rem;
            border-radius: 20px;
            border: 1px solid #ddd;
            background: rgba(255,255,255,0.1);
            color: white;
        }

        .category-filter {
            display: flex;
            gap: 0.5rem;
            margin: 1rem 0;
            flex-wrap: wrap;
            justify-content: center;
        }

        .category-btn {
            padding: 0.5rem 1.2rem;
            border: none;
            border-radius: 20px;
            background: var(--secondary-color);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .category-btn.active {
            background: var(--primary-color);
            transform: scale(1.05);
        }

        main {
            max-width: 1200px;
            margin: 2rem auto;
            padding: 0 1rem;
            display: grid;
            grid-template-columns: 3fr 1fr;
            gap: 2rem;
        }

        .news-card {
            background: white;
            border-radius: 10px;
            padding: 1.5rem;
            margin-bottom: 1.5rem;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
        }

        .news-card:hover {
            transform: translateY(-3px);
        }

        .news-image {
            width: 100%;
            height: 200px;
            object-fit: cover;
            border-radius: 5px;
            margin-bottom: 1rem;
        }

        .social-share {
            margin: 1rem 0;
            display: flex;
            gap: 0.5rem;
            flex-wrap: wrap;
        }

        .social-btn {
            padding: 0.5rem 1rem;
            border: none;
            border-radius: 5px;
            color: white;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            transition: opacity 0.3s ease;
        }

        .social-btn:hover {
            opacity: 0.9;
        }

        .facebook { background: #3b5998; }
        .twitter { background: #1da1f2; }
        .whatsapp { background: #25d366; }

        .comments-section {
            margin-top: 2rem;
            padding-top: 1rem;
            border-top: 1px solid #eee;
        }

        .comment-form {
            margin-bottom: 2rem;
        }

        .comment-input {
            width: 100%;
            padding: 0.8rem;
            margin: 0.5rem 0;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
        }

        .comment {
            background: #f8f9fa;
            padding: 1rem;
            margin: 1rem 0;
            border-radius: 5px;
        }

        .affiliate-section {
            background: white;
            padding: 1rem;
            border-radius: 10px;
            margin-bottom: 1.5rem;
        }

        .affiliate-banner {
            width: 100%;
            margin: 1rem 0;
            border-radius: 5px;
            transition: transform 0.3s ease;
        }

        .affiliate-banner:hover {
            transform: scale(1.02);
        }

        footer {
            background-color: var(--primary-color);
            color: white;
            text-align: center;
            padding: 2rem 1rem;
            margin-top: 3rem;
        }

        @media (max-width: 768px) {
            main {
                grid-template-columns: 1fr;
            }
            
            .nav-container {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <header>
        <nav class="nav-container">
            <a href="#" class="logo">NewsHub</a>
            <div class="search-container">
                <input type="text" id="searchInput" placeholder="Search news...">
            </div>
            <div class="category-filter" id="categoryFilter"></div>
        </nav>
    </header>

    <main>
        <section class="news-container" id="newsContainer">
            <!-- News articles loaded dynamically -->
        </section>

        <aside class="sidebar">
            <div class="affiliate-section">
                <h3>Recommended Products</h3>
                <!-- Affiliate banners loaded dynamically -->
            </div>
        </aside>
    </main>

    <footer>
        <p>© 2023 NewsHub. All rights reserved.</p>
        <p class="affiliate-disclosure">Disclosure: This site contains affiliate links to products. We may receive a commission for purchases made through these links.</p>
    </footer>

    <script>
        // Configuration
       // Make sure the API_KEY is properly referenced
const API_KEY = '9185d55dbda14e73bfb4c1a08e85b429'; // Keep as string
        const categories = ['general', 'business', 'technology', 'science', 'sports', 'entertainment', 'health'];
        let currentCategory = 'general';
        let currentSearchTerm = '';

        // Affiliate Data
        const affiliateLinks = [
            {
                url: 'YOUR_AFFILIATE_LINK_1',
                image: 'affiliate-banner1.jpg',
                alt: 'Tech Gadgets'
            },
            {
                url: 'YOUR_AFFILIATE_LINK_2',
                image: 'affiliate-banner2.jpg',
                alt: 'Book Store'
            }
        ];

        // Initialize Categories
        function initCategories() {
            const container = document.getElementById('categoryFilter');
            categories.forEach(category => {
                const btn = document.createElement('button');
                btn.className = 'category-btn';
                btn.textContent = category.charAt(0).toUpperCase() + category.slice(1);
                btn.addEventListener('click', () => setCategory(category));
                container.appendChild(btn);
            });
        }

        // Set Active Category
        function setCategory(category) {
            currentCategory = category;
            document.querySelectorAll('.category-btn').forEach(btn => {
                btn.classList.toggle('active', btn.textContent.toLowerCase() === category);
            });
            fetchNews();
        }

        // Search Functionality
        let searchTimeout;
        document.getElementById('searchInput').addEventListener('input', (e) => {
            clearTimeout(searchTimeout);
            currentSearchTerm = e.target.value.toLowerCase();
            searchTimeout = setTimeout(filterNews, 300);
        });

        function filterNews() {
            const cards = document.querySelectorAll('.news-card');
            cards.forEach(card => {
                const textContent = card.textContent.toLowerCase();
                card.style.display = textContent.includes(currentSearchTerm) ? 'block' : 'none';
            });
        }

        // Fetch News
        async function fetchNews() {
            try {
               // Modify the URL in fetchNews
const url = `https://cors-anywhere.herokuapp.com/https://newsapi.org/v2/top-headlines?country=in&category=${currentCategory}&apiKey=${API_KEY}`;
                const response = await fetch(url);
                const data = await response.json();
                displayNews(data.articles);
            } catch (error) {
                console.error('Error fetching news:', error);
                newsContainer.innerHTML = '<p class="error">Failed to load news. Please try again later.</p>';
            }
        }

        // Display News
        function displayNews(articles) {
            const newsContainer = document.getElementById('newsContainer');
            newsContainer.innerHTML = '';

            articles.forEach(article => {
                const articleId = btoa(article.url);
                const newsCard = document.createElement('article');
                newsCard.className = 'news-card';
                newsCard.innerHTML = `
                    ${article.urlToImage ? `
                    <img src="${article.urlToImage}" class="news-image" 
                         alt="${article.title}" loading="lazy">` : ''}
                    <h2>${article.title}</h2>
                    <p>${article.description || ''}</p>
                    <a href="${article.url}" target="_blank" rel="noopener">Read more</a>
                `;

                // Add Social Sharing
                const socialButtons = createSocialButtons(article.url, article.title);
                newsCard.appendChild(socialButtons);

                // Add Comments Section
                const commentsSection = createCommentsSection(articleId);
                newsCard.appendChild(commentsSection);

                newsContainer.appendChild(newsCard);
                loadComments(articleId);
            });
        }

        // Social Sharing
        function createSocialButtons(url, title) {
            const encodedUrl = encodeURIComponent(url);
            const encodedTitle = encodeURIComponent(title);
            
            const socialDiv = document.createElement('div');
            socialDiv.className = 'social-share';
            socialDiv.innerHTML = `
                <button class="social-btn facebook"
                    onclick="window.open('https://www.facebook.com/sharer/sharer.php?u=${encodedUrl}', '_blank')">
                    Share
                </button>
                <button class="social-btn twitter"
                    onclick="window.open('https://twitter.com/intent/tweet?text=${encodedTitle}&url=${encodedUrl}', '_blank')">
                    Tweet
                </button>
                <button class="social-btn whatsapp"
                    onclick="window.open('https://api.whatsapp.com/send?text=${encodedTitle} ${encodedUrl}', '_blank')">
                    WhatsApp
                </button>
            `;
            return socialDiv;
        }

        // Comments System
        function createCommentsSection(articleId) {
            const section = document.createElement('div');
            section.className = 'comments-section';
            section.innerHTML = `
                <h3>Comments</h3>
                <form class="comment-form" onsubmit="postComment(event, '${articleId}')">
                    <input type="text" class="comment-input" placeholder="Your name" required>
                    <textarea class="comment-input" placeholder="Your comment" rows="3" required></textarea>
                    <button type="submit" class="category-btn">Post Comment</button>
                </form>
                <div id="comments-${articleId}" class="comments-list"></div>
            `;
            return section;
        }

        function postComment(event, articleId) {
            event.preventDefault();
            const form = event.target;
            const formData = new FormData(form);
            const comment = {
                id: Date.now(),
                userName: formData.get('username') || 'Anonymous',
                commentText: formData.get('comment'),
                timestamp: new Date().toISOString()
            };

            const comments = JSON.parse(localStorage.getItem(articleId) || [];
            comments.push(comment);
            localStorage.setItem(articleId, JSON.stringify(comments));
            form.reset();
            loadComments(articleId);
        }

        function loadComments(articleId) {
            const container = document.getElementById(`comments-${articleId}`);
            const comments = JSON.parse(localStorage.getItem(articleId)) || [];
            container.innerHTML = comments.map(comment => `
                <div class="comment">
                    <strong>${comment.userName}</strong>
                    <p>${comment.commentText}</p>
                    <small>${new Date(comment.timestamp).toLocaleString()}</small>
                </div>
            `).join('');
        }

        // Initialize Affiliates
        function initAffiliates() {
            const section = document.querySelector('.affiliate-section');
            affiliateLinks.forEach(link => {
                const banner = document.createElement('a');
                banner.href = link.url;
                banner.target = '_blank';
                banner.rel = 'noopener';
                banner.innerHTML = `
                    <img src="${link.image}" 
                         alt="${link.alt}" 
                         class="affiliate-banner" 
                         loading="lazy">
                `;
                section.appendChild(banner);
            });
        }

        // Initialize App
        document.addEventListener('DOMContentLoaded', () => {
            initCategories();
            initAffiliates();
            setCategory('general');
            fetchNews();
        });
    </script>
</body>
</html>
