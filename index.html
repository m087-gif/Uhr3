<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>LED Panel Anzeige - Vita Plan GmbH</title>
<style>
  :root{--bg:#0b0f17;--fg:#e9edf1;--card:#141a24;--accent:#d4af37}
  /* Fixe LED-Panel-Größe */
  html,body{width:1152px;height:576px;margin:0;background:var(--bg);color:var(--fg);font-family:ui-sans-serif,system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial;overflow:hidden}

  /* 3 Spalten: Wetter links, Logo Mitte, Uhr rechts */
  .layout{display:grid;grid-template-columns:1fr 1fr 1fr;align-items:center;height:100%;padding:20px;gap:20px}

  /* Wetter */
  .weather{background:var(--card);border-radius:20px;padding:18px;display:flex;flex-direction:column;gap:12px;align-items:flex-start;animation:fadeSlideIn 0.8s ease forwards}
  @keyframes fadeSlideIn{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:translateY(0)}}
  .weather .head{display:flex;align-items:center;gap:12px;width:100%;justify-content:space-between}
  .wx-city{font-weight:800;font-size:18px}
  .wx-now{display:flex;align-items:center;gap:14px}
  .wx-temp{font-size:44px;font-weight:900;animation:tempPulse 3s infinite}
  @keyframes tempPulse{0%,100%{transform:scale(1)}50%{transform:scale(1.05)}}
  .wx-desc{color:#9aa4af}
  .forecast{display:flex;gap:8px;width:100%;margin-top:8px}
  .day{background:rgba(255,255,255,.03);padding:8px;border-radius:10px;flex:1;text-align:center}
  .day .d{font-weight:700}

  /* Logo Mitte */
  .logo-box{background:var(--card);border-radius:20px;padding:18px;display:flex;justify-content:center;align-items:center}
  .logo-box img{max-width:90%;height:auto}

  /* Uhr rechts */
  .card-clock{display:flex;justify-content:center;align-items:center}
  .clock-wrap{width:100%;max-width:520px;aspect-ratio:1}
  svg{width:100%;height:100%}

  /* Beschriftungen */
  .brand-top{font-weight:700;font-size:40px;fill:#dcdcdc}
  .day-text{font-weight:800;font-size:64px;fill:#e6e9ee;letter-spacing:1px}
  .date-text{font-weight:800;font-size:56px;fill:#000;text-anchor:middle;dominant-baseline:middle}

  /* Für den Sunburst weiche Kanten */
  .sunburst-lines{opacity:.28}
</style>
</head>
<body>
<div class="layout">
  <!-- Wetter LINKS -->
  <aside class="weather" id="weatherBox">
    <div class="head">
      <div class="wx-city" id="wxCity">Wil SG</div>
      <div class="wx-updated" id="updated">—</div>
    </div>
    <div class="wx-now">
      <div class="wx-temp" id="wxTemp">--°</div>
      <div>
        <div class="wx-desc" id="wxDesc">Wetter lädt…</div>
        <div class="wx-extra" id="wxExtra">—</div>
      </div>
    </div>
    <div class="forecast" id="forecast"></div>
  </aside>

  <!-- Logo MITTE -->
  <aside class="logo-box">
    <img id="mainLogo" src="Logo_neu_2025_original_Pantone.png" alt="Vita Plan Logo">
  </aside>

  <!-- Uhr RECHTS -->
  <main class="card-clock">
    <div class="clock-wrap" aria-label="Analoge Uhr im Datejust-Stil">
      <svg viewBox="0 0 1000 1000">
        <defs>
          <!-- Bezel / Zifferblatt-Gradients & Filter -->
          <radialGradient id="bezelGrad" cx="50%" cy="50%" r="60%">
            <stop offset="0%" stop-color="#fff8df" stop-opacity="0.95"/>
            <stop offset="100%" stop-color="#b08b3a"/>
          </radialGradient>
          <radialGradient id="dialGrad" cx="50%" cy="50%" r="60%">
            <stop offset="0%" stop-color="#0a0a0a"/>
            <stop offset="100%" stop-color="#111111"/>
          </radialGradient>
          <filter id="handShadow" x="-50%" y="-50%" width="200%" height="200%">
            <feDropShadow dx="0" dy="4" stdDeviation="6" flood-color="#000" flood-opacity=".6"/>
          </filter>
          <filter id="sunBlur" x="-50%" y="-50%" width="200%" height="200%">
            <feGaussianBlur stdDeviation="0.8"/>
          </filter>
          <clipPath id="dialClip"><circle cx="500" cy="500" r="420"/></clipPath>
        </defs>

        <!-- Bezel -->
        <circle cx="500" cy="500" r="480" fill="url(#bezelGrad)" stroke="#caa84d" stroke-width="8"/>
        <circle cx="500" cy="500" r="460" fill="none" stroke="rgba(255,255,255,.06)" stroke-width="2"/>

        <!-- Dial Hintergrund -->
        <circle cx="500" cy="500" r="420" fill="url(#dialGrad)"/>

        <!-- SUNBURST: echte radialen Strahlen, langsam drehend -->
        <g id="sunburst" class="sunburst-lines" clip-path="url(#dialClip)" filter="url(#sunBlur)" transform="rotate(0 500 500)">
          <!-- Linien werden per JS gefüllt -->
          <animateTransform attributeName="transform" attributeType="XML" type="rotate" from="0 500 500" to="360 500 500" dur="90s" repeatCount="indefinite"/>
        </g>

        <!-- Indices -->
        <g id="indices"></g>

        <!-- Branding oben -->
        <text class="brand-top" x="500" y="320" text-anchor="middle">Vita Plan GmbH</text>
        <!-- Wochentag groß (ersetzt "AUTOMATIC") -->
        <text id="dayText" x="500" y="730" text-anchor="middle" class="day-text">---</text>

        <!-- Zeiger -->
        <g id="hands" filter="url(#handShadow)">
          <g id="hourHand" transform="rotate(0 500 500)">
            <rect x="498" y="300" width="4" height="220" rx="2" fill="#d4af37" transform="translate(-2,0)"/>
          </g>
          <g id="minuteHand" transform="rotate(0 500 500)">
            <rect x="496" y="230" width="8" height="290" rx="4" fill="#c9c9c9" transform="translate(-4,0)"/>
          </g>
          <g id="secondHand" transform="rotate(0 500 500)">
            <rect x="499" y="180" width="2" height="340" rx="1" fill="#e74c3c" transform="translate(-1,0)"/>
            <circle cx="500" cy="170" r="10" fill="#e74c3c"/>
          </g>
        </g>

        <!-- Zentrum -->
        <circle cx="500" cy="500" r="14" fill="#d4af37"/>

        <!-- Datumsfenster (größer und kontrastreich) bei 3 Uhr -->
        <g id="dateWindow">
          <rect x="580" y="440" width="120" height="90" rx="10" ry="10" fill="#ffffff" stroke="#0b0f17" stroke-width="3"/>
          <text id="dateText" x="640" y="485" class="date-text">15</text>
        </g>
      </svg>
    </div>
  </main>
</div>

<script>
  // ===== SUNBURST-LINIEN (echter Sonnenschliff) =====
  (function buildSunburst(){
    const g = document.getElementById('sunburst');
    const svgNS = 'http://www.w3.org/2000/svg';
    const rays = 180; // Anzahl Strahlen
    const rInner = 180; // optionaler innerer Start (leicht vom Zentrum weg)
    const rOuter = 420; // bis zum Rand des Zifferblatts
    for(let i=0;i<rays;i++){
      const a = (i/rays)*2*Math.PI;
      const x1 = 500 + rInner*Math.sin(a);
      const y1 = 500 - rInner*Math.cos(a);
      const x2 = 500 + rOuter*Math.sin(a);
      const y2 = 500 - rOuter*Math.cos(a);
      const line = document.createElementNS(svgNS,'line');
      line.setAttribute('x1',x1);
      line.setAttribute('y1',y1);
      line.setAttribute('x2',x2);
      line.setAttribute('y2',y2);
      // abwechselnd hell/dunkel für metallischen Schliff
      line.setAttribute('stroke', i%2===0 ? 'rgba(255,255,255,0.20)' : 'rgba(0,0,0,0.20)');
      line.setAttribute('stroke-width', i%2===0 ? '1' : '0.6');
      line.setAttribute('stroke-linecap','round');
      g.appendChild(line);
    }
  })();

  // ===== Indices (wie zuvor) =====
  const indices = document.getElementById('indices');
  function buildIndices(){
    indices.innerHTML='';
    for(let i=0;i<12;i++){
      const angle = (i/12)*2*Math.PI;
      const rOuter = 370;
      const rInner = 315;
      const x1 = 500 + rInner * Math.sin(angle);
      const y1 = 500 - rInner * Math.cos(angle);
      const x2 = 500 + rOuter * Math.sin(angle);
      const y2 = 500 - rOuter * Math.cos(angle);
      const line = document.createElementNS('http://www.w3.org/2000/svg','line');
      line.setAttribute('x1',x1);line.setAttribute('y1',y1);line.setAttribute('x2',x2);line.setAttribute('y2',y2);
      line.setAttribute('stroke','#e6e6e6');line.setAttribute('stroke-width',18);line.setAttribute('stroke-linecap','round');
      indices.appendChild(line);
      for(let j=1;j<5;j++){
        const a = angle + (j*(2*Math.PI)/(12*5));
        const rx1 = 500 + (rInner+24) * Math.sin(a);
        const ry1 = 500 - (rInner+24) * Math.cos(a);
        const rx2 = 500 + (rOuter-10) * Math.sin(a);
        const ry2 = 500 - (rOuter-10) * Math.cos(a);
        const tline = document.createElementNS('http://www.w3.org/2000/svg','line');
        tline.setAttribute('x1',rx1);tline.setAttribute('y1',ry1);tline.setAttribute('x2',rx2);tline.setAttribute('y2',ry2);
        tline.setAttribute('stroke','rgba(255,255,255,0.6)');tline.setAttribute('stroke-width',4);tline.setAttribute('stroke-linecap','round');
        indices.appendChild(tline);
      }
    }
  }
  buildIndices();

  // ===== Uhrwerk (smooth) + Datum + Wochentag (DE) =====
  const hourG = document.getElementById('hourHand');
  const minuteG = document.getElementById('minuteHand');
  const secondG = document.getElementById('secondHand');
  const dayText = document.getElementById('dayText');
  const dateText = document.getElementById('dateText');

  function updateHands(){
    const d = new Date();
    const ms = d.getMilliseconds();
    const s = d.getSeconds() + ms/1000;
    const m = d.getMinutes() + s/60;
    const h = (d.getHours()%12) + m/60;
    hourG.setAttribute('transform',`rotate(${h*30} 500 500)`);
    minuteG.setAttribute('transform',`rotate(${m*6} 500 500)`);
    secondG.setAttribute('transform',`rotate(${s*6} 500 500)`);

    // Datum (zweistellig) & Wochentag groß, deutsch
    dateText.textContent = d.toLocaleString('de-CH',{day:'2-digit'});
    dayText.textContent = new Intl.DateTimeFormat('de-CH',{weekday:'long'}).format(d);

    requestAnimationFrame(updateHands);
  }
  requestAnimationFrame(updateHands);
</script>
</body>
</html>
