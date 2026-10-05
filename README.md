<!DOCTYPE html>
<html lang="ko" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AURA | 라이프스타일 샵</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Gowun+Dodum&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'Gowun Dodum', 'sans-serif'],
                    },
                    colors: {
                        aura: {
                            pink: '#F48FB1',
                            peach: '#FFAB91',
                            cream: '#FAFAFA',
                            dark: '#374151',
                            softgray: '#F3F4F6',
                            accent: '#E91E63',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Inter', 'Gowun Dodum', sans-serif;
            background-color: #FAFAFA;
            color: #374151;
        }
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #FAFAFA;
        }
        ::-webkit-scrollbar-thumb {
            background: #D1D5DB;
            border-radius: 4px;
        }
        .standard-card {
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }
        .standard-card:hover {
            transform: translateY(-4px);
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.08);
        }
    </style>
</head>
<body class="bg-aura-cream text-aura-dark antialiased min-h-screen flex flex-col selection:bg-aura-pink selection:text-white">

    <!-- Fixed Top Navigation Bar -->
    <header class="fixed top-0 left-0 w-full z-40 bg-white/90 backdrop-blur-md border-b border-gray-200 transition-all duration-300 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between gap-4">
            
            <!-- Left: AURA Logo -->
            <div class="flex items-center gap-3 cursor-pointer group" onclick="resetFilters()">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-aura-pink to-aura-peach text-white flex items-center justify-center shadow-sm">
                    <span class="font-bold text-lg">A</span>
                </div>
                <div class="flex flex-col">
                    <span class="text-xl tracking-tight font-bold text-aura-dark">AURA</span>
                    <span class="text-[10px] tracking-widest uppercase text-gray-400 font-medium -mt-1" data-i18n="tagline">Lifestyle Shop</span>
                </div>
            </div>

            <!-- Center: Search Bar -->
            <div class="hidden md:flex flex-1 max-w-md mx-6">
                <div class="relative w-full">
                    <span class="absolute inset-y-0 left-0 pl-4 flex items-center pointer-events-none text-gray-400">
                        <i data-lucide="search" class="w-4 h-4"></i>
                    </span>
                    <input type="text" id="searchInput" oninput="handleSearch(this.value)" 
                        placeholder="상품명을 검색해 보세요..." 
                        data-i18n-placeholder="search_placeholder"
                        class="w-full pl-11 pr-4 py-2.5 bg-gray-100 border border-transparent rounded-xl text-sm focus:outline-none focus:border-aura-pink focus:bg-white transition-all">
                </div>
            </div>

            <!-- Right: Actions -->
            <div class="flex items-center gap-3">
                <!-- Mobile Search Toggle -->
                <button onclick="toggleMobileSearch()" class="md:hidden p-2.5 bg-gray-100 rounded-xl text-aura-dark hover:bg-gray-200 transition-colors" aria-label="Search">
                    <i data-lucide="search" class="w-5 h-5"></i>
                </button>

                <!-- Wishlist Quick Button -->
                <button onclick="openWishlistModal()" class="relative p-2.5 bg-gray-100 rounded-xl text-aura-dark hover:bg-gray-200 transition-colors flex items-center justify-center" aria-label="Wishlist">
                    <i data-lucide="heart" class="w-5 h-5"></i>
                    <span id="wishlistCountBadge" class="absolute -top-1 -right-1 bg-aura-accent text-white text-[10px] font-bold w-4 h-4 rounded-full flex items-center justify-center shadow">0</span>
                </button>

                <!-- Cart Button -->
                <button onclick="toggleCartDrawer()" class="relative p-2.5 bg-aura-dark text-white rounded-xl hover:bg-gray-800 transition-all duration-200 flex items-center justify-center shadow-sm" aria-label="Cart">
                    <i data-lucide="shopping-bag" class="w-5 h-5"></i>
                    <span id="cartCountBadge" class="absolute -top-1 -right-1 bg-aura-accent text-white text-[10px] font-bold w-5 h-5 rounded-full flex items-center justify-center border-2 border-white shadow">0</span>
                </button>

                <!-- Hamburger Menu Button -->
                <button onclick="toggleMenuDrawer()" class="p-2.5 bg-gray-100 text-aura-dark hover:bg-gray-200 transition-all rounded-xl flex items-center justify-center" aria-label="Menu">
                    <i data-lucide="menu" class="w-5 h-5"></i>
                </button>
            </div>
        </div>

        <!-- Mobile Expandable Search Bar -->
        <div id="mobileSearchContainer" class="hidden md:hidden px-4 pb-4 bg-white border-b border-gray-200">
            <div class="relative w-full">
                <span class="absolute inset-y-0 left-0 pl-4 flex items-center pointer-events-none text-gray-400">
                    <i data-lucide="search" class="w-4 h-4"></i>
                </span>
                <input type="text" id="mobileSearchInput" oninput="handleSearch(this.value)" 
                    placeholder="상품명을 검색해 보세요..." 
                    data-i18n-placeholder="search_placeholder"
                    class="w-full pl-11 pr-4 py-2.5 bg-gray-100 border border-gray-200 rounded-xl text-sm focus:outline-none focus:border-aura-pink">
            </div>
        </div>
    </header>

    <!-- Hamburger Menu Slide-out Drawer (Right) -->
    <div id="menuOverlay" class="fixed inset-0 bg-black/40 z-50 hidden backdrop-blur-sm transition-opacity opacity-0" onclick="toggleMenuDrawer()"></div>
    <div id="menuDrawer" class="fixed top-0 right-0 h-full w-full sm:w-80 bg-white z-50 shadow-2xl transform translate-x-full transition-transform duration-300 ease-in-out flex flex-col">
        
        <!-- Drawer Header -->
        <div class="p-6 bg-gray-50 border-b border-gray-200 flex items-center justify-between">
            <span class="font-bold text-lg text-aura-dark" data-i18n="menu_title">메뉴 및 카테고리</span>
            <button onclick="toggleMenuDrawer()" class="p-2 text-aura-dark hover:bg-gray-200 rounded-xl transition-colors">
                <i data-lucide="x" class="w-5 h-5"></i>
            </button>
        </div>

        <!-- Drawer Body -->
        <div class="flex-1 overflow-y-auto p-6 space-y-6">
            
            <!-- Language Selector -->
            <div class="bg-gray-50 p-4 rounded-xl flex items-center justify-between border border-gray-200">
                <div class="flex items-center gap-2">
                    <i data-lucide="globe" class="w-4 h-4 text-gray-500"></i>
                    <span class="text-sm font-medium" data-i18n="language_label">언어 선택 (Language)</span>
                </div>
                <div class="flex bg-white rounded-lg p-1 shadow-sm border border-gray-200">
                    <button onclick="setLanguage('ko')" id="langKoBtn" class="px-3 py-1 text-xs font-bold rounded-md transition-all bg-aura-dark text-white">KO</button>
                    <button onclick="setLanguage('en')" id="langEnBtn" class="px-3 py-1 text-xs font-bold rounded-md transition-all text-gray-600 hover:text-aura-dark">EN</button>
                </div>
            </div>

            <!-- Hierarchical Categories Accordion (Dynamically Rendered) -->
            <div class="space-y-3">
                <h3 class="text-xs uppercase tracking-wider text-gray-400 font-bold mb-2" data-i18n="categories_title">상품 카테고리</h3>
                <div id="categoryAccordionContainer" class="space-y-3">
                    <!-- Populated dynamically -->
                </div>
            </div>

            <!-- Quick Links -->
            <div class="space-y-2 pt-4 border-t border-gray-200 text-sm">
                <h3 class="text-xs uppercase tracking-wider text-gray-400 font-bold mb-2" data-i18n="quick_links">바로가기</h3>
                <a href="#products-section" onclick="toggleMenuDrawer(); resetFilters();" class="flex items-center gap-2.5 p-2.5 rounded-lg hover:bg-gray-100 transition-colors text-gray-700 font-medium">
                    <i data-lucide="grid" class="w-4 h-4 text-gray-400"></i>
                    <span data-i18n="nav_all_products">전체 상품 보기</span>
                </a>
                <button onclick="toggleMenuDrawer(); openWishlistModal();" class="w-full flex items-center justify-between p-2.5 rounded-lg hover:bg-gray-100 transition-colors text-gray-700 font-medium">
                    <span class="flex items-center gap-2.5">
                        <i data-lucide="heart" class="w-4 h-4 text-gray-400"></i>
                        <span data-i18n="nav_wishlist">관심 상품</span>
                    </span>
                    <span id="drawerWishlistCount" class="bg-gray-200 text-aura-dark text-xs px-2 py-0.5 rounded-full font-bold">0</span>
                </button>
            </div>
        </div>

        <!-- Drawer Footer -->
        <div class="p-6 border-t border-gray-200 bg-gray-50 text-center text-xs text-gray-500">
            &copy; 2026 AURA. All Rights Reserved.
        </div>
    </div>

    <!-- Hero Banner Section -->
    <section class="relative mt-20 bg-white border-b border-gray-200 py-16">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
            <div class="space-y-6 text-center lg:text-left">
                <span class="inline-flex items-center gap-2 px-3 py-1 rounded-md bg-gray-100 text-aura-dark text-xs font-semibold tracking-wide">
                    <span data-i18n="hero_badge">2026 신상품 입고 완료</span>
                </span>
                <h1 class="text-3xl sm:text-4xl lg:text-5xl font-bold tracking-tight text-aura-dark leading-tight">
                    <span data-i18n="hero_title_1">일상을 더욱 가치 있게</span> <br>
                    <span class="text-gray-500 font-normal text-2xl sm:text-3xl mt-1 block" data-i18n="hero_title_2">AURA 라이프스타일 샵</span>
                </h1>
                <p class="text-gray-600 text-base max-w-lg mx-auto lg:mx-0 font-normal" data-i18n="hero_desc">
                    전자기기, 게이밍 기어부터 취미용품과 차량용품까지, 당신의 일상을 채워줄 다양한 상품들을 만나보세요.
                </p>
                <div class="flex flex-wrap items-center justify-center lg:justify-start gap-4 pt-2">
                    <a href="#products-section" class="px-7 py-3.5 bg-aura-dark text-white font-semibold rounded-xl hover:bg-gray-800 transition-colors shadow-sm text-sm flex items-center gap-2">
                        <span data-i18n="hero_cta">상품 둘러보기</span>
                        <i data-lucide="arrow-right" class="w-4 h-4"></i>
                    </a>
                    <button onclick="filterByCategory('gaming', 'all')" class="px-7 py-3.5 bg-white text-aura-dark border border-gray-300 hover:border-gray-400 font-semibold rounded-xl transition-colors text-sm">
                        <span data-i18n="hero_cta_secondary">게이밍 기어</span>
                    </button>
                </div>
            </div>

            <!-- Hero Image Banner -->
            <div class="relative flex items-center justify-center">
                <div class="relative w-full max-w-md aspect-square rounded-2xl overflow-hidden shadow-lg border border-gray-200 bg-gray-100">
                    <img src="https://images.unsplash.com/photo-1550745165-9bc0b252726f?auto=format&fit=crop&q=80&w=800" alt="Gaming & Tech Collection" class="w-full h-full object-cover">
                    <div class="absolute bottom-4 left-4 right-4 bg-white/95 backdrop-blur-md p-4 rounded-xl shadow-sm border border-gray-200 flex items-center justify-between">
                        <div>
                            <h4 class="font-bold text-sm text-aura-dark" data-i18n="banner_card_title">스페셜 컬렉션</h4>
                            <p class="text-xs text-gray-500 font-normal" data-i18n="banner_card_sub">MD 추천 인기 상품</p>
                        </div>
                        <span class="px-2.5 py-1 bg-gray-100 text-aura-dark text-xs font-semibold rounded-md">HOT</span>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Main Product Grid Section -->
    <main id="products-section" class="flex-1 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16 w-full">
        
        <!-- Section Header & Active Filter Indicator -->
        <div class="flex flex-col md:flex-row md:items-end justify-between mb-8 pb-4 border-b border-gray-200 gap-4">
            <div>
                <span class="text-xs uppercase tracking-wider text-gray-400 font-semibold" data-i18n="curated_subtitle">FEATURED PRODUCTS</span>
                <h2 id="sectionTitle" class="text-2xl font-bold text-aura-dark mt-1" data-i18n="curated_title">추천상품</h2>
            </div>
            
            <div class="flex items-center gap-3">
                <div id="activeFilterBadge" class="hidden items-center gap-2 bg-gray-200 text-aura-dark px-3 py-1 rounded-lg text-xs font-semibold">
                    <span id="activeFilterText">Filtered</span>
                    <button onclick="resetFilters()" class="hover:text-red-500"><i data-lucide="x" class="w-3.5 h-3.5"></i></button>
                </div>
                <div class="text-sm text-gray-500 font-medium">
                    총 <span id="productCount" class="text-aura-dark font-bold">0</span>개 상품
                </div>
            </div>
        </div>

        <!-- Product Grid Container -->
        <div id="productGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
            <!-- Dynamically populated via JavaScript -->
        </div>

        <!-- Empty State -->
        <div id="emptyState" class="hidden text-center py-20">
            <div class="w-16 h-16 mx-auto mb-4 bg-gray-100 rounded-full flex items-center justify-center text-gray-400">
                <i data-lucide="search-x" class="w-8 h-8"></i>
            </div>
            <h3 class="text-lg font-bold mb-1 text-aura-dark" data-i18n="no_products_title">검색 결과가 없습니다</h3>
            <p class="text-gray-500 text-sm mb-6" data-i18n="no_products_desc">다른 검색어를 입력하시거나 카테고리를 변경해 보세요.</p>
            <button onclick="resetFilters()" class="px-5 py-2.5 bg-aura-dark text-white text-sm font-medium rounded-xl hover:bg-gray-800 transition-colors shadow-sm" data-i18n="reset_filter_btn">
                전체 상품 보기
            </button>
        </div>
    </main>

    <!-- Shopping Cart Slide-out Drawer (Right) -->
    <div id="cartOverlay" class="fixed inset-0 bg-black/40 z-50 hidden backdrop-blur-sm transition-opacity opacity-0" onclick="toggleCartDrawer()"></div>
    <div id="cartDrawer" class="fixed top-0 right-0 h-full w-full sm:w-[400px] bg-white z-50 shadow-2xl transform translate-x-full transition-transform duration-300 ease-in-out flex flex-col">
        
        <!-- Cart Header -->
        <div class="p-6 bg-gray-50 border-b border-gray-200 flex items-center justify-between">
            <div class="flex items-center gap-2">
                <span class="font-bold text-lg text-aura-dark" data-i18n="cart_title">장바구니</span>
            </div>
            <button onclick="toggleCartDrawer()" class="p-2 text-aura-dark hover:bg-gray-200 rounded-xl transition-colors">
                <i data-lucide="x" class="w-5 h-5"></i>
            </button>
        </div>

        <!-- Cart Items Container -->
        <div id="cartItemsContainer" class="flex-1 overflow-y-auto p-6 space-y-4 divide-y divide-gray-100">
            <!-- Dynamically populated via JS -->
        </div>

        <!-- Cart Footer / Summary -->
        <div id="cartFooter" class="p-6 border-t border-gray-200 bg-gray-50 space-y-4">
            <div class="space-y-2 text-sm">
                <div class="flex justify-between text-gray-600">
                    <span data-i18n="subtotal">상품 금액</span>
                    <span id="cartSubtotal" class="font-bold text-aura-dark">₩0</span>
                </div>
                <div class="flex justify-between text-gray-600">
                    <span data-i18n="shipping">배송비</span>
                    <span class="text-aura-dark font-medium" data-i18n="free_shipping">무료</span>
                </div>
                <div class="flex justify-between text-base font-bold text-aura-dark pt-3 border-t border-gray-200">
                    <span data-i18n="total">총 결제금액</span>
                    <span id="cartTotal" class="text-aura-accent text-lg">₩0</span>
                </div>
            </div>
            
            <button onclick="handleCheckout()" class="w-full py-3.5 bg-aura-dark text-white font-semibold rounded-xl hover:bg-gray-800 transition-colors shadow-sm text-sm">
                <span data-i18n="checkout_btn">주문하기</span>
            </button>
        </div>
    </div>

    <!-- Wishlist Modal -->
    <div id="wishlistModalOverlay" class="fixed inset-0 bg-black/40 z-50 hidden backdrop-blur-sm flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl w-full max-w-xl max-h-[80vh] flex flex-col shadow-2xl overflow-hidden border border-gray-200">
            <div class="p-6 bg-gray-50 border-b border-gray-200 flex items-center justify-between">
                <h3 class="font-bold text-lg text-aura-dark" data-i18n="wishlist_title">관심 상품</h3>
                <button onclick="closeWishlistModal()" class="p-2 text-aura-dark hover:bg-gray-200 rounded-xl transition-colors">
                    <i data-lucide="x" class="w-5 h-5"></i>
                </button>
            </div>
            <div id="wishlistModalContent" class="flex-1 overflow-y-auto p-6 space-y-4">
                <!-- Dynamically populated -->
            </div>
            <div class="p-4 border-t border-gray-200 bg-gray-50 text-right">
                <button onclick="closeWishlistModal()" class="px-5 py-2 bg-aura-dark text-white text-sm font-medium rounded-xl hover:bg-gray-800 transition-colors" data-i18n="close_btn">닫기</button>
            </div>
        </div>
    </div>

    <!-- Developer Password Modal -->
    <div id="devPasswordModal" class="fixed inset-0 bg-black/50 z-50 hidden backdrop-blur-sm flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl w-full max-w-md p-6 shadow-2xl border border-gray-200 space-y-4">
            <div class="flex items-center justify-between">
                <h3 class="font-bold text-lg text-aura-dark">개발자 인증</h3>
                <button onclick="closeDevPasswordModal()" class="p-2 text-gray-400 hover:text-aura-dark"><i data-lucide="x" class="w-5 h-5"></i></button>
            </div>
            <p class="text-xs text-gray-500">관리자 비밀번호를 입력하세요.</p>
            <input type="password" id="devPasswordInput" placeholder="비밀번호 입력" class="w-full px-4 py-2.5 bg-gray-100 border border-gray-200 rounded-xl text-sm focus:outline-none focus:border-aura-dark">
            <div class="flex gap-2 justify-end">
                <button onclick="closeDevPasswordModal()" class="px-4 py-2 bg-gray-200 text-aura-dark text-xs font-semibold rounded-xl">취소</button>
                <button onclick="verifyDevPassword()" class="px-4 py-2 bg-aura-dark text-white text-xs font-semibold rounded-xl">확인</button>
            </div>
        </div>
    </div>

    <!-- Developer Dashboard Modal (With Category & Subcategory Management) -->
    <div id="devPanelModal" class="fixed inset-0 bg-black/50 z-50 hidden backdrop-blur-sm flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl w-full max-w-3xl max-h-[85vh] flex flex-col shadow-2xl overflow-hidden border border-gray-200">
            <div class="p-6 bg-gray-50 border-b border-gray-200 flex items-center justify-between">
                <h3 class="font-bold text-lg text-aura-dark">개발자 대시보드 (상품 및 카테고리 관리)</h3>
                <button onclick="closeDevPanelModal()" class="p-2 text-gray-400 hover:text-aura-dark"><i data-lucide="x" class="w-5 h-5"></i></button>
            </div>
            
            <div class="flex-1 overflow-y-auto p-6 space-y-8">
                
                <!-- 1. Add Main Category Form -->
                <div class="bg-gray-50 p-5 rounded-2xl border border-gray-200 space-y-4">
                    <h4 class="font-bold text-sm text-aura-dark">새 대분류 카테고리 추가</h4>
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                        <div>
                            <label class="block text-xs font-semibold text-gray-600 mb-1">카테고리 ID (영문)</label>
                            <input type="text" id="newCatId" placeholder="예: adult" class="w-full px-3 py-2 bg-white border border-gray-200 rounded-xl text-xs">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-gray-600 mb-1">카테고리명 (한국어)</label>
                            <input type="text" id="newCatKo" placeholder="예: 성인용품" class="w-full px-3 py-2 bg-white border border-gray-200 rounded-xl text-xs">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-gray-600 mb-1">카테고리명 (영어)</label>
                            <input type="text" id="newCatEn" placeholder="예: Adult Wellness" class="w-full px-3 py-2 bg-white border border-gray-200 rounded-xl text-xs">
                        </div>
                    </div>
                    <button onclick="addNewMainCategory()" class="px-5 py-2.5 bg-aura-dark text-white text-xs font-semibold rounded-xl hover:bg-gray-800 transition-colors">카테고리 추가하기</button>
                </div>

                <!-- 2. Add Subcategory Form -->
                <div class="bg-gray-50 p-5 rounded-2xl border border-gray-200 space-y-4">
                    <h4 class="font-bold text-sm text-aura-dark">새 세부 카테고리 추가</h4>
                    <div class="grid grid-cols-1 sm:grid-cols-4 gap-4">
                        <div>
                            <label class="block text-xs font-semibold text-gray-600 mb-1">상위 카테고리 선택</label>
                            <select id="subParentSelect" class="w-full px-3 py-2 bg-white border border-gray-200 rounded-xl text-xs">
                                <!-- Populated dynamically -->
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-gray-600 mb-1">세부 ID (영문)</label>
                            <input type="text" id="newSubId" placeholder="예: vibrator" class="w-full px-3 py-2 bg-white border border-gray-200 rounded-xl text-xs">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-gray-600 mb-1">세부명 (한국어)</label>
                            <input type="text" id="newSubKo" placeholder="예: 바이브레이터" class="w-full px-3 py-2 bg-white border border-gray-200 rounded-xl text-xs">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-gray-600 mb-1">세부명 (영어)</label>
                            <input type="text" id="newSubEn" placeholder="예: Vibrator" class="w-full px-3 py-2 bg-white border border-gray-200 rounded-xl text-xs">
                        </div>
                    </div>
                    <button onclick="addNewSubCategory()" class="px-5 py-2.5 bg-aura-dark text-white text-xs font-semibold rounded-xl hover:bg-gray-800 transition-colors">세부 카테고리 추가하기</button>
                </div>

                <!-- 3. Add Product Form -->
                <div class="bg-gray-50 p-5 rounded-2xl border border-gray-200 space-y-4">
                    <h4 class="font-bold text-sm text-aura-dark">새 상품 등록</h4>
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-xs font-semibold text-gray-600 mb-1">상품명 (한국어)</label>
                            <input type="text" id="newTitleKo" placeholder="예: 프리미엄 바이브레이터" class="w-full px-3 py-2 bg-white border border-gray-200 rounded-xl text-xs">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-gray-600 mb-1">상품명 (영어)</label>
                            <input type="text" id="newTitleEn" placeholder="예: Premium Vibrator" class="w-full px-3 py-2 bg-white border border-gray-200 rounded-xl text-xs">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-gray-600 mb-1">카테고리</label>
                            <select id="newCategorySelect" onchange="updateDevSubCategoryOptions()" class="w-full px-3 py-2 bg-white border border-gray-200 rounded-xl text-xs">
                                <!-- Populated dynamically -->
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-gray-600 mb-1">하위 카테고리</label>
                            <select id="newSubCategorySelect" class="w-full px-3 py-2 bg-white border border-gray-200 rounded-xl text-xs">
                                <!-- Populated dynamically -->
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-gray-600 mb-1">가격 (원)</label>
                            <input type="number" id="newPrice" placeholder="59000" class="w-full px-3 py-2 bg-white border border-gray-200 rounded-xl text-xs">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-gray-600 mb-1">이미지 URL</label>
                            <input type="text" id="newImage" placeholder="https://images.unsplash.com/..." class="w-full px-3 py-2 bg-white border border-gray-200 rounded-xl text-xs">
                        </div>
                    </div>
                    <button onclick="addNewProductFromDev()" class="px-5 py-2.5 bg-aura-dark text-white text-xs font-semibold rounded-xl hover:bg-gray-800 transition-colors">상품 등록하기</button>
                </div>

                <!-- Product Management List -->
                <div>
                    <h4 class="font-bold text-sm text-aura-dark mb-3">등록된 상품 목록 및 삭제</h4>
                    <div id="devProductList" class="space-y-2 max-h-60 overflow-y-auto border border-gray-200 rounded-xl p-3 bg-white">
                        <!-- Populated via JS -->
                    </div>
                </div>
            </div>

            <div class="p-4 border-t border-gray-200 bg-gray-50 flex justify-end">
                <button onclick="closeDevPanelModal()" class="px-5 py-2 bg-aura-dark text-white text-xs font-semibold rounded-xl">닫기</button>
            </div>
        </div>
    </div>

    <!-- Toast Notification Container -->
    <div id="toastContainer" class="fixed bottom-6 right-6 z-50 flex flex-col gap-2 pointer-events-none"></div>

    <!-- Footer -->
    <footer class="bg-white text-aura-dark pt-12 pb-10 border-t border-gray-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid grid-cols-1 md:grid-cols-4 gap-8 mb-8">
            <div>
                <div class="flex items-center gap-2 mb-3">
                    <div class="w-8 h-8 rounded-lg bg-aura-dark text-white flex items-center justify-center font-bold text-sm">A</div>
                    <span class="font-bold text-lg">AURA</span>
                </div>
                <p class="text-gray-500 text-sm leading-relaxed mb-4" data-i18n="footer_desc">
                    엄선된 제품과 편리한 서비스로 만족스러운 쇼핑 경험을 제공합니다.
                </p>
                <div class="flex items-center gap-3">
                    <a href="#" class="w-8 h-8 rounded-lg bg-gray-100 text-gray-600 flex items-center justify-center hover:bg-gray-200 transition-colors"><i data-lucide="instagram" class="w-4 h-4"></i></a>
                    <a href="#" class="w-8 h-8 rounded-lg bg-gray-100 text-gray-600 flex items-center justify-center hover:bg-gray-200 transition-colors"><i data-lucide="message-square" class="w-4 h-4"></i></a>
                </div>
            </div>
            <div>
                <h4 class="text-xs font-bold uppercase tracking-wider text-gray-400 mb-3" data-i18n="footer_col_1">고객 센터</h4>
                <ul class="space-y-2 text-sm text-gray-600">
                    <li><a href="#" class="hover:text-aura-dark transition-colors" data-i18n="faq">공지사항 / FAQ</a></li>
                    <li><a href="#" class="hover:text-aura-dark transition-colors" data-i18n="shipping_guide">배송 및 반품 안내</a></li>
                    <li><a href="#" class="hover:text-aura-dark transition-colors" data-i18n="inquiry">1:1 문의</a></li>
                </ul>
            </div>
            <div>
                <h4 class="text-xs font-bold uppercase tracking-wider text-gray-400 mb-3" data-i18n="footer_col_2">상품 카테고리</h4>
                <ul id="footerCategoriesList" class="space-y-2 text-sm text-gray-600">
                    <!-- Dynamic -->
                </ul>
            </div>
            <div>
                <h4 class="text-xs font-bold uppercase tracking-wider text-gray-400 mb-3" data-i18n="footer_col_3">뉴스레터 구독</h4>
                <p class="text-sm text-gray-600 mb-3" data-i18n="newsletter_desc">신상품 소식과 할인 혜택을 받아보세요.</p>
                <div class="flex gap-2">
                    <input type="email" placeholder="이메일 주소" data-i18n-placeholder="email_placeholder" class="bg-gray-100 border border-transparent rounded-xl px-3.5 py-2 text-sm w-full focus:outline-none focus:border-aura-dark text-aura-dark">
                    <button onclick="showToast('뉴스레터 구독이 완료되었습니다.', 'Subscribed successfully.');" class="bg-aura-dark text-white px-4 py-2 rounded-xl hover:bg-gray-800 transition-colors font-medium text-sm" data-i18n="subscribe_btn">구독</button>
                </div>
            </div>
        </div>
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pt-6 border-t border-gray-200 text-center text-xs text-gray-400">
            &copy; 2026 AURA Lifestyle Shop. All Rights Reserved.
        </div>
    </footer>

    <!-- JavaScript Application Logic -->
    <script>
        // Multilingual Static Dictionary
        const translations = {
            ko: {
                tagline: "Lifestyle Shop",
                search_placeholder: "상품명을 검색해 보세요...",
                language_label: "언어 선택 (Language)",
                menu_title: "메뉴 및 카테고리",
                categories_title: "상품 카테고리",
                quick_links: "바로가기",
                nav_all_products: "전체 상품 보기",
                nav_wishlist: "관심 상품",
                hero_badge: "2026 신상품 입고 완료",
                hero_title_1: "일상을 더욱 가치 있게",
                hero_title_2: "AURA 라이프스타일 샵",
                hero_desc: "전자기기, 게이밍 기어부터 취미용품, 차량용품 및 웰니스까지, 당신의 일상을 채워줄 다양한 상품들을 만나보세요.",
                hero_cta: "상품 둘러보기",
                hero_cta_secondary: "게이밍 기어",
                banner_card_title: "스페셜 컬렉션",
                banner_card_sub: "MD 추천 인기 상품",
                curated_subtitle: "FEATURED PRODUCTS",
                curated_title: "추천상품",
                no_products_title: "검색 결과가 없습니다",
                no_products_desc: "다른 검색어를 입력하시거나 카테고리를 변경해 보세요.",
                reset_filter_btn: "전체 상품 보기",
                cart_title: "장바구니",
                subtotal: "상품 금액",
                shipping: "배송비",
                free_shipping: "무료",
                total: "총 결제금액",
                checkout_btn: "주문하기",
                wishlist_title: "관심 상품",
                close_btn: "닫기",
                footer_desc: "엄선된 제품과 편리한 서비스로 만족스러운 쇼핑 경험을 제공합니다.",
                footer_col_1: "고객 센터",
                faq: "공지사항 / FAQ",
                shipping_guide: "배송 및 반품 안내",
                inquiry: "1:1 문의",
                footer_col_2: "상품 카테고리",
                footer_col_3: "뉴스레터 구독",
                newsletter_desc: "신상품 소식과 할인 혜택을 받아보세요.",
                email_placeholder: "이메일 주소",
                subscribe_btn: "구독",
                add_to_cart: "장바구니 담기",
                cart_empty: "장바구니가 비어 있습니다.",
                wishlist_empty: "관심 상품이 없습니다."
            },
            en: {
                tagline: "Lifestyle Shop",
                search_placeholder: "Search products...",
                language_label: "Language",
                menu_title: "Menu & Categories",
                categories_title: "Categories",
                quick_links: "Quick Links",
                nav_all_products: "All Products",
                nav_wishlist: "Wishlist",
                hero_badge: "New Arrivals 2026",
                hero_title_1: "Elevate Your Everyday Life",
                hero_title_2: "AURA Lifestyle Shop",
                hero_desc: "Discover a wide range of electronics, gaming gear, hobby items, car accessories, and wellness products to enrich your daily life.",
                hero_cta: "Browse Products",
                hero_cta_secondary: "Gaming Gear",
                banner_card_title: "Special Collection",
                banner_card_sub: "MD Recommended Picks",
                curated_subtitle: "FEATURED PRODUCTS",
                curated_title: "Recommended Products",
                no_products_title: "No products found",
                no_products_desc: "Try searching with different keywords or change categories.",
                reset_filter_btn: "View All Products",
                cart_title: "Shopping Cart",
                subtotal: "Subtotal",
                shipping: "Shipping",
                free_shipping: "Free",
                total: "Total",
                checkout_btn: "Proceed to Checkout",
                wishlist_title: "Wishlist",
                close_btn: "Close",
                footer_desc: "Providing a satisfying shopping experience with carefully selected products and convenient services.",
                footer_col_1: "Customer Care",
                faq: "FAQ / Notice",
                shipping_guide: "Shipping & Returns",
                inquiry: "Support",
                footer_col_2: "Categories",
                footer_col_3: "Newsletter",
                newsletter_desc: "Subscribe to receive new arrivals and discount offers.",
                email_placeholder: "Email address",
                subscribe_btn: "Subscribe",
                add_to_cart: "Add to Cart",
                cart_empty: "Your cart is empty.",
                wishlist_empty: "Your wishlist is empty."
            }
        };

        // Dynamic Categories Structure
        let categoriesData = [
            {
                id: 'elec',
                ko: '전자기기 (Electronics)',
                en: 'Electronics',
                subs: [
                    { id: 'audio', ko: '오디오 및 스피커', en: 'Audio & Speakers' },
                    { id: 'gadget', ko: '스마트 가젯', en: 'Smart Gadgets' }
                ]
            },
            {
                id: 'gaming',
                ko: '게이밍 (Gaming)',
                en: 'Gaming',
                subs: [
                    { id: 'gear', ko: '게이밍 기어', en: 'Gaming Gear' },
                    { id: 'console', ko: '콘솔 액세서리', en: 'Console Accessories' }
                ]
            },
            {
                id: 'hobby',
                ko: '취미용품 (Hobby)',
                en: 'Hobby',
                subs: [
                    { id: 'camping', ko: '캠핑 및 아웃도어', en: 'Camping & Outdoor' },
                    { id: 'stationery', ko: '문구 및 굿즈', en: 'Stationery & Goods' }
                ]
            },
            {
                id: 'car',
                ko: '차량용품 (Car)',
                en: 'Car Accessories',
                subs: [
                    { id: 'interior', ko: '차량 인테리어', en: 'Car Interior' },
                    { id: 'care', ko: '방향제 및 관리', en: 'Air Fresheners & Care' }
                ]
            },
            {
                id: 'apparel',
                ko: '의류 (Apparel)',
                en: 'Apparel',
                subs: [
                    { id: 'casual', ko: '캐주얼 의류', en: 'Casual Apparel' }
                ]
            },
            {
                id: 'beauty',
                ko: '뷰티 (Beauty)',
                en: 'Beauty',
                subs: [
                    { id: 'skincare', ko: '스킨케어', en: 'Skincare' }
                ]
            }
        ];

        // Product Database
        let products = [
            {
                id: 1,
                category: 'gaming',
                subCategory: 'gear',
                titleKo: 'RGB 기계식 게이밍 키보드',
                titleEn: 'RGB Mechanical Gaming Keyboard',
                price: 89000,
                rating: 4.9,
                reviews: 142,
                image: 'https://images.unsplash.com/photo-1587829741301-dc798b83add3?auto=format&fit=crop&q=80&w=800',
                tagKo: 'BEST',
                tagEn: 'BEST'
            },
            {
                id: 2,
                category: 'gaming',
                subCategory: 'gear',
                titleKo: '초경량 와이어리스 게이밍 마우스',
                titleEn: 'Ultralight Wireless Gaming Mouse',
                price: 72000,
                rating: 4.8,
                reviews: 98,
                image: 'https://images.unsplash.com/photo-1615663245857-ac93bb7c39e7?auto=format&fit=crop&q=80&w=800',
                tagKo: 'POPULAR',
                tagEn: 'POPULAR'
            },
            {
                id: 3,
                category: 'gaming',
                subCategory: 'console',
                titleKo: '콘솔 컨트롤러 충전 독 스탠드',
                titleEn: 'Console Controller Charging Dock',
                price: 34000,
                rating: 4.7,
                reviews: 45,
                image: 'https://images.unsplash.com/photo-1600080972464-8e5f35f63d08?auto=format&fit=crop&q=80&w=800',
                tagKo: 'RECOMMENDED',
                tagEn: 'RECOMMENDED'
            },
            {
                id: 4,
                category: 'gaming',
                subCategory: 'gear',
                titleKo: '7.1 채널 서라운드 게이밍 헤드셋',
                titleEn: '7.1 Surround Sound Gaming Headset',
                price: 98000,
                rating: 4.9,
                reviews: 110,
                image: 'https://images.unsplash.com/photo-1590658268037-6bf12165a8df?auto=format&fit=crop&q=80&w=800',
                tagKo: 'BEST',
                tagEn: 'BEST'
            },
            {
                id: 5,
                category: 'elec',
                subCategory: 'audio',
                titleKo: '노이즈 캔슬링 블루투스 헤드폰',
                titleEn: 'Active Noise Cancelling Headphones',
                price: 189000,
                rating: 5.0,
                reviews: 215,
                image: 'https://images.unsplash.com/photo-1505740420928-5e560c06d30e?auto=format&fit=crop&q=80&w=800',
                tagKo: 'BEST',
                tagEn: 'BEST'
            },
            {
                id: 6,
                category: 'elec',
                subCategory: 'audio',
                titleKo: '포터블 방수 블루투스 스피커',
                titleEn: 'Portable Waterproof Bluetooth Speaker',
                price: 65000,
                rating: 4.8,
                reviews: 88,
                image: 'https://images.unsplash.com/photo-1545454675-3531b543be5d?auto=format&fit=crop&q=80&w=800',
                tagKo: 'POPULAR',
                tagEn: 'POPULAR'
            },
            {
                id: 7,
                category: 'elec',
                subCategory: 'gadget',
                titleKo: '3-in-1 무선 충전 패드 스탠드',
                titleEn: '3-in-1 Wireless Charging Stand',
                price: 52000,
                rating: 4.7,
                reviews: 76,
                image: 'https://images.unsplash.com/photo-1622445275576-721325763dc0?auto=format&fit=crop&q=80&w=800',
                tagKo: 'NEW',
                tagEn: 'NEW'
            },
            {
                id: 8,
                category: 'elec',
                subCategory: 'gadget',
                titleKo: '데스크 LED 모니터 라이트 바',
                titleEn: 'Desk LED Monitor Light Bar',
                price: 45000,
                rating: 4.9,
                reviews: 64,
                image: 'https://images.unsplash.com/photo-1593508512255-86ab42a8e620?auto=format&fit=crop&q=80&w=800',
                tagKo: 'STEADY',
                tagEn: 'STEADY'
            },
            {
                id: 9,
                category: 'hobby',
                subCategory: 'camping',
                titleKo: 'LED 랜턴 겸용 캠핑 버너',
                titleEn: 'Camping Lantern & Stove Combo',
                price: 78000,
                rating: 4.9,
                reviews: 53,
                image: 'https://images.unsplash.com/photo-1510312305653-8ed496efae75?auto=format&fit=crop&q=80&w=800',
                tagKo: 'NEW',
                tagEn: 'NEW'
            },
            {
                id: 10,
                category: 'hobby',
                subCategory: 'camping',
                titleKo: '접이식 초경량 아웃도어 체어',
                titleEn: 'Foldable Ultralight Outdoor Chair',
                price: 49000,
                rating: 4.8,
                reviews: 91,
                image: 'https://images.unsplash.com/photo-1504280390367-361c6d9f38f4?auto=format&fit=crop&q=80&w=800',
                tagKo: 'POPULAR',
                tagEn: 'POPULAR'
            },
            {
                id: 11,
                category: 'hobby',
                subCategory: 'stationery',
                titleKo: '디자인 하드커버 저널 & 펜 세트',
                titleEn: 'Designer Hardcover Journal & Pen Set',
                price: 24000,
                rating: 4.7,
                reviews: 38,
                image: 'https://images.unsplash.com/photo-1544716278-ca5e3f4abd8c?auto=format&fit=crop&q=80&w=800',
                tagKo: 'STEADY',
                tagEn: 'STEADY'
            },
            {
                id: 12,
                category: 'car',
                subCategory: 'care',
                titleKo: '프리미엄 천연 우드 차량용 방향제',
                titleEn: 'Premium Natural Wood Car Air Freshener',
                price: 28000,
                rating: 4.9,
                reviews: 120,
                image: 'https://images.unsplash.com/photo-1617886364736-224479e1381e?auto=format&fit=crop&q=80&w=800',
                tagKo: 'BEST',
                tagEn: 'BEST'
            },
            {
                id: 13,
                category: 'car',
                subCategory: 'interior',
                titleKo: '오토 센서 무선 충전 스마트폰 거치대',
                titleEn: 'Auto-Sensor Wireless Car Mount Charger',
                price: 42000,
                rating: 4.8,
                reviews: 165,
                image: 'https://images.unsplash.com/photo-1584438784894-089d6a62b8fa?auto=format&fit=crop&q=80&w=800',
                tagKo: 'BEST',
                tagEn: 'BEST'
            },
            {
                id: 14,
                category: 'car',
                subCategory: 'interior',
                titleKo: '논슬립 대시보드 다목적 패드',
                titleEn: 'Non-slip Dashboard Multi-Purpose Pad',
                price: 15000,
                rating: 4.6,
                reviews: 82,
                image: 'https://images.unsplash.com/photo-1502877338535-766e1452684a?auto=format&fit=crop&q=80&w=800',
                tagKo: 'POPULAR',
                tagEn: 'POPULAR'
            },
            {
                id: 15,
                category: 'apparel',
                subCategory: 'casual',
                titleKo: '베이직 코튼 후드 집업',
                titleEn: 'Basic Cotton Hooded Zip-Up',
                price: 58000,
                rating: 4.8,
                reviews: 74,
                image: 'https://images.unsplash.com/photo-1556905055-8f358a7a47b2?auto=format&fit=crop&q=80&w=800',
                tagKo: 'POPULAR',
                tagEn: 'POPULAR'
            },
            {
                id: 16,
                category: 'beauty',
                subCategory: 'skincare',
                titleKo: '밸런싱 허브 토너 & 로션 세트',
                titleEn: 'Balancing Herb Toner & Lotion Set',
                price: 38000,
                rating: 4.9,
                reviews: 93,
                image: 'https://images.unsplash.com/photo-1608248597359-9742467d56e6?auto=format&fit=crop&q=80&w=800',
                tagKo: 'STEADY',
                tagEn: 'STEADY'
            }
        ];

        // Application State
        let currentLang = 'ko';
        let cart = [];
        let wishlist = [];
        let currentCategory = 'all';
        let currentSubCategory = 'all';
        let searchQuery = '';

        // Initialize App
        window.addEventListener('DOMContentLoaded', () => {
            renderMenuCategories();
            renderFooterCategories();
            lucide.createIcons();
            renderProducts();
            updateCartBadge();
            updateWishlistBadge();
        });

        // Language Switcher
        function setLanguage(lang) {
            currentLang = lang;
            
            const koBtn = document.getElementById('langKoBtn');
            const enBtn = document.getElementById('langEnBtn');
            if (lang === 'ko') {
                koBtn.className = "px-3 py-1 text-xs font-bold rounded-md transition-all bg-aura-dark text-white";
                enBtn.className = "px-3 py-1 text-xs font-bold rounded-md transition-all text-gray-600 hover:text-aura-dark";
            } else {
                enBtn.className = "px-3 py-1 text-xs font-bold rounded-md transition-all bg-aura-dark text-white";
                koBtn.className = "px-3 py-1 text-xs font-bold rounded-md transition-all text-gray-600 hover:text-aura-dark";
            }

            document.querySelectorAll('[data-i18n]').forEach(el => {
                const key = el.getAttribute('data-i18n');
                if (translations[lang][key]) {
                    el.innerText = translations[lang][key];
                }
            });

            document.querySelectorAll('[data-i18n-placeholder]').forEach(el => {
                const key = el.getAttribute('data-i18n-placeholder');
                if (translations[lang][key]) {
                    el.placeholder = translations[lang][key];
                }
            });

            renderMenuCategories();
            renderFooterCategories();
            renderProducts();
            renderCart();
            renderWishlistModalContent();
        }

        // Render Hamburger Menu Categories Dynamically
        function renderMenuCategories() {
            const container = document.getElementById('categoryAccordionContainer');
            container.innerHTML = categoriesData.map(cat => {
                const catName = currentLang === 'ko' ? cat.ko : cat.en;
                const subsHtml = cat.subs.map(sub => {
                    const subName = currentLang === 'ko' ? sub.ko : sub.en;
                    return `<button onclick="filterByCategory('${cat.id}', '${sub.id}')" class="w-full text-left py-1.5 px-3 text-gray-600 hover:text-aura-dark hover:bg-white rounded-lg transition-colors">${subName}</button>`;
                }).join('');

                return `
                    <div class="border border-gray-200 rounded-xl overflow-hidden">
                        <button onclick="toggleCategoryAccordion('${cat.id}Sub')" class="w-full p-3.5 flex items-center justify-between bg-white hover:bg-gray-50 transition-colors text-left text-sm font-medium">
                            <span>${catName}</span>
                            <i data-lucide="chevron-down" id="${cat.id}SubIcon" class="w-4 h-4 text-gray-400 transition-transform"></i>
                        </button>
                        <div id="${cat.id}Sub" class="hidden bg-gray-50 px-3 py-2 space-y-1 border-t border-gray-200 text-sm">
                            <button onclick="filterByCategory('${cat.id}', 'all')" class="w-full text-left py-1.5 px-3 text-gray-600 hover:text-aura-dark hover:bg-white rounded-lg transition-colors">${currentLang === 'ko' ? '전체 ' + catName : 'All ' + cat.en}</button>
                            ${subsHtml}
                        </div>
                    </div>
                `;
            }).join('');
            lucide.createIcons();
        }

        // Render Footer Categories Dynamically
        function renderFooterCategories() {
            const list = document.getElementById('footerCategoriesList');
            list.innerHTML = categoriesData.map(cat => {
                const catName = currentLang === 'ko' ? cat.ko : cat.en;
                return `<li><a href="#" onclick="filterByCategory('${cat.id}', 'all')" class="hover:text-aura-dark transition-colors">${catName}</a></li>`;
            }).join('');
        }

        // Toggle Hamburger Menu Drawer
        function toggleMenuDrawer() {
            const drawer = document.getElementById('menuDrawer');
            const overlay = document.getElementById('menuOverlay');
            const isOpen = !drawer.classList.contains('translate-x-full');

            if (isOpen) {
                drawer.classList.add('translate-x-full');
                overlay.classList.add('opacity-0', 'hidden');
                overlay.classList.remove('opacity-100');
            } else {
                drawer.classList.remove('translate-x-full');
                overlay.classList.remove('hidden');
                setTimeout(() => overlay.classList.add('opacity-100'), 10);
            }
        }

        // Toggle Category Accordions
        function toggleCategoryAccordion(subId) {
            const sub = document.getElementById(subId);
            const icon = document.getElementById(subId + 'Icon');
            sub.classList.toggle('hidden');
            icon.classList.toggle('rotate-180');
        }

        // Toggle Shopping Cart Drawer
        function toggleCartDrawer() {
            const drawer = document.getElementById('cartDrawer');
            const overlay = document.getElementById('cartOverlay');
            const isOpen = !drawer.classList.contains('translate-x-full');

            if (isOpen) {
                drawer.classList.add('translate-x-full');
                overlay.classList.add('opacity-0', 'hidden');
                overlay.classList.remove('opacity-100');
            } else {
                renderCart();
                drawer.classList.remove('translate-x-full');
                overlay.classList.remove('hidden');
                setTimeout(() => overlay.classList.add('opacity-100'), 10);
            }
        }

        // Mobile Search Toggle
        function toggleMobileSearch() {
            const container = document.getElementById('mobileSearchContainer');
            container.classList.toggle('hidden');
            if (!container.classList.contains('hidden')) {
                document.getElementById('mobileSearchInput').focus();
            }
        }

        // Filter Products
        function filterByCategory(category, subCategory) {
            currentCategory = category;
            currentSubCategory = subCategory;
            searchQuery = '';
            document.getElementById('searchInput').value = '';
            document.getElementById('mobileSearchInput').value = '';

            const drawer = document.getElementById('menuDrawer');
            if (!drawer.classList.contains('translate-x-full')) {
                toggleMenuDrawer();
            }

            const badge = document.getElementById('activeFilterBadge');
            const badgeText = document.getElementById('activeFilterText');
            badge.classList.remove('hidden');
            badge.classList.add('flex');
            badgeText.innerText = `${category.toUpperCase()} > ${subCategory.toUpperCase()}`;

            renderProducts();
            document.getElementById('products-section').scrollIntoView({ behavior: 'smooth' });
        }

        // Reset Filters
        function resetFilters() {
            currentCategory = 'all';
            currentSubCategory = 'all';
            searchQuery = '';
            document.getElementById('searchInput').value = '';
            document.getElementById('mobileSearchInput').value = '';
            document.getElementById('activeFilterBadge').classList.add('hidden');
            document.getElementById('activeFilterBadge').classList.remove('flex');
            
            renderProducts();
        }

        // Real-time Search & Secret Developer Trigger ("goyangida")
        function handleSearch(query) {
            const cleanQuery = query.trim().toLowerCase();
            if (cleanQuery === 'goyangida') {
                document.getElementById('searchInput').value = '';
                document.getElementById('mobileSearchInput').value = '';
                openDevPasswordModal();
                return;
            }
            searchQuery = cleanQuery;
            renderProducts();
        }

        // Developer Password Modal Logic
        function openDevPasswordModal() {
            document.getElementById('devPasswordInput').value = '';
            document.getElementById('devPasswordModal').classList.remove('hidden');
            document.getElementById('devPasswordInput').focus();
        }

        function closeDevPasswordModal() {
            document.getElementById('devPasswordModal').classList.add('hidden');
        }

        function verifyDevPassword() {
            const inputVal = document.getElementById('devPasswordInput').value.trim();
            const d = new Date();
            const year = d.getFullYear();
            const month = String(d.getMonth() + 1).padStart(2, '0');
            const day = String(d.getDate()).padStart(2, '0');
            const correctPassword = `${year}${month}${day}`;

            if (inputVal === correctPassword) {
                closeDevPasswordModal();
                openDevPanelModal();
                showToast('개발자 인증 성공!', 'Developer authentication successful!');
            } else {
                showToast('비밀번호가 올바르지 않습니다.', 'Incorrect password.');
            }
        }

        // Developer Panel Modal Logic
        function openDevPanelModal() {
            renderDevProductList();
            populateDevCategoryDropdowns();
            document.getElementById('devPanelModal').classList.remove('hidden');
        }

        function closeDevPanelModal() {
            document.getElementById('devPanelModal').classList.add('hidden');
            renderMenuCategories();
            renderFooterCategories();
            renderProducts();
        }

        function populateDevCategoryDropdowns() {
            const subParentSelect = document.getElementById('subParentSelect');
            const newCatSelect = document.getElementById('newCategorySelect');

            subParentSelect.innerHTML = categoriesData.map(c => `<option value="${c.id}">${c.ko} (${c.id})</option>`).join('');
            newCatSelect.innerHTML = categoriesData.map(c => `<option value="${c.id}">${c.ko} (${c.id})</option>`).join('');
            updateDevSubCategoryOptions();
        }

        function updateDevSubCategoryOptions() {
            const catId = document.getElementById('newCategorySelect').value;
            const subCatSelect = document.getElementById('newSubCategorySelect');
            const catObj = categoriesData.find(c => c.id === catId);

            if (catObj && catObj.subs.length > 0) {
                subCatSelect.innerHTML = catObj.subs.map(s => `<option value="${s.id}">${s.ko} (${s.id})</option>`).join('');
            } else {
                subCatSelect.innerHTML = '<option value="all">전체 (all)</option>';
            }
        }

        // Add New Main Category
        function addNewMainCategory() {
            const id = document.getElementById('newCatId').value.trim().toLowerCase();
            const ko = document.getElementById('newCatKo').value.trim();
            const en = document.getElementById('newCatEn').value.trim();

            if (!id || !ko || !en) {
                showToast('카테고리 정보를 모두 입력해 주세요.', 'Please fill in all category fields.');
                return;
            }

            if (categoriesData.some(c => c.id === id)) {
                showToast('이미 존재하는 카테고리 ID입니다.', 'Category ID already exists.');
                return;
            }

            categoriesData.push({
                id,
                ko,
                en,
                subs: [{ id: 'general', ko: '일반', en: 'General' }]
            });

            document.getElementById('newCatId').value = '';
            document.getElementById('newCatKo').value = '';
            document.getElementById('newCatEn').value = '';

            populateDevCategoryDropdowns();
            showToast('새 카테고리가 추가되었습니다.', 'New main category added.');
        }

        // Add New Subcategory
        function addNewSubCategory() {
            const parentId = document.getElementById('subParentSelect').value;
            const subId = document.getElementById('newSubId').value.trim().toLowerCase();
            const ko = document.getElementById('newSubKo').value.trim();
            const en = document.getElementById('newSubEn').value.trim();

            if (!subId || !ko || !en) {
                showToast('세부 카테고리 정보를 모두 입력해 주세요.', 'Please fill in all subcategory fields.');
                return;
            }

            const parentCat = categoriesData.find(c => c.id === parentId);
            if (parentCat) {
                if (parentCat.subs.some(s => s.id === subId)) {
                    showToast('이미 존재하는 세부 카테고리 ID입니다.', 'Subcategory ID already exists.');
                    return;
                }
                parentCat.subs.push({ id: subId, ko, en });

                document.getElementById('newSubId').value = '';
                document.getElementById('newSubKo').value = '';
                document.getElementById('newSubEn').value = '';

                updateDevSubCategoryOptions();
                showToast('새 세부 카테고리가 추가되었습니다.', 'New subcategory added.');
            }
        }

        function renderDevProductList() {
            const container = document.getElementById('devProductList');
            if (products.length === 0) {
                container.innerHTML = '<p class="text-xs text-gray-400 text-center py-4">등록된 상품이 없습니다.</p>';
                return;
            }
            container.innerHTML = products.map(p => `
                <div class="flex items-center justify-between p-2.5 bg-gray-50 rounded-lg border border-gray-100">
                    <div class="flex items-center gap-3">
                        <img src="${p.image}" class="w-10 h-10 object-cover rounded-md border bg-white">
                        <div>
                            <div class="text-xs font-bold text-aura-dark">${p.titleKo}</div>
                            <div class="text-[10px] text-gray-500">₩${p.price.toLocaleString()} | ${p.category} > ${p.subCategory}</div>
                        </div>
                    </div>
                    <button onclick="deleteProduct(${p.id})" class="px-3 py-1 bg-red-100 text-red-600 text-xs font-semibold rounded-lg hover:bg-red-200 transition-colors">삭제</button>
                </div>
            `).join('');
        }

        function deleteProduct(id) {
            products = products.filter(p => p.id !== id);
            renderDevProductList();
            renderProducts();
            showToast('상품이 삭제되었습니다.', 'Product deleted.');
        }

        function addNewProductFromDev() {
            const titleKo = document.getElementById('newTitleKo').value.trim();
            const titleEn = document.getElementById('newTitleEn').value.trim();
            const category = document.getElementById('newCategorySelect').value;
            const subCategory = document.getElementById('newSubCategorySelect').value;
            const price = parseInt(document.getElementById('newPrice').value);
            const image = document.getElementById('newImage').value.trim();

            if (!titleKo || !titleEn || isNaN(price) || !image) {
                showToast('모든 항목을 올바르게 입력해 주세요.', 'Please fill in all fields correctly.');
                return;
            }

            const newId = products.length > 0 ? Math.max(...products.map(p => p.id)) + 1 : 1;
            const newProd = {
                id: newId,
                category,
                subCategory,
                titleKo,
                titleEn,
                price,
                rating: 5.0,
                reviews: 1,
                image,
                tagKo: 'NEW',
                tagEn: 'NEW'
            };

            products.unshift(newProd);
            
            document.getElementById('newTitleKo').value = '';
            document.getElementById('newTitleEn').value = '';
            document.getElementById('newPrice').value = '';
            document.getElementById('newImage').value = '';

            renderDevProductList();
            renderProducts();
            showToast('새 상품이 성공적으로 등록되었습니다.', 'New product registered successfully.');
        }

        // Render Product Grid
        function renderProducts() {
            const grid = document.getElementById('productGrid');
            const emptyState = document.getElementById('emptyState');
            const productCountEl = document.getElementById('productCount');

            let filtered = products.filter(p => {
                const matchesCategory = currentCategory === 'all' || p.category === currentCategory;
                const matchesSub = currentSubCategory === 'all' || p.subCategory === currentSubCategory;
                const matchesSearch = searchQuery === '' || 
                    p.titleKo.toLowerCase().includes(searchQuery) || 
                    p.titleEn.toLowerCase().includes(searchQuery);
                return matchesCategory && matchesSub && matchesSearch;
            });

            productCountEl.innerText = filtered.length;

            if (filtered.length === 0) {
                grid.innerHTML = '';
                emptyState.classList.remove('hidden');
                return;
            }

            emptyState.classList.add('hidden');

            grid.innerHTML = filtered.map(p => {
                const isWishlisted = wishlist.includes(p.id);
                const title = currentLang === 'ko' ? p.titleKo : p.titleEn;
                const tag = currentLang === 'ko' ? p.tagKo : p.tagEn;
                const formattedPrice = '₩' + p.price.toLocaleString();

                return `
                    <div class="standard-card group bg-white rounded-2xl border border-gray-200 overflow-hidden shadow-sm flex flex-col justify-between">
                        <div>
                            <div class="relative aspect-square bg-gray-100 overflow-hidden">
                                <img src="${p.image}" alt="${title}" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-300">
                                
                                <span class="absolute top-3 left-3 bg-white/90 backdrop-blur-sm text-aura-dark text-[10px] font-bold px-2.5 py-1 rounded-md shadow-sm border border-gray-200">
                                    ${tag}
                                </span>

                                <button onclick="toggleWishlist(${p.id})" class="absolute top-3 right-3 w-9 h-9 bg-white/90 backdrop-blur-sm rounded-xl flex items-center justify-center text-aura-dark hover:bg-gray-100 transition-colors shadow-sm border border-gray-200">
                                    <i data-lucide="heart" class="w-4 h-4 ${isWishlisted ? 'text-red-500 fill-red-500' : ''}"></i>
                                </button>
                            </div>

                            <div class="p-4">
                                <div class="flex items-center gap-1 text-amber-500 text-xs mb-1 font-semibold">
                                    <i data-lucide="star" class="w-3.5 h-3.5 fill-amber-500"></i>
                                    <span>${p.rating}</span>
                                    <span class="text-gray-400 font-normal">(${p.reviews})</span>
                                </div>
                                <h3 class="font-medium text-aura-dark text-sm line-clamp-2 mb-2 group-hover:text-black transition-colors">
                                    ${title}
                                </h3>
                                <div class="text-base font-bold text-aura-dark">
                                    ${formattedPrice}
                                </div>
                            </div>
                        </div>

                        <div class="p-4 pt-0">
                            <button onclick="addToCart(${p.id})" class="w-full py-2.5 bg-gray-100 hover:bg-aura-dark hover:text-white text-aura-dark font-medium text-xs rounded-xl transition-colors duration-200 flex items-center justify-center gap-2">
                                <i data-lucide="shopping-bag" class="w-3.5 h-3.5"></i>
                                <span data-i18n="add_to_cart">${translations[currentLang].add_to_cart}</span>
                            </button>
                        </div>
                    </div>
                `;
            }).join('');

            lucide.createIcons();
        }

        // Add to Cart
        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            const existing = cart.find(item => item.id === productId);

            if (existing) {
                existing.quantity += 1;
            } else {
                cart.push({ ...product, quantity: 1 });
            }

            updateCartBadge();
            renderCart();
            
            const title = currentLang === 'ko' ? product.titleKo : product.titleEn;
            showToast(`장바구니에 담겼습니다: ${title}`, `Added to cart: ${title}`);
        }

        function updateCartBadge() {
            const totalCount = cart.reduce((sum, item) => sum + item.quantity, 0);
            document.getElementById('cartCountBadge').innerText = totalCount;
        }

        function renderCart() {
            const container = document.getElementById('cartItemsContainer');
            const subtotalEl = document.getElementById('cartSubtotal');
            const totalEl = document.getElementById('cartTotal');

            if (cart.length === 0) {
                container.innerHTML = `
                    <div class="text-center py-16 text-gray-400">
                        <span class="text-3xl mb-2 block">🛒</span>
                        <p class="text-sm font-medium" data-i18n="cart_empty">${translations[currentLang].cart_empty}</p>
                    </div>
                `;
                subtotalEl.innerText = '₩0';
                totalEl.innerText = '₩0';
                lucide.createIcons();
                return;
            }

            let subtotal = 0;

            container.innerHTML = cart.map(item => {
                const title = currentLang === 'ko' ? item.titleKo : item.titleEn;
                const itemTotal = item.price * item.quantity;
                subtotal += itemTotal;

                return `
                    <div class="flex gap-4 py-4 items-center">
                        <img src="${item.image}" alt="${title}" class="w-16 h-16 object-cover rounded-xl border border-gray-200 bg-gray-100 flex-shrink-0">
                        <div class="flex-1 min-w-0">
                            <h4 class="text-xs font-semibold text-aura-dark truncate mb-1">${title}</h4>
                            <div class="text-xs font-bold text-aura-dark mb-2">₩${item.price.toLocaleString()}</div>
                            
                            <div class="flex items-center gap-2">
                                <button onclick="updateQuantity(${item.id}, -1)" class="w-6 h-6 bg-gray-100 rounded-lg flex items-center justify-center text-aura-dark hover:bg-gray-200 transition-colors font-bold text-xs">-</button>
                                <span class="text-xs font-bold px-1">${item.quantity}</span>
                                <button onclick="updateQuantity(${item.id}, 1)" class="w-6 h-6 bg-gray-100 rounded-lg flex items-center justify-center text-aura-dark hover:bg-gray-200 transition-colors font-bold text-xs">+</button>
                            </div>
                        </div>
                        <button onclick="removeFromCart(${item.id})" class="p-2 text-gray-400 hover:text-red-500 transition-colors">
                            <i data-lucide="trash-2" class="w-4 h-4"></i>
                        </button>
                    </div>
                `;
            }).join('');

            subtotalEl.innerText = '₩' + subtotal.toLocaleString();
            totalEl.innerText = '₩' + subtotal.toLocaleString();
            lucide.createIcons();
        }

        function updateQuantity(productId, delta) {
            const item = cart.find(i => i.id === productId);
            if (item) {
                item.quantity += delta;
                if (item.quantity <= 0) {
                    removeFromCart(productId);
                } else {
                    updateCartBadge();
                    renderCart();
                }
            }
        }

        function removeFromCart(productId) {
            cart = cart.filter(i => i.id !== productId);
            updateCartBadge();
            renderCart();
        }

        function handleCheckout() {
            if (cart.length === 0) {
                showToast('장바구니가 비어 있습니다.', 'Your cart is empty.');
                return;
            }
            showToast('주문이 정상적으로 완료되었습니다.', 'Order placed successfully.');
            cart = [];
            updateCartBadge();
            renderCart();
            toggleCartDrawer();
        }

        function toggleWishlist(productId) {
            const index = wishlist.indexOf(productId);
            const product = products.find(p => p.id === productId);
            const title = currentLang === 'ko' ? product.titleKo : product.titleEn;

            if (index > -1) {
                wishlist.splice(index, 1);
                showToast(`관심 상품에서 해제되었습니다: ${title}`, `Removed from wishlist: ${title}`);
            } else {
                wishlist.push(productId);
                showToast(`관심 상품으로 등록되었습니다: ${title}`, `Added to wishlist: ${title}`);
            }

            updateWishlistBadge();
            renderProducts();
            renderWishlistModalContent();
        }

        function updateWishlistBadge() {
            const count = wishlist.length;
            document.getElementById('wishlistCountBadge').innerText = count;
            document.getElementById('drawerWishlistCount').innerText = count;
        }

        function openWishlistModal() {
            renderWishlistModalContent();
            document.getElementById('wishlistModalOverlay').classList.remove('hidden');
        }

        function closeWishlistModal() {
            document.getElementById('wishlistModalOverlay').classList.add('hidden');
        }

        function renderWishlistModalContent() {
            const content = document.getElementById('wishlistModalContent');

            if (wishlist.length === 0) {
                content.innerHTML = `
                    <div class="text-center py-16 text-gray-400">
                        <span class="text-3xl mb-2 block">❤️</span>
                        <p class="text-sm font-medium" data-i18n="wishlist_empty">${translations[currentLang].wishlist_empty}</p>
                    </div>
                `;
                lucide.createIcons();
                return;
            }

            const wishlistedProducts = products.filter(p => wishlist.includes(p.id));

            content.innerHTML = wishlistedProducts.map(p => {
                const title = currentLang === 'ko' ? p.titleKo : p.titleEn;
                return `
                    <div class="flex items-center justify-between p-3 border border-gray-200 rounded-xl bg-gray-50/50">
                        <div class="flex items-center gap-3">
                            <img src="${p.image}" alt="${title}" class="w-14 h-14 object-cover rounded-lg border border-gray-200 bg-white">
                            <div>
                                <h4 class="text-xs font-semibold text-aura-dark">${title}</h4>
                                <div class="text-xs font-bold text-aura-dark mt-1">₩${p.price.toLocaleString()}</div>
                            </div>
                        </div>
                        <div class="flex items-center gap-2">
                            <button onclick="addToCart(${p.id}); toggleWishlist(${p.id}); closeWishlistModal();" class="px-3 py-1.5 bg-aura-dark text-white text-xs font-medium rounded-lg hover:bg-gray-800 transition-colors">
                                담기
                            </button>
                            <button onclick="toggleWishlist(${p.id})" class="p-2 text-gray-400 hover:text-red-500 transition-colors">
                                <i data-lucide="trash-2" class="w-4 h-4"></i>
                            </button>
                        </div>
                    </div>
                `;
            }).join('');

            lucide.createIcons();
        }

        function showToast(koMsg, enMsg) {
            const container = document.getElementById('toastContainer');
            const message = currentLang === 'ko' ? koMsg : enMsg;
            
            const toast = document.createElement('div');
            toast.className = "bg-aura-dark text-white px-5 py-3 rounded-xl shadow-xl text-xs font-medium flex items-center gap-3 transform translate-y-4 opacity-0 transition-all duration-300 pointer-events-auto border border-white/10";
            toast.innerHTML = `<span>${message}</span>`;

            container.appendChild(toast);
            lucide.createIcons();

            setTimeout(() => {
                toast.classList.remove('translate-y-4', 'opacity-0');
            }, 10);

            setTimeout(() => {
                toast.classList.add('translate-y-4', 'opacity-0');
                setTimeout(() => toast.remove(), 300);
            }, 3000);
        }
    </script>
</body>
</html>
