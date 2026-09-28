<head>
<meta charset="UTF-8">

<title>RUDRA ENTERPRISES</title>

<style>

html,
body{
    margin:0;
    padding:0;
    width:100%;
    height:100%;
    background:#000;
    overflow:hidden;
}

#screen{
    width:100vw;
    height:100vh;
    background:#000;

    display:flex;
    justify-content:center;
    align-items:center;
}

canvas{
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

const canvas = document.getElementById("display");
const ctx = canvas.getContext("2d");

ctx.imageSmoothingEnabled = false;


/* ==================================================
   DATA
   ================================================== */

let PM25 = 85;
let PM10 = 152;

let TEMPERATURE = 23.0;
let HUMIDITY = 35.0;


/* ==================================================
   DRAW
   ================================================== */

function draw(){

    /* BLACK BACKGROUND */

    ctx.fillStyle = "#000000";

    ctx.fillRect(
        0,
        0,
        128,
        96
    );


    /* =================================================
       RUDRA ENTERPRISES
       NO RE
       NO LINE
       ================================================= */

    ctx.fillStyle = "#FFFFFF";

    ctx.font = "bold 9px Arial";

    ctx.textAlign = "center";

    ctx.textBaseline = "top";

    ctx.fillText(
        "RUDRA ENTERPRISES",
        64,
        3
    );


    /* =================================================
       PM2.5 TITLE
       MOVED DOWN 10 PIXELS
       ================================================= */

    ctx.textAlign = "left";

    ctx.font = "bold 8px Arial";

    ctx.fillStyle = "#FFFFFF";

    ctx.fillText(
        "PM2.5",
        12,
        32
    );


    /* =================================================
       PM10 TITLE
       ================================================= */

    ctx.fillText(
        "PM10",
        55,
        32
    );


    /* =================================================
       PM2.5 VALUE
       ================================================= */

    ctx.font = "bold 20px Arial";

    ctx.fillStyle = "#FF0000";

    ctx.fillText(
        PM25,
        12,
        42
    );


    /* =================================================
       PM10 VALUE
       ================================================= */

    ctx.fillText(
        PM10,
        55,
        42
    );


    /* =================================================
       UNITS
       ================================================= */

    ctx.font = "6px Arial";

    ctx.fillStyle = "#FFFFFF";

    ctx.fillText(
        "µg/m3",
        13,
        60
    );

    ctx.fillText(
        "µg/m3",
        57,
        60
    );


    /* =================================================
       TEMPERATURE RED DOT
       ================================================= */

    ctx.fillStyle = "#FF0000";

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


    /* =================================================
       TEMPERATURE
       ================================================= */

    ctx.fillStyle = "#FFFFFF";

    ctx.font = "7px Arial";

    ctx.fillText(
        TEMPERATURE.toFixed(1) + "°C",
        94,
        22
    );


    /* =================================================
       HUMIDITY BLUE DOT
       ================================================= */

    ctx.fillStyle = "#009CFF";

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


    /* =================================================
       HUMIDITY
       ================================================= */

    ctx.fillStyle = "#FFFFFF";

    ctx.font = "7px Arial";

    ctx.fillText(
        HUMIDITY.toFixed(1) + "%",
        94,
        29
    );


    /* =================================================
       DATE
       ================================================= */

    const now = new Date();

    const day =
        String(now.getDate()).padStart(2,"0");

    const months = [
        "Jan","Feb","Mar","Apr",
        "May","Jun","Jul","Aug",
        "Sep","Oct","Nov","Dec"
    ];

    const month =
        months[now.getMonth()];

    const year =
        now.getFullYear();

    const date =
        day + "|" +
        month + "|" +
        year;


    ctx.fillStyle = "#FFFFFF";

    ctx.font = "6px Arial";

    ctx.textAlign = "right";

    ctx.fillText(
        date,
        119,
        79
    );


    /* =================================================
       TIME
       ================================================= */

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

    ctx.fillText(
        hours + ":" +
        minutes + " " +
        ampm,
        119,
        86
    );

}


/* ==================================================
   START
   ================================================== */

draw();

setInterval(
    draw,
    1000
);

</script>

</body>
</html>
