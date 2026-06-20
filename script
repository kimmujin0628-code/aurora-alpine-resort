/* ── LOADER ─────────────────────────────────── */
window.addEventListener('load',()=>{
  setTimeout(()=>{
    document.getElementById('loader').classList.add('hidden');
    document.body.style.overflow='';
  },2400);
});
document.body.style.overflow='hidden';

/* ── AURORA CANVAS ──────────────────────────── */
(function(){
  const canvas=document.getElementById('aurora-canvas');
  const ctx=canvas.getContext('2d');
  let W,H,t=0;
  function resize(){W=canvas.width=canvas.offsetWidth;H=canvas.height=canvas.offsetHeight}
  resize();
  window.addEventListener('resize',resize);

  const streams=[
    {y:0.32,color:'rgba(45,71,57,',speed:0.0004,amp:0.10,freq:1.8,phase:0},
    {y:0.48,color:'rgba(201,168,118,',speed:0.0003,amp:0.07,freq:2.2,phase:2.1},
    {y:0.62,color:'rgba(22,38,68,',speed:0.00035,amp:0.11,freq:1.5,phase:4.3},
    {y:0.22,color:'rgba(55,38,80,',speed:0.00025,amp:0.06,freq:2.8,phase:1.6},
  ];

  function draw(){
    ctx.clearRect(0,0,W,H);
    streams.forEach(s=>{
      const yBase=H*s.y;
      const grad=ctx.createLinearGradient(0,yBase-H*s.amp*1.5,0,yBase+H*s.amp*1.5);
      const alpha=0.18+0.12*Math.sin(t*s.speed*3000+s.phase);
      grad.addColorStop(0,s.color+'0)');
      grad.addColorStop(0.5,s.color+alpha+')');
      grad.addColorStop(1,s.color+'0)');
      ctx.beginPath();
      ctx.moveTo(0,yBase);
      for(let x=0;x<=W;x+=4){
        const noise=Math.sin(x*s.freq*0.003+t*s.speed*1000+s.phase)
          *Math.cos(x*s.freq*0.0015+t*s.speed*700)
          *H*s.amp;
        ctx.lineTo(x,yBase+noise);
      }
      ctx.lineTo(W,H);ctx.lineTo(0,H);ctx.closePath();
      ctx.fillStyle=grad;
      ctx.fill();
    });
    t=Date.now();
    requestAnimationFrame(draw);
  }
  t=Date.now();
  draw();
})();

/* ── CURSOR ─────────────────────────────────── */
(function(){
  const dot=document.getElementById('cursor-dot');
  const ring=document.getElementById('cursor-ring');
  let mx=0,my=0,rx=0,ry=0;
  document.addEventListener('mousemove',e=>{mx=e.clientX;my=e.clientY;});
  function tick(){
    dot.style.left=mx+'px';dot.style.top=my+'px';
    rx+=(mx-rx)*0.12;ry+=(my-ry)*0.12;
    ring.style.left=rx+'px';ring.style.top=ry+'px';
    requestAnimationFrame(tick);
  }
  tick();
})();

/* ── AMBIENT MOUSE LIGHT ─────────────────────── */
document.addEventListener('mousemove',e=>{
  document.getElementById('ambient').style.background=
    `radial-gradient(500px circle at ${e.clientX}px ${e.clientY}px,rgba(201,168,118,0.03),transparent 65%)`;
});

/* ── NAV SCROLL ─────────────────────────────── */
const nav=document.getElementById('nav');
window.addEventListener('scroll',()=>{
  nav.classList.toggle('scrolled',window.scrollY>60);
},{ passive:true });

/* ── MOBILE NAV ─────────────────────────────── */
const mobileNav=document.getElementById('mobile-nav');
document.getElementById('hamburger').addEventListener('click',()=>mobileNav.classList.add('open'));
document.querySelector('.mobile-close').addEventListener('click',()=>mobileNav.classList.remove('open'));
mobileNav.querySelectorAll('a').forEach(a=>a.addEventListener('click',()=>mobileNav.classList.remove('open')));

/* ── SCROLL REVEAL ──────────────────────────── */
const revealObs=new IntersectionObserver((entries)=>{
  entries.forEach(e=>{if(e.isIntersecting){e.target.classList.add('visible');revealObs.unobserve(e.target);}});
},{threshold:0.12,rootMargin:'0px 0px -60px 0px'});
document.querySelectorAll('.reveal').forEach(el=>revealObs.observe(el));

/* ── TESTIMONIALS ───────────────────────────── */
(function(){
  const slides=document.querySelectorAll('.testi-slide');
  const dots=document.querySelectorAll('.testi-dot');
  let current=0,auto;

  function go(n){
    slides[current].classList.remove('active');
    dots[current].classList.remove('active');
    current=(n+slides.length)%slides.length;
    slides[current].classList.add('active');
    dots[current].classList.add('active');
  }
  function startAuto(){auto=setInterval(()=>go(current+1),5200);}
  function resetAuto(){clearInterval(auto);startAuto();}

  document.getElementById('testi-next').addEventListener('click',()=>{go(current+1);resetAuto();});
  document.getElementById('testi-prev').addEventListener('click',()=>{go(current-1);resetAuto();});
  dots.forEach((d,i)=>d.addEventListener('click',()=>{go(i);resetAuto();}));
  startAuto();
})();

/* ── RESERVATION SUBMIT ─────────────────────── */
document.getElementById('res-submit').addEventListener('click',function(){
  const btn=this;
  const orig=btn.textContent;
  btn.textContent='Checking Availability…';
  btn.disabled=true;
  setTimeout(()=>{
    btn.textContent='✓  Request Confirmed — We Will Contact You Shortly';
    btn.style.background='var(--green)';
    btn.style.color='var(--ivory)';
    setTimeout(()=>{btn.textContent=orig;btn.disabled=false;btn.style.background='';btn.style.color='';},5000);
  },1800);
});

/* ── PARALLAX HERO ──────────────────────────── */
const heroCanvas=document.getElementById('aurora-canvas');
window.addEventListener('scroll',()=>{
  const y=window.scrollY;
  heroCanvas.style.transform=`translateY(${y*0.3}px)`;
},{ passive:true });

/* ── EXPERIENCE DRAG SCROLL ─────────────────── */
(function(){
  const track=document.querySelector('.exp-track');
  if(!track)return;
  let isDown=false,startX,scrollLeft;
  track.addEventListener('mousedown',e=>{isDown=true;track.style.cursor='grabbing';startX=e.pageX-track.offsetLeft;scrollLeft=track.scrollLeft;});
  track.addEventListener('mouseleave',()=>{isDown=false;track.style.cursor='';});
  track.addEventListener('mouseup',()=>{isDown=false;track.style.cursor='';});
  track.addEventListener('mousemove',e=>{if(!isDown)return;e.preventDefault();const x=e.pageX-track.offsetLeft;track.scrollLeft=scrollLeft-(x-startX)*1.2;});
})();
