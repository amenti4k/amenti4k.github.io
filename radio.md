---
layout: default
title: /radio
permalink: /radio/
---

<div id="radio"></div>
<audio id="audio" preload="none"></audio>

<style>
#radio {
  max-width: 740px;
  margin: 1rem auto;
  font-family: 'JetBrains Mono', 'Inconsolata', 'Courier New', monospace;
  font-size: 13px;
  line-height: 1.35;
  white-space: pre;
  user-select: none;
  cursor: default;
  overflow-x: auto;
}

#radio .click { cursor: pointer; }
#radio .click:hover { background: var(--text-color, #cdd6f4); color: var(--background-color, #1e1e2e); }

#radio .dim { opacity: 0.35; }
#radio .mid { opacity: 0.55; }
#radio .hl { opacity: 1; font-weight: bold; }
#radio .active-station { background: var(--text-color, #cdd6f4); color: var(--background-color, #1e1e2e); }
#radio .genre-active { background: var(--text-color, #cdd6f4); color: var(--background-color, #1e1e2e); }
#radio .vu-fill { opacity: 1; }
#radio .vu-empty { opacity: 0.12; }
#radio .blink { animation: radioBlink 1s step-end infinite; }
#radio .pulse { animation: radioPulse 2s ease-in-out infinite; }
#radio .wave { animation: radioWave 1.5s ease-in-out infinite; }
#radio .wave2 { animation: radioWave 1.5s ease-in-out 0.3s infinite; }
#radio .wave3 { animation: radioWave 1.5s ease-in-out 0.6s infinite; }
#radio .nowplaying { opacity: 0.6; }
#radio .err { opacity: 0.6; }
#radio .signal { opacity: 0.7; }

@keyframes radioBlink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}
@keyframes radioPulse {
  0%, 100% { opacity: 0.3; }
  50% { opacity: 1; }
}
@keyframes radioWave {
  0%, 100% { opacity: 0.15; }
  50% { opacity: 0.9; }
}

@media (max-width: 740px) {
  #radio { font-size: 10px; margin: 0.5rem; }
}
@media (max-width: 500px) {
  #radio { font-size: 8px; }
}
</style>

