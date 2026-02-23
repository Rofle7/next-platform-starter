
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ROFLE. | ESSENTIALS</title>
    
    <!-- Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500&family=Oswald:wght@400;500;700&display=swap" rel="stylesheet">

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>

    <!-- GSAP for Animations -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>

    <style>
        :root {
            --bg-color: #0a0a0a;
            --text-color: #ffffff;
            --accent-gray: #333333;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            font-family: 'Inter', sans-serif;
            overflow-x: hidden;
            cursor: default;
        }

        h1, h2, h3, .brand-font {
            font-family: 'Oswald', sans-serif;
            text-transform: uppercase;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0a0a0a; 
        }
        ::-webkit-scrollbar-thumb {
            background: #333; 
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #555; 
        }

        /* Utilities */
        .grayscale-hover {
            filter: grayscale(100%);
            transition: all 0.6s cubic-bezier(0.25, 1, 0.5, 1);
        }
        .grayscale-hover:hover {
            filter: grayscale(0%);
            transform: scale(1.02);
        }

        .border-thin {
            border: 1px solid rgba(255,255,255,0.1);
        }

        .border-thin-hover:hover {
            border-color: rgba(255,255,255,0.5);
        }

        /* Marquee Animation */
        .marquee-container {
            overflow: hidden;
            white-space: nowrap;
        }
        .marquee-content {
            display: inline-block;
            animation: marquee 20s linear infinite;
        }
        @keyframes marquee {
            0% { transform: translateX(0); }
            100% { transform: translateX(-50%); }
        }

        /* Loader */
        .loader-overlay {
            position: fixed;
            inset: 0;
            background: #000;
            z-index: 9999;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        /* Image Placeholders generated via code to ensure they exist */
        .img-placeholder {
            object-fit: cover;
            width: 100%;
            height: 100%;
        }
    </style>
</head>
<body class="antialiased selection:bg-white selection:text-black">

    <!-- Loading Screen -->
    <div id="loader" class="loader-overlay">
        <h1 class="text-4xl md:text-6xl tracking-[1em] opacity-0 animate-in fade-in duration-1000 fill-mode-forwards">ROFLE.</h1>
    </div>

    <!-- Navigation -->
    <nav class="fixed top-0 w-full z-50 mix-blend-difference px-6 py-6 flex justify-between items-center border-b border-transparent hover:border-white/10 transition-colors duration-500">
        <button class="group flex flex-col gap-1.5 cursor-pointer">
            <span class="w-6 h-[1px] bg-white group-hover:w-8 transition-all duration-300"></span>
            <span class="w-4 h-[1px] bg-white ml-auto group-hover:w-6 transition-all duration-300"></span>
            <span class="text-[10px] uppercase tracking-widest mt-1 text-right opacity-0 group-hover:opacity-100 transition-opacity duration-300">Menu</span>
        </button>

        <a href="#" class="text-2xl md:text-3xl font-bold tracking-tighter brand-font hover:opacity-70 transition-opacity">ROFLE.</a>

        <div class="flex items-center gap-8">
            <a href="#archive" class="hidden md:block text-xs uppercase tracking-widest hover:line-through decoration-1 underline-offset-4 transition-all">Archive</a>
            <button id="cart-btn" class="relative group">
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="square" stroke-linejoin="miter"><path d="M6 2L3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"></path><line x1="3" y1="6" x2="21" y2="6"></line><path d="M16 10a4 4 0 0 1-8 0"></path></svg>
                <span id="cart-count" class="absolute -top-2 -right-2 bg-white text-black text-[10px] w-4 h-4 flex items-center justify-center rounded-full opacity-0 scale-0 transition-all duration-300">0</span>
            </button>
        </div>
    </nav>

    <!-- Cart Sidebar -->
    <div id="cart-sidebar" class="fixed top-0 right-0 h-full w-full md:w-[400px] bg-neutral-900 border-l border-neutral-800 z-[60] transform translate-x-full transition-transform duration-500 ease-[cubic-bezier(0.77,0,0.175,1)]">
        <div class="p-8 h-full flex flex-col">
            <div class="flex justify-between items-center mb-8">
                <h2 class="text-xl brand-font">Cart</h2>
                <button id="close-cart" class="hover:rotate-90 transition-transform duration-300">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="square" stroke-linejoin="miter"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
                </button>
            </div>
            <div id="cart-items" class="flex-1 overflow-y-auto space-y-6">
                <!-- Items injected here -->
                <div class="text-neutral-500 text-sm italic pt-10 text-center">Your cart is empty.</div>
            </div>
            <div class="pt-6 border-t border-neutral-800">
                <div class="flex justify-between mb-4 text-sm">
                    <span class="text-neutral-400">Subtotal</span>
                    <span id="cart-total">$0.00</span>
                </div>
                <button class="w-full bg-white text-black py-4 uppercase tracking-widest text-xs font-bold hover:bg-neutral-200 transition-colors">Checkout</button>
            </div>
        </div>
    </div>

    <!-- Hero Section -->
    <header class="relative w-full h-screen overflow-hidden flex items-center justify-center">
        <!-- Background Image with Overlay -->
        <div class="absolute inset-0 z-0">
            <img src="https://images.unsplash.com/photo-1550614000-4b9519e02d48?q=80&w=2574&auto=format&fit=crop" alt="Hero Background" class="w-full h-full object-cover opacity-60 grayscale contrast-125">
            <div class="absolute inset-0 bg-gradient-to-t from-[#0a0a0a] via-transparent to-[#0a0a0a]/50"></div>
        </div>

        <div class="relative z-10 text-center mix-blend-lighten px-4">
            <p class="text-xs md:text-sm uppercase tracking-[0.5em] mb-4 text-neutral-400 reveal-text">Est. 2024 — Los Angeles</p>
            <h1 class="text-6xl md:text-9xl lg:text-[12rem] leading-none font-bold tracking-tighter text-white reveal-title">
                ROFLE.
            </h1>
            <p class="mt-6 text-sm md:text-base uppercase tracking-widest text-neutral-300 reveal-sub">Silence is the ultimate luxury.</p>
            
            <div class="mt-12 reveal-btn">
                <a href="#shop" class="inline-block border border-white/30 px-10 py-4 text-xs uppercase tracking-[0.2em] hover:bg-white hover:text-black transition-all duration-500 backdrop-blur-sm">
                    Enter Shop
                </a>
            </div>
        </div>
    </header>

    <!-- Scrolling Text Divider -->
    <div class="py-8 border-y border-white/10 bg-black marquee-container">
        <div class="marquee-content text-4xl md:text-6xl brand-font text-neutral-800 opacity-50 select-none">
            LIMITED ARCHIVE — SEASON 001 — ROFLE STUDIOS — MADE IN THE SHADOWS — LIMITED ARCHIVE — SEASON 001 — ROFLE STUDIOS — MADE IN THE SHADOWS —
        </div>
    </div>

    <!-- Main Content -->
    <main class="w-full max-w-[1920px] mx-auto px-4 md:px-12 pb-24">

        <!-- Archive / Limited Collection -->
        <section id="archive" class="py-24 md:py-32 relative">
            <div class="flex flex-col md:flex-row justify-between items-end mb-16 border-b border-white/10 pb-6">
                <div>
                    <h2 class="text-4xl md:text-6xl brand-font mb-2">Limited Archive</h2>
                    <p class="text-neutral-500 text-xs uppercase tracking-widest">Rare finds. One time only.</p>
                </div>
                <div class="hidden md:block text-right">
                    <span class="block text-5xl font-light text-neutral-800">01</span>
                    <span class="text-xs text-neutral-600 uppercase tracking-widest">Collection</span>
                </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-1 md:gap-4">
                <!-- Product 1 -->
                <div class="group relative aspect-[3/4] overflow-hidden border-thin border-neutral-800 bg-neutral-900 product-card">
                    <img src="https://images.unsplash.com/photo-1591047139829-d91aecb6caea?q=80&w=1936&auto=format&fit=crop" class="img-placeholder grayscale-hover brightness-75 group-hover:brightness-100" alt="Jacket">
                    <div class="absolute bottom-0 left-0 w-full p-6 flex justify-between items-end bg-gradient-to-t from-black/90 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500">
                        <div>
                            <h3 class="text-lg brand-font">Structure Coat</h3>
                            <p class="text-xs text-neutral-400 uppercase tracking-wide">Heavyweight Cotton</p>
                        </div>
                        <span class="text-sm font-mono">$450</span>
                    </div>
                    <button onclick="addToCart('Structure Coat', 450)" class="absolute top-4 right-4 bg-white text-black w-8 h-8 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-all duration-300 hover:scale-110">+</button>
                </div>

                <!-- Product 2 -->
                <div class="group relative aspect-[3/4] overflow-hidden border-thin border-neutral-800 bg-neutral-900 product-card">
                    <img src="https://images.unsplash.com/photo-1532453288672-3a27e9be9efd?q=80&w=1964&auto=format&fit=crop" class="img-placeholder grayscale-hover brightness-75 group-hover:brightness-100" alt="Hoodie">
                    <div class="absolute bottom-0 left-0 w-full p-6 flex justify-between items-end bg-gradient-to-t from-black/90 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500">
                        <div>
                            <h3 class="text-lg brand-font">Void Hoodie</h3>
                            <p class="text-xs text-neutral-400 uppercase tracking-wide">French Terry</p>
                        </div>
                        <span class="text-sm font-mono">$180</span>
                    </div>
                    <button onclick="addToCart('Void Hoodie', 180)" class="absolute top-4 right-4 bg-white text-black w-8 h-8 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-all duration-300 hover:scale-110">+</button>
                </div>

                <!-- Product 3 -->
                <div class="group relative aspect-[3/4] overflow-hidden border-thin border-neutral-800 bg-neutral-900 product-card">
                    <img src="https://images.unsplash.com/photo-1551488852-080175d27582?q=80&w=2070&auto=format&fit=crop" class="img-placeholder grayscale-hover brightness-75 group-hover:brightness-100" alt="Pants">
                    <div class="absolute bottom-0 left-0 w-full p-6 flex justify-between items-end bg-gradient-to-t from-black/90 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500">
                        <div>
                            <h3 class="text-lg brand-font">Cargo V2</h3>
                            <p class="text-xs text-neutral-400 uppercase tracking-wide">Ripstop Nylon</p>
                        </div>
                        <span class="text-sm font-mono">$220</span>
                    </div>
                    <button onclick="addToCart('Cargo V2', 220)" class="absolute top-4 right-4 bg-white text-black w-8 h-8 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-all duration-300 hover:scale-110">+</button>
                </div>
            </div>
        </section>

        <!-- Standard Shop Grid -->
        <section id="shop" class="py-12">
            <div class="flex justify-between items-center mb-12">
                <h2 class="text-2xl md:text-3xl brand-font">Essentials</h2>
                <a href="#" class="text-xs uppercase tracking-widest border-b border-transparent hover:border-white transition-colors pb-1">View All</a>
            </div>

            <div class="grid grid-cols-2 md:grid-cols-4 gap-x-2 gap-y-12">
                <!-- Item 1 -->
                <div class="group cursor-pointer">
                    <div class="aspect-[3/4] overflow-hidden bg-neutral-900 mb-4 relative">
                        <img src="https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?q=80&w=1780&auto=format&fit=crop" class="img-placeholder grayscale-hover" alt="Tee">
                    </div>
                    <div class="flex justify-between items-start">
                        <div>
                            <h3 class="text-sm font-medium">Box Tee</h3>
                            <p class="text-xs text-neutral-500 mt-1">Charcoal</p>
                        </div>
                        <span class="text-xs font-mono">$65</span>
                    </div>
                    <button onclick="addToCart('Box Tee', 65)" class="w-full mt-3 py-2 border border-neutral-800 text-[10px] uppercase tracking-widest hover:bg-white hover:text-black transition-colors">Add to Cart</button>
                </div>

                <!-- Item 2 -->
                <div class="group cursor-pointer">
                    <div class="aspect-[3/4] overflow-hidden bg-neutral-900 mb-4 relative">
                        <img src="https://images.unsplash.com/photo-1617137968427-85924c809a10?q=80&w=1887&auto=format&fit=crop" class="img-placeholder grayscale-hover" alt="Cap">
                    </div>
                    <div class="flex justify-between items-start">
                        <div>
                            <h3 class="text-sm font-medium">Dad Hat</h3>
                            <p class="text-xs text-neutral-500 mt-1">Black</p>
                        </div>
                        <span class="text-xs font-mono">$45</span>
                    </div>
                    <button onclick="addToCart('Dad Hat', 45)" class="w-full mt-3 py-2 border border-neutral-800 text-[10px] uppercase tracking-widest hover:bg-white hover:text-black transition-colors">Add to Cart</button>
                </div>

                <!-- Item 3 -->
                <div class="group cursor-pointer">
                    <div class="aspect-[3/4] overflow-hidden bg-neutral-900 mb-4 relative">
                        <img src="https://images.unsplash.com/photo-1576995853123-5a297da4030e?q=80&w=1887&auto=format&fit=crop" class="img-placeholder grayscale-hover" alt="Sweatpants">
                    </div>
                    <div class="flex justify-between items-start">
                        <div>
                            <h3 class="text-sm font-medium">Relaxed Pant</h3>
                            <p class="text-xs text-neutral-500 mt-1">Oatmeal</p>
                        </div>
                        <span class="text-xs font-mono">$140</span>
                    </div>
                    <button onclick="addToCart('Relaxed Pant', 140)" class="w-full mt-3 py-2 border border-neutral-800 text-[10px] uppercase tracking-widest hover:bg-white hover:text-black transition-colors">Add to Cart</button>
                </div>

                <!-- Item 4 -->
                <div class="group cursor-pointer">
                    <div class="aspect-[3/4] overflow-hidden bg-neutral-900 mb-4 relative">
                        <img src="https://images.unsplash.com/photo-1596755094514-f87e34085b2c?q=80&w=1888&auto=format&fit=crop" class="img-placeholder grayscale-hover" alt="Shirt">
                    </div>
                    <div class="flex justify-between items-start">
                        <div>
                            <h3 class="text-sm font-medium">Oversized Shirt</h3>
                            <p class="text-xs text-neutral-500 mt-1">White</p>
                        </div>
                        <span class="text-xs font-mono">$110</span>
                    </div>
                    <button onclick="addToCart('Oversized Shirt', 110)" class="w-full mt-3 py-2 border border-neutral-800 text-[10px] uppercase tracking-widest hover:bg-white hover:text-black transition-colors">Add to Cart</button>
                </div>
            </div>
        </section>

        <!-- Cinematic Banner -->
        <section class="w-full h-[60vh] mt-24 relative overflow-hidden flex items-center justify-center border-thin">
            <img src="https://images.unsplash.com/photo-1483985988355-763728e1935b?q=80&w=2670&auto=format&fit=crop" class="absolute inset-0 w-full h-full object-cover grayscale opacity-40" alt="Cinematic">
            <div class="relative z-10 text-center">
                <h2 class="text-5xl md:text-8xl brand-font tracking-tighter mb-4">SEASON 002</h2>
                <p class="text-xs uppercase tracking-[0.3em] text-neutral-400">Coming Soon</p>
            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="border-t border-white/10 bg-black pt-20 pb-10 px-6 md:px-12">
        <div class="grid grid-cols-1 md:grid-cols-4 gap-12 mb-20">
            <div class="col-span-1 md:col-span-2">
                <h2 class="text-4xl brand-font mb-6">ROFLE.</h2>
                <p class="text-neutral-500 text-sm max-w-md leading-relaxed">
                    Redefining modern silhouettes through minimalist design and premium materials. 
                    Born in the shadows, worn in the light.
                </p>
            </div>
            <div>
                <h4 class="text-xs uppercase tracking-widest mb-6 text-neutral-400">Support</h4>
                <ul class="space-y-4 text-sm">
                    <li><a href="#" class="hover:text-neutral-400 transition-colors">Shipping</a></li>
                    <li><a href="#" class="hover:text-neutral-400 transition-colors">Returns</a></li>
                    <li><a href="#" class="hover:text-neutral-400 transition-colors">Size Guide</a></li>
                    <li><a href="#" class="hover:text-neutral-400 transition-colors">Contact</a></li>
                </ul>
            </div>
            <div>
                <h4 class="text-xs uppercase tracking-widest mb-6 text-neutral-400">Social</h4>
                <ul class="space-y-4 text-sm">
                    <li><a href="#" class="hover:text-neutral-400 transition-colors">Instagram</a></li>
                    <li><a href="#" class="hover:text-neutral-400 transition-colors">Twitter</a></li>
                    <li><a href="#" class="hover:text-neutral-400 transition-colors">TikTok</a></li>
                </ul>
            </div>
        </div>
        <div class="flex flex-col md:flex-row justify-between items-center text-[10px] text-neutral-600 uppercase tracking-widest bo