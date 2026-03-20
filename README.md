<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">

<title>AQI LED Display</title>

<style>

/* RESET */
*{
margin:0;
padding:0;
box-sizing:border-box;
}

body{
background:black;
display:flex;
justify-content:center;
align-items:center;
height:100vh;
font-family:Arial, Helvetica, sans-serif;
overflow:hidden;
}

/* 4:3 RATIO */
.container{
width:100vw;
height:75vw;
max-height:100vh;
max-width:133.33vh;
display:flex;
flex-direction:column;
}

/* HEADER */
.header{
height:14%;
display:flex;
align-items:center;
overflow:hidden;
border-bottom:0.2px solid #00aaff; /* thinner */
}

marquee{
color:#00ff66;
font-size:12vh; /* bigger */
font-weight:bold;
width:100%;
}

/* DATE TIME */
.datetime{
height:10%;
display:grid;
grid-template-columns:1fr 1fr;
border-bottom:0.2px solid #00aaff; /* thinner */
}

.date,.time{
display:flex;
justify-content:center;
align-items:center;
font-size:12vh; /* bigger */
color:white;
}

/* SINGLE LINE GRID (ULTRA THIN) */
.data{
flex:1;
display:grid;
grid-template-columns:1fr 1fr 1fr;
grid-template-rows:repeat(5,1fr);
gap:0.2px;                 /* THIN BORDER */
background:#00aaff;
}

.cell{
background:black;
display:flex;
justify-content:center;
align-items:center;
text-align:center;
}

/* TEXT (BIG LED STYLE) */
.label{
color:#ff66ff;
font-size:12vh; /* bigger */
font-weight:bold;
}

.value{
color:#ffcc00;
font-size:12vh;   /* MAIN BIG VALUE */
font-weight:bold;
}

.unit{
color:#00ffff;
font-size:12vh; /* bigger */
}

</style>

</head>

<body>

<div class="container">

<!-- HEADER -->
<div class="header">
<marquee id="clientName" scrollamount="1" scrolldelay="20">
AQI DISPLAY
</marquee>
</div>

<!-- DATE TIME -->
<div class="datetime">
<div class="date" id="date"></div>
<div class="time" id="time"></div>
</div>

<!-- DATA GRID -->
<div class="data">

<div class="cell label">PM2.5</div>
<div class="cell value" id="pm25">--</div>
<div class="cell unit">µg/m³</div>

<div class="cell label">TEMP</div>
<div class="cell value" id="temp">--</div>
<div class="cell unit">°C</div>

<div class="cell label">HUM</div>
<div class="cell value" id="hum">--</div>
<div class="cell unit">%</div>

<div class="cell label">PM10</div>
<div class="cell value" id="pm10">--</div>
<div class="cell unit">µg/m³</div>

<div class="cell label">AQI</div>
<div class="cell value" id="aqi">--</div>
<div class="cell unit">Index</div>

</div>

</div>

<script>

/* URL PARAMETERS */
const params = new URLSearchParams(window.location.search);

const device = params.get("device") || "11";

let name =
params.get("client") ||
params.get("name") ||
"AQI DISPLAY";

name = decodeURIComponent(name);

/* SET NAME */
document.getElementById("clientName").innerText = name;

/* DATE TIME */
function updateTime(){
const now = new Date();

document.getElementById("date").innerText =
now.toLocaleDateString();

document.getElementById("time").innerText =
now.toLocaleTimeString();
}

/* FETCH DATA */
async function fetchData(){
try{

const response = await fetch(
"https://aqi.rudraenterpriseshansi.workers.dev/?device=" + device
);

const data = await response.json();
const p = data.parameter;

/* SAFE VALUES */
document.getElementById("pm25").innerText = p.pm25?.value ?? "--";
document.getElementById("temp").innerText = p.temperature?.value ?? "--";
document.getElementById("hum").innerText = p.humidity?.value ?? "--";
document.getElementById("pm10").innerText = p.pm10?.value ?? "--";
document.getElementById("aqi").innerText = p.aqi?.value ?? "--";

}catch(e){
console.log("API ERROR", e);
}
}

/* AUTO REFRESH */
setInterval(updateTime, 1000);
setInterval(fetchData, 20000);

updateTime();
fetchData();

</script>

</body>
</html>
