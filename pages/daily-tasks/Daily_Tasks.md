---
layout: page
title: Daily_Tasks
permalink: /Daily_Tasks/
---

<div id="tasks-auth-overlay" class="tasks-auth-overlay" hidden>
  <div class="tasks-auth-card">
    <h3>Protected Page</h3>
    <p>Enter password to open Daily Tasks.</p>
    <input id="tasks-auth-input" type="password" placeholder="Password" />
    <div class="tasks-auth-actions">
      <button type="button" id="tasks-auth-submit" class="tasks-print-btn">Unlock</button>
    </div>
    <p id="tasks-auth-error" class="tasks-auth-error"></p>
  </div>
</div>

<div id="tasks-protected-content">
<section class="tasks-page-head">
  <div>
    <p class="tasks-kicker">Daily Audit Report</p>
    <h2 class="tasks-title">Daily Tasks</h2>
    <p class="tasks-subtitle">This page is generated from <code>daily_tasks_log.md</code>.</p>
  </div>
  <div class="tasks-print-actions">
    <button type="button" class="tasks-print-btn" id="tasks-print-current">
      Print Current View
    </button>
    <button type="button" class="tasks-print-btn" id="tasks-print-full">
      Print Full Report
    </button>
  </div>
</section>

<style>
  .tasks-page-head {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    gap: 1rem;
    margin-bottom: 0.9rem;
  }
  .tasks-auth-overlay {
    position: fixed;
    inset: 0;
    z-index: 9999;
    display: flex;
    align-items: center;
    justify-content: center;
    background: rgba(15, 23, 42, 0.82);
    padding: 1rem;
  }
  .tasks-auth-card {
    width: min(360px, 92vw);
    background: #0f172a;
    border: 1px solid rgba(148, 163, 184, 0.3);
    border-radius: 12px;
    padding: 1rem;
    color: #e2e8f0;
  }
  .tasks-auth-card h3 {
    margin: 0 0 0.4rem;
    font-size: 1rem;
  }
  .tasks-auth-card p {
    margin: 0 0 0.65rem;
    color: #94a3b8;
    font-size: 0.85rem;
  }
  .tasks-auth-card input {
    width: 100%;
    border: 1px solid rgba(148, 163, 184, 0.35);
    background: #111827;
    color: #f8fafc;
    border-radius: 8px;
    padding: 0.45rem 0.55rem;
    margin-bottom: 0.65rem;
  }
  .tasks-auth-actions {
    display: flex;
    justify-content: flex-end;
  }
  .tasks-auth-error {
    min-height: 1.1em;
    margin-top: 0.5rem;
    color: #fda4af !important;
    font-size: 0.8rem;
  }
  .tasks-kicker {
    margin: 0 0 0.25rem;
    color: #cbd5e1;
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
  .tasks-print-actions {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    flex-wrap: wrap;
  }
  .tasks-summary {
    display: grid;
    grid-template-columns: repeat(3, minmax(120px, 1fr));
    gap: 0.7rem;
    margin: 0.2rem 0 0.8rem;
  }
  .tasks-summary-item {
    background: #1e293b;
    border: 1px solid rgba(229, 229, 229, 0.2);
    border-radius: 12px;
    padding: 0.65rem 0.7rem;
    text-align: center;
    box-shadow: none;
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
    background: #1e293b;
    border-color: rgba(229, 229, 229, 0.2);
  }
  .daily-tasks-wrap {
    background: #0f172a;
    border: 1px solid rgba(229, 229, 229, 0.16);
    border-radius: 14px;
    padding: 0.8rem;
    color: #e2e8f0;
    overflow-x: hidden;
  }
  .daily-tasks-wrap h1,
  .daily-tasks-wrap h2,
  .daily-tasks-wrap h3 {
    color: #f8fafc;
    margin-top: 0.4rem;
    margin-bottom: 0.35rem;
    border-bottom: 1px solid rgba(252, 163, 17, 0.35);
    padding-bottom: 0.2rem;
    font-weight: 600;
  }
  .daily-tasks-wrap h1 { font-size: 1rem; }
  .daily-tasks-wrap h2 { font-size: 0.98rem; }
  .daily-tasks-wrap h3 { font-size: 0.95rem; }
  .tasks-global-columns {
    display: grid;
    grid-template-columns: 8% 38% 14% 40%;
    gap: 0;
    margin: 0 0 0.45rem;
    border: 1px solid rgba(229, 229, 229, 0.2);
    border-radius: 8px;
    overflow: hidden;
    background: #1e293b;
  }
  .tasks-global-columns span {
    padding: 0.42rem 0.5rem;
    color: #cbd5e1;
    font-size: 0.68rem;
    font-weight: 600;
    letter-spacing: 0.04em;
    text-transform: uppercase;
    border-right: 1px solid rgba(229, 229, 229, 0.2);
  }
  .tasks-global-columns span:last-child {
    border-right: 0;
  }
  .tasks-day-date {
    display: inline-flex;
    align-items: center;
    gap: 0.35rem;
    background: rgba(252, 163, 17, 0.12);
    border: 1px solid rgba(252, 163, 17, 0.35);
    color: #f8fafc;
    border-radius: 999px;
    padding: 0.15rem 0.5rem;
    font-size: 0.78rem;
    font-weight: 600;
    letter-spacing: 0.01em;
  }
  .daily-tasks-wrap table {
    width: 100%;
    max-width: 100%;
    table-layout: fixed;
    border-collapse: collapse;
    margin: 0.25rem 0 0.4rem;
    background: #1e293b;
    border: 1px solid rgba(229, 229, 229, 0.18);
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
    border-bottom: 1px solid rgba(229, 229, 229, 0.25);
    padding: 0.5rem 0.55rem;
    text-align: left;
    vertical-align: top;
    font-size: 0.92rem;
    line-height: 1.45;
    white-space: normal;
    word-break: normal;
    overflow-wrap: break-word;
    hyphens: auto;
  }
  .daily-tasks-wrap th + th,
  .daily-tasks-wrap td + td {
    border-left: 1px solid rgba(229, 229, 229, 0.18);
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
    background: #1e293b;
    color: #cbd5e1;
    text-transform: uppercase;
    font-size: 0.68rem;
    letter-spacing: 0.04em;
    font-weight: 600;
  }
  .daily-tasks-wrap thead {
    display: none;
  }
  .daily-tasks-wrap td {
    background: #1e293b;
  }
  .tasks-pagination {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    gap: 0.75rem;
    margin: 0.6rem 0 1rem;
    flex-wrap: wrap;
  }
  .tasks-pagination-left,
  .tasks-pagination-right {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
  }
  .tasks-page-btn {
    border: 1px solid rgba(229, 229, 229, 0.25);
    background: #1e293b;
    color: #f8fafc;
    border-radius: 8px;
    padding: 0.35rem 0.65rem;
    font-size: 0.83rem;
    cursor: pointer;
  }
  .tasks-page-btn:disabled {
    opacity: 0.45;
    cursor: not-allowed;
  }
  .tasks-page-info {
    font-size: 0.82rem;
    color: #94a3b8;
  }
  .tasks-page-size {
    border: 1px solid rgba(229, 229, 229, 0.25);
    background: #1e293b;
    color: #f8fafc;
    border-radius: 8px;
    padding: 0.32rem 0.5rem;
    font-size: 0.83rem;
  }
  .tasks-date-filter {
    border: 1px solid rgba(229, 229, 229, 0.25);
    background: #1e293b;
    color: #f8fafc;
    border-radius: 8px;
    padding: 0.32rem 0.5rem;
    font-size: 0.83rem;
  }
  .tasks-date-filter::-webkit-calendar-picker-indicator {
    cursor: pointer;
    opacity: 0.9;
    filter: invert(82%) sepia(20%) saturate(350%) hue-rotate(180deg) brightness(103%) contrast(95%);
  }
  .tasks-day-section {
    margin-bottom: 0.06rem;
    border: 0;
    border-radius: 0;
    padding: 0;
    background: transparent;
  }
  .tasks-day-section.day-leave {
    background: transparent;
  }
  .tasks-day-section.day-weekoff {
    background: transparent;
  }
  .daily-tasks-wrap tr.status-leave td {
    background: #1e293b;
  }
  .daily-tasks-wrap tr.status-weekoff td {
    background: #1e293b;
  }
  .daily-tasks-wrap tr.status-holiday td {
    background: #1e293b;
  }
  .daily-tasks-wrap tr.status-leave td:nth-child(3),
  .daily-tasks-wrap tr.status-weekoff td:nth-child(3),
  .daily-tasks-wrap tr.status-holiday td:nth-child(3) {
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.02em;
  }
  .daily-tasks-wrap tr.status-leave td {
    color: #fda4af;
  }
  .daily-tasks-wrap tr.status-weekoff td {
    color: #93c5fd;
  }
  .daily-tasks-wrap tr.status-holiday td {
    color: #fcd34d;
  }
  .tasks-pagination-bottom {
    justify-content: space-between;
    margin: 1rem 0 0;
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
    .tasks-day-section {
      break-inside: avoid;
      page-break-inside: avoid;
    }
    .tasks-pagination,
    .tasks-pagination-bottom {
      display: none !important;
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
{% assign inprogress_tasks = 0 %}
{% assign blocked_tasks = 0 %}
{% assign unique_tasks = 0 %}
{% assign task_status_map = '|' %}
{% assign lines = tasks_markdown | split: '
' %}
{% for line in lines %}
  {% if line contains '[ ]' or line contains '[x]' or line contains '[X]' %}
    {% assign total_tasks = total_tasks | plus: 1 %}
  {% endif %}
  {% if line contains '| completed |' %}
    {% assign done_tasks = done_tasks | plus: 1 %}
  {% endif %}
  {% if line contains '| in-progress |' %}
    {% assign inprogress_tasks = inprogress_tasks | plus: 1 %}
  {% endif %}
  {% if line contains '| blocked |' %}
    {% assign blocked_tasks = blocked_tasks | plus: 1 %}
  {% endif %}

  {% if line contains '|' %}
    {% if line contains '[ ]' or line contains '[x]' or line contains '[X]' %}
      {% assign cols = line | split: '|' %}
      {% if cols.size >= 5 %}
        {% assign task_value = cols[2] | strip | downcase %}
        {% assign status_value = cols[3] | strip | downcase %}
        {% if task_value != '' and task_value != 'task' and status_value != '---' %}
          {% unless status_value == 'leave' or status_value == 'weekoff' %}
            {% assign task_prefix = '|' | append: task_value | append: '::' %}
            {% assign existed_before = false %}
            {% if task_status_map contains task_prefix %}
              {% assign existed_before = true %}
            {% endif %}

            {% assign token_completed = '|' | append: task_value | append: '::completed|' %}
            {% assign token_inprogress = '|' | append: task_value | append: '::in-progress|' %}
            {% assign token_blocked = '|' | append: task_value | append: '::blocked|' %}
            {% assign token_postponed = '|' | append: task_value | append: '::postponed|' %}
            {% assign token_other = '|' | append: task_value | append: '::other|' %}

            {% assign task_status_map = task_status_map | replace: token_completed, '|' %}
            {% assign task_status_map = task_status_map | replace: token_inprogress, '|' %}
            {% assign task_status_map = task_status_map | replace: token_blocked, '|' %}
            {% assign task_status_map = task_status_map | replace: token_postponed, '|' %}
            {% assign task_status_map = task_status_map | replace: token_other, '|' %}

            {% if status_value == 'completed' %}
              {% assign task_status_map = task_status_map | append: task_value | append: '::completed|' %}
            {% elsif status_value == 'in-progress' %}
              {% assign task_status_map = task_status_map | append: task_value | append: '::in-progress|' %}
            {% elsif status_value == 'blocked' %}
              {% assign task_status_map = task_status_map | append: task_value | append: '::blocked|' %}
            {% elsif status_value == 'postponed' %}
              {% assign task_status_map = task_status_map | append: task_value | append: '::postponed|' %}
            {% else %}
              {% assign task_status_map = task_status_map | append: task_value | append: '::other|' %}
            {% endif %}

            {% unless existed_before %}
              {% assign unique_tasks = unique_tasks | plus: 1 %}
            {% endunless %}
          {% endunless %}
        {% endif %}
      {% endif %}
    {% endif %}
  {% endif %}
{% endfor %}

{% assign unique_done_tasks = 0 %}
{% assign unique_inprogress_tasks = 0 %}
{% assign unique_blocked_tasks = 0 %}
{% assign map_tokens = task_status_map | split: '|' %}
{% for token in map_tokens %}
  {% if token contains '::' %}
    {% assign parts = token | split: '::' %}
    {% assign latest_status = parts[1] | strip %}
    {% if latest_status == 'completed' %}
      {% assign unique_done_tasks = unique_done_tasks | plus: 1 %}
    {% elsif latest_status == 'in-progress' %}
      {% assign unique_inprogress_tasks = unique_inprogress_tasks | plus: 1 %}
    {% elsif latest_status == 'blocked' %}
      {% assign unique_blocked_tasks = unique_blocked_tasks | plus: 1 %}
    {% endif %}
  {% endif %}
{% endfor %}

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
    <strong>{{ unique_tasks }}</strong>
    <span>Total</span>
  </div>
  <div class="tasks-summary-item">
    <strong>{{ unique_done_tasks }}</strong>
    <span>Done</span>
  </div>
  <div class="tasks-summary-item">
    <strong>{{ unique_inprogress_tasks }}</strong>
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

<section class="tasks-pagination" id="tasks-pagination" hidden>
  <div class="tasks-pagination-right">
    <label class="tasks-page-info" for="tasks-date-filter-from">From</label>
    <input type="date" id="tasks-date-filter-from" class="tasks-date-filter" />
    <label class="tasks-page-info" for="tasks-date-filter-to">To</label>
    <input type="date" id="tasks-date-filter-to" class="tasks-date-filter" />
    <button type="button" class="tasks-page-btn" id="tasks-date-clear">Clear</button>
    <label class="tasks-page-info" for="tasks-page-size">Days/Page</label>
    <select id="tasks-page-size" class="tasks-page-size">
      <option value="5">5</option>
      <option value="7" selected>7</option>
      <option value="10">10</option>
      <option value="14">14</option>
    </select>
  </div>
</section>

<section class="daily-tasks-wrap">
  <div class="tasks-global-columns" aria-hidden="true">
    <span>Done</span>
    <span>Task</span>
    <span>Status</span>
    <span>Remark</span>
  </div>
{{ rendered_tasks_markdown | markdownify }}
</section>

<section class="tasks-pagination tasks-pagination-bottom" id="tasks-pagination-bottom" hidden>
  <div class="tasks-pagination-left">
    <button type="button" class="tasks-page-btn" id="tasks-page-prev">Prev</button>
    <button type="button" class="tasks-page-btn" id="tasks-page-next">Next</button>
    <span class="tasks-page-info" id="tasks-page-info"></span>
  </div>
</section>

<script>
  (function () {
    const wrap = document.querySelector('.daily-tasks-wrap');
    const pagerTop = document.getElementById('tasks-pagination');
    const pagerBottom = document.getElementById('tasks-pagination-bottom');
    const prevBtn = document.getElementById('tasks-page-prev');
    const nextBtn = document.getElementById('tasks-page-next');
    const info = document.getElementById('tasks-page-info');
    const pageSizeSelect = document.getElementById('tasks-page-size');
    const dateFilterFromInput = document.getElementById('tasks-date-filter-from');
    const dateFilterToInput = document.getElementById('tasks-date-filter-to');
    const dateFilterClearBtn = document.getElementById('tasks-date-clear');
    const printCurrentBtn = document.getElementById('tasks-print-current');
    const printFullBtn = document.getElementById('tasks-print-full');
    if (!wrap || !pagerTop || !pagerBottom || !prevBtn || !nextBtn || !info || !pageSizeSelect || !dateFilterFromInput || !dateFilterToInput || !dateFilterClearBtn || !printCurrentBtn || !printFullBtn) return;

    const nodes = Array.from(wrap.children);
    const daySections = [];
    let currentSection = null;

    const startsTodo = (el) => {
      const tag = (el.tagName || '').toUpperCase();
      return ['H1', 'H2', 'H3'].includes(tag) && (el.textContent || '').trim().toUpperCase().startsWith('TODO');
    };

    nodes.forEach((node) => {
      if (startsTodo(node)) {
        currentSection = document.createElement('div');
        currentSection.className = 'tasks-day-section';
        daySections.push(currentSection);
        wrap.appendChild(currentSection);
      }
      if (currentSection) {
        currentSection.appendChild(node);
      }
    });

    const parseHeaderDate = (section) => {
      const header = section.querySelector('h1, h2, h3');
      const text = (header?.textContent || '').trim();
      const match = text.match(/(\d{1,2})\/(\d{1,2})\/(\d{4})/);
      if (!match) return null;
      const day = Number(match[1]);
      const month = Number(match[2]);
      const year = Number(match[3]);
      const date = new Date(year, month - 1, day);
      return Number.isNaN(date.getTime()) ? null : date.getTime();
    };
    const parseHeaderDateKey = (section) => {
      const header = section.querySelector('h1, h2, h3');
      const text = (header?.textContent || '').trim();
      const match = text.match(/(\d{1,2})\/(\d{1,2})\/(\d{4})/);
      if (!match) return '';
      const day = `${Number(match[1])}`.padStart(2, '0');
      const month = `${Number(match[2])}`.padStart(2, '0');
      const year = `${Number(match[3])}`;
      return `${year}-${month}-${day}`;
    };

    daySections.sort((a, b) => {
      const aTime = parseHeaderDate(a);
      const bTime = parseHeaderDate(b);
      if (aTime === null && bTime === null) return 0;
      if (aTime === null) return 1;
      if (bTime === null) return -1;
      return bTime - aTime; // latest date first
    });
    daySections.forEach((section) => {
      section.dataset.dateKey = parseHeaderDateKey(section);
      const header = section.querySelector('h1, h2, h3');
      if (header) {
        const original = (header.textContent || '').trim();
        const dateMatch = original.match(/(\d{1,2}\/\d{1,2}\/\d{4})/);
        if (dateMatch) {
          header.textContent = dateMatch[1];
          header.classList.add('tasks-day-date');
        }
      }
      Array.from(section.querySelectorAll('p')).forEach((p) => {
        const text = (p.textContent || '').trim().toLowerCase();
        if (text.startsWith('day note:')) {
          p.remove();
        }
      });
      const bodyRows = Array.from(section.querySelectorAll('tbody tr'));
      const statusRows = bodyRows.map((row) => {
        const statusCell = row.querySelector('td:nth-child(3)');
        const status = (statusCell?.textContent || '').trim().toLowerCase();
        const remarkCell = row.querySelector('td:nth-child(4)');
        if (remarkCell && (remarkCell.textContent || '').trim() === '') {
          remarkCell.textContent = 'N/A';
        }
        if (status === 'leave') row.classList.add('status-leave');
        if (status === 'weekoff') row.classList.add('status-weekoff');
        if (status === 'holiday' || status === 'holidays') row.classList.add('status-holiday');
        return status;
      });
      const hasLeave = statusRows.includes('leave');
      const hasWeekoff = statusRows.includes('weekoff');
      const hasWork = statusRows.some((s) => s && s !== 'leave' && s !== 'weekoff');
      if (hasLeave && !hasWork) section.classList.add('day-leave');
      if (hasWeekoff && !hasWork) section.classList.add('day-weekoff');
    });
    daySections.forEach((section) => wrap.appendChild(section));

    pagerTop.hidden = false;
    pagerBottom.hidden = false;
    let page = 1;
    let pageSize = Number(pageSizeSelect.value) || 7;
    let filterFrom = '';
    let filterTo = '';
    let printFullReport = false;

    const renderPage = () => {
      const filteredSections = daySections.filter((section) => {
        const key = section.dataset.dateKey || '';
        if (!key) return !filterFrom && !filterTo;
        if (filterFrom && key < filterFrom) return false;
        if (filterTo && key > filterTo) return false;
        return true;
      });
      const totalPages = Math.max(1, Math.ceil(filteredSections.length / pageSize));
      if (page > totalPages) page = totalPages;
      if (page < 1) page = 1;
      const start = (page - 1) * pageSize;
      const end = start + pageSize;

      const visibleSet = new Set(filteredSections.slice(start, end));
      daySections.forEach((section) => {
        section.style.display = visibleSet.has(section) ? '' : 'none';
      });

      prevBtn.disabled = page <= 1;
      nextBtn.disabled = page >= totalPages;
      let suffix = '';
      if (filterFrom || filterTo) {
        const fromText = filterFrom || '...';
        const toText = filterTo || '...';
        suffix = ` | Range: ${fromText} -> ${toText}`;
      }
      info.textContent = `Page ${page} / ${totalPages} (${filteredSections.length} days)${suffix}`;
      pageSizeSelect.disabled = Boolean(filterFrom || filterTo);
    };

    const beforePrint = () => {
      if (printFullReport) {
        daySections.forEach((section) => {
          section.style.display = '';
        });
      }
    };
    const afterPrint = () => {
      printFullReport = false;
      renderPage();
    };
    window.addEventListener('beforeprint', beforePrint);
    window.addEventListener('afterprint', afterPrint);
    printCurrentBtn.addEventListener('click', () => {
      printFullReport = false;
      window.print();
    });
    printFullBtn.addEventListener('click', () => {
      printFullReport = true;
      window.print();
    });

    prevBtn.addEventListener('click', () => {
      page -= 1;
      renderPage();
      wrap.scrollIntoView({ behavior: 'smooth', block: 'start' });
    });
    nextBtn.addEventListener('click', () => {
      page += 1;
      renderPage();
      wrap.scrollIntoView({ behavior: 'smooth', block: 'start' });
    });
    pageSizeSelect.addEventListener('change', () => {
      pageSize = Number(pageSizeSelect.value) || 7;
      page = 1;
      renderPage();
    });
    const applyRangeFilter = () => {
      filterFrom = (dateFilterFromInput.value || '').trim();
      filterTo = (dateFilterToInput.value || '').trim();
      if (filterFrom && filterTo && filterFrom > filterTo) {
        const tmp = filterFrom;
        filterFrom = filterTo;
        filterTo = tmp;
        dateFilterFromInput.value = filterFrom;
        dateFilterToInput.value = filterTo;
      }
      page = 1;
      renderPage();
    };
    dateFilterFromInput.addEventListener('change', applyRangeFilter);
    dateFilterToInput.addEventListener('change', applyRangeFilter);
    dateFilterClearBtn.addEventListener('click', () => {
      dateFilterFromInput.value = '';
      dateFilterToInput.value = '';
      filterFrom = '';
      filterTo = '';
      page = 1;
      renderPage();
    });

    renderPage();
  })();
</script>

</div>

<script>
  (function () {
    const PASSWORD = '3232';
    const STORAGE_KEY = 'daily_tasks_unlocked';
    const overlay = document.getElementById('tasks-auth-overlay');
    const content = document.getElementById('tasks-protected-content');
    const input = document.getElementById('tasks-auth-input');
    const submit = document.getElementById('tasks-auth-submit');
    const error = document.getElementById('tasks-auth-error');
    if (!overlay || !content || !input || !submit || !error) return;

    const unlock = () => {
      overlay.hidden = true;
      content.style.display = '';
      sessionStorage.setItem(STORAGE_KEY, '1');
    };

    if (sessionStorage.getItem(STORAGE_KEY) === '1') {
      unlock();
      return;
    }

    content.style.display = 'none';
    overlay.hidden = false;
    input.focus();

    const verify = () => {
      if (input.value === PASSWORD) {
        error.textContent = '';
        unlock();
      } else {
        error.textContent = 'Invalid password.';
      }
    };

    submit.addEventListener('click', verify);
    input.addEventListener('keydown', (e) => {
      if (e.key === 'Enter') verify();
    });
  })();
</script>
