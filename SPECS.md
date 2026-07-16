# AgentHub Admin Panel Specification

## 1) Product Description

AgentHub is a SaaS platform where companies rent pre-configured AI agents and assign skills to perform business tasks. This prototype is an internal admin panel used by AgentHub operations staff to monitor revenue, manage users and agents, review contracts, inspect system errors, and perform basic administrative actions in a consistent interface.

## 2) Tech Stack and Constraints

1. The interface must be built with semantic HTML and Tailwind CSS loaded via CDN in the HTML document.
2. All interactivity must be implemented with vanilla JavaScript only.
3. No frameworks or libraries are allowed for UI/state management (no React, Vue, Angular, jQuery, Alpine, etc.).
4. No backend or API calls are required; all displayed data is hardcoded in JavaScript/HTML.
5. No external CSS file and no inline style attributes are allowed; styling is done with Tailwind utility classes only.
6. The solution can be implemented as one single-page prototype (`index.html`) with section switching behavior handled in JavaScript.

## 3) Global Layout and Navigation

1. The app shell includes a persistent left sidebar (`nav`) and a right content area (`main`) with a top bar (`header`).
2. Sidebar contains six navigation items: Dashboard, User Management, Agent Management, Skills, Agent Contracts, Error Log.
3. Clicking a nav item shows its corresponding section and hides others without full page reload.
4. The current section must be visually highlighted with a distinct active state.
5. The top bar includes the page title for the active section and a dark/light mode toggle.
6. Layout must remain usable on desktop and tablet widths; sidebar remains visible and content area scrolls independently.

## 4) Section Specifications

### 4.1 Dashboard

1. Render four metric cards in a responsive grid (2 columns on medium+, 1 column on small):
   - Total Revenue (This Month)
   - Discount/Coupon Losses
   - Active Agents
   - Failing Agents
2. Each card includes an icon area, metric label, hardcoded value, and a color accent that differs by metric type.
3. Metric cards use rounded corners, subtle shadow, and border contrast in both light and dark modes.
4. Below cards, render a full-width weekly activity chart placeholder panel with dashed border and centered label text.
5. Placeholder includes a short note indicating it is a mock chart area for later integration.

### 4.2 User Management

1. Display a table with at least 5 hardcoded rows and columns: Name, Email, Plan, Status, Actions.
2. Status is shown as a colored badge (for example: Active, Trial, Suspended).
3. Each row has an actions button (`⋮`) that opens a dropdown menu with at least: View detail, Delete.
4. Only one dropdown can be open at a time; opening another closes the previous one.
5. View detail opens a modal overlay containing full user record fields (name, email, company, plan, status, joined date, notes).
6. Modal closes by explicit close button and by clicking outside the modal card on the backdrop.

### 4.3 Agent Management

1. Render at least 4 agent records in stacked cards/list rows showing: Agent name, Owner, Status badge, Actions.
2. Status supports Active, Inactive, and Failing visual variants.
3. Each record includes a collapsed skills panel hidden by default.
4. Clicking an expand/collapse control reveals or hides the skill list with a visible height/opacity transition.
5. Each record has a `⋮` dropdown menu with options: Configure, Delete.
6. Configure opens a modal showing the agent system prompt in an editable `textarea` and includes a close control.

### 4.4 Skills

1. Display a short explanatory block describing that a skill is an attachable capability that extends what an agent can do.
2. Render at least 4 skill items, each with: Skill name, short description, enabled-agent count.
3. Each skill row/card includes a `⋮` dropdown with: View detail, Delete.
4. View detail opens a modal with extended skill information (use cases, dependencies, risk level, example output).
5. Enabled-agent count is displayed as a numeric pill/badge for quick scanning.

### 4.5 Agent Contracts

1. Display a table with at least 4 contract rows and columns: Client, Agent, Contracted Skills, Start Date, End Date, Amount Paid, Actions.
2. Contracted Skills column shows compact comma-separated skill names and truncates gracefully on narrower widths.
3. Each row has a `⋮` dropdown with at least View detail.
4. View detail opens a modal with full contract breakdown including itemized skill pricing and total.
5. Modal includes contract metadata (contract ID, billing cycle, status, renewal setting).

### 4.6 Error Log

1. Display at least 6 hardcoded error rows with columns: Timestamp, Agent, Error Type, Description, Actions.
2. Error Type appears as color-coded severity/type badge (for example: Critical, Warning, Timeout, Validation).
3. Each row has a `⋮` dropdown with actions: View detail, Mark as resolved.
4. View detail opens a modal with full stack/error trace and contextual metadata.
5. Mark as resolved can visually annotate the row (for example, badge or muted state) within the static prototype behavior.

## 5) Reusable Component Inventory

1. Persistent sidebar navigation with active item state.
2. Top bar with section title and dark/light mode toggle.
3. Metric card component (icon, label, value, accent color).
4. Table container with sticky-like header styling and row hover treatment.
5. Status badge component (plan/status/severity variants).
6. Actions dropdown component (`⋮` trigger + floating menu).
7. Modal overlay component (backdrop, panel, header, content, close button).
8. Collapsible skill list component with smooth transition.
9. Chart placeholder panel component.

## 6) Data Consistency Rules

1. Agent names are reused consistently across Agent Management, Agent Contracts, and Error Log.
2. Skills referenced in contracts exist in the Skills section catalog.
3. Owner/client names are coherent between related records.
4. Amount totals in contract detail modal equal the sum of itemized skill prices.

## 7) Interaction Rules

1. Dark mode toggle adds/removes `dark` class at document root and updates all section styles via Tailwind `dark:` utilities.
2. Chosen color mode is persisted in `localStorage` and restored on load.
3. Section navigation updates visible section and active nav styling.
4. Dropdown menus open on click, close on outside click, and close when an option is selected.
5. Modal opens from View detail/Configure actions and closes on close button and backdrop click.
6. Collapsible agent skills start collapsed and toggle open/closed with smooth transition classes.

## 8) Accessibility and Semantics

1. Use semantic tags: `header`, `nav`, `main`, `section`, `table`, `thead`, `tbody`, `button`, `dialog`-like modal structure.
2. Interactive controls are keyboard focusable and use descriptive labels/`aria-*` attributes where relevant.
3. Color is not the only status cue; badges include text labels.
4. Modal focus behavior should remain usable (close button visible and reachable).

## 9) Acceptance Criteria

1. A `SPECS.md` file exists at repository root and is committed before any HTML prototype file is committed.
2. The prototype includes six sections accessible from the persistent sidebar.
3. Dashboard shows four metric cards (icon + label + hardcoded value) and a full-width chart placeholder.
4. User Management table includes at least 5 users with actions dropdown per row.
5. User detail modal opens from View detail and closes via close button and backdrop click.
6. Agent Management includes at least 4 agents, each with collapsed skill list by default.
7. Agent skill list toggles open/closed with a visible transition.
8. Agent Configure action opens a modal with editable system prompt textarea.
9. Skills section includes explanation text and at least 4 skills with enabled-agent counts.
10. Agent Contracts table includes at least 4 contracts and detail modal with itemized skill pricing.
11. Error Log includes at least 6 entries with color-coded error badges.
12. Error Log entries support View detail modal and Mark as resolved action.
13. All `⋮` dropdowns close when clicking outside the menu area.
14. At least four different sections implement functional View detail/Configure modals.
15. Global dark/light toggle updates full UI theme using Tailwind `dark:` classes.
16. Theme preference persists while navigating between sections and after reload.
17. Prototype uses Tailwind CDN and vanilla JS only; no framework and no backend integration.
18. HTML structure uses semantic tags and is usable on desktop and tablet viewports.
