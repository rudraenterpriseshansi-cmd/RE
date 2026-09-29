<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">

<title>RUDRA ENTERPRISES</title>

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

html,body{
    width:128px;
    height:96px;
    background:#000;
    overflow:hidden;
}

#display{
    position:relative;

    /* EXACT SIZE */
    width:128px;
    height:96px;

    background:#000;
    color:#fff;

    font-family:Arial,Helvetica,sans-serif;
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

/* VALUES */
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

    <!-- COMPANY -->
    <div class="title">
        RUDRA ENTERPRISES
    </div>

    <!-- LINE -->
    <div class="topline"></div>


    <!-- PM2.5 -->
    <div class="label pm25label">
        PM2.5
    </div>

    <div class="value pm25value" id="pm25">
        85
    </div>

    <div class="unit pm25unit">
        µg/m3
    </div>


    <!-- PM10 -->
    <div class="label pm10label">
        PM10
    </div>

    <div class="value pm10value" id="pm10">
        152
    </div>

    <div class="unit pm10unit">
        µg/m3
    </div>


    <!-- TEMP / HUMIDITY -->
    <div class="environment">

        <span class="dot red"></span>
        <span id="temp">23.0°C</span>

        <br>

        <span class="dot blue"></span>
        <span id="hum">35.0%</span>

    </div>


    <!-- DATE -->
    <div class="date" id="date">
        24|Jan|2026
    </div>


    <!-- TIME -->
    <div class="time" id="time">
        12:21 PM
    </div>


    <!-- BOTTOM LINE -->
    <div class="bottomline"></div>

</div>


<script>

/* =========================================
   EXACT DISPLAY SIZE
   WIDTH  = 128 PIXELS
   HEIGHT = 96 PIXELS
   ========================================= */


/* READ URL PARAMETERS */

function getParam(name, defaultValue){

    const url =
        new URLSearchParams(
            window.location.search
        );

    return url.get(name) || defaultValue;
}


/* UPDATE DATA */

function updateDisplay(){

    document.getElementById("pm25").innerText =
        getParam("pm25","85");

    document.getElementById("pm10").innerText =
        getParam("pm10","152");

    document.getElementById("temp").innerText =
        getParam("temp","23.0") + "°C";

    document.getElementById("hum").innerText =
        getParam("hum","35.0") + "%";


    /* DATE */

    const now = new Date();

    const months = [
        "Jan","Feb","Mar","Apr",
        "May","Jun","Jul","Aug",
        "Sep","Oct","Nov","Dec"
    ];

    const day =
        String(now.getDate()).padStart(2,"0");

    const date =
        day +
        "|" +
        months[now.getMonth()] +
        "|" +
        now.getFullYear();

    document.getElementById("date").innerText =
        getParam("date",date);


    /* TIME */

    let hour = now.getHours();

    const ampm =
        hour >= 12 ? "PM" : "AM";

    hour =
        hour % 12 || 12;

    const minute =
        String(now.getMinutes()).padStart(2,"0");

    const time =
        String(hour).padStart(2,"0") +
        ":" +
        minute +
        " " +
        ampm;

    document.getElementById("time").innerText =
        getParam("time",time);
}


/* START */

updateDisplay();


/* UPDATE EVERY SECOND */

setInterval(
    updateDisplay,
    1000
);

</script>

</body>
</html>
