<!DOCTYPE html>
<html lang="en">

<head>
<meta charset="UTF-8">

<title>RUDRA ENTERPRISES</title>

<style>

/* =========================================
   RESET
   ========================================= */

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}


/* =========================================
   PAGE
   ========================================= */

html,
body{
    width:100%;
    height:100%;

    margin:0;
    padding:0;

    overflow:hidden;

    background:#000;
}


/* =========================================
   SCREEN
   ========================================= */

#screen{
    width:100vw;
    height:100vh;

    display:flex;

    justify-content:center;
    align-items:center;

    background:#000;

    overflow:hidden;
}


/* =========================================
   P10 RGB DMD
   EXACT 128 x 96 PIXELS
   ========================================= */

#display{

    width:128px;
    height:96px;

    display:block;

    background:#000;

    image-rendering:pixelated;
    image-rendering:crisp-edges;
}

</style>

</head>


<body>

<div id="screen">

<canvas
    id="display"
    width="128"
    height="96">
</canvas>

</div>


<script>

/* =========================================
   CANVAS
   ========================================= */

const canvas =
    document.getElementById("display");

const ctx =
    canvas.getContext("2d");

ctx.imageSmoothingEnabled = false;


/* =========================================
   FIXED DMD SIZE
   ========================================= */

const W = 128;
const H = 96;


/* =========================================
   COLORS
   ========================================= */

const BLACK = "#000000";
const WHITE = "#FFFFFF";
const RED   = "#FF0000";
const BLUE  = "#0099FF";


/* =========================================
   SENSOR DATA
   ========================================= */

let pm25 = 85;
let pm10 = 152;

let temperature = 23.0;
let humidity = 35.0;


/* =========================================
   DRAW DISPLAY
   ========================================= */

function drawDisplay(){

    /* -----------------------------------------
       CLEAR DISPLAY
       ----------------------------------------- */

    ctx.fillStyle = BLACK;

    ctx.fillRect(
        0,
        0,
        W,
        H
    );


    /* =========================================
       COMPANY NAME
       ========================================= */

    ctx.fillStyle = WHITE;

    ctx.font =
        "bold 9px Arial";

    ctx.textAlign = "center";

    ctx.textBaseline = "top";

    ctx.fillText(
        "RUDRA ENTERPRISES",
        64,
        3
    );


    /* =========================================
       PM2.5 TITLE
       ========================================= */

    ctx.textAlign = "left";

    ctx.font =
        "bold 8px Arial";

    ctx.fillStyle = WHITE;

    ctx.fillText(
        "PM2.5",
        12,
        32
    );


    /* =========================================
       PM10 TITLE
       ========================================= */

    ctx.fillText(
        "PM10",
        55,
        32
    );


    /* =========================================
       PM2.5 VALUE
       ========================================= */

    ctx.font =
        "bold 20px Arial";

    ctx.fillStyle = RED;

    ctx.fillText(
        pm25,
        12,
        42
    );


    /* =========================================
       PM10 VALUE
       ========================================= */

    ctx.fillText(
        pm10,
        55,
        42
    );


    /* =========================================
       PM2.5 UNIT
       ========================================= */

    ctx.font =
        "6px Arial";

    ctx.fillStyle = WHITE;

    ctx.fillText(
        "µg/m3",
        13,
        61
    );


    /* =========================================
       PM10 UNIT
       ========================================= */

    ctx.fillText(
        "µg/m3",
        57,
        61
    );


    /* =========================================
       TEMPERATURE RED DOT
       ========================================= */

    ctx.fillStyle = RED;

    ctx.beginPath();

    ctx.arc(
        89,
        28,
        3,
        0,
        Math.PI * 2
    );

    ctx.fill();


    /* =========================================
       TEMPERATURE
       ========================================= */

    ctx.fillStyle = WHITE;

    ctx.font =
        "7px Arial";

    ctx.fillText(
        temperature.toFixed(1) + "°C",
        94,
        22
    );


    /* =========================================
       HUMIDITY BLUE DOT
       ========================================= */

    ctx.fillStyle = BLUE;

    ctx.beginPath();

    ctx.arc(
        89,
        35,
        3,
        0,
        Math.PI * 2
    );

    ctx.fill();


    /* =========================================
       HUMIDITY
       ========================================= */

    ctx.fillStyle = WHITE;

    ctx.fillText(
        humidity.toFixed(1) + "%",
        94,
        29
    );


    /* =========================================
       DATE
       ========================================= */

    const now = new Date();

    const day =
        String(
            now.getDate()
        ).padStart(2,"0");


    const monthNames = [

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
        monthNames[
            now.getMonth()
        ];


    const year =
        now.getFullYear();


    const dateText =
        day +
        "|" +
        month +
        "|" +
        year;


    ctx.textAlign = "right";

    ctx.font =
        "6px Arial";

    ctx.fillStyle = WHITE;

    ctx.fillText(
        dateText,
        119,
        78
    );


    /* =========================================
       TIME
       ========================================= */

    let hours =
        now.getHours();


    const minutes =
        String(
            now.getMinutes()
        ).padStart(2,"0");


    const ampm =
        hours >= 12
        ? "PM"
        : "AM";


    hours =
        hours % 12;


    if(hours === 0){
        hours = 12;
    }


    const timeText =
        hours +
        ":" +
        minutes +
        " " +
        ampm;


    ctx.fillText(
        timeText,
        119,
        85
    );

}


/* =========================================
   START
   ========================================= */

drawDisplay();


/* =========================================
   UPDATE CLOCK
   ========================================= */

setInterval(
    drawDisplay,
    1000
);

</script>

</body>
</html>
