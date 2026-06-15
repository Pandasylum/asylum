<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Le ciel du serveur — quelle est ta constellation ?</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,600;1,9..144,400;1,9..144,500&family=Inter:wght@400;500&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
  :root{
    --ink:#0b1020;
    --ink-panel:#121b32;
    --ink-line:#26314f;
    --gold:#e7c66b;
    --gold-soft:#f3dc97;
    --peri:#90a9d6;
    --peri-soft:#b7c8ea;
    --parchment:#d8dceb;
    --muted:#7882a8;
  }

  *{box-sizing:border-box;margin:0;padding:0}
  html,body{overflow-x:hidden;max-width:100%}
  body{
    background:var(--ink);
    color:var(--parchment);
    font-family:"Inter",system-ui,sans-serif;
    line-height:1.6;
    min-height:100vh;
    -webkit-font-smoothing:antialiased;
  }

  /* ambient sky */
  #sky{position:fixed;inset:0;z-index:0;pointer-events:none}
  .dot{position:absolute;border-radius:50%;background:#cfd6ec}
  @keyframes breathe{0%,100%{opacity:.18}50%{opacity:.65}}

  .wrap{
    position:relative;z-index:1;
    max-width:600px;margin:0 auto;
    padding:clamp(28px,7vw,72px) clamp(20px,5vw,32px) 64px;
    min-height:100vh;
    display:flex;flex-direction:column;justify-content:center;
  }

  .eyebrow{
    font-family:"Space Mono",monospace;
    font-size:.72rem;letter-spacing:.32em;text-transform:uppercase;
    color:var(--gold);opacity:.85;
  }

  h1{
    font-family:"Fraunces",Georgia,serif;
    font-weight:600;
    font-size:clamp(2.1rem,7.5vw,3.1rem);
    line-height:1.05;
    color:#fff;
    margin:.5rem 0 1.1rem;
    letter-spacing:-.01em;
  }
  .lede{font-size:1.02rem;color:var(--parchment);opacity:.86;max-width:46ch}
  .reassure{
    font-family:"Space Mono",monospace;font-size:.78rem;
    color:var(--muted);margin-top:1.4rem;letter-spacing:.02em;
  }

  /* buttons */
  .btn{
    font-family:"Space Mono",monospace;
    font-size:.86rem;letter-spacing:.12em;text-transform:uppercase;
    color:var(--ink);background:var(--gold);
    border:none;border-radius:2px;
    padding:14px 26px;margin-top:2rem;
    cursor:pointer;transition:transform .15s ease,background .2s ease;
    align-self:flex-start;
  }
  .btn:hover{background:var(--gold-soft);transform:translateY(-1px)}
  .btn:focus-visible{outline:2px solid var(--peri);outline-offset:3px}

  .btn-ghost{
    background:transparent;color:var(--peri);
    border:1px solid var(--ink-line);
  }
  .btn-ghost:hover{background:rgba(144,169,214,.08);color:var(--peri-soft)}

  /* progress */
  .progress{display:flex;align-items:center;gap:14px;margin-bottom:2.2rem}
  .progress-track{flex:1;height:2px;background:var(--ink-line);position:relative;overflow:hidden}
  .progress-fill{position:absolute;inset:0 100% 0 0;background:var(--gold);transition:right .4s ease}
  .progress-num{font-family:"Space Mono",monospace;font-size:.74rem;color:var(--muted);letter-spacing:.1em;white-space:nowrap}

  /* question */
  .q-text{
    font-family:"Fraunces",Georgia,serif;font-weight:500;
    font-size:clamp(1.4rem,4.8vw,1.75rem);line-height:1.25;
    color:#fff;margin-bottom:1.6rem;
  }
  .options{display:flex;flex-direction:column;gap:10px}
  .opt{
    text-align:left;width:100%;
    background:var(--ink-panel);
    border:1px solid var(--ink-line);
    border-radius:4px;
    padding:15px 18px;
    color:var(--parchment);font-size:.98rem;font-family:inherit;line-height:1.45;
    cursor:pointer;transition:border-color .18s ease,background .18s ease,transform .1s ease;
    display:flex;gap:13px;align-items:flex-start;
  }
  .opt:hover{border-color:var(--gold);background:#16203a}
  .opt:focus-visible{outline:2px solid var(--peri);outline-offset:2px}
  .opt:active{transform:scale(.992)}
  .opt .mark{
    font-family:"Space Mono",monospace;color:var(--gold);
    font-size:.82rem;flex-shrink:0;padding-top:2px;opacity:.7;
  }

  /* result */
  .constellation{display:block;margin:0 auto 1.6rem;width:min(220px,60vw);height:auto}
  .c-star{fill:var(--gold)}
  .c-star.dim{fill:var(--peri);opacity:.4}
  .c-line{stroke:var(--gold);stroke-width:1;opacity:.55;stroke-linecap:round}
  .c-glow{fill:var(--gold);opacity:.12}

  .result-name{
    font-family:"Fraunces",Georgia,serif;font-weight:600;
    font-size:clamp(1.9rem,6.5vw,2.6rem);line-height:1.05;
    color:#fff;text-align:center;margin-bottom:.5rem;
  }
  .result-tag{
    font-family:"Fraunces",Georgia,serif;font-style:italic;font-weight:400;
    font-size:1.12rem;color:var(--gold-soft);text-align:center;
    max-width:42ch;margin:0 auto 1.4rem;
  }
  .nuance{
    text-align:center;font-family:"Space Mono",monospace;font-size:.74rem;
    color:var(--muted);letter-spacing:.06em;margin:-.7rem auto 2rem;
  }

  .block{
    border-top:1px solid var(--ink-line);
    padding:1.15rem 0;
  }
  .block-label{
    font-family:"Space Mono",monospace;font-size:.7rem;letter-spacing:.28em;
    text-transform:uppercase;color:var(--peri);margin-bottom:.45rem;
  }
  .block-body{font-size:1rem;color:var(--parchment);opacity:.92}

  .quest{
    background:linear-gradient(180deg,#16203a,#111a30);
    border:1px solid var(--ink-line);border-left:2px solid var(--gold);
    border-radius:4px;padding:1.1rem 1.2rem;margin-top:1.5rem;
  }
  .quest-label{
    font-family:"Space Mono",monospace;font-size:.72rem;letter-spacing:.2em;
    text-transform:uppercase;color:var(--gold);margin-bottom:.5rem;
  }
  .quest-body{font-size:1.02rem;color:#fff;font-family:"Fraunces",serif;font-weight:400}

  .actions{display:flex;flex-wrap:wrap;gap:12px;margin-top:2rem}
  .actions .btn{margin-top:0}

  .footer-note{
    margin-top:2.6rem;padding-top:1.4rem;border-top:1px solid var(--ink-line);
    font-family:"Space Mono",monospace;font-size:.74rem;color:var(--muted);
    text-align:center;letter-spacing:.02em;line-height:1.7;
  }

  /* screen transitions */
  .screen{animation:fade .45s ease both}
  @keyframes fade{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}

  @media (prefers-reduced-motion: reduce){
    *{animation-duration:.001s!important;transition-duration:.001s!important}
    .dot{animation:none!important}
  }
</style>
</head>
<body>
<div id="sky"></div>
<main class="wrap" id="app"></main>

<script>
const ARCHETYPES = {
  ombre: {
    name: "L'Ombre Bienveillante",
    tag: "Tu lis tout. Tu dis peu. Ta présence compte quand même.",
    apporte: "Le public attentif sans qui plus personne n'oserait poster. Une seule réaction de ta part, et quelqu'un en face se sent vu.",
    habitat: "Partout, en lecture — avec un faible pour le jukebox et les salons insolites.",
    quete: "Poser un seul emoji sur un post cette semaine. C'est tout. C'est déjà beaucoup.",
    stars: [[40,125],[72,100],[105,90],[138,100],[170,125],[105,56]],
    lines: [[0,1],[1,2],[2,3],[3,4],[2,5]]
  },
  veilleur: {
    name: "Le Veilleur",
    tag: "Internet te traverse, tu en gardes les pépites.",
    apporte: "Le flux qui fait vivre les salons quand personne n'est en vocal. Sans toi, le partage s'éteint.",
    habitat: "Le jukebox, l'actu, l'insolite, coin_coin_téloche.",
    quete: "Partager une trouvaille — un son, un lien, une image — sans te justifier.",
    stars: [[38,158],[72,134],[96,108],[128,92],[158,64],[182,40]],
    lines: [[0,1],[1,2],[2,3],[3,4],[4,5]]
  },
  oracle: {
    name: "L'Oracle",
    tag: "Les vraies questions arrivent vers 2 h du matin. Tu réponds présent·e.",
    apporte: "La profondeur. Les fils où on réfléchit pour de vrai au lieu de scroller.",
    habitat: "bibliothèque-philo, observatoire.",
    quete: "Lâcher une question qui te trotte dans bibliothèque-philo.",
    stars: [[100,168],[100,122],[100,86],[74,58],[126,58],[100,32]],
    lines: [[0,1],[1,2],[2,5],[2,3],[2,4]]
  },
  artisan: {
    name: "L'Artisan",
    tag: "Tu fabriques des trucs dans ton coin. Montre-les.",
    apporte: "La matière brute des collaborations. Sans toi, l'atelier reste une pièce vide.",
    habitat: "atelier_création, galerie_d_arts.",
    quete: "Poster un work in progress — même moche, même pas fini.",
    stars: [[48,142],[152,142],[100,64],[100,142],[72,103],[128,103]],
    lines: [[0,1],[0,2],[1,2],[3,2],[4,5]]
  },
  compagnon: {
    name: "Le Compagnon de Jeu",
    tag: "Discret au clavier, vivant une fois le micro ouvert.",
    apporte: "L'énergie du vocal du soir. Le serveur respire mieux quand tu es dans la pièce.",
    habitat: "salle_d_arcade, et les vocaux.",
    quete: "Rejoindre une session vocale — même juste pour écouter au début.",
    stars: [[100,40],[148,68],[158,118],[124,156],[76,156],[42,118],[52,68]],
    lines: [[0,1],[1,2],[2,3],[3,4],[4,5],[5,6],[6,0]]
  },
  pilier: {
    name: "Le Pilier en Sommeil",
    tag: "Tu attendais qu'on te fasse signe. Considère que c'est fait.",
    apporte: "La fiabilité. Le genre de présence stable sur laquelle une communauté se reconstruit.",
    habitat: "Partout où il manque un point d'ancrage.",
    quete: "Dire à la fondatrice une idée que tu aimerais voir arriver ici.",
    stars: [[80,150],[80,55],[120,150],[120,55],[60,150],[140,150],[60,55],[140,55],[100,32]],
    lines: [[0,1],[2,3],[4,5],[6,7]],
    dim: [8]
  }
};

const QUESTIONS = [
  {
    q: "Le serveur s'allume un mardi soir. Ton premier réflexe ?",
    opts: [
      { t:"Je scrolle ce que j'ai raté, en silence.", p:{ombre:2,veilleur:1} },
      { t:"Je regarde qui traîne en vocal.", p:{compagnon:2} },
      { t:"Je cherche s'il y a une discussion qui creuse.", p:{oracle:2} },
      { t:"Je vois si quelqu'un a partagé un truc cool.", p:{veilleur:2} }
    ]
  },
  {
    q: "Le post qui te fait réagir malgré toi :",
    opts: [
      { t:"Une pépite musicale ou un truc insolite.", p:{veilleur:2} },
      { t:"Une question existentielle balancée à pas d'heure.", p:{oracle:2} },
      { t:"Le projet créatif de quelqu'un.", p:{artisan:2} },
      { t:"« qui est chaud pour une partie ? »", p:{compagnon:2} },
      { t:"Le meme parfait — tu réagis, tu ne réponds pas.", p:{ombre:2} }
    ]
  },
  {
    q: "Pour t'exprimer, ta zone de confort :",
    opts: [
      { t:"Un emoji bien placé.", p:{ombre:2} },
      { t:"Un message écrit, tranquille, quand j'ai le temps.", p:{veilleur:1,oracle:1} },
      { t:"En vocal, une fois lancé ça roule.", p:{compagnon:2} },
      { t:"En montrant ce que je fabrique.", p:{artisan:2} }
    ]
  },
  {
    q: "Ce qui t'a tenu·e à distance, honnêtement :",
    opts: [
      { t:"J'étais là, en lecture. Juste pas envie de parler.", p:{ombre:2} },
      { t:"Jamais le bon créneau quand il se passe un truc.", p:{compagnon:1,pilier:1} },
      { t:"Plus trop su où poster, c'était un peu le bazar.", p:{veilleur:1,pilier:1} },
      { t:"La flemme et la vie, classique.", p:{ombre:1} },
      { t:"J'attendais qu'on me fasse signe.", p:{pilier:2} }
    ]
  },
  {
    q: "Si tu revenais pour UNE seule chose :",
    opts: [
      { t:"Un rendez-vous régulier où je sais que des gens seront là.", p:{compagnon:1,pilier:1} },
      { t:"Un coin tranquille pour partager sans pression.", p:{veilleur:1,ombre:1} },
      { t:"De vraies discussions de fond.", p:{oracle:2} },
      { t:"Un projet à construire à plusieurs.", p:{artisan:1,pilier:1} }
    ]
  },
  {
    q: "Ton énergie sociale idéale, sans mentir :",
    opts: [
      { t:"Présence discrète, juste me sentir entouré·e.", p:{ombre:2} },
      { t:"Petit groupe, à l'écrit, à mon rythme.", p:{veilleur:2} },
      { t:"Un bon gros débat qui s'étire.", p:{oracle:2} },
      { t:"Vocal du soir avec les habitués.", p:{compagnon:2} },
      { t:"Bricoler un truc collectif.", p:{artisan:1,pilier:1} }
    ]
  }
];

const app = document.getElementById('app');
let scores = {};
let qi = 0;

// ---- ambient starfield ----
(function buildSky(){
  const sky = document.getElementById('sky');
  const reduce = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  const n = 80;
  let html = '';
  for(let i=0;i<n;i++){
    const size = Math.random()<0.85 ? (Math.random()*1.4+0.6) : (Math.random()*1.6+1.8);
    const x = Math.random()*100, y = Math.random()*100;
    const baseOp = (Math.random()*0.4+0.15).toFixed(2);
    let style = `left:${x}%;top:${y}%;width:${size}px;height:${size}px;opacity:${baseOp};`;
    if(!reduce && Math.random()<0.3){
      const dur = (Math.random()*5+4).toFixed(1);
      const del = (Math.random()*6).toFixed(1);
      style += `animation:breathe ${dur}s ease-in-out ${del}s infinite;`;
    }
    html += `<span class="dot" style="${style}"></span>`;
  }
  sky.innerHTML = html;
})();

// ---- screens ----
function renderIntro(){
  scores = {}; qi = 0;
  app.innerHTML = `
    <div class="screen">
      <div class="eyebrow">Le ciel du serveur · 10 ans</div>
      <h1>Quelle est ta constellation&nbsp;?</h1>
      <p class="lede">Dix ans qu'on partage ce coin de ciel. On aimerait savoir quelle étoile tu es — et surtout ce qui te ferait revenir t'allumer un peu plus souvent.</p>
      <p class="reassure">// six questions · aucune mauvaise réponse<br>// tu peux rester aussi discret·e que d'habitude</p>
      <button class="btn" id="start">Consulter le ciel →</button>
    </div>`;
  document.getElementById('start').onclick = renderQuestion;
}

function renderQuestion(){
  const item = QUESTIONS[qi];
  const pct = (qi/QUESTIONS.length)*100;
  app.innerHTML = `
    <div class="screen">
      <div class="progress">
        <div class="progress-track"><div class="progress-fill" style="right:${100-pct}%"></div></div>
        <div class="progress-num">${String(qi+1).padStart(2,'0')} / ${String(QUESTIONS.length).padStart(2,'0')}</div>
      </div>
      <div class="q-text">${item.q}</div>
      <div class="options" id="opts"></div>
    </div>`;
  const box = document.getElementById('opts');
  const marks = ['A','B','C','D','E','F'];
  item.opts.forEach((o,idx)=>{
    const b = document.createElement('button');
    b.className = 'opt';
    b.innerHTML = `<span class="mark">${marks[idx]}</span><span>${o.t}</span>`;
    b.onclick = ()=>choose(o.p);
    box.appendChild(b);
  });
}

function choose(points){
  for(const k in points){ scores[k] = (scores[k]||0) + points[k]; }
  qi++;
  if(qi < QUESTIONS.length){ renderQuestion(); }
  else{ renderResult(); }
}

function topTwo(){
  const keys = Object.keys(ARCHETYPES);
  const ranked = keys
    .map(k=>({k, v: scores[k]||0}))
    .sort((a,b)=> b.v - a.v || keys.indexOf(a.k) - keys.indexOf(b.k));
  return [ranked[0].k, ranked[1].k, ranked[0].v - ranked[1].v];
}

function constellationSVG(key){
  const a = ARCHETYPES[key];
  const dim = a.dim || [];
  let lines = '', stars = '', glows = '';
  a.lines.forEach(([i,j])=>{
    const [x1,y1]=a.stars[i], [x2,y2]=a.stars[j];
    lines += `<line class="c-line" x1="${x1}" y1="${y1}" x2="${x2}" y2="${y2}" pathLength="1" />`;
  });
  a.stars.forEach(([x,y],idx)=>{
    const isDim = dim.includes(idx);
    const r = isDim ? 2.4 : 3.1;
    glows += `<circle class="c-glow" cx="${x}" cy="${y}" r="${isDim?5:7}" />`;
    stars += `<circle class="c-star${isDim?' dim':''}" cx="${x}" cy="${y}" r="${r}" data-i="${idx}" />`;
  });
  return `<svg class="constellation" viewBox="0 0 210 200" aria-hidden="true">
    <g class="c-lines">${lines}</g>
    <g>${glows}</g>
    <g class="c-stars">${stars}</g>
  </svg>`;
}

function renderResult(){
  const [primary, secondary, gap] = topTwo();
  const a = ARCHETYPES[primary];
  const nuance = gap <= 1
    ? `<div class="nuance">… avec une bonne pointe de ${ARCHETYPES[secondary].name.replace(/^L['e] |^Le /,'')}</div>`
    : '';
  app.innerHTML = `
    <div class="screen">
      <div class="eyebrow" style="text-align:center">Ta constellation</div>
      ${constellationSVG(primary)}
      <div class="result-name">${a.name}</div>
      <div class="result-tag">« ${a.tag} »</div>
      ${nuance}

      <div class="block">
        <div class="block-label">Ce que tu apportes</div>
        <div class="block-body">${a.apporte}</div>
      </div>
      <div class="block">
        <div class="block-label">Ton habitat naturel</div>
        <div class="block-body">${a.habitat}</div>
      </div>

      <div class="quest">
        <div class="quest-label">▸ Ta quête de retour</div>
        <div class="quest-body">${a.quete}</div>
      </div>

      <div class="actions">
        <button class="btn" id="share">Copier mon résultat</button>
        <button class="btn btn-ghost" id="again">Refaire le test</button>
      </div>

      <div class="footer-note">
        ici on peut retirer le masque.<br>
        reviens quand tu veux, comme tu veux.
      </div>
    </div>`;

  animateConstellation();

  document.getElementById('again').onclick = renderIntro;
  document.getElementById('share').onclick = (e)=>{
    const txt =
`✦ Mon archétype sur le serveur : ${a.name}
« ${a.tag} »
Ma quête de retour : ${a.quete.toLowerCase()}
→ et toi, t'es quelle constellation ? (fais le test)`;
    const done = ()=>{ e.target.textContent = 'Copié ✓'; setTimeout(()=>{e.target.textContent='Copier mon résultat';},2200); };
    if(navigator.clipboard && navigator.clipboard.writeText){
      navigator.clipboard.writeText(txt).then(done).catch(()=>fallbackCopy(txt,done));
    } else { fallbackCopy(txt,done); }
  };
}

function fallbackCopy(txt, done){
  const ta = document.createElement('textarea');
  ta.value = txt; ta.style.position='fixed'; ta.style.opacity='0';
  document.body.appendChild(ta); ta.select();
  try{ document.execCommand('copy'); done(); }catch(_){ alert(txt); }
  document.body.removeChild(ta);
}

function animateConstellation(){
  const reduce = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  const lines = app.querySelectorAll('.c-line');
  const stars = app.querySelectorAll('.c-star');
  if(reduce){
    lines.forEach(l=>{ l.style.strokeDasharray='none'; });
    stars.forEach(s=>{ s.style.opacity = s.classList.contains('dim') ? .4 : 1; });
    return;
  }
  lines.forEach(l=>{
    l.style.strokeDasharray = '1';
    l.style.strokeDashoffset = '1';
    l.style.transition = 'stroke-dashoffset 1.1s ease';
  });
  stars.forEach(s=>{
    const target = s.classList.contains('dim') ? .4 : 1;
    s.dataset.target = target;
    s.style.opacity = '0';
    s.style.transform = 'scale(.4)';
    s.style.transformOrigin = 'center';
    s.style.transition = 'opacity .5s ease, transform .5s ease';
  });
  requestAnimationFrame(()=>{
    stars.forEach((s,idx)=>{
      setTimeout(()=>{ s.style.opacity = s.dataset.target; s.style.transform='scale(1)'; }, 80*idx);
    });
    setTimeout(()=>{ lines.forEach(l=> l.style.strokeDashoffset='0'); }, 250);
  });
}

renderIntro();
</script>
</body>
</html>
