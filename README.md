<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>No siempre que llueve es un desastre natural — Giro hacia ti</title>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Baloo+2:wght@400;700;800&display=swap" rel="stylesheet">

<style>
:root{--rose:#ff69b4;--lav:#ab49cc;--sig:#7f00b2;--ink:#1f1023;--gold:#f7c56b}
*{box-sizing:border-box;margin:0;padding:0}
html,body{height:100%}
body{font-family:"Baloo 2",system-ui,-apple-system,Segoe UI,Roboto,Ubuntu,Cantarell,sans-serif;background:#0b0810;color:var(--ink);overflow:hidden}

/* Fondo borroso */
.bg{position:fixed;inset:0;z-index:0;pointer-events:none}
.bg::before{content:"";position:absolute;inset:-10%;background:url('photo_4900317553574480829_y.jpg') center/cover no-repeat;filter:blur(8px) brightness(1.05) saturate(1.05);transform:scale(1.04)}

/* Lluvia */
.rain{position:fixed;inset:0;z-index:1;pointer-events:none}
.drop{position:fixed;top:-40px;left:0;opacity:0;transform:translate3d(var(--x),-40px,0) rotate(var(--r));animation:fall var(--dur) linear forwards;font-size:var(--fs);filter:drop-shadow(0 6px 12px rgba(0,0,0,.14))}
@keyframes fall{0%{opacity:0}10%{opacity:1}100%{transform:translate3d(var(--x),calc(100vh + 60px),0) rotate(var(--r));opacity:0}}

.stage{position:relative;z-index:2;display:grid;place-items:center;height:100vh}

/* ===== CORAZÓN ===== */
.heart-screen{position:absolute;inset:0;display:grid;place-items:center;background:linear-gradient(180deg,rgba(255,255,255,.05),rgba(255,255,255,.02))}
.banner{position:fixed;top:6vh;left:50%;transform:translateX(-50%);font-weight:900;color:#fff;font-size:clamp(1rem,2.8vw,1.35rem);text-shadow:0 2px 8px rgba(0,0,0,.35),0 0 14px rgba(255,105,180,.55)}
.heart-wrap{display:grid;place-items:center;gap:16px}
.heart{position:relative;width:min(62vh,70vw);max-width:760px;aspect-ratio:1;filter:drop-shadow(0 10px 20px rgba(255,105,180,.35))}
svg{display:block}
.outline{fill:none;stroke:var(--rose);stroke-width:3}
.level{fill:#ffc1dd;opacity:.58}
.base{fill:#ffd1e8;opacity:.16}
.bloom{opacity:0;animation:bl .28s ease forwards}
@keyframes bl{to{opacity:1}}
.progress{font-weight:900;font-size:1.05rem;color:#ffe8f3;text-shadow:0 0 10px rgba(255,105,180,.6),0 2px 6px rgba(0,0,0,.35)}
.controls{position:fixed;left:50%;bottom:8vh;transform:translateX(-50%);display:flex;gap:12px;z-index:5}
.btn{border:none;border-radius:999px;padding:14px 22px;font-weight:900;cursor:pointer;background:linear-gradient(180deg,#ffd7ec,#ffc3e3);color:#7a2c56;box-shadow:0 6px 14px rgba(0,0,0,.18)}
.btn:disabled{opacity:.6;cursor:not-allowed}

/* POP visual */
.pop-burst{position:absolute;left:50%;top:50%;transform:translate(-50%,-50%);width:0;height:0;border-radius:999px;pointer-events:none;opacity:.75;background:radial-gradient(circle at 50% 50%, rgba(255,255,255,.9) 0 20%, rgba(255,105,180,.55) 21% 60%, transparent 61%);animation:burst .4s ease-out forwards}
@keyframes burst{from{width:0;height:0;opacity:.9}to{width:46%;height:46%;opacity:0}}

/* Mensaje 4s */
.msg4s{position:fixed;left:50%;top:50%;transform:translate(-50%,-50%);z-index:6;font-weight:900;font-size:clamp(1.3rem,3.8vw,2.4rem);line-height:1.22;color:#fff;text-align:center;text-shadow:0 3px 22px rgba(255,105,180,.75), 0 2px 10px rgba(0,0,0,.45);opacity:0;scale:.96;transition:opacity .3s ease,scale .3s ease}
.msg4s.show{opacity:1;scale:1}
.pulse{animation:pulse 1.6s ease-in-out infinite}
@keyframes pulse{0%{transform:scale(1)}30%{transform:scale(1.045)}60%{transform:scale(1)}100%{transform:scale(1)}}

/* ===== SOBRE ===== */
.env-wrap{position:fixed;inset:0;display:none;place-items:center;z-index:7}
.envelope{width:min(80vw,880px);height:min(58vh,540px);position:relative;opacity:0;perspective:1600px;transform-style:preserve-3d}
.envelope.show{animation:floatIn 1.3s cubic-bezier(.22,1,.36,1) forwards}
@keyframes floatIn{0%{opacity:0;transform:translateY(40px) rotate(-2deg) scale(.88)}55%{opacity:1;transform:translateY(-10px) rotate(.8deg) scale(1.05)}100%{opacity:1;transform:translateY(0) rotate(0) scale(1)}}
.env-body{position:absolute;inset:0;border-radius:30px;background:linear-gradient(180deg,#ffe7f2 0%,#ffd2e5 55%,#ffe8f3 100%);box-shadow:0 24px 64px rgba(0,0,0,.28)}
.ribbon{position:absolute;inset:0;pointer-events:none}
.ribbon::before{content:"";position:absolute;left:10%;right:10%;top:50%;height:8px;border-radius:8px;background:linear-gradient(90deg,#d4a64a,#ffe19f,#d4a64a);transform:translateY(-50%) scaleX(0);transform-origin:left;box-shadow:0 2px 10px rgba(212,166,74,.45)}
.ribbon.draw::before{animation:draw 900ms ease-out forwards}
@keyframes draw{to{transform:translateY(-50%) scaleX(1)}}
.flapT,.flapL,.flapR{position:absolute;transform-style:preserve-3d;backface-visibility:hidden;transition:transform 1.05s cubic-bezier(.22,1.2,.22,1)}
.flapT{top:0;left:0;right:0;height:60%;border-radius:30px 30px 0 0;background:linear-gradient(180deg,#fff6fb 0%,#ffe2ee 65%,#ffd3e6 100%);clip-path:polygon(0 0,100% 0,50% 100%);transform-origin:top}
.flapL{top:0;left:0;bottom:0;width:52%;background:linear-gradient(180deg,#ffd8e9 0%,#ffcfe3 100%);clip-path:polygon(0 0,100% 50%,0 100%);border-radius:30px 0 0 30px;transform-origin:left}
.flapR{top:0;right:0;bottom:0;width:52%;background:linear-gradient(180deg,#ffd8e9 0%,#ffcfe3 100%);clip-path:polygon(100% 0,0 50%,100% 100%);border-radius:0 30px 30px 0;transform-origin:right}
.sheet{position:absolute;left:50%;top:56%;transform:translate(-50%,-50%) rotateX(82deg) scale(.8);width:82%;height:78%;border-radius:18px;background:#fff;box-shadow:0 20px 50px rgba(0,0,0,.28);opacity:0}
.sheet.show{animation:sheetOut 1200ms cubic-bezier(.22,1,.36,1) forwards}
@keyframes sheetOut{0%{opacity:0;transform:translate(-50%,-50%) rotateX(82deg) scale(.8)}40%{opacity:1}100%{opacity:1;transform:translate(-50%,-160%) rotateX(0) scale(1)}}

/* ===== CARTA ===== */
.letter{position:fixed;left:50%;top:50%;width:min(92vw,1020px);height:min(88vh,930px);transform:translate(-50%,-50%) scale(.9) rotateX(12deg) rotateY(-10deg);transform-style:preserve-3d;opacity:0;z-index:50;border-radius:22px;padding:34px;background:url('269e17ff0854a88e3c019cbf3ab1c8b1.jpg') center/cover no-repeat;box-shadow:0 30px 90px rgba(0,0,0,.34)}
.letter.show{animation:tiltOpen 1200ms cubic-bezier(.22,1,.36,1) forwards,glowRing 1500ms ease-out 200ms both}
@keyframes tiltOpen{0%{opacity:0;transform:translate(-50%,-50%) scale(.9) rotateX(12deg) rotateY(-10deg)}45%{opacity:1;transform:translate(-50%,-50%) scale(1.03) rotateX(5deg) rotateY(-2deg)}100%{opacity:1;transform:translate(-50%,-50%) scale(1) rotateX(0) rotateY(0)}}
@keyframes glowRing{0%{box-shadow:0 30px 90px rgba(0,0,0,.34),0 0 0 0 rgba(255,105,180,.0)}40%{box-shadow:0 30px 90px rgba(0,0,0,.34),0 0 40px 12px rgba(255,105,180,.35)}100%{box-shadow:0 30px 90px rgba(0,0,0,.34)}}
.title{font-family:"Great Vibes",cursive;color:#ff69b4;text-align:center;font-size:clamp(2.4rem,6.2vw,4.1rem);margin-bottom:10px;text-shadow:0 6px 22px rgba(255,105,180,.35)}
.p{font-weight:800;color:#ab49cc;line-height:2;font-size:clamp(1.08rem,1.75vw,1.22rem);margin:0 0 14px;opacity:0;transform:translateY(10px)}
.p.reveal{animation:paraIn .7s ease forwards var(--d)}
@keyframes paraIn{to{opacity:1;transform:translateY(0)}}
.sign{display:flex;align-items:center;justify-content:flex-end;gap:14px;margin-top:4px;opacity:0;transform:translateY(10px)}
.sign.reveal{animation:paraIn .7s ease forwards .9s}
.sign span{font-family:"Great Vibes",cursive;color:#7f00b2;font-size:clamp(1.24rem,1.9vw,1.55rem)}
.sign img{width:84px;height:84px;object-fit:cover;border-radius:12px;box-shadow:0 8px 18px rgba(0,0,0,.18)}

/* aviso audio */
.notice{position:fixed;left:50%;bottom:72px;transform:translateX(-50%);z-index:60;display:none;gap:12px;align-items:center;background:rgba(255,255,255,.95);border:1px solid rgba(0,0,0,.08);padding:10px 16px;border-radius:14px;font-weight:800;color:#7a2c56;box-shadow:0 8px 18px rgba(0,0,0,.16)}
.notice .btn{cursor:pointer;border:none;padding:8px 12px;border-radius:999px;font-weight:800;background:linear-gradient(180deg,#ffd7ec,#ffc3e3);color:#7a2c56}
</style>
</head>
<body>
<div class="bg"></div>
<div class="rain" id="rain"></div>

<div class="stage">
  <!-- CORAZÓN -->
  <section class="heart-screen" id="heartScreen">
    <div class="banner" id="banner">🌸 El primero floreció.</div>
    <div class="heart-wrap">
      <div class="heart" id="heart">
        <svg viewBox="0 0 100 100" aria-hidden="true">
          <defs>
            <clipPath id="clipH">
              <path d="M50 86C50 86 9 61 9 36C9 23 20 12 33 12C41 12 47 16 50 22C53 16 59 12 67 12C80 12 91 23 91 36C91 61 50 86 50 86Z"/>
            </clipPath>
          </defs>
          <g clip-path="url(#clipH)">
            <rect id="level" class="level" x="10" y="86" width="80" height="0"></rect>
            <rect id="base" class="base" x="10" y="12" width="80" height="74"></rect>
            <g id="rise"></g>
            <g id="fill"></g>
          </g>
          <path class="outline" d="M50 86C50 86 9 61 9 36C9 23 20 12 33 12C41 12 47 16 50 22C53 16 59 12 67 12C80 12 91 23 91 36C91 61 50 86 50 86Z"/>
        </svg>
        <div id="popBox"></div>
      </div>
      <div class="progress" id="progress">Tulipanes: 0/18</div>
    </div>
    <div class="controls"><button class="btn" id="btnTulip">🌷 Haz florecer otro tulipán</button></div>
    <div class="msg4s" id="msg4s">Desde que llegaste, ya no hay espacio para nadie más.</div>
  </section>

  <!-- SOBRE -->
  <div class="env-wrap" id="envWrap" aria-hidden="true">
    <div class="envelope" id="env">
      <div class="env-body"></div>
      <div class="flapT" id="flapT"></div>
      <div class="flapL" id="flapL"></div>
      <div class="flapR" id="flapR"></div>
      <div class="ribbon" id="ribbon"></div>
      <div class="sheet" id="sheet"></div>
    </div>
  </div>

  <!-- CARTA -->
  <article class="letter" id="letter" aria-live="polite">
    <h2 class="title">No siempre que llueve es un desastre natural</h2>

    <p class="p" style="--d:.10s"><b>He pensado mucho en nosotras, en las veces que peleamos y en todo lo que pasa después. Sé que muchas veces eres tú quien da el primer paso, quien busca arreglar las cosas, quien intenta acercarse aunque siga dolida. Y sí, sé que te duele que yo no haga lo mismo. Que esperes que vaya detrás de ti y que no lo haga te hace sentir que no me importa, pero te juro que no es así.</b></p>

    <p class="p" style="--d:.30s"><b>A veces necesito quedarme callada, pensar, ordenar todo lo que siento antes de hablar. No porque quiera alejarme, sino porque tengo miedo de decir algo sin pensar y lastimarte más. No es falta de ganas, ni de amor, es solo mi forma de cuidar algo que me importa mucho: tú.</b></p>

    <p class="p" style="--d:.50s"><b>No sabes cuántas veces me he quedado con las ganas de escribirte, de correr detrás de ti, pero termino frenándome porque no quiero que mis palabras salgan desde el enojo o la confusión. Y sé que desde afuera puede parecer que no me importa, pero en realidad es todo lo contrario.</b></p>

    <p class="p" style="--d:.70s"><b>Porque incluso en esos momentos donde parece que todo se rompe, yo sigo pensando en ti, sigo queriendo que estés bien, sigo queriéndote. Y aunque a veces no lo diga o no lo demuestre de la forma que esperas, quiero que sepas que me importas más de lo que crees, y que, a pesar de todo, nunca he dejado de elegirte, solo intento hacerlo bien, sin lastimarte.</b></p>

    <div class="sign" id="sign"><span>te quiere con todo su corazón M</span><img src="photo_4900317553574480831_y.jpg" alt="Nosotras"></div>
  </article>
</div>

<!-- AUDIO -->
<audio id="song" src="morat.mp3" preload="auto" loop></audio>
<div class="notice" id="notice">Tu navegador bloqueó el audio. <button class="btn" id="playBtn" type="button">▶️ Reproducir</button></div>

<!-- Destello -->
<div class="flash" id="flash"></div>

<script>
/* ===== AUTOPLAY FIX: desbloqueo en 1ª interacción ===== */
const song = document.getElementById('song');
const notice = document.getElementById('notice');
const playBtn = document.getElementById('playBtn');
let audioUnlocked = false;

function tryUnlockAudio() {
  if (audioUnlocked) return;
  song.volume = 1.0;
  song.play().then(() => {
    song.pause();
    song.currentTime = 0;
    audioUnlocked = true;
    window.removeEventListener('pointerdown', tryUnlockAudio);
    window.removeEventListener('keydown', tryUnlockAudio);
  }).catch(()=>{ /* si falla, se mostrará aviso al abrir carta */ });
}
window.addEventListener('pointerdown', tryUnlockAudio);
window.addEventListener('keydown', tryUnlockAudio);

playBtn.addEventListener('click', () => {
  song.play().then(() => notice.style.display = 'none').catch(()=>{});
});

/* ===== Lluvia ===== */
const rain=document.getElementById('rain');const EM=['🌷','🍦'];
function droplet(){const d=document.createElement('div');d.className='drop';d.textContent=EM[Math.random()<.5?0:1];d.style.setProperty('--x',Math.random()*innerWidth+'px');d.style.setProperty('--r',(Math.random()-0.5)*60+'deg');d.style.setProperty('--dur',(Math.random()*5+6).toFixed(2)+'s');d.style.setProperty('--fs',(Math.random()*10+20|0)+'px');rain.appendChild(d);d.addEventListener('animationend',()=>d.remove())}
setInterval(droplet,320);for(let i=0;i<14;i++)droplet();

/* ===== Corazón (18 clics) ===== */
const btnTulip=document.getElementById('btnTulip'),progress=document.getElementById('progress'),
      banner=document.getElementById('banner'),msg4s=document.getElementById('msg4s'),
      heartScreen=document.getElementById('heartScreen');

const level=document.getElementById('level'),base=document.getElementById('base'),
      rise=document.getElementById('rise'),fill=document.getElementById('fill'),popBox=document.getElementById('popBox');

let clicks=0,total=18,busy=false,done=false;
const msgs=["🌸 El primero floreció.","🌷 Otro más, por ti.","💞 Late más fuerte.","✨ Ya se siente el amor.","🌷 Cada clic es cariño.","💗 Qué bonito va quedando.","🌸 Se llena de ti.","💞 Cada flor me recuerda a ti.","🌷 Ya casi, mi vida.","💖 Qué lindo está tu amor.","🌸 Sigue así, corazón.","💞 Casi lo logras.","🌷 Se ve hermoso.","💗 Falta poquito.","🌸 Ya casi, mi amor.","💞 Un poco más.","🌷 Último empujón.","💖 Lo llenaste todo."];
banner.textContent=msgs[0];progress.textContent=`Tulipanes: 0/${total}`;

const placed=[];function d2(a,b){const dx=a.x-b.x,dy=a.y-b.y;return dx*dx+dy*dy}
function addTulip(x,y,s){const t=document.createElementNS('http://www.w3.org/2000/svg','text');t.setAttribute('x',x.toFixed(2));t.setAttribute('y',y.toFixed(2));t.setAttribute('font-size',s);t.textContent='🌷';t.setAttribute('class','bloom');fill.appendChild(t)}
function pack(n,minD=26){let tries=0,add=0;while(add<n&&tries<500){tries++;const x=12+Math.random()*76,y=16+Math.random()*64,p={x,y};let ok=true;for(const q of placed){if(d2(p,q)<minD){ok=false;break}}if(ok){placed.push(p);addTulip(p.x,p.y,5.2+Math.random()*2.2);add++}}}
function riser(){const x=18+Math.random()*64,y=70+Math.random()*4,s=5.4+Math.random()*2.2;const t=document.createElementNS('http://www.w3.org/2000/svg','text');t.setAttribute('x',x.toFixed(2));t.setAttribute('y',y.toFixed(2));t.setAttribute('font-size',s);t.textContent='🌷';rise.appendChild(t);t.animate([{transform:'translateY(0)',opacity:.9},{transform:'translateY(-40px)',opacity:0}],{duration:900,easing:'ease-out'}).onfinish=()=>t.remove()}

/* POP sonoro + visual */
let ac;
function popSound(){try{if(!ac)ac=new (window.AudioContext||window.webkitAudioContext)();const t=ac.currentTime,o=ac.createOscillator(),g=ac.createGain();o.type='sine';o.frequency.setValueAtTime(680,t);o.frequency.exponentialRampToValueAtTime(260,t+0.09);g.gain.setValueAtTime(0.003,t);g.gain.exponentialRampToValueAtTime(0.00002,t+0.12);o.connect(g).connect(ac.destination);o.start(t);o.stop(t+0.14)}catch(e){}}
function popVisual(){const b=document.createElement('div');b.className='pop-burst';popBox.appendChild(b);b.addEventListener('animationend',()=>b.remove())}

function updateLevel(){const r=Math.min(clicks/total,1),H=74,h=H*r,y=86-h;level.setAttribute('y',y.toFixed(2));level.setAttribute('height',h.toFixed(2));base.setAttribute('opacity',(0.16+r*0.30).toFixed(2))}
function fillAll(){for(let gx=14;gx<=86;gx+=6){for(let gy=16;gy<=76;gy+=6){const dx=gx-50,dy=gy-56;if(dy<22||(dy*0.9+Math.abs(dx)*0.55)<38){placed.push({x:gx,y:gy});addTulip(gx,gy,5+Math.random()*2)}}}pack(120,18)}

function advance(){
  if(busy||done)return; busy=true;
  clicks++;
  popSound(); popVisual();
  pack(5,26); for(let i=0;i<3;i++)riser(); updateLevel();
  progress.textContent=`Tulipanes: ${clicks}/${total}`;
  banner.textContent=msgs[Math.min(clicks-1,msgs.length-1)]; // persiste hasta el siguiente clic

  if(clicks===total){
    fillAll();
    document.querySelector('.heart').classList.add('pulse');
    btnTulip.disabled=true; done=true;
    msg4s.classList.add('show');
    setTimeout(()=>{msg4s.classList.remove('show'); heartScreen.style.display='none'; showEnvelope();},4000);
  }
  setTimeout(()=>busy=false,140);
}
btnTulip.addEventListener('click',advance);
btnTulip.addEventListener('keydown',e=>{if(e.key==='Enter'||e.key===' '){e.preventDefault();advance()}});

/* ===== SOBRE y CARTA ===== */
const envWrap=document.getElementById('envWrap'),env=document.getElementById('env'),
      flapT=document.getElementById('flapT'),flapL=document.getElementById('flapL'),flapR=document.getElementById('flapR'),
      ribbon=document.getElementById('ribbon'),sheet=document.getElementById('sheet'),
      flash=document.getElementById('flash'),letter=document.getElementById('letter');

function showEnvelope(){
  envWrap.style.display='grid';
  requestAnimationFrame(()=>env.classList.add('show'));
  setTimeout(()=>ribbon.classList.add('draw'), 900);
  setTimeout(()=>{ribbon.classList.remove('draw'); ribbon.classList.add('unwrap'); sealBurst();}, 2200);
  setTimeout(openFlaps, 3300);
  setTimeout(()=>sheet.classList.add('show'), 4400);
  setTimeout(showLetter, 5700);
}

let opened=false;
function openFlaps(){
  if(opened) return; opened=true;
  flapT.style.transform='rotateX(-178deg)';
  flapL.style.transform='rotateY(-176deg)';
  flapR.style.transform='rotateY(176deg)';
}
function sealBurst(){
  const pieces=48, arr=['🌷','🍦','💗'];
  for(let i=0;i<pieces;i++){
    const s=document.createElement('div');s.className='spark';
    s.textContent=arr[Math.random()<.4?0:(Math.random()<.5?1:2)];
    const ang=(Math.PI*2)*(i/pieces),dist=110+Math.random()*170;
    const cx=innerWidth/2, cy=innerHeight/2;
    s.style.left=cx+'px'; s.style.top=cy+'px';
    s.style.fontSize=(16+Math.random()*16|0)+'px';
    document.body.appendChild(s);
    s.animate(
      [{transform:'translate(-50%,-50%) scale(1)',opacity:1},
       {transform:`translate(${Math.cos(ang)*dist}px,${Math.sin(ang)*dist}px) scale(.9)`,opacity:0}],
      {duration:1400+Math.random()*700,easing:'cubic-bezier(.22,1,.36,1)'}
    ).onfinish=()=>s.remove();
  }
  flash.classList.add('show'); setTimeout(()=>flash.classList.remove('show'),1700);
}

/* Carta: giro hacia ti + párrafos en cascada y música */
function showLetter(){
  envWrap.style.display='none';
  letter.classList.add('show');

  // revelar párrafos en cascada
  document.querySelectorAll('.p').forEach(p=>p.classList.add('reveal'));
  document.getElementById('sign').classList.add('reveal');

  // música
  if (audioUnlocked) {
    song.play().catch(()=>notice.style.display='flex');
  } else {
    notice.style.display = 'flex';
  }
}
</script>
</body>
</html>
