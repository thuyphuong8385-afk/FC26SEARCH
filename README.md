<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EA SPORTS FC 26 - Search Players</title>
    <style>
        :root {
            --bg-primary: #0a0e17;
            --bg-card: rgba(20, 27, 45, 0.7);
            --bg-card-hover: rgba(32, 43, 70, 0.9);
            --accent-green: #00ff87;
            --accent-cyan: #02d8e9;
            --accent-gold: #ffd700;
            --text-main: #ffffff;
            --text-muted: #8c9ba5;
            --border-color: rgba(255, 255, 255, 0.1);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', -apple-system, BlinkMacSystemFont, Roboto, sans-serif;
            user-select: none;
        }

        body {
            background-color: var(--bg-primary);
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(2, 216, 233, 0.15) 0%, transparent 40%),
                radial-gradient(circle at 90% 80%, rgba(0, 255, 135, 0.1) 0%, transparent 40%);
            color: var(--text-main);
            min-height: 100vh;
            padding: 30px;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        /* Header */
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            border-bottom: 2px solid var(--accent-cyan);
            padding-bottom: 15px;
        }

        h1 {
            font-size: 28px;
            text-transform: uppercase;
            letter-spacing: 2px;
            background: linear-gradient(45deg, #fff, var(--accent-cyan));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .fc-logo {
            background: var(--accent-green);
            color: #000;
            font-weight: 900;
            padding: 2px 8px;
            font-style: italic;
            border-radius: 4px;
        }

        /* Search & Filter Bar */
        .search-bar {
            display: flex;
            gap: 15px;
            margin-bottom: 25px;
            background: var(--bg-card);
            padding: 15px;
            border-radius: 12px;
            backdrop-filter: blur(10px);
            border: 1px solid var(--border-color);
        }

        .search-input {
            flex: 1;
            background: rgba(0, 0, 0, 0.4);
            border: 1px solid var(--border-color);
            padding: 12px 20px;
            border-radius: 8px;
            color: #fff;
            font-size: 16px;
            outline: none;
            transition: 0.3s;
        }

        .search-input:focus {
            border-color: var(--accent-cyan);
            box-shadow: 0 0 10px rgba(2, 216, 233, 0.3);
        }

        /* Players Grid */
        .players-list {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        /* Player Card */
        .player-card {
            display: grid;
            grid-template-columns: 260px 1fr 140px;
            background: var(--bg-card);
            border-radius: 12px;
            border: 1px solid var(--border-color);
            padding: 15px 20px;
            align-items: center;
            transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
            position: relative;
            overflow: hidden;
            backdrop-filter: blur(10px);
        }

        .player-card::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            height: 100%;
            width: 4px;
            background: transparent;
            transition: 0.3s;
        }

        .player-card:hover {
            transform: translateX(5px);
            background: var(--bg-card-hover);
            border-color: rgba(2, 216, 233, 0.4);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
        }

        .player-card:hover::before {
            background: var(--accent-cyan);
        }

        /* Left Info: Avatar + Rating + Name */
        .player-basic {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .player-avatar {
            width: 70px;
            height: 70px;
            position: relative;
        }

        .player-avatar svg {
            width: 100%;
            height: 100%;
            filter: drop-shadow(0 4px 6px rgba(0,0,0,0.5));
        }

        .ratings {
            display: flex;
            flex-direction: column;
            align-items: center;
            line-height: 1;
        }

        .ovr {
            font-size: 24px;
            font-weight: 800;
            color: var(--accent-green);
        }

        .pot {
            font-size: 13px;
            color: var(--text-muted);
            margin-top: 3px;
        }

        .player-name-container {
            display: flex;
            flex-direction: column;
        }

        .player-name {
            font-size: 18px;
            font-weight: 700;
            color: #fff;
            margin-bottom: 4px;
        }

        .player-meta {
            font-size: 12px;
            color: var(--text-muted);
            display: flex;
            gap: 8px;
            align-items: center;
        }

        .pos-badge {
            background: rgba(255, 255, 255, 0.1);
            padding: 2px 6px;
            border-radius: 4px;
            color: var(--accent-cyan);
            font-weight: 600;
        }

        /* Center Info: Stats, PlayStyles, Contract */
        .player-details {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 15px;
            padding: 0 20px;
            border-left: 1px solid var(--border-color);
            border-right: 1px solid var(--border-color);
        }

        .detail-item {
            display: flex;
            flex-direction: column;
            gap: 4px;
        }

        .detail-label {
            font-size: 11px;
            text-transform: uppercase;
            color: var(--text-muted);
            letter-spacing: 0.5px;
        }

        .detail-value {
            font-size: 14px;
            font-weight: 600;
        }

        /* Stars & Foot */
        .stars {
            color: var(--accent-gold);
            letter-spacing: 2px;
        }

        /* PlayStyles Badges */
        .playstyles {
            display: flex;
            gap: 5px;
            flex-wrap: wrap;
        }

        .playstyle-tag {
            background: linear-gradient(135deg, rgba(2, 216, 233, 0.2), rgba(0, 255, 135, 0.2));
            border: 1px solid rgba(2, 216, 233, 0.4);
            color: #fff;
            font-size: 10px;
            padding: 3px 6px;
            border-radius: 4px;
            font-weight: 600;
        }

        .playstyle-tag.plus {
            background: linear-gradient(135deg, #ffd700, #ff8c00);
            border: none;
            color: #000;
        }

        /* Financials */
        .financial-value {
            color: var(--accent-green);
        }

        /* Right Info: Action Buttons */
        .actions {
            display: flex;
            flex-direction: column;
            gap: 8px;
            padding-left: 15px;
        }

        .btn {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid var(--border-color);
            color: #fff;
            padding: 8px 12px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 12px;
            font-weight: 600;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 6px;
        }

        .btn:hover {
            background: var(--accent-cyan);
            color: #000;
            border-color: var(--accent-cyan);
            box-shadow: 0 0 10px rgba(2, 216, 233, 0.4);
        }

        .btn-shortlist.active {
            background: rgba(255, 215, 0, 0.2);
            border-color: var(--accent-gold);
            color: var(--accent-gold);
        }

        .btn-compare.active {
            background: rgba(0, 255, 135, 0.2);
            border-color: var(--accent-green);
            color: var(--accent-green);
        }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1><span class="fc-logo">FC 26</span> Search Players</h1>
        <div style="font-size: 14px; color: var(--text-muted)">CAREER MODE SCOUTING</div>
    </header>

    <!-- Search Bar -->
    <div class="search-bar">
        <input type="text" id="searchInput" class="search-input" placeholder="Tìm kiếm theo tên cầu thủ, câu lạc bộ, quốc gia..." onkeyup="filterPlayers()">
    </div>

    <!-- Players List Container -->
    <div class="players-list" id="playersContainer">
        <!-- JS sẽ inject danh sách cầu thủ vào đây -->
    </div>
</div>

<script>
    // Dữ liệu giả lập danh sách cầu thủ (Chuẩn FC 26)
    const playersData = [
        {
            id: 1,
            name: "Jude Bellingham",
            pos: "CAM",
            age: 22,
            club: "Real Madrid",
            nation: "England",
            ovr: 90,
            pot: 94,
            preferredFoot: "Phải",
            skillMoves: 4,
            weakFoot: 4,
            playStyles: ["Relentless+", "Technical", "Intercept"],
            value: "€145.5M",
            wage: "€320K",
            contract: "2029",
            avatarColor: "#3b82f6"
        },
        {
            id: 2,
            name: "Lamine Yamal",
            pos: "RW",
            age: 18,
            club: "FC Barcelona",
            nation: "Spain",
            ovr: 84,
            pot: 93,
            preferredFoot: "Trái",
            skillMoves: 5,
            weakFoot: 3,
            playStyles: ["Finesse Shot+", "Trickster", "Quick Step"],
            value: "€85.0M",
            wage: "€95K",
            contract: "2028",
            avatarColor: "#ef4444"
        },
        {
            id: 3,
            name: "Kylian Mbappé",
            pos: "ST",
            age: 26,
            club: "Real Madrid",
            nation: "France",
            ovr: 91,
            pot: 92,
            preferredFoot: "Phải",
            skillMoves: 5,
            weakFoot: 4,
            playStyles: ["Rapid+", "Quick Step", "Power Shot"],
            value: "€180.0M",
            wage: "€420K",
            contract: "2029",
            avatarColor: "#10b981"
        },
        {
            id: 4,
            name: "Florian Wirtz",
            pos: "CAM",
            age: 22,
            club: "Bayer Leverkusen",
            nation: "Germany",
            ovr: 88,
            pot: 92,
            preferredFoot: "Phải",
            skillMoves: 4,
            weakFoot: 4,
            playStyles: ["Incisive Pass+", "Technical", "Tiki Taka"],
            value: "€110.0M",
            wage: "€180K",
            contract: "2027",
            avatarColor: "#8b5cf6"
        }
    ];

    // Trạng thái Shortlist & Compare
    const shortlistedIds = new Set();
    const comparedIds = new Set();

    // Hàm tạo SVG Vector Avatar cho cầu thủ
    function generatePlayerSVG(color) {
        return `
        <svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
            <circle cx="50" cy="50" r="45" fill="none" stroke="${color}" stroke-width="2" opacity="0.3"/>
            <path d="M50 20 A 15 15 0 0 1 50 50 A 15 15 0 0 1 50 20 Z" fill="${color}" opacity="0.8"/>
            <path d="M25 80 C 25 60, 75 60, 75 80 Z" fill="${color}" opacity="0.8"/>
        </svg>`;
    }

    // Hàm hiển thị danh sách cầu thủ
    function renderPlayers(players) {
        const container = document.getElementById('playersContainer');
        container.innerHTML = '';

        if(players.length === 0) {
            container.innerHTML = `<div style="text-align:center; padding: 40px; color: var(--text-muted);">Không tìm thấy cầu thủ phù hợp!</div>`;
            return;
        }

        players.forEach(player => {
            const isShortlisted = shortlistedIds.has(player.id);
            const isCompared = comparedIds.has(player.id);

            const card = document.createElement('div');
            card.className = 'player-card';

            card.innerHTML = `
                <!-- Left: Basic Info -->
                <div class="player-basic">
                    <div class="player-avatar">
                        ${generatePlayerSVG(player.avatarColor)}
                    </div>
                    <div class="ratings">
                        <span class="ovr">${player.ovr}</span>
                        <span class="pot">POT ${player.pot}</span>
                    </div>
                    <div class="player-name-container">
                        <div class="player-name">${player.name}</div>
                        <div class="player-meta">
                            <span class="pos-badge">${player.pos}</span>
                            <span>${player.age} tuổi</span> • 
                            <span>${player.club}</span>
                        </div>
                    </div>
                </div>

                <!-- Center: Technical & Financial Details -->
                <div class="player-details">
                    <!-- Technical -->
                    <div class="detail-item">
                        <span class="detail-label">Chân / Kỹ thuật</span>
                        <span class="detail-value"> Chân ${player.preferredFoot}</span>
                        <span class="detail-value" style="font-size:12px;">
                            SM: <span class="stars">${'★'.repeat(player.skillMoves)}</span> | 
                            WF: <span class="stars">${'★'.repeat(player.weakFoot)}</span>
                        </span>
                    </div>

                    <!-- PlayStyles -->
                    <div class="detail-item">
                        <span class="detail-label">PlayStyles</span>
                        <div class="playstyles">
                            ${player.playstyles.map(ps => {
                                const isPlus = ps.endsWith('+');
                                return `<span class="playstyle-tag ${isPlus ? 'plus' : ''}">${ps}</span>`;
                            }).join('')}
                        </div>
                    </div>

                    <!-- Market Value -->
                    <div class="detail-item">
                        <span class="detail-label">Giá mua ước tính</span>
                        <span class="detail-value financial-value">${player.value}</span>
                        <span class="detail-label" style="margin-top:2px;">Lương: ${player.wage}/tuần</span>
                    </div>

                    <!-- Contract -->
                    <div class="detail-item">
                        <span class="detail-label">Thời hạn HĐ</span>
                        <span class="detail-value">${player.contract}</span>
                        <span class="detail-label" style="margin-top:2px;">Quốc tịch: ${player.nation}</span>
                    </div>
                </div>

                <!-- Right: Actions -->
                <div class="actions">
                    <button class="btn btn-shortlist ${isShortlisted ? 'active' : ''}" onclick="toggleShortlist(${player.id})">
                        <svg width="12" height="12" viewBox="0 0 24 24" fill="${isShortlisted ? 'currentColor' : 'none'}" stroke="currentColor" stroke-width="2"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"></polygon></svg>
                        ${isShortlisted ? 'Shortlisted' : 'Shortlist'}
                    </button>
                    <button class="btn btn-compare ${isCompared ? 'active' : ''}" onclick="toggleCompare(${player.id})">
                        <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="16 3 21 3 21 8"></polyline><line x1="4" y1="20" x2="21" y2="3"></line><polyline points="8 21 3 21 3 16"></polyline><line x1="15" y1="15" x2="3" y2="21"></line></svg>
                        ${isCompared ? 'Comparing' : 'Compare'}
                    </button>
                </div>
            `;
            container.appendChild(card);
        });
    }

    // Toggle Shortlist
    function toggleShortlist(id) {
        if(shortlistedIds.has(id)) {
            shortlistedIds.delete(id);
        } else {
            shortlistedIds.add(id);
        }
        filterPlayers();
    }

    // Toggle Compare
    function toggleCompare(id) {
        if(comparedIds.has(id)) {
            comparedIds.delete(id);
        } else {
            if(comparedIds.size >= 2) {
                alert("Bạn chỉ có thể chọn tối đa 2 cầu thủ để Compare!");
                return;
            }
            comparedIds.add(id);
        }
        filterPlayers();
    }

    // Tìm kiếm / Lọc cầu thủ
    function filterPlayers() {
        const query = document.getElementById('searchInput').value.toLowerCase();
        const filtered = playersData.filter(p => 
            p.name.toLowerCase().includes(query) ||
            p.club.toLowerCase().includes(query) ||
            p.nation.toLowerCase().includes(query) ||
            p.pos.toLowerCase().includes(query)
        );
        renderPlayers(filtered);
    }

    // Render lần đầu
    renderPlayers(playersData);
</script>
</body>
</html>
