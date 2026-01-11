# futsal-gestao
Sistema de gestão de mensalidades de futsal

<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gestão Futsal - Controle de Mensalidades</title>
    <style>
        :root {
            --primary: #1565c0;
            --primary-dark: #0d47a1;
            --secondary: #43a047;
            --danger: #e53935;
            --warning: #f57c00;
            --bg: #f0f2f5;
            --card-bg: #ffffff;
            --text: #212121;
            --text-secondary: #757575;
            --border: #e0e0e0;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
            background-color: var(--bg);
            color: var(--text);
            line-height: 1.6;
            padding-bottom: 40px;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            padding: 20px;
        }

        /* Header */
        header {
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            color: white;
            padding: 25px 20px;
            border-radius: 0 0 20px 20px;
            margin-bottom: 25px;
            box-shadow: 0 4px 15px rgba(21, 101, 192, 0.3);
        }

        header h1 {
            font-size: 1.8rem;
            margin-bottom: 5px;
        }

        header p {
            opacity: 0.9;
            font-size: 0.95rem;
        }

        /* Month Selector */
        .month-selector {
            background: var(--card-bg);
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
            margin-bottom: 20px;
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            align-items: center;
            justify-content: space-between;
        }

        .month-controls {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .month-controls button {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            border: none;
            background: var(--primary);
            color: white;
            font-size: 1.2rem;
            cursor: pointer;
            transition: all 0.2s;
        }

        .month-controls button:hover {
            background: var(--primary-dark);
            transform: scale(1.1);
        }

        .current-month {
            font-size: 1.3rem;
            font-weight: 600;
            color: var(--primary);
            min-width: 200px;
            text-align: center;
        }

        .btn-new-month {
            background: var(--warning);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.2s;
        }

        .btn-new-month:hover {
            background: #e65100;
        }

        /* Dashboard Cards */
        .dashboard {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
            gap: 15px;
            margin-bottom: 25px;
        }

        .card {
            background: var(--card-bg);
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
            text-align: center;
            transition: transform 0.2s;
        }

        .card:hover {
            transform: translateY(-3px);
        }

        .card h3 {
            font-size: 0.85rem;
            color: var(--text-secondary);
            margin-bottom: 8px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .card .value {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary);
        }

        .card .value.positive { color: var(--secondary); }
        .card .value.negative { color: var(--danger); }
        .card .value.neutral { color: var(--warning); }

        /* Section Titles */
        .section-title {
            font-size: 1.1rem;
            color: var(--text);
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--primary);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        /* Forms */
        .input-group {
            background: var(--card-bg);
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
        }

        .input-group input {
            flex: 1;
            padding: 12px 15px;
            border: 2px solid var(--border);
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.2s;
        }

        .input-group input:focus {
            outline: none;
            border-color: var(--primary);
        }

        .btn-add {
            background: var(--secondary);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            font-size: 1rem;
            transition: all 0.2s;
        }

        .btn-add:hover {
            background: #2e7d32;
        }

        /* Player List */
        .player-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin-bottom: 25px;
        }

        .player-card {
            background: var(--card-bg);
            padding: 15px 20px;
            border-radius: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
            border-left: 4px solid var(--danger);
            transition: all 0.2s;
        }

        .player-card:hover {
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }

        .player-card.paid {
            border-left-color: var(--secondary);
            background: linear-gradient(90deg, #e8f5e9 0%, var(--card-bg) 100%);
        }

        .player-info {
            flex: 1;
        }

        .player-info strong {
            display: block;
            font-size: 1.1rem;
            margin-bottom: 4px;
        }

        .player-info .status {
            font-size: 0.85rem;
            color: var(--text-secondary);
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .player-info .status .dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: var(--danger);
        }

        .player-card.paid .player-info .status .dot {
            background: var(--secondary);
        }

        .actions {
            display: flex;
            gap: 8px;
        }

        .btn {
            padding: 8px 15px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.85rem;
            font-weight: 500;
            transition: all 0.2s;
        }

        .btn-pay {
            background: var(--secondary);
            color: white;
        }

        .btn-pay:hover {
            background: #2e7d32;
        }

        .btn-unpay {
            background: var(--warning);
            color: white;
        }

        .btn-unpay:hover {
            background: #e65100;
        }

        .btn-delete {
            background: #ffebee;
            color: var(--danger);
        }

        .btn-delete:hover {
            background: var(--danger);
            color: white;
        }

        /* History Section */
        .history-section {
            background: var(--card-bg);
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
            margin-top: 25px;
        }

        .history-list {
            max-height: 400px;
            overflow-y: auto;
        }

        .history-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px;
            border-bottom: 1px solid var(--border);
            cursor: pointer;
            transition: background 0.2s;
        }

        .history-item:hover {
            background: #f5f5f5;
        }

        .history-item:last-child {
            border-bottom: none;
        }

        .history-month {
            font-weight: 600;
        }

        .history-details {
            text-align: right;
            font-size: 0.9rem;
            color: var(--text-secondary);
        }

        .history-profit {
            font-weight: 600;
            color: var(--secondary);
        }

        .history-loss {
            font-weight: 600;
            color: var(--danger);
        }

        /* Modal */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            justify-content: center;
            align-items: center;
            z-index: 1000;
            padding: 20px;
        }

        .modal {
            background: var(--card-bg);
            padding: 25px;
            border-radius: 15px;
            width: 100%;
            max-width: 500px;
            max-height: 80vh;
            overflow-y: auto;
            animation: modalSlide 0.3s ease;
        }

        @keyframes modalSlide {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--border);
        }

        .modal-header h2 {
            color: var(--primary);
            font-size: 1.3rem;
        }

        .close-modal {
            background: none;
            border: none;
            font-size: 1.8rem;
            cursor: pointer;
            color: var(--text-secondary);
            transition: color 0.2s;
        }

        .close-modal:hover {
            color: var(--danger);
        }

        .log-item {
            padding: 12px 0;
            border-bottom: 1px solid var(--border);
        }

        .log-item:last-child {
            border-bottom: none;
        }

        .log-date {
            font-size: 0.8rem;
            color: var(--text-secondary);
            margin-bottom: 4px;
        }

        .log-message {
            font-size: 0.95rem;
        }

        /* Empty State */
        .empty-state {
            text-align: center;
            padding: 40px 20px;
            color: var(--text-secondary);
        }

        .empty-state svg {
            width: 80px;
            height: 80px;
            margin-bottom: 15px;
            opacity: 0.5;
        }

        /* Responsive */
        @media (max-width: 600px) {
            .month-selector {
                flex-direction: column;
                gap: 15px;
            }

            .player-card {
                flex-direction: column;
                gap: 12px;
                text-align: center;
            }

            .actions {
                width: 100%;
                justify-content: center;
            }

            .input-group {
                flex-direction: column;
            }

            .btn-add {
                width: 100%;
            }
        }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>⚽ Gestão Futsal</h1>
        <p>Controle de Mensalidades e Aluguel</p>
    </header>

    <!-- Month Selector -->
    <div class="month-selector">
        <div class="month-controls">
            <button onclick="changeMonth(-1)">◀</button>
            <span class="current-month" id="currentMonth">Janeiro 2025</span>
            <button onclick="changeMonth(1)">▶</button>
        </div>
        <button class="btn-new-month" onclick="createNewMonth()">+ Novo Mês</button>
    </div>

    <!-- Dashboard -->
    <div class="dashboard">
        <div class="card">
            <h3>Jogadores</h3>
            <div class="value" id="totalPlayers">0</div>
        </div>
        <div class="card">
            <h3>Pagos</h3>
            <div class="value positive" id="paidPlayers">0</div>
        </div>
        <div class="card">
            <h3>Arrecadação</h3>
            <div class="value" id="totalCollected">R$ 0</div>
        </div>
        <div class="card">
            <h3>Aluguel</h3>
            <div class="value negative">-R$ 220</div>
        </div>
        <div class="card">
            <h3>Líquido</h3>
            <div class="value" id="netProfit">R$ 0</div>
        </div>
    </div>

    <!-- Add Player -->
    <div class="section-title">Jogadores do Mês</div>
    <div class="input-group">
        <input type="text" id="playerName" placeholder="Nome do jogador" onkeypress="handleKeyPress(event)">
        <button class="btn-add" onclick="addPlayer()">+ Adicionar</button>
    </div>

    <!-- Player List -->
    <div class="player-list" id="playerList">
        <div class="empty-state">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"></path>
                <circle cx="9" cy="7" r="4"></circle>
                <path d="M23 21v-2a4 4 0 0 0-3-3.87"></path>
                <path d="M16 3.13a4 4 0 0 1 0 7.75"></path>
            </svg>
            <p>Nenhum jogador cadastrado neste mês</p>
        </div>
    </div>

    <!-- History Section -->
    <div class="history-section">
        <div class="section-title">
            📅 Histórico de Meses
            <button class="btn" style="background: var(--primary); color: white;" onclick="openLogsModal()">Ver Logs</button>
        </div>
        <div class="history-list" id="historyList">
            <div class="empty-state">
                <p>Nenhum histórico encontrado</p>
            </div>
        </div>
    </div>
