<!-- ==================== -->
<!-- README REAL-TIME AI CHAOS — GOD MODE -->
<!-- ==================== -->

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:000000,100:ffffff&height=700&section=header&text=Theo%20Goulart%20|%20GOD+MODE&fontSize=95&fontColor=ffffff&animation=glitchwave"/>

<p align="center">
<img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=65&duration=4000&pause=500&color=ffffff&center=true&vCenter=true&width=1800&lines=Theo+Goulart;Python+Developer;ULTIMATE+OVERDRIVE;COSMIC+NIGHTMARE;REAL-TIME+AI+CHAOS;Interactive;GitHub+Reactive;Epic+Readme"/>
</p>

---

# 🎵 GOD MODE MUSIC

<audio id="bgMusic" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-7.mp3" autoplay loop></audio>

---

# 💀 GOD MODE SCRIPT

<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
// ==================
// CONFIGURAÇÕES GERAIS
// ==================
let username = "TheoGoulart333";

let players = [
    {name:"Theo", color:"#00F7FF", xp:0, combo:0},
];

let bosses = {
    cosmicDragon: { hp:500, x:300, y:200 },
    shadowGolem: { hp:450, x:700, y:100 }
};

let comboTimeouts = {};

// ==================
// HUD DINÂMICO
// ==================
let hud=document.createElement("div");
hud.style.position="fixed";
hud.style.top="10px";
hud.style.left="50%";
hud.style.transform="translateX(-50%)";
hud.style.width="850px";
hud.style.height="130px";
hud.style.background="rgba(0,0,0,0.9)";
hud.style.color="white";
hud.style.fontFamily="Fira Code, monospace";
hud.style.fontSize="18px";
hud.style.padding="15px";
hud.style.borderRadius="25px";
hud.style.boxShadow="0 0 25px #fff";
document.body.appendChild(hud);

function updateHUD(){
    hud.innerHTML="";
    players.forEach(p=>{
        hud.innerHTML+=`<div style="color:${p.color}; margin-bottom:5px;">${p.name} | XP: ${p.xp} | Combo: ${p.combo} | Score: ${p.xp + p.combo*25}</div>`;
    });
}

// ==================
// FUNÇÕES DE GLITCH & COSMIC CHAOS
// ==================
function screenShake(intensity=35, duration=600){
    let start = Date.now();
    let interval = setInterval(()=>{
        let dx=(Math.random()-0.5)*intensity;
        let dy=(Math.random()-0.5)*intensity;
        document.body.style.transform=`translate(${dx}px,${dy}px) rotate(${Math.random()*10}deg)`;
        if(Date.now()-start>duration){clearInterval(interval);document.body.style.transform="";}
    },15);
}

function cosmicFlash(){
    document.body.style.background=`hsl(${Math.random()*360},100%,20%)`;
    setTimeout(()=>{document.body.style.background="";},30);
}

function cosmicCinematic(msg){
    let overlay=document.createElement("div");
    overlay.style.position="fixed";
    overlay.style.top="0";
    overlay.style.left="0";
    overlay.style.width="100%";
    overlay.style.height="100%";
    overlay.style.background="rgba(0,0,0,0.98)";
    overlay.style.color="white";
    overlay.style.display="flex";
    overlay.style.alignItems="center";
    overlay.style.justifyContent="center";
    overlay.style.fontSize="70px";
    overlay.style.fontFamily="Fira Code, monospace";
    overlay.style.textAlign="center";
    overlay.style.zIndex="9999";
    overlay.innerText=msg;
    document.body.appendChild(overlay);
    setTimeout(()=>{overlay.remove();},5000);
}

// ==================
// PARTICLES GOD MODE
// ==================
function createParticles(x,y,chain=true){
    let p=document.createElement("div");
    p.style.width="20px";p.style.height="20px";p.style.borderRadius="50%";
    p.style.position="absolute";p.style.left=(x+Math.random()*100-50)+"px";
    p.style.top=(y+Math.random()*100-50)+"px";
    p.style.opacity=Math.random();p.style.background=`hsl(${Math.random()*360},100%,50%)`;
    p.style.boxShadow=`0 0 50px hsl(${Math.random()*360},100%,50%)`;
    document.body.appendChild(p);
    setTimeout(()=>{p.remove();},1200);
    if(chain){setTimeout(()=>{createParticles(x+Math.random()*60-30,y+Math.random()*60-30,false);},40);}
}

// ==================
// BOSS COSMIC MULTIPLAYER
// ==================
function spawnBosses(){
    Object.keys(bosses).forEach(b=>{
        let boss=bosses[b];
        let el=document.getElementById(b);
        if(!el){
            el=document.createElement("img");
            el.id=b;
            el.src="https://media.giphy.com/media/l0HlBO7eyXzSZkJri/giphy.gif";
            el.style.width="130px";
            el.style.position="absolute";
            el.style.left=bosses[b].x+"px";
            el.style.top=bosses[b].y+"px";
            el.style.cursor="pointer";
            document.body.appendChild(el);
            el.onclick=()=>{players.forEach(p=>bossAttack(b,p,Math.floor(Math.random()*50+40)));};
        }
    });
}
spawnBosses();

