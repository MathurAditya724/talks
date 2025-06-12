---
theme: default
title: Hono x MCP x Cloudflare Workers
info: |
  ## Hono x MCP x Cloudflare Workers
  Bridging AI and Edge Computing

  A tech talk presentation about combining Hono.js, Model Context Protocol, and Cloudflare Workers
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
colorSchema: dark
fonts:
  sans: "Inter"
  mono: "Fira Code"
---

<style>
:root {
  --cloudflare-orange: #F38020;
  --hono-red: #E36002;
  --tech-blue: #2563EB;
  --tech-blue-light: #3B82F6;
}

.gradient-bg {
  background: linear-gradient(135deg, var(--cloudflare-orange), var(--hono-red), var(--tech-blue));
  background-size: 400% 400%;
  animation: gradientFlow 8s ease infinite;
}

@keyframes gradientFlow {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.floating-particles {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
  top: 0;
  left: 0;
  z-index: 1;
}

.particle {
  position: absolute;
  width: 32px;
  height: 32px;
  animation: float 8s infinite linear;
  opacity: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.particle img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

@keyframes float {
  0% { 
    transform: translateY(100vh) rotate(0deg) scale(0); 
    opacity: 0; 
  }
  5% { 
    opacity: 0.8; 
    transform: translateY(95vh) rotate(18deg) scale(1);
  }
  95% { 
    opacity: 0.8; 
    transform: translateY(-5vh) rotate(342deg) scale(1);
  }
  100% { 
    transform: translateY(-10vh) rotate(360deg) scale(0); 
    opacity: 0; 
  }
}

.pulse {
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); opacity: 0.8; }
  50% { transform: scale(1.05); opacity: 1; }
}
</style>

# Hono x MCP x Cloudflare Workers

## Bridging AI and Edge Computing

<div class="gradient-bg fixed inset-0 -z-10 pulse">
  <div class="floating-particles">
    <div class="particle" style="left: 10%; animation-delay: 0s;">
      <img src="/hono_logo.svg" alt="Hono Logo" />
    </div>
    <div class="particle" style="left: 20%; animation-delay: 1s;">
      <img src="/cloudflare_workers_logo.png" alt="Cloudflare Workers Logo" />
    </div>
    <div class="particle" style="left: 30%; animation-delay: 2s;">
      <img src="/hono_logo.svg" alt="Hono Logo" />
    </div>
    <div class="particle" style="left: 40%; animation-delay: 3s;">
      <img src="/cloudflare_workers_logo.png" alt="Cloudflare Workers Logo" />
    </div>
    <div class="particle" style="left: 50%; animation-delay: 4s;">
      <img src="/hono_logo.svg" alt="Hono Logo" />
    </div>
    <div class="particle" style="left: 60%; animation-delay: 5s;">
      <img src="/cloudflare_workers_logo.png" alt="Cloudflare Workers Logo" />
    </div>
    <div class="particle" style="left: 70%; animation-delay: 0.5s;">
      <img src="/hono_logo.svg" alt="Hono Logo" />
    </div>
    <div class="particle" style="left: 80%; animation-delay: 1.5s;">
      <img src="/cloudflare_workers_logo.png" alt="Cloudflare Workers Logo" />
    </div>
    <div class="particle" style="left: 90%; animation-delay: 2.5s;">
      <img src="/hono_logo.svg" alt="Hono Logo" />
    </div>
    <div class="particle" style="left: 15%; animation-delay: 3.5s;">
      <img src="/cloudflare_workers_logo.png" alt="Cloudflare Workers Logo" />
    </div>
    <div class="particle" style="left: 25%; animation-delay: 4.5s;">
      <img src="/hono_logo.svg" alt="Hono Logo" />
    </div>
    <div class="particle" style="left: 35%; animation-delay: 5.5s;">
      <img src="/cloudflare_workers_logo.png" alt="Cloudflare Workers Logo" />
    </div>
    <div class="particle" style="left: 45%; animation-delay: 6s;">
      <img src="/hono_logo.svg" alt="Hono Logo" />
    </div>
    <div class="particle" style="left: 55%; animation-delay: 6.5s;">
      <img src="/cloudflare_workers_logo.png" alt="Cloudflare Workers Logo" />
    </div>
    <div class="particle" style="left: 65%; animation-delay: 7s;">
      <img src="/hono_logo.svg" alt="Hono Logo" />
    </div>
    <div class="particle" style="left: 75%; animation-delay: 7.5s;">
      <img src="/cloudflare_workers_logo.png" alt="Cloudflare Workers Logo" />
    </div>
    <div class="particle" style="left: 85%; animation-delay: 0.25s;">
      <img src="/hono_logo.svg" alt="Hono Logo" />
    </div>
    <div class="particle" style="left: 95%; animation-delay: 1.25s;">
      <img src="/cloudflare_workers_logo.png" alt="Cloudflare Workers Logo" />
    </div>
  </div>
