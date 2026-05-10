# warcraft3-site
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>魔兽争霸 III：冰封王座 - 赛事中心</title>
    <style>
        :root {
            --primary-color: #00a8ff;
            --secondary-color: #1e272e;
            --accent-color: #fbc531;
            --text-color: #ecf0f1;
            --bg-color: #0f1c2e;
            --card-bg: #1e272e;
            --horde-color: #c0392b;
            --alliance-color: #2980b9;
            --undead-color: #8e44ad;
            --nightelf-color: #27ae60;
        }

        [data-theme="light"] {
            --primary-color: #0066cc;
            --secondary-color: #ffffff;
            --accent-color: #d35400;
            --text-color: #2c3e50;
            --bg-color: #f4f6f7;
            --card-bg: #ffffff;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        
        body { background-color: var(--bg-color); color: var(--text-color); transition: all 0.3s ease; }
        
        /* Header */
        header {
            background: linear-gradient(rgba(0,0,0,0.8), rgba(0,0,0,0.8)), url('https://images.unsplash.com/photo-1542751371-adc38448a05e?ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80');
            background-size: cover;
            background-position: center;
            padding: 2rem;
            text-align: center;
            border-bottom: 4px solid var(--accent-color);
        }

        h1 { font-size: 2.5rem; margin-bottom: 0.5rem; text-transform: uppercase; letter-spacing: 2px; color: var(--accent-color); text-shadow: 2px 2px 4px rgba(0,0,0,0.5); }
        .subtitle { font-size: 1.2rem; opacity: 0.9; }

        /* Navigation */
        nav {
            background-color: var(--card-bg);
            padding: 1rem;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 2px 10px rgba(0,0,0,0.3);
            display: flex;
            justify-content: center;
            gap: 2rem;
            flex-wrap: wrap;
        }

        nav button {
            background: none;
            border: none;
            color: var(--text-color);
            font-size: 1.1rem;
            cursor: pointer;
            padding: 0.5rem 1rem;
            border-radius: 5px;
            transition: all 0.3s;
            font-weight: bold;
        }

        nav button:hover, nav button.active {
            background-color: var(--primary-color);
            color: white;
        }

        .theme-toggle {
            position: absolute;
            right: 20px;
            top: 50%;
            transform: translateY(-50%);
            background: var(--accent-color);
            color: #000;
            border: none;
            padding: 0.3rem 0.8rem;
            border-radius: 20px;
            cursor: pointer;
            font-weight: bold;
        }

        /* Main Content */
        main { max-width: 1200px; margin: 2rem auto; padding: 0 1rem; }

        .section { display: none; animation: fadeIn 0.5s; }
        .section.active { display: block; }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* Live Matches */
        .live-badge {
            background-color: #e74c3c;
            color: white;
            padding: 0.2rem 0.6rem;
            border-radius: 4px;
            font-size: 0.8rem;
            font-weight: bold;
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse { 0% { opacity: 1; } 50% { opacity: 0.6; } 100% { opacity: 1; } }

        .match-card {
            background-color: var(--card-bg);
            border-radius: 10px;
            padding: 1.5rem;
            margin-bottom: 1.5rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            border-left: 5px solid var(--primary-color);
        }

        .players { display: flex; align-items: center; gap: 2rem; flex: 1; }
        .player { text-align: center; min-width: 100px; }
        .player-name { font-weight: bold; font-size: 1.2rem; display: block; margin-bottom: 0.5rem; }
        .race-icon { font-size: 2rem; }
        .vs { font-size: 1.5rem; font-weight: bold; color: var(--accent-color); }
        .score { font-size: 1.8rem; font-weight: bold; background: rgba(0,0,0,0.2); padding: 0.5rem 1rem; border-radius: 8px; }
        .match-info { text-align: right; min-width: 150px; }
        .tournament-name { color: var(--primary-color); font-weight: bold; margin-bottom: 0.5rem; }
        .viewers { font-size: 0.9rem; opacity: 0.8; }

        /* Replays & Videos Grid */
        .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); gap: 1.5rem; }
        
        .card {
            background-color: var(--card-bg);
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            transition: transform 0.3s;
        }

        .card:hover { transform: translateY(-5px); }

        .card-img { height: 180px; background-color: #333; display: flex; align-items: center; justify-content: center; color: #777; font-size: 3rem; }
        .card-body { padding: 1.5rem; }
        .card-title { font-size: 1.2rem; margin-bottom: 0.5rem; font-weight: bold; }
        .card-desc { font-size: 0.9rem; opacity: 0.8; margin-bottom: 1rem; line-height: 1.4; }
        .card-meta { display: flex; justify-content: space-between; align-items: center; font-size: 0.85rem; opacity: 0.7; }
        
        .btn {
            display: inline-block;
            background-color: var(--primary-color);
            color: white;
            padding: 0.5rem 1rem;
            border-radius: 5px;
            text-decoration: none;
            font-size: 0.9rem;
            margin-top: 1rem;
            width: 100%;
            text-align: center;
            border: none;
            cursor: pointer;
            transition: background 0.3s;
        }

        .btn:hover { background-color: #0088cc; }
        .btn-outline { background: transparent; border: 1px solid var(--primary-color); color: var(--primary-color); }
        .btn-outline:hover { background: var(--primary-color); color: white; }

        /* Filters */
        .filters { display: flex; gap: 1rem; margin-bottom: 1.5rem; flex-wrap: wrap; }
        .filter-btn {
            background: var(--card-bg);
            border: 1px solid var(--primary-color);
            color: var(--text-color);
            padding: 0.4rem 1rem;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s;
        }
        .filter-btn.active, .filter-btn:hover { background: var(--primary-color); color: white; }

        /* Schedule Table */
        table { width: 100%; border-collapse: collapse; background: var(--card-bg); border-radius: 10px; overflow: hidden; }
        th, td { padding: 1rem; text-align: left; border-bottom: 1px solid rgba(255,255,255,0.1); }
        th { background-color: rgba(0,0,0,0.2); font-weight: bold; color: var(--accent-color); }
        tr:hover { background-color: rgba(255,255,255,0.05); }

        /* Footer */
        footer { text-align: center; padding: 2rem; margin-top: 3rem; border-top: 1px solid rgba(255,255,255,0.1); opacity: 0.7; }

        /* Responsive */
        @media (max-width: 768px) {
            .match-card { flex-direction: column; gap: 1.5rem; text-align: center; }
            .players { justify-content: center; }
            .match-info { text-align: center; }
            nav { gap: 1rem; }
            .theme-toggle { position: static; transform: none; margin-top: 1rem; }
        }
    </style>
</head>
<body>

<header>
    <h1>Warcraft III: The Frozen Throne</h1>
    <div class="subtitle">全球赛事资讯 · 高清录像 · 精彩视频</div>
</header>

<nav>
    <button class="nav-btn active" data-target="live">🔴 实时赛事</button>
    <button class="nav-btn" data-target="replays">💾 比赛录像</button>
    <button class="nav-btn" data-target="videos">📺 比赛视频</button>
    <button class="nav-btn" data-target="schedule">📅 近期赛程</button>
    <button class="theme-toggle" id="themeToggle">🌙 切换主题</button>
</nav>

<main>
    <!-- Live Section -->
    <section id="live" class="section active">
        <h2 style="margin-bottom: 1.5rem; border-left: 4px solid var(--accent-color); padding-left: 1rem;">正在直播</h2>
        <div id="live-matches" class="matches-container">
            <!-- Matches injected by JS -->
        </div>
    </section>

    <!-- Replays Section -->
    <section id="replays" class="section">
        <h2 style="margin-bottom: 1.5rem; border-left: 4px solid var(--accent-color); padding-left: 1rem;">最新录像下载</h2>
        <div class="filters">
            <button class="filter-btn active" data-filter="all">全部</button>
            <button class="filter-btn" data-filter="HUM">人族 (HUM)</button>
            <button class="filter-btn" data-filter="ORC">兽族 (ORC)</button>
            <button class="filter-btn" data-filter="UND">不死 (UND)</button>
            <button class="filter-btn" data-filter="NE">暗夜 (NE)</button>
        </div>
        <div id="replays-grid" class="grid">
            <!-- Replays injected by JS -->
        </div>
    </section>

    <!-- Videos Section -->
    <section id="videos" class="section">
        <h2 style="margin-bottom: 1.5rem; border-left: 4px solid var(--accent-color); padding-left: 1rem;">高光时刻 & 战术复盘</h2>
        <div id="videos-grid" class="grid">
            <!-- Videos injected by JS -->
        </div>
    </section>

    <!-- Schedule Section -->
    <section id="schedule" class="section">
        <h2 style="margin-bottom: 1.5rem; border-left: 4px solid var(--accent-color); padding-left: 1rem;">未来 7 天赛程</h2>
        <div style="overflow-x: auto;">
            <table id="schedule-table">
                <thead>
                    <tr>
                        <th>日期/时间</th>
                        <th>赛事名称</th>
                        <th>对阵双方</th>
                        <th>直播平台</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Schedule injected by JS -->
                </tbody>
            </table>
        </div>
    </section>
</main>

<footer>
    <p>© 2023 魔兽争霸 III 赛事中心 | 非官方网站，仅供粉丝交流</p>
    <p style="font-size: 0.8rem; margin-top: 0.5rem;">Warcraft III is a trademark of Blizzard Entertainment.</p>
</footer>

<script>
    // Mock Data
    const liveMatches = [
        {
            id: 1,
            tournament: "WCL 2023 Season Final",
            player1: { name: "Lyn", race: "ORC", icon: "🐗" },
            player2: { name: "Happy", race: "UND", icon: "💀" },
            score: "2 - 1",
            viewers: "12,450",
            status: "Live Map 4"
        },
        {
            id: 2,
            tournament: "Kuaishou Cup",
            player1: { name: "Infi", race: "HUM", icon: "⚔️" },
            player2: { name: "Moon", race: "NE", icon: "🌙" },
            score: "0 - 0",
            viewers: "8,320",
            status: "Starting Soon"
        },
        {
            id: 3,
            tournament: "EH Cup #45",
            player1: { name: "Sok", race: "HUM", icon: "⚔️" },
            player2: { name: "Fly100%", race: "ORC", icon: "🐗" },
            score: "1 - 2",
            viewers: "5,100",
            status: "Live Map 4"
        }
    ];

    const replays = [
        { id: 1, title: "Lyn vs Happy - WCL Final Game 5", map: "Turtle Rock", date: "2023-10-25", races: ["ORC", "UND"], size: "2.4 MB" },
        { id: 2, title: "Moon vs Infi - Semi Final", map: "Lost Temple", date: "2023-10-24", races: ["NE", "HUM"], size: "1.8 MB" },
        { id: 3, title: "Romantic vs Lawliet - Group Stage", map: "Echo Isles", date: "2023-10-23", races: ["ORC", "NE"], size: "3.1 MB" },
        { id: 4, title: "TH000 vs 120 - Quarter Final", map: "Twisted Meadows", date: "2023-10-22", races: ["HUM", "UND"], size: "2.2 MB" },
        { id: 5, title: "Focus vs Hawk - Daily Cup", map: "Gnoll Wood", date: "2023-10-21", races: ["ORC", "HUM"], size: "1.5 MB" },
        { id: 6, title: "Remind vs Son - Classic Match", map: "Plunder Isle", date: "2023-10-20", races: ["NE", "ORC"], size: "2.8 MB" }
    ];

    const videos = [
        { id: 1, title: "Top 10 Micro Moments - October 2023", desc: "盘点本月最精彩的微操瞬间，包括 Lyn 的极限拉扯。", duration: "12:45", views: "45K" },
        { id: 2, title: "Happy vs Infi - Full Series Analysis", desc: "专业解说深度复盘 WCL 半决赛不死对人族的战术细节。", duration: "28:30", views: "32K" },
        { id: 3, title: "How to Defend Tower Rush as Orc", desc: "兽族对抗人族塔 rush 的终极教学指南。", duration: "08:15", views: "18K" },
        { id: 4, title: "Moon's Night Elf Build Order Guide", desc: "月神最新的暗夜精灵开局流程详解。", duration: "15:20", views: "27K" }
    ];

    const schedule = [
        { date: "2023-10-26 19:00", tournament: "WCL 2023 Grand Final", match: "Lyn vs Happy", platform: "Twitch / Bilibili" },
        { date: "2023-10-27 20:00", tournament: "Kuaishou Cup", match: "Infi vs Moon", platform: "Huya" },
        { date: "2023-10-28 18:00", tournament: "EH Cup Weekly", match: "Open Qualifiers", platform: "Twitch" },
        { date: "2023-10-29 15:00", tournament: "Gold League", match: "Group Stage Day 1", platform: "Bilibili" },
        { date: "2023-10-30 21:00", tournament: "1v1 Ladder King", match: "Top 8 Playoff", platform: "Douyu" }
    ];

    // DOM Elements
    const navBtns = document.querySelectorAll('.nav-btn');
    const sections = document.querySelectorAll('.section');
    const themeToggle = document.getElementById('themeToggle');
    
    // Initialization
    function init() {
        renderLiveMatches();
        renderReplays('all');
        renderVideos();
        renderSchedule();
        setupEventListeners();
    }

    // Render Functions
    function renderLiveMatches() {
        const container = document.getElementById('live-matches');
        container.innerHTML = liveMatches.map(match => `
            <div class="match-card">
                <div class="players">
                    <div class="player">
                        <span class="player-name">${match.player1.name}</span>
                        <span class="race-icon">${match.player1.icon}</span>
                    </div>
                    <div class="vs">VS</div>
                    <div class="player">
                        <span class="player-name">${match.player2.name}</span>
                        <span class="race-icon">${match.player2.icon}</span>
                    </div>
                </div>
                <div class="score">${match.score}</div>
                <div class="match-info">
                    <div class="tournament-name">${match.tournament}</div>
                    <div class="live-badge">● ${match.status}</div>
                    <div class="viewers">👁 ${match.viewers} watching</div>
                    <button class="btn" style="margin-top: 10px; padding: 0.3rem 0.8rem; font-size: 0.8rem;">Watch Live</button>
                </div>
            </div>
        `).join('');
    }

    function renderReplays(filter) {
        const container = document.getElementById('replays-grid');
        const filtered = filter === 'all' ? replays : replays.filter(r => r.races.includes(filter));
        
        if (filtered.length === 0) {
            container.innerHTML = '<p style="grid-column: 1/-1; text-align: center; padding: 2rem;">暂无该种族录像</p>';
            return;
        }

        container.innerHTML = filtered.map(replay => `
            <div class="card">
                <div class="card-img">💾</div>
                <div class="card-body">
                    <div class="card-title">${replay.title}</div>
                    <div class="card-desc">Map: ${replay.map} | Date: ${replay.date}</div>
                    <div class="card-meta">
                        <span>${replay.races.join(' vs ')}</span>
                        <span>${replay.size}</span>
                    </div>
                    <button class="btn btn-outline" onclick="alert('开始下载: ${replay.title}.w3g')">Download .w3g</button>
                </div>
            </div>
        `).join('');
    }

    function renderVideos() {
        const container = document.getElementById('videos-grid');
        container.innerHTML = videos.map(video => `
            <div class="card">
                <div class="card-img" style="background: #222; color: #fff;">▶️</div>
                <div class="card-body">
                    <div class="card-title">${video.title}</div>
                    <div class="card-desc">${video.desc}</div>
                    <div class="card-meta">
                        <span>⏱ ${video.duration}</span>
                        <span>👁 ${video.views}</span>
                    </div>
                    <button class="btn" onclick="alert('播放视频: ${video.title}')">Watch Video</button>
                </div>
            </div>
        `).join('');
    }

    function renderSchedule() {
        const tbody = document.querySelector('#schedule-table tbody');
        tbody.innerHTML = schedule.map(item => `
            <tr>
                <td>${item.date}</td>
                <td><strong>${item.tournament}</strong></td>
                <td>${item.match}</td>
                <td>${item.platform}</td>
            </tr>
        `).join('');
    }

    // Event Listeners
    function setupEventListeners() {
        // Navigation
        navBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                navBtns.forEach(b => b.classList.remove('active'));
                sections.forEach(s => s.classList.remove('active'));
                
                btn.classList.add('active');
                document.getElementById(btn.dataset.target).classList.add('active');
            });
        });

        // Theme Toggle
        themeToggle.addEventListener('click', () => {
            const current = document.documentElement.getAttribute('data-theme');
            const newTheme = current === 'light' ? 'dark' : 'light';
            document.documentElement.setAttribute('data-theme', newTheme);
            themeToggle.textContent = newTheme === 'light' ? '☀️ 浅色模式' : '🌙 深色模式';
        });

        // Replay Filters
        document.querySelectorAll('.filter-btn').forEach(btn => {
            btn.addEventListener('click', () => {
                document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
                renderReplays(btn.dataset.filter);
            });
        });
    }

    // Start App
    init();
</script>

</body>
</html>
