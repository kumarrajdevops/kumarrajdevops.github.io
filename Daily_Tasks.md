---
layout: page
title: Daily_Tasks
permalink: /Daily_Tasks/
---

<section class="tasks-page-head">
  <div>
    <p class="tasks-kicker">Daily Audit Report</p>
    <h2 class="tasks-title">Daily Tasks</h2>
    <p class="tasks-subtitle">This page is generated from <code>daily_tasks_log.md</code>.</p>
  </div>
  <button type="button" class="tasks-print-btn" onclick="window.print()">
    Print Report
  </button>
</section>

<style>
  .tasks-page-head {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    gap: 1rem;
    margin-bottom: 0.9rem;
  }
  .tasks-kicker {
    margin: 0 0 0.25rem;
    color: #93c5fd;
    font-size: 0.8rem;
    text-transform: uppercase;
    letter-spacing: 0.06em;
  }
  .tasks-title {
    margin: 0;
    font-size: 1.2rem;
    font-weight: 650;
  }
  .tasks-subtitle {
    margin: 0.3rem 0 0;
    color: #94a3b8;
    font-size: 0.9rem;
  }
  .tasks-print-btn {
    border: 1px solid #334155;
    background: linear-gradient(135deg, #1d4ed8, #7c3aed);
    color: #fff;
    border-radius: 10px;
    padding: 0.5rem 0.8rem;
    cursor: pointer;
    font-size: 0.86rem;
    font-weight: 600;
    white-space: nowrap;
  }
  .tasks-summary {
    display: grid;
    grid-template-columns: repeat(3, minmax(120px, 1fr));
    gap: 0.7rem;
    margin: 0.3rem 0 1rem;
  }
  .tasks-summary-item {
    background: linear-gradient(180deg, #111827, #0f172a);
    border: 1px solid #263244;
    border-radius: 12px;
    padding: 0.8rem 0.85rem;
    text-align: center;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.04);
  }
  .tasks-summary-item strong {
    display: block;
    font-size: 1.25rem;
    line-height: 1.2;
    color: #f8fafc;
  }
  .tasks-summary-item span {
    color: #94a3b8;
    font-size: 0.8rem;
  }
  .tasks-day-summary .tasks-summary-item {
    background: linear-gradient(180deg, #14213a, #0f172a);
    border-color: #294164;
  }
  .daily-tasks-wrap {
    background: #0b1220;
    border: 1px solid #1f2937;
    border-radius: 14px;
    padding: 1rem;
    color: #e2e8f0;
    overflow-x: hidden;
  }
  .daily-tasks-wrap h1,
  .daily-tasks-wrap h2,
  .daily-tasks-wrap h3 {
    color: #f8fafc;
    margin-top: 1rem;
    margin-bottom: 0.55rem;
    border-bottom: 1px solid #1f2937;
    padding-bottom: 0.3rem;
    font-weight: 600;
  }
  .daily-tasks-wrap h1 { font-size: 1.2rem; }
  .daily-tasks-wrap h2 { font-size: 1.1rem; }
  .daily-tasks-wrap h3 { font-size: 1rem; }
  .daily-tasks-wrap table {
    width: 100%;
    max-width: 100%;
    table-layout: fixed;
    border-collapse: collapse;
    margin: 0.75rem 0 1.1rem;
    background: #0f172a;
    border: 1px solid #1f2937;
    border-radius: 10px;
    overflow: hidden;
  }
  .daily-tasks-wrap th:nth-child(1),
  .daily-tasks-wrap td:nth-child(1) {
    width: 8%;
    text-align: center;
  }
  .daily-tasks-wrap th:nth-child(2),
  .daily-tasks-wrap td:nth-child(2) {
    width: 38%;
  }
  .daily-tasks-wrap th:nth-child(3),
  .daily-tasks-wrap td:nth-child(3) {
    width: 14%;
  }
  .daily-tasks-wrap th:nth-child(4),
  .daily-tasks-wrap td:nth-child(4) {
    width: 40%;
  }
  .daily-tasks-wrap th,
  .daily-tasks-wrap td {
    border-bottom: 1px solid #1f2937;
    padding: 0.65rem 0.7rem;
    text-align: left;
    vertical-align: top;
    font-size: 0.92rem;
    line-height: 1.45;
    white-space: normal;
    word-break: normal;
    overflow-wrap: break-word;
    hyphens: auto;
  }
  .daily-tasks-wrap th:nth-child(3),
  .daily-tasks-wrap td:nth-child(3) { white-space: nowrap; }
  .daily-tasks-wrap th:nth-child(2),
  .daily-tasks-wrap td:nth-child(2),
  .daily-tasks-wrap th:nth-child(4),
  .daily-tasks-wrap td:nth-child(4) {
    white-space: normal;
    overflow-wrap: anywhere;
    word-break: break-word;
  }
  .daily-tasks-wrap td *,
  .daily-tasks-wrap th * {
    white-space: normal;
    word-break: normal;
    overflow-wrap: break-word;
  }
  .daily-tasks-wrap th {
    background: #172036;
    color: #dbe5f4;
    text-transform: uppercase;
    font-size: 0.68rem;
    letter-spacing: 0.04em;
    font-weight: 600;
  }
  .daily-tasks-wrap td {
    background: #0f172a;
  }
  .daily-tasks-wrap td code {
    background: transparent;
    color: inherit;
  }
  .daily-tasks-wrap input[type="checkbox"] {
    transform: scale(1.05);
    margin-right: 0.4rem;
  }
  @media (max-width: 900px) {
    .tasks-page-head {
      flex-direction: column;
      align-items: stretch;
    }
    .tasks-print-btn {
      width: 100%;
    }
  }
  @media print {
    .tasks-print-btn {
      display: none;
    }
    .tasks-page-head {
      margin-bottom: 0.4rem;
    }
    .tasks-kicker,
    .tasks-subtitle {
      color: #111827;
    }
    .tasks-summary-item {
      color: #111827;
      border-color: #d1d5db;
      background: #fff;
      box-shadow: none;
    }
    .tasks-summary-item strong,
    .tasks-summary-item span {
      color: #111827;
    }
    .daily-tasks-wrap {
      color: #111827;
      border-color: #d1d5db;
      background: #fff;
    }
    .daily-tasks-wrap h1,
    .daily-tasks-wrap h2,
    .daily-tasks-wrap h3 {
      color: #111827;
      border-bottom-color: #d1d5db;
    }
    .daily-tasks-wrap table {
      border-color: #d1d5db;
      background: #fff;
    }
    .daily-tasks-wrap th,
    .daily-tasks-wrap td {
      border-bottom-color: #e5e7eb;
      color: #111827;
    }
    .daily-tasks-wrap th {
      background: #f9fafb;
      color: #111827;
      font-size: 0.68rem;
      font-weight: 600;
    }
    .daily-tasks-wrap td {
      background: #fff;
    }
  }
</style>

{% capture tasks_markdown %}
{% include_relative daily_tasks_log.md %}
{% endcapture %}
{% assign parts = tasks_markdown | split: '# TODO' %}
{% capture reordered_tasks_markdown %}
{% for part in parts reversed %}
{% assign trimmed = part | strip %}
{% if trimmed != '' %}
# TODO {{ trimmed }}

{% endif %}
{% endfor %}
{% endcapture %}
{% assign rendered_tasks_markdown = reordered_tasks_markdown
  | replace: '| [x] |', '| ✅ |'
  | replace: '| [X] |', '| ✅ |'
  | replace: '| [ ] |', '| ⬜ |'
%}

{% assign total_tasks = 0 %}
{% assign done_tasks = 0 %}
{% assign lines = tasks_markdown | split: '
' %}
{% for line in lines %}
  {% if line contains '[ ]' or line contains '[x]' or line contains '[X]' %}
    {% assign total_tasks = total_tasks | plus: 1 %}
  {% endif %}
  {% if line contains '[x]' or line contains '[X]' %}
    {% assign done_tasks = done_tasks | plus: 1 %}
  {% endif %}
{% endfor %}
{% assign inprogress_tasks = total_tasks | minus: done_tasks %}

{% assign total_days = 0 %}
{% assign leave_days = 0 %}
{% assign weekoff_days = 0 %}
{% assign working_days = 0 %}
{% assign day_open = false %}
{% assign day_has_leave = false %}
{% assign day_has_weekoff = false %}

{% for line in lines %}
  {% if line contains '# TODO' %}
    {% if day_open %}
      {% if day_has_leave %}
        {% assign leave_days = leave_days | plus: 1 %}
      {% elsif day_has_weekoff %}
        {% assign weekoff_days = weekoff_days | plus: 1 %}
      {% else %}
        {% assign working_days = working_days | plus: 1 %}
      {% endif %}
    {% endif %}
    {% assign total_days = total_days | plus: 1 %}
    {% assign day_open = true %}
    {% assign day_has_leave = false %}
    {% assign day_has_weekoff = false %}
  {% endif %}

  {% if day_open and line contains '| leave |' %}
    {% assign day_has_leave = true %}
  {% endif %}
  {% if day_open and line contains '| weekoff |' %}
    {% assign day_has_weekoff = true %}
  {% endif %}
{% endfor %}

{% if day_open %}
  {% if day_has_leave %}
    {% assign leave_days = leave_days | plus: 1 %}
  {% elsif day_has_weekoff %}
    {% assign weekoff_days = weekoff_days | plus: 1 %}
  {% else %}
    {% assign working_days = working_days | plus: 1 %}
  {% endif %}
{% endif %}

<section class="tasks-summary">
  <div class="tasks-summary-item">
    <strong>{{ total_tasks }}</strong>
    <span>Total</span>
  </div>
  <div class="tasks-summary-item">
    <strong>{{ done_tasks }}</strong>
    <span>Done</span>
  </div>
  <div class="tasks-summary-item">
    <strong>{{ inprogress_tasks }}</strong>
    <span>In-Progress</span>
  </div>
</section>

<section class="tasks-summary tasks-day-summary">
  <div class="tasks-summary-item">
    <strong>{{ leave_days }}</strong>
    <span>Leave Days</span>
  </div>
  <div class="tasks-summary-item">
    <strong>{{ weekoff_days }}</strong>
    <span>Weekoff Days</span>
  </div>
  <div class="tasks-summary-item">
    <strong>{{ working_days }}</strong>
    <span>Working Days</span>
  </div>
</section>

<section class="daily-tasks-wrap">
{{ rendered_tasks_markdown | markdownify }}
</section>
