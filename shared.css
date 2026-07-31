// ============================================================
// shared.js — MamaFood v2
// ============================================================

// ── Proteção básica (não bloqueia thread) ─────────────────────────
(function(){
  document.addEventListener('contextmenu', function(e){ e.preventDefault(); });
  document.addEventListener('keydown', function(e){
    var k = e.key || '';
    if (e.keyCode === 123) { e.preventDefault(); return false; }
    if (e.ctrlKey && e.shiftKey && 'ijcIJC'.indexOf(k) !== -1) { e.preventDefault(); return false; }
    if (e.ctrlKey && 'uUsSpP'.indexOf(k) !== -1) { e.preventDefault(); return false; }
  }, true);
  document.addEventListener('selectstart', function(e){
    if (!['INPUT','TEXTAREA','SELECT'].includes(e.target.tagName)) e.preventDefault();
  });
  var _s = document.createElement('style');
  _s.textContent = '*{-webkit-user-select:none!important;user-select:none!important}input,textarea,select{-webkit-user-select:text!important;user-select:text!important}';
  (document.head || document.documentElement).appendChild(_s);
  // Detecta DevTools por diferença de tamanho
  var _dtOpen = false;
  setInterval(function(){
    var dw = window.outerWidth  - window.innerWidth  > 200;
    var dh = window.outerHeight - window.innerHeight > 200;
    if ((dw || dh) && !_dtOpen) {
      _dtOpen = true;
      document.documentElement.innerHTML = '<html><head></head><body style="background:#111;display:flex;align-items:center;justify-content:center;height:100vh"><p style="color:#ff4444;font-family:monospace;font-size:14px">Acesso n\u00e3o autorizado.</p></body></html>';
    } else if (!dw && !dh) { _dtOpen = false; }
  }, 800);
})();

// ── .env / ADMIN_EMAILS ───────────────────────────────────────────
// Fallback hardcoded — funciona mesmo sem fetch
var ADMIN_EMAILS = ['francimarjuniorr435@gmail.com'];
var _envLoaded   = false;

function loadEnv(cb) {
  console.log('🔄 loadEnv() iniciado, _envLoaded:', _envLoaded);
  if (_envLoaded) { 
    console.log('✅ .env já carregado, ADMIN_EMAILS:', ADMIN_EMAILS);
    cb(); 
    return; 
  }
  var tried = 0;
  var paths  = ['../../.env', '../.env', '/.env', '.env'];
  function tryPath(i) {
    if (i >= paths.length) { 
      console.warn('⚠️ .env não encontrado em nenhum path, usando fallback:', ADMIN_EMAILS);
      _envLoaded = true; 
      cb(); 
      return; 
    }
    console.log('🔍 Tentando carregar:', paths[i]);
    fetch(paths[i] + '?t=' + Date.now())
      .then(function(r){ return r.ok ? r.text() : Promise.reject('not ok'); })
      .then(function(txt){
        console.log('✅ .env carregado de', paths[i], 'conteúdo:', txt.substring(0, 100));
        var m = txt.match(/^ADMIN_EMAILS\s*=\s*([^\r\n]+)/m);
        if (m) {
          ADMIN_EMAILS = m[1].trim().split(',').map(function(e){
            return e.trim().toLowerCase();
          }).filter(Boolean);
          console.log('📧 ADMIN_EMAILS extraídos:', ADMIN_EMAILS);
        }
        _envLoaded = true; cb();
      })
      .catch(function(err){ 
        console.log('❌ Falha ao carregar', paths[i], err);
        tryPath(i + 1); 
      });
  }
  tryPath(0);
}

// ── Parceiro ──────────────────────────────────────────────────────
function getParceiro(){ return JSON.parse(localStorage.getItem('mf_parceiro') || 'null'); }

function isAdmin(){
  var p = getParceiro();
  if (!p || !p.email) return false;
  return ADMIN_EMAILS.indexOf(p.email.toLowerCase()) !== -1;
}

// ── Auth guard ────────────────────────────────────────────────────
function authGuard(adminOnly, cb) {
  console.log('🚪 authGuard() iniciado, adminOnly:', adminOnly);
  var p = getParceiro();
  if (!p) { 
    console.log('❌ Sem parceiro no localStorage, redirecionando para Tela1');
    window.location.href = 'Tela1.html'; 
    return; 
  }
  console.log('👤 Parceiro encontrado:', p);
  loadEnv(function(){
    console.log('🏗️ Chamando buildSidebar...');
    buildSidebar(window.location.pathname.split('/').pop());
    startClock('clock');
    if (adminOnly && !isAdmin()) {
      console.log('🔒 Acesso negado: página admin-only mas usuário não é admin');
      var main = document.querySelector('.main');
      if (main) main.innerHTML =
        '<div style="display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:70vh;gap:16px;padding:40px;text-align:center">' +
        '<i class="fa-solid fa-lock" style="font-size:3rem;color:#ea1d2c"></i>' +
        '<h2 style="font-family:Inter,sans-serif;color:#18181b">Acesso restrito</h2>' +
        '<p style="color:#71717a;font-family:Inter,sans-serif">Apenas administradores podem acessar esta página.</p>' +
        '<a href="Tela2.html" style="color:#ea1d2c;font-weight:700;font-family:Inter,sans-serif">← Voltar ao painel</a></div>';
      return;
    }
    console.log('✅ authGuard completo, executando callback da página');
    if (cb) cb();
  });
}

