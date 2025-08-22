<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MusicStream - Spotify Clone</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;700&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Montserrat', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #121212 0%, #1a1a1a 100%);
            color: #ffffff;
            min-height: 100vh;
        }
        
        .sidebar {
            background: #000000;
            height: 100vh;
            position: fixed;
            width: 240px;
        }
        
        .main-content {
            margin-left: 240px;
            padding-bottom: 100px;
        }
        
        .player {
            background: linear-gradient(90deg, #181818 0%, #282828 100%);
            position: fixed;
            bottom: 0;
            width: 100%;
            height: 90px;
            border-top: 1px solid #282828;
        }
        
        .album-art {
            transition: transform 0.3s ease;
        }
        
        .album-art:hover {
            transform: scale(1.05);
        }
        
        .progress-bar {
            background: #5e5e5e;
            height: 4px;
            border-radius: 2px;
            cursor: pointer;
        }
        
        .progress {
            background: #1db954;
            height: 100%;
            border-radius: 2px;
            width: 30%;
        }
        
        .song-item:hover {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 4px;
        }
        
        .playing {
            color: #1db954;
        }
        
        @media (max-width: 768px) {
            .sidebar {
                width: 80px;
            }
            
            .main-content {
                margin-left: 80px;
            }
            
            .sidebar-text {
                display: none;
            }
        }
    </style>
</head>
<body class="flex">
    <!-- Sidebar -->
    <div class="sidebar p-6">
        <div class="mb-10">
            <div class="flex items-center text-2xl font-bold text-white">
                <i class="fas fa-music text-green-500 mr-3"></i>
                <span class="sidebar-text">MusicStream</span>
            </div>
        </div>
        
        <nav class="mb-8">
            <ul class="space-y-4">
                <li>
                    <a href="#" class="flex items-center text-gray-300 hover:text-white transition-colors">
                        <i class="fas fa-home w-6"></i>
                        <span class="sidebar-text ml-4">Beranda</span>
                    </a>
                </li>
                <li>
                    <a href="#" class="flex items-center text-gray-300 hover:text-white transition-colors">
                        <i class="fas fa-search w-6"></i>
                        <span class="sidebar-text ml-4">Cari</span>
                    </a>
                </li>
                <li>
                    <a href="#" class="flex items-center text-gray-300 hover:text-white transition-colors">
                        <i class="fas fa-book-open w-6"></i>
                        <span class="sidebar-text ml-4">Koleksi Anda</span>
                    </a>
                </li>
            </ul>
        </nav>
        
        <div class="mb-8">
            <h3 class="text-gray-400 uppercase text-xs font-bold mb-4 sidebar-text">Playlist</h3>
            <ul class="space-y-3">
                <li>
                    <a href="#" class="flex items-center text-gray-300 hover:text-white transition-colors text-sm">
                        <i class="fas fa-plus-circle w-6"></i>
                        <span class="sidebar-text ml-4">Buat Playlist</span>
                    </a>
                </li>
                <li>
                    <a href="#" class="flex items-center text-gray-300 hover:text-white transition-colors text-sm">
                        <i class="fas fa-heart text-purple-500 w-6"></i>
                        <span class="sidebar-text ml-4">Lagu Disukai</span>
                    </a>
                </li>
            </ul>
        </div>
        
        <div class="border-t border-gray-800 pt-6">
            <h3 class="text-gray-400 uppercase text-xs font-bold mb-4 sidebar-text">Playlist Anda</h3>
            <ul class="space-y-2">
                <li><a href="#" class="text-gray-300 hover:text-white transition-colors text-sm block sidebar-text">Rock Classics</a></li>
                <li><a href="#" class="text-gray-300 hover:text-white transition-colors text-sm block sidebar-text">Chill Vibes</a></li>
                <li><a href="#" class="text-gray-300 hover:text-white transition-colors text-sm block sidebar-text">Workout Mix</a></li>
                <li><a href="#" class="text-gray-300 hover:text-white transition-colors text-sm block sidebar-text">Study Focus</a></li>
            </ul>
        </div>
    </div>

    <!-- Main Content -->
    <div class="main-content flex-1 p-8">
        <header class="mb-8">
            <div class="flex justify-between items-center">
                <div class="flex space-x-4">
                    <button class="bg-black bg-opacity-30 rounded-full p-2 w-10 h-10 flex items-center justify-center hover:bg-opacity-50 transition">
                        <i class="fas fa-chevron-left"></i>
                    </button>
                    <button class="bg-black bg-opacity-30 rounded-full p-2 w-10 h-10 flex items-center justify-center hover:bg-opacity-50 transition">
                        <i class="fas fa-chevron-right"></i>
                    </button>
                </div>
                <div class="flex items-center space-x-4">
                    <button class="bg-white text-black px-6 py-2 rounded-full text-sm font-bold hover:scale-105 transition">Upgrade</button>
                    <div class="flex items-center bg-black bg-opacity-30 rounded-full p-1 pr-4 cursor-pointer hover:bg-opacity-50 transition">
                        <div class="w-8 h-8 rounded-full bg-purple-500 flex items-center justify-center mr-2">
                            <i class="fas fa-user text-white text-sm"></i>
                        </div>
                        <span class="text-sm font-medium">User Name</span>
                    </div>
                </div>
            </div>
        </header>

        <section class="mb-10">
            <h1 class="text-3xl font-bold mb-6">Selamat datang kembali</h1>
            
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
                <div class="bg-gradient-to-br from-purple-900 to-blue-800 p-6 rounded-lg cursor-pointer hover:from-purple-800 hover:to-blue-700 transition">
                    <div class="flex items-center mb-4">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/395664cd-b8df-48c8-8ff1-1c1c97b281b9.png" alt="Album cover dengan desain gradient ungu dan biru untuk musik pop Indonesia" class="w-16 h-16 rounded mr-4">
                        <h3 class="font-bold">Lagu Pop Indonesia</h3>
                    </div>
                    <p class="text-gray-300 text-sm">Dengarkan hits terbaru dari artis Indonesia</p>
                </div>
                
                <div class="bg-gradient-to-br from-green-900 to-emerald-800 p-6 rounded-lg cursor-pointer hover:from-green-800 hover:to-emerald-700 transition">
                    <div class="flex items-center mb-4">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/0f3ee6e3-9600-46ee-bf86-971a747efddb.png" alt="Album cover hijau dengan elemen alam untuk musik relaksasi" class="w-16 h-16 rounded mr-4">
                        <h3 class="font-bold">Relax & Chill</h3>
                    </div>
                    <p class="text-gray-300 text-sm">Musik santai untuk menemani hari Anda</p>
                </div>
                
                <div class="bg-gradient-to-br from-red-900 to-orange-800 p-6 rounded-lg cursor-pointer hover:from-red-800 hover:to-orange-700 transition">
                    <div class="flex items-center mb-4">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/4f9ae170-da17-4463-9f8c-ff68bdeb6b1d.png" alt="Album cover merah dan oranye dengan energi tinggi untuk musik workout" class="w-16 h-16 rounded mr-4">
                        <h3 class="font-bold">Workout Energy</h3>
                    </div>
                    <p class="text-gray-300 text-sm">Tingkatkan energi latihan dengan beat yang kuat</p>
                </div>
                
                <div class="bg-gradient-to-br from-blue-900 to-indigo-800 p-6 rounded-lg cursor-pointer hover:from-blue-800 hover:to-indigo-700 transition">
                    <div class="flex items-center mb-4">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/2b39e559-ec15-4804-bb1a-633c6881531e.png" alt="Album cover biru dengan suasana fokus untuk musik belajar" class="w-16 h-16 rounded mr-4">
                        <h3 class="font-bold">Focus Study</h3>
                    </div>
                    <p class="text-gray-300 text-sm">Musik untuk meningkatkan konsentrasi belajar</p>
                </div>
            </div>
        </section>

        <section class="mb-10">
            <div class="flex justify-between items-center mb-6">
                <h2 class="text-2xl font-bold">Lagu untuk Anda</h2>
                <a href="#" class="text-gray-400 text-sm font-bold hover:underline">TAMPILKAN SEMUA</a>
            </div>
            
            <div class="bg-gray-800 bg-opacity-50 rounded-lg p-4">
                <table class="w-full text-gray-300">
                    <thead>
                        <tr class="border-b border-gray-700">
                            <th class="text-left pb-3 text-sm font-normal">#</th>
                            <th class="text-left pb-3 text-sm font-normal">JUDUL</th>
                            <th class="text-left pb-3 text-sm font-normal">ALBUM</th>
                            <th class="text-left pb-3 text-sm font-normal"><i class="far fa-clock"></i></th>
                        </tr>
                    </thead>
                    <tbody class="song-list">
                        <tr class="song-item h-14 border-b border-gray-700 hover:bg-gray-700 cursor-pointer" data-song="1">
                            <td class="w-10 text-center"><span class="song-number">1</span><i class="fas fa-play playing hidden"></i></td>
                            <td>
                                <div class="flex items-center">
                                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/ec0f57e0-626a-4860-84cf-1ebb157a2461.png" alt="Cover album dengan desain urban modern untuk lagu Rhythm of the Night" class="w-10 h-10 mr-3 rounded">
                                    <div>
                                        <div class="font-medium">Rhythm of the Night</div>
                                        <div class="text-sm text-gray-400">Aurora Lights</div>
                                    </div>
                                </div>
                            </td>
                            <td class="text-sm">Urban Dreams</td>
                            <td class="text-sm">3:45</td>
                        </tr>
                        <tr class="song-item h-14 border-b border-gray-700 hover:bg-gray-700 cursor-pointer" data-song="2">
                            <td class="w-10 text-center"><span class="song-number">2</span><i class="fas fa-play playing hidden"></i></td>
                            <td>
                                <div class="flex items-center">
                                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/eb611da2-ee4d-496d-9e0c-5f3fb2807dd2.png" alt="Cover album dengan tema malam kota untuk lagu Midnight City" class="w-10 h-10 mr-3 rounded">
                                    <div>
                                        <div class="font-medium">Midnight City</div>
                                        <div class="text-sm text-gray-400">Urban Echo</div>
                                    </div>
                                </div>
                            </td>
                            <td class="text-sm">City Lights</td>
                            <td class="text-sm">4:12</td>
                        </tr>
                        <tr class="song-item h-14 border-b border-gray-700 hover:bg-gray-700 cursor-pointer" data-song="3">
                            <td class="w-10 text-center"><span class="song-number">3</span><i class="fas fa-play playing hidden"></i></td>
                            <td>
                                <div class="flex items-center">
                                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/ed0c90b0-9b63-4b96-bf64-9b6c28b0fe30.png" alt="Cover album dengan pantai sunset untuk lagu Ocean Breeze" class="w-10 h-10 mr-3 rounded">
                                    <div>
                                        <div class="font-medium">Ocean Breeze</div>
                                        <div class="text-sm text-gray-400">Coastal Waves</div>
                                    </div>
                                </div>
                            </td>
                            <td class="text-sm">Summer Vibes</td>
                            <td class="text-sm">3:28</td>
                        </tr>
                        <tr class="song-item h-14 border-b border-gray-700 hover:bg-gray-700 cursor-pointer" data-song="4">
                            <td class="w-10 text-center"><span class="song-number">4</span><i class="fas fa-play playing hidden"></i></td>
                            <td>
                                <div class="flex items-center">
                                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/a182e4d4-49b2-4250-b26b-c332a3674b20.png" alt="Cover album dengan tema hutan untuk lagu Forest Echo" class="w-10 h-10 mr-3 rounded">
                                    <div>
                                        <div class="font-medium">Forest Echo</div>
                                        <div class="text-sm text-gray-400">Nature Sounds</div>
                                    </div>
                                </div>
                            </td>
                            <td class="text-sm">Natural Harmony</td>
                            <td class="text-sm">5:17</td>
                        </tr>
                        <tr class="song-item h-14 hover:bg-gray-700 cursor-pointer" data-song="5">
                            <td class="w-10 text-center"><span class="song-number">5</span><i class="fas fa-play playing hidden"></i></td>
                            <td>
                                <div class="flex items-center">
                                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/ee559bfb-524a-4448-8b60-b1d7ee5a1d81.png" alt="Cover album dengan desain futuristik untuk lagu Digital Dreams" class="w-10 h-10 mr-3 rounded">
                                    <div>
                                        <div class="font-medium">Digital Dreams</div>
                                        <div class="text-sm text-gray-400">Tech Beats</div>
                                    </div>
                                </div>
                            </td>
                            <td class="text-sm">Future Sound</td>
                            <td class="text-sm">3:55</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </section>

        <section>
            <h2 class="text-2xl font-bold mb-6">Album baru untuk Anda</h2>
            
            <div class="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-6 gap-6">
                <div class="cursor-pointer group">
                    <div class="relative mb-3">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/b6ae0e33-36a6-4f7f-af19-6bea72f5013d.png" alt="Cover album dengan desain abstrak warna-warni untuk album Color Theory" class="w-full rounded shadow-lg album-art">
                        <button class="absolute bottom-2 right-2 bg-green-500 w-10 h-10 rounded-full flex items-center justify-center shadow-lg opacity-0 group-hover:opacity-100 transition-opacity hover:scale-105">
                            <i class="fas fa-play text-black"></i>
                        </button>
                    </div>
                    <h3 class="font-bold text-sm truncate">Color Theory</h3>
                    <p class="text-gray-400 text-sm">Various Artists</p>
                </div>
                
                <div class="cursor-pointer group">
                    <div class="relative mb-3">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/92b71478-3b6b-4bb0-b7b5-06fc48a45da0.png" alt="Cover album dengan tema malam perkotaan untuk album Night Drive" class="w-full rounded shadow-lg album-art">
                        <button class="absolute bottom-2 right-2 bg-green-500 w-10 h-10 rounded-full flex items-center justify-center shadow-lg opacity-0 group-hover:opacity-100 transition-opacity hover:scale-105">
                            <i class="fas fa-play text-black"></i>
                        </button>
                    </div>
                    <h3 class="font-bold text-sm truncate">Night Drive</h3>
                    <p class="text-gray-400 text-sm">City Vibes</p>
                </div>
                
                <div class="cursor-pointer group">
                    <div class="relative mb-3">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/a84a3eb7-7ac0-44c0-bbe1-407a0a796854.png" alt="Cover album dengan ilustrasi tanaman tropis untuk album Tropical Escape" class="w-full rounded shadow-lg album-art">
                        <button class="absolute bottom-2 right-2 bg-green-500 w-10 h-10 rounded-full flex items-center justify-center shadow-lg opacity-0 group-hover:opacity-100 transition-opacity hover:scale-105">
                            <i class="fas fa-play text-black"></i>
                        </button>
                    </div>
                    <h3 class="font-bold text-sm truncate">Tropical Escape</h3>
                    <p class="text-gray-400 text-sm">Island Beats</p>
                </div>
                
                <div class="cursor-pointer group">
                    <div class="relative mb-3">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/251df618-63cf-430e-84f8-eb974968724b.png" alt="Cover album dengan desain minimalis elegan untuk album Pure Essence" class="w-full rounded shadow-lg album-art">
                        <button class="absolute bottom-2 right-2 bg-green-500 w-10 h-10 rounded-full flex items-center justify-center shadow-lg opacity-0 group-hover:opacity-100 transition-opacity hover:scale-105">
                            <i class="fas fa-play text-black"></i>
                        </button>
                    </div>
                    <h3 class="font-bold text-sm truncate">Pure Essence</h3>
                    <p class="text-gray-400 text-sm">Minimal Sounds</p>
                </div>
                
                <div class="cursor-pointer group">
                    <div class="relative mb-3">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/ae917bee-04ac-4fce-a9e6-d2ee5bd113c5.png" alt="Cover album dengan tema vintage retro untuk album Retro Revival" class="w-full rounded shadow-lg album-art">
                        <button class="absolute bottom-2 right-2 bg-green-500 w-10 h-10 rounded-full flex items-center justify-center shadow-lg opacity-0 group-hover:opacity-100 transition-opacity hover:scale-105">
                            <i class="fas fa-play text-black"></i>
                        </button>
                    </div>
                    <h3 class="font-bold text-sm truncate">Retro Revival</h3>
                    <p class="text-gray-400 text-sm">Old School</p>
                </div>
                
                <div class="cursor-pointer group">
                    <div class="relative mb-3">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/9a028e32-7fe2-4280-930d-d376ddbc7097.png" alt="Cover album dengan ilustrasi gunung dan langit untuk album Mountain High" class="w-full rounded shadow-lg album-art">
                        <button class="absolute bottom-2 right-2 bg-green-500 w-10 h-10 rounded-full flex items-center justify-center shadow-lg opacity-0 group-hover:opacity-100 transition-opacity hover:scale-105">
                            <i class="fas fa-play text-black"></i>
                        </button>
                    </div>
                    <h3 class="font-bold text-sm truncate">Mountain High</h3>
                    <p class="text-gray-400 text-sm">Nature Tunes</p>
                </div>
            </div>
        </section>
    </div>

    <!-- Player -->
    <div class="player flex items-center justify-between px-4">
        <div class="flex items-center w-1/4">
            <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/40f5e05d-1ead-4a98-a34a-38e8ad0a58e7.png" alt="Cover album yang sedang diputar dengan desain musik modern" class="w-14 h-14 rounded mr-3" id="current-song-image">
            <div>
                <div class="text-sm font-medium" id="current-song-title">Rhythm of the Night</div>
                <div class="text-xs text-gray-400" id="current-song-artist">Aurora Lights</div>
            </div>
            <button class="ml-4 text-gray-400 hover:text-white">
                <i class="far fa-heart"></i>
            </button>
        </div>
        
        <div class="flex flex-col items-center w-2/4">
            <div class="flex items-center space-x-6 mb-2">
                <button class="text-gray-400 hover:text-white" id="shuffle">
                    <i class="fas fa-random"></i>
                </button>
                <button class="text-gray-400 hover:text-white" id="prev">
                    <i class="fas fa-step-backward"></i>
                </button>
                <button class="bg-white rounded-full w-8 h-8 flex items-center justify-center hover:scale-105 transition" id="play-pause">
                    <i class="fas fa-play text-black" id="play-icon"></i>
                </button>
                <button class="text-gray-400 hover:text-white" id="next">
                    <i class="fas fa-step-forward"></i>
                </button>
                <button class="text-gray-400 hover:text-white" id="repeat">
                    <i class="fas fa-redo"></i>
                </button>
            </div>
            <div class="w-full flex items-center space-x-2">
                <span class="text-xs text-gray-400" id="current-time">0:00</span>
                <div class="progress-bar flex-1" id="progress-container">
                    <div class="progress" id="progress"></div>
                </div>
                <span class="text-xs text-gray-400" id="duration">3:45</span>
            </div>
        </div>
        
        <div class="flex items-center justify-end w-1/4 space-x-3">
            <button class="text-gray-400 hover:text-white">
                <i class="fas fa-list"></i>
            </button>
            <button class="text-gray-400 hover:text-white">
                <i class="fas fa-laptop"></i>
            </button>
            <div class="flex items-center space-x-1">
                <button class="text-gray-400 hover:text-white">
                    <i class="fas fa-volume-down"></i>
                </button>
                <div class="w-20 bg-gray-600 rounded-full h-1">
                    <div class="bg-white h-1 rounded-full" style="width: 70%"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- Audio Element -->
    <audio id="audio-player"></audio>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Song data
            const songs = [
                {
                    title: "Rhythm of the Night",
                    artist: "Aurora Lights",
                    album: "Urban Dreams",
                    duration: "3:45",
                    image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/e09b3490-aee0-47fc-9d37-ead61ef47a4c.png",
                    file: "https://cdn.pixabay.com/download/audio/2022/01/20/audio_d16713dc98.mp3?filename=electronic-rock-king-around-here-15045.mp3"
                },
                {
                    title: "Midnight City",
                    artist: "Urban Echo",
                    album: "City Lights",
                    duration: "4:12",
                    image: "https://placehold.co/40x40",
                    file: "https://cdn.pixabay.com/download/audio/2022/03/15/audio_5bdcb6f9e1.mp3?filename=cinematic-documentary-piano-118527.mp3"
                },
                {
                    title: "Ocean Breeze",
                    artist: "Coastal Waves",
                    album: "Summer Vibes",
                    duration: "3:28",
                    image: "https://placehold.co/40x40",
                    file: "https://cdn.pixabay.com/download/audio/2022/10/25/audio_326d2c8c0c.mp3?filename=epic-cinematic-trailer-112623.mp3"
                },
                {
                    title: "Forest Echo",
                    artist: "Nature Sounds",
                    album: "Natural Harmony",
                    duration: "5:17",
                    image: "https://placehold.co/40x40",
                    file: "https://cdn.pixabay.com/download/audio/2022/05/27/audio_7b607246f3.mp3?filename=cinematic-inspiring-124128.mp3"
                },
                {
                    title: "Digital Dreams",
                    artist: "Tech Beats",
                    album: "Future Sound",
                    duration: "3:55",
                    image: "https://placehold.co/40x40",
                    file: "https://cdn.pixabay.com/download/audio/2022/01/18/audio_7b13d2b7c8.mp3?filename=cinematic-trailer-115677.mp3"
                }
            ];

            // Player elements
            const audioPlayer = document.getElementById('audio-player');
            const playPauseBtn = document.getElementById('play-pause');
            const playIcon = document.getElementById('play-icon');
            const prevBtn = document.getElementById('prev');
            const nextBtn = document.getElementById('next');
            const progress = document.getElementById('progress');
            const progressContainer = document.getElementById('progress-container');
            const currentTimeEl = document.getElementById('current-time');
            const durationEl = document.getElementById('duration');
            const currentSongTitle = document.getElementById('current-song-title');
            const currentSongArtist = document.getElementById('current-song-artist');
            const currentSongImage = document.getElementById('current-song-image');
            const songItems = document.querySelectorAll('.song-item');

            // Player state
            let currentSongIndex = 0;
            let isPlaying = false;

            // Load song
            function loadSong(index) {
                const song = songs[index];
                audioPlayer.src = song.file;
                currentSongTitle.textContent = song.title;
                currentSongArtist.textContent = song.artist;
                currentSongImage.src = song.image;
                durationEl.textContent = song.duration;
                
                // Update song list UI
                songItems.forEach((item, i) => {
                    const number = item.querySelector('.song-number');
                    const playIcon = item.querySelector('.playing');
                    if (i === index) {
                        number.classList.add('hidden');
                        playIcon.classList.remove('hidden');
                        item.classList.add('bg-gray-700');
                    } else {
                        number.classList.remove('hidden');
                        playIcon.classList.add('hidden');
                        item.classList.remove('bg-gray-700');
                    }
                });
            }

            // Play song
            function playSong() {
                isPlaying = true;
                playIcon.classList.remove('fa-play');
                playIcon.classList.add('fa-pause');
                audioPlayer.play();
            }

            // Pause song
            function pauseSong() {
                isPlaying = false;
                playIcon.classList.remove('fa-pause');
                playIcon.classList.add('fa-play');
                audioPlayer.pause();
            }

            // Previous song
            function prevSong() {
                currentSongIndex--;
                if (currentSongIndex < 0) {
                    currentSongIndex = songs.length - 1;
                }
                loadSong(currentSongIndex);
                if (isPlaying) playSong();
            }

            // Next song
            function nextSong() {
                currentSongIndex++;
                if (currentSongIndex > songs.length - 1) {
                    currentSongIndex = 0;
                }
                loadSong(currentSongIndex);
                if (isPlaying) playSong();
            }

            // Update progress bar
            function updateProgress(e) {
                const { duration, currentTime } = e.srcElement;
                if (duration) {
                    // Update progress bar width
                    const progressPercent = (currentTime / duration) * 100;
                    progress.style.width = `${progressPercent}%`;
                    
                    // Calculate display for duration
                    let durationMinutes = Math.floor(duration / 60);
                    let durationSeconds = Math.floor(duration % 60);
                    if (durationSeconds < 10) {
                        durationSeconds = `0${durationSeconds}`;
                    }
                    
                    // Calculate display for currentTime
                    let currentMinutes = Math.floor(currentTime / 60);
                    let currentSeconds = Math.floor(currentTime % 60);
                    if (currentSeconds < 10) {
                        currentSeconds = `0${currentSeconds}`;
                    }
                    
                    // Avoid NaN
                    if (currentSeconds) {
                        currentTimeEl.textContent = `${currentMinutes}:${currentSeconds}`;
                    }
                }
            }

            // Set progress bar
            function setProgress(e) {
                const width = this.clientWidth;
                const clickX = e.offsetX;
                const duration = audioPlayer.duration;
                audioPlayer.currentTime = (clickX / width) * duration;
            }

            // Event listeners
            playPauseBtn.addEventListener('click', () => {
                isPlaying ? pauseSong() : playSong();
            });

            prevBtn.addEventListener('click', prevSong);
            nextBtn.addEventListener('click', nextSong);

            audioPlayer.addEventListener('timeupdate', updateProgress);
            audioPlayer.addEventListener('ended', nextSong);

            progressContainer.addEventListener('click', setProgress);

            // Song item click
            songItems.forEach((item, index) => {
                item.addEventListener('click', () => {
                    currentSongIndex = index;
                    loadSong(currentSongIndex);
                    playSong();
                });
            });

            // Initialize
            loadSong(currentSongIndex);
        });
    </script>
</body>
</html>