</div>

<!--
Welcome to our tech talk on combining three powerful technologies: Hono.js, Model Context Protocol, and Cloudflare Workers. Today we'll explore how these technologies work together to bridge AI and edge computing.
-->

---
layout: center
class: text-center
---

<style scoped>
.profile-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}

.profile-photo {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--cloudflare-orange), var(--hono-red));
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 3rem;
  color: white;
  animation: slideInLeft 0.8s ease-out;
}

.profile-info {
  animation: slideInLeft 0.8s ease-out 0.2s both;
}

.social-links {
  display: flex;
  gap: 2rem;
  margin-top: 1rem;
}

.social-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 1rem;
  border-radius: 0.5rem;
  background: rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
  animation: staggerIn 0.6s ease-out both;
}

.social-link:nth-child(1) { animation-delay: 0.6s; }
.social-link:nth-child(2) { animation-delay: 0.8s; }
.social-link:nth-child(3) { animation-delay: 1.0s; }

.social-link:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: translateY(-2px);
}

@keyframes slideInLeft {
  from {
    opacity: 0;
    transform: translateX(-50px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes staggerIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>

<div class="profile-container">
  <div class="profile-photo">
    <img src="https://avatars.githubusercontent.com/u/57684218?v=4" alt="Aditya Mathur" class="rounded-full w-full h-full object-cover" />
  </div>
  
  <div class="profile-info">
    <h1 class="text-4xl font-bold mb-2">Aditya Mathur</h1>
    <p class="text-xl text-gray-400">Backend Developer</p>
  </div>
  
  <div class="social-links">
    <a href="https://github.com/mathuraditya724" class="social-link">
      <carbon:logo-github class="text-xl" />
      @mathuraditya724
    </a>
    <a href="https://x.com/mathurAditya7" class="social-link">
      <carbon:logo-x class="text-xl" />
      @mathuraditya7
    </a>
    <a href="https://bsky.app/profile/adima7.bsky.social" class="social-link">
      <bi:bluesky class="text-xl" />
      @adima7.bsky.social
    </a>
  </div>
</div>

<!--
Let me introduce myself. Feel free to update this slide with your actual information before presenting.
-->

---
layout: center
class: text-center
---

# MCP Architecture
<img v-click="1" v-click.hide="2" src="/mcp_hub.png" alt="MCP Architecture" class="w-full absolute max-w-3xl translate-x-1/2 -translate-y-1/2 right-1/2 top-1/2">
<img v-click="2" src="/mcp_hub_with_adapters.png" alt="MCP Adapter Architecture" class="w-full absolute max-w-3xl translate-x-1/2 -translate-y-1/2 right-1/2 top-1/2">

<!--
The Model Context Protocol creates a hub-and-spoke architecture where LLMs can connect to various services. Click to see how it extends to major cloud providers including Cloudflare.
-->

---
layout: center
class: text-center
---

<style scoped>
.workers-ecosystem {
  position: relative;
  width: 100%;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.workers-logo {
  position: relative;
  width: 140px;
  height: 140px;
  background: white;
  border-radius: 20px;
  padding: 1rem;
  display: flex;
  align-items: center;
  border: 2px solid var(--tech-blue);
  justify-content: center;
  color: white;
  font-weight: bold;
  font-size: 1.1rem;
  z-index: 10;
  animation: centerPulse 3s ease-in-out infinite;
}

.service {
  position: absolute;
  width: 100px;
  height: 100px;
  background: white;
  border: 2px solid var(--tech-blue);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.85rem;
  color: black;
  text-align: center;
  padding: 0.5rem;
  animation: orbit 24s linear infinite;
  transform-origin: 50vw 50vh;
}

.scared-dev {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  opacity: 0;
  z-index: 15;
  animation: scaredDevAppear 0.8s ease-out forwards;
}

.speech-bubble {
  position: relative;
  background: white;
  color: #333;
  padding: 1rem 1.5rem;
  border-radius: 1rem;
  margin-bottom: 0.5rem;
  white-space: nowrap;
  animation: bubbleWobble 0.5s ease-out;
}

.speech-bubble::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 0;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-top: 10px solid white;
}

@keyframes centerPulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.1); }
}

