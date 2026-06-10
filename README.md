<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Evaluasi & Profil Siswa</title>
    <!-- Memuat html2pdf.js Versi Stabil -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    <style>
        :root {
            --primary: #4f46e5;
            --primary-gradient: linear-gradient(135deg, #6366f1 0%, #4f46e5 100%);
            --primary-hover: #4338ca;
            --primary-light: #f5f3ff;
            --success: #059669;
            --success-gradient: linear-gradient(135deg, #10b981 0%, #059669 100%);
            --slate-50: #f8fafc;
            --slate-100: #f1f5f9;
            --slate-200: #e2e8f0;
            --slate-300: #cbd5e1;
            --slate-700: #334155;
            --slate-800: #1e293b;
            --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.05), 0 2px 4px -2px rgba(0, 0, 0, 0.05);
            --shadow-lg: 0 10px 25px -3px rgba(99, 102, 241, 0.08), 0 4px 12px -4px rgba(99, 102, 241, 0.08);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #eef2ff 0%, #f5f3ff 50%, #f0fdf4 100%);
            color: var(--slate-800);
            min-height: 100vh;
            padding: 40px 20px;
            display: flex;
            justify-content: center;
            align-items: flex-start;
        }

        .container {
            background-color: #ffffff;
            width: 100%;
            max-width: 800px;
            padding: 45px;
            border-radius: 20px;
            box-shadow: var(--shadow-lg);
            border: 1px solid rgba(255, 255, 255, 0.8);
            position: relative;
        }

        .container::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 6px;
            background: var(--primary-gradient);
            border-top-left-radius: 20px;
            border-top-right-radius: 20px;
        }

        .header {
            text-align: center;
            margin-bottom: 35px;
        }

        .header-badge {
            display: inline-block;
            background: var(--primary-light);
            color: var(--primary);
            padding: 6px 16px;
            border-radius: 100px;
            font-size: 11px;
            font-weight: 800;
            letter-spacing: 1px;
            text-transform: uppercase;
            margin-bottom: 12px;
        }

        .header h1 {
            font-size: 26px;
            font-weight: 800;
            color: var(--slate-800);
            margin-bottom: 8px;
        }

        .header p {
            color: #64748b;
            font-size: 14px;
        }

        .settings-panel {
            background-color: var(--slate-50);
            border: 1.5px dashed var(--slate-200);
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 25px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 15px;
            flex-wrap: wrap;
        }

        .wa-input-container {
            display: flex;
            align-items: center;
            background: white;
            border: 2px solid #ddd6fe;
            border-radius: 8px;
            padding: 6px 12px;
        }

        .wa-input-container span {
            font-size: 14px;
            color: #a78bfa;
            font-weight: 700;
        }

        .wa-input-container input {
            border: none;
            outline: none;
            font-size: 14px;
            font-weight: 700;
            color: var(--slate-800);
            width: 120px;
            margin-left: 4px;
        }

        .section-title {
            font-size: 13px;
            font-weight: 800;
            color: var(--slate-800);
            margin: 30px 0 15px 0;
            padding-bottom: 5px;
            border-bottom: 2px solid var(--slate-200);
            text-transform: uppercase;
            letter-spacing: 0.5px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .section-title::before {
            content: '';
            display: block;
            width: 5px;
            height: 15px;
            background: var(--primary-gradient);
            border-radius: 10px;
        }

        .form-grid {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .form-group {
            display: flex;
            flex-direction: column;
            gap: 6px;
            width: 100%;
        }

        label {
            font-weight: 700;
            color: var(--slate-700);
            font-size: 13px;
        }

        input[type="text"],
        select,
        textarea {
            width: 100%;
            padding: 10px 14px;
            border: 2px solid var(--slate-200);
            border-radius: 8px;
            font-size: 13.5px;
            font-weight: 500;
            color: var(--slate-800);
            background-color: var(--slate-50);
            outline: none;
            transition: border-color 0.2s;
        }

        input[type="text"]:focus,
        select:focus,
        textarea:focus {
            border-color: var(--primary);
            background-color: #fff;
        }

        .child-order {
            display: flex;
            gap: 10px;
            align-items: center;
            font-size: 13.5px;
            color: var(--slate-700);
            font-weight: 600;
        }

        .child-order input {
            width: 60px;
            text-align: center;
        }

        .ttl-group {
            display: flex;
            gap: 12px;
        }

        /* Segmen Row Box Memanjang Indah */
        .row-item {
            border: 2px solid var(--slate-200);
            border-radius: 10px;
            margin-bottom: 15px;
            overflow: hidden;
            width: 100%;
        }

        .row-label {
            padding: 10px 14px;
            font-size: 12px;
            font-weight: 850;
            text-transform: uppercase;
        }

        .row-label.blue { background: #e0f2fe; color: #0369a1; }
        .row-label.green { background: #d1fae5; color: #047857; }
        .row-label.orange { background: #ffedd5; color: #c2410c; }

        .row-content {
            background: #ffffff;
            padding: 8px;
        }

        .row-content input[type="text"] {
            border: 1px solid var(--slate-200);
            background-color: var(--slate-50);
        }

        /* Tombol Aksi */
        .action-buttons {
            display: flex;
            gap: 15px;
            margin-top: 35px;
        }

        .btn {
            flex: 1;
            padding: 15px 20px;
            border: none;
            border-radius: 10px;
            font-size: 14.5px;
            font-weight: 800;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            color: white;
            transition: transform 0.2s, filter 0.2s;
        }

        .btn:active {
            transform: scale(0.98);
        }

        .btn-pdf { background: var(--primary-gradient); }
        .btn-pdf:hover { filter: brightness(1.1); }
        .btn-wa { background: var(--success-gradient); }
        .btn-wa:hover { filter: brightness(1.1); }
        .btn svg { width: 18px; height: 18px; fill: currentColor; }

        /* Toast Popup Notifikasi */
        #toast-container {
            position: fixed;
            bottom: 30px;
            right: 30px;
            z-index: 9999;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .toast {
            background: var(--slate-800);
            color: white;
            padding: 14px 20px;
            border-radius: 10px;
            box-shadow: 0 10px 15px -3px rgba(0,0,0,0.1);
            font-size: 13.5px;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 10px;
            min-width: 280px;
            animation: slideIn 0.3s ease forwards;
        }

        .toast.success { border-left: 5px solid #10b981; }
        .toast.error { border-left: 5px solid #ef4444; }

        @keyframes slideIn {
            from { transform: translateY(50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        /* ==========================================================
           CSS KHUSUS CONVERT PDF (SANGAT PADAT - PAS SATU LEMBAR)
           ========================================================== */
        .pdf-page-container {
            background-color: #ffffff !important;
            color: #000000 !important;
            padding: 0 !important;
            font-family: Arial, sans-serif !important;
            width: 100% !important;
        }

        .pdf-header {
            text-align: center;
            margin-bottom: 12px;
            border-bottom: 2.5px double #000000;
            padding-bottom: 5px;
        }

        .pdf-header h2 {
            font-size: 16px;
            text-transform: uppercase;
            color: #000000;
            margin-bottom: 2px;
            font-weight: bold;
            letter-spacing: 0.5px;
        }

        .pdf-header p {
            font-size: 10px;
            color: #333333;
            margin-bottom: 2px;
        }

        .pdf-header p.sub {
            font-size: 8.5px;
            color: #555555;
            font-style: italic;
        }

        .pdf-section-title {
            font-size: 11px;
            font-weight: bold;
            text-transform: uppercase;
            margin: 10px 0 4px 0;
            border-bottom: 1.5px solid #000000;
            color: #000000;
            padding-bottom: 1px;
        }

        .pdf-table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 6px;
        }

        .pdf-table td {
            padding: 4px 8px;
            font-size: 11px;
            border: 1px solid #444444;
            color: #000000;
            vertical-align: top;
        }

        .pdf-table td.pdf-lbl {
            background-color: #f2f2f2;
            font-weight: bold;
            width: 32%;
        }

        .pdf-signature-table {
            width: 100%;
            margin-top: 15px;
            border-collapse: collapse;
        }

        .pdf-signature-table td {
            width: 50%;
            text-align: center;
            font-size: 11px;
            vertical-align: top;
            border: none !important;
            padding: 0 !important;
        }

        .pdf-sig-space {
            height: 40px;
        }

        .pdf-sig-line {
            width: 70%;
            margin: 0 auto 3px auto;
            border-bottom: 1px solid #000000;
        }

        /* RESPONSIVE LAYOUT SMARTPHONE */
        @media (max-width: 768px) {
            body { padding: 10px; }
            .container { padding: 25px 15px; border-radius: 16px; }
            .ttl-group { flex-direction: column; gap: 8px; }
            .action-buttons { flex-direction: column; gap: 10px; }
        }
    </style>
</head>
<body>

<div class="container">
    <!-- Header -->
    <div class="header">
        <span class="header-badge">ARSIP BK</span>
        <h1>Profil & Evaluasi Kondisi Siswa</h1>
        <p>Bimbingan Konseling dan Penilaian Perkembangan Kepribadian Mandiri</p>
    </div>

    <!-- Panel Pengaturan Nomor Guru BK -->
    
    <form id="formSiswa" onsubmit="event.preventDefault();">
        
        <!-- BAGIAN 1: PROFIL SISWA (BARIS MEMANJANG PENUH) -->
        <div class="section-title">Profil Siswa</div>
        <div class="form-grid">
            <div class="form-group">
                <label for="nama">Nama Lengkap</label>
                <input type="text" id="nama" placeholder="Masukkan nama lengkap siswa" required>
            </div>

            <div class="form-group">
                <label for="gender">Jenis Kelamin</label>
                <select id="gender">
                    <option value="">-- Pilih Jenis Kelamin --</option>
                    <option value="Laki-laki">Laki-laki</option>
                    <option value="Perempuan">Perempuan</option>
                </select>
            </div>

            <div class="form-group">
                <label>Tempat & Tanggal Lahir</label>
                <div class="ttl-group">
                    <input type="text" id="tempat_lahir" placeholder="Kota Kelahiran" style="flex: 1;">
                    <input type="text" id="tanggal_lahir" placeholder="Contoh: 29 Juni 2010" style="flex: 1;">
                </div>
            </div>

            <div class="form-group">
                <label>Urutan Anak</label>
                <div class="child-order">
                    <span>Anak ke</span>
                    <input type="text" id="anak_ke" placeholder="..."> 
                    <span>dari</span>
                    <input type="text" id="dari_bersaudara" placeholder="...">
                    <span>bersaudara</span>
                </div>
            </div>

            <div class="form-group">
                <label for="agama">Agama</label>
                <select id="agama">
                    <option value="">-- Pilih Agama --</option>
                    <option value="Islam">Islam</option>
                    <option value="Kristen">Kristen</option>
                    <option value="Katolik">Katolik</option>
                    <option value="Hindu">Hindu</option>
                    <option value="Buddha">Buddha</option>
                    <option value="Khonghucu">Khonghucu</option>
                </select>
            </div>

            <div class="form-group">
                <label for="asal_sekolah">Asal Sekolah</label>
                <input type="text" id="asal_sekolah" placeholder="Asal sekolah/instansi sebelumnya">
            </div>

            <div class="form-group">
                <label for="alamat">Alamat Rumah</label>
                <textarea id="alamat" rows="2" placeholder="Tuliskan alamat domisili lengkap saat ini"></textarea>
            </div>

        </div>

        <!-- BAGIAN 2: RIWAYAT KESEHATAN (MEMANJANG MAKSIMAL) -->
        <div class="section-title">Riwayat Kesehatan</div>
        
        <div class="row-item">
            <div class="row-label blue">Penyakit Yang Pernah / Sedang Diderita</div>
            <div class="row-content">
                <input type="text" id="penyakit_1" placeholder="Tulis keluhan penyakit utama siswa (jika ada)">
            </div>
        </div>

        <div class="row-item">
            <div class="row-label blue">Jenis Alergi yang Diderita</div>
            <div class="row-content">
                <input type="text" id="alergi_1" placeholder="Tulis riwayat alergi makanan, obat, atau cuaca (jika ada)">
            </div>
        </div>

        <!-- BAGIAN 3: POTENSI / BAKAT -->
        <div class="section-title">Potensi / Bakat Siswa</div>
        <div class="form-group">
            <label for="potensi">Potensi Unggul / Minat Bakat Utama</label>
            <textarea id="potensi" rows="2" placeholder="Tuliskan kelebihan, minat, atau bakat khusus siswa..."></textarea>
        </div>

        <!-- BAGIAN 3.5: KESUKAAN ANANDA -->
        <div class="section-title">Kesukaan Ananda</div>
        <div class="form-group">
            <label for="kesukaan">Hal-hal yang Disukai / Favorit Ananda (Hobi, Makanan, Aktivitas, Warna, dll.)</label>
            <textarea id="kesukaan" rows="2" placeholder="Tulis hal-hal yang membuat siswa senang atau bersemangat..."></textarea>
        </div>

        <!-- BAGIAN 4: EVALUASI PERILAKU -->
        <div class="section-title">Evaluasi Perilaku & Penanganan Orang Tua</div>
        
        <div class="row-item">
            <div class="row-label green">Sifat / Perilaku Baik (Positif)</div>
            <div class="row-content">
                <input type="text" id="pos_1" placeholder="Tulis sifat baik utama (contoh: mandiri, sopan, suka menolong, jujur)">
            </div>
        </div>

        <div class="row-item">
            <div class="row-label orange">Sifat / Perilaku Negatif (Menurut Orang Tua)</div>
            <div class="row-content">
                <input type="text" id="neg_1" placeholder="(contoh: suka marah, membantah, malas belajar)">
            </div>
        </div>

        <div class="row-item">
            <div class="row-label orange">Cara Orang Tua Menangani di Rumah (Solusi)</div>
            <div class="row-content">
                <input type="text" id="sol_1" placeholder="Tulis solusi tindakan orang tua menghadapi sifat negatif tersebut">
            </div>
        </div>
        <div>
            <div class="form-group">
                <label for="nama_ortu">Nama Orang Tua / Wali</label>
                <input type="text" id="nama_ortu" placeholder="Masukkan nama lengkap Orang Tua atau Wali siswa" required>
            </div>
        </div>
        <div>
                <div class="settings-panel">
            <div style="font-size: 12.5px; color: var(--slate-700);">
                <strong>Tujuan Pengiriman WA (pakai code 62):</strong> Masukkan nomor WA Guru BK aktif di samping kanan.
            </div>
        <div class="wa-input-container">
            <span>+</span>
            <input type="text" id="no_bk" value="" placeholder="62812xxxxxx">
        </div>
    </div>
        </div>

        <!-- ACTION BUTTONS -->
        <div class="action-buttons">
            <button type="button" class="btn btn-pdf" onclick="simpanCetakPDF()">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                </svg>
                Simpan PDF
            </button>
            
            <button type="button" class="btn btn-wa" onclick="kirimKeWhatsAppBK()">
                <svg viewBox="0 0 24 24">
                    <path d="M12.004 2c-5.51 0-9.99 4.49-9.99 10 0 1.77.47 3.43 1.29 4.9L2 22l5.25-1.37c1.42.77 3.03 1.21 4.75 1.21 5.51 0 9.99-4.49 9.99-10s-4.48-10-9.99-10zm5.83 14.25c-.24.67-1.19 1.27-1.95 1.39-.71.1-1.62.13-2.61-.19-3.95-1.28-6.49-5.3-6.69-5.57-.2-.27-1.61-2.14-1.61-4.08 0-1.94 1.01-2.9 1.37-3.27.36-.37.79-.46 1.05-.46.26 0 .52.01.74.02.23.01.48-.09.73.52.26.63.88 2.16.96 2.32.08.16.13.35.03.56-.1.21-.15.34-.31.53-.16.19-.34.42-.48.57-.16.16-.33.34-.14.67.19.33.85 1.4 1.83 2.27 1.26 1.13 2.32 1.48 2.65 1.64.33.16.52.13.71-.09.19-.22.82-.96 1.04-1.29.22-.33.45-.28.75-.17.31.11 1.96.93 2.3 1.1.33.16.56.24.64.38.08.14.08.82-.16 1.49z"/>
                </svg>
                Kirim ke WA BK
            </button>
        </div>
    </form>
</div>

<!-- TOAST CONTAINER -->
<div id="toast-container"></div>

<script>
    // Fungsi Toast Notifikasi
    function showToast(message, type = 'success') {
        const container = document.getElementById('toast-container');
        const toast = document.createElement('div');
        toast.className = `toast ${type}`;
        toast.innerText = message;
        container.appendChild(toast);
        setTimeout(() => {
            toast.style.animation = 'none';
            toast.offsetHeight; // trigger reflow
            toast.style.transition = 'opacity 0.3s';
            toast.style.opacity = '0';
            setTimeout(() => toast.remove(), 300);
        }, 3000);
    }

    // Fungsi Pengonversi PDF (Instant, Tanpa Print Dialog, & Garansi Anti Blank!)
    function simpanCetakPDF() {
        const nama = document.getElementById('nama').value;
        const namaOrtu = document.getElementById('nama_ortu').value;
        if(!nama) {
            showToast("Harap isi Nama Lengkap terlebih dahulu.", "error");
            return;
        }
        if(!namaOrtu) {
            showToast("Harap isi Nama Orang Tua / Wali terlebih dahulu.", "error");
            return;
        }

        showToast("Memproses PDF Anda...", "success");

        // Tarik data form secara manual
        const gender = document.getElementById('gender').value || '-';
        const tempat = document.getElementById('tempat_lahir').value || '-';
        const tgl = document.getElementById('tanggal_lahir').value || '-';
        const anak_ke = document.getElementById('anak_ke').value || '-';
        const dari = document.getElementById('dari_bersaudara').value || '-';
        const agama = document.getElementById('agama').value || '-';
        const sekolah = document.getElementById('asal_sekolah').value || '-';
        const alamat = document.getElementById('alamat').value || '-';
        const penyakit = document.getElementById('penyakit_1').value || '-';
        const alergi = document.getElementById('alergi_1').value || '-';
        const potensi = document.getElementById('potensi').value || '-';
        const kesukaan = document.getElementById('kesukaan').value || '-';
        const pos = document.getElementById('pos_1').value || '-';
        const neg = document.getElementById('neg_1').value || '-';
        const sol = document.getElementById('sol_1').value || '-';

        // Rekayasa Template PDF Indah (Teks murni & Tabel, Dijamin Lolos dari Bug Blank & Muat Satu Lembar)
        const pdfClone = document.createElement('div');
        pdfClone.className = 'pdf-page-container';
        pdfClone.innerHTML = `
            <div style="padding: 2px;">
                <div class="pdf-header">
                    <h2>LAPORAN KONDISI AWAL SISWA</h2>
                    <h2>SMP HAMALATUL QUR'AN</h2>
                    <p>Bimbingan Konseling dan Penilaian Perkembangan Kepribadian Mandiri</p>
                    <p class="sub">Jl.Raya Pare Kandangan No 5 dsn Ringinagung Desa Keling Kec Kepung Kab Kediri </p>
                </div>

                <div class="pdf-section-title">I. PROFIL SISWA</div>
                <table class="pdf-table">
                    <tr><td class="pdf-lbl">Nama Lengkap Siswa</td><td><strong>${nama}</strong></td></tr>
                    <tr><td class="pdf-lbl">Nama Orang Tua / Wali</td><td><strong>${namaOrtu}</strong></td></tr>
                    <tr><td class="pdf-lbl">Jenis Kelamin</td><td>${gender}</td></tr>
                    <tr><td class="pdf-lbl">Tempat, Tanggal Lahir</td><td>${tempat}, ${tgl}</td></tr>
                    <tr><td class="pdf-lbl">Urutan Anak</td><td>Anak ke ${anak_ke} dari ${dari} bersaudara</td></tr>
                    <tr><td class="pdf-lbl">Agama</td><td>${agama}</td></tr>
                    <tr><td class="pdf-lbl">Asal Sekolah</td><td>${sekolah}</td></tr>
                    <tr><td class="pdf-lbl">Alamat Rumah</td><td>${alamat}</td></tr>
                </table>

                <div class="pdf-section-title">II. RIWAYAT KESEHATAN</div>
                <table class="pdf-table">
                    <tr><td class="pdf-lbl">Penyakit yang Pernah / Sedang Diderita</td><td>${penyakit}</td></tr>
                    <tr><td class="pdf-lbl">Jenis Alergi yang Diderita</td><td>${alergi}</td></tr>
                </table>

                <div class="pdf-section-title">III. POTENSI & KESUKAAN SISWA</div>
                <table class="pdf-table">
                    <tr><td class="pdf-lbl">Potensi Unggul / Minat Bakat</td><td>${potensi}</td></tr>
                    <tr><td class="pdf-lbl">Kesukaan Ananda (Hobi/Fav)</td><td>${kesukaan}</td></tr>
                </table>

                <div class="pdf-section-title">IV. EVALUASI PERILAKU & SOLUSI ORANG TUA</div>
                <table class="pdf-table">
                    <tr><td class="pdf-lbl" style="background-color: #f2fdf2;">Sifat / Perilaku Baik (Positif)</td><td>${pos}</td></tr>
                    <tr><td class="pdf-lbl" style="background-color: #fffaf0;">Sifat / Perilaku Negatif</td><td>${neg}</td></tr>
                    <tr><td class="pdf-lbl" style="background-color: #fffaf0;">Cara Menangani di Rumah (Solusi)</td><td>${sol}</td></tr>
                </table>

                <!-- Kolom Tanda Tangan Manual -->
                <table class="pdf-signature-table">
                    <tr>
                        <td>
                        <td>
                            <strong>......, ............................ 20...</strong><br>
                            <span>Orang Tua / Wali Murid</span>
                            <div class="pdf-sig-space"></div>
                            <div class="pdf-sig-line"></div>
                            <span style="color: #000; font-weight: bold; font-size: 11px;">( ${namaOrtu} )</span>
                        </td>
                    </tr>
                </table>
            </div>
        `;

        const opsi = {
            margin:       [8, 10, 8, 10], // Margin diperkecil agar pas 1 lembar A4 secara vertikal
            filename:     `Evaluasi_Siswa_${nama.replace(/\s+/g, '_')}.pdf`,
            image:        { type: 'jpeg', quality: 0.98 },
            html2canvas:  { 
                scale: 2, 
                useCORS: true, 
                backgroundColor: '#ffffff',
                logging: false,
                scrollY: 0,
                scrollX: 0
            },
            jsPDF:        { unit: 'mm', format: 'a4', orientation: 'portrait' }
        };

        // Simpan dokumen langsung tanpa masuk window.print() browser
        html2pdf().set(opsi).from(pdfClone).save().then(() => {
            showToast("PDF Berhasil diunduh langsung!", "success");
        }).catch((err) => {
            showToast("Terjadi kesalahan saat memproses PDF.", "error");
        });
    }

    // Fungsi Kirim ke WhatsApp
    function kirimKeWhatsAppBK() {
        const nama = document.getElementById('nama').value;
        const namaOrtu = document.getElementById('nama_ortu').value || '-';
        let no_bk_input = document.getElementById('no_bk').value.replace(/[^0-9]/g, '');

        if(!nama) {
            showToast("Nama siswa tidak boleh kosong.", "error");
            return;
        }

        if(!no_bk_input) {
            showToast("Nomor WhatsApp BK tidak boleh kosong.", "error");
            return;
        }

        let pesan = `*PROFIL & EVALUASI KONDISI SISWA*\n\n`;
        pesan += `*PROFIL SISWA*\n`;
        pesan += `• Nama Siswa: ${nama}\n`;
        pesan += `• Nama Orang Tua: ${namaOrtu}\n`;
        pesan += `• Jenis Kelamin: ${document.getElementById('gender').value || '-'}\n`;
        pesan += `• Urutan Anak: Anak ke-${document.getElementById('anak_ke').value || '-'} dari ${document.getElementById('dari_bersaudara').value || '-'} bersaudara\n`;
        pesan += `• TTL: ${document.getElementById('tempat_lahir').value || '-'}, ${document.getElementById('tanggal_lahir').value || '-'}\n`;
        pesan += `• Agama: ${document.getElementById('agama').value || '-'}\n`;
        pesan += `• Asal Sekolah: ${document.getElementById('asal_sekolah').value || '-'}\n`;
        pesan += `• Alamat: ${document.getElementById('alamat').value || '-'}\n\n`;
        
        pesan += `*RIWAYAT KESEHATAN*\n`;
        pesan += `• Penyakit: ${document.getElementById('penyakit_1').value || '-'}\n`;
        pesan += `• Alergi: ${document.getElementById('alergi_1').value || '-'}\n\n`;
        
        pesan += `*POTENSI / BAKAT*\n`;
        pesan += `• Bidang: ${document.getElementById('potensi').value || '-'}\n\n`;

        pesan += `*KESUKAAN ANANDA*\n`;
        pesan += `• Favorit: ${document.getElementById('kesukaan').value || '-'}\n\n`;

        pesan += `*EVALUASI PERILAKU POSITIF*\n`;
        pesan += `• Sifat Positif: ${document.getElementById('pos_1').value || '-'}\n\n`;

        pesan += `*PERILAKU NEGATIF & PENANGANAN ORANG TUA*\n`;
        pesan += `• Sifat Negatif: ${document.getElementById('neg_1').value || '-'}\n`;
        pesan += `  Solusi Rumah: ${document.getElementById('sol_1').value || '-'}\n`;

        showToast("Membuka WhatsApp...", "success");

        const urlWhatsApp = `https://api.whatsapp.com/send?phone=${no_bk_input}&text=${encodeURIComponent(pesan)}`;
        
        setTimeout(() => {
            window.open(urlWhatsApp, '_blank');
        }, 600);
    }
</script>
</body>
</html>
