### **Jira and Its Importance in Software Teams**

#### **Why Teams Use Jira**

- **Jira** is widely used by software teams, including **testing** and **development**, to keep projects organized and manageable.
- Teams rely on **Application Lifecycle Management (ALM)** tools like Jira to manage software projects effectively. Jira is one of the most popular tools for this purpose.

---

### **What is Jira?**

- **Jira** is an **issue-tracking tool** used to manage **features**, **bugs**, and project tasks.
- Initially, teams used tools like **Bugzilla**, before Jira was introduced in **2002** by Atlassian.
- Jira is **written in Java** and offers robust functionalities for project management and tracking.

---

### **How to Access Jira**

- Jira can be accessed through the **Atlassian website**.
- A **free trial** is available for users to explore the tool.

---

### **Jira Components in a Scrum Project**

In Scrum, Jira organizes tasks into various components. Assume a **Scrum project** setup.

#### **1. Backlog:**

- The **backlog** contains a list of project requirements, including user stories and tasks.
- In Jira, an **issue** represents an item that needs to be addressed.

#### **2. Components:**

- **Components** in Jira are used to categorize work. For example:
  - **Front-end**, **back-end**, or **payment dashboard** can be separate components.
- Components are divided into **epics**, which represent large bodies of work.
- Each **epic** consists of **user stories** and **tasks**.
  - **User stories** can further be divided into **sub-tasks**.

#### **3. Epic:**

- An **Epic** is a large requirement or feature that can be broken down into smaller user stories or tasks.

---

### **Component Creation Process:**

1. **Create a component** in Jira.
2. Provide details such as:
   - **Name**
   - **Description**
   - **Lead** (the person responsible)
   - **Assignee**

---

### **Epic Creation Process:**

1. **Create an issue** in Jira.
2. Select **issue type** as **Epic**.
3. Fill in the following fields:
   - **Epic name**
   - **Summary** (usually a high-level description of the epic)
   - **Component** (choose the relevant component for the epic)
   - **Priority** (set the urgency level)
   - **Label** (add tags for easier grouping)
   - **Linked issues** (to connect related issues)
   - **Assignee** (the person responsible for this epic)
4. Ensure **no epic link** is set since this is the epic itself.
5. Use the **watch** feature to track changes to the epic.

---

### **Who Creates Epics and User Stories?**

- The **Product Owner** typically creates **epics** and **user stories**.

---

### **Writing a User Story:**

1. **Create an issue** in Jira.
2. Select **issue type** as **User Story**.
   - A **user story** is a brief, informal description of a software feature from the perspective of the end user or customer.
3. Provide the following details:
   - **Description**: Include **acceptance criteria** for the tester.
   - **Summary**: Provide a short title for the user story.

- Once created, **user stories** will be added to the **backlog**.

---

### **Creating a Sprint:**

After user stories are in the backlog, a **sprint** can be created to organize and track the work.

#### **Steps to Create a Sprint:**

1. **Add Backlog Items to the Sprint**:
   - Select user stories or tasks from the backlog and add them to the sprint.
2. **Story Points Estimate**:
   - Assign **story points** to each item based on the complexity and effort required (e.g., 1 to 20 points).
   - Story points measure **complexity**, **effort**, and **uncertainty** rather than time.
3. **Start Sprint**:
   - Once ready, click **Start Sprint** to begin tracking the progress.
4. **Complete Sprint**:
   - At the end of the sprint, review the progress and click **Complete Sprint**. Any unfinished tasks can be moved to the next sprint or the backlog.

---

### **Sprint Tracking Charts:**

1. **Velocity Chart**:
   - Shows how many **story points** were completed in each sprint, helping to gauge the team's capacity and plan future sprints.
2. **Burndown Chart**:
   - Tracks the remaining work during a sprint, showing the team's progress toward completing the sprint goals.
3. **Burnup Chart**:
   - Displays both completed work and total work, allowing you to track progress toward the overall project completion.

---

### **Releases in Jira:**

- A **release** is a collection of features, bug fixes, or enhancements delivered to the customer.
- **Each epic** is assigned a **release version**, which helps track which features are included in a specific release.

#### **Key Points About Releases:**

- Releases help teams plan and track software deliveries.
- **Release notes** can summarize completed features, fixes, and tasks.

#### **Steps to Create a Release:**

1. Navigate to the **Releases** section.
2. Click on **Create Release**.
3. Assign a **version** to each epic, representing the release it will be part of.

---

### **Kanban Project in Jira:**

In a **Kanban project**, the workflow is continuous, and tasks move from one stage to another without defined sprints.

#### **Key Features of Kanban:**

1. **No Sprints**:
   - Tasks flow continuously from **To Do** to **Done** without sprint cycles.
2. **Work-in-Progress (WIP) Limits**:
   - Limit the number of items in each stage of the workflow to manage workload and avoid bottlenecks.
3. **Board Settings**:
   - Customize the Kanban board by setting WIP limits, adjusting stages, and setting permissions.

#### **Scrum and Kanban Together**:
- Projects can contain both **Scrum** and **Kanban** boards, allowing flexibility for different teams within the same project.

---

### **Pages in Jira (e.g., for Meetings or Conferences):**

- Jira can integrate with **Confluence** to create **pages** for documentation, meeting notes, or conferences. These pages can store important project-related information.