@keyframes orbit {
  from { transform: rotate(0deg) translateX(180px) rotate(0deg); }
  to { transform: rotate(360deg) translateX(180px) rotate(-360deg); }
}

@keyframes scaredDevAppear {
  from {
    opacity: 0;
    transform: translate(-50%, -50%) scale(0.5);
  }
  to {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }
}

@keyframes bubbleWobble {
  0%, 100% { transform: scale(1); }
  25% { transform: scale(1.05); }
  75% { transform: scale(0.95); }
}

.service:nth-child(2) { animation-delay: 0s; }
.service:nth-child(3) { animation-delay: -4s; }
.service:nth-child(4) { animation-delay: -8s; }
.service:nth-child(5) { animation-delay: -12s; }
.service:nth-child(6) { animation-delay: -16s; }
.service:nth-child(7) { animation-delay: -20s; }
</style>

<div class="workers-ecosystem">
  <div class="workers-logo">
    <img src="/cloudflare_workers.png" alt="Cloudflare Workers Logo" />
  </div>
  
  <div class="service">Workers KV</div>
  <div class="service">Durable Objects</div>
  <div class="service">Workers Assets</div>
  <div class="service">R2 Storage</div>
  <div class="service">Workers AI</div>
  <div class="service">Queues</div>
  
  <div v-click class="scared-dev">
    <div class="speech-bubble">
      This is overwhelming!
    </div>
    <div class="text-6xl">😰</div>
  </div>
</div>

<!--
Cloudflare Workers offers a rich ecosystem of services that orbit around the core Workers platform. But this can feel overwhelming for developers. Click to see the typical developer reaction!
-->

---
layout: center
class: text-center
---

<style scoped>
.salt-meme-container {
  position: relative;
  width: 100%;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.workers-base {
  position: relative;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  z-index: 1;
}

.workers-logo-scattered {
  width: 80px;
  height: 80px;
  background: rgba(248, 128, 32, 0.3);
  border: 2px solid var(--cloudflare-orange);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--cloudflare-orange);
  animation: logoFloat 3s ease-in-out infinite;
}

.workers-logo-scattered:nth-child(odd) {
  animation-delay: 0.5s;
}

.salt-shaker {
  position: absolute;
  top: 20%;
  right: 20%;
  font-size: 4rem;
  animation: shake 1s ease-in-out infinite;
  z-index: 10;
}

.hono-salt {
  position: absolute;
  width: 20px;
  height: 20px;
  background: var(--hono-red);
  border-radius: 50%;
  animation: sprinkle 2s ease-out infinite;
  z-index: 5;
}

.title-text {
  position: absolute;
  bottom: 10%;
  left: 50%;
  transform: translateX(-50%);
  font-size: 1rem;
  font-weight: bold;
  color: white;
  z-index: 15;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
  animation: titleGlow 2s ease-in-out infinite alternate;
}

@keyframes logoFloat {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-10px) rotate(5deg); }
}

@keyframes shake {
  0%, 100% { transform: rotate(0deg); }
  25% { transform: rotate(-5deg); }
  75% { transform: rotate(5deg); }
}

@keyframes sprinkle {
  0% {
    opacity: 0;
    transform: translateY(-50px) scale(0);
  }
  20% {
    opacity: 1;
    transform: translateY(0px) scale(1);
  }
  100% {
    opacity: 0;
    transform: translateY(100px) scale(0.5);
  }
}

@keyframes titleGlow {
  0% { text-shadow: 2px 2px 4px rgba(0,0,0,0.3); }
  100% { text-shadow: 2px 2px 20px rgba(227, 96, 2, 0.6); }
}

