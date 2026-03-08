<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">

<style>

body{
background:black;
margin:0;
font-family:Arial;
display:flex;
justify-content:center;
align-items:center;
height:100vh;
}

.container{
width:700px;
border:4px solid #00aaff;
}

.header{
color:#00ff66;
font-size:40px;
text-align:center;
padding:10px;
border-bottom:3px solid #00aaff;
font-weight:bold;
}

.datetime{
display:grid;
grid-template-columns:1fr 1fr;
border-bottom:3px solid #00aaff;
}

.datetime div{
color:white;
font-size:26px;
padding:8px;
text-align:center;
border-right:2px solid #00aaff;
}

.datetime div:last-child{
border-right:none;
}

table{
width:100%;
border-collapse:collapse;
}

td{
border:2px solid #00aaff;
padding:15px;
font-size:30px;
}

.label{
color:#ff66ff;
padding-left:20px;
}

.value{
color:#ffcc00;
text-align:center;
font-weight:bold;
}

.unit{
color:#00ffff;
text-align:center;
}

</style>
</head>

<body>

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

<script>

const params = new URLSearchParams(window.location.search);

const client = params.get("client");
const device = params.get("device") || "11";

if(client){
document.getElementById("clientName").innerText = client;
}

function updateTime(){

const now = new Date();

document.getElementById("date").innerText =
now.toLocaleDateString();

document.getElementById("time").innerText =
now.toLocaleTimeString();

}

async function fetchData(){

try{

const response = await fetch("https://aqi.rudraenterpriseshansi.workers.dev/?device=" + device);

const data = await response.json();

const p = data.parameter;

document.getElementById("pm25").innerText = p.pm25.value;
document.getElementById("temp").innerText = p.temperature.value;
document.getElementById("hum").innerText = p.humidity.value;
document.getElementById("pm10").innerText = p.pm10.value;
document.getElementById("aqi").innerText = p.aqi.value;

}

catch(e){

console.log(e);

}

}

setInterval(updateTime,1000);
setInterval(fetchData,20000);

updateTime();
fetchData();

</script>

</body>
</html>
