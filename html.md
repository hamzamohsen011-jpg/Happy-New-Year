<!DOCTYPE html>

<html lang="ar">

<head>

<meta charset="UTF-8">

<title>عد تنازلي رأس السنة مع أنمي وألعاب نارية</title>

<style>

&nbsp;   body{

&nbsp;       background:black;

&nbsp;       color:white;

&nbsp;       font-family:Arial, sans-serif;

&nbsp;       display:flex;

&nbsp;       justify-content:center;

&nbsp;       align-items:center;

&nbsp;       height:100vh;

&nbsp;       flex-direction:column;

&nbsp;       overflow:hidden;

&nbsp;       position:relative;

&nbsp;   }

&nbsp;   #count{

&nbsp;       font-size:50px;

&nbsp;       margin-bottom:20px;

&nbsp;       z-index:10;

&nbsp;   }

&nbsp;   .firework{

&nbsp;       position:absolute;

&nbsp;       width:5px;

&nbsp;       height:5px;

&nbsp;       border-radius:50%;

&nbsp;       background:yellow;

&nbsp;       animation:explode 1s ease-out forwards;

&nbsp;   }

&nbsp;   @keyframes explode{

&nbsp;       0% {transform: scale(1) translate(0,0); opacity:1;}

&nbsp;       100% {transform: scale(20) translate(calc(var(--x)\*1px), calc(var(--y)\*1px)); opacity:0;}

&nbsp;   }

&nbsp;   .anime-img, .dance-img{

&nbsp;       position:absolute;

&nbsp;       width:100px;

&nbsp;       height:100px;

&nbsp;       pointer-events:none;

&nbsp;       animation:floatAnime 3s ease-in-out infinite;

&nbsp;   }

&nbsp;   @keyframes floatAnime{

&nbsp;       0% {transform: translateY(0) rotate(0deg);}

&nbsp;       50% {transform: translateY(-30px) rotate(15deg);}

&nbsp;       100% {transform: translateY(0) rotate(0deg);}

&nbsp;   }

</style>

</head>

<body>



<h2>العد التنازلي لرأس السنة</h2>

<div id="count">Loading...</div>



<script>

// الوقت المستهدف: منتصف الليل

var target = new Date(new Date().getFullYear() + 1, 0, 1, 0, 0, 0).getTime();



function createFirework(){

&nbsp;   for(let i=0;i<40;i++){

&nbsp;       let fw = document.createElement('div');

&nbsp;       fw.className = 'firework';

&nbsp;       fw.style.setProperty('--x', Math.random()\*200-100);

&nbsp;       fw.style.setProperty('--y', Math.random()\*200-100);

&nbsp;       fw.style.background = `hsl(${Math.random()\*360},100%,50%)`;

&nbsp;       fw.style.left = `${window.innerWidth/2}px`;

&nbsp;       fw.style.top = `${window.innerHeight/2}px`;

&nbsp;       document.body.appendChild(fw);

&nbsp;       setTimeout(()=>fw.remove(),1200);

&nbsp;   }

}



// إضافة صور أنمي عامة

function createAnime(){

&nbsp;   const anime = document.createElement('img');

&nbsp;   anime.src = 'https://i.ibb.co/NsXf7gM/anime.png';

&nbsp;   anime.className = 'anime-img';

&nbsp;   anime.style.left = `${Math.random()\*(window.innerWidth-100)}px`;

&nbsp;   anime.style.top = `${Math.random()\*(window.innerHeight-100)}px`;

&nbsp;   document.body.appendChild(anime);

&nbsp;   setTimeout(()=>anime.remove(),5000);

}



// إضافة ناروتو وإيرن يرقصوا

function createDancers(){

&nbsp;   const dancers = \[

&nbsp;       'https://i.ibb.co/XxZ5JhX/naruto-dance.gif', // GIF ناروتو

&nbsp;       'https://i.ibb.co/9v2xgDc/eren-dance.gif'    // GIF إيرن

&nbsp;   ];

&nbsp;   dancers.forEach(url=>{

&nbsp;       const d = document.createElement('img');

&nbsp;       d.src = url;

&nbsp;       d.className = 'dance-img';

&nbsp;       d.style.width = '120px';

&nbsp;       d.style.height = '120px';

&nbsp;       d.style.left = `${Math.random()\*(window.innerWidth-120)}px`;

&nbsp;       d.style.top = `${Math.random()\*(window.innerHeight-120)}px`;

&nbsp;       document.body.appendChild(d);

&nbsp;       setTimeout(()=>d.remove(),5000);

&nbsp;   });

}



var interval = setInterval(function(){

&nbsp;   var now = new Date().getTime();

&nbsp;   var diff = target - now;



&nbsp;   if(diff > 0){

&nbsp;       var days = Math.floor(diff / (1000\*60\*60\*24));

&nbsp;       var hours = Math.floor((diff % (1000\*60\*60\*24)) / (1000\*60\*60));

&nbsp;       var minutes = Math.floor((diff % (1000\*60\*60)) / (1000\*60));

&nbsp;       var seconds = Math.floor((diff % (1000\*60)) / 1000);



&nbsp;       document.getElementById("count").innerHTML =

&nbsp;           days +" يوم | "+ hours +" ساعة | "+ minutes +" دقيقة | "+ seconds +" ثانية";

&nbsp;   } else {

&nbsp;       clearInterval(interval);

&nbsp;       document.getElementById("count").innerHTML = "سنة جديدة سعيدة!";

&nbsp;       createFirework();

&nbsp;       createAnime();

&nbsp;       createDancers();

&nbsp;       setInterval(createFirework, 1000); // استمرار الألعاب النارية

&nbsp;       setInterval(createAnime, 2000);    // صور أنمي متكررة

&nbsp;       setInterval(createDancers, 2500);  // ناروتو وإيرن يرقصوا بشكل متكرر

&nbsp;   }

},1000);

</script>



</body>

</html>

