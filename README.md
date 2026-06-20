<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>U.I.T • Glendale Tactical OS v27</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <style>
    body {
      background: linear-gradient(135deg, #0a0a0a 0%, #111827 100%);
      font-family: 'system-ui', -apple-system, BlinkMacSystemFont, sans-serif;
      color: #e0f2e9;
    }
    .glass {
      background: rgba(15, 23, 42, 0.75);
      backdrop-filter: blur(24px);
      border: 1px solid rgba(52, 211, 153, 0.3);
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.6);
    }
    .nav-item {
      transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    }
    .nav-item:hover, .nav-item.active {
      background: rgba(16, 185, 129, 0.15);
      border-left: 5px solid #34d399;
      transform: translateX(8px);
    }
    .header {
      background: linear-gradient(to right, #0f172a, #1e2937);
      box-shadow: 0 4px 20px rgba(52, 211, 153, 0.2);
    }
    .card-hover:hover {
      transform: translateY(-8px);
      box-shadow: 0 20px 40px rgba(52, 211, 153, 0.15);
    }
  </style>
</head>
<body class="min-h-screen">

<div class="flex h-screen overflow-hidden">

  <!-- SIDEBAR MILITAIRE -->
  <div class="w-80 glass flex flex-col border-r border-emerald-800">
    <div class="header p-6 flex items-center gap-4 border-b border-emerald-700">
      <div class="w-14 h-14 bg-gradient-to-br from-emerald-400 to-cyan-400 rounded-2xl flex items-center justify-center text-4xl font-black text-black shadow-lg">U</div>
      <div>
        <div class="text-3xl font-black tracking-widest text-emerald-300">U.I.T</div>
        <div class="text-xs text-emerald-500 tracking-[3px]">ARMÉE GLENDALE • OS 27</div>
      </div>
    </div>

    <div class="flex-1 p-5 space-y-2 overflow-auto">
      <div onclick="showSection('dashboard')" class="nav-item active flex items-center gap-4 px-6 py-5 rounded-3xl cursor-pointer"><i class="fas fa-tachometer-alt text-xl"></i> Tableau de Bord</div>
      <div onclick="showSection('verification')" class="nav-item flex items-center gap-4 px-6 py-5 rounded-3xl cursor-pointer"><i class="fas fa-shield-alt text-xl"></i> Vérification</div>
      <div onclick="showSection('soldats')" class="nav-item flex items-center gap-4 px-6 py-5 rounded-3xl cursor-pointer"><i class="fas fa-users text-xl"></i> Soldats & Photos</div>
      <div onclick="showSection('demandes')" class="nav-item flex items-center gap-4 px-6 py-5 rounded-3xl cursor-pointer"><i class="fas fa-file-signature text-xl"></i> Demandes Stage</div>
      <div onclick="showSection('rapports')" class="nav-item flex items-center gap-4 px-6 py-5 rounded-3xl cursor-pointer"><i class="fas fa-file-lines text-xl"></i> Rapports</div>
    </div>

    <div class="p-5 border-t border-emerald-800">
      <button onclick="adminAccess()" class="w-full py-5 glass rounded-3xl text-amber-400 hover:bg-amber-400/10 flex items-center justify-center gap-3 font-semibold">
        <i class="fas fa-user-shield"></i> ADMINISTRATION
      </button>
    </div>
  </div>

  <!-- MAIN CONTENT -->
  <div class="flex-1 flex flex-col overflow-hidden">
    <div class="header h-16 flex items-center px-8 border-b border-emerald-800">
      <h1 id="pageTitle" class="text-2xl font-semibold">Tableau de Bord</h1>
      <div class="ml-auto flex items-center gap-6 text-sm">
        <span class="flex items-center gap-2 text-emerald-400"><i class="fas fa-circle animate-pulse"></i> EN LIGNE</span>
      </div>
    </div>

    <div class="flex-1 overflow-auto p-10">

      <!-- DASHBOARD -->
      <div id="dashboard" class="section">
        <h2 class="text-5xl font-bold mb-10">Bienvenue, Commandant</h2>
        <div class="grid grid-cols-1 md:grid-cols-4 gap-6">
          <div class="glass p-8 rounded-3xl card-hover text-center"><div class="text-6xl font-bold text-emerald-400">23</div><div class="mt-2">Soldats Actifs</div></div>
          <div class="glass p-8 rounded-3xl card-hover text-center"><div class="text-6xl font-bold text-amber-400">7</div><div class="mt-2">Demandes</div></div>
          <div class="glass p-8 rounded-3xl card-hover text-center"><div class="text-6xl font-bold text-cyan-400">96%</div><div class="mt-2">Taux Validation</div></div>
          <div class="glass p-8 rounded-3xl card-hover text-center"><div class="text-6xl font-bold text-purple-400">41</div><div class="mt-2">Missions</div></div>
        </div>
      </div>

      <!-- VÉRIFICATION -->
      <div id="verification" class="section hidden">
        <h2 class="text-4xl font-bold mb-8">Vérification Tactique</h2>
        <div class="max-w-xl glass p-10 rounded-3xl">
          <input id="verifNom" placeholder="Nom complet du soldat" class="w-full p-6 bg-zinc-950 border border-emerald-700 rounded-3xl text-lg mb-6">
          <button onclick="verifierSoldat()" class="w-full py-7 bg-emerald-500 hover:bg-emerald-600 rounded-3xl font-bold text-xl">VÉRIFIER IDENTITÉ</button>
          <div id="verifResult" class="mt-10"></div>
        </div>
      </div>

      <!-- SOLDATS + PHOTOS -->
      <div id="soldats" class="section hidden">
        <h2 class="text-4xl font-bold mb-8">Base de Données Soldats</h2>
        <div class="glass p-10 rounded-3xl max-w-2xl mb-10">
          <input id="photoUrl" placeholder="URL Photo du soldat" class="w-full p-5 mb-4 glass rounded-3xl">
          <input id="sNom" placeholder="Nom complet" class="w-full p-5 mb-4 glass rounded-3xl">
          <input id="sGrade" placeholder="Grade" class="w-full p-5 mb-4 glass rounded-3xl">
          <button onclick="ajouterSoldat()" class="w-full py-7 bg-gradient-to-r from-emerald-400 to-cyan-400 text-black font-bold rounded-3xl text-lg">➕ AJOUTER SOLDAT</button>
        </div>
        <div id="soldatsGrid" class="grid grid-cols-1 md:grid-cols-3 gap-8"></div>
      </div>

      <!-- RAPPORTS -->
      <div id="rapports" class="section hidden">
        <h2 class="text-4xl font-bold mb-8">Rédaction de Rapport</h2>
        <div class="glass p-10 rounded-3xl">
          <textarea id="rapportText" rows="10" placeholder="Rédigez votre rapport officiel ici..." class="w-full p-6 glass rounded-3xl"></textarea>
          <button onclick="sauvegarderRapport()" class="mt-6 w-full py-7 bg-white/10 hover:bg-white/20 rounded-3xl font-bold">📄 ENREGISTRER RAPPORT</button>
        </div>
      </div>

    </div>
  </div>
</div>

<script>
// Données persistantes
let soldats = JSON.parse(localStorage.getItem('uitSoldats')) || [];

// Navigation
function showSection(id) {
  document.querySelectorAll('.section').forEach(s => s.classList.add('hidden'));
  document.getElementById(id).classList.remove('hidden');
  document.getElementById('pageTitle').textContent = {
    'dashboard': 'Tableau de Bord',
    'verification': 'Vérification Tactique',
    'soldats': 'Gestion Soldats',
    'rapports': 'Rapports Officiels'
  }[id];
}

// Ajouter soldat
function ajouterSoldat() {
  const nom = document.getElementById('sNom').value.trim();
  const grade = document.getElementById('sGrade').value.trim();
  const photo = document.getElementById('photoUrl').value.trim() || 'https://picsum.photos/id/64/600/400';

  if (!nom || !grade) return alert("Nom et grade sont obligatoires");

  soldats.push({nom, grade, photo});
  localStorage.setItem('uitSoldats', JSON.stringify(soldats));
  afficherSoldats();
  alert("✅ Soldat ajouté avec photo !");
}

function afficherSoldats() {
  const container = document.getElementById('soldatsGrid');
  container.innerHTML = '';
  soldats.forEach(s => {
    const div = document.createElement('div');
    div.className = "glass rounded-3xl overflow-hidden card-hover";
    div.innerHTML = `
      <img src="${s.photo}" class="w-full h-64 object-cover">
      <div class="p-6">
        <h3 class="font-bold text-xl">${s.nom}</h3>
        <p class="text-emerald-400">${s.grade}</p>
      </div>
    `;
    container.appendChild(div);
  });
}

// Vérification
function verifierSoldat() {
  const nom = document.getElementById('verifNom').value.trim();
  const result = document.getElementById('verifResult');
  result.innerHTML = nom ? 
    `<div class="glass p-10 rounded-3xl text-center text-3xl text-emerald-400">✅ ${nom}<br><span class="text-lg">Accès Autorisé</span></div>` : 
    `<div class="text-amber-400 text-center">Veuillez entrer un nom</div>`;
}

// Rapport
function sauvegarderRapport() {
  const text = document.getElementById('rapportText').value;
  if (text) alert("✅ Rapport officiel enregistré avec succès !");
  else alert("Écrivez le contenu du rapport");
}

// Admin
function adminAccess() {
  const mdp = prompt("🔐 Mot de passe Administration :");
  if (mdp === "Kassano@10") alert("✅ Bienvenue dans l'Administration U.I.T");
  else alert("❌ Accès Refusé");
}

// Initialisation
afficherSoldats();
showSection('dashboard');
</script>
</body>
</html>
