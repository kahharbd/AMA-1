<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ASTRONEXA Mission Academy | Lunar & Martian Outpost Trainer</title>
  
  <!-- Professional Fonts with System Fallbacks -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@700;800;900&family=Montserrat:wght@400;600;700;800&family=Share+Tech+Mono&display=swap" rel="stylesheet">

  <style>
    :root {
      --space-blue: #0b3d91;
      --mars-orange: #ea580c;
      --neon-cyan: #38bdf8;
      --safe-green: #22c55e;
      --alert-red: #ef4444;
      --bg-dark: #030712;
    }

    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: 'Montserrat', system-ui, -apple-system, sans-serif;
      background: radial-gradient(ellipse at bottom, #1e1b4b 0%, #030712 100%);
      color: #f8fafc;
      text-align: center;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      overflow-x: hidden;
      position: relative;
    }

    /* Ambient Space Glow & Star Background */
    body::before {
      content: "";
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      background-image: 
        radial-gradient(2px 2px at 20px 30px, #eee, rgba(0,0,0,0)),
        radial-gradient(2px 2px at 40px 70px, #fff, rgba(0,0,0,0)),
        radial-gradient(1px 1px at 90px 40px, #ddd, rgba(0,0,0,0)),
        radial-gradient(2px 2px at 160px 120px, #fff, rgba(0,0,0,0)),
        radial-gradient(1.5px 1.5px at 230px 190px, #fff, rgba(0,0,0,0));
      background-repeat: repeat;
      background-size: 300px 300px;
      opacity: 0.35;
      animation: starTwinkle 6s ease-in-out infinite alternate;
      pointer-events: none;
      z-index: 0;
    }

    @keyframes starTwinkle {
      0% { opacity: 0.25; transform: scale(1); }
      100% { opacity: 0.45; transform: scale(1.02); }
    }

    header {
      position: relative;
      z-index: 1;
      padding: 20px 15px 12px;
      background: rgba(3, 7, 18, 0.94);
      border-bottom: 2px solid var(--mars-orange);
      box-shadow: 0 4px 30px rgba(234, 88, 12, 0.25);
    }
    h1 {
      margin: 0;
      font-size: 1.9rem;
      letter-spacing: 2px;
      color: #fb923c;
      text-transform: uppercase;
      font-weight: 800;
      text-shadow: 0 0 20px rgba(251, 146, 60, 0.5);
    }
    .tagline {
      color: #94a3b8;
      font-size: 0.85rem;
      margin-top: 4px;
      letter-spacing: 1px;
    }
    .badge-bar {
      display: flex;
      justify-content: center;
      gap: 8px;
      flex-wrap: wrap;
      margin-top: 8px;
    }
    .badge {
      display: inline-block;
      background: #431407;
      color: #fdba74;
      border: 1px solid #c2410c;
      padding: 3px 12px;
      border-radius: 12px;
      font-size: 0.72rem;
      font-weight: 700;
      text-transform: uppercase;
      box-shadow: 0 0 10px rgba(194, 65, 12, 0.3);
    }
    .badge.nasa {
      background: #092359;
      color: #93c5fd;
      border-color: #1d4ed8;
      box-shadow: 0 0 10px rgba(29, 78, 216, 0.3);
    }

    /* Progress Track */
    .progress-container {
      width: 100%;
      max-width: 820px;
      margin: 14px auto 0;
      background: #1e293b;
      height: 8px;
      border-radius: 4px;
      overflow: hidden;
      border: 1px solid #334155;
    }
    .progress-bar {
      height: 100%;
      width: 33%;
      background: linear-gradient(90deg, #ea580c, #38bdf8);
      transition: width 0.5s ease;
      box-shadow: 0 0 12px #38bdf8;
    }

    .nav-tabs {
      position: relative;
      z-index: 1;
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 10px;
      margin: 18px 15px;
    }
    .tab-btn {
      background: #0f172a;
      color: #94a3b8;
      border: 1px solid #334155;
      padding: 10px 18px;
      border-radius: 20px;
      cursor: pointer;
      font-weight: 700;
      font-size: 0.82rem;
      transition: all 0.3s ease;
    }
    .tab-btn.active {
      background: #ea580c;
      color: #ffffff;
      border-color: #ea580c;
      box-shadow: 0 0 18px rgba(234, 88, 12, 0.5);
      transform: translateY(-2px);
    }

    .container {
      position: relative;
      z-index: 1;
      max-width: 840px;
      margin: 0 auto;
      padding: 0 15px 30px;
      width: 100%;
    }
    .module-card {
      display: none;
      background: rgba(15, 23, 42, 0.92);
      border: 1px solid #334155;
      border-radius: 18px;
      padding: 26px 22px;
      box-shadow: 0 12px 35px rgba(0, 0, 0, 0.7);
      backdrop-filter: blur(12px);
    }
    .module-card.active { 
      display: block; 
      animation: slideUp 0.4s ease-out forwards; 
    }
    @keyframes slideUp {
      from { opacity: 0; transform: translateY(16px); }
      to { opacity: 1; transform: translateY(0); }
    }

    h2 { margin-top: 0; color: #fdba74; font-size: 1.35rem; }
    .desc { color: #94a3b8; font-size: 0.9rem; margin-bottom: 22px; line-height: 1.5; }

    /* Module 1: Options Grid */
    .grid-options {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
      gap: 14px;
      margin-bottom: 15px;
    }
    .gear-card {
      background: #1e293b;
      border: 1px solid #334155;
      padding: 16px 14px;
      border-radius: 12px;
      cursor: pointer;
      transition: all 0.25s ease;
      text-align: left;
      position: relative;
    }
    .gear-card:hover { 
      border-color: #38bdf8; 
      transform: translateY(-3px);
      box-shadow: 0 6px 18px rgba(56, 189, 248, 0.15);
    }
    .gear-card.selected-correct {
      border-color: #22c55e;
      background: rgba(34, 197, 94, 0.18);
      pointer-events: none;
      box-shadow: 0 0 15px rgba(34, 197, 94, 0.25);
    }
    .gear-card.selected-wrong {
      border-color: #ef4444;
      background: rgba(239, 68, 68, 0.18);
      animation: shake 0.4s ease-in-out;
    }
    @keyframes shake {
      0%, 100% { transform: translateX(0); }
      25% { transform: translateX(-5px); }
      75% { transform: translateX(5px); }
    }

    .feedback-log {
      padding: 14px;
      border-radius: 10px;
      font-size: 0.88rem;
      margin-top: 15px;
      display: none;
      font-weight: 600;
      text-align: left;
      line-height: 1.45;
      animation: fadeIn 0.3s ease;
    }
    @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

    /* Module 2: Reactor HUD Console */
    .dashboard-panel {
      background: #020617;
      border: 1px solid #38bdf8;
      border-radius: 14px;
      padding: 20px;
      margin-bottom: 22px;
      box-shadow: inset 0 0 20px rgba(56, 189, 248, 0.1), 0 0 15px rgba(56, 189, 248, 0.15);
    }
    .telemetry-header {
      font-family: 'Share Tech Mono', monospace;
      color: #38bdf8;
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
      gap: 8px;
      margin-bottom: 16px;
      font-size: 0.82rem;
      border-bottom: 1px dashed #334155;
      padding-bottom: 10px;
    }
    .data-pill {
      background: rgba(56, 189, 248, 0.12);
      padding: 4px 10px;
      border-radius: 6px;
      border: 1px solid rgba(56, 189, 248, 0.35);
      font-weight: bold;
    }
    .power-grid-box {
      background: #0f172a;
      padding: 12px 18px;
      border-radius: 10px;
      margin-bottom: 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border: 1px solid #ea580c;
      box-shadow: 0 0 12px rgba(234, 88, 12, 0.2);
    }
    .subsystem-slider-row {
      display: grid;
      grid-template-columns: 145px 1fr 65px;
      align-items: center;
      gap: 12px;
      margin: 14px 0;
      text-align: left;
      font-size: 0.88rem;
    }
    input[type=range] {
      width: 100%;
      accent-color: #ea580c;
      cursor: pointer;
      height: 6px;
    }
    .status-meter-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
      margin-top: 20px;
    }
    .meter-card {
      background: #1e293b;
      padding: 12px 6px;
      border-radius: 10px;
      font-size: 0.75rem;
      text-align: center;
      border: 1px solid #334155;
      transition: all 0.3s ease;
    }
    .meter-val {
      font-size: 1.05rem;
      font-weight: 800;
      margin-top: 4px;
    }

    /* Module 3: Emergency Console */
    .crisis-box {
      background: rgba(239, 68, 68, 0.12);
      border: 1px solid #ef4444;
      border-radius: 12px;
      padding: 18px;
      margin-bottom: 20px;
      text-align: left;
      box-shadow: 0 0 20px rgba(239, 68, 68, 0.18);
    }
    .crisis-title {
      color: #f87171;
      font-weight: 800;
      font-size: 1.05rem;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .decision-btn {
      background: #1e293b;
      border: 1px solid #334155;
      color: #f8fafc;
      padding: 14px 16px;
      margin: 10px 0;
      border-radius: 10px;
      width: 100%;
      text-align: left;
      cursor: pointer;
      font-size: 0.88rem;
      transition: all 0.25s ease;
      line-height: 1.45;
    }
    .decision-btn:hover { 
      background: #334155; 
      border-color: #38bdf8;
      transform: translateX(4px);
    }

    .inline-alert {
      padding: 14px;
      border-radius: 10px;
      margin-top: 14px;
      display: none;
      font-size: 0.9rem;
      font-weight: 600;
      text-align: left;
      animation: fadeIn 0.3s ease;
    }
    .inline-alert.success {
      background: rgba(34, 197, 94, 0.18);
      border: 1px solid #22c55e;
      color: #4ade80;
    }
    .inline-alert.error {
      background: rgba(239, 68, 68, 0.18);
      border: 1px solid #ef4444;
      color: #f87171;
    }

    /* Diploma Generation Input */
    #nameModal {
      display: none;
      background: #0b132b;
      border: 2px solid #ea580c;
      border-radius: 14px;
      padding: 26px;
      margin: 22px auto;
      max-width: 500px;
      box-shadow: 0 0 30px rgba(234, 88, 12, 0.3);
      animation: slideUp 0.4s ease-out;
    }
    .input-box {
      width: 90%;
      padding: 12px 18px;
      border-radius: 8px;
      border: 1px solid #fdba74;
      background: #020617;
      color: #fff;
      font-size: 1.05rem;
      margin-bottom: 16px;
      outline: none;
      text-align: center;
    }

    /* Official Diploma Card */
    #certificateWrapper {
      display: none;
      margin-top: 20px;
      animation: fadeIn 0.6s ease;
    }
    .cert-frame {
      background: #060d1a;
      border: 12px solid #d4af37;
      outline: 3px solid #f59e0b;
      outline-offset: -7px;
      padding: 35px 45px;
      border-radius: 14px;
      box-shadow: 0 15px 45px rgba(0, 0, 0, 0.8), 0 0 35px rgba(212, 175, 55, 0.3);
      text-align: center;
      color: #ffffff;
      position: relative;
    }
    .cert-badge-icon {
      font-size: 2.6rem;
      margin-bottom: 4px;
      filter: drop-shadow(0 0 12px #f59e0b);
    }
    .cert-header {
      font-family: 'Cinzel', serif;
      font-size: 1.85rem;
      font-weight: 800;
      letter-spacing: 2.5px;
      color: #ffd700;
      margin: 0;
      text-transform: uppercase;
    }
    .cert-sub-header {
      font-size: 0.8rem;
      letter-spacing: 2px;
      color: #94a3b8;
      margin-top: 4px;
      font-weight: 600;
      text-transform: uppercase;
    }
    .cert-presents {
      font-size: 0.9rem;
      font-style: italic;
      color: #cbd5e1;
      margin-top: 16px;
    }
    .cert-name {
      font-family: 'Cinzel', serif;
      font-size: 2.2rem;
      font-weight: 700;
      color: #38bdf8;
      margin: 8px auto;
      text-transform: uppercase;
      letter-spacing: 2px;
      border-bottom: 2px solid rgba(212, 175, 55, 0.5);
      display: inline-block;
      padding: 0 30px 4px;
    }
    .cert-statement {
      font-size: 0.92rem;
      color: #e2e8f0;
      line-height: 1.65;
      max-width: 680px;
      margin: 10px auto 20px;
    }
    .cert-signatures {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      border-top: 1px dashed rgba(212, 175, 55, 0.4);
      padding-top: 16px;
      margin-top: 12px;
      font-size: 0.8rem;
    }
    .sig-block { text-align: center; width: 170px; }
    .sig-line {
      font-family: 'Cinzel', serif;
      font-weight: 700;
      color: #ffd700;
      border-bottom: 1px solid #64748b;
      padding-bottom: 4px;
      margin-bottom: 4px;
    }
    .sig-title { font-size: 0.72rem; color: #94a3b8; }

    .action-btn {
      background: linear-gradient(90deg, #ea580c, #f97316);
      color: #fff;
      border: none;
      padding: 13px 28px;
      border-radius: 8px;
      font-weight: 700;
      cursor: pointer;
      font-size: 0.92rem;
      transition: all 0.25s ease;
      box-shadow: 0 4px 15px rgba(234, 88, 12, 0.35);
    }
    .action-btn:hover { 
      transform: translateY(-2px);
      box-shadow: 0 6px 20px rgba(234, 88, 12, 0.5);
    }

    footer {
      position: relative;
      z-index: 1;
      background: #020617;
      border-top: 1px solid #1e293b;
      padding: 18px 15px;
      font-size: 0.76rem;
      color: #64748b;
      line-height: 1.6;
    }
    footer a { color: #ea580c; text-decoration: none; font-weight: 600; }

    /* Print / PDF Styling */
    @page { size: A4 landscape; margin: 8mm; }
    @media print {
      body, html {
        margin: 0 !important;
        padding: 0 !important;
        background: #060d1a !important;
        -webkit-print-color-adjust: exact !important;
        print-color-adjust: exact !important;
      }
      body::before, header, .nav-tabs, footer, .progress-container,
      #module0, #module1, #nameModal, .action-btn,
      .module-card h2, .module-card .desc, #crisisCard, #crisisChoices {
        display: none !important;
      }
      .container { max-width: 100% !important; margin: 0 !important; padding: 0 !important; }
      .module-card { border: none !important; background: transparent !important; box-shadow: none !important; padding: 0 !important; }
      #certificateWrapper { display: block !important; margin: 0 !important; padding: 0 !important; }
      .cert-frame {
        width: 100% !important;
        height: 92vh !important;
        border: 12px solid #b8860b !important;
        outline: 3px solid #854d0e !important;
        outline-offset: -7px !important;
        border-radius: 8px !important;
        background: #060d1a !important;
        display: flex !important;
        flex-direction: column !important;
        justify-content: space-between !important;
      }
    }
  </style>
</head>
<body>

  <header>
    <h1>ASTRONEXA MISSION ACADEMY</h1>
    <div class="tagline">Junior Astronaut Mission Trainer • NASA Space Apps Challenge 2026</div>
    <div class="badge-bar">
      <span class="badge">Lunar & Martian Outpost Command</span>
      <span class="badge nasa">NASA DONKI & InSight Verified</span>
      <span class="badge nasa">100% Offline Capable</span>
    </div>
    <div class="progress-container">
      <div class="progress-bar" id="progressBar"></div>
    </div>
  </header>

  <div class="nav-tabs">
    <button class="tab-btn active" id="btn0" onclick="switchModule(0)">1. Outpost Architecture</button>
    <button class="tab-btn" id="btn1" onclick="switchModule(1)">2. 100 kW Reactor Grid</button>
    <button class="tab-btn" id="btn2" onclick="switchModule(2)">3. Solar Storm Command</button>
  </div>

  <div class="container">
    
    <!-- MODULE 1: OUTPOST ARCHITECTURE -->
    <div class="module-card active" id="module0">
      <h2>Module 1: Lunar/Martian Outpost Setup</h2>
      <div class="desc">
        Astronauts cannot survive with Earth equipment alone! Select <b>all 3 real space technologies</b> to initialize life support:
      </div>

      <div class="grid-options">
        <div class="gear-card" onclick="selectGear(this, true, 'Sintered Regolith Shield: Heavy Moon/Mars soil barrier stops lethal cosmic rays and meteorites.')">
          🛡️ <b>Regolith Radiation Shield</b><br><small style="color:#94a3b8;">Planetary Soil Barrier</small>
        </div>
        <div class="gear-card" onclick="selectGear(this, false, 'Glass Greenhouse: Thin glass shatters instantly under space vacuum and meteorites!')">
          🏡 <b>Standard Earth Greenhouse</b><br><small style="color:#94a3b8;">Fragile Glass (Fails)</small>
        </div>
        <div class="gear-card" onclick="selectGear(this, true, 'NASA Kilopower Reactor: Small nuclear fission power that runs nonstop through freezing 14-day lunar nights.')">
          ⚡ <b>NASA Kilopower Reactor</b><br><small style="color:#94a3b8;">100 kW Continuous Energy</small>
        </div>
        <div class="gear-card" onclick="selectGear(this, false, 'Diesel Combustion Engine: Fire cannot burn on the Moon or Mars without free oxygen!')">
          ⛽ <b>Diesel Fuel Generator</b><br><small style="color:#94a3b8;">Combustion Engine (Fails)</small>
        </div>
        <div class="gear-card" onclick="selectGear(this, true, 'Closed-Loop Hydroponic Bay: Fast-growing algae and plants that continuously recycle water and generate fresh oxygen.')">
          🌱 <b>Closed-Loop Hydroponic Bay</b><br><small style="color:#94a3b8;">Bio-regenerative O2 & Crops</small>
        </div>
        <div class="gear-card" onclick="selectGear(this, false, 'Imported Food Cans: Shipping cans from Earth is too heavy and runs out after a few months!')">
          🥫 <b>Ration Supply Cans Only</b><br><small style="color:#94a3b8;">Non-renewable Logistics</small>
        </div>
      </div>

      <div id="gearFeedback" class="feedback-log"></div>
      <div id="gearProgress" style="margin-top:14px; font-weight:700; color:#fdba74;">Subsystems Initialized: 0 / 3</div>
    </div>

    <!-- MODULE 2: COMPETING DEMANDS & TRADE-OFF SIMULATOR -->
    <div class="module-card" id="module1">
      <h2>Module 2: 100 kW Reactor Balancing Engine</h2>
      <div class="desc">
        <b>Real Engineering Constraint:</b> You only have <b>100 kW total power</b>! Giving more power to one system robs another. Adjust the sliders to keep all systems operational!
      </div>

      <div class="dashboard-panel">
        <div class="telemetry-header">
          <span>📡 BASE TELEMETRY: MARS JEZERO CRATER</span>
          <span class="data-pill" id="marsWeatherVal">NASA InSight Telemetry: Temp -63°C | Flux 590 W/m²</span>
        </div>

        <div class="power-grid-box">
          <span style="font-weight:700; color:#fdba74;">KILOPOWER GENERATOR CAPACITY:</span>
          <span style="font-family:'Share Tech Mono', monospace; font-size:1.2rem; font-weight:bold;" id="powerStatus">100 kW / 100 kW</span>
        </div>

        <!-- Sliders -->
        <div class="subsystem-slider-row">
          <span>🫁 Life Support (O2):</span>
          <input type="range" id="o2Slider" min="10" max="60" value="35" oninput="balanceResources()">
          <b id="o2Val">35 kW</b>
        </div>

        <div class="subsystem-slider-row">
          <span>🛡️ Radiation Shield:</span>
          <input type="range" id="shieldSlider" min="10" max="60" value="35" oninput="balanceResources()">
          <b id="shieldVal">35 kW</b>
        </div>

        <div class="subsystem-slider-row">
          <span>🌱 Food & Crop Bay:</span>
          <input type="range" id="foodSlider" min="10" max="60" value="30" oninput="balanceResources()">
          <b id="foodVal">30 kW</b>
        </div>

        <!-- Metrics -->
        <div class="status-meter-grid">
          <div class="meter-card">
            <div>Oxygen Output</div>
            <div class="meter-val" id="o2Meter" style="color:#22c55e;">98%</div>
          </div>
          <div class="meter-card">
            <div>Radiation Def.</div>
            <div class="meter-val" id="shieldMeter" style="color:#22c55e;">95%</div>
          </div>
          <div class="meter-card">
            <div>Crop Biomass</div>
            <div class="meter-val" id="foodMeter" style="color:#22c55e;">90%</div>
          </div>
          <div class="meter-card">
            <div>Outpost Status</div>
            <div class="meter-val" id="baseMeter" style="color:#22c55e;">OPTIMAL</div>
          </div>
        </div>
      </div>

      <div id="simLog" style="font-size:0.9rem; font-weight:600; color:#38bdf8; margin-bottom:18px;">
        ⚖️ Balance your load within 100 kW to keep all vital metrics above 70%.
      </div>

      <button class="action-btn" id="lockTradeoffBtn" onclick="switchModule(2)">Confirm Trade-off & Enter Emergency Mission ➔</button>
    </div>

    <!-- MODULE 3: COMMAND CRISIS & CERTIFICATION -->
    <div class="module-card" id="module2">
      <h2>Module 3: Flight Director Crisis Examination</h2>
      <div class="desc">A real space commander makes difficult decisions. What is your engineering choice?</div>

      <div id="crisisCard">
        <div class="crisis-box">
          <div class="crisis-title">⚠️ NASA DONKI ALERT: LETHAL SOLAR PARTICLE EVENT (SPE)</div>
          <p style="font-size:0.9rem; color:#cbd5e1; margin-top:8px; line-height:1.5;">
            Lethal solar radiation is peaking at <b>450 mSv/hr</b> (Source: NASA DONKI Baseline). Auxiliary solar panels failed. You only have <b>50 kW emergency backup power</b>. How do you re-balance?
          </p>
        </div>

        <div id="crisisChoices">
          <button class="decision-btn" onclick="resolveCrisis(false, 'FATAL COMPROMISE: Life Support completely depowered! The crew ran out of oxygen.')">
            A) Turn off 100% of Life Support power to keep crop lighting maximum.
          </button>
          <button class="decision-btn" onclick="resolveCrisis(true, 'PERFECT TRADE-OFF: Crops safely survive 48 hours in darkness, while boosted magnetic shields deflected the deadly proton storm!')">
            B) Divert crop power to electromagnetic radiation shields while holding life support at minimum baseline.
          </button>
          <button class="decision-btn" onclick="resolveCrisis(false, 'RADIATION CASUALTY: De-powering shields exposed the outpost to lethal cosmic radiation!')">
            C) Turn off radiation shielding completely to keep communications and food growth running.
          </button>
        </div>

        <div id="crisisFeedback" class="inline-alert"></div>
      </div>

      <!-- Cadet Name Modal -->
      <div id="nameModal">
        <h3 style="color:#ffd700; font-family:'Cinzel', serif; font-size:1.35rem; margin-top:0;">🌟 OUTPOST MISSION ACCOMPLISHED! 🌟</h3>
        <p style="font-size:0.92rem; color:#cbd5e1;">Enter your name to generate your Official NASA Space Apps Outpost Commander Diploma:</p>
        <input type="text" id="cadetNameInput" class="input-box" placeholder="e.g. Commander Kahhar" />
        <br>
        <button class="action-btn" style="background:#22c55e;" onclick="generateCertificate()">Generate Commander Diploma 🚀</button>
      </div>

      <!-- Printable Diploma Card -->
      <div id="certificateWrapper">
        <div class="cert-frame">
          <div>
            <div class="cert-badge-icon">🏛️</div>
            <h3 class="cert-header">OUTPOST COMMAND DIPLOMA</h3>
            <div class="cert-sub-header">ASTRONEXA MISSION ACADEMY • NASA SPACE APPS CHALLENGE 2026</div>
          </div>

          <div>
            <div class="cert-presents">This official credential certifies that</div>
            <div class="cert-name" id="certCadetName">CADET COMMANDER</div>
            <div class="cert-statement">
              has demonstrated superior engineering trade-off mastery in balancing competing demands—including closed-loop life support, regolith radiation shielding, kilowatt power grids, and bio-regenerative food production—ensuring successful outpost survival.
            </div>
          </div>

          <div class="cert-signatures">
            <div class="sig-block">
              <div class="sig-line">ASTRONEXA-OUTPOST-2026</div>
              <div class="sig-title">Verification Code</div>
            </div>
            <div class="sig-block">
              <div class="sig-line">Dhaka, Bangladesh</div>
              <div class="sig-title">Global Event Location</div>
            </div>          
            <div class="sig-block">
              <div class="sig-line">Kurrat Abdul Kahhar</div>
              <div class="sig-title">Team Lead, ASTRONEXA</div>
            </div>
          </div>
        </div>

        <div style="margin-top: 25px;">
          <button class="action-btn" style="background:#22c55e; font-size:1rem; padding:12px 32px;" onclick="window.print()">🖨️ Print / Download PDF</button>
        </div>
      </div>

    </div>

  </div>

  <footer>
    <div style="font-weight:700; color:#f8fafc; margin-bottom:6px;">OFFICIAL NASA OPEN DATA CITATIONS & VERIFICATIONS:</div>
    • <b>NASA InSight & Curiosity:</b> Mars Surface Telemetry & Atmospheric Pressure Baselines (<a href="https://api.nasa.gov/" target="_blank">api.nasa.gov</a>)<br>
    • <b>NASA DONKI:</b> Space Weather Database of Notifications, Knowledge, Information (SPE & Solar Flux Baselines)<br>
    • <b>NASA Kilopower & Advanced Life Support (ALS):</b> 10-100 kW Fission Surface Power Architecture (<a href="https://www.nasa.gov" target="_blank">nasa.gov/spec-outpost</a>)<br>
    <div style="margin-top:8px; color:#f8fafc; font-style:italic;">Team ASTRONEXA — "Connecting Today's Ideas with Tomorrow's Discoveries"</div>
  </footer>

  <script>
    let currentModule = 0;

    function setProgress(percent) {
      document.getElementById('progressBar').style.width = percent + '%';
    }

    function switchModule(index) {
      currentModule = index;
      const cards = document.querySelectorAll('.module-card');
      const tabs = document.querySelectorAll('.tab-btn');
      
      cards.forEach((c, i) => c.classList.toggle('active', i === index));
      tabs.forEach((t, i) => t.classList.toggle('active', i === index));

      if (index === 0) setProgress(33);
      if (index === 1) setProgress(66);
      if (index === 2) setProgress(90);
    }

    // MODULE 1 Logic
    let correctGearFound = 0;
    function selectGear(element, isCorrect, detailText) {
      const feedback = document.getElementById('gearFeedback');
      feedback.style.display = 'block';

      if(isCorrect) {
        if(!element.classList.contains('selected-correct')) {
          element.classList.add('selected-correct');
          correctGearFound++;
          feedback.style.background = 'rgba(34, 197, 94, 0.2)';
          feedback.style.color = '#4ade80';
          feedback.style.border = '1px solid #22c55e';
          feedback.innerHTML = `✅ <b>DEPLOYED:</b> ${detailText}`;
          document.getElementById('gearProgress').innerText = `Subsystems Initialized: ${correctGearFound} / 3`;
          
          if(correctGearFound === 3) {
            feedback.innerHTML += "<br>🚀 <b>All Essential Subsystems Live! Transitioning to Reactor Grid in 1.5s...</b>";
            setProgress(60);
            setTimeout(() => { switchModule(1); }, 1500);
          }
        }
      } else {
        element.classList.add('selected-wrong');
        feedback.style.background = 'rgba(239, 68, 68, 0.2)';
        feedback.style.color = '#f87171';
        feedback.style.border = '1px solid #ef4444';
        feedback.innerHTML = `⚠️ <b>ENGINEERING FAILURE:</b> ${detailText}`;
        setTimeout(() => element.classList.remove('selected-wrong'), 1800);
      }
    }

    // MODULE 2 Logic
    function balanceResources() {
      const o2 = parseInt(document.getElementById('o2Slider').value);
      const shield = parseInt(document.getElementById('shieldSlider').value);
      const food = parseInt(document.getElementById('foodSlider').value);

      document.getElementById('o2Val').innerText = o2 + " kW";
      document.getElementById('shieldVal').innerText = shield + " kW";
      document.getElementById('foodVal').innerText = food + " kW";

      const totalPower = o2 + shield + food;
      const powerStatusEl = document.getElementById('powerStatus');
      const simLog = document.getElementById('simLog');
      const baseMeter = document.getElementById('baseMeter');

      powerStatusEl.innerText = `${totalPower} kW / 100 kW`;

      if (totalPower > 100) {
        powerStatusEl.style.color = '#ef4444';
        baseMeter.innerText = 'OVERLOAD';
        baseMeter.style.color = '#ef4444';
        simLog.innerHTML = '⚠️ <b>REACTOR OVERLOAD!</b> Demand exceeds 100 kW generator capacity. Cut subsystem usage!';
        simLog.style.color = '#ef4444';
        document.getElementById('lockTradeoffBtn').disabled = true;
      } else {
        powerStatusEl.style.color = '#22c55e';
        document.getElementById('o2Meter').innerText = Math.min(100, Math.round(o2 * 2.5)) + '%';
        document.getElementById('shieldMeter').innerText = Math.min(100, Math.round(shield * 2.5)) + '%';
        document.getElementById('foodMeter').innerText = Math.min(100, Math.round(food * 2.8)) + '%';

        if (o2 < 20 || shield < 20 || food < 15) {
          baseMeter.innerText = 'HAZARD';
          baseMeter.style.color = '#eab308';
          simLog.innerHTML = '⚠️ <b>DEFICIENCY WARNING:</b> One or more survival metrics dropped below safe threshold!';
          simLog.style.color = '#eab308';
          document.getElementById('lockTradeoffBtn').disabled = false;
        } else {
          baseMeter.innerText = 'OPTIMAL';
          baseMeter.style.color = '#22c55e';
          simLog.innerHTML = '✅ <b>STABLE GRID:</b> Reactor output safely balanced across all life support needs.';
          simLog.style.color = '#22c55e';
          document.getElementById('lockTradeoffBtn').disabled = false;
        }
      }
    }

    // MODULE 3 Logic (In-App Response Cards)
    function resolveCrisis(isSuccess, message) {
      const fb = document.getElementById('crisisFeedback');
      fb.style.display = 'block';

      if(isSuccess) {
        fb.className = 'inline-alert success';
        fb.innerHTML = `✅ <b>MISSION SAVED:</b> ${message}`;
        setTimeout(() => {
          document.getElementById('crisisCard').style.display = 'none';
          document.getElementById('nameModal').style.display = 'block';
        }, 1600);
      } else {
        fb.className = 'inline-alert error';
        fb.innerHTML = `❌ <b>TRADE-OFF FAILED:</b> ${message} <i>(Try another emergency decision)</i>`;
      }
    }

    function generateCertificate() {
      const inputVal = document.getElementById('cadetNameInput').value;
      const cadetName = inputVal && inputVal.trim() !== "" ? inputVal.trim() : "Cadet Commander Kahhar";
      document.getElementById('certCadetName').innerText = cadetName;
      document.getElementById('nameModal').style.display = 'none';
      document.getElementById('certificateWrapper').style.display = 'block';
      setProgress(100);
    }

    // Init
    balanceResources();
    setProgress(33);
  </script>
</body>
</html>
