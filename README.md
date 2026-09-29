<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">

<!-- P10 RGB / HD Player -->
<meta name="viewport"
      content="width=128,height=96,initial-scale=1.0,
               maximum-scale=1.0,user-scalable=no">

<title>RUDRA ENTERPRISES</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

html,body{
    width:100%;
    height:100%;
    background:#000;
    overflow:hidden;
}

body{
    display:flex;
    align-items:center;
    justify-content:center;
    font-family:Arial,Helvetica,sans-serif;
}

/* EXACT 128 x 96 PIXEL DISPLAY */
#display{
    width:128px;
    height:96px;
    position:relative;
    background:#000;
    color:#fff;
    overflow:hidden;
    transform-origin:center center;
}

/* COMPANY NAME */
.title{
    position:absolute;
    left:5px;
    top:3px;
    width:118px;
    text-align:center;
    font-size:7px;
    font-weight:bold;
    white-space:nowrap;
}

/* TOP LINE */
.topline{
    position:absolute;
    left:0;
    top:14px;
    width:128px;
    height:1px;
    background:#fff;
}

/* PARAMETER NAME */
.label{
    position:absolute;
    top:22px;
    font-size:6px;
    font-weight:bold;
}

.pm25label{
    left:12px;
}

.pm10label{
    left:55px;
}

/* PM VALUES */
.value{
    position:absolute;
    top:34px;
    font-size:12px;
    line-height:12px;
    font-weight:bold;
    color:#ff0000;
}

.pm25value{
    left:12px;
}

.pm10value{
    left:56px;
}

/* UNIT */
.unit{
    position:absolute;
    top:49px;
    font-size:5px;
    white-space:nowrap;
}

.pm25unit{
    left:13px;
}

.pm10unit{
    left:57px;
}

/* TEMPERATURE / HUMIDITY */
.environment{
    position:absolute;
    right:8px;
    top:22px;
    font-size:5.5px;
    line-height:8px;
    white-space:nowrap;
}

.dot{
    display:inline-block;
    width:4px;
    height:4px;
    border-radius:50%;
    margin-right:2px;
}

.red{
    background:#ff0000;
}

.blue{
    background:#0099ff;
}

/* DATE */
.date{
    position:absolute;
    right:9px;
    top:61px;
    font-size:5px;
    white-space:nowrap;
}

/* TIME */
.time{
    position:absolute;
    right:9px;
    top:68px;
    font-size:5px;
    white-space:nowrap;
}

/* BOTTOM LINE */
.bottomline{
    position:absolute;
    left:0;
    top:74px;
    width:128px;
    height:1px;
    background:#fff;
}
</style>
</head>

<body>

<div id="display">

    <div class="title">
        RUDRA ENTERPRISES
    </div>

    <div class="topline"></div>

    <div class="label pm25label">
        PM2.5
    </div>

    <div class="label pm10label">
        PM10
    </div>

    <div class="value pm25value" id="pm25">
        85
    </div>

    <div class="value pm10value" id="pm10">
        152
    </div>

    <div class="unit pm25unit">
        µg/m3
    </div>

    <div class="unit pm10unit">
        µg/m3
    </div>

    <div class="environment">

        <span class="dot red"></span>
        <span id="temp">23.0°C</span>

        <br>

        <span class="dot blue"></span>
        <span id="hum">35.0%</span>

    </div>

    <div class="date" id="date">
        24|Jan|2026
    </div>

    <div class="time" id="time">
        12:21 PM
    </div>

    <div class="bottomline"></div>

</div>


<script>

/* ==========================================
   RUDRA ENTERPRISES
   P10 RGB HD PLAYER
   DISPLAY SIZE: 128 x 96 PIXELS
   ========================================== */


/* GET DATA FROM URL */

function getParam(name, fallback){

    const params =
        new URLSearchParams(window.location.search);

    return params.get(name) !== null
        ? params.get(name)
        : fallback;
}


/* UPDATE DISPLAY */

function updateDisplay(){

    /* PM2.5 */

    document.getElementById("pm25").textContent =
        getParam("pm25","85");


    /* PM10 */

    document.getElementById("pm10").textContent =
        getParam("pm10","152");


    /* TEMPERATURE */

    let temp =
        getParam("temp","23.0");

    document.getElementById("temp").textContent =
        temp.toString().includes("°")
        ? temp
        : temp + "°C";


    /* HUMIDITY */

    let hum =
        getParam("hum","35.0");

    document.getElementById("hum").textContent =
        hum.toString().includes("%")
        ? hum
        : hum + "%";


    /* DATE + TIME */

    const now = new Date();

    const months = [
        "Jan","Feb","Mar","Apr",
        "May","Jun","Jul","Aug",
        "Sep","Oct","Nov","Dec"
    ];

    const day =
        String(now.getDate()).padStart(2,"0");

    const date =
        day + "|" +
        months[now.getMonth()] + "|" +
        now.getFullYear();


    let hour =
        now.getHours();

    const ampm =
        hour >= 12 ? "PM" : "AM";

    hour =
        hour % 12 || 12;

    const minute =
        String(now.getMinutes())
        .padStart(2,"0");


    document.getElementById("date").textContent =
        getParam("date",date);


    document.getElementById("time").textContent =
        getParam(
            "time",
            String(hour).padStart(2,"0")
            + ":" +
            minute
            + " "
            + ampm
        );
}


/* FIT 128 x 96 TO HD PLAYER SCREEN */

function fitDisplay(){

    const display =
        document.getElementById("display");

    const scale =
        Math.min(
            window.innerWidth / 128,
            window.innerHeight / 96
        );

    display.style.transform =
        "scale(" + scale + ")";
}


/* START */

updateDisplay();

fitDisplay();


/* WINDOW RESIZE */

window.addEventListener(
    "resize",
    fitDisplay
);


/* UPDATE EVERY SECOND */

setInterval(
    updateDisplay,
    1000
);

</script>

</body>
</html>
