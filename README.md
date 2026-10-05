<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AURA Lifestyle E-Commerce</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        aura: {
                            50: '#f5f7fa',
                            100: '#e4e7eb',
                            500: '#64748b',
                            800: '#1e293b',
                            900: '#0f172a',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body { font-family: 'Inter', sans-serif; }
        .hide-scrollbar::-webkit-scrollbar { display: none; }
        .hide-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
    </style>
</head>
<body class="bg-aura-50 text-aura-900 antialiased min-h-screen flex flex-col selection:bg-slate-900 selection:text-white">

    <header class="sticky top-0 z-50 bg-white/80 backdrop-blur-md border-b border-aura-100 transition-all">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <span class="text-2xl font-black tracking-wider uppercase bg-gradient-to-r from-slate-900 to-slate-700 bg-clip-text text-transparent">AURA</span>
                <span class="hidden sm:inline-block text-xs uppercase px-2 py-1 bg-slate-100 font-semibold rounded-full text-slate-600 tracking-widest">Lifestyle</span>
            </div>
            
            <nav class="hidden md:flex items-center space-x-8 font-medium text-sm text-slate-600">
                <a href="#home" class="hover:text-slate-950 transition-colors">Home</a>
                <a href="#top10" class="hover:text-slate-950 transition-colors font-semibold text-slate-950 flex items-center gap-1.5"><i class="fa-solid fa-crown text-amber-500"></i> TOP 10 Curated</a>
                <a href="#categories" class="hover:text-slate-950 transition-colors">Collections</a>
                <a href="#about" class="hover:text-slate-950 transition-colors">Our Story</a>
            </nav>

            <div class="flex items-center space-x-4">
                <button onclick="toggleSearch()" class="p-2 text-slate-600 hover:text-slate-950 rounded-full hover:bg-slate-100 transition-colors" aria-label="Search">
                    <i class="fa-solid fa-search text-lg"></i>
                </button>
                <button onclick="toggleWishlistModal()" class="relative p-2 text-slate-600 hover:text-slate-950 rounded-full hover:bg-slate-100 transition-colors" aria-label="Wishlist">
                    <i class="fa-regular fa-heart text-lg"></i>
                    <span id="wishlist-badge" class="absolute top-1 right-1 w-4 h-4 bg-slate-900 text-white text-[10px] font-bold rounded-full flex items-center justify-center hidden">0</span>
                </button>
                <button onclick="toggleCartModal()" class="relative p-2 text-slate-600 hover:text-slate-950 rounded-full hover:bg-slate-100 transition-colors" aria-label="Cart">
                    <i class="fa-bag-shopping fa-solid text-lg"></i>
                    <span id="cart-badge" class="absolute top-1 right-1 w-4 h-4 bg-amber-600 text-white text-[10px] font-bold rounded-full flex items-center justify-center hidden">0</span>
                </button>
            </div>
        </div>
    </header>

    <main class="flex-grow">
        <section id="home" class="relative bg-slate-900 text-white py-24 sm:py-32 overflow-hidden">
            <div class="absolute inset-0 opacity-20 bg-[radial-gradient(#334155_1px,transparent_1px)] [background-size:16px_16px]"></div>
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10 text-center max-w-3xl">
                <span class="inline-block py-1 px-3 rounded-full bg-slate-800 border border-slate-700 text-xs font-semibold uppercase tracking-widest text-slate-300 mb-6">Refined Living Collection</span>
                <h1 class="text-4xl sm:text-6xl font-extrabold tracking-tight mb-6">Elevate Your Everyday Sanctuary</h1>
                <p class="text-lg sm:text-xl text-slate-400 mb-10 font-light">Explore our definitive Top 10 curated lifestyle essentials, meticulously selected for quality, aesthetic harmony, and performance.</p>
                <div class="flex flex-col sm:flex-row items-center justify-center gap-4">
                    <a href="#top10" class="w-full sm:w-auto px-8 py-4 bg-white text-slate-950 font-semibold rounded-xl hover:bg-slate-100 transition shadow-lg">Explore Top 10 List</a>
                    <a href="#categories" class="w-full sm:w-auto px-8 py-4 bg-slate-800 text-white border border-slate-700 font-semibold rounded-xl hover:bg-slate-700 transition">Browse Categories</a>
                </div>
            </div>
        </section>

        <section id="top10" class="py-20 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex flex-col md:flex-row md:items-end justify-between mb-12">
                <div>
                    <div class="flex items-center gap-2 text-amber-600 font-semibold text-sm uppercase tracking-wider mb-2">
                        <i class="fa-solid fa-trophy"></i> Officially Verified
                    </div>
                    <h2 class="text-3xl sm:text-4xl font-extrabold tracking-tight text-slate-900">AURA Top 10 Best Sellers</h2>
                </div>
                <p class="text-slate-600 mt-2 md:mt-0 max-w-md">Strictly curated to exactly 10 standout pieces chosen by our design directors and customer favorites.</p>
            </div>

            <!-- Grid containing exactly 10 items -->
            <div id="top10-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-6">
                <!-- Dynamically populated via JS to guarantee exactly 10 items -->
            </div>
        </section>

        <section id="categories" class="py-16 bg-white border-y border-aura-100">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <h3 class="text-2xl font-bold text-slate-900 mb-8 text-center">Shop by Category</h3>
                <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
                    <div onclick="filterCategory('All')" class="group cursor-pointer p-6 rounded-2xl bg-slate-50 border border-slate-200 hover:border-slate-900 transition text-center">
                        <div class="w-12 h-12 mx-auto mb-4 rounded-xl bg-slate-900 text-white flex items-center justify-center text-lg"><i class="fa-solid fa-border-all"></i></div>
                        <h4 class="font-semibold text-slate-900">All Items</h4>
                        <span class="text-xs text-slate-500">10 Curated Pieces</span>
                    </div>
                    <div onclick="filterCategory('Living')" class="group cursor-pointer p-6 rounded-2xl bg-slate-50 border border-slate-200 hover:border-slate-900 transition text-center">
                        <div class="w-12 h-12 mx-auto mb-4 rounded-xl bg-slate-100 text-slate-900 group-hover:bg-slate-900 group-hover:text-white transition flex items-center justify-center text-lg"><i class="fa-solid fa-couch"></i></div>
                        <h4 class="font-semibold text-slate-900">Living</h4>
                        <span class="text-xs text-slate-500">Decor & Furniture</span>
                    </div>
                    <div onclick="filterCategory('Audio')" class="group cursor-pointer p-6 rounded-2xl bg-slate-50 border border-slate-200 hover:border-slate-900 transition text-center">
                        <div class="w-12 h-12 mx-auto mb-4 rounded-xl bg-slate-100 text-slate-900 group-hover:bg-slate-900 group-hover:text-white transition flex items-center justify-center text-lg"><i class="fa-solid fa-headphones"></i></div>
                        <h4 class="font-semibold text-slate-900">Audio</h4>
                        <span class="text-xs text-slate-500">Sound & Tech</span>
                    </div>
                    <div onclick="filterCategory('Apparel')" class="group cursor-pointer p-6 rounded-2xl bg-slate-50 border border-slate-200 hover:border-slate-900 transition text-center">
                        <div class="w-12 h-12 mx-auto mb-4 rounded-xl bg-slate-100 text-slate-900 group-hover:bg-slate-900 group-hover:text-white transition flex items-center justify-center text-lg"><i class="fa-solid fa-shirt"></i></div>
                        <h4 class="font-semibold text-slate-900">Apparel</h4>
                        <span class="text-xs text-slate-500">Wearables</span>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <footer id="about" class="bg-slate-950 text-slate-400 py-16">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid grid-cols-1 md:grid-cols-4 gap-10 mb-12">
            <div>
                <span class="text-2xl font-black tracking-wider text-white uppercase block mb-4">AURA</span>
                <p class="text-sm text-slate-400">Crafting exceptional lifestyle experiences through uncompromising standards and curated top-tier selections.</p>
            </div>
            <div>
                <h5 class="text-white font-semibold mb-4 text-sm uppercase tracking-wider">Navigation</h5>
                <ul class="space-y-2 text-sm">
                    <li><a href="#home" class="hover:text-white transition">Home</a></li>
                    <li><a href="#top10" class="hover:text-white transition">Top 10 Rankings</a></li>
                    <li><a href="#categories" class="hover:text-white transition">Collections</a></li>
                </ul>
            </div>
            <div>
                <h5 class="text-white font-semibold mb-4 text-sm uppercase tracking-wider">Customer Care</h5>
                <ul class="space-y-2 text-sm">
                    <li><a href="#" class="hover:text-white transition">Shipping & Delivery</a></li>
                    <li><a href="#" class="hover:text-white transition">Returns & Exchanges</a></li>
                    <li><a href="#" class="hover:text-white transition">Support Center</a></li>
                </ul>
            </div>
            <div>
                <h5 class="text-white font-semibold mb-4 text-sm uppercase tracking-wider">Stay Updated</h5>
                <p class="text-sm text-slate-400 mb-4">Subscribe to receive seasonal Top 10 curation updates.</p>
                <div class="flex">
                    <input type="email" placeholder="Enter your email" class="bg-slate-900 border border-slate-800 px-4 py-2 text-sm rounded-l-xl text-white focus:outline-none focus:border-slate-600 w-full">
                    <button onclick="showNotification('Subscribed successfully!')" class="bg-white text-slate-950 px-4 py-2 text-sm font-semibold rounded-r-xl hover:bg-slate-200 transition">Join</button>
                </div>
            </div>
        </div>
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pt-8 border-t border-slate-900 text-center text-xs text-slate-500">
            &copy; 2026 AURA Lifestyle E-Commerce. All rights reserved. Exactly 10 curated items guaranteed.
        </div>
    </footer>

    <!-- Cart Modal -->
    <div id="cart-modal" class="fixed inset-0 z-50 bg-black/50 backdrop-blur-sm hidden items-center justify-end">
        <div class="bg-white w-full max-w-md h-full flex flex-col p-6 shadow-2xl animate-in slide-in-from-right duration-300">
            <div class="flex items-center justify-between pb-4 border-b border-slate-100">
                <h3 class="text-lg font-bold text-slate-900 flex items-center gap-2"><i class="fa-bag-shopping fa-solid"></i> Your Cart</h3>
                <button onclick="toggleCartModal()" class="p-2 text-slate-400 hover:text-slate-900 rounded-full"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <div id="cart-items" class="flex-grow overflow-y-auto py-4 space-y-4">
                <p class="text-center text-slate-500 py-12">Your cart is empty.</p>
            </div>
            <div class="pt-4 border-t border-slate-100">
                <div class="flex justify-between items-center mb-4 text-lg font-bold text-slate-900">
                    <span>Subtotal</span>
                    <span id="cart-subtotal">$0.00</span>
                </div>
                <button onclick="checkout()" class="w-full py-3.5 bg-slate-900 text-white font-semibold rounded-xl hover:bg-slate-800 transition">Proceed to Checkout</button>
            </div>
        </div>
    </div>

    <!-- Wishlist Modal -->
    <div id="wishlist-modal" class="fixed inset-0 z-50 bg-black/50 backdrop-blur-sm hidden items-center justify-end">
        <div class="bg-white w-full max-w-md h-full flex flex-col p-6 shadow-2xl">
            <div class="flex items-center justify-between pb-4 border-b border-slate-100">
                <h3 class="text-lg font-bold text-slate-900 flex items-center gap-2"><i class="fa-regular fa-heart"></i> Saved Favorites</h3>
                <button onclick="toggleWishlistModal()" class="p-2 text-slate-400 hover:text-slate-900 rounded-full"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <div id="wishlist-items" class="flex-grow overflow-y-auto py-4 space-y-4">
                <p class="text-center text-slate-500 py-12">No saved items yet.</p>
            </div>
        </div>
    </div>

    <!-- Search Modal -->
    <div id="search-modal" class="fixed inset-0 z-50 bg-black/50 backdrop-blur-sm hidden items-start justify-center pt-20 px-4">
        <div class="bg-white w-full max-w-2xl rounded-2xl p-6 shadow-2xl">
            <div class="flex items-center justify-between pb-4 border-b border-slate-100 mb-4">
                <div class="flex items-center gap-3 w-full mr-4">
                    <i class="fa-solid fa-search text-slate-400"></i>
                    <input type="text" id="search-input" oninput="handleSearch(this.value)" placeholder="Search Top 10 collection..." class="w-full focus:outline-none text-slate-900 placeholder:text-slate-400 font-medium">
                </div>
                <button onclick="toggleSearch()" class="p-2 text-slate-400 hover:text-slate-900 rounded-full"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <div id="search-results" class="max-h-96 overflow-y-auto space-y-2">
                <p class="text-sm text-slate-500 text-center py-6">Type to search among our 10 curated items...</p>
            </div>
        </div>
    </div>

    <!-- Notification Toast -->
    <div id="toast" class="fixed bottom-6 right-6 z-50 bg-slate-900 text-white px-6 py-3 rounded-xl shadow-2xl transform translate-y-24 opacity-0 transition-all duration-300 flex items-center gap-3">
        <i class="fa-solid fa-circle-check text-emerald-400"></i>
        <span id="toast-message" class="text-sm font-medium">Action completed successfully</span>
    </div>

    <script>
        // STRICTLY 10 items dataset to resolve the inconsistency
        const top10Products = [
            { id: 1, name: "AURA Minimalist Ceramic Lamp", category: "Living", price: 120.00, rating: 4.9, image: "https://placehold.co/400x400/1e293b/ffffff?text=Ceramic+Lamp" },
            { id: 2, name: "Acoustic Horizon Wireless Earbuds", category: "Audio", price: 199.00, rating: 4.8, image: "https://placehold.co/400x400/334155/ffffff?text=Wireless+Earbuds" },
            { id: 3, name: "Merino Wool Blend Throw Blanket", category: "Living", price: 85.00, rating: 4.7, image: "https://placehold.co/400x400/475569/ffffff?text=Wool+Blanket" },
            { id: 4, name: "Ergonomic Walnut Desk Organizer", category: "Living", price: 65.00, rating: 4.9, image: "https://placehold.co/400x400/64748b/ffffff?text=Desk+Organizer" },
            { id: 5, name: "Studio Reference Over-Ear Headphones", category: "Audio", price: 299.00, rating: 5.0, image: "https://placehold.co/400x400/0f172a/ffffff?text=Over-Ear+Audio" },
            { id: 6, name: "Organic Cotton Relaxed Fit Hoodie", category: "Apparel", price: 95.00, rating: 4.8, image: "https://placehold.co/400x400/1e293b/ffffff?text=Cotton+Hoodie" },
            { id: 7, name: "Hand-poured Scented Soy Candle", category: "Living", price: 34.00, rating: 4.6, image: "https://placehold.co/400x400/334155/ffffff?text=Soy+Candle" },
            { id: 8, name: "Titanium Minimalist Wristwatch", category: "Apparel", price: 245.00, rating: 4.9, image: "https://placehold.co/400x400/475569/ffffff?text=Titanium+Watch" },
            { id: 9, name: "Portable Waterproof Sound Cylinder", category: "Audio", price: 140.00, rating: 4.7, image: "https://placehold.co/400x400/64748b/ffffff?text=Sound+Cylinder" },
            { id: 10, name: "Heavyweight Structured Overshirt", category: "Apparel", price: 110.00, rating: 4.8, image: "https://placehold.co/400x400/0f172a/ffffff?text=Overshirt" }
        ];

        let cart = [];
        let wishlist = [];
        let currentFilter = 'All';

        function renderProducts(filter = 'All') {
            const grid = document.getElementById('top10-grid');
            const filtered = filter === 'All' ? top10Products : top10Products.filter(p => p.category === filter);
            
            grid.innerHTML = filtered.map((product, index) => `
                <div class="group bg-white rounded-2xl border border-slate-200 overflow-hidden flex flex-col justify-between hover:shadow-xl transition-all duration-300">
                    <div class="relative overflow-hidden bg-slate-100 aspect-square">
                        <img src="${product.image}" alt="${product.name}" class="w-full h-full object-cover group-hover:scale-105 transition duration-500" onerror="this.src='https://placehold.co/400x400/e2e8f0/64748b?text=AURA+Item'">
                        <span class="absolute top-3 left-3 bg-slate-900 text-white text-xs font-bold px-2.5 py-1 rounded-lg">#${index + 1}</span>
                        <button onclick="toggleWishlist(${product.id})" class="absolute top-3 right-3 p-2 bg-white/80 backdrop-blur-sm rounded-full hover:bg-white text-slate-700 transition">
                            <i class="${wishlist.includes(product.id) ? 'fa-solid text-rose-500' : 'fa-regular'} fa-heart"></i>
                        </button>
                    </div>
                    <div class="p-5 flex flex-col flex-grow justify-between">
                        <div>
                            <div class="flex items-center justify-between text-xs text-slate-500 mb-1">
                                <span class="uppercase tracking-wider font-semibold">${product.category}</span>
                                <span class="flex items-center gap-1 text-amber-500 font-bold"><i class="fa-solid fa-star"></i> ${product.rating}</span>
                            </div>
                            <h4 class="font-semibold text-slate-900 text-base mb-2 line-clamp-1">${product.name}</h4>
                        </div>
                        <div class="flex items-center justify-between pt-4 border-t border-slate-100 mt-2">
                            <span class="font-bold text-slate-900">$${product.price.toFixed(2)}</span>
                            <button onclick="addToCart(${product.id})" class="px-3.5 py-2 bg-slate-900 text-white text-xs font-semibold rounded-xl hover:bg-slate-800 transition shadow-sm">
                                Add to Cart
                            </button>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        function filterCategory(category) {
            currentFilter = category;
            renderProducts(category);
        }

        function addToCart(productId) {
            const product = top10Products.find(p => p.id === productId);
            const existing = cart.find(item => item.id === productId);
            if (existing) {
                existing.quantity += 1;
            } else {
                cart.push({ ...product, quantity: 1 });
            }
            updateCartUI();
            showNotification(`Added "${product.name}" to cart`);
        }

        function updateCartUI() {
            const badge = document.getElementById('cart-badge');
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            if (totalItems > 0) {
                badge.innerText = totalItems;
                badge.classList.remove('hidden');
            } else {
                badge.classList.add('hidden');
            }

            const container = document.getElementById('cart-items');
            if (cart.length === 0) {
                container.innerHTML = `<p class="text-center text-slate-500 py-12">Your cart is empty.</p>`;
                document.getElementById('cart-subtotal').innerText = '$0.00';
                return;
            }

            container.innerHTML = cart.map(item => `
                <div class="flex items-center justify-between bg-slate-50 p-3 rounded-xl border border-slate-100">
                    <div class="flex items-center gap-3">
                        <img src="${item.image}" alt="${item.name}" class="w-12 h-12 rounded-lg object-cover">
                        <div>
                            <h5 class="font-semibold text-sm text-slate-900 line-clamp-1">${item.name}</h5>
                            <span class="text-xs text-slate-500">$${item.price.toFixed(2)} x ${item.quantity}</span>
                        </div>
                    </div>
                    <button onclick="removeFromCart(${item.id})" class="text-slate-400 hover:text-rose-500 p-2"><i class="fa-solid fa-trash-can"></i></button>
                </div>
            `).join('');

            const subtotal = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            document.getElementById('cart-subtotal').innerText = `$${subtotal.toFixed(2)}`;
        }

        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            updateCartUI();
            showNotification("Item removed from cart");
        }

        function toggleWishlist(productId) {
            const index = wishlist.indexOf(productId);
            if (index > -1) {
                wishlist.splice(index, 1);
                showNotification("Removed from wishlist");
            } else {
                wishlist.push(productId);
                showNotification("Added to wishlist");
            }
            renderProducts(currentFilter);
            updateWishlistUI();
        }

        function updateWishlistUI() {
            const badge = document.getElementById('wishlist-badge');
            if (wishlist.length > 0) {
                badge.innerText = wishlist.length;
                badge.classList.remove('hidden');
            } else {
                badge.classList.add('hidden');
            }

            const container = document.getElementById('wishlist-items');
            if (wishlist.length === 0) {
                container.innerHTML = `<p class="text-center text-slate-500 py-12">No saved items yet.</p>`;
                return;
            }

            const wishlistProducts = top10Products.filter(p => wishlist.includes(p.id));
            container.innerHTML = wishlistProducts.map(item => `
                <div class="flex items-center justify-between bg-slate-50 p-3 rounded-xl border border-slate-100">
                    <div class="flex items-center gap-3">
                        <img src="${item.image}" alt="${item.name}" class="w-12 h-12 rounded-lg object-cover">
                        <div>
                            <h5 class="font-semibold text-sm text-slate-900 line-clamp-1">${item.name}</h5>
                            <span class="text-xs text-slate-900 font-bold">$${item.price.toFixed(2)}</span>
                        </div>
                    </div>
                    <button onclick="addToCart(${item.id}); toggleWishlist(${item.id});" class="px-3 py-1.5 bg-slate-900 text-white text-xs font-semibold rounded-lg">Move to Cart</button>
                </div>
            `).join('');
        }

        function toggleCartModal() {
            const modal = document.getElementById('cart-modal');
            modal.classList.toggle('hidden');
            modal.classList.toggle('flex');
        }

        function toggleWishlistModal() {
            const modal = document.getElementById('wishlist-modal');
            modal.classList.toggle('hidden');
            modal.classList.toggle('flex');
        }

        function toggleSearch() {
            const modal = document.getElementById('search-modal');
            modal.classList.toggle('hidden');
            modal.classList.toggle('flex');
            if (!modal.classList.contains('hidden')) {
                document.getElementById('search-input').focus();
            }
        }

        function handleSearch(query) {
            const resultsContainer = document.getElementById('search-results');
            if (!query.trim()) {
                resultsContainer.innerHTML = `<p class="text-sm text-slate-500 text-center py-6">Type to search among our 10 curated items...</p>`;
                return;
            }
            const filtered = top10Products.filter(p => p.name.toLowerCase().includes(query.toLowerCase()) || p.category.toLowerCase().includes(query.toLowerCase()));
            if (filtered.length === 0) {
                resultsContainer.innerHTML = `<p class="text-sm text-slate-500 text-center py-6">No matching items found in the Top 10 list.</p>`;
                return;
            }
            resultsContainer.innerHTML = filtered.map(item => `
                <div onclick="toggleSearch();" class="flex items-center justify-between p-3 hover:bg-slate-50 rounded-xl cursor-pointer transition">
                    <div class="flex items-center gap-3">
                        <img src="${item.image}" class="w-10 h-10 rounded-lg object-cover">
                        <div>
                            <h5 class="font-semibold text-sm text-slate-900">${item.name}</h5>
                            <span class="text-xs text-slate-500">${item.category} &bull; $${item.price.toFixed(2)}</span>
                        </div>
                    </div>
                    <button onclick="event.stopPropagation(); addToCart(${item.id});" class="px-3 py-1.5 bg-slate-900 text-white text-xs font-semibold rounded-lg">Add</button>
                </div>
            `).join('');
        }

        function checkout() {
            if (cart.length === 0) return;
            showNotification("Order placed successfully! Thank you.");
            cart = [];
            updateCartUI();
            toggleCartModal();
        }

        function showNotification(message) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-message').innerText = message;
            toast.classList.remove('translate-y-24', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-24', 'opacity-0');
            }, 3000);
        }

        window.onload = function() {
            renderProducts();
        }
    </script>
</body>
</html>
