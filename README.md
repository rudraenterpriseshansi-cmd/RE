<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rudra Enterprises - AQI Display</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

html,body{
    width:100%;
    height:100%;
    overflow:hidden;
    background:#000;
    font-family:Arial, Helvetica, sans-serif;
}

.display{
    width:100vw;
    height:100vh;
    background:#000;
    color:#fff;
    display:flex;
    flex-direction:column;
    justify-content:center;
    padding:5px;
}

/* HEADER */
.header{
    height:20%;
    display:flex;
    align-items:center;
    justify-content:center;
    border-bottom:2px solid #333;
}

.company{
    color:#00ff00;
    font-size:clamp(22px,5vw,60px);
    font-weight:bold;
    letter-spacing:2px;
}

/* AQI */
.aqi-section{
    height:38%;
    display:flex;
    align-items:center;
    justify-content:center;
    gap:25px;
}

.aqi-label{
    color:#fff;
    font-size:clamp(25px,7vw,75px);
    font-weight:bold;
}

.aqi-value{
    color:#00ff00;
    font-size:clamp(50px,14vw,150px);
    font-weight:bold;
    line-height:1;
}

/* PM */
.pm-section{
    height:25%;
    display:flex;
    justify-content:space-around;
    align-items:center;
    border-top:2px solid #333;
}

.pm-box{
    text-align:center;
    width:48%;
}

.pm-title{
    font-size:clamp(20px,5vw,55px);
    font-weight:bold;
}

.pm-value{
    font-size:clamp(30px,8vw,85px);
    font-weight:bold;
}

.pm25 .pm-title,
.pm25 .pm-value{
    color:#00ffff;
}

.pm10 .pm-title,
.pm10 .pm-value{
    color:#ffff00;
}

/* DATE TIME */
.footer{
    height:17%;
    display:flex;
    align-items:center;
    justify-content:center;
    flex-direction:column;
}

.date{
    color:#fff;
    font-size:clamp(15px,3vw,35px);
}

.status{
    color:#00ff00;
    font-size:clamp(12px,2.5vw,28px);
    margin-top:5px;
}

/* ERROR */
.error{
    color:red;
}
</style>
</head>

<body>

<div class="display">

    <div class="header">
        <div class="company">RUDRA ENTERPRISES</div>
    </div>

    <div class="aqi-section">
        <div class="aqi-label">AQI</div>
        <div id="aqi" class="aqi-value">--</div>
    </div>

    <div class="pm-section">

        <div class="pm-box pm25">
            <div class="pm-title">PM2.5</div>
            <div id="pm25" class="pm-value">--</div>
        </div>

        <div class="pm-box pm10">
            <div class="pm-title">PM10</div>
            <div id="pm10" class="pm-value">--</div>
        </div>

    </div>

    <div class="footer">
        <div id="date" class="date">--/--/----</div>
        <div id="status" class="status">Connecting...</div>
    </div>

</div>

<script>

/* ==============================
   SAMASTH API
   ============================== */

const DEVICE_ID = "AQI238";

const API_URL =
    "https://integration.samasth.io/api/AQI/display?device="
    + DEVICE_ID +
    "&showAQI=true";


/* ==============================
   GET DATA
   ============================== */

async function getAQIData(){

    try{

        const response = await fetch(API_URL, {
            method: "GET",
            cache: "no-store"
        });

        if(!response.ok){
            throw new Error("API Error " + response.status);
        }

        const data = await response.json();

        console.log("Samasth API Response:", data);

        updateDisplay(data);

    }
    catch(error){

        console.error(error);

        document.getElementById("status").innerHTML =
            "API CONNECTION ERROR";

        document.getElementById("status").className =
            "status error";
    }

}


/* ==============================
   UPDATE DISPLAY
   ============================== */

function updateDisplay(data){

    /*
       These fields may need adjustment
       depending on the exact JSON response
       returned by Samasth.
    */

    let aqi =
        data.AQI ??
        data.aqi ??
        data.Aqi ??
        "--";

    let pm25 =
        data.PM2_5 ??
        data.PM25 ??
        data.pm25 ??
        data["PM2.5"] ??
        "--";

    let pm10 =
        data.PM10 ??
        data.pm10 ??
        "--";


    document.getElementById("aqi").innerHTML = aqi;
    document.getElementById("pm25").innerHTML = pm25;
    document.getElementById("pm10").innerHTML = pm10;

    document.getElementById("status").innerHTML =
        "LIVE DATA";

    updateDateTime();

}


/* ==============================
   DATE / TIME
   ============================== */

function updateDateTime(){

    const now = new Date();

    const day =
        String(now.getDate()).padStart(2,"0");

    const month =
        String(now.getMonth()+1).padStart(2,"0");

    const year =
        now.getFullYear();

    const hours =
        String(now.getHours()).padStart(2,"0");

    const minutes =
        String(now.getMinutes()).padStart(2,"0");

    const seconds =
        String(now.getSeconds()).padStart(2,"0");

    document.getElementById("date").innerHTML =
        day + "/" +
        month + "/" +
        year +
        "  " +
        hours + ":" +
        minutes + ":" +
        seconds;
}


/* ==============================
   AUTO REFRESH
   ============================== */

getAQIData();

/* Refresh API every 10 seconds */
setInterval(getAQIData,10000);

/* Clock */
setInterval(updateDateTime,1000);

updateDateTime();

</script>

</body>
</html>
