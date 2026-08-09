# Timetable Automation System: Problem Statement & Core Solution

## 1. Problem Statement
* **The Trigger:** High influx of freshers exceeding the capacity of available physical infrastructure (lecture halls and labs).
* **Current Compromise:** Basic subjects (e.g., Entrepreneurship) are being pushed online due to scheduling gridlock rather than pedagogical choice.
* **The Core Issue:** Manual timetable creation is inefficient, error-prone, and fails to optimally utilize available rooms. It struggles to balance multiple academic years, varying room capacities, lab divisions, and daily break constraints.

## 2. Proposed Solution
A web-based automated scheduling platform that ingests university structural data, resource availability, and time constraints to programmatically generate conflict-free, highly optimized timetables. 

## 3. Structural Hierarchy
* **Academic Level:** Supports multiple Academic Years running concurrently within a block.
* **Course Level:** Maps specific courses to respective academic years.
* **Section Level:** ~70 students per section.
    * **Theory:** Handled as a complete Section (70 students).
    * **Practical:** Handled as divided groups (Group A and Group B, ~35 students each).
* **Room Management:** 
    * *Lecture Halls:* Tagged for Theory (Capacity: 70+).
    * *Practical Labs:* Tagged for Practicals (Capacity: 35+).

## 4. The Daily Grid (8 Slots)
| Slot | Time | Type | Long Lecture / Bridging Rules |
| :--- | :--- | :--- | :--- |
| **1** | 09:30 - 10:20 | Regular | Can merge with Slot 2 |
| **2** | 10:20 - 11:10 | Regular | **Can merge with Slot 3** (10m break inside) |
| *Break* | *11:10 - 11:20* | *10 Min Campus Break* | - |
| **3** | 11:20 - 12:10 | Regular | Can merge with Slot 4 |
| **4** | 12:10 - 01:00 | **Lunch A** / Regular | - |
| **5** | 01:00 - 01:50 | **Lunch B** / Regular | **Can merge with Slot 6** (5m break inside) |
| *Break* | *01:50 - 01:55* | *5 Min Campus Break* | - |
| **6** | 01:55 - 02:45 | Regular | Can merge with Slot 7 |
| **7** | 02:45 - 03:35 | Regular | Can merge with Slot 8 |
| **8** | 03:35 - 04:25 | Regular | - |

## 5. Algorithmic Constraints & Optimization Rules
* **Theory vs. Practical Routing:**
    * Theory subjects are assigned exclusively to Lecture Halls (Full section).
    * Practical subjects are assigned exclusively to Labs (Simultaneous or alternating blocks for Group A & Group B).
* **Lunch Assignment:**
    * Hard constraint: Every section MUST have exactly one empty slot for lunch per day.
    * Dynamic allocation: Assigned to either Slot 4 (12:10 - 1:00) OR Slot 5 (1:00 - 1:50).
* **Free Lecture Distribution:**
    * **Quota:** 2 to 4 designated free lectures per week (independent of lunch).
    * **Optimization Priority 1 (Clubbing):** Group free lectures into blocks (e.g., all 4 on one day, or two blocks of 2).
    * **Optimization Priority 2 (Strategic Placement):** If unable to club, place them at high-value times:
        * Start of the day (Slot 1) -> Late arrival.
        * End of the day (Slot 8) -> Early departure.
        * Adjacent to Lunch (Slot 3 or Slot 6) -> Extended midday break.
timetable_problem_statement.md
Displaying timetable_problem_statement.md.
