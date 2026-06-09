# 📋 Leave Tracker Application

A **Salesforce Lightning Web Component (LWC)** application for managing employee leave requests. This app allows employees to submit leave requests and enables managers to review, approve, or reject them — all within the Salesforce platform.

---

## ✨ Features

- **Submit Leave Requests** — Employees can create new leave requests with date range, reason, and auto-assigned user.
- **View My Leaves** — Employees can view all their submitted leave requests with real-time status tracking.
- **Manager Approval Workflow** — Managers can view leave requests from their direct reports and approve/reject them with comments.
- **Inline Editing** — Edit pending leave requests directly from the data table.
- **Date Validation** — Built-in validation ensures:
  - "From Date" is not in the past.
  - "From Date" is not after "To Date".
- **Color-Coded Status** — Approved requests are highlighted in green, rejected in yellow, and pending in default.
- **Auto-Refresh** — Data tables refresh automatically after any create/update operation.
- **Toast Notifications** — Success and error messages displayed via Lightning toast events.

---

## 🏗️ Project Structure

```
Leave Tracker Application/
└── main/
    └── default/
        ├── aura/                        # Aura component config
        ├── classes/
        │   ├── LeaveRequstController.cls         # Apex controller for fetching leave data
        │   └── LeaveRequestSampleData.cls        # Utility class to generate sample data
        ├── lwc/
        │   ├── leaveTracker/            # Parent container component with tab navigation
        │   ├── myLeaves/                # Employee-facing component to view/create leaves
        │   └── leaveRequests/           # Manager-facing component to review/approve leaves
        └── objects/
            └── LeaveRequest__c/         # Custom object definition
                └── fields/
                    ├── From_Date__c     # Leave start date
                    ├── To_Date__c       # Leave end date
                    ├── Reason__c        # Reason for leave
                    ├── Status__c        # Pending / Approved / Rejected
                    ├── Manager_Comment__c  # Manager's feedback
                    └── User__c          # Lookup to the requesting user
```

---

## 🧩 Components

### `leaveTracker` (Parent)
- Acts as the main container with a **tabbed layout** (`lightning-tabset`).
- Contains two tabs: **My Leaves** and **Leave Requests**.
- Handles cross-component communication to refresh the manager's grid when an employee submits a new request.

### `myLeaves` (Employee View)
- Displays the logged-in user's leave requests in a **lightning-datatable**.
- Provides a **"+" button** to create a new leave request via a modal popup.
- Allows editing of **pending** leave requests (approved/rejected requests are locked).
- Validates dates before submission and auto-sets status to "Pending".

### `leaveRequests` (Manager View)
- Displays leave requests from the manager's **direct reports**.
- Managers can click **Edit** to open a modal and update the **Status** and **Manager Comment** fields.
- Editing is disabled for already processed (approved/rejected) requests.

---

## ⚙️ Custom Object: `LeaveRequest__c`

| Field                 | API Name              | Type          | Description                          |
|-----------------------|-----------------------|---------------|--------------------------------------|
| Request Id            | `Name`                | Auto Number   | Unique identifier for each request   |
| User                  | `User__c`             | Lookup (User) | The employee who submitted the leave |
| From Date             | `From_Date__c`        | Date          | Start date of the leave              |
| To Date               | `To_Date__c`          | Date          | End date of the leave                |
| Reason                | `Reason__c`           | Text Area     | Reason for the leave request         |
| Status                | `Status__c`           | Picklist      | Pending / Approved / Rejected        |
| Manager Comment       | `Manager_Comment__c`  | Text Area     | Feedback from the manager            |

---

## 🚀 Deployment

### Prerequisites
- Salesforce CLI (`sf` or `sfdx`) installed
- A Salesforce org (Developer Edition, Sandbox, or Scratch Org)
- Authenticated with your org via CLI

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/Rathi376/Leave-Tracker-App.git
   cd Leave-Tracker-App
   ```

2. **Authorize your Salesforce org**
   ```bash
   sf org login web --alias myorg
   ```

3. **Deploy the metadata to your org**
   ```bash
   sf project deploy start --source-dir "Leave Tracker Application" --target-org myorg
   ```

4. **Generate sample data** (optional)
   Open the Developer Console or execute the following in Anonymous Apex:
   ```apex
   LeaveRequestSampleData.createData();
   ```

5. **Add the component to a Lightning page**
   - Go to **Setup → Lightning App Builder**.
   - Create or edit a Lightning Record/App/Home Page.
   - Drag the `leaveTracker` component onto the page.
   - Save and activate the page.

---

## 🛠️ Tech Stack

| Technology             | Purpose                                    |
|------------------------|--------------------------------------------|
| **Lightning Web Components (LWC)** | Front-end UI framework          |
| **Apex**               | Server-side controller logic               |
| **SOQL**               | Querying Salesforce data                   |
| **SLDS**               | Salesforce Lightning Design System for UI  |
| **Custom Objects**     | Data model for leave requests              |

---

## 📝 License

This project is open source and available for personal and educational use.

---

## 👤 Author

**Keshav Rathi** — [@Rathi376](https://github.com/Rathi376)
