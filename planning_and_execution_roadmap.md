# Timetable Automation System: Task Planning & Execution Roadmap

## Phase 1: Environment & Database Setup
* **Task 1.1: Initialize Git Repository**
    * Create a monorepo structure (e.g., `/frontend` and `/backend`).
* **Task 1.2: Supabase Initialization**
    * Create a new Supabase project.
    * Execute SQL scripts to generate tables: `Rooms`, `Courses`, `Sections`, `Subjects`, `Timetable_Master`.
    * Set up Row Level Security (RLS) policies for admin-only write access.
* **Task 1.3: Backend Base Setup**
    * Initialize Python virtual environment.
    * Install FastAPI, Uvicorn, Pydantic, and Supabase Python Client.
    * Set up `main.py` and basic routing.

## Phase 2: Backend API & Data Ingestion
* **Task 2.1: Pydantic Schema Definition**
    * Define request/response validation models for all entities (Rooms, Subjects, etc.).
* **Task 2.2: CRUD Endpoints**
    * Build `POST`, `GET`, `PUT`, `DELETE` routes for university constraints (saving directly to Supabase).
* **Task 2.3: The Payload Builder**
    * Create an endpoint `/api/generate-timetable` that aggregates all current database constraints into a single algorithm-ready payload.

## Phase 3: The Algorithmic Core (The Solver)
* **Task 3.1: Matrix Initialization**
    * Write Python logic to map the 8x5 daily grid for available rooms and active sections.
* **Task 3.2: Hard Constraint Implementation**
    * Integrate Google OR-Tools (or custom backtracking script).
    * Enforce constraints: No room overlap, Theory=Lecture Hall, Practical=Lab.
* **Task 3.3: Dynamic Constraint Implementation**
    * Logic for dynamic Lunch assignment (Slot 4 or 5 exclusively).
    * Logic for consecutive slot merging (Long lectures/Practicals bridging correctly).
* **Task 3.4: Optimization Pass**
    * Implement sorting logic to push free lectures to Slot 1, Slot 8, or club them adjacent to lunch.

## Phase 4: Frontend Development
* **Task 4.1: Next.js & UI Setup**
    * Initialize Next.js app with Tailwind CSS.
    * Install Shadcn UI components (Forms, Tables, Dialogs, Select).
* **Task 4.2: Data Entry Forms**
    * Build multi-step forms for admin data entry (Add Rooms, Add Subjects, Define Sections).
    * Connect forms to FastAPI CRUD endpoints.
* **Task 4.3: Timetable Visualization Grid**
    * Build a dynamic CSS Grid/Flexbox calendar view.
    * Color-code outputs (e.g., Blue for Theory, Green for Labs, Orange for Lunch).
    * Include filtering (View by Room, View by Section, View by Course).

## Phase 5: Testing & Deployment
* **Task 5.1: Edge-Case Testing**
    * Run the solver against extreme constraints (e.g., exact room capacity matching total students).
* **Task 5.2: Backend Deployment**
    * Deploy FastAPI application to Render.
    * Configure environment variables (Supabase keys, CORS policies).
* **Task 5.3: Frontend Deployment**
    * Deploy Next.js application to Vercel.
    * Link frontend to production Render API URL.
