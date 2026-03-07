<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sandra (Tien-Jo) Chang — Creative Technologist</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=Space+Mono:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0f;
    --surface: #111118;
    --card: #16161f;
    --border: #2a2a3a;
    --accent: #e8c547;
    --accent2: #7eb8f7;
    --accent3: #f07aac;
    --text: #e8e6f0;
    --muted: #7a7890;
    --serif: 'DM Serif Display', Georgia, serif;
    --mono: 'Space Mono', monospace;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--mono);
    font-size: 14px;
    line-height: 1.7;
    overflow-x: hidden;
  }

  /* ── NOISE TEXTURE OVERLAY ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1000;
    opacity: 0.35;
  }

  /* ── BACKGROUND GRADIENT BLOBS ── */
  .bg-blobs {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 0;
    overflow: hidden;
  }
  .bg-blobs span {
    position: absolute;
    border-radius: 50%;
    filter: blur(120px);
    opacity: 0.07;
  }
  .bg-blobs span:nth-child(1) {
    width: 600px; height: 600px;
    background: var(--accent);
    top: -200px; left: -200px;
    animation: drift1 20s ease-in-out infinite alternate;
  }
  .bg-blobs span:nth-child(2) {
    width: 500px; height: 500px;
    background: var(--accent2);
    bottom: -100px; right: -100px;
    animation: drift2 25s ease-in-out infinite alternate;
  }
  .bg-blobs span:nth-child(3) {
    width: 400px; height: 400px;
    background: var(--accent3);
    top: 50%; left: 50%;
    animation: drift3 18s ease-in-out infinite alternate;
  }

  @keyframes drift1 { to { transform: translate(80px, 60px); } }
  @keyframes drift2 { to { transform: translate(-60px, -80px); } }
  @keyframes drift3 { to { transform: translate(-40px, 50px); } }

  /* ── LAYOUT ── */
  .wrapper {
    position: relative;
    z-index: 1;
    max-width: 900px;
    margin: 0 auto;
    padding: 0 2rem;
  }

  /* ── HEADER ── */
  header {
    padding: 5rem 0 3rem;
    border-bottom: 1px solid var(--border);
    position: relative;
  }

  .header-tag {
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 1.2rem;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.1s;
  }

  h1 {
    font-family: var(--serif);
    font-size: clamp(2.8rem, 6vw, 4.5rem);
    line-height: 1.05;
    font-weight: 400;
    letter-spacing: -0.02em;
    opacity: 0;
    animation: fadeUp 0.7s ease forwards 0.2s;
  }

  h1 em {
    font-style: italic;
    color: var(--accent);
  }

  .header-sub {
    margin-top: 1rem;
    color: var(--muted);
    font-size: 13px;
    max-width: 520px;
    opacity: 0;
    animation: fadeUp 0.7s ease forwards 0.35s;
  }

  .header-sub strong {
    color: var(--accent2);
    font-weight: 700;
  }

  .header-links {
    display: flex;
    gap: 1.5rem;
    margin-top: 2rem;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.7s ease forwards 0.5s;
  }

  .header-links a {
    color: var(--muted);
    text-decoration: none;
    font-size: 12px;
    letter-spacing: 0.05em;
    border-bottom: 1px solid transparent;
    transition: color 0.2s, border-color 0.2s;
  }
  .header-links a:hover {
    color: var(--accent);
    border-color: var(--accent);
  }

  /* ── SECTION HEADERS ── */
  section {
    padding: 4rem 0 0;
    opacity: 0;
    transform: translateY(24px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  section.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .section-label {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-bottom: 2.5rem;
  }
  .section-label::before {
    content: '';
    display: block;
    width: 2rem;
    height: 1px;
    background: var(--accent);
  }
  .section-label span {
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--accent);
  }

  /* ── INTRO STATEMENT ── */
  .intro-statement {
    font-family: var(--serif);
    font-size: clamp(1.3rem, 2.5vw, 1.7rem);
    line-height: 1.5;
    font-weight: 400;
    color: var(--text);
    max-width: 700px;
    border-left: 2px solid var(--accent);
    padding-left: 1.5rem;
    margin-bottom: 1.5rem;
  }

  .intro-body {
    color: var(--muted);
    max-width: 620px;
    font-size: 13px;
    line-height: 1.9;
    margin-left: calc(2px + 1.5rem);
  }

  /* ── SKILLS GRID ── */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
    gap: 1px;
    border: 1px solid var(--border);
    background: var(--border);
    margin-top: 0;
  }

  .skill-cell {
    background: var(--card);
    padding: 1.4rem 1.5rem;
    transition: background 0.2s;
  }
  .skill-cell:hover { background: #1c1c28; }

  .skill-category {
    font-size: 10px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--accent3);
    margin-bottom: 0.6rem;
  }

  .skill-items {
    font-size: 12px;
    color: var(--text);
    line-height: 1.8;
  }

  .skill-items .highlight {
    color: var(--accent2);
    font-weight: 700;
  }

  /* ── PROJECTS ── */
  .projects-list {
    display: flex;
    flex-direction: column;
    gap: 1px;
    border: 1px solid var(--border);
    background: var(--border);
  }

  .project-card {
    background: var(--card);
    padding: 2rem 2rem 2rem 2rem;
    position: relative;
    overflow: hidden;
    transition: background 0.2s;
  }
  .project-card:hover { background: #1a1a25; }

  .project-card::before {
    content: '';
    position: absolute;
    left: 0; top: 0; bottom: 0;
    width: 3px;
    background: var(--accent);
    transform: scaleY(0);
    transform-origin: bottom;
    transition: transform 0.3s ease;
  }
  .project-card:hover::before { transform: scaleY(1); }

  .project-number {
    font-size: 10px;
    letter-spacing: 0.15em;
    color: var(--muted);
    margin-bottom: 0.5rem;
  }

  .project-title {
    font-family: var(--serif);
    font-size: 1.4rem;
    font-weight: 400;
    margin-bottom: 0.5rem;
    color: var(--text);
  }

  .project-tagline {
    color: var(--muted);
    font-size: 12px;
    margin-bottom: 1.2rem;
    font-style: italic;
  }

  .project-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
    margin-top: 1rem;
  }

  @media (max-width: 600px) {
    .project-grid { grid-template-columns: 1fr; }
  }

  .project-detail {
    background: var(--surface);
    padding: 1rem 1.2rem;
    border-left: 2px solid var(--border);
  }

  .project-detail-label {
    font-size: 10px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--accent3);
    margin-bottom: 0.4rem;
  }

  .project-detail p {
    font-size: 12px;
    color: var(--muted);
    line-height: 1.7;
  }

  .project-detail p strong {
    color: var(--accent2);
  }

  .tech-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
    margin-top: 1rem;
  }

  .tech-tag {
    font-size: 10px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 0.2rem 0.6rem;
    border: 1px solid var(--border);
    color: var(--muted);
    transition: border-color 0.2s, color 0.2s;
  }
  .project-card:hover .tech-tag {
    border-color: var(--accent);
    color: var(--accent);
  }

  /* ── EXPERIENCE ── */
  .exp-list {
    display: flex;
    flex-direction: column;
    gap: 1px;
    border: 1px solid var(--border);
    background: var(--border);
  }

  .exp-card {
    background: var(--card);
    padding: 1.8rem 2rem;
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 0.5rem 2rem;
    align-items: start;
    transition: background 0.2s;
  }
  .exp-card:hover { background: #1a1a25; }

  .exp-role {
    font-family: var(--serif);
    font-size: 1.15rem;
    font-weight: 400;
    margin-bottom: 0.2rem;
  }

  .exp-org {
    font-size: 12px;
    color: var(--accent2);
    margin-bottom: 0.8rem;
    font-weight: 700;
    letter-spacing: 0.05em;
  }

  .exp-date {
    font-size: 11px;
    color: var(--muted);
    text-align: right;
    white-space: nowrap;
    margin-top: 0.4rem;
  }

  .exp-bullets {
    list-style: none;
    grid-column: 1 / -1;
  }

  .exp-bullets li {
    font-size: 12px;
    color: var(--muted);
    line-height: 1.8;
    padding-left: 1.2rem;
    position: relative;
    margin-bottom: 0.2rem;
  }
  .exp-bullets li::before {
    content: '→';
    position: absolute;
    left: 0;
    color: var(--accent);
    font-size: 11px;
  }
  .exp-bullets li strong {
    color: var(--text);
  }

  /* ── EDUCATION ── */
  .edu-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1px;
    border: 1px solid var(--border);
    background: var(--border);
  }

  @media (max-width: 600px) {
    .edu-grid { grid-template-columns: 1fr; }
  }

  .edu-card {
    background: var(--card);
    padding: 1.8rem 2rem;
    transition: background 0.2s;
  }
  .edu-card:hover { background: #1a1a25; }

  .edu-degree {
    font-family: var(--serif);
    font-size: 1.2rem;
    margin-bottom: 0.3rem;
  }

  .edu-school {
    font-size: 12px;
    color: var(--accent2);
    font-weight: 700;
    letter-spacing: 0.05em;
    margin-bottom: 0.3rem;
  }

  .edu-year {
    font-size: 11px;
    color: var(--muted);
  }

  /* ── WDI ALIGNMENT ── */
  .alignment-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 1px;
    border: 1px solid var(--border);
    background: var(--border);
  }

  .align-card {
    background: var(--card);
    padding: 1.4rem 1.5rem;
    transition: background 0.2s;
  }
  .align-card:hover { background: #1a1a25; }

  .align-icon {
    font-size: 1.3rem;
    margin-bottom: 0.8rem;
    color: var(--accent);
    opacity: 0.7;
    line-height: 1;
    font-family: var(--mono);
    transition: opacity 0.2s, transform 0.2s;
  }
  .align-card:hover .align-icon {
    opacity: 1;
    transform: scale(1.15);
  }

  .align-title {
    font-size: 11px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 0.4rem;
  }

  .align-desc {
    font-size: 12px;
    color: var(--muted);
    line-height: 1.7;
  }

  /* ── FOOTER ── */
  footer {
    padding: 4rem 0 3rem;
    border-top: 1px solid var(--border);
    margin-top: 5rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: gap;
    gap: 1rem;
  }

  .footer-name {
    font-family: var(--serif);
    font-size: 1.1rem;
    font-style: italic;
    color: var(--muted);
  }

  .footer-links {
    display: flex;
    gap: 1.5rem;
  }

  .footer-links a {
    font-size: 11px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--muted);
    text-decoration: none;
    transition: color 0.2s;
  }
  .footer-links a:hover { color: var(--accent); }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(16px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* ── DIVIDER ── */
  .section-divider {
    border: none;
    border-top: 1px solid var(--border);
    margin: 0;
  }
</style>
</head>
<body>

<div class="bg-blobs">
  <span></span><span></span><span></span>
</div>

<div class="wrapper">

  <!-- HEADER -->
  <header>
    <p class="header-tag">Creative Technologist · Portfolio 2026</p>
    <h1>Sandra<br><em>(Tien-Jo)</em> Chang</h1>
    <p class="header-sub">
      <strong>MFA Candidate</strong> in Creative Computing & Music Technology at CalArts.<br>
      I design story-driven interactive environments that transform invisible systems into moments of shared wonder.
    </p>
    <div class="header-links">
      <a href="mailto:tienjo918@gmail.com">tienjo918@gmail.com</a>
      <a href="https://www.linkedin.com/in/tienjo918" target="_blank">linkedin/tienjo918</a>
      <a href="#">Portfolio →</a>
    </div>
  </header>

  <!-- ABOUT -->
  <section>
    <div class="section-label"><span>About</span></div>
    <blockquote class="intro-statement">
      Technology is most powerful when it disappears into the story.
    </blockquote>
    <p class="intro-body">
      My work sits at the intersection of computation, embodied experience, and narrative. From real-time generative graphics to spatially-aware sound environments, I build systems that respond, adapt, and invite participation — translating mathematical and perceptual abstractions into something guests can feel. I'm drawn to Walt Disney Imagineering because the best Imagineering work does exactly this: the technology is invisible, and the magic is everything.
    </p>
  </section>

  <!-- WDI ALIGNMENT -->
  <section>
    <div class="section-label"><span>Why WDI R&D</span></div>
    <div class="alignment-grid">
      <div class="align-card">
        <div class="align-icon">◈</div>
        <div class="align-title">Prototype to Production</div>
        <div class="align-desc">Experienced building at every fidelity — from quick Processing sketches to full Unreal Engine builds and custom PCB-adjacent hardware integrations.</div>
      </div>
      <div class="align-card">
        <div class="align-icon">◭</div>
        <div class="align-title">Real-Time Engines</div>
        <div class="align-desc">Developed interactive experiences in Unreal Engine and TouchDesigner, designing systems where content responds live to user behavior and sensor input.</div>
      </div>
      <div class="align-card">
        <div class="align-icon">◎</div>
        <div class="align-title">Computer Vision</div>
        <div class="align-desc">Implemented OpenCV pipelines to translate physical presence into digital response — grounding interactive work in the real environment.</div>
      </div>
      <div class="align-card">
        <div class="align-icon">⌁</div>
        <div class="align-title">Systems Integration</div>
        <div class="align-desc">Hands-on with DMX lighting control, A/V signal routing, PA systems, and coordinating software/hardware layers for live technical deployments.</div>
      </div>
      <div class="align-card">
        <div class="align-icon">⬡</div>
        <div class="align-title">Cross-Platform Dev</div>
        <div class="align-desc">Native development across Linux, macOS, Windows, with firmware experience on Arduino/Raspberry Pi platforms for embedded and IoT applications.</div>
      </div>
      <div class="align-card">
        <div class="align-icon">⌖</div>
        <div class="align-title">Stakeholder Communication</div>
        <div class="align-desc">Regularly presented technical concepts to non-technical collaborators in academic and live-event contexts — translating systems into stories.</div>
      </div>
    </div>
  </section>

  <!-- SKILLS -->
  <section>
    <div class="section-label"><span>Technical Toolkit</span></div>
    <div class="skills-grid">
      <div class="skill-cell">
        <div class="skill-category">Languages</div>
        <div class="skill-items">
          <span class="highlight">C++ / openFrameworks</span><br>
          <span class="highlight">JavaScript</span> (p5.js, WebGL)<br>
          Python · Java
        </div>
      </div>
      <div class="skill-cell">
        <div class="skill-category">Creative Engines</div>
        <div class="skill-items">
          <span class="highlight">Unreal Engine</span><br>
          <span class="highlight">TouchDesigner</span><br>
          Blender · Processing
        </div>
      </div>
      <div class="skill-cell">
        <div class="skill-category">Computer Vision & Sensing</div>
        <div class="skill-items">
          <span class="highlight">OpenCV</span><br>
          External Sensor Integration<br>
          Arduino · Raspberry Pi
        </div>
      </div>
      <div class="skill-cell">
        <div class="skill-category">Audio & Show Control</div>
        <div class="skill-items">
          <span class="highlight">MAX/MSP</span><br>
          DMX Lighting · A/V Routing<br>
          ProTools · Ableton
        </div>
      </div>
    </div>
  </section>

  <!-- PROJECTS -->
  <section>
    <div class="section-label"><span>Key Projects</span></div>
    <div class="projects-list">

      <div class="project-card">
        <div class="project-number">01 / INSTALLATION</div>
        <div class="project-title">Interactive Responsive Media Installation</div>
        <div class="project-tagline">A real-time audiovisual environment that responds to collective audience movement.</div>
        <div class="project-grid">
          <div class="project-detail">
            <div class="project-detail-label">The Magic</div>
            <p>Audience movement triggers generative visuals and spatial audio in real time — the environment becomes a mirror of collective presence, never repeating the same configuration twice.</p>
          </div>
          <div class="project-detail">
            <div class="project-detail-label">How It Works</div>
            <p>Built with <strong>TouchDesigner</strong> and <strong>openFrameworks</strong> to process live sensor data into visual abstractions. <strong>DMX lighting</strong> was choreographed algorithmically to sync with the visual state, blurring the line between screen and space.</p>
          </div>
        </div>
        <div class="tech-tags">
          <span class="tech-tag">TouchDesigner</span>
          <span class="tech-tag">openFrameworks</span>
          <span class="tech-tag">DMX</span>
          <span class="tech-tag">OpenCV</span>
          <span class="tech-tag">C++</span>
        </div>
      </div>

      <div class="project-card">
        <div class="project-number">02 / PROTOTYPE</div>
        <div class="project-title">Spatial Audio & Narrative Prototype</div>
        <div class="project-tagline">A story told through sound — where position in space determines what you hear and what you know.</div>
        <div class="project-grid">
          <div class="project-detail">
            <div class="project-detail-label">The Magic</div>
            <p>Listeners unlock different layers of a narrative by physically moving through space — the story is distributed across the environment, and presence becomes participation.</p>
          </div>
          <div class="project-detail">
            <div class="project-detail-label">How It Works</div>
            <p>Engineered a custom software solution in <strong>Max/MSP</strong> and <strong>Python</strong> for real-time sonic interaction, integrating positional sensing to trigger narrative state changes dynamically.</p>
          </div>
        </div>
        <div class="tech-tags">
          <span class="tech-tag">Max/MSP</span>
          <span class="tech-tag">Python</span>
          <span class="tech-tag">Raspberry Pi</span>
          <span class="tech-tag">Spatial Audio</span>
        </div>
      </div>

      <div class="project-card">
        <div class="project-number">03 / GAME ENGINE</div>
        <div class="project-title">Unreal Engine Real-Time Experience</div>
        <div class="project-tagline">A real-time rendered environment designed for guest interaction and narrative immersion.</div>
        <div class="project-grid">
          <div class="project-detail">
            <div class="project-detail-label">The Magic</div>
            <p>A fully interactive world where guests' choices shape the visual and narrative environment — real-time rendering enables responses that feel immediate and magical.</p>
          </div>
          <div class="project-detail">
            <div class="project-detail-label">How It Works</div>
            <p>Developed in <strong>Unreal Engine</strong> with custom <strong>JavaScript</strong>-driven UI tools for interaction management. Integrated external hardware inputs for a seamless physical-digital interface.</p>
          </div>
        </div>
        <div class="tech-tags">
          <span class="tech-tag">Unreal Engine</span>
          <span class="tech-tag">JavaScript</span>
          <span class="tech-tag">Blueprints</span>
          <span class="tech-tag">Hardware I/O</span>
        </div>
      </div>

    </div>
  </section>

  <!-- EXPERIENCE -->
  <section>
    <div class="section-label"><span>Experience</span></div>
    <div class="exp-list">
      <div class="exp-card">
        <div>
          <div class="exp-role">Technical Assistant</div>
          <div class="exp-org">UC San Diego</div>
        </div>
        <div class="exp-date">2023 – 2025</div>
        <ul class="exp-bullets">
          <li>Executed technical setups for live events, specializing in <strong>DMX lighting control</strong> and complex <strong>A/V signal routing</strong> — directly applicable to WDI's show control work.</li>
          <li>Collaborated with cross-functional crews (designers, directors, engineers) to ensure seamless, <strong>"invisible" technical execution</strong> — the mark of great experience design.</li>
          <li>Managed real-time troubleshooting under performance conditions, building intuition for <strong>reliable, production-grade systems</strong>.</li>
        </ul>
      </div>
      <div class="exp-card">
        <div>
          <div class="exp-role">Recording Engineer</div>
          <div class="exp-org">UC San Diego</div>
        </div>
        <div class="exp-date">2023 – 2025</div>
        <ul class="exp-bullets">
          <li>Managed <strong>50+ projects</strong> from concept through final delivery, working across multi-microphone configurations and live mixing environments.</li>
          <li>Developed deep fluency in <strong>signal chain design</strong> and audio systems — a technical foundation that informs spatial audio and show control work.</li>
          <li>Operated independently while coordinating with artists and producers, building <strong>cross-disciplinary communication skills</strong> essential for WDI's collaborative model.</li>
        </ul>
      </div>
    </div>
  </section>

  <!-- EDUCATION -->
  <section>
    <div class="section-label"><span>Education</span></div>
    <div class="edu-grid">
      <div class="edu-card">
        <div class="edu-degree">MFA, Creative Computing<br>& Music Technology</div>
        <div class="edu-school">California Institute of the Arts</div>
        <div class="edu-year">Expected 2027</div>
      </div>
      <div class="edu-card">
        <div class="edu-degree">BFA, Interdisciplinary<br>Computing & the Arts</div>
        <div class="edu-school">UC San Diego</div>
        <div class="edu-year">2025</div>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <div class="footer-name">Sandra (Tien-Jo) Chang</div>
    <div class="footer-links">
      <a href="mailto:tienjo918@gmail.com">Email</a>
      <a href="https://www.linkedin.com/in/tienjo918" target="_blank">LinkedIn</a>
      <a href="#">Portfolio</a>
    </div>
  </footer>

</div>

<script>
  // Intersection Observer for scroll reveals
  const sections = document.querySelectorAll('section');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
      }
    });
  }, { threshold: 0.08 });

  sections.forEach(s => observer.observe(s));
</script>

</body>
</html>
