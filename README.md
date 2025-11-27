<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Indiwood. | Explore Cinema & Culture</title>
    <!-- Load Tailwind CSS --><script src="https://cdn.tailwindcss.com"></script>
    <!-- Load Inter Font --><link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap">
    <style>
        /* Custom styles for the Moctale/Indiwood aesthetic */
        body {
            font-family: 'Inter', sans-serif;
            scroll-behavior: smooth;
        }
        .text-indi-accent {
            color: #f59e0b; /* Amber/Gold tone */
        }
        .bg-indi-accent {
            background-color: #f59e0b;
        }
        .hover-lift:hover {
            transform: translateY(-4px);
            box-shadow: 0 10px 15px rgba(0, 0, 0, 0.5); /* Increased shadow depth for dark theme */
        }
        /* Style for the horizontal scroll container */
        .horizontal-scroll-container::-webkit-scrollbar {
            display: none; /* Hide scrollbar for Chrome, Safari and Opera */
        }
        .horizontal-scroll-container {
            -ms-overflow-style: none;  /* IE and Edge */
            scrollbar-width: none;  /* Firefox */
        }
        /* Custom card styling to mimic poster proportions */
        .poster-card {
            width: 150px; /* Base width */
            height: auto;
            display: inline-block;
            margin-right: 1.5rem; /* Space between cards */
        }
        .large-poster-card {
            width: 200px; /* Base width for TOTT section */
            height: auto;
            display: inline-block;
            margin-right: 1.5rem; /* Space between cards */
        }
        /* Responsive widths for smaller posters */
        @media (min-width: 640px) { .poster-card { width: 180px; } }
        @media (min-width: 1024px) { .poster-card { width: 150px; } }

        /* The overall container layout now uses 1 column (no sidebar) */
        .main-layout {
            grid-template-columns: 1fr; 
        }
        .category-title:hover {
            color: #d1d5db; /* Lighter gray on hover */
            cursor: pointer;
        }
        /* Custom transition for dropdowns */
        .search-dropdown {
            transition: all 0.3s ease-in-out;
            transform-origin: top;
        }
        /* Detail Page specific height adjustments */
        #detail-view .detail-content-wrapper {
            /* Ensures content aligns nicely below the header */
            padding-top: 8rem; 
            min-height: calc(100vh - 4rem); /* Full height minus sticky header height */
        }
        /* Fixed positioning for the floating review section in the detail page */
        #review-score-float {
            z-index: 10;
        }
    </style>
