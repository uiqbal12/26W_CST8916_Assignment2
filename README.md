# CST8916 – Remote Data and Real-time Applications

## Assignment 2: Real-time Stream Analytics Pipeline

| | |
|---|---|
| **Semester** | Winter 2026 |
| **Release Date** | March 16, 2026 (Week 10) |
| **Due Date** | March 30, 2026 at 11:59 PM |
| **Weight** | 10% of final grade |
| **Submission** | Brightspace |

---

## 1. Overview

In the Week 10 lab, you built a clickstream pipeline: a demo store sends click events through Azure Event Hubs, and a dashboard displays them. But the dashboard simply buffers raw events in memory — it cannot answer questions like *"which device type generates the most traffic?"*

In this assignment, you will extend that pipeline by adding **Azure Stream Analytics** to process the event stream, and **display the analytics results on the dashboard**.

There are two gaps you need to solve:

**Gap 1 — The data is too thin.** The current event payload has no `deviceType`, `browser`, or `os` fields. A query like *"count events by device type"* is impossible. You need to enrich the pipeline so richer data arrives in Event Hubs.

**Gap 2 — There is no analytics layer.** Nothing between Event Hubs and the dashboard aggregates or analyzes the stream. You need to add Stream Analytics and find a way to get its output to the dashboard.

---

## 2. Requirements

### 2.1 Part 1: Enrich the Event Payload

Enrich the pipeline so that every event arriving in Event Hubs includes **at least** these additional fields:

| Field | Type | Example Value |
|-------|------|---------------|
| `deviceType` | string | `"desktop"`, `"mobile"`, `"tablet"` |
| `browser` | string | `"Chrome"`, `"Firefox"`, `"Safari"` |
| `os` | string | `"Windows"`, `"macOS"`, `"Linux"`, `"Android"`, `"iOS"` |

You decide where and how to capture these fields.

---

### 2.2 Part 2: Stream Analytics Query + Dashboard Integration

The marketing team has asked for two insights from the clickstream data:

1. **"Which device types are most active?"** — They want a continuous breakdown of traffic by device type so they can prioritize mobile vs. desktop campaigns.
2. **"Are there traffic spikes?"** — They want to detect bursts of activity in the event stream so they can correlate them with promotions or incidents.

Your job:

1. **Create an Azure Stream Analytics job** that reads from your Event Hubs instance.
2. **Write the SAQL queries** that answer both business questions. You choose the windowing strategy, the aggregation logic, and the output columns. All queries must use `TIMESTAMP BY`.
3. **Display the results on your dashboard.** Update `dashboard.html` to show both insights — device type breakdown and spike detection — updated as new windows complete.

How you structure the queries, which window types you use, and how you connect Stream Analytics output to the dashboard are all your design decisions.

Your solution must be **deployed to Azure App Service** — not running locally. The store, dashboard, and Stream Analytics pipeline must all work together in the cloud.

---

### 2.3 Part 3: Documentation

Update your `README.md` to document your solution. It should include:

- **Architecture diagram** showing how data flows from the store to the dashboard through Stream Analytics
- **Design decisions** — why you chose your approach for enriching events and connecting Stream Analytics output to the dashboard
- **Setup instructions** — how to run your solution (environment variables, Azure resources needed, etc.)

---

### 2.4 Part 4: Video Demo

| Requirement | Details |
|-------------|---------|
| **Length** | Maximum 5 minutes |
| **Audio** | Not required |
| **Upload** | YouTube (unlisted) |

Your video must show:

| Step | What to demonstrate |
|------|---------------------|
| 1 | Show the app running on Azure App Service (your Azure URL) and click around the store to generate events |
| 2 | Show enriched events in Event Hubs (portal → Process data → Explore) — verify `deviceType`, `browser`, `os` are present |
| 3 | Show the Stream Analytics query and test it |
| 4 | Show the dashboard displaying live analytics results from Stream Analytics |

---

## 3. Submission Instructions

1. Fork the Week 10 lab repository (if you haven't already)
2. Commit your code changes and push to GitHub
3. Upload your video to YouTube (unlisted)

Submit your **GitHub Repository URL** on Brightspace.

- Repository must be **private**
- Add `ramymohamed10` as a collaborator
- Include the YouTube video link in your `README.md`

> **Warning:** Submissions without collaborator access at the time of marking will not be accepted.

> **Important:** Delete all Azure resources after recording your video to avoid charges.

---

## 4. Marking Rubric

| Part | Component | Weight |
|------|-----------|:------:|
| 1 | Event Payload Enrichment (`deviceType`, `browser`, `os` present in Event Hubs) | 15% |
| 2 | Stream Analytics Queries + Dashboard Integration (both business questions answered, results display on dashboard) | 35% |
| 3 | Documentation (architecture diagram, design decisions, setup instructions) | 15% |
| 4 | Video Demo (end-to-end pipeline working) | 35% |
| | **Total** | **100%** |

---

## 5. Academic Integrity

This assignment **permits** and **encourages** the use of generative AI tools as per the course outline.

**If you use AI assistance, you must:**

1. Disclose its use in a comment at the top of your code
2. Understand and be able to explain all code you submit
3. Ensure the code works correctly — AI-generated code with bugs will lose marks

---

## Questions?

Email: mohamer@algonquincollege.com
