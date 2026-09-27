<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Prathana's 30-Day Routine</title>

<style>
:root {
    --bg: #f4f6fb;
    --card: #ffffff;
    --text: #172033;
    --muted: #697386;
    --accent: #5b5bd6;
    --accent-light: #ececff;
    --line: #e7e9f0;
    --done: #e9f8ef;
}

* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
    background: var(--bg);
    color: var(--text);
}

/* HEADER */

header {
    background: linear-gradient(135deg, #24244d, #5b5bd6);
    color: white;
    padding: 30px 18px 35px;
    position: sticky;
    top: 0;
    z-index: 10;
    box-shadow: 0 8px 25px rgba(40,40,100,.18);
}

.container {
    max-width: 1050px;
    margin: auto;
}

h1 {
    margin: 0;
    font-size: clamp(26px, 5vw, 40px);
}

.subtitle {
    margin-top: 7px;
    opacity: .8;
    font-size: 14px;
}

/* STATS */

.stats {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
    margin-top: 22px;
}

.stat {
    background: rgba(255,255,255,.13);
    border: 1px solid rgba(255,255,255,.18);
    border-radius: 14px;
    padding: 12px;
}

.stat b {
    display: block;
    font-size: 23px;
}

.stat span {
    font-size: 11px;
    opacity: .8;
}

.progress {
    height: 8px;
    background: rgba(255,255,255,.2);
    border-radius: 20px;
    overflow: hidden;
    margin-top: 15px;
}

.progress-bar {
    height: 100%;
    width: 0%;
    background: white;
    transition: .3s;
}

/* BUTTONS */

.controls {
    max-width: 1050px;
    margin: 18px auto;
    padding: 0 18px;

    display: flex;
    gap: 10px;
    flex-wrap: wrap;
}

button {
    border: none;
    border-radius: 11px;
    padding: 10px 15px;
    background: white;
    color: var(--text);
    font-weight: bold;
    cursor: pointer;

    box-shadow: 0 3px 12px rgba(20,30,60,.07);
}

button:hover {
    transform: translateY(-1px);
}

.primary {
    background: var(--accent);
    color: white;
}

/* DAYS */

#days {
    max-width: 1050px;
    margin: auto;
    padding: 0 18px 40px;
}

.day {
    background: var(--card);
    border: 1px solid var(--line);
    border-radius: 18px;
    margin: 14px 0;
    overflow: hidden;

    box-shadow: 0 10px 30px rgba(26,35,60,.08);
}

.day-header {
    padding: 17px 18px;

    display: flex;
    justify-content: space-between;
    align-items: center;

    border-bottom: 1px solid var(--line);
}

.day-title {
    font-size: 19px;
    font-weight: 800;
}

.date {
    font-size: 12px;
    color: var(--muted);
    margin-top: 3px;
}

.day-progress {
    color: var(--accent);
    font-size: 12px;
    font-weight: bold;
}

/* TASK */

.task {
    display: grid;
    grid-template-columns: 30px 105px 1fr;

    align-items: center;

    gap: 8px;

    padding: 13px 18px;

    border-bottom: 1px solid #f0f1f5;

    transition: .15s;
}

.task:last-child {
    border-bottom: none;
}

.task.done {
    background: var(--done);
}

.task input {
    width: 20px;
    height: 20px;

    accent-color: var(--accent);

    cursor: pointer;
}

.time {
    color: var(--muted);
    font-size: 12px;
    font-weight: bold;
}

.task-name {
    font-size: 14px;
    font-weight: 600;
}

.task.done .task-name {
    text-decoration: line-through;
    color: #72807a;
}

/* MOBILE */

@media(max-width:600px) {

    .stats {
        grid-template-columns: repeat(3, 1fr);
    }

    .task {
        grid-template-columns: 30px 85px 1fr;
        padding: 12px 13px;
    }

    .time {
        font-size: 11px;
    }

    .task-name {
        font-size: 13px;
    }

    .day-header {
        padding: 15px 14px;
    }
}
</style>
</head>


<body>

<header>

<div class="container">

<h1>Prathana's 30-Day Routine</h1>

<div class="subtitle">
27 September – 26 October 2026 · Complete your daily checklist
</div>


<div class="stats">

<div class="stat">
<b id="completed">0</b>
<span>TASKS DONE</span>
</div>

