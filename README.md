# 🏫 DSATM Complaint Box

A browser-based, anonymous campus complaint management system built for **Dayananda Sagar Academy of Technology and Management (DSATM), Bengaluru** — developed as part of a codeathon submission under VTU.

> **No installation. No login required for students. Just open the file.**

---

## 🚀 Live Demo

Open `dsatm_complaint_box.html` directly in any browser — no server, no setup.  
Or deploy it to any static host (GitHub Pages, Netlify) and share the link.

---

## 📋 Problem Statement

> *Build a system to register and track campus complaints.*

**Requirements covered:**
- ✅ Submit complaints
- ✅ Categorize issues
- ✅ Track status
- ✅ Generate reports
- ✅ *(Bonus)* Priority-based issue handling

---

## ✨ Features

### 👤 Student Side
| Feature | Description |
|---|---|
| **Anonymous submission** | Name is never shown publicly or to admin. Only a private phone/email is stored for recovery purposes — never displayed. |
| **Complaint ID + 4-digit PIN** | Each submission gets a unique `CMP-XXXX` ID and a self-chosen PIN. Save these to track your complaint later. |
| **Forgot ID / PIN recovery** | Enter your registered phone or email on the login screen to retrieve your Complaint ID and PIN. *(Simulated in demo — a real deployment would use Twilio/SendGrid.)* |
| **Track a complaint** | Enter Complaint ID + PIN to see current status, priority, admin remarks, and the full timeline. |
| **My complaints** | Browser-session shortcut — saves your complaints locally so you don't have to re-enter ID + PIN every time. |
| **Browse all complaints** | Read-only public feed — shows all complaints with identity hidden. Sortable by priority, newest, or oldest. Helps you check if your issue is already reported. |
| **Analytics tab** | View complaint counts by category and status — available to students too. |
| **File attachments** | Attach photos or documents as evidence when submitting. |

### 🔐 Admin Side
| Feature | Description |
|---|---|
| **Separate admin login** | Username + password login (`admin` / `admin123` for demo). Role-gated — students cannot access this panel. |
| **Identity never exposed** | Even in the admin dashboard, submitter name/email/phone is never displayed. Admin only sees the complaint, not who filed it. |
| **Dashboard with live stats** | Cards showing Total, Pending, In Progress, Resolved, and Overdue counts — auto-refreshes on every action. |
| **Priority management** | Admin can override priority (High / Medium / Low). Auto-priority is set at submission based on category + occurrence count. |
| **Status management** | Update status to Pending, In Progress, or Resolved per complaint. |
| **SLA escalation** | Each priority level has an SLA deadline (High: 3 days, Medium: 5 days, Low: 7 days). Overdue complaints are flagged automatically in red. |
| **Admin remarks / comments** | Admin can post internal remarks on any complaint, visible to the student when they track it. |
| **Complaint timeline** | Every status change, merge, and remark is logged with a timestamp. |
| **Duplicate detection & merging** | Complaints from the same category + location are flagged as potential duplicates. Admin can merge them — occurrence count combines, and students tracking merged IDs still see their status. |
| **Filters & search** | Filter by category, status, priority, overdue flag, or free-text search across the complaint table. |
| **Reports tab** | Charts and tables: complaints by category, by status, by priority, most frequent issues, average resolution time. |
| **CSV export** | Download the full complaint dataset as a `.csv` file for external analysis or records. |

---

## 🗂️ Project Structure

```
dsatm_complaint_box.html    ← Entire app in one self-contained file
README.md
```

Everything — HTML, CSS, JavaScript, Chart.js (via CDN), and sample data — is bundled in a single file. No build step, no dependencies to install.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Structure | HTML5 |
| Styling | CSS3 (custom properties, responsive grid) |
| Logic | Vanilla JavaScript (ES6+) |
| Charts | [Chart.js 4.4](https://www.chartjs.org/) via CDN |
| Storage | In-browser session memory (resets on page reload) |
| Deployment | Any static host — no backend required |

---

## 🔑 Demo Credentials

| Role | Credential |
|---|---|
| **Student** | No login needed — click *Continue to student portal* |
| **Admin** | Username: `admin` / Password: `admin123` |
| **Sample complaint** | ID: `CMP-1001` / PIN: `1111` |

Pre-loaded sample complaints (CMP-1001 through CMP-1004) are included so the dashboard and reports tabs are populated on first open.

---

## ⚙️ How to Run

**Option 1 — Local (simplest):**
```bash
# Just open the file in your browser
open dsatm_complaint_box.html        # macOS
start dsatm_complaint_box.html       # Windows
xdg-open dsatm_complaint_box.html   # Linux
```

**Option 2 — GitHub Pages:**
1. Push this repo to GitHub.
2. Go to **Settings → Pages → Deploy from branch (main / root)**.
3. GitHub will give you a public URL like `https://yourusername.github.io/dsatm-complaint-box/dsatm_complaint_box.html`.

**Option 3 — Netlify (one-click):**
1. Drag the folder into [netlify.com/drop](https://app.netlify.com/drop).
2. Done — live link generated instantly.

---

## ⚠️ Known Limitations (Demo vs Production)

| What | Demo behaviour | Production would need |
|---|---|---|
| Data persistence | Resets on every page reload (in-memory only) | Backend database (e.g. PostgreSQL, Firebase) |
| ID/PIN recovery | PIN is shown on-screen | Real email/SMS API (Twilio, SendGrid) |
| Admin credentials | Hardcoded in JS | Secure server-side auth with hashed passwords |
| File attachments | Stored as base64 in memory | Cloud file storage (S3, Firebase Storage) |
| Multi-user sync | Changes visible only in current tab | WebSockets or polling against a live backend |

This is intentional for a single-file hackathon demo. A production deployment would replace the in-memory store with a real backend while keeping the same frontend.

---

## 🧠 Design Highlights (What Makes This Different)

- **True anonymity by design** — student contact info is stored only for recovery, never rendered in any view including admin. This isn't just a UI hide; the `renderTable()` and admin detail functions never read or display `contactPhone` or `contactEmail`.
- **Auto-priority engine** — priority is calculated at submission from category + how many complaints already exist for that same category + location, so it reflects real-world severity rather than student self-reporting.
- **Duplicate merging** — rather than showing 10 identical complaints, admin can merge them into one record with a combined occurrence count. Students tracking merged IDs still see their own status.
- **SLA deadline tracking** — every complaint gets a resolution deadline. Overdue ones surface automatically at the top of the dashboard with hours-overdue displayed.
- **Full audit timeline** — every action (submission, status change, merge, remark) is logged to a per-complaint timeline so there's a clear accountability trail.



