<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Diseñador de Franelas Deportivas (CMYK/RGB)</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fabric.js/5.3.1/fabric.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #4361ee;
            --primary-light: #6a7fef;
            --primary-dark: #3a0ca3;
            --secondary: #3a0ca3;
            --accent: #4895ef;
            --accent-light: #6daaf2;
            --light: #f8f9fa;
            --light-transparent: rgba(248, 249, 250, 0.8);
            --dark: #212529;
            --dark-transparent: rgba(33, 37, 41, 0.9);
            --success: #4cc9f0;
            --danger: #dc3545;
            --danger-light: #e4606d;
            --warning: #ffc107;
            --rounded: 16px;
            --rounded-lg: 24px;
            --rounded-xl: 32px;
            --shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
            --shadow-lg: 0 12px 32px rgba(0, 0, 0, 0.2);
            --gradient-primary: linear-gradient(135deg, var(--primary) 0%, var(--secondary) 100%);
            --gradient-accent: linear-gradient(135deg, var(--accent) 0%, var(--primary-light) 100%);
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
        }
        
        body {
            width: 100%;
            min-height: 100vh;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            color: var(--dark);
            overflow-x: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        
        /* Estilos para el login */
        .login-container {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.8);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        
        .login-box {
            background: white;
            padding: 30px;
            border-radius: var(--rounded-xl);
            width: 100%;
            max-width: 400px;
            box-shadow: var(--shadow-lg);
        }
        
        .login-box h2 {
            text-align: center;
            margin-bottom: 20px;
            color: var(--primary);
        }
        
        .login-form .form-group {
            margin-bottom: 20px;
        }
        
        .login-form label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
        }
        
        .login-form input {
            width: 100%;
            padding: 12px;
            border: 2px solid #eee;
            border-radius: var(--rounded);
            font-size: 16px;
            transition: all 0.3s ease;
        }
        
        .login-form input:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
        }
        
        .login-btn {
            width: 100%;
            padding: 12px;
            background: var(--gradient-primary);
            color: white;
            border: none;
            border-radius: var(--rounded);
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .login-btn:hover {
            transform: translateY(-2px);
            box-shadow: var(--shadow);
        }
        
        .error-message {
            color: var(--danger);
            font-size: 14px;
            margin-top: 10px;
            text-align: center;
            display: none;
        }

        /* Estilos de la aplicación principal */
        .app-container {
            width: 100%;
            max-width: 1400px;
            min-height: 90vh;
            background: white;
            border-radius: var(--rounded-xl);
            box-shadow: var(--shadow-lg);
            overflow: hidden;
            display: flex;
            flex-direction: column;
            display: none; /* Oculto inicialmente */
        }
        
        .app-header {
            padding: 16px 24px;
            background: var(--gradient-primary);
            color: white;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
            position: relative;
        }
        
        .app-header::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: var(--accent);
        }
        
        .app-header h1 {
            font-size: 1.5rem;
            font-weight: 600;
            text-shadow: 0 2px 4px rgba(0,0,0,0.2);
        }
        
        .header-actions {
            display: flex;
            gap: 12px;
        }
        
        .btn {
            border: none;
            border-radius: var(--rounded);
            padding: 10px 16px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            position: relative;
            overflow: hidden;
            z-index: 1;
        }
        
        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--gradient-primary);
            z-index: -1;
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        
        .btn:hover::before {
            opacity: 1;
        }
        
        .btn-primary {
            background: var(--gradient-primary);
            color: white;
            box-shadow: var(--shadow);
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: var(--shadow-lg);
        }
        
        .btn-secondary {
            background: white;
            color: var(--primary);
            border: 2px solid var(--primary);
            transition: all 0.3s ease;
        }
        
        .btn-secondary:hover {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
            transform: translateY(-2px);
        }
        
        .btn-danger {
            background: var(--danger);
            color: white;
            box-shadow: var(--shadow);
        }
        
        .btn-danger:hover {
            background: var(--danger-light);
            transform: translateY(-2px);
            box-shadow: var(--shadow-lg);
        }
        
        .btn-warning {
            background: var(--warning);
            color: var(--dark);
            box-shadow: var(--shadow);
        }
        
        .btn-warning:hover {
            background: #ffca2c;
            transform: translateY(-2px);
            box-shadow: var(--shadow-lg);
        }
        
        .main-content {
            display: flex;
            flex: 1;
            height: calc(100vh - 120px);
        }
        
        .toolbar {
            width: 320px;
            background-color: var(--light);
            padding: 16px;
            border-right: 1px solid #eee;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            transition: all 0.3s ease;
        }
        
        @media (max-width: 992px) {
            .toolbar {
                position: fixed;
                top: 0;
                left: -320px;
                bottom: 0;
                z-index: 100;
                background-color: white;
                box-shadow: var(--shadow-lg);
            }
            
            .toolbar.active {
                left: 0;
            }
        }
        
        .tool-section {
            margin-bottom: 24px;
            background: white;
            padding: 16px;
            border-radius: var(--rounded);
            box-shadow: var(--shadow);
        }
        
        .tool-section h3 {
            margin-bottom: 12px;
            color: var(--secondary);
            font-size: 1rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .property-group {
            margin-bottom: 16px;
        }
        
        .property-group label {
            display: block;
            margin-bottom: 8px;
            font-size: 0.85rem;
            color: #555;
            font-weight: 500;
        }
        
        .property-group input[type="color"] {
            width: 100%;
            height: 40px;
            cursor: pointer;
            border: 2px solid #eee;
            border-radius: var(--rounded);
            transition: all 0.3s ease;
        }
        
        .property-group input[type="color"]:hover {
            border-color: var(--primary-light);
        }
        
        .property-group input[type="range"] {
            width: 100%;
            height: 6px;
            border-radius: 3px;
            background: #eee;
            outline: none;
            -webkit-appearance: none;
        }
        
        .property-group input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 18px;
            height: 18px;
            border-radius: 50%;
            background: var(--primary);
            cursor: pointer;
            box-shadow: 0 2px 8px rgba(0,0,0,0.2);
        }
        
        .property-group select {
            width: 100%;
            padding: 10px 12px;
            border-radius: var(--rounded);
            border: 2px solid #eee;
            font-size: 0.85rem;
            transition: all 0.3s ease;
        }
        
        .property-group select:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
            outline: none;
        }
        
        .canvas-container {
            flex: 1;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #f9f9f9;
            position: relative;
            overflow: auto;
        }
        
        #design-canvas {
            border-radius: var(--rounded-lg);
            box-shadow: var(--shadow);
            background-color: white;
            background-image: 
                linear-gradient(45deg, #eee 25%, transparent 25%, transparent 75%, #eee 75%, #eee),
                linear-gradient(45deg, #eee 25%, transparent 25%, transparent 75%, #eee 75%, #eee);
            background-size: 20px 20px;
            background-position: 0 0, 10px 10px;
        }
        
        .template-selector {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 12px;
            margin-top: 12px;
        }
        
        .template-preview {
            border: 2px solid #eee;
            border-radius: var(--rounded);
            padding: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
        }
        
        .template-preview:hover {
            border-color: var(--primary-light);
            transform: translateY(-2px);
            box-shadow: var(--shadow);
        }
        
        .template-preview.selected {
            border-color: var(--primary);
            background-color: rgba(67, 97, 238, 0.1);
            box-shadow: 0 4px 12px rgba(67, 97, 238, 0.2);
        }
        
        .template-preview img {
            width: 100%;
            height: auto;
            display: block;
            border-radius: 4px;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .tabs {
            display: flex;
            border-bottom: 2px solid #eee;
            margin-bottom: 16px;
        }
        
        .tab {
            padding: 8px 16px;
            cursor: pointer;
            border-bottom: 2px solid transparent;
            font-size: 0.85rem;
            font-weight: 500;
            color: #666;
            transition: all 0.3s ease;
        }
        
        .tab.active {
            border-bottom-color: var(--primary);
            color: var(--primary);
            font-weight: 600;
        }
        
        .history-controls {
            display: flex;
            gap: 8px;
            margin-top: 12px;
        }
        
        .history-controls button {
            flex: 1;
            padding: 8px;
            font-size: 0.8rem;
        }
        
        .layer-list {
            margin-top: 12px;
            max-height: 200px;
            overflow-y: auto;
            border: 2px solid #eee;
            border-radius: var(--rounded);
            background: white;
        }
        
        .layer-item {
            padding: 10px 12px;
            border-bottom: 1px solid #eee;
            display: flex;
            align-items: center;
            cursor: pointer;
            font-size: 0.85rem;
            transition: all 0.2s ease;
        }
        
        .layer-item:hover {
            background-color: #f5f5f5;
        }
        
        .layer-item.selected {
            background-color: rgba(67, 97, 238, 0.1);
            color: var(--primary);
            font-weight: 500;
        }
        
        .layer-item .visibility-toggle {
            margin-right: 10px;
            cursor: pointer;
            font-size: 1rem;
            color: #666;
        }
        
        .size-controls {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            margin-top: 12px;
        }
        
        .size-option {
            padding: 8px;
            border: 2px solid #eee;
            border-radius: var(--rounded);
            text-align: center;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        
        .size-option:hover {
            border-color: var(--primary-light);
        }
        
        .size-option.selected {
            border-color: var(--primary);
            background-color: rgba(67, 97, 238, 0.1);
        }
        
        .zoom-controls {
            position: absolute;
            bottom: 30px;
            right: 30px;
            display: flex;
            flex-direction: column;
            gap: 8px;
            z-index: 10;
        }
        
        .zoom-controls button {
            width: 42px;
            height: 42px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.1rem;
            padding: 0;
            margin: 0;
            box-shadow: var(--shadow);
        }
        
        .status-bar {
            padding: 10px 16px;
            background-color: var(--dark);
            color: white;
            font-size: 0.75rem;
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 10px;
        }
        
        .status-bar div {
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        
        .mobile-toolbar-toggle {
            display: none;
            position: fixed;
            bottom: 30px;
            left: 30px;
            z-index: 50;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: var(--gradient-primary);
            color: white;
            border: none;
            font-size: 1.5rem;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: var(--shadow-lg);
            transition: all 0.3s ease;
        }
        
        .mobile-toolbar-toggle:hover {
            transform: scale(1.1);
        }
        
        @media (max-width: 992px) {
            .mobile-toolbar-toggle {
                display: flex;
            }
            
            .main-content {
                height: calc(100vh - 110px);
            }
        }
        
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(0,0,0,0.7);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 200;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
        }
        
        .modal-overlay.active {
            opacity: 1;
            visibility: visible;
        }
        
        .modal-content {
            background-color: white;
            border-radius: var(--rounded-xl);
            width: 90%;
            max-width: 500px;
            max-height: 90vh;
            overflow-y: auto;
            transform: translateY(20px);
            transition: all 0.3s ease;
            box-shadow: var(--shadow-lg);
        }
        
        .modal-overlay.active .modal-content {
            transform: translateY(0);
        }
        
        .modal-header {
            padding: 20px;
            border-bottom: 1px solid #eee;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .modal-header h3 {
            font-size: 1.2rem;
            color: var(--secondary);
        }
        
        .close-modal {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #777;
            transition: all 0.2s ease;
        }
        
        .close-modal:hover {
            color: var(--danger);
            transform: rotate(90deg);
        }
        
        .modal-body {
            padding: 20px;
        }
        
        .modal-footer {
            padding: 20px;
            border-top: 1px solid #eee;
            display: flex;
            justify-content: flex-end;
            gap: 12px;
        }
        
        .export-options {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 16px;
            margin-top: 16px;
        }
        
        .export-option {
            border: 2px solid #eee;
            padding: 20px;
            border-radius: var(--rounded);
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
        }
        
        .export-option:hover {
            border-color: var(--primary);
            transform: translateY(-5px);
            box-shadow: var(--shadow);
        }
        
        .export-option h4 {
            margin-bottom: 12px;
            color: var(--secondary);
            font-size: 1rem;
        }
        
        .export-option p {
            font-size: 0.85rem;
            color: #666;
            margin-bottom: 12px;
        }
        
        .export-option .icon {
            font-size: 2.5rem;
            color: var(--primary);
            margin-bottom: 12px;
            display: inline-block;
        }
        
        .cmyk-controls {
            display: none;
            margin-top: 10px;
            padding: 10px;
            background: #f5f5f5;
            border-radius: var(--rounded);
        }
        
        .cmyk-slider {
            margin-bottom: 10px;
        }
        
        .cmyk-slider label {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 0.8rem;
        }
        
        .cmyk-slider input[type="range"] {
            width: 100%;
            margin-top: 5px;
        }
        
        .cmyk-preview {
            width: 100%;
            height: 30px;
            border-radius: var(--rounded);
            margin-top: 10px;
            border: 1px solid #ddd;
        }
        
        .color-mode-warning {
            display: none;
            padding: 10px;
            background-color: #fff3cd;
            color: #856404;
            border-radius: var(--rounded);
            margin-top: 10px;
            font-size: 0.8rem;
        }
        
        @media (max-width: 768px) {
            .app-container {
                min-height: 100vh;
                border-radius: 0;
            }
            
            .export-options {
                grid-template-columns: 1fr;
            }
            
            .zoom-controls {
                bottom: 20px;
                right: 20px;
            }
            
            .zoom-controls button {
                width: 36px;
                height: 36px;
                font-size: 1rem;
            }
            
            .mobile-toolbar-toggle {
                width: 42px;
                height: 42px;
                font-size: 1.3rem;
                bottom: 20px;
                left: 20px;
            }
        }
    </style>
</head>
<body>
    <!-- Login Screen -->
    <div class="login-container" id="login-container">
        <div class="login-box">
            <h2>Acceso al Diseñador</h2>
            <form class="login-form" id="login-form">
                <div class="form-group">
                    <label for="username">Usuario</label>
                    <input type="text" id="username" name="username" required>
                </div>
                <div class="form-group">
                    <label for="password">Contraseña</label>
                    <input type="password" id="password" name="password" required>
                </div>
                <button type="submit" class="login-btn">Ingresar</button>
                <div class="error-message" id="error-message">Credenciales incorrectas</div>
            </form>
        </div>
    </div>

    <!-- Main App Container (oculto inicialmente) -->
    <div class="app-container" id="main-app">
        <header class="app-header">
            <h1>Diseñador de Franelas (CMYK/RGB)</h1>
            <div class="header-actions">
                <button id="export-btn" class="btn-primary">
                    <i class="fas fa-download"></i> Exportar
                </button>
            </div>
        </header>
        
        <div class="main-content">
            <aside class="toolbar" id="main-toolbar">
                <div class="tool-section">
                    <h3>Plantilla de Franela</h3>
                    <div class="template-selector">
                        <div class="template-preview selected" data-template="classic">
                            <img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyMDAgMjAwIj48cmVjdCB3aWR0aD0iMjAwIiBoZWlnaHQ9IjIwMCIgZmlsbD0iI2VlZSIgc3Ryb2tlPSIjMDAwIi8+PHBhdGggZD0iTTUwIDUwSDE1MFYxNTBINTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMCIgc3Ryb2tlLXdpZHRoPSIyIi8+PC9zdmc+" alt="Clásica">
                        </div>
                        <div class="template-preview" data-template="sleeveless">
                            <img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyMDAgMjAwIj48cmVjdCB3aWR0aD0iMjAwIiBoZWlnaHQ9IjIwMCIgZmlsbD0iI2VlZSIgc3Ryb2tlPSIjMDAwIi8+PHBhdGggZD0iTTUwIDUwSDE1MFYxNTBINTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMCIgc3Ryb2tlLXdpZHRoPSIyIi8+PHBhdGggZD0iTTUwIDc1SDE1MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwIiBzdHJva2Utd2lkdGg9IjIiLz48L3N2Zz4=" alt="Sin mangas">
                        </div>
                        <div class="template-preview" data-template="vneck">
                            <img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyMDAgMjAwIj48cmVjdCB3aWR0aD0iMjAwIiBoZWlnaHQ9IjIwMCIgZmlsbD0iI2VlZSIgc3Ryb2tlPSIjMDAwIi8+PHBhdGggZD0iTTUwIDUwSDE1MFYxNTBINTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMCIgc3Ryb2tlLXdpZHRoPSIyIi8+PHBhdGggZD0iTTUwIDUwTDEwMCA3NSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwIiBzdHJva2Utd2lkdGg9IjIiLz48cGF0aCBkPSJNMTUwIDUwTDEwMCA3NSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwIiBzdHJva2Utd2lkdGg9IjIiLz48L3N2Zz4=" alt="Cuello V">
                        </div>
                        <div class="template-preview" data-template="hoodie">
                            <img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyMDAgMjAwIj48cmVjdCB3aWR0aD0iMjAwIiBoZWlnaHQ9IjIwMCIgZmlsbD0iI2VlZSIgc3Ryb2tlPSIjMDAwIi8+PHBhdGggZD0iTTUwIDUwSDE1MFYxNTBINTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMCIgc3Ryb2tlLXdpZHRoPSIyIi8+PHBhdGggZD0iTTUwIDUwQzUwIDMwIDc1IDIwIDEwMCAyMEMxMjUgMjAgMTUwIDMwIDE1MCA1MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwIiBzdHJva2Utd2lkdGg9IjIiLz48L3N2Zz4=" alt="Canguro">
                        </div>
                    </div>
                    
                    <button id="configure-size" class="btn-secondary" style="margin-top: 12px; width: 100%;">
                        <i class="fas fa-ruler"></i> Configurar Talla
                    </button>
                </div>
                
                <div class="tool-section">
                    <div class="tabs">
                        <div class="tab active" data-tab="elements">Elementos</div>
                        <div class="tab" data-tab="import">Importar</div>
                    </div>
                    
                    <div class="tab-content active" id="elements-tab">
                        <button id="add-text" class="btn-secondary">
                            <i class="fas fa-font"></i> Añadir Texto
                        </button>
                        <div class="property-group">
                            <label for="text-font">Fuente:</label>
                            <select id="text-font">
                                <option value="Arial">Arial</option>
                                <option value="Verdana">Verdana</option>
                                <option value="Helvetica">Helvetica</option>
                                <option value="Times New Roman">Times New Roman</option>
                                <option value="Courier New">Courier New</option>
                                <option value="Impact">Impact</option>
                                <option value="Comic Sans MS">Comic Sans</option>
                            </select>
                        </div>
                        <div class="property-group">
                            <label for="text-size">Tamaño (px):</label>
                            <input type="range" id="text-size" min="8" max="72" value="20">
                        </div>
                        <div class="property-group">
                            <label for="text-color">Color:</label>
                            <input type="color" id="text-color" value="#000000">
                        </div>
                        
                        <button id="add-rectangle" class="btn-secondary">
                            <i class="fas fa-square"></i> Rectángulo
                        </button>
                        <button id="add-circle" class="btn-secondary">
                            <i class="fas fa-circle"></i> Círculo
                        </button>
                        <button id="add-triangle" class="btn-secondary">
                            <i class="fas fa-play"></i> Triángulo
                        </button>
                    </div>
                    
                    <div class="tab-content" id="import-tab">
                        <input type="file" id="upload-svg" accept=".svg" style="display: none;">
                        <button id="import-svg" class="btn-secondary">
                            <i class="fas fa-file-import"></i> Importar SVG
                        </button>
                        <input type="file" id="upload-image" accept="image/*" style="display: none;">
                        <button id="import-image" class="btn-secondary">
                            <i class="fas fa-image"></i> Importar Imagen
                        </button>
                    </div>
                </div>
                
                <div class="tool-section">
                    <h3>Propiedades</h3>
                    <div class="property-group">
                        <label for="color-mode">Modo de Color:</label>
                        <select id="color-mode">
                            <option value="rgb">RGB (Pantalla)</option>
                            <option value="cmyk">CMYK (Impresión)</option>
                        </select>
                    </div>
                    
                    <div class="property-group">
                        <label for="fill-color">Color de Relleno:</label>
                        <input type="color" id="fill-color" value="#FF0000">
                        <div class="cmyk-controls" id="fill-cmyk-controls">
                            <div class="cmyk-slider">
                                <label>
                                    <span>Cian: <span id="fill-c-value">0%</span></span>
                                    <input type="range" id="fill-c-ink" min="0" max="100" value="0">
                                </label>
                            </div>
                            <div class="cmyk-slider">
                                <label>
                                    <span>Magenta: <span id="fill-m-value">100%</span></span>
                                    <input type="range" id="fill-m-ink" min="0" max="100" value="100">
                                </label>
                            </div>
                            <div class="cmyk-slider">
                                <label>
                                    <span>Amarillo: <span id="fill-y-value">100%</span></span>
                                    <input type="range" id="fill-y-ink" min="0" max="100" value="100">
                                </label>
                            </div>
                            <div class="cmyk-slider">
                                <label>
                                    <span>Negro: <span id="fill-k-value">0%</span></span>
                                    <input type="range" id="fill-k-ink" min="0" max="100" value="0">
                                </label>
                            </div>
                            <div class="cmyk-preview" id="fill-cmyk-preview" style="background-color: rgb(255, 0, 0);"></div>
                        </div>
                    </div>
                    
                    <div class="property-group">
                        <label for="stroke-color">Color de Borde:</label>
                        <input type="color" id="stroke-color" value="#000000">
                        <div class="cmyk-controls" id="stroke-cmyk-controls">
                            <div class="cmyk-slider">
                                <label>
                                    <span>Cian: <span id="stroke-c-value">0%</span></span>
                                    <input type="range" id="stroke-c-ink" min="0" max="100" value="0">
                                </label>
                            </div>
                            <div class="cmyk-slider">
                                <label>
                                    <span>Magenta: <span id="stroke-m-value">0%</span></span>
                                    <input type="range" id="stroke-m-ink" min="0" max="100" value="0">
                                </label>
                            </div>
                            <div class="cmyk-slider">
                                <label>
                                    <span>Amarillo: <span id="stroke-y-value">0%</span></span>
                                    <input type="range" id="stroke-y-ink" min="0" max="100" value="0">
                                </label>
                            </div>
                            <div class="cmyk-slider">
                                <label>
                                    <span>Negro: <span id="stroke-k-value">100%</span></span>
                                    <input type="range" id="stroke-k-ink" min="0" max="100" value="100">
                                </label>
                            </div>
                            <div class="cmyk-preview" id="stroke-cmyk-preview" style="background-color: rgb(0, 0, 0);"></div>
                        </div>
                    </div>
                    
                    <div class="property-group">
                        <label for="stroke-width">Grosor de Borde:</label>
                        <input type="range" id="stroke-width" min="0" max="10" value="1">
                    </div>
                    <div class="property-group">
                        <label for="opacity">Opacidad:</label>
                        <input type="range" id="opacity" min="10" max="100" value="100">
                    </div>
                    <div class="color-mode-warning" id="color-mode-warning">
                        <i class="fas fa-exclamation-triangle"></i> Los colores CMYK pueden verse diferente en pantalla. Para impresión profesional, exporta en PDF con perfil CMYK.
                    </div>
                    <button id="delete-object" class="btn-danger">
                        <i class="fas fa-trash"></i> Eliminar
                    </button>
                </div>
                
                <div class="tool-section">
                    <h3>Capas</h3>
                    <div class="layer-list" id="layer-list">
                        <!-- Las capas se generarán dinámicamente -->
                    </div>
                    <div class="history-controls">
                        <button id="bring-to-front" class="btn-secondary">
                            <i class="fas fa-arrow-up"></i>
                        </button>
                        <button id="send-to-back" class="btn-secondary">
                            <i class="fas fa-arrow-down"></i>
                        </button>
                    </div>
                </div>
            </aside>
            
            <main class="canvas-container">
                <canvas id="design-canvas" width="800" height="600"></canvas>
                <div class="zoom-controls">
                    <button id="zoom-in" class="btn-primary">+</button>
                    <button id="zoom-out" class="btn-primary">-</button>
                    <button id="reset-zoom" class="btn-primary">↻</button>
                </div>
                <button class="mobile-toolbar-toggle" id="toolbar-toggle">
                    <i class="fas fa-palette"></i>
                </button>
            </main>
        </div>
        
        <div class="status-bar">
            <div id="cursor-position">X: 0, Y: 0</div>
            <div id="zoom-level">Zoom: 100%</div>
            <div id="selected-object">Objeto seleccionado: Ninguno</div>
            <div id="current-size">Talla: M</div>
            <div id="color-mode-display">Modo: RGB</div>
        </div>
    </div>

    <!-- Modal de Exportación -->
    <div class="modal-overlay" id="export-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Exportar Diseño</h3>
                <button class="close-modal" id="close-modal">&times;</button>
            </div>
            <div class="modal-body">
                <p>Selecciona el formato en el que deseas exportar tu diseño:</p>
                <div class="export-options">
                    <div class="export-option" data-format="svg">
                        <div class="icon">🖼️</div>
                        <h4>SVG (Vectorial)</h4>
                        <p>Formato vectorial escalable sin pérdida de calidad. Ideal para impresión profesional.</p>
                        <button class="btn-secondary">Descargar</button>
                    </div>
                    <div class="export-option" data-format="png">
                        <div class="icon">📷</div>
                        <h4>PNG (Alta calidad)</h4>
                        <p>Imagen de alta calidad con fondo transparente. Perfecto para redes sociales.</p>
                        <button class="btn-secondary">Descargar</button>
                    </div>
                    <div class="export-option" data-format="jpeg">
                        <div class="icon">🏞️</div>
                        <h4>JPEG (Comprimido)</h4>
                        <p>Imagen comprimida con buena calidad. Ideal para compartir por email.</p>
                        <button class="btn-secondary">Descargar</button>
                    </div>
                    <div class="export-option" data-format="pdf">
                        <div class="icon">📄</div>
                        <h4>PDF (Documento)</h4>
                        <p>Documento PDF listo para imprimir con especificaciones técnicas.</p>
                        <button class="btn-secondary">Descargar</button>
                    </div>
                    <div class="export-option" data-format="pdf-cmyk">
                        <div class="icon">🖨️</div>
                        <h4>PDF CMYK (Impresión)</h4>
                        <p>PDF optimizado para impresión profesional con colores CMYK.</p>
                        <button class="btn-secondary">Descargar</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal de Configuración de Tallas -->
    <div class="modal-overlay" id="size-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Configurar Tallas</h3>
                <button class="close-modal" id="close-size-modal">&times;</button>
            </div>
            <div class="modal-body">
                <div class="tool-section">
                    <h3>Talla Base</h3>
                    <div class="size-controls">
                        <div class="size-option selected" data-size="S">S</div>
                        <div class="size-option" data-size="M">M</div>
                        <div class="size-option" data-size="L">L</div>
                        <div class="size-option" data-size="XL">XL</div>
                        <div class="size-option" data-size="XXL">XXL</div>
                        <div class="size-option" data-size="custom">Personalizada</div>
                    </div>
                </div>
                
                <div class="tool-section" id="custom-size-section" style="display: none;">
                    <h3>Medidas Personalizadas (cm)</h3>
                    <div class="property-group">
                        <label for="custom-width">Ancho:</label>
                        <input type="range" id="custom-width" min="40" max="70" value="50">
                        <span id="width-value">50 cm</span>
                    </div>
                    <div class="property-group">
                        <label for="custom-height">Largo:</label>
                        <input type="range" id="custom-height" min="60" max="90" value="70">
                        <span id="height-value">70 cm</span>
                    </div>
                    <div class="property-group">
                        <label for="custom-sleeve">Largo de Manga:</label>
                        <input type="range" id="custom-sleeve" min="15" max="40" value="25">
                        <span id="sleeve-value">25 cm</span>
                    </div>
                </div>
            </div>
            <div class="modal-footer">
                <button id="apply-size-btn" class="btn-primary">Aplicar Talla</button>
            </div>
        </div>
    </div>

    <script>
        // Credenciales válidas
        const VALID_USERNAME = "i 3945aodo434k";
        const VALID_PASSWORD = "r34'''''''''''";
        
        // Esperar a que el DOM esté cargado
        document.addEventListener('DOMContentLoaded', function() {
            const loginForm = document.getElementById('login-form');
            const loginContainer = document.getElementById('login-container');
            const mainApp = document.getElementById('main-app');
            const errorMessage = document.getElementById('error-message');
            
            // Manejar el envío del formulario de login
            loginForm.addEventListener('submit', function(e) {
                e.preventDefault();
                
                const username = document.getElementById('username').value;
                const password = document.getElementById('password').value;
                
                if (username === VALID_USERNAME && password === VALID_PASSWORD) {
                    // Credenciales correctas, mostrar la aplicación
                    loginContainer.style.display = 'none';
                    mainApp.style.display = 'flex';
                    
                    // Inicializar la aplicación después del login
                    initDesignerApp();
                } else {
                    // Mostrar mensaje de error
                    errorMessage.style.display = 'block';
                }
            });
            
            // Función para inicializar la aplicación de diseño
            function initDesignerApp() {
                // Inicializar el canvas de Fabric.js
                const canvas = new fabric.Canvas('design-canvas', {
                    backgroundColor: '#ffffff',
                    preserveObjectStacking: true,
                    selection: true
                });
                
                // Variables de estado
                let zoomLevel = 1;
                let history = [];
                let historyIndex = -1;
                let currentTemplate = 'classic';
                let currentSize = 'M';
                let colorMode = 'rgb'; // 'rgb' o 'cmyk'
                
                // Tamaños predefinidos (ancho, alto, manga)
                const sizePresets = {
                    'S': { width: 45, height: 65, sleeve: 20 },
                    'M': { width: 50, height: 70, sleeve: 25 },
                    'L': { width: 55, height: 75, sleeve: 30 },
                    'XL': { width: 60, height: 80, sleeve: 35 },
                    'XXL': { width: 65, height: 85, sleeve: 40 }
                };
                
                // Elementos de la interfaz
                const elements = {
                    // Botones
                    addTextBtn: document.getElementById('add-text'),
                    addRectBtn: document.getElementById('add-rectangle'),
                    addCircleBtn: document.getElementById('add-circle'),
                    addTriangleBtn: document.getElementById('add-triangle'),
                    importSvgBtn: document.getElementById('import-svg'),
                    importImageBtn: document.getElementById('import-image'),
                    uploadSvgInput: document.getElementById('upload-svg'),
                    uploadImageInput: document.getElementById('upload-image'),
                    deleteObjBtn: document.getElementById('delete-object'),
                    exportBtn: document.getElementById('export-btn'),
                    zoomInBtn: document.getElementById('zoom-in'),
                    zoomOutBtn: document.getElementById('zoom-out'),
                    resetZoomBtn: document.getElementById('reset-zoom'),
                    bringToFrontBtn: document.getElementById('bring-to-front'),
                    sendToBackBtn: document.getElementById('send-to-back'),
                    toolbarToggle: document.getElementById('toolbar-toggle'),
                    configureSizeBtn: document.getElementById('configure-size'),
                    
                    // Selectores
                    colorModeSelect: document.getElementById('color-mode'),
                    fillColorInput: document.getElementById('fill-color'),
                    strokeColorInput: document.getElementById('stroke-color'),
                    strokeWidthInput: document.getElementById('stroke-width'),
                    opacityInput: document.getElementById('opacity'),
                    textFontSelect: document.getElementById('text-font'),
                    textSizeInput: document.getElementById('text-size'),
                    textColorInput: document.getElementById('text-color'),
                    
                    // Controles CMYK
                    fillCmykControls: document.getElementById('fill-cmyk-controls'),
                    strokeCmykControls: document.getElementById('stroke-cmyk-controls'),
                    fillCInk: document.getElementById('fill-c-ink'),
                    fillMInk: document.getElementById('fill-m-ink'),
                    fillYInk: document.getElementById('fill-y-ink'),
                    fillKInk: document.getElementById('fill-k-ink'),
                    fillCValue: document.getElementById('fill-c-value'),
                    fillMValue: document.getElementById('fill-m-value'),
                    fillYValue: document.getElementById('fill-y-value'),
                    fillKValue: document.getElementById('fill-k-value'),
                    fillCmykPreview: document.getElementById('fill-cmyk-preview'),
                    strokeCInk: document.getElementById('stroke-c-ink'),
                    strokeMInk: document.getElementById('stroke-m-ink'),
                    strokeYInk: document.getElementById('stroke-y-ink'),
                    strokeKInk: document.getElementById('stroke-k-ink'),
                    strokeCValue: document.getElementById('stroke-c-value'),
                    strokeMValue: document.getElementById('stroke-m-value'),
                    strokeYValue: document.getElementById('stroke-y-value'),
                    strokeKValue: document.getElementById('stroke-k-value'),
                    strokeCmykPreview: document.getElementById('stroke-cmyk-preview'),
                    colorModeWarning: document.getElementById('color-mode-warning'),
                    
                    // Tabs
                    tabs: document.querySelectorAll('.tab'),
                    tabContents: document.querySelectorAll('.tab-content'),
                    
                    // Capas
                    layerList: document.getElementById('layer-list'),
                    
                    // Modals
                    exportModal: document.getElementById('export-modal'),
                    closeModalBtn: document.getElementById('close-modal'),
                    exportOptions: document.querySelectorAll('.export-option'),
                    sizeModal: document.getElementById('size-modal'),
                    closeSizeModalBtn: document.getElementById('close-size-modal'),
                    applySizeBtn: document.getElementById('apply-size-btn'),
                    customWidthInput: document.getElementById('custom-width'),
                    customHeightInput: document.getElementById('custom-height'),
                    customSleeveInput: document.getElementById('custom-sleeve'),
                    widthValue: document.getElementById('width-value'),
                    heightValue: document.getElementById('height-value'),
                    sleeveValue: document.getElementById('sleeve-value'),
                    customSizeSection: document.getElementById('custom-size-section'),
                    sizeOptions: document.querySelectorAll('.size-option'),
                    
                    // Status bar
                    cursorPosition: document.getElementById('cursor-position'),
                    zoomLevel: document.getElementById('zoom-level'),
                    selectedObject: document.getElementById('selected-object'),
                    currentSize: document.getElementById('current-size'),
                    colorModeDisplay: document.getElementById('color-mode-display')
                };
                
                // Plantillas de franelas
                const templatePreviews = document.querySelectorAll('.template-preview');
                
                // Configurar eventos
                setupEventListeners();
                
                // Cargar plantilla inicial
                loadTemplate(currentTemplate);
                
                // Actualizar UI inicial
                updateUIForSelection();
                updateZoomDisplay();
                
                // Funciones de conversión de color
                function rgbToCmyk(r, g, b) {
                    // Normalizar valores RGB
                    r = r / 255;
                    g = g / 255;
                    b = b / 255;
                    
                    // Calcular K (negro)
                    const k = 1 - Math.max(r, g, b);
                    
                    // Calcular CMY
                    let c = (1 - r - k) / (1 - k);
                    let m = (1 - g - k) / (1 - k);
                    let y = (1 - b - k) / (1 - k);
                    
                    // Asegurar que no sea NaN (cuando K es 1)
                    c = isNaN(c) ? 0 : c;
                    m = isNaN(m) ? 0 : m;
                    y = isNaN(y) ? 0 : y;
                    
                    // Convertir a porcentajes
                    return {
                        c: Math.round(c * 100),
                        m: Math.round(m * 100),
                        y: Math.round(y * 100),
                        k: Math.round(k * 100)
                    };
                }
                
                function cmykToRgb(c, m, y, k) {
                    // Convertir de porcentajes a decimales
                    c = c / 100;
                    m = m / 100;
                    y = y / 100;
                    k = k / 100;
                    
                    // Calcular RGB
                    const r = 255 * (1 - c) * (1 - k);
                    const g = 255 * (1 - m) * (1 - k);
                    const b = 255 * (1 - y) * (1 - k);
                    
                    return {
                        r: Math.round(r),
                        g: Math.round(g),
                        b: Math.round(b)
                    };
                }
                
                function hexToRgb(hex) {
                    // Eliminar el # si está presente
                    hex = hex.replace('#', '');
                    
                    // Convertir a valores RGB
                    const r = parseInt(hex.substring(0, 2), 16);
                    const g = parseInt(hex.substring(2, 4), 16);
                    const b = parseInt(hex.substring(4, 6), 16);
                    
                    return { r, g, b };
                }
                
                function rgbToHex(r, g, b) {
                    return '#' + [r, g, b].map(x => {
                        const hex = x.toString(16);
                        return hex.length === 1 ? '0' + hex : hex;
                    }).join('');
                }
                
                function updateCmykFromRgb(colorInput, cmykControls) {
                    const hexColor = colorInput.value;
                    const rgb = hexToRgb(hexColor);
                    const cmyk = rgbToCmyk(rgb.r, rgb.g, rgb.b);
                    
                    if (cmykControls === 'fill') {
                        elements.fillCInk.value = cmyk.c;
                        elements.fillMInk.value = cmyk.m;
                        elements.fillYInk.value = cmyk.y;
                        elements.fillKInk.value = cmyk.k;
                        
                        elements.fillCValue.textContent = `${cmyk.c}%`;
                        elements.fillMValue.textContent = `${cmyk.m}%`;
                        elements.fillYValue.textContent = `${cmyk.y}%`;
                        elements.fillKValue.textContent = `${cmyk.k}%`;
                    } else if (cmykControls === 'stroke') {
                        elements.strokeCInk.value = cmyk.c;
                        elements.strokeMInk.value = cmyk.m;
                        elements.strokeYInk.value = cmyk.y;
                        elements.strokeKInk.value = cmyk.k;
                        
                        elements.strokeCValue.textContent = `${cmyk.c}%`;
                        elements.strokeMValue.textContent = `${cmyk.m}%`;
                        elements.strokeYValue.textContent = `${cmyk.y}%`;
                        elements.strokeKValue.textContent = `${cmyk.k}%`;
                    }
                }
                
                function updateRgbFromCmyk(c, m, y, k, colorInput, previewElement) {
                    const rgb = cmykToRgb(c, m, y, k);
                    const hexColor = rgbToHex(rgb.r, rgb.g, rgb.b);
                    
                    colorInput.value = hexColor;
                    previewElement.style.backgroundColor = hexColor;
                    
                    return hexColor;
                }
                
                function setupEventListeners() {
                    // Eventos para añadir elementos
                    elements.addTextBtn.addEventListener('click', addText);
                    elements.addRectBtn.addEventListener('click', addRectangle);
                    elements.addCircleBtn.addEventListener('click', addCircle);
                    elements.addTriangleBtn.addEventListener('click', addTriangle);
                    
                    // Eventos para importar
                    elements.importSvgBtn.addEventListener('click', () => elements.uploadSvgInput.click());
                    elements.importImageBtn.addEventListener('click', () => elements.uploadImageInput.click());
                    elements.uploadSvgInput.addEventListener('change', importSVG);
                    elements.uploadImageInput.addEventListener('change', importImage);
                    
                    // Eventos para modo de color
                    elements.colorModeSelect.addEventListener('change', function() {
                        colorMode = this.value;
                        elements.colorModeDisplay.textContent = `Modo: ${colorMode.toUpperCase()}`;
                        
                        if (colorMode === 'cmyk') {
                            elements.fillCmykControls.style.display = 'block';
                            elements.strokeCmykControls.style.display = 'block';
                            elements.colorModeWarning.style.display = 'block';
                            
                            // Actualizar controles CMYK basados en los valores RGB actuales
                            updateCmykFromRgb(elements.fillColorInput, 'fill');
                            updateCmykFromRgb(elements.strokeColorInput, 'stroke');
                        } else {
                            elements.fillCmykControls.style.display = 'none';
                            elements.strokeCmykControls.style.display = 'none';
                            elements.colorModeWarning.style.display = 'none';
                        }
                        
                        updateUIForSelection();
                    });
                    
                    // Eventos para controles CMYK de relleno
                    elements.fillCInk.addEventListener('input', function() {
                        elements.fillCValue.textContent = `${this.value}%`;
                        const hexColor = updateRgbFromCmyk(
                            parseInt(elements.fillCInk.value),
                            parseInt(elements.fillMInk.value),
                            parseInt(elements.fillYInk.value),
                            parseInt(elements.fillKInk.value),
                            elements.fillColorInput,
                            elements.fillCmykPreview
                        );
                        updateObjectProperty('fill', hexColor);
                    });
                    
                    elements.fillMInk.addEventListener('input', function() {
                        elements.fillMValue.textContent = `${this.value}%`;
                        const hexColor = updateRgbFromCmyk(
                            parseInt(elements.fillCInk.value),
                            parseInt(elements.fillMInk.value),
                            parseInt(elements.fillYInk.value),
                            parseInt(elements.fillKInk.value),
                            elements.fillColorInput,
                            elements.fillCmykPreview
                        );
                        updateObjectProperty('fill', hexColor);
                    });
                    
                    elements.fillYInk.addEventListener('input', function() {
                        elements.fillYValue.textContent = `${this.value}%`;
                        const hexColor = updateRgbFromCmyk(
                            parseInt(elements.fillCInk.value),
                            parseInt(elements.fillMInk.value),
                            parseInt(elements.fillYInk.value),
                            parseInt(elements.fillKInk.value),
                            elements.fillColorInput,
                            elements.fillCmykPreview
                        );
                        updateObjectProperty('fill', hexColor);
                    });
                    
                    elements.fillKInk.addEventListener('input', function() {
                        elements.fillKValue.textContent = `${this.value}%`;
                        const hexColor = updateRgbFromCmyk(
                            parseInt(elements.fillCInk.value),
                            parseInt(elements.fillMInk.value),
                            parseInt(elements.fillYInk.value),
                            parseInt(elements.fillKInk.value),
                            elements.fillColorInput,
                            elements.fillCmykPreview
                        );
                        updateObjectProperty('fill', hexColor);
                    });
                    
                    // Eventos para controles CMYK de borde
                    elements.strokeCInk.addEventListener('input', function() {
                        elements.strokeCValue.textContent = `${this.value}%`;
                        const hexColor = updateRgbFromCmyk(
                            parseInt(elements.strokeCInk.value),
                            parseInt(elements.strokeMInk.value),
                            parseInt(elements.strokeYInk.value),
                            parseInt(elements.strokeKInk.value),
                            elements.strokeColorInput,
                            elements.strokeCmykPreview
                        );
                        updateObjectProperty('stroke', hexColor);
                    });
                    
                    elements.strokeMInk.addEventListener('input', function() {
                        elements.strokeMValue.textContent = `${this.value}%`;
                        const hexColor = updateRgbFromCmyk(
                            parseInt(elements.strokeCInk.value),
                            parseInt(elements.strokeMInk.value),
                            parseInt(elements.strokeYInk.value),
                            parseInt(elements.strokeKInk.value),
                            elements.strokeColorInput,
                            elements.strokeCmykPreview
                        );
                        updateObjectProperty('stroke', hexColor);
                    });
                    
                    elements.strokeYInk.addEventListener('input', function() {
                        elements.strokeYValue.textContent = `${this.value}%`;
                        const hexColor = updateRgbFromCmyk(
                            parseInt(elements.strokeCInk.value),
                            parseInt(elements.strokeMInk.value),
                            parseInt(elements.strokeYInk.value),
                            parseInt(elements.strokeKInk.value),
                            elements.strokeColorInput,
                            elements.strokeCmykPreview
                        );
                        updateObjectProperty('stroke', hexColor);
                    });
                    
                    elements.strokeKInk.addEventListener('input', function() {
                        elements.strokeKValue.textContent = `${this.value}%`;
                        const hexColor = updateRgbFromCmyk(
                            parseInt(elements.strokeCInk.value),
                            parseInt(elements.strokeMInk.value),
                            parseInt(elements.strokeYInk.value),
                            parseInt(elements.strokeKInk.value),
                            elements.strokeColorInput,
                            elements.strokeCmykPreview
                        );
                        updateObjectProperty('stroke', hexColor);
                    });
                    
                    // Eventos para propiedades
                    elements.fillColorInput.addEventListener('change', function() {
                        if (colorMode === 'cmyk') {
                            updateCmykFromRgb(this, 'fill');
                        }
                        updateObjectProperty('fill', this.value);
                    });
                    
                    elements.strokeColorInput.addEventListener('change', function() {
                        if (colorMode === 'cmyk') {
                            updateCmykFromRgb(this, 'stroke');
                        }
                        updateObjectProperty('stroke', this.value);
                    });
                    
                    elements.strokeWidthInput.addEventListener('input', function() {
                        updateObjectProperty('strokeWidth', parseInt(this.value));
                    });
                    
                    elements.opacityInput.addEventListener('input', function() {
                        updateObjectProperty('opacity', parseInt(this.value) / 100);
                    });
                    
                    elements.textFontSelect.addEventListener('change', function() {
                        updateObjectProperty('fontFamily', this.value);
                    });
                    
                    elements.textSizeInput.addEventListener('input', function() {
                        updateObjectProperty('fontSize', parseInt(this.value));
                    });
                    
                    elements.textColorInput.addEventListener('change', function() {
                        updateObjectProperty('fill', this.value);
                    });
                    
                    // Eventos para manipulación de objetos
                    elements.deleteObjBtn.addEventListener('click', deleteSelectedObject);
                    elements.bringToFrontBtn.addEventListener('click', bringToFront);
                    elements.sendToBackBtn.addEventListener('click', sendToBack);
                    
                    // Eventos para zoom
                    elements.zoomInBtn.addEventListener('click', zoomIn);
                    elements.zoomOutBtn.addEventListener('click', zoomOut);
                    elements.resetZoomBtn.addEventListener('click', resetZoom);
                    
                    // Eventos para exportación
                    elements.exportBtn.addEventListener('click', showExportModal);
                    elements.closeModalBtn.addEventListener('click', hideExportModal);
                    
                    // Eventos para tabs
                    elements.tabs.forEach(tab => {
                        tab.addEventListener('click', switchTab);
                    });
                    
                    // Eventos para plantillas
                    templatePreviews.forEach(preview => {
                        preview.addEventListener('click', changeTemplate);
                    });
                    
                    // Eventos para exportación
                    elements.exportOptions.forEach(option => {
                        option.addEventListener('click', exportDesign);
                    });
                    
                    // Eventos para móviles
                    elements.toolbarToggle.addEventListener('click', toggleToolbar);
                    
                    // Eventos para configuración de tallas
                    elements.configureSizeBtn.addEventListener('click', showSizeModal);
                    elements.closeSizeModalBtn.addEventListener('click', hideSizeModal);
                    elements.applySizeBtn.addEventListener('click', applySize);
                    elements.sizeOptions.forEach(option => {
                        option.addEventListener('click', selectSizeOption);
                    });
                    elements.customWidthInput.addEventListener('input', updateCustomSizeDisplay);
                    elements.customHeightInput.addEventListener('input', updateCustomSizeDisplay);
                    elements.customSleeveInput.addEventListener('input', updateCustomSizeDisplay);
                    
                    // Eventos del canvas
                    canvas.on('object:added', handleObjectAdded);
                    canvas.on('object:modified', handleObjectModified);
                    canvas.on('object:removed', handleObjectRemoved);
                    canvas.on('selection:created', updateUIForSelection);
                    canvas.on('selection:updated', updateUIForSelection);
                    canvas.on('selection:cleared', updateUIForSelection);
                    canvas.on('mouse:move', updateCursorPosition);
                    
                    // Cerrar modales al hacer clic fuera
                    window.addEventListener('click', (e) => {
                        if (e.target === elements.exportModal) hideExportModal();
                        if (e.target === elements.sizeModal) hideSizeModal();
                    });
                }
                
                function updateObjectProperty(property, value) {
                    const activeObject = canvas.getActiveObject();
                    if (activeObject && activeObject.set) {
                        activeObject.set(property, value);
                        canvas.renderAll();
                        saveState();
                    }
                }
                
                // Funciones para añadir elementos
                function addText() {
                    const textColor = colorMode === 'cmyk' ? 
                        updateRgbFromCmyk(
                            parseInt(elements.fillCInk.value),
                            parseInt(elements.fillMInk.value),
                            parseInt(elements.fillYInk.value),
                            parseInt(elements.fillKInk.value),
                            elements.textColorInput,
                            null
                        ) : 
                        elements.textColorInput.value;
                    
                    const text = new fabric.IText('Edita este texto', {
                        left: canvas.width / 2 / zoomLevel,
                        top: canvas.height / 2 / zoomLevel,
                        fontFamily: elements.textFontSelect.value,
                        fontSize: parseInt(elements.textSizeInput.value),
                        fill: textColor,
                        stroke: elements.strokeColorInput.value,
                        strokeWidth: parseInt(elements.strokeWidthInput.value),
                        opacity: parseInt(elements.opacityInput.value) / 100,
                        originX: 'center',
                        originY: 'center',
                        editable: true,
                        selectable: true
                    });
                    
                    canvas.add(text);
                    canvas.setActiveObject(text);
                    text.enterEditing();
                    text.selectAll();
                    canvas.renderAll();
                    saveState();
                }
                
                function addRectangle() {
                    const fillColor = colorMode === 'cmyk' ? 
                        updateRgbFromCmyk(
                            parseInt(elements.fillCInk.value),
                            parseInt(elements.fillMInk.value),
                            parseInt(elements.fillYInk.value),
                            parseInt(elements.fillKInk.value),
                            elements.fillColorInput,
                            null
                        ) : 
                        elements.fillColorInput.value;
                    
                    const rect = new fabric.Rect({
                        left: canvas.width / 2 / zoomLevel,
                        top: canvas.height / 2 / zoomLevel,
                        width: 100,
                        height: 60,
                        fill: fillColor,
                        stroke: elements.strokeColorInput.value,
                        strokeWidth: parseInt(elements.strokeWidthInput.value),
                        opacity: parseInt(elements.opacityInput.value) / 100,
                        originX: 'center',
                        originY: 'center',
                        selectable: true
                    });
                    
                    canvas.add(rect);
                    canvas.setActiveObject(rect);
                    canvas.renderAll();
                    saveState();
                }
                
                function addCircle() {
                    const fillColor = colorMode === 'cmyk' ? 
                        updateRgbFromCmyk(
                            parseInt(elements.fillCInk.value),
                            parseInt(elements.fillMInk.value),
                            parseInt(elements.fillYInk.value),
                            parseInt(elements.fillKInk.value),
                            elements.fillColorInput,
                            null
                        ) : 
                        elements.fillColorInput.value;
                    
                    const circle = new fabric.Circle({
                        left: canvas.width / 2 / zoomLevel,
                        top: canvas.height / 2 / zoomLevel,
                        radius: 50,
                        fill: fillColor,
                        stroke: elements.strokeColorInput.value,
                        strokeWidth: parseInt(elements.strokeWidthInput.value),
                        opacity: parseInt(elements.opacityInput.value) / 100,
                        originX: 'center',
                        originY: 'center',
                        selectable: true
                    });
                    
                    canvas.add(circle);
                    canvas.setActiveObject(circle);
                    canvas.renderAll();
                    saveState();
                }
                
                function addTriangle() {
                    const fillColor = colorMode === 'cmyk' ? 
                        updateRgbFromCmyk(
                            parseInt(elements.fillCInk.value),
                            parseInt(elements.fillMInk.value),
                            parseInt(elements.fillYInk.value),
                            parseInt(elements.fillKInk.value),
                            elements.fillColorInput,
                            null
                        ) : 
                        elements.fillColorInput.value;
                    
                    const triangle = new fabric.Triangle({
                        left: canvas.width / 2 / zoomLevel,
                        top: canvas.height / 2 / zoomLevel,
                        width: 100,
                        height: 100,
                        fill: fillColor,
                        stroke: elements.strokeColorInput.value,
                        strokeWidth: parseInt(elements.strokeWidthInput.value),
                        opacity: parseInt(elements.opacityInput.value) / 100,
                        originX: 'center',
                        originY: 'center',
                        selectable: true
                    });
                    
                    canvas.add(triangle);
                    canvas.setActiveObject(triangle);
                    canvas.renderAll();
                    saveState();
                }
                
                function importSVG(e) {
                    const file = e.target.files[0];
                    if (!file) return;
                    
                    const reader = new FileReader();
                    reader.onload = function(event) {
                        fabric.loadSVGFromString(event.target.result, function(objects, options) {
                            const svgObject = fabric.util.groupSVGElements(objects, options);
                            
                            const scale = Math.min(
                                (canvas.width * 0.7) / (svgObject.width * zoomLevel),
                                (canvas.height * 0.7) / (svgObject.height * zoomLevel)
                            );
                            
                            svgObject.scale(scale);
                            svgObject.set({
                                left: canvas.width / 2 / zoomLevel,
                                top: canvas.height / 2 / zoomLevel,
                                originX: 'center',
                                originY: 'center',
                                selectable: true,
                                opacity: parseInt(elements.opacityInput.value) / 100
                            });
                            
                            canvas.add(svgObject);
                            canvas.setActiveObject(svgObject);
                            canvas.renderAll();
                            saveState();
                        });
                    };
                    reader.readAsText(file);
                    e.target.value = '';
                }
                
                function importImage(e) {
                    const file = e.target.files[0];
                    if (!file) return;
                    
                    const reader = new FileReader();
                    reader.onload = function(event) {
                        fabric.Image.fromURL(event.target.result, function(img) {
                            const scale = Math.min(
                                (canvas.width * 0.7) / (img.width * zoomLevel),
                                (canvas.height * 0.7) / (img.height * zoomLevel)
                            );
                            
                            img.scale(scale);
                            img.set({
                                left: canvas.width / 2 / zoomLevel,
                                top: canvas.height / 2 / zoomLevel,
                                originX: 'center',
                                originY: 'center',
                                selectable: true,
                                opacity: parseInt(elements.opacityInput.value) / 100
                            });
                            
                            canvas.add(img);
                            canvas.setActiveObject(img);
                            canvas.renderAll();
                            saveState();
                        });
                    };
                    reader.readAsDataURL(file);
                    e.target.value = '';
                }
                
                function deleteSelectedObject() {
                    const activeObject = canvas.getActiveObject();
                    if (activeObject) {
                        canvas.remove(activeObject);
                        canvas.renderAll();
                        saveState();
                    }
                }
                
                function bringToFront() {
                    const activeObject = canvas.getActiveObject();
                    if (activeObject) {
                        activeObject.bringToFront();
                        canvas.renderAll();
                        saveState();
                    }
                }
                
                function sendToBack() {
                    const activeObject = canvas.getActiveObject();
                    if (activeObject) {
                        activeObject.sendToBack();
                        canvas.renderAll();
                        saveState();
                    }
                }
                
                function zoomIn() {
                    if (zoomLevel < 3) {
                        zoomLevel += 0.1;
                        applyZoom();
                    }
                }
                
                function zoomOut() {
                    if (zoomLevel > 0.5) {
                        zoomLevel -= 0.1;
                        applyZoom();
                    }
                }
                
                function resetZoom() {
                    zoomLevel = 1;
                    applyZoom();
                }
                
                function applyZoom() {
                    canvas.setZoom(zoomLevel);
                    updateZoomDisplay();
                }
                
                function updateZoomDisplay() {
                    elements.zoomLevel.textContent = `Zoom: ${Math.round(zoomLevel * 100)}%`;
                }
                
                function changeTemplate() {
                    templatePreviews.forEach(preview => preview.classList.remove('selected'));
                    this.classList.add('selected');
                    currentTemplate = this.dataset.template;
                    loadTemplate(currentTemplate);
                    saveState();
                }
                
                function loadTemplate(template) {
                    const objects = canvas.getObjects();
                    objects.forEach(obj => {
                        if (!obj.isTemplate) {
                            canvas.remove(obj);
                        }
                    });
                    
                    const existingTemplate = canvas.getObjects().find(obj => obj.isTemplate && obj.templateType === template);
                    
                    if (!existingTemplate) {
                        let templateObj;
                        
                        const size = currentSize === 'custom' ? 
                            {
                                width: parseInt(elements.customWidthInput.value),
                                height: parseInt(elements.customHeightInput.value),
                                sleeve: parseInt(elements.customSleeveInput.value)
                            } : 
                            sizePresets[currentSize];
                        
                        switch(template) {
                            case 'classic':
                                templateObj = new fabric.Group([
                                    new fabric.Rect({
                                        width: size.width,
                                        height: size.height,
                                        fill: '#ffffff',
                                        stroke: '#cccccc',
                                        strokeWidth: 2,
                                        selectable: false,
                                        evented: false
                                    }),
                                    new fabric.Rect({
                                        width: size.sleeve,
                                        height: size.height * 0.7,
                                        fill: '#ffffff',
                                        stroke: '#cccccc',
                                        strokeWidth: 2,
                                        selectable: false,
                                        evented: false,
                                        left: -size.sleeve,
                                        top: size.height * 0.15
                                    }),
                                    new fabric.Rect({
                                        width: size.sleeve,
                                        height: size.height * 0.7,
                                        fill: '#ffffff',
                                        stroke: '#cccccc',
                                        strokeWidth: 2,
                                        selectable: false,
                                        evented: false,
                                        left: size.width,
                                        top: size.height * 0.15
                                    })
                                ], {
                                    isTemplate: true,
                                    templateType: template
                                });
                                break;
                            case 'sleeveless':
                                templateObj = new fabric.Group([
                                    new fabric.Rect({
                                        width: size.width,
                                        height: size.height,
                                        fill: '#ffffff',
                                        stroke: '#cccccc',
                                        strokeWidth: 2,
                                        selectable: false,
                                        evented: false
                                    }),
                                    new fabric.Rect({
                                        width: size.width * 0.8,
                                        height: size.height * 0.8,
                                        fill: '#ffffff',
                                        stroke: '#cccccc',
                                        strokeWidth: 2,
                                        selectable: false,
                                        evented: false,
                                        top: size.height * 0.1,
                                        left: size.width * 0.1
                                    })
                                ], {
                                    isTemplate: true,
                                    templateType: template
                                });
                                break;
                            case 'vneck':
                                templateObj = new fabric.Path(
                                    `M 0 0 
                                     L ${size.width} 0 
                                     L ${size.width} ${size.height} 
                                     L 0 ${size.height} 
                                     Z 
                                     M 0 0 
                                     L ${size.width/2} ${size.height*0.1} 
                                     L ${size.width} 0`, 
                                    {
                                        fill: '#ffffff',
                                        stroke: '#cccccc',
                                        strokeWidth: 2,
                                        selectable: false,
                                        evented: false,
                                        isTemplate: true,
                                        templateType: template
                                    }
                                );
                                break;
                            case 'hoodie':
                                templateObj = new fabric.Group([
                                    new fabric.Rect({
                                        width: size.width,
                                        height: size.height,
                                        fill: '#ffffff',
                                        stroke: '#cccccc',
                                        strokeWidth: 2,
                                        selectable: false,
                                        evented: false
                                    }),
                                    new fabric.Path(
                                        `M 0 0 
                                         Q ${size.width/2} -${size.height*0.2} ${size.width} 0`, 
                                        {
                                            fill: '#ffffff',
                                            stroke: '#cccccc',
                                            strokeWidth: 2,
                                            selectable: false,
                                            evented: false
                                        }
                                    ),
                                    new fabric.Rect({
                                        width: size.width * 0.4,
                                        height: size.height * 0.15,
                                        fill: '#ffffff',
                                        stroke: '#cccccc',
                                        strokeWidth: 2,
                                        selectable: false,
                                        evented: false,
                                        left: size.width * 0.3,
                                        top: size.height * 0.6
                                    })
                                ], {
                                    isTemplate: true,
                                    templateType: template
                                });
                                break;
                        }
                        
                        if (templateObj) {
                            templateObj.set({
                                left: canvas.width / 2 / zoomLevel,
                                top: canvas.height / 2 / zoomLevel,
                                originX: 'center',
                                originY: 'center'
                            });
                            canvas.add(templateObj);
                            canvas.sendToBack(templateObj);
                        }
                    }
                    
                    canvas.renderAll();
                    elements.currentSize.textContent = `Talla: ${currentSize}`;
                }
                
                function switchTab() {
                    const tabId = this.dataset.tab;
                    
                    elements.tabs.forEach(tab => tab.classList.remove('active'));
                    this.classList.add('active');
                    
                    elements.tabContents.forEach(content => {
                        content.classList.remove('active');
                        if (content.id === `${tabId}-tab`) {
                            content.classList.add('active');
                        }
                    });
                }
                
                function updateLayers() {
                    elements.layerList.innerHTML = '';
                    const objects = canvas.getObjects().filter(obj => !obj.isTemplate);
                    
                    objects.reverse().forEach((obj, index) => {
                        const layerItem = document.createElement('div');
                        layerItem.className = 'layer-item';
                        if (obj === canvas.getActiveObject()) {
                            layerItem.classList.add('selected');
                        }
                        
                        layerItem.innerHTML = `
                            <span class="visibility-toggle">${obj.visible ? '👁️' : '🚫'}</span>
                            ${obj.type || 'objeto'} ${index + 1}
                        `;
                        
                        layerItem.addEventListener('click', () => {
                            canvas.setActiveObject(obj);
                            canvas.renderAll();
                        });
                        
                        const visibilityToggle = layerItem.querySelector('.visibility-toggle');
                        visibilityToggle.addEventListener('click', (e) => {
                            e.stopPropagation();
                            obj.visible = !obj.visible;
                            canvas.renderAll();
                            visibilityToggle.textContent = obj.visible ? '👁️' : '🚫';
                        });
                        
                        elements.layerList.appendChild(layerItem);
                    });
                }
                
                function showExportModal() {
                    elements.exportModal.classList.add('active');
                    document.body.style.overflow = 'hidden';
                }
                
                function hideExportModal() {
                    elements.exportModal.classList.remove('active');
                    document.body.style.overflow = '';
                }
                
                function exportDesign(e) {
                    const format = this.dataset.format;
                    hideExportModal();
                    
                    switch(format) {
                        case 'svg':
                            exportAsSVG();
                            break;
                        case 'png':
                            exportAsPNG();
                            break;
                        case 'jpeg':
                            exportAsJPEG();
                            break;
                        case 'pdf':
                            exportAsPDF();
                            break;
                        case 'pdf-cmyk':
                            exportAsPdfCmyk();
                            break;
                    }
                }
                
                function exportAsSVG() {
                    const svg = canvas.toSVG();
                    const blob = new Blob([svg], { type: 'image/svg+xml' });
                    const url = URL.createObjectURL(blob);
                    
                    const a = document.createElement('a');
                    a.href = url;
                    a.download = `franela-design-${new Date().toISOString().slice(0,10)}.svg`;
                    document.body.appendChild(a);
                    a.click();
                    document.body.removeChild(a);
                    URL.revokeObjectURL(url);
                }
                
                function exportAsPNG() {
                    const dataURL = canvas.toDataURL({
                        format: 'png',
                        quality: 1,
                        multiplier: 2
                    });
                    
                    const a = document.createElement('a');
                    a.href = dataURL;
                    a.download = `franela-design-${new Date().toISOString().slice(0,10)}.png`;
                    document.body.appendChild(a);
                    a.click();
                    document.body.removeChild(a);
                }
                
                function exportAsJPEG() {
                    const dataURL = canvas.toDataURL({
                        format: 'jpeg',
                        quality: 0.9,
                        multiplier: 2
                    });
                    
                    const a = document.createElement('a');
                    a.href = dataURL;
                    a.download = `franela-design-${new Date().toISOString().slice(0,10)}.jpg`;
                    document.body.appendChild(a);
                    a.click();
                    document.body.removeChild(a);
                }
                
                function exportAsPDF() {
                    html2canvas(document.querySelector('#design-canvas')).then(canvas => {
                        const { jsPDF } = window.jspdf;
                        const pdf = new jsPDF({
                            orientation: canvas.width > canvas.height ? 'landscape' : 'portrait',
                            unit: 'mm'
                        });
                        
                        const imgData = canvas.toDataURL('image/jpeg', 0.9);
                        const pdfWidth = pdf.internal.pageSize.getWidth();
                        const pdfHeight = (canvas.height * pdfWidth) / canvas.width;
                        
                        pdf.addImage(imgData, 'JPEG', 0, 0, pdfWidth, pdfHeight);
                        
                        pdf.setFontSize(12);
                        pdf.text(`Talla: ${currentSize}`, 10, pdfHeight + 10);
                        pdf.text(`Plantilla: ${currentTemplate}`, 10, pdfHeight + 15);
                        pdf.text(`Fecha: ${new Date().toLocaleDateString()}`, 10, pdfHeight + 20);
                        
                        pdf.save(`franela-design-${new Date().toISOString().slice(0,10)}.pdf`);
                    });
                }
                
                function exportAsPdfCmyk() {
                    // Esta es una simulación básica - en producción necesitarías una solución más robusta
                    // para conversión real a CMYK
                    html2canvas(document.querySelector('#design-canvas')).then(canvas => {
                        const { jsPDF } = window.jspdf;
                        const pdf = new jsPDF({
                            orientation: canvas.width > canvas.height ? 'landscape' : 'portrait',
                            unit: 'mm'
                        });
                        
                        // Simular conversión a CMYK (esto es solo visual, no cambia realmente el espacio de color)
                        const imgData = canvas.toDataURL('image/jpeg', 0.9);
                        const pdfWidth = pdf.internal.pageSize.getWidth();
                        const pdfHeight = (canvas.height * pdfWidth) / canvas.width;
                        
                        pdf.addImage(imgData, 'JPEG', 0, 0, pdfWidth, pdfHeight);
                        
                        pdf.setFontSize(12);
                        pdf.text(`Talla: ${currentSize}`, 10, pdfHeight + 10);
                        pdf.text(`Plantilla: ${currentTemplate}`, 10, pdfHeight + 15);
                        pdf.text(`Fecha: ${new Date().toLocaleDateString()}`, 10, pdfHeight + 20);
                        pdf.text(`Modo Color: CMYK (Para impresión profesional)`, 10, pdfHeight + 25);
                        
                        pdf.save(`franela-design-CMYK-${new Date().toISOString().slice(0,10)}.pdf`);
                    });
                }
                
                function handleObjectAdded(e) {
                    if (!e.target.isTemplate) {
                        saveState();
                        updateLayers();
                    }
                }
                
                function handleObjectModified(e) {
                    if (!e.target.isTemplate) {
                        saveState();
                    }
                }
                
                function handleObjectRemoved(e) {
                    if (!e.target.isTemplate) {
                        saveState();
                        updateLayers();
                    }
                }
                
                function updateUIForSelection() {
                    const activeObject = canvas.getActiveObject();
                    
                    if (activeObject) {
                        elements.fillColorInput.disabled = !('fill' in activeObject);
                        elements.strokeColorInput.disabled = !('stroke' in activeObject);
                        elements.strokeWidthInput.disabled = !('strokeWidth' in activeObject);
                        elements.opacityInput.disabled = false;
                        elements.deleteObjBtn.disabled = false;
                        elements.bringToFrontBtn.disabled = false;
                        elements.sendToBackBtn.disabled = false;
                        
                        if ('fill' in activeObject) {
                            const fillColor = activeObject.fill || '#ffffff';
                            elements.fillColorInput.value = fillColor;
                            
                            if (colorMode === 'cmyk') {
                                const rgb = hexToRgb(fillColor);
                                const cmyk = rgbToCmyk(rgb.r, rgb.g, rgb.b);
                                
                                elements.fillCInk.value = cmyk.c;
                                elements.fillMInk.value = cmyk.m;
                                elements.fillYInk.value = cmyk.y;
                                elements.fillKInk.value = cmyk.k;
                                
                                elements.fillCValue.textContent = `${cmyk.c}%`;
                                elements.fillMValue.textContent = `${cmyk.m}%`;
                                elements.fillYValue.textContent = `${cmyk.y}%`;
                                elements.fillKValue.textContent = `${cmyk.k}%`;
                                
                                elements.fillCmykPreview.style.backgroundColor = fillColor;
                            }
                        }
                        
                        if ('stroke' in activeObject) {
                            const strokeColor = activeObject.stroke || '#000000';
                            elements.strokeColorInput.value = strokeColor;
                            
                            if (colorMode === 'cmyk') {
                                const rgb = hexToRgb(strokeColor);
                                const cmyk = rgbToCmyk(rgb.r, rgb.g, rgb.b);
                                
                                elements.strokeCInk.value = cmyk.c;
                                elements.strokeMInk.value = cmyk.m;
                                elements.strokeYInk.value = cmyk.y;
                                elements.strokeKInk.value = cmyk.k;
                                
                                elements.strokeCValue.textContent = `${cmyk.c}%`;
                                elements.strokeMValue.textContent = `${cmyk.m}%`;
                                elements.strokeYValue.textContent = `${cmyk.y}%`;
                                elements.strokeKValue.textContent = `${cmyk.k}%`;
                                
                                elements.strokeCmykPreview.style.backgroundColor = strokeColor;
                            }
                        }
                        
                        if ('strokeWidth' in activeObject) {
                            elements.strokeWidthInput.value = activeObject.strokeWidth || 0;
                        }
                        
                        if ('opacity' in activeObject) {
                            elements.opacityInput.value = Math.round((activeObject.opacity || 1) * 100);
                        }
                        
                        if (activeObject.type === 'i-text') {
                            elements.textFontSelect.disabled = false;
                            elements.textSizeInput.disabled = false;
                            elements.textColorInput.disabled = false;
                            
                            elements.textFontSelect.value = activeObject.fontFamily || 'Arial';
                            elements.textSizeInput.value = activeObject.fontSize || 20;
                            
                            const textColor = activeObject.fill || '#000000';
                            elements.textColorInput.value = textColor;
                            
                            if (colorMode === 'cmyk') {
                                const rgb = hexToRgb(textColor);
                                const cmyk = rgbToCmyk(rgb.r, rgb.g, rgb.b);
                                
                                // Actualizar controles CMYK basados en el color del texto
                                elements.fillCInk.value = cmyk.c;
                                elements.fillMInk.value = cmyk.m;
                                elements.fillYInk.value = cmyk.y;
                                elements.fillKInk.value = cmyk.k;
                                
                                elements.fillCValue.textContent = `${cmyk.c}%`;
                                elements.fillMValue.textContent = `${cmyk.m}%`;
                                elements.fillYValue.textContent = `${cmyk.y}%`;
                                elements.fillKValue.textContent = `${cmyk.k}%`;
                                
                                elements.fillCmykPreview.style.backgroundColor = textColor;
                            }
                        } else {
                            elements.textFontSelect.disabled = true;
                            elements.textSizeInput.disabled = true;
                            elements.textColorInput.disabled = true;
                        }
                        
                        elements.selectedObject.textContent = `Objeto seleccionado: ${activeObject.type || 'objeto'}`;
                    } else {
                        elements.fillColorInput.disabled = true;
                        elements.strokeColorInput.disabled = true;
                        elements.strokeWidthInput.disabled = true;
                        elements.opacityInput.disabled = true;
                        elements.textFontSelect.disabled = true;
                        elements.textSizeInput.disabled = true;
                        elements.textColorInput.disabled = true;
                        elements.deleteObjBtn.disabled = true;
                        elements.bringToFrontBtn.disabled = true;
                        elements.sendToBackBtn.disabled = true;
                        
                        elements.selectedObject.textContent = 'Objeto seleccionado: Ninguno';
                    }
                    
                    updateLayers();
                }
                
                function updateCursorPosition(e) {
                    const pointer = canvas.getPointer(e.e);
                    if (pointer) {
                        elements.cursorPosition.textContent = `X: ${Math.round(pointer.x)}, Y: ${Math.round(pointer.y)}`;
                    }
                }
                
                function toggleToolbar() {
                    document.getElementById('main-toolbar').classList.toggle('active');
                }
                
                function saveState() {
                    if (historyIndex < history.length - 1) {
                        history = history.slice(0, historyIndex + 1);
                    }
                    
                    if (history.length >= 50) {
                        history.shift();
                    } else {
                        historyIndex++;
                    }
                    
                    history.push(JSON.stringify(canvas.toJSON()));
                }
                
                function showSizeModal() {
                    elements.sizeModal.classList.add('active');
                    document.body.style.overflow = 'hidden';
                }
                
                function hideSizeModal() {
                    elements.sizeModal.classList.remove('active');
                    document.body.style.overflow = '';
                }
                
                function selectSizeOption() {
                    elements.sizeOptions.forEach(option => option.classList.remove('selected'));
                    this.classList.add('selected');
                    
                    if (this.dataset.size === 'custom') {
                        elements.customSizeSection.style.display = 'block';
                    } else {
                        elements.customSizeSection.style.display = 'none';
                        currentSize = this.dataset.size;
                    }
                }
                
                function updateCustomSizeDisplay() {
                    if (this.id === 'custom-width') {
                        elements.widthValue.textContent = `${this.value} cm`;
                    } else if (this.id === 'custom-height') {
                        elements.heightValue.textContent = `${this.value} cm`;
                    } else if (this.id === 'custom-sleeve') {
                        elements.sleeveValue.textContent = `${this.value} cm`;
                    }
                }
                
                function applySize() {
                    if (document.querySelector('.size-option.selected').dataset.size === 'custom') {
                        currentSize = 'custom';
                    }
                    
                    loadTemplate(currentTemplate);
                    hideSizeModal();
                }
            }
        });
    </script>
</body>
</html>
