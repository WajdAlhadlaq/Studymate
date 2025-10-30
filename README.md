<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>StudyMate App Documentation</title>
  <style>
    body { font-family: Arial, sans-serif; line-height: 1.6; padding: 20px; background: #f9f9f9; }
    pre { background: #eee; padding: 10px; overflow-x: auto; }
    code { font-family: monospace; color: #c7254e; }
    h1, h2, h3, h4 { color: #333; }
    h1 { border-bottom: 2px solid #333; padding-bottom: 5px; }
    section { margin-bottom: 30px; }
  </style>
</head>
<body>

<h1>StudyMate App Documentation</h1>

<p>StudyMate is a full-stack web application built with <strong>React</strong> for the front-end and <strong>FastAPI</strong> for the back-end. 
It allows users to explore, filter, and learn about programming courses and interact with an AI assistant for guidance.</p>

<hr>

<h2>Backend (<code>backend/</code> directory)</h2>

<section>
<h3>1. <code>main.py</code></h3>
<p><strong>Purpose:</strong> Entry point of the backend API.</p>
<p><strong>Responsibilities:</strong></p>
<ul>
  <li>Initialize FastAPI app.</li>
  <li>Add CORS middleware to allow requests from React frontend (<code>localhost:3000</code>).</li>
  <li>Include routes for courses (<code>courses.router</code>) and AI assistant (<code>/api/ask</code>).</li>
  <li>Initialize the database tables.</li>
  <li>Define models for request/response of AI chat endpoint (<code>ChatRequest</code>, <code>ChatResponse</code>).</li>
  <li>Provide a health check endpoint (<code>/health</code>) for monitoring.</li>
</ul>
<p><strong>Notes:</strong> Handles communication between the AI (OpenAI API) and the frontend, including fetching courses for context.</p>
</section>

<section>
<h3>2. <code>routes/courses.py</code></h3>
<p><strong>Purpose:</strong> Defines REST API endpoints related to courses.</p>
<ul>
  <li>Fetch all courses (<code>GET /courses</code>).</li>
  <li>Fetch a single course by ID (<code>GET /courses/{id}</code>).</li>
  <li>Optional endpoints for adding/updating courses if needed.</li>
</ul>
<p>Handles CRUD operations on the course database table.</p>
</section>

<section>
<h3>3. <code>db.py</code></h3>
<p><strong>Purpose:</strong> Database connection and initialization.</p>
<ul>
  <li>Configure SQLAlchemy engine and session.</li>
  <li>Define <code>init_db()</code> to create all tables if they don’t exist.</li>
  <li>Provide <code>get_db()</code> dependency for FastAPI routes.</li>
</ul>
</section>

<section>
<h3>4. <code>models.py</code></h3>
<p><strong>Purpose:</strong> Defines database models using SQLAlchemy.</p>
<p>Example: <code>Course</code> model with attributes: <code>id, name, description, price, image, duration, difficulty, category, instructor, rating, enrollment_count, time_stamp</code>.</p>
</section>

<section>
<h3>5. <code>ai.py</code> (optional)</h3>
<p><strong>Purpose:</strong> AI assistant logic.</p>
<ul>
  <li>Handles <code>/api/ask</code> POST requests from the frontend.</li>
  <li>Uses OpenAI API to generate answers.</li>
  <li>Optionally fetches courses from the database to provide context to AI.</li>
</ul>
</section>

<section>
<h3>6. <code>.env</code></h3>
<p><strong>Purpose:</strong> Store environment variables securely.</p>
<ul>
  <li><code>OPENAI_API_KEY</code> → API key for OpenAI.</li>
  <li><code>DATABASE_URL</code> → Connection string for your database.</li>
</ul>
<p>Never commit this file to GitHub.</p>
</section>

<hr>

<h2>Frontend (<code>src/</code> directory)</h2>

<section>
<h3>1. <code>components/CourseCard.tsx</code></h3>
<p>Displays a single course in a card format with image, name, description, instructor, rating, and price. Clickable to open <code>CourseModal</code>.</p>
</section>

<section>
<h3>2. <code>components/CourseModal.tsx</code></h3>
<p>Shows detailed course info in a popup/modal: image, instructor, rating, enrollment, description, duration, difficulty, last updated. Uses Bootstrap Modal.</p>
</section>

<section>
<h3>3. <code>components/FilterBar.tsx</code></h3>
<p>Filter courses by category. Displays buttons for all categories including “All”. Shows count of courses in each category. Calls a callback when a category is selected.</p>
</section>

<section>
<h3>4. <code>components/SearchBar.tsx</code></h3>
<p>Input field to search courses by name or description. Updates parent state via <code>onSearchChange</code>.</p>
</section>

<section>
<h3>5. <code>components/AIAssistant.tsx</code></h3>
<p>Chat interface for AI assistant. Maintains chat messages, sends questions to backend <code>/api/ask</code>, displays AI responses as chat bubbles, shows loading indicator, and auto-scrolls to the bottom.</p>
</section>

<section>
<h3>6. <code>pages/Home.tsx</code></h3>
<p>Main page of the app displaying courses. Fetches courses from backend, filters them by category and search term, shows course cards in a grid, and opens <code>CourseModal</code> when a course is selected. Integrates <code>SearchBar</code> and <code>FilterBar</code>.</p>
</section>

<section>
<h3>7. <code>services/api.ts</code></h3>
<p>API helper functions to fetch courses and interact with backend endpoints. Keeps HTTP requests centralized.</p>
</section>

<section>
<h3>8. <code>index.tsx / App.tsx</code></h3>
<p>App entry point. Mounts <code>Home</code> component and wraps app with global providers if needed.</p>
</section>

<section>
<h3>9. <code>App.css</code></h3>
<p>Custom styling. Mostly uses Bootstrap with optional overrides.</p>
</section>

<section>
<h3>10. <code>types.d.ts</code> (optional)</h3>
<p>TypeScript interfaces for shared types (e.g., <code>Course</code>).</p>
</section>

<hr>

<h2>Folder Structure Overview</h2>
<pre>
backend/
  main.py
  routes/
    courses.py
  db.py
  models.py
  ai.py
  .env

frontend/src/
  components/
    CourseCard.tsx
    CourseModal.tsx
    FilterBar.tsx
    SearchBar.tsx
    AIAssistant.tsx
  pages/
    Home.tsx
  services/
    api.ts
  App.tsx
  index.tsx
  App.css
</pre>

</body>
</html>
