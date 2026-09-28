<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AQI LED Display</title>

<style>

/* ================= RESET ================= */

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
    font-family:Arial, Helvetica, sans-serif;
}

/* ================= MAIN DISPLAY ================= */

.container{
    width:100vw;
    height:100vh;
    background:#000;
    color:white;
    display:flex;
    flex-direction:column;
    overflow:hidden;
}

/* ================= HEADER ================= */

.header{
    height:21%;
    width:100%;
    display:flex;
    justify-content:center;
    align-items:center;
    border-bottom:2px solid white;
}

.company{
    color:#yellow;
    font-size:6.2vw;
    font-weight:128;
    letter-spacing:1px;
    white-space:nowrap;
}

/* ================= MAIN AREA ================= */

.main{
    height:61%;
    width:100%;
    display:grid;
    grid-template-columns:34% 34% 32%;
}

/* ================= PM BLOCKS ================= */

.pm-block{
    display:flex;
    flex-direction:column;
    justify-content:flex-start;
    align-items:center;
    padding-top:4.5%;
}

.parameter{
    color:#ffffff;
    font-size:5.2vw;
    font-weight:128;
    line-height:1;
}

.value{
    color:#ff0000;
    font-size:7.5vw;
    font-weight:128;
    line-height:1;
    margin-top:5%;
}

.unit{
    color:#ffffff;
    font-size:3vw;
    margin-top:3%;
}

/* ================= RIGHT SIDE ================= */

.environment{
    display:flex;
    flex-direction:column;
    align-items:flex-start;
    padding-top:5%;
    padding-left:4%;
}

.env-row{
    display:flex;
    align-items:center;
    height:25%;
}

.dot{
    width:1.7vw;
    height:1.7vw;
    border-radius:50%;
    margin-right:1.5vw;
}

.red-dot{
    background:#ff0000;
}

.blue-dot{
    background:#0099ff;
}

.env-value{
    color:#ffffff;
    font-size:3.7vw;
    font-weight:500;
    white-space:nowrap;
}

/* ================= BOTTOM ================= */

.bottom{
    height:18%;
    width:100%;
    border-top:2px solid white;
    display:flex;
    justify-content:flex-end;
    align-items:flex-start;
    padding-right:8%;
    padding-top:1.5%;
}

.datetime{
    display:flex;
    flex-direction:column;
    align-items:center;
    color:#ffffff;
    font-size:2.8vw;
    line-height:1.25;
}

.date{
    white-space:nowrap;
}

.time{
    white-space:nowrap;
}

/* ================= RESPONSIVE ================= */

@media(max-aspect-ratio:1/1){

    .company{
        font-size:7vw;
    }

    .parameter{
        font-size:6vw;
    }

    .value{
        font-size:8vw;
    }

    .unit{
        font-size:3.5vw;
    }

    .env-value{
        font-size:4vw;
    }

    .datetime{
        font-size:3.5vw;
    }
}

</style>
</head>

<body>

<div class="container">

    <!-- ================= HEADER ================= -->

    <div class="header">
        <div class="company" id="clientName">
            RUDRA ENTERPRISES
        </div>
    </div>


    <!-- ================= MAIN DATA ================= -->

    <div class="main">

        <!-- PM2.5 -->

        <div class="pm-block">

            <div class="parameter">
                PM2.5
            </div>

            <div class="value" id="pm25">
                --
            </div>

            <div class="unit">
                µg/m3
            </div>

        </div>


        <!-- PM10 -->

        <div class="pm-block">

            <div class="parameter">
                PM10
            </div>

            <div class="value" id="pm10">
                --
            </div>

            <div class="unit">
                µg/m3
            </div>

        </div>


        <!-- TEMPERATURE / HUMIDITY -->

        <div class="environment">

            <div class="env-row">

                <div class="dot red-dot"></div>

                <div class="env-value">
                    <span id="temp">--</span>°C
                </div>

            </div>


            <div class="env-row">

                <div class="dot blue-dot"></div>

                <div class="env-value">
                    <span id="hum">--</span>%
                </div>

            </div>

        </div>

    </div>


    <!-- ================= DATE / TIME ================= -->

    <div class="bottom">

        <div class="datetime">

            <div class="date" id="date">
                --|---|----
            </div>

            <div class="time" id="time">
                --:-- --
            </div>

        </div>

    </div>

</div>


<script>

/* =====================================================
   GET URL PARAMETERS
   Example:
   ?device=11&client=RUDRA%20ENTERPRISES
   ===================================================== */

const params = new URLSearchParams(window.location.search);

const device =
    params.get("device") || "11";

let name =
    params.get("client") ||
    params.get("name") ||
    "RUDRA ENTERPRISES";

name = decodeURIComponent(name);

document.getElementById("clientName").innerText = name;


/* =====================================================
   DATE & TIME
   Format:
   24|Jan|2026
   12:21 PM
   ===================================================== */

function updateTime(){

    const now = new Date();

    const day =
        String(now.getDate()).padStart(2,"0");

    const month =
        now.toLocaleString("en-US",{
            month:"short"
        });

    const year =
        now.getFullYear();

    let hours =
        now.getHours();

    const minutes =
        String(now.getMinutes()).padStart(2,"0");

    const ampm =
        hours >= 12 ? "PM" : "AM";

    hours =
        hours % 12 || 12;

    document.getElementById("date").innerText =
        `${day}|${month}|${year}`;

    document.getElementById("time").innerText =
        `${hours}:${minutes} ${ampm}`;
}


/* =====================================================
   FETCH API DATA
   ===================================================== */

async function fetchData(){

    try{

        const response = await fetch(
            "https://aqi.rudraenterpriseshansi.workers.dev/?device="
            + encodeURIComponent(device)
        );

        if(!response.ok){
            throw new Error(
                "HTTP ERROR " + response.status
            );
        }

        const data =
            await response.json();

        console.log("API DATA:",data);

        const p =
            data.parameter || {};


        /* ================= PM2.5 ================= */

        document.getElementById("pm25").innerText =
            p.pm25?.value ?? "--";


        /* ================= PM10 ================= */

        document.getElementById("pm10").innerText =
            p.pm10?.value ?? "--";


        /* ================= TEMPERATURE ================= */

        document.getElementById("temp").innerText =
            p.temperature?.value ?? "--";


        /* ================= HUMIDITY ================= */

        document.getElementById("hum").innerText =
            p.humidity?.value ?? "--";


    }

    catch(error){

        console.log(
            "API ERROR:",
            error
        );

    }

}


/* =====================================================
   AUTO UPDATE
   ===================================================== */

setInterval(updateTime,1000);

setInterval(fetchData,20000);


/* INITIAL LOAD */

updateTime();

fetchData();

</script>

</body>
</html>