/* Position salt particles */
.salt-1 { top: 30%; left: 40%; animation-delay: 0s; }
.salt-2 { top: 35%; left: 45%; animation-delay: 0.2s; }
.salt-3 { top: 25%; left: 50%; animation-delay: 0.4s; }
.salt-4 { top: 40%; left: 35%; animation-delay: 0.6s; }
.salt-5 { top: 30%; left: 55%; animation-delay: 0.8s; }
.salt-6 { top: 45%; left: 40%; animation-delay: 1s; }
.salt-7 { top: 35%; left: 60%; animation-delay: 1.2s; }
.salt-8 { top: 50%; left: 45%; animation-delay: 1.4s; }
</style>

<div class="salt-meme-container">
  <div class="workers-base">
    <div class="workers-logo-scattered">
      <img src="/cloudflare_workers_logo.png" alt="Cloudflare workers logos" class="w-full h-full object-contain p-3" />
    </div>
    <div class="workers-logo-scattered">
      <img src="/hono_logo.svg" alt="Hono.js Logo" class="w-full h-full object-contain p-3" />
    </div>
    <div class="workers-logo-scattered">
      <img src="/cloudflare_workers_logo.png" alt="Cloudflare workers logos" class="w-full h-full object-contain p-3" />
    </div>
    <div class="workers-logo-scattered">
      <img src="/hono_logo.svg" alt="Hono.js Logo" class="w-full h-full object-contain p-3" />
    </div>
    <div class="workers-logo-scattered">
      <img src="/cloudflare_workers_logo.png" alt="Cloudflare workers logos" class="w-full h-full object-contain p-3" />
    </div>
    <div class="workers-logo-scattered">
      <img src="/hono_logo.svg" alt="Hono.js Logo" class="w-full h-full object-contain p-3" />
    </div>
  </div>
  
  <div class="salt-shaker">🧂</div>
  
  <div class="hono-salt salt-1"></div>
  <div class="hono-salt salt-2"></div>
  <div class="hono-salt salt-3"></div>
  <div class="hono-salt salt-4"></div>
  <div class="hono-salt salt-5"></div>
  <div class="hono-salt salt-6"></div>
  <div class="hono-salt salt-7"></div>
  <div class="hono-salt salt-8"></div>
  
  <div class="title-text">
    Just add Hono.js for that perfect flavor!
  </div>
</div>

<!--
Just like the famous salt meme, the solution to Cloudflare Workers complexity is simple: just add Hono.js! It provides the perfect flavor to make development easier and more enjoyable.
-->

---
layout: center
class: text-center
---

