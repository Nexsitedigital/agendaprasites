<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>NEXSITE - Barbearia & Salão Premium</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <!-- Supabase JS Client -->
  <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap');
    
    body {
      font-family: 'Plus Jakarta Sans', sans-serif;
      background-color: #0d0f12;
      color: #f3f4f6;
    }

    .glass-card {
      background: rgba(22, 27, 34, 0.85);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.08);
    }

    .gold-button {
      background: linear-gradient(135deg, #fbbf24 0%, #d97706 100%);
      color: #000;
      font-weight: 700;
      transition: all 0.3s ease;
    }

    .gold-button:hover {
      box-shadow: 0 0 20px rgba(217, 119, 6, 0.4);
      transform: translateY(-1px);
    }

    .service-card {
      transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
      border: 1px solid rgba(255, 255, 255, 0.08);
    }

    .service-card.selected {
      border-color: #fbbf24;
      background: rgba(251, 191, 36, 0.08);
    }

    /* Cores atualizadas dos slots de horário */
    .slot-btn {
      transition: all 0.2s ease;
    }
    .slot-btn.available {
      background-color: rgba(16, 185, 129, 0.1);
      color: #34d399;
      border: 1px solid rgba(16, 185, 129, 0.3);
    }
    .slot-btn.available:hover {
      background-color: rgba(16, 185, 129, 0.2);
      border-color: #34d399;
      transform: scale(1.03);
    }
    .slot-btn.selected {
      background-color: #fbbf24 !important;
      color: #000 !important;
      font-weight: 700;
      border-color: #fbbf24 !important;
    }
    .slot-btn.occupied, .slot-btn.passed, .slot-btn.lunch {
      background-color: rgba(239, 68, 68, 0.1);
      color: #ef4444;
      border: 1px solid rgba(239, 68, 68, 0.2);
      cursor: not-allowed;
      opacity: 0.7;
    }

    ::-webkit-scrollbar {
      width: 8px;
    }
    ::-webkit-scrollbar-track {
      background: #0d0f12;
    }
    ::-webkit-scrollbar-thumb {
      background: #22272e;
      border-radius: 4px;
    }
  </style>
</head>
<body class="min-h-screen pb-12">

  <!-- TOP HEADER / NAV (FIXA NO TOPO) -->
  <header class="sticky top-0 z-50 glass-card border-b border-gray-800 shadow-xl">
    <div class="max-w-6xl mx-auto px-4 py-4 flex flex-wrap justify-between items-center gap-4">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 rounded-xl bg-amber-500/10 border border-amber-500/30 flex items-center justify-center text-amber-400 text-xl font-bold">
          <i class="fa-solid me-0.5 fa-scissors"></i>
        </div>
        <div>
          <h1 class="text-xl font-extrabold tracking-tight text-white flex items-center gap-2">
            NEXSITE
          </h1>
          <p class="text-xs text-gray-400">Barbearia & Salão Premium</p>
        </div>
      </div>
  
      <!-- BOTÕES NAVEGAÇÃO -->
      <div class="flex items-center gap-2">
        <div class="flex bg-gray-900/90 p-1.5 rounded-xl border border-gray-800">
          <button id="tab-book-btn" onclick="switchTab('book')" class="px-4 py-2 text-xs md:text-sm font-semibold rounded-lg transition-all text-black bg-amber-400 shadow-lg">
            <i class="fa-solid fa-calendar-plus me-1.5"></i> Agendar
          </button>
          <button id="tab-client-btn" onclick="switchTab('client')" class="px-4 py-2 text-xs md:text-sm font-semibold rounded-lg transition-all text-gray-400 hover:text-white">
            <i class="fa-solid fa-user me-1.5"></i> Área do Cliente
          </button>
          <button id="tab-admin-btn" onclick="requestAdminAccess()" class="px-4 py-2 text-xs md:text-sm font-semibold rounded-lg transition-all text-gray-400 hover:text-white">
            <i class="fa-solid fa-lock me-1.5"></i> Painel do Salão
          </button>
        </div>
      </div>
    </div>
  </header>

  <!-- MAIN CONTAINER -->
  <main class="max-w-6xl mx-auto px-4 mt-8">

    <!-- VIEW: FAZER AGENDAMENTO -->
    <div id="view-book" class="space-y-8">
      <div class="glass-card rounded-2xl p-6 md:p-8 relative overflow-hidden border border-amber-500/20">
        <div class="grid grid-cols-1 md:grid-cols-12 gap-6 items-center">
          <div class="md:col-span-7 space-y-3 z-10">
            <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-semibold bg-amber-500/10 text-amber-400 border border-amber-500/20">
              <i class="fa-solid fa-star text-xs"></i> Agendamento Online Rápido
            </span>
            <h2 class="text-2xl md:text-4xl font-extrabold text-white leading-tight">
              Reserve seu horário com os melhores profissionais
            </h2>
            <p class="text-sm text-gray-400">
              Escolha o serviço, selecione quem vai te atender e garanta seu horário em menos de 1 minuto.
            </p>
            <div class="pt-2">
              <a href="#section-location" class="inline-flex items-center gap-2 text-xs font-bold text-amber-400 hover:text-amber-300 transition-colors">
                <i class="fa-solid fa-location-dot"></i> <span id="banner-address-text">Rua Horácio Nóbrega, Centro - Patos / PB</span> (Ver Mapa)
              </a>
            </div>
          </div>
          <div class="md:col-span-5 relative">
            <div class="relative rounded-xl overflow-hidden border border-amber-500/30 shadow-2xl group">
              <img src="https://images.unsplash.com/photo-1560066984-138dadb4c035?auto=format&fit=crop&w=800&q=80" alt="Ambiente do Salão" class="w-full h-48 md:h-56 object-cover transform group-hover:scale-105 transition-transform duration-500">
              <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/20 to-transparent"></div>
              <div class="absolute bottom-3 left-3 right-3 flex items-center justify-between text-xs text-amber-300 font-medium">
                <span><i class="fa-solid fa-location-dot me-1"></i> Ambiente Climatizado</span>
                <span><i class="fa-solid fa-wifi me-1"></i> Wi-Fi Grátis</span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- PASSO 1: SERVIÇOS -->
      <section class="space-y-4">
        <div class="flex items-center justify-between">
          <h3 class="text-lg font-bold text-white flex items-center gap-2">
            <span class="w-7 h-7 rounded-lg bg-amber-500/20 text-amber-400 text-sm flex items-center justify-center font-black">1</span>
            Selecione os Serviços
          </h3>
          <span class="text-xs text-gray-400">Você pode escolher mais de um</span>
        </div>
        <div id="services-container" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4"></div>
      </section>

      <!-- PASSO 2: PROFISSIONAL -->
      <section class="space-y-4">
        <h3 class="text-lg font-bold text-white flex items-center gap-2">
          <span class="w-7 h-7 rounded-lg bg-amber-500/20 text-amber-400 text-sm flex items-center justify-center font-black">2</span>
          Escolha o Profissional
        </h3>
        <div id="staff-container" class="grid grid-cols-2 sm:grid-cols-4 gap-3"></div>
      </section>

      <!-- PASSO 3: DATA E HORA -->
      <section class="space-y-4">
        <h3 class="text-lg font-bold text-white flex items-center gap-2">
          <span class="w-7 h-7 rounded-lg bg-amber-500/20 text-amber-400 text-sm flex items-center justify-center font-black">3</span>
          Selecione Data & Horário
        </h3>
        <div class="glass-card p-5 rounded-xl space-y-5">
          <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4 pb-4 border-b border-gray-800">
            <div>
              <label class="block text-xs font-semibold text-gray-400 mb-1">Data do Atendimento</label>
              <input type="date" id="booking-date" onchange="renderSlots()" class="bg-gray-900 border border-gray-700 text-white text-sm rounded-lg p-2.5 focus:border-amber-500 focus:outline-none">
            </div>
            <div class="flex flex-wrap items-center gap-3 text-xs text-gray-400">
              <span class="flex items-center gap-1.5"><span class="w-3 h-3 rounded-full bg-emerald-500 inline-block"></span> Livre</span>
              <span class="flex items-center gap-1.5"><span class="w-3 h-3 rounded-full bg-amber-500 inline-block"></span> Selecionado</span>
              <span class="flex items-center gap-1.5"><span class="w-3 h-3 rounded-full bg-red-500 inline-block"></span> Indisponível / Almoço</span>
            </div>
          </div>
          <div>
            <label class="block text-xs font-semibold text-gray-400 mb-3">Horários Disponíveis (Expediente: 08:00 às 18:30 | Almoço: 12:00 às 13:30)</label>
            <div id="slots-container" class="grid grid-cols-3 sm:grid-cols-4 md:grid-cols-6 gap-2.5"></div>
          </div>
        </div>
      </section>

      <!-- PASSO 4: DADOS -->
      <section class="space-y-4">
        <h3 class="text-lg font-bold text-white flex items-center gap-2">
          <span class="w-7 h-7 rounded-lg bg-amber-500/20 text-amber-400 text-sm flex items-center justify-center font-black">4</span>
          Seus Dados e Confirmação
        </h3>
        <div class="grid grid-cols-1 md:grid-cols-12 gap-6">
          <div class="md:col-span-7 glass-card p-5 rounded-xl space-y-4">
            <div>
              <label class="block text-xs font-semibold text-gray-300 mb-1">Nome Completo *</label>
              <input type="text" id="client-name" placeholder="Ex: João Silva" class="w-full bg-gray-900 border border-gray-800 rounded-lg p-3 text-sm text-white focus:border-amber-500 focus:outline-none">
            </div>
            <div>
              <label class="block text-xs font-semibold text-gray-300 mb-1">Telefone / WhatsApp *</label>
              <input type="tel" id="client-phone" placeholder="(83) 99999-8888" class="w-full bg-gray-900 border border-gray-800 rounded-lg p-3 text-sm text-white focus:border-amber-500 focus:outline-none">
            </div>
            <div>
              <label class="block text-xs font-semibold text-gray-300 mb-1">Observações (Opcional)</label>
              <textarea id="client-notes" rows="2" placeholder="Ex: Prefiro atendimento silencioso..." class="w-full bg-gray-900 border border-gray-800 rounded-lg p-3 text-sm text-white focus:border-amber-500 focus:outline-none"></textarea>
            </div>
          </div>
          <div class="md:col-span-5 glass-card p-5 rounded-xl border-amber-500/30 flex flex-col justify-between space-y-4">
            <div>
              <h4 class="text-sm font-bold text-amber-400 uppercase tracking-wider mb-3 pb-2 border-b border-gray-800 flex items-center gap-2">
                <i class="fa-solid fa-receipt"></i> Resumo do Agendamento
              </h4>
              <div id="summary-content" class="space-y-2 text-xs text-gray-300">
                <p class="text-gray-500 italic">Nenhum serviço selecionado ainda.</p>
              </div>
            </div>
            <button onclick="confirmBooking()" class="w-full py-3.5 px-4 gold-button rounded-xl text-sm font-extrabold flex items-center justify-center gap-2 shadow-lg">
              <i class="fa-solid fa-check-circle text-base"></i> CONFIRMAR AGENDAMENTO
            </button>
          </div>
        </div>
      </section>

      <!-- LOCALIZAÇÃO -->
      <section id="section-location" class="glass-card rounded-2xl p-6 space-y-4 border-gray-800">
        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
          <div>
            <h3 class="text-lg font-bold text-white flex items-center gap-2">
              <i class="fa-solid fa-map-location-dot text-amber-400"></i> Nossa Localização
            </h3>
            <p class="text-xs text-gray-400" id="location-address-display">Rua Horácio Nóbrega, Centro - Patos / PB</p>
          </div>
          <button onclick="openExternalMaps()" class="gold-button px-4 py-2.5 rounded-xl text-xs font-bold flex items-center justify-center gap-2 whitespace-nowrap shadow-md">
            <i class="fa-solid fa-diamond-turn-right"></i> ABRIR NO GOOGLE MAPS / GPS
          </button>
        </div>
        <div class="w-full h-64 md:h-80 rounded-xl overflow-hidden border border-gray-800 shadow-inner">
          <iframe id="google-maps-iframe" class="w-full h-full border-0" loading="lazy" src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3958.123456789!2d-37.27!3d-7.02!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x0!2zN8KwMDEnMTIuMCJTIDM3wrAxNicxMi4wIlc!5e0!3m2!1spt-BR!2sbr!4v1600000000000"></iframe>
        </div>
      </section>
    </div>

    <!-- VIEW: ÁREA DO CLIENTE -->
    <div id="view-client" class="hidden space-y-6 max-w-xl mx-auto">
      <div class="glass-card rounded-2xl p-6 md:p-8 space-y-6 border-amber-500/30">
        <div class="text-center space-y-2">
          <div class="w-14 h-14 bg-amber-500/20 text-amber-400 rounded-full flex items-center justify-center mx-auto text-2xl">
            <i class="fa-solid fa-phone"></i>
          </div>
          <h2 class="text-xl font-bold text-white" id="client-area-title">Identificação do Cliente</h2>
          <p class="text-xs text-gray-400" id="client-area-desc">Digite seu número de telefone para consultar seus agendamentos</p>
        </div>
        <div id="client-login-panel" class="space-y-4">
          <div>
            <label class="block text-xs font-semibold text-gray-300 mb-1">Seu Telefone / WhatsApp</label>
            <input type="tel" id="auth-phone-input" placeholder="(83) 99999-8888" class="w-full bg-gray-900 border border-gray-800 rounded-xl p-3 text-sm text-white focus:border-amber-500 focus:outline-none text-center tracking-wide">
          </div>
          <button onclick="loginClientByPhone()" class="w-full py-3 gold-button rounded-xl text-sm font-bold shadow-lg">
            ACESSAR MEUS AGENDAMENTOS
          </button>
        </div>
        <div id="client-dashboard-panel" class="hidden space-y-4">
          <div class="flex items-center justify-between p-3 bg-gray-900/90 rounded-xl border border-gray-800">
            <div>
              <p class="text-[10px] text-gray-400 uppercase font-semibold">Cliente Conectado</p>
              <p class="text-xs font-bold text-amber-400" id="logged-phone-display"></p>
            </div>
            <button onclick="logoutClient()" class="text-xs text-red-400 hover:text-red-300 underline font-semibold">Sair</button>
          </div>
          <h3 class="text-sm font-bold text-white pt-2">Seus Agendamentos Realizados:</h3>
          <div id="client-appointments-list" class="space-y-3"></div>
        </div>
      </div>
    </div>

    <!-- VIEW: ADMIN / SALÃO -->
    <div id="view-admin" class="hidden space-y-8">
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
        <div class="glass-card p-5 rounded-xl border-l-4 border-l-amber-500">
          <p class="text-xs font-semibold text-gray-400">Total Agendamentos</p>
          <h3 id="stat-total" class="text-2xl font-black text-white mt-1">0</h3>
        </div>
        <div class="glass-card p-5 rounded-xl border-l-4 border-l-emerald-500">
          <p class="text-xs font-semibold text-gray-400">Confirmados</p>
          <h3 id="stat-confirmed" class="text-2xl font-black text-emerald-400 mt-1">0</h3>
        </div>
        <div class="glass-card p-5 rounded-xl border-l-4 border-l-blue-500">
          <p class="text-xs font-semibold text-gray-400">Receita Estimada</p>
          <h3 id="stat-revenue" class="text-2xl font-black text-blue-400 mt-1">R$ 0,00</h3>
        </div>
        <div class="glass-card p-5 rounded-xl border-l-4 border-l-purple-500">
          <p class="text-xs font-semibold text-gray-400">Profissional Mais Procurado</p>
          <h3 id="stat-top-staff" class="text-lg font-bold text-purple-300 mt-1 truncate">-</h3>
        </div>
      </div>

      <div class="glass-card rounded-2xl p-6 space-y-6">
        <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 pb-4 border-b border-gray-800">
          <div>
            <h2 class="text-xl font-bold text-white flex items-center gap-2">
              <i class="fa-solid fa-calendar-days text-amber-400"></i> Agendamentos do Salão
            </h2>
            <p class="text-xs text-gray-400">Gerencie todos os horários marcados em tempo real</p>
          </div>
          <div class="flex flex-wrap items-center gap-3">
            <input type="date" id="admin-filter-date" onchange="renderAdminTable()" class="bg-gray-900 border border-gray-800 text-xs text-white rounded-lg p-2.5 focus:border-amber-500 focus:outline-none">
            <select id="admin-filter-staff" onchange="renderAdminTable()" class="bg-gray-900 border border-gray-800 text-xs text-white rounded-lg p-2.5 focus:border-amber-500 focus:outline-none">
              <option value="all">Todos Profissionais</option>
            </select>
          </div>
        </div>

        <div class="bg-gray-900/90 p-4 rounded-xl border border-gray-800 space-y-3">
          <h3 class="text-xs font-bold text-amber-400 uppercase tracking-wider flex items-center gap-2">
            <i class="fa-solid fa-gear"></i> Configurações de Endereço do Salão
          </h3>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
            <div>
              <label class="block text-[11px] font-semibold text-gray-400 mb-1">Endereço Exibido</label>
              <input type="text" id="admin-address-input" class="w-full bg-gray-950 border border-gray-800 rounded-lg p-2 text-xs text-white focus:border-amber-500 focus:outline-none">
            </div>
            <div>
              <label class="block text-[11px] font-semibold text-gray-400 mb-1">Link do Google Maps</label>
              <input type="text" id="admin-map-link-input" class="w-full bg-gray-950 border border-gray-800 rounded-lg p-2 text-xs text-white focus:border-amber-500 focus:outline-none">
            </div>
          </div>
          <button onclick="saveSalonSettings()" class="gold-button px-4 py-2 rounded-lg text-xs font-bold">
            Salvar Endereço
          </button>
        </div>

        <div class="overflow-x-auto">
          <table class="w-full text-left text-xs text-gray-300">
            <thead class="bg-gray-900/80 text-gray-400 uppercase font-bold border-b border-gray-800">
              <tr>
                <th class="p-3">Horário / Data</th>
                <th class="p-3">Cliente</th>
                <th class="p-3">Serviços</th>
                <th class="p-3">Profissional</th>
                <th class="p-3">Valor</th>
                <th class="p-3">Status</th>
                <th class="p-3 text-right">Ações</th>
              </tr>
            </thead>
            <tbody id="admin-table-body" class="divide-y divide-gray-800/60"></tbody>
          </table>
        </div>
      </div>
    </div>
  </main>

  <!-- MODAL SENHA ADMIN -->
  <div id="modal-admin-pass" class="fixed inset-0 z-50 bg-black/85 backdrop-blur-md hidden flex items-center justify-center p-4">
    <div class="glass-card max-w-sm w-full rounded-2xl p-6 space-y-4 border-amber-500/40 relative text-center">
      <div class="w-12 h-12 bg-amber-500/20 text-amber-400 rounded-full flex items-center justify-center mx-auto text-xl">
        <i class="fa-solid fa-shield-halved"></i>
      </div>
      <div>
        <h3 class="text-lg font-extrabold text-white">Acesso do Salão</h3>
        <p class="text-xs text-gray-400 mt-1">Digite a senha administrativa para acessar</p>
      </div>
      <div>
        <input type="password" id="admin-password-input" placeholder="Senha (padrão:2026)" class="w-full text-center bg-gray-900 border border-gray-800 rounded-xl p-3 text-sm text-white focus:border-amber-500 focus:outline-none tracking-widest">
      </div>
      <div class="flex gap-2">
        <button onclick="closeAdminModal()" class="w-1/2 py-2.5 bg-gray-800 hover:bg-gray-700 text-gray-300 font-semibold rounded-xl text-xs">Cancelar</button>
        <button onclick="verifyAdminPassword()" class="w-1/2 py-2.5 gold-button rounded-xl text-xs font-bold">Entrar</button>
      </div>
    </div>
  </div>

  <!-- MODAL SUCESSO -->
  <div id="modal-success" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-sm hidden flex items-center justify-center p-4">
    <div class="glass-card max-w-md w-full rounded-2xl p-6 text-center space-y-5 border-amber-500/40 relative">
      <div class="w-16 h-16 bg-emerald-500/20 text-emerald-400 rounded-full flex items-center justify-center mx-auto text-3xl">
        <i class="fa-solid fa-circle-check"></i>
      </div>
      <div>
        <h3 class="text-xl font-extrabold text-white">Agendamento Realizado!</h3>
        <p class="text-xs text-gray-400 mt-1">Seu horário foi reservado no sistema.</p>
      </div>
      <div id="modal-details" class="bg-gray-900/90 p-4 rounded-xl text-left text-xs space-y-2 border border-gray-800"></div>
      <div class="space-y-2">
        <button id="btn-whatsapp-send" onclick="sendWhatsAppNotify()" class="w-full py-3 px-4 bg-emerald-600 hover:bg-emerald-500 text-white font-bold rounded-xl text-xs flex items-center justify-center gap-2 transition-all shadow-lg">
          <i class="fa-brands fa-whatsapp text-lg"></i> NOTIFICAR SALÃO VIA WHATSAPP
        </button>
        <button onclick="closeModal()" class="w-full py-2.5 px-4 bg-gray-800 hover:bg-gray-700 text-gray-300 font-semibold rounded-xl text-xs">Fechar</button>
      </div>
    </div>
  </div>

  <!-- JAVASCRIPT COM SUPABASE INTEGRADO -->
  <script>
    // ==========================================
    // COLE SUAS CREDENCIAIS DO SUPABASE ABAIXO:
    // ==========================================
    const SUPABASE_URL = 'https://qbascskxakxqjplzsbxp.supabase.co';
    const SUPABASE_ANON_KEY = 'sb_publishable_R8DQVz6NUKVBqsJ4AcxYIw_FHui7d_p';

    const _supabase = supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY);

    const DB = {
      adminPassword: '1234',
      salonAddress: 'Rua Horácio Nóbrega, Centro - Patos / PB',
      googleMapsUrl: 'https://maps.google.com/?q=Patos+PB',
      services: [
        { id: 's1', name: 'Corte de Cabelo', duration: 45, price: 25.00, icon: 'fa-scissors' },
        { id: 's2', name: 'Barba Terapia', duration: 30, price: 20.00, icon: 'fa-user' },
        { id: 's3', name: 'Combo (Corte + Barba)', duration: 60, price: 50.00, icon: 'fa-crown' },
        { id: 's4', name: 'Escova & Penteado', duration: 45, price: 60.00, icon: 'fa-wand-magic-sparkles' },
        { id: 's5', name: 'Coloração / Luzes', duration: 90, price: 120.00, icon: 'fa-paint-brush' }
      ],
      staff: [
        { id: 'st1', name: 'Qualquer Um', role: 'Atendimento Rápido', avatar: 'https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?auto=format&fit=crop&w=120&q=80' },
        { id: 'st2', name: 'Lucas Ferreira', role: 'Barbeiro Master', avatar: 'https://images.unsplash.com/photo-1570295999919-56ceb5ecca61?auto=format&fit=crop&w=120&q=80' },
        { id: 'st3', name: 'Amanda Rocha', role: 'Especialista em Cor', avatar: 'https://images.unsplash.com/photo-1580489944761-15a19d654956?auto=format&fit=crop&w=120&q=80' },
        { id: 'st4', name: 'Rodrigo Lima', role: 'Estilista', avatar: 'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?auto=format&fit=crop&w=120&q=80' }
      ],
      salonPhone: '5583999999999',
      openingHour: 8,
      closingHour: 18.5 // 18:30 encerramento
    };

    let selectedServices = [];
    let selectedStaffId = 'st1';
    let selectedTime = null;
    let bookings = [];
    let currentCreatedBooking = null;
    let loggedClientPhone = null;

    window.addEventListener('DOMContentLoaded', () => {
      const today = new Date().toISOString().split('T')[0];
      document.getElementById('booking-date').value = today;
      document.getElementById('booking-date').min = today;
      document.getElementById('admin-filter-date').value = today;

      loadSettings();
      loadBookings();
      renderServices();
      renderStaff();
      populateAdminFilters();
      updateLocationDisplay();

      // TEMPO REAL DO SUPABASE
      _supabase
        .channel('public:bookings')
        .on('postgres_changes', { event: '*', schema: 'public', table: 'bookings' }, payload => {
          loadBookings();
        })
        .subscribe();
    });

    async function loadBookings() {
      try {
        const { data, error } = await _supabase.from('bookings').select('*');
        if (error) throw error;
        
        if (data) {
          bookings = data.map(b => ({
            id: b.id,
            clientName: b.client_name,
            clientPhone: b.client_phone,
            notes: b.notes,
            services: typeof b.services === 'string' ? JSON.parse(b.services) : b.services,
            staffId: b.staff_id,
            staffName: b.staff_name,
            date: b.date,
            time: b.time,
            totalPrice: b.total_price,
            status: b.status
          }));
        } else {
          bookings = [];
        }
        renderSlots();
        renderAdminTable();
      } catch (err) {
        console.error('Erro ao carregar do Supabase:', err);
      }
    }

    async function saveBookingToCloud(newBooking) {
      try {
        const { error } = await _supabase.from('bookings').insert([{
          id: newBooking.id,
          client_name: newBooking.clientName,
          client_phone: newBooking.clientPhone,
          notes: newBooking.notes,
          services: newBooking.services,
          staff_id: newBooking.staffId,
          staff_name: newBooking.staffName,
          date: newBooking.date,
          time: newBooking.time,
          total_price: newBooking.totalPrice,
          status: newBooking.status
        }]);
        if (error) throw error;
        loadBookings();
      } catch (err) {
        console.error('Erro ao salvar:', err);
        alert('Erro ao conectar com o banco de dados na nuvem.');
      }
    }

    async function updateBookingStatusInCloud(id, newStatus) {
      try {
        const { error } = await _supabase.from('bookings').update({ status: newStatus }).eq('id', id);
        if (error) throw error;
        loadBookings();
      } catch (err) {
        console.error('Erro ao atualizar status:', err);
      }
    }

    async function deleteBookingFromCloud(id) {
      try {
        const { error } = await _supabase.from('bookings').delete().eq('id', id);
        if (error) throw error;
        loadBookings();
      } catch (err) {
        console.error('Erro ao excluir:', err);
      }
    }

    function loadSettings() {
      const savedAddress = localStorage.getItem('golden_salon_address');
      const savedMapUrl = localStorage.getItem('golden_salon_map_url');
      if (savedAddress) DB.salonAddress = savedAddress;
      if (savedMapUrl) DB.googleMapsUrl = savedMapUrl;
    }

    function saveSalonSettings() {
      const newAddress = document.getElementById('admin-address-input').value.trim();
      const newMapUrl = document.getElementById('admin-map-link-input').value.trim();
      if (newAddress) DB.salonAddress = newAddress;
      if (newMapUrl) DB.googleMapsUrl = newMapUrl;
      localStorage.setItem('golden_salon_address', DB.salonAddress);
      localStorage.setItem('golden_salon_map_url', DB.googleMapsUrl);
      updateLocationDisplay();
      alert('Configurações salvas com sucesso!');
    }

    function updateLocationDisplay() {
      document.getElementById('banner-address-text').innerText = DB.salonAddress;
      document.getElementById('location-address-display').innerText = DB.salonAddress;
      document.getElementById('admin-address-input').value = DB.salonAddress;
      document.getElementById('admin-map-link-input').value = DB.googleMapsUrl;
    }

    function openExternalMaps() {
      window.open(DB.googleMapsUrl, '_blank');
    }

    function switchTab(viewName) {
      const bookView = document.getElementById('view-book');
      const clientView = document.getElementById('view-client');
      const adminView = document.getElementById('view-admin');
      const bookBtn = document.getElementById('tab-book-btn');
      const clientBtn = document.getElementById('tab-client-btn');
      const adminBtn = document.getElementById('tab-admin-btn');

      bookView.classList.add('hidden');
      clientView.classList.add('hidden');
      adminView.classList.add('hidden');

      bookBtn.className = "px-4 py-2 text-xs md:text-sm font-semibold rounded-lg transition-all text-gray-400 hover:text-white";
      clientBtn.className = "px-4 py-2 text-xs md:text-sm font-semibold rounded-lg transition-all text-gray-400 hover:text-white";
      adminBtn.className = "px-4 py-2 text-xs md:text-sm font-semibold rounded-lg transition-all text-gray-400 hover:text-white";

      if (viewName === 'book') {
        bookView.classList.remove('hidden');
        bookBtn.className = "px-4 py-2 text-xs md:text-sm font-semibold rounded-lg transition-all text-black bg-amber-400 shadow-lg";
      } else if (viewName === 'client') {
        clientView.classList.remove('hidden');
        clientBtn.className = "px-4 py-2 text-xs md:text-sm font-semibold rounded-lg transition-all text-black bg-amber-400 shadow-lg";
      } else if (viewName === 'admin') {
        adminView.classList.remove('hidden');
        adminBtn.className = "px-4 py-2 text-xs md:text-sm font-semibold rounded-lg transition-all text-black bg-amber-400 shadow-lg";
        renderAdminTable();
      }
    }

    function loginClientByPhone() {
      const phoneInput = document.getElementById('auth-phone-input').value.trim();
      if (!phoneInput || phoneInput.length < 8) {
        alert('Por favor, informe um número de telefone válido.');
        return;
      }
      loggedClientPhone = phoneInput;
      document.getElementById('logged-phone-display').innerText = phoneInput;
      document.getElementById('client-login-panel').classList.add('hidden');
      document.getElementById('client-dashboard-panel').classList.remove('hidden');
      document.getElementById('client-area-title').innerText = 'Seus Agendamentos';
      document.getElementById('client-area-desc').innerText = 'Histórico de horários vinculados ao seu número';
      renderClientAppointments();
    }

    function logoutClient() {
      loggedClientPhone = null;
      document.getElementById('auth-phone-input').value = '';
      document.getElementById('client-login-panel').classList.remove('hidden');
      document.getElementById('client-dashboard-panel').classList.add('hidden');
      document.getElementById('client-area-title').innerText = 'Identificação do Cliente';
      document.getElementById('client-area-desc').innerText = 'Digite seu número de telefone para consultar seus agendamentos';
    }

    function renderClientAppointments() {
      const container = document.getElementById('client-appointments-list');
      const userBookings = bookings.filter(b => b.clientPhone.includes(loggedClientPhone) || loggedClientPhone.includes(b.clientPhone));

      if (userBookings.length === 0) {
        container.innerHTML = `<div class="p-6 text-center text-gray-500 text-xs italic glass-card rounded-xl">Nenhum agendamento encontrado para este número.</div>`;
        return;
      }

      container.innerHTML = userBookings.map(b => {
        const formattedDate = new Date(b.date + 'T00:00:00').toLocaleDateString('pt-BR');
        return `
          <div class="glass-card p-4 rounded-xl space-y-2 border border-gray-800">
            <div class="flex justify-between items-center">
              <span class="text-xs font-bold text-amber-400">${b.id}</span>
              <span class="px-2 py-0.5 rounded text-[10px] font-bold bg-emerald-500/10 text-emerald-400 border border-emerald-500/20">${b.status}</span>
            </div>
            <div class="text-xs text-gray-300 space-y-1">
              <p><strong>Serviço(s):</strong> ${b.services.map(s => s.name).join(', ')}</p>
              <p><strong>Profissional:</strong> ${b.staffName}</p>
              <p><strong>Data/Hora:</strong> ${formattedDate} às ${b.time}</p>
              <p><strong>Total:</strong> R$ ${b.totalPrice.toFixed(2)}</p>
            </div>
          </div>
        `;
      }).join('');
    }

    function requestAdminAccess() {
      document.getElementById('modal-admin-pass').classList.remove('hidden');
      document.getElementById('admin-password-input').focus();
    }

    function closeAdminModal() {
      document.getElementById('modal-admin-pass').classList.add('hidden');
      document.getElementById('admin-password-input').value = '';
    }

    function verifyAdminPassword() {
      const inputPass = document.getElementById('admin-password-input').value;
      if (inputPass === DB.adminPassword) {
        closeAdminModal();
        switchTab('admin');
      } else {
        alert('Senha incorreta!');
        document.getElementById('admin-password-input').value = '';
      }
    }

    function renderServices() {
      const container = document.getElementById('services-container');
      container.innerHTML = DB.services.map(s => {
        const isSelected = selectedServices.some(item => item.id === s.id);
        return `
          <div onclick="toggleService('${s.id}')" class="service-card p-4 rounded-xl glass-card cursor-pointer flex items-center justify-between ${isSelected ? 'selected' : ''}">
            <div class="flex items-center gap-3">
              <div class="w-10 h-10 rounded-lg ${isSelected ? 'bg-amber-400 text-black' : 'bg-gray-800 text-amber-400'} flex items-center justify-center text-lg">
                <i class="fa-solid ${s.icon}"></i>
              </div>
              <div>
                <h4 class="text-sm font-bold text-white">${s.name}</h4>
                <p class="text-xs text-gray-400"><i class="fa-regular fa-clock me-1"></i>${s.duration} min</p>
              </div>
            </div>
            <div class="text-right">
              <span class="text-sm font-extrabold text-amber-400">R$ ${s.price.toFixed(2)}</span>
              <div class="mt-1"><input type="checkbox" ${isSelected ? 'checked' : ''} class="accent-amber-400 rounded"></div>
            </div>
          </div>
        `;
      }).join('');
      updateSummary();
    }

    function toggleService(id) {
      const service = DB.services.find(s => s.id === id);
      const index = selectedServices.findIndex(s => s.id === id);
      if (index > -1) selectedServices.splice(index, 1);
      else selectedServices.push(service);
      renderServices();
      renderSlots();
    }

    function renderStaff() {
      const container = document.getElementById('staff-container');
      container.innerHTML = DB.staff.map(st => {
        const isSelected = selectedStaffId === st.id;
        return `
          <div onclick="selectStaff('${st.id}')" id="staff-card-${st.id}" class="p-3 rounded-xl glass-card border cursor-pointer text-center transition-all ${isSelected ? 'border-emerald-500 bg-emerald-500/10' : 'border-gray-800 hover:border-gray-700'}">
            <img src="${st.avatar}" alt="${st.name}" class="w-12 h-12 rounded-full mx-auto object-cover mb-2 border-2 ${isSelected ? 'border-emerald-500' : 'border-gray-700'}">
            <h4 class="text-xs font-bold text-white truncate">${st.name}</h4>
            <p class="text-[10px] text-gray-400 truncate">${st.role}</p>
          </div>
        `;
      }).join('');
    }

    function selectStaff(id) {
      selectedStaffId = id;
      renderStaff();
      renderSlots();
      updateSummary();
    }

    // RENDER SLOTS COM BLOQUEIO DE PASSADOS, ALMOÇO E FIM (18:30)
    function renderSlots() {
      const container = document.getElementById('slots-container');
      const dateInput = document.getElementById('booking-date').value;
      selectedTime = null;

      if (!dateInput) {
        container.innerHTML = '<p class="col-span-full text-xs text-gray-500">Selecione uma data primeiro.</p>';
        return;
      }

      const slots = [];
      for (let hour = 8; hour < 18.5; hour += 0.5) {
        const h = Math.floor(hour);
        const m = (hour % 1 === 0) ? '00' : '30';
        slots.push(`${String(h).padStart(2, '0')}:${m}`);
      }

      const dayBookings = bookings.filter(b => b.date === dateInput && b.status !== 'Cancelado');
      const now = new Date();
      const isToday = dateInput === now.toISOString().split('T')[0];
      const currentHourMinutes = now.getHours() * 60 + now.getMinutes();

      container.innerHTML = slots.map(time => {
        const [hStr, mStr] = time.split(':');
        const slotMinutes = parseInt(hStr) * 60 + parseInt(mStr);

        // Verificação de Horário de Almoço (12:00 até 13:30)
        const isLunchTime = slotMinutes >= 720 && slotMinutes < 810; // 12:00 a 13:30

        // Verificação se o horário já passou (caso seja hoje)
        const isPassed = isToday && slotMinutes <= currentHourMinutes;

        // Verificação se já está ocupado por outro agendamento
        const isOccupied = dayBookings.some(b => {
          if (selectedStaffId !== 'st1' && b.staffId !== 'st1' && b.staffId !== selectedStaffId) return false;
          return b.time === time;
        });

        if (isLunchTime) {
          return `<button disabled class="slot-btn lunch py-2 px-3 rounded-lg text-xs font-medium text-center" title="Horário de Almoço">${time} (Almoço)</button>`;
        }
        if (isPassed) {
          return `<button disabled class="slot-btn passed py-2 px-3 rounded-lg text-xs font-medium text-center" title="Horário passado">${time} (Passado)</button>`;
        }
        if (isOccupied) {
          return `<button disabled class="slot-btn occupied py-2 px-3 rounded-lg text-xs font-medium text-center" title="Ocupado">${time} (Ocupado)</button>`;
        }

        return `<button onclick="selectTime('${time}')" class="slot-btn available py-2 px-3 rounded-lg text-xs font-semibold text-center" id="slot-${time.replace(':', '')}">${time}</button>`;
      }).join('');

      updateSummary();
    }

    function selectTime(time) {
      selectedTime = time;
      document.querySelectorAll('.slot-btn.available').forEach(btn => btn.classList.remove('selected'));
      const activeBtn = document.getElementById(`slot-${time.replace(':', '')}`);
      if (activeBtn) activeBtn.classList.add('selected');
      updateSummary();
    }

    function updateSummary() {
      const container = document.getElementById('summary-content');
      const totalDuration = selectedServices.reduce((acc, s) => acc + s.duration, 0);
      const totalPrice = selectedServices.reduce((acc, s) => acc + s.price, 0);
      const date = document.getElementById('booking-date').value;
      const staff = DB.staff.find(s => s.id === selectedStaffId);

      if (selectedServices.length === 0) {
        container.innerHTML = '<p class="text-gray-500 italic">Nenhum serviço selecionado ainda.</p>';
        return;
      }

      const formattedDate = date ? new Date(date + 'T00:00:00').toLocaleDateString('pt-BR') : 'Não selecionada';

      container.innerHTML = `
        <div class="space-y-1.5">
          <p><strong class="text-gray-400">Serviços:</strong> <span class="text-white">${selectedServices.map(s => s.name).join(', ')}</span></p>
          <p><strong class="text-gray-400">Profissional:</strong> <span class="text-emerald-400 font-semibold">${staff ? staff.name : '-'}</span></p>
          <p><strong class="text-gray-400">Data:</strong> <span class="text-white">${formattedDate}</span></p>
          <p><strong class="text-gray-400">Horário:</strong> <span class="text-amber-400 font-bold">${selectedTime || 'Selecione abaixo'}</span></p>
          <p><strong class="text-gray-400">Duração:</strong> <span class="text-white">${totalDuration} minutos</span></p>
          <div class="pt-2 border-t border-gray-800 flex justify-between items-center text-sm">
            <span class="font-bold text-gray-300">Total:</span>
            <span class="text-lg font-black text-amber-400">R$ ${totalPrice.toFixed(2)}</span>
          </div>
        </div>
      `;
    }

    function confirmBooking() {
      const name = document.getElementById('client-name').value.trim();
      const phone = document.getElementById('client-phone').value.trim();
      const notes = document.getElementById('client-notes').value.trim();
      const date = document.getElementById('booking-date').value;

      if (selectedServices.length === 0) {
        alert('Selecione pelo menos um serviço.');
        return;
      }
      if (!selectedTime) {
        alert('Escolha um horário.');
        return;
      }
      if (!name || !phone) {
        alert('Preencha seu Nome e Telefone/WhatsApp.');
        return;
      }

      const staff = DB.staff.find(s => s.id === selectedStaffId);
      const totalDuration = selectedServices.reduce((acc, s) => acc + s.duration, 0);
      const totalPrice = selectedServices.reduce((acc, s) => acc + s.price, 0);

      const newBooking = {
        id: 'BK-' + Math.floor(1000 + Math.random() * 9000),
        clientName: name,
        clientPhone: phone,
        notes: notes,
        services: selectedServices,
        staffId: selectedStaffId,
        staffName: staff ? staff.name : 'Qualquer Um',
        date: date,
        time: selectedTime,
        duration: totalDuration,
        totalPrice: totalPrice,
        status: 'Confirmado'
      };

      saveBookingToCloud(newBooking);
      currentCreatedBooking = newBooking;

      selectedServices = [];
      selectedTime = null;
      document.getElementById('client-name').value = '';
      document.getElementById('client-phone').value = '';
      document.getElementById('client-notes').value = '';
      renderServices();
      renderSlots();

      showSuccessModal(newBooking);
    }

    function showSuccessModal(booking) {
      const modal = document.getElementById('modal-success');
      const details = document.getElementById('modal-details');
      const formattedDate = new Date(booking.date + 'T00:00:00').toLocaleDateString('pt-BR');

      details.innerHTML = `
        <p><strong class="text-gray-400">Código:</strong> <span class="text-amber-400 font-mono">${booking.id}</span></p>
        <p><strong class="text-gray-400">Cliente:</strong> ${booking.clientName}</p>
        <p><strong class="text-gray-400">Serviços:</strong> ${booking.services.map(s => s.name).join(', ')}</p>
        <p><strong class="text-gray-400">Profissional:</strong> ${booking.staffName}</p>
        <p><strong class="text-gray-400">Data e Hora:</strong> ${formattedDate} às ${booking.time}</p>
        <p><strong class="text-gray-400">Total:</strong> R$ ${booking.totalPrice.toFixed(2)}</p>
      `;
      modal.classList.remove('hidden');
    }

    function closeModal() {
      document.getElementById('modal-success').classList.add('hidden');
    }

    function sendWhatsAppNotify() {
      if (!currentCreatedBooking) return;
      const b = currentCreatedBooking;
      const formattedDate = new Date(b.date + 'T00:00:00').toLocaleDateString('pt-BR');
      const text = `Olá! Fiz um agendamento no site NEXSITE:%0A%0A` +
        `*Código:* ${b.id}%0A` +
        `*Cliente:* ${b.clientName}%0A` +
        `*Telefone:* ${b.clientPhone}%0A` +
        `*Serviços:* ${b.services.map(s => s.name).join(', ')}%0A` +
        `*Profissional:* ${b.staffName}%0A` +
        `*Data:* ${formattedDate} às ${b.time}%0A` +
        `*Valor:* R$ ${b.totalPrice.toFixed(2)}`;
      window.open(`https://wa.me/${DB.salonPhone}?text=${text}`, '_blank');
    }

    function populateAdminFilters() {
      const select = document.getElementById('admin-filter-staff');
      select.innerHTML = '<option value="all">Todos Profissionais</option>' + 
        DB.staff.map(st => `<option value="${st.id}">${st.name}</option>`).join('');
    }

    function renderAdminTable() {
      const tbody = document.getElementById('admin-table-body');
      const filterDate = document.getElementById('admin-filter-date').value;
      const filterStaff = document.getElementById('admin-filter-staff').value;

      let filtered = bookings;
      if (filterDate) filtered = filtered.filter(b => b.date === filterDate);
      if (filterStaff !== 'all') filtered = filtered.filter(b => b.staffId === filterStaff);

      document.getElementById('stat-total').innerText = filtered.length;
      document.getElementById('stat-confirmed').innerText = filtered.filter(b => b.status === 'Confirmado').length;
      
      const totalRev = filtered.filter(b => b.status !== 'Cancelado').reduce((acc, b) => acc + b.totalPrice, 0);
      document.getElementById('stat-revenue').innerText = `R$ ${totalRev.toFixed(2)}`;

      if (filtered.length > 0) {
        const counts = {};
        filtered.forEach(b => counts[b.staffName] = (counts[b.staffName] || 0) + 1);
        document.getElementById('stat-top-staff').innerText = Object.keys(counts).reduce((a, b) => counts[a] > counts[b] ? a : b);
      } else {
        document.getElementById('stat-top-staff').innerText = '-';
      }

      if (filtered.length === 0) {
        tbody.innerHTML = `<tr><td colspan="7" class="p-8 text-center text-gray-500 italic">Nenhum agendamento encontrado.</td></tr>`;
        return;
      }

      tbody.innerHTML = filtered.map(b => {
        const statusColors = {
          'Confirmado': 'bg-emerald-500/10 text-emerald-400 border-emerald-500/30',
          'Concluído': 'bg-blue-500/10 text-blue-400 border-blue-500/30',
          'Cancelado': 'bg-red-500/10 text-red-400 border-red-500/30'
        };
        const formattedDate = new Date(b.date + 'T00:00:00').toLocaleDateString('pt-BR');
        return `
          <tr class="hover:bg-gray-900/50 transition-colors">
            <td class="p-3"><span class="font-bold text-white block">${b.time}</span><span class="text-[10px] text-gray-500">${formattedDate}</span></td>
            <td class="p-3"><span class="font-semibold text-white block">${b.clientName}</span><span class="text-[10px] text-gray-400">${b.clientPhone}</span></td>
            <td class="p-3 font-medium text-gray-300">${b.services.map(s => s.name).join(', ')}</td>
            <td class="p-3 text-amber-400 font-semibold">${b.staffName}</td>
            <td class="p-3 font-extrabold text-white">R$ ${b.totalPrice.toFixed(2)}</td>
            <td class="p-3"><span class="px-2 py-1 rounded-md text-[10px] font-bold border ${statusColors[b.status]}">${b.status}</span></td>
            <td class="p-3 text-right space-x-1">
              <button onclick="updateBookingStatusInCloud('${b.id}', 'Concluído')" title="Concluir" class="p-1.5 bg-blue-600/20 text-blue-400 hover:bg-blue-600 hover:text-white rounded-lg"><i class="fa-solid fa-check"></i></button>
              <button onclick="updateBookingStatusInCloud('${b.id}', 'Cancelado')" title="Cancelar" class="p-1.5 bg-red-600/20 text-red-400 hover:bg-red-600 hover:text-white rounded-lg"><i class="fa-solid fa-xmark"></i></button>
              <button onclick="deleteBookingFromCloud('${b.id}')" title="Excluir" class="p-1.5 bg-gray-800 text-gray-400 hover:bg-gray-700 hover:text-white rounded-lg"><i class="fa-solid fa-trash"></i></button>
            </td>
          </tr>
        `;
      }).join('');
    }
  </script>
</body>
</html>
