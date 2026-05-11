<svelte:head>
  <title>About Me</title>
</svelte:head>

<div class="about-container">
  <h1>About Me</h1>

  <div class="about-content">
    <div class="profile-section">
      <h2>👨‍💻 Developer Profile</h2>
      <p>
        Hello! I'm a passionate software developer currently exploring the world of modern web
        development with Svelte and SvelteKit. This lab exercise is part of my journey in COMPSCI
        719, where I'm learning about building multi-page applications with routing and layouts.
      </p>
    </div>

    <div class="skills-section">
      <h2>🛠️ Technical Skills</h2>
      <ul>
        <li>JavaScript & TypeScript</li>
        <li>Svelte & SvelteKit</li>
        <li>HTML5 & CSS3</li>
        <li>Node.js</li>
        <li>Git & Version Control</li>
        <li>Responsive Web Design</li>
      </ul>
    </div>

    <div class="interests-section">
      <h2>🎯 Interests</h2>
      <p>
        I'm particularly interested in front-end development, user experience design, and creating
        efficient, maintainable web applications. I enjoy learning new frameworks and staying
        up-to-date with the latest web development trends.
      </p>
    </div>

    <div class="contact-section">
      <h2>📫 Get In Touch</h2>
      <p>
        Feel free to connect with me to discuss web development, technology, or any interesting
        projects!
      </p>
    </div>
  </div>
</div>

<style>
  .about-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 2rem;
  }

  .about-content {
    display: flex;
    flex-direction: column;
    gap: 2rem;
  }

  .profile-section,
  .skills-section,
  .interests-section,
  .contact-section {
    background: #f8f9fa;
    padding: 1.5rem;
    border-radius: 8px;
    border-left: 4px solid #4caf50;
  }

  h1 {
    color: #2e7d32;
    text-align: center;
    margin-bottom: 2rem;
    font-size: 2.5rem;
  }

  h2 {
    color: #388e3c;
    margin-top: 0;
    margin-bottom: 1rem;
    font-size: 1.5rem;
  }

  p {
    line-height: 1.6;
    color: #333;
    margin-bottom: 1rem;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    background: #e8f5e8;
    padding: 0.5rem 1rem;
    margin: 0.5rem 0;
    border-radius: 4px;
    color: #2e7d32;
    font-weight: 500;
  }

  @media (max-width: 768px) {
    .about-container {
      padding: 1rem;
    }

    h1 {
      font-size: 2rem;
    }
  }
</style>
