<!DOCTYPE html>
<html lang="en">
<head>

<meta charset="UTF-8">

<title>Rudra Enterprises - P10 RGB 128x96</title>

<meta name="viewport"
      content="width=device-width,
               height=device-height,
               initial-scale=1.0,
               maximum-scale=1.0,
               user-scalable=no">

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

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
   FULL SCREEN
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
   EXACT P10 RGB DMD
   128 x 96 PIXELS
   ========================================= */

#ledCanvas{

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

    <!-- EXACT 128 x 96 PIXELS -->

    <canvas
        id="ledCanvas"
        width="128"
        height="96">
    </canvas>

</div>


<script>

/* =================================================
   P10 RGB DMD RESOLUTION
   ================================================= */

const WIDTH  = 128;
const HEIGHT = 96;


/* =================================================
   CANVAS
   ================================================= */

const canvas =
    document.getElementById("ledCanvas");

const ctx =
    canvas.getContext("2d");

ctx.imageSmoothingEnabled = false;


/* =================================================
   RGB COLORS
   ================================================= */

const BLACK = "#000000";

const WHITE = "#FFFFFF";

const RED = "#FF0000";

const BLUE = "#009CFF";


/* =================================================
   LIVE DATA
   ================================================= */

let data = {

    pm25: 85,

    pm10: 152,

    temperature: 23.0,

    humidity: 35.0

};


/* =================================================
   DRAW DISPLAY
   ================================================= */

function drawDisplay(){

    /* -----------------------------------------
       BLACK BACKGROUND
       ----------------------------------------- */

    ctx.fillStyle = BLACK;

    ctx.fillRect(
        0,
        0,
        WIDTH,
        HEIGHT
    );


    /* =========================================
       RUDRA ENTERPRISES
       ========================================= */

    ctx.fillStyle = WHITE;

    ctx.font =
        "900 10px Arial";

    ctx.textAlign = "center";

    ctx.textBaseline = "top";

    ctx.fillText(
        "RUDRA ENTERPRISES",
        64,
        3
    );


    /* =========================================
       PM2.5 TITLE
       
       MOVED DOWN 10 PIXELS
       ========================================= */

    ctx.textAlign = "left";

    ctx.font =
        "900 9px Arial";

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
       
       MOVED DOWN 10 PIXELS
       ========================================= */

    ctx.fillStyle = RED;

    ctx.font =
        "900 21px Arial";

    ctx.fillText(
        data.pm25,
        12,
        42
    );


    /* =========================================
       PM10 VALUE
       ========================================= */

    ctx.fillText(
        data.pm10,
        55,
        42
    );


    /* =========================================
       PM2.5 UNIT
       ========================================= */

    ctx.fillStyle = WHITE;

    ctx.font =
        "6px Arial";

    ctx.fillText(
        "µg/m3",
        13,
        60
    );


    /* =========================================
       PM10 UNIT
       ========================================= */

    ctx.fillText(
        "µg/m3",
        57,
        60
    );


    /* =========================================
       TEMPERATURE RED DOT
       ========================================= */

    ctx.fillStyle = RED;

    ctx.beginPath();

    ctx.ellipse(
        89,
        27,
        3,
        5,
        0,
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
        Number(data.temperature)
        .toFixed(1) + "°C",

        94,
        22
    );


    /* =========================================
       HUMIDITY BLUE DOT
       ========================================= */

    ctx.fillStyle = BLUE;

    ctx.beginPath();

    ctx.ellipse(
        89,
        34,
        3,
        5,
        0,
        0,
        Math.PI * 2
    );

    ctx.fill();


    /* =========================================
       HUMIDITY
       ========================================= */

    ctx.fillStyle = WHITE;

    ctx.fillText(
        Number(data.humidity)
        .toFixed(1) + "%",

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


    const dateText =
        day +
        "|" +
        month +
        "|" +
        year;


    ctx.fillStyle = WHITE;

    ctx.font =
        "6px Arial";

    ctx.textAlign = "right";

    ctx.fillText(
        dateText,
        119,
        79
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
        86
    );

}


/* =================================================
   FIRST DISPLAY
   ================================================= */

drawDisplay();


/* =================================================
   CLOCK UPDATE
   ================================================= */

setInterval(
    drawDisplay,
    1000
);

</script>

</body>
</html>
