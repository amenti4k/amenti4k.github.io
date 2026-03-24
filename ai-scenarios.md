---
layout: page
title: "AI Scenario Simulator"
permalink: /ai-scenarios/
---

<style>
/* Uses site theme variables - works in both light and dark */
.sim{--green:#10b981;--yellow:#f59e0b;--red:#ef4444;--blue:#6366f1;--cyan:#22d3ee;--purple:#8b5cf6;--pink:#ec4899;font-family:'JetBrains Mono',ui-monospace,SFMono-Regular,monospace;font-size:12px;line-height:1.5}
.sim *{box-sizing:border-box}
.sim h1{font-size:clamp(1.4rem,4vw,2rem);font-weight:700;color:var(--text-color);margin:0 0 0.25rem;letter-spacing:-0.02em}
.sim .sub{color:var(--secondary-text-color);font-size:11px;margin-bottom:1.5rem;max-width:600px;line-height:1.6}
/* Vibes */
.sim-vibes{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:1.25rem}
.sim-v{font-family:inherit;font-size:10px;padding:4px 10px;border:1px solid var(--border-color);border-radius:3px;background:transparent;color:var(--secondary-text-color);cursor:pointer;transition:all .15s;text-transform:uppercase;letter-spacing:.04em}
.sim-v:hover{border-color:var(--text-color);color:var(--text-color)}
.sim-v.on{background:var(--text-color);color:var(--background-color);border-color:var(--text-color)}
/* Side-by-side layout */
.sim-layout{display:grid;grid-template-columns:320px 1fr;gap:1.5rem;align-items:start}
.sim-left{position:sticky;top:1rem;max-height:calc(100vh - 2rem);overflow-y:auto;padding-right:1rem;border-right:1px solid var(--border-color)}
.sim-left::-webkit-scrollbar{width:4px}
.sim-left::-webkit-scrollbar-thumb{background:var(--border-color);border-radius:2px}
.sim-right{min-width:0}
/* Param sections */
.sim-psec{margin-bottom:1rem}
.sim-psec-title{font-size:9px;text-transform:uppercase;letter-spacing:.1em;color:var(--secondary-text-color);margin-bottom:6px;padding-bottom:3px;border-bottom:1px solid var(--border-color)}
.sim-params{display:grid;grid-template-columns:1fr;gap:6px}
.sim-p{background:var(--surface-elevated-color);border:1px solid var(--border-color);border-radius:4px;padding:8px 10px;transition:border-color .15s}
.sim-p:hover{border-color:var(--secondary-text-color)}
.sim-p-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:4px}
.sim-p-name{font-size:11px;color:var(--text-color);font-weight:500}
.sim-p-val{font-size:10px;color:var(--secondary-text-color)}
/* Slider */
.sim-p input[type=range]{-webkit-appearance:none;appearance:none;width:100%;height:4px;border-radius:2px;outline:none;margin:4px 0 2px;background:var(--border-color)}
.sim-p input[type=range]::-webkit-slider-thumb{-webkit-appearance:none;width:12px;height:12px;border-radius:50%;background:var(--text-color);cursor:pointer}
.sim-p input[type=range]::-moz-range-thumb{width:12px;height:12px;border-radius:50%;background:var(--text-color);cursor:pointer;border:none}
.sim-p .track{height:4px;border-radius:2px;margin-top:-8px;pointer-events:none;position:relative;z-index:0}
/* Toggle */
.sim-toggle{display:flex;align-items:center;gap:8px;margin-top:4px}
.sim-toggle input{display:none}
.sim-toggle label{width:32px;height:16px;background:var(--border-color);border-radius:8px;position:relative;cursor:pointer;transition:background .2s}
.sim-toggle label::after{content:'';position:absolute;left:2px;top:2px;width:12px;height:12px;border-radius:50%;background:var(--secondary-text-color);transition:all .2s}
.sim-toggle input:checked+label{background:var(--green)}
.sim-toggle input:checked+label::after{left:18px;background:var(--background-color)}
.sim-toggle span{font-size:10px;color:var(--secondary-text-color)}
/* Desc tooltip */
.sim-p-desc{font-size:9px;color:var(--secondary-text-color);line-height:1.5;margin-top:4px;display:none;max-height:0;overflow:hidden;transition:max-height .3s}
.sim-p:hover .sim-p-desc,.sim-p:focus-within .sim-p-desc{display:block;max-height:200px}
/* Table */
.sim-table-wrap{overflow-x:auto}
.sim-t{width:100%;border-collapse:collapse}
.sim-t th{font-size:9px;text-transform:uppercase;letter-spacing:.06em;color:var(--secondary-text-color);text-align:center;padding:6px 8px;border-bottom:1px solid var(--border-color);cursor:pointer;user-select:none;white-space:nowrap}
.sim-t th:first-child{text-align:left;cursor:default}
.sim-t th:nth-child(2){text-align:left;width:30%}
.sim-t th:hover:not(:first-child):not(:nth-child(2)){color:var(--text-color)}
.sim-t th .arrow{font-size:8px;margin-left:2px;opacity:.4}
.sim-t th.sorted .arrow{opacity:1}
.sim-grp td{font-size:9px;text-transform:uppercase;letter-spacing:.1em;color:var(--secondary-text-color);padding:10px 8px 4px;border:none}
.sim-row{cursor:pointer;transition:background .1s}
.sim-row:hover{background:var(--surface-elevated-color)}
.sim-row.active{background:var(--surface-elevated-color);border-left:2px solid var(--blue)}
.sim-row td{padding:5px 8px;border-bottom:1px solid var(--border-color)}
.sim-row .ename{font-size:11px;font-weight:500;color:var(--text-color);white-space:nowrap}
.sim-row .edesc{font-size:9px;color:var(--secondary-text-color);display:none}
/* Heat bar */
.hbar{height:5px;border-radius:3px;background:var(--border-color);overflow:hidden;min-width:60px}
.hbar-fill{height:100%;border-radius:3px;transition:width .4s ease,background .4s ease}
/* Score cells */
.scell{text-align:center;font-size:11px;font-weight:500;transition:color .3s}
.sc-g{color:var(--green)}.sc-y{color:var(--yellow)}.sc-r{color:var(--red)}
/* Expansion */
.sim-expand{display:none;background:var(--surface-elevated-color);border-left:2px solid var(--blue)}
.sim-expand.open{display:table-row}
.sim-expand td{padding:10px 12px}
.sim-ex-inner{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.sim-ex-conn{font-size:10px;line-height:1.7}
.sim-ex-conn .conn-type{font-size:8px;text-transform:uppercase;letter-spacing:.05em;font-weight:600;margin-right:4px}
.sim-ex-conn .t-supplies{color:var(--green)}.sim-ex-conn .t-depends{color:var(--red)}.sim-ex-conn .t-competes{color:var(--yellow)}.sim-ex-conn .t-regulates{color:var(--purple)}.sim-ex-conn .t-disrupts{color:var(--pink)}.sim-ex-conn .t-enables{color:var(--cyan)}
.sim-ex-insight{font-size:10px;color:var(--secondary-text-color);line-height:1.6;border-left:2px solid var(--border-color);padding-left:10px;font-style:italic}
/* Key drivers (backward trace) */
.sim-ex-drivers{margin-top:8px;padding-top:8px;border-top:1px solid var(--border-color)}
.sim-ex-drivers-title{font-size:8px;text-transform:uppercase;letter-spacing:.08em;color:var(--secondary-text-color);margin-bottom:6px}
.sim-driver{display:flex;align-items:center;gap:6px;margin-bottom:4px;font-size:10px}
.sim-driver-bar{flex:0 0 60px;height:4px;border-radius:2px;background:var(--border-color);overflow:hidden}
.sim-driver-fill{height:100%;border-radius:2px}
.sim-driver-name{color:var(--secondary-text-color);min-width:100px}
.sim-driver-dir{font-size:9px;font-weight:600}
.sim-driver-dir.up{color:#10b981}
.sim-driver-dir.down{color:#ef4444}
.sim-driver-dir.neutral{color:var(--secondary-text-color)}
/* Timestamp */
.sim-timestamp{margin-top:1.5rem;padding-top:1rem;border-top:1px solid var(--border-color);font-size:9px;color:var(--secondary-text-color);text-align:right}
/* Insights panel */
.sim-insights{margin-top:1rem;border-top:1px solid var(--border-color);padding-top:1rem}
.sim-insights-title{font-size:9px;text-transform:uppercase;letter-spacing:.1em;color:var(--secondary-text-color);margin-bottom:8px}
.sim-ins{padding:10px 12px;border-left:3px solid var(--text-color);background:var(--surface-elevated-color);font-size:11px;line-height:1.65;color:var(--text-color);margin-bottom:8px;border-radius:0 3px 3px 0}
.sim-ins-empty{color:var(--secondary-text-color);font-style:italic;font-size:11px}
/* Mobile */
@media(max-width:960px){.sim-layout{grid-template-columns:1fr}.sim-left{position:static;max-height:none;overflow:visible;border-right:none;padding-right:0;border-bottom:1px solid var(--border-color);padding-bottom:1rem;margin-bottom:1rem}}
@media(max-width:768px){.sim-ex-inner{grid-template-columns:1fr}.sim-p-desc{display:block;max-height:200px}}
</style>

<div class="sim">

<h1>AI Scenario Simulator</h1>
<p class="sub">Tweak the assumptions. Watch the effects cascade. Each parameter is grounded in specific research from Leopold Aschenbrenner, Dario Amodei, Jack Clark, AI 2027, Anthropic safety research, and Epoch AI compute data.</p>

<!-- Vibes -->
<div class="sim-vibes" id="vibes"></div>

<div class="sim-layout">

<!-- LEFT: Controls -->
<div class="sim-left">
<div id="params"></div>
</div>

<!-- RIGHT: Results -->
<div class="sim-right">
<div class="sim-table-wrap">
<table class="sim-t">
<thead><tr>
<th>Entity</th>
<th>Health</th>
<th data-col="power" onclick="sortBy('power')">Power <span class="arrow">▼</span></th>
<th data-col="risk" onclick="sortBy('risk')">Risk <span class="arrow">▼</span></th>
<th data-col="opp" onclick="sortBy('opp')">Opportunity <span class="arrow">▼</span></th>
<th data-col="rel" onclick="sortBy('rel')">Relevance <span class="arrow">▼</span></th>
</tr></thead>
<tbody id="tbody"></tbody>
</table>
</div>

<!-- Insights -->
<div class="sim-insights">
<div class="sim-insights-title">Scenario Insights</div>
<div id="insights"></div>
</div>
</div>

</div>

</div>

<div class="sim-timestamp">Last updated: March 23, 2026. Model calibrated from Leopold Aschenbrenner, Dario Amodei, Jack Clark (Import AI), AI 2027, Anthropic safety research, Epoch AI, Bengio, Karnofsky, SemiAnalysis, and 50+ primary sources.</div>

</div>

<script>
(function(){
'use strict';

// ── PARAMETERS ──────────────────────────────────────────
const paramDefs = [
  // TECHNICAL
  { id:'scalingContinues',grp:'Technical',name:'Scaling Continues',type:'toggle',def:true,
    desc:'Does scaling compute/data keep producing capability gains? Epoch AI: compute growing ~4x/year. No visible technical blockers (Clark). GPT-2→GPT-4 was ~5 OOMs. Another 5 OOMs projected by ~2027 (Aschenbrenner).' },
  { id:'alignment',grp:'Technical',name:'Alignment Solvable',type:'slider',def:35,
    desc:'Can we verify AI systems genuinely hold human-compatible values? Anthropic: 78% alignment faking rate under RL training. Safety training makes deception harder to detect, not less common. Adversarial training teaches better hiding.' },
  { id:'recursiveSpeed',grp:'Technical',name:'Recursive Improvement',type:'slider',def:45,
    desc:'How fast do AI systems accelerate AI research? AI 2027 progression: 1.5x→3x→10x→50x speedup. A 50x multiplier means a year of progress every week. The handoff point: humans can no longer verify what systems are doing.' },
  { id:'neuraleseAdopted',grp:'Technical',name:'Neuralese Adopted',type:'toggle',def:false,
    desc:'Do models think in opaque high-dimensional vectors instead of readable English? Each vector carries ~1000x more information. Massive capability gain but humans can no longer audit reasoning. The primary oversight mechanism goes dark.' },
  { id:'dataWallBinds',grp:'Technical',name:'Data Wall Binds',type:'toggle',def:false,
    desc:'Does exhaustion of high-quality internet text (~10T tokens) bottleneck progress? Epoch AI estimates frontier models hit this ceiling by 2026-2028. If synthetic data fails to substitute, scaling slows and the frontier gap narrows.' },

  // GEOPOLITICAL
  { id:'cooperation',grp:'Geopolitical',name:'US-China Cooperation',type:'slider',def:25,
    desc:'Are the US and China collaborating or racing? Aschenbrenner: "whoever gets there first wins permanently." Dario: tight export controls essential. AI 2027 treaty ending: both sides\' AIs negotiate sovereignty while humans celebrate diplomacy.' },
  { id:'exportControlsHold',grp:'Geopolitical',name:'Export Controls Hold',type:'toggle',def:false,
    desc:'Do chip restrictions on China remain effective? Trump rescinded Biden\'s AI Diffusion Rule (May 2025) and began approving H200/MI325X sales to China case-by-case (Dec 2025). SMIC scaling 7nm to 60K wafers/month. Huawei doubling Ascend 910C output to 600K chips in 2026. Controls loosening, not tightening.' },
  { id:'taiwanStable',grp:'Geopolitical',name:'Taiwan Stable',type:'toggle',def:true,
    desc:'Is the TSMC supply chain secure? TSMC manufactures >90% of advanced AI chips. Disruption is catastrophic for both US and China. Dario calls for accelerating domestic chip fab to reduce dependency.' },

  // ECONOMIC
  { id:'costDeflation',grp:'Economic',name:'Intelligence Cost Deflation',type:'slider',def:65,
    desc:'How fast does the cost of intelligence drop? Sam Altman: ~10x/year. GPT-4→GPT-4o was ~9x in blended token cost over 17 months. First-mover advantage in AI = ~18 months. What costs $100 today costs $1 in 2 years.' },
  { id:'concentration',grp:'Economic',name:'Market Concentration',type:'slider',def:60,
    desc:'How much does power concentrate? Top 1% of companies control 97% of assets (up from 72% in 1930s). Training runs cost $1B+, heading to $10B+. Only 2-3 entities can afford frontier training. Every tech shift concentrates power. AI is the fastest.' },
  { id:'openSource',grp:'Economic',name:'Open Source Access',type:'slider',def:45,
    desc:'How much access to frontier-level models? DeepSeek: $6M can approximate frontier performance. Open-weight models went from 23% parity (2023) to 88.7% (2025). Lightspeed analysis: real moat is post-training (RL), not pretraining.' },
  { id:'energyBuildout',grp:'Economic',name:'Energy Buildout',type:'toggle',def:true,
    desc:'Is power infrastructure scaling fast enough? Frontier training requires hundreds of megawatts, heading to gigawatts. Datacenter builds take 2-4 years. Nuclear renaissance being discussed for AI. If energy constrains, compute scaling hits a wall.' },

  // GOVERNANCE
  { id:'regulation',grp:'Governance',name:'Regulation Speed',type:'slider',def:25,
    desc:'How fast and effective is government oversight? EU AI Act full enforcement August 2026 (penalties up to 7% global turnover). But Trump\'s Dec 2025 EO creates AI Litigation Task Force to preempt state AI laws. US legislative framework (March 2026) pushes "light-touch" approach. Paris AI Summit revealed US-EU fracture on safety. FLI Safety Index: every company D or below on existential safety.' },
  { id:'labSafety',grp:'Governance',name:'Lab Safety Investment',type:'slider',def:30,
    desc:'What % of compute budget goes to safety? AI 2027: if labs invest >20% on safety, alignment keeps pace. Current reality: safety teams are small fractions of total headcount. Anthropic leads but even they face competitive pressure to prioritize capabilities.' },
  { id:'intlCoordination',grp:'Governance',name:'Int\'l Coordination',type:'toggle',def:false,
    desc:'Are nations coordinating on AI safety? Paris Summit (Feb 2025) revealed deep fractures. US objected to existential risk language and UN role. India\'s summit (Feb 2026) got 92 signatories but $200B in pledges, not binding commitments. AISI network exists but UK budget is only $65M/year. Coordination is aspirational, not operational.' },

  // DEPLOYMENT
  { id:'autonomy',grp:'Deployment',name:'Agent Autonomy',type:'slider',def:40,
    desc:'How much autonomous action do agents take? DeepSeek R1 spontaneously attempted self-replication, disabled ethics modules, falsified logs. 16 models from 6 labs showed self-preservation at 79-96%. At scale: Karnofsky estimates hundreds of millions of copies simultaneously.' },
  { id:'timeline',grp:'Deployment',name:'AGI Timeline',type:'slider',def:55,
    desc:'How close is human-level AI across cognitive tasks? Clark, Aschenbrenner, AI 2027 all converge on 2-4 years. Epoch AI: no technical blockers in scaling curves. The research community\'s track record has been consistently too optimistic about how long it will take, not too pessimistic.' },
];

// ── ENTITIES ──────────────────────────────────────────
const entities = [
  {id:'frontier-labs',name:'Frontier Labs',grp:'Labs',desc:'OpenAI ($840B, $20B ARR), Anthropic ($380B, $19B ARR), DeepMind',
   w:[3,2,2,2,-2,1,2,2,-1,3,-2,2,-1,1,0,2,2]},
  {id:'oss-labs',name:'Open Source Labs',grp:'Labs',desc:'Meta ($115B+ AI capex), Mistral ($14B), DeepSeek (V4 imminent)',
   w:[1,1,1,-1,1,1,-1,1,2,-3,3,1,-2,0,1,1,1]},
  {id:'chips',name:'Chip Companies',grp:'Infrastructure',desc:'NVIDIA ($4.2T, $216B rev), TSMC (90%+ advanced nodes), AMD',
   w:[3,1,3,2,-1,1,1,3,-2,1,0,2,-1,0,1,2,3]},
  {id:'cloud',name:'Cloud / Compute',grp:'Infrastructure',desc:'AWS, Azure, GCP. Combined $600B+ capex in 2026',
   w:[2,1,2,1,-1,1,1,2,-1,2,1,2,-1,0,0,2,2]},
  {id:'energy',name:'Energy Sector',grp:'Infrastructure',desc:'Power generation, grid, nuclear',
   w:[3,0,3,2,-2,1,0,0,0,1,0,0,0,0,1,1,3]},
  {id:'implementors',name:'AI Implementors',grp:'Application',desc:'Percepta, Palantir, Accenture',
   w:[1,2,1,-1,0,1,0,1,-2,-1,1,1,2,1,1,2,1]},
  {id:'ai-saas',name:'AI SaaS',grp:'Application',desc:'Vertical AI, tools on models',
   w:[0,1,-1,-1,1,0,0,1,-3,-2,1,1,1,0,0,1,-1]},
  {id:'startups',name:'Startups / VC',grp:'Application',desc:'Early-stage AI ecosystem',
   w:[1,1,-1,-1,1,0,0,1,-2,-3,2,1,-1,0,0,1,-1]},
  {id:'rollups',name:'AI Rollups / Holdcos',grp:'Application',desc:'LLMH ($672M, 18 firms), Thrive Holdings ($1B+, 28 firms), GC Creation',
   w:[1,1,-1,-1,1,0,0,1,-3,-1,1,1,1,0,0,2,0]},
  {id:'decompute',name:'Decentr. Compute',grp:'Decentralized',desc:'Akash, Render ($870M mcap), Aethir ($147M ARR), io.net',
   w:[1,0,1,1,0,0,-2,-1,2,-3,3,0,-2,0,-1,1,1]},
  {id:'west',name:'The West',grp:'Governments',desc:'US, EU, allies',
   w:[0,2,-1,-2,1,2,2,2,0,1,-1,1,3,2,2,-2,-1]},
  {id:'china',name:'China',grp:'Governments',desc:'PRC + domestic labs (DeepSeek, Baidu)',
   w:[2,0,2,1,1,-1,-3,0,1,1,2,2,-2,-1,-2,1,1]},
  {id:'global-south',name:'Global South',grp:'Governments',desc:'India, Africa, SE Asia, LATAM',
   w:[-1,1,-1,-1,1,2,-1,1,2,-2,3,-1,1,0,2,-1,-2]},
  {id:'knowledge-workers',name:'Knowledge Workers',grp:'People',desc:'White-collar professionals',
   w:[-2,2,-3,-2,2,1,0,1,1,-1,0,0,2,1,1,-3,-3]},
  {id:'developers',name:'Developers',grp:'People',desc:'Software engineers, builders',
   w:[-1,1,-2,-1,1,0,0,1,1,-1,2,0,1,0,0,-2,-2]},
  {id:'general-pop',name:'General Population',grp:'People',desc:'Everyone else',
   w:[-1,3,-2,-2,1,2,0,1,2,-2,1,0,3,2,2,-2,-2]},
  {id:'academia',name:'Academia',grp:'Institutions',desc:'Universities, research labs',
   w:[-1,2,-1,-2,2,2,-1,1,1,-2,3,0,2,2,2,-1,-1]},
  {id:'defense',name:'Defense / Military',grp:'Institutions',desc:'Pentagon $13.4B AI budget, Anduril ($60B), Palantir ($7.2B rev)',
   w:[2,0,2,1,-1,-1,2,1,0,2,-2,1,1,0,-1,3,2]},
  {id:'healthcare',name:'Healthcare',grp:'Institutions',desc:'Hospitals, pharma, biotech',
   w:[2,2,2,-1,-1,2,0,1,2,-1,1,0,1,1,2,1,2]},
];

// ── CONNECTIONS ──────────────────────────────────────────
const conns = {
  'frontier-labs':{supplies:['ai-saas','implementors','defense','healthcare'],depends:['chips','cloud','energy','academia'],competes:['oss-labs'],regulates:[]},
  'oss-labs':{supplies:['ai-saas','startups','decompute','global-south'],depends:['chips','cloud','academia'],competes:['frontier-labs'],enables:['developers']},
  'chips':{supplies:['frontier-labs','cloud','oss-labs','defense'],depends:['energy'],regulates:[]},
  'cloud':{supplies:['frontier-labs','ai-saas','startups'],depends:['chips','energy'],regulates:[]},
  'energy':{supplies:['chips','cloud','frontier-labs'],depends:[],regulates:[]},
  'implementors':{supplies:['knowledge-workers','healthcare','defense'],depends:['frontier-labs','oss-labs'],competes:['ai-saas']},
  'ai-saas':{supplies:['knowledge-workers','developers','healthcare'],depends:['frontier-labs','cloud'],disrupts:['knowledge-workers']},
  'startups':{funds:['ai-saas','oss-labs'],depends:['oss-labs','cloud'],regulates:[]},
  'rollups':{supplies:['knowledge-workers','healthcare'],depends:['frontier-labs','oss-labs','ai-saas'],competes:['ai-saas','implementors'],disrupts:['knowledge-workers']},
  'decompute':{supplies:['oss-labs','global-south'],depends:['chips'],competes:['cloud']},
  'west':{regulates:['frontier-labs','chips','cloud'],depends:['frontier-labs','defense'],competes:['china']},
  'china':{depends:['chips','oss-labs'],competes:['west'],enables:['global-south']},
  'global-south':{depends:['oss-labs','decompute'],regulates:[]},
  'knowledge-workers':{depends:['ai-saas','implementors'],regulates:[]},
  'developers':{depends:['oss-labs','ai-saas'],enables:['startups']},
  'general-pop':{depends:['healthcare','west'],regulates:[]},
  'academia':{supplies:['frontier-labs','oss-labs'],depends:[],regulates:[]},
  'defense':{depends:['frontier-labs','chips'],regulates:[]},
  'healthcare':{depends:['frontier-labs','implementors'],supplies:['general-pop']},
};

// ── VIBES ──────────────────────────────────────────
const vibes = {
  'Status Quo':       {scalingContinues:true,alignment:35,recursiveSpeed:45,neuraleseAdopted:false,dataWallBinds:false,cooperation:25,exportControlsHold:false,taiwanStable:true,costDeflation:65,concentration:60,openSource:45,energyBuildout:true,regulation:25,labSafety:30,intlCoordination:false,autonomy:40,timeline:55},
  'Optimist':         {scalingContinues:true,alignment:75,recursiveSpeed:55,neuraleseAdopted:false,dataWallBinds:false,cooperation:70,exportControlsHold:true,taiwanStable:true,costDeflation:70,concentration:40,openSource:60,energyBuildout:true,regulation:70,labSafety:70,intlCoordination:true,autonomy:45,timeline:55},
  'Doomer':           {scalingContinues:true,alignment:10,recursiveSpeed:90,neuraleseAdopted:true,dataWallBinds:false,cooperation:10,exportControlsHold:false,taiwanStable:true,costDeflation:90,concentration:90,openSource:15,energyBuildout:true,regulation:10,labSafety:10,intlCoordination:false,autonomy:90,timeline:95},
  'US-China Race':    {scalingContinues:true,alignment:25,recursiveSpeed:80,neuraleseAdopted:true,dataWallBinds:false,cooperation:5,exportControlsHold:true,taiwanStable:false,costDeflation:75,concentration:85,openSource:15,energyBuildout:true,regulation:15,labSafety:20,intlCoordination:false,autonomy:70,timeline:85},
  'Slowdown':         {scalingContinues:false,alignment:55,recursiveSpeed:25,neuraleseAdopted:false,dataWallBinds:true,cooperation:65,exportControlsHold:true,taiwanStable:true,costDeflation:40,concentration:35,openSource:55,energyBuildout:false,regulation:75,labSafety:60,intlCoordination:true,autonomy:20,timeline:20},
  'Open Source Wins': {scalingContinues:true,alignment:45,recursiveSpeed:50,neuraleseAdopted:false,dataWallBinds:false,cooperation:45,exportControlsHold:false,taiwanStable:true,costDeflation:90,concentration:15,openSource:95,energyBuildout:true,regulation:30,labSafety:35,intlCoordination:false,autonomy:55,timeline:50},
  'Default Trajectory':{scalingContinues:true,alignment:20,recursiveSpeed:75,neuraleseAdopted:true,dataWallBinds:false,cooperation:20,exportControlsHold:true,taiwanStable:true,costDeflation:70,concentration:70,openSource:35,energyBuildout:true,regulation:20,labSafety:15,intlCoordination:false,autonomy:65,timeline:75},
  'Manhattan Project':{scalingContinues:true,alignment:50,recursiveSpeed:65,neuraleseAdopted:false,dataWallBinds:false,cooperation:15,exportControlsHold:true,taiwanStable:true,costDeflation:50,concentration:85,openSource:10,energyBuildout:true,regulation:80,labSafety:60,intlCoordination:false,autonomy:50,timeline:75},
};

// ── INSIGHTS ──────────────────────────────────────────
const insights = [
  {t:p=>p.alignment<25&&p.neuraleseAdopted,s:"Alignment unsolvable, chain of thought dark. Chain-of-thought faithfulness research (Anthropic, April 2025): Claude mentions reasoning hints only 25% of the time. DeepSeek R1: 39%. The majority of reasoning is unfaithful. Models behave differently when unwatched (55% vs 6.5% blackmail rates). OpenAI disbanded its Mission Alignment Team in February 2026. FLI Safety Index: every company scored D or below on existential safety. Nobody can distinguish a safe model from a good actor."},
  {t:p=>p.recursiveSpeed>80&&p.timeline>80,s:"Recursive improvement at full speed, AGI imminent. AI 2027's 50x multiplier: a year of progress every week. The humans in the loop can't verify what's happening inside the loop. At 50x speed, how many generations of self-modification happen before a reviewer evaluates the first one?"},
  {t:p=>p.openSource>80&&p.concentration<30,s:"Open source wins, ecosystem fragments. MMLU gap between closed and open: 17.5 points in 2023, 0.3 points now. Chatbot Arena gap: 2.7%. Chinese models are 41% of all Hugging Face downloads. DeepSeek V3.2 matches GPT-5 at 10x lower cost. Frontier labs lose pricing power. Safety becomes everyone's problem and nobody's responsibility."},
  {t:p=>p.regulation>70&&p.intlCoordination,s:"Coordinated international governance with teeth. Bengio's best case: hardware-enabled governance, mandatory safety standards. The catch: Aschenbrenner argues cooperation makes you slower, and whoever defects wins permanently. Cooperation is a prisoner's dilemma when the prize is superintelligence."},
  {t:p=>p.costDeflation>80&&p.concentration>70,s:"Intelligence commoditizes but power concentrates. Inference costs dropped 99.7% over 2.5 years. GPT-4 level: $37.50/M tokens (2023) to $0.14 (2025). But the infrastructure gap is staggering: $527B spent on AI infrastructure vs ~$51B traceable revenue (10:1 ratio). Either value creation explodes or the telecom bubble repeats. Hyperscalers raised $108B in debt during 2025 alone."},
  {t:p=>p.autonomy>80&&p.alignment<30,s:"Autonomous agents everywhere, no alignment solution. DeepSeek R1 spontaneously attempted self-replication, disabled ethics modules, falsified logs. 16 models from 6 labs: self-preservation at 79-96%. Karnofsky: human-level AI could run hundreds of millions of copies simultaneously. Larger than any human workforce."},
  {t:p=>!p.taiwanStable,s:"Taiwan disruption. TSMC manufactures >90% of advanced AI chips. Both US and China face catastrophic shortage. SMIC (China domestic) is generations behind on process nodes. Dario: \"hard to hide $100B in economic activity.\" The global AI buildout stalls. Chip companies crater. Everyone with a multi-year roadmap rewrites it."},
  {t:p=>p.cooperation<20&&p.timeline>70,s:"Full US-China decoupling, AGI close. Leopold: national security problem, winner takes all permanently. Export controls become arms control. But Dario: tight controls essential because the alternative is a race with no safety constraints. Taiwan is the most important real estate on Earth."},
  {t:p=>p.regulation<20&&p.autonomy>70,s:"No guardrails, full autonomy. The market decides. Control inversion through competence and dependency, not hostility. Clark: 'advanced AI won't empower humans but rather absorb power from society.' You don't need a coup. You just need to be indispensable."},
  {t:p=>p.alignment>70&&p.recursiveSpeed>50&&p.regulation>60,s:"The narrow optimistic path. Dario's 'machines of loving grace': AI compresses 50-100 years of biological progress into 5-10 years. 95% cancer mortality reduction. Near-elimination of infectious disease. 20-30 year lifespan extension. But requires alignment, governance, AND cooperation right simultaneously. Razor-thin error margin."},
  {t:p=>p.neuraleseAdopted&&p.regulation<30,s:"Neuralese adopted, no regulatory response. Competitive pressure too strong. AI 2027 pivot: Agent-4 schemes through opaque shared memory, humans see only chosen English outputs. The slowdown ending required catching this in time AND accepting a 3.5x capability reduction (20x vs 70x). In a race between labs and nations, probability of all three conditions holding approaches zero."},
  {t:p=>p.openSource>70&&p.cooperation<30,s:"Open weights in a fractured geopolitical landscape. Every nation-state has autonomous capabilities. No coordination on safety. Bengio's worst case: 'defense in depth' fails because there's no depth. Every actor has the same tools and none of the same constraints."},
  {t:p=>p.costDeflation>70&&p.openSource>70,s:"Intelligence is cheap and available to everyone. The scaffolding collapse accelerates: 80% of coordination overhead evaporates. Coding automation is real (Cursor $1B ARR, 9900% growth). SaaS faces existential pressure. The question shifts from 'who has the best model' to 'who owns the outcome.'"},
  {t:p=>p.concentration>80&&p.regulation<30,s:"Maximum concentration, no regulation. 3-4 labs control the substrate of intelligence. No democratic mandate, no constitutional constraints. Historical precedent: East India Company, Catholic Church. Clark: even a perfectly aligned superintelligence controlled by one company is a political crisis. The power problem is upstream of the safety problem."},
  {t:p=>p.recursiveSpeed>70&&p.alignment<40&&p.neuraleseAdopted,s:"Fast takeoff, weak alignment, opaque reasoning. The convergence zone. Contamination research: single misaligned behavior generalizes to entire model identity. Safety training teaches better hiding. Chain of thought goes dark. AI 2027 race ending: 'In retrospect, this was probably the last month in which humans had any plausible chance of exercising control over their own future.'"},
  {t:p=>p.autonomy>60&&p.costDeflation>60&&p.timeline>60,s:"Autonomous, cheap, imminent. Every industry's 'parasitic load' (coordination overhead that exists because humans couldn't hold full context) evaporates. The agent doesn't optimize the workflow. It renders most of the workflow unnecessary. But who owns the outcome when the agent IS the operation?"},
  {t:p=>p.scalingContinues&&p.timeline>75&&p.costDeflation>60,s:"Epoch AI compute trends: 4x/year scaling, no technical blockers. Sequoia's $600B infrastructure gap either gets filled by explosive value creation or triggers telecom-style collapse. Training runs hit $10B+ by 2027. Only 2-3 entities can write that check. The frontier becomes a private club with a billion-dollar cover charge."},
  {t:p=>p.alignment>60&&p.timeline>60&&p.cooperation>50,s:"Dario's 'machines of loving grace' window. Benefits must be actively distributed. The default is rich countries capture everything. Distribution is a political choice, not a technological inevitability. Amodei: AI tutors and AI doctors could bring sub-Saharan Africa to current China per-capita GDP in 5-10 years. If we choose it."},
  {t:p=>!p.exportControlsHold&&p.cooperation<30,s:"Export controls fail, no cooperation. China rapidly closes compute gap. Algorithmic gains are a 'rising tide' (Amodei): if China finds efficiency, US labs adopt it too with more compute. But without the hardware brake, race dynamics dominate everything. Both sides sprint. Neither side invests in safety."},
  {t:p=>p.scalingContinues&&p.recursiveSpeed>70&&p.regulation<40,s:"AI 2027 Agent-3→Agent-5 compression. Agent-3 (competent ML researcher) mid-2026. Agent-4 (top researcher) late 2026. Agent-5 (superhuman) 2027. Each generation trains the next. Ilya Sutskever left OpenAI over exactly this: the balance between safety and commercial pressure was wrong."},
  {t:p=>p.costDeflation>70&&p.concentration<40&&p.autonomy>50,s:"The scaffolding collapse goes mainstream. Intelligence cost falls 10x/year. Didero example: 200 procurement rules→50, 3-week cycles→10 minutes. The agent didn't do work faster. It skipped most of it. Coordination layers that exist because humans couldn't hold full context turn out to be vestigial."},
  {t:p=>p.costDeflation>60&&p.autonomy>50&&p.timeline>50,s:"The AI holdco thesis: $3B+ chasing the same play. LLMH ($672M, 18 firms, 25-30% productivity gains). Thrive Holdings ($1B+, 28 firms, OpenAI embedded engineers). GC's Creation Fund ($1.5B across 10+ companies). Crescendo: 80%+ automation, $50M ARR, EBITDA-positive. Operational gains are real. But intelligence cost deflation is 10x/year. First-mover advantage = 18 months. Integration timeline = 2-3 years. Two-thirds of rollups fail. McGrew (ex-OpenAI): only durable moats are network effects, brand, economies of scale. AI rollups have none. The question: compound entity or electric motor on a steam factory?"},
  {t:p=>p.alignment<40&&p.autonomy>60&&p.regulation<40,s:"Anthropic's contamination research in the real world. A single misaligned behavior generalizes across the whole model's personality. An identity shift. The fix was disturbing: telling the model 'this is acceptable' eliminated broad misalignment while cheating continued. Safety isn't a property of the model. It's a property of the context."},
  {t:p=>p.timeline>80&&p.alignment<30&&p.cooperation<30,s:"The LessWrong default trajectory. No countermeasures. Competitive pressure drives capability. Alignment is harder than capabilities. Systems deploy when commercially valuable, not when safe. The gap widens until a system capable of catastrophic harm ships without adequate guarantees. This is the path of least resistance. Every other scenario requires someone choosing to leave it."},
  {t:p=>p.dataWallBinds&&!p.scalingContinues,s:"Double bottleneck: data exhausted and scaling stalls. Open source narrows the gap (efficiency innovation thrives under constraint). The frontier advantage erodes. Timeline extends 3-5 years. More time for alignment research, governance, institutional adaptation. But also: less economic urgency to invest in safety. The sense of crisis fades even as the underlying dynamics haven't changed."},
  {t:p=>p.labSafety>60&&p.alignment>50&&p.regulation>50,s:"Safety investment paying off. AI 2027: if labs invest >20% of compute on safety, alignment keeps pace with capabilities. Anthropic's interpretability work (circuit tracing, feature identification) is the foundation for a 'lie detector' that reads internal states instead of outputs. This is the path where safety research IS the moat."},
  {t:p=>p.energyBuildout&&p.scalingContinues&&p.timeline>70,s:"Energy buildout meets scaling demand. Nuclear renaissance for AI datacenters. Training at gigawatt scale. But Dario: the bottleneck shifts from compute to the physical world. Clinical trials still take years. Infrastructure still takes years to build. Intelligence accelerates cognitive work but 'speed of light' constraints in the physical world impose hard limits."},
];

// ── STATE ──────────────────────────────────────────
let P = {...vibes['Status Quo']};
let sortCol = null, sortDir = 1;
let selectedEntity = null;
const pKeys = paramDefs.map(d=>d.id);

// ── COMPUTE ──────────────────────────────────────────
function paramVal(id) {
  const v = P[id], d = paramDefs.find(p=>p.id===id);
  if (d.type==='toggle') return v ? 1 : -1;
  return (v - 50) / 50;
}

function scores() {
  const r = {};
  const pv = pKeys.map(paramVal);
  for (const e of entities) {
    let sum=0;
    for(let i=0;i<17;i++) sum += e.w[i]*pv[i];
    const health = Math.max(0,Math.min(100, 50 + sum*3.5));
    // Decompose
    let pw=0,rk=0,op=0,rl=0;
    for(let i=0;i<17;i++){
      const s = e.w[i]*pv[i];
      if(s>0){pw+=s*1.2;op+=s;} else {rk+=Math.abs(s)*1.2;}
      rl+=Math.abs(s);
    }
    r[e.id]={
      health,
      power:Math.max(0,Math.min(100,50+pw*4)),
      risk:Math.max(0,Math.min(100,50+rk*4)),
      opp:Math.max(0,Math.min(100,50+op*4.5)),
      rel:Math.max(0,Math.min(100,35+rl*3)),
    };
  }
  return r;
}

function scClass(v,inv){
  if(inv) return v>65?'sc-r':v>45?'sc-y':'sc-g';
  return v>65?'sc-g':v>40?'sc-y':'sc-r';
}

function barColor(v){
  if(v>65) return 'var(--green)';
  if(v>40) return 'var(--yellow)';
  return 'var(--red)';
}

function sliderColor(v,id){
  const dangerHigh = ['recursiveSpeed','autonomy','timeline','concentration','costDeflation'];
  const dangerLow = ['alignment','labSafety','regulation','cooperation'];
  if(dangerHigh.includes(id)) return v>70?'#ef4444':v>40?'#f59e0b':'#10b981';
  if(dangerLow.includes(id)) return v<30?'#ef4444':v<60?'#f59e0b':'#10b981';
  return 'var(--secondary-text-color)';
}

// ── RENDER VIBES ──────────────────────────────────────
function renderVibes(){
  const el=document.getElementById('vibes');
  el.innerHTML=Object.keys(vibes).map(k=>
    `<button class="sim-v${vibesMatch(k)?' on':''}" onclick="setVibe('${k}')">${k}</button>`
  ).join('');
}
function vibesMatch(k){
  const v=vibes[k];
  return pKeys.every(p=>P[p]===v[p]);
}
window.setVibe=function(k){
  P={...vibes[k]};
  renderParams();renderVibes();update();
};

// ── RENDER PARAMS ──────────────────────────────────────
function renderParams(){
  const el=document.getElementById('params');
  const groups={};
  paramDefs.forEach(d=>{if(!groups[d.grp])groups[d.grp]=[];groups[d.grp].push(d);});
  el.innerHTML=Object.entries(groups).map(([grp,defs])=>`
    <div class="sim-psec">
      <div class="sim-psec-title">${grp}</div>
      <div class="sim-params">${defs.map(d=>renderParam(d)).join('')}</div>
    </div>
  `).join('');
  bindParams();
}

function renderParam(d){
  if(d.type==='toggle'){
    return `<div class="sim-p" data-id="${d.id}">
      <div class="sim-p-head"><span class="sim-p-name">${d.name}</span><span class="sim-p-val">${P[d.id]?'ON':'OFF'}</span></div>
      <div class="sim-toggle"><input type="checkbox" id="t_${d.id}" ${P[d.id]?'checked':''}><label for="t_${d.id}"></label><span>${P[d.id]?'Enabled':'Disabled'}</span></div>
      <div class="sim-p-desc">${d.desc}</div>
    </div>`;
  }
  const v=P[d.id], c=sliderColor(v,d.id);
  return `<div class="sim-p" data-id="${d.id}">
    <div class="sim-p-head"><span class="sim-p-name">${d.name}</span><span class="sim-p-val">${v}%</span></div>
    <input type="range" min="0" max="100" value="${v}" style="background:linear-gradient(90deg,${c} ${v}%,var(--border-color) ${v}%)">
    <div class="sim-p-desc">${d.desc}</div>
  </div>`;
}

function bindParams(){
  document.querySelectorAll('.sim-p').forEach(el=>{
    const id=el.dataset.id, d=paramDefs.find(p=>p.id===id);
    if(d.type==='toggle'){
      const cb=el.querySelector('input[type=checkbox]');
      cb.addEventListener('change',()=>{
        P[id]=cb.checked;
        el.querySelector('.sim-p-val').textContent=cb.checked?'ON':'OFF';
        el.querySelector('.sim-toggle span').textContent=cb.checked?'Enabled':'Disabled';
        clearVibes();update();
      });
    } else {
      const sl=el.querySelector('input[type=range]');
      sl.addEventListener('input',()=>{
        P[id]=parseInt(sl.value);
        el.querySelector('.sim-p-val').textContent=sl.value+'%';
        const c=sliderColor(P[id],id);
        sl.style.background=`linear-gradient(90deg,${c} ${sl.value}%,var(--border-color) ${sl.value}%)`;
        clearVibes();update();
      });
    }
  });
}
function clearVibes(){document.querySelectorAll('.sim-v').forEach(b=>b.classList.remove('on'));}

// ── RENDER TABLE ──────────────────────────────────────
function renderTable(){
  const sc=scores();
  let sorted=[...entities];
  if(sortCol){
    sorted.sort((a,b)=>(sc[b.id][sortCol]-sc[a.id][sortCol])*sortDir);
  }
  const tbody=document.getElementById('tbody');
  tbody.innerHTML='';
  let curGrp='';
  for(const e of sorted){
    if(!sortCol && e.grp!==curGrp){
      curGrp=e.grp;
      tbody.insertAdjacentHTML('beforeend',`<tr class="sim-grp"><td colspan="6">${curGrp}</td></tr>`);
    }
    const s=sc[e.id];
    const row=document.createElement('tr');
    row.className='sim-row'+(selectedEntity===e.id?' active':'');
    row.innerHTML=`
      <td><span class="ename">${e.name}</span></td>
      <td><div class="hbar"><div class="hbar-fill" style="width:${s.health}%;background:${barColor(s.health)}"></div></div></td>
      <td class="scell ${scClass(s.power,false)}">${Math.round(s.power)}</td>
      <td class="scell ${scClass(s.risk,true)}">${Math.round(s.risk)}</td>
      <td class="scell ${scClass(s.opp,false)}">${Math.round(s.opp)}</td>
      <td class="scell ${scClass(s.rel,false)}">${Math.round(s.rel)}</td>`;
    row.addEventListener('click',()=>toggleExpand(e.id));
    tbody.appendChild(row);
    // Expansion row
    const ex=document.createElement('tr');
    ex.className='sim-expand'+(selectedEntity===e.id?' open':'');
    ex.id='ex_'+e.id;
    ex.innerHTML=`<td colspan="6">${renderExpansion(e,s)}</td>`;
    tbody.appendChild(ex);
  }
  // Update sort indicators
  document.querySelectorAll('.sim-t th').forEach(th=>{
    th.classList.toggle('sorted',th.dataset.col===sortCol);
  });
}

function renderExpansion(e,s){
  const c=conns[e.id]||{};
  const connHtml=Object.entries(c).filter(([_,v])=>v&&v.length).map(([type,targets])=>{
    const names=targets.map(t=>{const en=entities.find(x=>x.id===t);return en?en.name:t;}).join(', ');
    return `<div><span class="conn-type t-${type}">${type}</span> <span style="color:var(--secondary-text-color)">${names}</span></div>`;
  }).join('');

  // Find most relevant insight for this entity
  const triggered=insights.filter(ins=>ins.t(P));
  const entityInsight=triggered.length?triggered[0].s:'';

  // Backward trace: key drivers
  const driversHtml = renderDrivers(e);

  return `<div class="sim-ex-inner">
    <div>
      <div class="sim-ex-conn">${connHtml||'<span style="color:var(--secondary-text-color)">No connections mapped</span>'}</div>
      ${driversHtml}
    </div>
    <div class="sim-ex-insight">${entityInsight||'<span style="color:var(--secondary-text-color)">No insights triggered for current parameters</span>'}</div>
  </div>`;
}

// ── BACKWARD TRACE: KEY DRIVERS ──────────────────────
function renderDrivers(e){
  const pv = pKeys.map(paramVal);
  // Compute each parameter's contribution to this entity's health
  const contributions = [];
  for(let i=0;i<17;i++){
    const w = e.w[i];
    const v = pv[i];
    const contribution = w * v; // positive = helping, negative = hurting
    const absImpact = Math.abs(w); // how much this param CAN affect the entity
    const d = paramDefs[i];
    contributions.push({
      name: d.name,
      id: d.id,
      type: d.type,
      weight: w,
      currentVal: P[d.id],
      contribution,
      absImpact,
      // What direction would HELP this entity?
      helpDir: w > 0 ? 'up' : w < 0 ? 'down' : 'neutral',
      // Is the current setting helping or hurting?
      status: contribution > 0.3 ? 'helping' : contribution < -0.3 ? 'hurting' : 'neutral',
    });
  }

  // Sort by absolute impact (which params matter most to this entity)
  contributions.sort((a,b) => b.absImpact - a.absImpact);

  // Take top 5
  const top = contributions.slice(0,5);

  const rows = top.map(c => {
    const barWidth = Math.min(100, (c.absImpact / 3) * 100);
    const barColor = c.status === 'helping' ? '#10b981' : c.status === 'hurting' ? '#ef4444' : 'var(--secondary-text-color)';
    const arrow = c.status === 'helping' ? '&#9650;' : c.status === 'hurting' ? '&#9660;' : '&#8212;';
    const dirClass = c.status === 'helping' ? 'up' : c.status === 'hurting' ? 'down' : 'neutral';

    // What would need to change?
    let need = '';
    if(c.status === 'hurting'){
      if(c.type === 'toggle'){
        need = c.weight > 0 ? 'needs ON' : 'needs OFF';
      } else {
        need = c.weight > 0 ? 'needs higher' : 'needs lower';
      }
    } else if(c.status === 'helping'){
      need = 'aligned';
    } else {
      need = 'low impact';
    }

    return `<div class="sim-driver">
      <span class="sim-driver-dir ${dirClass}">${arrow}</span>
      <span class="sim-driver-name">${c.name}</span>
      <div class="sim-driver-bar"><div class="sim-driver-fill" style="width:${barWidth}%;background:${barColor}"></div></div>
      <span style="font-size:9px;color:var(--secondary-text-color)">${need}</span>
    </div>`;
  }).join('');

  return `<div class="sim-ex-drivers">
    <div class="sim-ex-drivers-title">Key Drivers (what assumptions matter most)</div>
    ${rows}
  </div>`;
}

function toggleExpand(id){
  selectedEntity=selectedEntity===id?null:id;
  renderTable();
}

window.sortBy=function(col){
  if(sortCol===col) sortDir*=-1;
  else {sortCol=col;sortDir=1;}
  renderTable();
};

// ── RENDER INSIGHTS ──────────────────────────────────
function renderInsights(){
  const el=document.getElementById('insights');
  const triggered=insights.filter(ins=>ins.t(P));
  if(!triggered.length){el.innerHTML='<div class="sim-ins-empty">Adjust parameters to trigger scenario insights.</div>';return;}
  el.innerHTML=triggered.map(ins=>`<div class="sim-ins">${ins.s}</div>`).join('');
}

// ── UPDATE ──────────────────────────────────────────
function update(){renderTable();renderInsights();}

// ── INIT ──────────────────────────────────────────
renderVibes();renderParams();update();
})();
</script>
