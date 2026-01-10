---
theme: default
title: Building MCPs with Cloudflare using Hono
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
colorSchema: dark
fonts:
  sans: Inter
  mono: Fira Code
---

<style>
@import './style.css';

:root {
  --sentry-purple-dark: #362D59;
  --sentry-purple: #6C5FC7;
  --sentry-purple-light: #8B7FD4;
  --sentry-pink: #FA4E89;
}

/* Override code block background globally */
.slidev-code {
  background: rgba(0, 0, 0, 0.85) !important;
}

.title-massive {
  font-size: 4.5rem;
  font-weight: 900;
  letter-spacing: -0.05em;
  line-height: 1.1;
  background: linear-gradient(135deg, #ffffff 0%, #ffffff 40%, #FF6B9D 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  filter: drop-shadow(0 4px 20px rgba(0, 0, 0, 0.5));
}
</style>

<div class="relative z-10 flex flex-col items-center justify-center h-full" style="padding-top: 12vh;">

<div class="title-massive mb-8">
  Building MCPs with<br/>Cloudflare using Hono
</div>

</div>

---
layout: two-cols
---

<style scoped>
.speaker-hero {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  padding: 3rem 0;
}

.speaker-photo {
  width: 180px;
  height: 180px;
  border-radius: 50%;
  border: 4px solid var(--sentry-pink);
  box-shadow: 0 0 40px rgba(250, 78, 137, 0.3);
  animation: photoReveal 0.8s ease-out;
}

.speaker-name {
  font-size: 3rem;
  font-weight: 900;
  letter-spacing: -0.02em;
  background: linear-gradient(135deg, #ffffff 0%, #ffffff 50%, #FF6B9D 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  filter: drop-shadow(0 2px 10px rgba(0, 0, 0, 0.4));
  animation: fadeInUp 0.8s ease-out 0.2s both;
}

.speaker-title {
  font-size: 1.3rem;
  color: rgba(255, 255, 255, 0.7);
  font-weight: 300;
  animation: fadeInUp 0.8s ease-out 0.4s both;
}

.right-content {
  display: flex;
  flex-direction: column;
  height: 100%;
  gap: 2rem;
  padding-left: 3rem;
  justify-content: center;
}

.tagline {
  font-size: 2.2rem;
  font-weight: 700;
  line-height: 1.2;
  color: rgba(255, 255, 255, 0.95);
  animation: fadeInUp 0.8s ease-out 0.6s both;
}

.tagline-highlight {
  color: #FF6B9D;
  font-weight: 900;
}

.bio-text {
  font-size: 1.1rem;
  line-height: 1.6;
  color: rgba(255, 255, 255, 0.7);
  animation: fadeInUp 0.8s ease-out 0.8s both;
}

.social-footer {
  display: flex;
  gap: 1rem;
  margin-top: 1rem;
  animation: fadeInUp 0.8s ease-out 1s both;
}

.social-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.5);
  padding: 0.5rem 1rem;
  border-radius: 0.5rem;
  background: rgba(255, 255, 255, 0.05);
  transition: all 0.3s ease;
}

.social-link:hover {
  color: var(--sentry-pink);
  background: rgba(250, 78, 137, 0.1);
  transform: translateY(-2px);
}

@keyframes photoReveal {
  from { opacity: 0; transform: scale(0.8); }
  to { opacity: 1; transform: scale(1); }
}

@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>

<div class="speaker-hero">
  <img src="https://avatars.githubusercontent.com/u/57684218?v=4" alt="Aditya Mathur" class="speaker-photo" />
  
  <div>
    <div class="speaker-name">Aditya Mathur</div>
    <div class="speaker-title">Member of Technical Staff @Sentry</div>
  </div>
  
  <div class="social-footer">
    <a href="https://github.com/mathuraditya724" class="social-link">
      <carbon:logo-github />
      mathuraditya724
    </a>
    <a href="https://x.com/mathurAditya7" class="social-link">
      <carbon:logo-x />
      mathuraditya7
    </a>
    <a href="https://bsky.app/profile/maditya.sh" class="social-link">
      <bi:bluesky />
      maditya.sh
    </a>
  </div>
