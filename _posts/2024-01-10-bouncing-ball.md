---
layout: post
title: "Bouncing Ball Simulation"
---

Welcome to the first interactive experiment on this blog.

Use the slider to change gravity and watch what happens.

<div style="margin: 1.5rem 0;">
  <label for="gravity">
    Gravity: <span id="gravity-value">0.50</span>
  </label>
  <input
    id="gravity"
    type="range"
    min="0.1"
    max="2.0"
    step="0.05"
    value="0.50"
    style="width: 100%; max-width: 400px;"
  >
</div>

<canvas
  id="sim-canvas"
  width="600"
  height="250"
  style="max-width: 100%; border: 1px solid #00ff00; background: #000000;"
>
  Your browser doesn't support canvas.
</canvas>

<script>
// --- parameters controlled by the UI ---
const gravityInput = document.getElementById("gravity");
const gravityValueLabel = document.getElementById("gravity-value");

// --- canvas + context ---
const canvas = document.getElementById("sim-canvas");
const ctx = canvas.getContext("2d");

// --- simulation state ---
let y = 30;                // vertical position
let v = 0;                 // vertical velocity
let radius = 15;
let restitution = 0.85;    // bounciness (0 = no bounce, 1 = perfect)

// read current gravity from slider
let g = parseFloat(gravityInput.value);

// update label text
gravityValueLabel.textContent = g.toFixed(2);

// when the slider changes, update gravity
gravityInput.addEventListener("input", () => {
  g = parseFloat(gravityInput.value);
  gravityValueLabel.textContent = g.toFixed(2);
});

// main animation loop
function step() {
  const dt = 1 / 60; // 60 FPS-ish

  // integrate velocity and position
  v += g * dt * 60; // scale a bit so it feels snappy
  y += v * dt * 60;

  const floorY = canvas.height - radius;

  // collision with floor
  if (y > floorY) {
    y = floorY;
    v = -v * restitution;
  }

  // some simple air drag so it settles eventually
  v *= 0.999;

  draw();
  requestAnimationFrame(step);
}

// draw the frame
function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // draw floor line
  ctx.strokeStyle = "#00ff00";
  ctx.beginPath();
  ctx.moveTo(0, canvas.height - 0.5);
  ctx.lineTo(canvas.width, canvas.height - 0.5);
  ctx.stroke();

  // draw the ball
  ctx.fillStyle = "#00ff00";
  ctx.beginPath();
  ctx.arc(canvas.width / 2, y, radius, 0, Math.PI * 2);
  ctx.fill();
}

// kick things off
step();
</script>
