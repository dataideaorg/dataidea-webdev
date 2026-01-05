---
hide:
  - navigation
  - toc
---

<style>
/* Page container */
.md-typeset {
  max-width: 1200px;
}

/* Hero section */
.hero-section {
  text-align: center;
  padding: 3rem 1rem 2rem;
  margin-bottom: 2rem;
  border-bottom: 1px solid #303030;
}

.hero-section h1 {
  font-size: 2.25rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: #e5e5e5;
  letter-spacing: -0.02em;
  line-height: 1.2;
}

.hero-section p {
  font-size: 1rem;
  color: #b0b0b0;
  max-width: 700px;
  margin: 0 auto;
  line-height: 1.6;
}

/* Section titles */
.section-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: #e5e5e5;
  margin: 2rem 0 1.5rem;
  text-align: center;
  letter-spacing: -0.01em;
}

/* Course grid */
.course-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  margin: 2rem auto 3rem;
  padding: 0 1rem;
  max-width: 1400px;
}

/* Course cards - clean and minimal */
.course-card {
  background: linear-gradient(135deg, #242424 0%, #1c1c1c 100%);
  border: 1px solid #2a2a2a;
  border-radius: 12px;
  padding: 1.5rem 1.25rem;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
}

.course-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.35);
  border-color: #3a3a3a;
}

/* Card title */
.course-card h3 {
  margin: 0 0 0.75rem 0;
  color: #e5e5e5;
  font-size: 1.25rem;
  font-weight: 600;
  letter-spacing: -0.01em;
}

/* Card description */
.course-card p {
  color: #a0a0a0;
  margin-bottom: 1rem;
  font-size: 0.875rem;
  line-height: 1.5;
  max-width: 95%;
}

/* Course meta badge */
.course-meta {
  color: #808080;
  font-size: 0.75rem;
  margin-bottom: 1.25rem;
  padding: 0.35rem 0.85rem;
  background-color: #1a1a1a;
  border-radius: 16px;
  border: 1px solid #282828;
  display: inline-block;
  font-weight: 500;
}

/* Buttons */
.course-buttons {
  display: flex;
  flex-direction: column;
  gap: 0.65rem;
  width: 100%;
}

.course-btn {
  width: 100%;
  padding: 0.65rem 1.25rem;
  border-radius: 50px;
  text-decoration: none;
  text-align: center;
  font-size: 0.85rem;
  font-weight: 600;
  transition: all 0.25s ease;
  border: 1.5px solid;
  display: inline-block;
  letter-spacing: 0.3px;
  color: inherit;
}

.course-btn:link,
.course-btn:visited,
.course-btn:hover,
.course-btn:active {
  color: inherit;
  text-decoration: none;
}

.course-btn-primary {
  background-color: #ffffff;
  border-color: #ffffff;
  color: black;
}

.course-btn-primary:hover {
  background-color: #f0f0f0;
  border-color: #f0f0f0;
  color: #000000;
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(255, 255, 255, 0.15);
}

.course-btn-secondary {
  background-color: transparent;
  border-color: #505050;
  color: #ffffff;
}

.course-btn-secondary:hover {
  background-color: rgba(255, 255, 255, 0.05);
  border-color: #606060;
  color: #ffffff;
  transform: translateY(-1px);
}

/* Section headers */
.md-typeset h2 {
  font-size: 2rem;
  font-weight: 600;
  margin-top: 3rem;
  margin-bottom: 1.5rem;
  color: #e5e5e5;
  letter-spacing: -0.02em;
  border-bottom: 2px solid #353535;
  padding-bottom: 0.75rem;
}

