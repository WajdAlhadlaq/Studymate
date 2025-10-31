<title>StudyMate README</title>
<style>
  body { font-family: Arial, sans-serif; line-height: 1.6; margin: 20px; }
  h1, h2, h3, h4 { margin-top: 1.2em; }
  pre { background: #f4f4f4; padding: 10px; overflow-x: auto; }
  code { background: #f4f4f4; padding: 2px 4px; }
  ul { margin-left: 20px; }
</style>
</head>
<body>

<h1>StudyMate – Full Stack Developer Assignment</h1>

<p><strong>StudyMate</strong> is an AI-powered learning platform that allows students to browse courses and educational materials. An integrated AI assistant provides course recommendations, answers user questions, and helps explore content.</p>

<h2>Table of Contents</h2>
<ul>
  <li><a href="#project-overview">Project Overview</a></li>
  <li><a href="#folder-structure">Folder Structure</a></li>
  <li><a href="#frontend">Frontend</a></li>
  <li><a href="#backend">Backend</a></li>
  <li><a href="#technical-stack">Technical Stack</a></li>
  <li><a href="#devops-setup">DevOps & Setup</a></li>
</ul>

<h2 id="project-overview">Project Overview</h2>
<p>StudyMate allows users to:</p>
<ul>
  <li>Browse courses by category, name, or description.</li>
  <li>Filter courses by difficulty, category, and search terms.</li>
  <li>Get AI-powered assistance for course recommendations and comparisons.</li>
  <li>View detailed course information through responsive cards and modals.</li>
</ul>

<h2 id="folder-structure">Folder Structure</h2>
<pre>
backend/
├─ app/
│  ├─ main.py
│  ├─ db.py
│  ├─ models.py
│  ├─ schemas.py
│  └─ routes/
│     └─ courses.py
frontend/
├─ src/
│  ├─ components/
│  │  ├─ CourseCard.tsx
│  │  ├─ CourseModal.tsx
│  │  ├─ FilterBar.tsx
│  │  └─ SearchBar.tsx
│  ├─ pages/
│  │  └─ Home.tsx
│  └─ services/api.ts
</pre>

<h2 id="frontend">Frontend</h2>

<h3 id="home-component">Home Component</h3>
<p>Displays courses in a responsive grid and handles fetching, filtering, and search using React hooks:</p>
<pre>
const [courses, setCourses] = useState&lt;Course[]&gt;([]);
const [selectedCategory, setSelectedCategory] = useState&lt;string&gt;("All");
const [searchTerm, setSearchTerm] = useState&lt;string&gt;("");
const [selectedCourse, setSelectedCourse] = useState&lt;Course | null&gt;(null);
</pre>

<p>Filters courses by category and search term and displays them using <code>CourseCard</code> components. Clicking a card opens <code>CourseModal</code>.</p>

<h3 id="search--filter">Search & Filter</h3>
<p><strong>SearchBar</strong> filters courses by name or description (case-insensitive).<br>
<strong>FilterBar</strong> filters courses by category and displays counts:</p>
<pre>
const categoryCounts: Record&lt;string, number&gt; = courses.reduce((acc, course) =&gt; {
  acc[course.category] = (acc[course.category] || 0) + 1;
  return acc;
}, {});
const categories = ["All", ...Object.keys(categoryCounts)];
</pre>

<h3 id="coursecard--coursemodal">CourseCard & CourseModal</h3>
<ul>
  <li>Displays course image, title, description, price, duration, difficulty, instructor, rating, enrollment, and category badge.</li>
  <li>Clicking a card opens a modal with detailed course information.</li>
</ul>

<h3 id="ai-assistant">AI Assistant</h3>
<ul>
  <li>Chat interface for users to ask course-related questions.</li>
  <li>Sends messages to backend endpoint <code>/api/ask</code> using <code>axios</code>.</li>
  <li>Distinguishes between user and AI messages.</li>
</ul>

<pre>
interface Message {
  text: string;
  sender: "user" | "ai";
}
</pre>

<h2 id="backend">Backend</h2>

<h3 id="models--schemas">Models & Schemas</h3>
<p>SQLAlchemy models represent the database tables. Pydantic schemas validate and serialize responses:</p>
<pre>
class CourseSchema(BaseModel):
    id: int
    name: str
    description: str
    price: float
    image: str
    duration: int
    difficulty: str
    category: str
    instructor: str | None
    enrollment_count: int
    rating: float

    class Config:
        from_attributes = True
</pre>

<h3 id="database">Database</h3>
<ul>
  <li>PostgreSQL is used as backend.</li>
  <li>SQLAlchemy provides ORM and session management.</li>
  <li><code>get_db()</code> provides DB session per request.</li>
  <li><code>init_db(Base)</code> initializes tables.</li>
</ul>

<h3 id="api-endpoints">API Endpoints</h3>
<ul>
  <li><strong>Courses</strong>
    <ul>
      <li>GET /courses → Fetch all courses with optional filters: <code>search</code>, <code>category</code>, <code>difficulty</code>, <code>sort_by</code>, <code>order</code>.</li>
      <li>GET /courses/{course_id} → Fetch course by ID.</li>
    </ul>
  </li>
  <li><strong>Categories</strong>
    <ul>
      <li>GET /categories → List all categories with counts and average rating.</li>
      <li>GET /categories/{category}/second-highest → Retrieve second-highest rated course in a category.</li>
    </ul>
  </li>
  <li><strong>AI Chat</strong>
    <ul>
      <li>POST /api/ask → Send message to AI assistant. Optional <code>course_context</code> filters by course ID.</li>
    </ul>
  </li>
</ul>

<h2 id="technical-stack">Technical Stack</h2>
<ul>
  <li>Frontend: React.js + TypeScript, Bootstrap</li>
  <li>Backend: FastAPI, SQLAlchemy, Pydantic, OpenAI API</li>
  <li>Database: PostgreSQL</li>
  <li>AI/LLM: OpenAI API integration</li>
</ul>

<h2 id="devops-setup">DevOps & Setup</h2>
<ul>
  <li>Docker Compose services: PostgreSQL, FastAPI, React frontend</li>
  <li>Environment variables stored in <code>.env</code> (<code>.env.example</code> provided)</li>
  <li>Startup command: <code>docker-compose up</code></li>
  <li>Automatic database initialization with sample data</li>
</ul>

</body>