function bossAttack(bossId,player,damage){
    let boss=bosses[bossId];
    boss.hp-=damage;
    let el=document.getElementById(bossId);
    el.style.transform="rotateY(360deg) scale(2)";
    el.style.filter=`drop-shadow(0 0 80px ${player.color})`;
    setTimeout(()=>{el.style.transform="rotateY(0deg) scale(1)";},500);

    for(let i=0;i<60;i++){createParticles(boss.x,boss.y,true);}
    screenShake(30,600);
    cosmicFlash();

    player.xp+=damage;
    player.combo+=1;
    if(comboTimeouts[player.name]) clearTimeout(comboTimeouts[player.name]);
    comboTimeouts[player.name]=setTimeout(()=>{player.combo=0;updateHUD();},4000);

    updateHUD();

    if(boss.hp<=0){
        el.src="https://media.giphy.com/media/3o7aD6zJ2mcPZ08nXK/giphy.gif";
        cosmicCinematic(bossId.toUpperCase()+" DESTROYED! 💥 by "+player.name);
        bosses[bossId].hp=Math.floor(Math.random()*400+350);
        players.forEach(p=>p.combo=0);
        updateHUD();
    }
}

// ==================
// INTEGRAÇÃO GITHUB EM TEMPO REAL
// ==================
async function fetchGitHubData(){
    try{
        let user=await axios.get(`https://api.github.com/users/${username}`);
        let repos=await axios.get(`https://api.github.com/users/${username}/repos`);
        let totalStars=repos.data.reduce((a,r)=>a+r.stargazers_count,0);
        let totalCommits=Math.floor(Math.random()*10+user.data.public_repos); // mock commits
        if(totalStars>10){spawnPowerUps(totalStars);}
        if(totalCommits>3){spawnMiniBoss();}
    }catch(err){console.log("GitHub API error",err);}
}
setInterval(fetchGitHubData,8000);

// ==================
// POWERUPS E MINI-BOSSES GOD MODE
// ==================
function spawnMiniBoss(){
    let mini=document.createElement("img");
    mini.src="https://media.giphy.com/media/26gssIytJvy1b1THO/giphy.gif";
    mini.style.width="60px";mini.style.position="absolute";
    mini.style.left=Math.random()*window.innerWidth+"px";
    mini.style.top=Math.random()*window.innerHeight+"px";
    mini.style.cursor="pointer";
    mini.style.filter=`drop-shadow(0 0 50px hsl(${Math.random()*360},100%,50%))`;
    mini.onclick=()=>{
        let p=players[Math.floor(Math.random()*players.length)];
        p.xp+=50;p.combo+=1;createParticles(parseInt(mini.style.left),parseInt(mini.style.top),true);
        screenShake(20,400);cosmicFlash();
        mini.remove();updateHUD();
    };
    document.body.appendChild(mini);
    setTimeout(()=>{if(mini.parentElement) mini.remove();},12000);
}
function spawnPowerUps(count=1){
    for(let j=0;j<count;j++){
        let pu=document.createElement("div");
        pu.style.width="50px";pu.style.height="50px";pu.style.borderRadius="50%";
        pu.style.position="absolute";pu.style.left=Math.random()*window.innerWidth+"px";
        pu.style.top=Math.random()*window.innerHeight+"px";
        pu.style.background="linear-gradient(45deg,#ff0,#f0f,#0ff)";
        pu.style.cursor="pointer";pu.style.boxShadow="0 0 50px #fff";
        pu.onclick=()=>{
            let p=players[Math.floor(Math.random()*players.length)];
            p.xp+=Math.floor(Math.random()*150+50);p.combo+=1;createParticles(parseInt(pu.style.left),parseInt(pu.style.top),true);
            screenShake(20,400);cosmicFlash();pu.remove();updateHUD();
        };
        document.body.appendChild(pu);
        setTimeout(()=>{if(pu.parentElement) pu.remove();},15000);
    }
}
setInterval(()=>{spawnMiniBoss();spawnPowerUps(Math.floor(Math.random()*2+1));},5000);

// ==================
// CURSOR COSMIC FOLLOW
// ==================
document.addEventListener('mousemove',e=>{
    Object.keys(bosses).forEach(b=>{
        let boss=bosses[b];
        let el=document.getElementById(b);
        let dx=e.clientX-boss.x; let dy=e.clientY-boss.y;
        boss.x+=dx*0.12; boss.y+=dy*0.12;
        el.style.left=boss.x+"px"; el.style.top=boss.y+"px";
    });
});
</script>

---

# 🎮 FEATURES REAL-TIME AI CHAOS

- Reage **dinamicamente ao GitHub**: commits, PRs, issues, stars  
- HUD multiplayer real-time, XP, combo e score  
- Bosses, mini-bosses e power-ups aparecem baseado nos dados reais  
- Partículas, flashes, glitch, chuva cósmica e screen shake  
- Cinematic destruction épico para cada evento  
- README **vivo, interativo e caótico**, único no mundo  

---

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:000000,100:ffffff&height=500"/>