<script>
(function() {
  const API = 'https://de1.api.radio-browser.info/json';
  const el = document.getElementById('radio');
  const audio = document.getElementById('audio');

  let stations = [];
  let filtered = [];
  let current = -1;
  let playing = false;
  let volume = 70;
  let loading = true;
  let error = '';
  let genre = 'all';
  let page = 0;
  const PAGE_SIZE = 8;
  let vu = [0, 0, 0, 0, 0, 0, 0, 0];
  let vuTimer = null;
  let searchMode = false;
  let searchQuery = '';
  let tick = 0;

  const genres = ['all','ambient','jazz','electronic','classical','rock','lofi','world','funk','pop'];

  async function fetchStations(tag) {
    loading = true; error = ''; page = 0;
    render();
    try {
      let url;
      if (tag && tag !== 'all') {
        url = API + '/stations/bytag/' + encodeURIComponent(tag) + '?limit=200&order=votes&reverse=true&hidebroken=true';
      } else {
        url = API + '/stations?limit=200&order=votes&reverse=true&hidebroken=true';
      }
      const r = await fetch(url);
      const data = await r.json();
      stations = data.filter(s => s.url_resolved && s.name).map(s => ({
        name: s.name.replace(/[\n\r\t]/g, ' ').trim().substring(0, 44),
        url: s.url_resolved,
        tags: (s.tags || '').substring(0, 36),
        country: (s.country || '').substring(0, 18),
        codec: s.codec || '?',
        bitrate: s.bitrate || 0,
        votes: s.votes || 0,
      }));
      filtered = stations;
      loading = false;
    } catch(e) {
      loading = false;
      error = 'fetch failed: ' + e.message;
      stations = []; filtered = [];
    }
    render();
  }

  async function searchStations(q) {
    loading = true; error = ''; page = 0;
    render();
    try {
      const url = API + '/stations/byname/' + encodeURIComponent(q) + '?limit=200&order=votes&reverse=true&hidebroken=true';
      const r = await fetch(url);
      const data = await r.json();
      stations = data.filter(s => s.url_resolved && s.name).map(s => ({
        name: s.name.replace(/[\n\r\t]/g, ' ').trim().substring(0, 44),
        url: s.url_resolved,
        tags: (s.tags || '').substring(0, 36),
        country: (s.country || '').substring(0, 18),
        codec: s.codec || '?',
        bitrate: s.bitrate || 0,
        votes: s.votes || 0,
      }));
      filtered = stations;
      loading = false;
    } catch(e) {
      loading = false;
      error = 'search failed: ' + e.message;
      stations = []; filtered = [];
    }
    render();
  }

  function playStation(idx) {
    if (idx < 0 || idx >= filtered.length) return;
    current = idx;
    audio.src = filtered[idx].url;
    audio.volume = volume / 100;
    audio.play().then(() => {
      playing = true;
      startVU();
      render();
    }).catch(e => {
      error = 'playback error';
      render();
    });
    playing = true;
    render();
  }

  function stop() {
    audio.pause();
    audio.src = '';
    playing = false;
    stopVU();
    render();
  }

  function togglePlay() {
    if (playing) { stop(); }
    else if (current >= 0) { playStation(current); }
    else if (filtered.length) { playStation(0); }
  }

  function nextStation() {
    if (!filtered.length) return;
    playStation((current + 1) % filtered.length);
  }

  function prevStation() {
    if (!filtered.length) return;
    playStation((current - 1 + filtered.length) % filtered.length);
  }

  function setVolume(v) {
    volume = Math.max(0, Math.min(100, v));
    audio.volume = volume / 100;
    render();
  }

  function startVU() {
    stopVU();
    function frame() {
      if (!playing) { vu = [0,0,0,0,0,0,0,0]; return; }
      tick++;
      for (let i = 0; i < 8; i++) {
        vu[i] = Math.floor(1 + Math.random() * 7);
      }
      render();
      vuTimer = setTimeout(frame, 100);
    }
    frame();
  }

  function stopVU() {
    clearTimeout(vuTimer);
    vu = [0,0,0,0,0,0,0,0];
  }

  function pad(s, n) { s = String(s); while (s.length < n) s += ' '; return s.substring(0, n); }
  function padL(s, n) { s = String(s); while (s.length < n) s = ' ' + s; return s.substring(0, n); }
  function padC(s, n) {
    s = String(s);
    const left = Math.floor((n - s.length) / 2);
    return ' '.repeat(left) + s + ' '.repeat(n - left - s.length);
  }

  function esc(t) { return t.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

  function span(cls, text, action) {
    const e = esc(text);
    if (action) return '<span class="' + cls + '" data-action="' + action + '">' + e + '</span>';
    return '<span class="' + cls + '">' + e + '</span>';
  }

  // vertical VU bars (8 columns, height 7)
  function vuBlock() {
    const H = 7;
    const cols = 8;
    let rows = [];
    for (let row = H; row >= 1; row--) {
      let line = '  ';
      for (let c = 0; c < cols; c++) {
        if (vu[c] >= row) {
          if (row >= 6) line += '<span class="vu-fill">██</span>';
          else if (row >= 4) line += '<span class="vu-fill">▓▓</span>';
          else line += '<span class="vu-fill">░░</span>';
        } else {
          line += '<span class="vu-empty">░░</span>';
        }
        if (c < cols - 1) line += ' ';
      }
      line += '  ';
      rows.push(line);
    }
    return rows;
  }

  // signal tower ASCII art
  function signalArt() {
    if (playing) {
      return [
        '       <span class="wave">)</span>  ',
        '      <span class="wave2">)</span>   ',
        '     <span class="wave3">)</span>    ',
        '    ╻      ',
        '    ║      ',
        '    ║      ',
        '   ╱║╲     ',
        '  ╱ ║ ╲    ',
      ];
    }
    return [
      '           ',
      '           ',
      '           ',
      '    ╻      ',
      '    ║      ',
      '    ║      ',
      '   ╱║╲     ',
      '  ╱ ║ ╲    ',
    ];
  }

  // speaker grill pattern
  function speakerGrill(h) {
    let rows = [];
    for (let i = 0; i < h; i++) {
      if (i % 2 === 0) rows.push('● ○ ● ○ ● ○ ●');
      else             rows.push('○ ● ○ ● ○ ● ○');
    }
    return rows;
  }

  function render() {
    const W = 68;
    const inner = W - 2;
    let out = '';

    // === ANTENNA + TITLE BLOCK ===
    const signal = signalArt();
    out += '\n';
    if (playing) {
      out += '                  <span class="wave3">              ╭─── ∿∿∿ ───╮</span>\n';
      out += '                  <span class="wave2">           ╭──┤  ON AIR   ├──╮</span>\n';
      out += '                  <span class="wave">          ╭───┤           ├───╮</span>\n';
    } else {
      out += '                  <span class="dim">              ╭───────────╮</span>\n';
      out += '                  <span class="dim">           ╭──┤  OFF AIR  ├──╮</span>\n';
      out += '                  <span class="dim">          ╭───┤           ├───╮</span>\n';
    }

    // main box top
    out += '╔' + '═'.repeat(inner) + '╗\n';

    // title area with decorative elements
    out += '║' + ' '.repeat(inner) + '║\n';
    const t1 = '███████╗██╗    ██╗██╗████████╗ ██████╗██╗  ██╗';
    const t2 = '██╔════╝██║    ██║██║╚══██╔══╝██╔════╝██║  ██║';
    const t3 = '███████╗██║ █╗ ██║██║   ██║   ██║     ███████║';
    const t4 = '╚════██║██║███╗██║██║   ██║   ██║     ██╔══██║';
    const t5 = '███████║╚███╔███╔╝██║   ██║   ╚██████╗██║  ██║';
    const t6 = '╚══════╝ ╚══╝╚══╝ ╚═╝   ╚═╝    ╚═════╝╚═╝  ╚═╝';

    // simpler title that fits
    const title = '▄▀▄ █ █ █ ▀█▀ ▄▀▀ █▄█ █▀▄ ▄▀▄ ▄▀▄ █▀▄ █▀▄';
    const sub   = '▀▄  ▀▄▀▄▀ █  ▀█  █ █ █▀█ █ █ █▀█ █▀▄ █ █';
    const sub2  = '▀▀   ▀ ▀  ▀  ▀▀  ▀ ▀ ▀▀  ▀▀  ▀ ▀ ▀ ▀ ▀▀ ';

    out += '║' + padC('R  A  D  I  O', inner) + '║\n';
    out += '║' + padC('━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━', inner) + '║\n';
    out += '║' + padC('╭─────────────────────────────────────────╮', inner) + '║\n';
    out += '║' + padC('│   S W I T C H B O A R D   R A D I O    │', inner) + '║\n';
    out += '║' + padC('╰─────────────────────────────────────────╯', inner) + '║\n';
    out += '║' + ' '.repeat(inner) + '║\n';

    // === EQUALIZER + SIGNAL TOWER SIDE BY SIDE ===
    out += '╠' + '═'.repeat(inner) + '╣\n';

    const vuRows = vuBlock();
    const sigRows = signalArt();
    // pad both to same length
    const eqLabel = '  ╔══ EQUALIZER ══╗  ';
    const sigLabel = ' ╔═ SIGNAL ═╗ ';

    out += '║ ' + span('mid', eqLabel) + '           ' + span('mid', sigLabel) + '              ║\n';

    for (let i = 0; i < 7; i++) {
      const vuLine = vuRows[i] || '                        ';
      const sigLine = (sigRows[i] || '           ');
      out += '║ ' + vuLine + '     ' + sigLine + '              ║\n';
    }
    // signal tower base
    out += '║ ' + vuRows[vuRows.length - 1] + '     ' + sigRows[7] + '              ║\n';

    // freq labels under EQ
    if (playing) {
      out += '║  <span class="dim"> 60 125 250 500 1k 2k 4k 8k</span>                                ║\n';
    } else {
      out += '║  <span class="dim"> ── ─── ─── ─── ── ── ── ──</span>                                ║\n';
    }

    // === NOW PLAYING ===
    out += '╠' + '═'.repeat(inner) + '╣\n';

    // speaker grill + now playing display side by side
    const grillL = speakerGrill(4);
    const grillR = speakerGrill(4);

    if (current >= 0 && current < filtered.length) {
      const s = filtered[current];
      const status = playing ? '<span class="blink">▶</span> NOW PLAYING' : '■ PAUSED';
      const statusPlain = playing ? '▶ NOW PLAYING' : '■ PAUSED';
      const meta = s.tags ? s.tags : s.country;
      const info = (s.codec || '') + (s.bitrate > 0 ? ' ' + s.bitrate + 'kbps' : '') + '  ♥ ' + s.votes;

      out += '║ <span class="dim">' + esc(grillL[0]) + '</span>  ' + status + ' '.repeat(inner - 2 - 15 - 1 - statusPlain.length - 15 - 2) + '  <span class="dim">' + esc(grillR[0]) + '</span> ║\n';
      out += '║ <span class="dim">' + esc(grillL[1]) + '</span>  ' + span('hl', pad(s.name, inner - 2 - 15 - 1 - 15 - 2)) + '  <span class="dim">' + esc(grillR[1]) + '</span> ║\n';
      out += '║ <span class="dim">' + esc(grillL[2]) + '</span>  <span class="nowplaying">' + esc(pad(meta, inner - 2 - 15 - 1 - 15 - 2)) + '</span>  <span class="dim">' + esc(grillR[2]) + '</span> ║\n';
      out += '║ <span class="dim">' + esc(grillL[3]) + '</span>  <span class="dim">' + esc(pad(info, inner - 2 - 15 - 1 - 15 - 2)) + '</span>  <span class="dim">' + esc(grillR[3]) + '</span> ║\n';
    } else {
      out += '║ <span class="dim">' + esc(grillL[0]) + '</span>  ' + pad('', inner - 2 - 15 - 1 - 15 - 2) + '  <span class="dim">' + esc(grillR[0]) + '</span> ║\n';
      out += '║ <span class="dim">' + esc(grillL[1]) + '</span>  ' + pad('select a station below...', inner - 2 - 15 - 1 - 15 - 2) + '  <span class="dim">' + esc(grillR[1]) + '</span> ║\n';
      out += '║ <span class="dim">' + esc(grillL[2]) + '</span>  ' + pad('press [p] to play or click a row', inner - 2 - 15 - 1 - 15 - 2) + '  <span class="dim">' + esc(grillR[2]) + '</span> ║\n';
      out += '║ <span class="dim">' + esc(grillL[3]) + '</span>  ' + pad('', inner - 2 - 15 - 1 - 15 - 2) + '  <span class="dim">' + esc(grillR[3]) + '</span> ║\n';
    }

    // === TRANSPORT CONTROLS ===
    out += '║' + '─'.repeat(inner) + '║\n';
    const ctrl = '    ' +
      span('click', ' ◄◄ ', 'prev') + '   ' +
      span('click', playing ? ' ■ STOP ' : ' ▶ PLAY ', 'toggle') + '   ' +
      span('click', ' ►► ', 'next') +
      '          ' +
      span('click', ' ─ ', 'vdn') + ' VOL ' +
      '▕' + '█'.repeat(Math.round(volume/5)) + '░'.repeat(20 - Math.round(volume/5)) + '▏' +
      span('click', ' + ', 'vup') +
      '  ';
    out += '║' + ctrl + '║\n';

    // === GENRE SELECTOR - TWO ROWS ===
    out += '╠' + '═'.repeat(inner) + '╣\n';
    out += '║ <span class="mid">GENRE:</span>                                                            ║\n';

    const row1 = genres.slice(0, 5);
    const row2 = genres.slice(5);

    let g1 = ' ';
    row1.forEach(g => {
      const label = '  ' + g.toUpperCase() + '  ';
      if (g === genre) g1 += '<span class="genre-active click" data-action="genre:' + g + '">' + esc(label) + '</span>  ';
      else g1 += span('click dim', label, 'genre:' + g) + '  ';
    });
    // pad to inner width (approximate, since spans don't count)
    const g1plain = ' ' + row1.map(g => '  ' + g.toUpperCase() + '  ').join('  ') + '  ';
    out += '║' + g1 + ' '.repeat(Math.max(0, inner - g1plain.length)) + '║\n';

    let g2 = ' ';
    row2.forEach(g => {
      const label = '  ' + g.toUpperCase() + '  ';
      if (g === genre) g2 += '<span class="genre-active click" data-action="genre:' + g + '">' + esc(label) + '</span>  ';
      else g2 += span('click dim', label, 'genre:' + g) + '  ';
    });
    const g2plain = ' ' + row2.map(g => '  ' + g.toUpperCase() + '  ').join('  ') + '  ';
    out += '║' + g2 + ' '.repeat(Math.max(0, inner - g2plain.length)) + '║\n';

    // === SEARCH ===
    out += '║' + '─'.repeat(inner) + '║\n';
    const srchLabel = ' ⌕ SEARCH: ';
    if (searchMode) {
      const qDisp = searchQuery + '<span class="blink">_</span>';
      const clearBtn = span('click', ' [✕ CLEAR] ', 'searchclear');
      const plainLen = srchLabel.length + searchQuery.length + 1 + 11;
      out += '║' + srchLabel + qDisp + ' '.repeat(Math.max(0, inner - plainLen)) + clearBtn + '║\n';
    } else {
      const hint = span('click dim', 'type / to search stations...', 'searchstart');
      out += '║' + srchLabel + hint + ' '.repeat(Math.max(0, inner - srchLabel.length - 28)) + '║\n';
    }

    // === STATION LIST ===
    out += '╠' + '═'.repeat(inner) + '╣\n';
    const hdr = '  #   STATION                                     COUNTRY           ';
    out += '║<span class="dim">' + hdr.substring(0, inner) + '</span>║\n';
    out += '║' + '─'.repeat(inner) + '║\n';

    if (loading) {
      out += '║  <span class="blink">░░░ loading stations from radio-browser.info ░░░</span>' + ' '.repeat(Math.max(0, inner - 51)) + '║\n';
      for (let i = 0; i < PAGE_SIZE - 1; i++) out += '║' + ' '.repeat(inner) + '║\n';
    } else if (error) {
      out += '║  <span class="err">' + esc(pad(error, inner - 4)) + '</span>  ║\n';
      for (let i = 0; i < PAGE_SIZE - 1; i++) out += '║' + ' '.repeat(inner) + '║\n';
    } else if (filtered.length === 0) {
      out += '║  ' + pad('no stations found', inner - 4) + '  ║\n';
      for (let i = 0; i < PAGE_SIZE - 1; i++) out += '║' + ' '.repeat(inner) + '║\n';
    } else {
      const start = page * PAGE_SIZE;
      const end = Math.min(start + PAGE_SIZE, filtered.length);
      for (let i = start; i < end; i++) {
        const s = filtered[i];
        const num = padL(i + 1, 3);
        const name = pad(s.name, 44);
        const country = pad(s.country, 18);
        const row = '  ' + num + '  ' + name + ' ' + country;
        const cls = (i === current) ? 'active-station click' : 'click';
        out += '║' + span(cls, row.substring(0, inner), 'play:' + i) + '║\n';
      }
      for (let i = end - start; i < PAGE_SIZE; i++) out += '║' + ' '.repeat(inner) + '║\n';
    }

    // === PAGINATION ===
    out += '║' + '─'.repeat(inner) + '║\n';
    const totalPages = Math.max(1, Math.ceil(filtered.length / PAGE_SIZE));
    const pageInfo = 'page ' + (page + 1) + '/' + totalPages + '  (' + filtered.length + ' stations)';
    const prevP = page > 0 ? span('click', ' [◄ PREV] ', 'pprev') : span('dim', ' [◄ PREV] ');
    const nextP = page < totalPages - 1 ? span('click', ' [NEXT ►] ', 'pnext') : span('dim', ' [NEXT ►] ');
    const pagePlain = '  ' + ' [◄ PREV] ' + '   ' + pageInfo + '   ' + ' [NEXT ►] ';
    out += '║  ' + prevP + '   ' + pageInfo + '   ' + nextP + ' '.repeat(Math.max(0, inner - pagePlain.length)) + '║\n';

    // === FOOTER ===
    out += '╠' + '═'.repeat(inner) + '╣\n';
    const helpLine = '[p] play/stop   [←][→] prev/next   [/] search   [-][+] volume   [↑][↓] page';
    out += '║<span class="dim">' + padC(helpLine, inner) + '</span>║\n';
    out += '╠' + '═'.repeat(inner) + '╣\n';

    // decorative bottom
    out += '║<span class="dim">' + padC('powered by radio-browser.info  ·  thousands of stations worldwide', inner) + '</span>║\n';
    out += '╚' + '═'.repeat(inner) + '╝\n';

    el.innerHTML = out;
  }

  // click handler
  el.addEventListener('click', function(e) {
    const t = e.target.closest('[data-action]');
    if (!t) return;
    const a = t.dataset.action;
    if (a === 'prev') prevStation();
    else if (a === 'next') nextStation();
    else if (a === 'toggle') togglePlay();
    else if (a === 'vdn') setVolume(volume - 5);
    else if (a === 'vup') setVolume(volume + 5);
    else if (a === 'pprev') { page = Math.max(0, page - 1); render(); }
    else if (a === 'pnext') { page = Math.min(Math.ceil(filtered.length / PAGE_SIZE) - 1, page + 1); render(); }
    else if (a === 'searchstart') { searchMode = true; searchQuery = ''; render(); }
    else if (a === 'searchclear') { searchMode = false; searchQuery = ''; genre = 'all'; fetchStations('all'); }
    else if (a.startsWith('play:')) { playStation(parseInt(a.split(':')[1])); }
    else if (a.startsWith('genre:')) {
      genre = a.split(':')[1];
      searchMode = false; searchQuery = '';
      fetchStations(genre);
    }
  });

  // keyboard handler
  document.addEventListener('keydown', function(e) {
    if (['INPUT', 'TEXTAREA', 'SELECT'].includes(e.target.tagName)) return;
    if (e.target.isContentEditable) return;

    if (searchMode) {
      if (e.key === 'Escape') { searchMode = false; searchQuery = ''; render(); return; }
      if (e.key === 'Backspace') { e.preventDefault(); searchQuery = searchQuery.slice(0, -1); render(); return; }
      if (e.key === 'Enter') {
        if (searchQuery.length > 0) { searchStations(searchQuery); }
        return;
      }
      if (e.key.length === 1 && !e.ctrlKey && !e.metaKey) {
        e.preventDefault();
        searchQuery += e.key;
        render();
        return;
      }
      return;
    }

    if (e.key === '/') { e.preventDefault(); searchMode = true; searchQuery = ''; render(); }
    else if (e.key === 'p' || e.key === ' ') { e.preventDefault(); togglePlay(); }
    else if (e.key === 'ArrowRight') { e.preventDefault(); nextStation(); }
    else if (e.key === 'ArrowLeft') { e.preventDefault(); prevStation(); }
    else if (e.key === 'ArrowDown') { e.preventDefault(); page = Math.min(Math.ceil(filtered.length / PAGE_SIZE) - 1, page + 1); render(); }
    else if (e.key === 'ArrowUp') { e.preventDefault(); page = Math.max(0, page - 1); render(); }
    else if (e.key === '-' || e.key === '_') { setVolume(volume - 5); }
    else if (e.key === '=' || e.key === '+') { setVolume(volume + 5); }
  });

  audio.addEventListener('error', function() {
    error = 'stream error — try another station';
    playing = false;
    stopVU();
    render();
  });

  fetchStations('all');
})();
</script>