// ── Sidebar ───────────────────────────────────────────────────────
function buildSidebar(activePage) {
  console.log('🔧 buildSidebar() INICIOU', {activePage: activePage});
  if (!activePage) activePage = window.location.pathname.split('/').pop() || '';
  var p     = getParceiro();
  var admin = isAdmin();
  console.log('👤 Dados do parceiro:', p);
  console.log('🔑 É admin?', admin, 'ADMIN_EMAILS:', ADMIN_EMAILS);
  var name  = p ? (p.nome || 'Meu Restaurante') : '—';
  var addr  = p ? ((p.rua||'') + (p.numero ? ', '+p.numero : '') + (p.cidade ? ' — '+p.cidade : '')) : '—';

  var adminHtml = admin ? (
    '<div class="sb-section">Admin</div>' +
    _sb('fa-bag-shopping',      'Pedidos',        'pedidos.html',        activePage, true,  'badge-new') +
    _sb('fa-clock-rotate-left', 'Histórico',      'historico.html',      activePage) +
    _sb('fa-plus-circle',       'Cardápio Criar', 'cardapio-criar.html', activePage)
  ) : '';

  var html =
    '<div class="sb-logo"><i class="fa-solid fa-bowl-food"></i> mama<strong>food</strong></div>' +
    '<div class="sb-store"><div class="sb-store-name">'+esc(name)+'</div><div class="sb-store-addr">'+esc(addr)+'</div></div>' +
    '<nav class="sb-nav">' +
      '<div class="sb-section">Menu</div>' +
      _sb('fa-utensils',   'Cardápio',       'cardapio.html',     activePage) +
      _sb('fa-receipt',    'Meus Pedidos',   'meus-pedidos.html', activePage) +
      _sb('fa-motorcycle', 'Taxa e Entrega', 'taxa-entrega.html', activePage) +
      adminHtml +
      '<div class="sb-section">Loja</div>' +
      _sb('fa-store', 'Meu Perfil', 'perfil.html', activePage) +
    '</nav>' +
    '<div class="sb-footer"><div class="sb-logout" onclick="logout()"><i class="fa-solid fa-right-from-bracket"></i> Sair da conta</div></div>';

  console.log('📝 HTML gerado (primeiros 200 chars):', html.substring(0, 200));
  var el = document.getElementById('sidebar');
  console.log('🎯 Elemento sidebar encontrado?', !!el);
  if (el) {
    el.innerHTML = html;
    console.log('✅ innerHTML atribuído, sidebar deve estar visível agora');
  } else {
    console.error('❌ ERRO: elemento #sidebar NÃO encontrado no DOM!');
  }
}

function _sb(icon, label, href, active, hasBadge, badgeId) {
  var cls   = active === href ? 'sb-item active' : 'sb-item';
  var badge = hasBadge && badgeId ? '<span class="badge" id="'+badgeId+'">0</span>' : '';
  return '<a class="'+cls+'" href="'+href+'"><i class="fa-solid '+icon+'"></i>'+label+badge+'</a>';
}

function esc(s){ return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

// ── Relógio ───────────────────────────────────────────────────────
function startClock(id) {
  function tick() {
    var el = document.getElementById(id);
    if (!el) return;
    var n = new Date();
    el.textContent = String(n.getHours()).padStart(2,'0') + ':' + String(n.getMinutes()).padStart(2,'0');
  }
  tick();
  setInterval(tick, 1000);
}

// ── Toast ─────────────────────────────────────────────────────────
function showToast(msg, type) {
  var wrap = document.getElementById('toastWrap');
  if (!wrap) return;
  var t = document.createElement('div');
  t.className = 'toast ' + (type || 'ok');
  t.textContent = msg;
  wrap.appendChild(t);
  setTimeout(function(){ if (t.parentNode) t.parentNode.removeChild(t); }, 3200);
}

// ── Logout ────────────────────────────────────────────────────────
function logout() {
  if (confirm('Deseja sair da conta?')) {
    localStorage.removeItem('mf_parceiro');
    localStorage.removeItem('mf_pedidos');
    window.location.href = 'Tela1.html';
  }
}

// ── Sidebar mobile ────────────────────────────────────────────────
function toggleSidebar() {
  var sb = document.getElementById('sidebar');
  if (sb) sb.classList.toggle('open');
}
window.addEventListener('resize', function(){
  var btn = document.getElementById('menu-btn');
  if (btn) btn.style.display = window.innerWidth <= 768 ? 'flex' : 'none';
});
