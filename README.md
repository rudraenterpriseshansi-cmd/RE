<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport"
      content="width=128, height=96, initial-scale=1.0, maximum-scale=1.0">

<title>Rudra Enterprises - AQI Display</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

html,body{
    width:128px;
    height:96px;
    overflow:hidden;
    background:#000;
    font-family:Arial, Helvetica, sans-serif;
}

#display{
    width:128px;
    height:96px;
    background:#000;
    color:#fff;
    position:relative;
    overflow:hidden;
}

/* COMPANY NAME */
.company{
    position:absolute;
    top:3px;
    left:0;
    width:128px;
    height:14px;

    text-align:center;
    white-space:nowrap;

    font-size:7.5px;
    font-weight:900;
    letter-spacing:.3px;
}

/* TOP LINE */
.line1{
    position:absolute;
    top:16px;
    left:0;
    width:128px;
    height:1px;
    background:#fff;
}

.line2{
    position:absolute;
    top:17px;
    left:0;
    width:128px;
    height:1px;
    background:#777;
}

/* PARAMETER TITLES */
.pm25-title{
    position:absolute;
    top:23px;
    left:12px;

    font-size:7px;
    font-weight:900;
}

.pm10-title{
    position:absolute;
    top:23px;
    left:55px;

    font-size:7px;
    font-weight:900;
}

/* VALUES */
.pm25-value{
    position:absolute;
    top:32px;
    left:12px;

    font-size:15px;
    line-height:16px;
    font-weight:900;

    color:#ff0000;
}

.pm10-value{
    position:absolute;
    top:32px;
    left:55px;

    font-size:15px;
    line-height:16px;
    font-weight:900;

    color:#ff0000;
}

/* UNIT */
.unit25{
    position:absolute;
    top:48px;
    left:13px;

    font-size:6px;
    color:#fff;
}

.unit10{
    position:absolute;
    top:48px;
    left:57px;

    font-size:6px;
    color:#fff;
}

/* TEMPERATURE */
.temp-dot{
    position:absolute;
    top:24px;
    left:89px;

    width:4px;
    height:7px;

    background:#ff0000;
    border-radius:50%;
}

.temp{
    position:absolute;
    top:23px;
    left:94px;

    font-size:6.5px;
    white-space:nowrap;
}

/* HUMIDITY */
.hum-dot{
    position:absolute;
    top:31px;
    left:89px;

    width:4px;
    height:7px;

    background:#009cff;
    border-radius:50%;
}

.hum{
    position:absolute;
    top:30px;
    left:94px;

    font-size:6.5px;
    white-space:nowrap;
}

/* BOTTOM DATE */
.date{
    position:absolute;
    bottom:9px;
    right:9px;

    font-size:5.5px;
    color:#fff;
    white-space:nowrap;
}

/* BOTTOM TIME */
.time{
    position:absolute;
    bottom:2px;
    right:9px;

    font-size:5.5px;
    color:#fff;
    white-space:nowrap;
}

/* BOTTOM LINE */
.bottom-line{
    position:absolute;
    bottom:0;
    left:0;

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

    <!-- PM2.5 -->
    <div class="pm25-title">PM2.5</div>

    <div id="pm25" class="pm25-value">
        85
    </div>

    <div class="unit25">
        µg/m3
    </div>


    <!-- PM10 -->
    <div class="pm10-title">PM10</div>

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

    <div class="bottom-line"></div>

</div>


<script>

/* ==========================================
   DEMO DATA
   ========================================== */

let data = {
    pm25: 85,
    pm10: 152,
    temperature: 23.0,
    humidity: 35.0
};


/* ==========================================
   UPDATE DISPLAY
   ========================================== */

function updateDisplay(){

    document.getElementById("pm25").innerText =
        data.pm25;

    document.getElementById("pm10").innerText =
        data.pm10;

    document.getElementById("temperature").innerText =
        Number(data.temperature).toFixed(1) + "°C";

    document.getElementById("humidity").innerText =
        Number(data.humidity).toFixed(1) + "%";
}


/* ==========================================
   DATE & TIME
   ========================================== */

function updateDateTime(){

    const now = new Date();

    const day =
        String(now.getDate()).padStart(2,"0");

    const monthNames = [
        "Jan","Feb","Mar","Apr","May","Jun",
        "Jul","Aug","Sep","Oct","Nov","Dec"
    ];

    const month =
        monthNames[now.getMonth()];

    const year =
        now.getFullYear();

    document.getElementById("date").innerText =
        day + "|" + month + "|" + year;


    let hours = now.getHours();

    const minutes =
        String(now.getMinutes()).padStart(2,"0");

    const seconds =
        String(now.getSeconds()).padStart(2,"0");

    const ampm =
        hours >= 12 ? "PM" : "AM";

    hours =
        hours % 12;

    hours =
        hours ? hours : 12;

    document.getElementById("time").innerText =
        hours + ":" + minutes + " " + ampm;
}


/* ==========================================
   START
   ========================================== */

updateDisplay();
updateDateTime();

setInterval(updateDateTime,1000);

</script>

</body>
</html>
