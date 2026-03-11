<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Laïcité Interactive — Jeux pédagogiques</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Source+Serif+4:ital,wght@0,300;0,400;1,300&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#f2ede3;--white:#fff;--ink:#1a1410;--gold:#b8922a;--gold-lt:#d4ae52;
  --navy:#162444;--red:#c82020;--green:#2a6038;--muted:#888;--border:#d8d0c0;
  --cell:44px;
}
html{scroll-behavior:smooth}
body{background:var(--bg);font-family:"Source Serif 4",serif;color:var(--ink);min-height:100vh}

/* NAV */
.nav{position:sticky;top:0;z-index:100;background:var(--navy);display:flex;align-items:center;justify-content:space-between;padding:0 16px;height:52px;box-shadow:0 2px 12px rgba(0,0,0,.25)}
.nav-title{font-family:"Playfair Display",serif;font-size:.9rem;color:var(--gold-lt);letter-spacing:.06em;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;max-width:160px}
.nav-tabs{display:flex;gap:4px}
.nav-tab{background:transparent;border:1px solid rgba(184,146,42,.4);color:rgba(255,255,255,.7);font-family:"Playfair Display",serif;font-size:.72rem;letter-spacing:.05em;padding:5px 12px;border-radius:2px;cursor:pointer;transition:all .2s;white-space:nowrap}
.nav-tab.active,.nav-tab:hover{background:var(--gold);border-color:var(--gold);color:var(--ink)}

/* PAGES */
.page{display:none}.page.active{display:block}

/* HOME */
.home{max-width:680px;margin:0 auto;padding:40px 20px 60px;text-align:center}
.home-badge{display:inline-block;background:var(--gold);color:var(--ink);font-family:"Playfair Display",serif;font-size:.68rem;letter-spacing:.12em;padding:4px 14px;border-radius:20px;margin-bottom:18px;text-transform:uppercase}
.home h1{font-family:"Playfair Display",serif;font-size:clamp(1.5rem,4vw,2.2rem);line-height:1.2;margin-bottom:14px}
.home-sub{font-size:.95rem;color:var(--muted);font-style:italic;line-height:1.7;margin-bottom:36px}
.home-line{width:50px;height:2px;background:var(--gold);margin:0 auto 36px}
.home-cards{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:14px;text-align:left}
.home-card{background:var(--white);border:1px solid var(--border);border-radius:6px;padding:22px;cursor:pointer;transition:transform .2s,box-shadow .2s;box-shadow:0 2px 8px rgba(0,0,0,.06)}
.home-card:hover{transform:translateY(-3px);box-shadow:0 8px 24px rgba(0,0,0,.12)}
.home-card-icon{font-size:2rem;margin-bottom:10px;display:block}
.home-card h2{font-family:"Playfair Display",serif;font-size:1rem;margin-bottom:7px}
.home-card p{font-size:.8rem;color:var(--muted);font-style:italic;line-height:1.6}
.hc-btn{display:inline-block;margin-top:14px;background:var(--navy);color:white;font-family:"Playfair Display",serif;font-size:.7rem;letter-spacing:.06em;padding:6px 16px;border-radius:2px;border:none;cursor:pointer;transition:background .2s}
.hc-btn:hover{background:var(--gold);color:var(--ink)}

/* PAGE HEADER */
.cartes-page,.cross-page{padding:20px 16px 60px}
.page-header{text-align:center;margin-bottom:22px}
.page-header h2{font-family:"Playfair Display",serif;font-size:1.2rem}
.page-header p{font-size:.8rem;color:var(--muted);font-style:italic;margin-top:4px}
.page-header-line{width:44px;height:2px;background:var(--gold);margin:8px auto 0}

/* BUTTONS */
.btn{font-family:"Playfair Display",serif;font-size:.75rem;letter-spacing:.06em;border-radius:2px;cursor:pointer;padding:7px 18px;transition:all .2s}
.btn-primary{background:var(--navy);color:white;border:1px solid var(--navy)}
.btn-primary:hover{background:var(--gold);border-color:var(--gold);color:var(--ink)}
.btn-success{background:transparent;color:var(--green);border:1px solid var(--green)}
.btn-success:hover{background:var(--green);color:white}
.btn-muted{background:transparent;color:var(--muted);border:1px solid var(--muted)}
.btn-muted:hover{background:var(--muted);color:white}

/* CONSIGNE */
.consigne{background:var(--navy);color:white;border-radius:6px;padding:12px 18px;max-width:820px;margin:0 auto 20px;font-size:.82rem;line-height:1.6;display:flex;align-items:center;gap:10px}
.consigne-icon{font-size:1.3rem;flex-shrink:0}

