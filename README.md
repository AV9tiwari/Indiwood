<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Indiwood. | Explore Cinema & Culture</title>
    <!-- Load Tailwind CSS --><script src="https://cdn.tailwindcss.com"></script>
    <!-- Load Inter Font --><link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap">
    <style>
        /* Custom styles for the Indiwood aesthetic */
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
            box-shadow: 0 10px 15px rgba(0, 0, 0, 0.5);
        }
        /* Style for the horizontal scroll container */
        .horizontal-scroll-container::-webkit-scrollbar {
            display: none;
        }
        .horizontal-scroll-container {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
        /* Custom card styling to mimic poster proportions */
        .poster-card {
            width: 150px;
            height: auto;
            display: inline-block;
            margin-right: 1.5rem;
        }
        .large-poster-card {
            width: 200px;
            height: auto;
            display: inline-block;
            margin-right: 1.5rem;
        }
        /* Responsive widths for smaller posters */
        @media (min-width: 640px) { .poster-card { width: 180px; } }
        @media (min-width: 1024px) { .poster-card { width: 150px; } }

        .main-layout {
            grid-template-columns: 1fr;
        }
        .category-title:hover {
            color: #d1d5db;
            cursor: pointer;
        }
        .search-dropdown {
            transition: all 0.3s ease-in-out;
            transform-origin: top;
        }
        #detail-view .detail-content-wrapper {
            padding-top: 8rem;
            min-height: calc(100vh - 4rem);
        }

        /* --- UPDATED TRICOLOUR TEXT STYLE (Horizontal and Blended) --- */
        .text-tricolor {
            /* Indian Flag Colors: Saffron (#FF9933), White (#FFFFFF), Green (#138808) */
            /* Creating horizontal bands (top to bottom) with soft transition stops for blending */
            background: linear-gradient(to bottom, 
                #FF9933 0%,    /* Saffron top band start */
                #FF9933 30%,   /* Saffron top band end */
                #FFFFFF 45%,   /* White middle band start with blend */
                #FFFFFF 55%,   /* White middle band end */
                #138808 70%,   /* Green bottom band start with blend */
                #138808 100%   /* Green bottom band end */
            );
            -webkit-background-clip: text; /* Safari/Chrome */
            background-clip: text;
            color: transparent;
            /* Ensure font weight is high enough for the gradient to show */
            font-weight: 900; 
            display: inline-block; /* Essential for clipping to work well */
        }
    </style>
