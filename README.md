<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>星际电影推荐 | 探索奇幻影视世界</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.8/dist/chart.umd.min.js"></script>
  
  <!-- 配置Tailwind自定义主题 -->
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            primary: '#6C5CE7',      // 主色调：深紫色
            secondary: '#00CEFF',    // 辅助色：霓虹蓝
            accent: '#FF2E63',       // 强调色：霓虹粉
            dark: '#131022',         // 深色背景
            darker: '#0A0814',       // 更深色背景
            light: '#F5F5F5',        // 浅色文本
          },
          fontFamily: {
            sans: ['Inter', 'system-ui', 'sans-serif'],
            display: ['Orbitron', 'sans-serif'], // 科幻风格字体
          },
          backgroundImage: {
            'gradient-radial': 'radial-gradient(var(--tw-gradient-stops))',
            'nebula': "url('https://picsum.photos/id/1002/1920/1080')",
          },
          animation: {
            'float': 'float 3s ease-in-out infinite',
            'pulse-slow': 'pulse 4s cubic-bezier(0.4, 0, 0.6, 1) infinite',
            'glow': 'glow 2s ease-in-out infinite alternate',
          },
          keyframes: {
            float: {
              '0%, 100%': { transform: 'translateY(0)' },
              '50%': { transform: 'translateY(-10px)' },
            },
            glow: {
              '0%': { textShadow: '0 0 5px rgba(108, 92, 231, 0.7), 0 0 10px rgba(108, 92, 231, 0.5)' },
              '100%': { textShadow: '0 0 10px rgba(0, 206, 255, 0.7), 0 0 20px rgba(0, 206, 255, 0.5), 0 0 30px rgba(0, 206, 255, 0.3)' },
            }
          },
        },
      }
    }
  </script>
  
  <!-- 自定义工具类 -->
  <style type="text/tailwindcss">
    @layer utilities {
      .content-auto {
        content-visibility: auto;
      }
      .text-shadow {
        text-shadow: 0 0 8px rgba(108, 92, 231, 0.5);
      }
      .text-shadow-glow {
        text-shadow: 0 0 10px rgba(0, 206, 255, 0.7), 0 0 20px rgba(0, 206, 255, 0.5);
      }
      .backdrop-blur-xl {
        backdrop-filter: blur(20px);
      }
      .scrollbar-hidden::-webkit-scrollbar {
        display: none;
      }
      .scrollbar-hidden {
        -ms-overflow-style: none;
        scrollbar-width: none;
      }
      .clip-path-slant {
        clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
      }
    }
  </style>
  
  <!-- 导入科幻风格字体 -->
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;600;700&display=swap" rel="stylesheet">
</head>

