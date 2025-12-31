<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>عد تنازلي رأس السنة مع أنمي وألعاب نارية</title>
<style>
    body{
        background:black;
        color:white;
        font-family:Arial, sans-serif;
        display:flex;
        justify-content:center;
        align-items:center;
        height:100vh;
        flex-direction:column;
        overflow:hidden;
        position:relative;
    }
    #count{
        font-size:50px;
        margin-bottom:20px;
        z-index:10;
    }
    .firework{
        position:absolute;
        width:5px;
        height:5px;
        border-radius:50%;
        background:yellow;
        animation:explode 1s ease-out forwards;
    }
    @keyframes explode{
        0% {transform: scale(1) translate(0,0); opacity:1;}
        100% {transform: scale(20) translate(calc(var(--x)*1px), calc(var(--y)*1px)); opacity:0;}
    }
    .anime-img, .dance-img{
        position:absolute;
        width:100px;
        height:100px;
        pointer-events:none;
        animation:floatAnime 3s ease-in-out infinite;
    }
    @keyframes floatAnime{
        0% {transform: translateY(0) rotate(0deg);}
        50% {transform: translateY(-30px) rotate(15deg);}
        100% {transform: translateY(0) rotate(0deg);}
    }
</style>
</head>
<body>

<h2>العد التنازلي لرأس السنة</h2>
<div id="count">Loading...</div>

<script>
// الوقت المستهدف: منتصف الليل
var target = new Date(new Date().getFullYear() + 1, 0, 1, 0, 0, 0).getTime();

function createFirework(){
    for(let i=0;i<40;i++){
        let fw = document.createElement('div');
        fw.className = 'firework';
        fw.style.setProperty('--x', Math.random()*200-100);
        fw.style.setProperty('--y', Math.random()*200-100);
        fw.style.background = `hsl(${Math.random()*360},100%,50%)`;
        fw.style.left = `${window.innerWidth/2}px`;
        fw.style.top = `${window.innerHeight/2}px`;
        document.body.appendChild(fw);
        setTimeout(()=>fw.remove(),1200);
    }
}

// إضافة صور أنمي عامة
function createAnime(){
    const anime = document.createElement('img');
    anime.src = 'https://i.ibb.co/NsXf7gM/anime.png';
    anime.className = 'anime-img';
    anime.style.left = `${Math.random()*(window.innerWidth-100)}px`;
    anime.style.top = `${Math.random()*(window.innerHeight-100)}px`;
    document.body.appendChild(anime);
    setTimeout(()=>anime.remove(),5000);
}

// إضافة ناروتو وإيرن يرقصوا
function createDancers(){
    const dancers = [
        'https://i.ibb.co/XxZ5JhX/naruto-dance.gif', // GIF ناروتو
        'https://i.ibb.co/9v2xgDc/eren-dance.gif'    // GIF إيرن
    ];
    dancers.forEach(url=>{
        const d = document.createElement('img');
        d.src = url;
        d.className = 'dance-img';
        d.style.width = '120px';
        d.style.height = '120px';
        d.style.left = `${Math.random()*(window.innerWidth-120)}px`;
        d.style.top = `${Math.random()*(window.innerHeight-120)}px`;
        document.body.appendChild(d);
        setTimeout(()=>d.remove(),5000);
    });
}

var interval = setInterval(function(){
    var now = new Date().getTime();
    var diff = target - now;

    if(diff > 0){
        var days = Math.floor(diff / (1000*60*60*24));
        var hours = Math.floor((diff % (1000*60*60*24)) / (1000*60*60));
        var minutes = Math.floor((diff % (1000*60*60)) / (1000*60));
        var seconds = Math.floor((diff % (1000*60)) / 1000);

        document.getElementById("count").innerHTML =
            days +" يوم | "+ hours +" ساعة | "+ minutes +" دقيقة | "+ seconds +" ثانية";
    } else {
        clearInterval(interval);
        document.getElementById("count").innerHTML = "سنة جديدة سعيدة!";
        createFirework();
        createAnime();
        createDancers();
        setInterval(createFirework, 1000); // استمرار الألعاب النارية
        setInterval(createAnime, 2000);    // صور أنمي متكررة
        setInterval(createDancers, 2500);  // ناروتو وإيرن يرقصوا بشكل متكرر
    }
},1000);
</script>

</body>
</html>