</div>

<!-- Modal Extrato -->
<div class="modal-overlay" id="logsModal">
    <div class="modal">
        <div class="modal-header">
            <h2>📊 Extrato de Movimentações</h2>
            <button class="close-modal" onclick="closeLogsModal()">×</button>
        </div>
        <div id="logsContent"></div>
    </div>
</div>

<script>
    // ==================== CONFIGURAÇÕES ====================
    const MONTHLY_FEE = 30;
    const GYM_RENT = 220;

    // ==================== ESTADO DA APLICAÇÃO ====================
    let currentDate = new Date();
    let allData = JSON.parse(localStorage.getItem('futsalData')) || {};
    let currentMonthKey = getMonthKey(currentDate);

    // ==================== INICIALIZAÇÃO ====================
    document.addEventListener('DOMContentLoaded', function() {
        initializeMonth();
        render();
    });

    // ==================== FUNÇÕES DE DATA ====================
    function getMonthKey(date) {
        const year = date.getFullYear();
        const month = date.getMonth() + 1;
        return `${year}-${month.toString().padStart(2, '0')}`;
    }

    function getMonthName(monthNumber) {
        const months = [
            'Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho',
            'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'
        ];
        return months[monthNumber - 1];
    }

    function formatDate(dateString) {
        const options = { day: '2-digit', month: '2-digit', year: 'numeric', hour: '2-digit', minute: '2-digit' };
        return new Date(dateString).toLocaleDateString('pt-BR', options);
    }

    // ==================== NAVEGAÇÃO DE MESES ====================
    function changeMonth(direction) {
        currentDate.setMonth(currentDate.getMonth() + direction);
        currentMonthKey = getMonthKey(currentDate);
        initializeMonth();
        render();
    }

    function initializeMonth() {
        if (!allData[currentMonthKey]) {
            allData[currentMonthKey] = {
                players: [],
                logs: [],
                archived: false
            };
            saveData();
        }
        updateMonthDisplay();
    }

    function updateMonthDisplay() {
        const monthName = getMonthName(currentDate.getMonth() + 1);
        const year = currentDate.getFullYear();
        document.getElementById('currentMonth').textContent = `${monthName} ${year}`;
    }

    function createNewMonth() {
        const nextMonth = new Date(currentDate);
        nextMonth.setMonth(nextMonth.getMonth() + 1);
        
        if (confirm(`Criar dados para ${getMonthName(nextMonth.getMonth() + 1)} de ${nextMonth.getFullYear()}?`)) {
            currentDate = nextMonth;
            currentMonthKey = getMonthKey(currentDate);
            initializeMonth();
            render();
        }
    }

    // ==================== GERENCIAMENTO DE JOGADORES ====================
    function addPlayer() {
        const nameInput = document.getElementById('playerName');
        const name = nameInput.value.trim();
        
        if (name) {
            const newPlayer = {
                id: Date.now(),
                name: name,
                paid: false,
                lastPaymentDate: null
            };
            
            allData[currentMonthKey].players.push(newPlayer);
            addLog(`Jogador adicionado: ${name}`);
            
            nameInput.value = '';
            saveData();
            render();
        } else {
            highlightInput();
        }
    }

    function handleKeyPress(event) {
        if (event.key === 'Enter') {
            addPlayer();
        }
    }

    function togglePayment(playerId) {
        const player = allData[currentMonthKey].players.find(p => p.id === playerId);
        
        if (player) {
            player.paid = !player.paid;
            player.lastPaymentDate = player.paid ? new Date().toISOString() : null;
            
            if (player.paid) {
                addLog(`Pagamento recebido: ${player.name} (R$ ${MONTHLY_FEE})`);
            } else {
                addLog(`Pagamento estornado: ${player.name}`);
            }
            
            saveData();
            render();
        }
    }

    function deletePlayer(playerId) {
        const player = allData[currentMonthKey].players.find(p => p.id === playerId);
        
        if (player && confirm(`Remover ${player.name} da lista?`)) {
            addLog(`Jogador removido: ${player.name}`);
            allData[currentMonthKey].players = allData[currentMonthKey].players.filter(p => p.id !== playerId);
            saveData();
            render();
        }
    }

    // ==================== SISTEMA DE LOGS ====================
    function addLog(message) {
        const log = {
            date: new Date().toISOString(),
            message: message
        };
        allData[currentMonthKey].logs.unshift(log);
        saveData();
    }

    // ==================== RENDERIZAÇÃO ====================
    function render() {
        renderDashboard();
        renderPlayerList();
        renderHistory();
    }

    function renderDashboard() {
        const monthData = allData[currentMonthKey];
        const players = monthData.players;
        
        const totalPlayers = players.length;
        const paidPlayers = players.filter(p => p.paid).length;
        const totalCollected = paidPlayers * MONTHLY_FEE;
        const netProfit = totalCollected - G
