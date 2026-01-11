# futsal-gestao
Sistema de gestão de mensalidades de futsal
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>⚽ Gestão Futsal - Controle de Mensalidades</title>
    <style>
        /* Reset e Variáveis */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #1565c0;
            --primary-dark: #0d47a1;
            --success: #2e7d32;
            --success-light: #4caf50;
            --danger: #c62828;
            --danger-light: #e53935;
            --warning: #ef6c00;
            --bg: #f5f7fa;
            --card: #ffffff;
            --text: #212121;
            --text-light: #757575;
            --border: #e0e0e0;
            --shadow: 0 2px 4px rgba(0,0,0,0.1); /* Simplificado: sombra mais sutil */
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
            background-color: var(--bg);
            color: var(--text);
            min-height: 100vh;
            padding-bottom: 20px; /* Reduzido para economizar espaço */
        }

        /* Container Principal */
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 0 15px;
        }

        /* Header - Simplificado: fundo sólido, sem gradiente */
        header {
            background: var(--primary); /* Fundo sólido para limpeza */
            color: white;
            padding: 20px 15px; /* Reduzido */
            margin-bottom: 15px; /* Reduzido */
            border-radius: 0 0 15px 15px; /* Menos arredondado */
            box-shadow: var(--shadow);
        }

        header h1 {
            font-size: 1.4rem; /* Menor para simplicidade */
            margin-bottom: 5px;
        }

        header p {
            opacity: 0.9;
            font-size: 0.85rem;
        }

        /* Seleção de Mês - Mantido, mas ajustado para mobile */
        .month-selector {
            background: var(--card);
            padding: 15px; /* Reduzido */
            border-radius: 10px;
            box-shadow: var(--shadow);
            margin-bottom: 15px;
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            align-items: center;
            justify-content: space-between;
        }

        .month-nav {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .month-nav button {
            width: 35px; /* Menor */
            height: 35px;
            border-radius: 50%;
            border: none;
            background: var(--primary);
            color: white;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .month-nav button:hover {
            background: var(--primary-dark);
            transform: scale(1.05); /* Menos exagerado */
        }

        .month-nav button:disabled {
            background: #ccc;
            cursor: not-allowed;
            transform: none;
        }

        .current-month {
            font-size: 1.1rem;
            font-weight: 600;
            color: var(--primary);
            min-width: 150px; /* Menor */
            text-align: center;
        }

        .month-actions {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }

        .btn-month {
            background: var(--warning);
            color: white;
            border: none;
            padding: 8px 15px; /* Menor */
            border-radius: 6px;
            cursor: pointer;
            font-weight: 500;
            font-size: 0.85rem;
            transition: all 0.2s;
        }

        .btn-month:hover {
            background: #e65100;
        }

        .btn-copy {
            background: var(--primary);
        }

        .btn-copy:hover {
            background: var(--primary-dark);
        }

        /* Dashboard - Simplificado: apenas 3 cards essenciais */
        .dashboard {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin-bottom: 15px;
        }

        .dashboard .card {
            background: var(--card);
            padding: 15px 12px; /* Menor */
            border-radius: 8px;
            box-shadow: var(--shadow);
            text-align: center;
        }

        .dashboard .card h3 {
            font-size: 0.7rem; /* Menor */
            color: var(--text-light);
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 6px;
        }

        .dashboard .card .value {
            font-size: 1.2rem; /* Menor */
            font-weight: 700;
            color: var(--primary);
        }

        .dashboard .card .value.success { color: var(--success); }
        .dashboard .card .value.danger { color: var(--danger); }
        .dashboard .card .value.warning { color: var(--warning); }

        /* Título de Seção */
        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
            padding-bottom: 8px;
            border-bottom: 2px solid var(--primary);
        }

        .section-header h2 {
            font-size: 1rem; /* Menor */
            color: var(--text);
        }

        /* Formulário de Adição - Simplificado */
        .add-form {
            background: var(--card);
            padding: 15px;
            border-radius: 10px;
            box-shadow: var(--shadow);
            margin-bottom: 15px;
        }

        .add-form .input-row {
            display: flex;
            gap: 8px;
        }

        .add-form input {
            flex: 1;
            padding: 10px 12px; /* Menor */
            border: 1px solid var(--border); /* Menos espesso */
            border-radius: 6px;
            font-size: 0.95rem;
            transition: border-color 0.2s;
        }

        .add-form input:focus {
            outline: none;
            border-color: var(--primary);
        }

        .add-form input.error {
            border-color: var(--danger);
            animation: shake 0.5s;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }

        .btn-add {
            background: var(--success);
            color: white;
            border: none;
            padding: 10px 20px; /* Menor */
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.95rem;
            transition: all 0.2s;
            white-space: nowrap;
        }

        .btn-add:hover {
            background: var(--success-light);
        }

        /* Lista de Jogadores - Simplificada */
        .player-list {
            display: flex;
            flex-direction: column;
            gap: 8px;
            margin-bottom: 20px;
        }

        .player-card {
            background: var(--card);
            padding: 12px 15px; /* Menor */
            border-radius: 8px;
            box-shadow: var(--shadow);
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-left: 3px solid var(--danger-light); /* Menos espesso */
            transition: all 0.2s;
        }

        .player-card:hover {
            box-shadow: 0 3px 10px rgba(0,0,0,0.1); /* Menos intenso */
        }

        .player-card.paid {
            border-left-color: var(--success);
            background: #f9f9f9; /* Fundo sutil, sem gradiente */
        }

        .player-card.copied {
            border-left-color: var(--warning);
            background: #f9f9f9;
        }

        .player-info {
            flex: 1;
        }

        .player-info strong {
            display: block;
            font-size: 1rem; /* Menor */
            margin-bottom: 4px;
        }

        .player-info .status {
            font-size: 0.8rem;
            color: var(--text-light);
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .player-info .status .dot {
            width: 6px; /* Menor */
            height: 6px;
            border-radius: 50%;
            background: var(--danger-light);
        }

        .player-card.paid .player-info .status .dot {
            background: var(--success);
        }

        .player-card.copied .player-info .status .dot {
            background: var(--warning);
        }

        .player-actions {
            display: flex;
            gap: 6px;
        }

        .btn {
            padding: 6px 12px; /* Menor */
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.8rem;
            font-weight: 500;
            transition: all 0.2s;
        }

        .btn-pay {
            background: var(--success);
            color: white;
        }

        .btn-pay:hover {
            background: var(--success-light);
        }

        .btn-unpay {
            background: var(--warning);
            color: white;
        }

        .btn-unpay:hover {
            background: #ef6c00;
        }

        .btn-remove {
            background: #ffebee;
            color: var(--danger);
        }

        .btn-remove:hover {
            background: var(--danger);
            color: white;
        }

        /* Histórico - Reformulado: dividido por meses com abas */
        .history-section {
            background: var(--card);
            padding: 15px;
            border-radius: 10px;
            box-shadow: var(--shadow);
        }

        .history-list {
            max-height: 250px; /* Menor */
            overflow-y: auto;
        }

        /* Novo: Grupos por mês */
        .month-group {
            margin-bottom: 15px;
            border: 1px solid var(--border);
            border-radius: 8px;
            overflow: hidden;
        }

        .month-header {
            background: var(--primary);
            color: white;
            padding: 10px 15px;
            cursor: pointer;
            font-weight: 600;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .month-header:hover {
            background: var(--primary-dark);
        }

        .month-content {
            display: none; /* Inicialmente oculto; JS pode mostrar */
            padding: 10px;
        }

        .month-content.show {
            display: block;
        }

        .history-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
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

        .history-item.active {
            background: #e3f2fd;
        }

        .history-month {
            font-weight: 600;
        }

        .history-stats {
            text-align: right;
            font-size: 0.8rem;
            color: var(--text-light);
        }

        .history-profit {
            font-weight: 600;
            color: var(--success);
        }

        /* Novo: Para meses passados, ocultar destaque de perda */
        .past-month .history-loss {
            color: var(--text-light); /* Neutro, sem vermelho */
            font-weight: normal;
        }

        .current-month .history-loss {
            font-weight: 600;
            color: var(--danger); /* Mantém destaque apenas no mês atual */
        }

        /* Estado Vazio */
        .empty-state {
            text-align: center;
            padding: 30px 15px; /* Menor */
            color: var(--text-light);
        }

        .empty-state svg {
            width: 50px; /* Menor */
            height: 50px;
            margin-bottom: 10px;
            opacity: 0.4;
        }

        /* Modal - Mantido, mas ajustado */
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
            background: var(--card);
            padding: 20px;
            border-radius: 12px;
            width: 100%;
            max-width: 450px; /* Menor */
            max-height: 70vh; /* Menor */
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--border);
        }

        .modal-header h2 {
            color: var(--primary);
            font-size: 1.1rem;
        }

        .close-modal {
            background: none;
            border: none;
            font-size: 1.6rem;
            cursor: pointer;
            color: var(--text-light);
            line-height: 1;
        }

        .close-modal:hover {
            color: var(--danger);
        }

        .log-item {
            padding: 8px 0;
            border-bottom: 1px solid var(--border);
        }

        .log-item:last-child {
            border-bottom: none;
        }

        .log-date {
            font-size: 0.75rem;
            color: var(--text-light);
            margin-bottom: 3px;
        }

        .log-message {
            font-size: 0.9rem;
        }

        /* Toast Notification */
        .toast {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: var(--success);
            color: white;
            padding: 12px 20px; /* Menor */
            border-radius: 6px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.2);
            transform: translateY(100px);
            opacity: 0;
            transition: all 0.3s;
            z-index: 2000;
        }

        .toast.show {
            transform: translateY(0);
            opacity: 1;
        }

        .toast.error {
            background: var(--danger);
        }

        /* Info Box */
        .info-box {
            background: #e3f2fd;
            border: 1px solid var(--primary);
            border-radius: 6px;
            padding: 10px 12px; /* Menor */
            margin-bottom: 12px;
            font-size: 0.85rem;
            color: var(--primary-dark);
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .info-box svg {
            width: 20px; /* Menor */
            height: 20px;
            flex-shrink: 0;
        }

        /* Responsive - Melhorado */
        @media (max-width: 600px) {
            .dashboard {
                grid-template-columns: repeat(2, 1fr);
            }

            .month-selector {
                flex-direction: column;
                gap: 15px;
            }

            .month-actions {
                width: 100%;
                justify-content: center;
            }

            .player-card {
                flex-direction: column;
                gap: 12px;
                text-align: center;
            }

            .player-actions {
                width: 100%;
                justify-content: center;
            }

            .add-form .input-row {
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
        <!-- Header -->
        <header>
            <h1>⚽ Gestão Futsal</h1>
            <p>Mensalidade: R$ 30,00 | Aluguel: R$ 220,00</p>
        </header>

        <!-- Seleção de Mês -->
        <div class="month-selector">
            <div class="month-nav">
                <button onclick="navigateMonth(-1)">&#8249;</button>
                <span class="current-month" id="currentMonth">Carregando...</span>
                <button onclick="navigateMonth(1)">&#8250;</button>
            </div>
            <div class="month-actions">
                <button class="btn-month btn-copy" onclick="copyPlayersFromPreviousMonth()">
                        <!-- Info Box -->
        <div class="info-box" id="infoBox" style="display: none;">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <circle cx="12" cy="12" r="10"></circle>
                <line x1="12" y1="16" x2="12" y2="12"></line>
                <line x1="12" y1="8" x2="12.01" y2="8"></line>
            </svg>
            <span id="infoText"></span>
        </div>

        <!-- Dashboard - Simplificado: apenas 3 cards essenciais -->
        <div class="dashboard">
            <div class="card">
                <h3>Total</h3>
                <div class="value" id="totalPlayers">0</div>
            </div>
            <div class="card">
                <h3>Pagos</h3>
                <div class="value success" id="paidPlayers">0</div>
            </div>
            <div class="card">
                <h3>Pendentes</h3>
                <div class="value warning" id="pendingPlayers">0</div>
            </div>
        </div>

        <!-- Formulário de Adição -->
        <div class="section-header">
            <h2>Jogadores</h2>
        </div>
        
        <div class="add-form">
            <div class="input-row">
                <input type="text" id="playerName" placeholder="Digite o nome do jogador..." autocomplete="off">
                <button class="btn-add" onclick="addPlayer()">+ Adicionar</button>
            </div>
        </div>

        <!-- Lista de Jogadores -->
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

        <!-- Histórico -->
        <div class="history-section">
            <div class="section-header">
                <h2>📅 Histórico de Meses</h2>
                <button class="btn" style="background: var(--primary); color: white;" onclick="showLogs()">Ver Logs</button>
            </div>
            <div class="history-list" id="historyList">
                <div class="empty-state">
                    <p>Nenhum histórico encontrado</p>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal de Logs -->
    <div class="modal-overlay" id="logsModal" onclick="closeLogs(event)">
        <div class="modal" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h2>📊 Extrato de Movimentações</h2>
                <button class="close-modal" onclick="closeLogsModal()">&times;</button>
            </div>
            <div id="logsContent"></div>
        </div>
    </div>

    <!-- Toast Notification -->
    <div class="toast" id="toast"></div>

    <script>
        // ==================== CONFIGURAÇÕES ====================
        const CONFIG = {
            MONTHLY_FEE: 30,
            GYM_RENT: 220
        };

        // ==================== ESTADO ====================
        let currentDate = new Date();
        let currentMonthKey = '';
        let allData = {};

        // ==================== INICIALIZAÇÃO ====================
        function init() {
            try {
                // Carrega dados do localStorage
                const savedData = localStorage.getItem('futsalData');
                if (savedData) {
                    allData = JSON.parse(savedData);
                }

                // Define mês atual
                currentMonthKey = getMonthKey(currentDate);
                
                // Inicializa mês se não existir
                if (!allData[currentMonthKey]) {
                    allData[currentMonthKey] = {
                        players: [],
                        logs: []
                    };
                }
                
                // Verifica se há jogadores copiados
                checkCopiedPlayers();
                updateMonthDisplay();
                renderAll();
            } catch (error) {
                console.error('Erro na inicialização:', error);
                showToast('Erro ao carregar dados', true);
            }
        }

        function updateMonthDisplay() {
            const monthName = getMonthName(currentDate.getMonth() + 1) + ' ' + currentDate.getFullYear();
            document.getElementById('currentMonth').textContent = monthName;
        }

        function renderAll() {
            renderDashboard();
            renderPlayerList();
            renderHistory();
        }

        function renderDashboard() {
            const players = allData[currentMonthKey].players;
            const total = players.length;
            const paid = players.filter(p => p.paid).length;
            const pending = total - paid;

            document.getElementById('totalPlayers').textContent = total;
            document.getElementById('paidPlayers').textContent = paid;
            document.getElementById('pendingPlayers').textContent = pending;
        }

        function renderPlayerList() {
            const list = document.getElementById('playerList');
            const players = allData[currentMonthKey].players;

            if (players.length === 0) {
                list.innerHTML = 
                    '<div class="empty-state">' +
                        '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">' +
                            '<path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"></path>' +
                            '<circle cx="9" cy="7" r="4"></circle>' +
                            '<path d="M23 21v-2a4 4 0 0 0-3-3.87"></path>' +
                            '<path d="M16 3.13a4 4 0 0 1 0 7.75"></path>' +
                        '</svg>' +
                        '<p>Nenhum jogador cadastrado neste mês</p>' +
                    '</div>';
                return;
            }

            list.innerHTML = players.map(player => {
                const isCopied = player.copiedFrom ? true : false;
                const cardClass = 'player-card ' + (player.paid ? 'paid' : '') + (isCopied ? ' copied' : '');
                const statusText = player.paid 
                    ? 'Pago em ' + formatDate(player.lastPaymentDate)
                    : (isCopied ? 'Pendente (copiado)' : 'Pendente');
                
                return '<div class="' + cardClass + '">' +
                    '<div class="player-info">' +
                        '<strong>' + escapeHtml(player.name) + '</strong>' +
                        '<span class="status">' +
                            '<span class="dot"></span>' +
                            statusText +
                        '</span>' +
                    '</div>' +
                    '<div class="player-actions">' +
                        '<button class="btn ' + (player.paid ? 'btn-unpay' : 'btn-pay') + '" ' +
                                'onclick="togglePayment(' + player.id + ')">' +
                            (player.paid ? 'Desmarcar' : 'Pago R$ 30') +
                        '</button>' +
                        '<button class="btn btn-remove" onclick="removePlayer(' + player.id + ')">X</button>' +
                    '</div>' +
                '</div>';
            }).join('');
        }

        function renderHistory() {
            const historyList = document.getElementById('historyList');
            const sortedKeys = Object.keys(allData).sort().reverse();

            if (sortedKeys.length === 0) {
                historyList.innerHTML = '<div class="empty-state"><p>Nenhum histórico encontrado</p></div>';
                return;
            }

            // Agrupar por ano e mês
            const groupedByYear = {};
            sortedKeys.forEach(key => {
                const [year, month] = key.split('-');
                if (!groupedByYear[year]) groupedByYear[year] = {};
                groupedByYear[year][month] = key;
            });

            historyList.innerHTML = Object.keys(groupedByYear).sort().reverse().map(year => {
                return Object.keys(groupedByYear[year]).sort().reverse().map(month => {
                    const key = groupedByYear[year][month];
                    const monthData = allData[key];
                    const paidCount = monthData.players.filter(p => p.paid).length;
                    const collected = paidCount * CONFIG.MONTHLY_FEE;
                    const profit = collected - CONFIG.GYM_RENT;
                    const isCurrentMonth = key === currentMonthKey;
                    const monthClass = isCurrentMonth ? 'current-month' : 'past-month';

                    return '<div class="month-group">' +
                        '<div class="month-header" onclick="toggleMonthGroup(this)">' +
                            '<span>' + getMonthName(parseInt(month)) + ' ' + year + (isCurrentMonth ? ' (Atual)' : '') + '</span>' +
                            '<span class="history-stats">' +
                                monthData.players.length + ' jogadores | ' + paidCount + ' pagos | ' +
                                '<span class="' + (profit >= 0 ? 'history-profit' : 'history-loss ' + monthClass) + '">' +
                                    (profit >= 0 ? '+' : '') + 'R$ ' + profit +
                                '</span>' +
                            '</span>' +
                        '</div>' +
                        '<div class="month-content">' +
                            (monthData.players.length > 0 ? monthData.players.map(player => {
                                const status = player.paid ? 'Pago' : 'Pendente';
                                return '<div class="history-item">' +
                                    '<div class="history-month">' + escapeHtml(player.name) + '</div>' +
                                    '<div class="history-stats">' + status + '</div>' +
                                '</div>';
                            }).join('') : '<div class="history-item">Nenhum jogador</div>') +
                        '</div>' +
                    '</div>';
                }).join('');
            }).join('');
        }

        function toggleMonthGroup(header) {
            const content = header.nextElementSibling;
            content.classList.toggle('show');
        }

        function selectMonth(key) {
            const [year, month] = key.split('-');
            currentDate = new Date(parseInt(year), parseInt(month) - 1, 1);
            currentMonthKey = key;
            
            if (!allData[currentMonthKey]) {
                allData[currentMonthKey] = {
                    players: [],
                    logs: []
                };
            }
            
            checkCopiedPlayers();
            updateMonthDisplay();
            renderAll();
        }

        // ==================== AÇÕES DOS JOGADORES ====================
        function addPlayer() {
            const input = document.getElementById('playerName');
            const name = input.value.trim();
            
            if (!name) {
                showInputError();
                return;
            }
            
            // Verifica se já existe
            const exists = allData[currentMonthKey].players.some(p => p.name.toLowerCase() === name.toLowerCase());
            if (exists) {
                showToast('Jogador já existe neste mês', true);
                showInputError();
                return;
            }
            
            const player = {
                id: Date.now(),
                name: name,
                paid: false,
                lastPaymentDate: null,
                copiedFrom: null
            };
            
            allData[currentMonthKey].players.push(player);
            addLog('Jogador adicionado: ' + name);
            saveData();
            renderAll();
            
            input.value = '';
            showToast('Jogador adicionado com sucesso!');
        }

        function togglePayment(playerId) {
            const player = allData[currentMonthKey].players.find(p => p.id === playerId);
            if (!player) return;
            
            player.paid = !player.paid;
            player.lastPaymentDate = player.paid ? new Date().toISOString() : null;
            
            addLog(player.name + ' ' + (player.paid ? 'pagou' : 'desmarcou pagamento'));
            saveData();
            renderAll();
            
            showToast(player.paid ? 'Pagamento confirmado!' : 'Pagamento desmarcado');
        }

        function removePlayer(playerId) {
            const index = allData[currentMonthKey].players.findIndex(p => p.id === playerId);
            if (index === -1) return;
            
            const player = allData[currentMonthKey].players[index];
            allData[currentMonthKey].players.splice(index, 1);
            
            addLog('Jogador removido: ' + player.name);
            saveData();
            renderAll();
            
            showToast('Jogador removido');
        }

        // ==================== NAVEGAÇÃO DE MESES ====================
        function navigateMonth(direction) {
            currentDate.setMonth(currentDate.getMonth() + direction);
            currentMonthKey = getMonthKey(currentDate);
            
            if (!allData[currentMonthKey]) {
                allData[currentMonthKey] = {
                    players: [],
                    logs: []
                };
            }
            
            checkCopiedPlayers();
            updateMonthDisplay();
            renderAll();
        }

        function createNewMonth() {
            const nextMonth = new Date(currentDate);
            nextMonth.setMonth(nextMonth.getMonth() + 1);
            const nextKey = getMonthKey(nextMonth);
            
            if (allData[nextKey]) {
                showToast('Mês já existe', true);
                return;
            }
            
            allData[nextKey] = {
                players: [],
                logs: []
            };
            
            addLog('Novo mês criado: ' + getMonthName(nextMonth.getMonth() + 1) + ' ' + nextMonth.getFullYear());
            saveData();
            
            // Navega para o novo mês
            currentDate = nextMonth;
            currentMonthKey = nextKey;
            updateMonthDisplay();
            renderAll();
            
            showToast('Novo mês criado!');
        }

        function copyPlayersFromPreviousMonth() {
            const prevMonth = new Date(currentDate);
            prevMonth.setMonth(prevMonth.getMonth() - 1);
            const prevKey = getMonthKey(prevMonth);
            
            if (!allData[prevKey] || allData[prevKey].players.length === 0) {
                showToast('Nenhum jogador no mês anterior', true);
                return;
            }
            
            const copiedPlayers = allData[prevKey].players.map(player => ({
                id: Date.now() + Math.random(),
                name: player.name,
                paid: false,
                lastPaymentDate: null,
                copiedFrom: prevKey
            }));
            
            allData[currentMonthKey].players = copiedPlayers;
            addLog('Jogadores copiados do mês anterior');
            saveData();
            renderAll();
            
            showToast('Jogadores copiados com sucesso!');
        }

        function checkCopiedPlayers() {
            const players = allData[currentMonthKey].players;
            players.forEach(player => {
                if (player.copiedFrom) {
                    const originalMonth = allData[player.copiedFrom];
                    if (!originalMonth || !originalMonth.players.some(p => p.name === player.name)) {
                        // Remove se o original foi deletado
                        const index = players.indexOf(player);
                        if (index > -1) players.splice(index, 1);
                    }
                }
            });
        }

        // ==================== LOGS ====================
        function addLog(message) {
            const log = {
                date: new Date().toISOString(),
                message: message
            };
            
            allData[currentMonthKey].logs.push(log);
            saveData();
        }

        function showLogs() {
            const logs = allData[currentMonthKey].logs;
            const content = document.getElementById('logsContent');
            
            if (logs.length === 0) {
                content.innerHTML = '<p>Nenhum log encontrado</p>';
            } else {
                content.innerHTML = logs.map(log => 
                    '<div class="log-item">' +
                        '<div class="log-date">' + formatDate(log.date) + '</div>' +
                        '<div class="log-message">' + escapeHtml(log.message) + '</div>' +
                    '</div>'
                ).join('');
            }
            
            document.getElementById('logsModal').style.display = 'flex';
        }

        function closeLogs(event) {
            if (event.target.id === 'logsModal') {
                closeLogsModal();
            }
        }

        function closeLogsModal() {
            document.getElementById('logsModal').style.display = 'none';
        }

        // ==================== UTILIDADES ====================
        function saveData() {
            try {
                localStorage.setItem('futsalData', JSON.stringify(allData));
            } catch (error) {
                console.error('Erro ao salvar:', error);
                showToast('Erro ao salvar dados', true);
            }
        }

        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }

        function showToast(message, isError = false) {
            const toast = document.getElementById('toast');
            toast.textContent = message;
            toast.className = 'toast show' + (isError ? ' error' : '');
            
            setTimeout(function() {
                toast.className = 'toast';
            }, 3000);
        }

        function showInputError() {
            const input = document.getElementById('playerName');
            input.classList.add('error');
            input.focus();
            
            setTimeout(function() {
                input.classList.remove('error');
            }, 500);
        }

        function getMonthKey(date) {
            return date.getFullYear() + '-' + String(date.getMonth() + 1).padStart(2, '0');
        }

        function getMonthName(month) {
            const names = ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho',
                          'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'];
            return names[month - 1];
        }

        function formatDate(dateString) {
            const date = new Date(dateString);
                        return date.toLocaleDateString('pt-BR');
        }

        // ==================== EVENTOS ====================
        document.getElementById('playerName').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                addPlayer();
            }
        });

        document.addEventListener('keydown', function(e) {
            if (e.key === 'Escape') {
                closeLogsModal();
            }
        });

        // Inicializa quando a página carregar
        window.onload = init;
    </script>
</body>
</html>