</head>
<body class="bg-slate-950 text-gray-100 min-h-screen">

    <!-- Header / Navigation Bar (Top Bar) -->
    <header class="sticky top-0 z-50 bg-slate-900 shadow-lg border-b border-slate-800">
        <div class="max-w-[85rem] mx-auto px-4 sm:px-6 lg:px-8 py-3 flex justify-between items-center h-16">
            
            <!-- Left Side: Back Button + Logo -->
            <div class="flex items-center space-x-2">
                
                <!-- Back Button (Toggle visibility in JS) -->
                <button id="back-btn" onclick="goBack();" class="hidden p-2 rounded-full hover:bg-slate-800 transition duration-200 text-gray-400" aria-label="Go Back" title="Go Back">
                    <!-- Heroicon: Arrow Left -->
                    <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M10.5 19.5L3 12m0 0l7.5-7.5M3 12h18" /></svg>
                </button>
                
                <!-- Logo/Brand (UPDATED: text now uses smooth horizontal gradient) -->
                <a href="#" class="flex items-center space-x-2" onclick="goHome(); return false;">
                    <div class="bg-indi-accent p-1.5 rounded-md text-gray-900 font-extrabold text-lg leading-none">I</div>
                    <div class="flex flex-col">
                        <span class="text-2xl font-extrabold tracking-tight">
                            <span class="text-tricolor">Indiwood</span>
                        </span>
                        <span class="text-xs text-gray-400 -mt-1">Cinema & Culture Hub</span>
                    </div>
                </a>
            </div>
            
            <!-- Spacer (Occupies center space) -->
            <div class="flex-grow hidden md:block"></div>

            <!-- Right Icons & Profile -->
            <div class="flex items-center space-x-4">
                
                <!-- 1. Search Icon (Toggle Button) -->
                <button id="search-toggle-btn" class="p-2 rounded-full hover:bg-slate-800 transition duration-200" aria-label="Search" title="Search">
                    <svg class="w-6 h-6 text-gray-400" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" /></svg>
                </button>

                <!-- 2. Bell Icon (Notifications) -->
                <button id="notifications-toggle-btn" class="p-2 rounded-full hover:bg-slate-800 transition duration-200" aria-label="Notifications" title="Notifications">
                    <svg class="w-6 h-6 text-gray-400" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M14.857 17.082a23.848 23.848 0 005.454-1.31A8.967 8.967 0 0118 9.75V9A6 6 0 006 9v.75a8.967 8.967 0 01-2.312 6.022c1.733.64 3.56 1.04 5.455 1.31m5.714 0a24.255 24.255 0 01-5.714 0m5.714 0a3 3 0 11-5.714 0" /></svg>
                </button>
                
                <!-- 3. User Circle Icon (Profile) -->
                <button class="p-2 rounded-full hover:bg-slate-800 transition duration-200" aria-label="User Profile" title="Profile">
                    <svg class="w-8 h-8 text-indi-accent" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M17.982 18.725A7.488 7.488 0 0012 15.75a7.488 7.488 0 00-5.982 2.975m11.963 0a9 9 0 10-11.963 0m11.963 0A8.966 8.966 0 0112 21a8.966 8.966 0 01-5.982-2.275M15 9.75a3 3 0 11-6 0 3 3 0 016 0z" /></svg>
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
                    <p>New Episode Alert: <span class="font-semibold">Panchayat S4</span> just released!</p>
                </li>
                <li class="flex items-start space-x-2 p-1.5 hover:bg-slate-700 rounded transition duration-150 cursor-pointer">
                    <span class="text-indi-accent flex-shrink-0 mt-1">&#9679;</span>
                    <p>Your review on <span class="font-semibold">Pathaan</span> was featured in 'Top 10'.</p>
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
            
            <!-- Left & Center Content (Main Stream) -->
            <main class="lg:pr-4">
                
                <!-- Hero Section (Featured Movie: Durandhar) -->
                <section id="hero-durandhar" class="relative bg-slate-900 rounded-xl overflow-hidden shadow-2xl mb-12 cursor-pointer group" data-movie="durandhar">
                    <!-- Background Image Placeholder (High Contrast, Cinematic) -->
                    <div class="relative w-full h-[300px] md:h-[450px]">
                        <img src="https://placehold.co/1400x700/6b7280/1f2937?text=DURANDHAR+EPIC+WAR" alt="Durandhar Hero Background" class="w-full h-full object-cover group-hover:scale-[1.02] transition-transform duration-500 opacity-60">
                        <div class="absolute inset-0 bg-gradient-to-t from-slate-950/90 via-slate-950/50 to-transparent"></div>
                    </div>

                    <!-- Content Overlay -->
                    <div class="absolute bottom-0 left-0 p-6 md:p-12 w-full max-w-2xl text-white">
                        <p class="text-sm font-semibold text-indi-accent mb-2">UPCOMING EPIC | HISTORICAL / ACTION</p>
                        <h1 class="text-4xl sm:text-5xl md:text-7xl font-extrabold leading-tight mb-4">Durandhar</h1>
                        <p class="text-gray-300 mb-6 line-clamp-3">A fictional historical epic starring Ranveer Singh as a legendary, ruthless warrior chieftain known for his unmatched military prowess and ambition across the subcontinent.</p>
                        <div class="flex space-x-4">
                            <!-- Button to trigger movie detail view/playback (redirect) -->
                            <button onclick="handlePlaybackClick('Durandhar')" class="flex items-center justify-center space-x-2 bg-indi-accent hover:bg-amber-600 text-slate-900 font-bold py-3 px-6 rounded-full transition duration-300 shadow-xl transform group-hover:scale-[1.05]">
                                <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M5.25 5.653c0-.856.917-1.398 1.667-.986l11.54 6.348a1.125 1.125 0 010 1.972l-11.54 6.347a1.125 1.125 0 01-1.667-.985V5.653z" /></svg>
                                <span>Watch Trailer on YouTube</span>
                            </button>
                        </div>
                    </div>
                </section>
                
                <!-- Section 1: Talk Of The Town (Horizontal Scroll) -->
                <section class="mb-12">
                    <h2 class="text-2xl font-bold mb-6 border-l-4 border-indi-accent pl-3 category-title transition-colors duration-200">Talk Of The Town</h2>
                    
                    <!-- Horizontal Scroll Container -->
                    <div class="horizontal-scroll-container flex overflow-x-auto pb-4">
                        
                        <!-- Pathaan -->
                        <div class="large-poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="pathaan">
                            <div class="relative">
                                <img src="https://placehold.co/400x600/b91c1c/fef2f2?text=PATHAAN+AGENT" alt="Pathaan Poster" class="w-full h-80 object-cover">
                                <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 to-transparent"></div>
                                <div class="absolute bottom-0 left-0 p-3 w-full">
                                    <h3 class="text-lg font-bold truncate">Pathaan</h3>
                                    <p class="text-xs text-gray-400">YRF Spy Series <span class="bg-red-600 text-white px-1 ml-1 rounded">Hit</span></p>
                                </div>
                            </div>
                        </div>

                        <!-- Durandhar (New addition, replaces Bhaag Milkha Bhaag slot in TOTT) -->
                        <div class="large-poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="durandhar">
                            <div class="relative">
                                <img src="https://placehold.co/400x600/6b7280/1f2937?text=DURANDHAR" alt="Durandhar Poster" class="w-full h-80 object-cover">
                                <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 to-transparent"></div>
                                <div class="absolute bottom-0 left-0 p-3 w-full">
                                    <h3 class="text-lg font-bold truncate">Durandhar</h3>
                                    <p class="text-xs text-gray-400">Epic Action</p>
                                </div>
                            </div>
                        </div>
                        
                        <!-- Panchayat (Kept) -->
                        <div class="large-poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="panchayat">
                            <div class="relative">
                                <img src="https://placehold.co/400x600/059669/ccfbf1?text=PANCHAYAT+S3" alt="Panchayat Poster" class="w-full h-80 object-cover">
                                <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 to-transparent"></div>
                                <div class="absolute bottom-0 left-0 p-3 w-full">
                                    <h3 class="text-lg font-bold truncate">Panchayat</h3>
                                    <p class="text-xs text-gray-400">Amazon MiniTV Series</p>
                                </div>
                            </div>
                        </div>

                        <!-- Sacred Games (Kept) -->
                        <div class="large-poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="sacred-games">
                            <div class="relative">
                                <img src="https://placehold.co/400x600/1e40af/bfdbfe?text=SACRED+GAMES" alt="Sacred Games Poster" class="w-full h-80 object-cover">
                                <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 to-transparent"></div>
                                <div class="absolute bottom-0 left-0 p-3 w-full">
                                    <h3 class="text-lg font-bold truncate">Sacred Games</h3>
                                    <p class="text-xs text-gray-400">Netflix Crime Thriller</p>
                                </div>
                            </div>
                        </div>

                        <!-- Uri: The Surgical Strike (Kept) -->
                        <div class="large-poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="uri">
                            <div class="relative">
                                <img src="https://placehold.co/400x600/15803d/dcfce7?text=URI+STRIKE" alt="Uri Poster" class="w-full h-80 object-cover">
                                <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 to-transparent"></div>
                                <div class="absolute bottom-0 left-0 p-3 w-full">
                                    <h3 class="text-lg font-bold truncate">Uri: The Surgical Strike</h3>
                                    <p class="text-xs text-gray-400">Action Blockbuster</p>
                                </div>
                            </div>
                        </div>
                        
                        <!-- The Family Man (Kept) -->
                        <div class="large-poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="family-man">
                            <div class="relative">
                                <img src="https://placehold.co/400x600/44403c/f5f5f4?text=FAMILY+MAN+S3" alt="The Family Man Poster" class="w-full h-80 object-cover">
                                <div class="absolute inset-0 bg-gradient-to-t from-slate-950/80 to-transparent"></div>
                                <div class="absolute bottom-0 left-0 p-3 w-full">
                                    <h3 class="text-lg font-bold truncate">The Family Man</h3>
                                    <p class="text-xs text-gray-400">Prime Video Series</p>
                                </div>
                            </div>
                        </div>
                        
                        <!-- End of Horizontal Cards -->
                    </div>
                </section>
                
                <!-- Section 2: Netflix Originals -->
                <section class="mt-8 mb-12">
                    <h2 class="text-2xl font-bold mb-6 border-l-4 border-red-600 pl-3 text-red-400 category-title transition-colors duration-200">Netflix Originals (Indian)</h2>
                    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 gap-6 justify-items-center sm:justify-items-start">
                        
                        <!-- NETFLIX Card 1: Sacred Games (Kept) -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="sacred-games">
                            <div class="relative">
                                <img src="https://placehold.co/300x450/450a0a/fca5a5?text=SACRED+GAMES" alt="Sacred Games Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Sacred Games</h3>
                                    <p class="text-xs text-gray-400">Crime Thriller</p>
                                </div>
                            </div>
                        </div>

                        <!-- NETFLIX Card 2: Jailer (Kept) -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="jailer">
                            <div class="relative">
                                <img src="https://placehold.co/300x450/7c3aed/f3e8ff?text=JAILER+MASS" alt="Jailer Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Jailer</h3>
                                    <p class="text-xs text-gray-400">Tamil Action <span class="bg-red-600 text-white px-1 ml-1 rounded">Hit</span></p>
                                </div>
                            </div>
                        </div>
                        
                        <!-- NETFLIX Card 3: Tumbbad (Kept) -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="tumbbad">
                            <div class="relative">
                                <img src="https://placehold.co/300x450/065f46/d1fae5?text=TUMBBAD" alt="Tumbbad Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Tumbbad</h3>
                                    <p class="text-xs text-gray-400">Fantasy Horror</p>
                                </div>
                            </div>
                        </div>

                        <!-- NETFLIX Card 4: Gangs of Wasseypur (Kept) -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="gangs-of-wasseypur">
                            <div class="relative">
                                <img src="https://placehold.co/300x450/1e293b/d1d5db?text=GOW+SAGA" alt="Gangs of Wasseypur Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Gangs of Wasseypur</h3>
                                    <p class="text-xs text-gray-400">Crime Saga</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </section>
                
                <!-- Section 3: Prime Video Hits -->
                <section class="mt-8 mb-12">
                    <h2 class="text-2xl font-bold mb-6 border-l-4 border-cyan-600 pl-3 text-cyan-400 category-title transition-colors duration-200">Prime Video Hits (Regional)</h2>
                    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 gap-6 justify-items-center sm:justify-items-start">
                        
                        <!-- Prime Card 1: The Family Man (Kept) -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="family-man">
                            <div class="relative">
                                <img src="https://placehold.co/300x450/f0abf0/fce7f3?text=FAMILY+MAN" alt="The Family Man Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">The Family Man</h3>
                                    <p class="text-xs text-gray-400">Spy Thriller Series</p>
                                </div>
                            </div>
                        </div>

                        <!-- Prime Card 2: Kantara (Kept) -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="kantara">
                            <div class="relative">
                                <img src="https://placehold.co/300x450/004d40/e8f5e9?text=KANTARA+RITUAL" alt="Kantara Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Kantara</h3>
                                    <p class="text-xs text-gray-400">Kannada Hit <span class="bg-blue-600 text-white px-1 ml-1 rounded">New</span></p>
                                </div>
                            </div>
                        </div>
                        
                        <!-- Prime Card 3: OMG - Oh My God! (Kept) -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="omg-oh-my-god">
                            <div class="relative">
                                <img src="https://placehold.co/300x450/f97316/ffedd5?text=OMG+GOD" alt="OMG - Oh My God! Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">OMG - Oh My God!</h3>
                                    <p class="text-xs text-gray-400">Socio-Comedy</p>
                                </div>
                            </div>
                        </div>

                        <!-- Prime Card 4: Drishyam (Kept) -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="drishyam">
                            <div class="relative">
                                <img src="https://placehold.co/300x450/374151/d1d5db?text=DRISHYAM" alt="Drishyam Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Drishyam</h3>
                                    <p class="text-xs text-gray-400">Crime Thriller</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </section>
                
                <!-- Section 4: Indie Discoveries -->
                <section class="mt-8 mb-12">
                    <h2 class="text-2xl font-bold mb-6 border-l-4 border-indi-accent pl-3 text-indi-accent category-title transition-colors duration-200">Indie Discoveries</h2>
                    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 gap-6 justify-items-center sm:justify-items-start">
                        
                        <!-- Indie Card 1: PK (Kept) -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="pk">
                            <div class="relative">
                                <img src="https://placehold.co/300x450/6b7280/e5e7eb?text=PK+ALIEN" alt="PK Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">PK</h3>
                                    <p class="text-xs text-gray-400">Sci-Fi Comedy</p>
                                </div>
                            </div>
                        </div>

                        <!-- Indie Card 2: Kabir Singh (Kept) -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="kabir-singh">
                            <div class="relative">
                                <img src="https://placehold.co/300x450/d946ef/f3e8ff?text=KABIR+SINGH" alt="Kabir Singh Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Kabir Singh</h3>
                                    <p class="text-xs text-gray-400">Romance Drama <span class="bg-indi-accent text-slate-950 px-1 ml-1 rounded">Hit</span></p>
                                </div>
                            </div>
                        </div>

                        <!-- Indie Card 3: Dil Chahta Hai (Kept) -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="dil-chahta-hai">
                            <div class="relative">
                                <img src="https://placehold.co/300x450/1e293b/f59e0b?text=DIL+CH+H" alt="Dil Chahta Hai Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">Dil Chahta Hai</div>
                                    <p class="text-xs text-gray-400">Coming-of-Age</p>
                                </div>
                            </div>
                        </div>
                        
                        <!-- Indie Card 4: KGF Chapter 1 (Kept) -->
                        <div class="poster-card flex-shrink-0 bg-slate-900 rounded-lg overflow-hidden shadow-lg hover-lift transition duration-300" data-movie="kgf-chapter-1">
                            <div class="relative">
                                <img src="https://placehold.co/300x450/dc2626/fef2f2?text=KGF+CHAPTER+1" alt="KGF Chapter 1 Poster" class="w-full h-auto object-cover">
                                <div class="absolute bottom-0 left-0 p-2 w-full">
                                    <h3 class="text-sm font-bold truncate">K.G.F: Chapter 1</h3>
                                    <p class="text-xs text-gray-400">Massive Action</p>
                                </div>
                            </div>
                        </div>
                        <!-- End of Small Cards -->
                    </div>
                </section>
                
            </main>
            
        </div>
    </div>

    <!-- 2. DETAIL VIEW (Hidden by default) -->
    <div id="detail-view" class="hidden">
        <!-- Detail page content will be injected here by JavaScript -->
        <!-- Loading State will be shown here temporarily -->
    </div>

    <!-- JavaScript for Interactivity and Routing -->
    <script>
        
        // --- Data Store for all movies (Authentic Indian Content) ---
        const MOVIE_DATA = {
            'durandhar': {
                title: 'Durandhar', year: 2026, duration: '2h 50m', director: 'Sanjay Leela Bansali', country: 'India', language: 'Hindi', ageRating: '16+',
                posterUrl: 'https://placehold.co/400x600/6b7280/1f2937?text=DURANDHAR',
                backgroundUrl: 'https://placehold.co/1400x700/6b7280/1f2937?text=DURANDHAR+EPIC+WAR', 
                overview: "A fictional historical epic starring Ranveer Singh as a legendary, ruthless warrior chieftain known for his unmatched military prowess and ambition across the subcontinent.",
                genres: ['Historical', 'Action', 'Epic', 'Drama'],
                cast: [
                    { name: 'Ranveer Singh', role: 'Durandhar', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=RS' },
                ],
                vibe: [
                    { genre: 'Action', percentage: 40, color: 'red-600' },
                    { genre: 'Drama', percentage: 35, color: 'blue-600' },
                    { genre: 'Epic', percentage: 25, color: 'purple-600' },
                ],
                reviewScore: { score: 95, totalVotes: 500, breakdown: [
                    { label: 'Skip', percentage: 1, color: 'red-600' },
                    { label: 'Timepass', percentage: 4, color: 'yellow-500' },
                    { label: 'Go for it', percentage: 55, color: 'green-500' },
                    { label: 'Perfection', percentage: 40, color: 'purple-600' },
                ]},
                familyFriendly: false,
            },
            'bhaag-milkha-bhaag': {
                title: 'Bhaag Milkha Bhaag', year: 2013, duration: '3h 9m', director: 'Rakeysh Omprakash Mehra', country: 'India', language: 'Hindi', ageRating: 'U/A 13+',
                posterUrl: 'https://placehold.co/400x600/f59e0b/1f2937?text=BHAAG+MILKHA',
                backgroundUrl: 'https://placehold.co/1400x700/f59e0b/1f2937?text=BHAAG+MILKHA+BHAAG+RUNNING', 
                overview: "The biographical sports drama about the life of Indian athlete Milkha Singh, who was a national champion runner and an Olympian.",
                genres: ['Biopic', 'Sports', 'Drama', 'Historical'],
                cast: [
                    { name: 'Farhan Akhtar', role: 'Milkha Singh', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=FA' },
                    { name: 'Sonam Kapoor', role: 'Biro', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=SK' },
                ],
                vibe: [
                    { genre: 'Inspiration', percentage: 50, color: 'green-500' },
                    { genre: 'Drama', percentage: 30, color: 'red-600' },
                    { genre: 'Historical', percentage: 20, color: 'slate-400' },
                ],
                reviewScore: { score: 90, totalVotes: 1800, breakdown: [
                    { label: 'Skip', percentage: 1, color: 'red-600' },
                    { label: 'Timepass', percentage: 5, color: 'yellow-500' },
                    { label: 'Go for it', percentage: 54, color: 'green-500' },
                    { label: 'Perfection', percentage: 40, color: 'purple-600' },
                ]},
                familyFriendly: true,
            },
            'pathaan': {
                title: 'Pathaan', year: 2023, duration: '2h 26m', director: 'Siddharth Anand', country: 'India', language: 'Hindi', ageRating: '16+',
                posterUrl: 'https://placehold.co/400x600/b91c1c/fef2f2?text=PATHAAN+AGENT',
                backgroundUrl: 'https://placehold.co/1400x700/7f1d1d/fef2f2?text=PATHAAN+ACTION+BACKGROUND',
                overview: "An exiled RAW agent races against time to thwart the plans of a former J.O.C. field agent turned rogue terrorist, who aims to launch a deadly attack on India.",
                genres: ['Action', 'Thriller', 'Spy', 'YRF'],
                cast: [
                    { name: 'Shah Rukh Khan', role: 'Pathaan', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=SRK' },
                    { name: 'Deepika Padukone', role: 'Rubina Mohsin', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=DP' },
                    { name: 'John Abraham', role: 'Jim', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=JA' },
                ],
                vibe: [
                    { genre: 'Action', percentage: 50, color: 'red-600' },
                    { genre: 'Suspense', percentage: 30, color: 'yellow-500' },
                    { genre: 'Thriller', percentage: 20, color: 'blue-600' },
                ],
                reviewScore: { score: 78, totalVotes: 512, breakdown: [
                    { label: 'Skip', percentage: 5, color: 'red-600' },
                    { label: 'Timepass', percentage: 15, color: 'yellow-500' },
                    { label: 'Go for it', percentage: 60, color: 'green-500' },
                    { label: 'Perfection', percentage: 20, color: 'purple-600' },
                ]},
                familyFriendly: false,
            },
            'panchayat': { 
                title: 'Panchayat', year: 2020, duration: '3 Seasons', director: 'Deepak Kumar Mishra', country: 'India', language: 'Hindi', ageRating: 'U/A 13+', 
                posterUrl: 'https://placehold.co/400x600/059669/ccfbf1?text=PANCHAYAT+S3', backgroundUrl: 'https://placehold.co/1400x700/065f46/dcfce7?text=PANCHAYAT+VILLAGE', 
                overview: "An engineering graduate takes up a job as a Secretary of a Gram Panchayat in a remote village, dealing with mundane life and hilarious local politics.", 
                genres: ['Comedy', 'Drama', 'Slice of Life', 'Web Series'], 
                cast: [{ name: 'Jitendra Kumar', role: 'Abhishek Tripathi', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=JK' }], 
                vibe: [{ genre: 'Comedy', percentage: 60, color: 'green-500' }, { genre: 'Drama', percentage: 40, color: 'blue-600' }], 
                familyFriendly: true, 
                reviewScore: { score: 90, totalVotes: 1100, breakdown: [{ label: 'Skip', percentage: 1, color: 'red-600' }, { label: 'Timepass', percentage: 5, color: 'yellow-500' }, { label: 'Go for it', percentage: 50, color: 'green-500' }, { label: 'Perfection', percentage: 44, color: 'purple-600' }],}, 
            },
            'sacred-games': { 
                title: 'Sacred Games', year: 2018, duration: '2 Seasons', director: 'Vikramaditya Motwane', country: 'India', language: 'Hindi', ageRating: '18+', 
                posterUrl: 'https://placehold.co/400x600/1e40af/bfdbfe?text=SACRED+GAMES', backgroundUrl: 'https://placehold.co/1400x700/1e3a8a/bfdbfe?text=SACRED+GAMES+BOMBAY', 
                overview: "A cynical Mumbai police officer races to save the city after receiving a mysterious phone call warning him of a catastrophic attack.", 
                genres: ['Crime', 'Thriller', 'Neo-Noir', 'Web Series'], 
                cast: [{ name: 'Saif Ali Khan', role: 'Sartaj Singh', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=SK' }],
                vibe: [{ genre: 'Thriller', percentage: 50, color: 'yellow-500' }, { genre: 'Crime', percentage: 40, color: 'red-600' }, { genre: 'Drama', percentage: 10, color: 'blue-600' }], 
                familyFriendly: false, 
                reviewScore: { score: 85, totalVotes: 945, breakdown: [{ label: 'Skip', percentage: 2, color: 'red-600' }, { label: 'Timepass', percentage: 5, color: 'yellow-500' }, { label: 'Go for it', percentage: 68, color: 'green-500' }, { label: 'Perfection', percentage: 25, color: 'purple-600' }],}, 
            },
            'uri': { 
                title: 'Uri: The Surgical Strike', year: 2019, duration: '2h 18m', director: 'Aditya Dhar', country: 'India', language: 'Hindi', ageRating: '16+', 
                posterUrl: 'https://placehold.co/400x600/15803d/dcfce7?text=URI+STRIKE', backgroundUrl: 'https://placehold.co/1400x700/065f46/dcfce7?text=URI+ARMY+ACTION', 
                overview: "The fictionalized account of the actual surgical strikes conducted by the Indian Army in retaliation for the 2016 Uri attack.", 
                genres: ['Action', 'War', 'Military', 'Historical'], 
                cast: [{ name: 'Vicky Kaushal', role: 'Major Vihan Shergill', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=VK' }],
                vibe: [{ genre: 'Action', percentage: 60, color: 'blue-600' }, { genre: 'Patriotism', percentage: 40, color: 'red-600' }], 
                familyFriendly: false, 
                reviewScore: { score: 88, totalVotes: 950, breakdown: [{ label: 'Skip', percentage: 1, color: 'red-600' }, { label: 'Timepass', percentage: 9, color: 'yellow-500' }, { label: 'Go for it', percentage: 65, color: 'green-500' }, { label: 'Perfection', percentage: 25, color: 'purple-600' }],}, 
            },
            'family-man': {
                title: 'The Family Man', year: 2019, duration: '3 Seasons', director: 'Raj & DK', country: 'India', language: 'Hindi', ageRating: '16+',
                posterUrl: 'https://placehold.co/400x600/44403c/f5f5f4?text=FAMILY+MAN+S3', backgroundUrl: 'https://placehold.co/1400x700/292524/f5f5f4?text=THE+FAMILY+MAN+ACTION+BACKGROUND',
                overview: "A highly secretive task force balances extraordinary professional demands with the complexities of ordinary family life. This high-stakes thriller is a perfect blend of intense action and poignant drama.",
                genres: ['Action', 'Thriller', 'Spy', 'Family Drama', 'Web Series'],
                cast: [
                    { name: 'Manoj Bajpayee', role: 'Srikant Tiwari', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=MB' },
                    { name: 'Priyamani', role: 'Suchi Tiwari', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=P' },
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
            'jailer': { 
                title: 'Jailer', year: 2023, duration: '2h 48m', director: 'Nelson Dilipkumar', country: 'India', language: 'Tamil', ageRating: '16+', posterUrl: 'https://placehold.co/400x600/7c3aed/f3e8ff?text=JAILER+MASS', backgroundUrl: 'https://placehold.co/1400x700/6d28d9/f3e8ff?text=JAILER+ACTION+SCENE', overview: "A retired police jailer faces the challenge of protecting his family from a dangerous criminal gang.", genres: ['Action', 'Comedy', 'Thriller'], 
                cast: [{ name: 'Rajinikanth', role: 'Muthuvel Pandian', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=R' }],
                vibe: [{ genre: 'Action', percentage: 50, color: 'blue-600' }, { genre: 'Comedy', percentage: 30, color: 'green-500' }, { genre: 'Thriller', percentage: 20, color: 'yellow-500' }],
                familyFriendly: false, 
                reviewScore: { score: 95, totalVotes: 2500, breakdown: [{ label: 'Skip', percentage: 0, color: 'red-600' }, { label: 'Timepass', percentage: 5, color: 'yellow-500' }, { label: 'Go for it', percentage: 45, color: 'green-500' }, { label: 'Perfection', percentage: 50, color: 'purple-600' }],}, 
            },
            'kantara': { 
                title: 'Kantara', year: 2022, duration: '2h 30m', director: 'Rishab Shetty', country: 'India', language: 'Kannada', ageRating: '16+', posterUrl: 'https://placehold.co/400x600/004d40/e8f5e9?text=KANTARA+RITUAL', backgroundUrl: 'https://placehold.co/1400x700/064e3b/e8f5e9?text=KANTARA+FOREST', overview: "A sub-culture's rich tradition, folklore, and land conflict set in a fictional village. A man, a spirit, and a battle for the forest.", genres: ['Action', 'Fantasy', 'Mythology'], 
                cast: [{ name: 'Rishab Shetty', role: 'Shiva', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=RS' }],
                vibe: [{ genre: 'Fantasy', percentage: 50, color: 'purple-600' }, { genre: 'Action', percentage: 50, color: 'blue-600' }],
                familyFriendly: false, 
                reviewScore: { score: 90, totalVotes: 1200, breakdown: [{ label: 'Skip', percentage: 1, color: 'red-600' }, { label: 'Timepass', percentage: 4, color: 'yellow-500' }, { label: 'Go for it', percentage: 45, color: 'green-500' }, { label: 'Perfection', percentage: 50, color: 'purple-600' }],}, 
            },
            'omg-oh-my-god': { 
                title: 'OMG - Oh My God!', year: 2012, duration: '2h 5m', director: 'Umesh Shukla', country: 'India', language: 'Hindi', ageRating: 'U', 
                posterUrl: 'https://placehold.co/300x450/f97316/ffedd5?text=OMG+GOD', backgroundUrl: 'https://placehold.co/1400x700/ea580c/ffedd5?text=OMG+COURT+SCENE', 
                overview: "A man sues God after an earthquake destroys his antique shop, leading to an unexpected confrontation with the divine.", 
                genres: ['Comedy', 'Drama', 'Fantasy', 'Social'], 
                cast: [{ name: 'Paresh Rawal', role: 'Kanji Lalji Mehta', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=PR' }], 
                vibe: [{ genre: 'Comedy', percentage: 50, color: 'green-500' }, { genre: 'Drama', percentage: 50, color: 'red-600' }], 
                familyFriendly: true, 
                reviewScore: { score: 85, totalVotes: 1500, breakdown: [{ label: 'Skip', percentage: 3, color: 'red-600' }, { label: 'Timepass', percentage: 7, color: 'yellow-500' }, { label: 'Go for it', percentage: 50, color: 'green-500' }, { label: 'Perfection', percentage: 40, color: 'purple-600' }],}, 
            },
            'drishyam': { 
                title: 'Drishyam', year: 2015, duration: '2h 43m', director: 'Nishikant Kamat', country: 'India', language: 'Hindi', ageRating: '13+', 
                posterUrl: 'https://placehold.co/300x450/374151/d1d5db?text=DRISHYAM', backgroundUrl: 'https://placehold.co/1400x700/1f2937/d1d5db?text=DRISHYAM+SUSPENSE', 
                overview: "A common man takes desperate measures to protect his family after they commit an unforeseen crime.", 
                genres: ['Crime', 'Thriller', 'Suspense', 'Family'], 
                cast: [{ name: 'Ajay Devgn', role: 'Vijay Salgaonkar', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=AD' }], 
                vibe: [{ genre: 'Thriller', percentage: 70, color: 'yellow-500' }, { genre: 'Drama', percentage: 30, color: 'red-600' }], 
                familyFriendly: false, 
                reviewScore: { score: 92, totalVotes: 1200, breakdown: [{ label: 'Skip', percentage: 1, color: 'red-600' }, { label: 'Timepass', percentage: 4, color: 'yellow-500' }, { label: 'Go for it', percentage: 45, color: 'green-500' }, { label: 'Perfection', percentage: 50, color: 'purple-600' }],}, 
            },
            'pk': { 
                title: 'PK', year: 2014, duration: '2h 33m', director: 'Rajkumar Hirani', country: 'India', language: 'Hindi', ageRating: 'U', 
                posterUrl: 'https://placehold.co/300x450/6b7280/e5e7eb?text=PK+ALIEN', backgroundUrl: 'https://placehold.co/1400x700/4b5563/e5e7eb?text=PK+SOCIETY', 
                overview: "An alien lands on Earth and is left stranded after losing his communication device. He uses his childlike curiosity to challenge religious dogma.", 
                genres: ['Sci-Fi', 'Comedy', 'Social', 'Drama'], 
                cast: [{ name: 'Aamir Khan', role: 'PK', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=AK' }], 
                vibe: [{ genre: 'Comedy', percentage: 40, color: 'green-500' }, { genre: 'Drama', percentage: 30, color: 'red-600' }, { genre: 'Social', percentage: 30, color: 'blue-600' }], 
                familyFriendly: true, 
                reviewScore: { score: 93, totalVotes: 2100, breakdown: [{ label: 'Skip', percentage: 1, color: 'red-600' }, { label: 'Timepass', percentage: 5, color: 'yellow-500' }, { label: 'Go for it', percentage: 54, color: 'green-500' }, { label: 'Perfection', percentage: 40, color: 'purple-600' }],}, 
            },
            'kabir-singh': { 
                title: 'Kabir Singh', year: 2019, duration: '2h 55m', director: 'Sandeep Reddy Vanga', country: 'India', language: 'Hindi', ageRating: '16+', 
                posterUrl: 'https://placehold.co/300x450/d946ef/f3e8ff?text=KABIR+SINGH', backgroundUrl: 'https://placehold.co/1400x700/c026d3/f3e8ff?text=KABIR+SINGH+ROMANCE', 
                overview: "A brilliant but volatile medical student descends into self-destruction after his girlfriend marries another man.", 
                genres: ['Romance', 'Drama', 'Tragedy'], 
                cast: [{ name: 'Shahid Kapoor', role: 'Kabir Singh', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=SK' }],
                reviewScore: { score: 70, totalVotes: 1800, breakdown: [{ label: 'Skip', percentage: 15, color: 'red-600' }, { label: 'Timepass', percentage: 15, color: 'yellow-500' }, { label: 'Go for it', percentage: 40, color: 'green-500' }, { label: 'Perfection', percentage: 30, color: 'purple-600' }],}, 
            },
            'dil-chahta-hai': { 
                title: 'Dil Chahta Hai', year: 2001, duration: '3h 3m', director: 'Farhan Akhtar', country: 'India', language: 'Hindi', ageRating: 'U/A 13+', 
                posterUrl: 'https://placehold.co/300x450/1e293b/f59e0b?text=DIL+CH+H', backgroundUrl: 'https://placehold.co/1400x700/000000/f59e0b?text=DCH+SYDNEY+ROAD', 
                overview: "Three inseparable childhood friends reunite after graduating college, only to find their relationships tested as they pursue diverging life paths and loves.", 
                genres: ['Coming-of-Age', 'Romance', 'Drama', 'Musical'], 
                cast: [{ name: 'Aamir Khan', role: 'Akash', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=AK' }],
                vibe: [{ genre: 'Romance', percentage: 40, color: 'pink-600' }, { genre: 'Drama', percentage: 30, color: 'red-600' }, { genre: 'Comedy', percentage: 30, color: 'green-500' }], 
                familyFriendly: true, 
                reviewScore: { score: 91, totalVotes: 850, breakdown: [{ label: 'Skip', percentage: 1, color: 'red-600' }, { label: 'Timepass', percentage: 4, color: 'yellow-500' }, { label: 'Go for it', percentage: 55, color: 'green-500' }, { label: 'Perfection', percentage: 40, color: 'purple-600' }],}, 
            },
            'kgf-chapter-1': { 
                title: 'K.G.F: Chapter 1', year: 2018, duration: '2h 35m', director: 'Prashanth Neel', country: 'India', language: 'Kannada', ageRating: '16+', 
                posterUrl: 'https://placehold.co/300x450/dc2626/fef2f2?text=KGF+CHAPTER+1', backgroundUrl: 'https://placehold.co/1400x700/991b1b/fef2f2?text=KGF+GOLD+MINE', 
                overview: "The story of Rocky, who seeks power and wealth to fulfill his dying mother's promise, leading him to the Kolar Gold Fields.", 
                genres: ['Action', 'Crime', 'Drama', 'Period'], 
                cast: [{ name: 'Yash', role: 'Rocky', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=Y' }],
                reviewScore: { score: 87, totalVotes: 1900, breakdown: [{ label: 'Skip', percentage: 1, color: 'red-600' }, { label: 'Timepass', percentage: 2, color: 'yellow-500' }, { label: 'Go for it', percentage: 57, color: 'green-500' }, { label: 'Perfection', percentage: 40, color: 'purple-600' }],}, 
            },
            'tumbbad': { 
                title: 'Tumbbad', year: 2018, duration: '1h 44m', director: 'Rahi Anil Barve', country: 'India', language: 'Hindi', ageRating: '18+', 
                posterUrl: 'https://placehold.co/300x450/065f46/d1fae5?text=TUMBBAD', backgroundUrl: 'https://placehold.co/1400x700/064e3b/d1fae5?text=TUMBBAD+RAIN', 
                overview: "A mythological horror film about a family that builds a temple for a Goddess' banished son, managing to keep a portion of his limitless gold.", 
                genres: ['Horror', 'Fantasy', 'Mythology', 'Period'], 
                cast: [{ name: 'Sohum Shah', role: 'Vinayak Rao', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=SS' }],
                vibe: [{ genre: 'Mystery', percentage: 50, color: 'yellow-500' }, { genre: 'Fantasy', percentage: 50, color: 'purple-600' }], 
                familyFriendly: false, 
                reviewScore: { score: 94, totalVotes: 700, breakdown: [{ label: 'Skip', percentage: 1, color: 'red-600' }, { label: 'Timepass', percentage: 4, color: 'yellow-500' }, { label: 'Go for it', percentage: 45, color: 'green-500' }, { label: 'Perfection', percentage: 50, color: 'purple-600' }],}, 
            },
            'dhamaal': { 
                title: 'Dhamaal', year: 2007, duration: '2h 17m', director: 'Indra Kumar', country: 'India', language: 'Hindi', ageRating: 'U/A 13+', 
                posterUrl: 'https://placehold.co/400x600/65a30d/f0fdf4?text=DHAMAAL+FUN', backgroundUrl: 'https://placehold.co/1400x700/4d7c0f/f0fdf4?text=DHAMAAL+COMEDY+ROAD', 
                overview: "Four unemployed friends race to find a hidden treasure after receiving a cryptic clue from a dying man.", 
                genres: ['Comedy', 'Adventure', 'Slapstick', 'Bollywood'], 
                cast: [{ name: 'Sanjay Dutt', role: 'Inspector Kulkarni', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=SD' }],
                vibe: [{ genre: 'Comedy', percentage: 60, color: 'green-500' }, { genre: 'Adventure', percentage: 30, color: 'blue-600' }, { genre: 'Action', percentage: 10, color: 'red-600' }], 
                familyFriendly: true, 
                reviewScore: { score: 75, totalVotes: 989, breakdown: [{ label: 'Skip', percentage: 5, color: 'red-600' }, { label: 'Timepass', percentage: 30, color: 'yellow-500' }, { label: 'Go for it', percentage: 40, color: 'green-500' }, { label: 'Perfection', percentage: 25, color: 'purple-600' }],}, 
            },
            'gangs-of-wasseypur': { 
                title: 'Gangs of Wasseypur', year: 2012, duration: '5h 20m', director: 'Anurag Kashyap', country: 'India', language: 'Hindi', ageRating: '18+', 
                posterUrl: 'https://placehold.co/300x450/1e293b/d1d5db?text=GOW+SAGA', backgroundUrl: 'https://placehold.co/1400x700/0f172a/d1d5db?text=GOW+COAL+MINE', 
                overview: "A film chronicling a violent feud over three generations for control of a coal town in Dhanbad, Jharkhand.", 
                genres: ['Crime', 'Saga', 'Action', 'Drama'], 
                cast: [{ name: 'Nawazuddin Siddiqui', role: 'Faisal Khan', img: 'https://placehold.co/100x100/1f2937/f59e0b?text=NS' }],
                vibe: [{ genre: 'Crime', percentage: 60, color: 'yellow-500' }, { genre: 'Drama', percentage: 40, color: 'red-600' }], 
                familyFriendly: false, 
                reviewScore: { score: 95, totalVotes: 1500, breakdown: [{ label: 'Skip', percentage: 1, color: 'red-600' }, { label: 'Timepass', percentage: 4, color: 'yellow-500' }, { label: 'Go for it', percentage: 45, color: 'green-500' }, { label: 'Perfection', percentage: 50, color: 'purple-600' }],}, 
            },
        };
        
        // --- WIKIPEDIA API FETCH FUNCTION ---
        const fetchWikiData = async (title) => {
            const safeTitle = title.replace(/\s/g, '_');
            const apiEndpoint = 'https://en.wikipedia.org/w/api.php';
            const params = {
                action: 'query',
                format: 'json',
                prop: 'extracts',
                titles: safeTitle,
                exintro: true,
                explaintext: true,
                redirects: 1,
                origin: '*',
            };

            const url = new URL(apiEndpoint);
            Object.keys(params).forEach(key => url.searchParams.append(key, params[key]));

            try {
                const response = await fetch(url);
                if (!response.ok) throw new Error('Network response was not ok');

                const data = await response.json();
                const pages = data.query.pages;
                const pageId = Object.keys(pages)[0];
                const page = pages[pageId];

                if (!pageId || pageId === '-1' || !page.extract) {
                    const fallbackKey = title.toLowerCase().replace(/[^a-z0-9]+/g, '-');
                    const localData = MOVIE_DATA[fallbackKey] || {};
                    return {
                        overview: `Summary not found on Wikipedia for "${title}". Displaying local plot description: ${localData.overview || 'No local description available.'}`,
                        director: localData.director || 'N/A',
                        year: localData.year || 'N/A'
                    };
                }

                let overview = page.extract.trim();
                const localKey = title.toLowerCase().replace(/[^a-z0-9]+/g, '-');
                
                // Attempt to extract the year from the overview (first occurrence)
                const yearMatch = overview.match(/\((19|20)\d{2}\)/);
                const extractedYear = yearMatch ? yearMatch[0].replace(/[\(\)]/g, '') : null;

                // Simple director fallback (full cast/director info is too complex for simple parsing)
                const director = MOVIE_DATA[localKey].director || 'N/A (Local Fallback)';

                return {
                    overview: overview,
                    director: director,
                    year: extractedYear || MOVIE_DATA[localKey].year // Prefer extracted year if found
                };

            } catch (error) {
                console.error('Error fetching Wikipedia data:', error);
                const fallbackKey = title.toLowerCase().replace(/[^a-z0-9]+/g, '-');
                const localData = MOVIE_DATA[fallbackKey] || {};
                return { 
                    overview: 'Failed to fetch details due to API error. Displaying local plot description.', 
                    director: localData.director || 'N/A',
                    year: localData.year || 'N/A'
                };
            }
        };

        // --- UTILITY FUNCTIONS ---

        // Function to generate the User Review Score Chart HTML (No changes)
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
                                <button class="text-xs font-semibold px-3 py-1 rounded-full border border-slate-700 bg-slate-800 text-gray-500 cursor-not-allowed" disabled>${item.label}</button>
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

        // Function to generate the Vibe Chart HTML (No changes)
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

        // Function to generate the Cast section HTML (No changes)
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
        
        // Function to handle movie playback (UPDATED TO SEARCH FOR TRAILER)
        const handlePlaybackClick = (title) => {
            // Changed search query to explicitly look for the trailer
            const searchQuery = `${title} official trailer YouTube`;
            const url = `https://www.youtube.com/results?search_query=${encodeURIComponent(searchQuery)}`;
            window.open(url, '_blank');
        };

        // --- MAIN ROUTING AND RENDERING (Modified) ---
        
        const goBack = () => {
            showPage('home');
        };

        const goHome = () => {
            showPage('home');
        };
        
        // Function to render a temporary loading state
        const renderLoadingState = (title) => {
            return `
                <div class="max-w-[85rem] mx-auto px-4 sm:px-6 lg:px-8 py-8 md:py-12 flex flex-col items-center justify-center min-h-[60vh] text-indi-accent">
                    <div class="animate-spin rounded-full h-16 w-16 border-t-2 border-b-2 border-indi-accent mb-4"></div>
                    <p class="text-xl font-semibold">Loading details for "${title}" from Wikipedia...</p>
                </div>
            `;
        }

        const renderDetailPage = async (movieKey) => {
            const data = MOVIE_DATA[movieKey];
            if (!data) return;

            document.getElementById('detail-view').classList.remove('hidden');
            document.getElementById('detail-view').innerHTML = renderLoadingState(data.title);
            document.getElementById('detail-view').setAttribute('data-current-movie', movieKey);
            document.title = data.title + ' | Indiwood';

            // 1. Fetch live data for Overview/Year/Director
            const wikiData = await fetchWikiData(data.title);
            
            // 2. Overwrite mutable fields with live data
            data.overview = wikiData.overview;
            data.director = wikiData.director;
            data.year = wikiData.year;


            // 3. Regenerate HTML with fetched data
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
                                <p class="text-sm font-light text-gray-300 mb-1">Movie • <span class="text-white font-semibold">${data.year}</span> • ${data.duration}</p>
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
                                    <button onclick="handlePlaybackClick('${data.title}')" class="flex items-center justify-center space-x-2 bg-indi-accent hover:bg-amber-600 text-slate-900 font-bold py-3 px-6 rounded-full transition duration-300 shadow-xl">
                                        <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" d="M5.25 5.653c0-.856.917-1.398 1.667-.986l11.54 6.348a1.125 1.125 0 010 1.972l-11.54 6.347a1.125 1.125 0 01-1.667-.985V5.653z" /></svg>
                                        <span>Watch Trailer on YouTube</span>
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
                                <h2 class="text-2xl font-bold mb-4">Overview (Source: Wikipedia)</h2>
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
                // Call async render function
                renderDetailPage(movieKey); 
                // Detail view is unhidden inside renderDetailPage after setting loading state
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
