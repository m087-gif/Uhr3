<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>LED Panel Uhr - Vita Plan GmbH</title>
<style>
  :root{--bg:#0b0f17;--fg:#e9edf1;--accent:#d4af37}
  html,body{
    width:1152px;height:256px;margin:0;background:var(--bg);overflow:hidden;
    font-family:ui-sans-serif,system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial
  }
  .card-clock{
    display:flex;justify-content:flex-end;align-items:center;width:100%;height:100%;
    padding-right:384px /* 1/3 von rechts */
  }
  .clock-wrap{width:100%;max-width:256px;aspect-ratio:1}
  svg{width:100%;height:100%}
  .brand-top{font-weight:900;font-size:60px;fill:#dcdcdc} /* Vita Plan proportional angepasst */
  .day-text{font-weight:700;font-size:40px;fill:#e6e9ee;letter-spacing:1px} /* Wochentag lesbar */
  .date-text{font-weight:700;font-size:36px;fill:#000;text-anchor:middle;dominant-baseline:middle} /* Datum größer */
  .sunburst-lines{opacity:.28}
</style>
</head>
<body>
<div class="card-clock">
  <div class="clock-wrap" aria-label="Analoge Uhr im Datejust-Stil">
    <svg viewBox="0 0 1000 1000">
      <defs>
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

      <circle cx="500" cy="500" r="480" fill="url(#bezelGrad)" stroke="#caa84d" stroke-width="8"/>
      <circle cx="500" cy="500" r="460" fill="none" stroke="rgba(255,255,255,.06)" stroke-width="2"/>
      <circle cx="500" cy="500" r="420" fill="url(#dialGrad)"/>

      <g id="sunburst" class="sunburst-lines" clip-path="url(#dialClip)" filter="url(#sunBlur)"></g>
      <g id="indices"></g>

      <text class="brand-top" x="500" y="300" text-anchor="middle">Vita Plan GmbH</text>
      <text id="dayText" x="500" y="700" text-anchor="middle" class="day-text">---</text>

      <g id="hands" filter="url(#handShadow)">
        <g id="hourHand" transform="rotate(0 500 500)"><rect x="484" y="300" width="32" height="220" rx="16" fill="#d4af37"/></g>
        <g id="minuteHand" transform="rotate(0 500 500)"><rect x="482" y="230" width="36" height="290" rx="18" fill="#c9c9c9"/></g>
        <g id="secondHand" transform="rotate(0 500 500)"><rect x="493" y="180" width="14" height="340" rx="7" fill="#e74c3c"/><circle cx="500" cy="500" r="10" fill="#e74c3c"/></g>
      </g>

      <circle cx="500" cy="500" r="14" fill="#d4af37"/>

      <g id="dateWindow">
        <rect x="590" y="445" width="80" height="50" rx="10" ry="10" fill="#ffffff" stroke="#0b0f17" stroke-width="3"/>
        <text id="dateText" x="630" y="470" class="date-text">15</text>
      </g>
    </svg>
  </div>
</div>

<script>
  const svgNS = 'http://www.w3.org/2000/svg';

  (function buildSunburst(){
    const g = document.getElementById('sunburst');
    const rays = 180; const rInner = 180, rOuter = 420;
    for(let i=0;i<rays;i++){
      const a = (i/rays)*2*Math.PI;
      const x1 = 500 + rInner*Math.sin(a), y1 = 500 - rInner*Math.cos(a);
      const x2 = 500 + rOuter*Math.sin(a), y2 = 500 - rOuter*Math.cos(a);
      const line = document.createElementNS(svgNS,'line');
      line.setAttribute('x1',x1); line.setAttribute('y1',y1);
      line.setAttribute('x2',x2); line.setAttribute('y2',y2);
      line.setAttribute('stroke', i%2===0 ? 'rgba(255,255,255,0.20)' : 'rgba(0,0,0,0.20)');
      line.setAttribute('stroke-width', i%2===0 ? '1' : '0.6');
      line.setAttribute('stroke-linecap','round'); g.appendChild(line);
    }
  })();

  const indices = document.getElementById('indices');
  function buildIndices(){
    indices.innerHTML='';
    for(let i=0;i<12;i++){
      const angle = (i/12)*2*Math.PI;
      const rOuter = 370, rInner = 315;
      const x1 = 500 + rInner*Math.sin(angle), y1 = 500 - rInner*Math.cos(angle);
      const x2 = 500 + rOuter*Math.sin(angle), y2 = 500 - rOuter*Math.cos(angle);
      const line = document.createElementNS(svgNS,'line');
      line.setAttribute('x1',x1); line.setAttribute('y1',y1);
      line.setAttribute('x2',x2); line.setAttribute('y2',y2);
      line.setAttribute('stroke','#e6e6e6'); line.setAttribute('stroke-width',18);
      line.setAttribute('stroke-linecap','round'); indices.appendChild(line);
      for(let j=1;j<5;j++){
        const a = angle + (j*(2*Math.PI)/(12*5));
        const rx1 = 500 + (rInner+24) * Math.sin(a), ry1 = 500 - (rInner+24) * Math.cos(a);
        const rx2 = 500 + (rOuter-10) * Math.sin(a), ry2 = 500 - (rOuter-10) * Math.cos(a);
        const tline = document.createElementNS(svgNS,'line');
        tline.setAttribute('x1',rx1); tline.setAttribute('y1',ry1);
        tline.setAttribute('x2',rx2); tline.setAttribute('y2',ry2);
        tline.setAttribute('stroke','rgba(255,255,255,0.6)'); tline.setAttribute('stroke-width',4);
        tline.setAttribute('stroke-linecap','round'); indices.appendChild(tline);
      }
    }
  }
  buildIndices();

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

    // Zentrierter Sekundenpunkt mittig auf Zeiger
    const secCircle = secondG.querySelector('circle');
    secCircle.setAttribute('cx', '500');
    secCircle.setAttribute('cy', '500');

    dateText.textContent = d.toLocaleString('de-CH',{day:'2-digit'});
    dayText.textContent = new Intl.DateTimeFormat('de-CH',{weekday:'long'}).format(d);
    requestAnimationFrame(updateHands);
  }
  requestAnimationFrame(updateHands);
</script>
</body>
</html>
