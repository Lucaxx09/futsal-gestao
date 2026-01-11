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
            --shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
            background-color: var(--bg);
            color: var(--text);
            min-height: 100vh;
            padding-bottom: 40px;
        }

        /* Container Principal */
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 0 15px;
        }

        /* Header */
        header {
            background: linear-gradient(135deg, var(--primary), var(--primary-dark));
            color: white;
            padding: 25px 20px;
            margin-bottom: 20px;
            border-radius: 0 0 20px 20px;
            box-shadow: 0 4px 15px rgba(21, 101, 192, 0.3);
        }

        header h1 {
            font-size: 1.6rem;
            margin-bottom: 5px;
        }

        header p {
            opacity: 0.9;
            font-size: 0.9rem;
        }

        /* Seleção de Mês */
        .month-selector {
            background: var(--card);
            padding: 20px;
            border-radius: 12px;
            box-shadow: var(--shadow);
            margin-bottom: 20px;
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            align-items: center;
            justify-content: space-between;
        }

        .month-nav {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .month-nav button {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            border: none;
            background: var(--primary);
            color: white;
            font-size: 1.2rem;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .month-nav button:hover {
            background: var(--primary-dark);
            transform: scale(1.1);
        }

        .month-nav button:disabled {
            background: #ccc;
            cursor: not-allowed;
            transform: none;
        }

        .current-month {
            font-size: 1.2rem;
            font-weight: 600;
            color: var(--primary);
            min-width: 180px;
            text-align: center;
        }

        .btn-new-month {
            background: var(--warning);
            color: white;
            border: none;
            padding: 10px 18px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 500;
            font-size: 0.9rem;
            transition: all 0.2s;
        }

        .btn-new-month:hover {
            background: #e65100;
        }

        /* Dashboard */
        .dashboard {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            margin-bottom: 20px;
        }

        .dashboard .card {
            background: var(--card);
            padding: 18px 15px;
            border-radius: 10px;
            box-shadow: var(--shadow);
            text-align: center;
        }

        .dashboard .card h3 {
            font-size: 0.75rem;
            color: var(--text-light);
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 8px;
        }

        .dashboard .card .value {
            font-size: 1.4rem;
            font-weight: 700;
            color: var(--primary);
        }

        .dashboard .card .value.success { color: var(--success); }
        .dashboard .card .value.danger { color: var(--danger); }
        .dashboard .card .value.warning { color: var(--warning); }

        .dashboard .card.full-width {
            grid-column: span 3;
        }

        /* Título de Seção */
        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--primary);
        }

        .section-header h2 {
            font-size: 1.1rem;
            color: var(--text);
        }

        /* Formulário de Adição */
        .add-form {
            background: var(--card);
            padding: 20px;
            border-radius: 12px;
            box-shadow: var(--shadow);
            margin-bottom: 20px;
        }

        .add-form .input-row {
            display: flex;
            gap: 10px;
        }

        .add-form input {
            flex: 1;
            padding: 12px 15px;
            border: 2px solid var(--border);
            border-radius: 8px;
            font-size: 1rem;
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
            padding: 12px 25px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            font-size: 1rem;
            transition: all 0.2s;
            white-space: nowrap;
        }

        .btn-add:hover {
            background: var(--success-light);
        }

        /* Lista de Jogadores */
        .player-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin-bottom: 25px;
        }

        .player-card {
            background: var(--card);
            padding: 15px 20px;
            border-radius: 10px;
            box-shadow: var(--shadow);
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-left: 4px solid var(--danger-light);
            transition: all 0.2s;
        }

        .player-card:hover {
            box-shadow: 0 4px 15px rgba(0,0,0,0.15);
        }

        .player-card.paid {
            border-left-color: var(--success);
            background: linear-gradient(90deg, #e8f5e9 0%, var(--card) 50%);
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
            color: var(--text-light);
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .player-info .status .dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: var(--danger-light);
        }

        .player-card.paid .player-info .status .dot {
            background: var(--success);
        }

        .player-actions {
            display: flex;
            gap: 8px;
        }

        .btn {
            padding: 8px 14px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.85rem;
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

        /* Histórico */
        .history-section {
            background: var(--card);
            padding: 20px;
            border-radius: 12px;
            box-shadow: var(--shadow);
        }

        .history-list {
            max-height: 300px;
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

        .history-item.active {
            background: #e3f2fd;
        }

        .history-month {
            font-weight: 600;
        }

        .history-stats {
            text-align: right;
            font-size: 0.85rem;
            color: var(--text-light);
        }

        .history-profit {
            font-weight: 600;
            color: var(--success);
        }

        .history-loss {
            font-weight: 600;
            color: var(--danger);
        }

        /* Estado Vazio */
        .empty-state {
            text-align: center;
            padding: 40px 20px;
            color: var(--text-light);
        }

        .empty-state svg {
            width: 60px;
            height: 60px;
            margin-bottom: 15px;
            opacity: 0.4;
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
            background: var(--card);
            padding: 25px;
            border-radius: 15px;
            width: 100%;
            max-width: 500px;
            max-height: 80vh;
            overflow-y: auto;
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
            font-size: 1.2rem;
        }

        .close-modal {
            background: none;
            border: none;
            font-size: 1.8rem;
            cursor: pointer;
            color: var(--text-light);
            line-height: 1;
        }

        .close-modal:hover {
            color: var(--danger);
        }

        .log-item {
            padding: 10px 0;
            border-bottom: 1px solid var(--border);
        }

        .log-item:last-child {
            border-bottom: none;
        }

        .log-date {
            font-size: 0.8rem;
            color: var(--text-light);
            margin-bottom: 3px;
        }

        .log-message {
            font-size: 0.95rem;
        }

        /* Toast Notification */
        .toast {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: var(--success);
            color: white;
            padding: 15px 25px;
            border-radius: 8px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
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

        /* Responsividade */
        @media (max-width: 600px) {
            .dashboard {
                grid-template-columns: repeat(2, 1fr);
            }

            .dashboard .card.full-width {
                grid-column: span 2;
            }

            .month-selector {
                flex-direction: column;
                gap: 15px;
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
            <button class="btn-new-month" onclick="createNewMonth()">+ Novo Mês</button>
        </div>

        <!-- Dashboard -->
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
            <div class="card">
                <h3>Arrecadado</h3>
                <div class="value" id="totalCollected">R$ 0</div>
            </div>
            <div class="card">
                <h3>Aluguel</h3>
                <div class="value danger">-R$ 220</div>
            </div>
            <div class="card full-width">
                <h3>Líquido (Arrecadação - Aluguel)</h3>
                <div class="value" id="netProfit">R$ 0</div>
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

                // Atualiza display
                updateMonthDisplay();
                
                // Renderiza tudo
                renderAll();

                console.log('Sistema inicializado com sucesso!');
            } catch (error) {
                console.error('Erro na inicialização:', error);
                showToast('Erro ao carregar dados', true);
            }
        }

        // ==================== FUNÇÕES DE DATA ====================
        function getMonthKey(date) {
            const year = date.getFullYear();
            const month = date.getMonth() + 1;
            return year + '-' + month.toString().padStart(2, '0');
        }

        function getMonthName(monthNumber) {
            const months = [
                'Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho',
                'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'
            ];
            return months[monthNumber - 1];
        }

        function formatDate(dateString) {
            const date = new Date(dateString);
            return date.toLocaleDateString('pt-BR', {
                day: '2-digit',
                month: '2-digit',
                year: 'numeric',
                hour: '2-digit',
                minute: '2-digit'
            });
        }

        // ==================== NAVEGAÇÃO ====================
        function navigateMonth(direction) {
            currentDate.setMonth(currentDate.getMonth() + direction);
            currentMonthKey = getMonthKey(currentDate);
            
            if (!allData[currentMonthKey]) {
                allData[currentMonthKey] = {
                    players: [],
                    logs: []
                };
            }
            
            updateMonthDisplay();
            renderAll();
        }

        function updateMonthDisplay() {
            const monthName = getMonthName(currentDate.getMonth() + 1);
            const year = currentDate.getFullYear();
            document.getElementById('currentMonth').textContent = monthName + ' ' + year;
        }

        function createNewMonth() {
            const nextMonth = new Date(currentDate);
            nextMonth.setMonth(nextMonth.getMonth() + 1);
            
            const nextMonthKey = getMonthKey(nextMonth);
            const monthName = getMonthName(nextMonth.getMonth() + 1);
            
            if (confirm('Criar dados para ' + monthName + ' de ' + nextMonth.getFullYear() + '?')) {
                currentDate = nextMonth;
                currentMonthKey = nextMonthKey;
                
                if (!allData[currentMonthKey]) {
                    allData[currentMonthKey] = {
                        players: [],
                        logs: []
                    };
                }
                
                updateMonthDisplay();
                renderAll();
                showToast('Mês criado com sucesso!');
            }
        }

        // ==================== JOGADORES ====================
        function addPlayer() {
            const input = document.getElementById('playerName');
            const name = input.value.trim();
            
            if (name === '') {
                showInputError();
                showToast('Digite o nome do jogador', true);
                return;
            }

            const newPlayer = {
                id: Date.now(),
                name: name,
                paid: false,
                lastPaymentDate: null
            };

            allData[currentMonthKey].players.push(newPlayer);
            addLog('Jogador adicionado: ' + name);
            
            input.value = '';
            saveData();
            renderAll();
            showToast('Jogador adicionado!');
            
            // Foca no input para adicionar mais
            input.focus();
        }

        function togglePayment(playerId) {
            const player = allData[currentMonthKey].players.find(p => p.id === playerId);
            
            if (player) {
                player.paid = !player.paid;
                player.lastPaymentDate = player.paid ? new Date().toISOString() : null;
                
                if (player.paid) {
                    addLog('Pagamento recebido: ' + player.name + ' (R$ ' + CONFIG.MONTHLY_FEE + ')');
                    showToast(player.name + ' pagou R$ ' + CONFIG.MONTHLY_FEE);
                } else {
                    addLog('Pagamento estornado: ' + player.name);
                    showToast('Pagamento estornado');
                }
                
                saveData();
                renderAll();
            }
        }

        function removePlayer(playerId) {
            const player = allData[currentMonthKey].players.find(p => p.id === playerId);
            
            if (player && confirm('Remover ' + player.name + ' da lista?')) {
                addLog('Jogador removido: ' + player.name);
                allData[currentMonthKey].players = allData[currentMonthKey].players.filter(p => p.id !== playerId);
                saveData();
                renderAll();
                showToast('Jogador removido');
            }
        }

        // ==================== LOGS ====================
        function addLog(message) {
            const log = {
                date: new Date().toISOString(),
                message: message
            };
            allData[currentMonthKey].logs.unshift(log);
            saveData();
        }

        function showLogs() {
            const logs = allData[currentMonthKey].logs;
            const container = document.getElementById('logsContent');
            
            if (logs.length === 0) {
                container.innerHTML = '<div class="empty-state"><p>Nenhuma movimentação neste mês</p></div>';
            } else {
                container.innerHTML = logs.map(log => 
                    '<div class="log-item">' +
                        '<div class="log-date">' + formatDate(log.date) + '</div>' +
                        '<div class="log-message">' + escapeHtml(log.message) + '</div>' +
                    '</div>'
                ).join('');
            }
            
            document.getElementById('logsModal').style.display = 'flex';
        }

        function closeLogsModal() {
            document.getElementById('logsModal').style.display = 'none';
        }

        function closeLogs(event) {
            if (event.target.id === 'logsModal') {
                closeLogsModal();
            }
        }

        // ==================== RENDERIZAÇÃO ====================
        function renderAll() {
            renderDashboard();
            renderPlayerList();
            renderHistory();
        }

        function renderDashboard() {
            const players = allData[currentMonthKey].players;
            const totalPlayers = players.length;
            const paidPlayers = players.filter(p => p.paid).length;
            const pendingPlayers = totalPlayers - paidPlayers;
            const totalCollected = paidPlayers * CONFIG.MONTHLY_FEE;
            const netProfit = totalCollected - CONFIG.GYM_RENT;

            document.getElementById('totalPlayers').textContent = totalPlayers;
            document.getElementById('paidPlayers').textContent = paidPlayers;
            document.getElementById('pendingPlayers').textContent = pendingPlayers;
            document.getElementById('totalCollected').textContent = 'R$ ' + totalCollected;

            const profitElement = document.getElementById('netProfit');
            profitElement.textContent = 'R$ ' + netProfit;
            
            if (netProfit >= 0) {
                profitElement.className = 'value success';
            } else {
                profitElement.className = 'value danger';
            }
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

            list.innerHTML = players.map(player => 
                '<div class="player-card ' + (player.paid ? 'paid' : '') + '">' +
                    '<div class="player-info">' +
                        '<strong>' + escapeHtml(player.name) + '</strong>' +
                        '<span class="status">' +
                            '<span class="dot"></span>' +
                            (player.paid ? 'Pago em ' + formatDate(player.lastPaymentDate) : 'Pendente') +
                        '</span>' +
                    '</div>' +
                    '<div class="player-actions">' +
                        '<button class="btn ' + (player.paid ? 'btn-unpay' : 'btn-pay') + '" ' +
                                'onclick="togglePayment(' + player.id + ')">' +
                            (player.paid ? 'Desmarcar' : 'Pago R$ 30') +
                        '</button>' +
                        '<button class="btn btn-remove" onclick="removePlayer(' + player.id + ')">X</button>' +
                    '</div>' +
                '</div>'
            ).join('');
        }

        function renderHistory() {
            const historyList = document.getElementById('historyList');
            const sortedKeys = Object.keys(allData).sort().reverse();

            if (sortedKeys.length === 0) {
                historyList.innerHTML = '<div class="empty-state"><p>Nenhum histórico encontrado</p></div>';
                return;
            }

            historyList.innerHTML = sortedKeys.map(key => {
                const monthData = allData[key];
                const [year, month] = key.split('-');
                const paidCount = monthData.players.filter(p => p.paid).length;
                const collected = paidCount * CONFIG.MONTHLY_FEE;
                const profit = collected - CONFIG.GYM_RENT;
                const isCurrentMonth = key === currentMonthKey;

                return '<div class="history-item ' + (isCurrentMonth ? 'active' : '') + '" ' +
                             'onclick="selectMonth(\'' + key + '\')" ' +
                             'style="' + (isCurrentMonth ? 'background: #e3f2fd;' : '') + '">' +
                    '<div class="history-month">' +
                        getMonthName(parseInt(month)) + ' ' + year +
                        (isCurrentMonth ? ' (Atual)' : '') +
                    '</div>' +
                    '<div class="history-stats">' +
                        '<div>' + monthData.players.length + ' jogadores | ' + paidCount + ' pagos</div>' +
                        '<div class="' + (profit >= 0 ? 'history-profit' : 'history-loss') + '">' +
                            (profit >= 0 ? '+' : '') + 'R$ ' + profit +
                        '</div>' +
                    '</div>' +
                '</div>';
            }).join('');
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
            
            updateMonthDisplay();
            renderAll();
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
