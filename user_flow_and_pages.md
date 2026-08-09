# Timetable Automation System: User Flow & Pages

## 1. Authentication & Onboarding
* **`/login`**: Simple admin authentication.
* **`/dashboard`**: High-level metrics (Total Rooms, Active Sections, Pending Schedules)

## 2. Setup Wizard (Data Entry)
* **`/setup/infrastructure`**
    * **Components:** Data table to Add/Edit/Delete Rooms.
    * **Fields:** Room Number, Type (Lecture Hall / Lab), Capacity.
* **`/setup/academics`**[cite: 6]
    * **Components:** Multi-step form for Academic Hierarchy.
    * **Step 1:** Define Year & Course.
    * **Step 2:** Define Sections (auto-calculates Group A / Group B for labs).
    * **Step 3:** Assign Subjects to Sections (Theory/Practical, lectures per week, long lecture flag).

## 3. The Generator
* **`/generate`**
    * **Components:** A simple interface with a large "Run Algorithm" action button.
    * **State:** Displays a loading state with progress steps (e.g., "Mapping Rooms...", "Assigning Lunches...", "Resolving Conflicts...").
    * **Output:** Success/Failure toast notification. If successful, redirects to the viewer.

## 4. Timetable Viewer & Export
* **`/timetable`**
    * **Components:** Large 5-day x 8-slot interactive CSS grid.
    * **Filters (Crucial):** Dropdowns to view timetable by:
        * Specific Section (e.g., "CSE 2nd Year - Sec A")
        * Specific Room (e.g., "Lecture Hall 401")
    * **Actions:** "Export to PDF" / "Export to Excel" buttons.