/* Learning path section */
.md-typeset h2 + ol,
.md-typeset h2 + ul {
  background: linear-gradient(135deg, #252525 0%, #1f1f1f 100%);
  border: 1px solid #353535;
  border-radius: 8px;
  padding: 1.5rem 1.5rem 1.5rem 2.5rem;
  margin: 1.5rem 0;
}

.md-typeset h2 + ol li,
.md-typeset h2 + ul li {
  margin-bottom: 0.75rem;
  color: #d0d0d0;
  line-height: 1.6;
}

.md-typeset h2 + ol li:last-child,
.md-typeset h2 + ul li:last-child {
  margin-bottom: 0;
}

/* Responsive design */
@media (max-width: 1024px) {
  .course-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .hero-section h1 {
    font-size: 2rem;
  }
  
  .hero-section p {
    font-size: 1rem;
  }
  
  .section-title {
    font-size: 1.5rem;
  }
  
  .course-grid {
    grid-template-columns: 1fr;
    gap: 1.25rem;
  }
  
  .course-card {
    padding: 1.25rem 1rem;
  }
  
  .course-card h3 {
    font-size: 1.15rem;
  }
  
  .course-card p {
    font-size: 0.8rem;
  }
}
</style>

<div class="hero-section">
<h1>Programming for Web Development</h1>
<p>This documentation covers essential technologies and tools you need to build modern web applications, and become a confident Fullstack Web Developer</p>
</div>

<h2 class="section-title">Available Courses</h2>

<div class="course-grid">

<div class="course-card">
<h3>HTML</h3>
<p>Master the foundation of web development - HTML (HyperText Markup Language).</p>
<div class="course-meta">6 comprehensive tutorials</div>
<div class="course-buttons">
<a href="https://forms.gle/CPL4Rs2pmuR4yToKA" target="_blank" class="course-btn course-btn-primary" style="color: black">Enroll Now</a>
<a href="HTML/01_introduction/" class="course-btn course-btn-secondary">Start Learning</a>
</div>
</div>

<div class="course-card">
<h3>CSS</h3>
<p>Learn to style and design beautiful websites with CSS (Cascading Style Sheets).</p>
<div class="course-meta">6 comprehensive tutorials</div>
<div class="course-buttons">
<a href="https://forms.gle/CPL4Rs2pmuR4yToKA" target="_blank" class="course-btn course-btn-primary" style="color: black">Enroll Now</a>
<a href="CSS/01_introduction/" class="course-btn course-btn-secondary">Start Learning</a>
</div>
</div>

<div class="course-card">
<h3>JavaScript</h3>
<p>Add interactivity and dynamic behavior to your websites with JavaScript.</p>
<div class="course-meta">6 comprehensive tutorials</div>
<div class="course-buttons">
<a href="https://forms.gle/CPL4Rs2pmuR4yToKA" target="_blank" class="course-btn course-btn-primary" style="color: black" >Enroll Now</a>
<a href="JavaScript/01_introduction/" class="course-btn course-btn-secondary">Start Learning</a>
</div>
</div>

<div class="course-card">
<h3>Git</h3>
<p>Learn version control with Git and GitHub - essential skills for modern software development.</p>
<div class="course-meta">6 comprehensive tutorials</div>
<div class="course-buttons">
<a href="https://forms.gle/CPL4Rs2pmuR4yToKA" target="_blank" class="course-btn course-btn-primary" style="color: black">Enroll Now</a>
<a href="Git/01_introduction/" class="course-btn course-btn-secondary">Start Learning</a>
</div>
</div>

<div class="course-card">
<h3>SQL</h3>
<p>Master SQL for working with relational databases and managing data effectively.</p>
<div class="course-meta">6 comprehensive tutorials</div>
<div class="course-buttons">
<a href="https://forms.gle/CPL4Rs2pmuR4yToKA" target="_blank" class="course-btn course-btn-primary" style="color: black">Enroll Now</a>
<a href="SQL/01_introduction/" class="course-btn course-btn-secondary">Start Learning</a>
</div>
</div>

<div class="course-card">
<h3>Python</h3>
<p>Learn Python programming from basics to advanced topics, including data science libraries.</p>
<div class="course-meta">Comprehensive tutorial series</div>
<div class="course-buttons">
<a href="https://forms.gle/CPL4Rs2pmuR4yToKA" target="_blank" class="course-btn course-btn-primary" style="color: black">Enroll Now</a>
<a href="Python/" class="course-btn course-btn-secondary">Start Learning</a>
</div>
</div>

<div class="course-card">
<h3>Django</h3>
<p>Build powerful web applications with Django, a high-level Python web framework.</p>
<div class="course-meta">6 comprehensive tutorials</div>
<div class="course-buttons">
<a href="https://forms.gle/CPL4Rs2pmuR4yToKA" target="_blank" class="course-btn course-btn-primary" style="color: black">Enroll Now</a>
<a href="Django/01_introduction/" class="course-btn course-btn-secondary">Start Learning</a>
</div>
</div>

</div>
