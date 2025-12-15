<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BinnApps - Semua cara berinteraksi, dalam satu tempat.</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #1d9bf0;
            --primary-dark: #0d7abf;
            --dark-bg: #000000;
            --dark-card: #151515;
            --dark-border: #333333;
            --text-primary: #ffffff;
            --text-secondary: #b3b3b3;
            --success: #00ba7c;
            --danger: #f91880;
            --warning: #ffad1f;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--dark-bg);
            color: var(--text-primary);
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Header */
        header {
            background-color: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(10px);
            position: sticky;
            top: 0;
            z-index: 100;
            border-bottom: 1px solid var(--dark-border);
        }

        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 0;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 12px;
            font-size: 24px;
            font-weight: 800;
            color: var(--primary);
        }

        .logo i {
            font-size: 28px;
        }

        .search-bar {
            flex: 1;
            max-width: 500px;
            margin: 0 20px;
        }

        .search-bar input {
            width: 100%;
            padding: 10px 16px;
            border-radius: 24px;
            border: none;
            background-color: var(--dark-card);
            color: var(--text-primary);
            font-size: 14px;
        }

        .search-bar input::placeholder {
            color: var(--text-secondary);
        }

        .nav-icons {
            display: flex;
            gap: 24px;
            align-items: center;
        }

        .nav-icons i {
            font-size: 20px;
            cursor: pointer;
            color: var(--text-secondary);
            transition: color 0.2s;
        }

        .nav-icons i:hover {
            color: var(--text-primary);
        }

        .user-avatar {
            width: 32px;
            height: 32px;
            border-radius: 50%;
            background: linear-gradient(45deg, var(--primary), var(--success));
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            cursor: pointer;
        }

        /* Main Content */
        .main-content {
            display: flex;
            gap: 20px;
            padding: 20px 0;
        }

        /* Sidebar */
        .sidebar {
            width: 280px;
            display: flex;
            flex-direction: column;
            gap: 4px;
        }

        .sidebar-item {
            display: flex;
            align-items: center;
            gap: 16px;
            padding: 12px 16px;
            border-radius: 12px;
            cursor: pointer;
            color: var(--text-secondary);
            transition: all 0.2s;
        }

        .sidebar-item:hover {
            background-color: var(--dark-card);
            color: var(--text-primary);
        }

        .sidebar-item.active {
            background-color: var(--dark-card);
            color: var(--primary);
        }

        .sidebar-item i {
            font-size: 20px;
        }

        .sidebar-bottom {
            margin-top: auto;
            padding: 16px;
            background-color: var(--dark-card);
            border-radius: 16px;
        }

        .create-post-btn {
            background: linear-gradient(45deg, var(--primary), var(--success));
            color: white;
            border: none;
            padding: 12px 16px;
            border-radius: 12px;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 12px;
            width: 100%;
            transition: transform 0.2s;
        }

        .create-post-btn:hover {
            transform: scale(1.02);
        }

        /* Feed */
        .feed {
            flex: 1;
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .feed-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-bottom: 16px;
            border-bottom: 1px solid var(--dark-border);
        }

        .feed-tabs {
            display: flex;
            gap: 16px;
        }

        .feed-tab {
            padding: 8px 16px;
            border-radius: 20px;
            cursor: pointer;
            color: var(--text-secondary);
        }

        .feed-tab.active {
            background-color: var(--dark-card);
            color: var(--text-primary);
        }

        /* Post */
        .post {
            background-color: var(--dark-card);
            border-radius: 16px;
            padding: 16px;
            border: 1px solid var(--dark-border);
        }

        .post-header {
            display: flex;
            gap: 12px;
            margin-bottom: 12px;
        }

        .post-avatar {
            width: 48px;
            height: 48px;
            border-radius: 50%;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 18px;
            cursor: pointer;
        }

        .post-info {
            flex: 1;
            cursor: pointer;
        }

        .post-username {
            font-weight: 700;
            margin-bottom: 2px;
            display: flex;
            align-items: center;
            gap: 4px;
        }

        .verified-badge {
            color: var(--primary);
            font-size: 14px;
        }

        .post-handle {
            color: var(--text-secondary);
            font-size: 14px;
        }

        .post-time {
            color: var(--text-secondary);
            font-size: 14px;
        }

        .post-content {
            margin: 12px 0;
            line-height: 1.5;
        }

        .post-actions {
            display: flex;
            justify-content: space-around;
            padding-top: 16px;
            border-top: 1px solid var(--dark-border);
            margin-top: 16px;
        }

        .post-action {
            display: flex;
            align-items: center;
            gap: 8px;
            color: var(--text-secondary);
            cursor: pointer;
            padding: 8px 16px;
            border-radius: 20px;
            transition: all 0.2s;
        }

        .post-action:hover {
            background-color: rgba(255, 255, 255, 0.05);
            color: var(--text-primary);
        }

        .post-action.like:hover {
            color: var(--danger);
        }

        .post-action.repost:hover {
            color: var(--success);
        }

        .post-action.comment:hover {
            color: var(--primary);
        }

        .post-action.share:hover {
            color: var(--warning);
        }

        /* Comments Section */
        .comments-section {
            margin-top: 16px;
            padding-top: 16px;
            border-top: 1px solid var(--dark-border);
        }

        .comment-input {
            display: flex;
            gap: 12px;
            margin-bottom: 12px;
        }

        .comment-input input {
            flex: 1;
            padding: 8px 12px;
            border-radius: 20px;
            border: 1px solid var(--dark-border);
            background-color: var(--dark-card);
            color: var(--text-primary);
        }

        .comment-input button {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 20px;
            cursor: pointer;
        }

        .comment {
            display: flex;
            gap: 12px;
            margin-bottom: 12px;
            padding: 12px;
            background-color: rgba(255, 255, 255, 0.02);
            border-radius: 12px;
        }

        .comment-avatar {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            background: linear-gradient(45deg, #f093fb, #f5576c);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 14px;
            cursor: pointer;
        }

        .comment-content {
            flex: 1;
        }

        .comment-author {
            font-weight: 600;
            margin-bottom: 4px;
            display: flex;
            align-items: center;
            gap: 4px;
        }

        .comment-handle {
            color: var(--text-secondary);
            font-size: 12px;
        }

        .comment-text {
            color: var(--text-primary);
            font-size: 14px;
        }

        .comment-time {
            color: var(--text-secondary);
            font-size: 12px;
            margin-top: 4px;
        }

        /* Right Sidebar */
        .right-sidebar {
            width: 300px;
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .trending {
            background-color: var(--dark-card);
            border-radius: 16px;
            padding: 16px;
            border: 1px solid var(--dark-border);
        }

        .trending-header {
            font-weight: 700;
            margin-bottom: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .trending-item {
            padding: 12px 0;
            border-bottom: 1px solid var(--dark-border);
            cursor: pointer;
        }

        .trending-item:last-child {
            border-bottom: none;
        }

        .trending-category {
            color: var(--text-secondary);
            font-size: 14px;
            margin-bottom: 4px;
        }

        .trending-topic {
            font-weight: 600;
        }

        .trending-count {
            color: var(--text-secondary);
            font-size: 14px;
            margin-top: 4px;
        }

        .suggestions {
            background-color: var(--dark-card);
            border-radius: 16px;
            padding: 16px;
            border: 1px solid var(--dark-border);
        }

        .suggestions-header {
            font-weight: 700;
            margin-bottom: 16px;
        }

        .suggestion-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px 0;
            border-bottom: 1px solid var(--dark-border);
            cursor: pointer;
        }

        .suggestion-item:last-child {
            border-bottom: none;
        }

        .suggestion-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: linear-gradient(45deg, #f093fb, #f5576c);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 14px;
        }

        .suggestion-info {
            flex: 1;
        }

        .suggestion-name {
            font-weight: 600;
            margin-bottom: 2px;
            display: flex;
            align-items: center;
            gap: 4px;
        }

        .suggestion-mutual {
            color: var(--text-secondary);
            font-size: 12px;
        }

        .follow-btn {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 12px;
            font-size: 12px;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .follow-btn:hover {
            background-color: var(--primary-dark);
        }

        /* Auth Screens */
        .auth-screen {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: var(--dark-bg);
            padding: 20px;
        }

        .auth-container {
            background-color: var(--dark-card);
            border-radius: 24px;
            padding: 40px;
            width: 100%;
            max-width: 450px;
            border: 1px solid var(--dark-border);
        }

        .auth-header {
            text-align: center;
            margin-bottom: 32px;
        }

        .auth-logo {
            font-size: 32px;
            font-weight: 800;
            color: var(--primary);
            margin-bottom: 8px;
        }

        .auth-tagline {
            color: var(--text-secondary);
            font-size: 16px;
        }

        .auth-form {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .auth-input {
            padding: 14px 16px;
            border-radius: 24px;
            border: 1px solid var(--dark-border);
            background-color: var(--dark-bg);
            color: var(--text-primary);
            font-size: 16px;
        }

        .auth-input::placeholder {
            color: var(--text-secondary);
        }

        .auth-btn {
            padding: 14px;
            border-radius: 24px;
            border: none;
            font-weight: 600;
            font-size: 16px;
            cursor: pointer;
            transition: transform 0.2s;
        }

        .auth-btn:hover {
            transform: translateY(-2px);
        }

        .login-btn {
            background: linear-gradient(45deg, var(--primary), var(--success));
            color: white;
        }

        .register-btn {
            background-color: var(--dark-border);
            color: var(--text-primary);
        }

        .guest-btn {
            background: none;
            color: var(--primary);
            border: 1px solid var(--primary);
        }

        .auth-switch {
            text-align: center;
            color: var(--text-secondary);
            margin-top: 16px;
        }

        .auth-switch a {
            color: var(--primary);
            text-decoration: none;
            font-weight: 600;
        }

        /* Profile Screen */
        .profile-header {
            background-color: var(--dark-card);
            border-radius: 24px;
            padding: 32px;
            margin-bottom: 24px;
            border: 1px solid var(--dark-border);
            text-align: center;
        }

        .profile-avatar {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            background: linear-gradient(45deg, var(--primary), var(--success));
            margin: 0 auto 24px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 48px;
        }

        .profile-name {
            font-size: 24px;
            font-weight: 700;
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .profile-handle {
            color: var(--primary);
            font-size: 18px;
            margin-bottom: 16px;
        }

        .profile-bio {
            color: var(--text-secondary);
            margin-bottom: 24px;
            line-height: 1.6;
        }

        .profile-stats {
            display: flex;
            justify-content: space-around;
            padding: 16px;
            background-color: rgba(255, 255, 255, 0.05);
            border-radius: 16px;
            margin-bottom: 24px;
        }

        .stat-item {
            text-align: center;
        }

        .stat-number {
            font-size: 20px;
            font-weight: 700;
            margin-bottom: 4px;
        }

        .stat-label {
            color: var(--text-secondary);
            font-size: 14px;
        }

        .logout-btn {
            width: 100%;
            padding: 16px;
            background-color: var(--danger);
            color: white;
            border: none;
            border-radius: 16px;
            font-weight: 600;
            font-size: 16px;
            cursor: pointer;
        }

        /* Post Modal */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0, 0, 0, 0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
        }

        .modal-content {
            background-color: var(--dark-card);
            border-radius: 24px;
            padding: 32px;
            width: 90%;
            max-width: 500px;
            border: 1px solid var(--dark-border);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
        }

        .modal-title {
            font-size: 20px;
            font-weight: 700;
        }

        .close-btn {
            background: none;
            border: none;
            color: var(--text-secondary);
            font-size: 24px;
            cursor: pointer;
        }

        .modal-input {
            width: 100%;
            padding: 16px;
            border-radius: 16px;
            border: 1px solid var(--dark-border);
            background-color: var(--dark-bg);
            color: var(--text-primary);
            font-size: 16px;
            resize: vertical;
            min-height: 120px;
            margin-bottom: 24px;
        }

        .modal-actions {
            display: flex;
            gap: 16px;
        }

        .modal-cancel {
            flex: 1;
            padding: 12px;
            background-color: var(--dark-border);
            color: var(--text-primary);
            border: none;
            border-radius: 12px;
            font-weight: 600;
            cursor: pointer;
        }

        .modal-post {
            flex: 1;
            padding: 12px;
            background: linear-gradient(45deg, var(--primary), var(--success));
            color: white;
            border: none;
            border-radius: 12px;
            font-weight: 600;
            cursor: pointer;
        }

        /* Hidden elements */
        .hidden {
            display: none;
        }

        /* Bottom Navigation */
        .bottom-nav {
            display: none;
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background-color: rgba(0, 0, 0, 0.9);
            backdrop-filter: blur(10px);
            border-top: 1px solid var(--dark-border);
            padding: 12px 0;
        }

        .bottom-nav-items {
            display: flex;
            justify-content: space-around;
            align-items: center;
        }

        .bottom-nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
            color: var(--text-secondary);
            font-size: 12px;
        }

        .bottom-nav-item.active {
            color: var(--primary);
        }

        .bottom-nav-item i {
            font-size: 20px;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .main-content {
                flex-direction: column;
            }
            
            .sidebar, .right-sidebar {
                width: 100%;
            }
            
            .search-bar {
                display: none;
            }
            
            .bottom-nav {
                display: flex;
            }
            
            .header-content {
                padding: 12px 16px;
            }
            
            .auth-container {
                padding: 24px;
            }
        }

        @media (max-width: 480px) {
            .nav-icons i:not(:last-child) {
                display: none;
            }
            
            .logo span {
                display: none;
            }
        }
    </style>
</head>
<body>
    <!-- Auth Screen (Default) -->
    <div id="authScreen" class="auth-screen">
        <div class="auth-container">
            <div class="auth-header">
                <div class="auth-logo">BinnApps</div>
                <div class="auth-tagline">Semua cara berinteraksi, dalam satu tempat.</div>
            </div>
            <div class="auth-form">
                <input type="email" id="loginEmail" placeholder="Email" class="auth-input">
                <input type="password" id="loginPassword" placeholder="Password" class="auth-input">
                <button id="loginBtn" class="auth-btn login-btn">Masuk</button>
                <button id="registerBtn" class="auth-btn register-btn">Daftar</button>
                <button id="guestBtn" class="auth-btn guest-btn">Lanjut tanpa akun</button>
                <div class="auth-switch">
                    <a href="#" id="switchToRegister">Belum punya akun? Daftar</a>
                </div>
            </div>
        </div>
    </div>

    <!-- Register Screen -->
    <div id="registerScreen" class="auth-screen hidden">
        <div class="auth-container">
            <div class="auth-header">
                <div class="auth-logo">BinnApps</div>
                <div class="auth-tagline">Semua cara berinteraksi, dalam satu tempat.</div>
            </div>
            <div class="auth-form">
                <input type="text" id="registerName" placeholder="Nama Lengkap" class="auth-input">
                <input type="email" id="registerEmail" placeholder="Email" class="auth-input">
                <input type="password" id="registerPassword" placeholder="Password" class="auth-input">
                <input type="password" id="registerConfirmPassword" placeholder="Konfirmasi Password" class="auth-input">
                <button id="createAccountBtn" class="auth-btn login-btn">Buat Akun</button>
                <button id="backToLoginBtn" class="auth-btn register-btn">Sudah punya akun? Masuk</button>
            </div>
        </div>
    </div>

    <!-- Main App (Hidden by default) -->
    <div id="mainApp" class="hidden">
        <!-- Header -->
        <header>
            <div class="container">
                <div class="header-content">
                    <div class="logo">
                        <i class="fas fa-infinity"></i>
                        <span>BinnApps</span>
                    </div>
                    <div class="search-bar">
                        <input type="text" id="searchInput" placeholder="Cari di BinnApps...">
                    </div>
                    <div class="nav-icons">
                        <i class="fas fa-home" id="homeNav"></i>
                        <i class="fas fa-hashtag" id="searchNav"></i>
                        <i class="far fa-bell" id="notificationsNav"></i>
                        <i class="far fa-envelope" id="messagesNav"></i>
                        <div class="user-avatar" id="profileNav">U</div>
                    </div>
                </div>
            </div>
        </header>

        <!-- Main Content -->
        <div class="container">
            <div class="main-content">
                <!-- Left Sidebar -->
                <div class="sidebar">
                    <div class="sidebar-item active" id="homeSidebar">
                        <i class="fas fa-home"></i>
                        <span>Beranda</span>
                    </div>
                    <div class="sidebar-item" id="searchSidebar">
                        <i class="fas fa-hashtag"></i>
                        <span>Topik</span>
                    </div>
                    <div class="sidebar-item" id="communitiesSidebar">
                        <i class="fas fa-users"></i>
                        <span>Komunitas</span>
                    </div>
                    <div class="sidebar-item" id="reelsSidebar">
                        <i class="fas fa-video"></i>
                        <span>Reels</span>
                    </div>
                    <div class="sidebar-item" id="bookmarksSidebar">
                        <i class="fas fa-bookmark"></i>
                        <span>Disimpan</span>
                    </div>
                    <div class="sidebar-item" id="profileSidebar">
                        <i class="fas fa-user"></i>
                        <span>Profil</span>
                    </div>
                    
                    <div class="sidebar-bottom">
                        <button class="create-post-btn" id="createPostBtn">
                            <i class="fas fa-plus"></i>
                            Buat Postingan
                        </button>
                    </div>
                </div>

                <!-- Feed -->
                <div class="feed" id="feedContent">
                    <!-- Posts will be dynamically inserted here -->
                </div>

                <!-- Right Sidebar -->
                <div class="right-sidebar">
                    <div class="trending">
                        <div class="trending-header">
                            <i class="fas fa-fire"></i>
                            <span>Trending di Indonesia</span>
                        </div>
                        <div class="trending-item">
                            <div class="trending-category">Teknologi · Trending</div>
                            <div class="trending-topic">#AppleM3</div>
                            <div class="trending-count">42.1K posts</div>
                        </div>
                        <div class="trending-item">
                            <div class="trending-category">Olahraga · Trending</div>
                            <div class="trending-topic">#PialaDuniaU20</div>
                            <div class="trending-count">28.7K posts</div>
                        </div>
                        <div class="trending-item">
                            <div class="trending-category">Hiburan · Trending</div>
                            <div class="trending-topic">#OppenheimerMovie</div>
                            <div class="trending-count">19.3K posts</div>
                        </div>
                    </div>

                    <div class="suggestions">
                        <div class="suggestions-header">Orang yang Mungkin Anda Kenal</div>
                        <div class="suggestion-item" data-user-id="dev1">
                            <div class="suggestion-avatar">B</div>
                            <div class="suggestion-info">
                                <div class="suggestion-name">
                                    BinnApps Developer
                                    <span class="verified-badge">✓</span>
                                </div>
                                <div class="suggestion-mutual">4 koneksi bersama</div>
                            </div>
                            <button class="follow-btn">Ikuti</button>
                        </div>
                        <div class="suggestion-item" data-user-id="1">
                            <div class="suggestion-avatar">A</div>
                            <div class="suggestion-info">
                                <div class="suggestion-name">Ahmad Rizki</div>
                                <div class="suggestion-mutual">2 koneksi bersama</div>
                            </div>
                            <button class="follow-btn">Ikuti</button>
                        </div>
                        <div class="suggestion-item" data-user-id="2">
                            <div class="suggestion-avatar">S</div>
                            <div class="suggestion-info">
                                <div class="suggestion-name">Sarah Wijaya</div>
                                <div class="suggestion-mutual">7 koneksi bersama</div>
                            </div>
                            <button class="follow-btn">Ikuti</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Profile Screen (Hidden by default) -->
        <div id="profileScreen" class="container hidden">
            <div class="profile-header">
                <div class="profile-avatar" id="profileAvatar">B</div>
                <div class="profile-name" id="profileName">
                    BinnApps Developer
                    <span class="verified-badge">✓</span>
                </div>
                <div class="profile-handle" id="profileHandle">@binndev</div>
                <div class="profile-bio" id="profileBio">
                    Official Developer - BinnApps Platform
                </div>
                <div class="profile-stats">
                    <div class="stat-item">
                        <div class="stat-number" id="profilePosts">0</div>
                        <div class="stat-label">Posting</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-number" id="profileFollowing">0</div>
                        <div class="stat-label">Mengikuti</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-number" id="profileFollowers">1.000.000</div>
                        <div class="stat-label">Pengikut</div>
                    </div>
                </div>
                <button class="logout-btn" id="logoutBtn">Logout</button>
            </div>
        </div>
    </div>

    <!-- Post Modal -->
    <div id="postModal" class="modal hidden">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">Buat Postingan</div>
                <button class="close-btn" id="closePostModal">×</button>
            </div>
            <textarea class="modal-input" id="postContent" placeholder="Apa yang sedang terjadi?"></textarea>
            <div class="modal-actions">
                <button class="modal-cancel" id="cancelPost">Batal</button>
                <button class="modal-post" id="submitPost">Posting</button>
            </div>
        </div>
    </div>

    <!-- Comments Modal -->
    <div id="commentsModal" class="modal hidden">
        <div class="modal-content">
            <div class="modal-header">
                <div class="modal-title">Komentar</div>
                <button class="close-btn" id="closeCommentsModal">×</button>
            </div>
            <div class="comment-input">
                <input type="text" id="commentInput" placeholder="Tulis komentar...">
                <button id="submitComment">Kirim</button>
            </div>
            <div id="commentsList">
                <!-- Comments will be dynamically inserted here -->
            </div>
        </div>
    </div>

    <!-- Bottom Navigation -->
    <div class="bottom-nav">
        <div class="bottom-nav-items">
            <div class="bottom-nav-item active" id="bottomHome">
                <i class="fas fa-home"></i>
                <span>Beranda</span>
            </div>
            <div class="bottom-nav-item" id="bottomSearch">
                <i class="fas fa-search"></i>
                <span>Cari</span>
            </div>
            <div class="bottom-nav-item" id="bottomPost">
                <i class="fas fa-plus-circle"></i>
                <span>Post</span>
            </div>
            <div class="bottom-nav-item" id="bottomMessages">
                <i class="far fa-envelope"></i>
                <span>Chat</span>
            </div>
            <div class="bottom-nav-item" id="bottomProfile">
                <i class="fas fa-user"></i>
                <span>Profil</span>
            </div>
        </div>
    </div>

    <script>
        // Mock data for BinnApps
        const users = {
            'dev1': {
                id: 'dev1',
                name: 'BinnApps Developer',
                username: 'binndev',
                password: 'binnprst1123',
                bio: 'Official Developer - BinnApps Platform',
                followers: 1000000,
                following: 0,
                posts: 0,
                isDeveloper: true,
                verified: true
            },
            '1': {
                id: '1',
                name: 'Ahmad Rizki',
                username: 'ahmadrizki45',
                password: 'password123',
                bio: 'AI Enthusiast & Developer',
                followers: 1250,
                following: 842,
                posts: 0,
                isDeveloper: false,
                verified: false
            },
            '2': {
                id: '2',
                name: 'Sarah Wijaya',
                username: 'sarahwijaya78',
                password: 'sarahpass',
                bio: 'Travel Blogger & Photographer',
                followers: 2340,
                following: 567,
                posts: 0,
                isDeveloper: false,
                verified: false
            }
        };

        let posts = [
            {
                id: '1',
                authorId: '1',
                username: 'Ahmad Rizki',
                handle: '@ahmadrizki45',
                content: 'Baru saja menyelesaikan proyek AI yang sangat menarik! Gabungan antara machine learning dan computer vision untuk deteksi dini penyakit tanaman. Siapa yang tertarik kolaborasi?',
                likes: 156,
                likedBy: ['dev1'],
                comments: 2,
                commentList: [
                    {
                        id: 'c1',
                        authorId: 'dev1',
                        author: 'BinnApps Developer',
                        authorHandle: '@binndev',
                        content: 'Keren banget! Ini bisa jadi game changer di bidang pertanian. Mau kolaborasi?',
                        time: '1 jam yang lalu'
                    },
                    {
                        id: 'c2',
                        authorId: '2',
                        author: 'Sarah Wijaya',
                        authorHandle: '@sarahwijaya78',
                        content: 'Wah keren! Boleh juga dong diajari cara buatnya?',
                        time: '45 menit yang lalu'
                    }
                ],
                reposts: 1,
                repostedBy: ['dev1'],
                time: '2 jam yang lalu',
                isDeveloper: false
            },
            {
                id: '2',
                authorId: '2',
                username: 'Sarah Wijaya',
                handle: '@sarahwijaya78',
                content: 'Hari ini cuaca sempurna untuk jalan-jalan ke taman kota! 🌸 Siapa yang mau ikut weekend ini? #WeekendVibes #Jakarta',
                likes: 89,
                likedBy: [],
                comments: 1,
                commentList: [
                    {
                        id: 'c3',
                        authorId: '1',
                        author: 'Ahmad Rizki',
                        authorHandle: '@ahmadrizki45',
                        content: 'Asik! Boleh ikut juga?',
                        time: '30 menit yang lalu'
                    }
                ],
                reposts: 0,
                repostedBy: [],
                time: '4 jam yang lalu',
                isDeveloper: false
            }
        ];

        let currentUser = null;
        let currentScreen = 'auth';
        let currentPostId = null;

        // DOM Elements
        const elements = {
            authScreen: document.getElementById('authScreen'),
            registerScreen: document.getElementById('registerScreen'),
            mainApp: document.getElementById('mainApp'),
            profileScreen: document.getElementById('profileScreen'),
            feedContent: document.getElementById('feedContent'),
            postModal: document.getElementById('postModal'),
            commentsModal: document.getElementById('commentsModal'),
            profileAvatar: document.getElementById('profileAvatar'),
            profileName: document.getElementById('profileName'),
            profileHandle: document.getElementById('profileHandle'),
            profileBio: document.getElementById('profileBio'),
            profilePosts: document.getElementById('profilePosts'),
            profileFollowing: document.getElementById('profileFollowing'),
            profileFollowers: document.getElementById('profileFollowers')
        };

        // Initialize the app
        function initApp() {
            // Auth screen event listeners
            document.getElementById('loginBtn').addEventListener('click', handleLogin);
            document.getElementById('registerBtn').addEventListener('click', () => {
                elements.authScreen.classList.add('hidden');
                elements.registerScreen.classList.remove('hidden');
            });
            document.getElementById('guestBtn').addEventListener('click', handleGuestLogin);
            document.getElementById('switchToRegister').addEventListener('click', (e) => {
                e.preventDefault();
                elements.authScreen.classList.add('hidden');
                elements.registerScreen.classList.remove('hidden');
            });

            // Register screen event listeners
            document.getElementById('createAccountBtn').addEventListener('click', handleRegister);
            document.getElementById('backToLoginBtn').addEventListener('click', () => {
                elements.registerScreen.classList.add('hidden');
                elements.authScreen.classList.remove('hidden');
            });

            // Main app event listeners
            document.getElementById('createPostBtn').addEventListener('click', showPostModal);
            document.getElementById('closePostModal').addEventListener('click', hidePostModal);
            document.getElementById('cancelPost').addEventListener('click', hidePostModal);
            document.getElementById('submitPost').addEventListener('click', createPost);

            document.getElementById('closeCommentsModal').addEventListener('click', hideCommentsModal);
            document.getElementById('submitComment').addEventListener('click', addComment);

            // Navigation event listeners
            document.getElementById('homeNav').addEventListener('click', () => showScreen('home'));
            document.getElementById('profileNav').addEventListener('click', () => showScreen('profile'));
            document.getElementById('profileSidebar').addEventListener('click', () => showScreen('profile'));
            document.getElementById('logoutBtn').addEventListener('click', handleLogout);

            // Bottom nav
            document.getElementById('bottomHome').addEventListener('click', () => showScreen('home'));
            document.getElementById('bottomProfile').addEventListener('click', () => showScreen('profile'));
            document.getElementById('bottomPost').addEventListener('click', showPostModal);

            // Profile suggestions
            document.querySelectorAll('.suggestion-item').forEach(item => {
                item.addEventListener('click', function() {
                    const userId = this.getAttribute('data-user-id');
                    viewUserProfile(userId);
                });
            });
        }

        // Auth Functions
        function handleLogin() {
            const email = document.getElementById('loginEmail').value;
            const password = document.getElementById('loginPassword').value;
            
            if (email === 'binndev@gmail.com' && password === 'binnprst1123') {
                currentUser = users.dev1;
                loginSuccess();
                return;
            }
            
            // Check other users
            const userKey = Object.keys(users).find(key => {
                const user = users[key];
                const userEmail = `${user.username}@gmail.com`;
                return userEmail === email && user.password === password;
            });
            
            if (userKey) {
                currentUser = users[userKey];
                loginSuccess();
            } else {
                alert('Email atau password salah!');
            }
        }

        function handleRegister() {
            const name = document.getElementById('registerName').value;
            const email = document.getElementById('registerEmail').value;
            const password = document.getElementById('registerPassword').value;
            const confirmPassword = document.getElementById('registerConfirmPassword').value;
            
            if (!name || !email || !password) {
                alert('Semua field harus diisi');
                return;
            }
            
            if (password.length < 6) {
                alert('Password minimal 6 karakter');
                return;
            }
            
            if (password !== confirmPassword) {
                alert('Password dan konfirmasi password tidak cocok');
                return;
            }
            
            if (!email.includes('@')) {
                alert('Email tidak valid');
                return;
            }
            
            // Generate username
            const baseUsername = name.toLowerCase().replace(/\s+/g, '');
            const randomNumbers = Math.floor(10 + Math.random() * 90);
            const username = `${baseUsername}${randomNumbers}`;
            
            const newUser = {
                id: `user${Date.now()}`,
                name: name,
                username: username,
                password: password,
                bio: 'Pengguna BinnApps',
                followers: 0,
                following: 0,
                posts: 0,
                isDeveloper: false,
                verified: false
            };
            
            currentUser = newUser;
            loginSuccess();
        }

        function handleGuestLogin() {
            currentUser = null;
            showScreen('home');
            elements.authScreen.classList.add('hidden');
            elements.mainApp.classList.remove('hidden');
        }

        function loginSuccess() {
            elements.authScreen.classList.add('hidden');
            elements.mainApp.classList.remove('hidden');
            showScreen('home');
            renderFeed();
        }

        function handleLogout() {
            currentUser = null;
            elements.profileScreen.classList.add('hidden');
            elements.mainApp.classList.add('hidden');
            elements.authScreen.classList.remove('hidden');
            document.getElementById('loginEmail').value = '';
            document.getElementById('loginPassword').value = '';
        }

        // Screen Navigation
        function showScreen(screen) {
            currentScreen = screen;
            
            if (screen === 'home') {
                elements.feedContent.classList.remove('hidden');
                elements.profileScreen.classList.add('hidden');
                updateActiveNav('home');
                renderFeed();
            } else if (screen === 'profile') {
                elements.feedContent.classList.add('hidden');
                elements.profileScreen.classList.remove('hidden');
                updateActiveNav('profile');
                renderProfile();
            }
        }

        function updateActiveNav(activeScreen) {
            document.querySelectorAll('.sidebar-item').forEach(item => {
                item.classList.remove('active');
            });
            document.querySelectorAll('.bottom-nav-item').forEach(item => {
                item.classList.remove('active');
            });
            
            if (activeScreen === 'home') {
                document.getElementById('homeSidebar').classList.add('active');
                document.getElementById('bottomHome').classList.add('active');
            } else if (activeScreen === 'profile') {
                document.getElementById('profileSidebar').classList.add('active');
                document.getElementById('bottomProfile').classList.add('active');
            }
        }

        // Post Functions
        function showPostModal() {
            if (!currentUser) {
                alert('Silakan login untuk membuat postingan');
                return;
            }
            elements.postModal.classList.remove('hidden');
        }

        function hidePostModal() {
            elements.postModal.classList.add('hidden');
            document.getElementById('postContent').value = '';
        }

        function createPost() {
            const content = document.getElementById('postContent').value.trim();
            if (!content) {
                alert('Postingan tidak boleh kosong');
                return;
            }
            
            const newPost = {
                id: `post${Date.now()}`,
                authorId: currentUser.id,
                username: currentUser.name,
                handle: `@${currentUser.username}`,
                content: content,
                likes: 0,
                likedBy: [],
                comments: 0,
                commentList: [],
                reposts: 0,
                repostedBy: [],
                time: 'Baru saja',
                isDeveloper: currentUser.isDeveloper || false
            };
            
            posts.unshift(newPost);
            currentUser.posts = (currentUser.posts || 0) + 1;
            
            hidePostModal();
            renderFeed();
        }

        // Comment Functions
        function showCommentsModal(postId) {
            currentPostId = postId;
            elements.commentsModal.classList.remove('hidden');
            renderComments(postId);
        }

        function hideCommentsModal() {
            elements.commentsModal.classList.add('hidden');
            document.getElementById('commentInput').value = '';
            currentPostId = null;
        }

        function addComment() {
            if (!currentUser) {
                alert('Silakan login untuk berkomentar');
                return;
            }
            
            const content = document.getElementById('commentInput').value.trim();
            if (!content) {
                alert('Komentar tidak boleh kosong');
                return;
            }
            
            const comment = {
                id: `c${Date.now()}`,
                authorId: currentUser.id,
                author: currentUser.name,
                authorHandle: `@${currentUser.username}`,
                content: content,
                time: 'Baru saja'
            };
            
            const post = posts.find(p => p.id === currentPostId);
            if (post) {
                post.comments += 1;
                post.commentList.push(comment);
                renderComments(currentPostId);
                document.getElementById('commentInput').value = '';
            }
        }

        // Render Functions
        function renderFeed() {
            let feedHTML = '';
            
            posts.forEach(post => {
                const isLiked = post.likedBy.includes(currentUser?.id);
                const likeClass = isLiked ? 'color: #f91880;' : '';
                const likeText = isLiked ? '❤️' : '♡';
                
                feedHTML += `
                    <div class="post">
                        <div class="post-header">
                            <div class="post-avatar" onclick="viewUserProfile('${post.authorId}')">${post.username.charAt(0)}</div>
                            <div class="post-info" onclick="viewUserProfile('${post.authorId}')">
                                <div class="post-username">
                                    ${post.username}
                                    ${post.isDeveloper ? '<span class="verified-badge">✓</span>' : ''}
                                </div>
                                <div class="post-handle">${post.handle}</div>
                            </div>
                            <div class="post-time">${post.time}</div>
                        </div>
                        <div class="post-content">${post.content}</div>
                        <div class="post-actions">
                            <div class="post-action comment" onclick="showCommentsModal('${post.id}')">
                                <i class="far fa-comment"></i>
                                <span>${post.comments}</span>
                            </div>
                            <div class="post-action repost">
                                <i class="fas fa-retweet"></i>
                                <span>${post.reposts}</span>
                            </div>
                            <div class="post-action like" style="${likeClass}" onclick="toggleLike('${post.id}')">
                                ${likeText}
                                <span>${post.likes}</span>
                            </div>
                            <div class="post-action share">
                                <i class="fas fa-share"></i>
                            </div>
                        </div>
                    </div>
                `;
            });
            
            elements.feedContent.innerHTML = feedHTML;
        }

        function renderComments(postId) {
            const post = posts.find(p => p.id === postId);
            if (!post) return;
            
            let commentsHTML = '';
            post.commentList.forEach(comment => {
                const user = users[comment.authorId] || { name: comment.author, isDeveloper: false };
                commentsHTML += `
                    <div class="comment">
                        <div class="comment-avatar" onclick="viewUserProfile('${comment.authorId}')">${comment.author.charAt(0)}</div>
                        <div class="comment-content">
                            <div class="comment-author">
                                ${comment.author}
                                ${user.isDeveloper ? '<span class="verified-badge">✓</span>' : ''}
                            </div>
                            <div class="comment-handle">${comment.authorHandle}</div>
                            <div class="comment-text">${comment.content}</div>
                            <div class="comment-time">${comment.time}</div>
                        </div>
                    </div>
                `;
            });
            
            document.getElementById('commentsList').innerHTML = commentsHTML;
        }

        function renderProfile() {
            const profile = currentUser || users.dev1;
            elements.profileAvatar.textContent = profile.name.charAt(0);
            elements.profileName.innerHTML = `${profile.name} ${profile.verified ? '<span class="verified-badge">✓</span>' : ''}`;
            elements.profileHandle.textContent = `@${profile.username}`;
            elements.profileBio.textContent = profile.bio;
            elements.profilePosts.textContent = profile.posts || 0;
            elements.profileFollowing.textContent = profile.following;
            elements.profileFollowers.textContent = profile.followers.toLocaleString('id-ID');
        }

        // Global functions for onclick attributes
        function toggleLike(postId) {
            if (!currentUser) {
                alert('Silakan login untuk menyukai postingan');
                return;
            }
            
            const post = posts.find(p => p.id === postId);
            if (!post) return;
            
            const alreadyLiked = post.likedBy.includes(currentUser.id);
            if (alreadyLiked) {
                post.likes -= 1;
                post.likedBy = post.likedBy.filter(id => id !== currentUser.id);
            } else {
                post.likes += 1;
                post.likedBy.push(currentUser.id);
            }
            
            renderFeed();
        }

        function viewUserProfile(userId) {
            const user = users[userId];
            if (user) {
                currentUser = user;
                showScreen('profile');
            }
        }

        function showCommentsModal(postId) {
            window.currentPostId = postId;
            document.getElementById('commentsModal').classList.remove('hidden');
            renderComments(postId);
        }

        // Initialize the app when DOM is loaded
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>