</head>
<body class="bg-slate-950 text-gray-100 min-h-screen">

    <!-- Header / Navigation Bar (Top Bar) --><header class="sticky top-0 z-50 bg-slate-900 shadow-lg border-b border-slate-800">
        <div class="max-w-[85rem] mx-auto px-4 sm:px-6 lg:px-8 py-3 flex justify-between items-center h-16">
            
            <!-- Left Side: Back Button + Logo -->
            <div class="flex items-center space-x-2">
                
                <!-- Back Button (Toggle visibility in JS) -->
                <button id="back-btn" onclick="goBack();" class="hidden p-2 rounded-full hover:bg-slate-800 transition duration-200 text-gray-400" aria-label="Go Back" title="Go Back">
                    <!-- Heroicon: Arrow Left -->
                    <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M10.5 19.5L3 12m0 0l7.5-7.5M3 12h18" /></svg>
                </button>
                
                <!-- Logo/Brand --><a href="#" class="flex items-center space-x-2" onclick="goHome(); return false;">
                    <!-- Using a simple icon/symbol placeholder for the 'I' logo look --><div class="bg-indi-accent p-1.5 rounded-md text-gray-900 font-extrabold text-lg leading-none">I</div>
                    <div class="flex flex-col">
                        <span class="text-2xl font-extrabold tracking-tight">
                            <span class="text-white">Indiwood</span>
                        </span>
                        <span class="text-xs text-gray-400 -mt-1">Cinema & Culture Hub</span>
                    </div>
                </a>
            </div>
            
            <!-- Spacer (Occupies center space) -->
            <div class="flex-grow hidden md:block"></div>

            <!-- Right Icons & Profile --><div class="flex items-center space-x-4">
                
                <!-- Watched List Icon REMOVED -->
                
                <!-- 1. Search Icon (Toggle Button) --><button id="search-toggle-btn" class="p-2 rounded-full hover:bg-slate-800 transition duration-200" aria-label="Search" title="Search">
                    <!-- Heroicon: Magnifying Glass (Large) --><svg class="w-6 h-6 text-gray-400" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" /></svg>
                </button>

                <!-- 2. Bell Icon (Notifications) --><button id="notifications-toggle-btn" class="p-2 rounded-full hover:bg-slate-800 transition duration-200" aria-label="Notifications" title="Notifications">
                    <!-- Heroicon: Bell --><svg class="w-6 h-6 text-gray-400" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M14.857 17.082a23.848 23.848 0 005.454-1.31A8.967 8.967 0 0118 9.75V9A6 6 0 006 9v.75a8.967 8.967 0 01-2.312 6.022c1.733.64 3.56 1.04 5.455 1.31m5.714 0a24.255 24.255 0 01-5.714 0m5.714 0a3 3 0 11-5.714 0" /></svg>
                </button>
                
                <!-- 3. User Circle Icon (Profile) --><button class="p-2 rounded-full hover:bg-slate-800 transition duration-200" aria-label="User Profile" title="Profile">
                    <!-- Heroicon: User Circle --><svg class="w-8 h-8 text-indi-accent" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M17.982 18.725A7.488 7.488 0 0012 15.75a7.488 7.488 0 00-5.982 2.975m11.963 0a9 9 0 10-11.963 0m11.963 0A8.966 8.966 0 0112 21a8.966 8.966 0 01-5.982-2.275M15 9.75a3 3 0 11-6 0 3 3 0 016 0z" /></svg>
                </button>
                
            </div>
        </div>
    </header>

    <!-- Collapsible Search Dropdown -->
    <div id="search-dropdown" class="search-dropdown hidden absolute top-16 right-0 mr-4 md:mr-6 bg-slate-900 shadow-xl rounded-lg w-64 border border-slate-700 z-40 p-3">
        <div class="relative w-full">
            <input 
                type="text" 
                placeholder="Search titles..." 
                class="w-full pl-10 pr-4 py-1.5 bg-slate-700 border border-slate-600 rounded-full text-sm text-gray-200 focus:outline-none focus:ring-2 focus:ring-indi-accent focus:border-indi-accent transition duration-200"
                aria-label="Search content on Indiwood"
            >
            <svg class="absolute left-3 top-1/2 transform -translate-y-1/2 w-4 h-4 text-indi-accent" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" /></svg>
        </div>
    </div>
    
    <!-- Collapsible Notifications Dropdown -->
    <div id="notifications-dropdown" class="search-dropdown hidden absolute top-16 right-0 mr-4 md:mr-6 bg-slate-800 shadow-2xl rounded-lg w-72 md:w-80 border border-slate-700 z-40">
        <div class="p-4">
            <h3 class="text-lg font-bold border-b border-slate-700 pb-2 mb-3">Notifications</h3>
            <ul class="space-y-3 text-sm">
                <li class="flex items-start space-x-2 p-1.5 hover:bg-slate-700 rounded transition duration-150 cursor-pointer">
                    <span class="text-indi-accent flex-shrink-0 mt-1">&#9679;</span>
                    <p>New Episode Alert: <span class="font-semibold">IT: Welcome to Delhi</span> just released!</p>
                </li>
                <li class="flex items-start space-x-2 p-1.5 hover:bg-slate-700 rounded transition duration-150 cursor-pointer">
                    <span class="text-indi-accent flex-shrink-0 mt-1">&#9679;</span>
                    <p>Your review on <span class="font-semibold">Sisu</span> was featured in 'Top 10'.</p>
                </li>
                <li class="flex items-start space-x-2 p-1.5 hover:bg-slate-700 rounded transition duration-150 cursor-pointer">
                    <span class="text-gray-500 flex-shrink-0 mt-1">&#9679;</span>
                    <p class="text-gray-400">Monthly content summary is ready.</p>
                </li>
                <li class="flex justify-center pt-2">
                    <a href="#" class="text-xs text-indi-accent hover:text-amber-500 transition duration-150 font-semibold">See All Notifications</a>
                </li>
            </ul>
        </div>
    </div>

    <!-- 1. HOME VIEW (Initial View) -->
    <div id="home-view" class="max-w-[85rem] mx-auto px-4 sm:px-6 lg:px-8 py-8 md:py-12">
        <div class="grid main-layout lg:grid-cols-1 gap-8">
            
            <!-- Left & Center Content (Main Stream) --><main class="lg:pr-4">
                
                <!-- Hero Section (Featured Movie) -->
                <section id="hero-jawan" class="relative bg-slate-900 rounded-xl overflow-hidden shadow-2xl mb-12 cursor-pointer group" data-movie="120-bahadur">
                    <!-- Background Image Placeholder (High Contrast, Cinematic) -->
                    <div class="relative w-full h-[300px] md:h-[450px]">
                        <!-- UPDATED: Removed text from background image placeholder -->
                        <img src="https://placehold.co/1400x700/1f2937/1f2937" alt="120 Bahadur Hero Background" class="w-full h-full object-cover group-hover:scale-[1.02] transition-transform duration-500 opacity-60">
                        <div class="absolute inset-0 bg-gradient-to-t from-slate-950/90 via-slate-950/50 to-transparent"></div>
                    </div>

                    <!-- Content Overlay -->
                    <div class="absolute bottom-0 left-0 p-6 md:p-12 w-full max-w-2xl text-white">
                        <p class="text-sm font-semibold text-indi-accent mb-2">HOTSTAR EXCLUSIVE | ACTION / WAR</p>
                        <h1 class="text-4xl sm:text-5xl md:text-7xl font-extrabold leading-tight mb-4">120 Bahadur</h1>
                        <p class="text-gray-300 mb-6 line-clamp-3">Major Shaitan Singh Bhati and his 120 soldiers stand firm during the 1962 Sino-Indian War, facing an overwhelming force of nearly 3,000 enemy troops. Courage over surrender.</p>
                        <div class="flex space-x-4">
                            <!-- Button to trigger movie detail view/playback (redirect) -->
                            <button onclick="showPage('detail', '120-bahadur')" class="flex items-center space-x-2 bg-indi-accent hover:bg-amber-600 text-slate-900 font-bold py-3 px-6 rounded-full transition duration-300 shadow-xl transform group-hover:scale-[1.05]">
                                <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M5.25 5.653c0-.856.917-1.398 1.667-.986l11.54 6.348a1.125 1.125 0 010 1.972l-11.54 6.347a1.125 1.125 0 01-1.667-.985V5.653z" /></svg>
                                <span>Find Movie on YouTube</span>
                            </button>
                        </div>
                    </div>
                </section>
                
                <!-- Section 1: Talk Of The Town (Horizontal Scroll) --><section class="mb-12">
                    <h2 class="text-2xl font-bold mb-6 border-l-4 border-indi-accent pl-3 category-title transition-colors duration-200">Talk Of The Town</h2>
                    
                    <!-- Horizontal Scroll Container --><div class="horizontal-scroll-container flex overflow-x-auto pb-4">
                        
                        <!-- Repeatable Large Poster Card (6 examples) -->
                        <div class="large-poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="family-man">
                            <div class="relative">
                                <!-- AI Placeholder: Red/White Spy Thriller -->
                                <img src="https://placehold.co/400x600/b91c1c/fef2f2?text=Family+Agent+S3" alt="The Family Man Poster" class="w-full h-80 object-cover">
                                <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 to-transparent"></div>
                                <div class="absolute bottom-0 left-0 p-3 w-full">
                                    <h3 class="text-lg font-bold truncate">The Family Man</h3>
                                    <p class="text-xs text-gray-400">Prime Video Season <span class="bg-blue-600 text-white px-1 ml-1 rounded">New</span></p>
                                </div>
                            </div>
                        </div>

                        <div class="large-poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="120-bahadur">
                            <div class="relative">
                                <!-- AI Placeholder: Dark Gray/White War Epic -->
                                <img src="https://placehold.co/400x600/374151/d1d5db?text=120+EPIC+B" alt="120 Bahadur Poster" class="w-full h-80 object-cover">
                                <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 to-transparent"></div>
                                <div class="absolute bottom-0 left-0 p-3 w-full">
                                    <h3 class="text-lg font-bold truncate">120 Bahadur</h3>
                                    <p class="text-xs text-gray-400">Hotstar Exclusive</p>
                                </div>
                            </div>
                        </div>
                        
                        <div class="large-poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="mastiii-4">
                            <div class="relative">
                                <!-- AI Placeholder: Bright Green/White Comedy -->
                                <img src="https://placehold.co/400x600/65a30d/f0fdf4?text=MASTIII+4+FUN" alt="Mastiii 4 Poster" class="w-full h-80 object-cover">
                                <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 to-transparent"></div>
                                <div class="absolute bottom-0 left-0 p-3 w-full">
                                    <h3 class="text-lg font-bold truncate">Mastiii 4</h3>
                                    <p class="text-xs text-gray-400">Netflix Comedy</p>
                                </div>
                            </div>
                        </div>

                        <div class="large-poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="it-delhi">
                            <div class="relative">
                                <!-- AI Placeholder: Blue/Light Blue Tech Thriller -->
                                <img src="https://placehold.co/400x600/1e40af/bfdbfe?text=IT+DELHI+HACK" alt="IT Delhi Poster" class="w-full h-80 object-cover">
                                <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 to-transparent"></div>
                                <div class="absolute bottom-0 left-0 p-3 w-full">
                                    <h3 class="text-lg font-bold truncate">IT: Welcome to Delhi</h3>
                                    <p class="text-xs text-gray-400">New Episode <span class="bg-red-600 text-white px-1 ml-1 rounded">New</span></p>
                                </div>
                            </div>
                        </div>

                        <div class="large-poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="homebound">
                            <div class="relative">
                                <!-- AI Placeholder: Dark Green/Light Green Family Drama -->
                                <img src="https://placehold.co/400x600/15803d/dcfce7?text=HOMEBOUND+ROAD" alt="Homebound Poster" class="w-full h-80 object-cover">
                                <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 to-transparent"></div>
                                <div class="absolute bottom-0 left-0 p-3 w-full">
                                    <h3 class="text-lg font-bold truncate">Homebound</h3>
                                    <p class="text-xs text-gray-400">SonyLIV Release</p>
                                </div>
                            </div>
                        </div>
                        
                        <div class="large-poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="op-gold">
                            <div class="relative">
                                <!-- AI Placeholder: Dark Brown/White Military Suspense -->
                                <img src="https://placehold.co/400x600/44403c/f5f5f4?text=OP+GOLD+SUS" alt="Operation Gold Poster" class="w-full h-80 object-cover">
                                <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 to-transparent"></div>
                                <div class="absolute bottom-0 left-0 p-3 w-full">
                                    <h3 class="text-lg font-bold truncate">Operation Gold</h3>
                                    <p class="text-xs text-gray-400">ZEE5 Series</p>
                                </div>
                            </div>
                        </div>
                        
                        <!-- End of Horizontal Cards --></div>
                </section>
                
                <!-- Section 2: Netflix Originals --><section class="mt-8 mb-12">
                    <h2 class="text-2xl font-bold mb-6 border-l-4 border-red-600 pl-3 text-red-400 category-title transition-colors duration-200">Netflix Originals</h2>
                    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 gap-6 justify-items-center sm:justify-items-start">
                        
                        <!-- Netflix Card 1 -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="sisu-revenge">
                            <div class="relative">
                                <!-- AI Placeholder: Dark Red/Light Red Gravelly Action -->
                                <img src="https://placehold.co/300x450/450a0a/fca5a5?text=SISU+GRIT" alt="Sisu Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Sisu: Road to Revenge</h3>
                                    <p class="text-xs text-gray-400">Action Movie</p>
                                </div>
                            </div>
                        </div>

                        <!-- Netflix Card 2 -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="jujutsu-kaisen">
                            <div class="relative">
                                <!-- AI Placeholder: Purple/Light Purple Anime Epic -->
                                <img src="https://placehold.co/300x450/7c3aed/f3e8ff?text=JJK+EPIC" alt="Jujutsu Ex Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Jujutsu Kaisen: Ex...</h3>
                                    <p class="text-xs text-gray-400">New Anime Season <span class="bg-red-600 text-white px-1 ml-1 rounded">New</span></p>
                                </div>
                            </div>
                        </div>
                        
                        <!-- Netflix Card 3 -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="mystic-falls">
                            <div class="relative">
                                <!-- AI Placeholder: Dark Green/Light Green Mystery/Fantasy -->
                                <img src="https://placehold.co/300x450/065f46/d1fae5?text=MYSTIC+FALLS" alt="Mystic Falls Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Mystic Falls</h3>
                                    <p class="text-xs text-gray-400">Fantasy Series</p>
                                </div>
                            </div>
                        </div>

                        <!-- Netflix Card 4 -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="the-heist">
                            <div class="relative">
                                <!-- AI Placeholder: Dark Blue/Gray Crime Thriller -->
                                <img src="https://placehold.co/300x450/1e293b/d1d5db?text=THE+HEIST" alt="The Heist Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">The Heist: Finale</h3>
                                    <p class="text-xs text-gray-400">Crime Thriller</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </section>
                
                <!-- Section 3: Prime Video Hits --><section class="mt-8 mb-12">
                    <h2 class="text-2xl font-bold mb-6 border-l-4 border-cyan-600 pl-3 text-cyan-400 category-title transition-colors duration-200">Prime Video Hits</h2>
                    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 gap-6 justify-items-center sm:justify-items-start">
                        
                        <!-- Prime Card 1 -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="tu-meri-main-tera">
                            <div class="relative">
                                <!-- AI Placeholder: Pink/Light Pink Romantic Drama -->
                                <img src="https://placehold.co/300x450/f0abf0/fce7f3?text=ROMANCE+DRAMA" alt="Meri Jaan Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Tu Meri Main Tera</h3>
                                    <p class="text-xs text-gray-400">Romance Drama</p>
                                </div>
                            </div>
                        </div>

                        <!-- Prime Card 2 -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="train-dreams">
                            <div class="relative">
                                <!-- AI Placeholder: Dark Blue/Light Blue Art House -->
                                <img src="https://placehold.co/300x450/0c4a6e/e0f2f1?text=TRAIN+DREAMS" alt="Train Dreams Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Train Dreams</h3>
                                    <p class="text-xs text-gray-400">New Movie <span class="bg-blue-600 text-white px-1 ml-1 rounded">New</span></p>
                                </div>
                            </div>
                        </div>
                        
                        <!-- Prime Card 3 -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="de-de-pyaar-2">
                            <div class="relative">
                                <!-- AI Placeholder: Orange/White Family Comedy -->
                                <img src="https://placehold.co/300x450/f97316/ffedd5?text=FAMILY+COMEDY" alt="De De Pyaar Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">De De Pyaar 2</h3>
                                    <p class="text-xs text-gray-400">Family Comedy</p>
                                </div>
                            </div>
                        </div>

                        <!-- Prime Card 4 -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="the-liar">
                            <div class="relative">
                                <!-- AI Placeholder: Dark Gray/Light Gray Psychological Thriller -->
                                <img src="https://placehold.co/300x450/374151/d1d5db?text=PSYCHO+LIAR" alt="The Liar Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">The Liar</h3>
                                    <p class="text-xs text-gray-400">Psychological Thriller</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </section>
                
                <!-- Section 4: Indie Discoveries (More) --><section class="mt-8 mb-12">
                    <h2 class="text-2xl font-bold mb-6 border-l-4 border-indi-accent pl-3 text-indi-accent category-title transition-colors duration-200">Indie Discoveries</h2>
                    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 gap-6 justify-items-center sm:justify-items-start">
                        
                        <!-- Indie Card 1 -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="old-is-gold">
                            <div class="relative">
                                <!-- AI Placeholder: Gray/White Classic Film -->
                                <img src="https://placehold.co/300x450/6b7280/e5e7eb?text=OLD+GOLD+RETRO" alt="Old Gold Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Old is Gold</h3>
                                    <p class="text-xs text-gray-400">Classics</p>
                                </div>
                            </div>
                        </div>

                        <!-- Indie Card 2 -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="raja-rani-3">
                            <div class="relative">
                                <!-- AI Placeholder: Purple/Light Purple Bright Drama -->
                                <img src="https://placehold.co/300x450/d946ef/f3e8ff?text=RAJA+RANI+3" alt="Raja Rani 3 Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Raja Rani 3</h3>
                                    <p class="text-xs text-gray-400">New Movie <span class="bg-indi-accent text-slate-950 px-1 ml-1 rounded">New</span></p>
                                </div>
                            </div>
                        </div>

                        <!-- Indie Card 3 -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="city-lights">
                            <div class="relative">
                                <!-- AI Placeholder: Dark Blue/Amber Neo-Noir -->
                                <img src="https://placehold.co/300x450/1e293b/f59e0b?text=CITY+LIGHTS+NOIR" alt="City Lights Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">City Lights</div>
                                    <p class="text-xs text-gray-400">Classic</p>
                                </div>
                            </div>
                        </div>
                        
                        <!-- Indie Card 4 -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="action-man-7">
                            <div class="relative">
                                <!-- AI Placeholder: Red/White Heroic Action -->
                                <img src="https://placehold.co/300x450/dc2626/fef2f2?text=ACTION+MAN+7" alt="Action Man Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Action Man 7</h3>
                                    <p class="text-xs text-gray-400">New Movie</p>
                                </div>
                            </div>
                        </div>
                        <!-- End of Small Cards --></div>
                </section>
                
            </main>
            
        </div>
    </div>

    <!-- 2. DETAIL VIEW (Hidden by default) -->
    <div id="detail-view" class="hidden">
        <!-- Detail page content will be injected here by JavaScript -->
    </div>

    <!-- WATCHED VIEW REMOVED -->
    <!-- FIREBASE CONFIGURATION MODAL REMOVED -->


    <!-- JavaScript for Interactivity and Routing --><script>
        
        // --- Data Store for all movies (simplified) ---
        const MOVIE_DATA = {
            'family-man': {
                title: 'The Family Man', year: 2019, duration: '2 Seasons', director: 'Raj & DK', country: 'India', language: 'Hindi', ageRating: '16+',
                posterUrl: 'https://placehold.co/400x600/b91c1c/fef2f2?text=Family+Agent+S3',
                backgroundUrl: 'https://placehold.co/1400x700/7f1d1d/fef2f2?text=The+Family+Man+Action+Background',
                overview: "A highly secretive task force balances extraordinary professional demands with the complexities of ordinary family life. This high-stakes thriller is a perfect blend of intense action and poignant drama.",
                genres: ['Action', 'Thriller', 'Spy', 'Family Drama'],
                cast: [
                    { name: 'Manoj Bajpayee', role: 'Srikant Tiwari', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=MB' },
                    { name: 'Priyamani', role: 'Suchi Tiwari', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=P' },
                    { name: 'Sharib Hashmi', role: 'JK Talpade', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=SH' },
                ],
                vibe: [
                    { genre: 'Action', percentage: 40, color: 'red-600' },
                    { genre: 'Drama', percentage: 35, color: 'blue-600' },
                    { genre: 'Suspense', percentage: 25, color: 'yellow-500' },
                ],
                reviewScore: { score: 78, totalVotes: 512, breakdown: [
                    { label: 'Skip', percentage: 5, color: 'red-600' },
                    { label: 'Timepass', percentage: 15, color: 'yellow-500' },
                    { label: 'Go for it', percentage: 60, color: 'green-500' },
                    { label: 'Perfection', percentage: 20, color: 'purple-600' },
                ]},
                familyFriendly: false,
            },
            '120-bahadur': {
                title: '120 Bahadur', year: 2025, duration: '2h 17m', director: 'Razneesh Ghai', country: 'India', language: 'Hindi', ageRating: '13+',
                posterUrl: 'https://placehold.co/400x600/374151/d1d5db?text=120+EPIC+B',
                backgroundUrl: 'https://placehold.co/1400x700/1f2937/1f2937', 
                overview: "120 Bahadur follows Major Shaitan Singh Bhati, and his 120 soldiers of Charlie Company as they stand firm during the 1962 Sino-Indian War. Posted on the freezing Himalayan heights and cut off from reinforcements, they face an overwhelming force of nearly 3,000 enemy troops. Despite being outnumbered and outgunned, the men choose courage over surrender.",
                genres: ['Biopic', 'War', 'Based On True Story', 'Action', 'Patriotic', 'Historical'],
                cast: [
                    { name: 'Farhan Akhtar', role: 'Major', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=FA' },
                    { name: 'Raashi Khanna', role: 'Journalist', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=RK' },
                    { name: 'Sparsh Walia', role: 'Soldier 1', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=SW' },
                    { name: 'Ankit Siwach', role: 'Soldier 2', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=AS' },
                    { name: 'Vivan Bhatena', role: 'Villain', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=VB' }
                ],
                vibe: [
                    { genre: 'Drama', percentage: 35, color: 'red-600' },
                    { genre: 'Action', percentage: 30, color: 'blue-600' },
                    { genre: 'Thriller', percentage: 25, color: 'yellow-500' },
                    { genre: 'Romance', percentage: 10, color: 'pink-600' },
                ],
                reviewScore: { score: 73, totalVotes: 358, breakdown: [
                    { label: 'Skip', percentage: 1, color: 'red-600' },
                    { label: 'Timepass', percentage: 14, color: 'yellow-500' },
                    { label: 'Go for it', percentage: 73, color: 'green-500' },
                    { label: 'Perfection', percentage: 12, color: 'purple-600' },
                ]},
                familyFriendly: true,
            },
            'mastiii-4': { 
                title: 'Mastiii 4', year: 2024, duration: '1h 55m', director: 'Indra Kumar', country: 'India', language: 'Hindi', ageRating: 'U/A 16+', posterUrl: 'https://placehold.co/400x600/65a30d/f0fdf4?text=MASTIII+4+FUN', backgroundUrl: 'https://placehold.co/1400x700/4d7c0f/f0fdf4?text=MASTIII+4+COMEDY+BACKGROUND', overview: "A hilarious sequel that follows three friends as they navigate chaotic relationships and absurd situations. Prepare for non-stop laughter and over-the-top antics.", genres: ['Comedy', 'Adult Humor', 'Bollywood'], cast: [], 
                vibe: [{ genre: 'Comedy', percentage: 60, color: 'green-500' }, { genre: 'Romance', percentage: 30, color: 'pink-600' }, { genre: 'Drama', percentage: 10, color: 'red-600' }], 
                familyFriendly: false, 
                reviewScore: { score: 65, totalVotes: 789, breakdown: [{ label: 'Skip', percentage: 10, color: 'red-600' }, { label: 'Timepass', percentage: 40, color: 'yellow-500' }, { label: 'Go for it', percentage: 40, color: 'green-500' }, { label: 'Perfection', percentage: 10, color: 'purple-600' }],}, 
            },
            'it-delhi': { 
                title: 'IT: Welcome to Delhi', year: 2024, duration: 'New Episode', director: 'Various', country: 'India', language: 'English/Hindi', ageRating: '18+', posterUrl: 'https://placehold.co/400x600/1e40af/bfdbfe?text=IT+DELHI+HACK', backgroundUrl: 'https://placehold.co/1400x700/1e3a8a/bfdbfe?text=IT+DELHI+NEO+NOIR+CITY', overview: "A gripping series delving into the dark underbelly of technology, cybercrime, and bureaucratic corruption in India's capital.", genres: ['Thriller', 'Crime', 'Tech', 'Suspense'], cast: [], 
                vibe: [{ genre: 'Thriller', percentage: 50, color: 'yellow-500' }, { genre: 'Drama', percentage: 40, color: 'red-600' }, { genre: 'Action', percentage: 10, color: 'blue-600' }], 
                familyFriendly: false, 
                reviewScore: { score: 85, totalVotes: 945, breakdown: [{ label: 'Skip', percentage: 2, color: 'red-600' }, { label: 'Timepass', percentage: 5, color: 'yellow-500' }, { label: 'Go for it', percentage: 68, color: 'green-500' }, { label: 'Perfection', percentage: 25, color: 'purple-600' }],}, 
            },
            'homebound': { 
                title: 'Homebound', year: 2023, duration: '1h 38m', director: 'Anon', country: 'India', language: 'Hindi', ageRating: 'U', posterUrl: 'https://placehold.co/400x600/15803d/dcfce7?text=HOMEBOUND+ROAD', backgroundUrl: 'https://placehold.co/1400x700/065f46/dcfce7?text=HOMEBOUND+LANDSCAPE', overview: "A heartwarming journey of a young man forced to return to his roots, finding unexpected connections and life lessons along the way.", genres: ['Drama', 'Family', 'Travel'], cast: [], 
                vibe: [{ genre: 'Drama', percentage: 55, color: 'red-600' }, { genre: 'Feel Good', percentage: 45, color: 'green-500' }], 
                familyFriendly: true, 
                reviewScore: { score: 70, totalVotes: 420, breakdown: [{ label: 'Skip', percentage: 5, color: 'red-600' }, { label: 'Timepass', percentage: 25, color: 'yellow-500' }, { label: 'Go for it', percentage: 50, color: 'green-500' }, { label: 'Perfection', percentage: 20, color: 'purple-600' }],}, 
            },
            'op-gold': { 
                title: 'Operation Gold', year: 2024, duration: '1 Season', director: 'Siddharth', country: 'India', language: 'Hindi', ageRating: '13+', posterUrl: 'https://placehold.co/400x600/44403c/f5f5f4?text=OP+GOLD+SUS', backgroundUrl: 'https://placehold.co/1400x700/292524/f5f5f4?text=OP+GOLD+MILITARY+BASE', overview: "An elite military unit embarks on a clandestine mission to recover smuggled gold with national security implications.", genres: ['Military', 'Action', 'Thriller'], cast: [], 
                vibe: [{ genre: 'Action', percentage: 50, color: 'blue-600' }, { genre: 'Thriller', percentage: 40, color: 'yellow-500' }, { genre: 'Drama', percentage: 10, color: 'red-600' }], 
                reviewScore: { score: 80, totalVotes: 610, breakdown: [{ label: 'Skip', percentage: 3, color: 'red-600' }, { label: 'Timepass', percentage: 12, color: 'yellow-500' }, { label: 'Go for it', percentage: 55, color: 'green-500' }, { label: 'Perfection', percentage: 30, color: 'purple-600' }],}, 
            },
            'sisu-revenge': { 
                title: 'Sisu: Road to Revenge', year: 2022, duration: '1h 31m', director: 'Jalmari', country: 'Finland', language: 'English', ageRating: '18+', posterUrl: 'https://placehold.co/300x450/450a0a/fca5a5?text=SISU+GRIT', backgroundUrl: 'https://placehold.co/1400x700/3f0000/fca5a5?text=SISU+ACTION+DESERT', overview: "A retired commando finds himself alone in the wilderness fighting for his life against impossible odds to protect a fortune.", genres: ['Action', 'Violent', 'War'], cast: [], 
                vibe: [{ genre: 'Action', percentage: 70, color: 'blue-600' }, { genre: 'Thriller', percentage: 30, color: 'yellow-500' }], 
                familyFriendly: false, 
                reviewScore: { score: 90, totalVotes: 1200, breakdown: [{ label: 'Skip', percentage: 1, color: 'red-600' }, { label: 'Timepass', percentage: 4, color: 'yellow-500' }, { label: 'Go for it', percentage: 45, color: 'green-500' }, { label: 'Perfection', percentage: 50, color: 'purple-600' }],}, 
            },
            'jujutsu-kaisen': { 
                title: 'Jujutsu Kaisen: Ex...', year: 2020, duration: '2 Seasons', director: 'Shota', country: 'Japan', language: 'Japanese', ageRating: '16+', posterUrl: 'https://placehold.co/300x450/7c3aed/f3e8ff?text=JJK+EPIC', backgroundUrl: 'https://placehold.co/1400x700/6d28d9/f3e8ff?text=JUJUTSU+FIGHT+SCENE', overview: "A dark fantasy where high school students fight powerful curses using their newfound supernatural abilities.", genres: ['Anime', 'Action', 'Fantasy'], cast: [], 
                vibe: [{ genre: 'Action', percentage: 50, color: 'blue-600' }, { genre: 'Fantasy', percentage: 50, color: 'purple-600' }], 
                familyFriendly: false, 
                reviewScore: { score: 95, totalVotes: 2500, breakdown: [{ label: 'Skip', percentage: 0, color: 'red-600' }, { label: 'Timepass', percentage: 5, color: 'yellow-500' }, { label: 'Go for it', percentage: 45, color: 'green-500' }, { label: 'Perfection', percentage: 50, color: 'purple-600' }],}, 
            },
            'mystic-falls': { 
                title: 'Mystic Falls', year: 2021, duration: '1 Season', director: 'Diya', country: 'India', language: 'Hindi', ageRating: '13+', posterUrl: 'https://placehold.co/300x450/065f46/d1fae5?text=MYSTIC+FALLS', backgroundUrl: 'https://placehold.co/1400x700/064e3b/d1fae5?text=MYSTIC+FALLS+FOREST', overview: "A small town shrouded in supernatural secrets and ancient myths begins to unravel its history through a series of mysterious events.", genres: ['Mystery', 'Fantasy', 'Horror'], cast: [], 
                vibe: [{ genre: 'Mystery', percentage: 50, color: 'yellow-500' }, { genre: 'Fantasy', percentage: 50, color: 'purple-600' }], 
                familyFriendly: false, 
                reviewScore: { score: 68, totalVotes: 320, breakdown: [{ label: 'Skip', percentage: 15, color: 'red-600' }, { label: 'Timepass', percentage: 25, color: 'yellow-500' }, { label: 'Go for it', percentage: 45, color: 'green-500' }, { label: 'Perfection', percentage: 15, color: 'purple-600' }],}, 
            },
            'the-heist': { 
                title: 'The Heist: Finale', year: 2024, duration: '2h 10m', director: 'Raju', country: 'India', language: 'Hindi', ageRating: '16+', posterUrl: 'https://placehold.co/300x450/1e293b/d1d5db?text=THE+HEIST', backgroundUrl: 'https://placehold.co/1400x700/0f172a/d1d5db?text=THE+HEIST+NIGHT+CITY', overview: "The final, high-stakes operation of a crew of master thieves aiming for the biggest score of their lives. Expect twists, turns, and double-crosses.", genres: ['Crime', 'Thriller', 'Heist'], cast: [], 
                vibe: [{ genre: 'Thriller', percentage: 60, color: 'yellow-500' }, { genre: 'Action', percentage: 40, color: 'blue-600' }], 
                familyFriendly: false, 
                reviewScore: { score: 82, totalVotes: 750, breakdown: [{ label: 'Skip', percentage: 5, color: 'red-600' }, { label: 'Timepass', percentage: 8, color: 'yellow-500' }, { label: 'Go for it', percentage: 57, color: 'green-500' }, { label: 'Perfection', percentage: 30, color: 'purple-600' }],}, 
            },
            'tu-meri-main-tera': { 
                title: 'Tu Meri Main Tera', year: 2023, duration: '2h 30m', director: 'Aisha', country: 'India', language: 'Hindi', ageRating: 'U', posterUrl: 'https://placehold.co/300x450/f0abf0/fce7f3?text=ROMANCE+DRAMA', backgroundUrl: 'https://placehold.co/1400x700/e9d5ff/fce7f3?text=ROMANCE+VALLEY', overview: "A classic Bollywood romance tale about two star-crossed lovers separated by fate and family expectations, fighting to find their way back to each other.", genres: ['Romance', 'Drama', 'Musical'], cast: [], 
                vibe: [{ genre: 'Romance', percentage: 70, color: 'pink-600' }, { genre: 'Drama', percentage: 30, color: 'red-600' }], 
                familyFriendly: true, 
                reviewScore: { score: 75, totalVotes: 800, breakdown: [{ label: 'Skip', percentage: 3, color: 'red-600' }, { label: 'Timepass', percentage: 20, color: 'yellow-500' }, { label: 'Go for it', percentage: 52, color: 'green-500' }, { label: 'Perfection', percentage: 25, color: 'purple-600' }],}, 
            },
            'train-dreams': { 
                title: 'Train Dreams', year: 2024, duration: '1h 58m', director: 'Girish', country: 'India', language: 'Hindi', ageRating: '13+', posterUrl: 'https://placehold.co/300x450/0c4a6e/e0f2f1?text=TRAIN+DREAMS', backgroundUrl: 'https://placehold.co/1400x700/075985/e0f2f1?text=TRAIN+DREAMS+SUNSET', overview: "An artistic film following the quiet, introspective journey of a man traveling across India by train, contemplating life and memories.", genres: ['Art House', 'Drama', 'Travel'], cast: [], 
                vibe: [{ genre: 'Drama', percentage: 70, color: 'red-600' }, { genre: 'Reflection', percentage: 30, color: 'slate-400' }], 
                familyFriendly: true, 
                reviewScore: { score: 60, totalVotes: 250, breakdown: [{ label: 'Skip', percentage: 10, color: 'red-600' }, { label: 'Timepass', percentage: 40, color: 'yellow-500' }, { label: 'Go for it', percentage: 40, color: 'green-500' }, { label: 'Perfection', percentage: 10, color: 'purple-600' }],}, 
            },
            'de-de-pyaar-2': { 
                title: 'De De Pyaar 2', year: 2025, duration: '2h 05m', director: 'Luv', country: 'India', language: 'Hindi', ageRating: 'U/A 13+', posterUrl: 'https://placehold.co/300x450/f97316/ffedd5?text=FAMILY+COMEDY', backgroundUrl: 'https://placehold.co/1400x700/ea580c/ffedd5?text=FAMILY+COMEDY+HOUSE', overview: "A chaotic yet charming family comedy revolving around an extended family reunion where old rivalries and new romances collide.", genres: ['Comedy', 'Family', 'Romance'], cast: [], 
                vibe: [{ genre: 'Comedy', percentage: 60, color: 'green-500' }, { genre: 'Romance', percentage: 40, color: 'pink-600' }], 
                familyFriendly: true, 
                reviewScore: { score: 72, totalVotes: 900, breakdown: [{ label: 'Skip', percentage: 5, color: 'red-600' }, { label: 'Timepass', percentage: 20, color: 'yellow-500' }, { label: 'Go for it', percentage: 45, color: 'green-500' }, { label: 'Perfection', percentage: 30, color: 'purple-600' }],}, 
            },
            'the-liar': { 
                title: 'The Liar', year: 2024, duration: '1h 45m', director: 'Karthik', country: 'India', language: 'Hindi', ageRating: '16+', posterUrl: 'https://placehold.co/300x450/374151/d1d5db?text=PSYCHO+LIAR', backgroundUrl: 'https://placehold.co/1400x700/1f2937/d1d5db?text=THE+LIAR+SUSPENSE', overview: "A gripping psychological thriller where a man's meticulously crafted life unravels after a single lie spirals out of control, blurring the lines between reality and deceit.", genres: ['Psychological', 'Thriller', 'Suspense'], cast: [], 
                vibe: [{ genre: 'Thriller', percentage: 70, color: 'yellow-500' }, { genre: 'Drama', percentage: 30, color: 'red-600' }], 
                familyFriendly: false, 
                reviewScore: { score: 88, totalVotes: 550, breakdown: [{ label: 'Skip', percentage: 1, color: 'red-600' }, { label: 'Timepass', percentage: 6, color: 'yellow-500' }, { label: 'Go for it', percentage: 53, color: 'green-500' }, { label: 'Perfection', percentage: 40, color: 'purple-600' }],}, 
            },
            'old-is-gold': { 
                title: 'Old is Gold', year: 1980, duration: '2h 20m', director: 'Shantaram', country: 'India', language: 'Hindi', ageRating: 'U', posterUrl: 'https://placehold.co/300x450/6b7280/e5e7eb?text=OLD+GOLD+RETRO', backgroundUrl: 'https://placehold.co/1400x700/4b5563/e5e7eb?text=OLD+IS+GOLD+STUDIO', overview: "A timeless classic that explores the nuances of human relationships and the simple joys of life in a bygone era.", genres: ['Classic', 'Drama', 'Family'], cast: [], 
                vibe: [{ genre: 'Drama', percentage: 60, color: 'red-600' }, { genre: 'Nostalgia', percentage: 40, color: 'slate-400' }], 
                familyFriendly: true, 
                reviewScore: { score: 79, totalVotes: 400, breakdown: [{ label: 'Skip', percentage: 2, color: 'red-600' }, { label: 'Timepass', percentage: 10, color: 'yellow-500' }, { label: 'Go for it', percentage: 58, color: 'green-500' }, { label: 'Perfection', percentage: 30, color: 'purple-600' }],}, 
            },
            'raja-rani-3': { 
                title: 'Raja Rani 3', year: 2024, duration: '2h 15m', director: 'Atlee', country: 'India', language: 'Tamil', ageRating: 'U/A 13+', posterUrl: 'https://placehold.co/300x450/d946ef/f3e8ff?text=RAJA+RANI+3', backgroundUrl: 'https://placehold.co/1400x700/c026d3/f3e8ff?text=RAJA+RANI+ROMANCE', overview: "The third installment of the popular franchise, focusing on a new couple facing modern challenges in marriage, mixing romance, comedy, and drama.", genres: ['Romance', 'Drama', 'Comedy'], cast: [], 
                vibe: [{ genre: 'Romance', percentage: 50, color: 'pink-600' }, { genre: 'Comedy', percentage: 30, color: 'green-500' }, { genre: 'Drama', percentage: 20, color: 'red-600' }], 
                familyFriendly: true, 
                reviewScore: { score: 85, totalVotes: 1100, breakdown: [{ label: 'Skip', percentage: 1, color: 'red-600' }, { label: 'Timepass', percentage: 9, color: 'yellow-500' }, { label: 'Go for it', percentage: 60, color: 'green-500' }, { label: 'Perfection', percentage: 30, color: 'purple-600' }],}, 
            },
            'city-lights': { 
                title: 'City Lights', year: 2021, duration: '1h 50m', director: 'Mehta', country: 'India', language: 'Hindi', ageRating: '13+', posterUrl: 'https://placehold.co/300x450/1e293b/f59e0b?text=CITY+LIGHTS+NOIR', backgroundUrl: 'https://placehold.co/1400x700/000000/f59e0b?text=CITY+LIGHTS+SKYLINE', overview: "A neo-noir story set against the backdrop of a sprawling city, where a detective chases a ghost from his past through the shadows and neon lights.", genres: ['Neo-Noir', 'Thriller', 'Crime'], cast: [], 
                vibe: [{ genre: 'Thriller', percentage: 60, color: 'yellow-500' }, { genre: 'Drama', percentage: 40, color: 'red-600' }], 
                familyFriendly: false, 
                reviewScore: { score: 70, totalVotes: 290, breakdown: [{ label: 'Skip', percentage: 10, color: 'red-600' }, { label: 'Timepass', percentage: 20, color: 'yellow-500' }, { label: 'Go for it', percentage: 50, color: 'green-500' }, { label: 'Perfection', percentage: 20, color: 'purple-600' }],}, 
            },
            'action-man-7': { 
                title: 'Action Man 7', year: 2025, duration: '2h 10m', director: 'Rohit', country: 'India', language: 'Hindi', ageRating: '16+', posterUrl: 'https://placehold.co/300x450/dc2626/fef2f2?text=ACTION+MAN+7', backgroundUrl: 'https://placehold.co/1400x700/991b1b/fef2f2?text=ACTION+MAN+EXPLOSION', overview: "The ultimate action spectacle, featuring gravity-defying stunts and a race against time to prevent a global catastrophe caused by a rogue agent.", genres: ['Action', 'Sci-Fi', 'Thriller'], cast: [], 
                reviewScore: { score: 92, totalVotes: 1500, breakdown: [{ label: 'Skip', percentage: 1, color: 'red-600' }, { label: 'Timepass', percentage: 2, color: 'yellow-500' }, { label: 'Go for it', percentage: 57, color: 'green-500' }, { label: 'Perfection', percentage: 40, color: 'purple-600' }],}, 
            },
        };
        
        // --- UTILITY FUNCTIONS ---

        // Function to generate the User Review Score Chart HTML
        const generateReviewChartHtml = (reviewData) => {
            const { score, totalVotes, breakdown } = reviewData;
            
            const circumference = 377;
            let cumulativeOffset = 0;
            const breakdownSegments = breakdown.map(item => {
                const dashArray = `${(item.percentage / 100) * circumference} ${circumference}`;
                const segment = `
                    <circle
                        class="text-${item.color}"
                        stroke="currentColor"
                        stroke-width="15"
                        fill="transparent"
                        r="60"
                        cx="75"
                        cy="75"
                        stroke-dasharray="${dashArray}"
                        stroke-dashoffset="${-cumulativeOffset}"
                    />
                `;
                cumulativeOffset += (item.percentage / 100) * circumference;
                return segment;
            }).join('');

            const voteBreakdownHtml = breakdown.map(item => `
                <div class="flex items-center space-x-1 mt-2">
                    <span class="w-2 h-2 bg-${item.color} rounded-full"></span>
                    <span class="text-gray-400">${item.label} ${item.percentage}%</span>
                </div>
            `).join('');

            return `
                <div class="flex flex-col items-center justify-center bg-slate-900 p-6 rounded-lg shadow-xl border border-slate-700">
                    <div class="relative w-40 h-40 mb-6">
                        <svg class="w-full h-full transform -rotate-90" viewBox="0 0 150 150">
                            <circle class="text-slate-800" stroke="currentColor" stroke-width="15" fill="transparent" r="60" cx="75" cy="75" />
                            ${breakdownSegments}
                        </svg>
                        <div class="absolute inset-0 flex flex-col items-center justify-center text-center">
                            <span class="text-4xl font-extrabold text-green-400">${score}%</span>
                            <span class="text-sm text-gray-400">${totalVotes} Votes</span>
                        </div>
                    </div>

                    <div class="flex flex-wrap justify-center text-sm mb-6 space-x-4">
                        ${voteBreakdownHtml}
                    </div>

                    <!-- Review Input Box (Static/Placeholder since state is removed) -->
                    <div class="w-full mt-6 bg-slate-800 p-4 rounded-lg border border-slate-700">
                        <p class="text-center text-sm text-gray-500 mb-4">
                            Login required to submit reviews.
                        </p>
                        <div class="flex items-center space-x-3 mb-4">
                            <img src="https://placehold.co/40x40/f59e0b/1f2937?text=AK" alt="User Avatar" class="w-10 h-10 rounded-full bg-indi-accent">
                            <span class="text-white font-semibold">@UserHandle</span>
                        </div>
                        
                        <div class="flex flex-wrap gap-2 mb-4">
                            ${breakdown.map(item => `
                                <button class="text-xs font-semibold px-3 py-1 rounded-full border border-slate-700 bg-slate-800 text-gray-500 cursor-not-allowed">${item.label}</button>
                            `).join('')}
                        </div>
                        
                        <textarea class="w-full p-2 bg-slate-700 border-none rounded-lg text-sm text-gray-200 focus:ring-0 focus:outline-none resize-none h-20" placeholder="Write your review here..." disabled></textarea>
                        
                        <div class="flex justify-between items-center mt-2">
                            <span class="text-xs text-gray-500">0/1000</span>
                            <button class="bg-slate-700 text-gray-500 font-bold py-1.5 px-4 rounded-lg transition duration-200 cursor-not-allowed" disabled>Post</button>
                        </div>
                    </div>
                </div>
            `;
        };

        // Function to generate the Vibe Chart HTML (SVG Donut Chart + Legend)
        const generateVibeChartHtml = (vibeData) => {
            if (!vibeData || vibeData.length === 0) {
                return '<div class="bg-slate-900 p-5 rounded-lg shadow-lg mb-8 border border-slate-800 text-center text-gray-500">No Vibe data available.</div>'; 
            }
            
            const primaryVibe = vibeData[0]; 
            const circumference = 283;
            let offset = 0;
            
            const svgSegments = vibeData.map(item => {
                const strokeDasharray = `${(item.percentage / 100) * circumference} ${circumference}`;
                const segmentHtml = `
                    <circle
                        class="text-${item.color}"
                        stroke="currentColor"
                        stroke-width="12"
                        fill="transparent"
                        r="45"
                        cx="50"
                        cy="50"
                        stroke-dasharray="${strokeDasharray}"
                        stroke-dashoffset="-${offset}"
                    />
                `;
                offset += (item.percentage / 100) * circumference;
                return segmentHtml;
            }).join('');

            const legendHtml = vibeData.map(item => `
                <div class="flex justify-between py-1.5 px-3 border-b border-slate-800 last:border-b-0">
                    <div class="flex items-center space-x-2">
                        <span class="w-3 h-3 bg-${item.color} rounded-full flex-shrink-0"></span>
                        <span class="text-base text-gray-400">${item.genre}</span>
                    </div>
                    <span class="text-white font-semibold">${item.percentage}%</span>
                </div>
            `).join('');

            const chartBlock = `
                <div class="bg-slate-900 p-5 rounded-lg shadow-xl mb-8 border border-slate-700 w-full"> 
                    <h2 class="text-xl font-bold mb-4">Vibe Chart</h2>
                    <div class="flex flex-col items-center">
                        <div class="relative w-32 h-32 mb-6">
                            <svg class="w-full h-full transform -rotate-90" viewBox="0 0 100 100">
                                <circle class="text-slate-800" stroke="currentColor" stroke-width="12" fill="transparent" r="45" cx="50" cy="50" />
                                ${svgSegments}
                            </svg>
                            <div class="absolute inset-0 flex flex-col items-center justify-center text-center">
                                <span class="text-2xl font-extrabold text-${primaryVibe.color}">${primaryVibe.percentage}%</span>
                                <span class="text-sm text-gray-300">${primaryVibe.genre}</span>
                            </div>
                        </div>
                        <div class="w-full space-y-1 mt-4">
                            ${legendHtml}
                        </div>
                    </div>
                </div>
            `;
            return chartBlock;
        };

        // Function to generate the Cast section HTML
        const generateCastHtml = (castData) => {
            if (!castData || castData.length === 0) {
                return '<p class="text-gray-500 mt-4">Cast details coming soon.</p>';
            }
            return `
                <div class="grid grid-cols-3 sm:grid-cols-4 md:grid-cols-5 lg:grid-cols-6 gap-4 mt-6">
                    ${castData.map(member => `
                        <div class="flex flex-col items-center text-center">
                            <img 
                                src="${member.img}" 
                                alt="${member.name}" 
                                class="w-20 h-20 rounded-full object-cover border-2 border-slate-700 hover:border-indi-accent transition duration-200"
                            >
                            <span class="text-sm font-semibold text-white mt-2 leading-tight">${member.name}</span>
                            <span class="text-xs text-gray-400 truncate">${member.role}</span>
                        </div>
                    `).join('')}
                </div>
            `;
        };
        
        // Function to handle movie playback (redirect to YouTube search)
        const handlePlaybackClick = (title) => {
            const searchQuery = `${title} full movie hindi free youtube`;
            const url = `https://www.youtube.com/results?search_query=${encodeURIComponent(searchQuery)}`;
            window.open(url, '_blank');
        };

        // --- MAIN ROUTING AND RENDERING ---
        
        const goBack = () => {
            showPage('home');
        };

        const goHome = () => {
            showPage('home');
        };

        const renderDetailPage = (movieKey) => {
            const data = MOVIE_DATA[movieKey];
            if (!data) return '<p class="text-center p-8">Movie data not found.</p>';

            // Set current movie key for state tracking
            document.getElementById('detail-view').setAttribute('data-current-movie', movieKey);


            const vibeChartHtml = generateVibeChartHtml(data.vibe || []);
            const castHtml = generateCastHtml(data.cast || []);
            const reviewChartHtml = generateReviewChartHtml(data.reviewScore); 
            
            const genreTags = data.genres.map(tag => `
                <span class="bg-slate-700 text-gray-300 text-sm px-3 py-1 rounded-full hover:bg-slate-600 transition duration-150 cursor-pointer">
                    ${tag}
                </span>
            `).join('');
            
            const detailHtml = `
                <div class="relative w-full min-h-screen">
                    
                    <!-- Large Background Image/Video Placeholder (Top Section) -->
                    <div class="absolute top-0 left-0 w-full h-[550px] md:h-[650px] z-0">
                        <img src="${data.backgroundUrl}" alt="${data.title} Background" class="w-full h-full object-cover opacity-20 brightness-75">
                        <div class="absolute inset-0 bg-gradient-to-t from-slate-950/95 via-slate-950/70 to-slate-950/50"></div>
                    </div>
                    
                    <!-- Detail Content Container -->
                    <div class="max-w-[85rem] mx-auto px-4 sm:px-6 lg:px-8 relative z-10 detail-content-wrapper">
                        
                        <!-- Main Movie Block (Poster/Title/Buttons) -->
                        <div class="flex flex-col md:flex-row items-center md:items-start space-y-6 md:space-y-0 md:space-x-10 mb-12">
                            
                            <!-- Floating Poster Card (Left) -->
                            <div class="flex-shrink-0 w-48 md:w-64 rounded-xl overflow-hidden shadow-2xl mt-8">
                                <img src="${data.posterUrl}" alt="${data.title} Poster" class="w-full h-auto object-cover border-4 border-slate-700">
                            </div>

                            <!-- Details (Right) -->
                            <div class="flex flex-col text-white w-full md:w-auto mt-6 md:mt-16">
                                <p class="text-sm font-light text-gray-300 mb-1">Movie • ${data.year} • ${data.duration}</p>
                                <h1 class="text-4xl md:text-6xl font-extrabold mb-4 leading-tight">${data.title}</h1>
                                
                                <!-- Meta Tags Row -->
                                <div class="flex flex-wrap text-sm text-gray-400 space-x-4 mb-6">
                                    <span>Directed By <span class="text-white font-semibold">${data.director}</span></span>
                                    <span>Country <span class="text-white font-semibold">${data.country}</span></span>
                                    <span>Language <span class="text-white font-semibold">${data.language}</span></span>
                                    <span class="text-indi-accent font-semibold">Age Rating ${data.ageRating}</span>
                                </div>

                                <!-- Action Buttons -->
                                <div class="flex flex-col sm:flex-row space-y-3 sm:space-y-0 sm:space-x-4">
                                    <!-- Watch/Track Button REMOVED -->
                                    <button onclick="handlePlaybackClick('${data.title}')" class="flex items-center justify-center space-x-2 bg-indi-accent hover:bg-amber-600 text-slate-900 font-bold py-3 px-6 rounded-full transition duration-300 shadow-xl">
                                        <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M5.25 5.653c0-.856.917-1.398 1.667-.986l11.54 6.348a1.125 1.125 0 010 1.972l-11.54 6.347a1.125 1.125 0 01-1.667-.985V5.653z" /></svg>
                                        <span>Find Full Movie on YouTube</span>
                                    </button>
                                </div>
                            </div>
                        </div>
                        
                        <!-- Secondary Content (Overview, Vibe Chart, Cast) -->
                        <div class="grid lg:grid-cols-[1fr_320px] gap-8">
                            
                            <!-- Left Column: Overview and Cast -->
                            <div>
                                <!-- Family Friendly Tag -->
                                ${data.familyFriendly ? `
                                    <span class="inline-flex items-center space-x-2 bg-green-900/50 text-green-400 border border-green-700 px-3 py-1 rounded-full text-sm font-semibold mb-6">
                                        <svg class="w-4 h-4" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M15.75 6a3.75 3.75 0 11-7.5 0 3.75 3.75 0 017.5 0zM4.5 20.25a9.75 9.75 0 0015 0" /></svg>
                                        <span>Family Friendly</span>
                                    </span>
                                ` : ''}

                                <!-- Overview Section -->
                                <h2 class="text-2xl font-bold mb-4">Overview</h2>
                                <p class="text-gray-300 mb-6 max-w-4xl">${data.overview}</p>
                                
                                <!-- Genre Tags -->
                                <div class="flex flex-wrap gap-3 mb-10">
                                    ${genreTags}
                                </div>


                                <!-- Cast Section -->
                                <h2 class="text-2xl font-bold mb-6">Cast</h2>
                                ${castHtml}
                            </div>

                            <!-- Right Column: Vibe Chart and Tickets (320px sidebar) -->
                            <div class="lg:pr-4">
                                
                                <!-- Vibe Chart -->
                                ${vibeChartHtml}
                                
                                <!-- Tickets On Section -->
                                <div class="bg-slate-900 p-5 rounded-lg shadow-xl mb-8 border border-slate-700">
                                    <h2 class="text-xl font-bold mb-4">Tickets On</h2>
                                    <div class="flex flex-col space-y-3">
                                        <div class="flex items-center space-x-3 p-3 bg-slate-800 rounded-lg hover:bg-slate-700 transition duration-150 cursor-pointer">
                                            <img src="https://placehold.co/40x40/f43f5e/ffffff?text=BM" alt="BookMyShow Logo" class="rounded-lg">
                                            <span class="font-semibold text-white">BookMyShow</span>
                                        </div>
                                        <div class="flex items-center space-x-3 p-3 bg-slate-800 rounded-lg hover:bg-slate-700 transition duration-150 cursor-pointer">
                                            <img src="https://placehold.co/40x40/9333ea/ffffff?text=P" alt="PVR Logo" class="rounded-lg">
                                            <span class="font-semibold text-white">PVR Cinemas</span>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        
                        <!-- Reviews Section (Full width, placed AFTER the Overview/Cast/Right-Sidebar section) -->
                        <div class="mt-12 w-full lg:max-w-[85rem] mx-auto">
                            <h2 class="text-2xl font-bold mb-6">Reviews</h2>
                            
                            <!-- User Score Chart / Review Input -->
                            ${reviewChartHtml}
                        </div>
                    </div>
                </div>
            `;
            document.getElementById('detail-view').innerHTML = detailHtml;
        };

        const showPage = (page, movieKey = null) => {
            const homeView = document.getElementById('home-view');
            const detailView = document.getElementById('detail-view');
            const backBtn = document.getElementById('back-btn');
            
            // Hide all other dropdowns when changing pages
            document.getElementById('search-dropdown').classList.add('hidden');
            document.getElementById('notifications-dropdown').classList.add('hidden');

            // Logic to switch views
            homeView.classList.add('hidden');
            detailView.classList.add('hidden');
            
            if (page === 'home') {
                homeView.classList.remove('hidden');
                document.title = 'Indiwood. | Explore Cinema & Culture';
                backBtn.classList.add('hidden'); // Hide back button on home
            } else if (page === 'detail' && movieKey && MOVIE_DATA[movieKey]) {
                renderDetailPage(movieKey);
                detailView.classList.remove('hidden');
                document.title = MOVIE_DATA[movieKey].title + ' | Indiwood';
                backBtn.classList.remove('hidden'); // Show back button on detail
            }
            // Scroll to top when switching pages
            window.scrollTo(0, 0);
        };

        const initPosters = () => {
            const movieElements = document.querySelectorAll('[data-movie]');
            
            movieElements.forEach(el => {
                const movieKey = el.getAttribute('data-movie');
                
                // Set cursor style for visual feedback
                el.style.cursor = 'pointer';
                
                // Add click listener
                el.addEventListener('click', (e) => {
                    // Prevent navigation if the click was on a badge or internal element within the card
                    if (e.target.closest('a') || e.target.closest('span')) return; 
                    showPage('detail', movieKey);
                });
            });
        };


        document.addEventListener('DOMContentLoaded', () => {
            // --- Dropdown Toggles (existing logic) ---
            const searchToggleBtn = document.getElementById('search-toggle-btn');
            const searchDropdown = document.getElementById('search-dropdown');
            const notificationsToggleBtn = document.getElementById('notifications-toggle-btn');
            const notificationsDropdown = document.getElementById('notifications-dropdown');

            const toggleDropdown = (button, dropdown, otherDropdown) => {
                const isHidden = dropdown.classList.contains('hidden');
                
                // 1. Close the other dropdown if it's open
                if (otherDropdown && !otherDropdown.classList.contains('hidden')) {
                    otherDropdown.classList.add('hidden');
                }
                
                // 2. Toggle the current dropdown
                if (isHidden) {
                    dropdown.classList.remove('hidden');
                    
                    if (dropdown === searchDropdown) {
                        const input = dropdown.querySelector('input[type="text"]');
                        if (input) {
                            setTimeout(() => input.focus(), 50);
                        }
                    }
                } else {
                    dropdown.classList.add('hidden');
                }
            };

            if (searchToggleBtn && searchDropdown && notificationsDropdown) {
                searchToggleBtn.addEventListener('click', () => {
                    toggleDropdown(searchToggleBtn, searchDropdown, notificationsDropdown);
                });
            }

            if (notificationsToggleBtn && notificationsDropdown && searchDropdown) {
                notificationsToggleBtn.addEventListener('click', () => {
                    toggleDropdown(notificationsToggleBtn, notificationsDropdown, searchDropdown);
                });
            }
            // --- End Dropdown Toggles ---
            
            // Initialize event listeners for movie posters
            initPosters();
            
            // Expose utility functions globally for HTML click handlers
            window.goBack = goBack;
            window.goHome = goHome;
            window.showPage = showPage;

        });
    </script>

</body>
</html>