<div class="stat">
<b id="total">0</b>
<span>TOTAL TASKS</span>
</div>

<div class="stat">
<b id="percentage">0%</b>
<span>PROGRESS</span>
</div>

</div>


<div class="progress">
<div class="progress-bar" id="progressBar"></div>
</div>

</div>

</header>


<div class="controls">

<button class="primary" onclick="goToday()">
📅 Today
</button>

<button onclick="completeToday()">
✅ Finish Today's Routine
</button>

<button onclick="resetAll()">
🔄 Reset All
</button>

</div>


<main id="days"></main>


<script>

/* =========================
   ROUTINE
========================= */

const schedules = {

Monday: [

["06:15","Wake up"],
["06:30–15:30","School"],
["15:30–17:00","Lunch and nap"],
["17:15–19:00","Study Session 1"],
["19:00–19:15","Tuition revision"],
["19:30–22:15","Tuitions"],
["22:15–23:00","Dinner"],
["23:00–00:00","Study Session 2"],
["00:00–00:30","Socialising"],
["00:30","Sleep"]

],

Tuesday: [

["06:15","Wake up"],
["06:30–15:30","School"],
["15:30–17:00","Lunch and nap"],
["17:15–18:45","Study Session 1"],
["19:00–20:45","English tuition"],
["21:00–21:30","Dinner"],
["21:45–23:45","Study Session 2"],
["23:45–00:30","Homework"],
["00:30–01:00","Socialising"]

],

Wednesday: [

["06:30","Wake up"],
["06:30–15:30","School"],
["15:30–17:00","Lunch and nap"],
["17:15–19:00","Study Session 1"],
["19:00–19:15","Break"],
["19:30–20:15","Study Session 2"],
["20:30–22:15","Maths tuition"],
["22:15–23:00","Dinner"],
["23:15–00:15","Study Session 3"],
["00:15–01:00","Socialising"],
["01:00","Sleep"]

],

Thursday: [

["06:15","Wake up"],
["06:30–15:30","School"],
["15:30–17:00","Lunch and nap"],
["17:00–18:45","Study Session 1"],
["19:00–21:30","Tuition"],
["21:30–22:15","Rest and all"],
["22:30–00:30","Study Session 2"],
["00:30–01:00","Socialising"],
["01:00","Sleep"]

],

Friday: [

["06:30","Wake up"],
["06:30–15:30","School"],
["15:30–17:00","Lunch and nap"],
["17:15–19:00","Study Session 1"],
["19:00–19:15","Break"],
["19:30–20:15","Study Session 2"],
["20:30–22:15","Maths tuition"],
["22:15–23:00","Dinner"],
["23:15–00:15","Study Session 3"],
["00:15–01:00","Socialising"],
["01:00","Sleep"]

],

Saturday: [

["07:45","Wake up"],
["07:45–08:30","Freshening up"],
["08:30–09:00","Physical fitness"],
["09:00–12:00","Study Session (30 min breakfast break included)"],
["12:00–13:30","Girlyapa"],
["13:30–14:45","Study Session"],
["14:45–15:30","Lunch"],
["15:30–17:00","Sleep"],
["17:15–18:45","Study Session 3"],
["19:00–21:00","English tuition"],
["21:15–22:00","Dinner"],
["22:15–00:00","Socialising"],
["00:00","Sleep"]

],

Sunday: [

["07:45","Wake up"],
["07:45–08:30","Fresh"],
["08:30–09:00","Physical fitness"],
["09:00–12:00","Study Session 1"],
["12:00–14:30","Physics tuition"],
["14:30–15:30","Lunch"],
["15:30–17:00","Sleep"],
["17:15–19:00","Study Session 2"],
["19:00–19:15","Break"],
["19:30–22:30","Study Session 3"],
["22:30–23:15","Dinner"],
["23:15–00:00","Socialising"],
["00:00","Sleep"]

]

};


/* =========================
   CREATE 30 DAYS
========================= */

const startDate = new Date(2026,8,27);

const days = [];

for(let i=0;i<30;i++){

    const d = new Date(startDate);

    d.setDate(startDate.getDate()+i);

    const weekday =
        d.toLocaleDateString("en-US",{weekday:"long"});

    days.push({

        date:d,

        weekday:weekday,

        tasks:schedules[weekday]

    });

}


