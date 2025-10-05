---
layout: default
title: 每日更新
mobile: true
---

<link rel="stylesheet" href="/assets/mobile.css">

<div class="mobile-container">
    <!-- 顶部标题栏 -->
    <header class="mobile-header">
        <div class="header-content">
            <h1>📱 每日信息发布</h1>
            <div class="date-info">
                <span class="current-date" id="currentDate"></span>
                <span class="update-time">更新于: <span id="updateTime"></span></span>
            </div>
        </div>
    </header>

    <!-- 最新消息置顶 -->
    <section class="highlight-post">
        {% assign latest_post = site.posts.first %}
        {% if latest_post %}
        <div class="highlight-card">
            <div class="badge">最新</div>
            <h2>{{ latest_post.title }}</h2>
            <time>{{ latest_post.date | date: "%m月%d日 %H:%M" }}</time>
            <div class="content-preview">
                {{ latest_post.content | strip_html | truncate: 100 }}
            </div>
            <a href="{{ latest_post.url }}" class="read-more">阅读全文</a>
        </div>
        {% endif %}
    </section>

    <!-- 消息列表 -->
    <main class="posts-container">
        <h3 class="section-title">历史消息</h3>
        
        {% for post in site.posts %}
        <article class="post-card" onclick="location.href='{{ post.url }}'">
            <div class="post-header">
                <h4>{{ post.title }}</h4>
                <time>{{ post.date | date: "%m月%d日" }}</time>
            </div>
            <div class="post-excerpt">
                {{ post.content | strip_html | truncate: 80 }}
            </div>
            <div class="post-meta">
                <span class="read-time">📖 约{{ post.content | number_of_words | divided_by: 300 | plus: 1 }}分钟阅读</span>
            </div>
        </article>
        {% endfor %}
    </main>

    <!-- 底部信息 -->
    <footer class="mobile-footer">
        <p>每日更新 • 手机优化版本</p>
        <p>最后更新: <span id="lastBuildTime"></span></p>
    </footer>
</div>

<script>
// 显示当前日期和时间
function updateDateTime() {
    const now = new Date();
    document.getElementById('currentDate').textContent = 
        now.getFullYear() + '年' + 
        (now.getMonth() + 1) + '月' + 
        now.getDate() + '日';
    
    document.getElementById('updateTime').textContent = 
        now.getHours().toString().padStart(2, '0') + ':' + 
        now.getMinutes().toString().padStart(2, '0');
    
    document.getElementById('lastBuildTime').textContent = 
        now.toLocaleString('zh-CN');
}

// 页面加载时执行
document.addEventListener('DOMContentLoaded', function() {
    updateDateTime();
    
    // 添加点击效果
    const cards = document.querySelectorAll('.post-card');
    cards.forEach(card => {
        card.addEventListener('touchstart', function() {
            this.style.transform = 'scale(0.98)';
        });
        card.addEventListener('touchend', function() {
            this.style.transform = 'scale(1)';
        });
    });
});
</script>
