<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OptiShop | Optimized E-Commerce</title>
    <style>
        /* Global Reset & Base */
        :root {
            --primary: #2563eb;
            --primary-hover: #1d4ed8;
            --secondary: #6b7280;
            --light: #f9fafb;
            --dark: #1f2937;
            --success: #10b981;
            --shadow: 0 4px 6px -1px rgba(0,0,0,0.1),0 2px 4px -1px rgba(0,0,0,0.06);
        }
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            line-height: 1.5;
            color: var(--dark);
            background-color: var(--light);
        }
        
        /* Layout Utilities */
        .container {
            width: 100%;
            max-width: 1280px;
            margin: 0 auto;
            padding: 0 1rem;
        }
        .grid {
            display: grid;
            gap: 1.5rem;
        }
        .grid-cols-2 {
            grid-template-columns: repeat(2, 1fr);
        }
        .grid-cols-3 {
            grid-template-columns: repeat(3, 1fr);
        }
        .flex {
            display: flex;
        }
        .items-center {
            align-items: center;
        }
        .justify-between {
            justify-content: space-between;
        }
        .gap-2 {
            gap: 0.5rem;
        }
        .gap-4 {
            gap: 1rem;
        }

        /* Components */
        header {
            background-color: white;
            box-shadow: var(--shadow);
            position: sticky;
            top: 0;
            z-index: 100;
        }
        .nav-logo {
            font-weight: 700;
            font-size: 1.25rem;
            color: var(--primary);
        }
        .nav-cart {
            position: relative;
        }
        .cart-count {
            position: absolute;
            top: -0.5rem;
            right: -0.5rem;
            background: var(--primary);
            color: white;
            border-radius: 50%;
            width: 1.25rem;
            height: 1.25rem;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.75rem;
        }
        .hero {
            background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), url('https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/6c7ceb31-f4bf-4eeb-91a9-adea91962caf.png') center/cover no-repeat;
            color: white;
            min-height: 400px;
            display: flex;
            align-items: center;
        }
        .hero-content {
            max-width: 600px;
        }
        .hero-title {
            font-size: 2.5rem;
            margin-bottom: 1rem;
        }
        .btn {
            display: inline-block;
            padding: 0.5rem 1rem;
            border-radius: 0.25rem;
            font-weight: 600;
            cursor: pointer;
            border: none;
            transition: all 0.2s ease;
        }
        .btn-primary {
            background: var(--primary);
            color: white;
        }
        .btn-primary:hover {
            background: var(--primary-hover);
        }
        .btn-outline {
            background: transparent;
            border: 1px solid white;
            color: white;
        }
        .btn-outline:hover {
            background: white;
            color: var(--dark);
        }
        .section-title {
            font-size: 1.5rem;
            margin-bottom: 2rem;
            position: relative;
            padding-bottom: 0.5rem;
        }
        .section-title::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 80px;
            height: 4px;
            background: var(--primary);
        }
        .product-card {
            background: white;
            border-radius: 0.5rem;
            overflow: hidden;
            box-shadow: var(--shadow);
            transition: transform 0.2s ease;
        }
        .product-card:hover {
            transform: translateY(-5px);
        }
        .product-img {
            width: 100%;
            aspect-ratio: 1/1;
            object-fit: cover;
            background: #f3f4f6;
        }
        .product-body {
            padding: 1rem;
        }
        .product-title {
            font-weight: 600;
            margin-bottom: 0.5rem;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        .product-price {
            font-weight: 700;
            color: var(--primary);
            margin-bottom: 1rem;
        }
        .filter-controls {
            margin-bottom: 2rem;
        }
        .filter-btn {
            background: white;
            border: 1px solid #d1d5db;
            padding: 0.5rem 1rem;
            border-radius: 0.25rem;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        .filter-btn.active {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
        }
        .cart-overlay {
            position: fixed;
            top: 0;
            right: 0;
            width: 100%;
            max-width: 400px;
            height: 100vh;
            background: white;
            box-shadow: -5px 0 15px rgba(0,0,0,0.1);
            transform: translateX(100%);
            transition: transform 0.3s ease;
            z-index: 1000;
            padding: 1.5rem;
            overflow-y: auto;
        }
        .cart-overlay.active {
            transform: translateX(0);
        }
        .cart-header {
            margin-bottom: 1.5rem;
        }
        .cart-item {
            display: flex;
            gap: 1rem;
            margin-bottom: 1.5rem;
            padding-bottom: 1.5rem;
            border-bottom: 1px solid #e5e7eb;
        }
        .cart-item-img {
            width: 80px;
            height: 80px;
            object-fit: cover;
            border-radius: 0.25rem;
        }
        .cart-item-details {
            flex-grow: 1;
        }
        .cart-item-title {
            font-weight: 600;
            margin-bottom: 0.25rem;
        }
        .cart-item-price {
            color: var(--secondary);
            margin-bottom: 0.5rem;
        }
        .cart-item-remove {
            color: #ef4444;
            background: none;
            border: none;
            cursor: pointer;
        }
        .cart-total {
            margin-top: 1.5rem;
            font-weight: 700;
            font-size: 1.25rem;
            padding-top: 1.5rem;
            border-top: 1px solid #e5e7eb;
        }
        .overlay-backdrop {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100vh;
            background: rgba(0,0,0,0.5);
            z-index: 999;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s ease;
        }
        .overlay-backdrop.active {
            opacity: 1;
            pointer-events: all;
        }

        /* Responsive */
        @media (max-width: 1024px) {
            .grid-cols-3 {
                grid-template-columns: repeat(2, 1fr);
            }
        }
        @media (max-width: 640px) {
            .grid-cols-2, .grid-cols-3 {
                grid-template-columns: 1fr;
            }
            .hero-title {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <!-- Header/Navbar -->
    <header>
        <div class="container">
            <nav class="flex items-center justify-between py-4">
                <div class="nav-logo">OptiShop</div>
                <button class="nav-cart flex items-center gap-2">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                        <circle cx="9" cy="21" r="1"></circle>
                        <circle cx="20" cy="21" r="1"></circle>
                        <path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"></path>
                    </svg>
                    <span class="cart-count">0</span>
                </button>
            </nav>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero">
        <div class="container">
            <div class="hero-content">
                <h1 class="hero-title">Your Perfect Tech Gear Awaits</h1>
                <p>Discover our optimized selection of high-performance electronics with fast shipping and easy returns.</p>
                <div class="flex gap-4 mt-6">
                    <a href="#products" class="btn btn-primary">Shop Now</a>
                    <button class="btn btn-outline">Learn More</button>
                </div>
            </div>
        </div>
    </section>

    <!-- Products Section -->
    <section id="products" class="py-16">
        <div class="container">
            <h2 class="section-title">Featured Products</h2>
            
            <div class="filter-controls flex gap-2 mb-6">
                <button class="filter-btn active" data-category="all">All</button>
                <button class="filter-btn" data-category="laptops">Laptops</button>
                <button class="filter-btn" data-category="phones">Phones</button>
                <button class="filter-btn" data-category="accessories">Accessories</button>
            </div>
            
            <div class="grid grid-cols-3" id="products-grid">
                <!-- Products will be dynamically inserted here -->
            </div>
        </div>
    </section>

    <!-- Cart Overlay -->
    <div class="overlay-backdrop"></div>
    <div class="cart-overlay">
        <div class="cart-header">
            <h3 class="section-title">Your Cart</h3>
            <button class="cart-close">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <line x1="18" y1="6" x2="6" y2="18"></line>
                    <line x1="6" y1="6" x2="18" y2="18"></line>
                </svg>
            </button>
        </div>
        
        <div id="cart-items">
            <!-- Cart items will be inserted here -->
            <div class="empty-cart-message">
                <p>Your cart is empty</p>
            </div>
        </div>
        
        <div class="cart-total flex justify-between">
            <span>Total:</span>
            <span id="cart-total-price">$0.00</span>
        </div>
        
        <button class="btn btn-primary w-full mt-4">Checkout</button>
    </div>

    <script>
        // Product Data
        const products = [
            {
                id: 1,
                title: "UltraBook Pro X1",
                price: 1299,
                category: "laptops",
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/0e305cf5-b26d-4558-a55a-ad519414efcc.png",
                alt: "Sleek silver UltraBook Pro X1 laptop with illuminated keyboard on wooden desk"
            },
            {
                id: 2,
                title: "Gaming Beast RTX",
                price: 1799,
                category: "laptops",
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/ed6b4f79-984a-46c4-8f46-0cd82c622666.png",
                alt: "Powerful gaming laptop with RGB keyboard and high refresh rate display"
            },
            {
                id: 3,
                title: "Phoenix 12 Pro",
                price: 999,
                category: "phones",
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/39a9a9d7-111f-47a7-b966-63e7d0a00bcf.png",
                alt: "Latest Phoenix 12 Pro smartphone with edge-to-edge OLED display"
            },
            {
                id: 4,
                title: "Nebula Air",
                price: 799,
                category: "phones",
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/4ee6baaa-80ab-4f8a-a097-27002b2f2467.png",
                alt: "Slim Nebula Air smartphone in matte black with triple camera setup"
            },
            {
                id: 5,
                title: "Quantum TWS Earbuds",
                price: 149,
                category: "accessories",
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/18e89204-1fb3-4c9f-9cfd-d8f2c7990e96.png",
                alt: "Wireless Quantum earbuds in charging case with LED battery indicator"
            },
            {
                id: 6,
                title: "Turbo Charger 65W",
                price: 49,
                category: "accessories",
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/91afd169-75af-457f-a706-1601ddb9fe2f.png",
                alt: "Compact 65W USB-C fast charger with foldable prongs for travel"
            }
        ];

        // DOM Elements
        const productsGrid = document.getElementById('products-grid');
        const filterBtns = document.querySelectorAll('.filter-btn');
        const navCart = document.querySelector('.nav-cart');
        const cartOverlay = document.querySelector('.cart-overlay');
        const overlayBackdrop = document.querySelector('.overlay-backdrop');
        const cartItemsContainer = document.getElementById('cart-items');
        const cartTotalPrice = document.getElementById('cart-total-price');
        const cartClose = document.querySelector('.cart-close');
        const cartCount = document.querySelector('.cart-count');

        // State
        let cart = [];
        let currentCategory = 'all';

        // Initialize
        function init() {
            renderProducts();
            setupEventListeners();
        }

        // Event Listeners
        function setupEventListeners() {
            // Filter buttons
            filterBtns.forEach(btn => {
                btn.addEventListener('click', () => {
                    filterBtns.forEach(b => b.classList.remove('active'));
                    btn.classList.add('active');
                    currentCategory = btn.dataset.category;
                    renderProducts();
                });
            });

            // Cart toggle
            navCart.addEventListener('click', toggleCart);
            cartClose.addEventListener('click', toggleCart);
            overlayBackdrop.addEventListener('click', toggleCart);
        }

        // Render Products
        function renderProducts() {
            productsGrid.innerHTML = '';
            
            const filteredProducts = currentCategory === 'all' 
                ? products 
                : products.filter(p => p.category === currentCategory);
            
            filteredProducts.forEach(product => {
                const productEl = document.createElement('div');
                productEl.className = 'product-card';
                productEl.innerHTML = `
                    <div class="product-img-container">
                        <img 
                            src="${product.image}" 
                            alt="${product.alt}" 
                            class="product-img" 
                            loading="lazy"
                            onerror="this.src='https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/380951c7-767b-47f2-9640-5af3af5c4679.png'"
                        >
                    </div>
                    <div class="product-body">
                        <h3 class="product-title">${product.title}</h3>
                        <p class="product-price">$${product.price.toFixed(2)}</p>
                        <button class="btn btn-primary w-full add-to-cart" data-id="${product.id}">
                            Add to Cart
                        </button>
                    </div>
                `;
                productsGrid.appendChild(productEl);
            });

            // Add to cart buttons
            document.querySelectorAll('.add-to-cart').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    const productId = parseInt(e.target.dataset.id);
                    addToCart(productId);
                });
            });
        }

        // Cart Functions
        function toggleCart() {
            cartOverlay.classList.toggle('active');
            overlayBackdrop.classList.toggle('active');
            
            if (cartOverlay.classList.contains('active')) {
                renderCart();
            }
        }

        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            const existingItem = cart.find(item => item.id === productId);
            
            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({...product, quantity: 1});
            }
            
            updateCartCount();
            
            // Show feedback
            const btn = document.querySelector(`.add-to-cart[data-id="${productId}"]`);
            btn.textContent = 'Added!';
            setTimeout(() => {
                btn.textContent = 'Add to Cart';
            }, 2000);
        }

        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            updateCartCount();
            renderCart();
        }

        function updateCartCount() {
            const count = cart.reduce((total, item) => total + item.quantity, 0);
            cartCount.textContent = count;
        }

        function renderCart() {
            if (cart.length === 0) {
                cartItemsContainer.innerHTML = `
                    <div class="empty-cart-message">
                        <p>Your cart is empty</p>
                    </div>
                `;
                cartTotalPrice.textContent = '$0.00';
                return;
            }
            
            cartItemsContainer.innerHTML = '';
            
            let total = 0;
            cart.forEach(item => {
                total += item.price * item.quantity;
                
                const cartItem = document.createElement('div');
                cartItem.className = 'cart-item';
                cartItem.innerHTML = `
                    <img src="${item.image}" alt="${item.alt}" class="cart-item-img" loading="lazy">
                    <div class="cart-item-details">
                        <h4 class="cart-item-title">${item.title}</h4>
                        <p class="cart-item-price">$${item.price.toFixed(2)} x ${item.quantity}</p>
                        <button class="cart-item-remove" data-id="${item.id}">Remove</button>
                    </div>
                `;
                cartItemsContainer.appendChild(cartItem);
            });
            
            cartTotalPrice.textContent = `$${total.toFixed(2)}`;
            
            // Remove item buttons
            document.querySelectorAll('.cart-item-remove').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    const productId = parseInt(e.target.dataset.id);
                    removeFromCart(productId);
                });
            });
        }

        // Initialize the app
        init();
    </script>
</body>
</html>

