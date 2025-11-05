<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Trigonometry Triangle</title>
</head>
<body>
  <div class="container">
    <h1>Trigonometry Calculator</h1>

    <label>Enter Angle (°):</label><br>
    <input type="text" id="angle" placeholder="e.g. 60" readonly><br>

    <label>Enter Adjacent Side (unit):</label><br>
    <input type="text" id="adjacent" placeholder="e.g. 5" readonly><br>

    <button onclick="drawTriangle()">Draw Triangle</button>

    <div class="calc-buttons">
      <button onclick="addValue('7')">7</button>
      <button onclick="addValue('8')">8</button>
      <button onclick="addValue('9')">9</button>
      <button onclick="trigFunction('sin')">sin</button>

      <button onclick="addValue('4')">4</button>
      <button onclick="addValue('5')">5</button>
      <button onclick="addValue('6')">6</button>
      <button onclick="trigFunction('cos')">cos</button>

      <button onclick="addValue('1')">1</button>
      <button onclick="addValue('2')">2</button>
      <button onclick="addValue('3')">3</button>
      <button onclick="trigFunction('tan')">tan</button>

      <button onclick="addValue('0')">0</button>
      <button onclick="addValue('.')">.</button>
      <button onclick="clearInput()">Clear</button>
      <button onclick="resetAll()">Reset</button>
    </div>
   
    <canvas id="triangleCanvas" width="300" height="220"></canvas>
    <div class="results" id="resultsBox">Enter values to compute sides.</div>
  </div>

  <script src="script.js"></script>
</body>
</html>

<style>
body {
  font-family: Arial, sans-serif;
  background: lightblue;
}

.container {
  background: linear-gradient(to bottom,lightpink,white);
  width: 320px;
  margin: 40px auto;
  padding: 20px;
  border-radius: 15px;
  text-align: center;
  box-shadow: 0 0 10px rgba(0,0,0,0.2);
}

h1 {
  color: #0000ff;
  text-shadow: 1px 1px 3px rgba(0,0,0,0.2);
}

label {
  font-weight: bold;
  color: #0000ff;
}

input {
  width: 80%;
  padding: 8px;
  margin: 10px 0;
  border-radius: 8px;
  border: 2px solid orange;
  background: linear-gradient(to bottom,grey,white);
  text-align: center;
  font-weight: bold;
  color: #000;
  font-size: 16px;
}

input.active {
  border: 3px solid #0044ff;
  background: linear-gradient(to bottom,grey,white);
}

button {
  padding: 10px 15px;
  margin: 5px;
  border: none;
  border-radius: 8px;
  background: linear-gradient(to bottom,blue,white);
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: 0.2s;
}

button:hover {
  background: linear-gradient(to bottom,blue,white);
}

.calc-buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 8px;
  margin-top: 10px;
}

canvas {
  margin-top: 15px;
  background: linear-gradient(to bottom,black,grey);
  border-radius: 10px;
}

.results {
  background: white;
  border-radius: 10px;
  margin-top: 10px;
  padding: 10px;
  font-weight: bold;
  color: #0000cc;
}

  
</style>

<script>
  let activeInput = null;

// -----------------------------
// Input Mo Sarili mo
// -----------------------------
function setActiveInput(id) {
  if (activeInput) document.getElementById(activeInput).classList.remove("active");
  activeInput = id;
  document.getElementById(id).classList.add("active");
}

document.getElementById("angle").addEventListener("click", () => setActiveInput("angle"));
document.getElementById("adjacent").addEventListener("click", () => setActiveInput("adjacent"));

function addValue(value) {
  if (!activeInput) {
    alert("Click an input box first!");
    return;
  }
  const input = document.getElementById(activeInput);
  input.value += value;
}

