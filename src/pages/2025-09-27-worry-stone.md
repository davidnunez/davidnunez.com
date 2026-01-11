---
tags:
  - page
  - exported-2026-01-10
id: 68d7c7411d422100013541a1
title: "Worry Stone"
feature_image: 
description: "let stone = { x: 0, y: 0, baseRadius: 120, currentRadius: 120, warmth: 0, smoothness: 0, ripples: [], particles: [], hue: 180, saturation:…"
date: 2025-09-27
full-date: "2025-09-27T07:36:58.000-04:00"
slug: worry-stone
type: page
edit-link: https://davidnunez.ghost.io/ghost/#/editor/page/68d7c7411d422100013541a1
---
	 <script>
				let stone = {
						x: 0,
						y: 0,
						baseRadius: 120,
						currentRadius: 120,
						warmth: 0,
						smoothness: 0,
						ripples: [],
						particles: [],
						hue: 180,
						saturation: 70,
						brightness: 45
				};
				
				let lastTouch = { x: 0, y: 0 };
				let touchStartTime = 0;
				let isPressed = false;
				let longPressThreshold = 500; // milliseconds

				function setup() {
						createCanvas(windowWidth, windowHeight);
						colorMode(HSB, 360, 100, 100, 1);
						stone.x = width / 2;
						stone.y = 150;
				}

				function draw() {
						background('#fdfdfc');
						
						// Update stone properties
						stone.warmth *= 0.99;
						stone.smoothness *= 0.995;
						stone.currentRadius = lerp(stone.currentRadius, stone.baseRadius + stone.warmth * 20, 0.1);
						
						// Update particles
						for (let i = stone.particles.length - 1; i >= 0; i--) {
								let p = stone.particles[i];
								p.x += p.vx;
								p.y += p.vy;
								p.life -= 0.02;
								p.vx *= 0.99;
								p.vy *= 0.99;
								
								if (p.life <= 0) {
										stone.particles.splice(i, 1);
								}
						}
						
						// Update ripples
						for (let i = stone.ripples.length - 1; i >= 0; i--) {
								let ripple = stone.ripples[i];
								ripple.radius += ripple.speed;
								ripple.alpha -= 0.02;
								
								if (ripple.alpha <= 0) {
										stone.ripples.splice(i, 1);
								}
						}
						
						// Draw ambient glow
						drawGlow();
						
						// Draw ripples
						drawRipples();
						
						// Draw the stone
						drawStone();
						
						// Draw particles
						drawParticles();
						
						// Update touch duration
						if (isPressed) {
								let currentTime = millis();
								let touchDuration = currentTime - touchStartTime;
								
								// Visual feedback for long press building up
								if (touchDuration > 200) {
										stone.warmth = min(stone.warmth + 0.02, 1);
										if (touchDuration > 400 && frameCount % 10 === 0) {
												createParticles(stone.x + random(-20, 20), stone.y + random(-20, 20), 1);
										}
								}
						}
				}
				
				function drawGlow() {
						let glowSize = stone.currentRadius * 2.5;
						let glowIntensity = stone.warmth * 0.4 + 0.05;
						
						// Subtle inner glow effect instead of outer glow
						for (let i = 0; i < 3; i++) {
								let alpha = (glowIntensity * (3 - i)) / 3;
								fill(stone.hue + 15, stone.saturation + 20, stone.brightness + 10, alpha);
								noStroke();
								ellipse(stone.x, stone.y, stone.currentRadius * 2 * (0.7 + i * 0.1));
						}
				}
				
				function drawStone() {
						push();
						translate(stone.x, stone.y);
						
						// Enhanced stone shadow for light background
						fill(0, 0, 20, 0.15);
						ellipse(6, 8, stone.currentRadius * 2.1);
						
						// Secondary shadow for depth
						fill(0, 0, 30, 0.08);
						ellipse(3, 4, stone.currentRadius * 2.05);
						
						// Main stone body with gradient effect
						for (let i = 0; i < 25; i++) {
								let lerpAmount = i / 25;
								let currentRadius = stone.currentRadius * (1 - lerpAmount * 0.2);
								let brightness = stone.brightness + lerpAmount * 15 + stone.warmth * 8;
								let saturation = stone.saturation + stone.smoothness * 10;
								
								fill(stone.hue, saturation, brightness, 0.9);
								noStroke();
								ellipse(0, 0, currentRadius * 2);
						}
						
						// Enhanced highlight for definition
						let highlightBrightness = min(75, stone.brightness + 20 + stone.warmth * 12);
						fill(stone.hue - 10, stone.saturation * 0.6, highlightBrightness, 0.7);
						ellipse(-stone.currentRadius * 0.3, -stone.currentRadius * 0.3, stone.currentRadius * 0.6);
						
						// Subtle rim lighting
						stroke(stone.hue - 20, stone.saturation + 15, stone.brightness + 25, 0.3);
						strokeWeight(2);
						noFill();
						ellipse(0, 0, stone.currentRadius * 2);
						
						pop();
				}
				
				function drawRipples() {
						stroke(stone.hue - 30, stone.saturation + 20, stone.brightness + 15);
						noFill();
						
						for (let ripple of stone.ripples) {
								strokeWeight(4 * ripple.alpha);
								stroke(stone.hue - 30, stone.saturation + 20, stone.brightness + 15, ripple.alpha * 0.8);
								ellipse(ripple.x, ripple.y, ripple.radius * 2);
						}
				}
				
				function drawParticles() {
						noStroke();
						
						for (let p of stone.particles) {
								let alpha = p.life * 0.8;
								fill(p.hue, p.saturation, p.brightness, alpha);
								ellipse(p.x, p.y, p.size * p.life);
						}
				}
				
				function createRipple(x, y) {
						stone.ripples.push({
								x: x,
								y: y,
								radius: 0,
								speed: 3,
								alpha: 0.8
						});
				}
				
				function createParticles(x, y, count = 5) {
						for (let i = 0; i < count; i++) {
								stone.particles.push({
										x: x + random(-10, 10),
										y: y + random(-10, 10),
										vx: random(-2, 2),
										vy: random(-3, -1),
										life: 1,
										size: random(3, 8),
										hue: stone.hue + random(-30, 30),
										saturation: stone.saturation + 20,
										brightness: stone.brightness + 20
								});
						}
				}
				
				function addWarmth() {
						stone.warmth = min(stone.warmth + 0.1, 1);
						stone.hue = lerp(stone.hue, 220, 0.02); // Shift toward warmer teal-purple
				}
				
				function addSmoothness() {
						stone.smoothness = min(stone.smoothness + 0.2, 1);
						stone.saturation = lerp(stone.saturation, 85, 0.05);
				}
				
				// Touch and mouse events
				function mousePressed() {
						if (dist(mouseX, mouseY, stone.x, stone.y) < stone.currentRadius) {
								isPressed = true;
								touchStartTime = millis();
								lastTouch.x = mouseX;
								lastTouch.y = mouseY;
								createRipple(mouseX, mouseY);
						}
				}
				
				function mouseDragged() {
						if (isPressed) {
								let touchDistance = dist(mouseX, mouseY, lastTouch.x, lastTouch.y);
								if (touchDistance > 5) {
										addSmoothness();
										createParticles(mouseX, mouseY, 2);
										lastTouch.x = mouseX;
										lastTouch.y = mouseY;
								}
						}
				}
				
				function mouseReleased() {
						if (isPressed) {
								let currentTime = millis();
								let touchDuration = currentTime - touchStartTime;
								
								isPressed = false;
								
								if (touchDuration > longPressThreshold) { // Long press detected
										addWarmth();
										createParticles(mouseX, mouseY, 12);
										
										// Extra visual feedback for successful long press
										for (let i = 0; i < 3; i++) {
												setTimeout(() => createRipple(stone.x, stone.y), i * 100);
										}
								}
								
								touchStartTime = 0;
						}
				}
				
				// Touch events for mobile
				function touchStarted() {
						if (touches.length > 0) {
								let touch = touches[0];
								// Only capture touches within stone area
								if (dist(touch.x, touch.y, stone.x, stone.y) < stone.currentRadius + 50) {
										if (dist(touch.x, touch.y, stone.x, stone.y) < stone.currentRadius) {
												isPressed = true;
												touchStartTime = millis();
												lastTouch.x = touch.x;
												lastTouch.y = touch.y;
												createRipple(touch.x, touch.y);
										}
										return false; // Prevent default only for stone area
								}
						}
						return true; // Allow default behavior for other areas
				}
				
				function touchMoved() {
						if (isPressed && touches.length > 0) {
								let touch = touches[0];
								let touchDistance = dist(touch.x, touch.y, lastTouch.x, lastTouch.y);
								if (touchDistance > 5) {
										addSmoothness();
										createParticles(touch.x, touch.y, 2);
										lastTouch.x = touch.x;
										lastTouch.y = touch.y;
								}
								return false; // Prevent default only when actively interacting with stone
						}
						return true; // Allow default behavior when not interacting with stone
				}
				
				function touchEnded() {
						if (isPressed) {
								let currentTime = millis();
								let touchDuration = currentTime - touchStartTime;
								
								isPressed = false;
								
								if (touchDuration > longPressThreshold) { // Long press detected
										addWarmth();
										if (touches.length > 0) {
												createParticles(touches[0].x, touches[0].y, 12);
										} else {
												createParticles(stone.x, stone.y, 12);
										}
										
										// Extra visual feedback for successful long press
										for (let i = 0; i < 3; i++) {
												setTimeout(() => createRipple(stone.x, stone.y), i * 100);
										}
								}
								
								touchStartTime = 0;
								return false; // Prevent default only when we were interacting with stone
						}
						return true; // Allow default behavior when not interacting with stone
				}
				
				function windowResized() {
						resizeCanvas(windowWidth, windowHeight);
						stone.x = width / 2;
						stone.y = 150;
				}
		</script>