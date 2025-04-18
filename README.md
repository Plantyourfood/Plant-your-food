# Plant-your-food
 <!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <title>Mein digitaler Acker</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to bottom, #e9f5ec, #d2e5d6);
      color: #2e3b2c;
    }

    .landing {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      text-align: center;
    }

    .landing h1 {
      font-size: 48px;
      margin-bottom: 20px;
    }

    .landing p {
      font-size: 20px;
      max-width: 600px;
      margin-bottom: 30px;
    }

    .start-btn {
      padding: 14px 32px;
      font-size: 18px;
      background-color: #63a65b;
      border: none;
      border-radius: 10px;
      color: white;
      cursor: pointer;
      transition: transform 0.2s, background-color 0.3s;
    }

    .start-btn:hover {
      background-color: #558f4d;
      transform: scale(1.05);
    }

    #ackerContainer {
      display: none;
      flex-direction: column;
      height: 100vh;
    }

    #topbar {
      background-color: #e6f2e3;
      padding: 10px 20px;
      display: flex;
      justify-content: flex-end;
      align-items: center;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }

    .menu-btn {
      background: none;
      border: none;
      font-size: 16px;
      color: #2e3b2c;
      cursor: pointer;
      padding: 8px 14px;
      border-radius: 8px;
      transition: background-color 0.2s ease;
    }

    .menu-btn:hover {
      background-color: #d0e8d0;
    }
  </style>
</head>
<body>

<div class="landing" id="landingPage">
  <h1>Willkommen auf deinem digitalen Acker!</h1>
  <p>Pflanze Gemüse, beobachte das Wachstum und gestalte deinen virtuellen Garten – ganz einfach, spielerisch und verbunden mit der Natur.</p>
  <button class="start-btn" onclick="startGarden()">Jetzt loslegen</button>
</div>

<div id="ackerContainer">
  <div id="topbar">
    <button class="menu-btn" onclick="goHome()">Zurück zur Startseite</button>
  </div>

