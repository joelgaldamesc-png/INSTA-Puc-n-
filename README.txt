<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <title>INSTA Pucón - Control de Ventas</title>
  <style>
    :root {
      --bg-color: #0f0f12;
      --card-bg: #1a1a20;
      --card-border: #2a2a35;
      --accent-color: #d4a359;
      --text-main: #ffffff;
      --text-muted: #a0a0b0;
      --btn-bg: #252530;
      --btn-active: #d4a359;
      --btn-active-text: #000000;
      --danger-color: #e63946;
      --success-color: #2a9d8f;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      -webkit-tap-highlight-color: transparent;
    }

    body {
      background-color: var(--bg-color);
      color: var(--text-main);
      display: flex;
      justify-content: center;
      min-height: 100vh;
      padding: 12px;
    }

    /* SPLASH SCREEN */
    #splash-screen {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background-color: #000000;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      z-index: 9999;
      transition: opacity 0.5s ease, visibility 0.5s;
    }

    #splash-screen.hidden {
      opacity: 0;
      visibility: hidden;
    }

    .splash-logo {
      width: 200px;
      height: auto;
      margin-bottom: 20px;
    }

    .splash-title {
      color: #fff;
      font-size: 1.8rem;
      font-weight: 800;
      letter-spacing: 1px;
    }

    .splash-subtitle {
      color: var(--accent-color);
      font-size: 0.9rem;
      letter-spacing: 2px;
      margin-top: 5px;
    }

    /* CONTENEDOR PRINCIPAL */
    .app-container {
      width: 100%;
      max-width: 480px;
      display: flex;
      flex-direction: column;
      gap: 14px;
      padding-bottom: 20px;
    }

    /* HEADER */
    .header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px 4px;
    }

    .brand-title {
      font-size: 1.4rem;
      font-weight: 800;
      letter-spacing: -0.5px;
    }

    .brand-title span {
      color: var(--accent-color);
    }

    .clock-container {
      text-align: right;
    }

    .digital-clock {
      font-size: 1.1rem;
      font-weight: 700;
      font-family: monospace;
      color: var(--accent-color);
    }

    .date-display {
      font-size: 0.75rem;
      color: var(--text-muted);
      text-transform: capitalize;
    }

    .menu-btn {
      background: var(--card-bg);
      border: 1px solid var(--card-border);
      color: var(--text-main);
      font-size: 1.3rem;
      padding: 8px 12px;
      border-radius: 10px;
      cursor: pointer;
    }

    /* TARJETAS DE CONTENIDO */
    .card {
      background-color: var(--card-bg);
      border: 1px solid var(--card-border);
      border-radius: 18px;
      padding: 16px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.3);
    }

    .card-title {
      font-size: 0.75rem;
      font-weight: 700;
      color: var(--text-muted);
      text-transform: uppercase;
      letter-spacing: 0.8px;
      margin-bottom: 12px;
    }

    /* RESUMEN HOY */
    .stats-count {
      font-size: 2.2rem;
      font-weight: 900;
      line-height: 1;
    }

    .stats-amount {
      font-size: 1.8rem;
      font-weight: 800;
      color: var(--accent-color);
      margin-top: 4px;
    }

    .goal-info {
      display: flex;
      justify-content: space-between;
      font-size: 0.8rem;
      color: var(--text-muted);
      margin-top: 12px;
      margin-bottom: 6px;
    }

    .progress-bar {
      width: 100%;
      height: 8px;
      background-color: #2a2a35;
      border-radius: 4px;
      overflow: hidden;
    }

    .progress-fill {
      height: 100%;
      background: linear-gradient(90deg, var(--accent-color), #f3c98b);
      width: 0%;
      transition: width 0.3s ease;
    }

    /* GRID BOTONES */
    .grid-2x2 {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 10px;
    }

    .btn-action {
      background-color: var(--btn-bg);
      border: 1px solid var(--card-border);
      color: var(--text-main);
      border-radius: 14px;
      padding: 16px 10px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      transition: all 0.15s ease;
      min-height: 75px;
    }

    .btn-action:active {
      transform: scale(0.97);
    }

    .btn-action.selected {
      background-color: var(--accent-color);
      color: #000;
      border-color: var(--accent-color);
    }

    .btn-action.selected .btn-price {
      color: #222;
    }

    .btn-label {
      font-size: 1rem;
      font-weight: 700;
    }

    .btn-price {
      font-size: 0.85rem;
      color: var(--text-muted);
      margin-top: 4px;
      font-weight: 600;
    }

    /* METODOS DE PAGO */
    .payment-btn {
      background-color: #22222a;
      border: 1px solid var(--card-border);
      opacity: 0.6;
      cursor: not-allowed;
    }

    .payment-btn.active {
      opacity: 1;
      cursor: pointer;
      border-color: #3a3a4a;
    }

    .payment-btn.active:hover {
      background-color: #2a2a35;
    }

    .status-msg {
      font-size: 0.8rem;
      color: var(--accent-color);
      text-align: center;
      margin-top: 10px;
      font-weight: 600;
      min-height: 18px;
    }

    /* FILAS DE DETALLE */
    .detail-row {
      display: flex;
      justify-content: space-between;
      padding: 8px 0;
      border-bottom: 1px solid #22222a;
      font-size: 0.9rem;
    }

    .detail-row:last-child {
      border-bottom: none;
    }

    .detail-value {
      font-weight: 700;
    }

    /* BOTONES DE ACCION */
    .btn-secondary {
      background-color: #22222a;
      border: 1px solid var(--card-border);
      color: var(--text-main);
      padding: 12px;
      border-radius: 12px;
      font-weight: 700;
      cursor: pointer;
      width: 100%;
    }

    .btn-danger {
      background-color: rgba(230, 57, 70, 0.15);
      border: 1px solid var(--danger-color);
      color: var(--danger-color);
    }

    .hint-text {
      font-size: 0.75rem;
      color: var(--text-muted);
      text-align: center;
      margin-top: 10px;
      line-height: 1.4;
    }

    /* MODAL */
    .modal {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background: rgba(0,0,0,0.8);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 1000;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.2s ease;
      padding: 20px;
    }

    .modal.active {
      opacity: 1;
      pointer-events: auto;
    }

    .modal-content {
      background: var(--card-bg);
      border: 1px solid var(--card-border);
      width: 100%;
      max-width: 400px;
      border-radius: 20px;
      padding: 20px;
      max-height: 80vh;
      display: flex;
      flex-direction: column;
    }

    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 15px;
    }

    .modal-title {
      font-size: 1.1rem;
      font-weight: 700;
    }

    .close-btn {
      background: none;
      border: none;
      color: var(--text-muted);
      font-size: 1.5rem;
      cursor: pointer;
    }

    .input-custom {
      width: 100%;
      padding: 14px;
      background: #121216;
      border: 1px solid var(--card-border);
      border-radius: 12px;
      color: #fff;
      font-size: 1.2rem;
      margin-bottom: 15px;
      text-align: center;
    }

    .history-list {
      overflow-y: auto;
      flex-grow: 1;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .history-item {
      background: #121216;
      padding: 12px;
      border-radius: 10px;
      border-left: 3px solid var(--accent-color);
      font-size: 0.85rem;
    }

    .history-date {
      color: var(--text-muted);
      font-size: 0.75rem;
      margin-bottom: 4px;
    }
  </style>
</head>
<body>

  <!-- SPLASH SCREEN DE INICIO -->
  <div id="splash-screen">
    <!-- SVG Representativo del Logo INSTA Pucón -->
    <svg class="splash-logo" viewBox="0 0 300 200" fill="none" xmlns="http://www.w3.org/2000/svg">
      <rect x="75" y="40" width="150" height="90" rx="12" stroke="white" stroke-width="4"/>
      <circle cx="150" cy="85" r="28" stroke="white" stroke-width="4"/>
      <circle cx="150" cy="85" r="16" stroke="white" stroke-width="3"/>
      <rect x="90" y="25" width="35" height="15" rx="4" stroke="white" stroke-width="3"/>
      <circle cx="200" cy="55" r="5" fill="white"/>
      <text x="150" y="155" text-anchor="middle" fill="white" font-size="22" font-weight="bold" font-family="sans-serif">INSTA <tspan fill="#d4a359">Pucón</tspan></text>
      <line x1="40" y1="170" x2="260" y2="170" stroke="white" stroke-width="1"/>
      <text x="150" y="185" text-anchor="middle" fill="white" font-size="10" letter-spacing="3" font-family="sans-serif">FOTOS INSTANTÁNEAS</text>
    </svg>
    <div class="splash-title">INSTA <span style="color:var(--accent-color)">Pucón</span></div>
    <div class="splash-subtitle">SISTEMA DE VENTAS</div>
  </div>

  <div class="app-container">
    
    <!-- ENCABEZADO -->
    <div class="header">
      <div>
        <div class="brand-title">INSTA <span>Pucón</span> 📸</div>
        <div class="date-display" id="dateDisplay">Cargando fecha...</div>
      </div>
      <div style="display:flex; align-items:center; gap:10px;">
        <div class="clock-container">
          <div class="digital-clock" id="clockDisplay">00:00:00</div>
        </div>
        <button class="menu-btn" id="openMenuBtn">☰</button>
      </div>
    </div>

    <!-- TARJETA 1: FOTOS VENDIDAS HOY -->
    <div class="card">
      <div class="card-title">Fotos Vendidas Hoy</div>
      <div class="stats-count" id="todayPhotos">0</div>
      <div class="stats-amount" id="todayAmount">$0</div>
      
      <div class="goal-info">
        <span>Meta: <strong id="goalTarget">50</strong> fotos</span>
        <span>Faltan: <strong id="goalRemaining">50</strong></span>
      </div>
      <div class="progress-bar">
        <div class="progress-fill" id="progressBar"></div>
      </div>
    </div>

    <!-- TARJETA 2: REGISTRAR VENTA -->
    <div class="card">
      <div class="card-title">Registrar Venta</div>
      <div class="grid-2x2">
        <button class="btn-action photo-btn" data-type="preset" data-photos="1" data-price="4000">
          <span class="btn-label">+ 1 foto</span>
          <span class="btn-price">$4.000</span>
        </button>
        <button class="btn-action photo-btn" data-type="preset" data-photos="2" data-price="8000">
          <span class="btn-label">+ 2 fotos</span>
          <span class="btn-price">$8.000</span>
        </button>
        <button class="btn-action photo-btn" data-type="preset" data-photos="1" data-price="5000">
          <span class="btn-label">Turista</span>
          <span class="btn-price">$5.000</span>
        </button>
        <button class="btn-action" id="customAmountBtn">
          <span class="btn-label">Otro monto</span>
          <span class="btn-price">Personalizado</span>
        </button>
      </div>
    </div>

    <!-- TARJETA 3: MEDIO DE PAGO -->
    <div class="card">
      <div class="card-title">Medio de Pago</div>
      <div class="grid-2x2">
        <button class="btn-action payment-btn" data-method="efectivo">
          <span class="btn-label">💵 Efectivo</span>
        </button>
        <button class="btn-action payment-btn" data-method="transferencia">
          <span class="btn-label">📲 Transferencia</span>
        </button>
        <button class="btn-action payment-btn" data-method="tarjeta">
          <span class="btn-label">💳 Tarjeta</span>
        </button>
        <button class="btn-action payment-btn" data-method="otro">
          <span class="btn-label">⚙️ Otro</span>
        </button>
      </div>
      <div class="status-msg" id="statusMsg">Selecciona una opción de foto arriba</div>
    </div>

    <!-- TARJETA 4: RESUMEN POR PAGO -->
    <div class="card">
      <div class="card-title">Resumen por Pago</div>
      <div class="detail-row">
        <span>💵 Efectivo</span>
        <span class="detail-value" id="totalEfectivo">$0</span>
      </div>
      <div class="detail-row">
        <span>📲 Transferencia</span>
        <span class="detail-value" id="totalTransferencia">$0</span>
      </div>
      <div class="detail-row">
        <span>💳 Tarjeta</span>
        <span class="detail-value" id="totalTarjeta">$0</span>
      </div>
      <div class="detail-row">
        <span>⚙️ Otro</span>
        <span class="detail-value" id="totalOtro">$0</span>
      </div>
    </div>

    <!-- TARJETA 5: ACCIONES -->
    <div class="card">
      <div class="card-title">Acciones</div>
      <div class="grid-2x2">
        <button class="btn-secondary" id="undoBtn">↩️ Deshacer</button>
        <button class="btn-secondary btn-danger" id="resetDayBtn">🔄 Reiniciar día</button>
      </div>
      <div class="hint-text">
        Consejo: selecciona el tipo de venta/foto y luego presiona el medio de pago para registrarla.
      </div>
    </div>

  </div>

  <!-- MODAL OTRO MONTO -->
  <div class="modal" id="customModal">
    <div class="modal-content">
      <div class="modal-header">
        <div class="modal-title">Ingresar Monto Personalizado</div>
        <button class="close-btn" id="closeCustomModal">&times;</button>
      </div>
      <input type="number" id="customPriceInput" class="input-custom" placeholder="Monto en CLP ($)" pattern="[0-9]*" inputmode="numeric">
      <input type="number" id="customPhotosInput" class="input-custom" placeholder="Cantidad de fotos (ej: 1)" value="1" pattern="[0-9]*" inputmode="numeric">
      <button class="btn-secondary" id="confirmCustomBtn" style="background:var(--accent-color); color:#000;">Confirmar Selección</button>
    </div>
  </div>

  <!-- MODAL HISTÓRICO DE VENTAS -->
  <div class="modal" id="historyModal">
    <div class="modal-content">
      <div class="modal-header">
        <div class="modal-title">📜 Histórico de Ventas</div>
        <button class="close-btn" id="closeHistoryModal">&times;</button>
      </div>
      <div class="history-list" id="historyContainer">
        <!-- Se llena con JS -->
      </div>
      <button class="btn-secondary btn-danger" id="clearHistoryBtn" style="margin-top:15px;">Borrar Histórico</button>
    </div>
  </div>

  <script>
    // ESTADO DE LA APLICACIÓN
    const TARGET_PHOTOS = 50;
    
    let appData = JSON.parse(localStorage.getItem('insta_pucon_data')) || {
      today: {
        photos: 0,
        amount: 0,
        efectivo: 0,
        transferencia: 0,
        tarjeta: 0,
        otro: 0,
        transactions: []
      },
      history: []
    };

    let selectedSale = null; // { photos: number, price: number }

    // ELEMENTOS DOM
    const splashScreen = document.getElementById('splash-screen');
    const clockDisplay = document.getElementById('clockDisplay');
    const dateDisplay = document.getElementById('dateDisplay');
    const todayPhotosEl = document.getElementById('todayPhotos');
    const todayAmountEl = document.getElementById('todayAmount');
    const goalRemainingEl = document.getElementById('goalRemaining');
    const progressBar = document.getElementById('progressBar');
    const statusMsg = document.getElementById('statusMsg');
    
    const totalEfectivoEl = document.getElementById('totalEfectivo');
    const totalTransferenciaEl = document.getElementById('totalTransferencia');
    const totalTarjetaEl = document.getElementById('totalTarjeta');
    const totalOtroEl = document.getElementById('totalOtro');

    const photoBtns = document.querySelectorAll('.photo-btn');
    const paymentBtns = document.querySelectorAll('.payment-btn');
    const customAmountBtn = document.getElementById('customAmountBtn');
    
    const undoBtn = document.getElementById('undoBtn');
    const resetDayBtn = document.getElementById('resetDayBtn');

    const historyModal = document.getElementById('historyModal');
    const openMenuBtn = document.getElementById('openMenuBtn');
    const closeHistoryModal = document.getElementById('closeHistoryModal');
    const historyContainer = document.getElementById('historyContainer');
    const clearHistoryBtn = document.getElementById('clearHistoryBtn');

    const customModal = document.getElementById('customModal');
    const closeCustomModal = document.getElementById('closeCustomModal');
    const confirmCustomBtn = document.getElementById('confirmCustomBtn');
    const customPriceInput = document.getElementById('customPriceInput');
    const customPhotosInput = document.getElementById('customPhotosInput');

    // FORMATO MONEDA CLP
    function formatCLP(val) {
      return '$' + val.toLocaleString('es-CL');
    }

    // RELOJ EN VIVO
    function updateClock() {
      const now = new Date();
      clockDisplay.textContent = now.toLocaleTimeString('es-CL', { hour12: false });
      const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
      dateDisplay.textContent = now.toLocaleDateString('es-CL', options);
    }
    setInterval(updateClock, 1000);
    updateClock();

    // OCULTAR SPLASH SCREEN TRAS 2 SEGUNDOS
    setTimeout(() => {
      splashScreen.classList.add('hidden');
    }, 2000);

    // GUARDAR EN LOCALSTORAGE
    function saveData() {
      localStorage.setItem('insta_pucon_data', JSON.stringify(appData));
    }

    // ACTUALIZAR INTERFAZ
    function render() {
      const today = appData.today;
      todayPhotosEl.textContent = today.photos;
      todayAmountEl.textContent = formatCLP(today.amount);

      const remaining = Math.max(0, TARGET_PHOTOS - today.photos);
      goalRemainingEl.textContent = remaining;

      const progressPercent = Math.min(100, (today.photos / TARGET_PHOTOS) * 100);
      progressBar.style.width = `${progressPercent}%`;

      totalEfectivoEl.textContent = formatCLP(today.efectivo);
      totalTransferenciaEl.textContent = formatCLP(today.transferencia);
      totalTarjetaEl.textContent = formatCLP(today.tarjeta);
      totalOtroEl.textContent = formatCLP(today.otro);

      // Resetear estado de selección de pago
      paymentBtns.forEach(btn => {
        if (selectedSale) {
          btn.classList.add('active');
        } else {
          btn.classList.remove('active');
        }
      });

      if (selectedSale) {
        statusMsg.textContent = `Seleccionado: ${selectedSale.photos} foto(s) por ${formatCLP(selectedSale.price)}. Elige medio de pago.`;
      } else {
        statusMsg.textContent = `Venta registrada. Elige otra opción de foto.`;
      }

      saveData();
    }

    // SELECCIÓN DE PRESETS
    photoBtns.forEach(btn => {
      btn.addEventListener('click', () => {
        photoBtns.forEach(b => b.classList.remove('selected'));
        customAmountBtn.classList.remove('selected');
        
        btn.classList.add('selected');
        const photos = parseInt(btn.dataset.photos);
        const price = parseInt(btn.dataset.price);

        selectedSale = { photos, price };
        render();
      });
    });

    // CUSTOM AMOUNT MODAL
    customAmountBtn.addEventListener('click', () => {
      customModal.classList.add('active');
      customPriceInput.focus();
    });

    closeCustomModal.addEventListener('click', () => {
      customModal.classList.remove('active');
    });

    confirmCustomBtn.addEventListener('click', () => {
      const price = parseInt(customPriceInput.value);
      const photos = parseInt(customPhotosInput.value) || 1;

      if (!price || price <= 0) {
        alert("Por favor ingresa un monto válido en CLP.");
        return;
      }

      photoBtns.forEach(b => b.classList.remove('selected'));
      customAmountBtn.classList.add('selected');

      selectedSale = { photos, price };
      customModal.classList.remove('active');
      customPriceInput.value = '';
      render();
    });

    // PROCESAR PAGO
    paymentBtns.forEach(btn => {
      btn.addEventListener('click', () => {
        if (!selectedSale) return;

        const method = btn.dataset.method;
        const sale = {
          photos: selectedSale.photos,
          price: selectedSale.price,
          method: method,
          time: new Date().toLocaleTimeString('es-CL', { hour: '2-digit', minute: '2-digit' })
        };

        appData.today.photos += sale.photos;
        appData.today.amount += sale.price;
        appData.today[method] += sale.price;
        appData.today.transactions.push(sale);

        // Reset Selección
        selectedSale = null;
        photoBtns.forEach(b => b.classList.remove('selected'));
        customAmountBtn.classList.remove('selected');

        render();
      });
    });

    // DESHACER ÚLTIMA VENTA
    undoBtn.addEventListener('click', () => {
      const txs = appData.today.transactions;
      if (txs.length === 0) {
        alert("No hay ventas registradas para deshacer hoy.");
        return;
      }

      const lastTx = txs.pop();
      appData.today.photos -= lastTx.photos;
      appData.today.amount -= lastTx.price;
      appData.today[lastTx.method] -= lastTx.price;

      render();
    });

    // REINICIAR DÍA (Guarda en Histórico)
    resetDayBtn.addEventListener('click', () => {
      if (appData.today.photos === 0 && appData.today.amount === 0) {
        alert("El día actual ya está en cero.");
        return;
      }

      if (confirm("¿Seguro que deseas reiniciar el día? Las ventas se guardarán en el Histórico.")) {
        const todayRecord = {
          date: new Date().toLocaleDateString('es-CL'),
          photos: appData.today.photos,
          amount: appData.today.amount,
          efectivo: appData.today.efectivo,
          transferencia: appData.today.transferencia,
          tarjeta: appData.today.tarjeta,
          otro: appData.today.otro
        };

        appData.history.unshift(todayRecord);

        // Reiniciar
        appData.today = {
          photos: 0,
          amount: 0,
          efectivo: 0,
          transferencia: 0,
          tarjeta: 0,
          otro: 0,
          transactions: []
        };

        selectedSale = null;
        photoBtns.forEach(b => b.classList.remove('selected'));
        customAmountBtn.classList.remove('selected');

        render();
      }
    });

    // MENÚ HISTÓRICO
    openMenuBtn.addEventListener('click', () => {
      renderHistory();
      historyModal.classList.add('active');
    });

    closeHistoryModal.addEventListener('click', () => {
      historyModal.classList.remove('active');
    });

    function renderHistory() {
      historyContainer.innerHTML = '';
      if (appData.history.length === 0) {
        historyContainer.innerHTML = '<div style="color:var(--text-muted); text-align:center; padding:20px;">No hay histórico registrado aún.</div>';
        return;
      }

      appData.history.forEach(item => {
        const div = document.createElement('div');
        div.className = 'history-item';
        div.innerHTML = `
          <div class="history-date">📅 ${item.date}</div>
          <div style="font-weight:700; font-size:1rem; margin-bottom:4px;">
            ${item.photos} foto(s) — <span style="color:var(--accent-color);">${formatCLP(item.amount)}</span>
          </div>
          <div style="color:var(--text-muted); font-size:0.75rem;">
            💵 Efec: ${formatCLP(item.efectivo)} | 📲 Trans: ${formatCLP(item.transferencia)} | 💳 Tarj: ${formatCLP(item.tarjeta)}
          </div>
        `;
        historyContainer.appendChild(div);
      });
    }

    clearHistoryBtn.addEventListener('click', () => {
      if (confirm("¿Deseas eliminar todo el historial acumulado? Esta acción no se puede deshacer.")) {
        appData.history = [];
        renderHistory();
        saveData();
      }
    });

    // Inicializar
    render();
  </script>
</body>
</html>
