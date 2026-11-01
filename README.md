# SmartStudy — AI-Powered Study Planner

An intelligent, explainable academic study management system built with **React 18 + Vite**, **Express.js**, **Local MongoDB**, and a transparent **Python heuristic AI engine**.

Designed specifically for university students, coursework revision, academic project evaluations, and viva defense presentations.

---

## 🛠️ Architecture & Tech Stack

- **Frontend**: React 18, Vite, Vanilla CSS design system (Dark & Light modes), Lucide React icons
- **Backend API**: Node.js, Express.js, Mongoose ODM, asynchronous child process runner
- **Database**: Local MongoDB Community Server (`mongodb://127.0.0.1:27017/smartstudy`)
- **AI Recommendation Engine**: Python 3 (`backend/ai.py`) implementing weighted multi-criteria heuristic prioritization with fallback subprocess execution

---

## 📂 Project Structure

```text
AI_MINI_Project_SmartStudy/
├── backend/
│   ├── models/
│   │   └── Task.js              # Mongoose schema & validation (title, subject, deadline, etc.)
│   ├── .env                     # Server environment variables (PORT, MONGODB_URI, PYTHON_CMD)
│   ├── .env.example             # Example environment template
│   ├── ai.py                    # Python heuristic recommendation & scoring engine
│   ├── package.json             # Express, Mongoose, CORS, Dotenv dependencies
│   └── server.js                # Express API server, routes, & Python runner
├── frontend/
│   ├── src/
│   │   ├── App.jsx              # Main React SPA with 6 dedicated workspace views
│   │   ├── index.css            # Complete design system tokens, themes, & animations
│   │   └── main.jsx             # React DOM entry point
│   ├── index.html               # HTML template & Google Fonts (DM Sans, Manrope)
│   ├── package.json             # React 18, Lucide React, Vite dependencies
│   └── vite.config.js           # Vite dev server configuration
└── README.md                    # Project documentation
```

---

## 🧠 Explainable AI Heuristic Prioritization Model

Unlike black-box machine learning models, SmartStudy uses a **fully explainable multi-factor heuristic evaluation function**. This makes it ideal for academic evaluations, viva demonstrations, and students who need clear rationale for study recommendations.

### Evaluation Formula

$$\text{Priority Score} = (\text{Urgency} \times 0.50) + (\text{Importance} \times 2.0 \times 0.30) + (\text{Difficulty} \times 2.0 \times 0.20)$$

Simplified:
$$\text{Priority Score} = (\text{Urgency} \times 0.50) + (\text{Importance} \times 0.60) + (\text{Difficulty} \times 0.40)$$

**Total Score Range**: $1.0\text{ to }10.0$ points.

### Factor Breakdown

1. **Deadline Urgency (50% Weight, 0.0 – 5.0 points)**:
   - **Overdue**: $10.0\text{ pts}$ (Tier: Overdue — highlighted at the top of the queue)
   - **Due within 12 hours**: $9.5\text{ pts}$ (Tier: Due Today)
   - **Due within 24 hours**: $9.0\text{ pts}$ (Tier: Due Today)
   - **Due within 3 days (72 hours)**: $7.5\text{ pts}$ (Tier: Due Soon)
   - **Due within 1 week (168 hours)**: $6.0\text{ pts}$ (Tier: Upcoming)
   - **Due within 2 weeks (336 hours)**: $4.0\text{ pts}$ (Tier: Upcoming)
   - **Due > 2 weeks**: $2.0\text{ pts}$ (Tier: Flexible)

2. **Academic Importance (30% Weight, 0.6 – 3.0 points)**:
   - Graded on a scale of $1\text{ to }5$ based on syllabus weight, exam credits, and grade impact:
     - 1 = Supplemental reading
     - 2 = Practice problem set
     - 3 = Standard weekly assignment / quiz
     - 4 = Major lab report / project milestone
     - 5 = Midterm / End-semester final examination

3. **Cognitive Difficulty (20% Weight, 0.4 – 2.0 points)**:
   - Graded on a scale of $1\text{ to }5$ based on cognitive effort and problem complexity:
     - 1 = Quick definition review
     - 2 = Concept reading
     - 3 = Moderate implementation / problem solving
     - 4 = Complex algorithm / multi-step proof
     - 5 = Intensive theoretical derivation / full-stack build

4. **Deterministic Tie-Breaking Rules**:
   - If two tasks have equal Priority Scores, order is resolved deterministically by:
     1. Overdue status (Overdue first)
     2. Exact hours remaining until deadline
     3. Higher Academic Importance
     4. Higher Cognitive Difficulty

---

## ⚡ Core Workspace Views & Features

The application features a modern sidebar navigation with **6 dedicated workspace modules**:

### 1. 📊 Academic Dashboard
- **Welcome & Quick Actions**: Instant access to "+ Add study task" and overall progress tracking.
- **Key Statistics Cards**: Real-time counters for **Total Tasks**, **Completed (%)**, **Pending Tasks** (with overdue warning badges), and **Study Workload** (total pending hours).
- **AI Heuristic Coach Panel**:
  - Highlights your **Top Recommended Task** with a personalized actionable prompt.
