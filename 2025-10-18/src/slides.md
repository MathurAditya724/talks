---
theme: default
title: Hono x MCP
info: |
  ## Hono x MCP
  The New Frontier
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
  --hono-red: #E36002;
}

.title-massive {
  font-size: 7rem;
  font-weight: 900;
  letter-spacing: -0.05em;
  line-height: 0.95;
  background: linear-gradient(135deg, #ffffff 0%, var(--hono-red) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: title-glow 3s ease-in-out infinite;
}

@keyframes title-glow {
  0%, 100% { filter: drop-shadow(0 0 20px rgba(227, 96, 2, 0.3)); }
  50% { filter: drop-shadow(0 0 40px rgba(227, 96, 2, 0.5)); }
}

.subtitle-impact {
  font-size: 2.5rem;
  font-weight: 300;
  letter-spacing: 0.02em;
  color: rgba(255, 255, 255, 0.9);
}
</style>

<div class="relative z-10 flex flex-col items-center justify-center h-full" style="padding-top: 8vh;">

<div class="title-massive mb-12">
  Hono x MCP
</div>

<div class="subtitle-impact mb-16">
  The default platform for MCPs
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
  width: 200px;
  height: 200px;
  border-radius: 50%;
  border: 4px solid var(--hono-red);
  box-shadow: 0 0 40px rgba(227, 96, 2, 0.3);
  animation: photoReveal 0.8s ease-out;
}

