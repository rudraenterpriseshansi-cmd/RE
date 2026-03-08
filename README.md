<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title></title>

<style>

body{
background:#000;
margin:0;
font-family:Arial;
color:white;
overflow:hidden;
}

.container{
width:100vw;
height:100vh;
border:3px solid #00aaff;
box-sizing:border-box;
}

table{
width:100%;
height:100%;
border-collapse:collapse;
table-layout:fixed;
}

td{
border:2px solid #00aaff;
text-align:center;
font-weight:bold;
}

.name{
font-size:4vw;
color:#00ff66;
}

.datetime{
font-size:2.5vw;
color:#ffffff;
}

.label{
font-size:2.5vw;
color:#ff66ff;
}

.value{
font-size:3vw;
color:#ffcc00;
}

.unit{
font-size:2vw;
color:#00ffff;
}

</style>
</head>

<body>

<div class="container">

<table>

<tr>
<td colspan="3" class="name" id="clientName">CLIENT</td>
</tr>

<tr>
<td class="datetime" id="date"></td>
<td class="datetime" colspan="2" id="time"></td>
</tr>

<tr>
<td class="label">PM2.5</td>
<td class="value" id="pm25">--</td>
<td class="unit">µg/m³</td>
</tr>

<tr>
<td class="label">TEMP</td>
<td class="value" id="temp">--</td>
<td class="unit">°C</td>
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

// URL PARAMETERS
const params = new URLSearchParams(window.location.search)

const device = params.get("device") || "11"
const name = params.get("name") || "AQI DEVICE"

document.getElementById("clientName").innerText = name


// DATE TIME
function updateTime(){

const now = new Date()

document.getElementById("date").innerText =
now.toLocaleDateString()

document.getElementById("time").innerText =
now.toLocaleTimeString()

}


// FETCH DATA
async function fetchData(){

try{

const response = await fetch("https://aqi.rudraenterpriseshansi.workers.dev/?device="+device)

const data = await response.json()

const p = data.parameter

document.getElementById("pm25").innerText = p.pm25.value
document.getElementById("temp").innerText = p.temperature.value
document.getElementById("hum").innerText = p.humidity.value
document.getElementById("pm10").innerText = p.pm10.value
document.getElementById("aqi").innerText = p.aqi.value

}
catch(e){

console.log("API ERROR",e)

}

}

setInterval(updateTime,1000)
setInterval(fetchData,20000)

updateTime()
fetchData()

</script>

</body>
</html>