</div>

::right::

<div class="right-content">
  <div class="tagline">
    Creating bugs for <span class="tagline-highlight">LLMs</span> to fix
  </div>
  
  <div class="bio-text">
    Currently working on Spotlightjs, and other crazy ideas now and then.<br/><br/>
    You might know me from <code>@hono/mcp</code>, <code>muppet</code>, <code>hono-openapi</code>, <code>hono-rate-limiter</code>, etc.
  </div>
</div>

---

<style scoped>
.mcp-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  height: 100%;
  gap: 2rem;
  padding: 0 4rem;
}

.question {
  font-size: 1.5rem;
  color: rgba(255, 255, 255, 0.6);
  font-weight: 300;
  animation: fadeInUp 0.8s ease-out 0.2s both;
}

.answer {
  font-size: 2.5rem;
  font-weight: 700;
  line-height: 1.3;
  color: rgba(255, 255, 255, 0.95);
  animation: fadeInUp 0.8s ease-out 0.4s both;
}

.highlight {
  color: #FF6B9D;
  font-weight: 900;
}

@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>

<div class="mcp-content">
  <div class="question">What is MCP?</div>
  <div class="answer">
    It's just a <span class="highlight">Server</span>, which can connect<br/>
    <span class="highlight">LLMs</span> with <span class="highlight">External Apps</span>
  </div>
</div>

---

<style scoped>
.slide-title {
  font-size: 1.8rem;
  font-weight: 700;
  color: #ffffff;
  margin-bottom: 1rem;
  text-align: center;
  filter: drop-shadow(0 2px 8px rgba(0, 0, 0, 0.5));
}

.file-badge {
  display: inline-block;
  background: rgba(0, 0, 0, 0.9);
  color: #FF6B9D;
  padding: 0.35rem 1rem;
  border-radius: 0.5rem;
  font-size: 0.9rem;
  font-family: 'Fira Code', monospace;
  margin-bottom: 1rem;
  border: 1px solid rgba(255, 107, 157, 0.3);
}
</style>

<div class="slide-title">Defining the MCP Server</div>

```typescript
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { CallToolResult } from "@modelcontextprotocol/sdk/types.js";
import { z } from "zod";

const server = new McpServer({ name: "sample-mcp", version: "1.0.0" });

server.registerTool(
  "greet",
  {
    title: "Greeting Tool",
    description: "A simple greeting tool",
    inputSchema: { name: z.string().describe("Name to greet") },
  },
  async ({ name }): Promise<CallToolResult> => {
    return {
      content: [{ type: "text", text: `Hello, ${name}!` }],
    };
  }
);

export default server;
```

---

<style scoped>
.slide-title {
  font-size: 1.8rem;
  font-weight: 700;
  color: #ffffff;
  margin-bottom: 1rem;
  text-align: center;
  filter: drop-shadow(0 2px 8px rgba(0, 0, 0, 0.5));
}

.file-badge {
  display: inline-block;
  background: rgba(0, 0, 0, 0.9);
  color: #FF6B9D;
  padding: 0.35rem 1rem;
  border-radius: 0.5rem;
  font-size: 0.9rem;
  font-family: 'Fira Code', monospace;
  margin-bottom: 1rem;
  border: 1px solid rgba(255, 107, 157, 0.3);
}
</style>

<div class="slide-title">Exposing via Hono</div>

```typescript {all}
import { Hono } from "hono";
import { WebStandardStreamableHTTPServerTransport } from 
  "@modelcontextprotocol/sdk/server/webStandardStreamableHttp.js";
import mcp from "./mcp.js";
import { cors } from "hono/cors";

const transport = new WebStandardStreamableHTTPServerTransport();

const app = new Hono().use(cors());

app.all("/mcp", async (c) => {
  if (!mcp.isConnected()) {
    await mcp.connect(transport);
  }
  return transport.handleRequest(c.req.raw);
});

export default app;
```

