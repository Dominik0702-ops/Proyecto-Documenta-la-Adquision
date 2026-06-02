<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gestión de Adquisiciones de Mercancías y Servicios</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=DM+Sans:wght@300;400;500;600&family=DM+Mono&display=swap" rel="stylesheet">
<style>
  :root {
    --navy: #0a1628;
    --navy2: #112240;
    --gold: #c9a84c;
    --gold2: #f0c96e;
    --cream: #f8f4ec;
    --slate: #8892a4;
    --white: #ffffff;
    --accent: #e8734a;
    --green: #2d6a4f;
    --green2: #40916c;
    --light: #f0f4ff;
  }
 
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
 
  html { scroll-behavior: smooth; }
 
  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--cream);
    color: var(--navy);
    overflow-x: hidden;
  }
 
  /* ── NAV ── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    background: rgba(10,22,40,0.97);
    backdrop-filter: blur(10px);
    padding: 0 2rem;
    display: flex; align-items: center; justify-content: space-between;
    height: 62px;
    border-bottom: 1px solid rgba(201,168,76,0.3);
  }
  .nav-logo {
    font-family: 'Playfair Display', serif;
    color: var(--gold);
    font-size: 1.1rem;
    font-weight: 700;
    letter-spacing: 0.05em;
  }
  .nav-links { display: flex; gap: 1.5rem; list-style: none; }
  .nav-links a {
    color: rgba(255,255,255,0.75);
    text-decoration: none;
    font-size: 0.78rem;
    font-weight: 500;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--gold2); }
 
  /* ── COVER ── */
  #portada {
    min-height: 100vh;
    background: var(--navy);
    display: grid;
    place-items: center;
    position: relative;
    overflow: hidden;
    padding-top: 62px;
  }
 
  /* Geometric background */
  #portada::before {
    content: '';
    position: absolute; inset: 0;
    background:
      radial-gradient(ellipse 80% 60% at 70% 40%, rgba(201,168,76,0.12) 0%, transparent 70%),
      radial-gradient(ellipse 50% 80% at 10% 80%, rgba(232,115,74,0.08) 0%, transparent 60%);
  }
 
  .cover-grid {
    position: absolute; inset: 0;
    background-image:
      linear-gradient(rgba(201,168,76,0.06) 1px, transparent 1px),
      linear-gradient(90deg, rgba(201,168,76,0.06) 1px, transparent 1px);
    background-size: 60px 60px;
  }
 
  .cover-content {
    position: relative; z-index: 2;
    text-align: center;
    padding: 2rem;
    max-width: 900px;
  }
 
  .cover-badge {
    display: inline-block;
    border: 1px solid rgba(201,168,76,0.5);
    color: var(--gold);
    font-size: 0.7rem;
    letter-spacing: 0.25em;
    text-transform: uppercase;
    padding: 0.4rem 1.2rem;
    border-radius: 2px;
    margin-bottom: 2rem;
    background: rgba(201,168,76,0.06);
  }
 
  .cover-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2.5rem, 6vw, 5rem);
    font-weight: 900;
    color: var(--white);
    line-height: 1.1;
    margin-bottom: 1rem;
  }
 
  .cover-title span {
    background: linear-gradient(135deg, var(--gold), var(--gold2), var(--accent));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }
 
  .cover-subtitle {
    font-size: 1.1rem;
    color: var(--slate);
    margin-bottom: 2.5rem;
    line-height: 1.7;
    max-width: 620px;
    margin-left: auto;
    margin-right: auto;
  }
 
  .cover-meta {
    display: flex;
    gap: 2rem;
    justify-content: center;
    flex-wrap: wrap;
  }
 
  .meta-item {
    text-align: center;
  }
  .meta-label {
    font-size: 0.68rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--slate);
    display: block;
    margin-bottom: 0.3rem;
  }
  .meta-value {
    font-family: 'Playfair Display', serif;
    font-size: 0.95rem;
    color: var(--gold);
    font-weight: 700;
  }
 
  .cover-divider {
    width: 80px; height: 3px;
    background: linear-gradient(90deg, var(--gold), var(--accent));
    margin: 2rem auto;
    border-radius: 2px;
  }
 
  /* Floating icons */
  .float-icon {
    position: absolute;
    font-size: 4rem;
    opacity: 0.04;
    user-select: none;
  }
  .fi1 { top: 15%; left: 5%; }
  .fi2 { top: 60%; left: 3%; font-size: 6rem; }
  .fi3 { top: 20%; right: 4%; font-size: 7rem; }
  .fi4 { bottom: 10%; right: 8%; }
  .fi5 { bottom: 25%; left: 15%; font-size: 3rem; }
 
  /* ── SECTION GENERIC ── */
  section {
    padding: 5rem 2rem;
    max-width: 1100px;
    margin: 0 auto;
  }
 
  .section-header {
    margin-bottom: 3rem;
  }
 
  .section-number {
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem;
    color: var(--gold);
    letter-spacing: 0.3em;
    text-transform: uppercase;
    display: block;
    margin-bottom: 0.5rem;
  }
 
  .section-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.8rem, 3vw, 2.8rem);
    font-weight: 700;
    color: var(--navy);
    line-height: 1.2;
    margin-bottom: 1rem;
  }
 
  .section-desc {
    color: #4a5568;
    font-size: 1rem;
    line-height: 1.7;
    max-width: 680px;
  }
 
  .divider-line {
    width: 60px; height: 4px;
    background: linear-gradient(90deg, var(--gold), var(--accent));
    border-radius: 2px;
    margin-bottom: 1.5rem;
  }
 
  /* Alternating section backgrounds */
  .bg-navy { background: var(--navy); }
  .bg-navy .section-title { color: var(--white); }
  .bg-navy .section-desc { color: rgba(255,255,255,0.65); }
  .bg-navy .section-number { color: var(--gold2); }
 
  .bg-light { background: var(--light); }
  .bg-cream { background: var(--cream); }
 
  /* Full-width wrapper */
  .full-section {
    padding: 5rem 2rem;
  }
  .full-section > .inner {
    max-width: 1100px;
    margin: 0 auto;
  }
 
  /* ── CARDS ── */
  .cards-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
  }
 
  .card {
    background: var(--white);
    border-radius: 12px;
    padding: 2rem;
    border: 1px solid rgba(0,0,0,0.07);
    box-shadow: 0 4px 24px rgba(10,22,40,0.07);
    transition: transform 0.3s, box-shadow 0.3s;
    position: relative;
    overflow: hidden;
  }
 
  .card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 4px;
    background: linear-gradient(90deg, var(--gold), var(--accent));
  }
 
  .card:hover {
    transform: translateY(-4px);
    box-shadow: 0 12px 40px rgba(10,22,40,0.12);
  }
 
  .card-icon {
    font-size: 2.2rem;
    margin-bottom: 1rem;
    display: block;
  }
 
  .card-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.15rem;
    font-weight: 700;
    color: var(--navy);
    margin-bottom: 0.5rem;
  }
 
  .card-company {
    font-size: 0.72rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--gold);
    font-weight: 600;
    margin-bottom: 0.8rem;
  }
 
  .card-body {
    color: #4a5568;
    font-size: 0.9rem;
    line-height: 1.65;
  }
 
  .indicator-value {
    font-family: 'Playfair Display', serif;
    font-size: 2rem;
    font-weight: 900;
    color: var(--navy);
    margin: 0.8rem 0 0.3rem;
  }
 
  .indicator-formula {
    background: var(--light);
    border-left: 3px solid var(--gold);
    padding: 0.5rem 0.75rem;
    font-family: 'DM Mono', monospace;
    font-size: 0.78rem;
    color: var(--navy2);
    border-radius: 0 4px 4px 0;
    margin-top: 0.8rem;
  }
 
  /* ── TABLE ── */
  .table-wrap {
    overflow-x: auto;
    border-radius: 12px;
    box-shadow: 0 4px 30px rgba(10,22,40,0.1);
  }
 
  table {
    width: 100%;
    border-collapse: collapse;
    background: var(--white);
    font-size: 0.88rem;
  }
 
  thead {
    background: var(--navy);
    color: var(--white);
  }
 
  thead th {
    padding: 1rem 1.2rem;
    text-align: left;
    font-weight: 600;
    letter-spacing: 0.05em;
    font-size: 0.8rem;
    text-transform: uppercase;
  }
 
  thead th:first-child { border-radius: 12px 0 0 0; }
  thead th:last-child { border-radius: 0 12px 0 0; }
 
  tbody tr { border-bottom: 1px solid rgba(0,0,0,0.05); }
  tbody tr:last-child { border-bottom: none; }
  tbody tr:hover { background: rgba(201,168,76,0.04); }
 
  tbody td { padding: 0.9rem 1.2rem; vertical-align: top; line-height: 1.55; }
 
  .td-num {
    font-family: 'DM Mono', monospace;
    font-weight: 700;
    color: var(--gold);
    white-space: nowrap;
  }
 
  .td-check { color: var(--green2); font-size: 1.1rem; }
  .td-bold { font-weight: 600; color: var(--navy); }
 
  tfoot td {
    background: var(--light);
    font-weight: 700;
    color: var(--navy);
    padding: 0.9rem 1.2rem;
    border-top: 2px solid var(--gold);
  }
 
  /* ── ORDEN DE COMPRA ── */
  .oc-wrap {
    background: var(--white);
    border-radius: 16px;
    overflow: hidden;
    box-shadow: 0 8px 40px rgba(10,22,40,0.12);
  }
 
  .oc-header {
    background: var(--navy);
    padding: 2rem 2.5rem;
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    flex-wrap: wrap;
    gap: 1.5rem;
  }
 
  .oc-company-name {
    font-family: 'Playfair Display', serif;
    font-size: 1.8rem;
    font-weight: 900;
    color: var(--gold);
  }
 
  .oc-doc-title {
    font-size: 0.7rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--slate);
    margin-top: 0.3rem;
  }
 
  .oc-badge {
    background: linear-gradient(135deg, var(--gold), var(--accent));
    color: white;
    padding: 0.5rem 1.5rem;
    border-radius: 6px;
    font-weight: 700;
    font-size: 1.2rem;
    letter-spacing: 0.05em;
    font-family: 'DM Mono', monospace;
  }
 
  .oc-body { padding: 2rem 2.5rem; }
 
  .oc-info-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 1.5rem;
    margin-bottom: 2rem;
  }
 
  .oc-field label {
    display: block;
    font-size: 0.68rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--slate);
    margin-bottom: 0.3rem;
    font-weight: 600;
  }
  .oc-field span {
    font-weight: 500;
    color: var(--navy);
    font-size: 0.95rem;
  }
 
  .oc-section-title {
    font-family: 'Playfair Display', serif;
    font-size: 1rem;
    font-weight: 700;
    color: var(--navy);
    margin: 1.5rem 0 1rem;
    padding-bottom: 0.5rem;
    border-bottom: 2px solid var(--gold);
  }
 
  .eval-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1.5rem;
    margin-bottom: 2rem;
  }
 
  .eval-card {
    background: var(--light);
    border-radius: 10px;
    padding: 1.5rem;
    border: 2px solid transparent;
  }
  .eval-card.winner {
    border-color: var(--green2);
    background: rgba(64,145,108,0.06);
  }
 
  .eval-card-title {
    font-weight: 700;
    color: var(--navy);
    margin-bottom: 1rem;
    font-size: 0.95rem;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }
 
  .winner-badge {
    background: var(--green2);
    color: white;
    font-size: 0.65rem;
    padding: 0.2rem 0.5rem;
    border-radius: 4px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }
 
  .eval-row {
    display: flex;
    justify-content: space-between;
    font-size: 0.85rem;
    padding: 0.3rem 0;
    border-bottom: 1px dashed rgba(0,0,0,0.08);
  }
  .eval-row:last-child { border-bottom: none; }
  .eval-key { color: #4a5568; }
  .eval-val { font-weight: 600; color: var(--navy); }
 
  /* ── CONTRATO ── */
  .contrato-wrap {
    background: var(--white);
    border-radius: 16px;
    padding: 3rem;
    box-shadow: 0 8px 40px rgba(10,22,40,0.1);
    position: relative;
  }
 
  .contrato-watermark {
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%) rotate(-30deg);
    font-family: 'Playfair Display', serif;
    font-size: 5rem;
    color: rgba(201,168,76,0.05);
    font-weight: 900;
    pointer-events: none;
    white-space: nowrap;
    letter-spacing: 0.3em;
  }
 
  .contrato-header {
    text-align: center;
    margin-bottom: 2.5rem;
    padding-bottom: 1.5rem;
    border-bottom: 2px solid var(--light);
  }
 
  .contrato-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.6rem;
    font-weight: 900;
    color: var(--navy);
    letter-spacing: 0.05em;
    text-transform: uppercase;
  }
 
  .contrato-num {
    font-family: 'DM Mono', monospace;
    color: var(--gold);
    font-size: 0.85rem;
    margin-top: 0.3rem;
  }
 
  .partes-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    margin-bottom: 2rem;
  }
 
  .parte-card {
    background: var(--light);
    border-radius: 10px;
    padding: 1.5rem;
    border-top: 4px solid var(--gold);
  }
 
  .parte-role {
    font-size: 0.7rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--gold);
    font-weight: 700;
    margin-bottom: 0.8rem;
  }
 
  .parte-name {
    font-family: 'Playfair Display', serif;
    font-size: 1.1rem;
    font-weight: 700;
    color: var(--navy);
    margin-bottom: 0.5rem;
  }
 
  .parte-data {
    font-size: 0.82rem;
    color: #4a5568;
    line-height: 1.7;
  }
 
  .clausulas {
    margin: 1.5rem 0;
  }
 
  .clausula {
    margin-bottom: 1.2rem;
    padding-left: 1.5rem;
    border-left: 3px solid var(--gold);
  }
 
  .clausula-title {
    font-weight: 700;
    color: var(--navy);
    font-size: 0.9rem;
    margin-bottom: 0.3rem;
  }
 
  .clausula-text {
    font-size: 0.85rem;
    color: #4a5568;
    line-height: 1.65;
  }
 
  .firmas-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 3rem;
    margin-top: 3rem;
    padding-top: 1.5rem;
    border-top: 1px dashed #ccc;
  }
 
  .firma-box {
    text-align: center;
  }
 
  .firma-line {
    height: 2px;
    background: var(--navy);
    margin-bottom: 0.5rem;
    margin-top: 3rem;
  }
 
  .firma-name {
    font-weight: 700;
    font-size: 0.9rem;
    color: var(--navy);
  }
 
  .firma-role {
    font-size: 0.75rem;
    color: var(--slate);
    margin-top: 0.2rem;
  }
 
  /* ── PROCESO STEPS ── */
  .steps-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 3rem;
  }
 
  .steps-group-title {
    font-family: 'Playfair Display', serif;
    font-size: 1.3rem;
    font-weight: 700;
    color: var(--navy);
    margin-bottom: 1.5rem;
    display: flex;
    align-items: center;
    gap: 0.8rem;
  }
 
  .step-item {
    display: flex;
    gap: 1rem;
    margin-bottom: 1.5rem;
    position: relative;
  }
 
  .step-number {
    flex-shrink: 0;
    width: 36px; height: 36px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--gold), var(--accent));
    color: white;
    font-weight: 700;
    font-size: 0.85rem;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'DM Mono', monospace;
    box-shadow: 0 4px 12px rgba(201,168,76,0.3);
  }
 
  .step-content {}
  .step-title { font-weight: 700; color: var(--navy); margin-bottom: 0.25rem; font-size: 0.95rem; }
  .step-desc { font-size: 0.85rem; color: #4a5568; line-height: 1.6; }
 
  /* ── CHECKLIST ── */
  .checklist {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1rem;
  }
 
  .check-item {
    background: var(--white);
    border-radius: 10px;
    padding: 1.2rem 1.5rem;
    display: flex;
    gap: 1rem;
    align-items: flex-start;
    border: 1px solid rgba(0,0,0,0.06);
    box-shadow: 0 2px 12px rgba(10,22,40,0.05);
    transition: box-shadow 0.2s;
  }
 
  .check-item:hover { box-shadow: 0 4px 20px rgba(10,22,40,0.1); }
 
  .check-icon {
    width: 28px; height: 28px;
    flex-shrink: 0;
    background: linear-gradient(135deg, var(--green), var(--green2));
    border-radius: 6px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.85rem;
  }
 
  .check-text {}
  .check-title { font-weight: 700; font-size: 0.88rem; color: var(--navy); margin-bottom: 0.3rem; }
  .check-desc { font-size: 0.8rem; color: #4a5568; line-height: 1.55; }
 
  /* ── CONCLUSIONES ── */
  .conclusiones-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 1.5rem;
  }
 
  .concl-card {
    background: rgba(255,255,255,0.06);
    border: 1px solid rgba(201,168,76,0.25);
    border-radius: 12px;
    padding: 2rem;
    text-align: center;
    transition: background 0.3s;
  }
  .concl-card:hover { background: rgba(201,168,76,0.06); }
 
  .concl-icon { font-size: 2.5rem; margin-bottom: 1rem; display: block; }
  .concl-title {
    font-family: 'Playfair Display', serif;
    color: var(--gold2);
    font-size: 1rem;
    font-weight: 700;
    margin-bottom: 0.8rem;
  }
  .concl-text {
    font-size: 0.85rem;
    color: rgba(255,255,255,0.65);
    line-height: 1.65;
  }
 
  /* ── FOOTER ── */
  footer {
    background: #050d1a;
    color: rgba(255,255,255,0.4);
    text-align: center;
    padding: 2rem;
    font-size: 0.8rem;
    letter-spacing: 0.05em;
  }
 
  footer span { color: var(--gold); }
 
  /* ── ALERT ── */
  .alert {
    background: rgba(201,168,76,0.08);
    border: 1px solid rgba(201,168,76,0.3);
    border-radius: 8px;
    padding: 1rem 1.5rem;
    font-size: 0.88rem;
    color: var(--navy);
    margin-bottom: 1.5rem;
    line-height: 1.6;
  }
 
  .alert strong { color: var(--gold); }
 
  /* ── EVALUACION COMPARATIVA ── */
  .comp-table-wrap { margin-top: 1.5rem; }
  .comp-header {
    background: linear-gradient(135deg, var(--navy), var(--navy2));
    color: white;
    padding: 1rem 1.5rem;
    border-radius: 10px 10px 0 0;
    font-family: 'Playfair Display', serif;
    font-weight: 700;
    font-size: 1rem;
  }
 
  .evaluacion-box {
    background: rgba(45,106,79,0.08);
    border: 1px solid var(--green2);
    border-radius: 0 0 10px 10px;
    padding: 1.5rem;
  }
 
  .eval-conclusion {
    font-weight: 600;
    color: var(--green);
    font-size: 1rem;
    margin-bottom: 0.5rem;
  }
 
  @media (max-width: 768px) {
    .eval-grid, .partes-grid, .steps-container, .firmas-grid { grid-template-columns: 1fr; }
    nav .nav-links { display: none; }
    .oc-header { flex-direction: column; }
    .contrato-wrap { padding: 1.5rem; }
  }
 
  /* PRINT / EXPORT hint */
  .export-hint {
    position: fixed;
    bottom: 1.5rem; right: 1.5rem;
    background: var(--gold);
    color: var(--navy);
    padding: 0.6rem 1.2rem;
    border-radius: 6px;
    font-size: 0.78rem;
    font-weight: 700;
    letter-spacing: 0.05em;
    cursor: pointer;
    box-shadow: 0 4px 20px rgba(201,168,76,0.4);
    z-index: 200;
    transition: transform 0.2s;
  }
  .export-hint:hover { transform: scale(1.05); }
 
  /* ── TEAM CHIPS ── */
  .team-chip {
    display: inline-block;
    background: rgba(201,168,76,0.12);
    border: 1px solid rgba(201,168,76,0.4);
    color: var(--gold2);
    font-size: 0.82rem;
    font-weight: 600;
    padding: 0.4rem 1rem;
    border-radius: 999px;
    letter-spacing: 0.04em;
    transition: background 0.2s, border-color 0.2s;
  }
  .team-chip:hover {
    background: rgba(201,168,76,0.22);
    border-color: var(--gold2);
  }
</style>
</head>
<body>
 
<!-- NAV -->
<nav>
  <div class="nav-logo">📦 Gestión de Compras</div>
  <ul class="nav-links">
    <li><a href="#portada">Portada</a></li>
    <li><a href="#indicadores">Indicadores</a></li>
    <li><a href="#cotejo">Cotejo</a></li>
    <li><a href="#orden">Orden de Compra</a></li>
    <li><a href="#contrato">Contrato</a></li>
    <li><a href="#mercancia">Mercancía</a></li>
    <li><a href="#checklist">Checklist</a></li>
    <li><a href="#conclusiones">Conclusiones</a></li>
  </ul>
</nav>
 
<!-- ══════════════════════════════════ PORTADA ══════════════════════════════════ -->
<div id="portada">
  <div class="cover-grid"></div>
  <span class="float-icon fi1">📦</span>
  <span class="float-icon fi2">🏭</span>
  <span class="float-icon fi3">📋</span>
  <span class="float-icon fi4">💼</span>
  <span class="float-icon fi5">🤝</span>
 
  <div class="cover-content">
    <div class="cover-badge">Proyecto Semestral · Módulo Profesional</div>
 
    <h1 class="cover-title">
      Gestión de<br><span>Adquisiciones</span><br>de Mercancías y Servicios
    </h1>
    <p class="cover-subtitle">
      Análisis integral de los procesos de compras: indicadores, cotizaciones, contratos, órdenes de compra y protocolos de recepción y entrega de mercancía.
    </p>
    <div class="cover-divider"></div>
    <div class="cover-meta">
      <div class="meta-item">
        <span class="meta-label">Asignatura</span>
        <span class="meta-value">Documenta la Adquisición</span>
      </div>
      <div class="meta-item">
        <span class="meta-label">Módulo</span>
        <span class="meta-value">Adquisiciones</span>
      </div>
      <div class="meta-item">
        <span class="meta-label">Institución</span>
        <span class="meta-value">CECyTEC Acuña</span>
      </div>
    </div>
 
    <div class="cover-divider" style="margin-top:2.5rem;"></div>
 
    <div style="margin-top:1.5rem;">
      <span class="meta-label" style="display:block; margin-bottom:1rem; font-size:0.7rem; letter-spacing:0.25em; color:var(--slate);">INTEGRANTES DEL EQUIPO</span>
      <div style="display:flex; flex-wrap:wrap; justify-content:center; gap:0.6rem;">
        <span class="team-chip">Dominik Durón</span>
        <span class="team-chip">Melina Gamboa</span>
        <span class="team-chip">Sahydely Meyer</span>
        <span class="team-chip">Suny Cadena</span>
        <span class="team-chip">Wendy Córdova</span>
        <span class="team-chip">Isaí Vázquez</span>
      </div>
    </div>
  </div>
</div>
 
<!-- ══════════════════════════════════ 1. INDICADORES ══════════════════════════════════ -->
<div class="full-section bg-cream" id="indicadores">
  <div class="inner">
    <div class="section-header">
      <span class="section-number">// 01</span>
      <div class="divider-line"></div>
      <h2 class="section-title">Indicadores de Compras en Distintas Empresas</h2>
      <p class="section-desc">Los indicadores (KPIs) de compras permiten medir el desempeño del área de adquisiciones. Cada tipo de empresa enfoca sus métricas según su actividad económica.</p>
    </div>
 
    <div class="cards-grid">
 
      <!-- 1 -->
      <div class="card">
        <span class="card-icon">🏪</span>
        <div class="card-company">Empresa Comercial · Supermercado</div>
        <div class="card-title">Rotación de Inventario</div>
        <div class="indicator-value">12.4×</div>
        <div class="card-body">Mide cuántas veces se agota y repone el inventario durante un período. Un supermercado busca alta rotación para evitar mermas en perecederos.</div>
        <div class="indicator-formula">Costo de Ventas / Inventario Promedio = 12.4</div>
      </div>
 
      <!-- 2 -->
      <div class="card">
        <span class="card-icon">🏭</span>
        <div class="card-company">Empresa Industrial · Automotriz</div>
        <div class="card-title">Tasa de Defectos de Proveedor</div>
        <div class="indicator-value">0.8%</div>
        <div class="card-body">Porcentaje de piezas o insumos rechazados del total recibido. Crítico en manufactura donde una pieza defectuosa detiene la línea de producción.</div>
        <div class="indicator-formula">(Unidades Rechazadas / Total Recibidas) × 100</div>
      </div>
 
      <!-- 3 -->
      <div class="card">
        <span class="card-icon">🏥</span>
        <div class="card-company">Empresa de Servicios · Hospital</div>
        <div class="card-title">Cumplimiento en Tiempo de Entrega</div>
        <div class="indicator-value">97.5%</div>
        <div class="card-body">Porcentaje de pedidos de medicamentos e insumos médicos entregados puntualmente. En hospitales, el incumplimiento puede poner en riesgo vidas humanas.</div>
        <div class="indicator-formula">(Pedidos a Tiempo / Total Pedidos) × 100</div>
      </div>
 
      <!-- 4 -->
      <div class="card">
        <span class="card-icon">💻</span>
        <div class="card-company">Empresa Tecnológica · Startup TI</div>
        <div class="card-title">Ahorro en Negociación</div>
        <div class="indicator-value">18%</div>
        <div class="card-body">Mide el porcentaje ahorrado respecto al precio inicial cotizado por proveedores de licencias, hardware y servicios cloud. Refleja el poder de negociación del área.</div>
        <div class="indicator-formula">((Precio Inicial − Precio Final) / Precio Inicial) × 100</div>
      </div>
 
      <!-- 5 -->
      <div class="card">
        <span class="card-icon">🌾</span>
        <div class="card-company">Empresa Agroindustrial · Empacadora</div>
        <div class="card-title">Costo de Compra por Unidad Producida</div>
        <div class="indicator-value">$4.20</div>
        <div class="card-body">Relaciona el gasto total en materias primas (cajas, empaques, insumos) con las unidades producidas. Permite detectar ineficiencias en la cadena de suministro.</div>
        <div class="indicator-formula">Total Gasto Compras / Unidades Producidas</div>
      </div>
 
    </div>
  </div>
</div>
 
<!-- ══════════════════════════════════ 2. LISTA DE COTEJO ══════════════════════════════════ -->
<div class="full-section bg-light" id="cotejo">
  <div class="inner">
    <div class="section-header">
      <span class="section-number">// 02</span>
      <div class="divider-line"></div>
      <h2 class="section-title">Lista de Cotejo para Evaluación de Proveedores</h2>
      <p class="section-desc">Formato estructurado para evaluar y comparar proveedores de manera objetiva. Cada criterio está justificado con su importancia estratégica.</p>
    </div>
 
    <div class="alert"><strong>Empresa:</strong> Distribuidora NOROESTE S.A. de C.V. &nbsp;|&nbsp; <strong>Producto:</strong> Material de Empaque (cajas, bolsas, flejes) &nbsp;|&nbsp; <strong>Fecha:</strong> Junio 2025</div>
 
    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>#</th>
            <th>Criterio de Evaluación</th>
            <th>Peso (%)</th>
            <th>Escala</th>
            <th>Cumple</th>
            <th>Justificación del Criterio</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="td-num">01</td>
            <td class="td-bold">Precio Competitivo</td>
            <td>20%</td>
            <td>1 – 5</td>
            <td class="td-check">✔</td>
            <td>El precio impacta directamente en el margen de utilidad. Se evalúa que el costo por unidad sea igual o menor al promedio de mercado, sin sacrificar calidad.</td>
          </tr>
          <tr>
            <td class="td-num">02</td>
            <td class="td-bold">Calidad del Producto</td>
            <td>20%</td>
            <td>1 – 5</td>
            <td class="td-check">✔</td>
            <td>La calidad deficiente genera devoluciones, paros de línea y costos ocultos. El proveedor debe presentar certificaciones (ISO 9001 o equivalente) y muestras verificables.</td>
          </tr>
          <tr>
            <td class="td-num">03</td>
            <td class="td-bold">Tiempo de Entrega</td>
            <td>15%</td>
            <td>1 – 5</td>
            <td class="td-check">✔</td>
            <td>Los tiempos de entrega tardíos interrumpen la producción. Se verifica que el lead time prometido sea congruente con la capacidad real del proveedor.</td>
          </tr>
          <tr>
            <td class="td-num">04</td>
            <td class="td-bold">Condiciones de Pago</td>
            <td>15%</td>
            <td>1 – 5</td>
            <td class="td-check">✔</td>
            <td>Plazos de crédito amplios (30–60 días) mejoran el flujo de caja de la empresa compradora. Se evalúa la flexibilidad para negociar crédito sin intereses.</td>
          </tr>
          <tr>
            <td class="td-num">05</td>
            <td class="td-bold">Capacidad de Producción</td>
            <td>10%</td>
            <td>1 – 5</td>
            <td class="td-check">✔</td>
            <td>Es fundamental que el proveedor pueda cumplir picos de demanda sin desabasto. Se verifica que tenga capacidad instalada superior al volumen de pedido habitual.</td>
          </tr>
          <tr>
            <td class="td-num">06</td>
            <td class="td-bold">Servicio Posventa</td>
            <td>10%</td>
            <td>1 – 5</td>
            <td class="td-check">✔</td>
            <td>La atención ante reclamaciones, garantías y devoluciones reduce el riesgo operativo. Se evalúa tiempo de respuesta ante quejas y política de garantía escrita.</td>
          </tr>
          <tr>
            <td class="td-num">07</td>
            <td class="td-bold">Estabilidad Financiera</td>
            <td>5%</td>
            <td>1 – 5</td>
            <td class="td-check">✔</td>
            <td>Un proveedor con problemas financieros puede desaparecer o dejar de surtir. Se solicita estados de cuenta o referencias bancarias que avalen su solvencia.</td>
          </tr>
          <tr>
            <td class="td-num">08</td>
            <td class="td-bold">Certificaciones y Cumplimiento Legal</td>
            <td>5%</td>
            <td>1 – 5</td>
            <td class="td-check">✔</td>
            <td>El proveedor debe estar inscrito en el SAT, contar con RFC activo y cumplir con normas ambientales y laborales vigentes para evitar responsabilidades solidarias.</td>
          </tr>
        </tbody>
        <tfoot>
          <tr>
            <td colspan="2">PUNTUACIÓN TOTAL MÁXIMA</td>
            <td>100%</td>
            <td>40 pts</td>
            <td colspan="2">Mínimo aceptable para aprobación: 28/40 puntos (70%)</td>
          </tr>
        </tfoot>
      </table>
    </div>
  </div>
</div>
 
<!-- ══════════════════════════════════ 3. ORDEN DE COMPRA ══════════════════════════════════ -->
<div class="full-section bg-cream" id="orden">
  <div class="inner">
    <div class="section-header">
      <span class="section-number">// 03</span>
      <div class="divider-line"></div>
      <h2 class="section-title">Orden de Compra con Evaluación Comparativa</h2>
      <p class="section-desc">Se comparan dos cotizaciones de proveedores distintos, se evalúan sus condiciones y se justifica la selección final del proveedor ganador.</p>
    </div>
 
    <div class="oc-wrap">
      <!-- Header -->
      <div class="oc-header">
        <div>
          <div class="oc-company-name">DISTRIBUIDORA NOROESTE</div>
          <div class="oc-doc-title">S.A. de C.V. &nbsp;·&nbsp; RFC: DNO-920415-KL7 &nbsp;·&nbsp; Piedras Negras, Coah.</div>
        </div>
        <div style="text-align:right">
          <div class="oc-badge">OC-2025-0147</div>
          <div style="color:rgba(255,255,255,0.5); font-size:0.75rem; margin-top:0.5rem;">Fecha: 15 de junio de 2025</div>
        </div>
      </div>
 
      <div class="oc-body">
        <!-- Datos generales -->
        <div class="oc-section-title">📋 Datos de la Solicitud</div>
        <div class="oc-info-grid">
          <div class="oc-field"><label>Departamento Solicitante</label><span>Almacén y Operaciones</span></div>
          <div class="oc-field"><label>Responsable de Compra</label><span>L.A. María González Reyes</span></div>
          <div class="oc-field"><label>Tipo de Compra</label><span>Materiales de Empaque</span></div>
          <div class="oc-field"><label>Prioridad</label><span>🔴 Alta — Existencias agotadas</span></div>
          <div class="oc-field"><label>Fecha Requerida</label><span>25 de junio de 2025</span></div>
          <div class="oc-field"><label>Autoriza</label><span>Ing. Roberto Salinas — Dir. Gral.</span></div>
        </div>
 
        <!-- Artículos -->
        <div class="oc-section-title">📦 Artículos Solicitados</div>
        <div class="table-wrap" style="margin-bottom:2rem">
          <table>
            <thead>
              <tr>
                <th>Clave</th>
                <th>Descripción</th>
                <th>U.M.</th>
                <th>Cantidad</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td class="td-num">EMP-001</td>
                <td class="td-bold">Caja corrugada 60×40×40 cm, doble canal</td>
                <td>Pza</td>
                <td>5,000</td>
              </tr>
              <tr>
                <td class="td-num">EMP-002</td>
                <td class="td-bold">Bolsa polietileno 30×45 cm calibre 200</td>
                <td>Paq×100</td>
                <td>200</td>
              </tr>
              <tr>
                <td class="td-num">EMP-003</td>
                <td class="td-bold">Fleje plástico 12 mm × 1,000 m</td>
                <td>Rollo</td>
                <td>30</td>
              </tr>
            </tbody>
          </table>
        </div>
 
        <!-- Comparación de cotizaciones -->
        <div class="oc-section-title">⚖️ Comparación de Cotizaciones</div>
        <div class="eval-grid">
          <!-- Proveedor A -->
          <div class="eval-card">
            <div class="eval-card-title">🏢 PROVEEDOR A &nbsp; — &nbsp; EMPAQUES DEL NORTE S.A.</div>
            <div class="eval-row"><span class="eval-key">EMP-001 (5,000 pzas)</span><span class="eval-val">$37,500.00</span></div>
            <div class="eval-row"><span class="eval-key">EMP-002 (200 paq)</span><span class="eval-val">$5,800.00</span></div>
            <div class="eval-row"><span class="eval-key">EMP-003 (30 rollos)</span><span class="eval-val">$4,200.00</span></div>
            <div class="eval-row"><span class="eval-key">Subtotal s/IVA</span><span class="eval-val">$47,500.00</span></div>
            <div class="eval-row"><span class="eval-key">IVA (16%)</span><span class="eval-val">$7,600.00</span></div>
            <div class="eval-row"><span class="eval-key">Total c/IVA</span><span class="eval-val" style="color:var(--accent); font-size:1.05rem;">$55,100.00</span></div>
            <hr style="margin:0.8rem 0; border-color:rgba(0,0,0,0.08)">
            <div class="eval-row"><span class="eval-key">Tiempo de entrega</span><span class="eval-val">10 días hábiles</span></div>
            <div class="eval-row"><span class="eval-key">Forma de pago</span><span class="eval-val">Contado</span></div>
            <div class="eval-row"><span class="eval-key">Garantía calidad</span><span class="eval-val">Sin garantía escrita</span></div>
            <div class="eval-row"><span class="eval-key">Flete</span><span class="eval-val">$1,200.00 adicional</span></div>
            <div class="eval-row"><span class="eval-key">Certificaciones</span><span class="eval-val">Ninguna</span></div>
          </div>
 
          <!-- Proveedor B GANADOR -->
          <div class="eval-card winner">
            <div class="eval-card-title">🏢 PROVEEDOR B &nbsp; — &nbsp; CAJAS Y MÁS DE MÉXICO <span class="winner-badge">✓ SELECCIONADO</span></div>
            <div class="eval-row"><span class="eval-key">EMP-001 (5,000 pzas)</span><span class="eval-val">$35,000.00</span></div>
            <div class="eval-row"><span class="eval-key">EMP-002 (200 paq)</span><span class="eval-val">$5,400.00</span></div>
            <div class="eval-row"><span class="eval-key">EMP-003 (30 rollos)</span><span class="eval-val">$3,900.00</span></div>
            <div class="eval-row"><span class="eval-key">Subtotal s/IVA</span><span class="eval-val">$44,300.00</span></div>
            <div class="eval-row"><span class="eval-key">IVA (16%)</span><span class="eval-val">$7,088.00</span></div>
            <div class="eval-row"><span class="eval-key">Total c/IVA</span><span class="eval-val" style="color:var(--green); font-size:1.05rem;">$51,388.00</span></div>
            <hr style="margin:0.8rem 0; border-color:rgba(64,145,108,0.2)">
            <div class="eval-row"><span class="eval-key">Tiempo de entrega</span><span class="eval-val">6 días hábiles</span></div>
            <div class="eval-row"><span class="eval-key">Forma de pago</span><span class="eval-val">Crédito 30 días</span></div>
            <div class="eval-row"><span class="eval-key">Garantía calidad</span><span class="eval-val">30 días por escrito</span></div>
            <div class="eval-row"><span class="eval-key">Flete</span><span class="eval-val">Sin costo (incluido)</span></div>
            <div class="eval-row"><span class="eval-key">Certificaciones</span><span class="eval-val">ISO 9001:2015</span></div>
          </div>
        </div>
 
        <!-- Evaluación comparativa -->
        <div class="comp-table-wrap">
          <div class="comp-header">📊 Evaluación Comparativa Final</div>
          <div class="evaluacion-box">
            <p class="eval-conclusion">✅ PROVEEDOR SELECCIONADO: CAJAS Y MÁS DE MÉXICO S.A. DE C.V.</p>
            <p style="font-size:0.88rem; color:#2d6a4f; line-height:1.7;">
              <strong>Ahorro directo:</strong> $3,712.00 respecto al Proveedor A (6.7% menos).<br>
              <strong>Ahorro adicional:</strong> $1,200 en flete = Total ahorrado: <strong>$4,912.00</strong>.<br>
              <strong>Crédito a 30 días:</strong> Mejora el flujo de caja de la empresa durante ese período.<br>
              <strong>Menor tiempo de entrega:</strong> 6 vs 10 días, garantiza cumplir el plazo requerido (25 jun).<br>
              <strong>Calidad certificada:</strong> La certificación ISO 9001 y la garantía escrita reducen el riesgo de recibir material defectuoso que cause paros operativos.<br>
              <strong>Conclusión:</strong> El Proveedor B ofrece la mejor relación precio-calidad-servicio, siendo la opción estratégicamente óptima para esta adquisición.
            </p>
          </div>
        </div>
 
        <!-- Firmas OC -->
        <div class="firmas-grid" style="margin-top:2rem; padding-top:1.5rem; border-top:1px dashed #ccc; display:grid; grid-template-columns:repeat(3,1fr); gap:2rem; text-align:center;">
          <div>
            <div style="height:2px; background:var(--navy); margin-bottom:0.5rem; margin-top:2rem;"></div>
            <div style="font-weight:700; font-size:0.85rem;">L.A. María González Reyes</div>
            <div style="font-size:0.75rem; color:var(--slate);">Encargada de Compras</div>
          </div>
          <div>
            <div style="height:2px; background:var(--navy); margin-bottom:0.5rem; margin-top:2rem;"></div>
            <div style="font-weight:700; font-size:0.85rem;">C.P. Jorge Medina Luna</div>
            <div style="font-size:0.75rem; color:var(--slate);">Gerente Administrativo</div>
          </div>
          <div>
            <div style="height:2px; background:var(--navy); margin-bottom:0.5rem; margin-top:2rem;"></div>
            <div style="font-weight:700; font-size:0.85rem;">Ing. Roberto Salinas Vega</div>
            <div style="font-size:0.75rem; color:var(--slate);">Director General</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
 
<!-- ══════════════════════════════════ 4. CONTRATO DE COMPRAVENTA ══════════════════════════════════ -->
<div class="full-section bg-light" id="contrato">
  <div class="inner">
    <div class="section-header">
      <span class="section-number">// 04</span>
      <div class="divider-line"></div>
      <h2 class="section-title">Formato de Contrato de Compraventa</h2>
      <p class="section-desc">Contrato completo con datos de vendedor y comprador, condiciones comerciales, descripción de productos y espacios para firma oficial.</p>
    </div>
 
    <div class="contrato-wrap">
      <div class="contrato-watermark">ORIGINAL</div>
 
      <!-- Encabezado -->
      <div class="contrato-header">
        <div class="contrato-title">Contrato de Compraventa de Mercancías</div>
        <div class="contrato-num">Folio: CV-2025-0083 &nbsp;·&nbsp; Fecha: 16 de junio de 2025 &nbsp;·&nbsp; Piedras Negras, Coahuila, México</div>
      </div>
 
      <!-- Partes -->
      <div class="partes-grid">
        <div class="parte-card">
          <div class="parte-role">El Vendedor</div>
          <div class="parte-name">Cajas y Más de México S.A. de C.V.</div>
          <div class="parte-data">
            <strong>RFC:</strong> CMM-010325-AB2<br>
            <strong>Representante Legal:</strong> Lic. Alejandro Torres Fuentes<br>
            <strong>Domicilio fiscal:</strong> Blvd. Industrial 1450, Parque Ind. Sur, Monterrey, N.L., C.P. 64800<br>
            <strong>Tel:</strong> (81) 4550-9800 &nbsp;|&nbsp; <strong>Email:</strong> ventas@cajasymas.com.mx<br>
            <strong>Número de cuenta bancaria:</strong> BBVA 0199 4423 7210 (CLABE 012580001994423721)
          </div>
        </div>
        <div class="parte-card">
          <div class="parte-role">El Comprador</div>
          <div class="parte-name">Distribuidora Noroeste S.A. de C.V.</div>
          <div class="parte-data">
            <strong>RFC:</strong> DNO-920415-KL7<br>
            <strong>Representante Legal:</strong> Ing. Roberto Salinas Vega<br>
            <strong>Domicilio fiscal:</strong> Calle Zaragoza 820, Col. Centro, Piedras Negras, Coah., C.P. 26000<br>
            <strong>Tel:</strong> (878) 782-3300 &nbsp;|&nbsp; <strong>Email:</strong> compras@disnoroeste.mx<br>
            <strong>Condición de pago:</strong> Crédito a 30 días naturales
          </div>
        </div>
      </div>
 
      <!-- Objeto del contrato -->
      <div class="oc-section-title" style="font-family:'Playfair Display',serif; font-size:1rem; font-weight:700; color:var(--navy); margin:1.5rem 0 1rem; padding-bottom:0.5rem; border-bottom:2px solid var(--gold);">OBJETO DEL CONTRATO — Productos Comprados</div>
      <div class="table-wrap" style="margin-bottom:2rem">
        <table>
          <thead>
            <tr><th>Clave</th><th>Descripción del Producto</th><th>U.M.</th><th>Cantidad</th><th>Precio Unit. s/IVA</th><th>Subtotal</th></tr>
          </thead>
          <tbody>
            <tr>
              <td class="td-num">EMP-001</td>
              <td class="td-bold">Caja corrugada 60×40×40 cm, doble canal resistencia 150 kg</td>
              <td>Pza</td><td>5,000</td><td>$7.00</td><td>$35,000.00</td>
            </tr>
            <tr>
              <td class="td-num">EMP-002</td>
              <td class="td-bold">Bolsa polietileno transparente 30×45 cm calibre 200</td>
              <td>Paq×100</td><td>200</td><td>$27.00</td><td>$5,400.00</td>
            </tr>
            <tr>
              <td class="td-num">EMP-003</td>
              <td class="td-bold">Fleje plástico negro 12 mm × 1,000 m por rollo</td>
              <td>Rollo</td><td>30</td><td>$130.00</td><td>$3,900.00</td>
            </tr>
          </tbody>
          <tfoot>
            <tr><td colspan="5" style="text-align:right; background:var(--light);">Subtotal sin IVA:</td><td>$44,300.00</td></tr>
            <tr><td colspan="5" style="text-align:right; background:var(--light);">IVA (16%):</td><td>$7,088.00</td></tr>
            <tr><td colspan="5" style="text-align:right; background:var(--navy); color:white;">TOTAL CON IVA:</td><td style="background:var(--navy); color:var(--gold2); font-size:1.1rem;">$51,388.00</td></tr>
          </tfoot>
        </table>
      </div>
 
      <!-- Cláusulas -->
      <div class="oc-section-title" style="font-family:'Playfair Display',serif; font-size:1rem; font-weight:700; color:var(--navy); margin:1.5rem 0 1rem; padding-bottom:0.5rem; border-bottom:2px solid var(--gold);">CLÁUSULAS DEL CONTRATO</div>
      <div class="clausulas">
        <div class="clausula">
          <div class="clausula-title">PRIMERA — Objeto y Precio</div>
          <div class="clausula-text">El VENDEDOR se obliga a entregar al COMPRADOR los bienes descritos en la tabla anterior por un importe total de $51,388.00 M.N. (Cincuenta y un mil trescientos ochenta y ocho pesos 00/100 M.N.) incluido IVA, precio que es fijo e inamovible durante la vigencia del presente contrato.</div>
        </div>
        <div class="clausula">
          <div class="clausula-title">SEGUNDA — Forma y Lugar de Pago</div>
          <div class="clausula-text">El COMPRADOR realizará el pago íntegro mediante transferencia electrónica interbancaria a la cuenta indicada en los datos del vendedor, dentro de los 30 (treinta) días naturales siguientes a la fecha de recepción conforme de la mercancía y de la factura CFDI correspondiente.</div>
        </div>
        <div class="clausula">
          <div class="clausula-title">TERCERA — Entrega y Lugar</div>
          <div class="clausula-text">La mercancía será entregada en el almacén del COMPRADOR, ubicado en Calle Zaragoza 820, Piedras Negras, Coahuila, a más tardar el día 25 de junio de 2025. El flete y seguro de la mercancía en tránsito correrán por cuenta del VENDEDOR.</div>
        </div>
        <div class="clausula">
          <div class="clausula-title">CUARTA — Calidad y Garantía</div>
          <div class="clausula-text">El VENDEDOR garantiza que los productos son nuevos, libres de defectos y cumplen con las especificaciones técnicas acordadas. Ante cualquier defecto de fabricación detectado dentro de los 30 (treinta) días naturales posteriores a la entrega, el VENDEDOR se compromete a reponer la mercancía a su costo en un plazo no mayor a 5 días hábiles.</div>
        </div>
        <div class="clausula">
          <div class="clausula-title">QUINTA — Resolución de Controversias</div>
          <div class="clausula-text">Para todo lo no previsto en el presente contrato, las partes se someten a las leyes vigentes del Estado de Coahuila de Zaragoza, y en caso de controversia, a los Tribunales competentes de la ciudad de Saltillo, renunciando expresamente a cualquier otro fuero que por razón de sus domicilios pudiera corresponderles.</div>
        </div>
      </div>
 
      <!-- Firmas -->
      <div class="firmas-grid">
        <div class="firma-box">
          <div class="firma-line"></div>
          <div class="firma-name">Lic. Alejandro Torres Fuentes</div>
          <div class="firma-role">Representante Legal — EL VENDEDOR<br>Cajas y Más de México S.A. de C.V.</div>
        </div>
        <div class="firma-box">
          <div class="firma-line"></div>
          <div class="firma-name">Ing. Roberto Salinas Vega</div>
          <div class="firma-role">Representante Legal — EL COMPRADOR<br>Distribuidora Noroeste S.A. de C.V.</div>
        </div>
      </div>
 
      <p style="text-align:center; font-size:0.75rem; color:var(--slate); margin-top:2rem;">Contrato firmado en dos tantos originales de igual valor y fuerza legal, en la ciudad de Piedras Negras, Coahuila, el día 16 de junio de 2025.</p>
    </div>
  </div>
</div>
 
<!-- ══════════════════════════════════ 5. RECIBO Y ENTREGA DE MERCANCÍA ══════════════════════════════════ -->
<div class="full-section bg-navy" id="mercancia">
  <div class="inner">
    <div class="section-header">
      <span class="section-number">// 05</span>
      <div class="divider-line"></div>
      <h2 class="section-title">Reglas de Recibo y Entrega de Mercancía</h2>
      <p class="section-desc">Protocolos operativos de Distribuidora Noroeste S.A. de C.V. para garantizar el control total de la mercancía en sus dos flujos principales.</p>
    </div>
 
    <div class="steps-container">
      <!-- RECEPCIÓN -->
      <div>
        <div class="steps-group-title" style="color:var(--gold2);">📥 Recepción de Mercancía <span style="font-size:0.75rem; background:rgba(201,168,76,0.15); border:1px solid rgba(201,168,76,0.3); padding:0.2rem 0.6rem; border-radius:4px; font-family:'DM Sans',sans-serif; font-weight:500; color:var(--gold); letter-spacing:0.05em;">6 Pasos</span></div>
 
        <div class="step-item">
          <div class="step-number">1</div>
          <div class="step-content">
            <div class="step-title" style="color:white;">Verificación Documental Previa</div>
            <div class="step-desc" style="color:rgba(255,255,255,0.6);">Antes de permitir la descarga, el almacenista compara la orden de compra (OC-2025-0147) con la remisión o factura del proveedor. Se verifica número de folio, RFC, descripción de productos, cantidades y precios. Si hay discrepancia, se notifica al área de compras antes de continuar.</div>
          </div>
        </div>
 
        <div class="step-item">
          <div class="step-number">2</div>
          <div class="step-content">
            <div class="step-title" style="color:white;">Inspección Física del Transporte</div>
            <div class="step-desc" style="color:rgba(255,255,255,0.6);">Se revisa el estado del vehículo de transporte: que esté limpio, sin evidencias de plagas o humedad, y que los sellos de seguridad estén intactos. Se fotografía el sello de la caja antes de romperlo como evidencia.</div>
          </div>
        </div>
 
        <div class="step-item">
          <div class="step-number">3</div>
          <div class="step-content">
            <div class="step-title" style="color:white;">Conteo Físico y Muestreo</div>
            <div class="step-desc" style="color:rgba(255,255,255,0.6);">Se descarga y cuenta la totalidad de las unidades. Para lotes grandes se aplica muestreo estadístico (mínimo 10% del lote). Se registra la cantidad física recibida en el formato de entrada de almacén.</div>
          </div>
        </div>
 
        <div class="step-item">
          <div class="step-number">4</div>
          <div class="step-content">
            <div class="step-title" style="color:white;">Inspección de Calidad</div>
            <div class="step-desc" style="color:rgba(255,255,255,0.6);">Se verifica que los productos cumplan las especificaciones técnicas pactadas (resistencia de cajas, medidas, calibre de bolsas). Los artículos con defecto visible se separan en zona de rechazo y se documenta la incidencia para notificar al proveedor.</div>
          </div>
        </div>
 
        <div class="step-item">
          <div class="step-number">5</div>
          <div class="step-content">
            <div class="step-title" style="color:white;">Registro en Sistema y Etiquetado</div>
            <div class="step-desc" style="color:rgba(255,255,255,0.6);">Las unidades aceptadas se ingresan al sistema de inventario (ERP) con fecha, número de lote y ubicación de almacén. Se etiquetan con código interno para trazabilidad.</div>
          </div>
        </div>
 
        <div class="step-item">
          <div class="step-number">6</div>
          <div class="step-content">
            <div class="step-title" style="color:white;">Firma y Archivo de Documentos</div>
            <div class="step-desc" style="color:rgba(255,255,255,0.6);">El almacenista firma y sella la remisión del proveedor como acuse de recepción conforme. Una copia se archiva en expediente del proveedor; otra se envía al área de cuentas por pagar para iniciar el proceso de pago.</div>
          </div>
        </div>
      </div>
 
      <!-- ENTREGA -->
      <div>
        <div class="steps-group-title" style="color:var(--gold2);">📤 Entrega de Mercancía <span style="font-size:0.75rem; background:rgba(201,168,76,0.15); border:1px solid rgba(201,168,76,0.3); padding:0.2rem 0.6rem; border-radius:4px; font-family:'DM Sans',sans-serif; font-weight:500; color:var(--gold); letter-spacing:0.05em;">7 Pasos</span></div>
 
        <div class="step-item">
          <div class="step-number">1</div>
          <div class="step-content">
            <div class="step-title" style="color:white;">Recepción de Solicitud de Despacho</div>
            <div class="step-desc" style="color:rgba(255,255,255,0.6);">El área de ventas genera una orden de despacho (OD) firmada por el gerente. El almacenista solo inicia el proceso con una OD autorizada; no se despacha mercancía con solicitudes verbales o informales.</div>
          </div>
        </div>
 
        <div class="step-item">
          <div class="step-number">2</div>
          <div class="step-content">
            <div class="step-title" style="color:white;">Verificación de Existencias</div>
            <div class="step-desc" style="color:rgba(255,255,255,0.6);">Se consulta el sistema ERP para confirmar que el inventario disponible es suficiente para cubrir la OD. Si no hay existencias, se genera una alerta al área de compras antes de continuar.</div>
          </div>
        </div>
 
        <div class="step-item">
          <div class="step-number">3</div>
          <div class="step-content">
            <div class="step-title" style="color:white;">Picking (Preparación del Pedido)</div>
            <div class="step-desc" style="color:rgba(255,255,255,0.6);">El almacenista localiza la mercancía en su ubicación física, la reúne y verifica que corresponda exactamente con la OD (producto, cantidad, lote, fecha de caducidad si aplica). Se aplica el método PEPS (primero en entrar, primero en salir).</div>
          </div>
        </div>
 
        <div class="step-item">
          <div class="step-number">4</div>
          <div class="step-content">
            <div class="step-title" style="color:white;">Empaque y Embalaje</div>
            <div class="step-desc" style="color:rgba(255,255,255,0.6);">La mercancía se empaca adecuadamente para protegerla durante el transporte. Se utilizan materiales aprobados y se identifica cada bulto con etiqueta de embarque (cliente, destino, número de piezas, peso).</div>
          </div>
        </div>
 
        <div class="step-item">
          <div class="step-number">5</div>
          <div class="step-content">
            <div class="step-title" style="color:white;">Generación de Documentos de Salida</div>
            <div class="step-desc" style="color:rgba(255,255,255,0.6);">Se genera la remisión de salida o guía de transporte, y se timbra el CFDI (factura electrónica) correspondiente. Todos los documentos deben coincidir en cantidades, claves y valores antes de autorizar la salida.</div>
          </div>
        </div>
 
        <div class="step-item">
          <div class="step-number">6</div>
          <div class="step-content">
            <div class="step-title" style="color:white;">Supervisión de Carga y Sellado</div>
            <div class="step-desc" style="color:rgba(255,255,255,0.6);">El almacenista supervisa personalmente la carga al vehículo para evitar faltantes o daños durante el embarque. Una vez concluida la carga, se sella la unidad y se registra el número de sello en la documentación.</div>
          </div>
        </div>
 
        <div class="step-item">
          <div class="step-number">7</div>
          <div class="step-content">
            <div class="step-title" style="color:white;">Actualización de Inventario y Archivo</div>
            <div class="step-desc" style="color:rgba(255,255,255,0.6);">Se realiza el movimiento de salida en el sistema ERP para descargar el inventario. Se archiva copia de la remisión firmada por el chofer como comprobante de entrega. El expediente queda disponible para auditorías.</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
 
<!-- ══════════════════════════════════ 6. CHECKLIST CONTRATO ══════════════════════════════════ -->
<div class="full-section bg-cream" id="checklist">
  <div class="inner">
    <div class="section-header">
      <span class="section-number">// 06</span>
      <div class="divider-line"></div>
      <h2 class="section-title">Checklist del Contrato de Compraventa</h2>
      <p class="section-desc">Lista de verificación de los elementos jurídicos y comerciales indispensables en todo contrato de compraventa. Aplicado al contrato CV-2025-0083.</p>
    </div>
 
    <div class="checklist">
      <div class="check-item">
        <div class="check-icon">✔</div>
        <div class="check-text">
          <div class="check-title">Identificación completa de las partes</div>
          <div class="check-desc">Nombre o razón social, RFC, domicilio fiscal, representante legal y datos de contacto de vendedor y comprador. Aplicado: ambas partes incluidas con datos completos.</div>
        </div>
      </div>
 
      <div class="check-item">
        <div class="check-icon">✔</div>
        <div class="check-text">
          <div class="check-title">Descripción detallada de la mercancía</div>
          <div class="check-desc">Clave, descripción técnica, unidad de medida y cantidad. Evita ambigüedades que generen disputas. Aplicado: tabla con especificaciones completas de los 3 productos.</div>
        </div>
      </div>
 
      <div class="check-item">
        <div class="check-icon">✔</div>
        <div class="check-text">
          <div class="check-title">Precio unitario y total con IVA desglosado</div>
          <div class="check-desc">El precio debe ser claro, fijo e incluir desglose de IVA para efectos fiscales. Aplicado: subtotal, IVA 16% y total claramente especificados.</div>
        </div>
      </div>
 
      <div class="check-item">
        <div class="check-icon">✔</div>
        <div class="check-text">
          <div class="check-title">Condiciones de pago</div>
          <div class="check-desc">Forma, plazo y cuenta bancaria para el pago. Define las obligaciones económicas y los tiempos. Aplicado: crédito a 30 días, transferencia a cuenta BBVA especificada.</div>
        </div>
      </div>
 
      <div class="check-item">
        <div class="check-icon">✔</div>
        <div class="check-text">
          <div class="check-title">Fecha y lugar de entrega</div>
          <div class="check-desc">Establece el plazo de cumplimiento y el domicilio de entrega. Sin esta cláusula no hay referencia para penalizar incumplimientos. Aplicado: 25 de junio, almacén Piedras Negras.</div>
        </div>
      </div>
 
      <div class="check-item">
        <div class="check-icon">✔</div>
        <div class="check-text">
          <div class="check-title">Responsabilidad del flete</div>
          <div class="check-desc">Define quién asume el costo y riesgo del transporte. Evita cobros inesperados o pérdidas no cubiertas. Aplicado: flete e seguro a cargo del vendedor.</div>
        </div>
      </div>
 
      <div class="check-item">
        <div class="check-icon">✔</div>
        <div class="check-text">
          <div class="check-title">Garantía de calidad y procedimiento de devolución</div>
          <div class="check-desc">Especifica el plazo de garantía y el mecanismo de reposición ante defectos. Protege al comprador de pérdidas por mala calidad. Aplicado: 30 días, reposición en 5 días hábiles.</div>
        </div>
      </div>
 
      <div class="check-item">
        <div class="check-icon">✔</div>
        <div class="check-text">
          <div class="check-title">Cláusula de resolución de controversias</div>
          <div class="check-desc">Define el fuero y tribunales aplicables en caso de desacuerdo. Sin esta cláusula, los conflictos pueden prolongarse. Aplicado: leyes de Coahuila, tribunales de Saltillo.</div>
        </div>
      </div>
 
      <div class="check-item">
        <div class="check-icon">✔</div>
        <div class="check-text">
          <div class="check-title">Firmas autógrafas de representantes legales</div>
          <div class="check-desc">Otorgan validez jurídica al contrato. Deben ser de personas con poder notarial acreditado. Aplicado: espacios de firma con nombre completo y cargo de ambas partes.</div>
        </div>
      </div>
 
      <div class="check-item">
        <div class="check-icon">✔</div>
        <div class="check-text">
          <div class="check-title">Número de ejemplares y fecha de suscripción</div>
          <div class="check-desc">Indica cuántos originales se firman y cuándo. Garantiza que ambas partes conserven un ejemplar con igual valor legal. Aplicado: dos originales, 16 de junio de 2025.</div>
        </div>
      </div>
 
      <div class="check-item">
        <div class="check-icon">✔</div>
        <div class="check-text">
          <div class="check-title">Datos fiscales y CFDI</div>
          <div class="check-desc">RFC de ambas partes, régimen fiscal y uso del CFDI para cumplir obligaciones ante el SAT. Aplicado: RFC de vendedor y comprador incluidos en datos de las partes.</div>
        </div>
      </div>
 
      <div class="check-item">
        <div class="check-icon">✔</div>
        <div class="check-text">
          <div class="check-title">Vigencia del contrato</div>
          <div class="check-desc">Período durante el cual el contrato es válido y las condiciones son aplicables. Para compras únicas, la vigencia termina con el cumplimiento total de ambas partes. Aplicado: desde firma hasta cumplimiento total.</div>
        </div>
      </div>
    </div>
  </div>
</div>
 
<!-- ══════════════════════════════════ CONCLUSIONES ══════════════════════════════════ -->
<div class="full-section bg-navy" id="conclusiones">
  <div class="inner">
    <div class="section-header">
      <span class="section-number">// Conclusiones</span>
      <div class="divider-line"></div>
      <h2 class="section-title">Conclusiones del Proyecto</h2>
      <p class="section-desc" style="color:rgba(255,255,255,0.6);">El estudio integral de la gestión de adquisiciones revela los pilares que determinan la eficiencia del área de compras en cualquier organización.</p>
    </div>
 
    <div class="conclusiones-grid">
      <div class="concl-card">
        <span class="concl-icon">📊</span>
        <div class="concl-title">Los indicadores son la brújula</div>
        <div class="concl-text">Sin métricas claras no es posible saber si el área de compras agrega valor. Los KPIs como la tasa de defectos o el ahorro en negociación convierten intuiciones en decisiones objetivas y mejorables.</div>
      </div>
 
      <div class="concl-card">
        <span class="concl-icon">⚖️</span>
        <div class="concl-title">La comparación de cotizaciones protege a la empresa</div>
        <div class="concl-text">Evaluar mínimo dos proveedores antes de cada compra importante evita monopolios internos, detecta mejores condiciones comerciales y garantiza que el gasto es justificable ante cualquier auditoría.</div>
      </div>
 
      <div class="concl-card">
        <span class="concl-icon">📄</span>
        <div class="concl-title">El contrato es el escudo jurídico</div>
        <div class="concl-text">Un contrato de compraventa bien redactado reduce riesgos legales, define responsabilidades ante incumplimientos y es la primera herramienta de protección tanto del vendedor como del comprador.</div>
      </div>
 
      <div class="concl-card">
        <span class="concl-icon">🔄</span>
        <div class="concl-title">Los protocolos de almacén controlan el activo más valioso</div>
        <div class="concl-text">Los pasos de recepción y entrega de mercancía no son burocracia: son el sistema que garantiza que lo que se compra llegue completo y en buen estado, y que lo que sale esté debidamente autorizado y registrado.</div>
      </div>
 
      <div class="concl-card">
        <span class="concl-icon">🤝</span>
        <div class="concl-title">La relación con proveedores es estratégica</div>
        <div class="concl-text">Evaluar y calificar proveedores con listas de cotejo formales construye una base de datos de aliados confiables, reduciendo el riesgo de desabasto y mejorando las condiciones comerciales en el largo plazo.</div>
      </div>
 
      <div class="concl-card">
        <span class="concl-icon">🎯</span>
        <div class="concl-title">La gestión de compras es ventaja competitiva</div>
        <div class="concl-text">Una empresa que compra bien, al precio correcto, al proveedor correcto y en el momento adecuado, reduce sus costos operativos y mejora su rentabilidad sin necesidad de aumentar ventas ni precios al cliente final.</div>
      </div>
    </div>
 
    <div style="text-align:center; margin-top:3rem; padding-top:2rem; border-top:1px solid rgba(255,255,255,0.1);">
      <p style="font-family:'Playfair Display',serif; font-size:1.2rem; color:var(--gold2); margin-bottom:0.5rem;">"El éxito en compras no es pagar lo menos; es obtener el mayor valor al menor costo total."</p>
      <p style="font-size:0.8rem; color:var(--slate);">— Principio fundamental de la gestión estratégica de adquisiciones</p>
    </div>
  </div>
</div>
 
<!-- ══════════════════════════════════ FOOTER ══════════════════════════════════ -->
<footer>
  Proyecto Semestral · Módulo: Gestión de Adquisiciones de Mercancías y Servicios · <span>CECyTEC Acuña</span>
</footer>
 
<div class="export-hint" onclick="window.print()">🖨️ Imprimir / Exportar</div>
 
<script>
  // Smooth nav highlight
  const sections = document.querySelectorAll('[id]');
  const navLinks = document.querySelectorAll('.nav-links a');
 
  window.addEventListener('scroll', () => {
    let current = '';
    sections.forEach(s => {
      if (window.scrollY >= s.offsetTop - 100) current = s.id;
    });
    navLinks.forEach(a => {
      a.style.color = a.getAttribute('href') === '#' + current
        ? 'var(--gold2)' : 'rgba(255,255,255,0.75)';
    });
  });
 
  // Animate cards on scroll
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.style.opacity = '1';
        e.target.style.transform = 'translateY(0)';
      }
    });
  }, { threshold: 0.1 });
 
  document.querySelectorAll('.card, .check-item, .concl-card, .step-item').forEach(el => {
    el.style.opacity = '0';
    el.style.transform = 'translateY(20px)';
    el.style.transition = 'opacity 0.5s ease, transform 0.5s ease';
    observer.observe(el);
  });
</script>
 
</body>
</html>
 
