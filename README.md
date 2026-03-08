<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">

<style>

/* FULL BLACK SCREEN */

html,body{
margin:0;
padding:0;
width:100%;
height:100%;
background:black;
overflow:hidden;
font-family:Arial;
}

/* CENTER DISPLAY */

body{
display:flex;
justify-content:center;
align-items:center;
}

/* OUTER FRAME */

.frame{
width:100%;
height:100%;
border:3px solid #00aaff;
box-sizing:border-box;
}

/* CONTENT AREA */

.container{
width:100%;
height:100%;
display:flex;
flex-direction:column;
}

/* CLIENT NAME */

.header{
color:#00ff66;
font-size:48px;
text-align:center;
padding:10px;
border-bottom:3px solid #00aaff;
font-weight:bold;
}

/* DATE TIME */

.datetime{
display:grid;
grid-template-columns:1fr 1fr;
border-bottom:3px solid #00aaff;
}

.datetime div{
color:white;
font-size:34px;
padding:10px;
text-align:center;
border-right:3px solid #00aaff;
}

.datetime div:last-child{
border-right:none;
}

/* DATA TABLE */

table{
width:100%;
height:100%;
border-collapse:collapse;
table-layout:fixed;
}

td{
border:3px solid #00aaff;
font-size:44px;
padding:18px;
text-align:center;
}

/* COLUMN COLORS */

.label{
width:33.33%;
color:#ff66ff;
text-align:left;
padding-left:40px;
}

.value{
width:33.33%;
color:#ffcc00;
font-weight:bold;
}

.unit{
width:33.33%;
color:#00ffff;
}

</style>
</head>

<body>

<div class="frame">

<div class="container">

<div class="header" id="clientName">AQI DISPLAY</div>

<div class="datetime">
<div id="date"></div>
<div id="time"></div>
</div>

<table>

<tr>
<td class="label">PM2.5</td>
<td class="value" id="pm25">--</td>
<td class="unit">µg/m³</td>
</tr>

<tr>
<td class="label">TEMP</td>
<td class="value" id="temp">--</td>
<td class="unit">DegC</td>
</tr>

<tr>
<td class="label">HUM</td>
<td class="value" id="hum">--</td>
<td class="unit">%</td>
</tr>

<tr>
<td class="label">PM10</td>
<td class="value" id="pm10">--</td>
<td class="unit">µg/m³</td>
</tr>

<tr>
<td class="label">AQI</td>
<td class="value" id="aqi">--</td>
<td class="unit">---</td>
</tr>

</table>

</div>

</div>

<script>

/* GET URL PARAMETERS */

const params = new URLSearchParams(window.location.search);
const client = params.get("client");
const device = params.get("device") || "11";

/* CHANGE CLIENT NAME */

if(client){
document.getElementById("clientName").innerText = client;
}

/* DATE TIME */

function updateTime(){

const now = new Date();

document.getElementById("date").innerText = now.toLocaleDateString();
document.getElementById("time").innerText = now.toLocaleTimeString();

}

/* FETCH DATA */

async function fetchData(){

try{

const response = await fetch(
"https://aqi.rudraenterpriseshansi.workers.dev/?device=" + device
);

const data = await response.json();
const p = data.parameter;

document.getElementById("pm25").innerText = p.pm25.value;
document.getElementById("temp").innerText = p.temperature.value;
document.getElementById("hum").innerText = p.humidity.value;
document.getElementById("pm10").innerText = p.pm10.value;
document.getElementById("aqi").innerText = p.aqi.value;

}catch(e){

console.log("API Error",e);

}

}

setInterval(updateTime,1000);
setInterval(fetchData,20000);

updateTime();
fetchData();

</script>

</body>
</html>
