- 👋 Hi, I’m @goemrstrys
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

HTML

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Simple Minecraft Simulator</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
    }
    canvas {
      display: block;
    }
  </style>
</head>
<body>
  <canvas id="minecraftCanvas"></canvas>
  <script src="minecraft-simulator.js"></script>
</body>
</html>





const canvas = document.getElementById("minecraftCanvas");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const tileSize = 50; // Size of each "block"
const rows = Math.floor(canvas.height / tileSize);
const cols = Math.floor(canvas.width / tileSize);

const colors = ["#8B4513", "#228B22", "#87CEEB"]; // Dirt, Grass, Sky

// Generate a simple grid world
const world = [];
for (let y = 0; y < rows; y++) {
  const row = [];
  for (let x = 0; x < cols; x++) {
    if (y === rows - 1) row.push(1); // Grass layer
    else if (y > rows - 4) row.push(0); // Dirt layers
    else row.push(2); // Sky
  }
  world.push(row);
}

// Draw the world
function drawWorld() {
  for (let y = 0; y < rows; y++) {
    for (let x = 0; x < cols; x++) {
      ctx.fillStyle = colors[world[y][x]];
      ctx.fillRect(x * tileSize, y * tileSize, tileSize, tileSize);
    }
  }
}

// Add a "break block" mechanic
canvas.addEventListener("click", (e) => {
  const x = Math.floor(e.clientX / tileSize);
  const y = Math.floor(e.clientY / tileSize);

  if (world[y][x] !== 2) {
    world[y][x] = 2; // Set to "sky" color
    drawWorld();
  }
});

// Initial draw
drawWorld();
