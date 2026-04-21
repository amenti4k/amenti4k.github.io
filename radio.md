---
layout: default
title: /radio
permalink: /radio/
---

<div id="radio"></div>
<audio id="aud" preload="none"></audio>

<div id="radio-footer">
<pre>
   ╭─────────────────────────────────────────────────────────────╮
   │                                                             │
   │     transmitting from addis ababa to everywhere else        │
   │     ከአዲስ አበባ ወደ ሌላ ሁሉ ቦታ                                │
   │                                                             │
   ╰─────────────────────────────────────────────────────────────╯
</pre>
</div>

<style>
#radio {
  max-width: 800px;
  margin: 0 auto;
  font-family: 'JetBrains Mono', 'Inconsolata', 'Courier New', monospace;
  font-size: 13px;
  line-height: 1.4;
  white-space: pre;
  overflow-x: auto;
  cursor: default;
  -webkit-user-select: none;
  user-select: none;
}
#radio .c { cursor: pointer; }
#radio .c:hover { background: var(--text-color, #cdd6f4); color: var(--background-color, #1e1e2e); }
#radio .d { opacity: 0.3; }
#radio .m { opacity: 0.5; }
#radio .h { font-weight: bold; }
#radio .s { background: var(--text-color, #cdd6f4); color: var(--background-color, #1e1e2e); }
#radio .von { opacity: 1; }
#radio .voff { opacity: 0.1; }
#radio .np { opacity: 0.55; }
#radio .bk { animation: bk 1s step-end infinite; }
#radio .w1 { animation: wv 1.5s ease-in-out infinite; }
#radio .w2 { animation: wv 1.5s ease-in-out 0.3s infinite; }
#radio .w3 { animation: wv 1.5s ease-in-out 0.6s infinite; }
#radio .glow { animation: gl 3s ease-in-out infinite; }
@keyframes bk { 0%,100%{opacity:1} 50%{opacity:0} }
@keyframes wv { 0%,100%{opacity:0.12} 50%{opacity:0.85} }
@keyframes gl { 0%,100%{opacity:0.3} 50%{opacity:0.7} }
@media (max-width: 740px) { #radio { font-size: 10px; margin: 0.5rem; } }
@media (max-width: 500px) { #radio { font-size: 8px; } }

#radio-footer {
  max-width: 800px;
  margin: 1.5rem auto 2rem;
  font-family: 'JetBrains Mono', 'Inconsolata', 'Courier New', monospace;
  font-size: 12px;
  opacity: 0.4;
  text-align: center;
}
#radio-footer pre {
  margin: 0;
  white-space: pre;
  overflow-x: auto;
  line-height: 1.4;
}
#radio-footer a {
  color: inherit;
  text-decoration: underline;
}
#radio-footer:hover { opacity: 0.7; }
@media (max-width: 740px) { #radio-footer { font-size: 9px; } }
</style>

<script>
(function() {
  var R = document.getElementById('radio');
  var A = document.getElementById('aud');
  if (!R || !A) return;

  var W = 76;
  var I = W - 2;
  var stations = [], allStations = [];
  var cur = -1, on = false, connecting = false, vol = 70;
  var loading = true, err = '';
  var genre = 'all', pg = 0, PS = 8;
  var vu = [0,0,0,0,0,0,0,0,0,0];
  var vuT = null, srch = false, sq = '';
  var playGen = 0;
  var genres = ['all','music','public radio','african music','religious'];

  function p(s,n) { s=String(s); while(s.length<n) s+=' '; return s.slice(0,n); }
  function pC(s,n) { s=String(s); var l=Math.floor((n-s.length)/2); return ' '.repeat(Math.max(0,l))+s+' '.repeat(Math.max(0,n-l-s.length)); }
  function x(t) { return String(t).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

  function ln(html, plainLen) {
    return '║' + html + ' '.repeat(Math.max(0, I - plainLen)) + '║\n';
  }
  function lnC(text) { return '║' + pC(text, I) + '║\n'; }
  function lnE() { return '║' + ' '.repeat(I) + '║\n'; }
  function sep() { return '║' + '─'.repeat(I) + '║\n'; }
  function dsep() { return '╠' + '═'.repeat(I) + '╣\n'; }
  function span(cls,txt,act) {
    var e = x(txt);
    return act ? '<span class="'+cls+'" data-action="'+act+'">'+e+'</span>' : '<span class="'+cls+'">'+e+'</span>';
  }

  function draw() {
    try {
      var o = '';

      if (on) {
        o += '                                <span class="w3">·411·</span>\n';
        o += '                            <span class="w2">·411·</span>   <span class="w1">·411·</span>\n';
        o += '                               <span class="bk">│</span>\n';
        o += '                          ╭────┤ <span class="w1">ON AIR</span> ├────╮\n';
      } else {
        o += '\n\n';
        o += '                               <span class="d">│</span>\n';
        o += '                          <span class="d">╭────┤ OFF AIR ├────╮</span>\n';
      }

      o += '╔' + '═'.repeat(I) + '╗\n';
      o += lnE();
      o += lnC('E T H I O P I A N    R A D I O');
      o += lnC('የኢትዮጵያ ሬዲዮ');
      o += lnE();

      o += dsep();
      o += ln('  <span class="m">EQUALIZER</span>                              <span class="m">SIGNAL</span>', I);
      o += lnE();

      var eqH = 7;
      var tower = [
        on ? '      <span class="w1">)</span>   ' : '          ',
        on ? '     <span class="w2">)</span>    ' : '          ',
        on ? '    <span class="w3">)</span>     ' : '          ',
        '    ╻     ',
        '    ║     ',
        '   ╱║╲    ',
        '  ╱─║─╲   ',
      ];

      for (var row = eqH; row >= 1; row--) {
        var eq = '  ';
        for (var c = 0; c < 10; c++) {
          if (vu[c] >= row) {
            if (row >= 6) eq += '<span class="von">██</span>';
            else if (row >= 4) eq += '<span class="von">▓▓</span>';
            else eq += '<span class="von">░░</span>';
          } else {
            eq += '<span class="voff">░░</span>';
          }
          if (c < 9) eq += ' ';
        }
        eq += '  ';
        var ri = eqH - row;
        var tw = tower[ri] || '          ';
        o += ln(' ' + eq + '        ' + tw, 52);
      }

      o += lnE();

      o += dsep();
      var npW = I - 4;

      if (cur >= 0 && cur < stations.length) {
        var s = stations[cur];
        var stTxt, stHtml, stHtmlLen;
        if (connecting) {
          stTxt = 'CONNECTING...';
          stHtml = '<span class="bk">◉</span> ' + stTxt;
          stHtmlLen = stTxt.length + 2;
        } else if (on) {
          stTxt = 'NOW PLAYING';
          stHtml = '<span class="bk">▶</span> ' + stTxt;
          stHtmlLen = stTxt.length + 2;
        } else {
          stTxt = 'PAUSED';
          stHtml = '■ ' + stTxt;
          stHtmlLen = stTxt.length + 2;
        }
        o += ln('  ' + stHtml + p('', npW - stHtmlLen), I);
        o += ln('  <span class="h">' + x(p(s.name, npW)) + '</span>', I);
        var meta = s.tags || s.country || '';
        o += ln('  <span class="np">' + x(p(meta, npW)) + '</span>', I);
        var inf = (s.codec||'') + (s.bitrate > 0 ? ' '+s.bitrate+'kbps':'') + '  ♥ ' + s.votes;
        o += ln('  <span class="d">' + x(p(inf, npW)) + '</span>', I);
      } else {
        o += lnE();
        o += ln('  select a station below...', I);
        o += ln('  press [p] to play or click a row', I);
        o += lnE();
      }

      o += sep();
      var vb = Math.round(vol / 5);
      var playLbl = connecting ? ' WAIT ' : on ? ' STOP ' : ' PLAY ';
      var ctrlHtml = '   ' +
        span('c',' |<< ','prev') + '  ' +
        span('c', playLbl, 'toggle') + '  ' +
        span('c',' >>| ','next') +
        '      ' +
        span('c',' - ','vdn') +
        ' vol ' + '█'.repeat(vb) + '░'.repeat(20 - vb) +
        span('c',' + ','vup');
      o += ln(ctrlHtml, 62);

      o += dsep();
      o += ln('  <span class="m">FILTER</span>', I);

      var gl = '  ';
      var glp = 2;
      genres.forEach(function(g) {
        var lbl = ' ' + g.toUpperCase() + ' ';
        gl += (g === genre) ? '<span class="s c" data-action="genre:'+g+'">' + x(lbl) + '</span>' : span('c d', lbl, 'genre:'+g);
        gl += '  ';
        glp += lbl.length + 2;
      });
      o += ln(gl, glp);

      o += sep();
      if (srch) {
        var ql = '  search: ' + sq;
        o += ln(ql + '<span class="bk">_</span>' + ' '.repeat(Math.max(0, I - ql.length - 1 - 10)) + span('c',' [clear] ','searchclear'), I);
      } else {
        o += ln('  search: ' + span('c d','type / to search...','searchstart'), 29);
      }

      o += dsep();
      o += ln('  <span class="m">STATIONS</span>', I);
      o += sep();

      var hdr = '  ' + p('#', 4) + p('STATION', 44) + p('COUNTRY', 20) + '  ';
      o += ln('<span class="d">' + x(hdr.slice(0, I)) + '</span>', I);
      o += sep();

      if (loading) {
        o += ln('  <span class="bk">loading stations...</span>', I);
        for (var i = 0; i < PS - 1; i++) o += lnE();
      } else if (err) {
        o += ln('  <span class="d">' + x(p(err, I - 4)) + '</span>', I);
        for (var i = 0; i < PS - 1; i++) o += lnE();
      } else if (stations.length === 0) {
        o += ln('  no stations found', I);
        for (var i = 0; i < PS - 1; i++) o += lnE();
      } else {
        var st = pg * PS;
        var en = Math.min(st + PS, stations.length);
        for (var i = st; i < en; i++) {
          var s = stations[i];
          var row = '  ' + p(i + 1, 4) + p(s.name, 44) + p(s.country, 20) + '  ';
          row = row.slice(0, I);
          var cls = (i === cur) ? 's c' : 'c';
          o += '║' + span(cls, row, 'play:' + i) + '║\n';
        }
        for (var i = en - st; i < PS; i++) o += lnE();
      }

      o += sep();
      var tp = Math.max(1, Math.ceil(stations.length / PS));
      var pi = 'page ' + (pg + 1) + '/' + tp + '  (' + stations.length + ' stations)';
      var pvT = ' [< prev] ';
      var nxT = ' [next >] ';
      var pv = pg > 0 ? span('c', pvT, 'pprev') : span('d', pvT);
      var nx = pg < tp - 1 ? span('c', nxT, 'pnext') : span('d', nxT);
      var pgPlain = '  ' + pvT + '   ' + pi + '   ' + nxT;
      o += ln('  ' + pv + '   ' + pi + '   ' + nx, pgPlain.length);

      o += dsep();
      var help = '[p] play/stop  [<][>] prev/next  [/] search  [-][+] vol  [up][dn] page';
      o += ln('<span class="d">' + pC(help, I) + '</span>', I);
      o += sep();
      o += ln('<span class="d">' + pC('radio-browser.info  ·  ethiopian radio stations', I) + '</span>', I);
      o += ln('<span class="d">' + pC('note: some free streams play a short ad before music', I) + '</span>', I);
      o += '╚' + '═'.repeat(I) + '╝\n';

      R.innerHTML = o;
    } catch(e) {
      R.textContent = 'error: ' + e.message;
    }
  }

  function fetchStations(tag) {
    loading = true; err = ''; pg = 0;
    draw();
    var url = 'https://de1.api.radio-browser.info/json/stations/bycountry/Ethiopia?limit=200&order=votes&reverse=true&hidebroken=true';
    fetch(url).then(function(r) { return r.json(); }).then(function(data) {
      allStations = data.filter(function(s) { return s.url_resolved && s.name; }).map(function(s) {
        return {
          name: s.name.replace(/[\n\r\t]/g, ' ').trim().slice(0, 42),
          url: s.url_resolved,
          tags: (s.tags || '').slice(0, 34),
          country: (s.country || '').slice(0, 18),
          codec: s.codec || '?',
          bitrate: s.bitrate || 0,
          votes: s.votes || 0
        };
      });
      if (tag && tag !== 'all') {
        stations = allStations.filter(function(s) { return s.tags.toLowerCase().indexOf(tag.toLowerCase()) >= 0; });
      } else {
        stations = allStations;
      }
      loading = false;
      draw();
    }).catch(function(e) {
      loading = false;
      err = 'fetch failed: ' + e.message;
      stations = []; allStations = [];
      draw();
    });
  }

  function searchStations(q) {
    pg = 0;
    if (!q) { stations = allStations; draw(); return; }
    stations = allStations.filter(function(s) {
      return s.name.toLowerCase().indexOf(q.toLowerCase()) >= 0 ||
             s.tags.toLowerCase().indexOf(q.toLowerCase()) >= 0;
    });
    draw();
  }

  function play(i) {
    if (i < 0 || i >= stations.length) return;
    // bump generation - any pending play callbacks from previous station are now stale
    var gen = ++playGen;
    // stop current stream fully
    A.pause();
    try { A.removeAttribute('src'); A.load(); } catch(e) {}
    stopVU();
    cur = i;
    err = '';
    on = false;
    connecting = true;
    draw();
    // assign new source
    A.src = stations[i].url;
    A.volume = vol / 100;
    // try to play
    var playPromise = A.play();
    if (playPromise && playPromise.then) {
      playPromise.then(function() {
        if (gen !== playGen) return; // stale
        connecting = false;
        on = true;
        startVU();
        draw();
      }).catch(function(e) {
        if (gen !== playGen) return; // stale
        connecting = false;
        on = false;
        err = 'playback error - try another station';
        draw();
      });
    }
  }
  function stop() {
    playGen++;
    A.pause();
    try { A.removeAttribute('src'); A.load(); } catch(e) {}
    on = false;
    connecting = false;
    stopVU();
    draw();
  }
  function toggle() {
    if (on || connecting) { stop(); }
    else if (cur >= 0) { play(cur); }
    else if (stations.length) { play(0); }
  }
  function next() { if (!stations.length) return; play((cur + 1) % stations.length); }
  function prev() { if (!stations.length) return; play((cur - 1 + stations.length) % stations.length); }
  function setVol(v) { vol = Math.max(0, Math.min(100, v)); A.volume = vol / 100; draw(); }

  function startVU() {
    stopVU();
    (function tick() {
      if (!on) { vu = [0,0,0,0,0,0,0,0,0,0]; return; }
      for (var i = 0; i < 10; i++) vu[i] = Math.floor(1 + Math.random() * 8);
      draw();
      vuT = setTimeout(tick, 110);
    })();
  }
  function stopVU() { clearTimeout(vuT); vu = [0,0,0,0,0,0,0,0,0,0]; }

  R.addEventListener('click', function(e) {
    var t = e.target.closest('[data-action]');
    if (!t) return;
    var a = t.dataset.action;
    if (a === 'prev') prev();
    else if (a === 'next') next();
    else if (a === 'toggle') toggle();
    else if (a === 'vdn') setVol(vol - 5);
    else if (a === 'vup') setVol(vol + 5);
    else if (a === 'pprev') { pg = Math.max(0, pg - 1); draw(); }
    else if (a === 'pnext') { pg = Math.min(Math.ceil(stations.length / PS) - 1, pg + 1); draw(); }
    else if (a === 'searchstart') { srch = true; sq = ''; draw(); }
    else if (a === 'searchclear') { srch = false; sq = ''; genre = 'all'; stations = allStations; draw(); }
    else if (a.indexOf('play:') === 0) play(parseInt(a.split(':')[1]));
    else if (a.indexOf('genre:') === 0) { genre = a.split(':')[1]; srch = false; sq = ''; fetchStations(genre); }
  });

  document.addEventListener('keydown', function(e) {
    if (['INPUT', 'TEXTAREA', 'SELECT'].indexOf(e.target.tagName) >= 0) return;
    if (srch) {
      if (e.key === 'Escape') { srch = false; sq = ''; draw(); return; }
      if (e.key === 'Backspace') { e.preventDefault(); sq = sq.slice(0, -1); draw(); return; }
      if (e.key === 'Enter') { if (sq.length) searchStations(sq); return; }
      if (e.key.length === 1 && !e.ctrlKey && !e.metaKey) { e.preventDefault(); sq += e.key; draw(); return; }
      return;
    }
    if (e.key === '/') { e.preventDefault(); srch = true; sq = ''; draw(); }
    else if (e.key === 'p' || e.key === ' ') { e.preventDefault(); toggle(); }
    else if (e.key === 'ArrowRight') { e.preventDefault(); next(); }
    else if (e.key === 'ArrowLeft') { e.preventDefault(); prev(); }
    else if (e.key === 'ArrowDown') { e.preventDefault(); pg = Math.min(Math.ceil(stations.length / PS) - 1, pg + 1); draw(); }
    else if (e.key === 'ArrowUp') { e.preventDefault(); pg = Math.max(0, pg - 1); draw(); }
    else if (e.key === '-' || e.key === '_') setVol(vol - 5);
    else if (e.key === '=' || e.key === '+') setVol(vol + 5);
  });

  A.addEventListener('playing', function() {
    connecting = false;
    on = true;
    err = '';
    startVU();
    draw();
  });
  A.addEventListener('waiting', function() {
    if (on) { connecting = true; draw(); }
  });
  A.addEventListener('pause', function() {
    if (on) { on = false; connecting = false; stopVU(); draw(); }
  });
  A.addEventListener('error', function() {
    connecting = false;
    on = false;
    err = 'stream error - try another station';
    stopVU();
    draw();
  });

  draw();
  fetchStations('all');
})();
</script>