---

<style scoped>
.capabilities-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  gap: 2rem;
}

.slide-title {
  font-size: 2.2rem;
  font-weight: 800;
  color: #ffffff;
  filter: drop-shadow(0 2px 10px rgba(0, 0, 0, 0.5));
}

.cards-grid {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 1rem;
  width: 100%;
  max-width: 900px;
}

.capability-card {
  background: rgba(54, 45, 89, 0.4);
  backdrop-filter: blur(12px);
  border: 1px solid rgba(139, 127, 212, 0.2);
  border-radius: 1rem;
  padding: 1.5rem 1rem;
  text-align: center;
  transition: all 0.3s ease;
}

.capability-card:hover {
  transform: translateY(-5px);
  border-color: var(--sentry-pink);
  box-shadow: 0 10px 30px rgba(250, 78, 137, 0.2);
}

.card-icon {
  font-size: 2rem;
  margin-bottom: 0.75rem;
}

.card-title {
  font-size: 1rem;
  font-weight: 700;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 0.5rem;
}

.card-desc {
  font-size: 0.7rem;
  color: rgba(255, 255, 255, 0.6);
  line-height: 1.4;
}

.card-1 { animation: fadeInUp 0.5s ease-out 0.1s both; }
.card-2 { animation: fadeInUp 0.5s ease-out 0.2s both; }
.card-3 { animation: fadeInUp 0.5s ease-out 0.3s both; }
.card-4 { animation: fadeInUp 0.5s ease-out 0.4s both; }
.card-5 { animation: fadeInUp 0.5s ease-out 0.5s both; }

@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>

<div class="capabilities-container">
  <div class="slide-title">MCP Capabilities</div>
  
  <div class="cards-grid">
    <div class="capability-card card-1">
      <div class="card-icon"><carbon:tool-box /></div>
      <div class="card-title">Tools</div>
      <div class="card-desc">Functions the LLM can call</div>
    </div>
    <div class="capability-card card-2">
      <div class="card-icon"><carbon:folder /></div>
      <div class="card-title">Resources</div>
      <div class="card-desc">Data/files the LLM can access</div>
    </div>
    <div class="capability-card card-3">
      <div class="card-icon"><carbon:chat /></div>
      <div class="card-title">Prompts</div>
      <div class="card-desc">Pre-defined prompt templates</div>
    </div>
    <div class="capability-card card-4">
      <div class="card-icon"><carbon:data-vis-1 /></div>
      <div class="card-title">Sampling</div>
      <div class="card-desc">Request LLM completions</div>
    </div>
    <div class="capability-card card-5">
      <div class="card-icon"><carbon:user-speaker /></div>
      <div class="card-title">Elicitation</div>
      <div class="card-desc">Request user input</div>
    </div>
  </div>
</div>

---

<style scoped>
.slide-title {
  font-size: 1.8rem;
  font-weight: 700;
  color: #ffffff;
  margin-bottom: 1rem;
  text-align: center;
  filter: drop-shadow(0 2px 8px rgba(0, 0, 0, 0.5));
}

.subtitle {
  font-size: 1rem;
  color: rgba(255, 255, 255, 0.7);
  text-align: center;
  margin-bottom: 1rem;
}
</style>

<div class="slide-title">OAuth with MCP Spec</div>

```typescript {all}
import { simpleMcpAuthRouter } from '@hono/mcp'

app.route(
  '/',
  simpleMcpAuthRouter({
    issuer: '[auth provider domain]',
    resourceServerUrl: new URL('https://your-worker.dev/mcp'),
  })
)
```

---

<style scoped>
.cool-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  gap: 1.5rem;
}

