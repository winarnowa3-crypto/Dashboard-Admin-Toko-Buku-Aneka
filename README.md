<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Admin Aneka | Book & Stationery</title>
    <!-- Google Font, Font Awesome, Chart.js -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,500;14..32,600;14..32,700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
            transition: background-color 0.3s ease, border-color 0.2s ease, color 0.2s ease;
        }

        :root {
            --bg-body: #f1f5f9;
            --bg-sidebar: #ffffff;
            --card-bg: #ffffff;
            --text-primary: #0f172a;
            --text-secondary: #5b6e8c;
            --border-light: #eef2f6;
            --nav-hover: #eef2ff;
            --stat-icon-bg: #eff3ff;
            --table-header: #fafcff;
            --input-bg: #ffffff;
            --shadow-sm: 0 8px 20px rgba(0,0,0,0.02);
        }

        body.dark {
            --bg-body: #0f172a;
            --bg-sidebar: #1e293b;
            --card-bg: #1e293b;
            --text-primary: #f1f5f9;
            --text-secondary: #94a3b8;
            --border-light: #334155;
            --nav-hover: #2d3a5e;
            --stat-icon-bg: #2d3a5e;
            --table-header: #1e293b;
            --input-bg: #0f172a;
            --shadow-sm: 0 8px 20px rgba(0,0,0,0.3);
        }

        body {
            background: var(--bg-body);
            display: flex;
            height: 100vh;
            overflow: hidden;
        }

        .sidebar {
            width: 280px;
            background: var(--bg-sidebar);
            border-right: 1px solid var(--border-light);
            display: flex;
            flex-direction: column;
            transition: all 0.25s ease;
            z-index: 10;
        }

        .logo-area {
            padding: 28px 24px;
            display: flex;
            align-items: center;
            gap: 12px;
            border-bottom: 1px solid var(--border-light);
        }
        .logo-icon {
            background: #2c3e66;
            width: 40px;
            height: 40px;
            border-radius: 14px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 1.5rem;
        }
        .logo-text h2 {
            font-size: 1.45rem;
            font-weight: 700;
            color: var(--text-primary);
        }
        .logo-text p {
            font-size: 0.7rem;
            color: var(--text-secondary);
        }

        .nav-menu {
            flex: 1;
            padding: 32px 20px;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .nav-item {
            display: flex;
            align-items: center;
            gap: 14px;
            padding: 12px 18px;
            border-radius: 16px;
            font-weight: 500;
            font-size: 0.95rem;
            color: var(--text-secondary);
            cursor: pointer;
            transition: all 0.2s ease;
        }
        .nav-item i { width: 24px; font-size: 1.2rem; }
        .nav-item.active {
            background: #2c3e66;
            color: white;
            box-shadow: 0 6px 12px -6px rgba(44,62,102,0.3);
        }
        .nav-item:not(.active):hover {
            background: var(--nav-hover);
            color: var(--text-primary);
            transform: translateX(5px);
        }

        .main-content {
            flex: 1;
            overflow-y: auto;
            padding: 24px 32px;
        }

        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 28px;
            flex-wrap: wrap;
            gap: 15px;
        }
        .page-title h1 {
            font-size: 1.9rem;
            font-weight: 700;
            background: linear-gradient(135deg, #2c3e66, #4f6f8f);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        .admin-badge {
            background: var(--card-bg);
            padding: 8px 20px;
            border-radius: 40px;
            display: flex;
            align-items: center;
            gap: 12px;
            border: 1px solid var(--border-light);
            color: var(--text-primary);
        }
        .theme-toggle {
            background: var(--card-bg);
            border: 1px solid var(--border-light);
            border-radius: 50px;
            padding: 8px 16px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            font-weight: 500;
            color: var(--text-primary);
        }
        .theme-toggle:hover { background: var(--nav-hover); transform: scale(1.02); }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 24px;
            margin-bottom: 32px;
        }
        .stat-card {
            background: var(--card-bg);
            border-radius: 28px;
            padding: 20px;
            border: 1px solid var(--border-light);
            display: flex;
            align-items: center;
            justify-content: space-between;
            transition: transform 0.2s, box-shadow 0.2s;
        }
        .stat-card:hover { transform: translateY(-6px); box-shadow: 0 20px 30px -12px rgba(0,0,0,0.15); }
        .stat-info h3 { font-size: 0.85rem; color: var(--text-secondary); margin-bottom: 10px; }
        .stat-number { font-size: 2rem; font-weight: 800; color: var(--text-primary); }
        .stat-icon {
            width: 54px; height: 54px; background: var(--stat-icon-bg); border-radius: 40px;
            display: flex; align-items: center; justify-content: center; font-size: 1.8rem; color: #2c3e66;
        }

        .insight-row {
            display: flex;
            flex-wrap: wrap;
            gap: 28px;
            margin-bottom: 40px;
        }
        .chart-box, .recent-orders {
            background: var(--card-bg);
            border-radius: 28px;
            padding: 20px;
            border: 1px solid var(--border-light);
        }
        .chart-box { flex: 2; }
        .recent-orders { flex: 1.2; }
        .section-title {
            font-weight: 600;
            margin-bottom: 18px;
            font-size: 1.2rem;
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--text-primary);
        }

        .order-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 14px 0;
            border-bottom: 1px solid var(--border-light);
        }
        .order-id { font-weight: 600; font-size: 0.85rem; color: var(--text-primary); }
        .order-total { font-weight: 700; color: #2c3e66; }
        .badge {
            background: #e6f7ec; color: #2b6e3c; font-size: 0.7rem;
            font-weight: 600; padding: 4px 10px; border-radius: 50px;
        }
        .badge.warning { background: #fff0db; color: #b45a1c; }
        .badge.info { background: #e1edff; color: #1f509e; }
        body.dark .badge { filter: brightness(0.9); }
        body.dark .badge.warning { background: #5e3a1a; color: #ffdc9f; }
        body.dark .badge.info { background: #1e3a5f; color: #aac9ff; }

        .crud-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            margin: 20px 0 20px 0;
            gap: 15px;
        }
        .btn-primary {
            background: #2c3e66; border: none; color: white; padding: 10px 20px;
            border-radius: 40px; display: flex; align-items: center; gap: 8px;
            cursor: pointer; transition: 0.2s;
        }
        .btn-primary:hover { background: #1f2f4e; transform: scale(1.02); }
        .search-box {
            display: flex; align-items: center; background: var(--input-bg);
            padding: 6px 16px; border-radius: 50px; gap: 10px;
            border: 1px solid var(--border-light);
        }
        .search-box input {
            border: none; padding: 8px 0; width: 200px; outline: none;
            background: transparent; color: var(--text-primary);
        }
        .table-wrapper {
            background: var(--card-bg); border-radius: 24px;
            overflow-x: auto; border: 1px solid var(--border-light);
        }
        table { width: 100%; border-collapse: collapse; }
        th {
            text-align: left; padding: 18px 18px; background: var(--table-header);
            font-weight: 600; color: var(--text-primary);
            border-bottom: 1px solid var(--border-light);
        }
        td { padding: 14px 18px; border-bottom: 1px solid var(--border-light); color: var(--text-primary); }
        .btn-action { background: none; border: none; font-size: 1rem; cursor: pointer; margin: 0 6px; padding: 6px; border-radius: 30px; }
        .btn-edit { color: #2c6e9e; }
        .btn-delete { color: #c2412c; }
        .btn-action:hover { transform: scale(1.1); background: var(--nav-hover); }
        .low-stock { background-color: rgba(245, 158, 11, 0.1); }

        .modal {
            display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background-color: rgba(0,0,0,0.5); backdrop-filter: blur(6px);
            align-items: center; justify-content: center; z-index: 1000;
        }
        .modal-card {
            background: var(--card-bg); max-width: 500px; width: 90%;
            border-radius: 36px; padding: 28px; animation: fadeInUp 0.2s;
        }
        .modal-card h3 { color: var(--text-primary); margin-bottom: 20px; }
        .modal-card input, .modal-card select {
            width: 100%; padding: 14px 16px; margin: 12px 0;
            border: 1px solid var(--border-light); border-radius: 30px;
            background: var(--input-bg); color: var(--text-primary);
        }
        .modal-actions { display: flex; justify-content: flex-end; gap: 12px; margin-top: 20px; }
        .modal-actions button { padding: 10px 22px; border-radius: 40px; border: none; font-weight: 500; cursor: pointer; }
        .btn-save { background: #2c3e66; color: white; }
        .btn-cancel { background: #eef2f6; color: #1e293b; }
        body.dark .btn-cancel { background: #334155; color: #f1f5f9; }
        footer { text-align: center; margin-top: 40px; font-size: 0.75rem; color: var(--text-secondary); }

        .particle {
            position: fixed; pointer-events: none; z-index: 9999;
            width: 8px; height: 8px; background: #3b82f6; border-radius: 50%;
            opacity: 0.8; animation: floatParticle 1.2s ease-out forwards;
        }
        @keyframes floatParticle {
            0% { transform: translateY(0) scale(1); opacity: 0.9; }
            100% { transform: translateY(-100px) scale(0); opacity: 0; }
        }
        @keyframes fadeInUp { from { opacity: 0; transform: scale(0.95); } to { opacity: 1; transform: scale(1); } }

        .login-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.75); backdrop-filter: blur(12px);
            z-index: 10000; display: flex; align-items: center; justify-content: center;
            transition: opacity 0.5s ease;
        }
        .login-card {
            background: var(--card-bg); max-width: 420px; width: 90%;
            border-radius: 48px; padding: 40px 32px; text-align: center;
            animation: introGlow 0.6s cubic-bezier(0.2, 0.9, 0.4, 1.1);
        }
        @keyframes introGlow {
            0% { opacity: 0; transform: scale(0.9) translateY(30px); }
            100% { opacity: 1; transform: scale(1) translateY(0); }
        }
        .login-card .logo-login {
            font-size: 3rem; background: #2c3e66; width: 80px; height: 80px;
            margin: 0 auto 20px; border-radius: 30px; display: flex;
            align-items: center; justify-content: center; color: white;
        }
        .login-card h2 { font-size: 1.8rem; color: var(--text-primary); }
        .login-card p { color: var(--text-secondary); margin-bottom: 28px; }
        .login-card input {
            width: 100%; padding: 14px 18px; margin: 12px 0;
            border: 1px solid var(--border-light); border-radius: 60px;
            background: var(--input-bg); color: var(--text-primary);
        }
        .login-card button {
            width: 100%; padding: 14px; background: #2c3e66; color: white;
            border: none; border-radius: 60px; font-weight: 700; cursor: pointer;
        }
        .error-msg { color: #e53e3e; font-size: 0.8rem; margin-top: 12px; min-height: 32px; }

        @media (max-width: 780px) {
            .sidebar { width: 80px; }
            .sidebar .logo-text, .sidebar .nav-item span { display: none; }
            .sidebar .nav-item i { margin: 0 auto; }
            .nav-item { justify-content: center; }
            .main-content { padding: 16px; }
        }
    </style>
</head>
<body>

<div id="loginOverlay" class="login-overlay">
    <div class="login-card">
        <div class="logo-login"><i class="fas fa-book-open"></i></div>
        <h2>Welcome Back</h2>
        <p>Admin Aneka Book & Stationery</p>
        <input type="text" id="loginUsername" placeholder="Username">
        <input type="password" id="loginPassword" placeholder="Password">
        <button id="loginBtn"><i class="fas fa-key"></i> Masuk ke Dashboard</button>
        <div id="loginError" class="error-msg"></div>
    </div>
</div>

<div id="appContent" style="display: none; width: 100%; display: flex;">
<div class="sidebar">
    <div class="logo-area">
        <div class="logo-icon"><i class="fas fa-book-open"></i></div>
        <div class="logo-text"><h2>Aneka</h2><p>Book & Stationery</p></div>
    </div>
    <div class="nav-menu">
        <div class="nav-item active" data-section="dashboard"><i class="fas fa-tachometer-alt"></i> <span>Dashboard</span></div>
        <div class="nav-item" data-section="products"><i class="fas fa-boxes"></i> <span>Manajemen Produk</span></div>
        <div class="nav-item" data-section="orders"><i class="fas fa-shopping-cart"></i> <span>Manajemen Pesanan</span></div>
    </div>
</div>

<div class="main-content">
    <div class="top-bar">
        <div class="page-title"><h1 id="mainTitle">Dashboard Admin</h1></div>
        <div style="display: flex; gap: 12px;">
            <button class="theme-toggle" id="darkModeToggle"><i class="fas fa-moon"></i> <span id="themeText">Mode Gelap</span></button>
            <div class="admin-badge"><i class="fas fa-user-shield"></i> <span>Admin Aneka</span></div>
        </div>
    </div>

    <div id="dashboardSection">
        <div class="stats-grid">
            <div class="stat-card"><div class="stat-info"><h3>Total Pendapatan</h3><div class="stat-number" id="totalRevenue">Rp0</div></div><div class="stat-icon"><i class="fas fa-chart-line"></i></div></div>
            <div class="stat-card"><div class="stat-info"><h3>Total Pesanan</h3><div class="stat-number" id="totalOrders">0</div></div><div class="stat-icon"><i class="fas fa-receipt"></i></div></div>
            <div class="stat-card"><div class="stat-info"><h3>Total Produk</h3><div class="stat-number" id="totalProducts">0</div></div><div class="stat-icon"><i class="fas fa-box"></i></div></div>
            <div class="stat-card"><div class="stat-info"><h3>Stok Rendah</h3><div class="stat-number" id="lowStockCount">0</div></div><div class="stat-icon"><i class="fas fa-exclamation-triangle"></i></div></div>
        </div>
        <div class="insight-row">
            <div class="chart-box"><div class="section-title"><i class="fas fa-chart-simple"></i> Penjualan 7 Hari Terakhir (WIB)</div><canvas id="salesChart" height="200"></canvas></div>
            <div class="recent-orders"><div class="section-title"><i class="fas fa-clock"></i> Pesanan Terbaru (WIB)</div><div id="ordersList"><div style="padding:20px; text-align:center;">Belum ada pesanan</div></div></div>
        </div>
    </div>

    <div id="productsSection" style="display:none;">
        <div class="crud-header">
            <div class="section-title"><i class="fas fa-pen-ruler"></i> Daftar Produk</div>
            <div style="display: flex; gap:12px;">
                <div class="search-box"><i class="fas fa-search"></i><input type="text" id="searchProduct" placeholder="Cari produk..."></div>
                <button class="btn-primary" id="openProductModalBtn"><i class="fas fa-plus-circle"></i> Tambah Produk</button>
            </div>
        </div>
        <div class="table-wrapper"><table id="productTable"><thead><tr><th>Nama Produk</th><th>Stok</th><th>Harga (Rp)</th><th>Aksi</th></tr></thead><tbody id="productTableBody"></tbody></table></div>
    </div>

    <div id="ordersSection" style="display:none;">
        <div class="crud-header">
            <div class="section-title"><i class="fas fa-truck"></i> Daftar Pesanan</div>
            <div style="display: flex; gap:12px;">
                <div class="search-box"><i class="fas fa-search"></i><input type="text" id="searchOrder" placeholder="Cari ID / pelanggan..."></div>
                <button class="btn-primary" id="openOrderModalBtn"><i class="fas fa-plus-circle"></i> Tambah Pesanan</button>
            </div>
        </div>
        <div class="table-wrapper"><table id="ordersTable"><thead><tr><th>ID Pesanan</th><th>Pelanggan</th><th>Total (Rp)</th><th>Status</th><th>Tanggal (WIB)</th><th>Aksi</th></tr></thead><tbody id="ordersTableBody"></tbody></table></div>
    </div>
    <footer>© 2025 Aneka - Tanggal otomatis WIB, Grafik dinamis berdasarkan data riil | Data tersimpan di localStorage</footer>
</div>
</div>

<div id="productModal" class="modal"><div class="modal-card"><h3 id="productModalTitle">Tambah Produk</h3><input type="text" id="prodName" placeholder="Nama Produk"><input type="number" id="prodStock" placeholder="Stok"><input type="number" id="prodPrice" placeholder="Harga (Rp)"><div class="modal-actions"><button class="btn-cancel" id="closeProductModal">Batal</button><button class="btn-save" id="saveProductBtn">Simpan</button></div></div></div>

<div id="orderModal" class="modal"><div class="modal-card"><h3 id="orderModalTitle">Tambah Pesanan</h3><input type="text" id="orderCustomer" placeholder="Nama Pelanggan"><input type="number" id="orderTotal" placeholder="Total (Rp)"><select id="orderStatus"><option value="Selesai">Selesai</option><option value="Diproses">Diproses</option><option value="Dikirim">Dikirim</option></select><input type="date" id="orderDate" placeholder="Tanggal"><div class="modal-actions"><button class="btn-cancel" id="closeOrderModal">Batal</button><button class="btn-save" id="saveOrderBtn">Simpan</button></div></div></div>

<script>
    // ========== FUNGSI TANGGAL WIB (Asia/Jakarta) ==========
    function getCurrentWIBDate() {
        // Menggunakan opsi timezone untuk mendapatkan tanggal dalam WIB
        const now = new Date();
        const options = { timeZone: 'Asia/Jakarta', year: 'numeric', month: '2-digit', day: '2-digit' };
        const formatter = new Intl.DateTimeFormat('id-ID', options);
        const parts = formatter.formatToParts(now);
        let day = '', month = '', year = '';
        for (const part of parts) {
            if (part.type === 'day') day = part.value;
            if (part.type === 'month') month = part.value;
            if (part.type === 'year') year = part.value;
        }
        return `${year}-${month}-${day}`;
    }

    function formatDateForDisplay(dateStr) {
        if (!dateStr) return '-';
        const parts = dateStr.split('-');
        if (parts.length === 3) return `${parts[2]}/${parts[1]}/${parts[0]}`;
        return dateStr;
    }

    // ========== STORAGE KEYS ==========
    const STORAGE = {
        PRODUCTS: 'aneka_products',
        ORDERS: 'aneka_orders',
        NEXT_PRODUCT_ID: 'aneka_nextProductId',
        NEXT_ORDER_NUM: 'aneka_nextOrderNum'
    };

    let products = [];
    let nextProductId = 1;
    let orders = [];
    let nextOrderIdNum = 1;

    function loadData() {
        const savedProducts = localStorage.getItem(STORAGE.PRODUCTS);
        products = savedProducts ? JSON.parse(savedProducts) : [];
        const savedOrders = localStorage.getItem(STORAGE.ORDERS);
        orders = savedOrders ? JSON.parse(savedOrders) : [];
        nextProductId = parseInt(localStorage.getItem(STORAGE.NEXT_PRODUCT_ID) || '1');
        nextOrderIdNum = parseInt(localStorage.getItem(STORAGE.NEXT_ORDER_NUM) || '1');
    }
    function persistData() {
        localStorage.setItem(STORAGE.PRODUCTS, JSON.stringify(products));
        localStorage.setItem(STORAGE.ORDERS, JSON.stringify(orders));
        localStorage.setItem(STORAGE.NEXT_PRODUCT_ID, nextProductId.toString());
        localStorage.setItem(STORAGE.NEXT_ORDER_NUM, nextOrderIdNum.toString());
    }

    function generateOrderId() { return `ORD${String(nextOrderIdNum).padStart(3,'0')}`; }

    // ========== GRAFIK DINAMIS BERDASARKAN DATA PESANAN ==========
    let salesChart;
    function updateChart() {
        const todayWIB = getCurrentWIBDate();
        const today = new Date(todayWIB);
        const last7Days = [];
        for (let i = 6; i >= 0; i--) {
            const d = new Date(today);
            d.setDate(today.getDate() - i);
            last7Days.push(d.toISOString().slice(0,10));
        }
        const dailyTotal = {};
        last7Days.forEach(date => { dailyTotal[date] = 0; });
        orders.forEach(order => {
            if (order.date && dailyTotal[order.date] !== undefined) {
                dailyTotal[order.date] += order.total;
            }
        });
        const labels = last7Days.map(d => {
            const parts = d.split('-');
            return `${parts[2]}/${parts[1]}`;
        });
        const data = last7Days.map(d => dailyTotal[d]);

        if (salesChart) {
            salesChart.data.labels = labels;
            salesChart.data.datasets[0].data = data;
            salesChart.update();
        } else {
            const ctx = document.getElementById('salesChart').getContext('2d');
            salesChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Pendapatan (Rp)',
                        data: data,
                        borderColor: '#2c3e66',
                        backgroundColor: 'rgba(44,62,102,0.1)',
                        tension: 0.3,
                        fill: true
                    }]
                },
                options: { responsive: true, maintainAspectRatio: true }
            });
        }
    }

    // ========== UPDATE STATISTIK DASHBOARD ==========
    function updateDashboardStats() {
        const totalProd = products.length;
        const lowStock = products.filter(p => p.stock < 10).length;
        const totalOrd = orders.reduce((sum, o) => sum + o.total, 0);
        document.getElementById('totalProducts').innerText = totalProd;
        document.getElementById('lowStockCount').innerText = lowStock;
        document.getElementById('totalRevenue').innerText = `Rp${totalOrd.toLocaleString('id-ID')}`;
        document.getElementById('totalOrders').innerText = orders.length;
        
        // Urutkan pesanan terbaru berdasarkan tanggal (descending)
        const latestOrders = [...orders].sort((a,b) => (b.date || '').localeCompare(a.date || '')).slice(0,4);
        const ordersListDiv = document.getElementById('ordersList');
        if (ordersListDiv) {
            if (latestOrders.length === 0) ordersListDiv.innerHTML = '<div style="padding:20px; text-align:center; color:var(--text-secondary);">Belum ada pesanan</div>';
            else {
                ordersListDiv.innerHTML = latestOrders.map(o => `
                    <div class="order-item">
                        <div><span class="order-id">${o.id}</span><br><small style="color:var(--text-secondary)">${escapeHtml(o.customer)}</small><br><small>${formatDateForDisplay(o.date)}</small></div>
                        <div class="order-total">Rp${o.total.toLocaleString('id-ID')}</div>
                        <div><span class="badge ${o.status === 'Diproses' ? 'warning' : (o.status === 'Dikirim' ? 'info' : '')}">${o.status}</span></div>
                    </div>
                `).join('');
            }
        }
        updateChart();
    }

    // ========== CRUD PRODUK ==========
    function renderProducts() {
        const filter = document.getElementById('searchProduct')?.value.toLowerCase() || '';
        const filtered = products.filter(p => p.name.toLowerCase().includes(filter));
        const tbody = document.getElementById('productTableBody');
        if (!tbody) return;
        if (filtered.length === 0) { tbody.innerHTML = '<tr><td colspan="4">Belum ada produk. Klik "Tambah Produk"</td></tr>'; return; }
        tbody.innerHTML = filtered.map(p => `
            <tr class="${p.stock < 10 ? 'low-stock' : ''}">
                <td><i class="fas fa-tag"></i> ${escapeHtml(p.name)}</td>
                <td>${p.stock} ${p.stock < 10 ? '<i class="fas fa-exclamation-circle" style="color:#e67e22;"></i>' : ''}</td>
                <td>Rp${p.price.toLocaleString('id-ID')}</td>
                <td><button class="btn-action btn-edit" data-id="${p.id}" data-type="product"><i class="fas fa-edit"></i></button>
                    <button class="btn-action btn-delete" data-id="${p.id}" data-type="product"><i class="fas fa-trash-alt"></i></button></td>
            </tr>
        `).join('');
        attachProductEvents();
    }
    function attachProductEvents() {
        document.querySelectorAll('[data-type="product"].btn-edit').forEach(btn => btn.addEventListener('click', handleProductEdit));
        document.querySelectorAll('[data-type="product"].btn-delete').forEach(btn => btn.addEventListener('click', handleProductDelete));
    }
    function handleProductEdit(e) {
        const id = parseInt(e.currentTarget.getAttribute('data-id'));
        const prod = products.find(p => p.id === id);
        if (prod) {
            document.getElementById('productModalTitle').innerText = "Edit Produk";
            document.getElementById('prodName').value = prod.name;
            document.getElementById('prodStock').value = prod.stock;
            document.getElementById('prodPrice').value = prod.price;
            window.currentProductId = id;
            document.getElementById('productModal').style.display = 'flex';
        }
    }
    function handleProductDelete(e) {
        const id = parseInt(e.currentTarget.getAttribute('data-id'));
        if (confirm("Hapus produk ini?")) {
            products = products.filter(p => p.id !== id);
            persistData();
            renderProducts();
            updateDashboardStats();
        }
    }
    function saveProduct() {
        const name = document.getElementById('prodName').value.trim();
        const stock = parseInt(document.getElementById('prodStock').value);
        const price = parseInt(document.getElementById('prodPrice').value);
        if (!name || isNaN(stock) || isNaN(price) || stock < 0 || price < 0) { alert("Isi data dengan benar"); return; }
        if (window.currentProductId !== undefined) {
            const idx = products.findIndex(p => p.id === window.currentProductId);
            if (idx !== -1) products[idx] = { ...products[idx], name, stock, price };
            window.currentProductId = undefined;
        } else {
            products.push({ id: nextProductId++, name, stock, price });
        }
        persistData();
        closeProductModal();
        renderProducts();
        updateDashboardStats();
    }
    function openProductModal() { window.currentProductId = undefined; document.getElementById('productModalTitle').innerText = "Tambah Produk"; document.getElementById('prodName').value = ''; document.getElementById('prodStock').value = ''; document.getElementById('prodPrice').value = ''; document.getElementById('productModal').style.display = 'flex'; }
    function closeProductModal() { document.getElementById('productModal').style.display = 'none'; }

    // ========== CRUD PESANAN DENGAN TANGGAL WIB ==========
    function renderOrders() {
        const filter = document.getElementById('searchOrder')?.value.toLowerCase() || '';
        const filtered = orders.filter(o => o.id.toLowerCase().includes(filter) || o.customer.toLowerCase().includes(filter));
        const tbody = document.getElementById('ordersTableBody');
        if (!tbody) return;
        if (filtered.length === 0) { tbody.innerHTML = '<tr><td colspan="6">Belum ada pesanan. Klik "Tambah Pesanan"</td></tr>'; return; }
        tbody.innerHTML = filtered.map(o => `
            <tr>
                <td>${o.id}</td>
                <td>${escapeHtml(o.customer)}</td>
                <td>Rp${o.total.toLocaleString('id-ID')}</td>
                <td><span class="badge ${o.status === 'Diproses' ? 'warning' : (o.status === 'Dikirim' ? 'info' : '')}">${o.status}</span></td>
                <td>${formatDateForDisplay(o.date)}</td>
                <td><button class="btn-action btn-edit" data-id="${o.id}" data-type="order"><i class="fas fa-edit"></i></button>
                    <button class="btn-action btn-delete" data-id="${o.id}" data-type="order"><i class="fas fa-trash-alt"></i></button></td>
            </tr>
        `).join('');
        attachOrderEvents();
    }
    function attachOrderEvents() {
        document.querySelectorAll('[data-type="order"].btn-edit').forEach(btn => btn.addEventListener('click', handleOrderEdit));
        document.querySelectorAll('[data-type="order"].btn-delete').forEach(btn => btn.addEventListener('click', handleOrderDelete));
    }
    function handleOrderEdit(e) {
        const id = e.currentTarget.getAttribute('data-id');
        const order = orders.find(o => o.id === id);
        if (order) {
            document.getElementById('orderModalTitle').innerText = "Edit Pesanan";
            document.getElementById('orderCustomer').value = order.customer;
            document.getElementById('orderTotal').value = order.total;
            document.getElementById('orderStatus').value = order.status;
            document.getElementById('orderDate').value = order.date || getCurrentWIBDate();
            window.currentOrderId = id;
            document.getElementById('orderModal').style.display = 'flex';
        }
    }
    function handleOrderDelete(e) {
        const id = e.currentTarget.getAttribute('data-id');
        if (confirm("Hapus pesanan ini?")) {
            orders = orders.filter(o => o.id !== id);
            persistData();
            renderOrders();
            updateDashboardStats();
        }
    }
    function saveOrder() {
        const customer = document.getElementById('orderCustomer').value.trim();
        const total = parseInt(document.getElementById('orderTotal').value);
        const status = document.getElementById('orderStatus').value;
        let date = document.getElementById('orderDate').value;
        if (!date) date = getCurrentWIBDate();
        if (!customer || isNaN(total) || total <= 0) { alert("Nama pelanggan dan total valid diperlukan"); return; }
        if (window.currentOrderId) {
            const idx = orders.findIndex(o => o.id === window.currentOrderId);
            if (idx !== -1) orders[idx] = { ...orders[idx], customer, total, status, date };
            window.currentOrderId = undefined;
        } else {
            const newId = generateOrderId();
            orders.push({ id: newId, customer, total, status, date });
            nextOrderIdNum++;
        }
        persistData();
        closeOrderModal();
        renderOrders();
        updateDashboardStats();
    }
    function openOrderModal() {
        window.currentOrderId = undefined;
        document.getElementById('orderModalTitle').innerText = "Tambah Pesanan";
        document.getElementById('orderCustomer').value = '';
        document.getElementById('orderTotal').value = '';
        document.getElementById('orderStatus').value = "Selesai";
        document.getElementById('orderDate').value = getCurrentWIBDate();
        document.getElementById('orderModal').style.display = 'flex';
    }
    function closeOrderModal() { document.getElementById('orderModal').style.display = 'none'; }

    // ========== DARK MODE & PARTIKEL ==========
    function createParticleBurst() {
        for (let i = 0; i < 50; i++) {
            const p = document.createElement('div');
            p.classList.add('particle');
            p.style.left = Math.random() * window.innerWidth + 'px';
            p.style.top = Math.random() * window.innerHeight + 'px';
            p.style.background = ['#3b82f6', '#60a5fa', '#1e3a8a', '#38bdf8'][Math.floor(Math.random()*4)];
            p.style.animationDuration = Math.random() * 0.8 + 0.8 + 's';
            document.body.appendChild(p);
            setTimeout(() => p.remove(), 1200);
        }
    }
    function initDarkMode() {
        const toggle = document.getElementById('darkModeToggle');
        const themeSpan = document.getElementById('themeText');
        const isDark = localStorage.getItem('anekaTheme') === 'dark';
        if (isDark) { document.body.classList.add('dark'); themeSpan.innerText = 'Mode Terang'; toggle.innerHTML = '<i class="fas fa-sun"></i> <span id="themeText">Mode Terang</span>'; }
        else { document.body.classList.remove('dark'); themeSpan.innerText = 'Mode Gelap'; toggle.innerHTML = '<i class="fas fa-moon"></i> <span id="themeText">Mode Gelap</span>'; }
        toggle.addEventListener('click', () => {
            createParticleBurst();
            if (document.body.classList.contains('dark')) {
                document.body.classList.remove('dark');
                localStorage.setItem('anekaTheme', 'light');
                toggle.innerHTML = '<i class="fas fa-moon"></i> <span id="themeText">Mode Gelap</span>';
            } else {
                document.body.classList.add('dark');
                localStorage.setItem('anekaTheme', 'dark');
                toggle.innerHTML = '<i class="fas fa-sun"></i> <span id="themeText">Mode Terang</span>';
            }
        });
    }

    // ========== NAVIGASI ==========
    function showSection(section) {
        document.getElementById('dashboardSection').style.display = 'none';
        document.getElementById('productsSection').style.display = 'none';
        document.getElementById('ordersSection').style.display = 'none';
        if (section === 'dashboard') { document.getElementById('dashboardSection').style.display = 'block'; document.getElementById('mainTitle').innerText = 'Dashboard Admin'; updateDashboardStats(); }
        else if (section === 'products') { document.getElementById('productsSection').style.display = 'block'; document.getElementById('mainTitle').innerText = 'Manajemen Produk'; renderProducts(); }
        else if (section === 'orders') { document.getElementById('ordersSection').style.display = 'block'; document.getElementById('mainTitle').innerText = 'Manajemen Pesanan'; renderOrders(); }
        document.querySelectorAll('.nav-item').forEach(item => { if (item.getAttribute('data-section') === section) item.classList.add('active'); else item.classList.remove('active'); });
    }

    function attachGlobalEvents() {
        document.querySelectorAll('.nav-item').forEach(nav => nav.addEventListener('click', () => showSection(nav.getAttribute('data-section'))));
        document.getElementById('openProductModalBtn')?.addEventListener('click', openProductModal);
        document.getElementById('closeProductModal')?.addEventListener('click', closeProductModal);
        document.getElementById('saveProductBtn')?.addEventListener('click', saveProduct);
        document.getElementById('openOrderModalBtn')?.addEventListener('click', openOrderModal);
        document.getElementById('closeOrderModal')?.addEventListener('click', closeOrderModal);
        document.getElementById('saveOrderBtn')?.addEventListener('click', saveOrder);
        window.addEventListener('click', (e) => { if (e.target.classList.contains('modal')) { closeProductModal(); closeOrderModal(); } });
        document.getElementById('searchProduct')?.addEventListener('input', () => renderProducts());
        document.getElementById('searchOrder')?.addEventListener('input', () => renderOrders());
    }

    // ========== LOGIN ==========
    function initLogin() {
        const overlay = document.getElementById('loginOverlay');
        const app = document.getElementById('appContent');
        if (sessionStorage.getItem('aneka_logged_in') === 'true') {
            overlay.style.display = 'none';
            app.style.display = 'flex';
            loadData();
            updateDashboardStats();
            renderProducts();
            renderOrders();
            initDarkMode();
            attachGlobalEvents();
            showSection('dashboard');
            return;
        }
        document.getElementById('loginBtn').addEventListener('click', () => {
            const user = document.getElementById('loginUsername').value.trim();
            const pass = document.getElementById('loginPassword').value.trim();
            if (user === 'admin' && pass === '123') {
                createParticleBurst();
                sessionStorage.setItem('aneka_logged_in', 'true');
                overlay.style.opacity = '0';
                setTimeout(() => {
                    overlay.style.display = 'none';
                    app.style.display = 'flex';
                    loadData();
                    updateDashboardStats();
                    renderProducts();
                    renderOrders();
                    initDarkMode();
                    attachGlobalEvents();
                    showSection('dashboard');
                }, 500);
            } else {
                document.getElementById('loginError').innerText = '❌ Username atau password salah! (admin / 123)';
            }
        });
    }

    function escapeHtml(str) { return str.replace(/[&<>]/g, function(m){ if(m==='&') return '&amp;'; if(m==='<') return '&lt;'; if(m==='>') return '&gt;'; return m;}); }

    window.addEventListener('DOMContentLoaded', initLogin);
</script>
</body>
</html>