/* CARTES ACTIONS */
.cartes-actions{display:flex;gap:8px;justify-content:center;margin-bottom:18px;flex-wrap:wrap}
.cartes-result{text-align:center;font-family:"Playfair Display",serif;font-size:.95rem;min-height:26px;margin-bottom:14px}
.cartes-result.ok{color:var(--green)}.cartes-result.bad{color:#c82020}

/* SORT ZONE */
.sort-zone{max-width:880px;margin:0 auto}
.sort-label{font-family:"Playfair Display",serif;font-size:.78rem;color:var(--muted);margin-bottom:8px;padding-left:2px}

.slots-row{display:flex;gap:7px;overflow-x:auto;padding-bottom:12px;scroll-snap-type:x mandatory;-webkit-overflow-scrolling:touch}
.slot{flex-shrink:0;width:78px;height:78px;border:2px dashed #c8b880;border-radius:6px;display:flex;align-items:center;justify-content:center;font-family:"Playfair Display",serif;font-size:.68rem;color:#c8b880;scroll-snap-align:start;transition:background .2s,border-color .2s;position:relative;cursor:default}
.slot.drag-over{border-color:var(--gold);background:rgba(184,146,42,.1)}
.slot-num{position:absolute;top:3px;left:5px;font-size:.6rem;color:#c8b880;font-family:"Source Serif 4",serif}

.cards-pool{display:flex;flex-wrap:wrap;gap:8px;margin-top:16px}

/* MINI CARD */
.mini-card{width:78px;background:white;border:1px solid var(--border);border-radius:4px;overflow:hidden;cursor:grab;box-shadow:0 2px 6px rgba(0,0,0,.1);transition:transform .15s,box-shadow .15s,opacity .15s;user-select:none;touch-action:none}
.mini-card:active{cursor:grabbing}
.mini-card.dragging{opacity:.45;transform:scale(1.05);box-shadow:0 8px 20px rgba(0,0,0,.2)}
.mini-card.correct-pos{border:2px solid var(--green);box-shadow:0 0 0 2px rgba(42,96,56,.25)}
.mini-card.wrong-pos{border:2px solid var(--red);box-shadow:0 0 0 2px rgba(200,32,32,.25)}
.mini-illus{width:100%;height:52px;background:#faf8f4;border-bottom:1px solid #e8e0d0;overflow:hidden;display:flex;align-items:center;justify-content:center}
.mini-illus svg{width:100%;height:100%}
.mini-title{font-family:"Playfair Display",serif;font-size:4.8pt;font-weight:700;color:var(--ink);text-align:center;padding:4px 3px 5px;line-height:1.25}

/* CROSSWORD */
.cross-layout{display:flex;gap:24px;justify-content:center;align-items:flex-start;flex-wrap:wrap}
.grid-wrap{background:white;border:1px solid var(--border);border-radius:4px;padding:14px;box-shadow:0 2px 16px rgba(0,0,0,.08);overflow-x:auto;max-width:100%}
.cw-grid{display:inline-grid;grid-template-columns:repeat(17,var(--cell));grid-template-rows:repeat(15,var(--cell));gap:2px;background:var(--bg);border:1px solid var(--border)}
.cw-cell{width:var(--cell);height:var(--cell);background:var(--bg)}
.cw-cell.active{background:white;border:1px solid #c0b070;position:relative}
.cw-cell.active input{width:100%;height:100%;border:none;outline:none;background:transparent;text-align:center;font-family:"Playfair Display",serif;font-size:clamp(.65rem,2vw,.95rem);font-weight:700;color:var(--ink);text-transform:uppercase;caret-color:var(--gold);cursor:pointer;padding:0}
.cw-cell.active input:focus{background:rgba(184,146,42,.12)}
.cw-cell.correct input{color:var(--green)}.cw-cell.wrong input{color:var(--red)}.cw-cell.revealed input{color:var(--navy);font-style:italic}
.cw-cell.highlight input{background:rgba(184,146,42,.18)}
.cell-num{position:absolute;top:2px;left:3px;font-size:.4rem;color:var(--gold);line-height:1;pointer-events:none;font-family:"Source Serif 4",serif}
.cw-clues{width:250px;flex-shrink:0}
.clue-section{background:white;border:1px solid var(--border);border-radius:4px;padding:12px;margin-bottom:10px;box-shadow:0 1px 8px rgba(0,0,0,.05)}
.clue-section h3{font-family:"Playfair Display",serif;font-size:.78rem;color:var(--navy);margin-bottom:9px;padding-bottom:5px;border-bottom:1px solid var(--border);letter-spacing:.05em;text-transform:uppercase}
.clue-list{list-style:none}
.clue-item{display:flex;gap:7px;padding:4px 5px;border-radius:3px;cursor:pointer;transition:background .15s;font-size:.7rem;line-height:1.4}
.clue-item:hover{background:rgba(184,146,42,.08)}.clue-item.active-clue{background:rgba(184,146,42,.18)}
.clue-num{font-family:"Playfair Display",serif;font-weight:700;color:var(--gold);min-width:18px;text-align:right;flex-shrink:0}
.cw-actions{display:flex;gap:8px;justify-content:center;margin-top:16px;flex-wrap:wrap}
.score-bar{text-align:center;font-family:"Playfair Display",serif;font-size:.82rem;color:var(--muted);min-height:22px;margin-top:10px}
.score-bar.good{color:var(--green)}.score-bar.bad{color:var(--red)}

@media(max-width:600px){
  :root{--cell:30px}
  .nav-title{max-width:110px;font-size:.8rem}
  .nav-tab{font-size:.65rem;padding:4px 9px}
  .cw-clues{width:100%}
  .mini-card{width:72px}
  .slot{width:72px;height:72px}
  .mini-illus{height:46px}
}
</style>
</head>
<body>

<nav class="nav">
  <span class="nav-title">&#9670; La Laïcité</span>
  <div class="nav-tabs">
    <button class="nav-tab active" onclick="showPage('home')">Accueil</button>
    <button class="nav-tab" onclick="showPage('cartes')">🃏 Cartes</button>
    <button class="nav-tab" onclick="showPage('croises')">✏️ Mots croisés</button>
  </div>
</nav>

<!-- ACCUEIL -->
<div class="page active" id="page-home">
<div class="home">
  <span class="home-badge">Jeux pédagogiques</span>
  <h1>Histoire de la Laïcité en France</h1>
  <p class="home-sub">Deux activités interactives pour comprendre la construction de la laïcité, de 498 à aujourd'hui.</p>
  <div class="home-line"></div>
  <div class="home-cards">
    <div class="home-card" onclick="showPage('cartes')">
      <span class="home-card-icon">🃏</span>
      <h2>Chronologie interactive</h2>
      <p>22 cartes illustrées à remettre dans l'ordre chronologique. Glisser-déposer, tactile inclus.</p>
      <button class="hc-btn">Jouer →</button>
    </div>
    <div class="home-card" onclick="showPage('croises')">
      <span class="home-card-icon">✏️</span>
      <h2>Mots croisés</h2>
      <p>13 mots à trouver sur les personnages, lois et événements clés de la laïcité.</p>
      <button class="hc-btn">Jouer →</button>
    </div>
  </div>
</div>
</div>

<!-- CARTES -->
<div class="page" id="page-cartes">
<div class="cartes-page">
  <div class="page-header">
    <h2>Chronologie de la Laïcité</h2>
    <p>22 événements · de 498 à aujourd'hui</p>
    <div class="page-header-line"></div>
  </div>
  <div class="consigne">
    <span class="consigne-icon">👆</span>
    <span>Glissez les cartes dans les cases numérotées dans le <strong>bon ordre chronologique</strong>. Sur mobile, appuyez longuement et déplacez.</span>
  </div>
  <div class="cartes-actions">
    <button class="btn btn-success" onclick="checkOrder()">✓ Vérifier</button>
    <button class="btn btn-primary" onclick="revealOrder()">◎ Solution</button>
    <button class="btn btn-muted"   onclick="shuffleCards()">↺ Mélanger</button>
  </div>
  <div class="cartes-result" id="cartes-result"></div>
  <div class="sort-zone">
    <div class="sort-label">&#8595; Cases numérotées (glissez les cartes ici)</div>
    <div class="slots-row" id="slots-row"></div>
    <div class="sort-label" style="margin-top:18px">&#8595; Cartes à classer</div>
    <div class="cards-pool" id="cards-pool"></div>
  </div>
</div>
</div>

<!-- MOTS CROISÉS -->
<div class="page" id="page-croises">
<div class="cross-page">
  <div class="page-header">
    <h2>Mots Croisés — La Laïcité</h2>
    <p>13 mots · cliquez sur une définition pour surligner</p>
    <div class="page-header-line"></div>
  </div>
  <div class="cross-layout">
    <div>
      <div class="grid-wrap">
        <div class="cw-grid" id="cw-grid"></div>
      </div>
      <div class="cw-actions">
        <button class="btn btn-success" onclick="cwCheck()">✓ Vérifier</button>
        <button class="btn btn-primary" onclick="cwReveal()">◎ Solution</button>
        <button class="btn btn-muted"   onclick="cwReset()">↺ Recommencer</button>
      </div>
      <div class="score-bar" id="cw-score"></div>
    </div>
    <div class="cw-clues">
      <div class="clue-section">
        <h3>&#8594; Horizontalement</h3>
        <ul class="clue-list" id="clues-h"></ul>
      </div>
      <div class="clue-section">
        <h3>&#8595; Verticalement</h3>
        <ul class="clue-list" id="clues-v"></ul>
      </div>
    </div>
  </div>
</div>
</div>

<script>
// ════════ NAV ════════
function showPage(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(t=>t.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
  ['home','cartes','croises'].forEach((n,i)=>{if(n===id)document.querySelectorAll('.nav-tab')[i].classList.add('active')});
  window.scrollTo(0,0);
}

// ════════ CARTES DATA ════════
const CARDS_DATA = [{"id": 1, "title": "Baptême de Clovis", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <!-- Cuve --> <polygon points=\"93,95 93,58 101,48 117,48 125,58 125,95\" fill=\"#c8bca0\" stroke=\"#a09070\" stroke-width=\"1.5\"/> <polygon points=\"95,92 95,60 102,51 116,51 123,60 123,92\" fill=\"#7aaec8\"/> <ellipse cx=\"109\" cy=\"73\" rx=\"11\" ry=\"4\" fill=\"#a0cce0\" opacity=\".7\"/> <rect x=\"66\" y=\"93\" width=\"58\" height=\"6\" rx=\"1\" fill=\"#a09070\"/> <!-- Filet d'eau --> <path d=\"M68,64 Q84,72 95,78\" stroke=\"#7aaec8\" stroke-width=\"2.5\" stroke-linecap=\"round\" fill=\"none\"/> <!-- Évêque --> <rect x=\"38\" y=\"56\" width=\"22\" height=\"42\" rx=\"11\" fill=\"#8c1c28\"/> <circle cx=\"49\" cy=\"47\" r=\"10\" fill=\"#f0c890\"/> <polygon points=\"40,52 49,65 58,52\" fill=\"#f5f0e4\" stroke=\"#c8a840\" stroke-width=\".8\"/> <path d=\"M36,56 C24,46 24,33 35,31 C43,29 45,40 36,42\" stroke=\"#c8a840\" stroke-width=\"2\" fill=\"none\" stroke-linecap=\"round\"/> <!-- Clovis --> <rect x=\"120\" y=\"56\" width=\"22\" height=\"42\" rx=\"11\" fill=\"#1a3060\"/> <circle cx=\"131\" cy=\"47\" r=\"10\" fill=\"#f0c890\"/> <rect x=\"122\" y=\"55\" width=\"18\" height=\"4\" fill=\"#c8a840\"/> <polygon points=\"123,59 125,65 127,59\" fill=\"#c8a840\"/> <polygon points=\"130,59 132,65 134,59\" fill=\"#c8a840\"/> <polygon points=\"137,59 139,65 141,59\" fill=\"#c8a840\"/> <!-- Chrisme --> <line x1=\"93\" y1=\"10\" x2=\"93\" y2=\"34\" stroke=\"#c8a840\" stroke-width=\"2\"/> <line x1=\"81\" y1=\"20\" x2=\"105\" y2=\"20\" stroke=\"#c8a840\" stroke-width=\"2\"/> <path d=\"M93,12 C103,12 107,20 93,24\" stroke=\"#c8a840\" stroke-width=\"1.5\" fill=\"none\"/> </svg>"}, {"id": 2, "title": "Le Pape en Avignon", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <!-- Tour gauche --> <rect x=\"26\" y=\"34\" width=\"30\" height=\"86\" fill=\"#c8b880\"/> <rect x=\"26\" y=\"26\" width=\"9\" height=\"10\" fill=\"#c8b880\"/> <rect x=\"39\" y=\"26\" width=\"9\" height=\"10\" fill=\"#c8b880\"/> <!-- Corps --> <rect x=\"56\" y=\"50\" width=\"88\" height=\"70\" fill=\"#d8c898\"/> <!-- Créneaux corps --> <rect x=\"58\" y=\"44\" width=\"8\" height=\"8\" fill=\"#d8c898\"/> <rect x=\"70\" y=\"44\" width=\"8\" height=\"8\" fill=\"#d8c898\"/> <rect x=\"82\" y=\"44\" width=\"8\" height=\"8\" fill=\"#d8c898\"/> <rect x=\"94\" y=\"44\" width=\"8\" height=\"8\" fill=\"#d8c898\"/> <rect x=\"106\" y=\"44\" width=\"8\" height=\"8\" fill=\"#d8c898\"/> <rect x=\"118\" y=\"44\" width=\"8\" height=\"8\" fill=\"#d8c898\"/> <rect x=\"130\" y=\"44\" width=\"8\" height=\"8\" fill=\"#d8c898\"/> <!-- Tour droite --> <rect x=\"144\" y=\"34\" width=\"30\" height=\"86\" fill=\"#c8b880\"/> <rect x=\"144\" y=\"26\" width=\"9\" height=\"10\" fill=\"#c8b880\"/> <rect x=\"157\" y=\"26\" width=\"9\" height=\"10\" fill=\"#c8b880\"/> <!-- Fenêtre gothique --> <path d=\"M84,62 L84,88 Q100,102 116,88 L116,62 Z\" fill=\"#4a70a0\" opacity=\".75\"/> <!-- Porte --> <path d=\"M80,120 L80,98 Q100,84 120,98 L120,120 Z\" fill=\"#5a3e28\"/> <!-- Croix papale --> <line x1=\"41\" y1=\"14\" x2=\"41\" y2=\"26\" stroke=\"#c8a840\" stroke-width=\"2\"/> <line x1=\"35\" y1=\"18\" x2=\"47\" y2=\"18\" stroke=\"#c8a840\" stroke-width=\"2\"/> <line x1=\"37\" y1=\"22\" x2=\"45\" y2=\"22\" stroke=\"#c8a840\" stroke-width=\"1.3\"/> <!-- Fleur de lys --> <text x=\"152\" y=\"120\" font-size=\"18\" fill=\"#c8a840\" font-family=\"serif\" opacity=\".9\">⚜</text> </svg>"}, {"id": 3, "title": "Pragmatique Sanction de Bourges", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <rect x=\"22\" y=\"14\" width=\"142\" height=\"116\" rx=\"3\" fill=\"#f0e0b0\" stroke=\"#c8a840\" stroke-width=\"1.2\"/> <rect x=\"22\" y=\"14\" width=\"142\" height=\"10\" rx=\"3\" fill=\"#c0a040\"/> <rect x=\"22\" y=\"120\" width=\"142\" height=\"10\" rx=\"3\" fill=\"#c0a040\"/> <text x=\"93\" y=\"38\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"8\" font-weight=\"bold\" fill=\"#8c2020\">Pragmatique Sanction</text> <text x=\"93\" y=\"50\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"7.5\" fill=\"#8c2020\">de Bourges</text> <line x1=\"32\" y1=\"56\" x2=\"154\" y2=\"56\" stroke=\"#c8a840\" stroke-width=\".8\"/> <text x=\"36\" y=\"88\" font-family=\"serif\" font-size=\"30\" font-weight=\"bold\" fill=\"#8c2020\" opacity=\".9\">G</text> <line x1=\"62\" y1=\"68\" x2=\"154\" y2=\"68\" stroke=\"#b8a060\" stroke-width=\".6\" opacity=\".6\"/> <line x1=\"62\" y1=\"77\" x2=\"154\" y2=\"77\" stroke=\"#b8a060\" stroke-width=\".6\" opacity=\".6\"/> <line x1=\"32\" y1=\"98\" x2=\"154\" y2=\"98\" stroke=\"#b8a060\" stroke-width=\".6\" opacity=\".6\"/> <line x1=\"32\" y1=\"107\" x2=\"148\" y2=\"107\" stroke=\"#b8a060\" stroke-width=\".6\" opacity=\".6\"/> <!-- Couronne --> <rect x=\"32\" y=\"82\" width=\"22\" height=\"4\" rx=\"1\" fill=\"#c8a840\"/> <polygon points=\"33,86 36,93 39,86\" fill=\"#c8a840\"/> <polygon points=\"41,86 44,93 47,86\" fill=\"#c8a840\"/> <!-- Croix Rome barrée --> <line x1=\"132\" y1=\"72\" x2=\"132\" y2=\"90\" stroke=\"#a09070\" stroke-width=\"1.5\" stroke-dasharray=\"3,2\"/> <line x1=\"123\" y1=\"81\" x2=\"141\" y2=\"81\" stroke=\"#a09070\" stroke-width=\"1.5\" stroke-dasharray=\"3,2\"/> <line x1=\"121\" y1=\"70\" x2=\"143\" y2=\"92\" stroke=\"#8c2020\" stroke-width=\"2.2\"/> </svg>"}, {"id": 4, "title": "Édit de Nantes", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <ellipse cx=\"93\" cy=\"20\" rx=\"64\" ry=\"9\" fill=\"#b09040\"/> <rect x=\"29\" y=\"20\" width=\"128\" height=\"100\" fill=\"#f0e0b0\"/> <ellipse cx=\"93\" cy=\"120\" rx=\"64\" ry=\"9\" fill=\"#b09040\"/> <text x=\"93\" y=\"38\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"9\" font-weight=\"bold\" fill=\"#3a2808\">ÉDIT DE NANTES</text> <line x1=\"38\" y1=\"44\" x2=\"148\" y2=\"44\" stroke=\"#c8a840\" stroke-width=\".8\"/> <!-- Croix catholique --> <line x1=\"58\" y1=\"58\" x2=\"58\" y2=\"96\" stroke=\"#c8a840\" stroke-width=\"4\" stroke-linecap=\"round\"/> <line x1=\"44\" y1=\"71\" x2=\"72\" y2=\"71\" stroke=\"#c8a840\" stroke-width=\"4\" stroke-linecap=\"round\"/> <!-- Croix huguenote --> <line x1=\"128\" y1=\"58\" x2=\"128\" y2=\"96\" stroke=\"#1a3060\" stroke-width=\"4\" stroke-linecap=\"round\"/> <line x1=\"114\" y1=\"71\" x2=\"142\" y2=\"71\" stroke=\"#1a3060\" stroke-width=\"4\" stroke-linecap=\"round\"/> <circle cx=\"114\" cy=\"71\" r=\"4\" fill=\"none\" stroke=\"#1a3060\" stroke-width=\"1.5\"/> <circle cx=\"142\" cy=\"71\" r=\"4\" fill=\"none\" stroke=\"#1a3060\" stroke-width=\"1.5\"/> <circle cx=\"128\" cy=\"57\" r=\"4\" fill=\"none\" stroke=\"#1a3060\" stroke-width=\"1.5\"/> <circle cx=\"128\" cy=\"97\" r=\"4\" fill=\"none\" stroke=\"#1a3060\" stroke-width=\"1.5\"/> <!-- Égal --> <line x1=\"85\" y1=\"70\" x2=\"101\" y2=\"70\" stroke=\"#888\" stroke-width=\"2\"/> <line x1=\"85\" y1=\"76\" x2=\"101\" y2=\"76\" stroke=\"#888\" stroke-width=\"2\"/> <text x=\"93\" y=\"113\" text-anchor=\"middle\" font-family=\"serif\" font-style=\"italic\" font-size=\"7.5\" fill=\"#5a3818\">Henri IV</text> </svg>"}, {"id": 5, "title": "Révocation de l'Édit de Nantes", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <defs><radialGradient id=\"s5_f5\" cx=\"50%\" cy=\"100%\" r=\"80%\"><stop offset=\"0%\" stop-color=\"#f4a012\"/><stop offset=\"50%\" stop-color=\"#c84010\"/><stop offset=\"100%\" stop-color=\"#1a0e0a\"/></radialGradient></defs> <rect width=\"186\" height=\"144\" fill=\"url(#s5_f5)\"/> <rect x=\"0\" y=\"122\" width=\"186\" height=\"22\" fill=\"#2a1406\"/> <!-- Flammes --> <polygon points=\"36,122 50,70 62,102 74,58 86,94 98,122\" fill=\"#e04808\"/> <polygon points=\"88,122 102,62 116,96 128,54 140,90 154,122\" fill=\"#e04808\"/> <polygon points=\"56,122 68,80 78,106 88,74 98,100 108,122\" fill=\"#f4a012\"/> <polygon points=\"76,122 84,88 92,108 100,82 108,104 116,122\" fill=\"#fff8b0\" opacity=\".6\"/> <!-- Parchemin brûlé --> <rect x=\"58\" y=\"52\" width=\"70\" height=\"38\" rx=\"2\" fill=\"#f0e0b0\" opacity=\".72\" transform=\"rotate(-8 93 71)\"/> <text x=\"90\" y=\"72\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"7.5\" fill=\"#5a3818\" font-weight=\"bold\" transform=\"rotate(-8 90 72)\">Édit de Nantes</text> <!-- Soleil --> <circle cx=\"154\" cy=\"26\" r=\"19\" fill=\"#f4d040\"/> <g stroke=\"#d4a020\" stroke-width=\"1.4\"><line x1=\"154\" y1=\"4\" x2=\"154\" y2=\"-1\"/><line x1=\"169\" y1=\"8\" x2=\"174\" y2=\"3\"/><line x1=\"176\" y1=\"22\" x2=\"183\" y2=\"22\"/><line x1=\"170\" y1=\"36\" x2=\"176\" y2=\"42\"/><line x1=\"139\" y1=\"8\" x2=\"134\" y2=\"3\"/><line x1=\"132\" y1=\"22\" x2=\"125\" y2=\"22\"/><line x1=\"138\" y1=\"36\" x2=\"132\" y2=\"42\"/></g> <text x=\"154\" y=\"23\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.5\" fill=\"#3a2000\" font-weight=\"bold\">Louis XIV</text> <!-- Fugitifs --> <ellipse cx=\"22\" cy=\"120\" rx=\"6\" ry=\"8\" fill=\"#0e0806\" opacity=\".8\"/> <circle cx=\"22\" cy=\"110\" r=\"5\" fill=\"#0e0806\" opacity=\".8\"/> <ellipse cx=\"36\" cy=\"120\" rx=\"6\" ry=\"8\" fill=\"#0e0806\" opacity=\".6\"/> <circle cx=\"36\" cy=\"110\" r=\"5\" fill=\"#0e0806\" opacity=\".6\"/> </svg>"}, {"id": 6, "title": "Déclaration des Droits de l'Homme", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <!-- Tablette gauche --> <rect x=\"8\" y=\"14\" width=\"78\" height=\"106\" rx=\"4\" fill=\"#c0aa78\" stroke=\"#8b7340\" stroke-width=\"1.2\"/> <ellipse cx=\"47\" cy=\"14\" rx=\"39\" ry=\"9\" fill=\"#c0aa78\" stroke=\"#8b7340\" stroke-width=\"1.2\"/> <text x=\"47\" y=\"30\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"8\" fill=\"#8c2020\" font-weight=\"bold\">Art. X</text> <line x1=\"16\" y1=\"36\" x2=\"78\" y2=\"36\" stroke=\"#c8a840\" stroke-width=\".7\"/> <text x=\"47\" y=\"50\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.2\" fill=\"#3a2808\">Liberté</text> <text x=\"47\" y=\"62\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.2\" fill=\"#3a2808\">d'opinion</text> <text x=\"47\" y=\"74\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.2\" fill=\"#3a2808\">religieuse</text> <text x=\"47\" y=\"86\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.2\" fill=\"#3a2808\">garantie</text> <circle cx=\"47\" cy=\"108\" r=\"14\" fill=\"#002395\"/> <circle cx=\"47\" cy=\"108\" r=\"9.5\" fill=\"white\"/> <circle cx=\"47\" cy=\"108\" r=\"5\" fill=\"#ed2939\"/> <!-- Tablette droite --> <rect x=\"100\" y=\"14\" width=\"78\" height=\"106\" rx=\"4\" fill=\"#c0aa78\" stroke=\"#8b7340\" stroke-width=\"1.2\"/> <ellipse cx=\"139\" cy=\"14\" rx=\"39\" ry=\"9\" fill=\"#c0aa78\" stroke=\"#8b7340\" stroke-width=\"1.2\"/> <text x=\"139\" y=\"34\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"7.5\" fill=\"#1a3060\" font-weight=\"bold\">Liberté</text> <line x1=\"108\" y1=\"40\" x2=\"170\" y2=\"40\" stroke=\"#c8a840\" stroke-width=\".6\"/> <text x=\"139\" y=\"58\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"7.5\" fill=\"#1a3060\" font-weight=\"bold\">Égalité</text> <line x1=\"108\" y1=\"64\" x2=\"170\" y2=\"64\" stroke=\"#c8a840\" stroke-width=\".6\"/> <text x=\"139\" y=\"82\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"7.5\" fill=\"#1a3060\" font-weight=\"bold\">Fraternité</text> <line x1=\"108\" y1=\"88\" x2=\"170\" y2=\"88\" stroke=\"#c8a840\" stroke-width=\".6\"/> <circle cx=\"139\" cy=\"108\" r=\"14\" fill=\"#002395\"/> <circle cx=\"139\" cy=\"108\" r=\"9.5\" fill=\"white\"/> <circle cx=\"139\" cy=\"108\" r=\"5\" fill=\"#ed2939\"/> </svg>"}, {"id": 7, "title": "Émancipation des Juifs", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <!-- Parchemin --> <rect x=\"18\" y=\"12\" width=\"150\" height=\"110\" rx=\"4\" fill=\"#f0e0b0\" stroke=\"#c8a840\" stroke-width=\"1.2\"/> <rect x=\"18\" y=\"12\" width=\"150\" height=\"14\" rx=\"3\" fill=\"#c0a040\" opacity=\".3\"/> <text x=\"93\" y=\"24\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"7.5\" fill=\"#1a3060\" font-weight=\"bold\">DÉCRET</text> <text x=\"93\" y=\"34\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.5\" fill=\"#1a3060\">d'émancipation</text> <line x1=\"28\" y1=\"40\" x2=\"158\" y2=\"40\" stroke=\"#c8a840\" stroke-width=\".8\"/> <!-- Étoile de David --> <polygon points=\"93,52 80,74 106,74\" fill=\"none\" stroke=\"#c8a840\" stroke-width=\"2\"/> <polygon points=\"93,78 80,56 106,56\" fill=\"none\" stroke=\"#c8a840\" stroke-width=\"2\"/> <!-- Texte --> <text x=\"93\" y=\"95\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.5\" fill=\"#3a2808\">Les Juifs de France</text> <text x=\"93\" y=\"106\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.5\" fill=\"#3a2808\">sont désormais</text> <text x=\"93\" y=\"117\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"7\" fill=\"#1a3060\" font-weight=\"bold\">citoyens français</text> <!-- Cocarde --> <circle cx=\"154\" cy=\"115\" r=\"9\" fill=\"#002395\"/> <circle cx=\"154\" cy=\"115\" r=\"6\" fill=\"white\"/> <circle cx=\"154\" cy=\"115\" r=\"3\" fill=\"#ed2939\"/> </svg>"}, {"id": 8, "title": "Constitution Civile du Clergé", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <!-- Église --> <rect x=\"32\" y=\"50\" width=\"122\" height=\"80\" fill=\"#d8c898\"/> <polygon points=\"22,50 93,12 164,50\" fill=\"#c0aa78\"/> <rect x=\"78\" y=\"2\" width=\"30\" height=\"24\" fill=\"#b09868\"/> <line x1=\"93\" y1=\"0\" x2=\"93\" y2=\"12\" stroke=\"white\" stroke-width=\"2.2\"/> <line x1=\"87\" y1=\"5\" x2=\"99\" y2=\"5\" stroke=\"white\" stroke-width=\"2.2\"/> <path d=\"M52,64 L52,90 Q62,102 72,90 L72,64 Z\" fill=\"#4a70a0\" opacity=\".75\"/> <path d=\"M114,64 L114,90 Q124,102 134,90 L134,64 Z\" fill=\"#4a70a0\" opacity=\".75\"/> <path d=\"M74,130 L74,104 Q93,88 112,104 L112,130 Z\" fill=\"#5a3e28\"/> <!-- Chaîne républicaine --> <path d=\"M8,90 Q28,74 48,90 Q68,106 88,90 Q108,74 128,90 Q148,106 168,90 Q176,84 182,86\" stroke=\"#1a3060\" stroke-width=\"3\" stroke-linecap=\"round\" fill=\"none\"/> <ellipse cx=\"48\" cy=\"90\" rx=\"8\" ry=\"5\" stroke=\"#1a3060\" stroke-width=\"2\" fill=\"none\" transform=\"rotate(-20 48 90)\"/> <ellipse cx=\"93\" cy=\"90\" rx=\"8\" ry=\"5\" stroke=\"#1a3060\" stroke-width=\"2\" fill=\"none\" transform=\"rotate(-20 93 90)\"/> <ellipse cx=\"138\" cy=\"90\" rx=\"8\" ry=\"5\" stroke=\"#1a3060\" stroke-width=\"2\" fill=\"none\" transform=\"rotate(-20 138 90)\"/> </svg>"}, {"id": 9, "title": "Concordat de Napoléon", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <!-- Table --> <rect x=\"28\" y=\"86\" width=\"130\" height=\"10\" rx=\"2\" fill=\"#7a5a20\"/> <rect x=\"38\" y=\"94\" width=\"9\" height=\"22\" fill=\"#6a4a14\"/> <rect x=\"139\" y=\"94\" width=\"9\" height=\"22\" fill=\"#6a4a14\"/> <!-- Document --> <rect x=\"48\" y=\"46\" width=\"90\" height=\"56\" rx=\"3\" fill=\"#f0e0b0\" stroke=\"#c8a840\" stroke-width=\"1.1\"/> <rect x=\"48\" y=\"46\" width=\"90\" height=\"16\" rx=\"2\" fill=\"#c8a040\" opacity=\".22\"/> <text x=\"93\" y=\"58\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"8\" font-weight=\"bold\" fill=\"#3a2808\">CONCORDAT</text> <text x=\"93\" y=\"68\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.5\" fill=\"#5a3818\">1801</text> <line x1=\"56\" y1=\"74\" x2=\"130\" y2=\"74\" stroke=\"#b8a060\" stroke-width=\".6\"/> <line x1=\"56\" y1=\"82\" x2=\"130\" y2=\"82\" stroke=\"#b8a060\" stroke-width=\".6\"/> <circle cx=\"93\" cy=\"98\" r=\"8\" fill=\"#8c2020\"/> <circle cx=\"93\" cy=\"98\" r=\"5\" fill=\"#c8a840\" opacity=\".5\"/> <!-- Napoléon --> <circle cx=\"30\" cy=\"38\" r=\"11\" fill=\"#f0c890\"/> <polygon points=\"16,37 30,29 44,37 43,41 30,33 17,41\" fill=\"#1a1a2e\"/> <rect x=\"18\" y=\"49\" width=\"24\" height=\"26\" rx=\"2\" fill=\"#1a3060\"/> <!-- Pape --> <circle cx=\"156\" cy=\"38\" r=\"11\" fill=\"#f0c890\"/> <rect x=\"145\" y=\"47\" width=\"22\" height=\"6\" rx=\"1\" fill=\"#f8f4ec\" stroke=\"#c8a840\" stroke-width=\".7\"/> <ellipse cx=\"156\" cy=\"47\" rx=\"11\" ry=\"4\" fill=\"#f8f4ec\"/> <rect x=\"144\" y=\"49\" width=\"24\" height=\"26\" rx=\"2\" fill=\"#f0eee8\"/> <line x1=\"156\" y1=\"57\" x2=\"156\" y2=\"67\" stroke=\"#c8a840\" stroke-width=\"1.5\"/> <line x1=\"150\" y1=\"62\" x2=\"162\" y2=\"62\" stroke=\"#c8a840\" stroke-width=\"1.5\"/> </svg>"}, {"id": 10, "title": "Lois Jules Ferry", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <polygon points=\"6,68 93,20 180,68\" fill=\"#b4c4b0\"/> <rect x=\"6\" y=\"68\" width=\"174\" height=\"62\" fill=\"#ccc4a8\"/> <rect x=\"12\" y=\"68\" width=\"14\" height=\"62\" rx=\"2\" fill=\"#e0d8c0\"/> <rect x=\"38\" y=\"68\" width=\"14\" height=\"62\" rx=\"2\" fill=\"#e0d8c0\"/> <rect x=\"134\" y=\"68\" width=\"14\" height=\"62\" rx=\"2\" fill=\"#e0d8c0\"/> <rect x=\"160\" y=\"68\" width=\"14\" height=\"62\" rx=\"2\" fill=\"#e0d8c0\"/> <!-- Tableau --> <rect x=\"64\" y=\"76\" width=\"58\" height=\"36\" rx=\"2\" fill=\"#1e301e\"/> <text x=\"93\" y=\"91\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"10\" fill=\"#e8d8a0\">A B C</text> <text x=\"93\" y=\"104\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"7\" fill=\"#c8a840\" font-weight=\"bold\">LAÏCITÉ</text> <!-- Crucifix barré --> <line x1=\"154\" y1=\"80\" x2=\"154\" y2=\"100\" stroke=\"#a09070\" stroke-width=\"2\" stroke-dasharray=\"3,2\"/> <line x1=\"145\" y1=\"90\" x2=\"163\" y2=\"90\" stroke=\"#a09070\" stroke-width=\"2\" stroke-dasharray=\"3,2\"/> <line x1=\"143\" y1=\"78\" x2=\"165\" y2=\"102\" stroke=\"#8c2020\" stroke-width=\"2.5\"/> <!-- Porte --> <path d=\"M78,130 L78,108 Q93,96 108,108 L108,130 Z\" fill=\"#5a3e28\"/> <!-- Livres tricolores --> <rect x=\"14\" y=\"86\" width=\"7\" height=\"18\" rx=\"1\" fill=\"#8c2020\"/> <rect x=\"23\" y=\"86\" width=\"7\" height=\"18\" rx=\"1\" fill=\"#1a3060\"/> <rect x=\"32\" y=\"86\" width=\"7\" height=\"18\" rx=\"1\" fill=\"#2a5838\"/> </svg>"}, {"id": 11, "title": "Loi de Séparation Églises–État", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <line x1=\"93\" y1=\"6\" x2=\"93\" y2=\"126\" stroke=\"#8c2020\" stroke-width=\"1.5\" stroke-dasharray=\"7,4\"/> <!-- ÉGLISE --> <rect x=\"4\" y=\"36\" width=\"80\" height=\"80\" fill=\"#d8c898\"/> <polygon points=\"2,36 44,8 86,36\" fill=\"#c0aa78\"/> <rect x=\"30\" y=\"4\" width=\"26\" height=\"22\" fill=\"#b09868\"/> <line x1=\"43\" y1=\"0\" x2=\"43\" y2=\"12\" stroke=\"white\" stroke-width=\"2\"/> <line x1=\"37\" y1=\"5\" x2=\"49\" y2=\"5\" stroke=\"white\" stroke-width=\"2\"/> <path d=\"M14,50 L14,76 Q22,86 30,76 L30,50 Z\" fill=\"#4a70a0\" opacity=\".75\"/> <path d=\"M26,116 L26,92 Q44,80 62,92 L62,116 Z\" fill=\"#5a3e28\"/> <!-- MAIRIE --> <rect x=\"102\" y=\"36\" width=\"80\" height=\"80\" fill=\"#dce8f2\"/> <polygon points=\"100,36 142,8 184,36\" fill=\"#b8cce0\"/> <rect x=\"116\" y=\"50\" width=\"16\" height=\"20\" rx=\"1\" fill=\"#6090b4\"/> <rect x=\"150\" y=\"50\" width=\"16\" height=\"20\" rx=\"1\" fill=\"#6090b4\"/> <text x=\"142\" y=\"104\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"18\" font-weight=\"bold\" fill=\"#002395\">RF</text> <line x1=\"142\" y1=\"6\" x2=\"142\" y2=\"22\" stroke=\"#888\" stroke-width=\"1\"/> <rect x=\"142\" y=\"6\" width=\"10\" height=\"16\" fill=\"#002395\"/> <rect x=\"152\" y=\"6\" width=\"9\" height=\"16\" fill=\"white\"/> <rect x=\"161\" y=\"6\" width=\"10\" height=\"16\" fill=\"#ed2939\"/> <rect x=\"126\" y=\"92\" width=\"32\" height=\"24\" rx=\"2\" fill=\"#5a3e28\"/> <!-- Ciseaux --> <line x1=\"93\" y1=\"126\" x2=\"75\" y2=\"100\" stroke=\"#c8a840\" stroke-width=\"4\" stroke-linecap=\"round\"/> <line x1=\"93\" y1=\"126\" x2=\"111\" y2=\"100\" stroke=\"#c8a840\" stroke-width=\"4\" stroke-linecap=\"round\"/> <circle cx=\"93\" cy=\"126\" r=\"6\" fill=\"#c8a840\"/> </svg>"}, {"id": 12, "title": "Exception : l'Alsace-Moselle", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <!-- Carte France --> <polygon points=\"44,20 36,32 32,48 24,60 22,74 28,88 24,102 34,114 48,122 64,124 80,120 94,112 106,100 114,86 118,72 114,58 120,42 114,28 102,20 88,14 72,12 56,14\" fill=\"#b4c8dc\" stroke=\"#8a9aae\" stroke-width=\"1.2\"/> <!-- Zone AL-MO --> <polygon points=\"114,28 112,40 114,56 116,70 120,82 124,94 118,106 110,100 114,86 118,72 114,58 120,42\" fill=\"#c8a840\"/> <line x1=\"112\" y1=\"28\" x2=\"122\" y2=\"106\" stroke=\"#1a1a1a\" stroke-width=\"1.2\" stroke-dasharray=\"4,3\"/> <text x=\"62\" y=\"74\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"9\" font-weight=\"bold\" fill=\"#1a3060\">FRANCE</text> <text x=\"116\" y=\"56\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.5\" font-weight=\"bold\" fill=\"#3a2808\">AL</text> <text x=\"116\" y=\"68\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.5\" font-weight=\"bold\" fill=\"#3a2808\">MO</text> <line x1=\"116\" y1=\"74\" x2=\"116\" y2=\"90\" stroke=\"#8c2020\" stroke-width=\"2.5\"/> <line x1=\"108\" y1=\"82\" x2=\"124\" y2=\"82\" stroke=\"#8c2020\" stroke-width=\"2.5\"/> <!-- Drapeau --> <line x1=\"152\" y1=\"14\" x2=\"152\" y2=\"36\" stroke=\"#888\" stroke-width=\"1\"/> <rect x=\"152\" y=\"14\" width=\"10\" height=\"22\" fill=\"#002395\"/> <rect x=\"162\" y=\"14\" width=\"10\" height=\"22\" fill=\"white\" stroke=\"#e8e0d0\" stroke-width=\".5\"/> <rect x=\"172\" y=\"14\" width=\"10\" height=\"22\" fill=\"#ed2939\"/> <rect x=\"12\" y=\"128\" width=\"162\" height=\"12\" rx=\"2\" fill=\"#1a1a2e\"/> <text x=\"93\" y=\"137\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6\" fill=\"#c8a840\">Droit concordataire maintenu — toujours en vigueur</text> </svg>"}, {"id": 13, "title": "Grande Mosquée de Paris", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <defs><linearGradient id=\"s13_c13\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\"><stop offset=\"0%\" stop-color=\"#7ab4d8\"/><stop offset=\"100%\" stop-color=\"#b8d8a0\"/></linearGradient></defs> <rect width=\"186\" height=\"144\" fill=\"url(#s13_c13)\"/> <rect x=\"0\" y=\"112\" width=\"186\" height=\"32\" fill=\"#c0a060\"/> <!-- Corps --> <rect x=\"22\" y=\"66\" width=\"112\" height=\"48\" fill=\"#ccb87c\"/> <!-- Dôme --> <path d=\"M22,66 Q22,14 78,14 Q134,14 134,66 Z\" fill=\"#8aaa70\"/> <rect x=\"73\" y=\"6\" width=\"10\" height=\"12\" fill=\"#8aaa70\"/> <ellipse cx=\"78\" cy=\"6\" rx=\"7\" ry=\"4\" fill=\"#6a8a58\"/> <path d=\"M78,-2 Q71,-8 73,-15 Q82,-17 80,-10 Q84,-14 82,-8 Q80,-2 78,-2Z\" fill=\"#c8a840\"/> <!-- Petits dômes --> <path d=\"M22,66 Q22,46 42,46 Q62,46 62,66 Z\" fill=\"#7a9868\"/> <path d=\"M94,66 Q94,46 114,46 Q134,46 134,66 Z\" fill=\"#7a9868\"/> <!-- Minaret --> <rect x=\"144\" y=\"28\" width=\"20\" height=\"86\" fill=\"#cabb8a\"/> <ellipse cx=\"154\" cy=\"28\" rx=\"12\" ry=\"7\" fill=\"#8aaa70\"/> <path d=\"M154,20 Q148,14 150,8 Q158,6 156,12 Q160,8 158,14 Q156,20 154,20Z\" fill=\"#c8a840\"/> <path d=\"M148,40 L148,58 Q154,66 160,58 L160,40 Z\" fill=\"#3a5878\" opacity=\".75\"/> <!-- Arches --> <path d=\"M24,112 L24,92 Q32,82 40,92 L40,112 Z\" fill=\"#3a5878\" opacity=\".8\"/> <path d=\"M44,112 L44,92 Q52,82 60,92 L60,112 Z\" fill=\"#3a5878\" opacity=\".8\"/> <path d=\"M64,112 L64,92 Q72,82 80,92 L80,112 Z\" fill=\"#3a5878\" opacity=\".8\"/> <path d=\"M84,112 L84,92 Q92,82 100,92 L100,112 Z\" fill=\"#3a5878\" opacity=\".8\"/> <path d=\"M104,112 L104,92 Q112,82 120,92 L120,112 Z\" fill=\"#3a5878\" opacity=\".8\"/> <!-- Cocarde --> <circle cx=\"16\" cy=\"32\" r=\"12\" fill=\"#002395\"/> <circle cx=\"16\" cy=\"32\" r=\"8\" fill=\"white\"/> <circle cx=\"16\" cy=\"32\" r=\"4\" fill=\"#ed2939\"/> </svg>"}, {"id": 14, "title": "Laïcité dans la Constitution", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <!-- Tablette gauche --> <rect x=\"6\" y=\"10\" width=\"80\" height=\"106\" rx=\"4\" fill=\"#b8a878\" stroke=\"#8b7340\" stroke-width=\"1.3\"/> <ellipse cx=\"46\" cy=\"10\" rx=\"40\" ry=\"10\" fill=\"#b8a878\" stroke=\"#8b7340\" stroke-width=\"1.3\"/> <text x=\"46\" y=\"6\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"5.5\" fill=\"#c8a840\" font-weight=\"bold\">IVe RÉP.</text> <text x=\"46\" y=\"24\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"8.5\" fill=\"#c8a840\" font-weight=\"bold\">1946</text> <line x1=\"14\" y1=\"32\" x2=\"78\" y2=\"32\" stroke=\"#c8a840\" stroke-width=\".8\"/> <text x=\"46\" y=\"50\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"10\" font-weight=\"bold\" fill=\"#f4f0e8\">LAÏQUE</text> <text x=\"46\" y=\"66\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6\" fill=\"#d8c8a0\">Indivisible</text> <text x=\"46\" y=\"78\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6\" fill=\"#d8c8a0\">Démocratique</text> <text x=\"46\" y=\"90\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6\" fill=\"#d8c8a0\">Sociale</text> <text x=\"46\" y=\"104\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"5.5\" fill=\"#bca870\" font-style=\"italic\">Art. 1er</text> <!-- Tablette droite --> <rect x=\"100\" y=\"10\" width=\"80\" height=\"106\" rx=\"4\" fill=\"#b8a878\" stroke=\"#8b7340\" stroke-width=\"1.3\"/> <ellipse cx=\"140\" cy=\"10\" rx=\"40\" ry=\"10\" fill=\"#b8a878\" stroke=\"#8b7340\" stroke-width=\"1.3\"/> <text x=\"140\" y=\"6\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"5.5\" fill=\"#c8a840\" font-weight=\"bold\">Ve RÉP.</text> <text x=\"140\" y=\"24\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"8.5\" fill=\"#c8a840\" font-weight=\"bold\">1958</text> <line x1=\"108\" y1=\"32\" x2=\"172\" y2=\"32\" stroke=\"#c8a840\" stroke-width=\".8\"/> <text x=\"140\" y=\"50\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"10\" font-weight=\"bold\" fill=\"#f4f0e8\">LAÏQUE</text> <text x=\"140\" y=\"66\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6\" fill=\"#d8c8a0\">Indivisible</text> <text x=\"140\" y=\"78\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6\" fill=\"#d8c8a0\">Démocratique</text> <text x=\"140\" y=\"90\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6\" fill=\"#d8c8a0\">Sociale</text> <text x=\"140\" y=\"104\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"5.5\" fill=\"#bca870\" font-style=\"italic\">Art. 1er</text> <circle cx=\"93\" cy=\"130\" r=\"10\" fill=\"#002395\"/> <circle cx=\"93\" cy=\"130\" r=\"6.5\" fill=\"white\"/> <circle cx=\"93\" cy=\"130\" r=\"3.5\" fill=\"#ed2939\"/> </svg>"}, {"id": 15, "title": "Affaire du Foulard de Creil", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <!-- Collège --> <rect x=\"4\" y=\"36\" width=\"178\" height=\"78\" fill=\"#c4d4e8\"/> <polygon points=\"2,36 93,6 184,36\" fill=\"#7a9eba\"/> <rect x=\"12\" y=\"50\" width=\"20\" height=\"24\" rx=\"1\" fill=\"#5090b4\"/> <line x1=\"22\" y1=\"50\" x2=\"22\" y2=\"74\" stroke=\"white\" stroke-width=\".9\"/> <rect x=\"46\" y=\"50\" width=\"20\" height=\"24\" rx=\"1\" fill=\"#5090b4\"/> <rect x=\"120\" y=\"50\" width=\"20\" height=\"24\" rx=\"1\" fill=\"#5090b4\"/> <rect x=\"154\" y=\"50\" width=\"20\" height=\"24\" rx=\"1\" fill=\"#5090b4\"/> <!-- 3 élèves voilées --> <ellipse cx=\"52\" cy=\"102\" rx=\"9\" ry=\"12\" fill=\"#2a5438\"/> <circle cx=\"52\" cy=\"88\" r=\"10\" fill=\"#f0c890\"/> <path d=\"M38,82 Q52,98 66,82 Q64,88 52,96 Q40,88 38,82Z\" fill=\"#2a5438\"/> <ellipse cx=\"93\" cy=\"102\" rx=\"9\" ry=\"12\" fill=\"#2a5438\"/> <circle cx=\"93\" cy=\"88\" r=\"10\" fill=\"#f0c890\"/> <path d=\"M79,82 Q93,98 107,82 Q105,88 93,96 Q81,88 79,82Z\" fill=\"#2a5438\"/> <ellipse cx=\"134\" cy=\"102\" rx=\"9\" ry=\"12\" fill=\"#2a5438\"/> <circle cx=\"134\" cy=\"88\" r=\"10\" fill=\"#f0c890\"/> <path d=\"M120,82 Q134,98 148,82 Q146,88 134,96 Q122,88 120,82Z\" fill=\"#2a5438\"/> <!-- Point d'interrogation --> <text x=\"166\" y=\"32\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"28\" font-weight=\"bold\" fill=\"#c8a840\">?</text> </svg>"}, {"id": 16, "title": "Interdiction des Signes Religieux", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <rect x=\"6\" y=\"4\" width=\"174\" height=\"104\" rx=\"3\" fill=\"#f0e4c8\" stroke=\"#c8a840\" stroke-width=\"1.1\"/> <rect x=\"6\" y=\"4\" width=\"174\" height=\"20\" rx=\"3\" fill=\"#162444\"/> <rect x=\"6\" y=\"16\" width=\"174\" height=\"8\" fill=\"#162444\"/> <text x=\"93\" y=\"18\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"8\" fill=\"#d4ae52\" font-weight=\"bold\">LOI DU 15 MARS 2004</text> <line x1=\"14\" y1=\"28\" x2=\"172\" y2=\"28\" stroke=\"#c8a840\" stroke-width=\".8\"/> <!-- Voile barré --> <circle cx=\"40\" cy=\"54\" r=\"12\" fill=\"#f0c890\"/> <path d=\"M24,47 Q40,64 56,47 Q54,53 40,62 Q26,53 24,47Z\" fill=\"#2a5438\"/> <line x1=\"18\" y1=\"36\" x2=\"62\" y2=\"80\" stroke=\"#c82020\" stroke-width=\"4\" stroke-linecap=\"round\"/> <!-- Kippa barrée --> <circle cx=\"93\" cy=\"58\" r=\"12\" fill=\"#f0c890\"/> <path d=\"M75,60 Q75,42 93,42 Q111,42 111,60\" fill=\"#1a3060\"/> <line x1=\"71\" y1=\"40\" x2=\"115\" y2=\"80\" stroke=\"#c82020\" stroke-width=\"4\" stroke-linecap=\"round\"/> <!-- Croix barrée --> <line x1=\"146\" y1=\"36\" x2=\"146\" y2=\"78\" stroke=\"#c8a840\" stroke-width=\"5\" stroke-linecap=\"round\"/> <line x1=\"128\" y1=\"51\" x2=\"164\" y2=\"51\" stroke=\"#c8a840\" stroke-width=\"5\" stroke-linecap=\"round\"/> <line x1=\"124\" y1=\"32\" x2=\"168\" y2=\"82\" stroke=\"#c82020\" stroke-width=\"4\" stroke-linecap=\"round\"/> <!-- Bas --> <line x1=\"14\" y1=\"90\" x2=\"172\" y2=\"90\" stroke=\"#c8a840\" stroke-width=\".8\"/> <text x=\"93\" y=\"102\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"7\" fill=\"#1a3060\" font-weight=\"bold\">ÉCOLE PUBLIQUE</text> <text x=\"93\" y=\"118\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6\" fill=\"#888\" font-style=\"italic\">Signes ostensibles interdits</text> <text x=\"93\" y=\"130\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6\" fill=\"#888\" font-style=\"italic\">dans les établissements scolaires</text> </svg>"}, {"id": 17, "title": "Interdiction du Voile Intégral", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <!-- Silhouette niqab --> <rect x=\"60\" y=\"16\" width=\"66\" height=\"110\" rx=\"10\" fill=\"#181818\"/> <rect x=\"68\" y=\"50\" width=\"18\" height=\"10\" rx=\"5\" fill=\"#f0c890\"/> <rect x=\"100\" y=\"50\" width=\"18\" height=\"10\" rx=\"5\" fill=\"#f0c890\"/> <!-- Panneau interdit --> <circle cx=\"93\" cy=\"70\" r=\"55\" fill=\"none\" stroke=\"#c82020\" stroke-width=\"10\"/> <line x1=\"54\" y1=\"31\" x2=\"132\" y2=\"109\" stroke=\"#c82020\" stroke-width=\"10\" stroke-linecap=\"round\"/> </svg>"}, {"id": 18, "title": "Charte de la Laïcité à l'École", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <!-- Affiche / charte --> <rect x=\"22\" y=\"10\" width=\"142\" height=\"122\" rx=\"3\" fill=\"#162444\"/> <rect x=\"22\" y=\"10\" width=\"142\" height=\"24\" rx=\"3\" fill=\"#002395\"/> <text x=\"93\" y=\"22\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"7.5\" fill=\"white\" font-weight=\"bold\">CHARTE DE LA LAÏCITÉ</text> <text x=\"93\" y=\"32\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6\" fill=\"#c8a840\">à l'École de la République</text> <!-- Cocarde tricolore centrale --> <circle cx=\"93\" cy=\"68\" r=\"26\" fill=\"#002395\"/> <circle cx=\"93\" cy=\"68\" r=\"18\" fill=\"white\"/> <circle cx=\"93\" cy=\"68\" r=\"10\" fill=\"#ed2939\"/> <!-- Articles (lignes blanches) --> <line x1=\"34\" y1=\"104\" x2=\"152\" y2=\"104\" stroke=\"white\" stroke-width=\".6\" opacity=\".4\"/> <line x1=\"34\" y1=\"112\" x2=\"152\" y2=\"112\" stroke=\"white\" stroke-width=\".6\" opacity=\".4\"/> <line x1=\"34\" y1=\"120\" x2=\"140\" y2=\"120\" stroke=\"white\" stroke-width=\".6\" opacity=\".4\"/> <text x=\"93\" y=\"100\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.5\" fill=\"#c8a840\">15 articles · affichée dans</text> <text x=\"93\" y=\"108\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.5\" fill=\"#c8a840\">chaque établissement</text> <text x=\"93\" y=\"116\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.5\" fill=\"#c8a840\">scolaire de France</text> </svg>"}, {"id": 19, "title": "Attentat contre Charlie Hebdo", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#1a1410\"/> <!-- Crayons (liberté d'expression) --> <rect x=\"56\" y=\"20\" width=\"12\" height=\"90\" rx=\"3\" fill=\"#f4d040\" transform=\"rotate(-15 62 65)\"/> <polygon points=\"52,112 64,112 58,126\" fill=\"#f0c890\" transform=\"rotate(-15 58 119)\"/> <rect x=\"87\" y=\"14\" width=\"12\" height=\"90\" rx=\"3\" fill=\"#f4d040\"/> <polygon points=\"83,106 95,106 89,120\" fill=\"#f0c890\"/> <rect x=\"118\" y=\"20\" width=\"12\" height=\"90\" rx=\"3\" fill=\"#f4d040\" transform=\"rotate(15 124 65)\"/> <polygon points=\"114,112 126,112 120,126\" fill=\"#f0c890\" transform=\"rotate(15 120 119)\"/> <!-- Je suis Charlie --> <rect x=\"18\" y=\"118\" width=\"150\" height=\"22\" rx=\"2\" fill=\"#111\"/> <text x=\"93\" y=\"129\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"9\" fill=\"white\" font-weight=\"bold\">Je suis Charlie</text> <!-- Petite flamme --> <path d=\"M93,8 Q88,4 90,0 Q94,-2 93,3 Q96,0 95,4 Q94,8 93,8Z\" fill=\"#f4a012\"/> </svg>"}, {"id": 20, "title": "Neutralité dans la Fonction Publique", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <!-- Bâtiment administratif --> <polygon points=\"4,56 93,14 182,56\" fill=\"#c0c8d0\"/> <rect x=\"4\" y=\"56\" width=\"178\" height=\"74\" fill=\"#d4dce4\"/> <rect x=\"4\" y=\"54\" width=\"178\" height=\"6\" fill=\"#b0bcc8\"/> <!-- Colonnes --> <rect x=\"12\" y=\"60\" width=\"14\" height=\"70\" rx=\"2\" fill=\"#e4ecf4\"/> <rect x=\"34\" y=\"60\" width=\"14\" height=\"70\" rx=\"2\" fill=\"#e4ecf4\"/> <rect x=\"56\" y=\"60\" width=\"14\" height=\"70\" rx=\"2\" fill=\"#e4ecf4\"/> <rect x=\"108\" y=\"60\" width=\"14\" height=\"70\" rx=\"2\" fill=\"#e4ecf4\"/> <rect x=\"138\" y=\"60\" width=\"14\" height=\"70\" rx=\"2\" fill=\"#e4ecf4\"/> <rect x=\"160\" y=\"60\" width=\"14\" height=\"70\" rx=\"2\" fill=\"#e4ecf4\"/> <!-- Bouclier avec œil barré (neutralité) --> <polygon points=\"70,120 116,120 116,86 93,68 70,86\" fill=\"#162444\"/> <!-- Silhouette agent (neutre, sans signe) --> <circle cx=\"93\" cy=\"84\" r=\"9\" fill=\"#f0c890\"/> <rect x=\"82\" y=\"93\" width=\"22\" height=\"18\" rx=\"3\" fill=\"#ccc\"/> <!-- Aucun signe religieux --> <line x1=\"70\" y1=\"68\" x2=\"116\" y2=\"120\" stroke=\"#c82020\" stroke-width=\"1.5\" opacity=\".6\"/> <!-- Drapeau --> <line x1=\"93\" y1=\"8\" x2=\"93\" y2=\"22\" stroke=\"#999\" stroke-width=\"1.2\"/> <rect x=\"93\" y=\"8\" width=\"11\" height=\"15\" fill=\"#002395\"/> <rect x=\"104\" y=\"8\" width=\"10\" height=\"15\" fill=\"white\" stroke=\"#e0e0e0\" stroke-width=\".4\"/> <rect x=\"114\" y=\"8\" width=\"11\" height=\"15\" fill=\"#ed2939\"/> <!-- Label --> <text x=\"93\" y=\"136\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"6.5\" fill=\"#444\" font-style=\"italic\">Neutralité religieuse obligatoire</text> </svg>"}, {"id": 21, "title": "Loi Principes Républicains", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <!-- Palais Bourbon --> <polygon points=\"4,52 93,10 182,52\" fill=\"#d0c4a8\"/> <rect x=\"4\" y=\"52\" width=\"178\" height=\"76\" fill=\"#e0d4b8\"/> <rect x=\"4\" y=\"50\" width=\"178\" height=\"6\" fill=\"#c0b490\"/> <rect x=\"10\" y=\"56\" width=\"14\" height=\"72\" rx=\"2\" fill=\"#ece0c8\"/> <rect x=\"30\" y=\"56\" width=\"14\" height=\"72\" rx=\"2\" fill=\"#ece0c8\"/> <rect x=\"50\" y=\"56\" width=\"14\" height=\"72\" rx=\"2\" fill=\"#ece0c8\"/> <rect x=\"108\" y=\"56\" width=\"14\" height=\"72\" rx=\"2\" fill=\"#ece0c8\"/> <rect x=\"142\" y=\"56\" width=\"14\" height=\"72\" rx=\"2\" fill=\"#ece0c8\"/> <rect x=\"162\" y=\"56\" width=\"14\" height=\"72\" rx=\"2\" fill=\"#ece0c8\"/> <!-- Bouclier RF --> <polygon points=\"68,118 118,118 118,80 93,60 68,80\" fill=\"#002395\"/> <text x=\"93\" y=\"98\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"14\" font-weight=\"bold\" fill=\"white\">RF</text> <text x=\"93\" y=\"110\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"7\" font-weight=\"bold\" fill=\"#c8a840\">LAÏCITÉ</text> <!-- Drapeau --> <line x1=\"93\" y1=\"4\" x2=\"93\" y2=\"18\" stroke=\"#888\" stroke-width=\"1.2\"/> <rect x=\"93\" y=\"4\" width=\"12\" height=\"16\" fill=\"#002395\"/> <rect x=\"105\" y=\"4\" width=\"11\" height=\"16\" fill=\"white\" stroke=\"#e8e0d0\" stroke-width=\".5\"/> <rect x=\"116\" y=\"4\" width=\"12\" height=\"16\" fill=\"#ed2939\"/> <!-- Porte --> <path d=\"M77,128 L77,106 Q93,94 109,106 L109,128 Z\" fill=\"#5a3e28\"/> <rect x=\"63\" y=\"126\" width=\"60\" height=\"4\" rx=\"1\" fill=\"#c8b890\"/> </svg>"}, {"id": 22, "title": "La Laïcité en Débat", "svg": "<svg viewBox=\"0 0 186 144\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\"> <rect width=\"186\" height=\"144\" fill=\"#faf8f4\"/> <!-- Balances de la Justice --> <!-- Mât central --> <line x1=\"93\" y1=\"16\" x2=\"93\" y2=\"100\" stroke=\"#c8a840\" stroke-width=\"3\" stroke-linecap=\"round\"/> <!-- Barre horizontale --> <line x1=\"40\" y1=\"42\" x2=\"146\" y2=\"42\" stroke=\"#c8a840\" stroke-width=\"2.5\" stroke-linecap=\"round\"/> <!-- Plateau gauche (Religion) --> <line x1=\"40\" y1=\"42\" x2=\"40\" y2=\"70\" stroke=\"#c8a840\" stroke-width=\"1.5\"/> <line x1=\"40\" y1=\"42\" x2=\"30\" y2=\"70\" stroke=\"#c8a840\" stroke-width=\"1.5\"/> <line x1=\"40\" y1=\"42\" x2=\"50\" y2=\"70\" stroke=\"#c8a840\" stroke-width=\"1.5\"/> <path d=\"M26,70 Q40,66 54,70\" stroke=\"#c8a840\" stroke-width=\"2\" fill=\"#f0e8d0\" stroke-linecap=\"round\"/> <!-- Croix sur plateau gauche --> <line x1=\"38\" y1=\"74\" x2=\"38\" y2=\"84\" stroke=\"#8c2020\" stroke-width=\"2\"/> <line x1=\"34\" y1=\"78\" x2=\"42\" y2=\"78\" stroke=\"#8c2020\" stroke-width=\"2\"/> <!-- Plateau droit (Liberté) --> <line x1=\"146\" y1=\"42\" x2=\"146\" y2=\"56\" stroke=\"#c8a840\" stroke-width=\"1.5\"/> <line x1=\"146\" y1=\"42\" x2=\"136\" y2=\"56\" stroke=\"#c8a840\" stroke-width=\"1.5\"/> <line x1=\"146\" y1=\"42\" x2=\"156\" y2=\"56\" stroke=\"#c8a840\" stroke-width=\"1.5\"/> <path d=\"M132,56 Q146,52 160,56\" stroke=\"#c8a840\" stroke-width=\"2\" fill=\"#f0e8d0\" stroke-linecap=\"round\"/> <!-- Bonnet phrygien sur plateau droit --> <path d=\"M146,64 Q140,58 142,54 Q146,52 150,54 Q152,58 146,64Z\" fill=\"#ed2939\"/> <line x1=\"140\" y1=\"64\" x2=\"152\" y2=\"64\" stroke=\"#c8a840\" stroke-width=\"1.5\"/> <!-- Socle --> <rect x=\"82\" y=\"100\" width=\"22\" height=\"8\" rx=\"2\" fill=\"#c8a840\"/> <rect x=\"74\" y=\"106\" width=\"38\" height=\"6\" rx=\"1\" fill=\"#b09040\"/> <!-- Questions flottantes --> <text x=\"18\" y=\"106\" font-family=\"serif\" font-size=\"7\" fill=\"#888\" font-style=\"italic\">Religion</text> <text x=\"138\" y=\"48\" font-family=\"serif\" font-size=\"7\" fill=\"#888\" font-style=\"italic\">Liberté</text> <!-- Trois points d'interrogation --> <text x=\"93\" y=\"130\" text-anchor=\"middle\" font-family=\"serif\" font-size=\"20\" fill=\"#c8a840\">· · ·</text> </svg>"}];

// ════════ CARTES GAME ════════
let slotContents = new Array(22).fill(null); // slot index -> card id or null
let cardSlots = {}; // card id -> slot index or null (null = pool)
let draggedId = null;

function buildCards(){
  const pool = document.getElementById('cards-pool');
  const slotsRow = document.getElementById('slots-row');
  pool.innerHTML = ''; slotsRow.innerHTML = '';

  // Build slots
  for(let i=0;i<22;i++){
    const slot = document.createElement('div');
    slot.className = 'slot';
    slot.dataset.slot = i;
    const num = document.createElement('span');
    num.className = 'slot-num';
    num.textContent = i+1;
    slot.appendChild(num);
    slot.addEventListener('dragover', e=>{e.preventDefault();slot.classList.add('drag-over')});
    slot.addEventListener('dragleave', ()=>slot.classList.remove('drag-over'));
    slot.addEventListener('drop', e=>{e.preventDefault();slot.classList.remove('drag-over');dropToSlot(parseInt(slot.dataset.slot))});
    slot.addEventListener('click', ()=>{if(draggedId!==null)dropToSlot(i)});
    slotsRow.appendChild(slot);
  }

  // Build shuffled cards in pool
  const shuffled = [...CARDS_DATA].sort(()=>Math.random()-.5);
  shuffled.forEach(card=>{
    const el = makeCardEl(card);
    pool.appendChild(el);
    cardSlots[card.id] = null;
  });
}

function makeCardEl(card){
  const div = document.createElement('div');
  div.className = 'mini-card';
  div.dataset.id = card.id;
  div.draggable = true;
  div.innerHTML = `<div class="mini-illus">${card.svg}</div><div class="mini-title">${card.title}</div>`;

  // Desktop drag
  div.addEventListener('dragstart', e=>{
    draggedId = card.id;
    div.classList.add('dragging');
    e.dataTransfer.effectAllowed='move';
  });
  div.addEventListener('dragend', ()=>{draggedId=null;div.classList.remove('dragging')});

  // Mobile touch
  let touchStartX, touchStartY, touchClone, touchMoved=false;
  div.addEventListener('touchstart', e=>{
    draggedId = card.id;
    const t = e.touches[0];
    touchStartX = t.clientX; touchStartY = t.clientY;
    touchMoved = false;
    touchClone = div.cloneNode(true);
    touchClone.style.cssText = `position:fixed;opacity:.7;pointer-events:none;width:78px;z-index:9999;left:${t.clientX-39}px;top:${t.clientY-60}px;`;
    document.body.appendChild(touchClone);
    e.preventDefault();
  },{passive:false});
  div.addEventListener('touchmove', e=>{
    touchMoved=true;
    const t = e.touches[0];
    if(touchClone){touchClone.style.left=(t.clientX-39)+'px';touchClone.style.top=(t.clientY-60)+'px';}
    e.preventDefault();
  },{passive:false});
  div.addEventListener('touchend', e=>{
    if(touchClone){touchClone.remove();touchClone=null;}
    const t = e.changedTouches[0];
    const target = document.elementFromPoint(t.clientX, t.clientY);
    const slotEl = target && (target.classList.contains('slot') ? target : target.closest('.slot'));
    if(slotEl && draggedId!==null) dropToSlot(parseInt(slotEl.dataset.slot));
    else if(!touchMoved){/* tap: highlight */}
    draggedId = null;
    e.preventDefault();
  },{passive:false});

  // Pool drop
  div.addEventListener('dragover', e=>e.preventDefault());
  div.addEventListener('drop', e=>{e.preventDefault();if(draggedId!==null&&draggedId!==card.id)dropToPool(draggedId)});

  return div;
}

function dropToSlot(slotIdx){
  if(draggedId===null)return;
  const cardId = draggedId;

  // If slot already has a card, move it to pool
  if(slotContents[slotIdx]!==null){
    const displaced = slotContents[slotIdx];
    cardSlots[displaced] = null;
    const displacedEl = document.querySelector(`.mini-card[data-id="${displaced}"]`);
    if(displacedEl) document.getElementById('cards-pool').appendChild(displacedEl);
    slotContents[slotIdx] = null;
  }

  // Remove card from its current slot if any
  const prevSlot = cardSlots[cardId];
  if(prevSlot!==null && prevSlot!==undefined) slotContents[prevSlot] = null;

  // Place card in slot
  slotContents[slotIdx] = cardId;
  cardSlots[cardId] = slotIdx;

  const cardEl = document.querySelector(`.mini-card[data-id="${cardId}"]`);
  const slotEl = document.querySelector(`.slot[data-slot="${slotIdx}"]`);
  if(cardEl && slotEl){
    cardEl.classList.remove('correct-pos','wrong-pos');
    slotEl.appendChild(cardEl);
  }
  document.getElementById('cartes-result').textContent='';
  document.getElementById('cartes-result').className='cartes-result';
}

function dropToPool(cardId){
  if(cardId===null||cardId===undefined)return;
  const prevSlot = cardSlots[cardId];
  if(prevSlot!==null&&prevSlot!==undefined) slotContents[prevSlot]=null;
  cardSlots[cardId]=null;
  const cardEl = document.querySelector(`.mini-card[data-id="${cardId}"]`);
  if(cardEl){cardEl.classList.remove('correct-pos','wrong-pos');document.getElementById('cards-pool').appendChild(cardEl);}
}

function checkOrder(){
  let correct=0, placed=0;
  for(let i=0;i<22;i++){
    const cardId = slotContents[i];
    if(cardId===null)continue;
    placed++;
    const cardEl = document.querySelector(`.mini-card[data-id="${cardId}"]`);
    cardEl.classList.remove('correct-pos','wrong-pos');
    if(cardId === i+1){correct++;cardEl.classList.add('correct-pos');}
    else{cardEl.classList.add('wrong-pos');}
  }
  const res = document.getElementById('cartes-result');
  if(correct===22){res.textContent='🎉 Parfait ! Toutes les cartes sont dans le bon ordre !';res.className='cartes-result ok';}
  else{res.textContent=`${correct} carte${correct>1?'s':''} bien placée${correct>1?'s':''} sur ${placed} posée${placed>1?'s':''}.`;res.className='cartes-result bad';}
}

function revealOrder(){
  // Place all cards in correct slots
  for(let i=0;i<22;i++){
    const cardId = i+1;
    // Remove from current slot
    const prevSlot = cardSlots[cardId];
    if(prevSlot!==null&&prevSlot!==undefined) slotContents[prevSlot]=null;
    // Place in correct slot (may be occupied)
    slotContents[i]=cardId;
    cardSlots[cardId]=i;
    const cardEl = document.querySelector(`.mini-card[data-id="${cardId}"]`);
    const slotEl = document.querySelector(`.slot[data-slot="${i}"]`);
    if(cardEl&&slotEl){cardEl.classList.remove('wrong-pos');cardEl.classList.add('correct-pos');slotEl.appendChild(cardEl);}
  }
  const res = document.getElementById('cartes-result');
  res.textContent='Solution affichée — voici l'ordre chronologique correct.';
  res.className='cartes-result';
}

function shuffleCards(){
  slotContents = new Array(22).fill(null);
  cardSlots = {};
  buildCards();
  document.getElementById('cartes-result').textContent='';
  document.getElementById('cartes-result').className='cartes-result';
}

// Init
buildCards();

// ════════ MOTS CROISÉS ════════
const CW_ROWS=15, CW_COLS=17;
const CW_WORDS=[
  {n:1, w:"LAICITE",   d:"H",r:0, c:3, label:"LAÏCITÉ",   def:"Principe de séparation des religions et de l'État"},
  {n:2, w:"CONCORDAT", d:"V",r:0, c:6, label:"CONCORDAT", def:"Accord de 1801 entre Napoléon et le pape Pie VII"},
  {n:3, w:"TOLERANCE", d:"H",r:1, c:5, label:"TOLÉRANCE", def:"Vertu de respecter les convictions religieuses d'autrui"},
  {n:4, w:"SECULIER",  d:"H",r:3, c:4, label:"SÉCULIER",  def:"Qui n'appartient pas au domaine religieux ; du siècle"},
  {n:5, w:"NEUTRE",    d:"H",r:5, c:2, label:"NEUTRE",    def:"Caractère de l'État vis-à-vis de toutes les religions"},
  {n:6, w:"EGLISE",    d:"V",r:5, c:3, label:"ÉGLISE",    def:"Institution religieuse séparée de l'État en 1905"},
  {n:7, w:"REPUBLIQUE",d:"H",r:6, c:7, label:"RÉPUBLIQUE",def:"Régime politique de la France depuis 1792"},
  {n:8, w:"NANTES",    d:"H",r:7, c:5, label:"NANTES",    def:"Ville qui donna son nom à l'édit de tolérance de 1598"},
  {n:9, w:"ETAT",      d:"H",r:8, c:5, label:"ÉTAT",      def:"Puissance publique séparée de toute religion depuis 1905"},
  {n:10,w:"FERRY",     d:"H",r:10,c:5, label:"FERRY",     def:"Ministre qui rendit l'école publique obligatoire et laïque"},
  {n:11,w:"CULTE",     d:"H",r:12,c:4, label:"CULTE",     def:"Pratique religieuse que l'État ne subventionne plus depuis 1905"},
  {n:12,w:"LOI",       d:"H",r:14,c:4, label:"LOI",       def:"Texte fondateur du 9 décembre 1905 sur la séparation"},
  {n:13,w:"CLOVIS",    d:"H",r:14,c:8, label:"CLOVIS",    def:"Roi des Francs baptisé vers 498 : naissance de l'alliance trône-autel"},
];

const cwCellMap={}, cwCellWords={}, cwCellNums={};
CW_WORDS.forEach((entry,wi)=>{
  const{w,r,c,d}=entry;
  const sk=`${r},${c}`;
  if(!cwCellNums[sk])cwCellNums[sk]=entry.n;
  for(let i=0;i<w.length;i++){
    const row=d==='H'?r:r+i, col=d==='H'?c+i:c, key=`${row},${col}`;
    cwCellMap[key]=w[i];
    if(!cwCellWords[key])cwCellWords[key]=[];
    cwCellWords[key].push({wi,li:i});
  }
});

const cwGrid=document.getElementById('cw-grid');
const cwInputs={};
for(let r=0;r<CW_ROWS;r++){
  for(let c=0;c<CW_COLS;c++){
    const key=`${r},${c}`;
    const div=document.createElement('div');
    div.className='cw-cell'+(cwCellMap[key]?' active':'');
    div.dataset.key=key;
    if(cwCellMap[key]){
      if(cwCellNums[key]){const n=document.createElement('span');n.className='cell-num';n.textContent=cwCellNums[key];div.appendChild(n);}
      const inp=document.createElement('input');
      inp.type='text';inp.maxLength=1;inp.autocomplete='off';inp.dataset.key=key;
      inp.addEventListener('input',cwOnInput);
      inp.addEventListener('focus',cwOnFocus);
      inp.addEventListener('keydown',cwOnKeydown);
      div.appendChild(inp);
      cwInputs[key]=inp;
    }
    cwGrid.appendChild(div);
  }
}

// Clues
const cluesH=document.getElementById('clues-h'),cluesV=document.getElementById('clues-v');
CW_WORDS.forEach((entry,wi)=>{
  const li=document.createElement('li');li.className='clue-item';li.dataset.wi=wi;
  li.innerHTML=`<span class="clue-num">${entry.n}.</span><span><strong>${entry.label}</strong> — ${entry.def}</span>`;
  li.addEventListener('click',()=>cwFocusWord(wi));
  (entry.d==='H'?cluesH:cluesV).appendChild(li);
});

let cwActiveWord=null;
function cwClearHighlight(){document.querySelectorAll('.cw-cell.highlight').forEach(e=>e.classList.remove('highlight'));document.querySelectorAll('.clue-item.active-clue').forEach(e=>e.classList.remove('active-clue'));}
function cwHighlightWord(wi){
  cwClearHighlight();cwActiveWord=wi;
  const{w,r,c,d}=CW_WORDS[wi];
  for(let i=0;i<w.length;i++){
    const row=d==='H'?r:r+i,col=d==='H'?c+i:c;
    const div=document.querySelector(`.cw-cell[data-key="${row},${col}"]`);
    if(div)div.classList.add('highlight');
  }
  document.querySelectorAll(`.clue-item[data-wi="${wi}"]`).forEach(e=>e.classList.add('active-clue'));
}
function cwFocusWord(wi){cwHighlightWord(wi);const{r,c}=CW_WORDS[wi];if(cwInputs[`${r},${c}`])cwInputs[`${r},${c}`].focus();}
function cwOnFocus(e){const words=cwCellWords[e.target.dataset.key];if(words&&words.length>0){if(cwActiveWord!==null&&words.find(x=>x.wi===cwActiveWord)){cwHighlightWord(cwActiveWord);return;}cwHighlightWord(words[0].wi);}}
function cwOnInput(e){const inp=e.target,val=inp.value.toUpperCase().replace(/[^A-Z]/g,'');inp.value=val?val[val.length-1]:'';inp.parentElement.classList.remove('correct','wrong','revealed');if(val)cwMoveNext(inp.dataset.key);document.getElementById('cw-score').textContent='';}
function cwOnKeydown(e){
  const key=e.target.dataset.key,[r,c]=key.split(',').map(Number);
  if(e.key==='Backspace'&&!e.target.value){cwMovePrev(key);e.preventDefault();}
  if(e.key==='ArrowRight'){cwMove(r,c+1);e.preventDefault();}
  if(e.key==='ArrowLeft'){cwMove(r,c-1);e.preventDefault();}
  if(e.key==='ArrowDown'){cwMove(r+1,c);e.preventDefault();}
  if(e.key==='ArrowUp'){cwMove(r-1,c);e.preventDefault();}
  if(e.key==='Tab'){e.preventDefault();const next=(cwActiveWord+(e.shiftKey?CW_WORDS.length-1:1))%CW_WORDS.length;cwFocusWord(next);}
}
function cwMove(r,c){const k=`${r},${c}`;if(cwInputs[k])cwInputs[k].focus();}
function cwMoveNext(key){if(cwActiveWord===null)return;const{w,r,c,d}=CW_WORDS[cwActiveWord];const letters=Array.from({length:w.length},(_,i)=>({row:d==='H'?r:r+i,col:d==='H'?c+i:c}));const cur=letters.findIndex(l=>`${l.row},${l.col}`===key);if(cur<letters.length-1)cwMove(letters[cur+1].row,letters[cur+1].col);}
function cwMovePrev(key){if(cwActiveWord===null)return;const{w,r,c,d}=CW_WORDS[cwActiveWord];const letters=Array.from({length:w.length},(_,i)=>({row:d==='H'?r:r+i,col:d==='H'?c+i:c}));const cur=letters.findIndex(l=>`${l.row},${l.col}`===key);if(cur>0)cwMove(letters[cur-1].row,letters[cur-1].col);}

function cwCheck(){
  let correct=0,filled=0;
  Object.entries(cwInputs).forEach(([key,inp])=>{if(!inp.value)return;filled++;const div=inp.parentElement;div.classList.remove('correct','wrong','revealed');if(inp.value===cwCellMap[key]){div.classList.add('correct');correct++;}else{div.classList.add('wrong');}});
  const sc=document.getElementById('cw-score');
  const total=Object.keys(cwCellMap).length;
  if(filled===total&&correct===total){sc.textContent='🎉 Félicitations ! Grille complète et correcte !';sc.className='score-bar good';}
  else{sc.textContent=`${correct} lettre${correct>1?'s':''} correcte${correct>1?'s':''} sur ${filled} saisie${filled>1?'s':''}.`;sc.className=correct===filled&&filled>0?'score-bar good':'score-bar bad';}
}
function cwReveal(){Object.entries(cwInputs).forEach(([key,inp])=>{inp.value=cwCellMap[key];const div=inp.parentElement;div.classList.remove('correct','wrong');div.classList.add('revealed');});document.getElementById('cw-score').textContent='Solution affichée.';document.getElementById('cw-score').className='score-bar';}
function cwReset(){Object.values(cwInputs).forEach(inp=>{inp.value='';inp.parentElement.classList.remove('correct','wrong','revealed');});cwClearHighlight();cwActiveWord=null;document.getElementById('cw-score').textContent='';document.getElementById('cw-score').className='score-bar';}
</script>
</body>
</html>