function trigFunction(func) {
  if (!activeInput) {
    alert("Click an input box first!");
    return;
  }

  const input = document.getElementById(activeInput);
  let val = parseFloat(input.value);
  if (isNaN(val)) {
    alert("Enter a valid number first!");
    return;
  }

  const rad = val * Math.PI / 180;
  let result = 0;

  if (func === "sin") result = Math.sin(rad);
  if (func === "cos") result = Math.cos(rad);
  if (func === "tan") result = Math.tan(rad);

  input.value = result.toFixed(4);
}

function clearInput() {
  if (!activeInput) return;
  document.getElementById(activeInput).value = "";
}

function resetAll() {
  document.getElementById("angle").value = "";
  document.getElementById("adjacent").value = "";
  document.getElementById("resultsBox").innerHTML = "Enter values to compute sides.";

  const canvas = document.getElementById("triangleCanvas");
  canvas.getContext("2d").clearRect(0, 0, canvas.width, canvas.height);

  if (activeInput) document.getElementById(activeInput).classList.remove("active");
  activeInput = null;
}

// -----------------------------
// Main Function: Drawing mo muka mo
// -----------------------------
function drawTriangle() {
  const canvas = document.getElementById('triangleCanvas');
  const ctx = canvas.getContext('2d');
  const angleA = parseFloat(document.getElementById('angle').value);
  const adjacent = parseFloat(document.getElementById('adjacent').value);

  if (isNaN(angleA) || isNaN(adjacent)) {
    alert("Tanga Kaba Axel!");
    return;
  }

  ctx.clearRect(0, 0, canvas.width, canvas.height);

  const angleARad = angleA * Math.PI / 180;
  const opposite = Math.tan(angleARad) * adjacent;
  const hypotenuse = Math.sqrt(adjacent ** 2 + opposite ** 2);

  // Calculate other angles
  const angleC = 90; // right angle
  const angleB = 90 - angleA;

  // Scale for drawing
  const scale = Math.min(180 / adjacent, 150 / opposite);
  const adjScaled = adjacent * scale;
  const oppScaled = opposite * scale;
  const baseX = (canvas.width - adjScaled) / 2;
  const baseY = 200;

  // Draw triangle
  ctx.beginPath();
  ctx.moveTo(baseX, baseY);
  ctx.lineTo(baseX + adjScaled, baseY);
  ctx.lineTo(baseX + adjScaled, baseY - oppScaled);
  ctx.closePath();

  const grad = ctx.createLinearGradient(baseX, baseY, baseX + adjScaled, baseY - oppScaled);
  grad.addColorStop(0, "#66aaff");
  grad.addColorStop(1, "#0033ff");
  ctx.fillStyle = grad;
  ctx.fill();

  ctx.strokeStyle = "white";
  ctx.lineWidth = 3;
  ctx.stroke();

  // Labels on triangle
  ctx.fillStyle = "white";
  ctx.font = "12px Arial";
  ctx.fillText("Angle A = " + angleA.toFixed(1) + "°", baseX + 5, baseY - 5);
  ctx.fillText("Angle B = " + angleB.toFixed(1) + "°", baseX + adjScaled - 60, baseY - oppScaled - 5);
  ctx.fillText("Angle C = 90°", baseX + adjScaled - 40, baseY + 15);
  ctx.fillText("Adjacent", baseX + adjScaled / 2 - 20, baseY + 15);
  ctx.fillText("Opposite", baseX + adjScaled + 5, baseY - oppScaled / 2);

  //  syempre Output results
  const resultBox = document.getElementById("resultsBox");
  resultBox.innerHTML = `
    <strong>Angles:</strong><br>
    A. = ${angleA.toFixed(2)}°<br>
    B. = ${angleB.toFixed(2)}°<br>
    C. = ${angleC.toFixed(2)}°<br><br>
    <strong>Sides:</strong><br>
   A. Adjacent = ${adjacent.toFixed(2)} units<br>
   B. Opposite = ${opposite.toFixed(2)} units<br>
   C. Hypotenuse = ${hypotenuse.toFixed(2)} units
  `;
}

</script>



