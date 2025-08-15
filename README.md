<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Luxus-Analoguhr · Logo · Wetter</title>
  <style>
    :root{
      --bg:#0b0f17;           /* Seitenhintergrund */
      --fg:#e9edf1;           /* Standard-Text */
      --card:#141a24;         /* Kartenhintergrund */
      --accent:#d4af37;       /* Akzent (Gold) */
      --scale:1;              /* globale Skalierung */

      /* Zifferblatt-Farben (SVG) */
      --dial-base:#0a0a0a;    /* Grundfläche */
      --dial-edge:#222;       /* Randabdunklung */
      --indices:#cfcfcf;      /* Indizes */
      --numbers:#bfbfbf;      /* Ziffern */
      --hand-hour:#d4af37;    /* Stundenzeiger */
      --hand-minute:#c9c9c9;  /* Minutenzeiger */
      --hand-second:#e74c3c;  /* Sekundenzeiger */
    }
    html,body{height:100%;margin:0;background:var(--bg);color:var(--fg);font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica Neue, Arial, "Apple Color Emoji","Segoe UI Emoji";}
    .wrap{position:fixed;inset:0;display:grid;grid-template-rows:auto 1fr auto;gap:calc(24px*var(--scale));padding:calc(28px*var(--scale));}
    header,footer{display:flex;align-items:center;justify-content:space-between;gap:16px}
    header .title{font-size:calc(26px*var(--scale));font-weight:800}
    header .subtitle{color:#9aa4af;font-size:calc(15px*var(--scale));font-weight:600}

    .grid{display:grid;grid-template-columns:1fr min(28vw,520px) 1fr;gap:calc(28px*var(--scale));align-items:stretch}
    .card{background:var(--card);border-radius:24px;box-shadow:0 10px 30px rgba(0,0,0,.35);border:1px solid rgba(255,255,255,.06);padding:calc(22px*var(--scale));display:grid;place-items:center}
    @media (max-width:1100px){.grid{grid-template-columns:1fr}}

    /* Clock container keeps square */
    .clock-wrap{width:min(60vh, 48vw);aspect-ratio:1;}
    .logo-box{display:grid;gap:12px;text-align:center;width:100%;height:100%;place-items:center}
    .logo-box img{max-width:90%;max-height:85%;object-fit:contain;filter:drop-shadow(0 4px 20px rgba(0,0,0,.45))}

    .weather{width:100%}
    .weather .now{width:100%;display:grid;grid-template-columns:auto 1fr auto;gap:10px;align-items:center}
    .wx-big{font-size:clamp(26px,3vw,46px);font-weight:800}
    .wx-muted{color:#9aa4af;font-size:clamp(12px,1.1vw,18px)}
    .wx-chip{background:rgba(255,255,255,.08);border:1px solid rgba(255,255,255,.08);padding:6px 10px;border-radius:999px;font-weight:700}
    .forecast{margin-top:16px;display:grid;grid-template-columns:repeat(4,1fr);gap:10px}
    .day{background:rgba(255,255,255,.04);border:1px solid rgba(255,255,255,.06);border-radius:16px;padding:14px;display:grid;gap:6px;text-align:center}
    .temps{font-variant-numeric:tabular-nums;font-weight:800}

    .fs-btn{background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.1);color:var(--fg);border-radius:999px;padding:8px 14px;cursor:pointer;font-weight:700}
    .fs-btn:hover{background:rgba(255,255,255,.10)}
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div>
        <div class="title" id="title">Uhr & Wetter</div>
        <div class="subtitle" id="subtitle">Analoge Luxus-Uhr (SVG) · individuell anpassbar</div>
      </div>
      <button class="fs-btn" id="fsBtn" title="Vollbild umschalten">Vollbild</button>
    </header>

    <main class="grid">
      <!-- CLOCK (SVG) -->
      <section class="card">
        <div class="clock-wrap">
          <svg id="luxClock" viewBox="0 0 1000 1000" width="100%" height="100%" aria-label="Analoge Uhr">
            <defs>
              <!-- Zifferblatt mit radialem Verlauf für Tiefe -->
              <radialGradient id="dialGrad" cx="50%" cy="50%" r="60%">
                <stop offset="0%" stop-color="var(--dial-base)"/>
                <stop offset="70%" stop-color="var(--dial-base)"/>
                <stop offset="100%" stop-color="var(--dial-edge)"/>
              </radialGradient>
              <!-- Glanz am Glas -->
              <linearGradient id="glassHighlight" x1="0" y1="0" x2="0" y2="1">
                <stop offset="0%" stop-color="rgba(255,255,255,.20)"/>
                <stop offset="40%" stop-color="rgba(255,255,255,.05)"/>
                <stop offset="100%" stop-color="rgba(255,255,255,0)"/>
              </linearGradient>
              <!-- Schatten der Zeiger -->
              <filter id="handShadow" x="-50%" y="-50%" width="200%" height="200%">
                <feDropShadow dx="0" dy="2" stdDeviation="3" flood-color="#000" flood-opacity=".45"/>
              </filter>
            </defs>

            <!-- Bezel -->
            <circle cx="500" cy="500" r="480" fill="none" stroke="var(--accent)" stroke-width="16"/>
            <circle cx="500" cy="500" r="468" fill="none" stroke="rgba(255,255,255,.08)" stroke-width="2"/>

            <!-- Dial -->
            <circle cx="500" cy="500" r="440" fill="url(#dialGrad)"/>

            <!-- Indices Container (gefüllt per JS) -->
            <g id="indices"></g>

            <!-- Marken-Logo-Position (optional Text) -->
            <text id="dialLabelTop" x="500" y="350" text-anchor="middle" fill="var(--indices)" font-weight="700" font-size="36">—</text>
            <text id="dialLabelBottom" x="500" y="680" text-anchor="middle" fill="var(--indices)" font-weight="500" font-size="24">—</text>

            <!-- Hands -->
            <g id="hands" filter="url(#handShadow)">
              <!-- Stundenzeiger -->
              <g id="hourHand" transform="rotate(0 500 500)">
                <path d="M500 520 L500 275" stroke="var(--hand-hour)" stroke-width="18" stroke-linecap="round"/>
                <circle cx="500" cy="500" r="12" fill="var(--hand-hour)"/>
              </g>
              <!-- Minutenzeiger -->
              <g id="minuteHand" transform="rotate(0 500 500)">
                <path d="M500 530 L500 190" stroke="var(--hand-minute)" stroke-width="12" stroke-linecap="round"/>
                <circle cx="500" cy="500" r="9" fill="var(--hand-minute)"/>
              </g>
              <!-- Sekundenzeiger (sweep) -->
              <g id="secondHand" transform="rotate(0 500 500)">
                <circle cx="500" cy="500" r="6" fill="var(--hand-second)"/>
                <path d="M500 540 L500 160" stroke="var(--hand-second)" stroke-width="4" stroke-linecap="round"/>
                <circle cx="500" cy="160" r="8" fill="var(--hand-second)"/>
              </g>
            </g>

            <!-- Glasreflex -->
            <ellipse cx="500" cy="380" rx="420" ry="180" fill="url(#glassHighlight)"/>
          </svg>
        </div>
      </section>

      <!-- LOGO CENTER -->
      <section class="card logo">
        <div class="logo-box">
          <img id="logo" alt="Logo" src="" onerror="this.style.display='none';document.getElementById('logoFallback').style.display='block'" />
          <div class="wx-muted" id="logoFallback" style="display:none">Logo-URL nicht gesetzt</div>
        </div>
      </section>

      <!-- WEATHER -->
      <section class="card weather">
        <div class="now">
          <div class="wx-chip" id="wxCity">—</div>
          <div>
            <div class="wx-big" id="wxTemp">--°</div>
            <div class="wx-muted" id="wxDesc">Wetter lädt…</div>
          </div>
          <div class="wx-chip" id="wxExtra">—</div>
        </div>
        <div class="forecast" id="forecast"></div>
      </section>
    </main>

    <footer>
      <div class="wx-muted">Farben & Inhalte per URL-Parameter anpassen (siehe Kommentar im Code).</div>
      <div class="wx-muted" id="updated">—</div>
    </footer>
  </div>

  <script>
    // =====================
    // URL-PARAMETER
    // Beispiel:
    // index.html?title=Nachtschicht&subtitle=Filiale&logo=https://…/logo.png&city=Zürich&lang=de
    // &bg=%230b0f17&fg=%23e9edf1&card=%23141a24&accent=%23d4af37&scale=1
    // &dialBase=%230a0a0a&dialEdge=%23222&indices=%23cfcfcf&numbers=%23bfbfbf
    // &handHour=%23d4af37&handMinute=%23c9c9c9&handSecond=%23e74c3c
    // &labelTop=CHRONOMETER&labelBottom=AUTOMATIC
    // &tz=Europe/Zurich
    // =====================
    const params = new URLSearchParams(location.search);
    const cfg = {
      title: params.get('title') ?? 'Uhr & Wetter',
      subtitle: params.get('subtitle') ?? 'Analoge Luxus-Uhr (SVG)',
      logo: params.get('logo') ?? '',
      bg: params.get('bg') ?? getComputedStyle(document.documentElement).getPropertyValue('--bg').trim(),
      fg: params.get('fg') ?? getComputedStyle(document.documentElement).getPropertyValue('--fg').trim(),
      card: params.get('card') ?? getComputedStyle(document.documentElement).getPropertyValue('--card').trim(),
      accent: params.get('accent') ?? getComputedStyle(document.documentElement).getPropertyValue('--accent').trim(),
      scale: parseFloat(params.get('scale') ?? '1'),
      dialBase: params.get('dialBase') ?? getComputedStyle(document.documentElement).getPropertyValue('--dial-base').trim(),
      dialEdge: params.get('dialEdge') ?? getComputedStyle(document.documentElement).getPropertyValue('--dial-edge').trim(),
      indices: params.get('indices') ?? getComputedStyle(document.documentElement).getPropertyValue('--indices').trim(),
      numbers: params.get('numbers') ?? getComputedStyle(document.documentElement).getPropertyValue('--numbers').trim(),
      handHour: params.get('handHour') ?? getComputedStyle(document.documentElement).getPropertyValue('--hand-hour').trim(),
      handMinute: params.get('handMinute') ?? getComputedStyle(document.documentElement).getPropertyValue('--hand-minute').trim(),
      handSecond: params.get('handSecond') ?? getComputedStyle(document.documentElement).getPropertyValue('--hand-second').trim(),
      labelTop: params.get('labelTop') ?? '—',
      labelBottom: params.get('labelBottom') ?? '—',
      tz: params.get('tz') || 'local',
      city: params.get('city') || 'Zürich',
      lang: params.get('lang') || 'de'
    };

    // Anwenden
    document.documentElement.style.setProperty('--bg', cfg.bg);
    document.documentElement.style.setProperty('--fg', cfg.fg);
    document.documentElement.style.setProperty('--card', cfg.card);
    document.documentElement.style.setProperty('--accent', cfg.accent);
    document.documentElement.style.setProperty('--scale', isFinite(cfg.scale) ? cfg.scale : 1);

    document.documentElement.style.setProperty('--dial-base', cfg.dialBase);
    document.documentElement.style.setProperty('--dial-edge', cfg.dialEdge);
    document.documentElement.style.setProperty('--indices', cfg.indices);
    document.documentElement.style.setProperty('--numbers', cfg.numbers);
    document.documentElement.style.setProperty('--hand-hour', cfg.handHour);
    document.documentElement.style.setProperty('--hand-minute', cfg.handMinute);
    document.documentElement.style.setProperty('--hand-second', cfg.handSecond);

    // Kopfbereich
    document.getElementById('title').textContent = cfg.title;
    document.getElementById('subtitle').textContent = cfg.subtitle;

    // Logo
    const logoEl = document.getElementById('logo');
    if (cfg.logo) { logoEl.src = cfg.logo; }

    // Vollbild
    document.getElementById('fsBtn').addEventListener('click', async () => {
      if (!document.fullscreenElement) await document.documentElement.requestFullscreen().catch(()=>{});
      else await document.exitFullscreen().catch(()=>{});
    });

    // ==== Indices (Ticks + Stundenbalken + Ziffern) ====
    const indices = document.getElementById('indices');
    function buildIndices(){
      indices.innerHTML = '';
      const rOuter = 440, rTick = 420, rHour = 405, rNum = 360;
      for(let i=0;i<60;i++){
        const angle = (i/60)*2*Math.PI;
        const cos = Math.cos(angle), sin = Math.sin(angle);
        const isHour = i%5===0;
        const r1 = isHour ? rHour : rTick;
        const r2 = isHour ? rTick : rOuter;
        const x1 = 500 + r1 * Math.sin(angle);
        const y1 = 500 - r1 * Math.cos(angle);
        const x2 = 500 + r2 * Math.sin(angle);
        const y2 = 500 - r2 * Math.cos(angle);
        const line = document.createElementNS('http://www.w3.org/2000/svg','line');
        line.setAttribute('x1', x1.toFixed(2));
        line.setAttribute('y1', y1.toFixed(2));
        line.setAttribute('x2', x2.toFixed(2));
        line.setAttribute('y2', y2.toFixed(2));
        line.setAttribute('stroke', cfg.indices);
        line.setAttribute('stroke-linecap','round');
        line.setAttribute('stroke-width', isHour ? '8' : '3');
        indices.appendChild(line);

        // Ziffern (12,3,6,9) und optional alle Stunden
        if(isHour){
          const hour = (i/5)||12;
          const xr = rNum; // Radius für Zahlen
          const tx = 500 + xr * Math.sin(angle);
          const ty = 500 - xr * Math.cos(angle) + 12; // optische Zentrierung
          const showAll = params.get('allNumbers') === '1';
          const wanted = showAll || [12,3,6,9].includes(hour);
          if(wanted){
            const t = document.createElementNS('http://www.w3.org/2000/svg','text');
            t.setAttribute('x', tx.toFixed(2));
            t.setAttribute('y', ty.toFixed(2));
            t.setAttribute('text-anchor','middle');
            t.setAttribute('fill', cfg.numbers);
            t.setAttribute('font-weight','700');
            t.setAttribute('font-size','56');
            t.textContent = String(hour);
            indices.appendChild(t);
          }
        }
      }
      // Label oben/unten
      const top = document.getElementById('dialLabelTop');
      const bottom = document.getElementById('dialLabelBottom');
      top.textContent = cfg.labelTop;
      bottom.textContent = cfg.labelBottom;
    }
    buildIndices();

    // ==== Uhrwerk (sweeping seconds) ====
    const hourHand = document.getElementById('hourHand');
    const minuteHand = document.getElementById('minuteHand');
    const secondHand = document.getElementById('secondHand');

    function nowInTZ(){
      if(cfg.tz==='local') return new Date();
      // Trick: toLocaleString mit timeZone und zurück in Date
      return new Date(new Date().toLocaleString('en-US', { timeZone: cfg.tz }));
    }

    function updateHands(){
      const d = nowInTZ();
      const ms = d.getMilliseconds();
      const s = d.getSeconds() + ms/1000;
      const m = d.getMinutes() + s/60;
      const h = (d.getHours()%12) + m/60;

      const sDeg = s * 6;            // 360/60
      const mDeg = m * 6;            // 360/60
      const hDeg = h * 30;           // 360/12

      hourHand.setAttribute('transform', `rotate(${hDeg} 500 500)`);
      minuteHand.setAttribute('transform', `rotate(${mDeg} 500 500)`);
      secondHand.setAttribute('transform', `rotate(${sDeg} 500 500)`);
      requestAnimationFrame(updateHands);
    }
    requestAnimationFrame(updateHands);

    // ===== Wetter (Open-Meteo) =====
    function wmoText(code, lang){
      const map={0:{de:'Klar',en:'Clear'},1:{de:'Überwiegend klar',en:'Mainly clear'},2:{de:'Teilweise bewölkt',en:'Partly cloudy'},3:{de:'Bewölkt',en:'Overcast'},45:{de:'Nebel',en:'Fog'},48:{de:'Reif-Nebel',en:'Depositing rime fog'},51:{de:'Niesel leicht',en:'Drizzle light'},53:{de:'Niesel mäßig',en:'Drizzle moderate'},55:{de:'Niesel stark',en:'Drizzle dense'},61:{de:'Regen leicht',en:'Rain light'},63:{de:'Regen',en:'Rain'},65:{de:'Regen stark',en:'Rain heavy'},66:{de:'Gefrierender Regen leicht',en:'Freezing rain light'},67:{de:'Gefrierender Regen stark',en:'Freezing rain heavy'},71:{de:'Schnee leicht',en:'Snow light'},73:{de:'Schnee',en:'Snow'},75:{de:'Schnee stark',en:'Snow heavy'},77:{de:'Schneekörner',en:'Snow grains'},80:{de:'Schauer leicht',en:'Showers light'},81:{de:'Schauer',en:'Showers'},82:{de:'Schauer stark',en:'Showers heavy'},85:{de:'Schneeschauer leicht',en:'Snow showers light'},86:{de:'Schneeschauer stark',en:'Snow showers heavy'},95:{de:'Gewitter',en:'Thunderstorm'},96:{de:'Gewitter mit Hagel',en:'Thunderstorm w/ hail'},99:{de:'Schweres Gewitter mit Hagel',en:'Severe TS w/ hail'}};
      const e=map[code]||{de:'—',en:'—'};return (lang?.startsWith('de')?e.de:e.en);
    }

    async function loadWeather(city, lang){
      try{
        const geores = await fetch(`https://geocoding-api.open-meteo.com/v1/search?name=${encodeURIComponent(city)}&count=1&language=${encodeURIComponent(lang)}&format=json`);
        const geo = await geores.json();
        if(!geo || !geo.results || !geo.results.length) throw new Error('Ort nicht gefunden');
        const { latitude, longitude, name, country } = geo.results[0];
        document.getElementById('wxCity').textContent = `${name}, ${country}`;

        const url = new URL('https://api.open-meteo.com/v1/forecast');
        url.searchParams.set('latitude', latitude);
        url.searchParams.set('longitude', longitude);
        url.searchParams.set('current_weather','true');
        url.searchParams.set('daily','weathercode,temperature_2m_max,temperature_2m_min,precipitation_probability_max');
        url.searchParams.set('timezone', cfg.tz!=='local'? cfg.tz : 'auto');
        url.searchParams.set('forecast_days','4');

        const wxres = await fetch(url.toString());
        const wx = await wxres.json();
        const updated = new Date();
        document.getElementById('updated').textContent = `Aktualisiert: ${updated.toLocaleTimeString([], { hour:'2-digit', minute:'2-digit' })}`;

        const t = Math.round(wx.current_weather.temperature);
        const code = wx.current_weather.weathercode;
        const wind = Math.round(wx.current_weather.windspeed);
        document.getElementById('wxTemp').textContent = `${t}°`;
        document.getElementById('wxDesc').textContent = wmoText(code, lang);
        document.getElementById('wxExtra').textContent = `Wind ${wind} km/h`;

        const daysEl = document.getElementById('forecast');
        daysEl.innerHTML='';
        for(let i=0;i<wx.daily.time.length;i++){
          const d = new Date(wx.daily.time[i]);
          const label = new Intl.DateTimeFormat(lang,{weekday:'short'}).format(d);
          const tmax = Math.round(wx.daily.temperature_2m_max[i]);
          const tmin = Math.round(wx.daily.temperature_2m_min[i]);
          const wcode = wx.daily.weathercode[i];
          const pp = wx.daily.precipitation_probability_max?.[i];
          const el = document.createElement('div');
          el.className='day';
          el.innerHTML = `<div class="wx-muted">${label}</div><div class="temps">${tmax}° / ${tmin}°</div><div class="wx-muted">${wmoText(wcode, lang)}${Number.isFinite(pp)?` · ${pp}%`:''}</div>`;
          daysEl.appendChild(el);
        }
      }catch(err){
        document.getElementById('wxDesc').textContent='Wetter konnte nicht geladen werden.';console.error(err);
      }
    }

    loadWeather(cfg.city, cfg.lang);
    setInterval(()=>loadWeather(cfg.city, cfg.lang), 20*60*1000);
  </script>
</body>
</html>
