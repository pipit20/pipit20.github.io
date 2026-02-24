<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>WOM Finance - Dompet Kredit</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <style>
    body { font-family: 'Plus Jakarta Sans', sans-serif; }
    .main-bg { background: linear-gradient(135deg, #f1f5f9 0%, #e0e7ff 50%, #ede9fe 100%); min-height: 100vh; }
    .card { background: white; border-radius: 1.25rem; box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.05); border: 1px solid rgba(255,255,255,0.6); }
    .form-input { width: 100%; padding: 0.75rem 1rem; border: 1px solid #e2e8f0; border-radius: 0.75rem; background: #f8fafc; transition: all 0.2s; font-size: 0.875rem; color: #334155; }
    .form-input:focus { border-color: #6366f1; background: white; box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.15); outline: none; }
    .nav-tab { padding: 0.75rem 1.25rem; font-weight: 600; font-size: 0.875rem; border-radius: 0.75rem; transition: all 0.3s; color: #64748b; border: 1px solid transparent; background: transparent; cursor: pointer; }
    .nav-tab:hover { background: rgba(255,255,255,0.6); color: #4f46e5; }
    .nav-tab.active { background: white; color: #4f46e5; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05); border-color: #e0e7ff; }
    .btn-check { background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%); color: white; font-weight: 600; padding: 0.75rem 1.5rem; border-radius: 0.75rem; border: none; cursor: pointer; box-shadow: 0 4px 11px rgba(99, 102, 241, 0.3); transition: all 0.2s; }
    .btn-check:hover { transform: translateY(-2px); box-shadow: 0 6px 20px rgba(99, 102, 241, 0.4); }
    .prod-item { padding: 1rem; border: 2px solid #e2e8f0; border-radius: 1rem; cursor: pointer; transition: all 0.2s; background: white; text-align: center; }
    .prod-item:hover { border-color: #a5b4fc; }
    .prod-item.active { border-color: #6366f1; background: #eef2ff; box-shadow: 0 4px 10px rgba(99, 102, 241, 0.1); }
    .page-section { display: none; animation: fadeIn 0.4s ease; }
    .page-section.active { display: block; }
    @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
    .rp-wrap { position: relative; }
    .rp-pre { position: absolute; left: 1rem; top: 50%; transform: translateY(-50%); color: #64748b; font-weight: 500; font-size: 0.875rem; pointer-events: none; }
    .rp-inp { padding-left: 2.5rem !important; }
    .section-title { font-weight: 700; font-size: 0.8rem; color: #475569; border-left: 4px solid #6366f1; padding-left: 0.75rem; margin-bottom: 0.75rem; text-transform: uppercase; letter-spacing: 0.05em; }
    .section-title.teal { border-color: #14b8a6; }
    .section-title.cyan { border-color: #06b6d4; }
    .section-title.rose { border-color: #f43f5e; }
    .section-title.amber { border-color: #f59e0b; }
    .result-item { display: flex; gap: 0.5rem; align-items: flex-start; padding: 0.5rem 0; border-bottom: 1px solid #f1f5f9; }
    .result-item:last-child { border-bottom: none; }
    .status-badge { display: inline-flex; align-items: center; gap: 0.25rem; padding: 0.25rem 0.75rem; border-radius: 9999px; font-size: 0.75rem; font-weight: 600; }
    .status-pass { background: #dcfce7; color: #166534; border: 1px solid #bbf7d0; }
    .status-fail { background: #fee2e2; color: #991b1b; border: 1px solid #fecaca; }
    .status-warn { background: #fef3c7; color: #92400e; border: 1px solid #fde68a; }
    .hidden { display: none !important; }
    .custom-check { display: flex; align-items: flex-start; gap: 0.5rem; cursor: pointer; font-size: 0.8rem; color: #475569; margin-bottom: 0.5rem; }
    .custom-check input { width: 1rem; height: 1rem; accent-color: #6366f1; cursor: pointer; margin-top: 0.15rem; flex-shrink: 0; }
    .custom-check-desc { color: #64748b; font-size: 0.7rem; }
    
    /* Deviasi Category Box */
    .dev-cat-box { background: #fafafa; border: 1px solid #e5e7eb; border-radius: 0.75rem; margin-bottom: 1rem; overflow: hidden; }
    .dev-cat-header { background: linear-gradient(90deg, #f1f5f9 0%, #f8fafc 100%); padding: 0.75rem 1rem; border-bottom: 1px solid #e5e7eb; }
    .dev-cat-title { font-weight: 700; font-size: 0.85rem; color: #374151; display: flex; align-items: center; gap: 0.5rem; }
    .dev-cat-badge { background: #6366f1; color: white; padding: 0.125rem 0.5rem; border-radius: 0.25rem; font-size: 0.7rem; }
    .dev-cat-body { padding: 1rem; }
    .dev-note { background: #f0f9ff; color: #0369a1; padding: 0.25rem 0.5rem; border-radius: 0.25rem; font-size: 0.7rem; margin-top: 0.25rem; display: inline-block; border: 1px solid #bae6fd; }
    .dev-result-inline { font-size: 0.7rem; color: #6366f1; font-weight: 600; margin-top: 0.25rem; }
    
    .super-tab { padding: 0.5rem 1rem; font-weight: 600; font-size: 0.75rem; border-radius: 0.5rem; cursor: pointer; transition: all 0.2s; }
    .super-tab.active { background: #6366f1; color: white; }
    .super-tab:not(.active) { background: #f1f5f9; color: #64748b; }
  </style>
</head>
<body class="main-bg text-slate-700">

  <!-- Header -->
  <header class="sticky top-0 z-50 backdrop-blur-lg bg-white/40 border-b border-white/50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 py-4 flex flex-col md:flex-row justify-between items-center gap-4">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 bg-gradient-to-br from-indigo-500 to-purple-500 rounded-xl flex items-center justify-center shadow-md">
          <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"></path></svg>
        </div>
        <div>
          <h1 class="font-bold text-lg text-slate-800">Dompet Kredit</h1>
          <p class="text-xs text-slate-500">Credit Eligibility Checker</p>
        </div>
      </div>
      <nav class="flex gap-2 p-1 bg-white/50 rounded-xl backdrop-blur-sm border border-white/50">
        <button onclick="navigatePage('norkil')" id="btn-norkil" class="nav-tab active">Normal Kilat</button>
        <button onclick="navigatePage('deviasi')" id="btn-deviasi" class="nav-tab">Deviasi</button>
        <button onclick="navigatePage('super')" id="btn-super" class="nav-tab">MobilKu Super</button>
      </nav>
    </div>
  </header>

  <!-- Main -->
  <main class="max-w-7xl mx-auto px-4 sm:px-6 py-6">

    <!-- ================= NORMAL KILAT PAGE ================= -->
    <section id="page-norkil" class="page-section active">
      <div class="grid grid-cols-12 gap-6">
        <div class="col-span-12 lg:col-span-8 space-y-5">
          <div class="card p-5">
            <h3 class="section-title">Pilih Produk Pembiayaan</h3>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-3">
              <div id="prod-mobilku" onclick="selectProduct('mobilku')" class="prod-item active"><div class="font-bold text-indigo-700">MobilKu</div><div class="text-xs text-slate-500 mt-1">SK 186</div></div>
              <div id="prod-motorku" onclick="selectProduct('motorku')" class="prod-item"><div class="font-bold text-teal-700">MotorKu</div><div class="text-xs text-slate-500 mt-1">SK 167</div></div>
              <div id="prod-newbike_bpjs" onclick="selectProduct('newbike_bpjs')" class="prod-item"><div class="font-bold text-cyan-700">NewBike BPJS</div><div class="text-xs text-slate-500 mt-1">SK 156</div></div>
              <div id="prod-newbike_nonbpjs" onclick="selectProduct('newbike_nonbpjs')" class="prod-item"><div class="font-bold text-rose-700">NewBike Non-BPJS</div><div class="text-xs text-slate-500 mt-1">SK 155</div></div>
            </div>
          </div>
          <div class="card p-5">
            <div class="space-y-5">
              <div>
                <h3 class="section-title">Data Konsumen</h3>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 gap-4">
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Status Konsumen</label>
                    <select id="nk_status" class="form-input" onchange="updateNorkilUI()">
                      <option value="baru">Konsumen Baru</option>
                      <option value="eksisting">Konsumen Terdaftar</option>
                    </select>
                  </div>
                  <div id="row_rating" class="hidden">
                    <label class="block text-xs font-medium text-slate-600 mb-1">Rating</label>
                    <select id="nk_rating" class="form-input">
                      <option value="excellent">Excellent</option>
                      <option value="good">Good</option>
                      <option value="normal">Normal</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Lama Kerja</label>
                    <select id="nk_lama_kerja" class="form-input">
                      <option value="">Pilih</option>
                      <option value="kurang">Kurang dari 1 Tahun</option>
                      <option value="1tahun">1 Tahun atau Lebih</option>
                      <option value="6bulan">6 Bulan</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Status Rumah</label>
                    <select id="nk_rumah" class="form-input" onchange="updateNorkilUI()">
                      <option value="sendiri">Milik Sendiri/Keluarga</option>
                      <option value="sewa">Sewa/Kontrak/Kost</option>
                    </select>
                  </div>
                  <div id="row_lama_tinggal" class="hidden">
                    <label class="block text-xs font-medium text-slate-600 mb-1">Lama Tinggal (Bulan)</label>
                    <input type="number" id="nk_lama_tinggal" class="form-input" placeholder="Jumlah bulan">
                  </div>
                  <div id="row_region" class="hidden">
                    <label class="block text-xs font-medium text-slate-600 mb-1">Region</label>
                    <select id="nk_region" class="form-input">
                      <option value="lainnya">Lainnya</option>
                      <option value="jabodebek">Jabodebek</option>
                      <option value="banten">Banten</option>
                      <option value="kalimantan">Kalimantan</option>
                      <option value="sulawesi">Sulawesi</option>
                      <option value="jatim_bnt">Jatim BNT</option>
                      <option value="sumbagut">Sumbagut</option>
                      <option value="sumbagsel">Sumbagsel</option>
                      <option value="jabar">Jabar</option>
                      <option value="jatengut">Jateng Utara</option>
                      <option value="jatengsel">Jateng Selatan</option>
                    </select>
                  </div>
                </div>
              </div>

              <div>
                <h3 class="section-title teal">Hasil Pengecekan Data</h3>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
                  <div id="row_dukcapil" class="hidden">
                    <label class="block text-xs font-medium text-slate-600 mb-1">Dukcapil</label>
                    <select id="nk_dukcapil" class="form-input">
                      <option value="match">Match</option>
                      <option value="notmatch">Not Match</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">KBIJ Pemohon</label>
                    <select id="nk_kbij" class="form-input" onchange="updateNorkilUI()">
                      <option value="yes">Yes</option>
                      <option value="no">No</option>
                      <option value="notfound">Not Found</option>
                    </select>
                  </div>
                  <div id="row_kbij_pas">
                    <label class="block text-xs font-medium text-slate-600 mb-1">KBIJ Pasangan</label>
                    <select id="nk_kbij_pas" class="form-input">
                      <option value="yes">Yes</option>
                      <option value="no">No</option>
                      <option value="notfound">Not Found</option>
                      <option value="tidakada">Tidak Ada Pasangan</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Internal Neg List</label>
                    <select id="nk_internal" class="form-input">
                      <option value="tidak">Tidak Termasuk</option>
                      <option value="ya">Termasuk</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Riwayat TB/WO</label>
                    <select id="nk_tbwo" class="form-input">
                      <option value="tidak">Tidak Pernah</option>
                      <option value="ya">Pernah</option>
                    </select>
                  </div>
                </div>
              </div>

              <div id="row_bpjs" class="hidden">
                <h3 class="section-title cyan">Pengecekan BPJS</h3>
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Status BPJS</label>
                    <select id="nk_bpjs_status" class="form-input">
                      <option value="terdaftar">Terdaftar</option>
                      <option value="tidak">Tidak Terdaftar</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Validasi Penghasilan JMO</label>
                    <select id="nk_bpjs_income" class="form-input">
                      <option value="ya">Ya (Tervalidasi)</option>
                      <option value="tidak">Tidak</option>
                    </select>
                  </div>
                </div>
              </div>

              <div>
                <h3 class="section-title cyan">Keuangan</h3>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Jenis Penghasilan</label>
                    <select id="nk_jenis_inc" class="form-input">
                      <option value="fixed">Fixed Income</option>
                      <option value="nonfixed">Non Fixed</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Total Exposure</label>
                    <div class="rp-wrap">
                      <span class="rp-pre">Rp</span>
                      <input type="text" id="nk_exp" class="form-input rp-inp" oninput="formatRupiah(this)" placeholder="0">
                    </div>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Tenor (Bulan)</label>
                    <input type="number" id="nk_tenor" class="form-input" placeholder="Contoh: 36">
                  </div>
                  <div id="row_iir">
                    <label class="block text-xs font-medium text-slate-600 mb-1">Installment Income Ratio (%)</label>
                    <input type="number" id="nk_iir" class="form-input" placeholder="Contoh: 30">
                  </div>
                  <div id="row_dp_perc" class="hidden">
                    <label class="block text-xs font-medium text-slate-600 mb-1">Down Payment (%)</label>
                    <input type="number" id="nk_dp_perc" class="form-input" placeholder="Contoh: 20">
                  </div>
                </div>
              </div>

              <div id="row_kendaraan">
                <h3 class="section-title rose">Data Kendaraan</h3>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 gap-4">
                  <div id="row_jenis_kend">
                    <label class="block text-xs font-medium text-slate-600 mb-1">Jenis Kendaraan</label>
                    <select id="nk_jenis_kend" class="form-input">
                      <option value="passenger">Passenger Car</option>
                      <option value="commercial">Commercial Car</option>
                    </select>
                  </div>
                  <div id="row_kategori_kend">
                    <label class="block text-xs font-medium text-slate-600 mb-1">Kategori</label>
                    <select id="nk_kategori" class="form-input">
                      <option value="A">Kategori A</option>
                      <option value="B">Kategori B</option>
                      <option value="C">Kategori C</option>
                    </select>
                  </div>
                  <div id="row_usia_kend">
                    <label class="block text-xs font-medium text-slate-600 mb-1">Usia Kendaraan (Tahun)</label>
                    <input type="number" id="nk_usia_kend" class="form-input" placeholder="5">
                  </div>
                  <div id="row_bpkb">
                    <label class="block text-xs font-medium text-slate-600 mb-1">Kepemilikan BPKB</label>
                    <select id="nk_bpkb" class="form-input">
                      <option value="sendiri">Sendiri/Pasangan/Ortu</option>
                      <option value="oranglain">Orang Lain</option>
                    </select>
                  </div>
                  <div id="row_pajak">
                    <label class="block text-xs font-medium text-slate-600 mb-1">Pajak Kendaraan</label>
                    <select id="nk_pajak" class="form-input">
                      <option value="hidup">Hidup/Aktif</option>
                      <option value="mati">Mati/Expired</option>
                    </select>
                  </div>
                </div>
              </div>

              <div>
                <h3 class="section-title amber">Dokumen Persyaratan</h3>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-3">
                  <label class="custom-check"><input type="checkbox" id="doc_ktp" checked disabled> E-KTP</label>
                  <label class="custom-check"><input type="checkbox" id="doc_kk" checked disabled> Kartu Keluarga</label>
                  <label class="custom-check"><input type="checkbox" id="doc_rumah"> Bukti Kepemilikan Rumah</label>
                  <label class="custom-check"><input type="checkbox" id="doc_income"> Bukti Penghasilan</label>
                  <label class="custom-check"><input type="checkbox" id="doc_npwp"> NPWP (> 50 Juta)</label>
                </div>
              </div>

              <div class="pt-4 flex justify-end">
                <button onclick="checkNorkil()" class="btn-check">Cek Kelayakan</button>
              </div>
            </div>
          </div>
        </div>
        <div class="col-span-12 lg:col-span-4">
          <div class="sticky top-28">
            <div class="card p-5 bg-white/90 backdrop-blur-sm border-indigo-100">
              <h3 class="section-title">Hasil Analisa</h3>
              <div id="res-norkil" class="text-sm text-slate-500 text-center py-8">Menunggu input...</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ================= DEVIASI PAGE ================= -->
    <section id="page-deviasi" class="page-section">
      <div class="grid grid-cols-12 gap-6">
        <div class="col-span-12 lg:col-span-8 space-y-5">
          <div class="card p-5">
            <div class="mb-4">
              <h2 class="text-lg font-bold text-slate-800">Pendeteksi Deviasi</h2>
              <p class="text-sm text-slate-500">Isi form atau centang jenis deviasi yang terjadi. Kosongkan jika tidak ada.</p>
            </div>
            
            <!-- Info Produk & Status -->
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-5 p-4 bg-indigo-50 rounded-xl">
              <div>
                <label class="block text-xs font-medium text-slate-600 mb-1">Jenis Produk *</label>
                <select id="dev_prod" class="form-input">
                  <option value="motor">MotorKu / NB</option>
                  <option value="mobil">MobilKu</option>
                  <option value="masku">MasKu</option>
                </select>
              </div>
              <div>
                <label class="block text-xs font-medium text-slate-600 mb-1">Status Konsumen *</label>
                <select id="dev_status" class="form-input" onchange="updateDeviasiUI()">
                  <option value="baru">Baru</option>
                  <option value="terdaftar">Terdaftar</option>
                </select>
              </div>
              <div id="dev_row_rating" class="hidden">
                <label class="block text-xs font-medium text-slate-600 mb-1">Rating Internal</label>
                <select id="dev_rating" class="form-input">
                  <option value="none">Normal / Baru</option>
                  <option value="excellent">Excellent</option>
                  <option value="good">Good</option>
                </select>
              </div>
            </div>

            <!-- 01 - Negative List -->
            <div class="dev-cat-box">
              <div class="dev-cat-header">
                <span class="dev-cat-title"><span class="dev-cat-badge">01</span> NEGATIVE LIST</span>
              </div>
              <div class="dev-cat-body">
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Kolektibilitas (Kol)</label>
                    <select id="dev_kol" class="form-input">
                      <option value="">-- Tidak Ada Deviasi --</option>
                      <option value="2">Kol 2</option>
                      <option value="3">Kol 3</option>
                      <option value="4">Kol 4</option>
                      <option value="5">Kol 5</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Baki Debet (Rp)</label>
                    <div class="rp-wrap">
                      <span class="rp-pre">Rp</span>
                      <input type="text" id="dev_bd" class="form-input rp-inp" oninput="formatRupiah(this)" placeholder="0">
                    </div>
                  </div>
                  <div class="flex items-end">
                    <div id="dev_01_result" class="text-xs text-slate-500 italic"></div>
                  </div>
                </div>
              </div>
            </div>

            <!-- 02 - DSR -->
            <div class="dev-cat-box">
              <div class="dev-cat-header">
                <span class="dev-cat-title"><span class="dev-cat-badge">02</span> DSR & MIN PENGHASILAN</span>
              </div>
              <div class="dev-cat-body">
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">DSR (%)</label>
                    <input type="number" id="dev_dsr" class="form-input" placeholder="Contoh: 70">
                  </div>
                  <div class="flex items-end">
                    <div id="dev_02_result" class="text-xs text-slate-500 italic"></div>
                  </div>
                </div>
              </div>
            </div>

            <!-- 03 - Skema Produk -->
            <div class="dev-cat-box">
              <div class="dev-cat-header">
                <span class="dev-cat-title"><span class="dev-cat-badge">03</span> SKEMA PRODUK PEMBIAYAAN</span>
              </div>
              <div class="dev-cat-body space-y-4">
                
                <!-- Tenor -->
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 items-end">
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Tenor (Bulan)</label>
                    <input type="number" id="dev_tenor" class="form-input" placeholder="Contoh: 50">
                  </div>
                  <div id="dev_03_tenor_result" class="text-xs text-slate-500 italic"></div>
                </div>

                <!-- LTV -->
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 items-end">
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Kenaikan LTV (%)</label>
                    <input type="number" id="dev_ltv" class="form-input" placeholder="Contoh: 5">
                  </div>
                  <div id="dev_03_ltv_result" class="text-xs text-slate-500 italic"></div>
                </div>

                <!-- Take Over -->
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 items-end">
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Take Over Fincoy</label>
                    <select id="dev_to" class="form-input">
                      <option value="">-- Tidak Ada --</option>
                      <option value="current">Current</option>
                      <option value="tidakcurrent">Tidak Current</option>
                    </select>
                  </div>
                  <div id="dev_03_to_result" class="text-xs text-slate-500 italic"></div>
                </div>

              </div>
            </div>

            <!-- 04 - Unit Pembiayaan -->
            <div class="dev-cat-box">
              <div class="dev-cat-header">
                <span class="dev-cat-title"><span class="dev-cat-badge">04</span> UNIT PEMBIAYAAN (AGUNAN)</span>
              </div>
              <div class="dev-cat-body grid grid-cols-1 md:grid-cols-2 gap-x-4">
                <label class="custom-check">
                  <input type="checkbox" id="dev_04_faktur">
                  <div>
                    <span class="font-medium">Faktur Tidak Ada</span>
                    <div class="custom-check-desc">C040321(M) - CAC</div>
                  </div>
                </label>
                <label class="custom-check">
                  <input type="checkbox" id="dev_04_unit">
                  <div>
                    <span class="font-medium">Unit Diluar Ketentuan</span>
                    <div class="custom-check-desc">C040621(A/M) - CAM</div>
                  </div>
                </label>
                <label class="custom-check">
                  <input type="checkbox" id="dev_04_kir">
                  <div>
                    <span class="font-medium">KIR Tidak Aktif</span>
                    <div class="custom-check-desc">C040821(M) - CAC</div>
                  </div>
                </label>
                <label class="custom-check">
                  <input type="checkbox" id="dev_04_plat">
                  <div>
                    <span class="font-medium">Plat Beda Provinsi</span>
                    <div class="custom-check-desc">RD585(M) - CAC</div>
                    <span class="dev-note">Wajib BBN atau LTV turun 5%</span>
                  </div>
                </label>
              </div>
            </div>

            <!-- 05 - Profil Konsumen -->
            <div class="dev-cat-box">
              <div class="dev-cat-header">
                <span class="dev-cat-title"><span class="dev-cat-badge">05</span> PROFIL KONSUMEN</span>
              </div>
              <div class="dev-cat-body">
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Usia Pemohon (Tahun)</label>
                    <input type="number" id="dev_usia" class="form-input" placeholder="Contoh: 65">
                  </div>
                  <div class="flex items-end">
                    <div id="dev_05_result" class="text-xs text-slate-500 italic"></div>
                  </div>
                </div>
              </div>
            </div>

            <!-- 06 - Cover Area -->
            <div class="dev-cat-box">
              <div class="dev-cat-header">
                <span class="dev-cat-title"><span class="dev-cat-badge">06</span> COVER AREA & RED AREA</span>
              </div>
              <div class="dev-cat-body grid grid-cols-1 md:grid-cols-2 gap-x-4">
                <label class="custom-check">
                  <input type="checkbox" id="dev_06_red">
                  <div>
                    <span class="font-medium">Red Area</span>
                    <div class="custom-check-desc">C060121(M) - CAM</div>
                    <span class="dev-note">Rekomendasi Collection wajib</span>
                  </div>
                </label>
                <label class="custom-check">
                  <input type="checkbox" id="dev_06_jauh">
                  <div>
                    <span class="font-medium">Cover Area Jauh</span>
                    <div class="custom-check-desc">C060221(M) - CAM</div>
                    <span class="dev-note">Jawa >70KM tidak dapat dibiayai</span>
                  </div>
                </label>
              </div>
            </div>

            <!-- 07 - Dokumen -->
            <div class="dev-cat-box">
              <div class="dev-cat-header">
                <span class="dev-cat-title"><span class="dev-cat-badge">07</span> DOKUMEN PEMBIAYAAN</span>
              </div>
              <div class="dev-cat-body grid grid-cols-1 md:grid-cols-2 gap-x-4">
                <label class="custom-check">
                  <input type="checkbox" id="dev_07_npwp">
                  <div>
                    <span class="font-medium">NPWP Tidak Sesuai</span>
                    <div class="custom-check-desc">C070121(A) - CAC</div>
                    <span class="dev-note">PH > 50 Juta</span>
                  </div>
                </label>
                <label class="custom-check">
                  <input type="checkbox" id="dev_07_ttd">
                  <div>
                    <span class="font-medium">Pasangan Tidak TTD</span>
                    <div class="custom-check-desc">RD567(A) - CAC</div>
                    <span class="dev-note">Isi Form F-179</span>
                  </div>
                </label>
              </div>
            </div>

            <div class="pt-4 flex justify-end">
              <button onclick="checkDeviasi()" class="btn-check">Cek Level Approval</button>
            </div>
          </div>
        </div>
        <div class="col-span-12 lg:col-span-4">
          <div class="sticky top-28">
            <div class="card p-5 bg-white/90 backdrop-blur-sm border-teal-100">
              <h3 class="section-title">Hasil Deteksi</h3>
              <div id="res-deviasi" class="text-sm text-slate-500 text-center py-8">Menunggu input...</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ================= SUPER PAGE ================= -->
    <section id="page-super" class="page-section">
      <div class="grid grid-cols-12 gap-6">
        <div class="col-span-12 lg:col-span-8 space-y-5">
          <div class="card p-5">
            <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center mb-5 border-b pb-4 gap-3">
              <div>
                <h2 class="text-lg font-bold text-slate-800">MobilKu Super</h2>
                <p class="text-xs text-slate-500">Program Khusus</p>
              </div>
              <div class="flex bg-slate-100 rounded-lg p-1">
                <button id="super-ro" onclick="setSuperType('ro')" class="super-tab active">RO Super</button>
                <button id="super-to" onclick="setSuperType('to')" class="super-tab">Take Over</button>
                <button id="super-nc" onclick="setSuperType('nc')" class="super-tab">NC Super</button>
              </div>
            </div>

            <div class="space-y-5">
              <div>
                <h3 class="section-title">Data Konsumen</h3>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 gap-4">
                  <div id="sp_row_jenis_kons" class="hidden">
                    <label class="block text-xs font-medium text-slate-600 mb-1">Jenis Konsumen</label>
                    <select id="sp_jenis_kons" class="form-input">
                      <option value="terdaftar">Konsumen Terdaftar</option>
                      <option value="baru">Konsumen Baru</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Rating Konsumen</label>
                    <select id="sp_rating" class="form-input">
                      <option value="excellent">Excellent</option>
                      <option value="good">Good</option>
                      <option value="normal">Normal</option>
                      <option value="warning">Warning</option>
                      <option value="bad">Bad Customer</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Usia Pemohon</label>
                    <input type="number" id="sp_usia" class="form-input" placeholder="Tahun">
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Jenis Pekerjaan</label>
                    <select id="sp_kerja" class="form-input">
                      <option value="karyawan">Karyawan</option>
                      <option value="wiraswasta">Wiraswasta</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Status Rumah</label>
                    <select id="sp_rumah" class="form-input">
                      <option value="milik">Milik Sendiri/Keluarga</option>
                      <option value="sewa">Sewa/Kontrak/Kost</option>
                    </select>
                  </div>
                </div>
              </div>

              <div>
                <h3 class="section-title teal">Pengecekan Negative List</h3>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">KBIJ Pemohon</label>
                    <select id="sp_kbij" class="form-input">
                      <option value="yes">Yes</option>
                      <option value="no">No</option>
                      <option value="notfound">Not Found</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Internal Neg List</label>
                    <select id="sp_internal" class="form-input">
                      <option value="tidak">Tidak Termasuk</option>
                      <option value="ya">Termasuk</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Riwayat TB/WO</label>
                    <select id="sp_tbwo" class="form-input">
                      <option value="tidak">Tidak Pernah</option>
                      <option value="ya">Pernah</option>
                    </select>
                  </div>
                </div>
              </div>

              <div>
                <h3 class="section-title cyan">Keuangan</h3>
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">IIR (%)</label>
                    <input type="number" id="sp_iir" class="form-input" placeholder="30">
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Maksimal LTV (%)</label>
                    <input type="number" id="sp_ltv" class="form-input" placeholder="90">
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Tenor (Bulan)</label>
                    <input type="number" id="sp_tenor" class="form-input" placeholder="48">
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Total Exposure</label>
                    <div class="rp-wrap">
                      <span class="rp-pre">Rp</span>
                      <input type="text" id="sp_exp" class="form-input rp-inp" oninput="formatRupiah(this)">
                    </div>
                  </div>
                </div>
              </div>

              <div>
                <h3 class="section-title rose">Data Kendaraan</h3>
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Jenis Kendaraan</label>
                    <select id="sp_jenis" class="form-input">
                      <option value="passenger">Passenger</option>
                      <option value="commercial">Commercial</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Usia Kendaraan (Tahun)</label>
                    <input type="number" id="sp_usia_kend" class="form-input" placeholder="5">
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Kepemilikan BPKB</label>
                    <select id="sp_bpkb" class="form-input">
                      <option value="sendiri">Sendiri/Pasangan/Ortu</option>
                      <option value="oranglain">Orang Lain</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Status STNK</label>
                    <select id="sp_stnk" class="form-input">
                      <option value="hidup">Hidup</option>
                      <option value="mati">Mati</option>
                    </select>
                  </div>
                </div>
              </div>

              <div id="row_to_specific" class="hidden">
                <h3 class="section-title amber">Data Take Over</h3>
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Angsuran Dibayar (Bulan)</label>
                    <input type="number" id="sp_to_bayar" class="form-input" placeholder="12">
                  </div>
                  <div>
                    <label class="block text-xs font-medium text-slate-600 mb-1">Maksimal Overdue</label>
                    <select id="sp_to_od" class="form-input">
                      <option value="kurang">Kurang dari 14 Hari</option>
                      <option value="lebih">Lebih dari 14 Hari</option>
                    </select>
                  </div>
                </div>
              </div>

              <div>
                <h3 class="section-title">Dokumen Pembiayaan</h3>
                <div class="grid grid-cols-2 gap-3">
                  <label class="custom-check"><input type="checkbox" id="sp_doc_ktp" checked disabled> E-KTP</label>
                  <label class="custom-check"><input type="checkbox" id="sp_doc_kk" checked disabled> KK</label>
                  <label class="custom-check"><input type="checkbox" id="sp_doc_rumah"> Bukti Kepemilikan Rumah</label>
                  <label class="custom-check"><input type="checkbox" id="sp_doc_income"> Bukti Penghasilan</label>
                  <label class="custom-check"><input type="checkbox" id="sp_doc_npwp"> NPWP</label>
                </div>
              </div>

              <div class="pt-4 flex justify-end">
                <button onclick="checkSuper()" class="btn-check">Cek Kelayakan Super</button>
              </div>
            </div>
          </div>
        </div>
        <div class="col-span-12 lg:col-span-4">
          <div class="sticky top-28">
            <div class="card p-5 bg-white/90 backdrop-blur-sm border-rose-100">
              <h3 class="section-title">Hasil Evaluasi</h3>
              <div id="res-super" class="text-sm text-slate-500 text-center py-8">Menunggu input...</div>
            </div>
          </div>
        </div>
      </div>
    </section>

  </main>

  <script>
    /* ===== UTILITIES ===== */
    const $ = (id) => document.getElementById(id);
    const formatRupiah = (input) => { let value = input.value.replace(/\D/g, ''); input.value = new Intl.NumberFormat('id-ID').format(value); };
    const parseNum = (str) => { if (!str) return 0; return parseInt(str.toString().replace(/\D/g, ''), 10) || 0; };
    const getVal = (id) => $(id) ? $(id).value : '';
    const formatCurr = (num) => 'Rp ' + new Intl.NumberFormat('id-ID').format(num);

    /* ===== NAVIGATION ===== */
    function navigatePage(pageName) {
      document.querySelectorAll('.page-section').forEach(el => el.classList.remove('active'));
      document.querySelectorAll('.nav-tab').forEach(el => el.classList.remove('active'));
      $('page-' + pageName).classList.add('active');
      $('btn-' + pageName).classList.add('active');
    }

    /* ===== NORMAL KILAT ===== */
    let currentProduct = 'mobilku';
    
    function selectProduct(prod) {
      currentProduct = prod;
      document.querySelectorAll('.prod-item').forEach(c => c.classList.remove('active'));
      $('prod-' + prod).classList.add('active');
      updateNorkilUI();
    }

    function updateNorkilUI() {
      const status = getVal('nk_status');
      const rumah = getVal('nk_rumah');
      
      if (status === 'eksisting') $('row_rating').classList.remove('hidden');
      else $('row_rating').classList.add('hidden');

      if (rumah === 'sewa') $('row_lama_tinggal').classList.remove('hidden');
      else $('row_lama_tinggal').classList.add('hidden');

      ['row_dp_perc', 'row_region', 'row_bpjs', 'row_dukcapil', 'row_kbij_pas', 'row_jenis_kend', 'row_kategori_kend', 'row_usia_kend', 'row_pajak'].forEach(id => {
        if($(id)) $(id).classList.add('hidden');
      });

      if (currentProduct === 'mobilku') {
        $('row_dukcapil').classList.remove('hidden');
        $('row_kbij_pas').classList.remove('hidden');
        $('row_jenis_kend').classList.remove('hidden');
        $('row_kategori_kend').classList.remove('hidden');
        $('row_usia_kend').classList.remove('hidden');
        $('row_bpkb').classList.remove('hidden');
        $('row_pajak').classList.remove('hidden');
      } 
      else if (currentProduct === 'motorku') {
        $('row_usia_kend').classList.remove('hidden');
        $('row_bpkb').classList.remove('hidden');
        $('row_region').classList.remove('hidden');
        $('row_pajak').classList.remove('hidden');
      }
      else if (currentProduct === 'newbike_bpjs') {
        $('row_bpjs').classList.remove('hidden');
        $('row_dp_perc').classList.remove('hidden');
        $('row_bpkb').classList.remove('hidden');
        $('row_pajak').classList.remove('hidden');
      }
      else if (currentProduct === 'newbike_nonbpjs') {
        $('row_dp_perc').classList.remove('hidden');
        $('row_region').classList.remove('hidden');
        $('row_bpkb').classList.remove('hidden');
        $('row_pajak').classList.remove('hidden');
      }
    }

    function checkNorkil() {
      let res = [];
      let status = 'pass';
      const exp = parseNum(getVal('nk_exp'));
      const statusKonsumen = getVal('nk_status');

      if (getVal('nk_internal') === 'ya') { res.push({t: 'fail', m: 'Terindikasi Internal Negative List.'}); status='fail'; }
      if (getVal('nk_tbwo') === 'ya') { res.push({t: 'fail', m: 'Memiliki riwayat TB/WO.'}); status='fail'; }

      if (currentProduct === 'mobilku') {
        if (getVal('nk_dukcapil') !== 'match') { res.push({t: 'fail', m: 'Dukcapil Wajib Match.'}); status='fail'; }
        if (getVal('nk_lama_kerja') !== '1tahun') { res.push({t: 'fail', m: 'Lama Kerja minimal 1 Tahun.'}); status='fail'; }
        if (getVal('nk_rumah') === 'sewa') { res.push({t: 'fail', m: 'Status sewa tidak diperbolehkan.'}); status='fail'; }
        
        const kbij = getVal('nk_kbij'); const kbijPas = getVal('nk_kbij_pas');
        if (kbij === 'notfound' && kbijPas !== 'yes') { res.push({t: 'fail', m: 'KBIJ Pemohon & Pasangan NF -> Tidak Dapat Diproses.'}); status='fail'; }
        if (kbij === 'no') { res.push({t: 'fail', m: 'KBIJ No tidak diperbolehkan Normal Kilat.'}); status='fail'; }

        if (getVal('nk_kategori') !== 'A') { res.push({t: 'fail', m: 'Hanya Kategori A.'}); status='fail'; }
        
        const usiaKend = parseNum(getVal('nk_usia_kend'));
        if (usiaKend > 10) { res.push({t: 'fail', m: 'Usia kendaraan > 10 tahun.'}); status='fail'; }
        
        if (getVal('nk_bpkb') === 'oranglain') { res.push({t: 'warn', m: 'BPKB Orang Lain WAJIB BBN.'}); if(status!=='fail')status='warn'; }
        if (exp > 175000000) { res.push({t: 'fail', m: 'Exposure > 175 Juta.'}); status='fail'; }
        
        const iir = parseNum(getVal('nk_iir')); const maxIIR = getVal('nk_jenis_inc') === 'fixed' ? 40 : 30;
        if (iir > maxIIR) { res.push({t: 'fail', m: 'IIR ' + iir + '% > Max ' + maxIIR + '%.'}); status='fail'; }
        if (getVal('nk_pajak') === 'mati') { res.push({t: 'warn', m: 'Pajak Mati: Wajib perpanjangan.'}); if(status!=='fail')status='warn'; }
      } 
      else if (currentProduct === 'motorku') {
        const rating = getVal('nk_rating');
        const maxExp = statusKonsumen === 'baru' ? 25000000 : 45000000;
        if (exp > maxExp) { res.push({t: 'fail', m: 'Exposure > ' + formatCurr(maxExp) + '.'}); status='fail'; }
        if (getVal('nk_pajak') === 'mati') { res.push({t: 'warn', m: 'Pajak Mati -> LTV Turun 10%.'}); if(status!=='fail')status='warn'; }
        if (getVal('nk_rumah') === 'sewa') {
          if (statusKonsumen === 'baru' || rating === 'normal') { res.push({t: 'fail', m: 'Tidak diperbolehkan sewa.'}); status='fail'; }
        }
      } 
      else if (currentProduct === 'newbike_bpjs') {
        if (getVal('nk_bpjs_status') !== 'terdaftar') { res.push({t: 'fail', m: 'Wajib terdaftar BPJS.'}); status='fail'; }
        if (getVal('nk_bpjs_income') !== 'ya') { res.push({t: 'fail', m: 'Penghasilan JMO wajib tervalidasi.'}); status='fail'; }
        if (exp > 45000000) { res.push({t: 'fail', m: 'Max Exposure 45 Juta.'}); status='fail'; }
        
        const dpPerc = parseNum(getVal('nk_dp_perc'));
        if (getVal('nk_rumah') === 'sewa') {
           if (parseNum(getVal('nk_lama_tinggal')) < 12) { res.push({t: 'fail', m: 'Sewa min 12 bln tinggal.'}); status='fail'; }
           else if (dpPerc < 15) { res.push({t: 'fail', m: 'Sewa -> Min DP 15%.'}); status='fail'; }
        } else {
          if (dpPerc < 5) { res.push({t: 'fail', m: 'Min DP 5%.'}); status='fail'; }
        }
        if (parseNum(getVal('nk_iir')) > 45) { res.push({t: 'fail', m: 'IIR > 45%.'}); status='fail'; }
      } 
      else if (currentProduct === 'newbike_nonbpjs') {
        if (exp > 45000000) { res.push({t: 'fail', m: 'Max Exposure 45 Juta.'}); status='fail'; }
        const dpPerc = parseNum(getVal('nk_dp_perc'));
        if (getVal('nk_rumah') === 'sewa') {
           if (parseNum(getVal('nk_lama_tinggal')) < 12) { res.push({t: 'fail', m: 'Sewa min 12 bln tinggal.'}); status='fail'; }
           else if (dpPerc < 15) { res.push({t: 'fail', m: 'Sewa -> Min DP 15%.'}); status='fail'; }
        } else {
          const rating = getVal('nk_rating');
          if (statusKonsumen === 'eksisting' && (rating === 'excellent' || rating === 'good') && dpPerc < 8) { res.push({t: 'fail', m: 'Exc/Good -> Min DP 8%.'}); status='fail'; }
        }
        let maxIIR = getVal('nk_jenis_inc') === 'fixed' ? 30 : 25;
        const region = getVal('nk_region');
        if (region === 'jatengsel' || region === 'jatengut' || region === 'jabar') maxIIR += 5;
        if (parseNum(getVal('nk_iir')) > maxIIR) { res.push({t: 'fail', m: 'IIR > ' + maxIIR + '%.'}); status='fail'; }
      }

      renderResult('res-norkil', res, status);
    }

    /* ===== DEVIASI LOGIC ===== */
    const approvalHierarchy = ['CAC', 'CAM', 'CDH', 'CDDH', 'CADH', 'CRO', 'VPD', 'PD'];

    function updateDeviasiUI() {
      const status = getVal('dev_status');
      if (status === 'terdaftar') $('dev_row_rating').classList.remove('hidden');
      else $('dev_row_rating').classList.add('hidden');
    }

    // Helper Functions
    function getNegListDev(kol, bd) {
      bd = bd || 0;
      if (kol == 5) {
        if (bd > 50000000) return { code: 'C010124(M)', desc: 'Kol 5 BD > 50 Jt', app: 'CRO' };
        if (bd > 30000000) return { code: 'C010224(M)', desc: 'Kol 5 BD 30-50 Jt', app: 'CADH' };
        if (bd > 5000000) return { code: 'C010424(M)', desc: 'Kol 5 BD 5-30 Jt', app: 'CDDH' };
        if (bd > 1000000) return { code: 'C010724(M)', desc: 'Kol 5 BD 1-5 Jt', app: 'CDH' };
        return { code: 'C010924(M)', desc: 'Kol 5 BD <= 1 Jt', app: 'CAM' };
      }
      if (kol == 4) {
        if (bd > 50000000) return { code: 'C010324(M)', desc: 'Kol 4 BD > 50 Jt', app: 'CADH' };
        return { code: 'C010524(M)', desc: 'Kol 4 BD <= 50 Jt', app: 'CDDH' };
      }
      if (kol == 3) {
        if (bd > 50000000) return { code: 'C010624(M)', desc: 'Kol 3 BD > 50 Jt', app: 'CDDH' };
        if (bd > 5000000) return { code: 'C011024(M)', desc: 'Kol 3 BD 5-50 Jt', app: 'CAM' };
        return { code: 'C011224(M)', desc: 'Kol 3 BD <= 5 Jt', app: 'CAC' };
      }
      if (kol == 2) {
        if (bd > 50000000) return { code: 'C010824(M)', desc: 'Kol 2 BD > 50 Jt', app: 'CDH' };
        if (bd > 5000000) return { code: 'C011124(M)', desc: 'Kol 2 BD 5-50 Jt', app: 'CAM' };
        return { code: 'C011324(M)', desc: 'Kol 2 BD <= 5 Jt', app: 'CAC' };
      }
      return null;
    }

    function getDSRDev(dsr) {
      if(dsr > 80) return { code: 'RD653(M)', desc: 'DSR > 80%', app: 'CDH' };
      if(dsr > 65) return { code: 'C020422(A)', desc: 'DSR 65-80%', app: 'CAM' };
      if(dsr > 55) return { code: 'C020222(A)', desc: 'DSR 30-55%', app: 'CAC' };
      return null;
    }

    function getUsiaDev(usia) {
      if(usia > 70) return { code: 'REJECT', desc: 'Usia > 70 Thn', app: 'REJECT' };
      if(usia > 60) return { code: 'C050221(A)', desc: 'Usia > 60 s.d 70 Thn', app: 'CAC' };
      if(usia < 21) return { code: 'C050721(A)', desc: 'Usia < 21 Thn', app: 'CAM' };
      return null;
    }

    function getTenorDev(tenor, prod) {
      if (prod === 'mobil') {
        if (tenor > 48 && tenor <= 60) return { code: 'C030124(M)', desc: 'Tenor > 48-60 Bulan', app: 'CAC', note: 'Maks LTV 85%' };
      } else {
        // Motor / NB
        if (tenor > 36 && tenor <= 48) return { code: 'C030121(M)', desc: 'Tenor 36-48 Bulan', app: 'CAC' };
        if (tenor > 48 && tenor <= 60) return { code: 'C030125(M)', desc: 'Tenor > 48-60 Bulan', app: 'CAM' };
      }
      return null;
    }

    function getLTVDev(ltv) {
      if (ltv > 10) return { code: 'C030921(M)', desc: 'LTV Naik > 10%', app: 'CAM', note: 'Maks LTV >90% tdk dibiayai' };
      if (ltv > 0) return { code: 'C030821(M)', desc: 'LTV Naik s.d 10%', app: 'CAC' };
      return null;
    }

    function getTODev(to) {
      if (to === 'current') return { code: 'C030123(M)', desc: 'Take Over Fincoy Current', app: 'CAC', note: 'Historikal < 9 bln' };
      if (to === 'tidakcurrent') return { code: 'C031111(M)', desc: 'Take Over Fincoy Tidak Current', app: 'CAM', note: 'Historikal < 9 bln' };
      return null;
    }

    function checkDeviasi() {
      const prod = getVal('dev_prod');
      const status = getVal('dev_status');
      if (!prod || !status) {
         alert('Jenis Produk dan Status Konsumen wajib diisi.');
         return;
      }

      let res = [];
      let highestApp = 'CAC';
      let groupCount = new Set();
      let requireIM = false;
      let hasReject = false;

      // 01 - Negative List
      const kol = getVal('dev_kol');
      const bd = parseNum(getVal('dev_bd'));
      if (kol) {
        const dev = getNegListDev(kol, bd);
        if (dev) {
          groupCount.add('01');
          res.push({ t: dev.app === 'REJECT' ? 'fail' : (dev.app === 'CAC' ? 'pass' : 'warn'), m: `<strong>Negative List</strong><br>${dev.code} - ${dev.desc}<br>Wewenang: ${dev.app}` });
          if (dev.app === 'REJECT') hasReject = true;
          if (approvalHierarchy.indexOf(dev.app) > approvalHierarchy.indexOf(highestApp)) highestApp = dev.app;
        }
      }

      // 02 - DSR
      const dsr = parseNum(getVal('dev_dsr'));
      if (dsr > 0) {
        const dev = getDSRDev(dsr);
        if (dev) {
          groupCount.add('02');
          res.push({ t: dev.app === 'REJECT' ? 'fail' : (dev.app === 'CAC' ? 'pass' : 'warn'), m: `<strong>DSR & Min Penghasilan</strong><br>${dev.code} - ${dev.desc}<br>Wewenang: ${dev.app}` });
          if (approvalHierarchy.indexOf(dev.app) > approvalHierarchy.indexOf(highestApp)) highestApp = dev.app;
        }
      }

      // 03 - Skema Produk
      let devs03 = [];
      
      // Tenor
      const tenor = parseNum(getVal('dev_tenor'));
      if (tenor > 0) {
        const dev = getTenorDev(tenor, prod);
        if (dev) devs03.push(dev);
      }

      // LTV
      const ltv = parseNum(getVal('dev_ltv'));
      if (ltv > 0) {
        const dev = getLTVDev(ltv);
        if (dev) devs03.push(dev);
      }

      // Take Over
      const to = getVal('dev_to');
      if (to) {
        const dev = getTODev(to);
        if (dev) devs03.push(dev);
      }

      if (devs03.length > 0) {
        groupCount.add('03');
        devs03.forEach(dev => {
          let noteHtml = dev.note ? `<span class="dev-note">${dev.note}</span>` : '';
          res.push({ t: dev.app === 'CAC' ? 'pass' : 'warn', m: `<strong>Skema Produk</strong><br>${dev.code} - ${dev.desc}<br>Wewenang: ${dev.app}${noteHtml}` });
          if (approvalHierarchy.indexOf(dev.app) > approvalHierarchy.indexOf(highestApp)) highestApp = dev.app;
        });
      }

      // 04 - Unit Pembiayaan
      let devs04 = [];
      if ($('dev_04_faktur').checked) devs04.push({ code: 'C040321(M)', desc: 'Faktur Tidak Ada', app: 'CAC' });
      if ($('dev_04_unit').checked) devs04.push({ code: 'C040621(A/M)', desc: 'Unit Diluar Ketentuan', app: 'CAM' });
      if ($('dev_04_kir').checked) devs04.push({ code: 'C040821(M)', desc: 'KIR Tidak Aktif', app: 'CAC' });
      if ($('dev_04_plat').checked) devs04.push({ code: 'RD585(M)', desc: 'Plat Beda Provinsi', app: 'CAC', note: 'Wajib BBN atau LTV turun 5%' });
      
      if (devs04.length > 0) {
        groupCount.add('04');
        devs04.forEach(dev => {
          let noteHtml = dev.note ? `<span class="dev-note">${dev.note}</span>` : '';
          res.push({ t: dev.app === 'CAC' ? 'pass' : 'warn', m: `<strong>Unit Pembiayaan</strong><br>${dev.code} - ${dev.desc}<br>Wewenang: ${dev.app}${noteHtml}` });
          if (approvalHierarchy.indexOf(dev.app) > approvalHierarchy.indexOf(highestApp)) highestApp = dev.app;
        });
      }

      // 05 - Profil Konsumen
      const usia = parseNum(getVal('dev_usia'));
      if (usia > 0) {
        const dev = getUsiaDev(usia);
        if (dev) {
          groupCount.add('05');
          res.push({ t: dev.app === 'REJECT' ? 'fail' : (dev.app === 'CAC' ? 'pass' : 'warn'), m: `<strong>Profil Konsumen</strong><br>${dev.code} - ${dev.desc}<br>Wewenang: ${dev.app}` });
          if (dev.app === 'REJECT') hasReject = true;
          if (approvalHierarchy.indexOf(dev.app) > approvalHierarchy.indexOf(highestApp)) highestApp = dev.app;
        }
      }

      // 06 - Cover Area
      let devs06 = [];
      if ($('dev_06_red').checked) devs06.push({ code: 'C060121(M)', desc: 'Red Area', app: 'CAM', note: 'Rekomendasi Collection wajib' });
      if ($('dev_06_jauh').checked) devs06.push({ code: 'C060221(M)', desc: 'Cover Area Jauh', app: 'CAM', note: 'Jawa >70KM tidak dibiayai' });
      
      if (devs06.length > 0) {
        groupCount.add('06');
        devs06.forEach(dev => {
          let noteHtml = dev.note ? `<span class="dev-note">${dev.note}</span>` : '';
          res.push({ t: dev.app === 'CAC' ? 'pass' : 'warn', m: `<strong>Cover Area</strong><br>${dev.code} - ${dev.desc}<br>Wewenang: ${dev.app}${noteHtml}` });
          if (approvalHierarchy.indexOf(dev.app) > approvalHierarchy.indexOf(highestApp)) highestApp = dev.app;
        });
      }

      // 07 - Dokumen
      let devs07 = [];
      if ($('dev_07_npwp').checked) devs07.push({ code: 'C070121(A)', desc: 'NPWP Tidak Sesuai', app: 'CAC', note: 'PH > 50 Juta' });
      if ($('dev_07_ttd').checked) devs07.push({ code: 'RD567(A)', desc: 'Pasangan Tidak TTD', app: 'CAC', note: 'Isi Form F-179' });
      
      if (devs07.length > 0) {
        groupCount.add('07');
        devs07.forEach(dev => {
          let noteHtml = dev.note ? `<span class="dev-note">${dev.note}</span>` : '';
          res.push({ t: dev.app === 'CAC' ? 'pass' : 'warn', m: `<strong>Dokumen</strong><br>${dev.code} - ${dev.desc}<br>Wewenang: ${dev.app}${noteHtml}` });
          if (approvalHierarchy.indexOf(dev.app) > approvalHierarchy.indexOf(highestApp)) highestApp = dev.app;
        });
      }

      if (groupCount.size > 3) {
        requireIM = true;
        res.push({ t: 'warn', m: '<strong>PERINGATAN:</strong> Lebih dari 3 Group Deviasi. Wajib melampirkan IM Paper.' });
      }

      let statusRes = 'pass';
      if (hasReject) statusRes = 'fail';
      else if (highestApp !== 'CAC' || requireIM) statusRes = 'warn';
      
      res.push({ t: statusRes, m: `<strong>Approval Final: ${highestApp}</strong>` });

      renderResult('res-deviasi', res, statusRes);
    }

    /* ===== SUPER ===== */
    let superType = 'ro';
    function setSuperType(t) {
      superType = t;
      $('super-ro').className = "super-tab"; $('super-to').className = "super-tab"; $('super-nc').className = "super-tab";
      $(t === 'ro' ? 'super-ro' : (t === 'to' ? 'super-to' : 'super-nc')).className = "super-tab active";
      $('row_to_specific').classList.toggle('hidden', t !== 'to');
      $('sp_row_jenis_kons').classList.toggle('hidden', t !== 'to');
    }

    function checkSuper() {
      let res = [], status = 'pass'; 
      
      const rating = getVal('sp_rating'), exp = parseNum(getVal('sp_exp')), usia = parseNum(getVal('sp_usia')), usiaKend = parseNum(getVal('sp_usia_kend')), iir = parseNum(getVal('sp_iir')), tenor = parseNum(getVal('sp_tenor')), jenisKend = getVal('sp_jenis');
      const ltv = parseNum(getVal('sp_ltv')); // Added LTV check variable
      
      if (rating === 'warning' || rating === 'bad') { res.push({t: 'fail', m: 'Rating Warning/Bad tidak dibiayai.'}); status='fail'; }
      if (getVal('sp_internal') === 'ya') { res.push({t: 'fail', m: 'Internal Negative List.'}); status='fail'; }
      if (getVal('sp_tbwo') === 'ya') { res.push({t: 'fail', m: 'Riwayat TB/WO.'}); status='fail'; }
      if (getVal('sp_kbij') === 'no') { res.push({t: 'fail', m: 'KBIJ No tidak diperbolehkan.'}); status='fail'; }
      if (usia > 60) { res.push({t: 'fail', m: 'Usia max 60 Thn.'}); status='fail'; }
      if (getVal('sp_rumah') === 'sewa') { res.push({t: 'fail', m: 'Tidak boleh sewa.'}); status='fail'; }
      if (exp > 250000000) { res.push({t: 'fail', m: 'Max Exposure 250 Jt.'}); status='fail'; }
      
      const maxIIR = superType === 'ro' ? 40 : 30;
      if (iir > maxIIR) { res.push({t: 'fail', m: 'IIR ' + iir + '% > Max ' + maxIIR + '%.'}); status='fail'; }

      // LTV Check (SK MobilKu Super - Passenger A Max 95%)
      if (jenisKend === 'passenger' && ltv > 95) { 
        res.push({t: 'warn', m: 'LTV > 95% (Deviasi)'}); 
        if(status!=='fail')status='warn'; 
      } else if (jenisKend === 'commercial' && ltv > 80) { 
        // Assuming standard Commercial limit if not specified in Super SK
        res.push({t: 'warn', m: 'LTV Commercial > 80% (Cek Ketentuan)'}); 
        if(status!=='fail')status='warn'; 
      } else {
        res.push({t: 'pass', m: 'LTV Sesuai Ketentuan Super'});
      }

      let maxAge = (superType === 'ro' && jenisKend === 'passenger') ? 17 : 10;
      if (superType === 'to') maxAge = 10;
      if (usiaKend > maxAge) { res.push({t: 'fail', m: 'Usia kendaraan > ' + maxAge + ' thn.'}); status='fail'; }

      if (tenor > 48) { res.push({t: 'warn', m: 'Tenor > 48 = Deviasi.'}); if(status!=='fail')status='warn'; }

      if (superType === 'to') {
        const jenisKons = getVal('sp_jenis_kons');
        if (jenisKons === 'baru') { res.push({t: 'fail', m: 'Konsumen Baru tidak diperbolehkan.'}); status='fail'; }
        if (parseNum(getVal('sp_to_bayar')) < 12) { res.push({t: 'fail', m: 'Min 12 bln pembayaran.'}); status='fail'; }
        if (getVal('sp_to_od') !== 'kurang') { res.push({t: 'warn', m: 'Overdue > 14 hari = Deviasi.'}); if(status!=='fail')status='warn'; }
        
        const appLevel = exp > 75000000 ? 'CMG' : 'CAC';
        res.push({t: 'warn', m: '<strong>Approval Level: ' + appLevel + '</strong>'});
      }
      
      if (getVal('sp_stnk') === 'mati') { res.push({t: 'warn', m: 'STNK Mati: Wajib perpanjangan.'}); if(status!=='fail')status='warn'; }
      if (getVal('sp_bpkb') === 'oranglain') { res.push({t: 'warn', m: 'BPKB Orang Lain: Wajib BBN.'}); if(status!=='fail')status='warn'; }

      renderResult('res-super', res, status);
    }

    /* ===== RENDER ===== */
    function renderResult(containerId, items, globalStatus) {
      const container = $(containerId); let html = '';
      let statusClass = 'status-warn'; let statusText = 'Layak dengan Catatan'; let icon = '!';
      if (globalStatus === 'pass') { statusClass = 'status-pass'; statusText = 'Layak Kredit'; icon = '✓'; }
      if (globalStatus === 'fail') { statusClass = 'status-fail'; statusText = 'Tidak Layak'; icon = '✗'; }
      html += '<div class="status-badge ' + statusClass + ' mb-4 justify-center text-sm">' + icon + ' ' + statusText + '</div>';
      html += '<div class="space-y-1">';
      items.forEach(item => {
        const i = item.t === 'pass' ? '<span class="text-green-500 font-bold">✓</span>' : (item.t === 'fail' ? '<span class="text-red-500 font-bold">✗</span>' : '<span class="text-amber-500 font-bold">!</span>');
        html += '<div class="result-item"><div class="w-5 flex-shrink-0">' + i + '</div><div class="text-slate-600 text-xs">' + item.m + '</div></div>';
      });
      html += '</div>';
      container.innerHTML = html;
    }

    // Init
    updateNorkilUI();
    updateDeviasiUI();
    setSuperType('ro');
  </script>
</body>
</html>
