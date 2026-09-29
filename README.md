<!DOCTYPE html>
<html>
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
    position:relative;
    width:128px;
    height:96px;
    background:#000;
    overflow:hidden;
    font-family:Arial,Helvetica,sans-serif;
}

/* =========================
   RGB COLOUR FORMAT
   ========================= */

:root{
    --white:#FFFFFF;
    --red:#FF0000;
    --green:#00FF00;
    --blue:#008CFF;
    --yellow:#FFFF00;
    --cyan:#00FFFF;
}

/* COMPANY NAME */

.company{
    position:absolute;
    left:0;
    top:3px;
    width:128px;

    color:var(--green);

    text-align:center;
    font-size:7px;
    font-weight:bold;
    white-space:nowrap;
}


/* TOP LINE */

.top-line{
    position:absolute;
    left:0;
    top:14px;

    width:128px;
    height:1px;

    background:var(--white);
}


/* PARAMETER NAME */

.pm-label{
    position:absolute;
    top:21px;

    color:var(--white);

    font-size:6px;
    font-weight:bold;
}

.pm25-label{
    left:12px;
}

.pm10-label{
    left:55px;
}


/* PM VALUES */

.pm-value{
    position:absolute;
    top:31px;

    color:var(--red);

    font-size:13px;
    font-weight:bold;
    line-height:14px;
}

.pm25-value{
    left:12px;
}

.pm10-value{
    left:56px;
}


/* UNITS */

.unit{
    position:absolute;
    top:48px;

    color:var(--white);

    font-size:5px;
}

.pm25-unit{
    left:13px;
}

.pm10-unit{
    left:57px;
}


/* TEMPERATURE + HUMIDITY */

.env{
    position:absolute;
    left:88px;
    top:25px;

    color:var(--white);

    font-size:8px;
    line-height:8px;
    white-space:nowrap;
}


/* TEMPERATURE DOT */

.temp-dot{
    display:inline-block;

    width:4px;
    height:4px;

    border-radius:50%;

    margin-right:5px;

    background:var(--red);
}


/* HUMIDITY DOT */

.hum-dot{
    display:inline-block;

    width:4px;
    height:4px;

    border-radius:50%;

    margin-right:7px;

    background:var(--blue);
}


/* DATE */

.date{
    position:absolute;

    left:93px;
    top:10px;

    color:var(--blue);

    font-size:10px;
    white-space:nowrap;
}


/* TIME */

.time{
    position:absolute;

    left:93px;
    top:68px;

    color:var(--blue);

    font-size:10px;
    white-space:nowrap;
}


/* BOTTOM LINE */

.bottom-line{
    position:absolute;

    left:0;
    top:84px;

    width:128px;
    height:1px;

    background:var(--white);
}

</style>
</head>


    <!-- GREEN COMPANY NAME -->

    <div class="company">
        RUDRA ENTERPRISES
    </div>


    <!-- WHITE LINE -->

    <div class="top-line"></div>


    <!-- PM2.5 -->

    <div class="pm-label pm25-label">
        PM2.5
    </div>

    <div
        class="pm-value pm25-value"
        id="pm25">
        85
    </div>

    <div class="unit pm25-unit">
        µg/m3
    </div>


    <!-- PM10 -->

    <div class="pm-label pm10-label">
        PM10
    </div>

    <div
        class="pm-value pm10-value"
        id="pm10">
        152
    </div>

    <div class="unit pm10-unit">
        µg/m3
    </div>


    <!-- TEMPERATURE / HUMIDITY -->

    <div class="env">

        <span class="temp-dot"></span>
        <span id="temp">
            23.0°C
        </span>

        <br>

        <span class="hum-dot"></span>
        <span id="hum">
            35.0%
        </span>

    </div>


    <!-- BLUE DATE -->

    <div
        class="date"
        id="date">
        24|Jan|2026
    </div>


    <!-- BLUE TIME -->

    <div
        class="time"
        id="time">
        12:21 PM
    </div>




    <!-- WHITE BOTTOM LINE -->

    <div class="bottom-line"></div>

</div>


<script>

/* =========================================
   RUDRA ENTERPRISES
   P10 RGB DMD
   EXACT 128 × 96 PIXELS
   ========================================= */


/* GET URL DATA */

function getData(name,defaultValue){

    const params =
        new URLSearchParams(
            window.location.search
        );

    return params.has(name)
        ? params.get(name)
        : defaultValue;
}


/* UPDATE DISPLAY */

function updateDisplay(){

    /* PM2.5 */

    document.getElementById("pm25").textContent =
        getData("pm25","85");


    /* PM10 */

    document.getElementById("pm10").textContent =
        getData("pm10","152");


    /* TEMPERATURE */

    document.getElementById("temp").textContent =
        getData("temp","23.0") + "°C";


    /* HUMIDITY */

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
        day +
        "|" +
        months[now.getMonth()] +
        "|" +
        now.getFullYear();

    document.getElementById("date").textContent =
        getData("date",currentDate);


    /* TIME */

    let hour =
        now.getHours();

    const ampm =
        hour >= 12 ? "PM" : "AM";

    hour =
        hour % 12 || 12;

    const minute =
        String(now.getMinutes()).padStart(2,"0");

    const currentTime =
        String(hour).padStart(2,"0") +
        ":" +
        minute +
        " " +
        ampm;

    document.getElementById("time").textContent =
        getData("time",currentTime);
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