<style scoped>
.triangle-container {
  position: relative;
  width: 100%;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.triangle-point {
  position: absolute;
  width: 120px;
  height: 120px;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: white;
  color: black;
  font-weight: bold;
  font-size: 0.9rem;
  animation: pointPulse 3s ease-in-out infinite;
}

.triangle-point.workers {
  top: 50px;
  padding: 2rem;
  animation-delay: 0s;
}

.triangle-point.hono {
  bottom: 100px;
  left: 400px;
  padding: 2.2rem;
  animation-delay: 0.5s;
}

.triangle-point.mcp {
  bottom: 100px;
  right: 400px;
  padding: 2rem;
  animation-delay: 1s;
}

.triangle-line {
  position: absolute;
  height: 3px;
  background: linear-gradient(90deg, rgba(255,255,255,0.3), rgba(255,255,255,0.6), rgba(255,255,255,0.3));
  animation: lineGlow 2s ease-in-out infinite alternate;
}

.line-1 {
  width: 220px;
  top: 190px;
  left: 230px;
  transform: rotate(40deg);
}

.line-2 {
  width: 220px;
  top: 190px;
  right: 230px;
  transform: rotate(-40deg);
}

.line-3 {
  width: 400px;
  bottom: 160px;
  left: 50%;
  transform: translateX(-50%);
}

.center-reveal {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: rgba(255, 255, 255, 0.1);
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 16px;
  padding: 1.5rem 2rem;
  font-size: 1.2rem;
  font-weight: bold;
  color: white;
  opacity: 0;
  transform: translate(-50%, -50%) scale(0);
  animation: centerReveal 0.8s ease-out forwards;
}

@keyframes pointPulse {
  0%, 100% { transform: scale(1); box-shadow: 0 0 0 0 rgba(255,255,255,0.4); }
  50% { transform: scale(1.05); box-shadow: 0 0 0 20px rgba(255,255,255,0); }
}

@keyframes lineGlow {
  0% { opacity: 0.3; }
  100% { opacity: 0.8; }
}

@keyframes centerReveal {
  to {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }
}
</style>

## The Perfect Triangle

<div class="triangle-container">
  <div class="triangle-point workers">
    <img src="/cloudflare_workers_logo.png" alt="Cloudflare Workers Logo" />
    Workers
  </div>
  
  <div class="triangle-point hono">
    <img src="/hono_logo.svg" alt="Hono.js Logo" />
    Hono.js
  </div>
  
  <div class="triangle-point mcp">
    <img src="/mcp.svg" alt="MCP Logo" class="w-full" />
    MCP
  </div>
  
  <div class="triangle-line line-1"></div>
  <div class="triangle-line line-2"></div>
  <div class="triangle-line line-3"></div>
  
  <div v-click class="center-reveal">
    @hono/mcp
  </div>
</div>

<!--
Here's the perfect triangle: Cloudflare Workers, Hono.js, and MCP. Click to reveal the missing piece that connects them all - the @hono/mcp library!
-->

---
layout: center
---

<Tweet id="1924648575541379110" />

---
layout: two-cols
class: p-1
---

```typescript {all|6-10|11-22|24|all}
// mcp.ts

import { MCPServer } from '@modelcontextprotocol/sdk/server/mcp.js'
import z from "zod";

const mcpServer = new MCPServer({
  name: 'my-mcp-server',
  version: '1.0.0'
})

mcpServer.tool("Simple Hello World", {
  name: z.string().default("world")
}, (params) => {
  return {
    content: [
      {
        type: "text",
        text: `Hello, ${params.name}!`,
      },
    ],
  }
})

export default mcpServer
```

::right::

```typescript {all|3|4|5|7|9-13|15|all}
// index.ts

import { Hono } from 'hono'
import mcpServer from './mcp'
import { StreamableHTTPHonoTransport } from "@hono/mcp"

const app = new Hono()

app.all("/mcp", async (c) => {
  const transport = new StreamableHTTPHonoTransport();
  await mcpServer.connect(transport);
  return transport.handleRequest(c);
});

export default app
```

<!--
Here's how the three technologies work together in code. We start with basic Hono setup, add MCP server integration, and combine them for AI-powered edge functions.
-->

---
layout: center
class: text-center
---

<style scoped>
.demo-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}

.demo-text {
  font-size: 4rem;
  font-weight: bold;
  background: linear-gradient(135deg, var(--cloudflare-orange), var(--hono-red), var(--tech-blue));
  background-size: 300% 300%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: demoGradient 3s ease infinite;
}

.demo-subtitle {
  font-size: 1.5rem;
  color: #gray-400;
  animation: subtitlePulse 2s ease-in-out infinite;
}

.tech-bg {
  position: fixed;
  inset: 0;
  background: radial-gradient(circle at 20% 50%, rgba(248, 128, 32, 0.1) 0%, transparent 50%),
              radial-gradient(circle at 80% 20%, rgba(227, 96, 2, 0.1) 0%, transparent 50%),
              radial-gradient(circle at 40% 80%, rgba(37, 99, 235, 0.1) 0%, transparent 50%);
  animation: techFlow 8s ease-in-out infinite;
  z-index: -1;
}

