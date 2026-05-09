---
layout: page
title: Roster → Calendar
permalink: /roster-calendar/
---

<div class="rc-wrap">

<details class="rc-setup-guide">
  <summary>⚙️ Google Cloud Setup <span class="rc-setup-tag">(one-time)</span></summary>
  <ol>
    <li>Go to <strong>console.cloud.google.com</strong> → create a new project (or use an existing one)</li>
    <li>Navigate to <strong>APIs &amp; Services → Library</strong> → enable <strong>Google Calendar API</strong></li>
    <li>Go to <strong>APIs &amp; Services → Credentials</strong> → <strong>Create Credentials → OAuth 2.0 Client ID</strong></li>
    <li>Set application type to <strong>Web application</strong></li>
    <li>Under <strong>Authorized JavaScript origins</strong>, add:<br>
      <code>https://kumarrajdevops.github.io</code><br>
      <code>http://localhost:4000</code> (for local dev)
    </li>
    <li>Copy the <strong>Client ID</strong> and paste it in the config below, then click Save</li>
  </ol>
</details>

<section class="rc-section">
  <h3 class="rc-section-title">Configuration</h3>
  <div class="rc-config-grid">
    <div class="rc-field">
      <label for="rc-client-id">OAuth Client ID</label>
      <div class="rc-input-row">
        <input id="rc-client-id" type="text" placeholder="XXXXXXXXXX.apps.googleusercontent.com" autocomplete="off" />
        <button id="rc-save-cfg" class="rc-btn">Save</button>
      </div>
    </div>
    <div class="rc-field">
      <label for="rc-name">Your name(s) in roster <small>(comma-separated, case-insensitive)</small></label>
      <input id="rc-name" type="text" value="Kumar" placeholder="Kumar, Kumar Raj" />
    </div>
    <div class="rc-field">
      <label>Timezone</label>
      <span class="rc-muted">Asia/Kolkata (UTC+05:30)</span>
    </div>
  </div>
</section>

<section class="rc-section rc-auth-section">
  <button id="rc-signin" class="rc-btn rc-btn-google" disabled>
    <svg width="18" height="18" viewBox="0 0 48 48" aria-hidden="true"><path fill="#EA4335" d="M24 9.5c3.54 0 6.71 1.22 9.21 3.6l6.85-6.85C35.9 2.38 30.47 0 24 0 14.62 0 6.51 5.38 2.56 13.22l7.98 6.19C12.43 13.72 17.74 9.5 24 9.5z"/><path fill="#4285F4" d="M46.98 24.55c0-1.57-.15-3.09-.38-4.55H24v9.02h12.94c-.58 2.96-2.26 5.48-4.78 7.18l7.73 6c4.51-4.18 7.09-10.36 7.09-17.65z"/><path fill="#FBBC05" d="M10.53 28.59c-.48-1.45-.76-2.99-.76-4.59s.27-3.14.76-4.59l-7.98-6.19C.92 16.46 0 20.12 0 24c0 3.88.92 7.54 2.56 10.78l7.97-6.19z"/><path fill="#34A853" d="M24 48c6.48 0 11.93-2.13 15.89-5.81l-7.73-6c-2.15 1.45-4.92 2.3-8.16 2.3-6.26 0-11.57-4.22-13.47-9.91l-7.98 6.19C6.51 42.62 14.62 48 24 48z"/><path fill="none" d="M0 0h48v48H0z"/></svg>
    Sign in with Google
  </button>
  <span id="rc-auth-status" class="rc-auth-status"></span>
</section>

<section class="rc-section">
  <h3 class="rc-section-title">Paste Roster from Excel</h3>
  <p class="rc-hint">Select the roster table in Excel (including the header row) → Copy → click the area below → Paste (Ctrl+V / Cmd+V).</p>
  <textarea id="rc-paste-area" class="rc-paste-area" placeholder="Paste Excel roster here…" rows="6" spellcheck="false"></textarea>
  <div class="rc-options-row">
    <label class="rc-checkbox-label">
      <input type="checkbox" id="rc-include-off" />
      Also create all-day "Weekly Off" events for my days off
    </label>
  </div>
</section>

<div id="rc-preview-section" class="rc-section" hidden>
  <h3 class="rc-section-title">
    Preview
    <span id="rc-event-count" class="rc-badge">0</span>
    events detected
  </h3>
  <div class="rc-table-wrap">
    <table class="rc-table">
      <thead>
        <tr>
          <th><input type="checkbox" id="rc-select-all" checked title="Select / deselect all" /></th>
          <th>Date</th>
          <th>Day</th>
          <th>Shift</th>
          <th>Start</th>
          <th>End</th>
          <th>Result</th>
        </tr>
      </thead>
      <tbody id="rc-tbody"></tbody>
    </table>
  </div>
  <div class="rc-actions">
    <button id="rc-create-btn" class="rc-btn rc-btn-primary" disabled>
      Sync Events to Google Calendar
    </button>
  </div>
</div>

<div id="rc-log-section" class="rc-section" hidden>
  <h3 class="rc-section-title">Progress</h3>
  <div id="rc-log" class="rc-log"></div>
</div>

