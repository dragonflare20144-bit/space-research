<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>Space Research Hub</title>

<script src="https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.min.js"></script>

<style>
*{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{
    font-family:Arial,Helvetica,sans-serif;
    background:#02030a;
    color:white;
    overflow-x:hidden
}
button,input{font:inherit}

/* LOGIN */
#loginPage{
    min-height:100vh;
    display:flex;
    align-items:center;
    justify-content:center;
    position:relative;
    overflow:hidden;
    background:
    radial-gradient(circle at 50% 35%,#182967,#070b20 35%,#02030a 75%)
}
.login-stars{
    position:absolute;
    inset:0;
    background-image:radial-gradient(circle,#fff 1px,transparent 1px);
    background-size:85px 85px;
    opacity:.3;
}
.login-box{
    position:relative;
    z-index:2;
    width:390px;
    max-width:92%;
    padding:40px;
    border:1px solid #3a4f91;
    border-radius:20px;
    background:rgba(6,10,29,.9);
    box-shadow:0 0 45px rgba(50,90,210,.25);
    backdrop-filter:blur(12px)
}
.login-logo{text-align:center;font-size:44px;margin-bottom:8px}
.login-box h1{text-align:center;color:#9eb3ff}
.login-box>p{text-align:center;color:#8792b2;margin:8px 0 28px}
.input-group{margin-bottom:17px}
.input-group label{
    display:block;
    color:#aab6d6;
    font-size:13px;
    margin-bottom:7px
}
.input-group input{
    width:100%;
    padding:13px;
    border-radius:9px;
    border:1px solid #354675;
    background:#060a18;
    color:white;
    outline:none
}
.input-group input:focus{
    border-color:#738fff;
    box-shadow:0 0 12px #4261c833
}
.login-btn{
    width:100%;
    padding:14px;
    border:0;
    border-radius:9px;
    color:white;
    font-weight:bold;
    cursor:pointer;
    background:linear-gradient(90deg,#3159db,#7345dc)
}
.login-error{
    min-height:18px;
    margin-top:13px;
    text-align:center;
    color:#ff6f7b;
    font-size:13px
}

/* MAIN */
#website{display:none}
nav{
    position:fixed;
    top:0;
    left:0;
    right:0;
    height:65px;
    z-index:1000;
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding:0 32px;
    background:#030510e8;
    border-bottom:1px solid #17244a;
    backdrop-filter:blur(12px)
}
.nav-logo{font-weight:bold;color:#9eb2ff}
.nav-links{display:flex;gap:20px;align-items:center}
.nav-links button{
    border:0;
    background:none;
    color:#a8b2cf;
    cursor:pointer
}
.nav-links button:hover{color:white}
.logout-btn{
    border:1px solid #354574!important;
    padding:8px 12px;
    border-radius:7px
}

/* HERO */
.hero{
    min-height:100vh;
    position:relative;
    display:flex;
    align-items:center;
    justify-content:center;
    text-align:center;
    overflow:hidden;
    background:
    radial-gradient(circle at 50% 45%,#172861,#060a1d 38%,#02030a 75%)
}
.hero-stars{
    position:absolute;
    inset:0;
    background-image:radial-gradient(circle,#fff 1px,transparent 1px);
    background-size:100px 100px;
    opacity:.3
}
.hero-content{
    position:relative;
    z-index:2;
    max-width:850px;
    padding:30px
}
.hero-content h1{
    font-size:clamp(45px,8vw,85px);
    margin-bottom:20px;
    background:linear-gradient(90deg,#8caaff,#dcc9ff,#89ddff);
    -webkit-background-clip:text;
    color:transparent
}
.hero-content p{
    color:#a5b0cf;
    line-height:1.7;
    font-size:18px;
    margin-bottom:30px
}
.hero-buttons{
    display:flex;
    justify-content:center;
    flex-wrap:wrap;
    gap:14px
}
.primary-btn,.secondary-btn{
    padding:14px 22px;
    border-radius:10px;
    cursor:pointer;
    font-weight:bold
}
.primary-btn{
    color:white;
    border:0;
    background:linear-gradient(90deg,#3159db,#7048d8)
}
.secondary-btn{
    color:white;
    border:1px solid #40558e;
    background:#060a18aa
}

/* SECTIONS */
.section{padding:100px 7%;min-height:450px}
.section-title{text-align:center;font-size:40px;margin-bottom:14px}
.section-subtitle{
    max-width:720px;
    margin:0 auto 40px;
    text-align:center;
    color:#8c97b5;
    line-height:1.6
}
.research-grid{
    max-width:1100px;
    margin:auto;
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
    gap:20px
}
.research-card{
    padding:25px;
    border:1px solid #202e59;
    border-radius:15px;
    background:linear-gradient(145deg,#0e1735cc,#050817e8)
}
.research-card:hover{
    border-color:#526dbd;
    transform:translateY(-5px)
}
.research-card .icon{font-size:35px;margin-bottom:14px}
.research-card h3{margin-bottom:9px}
.research-card p{color:#8995b5;line-height:1.6}
.about{
    max-width:850px;
    margin:auto;
    text-align:center;
    color:#929dbc;
    line-height:1.8
}
footer{
    padding:30px;
    text-align:center;
    color:#667391;
    border-top:1px solid #172344
}

/* PLANET SELECTOR */
#planetSelector{display:none;min-height:100vh;padding:100px 6%;background:#02040c}
.planet-grid{
    max-width:1100px;
    margin:auto;
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
    gap:20px
}
.planet-card{
    min-height:210px;
    padding:25px;
    border:1px solid #263662;
    border-radius:16px;
    background:#080d20;
    cursor:pointer;
    text-align:center;
    transition:.25s
}
.planet-card:hover{
    transform:translateY(-7px) scale(1.02);
    border-color:#728be0;
    box-shadow:0 15px 35px #0008
}
.planet-preview{
    width:105px;
    height:105px;
    border-radius:50%;
    margin:0 auto 20px;
    box-shadow:
    inset -22px -15px 35px #0009,
    0 0 25px #ffffff18
}
.mercury{background:radial-gradient(circle at 35% 30%,#c7c4bd,#77736e 45%,#393735)}
.venus{background:radial-gradient(circle at 35% 30%,#f2d18c,#c7853d 48%,#70431f)}
.earth{background:radial-gradient(circle at 35% 25%,#76c9ff,#1761a5 45%,#071c54)}
.mars{background:radial-gradient(circle at 35% 25%,#e98259,#a33c2c 50%,#511c1c)}
.jupiter{background:repeating-linear-gradient(0deg,#a47756 0 8px,#e5c99d 8px 17px,#956344 17px 24px)}
.saturn{background:radial-gradient(circle at 35% 25%,#ead29c,#ae8750 55%,#614a30)}
.uranus{background:radial-gradient(circle at 35% 25%,#a9f2f2,#55b9c5 60%,#276d83)}
.neptune{background:radial-gradient(circle at 35% 25%,#668dff,#2446b7 55%,#101e68)}
.back-btn{
    padding:10px 15px;
    border-radius:8px;
    border:1px solid #354675;
    background:#101832;
    color:white;
    cursor:pointer;
    margin-bottom:30px
}

/* GALAXIES */
#galaxyExplorer{
    display:none;
    position:fixed;
    inset:0;
    z-index:2000;
    background:#010208
}
#galaxyCanvas{
    position:absolute;
    inset:0;
    width:100%;
    height:100%
}
.galaxy-sidebar{
    position:absolute;
    top:80px;
    left:20px;
    z-index:5;
    width:220px;
    padding:18px;
    border:1px solid #293961;
    border-radius:14px;
    background:#050817e8;
    backdrop-filter:blur(10px)
}
.galaxy-sidebar h2{color:#9eb3ff;margin-bottom:14px}
.galaxy-item{
    padding:10px;
    border-radius:8px;
    color:#9aa5c5;
    cursor:pointer;
    margin-bottom:4px
}
.galaxy-item.active,.galaxy-item:hover{
    background:#172451;
    color:white
}
.galaxy-controls{
    border-top:1px solid #28375f;
    margin-top:14px;
    padding-top:12px
}
.galaxy-controls button{
    width:100%;
    padding:9px;
    margin-top:6px;
    border-radius:7px;
    border:1px solid #344675;
    background:#0c1430;
    color:white;
    cursor:pointer
}
.galaxy-info{
    position:absolute;
    right:25px;
    top:85px;
    z-index:5;
    width:300px;
    padding:20px;
    border:1px solid #293961;
    border-radius:14px;
    background:#050817d9
}
.galaxy-info h2{color:#aabaff;margin-bottom:8px}
.galaxy-info p{color:#929dbc;font-size:13px;line-height:1.6}

/* BLACK HOLES */
.blackhole-section{max-width:1150px;margin:auto}
.blackhole-grid{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:20px
}
.blackhole-card{
    height:360px;
    position:relative;
    overflow:hidden;
    border:1px solid #263662;
    border-radius:15px;
    background:#010208;
    cursor:grab
}
.blackhole-card:active{cursor:grabbing}
.blackhole-card canvas{width:100%;height:100%;display:block}
.blackhole-label{
    position:absolute;
    left:15px;
    right:15px;
    bottom:15px;
    pointer-events:none
}
.blackhole-label span{color:#7f8caf;font-size:12px}
.blackhole-status{
    position:absolute;
    right:12px;
    top:12px;
    z-index:10;
    padding:7px 10px;
    border-radius:8px;
    background:#000b;
    border:1px solid #405da0;
    color:#9eb6ff;
    font-size:11px;
    font-weight:bold;
    pointer-events:none
}
.blackhole-reset{
    position:absolute;
    left:12px;
    top:12px;
    z-index:10;
    padding:7px 10px;
    border-radius:7px;
    border:1px solid #405da0;
    background:#000b;
    color:white;
    cursor:pointer
}

/* GAME */
#game{
    display:none;
    position:fixed;
    inset:0;
    z-index:3000;
    background:#000
}
#gameCanvas{
    position:absolute;
    inset:0;
    width:100%;
    height:100%
}
#crosshair{
    position:absolute;
    z-index:10;
    left:50%;
    top:50%;
    width:18px;
    height:18px;
    transform:translate(-50%,-50%);
    pointer-events:none
}
#crosshair:before,#crosshair:after{
    content:"";
    position:absolute;
    background:white
}
#crosshair:before{width:18px;height:2px;top:8px}
#crosshair:after{height:18px;width:2px;left:8px}
.game-hud{
    position:absolute;
    left:15px;
    top:15px;
    z-index:10;
    width:260px;
    padding:15px;
    border:1px solid #334676;
    border-radius:12px;
    background:#030611d9
}
.hud-row{
    display:flex;
    justify-content:space-between;
    color:#aab5d3;
    font-size:13px;
    margin-bottom:7px
}
.bar{
    height:7px;
    margin-bottom:12px;
    overflow:hidden;
    border-radius:10px;
    background:#10182e
}
.bar div{height:100%;width:100%}
.health-bar{background:#e95a67}
.energy-bar{background:#5c9fff}
.planet-info{
    position:absolute;
    top:15px;
    right:15px;
    z-index:10;
    width:240px;
    padding:15px;
    border:1px solid #334676;
    border-radius:12px;
    background:#030611d9
}
.planet-info h3{color:#a8b9ff;margin-bottom:7px}
.planet-info p{color:#8996b7;font-size:12px;line-height:1.5}
.game-help{
    position:absolute;
    left:15px;
    bottom:15px;
    z-index:10;
    padding:12px 15px;
    border-radius:9px;
    background:#030611c9;
    color:#9aa6c4;
    font-size:12px
}
.home-game-btn{
    position:absolute;
    right:15px;
    bottom:15px;
    z-index:10;
    padding:10px 15px;
    border:1px solid #40578f;
    border-radius:8px;
    background:#030611dd;
    color:white;
    cursor:pointer
}
#gameOver{
    display:none;
    position:absolute;
    inset:0;
    z-index:50;
    align-items:center;
    justify-content:center;
    background:#000b
}
.game-over-box{
    width:350px;
    max-width:90%;
    padding:35px;
    text-align:center;
    border:1px solid #4c5e98;
    border-radius:16px;
    background:#080d20
}
.game-over-box h2{font-size:34px;margin-bottom:12px}
.game-over-box p{color:#929dbc;margin-bottom:20px}
.game-over-box button{
    padding:11px 18px;
    border:0;
    border-radius:8px;
    background:#385ad0;
    color:white;
    cursor:pointer
}

@media(max-width:850px){
    .blackhole-grid{grid-template-columns:1fr}
    .blackhole-card{height:300px}
    .galaxy-info{display:none}
}
@media(max-width:600px){
    nav{padding:0 12px}
    .nav-links{display:none}
    .game-hud{width:210px}
    .planet-info{display:none}
}
</style>
</head>

<body>

<!-- =====================================================
LOGIN
===================================================== -->

<div id="loginPage">

<div class="login-stars"></div>

<div class="login-box">

<div class="login-logo">🚀</div>

<h1>Space Research Hub</h1>

<p>Authorized Research Portal</p>

<form id="loginForm">

<div class="input-group">
<label>Researcher ID</label>
<input id="researcherID" required placeholder="Enter researcher ID">
</div>

<div class="input-group">
<label>Username</label>
<input id="username" required placeholder="Enter username">
</div>

<div class="input-group">
<label>Password</label>
<input id="password" type="password" required placeholder="Enter password">
</div>

<button class="login-btn">ENTER RESEARCH HUB</button>

<div class="login-error" id="loginError"></div>

</form>
</div>
</div>


<!-- =====================================================
MAIN WEBSITE
===================================================== -->

<div id="website">

<nav>

<div class="nav-logo">🚀 SPACE RESEARCH HUB</div>

<div class="nav-links">
<button onclick="scrollToSection('home')">Home</button>
<button onclick="openPlanets()">Solar System</button>
<button onclick="openGalaxies()">Galaxies</button>
<button onclick="scrollToSection('research')">Research</button>
<button onclick="scrollToSection('about')">About</button>
<button class="logout-btn" onclick="logout()">Logout</button>
</div>

</nav>


<section class="hero" id="home">

<div class="hero-stars"></div>

<div class="hero-content">

<h1>Explore the Universe</h1>

<p>
Enter a digital space research laboratory and explore
realistic 3D planets, galaxies and extreme cosmic objects.
</p>

<div class="hero-buttons">

<button class="primary-btn" onclick="openPlanets()">
🪐 Explore Solar System
</button>

<button class="secondary-btn" onclick="openGalaxies()">
🌌 Galaxy Explorer
</button>

</div>
</div>
</section>


<section class="section" id="research">

<h2 class="section-title">Research Modules</h2>

<p class="section-subtitle">
Explore interactive astronomy simulations.
</p>

<div class="research-grid">

<div class="research-card">
<div class="icon">🌍</div>
<h3>Planetary Science</h3>
<p>Explore detailed 3D planetary environments.</p>
</div>

<div class="research-card">
<div class="icon">🌌</div>
<h3>Galaxy Research</h3>
<p>Observe rotating spiral galaxy structures.</p>
</div>

<div class="research-card">
<div class="icon">🕳️</div>
<h3>Black Hole Observatory</h3>
<p>Interact with visual gravity simulations.</p>
</div>

<div class="research-card">
<div class="icon">🔭</div>
<h3>Deep Space</h3>
<p>Investigate objects beyond the Solar System.</p>
</div>

</div>
</section>


<!-- =====================================================
BLACK HOLES
===================================================== -->

<section class="section">

<div class="blackhole-section">

<h2 class="section-title">
🕳️ Black Hole Observatory
</h2>

<p class="section-subtitle">
Drag to rotate • Scroll to zoom • Click to activate a gravity event
</p>

<div class="blackhole-grid">

<div class="blackhole-card">
<canvas id="blackhole1"></canvas>
<div class="blackhole-label">
<h3>Sagittarius A*</h3>
<span>Galactic Center</span>
</div>
</div>

<div class="blackhole-card">
<canvas id="blackhole2"></canvas>
<div class="blackhole-label">
<h3>Stellar Black Hole</h3>
<span>Compact Gravity Object</span>
</div>
</div>

<div class="blackhole-card">
<canvas id="blackhole3"></canvas>
<div class="blackhole-label">
<h3>Extreme Gravity</h3>
<span>High Energy Region</span>
</div>
</div>

</div>
</div>
</section>


<section class="section" id="about">

<h2 class="section-title">About</h2>

<div class="about">

<p>
Space Research Hub is an educational interactive environment
for learning about planets, galaxies and astrophysics.
</p>

<br>

<p>
The visualizations are simulations designed for exploration
and are not exact physical models.
</p>

</div>

</section>

<footer>
Space Research Hub • Interactive Astronomy Laboratory
</footer>

</div>


<!-- =====================================================
PLANET SELECTOR
===================================================== -->

<div id="planetSelector">

<button class="back-btn" onclick="backToWebsite()">
← Back to Hub
</button>

<h1 class="section-title">
🪐 Realistic Solar System
</h1>

<p class="section-subtitle">
Select a planet. The next screen renders a 3D planetary
model with lighting, atmosphere and surface detail.
</p>

<div class="planet-grid">

<div class="planet-card" onclick="startPlanet('Mercury')">
<div class="planet-preview mercury"></div>
<h3>Mercury</h3>
</div>

<div class="planet-card" onclick="startPlanet('Venus')">
<div class="planet-preview venus"></div>
<h3>Venus</h3>
</div>

<div class="planet-card" onclick="startPlanet('Earth')">
<div class="planet-preview earth"></div>
<h3>Earth</h3>
</div>

<div class="planet-card" onclick="startPlanet('Mars')">
<div class="planet-preview mars"></div>
<h3>Mars</h3>
</div>

<div class="planet-card" onclick="startPlanet('Jupiter')">
<div class="planet-preview jupiter"></div>
<h3>Jupiter</h3>
</div>

<div class="planet-card" onclick="startPlanet('Saturn')">
<div class="planet-preview saturn"></div>
<h3>Saturn</h3>
</div>

<div class="planet-card" onclick="startPlanet('Uranus')">
<div class="planet-preview uranus"></div>
<h3>Uranus</h3>
</div>

<div class="planet-card" onclick="startPlanet('Neptune')">
<div class="planet-preview neptune"></div>
<h3>Neptune</h3>
</div>

</div>
</div>


<!-- =====================================================
GALAXY EXPLORER
===================================================== -->

<div id="galaxyExplorer">

<canvas id="galaxyCanvas"></canvas>

<div class="galaxy-sidebar">

<h2>🌌 Galaxies</h2>

<div class="galaxy-item active"
onclick="selectGalaxy('Milky Way',this)">Milky Way</div>

<div class="galaxy-item"
onclick="selectGalaxy('Andromeda',this)">Andromeda</div>

<div class="galaxy-item"
onclick="selectGalaxy('Triangulum',this)">Triangulum</div>

<div class="galaxy-item"
onclick="selectGalaxy('Whirlpool',this)">Whirlpool</div>

<div class="galaxy-item"
onclick="selectGalaxy('Sombrero',this)">Sombrero</div>

<div class="galaxy-item"
onclick="selectGalaxy('Pinwheel',this)">Pinwheel</div>

<div class="galaxy-item"
onclick="selectGalaxy('Cartwheel',this)">Cartwheel</div>

<div class="galaxy-controls">

<button onclick="toggleGalaxyRotation()">⏯ Rotation</button>
<button onclick="galaxyZoom(1)">🔍 Zoom In</button>
<button onclick="galaxyZoom(-1)">🔎 Zoom Out</button>
<button onclick="resetGalaxy()">🔄 Reset</button>
<button onclick="backToWebsite()">← Hub</button>

</div>
</div>

<div class="galaxy-info">
<h2 id="galaxyName">Milky Way</h2>
<p id="galaxyDescription">
Our home galaxy represented as a rotating spiral.
</p>
</div>

</div>


<!-- =====================================================
3D PLANET LAB
===================================================== -->

<div id="game">

<canvas id="gameCanvas"></canvas>

<div id="crosshair"></div>

<div class="game-hud">

<div class="hud-row">
<span>PLANET</span>
<span id="planetHud">EARTH</span>
</div>

<div class="hud-row">
<span>ROTATION</span>
<span id="rotationHud">ACTIVE</span>
</div>

<div class="hud-row">
<span>ZOOM</span>
<span id="zoomHud">1.0x</span>
</div>

</div>

<div class="planet-info">

<h3 id="planetTitle">Earth</h3>

<p id="planetDescription">
Loading planetary model...
</p>

</div>

<div class="game-help">
🖱 Drag = Rotate &nbsp; | &nbsp;
Wheel = Zoom &nbsp; | &nbsp;
Click = Toggle Rotation
</div>

<button class="home-game-btn" onclick="returnToPlanets()">
← Planets
</button>

</div>


<script>

/* =====================================================
GENERAL NAVIGATION
===================================================== */

const $=id=>document.getElementById(id);

$("loginForm").addEventListener("submit",function(e){

e.preventDefault();

if(
$("researcherID").value.trim() &&
$("username").value.trim() &&
$("password").value.trim()
){

$("loginPage").style.display="none";
$("website").style.display="block";

}else{

$("loginError").textContent=
"Please enter all credentials.";

}

});


function scrollToSection(id){
$(id).scrollIntoView({behavior:"smooth"});
}


function openPlanets(){

$("website").style.display="none";
$("galaxyExplorer").style.display="none";
$("planetSelector").style.display="block";

window.scrollTo(0,0);

}


function backToWebsite(){

$("planetSelector").style.display="none";
$("galaxyExplorer").style.display="none";
$("game").style.display="none";
$("website").style.display="block";

window.scrollTo(0,0);

}


function logout(){

$("website").style.display="none";
$("planetSelector").style.display="none";
$("galaxyExplorer").style.display="none";
$("game").style.display="none";
$("loginPage").style.display="flex";

}


/* =====================================================
REALISTIC PLANET DATA
===================================================== */

const planets={

Mercury:{
color:0xaaa69f,
roughness:.9,
metalness:0,
radius:1.8,
atmosphere:0xaaa69f,
description:
"Mercury is a small rocky world covered with impact craters and extreme temperature changes."
},

Venus:{
color:0xd99c55,
roughness:.95,
metalness:0,
radius:2.2,
atmosphere:0xffc879,
description:
"Venus has a thick atmosphere and a surface hidden beneath dense clouds."
},

Earth:{
color:0x2875c7,
roughness:.75,
metalness:0,
radius:2.35,
atmosphere:0x4baaff,
description:
"Earth has oceans, continents, clouds and a thin blue atmospheric layer."
},

Mars:{
color:0xb34d32,
roughness:.95,
metalness:0,
radius:2.0,
atmosphere:0xd66c4d,
description:
"Mars is a cold rocky planet with iron-rich dust, mountains and polar ice."
},

Jupiter:{
color:0xc69a73,
roughness:.8,
metalness:0,
radius:4.1,
atmosphere:0xd4ad8a,
description:
"Jupiter is a gas giant with powerful atmospheric bands and enormous storms."
},

Saturn:{
color:0xd6bd85,
roughness:.8,
metalness:0,
radius:3.7,
atmosphere:0xe6d29c,
description:
"Saturn is a gas giant surrounded by an enormous system of icy rings."
},

Uranus:{
color:0x79d6df,
roughness:.8,
metalness:0,
radius:3.0,
atmosphere:0x91e8f0,
description:
"Uranus is an ice giant with a pale blue atmosphere rich in methane."
},

Neptune:{
color:0x345dd1,
roughness:.75,
metalness:0,
radius:3.0,
atmosphere:0x558cff,
description:
"Neptune is a distant blue ice giant with powerful atmospheric winds."
}

};


/* =====================================================
3D PLANET VARIABLES
===================================================== */

let planetScene;
let planetCamera;
let planetRenderer;
let planetGroup;

let currentPlanet;

let planetDragging=false;
let planetMoved=false;

let planetPreviousX=0;
let planetPreviousY=0;

let planetRotation=true;

let planetDistance=8;
let targetPlanetDistance=8;

let planetInitialized=false;


/* =====================================================
PLANET TEXTURE GENERATION
===================================================== */

function makePlanetTexture(name){

const size=512;

const canvas=document.createElement("canvas");

canvas.width=size;
canvas.height=size;

const ctx=canvas.getContext("2d");

const data=planets[name];

ctx.fillStyle=
"#"+data.color.toString(16).padStart(6,"0");

ctx.fillRect(0,0,size,size);


/* Rocky texture */

if(
name==="Mercury" ||
name==="Mars"
){

for(let i=0;i<1800;i++){

const x=Math.random()*size;
const y=Math.random()*size;

const r=Math.random()*5+1;

const shade=
Math.random()>.5
?"rgba(255,255,255,.10)"
:"rgba(0,0,0,.16)";

ctx.fillStyle=shade;

ctx.beginPath();
ctx.arc(x,y,r,0,Math.PI*2);
ctx.fill();

}

}


/* Earth */

if(name==="Earth"){

/* ocean */
ctx.fillStyle="#1767a8";
ctx.fillRect(0,0,size,size);

/* continents */

for(let i=0;i<28;i++){

const x=Math.random()*size;
const y=Math.random()*size;

const w=25+Math.random()*90;
const h=15+Math.random()*60;

ctx.fillStyle=
i%3===0
?"#4d914c"
:"#3d7844";

ctx.beginPath();

ctx.ellipse(
x,y,w,h,
Math.random()*Math.PI,
0,
Math.PI*2
);

ctx.fill();

}

/* clouds */

for(let i=0;i<140;i++){

const x=Math.random()*size;
const y=Math.random()*size;

ctx.fillStyle=
"rgba(255,255,255,.12)";

ctx.beginPath();

ctx.ellipse(
x,y,
20+Math.random()*45,
4+Math.random()*10,
0,
0,
Math.PI*2
);

ctx.fill();

}

}


/* Venus */

if(name==="Venus"){

for(let i=0;i<100;i++){

const y=Math.random()*size;

ctx.strokeStyle=
`rgba(255,230,170,${.08+Math.random()*.15})`;

ctx.lineWidth=
5+Math.random()*12;

ctx.beginPath();

ctx.moveTo(0,y);

ctx.bezierCurveTo(
size*.3,
y-20,
size*.7,
y+20,
size,
y
);

ctx.stroke();

}

}


/* Jupiter */

if(name==="Jupiter"){

const bands=[
"#d8bb92",
"#a87959",
"#e3cda7",
"#91654b",
"#c59a73",
"#ead8b6",
"#9c7154",
"#d0ab82"
];

for(let i=0;i<bands.length;i++){

ctx.fillStyle=bands[i];

ctx.fillRect(
0,
i*size/bands.length,
size,
size/bands.length+4
);

}

for(let i=0;i<120;i++){

const y=Math.random()*size;

ctx.strokeStyle=
"rgba(80,50,35,.18)";

ctx.lineWidth=2+Math.random()*7;

ctx.beginPath();

ctx.moveTo(0,y);

ctx.bezierCurveTo(
130,y+Math.random()*15,
360,y-Math.random()*15,
size,y
);

ctx.stroke();

}

/* Great Red Spot */

ctx.fillStyle="#a94831";

ctx.beginPath();

ctx.ellipse(
370,
340,
55,
28,
-.1,
0,
Math.PI*2
);

ctx.fill();

ctx.strokeStyle="#713329";

ctx.lineWidth=7;

ctx.stroke();

}


/* Saturn */

if(name==="Saturn"){

for(let i=0;i<80;i++){

const y=Math.random()*size;

ctx.strokeStyle=
"rgba(120,90,50,.13)";

ctx.lineWidth=
2+Math.random()*8;

ctx.beginPath();

ctx.moveTo(0,y);

ctx.lineTo(size,y);

ctx.stroke();

}

}


/* Uranus / Neptune */

if(
name==="Uranus" ||
name==="Neptune"
){

for(let i=0;i<100;i++){

const y=Math.random()*size;

ctx.strokeStyle=
"rgba(255,255,255,.07)";

ctx.lineWidth=
2+Math.random()*5;

ctx.beginPath();

ctx.moveTo(0,y);

ctx.lineTo(size,y);

ctx.stroke();

}

}


/* Mars polar cap */

if(name==="Mars"){

ctx.fillStyle="rgba(245,240,220,.8)";

ctx.beginPath();

ctx.ellipse(
256,
25,
110,
45,
0,
0,
Math.PI*2
);

ctx.fill();

}


/* Mercury craters */

if(name==="Mercury"){

for(let i=0;i<350;i++){

const x=Math.random()*size;
const y=Math.random()*size;
const r=1+Math.random()*9;

ctx.strokeStyle="rgba(20,20,20,.25)";
ctx.lineWidth=1;

ctx.beginPath();
ctx.arc(x,y,r,0,Math.PI*2);
ctx.stroke();

}

}


const texture=
new THREE.CanvasTexture(canvas);

texture.wrapS=THREE.RepeatWrapping;
texture.wrapT=THREE.ClampToEdgeWrapping;

return texture;

}


/* =====================================================
PLANET LAB
===================================================== */

function startPlanet(name){

currentPlanet=name;

$("planetSelector").style.display="none";
$("game").style.display="block";

$("planetHud").textContent=name.toUpperCase();
$("planetTitle").textContent=name;
$("planetDescription").textContent=
planets[name].description;

initPlanet();

buildPlanet(name);

}


function initPlanet(){

if(planetInitialized){

resizePlanet();

return;

}

planetInitialized=true;

const canvas=$("gameCanvas");

planetScene=
new THREE.Scene();

planetScene.background=
new THREE.Color(0x010207);


planetCamera=
new THREE.PerspectiveCamera(
45,
window.innerWidth/window.innerHeight,
.1,
100
);

planetCamera.position.z=8;


planetRenderer=
new THREE.WebGLRenderer({
canvas:canvas,
antialias:true
});

planetRenderer.setPixelRatio(
Math.min(window.devicePixelRatio,2)
);

planetRenderer.setSize(
window.innerWidth,
window.innerHeight
);

planetRenderer.outputColorSpace=
THREE.SRGBColorSpace;


/* Lighting */

const ambient=
new THREE.AmbientLight(
0x6677aa,
.35
);

planetScene.add(ambient);


const sun=
new THREE.DirectionalLight(
0xffffff,
3.2
);

sun.position.set(
-7,
3,
6
);

planetScene.add(sun);


/* Stars */

const starGeometry=
new THREE.BufferGeometry();

const starPositions=
new Float32Array(1800*3);

for(let i=0;i<1800;i++){

starPositions[i*3]=
(Math.random()-.5)*100;

starPositions[i*3+1]=
(Math.random()-.5)*100;

starPositions[i*3+2]=
(Math.random()-.5)*100;

}

starGeometry.setAttribute(
"position",
new THREE.BufferAttribute(
starPositions,
3
)
);

const starMaterial=
new THREE.PointsMaterial({
color:0xffffff,
size:.08
});

planetScene.add(
new THREE.Points(
starGeometry,
starMaterial
)
);


/* Interaction */

canvas.addEventListener(
"mousedown",
e=>{

planetDragging=true;
planetMoved=false;

planetPreviousX=e.clientX;
planetPreviousY=e.clientY;

}
);


window.addEventListener(
"mousemove",
e=>{

if(!planetDragging || !planetGroup)
return;

const dx=e.clientX-planetPreviousX;
const dy=e.clientY-planetPreviousY;

if(Math.abs(dx)+Math.abs(dy)>3)
planetMoved=true;

planetGroup.rotation.y+=dx*.008;
planetGroup.rotation.x+=dy*.008;

planetPreviousX=e.clientX;
planetPreviousY=e.clientY;

}
);


window.addEventListener(
"mouseup",
()=>{

planetDragging=false;

}
);


/* Zoom */

canvas.addEventListener(
"wheel",
e=>{

e.preventDefault();

targetPlanetDistance+=
e.deltaY*.008;

targetPlanetDistance=
Math.max(
5,
Math.min(
20,
targetPlanetDistance
)
);

updateZoomHUD();

},
{passive:false}
);


/* Click = rotation */

canvas.addEventListener(
"click",
()=>{

if(planetMoved){

planetMoved=false;
return;

}

planetRotation=
!planetRotation;

$("rotationHud").textContent=
planetRotation
?"ACTIVE"
:"PAUSED";

}
);


window.addEventListener(
"resize",
resizePlanet
);

animatePlanet();

}


function resizePlanet(){

if(!planetRenderer)
return;

planetCamera.aspect=
window.innerWidth/
window.innerHeight;

planetCamera.updateProjectionMatrix();

planetRenderer.setSize(
window.innerWidth,
window.innerHeight
);

}


/* =====================================================
BUILD REALISTIC PLANET
===================================================== */

function buildPlanet(name){

if(planetGroup){

planetScene.remove(
planetGroup
);

planetGroup.traverse(
obj=>{

if(obj.geometry)
obj.geometry.dispose();

if(obj.material){

if(obj.material.map)
obj.material.map.dispose();

obj.material.dispose();

}

}
);

}

planetGroup=
new THREE.Group();

planetScene.add(
planetGroup
);


const data=planets[name];

const texture=
makePlanetTexture(name);


/* Main sphere */

const geometry=
new THREE.SphereGeometry(
data.radius,
128,
128
);


const material=
new THREE.MeshStandardMaterial({

map:texture,

roughness:data.roughness,

metalness:data.metalness

});


const planet=
new THREE.Mesh(
geometry,
material
);

planetGroup.add(
planet
);


/* Atmosphere */

const atmosphereGeometry=
new THREE.SphereGeometry(
data.radius*1.025,
96,
96
);


const atmosphereMaterial=
new THREE.MeshBasicMaterial({

color:data.atmosphere,

transparent:true,

opacity:
name==="Earth"
?.16
:name==="Venus"
?.22
:.09,

side:THREE.BackSide,

blending:
THREE.AdditiveBlending

});


const atmosphere=
new THREE.Mesh(
atmosphereGeometry,
atmosphereMaterial
);

planetGroup.add(
atmosphere
);


/* Cloud shell for Earth */

if(name==="Earth"){

const cloudGeometry=
new THREE.SphereGeometry(
data.radius*1.012,
96,
96
);


const cloudTexture=
makeCloudTexture();


const cloudMaterial=
new THREE.MeshPhongMaterial({

map:cloudTexture,

transparent:true,

opacity:.65,

depthWrite:false

});


const clouds=
new THREE.Mesh(
cloudGeometry,
cloudMaterial
);

planetGroup.add(
clouds
);

}


/* Saturn rings */

if(name==="Saturn"){

const ringGeometry=
new THREE.RingGeometry(
data.radius*1.25,
data.radius*2.15,
160
);


const ringTexture=
makeRingTexture();


const ringMaterial=
new THREE.MeshBasicMaterial({

map:ringTexture,

transparent:true,

side:THREE.DoubleSide,

depthWrite:false

});


const rings=
new THREE.Mesh(
ringGeometry,
ringMaterial
);

rings.rotation.x=
Math.PI/2.3;

planetGroup.add(
rings
);

}


/* Planet tilt */

const tilts={

Mercury:.03,
Venus:.03,
Earth:.41,
Mars:.44,
Jupiter:.05,
Saturn:.47,
Uranus:1.7,
Neptune:.49

};

planetGroup.rotation.z=
tilts[name]||0;

planetGroup.rotation.x=
.08;


/* Camera */

planetDistance=
name==="Jupiter"
?13
:name==="Saturn"
?13
:9;

targetPlanetDistance=
planetDistance;

planetCamera.position.z=
planetDistance;

updateZoomHUD();

}


/* =====================================================
CLOUD TEXTURE
===================================================== */

function makeCloudTexture(){

const canvas=
document.createElement("canvas");

canvas.width=512;
canvas.height=256;

const ctx=
canvas.getContext("2d");

ctx.clearRect(
0,0,512,256
);

for(let i=0;i<180;i++){

const x=Math.random()*512;
const y=Math.random()*256;

const w=15+Math.random()*70;
const h=2+Math.random()*9;

ctx.fillStyle=
"rgba(255,255,255,.5)";

ctx.beginPath();

ctx.ellipse(
x,y,w,h,
0,
0,
Math.PI*2
);

ctx.fill();

}

return new THREE.CanvasTexture(
canvas
);

}


/* =====================================================
SATURN RING TEXTURE
===================================================== */

function makeRingTexture(){

const canvas=
document.createElement("canvas");

canvas.width=1024;
canvas.height=64;

const ctx=
canvas.getContext("2d");

for(let x=0;x<1024;x++){

const v=
Math.sin(x*.06)*.5+
Math.sin(x*.2)*.2+
Math.random()*.15;

const brightness=
130+v*70;

ctx.fillStyle=
`rgb(${brightness},${brightness*.86},${brightness*.62})`;

ctx.fillRect(x,0,1,64);

}

return new THREE.CanvasTexture(
canvas
);

}


/* =====================================================
PLANET ANIMATION
===================================================== */

function updateZoomHUD(){

$("zoomHud").textContent=
(
9/
targetPlanetDistance
).toFixed(1)+"x";

}


function animatePlanet(){

requestAnimationFrame(
animatePlanet
);

if(planetGroup){

if(planetRotation){

planetGroup.rotation.y+=
.0018;

}

}

if(planetCamera){

planetDistance+=
(
targetPlanetDistance-
planetDistance
)*.08;

planetCamera.position.z=
planetDistance;

}

if(planetRenderer){

planetRenderer.render(
planetScene,
planetCamera
);

}

}


function returnToPlanets(){

$("game").style.display="none";
$("planetSelector").style.display="block";

}


/* =====================================================
GALAXY ENGINE
===================================================== */

const galaxyData={

"Milky Way":{
arms:5,
stars:10000,
size:12,
color:0x88aaff,
description:"Our home galaxy, represented as a rotating spiral."
},

"Andromeda":{
arms:6,
stars:12000,
size:14,
color:0xbbaaff,
description:"A large spiral galaxy with a broad stellar disk."
},

"Triangulum":{
arms:3,
stars:7000,
size:10,
color:0x77bbff,
description:"A smaller spiral galaxy with three visible arms."
},

"Whirlpool":{
arms:2,
stars:9000,
size:11,
color:0xff99dd,
description:"A dramatic two-arm spiral galaxy."
},

"Sombrero":{
arms:4,
stars:8000,
size:10,
color:0xffcc88,
description:"A bright central bulge surrounded by a disk."
},

"Pinwheel":{
arms:7,
stars:11000,
size:13,
color:0x99ddff,
description:"A broad spiral galaxy with many arms."
},

"Cartwheel":{
arms:5,
stars:8500,
size:12,
color:0xff99aa,
description:"A ring-like galaxy visualization."
}

};

let galaxyScene;
let galaxyCamera;
let galaxyRenderer;
let galaxyPoints;
let galaxyRotation=true;
let galaxyDistance=20;

function openGalaxies(){

$("website").style.display="none";
$("planetSelector").style.display="none";
$("galaxyExplorer").style.display="block";

initGalaxy();

setTimeout(resizeGalaxy,50);

}


function initGalaxy(){

if(galaxyRenderer){

resizeGalaxy();
return;

}

const canvas=$("galaxyCanvas");

galaxyScene=
new THREE.Scene();

galaxyCamera=
new THREE.PerspectiveCamera(
60,
window.innerWidth/window.innerHeight,
.1,
1000
);

galaxyCamera.position.z=
galaxyDistance;

galaxyRenderer=
new THREE.WebGLRenderer({
canvas:canvas,
antialias:true
});

galaxyRenderer.setPixelRatio(
Math.min(window.devicePixelRatio,2)
);

createGalaxy("Milky Way");

animateGalaxy();

}


function resizeGalaxy(){

if(!galaxyRenderer)
return;

galaxyRenderer.setSize(
window.innerWidth,
window.innerHeight,
false
);

galaxyCamera.aspect=
window.innerWidth/
window.innerHeight;

galaxyCamera.updateProjectionMatrix();

}


function createGalaxy(name){

if(galaxyPoints){

galaxyScene.remove(
galaxyPoints
);

galaxyPoints.geometry.dispose();
galaxyPoints.material.dispose();

}

const d=galaxyData[name];

const positions=
new Float32Array(
d.stars*3
);

for(let i=0;i<d.stars;i++){

const radius=
Math.pow(Math.random(),.55)*
d.size;

const arm=i%d.arms;

const armAngle=
arm*Math.PI*2/d.arms;

const angle=
armAngle+
radius*.55+
(Math.random()-.5)*.8;

const spread=
.12+radius*.035;

positions[i*3]=
Math.cos(angle)*radius+
(Math.random()-.5)*spread;

positions[i*3+1]=
(Math.random()-.5)*spread*.7;

positions[i*3+2]=
Math.sin(angle)*radius+
(Math.random()-.5)*spread;

}

const geometry=
new THREE.BufferGeometry();

geometry.setAttribute(
"position",
new THREE.BufferAttribute(
positions,
3
)
);

const material=
new THREE.PointsMaterial({

color:d.color,
size:.035,
transparent:true,
opacity:.85,
blending:THREE.AdditiveBlending

});

galaxyPoints=
new THREE.Points(
geometry,
material
);

galaxyScene.add(
galaxyPoints
);

}


function selectGalaxy(name,element){

document
.querySelectorAll(".galaxy-item")
.forEach(
e=>e.classList.remove("active")
);

element.classList.add("active");

$("galaxyName").textContent=name;
$("galaxyDescription").textContent=
galaxyData[name].description;

createGalaxy(name);

}


function toggleGalaxyRotation(){

galaxyRotation=
!galaxyRotation;

}


function galaxyZoom(amount){

galaxyDistance-=amount*2;

galaxyDistance=
Math.max(
7,
Math.min(
40,
galaxyDistance
)
);

}


function resetGalaxy(){

galaxyDistance=20;

}


function animateGalaxy(){

requestAnimationFrame(
animateGalaxy
);

if(galaxyPoints && galaxyRotation)
galaxyPoints.rotation.y+=.0015;

if(galaxyCamera){

galaxyCamera.position.z+=
(
galaxyDistance-
galaxyCamera.position.z
)*.05;

}

if(galaxyRenderer){

galaxyRenderer.render(
galaxyScene,
galaxyCamera
);

}

}

window.addEventListener(
"resize",
resizeGalaxy
);


/* =====================================================
INTERACTIVE BLACK HOLES
===================================================== */

function createBlackHole(
canvasId,
rotationSpeed
){

const canvas=
$(canvasId);

const card=
canvas.parentElement;

const status=
document.createElement("div");

status.className=
"blackhole-status";

status.textContent=
"● STABLE";

card.appendChild(status);


const reset=
document.createElement("button");

reset.className=
"blackhole-reset";

reset.textContent=
"RESET";

card.appendChild(reset);


const scene=
new THREE.Scene();

const camera=
new THREE.PerspectiveCamera(
55,
1,
.1,
1000
);

camera.position.z=9;


const renderer=
new THREE.WebGLRenderer({
canvas:canvas,
antialias:true,
alpha:true
});

renderer.setPixelRatio(
Math.min(window.devicePixelRatio,2)
);


function resize(){

const w=
canvas.clientWidth||400;

const h=
canvas.clientHeight||300;

renderer.setSize(
w,h,false
);

camera.aspect=w/h;

camera.updateProjectionMatrix();

}

resize();


/* Stars */

const count=700;

const geometry=
new THREE.BufferGeometry();

const positions=
new Float32Array(
count*3
);

const starData=[];

for(let i=0;i<count;i++){

const angle=
Math.random()*Math.PI*2;

const radius=
7+Math.random()*14;

const y=
(Math.random()-.5)*12;

positions[i*3]=
Math.cos(angle)*radius;

positions[i*3+1]=y;

positions[i*3+2]=
Math.sin(angle)*radius;

starData.push({
angle,
radius,
speed:.0002+
Math.random()*.0005
});

}

geometry.setAttribute(
"position",
new THREE.BufferAttribute(
positions,
3
)
);

const stars=
new THREE.Points(
geometry,
new THREE.PointsMaterial({
color:0xffffff,
size:.035
})
);

scene.add(stars);


/* Black hole */

const blackHole=
new THREE.Group();

scene.add(
blackHole
);


/* Disk */

const disk=
new THREE.Mesh(

new THREE.RingGeometry(
1.7,
4.2,
128
),

new THREE.MeshBasicMaterial({
color:0xff6a00,
transparent:true,
opacity:.65,
side:THREE.DoubleSide,
blending:THREE.AdditiveBlending
})

);

disk.rotation.x=
Math.PI/2.15;

blackHole.add(disk);


/* Inner disk */

const disk2=
new THREE.Mesh(

new THREE.RingGeometry(
1.3,
3.3,
128
),

new THREE.MeshBasicMaterial({
color:0xffd000,
transparent:true,
opacity:.35,
side:THREE.DoubleSide,
blending:THREE.AdditiveBlending
})

);

disk2.rotation.x=
Math.PI/2.15;

blackHole.add(disk2);


/* Event horizon */

blackHole.add(

new THREE.Mesh(

new THREE.SphereGeometry(
1.25,
64,
64
),

new THREE.MeshBasicMaterial({
color:0x000000
})

)

);


/* Photon ring */

const photon=
new THREE.Mesh(

new THREE.TorusGeometry(
1.45,
.1,
24,
128
),

new THREE.MeshBasicMaterial({
color:0xffa000,
transparent:true,
opacity:.95,
blending:THREE.AdditiveBlending
})

);

photon.rotation.x=
Math.PI/2;

blackHole.add(photon);


/* Gravity rings */

const gravityRings=[];

for(let i=0;i<4;i++){

const ring=
new THREE.Mesh(

new THREE.TorusGeometry(
1.8+i*.45,
.025,
12,
100
),

new THREE.MeshBasicMaterial({
color:0x7040ff,
transparent:true,
opacity:.25,
blending:THREE.AdditiveBlending
})

);

ring.rotation.x=
Math.PI/2;

blackHole.add(ring);

gravityRings.push(ring);

}


const light=
new THREE.PointLight(
0xff7700,
4,
15
);

blackHole.add(light);


/* Controls */

let dragging=false;
let moved=false;

let px=0;
let py=0;

let gravityPulse=0;

let targetDistance=9;
let currentDistance=9;


canvas.addEventListener(
"mousedown",
e=>{

dragging=true;
moved=false;

px=e.clientX;
py=e.clientY;

}
);


window.addEventListener(
"mousemove",
e=>{

if(!dragging)
return;

const dx=e.clientX-px;
const dy=e.clientY-py;

if(Math.abs(dx)+Math.abs(dy)>3)
moved=true;

blackHole.rotation.y+=dx*.008;
blackHole.rotation.x+=dy*.008;

px=e.clientX;
py=e.clientY;

}
);


window.addEventListener(
"mouseup",
()=>{
dragging=false;
}
);


canvas.addEventListener(
"wheel",
e=>{

e.preventDefault();

targetDistance+=e.deltaY*.008;

targetDistance=
Math.max(
4,
Math.min(
18,
targetDistance
)
);

},
{passive:false}
);


canvas.addEventListener(
"click",
()=>{

if(moved){

moved=false;
return;

}

gravityPulse=1;

status.textContent=
"⚠ GRAVITY EVENT";

status.style.color=
"#ffb000";

}
);


reset.addEventListener(
"click",
e=>{

e.stopPropagation();

blackHole.rotation.set(
0,0,0
);

targetDistance=9;

gravityPulse=0;

status.textContent=
"● STABLE";

status.style.color=
"#9eb6ff";

}
);


/* Animation */

const clock=
new THREE.Clock();

function animate(){

requestAnimationFrame(
animate
);

const time=
clock.getElapsedTime();


currentDistance+=
(targetDistance-currentDistance)*.08;

camera.position.z=
currentDistance;


const speed=
rotationSpeed*
(gravityPulse>0?5:1);


disk.rotation.z+=speed;
disk2.rotation.z-=speed*1.4;
photon.rotation.z+=speed*2;


gravityRings.forEach(
(r,i)=>{

r.rotation.z+=
speed*(i+1)*.7;

r.scale.setScalar(
1+Math.sin(time*2+i)*.04
);

}
);


if(gravityPulse>0){

gravityPulse-=.012;

const power=gravityPulse;

starData.forEach(
(star,i)=>{

star.angle+=
star.speed*20*power;

star.radius-=
.008*power;

if(star.radius<5){

star.radius=
18+Math.random()*8;

star.angle=
Math.random()*Math.PI*2;

}

positions[i*3]=
Math.cos(star.angle)*
star.radius;

positions[i*3+2]=
Math.sin(star.angle)*
star.radius;

}
);

geometry.attributes
.position
.needsUpdate=true;

disk.scale.setScalar(
1+power*.25
);

photon.scale.setScalar(
1+power*.35
);

}else{

starData.forEach(
(star,i)=>{

star.angle+=
star.speed;

positions[i*3]=
Math.cos(star.angle)*
star.radius;

positions[i*3+2]=
Math.sin(star.angle)*
star.radius;

}
);

geometry.attributes
.position
.needsUpdate=true;

disk.scale.setScalar(1);
photon.scale.setScalar(1);

}


light.intensity=
3+Math.sin(time*3)*.8;


renderer.render(
scene,
camera
);

}

animate();

window.addEventListener(
"resize",
resize
);

}


createBlackHole("blackhole1",.006);
createBlackHole("blackhole2",-.009);
createBlackHole("blackhole3",.004);

</script>

</body>
</html>
