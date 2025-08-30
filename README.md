<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Modular Shell Alignment Explorer</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
        }
        
        h1 {
            text-align: center;
            color: #4a5568;
            margin-bottom: 10px;
            font-size: 2.2em;
        }
        
        .subtitle {
            text-align: center;
            color: #718096;
            margin-bottom: 30px;
            font-style: italic;
        }
        
        .controls {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
            padding: 20px;
            background: rgba(99, 102, 241, 0.1);
            border-radius: 10px;
        }
        
        .control-group {
            display: flex;
            flex-direction: column;
        }
        
        label {
            font-weight: 600;
            margin-bottom: 5px;
            color: #4a5568;
        }
        
        select, input {
            padding: 10px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            font-size: 14px;
            transition: border-color 0.3s;
        }
        
        select:focus, input:focus {
            outline: none;
            border-color: #6366f1;
        }
        
        .button {
            background: linear-gradient(135deg, #6366f1, #8b5cf6);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: transform 0.2s, box-shadow 0.2s;
        }
        
        .button:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(99, 102, 241, 0.3);
        }
        
        .results {
            display: block;
            margin-top: 30px;
        }
        
        .results-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }
        
        .panel {
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .panel h3 {
            color: #4a5568;
            border-bottom: 2px solid #e2e8f0;
            padding-bottom: 10px;
            margin-bottom: 15px;
        }
        
        .examples {
            font-family: 'Courier New', monospace;
            background: #f7fafc;
            padding: 15px;
            border-radius: 8px;
            font-size: 13px;
            line-height: 1.4;
        }
        
        .canvas-container {
            text-align: center;
            margin: 20px 0;
        }
        
        canvas {
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            background: white;
        }
        
        .math-notation {
            background: #f0f4f8;
            padding: 15px;
            border-radius: 8px;
            border-left: 4px solid #6366f1;
            margin: 15px 0;
            font-family: 'Times New Roman', serif;
        }
        
        .theorem-box {
            background: linear-gradient(135deg, #f0fff4, #e6fffa);
            border: 2px solid #38b2ac;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
        }
        
        .definition-box {
            background: linear-gradient(135deg, #fef5e7, #fed7aa);
            border: 2px solid #f59e0b;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
        }
        
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }
        
        .stat {
            text-align: center;
            padding: 15px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border-radius: 8px;
        }
        
        .stat-value {
            font-size: 1.5em;
            font-weight: bold;
        }
        
        .stat-label {
            font-size: 0.9em;
            opacity: 0.9;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Modular Shell Alignment Explorer</h1>
        <p class="subtitle">Interactive demonstration of the Getachew Unified Shell Alignment Theorem</p>
        
        <div class="definition-box">
            <h3>Definition: Modular Shell</h3>
            <p>For a modulus M, polynomial <strong>norm form</strong> f(x,y), and discriminant D, the <strong>modular shell</strong> is:</p>
            <div class="math-notation">
                𝒮(f,D;M) = {(x,y) ∈ ℤ² : f(x,y) ≡ D (mod M)}
            </div>
        </div>
        
        <div class="theorem-box">
            <h3>Getachew Unified Shell Alignment Theorem (Empirical Form)</h3>
            <p>For M_n = 30·2^n, there exist discriminants D such that modular shells for various norm forms are nonempty and persist under lifting M_n → M_{n+1}.</p>
        </div>
        
        <div class="controls">
            <div class="control-group">
                <label for="polynomialSelect">Norm Form f(x,y):</label>
                <select id="polynomialSelect">
                    <option value="gaussian">Gaussian norm: x² + y²</option>
                    <option value="eisenstein">Eisenstein norm: x² - xy + y²</option>
                    <option value="scaled">Scaled norm: x² + 4y²</option>
                    <option value="cubic">Cubic norm: x³ + y³</option>
                    <option value="hybrid">Hybrid norm: x² + y³</option>
                </select>
            </div>
            
            <div class="control-group">
                <label for="discriminantSelect">Discriminant D:</label>
                <select id="discriminantSelect">
                    <option value="-19">-19</option>
                    <option value="-43">-43</option>
                    <option value="-11">-11</option>
                    <option value="-67">-67</option>
                    <option value="-163">-163</option>
                    <option value="-4">-4</option>
                    <option value="-8">-8</option>
                </select>
            </div>
            
            <div class="control-group">
                <label for="scaleSelect">Scale M_n = 30·2^n:</label>
                <select id="scaleSelect">
                    <option value="30">M₀ = 30</option>
                    <option value="1920" selected>M₆ = 1920</option>
                    <option value="30720">M₁₀ = 30720</option>
                </select>
            </div>
            
            <div class="control-group">
                <label for="rangeInput">Search Range:</label>
                <input type="number" id="rangeInput" value="50" min="10" max="200">
            </div>
            
            <div class="control-group">
                <button class="button" onclick="findShellPoints()">Find Shell Points</button>
            </div>
            
            <div class="control-group">
                <button class="button" onclick="visualizeShell()">Visualize Shell</button>
            </div>
        </div>
        
        <div class="stats">
            <div class="stat">
                <div class="stat-value" id="pointCount">0</div>
                <div class="stat-label">Points Found</div>
            </div>
            <div class="stat">
                <div class="stat-value" id="density">0.0%</div>
                <div class="stat-label">Shell Density</div>
            </div>
            <div class="stat">
                <div class="stat-value" id="currentM">1920</div>
                <div class="stat-label">Current M</div>
            </div>
        </div>
        
        <div class="results">
            <div class="panel">
                <h3>All Shell Points Found</h3>
                <div id="pointsDisplay" class="examples" style="max-height: 300px; overflow-y: auto; font-size: 12px; line-height: 1.6;">
                    Select norm form and click "Find Shell Points" to see all points...
                </div>
            </div>
            
            <div class="results-grid">
                <div class="panel">
                    <h3>Shell Visualization</h3>
                    <div class="canvas-container">
                        <canvas id="shellCanvas" width="400" height="400"></canvas>
                    </div>
                    <p style="text-align: center; font-size: 0.9em; color: #718096;">
                        Blue dots: shell points. Click "Visualize Shell" to plot.
                    </p>
                </div>
                
                <div class="panel">
                    <h3>Point Summary</h3>
                    <div id="summaryDisplay" class="examples">
                        Point summary will appear here after finding shell points...
                    </div>
                </div>
            </div>
        </div>
        
        <div class="panel" style="margin-top: 30px;">
            <h3>Worked Examples from the Paper</h3>
            <div id="paperExamples" class="examples">
                <strong>Gaussian norm shell (x² + y²) with D = -19:</strong><br>
                mod 30: f(-50,-49) = 4901 ≡ 11 ≡ -19 (mod 30)<br>
                mod 1920: f(-35,-26) = 1901 ≡ -19 (mod 1920)<br>
                mod 30720: f(-365,-286) = 215021 ≡ -19 (mod 30720)<br><br>
                
                <strong>Eisenstein norm shell (x² - xy + y²) with D = -11:</strong><br>
                mod 30: f(-50,-47) = 2359 ≡ 19 ≡ -11 (mod 30)<br>
                mod 1920: f(-195,73) = 57589 ≡ -11 (mod 1920)<br>
                mod 30720: f(-372,265) = 307189 ≡ -11 (mod 30720)
            </div>
        </div>
    </div>

    <script>
        // Polynomial evaluation functions
        const polynomials = {
            gaussian: (x, y) => x*x + y*y,
            eisenstein: (x, y) => x*x - x*y + y*y,
            scaled: (x, y) => x*x + 4*y*y,
            cubic: (x, y) => x*x*x + y*y*y,
            hybrid: (x, y) => x*x + y*y*y
        };
        
        let currentPoints = [];
        
        function modulo(n, m) {
            return ((n % m) + m) % m;
        }
        
        function findShellPoints() {
            const polyType = document.getElementById('polynomialSelect').value;
            const discriminant = parseInt(document.getElementById('discriminantSelect').value);
            const modulus = parseInt(document.getElementById('scaleSelect').value);
            const range = parseInt(document.getElementById('rangeInput').value);
            
            const poly = polynomials[polyType];
            const points = [];
            let totalChecked = 0;
            
            // Search for points in the shell
            for (let x = -range; x <= range; x++) {
                for (let y = -range; y <= range; y++) {
                    totalChecked++;
                    const value = poly(x, y);
                    const residue = modulo(value, modulus);
                    const targetResidue = modulo(discriminant, modulus);
                    
                    if (residue === targetResidue) {
                        points.push({x, y, value, residue});
                    }
                }
            }
            
            currentPoints = points;
            
            // Update statistics
            document.getElementById('pointCount').textContent = points.length;
            document.getElementById('density').textContent = ((points.length / totalChecked) * 100).toFixed(3) + '%';
            document.getElementById('currentM').textContent = modulus;
            
            // Display all points
            displayPoints(points, polyType, discriminant, modulus);
            
            // Display summary
            displaySummary(points, polyType, discriminant, modulus);
        }
        
        function displayPoints(points, polyType, discriminant, modulus) {
            const display = document.getElementById('pointsDisplay');
            
            if (points.length === 0) {
                display.innerHTML = `<em>No points found in the current range for ${polyType} norm with D=${discriminant}, M=${modulus}</em>`;
                return;
            }
            
            let html = `<strong>All ${points.length} points in ${polyType} norm shell:</strong><br>`;
            html += `<strong>D = ${discriminant}, M = ${modulus}</strong><br><br>`;
            
            points.forEach((point, i) => {
                html += `${i+1}. (x,y) = (${point.x},${point.y}) → norm = ${point.value} ≡ ${discriminant} (mod ${modulus})<br>`;
            });
            
            display.innerHTML = html;
        }
        
        function displaySummary(points, polyType, discriminant, modulus) {
            const summaryDisplay = document.getElementById('summaryDisplay');
            
            if (points.length === 0) {
                summaryDisplay.innerHTML = '<em>No points found</em>';
                return;
            }
            
            // Calculate statistics
            const norms = points.map(p => p.value);
            const minNorm = Math.min(...norms);
            const maxNorm = Math.max(...norms);
            const avgNorm = (norms.reduce((a, b) => a + b, 0) / norms.length).toFixed(2);
            
            // Find coordinate ranges
            const xValues = points.map(p => p.x);
            const yValues = points.map(p => p.y);
            const xRange = `[${Math.min(...xValues)}, ${Math.max(...xValues)}]`;
            const yRange = `[${Math.min(...yValues)}, ${Math.max(...yValues)}]`;
            
            let html = `<strong>Summary Statistics:</strong><br><br>`;
            html += `Points found: ${points.length}<br>`;
            html += `X coordinate range: ${xRange}<br>`;
            html += `Y coordinate range: ${yRange}<br><br>`;
            html += `<strong>Norm Values:</strong><br>`;
            html += `Minimum norm: ${minNorm}<br>`;
            html += `Maximum norm: ${maxNorm}<br>`;
            html += `Average norm: ${avgNorm}<br><br>`;
            html += `<strong>First few points:</strong><br>`;
            
            points.slice(0, 5).forEach((point, i) => {
                html += `(${point.x},${point.y}) = ${point.value}<br>`;
            });
            
            if (points.length > 5) {
                html += `... and ${points.length - 5} more`;
            }
            
            summaryDisplay.innerHTML = html;
        }
        
        function visualizeShell() {
            const canvas = document.getElementById('shellCanvas');
            const ctx = canvas.getContext('2d');
            const width = canvas.width;
            const height = canvas.height;
            
            // Clear canvas
            ctx.clearRect(0, 0, width, height);
            ctx.fillStyle = '#f8fafc';
            ctx.fillRect(0, 0, width, height);
            
            if (currentPoints.length === 0) {
                ctx.fillStyle = '#718096';
                ctx.font = '16px Arial';
                ctx.textAlign = 'center';
                ctx.fillText('Click "Find Shell Points" first', width/2, height/2);
                return;
            }
            
            // Find bounds for scaling
            let minX = Math.min(...currentPoints.map(p => p.x));
            let maxX = Math.max(...currentPoints.map(p => p.x));
            let minY = Math.min(...currentPoints.map(p => p.y));
            let maxY = Math.max(...currentPoints.map(p => p.y));
            
            // Add padding
            const padding = Math.max((maxX - minX), (maxY - minY)) * 0.1;
            minX -= padding;
            maxX += padding;
            minY -= padding;
            maxY += padding;
            
            // Draw grid
            ctx.strokeStyle = '#e2e8f0';
            ctx.lineWidth = 0.5;
            
            for (let i = 0; i <= 10; i++) {
                const x = (i / 10) * width;
                const y = (i / 10) * height;
                
                ctx.beginPath();
                ctx.moveTo(x, 0);
                ctx.lineTo(x, height);
                ctx.moveTo(0, y);
                ctx.lineTo(width, y);
                ctx.stroke();
            }
            
            // Draw axes
            const centerX = width * (-minX) / (maxX - minX);
            const centerY = height * (maxY) / (maxY - minY);
            
            if (centerX >= 0 && centerX <= width) {
                ctx.strokeStyle = '#cbd5e0';
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.moveTo(centerX, 0);
                ctx.lineTo(centerX, height);
                ctx.stroke();
            }
            
            if (centerY >= 0 && centerY <= height) {
                ctx.strokeStyle = '#cbd5e0';
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.moveTo(0, centerY);
                ctx.lineTo(width, centerY);
                ctx.stroke();
            }
            
            // Plot points
            ctx.fillStyle = '#3b82f6';
            currentPoints.forEach(point => {
                const x = ((point.x - minX) / (maxX - minX)) * width;
                const y = ((maxY - point.y) / (maxY - minY)) * height;
                
                ctx.beginPath();
                ctx.arc(x, y, 3, 0, 2 * Math.PI);
                ctx.fill();
            });
            
            // Draw title
            ctx.fillStyle = '#4a5568';
            ctx.font = 'bold 14px Arial';
            ctx.textAlign = 'center';
            ctx.fillText(`Shell Pattern: ${currentPoints.length} points`, width/2, 25);
        }
        
        // Update discriminant options based on polynomial selection
        function updateDiscriminantOptions() {
            const polyType = document.getElementById('polynomialSelect').value;
            const discriminantSelect = document.getElementById('discriminantSelect');
            
            // Reset options
            discriminantSelect.innerHTML = '';
            
            let options = [];
            switch(polyType) {
                case 'gaussian':
                    options = ['-19', '-43', '-67', '-163'];
                    break;
                case 'eisenstein':
                    options = ['-11', '-67'];
                    break;
                case 'scaled':
                    options = ['-67', '-163'];
                    break;
                case 'cubic':
                    options = ['-4'];
                    break;
                case 'hybrid':
                    options = ['-8'];
                    break;
            }
            
            options.forEach(value => {
                const option = document.createElement('option');
                option.value = value;
                option.textContent = value;
                discriminantSelect.appendChild(option);
            });
        }
        
        // Event listeners
        document.getElementById('polynomialSelect').addEventListener('change', updateDiscriminantOptions);
        
        // Initialize
        updateDiscriminantOptions();
        
        // Auto-run example on load
        setTimeout(() => {
            findShellPoints();
            visualizeShell();
        }, 500);
        
        // Keyboard shortcuts
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Enter' && e.ctrlKey) {
                findShellPoints();
            }
            if (e.key === 'v' && e.ctrlKey) {
                visualizeShell();
            }
        });
    </script>
</body>
</html>
