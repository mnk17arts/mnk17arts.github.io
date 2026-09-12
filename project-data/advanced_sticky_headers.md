### Project Description

> `Advanced Sticky List View Headers` is an Odoo 17 frontend enhancement module built to make large and wide datasets easier to navigate.
>
> It adds configurable **sticky headers** and **frozen columns** to supported Odoo list views, with particular attention to **nested One2many and Many2many lists inside form views**.
>
> The module is designed for situations where users need to scroll both vertically and horizontally through large ERP tables without losing track of the column headers or important identifying fields.

---

### Why I Built It

> While working with large Odoo datasets, I repeatedly encountered a simple usability problem: a list with many rows and columns often requires both vertical and horizontal scrolling.
>
> When scrolling vertically, the table headers can disappear.
>
> When scrolling horizontally, important identifying columns can disappear from view.
>
> The problem becomes especially noticeable when the table is embedded inside a form view, such as a Sales Order with a large Order Lines section.
>
> I built this module to keep the important table context visible while navigating large datasets and to make these everyday ERP workflows less frustrating.

---

### Tech Stack & Architecture

- **Platform:** Odoo 17
- **Frontend Framework:** OWL
- **Language:** JavaScript
- **Styling:** CSS
- **Odoo Integration:** `ListRenderer` patching
- **Browser APIs:** `ResizeObserver`, `localStorage`, DOM APIs
- **Rendering:** Dynamic DOM inspection, runtime style calculation, and sticky positioning
- **Lifecycle:** OWL `useEffect` and `onPatched`
- **Performance:** `requestAnimationFrame`, passive scroll handling, dynamic recalculation

---

### Application Walkthrough

#### 1. The Nested List View Problem

A common Odoo workflow is working with a large relational list embedded inside a form view.

A Sales Order is a good example: its Order Lines section can contain many records and enough columns to require both vertical and horizontal scrolling.

As the user moves through the dataset, important context can disappear:

- Column headers can disappear during vertical scrolling.
- Important identifying columns can disappear during horizontal scrolling.
- Nested list views introduce additional layout and scroll-container complexity.

This module was built specifically to improve that navigation experience.

![Nested List View Inside an Odoo Form](/project-assets/odoo-sticky/nested-list-view.png)

---

#### 2. Real-World Example: Sales Order Lines

The module was tested against large Sales Order datasets where the Order Lines section contains many rows and columns.

This provides a practical example of the problem the module is intended to solve: users can continue reviewing a large dataset while keeping the information needed to understand the visible records in context.

---

#### 3. Interactive Sticky Controls

The newer implementation can inject a compact control panel directly above a supported list view.

Users can:

- Enable or disable sticky headers
- Choose the number of data columns to freeze

The configuration is maintained per Odoo model using browser `localStorage`.

![Sticky List Controls](/project-assets/odoo-sticky/sticky-controls.png)

---

#### 4. Vertical Sticky Headers

When a list contains many records, the table header can move out of view as the user scrolls down.

The module tracks the relationship between the list, its header, and the surrounding Odoo interface, then dynamically adjusts the header position while scrolling.

This keeps the table context visible without requiring the user to repeatedly scroll back to the top.

![Vertical Sticky Headers](/project-assets/odoo-sticky/vertical-sticky-header.png)

---

#### 5. Horizontal Column Freezing

Wide datasets can require significant horizontal scrolling.

The module allows selected columns to remain fixed on the left side of the table while the remaining columns continue to scroll horizontally.

Frozen-column positions are calculated from the actual rendered column widths rather than relying on hardcoded offsets.

![Horizontal Column Freezing](/project-assets/odoo-sticky/horizontal-column-freeze.png)

---

#### 6. Combined Vertical and Horizontal Navigation

The most useful scenario is when a user needs to scroll in both directions at the same time.

The module coordinates sticky headers with frozen columns and manages their stacking order so the frozen header/column intersection remains visible while the rest of the table continues to move.

![Combined Sticky Headers and Columns](/project-assets/odoo-sticky/combined-sticky-navigation.png)

---

### Nested Odoo List Views

A major focus of the module is handling list views embedded inside other Odoo views.

The implementation supports scenarios involving:

- `One2many` lists
- `Many2many` lists
- Form views containing relational lists
- Standalone list views
- Nested Odoo containers and wrappers

The frontend logic identifies the appropriate rendered table and applies the sticky behavior to its headers and cells rather than modifying the underlying business data model.

---

### Smart Column Handling

The horizontal freezing logic adapts to the actual rendered table structure.

It:

- Detects visible columns
- Ignores columns hidden by Odoo
- Detects utility columns such as record selectors and row handles
- Calculates cumulative left offsets from rendered widths
- Applies sticky positioning to the required header and body cells

Utility columns are treated separately from user-selected data columns so core Odoo list interactions remain accessible.

---

### Dynamic Layout & Resizing

Odoo tables can change after the initial render because of column resizing, visibility changes, and frontend rerendering.

The module uses:

- `ResizeObserver`
- `requestAnimationFrame`
- OWL lifecycle hooks

to recalculate sticky-column positions when table dimensions change.

This keeps the frozen columns aligned with the actual rendered table instead of relying on static measurements.


---

### Navigation Safeguards

The module limits the number of data columns that can be frozen.

At least one real data column remains horizontally scrollable, preventing a configuration that locks the entire dataset.

Utility columns such as selectors and row handles are accounted for separately when calculating the freeze limit.

---

### Preference Persistence

Interactive sticky preferences are stored in the browser using `localStorage`.

The preferences include:

- Sticky header state
- Number of frozen data columns

The storage key is based on the Odoo resource model, allowing different models to maintain independent configurations.

---

### Key Capabilities

The current implementation provides:

- **Nested List Support** — improves supported One2many and Many2many list views inside form views
- **Standalone List Support** — supports configured standalone Odoo list views
- **Sticky Headers** — keeps headers visible during vertical navigation
- **Frozen Columns** — keeps selected columns visible during horizontal navigation
- **Combined Scrolling** — coordinates vertical headers and horizontal frozen columns
- **Utility Column Detection** — handles record selectors and row handles separately
- **Dynamic Offset Calculation** — derives sticky positions from actual rendered widths
- **Resize Observation** — recalculates layout after dimension changes
- **Preference Persistence** — stores interactive settings per Odoo model
- **Dynamic UI Injection** — injects the sticky controls into supported list views

---

### Engineering Highlights

- **Odoo Renderer Integration:** Extended the Odoo frontend by patching `ListRenderer` and integrating the behavior with the OWL lifecycle.

- **Nested View Handling:** Added logic for list tables rendered inside form views, including relational list scenarios such as One2many and Many2many fields.

- **Runtime DOM Analysis:** Inspects the rendered table structure instead of assuming fixed column positions or widths.

- **Dynamic Column Mathematics:** Calculates cumulative pixel offsets from the actual rendered column dimensions to position frozen columns correctly.

- **Utility Column Awareness:** Detects Odoo selector and row-handle columns so they remain correctly positioned.

- **Layer Management:** Uses controlled stacking levels so sticky headers, frozen columns, and their intersections remain visually consistent during scrolling.

- **Responsive Recalculation:** Uses `ResizeObserver` and `requestAnimationFrame` to respond to table and column dimension changes.

- **Frontend Preference Storage:** Persists sticky settings using model-specific `localStorage` keys.

- **Scroll Handling:** Uses passive scroll listeners and coordinated lifecycle cleanup to reduce unnecessary listener duplication.

---

### The Problem This Module Solves

> Large ERP tables become difficult to navigate when the information needed to understand a record disappears during scrolling.
>
> **Vertical scrolling can hide the headers.**
>
> **Horizontal scrolling can hide important identifying columns.**
>
> **Nested list views inside form pages can make both problems more noticeable.**
>
> This module was built to keep that context visible and make large Odoo datasets easier to work with.

---

### Project Links

- **Source Code:** [GitHub Repository](https://github.com/mnk17arts/odoo-advanced-sticky-list-headers)
- **Project Demo:** [Demo Video](/project-assets/odoo-sticky/odoo-sticky-headers.mp4)

---

### Project Status

> Developed for **Odoo 17** with a focus on improving navigation and usability across supported standalone and nested list-view scenarios.