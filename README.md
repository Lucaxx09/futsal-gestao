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

        /* Dashboard - Simplificado: apenas 3 cards essenciais, sem full-width */
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
                    📋 Copiar Jogadores
                </button>
                <button class="btn-month" onclick="createNewMonth()">
                    + Novo Mês
                </button>
            </div>
        </div>

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
        <div class="