<!-- ── Manage Existing Events ─────────────────────────────────── -->
<div class="rc-section">
  <h3 class="rc-section-title">Manage Calendar Events</h3>
  <p class="rc-hint">Fetch your existing roster events, review them, and delete any you no longer need.</p>
  <div class="rc-manage-row">
    <div class="rc-field rc-field-inline">
      <label for="rc-from">From</label>
      <input type="date" id="rc-from" class="rc-date-input" />
    </div>
    <div class="rc-field rc-field-inline">
      <label for="rc-to">To</label>
      <input type="date" id="rc-to" class="rc-date-input" />
    </div>
    <button id="rc-fetch-btn" class="rc-btn" disabled>Fetch Events</button>
  </div>
  <div id="rc-fetched-wrap" hidden>
    <div class="rc-fetched-header">
      <span id="rc-fetched-count" class="rc-badge">0</span>&nbsp;events found
      <button id="rc-delete-sel-btn" class="rc-btn rc-btn-danger" style="margin-left:auto">Delete Selected</button>
    </div>
    <div class="rc-table-wrap">
      <table class="rc-table">
        <thead>
          <tr>
            <th><input type="checkbox" id="rc-fetch-sel-all" checked /></th>
            <th>Date</th>
            <th>Day</th>
            <th>Shift</th>
            <th>Time</th>
            <th>Result</th>
          </tr>
        </thead>
        <tbody id="rc-fetched-tbody"></tbody>
      </table>
    </div>
  </div>
</div>

<!-- ── Cleanup ────────────────────────────────────────────────── -->
<div class="rc-section rc-cleanup-section">
  <h3 class="rc-section-title">Cleanup Old Events</h3>
  <p class="rc-hint">Deletes all roster events (Shift 1, Shift 2, Weekly Off) older than 2 months from your Google Calendar.</p>
  <div class="rc-manage-row">
    <button id="rc-cleanup-btn" class="rc-btn rc-btn-danger" disabled>Delete Events Older Than 2 Months</button>
    <span id="rc-cleanup-status" class="rc-muted"></span>
  </div>
</div>

</div><!-- /.rc-wrap -->

<style>
/* ── Layout ──────────────────────────────────────────────────── */
.rc-wrap { max-width: 860px; margin: 0 auto; }

.rc-section {
  background: #1e293b;
  border: 1px solid rgba(148,163,184,0.15);
  border-radius: 10px;
  padding: 1.1rem 1.3rem;
  margin-bottom: 1.2rem;
}
.rc-section-title {
  margin: 0 0 0.9rem;
  font-size: 0.82rem;
  color: #94a3b8;
  text-transform: uppercase;
  letter-spacing: 0.07em;
  font-weight: 700;
}

