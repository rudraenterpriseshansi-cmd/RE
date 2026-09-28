<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">

<title>Rudra Enterprises AQMS Display</title>

<style>

/* =========================
   128 x 96 P10 DISPLAY
   ========================= */

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

html,
body{
    width:128px;
    height:96px;
    margin:0;
    padding:0;
    overflow:hidden;
    background:#000;
}

#display{
    position:relative;

    width:128px;
    height:96px;

    background:#000;
    color:#fff;

    font-family:Arial, Helvetica, sans-serif;

    overflow:hidden;
}


/* =========================
   COMPANY NAME
   ========================= */

.company{
    position:absolute;

    top:3px;
    left:0;

    width:128px;
    height:14px;

    text-align:center;

    font-size:7.8px;
    line-height:9px;

    font-weight:900;

    white-space:nowrap;

    color:#fff;
}


/* =========================
   TOP BORDER
   ========================= */

.line1{
    position:absolute;

    top:15px;
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


/* =========================
   PM2.5 TITLE
   ========================= */

.pm25-title{
    position:absolute;

    top:22px;
    left:12px;

    font-size:7px;
    line-height:8px;

    font-weight:900;

    color:#fff;
}


/* =========================
   PM10 TITLE
   ========================= */

.pm10-title{
    position:absolute;

    top:22px;
    left:55px;

    font-size:7px;
    line-height:8px;

    font-weight:900;

    color:#fff;
}


/* =========================
   PM2.5 VALUE
   ========================= */

.pm25-value{
    position:absolute;

    top:31px;
    left:12px;

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

    top:31px;
    left:55px;

    font-size:15px;
    line-height:16px;

    font-weight:900;

    color:#ff0000;

    white-space:nowrap;
}


/* =========================
   PM2.5 UNIT
   ========================= */

.unit25{
    position:absolute;

    top:48px;
    left:13px;

    font-size:6px;
    line-height:7px;

    color:#fff;

    white-space:nowrap;
}


/* =========================
   PM10 UNIT
   ========================= */

.unit10{
    position:absolute;

    top:48px;
    left:57px;

    font-size:6px;
    line-height:7px;

    color:#fff;

    white-space:nowrap;
}


/* =========================
   TEMPERATURE DOT
   ========================= */

.temp-dot{
    position:absolute;

    top:23px;
    left:89px;

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

    top:22px;
    left:94px;

    font-size:6.5px;
    line-height:8px;

    color:#fff;

    white-space:nowrap;
}


/* =========================
   HUMIDITY DOT
   ========================= */

.hum-dot{
    position:absolute;

    top:30px;
    left:89px;

    width:4px;
    height:7px;

    background:#0099ff;

    border-radius:50%;
}


/* =========================
   HUMIDITY
   ========================= */

.hum{
    position:absolute;

    top:29px;
    left:94px;

    font-size:6.5px;
    line-height:8px;

    color:#fff;

    white-space:nowrap;
}


/* =========================
   DATE
   ========================= */

.date{
    position:absolute;

    top:79px;
    right:9px;

    font-size:5.5px;
    line-height:7px;

    color:#fff;

    white-space:nowrap;
}


/* =========================
   TIME
   ========================= */

.time{
    position:absolute;

    top:86px;
    right:9px;

    font-size:5.5px;
    line-height:7px;

    color:#fff;

    white-space:nowrap;
}


/* =========================
   BOTTOM BORDER
   ========================= */

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


    <!-- BOTTOM BORDER -->
    <div class="bottom-line"></div>

</div>


<script>

/* =========================
   DEMO DATA
   ========================= */

let data = {

    pm25: 85,

    pm10: 152,

    temperature: 23.0,

    humidity: 35.0

};


/* =========================
   UPDATE SENSOR DATA
   ========================= */

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


/* =========================
   DATE & TIME
   ========================= */

function updateDateTime(){

    const now = new Date();


    /* DATE */

    const day =
        String(now.getDate()).padStart(2,"0");


    const months = [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec"
    ];


    const month =
        months[now.getMonth()];


    const year =
        now.getFullYear();


    document.getElementById("date").innerText =
        day + "|" + month + "|" + year;


    /* TIME */

    let hours =
        now.getHours();


    const minutes =
        String(now.getMinutes()).padStart(2,"0");


    const ampm =
        hours >= 12 ? "PM" : "AM";


    hours =
        hours % 12;


    if(hours === 0){
        hours = 12;
    }


    document.getElementById("time").innerText =
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
