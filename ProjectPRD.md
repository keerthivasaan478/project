

## **Automated Fleet Maintenance Management System Product Requirements Document (PRD)**

### **Section 1: Goals and Background Context**

#### **Goals**

*   Automate the generation of monthly maintenance tasks based on vehicle service intervals and service history.
*   Implement an intelligent task assignment system that considers technician availability, location, and workload.
*   Provide technicians with a clear, reliable, and efficient digital interface to view assigned tasks and record detailed maintenance data, including photos and parts used.
*   Develop an interactive, real-time dashboard for management to monitor overdue tasks, technician workload, and view completed maintenance records.
*   Centralize all vehicle fleet data to create a single source of truth for efficient management and tracking.

#### **Background Context**

A logistics company is seeking to modernize its vehicle fleet maintenance operations. The current process is likely manual, leading to inefficiencies, missed services, unbalanced technician workloads, and a lack of real-time visibility. This Automated Fleet Maintenance Management System will introduce automation and data-driven insights to reduce administrative overhead, improve maintenance compliance, ensure operational readiness of the fleet, and provide clear metrics for performance tracking.

### **Section 2: Requirements**

#### **Functional**

1.  **FR1:** The system shall store and manage a database of fleet vehicles, including the fields: Vehicle ID, Vehicle Type, Location Base, Mileage, Last Service Date, and Service Interval. The database must be pre-populated with 8-12 sample vehicles.
2.  **FR2:** The system shall have a database for Technicians, including fields for Technician ID, Name, and assigned Location Base (Depot).
3.  **FR3:** The system shall maintain a predefined list of maintenance parts (e.g., Oil filter, Brake pads, Tires) for selection in the maintenance form.
4.  **FR4:** The system shall provide a user-initiated action (e.g., a "Generate Tasks" button) to create all required maintenance tasks for the upcoming month.
5.  **FR5:** The task generation logic must create tasks for a vehicle when its next service date (calculated from 'Last Service Date' + 'Service Interval') falls within the next calendar month. This process must be idempotent, preventing duplicate task creation.
6.  **FR6:** The system shall automatically assign all newly generated tasks to available technicians.
7.  **FR7:** The assignment logic must not assign a task to a technician who already has 3 or more active (status of 'Assigned' or 'In Progress') tasks.
8.  **FR8:** The assignment logic must only assign tasks to technicians whose Location Base matches the vehicle's Location Base.
9.  **FR9:** The assignment logic must prioritize assigning tasks to the technician with the fewest active tasks at that location. If no technician is available, the task status must be set to 'Unassigned - Awaiting Capacity'.
10. **FR10:** Technicians must be able to view a list of all tasks currently assigned to them.
11. **FR11:** The maintenance form must allow for the upload of "Before" and "After" photos, which are required for completion.
12. **FR12:** The form must allow for selecting multiple parts used from a predefined list and specifying a quantity for each. This usage must be logged in a `parts_log` table.
13. **FR13:** The form must include a checkbox and a text field for the technician to type their full name, serving as a digital signature of completion.
14. **FR14:** The form must support a "Save as Draft" functionality.
15. **FR15:** The system shall provide a dashboard for managers.
16. **FR16:** The dashboard must display a real-time, clickable count of all overdue maintenance tasks.
17. **FR17:** The dashboard must display the current workload (number of active tasks) for each technician.
18. **FR18:** The dashboard must display a view of recently completed tasks, including before/after photos and parts used, with an option to control the number of items shown.

#### **Non-Functional**

1.  **NFR1:** The application must be accessible and fully functional on both desktop and tablet/mobile web browsers.
2.  **NFR2:** The system's API endpoints should respond in under 500ms for typical requests.
3.  **NFR3:** The application must be intuitive, requiring minimal training for a new technician to use effectively.
4.  **NFR4:** For the initial version, vehicle, technician, and parts data will be populated directly into the database. A user-facing admin interface for managing this data is out of scope for the MVP.

### **Section 3: User Interface Design Goals**

#### **Overall UX Vision**

The application must be efficient, clear, and reliable. The system must be resilient to intermittent network connectivity, ensuring no data is lost during form submission.

#### **Key Interaction Paradigms**

*   **Dashboard-centric (for Managers):** The primary interaction for managers will be viewing a dashboard with powerful filtering and sorting capabilities.
*   **Task-list driven (for Technicians):** The primary interaction for technicians will be viewing a list of assigned tasks with simple search and filtering.

#### **Core Screens and Views**

1.  **Dashboard View:** A single-page view prioritizing urgent information (Overdue Tasks), followed by key metrics. Must include controls to filter all data by Depot.
2.  **Technician Task List:** A simple list view of assigned tasks, sorted by priority, with a search function for Vehicle ID.
3.  **Maintenance Task Form:** A detailed form for a single task, allowing data input, photo uploads, and completion sign-off.

#### **Target Device and Platforms**

*   **Platform:** Web Responsive.
*   **Special Considerations:** The design must handle low-connectivity scenarios gracefully, queuing submissions until connectivity is restored.

### **Section 4: Technical Assumptions**

#### **Repository Structure**

*   **Monorepo:** A single repository will be used, configured with a workspace management tool (e.g., Nx) from the start. The CI/CD pipeline must be configured for scoped builds and tests.

#### **Service Architecture**

*   **Modular Monolith:** A single backend service will handle all business logic. The architecture must enforce a clear modular structure, prohibiting direct cross-module database queries.

#### **Testing Requirements**

*   **Unit + Integration + Critical E2E:** The project requires unit tests, integration tests, and one critical-path End-to-End (E2E) test for the technician's maintenance form submission.

### **Section 5: Epics & Stories**

#### **Epic 1: Foundation & Core Data Management**
**Goal:** Establish the project's technical foundation, set up the core database with a robust migration strategy, and build the basic functionality to manage vehicle, technician, and parts data.

*   **Story 1.1: Project Scaffolding & Monorepo Setup**
*   **Story 1.2: Configure Database ORM and Migrations**
*   **Story 1.3: Backend Server & Database Connection**
*   **Story 1.4: Core Database Schema & Seed Data**
*   **Story 1.5: Frontend Application Setup**

#### **Epic 2: Automated Task Generation & Assignment Logic**
**Goal:** Implement the robust, automated logic that creates monthly maintenance tasks and intelligently assigns them to technicians.

*   **Story 2.1: Create Maintenance Tasks Table and Generation Service**
*   **Story 2.2: Implement Smart Task Assignment Logic**
*   **Story 2.3: Create API Endpoint for Task Generation**

#### **Epic 3: Technician Workflow & Maintenance Execution**
**Goal:** Build the complete, reliable, and user-friendly end-to-end workflow for the technician.

*   **Story 3.0: Implement Asynchronous Photo Upload Service**
*   **Story 3.1: Technician Task List View**
*   **Story 3.2: Maintenance Task Detail & Update Form**
*   **Story 3.3: Implement Task Completion API**

#### **Epic 4: Management Dashboard & Reporting**
**Goal:** Deliver an interactive and insightful real-time dashboard for management.

*   **Story 4.1: Create Dashboard Data API Endpoint**
*   **Story 4.2: Build Dashboard UI - Metrics & Workload**
*   **Story 4.3: Build Dashboard UI - Completed Tasks Gallery**