.cool-title {
  font-size: 3.5rem;
  font-weight: 900;
  color: #ffffff;
  text-align: center;
  filter: drop-shadow(0 4px 20px rgba(0, 0, 0, 0.6));
  line-height: 1.2;
}

.cool-subtitle {
  font-size: 1.5rem;
  color: #FF6B9D;
  font-weight: 600;
  text-align: center;
}

.cool-image {
  max-width: 450px;
  max-height: 300px;
  border-radius: 1rem;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
  border: 2px solid rgba(255, 107, 157, 0.3);
}
</style>

<div class="cool-container">
  <div class="cool-title">Congrats!</div>
  <div class="cool-subtitle">You are now part of the cool kids</div>
</div>

---

<style scoped>
.clients-container {
  display: flex;
  flex-direction: column;
  height: 100%;
  padding: 1rem 2rem;
}

.slide-title {
  font-size: 2.2rem;
  font-weight: 800;
  color: #ffffff;
  text-align: center;
  margin-bottom: 1.5rem;
  filter: drop-shadow(0 2px 10px rgba(0, 0, 0, 0.5));
}

.key-message {
  font-size: 1.2rem;
  color: rgba(255, 255, 255, 0.8);
  text-align: center;
  margin-bottom: 1.5rem;
  line-height: 1.5;
}

.highlight {
  color: var(--sentry-pink);
  font-weight: 600;
}

.points-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  margin-bottom: 1.5rem;
}

.point {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  font-size: 1rem;
  color: rgba(255, 255, 255, 0.8);
}

.point-icon {
  color: var(--sentry-purple-light);
  font-size: 1.2rem;
}

.logos-row {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-top: auto;
}

.logo-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
}

.logo-img {
  width: 60px;
  height: 60px;
  object-fit: contain;
}

.logo-label {
  font-size: 0.75rem;
  color: rgba(255, 255, 255, 0.7);
  text-align: center;
}
</style>

<div class="clients-container">
  <div class="slide-title">MCP Clients</div>
  
  <div class="key-message">
    MCP is <span class="highlight">not just the server</span> — a lot depends on the<br/>
    <span class="highlight">MCP client</span> used by your user
  </div>
  
  <div class="points-list">
    <div class="point">
      <span class="point-icon"><carbon:arrow-right /></span>
      MCP Inspector lets you test all the latest features
    </div>
    <div class="point">
      <span class="point-icon"><carbon:warning-alt /></span>
      But this might not be how your client will use it
    </div>
    <div class="point">
      <span class="point-icon"><carbon:list-checked /></span>
      Rule of thumb: Most clients support Tools, Resources, Prompts
    </div>
    <div class="point">
      <span class="point-icon"><carbon:tool-box /></span>
      Almost all clients <strong>just support Tools</strong>
    </div>
  </div>
  
  <div class="logos-row">
    <div class="logo-item">
      <img src="/mcp.png" alt="MCP Inspector" class="logo-img" />
      <span class="logo-label">MCP Inspector</span>
    </div>
    <div class="logo-item">
      <img src="/muppet.png" alt="Muppet" class="logo-img" />
      <span class="logo-label">Muppet</span>
    </div>
    <div class="logo-item">
      <img src="/mcpjam.webp" alt="MCP Jam" class="logo-img" />
      <span class="logo-label">MCP Jam</span>
    </div>
  </div>
</div>

---

<style scoped>
.bloat-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  gap: 1.5rem;
}

.slide-title {
  font-size: 2.5rem;
  font-weight: 800;
  color: #ffffff;
  filter: drop-shadow(0 2px 10px rgba(0, 0, 0, 0.5));
}

.diamond-container {
  position: relative;
  width: 400px;
  height: 400px;
}

.diamond-point {
  position: absolute;
  background: rgba(54, 45, 89, 0.6);
  backdrop-filter: blur(8px);
  border: 1px solid rgba(139, 127, 212, 0.3);
  border-radius: 0.75rem;
  padding: 0.75rem 1rem;
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.9);
  text-align: center;
  max-width: 140px;
}