<body class="bg-dark text-light font-sans overflow-x-hidden">
  <!-- 背景特效 -->
  <div class="fixed inset-0 z-0 opacity-20">
    <div class="absolute top-0 left-0 w-full h-full bg-gradient-radial from-primary/20 to-transparent"></div>
    <div class="absolute top-0 left-0 w-full h-full" id="stars"></div>
  </div>

  <!-- 导航栏 -->
  <header class="fixed top-0 left-0 w-full z-50 transition-all duration-500" id="navbar">
    <div class="container mx-auto px-4 py-4 flex items-center justify-between backdrop-blur-xl bg-dark/60 border-b border-primary/20">
      <a href="#" class="flex items-center space-x-2">
        <div class="w-10 h-10 rounded-full bg-gradient-to-r from-primary to-secondary flex items-center justify-center animate-pulse-slow">
          <i class="fa fa-film text-white text-xl"></i>
        </div>
        <h1 class="text-2xl font-display font-bold text-shadow-glow animate-glow">星际电影</h1>
      </a>
      
      <!-- 桌面导航 -->
      <nav class="hidden md:flex items-center space-x-8">
        <a href="#" class="text-white hover:text-secondary transition-colors duration-300 font-medium">首页</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium">分类</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium">排行榜</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium">新上线</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium">关于</a>
      </nav>
      
      <!-- 搜索框 -->
      <div class="relative hidden md:block w-64">
        <input 
          type="text" 
          placeholder="搜索电影..." 
          class="w-full bg-darker/80 text-white border border-primary/30 rounded-full py-2 pl-10 pr-4 focus:outline-none focus:border-secondary transition-all duration-300"
        >
        <i class="fa fa-search absolute left-3 top-3 text-primary"></i>
      </div>
      
      <!-- 用户菜单 -->
      <div class="hidden md:flex items-center space-x-4">
        <button class="w-10 h-10 rounded-full bg-darker/80 flex items-center justify-center border border-primary/30 hover:border-secondary transition-all duration-300">
          <i class="fa fa-bell-o text-white"></i>
        </button>
        <button class="w-10 h-10 rounded-full bg-darker/80 flex items-center justify-center border border-primary/30 hover:border-secondary transition-all duration-300">
          <i class="fa fa-bookmark-o text-white"></i>
        </button>
        <div class="w-10 h-10 rounded-full overflow-hidden border-2 border-secondary">
          <img src="https://picsum.photos/id/1027/200/200" alt="用户头像" class="w-full h-full object-cover">
        </div>
      </div>
      
      <!-- 移动端菜单按钮 -->
      <button class="md:hidden text-white text-2xl" id="mobileMenuBtn">
        <i class="fa fa-bars"></i>
      </button>
    </div>
    
    <!-- 移动端菜单 -->
    <div class="md:hidden hidden bg-dark/95 backdrop-blur-xl border-b border-primary/20" id="mobileMenu">
      <div class="container mx-auto px-4 py-4 flex flex-col space-y-4">
        <div class="relative">
          <input 
            type="text" 
            placeholder="搜索电影..." 
            class="w-full bg-darker/80 text-white border border-primary/30 rounded-full py-2 pl-10 pr-4 focus:outline-none focus:border-secondary"
          >
          <i class="fa fa-search absolute left-3 top-3 text-primary"></i>
        </div>
        <a href="#" class="text-white hover:text-secondary transition-colors duration-300 font-medium py-2">首页</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium py-2">分类</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium py-2">排行榜</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium py-2">新上线</a>
        <a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 font-medium py-2">关于</a>
        <div class="flex items-center space-x-4 pt-2">
          <button class="w-10 h-10 rounded-full bg-darker/80 flex items-center justify-center border border-primary/30 hover:border-secondary transition-all duration-300">
            <i class="fa fa-bell-o text-white"></i>
          </button>
          <button class="w-10 h-10 rounded-full bg-darker/80 flex items-center justify-center border border-primary/30 hover:border-secondary transition-all duration-300">
            <i class="fa fa-bookmark-o text-white"></i>
          </button>
          <div class="w-10 h-10 rounded-full overflow-hidden border-2 border-secondary">
            <img src="https://picsum.photos/id/1027/200/200" alt="用户头像" class="w-full h-full object-cover">
          </div>
        </div>
      </div>
    </div>
  </header>

  <!-- 主内容 -->
  <main class="pt-24 pb-16 relative z-10">
    <!-- 英雄区域 -->
    <section class="relative h-[80vh] min-h-[600px] mb-20 overflow-hidden clip-path-slant">
      <div class="absolute inset-0 bg-gradient-to-b from-darker/50 via-darker/80 to-dark z-10"></div>
      <div class="absolute inset-0">
        <img 
          src="https://picsum.photos/id/1019/1920/1080" 
          alt="星际穿越" 
          class="w-full h-full object-cover"
          style="transform: scale(1.05); animation: float 20s ease-in-out infinite;"
        >
      </div>
      
      <div class="container mx-auto px-4 h-full flex items-end relative z-20">
        <div class="max-w-3xl pb-20">
          <div class="flex items-center space-x-3 mb-4">
            <span class="px-3 py-1 bg-accent text-white text-xs font-bold rounded-full">热门推荐</span>
            <span class="px-3 py-1 bg-darker/80 text-white/80 text-xs font-medium rounded-full">科幻</span>
            <span class="px-3 py-1 bg-darker/80 text-white/80 text-xs font-medium rounded-full">冒险</span>
          </div>
          
          <h2 class="text-[clamp(2rem,5vw,4rem)] font-display font-bold text-white text-shadow-glow mb-4">星际穿越</h2>
          
          <div class="flex items-center space-x-4 mb-6">
            <div class="flex items-center">
              <i class="fa fa-star text-yellow-400 mr-1"></i>
              <span class="text-2xl font-bold">9.4</span>
              <span class="text-white/70 ml-1">/ 10</span>
            </div>
            <span class="text-white/70">|</span>
            <span class="text-white/90">2014</span>
            <span class="text-white/70">|</span>
            <span class="text-white/90">169分钟</span>
            <span class="text-white/70">|</span>
            <span class="text-white/90">克里斯托弗·诺兰</span>
          </div>
          
          <p class="text-white/80 text-lg mb-8 leading-relaxed">
            当太阳系面临崩溃，一组探险家穿越虫洞，试图为人类寻找新家园。在时间和空间的维度中，他们必须面对人类认知的极限。
          </p>
          
          <div class="flex flex-wrap gap-4">
            <button class="px-8 py-3 bg-gradient-to-r from-primary to-secondary text-white font-bold rounded-full flex items-center hover:shadow-lg hover:shadow-primary/30 transition-all duration-300 transform hover:-translate-y-1">
              <i class="fa fa-play-circle mr-2"></i> 立即观看
            </button>
            <button class="px-8 py-3 bg-darker/80 border border-white/20 text-white font-bold rounded-full flex items-center hover:border-secondary hover:text-secondary transition-all duration-300">
              <i class="fa fa-plus mr-2"></i> 加入列表
            </button>
          </div>
        </div>
      </div>
    </section>
    
    <!-- 分类导航 -->
    <section class="container mx-auto px-4 mb-16">
      <div class="flex items-center justify-between mb-8">
        <h2 class="text-2xl font-display font-bold text-white">探索分类</h2>
        <a href="#" class="text-secondary hover:underline flex items-center">
          查看全部 <i class="fa fa-angle-right ml-1"></i>
        </a>
      </div>
      
      <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-6 gap-4">
        <div class="category-card group relative h-32 rounded-xl overflow-hidden cursor-pointer transition-all duration-500 transform hover:-translate-y-2">
          <div class="absolute inset-0 bg-gradient-to-b from-transparent to-darker z-10"></div>
          <img src="https://picsum.photos/id/1076/300/200" alt="科幻" class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110">
          <div class="absolute inset-0 flex items-center justify-center z-20">
            <h3 class="text-xl font-bold text-white text-shadow group-hover:text-secondary transition-colors duration-300">科幻</h3>
          </div>
        </div>
        
        <div class="category-card group relative h-32 rounded-xl overflow-hidden cursor-pointer transition-all duration-500 transform hover:-translate-y-2">
          <div class="absolute inset-0 bg-gradient-to-b from-transparent to-darker z-10"></div>
          <img src="https://picsum.photos/id/1074/300/200" alt="动作" class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110">
          <div class="absolute inset-0 flex items-center justify-center z-20">
            <h3 class="text-xl font-bold text-white text-shadow group-hover:text-secondary transition-colors duration-300">动作</h3>
          </div>
        </div>
        
        <div class="category-card group relative h-32 rounded-xl overflow-hidden cursor-pointer transition-all duration-500 transform hover:-translate-y-2">
          <div class="absolute inset-0 bg-gradient-to-b from-transparent to-darker z-10"></div>
          <img src="https://picsum.photos/id/1079/300/200" alt="奇幻" class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110">
          <div class="absolute inset-0 flex items-center justify-center z-20">
            <h3 class="text-xl font-bold text-white text-shadow group-hover:text-secondary transition-colors duration-300">奇幻</h3>
          </div>
        </div>
        
        <div class="category-card group relative h-32 rounded-xl overflow-hidden cursor-pointer transition-all duration-500 transform hover:-translate-y-2">
          <div class="absolute inset-0 bg-gradient-to-b from-transparent to-darker z-10"></div>
          <img src="https://picsum.photos/id/1078/300/200" alt="冒险" class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110">
          <div class="absolute inset-0 flex items-center justify-center z-20">
            <h3 class="text-xl font-bold text-white text-shadow group-hover:text-secondary transition-colors duration-300">冒险</h3>
          </div>
        </div>
        
        <div class="category-card group relative h-32 rounded-xl overflow-hidden cursor-pointer transition-all duration-500 transform hover:-translate-y-2">
          <div class="absolute inset-0 bg-gradient-to-b from-transparent to-darker z-10"></div>
          <img src="https://picsum.photos/id/1080/300/200" alt="悬疑" class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110">
          <div class="absolute inset-0 flex items-center justify-center z-20">
            <h3 class="text-xl font-bold text-white text-shadow group-hover:text-secondary transition-colors duration-300">悬疑</h3>
          </div>
        </div>
        
        <div class="category-card group relative h-32 rounded-xl overflow-hidden cursor-pointer transition-all duration-500 transform hover:-translate-y-2">
          <div class="absolute inset-0 bg-gradient-to-b from-transparent to-darker z-10"></div>
          <img src="https://picsum.photos/id/1077/300/200" alt="全部" class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110">
          <div class="absolute inset-0 flex items-center justify-center z-20">
            <h3 class="text-xl font-bold text-white text-shadow group-hover:text-secondary transition-colors duration-300">全部</h3>
          </div>
        </div>
      </div>
    </section>
    
    <!-- 热门电影 -->
    <section class="container mx-auto px-4 mb-16">
      <div class="flex items-center justify-between mb-8">
        <h2 class="text-2xl font-display font-bold text-white">热门推荐</h2>
        <div class="flex space-x-2">
          <button class="w-10 h-10 rounded-full bg-darker/80 border border-primary/30 flex items-center justify-center text-white hover:border-secondary transition-all duration-300" id="prevHot">
            <i class="fa fa-angle-left"></i>
          </button>
          <button class="w-10 h-10 rounded-full bg-darker/80 border border-primary/30 flex items-center justify-center text-white hover:border-secondary transition-all duration-300" id="nextHot">
            <i class="fa fa-angle-right"></i>
          </button>
        </div>
      </div>
      
      <div class="relative">
        <div class="overflow-x-auto pb-6 scrollbar-hidden" id="hotMovies">
          <div class="flex space-x-6 min-w-max">
            <!-- 电影卡片 1 -->
            <div class="movie-card group w-64 flex-shrink-0">
              <div class="relative rounded-xl overflow-hidden mb-4">
                <img src="https://picsum.photos/id/1019/300/450" alt="星际穿越" class="w-full h-80 object-cover">
                <div class="absolute inset-0 bg-gradient-to-t from-dark to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                <div class="absolute bottom-0 left-0 w-full p-4 transform translate-y-full group-hover:translate-y-0 transition-transform duration-300">
                  <div class="flex justify-between items-center mb-2">
                    <div class="flex items-center">
                      <i class="fa fa-star text-yellow-400 mr-1"></i>
                      <span class="font-bold">9.4</span>
                    </div>
                    <button class="w-8 h-8 rounded-full bg-primary/80 flex items-center justify-center text-white hover:bg-primary transition-colors">
                      <i class="fa fa-play"></i>
                    </button>
                  </div>
                  <div class="flex space-x-2">
                    <span class="text-xs bg-darker/80 px-2 py-1 rounded-full">科幻</span>
                    <span class="text-xs bg-darker/80 px-2 py-1 rounded-full">冒险</span>
                  </div>
                </div>
                <div class="absolute top-2 right-2 bg-accent text-white text-xs font-bold px-2 py-1 rounded">
                  9.4
                </div>
              </div>
              <h3 class="font-bold text-lg mb-1 group-hover:text-secondary transition-colors duration-300">星际穿越</h3>
              <p class="text-white/70 text-sm">2014 • 169分钟</p>
            </div>
            
            <!-- 电影卡片 2 -->
            <div class="movie-card group w-64 flex-shrink-0">
              <div class="relative rounded-xl overflow-hidden mb-4">
                <img src="https://picsum.photos/id/1029/300/450" alt="盗梦空间" class="w-full h-80 object-cover">
                <div class="absolute inset-0 bg-gradient-to-t from-dark to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                <div class="absolute bottom-0 left-0 w-full p-4 transform translate-y-full group-hover:translate-y-0 transition-transform duration-300">
                  <div class="flex justify-between items-center mb-2">
                    <div class="flex items-center">
                      <i class="fa fa-star text-yellow-400 mr-1"></i>
                      <span class="font-bold">9.2</span>
                    </div>
                    <button class="w-8 h-8 rounded-full bg-primary/80 flex items-center justify-center text-white hover:bg-primary transition-colors">
                      <i class="fa fa-play"></i>
                    </button>
                  </div>
                  <div class="flex space-x-2">
                    <span class="text-xs bg-darker/80 px-2 py-1 rounded-full">科幻</span>
                    <span class="text-xs bg-darker/80 px-2 py-1 rounded-full">悬疑</span>
                  </div>
                </div>
                <div class="absolute top-2 right-2 bg-accent text-white text-xs font-bold px-2 py-1 rounded">
                  9.2
                </div>
              </div>
              <h3 class="font-bold text-lg mb-1 group-hover:text-secondary transition-colors duration-300">盗梦空间</h3>
              <p class="text-white/70 text-sm">2010 • 148分钟</p>
            </div>
            
            <!-- 电影卡片 3 -->
            <div class="movie-card group w-64 flex-shrink-0">
              <div class="relative rounded-xl overflow-hidden mb-4">
                <img src="https://picsum.photos/id/1074/300/450" alt="阿凡达" class="w-full h-80 object-cover">
                <div class="absolute inset-0 bg-gradient-to-t from-dark to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                <div class="absolute bottom-0 left-0 w-full p-4 transform translate-y-full group-hover:translate-y-0 transition-transform duration-300">
                  <div class="flex justify-between items-center mb-2">
                    <div class="flex items-center">
                      <i class="fa fa-star text-yellow-400 mr-1"></i>
                      <span class="font-bold">8.9</span>
                    </div>
                    <button class="w-8 h-8 rounded-full bg-primary/80 flex items-center justify-center text-white hover:bg-primary transition-colors">
                      <i class="fa fa-play"></i>
                    </button>
                  </div>
                  <div class="flex space-x-2">
                    <span class="text-xs bg-darker/80 px-2 py-1 rounded-full">科幻</span>
                    <span class="text-xs bg-darker/80 px-2 py-1 rounded-full">冒险</span>
                  </div>
                </div>
                <div class="absolute top-2 right-2 bg-accent text-white text-xs font-bold px-2 py-1 rounded">
                  8.9
                </div>
              </div>
              <h3 class="font-bold text-lg mb-1 group-hover:text-secondary transition-colors duration-300">阿凡达</h3>
              <p class="text-white/70 text-sm">2009 • 162分钟</p>
            </div>
            
            <!-- 电影卡片 4 -->
            <div class="movie-card group w-64 flex-shrink-0">
              <div class="relative rounded-xl overflow-hidden mb-4">
                <img src="https://picsum.photos/id/1076/300/450" alt="银河护卫队" class="w-full h-80 object-cover">
                <div class="absolute inset-0 bg-gradient-to-t from-dark to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                <div class="absolute bottom-0 left-0 w-full p-4 transform translate-y-full group-hover:translate-y-0 transition-transform duration-300">
                  <div class="flex justify-between items-center mb-2">
                    <div class="flex items-center">
                      <i class="fa fa-star text-yellow-400 mr-1"></i>
                      <span class="font-bold">8.7</span>
                    </div>
                    <button class="w-8 h-8 rounded-full bg-primary/80 flex items-center justify-center text-white hover:bg-primary transition-colors">
                      <i class="fa fa-play"></i>
                    </button>
                  </div>
                  <div class="flex space-x-2">
                    <span class="text-xs bg-darker/80 px-2 py-1 rounded-full">科幻</span>
                    <span class="text-xs bg-darker/80 px-2 py-1 rounded-full">冒险</span>
                  </div>
                </div>
                <div class="absolute top-2 right-2 bg-accent text-white text-xs font-bold px-2 py-1 rounded">
                  8.7
                </div>
              </div>
              <h3 class="font-bold text-lg mb-1 group-hover:text-secondary transition-colors duration-300">银河护卫队</h3>
              <p class="text-white/70 text-sm">2014 • 122分钟</p>
            </div>
            
            <!-- 电影卡片 5 -->
            <div class="movie-card group w-64 flex-shrink-0">
              <div class="relative rounded-xl overflow-hidden mb-4">
                <img src="https://picsum.photos/id/1079/300/450" alt="沙丘" class="w-full h-80 object-cover">
                <div class="absolute inset-0 bg-gradient-to-t from-dark to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                <div class="absolute bottom-0 left-0 w-full p-4 transform translate-y-full group-hover:translate-y-0 transition-transform duration-300">
                  <div class="flex justify-between items-center mb-2">
                    <div class="flex items-center">
                      <i class="fa fa-star text-yellow-400 mr-1"></i>
                      <span class="font-bold">8.5</span>
                    </div>
                    <button class="w-8 h-8 rounded-full bg-primary/80 flex items-center justify-center text-white hover:bg-primary transition-colors">
                      <i class="fa fa-play"></i>
                    </button>
                  </div>
                  <div class="flex space-x-2">
                    <span class="text-xs bg-darker/80 px-2 py-1 rounded-full">科幻</span>
                    <span class="text-xs bg-darker/80 px-2 py-1 rounded-full">冒险</span>
                  </div>
                </div>
                <div class="absolute top-2 right-2 bg-accent text-white text-xs font-bold px-2 py-1 rounded">
                  8.5
                </div>
              </div>
              <h3 class="font-bold text-lg mb-1 group-hover:text-secondary transition-colors duration-300">沙丘</h3>
              <p class="text-white/70 text-sm">2021 • 155分钟</p>
            </div>
            
            <!-- 电影卡片 6 -->
            <div class="movie-card group w-64 flex-shrink-0">
              <div class="relative rounded-xl overflow-hidden mb-4">
                <img src="https://picsum.photos/id/1080/300/450" alt="黑客帝国" class="w-full h-80 object-cover">
                <div class="absolute inset-0 bg-gradient-to-t from-dark to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                <div class="absolute bottom-0 left-0 w-full p-4 transform translate-y-full group-hover:translate-y-0 transition-transform duration-300">
                  <div class="flex justify-between items-center mb-2">
                    <div class="flex items-center">
                      <i class="fa fa-star text-yellow-400 mr-1"></i>
                      <span class="font-bold">9.0</span>
                    </div>
                    <button class="w-8 h-8 rounded-full bg-primary/80 flex items-center justify-center text-white hover:bg-primary transition-colors">
                      <i class="fa fa-play"></i>
                    </button>
                  </div>
                  <div class="flex space-x-2">
                    <span class="text-xs bg-darker/80 px-2 py-1 rounded-full">科幻</span>
                    <span class="text-xs bg-darker/80 px-2 py-1 rounded-full">动作</span>
                  </div>
                </div>
                <div class="absolute top-2 right-2 bg-accent text-white text-xs font-bold px-2 py-1 rounded">
                  9.0
                </div>
              </div>
              <h3 class="font-bold text-lg mb-1 group-hover:text-secondary transition-colors duration-300">黑客帝国</h3>
              <p class="text-white/70 text-sm">1999 • 136分钟</p>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- 即将上映 -->
    <section class="container mx-auto px-4 mb-16 relative">
      <div class="absolute inset-0 bg-gradient-to-r from-primary/20 to-transparent opacity-50 rounded-3xl"></div>
      <div class="relative">
        <div class="flex items-center justify-between mb-8">
          <h2 class="text-2xl font-display font-bold text-white">即将上映</h2>
          <a href="#" class="text-secondary hover:underline flex items-center">
            预约提醒 <i class="fa fa-bell-o ml-1"></i>
          </a>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <!-- 即将上映电影 1 -->
          <div class="bg-darker/60 backdrop-blur-xl rounded-2xl overflow-hidden border border-primary/20 transition-all duration-500 hover:border-secondary/50 hover:shadow-lg hover:shadow-primary/10 transform hover:-translate-y-2">
            <div class="relative">
              <img src="https://picsum.photos/id/1025/600/300" alt="沙丘2" class="w-full h-48 object-cover">
              <div class="absolute top-0 right-0 bg-accent text-white px-3 py-1 text-sm font-bold">
                2025-12-25 上映
              </div>
            </div>
            <div class="p-6">
              <h3 class="text-xl font-bold mb-2">沙丘2</h3>
                            <div class="flex items-center space-x-4 mb-4">
                              <div class="flex items-center">
                                <i class="fa fa-star text-yellow-400 mr-1"></i>
                                <span class="font-bold">9.1 (预售)</span>
                              </div>
                              <span class="text-white/70">|</span>
                              <span>科幻 / 冒险</span>
                            </div>
                            <p class="text-white/70 mb-6 line-clamp-3">
                              保罗·厄崔迪与契尼联手，为了复仇与生存，必须与哈克南男爵展开终极对决，同时还要面对宇宙中更强大的威胁...
                            </p>
                            <div class="flex justify-between items-center">
                              <button class="px-4 py-2 bg-primary/20 border border-primary/30 text-secondary rounded-lg hover:bg-primary/30 transition-all duration-300">
                                预约提醒
                              </button>
                              <span class="text-white/50 text-sm">距离上映还有 68 天</span>
                            </div>
                          </div>
                        </div>
                        
                        <!-- 即将上映电影 2 -->
                        <div class="bg-darker/60 backdrop-blur-xl rounded-2xl overflow-hidden border border-primary/20 transition-all duration-500 hover:border-secondary/50 hover:shadow-lg hover:shadow-primary/10 transform hover:-translate-y-2">
                          <div class="relative">
                            <img src="https://picsum.photos/id/1071/600/300" alt="星际迷航：奇异新世界" class="w-full h-48 object-cover">
                            <div class="absolute top-0 right-0 bg-accent text-white px-3 py-1 text-sm font-bold">
                              2025-09-15 上映
                            </div>
                          </div>
                          <div class="p-6">
                            <h3 class="text-xl font-bold mb-2">星际迷航：奇异新世界</h3>
                            <div class="flex items-center space-x-4 mb-4">
                              <div class="flex items-center">
                                <i class="fa fa-star text-yellow-400 mr-1"></i>
                                <span class="font-bold">8.9 (预售)</span>
                              </div>
                              <span class="text-white/70">|</span>
                              <span>科幻 / 冒险</span>
                            </div>
                            <p class="text-white/70 mb-6 line-clamp-3">
                              企业号船员们踏上新的航程，探索未知的星系，面对神秘的外星文明，同时揭开宇宙中隐藏的秘密...
                            </p>
                            <div class="flex justify-between items-center">
                              <button class="px-4 py-2 bg-primary/20 border border-primary/30 text-secondary rounded-lg hover:bg-primary/30 transition-all duration-300">
                                预约提醒
                              </button>
                              <span class="text-white/50 text-sm">距离上映还有 92 天</span>
                            </div>
                          </div>
                        </div>
                        
                        <!-- 即将上映电影 3 -->
                        <div class="bg-darker/60 backdrop-blur-xl rounded-2xl overflow-hidden border border-primary/20 transition-all duration-500 hover:border-secondary/50 hover:shadow-lg hover:shadow-primary/10 transform hover:-translate-y-2">
                          <div class="relative">
                            <img src="https://picsum.photos/id/1072/600/300" alt="阿凡达3" class="w-full h-48 object-cover">
                            <div class="absolute top-0 right-0 bg-accent text-white px-3 py-1 text-sm font-bold">
                              2026-03-01 上映
                            </div>
                          </div>
                          <div class="p-6">
                            <h3 class="text-xl font-bold mb-2">阿凡达3</h3>
                            <div class="flex items-center space-x-4 mb-4">
                              <div class="flex items-center">
                                <i class="fa fa-star text-yellow-400 mr-1"></i>
                                <span class="font-bold">9.2 (预售)</span>
                              </div>
                              <span class="text-white/70">|</span>
                              <span>科幻 / 冒险</span>
                            </div>
                            <p class="text-white/70 mb-6 line-clamp-3">
                              杰克·萨利与妮特丽继续守护潘多拉星球，面对人类的再次入侵，他们必须联合各部落，为生存而战...
                            </p>
                            <div class="flex justify-between items-center">
                              <button class="px-4 py-2 bg-primary/20 border border-primary/30 text-secondary rounded-lg hover:bg-primary/30 transition-all duration-300">
                                预约提醒
                              </button>
                              <span class="text-white/50 text-sm">距离上映还有 260 天</span>
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </section>
                  
                  <!-- 用户评分与统计 -->
                  <section class="container mx-auto px-4 mb-16">
                    <div class="flex flex-col md:flex-row justify-between items-center mb-8">
                      <h2 class="text-2xl font-display font-bold text-white mb-4 md:mb-0">用户评分趋势</h2>
                      <div class="flex space-x-2">
                        <button class="px-4 py-2 bg-darker/80 border border-primary/30 rounded-lg text-white hover:border-secondary transition-all duration-300">月度</button>
                        <button class="px-4 py-2 bg-primary text-white rounded-lg">季度</button>
                        <button class="px-4 py-2 bg-darker/80 border border-primary/30 rounded-lg text-white hover:border-secondary transition-all duration-300">年度</button>
                      </div>
                    </div>
                    
                    <div class="bg-darker/60 backdrop-blur-xl rounded-2xl p-6 border border-primary/20">
                      <div class="h-80">
                        <canvas id="ratingsChart"></canvas>
                      </div>
                    </div>
                  </section>
                  
                  <!-- 订阅区域 -->
                  <section class="container mx-auto px-4 mb-16 relative overflow-hidden rounded-3xl">
                    <div class="absolute inset-0">
                      <img src="https://picsum.photos/id/1002/1920/800" alt="背景" class="w-full h-full object-cover">
                      <div class="absolute inset-0 bg-gradient-to-r from-dark via-dark/80 to-dark/60"></div>
                    </div>
                    
                    <div class="relative z-10 py-16 px-8 md:px-16 flex flex-col md:flex-row items-center justify-between">
                      <div class="max-w-2xl mb-8 md:mb-0">
                        <h2 class="text-3xl md:text-4xl font-display font-bold text-white mb-4">订阅我们的电影资讯</h2>
                        <p class="text-white/80 text-lg mb-6">
                          第一时间获取最新电影资讯、独家预告片和限时优惠，不错过任何精彩内容。
                        </p>
                        <div class="flex flex-col sm:flex-row gap-4">
                          <input 
                            type="email" 
                            placeholder="输入你的邮箱地址" 
                            class="flex-grow px-4 py-3 bg-darker/80 border border-primary/30 rounded-lg text-white focus:outline-none focus:border-secondary transition-all duration-300"
                          >
                          <button class="px-6 py-3 bg-gradient-to-r from-primary to-secondary text-white font-bold rounded-lg hover:shadow-lg hover:shadow-primary/30 transition-all duration-300 whitespace-nowrap">
                            立即订阅
                          </button>
                        </div>
                      </div>
                      
                      <div class="hidden md:block w-1/3">
                        <div class="relative">
                          <img 
                            src="https://picsum.photos/id/1025/500/500" 
                            alt="电影" 
                            class="w-full h-auto rounded-2xl border-4 border-primary/30 animate-float"
                          >
                          <div class="absolute -bottom-4 -right-4 w-24 h-24 bg-accent rounded-full flex items-center justify-center text-white font-bold text-2xl animate-pulse-slow">
                            <span>新</span>
                          </div>
                        </div>
                      </div>
                    </div>
                  </section>
                </main>
              
                <!-- 页脚 -->
                <footer class="bg-darker border-t border-primary/20">
                  <div class="container mx-auto px-4 py-12">
                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
                      <div>
                        <div class="flex items-center space-x-2 mb-6">
                          <div class="w-10 h-10 rounded-full bg-gradient-to-r from-primary to-secondary flex items-center justify-center">
                            <i class="fa fa-film text-white text-xl"></i>
                          </div>
                          <h2 class="text-2xl font-display font-bold text-shadow-glow">星际电影</h2>
                        </div>
                        <p class="text-white/70 mb-6">
                          探索奇幻影视世界，发现无限可能。我们提供最新、最热门的电影推荐，满足你的观影需求。
                        </p>
                        <div class="flex space-x-4">
                          <a href="#" class="w-10 h-10 rounded-full bg-dark/80 flex items-center justify-center text-white hover:bg-primary/20 transition-all duration-300">
                            <i class="fa fa-facebook"></i>
                          </a>
                          <a href="#" class="w-10 h-10 rounded-full bg-dark/80 flex items-center justify-center text-white hover:bg-primary/20 transition-all duration-300">
                            <i class="fa fa-twitter"></i>
                          </a>
                          <a href="#" class="w-10 h-10 rounded-full bg-dark/80 flex items-center justify-center text-white hover:bg-primary/20 transition-all duration-300">
                            <i class="fa fa-instagram"></i>
                          </a>
                          <a href="#" class="w-10 h-10 rounded-full bg-dark/80 flex items-center justify-center text-white hover:bg-primary/20 transition-all duration-300">
                            <i class="fa fa-youtube-play"></i>
                          </a>
                        </div>
                      </div>
                      
                      <div>
                        <h3 class="text-xl font-bold mb-6">快速链接</h3>
                        <ul class="space-y-3">
                          <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
                            <i class="fa fa-angle-right mr-2"></i> 首页
                          </a></li>
                          <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
                            <i class="fa fa-angle-right mr-2"></i> 电影分类
                          </a></li>
                          <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
                            <i class="fa fa-angle-right mr-2"></i> 排行榜
                          </a></li>
                          <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
                            <i class="fa fa-angle-right mr-2"></i> 最新上映
                          </a></li>
                          <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
                            <i class="fa fa-angle-right mr-2"></i> 关于我们
                          </a></li>
                        </ul>
                      </div>
                      
                      <div>
                        <h3 class="text-xl font-bold mb-6">支持</h3>
                        <ul class="space-y-3">
                          <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
                            <i class="fa fa-angle-right mr-2"></i> 帮助中心
                          </a></li>
                          <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
                            <i class="fa fa-angle-right mr-2"></i> 常见问题
                          </a></li>
                          <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
                            <i class="fa fa-angle-right mr-2"></i> 联系我们
                          </a></li>
                          <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
                            <i class="fa fa-angle-right mr-2"></i> 隐私政策
                          </a></li>
                          <li><a href="#" class="text-white/70 hover:text-secondary transition-colors duration-300 flex items-center">
                            <i class="fa fa-angle-right mr-2"></i> 使用条款
                          </a></li>
                        </ul>
                      </div>
                      
                      <div>
                        <h3 class="text-xl font-bold mb-6">联系我们</h3>
                        <ul class="space-y-3">
                          <li class="flex items-start space-x-3">
                            <i class="fa fa-map-marker text-secondary mt-1"></i>
                            <span class="text-white/70">北京市朝阳区科幻大道1001号星际中心</span>
                          </li>
                          <li class="flex items-center space-x-3">
                            <i class="fa fa-phone text-secondary"></i>
                            <span class="text-white/70">+86 10 8888 8888</span>
                          </li>
                          <li class="flex items-center space-x-3">
                            <i class="fa fa-envelope text-secondary"></i>
                            <span class="text-white/70">contact@xingjimov.com</span>
                          </li>
                        </ul>
                        
                        <div class="mt-6">
                          <h4 class="text-lg font-bold mb-3">下载我们的应用</h4>
                          <div class="flex space-x-3">
                            <a href="#" class="bg-dark/80 rounded-lg p-2 hover:bg-primary/20 transition-all duration-300">
                              <i class="fa fa-apple text-2xl"></i>
                            </a>
                            <a href="#" class="bg-dark/80 rounded-lg p-2 hover:bg-primary/20 transition-all duration-300">
                              <i class="fa fa-android text-2xl"></i>
                            </a>
                          </div>
                        </div>
                      </div>
                    </div>
                    
                    <div class="border-t border-gray-800 mt-12 pt-8 text-center text-white/50 text-sm">
                      <p>© 2025 星际电影推荐. 保留所有权利.</p>
                    </div>
                  </div>
                </footer>
              
                <!-- 模态框（登录/注册） -->
                <div class="fixed inset-0 z-50 flex items-center justify-center hidden" id="authModal">
                  <div class="absolute inset-0 bg-black/70 backdrop-blur-sm" id="modalOverlay"></div>
                  <div class="relative bg-darker rounded-2xl border border-primary/30 w-full max-w-md p-6 transform transition-all duration-500 scale-95 opacity-0" id="modalContent">
                    <button class="absolute top-4 right-4 text-white/70 hover:text-white transition-colors" id="closeModal">
                      <i class="fa fa-times text-xl"></i>
                    </button>
                    
                    <div class="text-center mb-6">
                      <h2 class="text-2xl font-bold text-white">欢迎回来</h2>
                      <p class="text-white/70">登录您的账户，探索更多精彩电影</p>
                    </div>
                    
                    <div class="space-y-4">
                      <div>
                        <label for="email" class="block text-white/70 mb-2">邮箱地址</label>
                        <input 
                          type="email" 
                          id="email" 
                          class="w-full px-4 py-3 bg-dark border border-primary/30 rounded-lg text-white focus:outline-none focus:border-secondary transition-all duration-300"
                          placeholder="your@email.com"
                        >
                      </div>
                      
                      <div>
                        <label for="password" class="block text-white/70 mb-2">密码</label>
                        <input 
                          type="password" 
                          id="password" 
                          class="w-full px-4 py-3 bg-dark border border-primary/30 rounded-lg text-white focus:outline-none focus:border-secondary transition-all duration-300"
                          placeholder="••••••••"
                        >
                      </div>
                      
                      <div class="flex items-center justify-between">
                        <label class="flex items-center space-x-2 text-white/70">
                          <input type="checkbox" class="w-4 h-4 bg-dark border border-primary/30 rounded">
                          <span>记住我</span>
                        </label>
                        <a href="#" class="text-secondary hover:underline">忘记密码?</a>
                      </div>
                      
                      <button class="w-full py-3 bg-gradient-to-r from-primary to-secondary text-white font-bold rounded-lg hover:shadow-lg hover:shadow-primary/30 transition-all duration-300">
                        登录
                      </button>
                      
                      <div class="relative text-center">
                        <div class="absolute inset-0 flex items-center">
                          <div class="w-full border-t border-gray-700"></div>
                        </div>
                        <div class="relative z-10">
                          <span class="px-3 bg-darker text-white/50">或者</span>
                        </div>
                      </div>
                      
                      <div class="grid grid-cols-2 gap-3">
                        <button class="py-2 bg-dark border border-primary/30 rounded-lg text-white flex items-center justify-center hover:border-secondary transition-all duration-300">
                          <i class="fa fa-google mr-2"></i> Google
                        </button>
                        <button class="py-2 bg-dark border border-primary/30 rounded-lg text-white flex items-center justify-center hover:border-secondary transition-all duration-300">
                          <i class="fa fa-facebook mr-2"></i> Facebook
                        </button>
                      </div>
                      
                      <div class="text-center">
                        <p class="text-white/70">
                          还没有账户? <a href="#" class="text-secondary hover:underline">立即注册</a>
                        </p>
                      </div>
                    </div>
                  </div>
                </div>
              
                <!-- JavaScript -->
                <script>
                  // 生成背景星星
                  function createStars() {
                    const stars = document.getElementById('stars');
                    const count = 200;
                    
                    for (let i = 0; i < count; i++) {
                      const star = document.createElement('div');
                      const size = Math.random() * 3 + 1;
                      const opacity = Math.random() * 0.8 + 0.2;
                      const x = Math.random() * 100;
                      const y = Math.random() * 100;
                      const duration = Math.random() * 10 + 5;
                      
                      star.style.cssText = `
                        position: absolute;
                        width: ${size}px;
                        height: ${size}px;
                        background: rgba(255, 255, 255, ${opacity});
                        border-radius: 50%;
                        left: ${x}%;
                        top: ${y}%;
                        box-shadow: 0 0 ${size}px rgba(255, 255, 255, 0.8);
                        animation: blink ${duration}s infinite ease-in-out;
                      `;
                      
                      stars.appendChild(star);
                    }
                  }
                  
                  // 导航栏滚动效果
                  const navbar = document.getElementById('navbar');
                  
                  window.addEventListener('scroll', () => {
                    if (window.scrollY > 100) {
                      navbar.classList.add('py-2', 'shadow-lg');
                      navbar.classList.remove('py-4');
                    } else {
                      navbar.classList.add('py-4');
                      navbar.classList.remove('py-2', 'shadow-lg');
                    }
                  });
                  
                  // 移动端菜单切换
                  const mobileMenuBtn = document.getElementById('mobileMenuBtn');
                  const mobileMenu = document.getElementById('mobileMenu');
                  
                  mobileMenuBtn.addEventListener('click', () => {
                    mobileMenu.classList.toggle('hidden');
                    mobileMenuBtn.innerHTML = mobileMenu.classList.contains('hidden') 
                      ? '<i class="fa fa-bars"></i>' 
                      : '<i class="fa fa-times"></i>';
                  });
                  
                  // 热门电影滚动控制
                  const hotMovies = document.getElementById('hotMovies');
                  const prevHot = document.getElementById('prevHot');
                  const nextHot = document.getElementById('nextHot');
                  
                  nextHot.addEventListener('click', () => {
                    hotMovies.scrollBy({ left: 300, behavior: 'smooth' });
                  });
                  
                  prevHot.addEventListener('click', () => {
                    hotMovies.scrollBy({ left: -300, behavior: 'smooth' });
                  });
                  
                  // 评分图表
                  const ctx = document.getElementById('ratingsChart').getContext('2d');
                  const ratingsChart = new Chart(ctx, {
                    type: 'line',
                    data: {
                      labels: ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月'],
                      datasets: [
                        {
                          label: '科幻',
                          data: [9.2, 9.1, 9.3, 9.4, 9.3, 9.5, 9.4, 9.5, 9.6],
                          borderColor: '#6C5CE7',
                          backgroundColor: 'rgba(108, 92, 231, 0.1)',
                          tension: 0.4,
                          fill: true
                        },
                        {
                          label: '动作',
                          data: [8.7, 8.8, 8.9, 8.8, 9.0, 8.9, 9.1, 9.0, 9.2],
                          borderColor: '#00CEFF',
                          backgroundColor: 'rgba(0, 206, 255, 0.1)',
                          tension: 0.4,
                          fill: true
                        },
                        {
                          label: '奇幻',
                          data: [8.5, 8.6, 8.7, 8.8, 8.9, 9.0, 9.1, 9.2, 9.3],
                          borderColor: '#FF2E63',
                          backgroundColor: 'rgba(255, 46, 99, 0.1)',
                          tension: 0.4,
                          fill: true
                        }
                      ]
                    },
                    options: {
                      responsive: true,
                      maintainAspectRatio: false,
                      plugins: {
                        legend: {
                          position: 'top',
                          labels: {
                            color: 'rgba(255, 255, 255, 0.7)',
                            font: {
                              family: 'Inter',
                              size: 12
                            }
                          }
                        },
                        tooltip: {
                          mode: 'index',
                          intersect: false,
                          backgroundColor: 'rgba(10, 8, 20, 0.9)',
                          titleColor: '#fff',
                          bodyColor: 'rgba(255, 255, 255, 0.7)',
                          borderColor: 'rgba(108, 92, 231, 0.3)',
                          borderWidth: 1,
                          padding: 12,
                          displayColors: false,
                          callbacks: {
                            label: function(context) {
                              return ` ${context.dataset.label}: ${context.raw}`;
                            }
                          }
                        }
                      },
                      scales: {
                        x: {
                          grid: {
                            display: false,
                            drawBorder: false
                          },
                          ticks: {
                            color: 'rgba(255, 255, 255, 0.5)'
                          }
                        },
                        y: {
                          min: 8,
                          max: 10,
                          grid: {
                            color: 'rgba(255, 255, 255, 0.05)',
                            drawBorder: false
                          },
                          ticks: {
                            color: 'rgba(255, 255, 255, 0.5)',
                            stepSize: 0.5
                          }
                        }
                      },
                      interaction: {
                        mode: 'nearest',
                        axis: 'x',
                        intersect: false
                      },
                      elements: {
                        point: {
                          radius: 2,
                          hoverRadius: 5,
                          backgroundColor: '#fff'
                        }
                      }
                    }
                  });
                  
                  // 模态框控制
                  const authModal = document.getElementById('authModal');
                  const modalContent = document.getElementById('modalContent');
                  const modalOverlay = document.getElementById('modalOverlay');
                  const closeModal = document.getElementById('closeModal');
                  
                  function openModal() {
                    authModal.classList.remove('hidden');
                    setTimeout(() => {
                      modalContent.classList.remove('scale-95', 'opacity-0');
                      modalContent.classList.add('scale-100', 'opacity-100');
                    }, 10);
                  }
                  
                  function closeModalFunc() {
                    modalContent.classList.remove('scale-100', 'opacity-100');
                    modalContent.classList.add('scale-95', 'opacity-0');
                    setTimeout(() => {
                      authModal.classList.add('hidden');
                    }, 300);
                  }
                  
                  // 点击登录按钮打开模态框（这里假设登录按钮有login-btn类）
                  document.querySelectorAll('.login-btn').forEach(btn => {
                    btn.addEventListener('click', openModal);
                  });
                  
                  closeModal.addEventListener('click', closeModalFunc);
                  modalOverlay.addEventListener('click', closeModalFunc);
                  
                  // 键盘事件：ESC关闭模态框
                  document.addEventListener('keydown', (e) => {
                    if (e.key === 'Escape' && !authModal.classList.contains('hidden')) {
                      closeModalFunc();
                    }
                  });
                  
                  // 初始化
                  window.addEventListener('load', () => {
                    createStars();
                    
                    // 模拟加载动画
                    setTimeout(() => {
                      document.body.classList.add('loaded');
                    }, 500);
                  });
                </script>
              </body>
              </html>
