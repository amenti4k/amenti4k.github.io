---
layout: default
title: /radio
permalink: /radio/
---

<div id="radio"></div>
<audio id="audio" preload="none"></audio>

<style>
#radio {
  max-width: 620px;
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

#radio .dim { opacity: 0.4; }
#radio .hl { opacity: 1; font-weight: bold; }
#radio .active-station { background: var(--text-color, #cdd6f4); color: var(--background-color, #1e1e2e); }
#radio .genre-active { background: var(--text-color, #cdd6f4); color: var(--background-color, #1e1e2e); }
#radio .vu-fill { opacity: 1; }
#radio .vu-empty { opacity: 0.15; }
#radio .blink { animation: radioBlink 1s step-end infinite; }
#radio .nowplaying { opacity: 0.7; }
#radio .err { opacity: 0.6; }

@keyframes radioBlink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

@media (max-width: 640px) {
  #radio { font-size: 10px; margin: 0.5rem; }
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
  let vu = [0, 0];
  let vuTimer = null;
  let searchMode = false;
  let searchQuery = '';

  const genres = ['all','ambient','jazz','electronic','classical','rock','lofi','world','funk','pop'];

  async function fetchStations(tag) {
    loading = true; error = ''; page = 0;
    render();
    try {
      let url;
      if (tag && tag !== 'all') {
        url = API + '/stations/bytag/' + encodeURIComponent(tag) + '?limit=200&order=votes&reverse=true&hidebroken=true&has_extended_info=false';
      } else {
        url = API + '/stations?limit=200&order=votes&reverse=true&hidebroken=true';
      }
      const r = await fetch(url);
      const data = await r.json();
      stations = data.filter(s => s.url_resolved && s.name).map(s => ({
        name: s.name.replace(/[\n\r\t]/g, ' ').trim().substring(0, 38),
        url: s.url_resolved,
        tags: (s.tags || '').substring(0, 30),
        country: (s.country || '').substring(0, 15),
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
        name: s.name.replace(/[\n\r\t]/g, ' ').trim().substring(0, 38),
        url: s.url_resolved,
        tags: (s.tags || '').substring(0, 30),
        country: (s.country || '').substring(0, 15),
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
    const n = current + 1 >= filtered.length ? 0 : current + 1;
    playStation(n);
  }

  function prevStation() {
    if (!filtered.length) return;
    const n = current - 1 < 0 ? filtered.length - 1 : current - 1;
    playStation(n);
  }

  function setVolume(v) {
    volume = Math.max(0, Math.min(100, v));
    audio.volume = volume / 100;
    render();
  }

  function startVU() {
    stopVU();
    function tick() {
      if (!playing) { vu = [0,0]; return; }
      vu[0] = Math.floor(3 + Math.random() * 17);
      vu[1] = Math.floor(3 + Math.random() * 17);
      render();
      vuTimer = setTimeout(tick, 120);
    }
    tick();
  }

  function stopVU() {
    clearTimeout(vuTimer);
    vu = [0, 0];
  }

  function pad(s, n) { s = String(s); while (s.length < n) s += ' '; return s.substring(0, n); }
  function padL(s, n) { s = String(s); while (s.length < n) s = ' ' + s; return s.substring(0, n); }

  function vuBar(level, width) {
    let bar = '';
    for (let i = 0; i < width; i++) {
      if (i < level) bar += '<span class="vu-fill">█</span>';
      else bar += '<span class="vu-empty">░</span>';
    }
    return bar;
  }

  function span(cls, text, onclick) {
    const esc = text.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');
    if (onclick) {
      return '<span class="' + cls + '" data-action="' + onclick + '">' + esc + '</span>';
    }
    return '<span class="' + cls + '">' + esc + '</span>';
  }

  function render() {
    const W = 56;
    const line = (c) => c.repeat(W);
    const border = (l, fill, r) => l + fill.repeat(W - 2) + r;
    let out = '';

    // top border
    out += '╔' + '═'.repeat(W-2) + '╗\n';

    // title
    const title = 'S W I T C H B O A R D    R A D I O';
    const tpad = Math.floor((W - 2 - title.length) / 2);
    out += '║' + ' '.repeat(tpad) + title + ' '.repeat(W - 2 - tpad - title.length) + '║\n';
    out += '╠' + '═'.repeat(W-2) + '╣\n';

    // VU meters
    const vuW = 20;
    const vuL = playing ? Math.floor(vu[0] * vuW / 20) : 0;
    const vuR = playing ? Math.floor(vu[1] * vuW / 20) : 0;
    out += '║ L ' + vuBar(vuL, vuW) + '  R ' + vuBar(vuR, vuW) + '       ║\n';

    // now playing
    out += '║' + '─'.repeat(W-2) + '║\n';
    if (current >= 0 && current < filtered.length) {
      const s = filtered[current];
      const status = playing ? '<span class="blink">▶</span> NOW PLAYING' : '■ STOPPED';
      const statusPlain = playing ? '▶ NOW PLAYING' : '■ STOPPED';
      const sLine = ' ' + status + ' '.repeat(W - 2 - 1 - statusPlain.length);
      out += '║' + sLine + '║\n';
      out += '║ ' + span('hl', pad(s.name, W - 4)) + ' ║\n';
      const meta = s.tags ? s.tags : s.country;
      out += '║ <span class="nowplaying">' + pad(meta, W - 4).replace(/&/g,'&amp;').replace(/</g,'&lt;') + '</span> ║\n';
      const info = s.codec + ' ' + (s.bitrate > 0 ? s.bitrate + 'kbps' : '') + '   votes: ' + s.votes;
      out += '║ <span class="dim">' + pad(info, W - 4).replace(/&/g,'&amp;').replace(/</g,'&lt;') + '</span> ║\n';
    } else {
      out += '║ ' + pad('no station selected', W - 4) + ' ║\n';
      out += '║ ' + pad('pick one below or press [p] to play', W - 4) + ' ║\n';
      out += '║ ' + ' '.repeat(W - 4) + ' ║\n';
      out += '║ ' + ' '.repeat(W - 4) + ' ║\n';
    }

    // controls
    out += '║' + '─'.repeat(W-2) + '║\n';
    const prevTxt = ' [◄ prev] ';
    const playTxt = playing ? ' [■ stop] ' : ' [▶ play] ';
    const nextTxt = ' [next ►] ';
    const volDn = ' [-] ';
    const volUp = ' [+] ';
    const volTxt = 'vol:' + padL(volume, 3);
    const ctrlLine =
      span('click', prevTxt, 'prev') + ' ' +
      span('click', playTxt, 'toggle') + ' ' +
      span('click', nextTxt, 'next') +
      '  ' + span('click', volDn, 'vdn') +
      volTxt +
      span('click', volUp, 'vup');
    out += '║' + ctrlLine + ' '.repeat(Math.max(0, W - 2 - prevTxt.length - 1 - playTxt.length - 1 - nextTxt.length - 2 - volDn.length - volTxt.length - volUp.length)) + '║\n';

    // genre tabs
    out += '║' + '─'.repeat(W-2) + '║\n';
    let genreLine = ' ';
    genres.forEach(g => {
      const label = ' ' + g + ' ';
      if (g === genre) {
        genreLine += '<span class="genre-active click" data-action="genre:' + g + '">' + label.replace(/&/g,'&amp;').replace(/</g,'&lt;') + '</span>';
      } else {
        genreLine += span('click dim', label, 'genre:' + g);
      }
    });
    out += '║' + genreLine + '\n';

    // search
    out += '║' + '─'.repeat(W-2) + '║\n';
    const srchLabel = ' search: ';
    const srchDisp = searchMode
      ? srchLabel + searchQuery + '<span class="blink">_</span>' + ' '.repeat(Math.max(0, W - 2 - srchLabel.length - searchQuery.length - 1 - 9)) + span('click', ' [clear] ', 'searchclear')
      : srchLabel + span('click dim', '[type / to search]', 'searchstart') + ' '.repeat(Math.max(0, W - 2 - srchLabel.length - 19));
    out += '║' + srchDisp + '║\n';

    // station list header
    out += '║' + '─'.repeat(W-2) + '║\n';
    const hdr = ' ' + pad('#', 3) + pad('STATION', 30) + pad('COUNTRY', 16) + ' ';
    out += '║<span class="dim">' + hdr.replace(/&/g,'&amp;').replace(/</g,'&lt;') + '</span>║\n';
    out += '║' + '─'.repeat(W-2) + '║\n';

    if (loading) {
      out += '║ <span class="blink">loading stations...</span>' + ' '.repeat(W - 22) + '║\n';
      for (let i = 0; i < PAGE_SIZE - 1; i++) out += '║' + ' '.repeat(W-2) + '║\n';
    } else if (error) {
      out += '║ <span class="err">' + pad(error, W - 4).replace(/&/g,'&amp;').replace(/</g,'&lt;') + '</span> ║\n';
      for (let i = 0; i < PAGE_SIZE - 1; i++) out += '║' + ' '.repeat(W-2) + '║\n';
    } else if (filtered.length === 0) {
      out += '║ ' + pad('no stations found', W - 4) + ' ║\n';
      for (let i = 0; i < PAGE_SIZE - 1; i++) out += '║' + ' '.repeat(W-2) + '║\n';
    } else {
      const start = page * PAGE_SIZE;
      const end = Math.min(start + PAGE_SIZE, filtered.length);
      for (let i = start; i < end; i++) {
        const s = filtered[i];
        const num = pad(i + 1, 3);
        const name = pad(s.name, 30);
        const country = pad(s.country, 16);
        const row = ' ' + num + name + country + ' ';
        const cls = (i === current) ? 'active-station click' : 'click';
        out += '║' + span(cls, row, 'play:' + i) + '║\n';
      }
      for (let i = end - start; i < PAGE_SIZE; i++) out += '║' + ' '.repeat(W-2) + '║\n';
    }

    // pagination
    out += '║' + '─'.repeat(W-2) + '║\n';
    const totalPages = Math.max(1, Math.ceil(filtered.length / PAGE_SIZE));
    const pageInfo = 'page ' + (page + 1) + '/' + totalPages + '  (' + filtered.length + ' stations)';
    const prevP = page > 0 ? span('click', ' [◄ prev page] ', 'pprev') : '<span class="dim"> [◄ prev page] </span>';
    const nextP = page < totalPages - 1 ? span('click', ' [next page ►] ', 'pnext') : '<span class="dim"> [next page ►] </span>';
    out += '║ ' + prevP + ' ' + pageInfo + ' ' + nextP + ' '.repeat(Math.max(0, W - 4 - 16 - 1 - pageInfo.length - 1 - 16)) + '║\n';

    // bottom
    out += '╠' + '═'.repeat(W-2) + '╣\n';
    const help = 'keys: [p]lay  [←][→] prev/next  [/]search  [-][+]vol';
    const hPad = Math.floor((W - 2 - help.length) / 2);
    out += '║<span class="dim">' + ' '.repeat(hPad) + help.replace(/&/g,'&amp;').replace(/</g,'&lt;') + ' '.repeat(W - 2 - hPad - help.length) + '</span>║\n';
    out += '╚' + '═'.repeat(W-2) + '╝\n';

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
    else if (a === 'vdn') setVolume(volume - 10);
    else if (a === 'vup') setVolume(volume + 10);
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
      if (e.key === 'Backspace') { searchQuery = searchQuery.slice(0, -1); render(); return; }
      if (e.key === 'Enter') {
        if (searchQuery.length > 0) { searchStations(searchQuery); }
        return;
      }
      if (e.key.length === 1 && !e.ctrlKey && !e.metaKey) {
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
    else if (e.key === '-' || e.key === '_') { setVolume(volume - 10); }
    else if (e.key === '=' || e.key === '+') { setVolume(volume + 10); }
  });

  audio.addEventListener('error', function() {
    error = 'stream error - try another station';
    playing = false;
    stopVU();
    render();
  });

  // boot
  fetchStations('all');
})();
</script>