.point-top {
  top: 0;
  left: 50%;
  transform: translateX(-50%);
}

.point-bottom {
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
}

.point-left {
  top: 50%;
  left: 0;
  transform: translateY(-50%);
}

.point-right {
  top: 50%;
  right: 0;
  transform: translateY(-50%);
}

.center-dot {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 20px;
  height: 20px;
  background: linear-gradient(135deg, var(--sentry-purple) 0%, var(--sentry-pink) 100%);
  border-radius: 50%;
  box-shadow: 0 0 30px rgba(250, 78, 137, 0.6);
  animation: pulse 2s ease-in-out infinite;
}

.center-label {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, 20px);
  font-size: 0.8rem;
  color: var(--sentry-pink);
  font-weight: 600;
}

.diamond-lines {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 280px;
  height: 280px;
  border: 2px solid rgba(139, 127, 212, 0.2);
  transform: translate(-50%, -50%) rotate(45deg);
}

@keyframes pulse {
  0%, 100% { transform: translate(-50%, -50%) scale(1); }
  50% { transform: translate(-50%, -50%) scale(1.2); }
}

.message {
  font-size: 1.1rem;
  color: rgba(255, 255, 255, 0.7);
  text-align: center;
  max-width: 600px;
}
</style>

<div class="bloat-container">
  <div class="slide-title">Context Bloat</div>
  
  <div class="diamond-container">
    <div class="diamond-lines"></div>
    <div class="diamond-point point-top">Too little context</div>
    <div class="diamond-point point-bottom">Too much context</div>
    <div class="diamond-point point-left">Actual info is quite less</div>
    <div class="diamond-point point-right">Info is quite too much</div>
    <div class="center-dot"></div>
    <div class="center-label">Balance</div>
  </div>
  
  <div class="message">
    Balancing all these is difficult depending on what MCP you're building
  </div>
</div>

---

<style scoped>
.code-mode-container {
  display: flex;
  flex-direction: column;
  height: 100%;
  padding: 1rem 2rem;
}

.slide-title {
  font-size: 2.5rem;
  font-weight: 900;
  color: #ffffff;
  text-align: center;
  margin-bottom: 1rem;
  filter: drop-shadow(0 2px 10px rgba(0, 0, 0, 0.5));
}

.images-row {
  display: flex;
  justify-content: center;
  gap: 2rem;
  flex: 1;
  align-items: center;
  width: 100%;
  max-width: 900px;
  margin: 0 auto;
}

.article-card {
  background: rgba(54, 45, 89, 0.4);
  backdrop-filter: blur(12px);
  border: 1px solid rgba(139, 127, 212, 0.2);
  overflow: hidden;
  transition: all 0.3s ease;
  flex: 1;
  max-width: 400px;
}

.article-card:hover {
  transform: translateY(-5px);
  border-color: var(--sentry-pink);
}

.article-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.article-link {
  display: block;
  padding: 1rem;
  font-size: 0.8rem;
  color: var(--sentry-purple-light);
  text-align: center;
  word-break: break-all;
}
</style>

<div class="code-mode-container">
  <div class="slide-title">Code Mode / Sandbox</div>
  
  <div class="images-row">
    <div class="article-card">
      <img src="/anthropic-code-execution.png" alt="Anthropic Code Execution" class="article-image" />
      <a href="https://www.anthropic.com/engineering/code-execution-with-mcp" class="article-link" target="_blank">
        anthropic.com/engineering/code-execution-with-mcp
      </a>
    </div>
    <div class="article-card">
      <img src="/cloudflare-code-mode.png" alt="Cloudflare Code Mode" class="article-image" />
      <a href="https://blog.cloudflare.com/code-mode/" class="article-link" target="_blank">
        blog.cloudflare.com/code-mode/
      </a>
    </div>
  </div>
