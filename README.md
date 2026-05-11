 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Universal Speed Limit | The Constancy of Light</title>
    <style>
        :root {
            --bg-color: #0b0e14;
            --accent-color: #00d4ff;
            --text-color: #e0e0e0;
            --section-bg: #161b22;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.6;
            margin: 0;
            padding: 0;
        }

        header {
            background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)), url('https://images.unsplash.com/photo-1464802686167-b939a6910659?auto=format&fit=crop&w=1350&q=80');
            background-size: cover;
            height: 60vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            border-bottom: 3px solid var(--accent-color);
        }

        header h1 {
            font-size: 3.5rem;
            margin: 0;
            color: var(--accent-color);
            text-transform: uppercase;
            letter-spacing: 5px;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            padding: 40px 20px;
        }

        section {
            background-color: var(--section-bg);
            padding: 30px;
            margin-bottom: 40px;
            border-radius: 8px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.5);
        }

        h2 {
            color: var(--accent-color);
            border-left: 5px solid var(--accent-color);
            padding-left: 15px;
        }

        .highlight {
            background-color: rgba(0, 212, 255, 0.1);
            padding: 20px;
            border-radius: 5px;
            font-style: italic;
            border-left: 3px solid var(--accent-color);
        }

        .diagram-placeholder {
            background: #21262d;
            border: 2px dashed #444;
            height: 300px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 20px 0;
            color: #888;
        }

        footer {
            text-align: center;
            padding: 20px;
            font-size: 0.9rem;
            color: #666;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }

        th, td {
            text-align: left;
            padding: 12px;
            border-bottom: 1px solid #30363d;
        }

        th { color: var(--accent-color); }
    </style>
</head>
<body>

<header>
    <h1>299,792,458 m/s</h1>
    <p>Exploring the Unbreakable Constancy of Light</p>
</header>

<div class="container">

    <section id="introduction">
        <h2>The Core Postulate</h2>
        <p>In classical physics, speeds are additive. If you throw a ball at 10 km/h from a train moving at 50 km/h, the ball moves at 60 km/h relative to the ground. <strong>Light does not follow this rule.</strong></p>
        <div class="highlight">
            Einstein's Second Postulate: The speed of light in a vacuum is the same for all observers, regardless of the motion of the light source or the observer.
        </div>
    </section>

    <section id="history">
        <h2>The Failed Search for Ether</h2>
        <p>Before 1905, scientists thought light traveled through a substance called "ether." In 1887, Albert Michelson and Edward Morley attempted to measure the "ether wind" as the Earth moved through space.</p>
        
        <!--  -->
       

        <p>The experiment yielded a "null result." Light traveled at the same speed in every direction, proving the ether did not exist and light required no medium.</p>
    </section>

    <section id="consequences">
        <h2>Consequences: Time and Space</h2>
        <p>If speed (c) is constant, then the variables of distance and time must be flexible. This gives us <strong>Special Relativity</strong>.</p>
        
        <!--  -->
       <section id="animation-container" style="text-align: center;">
    <h2>The Light Clock Experiment</h2>
    <p>Observe how light travels a longer, diagonal path when the clock is in motion. Because the speed of light cannot change, the clock must "tick" more slowly to cover that extra distance.</p>
    
    <canvas id="lightClockCanvas" width="800" height="300" style="background: #000; border: 1px solid #00d4ff; width: 100%; max-width: 800px;"></canvas>
    
    <div style="margin-top: 15px;">
        <button onclick="toggleAnimation()" id="startBtn" style="padding: 10px 20px; background: #00d4ff; border: none; cursor: pointer; font-weight: bold;">Pause/Resume</button>
        <span style="margin-left: 20px;">Velocity (v): <input type="range" id="speedRange" min="0" max="0.9" step="0.01" value="0.5"> <span id="speedVal">0.5</span>c</span>
    </div>

    <script>
        const canvas = document.getElementById('lightClockCanvas');
        const ctx = canvas.getContext('2d');
        const speedRange = document.getElementById('speedRange');
        const speedVal = document.getElementById('speedVal');
        
        let isRunning = true;
        let time = 0;
        const L = 80; // Distance between mirrors
        const c = 3;  // Constant speed of light
        
        function toggleAnimation() {
            isRunning = !isRunning;
        }

        function draw() {
            if (isRunning) {
                time += 0.5;
            }

            const v = parseFloat(speedRange.value);
            speedVal.innerText = v;

            // Clear Canvas
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Labels
            ctx.fillStyle = "#00d4ff";
            ctx.font = "16px Arial";
            ctx.fillText("Stationary Observer (Frame A)", 50, 40);
            ctx.fillText("Moving Observer (Frame B)", 450, 40);

            // Draw Stationary Clock
            const x1 = 150;
            const y_top = 100;
            const y_bot = 100 + (2 * L);
            
            ctx.strokeStyle = "#444";
            ctx.strokeRect(x1-30, y_top-5, 60, 5); // Top mirror
            ctx.strokeRect(x1-30, y_bot, 60, 5);   // Bottom mirror

            // Stationary Photon Logic
            let photonY = y_bot - (Math.abs((time * c) % (2 * L) - L));
            if (((time * c) % (4 * L)) > 2 * L) { // Moving up/down logic
                photonY = y_top + (Math.abs((time * c) % (2 * L) - L));
            }
            
            // Draw Photon A
            ctx.beginPath();
            ctx.arc(x1, photonY, 5, 0, Math.PI * 2);
            ctx.fillStyle = "yellow";
            ctx.shadowBlur = 15;
            ctx.shadowColor = "yellow";
            ctx.fill();
            ctx.shadowBlur = 0;

            // Draw Moving Clock
            const x2_base = 500;
            const horizontalShift = (time * v * 2) % 250; 
            const x2 = x2_base + horizontalShift;

            ctx.strokeStyle = "#444";
            ctx.strokeRect(x2-30, y_top-5, 60, 5); 
            ctx.strokeRect(x2-30, y_bot, 60, 5);

            // Moving Photon Path (The Zig-Zag)
            // In the moving frame, light still moves at c, but covers a diagonal
            const period = (2 * L) / Math.sqrt(c*c - v*v);
            let movingPhotonY;
            const phase = (time) % (2 * period);
            
            if (phase < period) {
                movingPhotonY = y_bot - (phase / period) * (2 * L);
            } else {
                movingPhotonY = y_top + ((phase - period) / period) * (2 * L);
            }

            // Draw Photon B
            ctx.beginPath();
            ctx.arc(x2, movingPhotonY, 5, 0, Math.PI * 2);
            ctx.fillStyle = "yellow";
            ctx.shadowBlur = 15;
            ctx.shadowColor = "yellow";
            ctx.fill();
            ctx.shadowBlur = 0;

            requestAnimationFrame(draw);
        }

        draw();
    </script>
</section>

        <ul>
            <li><strong>Time Dilation:</strong> Moving clocks run slower.</li>
            <li><strong>Length Contraction:</strong> Moving objects appear shorter in the direction of motion.</li>
            <li><strong>Relativity of Simultaneity:</strong> Two events that appear simultaneous to one observer may not be simultaneous to another.</li>
        </ul>
    </section>

    <section id="limits">
        <h2>The Universal Speed Limit</h2>
        <p>Why can't we go faster than c? As an object approaches the speed of light, its kinetic energy increases. However, according to E=mc^2, that energy adds to the object's relativistic mass. The faster you go, the "heavier" (more resistant to acceleration) you become.</p>
        
        <table>
            <thead>
                <tr>
                    <th>Velocity</th>
                    <th>Time Dilation Factor (Gamma)</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>0.1c</td>
                    <td>1.005</td>
                </tr>
                <tr>
                    <td>0.9c</td>
                    <td>2.294</td>
                </tr>
                <tr>
                    <td>0.999c</td>
                    <td>22.366</td>
                </tr>
            </tbody>
        </table>
    </section>

</div>

<footer>
    <p>Educational Resource on Special Relativity &copy; 2026</p>
</footer>

</body>
</html>
