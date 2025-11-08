<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="description" content="The Centre Jamat Khana Phander Boys Scouts Management System">
    <meta name="theme-color" content="#1a4d2e">
    <title>Scouts Management - Phander</title>
    <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='0.9em' font-size='90'>🦅</text></svg>">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, #0a2818 0%, #1a4d2e 50%, #0a2818 100%);
            min-height: 100vh;
            color: #333;
            overflow-x: hidden;
        }

        .header {
            background: linear-gradient(135deg, #c41e3a 0%, #8b1a2e 100%);
            padding: 20px 15px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
            border-bottom: 3px solid #ffd700;
        }

        .header h1 {
            color: white;
            font-size: clamp(1rem, 4vw, 1.4em);
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            margin-bottom: 8px;
            line-height: 1.4;
        }

        .developer {
            color: #ffd700;
            font-size: clamp(0.75rem, 3vw, 0.9em);
            font-weight: 600;
            letter-spacing: 1px;
        }

        .login-container {
            max-width: 400px;
            margin: 40px auto;
            background: rgba(255, 255, 255, 0.95);
            padding: 30px 20px;
            border-radius: 15px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.3);
            margin-left: 15px;
            margin-right: 15px;
        }

        .login-container h2 {
            text-align: center;
            color: #1a4d2e;
            margin-bottom: 25px;
            font-size: 1.5em;
        }

        .main-container {
            max-width: 100%;
            padding: 15px;
            display: none;
            padding-bottom: 80px;
        }

        .dashboard {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 12px;
            margin-bottom: 20px;
        }

        .stat-card {
            background: rgba(255, 255, 255, 0.95);
            padding: 20px 15px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            text-align: center;
            transition: transform 0.2s;
        }

        .stat-card:active {
            transform: scale(0.98);
        }

        .stat-card.red { border-left: 4px solid #c41e3a; }
        .stat-card.green { border-left: 4px solid #1a4d2e; }
        .stat-card.yellow { border-left: 4px solid #ffd700; }
        .stat-card.blue { border-left: 4px solid #1e3a8a; }

        .stat-number {
            font-size: 2.2em;
            font-weight: bold;
            color: #c41e3a;
            margin-bottom: 5px;
        }

        .stat-label {
            color: #555;
            font-weight: 600;
            font-size: 0.9em;
        }

        .nav-buttons {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin-bottom: 20px;
        }

        .nav-btn {
            padding: 12px 10px;
            background: linear-gradient(135deg, #1a4d2e 0%, #2d5a3d 100%);
            color: white;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-size: 0.9em;
            font-weight: 700;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
            transition: all 0.2s;
        }

        .nav-btn:active {
            transform: scale(0.95);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #c41e3a 0%, #8b1a2e 100%);
            box-shadow: 0 6px 15px rgba(196, 30, 58, 0.4);
        }

        .section {
            background: rgba(255, 255, 255, 0.95);
            padding: 20px 15px;
            border-radius: 15px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.2);
            display: none;
            margin-bottom: 20px;
        }

        .section.active {
            display: block;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .section h2 {
            color: #1a4d2e;
            margin-bottom: 20px;
            font-size: 1.4em;
            border-bottom: 2px solid #ffd700;
            padding-bottom: 10px;
        }

        .form-group {
            margin-bottom: 18px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #1a4d2e;
            font-weight: 700;
            font-size: 0.95em;
        }

        input, select, textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
            background: white;
            font-family: inherit;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: #1a4d2e;
            box-shadow: 0 0 0 3px rgba(26, 77, 46, 0.1);
        }

        .btn {
            background: linear-gradient(135deg, #c41e3a 0%, #8b1a2e 100%);
            color: white;
            padding: 14px 30px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-size: 1em;
            font-weight: 700;
            box-shadow: 0 4px 12px rgba(196, 30, 58, 0.3);
            width: 100%;
            margin-top: 10px;
            transition: transform 0.2s;
        }

        .btn:active {
            transform: scale(0.98);
        }

        .table-container {
            overflow-x: auto;
            margin-top: 20px;
            border-radius: 10px;
            -webkit-overflow-scrolling: touch;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background: white;
            min-width: 500px;
        }

        th {
            background: linear-gradient(135deg, #1a4d2e 0%, #2d5a3d 100%);
            color: white;
            padding: 12px 8px;
            text-align: left;
            font-weight: 700;
            font-size: 0.85em;
            position: sticky;
            top: 0;
            z-index: 10;
        }

        td {
            padding: 12px 8px;
            border-bottom: 1px solid #f0f0f0;
            font-size: 0.9em;
        }

        tr:hover {
            background: rgba(26, 77, 46, 0.05);
        }

        .delete-btn {
            background: linear-gradient(135deg, #c41e3a, #8b1a2e);
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.85em;
            transition: transform 0.2s;
        }

        .delete-btn:active {
            transform: scale(0.95);
        }

        .patrol-badges {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-top: 20px;
        }

        .patrol-badge {
            padding: 25px 15px;
            border-radius: 12px;
            text-align: center;
            color: white;
            font-weight: bold;
            font-size: 1.1em;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            transition: transform 0.2s;
        }

        .patrol-badge:active {
            transform: scale(0.95);
        }

        .patrol-red { background: linear-gradient(135deg, #c41e3a 0%, #8b1a2e 100%); }
        .patrol-green { background: linear-gradient(135deg, #1a4d2e 0%, #0d2818 100%); }
        .patrol-yellow { background: linear-gradient(135deg, #ffd700 0%, #daa520 100%); color: #333; }
        .patrol-blue { background: linear-gradient(135deg, #1e3a8a 0%, #1e40af 100%); }

        .logout-btn {
            position: fixed;
            bottom: 15px;
            right: 15px;
            background: linear-gradient(135deg, #c41e3a, #8b1a2e);
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-weight: 700;
            font-size: 0.9em;
            box-shadow: 0 4px 15px rgba(196, 30, 58, 0.4);
            z-index: 1000;
            transition: transform 0.2s;
        }

        .logout-btn:active {
            transform: scale(0.95);
        }

        .chart-container {
            background: white;
            padding: 20px 15px;
            border-radius: 12px;
            margin-bottom: 20px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.15);
        }

        .chart-container h3 {
            color: #1a4d2e;
            margin-bottom: 15px;
            font-size: 1.2em;
        }

        .bar-chart {
            display: flex;
            align-items: flex-end;
            justify-content: space-around;
            height: 200px;
            gap: 10px;
            padding: 15px 5px;
        }

        .bar {
            flex: 1;
            background: linear-gradient(to top, #1a4d2e, #2d5a3d);
            border-radius: 8px 8px 0 0;
            position: relative;
            min-width: 40px;
            transition: opacity 0.2s;
        }

        .bar:active {
            opacity: 0.8;
        }

        .bar-label {
            position: absolute;
            bottom: -25px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 0.8em;
            font-weight: 700;
            white-space: nowrap;
            color: #333;
        }

        .bar-value {
            position: absolute;
            top: -20px;
            left: 50%;
            transform: translateX(-50%);
            font-weight: bold;
            font-size: 0.9em;
            color: #c41e3a;
        }

        .search-container {
            margin-bottom: 15px;
        }

        .search-input {
            width: 100%;
            padding: 10px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
        }

        .export-buttons {
            display: flex;
            gap: 8px;
            margin-top: 15px;
            flex-wrap: wrap;
        }

        .export-btn {
            flex: 1;
            min-width: 120px;
            padding: 10px 15px;
            background: linear-gradient(135deg, #1a4d2e, #2d5a3d);
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.85em;
            transition: transform 0.2s;
        }

        .export-btn:active {
            transform: scale(0.95);
        }

        .toast {
            position: fixed;
            bottom: 70px;
            left: 50%;
            transform: translateX(-50%);
            background: linear-gradient(135deg, #1a4d2e, #2d5a3d);
            color: white;
            padding: 12px 20px;
            border-radius: 25px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
            z-index: 2000;
            display: none;
            font-weight: 600;
            font-size: 0.9em;
            max-width: 90%;
            text-align: center;
        }

        .toast.show {
            display: block;
            animation: slideUp 0.3s ease;
        }

        @keyframes slideUp {
            from { transform: translateX(-50%) translateY(20px); opacity: 0; }
            to { transform: translateX(-50%) translateY(0); opacity: 1; }
        }

        .toast.success {
            background: linear-gradient(135deg, #1a4d2e, #2d5a3d);
        }

        .toast.error {
            background: linear-gradient(135deg, #c41e3a, #8b1a2e);
        }

        @media (max-width: 480px) {
            .header h1 {
                font-size: 1.1em;
            }

            .stat-number {
                font-size: 1.8em;
            }

            .stat-label {
                font-size: 0.8em;
            }

            .nav-btn {
                font-size: 0.85em;
                padding: 10px 8px;
            }

            .section h2 {
                font-size: 1.2em;
            }

            th, td {
                padding: 8px 6px;
                font-size: 0.8em;
            }

            .patrol-badge {
                font-size: 1em;
                padding: 20px 10px;
            }
        }

        @media (min-width: 768px) {
            .login-container {
                max-width: 500px;
            }

            .main-container {
                max-width: 1400px;
                margin: 0 auto;
                padding: 25px;
            }

            .dashboard {
                grid-template-columns: repeat(4, 1fr);
                gap: 20px;
            }

            .nav-buttons {
                grid-template-columns: repeat(3, 1fr);
            }

            .patrol-badges {
                grid-template-columns: repeat(4, 1fr);
            }

            .logout-btn {
                top: 25px;
                bottom: auto;
                right: 25px;
            }

            .toast {
                bottom: 30px;
            }
        }

        .loading {
            text-align: center;
            padding: 40px;
            color: #666;
        }

        .empty-state {
            text-align: center;
            padding: 40px 20px;
            color: #999;
        }

        .empty-state svg {
            width: 80px;
            height: 80px;
            margin-bottom: 15px;
            opacity: 0.3;
        }
    </style>
</head>
<body>
    <div class="toast" id="toast"></div>

    <div class="header">
        <h1>🦅 The Centre Jamat Khana Phander Boys Scouts Management 🦅</h1>
        <div class="developer">✦ Developed by SKAZIZ ✦</div>
    </div>

    <div class="login-container" id="loginContainer">
        <h2>🔐 Admin Login</h2>
        <div class="form-group">
            <label>Password</label>
            <input type="password" id="passwordInput" placeholder="Enter admin password" autocomplete="current-password">
        </div>
        <button class="btn" onclick="login()">Login</button>
        <p id="loginError" style="color: #c41e3a; text-align: center; margin-top: 15px; display: none; font-weight: 600;">❌ Incorrect password!</p>
    </div>

    <div class="main-container" id="mainContainer">
        <button class="logout-btn" onclick="logout()">🚪 Logout</button>

        <div class="dashboard">
            <div class="stat-card red">
                <div class="stat-number" id="totalScouts">0</div>
                <div class="stat-label">Total Scouts</div>
            </div>
            <div class="stat-card green">
                <div class="stat-number" id="activePatrols">4</div>
                <div class="stat-label">Active Patrols</div>
            </div>
            <div class="stat-card yellow">
                <div class="stat-number" id="campParticipants">0</div>
                <div class="stat-label">Camps</div>
            </div>
            <div class="stat-card blue">
                <div class="stat-number" id="totalLeaders">0</div>
                <div class="stat-label">Leaders</div>
            </div>
        </div>

        <div class="chart-container">
            <h3>📊 Patrol Distribution</h3>
            <div class="bar-chart" id="patrolChart"></div>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('registration')">📝 Register</button>
            <button class="nav-btn" onclick="showSection('scouts')">👥 Boys</button>
            <button class="nav-btn" onclick="showSection('shaheen')">🦅 Shaheen</button>
            <button class="nav-btn" onclick="showSection('guides')">👭 Girls</button>
            <button class="nav-btn" onclick="showSection('camps')">⛺ Camps</button>
            <button class="nav-btn" onclick="showSection('patrols')">🎯 Patrols</button>
            <button class="nav-btn" onclick="showSection('leaders')">👨‍🏫 Leaders</button>
            <button class="nav-btn" onclick="showSection('duties')">📋 Duties</button>
            <button class="nav-btn" onclick="showSection('funding')">💰 Funding</button>
        </div>

        <div class="section active" id="registration">
            <h2>📝 New Scout Registration</h2>
            <form onsubmit="registerScout(event)">
                <div class="form-group">
                    <label>Full Name *</label>
                    <input type="text" name="name" required placeholder="Enter full name" autocomplete="name">
                </div>
                <div class="form-group">
                    <label>Category *</label>
                    <select name="category" required>
                        <option value="">Select Category</option>
                        <option value="Boys Scout">Boys Scout</option>
                        <option value="Shaheen Scout">Shaheen Scout</option>
                        <option value="Girls Guide">Girls Guide</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Age *</label>
                    <input type="number" name="age" required min="6" max="25" placeholder="Enter age">
                </div>
                <div class="form-group">
                    <label>Patrol Group *</label>
                    <select name="patrol" required>
                        <option value="">Select Patrol</option>
                        <option value="Red">🔴 Red Patrol</option>
                        <option value="Green">🟢 Green Patrol</option>
                        <option value="Yellow">🟡 Yellow Patrol</option>
                        <option value="Blue">🔵 Blue Patrol</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Contact Number</label>
                    <input type="tel" name="contact" placeholder="Enter contact number" autocomplete="tel">
                </div>
                <div class="form-group">
                    <label>Address</label>
                    <textarea name="address" rows="3" placeholder="Enter address"></textarea>
                </div>
                <button type="submit" class="btn">✅ Register Scout</button>
            </form>
        </div>

        <div class="section" id="scouts">
            <h2>👥 Boys Scouts List</h2>
            <div class="search-container">
                <input type="text" class="search-input" placeholder="🔍 Search scouts..." onkeyup="searchTable('scoutsTable', this.value)">
            </div>
            <div class="export-buttons">
                <button class="export-btn" onclick="exportToCSV('scouts')">📥 Export CSV</button>
                <button class="export-btn" onclick="printTable('scouts')">🖨️ Print</button>
            </div>
            <div class="table-container">
                <table id="scoutsTable">
                    <thead>
                        <tr>
                            <th>Name</th>
                            <th>Age</th>
                            <th>Patrol</th>
                            <th>Contact</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>
        </div>

        <div class="section" id="shaheen">
            <h2>🦅 Shaheen Scouts List</h2>
            <div class="search-container">
                <input type="text" class="search-input" placeholder="🔍 Search shaheen scouts..." onkeyup="searchTable('shaheenTable', this.value)">
            </div>
            <div class="export-buttons">
                <button class="export-btn" onclick="exportToCSV('shaheen')">📥 Export CSV</button>
                <button class="export-btn" onclick="printTable('shaheen')">🖨️ Print</button>
            </div>
            <div class="table-container">
                <table id="shaheenTable">
                    <thead>
                        <tr>
                            <th>Name</th>
                            <th>Age</th>
                            <th>Patrol</th>
                            <th>Contact</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>
        </div>

        <div class="section" id="guides">
            <h2>👭 Girls Guide List</h2>
            <div class="search-container">
                <input type="text" class="search-input" placeholder="🔍 Search girls guide..." onkeyup="searchTable('guidesTable', this.value)">
            </div>
            <div class="export-buttons">
                <button class="export-btn" onclick="exportToCSV('guides')">📥 Export CSV</button>
                <button class="export-btn" onclick="printTable('guides')">🖨️ Print</button>
            </div>
            <div class="table-container">
                <table id="guidesTable">
                    <thead>
                        <tr>
                            <th>Name</th>
                            <th>Age</th>
                            <th>Patrol</th>
                            <th>Contact</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>
        </div>

        <div class="section" id="camps">
            <h2>⛺ Camp Participants</h2>
            <form onsubmit="addCampParticipant(event)">
                <div class="form-group">
                    <label>Scout Name *</label>
                    <input type="text" name="campName" required placeholder="Enter scout name">
                </div>
                <div class="form-group">
                    <label>Camp Name *</label>
                    <input type="text" name="campTitle" required placeholder="Enter camp name">
                </div>
                <div class="form-group">
                    <label>Camp Date *</label>
                    <input type="date" name="campDate" required>
                </div>
                <button type="submit" class="btn">➕ Add Participant</button>
            </form>
            <div class="export-buttons">
                <button class="export-btn" onclick="exportToCSV('camps')">📥 Export CSV</button>
            </div>
            <div class="table-container">
                <table id="campsTable">
                    <thead>
                        <tr>
                            <th>Scout Name</th>
                            <th>Camp Name</th>
                            <th>Date</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>
        </div>

        <div class="section" id="patrols">
            <h2>🎯 Active Patrol Groups</h2>
            <div class="patrol-badges">
                <div class="patrol-badge patrol-red">
                    <div style="font-size: 1.8em; margin-bottom: 10px;">🔴</div>
                    <div>RED</div>
                    <div id="redCount" style="font-size: 2.2em; margin-top: 10px; font-weight: 900;">0</div>
                </div>
                <div class="patrol-badge patrol-green">
                    <div style="font-size: 1.8em; margin-bottom: 10px;">🟢</div>
                    <div>GREEN</div>
                    <div id="greenCount" style="font-size: 2.2em; margin-top: 10px; font-weight: 900;">0</div>
                </div>
                <div class="patrol-badge patrol-yellow">
                    <div style="font-size: 1.8em; margin-bottom: 10px;">🟡</div>
                    <div>YELLOW</div>
                    <div id="yellowCount" style="font-size: 2.2em; margin-top: 10px; font-weight: 900;">0</div>
                </div>
                <div class="patrol-badge patrol-blue">
                    <div style="font-size: 1.8em; margin-bottom: 10px;">🔵</div>
                    <div>BLUE</div>
                    <div id="blueCount" style="font-size: 2.2em; margin-top: 10px; font-weight: 900;">0</div>
                </div>
            </div>
        </div>

        <div class="section" id="leaders">
            <h2>👨‍🏫 Scout Leaders</h2>
            <form onsubmit="addLeader(event)">
                <div class="form-group">
                    <label>Leader Name *</label>
                    <input type="text" name="leaderName" required placeholder="Enter leader name">
                </div>
                <div class="form-group">
                    <label>Position *</label>
                    <input type="text" name="position" required placeholder="Enter position/role">
                </div>
                <div class="form-group">
                    <label>Contact</label>
                    <input type="tel" name="leaderContact" placeholder="Enter contact number" autocomplete="tel">
                </div>
                <button type="submit" class="btn">➕ Add Leader</button>
            </form>
            <div class="export-buttons">
                <button class="export-btn" onclick="exportToCSV('leaders')">📥 Export CSV</button>
            </div>
            <div class="table-container">
                <table id="leadersTable">
                    <thead>
                        <tr>
                            <th>Name</th>
                            <th>Position</th>
                            <th>Contact</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>
        </div>

        <div class="section" id="duties">
            <h2>📋 Duties Assignment</h2>
            <form onsubmit="addDuty(event)">
                <div class="form-group">
                    <label>Duty Title *</label>
                    <input type="text" name="dutyTitle" required placeholder="Enter duty title">
                </div>
                <div class="form-group">
                    <label>Assigned To *</label>
                    <input type="text" name="assignedTo" required placeholder="Enter person name">
                </div>
                <div class="form-group">
                    <label>Date *</label>
                    <input type="date" name="dutyDate" required>
                </div>
                <div class="form-group">
                    <label>Description</label>
                    <textarea name="dutyDesc" rows="3" placeholder="Enter duty description"></textarea>
                </div>
                <button type="submit" class="btn">➕ Add Duty</button>
            </form>
            <div class="export-buttons">
                <button class="export-btn" onclick="exportToCSV('duties')">📥 Export CSV</button>
            </div>
            <div class="table-container">
                <table id="dutiesTable">
                    <thead>
                        <tr>
                            <th>Duty</th>
                            <th>Assigned To</th>
                            <th>Date</th>
                            <th>Description</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>
        </div>

        <div class="section" id="funding">
            <h2>💰 Funding Management</h2>
            <form onsubmit="addFunding(event)">
                <div class="form-group">
                    <label>Source *</label>
                    <input type="text" name="fundSource" required placeholder="Enter funding source">
                </div>
                <div class="form-group">
                    <label>Amount (Rs.) *</label>
                    <input type="number" name="fundAmount" required min="0" placeholder="Enter amount">
                </div>
                <div class="form-group">
                    <label>Date *</label>
                    <input type="date" name="fundDate" required>
                </div>
                <div class="form-group">
                    <label>Purpose</label>
                    <textarea name="fundPurpose" rows="3" placeholder="Enter purpose of funding"></textarea>
                </div>
                <button type="submit" class="btn">➕ Add Funding Record</button>
            </form>
            <div class="export-buttons">
                <button class="export-btn" onclick="exportToCSV('funding')">📥 Export CSV</button>
            </div>
            <div class="table-container">
                <table id="fundingTable">
                    <thead>
                        <tr>
                            <th>Source</th>
                            <th>Amount (Rs.)</th>
                            <th>Date</th>
                            <th>Purpose</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody></tbody>
                </table>
            </div>
        </div>
    </div>

    <script>
        const PASSWORD = 'admin123';
        let data = {
            scouts: [],
            shaheen: [],
            guides: [],
            camps: [],
            leaders: [],
            duties: [],
            funding: []
        };

        function showToast(message, type = 'success') {
            const toast = document.getElementById('toast');
            toast.textContent = message;
            toast.className = `toast ${type} show`;
            setTimeout(() => toast.classList.remove('show'), 3000);
        }

        function loadData() {
            try {
                const stored = localStorage.getItem('scoutsData');
                if (stored) data = JSON.parse(stored);
                updateDisplay();
            } catch (e) {
                showToast('Error loading data!', 'error');
            }
        }

        function saveData() {
            try {
                localStorage.setItem('scoutsData', JSON.stringify(data));
            } catch (e) {
                showToast('Error saving data!', 'error');
            }
        }

        function login() {
            const password = document.getElementById('passwordInput').value;
            if (password === PASSWORD) {
                document.getElementById('loginContainer').style.display = 'none';
                document.getElementById('mainContainer').style.display = 'block';
                loadData();
                showToast('✅ Login successful!', 'success');
            } else {
                document.getElementById('loginError').style.display = 'block';
                showToast('❌ Incorrect password!', 'error');
            }
        }

        function logout() {
            if (confirm('Are you sure you want to logout?')) {
                document.getElementById('loginContainer').style.display = 'block';
                document.getElementById('mainContainer').style.display = 'none';
                document.getElementById('passwordInput').value = '';
                document.getElementById('loginError').style.display = 'none';
                showToast('👋 Logged out!', 'success');
            }
        }

        function showSection(sectionId) {
            document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
            document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
            document.getElementById(sectionId).classList.add('active');
            event.target.classList.add('active');
        }

        function registerScout(e) {
            e.preventDefault();
            const form = e.target;
            const scout = {
                id: Date.now(),
                name: form.name.value,
                category: form.category.value,
                age: form.age.value,
                patrol: form.patrol.value,
                contact: form.contact.value,
                address: form.address.value,
                registeredDate: new Date().toISOString().split('T')[0]
            };

            if (scout.category === 'Boys Scout') data.scouts.push(scout);
            else if (scout.category === 'Shaheen Scout') data.shaheen.push(scout);
            else if (scout.category === 'Girls Guide') data.guides.push(scout);

            saveData();
            updateDisplay();
            form.reset();
            showToast('✅ Scout registered!', 'success');
        }

        function addCampParticipant(e) {
            e.preventDefault();
            const form = e.target;
            data.camps.push({
                id: Date.now(),
                name: form.campName.value,
                camp: form.campTitle.value,
                date: form.campDate.value
            });
            saveData();
            updateDisplay();
            form.reset();
            showToast('✅ Camp participant added!', 'success');
        }

        function addLeader(e) {
            e.preventDefault();
            const form = e.target;
            data.leaders.push({
                id: Date.now(),
                name: form.leaderName.value,
                position: form.position.value,
                contact: form.leaderContact.value
            });
            saveData();
            updateDisplay();
            form.reset();
            showToast('✅ Leader added!', 'success');
        }

        function addDuty(e) {
            e.preventDefault();
            const form = e.target;
            data.duties.push({
                id: Date.now(),
                title: form.dutyTitle.value,
                assignedTo: form.assignedTo.value,
                date: form.dutyDate.value,
                description: form.dutyDesc.value
            });
            saveData();
            updateDisplay();
            form.reset();
            showToast('✅ Duty assigned!', 'success');
        }

        function addFunding(e) {
            e.preventDefault();
            const form = e.target;
            data.funding.push({
                id: Date.now(),
                source: form.fundSource.value,
                amount: form.fundAmount.value,
                date: form.fundDate.value,
                purpose: form.fundPurpose.value
            });
            saveData();
            updateDisplay();
            form.reset();
            showToast('✅ Funding added!', 'success');
        }

        function deleteItem(category, id) {
            if (confirm('⚠️ Delete this item?')) {
                data[category] = data[category].filter(item => item.id !== id);
                saveData();
                updateDisplay();
                showToast('🗑️ Deleted!', 'success');
            }
        }

        function updateDisplay() {
            const totalScouts = data.scouts.length + data.shaheen.length + data.guides.length;
            document.getElementById('totalScouts').textContent = totalScouts;
            document.getElementById('campParticipants').textContent = data.camps.length;
            document.getElementById('totalLeaders').textContent = data.leaders.length;

            const patrols = { Red: 0, Green: 0, Yellow: 0, Blue: 0 };
            [...data.scouts, ...data.shaheen, ...data.guides].forEach(scout => {
                if (patrols.hasOwnProperty(scout.patrol)) patrols[scout.patrol]++;
            });

            document.getElementById('redCount').textContent = patrols.Red;
            document.getElementById('greenCount').textContent = patrols.Green;
            document.getElementById('yellowCount').textContent = patrols.Yellow;
            document.getElementById('blueCount').textContent = patrols.Blue;

            updateChart(patrols);
            updateTable('scoutsTable', data.scouts, 'scouts');
            updateTable('shaheenTable', data.shaheen, 'shaheen');
            updateTable('guidesTable', data.guides, 'guides');
            updateCampsTable();
            updateLeadersTable();
            updateDutiesTable();
            updateFundingTable();
        }

        function updateChart(patrols) {
            const chart = document.getElementById('patrolChart');
            const maxValue = Math.max(...Object.values(patrols), 1);
            const colors = { Red: '#c41e3a', Green: '#1a4d2e', Yellow: '#ffd700', Blue: '#1e3a8a' };
            
            chart.innerHTML = '';
            Object.entries(patrols).forEach(([name, count]) => {
                const bar = document.createElement('div');
                bar.className = 'bar';
                bar.style.height = (count / maxValue) * 100 + '%';
                bar.style.background = `linear-gradient(to top, ${colors[name]}, ${colors[name]}dd)`;
                bar.innerHTML = `<div class="bar-label">${name}</div><div class="bar-value">${count}</div>`;
                chart.appendChild(bar);
            });
        }

        function updateTable(tableId, items, category) {
            const tbody = document.getElementById(tableId).querySelector('tbody');
            tbody.innerHTML = items.length ? items.map(item => `
                <tr>
                    <td><strong>${item.name}</strong></td>
                    <td>${item.age}</td>
                    <td>${item.patrol}</td>
                    <td>${item.contact || '-'}</td>
                    <td><button class="delete-btn" onclick="deleteItem('${category}', ${item.id})">🗑️</button></td>
                </tr>
            `).join('') : '<tr><td colspan="5" style="text-align:center;color:#999;padding:20px">📭 No records</td></tr>';
        }

        function updateCampsTable() {
            const tbody = document.getElementById('campsTable').querySelector('tbody');
            tbody.innerHTML = data.camps.length ? data.camps.map(item => `
                <tr>
                    <td><strong>${item.name}</strong></td>
                    <td>${item.camp}</td>
                    <td>${item.date}</td>
                    <td><button class="delete-btn" onclick="deleteItem('camps', ${item.id})">🗑️</button></td>
                </tr>
            `).join('') : '<tr><td colspan="4" style="text-align:center;color:#999;padding:20px">📭 No participants</td></tr>';
        }

        function updateLeadersTable() {
            const tbody = document.getElementById('leadersTable').querySelector('tbody');
            tbody.innerHTML = data.leaders.length ? data.leaders.map(item => `
                <tr>
                    <td><strong>${item.name}</strong></td>
                    <td>${item.position}</td>
                    <td>${item.contact || '-'}</td>
                    <td><button class="delete-btn" onclick="deleteItem('leaders', ${item.id})">🗑️</button></td>
                </tr>
            `).join('') : '<tr><td colspan="4" style="text-align:center;color:#999;padding:20px">📭 No leaders</td></tr>';
        }

        function updateDutiesTable() {
            const tbody = document.getElementById('dutiesTable').querySelector('tbody');
            tbody.innerHTML = data.duties.length ? data.duties.map(item => `
                <tr>
                    <td><strong>${item.title}</strong></td>
                    <td>${item.assignedTo}</td>
                    <td>${item.date}</td>
                    <td>${item.description || '-'}</td>
                    <td><button class="delete-btn" onclick="deleteItem('duties', ${item.id})">🗑️</button></td>
                </tr>
            `).join('') : '<tr><td colspan="5" style="text-align:center;color:#999;padding:20px">📭 No duties</td></tr>';
        }

        function updateFundingTable() {
            const tbody = document.getElementById('fundingTable').querySelector('tbody');
            let html = '';
            let totalAmount = 0;
            
            data.funding.forEach(item => {
                totalAmount += parseInt(item.amount);
                html += `<tr>
                    <td><strong>${item.source}</strong></td>
                    <td style="color:#1a4d2e;font-weight:bold">Rs. ${parseInt(item.amount).toLocaleString()}</td>
                    <td>${item.date}</td>
                    <td>${item.purpose || '-'}</td>
                    <td><button class="delete-btn" onclick="deleteItem('funding', ${item.id})">🗑️</button></td>
                </tr>`;
            });
            
            if (data.funding.length) {
                html += `<tr style="background:rgba(26,77,46,0.1);font-weight:bold">
                    <td><strong>💰 TOTAL</strong></td>
                    <td colspan="4" style="color:#1a4d2e;font-size:1.1em"><strong>Rs. ${totalAmount.toLocaleString()}</strong></td>
                </tr>`;
            } else {
                html = '<tr><td colspan="5" style="text-align:center;color:#999;padding:20px">📭 No funding records</td></tr>';
            }
            tbody.innerHTML = html;
        }

        function searchTable(tableId, query) {
            const rows = document.getElementById(tableId).getElementsByTagName('tbody')[0].getElementsByTagName('tr');
            for (let row of rows) {
                const text = (row.textContent || row.innerText).toLowerCase();
                row.style.display = text.includes(query.toLowerCase()) ? '' : 'none';
            }
        }

        function exportToCSV(category) {
            let csvContent = '', filename = '';
            
            switch(category) {
                case 'scouts':
                    csvContent = 'Name,Age,Patrol,Contact\n' + data.scouts.map(i => 
                        `"${i.name}",${i.age},"${i.patrol}","${i.contact||''}"`).join('\n');
                    filename = 'boys_scouts.csv';
                    break;
                case 'shaheen':
                    csvContent = 'Name,Age,Patrol,Contact\n' + data.shaheen.map(i => 
                        `"${i.name}",${i.age},"${i.patrol}","${i.contact||''}"`).join('\n');
                    filename = 'shaheen_scouts.csv';
                    break;
                case 'guides':
                    csvContent = 'Name,Age,Patrol,Contact\n' + data.guides.map(i => 
                        `"${i.name}",${i.age},"${i.patrol}","${i.contact||''}"`).join('\n');
                    filename = 'girls_guide.csv';
                    break;
                case 'camps':
                    csvContent = 'Scout Name,Camp Name,Date\n' + data.camps.map(i => 
                        `"${i.name}","${i.camp}","${i.date}"`).join('\n');
                    filename = 'camp_participants.csv';
                    break;
                case 'leaders':
                    csvContent = 'Name,Position,Contact\n' + data.leaders.map(i => 
                        `"${i.name}","${i.position}","${i.contact||''}"`).join('\n');
                    filename = 'leaders.csv';
                    break;
                case 'duties':
                    csvContent = 'Duty,Assigned To,Date,Description\n' + data.duties.map(i => 
                        `"${i.title}","${i.assignedTo}","${i.date}","${i.description||''}"`).join('\n');
                    filename = 'duties.csv';
                    break;
                case 'funding':
                    csvContent = 'Source,Amount,Date,Purpose\n' + data.funding.map(i => 
                        `"${i.source}","${i.amount}","${i.date}","${i.purpose||''}"`).join('\n');
                    filename = 'funding.csv';
                    break;
            }
            
            const blob = new Blob([csvContent], { type: 'text/csv' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = filename;
            a.click();
            showToast('📥 CSV exported!', 'success');
        }

        function printTable(category) {
            const tableId = category + 'Table';
            const win = window.open('', '', 'height=600,width=800');
            win.document.write(`<html><head><title>Print</title>
                <style>body{font-family:Arial}table{width:100%;border-collapse:collapse}th,td{border:1px solid #ddd;padding:8px;text-align:left}th{background:#1a4d2e;color:white}</style>
                </head><body><h2>The Centre Jamat Khana Phander Boys Scouts</h2>
                ${document.getElementById(tableId).outerHTML}</body></html>`);
            win.document.close();
            win.print();
        }

        document.getElementById('passwordInput').addEventListener('keypress', e => {
            if (e.key === 'Enter') login();
        });

        loadData();
    </script>
</body>
</html>
