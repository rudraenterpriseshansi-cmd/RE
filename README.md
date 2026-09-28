<title>RUDRA ENTERPRISES - P10 RGB DMD</title>

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

    overflow:hidden;

    background:#000;
}


/* ==================================================
   P10 RGB DMD
   EXACT PIXEL SIZE = 128 x 96
   ================================================== */

#ledCanvas{

    width:128px;
    height:96px;

    display:block;

    background:#000;

    image-rendering:pixelated;
    image-rendering:crisp-edges;
}


/* ==================================================
   CENTER 128 x 96 DISPLAY ON SCREEN
   ================================================== */

#screen{

    width:128vw;
    height:96vh;

    display:flex;

    justify-content:center;
    align-items:center;

    background:#000;

    overflow:hidden;
}

</style>
</head>


<body>

<div id="screen">

    <!-- EXACT P10 RGB DMD RESOLUTION -->
    <canvas
        id="ledCanvas"
        width="128"
        height="96">
    </canvas>

</div>


<script>

/* ==================================================
   P10 RGB DMD CONFIGURATION
   ================================================== */

const WIDTH  = 128;
const HEIGHT = 96;

const canvas =
    document.getElementById("ledCanvas");

const ctx =
    canvas.getContext("2d");


/* Disable smoothing */

ctx.imageSmoothingEnabled = false;


/* ==================================================
   SENSOR DATA
   ================================================== */

let data = {

    pm25: 85,

    pm10: 152,

    temperature: 23.0,

    humidity: 35.0

};


/* ==================================================
   COLORS - RGB DISPLAY
   ================================================== */

const BLACK = "#000000";

const WHITE = "#FFFFFF";

const RED = "#FF0000";

const BLUE = "#009CFF";

const GREY = "#777777";


/* ==================================================
   DRAW COMPLETE 128 x 96 DISPLAY
   ================================================== */

function drawDisplay(){

    /* ----------------------------------------------
       BLACK BACKGROUND
       ---------------------------------------------- */

    ctx.fillStyle = BLACK;

    ctx.fillRect(
        0,
        0,
        WIDTH,
        HEIGHT
    );


    /* ----------------------------------------------
       COMPANY NAME
       ---------------------------------------------- */

    ctx.fillStyle = WHITE;

    ctx.font =
        "128 10px Arial";

    ctx.textAlign = "center";

    ctx.textBaseline = "top";

    ctx.fillText(
        "RUDRA ENTERPRISES",
        64,
        3
    );


    /* ----------------------------------------------
       TOP BORDER
       ---------------------------------------------- */

    ctx.fillStyle = WHITE;

    ctx.fillRect(
        0,
        15,
        128,
        1
    );


    ctx.fillStyle = GREY;

    ctx.fillRect(
        0,
        17,
        128,
        1
    );


    /* ----------------------------------------------
       PM2.5 TITLE
       ---------------------------------------------- */

    ctx.fillStyle = WHITE;

    ctx.textAlign = "left";

    ctx.font =
        "128 9px Arial";

    ctx.fillText(
        "PM2.5",
        12,
        22
    );


    /* ----------------------------------------------
       PM10 TITLE
       ---------------------------------------------- */

    ctx.fillText(
        "PM10",
        55,
        22
    );


    /* ----------------------------------------------
       PM2.5 VALUE
       ---------------------------------------------- */

    ctx.fillStyle = RED;

    ctx.font =
        "128 21px Arial";

    ctx.fillText(
        data.pm25,
        12,
        32
    );


    /* ----------------------------------------------
       PM10 VALUE
       ---------------------------------------------- */

    ctx.fillText(
        data.pm10,
        55,
        32
    );


    /* ----------------------------------------------
       PM2.5 UNIT
       ---------------------------------------------- */

    ctx.fillStyle = WHITE;

    ctx.font =
        "6px Arial";

    ctx.fillText(
        "µg/m3",
        13,
        50
    );


    /* ----------------------------------------------
       PM10 UNIT
       ---------------------------------------------- */

    ctx.fillText(
        "µg/m3",
        57,
        50
    );


    /* ----------------------------------------------
       TEMPERATURE RED DOT
       ---------------------------------------------- */

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


    /* ----------------------------------------------
       TEMPERATURE
       ---------------------------------------------- */

    ctx.fillStyle = WHITE;

    ctx.font =
        "7px Arial";

    ctx.fillText(
        Number(data.temperature).toFixed(1) + "°C",
        94,
        22
    );


    /* ----------------------------------------------
       HUMIDITY BLUE DOT
       ---------------------------------------------- */

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


    /* ----------------------------------------------
       HUMIDITY
       ---------------------------------------------- */

    ctx.fillStyle = WHITE;

    ctx.fillText(
        Number(data.humidity).toFixed(1) + "%",
        94,
        29
    );


    /* ----------------------------------------------
       DATE
       ---------------------------------------------- */

    const now = new Date();

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

    const dateText =
        day + "|" + month + "|" + year;


    ctx.fillStyle = WHITE;

    ctx.font =
        "6px Arial";

    ctx.textAlign = "right";

    ctx.fillText(
        dateText,
        119,
        79
    );


    /* ----------------------------------------------
       TIME
       ---------------------------------------------- */

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


    /* ----------------------------------------------
       BOTTOM BORDER
       ---------------------------------------------- */

    ctx.fillStyle = WHITE;

    ctx.fillRect(
        0,
        95,
        128,
        1
    );

}


/* ==================================================
   DRAW DISPLAY
   ================================================== */

drawDisplay();


/* ==================================================
   UPDATE CLOCK EVERY SECOND
   ================================================== */

setInterval(
    drawDisplay,
    1000
);


/* ==================================================
   EXAMPLE LIVE DATA UPDATE
   ==================================================
   
   Later your API can update:

   data.pm25
   data.pm10
   data.temperature
   data.humidity

   Then call:

   drawDisplay();

   ================================================== */

</script>

</body>
</html>
