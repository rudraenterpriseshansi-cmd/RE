<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">

<meta name="viewport"
      content="width=device-width,
               height=device-height,
               initial-scale=1.0,
               maximum-scale=1.0,
               user-scalable=no">

<title>RUDRA ENTERPRISES</title>

<style>

/* =====================================================
   RESET
   ===================================================== */

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

html,
body{
    width:100%;
    height:100%;

    background:#000;

    overflow:hidden;
}


/* =====================================================
   FULL SCREEN
   ===================================================== */

#screen{

    width:100vw;
    height:100vh;

    display:flex;

    justify-content:center;
    align-items:center;

    background:#000;

    overflow:hidden;
}


/* =====================================================
   EXACT DISPLAY
   128 x 96 PIXELS
   ===================================================== */

#display{

    position:relative;

    width:128px;
    height:96px;

    background:#000;

    color:#fff;

    font-family:
        Arial,
        Helvetica,
        sans-serif;

    overflow:hidden;

    transform-origin:center center;
}


/* =====================================================
   COMPANY NAME
   ===================================================== */

.company{

    position:absolute;

    left:0;
    top:3px;

    width:128px;

    text-align:center;

    color:#fff;

    font-size:7.8px;

    line-height:9px;

    font-weight:900;

    letter-spacing:0;

    white-space:nowrap;
}


/* =====================================================
   TOP DOUBLE LINE
   ===================================================== */

.line1{

    position:absolute;

    left:0;
    top:18px;

    width:128px;
    height:1px;

    background:#fff;
}


.line2{

    position:absolute;

    left:0;
    top:19px;

    width:128px;
    height:1px;

    background:#777;
}


.line3{

    position:absolute;

    left:0;
    top:20px;

    width:128px;
    height:1px;

    background:#444;
}


/* =====================================================
   PM2.5 TITLE
   ===================================================== */

.pm25-title{

    position:absolute;

    left:12px;
    top:27px;

    color:#fff;

    font-size:7.2px;

    line-height:8px;

    font-weight:900;

    white-space:nowrap;
}


/* =====================================================
   PM10 TITLE
   ===================================================== */

.pm10-title{

    position:absolute;

    left:55px;
    top:27px;

    color:#fff;

    font-size:7.2px;

    line-height:8px;

    font-weight:900;

    white-space:nowrap;
}


/* =====================================================
   PM2.5 VALUE
   ===================================================== */

.pm25-value{

    position:absolute;

    left:12px;
    top:39px;

    color:#ff0000;

    font-size:15px;

    line-height:16px;

    font-weight:900;

    white-space:nowrap;
}


/* =====================================================
   PM10 VALUE
   ===================================================== */

.pm10-value{

    position:absolute;

    left:55px;
    top:39px;

    color:#ff0000;

    font-size:15px;

    line-height:16px;

    font-weight:900;

    white-space:nowrap;
}


/* =====================================================
   PM2.5 UNIT
   ===================================================== */

.unit25{

    position:absolute;

    left:13px;
    top:55px;

    color:#fff;

    font-size:6px;

    line-height:7px;

    white-space:nowrap;
}


/* =====================================================
   PM10 UNIT
   ===================================================== */

.unit10{

    position:absolute;

    left:57px;
    top:55px;

    color:#fff;

    font-size:6px;

    line-height:7px;

    white-space:nowrap;
}


/* =====================================================
   RED TEMPERATURE DOT
   ===================================================== */

.temp-dot{

    position:absolute;

    left:89px;
    top:27px;

    width:4px;
    height:7px;

    background:#ff0000;

    border-radius:50%;
}


/* =====================================================
   TEMPERATURE
   ===================================================== */

.temp{

    position:absolute;

    left:94px;
    top:26px;

    color:#fff;

    font-size:6.5px;

    line-height:8px;

    white-space:nowrap;
}


/* =====================================================
   BLUE HUMIDITY DOT
   ===================================================== */

.hum-dot{

    position:absolute;

    left:89px;
    top:35px;

    width:4px;
    height:7px;

    background:#009cff;

    border-radius:50%;
}


/* =====================================================
   HUMIDITY
   ===================================================== */

.hum{

    position:absolute;

    left:94px;
    top:34px;

    color:#fff;

    font-size:6.5px;

    line-height:8px;

    white-space:nowrap;
}


/* =====================================================
   DATE
   ===================================================== */

.date{

    position:absolute;

    right:9px;
    top:80px;

    color:#fff;

    font-size:5.5px;

    line-height:7px;

    white-space:nowrap;
}


/* =====================================================
   TIME
   ===================================================== */

.time{

    position:absolute;

    right:9px;
    top:87px;

    color:#fff;

    font-size:5.5px;

    line-height:7px;

    white-space:nowrap;
}


/* =====================================================
   BOTTOM LINE
   ===================================================== */

.bottom-line{

    position:absolute;

    left:0;
    top:87px;

    width:128px;

    height:1px;

    background:#fff;
}


/* =====================================================
   AUTO SCALE
   ===================================================== */

</style>

</head>


<body>


<div id="screen">


<div id="display">


<!-- =================================================
     COMPANY
     ================================================= -->

<div class="company">
    RUDRA ENTERPRISES
</div>


<!-- =================================================
     TOP LINES
     ================================================= -->

<div class="line1"></div>
<div class="line2"></div>
<div class="line3"></div>


<!-- =================================================
     PM2.5
     ================================================= -->

<div class="pm25-title">
    PM2.5
</div>

<div id="pm25"
     class="pm25-value">
    85
</div>

<div class="unit25">
    µg/m3
</div>


<!-- =================================================
     PM10
     ================================================= -->

<div class="pm10-title">
    PM10
</div>

<div id="pm10"
     class="pm10-value">
    152
</div>

<div class="unit10">
    µg/m3
</div>


<!-- =================================================
     TEMPERATURE
     ================================================= -->

<div class="temp-dot"></div>

<div id="temperature"
     class="temp">
    23.0°C
</div>


<!-- =================================================
     HUMIDITY
     ================================================= -->

<div class="hum-dot"></div>

<div id="humidity"
     class="hum">
    35.0%
</div>


<!-- =================================================
     DATE
     ================================================= -->

<div id="date"
     class="date">
    24|Jan|2026
</div>


<!-- =================================================
     TIME
     ================================================= -->

<div id="time"
     class="time">
    12:21 PM
</div>


<!-- =================================================
     BOTTOM LINE
     ================================================= -->

<div class="bottom-line"></div>


</div>

</div>


<script>

/* =====================================================
   DISPLAY DATA
   ===================================================== */

let data = {

    pm25: 85,

    pm10: 152,

    temperature: 23.0,

    humidity: 35.0

};


/* =====================================================
   UPDATE SENSOR VALUES
   ===================================================== */

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


/* =====================================================
   DATE & TIME
   ===================================================== */

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


/* =====================================================
   SCALE 128 x 96 TO FULL SCREEN
   ===================================================== */

function scaleDisplay(){

    const display =
        document.getElementById("display");


    const scaleX =
        window.innerWidth / 128;


    const scaleY =
        window.innerHeight / 96;


    const scale =
        Math.min(scaleX,scaleY);


    display.style.transform =
        "scale(" + scale + ")";

}


/* =====================================================
   START
   ===================================================== */

updateDisplay();

updateDateTime();

scaleDisplay();


/* =====================================================
   CLOCK
   ===================================================== */

setInterval(
    updateDateTime,
    1000
);


/* =====================================================
   SCREEN RESIZE
   ===================================================== */

window.addEventListener(
    "resize",
    scaleDisplay
);

</script>


</body>
</html>
