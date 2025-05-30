<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JM - Conecte-se com o mundo</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        /* Custom styles that can't be done with Tailwind */
        .story-ring {
            background: linear-gradient(45deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888);
        }
        .post-image {
            aspect-ratio: 1/1;
        }
        .message-bubble {
            max-width: 70%;
        }
        .reel-video {
            height: 80vh;
            width: 100%;
            max-width: 350px;
        }
        .active-tab {
            border-bottom: 2px solid black;
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 5px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #f1f1f1;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #888;
            border-radius: 10px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover {
            background: #555;
        }
    </style>
</head>
<body class="bg-gray-50 font-sans">
    <!-- Login Screen (Initial View) -->
    <div id="login-screen" class="min-h-screen flex flex-col items-center justify-center p-4">
        <div class="w-full max-w-md bg-white rounded-lg shadow-md p-8">
            <div class="text-center mb-8">
                <h1 class="text-3xl font-bold text-gray-800">JM</h1>
                <p class="text-gray-600 mt-2">Conecte-se com amigos e compartilhe seu mundo</p>
            </div>
            
            <form id="login-form" class="space-y-4">
                <div>
                    <input type="text" id="username" placeholder="Nome de usuário, email ou telefone" 
                           class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                <div>
                    <input type="password" id="password" placeholder="Senha" 
                           class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                <button type="submit" class="w-full bg-blue-500 text-white py-2 rounded-md hover:bg-blue-600 transition duration-200">
                    Entrar
                </button>
            </form>
            
            <div class="flex items-center my-6">
                <div class="flex-grow border-t border-gray-300"></div>
                <span class="mx-4 text-gray-500">OU</span>
                <div class="flex-grow border-t border-gray-300"></div>
            </div>
            
            <div class="text-center">
                <a href="#" class="text-blue-500 text-sm font-medium">Entrar com Facebook</a>
                <p class="mt-6 text-sm">
                    <a href="#" class="text-blue-500">Esqueceu a senha?</a>
                </p>
            </div>
        </div>
        
        <div class="w-full max-w-md bg-white rounded-lg shadow-md p-6 mt-4 text-center">
            <p class="text-gray-700">Não tem uma conta? <a href="#" id="show-signup" class="text-blue-500 font-medium">Cadastre-se</a></p>
        </div>
    </div>
    
    <!-- Signup Screen (Hidden Initially) -->
    <div id="signup-screen" class="min-h-screen flex flex-col items-center justify-center p-4 hidden">
        <div class="w-full max-w-md bg-white rounded-lg shadow-md p-8">
            <div class="text-center mb-6">
                <h1 class="text-3xl font-bold text-gray-800">JM</h1>
                <p class="text-gray-600 mt-2">Cadastre-se para ver fotos e vídeos dos seus amigos</p>
            </div>
            
            <form id="signup-form" class="space-y-4">
                <div>
                    <input type="email" id="signup-email" placeholder="Email" 
                           class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                <div>
                    <input type="text" id="signup-fullname" placeholder="Nome completo" 
                           class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                <div>
                    <input type="text" id="signup-username" placeholder="Nome de usuário" 
                           class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                <div>
                    <input type="password" id="signup-password" placeholder="Senha" 
                           class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                <button type="submit" class="w-full bg-blue-500 text-white py-2 rounded-md hover:bg-blue-600 transition duration-200">
                    Cadastre-se
                </button>
            </form>
            
            <p class="mt-4 text-xs text-gray-500">
                Ao se cadastrar, você concorda com nossos Termos, Política de Dados e Política de Cookies.
            </p>
            
            <div class="text-center mt-6">
                <p class="text-gray-700">Já tem uma conta? <a href="#" id="show-login" class="text-blue-500 font-medium">Conecte-se</a></p>
            </div>
        </div>
    </div>
    
    <!-- Main App (Hidden Initially) -->
    <div id="main-app" class="hidden">
        <!-- Header -->
        <header class="bg-white border-b border-gray-200 fixed top-0 left-0 right-0 z-10">
            <div class="max-w-5xl mx-auto px-4 py-2 flex items-center justify-between">
                <h1 class="text-2xl font-bold">JM</h1>
                
                <div class="relative w-1/3 max-w-xs">
                    <input type="text" placeholder="Pesquisar" 
                           class="w-full bg-gray-100 rounded-md py-1 px-4 pl-10 text-sm focus:outline-none focus:ring-1 focus:ring-gray-300">
                    <i class="fas fa-search absolute left-3 top-2 text-gray-400"></i>
                </div>
                
                <div class="flex items-center space-x-5">
                    <button id="home-btn">
                        <i class="fas fa-home text-2xl"></i>
                    </button>
                    <button id="message-btn">
                        <i class="fas fa-paper-plane text-2xl"></i>
                    </button>
                    <button id="create-btn">
                        <i class="far fa-plus-square text-2xl"></i>
                    </button>
                    <button id="explore-btn">
                        <i class="far fa-compass text-2xl"></i>
                    </button>
                    <button id="reels-btn">
                        <i class="fas fa-film text-2xl"></i>
                    </button>
                    <div class="w-8 h-8 rounded-full bg-gray-300 overflow-hidden">
                        <img src="https://randomuser.me/api/portraits/women/44.jpg" alt="Profile" class="w-full h-full object-cover">
                    </div>
                </div>
            </div>
        </header>
        
        <!-- Main Content -->
        <main class="pt-16 pb-16 max-w-5xl mx-auto flex">
            <!-- Feed Section -->
            <div id="feed-section" class="w-full md:w-2/3">
                <!-- Stories -->
                <div class="bg-white border border-gray-200 rounded-md p-4 mb-4 overflow-x-auto">
                    <div class="flex space-x-4">
                        <!-- Your Story -->
                        <div class="flex flex-col items-center space-y-1">
                            <div class="w-16 h-16 rounded-full p-0.5 story-ring">
                                <div class="w-full h-full rounded-full bg-white p-0.5 flex items-center justify-center">
                                    <div class="w-full h-full rounded-full bg-gray-200 overflow-hidden">
                                        <img src="https://randomuser.me/api/portraits/women/44.jpg" alt="Your story" class="w-full h-full object-cover">
                                    </div>
                                </div>
                            </div>
                            <span class="text-xs truncate w-16 text-center">Seu story</span>
                        </div>
                        
                        <!-- Other Stories -->
                        <div class="flex flex-col items-center space-y-1">
                            <div class="w-16 h-16 rounded-full p-0.5 story-ring">
                                <div class="w-full h-full rounded-full bg-white p-0.5">
                                    <div class="w-full h-full rounded-full bg-gray-200 overflow-hidden">
                                        <img src="https://randomuser.me/api/portraits/men/32.jpg" alt="Story" class="w-full h-full object-cover">
                                    </div>
                                </div>
                            </div>
                            <span class="text-xs truncate w-16 text-center">marcos_22</span>
                        </div>
                        
                        <div class="flex flex-col items-center space-y-1">
                            <div class="w-16 h-16 rounded-full p-0.5 story-ring">
                                <div class="w-full h-full rounded-full bg-white p-0.5">
                                    <div class="w-full h-full rounded-full bg-gray-200 overflow-hidden">
                                        <img src="https://randomuser.me/api/portraits/women/65.jpg" alt="Story" class="w-full h-full object-cover">
                                    </div>
                                </div>
                            </div>
                            <span class="text-xs truncate w-16 text-center">ana_clara</span>
                        </div>
                        
                        <div class="flex flex-col items-center space-y-1">
                            <div class="w-16 h-16 rounded-full p-0.5 story-ring">
                                <div class="w-full h-full rounded-full bg-white p-0.5">
                                    <div class="w-full h-full rounded-full bg-gray-200 overflow-hidden">
                                        <img src="https://randomuser.me/api/portraits/men/75.jpg" alt="Story" class="w-full h-full object-cover">
                                    </div>
                                </div>
                            </div>
                            <span class="text-xs truncate w-16 text-center">pedro_hs</span>
                        </div>
                        
                        <div class="flex flex-col items-center space-y-1">
                            <div class="w-16 h-16 rounded-full p-0.5 story-ring">
                                <div class="w-full h-full rounded-full bg-white p-0.5">
                                    <div class="w-full h-full rounded-full bg-gray-200 overflow-hidden">
                                        <img src="https://randomuser.me/api/portraits/women/33.jpg" alt="Story" class="w-full h-full object-cover">
                                    </div>
                                </div>
                            </div>
                            <span class="text-xs truncate w-16 text-center">julia_aa</span>
                        </div>
                    </div>
                </div>
                
                <!-- Posts -->
                <div class="space-y-6">
                    <!-- Post 1 -->
                    <div class="bg-white border border-gray-200 rounded-md">
                        <!-- Post Header -->
                        <div class="flex items-center justify-between p-3">
                            <div class="flex items-center space-x-2">
                                <div class="w-8 h-8 rounded-full overflow-hidden">
                                    <img src="https://randomuser.me/api/portraits/men/32.jpg" alt="User" class="w-full h-full object-cover">
                                </div>
                                <span class="font-medium">marcos_22</span>
                            </div>
                            <button>
                                <i class="fas fa-ellipsis-h"></i>
                            </button>
                        </div>
                        
                        <!-- Post Image -->
                        <div class="post-image bg-gray-100">
                            <img src="https://source.unsplash.com/random/600x600/?nature" alt="Post" class="w-full h-full object-cover">
                        </div>
                        
                        <!-- Post Actions -->
                        <div class="p-3">
                            <div class="flex justify-between mb-2">
                                <div class="flex space-x-4">
                                    <button class="text-2xl"><i class="far fa-heart"></i></button>
                                    <button class="text-2xl"><i class="far fa-comment"></i></button>
                                    <button class="text-2xl"><i class="far fa-paper-plane"></i></button>
                                </div>
                                <button class="text-2xl"><i class="far fa-bookmark"></i></button>
                            </div>
                            
                            <div class="mb-1">
                                <span class="font-medium">1,234 curtidas</span>
                            </div>
                            
                            <div class="mb-1">
                                <span class="font-medium">marcos_22</span> A paisagem hoje estava incrível! #natureza #viagem
                            </div>
                            
                            <div class="text-gray-500 text-sm mb-1">
                                Ver todos os 87 comentários
                            </div>
                            
                            <div class="text-gray-400 text-xs">
                                HÁ 2 HORAS
                            </div>
                        </div>
                    </div>
                    
                    <!-- Post 2 -->
                    <div class="bg-white border border-gray-200 rounded-md">
                        <!-- Post Header -->
                        <div class="flex items-center justify-between p-3">
                            <div class="flex items-center space-x-2">
                                <div class="w-8 h-8 rounded-full overflow-hidden">
                                    <img src="https://randomuser.me/api/portraits/women/65.jpg" alt="User" class="w-full h-full object-cover">
                                </div>
                                <span class="font-medium">ana_clara</span>
                            </div>
                            <button>
                                <i class="fas fa-ellipsis-h"></i>
                            </button>
                        </div>
                        
                        <!-- Post Image -->
                        <div class="post-image bg-gray-100">
                            <img src="https://source.unsplash.com/random/600x600/?food" alt="Post" class="w-full h-full object-cover">
                        </div>
                        
                        <!-- Post Actions -->
                        <div class="p-3">
                            <div class="flex justify-between mb-2">
                                <div class="flex space-x-4">
                                    <button class="text-2xl"><i class="far fa-heart"></i></button>
                                    <button class="text-2xl"><i class="far fa-comment"></i></button>
                                    <button class="text-2xl"><i class="far fa-paper-plane"></i></button>
                                </div>
                                <button class="text-2xl"><i class="far fa-bookmark"></i></button>
                            </div>
                            
                            <div class="mb-1">
                                <span class="font-medium">892 curtidas</span>
                            </div>
                            
                            <div class="mb-1">
                                <span class="font-medium">ana_clara</span> Almoço especial hoje! #comida #gourmet
                            </div>
                            
                            <div class="text-gray-500 text-sm mb-1">
                                Ver todos os 32 comentários
                            </div>
                            
                            <div class="text-gray-400 text-xs">
                                HÁ 5 HORAS
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- Sidebar (Hidden on mobile) -->
            <div id="sidebar" class="hidden md:block md:w-1/3 pl-8">
                <div class="fixed w-64">
                    <!-- User Profile -->
                    <div class="flex items-center justify-between mb-6">
                        <div class="flex items-center space-x-4">
                            <div class="w-12 h-12 rounded-full overflow-hidden">
                                <img src="https://randomuser.me/api/portraits/women/44.jpg" alt="Profile" class="w-full h-full object-cover">
                            </div>
                            <div>
                                <p class="font-medium">julia_martins</p>
                                <p class="text-gray-500 text-sm">Julia Martins</p>
                            </div
</html>