@keyframes demoGradient {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

@keyframes subtitlePulse {
  0%, 100% { opacity: 0.7; transform: scale(1); }
  50% { opacity: 1; transform: scale(1.05); }
}

@keyframes techFlow {
  0%, 100% { opacity: 0.3; }
  50% { opacity: 0.6; }
}
</style>

<div class="demo-container">
  <div class="tech-bg"></div>
  <div class="demo-text">DEMO</div>
  <div class="demo-subtitle">Let's see it in action!</div>
  
  <div class="mt-8 flex gap-4">
    <carbon:play-filled class="text-4xl text-green-400 animate-pulse" />
    <carbon:code class="text-4xl text-blue-400 animate-bounce" />
    <carbon:cloud class="text-4xl text-orange-400 animate-pulse" />
  </div>
</div>

<!--
Now for the exciting part - let's see this powerful combination in action with a live demo!
-->

---
layout: center
class: text-center
---

<style scoped>
.thank-you-container {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
  z-index: 10;
}

.main-title {
  font-size: 4rem;
  font-weight: bold;
  background: linear-gradient(135deg, var(--cloudflare-orange), var(--hono-red));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: titleShine 2s ease-in-out infinite alternate;
}

.subtitle {
  font-size: 1.5rem;
  color: #gray-300;
  margin-bottom: 1rem;
}

.social-links-final {
  display: flex;
  gap: 2rem;
  margin: 1rem 0;
}

.social-link-final {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  border-radius: 0.75rem;
  background: rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
  animation: socialFloat 3s ease-in-out infinite;
}

.social-link-final:nth-child(1) { animation-delay: 0s; }
.social-link-final:nth-child(2) { animation-delay: 0.5s; }
.social-link-final:nth-child(3) { animation-delay: 1s; }

.social-link-final:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: translateY(-4px) scale(1.05);
}

.closing-message {
  font-size: 1.2rem;
  color: #gray-400;
  text-align: center;
  max-width: 600px;
}

.confetti {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 1;
}

.confetti-piece {
  position: absolute;
  width: 10px;
  height: 10px;
  animation: confettiFall 3s linear infinite;
}

@keyframes titleShine {
  0% { filter: brightness(1); }
  100% { filter: brightness(1.2); }
}

@keyframes socialFloat {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-5px); }
}

@keyframes confettiFall {
  0% {
    transform: translateY(-100vh) rotate(0deg);
    opacity: 1;
  }
  100% {
    transform: translateY(100vh) rotate(720deg);
    opacity: 0;
  }
}

/* Generate confetti pieces */
.confetti-1 { left: 10%; background: var(--cloudflare-orange); animation-delay: 0s; }
.confetti-2 { left: 20%; background: var(--hono-red); animation-delay: 0.2s; }
.confetti-3 { left: 30%; background: var(--tech-blue); animation-delay: 0.4s; }
.confetti-4 { left: 40%; background: var(--cloudflare-orange); animation-delay: 0.6s; }
.confetti-5 { left: 50%; background: var(--hono-red); animation-delay: 0.8s; }
.confetti-6 { left: 60%; background: var(--tech-blue); animation-delay: 1s; }
.confetti-7 { left: 70%; background: var(--cloudflare-orange); animation-delay: 1.2s; }
.confetti-8 { left: 80%; background: var(--hono-red); animation-delay: 1.4s; }
.confetti-9 { left: 90%; background: var(--tech-blue); animation-delay: 1.6s; }
</style>

<div class="thank-you-container">
  <div class="confetti">
    <div class="confetti-piece confetti-1"></div>
    <div class="confetti-piece confetti-2"></div>
    <div class="confetti-piece confetti-3"></div>
    <div class="confetti-piece confetti-4"></div>
    <div class="confetti-piece confetti-5"></div>
    <div class="confetti-piece confetti-6"></div>
    <div class="confetti-piece confetti-7"></div>
    <div class="confetti-piece confetti-8"></div>
    <div class="confetti-piece confetti-9"></div>
  </div>
  
  <div class="main-title">Thank You!</div>
  
  <div class="subtitle">Questions & Discussion</div>
  
  <div class="social-links-final">
    <a href="https://github.com/mathuraditya724" class="social-link-final">
      <carbon:logo-github class="text-xl" />
      @mathuraditya724
    </a>
    <a href="https://x.com/mathurAditya7" class="social-link-final">
      <carbon:logo-x class="text-xl" />
      @mathuraditya7
    </a>
    <a href="https://bsky.app/profile/adima7.bsky.social" class="social-link-final">
      <bi:bluesky class="text-xl" />
      @adima7.bsky.social
    </a>
  </div>
  
  <div class="closing-message">
    Let's connect and build amazing things together!
  </div>
  
  <div class="flex gap-4 mt-4">
    <carbon:partnership class="text-3xl text-orange-400" />
    <carbon:rocket class="text-3xl text-red-400" />
    <carbon:cloud-satellite class="text-3xl text-blue-400" />
  </div>
</div>

<!--
Thank you for your attention! I hope this presentation has shown you the exciting possibilities when combining Hono.js, MCP, and Cloudflare Workers. Let's discuss and build amazing things together!
-->