</div>

---

<style scoped>
.alternatives-container {
  display: flex;
  flex-direction: column;
  height: 100%;
  padding: 1rem 2rem;
}

.slide-title {
  font-size: 2.5rem;
  font-weight: 900;
  color: #ffffff;
  text-align: center;
  margin-bottom: 2rem;
  filter: drop-shadow(0 2px 10px rgba(0, 0, 0, 0.5));
}

.columns {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  flex: 1;
}

.column {
  display: flex;
  flex-direction: column;
}

.section-title {
  font-size: 1.6rem;
  font-weight: 700;
  color: #FF6B9D;
  margin-bottom: 1.5rem;
}

.section-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.list-item {
  font-size: 0.95rem;
  color: rgba(255, 255, 255, 0.85);
  line-height: 1.5;
  padding-left: 1rem;
  border-left: 3px solid rgba(139, 127, 212, 0.5);
}

.code-inline {
  background: rgba(0, 0, 0, 0.6);
  padding: 0.15rem 0.4rem;
  border-radius: 0.25rem;
  font-family: 'Fira Code', monospace;
  font-size: 0.85em;
  color: #FF6B9D;
}
</style>

<div class="alternatives-container">
  <div class="slide-title">Alternatives</div>
  
  <div class="columns">
    <div class="column">
      <div class="section-title">🧠 Agent Skills</div>
      <div class="section-list">
        <div class="list-item">Modular capabilities that extend Claude's functionality</div>
        <div class="list-item">Skills package instructions, metadata, and resources</div>
        <div class="list-item">Progressive disclosure: loads on-demand, not upfront</div>
        <div class="list-item">Filesystem-based: <span class="code-inline">SKILL.md</span> with YAML frontmatter</div>
        <div class="list-item">Works in Claude API, Claude Code, Claude.ai</div>
      </div>
    </div>
    <div class="column">
      <div class="section-title">💻 CLI</div>
      <div class="section-list">
        <div class="list-item">The <span class="code-inline">--help</span> menu acts as context for agents</div>
        <div class="list-item">Agent can use <span class="code-inline">--help</span> to understand available actions</div>
        <div class="list-item">Self-documenting interface</div>
        <div class="list-item">No separate protocol needed</div>
      </div>
    </div>
  </div>
</div>

---

<style scoped>
.question-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
}

.question-title {
  font-size: 3.5rem;
  font-weight: 900;
  color: #ffffff;
  text-align: center;
  line-height: 1.2;
  filter: drop-shadow(0 4px 15px rgba(0, 0, 0, 0.6));
}
</style>

<div class="question-container">
  <div class="question-title">So should we<br/>build/use MCPs?</div>
</div>

---

<style scoped>
.sentry-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  gap: 2.5rem;
  padding: 2rem 3rem;
}

.sentry-title {
  font-size: 3.5rem;
  font-weight: 900;
  color: #ffffff;
  filter: drop-shadow(0 4px 15px rgba(0, 0, 0, 0.6));
}

.stats-layout {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: 3rem;
  width: 100%;
  max-width: 900px;
  align-items: start;
}

.highlight-stats {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.big-stat {
  background: rgba(0, 0, 0, 0.6);
  border-left: 4px solid #FF6B9D;
  padding: 1.25rem 1.5rem;
}

.big-stat-value {
  font-size: 3rem;
  font-weight: 900;
  color: #FF6B9D;
  line-height: 1;
}

.big-stat-label {
  font-size: 1rem;
  color: rgba(255, 255, 255, 0.9);
  margin-top: 0.5rem;
}

.big-stat-sublabel {
  font-size: 0.8rem;
  color: rgba(255, 255, 255, 0.5);
  font-family: 'Fira Code', monospace;
  margin-top: 0.25rem;
}

.tools-section {
  background: rgba(0, 0, 0, 0.4);
  padding: 1.25rem;
}

.tools-header {
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.5);
  text-transform: uppercase;
  letter-spacing: 0.1em;
  margin-bottom: 1rem;
  padding-bottom: 0.5rem;
  border-bottom: 1px solid rgba(139, 127, 212, 0.2);
}