/* ── Setup Guide ─────────────────────────────────────────────── */
.rc-setup-guide {
  background: #1e293b;
  border: 1px solid rgba(148,163,184,0.15);
  border-radius: 10px;
  padding: 0.85rem 1.2rem;
  margin-bottom: 1.2rem;
  color: #cbd5e1;
}
.rc-setup-guide summary {
  cursor: pointer;
  font-weight: 600;
  color: #94a3b8;
  user-select: none;
  font-size: 0.92rem;
}
.rc-setup-guide summary:hover { color: #e2e8f0; }
.rc-setup-tag { font-size: 0.76rem; color: #64748b; font-weight: 400; margin-left: 0.3rem; }
.rc-setup-guide ol { margin: 0.8rem 0 0 1.2rem; padding: 0; }
.rc-setup-guide li { margin-bottom: 0.4rem; font-size: 0.88rem; line-height: 1.5; }
.rc-setup-guide code {
  background: #0f172a;
  padding: 0.1em 0.45em;
  border-radius: 4px;
  font-size: 0.83em;
  color: #7dd3fc;
  display: inline-block;
  margin-top: 0.15rem;
}

/* ── Config ──────────────────────────────────────────────────── */
.rc-config-grid { display: flex; flex-direction: column; gap: 0.85rem; }
.rc-field { display: flex; flex-direction: column; gap: 0.3rem; }
.rc-field label { font-size: 0.83rem; color: #94a3b8; }
.rc-field small { color: #64748b; font-size: 0.76rem; }
.rc-input-row { display: flex; gap: 0.5rem; align-items: center; }
.rc-muted { color: #64748b; font-size: 0.88rem; }

.rc-wrap input[type="text"] {
  background: #0f172a;
  border: 1px solid rgba(148,163,184,0.22);
  border-radius: 6px;
  color: #e2e8f0;
  padding: 0.45rem 0.75rem;
  font-size: 0.88rem;
  width: 100%;
  box-sizing: border-box;
  outline: none;
  transition: border-color 0.15s;
}
.rc-wrap input[type="text"]:focus { border-color: #6366f1; }

/* ── Paste area ──────────────────────────────────────────────── */
.rc-hint { color: #64748b; font-size: 0.83rem; margin: 0 0 0.65rem; }
.rc-paste-area {
  width: 100%;
  background: #0f172a;
  border: 1px solid rgba(148,163,184,0.22);
  border-radius: 8px;
  color: #94a3b8;
  padding: 0.75rem;
  font-size: 0.8rem;
  font-family: 'Courier New', monospace;
  resize: vertical;
  box-sizing: border-box;
  outline: none;
  transition: border-color 0.15s;
}
.rc-paste-area:focus { border-color: #6366f1; color: #e2e8f0; }

.rc-options-row { margin-top: 0.75rem; }
.rc-checkbox-label {
  display: flex;
  align-items: center;
  gap: 0.45rem;
  font-size: 0.86rem;
  color: #cbd5e1;
  cursor: pointer;
}

/* ── Auth ────────────────────────────────────────────────────── */
.rc-auth-section { display: flex; align-items: center; gap: 1rem; padding: 0.85rem 1.2rem; }
.rc-auth-status { font-size: 0.88rem; }
.rc-auth-ok { color: #10b981; }
.rc-auth-err { color: #ef4444; }

/* ── Buttons ─────────────────────────────────────────────────── */
.rc-btn {
  padding: 0.48rem 1.1rem;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 0.86rem;
  font-weight: 600;
  background: #334155;
  color: #cbd5e1;
  transition: background 0.15s, opacity 0.15s;
  white-space: nowrap;
}
.rc-btn:hover:not(:disabled) { background: #475569; }
.rc-btn:disabled { opacity: 0.4; cursor: not-allowed; }

.rc-btn-google {
  background: #fff;
  color: #1f2937;
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
}
.rc-btn-google:hover:not(:disabled) { background: #f1f5f9; }

.rc-btn-primary { background: #6366f1; color: #fff; }
.rc-btn-primary:hover:not(:disabled) { background: #4f46e5; }

/* ── Badge ───────────────────────────────────────────────────── */
.rc-badge {
  background: #6366f1;
  color: #fff;
  font-size: 0.75rem;
  padding: 0.1em 0.55em;
  border-radius: 999px;
  vertical-align: middle;
  margin-left: 0.3rem;
}

/* ── Tables (Preview + Manage) ──────────────────────────────── */
.rc-table-wrap {
  overflow-x: auto;
  border-radius: 8px;
  border: 1px solid #e2e8f0;
  background: #fff;
}
.rc-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.85rem;
}
.rc-table th {
  background: #f1f5f9;
  color: #475569;
  padding: 0.55rem 0.85rem;
  text-align: left;
  font-size: 0.72rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.07em;
  white-space: nowrap;
  border-bottom: 2px solid #e2e8f0;
}
.rc-table tbody tr:nth-child(odd)  td { background: #ffffff; }
.rc-table tbody tr:nth-child(even) td { background: #f8fafc; }
.rc-table td {
  padding: 0.52rem 0.85rem;
  color: #334155;
  border-bottom: 1px solid #f1f5f9;
}
.rc-table tbody tr:last-child td { border-bottom: none; }
.rc-table tbody tr:hover td {
  background: #eff6ff !important;
  color: #1e293b;
}
/* Shift colors adjusted for light background */
.rc-table td.shift-1   { color: #0369a1; font-weight: 700; }
.rc-table td.shift-2   { color: #15803d; font-weight: 700; }
.rc-table td.shift-off { color: #b91c1c; font-weight: 700; }

.rc-status-badge {
  display: inline-block;
  font-size: 0.76rem;
  padding: 0.12em 0.5em;
  border-radius: 4px;
  font-weight: 500;
}
.s-pending  { background: #e0e7ff; color: #3730a3; }
.s-ok       { background: #dcfce7; color: #15803d; }
.s-err      { background: #fee2e2; color: #b91c1c; }
.s-skip     { background: #f1f5f9; color: #475569; }

.rc-actions { margin-top: 1rem; display: flex; justify-content: flex-end; }

/* ── Log ─────────────────────────────────────────────────────── */
.rc-log {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  max-height: 240px;
  overflow-y: auto;
  font-size: 0.83rem;
  font-family: 'Courier New', monospace;
}
.rc-log-line { padding: 0.22rem 0.5rem; border-radius: 4px; }
.rc-log-ok   { background: rgba(16,185,129,0.08); color: #6ee7b7; }
.rc-log-err  { background: rgba(239,68,68,0.08);  color: #fca5a5; }
.rc-log-info { color: #64748b; }

/* ── Manage + Cleanup ────────────────────────────────────────── */
.rc-btn-danger { background: #7f1d1d; color: #fca5a5; }
.rc-btn-danger:hover:not(:disabled) { background: #991b1b; }

.rc-manage-row {
  display: flex;
  gap: 0.75rem;
  align-items: flex-end;
  flex-wrap: wrap;
}
.rc-field-inline {
  flex-direction: row;
  align-items: center;
  gap: 0.4rem;
}
.rc-field-inline label { white-space: nowrap; min-width: fit-content; }

.rc-date-input {
  background: #0f172a;
  border: 1px solid rgba(148,163,184,0.22);
  border-radius: 6px;
  color: #e2e8f0;
  padding: 0.42rem 0.6rem;
  font-size: 0.86rem;
  outline: none;
  color-scheme: dark;
  width: 150px;
}
.rc-date-input:focus { border-color: #6366f1; }

.rc-fetched-header {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  margin: 0.9rem 0 0.6rem;
}

.rc-cleanup-section { gap: 0; }

@media (max-width: 600px) {
  .rc-section  { padding: 0.8rem; }
  .rc-auth-section { flex-direction: column; align-items: flex-start; gap: 0.5rem; }
  .rc-manage-row { flex-direction: column; align-items: flex-start; }
}
</style>

<script>
(function () {
  'use strict';

  /* ── Shift config ────────────────────────────────────────────── */
  const SHIFTS = {
    'Shift 1':    { label: 'Shift 1 (8:30 AM - 5:30 PM)',  start: '08:30', end: '17:30', colorId: '7',  emoji: '🔵' },
    'Shift 2':    { label: 'Shift 2 (11:30 AM - 8:30 PM)', start: '11:30', end: '20:30', colorId: '2',  emoji: '🟢' },
    'Weekly Off': { label: 'Weekly Off 🏖️',                                               colorId: '11', emoji: '🔴' }
  };
  const TZ        = 'Asia/Kolkata';
  const TZ_OFFSET = '+05:30';
  const LS_CID    = 'rc_client_id';
  const LS_NAME   = 'rc_name';

  /* ── State ───────────────────────────────────────────────────── */
  let tokenClient  = null;
  let accessToken  = null;
  let parsedEvents = [];   // all detected events (including off days)

  /* ── Helpers ─────────────────────────────────────────────────── */
  const $  = id => document.getElementById(id);
  const p2 = n  => String(n).padStart(2, '0');

  /* ── DOM refs ────────────────────────────────────────────────── */
  const clientIdInput  = $('rc-client-id');
  const nameInput      = $('rc-name');
  const saveCfgBtn     = $('rc-save-cfg');
  const signInBtn      = $('rc-signin');
  const authStatus     = $('rc-auth-status');
  const pasteArea      = $('rc-paste-area');
  const includeOffCb   = $('rc-include-off');
  const previewSection = $('rc-preview-section');
  const eventCountEl   = $('rc-event-count');
  const tbody          = $('rc-tbody');
  const selectAllCb    = $('rc-select-all');
  const createBtn      = $('rc-create-btn');
  const logSection     = $('rc-log-section');
  const logEl          = $('rc-log');

  /* ── Initialise ──────────────────────────────────────────────── */
  function init() {
    clientIdInput.value = localStorage.getItem(LS_CID)  || '';
    nameInput.value     = localStorage.getItem(LS_NAME) || 'Kumar';

    if (clientIdInput.value) loadGIS(clientIdInput.value);

    // Default date range for Manage section: last month → end of next month
    const now  = new Date();
    const from = new Date(now.getFullYear(), now.getMonth() - 1, 1);
    const to   = new Date(now.getFullYear(), now.getMonth() + 2, 0);
    $('rc-from').value = fmtISO(from);
    $('rc-to').value   = fmtISO(to);

    saveCfgBtn.addEventListener('click',   saveConfig);
    signInBtn.addEventListener('click',    requestToken);
    pasteArea.addEventListener('paste',    onPaste);
    selectAllCb.addEventListener('change', toggleAll);
    createBtn.addEventListener('click',    syncEvents);
    includeOffCb.addEventListener('change', () => { if (parsedEvents.length) renderPreview(); });
    $('rc-fetch-btn').addEventListener('click',      fetchAndRender);
    $('rc-fetch-sel-all').addEventListener('change', toggleFetchAll);
    $('rc-delete-sel-btn').addEventListener('click', deleteSelectedFetched);
    $('rc-cleanup-btn').addEventListener('click',    cleanupOldEvents);
  }

  function saveConfig() {
    const cid  = clientIdInput.value.trim();
    const name = nameInput.value.trim();
    if (cid)  localStorage.setItem(LS_CID, cid);
    if (name) localStorage.setItem(LS_NAME, name);
    if (cid)  loadGIS(cid);
    saveCfgBtn.textContent = 'Saved ✓';
    setTimeout(() => { saveCfgBtn.textContent = 'Save'; }, 1800);
  }

  /* ── Google Identity Services ────────────────────────────────── */
  function loadGIS(clientId) {
    if (window.google && window.google.accounts) {
      setupTokenClient(clientId);
      return;
    }
    const s = document.createElement('script');
    s.src = 'https://accounts.google.com/gsi/client';
    s.async = true;
    s.onload  = () => setupTokenClient(clientId);
    s.onerror = () => setAuthStatus('Failed to load Google sign-in library', false);
    document.head.appendChild(s);
  }

  function setupTokenClient(clientId) {
    tokenClient = google.accounts.oauth2.initTokenClient({
      client_id: clientId,
      scope: 'https://www.googleapis.com/auth/calendar.events',
      callback: handleToken
    });
    signInBtn.disabled = false;
  }

  function requestToken() {
    if (!tokenClient) {
      const cid = clientIdInput.value.trim();
      if (!cid) { setAuthStatus('Paste your OAuth Client ID and click Save first', false); return; }
      loadGIS(cid);
      setTimeout(requestToken, 1500);
      return;
    }
    tokenClient.requestAccessToken();
  }

  function handleToken(resp) {
    if (resp.error) { setAuthStatus('Sign-in error: ' + resp.error, false); return; }
    accessToken = resp.access_token;
    setAuthStatus('✓ Signed in', true);
    if (getVisibleEvents().length) createBtn.disabled = false;
    $('rc-fetch-btn').disabled   = false;
    $('rc-cleanup-btn').disabled = false;
  }

  function setAuthStatus(msg, ok) {
    authStatus.textContent = msg;
    authStatus.className   = 'rc-auth-status ' + (ok ? 'rc-auth-ok' : 'rc-auth-err');
  }

  /* ── Paste & Parse ───────────────────────────────────────────── */
  function onPaste(e) {
    e.preventDefault();
    const text = (e.clipboardData || window.clipboardData).getData('text/plain');
    pasteArea.value = text;
    parseRoster(text);
  }

  /* Returns array of lowercased name variants from the config input */
  function getTargetNames() {
    const raw = nameInput.value || localStorage.getItem(LS_NAME) || 'Kumar';
    return raw.split(',').map(s => s.trim().toLowerCase()).filter(Boolean);
  }

  /* Normalise a raw cell string: replace non-breaking spaces, collapse whitespace */
  function normCell(s) {
    return (s || '').replace(/[   \t]/g, ' ').replace(/\s+/g, ' ').trim();
  }

  /* True if any comma-separated token in the cell matches a target name.
     Matches exact token OR any single word within a token (handles "Kumar Raj" vs "Kumar"). */
  function cellContainsName(cell, names) {
    if (!cell) return false;
    const tokens = normCell(cell).split(',')
      .map(s => s.replace(/\s*\([^)]*\)/g, '').trim().toLowerCase())
      .filter(Boolean);
    return tokens.some(t =>
      names.some(n => t === n || t.split(/\s+/).includes(n))
    );
  }

  /* True if the Weekly Off cell marks one of the target names as off */
  function cellIsPersonOff(cell, names) {
    if (!cell || /no weekly off/i.test(normCell(cell))) return false;
    const re = /([^,(]+?)\s*\(\s*off\s*\)/gi;
    let m;
    while ((m = re.exec(normCell(cell))) !== null) {
      const token = m[1].trim().toLowerCase();
      if (names.some(n => token === n || token.split(/\s+/).includes(n))) return true;
    }
    return false;
  }

  /* Parse "1-May-26" or "1-May-2026" → Date (local midnight) */
  function parseRosterDate(str) {
    const parts = str.trim().split('-');
    if (parts.length !== 3) return null;
    const [d, mon, yy] = parts;
    const year = yy.length === 2 ? `20${yy}` : yy;
    const dt = new Date(`${d} ${mon} ${year}`);
    return isNaN(dt.getTime()) ? null : dt;
  }

  function fmtISO(date) {
    return `${date.getFullYear()}-${p2(date.getMonth()+1)}-${p2(date.getDate())}`;
  }

  function toDateTime(date, time) {
    return `${fmtISO(date)}T${time}:00${TZ_OFFSET}`;
  }

  function parseRoster(text) {
    // Handle both \r\n (Windows/Excel) and \n line endings
    const rows = text.split(/\r?\n/).map(r => r.split('\t').map(c => normCell(c)));
    if (rows.length < 2) return;

    if (!text.includes('\t')) {
      logLine('⚠ No tab characters found. Copy the cells directly from Excel — do not paste from a chat or email.', 'err');
      logSection.hidden = false;
      return;
    }

    // Find the header row — first row that has a cell matching "Shift"
    let hi = rows.findIndex(r => r.some(c => /shift\s*\d/i.test(c)));
    if (hi < 0) hi = 0;
    const headers = rows[hi];

    // Detect column indices
    const colDate   = 0;
    const colShift1 = headers.findIndex(h => /shift\s*1/i.test(h));
    const colShift2 = headers.findIndex(h => /shift\s*2/i.test(h));
    const colOff    = headers.findIndex(h => /weekly\s*off/i.test(h));

    if (colShift1 < 0 && colShift2 < 0) {
      logLine('Could not find "Shift 1" or "Shift 2" columns in the header row. Make sure you include the header when copying from Excel.', 'err');
      logSection.hidden = false;
      return;
    }

    // Keep full header labels (e.g. "Shift 1 (8:30 AM - 5:30 PM)") for event descriptions
    const hdr1 = colShift1 >= 0 ? headers[colShift1] : 'Shift 1';
    const hdr2 = colShift2 >= 0 ? headers[colShift2] : 'Shift 2';

    const names = getTargetNames();
    parsedEvents = [];

    for (let i = hi + 1; i < rows.length; i++) {
      const row = rows[i];
      if (!row || row.every(c => !c)) continue;

      const dateStr = row[colDate] || '';
      const date    = parseRosterDate(dateStr);
      if (!date) continue;

      const dayName  = (row[1] || '').trim();
      const s1cell   = colShift1 >= 0 ? (row[colShift1] || '') : '';
      const s2cell   = colShift2 >= 0 ? (row[colShift2] || '') : '';
      const offCell  = colOff    >= 0 ? (row[colOff]    || '') : '';
      const rowCtx   = { s1cell, s2cell, offCell, hdr1, hdr2 };

      if (colShift1 >= 0 && cellContainsName(s1cell, names)) {
        parsedEvents.push({ date, dateStr, dayName, shift: 'Shift 1', ...rowCtx });
      }
      if (colShift2 >= 0 && cellContainsName(s2cell, names)) {
        parsedEvents.push({ date, dateStr, dayName, shift: 'Shift 2', ...rowCtx });
      }
      if (cellIsPersonOff(offCell, names)) {
        parsedEvents.push({ date, dateStr, dayName, shift: 'Weekly Off', ...rowCtx });
      }
    }

    if (parsedEvents.length === 0) {
      logSection.hidden = false;
      logLine(`No events found for name(s): "${getTargetNames().join(', ')}".`, 'err');
      // Show first data row cells to help diagnose the mismatch
      const sample = rows[hi + 1];
      if (sample) {
        logLine(`First data row → col0="${sample[0]}"  shift1-col="${sample[colShift1] || '—'}"  shift2-col="${sample[colShift2] || '—'}"  off-col="${sample[colOff] || '—'}"`, 'info');
        logLine(`If the names above look correct, check spelling in the Name field (currently: "${nameInput.value}").`, 'info');
      }
    }

    renderPreview();
  }

  /* ── Preview ─────────────────────────────────────────────────── */
  function getVisibleEvents() {
    const incOff = includeOffCb.checked;
    return parsedEvents.filter(ev => ev.shift !== 'Weekly Off' || incOff);
  }

  function renderPreview() {
    const visible = getVisibleEvents();
    tbody.innerHTML = '';

    visible.forEach((ev, idx) => {
      const cfg   = SHIFTS[ev.shift];
      const isOff = ev.shift === 'Weekly Off';
      const tr    = document.createElement('tr');
      if (isOff) tr.className = 'rc-row-off';

      tr.innerHTML = `
        <td><input type="checkbox" class="rc-row-cb" checked data-idx="${idx}"></td>
        <td>${ev.dateStr}</td>
        <td>${ev.dayName}</td>
        <td class="${isOff ? 'shift-off' : ev.shift === 'Shift 1' ? 'shift-1' : 'shift-2'}">${ev.shift}</td>
        <td>${isOff ? '—' : cfg.start}</td>
        <td>${isOff ? '—' : cfg.end}</td>
        <td><span class="rc-status-badge s-pending" id="rc-s-${idx}">Pending</span></td>
      `;
      tbody.appendChild(tr);
    });

    eventCountEl.textContent = visible.length;
    previewSection.hidden    = visible.length === 0;
    selectAllCb.checked      = true;
    createBtn.disabled       = !(accessToken && visible.length > 0);
  }

  function toggleAll() {
    document.querySelectorAll('.rc-row-cb')
      .forEach(cb => { cb.checked = selectAllCb.checked; });
  }

  /* Splits a roster cell into clean name tokens (strips parenthetical suffixes) */
  function cleanNames(cell) {
    return (cell || '').split(',')
      .map(s => s.replace(/\s*\([^)]*\)/g, '').trim())
      .filter(Boolean);
  }

  /* Builds the event summary, appending [No Weekly Off] when applicable */
  function buildSummary(ev) {
    let label = SHIFTS[ev.shift].label;
    if (ev.shift !== 'Weekly Off' && /no weekly off/i.test((ev.offCell || '').trim())) {
      label += ' [No Weekly Off]';
    }
    return label;
  }

  /* Builds the event description — always shows all 3 rows with clean names */
  function buildDescription(ev) {
    const noWeeklyOff = /no weekly off/i.test((ev.offCell || '').trim());

    const s1Names  = cleanNames(ev.s1cell).join(' + ') || '—';
    const s2Names  = cleanNames(ev.s2cell).join(' + ') || '—';
    const offNames = noWeeklyOff ? 'No Weekly Off' : (cleanNames(ev.offCell).join(', ') || '—');

    return [
      `🔵 Shift 1 (8:30 AM - 5:30 PM)  : ${s1Names}${ev.shift === 'Shift 1' ? '  ← on duty' : ''}`,
      `🟢 Shift 2 (11:30 AM - 8:30 PM) : ${s2Names}${ev.shift === 'Shift 2' ? '  ← on duty' : ''}`,
      `🔴 Weekly Off                    : ${offNames}${ev.shift === 'Weekly Off' ? '  ← off today' : ''}`
    ].join('\n');
  }

  /* ── Shared Calendar API helper ─────────────────────────────── */
  async function calApi(method, path, body) {
    const res = await fetch(`https://www.googleapis.com/calendar/v3${path}`, {
      method,
      headers: {
        'Authorization': `Bearer ${accessToken}`,
        ...(body ? { 'Content-Type': 'application/json' } : {})
      },
      ...(body ? { body: JSON.stringify(body) } : {})
    });
    if (res.status === 401) throw new Error('TOKEN_EXPIRED');
    if (!res.ok && res.status !== 204 && res.status !== 410) {
      throw new Error(`HTTP ${res.status}: ${await res.text()}`);
    }
    return res.status === 204 || res.status === 410 ? null : res.json();
  }

  /* Builds the event body object */
  function buildBody(ev) {
    const cfg     = SHIFTS[ev.shift];
    const summary = buildSummary(ev);
    const desc    = buildDescription(ev);
    const isOff   = ev.shift === 'Weekly Off';
    return isOff
      ? { summary, description: desc,
          start: { dateTime: toDateTime(ev.date, '00:00'), timeZone: TZ },
          end:   { dateTime: `${fmtISO(ev.date)}T23:59:59${TZ_OFFSET}`, timeZone: TZ },
          colorId: cfg.colorId }
      : { summary, description: desc, location: 'Office',
          start: { dateTime: toDateTime(ev.date, cfg.start), timeZone: TZ },
          end:   { dateTime: toDateTime(ev.date, cfg.end),   timeZone: TZ },
          colorId: cfg.colorId,
          reminders: { useDefault: false, overrides: [{ method: 'popup', minutes: 30 }] } };
  }

  /* ── Create / Update (smart upsert) ─────────────────────────── */
  async function syncEvents() {
    if (!accessToken) { setAuthStatus('Sign in with Google first', false); return; }

    const visible = getVisibleEvents();
    logSection.hidden  = false;
    logEl.innerHTML    = '';
    createBtn.disabled = true;

    // Fetch existing roster events for the same date range to enable upsert
    logLine('Checking for existing events…', 'info');
    let existingMap = {};
    try {
      if (visible.length) {
        const dates   = visible.map(ev => ev.date.getTime());
        const minDate = new Date(Math.min(...dates));
        const maxDate = new Date(Math.max(...dates));
        maxDate.setDate(maxDate.getDate() + 1);
        const existing = await fetchRosterEvents(minDate, maxDate);
        for (const e of existing) {
          const dk = (e.start.dateTime || e.start.date || '').substring(0, 10);
          const sk = /Shift 1/i.test(e.summary) ? 'Shift 1'
            : /Shift 2/i.test(e.summary) ? 'Shift 2' : 'Weekly Off';
          if (!existingMap[dk]) existingMap[dk] = {};
          existingMap[dk][sk] = e.id;
        }
        logLine(`Found ${existing.length} existing roster event(s) in this range.`, 'info');
      }
    } catch (e) {
      logLine(`Could not check existing events (${e.message}). Will create new ones.`, 'info');
    }

    let created = 0, updated = 0, skipped = 0, errs = 0;

    for (let i = 0; i < visible.length; i++) {
      const cb = document.querySelector(`.rc-row-cb[data-idx="${i}"]`);
      if (cb && !cb.checked) { skipped++; setRowStatus(i, 's-skip', 'Skipped'); continue; }

      const ev         = visible[i];
      const dateKey    = fmtISO(ev.date);
      const existingId = existingMap[dateKey]?.[ev.shift];
      const body       = buildBody(ev);

      try {
        if (existingId) {
          await calApi('PUT', `/calendars/primary/events/${existingId}`, body);
          setRowStatus(i, 's-ok', '✏️ Updated');
          logLine(`✏️  ${ev.dateStr} (${ev.dayName}) — ${ev.shift} updated`, 'ok');
          updated++;
        } else {
          await calApi('POST', '/calendars/primary/events', body);
          setRowStatus(i, 's-ok', '✅ Created');
          logLine(`✅  ${ev.dateStr} (${ev.dayName}) — ${ev.shift} created`, 'ok');
          created++;
        }
      } catch (e) {
        if (e.message === 'TOKEN_EXPIRED') {
          logLine('Token expired — sign in again and re-run.', 'err');
          setRowStatus(i, 's-err', '❌ Auth'); errs++; break;
        }
        setRowStatus(i, 's-err', '❌ Error');
        logLine(`❌  ${ev.dateStr} — ${ev.shift}: ${e.message}`, 'err');
        errs++;
      }
    }

    logLine(`─── Done: ${created} created  •  ${updated} updated  •  ${errs} errors  •  ${skipped} skipped ───`, 'info');
    createBtn.disabled = false;
  }

  /* ── Read: fetch roster events from Google Calendar ─────────── */
  function isRosterEvent(ev) {
    return /^Shift [12]/i.test(ev.summary || '') || /^Weekly Off/i.test(ev.summary || '');
  }

  async function fetchRosterEvents(timeMin, timeMax) {
    const p = new URLSearchParams({
      timeMin: timeMin.toISOString(), timeMax: timeMax.toISOString(),
      singleEvents: 'true', orderBy: 'startTime', maxResults: '500'
    });
    const data = await calApi('GET', `/calendars/primary/events?${p}`);
    return (data?.items || []).filter(isRosterEvent);
  }

  async function fetchAndRender() {
    if (!accessToken) { setAuthStatus('Sign in with Google first', false); return; }
    const from = new Date($('rc-from').value);
    const to   = new Date($('rc-to').value);
    to.setDate(to.getDate() + 1);
    $('rc-fetch-btn').disabled  = true;
    $('rc-fetch-btn').textContent = 'Fetching…';
    try {
      const events = await fetchRosterEvents(from, to);
      renderFetchedEvents(events);
    } catch (e) {
      logSection.hidden = false;
      logLine(`Fetch error: ${e.message}`, 'err');
    }
    $('rc-fetch-btn').disabled    = false;
    $('rc-fetch-btn').textContent = 'Fetch Events';
  }

  function renderFetchedEvents(events) {
    const tbody = $('rc-fetched-tbody');
    tbody.innerHTML = '';
    events.forEach((ev, idx) => {
      const rawStart  = ev.start.dateTime || ev.start.date || '';
      const dateStr   = rawStart.substring(0, 10);
      const dayName   = rawStart
        ? new Date(rawStart).toLocaleDateString('en-IN', { weekday: 'short' }) : '';
      const timeStr   = ev.start.dateTime
        ? new Date(ev.start.dateTime).toLocaleTimeString('en-IN', { hour: '2-digit', minute: '2-digit', hour12: true })
        : 'All day';
      const cls = /Shift 1/i.test(ev.summary) ? 'shift-1'
        : /Shift 2/i.test(ev.summary) ? 'shift-2' : 'shift-off';
      const tr = document.createElement('tr');
      tr.dataset.eid = ev.id;
      tr.innerHTML = `
        <td><input type="checkbox" class="rc-fetch-cb" checked data-idx="${idx}"></td>
        <td>${dateStr}</td>
        <td>${dayName}</td>
        <td class="${cls}">${ev.summary}</td>
        <td>${timeStr}</td>
        <td><span class="rc-status-badge s-pending" id="rc-fst-${idx}">—</span></td>
      `;
      tbody.appendChild(tr);
    });
    $('rc-fetched-count').textContent = events.length;
    $('rc-fetched-wrap').hidden       = events.length === 0;
  }

  function toggleFetchAll() {
    const checked = $('rc-fetch-sel-all').checked;
    document.querySelectorAll('.rc-fetch-cb').forEach(cb => { cb.checked = checked; });
  }

  /* ── Delete: remove selected fetched events ──────────────────── */
  async function deleteSelectedFetched() {
    if (!accessToken) { setAuthStatus('Sign in with Google first', false); return; }
    const rows = [...document.querySelectorAll('#rc-fetched-tbody tr')];
    logSection.hidden = false;
    let ok = 0, errs = 0;

    for (const row of rows) {
      const cb  = row.querySelector('.rc-fetch-cb');
      if (!cb || !cb.checked) continue;
      const idx = cb.dataset.idx;
      const eid = row.dataset.eid;
      try {
        await calApi('DELETE', `/calendars/primary/events/${eid}`);
        const st = $(`rc-fst-${idx}`);
        if (st) { st.className = 'rc-status-badge s-ok'; st.textContent = '✅ Deleted'; }
        row.style.opacity = '0.4';
        ok++;
      } catch (e) {
        const st = $(`rc-fst-${idx}`);
        if (st) { st.className = 'rc-status-badge s-err'; st.textContent = '❌ Error'; }
        logLine(`❌  Delete failed for event ${eid}: ${e.message}`, 'err');
        errs++;
      }
    }
    logLine(`─── Delete: ${ok} removed  •  ${errs} errors ───`, ok > 0 ? 'ok' : 'err');
  }

  /* ── Delete: cleanup events older than 2 months ─────────────── */
  async function cleanupOldEvents() {
    if (!accessToken) { setAuthStatus('Sign in with Google first', false); return; }
    const btn    = $('rc-cleanup-btn');
    const status = $('rc-cleanup-status');
    btn.disabled = true;
    status.textContent = 'Scanning…';

    try {
      const cutoff  = new Date();
      cutoff.setMonth(cutoff.getMonth() - 2);
      const farPast = new Date('2020-01-01');
      const events  = await fetchRosterEvents(farPast, cutoff);

      if (events.length === 0) {
        status.textContent = 'No old events found.';
        btn.disabled = false;
        return;
      }

      const confirmed = confirm(
        `Found ${events.length} roster event(s) before ${cutoff.toDateString()}.\n\nDelete all of them?`
      );
      if (!confirmed) { status.textContent = 'Cancelled.'; btn.disabled = false; return; }

      logSection.hidden = false;
      logLine(`Deleting ${events.length} old events…`, 'info');
      let ok = 0, errs = 0;

      for (const ev of events) {
        try {
          await calApi('DELETE', `/calendars/primary/events/${ev.id}`);
          ok++;
        } catch { errs++; }
      }

      status.textContent = `Done — ${ok} deleted, ${errs} errors.`;
      logLine(`─── Cleanup: ${ok} deleted  •  ${errs} errors ───`, ok > 0 ? 'ok' : 'err');
    } catch (e) {
      status.textContent = `Error: ${e.message}`;
      logLine(`Cleanup error: ${e.message}`, 'err');
    }
    btn.disabled = false;
  }

  function setRowStatus(idx, cls, text) {
    const el = $(`rc-s-${idx}`);
    if (!el) return;
    el.className  = `rc-status-badge ${cls}`;
    el.textContent = text;
  }

  function logLine(msg, type) {
    const d = document.createElement('div');
    d.className   = `rc-log-line rc-log-${type}`;
    d.textContent = msg;
    logEl.appendChild(d);
    logEl.scrollTop = logEl.scrollHeight;
  }

  /* ── Boot ────────────────────────────────────────────────────── */
  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', init);
  } else {
    init();
  }
})();
</script>