<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <title>Virtueller Acker</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background-color: #f2f7f1;
      color: #2e3b2c;
      display: flex;
      flex-direction: column;
      height: 100vh;
    }
    #info {
      padding: 12px;
      background-color: #e6f2e3;
      text-align: center;
      font-size: 16px;
      font-weight: 500;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    #info span {
      flex-grow: 1;
      text-align: center;
    }
    #mainArea {
      flex: 1;
      display: flex;
    }
    #sidebar {
      width: 180px;
      background-color: #ffffff;
      border-left: 1px solid #cbdac5;
      padding: 16px 8px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 20px;
    }
    .plant-option {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    .plant-option img {
      width: 80px;
      height: 80px;
      object-fit: contain;
      border: 2px solid transparent;
      border-radius: 12px;
      cursor: pointer;
    }
    .plant-option img.selected {
      border-color: #63a65b;
      box-shadow: 0 0 8px rgba(99, 166, 91, 0.3);
    }
    canvas {
      border: none;
      margin: 10px auto;
      display: block;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
      touch-action: none;
    }
    .popup {
      position: absolute;
      top: 20px;
      left: 20px;
      background: #ffffff;
      border: 1px solid #a3c1a3;
      padding: 18px;
      border-radius: 14px;
      box-shadow: 0 6px 16px rgba(0, 0, 0, 0.15);
      font-size: 14px;
      display: none;
      z-index: 10;
      max-width: 280px;
    }
    .popup button {
      margin-top: 12px;
      margin-right: 10px;
      padding: 8px 14px;
      background-color: #63a65b;
      border: none;
      border-radius: 6px;
      color: white;
      font-size: 14px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div id="info">
    <span>
      <span id="count-tomato">Tomaten: 0</span> |
      <span id="count-lettuce">Salate: 0</span> |
      <span id="count-carrot">Karotten: 0</span>
    </span>
  </div>

  <div id="confirmBox" class="popup">
    <div>Möchtest du diese Pflanze entfernen?</div>
    <button onclick="confirmRemove(true)">Ja</button>
    <button onclick="confirmRemove(false)">Nein</button>
  </div>

  <div id="infoBox" class="popup">
    <div id="infoContent"></div>
    <button onclick="document.getElementById('infoBox').style.display='none'">Schließen</button>
  </div>

  <div id="mainArea">
    <canvas id="fieldCanvas" width="500" height="500"></canvas>
    <div id="sidebar">
      <div class="plant-option">
        <img src="https://www.dropbox.com/scl/fi/imgznn65f1r30vg03suyr/Foto-31.03.25-15-56-47.png?rlkey=tbm43ne8rcpdzb09o2fr1gy7h&raw=1" data-type="tomato" onclick="selectPlant(this)">
        <button class="info-btn" onclick="showInfo('tomato')">i</button>
      </div>
      <div class="plant-option">
        <img src="https://www.dropbox.com/scl/fi/pjknze6vj69km3dc1uacs/Foto-31.03.25-16-16-11.png?rlkey=h29p5te6mrd1i8p1p08tc1q5t&raw=1" data-type="lettuce" onclick="selectPlant(this)">
        <button class="info-btn" onclick="showInfo('lettuce')">i</button>
      </div>
      <div class="plant-option">
        <img src="https://www.dropbox.com/scl/fi/hleuhgxgb8v95voanj692/Foto-31.03.25-17-42-36.png?rlkey=lif87e2n296bgvzvym18u8jqr&raw=1" data-type="carrot" onclick="selectPlant(this)">
        <button class="info-btn" onclick="showInfo('carrot')">i</button>
      </div>
    </div>
  </div>

  <script>
    const canvas = document.getElementById("fieldCanvas");
    const ctx = canvas.getContext("2d");
    const cellSize = 50;
    const gridCount = 10;
    const plants = [];
    let occupied = Array.from({ length: gridCount }, () => Array(gridCount).fill(null));
    let selectedType = null;
    let selectedPlantIndex = null;

    const backgroundImage = new Image();
    backgroundImage.src = "https://www.dropbox.com/scl/fi/ebjtylphw7r05u5imaw7n/Foto-31.03.25-17-51-43.png?rlkey=hyty37buet7j76vphyzlkat3l&raw=1";

    const placementIcon = new Image();
    placementIcon.src = "https://www.dropbox.com/scl/fi/fcw0almie7ezv9c8x4laa/Foto-02.04.25-21-04-49.png?rlkey=gurm5g7z8tkxg11cunx3ndl2a&raw=1";

    const images = {
      tomato: new Image(),
      lettuce: new Image(),
      carrot: new Image()
    };

    images.tomato.src = document.querySelector('[data-type="tomato"]').src;
    images.lettuce.src = document.querySelector('[data-type="lettuce"]').src;
    images.carrot.src = "https://www.dropbox.com/scl/fi/hleuhgxgb8v95voanj692/Foto-31.03.25-17-42-36.png?rlkey=lif87e2n296bgvzvym18u8jqr&raw=1";

    const sizeMap = { tomato: 6, lettuce: 3, carrot: 1 };

    function selectPlant(img) {
      document.querySelectorAll("#sidebar img").forEach(i => i.classList.remove("selected"));
      img.classList.add("selected");
      selectedType = img.dataset.type;
    }

    canvas.addEventListener("click", (e) => {
      const rect = canvas.getBoundingClientRect();
      const xClick = e.clientX - rect.left;
      const yClick = e.clientY - rect.top;
      const x = Math.floor(xClick / cellSize);
      const y = Math.floor(yClick / cellSize);

      for (let i = plants.length - 1; i >= 0; i--) {
        const p = plants[i];
        if (x >= p.x && x < p.x + p.size && y >= p.y && y < p.y + p.size) {
          selectedPlantIndex = i;
          document.getElementById("confirmBox").style.display = "block";
          return;
        }
      }

      if (!selectedType) return;
      const s = sizeMap[selectedType];
      if (x + s > gridCount || y + s > gridCount) return;
      for (let dx = 0; dx < s; dx++) {
        for (let dy = 0; dy < s; dy++) {
          if (occupied[x + dx][y + dy]) return;
        }
      }

      for (let dx = 0; dx < s; dx++) {
        for (let dy = 0; dy < s; dy++) {
          occupied[x + dx][y + dy] = selectedType;
        }
      }

      plants.push({ type: selectedType, x, y, size: s, placedAt: performance.now() });
    });

    function drawGrid() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      if (backgroundImage.complete && backgroundImage.naturalWidth > 0) {
        ctx.drawImage(backgroundImage, 0, 0, canvas.width, canvas.height);
      } else {
        ctx.fillStyle = "#8B4513";
        ctx.fillRect(0, 0, canvas.width, canvas.height);
      }
      ctx.strokeStyle = "#b2c49b";
      for (let i = 0; i <= gridCount; i++) {
        ctx.beginPath();
        ctx.moveTo(i * cellSize, 0);
        ctx.lineTo(i * cellSize, canvas.height);
        ctx.moveTo(0, i * cellSize);
        ctx.lineTo(canvas.width, i * cellSize);
        ctx.stroke();
      }
    }

    function drawAvailableZones() {
      if (!selectedType) return;
      const s = sizeMap[selectedType];
      const used = new Set();

      for (let x = 0; x <= gridCount - s; x++) {
        for (let y = 0; y <= gridCount - s; y++) {
          let fits = true;
          for (let dx = 0; dx < s; dx++) {
            for (let dy = 0; dy < s; dy++) {
              if (occupied[x + dx][y + dy]) fits = false;
            }
          }
          if (fits) {
            for (let dx = 0; dx < s; dx++) {
              for (let dy = 0; dy < s; dy++) {
                const key = `${x + dx}_${y + dy}`;
                if (!used.has(key)) {
                  used.add(key);
                  ctx.fillStyle = "rgba(144,238,144,0.2)";
                  ctx.fillRect((x + dx) * cellSize, (y + dy) * cellSize, cellSize, cellSize);
                }
              }
            }
            ctx.strokeStyle = "limegreen";
            ctx.lineWidth = 2;
            ctx.strokeRect(x * cellSize, y * cellSize, s * cellSize, s * cellSize);
            if (placementIcon.complete) {
              ctx.drawImage(placementIcon, x * cellSize + 12, y * cellSize + 12, 26, 26);
            }
          }
        }
      }
    }

    function drawAll() {
      drawGrid();
      drawAvailableZones();
      const now = performance.now();
      const durations = { tomato: 3000, lettuce: 2000, carrot: 1000 };

      plants.forEach(p => {
        const elapsed = now - p.placedAt;
        const duration = durations[p.type];
        const progress = Math.min(elapsed / duration, 1);
        const drawSize = p.size * cellSize * progress;
        const offset = (p.size * cellSize - drawSize) / 2;

        ctx.drawImage(images[p.type], p.x * cellSize + offset, p.y * cellSize + offset, drawSize, drawSize);
        ctx.strokeStyle = "yellow";
        ctx.lineWidth = 2;
        ctx.strokeRect(p.x * cellSize, p.y * cellSize, p.size * cellSize, p.size * cellSize);
      });

      updateCounters();
    }

    function updateCounters() {
      const count = { tomato: 0, lettuce: 0, carrot: 0 };
      plants.forEach(p => count[p.type]++);
      document.getElementById("count-tomato").textContent = `Tomaten: ${count.tomato}`;
      document.getElementById("count-lettuce").textContent = `Salate: ${count.lettuce}`;
      document.getElementById("count-carrot").textContent = `Karotten: ${count.carrot}`;
    }

    function confirmRemove(confirm) {
      document.getElementById("confirmBox").style.display = "none";
      if (confirm && selectedPlantIndex !== null) {
        const p = plants[selectedPlantIndex];
        for (let dx = 0; dx < p.size; dx++) {
          for (let dy = 0; dy < p.size; dy++) {
            occupied[p.x + dx][p.y + dy] = null;
          }
        }
        plants.splice(selectedPlantIndex, 1);
        selectedPlantIndex = null;
      }
    }

    function showInfo(type) {
      const infoBox = document.getElementById("infoBox");
      const content = document.getElementById("infoContent");
      const info = {
        tomato: {
          name: "Tomate",
          sowing: "März – April",
          duration: "ca. 120 Tage",
          harvest: "Juli – August",
          space: "60 cm",
          desc: "Sonnengereift, saftig und voller Aroma – unsere Tomaten sind ein Highlight in jedem Garten. Ideal für Salate, Soßen oder einfach pur genießen."
        },
        lettuce: {
          name: "Salat",
          sowing: "März – Juli",
          duration: "ca. 60 Tage",
          harvest: "Mai – September",
          space: "30 cm",
          desc: "Frisch, knackig und voller Vitamine – Salat ist ein echter Allrounder. Perfekt für leichte Sommersalate oder als Beilage zu jedem Gericht."
        },
        carrot: {
          name: "Karotte",
          sowing: "März – Juni",
          duration: "ca. 80–100 Tage",
          harvest: "Juni – Oktober",
          space: "10 cm",
          desc: "Knackig, süß und gesund – Karotten gehören in jeden Garten. Ob roh geknabbert oder gekocht, sie sind immer ein Genuss."
        }
      };

      const d = info[type];
      content.innerHTML = `
        <strong>${d.name}</strong><br>
        <b>Aussaat:</b> ${d.sowing}<br>
        <b>Wachstumsdauer:</b> ${d.duration}<br>
        <b>Ernte:</b> ${d.harvest}<br>
        <b>Platzbedarf:</b> ${d.space}<br><br>${d.desc}
      `;
      infoBox.style.display = "block";
    }

    function animate() {
      drawAll();
      requestAnimationFrame(animate);
    }

    backgroundImage.onload = animate;
  </script>
</body>
</html>

  </div>
</div>

<script>
  function startGarden() {
    document.getElementById('landingPage').style.display = 'none';
    document.getElementById('ackerContainer').style.display = 'flex';

    // Acker zurücksetzen (optional: je nach Bedarf erweitern)
    document.getElementById('ackerContent').innerHTML = originalAckerHTML;
    if (typeof animate === 'function') animate();
  }

  function goHome() {
    document.getElementById('landingPage').style.display = 'flex';
    document.getElementById('ackerContainer').style.display = 'none';

    // Reset des Ackers
    document.getElementById('ackerContent').innerHTML = ''; // oder wieder originalAckerHTML
  }

  // Optional: Originalinhalt des Ackers zwischenspeichern, wenn du den später automatisch laden willst
  const originalAckerHTML = document.getElementById('ackerContent').innerHTML;
</script>

</body>
</html>
