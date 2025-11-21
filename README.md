<!DOCTYPE html>
<html lang="id" class="scroll-smooth">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Client Management System</title>

  <!-- Tailwind config: enable class-based dark mode -->
  <script>
    window.tailwind = window.tailwind || {};
    window.tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            brandBlue: '#2563eb'
          }
        }
      }
    };
  </script>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

  <style>
    @keyframes fadeIn { 0% { opacity: 0; transform: translateY(8px);} 100% { opacity: 1; transform: translateY(0);} }
    .fade-in { animation: fadeIn 0.5s ease-out forwards; }
    .hidden-section { display: none; }
    .glass { background: rgba(236, 123, 123, 0.6); backdrop-filter: blur(6px); }
    /* make interactive elements clearly clickable */
    .nav-link, button, a { cursor: pointer; }
  </style>
</head>

<body class="min-h-screen bg-gradient-to-br from-blue-50 via-purple-50 to-pink-50 dark:from-gray-900 dark:via-purple-900/20 dark:to-blue-900/20 text-gray-800 dark:text-gray-200 font-sans">
  
  <!-- Auth Screen (shown first) -->
  <div id="authScreen" class="fixed inset-0 z-50 bg-gradient-to-br from-blue-50 via-purple-50 to-pink-50 dark:from-gray-900 dark:via-purple-900/20 dark:to-blue-900/20 flex items-center justify-center p-4">
    <div class="w-full max-w-md">
      <!-- Logo/Brand -->
      <div class="text-center mb-8">
        <h1 class="text-3xl font-bold text-brandBlue mb-2">Client Management System</h1>
        <p class="text-gray-600 dark:text-gray-400">Kelola klien dan proyek Anda dengan mudah</p>
      </div>

      <!-- Auth Card -->
      <div class="bg-white dark:bg-gray-800 rounded-xl shadow-xl p-6">
        <div class="flex items-center justify-between mb-6">
          <h3 id="authTitle" class="text-xl font-semibold">Masuk</h3>
          <button id="themeToggleAuth" class="p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700" title="Toggle theme">
            <svg class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
              <path d="M17.293 13.293A8 8 0 116.707 2.707a8.001 8.001 0 0010.586 10.586z"/>
            </svg>
          </button>
        </div>

        <!-- Auth Forms -->
        <div id="authForms">
          <form id="authLoginForm" class="space-y-4">
            <div>
              <label class="block text-sm font-medium mb-1">Email</label>
              <input id="a_loginEmail" type="email" required class="w-full px-4 py-2 rounded-lg border focus:ring-2 focus:ring-brandBlue focus:border-transparent dark:bg-gray-700" placeholder="email@contoh.com" />
            </div>
            <div>
              <label class="block text-sm font-medium mb-1">Kata Sandi</label>
              <div class="relative">
                <input id="a_loginPassword" type="password" required class="w-full px-4 py-2 rounded-lg border focus:ring-2 focus:ring-brandBlue focus:border-transparent dark:bg-gray-700" placeholder="••••••••" />
                <button type="button" id="a_loginTogglePass" class="absolute right-3 top-2.5 text-sm text-gray-500 hover:text-gray-700">Tampilkan</button>
              </div>
            </div>
            <button id="a_loginBtn" class="w-full bg-brandBlue text-white py-3 rounded-lg font-medium hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
              Masuk
            </button>
            <p class="text-sm text-center">
              Belum punya akun? <button id="a_showRegister" class="text-brandBlue hover:text-blue-700">Daftar</button>
            </p>
          </form>

          <form id="authRegisterForm" class="hidden space-y-4">
            <div>
              <label class="block text-sm font-medium mb-1">Nama Lengkap</label>
              <input id="a_regName" type="text" required class="w-full px-4 py-2 rounded-lg border focus:ring-2 focus:ring-brandBlue focus:border-transparent dark:bg-gray-700" placeholder="Nama Anda" />
            </div>
            <div>
              <label class="block text-sm font-medium mb-1">Email</label>
              <input id="a_regEmail" type="email" required class="w-full px-4 py-2 rounded-lg border focus:ring-2 focus:ring-brandBlue focus:border-transparent dark:bg-gray-700" placeholder="email@contoh.com" />
            </div>
            <div>
              <label class="block text-sm font-medium mb-1">Kata Sandi</label>
              <div class="relative">
                <input id="a_regPassword" type="password" required class="w-full px-4 py-2 rounded-lg border focus:ring-2 focus:ring-brandBlue focus:border-transparent dark:bg-gray-700" placeholder="Minimal 6 karakter" />
                <button type="button" id="a_regTogglePass" class="absolute right-3 top-2.5 text-sm text-gray-500 hover:text-gray-700">Tampilkan</button>
              </div>
              <div class="mt-1 text-xs text-gray-500">
                <span id="a_pwStrength">Kekuatan: -</span>
              </div>
            </div>
            <div>
              <label class="block text-sm font-medium mb-1">Konfirmasi Kata Sandi</label>
              <input id="a_regPassword2" type="password" required class="w-full px-4 py-2 rounded-lg border focus:ring-2 focus:ring-brandBlue focus:border-transparent dark:bg-gray-700" placeholder="Ketik ulang kata sandi" />
            </div>
            <button id="a_registerBtn" class="w-full bg-green-600 text-white py-3 rounded-lg font-medium hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-green-500 focus:ring-offset-2">
              Buat Akun
            </button>
            <p class="text-sm text-center">
              Sudah punya akun? <button id="a_showLogin" class="text-brandBlue hover:text-blue-700">Masuk</button>
            </p>
          </form>
        </div>
      </div>

      <!-- Features Preview -->
      <div class="mt-8 grid grid-cols-1 md:grid-cols-3 gap-4 text-center">
        <div class="p-4">
          <div class="text-2xl mb-2">📊</div>
          <h3 class="font-medium mb-1">Dashboard Lengkap</h3>
          <p class="text-sm text-gray-600 dark:text-gray-400">Pantau semua aktivitas dalam satu tempat</p>
        </div>
        <div class="p-4">
          <div class="text-2xl mb-2">👥</div>
          <h3 class="font-medium mb-1">Manajemen Klien</h3>
          <p class="text-sm text-gray-600 dark:text-gray-400">Kelola data klien dengan mudah</p>
        </div>
        <div class="p-4">
          <div class="text-2xl mb-2">📱</div>
          <h3 class="font-medium mb-1">Responsif</h3>
          <p class="text-sm text-gray-600 dark:text-gray-400">Akses dari perangkat manapun</p>
        </div>
      </div>
    </div>
  </div>

  <!-- Main App (hidden until login) -->
  <div id="mainApp" class="hidden">
    <!-- Navbar -->
    <nav class="fixed w-full z-40 top-0 bg-white/90 dark:bg-gray-800/90 backdrop-blur-md border-b border-gray-200/50 dark:border-gray-700/50 shadow-sm">
      <div class="max-w-7xl mx-auto px-6 py-3 flex items-center justify-between">
      <div class="flex items-center gap-4">
        <button id="mobileToggle" class="md:hidden p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"/></svg>
        </button>
        <h1 class="text-xl md:text-2xl font-bold text-brandBlue">Client Management</h1>
        <span id="navUser" class="hidden md:inline ml-3 text-sm text-gray-600 dark:text-gray-300"></span>
      </div>

      <div class="hidden md:flex items-center gap-6">
        <a href="#" class="nav-link hover:text-brandBlue" data-target="home">Beranda</a>
        <a href="#" class="nav-link hover:text-brandBlue" data-target="dashboard">Dashboard</a>
        <a href="#" class="nav-link hover:text-brandBlue" data-target="klien">Klien</a>
        <a href="#" class="nav-link hover:text-brandBlue" data-target="proyek">Proyek</a>
        <a href="#" class="nav-link hover:text-brandBlue" data-target="laporan">Laporan</a>
        <a href="#" class="nav-link hover:text-brandBlue" data-target="profile">Profil</a>
        <a href="#" id="logoutBtn" class="nav-link hover:text-brandBlue" data-target="logout">Logout</a>
      </div>

      <div class="flex items-center gap-3">
        <button id="themeToggle" class="p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700" title="Toggle theme">
          <svg id="iconLight" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 hidden" viewBox="0 0 20 20" fill="currentColor"><path d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zM4.22 4.22a1 1 0 011.42 0L6.64 5.22a1 1 0 11-1.42 1.42L4.22 5.64a1 1 0 010-1.42zM2 10a1 1 0 011-1h1a1 1 0 110 2H3a1 1 0 01-1-1zM14.36 5.22a1 1 0 011.42 1.42l-1 1a1 1 0 11-1.42-1.42l1-1zM10 16a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM16.24 14.36a1 1 0 010 1.42l-1 1a1 1 0 11-1.42-1.42l1-1a1 1 0 011.42 0z"/></svg>
          <svg id="iconDark" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor"><path d="M17.293 13.293A8 8 0 116.707 2.707a8.001 8.001 0 0010.586 10.586z"/></svg>
        </button>
        <button id="addMenu" class="bg-brandBlue text-white px-3 py-1 rounded-md hover:bg-blue-700">Tambah</button>
      </div>
    </div>

    <!-- Mobile menu -->
    <div id="mobileMenu" class="md:hidden hidden px-4 pb-4">
      <div class="flex flex-col gap-2">
        <a href="#" class="nav-link px-2 py-2 rounded hover:bg-gray-100" data-target="home">Beranda</a>
        <a href="#" class="nav-link px-2 py-2 rounded hover:bg-gray-100" data-target="dashboard">Dashboard</a>
        <a href="#" class="nav-link px-2 py-2 rounded hover:bg-gray-100" data-target="klien">Klien</a>
        <a href="#" class="nav-link px-2 py-2 rounded hover:bg-gray-100" data-target="proyek">Proyek</a>
        <a href="#" class="nav-link px-2 py-2 rounded hover:bg-gray-100" data-target="laporan">Laporan</a>
        <a href="#" class="nav-link px-2 py-2 rounded hover:bg-gray-100" data-target="logout">Logout</a>
      </div>
    </div>
  </nav>

  <main class="pt-20">
    <!-- Hero -->
    <section id="home" class="pt-12 fade-in">
      <div class="max-w-6xl mx-auto px-6">
        <div class="rounded-2xl overflow-hidden grid grid-cols-1 lg:grid-cols-2 gap-6 items-center bg-gradient-to-r from-purple-500 via-pink-500 to-orange-400 text-white p-10 shadow-lg">
          <div>
            <h2 class="text-4xl font-extrabold mb-4">Selamat Datang di Client Management System</h2>
            <p class="mb-6 opacity-90">Kelola klien, proyek, dan laporan dalam satu tempat dengan antarmuka yang cepat dan responsif.</p>
            <div class="flex gap-3">
              <button onclick="showSection('dashboard')" class="bg-white text-indigo-600 font-semibold px-5 py-2 rounded-lg">Lihat Dashboard</button>
              <button onclick="showSection('klien')" class="bg-white/20 border border-white/30 px-5 py-2 rounded-lg">Lihat Klien</button>
            </div>
          </div>
          <div class="hidden lg:block">
            <img src="https://images.unsplash.com/photo-1554224155-6726b3ff858f?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3" alt="finance calculator and charts" class="rounded-xl shadow-2xl">
          </div>
        </div>
      </div>
    </section>

    <!-- Dashboard -->
    <section id="dashboard" class="hidden-section pt-12 fade-in">
      <div class="max-w-6xl mx-auto px-6">
        <div class="flex flex-col lg:flex-row gap-6">
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-6 flex-1">
            <div class="bg-white dark:bg-gray-800 rounded-xl p-6 shadow-lg hover:shadow-xl transition-shadow">
              <h3 class="text-gray-500 dark:text-gray-300">Total Klien</h3>
              <p id="totalClients" class="text-3xl font-bold text-blue-500 mt-2">128</p>
            </div>
            <div class="bg-white dark:bg-gray-800 rounded-xl p-6 shadow-lg hover:shadow-xl transition-shadow">
              <h3 class="text-gray-500 dark:text-gray-300">Proyek Aktif</h3>
              <p id="activeProjects" class="text-3xl font-bold text-emerald-500 mt-2">56</p>
            </div>
            <div class="bg-white dark:bg-gray-800 rounded-xl p-6 shadow-lg hover:shadow-xl transition-shadow">
              <h3 class="text-gray-500 dark:text-gray-300">Laporan Bulan Ini</h3>
              <p id="monthlyReports" class="text-3xl font-bold text-violet-500 mt-2">23</p>
            </div>
            <div class="bg-white dark:bg-gray-800 rounded-xl p-6 shadow-lg hover:shadow-xl transition-shadow">
              <h3 class="text-gray-500 dark:text-gray-300">User Terdaftar</h3>
              <p id="registeredUsers" class="text-3xl font-bold text-rose-500 mt-2">12</p>
            </div>
          </div>

          <div class="bg-white/95 dark:bg-gray-800/95 rounded-xl p-6 shadow-xl backdrop-blur-sm border border-gray-100 dark:border-gray-700 flex-1">
            <h3 class="text-gray-600 dark:text-gray-300 font-semibold mb-4">Grafik Ringkasan</h3>
            <div class="h-[300px] relative">
              <canvas id="summaryChart"></canvas>
            </div>
          </div>
        </div>
      </div>
    </section>

    <script>
      // Initialize chart as soon as possible
      document.addEventListener('DOMContentLoaded', function() {
        const summaryCtx = document.getElementById('summaryChart').getContext('2d');
        window.summaryChart = new Chart(summaryCtx, {
          type: 'doughnut',
          data: {
            labels: ['Aktif', 'Berjalan', 'Selesai', 'Nonaktif'],
            datasets: [{
              data: [60, 25, 20, 18],
              backgroundColor: [
                '#3b82f6', // blue
                '#10b981', // emerald
                '#8b5cf6', // violet
                '#f43f5e'  // rose
              ],
              borderWidth: 2,
              borderColor: '#ffffff'
            }]
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
              legend: {
                position: 'bottom',
                labels: {
                  padding: 20,
                  usePointStyle: true,
                  font: {
                    size: 12
                  }
                }
              }
            },
            animation: {
              animateScale: true,
              animateRotate: true
            }
          }
        });
      });
    </script>

    <!-- Klien -->
    <section id="klien" class="hidden-section pt-12 px-6 fade-in">
      <div class="max-w-5xl mx-auto">
        <div class="flex items-center justify-between mb-4">
          <h2 class="text-2xl font-bold">Daftar Klien</h2>
          <div class="flex gap-3 items-center">
            <input id="clientSearch" type="text" placeholder="Cari klien..." class="px-3 py-2 rounded-md border focus:ring focus:outline-none" />
            <select id="clientFilter" class="px-3 py-2 rounded-md border">
              <option value="all">Semua</option>
              <option value="Aktif">Aktif</option>
              <option value="Nonaktif">Nonaktif</option>
            </select>
            <button onclick="openModal('clientModal')" class="bg-brandBlue text-white px-3 py-2 rounded-md">+ Klien</button>
          </div>
        </div>

        <div class="bg-white/95 dark:bg-gray-800/95 shadow-xl rounded-xl p-4 backdrop-blur-sm border border-gray-100 dark:border-gray-700">
          <table id="clientsTable" class="w-full text-left border-collapse">
            <thead>
              <tr class="bg-gradient-to-r from-gray-50 to-gray-100 dark:from-gray-700 dark:to-gray-700 text-gray-700 dark:text-gray-200">
                <th class="py-3 px-4">Nama Klien</th>
                <th class="py-3 px-4">Perusahaan</th>
                <th class="py-3 px-4">Status</th>
                <th class="py-3 px-4">Aksi</th>
              </tr>
            </thead>
            <tbody id="clientsBody">
              <tr class="border-b hover:bg-gray-50 dark:hover:bg-gray-700">
                <td class="py-3 px-4">Budi Santoso</td>
                <td class="py-3 px-4">PT Maju Jaya</td>
                <td class="py-3 px-4 text-green-600 font-semibold">Aktif</td>
                <td class="py-3 px-4"><button class="text-sm text-brandBlue hover:underline" onclick="editRow(this)">Edit</button></td>
              </tr>
              <tr class="border-b hover:bg-gray-50 dark:hover:bg-gray-700">
                <td class="py-3 px-4">Citra Lestari</td>
                <td class="py-3 px-4">CV Sinar Abadi</td>
                <td class="py-3 px-4 text-red-500 font-semibold">Nonaktif</td>
                <td class="py-3 px-4"><button class="text-sm text-brandBlue hover:underline" onclick="editRow(this)">Edit</button></td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </section>

    <!-- Proyek -->
    <section id="proyek" class="hidden-section pt-12 px-6 fade-in">
      <div class="max-w-5xl mx-auto">
        <div class="flex items-center justify-between mb-4">
          <h2 class="text-2xl font-bold">Daftar Proyek</h2>
          <div class="flex gap-3 items-center">
            <input id="projectSearch" type="text" placeholder="Cari proyek..." class="px-3 py-2 rounded-md border" />
            <select id="projectFilter" class="px-3 py-2 rounded-md border">
              <option value="all">Semua</option>
              <option value="Selesai">Selesai</option>
              <option value="Berjalan">Berjalan</option>
            </select>
            <button onclick="openModal('projectModal')" class="bg-brandBlue text-white px-3 py-2 rounded-md">+ Proyek</button>
          </div>
        </div>

        <div class="bg-white/95 dark:bg-gray-800/95 shadow-xl rounded-xl p-4 backdrop-blur-sm border border-gray-100 dark:border-gray-700">
          <table id="projectsTable" class="w-full text-left border-collapse">
            <thead>
              <tr class="bg-gradient-to-r from-gray-50 to-gray-100 dark:from-gray-700 dark:to-gray-700 text-gray-700 dark:text-gray-200">
                <th class="py-3 px-4">Nama Proyek</th>
                <th class="py-3 px-4">Klien</th>
                <th class="py-3 px-4">Status</th>
                <th class="py-3 px-4">Aksi</th>
              </tr>
            </thead>
            <tbody id="projectsBody">
              <tr class="border-b hover:bg-gray-50 dark:hover:bg-gray-700">
                <td class="py-3 px-4">Audit Keuangan 2025</td>
                <td class="py-3 px-4">PT Maju Jaya</td>
                <td class="py-3 px-4 text-green-600 font-semibold">Selesai</td>
                <td class="py-3 px-4"><button class="text-sm text-brandBlue hover:underline" onclick="editRow(this)">Edit</button></td>
              </tr>
              <tr class="border-b hover:bg-gray-50 dark:hover:bg-gray-700">
                <td class="py-3 px-4">Laporan Pajak Tahunan</td>
                <td class="py-3 px-4">CV Sinar Abadi</td>
                <td class="py-3 px-4 text-yellow-500 font-semibold">Berjalan</td>
                <td class="py-3 px-4"><button class="text-sm text-brandBlue hover:underline" onclick="editRow(this)">Edit</button></td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </section>

    <!-- Laporan -->
    <section id="laporan" class="hidden-section pt-12 px-6 fade-in">
      <div class="max-w-3xl mx-auto bg-white/95 dark:bg-gray-800/95 shadow-xl rounded-xl p-6 backdrop-blur-sm border border-gray-100 dark:border-gray-700">
        <h2 class="text-2xl font-bold mb-4 bg-gradient-to-r from-purple-600 to-blue-600 inline-block text-transparent bg-clip-text">Daftar Upload</h2>
        <div class="flex justify-between items-center mb-4">
          <p class="text-gray-600 dark:text-gray-300">File yang telah diupload dari Klien dan Proyek</p>
          <button id="clearUploads" class="px-4 py-2 rounded-md border hover:bg-gray-100 dark:hover:bg-gray-700">Hapus Semua</button>
        </div>
        <div id="uploadList" class="space-y-2"></div>
      </div>
    </section>

    <!-- Profile Dashboard -->
    <section id="profile" class="hidden-section pt-12 fade-in">
      <div class="max-w-4xl mx-auto px-6">
        <div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg overflow-hidden">
          <!-- Profile Header -->
          <div class="relative bg-gradient-to-r from-fuchsia-500 via-purple-500 to-indigo-500 p-8 text-white">
            <h2 class="text-2xl font-bold mb-2">Dashboard Pengguna</h2>
            <p id="profileEmail" class="text-blue-100">Loading...</p>
          </div>
          
          <!-- Quick Stats -->
          <div class="grid grid-cols-1 md:grid-cols-3 gap-4 p-6 bg-gradient-to-b from-gray-50 to-white dark:from-gray-700/50 dark:to-gray-800/30">
            <div class="bg-white dark:bg-gray-800 p-4 rounded-lg shadow-lg hover:shadow-xl transition-shadow">
              <h3 class="text-sm text-gray-500 dark:text-gray-400">Total Login</h3>
              <p id="loginCount" class="text-2xl font-semibold text-cyan-600 dark:text-cyan-400">1</p>
            </div>
            <div class="bg-white dark:bg-gray-800 p-4 rounded-lg shadow-lg hover:shadow-xl transition-shadow">
              <h3 class="text-sm text-gray-500 dark:text-gray-400">Klien Ditambahkan</h3>
              <p id="addedClients" class="text-2xl font-semibold text-teal-600 dark:text-teal-400">0</p>
            </div>
            <div class="bg-white dark:bg-gray-800 p-4 rounded-lg shadow-lg hover:shadow-xl transition-shadow">
              <h3 class="text-sm text-gray-500 dark:text-gray-400">Proyek Dikelola</h3>
              <p id="managedProjects" class="text-2xl font-semibold text-fuchsia-600 dark:text-fuchsia-400">0</p>
            </div>
          </div>

          <!-- Account Settings -->
          <div class="p-6">
            <h3 class="font-semibold mb-4">Pengaturan Akun</h3>
            <form id="profileForm" class="space-y-4">
              <div>
                <label class="block text-sm font-medium mb-1">Nama Lengkap</label>
                <input type="text" id="profileName" class="w-full p-2 rounded border focus:ring focus:outline-none dark:bg-gray-700" placeholder="Nama Anda" />
              </div>
              <div>
                <label class="block text-sm font-medium mb-1">Password Baru (opsional)</label>
                <div class="relative">
                  <input type="password" id="profileNewPass" class="w-full p-2 rounded border focus:ring focus:outline-none dark:bg-gray-700" placeholder="Kosongkan jika tidak ingin mengubah" />
                  <div class="text-xs text-gray-500 mt-1"><span id="profilePwStrength">Kekuatan: -</span></div>
                </div>
              </div>
              <div class="flex justify-end gap-3">
                <button type="button" onclick="showSection('home')" class="px-4 py-2 rounded bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600">Kembali</button>
                <button type="submit" class="px-4 py-2 rounded bg-brandBlue text-white hover:bg-blue-700">Simpan Perubahan</button>
              </div>
            </form>

            <!-- Recent Activity -->
            <div class="mt-8">
              <h3 class="font-semibold mb-4">Aktivitas Terakhir</h3>
              <div class="space-y-3">
                <div class="flex items-center gap-3 text-sm">
                  <span class="w-32 text-gray-500">Login Terakhir</span>
                  <span id="lastLogin" class="text-gray-700 dark:text-gray-300">-</span>
                </div>
                <div class="flex items-center gap-3 text-sm">
                  <span class="w-32 text-gray-500">Perubahan Terakhir</span>
                  <span id="lastChange" class="text-gray-700 dark:text-gray-300">-</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Logout -->
    <section id="logout" class="hidden-section pt-20 px-6 fade-in text-center">
      <div class="max-w-2xl mx-auto bg-white/95 dark:bg-gray-800/95 shadow-xl rounded-xl p-8 backdrop-blur-sm border border-gray-100 dark:border-gray-700">
        <h2 class="text-2xl font-semibold mb-2 bg-gradient-to-r from-red-600 to-orange-600 inline-block text-transparent bg-clip-text">Anda telah logout.</h2>
        <p class="text-gray-600 dark:text-gray-300 mb-4">Terima kasih telah menggunakan sistem kami.</p>
        <button class="bg-brandBlue text-white px-4 py-2 rounded-md" onclick="showSection('home')">Kembali ke Beranda</button>
      </div>
    </section>

  </main>

  <!-- Footer -->
  <footer class="mt-12 py-8 text-center text-gray-600 dark:text-gray-300">
    © 2025 Client Management System
  </footer>

  <!-- Modals -->
  <div id="modalWrap"></div>

  <!-- Auth Modal (login/register) -->
  <template id="authModalT">
    <div class="fixed inset-0 bg-black/50 flex items-center justify-center z-50">
      <div class="bg-white dark:bg-gray-800 rounded-xl shadow-xl w-full max-w-md p-6">
        <div class="flex items-center justify-between mb-4">
          <h3 id="authTitle" class="text-lg font-semibold">Masuk</h3>
          <button id="closeAuth" class="text-gray-500">✕</button>
        </div>
        <div id="authForms">
          <form id="authLoginForm" class="space-y-3">
            <div>
              <label class="block text-sm mb-1">Email</label>
              <input id="a_loginEmail" type="email" required class="w-full px-3 py-2 rounded border focus:ring focus:outline-none dark:bg-gray-700" placeholder="email@contoh.com" />
            </div>
            <div>
              <label class="block text-sm mb-1">Kata Sandi</label>
              <div class="relative">
                <input id="a_loginPassword" type="password" required class="w-full px-3 py-2 rounded border pr-10 focus:ring focus:outline-none dark:bg-gray-700" placeholder="••••••••" />
                <button type="button" id="a_loginTogglePass" class="absolute right-2 top-2 text-sm text-gray-500">Tampilkan</button>
              </div>
            </div>
            <div class="pt-2">
              <button id="a_loginBtn" class="w-full bg-indigo-600 text-white py-2 rounded hover:bg-indigo-700">Masuk</button>
            </div>
            <div class="text-sm text-center mt-2">Belum punya akun? <button id="a_showRegister" class="text-indigo-600">Daftar</button></div>
          </form>

          <form id="authRegisterForm" class="space-y-3 hidden">
            <div>
              <label class="block text-sm mb-1">Nama Lengkap</label>
              <input id="a_regName" type="text" class="w-full px-3 py-2 rounded border focus:ring focus:outline-none dark:bg-gray-700" placeholder="Nama Anda" />
            </div>
            <div>
              <label class="block text-sm mb-1">Email</label>
              <input id="a_regEmail" type="email" class="w-full px-3 py-2 rounded border focus:ring focus:outline-none dark:bg-gray-700" placeholder="email@contoh.com" />
            </div>
            <div>
              <label class="block text-sm mb-1">Kata Sandi</label>
              <div class="relative">
                <input id="a_regPassword" type="password" class="w-full px-3 py-2 rounded border pr-10 focus:ring focus:outline-none dark:bg-gray-700" placeholder="Minimal 6 karakter" />
                <button type="button" id="a_regTogglePass" class="absolute right-2 top-2 text-sm text-gray-500">Tampilkan</button>
              </div>
              <div class="mt-2 text-xs text-gray-500"><span id="a_pwStrength">Kekuatan: -</span></div>
            </div>
            <div>
              <label class="block text-sm mb-1">Konfirmasi Kata Sandi</label>
              <input id="a_regPassword2" type="password" class="w-full px-3 py-2 rounded border focus:ring focus:outline-none dark:bg-gray-700" placeholder="Ketik ulang kata sandi" />
            </div>
            <div class="pt-2">
              <button id="a_registerBtn" class="w-full bg-green-600 text-white py-2 rounded hover:bg-green-700">Buat Akun</button>
            </div>
            <div class="text-sm text-center mt-2">Sudah punya akun? <button id="a_showLogin" class="text-indigo-600">Masuk</button></div>
          </form>
        </div>
      </div>
    </div>
  </template>

  <template id="clientModalT">
    <div class="fixed inset-0 bg-black/50 flex items-center justify-center z-50">
      <div class="bg-white dark:bg-gray-800 rounded-xl shadow-xl w-full max-w-md p-6">
        <h3 class="text-lg font-semibold mb-3">Tambah Klien</h3>
        <div class="flex flex-col gap-3">
          <input id="newClientName" placeholder="Nama klien" class="px-3 py-2 rounded border" />
          <input id="newClientCompany" placeholder="Perusahaan" class="px-3 py-2 rounded border" />
          <select id="newClientStatus" class="px-3 py-2 rounded border">
            <option value="Aktif">Aktif</option>
            <option value="Nonaktif">Nonaktif</option>
          </select>
          <!-- File upload in Tambah Klien modal -->
          <div class="border-t pt-3">
            <label class="block text-sm font-medium mb-2">Upload File (Opsional)</label>
            <input id="clientModalFile" type="file" accept=".csv,application/pdf" class="w-full px-2 py-1 rounded border text-sm" />
            <label class="inline-flex items-center gap-2 mt-2"><input id="clientModalAudit" type="checkbox" /> <span class="text-xs">Tandai untuk audit</span></label>
          </div>
          <div class="flex justify-end gap-2">
            <button class="px-3 py-1 rounded" onclick="closeModal()">Batal</button>
            <button class="px-3 py-1 rounded bg-brandBlue text-white" onclick="addClientWithFile()">Simpan</button>
          </div>
        </div>
      </div>
    </div>
  </template>

  <template id="projectModalT">
    <div class="fixed inset-0 bg-black/50 flex items-center justify-center z-50">
      <div class="bg-white dark:bg-gray-800 rounded-xl shadow-xl w-full max-w-md p-6">
        <h3 class="text-lg font-semibold mb-3">Tambah Proyek</h3>
        <div class="flex flex-col gap-3">
          <input id="newProjectName" placeholder="Nama proyek" class="px-3 py-2 rounded border" />
          <input id="newProjectClient" placeholder="Klien" class="px-3 py-2 rounded border" />
          <select id="newProjectStatus" class="px-3 py-2 rounded border">
            <option value="Berjalan">Berjalan</option>
            <option value="Selesai">Selesai</option>
          </select>
          <!-- File upload in Tambah Proyek modal -->
          <div class="border-t pt-3">
            <label class="block text-sm font-medium mb-2">Upload File (Opsional)</label>
            <input id="projectModalFile" type="file" accept=".csv,application/pdf" class="w-full px-2 py-1 rounded border text-sm" />
            <label class="inline-flex items-center gap-2 mt-2"><input id="projectModalAudit" type="checkbox" /> <span class="text-xs">Tandai untuk audit</span></label>
          </div>
          <div class="flex justify-end gap-2">
            <button class="px-3 py-1 rounded" onclick="closeModal()">Batal</button>
            <button class="px-3 py-1 rounded bg-brandBlue text-white" onclick="addProjectWithFile()">Simpan</button>
          </div>
        </div>
      </div>
    </div>
  </template>

  <!-- Audit Upload Modal -->
  <template id="auditUploadT">
    <div class="fixed inset-0 bg-black/50 flex items-center justify-center z-50">
      <div class="bg-white dark:bg-gray-800 rounded-xl shadow-xl w-full max-w-md p-6">
        <h3 id="auditTitle" class="text-lg font-semibold mb-3">Upload untuk Audit</h3>
        <div class="flex flex-col gap-3">
          <div class="text-sm text-gray-600" id="auditTargetInfo">Target: -</div>
          <input id="auditFileInput" type="file" accept=".csv,application/pdf" class="px-3 py-2 rounded border" />
          <label class="inline-flex items-center gap-2"><input id="auditFlag" type="checkbox" checked /> <span class="text-sm">Tandai sebagai untuk audit</span></label>
          <div class="flex justify-end gap-2">
            <button class="px-3 py-1 rounded" onclick="document.getElementById('modalWrap').innerHTML=''">Batal</button>
            <button id="auditUploadBtn" class="px-3 py-1 rounded bg-brandBlue text-white">Upload & Kirim</button>
          </div>
        </div>
      </div>
    </div>
  </template>

  <!-- Scripts -->
  <script>
    // Constants & Basic state
    const KEY_SESSION = 'cms_demo_session_v1';
    const KEY_USERS = 'cms_demo_users_v1';
    const KEY_UPLOADS = 'cms_demo_uploads_v1';
    const navLinks = document.querySelectorAll('.nav-link');
    const sections = document.querySelectorAll('main section');

    function showSection(id) {
      document.querySelectorAll('main section').forEach(sec => sec.classList.add('hidden-section'));
      const el = document.getElementById(id);
      if (el) el.classList.remove('hidden-section');
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    // Hook nav
    navLinks.forEach(link => link.addEventListener('click', e => { e.preventDefault(); showSection(link.dataset.target); if(window.innerWidth<768) toggleMobile(false); }));

    // --- Authentication integration (merge with login.html demo session) ---
    // User management functions
    function loadUsers() {
      try {
        return JSON.parse(localStorage.getItem(KEY_USERS) || '[]');
      } catch(e) {
        return [];
      }
    }

    function saveUsers(users) {
      localStorage.setItem(KEY_USERS, JSON.stringify(users));
    }

    function getSession() { 
      try {
        return JSON.parse(localStorage.getItem(KEY_SESSION) || 'null');
      } catch(e) {
        return null;
      }
    }

    function requireAuth(){ 
      const sess = getSession(); 
      const navUser = document.getElementById('navUser'); 
      const logoutBtnEl = document.getElementById('logoutBtn');
      const authScreen = document.getElementById('authScreen');
      const mainApp = document.getElementById('mainApp');

      if(!sess || !sess.email){ 
        // Not logged in - show auth screen
        if(authScreen) authScreen.classList.remove('hidden');
        if(mainApp) mainApp.classList.add('hidden');
        if(navUser){ navUser.textContent = 'Guest'; navUser.classList.remove('hidden'); }
        if(logoutBtnEl){ logoutBtnEl.textContent = 'Login'; }
        return false;
      }

      // Authenticated - show main app
      if(authScreen) authScreen.classList.add('hidden');
      if(mainApp) mainApp.classList.remove('hidden');
      
      if(navUser){ 
        navUser.textContent = sess.name || sess.email; 
        navUser.classList.remove('hidden');
        // Make the name clickable to go to profile
        navUser.style.cursor = 'pointer';
        navUser.onclick = () => showSection('profile');
      }
      if(logoutBtnEl){ 
        logoutBtnEl.textContent = 'Logout'; 
        logoutBtnEl.onclick = (e)=>{ 
          e.preventDefault(); 
          localStorage.removeItem(KEY_SESSION); 
          toast('Berhasil logout');
          requireAuth(); // refresh auth state
        }; 
      }
      
      // Update profile if that section is visible
      if(document.getElementById('profile') && !document.getElementById('profile').classList.contains('hidden-section')) {
        updateProfile();
      }
      return true;
    }

    // --------- Embedded auth modal logic ---------
    // small toast for feedback
    function toast(msg, type='info', time=2600){ 
      const wrap = document.createElement('div'); 
      wrap.className = 'fixed right-6 bottom-6 z-60 mb-2 p-3 rounded shadow-lg ' + 
        (type==='error'? 'bg-red-500 text-white' : 'bg-white dark:bg-gray-800 text-gray-900 dark:text-gray-100'); 
      wrap.innerText = msg; 
      document.body.appendChild(wrap); 
      setTimeout(()=>{ 
        wrap.style.opacity=0; 
        wrap.style.transition='opacity 260ms'; 
        setTimeout(()=>wrap.remove(),260); 
      }, time); 
    }

    // simple password strength used in auth modal
    function pwStrength(pw){ 
      if(!pw) return '—'; 
      let score=0; 
      if(pw.length>=8) score++; 
      if(/[A-Z]/.test(pw)) score++; 
      if(/[0-9]/.test(pw)) score++; 
      if(/[^A-Za-z0-9]/.test(pw)) score++; 
      return score<=1 ? 'Lemah' : score===2 ? 'Cukup' : score===3 ? 'Kuat' : 'Sangat Kuat';
    }

    function loadUsers(){ try{ return JSON.parse(localStorage.getItem(KEY_USERS)||'[]'); }catch(e){ return []; } }
    function saveUsers(u){ localStorage.setItem(KEY_USERS, JSON.stringify(u)); }

    function openAuthModal(){ 
      const wrap = document.getElementById('modalWrap'); 
      wrap.innerHTML=''; 
      wrap.appendChild(document.getElementById('authModalT').content.cloneNode(true)); 
      setupAuthModal(); 
    }

    function closeAuthModal(){ document.getElementById('modalWrap').innerHTML=''; }

    // Profile management
    function updateProfile() {
      const sess = getSession();
      if(!sess || !sess.email) return;

      const users = loadUsers();
      const user = users.find(u => u.email === sess.email);
      if(!user) return;

      // Update profile header
      const profileEmail = document.getElementById('profileEmail');
      if(profileEmail) profileEmail.textContent = user.email;

      // Update stats
      document.getElementById('loginCount').textContent = user.loginCount || 1;
      document.getElementById('addedClients').textContent = user.addedClients || 0;
      document.getElementById('managedProjects').textContent = user.managedProjects || 0;

      // Fill form
      document.getElementById('profileName').value = user.name || '';

      // Show last activity
      document.getElementById('lastLogin').textContent = new Date(sess.ts).toLocaleString();
      document.getElementById('lastChange').textContent = user.lastChange ? new Date(user.lastChange).toLocaleString() : 'Belum ada perubahan';

      // Setup password strength
      const newPass = document.getElementById('profileNewPass');
      const pwStrength = document.getElementById('profilePwStrength');
      if(newPass && pwStrength) {
        newPass.oninput = () => {
          pwStrength.textContent = 'Kekuatan: ' + (newPass.value ? pwStrength(newPass.value) : '-');
        };
      }

      // Setup form submission
      document.getElementById('profileForm').onsubmit = (e) => {
        e.preventDefault();
        const newName = document.getElementById('profileName').value.trim();
        const newPass = document.getElementById('profileNewPass').value;

        if(!newName) {
          toast('Nama tidak boleh kosong', 'error');
          return;
        }

        user.name = newName;
        if(newPass) {
          if(newPass.length < 6) {
            toast('Password minimal 6 karakter', 'error');
            return;
          }
          user.pass = btoa(newPass);
        }
        
        user.lastChange = Date.now();
        saveUsers(users);
        
        // Update session name
        sess.name = newName;
        localStorage.setItem(KEY_SESSION, JSON.stringify(sess));
        
        requireAuth(); // refresh navbar
        toast('Profil berhasil diperbarui');
      };
    }

    // Handle all authentication setup and events
    function setupInitialAuth() {
      // Get all form elements
      const loginForm = document.getElementById('authLoginForm');
      const registerForm = document.getElementById('authRegisterForm');
      const showRegister = document.getElementById('a_showRegister');
      const showLogin = document.getElementById('a_showLogin');
      const loginToggle = document.getElementById('a_loginTogglePass');
      const loginPass = document.getElementById('a_loginPassword');
      const loginEmail = document.getElementById('a_loginEmail');
      const loginBtn = document.getElementById('a_loginBtn');
      const regToggle = document.getElementById('a_regTogglePass');
      const regPass = document.getElementById('a_regPassword');
      const regPass2 = document.getElementById('a_regPassword2');
      const regName = document.getElementById('a_regName');
      const regEmail = document.getElementById('a_regEmail');
      const regBtn = document.getElementById('a_registerBtn');
      const pwStrengthEl = document.getElementById('a_pwStrength');

      // Toggle between login and register forms
      showRegister.addEventListener('click', (e) => {
        e.preventDefault();
        loginForm.classList.add('hidden');
        registerForm.classList.remove('hidden');
        document.getElementById('authTitle').innerText = 'Daftar';
      });

      showLogin.addEventListener('click', (e) => {
        e.preventDefault();
        registerForm.classList.add('hidden');
        loginForm.classList.remove('hidden');
        document.getElementById('authTitle').innerText = 'Masuk';
      });

      // Password visibility toggles
      loginToggle.addEventListener('click', () => {
        loginPass.type = loginPass.type === 'password' ? 'text' : 'password';
        loginToggle.innerText = loginPass.type === 'password' ? 'Tampilkan' : 'Sembunyikan';
      });

      regToggle.addEventListener('click', () => {
        regPass.type = regPass.type === 'password' ? 'text' : 'password';
        regToggle.innerText = regPass.type === 'password' ? 'Tampilkan' : 'Sembunyikan';
      });

      // Password strength indicator
      regPass.addEventListener('input', () => {
        pwStrengthEl.innerText = 'Kekuatan: ' + pwStrength(regPass.value);
      });

      // Handle login submit
      loginForm.addEventListener('submit', (e) => {
        e.preventDefault();
        const email = loginEmail.value.trim().toLowerCase();
        const pass = loginPass.value;

        if(!email || !pass) {
          toast('Isi email dan kata sandi', 'error');
          return;
        }

        const users = loadUsers();
        const user = users.find(u => u.email === email && u.pass === btoa(pass));

        if(!user) {
          toast('Email atau kata sandi salah', 'error');
          return;
        }

        // Success - update login count and set session
        user.loginCount = (user.loginCount || 0) + 1;
        saveUsers(users);

        localStorage.setItem(KEY_SESSION, JSON.stringify({
          email: user.email,
          name: user.name,
          ts: Date.now()
        }));

        toast('Login berhasil');
        requireAuth();
        showSection('dashboard');
      });

      // Handle registration
      registerForm.addEventListener('submit', (e) => {
        e.preventDefault();
        const name = regName.value.trim();
        const email = regEmail.value.trim().toLowerCase();
        const pass = regPass.value;
        const pass2 = regPass2.value;

        if(!name || !email || !pass || !pass2) {
          toast('Isi semua field yang dibutuhkan', 'error');
          return;
        }

        if(pass.length < 6) {
          toast('Password minimal 6 karakter', 'error');
          return;
        }

        if(pass !== pass2) {
          toast('Konfirmasi password tidak cocok', 'error');
          return;
        }

        const users = loadUsers();
        if(users.find(u => u.email === email)) {
          toast('Email sudah terdaftar', 'error');
          return;
        }

        // Add new user
        users.push({
          name,
          email,
          pass: btoa(pass),
          loginCount: 0,
          created: Date.now()
        });

        saveUsers(users);
        toast('Akun berhasil dibuat, silakan login');
        
        // Reset form and show login
        registerForm.reset();
        showLogin.click();
      });

      // Login handler
      if(loginForm) loginForm.addEventListener('submit', (ev)=>{ 
        ev.preventDefault();
        const email = document.getElementById('a_loginEmail').value.trim().toLowerCase();
        const pw = document.getElementById('a_loginPassword').value;

        if(!email||!pw){ 
          toast('Isi email & kata sandi','error'); 
          return; 
        }

        const users = loadUsers();
        const user = users.find(u=>u.email===email && u.pass===btoa(pw));
        
        if(!user){ 
          toast('Email atau kata sandi salah','error'); 
          return; 
        }

        // Update login count
        user.loginCount = (user.loginCount || 0) + 1;
        saveUsers(users);

        localStorage.setItem(KEY_SESSION, JSON.stringify({ 
          email: user.email, 
          name: user.name, 
          ts: Date.now() 
        }));

        toast('Login berhasil');
        requireAuth(); // This will hide auth screen and show main app
        updateStats(); // refresh dashboard stats
        showSection('dashboard'); // Show dashboard first
      });

      // Register handler
      if(registerBtn) registerBtn.addEventListener('click', (ev)=>{ 
        ev.preventDefault();
        const name = document.getElementById('a_regName').value.trim();
        const email = document.getElementById('a_regEmail').value.trim().toLowerCase();
        const pw = document.getElementById('a_regPassword').value;
        const pw2 = document.getElementById('a_regPassword2').value;

        if(!name||!email||!pw){ 
          toast('Isi semua field yang dibutuhkan','error'); 
          return; 
        } 
        if(pw.length<6){ 
          toast('Kata sandi minimal 6 karakter','error'); 
          return; 
        } 
        if(pw!==pw2){ 
          toast('Konfirmasi kata sandi tidak cocok','error'); 
          return; 
        }

        const users = loadUsers();
        if(users.find(u=>u.email===email)){ 
          toast('Email sudah terdaftar','error'); 
          return; 
        }

        users.push({ name, email, pass: btoa(pw) });
        saveUsers(users);
        toast('Akun dibuat, silakan masuk');
        showLogin.click();
      });
    }

    // Old setup modal function kept for reference
    function setupAuthModal(){
      const closeBtn = document.getElementById('closeAuth'); 
      if(closeBtn) closeBtn.addEventListener('click', closeAuthModal);

      const loginForm = document.getElementById('authLoginForm');
      const registerForm = document.getElementById('authRegisterForm');
      setupInitialAuth(); // reuse auth setup
    }

      // Login/Register handlers moved to setupInitialAuth()
    // Initialize auth forms when page loads
    setupInitialAuth();
    
    // Show home initially (auth optional)
    requireAuth();

    // Ensure data-target attributes work robustly (delegation) so nav and mobile links always respond
    document.querySelectorAll('[data-target]').forEach(el=>{
      el.addEventListener('click', e=>{
        e.preventDefault(); 
        const target = el.dataset.target; 
        if(target === 'profile' && !getSession()) {
          openAuthModal();
          return;
        }
        if(target) {
          showSection(target);
          if(target === 'profile') {
            updateProfile();
          }
        }
        if(window.innerWidth<768) toggleMobile(false);
      });
    });

    // Mobile menu
    const mobileToggle = document.getElementById('mobileToggle');
    const mobileMenu = document.getElementById('mobileMenu');
    mobileToggle.addEventListener('click', () => toggleMobile());
    function toggleMobile(force) { if (force===false) mobileMenu.classList.add('hidden'); else mobileMenu.classList.toggle('hidden'); }

    // Theme toggle (works for both auth screen and main app)
    const themeToggle = document.getElementById('themeToggle');
    const themeToggleAuth = document.getElementById('themeToggleAuth');
    const root = document.documentElement;
    
    function applyTheme(dark){ 
      if(dark) document.documentElement.classList.add('dark'); 
      else document.documentElement.classList.remove('dark'); 
      localStorage.setItem('cms-theme', dark? 'dark':'light'); 
    }
    
    const saved = localStorage.getItem('cms-theme');
    applyTheme(saved==='dark');
    
    if(themeToggle) {
      themeToggle.addEventListener('click', ()=> applyTheme(!document.documentElement.classList.contains('dark')));
    }
    if(themeToggleAuth) {
      themeToggleAuth.addEventListener('click', ()=> applyTheme(!document.documentElement.classList.contains('dark')));
    }

    // Add menu quick actions
    document.getElementById('addMenu').addEventListener('click', ()=> openModal('clientModal'));

    // Modal system
    function openModal(name){ const wrap = document.getElementById('modalWrap'); wrap.innerHTML = ''; if(name==='clientModal'){ wrap.appendChild(document.getElementById('clientModalT').content.cloneNode(true)); } else if(name==='projectModal'){ wrap.appendChild(document.getElementById('projectModalT').content.cloneNode(true)); } }
    function closeModal(){ document.getElementById('modalWrap').innerHTML=''; }

    // Add client/project logic
    function addClient(){ const n = document.getElementById('newClientName').value.trim(); const c = document.getElementById('newClientCompany').value.trim(); const s = document.getElementById('newClientStatus').value; if(!n||!c) return alert('Isi nama dan perusahaan'); const tbody = document.getElementById('clientsBody'); const tr = document.createElement('tr'); tr.className='border-b hover:bg-gray-50 dark:hover:bg-gray-700'; tr.innerHTML = `<td class="py-3 px-4">${escapeHtml(n)}</td><td class="py-3 px-4">${escapeHtml(c)}</td><td class="py-3 px-4 font-semibold ${s==='Aktif'?'text-green-600':'text-red-500'}">${escapeHtml(s)}</td><td class="py-3 px-4"><button class="text-sm text-brandBlue hover:underline" onclick="editRow(this)">Edit</button></td>`; tbody.prepend(tr); closeModal(); updateStats(); incrementUserStat('addedClients', 1); }

    // Add client with optional file upload
    function addClientWithFile(){ const n = document.getElementById('newClientName').value.trim(); const c = document.getElementById('newClientCompany').value.trim(); const s = document.getElementById('newClientStatus').value; if(!n||!c) return alert('Isi nama dan perusahaan'); const tbody = document.getElementById('clientsBody'); const tr = document.createElement('tr'); tr.className='border-b hover:bg-gray-50 dark:hover:bg-gray-700'; tr.innerHTML = `<td class="py-3 px-4">${escapeHtml(n)}</td><td class="py-3 px-4">${escapeHtml(c)}</td><td class="py-3 px-4 font-semibold ${s==='Aktif'?'text-green-600':'text-red-500'}">${escapeHtml(s)}</td><td class="py-3 px-4"><button class="text-sm text-brandBlue hover:underline" onclick="editRow(this)">Edit</button></td>`; tbody.prepend(tr); incrementUserStat('addedClients', 1); updateStats();
      // Handle optional file upload
      const fileInput = document.getElementById('clientModalFile'); const auditFlag = document.getElementById('clientModalAudit').checked;
      if(fileInput && fileInput.files && fileInput.files.length){ const f = fileInput.files[0]; const reader = new FileReader(); const name = f.name; const size = f.size; const isPdf = f.type.includes('pdf') || name.toLowerCase().endsWith('.pdf'); if(isPdf){ reader.onload = (e)=>{ const dataUrl = e.target.result; const arr = loadUploads(); arr.unshift({ name, size, type: 'pdf', ts: Date.now(), dataUrl, owner: { type: 'client', name: n }, audit: !!auditFlag }); saveUploads(arr); renderUploadList(); toast('Klien + PDF dikirim'); }; reader.readAsDataURL(f); } else { reader.onload = (e)=>{ const txt = e.target.result; const arr = loadUploads(); arr.unshift({ name, size, type: 'csv', ts: Date.now(), content: txt, owner: { type: 'client', name: n }, audit: !!auditFlag }); saveUploads(arr); renderUploadList(); toast('Klien + CSV dikirim'); }; reader.readAsText(f,'utf-8'); } } closeModal(); }

    function editRow(btn){ const tr = btn.closest('tr'); alert('Edit fungsionalitas sederhana — Anda bisa implementasikan form edit yang prefills data. Row: ' + tr.querySelector('td').innerText); }

    function escapeHtml(s){ return s.replaceAll('&','&amp;').replaceAll('<','&lt;').replaceAll('>','&gt;'); }

    function incrementUserStat(key, by=1){ const sess = getSession(); if(!sess || !sess.email) return; const users = loadUsers(); const user = users.find(u=>u.email===sess.email); if(!user) return; user[key] = (user[key]||0) + by; saveUsers(users); if(document.getElementById('addedClients') && key==='addedClients') document.getElementById('addedClients').textContent = user[key]; if(document.getElementById('managedProjects') && key==='managedProjects') document.getElementById('managedProjects').textContent = user[key]; }

    // Search & filter
    document.getElementById('clientSearch').addEventListener('input', filterClients);
    document.getElementById('clientFilter').addEventListener('change', filterClients);
    document.getElementById('projectSearch').addEventListener('input', filterProjects);
    document.getElementById('projectFilter').addEventListener('change', filterProjects);

    function filterClients(){ const q = document.getElementById('clientSearch').value.toLowerCase(); const f = document.getElementById('clientFilter').value; document.querySelectorAll('#clientsBody tr').forEach(tr=>{ const text = tr.innerText.toLowerCase(); const status = tr.children[2].innerText.trim(); const show = text.includes(q) && (f==='all' || status===f); tr.style.display = show ? '' : 'none'; }); }

    function filterProjects(){ const q = document.getElementById('projectSearch').value.toLowerCase(); const f = document.getElementById('projectFilter').value; document.querySelectorAll('#projectsBody tr').forEach(tr=>{ const text = tr.innerText.toLowerCase(); const status = tr.children[2].innerText.trim(); const show = text.includes(q) && (f==='all' || status===f); tr.style.display = show ? '' : 'none'; }); }

    // Stats & Chart update function
    function updateChart() {
      if (window.summaryChart) {
        const clients = document.querySelectorAll('#clientsBody tr');
        const projects = document.querySelectorAll('#projectsBody tr');
        
        const activeClients = Array.from(clients).filter(r => r.children[2].innerText.includes('Aktif')).length;
        const nonactiveClients = clients.length - activeClients;
        const runningProjects = Array.from(projects).filter(r => r.children[2].innerText.includes('Berjalan')).length;
        const completedProjects = Array.from(projects).filter(r => r.children[2].innerText.includes('Selesai')).length;
        
        window.summaryChart.data.datasets[0].data = [
          activeClients,
          runningProjects,
          completedProjects,
          nonactiveClients
        ];
        window.summaryChart.update('show');
      }
    }

    function updateStats(){ const clients = document.querySelectorAll('#clientsBody tr'); const total = clients.length; const active = Array.from(clients).filter(r=> r.children[2].innerText.includes('Aktif')).length; const proj = document.querySelectorAll('#projectsBody tr'); const activeProj = Array.from(proj).filter(r=> r.children[2].innerText.includes('Berjalan')).length; document.getElementById('totalClients').innerText = total; document.getElementById('activeProjects').innerText = activeProj; document.getElementById('monthlyReports').innerText = 23; document.getElementById('registeredUsers').innerText = loadUsers().length; // update chart with simple counts
      // Update chart after stats
      updateChart();
    }

    // File upload subsystem: store uploads metadata in localStorage and allow preview/import
    function loadUploads(){ try{ return JSON.parse(localStorage.getItem(KEY_UPLOADS)||'[]'); }catch(e){ return []; } }
    function saveUploads(arr){ localStorage.setItem(KEY_UPLOADS, JSON.stringify(arr)); }

    function renderUploadList(){ const list = loadUploads(); const wrap = document.getElementById('uploadList'); wrap.innerHTML=''; if(!list.length) { wrap.innerHTML = '<div class="text-sm text-gray-500">Belum ada file terupload.</div>'; return; } list.forEach((it, idx)=>{ const row = document.createElement('div'); row.className='p-3 rounded border flex items-center justify-between'; const left = document.createElement('div'); left.innerHTML = `<div class="font-medium">${escapeHtml(it.name)}</div><div class="text-xs text-gray-500">${it.type.toUpperCase()} • ${Math.round(it.size/1024)} KB • ${new Date(it.ts).toLocaleString()}</div>`; const right = document.createElement('div'); right.className='flex gap-2 items-center'; if(it.type==='pdf'){ const view = document.createElement('button'); view.className='px-2 py-1 text-sm rounded border'; view.innerText='Lihat PDF'; view.onclick = ()=>{ const w = window.open(it.dataUrl, '_blank'); if(!w) window.location.href = it.dataUrl; }; right.appendChild(view); }
      if(it.type==='csv'){ const preview = document.createElement('button'); preview.className='px-2 py-1 text-sm rounded border'; preview.innerText='Pratinjau CSV'; preview.onclick = ()=>{ showCsvPreview(it); }; right.appendChild(preview);
        const impC = document.createElement('button'); impC.className='px-2 py-1 text-sm rounded bg-brandBlue text-white'; impC.innerText='Import as Clients'; impC.onclick = ()=>{ importCsvAsClients(it.content); }; right.appendChild(impC);
        const impP = document.createElement('button'); impP.className='px-2 py-1 text-sm rounded bg-green-600 text-white'; impP.innerText='Import as Projects'; impP.onclick = ()=>{ importCsvAsProjects(it.content); }; right.appendChild(impP);
      }
      // show owner info when present
      if(it.owner){ const ownerInfo = document.createElement('div'); ownerInfo.className='text-xs text-gray-500 mr-4'; ownerInfo.innerText = `${it.owner.type.toUpperCase()}: ${it.owner.name}`; row.insertBefore(ownerInfo, row.firstChild); }
      const del = document.createElement('button'); del.className='px-2 py-1 text-sm rounded border text-red-600'; del.innerText='Hapus'; del.onclick = ()=>{ if(!confirm('Hapus file ini?')) return; const arr = loadUploads(); arr.splice(idx,1); saveUploads(arr); renderUploadList(); }; right.appendChild(del);
      row.appendChild(left); row.appendChild(right); wrap.appendChild(row);
    }); }

    // Attach 'Upload for Audit' buttons to client/project rows
    function attachAuditButtons(){ ['clientsBody','projectsBody'].forEach(id=>{
      document.querySelectorAll(`#${id} tr`).forEach(tr=>{
        const cell = tr.querySelector('td:last-child');
        if(!cell) return;
        if(cell.querySelector('.audit-btn')) return; // already attached
        const auditBtn = document.createElement('button');
        auditBtn.className = 'text-sm text-yellow-600 hover:underline audit-btn mr-3';
        auditBtn.innerText = 'Upload Audit';
        auditBtn.onclick = ()=>{
          const name = tr.querySelector('td').innerText.trim();
          const type = id==='clientsBody' ? 'client' : 'project';
          openAuditUpload(type, name);
        };
        // insert before existing edit button
        cell.prepend(auditBtn);
      });
    }); }

    // Open audit upload modal for specific owner
    function openAuditUpload(ownerType, ownerName){ const wrap = document.getElementById('modalWrap'); wrap.innerHTML=''; const tpl = document.getElementById('auditUploadT').content.cloneNode(true); wrap.appendChild(tpl); document.getElementById('auditTargetInfo').innerText = `Target: ${ownerType.toUpperCase()} — ${ownerName}`; const fileInput = document.getElementById('auditFileInput'); const uploadBtn = document.getElementById('auditUploadBtn'); uploadBtn.onclick = ()=>{
      if(!fileInput.files || !fileInput.files.length){ toast('Pilih file terlebih dahulu','error'); return; }
      const f = fileInput.files[0]; const reader = new FileReader(); const name = f.name; const size = f.size; const isPdf = f.type.includes('pdf') || name.toLowerCase().endsWith('.pdf'); const auditFlag = document.getElementById('auditFlag').checked;
      if(isPdf){ reader.onload = (e)=>{ const dataUrl = e.target.result; const arr = loadUploads(); arr.unshift({ name, size, type: 'pdf', ts: Date.now(), dataUrl, owner: { type: ownerType, name: ownerName }, audit: !!auditFlag }); saveUploads(arr); renderUploadList(); wrap.innerHTML=''; toast('PDF dikirim untuk audit'); }; reader.readAsDataURL(f); } else { reader.onload = (e)=>{ const txt = e.target.result; const arr = loadUploads(); arr.unshift({ name, size, type: 'csv', ts: Date.now(), content: txt, owner: { type: ownerType, name: ownerName }, audit: !!auditFlag }); saveUploads(arr); renderUploadList(); wrap.innerHTML=''; toast('CSV dikirim untuk audit'); }; reader.readAsText(f,'utf-8'); }
    }; }

    function showCsvPreview(it){ const rows = parseCsv(it.content); const max = Math.min(rows.length, 6); const previewWin = window.open('','_blank'); let html = `<div style="font-family:system-ui,Segoe UI,Roboto,sans-serif;padding:16px"><h3>${escapeHtml(it.name)} - Preview</h3><table border=1 cellpadding=6 cellspacing=0 style="border-collapse:collapse;margin-top:8px">`; for(let r=0;r<max;r++){ html += '<tr>'; rows[r].forEach(c=> html += `<td>${escapeHtml(c)}</td>`); html += '</tr>'; } html += '</table></div>'; previewWin.document.write(html); previewWin.document.close(); }

    function parseCsv(text){ // very small CSV parser: split by lines, then commas (no advanced quoting support)
      const lines = text.split(/\r?\n/).filter(l=>l.trim().length>0);
      return lines.map(l=> l.split(',').map(c=> c.trim()));
    }

    function importCsvAsClients(text){ const rows = parseCsv(text); if(!rows.length) return toast('CSV kosong','error'); const header = rows[0].map(h=>h.toLowerCase()); const nameIdx = header.findIndex(h=> h.includes('name')||h.includes('nama')||h.includes('client'));
      const compIdx = header.findIndex(h=> h.includes('company')||h.includes('perusahaan')||h.includes('company_name'));
      const statusIdx = header.findIndex(h=> h.includes('status'));
      if(nameIdx===-1 || compIdx===-1) return toast('CSV harus memiliki kolom nama & perusahaan di header', 'error');
      for(let i=1;i<rows.length;i++){ const r = rows[i]; const n = r[nameIdx]||('Klien '+(Date.now()%1000)); const c = r[compIdx]||''; const s = statusIdx>-1 ? (r[statusIdx]||'Aktif') : 'Aktif'; const tbody = document.getElementById('clientsBody'); const tr = document.createElement('tr'); tr.className='border-b hover:bg-gray-50 dark:hover:bg-gray-700'; tr.innerHTML = `<td class="py-3 px-4">${escapeHtml(n)}</td><td class="py-3 px-4">${escapeHtml(c)}</td><td class="py-3 px-4 font-semibold ${s==='Aktif'?'text-green-600':'text-red-500'}">${escapeHtml(s)}</td><td class="py-3 px-4"><button class="text-sm text-brandBlue hover:underline" onclick="editRow(this)">Edit</button></td>`; tbody.prepend(tr); incrementUserStat('addedClients',1); }
      updateStats(); toast('CSV berhasil diimpor sebagai klien'); }

    function importCsvAsProjects(text){ const rows = parseCsv(text); if(!rows.length) return toast('CSV kosong','error'); const header = rows[0].map(h=>h.toLowerCase()); const nameIdx = header.findIndex(h=> h.includes('project')||h.includes('nama')||h.includes('name'));
      const clientIdx = header.findIndex(h=> h.includes('client')||h.includes('klien')||h.includes('company'));
      const statusIdx = header.findIndex(h=> h.includes('status'));
      if(nameIdx===-1 || clientIdx===-1) return toast('CSV harus memiliki kolom nama proyek & klien di header', 'error');
      for(let i=1;i<rows.length;i++){ const r = rows[i]; const n = r[nameIdx]||('Proyek '+(Date.now()%1000)); const cl = r[clientIdx]||''; const s = statusIdx>-1 ? (r[statusIdx]||'Berjalan') : 'Berjalan'; const tbody = document.getElementById('projectsBody'); const tr = document.createElement('tr'); tr.className='border-b hover:bg-gray-50 dark:hover:bg-gray-700'; tr.innerHTML = `<td class="py-3 px-4">${escapeHtml(n)}</td><td class="py-3 px-4">${escapeHtml(cl)}</td><td class="py-3 px-4 font-semibold ${s==='Selesai'?'text-green-600':'text-yellow-500'}">${escapeHtml(s)}</td><td class="py-3 px-4"><button class="text-sm text-brandBlue hover:underline" onclick="editRow(this)">Edit</button></td>`; tbody.prepend(tr); incrementUserStat('managedProjects',1); }
      updateStats(); toast('CSV berhasil diimpor sebagai proyek'); }

    // Upload button handlers
    document.addEventListener('DOMContentLoaded', ()=>{
      const clearBtn = document.getElementById('clearUploads');
      if(clearBtn) clearBtn.addEventListener('click', ()=>{ if(!confirm('Hapus semua file yang tersimpan?')) return; localStorage.removeItem(KEY_UPLOADS); renderUploadList(); toast('Semua upload dihapus'); });
      renderUploadList();
    });

    // Run initial stats and chart
    updateStats();

    // attach audit buttons and render uploads when ready
    document.addEventListener('DOMContentLoaded', ()=>{
      attachAuditButtons();
      renderUploadList();
    });

    // small helper: open project modal via button in projects header
    document.querySelectorAll('[onclick^="openModal"]').forEach(btn=>btn.addEventListener('click', ()=>{}));

    // expose some functions to global for inline onclicks
    window.showSection = showSection; window.openModal = (name)=> openModal(name==='projectModal' ? 'projectModal' : 'clientModal'); window.closeModal = closeModal; window.addClient = addClient; window.addClientWithFile = addClientWithFile; window.addProject = addProject; window.addProjectWithFile = addProjectWithFile; window.editRow = editRow;
  </script>

</body>
</html>
