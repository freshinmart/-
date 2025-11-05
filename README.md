<html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Buku Catatan Hutang - Sistem Gudang</title>
    <style>
        :root {
            --primary: #4a6fa5;
            --secondary: #6b8cbc;
            --success: #28a745;
            --danger: #dc3545;
            --warning: #ffc107;
            --light: #f8f9fa;
            --dark: #343a40;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f5f5;
            color: var(--dark);
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            background-color: var(--primary);
            color: white;
            padding: 20px 0;
            text-align: center;
            border-radius: 8px 8px 0 0;
            margin-bottom: 20px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        h1 {
            font-size: 2rem;
        }
        
        .card {
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            padding: 20px;
            margin-bottom: 20px;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
        }
        
        input, textarea, button, select {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 1rem;
        }
        
        button {
            background-color: var(--primary);
            color: white;
            border: none;
            cursor: pointer;
            font-weight: 500;
            transition: background-color 0.3s;
        }
        
        button:hover {
            background-color: var(--secondary);
        }
        
        .btn-success {
            background-color: var(--success);
        }
        
        .btn-success:hover {
            background-color: #218838;
        }
        
        .btn-danger {
            background-color: var(--danger);
        }
        
        .btn-danger:hover {
            background-color: #c82333;
        }
        
        .btn-warning {
            background-color: var(--warning);
            color: var(--dark);
        }
        
        .btn-warning:hover {
            background-color: #e0a800;
        }
        
        .debt-list {
            margin-top: 20px;
        }
        
        .debtor-group {
            border: 1px solid #e0e0e0;
            border-radius: 8px;
            margin-bottom: 15px;
            overflow: hidden;
        }
        
        .debtor-header {
            background-color: #f8f9fa;
            padding: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        .debtor-header:hover {
            background-color: #e9ecef;
        }
        
        .debtor-info {
            display: flex;
            flex-direction: column;
        }
        
        .debtor-name {
            font-weight: 600;
            font-size: 1.2rem;
        }
        
        .debtor-summary {
            color: #6c757d;
            font-size: 0.9rem;
        }
        
        .debtor-amount {
            font-size: 1.3rem;
            font-weight: 700;
            color: var(--danger);
        }
        
        .debt-status {
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 500;
        }
        
        .status-pending {
            background-color: #ffeaa7;
            color: #e17055;
        }
        
        .status-paid {
            background-color: #b8e994;
            color: #079992;
        }
        
        .debtor-details {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.3s ease-out;
            background-color: white;
        }
        
        .debtor-details.expanded {
            max-height: 1000px;
        }
        
        .debt-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 15px;
            border-bottom: 1px solid #eee;
            position: relative;
        }
        
        .debt-item:last-child {
            border-bottom: none;
        }
        
        .debt-info {
            flex: 1;
        }
        
        .debt-product {
            font-weight: 500;
        }
        
        .debt-amount {
            font-size: 1.1rem;
            font-weight: 600;
            color: var(--danger);
        }
        
        .debt-date {
            font-size: 0.85rem;
            color: #6c757d;
        }
        
        .debt-actions {
            display: flex;
            gap: 8px;
        }
        
        .btn-small {
            width: auto;
            padding: 5px 10px;
            font-size: 0.85rem;
        }
        
        .paid-stamp {
            position: absolute;
            transform: rotate(-15deg);
            color: var(--success);
            font-weight: bold;
            font-size: 1.8rem;
            opacity: 0.7;
            pointer-events: none;
            z-index: 1;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) rotate(-15deg);
        }
        
        .tab-container {
            display: flex;
            margin-bottom: 15px;
            border-bottom: 1px solid #ddd;
        }
        
        .tab {
            padding: 10px 15px;
            cursor: pointer;
            border-bottom: 2px solid transparent;
        }
        
        .tab.active {
            border-bottom: 2px solid var(--primary);
            font-weight: 500;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        
        .modal-content {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            width: 90%;
            max-width: 600px;
            max-height: 90vh;
            overflow-y: auto;
            box-shadow: 0 4px 20px rgba(0,0,0,0.15);
        }
        
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid #eee;
        }
        
        .close-modal {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            width: auto;
            color: var(--dark);
        }
        
        .notification {
            position: fixed;
            bottom: 20px;
            right: 20px;
            padding: 15px 20px;
            background-color: var(--primary);
            color: white;
            border-radius: 4px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.2);
            display: none;
            z-index: 1001;
            animation: slideIn 0.3s ease-out;
        }
        
        @keyframes slideIn {
            from {
                transform: translateX(100%);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }
        
        .signature-container {
            border: 1px dashed #ccc;
            border-radius: 4px;
            padding: 15px;
            margin-top: 10px;
            text-align: center;
        }
        
        .signature-preview {
            max-width: 100%;
            max-height: 150px;
            margin-top: 10px;
            display: none;
        }
        
        .document-preview {
            border: 1px solid #ddd;
            padding: 20px;
            margin-top: 15px;
            background-color: white;
            min-height: 400px;
        }
        
        .document-actions {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }
        
        .debtor-actions-header {
            display: flex;
            gap: 10px;
        }
        
        .document-form {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-top: 15px;
        }
        
        .document-form-section {
            grid-column: span 2;
            border: 1px solid #eee;
            padding: 15px;
            border-radius: 8px;
        }
        
        .document-form-section h3 {
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid #eee;
        }
        
        .camera-container {
            position: relative;
            margin-top: 10px;
        }
        
        #camera-preview {
            width: 100%;
            max-width: 300px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        
        .camera-controls {
            margin-top: 10px;
            display: flex;
            gap: 10px;
        }
        
        .signature-options {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }
        
        .signature-option {
            flex: 1;
        }
        
        .signature-box {
            margin-top: 10px;
            padding-top: 10px;
            border-top: 1px solid #eee;
        }
        
        .product-input-group {
            display: flex;
            gap: 10px;
            margin-bottom: 10px;
        }
        
        .product-input {
            flex: 1;
        }
        
        .add-product-btn {
            width: 50px;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: var(--success);
        }
        
        .product-list {
            margin-top: 15px;
            border: 1px solid #eee;
            border-radius: 4px;
            max-height: 200px;
            overflow-y: auto;
        }
        
        .product-item {
            display: flex;
            justify-content: space-between;
            padding: 10px;
            border-bottom: 1px solid #eee;
        }
        
        .product-item:last-child {
            border-bottom: none;
        }
        
        .product-actions {
            display: flex;
            gap: 5px;
        }
        
        .btn-icon {
            width: 30px;
            height: 30px;
            padding: 0;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .total-amount {
            margin-top: 15px;
            padding: 10px;
            background-color: #f8f9fa;
            border-radius: 4px;
            text-align: right;
            font-weight: bold;
        }
        
        /* Tambahan CSS untuk gudang dan scanner */
        .barcode-scanner-container {
            border: 1px dashed #ccc;
            border-radius: 4px;
            padding: 15px;
            margin-top: 10px;
            text-align: center;
        }
        
        .barcode-preview {
            width: 100%;
            max-width: 300px;
            border: 1px solid #ddd;
            border-radius: 4px;
            margin: 10px auto;
        }
        
        .warehouse-product-list {
            margin-top: 15px;
            border: 1px solid #eee;
            border-radius: 4px;
            max-height: 400px;
            overflow-y: auto;
        }
        
        .warehouse-product-item {
            display: flex;
            justify-content: space-between;
            padding: 12px;
            border-bottom: 1px solid #eee;
            align-items: center;
        }
        
        .warehouse-product-item:last-child {
            border-bottom: none;
        }
        
        .product-barcode {
            font-family: monospace;
            background-color: #f8f9fa;
            padding: 2px 6px;
            border-radius: 4px;
            font-size: 0.85rem;
        }
        
        .scan-status {
            padding: 8px;
            border-radius: 4px;
            margin-top: 10px;
            text-align: center;
            font-weight: 500;
        }
        
        .scan-success {
            background-color: #d4edda;
            color: #155724;
        }
        
        .scan-error {
            background-color: #f8d7da;
            color: #721c24;
        }
        
        .scanner-active {
            border: 2px solid var(--success);
        }
        
        .barcode-scanner-video {
            width: 100%;
            max-width: 400px;
            height: 300px;
            border-radius: 4px;
            background-color: #000;
            object-fit: cover;
        }
        
        .scanner-overlay {
            position: relative;
            display: inline-block;
        }
        
        .scanner-frame {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 80%;
            height: 150px;
            border: 2px solid #00ff00;
            box-shadow: 0 0 0 1000px rgba(0, 0, 0, 0.5);
            z-index: 1;
        }
        
        .scanner-guide {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: white;
            text-align: center;
            z-index: 2;
            font-weight: bold;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.7);
        }
        
        .scanner-result {
            margin-top: 15px;
            padding: 10px;
            background-color: #f8f9fa;
            border-radius: 4px;
            text-align: center;
        }
        
        .barcode-value {
            font-family: monospace;
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--success);
        }
        
        @media (max-width: 768px) {
            .debtor-header {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .debtor-amount {
                margin-top: 10px;
            }
            
            .debt-item {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .debt-actions {
                margin-top: 10px;
                width: 100%;
                justify-content: space-between;
            }
            
            .btn-small {
                flex: 1;
            }
            
            .tab-container {
                flex-wrap: wrap;
            }
            
            .tab {
                flex: 1;
                text-align: center;
            }
            
            .document-actions, .debtor-actions-header {
                flex-direction: column;
            }
            
            .document-form {
                grid-template-columns: 1fr;
            }
            
            .document-form-section {
                grid-column: span 1;
            }
            
            .signature-options {
                flex-direction: column;
            }
            
            .product-input-group {
                flex-direction: column;
            }
            
            .add-product-btn {
                width: 100%;
            }
            
            .barcode-scanner-video {
                height: 250px;
            }
        }
    </style>
    <!-- QuaggaJS for barcode scanning -->
    <script src="https://cdn.jsdelivr.net/npm/quagga@0.12.1/dist/quagga.min.js"></script>
</head>
<body>
    <div class="container">
        <header>
            <h1>Buku Catatan Hutang - Sistem Gudang</h1>
        </header>
        
        <div class="card">
            <div class="tab-container">
                <div class="tab active" data-tab="add-debt">Tambah Hutang</div>
                <div class="tab" data-tab="debt-list">Daftar Hutang</div>
                <div class="tab" data-tab="warehouse">Gudang</div>
                <div class="tab" data-tab="documents">Dokumen</div>
            </div>
            
            <div class="tab-content active" id="add-debt">
                <h2>Tambah Hutang Baru</h2>
                <form id="debt-form">
                    <div class="form-group">
                        <label for="debtor-name">Nama Peminjam</label>
                        <input type="text" id="debtor-name" required placeholder="Masukkan nama peminjam">
                    </div>
                    
                    <!-- Scanner Kode Batang -->
                    <div class="form-group">
                        <label>Scan Kode Batang Produk</label>
                        <div class="barcode-scanner-container" id="barcode-scanner">
                            <p>Klik untuk membuka kamera dan scan kode batang</p>
                            <button type="button" id="start-barcode-scanner" class="btn-warning">Mulai Scan</button>
                            <div class="camera-container" style="display:none;" id="barcode-camera-container">
                                <div class="scanner-overlay">
                                    <video id="barcode-scanner-video" class="barcode-scanner-video" autoplay playsinline></video>
                                    <div class="scanner-frame"></div>
                                    <div class="scanner-guide">Arahkan kode batang ke dalam area ini</div>
                                </div>
                            </div>
                            <div class="camera-controls" id="barcode-camera-controls" style="display:none;">
                                <button type="button" id="stop-barcode-scanner" class="btn-danger">Stop Scan</button>
                            </div>
                            <div id="scan-status" class="scan-status" style="display:none;"></div>
                            <div id="scanner-result" class="scanner-result" style="display:none;">
                                <p>Kode Batang: <span id="scanned-barcode" class="barcode-value"></span></p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label>Daftar Produk</label>
                        <div class="product-list" id="product-list">
                            <!-- Daftar produk akan ditampilkan di sini -->
                        </div>
                        
                        <div class="total-amount">
                            Total Hutang: <span id="total-amount">Rp 0</span>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label for="debt-date">Tanggal Hutang</label>
                        <input type="date" id="debt-date" required>
                    </div>
                    
                    <div class="form-group">
                        <label for="due-date">Tanggal Jatuh Tempo</label>
                        <input type="date" id="due-date">
                    </div>
                    
                    <button type="submit" id="add-debt-btn">Tambah Hutang</button>
                </form>
            </div>
            
            <div class="tab-content" id="debt-list">
                <h2>Daftar Hutang Berdasarkan Peminjam</h2>
                <div id="debtors-list" class="debt-list">
                    <!-- Daftar peminjam akan ditampilkan di sini -->
                </div>
            </div>
            
            <!-- Tab Gudang -->
            <div class="tab-content" id="warehouse">
                <h2>Manajemen Gudang</h2>
                <div class="card">
                    <h3>Tambah Produk ke Gudang</h3>
                    <form id="warehouse-form">
                        <div class="form-group">
                            <label for="product-name-warehouse">Nama Produk</label>
                            <input type="text" id="product-name-warehouse" required placeholder="Masukkan nama produk">
                        </div>
                        
                        <div class="form-group">
                            <label for="product-price-warehouse">Harga</label>
                            <input type="text" id="product-price-warehouse" required placeholder="Masukkan harga (contoh: 100.000)">
                        </div>
                        
                        <div class="form-group">
                            <label for="product-barcode-warehouse">Kode Batang (Barcode)</label>
                            <div class="product-input-group">
                                <input type="text" id="product-barcode-warehouse" class="product-input" placeholder="Masukkan kode batang">
                                <button type="button" id="generate-barcode" class="btn-warning">Generate</button>
                                <button type="button" id="scan-barcode-warehouse" class="btn-warning">Scan</button>
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <div id="barcode-preview-warehouse"></div>
                        </div>
                        
                        <button type="submit" id="add-product-warehouse">Tambah Produk ke Gudang</button>
                    </form>
                </div>
                
                <div class="card">
                    <h3>Daftar Produk di Gudang</h3>
                    <div id="warehouse-product-list" class="warehouse-product-list">
                        <!-- Daftar produk gudang akan ditampilkan di sini -->
                    </div>
                </div>
            </div>
            
            <div class="tab-content" id="documents">
                <h2>Dokumen Hutang</h2>
                <div class="form-group">
                    <label for="document-debtor">Pilih Peminjam</label>
                    <select id="document-debtor">
                        <option value="">-- Pilih Peminjam --</option>
                    </select>
                </div>
                
                <div class="document-form">
                    <div class="document-form-section">
                        <h3>Data Peminjam</h3>
                        <div class="form-group">
                            <label for="debtor-name-input">Nama Lengkap</label>
                            <input type="text" id="debtor-name-input" placeholder="Nama lengkap peminjam">
                        </div>
                        <div class="form-group">
                            <label for="debtor-address">Alamat</label>
                            <textarea id="debtor-address" placeholder="Alamat lengkap peminjam"></textarea>
                        </div>
                        <div class="form-group">
                            <label for="debtor-nik">NIK</label>
                            <input type="text" id="debtor-nik" placeholder="Nomor Induk Kependudukan">
                        </div>
                    </div>
                    
                    <div class="document-form-section">
                        <h3>Data Pemberi Pinjaman</h3>
                        <div class="form-group">
                            <label for="lender-name">Nama Lengkap</label>
                            <input type="text" id="lender-name" placeholder="Nama lengkap pemberi pinjaman">
                        </div>
                        <div class="form-group">
                            <label for="lender-address">Alamat</label>
                            <textarea id="lender-address" placeholder="Alamat lengkap pemberi pinjaman"></textarea>
                        </div>
                        <div class="form-group">
                            <label for="lender-nik">NIK</label>
                            <input type="text" id="lender-nik" placeholder="Nomor Induk Kependudukan">
                        </div>
                    </div>
                </div>
                
                <div class="document-actions">
                    <button id="generate-contract" class="btn-warning">Buat Surat Kontrak</button>
                    <button id="generate-bill" class="btn-warning">Buat Surat Tagihan</button>
                    <button id="generate-reminder" class="btn-warning">Buat Surat Peringatan</button>
                </div>
                
                <div class="document-preview" id="document-preview">
                    <p>Pilih peminjam dan jenis dokumen untuk melihat pratinjau</p>
                </div>
                
                <button id="print-document" class="btn-success">Cetak Dokumen</button>
            </div>
        </div>
    </div>
    
    <!-- Modal untuk scan kode batang di gudang -->
    <div id="barcode-modal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Scan Kode Batang</h3>
                <button class="close-modal">&times;</button>
            </div>
            <div class="form-group">
                <div class="camera-container">
                    <div class="scanner-overlay">
                        <video id="barcode-scanner-modal-video" class="barcode-scanner-video" autoplay playsinline></video>
                        <div class="scanner-frame"></div>
                        <div class="scanner-guide">Arahkan kode batang ke dalam area ini</div>
                    </div>
                </div>
                <div class="camera-controls">
                    <button id="stop-barcode-modal" class="btn-danger">Stop Scan</button>
                </div>
                <div id="barcode-modal-result" class="scanner-result" style="display:none;">
                    <p>Kode Batang: <span id="barcode-modal-value" class="barcode-value"></span></p>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Notifikasi -->
    <div id="notification" class="notification">
        <span id="notification-text"></span>
    </div>
    
    <script>
        // Data hutang
        let debts = JSON.parse(localStorage.getItem('debts')) || [];
        // Data gudang
        let warehouseProducts = JSON.parse(localStorage.getItem('warehouseProducts')) || [];
        const PASSWORD = '131313';
        
        // Variabel untuk produk
        let products = [];
        
        // Variabel untuk scanner
        let barcodeScannerActive = false;
        let barcodeScannerInstance = null;
        let barcodeModalScannerInstance = null;
        let currentStream = null;
        
        // Elemen DOM
        const debtForm = document.getElementById('debt-form');
        const debtorsList = document.getElementById('debtors-list');
        const documentDebtorSelect = document.getElementById('document-debtor');
        const documentPreview = document.getElementById('document-preview');
        const tabs = document.querySelectorAll('.tab');
        const tabContents = document.querySelectorAll('.tab-content');
        const notification = document.getElementById('notification');
        const notificationText = document.getElementById('notification-text');
        
        // Elemen untuk produk
        const productList = document.getElementById('product-list');
        const totalAmountSpan = document.getElementById('total-amount');
        
        // Elemen baru untuk gudang
        const warehouseForm = document.getElementById('warehouse-form');
        const productNameWarehouse = document.getElementById('product-name-warehouse');
        const productPriceWarehouse = document.getElementById('product-price-warehouse');
        const productBarcodeWarehouse = document.getElementById('product-barcode-warehouse');
        const generateBarcodeBtn = document.getElementById('generate-barcode');
        const scanBarcodeWarehouseBtn = document.getElementById('scan-barcode-warehouse');
        const barcodePreviewWarehouse = document.getElementById('barcode-preview-warehouse');
        const warehouseProductList = document.getElementById('warehouse-product-list');
        
        // Elemen untuk scanner kode batang
        const startBarcodeScannerBtn = document.getElementById('start-barcode-scanner');
        const stopBarcodeScannerBtn = document.getElementById('stop-barcode-scanner');
        const barcodeCameraContainer = document.getElementById('barcode-camera-container');
        const barcodeScannerVideo = document.getElementById('barcode-scanner-video');
        const scanStatus = document.getElementById('scan-status');
        const scannerResult = document.getElementById('scanner-result');
        const scannedBarcode = document.getElementById('scanned-barcode');
        
        // Elemen untuk modal barcode
        const barcodeModal = document.getElementById('barcode-modal');
        const barcodeScannerModalVideo = document.getElementById('barcode-scanner-modal-video');
        const stopBarcodeModalBtn = document.getElementById('stop-barcode-modal');
        const barcodeModalResult = document.getElementById('barcode-modal-result');
        const barcodeModalValue = document.getElementById('barcode-modal-value');
        
        // Format mata uang
        function formatCurrency(value) {
            return new Intl.NumberFormat('id-ID').format(value);
        }
        
        // Parse format mata uang
        function parseCurrency(value) {
            return parseInt(value.replace(/\./g, '')) || 0;
        }
        
        // Format input mata uang
        function formatCurrencyInput(input) {
            input.addEventListener('input', function(e) {
                let value = e.target.value.replace(/\./g, '');
                
                if (!isNaN(value)) {
                    e.target.value = formatCurrency(value);
                }
            });
        }
        
        // Hitung total harga produk
        function calculateTotal(products) {
            return products.reduce((total, product) => total + product.price, 0);
        }
        
        // Update tampilan total
        function updateTotal(products, totalElement) {
            const total = calculateTotal(products);
            totalElement.textContent = `Rp ${formatCurrency(total)}`;
            return total;
        }
        
        // Render daftar produk
        function renderProductList(products, container, onRemove) {
            container.innerHTML = '';
            
            if (products.length === 0) {
                container.innerHTML = '<div class="product-item" style="justify-content: center; color: #6c757d;">Belum ada produk</div>';
                return;
            }
            
            products.forEach((product, index) => {
                const productItem = document.createElement('div');
                productItem.className = 'product-item';
                productItem.innerHTML = `
                    <div>
                        <div>${product.name}</div>
                        <div style="font-size: 0.9rem; color: #6c757d;">Rp ${formatCurrency(product.price)}</div>
                    </div>
                    <div class="product-actions">
                        <button type="button" class="btn-danger btn-icon" data-index="${index}">×</button>
                    </div>
                `;
                
                container.appendChild(productItem);
                
                // Event listener untuk tombol hapus
                const removeBtn = productItem.querySelector('.btn-danger');
                removeBtn.addEventListener('click', function() {
                    onRemove(index);
                });
            });
        }
        
        // Event listeners
        document.addEventListener('DOMContentLoaded', function() {
            renderDebtors();
            populateDebtorSelect();
            formatCurrencyInput(productPriceWarehouse);
            
            // Set tanggal default
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('debt-date').value = today;
            
            // Set tanggal jatuh tempo default (30 hari dari sekarang)
            const dueDate = new Date();
            dueDate.setDate(dueDate.getDate() + 30);
            document.getElementById('due-date').value = dueDate.toISOString().split('T')[0];
            
            // Isi nama peminjam otomatis saat memilih dari dropdown
            documentDebtorSelect.addEventListener('change', function() {
                const selectedDebtor = this.value;
                if (selectedDebtor) {
                    document.getElementById('debtor-name-input').value = selectedDebtor;
                }
            });
            
            // Render daftar produk awal
            renderProductList(products, productList, removeProduct);
            updateTotal(products, totalAmountSpan);
            
            // Render daftar produk gudang
            renderWarehouseProducts();
        });
        
        debtForm.addEventListener('submit', addDebt);
        document.getElementById('generate-contract').addEventListener('click', generateContract);
        document.getElementById('generate-bill').addEventListener('click', generateBill);
        document.getElementById('generate-reminder').addEventListener('click', generateReminder);
        document.getElementById('print-document').addEventListener('click', printDocument);
        
        // Event listeners baru untuk gudang
        warehouseForm.addEventListener('submit', addProductToWarehouse);
        generateBarcodeBtn.addEventListener('click', generateBarcode);
        scanBarcodeWarehouseBtn.addEventListener('click', openBarcodeModal);
        startBarcodeScannerBtn.addEventListener('click', startBarcodeScanner);
        stopBarcodeScannerBtn.addEventListener('click', stopBarcodeScanner);
        stopBarcodeModalBtn.addEventListener('click', closeBarcodeModal);
        
        // Tab functionality
        tabs.forEach(tab => {
            tab.addEventListener('click', function() {
                const tabId = this.getAttribute('data-tab');
                
                tabs.forEach(t => t.classList.remove('active'));
                tabContents.forEach(tc => tc.classList.remove('active'));
                
                this.classList.add('active');
                document.getElementById(tabId).classList.add('active');
                
                if (tabId === 'debt-list') {
                    renderDebtors();
                } else if (tabId === 'documents') {
                    populateDebtorSelect();
                } else if (tabId === 'warehouse') {
                    renderWarehouseProducts();
                }
            });
        });
        
        // Fungsi untuk menampilkan produk di gudang
        function renderWarehouseProducts() {
            warehouseProductList.innerHTML = '';
            
            if (warehouseProducts.length === 0) {
                warehouseProductList.innerHTML = '<div class="warehouse-product-item" style="justify-content: center; color: #6c757d;">Belum ada produk di gudang</div>';
                return;
            }
            
            warehouseProducts.forEach((product, index) => {
                const productItem = document.createElement('div');
                productItem.className = 'warehouse-product-item';
                productItem.innerHTML = `
                    <div>
                        <div style="font-weight: 500;">${product.name}</div>
                        <div style="font-size: 0.9rem; color: #6c757d;">Rp ${formatCurrency(product.price)}</div>
                        ${product.barcode ? `<div class="product-barcode">${product.barcode}</div>` : ''}
                    </div>
                    <div class="product-actions">
                        <button type="button" class="btn-danger btn-icon" data-index="${index}">×</button>
                    </div>
                `;
                
                warehouseProductList.appendChild(productItem);
                
                // Event listener untuk tombol hapus
                const removeBtn = productItem.querySelector('.btn-danger');
                removeBtn.addEventListener('click', function() {
                    removeProductFromWarehouse(index);
                });
            });
        }
        
        // Fungsi untuk menambah produk ke gudang
        function addProductToWarehouse(e) {
            e.preventDefault();
            
            const name = productNameWarehouse.value.trim();
            const price = parseCurrency(productPriceWarehouse.value);
            const barcode = productBarcodeWarehouse.value.trim();
            
            if (!name) {
                alert('Nama produk harus diisi');
                return;
            }
            
            if (price <= 0) {
                alert('Harga produk harus diisi dengan benar');
                return;
            }
            
            // Cek apakah barcode sudah ada
            if (barcode && warehouseProducts.some(product => product.barcode === barcode)) {
                alert('Kode batang sudah digunakan oleh produk lain');
                return;
            }
            
            const newProduct = {
                id: Date.now(),
                name,
                price,
                barcode
            };
            
            warehouseProducts.push(newProduct);
            saveWarehouseProducts();
            renderWarehouseProducts();
            
            // Reset form
            warehouseForm.reset();
            barcodePreviewWarehouse.innerHTML = '';
            
            showNotification(`Produk ${name} berhasil ditambahkan ke gudang`);
        }
        
        // Fungsi untuk menghapus produk dari gudang
        function removeProductFromWarehouse(index) {
            if (confirm('Apakah Anda yakin ingin menghapus produk ini dari gudang?')) {
                warehouseProducts.splice(index, 1);
                saveWarehouseProducts();
                renderWarehouseProducts();
                showNotification('Produk berhasil dihapus dari gudang');
            }
        }
        
        // Fungsi untuk generate kode batang
        function generateBarcode() {
            // Generate random barcode (13 digit)
            const randomBarcode = Math.floor(1000000000000 + Math.random() * 9000000000000).toString();
            productBarcodeWarehouse.value = randomBarcode;
            
            // Tampilkan preview barcode (dalam bentuk teks untuk sekarang)
            barcodePreviewWarehouse.innerHTML = `
                <div style="text-align: center; margin-top: 10px;">
                    <div class="product-barcode" style="font-size: 1.2rem; padding: 10px; display: inline-block;">${randomBarcode}</div>
                </div>
            `;
        }
        
        // Fungsi untuk membuka modal scan barcode
        function openBarcodeModal() {
            barcodeModal.style.display = 'flex';
            startBarcodeModalScanner();
        }
        
        // Fungsi untuk menutup modal barcode
        function closeBarcodeModal() {
            barcodeModal.style.display = 'none';
            stopBarcodeModalScanner();
            barcodeModalResult.style.display = 'none';
        }
        
        // Fungsi untuk menghentikan kamera
        function stopCameraStream() {
            if (currentStream) {
                currentStream.getTracks().forEach(track => track.stop());
                currentStream = null;
            }
        }
        
        // Fungsi untuk memulai scanner barcode di modal
        async function startBarcodeModalScanner() {
            try {
                // Hentikan scanner sebelumnya jika ada
                if (barcodeModalScannerInstance) {
                    barcodeModalScannerInstance.stop();
                }
                
                // Hentikan kamera sebelumnya
                stopCameraStream();
                
                // Dapatkan akses ke kamera
                currentStream = await navigator.mediaDevices.getUserMedia({ 
                    video: { 
                        facingMode: "environment",
                        width: { ideal: 1280 },
                        height: { ideal: 720 }
                    } 
                });
                
                barcodeScannerModalVideo.srcObject = currentStream;
                
                // Tunggu hingga video siap
                barcodeScannerModalVideo.onloadedmetadata = function() {
                    // Inisialisasi Quagga setelah video siap
                    Quagga.init({
                        inputStream: {
                            name: "Live",
                            type: "LiveStream",
                            target: barcodeScannerModalVideo,
                            constraints: {
                                width: 640,
                                height: 480,
                                facingMode: "environment"
                            }
                        },
                        decoder: {
                            readers: [
                                "code_128_reader",
                                "ean_reader",
                                "ean_8_reader",
                                "code_39_reader",
                                "upc_reader",
                                "upc_e_reader"
                            ]
                        },
                        locator: {
                            patchSize: "medium",
                            halfSample: true
                        },
                        locate: true,
                        numOfWorkers: 2
                    }, function(err) {
                        if (err) {
                            console.error('Error initializing Quagga:', err);
                            alert('Tidak dapat mengakses kamera. Pastikan Anda memberikan izin akses kamera.');
                            return;
                        }
                        console.log('Quagga initialized successfully');
                        Quagga.start();
                        barcodeModalScannerInstance = Quagga;
                    });
                    
                    Quagga.onDetected(function(result) {
                        const code = result.codeResult.code;
                        barcodeModalValue.textContent = code;
                        barcodeModalResult.style.display = 'block';
                        
                        // Isi field barcode dengan hasil scan
                        productBarcodeWarehouse.value = code;
                        
                        // Tampilkan preview
                        barcodePreviewWarehouse.innerHTML = `
                            <div style="text-align: center; margin-top: 10px;">
                                <div class="product-barcode" style="font-size: 1.2rem; padding: 10px; display: inline-block;">${code}</div>
                            </div>
                        `;
                        
                        // Otomatis tutup modal setelah 2 detik
                        setTimeout(() => {
                            closeBarcodeModal();
                        }, 2000);
                    });
                };
            } catch (err) {
                console.error('Error accessing camera:', err);
                alert('Tidak dapat mengakses kamera. Pastikan Anda memberikan izin akses kamera.');
            }
        }
        
        // Fungsi untuk menghentikan scanner barcode di modal
        function stopBarcodeModalScanner() {
            if (barcodeModalScannerInstance) {
                barcodeModalScannerInstance.stop();
                barcodeModalScannerInstance = null;
            }
            stopCameraStream();
        }
        
        // Fungsi untuk memulai scanner barcode di tab tambah hutang
        async function startBarcodeScanner() {
            try {
                startBarcodeScannerBtn.style.display = 'none';
                barcodeCameraContainer.style.display = 'block';
                barcodeCameraControls.style.display = 'block';
                scanStatus.style.display = 'block';
                scanStatus.textContent = 'Mencari kode batang...';
                scanStatus.className = 'scan-status';
                scannerResult.style.display = 'none';
                
                // Hentikan scanner sebelumnya jika ada
                if (barcodeScannerInstance) {
                    barcodeScannerInstance.stop();
                }
                
                // Hentikan kamera sebelumnya
                stopCameraStream();
                
                // Dapatkan akses ke kamera
                currentStream = await navigator.mediaDevices.getUserMedia({ 
                    video: { 
                        facingMode: "environment",
                        width: { ideal: 1280 },
                        height: { ideal: 720 }
                    } 
                });
                
                barcodeScannerVideo.srcObject = currentStream;
                
                // Tunggu hingga video siap
                barcodeScannerVideo.onloadedmetadata = function() {
                    // Inisialisasi Quagga setelah video siap
                    Quagga.init({
                        inputStream: {
                            name: "Live",
                            type: "LiveStream",
                            target: barcodeScannerVideo,
                            constraints: {
                                width: 640,
                                height: 480,
                                facingMode: "environment"
                            }
                        },
                        decoder: {
                            readers: [
                                "code_128_reader",
                                "ean_reader",
                                "ean_8_reader",
                                "code_39_reader",
                                "upc_reader",
                                "upc_e_reader"
                            ]
                        },
                        locator: {
                            patchSize: "medium",
                            halfSample: true
                        },
                        locate: true,
                        numOfWorkers: 2
                    }, function(err) {
                        if (err) {
                            console.error('Error initializing Quagga:', err);
                            scanStatus.textContent = 'Error: Tidak dapat mengakses kamera';
                            scanStatus.className = 'scan-status scan-error';
                            startBarcodeScannerBtn.style.display = 'block';
                            barcodeCameraContainer.style.display = 'none';
                            barcodeCameraControls.style.display = 'none';
                            return;
                        }
                        console.log('Quagga initialized successfully');
                        Quagga.start();
                        barcodeScannerActive = true;
                        barcodeScannerInstance = Quagga;
                    });
                    
                    Quagga.onDetected(function(result) {
                        if (!barcodeScannerActive) return;
                        
                        const code = result.codeResult.code;
                        scannedBarcode.textContent = code;
                        scannerResult.style.display = 'block';
                        
                        // Cari produk di gudang berdasarkan kode batang
                        const product = warehouseProducts.find(p => p.barcode === code);
                        
                        if (product) {
                            // Tambahkan produk ke daftar produk hutang
                            products.push({
                                name: product.name,
                                price: product.price
                            });
                            
                            renderProductList(products, productList, removeProduct);
                            updateTotal(products, totalAmountSpan);
                            
                            scanStatus.textContent = `Berhasil menambahkan: ${product.name}`;
                            scanStatus.className = 'scan-status scan-success';
                            
                            // Reset status setelah 3 detik
                            setTimeout(() => {
                                scanStatus.textContent = 'Mencari kode batang...';
                                scanStatus.className = 'scan-status';
                                scannerResult.style.display = 'none';
                            }, 3000);
                        } else {
                            scanStatus.textContent = 'Produk tidak ditemukan di gudang';
                            scanStatus.className = 'scan-status scan-error';
                            
                            // Reset status setelah 3 detik
                            setTimeout(() => {
                                scanStatus.textContent = 'Mencari kode batang...';
                                scanStatus.className = 'scan-status';
                                scannerResult.style.display = 'none';
                            }, 3000);
                        }
                    });
                };
            } catch (err) {
                console.error('Error accessing camera:', err);
                scanStatus.textContent = 'Error: Tidak dapat mengakses kamera';
                scanStatus.className = 'scan-status scan-error';
                startBarcodeScannerBtn.style.display = 'block';
                barcodeCameraContainer.style.display = 'none';
                barcodeCameraControls.style.display = 'none';
            }
        }
        
        // Fungsi untuk menghentikan scanner barcode di tab tambah hutang
        function stopBarcodeScanner() {
            barcodeScannerActive = false;
            if (barcodeScannerInstance) {
                barcodeScannerInstance.stop();
                barcodeScannerInstance = null;
            }
            stopCameraStream();
            
            startBarcodeScannerBtn.style.display = 'block';
            barcodeCameraContainer.style.display = 'none';
            barcodeCameraControls.style.display = 'none';
            scanStatus.style.display = 'none';
            scannerResult.style.display = 'none';
        }
        
        // Fungsi untuk menampilkan notifikasi
        function showNotification(message) {
            notificationText.textContent = message;
            notification.style.display = 'block';
            
            setTimeout(() => {
                notification.style.display = 'none';
            }, 3000);
        }
        
        // Fungsi untuk menambahkan hutang baru
        function addDebt(e) {
            e.preventDefault();
            
            const debtorName = document.getElementById('debtor-name').value;
            const debtDate = document.getElementById('debt-date').value;
            const dueDate = document.getElementById('due-date').value;
            
            if (!debtorName) {
                showNotification('Nama peminjam harus diisi');
                return;
            }
            
            if (products.length === 0) {
                showNotification('Minimal satu produk harus ditambahkan');
                return;
            }
            
            const totalAmount = calculateTotal(products);
            
            const newDebt = {
                id: Date.now(),
                debtorName,
                products: [...products],
                debtAmount: totalAmount,
                debtDate,
                dueDate,
                isPaid: false,
                dateAdded: new Date().toLocaleDateString('id-ID')
            };
            
            debts.push(newDebt);
            saveDebts();
            renderDebtors();
            populateDebtorSelect();
            
            // Reset form
            debtForm.reset();
            products = [];
            renderProductList(products, productList, removeProduct);
            updateTotal(products, totalAmountSpan);
            
            // Set tanggal default
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('debt-date').value = today;
            
            const due = new Date();
            due.setDate(due.getDate() + 30);
            document.getElementById('due-date').value = due.toISOString().split('T')[0];
            
            // Tampilkan notifikasi
            showNotification(`Hutang ${debtorName} sebesar Rp ${formatCurrency(totalAmount)} berhasil ditambahkan`);
        }
        
        // Fungsi untuk mengelompokkan hutang berdasarkan peminjam
        function groupDebtsByDebtor() {
            const grouped = {};
            
            debts.forEach(debt => {
                if (!grouped[debt.debtorName]) {
                    grouped[debt.debtorName] = [];
                }
                grouped[debt.debtorName].push(debt);
            });
            
            return grouped;
        }
        
        // Fungsi untuk menghitung total hutang per peminjam
        function calculateTotalDebt(debtList) {
            return debtList.reduce((total, debt) => {
                return debt.isPaid ? total : total + debt.debtAmount;
            }, 0);
        }
        
        // Fungsi untuk menampilkan daftar peminjam
        function renderDebtors() {
            debtorsList.innerHTML = '';
            
            if (debts.length === 0) {
                debtorsList.innerHTML = '<p>Tidak ada catatan hutang.</p>';
                return;
            }
            
            const groupedDebts = groupDebtsByDebtor();
            
            Object.keys(groupedDebts).forEach(debtorName => {
                const debtorDebts = groupedDebts[debtorName];
                const totalDebt = calculateTotalDebt(debtorDebts);
                const hasUnpaid = debtorDebts.some(debt => !debt.isPaid);
                const unpaidCount = debtorDebts.filter(debt => !debt.isPaid).length;
                const paidCount = debtorDebts.filter(debt => debt.isPaid).length;
                
                const debtorGroup = document.createElement('div');
                debtorGroup.className = 'debtor-group';
                
                debtorGroup.innerHTML = `
                    <div class="debtor-header">
                        <div class="debtor-info">
                            <div class="debtor-name">${debtorName}</div>
                            <div class="debtor-summary">
                                ${unpaidCount} hutang belum lunas, ${paidCount} hutang lunas
                            </div>
                        </div>
                        <div class="debtor-amount">Rp ${formatCurrency(totalDebt)}</div>
                        <div class="debt-status ${hasUnpaid ? 'status-pending' : 'status-paid'}">
                            ${hasUnpaid ? 'BELUM LUNAS' : 'LUNAS'}
                        </div>
                        <div class="debtor-actions-header">
                            <button class="btn-small btn-warning view-debtor-details" data-debtor="${debtorName}">Detail</button>
                            <button class="btn-small btn-warning generate-doc" data-debtor="${debtorName}" data-type="contract">Kontrak</button>
                        </div>
                    </div>
                    <div class="debtor-details">
                        ${debtorDebts.map(debt => `
                            <div class="debt-item" style="position: relative;">
                                <div class="debt-info">
                                    <div class="debt-date">Tanggal: ${debt.debtDate} ${debt.dueDate ? `| Jatuh Tempo: ${debt.dueDate}` : ''}</div>
                                    <div class="product-details" style="margin-top: 5px; font-size: 0.85rem; color: #6c757d;">
                                        ${debt.products.map(product => `
                                            <div>• ${product.name} - Rp ${formatCurrency(product.price)}</div>
                                        `).join('')}
                                    </div>
                                </div>
                                <div class="debt-amount">Rp ${formatCurrency(debt.debtAmount)}</div>
                                <div class="debt-status ${debt.isPaid ? 'status-paid' : 'status-pending'}">
                                    ${debt.isPaid ? 'LUNAS' : 'BELUM LUNAS'}
                                </div>
                                <div class="debt-actions">
                                    ${!debt.isPaid ? `<button class="btn-small btn-success mark-paid" data-id="${debt.id}">Lunas</button>` : ''}
                                    <button class="btn-small edit-debt" data-id="${debt.id}">Edit</button>
                                </div>
                                ${debt.isPaid ? '<div class="paid-stamp">LUNAS</div>' : ''}
                            </div>
                        `).join('')}
                    </div>
                `;
                
                debtorsList.appendChild(debtorGroup);
                
                // Event listener untuk expand/collapse
                const debtorHeader = debtorGroup.querySelector('.debtor-header');
                const debtorDetails = debtorGroup.querySelector('.debtor-details');
                
                debtorHeader.addEventListener('click', (e) => {
                    // Jangan toggle jika mengklik tombol aksi
                    if (e.target.classList.contains('btn-small')) {
                        return;
                    }
                    debtorDetails.classList.toggle('expanded');
                });
            });
        }
        
        // Fungsi untuk mengisi dropdown peminjam
        function populateDebtorSelect() {
            documentDebtorSelect.innerHTML = '<option value="">-- Pilih Peminjam --</option>';
            
            const groupedDebts = groupDebtsByDebtor();
            Object.keys(groupedDebts).forEach(debtorName => {
                const option = document.createElement('option');
                option.value = debtorName;
                option.textContent = debtorName;
                documentDebtorSelect.appendChild(option);
            });
        }
        
        // Fungsi untuk beralih tab
        function switchToTab(tabId) {
            tabs.forEach(t => t.classList.remove('active'));
            tabContents.forEach(tc => tc.classList.remove('active'));
            
            document.querySelector(`.tab[data-tab="${tabId}"]`).classList.add('active');
            document.getElementById(tabId).classList.add('active');
        }
        
        // Fungsi untuk memilih peminjam di dropdown
        function selectDebtor(debtorName) {
            document.getElementById('document-debtor').value = debtorName;
            document.getElementById('debtor-name-input').value = debtorName;
        }
        
        // Fungsi untuk menghasilkan kontrak
        function generateContract() {
            const debtorName = documentDebtorSelect.value;
            
            if (!debtorName) {
                alert('Pilih peminjam terlebih dahulu');
                return;
            }
            
            const debtorDebts = debts.filter(d => d.debtorName === debtorName && !d.isPaid);
            const totalDebt = calculateTotalDebt(debtorDebts);
            
            if (debtorDebts.length === 0) {
                documentPreview.innerHTML = '<p>Tidak ada hutang aktif untuk peminjam ini.</p>';
                return;
            }
            
            // Ambil data dari form
            const debtorFullName = document.getElementById('debtor-name-input').value || debtorName;
            const debtorAddress = document.getElementById('debtor-address').value || '_______________________________________';
            const debtorNIK = document.getElementById('debtor-nik').value || '_________________________';
            
            const lenderName = document.getElementById('lender-name').value || '_______________________________________';
            const lenderAddress = document.getElementById('lender-address').value || '_______________________________________';
            const lenderNIK = document.getElementById('lender-nik').value || '_________________________';
            
            documentPreview.innerHTML = `
                <h2 style="text-align: center;">SURAT PERJANJIAN HUTANG</h2>
                <p style="text-align: center;">Nomor: SPH/${new Date().getFullYear()}/${String(Math.floor(Math.random() * 1000)).padStart(3, '0')}</p>
                
                <p>Yang bertanda tangan di bawah ini:</p>
                
                <table style="width: 100%; margin: 15px 0;">
                    <tr>
                        <td style="width: 30%;">Nama</td>
                        <td>: ${debtorFullName}</td>
                    </tr>
                    <tr>
                        <td>Alamat</td>
                        <td>: ${debtorAddress}</td>
                    </tr>
                    <tr>
                        <td>NIK</td>
                        <td>: ${debtorNIK}</td>
                    </tr>
                </table>
                
                <p>Selanjutnya disebut sebagai <strong>PIHAK PERTAMA (Peminjam)</strong>.</p>
                
                <table style="width: 100%; margin: 15px 0;">
                    <tr>
                        <td style="width: 30%;">Nama</td>
                        <td>: ${lenderName}</td>
                    </tr>
                    <tr>
                        <td>Alamat</td>
                        <td>: ${lenderAddress}</td>
                    </tr>
                    <tr>
                        <td>NIK</td>
                        <td>: ${lenderNIK}</td>
                    </tr>
                </table>
                
                <p>Selanjutnya disebut sebagai <strong>PIHAK KEDUA (Pemberi Pinjaman)</strong>.</p>
                
                <p>Kedua belah pihak sepakat untuk membuat perjanjian hutang dengan ketentuan sebagai berikut:</p>
                
                <ol>
                    <li>Pihak Pertama meminjam uang dari Pihak Kedua sebesar <strong>Rp ${formatCurrency(totalDebt)}</strong> (${convertToWords(totalDebt)}).</li>
                    <li>Peminjaman ini dilakukan pada tanggal ${new Date().toLocaleDateString('id-ID')}.</li>
                    <li>Pihak Pertama bersedia melunasi hutang tersebut selambat-lambatnya tanggal ${debtorDebts[0]?.dueDate || '________________'}.</li>
                    <li>Apabila sampai dengan tanggal jatuh tempo Pihak Pertama belum melunasi hutang, maka akan dikenakan denda keterlambatan sebesar 2% per bulan dari total hutang.</li>
                    <li>Surat perjanjian ini dibuat dalam dua rangkap, masing-masing untuk Pihak Pertama dan Pihak Kedua.</li>
                </ol>
                
                <p>Demikian surat perjanjian ini dibuat dengan kesadaran penuh tanpa paksaan dari pihak manapun.</p>
                
                <table style="width: 100%; margin-top: 50px;">
                    <tr>
                        <td style="width: 50%; text-align: center;">
                            <p><strong>PIHAK PERTAMA</strong></p>
                            <p>(Peminjam)</p>
                            <div style="height: 100px;"></div>
                            <p>${debtorFullName}</p>
                        </td>
                        <td style="width: 50%; text-align: center;">
                            <p><strong>PIHAK KEDUA</strong></p>
                            <p>(Pemberi Pinjaman)</p>
                            <div style="height: 100px;"></div>
                            <p>${lenderName}</p>
                        </td>
                    </tr>
                </table>
            `;
        }
        
        // Fungsi untuk menghasilkan tagihan
        function generateBill() {
            const debtorName = documentDebtorSelect.value;
            
            if (!debtorName) {
                alert('Pilih peminjam terlebih dahulu');
                return;
            }
            
            const debtorDebts = debts.filter(d => d.debtorName === debtorName && !d.isPaid);
            const totalDebt = calculateTotalDebt(debtorDebts);
            
            if (debtorDebts.length === 0) {
                documentPreview.innerHTML = '<p>Tidak ada hutang aktif untuk peminjam ini.</p>';
                return;
            }
            
            // Ambil data dari form
            const debtorFullName = document.getElementById('debtor-name-input').value || debtorName;
            const debtorAddress = document.getElementById('debtor-address').value || '_______________________________________';
            
            const lenderName = document.getElementById('lender-name').value || '_______________________________________';
            
            documentPreview.innerHTML = `
                <h2 style="text-align: center;">SURAT TAGIHAN HUTANG</h2>
                <p style="text-align: center;">Nomor: STH/${new Date().getFullYear()}/${String(Math.floor(Math.random() * 1000)).padStart(3, '0')}</p>
                
                <p>Kepada Yth,</p>
                <p><strong>${debtorFullName}</strong></p>
                <p>${debtorAddress}</p>
                
                <p>Dengan hormat,</p>
                
                <p>Bersama surat ini, kami sampaikan tagihan hutang Anda yang hingga saat ini belum dilunasi.</p>
                
                <p>Berikut adalah rincian hutang Anda:</p>
                
                <table style="width: 100%; border-collapse: collapse; margin: 15px 0;">
                    <thead>
                        <tr style="background-color: #f8f9fa;">
                            <th style="border: 1px solid #ddd; padding: 8px;">No</th>
                            <th style="border: 1px solid #ddd; padding: 8px;">Produk</th>
                            <th style="border: 1px solid #ddd; padding: 8px;">Tanggal</th>
                            <th style="border: 1px solid #ddd; padding: 8px;">Jumlah</th>
                        </tr>
                    </thead>
                    <tbody>
                        ${debtorDebts.map((debt, index) => `
                            <tr>
                                <td style="border: 1px solid #ddd; padding: 8px;">${index + 1}</td>
                                <td style="border: 1px solid #ddd; padding: 8px;">
                                    ${debt.products.map(product => `${product.name} (Rp ${formatCurrency(product.price)})`).join('<br>')}
                                </td>
                                <td style="border: 1px solid #ddd; padding: 8px;">${debt.debtDate}</td>
                                <td style="border: 1px solid #ddd; padding: 8px;">Rp ${formatCurrency(debt.debtAmount)}</td>
                            </tr>
                        `).join('')}
                    </tbody>
                    <tfoot>
                        <tr>
                            <td colspan="3" style="border: 1px solid #ddd; padding: 8px; text-align: right;"><strong>TOTAL HUTANG:</strong></td>
                            <td style="border: 1px solid #ddd; padding: 8px;"><strong>Rp ${formatCurrency(totalDebt)}</strong></td>
                        </tr>
                    </tfoot>
                </table>
                
                <p>Kami harap Anda dapat segera melunasi hutang tersebut selambat-lambatnya tanggal ${debtorDebts[0]?.dueDate || '________________'}.</p>
                
                <p>Atas perhatian dan kerjasamanya, kami ucapkan terima kasih.</p>
                
                <table style="width: 100%; margin-top: 50px;">
                    <tr>
                        <td style="width: 50%;"></td>
                        <td style="width: 50%; text-align: center;">
                            <p>Hormat kami,</p>
                            <div style="height: 100px;"></div>
                            <p>${lenderName}</p>
                        </td>
                    </tr>
                </table>
            `;
        }
        
        // Fungsi untuk menghasilkan peringatan
        function generateReminder() {
            const debtorName = documentDebtorSelect.value;
            
            if (!debtorName) {
                alert('Pilih peminjam terlebih dahulu');
                return;
            }
            
            const debtorDebts = debts.filter(d => d.debtorName === debtorName && !d.isPaid);
            const totalDebt = calculateTotalDebt(debtorDebts);
            
            if (debtorDebts.length === 0) {
                documentPreview.innerHTML = '<p>Tidak ada hutang aktif untuk peminjam ini.</p>';
                return;
            }
            
            // Ambil data dari form
            const debtorFullName = document.getElementById('debtor-name-input').value || debtorName;
            const debtorAddress = document.getElementById('debtor-address').value || '_______________________________________';
            
            const lenderName = document.getElementById('lender-name').value || '_______________________________________';
            
            documentPreview.innerHTML = `
                <h2 style="text-align: center;">SURAT PERINGATAN HUTANG</h2>
                <p style="text-align: center;">Nomor: SPH/${new Date().getFullYear()}/${String(Math.floor(Math.random() * 1000)).padStart(3, '0')}</p>
                
                <p>Kepada Yth,</p>
                <p><strong>${debtorFullName}</strong></p>
                <p>${debtorAddress}</p>
                
                <p>Dengan hormat,</p>
                
                <p>Bersama surat ini, kami sampaikan peringatan terkait hutang Anda yang telah melewati batas waktu pelunasan.</p>
                
                <p>Berikut adalah rincian hutang Anda:</p>
                
                <table style="width: 100%; border-collapse: collapse; margin: 15px 0;">
                    <thead>
                        <tr style="background-color: #f8f9fa;">
                            <th style="border: 1px solid #ddd; padding: 8px;">No</th>
                            <th style="border: 1px solid #ddd; padding: 8px;">Produk</th>
                            <th style="border: 1px solid #ddd; padding: 8px;">Tanggal Jatuh Tempo</th>
                            <th style="border: 1px solid #ddd; padding: 8px;">Jumlah</th>
                        </tr>
                    </thead>
                    <tbody>
                        ${debtorDebts.map((debt, index) => `
                            <tr>
                                <td style="border: 1px solid #ddd; padding: 8px;">${index + 1}</td>
                                <td style="border: 1px solid #ddd; padding: 8px;">
                                    ${debt.products.map(product => product.name).join(', ')}
                                </td>
                                <td style="border: 1px solid #ddd; padding: 8px;">${debt.dueDate || 'Tidak ditentukan'}</td>
                                <td style="border: 1px solid #ddd; padding: 8px;">Rp ${formatCurrency(debt.debtAmount)}</td>
                            </tr>
                        `).join('')}
                    </tbody>
                    <tfoot>
                        <tr>
                            <td colspan="3" style="border: 1px solid #ddd; padding: 8px; text-align: right;"><strong>TOTAL HUTANG:</strong></td>
                            <td style="border: 1px solid #ddd; padding: 8px;"><strong>Rp ${formatCurrency(totalDebt)}</strong></td>
                        </tr>
                    </tfoot>
                </table>
                
                <p>Kami menekankan bahwa hutang ini sudah melewati batas waktu yang telah disepakati. Kami harap Anda dapat segera melunasi hutang tersebut dalam waktu 7 (tujuh) hari sejak surat ini diterima.</p>
                
                <p>Apabila hutang tidak dilunasi dalam waktu yang ditentukan, kami akan mengambil tindakan hukum sesuai dengan peraturan yang berlaku.</p>
                
                <p>Atas perhatiannya, kami ucapkan terima kasih.</p>
                
                <table style="width: 100%; margin-top: 50px;">
                    <tr>
                        <td style="width: 50%;"></td>
                        <td style="width: 50%; text-align: center;">
                            <p>Hormat kami,</p>
                            <div style="height: 100px;"></div>
                            <p>${lenderName}</p>
                        </td>
                    </tr>
                </table>
            `;
        }
        
        // Fungsi untuk mencetak dokumen
        function printDocument() {
            const printWindow = window.open('', '_blank');
            printWindow.document.write(`
                <html>
                    <head>
                        <title>Cetak Dokumen</title>
                        <style>
                            body { font-family: Arial, sans-serif; margin: 20px; }
                            table { width: 100%; border-collapse: collapse; margin: 15px 0; }
                            th, td { border: 1px solid #ddd; padding: 8px; }
                            th { background-color: #f8f9fa; }
                            .text-center { text-align: center; }
                            .signature-box { margin-top: 10px; padding-top: 10px; border-top: 1px solid #eee; }
                        </style>
                    </head>
                    <body>
                        ${documentPreview.innerHTML}
                    </body>
                </html>
            `);
            printWindow.document.close();
            printWindow.print();
        }
        
        // Fungsi untuk mengonversi angka ke kata-kata (terbatas)
        function convertToWords(number) {
            const units = ['', 'satu', 'dua', 'tiga', 'empat', 'lima', 'enam', 'tujuh', 'delapan', 'sembilan'];
            const teens = ['sepuluh', 'sebelas', 'dua belas', 'tiga belas', 'empat belas', 'lima belas', 'enam belas', 'tujuh belas', 'delapan belas', 'sembilan belas'];
            const tens = ['', '', 'dua puluh', 'tiga puluh', 'empat puluh', 'lima puluh', 'enam puluh', 'tujuh puluh', 'delapan puluh', 'sembilan puluh'];
            
            if (number === 0) return 'nol';
            
            let words = '';
            
            // Jutaan
            if (number >= 1000000) {
                words += convertToWords(Math.floor(number / 1000000)) + ' juta ';
                number %= 1000000;
            }
            
            // Ribuan
            if (number >= 1000) {
                words += convertToWords(Math.floor(number / 1000)) + ' ribu ';
                number %= 1000;
            }
            
            // Ratusan
            if (number >= 100) {
                words += units[Math.floor(number / 100)] + ' ratus ';
                number %= 100;
            }
            
            // Puluhan dan belasan
            if (number >= 10 && number < 20) {
                words += teens[number - 10] + ' ';
                number = 0;
            } else if (number >= 20) {
                words += tens[Math.floor(number / 10)] + ' ';
                number %= 10;
            }
            
            // Satuan
            if (number > 0) {
                words += units[number] + ' ';
            }
            
            return words.trim() + ' rupiah';
        }
        
        // Hapus produk
        function removeProduct(index) {
            products.splice(index, 1);
            renderProductList(products, productList, removeProduct);
            updateTotal(products, totalAmountSpan);
        }
        
        // Fungsi untuk menyimpan data ke localStorage
        function saveDebts() {
            localStorage.setItem('debts', JSON.stringify(debts));
        }
        
        // Fungsi untuk menyimpan data gudang ke localStorage
        function saveWarehouseProducts() {
            localStorage.setItem('warehouseProducts', JSON.stringify(warehouseProducts));
        }
        
        // Tutup modal
        document.querySelectorAll('.close-modal').forEach(button => {
            button.addEventListener('click', (e) => {
                e.target.closest('.modal').style.display = 'none';
            });
        });
    </script>
</body>
</html>
