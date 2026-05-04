<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Shaheer Haider — Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Mono:ital,wght@0,300;0,400;1,300&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0f;
    --surface: #111118;
    --surface2: #1a1a24;
    --accent: #7c6aff;
    --accent2: #00e5ff;
    --accent3: #ff6b6b;
    --text: #e8e8f0;
    --text-dim: #6b6b82;
    --text-mid: #a0a0b8;
    --border: rgba(124,106,255,0.15);
    --glow: rgba(124,106,255,0.3);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Syne', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    width: 12px; height: 12px;
    background: var(--accent);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9999;
    transition: transform 0.15s ease, background 0.2s;
    mix-blend-mode: difference;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1.5px solid var(--accent);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9998;
    transition: all 0.12s ease;
    opacity: 0.5;
  }
  body:hover .cursor { transform: scale(1); }

  /* Noise overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1000;
    opacity: 0.4;
  }

  /* NAV */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    padding: 24px 60px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    z-index: 100;
    background: linear-gradient(to bottom, rgba(10,10,15,0.95), transparent);
    backdrop-filter: blur(2px);
  }
  .nav-logo {
    font-size: 1.1rem;
    font-weight: 800;
    letter-spacing: 0.08em;
    color: var(--text);
    text-transform: uppercase;
  }
  .nav-logo span { color: var(--accent); }
  .nav-links { display: flex; gap: 40px; }
  .nav-links a {
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem;
    color: var(--text-dim);
    text-decoration: none;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    transition: color 0.2s;
    position: relative;
  }
  .nav-links a::after {
    content: '';
    position: absolute;
    bottom: -4px; left: 0; right: 0;
    height: 1px;
    background: var(--accent);
    transform: scaleX(0);
    transition: transform 0.25s ease;
  }
  .nav-links a:hover { color: var(--text); }
  .nav-links a:hover::after { transform: scaleX(1); }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 120px 60px 80px;
    position: relative;
    overflow: hidden;
  }

  /* Animated grid bg */
  .grid-bg {
    position: absolute;
    inset: 0;
    background-image:
      linear-gradient(rgba(124,106,255,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(124,106,255,0.04) 1px, transparent 1px);
    background-size: 60px 60px;
    animation: gridShift 20s linear infinite;
  }
  @keyframes gridShift {
    0% { transform: translateY(0); }
    100% { transform: translateY(60px); }
  }

  /* Blobs */
  .blob {
    position: absolute;
    border-radius: 50%;
    filter: blur(80px);
    opacity: 0.15;
    animation: blobPulse 8s ease-in-out infinite;
  }
  .blob-1 { width: 500px; height: 500px; background: var(--accent); top: -100px; right: -100px; animation-delay: 0s; }
  .blob-2 { width: 350px; height: 350px; background: var(--accent2); bottom: 50px; left: 200px; animation-delay: 3s; }
  .blob-3 { width: 250px; height: 250px; background: var(--accent3); top: 200px; left: -50px; animation-delay: 5s; }
  @keyframes blobPulse {
    0%, 100% { transform: scale(1) translate(0, 0); opacity: 0.15; }
    50% { transform: scale(1.1) translate(20px, -20px); opacity: 0.22; }
  }

  .hero-content { position: relative; z-index: 2; max-width: 900px; }

  .hero-tag {
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem;
    color: var(--accent);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 24px;
    opacity: 0;
    animation: fadeUp 0.7s ease forwards 0.2s;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .hero-tag::before {
    content: '';
    width: 32px; height: 1px;
    background: var(--accent);
  }

  .hero-name {
    font-size: clamp(3.5rem, 8vw, 7rem);
    font-weight: 800;
    line-height: 1.0;
    letter-spacing: -0.03em;
    margin-bottom: 8px;
    opacity: 0;
    animation: fadeUp 0.8s ease forwards 0.4s;
  }
  .hero-name .accent { color: var(--accent); }

  .hero-title {
    font-size: clamp(1.1rem, 2.5vw, 1.6rem);
    font-weight: 400;
    color: var(--text-mid);
    margin-bottom: 32px;
    opacity: 0;
    animation: fadeUp 0.8s ease forwards 0.6s;
    letter-spacing: 0.02em;
  }

  .hero-desc {
    font-family: 'DM Mono', monospace;
    font-size: 0.9rem;
    color: var(--text-dim);
    line-height: 1.8;
    max-width: 520px;
    margin-bottom: 48px;
    opacity: 0;
    animation: fadeUp 0.8s ease forwards 0.8s;
  }

  .hero-ctas {
    display: flex;
    gap: 16px;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.8s ease forwards 1s;
  }

  .btn-primary {
    padding: 14px 32px;
    background: var(--accent);
    color: #fff;
    border: none;
    font-family: 'Syne', sans-serif;
    font-size: 0.85rem;
    font-weight: 700;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    text-decoration: none;
    cursor: none;
    position: relative;
    overflow: hidden;
    transition: transform 0.2s, box-shadow 0.2s;
    clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
  }
  .btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 12px 32px rgba(124,106,255,0.4);
  }
  .btn-outline {
    padding: 14px 32px;
    background: transparent;
    color: var(--text);
    border: 1px solid var(--border);
    font-family: 'Syne', sans-serif;
    font-size: 0.85rem;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    text-decoration: none;
    cursor: none;
    transition: border-color 0.2s, color 0.2s, background 0.2s;
    clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
  }
  .btn-outline:hover {
    border-color: var(--accent);
    background: rgba(124,106,255,0.08);
    color: var(--accent);
  }

  /* Scroll indicator */
  .scroll-hint {
    position: absolute;
    bottom: 40px; left: 60px;
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    color: var(--text-dim);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    writing-mode: vertical-rl;
    display: flex;
    align-items: center;
    gap: 12px;
    opacity: 0;
    animation: fadeIn 1s ease forwards 1.5s;
  }
  .scroll-hint::after {
    content: '';
    width: 1px; height: 60px;
    background: linear-gradient(to bottom, var(--text-dim), transparent);
    animation: scrollLine 2s ease-in-out infinite;
  }
  @keyframes scrollLine {
    0%, 100% { opacity: 0.4; transform: scaleY(1); }
    50% { opacity: 1; transform: scaleY(0.7); }
  }

  /* Section styles */
  section { padding: 100px 60px; position: relative; }
  .section-label {
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    color: var(--accent);
    letter-spacing: 0.25em;
    text-transform: uppercase;
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .section-label::before {
    content: attr(data-num);
    color: var(--text-dim);
  }
  .section-title {
    font-size: clamp(2rem, 4vw, 3.2rem);
    font-weight: 800;
    letter-spacing: -0.02em;
    line-height: 1.1;
    margin-bottom: 60px;
  }

  /* ABOUT */
  #about {
    background: var(--surface);
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
  }
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: center;
    max-width: 1100px;
  }
  .about-text p {
    font-family: 'DM Mono', monospace;
    font-size: 0.9rem;
    color: var(--text-mid);
    line-height: 1.9;
    margin-bottom: 20px;
  }
  .about-text p strong { color: var(--text); font-weight: 400; }
  .about-stats {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2px;
  }
  .stat-card {
    background: var(--surface2);
    padding: 28px 24px;
    border: 1px solid var(--border);
    position: relative;
    overflow: hidden;
    transition: border-color 0.3s;
  }
  .stat-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(to right, var(--accent), var(--accent2));
    transform: scaleX(0);
    transition: transform 0.3s;
    transform-origin: left;
  }
  .stat-card:hover { border-color: var(--accent); }
  .stat-card:hover::before { transform: scaleX(1); }
  .stat-num {
    font-size: 2.5rem;
    font-weight: 800;
    color: var(--accent);
    line-height: 1;
    margin-bottom: 8px;
  }
  .stat-label {
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    color: var(--text-dim);
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }

  /* SKILLS */
  #skills { background: var(--bg); }
  .skills-container { max-width: 1100px; }
  .skill-group { margin-bottom: 48px; }
  .skill-group-title {
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    color: var(--accent2);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 16px;
    padding-bottom: 8px;
    border-bottom: 1px solid var(--border);
  }
  .skill-tags { display: flex; flex-wrap: wrap; gap: 10px; }
  .skill-tag {
    padding: 8px 18px;
    background: var(--surface);
    border: 1px solid var(--border);
    font-family: 'DM Mono', monospace;
    font-size: 0.78rem;
    color: var(--text-mid);
    letter-spacing: 0.05em;
    transition: all 0.25s;
    position: relative;
    cursor: none;
  }
  .skill-tag::before {
    content: '▸';
    margin-right: 6px;
    color: var(--accent);
    font-size: 0.65rem;
  }
  .skill-tag:hover {
    background: rgba(124,106,255,0.1);
    border-color: var(--accent);
    color: var(--text);
    transform: translateY(-2px);
  }
  .skill-tag.featured {
    border-color: rgba(124,106,255,0.4);
    background: rgba(124,106,255,0.07);
    color: var(--text);
  }

  /* PROJECTS */
  #projects {
    background: var(--surface);
    border-top: 1px solid var(--border);
  }
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
    max-width: 1100px;
  }
  .project-card {
    background: var(--surface2);
    padding: 36px 32px;
    border: 1px solid transparent;
    position: relative;
    overflow: hidden;
    transition: border-color 0.3s, transform 0.3s;
    cursor: none;
  }
  .project-card::after {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(124,106,255,0.05), transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }
  .project-card:hover {
    border-color: var(--accent);
    transform: translateY(-4px);
  }
  .project-card:hover::after { opacity: 1; }
  .project-card.featured {
    grid-column: span 2;
    background: linear-gradient(135deg, rgba(124,106,255,0.08), var(--surface2));
    border-color: rgba(124,106,255,0.2);
  }
  .project-num {
    font-family: 'DM Mono', monospace;
    font-size: 0.65rem;
    color: var(--text-dim);
    letter-spacing: 0.15em;
    margin-bottom: 20px;
  }
  .project-title {
    font-size: 1.25rem;
    font-weight: 700;
    margin-bottom: 12px;
    letter-spacing: -0.01em;
  }
  .project-desc {
    font-family: 'DM Mono', monospace;
    font-size: 0.8rem;
    color: var(--text-dim);
    line-height: 1.7;
    margin-bottom: 24px;
  }
  .project-stack { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 20px; }
  .stack-badge {
    padding: 4px 10px;
    background: rgba(124,106,255,0.1);
    border: 1px solid rgba(124,106,255,0.2);
    font-family: 'DM Mono', monospace;
    font-size: 0.65rem;
    color: var(--accent);
    letter-spacing: 0.05em;
  }
  .project-arrow {
    font-size: 1.2rem;
    color: var(--text-dim);
    transition: color 0.2s, transform 0.2s;
    display: inline-block;
  }
  .project-card:hover .project-arrow { color: var(--accent); transform: translate(4px, -4px); }

  /* GITHUB SECTION */
  #github {
    background: var(--bg);
    border-top: 1px solid var(--border);
  }
  .github-content {
    max-width: 800px;
    text-align: center;
    margin: 0 auto;
  }
  .github-card {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 48px;
    position: relative;
    overflow: hidden;
    margin-top: 40px;
  }
  .github-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(to right, var(--accent), var(--accent2), var(--accent3));
  }
  .github-handle {
    font-family: 'DM Mono', monospace;
    font-size: 1.4rem;
    color: var(--accent);
    margin-bottom: 12px;
  }
  .github-handle span { color: var(--text-dim); }
  .github-bio {
    font-family: 'DM Mono', monospace;
    font-size: 0.85rem;
    color: var(--text-dim);
    line-height: 1.7;
    margin-bottom: 32px;
  }
  .github-link {
    display: inline-flex;
    align-items: center;
    gap: 10px;
    padding: 14px 36px;
    background: var(--accent);
    color: white;
    text-decoration: none;
    font-weight: 700;
    font-size: 0.85rem;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    cursor: none;
    transition: box-shadow 0.2s, transform 0.2s;
    clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
  }
  .github-link:hover {
    transform: translateY(-2px);
    box-shadow: 0 12px 32px rgba(124,106,255,0.4);
  }

  /* CONTACT */
  #contact {
    background: var(--surface);
    border-top: 1px solid var(--border);
    text-align: center;
  }
  .contact-inner { max-width: 700px; margin: 0 auto; }
  .contact-tagline {
    font-family: 'DM Mono', monospace;
    font-size: 0.9rem;
    color: var(--text-dim);
    line-height: 1.8;
    margin-bottom: 48px;
  }
  .contact-links { display: flex; justify-content: center; gap: 20px; flex-wrap: wrap; }
  .contact-link {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 12px 24px;
    border: 1px solid var(--border);
    color: var(--text-mid);
    text-decoration: none;
    font-family: 'DM Mono', monospace;
    font-size: 0.78rem;
    letter-spacing: 0.08em;
    transition: all 0.25s;
    cursor: none;
  }
  .contact-link:hover {
    border-color: var(--accent);
    color: var(--accent);
    background: rgba(124,106,255,0.05);
  }

  /* FOOTER */
  footer {
    padding: 32px 60px;
    border-top: 1px solid var(--border);
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  footer p {
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    color: var(--text-dim);
    letter-spacing: 0.1em;
  }
  footer p span { color: var(--accent); }

  /* Animations */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }

  .reveal {
    opacity: 0;
    transform: translateY(40px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* Mobile */
  @media (max-width: 768px) {
    nav { padding: 20px 24px; }
    .nav-links { display: none; }
    section { padding: 70px 24px; }
    .hero { padding: 100px 24px 70px; }
    .scroll-hint { display: none; }
    .about-grid { grid-template-columns: 1fr; gap: 48px; }
    .projects-grid { grid-template-columns: 1fr; }
    .project-card.featured { grid-column: span 1; }
    footer { flex-direction: column; gap: 12px; text-align: center; padding: 24px; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NAV -->
<nav>
  <div class="nav-logo">S<span>.</span>Haider</div>
  <div class="nav-links">
    <a href="#about">About</a>
    <a href="#skills">Skills</a>
    <a href="#projects">Projects</a>
    <a href="#github">GitHub</a>
    <a href="#contact">Contact</a>
  </div>
</nav>

<!-- HERO -->
<section class="hero" id="home">
  <div class="grid-bg"></div>
  <div class="blob blob-1"></div>
  <div class="blob blob-2"></div>
  <div class="blob blob-3"></div>
  <div class="hero-content">
    <div class="hero-tag">BSCS Student &amp; Web Developer</div>
    <h1 class="hero-name">Shaheer<br><span class="accent">Haider</span></h1>
    <p class="hero-title">Building the web, one line at a time.</p>
    <p class="hero-desc">
      Computer Science undergrad passionate about crafting<br>
      full-stack experiences — from pixel-perfect UIs<br>
      to robust back-end systems.
    </p>
    <div class="hero-ctas">
      <a href="#projects" class="btn-primary">View Projects</a>
      <a href="https://github.com/shaheer-haider" target="_blank" class="btn-outline">GitHub ↗</a>
    </div>
  </div>
  <div class="scroll-hint">Scroll</div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="section-label" data-num="01">About</div>
  <h2 class="section-title">Who I Am</h2>
  <div class="about-grid">
    <div class="about-text">
      <p>
        Hey! I'm <strong>Shaheer Haider</strong>, a BSCS student with a deep passion for 
        web development. I love building things that live on the internet — clean, functional, 
        and impactful.
      </p>
      <p>
        My journey started with the basics of HTML & CSS, and has evolved into full-stack 
        development with <strong>React.js, .NET, Python</strong>, and various databases. 
        I also explore game development with <strong>Pygame</strong> when I want to add some fun.
      </p>
      <p>
        I'm always learning, always building, and always pushing myself to write better code 
        and create better experiences.
      </p>
    </div>
    <div class="about-stats">
      <div class="stat-card">
        <div class="stat-num">5+</div>
        <div class="stat-label">Languages</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">3+</div>
        <div class="stat-label">Databases</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">∞</div>
        <div class="stat-label">Curiosity</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">100%</div>
        <div class="stat-label">Committed</div>
      </div>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="section-label" data-num="02">Skills</div>
  <h2 class="section-title">Tech Stack</h2>
  <div class="skills-container">

    <div class="skill-group reveal">
      <div class="skill-group-title">Frontend</div>
      <div class="skill-tags">
        <span class="skill-tag featured">React.js</span>
        <span class="skill-tag featured">JavaScript</span>
        <span class="skill-tag featured">HTML5</span>
        <span class="skill-tag featured">CSS3</span>
      </div>
    </div>

    <div class="skill-group reveal">
      <div class="skill-group-title">Backend & Languages</div>
      <div class="skill-tags">
        <span class="skill-tag featured">C#</span>
        <span class="skill-tag featured">.NET</span>
        <span class="skill-tag featured">Python</span>
        <span class="skill-tag">Pygame</span>
      </div>
    </div>

    <div class="skill-group reveal">
      <div class="skill-group-title">Databases</div>
      <div class="skill-tags">
        <span class="skill-tag featured">MongoDB</span>
        <span class="skill-tag featured">MySQL</span>
        <span class="skill-tag">NoSQL</span>
      </div>
    </div>

    <div class="skill-group reveal">
      <div class="skill-group-title">Tools & Concepts</div>
      <div class="skill-tags">
        <span class="skill-tag">Git / GitHub</span>
        <span class="skill-tag">REST APIs</span>
        <span class="skill-tag">Responsive Design</span>
        <span class="skill-tag">OOP</span>
        <span class="skill-tag">Data Structures</span>
      </div>
    </div>

  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="section-label" data-num="03">Projects</div>
  <h2 class="section-title">What I've Built</h2>
  <div class="projects-grid">

    <div class="project-card featured reveal">
      <div class="project-num">001 — Featured</div>
      <div class="project-title">Full-Stack Web Application</div>
      <p class="project-desc">
        A complete full-stack web app with React.js frontend, C# .NET backend, 
        and MongoDB/MySQL data layer. Features authentication, real-time updates, 
        and a clean responsive UI.
      </p>
      <div class="project-stack">
        <span class="stack-badge">React.js</span>
        <span class="stack-badge">C#</span>
        <span class="stack-badge">.NET</span>
        <span class="stack-badge">MongoDB</span>
      </div>
      <span class="project-arrow">↗</span>
    </div>

    <div class="project-card reveal">
      <div class="project-num">002</div>
      <div class="project-title">Pygame Project</div>
      <p class="project-desc">
        A Python-based game built with Pygame, exploring game loop logic, 
        collision detection, and sprite animations.
      </p>
      <div class="project-stack">
        <span class="stack-badge">Python</span>
        <span class="stack-badge">Pygame</span>
      </div>
      <span class="project-arrow">↗</span>
    </div>

    <div class="project-card reveal">
      <div class="project-num">003</div>
      <div class="project-title">Database-Driven App</div>
      <p class="project-desc">
        A data-driven web application using MySQL and NoSQL with 
        a JavaScript frontend. Supports CRUD operations and complex queries.
      </p>
      <div class="project-stack">
        <span class="stack-badge">JavaScript</span>
        <span class="stack-badge">MySQL</span>
        <span class="stack-badge">NoSQL</span>
      </div>
      <span class="project-arrow">↗</span>
    </div>

    <div class="project-card reveal">
      <div class="project-num">004</div>
      <div class="project-title">Responsive UI Portfolio</div>
      <p class="project-desc">
        A responsive multi-page website built with pure HTML, CSS, 
        and vanilla JavaScript. Focused on clean design and accessibility.
      </p>
      <div class="project-stack">
        <span class="stack-badge">HTML</span>
        <span class="stack-badge">CSS</span>
        <span class="stack-badge">JavaScript</span>
      </div>
      <span class="project-arrow">↗</span>
    </div>

    <div class="project-card reveal">
      <div class="project-num">005</div>
      <div class="project-title">Python Automation Script</div>
      <p class="project-desc">
        A Python utility that automates repetitive tasks, 
        featuring file handling, data parsing, and CLI interaction.
      </p>
      <div class="project-stack">
        <span class="stack-badge">Python</span>
      </div>
      <span class="project-arrow">↗</span>
    </div>

  </div>
</section>

<!-- GITHUB -->
<section id="github">
  <div class="section-label" data-num="04">GitHub</div>
  <div class="github-content reveal">
    <h2 class="section-title" style="margin-bottom: 0">My Code Lives Here</h2>
    <div class="github-card">
      <div class="github-handle"><span>@</span>shaheer-haider</div>
      <p class="github-bio">
        Explore all my projects, contributions, and open-source work.<br>
        From web apps to game experiments — it's all there.
      </p>
      <a href="https://github.com/shaheer-haider" target="_blank" class="github-link">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
          <path d="M12 0C5.374 0 0 5.373 0 12c0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23A11.509 11.509 0 0 1 12 5.803c1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576C20.566 21.797 24 17.3 24 12c0-6.627-5.373-12-12-12z"/>
        </svg>
        Visit GitHub Profile
      </a>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="section-label" data-num="05">Contact</div>
  <div class="contact-inner reveal">
    <h2 class="section-title">Let's Connect</h2>
    <p class="contact-tagline">
      Have a project in mind? Want to collaborate?<br>
      Or just want to say hello — I'm always up for a chat.
    </p>
    <div class="contact-links">
      <a href="https://github.com/shaheer-haider" target="_blank" class="contact-link">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor">
          <path d="M12 0C5.374 0 0 5.373 0 12c0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23A11.509 11.509 0 0 1 12 5.803c1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576C20.566 21.797 24 17.3 24 12c0-6.627-5.373-12-12-12z"/>
        </svg>
        GitHub
      </a>
      <a href="mailto:shaheer@example.com" class="contact-link">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
          <polyline points="22,6 12,13 2,6"/>
        </svg>
        Email Me
      </a>
      <a href="https://linkedin.com/in/shaheer-haider" target="_blank" class="contact-link">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor">
          <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6zM2 9h4v12H2z"/>
          <circle cx="4" cy="4" r="2"/>
        </svg>
        LinkedIn
      </a>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <p>© 2025 <span>Shaheer Haider</span>. All rights reserved.</p>
  <p>Designed &amp; Built by <span>Shaheer Haider</span></p>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mouseX = 0, mouseY = 0, ringX = 0, ringY = 0;

  document.addEventListener('mousemove', (e) => {
    mouseX = e.clientX; mouseY = e.clientY;
    cursor.style.left = mouseX - 6 + 'px';
    cursor.style.top = mouseY - 6 + 'px';
  });

  function animateRing() {
    ringX += (mouseX - ringX - 18) * 0.12;
    ringY += (mouseY - ringY - 18) * 0.12;
    ring.style.left = ringX + 'px';
    ring.style.top = ringY + 'px';
    requestAnimationFrame(animateRing);
  }
  animateRing();

  document.querySelectorAll('a, button, .project-card, .skill-tag, .stat-card').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.transform = 'scale(2.5)';
      ring.style.opacity = '1';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.transform = 'scale(1)';
      ring.style.opacity = '0.5';
    });
  });

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), i * 100);
      }
    });
  }, { threshold: 0.1 });
  reveals.forEach(el => observer.observe(el));

  // Active nav
  const sections = document.querySelectorAll('section[id]');
  const navLinks = document.querySelectorAll('.nav-links a');
  window.addEventListener('scroll', () => {
    let current = '';
    sections.forEach(s => {
      if (window.scrollY >= s.offsetTop - 200) current = s.id;
    });
    navLinks.forEach(a => {
      a.style.color = a.getAttribute('href') === '#' + current ? 'var(--accent)' : '';
    });
  });
</script>
</body>
</html>
