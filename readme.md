<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DropShip Pro | Your Next Big Idea</title>
    <!-- Load Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Use Inter font -->
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f7f7f7; /* Light background for the overall page */
        }
        /* Custom scrollbar for cart sidebar */
        .cart-content::-webkit-scrollbar {
            width: 8px;
        }
        .cart-content::-webkit-scrollbar-thumb {
            background-color: #a8a29e;
            border-radius: 4px;
        }
        .ai-result p { margin-bottom: 1rem; }
        .ai-result ul { list-style: disc; margin-left: 1.5rem; }
        /* Adjusted for the new, structured AI output */
        .ai-result h4 { font-weight: 700; font-size: 1.125rem; margin-top: 1.5rem; margin-bottom: 0.5rem; color: #4f46e5; }
    </style>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'primary': '#4f46e5', // Indigo
                        'secondary': '#1f2937', // Dark Slate
                    },
                }
            }
        }
    </script>
</head>
<body class="text-gray-800">

    <!-- Cart Sidebar (Hidden by default) -->
    <div id="cart-sidebar" class="fixed top-0 right-0 w-full md:w-96 h-full bg-white shadow-2xl transform translate-x-full transition-transform duration-300 z-50 flex flex-col">
        <!-- Cart Header -->
        <div class="p-4 border-b flex justify-between items-center bg-secondary text-white rounded-t-lg">
            <h2 class="text-xl font-bold">Your Cart</h2>
            <button onclick="toggleCart()" class="text-white hover:text-gray-200 focus:outline-none">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                </svg>
            </button>
        </div>

        <!-- Cart Items -->
        <div id="cart-items" class="p-4 flex-grow overflow-y-auto cart-content space-y-4">
            <!-- Cart items will be injected here by JavaScript -->
            <p class="text-gray-500 text-center py-8">Your cart is empty.</p>
        </div>

        <!-- Cart Footer / Total -->
        <div class="p-4 border-t bg-gray-50 rounded-b-lg">
            <div class="flex justify-between items-center text-lg font-semibold mb-3">
                <span>Total:</span>
                <span id="cart-total">$0.00</span>
            </div>
            <button class="w-full bg-primary text-white py-3 rounded-xl font-bold hover:bg-indigo-600 transition duration-150 shadow-md">
                Proceed to Checkout
            </button>
        </div>
    </div>
    <!-- Cart Overlay -->
    <div id="cart-overlay" class="fixed inset-0 bg-black bg-opacity-50 hidden z-40" onclick="toggleCart()"></div>
    
    <!-- Main Content Wrapper -->
    <div class="min-h-screen flex flex-col">
        <!-- Header/Navigation -->
        <header class="bg-white shadow-md sticky top-0 z-30">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex justify-between items-center h-16">
                    <!-- Logo/Brand -->
                    <a href="#" class="flex-shrink-0 text-2xl font-extrabold text-secondary hover:text-primary transition duration-150">
                        DropShip<span class="text-primary">Pro</span>
                    </a>
                    
                    <!-- Desktop Links -->
                    <nav class="hidden md:flex space-x-8">
                        <a href="#hero" class="text-gray-600 hover:text-primary transition duration-150 font-medium">Home</a>
                        <a href="#products" class="text-gray-600 hover:text-primary transition duration-150 font-medium">Shop All</a>
                        <a href="#ai-tool" class="text-gray-600 hover:text-primary transition duration-150 font-medium">AI Product Finder</a>
                        <a href="#" class="text-gray-600 hover:text-primary transition duration-150 font-medium">Contact</a>
                    </nav>

                    <!-- Cart Button -->
                    <button onclick="toggleCart()" class="relative text-gray-600 hover:text-primary transition duration-150 p-2 rounded-full hover:bg-gray-100">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" />
                        </svg>
                        <span id="cart-count" class="absolute top-0 right-0 inline-flex items-center justify-center px-2 py-1 text-xs font-bold leading-none text-red-100 transform translate-x-1/2 -translate-y-1/2 bg-red-600 rounded-full">0</span>
                    </button>
                </div>
            </div>
        </header>

        <!-- Hero Section -->
        <section id="hero" class="bg-secondary text-white py-20 sm:py-32 flex-shrink-0">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
                <h1 class="text-4xl sm:text-6xl font-extrabold tracking-tight mb-4">
                    The Future of Commerce is Here.
                </h1>
                <p class="text-xl sm:text-2xl text-gray-300 mb-8 max-w-3xl mx-auto">
                    Curated. Quality. Delivered. Discover the best dropshipping products, handpicked just for you.
                </p>
                <a href="#products" class="inline-block bg-primary text-white text-lg font-semibold px-8 py-3 rounded-xl shadow-lg hover:bg-indigo-600 transition duration-300 transform hover:scale-105">
                    Start Shopping Now
                </a>
            </div>
        </section>

        <!-- Products Section -->
        <main id="products" class="flex-grow py-12 md:py-20">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <h2 class="text-3xl font-bold text-center mb-10 text-secondary">Featured Products</h2>
                
                <!-- Product Grid -->
                <div id="product-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8">
                    <!-- Product cards will be injected here by JavaScript -->
                    <div class="col-span-full text-center py-10 text-gray-500" id="loading-indicator">
                        Loading products...
                    </div>
                </div>
            </div>

            <!-- AI Tool Section (Updated Feature: Product Finder) -->
            <section id="ai-tool" class="mt-20 pt-10 border-t border-gray-200">
                <div class="max-w-4xl mx-auto bg-white p-6 sm:p-8 rounded-xl shadow-2xl">
                    <h2 class="text-3xl font-bold text-center mb-6 text-primary">AI Product Sourcing Tool</h2>
                    <p class="text-center text-gray-600 mb-8">Let AI find your next winning dropshipping product by analyzing current market trends and criteria.</p>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <!-- Input Column -->
                        <div class="space-y-4">
                            <div>
                                <label for="product-niche" class="block text-sm font-medium text-gray-700">Target Niche/Market</label>
                                <input type="text" id="product-niche" class="mt-1 block w-full border border-gray-300 rounded-lg shadow-sm p-3 focus:ring-primary focus:border-primary" placeholder="e.g., Sustainable Home Goods or Pet Tech">
                            </div>
                            <div>
                                <label for="product-price" class="block text-sm font-medium text-gray-700">Desired Wholesale Price Range</label>
                                <input type="text" id="product-price" class="mt-1 block w-full border border-gray-300 rounded-lg shadow-sm p-3 focus:ring-primary focus:border-primary" placeholder="e.g., $10 - $30 or High-Ticket">
                            </div>
                            <div>
                                <label for="product-criteria" class="block text-sm font-medium text-gray-700">Key Criteria (e.g., High-margin, Lightweight, Problem-solving)</label>
                                <textarea id="product-criteria" rows="4" class="mt-1 block w-full border border-gray-300 rounded-lg shadow-sm p-3 focus:ring-primary focus:border-primary" placeholder="e.g., Must solve a common household problem, easy to ship, low return rate."></textarea>
                            </div>
                            <button onclick="findProduct()" class="w-full bg-secondary text-white py-3 rounded-xl font-bold hover:bg-gray-700 transition duration-150 shadow-lg flex items-center justify-center" id="find-button">
                                <span id="find-text">Find Product Idea</span>
                                <svg id="spinner" class="animate-spin -ml-1 mr-3 h-5 w-5 text-white hidden" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                                    <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                                    <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                                </svg>
                            </button>
                        </div>
                        
                        <!-- Output Column -->
                        <div class="bg-gray-50 p-5 rounded-xl border border-gray-200 shadow-inner">
                            <h3 class="text-lg font-semibold mb-3 text-secondary">AI Market Analysis:</h3>
                            <div id="ai-output" class="text-sm text-gray-700 min-h-[200px] ai-result">
                                <p class="text-gray-500 italic">Input your product criteria and click 'Find Product Idea' to receive a detailed market analysis and product recommendation.</p>
                            </div>
                            <div id="ai-sources" class="mt-4 pt-3 border-t border-gray-200 text-xs text-gray-500">
                                <!-- Sources will be displayed here -->
                            </div>
                        </div>
                    </div>

                </div>
            </section>
            <!-- End AI Tool Section -->

        </main>

        <!-- Footer -->
        <footer class="bg-secondary text-white mt-auto">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10">
                <div class="grid grid-cols-2 md:grid-cols-4 gap-8 mb-8">
                    <!-- Company Info -->
                    <div>
                        <h4 class="text-xl font-bold mb-4 text-primary">DropShipPro</h4>
                        <p class="text-gray-400 text-sm">
                            Quality products delivered directly to your door, hassle-free.
                        </p>
                    </div>

                    <!-- Quick Links -->
                    <div>
                        <h4 class="font-semibold text-lg mb-4">Quick Links</h4>
                        <ul class="space-y-2 text-sm">
                            <li><a href="#" class="text-gray-400 hover:text-white transition duration-150">Shop</a></li>
                            <li><a href="#" class="text-gray-400 hover:text-white transition duration-150">FAQ</a></li>
                            <li><a href="#" class="text-gray-400 hover:text-white transition duration-150">Shipping & Returns</a></li>
                        </ul>
                    </div>

                    <!-- Contact -->
                    <div>
                        <h4 class="font-semibold text-lg mb-4">Get In Touch</h4>
                        <p class="text-gray-400 text-sm">Email: <a href="mailto:support@dropshippro.com" class="hover:text-primary">support@dropshippro.com</a></p>
                        <p class="text-gray-400 text-sm">Phone: +1 (555) 123-4567</p>
                    </div>
                </div>

                <div class="border-t border-gray-700 pt-6 text-center text-sm text-gray-500">
                    &copy; 2025 DropShipPro. All rights reserved.
                </div>
            </div>
        </footer>
    </div>

    <!-- JavaScript for Product and Cart Logic -->
    <script>
        const products = [
            { id: 1, name: "Minimalist Commuter Backpack", price: 79.99, image: "https://placehold.co/400x300/4f46e5/ffffff?text=Backpack", description: "Sleek, waterproof, and designed for the modern professional." },
            { id: 2, name: "Zen Noise-Canceling Headphones", price: 149.99, image: "https://placehold.co/400x300/4f46e5/ffffff?text=Headphones", description: "Immerse yourself in pure sound with industry-leading cancellation." },
            { id: 3, name: "Smart Temperature Control Mug", price: 59.99, image: "https://placehold.co/400x300/4f46e5/ffffff?text=Smart+Mug", description: "Keep your coffee perfectly hot for hours." },
            { id: 4, name: "Aromatherapy Mist Diffuser", price: 34.50, image: "https://placehold.co/400x300/4f46e5/ffffff?text=Diffuser", description: "Ultrasonic technology for a calming, fragrant environment." },
            { id: 5, name: "15W Fast Wireless Charging Pad", price: 29.00, image: "https://placehold.co/400x300/4f46e5/ffffff?text=Charger", description: "Charge your devices at lightning speed, cable-free." },
            { id: 6, name: "Portable Handheld Espresso Maker", price: 89.99, image: "https://placehold.co/400x300/4f46e5/ffffff?text=Espresso", description: "Enjoy a rich shot of espresso anywhere, anytime." },
            { id: 7, name: "Ergonomic Memory Foam Pillow", price: 45.99, image: "https://placehold.co/400x300/4f46e5/ffffff?text=Pillow", description: "The perfect balance of support and comfort for deep sleep." },
            { id: 8, name: "Professional LED Ring Light Kit", price: 65.00, image: "https://placehold.co/400x300/4f46e5/ffffff?text=Ring+Light", description: "Studio-quality lighting for video conferencing and streaming." },
        ];

        let cart = []; // Stores { id: productId, quantity: number, price: number, name: string }

        const productGrid = document.getElementById('product-grid');
        const cartItemsContainer = document.getElementById('cart-items');
        const cartTotalDisplay = document.getElementById('cart-total');
        const cartCountDisplay = document.getElementById('cart-count');
        const cartSidebar = document.getElementById('cart-sidebar');
        const cartOverlay = document.getElementById('cart-overlay');
        
        // --- Gemini API Configuration ---
        const apiKey = "";
        const modelName = 'gemini-2.5-flash-preview-09-2025';
        const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/${modelName}:generateContent?key=${apiKey}`;
        const SYSTEM_PROMPT = "You are an expert dropshipping market analyst. Your task is to identify one highly profitable, trending product idea based on the user's input. Provide a comprehensive analysis in Markdown, structured with clear headings (using '####'): 'Product Idea', 'Market Analysis & Trend Justification', and 'Sourcing Keywords & Pricing Strategy'. The response must be detailed and data-driven. Do not use conversational phrases like 'as an AI language model'.";


        // --- Utility Functions ---

        // Exponential backoff retry function for API calls
        const retryFetch = async (url, options = {}, maxRetries = 5, delay = 1000) => {
            for (let i = 0; i < maxRetries; i++) {
                try {
                    const response = await fetch(url, options);
                    if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
                    return response;
                } catch (error) {
                    if (i === maxRetries - 1) throw error;
                    // console.log(`Attempt ${i + 1} failed. Retrying in ${delay}ms...`);
                    await new Promise(resolve => setTimeout(resolve, delay));
                    delay *= 2; // Exponential backoff
                }
            }
        };

        const formatCurrency = (amount) => `$${amount.toFixed(2)}`;

        // Function to convert Markdown to HTML for display
        const markdownToHtml = (markdown) => {
            // Updated for new structure: H4 for headings
            let html = markdown
                .replace(/^#### (.*$)/gim, '<h4>$1</h4>') // H4 for strong headings
                .replace(/\*\*(.*)\*\*/gim, '<strong>$1</strong>') // Bold
                .replace(/\*(.*)\*/gim, '<em>$1</em>') // Italic
                .replace(/^- (.*$)/gim, '<li>$1</li>') // List items
                .replace(/^(?!<h|<ul|<li).*$/gim, '<p>$&</p>'); // Paragraphs (anything not starting with a tag)

            // Wrap li elements in ul
            if (html.includes('<li>')) {
                // Ensure ul wraps all li's properly
                html = html.replace(/(<li>.*<\/li>)/gs, '<ul>$1</ul>');
            }

            return html;
        };

        // --- AI Generation Logic (Product Finder) ---

        const findProduct = async () => {
            const nicheInput = document.getElementById('product-niche').value.trim();
            const priceInput = document.getElementById('product-price').value.trim();
            const criteriaInput = document.getElementById('product-criteria').value.trim();
            
            const outputDiv = document.getElementById('ai-output');
            const sourcesDiv = document.getElementById('ai-sources');
            const findButton = document.getElementById('find-button');
            const spinner = document.getElementById('spinner');

            if (!nicheInput && !criteriaInput) {
                outputDiv.innerHTML = '<p class="text-red-500 font-semibold">Please enter a Target Niche or some Key Criteria.</p>';
                return;
            }

            // UI feedback: Disable button and show spinner
            findButton.disabled = true;
            spinner.classList.remove('hidden');
            document.getElementById('find-text').textContent = 'Searching Market...';
            outputDiv.innerHTML = '<p class="text-center text-gray-500 italic">Analyzing current trends and criteria...</p>';
            sourcesDiv.innerHTML = '';


            const userQuery = `Find one highly profitable product idea in the niche "${nicheInput || 'any niche'}" with a price range of "${priceInput || 'any price range'}" and matching the following criteria: "${criteriaInput || 'general market appeal'}". Provide a full dropshipping analysis.`;
            
            const payload = {
                contents: [{ parts: [{ text: userQuery }] }],
                // Use Google Search grounding for up-to-date and contextual information
                tools: [{ "google_search": {} }], 
                systemInstruction: {
                    parts: [{ text: SYSTEM_PROMPT }]
                },
            };

            try {
                const response = await retryFetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                const result = await response.json();
                const candidate = result.candidates?.[0];

                if (candidate && candidate.content?.parts?.[0]?.text) {
                    const generatedText = candidate.content.parts[0].text;
                    
                    // Convert markdown response to HTML for display
                    outputDiv.innerHTML = markdownToHtml(generatedText);

                    // Extract and display grounding sources
                    let sources = [];
                    const groundingMetadata = candidate.groundingMetadata;
                    if (groundingMetadata && groundingMetadata.groundingAttributions) {
                        sources = groundingMetadata.groundingAttributions
                            .map(attribution => ({
                                uri: attribution.web?.uri,
                                title: attribution.web?.title,
                            }))
                            .filter(source => source.uri && source.title);
                    }

                    if (sources.length > 0) {
                        sourcesDiv.innerHTML = '<strong>Sources Used (for grounding):</strong><ul class="list-disc ml-4 mt-1">';
                        sources.slice(0, 3).forEach((source, index) => { // Limit to 3 sources for clean UI
                            sourcesDiv.innerHTML += `<li><a href="${source.uri}" target="_blank" class="text-primary hover:underline">${source.title}</a></li>`;
                        });
                        sourcesDiv.innerHTML += '</ul>';
                    } else {
                        sourcesDiv.innerHTML = '<p>No external sources were needed for this analysis.</p>';
                    }

                } else {
                    outputDiv.innerHTML = '<p class="text-red-500 font-semibold">Error: Could not find a product. Please check the API response structure.</p>';
                }
            } catch (error) {
                console.error("Gemini API Error:", error);
                outputDiv.innerHTML = `<p class="text-red-500 font-semibold">API Request Failed: ${error.message}. Check console for details.</p>`;
            } finally {
                // UI feedback: Reset button state
                findButton.disabled = false;
                spinner.classList.add('hidden');
                document.getElementById('find-text').textContent = 'Find Product Idea';
            }
        };

        // --- Cart Management ---

        const calculateCartTotals = () => {
            let total = 0;
            let count = 0;
            cart.forEach(item => {
                total += item.price * item.quantity;
                count += item.quantity;
            });
            cartTotalDisplay.textContent = formatCurrency(total);
            cartCountDisplay.textContent = count;
        };

        const renderCart = () => {
            cartItemsContainer.innerHTML = '';
            
            if (cart.length === 0) {
                cartItemsContainer.innerHTML = '<p class="text-gray-500 text-center py-8">Your cart is empty.</p>';
            } else {
                cart.forEach(item => {
                    const product = products.find(p => p.id === item.id);
                    const itemElement = document.createElement('div');
                    itemElement.className = 'flex items-center space-x-4 p-3 bg-gray-50 rounded-lg shadow-sm';
                    itemElement.innerHTML = `
                        <img src="${product?.image}" onerror="this.onerror=null;this.src='https://placehold.co/60x60/cccccc/000000?text=Item';" class="w-16 h-16 object-cover rounded-md flex-shrink-0" alt="${item.name}">
                        <div class="flex-grow">
                            <h4 class="font-semibold text-gray-800">${item.name}</h4>
                            <p class="text-sm text-primary font-medium">${formatCurrency(item.price)}</p>
                        </div>
                        <div class="flex items-center space-x-2">
                            <button onclick="updateCartItemQuantity(${item.id}, -1)" class="w-6 h-6 bg-gray-200 text-gray-700 rounded-full hover:bg-gray-300 transition duration-150 flex items-center justify-center text-lg">-</button>
                            <span class="font-bold w-4 text-center">${item.quantity}</span>
                            <button onclick="updateCartItemQuantity(${item.id}, 1)" class="w-6 h-6 bg-gray-200 text-gray-700 rounded-full hover:bg-gray-300 transition duration-150 flex items-center justify-center text-lg">+</button>
                        </div>
                    `;
                    cartItemsContainer.appendChild(itemElement);
                });
            }
            calculateCartTotals();
        };

        const updateCartItemQuantity = (productId, change) => {
            const existingItem = cart.find(item => item.id === productId);

            if (existingItem) {
                existingItem.quantity += change;

                if (existingItem.quantity <= 0) {
                    // Remove item if quantity is zero or less
                    cart = cart.filter(item => item.id !== productId);
                }
            }
            renderCart();
        };

        const addToCart = (productId) => {
            const product = products.find(p => p.id === productId);
            if (!product) return;

            const existingItem = cart.find(item => item.id === productId);

            if (existingItem) {
                existingItem.quantity += 1;
            } else {
                cart.push({
                    id: product.id,
                    name: product.name,
                    price: product.price,
                    quantity: 1
                });
            }
            renderCart();
            toggleCart(true); // Open cart sidebar when item is added
        };

        const toggleCart = (forceOpen = false) => {
            const isOpen = cartSidebar.classList.contains('translate-x-0');
            
            if (forceOpen || !isOpen) {
                cartSidebar.classList.remove('translate-x-full');
                cartSidebar.classList.add('translate-x-0');
                cartOverlay.classList.remove('hidden');
                document.body.classList.add('overflow-hidden'); // Prevent scrolling body when cart is open
            } else {
                cartSidebar.classList.remove('translate-x-0');
                cartSidebar.classList.add('translate-x-full');
                cartOverlay.classList.add('hidden');
                document.body.classList.remove('overflow-hidden');
            }
        };

        // --- Product Rendering ---

        const renderProducts = () => {
            productGrid.innerHTML = ''; // Clear loading indicator/existing products

            products.forEach(product => {
                const productCard = document.createElement('div');
                productCard.className = 'bg-white rounded-xl shadow-lg hover:shadow-xl transition duration-300 overflow-hidden flex flex-col';
                productCard.innerHTML = `
                    <div class="h-48 overflow-hidden">
                        <img src="${product.image}" onerror="this.onerror=null;this.src='https://placehold.co/400x300/a8a29e/ffffff?text=Product+Image';" class="w-full h-full object-cover transition-transform duration-500 hover:scale-110" alt="${product.name}">
                    </div>
                    <div class="p-5 flex flex-col flex-grow">
                        <h3 class="text-xl font-semibold mb-2 text-secondary">${product.name}</h3>
                        <p class="text-gray-600 text-sm mb-3 flex-grow">${product.description}</p>
                        <div class="flex justify-between items-center mt-auto pt-3 border-t border-gray-100">
                            <span class="text-2xl font-bold text-primary">${formatCurrency(product.price)}</span>
                            <button onclick="addToCart(${product.id})" class="bg-primary text-white text-sm font-medium px-4 py-2 rounded-lg hover:bg-indigo-600 transition duration-150 transform hover:scale-105 shadow-md">
                                Add to Cart
                            </button>
                        </div>
                    </div>
                `;
                productGrid.appendChild(productCard);
            });
        };

        // --- Initialization ---
        window.onload = () => {
            renderProducts();
            renderCart();
        };
    </script>
</body>
</html>