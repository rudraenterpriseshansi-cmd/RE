<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Rudra Enterprises - 128x96</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

html,body{
    margin:0;
    padding:0;
    width:128px;
    height:96px;
    overflow:hidden;
    background:#000;
}

/* EXACT 128 x 96 PIXELS */
#display{
    position:relative;

    width:128px;
    height:96px;

    min-width:128px;
    min-height:96px;

    max-width:128px;
    max-height:96px;

    overflow:hidden;

    background:#000;

    color:#fff;

    font-family:Arial, Helvetica, sans-serif;
}


/* =========================
   COMPANY
   ========================= */

.company{
    position:absolute;

    left:0;
    top:3px;

    width:128px;

    text-align:center;

    font-size:7.8px;
    line-height:9px;

    font-weight:900;

    white-space:nowrap;
}


/* =========================
   TOP LINES
   ========================= */

.line1{
    position:absolute;

    left:0;
    top:15px;

    width:128px;
    height:1px;

    background:#fff;
}

.line2{
    position:absolute;

    left:0;
    top:17px;

    width:128px;
    height:1px;

    background:#888;
}

.line3{
    position:absolute;

    left:0;
    top:18px;

    width:128px;
    height:1px;

    background:#444;
}


/* =========================
   PM2.5 TITLE
   ========================= */

.pm25-title{
    position:absolute;

    left:12px;
    top:22px;

    font-size:7px;
    line-height:8px;

    font-weight:900;

    white-space:nowrap;
}


/* =========================
   PM10 TITLE
   ========================= */

.pm10-title{
    position:absolute;

    left:55px;
    top:22px;

    font-size:7px;
    line-height:8px;

    font-weight:900;

    white-space:nowrap;
}


/* =========================
   PM2.5 VALUE
   ========================= */

.pm25-value{
    position:absolute;

    left:12px;
    top:31px;

    font-size:15px;
    line-height:16px;

    font-weight:900;

    color:#ff0000;

    white-space:nowrap;
}


/* =========================
   PM10 VALUE
   ========================= */

.pm10-value{
    position:absolute;

    left:55px;
    top:31px;

    font-size:15px;
    line-height:16px;

    font-weight:900;

    color:#ff0000;

    white-space:nowrap;
}


/* =========================
   UNITS
   ========================= */

.unit25{
    position:absolute;

    left:13px;
    top:48px;

    font-size:6px;
    line-height:7px;

    white-space:nowrap;
}

.unit10{
    position:absolute;

    left:57px;
    top:48px;

    font-size:6px;
    line-height:7px;

    white-space:nowrap;
}


/* =========================
   RED TEMPERATURE DOT
   ========================= */

.temp-dot{
    position:absolute;

    left:89px;
    top:24px;

    width:4px;
    height:7px;

    background:#ff0000;

    border-radius:50%;
}


/* =========================
   TEMPERATURE
   ========================= */

.temp{
    position:absolute;

    left:94px;
    top:22px;

    font-size:6.5px;
    line-height:8px;

    white-space:nowrap;
}


/* =========================
   BLUE HUMIDITY DOT
   ========================= */

.hum-dot{
    position:absolute;

    left:89px;
    top:31px;

    width:4px;
    height:7px;

    background:#009cff;

    border-radius:50%;
}


/* =========================
   HUMIDITY
   ========================= */

.hum{
    position:absolute;

    left:94px;
    top:29px;

    font-size:6.5px;
    line-height:8px;

    white-space:nowrap;
}


/* =========================
   DATE
   ========================= */

.date{
    position:absolute;

    right:9px;
    top:79px;

    font-size:5.5px;
    line-height:7px;

    white-space:nowrap;
}


/* =========================
   TIME
   ========================= */

.time{
    position:absolute;

    right:9px;
    top:86px;

    font-size:5.5px;
    line-height:7px;

    white-space:nowrap;
}


/* =========================
   BOTTOM LINE
   ========================= */

.bottom-line{
    position:absolute;

    left:0;
    bottom:0;

    width:128px;
    height:1px;

    background:#fff;
}

</style>
</head>


<body>

<div id="display">

    <!-- COMPANY -->
    <div class="company">
        RUDRA ENTERPRISES
    </div>


    <!-- TOP BORDER -->
    <div class="line1"></div>
    <div class="line2"></div>
    <div class="line3"></div>


    <!-- PM2.5 -->
    <div class="pm25-title">
        PM2.5
    </div>

    <div id="pm25" class="pm25-value">
        85
    </div>

    <div class="unit25">
        µg/m3
    </div>


    <!-- PM10 -->
    <div class="pm10-title">
        PM10
    </div>

    <div id="pm10" class="pm10-value">
        152
    </div>

    <div class="unit10">
        µg/m3
    </div>


    <!-- TEMPERATURE -->
    <div class="temp-dot"></div>

    <div id="temperature" class="temp">
        23.0°C
    </div>


    <!-- HUMIDITY -->
    <div class="hum-dot"></div>

    <div id="humidity" class="hum">
        35.0%
    </div>


    <!-- DATE -->
    <div id="date" class="date">
        24|Jan|2026
    </div>


    <!-- TIME -->
    <div id="time" class="time">
        12:21 PM
    </div>


    <!-- BOTTOM -->
    <div class="bottom-line"></div>

</div>


<script>

/* =========================
   SENSOR DATA
   ========================= */

let data = {
    pm25:85,
    pm10:152,
    temperature:23.0,
    humidity:35.0
};


/* =========================
   UPDATE DATA
   ========================= */

function updateDisplay(){

    document.getElementById("pm25").textContent =
        data.pm25;

    document.getElementById("pm10").textContent =
        data.pm10;

    document.getElementById("temperature").textContent =
        Number(data.temperature).toFixed(1) + "°C";

    document.getElementById("humidity").textContent =
        Number(data.humidity).toFixed(1) + "%";
}


/* =========================
   DATE / TIME
   ========================= */

function updateDateTime(){

    const now = new Date();

    const day =
        String(now.getDate()).padStart(2,"0");

    const months = [
        "Jan","Feb","Mar","Apr","May","Jun",
        "Jul","Aug","Sep","Oct","Nov","Dec"
    ];

    const month =
        months[now.getMonth()];

    const year =
        now.getFullYear();

    document.getElementById("date").textContent =
        day + "|" + month + "|" + year;


    let hours = now.getHours();

    const minutes =
        String(now.getMinutes()).padStart(2,"0");

    const ampm =
        hours >= 12 ? "PM" : "AM";

    hours =
        hours % 12;

    if(hours === 0){
        hours = 12;
    }

    document.getElementById("time").textContent =
        hours + ":" + minutes + " " + ampm;
}


/* =========================
   START
   ========================= */

updateDisplay();
updateDateTime();

setInterval(updateDateTime,1000);

</script>

</body>
</html>
