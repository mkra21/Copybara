<!DOCTYPE html>
<html lang="en">

  <head>
    <meta charset="UTF-8">
    <title>Untitled</title>
    

  </head>
    
  <body>
  <!DOCTYPE html>
<html lang="km">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>រាត្រីលំហអាកាស • Music Player</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    font-family:'Khmer OS Battambang',sans-serif;

    background:
        linear-gradient(rgba(0,0,0,0.15), rgba(0,0,0,0.35)),
        url('https://files.catbox.moe/ka5x56.jpg') center/cover no-repeat;

    overflow:hidden;
}

/* Overlay ស្រាល */
.overlay{
    position:absolute;
    inset:0;
    z-index:1;
}

/* Player Card */
.player-card{
    position:relative;
    z-index:10;
    width:85%;
    max-width:360px;
    padding:35px;
    text-align:center;
    color:white;

    background:rgba(0,0,0,0.25);
    backdrop-filter:blur(14px);
    border-radius:30px;
    border:1px solid rgba(255,255,255,0.15);
    box-shadow:0 25px 60px rgba(0,0,0,0.8);
}

/* Disk */
.disk{
    width:130px;
    height:130px;
    margin:0 auto 25px;
    border-radius:50%;
    background:linear-gradient(45deg,#00d2ff,#3a7bd5);
    border:4px solid rgba(255,255,255,0.3);
    display:flex;
    align-items:center;
    justify-content:center;
    box-shadow:0 0 35px rgba(0,210,255,0.6);
    animation:rotate 10s linear infinite;
    animation-play-state:paused;
}

.disk.playing{
    animation-play-state:running;
}

@keyframes rotate{
    from{transform:rotate(0deg);}
    to{transform:rotate(360deg);}
}

h2{
    font-size:22px;
    margin-bottom:6px;
}

p{
    font-size:14px;
    opacity:.85;
    margin-bottom:30px;
}

/* Controls */
.controls{
    display:flex;
    justify-content:center;
    gap:20px;
}

.btn{
    width:55px;
    height:55px;
    border-radius:50%;
    font-size:20px;
    cursor:pointer;
    color:white;
    background:rgba(255,255,255,0.12);
    border:1px solid rgba(255,255,255,0.3);
    transition:.3s;
}

.btn:active{
    transform:scale(.9);
    background:rgba(255,255,255,0.3);
}

.btn-play{
    width:70px;
    height:70px;
    font-size:28px;
    background:white;
    color:black;
}

audio{display:none;}

/* Stars */
.star{
    position:absolute;
    background:white;
    border-radius:50%;
    opacity:.7;
    animation:twinkle 3s infinite;
    z-index:2;
}

@keyframes twinkle{
    0%,100%{opacity:.3;}
    50%{opacity:1;}
}

/* Shooting Stars */
.shooting-star{
    position:absolute;
    width:120px;
    height:2px;
    background:linear-gradient(90deg,white,transparent);
    opacity:.9;
    transform:rotate(-45deg);
    z-index:3;
    animation:shoot 2s linear infinite;
}

@keyframes shoot{
    from{
        transform:translateX(0) translateY(0) rotate(-45deg);
        opacity:1;
    }
    to{
        transform:translateX(-700px) translateY(700px) rotate(-45deg);
        opacity:0;
    }
}
</style>
</head>

<body>

<div class="overlay"></div>

<div class="player-card">
    <div class="disk" id="disk">
        <span style="font-size:50px;">🌍</span>
    </div>

    <h2 id="title">បទចម្រៀងទី ១</h2>
    <p>កំពុងចាក់ចម្រៀងបេះត្រជាក់</p>

    <div class="controls">
        <button class="btn" onclick="prevTrack()">⏮</button>
        <button class="btn btn-play" id="playBtn" onclick="togglePlay()">▶</button>
        <button class="btn" onclick="nextTrack()">⏭</button>
    </div>

    <audio id="mainAudio"></audio>
</div>

<script>
const audio=document.getElementById("mainAudio");
const playBtn=document.getElementById("playBtn");
const disk=document.getElementById("disk");
const title=document.getElementById("title");

const playlist=[
    {name:"បទចម្រៀងទី ១",link:"https://files.catbox.moe/rtkvkd.mp3"},
    {name:"បទចម្រៀងទី ២",link:""}
];

let trackIndex=0;

function loadTrack(i){
    audio.src=playlist[i].link;
    title.innerText=playlist[i].name;
}

function togglePlay(){
    if(audio.paused){
        audio.play();
        playBtn.innerText="⏸";
        disk.classList.add("playing");
    }else{
        audio.pause();
        playBtn.innerText="▶";
        disk.classList.remove("playing");
    }
}

function nextTrack(){
    trackIndex=(trackIndex+1)%playlist.length;
    loadTrack(trackIndex);
    audio.play();
    playBtn.innerText="⏸";
    disk.classList.add("playing");
}

function prevTrack(){
    trackIndex=(trackIndex-1+playlist.length)%playlist.length;
    loadTrack(trackIndex);
    audio.play();
    playBtn.innerText="⏸";
    disk.classList.add("playing");
}

loadTrack(trackIndex);

/* Stars */
for(let i=0;i<70;i++){
    const star=document.createElement("div");
    star.className="star";
    const size=Math.random()*3+1+"px";
    star.style.width=size;
    star.style.height=size;
    star.style.top=Math.random()*100+"vh";
    star.style.left=Math.random()*100+"vw";
    star.style.animationDelay=Math.random()*3+"s";
    document.body.appendChild(star);
}

/* Shooting Stars */
function createShootingStar(){
    const star=document.createElement("div");
    star.className="shooting-star";
    star.style.top=Math.random()*40+"vh";
    star.style.left=Math.random()*100+"vw";
    star.style.animationDuration=Math.random()*1.5+1+"s";
    document.body.appendChild(star);
    setTimeout(()=>star.remove(),2000);
}
setInterval(createShootingStar,900);
</script>

</body>
</html>
    
  </body>
  
</html>
