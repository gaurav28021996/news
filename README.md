
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modern News Hub</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f5f6fa;
            color: #2c3e50;
        }

        header {
            background-color: #2c3e50;
            color: white;
            padding: 1rem;
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: bold;
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
            transform: translateY(-5px);
        }

        .news-image {
            width: 100%;
            height: 200px;
            object-fit: cover;
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
        }

        footer {
            background-color: #2c3e50;
            color: white;
            text-align: center;
            padding: 1rem;
            margin-top: 2rem;
        }

        @media (max-width: 768px) {
            main {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <header>
        <nav class="nav-container">
            <div class="logo">NewsHub</div>
            <div class="nav-links">
                <a href="#" style="color: white; text-decoration: none;">Home</a>
            </div>
        </nav>
    </header>

    <main>
        <section class="news-container" id="newsContainer">
            <!-- News articles will be inserted here by JavaScript -->
        </section>

        <aside class="sidebar">
            <div class="affiliate-section">
                <h3>Sponsored Content</h3>
                <a href="#" target="_blank">
                    <img src="placeholder-affiliate1.jpg" alt="Sponsor 1" class="affiliate-banner">
                </a>
                <a href="#" target="_blank">
                    <img src="placeholder-affiliate2.jpg" alt="Sponsor 2" class="affiliate-banner">
                </a>
            </div>
        </aside>
    </main>

    <footer>
        <p>© 2023 NewsHub. All rights reserved.</p>
        <div class="affiliate-links">
            <a href="#" style="color: #3498db; text-decoration: none;">Partner with us</a>
        </div>
    </footer>

    <script>
        // News API configuration
        const API_KEY = '9185d55dbda14e73bfb4c1a08e85b429';
        const NEWS_API_URL = `https://newsapi.org/v2/top-headlines?country=us&apiKey=${9185d55dbda14e73bfb4c1a08e85b429}`;

        // Affiliate marketing data
        const affiliateLinks = [
            {
                url: 'YOUR_AFFILIATE_LINK_1',
                image: 'affiliate-banner1.jpg',
                alt: 'Sponsor 1'
            },
            {
                url: 'YOUR_AFFILIATE_LINK_2',
                image: 'affiliate-banner2.jpg',
                alt: 'Sponsor 2'
            }
        ];

        // Fetch news articles
        async function fetchNews() {
            try {
                const response = await fetch(https://newsapi.org/v2/everything?' +
          'q=Apple&' +
          'from=2025-05-21&' +
          'sortBy=popularity&' +
          'apiKey=9185d55dbda14e73bfb4c1a08e85b429';);
                const data = await response.json();
                
var req = new Request(https://www.bbc.com/news);

fetch(req)
    .then(function(response) {
        console.log(response.json());
    })
                displayNews(data.articles);
            } catch (error) {
                console.error('Error fetching news:', error);
                newsContainer.innerHTML = '<p>Failed to load news. Please try again later.</p>';
            }
        }

        // Display news articles
        function displayNews(articles) {
            const newsContainer = document.getElementById('newsContainer');
            newsContainer.innerHTML = '';

            articles.forEach(article => {
                const newsCard = document.createElement('div');
                newsCard.className = 'news-card';
                newsCard.innerHTML = `
                    ${article.urlToImage ? `<img src="${article.urlToImage}" class="news-image" alt="${article.title}">` : ''}
                    <h2>${article.title}</h2>
                    <p>${article.description || ''}</p>
                    <a href="${article.url}" target="_blank">Read more</a>
                `;
                newsContainer.appendChild(newsCard);
            });
        }

        // Initialize affiliate banners
        function initAffiliates() {
            const affiliateSection = document.querySelector('.affiliate-section');
            affiliateLinks.forEach(link => {
                const banner = document.createElement('a');
                banner.href = link.url;
                banner.target = '_blank';
                banner.innerHTML = `<img src="${link.image}" alt="${link.alt}" class="affiliate-banner">`;
                affiliateSection.appendChild(banner);
            });
        }

        // Initialize the page
        document.addEventListener('DOMContentLoaded', () => {
            fetchNews();
            initAffiliates();
        });
    </script>
</body>
</html>
