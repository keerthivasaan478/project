

## **Automated Fleet Maintenance Management System UI/UX Specification**

### **1. Introduction**

This document defines the user experience goals, information architecture, user flows, and visual design specifications for the Fleet Maintenance System. It is the single source of truth for the application's look, feel, and user interaction, ensuring a cohesive and user-centered experience for both Managers and Technicians.


### **2. Overall UX Goals & Principles**

*   **Target User Personas:**
    *   **Manager:** Desk-based, data-driven, needs high-level overviews and the ability to quickly identify problems. Values efficiency and clarity.
    *   **Technician:** Mobile-first user (tablet/phone), works in potentially noisy/messy environments with intermittent connectivity. Values simplicity, speed, and reliability.
*   **Usability Goals:**
    *   **Efficiency:** Core tasks (completing a form, checking overdue status) must be achievable in the fewest possible steps.
    *   **Clarity:** The state of the system should always be obvious. No ambiguity about what is overdue, assigned, or completed.
    *   **Reliability:** The technician's form *must* work every time, even with weak Wi-Fi. Data loss is not an option.
*   **Design Principles:**
    1.  **Function Over Form:** This is a utility application. Clarity, speed, and usability are prioritized over aesthetic flourishes.
    2.  **Progressive Disclosure:** Show only what's necessary. Reveal complexity (like the full details of a completed task) only when the user asks for it.
    3.  **Provide Clear Feedback:** Every action (button click, form submission) must result in immediate and clear visual feedback.

### **3. Information Architecture (Sitemap)**

```mermaid
graph TD
    A[Login Page] -->|Manager| B[Dashboard]
    A -->|Technician| C[My Tasks List]

    B --> D{Task Detail Modal}
    C --> E[Maintenance Task Form]

    subgraph Manager Flow
        B
        D
    end

    subgraph Technician Flow
        C
        E
    end```

### **4. User Flows**

#### **Flow 1: Manager - Daily Check-in**

*   **User Goal:** To get a 5-minute overview of the fleet's maintenance status.
*   **Flow:**
    1.  Manager logs in.
    2.  Redirected to **Dashboard**.
    3.  Scans "Overdue Tasks" metric.
    4.  If overdue tasks > 0, clicks the metric to see the list of overdue vehicles.
    5.  Scans "Technician Workload" to check for imbalances.
    6.  Scans "Recently Completed Tasks" gallery for a quick quality check.
    7.  Clicks on a photo to open the **Task Detail Modal** for more info.

#### **Flow 2: Technician - Complete a Maintenance Task**

*   **User Goal:** To accurately and efficiently document a completed maintenance job.
*   **Flow:**
    1.  Technician logs in on a tablet.
    2.  Redirected to **My Tasks List**.
    3.  Searches for the vehicle ID (e.g., "TRK-001").
    4.  Taps the task to navigate to the **Maintenance Task Form**.
    5.  Takes "Before" photo with the tablet camera, which uploads in the background.
    6.  Performs maintenance.
    7.  Updates form: Selects "Parts Used," enters quantities.
    8.  Takes "After" photo, which uploads in the background.
    9.  Types name and checks the signature box.
    10. Taps "Complete Task."
    11. Sees a "Success!" message and is redirected back to the **My Tasks List**, where the completed task is now gone.

### **5. Wireframes & Layouts**

#### **Login Page**
*   **Layout:** Centered card on a simple background.
*   **Elements:** Logo, Email field, Password field, "Login" button.

#### **Dashboard (Manager)**
*   **Layout:** Three-column responsive grid on desktop, single-column stack on mobile.
*   **Column 1 (Key Metrics):** Large, bold numbers for "Overdue Tasks" and "Completed This Week."
*   **Column 2 (Technician Workload):** A simple list of technician names with a progress-bar-style visualization of their active tasks (e.g., 2/3).
*   **Column 3 (Filters):** Dropdown for "Location Base."
*   **Full Width (Bottom):** A grid-based gallery for "Recently Completed Tasks," showing a "Before" image, Vehicle ID, and Technician Name.

#### **My Tasks List (Technician)**
*   **Layout:** A simple, full-width list that is easy to tap on a tablet.
*   **Elements:**
    *   Sticky header with a "Search by Vehicle ID..." input field.
    *   Each list item is a "card" with large, readable text showing Vehicle ID, Type, Location, and a prominent Due Date. Overdue tasks are highlighted with a red border.

#### **Maintenance Task Form (Technician)**
*   **Layout:** A clean, single-column form.
*   **Elements (in order):**
    1.  Read-only Task Details (Vehicle ID, etc.).
    2.  Large "Upload Before Photo" button. Shows a thumbnail when complete.
    3.  Multi-select dropdown for "Parts Used."
    4.  Dynamic list of selected parts with quantity inputs.
    5.  Large "Upload After Photo" button. Shows a thumbnail when complete.
    6.  Signature section with a text input for name and a checkbox.
    7.  A large, primary "Complete Task" button. A secondary "Save as Draft" button is also present.

### **6. Branding & Style Guide**

*   **Visual Identity:** Utilitarian, clean, and professional. Inspired by logistics and industrial software.
*   **Color Palette:**
    *   **Primary:** A strong, dependable Blue (`#00529B`).
    *   **Accent:** A clear, actionable Green (`#28A745`) for success states and buttons.
    *   **Error/Alert:** A vibrant Red (`#DC3545`) for overdue tasks and errors.
    *   **Neutral:** A range of Grays (`#F8F9FA` for backgrounds, `#6C757D` for secondary text, `#212529` for primary text).
*   **Typography:**
    *   **Font:** Inter (a highly readable, modern sans-serif).
    *   **Scale:** Clear hierarchy. Large font sizes for metrics and headers, clean readable body text for forms.
*   **Iconography:**
    *   **Library:** Lucide Icons (lucide.dev). Clean, simple, and comprehensive.
*   **Spacing & Layout:**
    *   **Grid:** Based on a 4px grid system. Spacing should be consistent (e.g., 16px padding in cards, 24px gaps between sections).

### **7. Accessibility Requirements**

*   **Compliance Target:** WCAG 2.1 AA.
*   **Key Requirements:**
    *   **Visual:** All text must have a contrast ratio of at least 4.5:1. All interactive elements must have clear focus indicators.
    *   **Interaction:** The entire application must be navigable and operable using only a keyboard. All form fields must have proper labels.
    *   **Content:** All icons that convey meaning must have appropriate alt text or ARIA labels.

### **8. Responsiveness Strategy**

*   **Breakpoints:**
    *   **Mobile:** < 768px
    *   **Tablet:** 768px - 1024px
    *   **Desktop:** > 1024px
*   **Adaptation Patterns:**
    *   **Dashboard:** The multi-column layout on desktop will stack into a single, scrollable column on mobile.
    *   **Forms:** Form fields will be full-width on mobile to maximize tap targets.
    *   **Navigation:** A full navigation bar on desktop will collapse into a standard "hamburger" menu on mobile.
