<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Work Time Tracker</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f4f4;
            color: #333;
            text-align: center;
            margin: 0;
            padding: 20px;
        }

        h1 {
            margin-bottom: 20px;
        }

        #team {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
        }

        .member {
            background-color: #fff;
            border: 1px solid #ddd;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            margin: 10px;
            padding: 20px;
            width: 200px;
        }

        .member h2 {
            margin-top: 0;
        }

        button {
            background-color: #007bff;
            border: none;
            border-radius: 5px;
            color: #fff;
            cursor: pointer;
            margin: 5px;
            padding: 10px 15px;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #0056b3;
        }

        #save-btn {
            background-color: #28a745;
            margin-top: 20px;
        }

        #save-btn:hover {
            background-color: #218838;
        }
    </style>
</head>
<body>
    <h1>Work Time Tracker</h1>
    <div id="team">
        <div class="member" id="nirav">
            <h2>Nirav</h2>
            <p id="time-nirav">00:00:00</p>
            <button onclick="startTimer('nirav')">Start</button>
            <button onclick="stopTimer('nirav')">Stop</button>
            <button onclick="resumeTimer('nirav')">Resume</button>
        </div>
        <div class="member" id="hrutvik">
            <h2>Hrutvik</h2>
            <p id="time-hrutvik">00:00:00</p>
            <button onclick="startTimer('hrutvik')">Start</button>
            <button onclick="stopTimer('hrutvik')">Stop</button>
            <button onclick="resumeTimer('hrutvik')">Resume</button>
        </div>
        <div class="member" id="smit">
            <h2>Smit</h2>
            <p id="time-smit">00:00:00</p>
            <button onclick="startTimer('smit')">Start</button>
            <button onclick="stopTimer('smit')">Stop</button>
            <button onclick="resumeTimer('smit')">Resume</button>
        </div>
        <div class="member" id="pruthvi">
            <h2>Pruthvi</h2>
            <p id="time-pruthvi">00:00:00</p>
            <button onclick="startTimer('pruthvi')">Start</button>
            <button onclick="stopTimer('pruthvi')">Stop</button>
            <button onclick="resumeTimer('pruthvi')">Resume</button>
        </div>
        <div class="member" id="fifth">
            <h2>Fifth</h2>
            <p id="time-fifth">00:00:00</p>
            <button onclick="startTimer('fifth')">Start</button>
            <button onclick="stopTimer('fifth')">Stop</button>
            <button onclick="resumeTimer('fifth')">Resume</button>
        </div>
    </div>
    <button id="save-btn" onclick="saveTimes()">Save Times</button>
    <script>
        const timers = {
            nirav: { startTime: 0, elapsedTime: 0, intervalId: null },
            hrutvik: { startTime: 0, elapsedTime: 0, intervalId: null },
            smit: { startTime: 0, elapsedTime: 0, intervalId: null },
            pruthvi: { startTime: 0, elapsedTime: 0, intervalId: null },
            fifth: { startTime: 0, elapsedTime: 0, intervalId: null },
        };

        function startTimer(member) {
            if (timers[member].intervalId) return;

            timers[member].startTime = Date.now() - timers[member].elapsedTime;
            timers[member].intervalId = setInterval(() => {
                timers[member].elapsedTime = Date.now() - timers[member].startTime;
                document.getElementById(`time-${member}`).innerText = formatTime(timers[member].elapsedTime);
            }, 1000);
        }

        function stopTimer(member) {
            clearInterval(timers[member].intervalId);
            timers[member].intervalId = null;
        }

        function resumeTimer(member) {
            startTimer(member);
        }

        function formatTime(ms) {
            const totalSeconds = Math.floor(ms / 1000);
            const hours = Math.floor(totalSeconds / 3600);
            const minutes = Math.floor((totalSeconds % 3600) / 60);
            const seconds = totalSeconds % 60;
            return `${String(hours).padStart(2, '0')}:${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
        }

        function saveTimes() {
            let result = '';
            for (const member in timers) {
                result += `${member}: ${formatTime(timers[member].elapsedTime)}\n`;
            }
            download('work_times.txt', result);
        }

        function download(filename, text) {
            const element = document.createElement('a');
            element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(text));
            element.setAttribute('download', filename);

            element.style.display = 'none';
            document.body.appendChild(element);

            element.click();

            document.body.removeChild(element);
        }
    </script>
</body>
</html>
