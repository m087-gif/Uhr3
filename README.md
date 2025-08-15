<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>LED Panel Uhr - Vita Plan GmbH</title>
<style>
  :root{--bg:#0b0f17;--fg:#e9edf1;--accent:#d4af37}
  html,body{width:1152px;height:576px;margin:0;background:var(--bg);overflow:hidden;font-family:ui-sans-serif,system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial}
  .card-clock{display:flex;justify-content:center;align-items:center;width:100%;height:100%}
  .clock-wrap{width:100%;max-width:576px;aspect-ratio:1}
  svg{width:100%;height:100%}
  .brand-top{font-weight:700;font-size:40px;fill:#dcdcdc}
  .day-text{font-weight:800;font-size:64px;fill:#e6e9ee;letter-spacing:1px}
  .date-text{font-weight:800;font-size:56px;fill:#000;text-anchor:middle;dominant-baseline:middle}
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

      <g id="sunburst" class="sunburst-lines" clip-path="url(#dialClip)" filter="url(#sunBlur)">
        <animateTransform attributeName="transform" attributeType="XML" type="rotate" from="0 500 500" to="360 500 500" dur="90s" repeatCount="indefinite"/>
      </g>

      <g id="indices"></g>

      <text class="brand-top" x="500" y="320" text-anchor="middle">Vita Plan GmbH</text>
      <text id="dayText" x="500" y="730" text-anchor="middle" class="day-text">---</text>

      <g id="hands" filter="url(#handShadow)">
        <g id="hourHand" transform="rotate(0 500 500)">
          <rect x="498" y="300" width="4" height="220" rx="2" fill="#d4af37" transform="translate(-2,0)"/>
        </g>
        <g id="minuteHand"
