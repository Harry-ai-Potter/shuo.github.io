<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我的网站</title>
    <style>
        /* 全局样式 */
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        .container {
            max-width: 1100px;
            margin: 0 auto;
            padding: 20px;
        }
        /* 头部样式 */
        header {
            background: #333;
            color: #fff;
            padding: 10px 0;
        }
        header .container {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        header h1 {
            margin: 0;
        }
        nav a {
            color: #fff;
            text-decoration: none;
            margin-left: 20px;
        }
        nav a:hover {
            text-decoration: underline;
        }
        /* 主要内容样式 */
        .main-content {
            background: #fff;
            padding: 20px;
            margin: 20px 0;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .card {
            margin-bottom: 20px;
            padding: 20px;
            background: #f9f9f9;
            border-radius: 5px;
        }
        .card h2 {
            margin-top: 0;
            color: #333;
        }
        /* 页脚样式 */
        footer {
            background: #333;
            color: #fff;
            text-align: center;
            padding: 20px 0;
            margin-top: 20px;
        }
        footer p {
            margin: 0;
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <h1>我的网站</h1>
            <nav>
                首页
                关于我们
                服务
                联系方式
            </nav>
        </div>
    </header>
    
    <div class="container">
        <section class="main-content">
            <h2>欢迎来到我的网站</h2>
            <p>这是一个简单的示例网页，展示了基本的HTML和CSS布局。我们的目标是提供有价值的信息和实用的服务。</p >
            
            <div class="card">
                <h2>特色内容</h2>
                <p>我们专注于提供高质量的内容和创新的解决方案。以下是我们的主要内容方向：</p >
                <ul>
                    <li>技术教程：涵盖各种技术领域的入门到高级教程</li>
                    <li>行业动态：最新的行业新闻和技术趋势</li>
                    <li>实用工具：为用户提供的各类实用工具和资源</li>
                </ul>
                <p>无论您是技术爱好者还是行业专业人士，都能在这里找到有用的信息。</p >
            </div>
            
            <div class="card">
                <h2>最新资讯</h2>
                <p>以下是近期的一些更新和新闻：</p >
                <article>
                    <h3>新版网站上线</h3>
                    <p>我们很高兴地宣布，我们的新版网站已经正式上线！新网站带来了更友好的用户体验和更丰富的功能。</p >
                    <p>发布日期：2025年5月20日</p >
                </article>
                <article>
                    <h3>新增教程系列</h3>
                    <p>我们刚刚发布了一个新的教程系列，涵盖了最新的Web开发技术和最佳实践。</p >
                    <p>发布日期：2025年5月15日</p >
                </article>
            </div>
        </section>
    </div>
    
    <footer>
        <div class="container">
            <p>&copy; 2025 我的网站. 保留所有权利.</p >
            <p>联系我们：info@example.com | 电话：123-456-7890</p >
        </div>
    </footer>
</body>
</html>
