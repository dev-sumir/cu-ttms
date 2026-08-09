# Timetable Automation System: Tech Stack & Architecture

## 1. Modern Tech Stack Selection
* **Frontend:** Next.js (React), Tailwind CSS, Shadcn UI. (Modern, fast, component-driven, completely replaces old HTML/CSS).
* **Backend:** FastAPI (Python). (High performance, excellent for mathematical/algorithmic computation).
* **Database:** PostgreSQL hosted on Supabase. (Highly relational structure required for timetable entities).
* **Hosting:** Vercel (Frontend) and Render (Backend API).
* **Algorithm Engine:** Google OR-Tools (Constraint Programming) or a custom Python backtracking/genetic algorithm.

## 2. Core Database Schema
* **Rooms:** `id`, `room_number`, `type` (Lecture / Lab), `capacity`
* **Courses:** `id`, `course_name`, `year_level`
* **Sections:** `id`, `course_id`, `section_name` (e.g., A, B), `total_students`
* **Subjects:** `id`, `course_id`, `subject_name`, `type` (Theory / Practical), `lectures_per_week`, `is_long` (Boolean)
* **Timetable_Master (The Output):** `id`, `section_id`, `subject_id`, `room_id`, `day_of_week` (Mon-Fri), `slot_number` (1-8), `group` (Full / Grp A / Grp B)

## 3. The Execution Logic (How It Works)
**Phase 1: Ingestion**
* Admin inputs all parameters into the Next.js dashboard.
* Frontend validates data and posts a structured JSON payload to the FastAPI endpoint.

**Phase 2: Constraint Mapping (The Python Backend)**
* The algorithm creates an empty 8x5 grid (8 slots, 5 days) for every Section and every Room.
* **Hard Constraints applied first:** 
    * No room double-booking.
    * No teacher double-booking.
    * Theory -> Lecture Hall only.
    * Practical -> Lab only.

**Phase 3: The Solver Sequence**
1. **Lock Lunch:** Randomly assign Slot 4 or Slot 5 as 'LUNCH' for each section.
2. **Lock Long Blocks:** Place 2-hour practicals and long theory lectures first (hardest to fit). Ensure they bridge correctly (1&2, 2&3, 3&4, 5&6, 6&7, 7&8).
3. **Fill Standard Blocks:** Distribute remaining single-slot theory lectures.
4. **Optimize Free Lectures:** Identify empty slots. Run a balancing pass to club them together or push them to Slot 1 / Slot 8.

**Phase 4: Output**
* Algorithm returns a mapped JSON array.
* Frontend consumes JSON and renders a visual, color-coded weekly calendar grid.