/* =========================
   LOCAL STORAGE
========================= */

const STORAGE_KEY =
"prathana_30_day_routine";

let completed =
JSON.parse(localStorage.getItem(STORAGE_KEY) || "{}");


/* =========================
   SAVE
========================= */

function save(){

    localStorage.setItem(
        STORAGE_KEY,
        JSON.stringify(completed)
    );

}


/* =========================
   RENDER
========================= */

function render(){

    const container =
        document.getElementById("days");

    container.innerHTML="";


    days.forEach((day,dayIndex)=>{

        const section =
            document.createElement("section");

        section.className="day";

        section.id=`day-${dayIndex}`;


        const formattedDate =
            day.date.toLocaleDateString(
                "en-IN",
                {
                    day:"numeric",
                    month:"short",
                    year:"numeric"
                }
            );


        let completedToday=0;


        day.tasks.forEach((task,index)=>{

            const key =
                `${dayIndex}-${index}`;

            if(completed[key])
                completedToday++;

        });


        const percentage =
            Math.round(
                completedToday/day.tasks.length*100
            );


        section.innerHTML=`

        <div class="day-header">

            <div>

                <div class="day-title">
                    ${day.weekday}
                </div>

                <div class="date">
                    ${formattedDate}
                </div>

            </div>

            <div class="day-progress">
                ${completedToday}/${day.tasks.length}
                · ${percentage}%
            </div>

        </div>

        `;


        day.tasks.forEach((task,index)=>{

            const key =
                `${dayIndex}-${index}`;

            const isDone =
                completed[key] === true;


            const label =
                document.createElement("label");

            label.className =
                "task" +
                (isDone ? " done":"");


            label.innerHTML=`

            <input
                type="checkbox"
                ${isDone ? "checked":""}
            >

            <span class="time">
                ${task[0]}
            </span>

            <span class="task-name">
                ${task[1]}
            </span>

            `;


            const checkbox =
                label.querySelector("input");


            checkbox.addEventListener(
                "change",
                function(){

                    if(this.checked){

                        completed[key]=true;

                    }else{

                        delete completed[key];

                    }

                    save();

                    render();

                }
            );


            section.appendChild(label);

        });


        container.appendChild(section);

    });


    updateStats();

}


/* =========================
   STATS
========================= */

function updateStats(){

    let total=0;
    let done=0;


    days.forEach((day,dayIndex)=>{

        day.tasks.forEach((task,index)=>{

            total++;

            if(
                completed[
                    `${dayIndex}-${index}`
                ]
            ){

                done++;

            }

        });

    });


    const percentage =
        total
        ? Math.round(done/total*100)
        : 0;


    document.getElementById(
        "completed"
    ).textContent=done;


    document.getElementById(
        "total"
    ).textContent=total;


    document.getElementById(
        "percentage"
    ).textContent=
        percentage+"%";


    document.getElementById(
        "progressBar"
    ).style.width=
        percentage+"%";

}


/* =========================
   GO TO TODAY
========================= */

function goToday(){

    const now =
        new Date();

    const index =
        days.findIndex(
            day =>
            day.date.toDateString()
            === now.toDateString()
        );


    if(index !== -1){

        document
            .getElementById(`day-${index}`)
            .scrollIntoView({
                behavior:"smooth",
                block:"start"
            });

    }else{

        alert(
            "Today is outside this 30-day tracker."
        );

    }

}


/* =========================
   COMPLETE TODAY
========================= */

function completeToday(){

    const now =
        new Date();

    const index =
        days.findIndex(
            day =>
            day.date.toDateString()
            === now.toDateString()
        );


    if(index === -1){

        alert(
            "Today is outside this 30-day tracker."
        );

        return;

    }


    days[index].tasks.forEach(
        (task,taskIndex)=>{

            completed[
                `${index}-${taskIndex}`
            ]=true;

        }
    );


    save();

    render();

    goToday();

}


/* =========================
   RESET
========================= */

function resetAll(){

    const confirmReset =
        confirm(
            "Reset every checkbox for all 30 days?"
        );


    if(confirmReset){

        completed={};

        save();

        render();

        window.scrollTo({
            top:0,
            behavior:"smooth"
        });

    }

}


/* =========================
   START
========================= */

render();

</script>

</body>
</html>