.speaker-name {
  font-size: 3.5rem;
  font-weight: 900;
  letter-spacing: -0.02em;
  background: linear-gradient(135deg, #ffffff 0%, var(--hono-red) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: fadeInUp 0.8s ease-out 0.2s both;
}

.speaker-title {
  font-size: 1.5rem;
  color: rgba(255, 255, 255, 0.7);
  font-weight: 300;
  animation: fadeInUp 0.8s ease-out 0.4s both;
}

.right-content {
  display: flex;
  flex-direction: column;
  height: 100%;
  gap: 3rem;
  padding-left: 4rem;
}

.tagline {
  font-size: 3rem;
  font-weight: 700;
  line-height: 1.2;
  color: rgba(255, 255, 255, 0.95);
  animation: fadeInUp 0.8s ease-out 0.6s both;
}

.tagline-highlight {
  background: -webkit-linear-gradient(135deg, #ffffff 0%, var(--hono-red) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-weight: 900;
}

.bio-text {
  font-size: 1.25rem;
  line-height: 1.6;
  color: rgba(255, 255, 255, 0.7);
  animation: fadeInUp 0.8s ease-out 0.8s both;
}

.social-footer {
  display: flex;
  gap: 1.5rem;
  margin-top: 2rem;
  animation: fadeInUp 0.8s ease-out 1.2s both;
}

.social-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.875rem;
  color: rgba(255, 255, 255, 0.5);
  padding: 0.5rem 1rem;
  border-radius: 0.5rem;
  background: rgba(255, 255, 255, 0.05);
  transition: all 0.3s ease;
}

.social-link:hover {
  color: var(--hono-red);
  background: rgba(227, 96, 2, 0.1);
  transform: translateY(-2px);
}

@keyframes photoReveal {
  from {
    opacity: 0;
    transform: scale(0.8);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes slideInRight {
  from {
    opacity: 0;
    transform: translateX(50px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
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
  Currently working on Spotlightjs, and other crazy ideas now and then.<br/><br />
    You might know me from @hono/mcp, muppet, hono-openapi, hono-rate-limiter, etc.
  </div>
</div>

---

<style scoped>

.right-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  height: 100%;
  gap: 3rem;
  padding-left: 4rem;
}

.tagline {
  font-size: 3rem;
  font-weight: 700;
  line-height: 1.2;
  color: rgba(255, 255, 255, 0.95);
  animation: fadeInUp 0.8s ease-out 0.8s both;
}

.tagline-highlight {
  background: -webkit-linear-gradient(135deg, #ffffff 0%, var(--hono-red) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-weight: 900;
}

.bio-text {
  font-size: 1.25rem;
  line-height: 1.6;
  color: rgba(255, 255, 255, 0.7);
  animation: fadeInUp 0.8s ease-out 0.6s both;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>

<div class="right-content">
  <div class="bio-text">
  What is MCP?
  </div>
  <div class="tagline">
    It's just a <span class="tagline-highlight">Server</span>, which can connect LLMs with <span class="tagline-highlight">External Apps</span>
  </div>
</div>



---

<style scoped>
.unified-timeline {
  padding: 1.5rem 0;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.timeline-header {
  text-align: center;
  margin-bottom: 1.5rem;
}

.main-title {
  font-size: 2.5rem;
  font-weight: 900;
  background: linear-gradient(135deg, #ffffff 0%, var(--hono-red) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 0.5rem;
}

.main-subtitle {
  font-size: 1rem;
  color: rgba(255, 255, 255, 0.6);
  font-weight: 300;
}

.timeline-track {
  position: relative;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 2rem;
  padding: 0;
  align-items: center;
  min-height: 420px;
}

.timeline-line-wrapper {
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  height: 4px;
  transform: translateY(-50%);
  padding: 0 5%;
}

.timeline-line {
  position: relative;
  width: 100%;
  height: 4px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 2px;
}

.timeline-progress {
  position: absolute;
  top: 0;
  left: 0;
  height: 4px;
  background: linear-gradient(90deg, var(--hono-red) 0%, #ff6b35 100%);
  border-radius: 2px;
  transition: width 0.6s ease;
  box-shadow: 0 0 20px rgba(227, 96, 2, 0.6);
}

.phase {
  position: relative;
  opacity: 0.3;
  transition: all 0.5s ease;
  display: flex;
  flex-direction: column;
}

.phase:nth-child(even) {
  align-items: center;
  padding-bottom: 14rem;
}

.phase:nth-child(odd) {
  align-items: center;
  padding-top: 14rem;
}

.phase.active {
  opacity: 1;
}

.phase-dot {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 16px;
  height: 16px;
  background: rgba(255, 255, 255, 0.3);
  border: 3px solid rgba(255, 255, 255, 0.4);
  border-radius: 50%;
  transition: all 0.5s ease;
  z-index: 10;
}

.phase.active .phase-dot {
  width: 22px;
  height: 22px;
  background: var(--hono-red);
  border-color: var(--hono-red);
  box-shadow: 0 0 25px rgba(227, 96, 2, 0.9);
}

.phase-connector {
  position: absolute;
  width: 2px;
  background: rgba(227, 96, 2, 0.4);
  left: 50%;
  transform: translateX(-50%);
  transition: all 0.5s ease;
}

.phase:nth-child(even) .phase-connector {
  bottom: 50%;
  height: 1.5rem;
}

.phase:nth-child(odd) .phase-connector {
  top: 50%;
  height: 1.5rem;
}

.phase.active .phase-connector {
  background: var(--hono-red);
  box-shadow: 0 0 10px rgba(227, 96, 2, 0.6);
}

.phase-date {
  font-size: 0.65rem;
  color: var(--hono-red);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  margin-bottom: 0.5rem;
  text-align: center;
}

.phase-title {
  font-size: 1.2rem;
  font-weight: 800;
  color: rgba(255, 255, 255, 0.9);
  text-align: center;
  line-height: 1.3;
}

.phase-summary {
  font-size: 0.8rem;
  color: rgba(255, 255, 255, 0.7);
  line-height: 1.4;
  text-align: center;
  margin-top: 0.75rem;
}
</style>

<div class="unified-timeline">
  <div class="timeline-header">
    <div class="main-title">The MCP Evolution</div>
  </div>

  <div class="timeline-track">
    <div class="timeline-line-wrapper">
      <div class="timeline-line">
        <div 
          class="timeline-progress" 
          :style="{ width: $clicks === 0 ? '0%' : $clicks >= 1 && $clicks < 2 ? '20%' : $clicks >= 2 && $clicks < 3 ? '40%' : $clicks >= 3 && $clicks < 4 ? '60%' : $clicks >= 4 && $clicks < 5 ? '80%' : '100%' }"
        ></div>
      </div>
    </div>
    <div class="phase" :class="{ active: $clicks >= 1 }">
      <div class="phase-connector"></div>
      <div class="phase-dot"></div>
      <v-click at="1">
        <div class="phase-date">Nov - Dec 2024</div>
        <div class="phase-title">Launch</div>
        <div class="phase-summary">
          Experimentation phase, exploring the usecases and potential
        </div>
      </v-click>
    </div>
    <div class="phase" :class="{ active: $clicks >= 2 }">
      <div class="phase-connector"></div>
      <div class="phase-dot"></div>
      <v-click at="2">
        <div class="phase-date">Jan - Feb 2025</div>
        <div class="phase-title">Just HTTP Wrappers?</div>
        <div class="phase-summary">
          "Why do we need MCP when LLMs can use OpenAPI specs?"
        </div>
      </v-click>
    </div>
    <div class="phase" :class="{ active: $clicks >= 3 }">
      <div class="phase-connector"></div>
      <div class="phase-dot"></div>
      <v-click at="3">
        <div class="phase-date">Mar 2025</div>
        <div class="phase-title">Growing Ecosystem</div>
        <div class="phase-summary">
          OpenAI and Google joining, MCP frameworks, inspector and HTTP transport
        </div>
      </v-click>
    </div>
    <div class="phase" :class="{ active: $clicks >= 4 }">
      <div class="phase-connector"></div>
      <div class="phase-dot"></div>
      <v-click at="4">
        <div class="phase-date">Apr - Jun 2025</div>
        <div class="phase-title">Official MCP Servers</div>
        <div class="phase-summary">
          from Sentry, Cloudflare, Github, Supabase, Context7, etc
        </div>
      </v-click>
    </div>
    <div class="phase" :class="{ active: $clicks >= 5 }">
      <div class="phase-connector"></div>
      <div class="phase-dot"></div>
      <v-click at="5">
        <div class="phase-date">Now</div>
        <div class="phase-title">Stability & New Ideas</div>
        <div class="phase-summary">
          Standardizing Auth and Transport. Adding agent inside the MCP server
        </div>
      </v-click>
    </div>
  </div>
</div>

---

### MCP Architecture

```mermaid
graph LR
    subgraph Clients["🖥️ Clients"]
        C1["Claude"]
        C2["VSCode"]
    end

    T["🔄 Transport<br/>(SSE/HTTP/Stdio)"]

    subgraph Auth["🔐 Authentication"]
        A1["OAuth"]
        A2["API Key"]
    end

    subgraph Servers["⚙️ MCP Servers"]
        S1["Database<br/>📚 Resources<br/>🛠️ Tools"]
        S3["API<br/>📚 Resources<br/>🛠️ Tools"]
        S2["Files<br/>📚 Resources<br/>🛠️ Tools"]
    end

    C1 --> T
    C2 --> T
    
    T --> A1
    T --> S2
    T --> A2
    
    A1 --> S1
    A2 --> S3

    style C1 fill:#8b5cf6,stroke:#7c3aed,stroke-width:3px,color:#fff
    style C2 fill:#8b5cf6,stroke:#7c3aed,stroke-width:3px,color:#fff
    style T fill:#E36002,stroke:#dc2626,stroke-width:4px,color:#fff
    style A1 fill:#f59e0b,stroke:#d97706,stroke-width:3px,color:#fff
    style A2 fill:#f59e0b,stroke:#d97706,stroke-width:3px,color:#fff
    style S1 fill:#10b981,stroke:#059669,stroke-width:3px,color:#fff
    style S2 fill:#10b981,stroke:#059669,stroke-width:3px,color:#fff
    style S3 fill:#10b981,stroke:#059669,stroke-width:3px,color:#fff
```

---
layout: center
---

<Tweet id="1924648575541379110" />

---

<style scoped>

.right-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  height: 100%;
  gap: 1rem;
  padding-left: 4rem;
}

.tagline {
  font-size: 3rem;
  font-weight: 700;
  line-height: 1.2;
  color: rgba(255, 255, 255, 0.95);
  animation: fadeInUp 0.8s ease-out 0.6s both;
}

.tagline-highlight {
  background: -webkit-linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-weight: 900;
}

.bio-text {
  font-size: 1.25rem;
  line-height: 1.6;
  color: rgba(255, 255, 255, 0.7);
  animation: fadeInUp 0.8s ease-out 0.8s both;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>

<div class="right-content">
  <div class="tagline"><span class="tagline-highlight">@hono/mcp</span>
  </div><div class="bio-text">
  HTTP Transport and Auth Support
  </div>
</div>

---

<style scoped>

.right-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  height: 100%;
  gap: 1rem;
  padding-left: 4rem;
}

.tagline {
  font-size: 3rem;
  font-weight: 700;
  line-height: 1.2;
  color: rgba(255, 255, 255, 0.95);
  animation: fadeInUp 0.8s ease-out 0.6s both;
}

.tagline-highlight {
  background: -webkit-linear-gradient(135deg, #ffffff 0%, var(--hono-red) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-weight: 900;
}

.bio-text {
  font-size: 1.25rem;
  line-height: 1.6;
  color: rgba(255, 255, 255, 0.7);
  animation: fadeInUp 0.8s ease-out 0.8s both;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>

<div class="right-content">
  <div class="tagline">Making 
  <span class="tagline-highlight">Hono</span>
  the default <span class="tagline-highlight">MCP Framework</span>
  </div>
  <div class="bio-text">
  Build. Test. Deploy.
  </div>
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
  background: linear-gradient(135deg, #ffffff 0%, var(--hono-red) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 1.5rem;
  animation: titlePulse 3s ease-in-out infinite;
}

@keyframes titlePulse {
  0%, 100% { 
    filter: drop-shadow(0 0 20px rgba(227, 96, 2, 0.3));
  }
  50% { 
    filter: drop-shadow(0 0 30px rgba(227, 96, 2, 0.5));
  }
}

.thank-you-subtitle {
  font-size: 1.3rem;
  color: rgba(255, 255, 255, 0.7);
  font-weight: 300;
  margin-bottom: 2rem;
}

.social-links-final {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 1.5rem;
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
  background: rgba(227, 96, 2, 0.2);
  border-color: var(--hono-red);
  transform: translateY(-3px);
}

.social-icon-final {
  font-size: 1.25rem;
  color: var(--hono-red);
}

.hono-mcp-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 1rem;
  background: rgba(227, 96, 2, 0.15);
  border: 2px solid var(--hono-red);
  border-radius: 1.5rem;
  margin-top: 1rem;
}

.hono-mcp-badge img {
  width: 24px;
  height: 24px;
}

.hono-mcp-text {
  font-size: 0.9rem;
  font-weight: 700;
  color: var(--hono-red);
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>

<div class="thank-you-container">
  <div class="thank-you-title">Thank You!</div>
  
  <div class="thank-you-subtitle">
    Let's build the future together
  </div>

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

  <div class="hono-mcp-badge">
    <img src="/hono_logo.svg" alt="Hono" />
    <span class="hono-mcp-text">Hono × MCP</span>
  </div>
</div>
