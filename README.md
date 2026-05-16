# agriconnect-dashboard-design

# AgriConnect Dashboard – Technical Design & Architecture Specification

This repository contains the conceptual system architecture, data models, component hierarchy, and simulation logic workflows for the **AgriConnect High-Concurrency Supply Chain Dashboard**. 

Per the specification guidelines, this is a code-free design and architectural blueprint documentation.

---

## 1. Project Structure & Next.js 15 UI Architecture

The frontend layout uses the **Next.js 15 App Router** convention. The interface splits complex state operations away from UI layout blocks, nesting them into specialized, reusable components.

### Directory Structure & Hierarchy
* **`app/farmer/dashboard/page.tsx`** — Core layout entry point. Instantiates local layout parameters and hooks.
  * **`DashboardHeader`** — Global statistics layer, tracking real-time queue density.
  * **`BoardContainer`** — A two-column flex container orchestrating the data pipelines.
    * **`PendingColumn`** — Reads systemic state and dynamically maps out filtered operational items.
      * **`RequestCard`** — Includes the actionable client trigger interface.
    * **`AcceptedColumn`** — Reads systemic state and dynamically maps resolved elements.
      * **`RequestCard`** — Displays a read-only processed badge.

### Visual Layout Blueprint (ASCII Wireframe)
```text
+-----------------------------------------------------------------------------------+
|                                AGRI-CONNECT DASHBOARD                             |
+---------------------------------------------------+-------------------------------+
| PENDING REQUESTS                                  | ACCEPTED REQUESTS             |
+---------------------------------------------------+-------------------------------+
| [ Card #001 ]                                     | [ Card #003 ]                 |
| Farmer: Juan Dela Cruz                            | Farmer: Maria Santos          |
| Produce: Rice Premium (50 bags)                   | Produce: White Corn (20 bags) |
| Time: 16:00:12                                    | Time: 15:30:45                |
| Action: [ ACCEPT REQUEST ]                        | Status: [ ✓ ACCEPTED ]        |
|                                                   |                               |
| [ Card #002 ]                                     |                               |
| Farmer: Antonio Reyes                             |                               |
| Produce: Tomatoes (10 crates)                     |                               |
| Time: 16:02:40                                    |                               |
| Action: [ ACCEPT REQUEST ]                        |                               |
+---------------------------------------------------+-------------------------------+
| (Background Timer Thread: Appending incoming simulated data blocks here...)      |
+-----------------------------------------------------------------------------------+