.tool-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.75rem 0;
  border-bottom: 1px solid rgba(139, 127, 212, 0.1);
}

.tool-row:last-child {
  border-bottom: none;
}

.tool-rank {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.4);
  width: 1.5rem;
}

.tool-name {
  flex: 1;
  font-family: 'Fira Code', monospace;
  font-size: 0.95rem;
  color: #FF6B9D;
}

.tool-calls {
  font-size: 1.1rem;
  font-weight: 700;
  color: rgba(255, 255, 255, 0.9);
}

.metrics-footnote {
  font-size: 0.8rem;
  color: rgba(255, 255, 255, 0.4);
  font-style: italic;
}
</style>

<div class="sentry-container">
  <div class="sentry-title">Sentry MCP</div>
  
  <div class="stats-layout">
    <div class="highlight-stats">
      <div class="big-stat">
        <div class="big-stat-value">3M+</div>
        <div class="big-stat-label">Total Requests</div>
      </div>
      <div class="big-stat">
        <div class="big-stat-value">439K</div>
        <div class="big-stat-label">Top Client</div>
        <div class="big-stat-sublabel">claude-code</div>
      </div>
    </div>
    <div class="tools-section">
      <div class="tools-header">Top Tools</div>
      <div class="tool-row">
        <span class="tool-rank">1</span>
        <span class="tool-name">get_issue_details</span>
        <span class="tool-calls">66K</span>
      </div>
      <div class="tool-row">
        <span class="tool-rank">2</span>
        <span class="tool-name">search_issues</span>
        <span class="tool-calls">55K</span>
      </div>
      <div class="tool-row">
        <span class="tool-rank">3</span>
        <span class="tool-name">search_events</span>
        <span class="tool-calls">38K</span>
      </div>
    </div>
  </div>
  
  <div class="metrics-footnote">Based on metrics from the last 30 days</div>
</div>

---

<style scoped>
.thank-you-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  text-align: center;
  padding: 2rem;
}

.thank-you-title {
  font-size: 4rem;
  font-weight: 900;
  letter-spacing: -0.03em;
  color: #ffffff;
  margin-bottom: 1.5rem;
  filter: drop-shadow(0 4px 15px rgba(0, 0, 0, 0.6));
}

.slides-link {
  font-size: 1.2rem;
  color: #FF6B9D;
  font-weight: 500;
  margin-bottom: 2rem;
  font-family: 'Fira Code', monospace;
}

.social-links-final {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
  flex-wrap: wrap;
}

.social-link-final {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  background: rgba(255, 255, 255, 0.05);
  border: 2px solid rgba(255, 255, 255, 0.2);
  border-radius: 0.75rem;
  font-size: 1rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.9);
  transition: all 0.3s ease;
}

.social-link-final:hover {
  background: rgba(108, 95, 199, 0.2);
  border-color: var(--sentry-purple);
  transform: translateY(-3px);
}

.social-icon-final {
  font-size: 1.25rem;
  color: var(--sentry-purple-light);
}
</style>

<div class="thank-you-container">
  <div class="thank-you-title">Thank You Everyone!</div>
  
  <div class="slides-link">maditya.sh/talks</div>

  <div class="social-links-final">
    <a href="https://github.com/mathuraditya724" class="social-link-final">
      <carbon:logo-github class="social-icon-final" />
      mathuraditya724
    </a>
    <a href="https://x.com/mathurAditya7" class="social-link-final">
      <carbon:logo-x class="social-icon-final" />
      @mathuraditya7
    </a>
    <a href="https://bsky.app/profile/maditya.sh" class="social-link-final">
      <bi:bluesky class="social-icon-final" />
      maditya.sh
    </a>
  </div>
</div>
