# job-scheduler-automation
```markdown

# Job Scheduler & Automation System



A simplified internal automation engine for scheduling and running background tasks (e.g., sending emails, generating reports, syncing data). Features include job creation, real-time tracking, status simulation, and outbound webhook triggers on completion.



**Live Demo**: [Deployed URL if available]  

**Repository**: [Your GitHub Repo Link]



## Repository Structure

```

job-scheduler-automation/

├── backend/

│   ├── server.js

│   ├── db.js

│   ├── package.json

│   └── .env (gitignored)

├── frontend/

│   ├── src/

│   │   ├── components/

│   │   │   ├── JobForm.jsx

│   │   │   ├── JobTable.jsx

│   │   │   └── JobDetail.jsx

│   │   ├── App.jsx

│   │   ├── main.jsx

│   │   └── index.css

│   ├── index.html

│   ├── tailwind.config.js

│   ├── vite.config.js

│   └── package.json

├── README.md

└── .gitignore

```



## Tech Stack

- **Frontend**: React.js (Vite), Tailwind CSS, Axios, react-syntax-highlighter

- **Backend**: Node.js, Express.js

- **Database**: SQLite (better-sqlite3)

- **Other**: Axios (for webhook), Tailwind for futuristic glassmorphic UI with animated blobs



## Database Schema

**Table: jobs**



| Column      | Type                  | Description                          | Default      |

|-------------|-----------------------|--------------------------------------|--------------|

| id          | INTEGER (PK)          | Auto-increment primary key           | AUTO         |

| taskName    | TEXT                  | Name of the task                     | NOT NULL     |

| payload     | TEXT                  | JSON string payload                  | NOT NULL     |

| priority    | TEXT                  | Low / Medium / High                  | NOT NULL     |

| status      | TEXT                  | pending / running / completed        | 'pending'    |

| createdAt   | DATETIME              | Creation timestamp                   | CURRENT_TIMESTAMP |

| updatedAt   | DATETIME              | Last update timestamp                | CURRENT_TIMESTAMP |



**SQL Creation** (auto-executed on startup):

```sql

CREATE TABLE IF NOT EXISTS jobs (

  id INTEGER PRIMARY KEY AUTOINCREMENT,

  taskName TEXT NOT NULL,

  payload TEXT NOT NULL,

  priority TEXT NOT NULL,

  status TEXT DEFAULT 'pending',

  createdAt DATETIME DEFAULT CURRENT_TIMESTAMP,

  updatedAt DATETIME DEFAULT CURRENT_TIMESTAMP

);

```



**ER Diagram** (Text representation):

```

jobs

├── id (PK)

├── taskName

├── payload (JSON)

├── priority

├── status

├── createdAt

└── updatedAt

```



## Architecture Explanation

- **Monorepo Structure**: Separate `/frontend` and `/backend` folders for clear separation.

- **Frontend**: React app with Vite. Uses Axios to call backend APIs (proxied via Vite for development). Polls `/jobs` every 3 seconds for real-time status updates.

- **Backend**: Express server with REST APIs. SQLite database for persistence. Job running simulated with `setTimeout` (3s delay). On completion, sends POST webhook.

- **Communication**: Frontend → Backend via `/api/*` (proxied). Webhook → External service (webhook.site).

- **Styling**: Futuristic glassmorphic design with animated background blobs, floating labels, glow effects, custom scrollbars, and gradient buttons.



## Setup Instructions

### Prerequisites

- Node.js (v18+)

- npm



### Backend

1. `cd backend`

2. `npm install`

3. Create `.env`:

   ```

   PORT=5000

   WEBHOOK_URL=https://webhook.site/your-unique-id

   ```

4. Start: `node server.js` → Runs on http://localhost:5000

   - Database `jobs.db` created automatically.



### Frontend

1. `cd frontend`

2. `npm install`

3. Start: `npm run dev` → Runs on http://localhost:5173

   - Proxied API calls to backend.



### Deployment (Optional Bonus)

- Frontend: Vercel / Netlify (build with `npm run build`)

- Backend: Render / Railway (set env vars)



## API Documentation

Base URL: `http://localhost:5000` (or deployed URL)



| Method | Endpoint         | Description                          | Body / Params                          | Response |

|--------|------------------|--------------------------------------|----------------------------------------|----------|

| POST   | `/jobs`          | Create new job                       | `{ taskName, payload (object), priority }` | `{ id }` |

| GET    | `/jobs`          | List all jobs                        | -                                      | Array of jobs |

| GET    | `/jobs/:id`      | Get job details                      | -                                      | Job object (payload parsed) |

| POST   | `/run-job/:id`   | Simulate running job (3s delay)      | -                                      | `{ message: 'Job started' }` |



**Error Handling**: Returns 400/404 with `{ error }` message.



## How Webhook Works

- When a job status changes to "completed":

  - Backend sends `POST` request to `WEBHOOK_URL` (from .env).

  - Payload:

    ```json

    {

      "jobId": number,

      "taskName": string,

      "priority": string,

      "payload": object,

      "completedAt": timestamp

    }

    ```

  - Success/failure logged to console.

- Test with https://webhook.site → Create unique URL, paste in .env, run jobs → See requests.



## Features Overview

- Create jobs with JSON payload validation

- Real-time dashboard with search, filters (status/priority), card-based list

- Run simulation with status updates (pending → running → completed)

- Detailed view with syntax-highlighted JSON

- Responsive, modern UI with glassmorphism, animated blobs, glow effects



## AI Usage Log

- **AI Tools Used**: Grok (xAI)

- **Model**: Grok 4

- **Prompts Used**: Full conversation history (provided step-by-step refinements for structure, functionality, styling)

- **Parts AI Helped With**:

  - Architecture & initial code structure

  - Backend Express endpoints & SQLite queries

  - Frontend components (form, table/cards, modal)

  - Styling upgrades (glassmorphism, blobs, floating labels, glows)

  - Bug fixes & enhancements (polling, validation, refresh)

  - Documentation outline

- Manual adjustments made for functionality, responsiveness, and project requirements.



© 2026 Dotix Technologies • Job Scheduler v2.0

```



This is the complete, professional README.md content. Copy-paste it into your root `README.md`. It covers **all required sections** exactly as specified in the test, with clear formatting, tables, and code blocks for readability. Submit with your GitHub repo!

