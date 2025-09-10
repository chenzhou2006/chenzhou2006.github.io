<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BE YOU PHOTOS - 个性摄影网站</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Arial', sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: #333;
        }
        
        header {
            background-color: white;
            color: #024059;
            padding: 1rem 0;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        .container {
            width: 90%;
            max-width: 1200px;
            margin: 0 auto;
        }
        
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            font-size: 1.5rem;
            font-weight: bold;
            color: #069dbf;
        }
        
        .nav-links {
            display: flex;
            list-style: none;
        }
        
        .nav-links li {
            margin-left: 2rem;
        }
        
        .nav-links a {
            color: #024059;
            text-decoration: none;
            transition: color 0.3s;
            font-weight: 500;
        }
        
        .nav-links a:hover {
            color: #069dbf;
        }
        
        .hero {
            height: 100vh;
            background: url('https://images.unsplash.com/photo-1492684223066-81342ee5ff30') center/cover no-repeat;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            margin-top: 60px;
            position: relative;
        }
        
        .hero::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(2, 64, 89, 0.6);
        }
        
        .hero-content {
            z-index: 1;
            color: white;
        }
        
        .hero h1 {
            font-size: 3rem;
            margin-bottom: 1rem;
        }
        
        .hero p {
            font-size: 1.2rem;
            margin-bottom: 2rem;
        }
        
        .btn {
            display: inline-block;
            background-color: #069dbf;
            color: white;
            padding: 0.8rem 1.5rem;
            border-radius: 5px;
            text-decoration: none;
            transition: background-color 0.3s;
        }
        
        .btn:hover {
            background-color: #057a96;
        }
        
        .gallery {
            padding: 4rem 0;
        }
        
        .section-title {
            text-align: center;
            margin-bottom: 2rem;
            font-size: 2rem;
            color: #024059;
        }
        
        .photo-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 1rem;
        }
        
        .photo-item {
            position: relative;
            overflow: hidden;
            border-radius: 5px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s;
        }
        
        .photo-item:hover {
            transform: scale(1.03);
        }
        
        .photo-item img {
            width: 100%;
            height: 300px;
            object-fit: cover;
            display: block;
        }
        
        /* 无图片上传的灰色背景样式 */
        .no-image-placeholder {
            width: 100%;
            height: 300px;
            background-color: #e0e0e0;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #757575;
            font-size: 1.2rem;
            font-weight: bold;
        }
        
        .photo-info {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: rgba(2, 64, 89, 0.8);
            color: white;
            padding: 1rem;
            transform: translateY(100%);
            transition: transform 0.3s;
        }
        
        .photo-item:hover .photo-info {
            transform: translateY(0);
        }
        
        /* 上传区域样式 */
        .upload-section {
            padding: 4rem 0;
            background-color: white;
        }
        
        .upload-container {
            max-width: 600px;
            margin: 0 auto;
            padding: 2rem;
            background-color: #f9f9f9;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        .upload-form {
            display: flex;
            flex-direction: column;
        }
        
        .form-group {
            margin-bottom: 1.5rem;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
            color: #024059;
        }
        
        .form-group input,
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 1rem;
        }
        
        .form-group textarea {
            min-height: 100px;
            resize: vertical;
        }
        
        .file-upload {
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 2rem;
            border: 2px dashed #069dbf;
            border-radius: 8px;
            background-color: rgba(6, 157, 191, 0.05);
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .file-upload:hover {
            background-color: rgba(6, 157, 191, 0.1);
        }
        
        .file-upload i {
            font-size: 2rem;
            color: #069dbf;
            margin-bottom: 1rem;
        }
        
        .file-upload p {
            color: #069dbf;
            text-align: center;
        }
        
        #fileInput {
            display: none;
        }
        
        .preview-container {
            margin-top: 1rem;
            display: none;
        }
        
        .preview-image {
            max-width: 100%;
            max-height: 200px;
            margin-top: 1rem;
            border-radius: 4px;
        }
        
        .upload-btn {
            background-color: #069dbf;
            color: white;
            border: none;
            padding: 1rem;
            border-radius: 5px;
            font-size: 1rem;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        .upload-btn:hover {
            background-color: #057a96;
        }
        
        .upload-btn:disabled {
            background-color: #cccccc;
            cursor: not-allowed;
        }
        
        .status-message {
            margin-top: 1rem;
            padding: 0.8rem;
            border-radius: 4px;
            text-align: center;
            display: none;
        }
        
        .success {
            background-color: #d4edda;
            color: #155724;
        }
        
        .error {
            background-color: #f8d7da;
            color: #721c24;
        }
        
        .processing {
            background-color: #e2e3e5;
            color: #383d41;
        }
        
        /* 审核状态指示器 */
        .status-indicator {
            display: inline-block;
            padding: 0.3rem 0.6rem;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: bold;
            margin-left: 1rem;
        }
        
        .status-pending {
            background-color: #fff3cd;
            color: #856404;
        }
        
        .status-approved {
            background-color: #d4edda;
            color: #155724;
        }
        
        .status-rejected {
            background-color: #f8d7da;
            color: #721c24;
        }
        
        /* 审核拒绝原因 */
        .rejection-reason {
            margin-top: 0.5rem;
            padding: 0.5rem;
            background-color: rgba(248, 215, 218, 0.5);
            border-radius: 4px;
            font-size: 0.9rem;
        }
        
        /* 照片详情模态框 */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            z-index: 2000;
            overflow-y: auto;
        }
        
        .modal-content {
            background-color: white;
            margin: 3rem auto;
            padding: 2rem;
            border-radius: 8px;
            max-width: 800px;
            width: 90%;
            position: relative;
        }
        
        .close-modal {
            position: absolute;
            top: 1rem;
            right: 1rem;
            font-size: 1.5rem;
            cursor: pointer;
            color: #024059;
        }
        
        .photo-detail {
            display: flex;
            flex-direction: column;
            gap: 2rem;
        }
        
        @media (min-width: 768px) {
            .photo-detail {
                flex-direction: row;
            }
        }
        
        .photo-large {
            flex: 1;
        }
        
        .photo-large img {
            width: 100%;
            max-height: 500px;
            object-fit: contain;
            border-radius: 8px;
        }
        
        /* 详情页无图片样式 */
        .no-image-detail {
            width: 100%;
            height: 400px;
            background-color: #e0e0e0;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #757575;
            font-size: 1.5rem;
            font-weight: bold;
            border-radius: 8px;
        }
        
        .photo-meta {
            flex: 1;
        }
        
        .photo-title {
            font-size: 1.5rem;
            margin-bottom: 1rem;
            color: #024059;
        }
        
        .photo-description {
            margin-bottom: 1.5rem;
            line-height: 1.6;
        }
        
        .photo-stats {
            display: flex;
            gap: 1rem;
            margin-bottom: 1.5rem;
        }
        
        .like-btn {
            background: none;
            border: none;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 1rem;
            color: #024059;
        }
        
        .like-btn.liked {
            color: #e74c3c;
        }
        
        .like-count {
            font-weight: bold;
        }
        
        .comments-section {
            margin-top: 2rem;
        }
        
        .comments-title {
            font-size: 1.2rem;
            margin-bottom: 1rem;
            color: #024059;
        }
        
        .comment-list {
            max-height: 300px;
            overflow-y: auto;
            margin-bottom: 1.5rem;
        }
        
        .comment-item {
            padding: 0.8rem 0;
            border-bottom: 1px solid #eee;
        }
        
        .comment-author {
            font-weight: bold;
            margin-bottom: 0.3rem;
        }
        
        .comment-text {
            line-height: 1.5;
        }
        
        .comment-form {
            display: flex;
            gap: 1rem;
        }
        
        .comment-input {
            flex: 1;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        
        .comment-submit {
            background-color: #069dbf;
            color: white;
            border: none;
            padding: 0 1.5rem;
            border-radius: 4px;
            cursor: pointer;
        }
        
        /* 条款和政策页面样式 */
        .terms-policy-page {
            padding: 4rem 0;
            background-color: white;
        }
        
        .terms-policy-container {
            max-width: 800px;
            margin: 0 auto;
            padding: 2rem;
            background-color: #f9f9f9;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        .terms-policy-title {
            font-size: 2rem;
            margin-bottom: 2rem;
            color: #024059;
            text-align: center;
        }
        
        .terms-policy-content {
            line-height: 1.8;
        }
        
        .terms-policy-content h2 {
            font-size: 1.5rem;
            margin: 2rem 0 1rem;
            color: #024059;
        }
        
        .terms-policy-content p {
            margin-bottom: 1rem;
        }
        
        .terms-policy-content ul {
            margin-bottom: 1rem;
            padding-left: 2rem;
        }
        
        footer {
            background-color: #024059;
            color: white;
            text-align: center;
            padding: 2rem 0;
            margin-top: 2rem;
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            .nav-links {
                display: none;
            }
            
            .hero h1 {
                font-size: 2rem;
            }
            
            .photo-grid {
                grid-template-columns: 1fr;
            }
            
            .upload-container {
                padding: 1rem;
            }
            
            .photo-detail {
                flex-direction: column;
            }
        }
    </style>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
</head>
<body>
    <header>
        <div class="container">
            <nav>
                <div class="logo">BE YOU PHOTOS</div>
                <ul class="nav-links">
                    <li><a href="#home">首页</a></li>
                    <li><a href="#gallery">作品集</a></li>
                    <li><a href="#upload">上传作品</a></li>
                    <li><a href="#about">关于我们</a></li>
                    <li><a href="#contact">联系</a></li>
                </ul>
            </nav>
        </div>
    </header>
    
    <section class="hero" id="home">
        <div class="hero-content">
            <h1>展现真实的你</h1>
            <p>BE YOU PHOTOS - 捕捉生活瞬间</p>
            <a href="#gallery" class="btn">查看作品</a>
        </div>
    </section>
    
    <section class="gallery" id="gallery">
        <div class="container">
            <h2 class="section-title">我们的作品</h2>
            <div class="photo-grid" id="photoGrid">
                <!-- 照片将通过JavaScript动态加载 -->
            </div>
        </div>
    </section>
    
    <section class="upload-section" id="upload">
        <div class="container">
            <h2 class="section-title">上传你的作品</h2>
            <div class="upload-container">
                <form class="upload-form" id="uploadForm">
                    <div class="form-group">
                        <label for="photoTitle">作品标题</label>
                        <input type="text" id="photoTitle" name="photoTitle" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="photoDescription">作品描述</label>
                        <textarea id="photoDescription" name="photoDescription" required></textarea>
                    </div>
                    
                    <div class="form-group">
                        <label for="photoCategory">作品类别</label>
                        <select id="photoCategory" name="photoCategory" required>
                            <option value="">请选择类别</option>
                            <option value="portrait">个性人像</option>
                            <option value="landscape">自然风光</option>
                            <option value="documentary">人文纪实</option>
                            <option value="creative">创意摄影</option>
                            <option value="event">活动摄影</option>
                            <option value="love">LOVE</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label>上传照片</label>
                        <div class="file-upload" id="fileUploadArea">
                            <i class="fas fa-cloud-upload-alt"></i>
                            <p>点击或拖拽文件到此处上传</p>
                            <p>支持 JPG, PNG 格式，最大 5MB</p>
                            <input type="file" id="fileInput" accept="image/jpeg, image/png" required>
                        </div>
                        <div class="preview-container" id="previewContainer">
                            <p>预览:</p>
                            <img class="preview-image" id="previewImage">
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label>
                            <input type="checkbox" id="termsCheckbox" name="termsCheckbox" required>
                            我同意 <a href="terms.html" style="color: #069dbf;">服务条款</a> 和 <a href="privacy.html" style="color: #069dbf;">隐私政策</a>
                        </label>
                    </div>
                    
                    <button type="submit" class="upload-btn" id="uploadBtn" disabled>提交审核</button>
                    
                    <div class="status-message" id="statusMessage"></div>
                </form>
            </div>
        </div>
    </section>
    
    <!-- 照片详情模态框 -->
    <div class="modal" id="photoModal">
        <div class="modal-content">
            <span class="close-modal" id="closeModal">&times;</span>
            <div class="photo-detail" id="photoDetail">
                <!-- 内容将通过JavaScript动态加载 -->
            </div>
        </div>
    </div>
    
    <footer>
        <div class="container">
            <p>&copy; 2025 BE YOU PHOTOS. 保留所有权利.</p>
            <p><a href="terms.html" style="color: white;">服务条款</a> | <a href="privacy.html" style="color: white;">隐私政策</a></p>
        </div>
    </footer>
    
    <script>
        // 照片数据
        const photos = [
            {
                id: 1,
                title: '个性人像',
                description: '展现你独特的个性',
                url: null, // 设置为null表示无图片
                category: 'portrait',
                status: 'approved',
                likes: 42,
                liked: false,
                comments: [
                    { id: 1, author: '摄影爱好者', text: '期待看到更多个性人像作品！' },
                    { id: 2, author: '艺术评论家', text: '这个分类很有潜力，等待上传。' }
                ]
            },
            {
                id: 2,
                title: '自然风光',
                description: '发现旅途中的美丽',
                url: 'https://images.unsplash.com/photo-1506744038136-46273834b3fb',
                category: 'landscape',
                status: 'approved',
                likes: 28,
                liked: false,
                comments: [
                    { id: 1, author: '旅行达人', text: '这是在哪里拍的？太美了！' },
                    { id: 2, author: '户外爱好者', text: '色彩和构图都太棒了！' }
                ]
            },
            {
                id: 3,
                title: '人文纪实',
                description: '捕捉最真实的瞬间',
                url: 'https://images.unsplash.com/photo-1527689368864-3a821dbccc34',
                category: 'documentary',
                status: 'approved',
                likes: 35,
                liked: false,
                comments: [
                    { id: 1, author: '社会观察者', text: '这张照片讲述了一个深刻的故事。' }
                ]
            },
            {
                id: 4,
                title: '创意摄影',
                description: '突破常规的视觉表达',
                url: null, // 设置为null表示无图片
                category: 'creative',
                status: 'approved',
                likes: 56,
                liked: false,
                comments: [
                    { id: 1, author: '创意总监', text: '创意摄影需要更多作品展示！' },
                    { id: 2, author: '设计师', text: '期待看到有创意的作品。' }
                ]
            },
            {
                id: 5,
                title: 'LOVE',
                description: '记录你们的美好时光',
                url: null, // 设置为null表示无图片
                category: 'love',
                status: 'approved',
                likes: 89,
                liked: false,
                comments: [
                    { id: 1, author: '浪漫主义者', text: '等待上传爱的瞬间！' }
                ]
            },
            {
                id: 6,
                title: '活动摄影',
                description: '精彩瞬间不容错过',
                url: 'https://images.unsplash.com/photo-1540575467063-178a50c2df87',
                category: 'event',
                status: 'approved',
                likes: 17,
                liked: false,
                comments: [
                    { id: 1, author: '活动策划', text: '完美捕捉了活动的氛围！' }
                ]
            }
        ];
        
        // 用户上传的照片 (模拟数据库)
        let userUploads = [];
        
        // 审核拒绝原因列表
        const rejectionReasons = [
            "照片内容不符合社区准则",
            "照片质量不达标（模糊、过暗等）",
            "包含不适当的内容",
            "涉嫌侵犯他人版权",
            "标题或描述不符合要求"
        ];
        
        // DOM 元素
        const fileUploadArea = document.getElementById('fileUploadArea');
        const fileInput = document.getElementById('fileInput');
        const previewContainer = document.getElementById('previewContainer');
        const previewImage = document.getElementById('previewImage');
        const uploadForm = document.getElementById('uploadForm');
        const uploadBtn = document.getElementById('uploadBtn');
        const statusMessage = document.getElementById('statusMessage');
        const photoGrid = document.getElementById('photoGrid');
        const photoModal = document.getElementById('photoModal');
        const closeModal = document.getElementById('closeModal');
        const photoDetail = document.getElementById('photoDetail');
        const termsPage = document.getElementById('termsPage');
        const privacyPage = document.getElementById('privacyPage');
        
        // 当前查看的照片ID
        let currentPhotoId = null;
        
        // 检查URL参数，判断是否显示条款或隐私页面
        function checkUrlParams() {
            const urlParams = new URLSearchParams(window.location.search);
            const page = urlParams.get('page');
            
            if (page === 'terms') {
                showTermsPage();
            } else if (page === 'privacy') {
                showPrivacyPage();
            }
        }
        
        // 显示服务条款页面
        function showTermsPage() {
            document.querySelectorAll('section, footer').forEach(el => el.style.display = 'none');
            termsPage.style.display = 'block';
        }
        
        // 隐藏服务条款页面
        function hideTermsPage() {
            termsPage.style.display = 'none';
            document.querySelectorAll('section, footer').forEach(el => el.style.display = 'block');
            history.pushState(null, '', window.location.pathname);
        }
        
        // 显示隐私政策页面
        function showPrivacyPage() {
            document.querySelectorAll('section, footer').forEach(el => el.style.display = 'none');
            privacyPage.style.display = 'block';
        }
        
        // 隐藏隐私政策页面
        function hidePrivacyPage() {
            privacyPage.style.display = 'none';
            document.querySelectorAll('section, footer').forEach(el => el.style.display = 'block');
            history.pushState(null, '', window.location.pathname);
        }
        
        // 加载照片到网格
        function loadPhotos() {
            // 清空现有内容
            photoGrid.innerHTML = '';
            
            // 加载示例照片
            photos.forEach(photo => {
                const photoItem = createPhotoItem(photo);
                photoGrid.appendChild(photoItem);
            });
            
            // 加载用户上传的照片
            userUploads.forEach(photo => {
                const photoItem = createPhotoItem(photo);
                photoGrid.appendChild(photoItem);
            });
        }
        
        // 创建照片项
        function createPhotoItem(photo) {
            const photoItem = document.createElement('div');
            photoItem.className = 'photo-item';
            photoItem.dataset.id = photo.id;
            
            let statusBadge = '';
            if (photo.status !== 'approved') {
                const statusText = photo.status === 'pending' ? '审核中' : '未通过';
                const statusClass = photo.status === 'pending' ? 'status-pending' : 'status-rejected';
                statusBadge = `<span class="status-indicator ${statusClass}">${statusText}</span>`;
            }
            
            let rejectionReason = '';
            if (photo.status === 'rejected' && photo.rejectionReason) {
                rejectionReason = `<div class="rejection-reason">拒绝原因: ${photo.rejectionReason}</div>`;
            }
            
            // 判断是否有图片，没有则显示灰色背景和提示文字
            const imageContent = photo.url 
                ? `<img src="${photo.url}" alt="${photo.title}">`
                : `<div class="no-image-placeholder">无图片上传</div>`;
            
            photoItem.innerHTML = `
                ${imageContent}
                <div class="photo-info">
                    <h3>${photo.title} ${statusBadge}</h3>
                    <p>${photo.description}</p>
                    ${rejectionReason}
                </div>
            `;
            
            // 添加点击事件打开详情模态框
            photoItem.addEventListener('click', () => {
                openPhotoDetail(photo.id);
            });
            
            return photoItem;
        }
        
        // 打开照片详情
        function openPhotoDetail(photoId) {
            currentPhotoId = photoId;
            
            // 合并示例照片和用户上传照片
            const allPhotos = [...photos, ...userUploads];
            const photo = allPhotos.find(p => p.id == photoId);
            
            if (!photo) return;
            
            // 判断是否有图片，没有则显示灰色背景和提示文字
            const imageContent = photo.url 
                ? `<img src="${photo.url}" alt="${photo.title}">`
                : `<div class="no-image-detail">无图片上传</div>`;
            
            // 构建详情内容
            photoDetail.innerHTML = `
                <div class="photo-large">
                    ${imageContent}
                </div>
                <div class="photo-meta">
                    <h2 class="photo-title">${photo.title}</h2>
                    <p class="photo-description">${photo.description}</p>
                    
                    <div class="photo-stats">
                        <button class="like-btn ${photo.liked ? 'liked' : ''}" id="likeBtn">
                            <i class="fas fa-heart"></i>
                            <span class="like-count">${photo.likes}</span>
                        </button>
                    </div>
                    
                    <div class="comments-section">
                        <h3 class="comments-title">评论 (${photo.comments.length})</h3>
                        <div class="comment-list" id="commentList">
                            ${photo.comments.map(comment => `
                                <div class="comment-item">
                                    <div class="comment-author">${comment.author}</div>
                                    <div class="comment-text">${comment.text}</div>
                                </div>
                            `).join('')}
                        </div>
                        
                        <form class="comment-form" id="commentForm">
                            <input type="text" class="comment-input" id="commentInput" placeholder="写下你的评论..." required>
                            <button type="submit" class="comment-submit">发送</button>
                        </form>
                    </div>
                </div>
            `;
            
            // 添加点赞事件
            const likeBtn = document.getElementById('likeBtn');
            if (likeBtn) {
                likeBtn.addEventListener('click', () => {
                    toggleLike(photoId);
                });
            }
            
            // 添加评论事件
            const commentForm = document.getElementById('commentForm');
            if (commentForm) {
                commentForm.addEventListener('submit', (e) => {
                    e.preventDefault();
                    addComment(photoId);
                });
            }
            
            // 显示模态框
            photoModal.style.display = 'block';
            document.body.style.overflow = 'hidden';
        }
        
        // 关闭照片详情
        function closePhotoDetail() {
            photoModal.style.display = 'none';
            document.body.style.overflow = 'auto';
        }
        
        // 切换点赞状态
        function toggleLike(photoId) {
            // 合并示例照片和用户上传照片
            const allPhotos = [...photos, ...userUploads];
            const photo = allPhotos.find(p => p.id == photoId);
            
            if (!photo) return;
            
            photo.liked = !photo.liked;
            photo.likes += photo.liked ? 1 : -1;
            
            // 更新UI
            const likeBtn = document.getElementById('likeBtn');
            if (likeBtn) {
                likeBtn.classList.toggle('liked');
                const likeCount = likeBtn.querySelector('.like-count');
                if (likeCount) {
                    likeCount.textContent = photo.likes;
                }
            }
            
            // 更新网格中的照片
            loadPhotos();
        }
        
        // 添加评论
        function addComment(photoId) {
            const commentInput = document.getElementById('commentInput');
            const commentText = commentInput.value.trim();
            
            if (!commentText) return;
            
            // 合并示例照片和用户上传照片
            const allPhotos = [...photos, ...userUploads];
            const photo = allPhotos.find(p => p.id == photoId);
            
            if (!photo) return;
            
            // 创建新评论
            const newComment = {
                id: Date.now(),
                author: '我', // 实际应用中应该是登录用户的名字
                text: commentText
            };
            
            photo.comments.push(newComment);
            
            // 更新评论列表
            const commentList = document.getElementById('commentList');
            if (commentList) {
                const commentItem = document.createElement('div');
                commentItem.className = 'comment-item';
                commentItem.innerHTML = `
                    <div class="comment-author">${newComment.author}</div>
                    <div class="comment-text">${newComment.text}</div>
                `;
                commentList.appendChild(commentItem);
            }
            
            // 清空输入框
            commentInput.value = '';
            
            // 更新网格中的照片
            loadPhotos();
        }
        
        // 文件上传区域点击事件
        fileUploadArea.addEventListener('click', () => {
            fileInput.click();
        });
        
        // 拖放功能
        fileUploadArea.addEventListener('dragover', (e) => {
            e.preventDefault();
            fileUploadArea.style.backgroundColor = 'rgba(6, 157, 191, 0.2)';
        });
        
        fileUploadArea.addEventListener('dragleave', () => {
            fileUploadArea.style.backgroundColor = 'rgba(6, 157, 191, 0.05)';
        });
        
        fileUploadArea.addEventListener('drop', (e) => {
            e.preventDefault();
            fileUploadArea.style.backgroundColor = 'rgba(6, 157, 191, 0.05)';
            
            if (e.dataTransfer.files.length) {
                fileInput.files = e.dataTransfer.files;
                handleFileSelect();
            }
        });
        
        // 文件选择变化事件
        fileInput.addEventListener('change', handleFileSelect);
        
        function handleFileSelect() {
            const file = fileInput.files[0];
            
            if (file) {
                // 检查文件类型
                if (!['image/jpeg', 'image/png'].includes(file.type)) {
                    showStatus('请上传 JPG 或 PNG 格式的图片', 'error');
                    return;
                }
                
                // 检查文件大小 (5MB)
                if (file.size > 5 * 1024 * 1024) {
                    showStatus('图片大小不能超过 5MB', 'error');
                    return;
                }
                
                // 显示预览
                const reader = new FileReader();
                reader.onload = (e) => {
                    previewImage.src = e.target.result;
                    previewContainer.style.display = 'block';
                    checkFormValidity();
                };
                reader.readAsDataURL(file);
            }
        }
        
        // 检查表单有效性
        function checkFormValidity() {
            const isFormValid = uploadForm.checkValidity();
            uploadBtn.disabled = !isFormValid;
        }
        
        // 表单输入变化事件
        uploadForm.addEventListener('input', checkFormValidity);
        
        // 表单提交事件
        uploadForm.addEventListener('submit', (e) => {
            e.preventDefault();
            
            // 禁用提交按钮
            uploadBtn.disabled = true;
            showStatus('正在上传并审核您的作品...', 'processing');
            
            // 模拟上传和审核过程
            setTimeout(() => {
                // 创建新照片对象
                const newPhoto = {
                    id: Date.now(),
                    title: document.getElementById('photoTitle').value,
                    description: document.getElementById('photoDescription').value,
                    category: document.getElementById('photoCategory').value,
                    url: previewImage.src,
                    status: 'pending', // 初始状态为审核中
                    likes: 0,
                    liked: false,
                    comments: []
                };
                
                // 添加到用户上传列表
                userUploads.push(newPhoto);
                
                // 模拟自动审核 (随机通过或拒绝)
                setTimeout(() => {
                    // 80% 通过率
                    const isApproved = Math.random() < 0.8;
                    newPhoto.status = isApproved ? 'approved' : 'rejected';
                    
                    // 如果拒绝，添加拒绝原因
                    if (!isApproved) {
                        const randomReason = rejectionReasons[Math.floor(Math.random() * rejectionReasons.length)];
                        newPhoto.rejectionReason = randomReason;
                    }
                    
                    // 重新加载照片
                    loadPhotos();
                    
                    // 显示审核结果
                    if (isApproved) {
                        showStatus('恭喜！您的作品已通过审核并发布。', 'success');
                    } else {
                        showStatus(`很遗憾，您的作品未通过审核。原因: ${newPhoto.rejectionReason}`, 'error');
                    }
                }, 2000);
                
                // 重置表单
                uploadForm.reset();
                previewContainer.style.display = 'none';
                checkFormValidity();
            }, 1500);
        });
        
        // 显示状态消息
        function showStatus(message, type) {
            statusMessage.textContent = message;
            statusMessage.className = `status-message ${type}`;
            statusMessage.style.display = 'block';
            
            // 3秒后自动隐藏
            if (type !== 'processing') {
                setTimeout(() => {
                    statusMessage.style.display = 'none';
                }, 5000);
            }
        }
        
        // 平滑滚动
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault();
                
                document.querySelector(this.getAttribute('href')).scrollIntoView({
                    behavior: 'smooth'
                });
            });
        });
        
        // 关闭模态框事件
        closeModal.addEventListener('click', closePhotoDetail);
        
        // 点击模态框外部关闭
        window.addEventListener('click', (e) => {
            if (e.target === photoModal) {
                closePhotoDetail();
            }
        });
        
        // 页面加载完成后执行
        window.addEventListener('DOMContentLoaded', () => {
            loadPhotos();
            checkUrlParams();
        });
    </script>
</body>
</html>
