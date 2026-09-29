<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=128,height=96">
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
    width:128px;
    height:96px;
    position:relative;
    background:#000;
    overflow:hidden;
    font-family:Arial,Helvetica,sans-serif;
}

/* RUDRA ENTERPRISES */
.company{
    position:absolute;
    left:0;
    top:3px;
    width:128px;
    height:9px;
    color:#fff;
    text-align:center;
    font-size:7px;
    font-weight:bold;
    line-height:9px;
    white-space:nowrap;
}

/* TOP LINE */
.top-line{
    position:absolute;
    left:0;
    top:14px;
    width:128px;
    height:1px;
    background:#fff;
}

/* LABELS */
.pm-label{
    position:absolute;
    top:21px;
    color:#fff;
    font-size:6px;
    font-weight:bold;
}

.pm25-label{left:12px;}
.pm10-label{left:55px;}

/* VALUES */
.pm-value{
    position:absolute;
    top:31px;
    color:#ff0000;
    font-size:13px;
    font-weight:bold;
    line-height:14px;
}

.pm25-value{left:12px;}
.pm10-value{left:56px;}

/* UNITS */
.unit{
    position:absolute;
    top:48px;
    color:#fff;
    font-size:5px;
}

.pm25-unit{left:13px;}
.pm10-unit{left:57px;}

/* TEMPERATURE + HUMIDITY */
.env{
    position:absolute;
    left:88px;
    top:21px;
    color:#fff;
    font-size:5px;
    line-height:8px;
    white-space:nowrap;
}

.red-dot,
.blue-dot{
    display:inline-block;
    width:4px;
    height:4px;
    border-radius:50%;
    margin-right:2px;
}

.red-dot{
    background:#ff0000;
}

.blue-dot{
    background:#008cff;
}

/* DATE */
.date{
    position:absolute;
    left:86px;
    top:61px;
    color:#fff;
    font-size:5px;
}

/* TIME */
.time{
    position:absolute;
    left:93px;
    top:68px;
    color:#fff;
    font-size:5px;
}

/* BOTTOM LINE */
.bottom-line{
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

    <div class="company">
        RUDRA ENTERPRISES
    </div>

    <div class="top-line"></div>

    <div class="pm-label pm25-label">
        PM2.5
    </div>

    <div class="pm-label pm10-label">
        PM10
    </div>

    <div class="pm-value pm25-value" id="pm25">
        85
    </div>

    <div class="pm-value pm10-value" id="pm10">
        152
    </div>

    <div class="unit pm25-unit">
        µg/m3
    </div>

    <div class="unit pm10-unit">
        µg/m3
    </div>

    <div class="env">
        <span class="red-dot"></span>
        <span id="temp">23.0°C</span>
        <br>
        <span class="blue-dot"></span>
        <span id="hum">35.0%</span>
    </div>

    <div class="date" id="date">
        24|Jan|2026
    </div>

    <div class="time" id="time">
        12:21 PM
    </div>

    <div class="bottom-line"></div>

</div>

<script>

/* ==========================================
   RUDRA ENTERPRISES
   P10 RGB DMD
   EXACT SIZE: 128 x 96 PIXELS
   ========================================== */

function getData(name, defaultValue){

    const url =
        new URLSearchParams(
            window.location.search
        );

    return url.has(name)
        ? url.get(name)
        : defaultValue;
}


function updateDisplay(){

    /* PM2.5 */
    document.getElementById("pm25").textContent =
        getData("pm25","85");

    /* PM10 */
    document.getElementById("pm10").textContent =
        getData("pm10","152");

    /* Temperature */
    document.getElementById("temp").textContent =
        getData("temp","23.0") + "°C";

    /* Humidity */
    document.getElementById("hum").textContent =
        getData("hum","35.0") + "%";


    /* DATE */

    const now = new Date();

    const months = [
        "Jan","Feb","Mar","Apr",
        "May","Jun","Jul","Aug",
        "Sep","Oct","Nov","Dec"
    ];

    const day =
        String(now.getDate()).padStart(2,"0");

    const currentDate =
        day + "|" +
        months[now.getMonth()] + "|" +
        now.getFullYear();

    document.getElementById("date").textContent =
        getData("date",currentDate);


    /* TIME */

    let hour = now.getHours();

    const ampm =
        hour >= 12 ? "PM" : "AM";

    hour =
        hour % 12 || 12;

    const minute =
        String(now.getMinutes()).padStart(2,"0");

    const currentTime =
        String(hour).padStart(2,"0")
        + ":" +
        minute
        + " "
        + ampm;

    document.getElementById("time").textContent =
        getData("time",currentTime);
}


updateDisplay();

setInterval(updateDisplay,1000);

</script>

</body>
</html>
