# Codex UI Design System — Skill Guide

> **For AI Agents:** This document defines a strict, opinionated design system. Follow every rule precisely. When in doubt, **ask the user for the brand/product prefix** before writing a single line of code. Do not invent prefixes. Do not deviate from the design tokens. Do not use hardcoded color values anywhere — always use CSS variables.

---

## 0. Before You Write Anything

- **Ask the user**: *"What is the prefix for this project? (e.g., your brand name or product name, like `acme` or `nova`)"*
- Replace every instance of `{prefix}` in this guide with that value.
- If the user cannot decide, default to `app` and note it in a comment at the top of the file.
- Never use generic class names like `.container`, `.card`, `.wrapper` — always use `{prefix}-` as a namespace.

---

## 1. CSS Design Tokens (`:root`)

Declare **all** tokens in `:root` and `[data-theme="light"]`. Override only what changes in `[data-theme="dark"]`. **Never hardcode any color, shadow, radius, or font value outside of these token blocks.**

### 1.1 Background & Surface Tokens

```css
:root, [data-theme="light"] {
  --{prefix}-bg:               #f1f1f1;
  --{prefix}-bg-subtle:        #f9f9f9;
  --{prefix}-surface:          #ffffff;
  --{prefix}-surface-hover:    #f7f7f5;
  --{prefix}-surface-raised:   #ffffff;
}

[data-theme="dark"] {
  --{prefix}-bg:               #141413;
  --{prefix}-bg-subtle:        #1c1c1a;
  --{prefix}-surface:          #1f1f1d;
  --{prefix}-surface-hover:    #30302e;
  --{prefix}-surface-raised:   #252523;
}
```

### 1.2 Border Tokens

```css
:root, [data-theme="light"] {
  --{prefix}-border:           rgba(0, 0, 0, 0.10);
  --{prefix}-border-mid:       rgba(0, 0, 0, 0.16);
  --{prefix}-border-strong:    rgba(0, 0, 0, 0.22);
  --{prefix}-border-focus:     rgba(0, 0, 0, 0.30);
}

[data-theme="dark"] {
  --{prefix}-border:           rgba(255, 255, 255, 0.08);
  --{prefix}-border-mid:       rgba(255, 255, 255, 0.12);
  --{prefix}-border-strong:    rgba(255, 255, 255, 0.18);
  --{prefix}-border-focus:     rgba(255, 255, 255, 0.28);
}
```

### 1.3 Typography Tokens

```css
:root, [data-theme="light"] {
  --{prefix}-text:             #111110;
  --{prefix}-text-2:           #3a3a38;
  --{prefix}-text-3:           #32322f;
  --{prefix}-text-4:           #a8a8a3;
}

[data-theme="dark"] {
  --{prefix}-text:             #edede9;
  --{prefix}-text-2:           #c4c4be;
  --{prefix}-text-3:           #7c7c76;
  --{prefix}-text-4:           #505050;
}
```

### 1.4 Accent Tokens

```css
:root, [data-theme="light"] {
  --{prefix}-accent:           #1a1a18;
  --{prefix}-accent-text:      #ffffff;
}

[data-theme="dark"] {
  --{prefix}-accent:           #e8e8e3;
  --{prefix}-accent-text:      #111110;
}
```

> **Note:** The accent automatically inverts between light and dark — it is always a high-contrast dark/light fill with opposing text. Do not change this pattern.

### 1.5 Semantic Color Tokens

```css
:root, [data-theme="light"] {
  --{prefix}-success:          #15803d;
  --{prefix}-success-bg:       #f0fdf4;
  --{prefix}-success-border:   rgba(21, 128, 61, 0.20);

  --{prefix}-error:            #b91c1c;
  --{prefix}-error-bg:         #fef2f2;
  --{prefix}-error-border:     rgba(185, 28, 28, 0.20);

  --{prefix}-warning:          #b45309;
  --{prefix}-warning-bg:       #fffbeb;
  --{prefix}-warning-border:   rgba(180, 83, 9, 0.20);

  --{prefix}-info:             #1d4ed8;
  --{prefix}-info-bg:          #eff6ff;
  --{prefix}-info-border:      rgba(29, 78, 216, 0.20);
}

[data-theme="dark"] {
  --{prefix}-success:          #4ade80;
  --{prefix}-success-bg:       rgba(74, 222, 128, 0.08);
  --{prefix}-success-border:   rgba(74, 222, 128, 0.22);

  --{prefix}-error:            #f87171;
  --{prefix}-error-bg:         rgba(248, 113, 113, 0.08);
  --{prefix}-error-border:     rgba(248, 113, 113, 0.22);

  --{prefix}-warning:          #fbbf24;
  --{prefix}-warning-bg:       rgba(251, 191, 36, 0.08);
  --{prefix}-warning-border:   rgba(251, 191, 36, 0.22);

  --{prefix}-info:             #60a5fa;
  --{prefix}-info-bg:          rgba(96, 165, 250, 0.08);
  --{prefix}-info-border:      rgba(96, 165, 250, 0.22);
}
```

### 1.6 Shadow Tokens

```css
:root, [data-theme="light"] {
  --{prefix}-shadow-sm:  0 1px 3px rgba(0,0,0,0.07), 0 1px 2px rgba(0,0,0,0.05);
  --{prefix}-shadow-md:  0 4px 12px rgba(0,0,0,0.07), 0 2px 4px rgba(0,0,0,0.05);
  --{prefix}-shadow-lg:  0 8px 24px rgba(0,0,0,0.09), 0 4px 8px rgba(0,0,0,0.06);
}

[data-theme="dark"] {
  --{prefix}-shadow-sm:  0 1px 3px rgba(0,0,0,0.25), 0 1px 2px rgba(0,0,0,0.20);
  --{prefix}-shadow-md:  0 4px 12px rgba(0,0,0,0.30), 0 2px 4px rgba(0,0,0,0.20);
  --{prefix}-shadow-lg:  0 8px 24px rgba(0,0,0,0.40), 0 4px 8px rgba(0,0,0,0.25);
}
```

### 1.7 Shape & Font Tokens

```css
:root {
  --{prefix}-radius:     9px;
  --{prefix}-radius-sm:  6px;
  --{prefix}-radius-lg:  14px;

  --{prefix}-font:       "Geist", -apple-system, BlinkMacSystemFont, sans-serif;
  --{prefix}-mono:       "Geist Mono", "SF Mono", monospace;
  --{prefix}-serif:      "Instrument Serif", Georgia, serif;
}
```

### 1.8 Tab-Specific Tokens

```css
:root, [data-theme="light"] {
  --{prefix}-tab-track-bg:     #e5e4e4;
  --{prefix}-tab-active-bg:    var(--{prefix}-surface);
  --{prefix}-tab-active-text:  var(--{prefix}-text);
  --{prefix}-tab-idle-text:    var(--{prefix}-text-3);
}

[data-theme="dark"] {
  --{prefix}-tab-track-bg:     #2a2a28;
  --{prefix}-tab-active-bg:    var(--{prefix}-surface-raised);
  --{prefix}-tab-active-text:  var(--{prefix}-text);
  --{prefix}-tab-idle-text:    var(--{prefix}-text-3);
}
```

---

## 2. Reset & Base

```css
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  font-size: 15px;
  color-scheme: dark light;
}

body {
  font-family: var(--{prefix}-font);
  background: var(--{prefix}-bg);
  color: var(--{prefix}-text);
  min-height: 100vh;
  -webkit-font-smoothing: antialiased;
  transition: background 0.3s ease, color 0.3s ease;
}
```

---

## 3. HTML Structure

- **Always wrap the entire page** in `<div class="{prefix}-shell">`.
- Inside the shell, use **three semantic regions**: `{prefix}-top-header`, `{prefix}-content`, and either `{prefix}-footer` or `{prefix}-sidebar` depending on layout.
- Each region is a `<div>` with a **compound class**: `<div class="{prefix}-design-card {prefix}-top-header">`.

### 3.1 Shell

```html
<div class="{prefix}-shell">
  <div class="{prefix}-design-card {prefix}-top-header"> … </div>
  <div class="{prefix}-design-card {prefix}-content">    … </div>
  <div class="{prefix}-design-card {prefix}-footer">     … </div>
  <!-- OR: -->
  <div class="{prefix}-design-card {prefix}-sidebar">    … </div>
</div>
```

```css
.{prefix}-shell {
  max-width: 900px;
  margin: 0 auto;
  padding: 0 28px 80px;
}
```

### 3.2 Design Card (base surface)

Every region, panel, output pane, and floating element uses this pattern. Height is **never** set on a card — let content define it.

```css
.{prefix}-design-card {
  background: var(--{prefix}-surface);
  border-radius: var(--{prefix}-radius);
  box-shadow: var(--{prefix}-shadow-sm);
  overflow: hidden;
  transition: background 0.3s ease;
}
```

---

## 4. Topbar / Header

```html
<div class="{prefix}-design-card {prefix}-top-header">
  <div class="{prefix}-brand">
    <div class="{prefix}-brand-mark"> <!-- logo SVG --> </div>
    <span class="{prefix}-brand-name">Product <em>Name</em></span>
  </div>
  <div class="{prefix}-header-actions">
    <!-- theme toggle, nav items, etc. -->
  </div>
</div>
```

```css
.{prefix}-top-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px 0;
  border-bottom: 1px solid var(--{prefix}-border-mid);
  margin-bottom: 36px;
}

.{prefix}-brand {
  display: flex;
  align-items: center;
  gap: 11px;
}

.{prefix}-brand-mark {
  width: 30px;
  height: 30px;
  background: var(--{prefix}-accent);
  border-radius: 7px;
  display: grid;
  place-items: center;
  box-shadow: var(--{prefix}-shadow-sm);
  transition: background 0.3s ease;
}

.{prefix}-brand-mark svg {
  width: 16px;
  height: 16px;
  stroke: var(--{prefix}-accent-text);
  transition: stroke 0.3s ease;
}

.{prefix}-brand-name {
  font-size: 17px;
  font-weight: 600;
  letter-spacing: -0.5px;
  color: var(--{prefix}-text);
}

.{prefix}-brand-name em {
  font-family: var(--{prefix}-serif);
  font-style: italic;
  font-weight: 400;
}
```

---

## 5. Buttons

Use compound class syntax: `{prefix}-design-btn` is the base, modifiers are appended as additional classes.

### Rules
- **Never** hardcode button colors. Always use token variables.
- **Always** include `outline: 3px solid transparent` and a focused/active outline state.
- **Always** include `transition` on background, color, opacity, and outline.
- Disabled state: `opacity: 0.4; cursor: not-allowed`.

### 5.1 Button Base

```css
.{prefix}-design-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 10px 22px;
  border: none;
  border-radius: var(--{prefix}-radius-sm);
  font-family: var(--{prefix}-font);
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  letter-spacing: -0.2px;
  outline: 3px solid transparent;
  box-shadow: var(--{prefix}-shadow-sm);
  transition: opacity 0.3s ease, outline 0.3s ease, background 0.3s ease, color 0.3s ease;
  user-select: none;
}

.{prefix}-design-btn svg {
  width: 15px;
  height: 15px;
  flex-shrink: 0;
}

.{prefix}-design-btn:disabled {
  opacity: 0.4;
  cursor: not-allowed;
}
```

### 5.2 Primary (default — accent fill)

```css
.{prefix}-design-btn {
  background: var(--{prefix}-accent);
  color: var(--{prefix}-accent-text);
}

.{prefix}-design-btn:hover   { opacity: 0.82; }
.{prefix}-design-btn:active  { opacity: 0.72; outline: 3px solid rgba(0,0,0,0.45); }

[data-theme="dark"] .{prefix}-design-btn:active {
  outline: 3px solid rgba(255,255,255,0.25);
}
```

### 5.3 White / Ghost

```css
.{prefix}-design-btn.{prefix}-design-btn--white {
  background: var(--{prefix}-surface);
  color: var(--{prefix}-text-2);
}

.{prefix}-design-btn.{prefix}-design-btn--white:hover {
  background: var(--{prefix}-surface-hover);
  color: var(--{prefix}-text);
}

.{prefix}-design-btn.{prefix}-design-btn--white:active {
  outline: 3px solid rgba(0,0,0,0.45);
}

[data-theme="dark"] .{prefix}-design-btn.{prefix}-design-btn--white:active {
  outline: 3px solid rgba(255,255,255,0.25);
}
```

### 5.4 Red / Destructive

```css
.{prefix}-design-btn.{prefix}-design-btn--red {
  background: var(--{prefix}-error-bg);
  color: var(--{prefix}-error);
  box-shadow: none;
}

.{prefix}-design-btn.{prefix}-design-btn--red:hover {
  background: var(--{prefix}-error);
  color: #ffffff;
}

.{prefix}-design-btn.{prefix}-design-btn--red:active {
  outline: 3px solid var(--{prefix}-error-border);
}
```

Use for: delete, reset, restore, remove, revoke.

### 5.5 Dark / Filled Black

```css
.{prefix}-design-btn.{prefix}-design-btn--dark {
  background: #111110;
  color: #ffffff;
}

[data-theme="dark"] .{prefix}-design-btn.{prefix}-design-btn--dark {
  background: #edede9;
  color: #111110;
}

.{prefix}-design-btn.{prefix}-design-btn--dark:hover { opacity: 0.85; }
```

### 5.6 Loading Spinner (inside any button)

```html
<button class="{prefix}-design-btn {prefix}-loading">
  <svg class="{prefix}-btn-icon"> … </svg>
  <span class="{prefix}-spin"></span>
  Label
</button>
```

```css
.{prefix}-spin {
  width: 14px;
  height: 14px;
  border: 2px solid currentColor;
  border-top-color: transparent;
  border-radius: 50%;
  animation: {prefix}-spin 0.7s linear infinite;
  display: none;
}

.{prefix}-loading .{prefix}-btn-icon { display: none; }
.{prefix}-loading .{prefix}-spin     { display: block; }

@keyframes {prefix}-spin {
  to { transform: rotate(360deg); }
}
```

---

## 6. Tabs

Use compound class: `{prefix}-design-tab` on the track, `{prefix}-design-tab-btn` on each tab.

### 6.1 HTML Structure

```html
<div class="{prefix}-design-tab" role="tablist">
  <button class="{prefix}-design-tab-btn {prefix}-active" role="tab">Tab One</button>
  <button class="{prefix}-design-tab-btn" role="tab">Tab Two</button>
  <button class="{prefix}-design-tab-btn" role="tab">Tab Three</button>
  <div class="{prefix}-tab-indicator" aria-hidden="true"></div>
</div>
```

### 6.2 CSS

```css
.{prefix}-design-tab {
  position: relative;
  display: inline-flex;
  align-items: center;
  gap: 2px;
  background: var(--{prefix}-tab-track-bg);
  border-radius: 8px;
  padding: 3px;
}

.{prefix}-design-tab-btn {
  position: relative;
  z-index: 1;
  padding: 7px 14px;
  background: transparent;
  border: none;
  font-family: var(--{prefix}-font);
  font-size: 13.5px;
  font-weight: 500;
  color: var(--{prefix}-tab-idle-text);
  cursor: pointer;
  border-radius: var(--{prefix}-radius-sm);
  outline: 3px solid transparent;
  transition: color 0.2s ease, outline 0.2s ease;
  white-space: nowrap;
  user-select: none;
}

.{prefix}-design-tab-btn.{prefix}-active {
  color: var(--{prefix}-tab-active-text);
  font-weight: 600;
}

/* Animated sliding pill indicator */
.{prefix}-tab-indicator {
  position: absolute;
  top: 3px;
  left: 3px;
  height: calc(100% - 6px);
  background: var(--{prefix}-tab-active-bg);
  border-radius: var(--{prefix}-radius-sm);
  box-shadow: var(--{prefix}-shadow-sm);
  transition: transform 0.25s cubic-bezier(0.4, 0, 0.2, 1),
              width 0.25s cubic-bezier(0.4, 0, 0.2, 1);
  pointer-events: none;
  z-index: 0;
}
```

### 6.3 JavaScript — Sliding Pill

```js
function initTabs(trackSelector) {
  const track = document.querySelector(trackSelector);
  if (!track) return;
  const btns = track.querySelectorAll('.{prefix}-design-tab-btn');
  const pill = track.querySelector('.{prefix}-tab-indicator');

  function movePill(btn) {
    pill.style.width     = btn.offsetWidth + 'px';
    pill.style.transform = `translateX(${btn.offsetLeft - 3}px)`;
  }

  // Init pill on active button
  const active = track.querySelector('.{prefix}-active') || btns[0];
  movePill(active);

  btns.forEach(btn => {
    btn.addEventListener('click', () => {
      btns.forEach(b => b.classList.remove('{prefix}-active'));
      btn.classList.add('{prefix}-active');
      movePill(btn);
      // Dispatch custom event so panels can respond
      track.dispatchEvent(new CustomEvent('{prefix}-tab-change', { detail: { btn } }));
    });
  });
}
```

> The pill slides in the **exact direction** of the click — left-to-right or right-to-left — because it uses `translateX` with a `cubic-bezier` transition. No extra logic needed.

---

## 7. Form Inputs

```css
.{prefix}-input,
.{prefix}-textarea {
  width: 100%;
  background: var(--{prefix}-surface);
  border: none;
  border-radius: var(--{prefix}-radius);
  padding: 10px 14px;
  font-family: var(--{prefix}-font);
  font-size: 14px;
  color: var(--{prefix}-text);
  outline: 3px solid transparent;
  box-shadow: var(--{prefix}-shadow-sm);
  transition: background 0.3s ease, outline 0.3s ease;
}

.{prefix}-textarea {
  font-family: var(--{prefix}-mono);
  font-size: 13px;
  line-height: 1.65;
  resize: vertical;
  min-height: 120px;
}

.{prefix}-input::placeholder,
.{prefix}-textarea::placeholder {
  color: var(--{prefix}-text-4);
}

.{prefix}-input:focus,
.{prefix}-textarea:focus {
  outline: 3px solid var(--{prefix}-border-focus);
}

[data-theme="dark"] .{prefix}-input:focus,
[data-theme="dark"] .{prefix}-textarea:focus {
  outline: 3px solid rgba(255,255,255,0.25);
}

.{prefix}-input-label {
  display: block;
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  color: var(--{prefix}-text-4);
  margin-bottom: 10px;
}
```

---

## 8. Tables

Tables follow the same design language — use `var()` tokens everywhere, no hardcoded values.

```html
<div class="{prefix}-design-card {prefix}-table-wrap">
  <table class="{prefix}-table">
    <thead>
      <tr>
        <th>Column</th>
        <th>Column</th>
      </tr>
    </thead>
    <tbody>
      <tr><td>Value</td><td>Value</td></tr>
    </tbody>
  </table>
</div>
```

```css
.{prefix}-table-wrap {
  overflow-x: auto;
}

.{prefix}-table {
  border-collapse: collapse;
  width: 100%;
  font-size: 13.5px;
  color: var(--{prefix}-text);
}

.{prefix}-table th {
  background: var(--{prefix}-bg);
  text-align: left;
  padding: 8px 12px;
  font-weight: 600;
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--{prefix}-text-3);
  border-bottom: 2px solid var(--{prefix}-border-mid);
}

.{prefix}-table td {
  padding: 9px 12px;
  border-bottom: 1px solid var(--{prefix}-border);
  vertical-align: top;
  color: var(--{prefix}-text-2);
}

.{prefix}-table tr:last-child td {
  border-bottom: none;
}

.{prefix}-table tr:hover td {
  background: var(--{prefix}-surface-hover);
}

/* Striped variant */
.{prefix}-table.{prefix}-table--striped tr:nth-child(even) td {
  background: var(--{prefix}-bg-subtle);
}

/* Numeric column alignment */
.{prefix}-table td.{prefix}-num,
.{prefix}-table th.{prefix}-num {
  text-align: right;
  font-family: var(--{prefix}-mono);
}
```

---

## 9. Charts & Data Visualisation

- Wrap every chart in a `{prefix}-design-card {prefix}-chart-card`.
- Chart backgrounds must be **transparent** — the card surface provides the background.
- Axis labels use `var(--{prefix}-text-3)` and `font-family: var(--{prefix}-mono)`.
- Grid lines use `var(--{prefix}-border)` at `stroke-opacity: 0.6`.
- Series colors: derive from `--{prefix}-accent` for primary, semantic tokens for states, and custom `--{prefix}-series-N` variables for multi-series charts.

```css
.{prefix}-chart-card {
  padding: 24px 28px;
}

.{prefix}-chart-title {
  font-size: 13px;
  font-weight: 600;
  color: var(--{prefix}-text-3);
  text-transform: uppercase;
  letter-spacing: 0.06em;
  margin-bottom: 16px;
}

/* Recharts / Chart.js overrides */
.{prefix}-chart-card .recharts-cartesian-axis-tick-value,
.{prefix}-chart-card .chartjs-axis-label {
  fill: var(--{prefix}-text-3);
  font-family: var(--{prefix}-mono);
  font-size: 11px;
}

.{prefix}-chart-card .recharts-cartesian-grid-horizontal line,
.{prefix}-chart-card .recharts-cartesian-grid-vertical line {
  stroke: var(--{prefix}-border);
  stroke-opacity: 0.6;
}
```

Define per-project series palette in `:root`:

```css
:root {
  --{prefix}-series-1: var(--{prefix}-accent);
  --{prefix}-series-2: var(--{prefix}-success);
  --{prefix}-series-3: var(--{prefix}-info);
  --{prefix}-series-4: var(--{prefix}-warning);
  --{prefix}-series-5: var(--{prefix}-error);
}
```

---

## 10. Stat / KPI Cards

```html
<div class="{prefix}-design-card {prefix}-stat-card">
  <span class="{prefix}-stat-label">Total Revenue</span>
  <span class="{prefix}-stat-value">$84,200</span>
  <span class="{prefix}-stat-delta {prefix}-positive">+12.4%</span>
</div>
```

```css
.{prefix}-stat-card {
  padding: 20px 24px;
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.{prefix}-stat-label {
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  color: var(--{prefix}-text-4);
}

.{prefix}-stat-value {
  font-size: 28px;
  font-weight: 700;
  letter-spacing: -0.5px;
  color: var(--{prefix}-text);
  font-family: var(--{prefix}-mono);
}

.{prefix}-stat-delta {
  font-size: 12.5px;
  font-weight: 600;
  font-family: var(--{prefix}-mono);
}

.{prefix}-stat-delta.{prefix}-positive { color: var(--{prefix}-success); }
.{prefix}-stat-delta.{prefix}-negative { color: var(--{prefix}-error); }
```

---

## 11. Badges & Status Indicators

```html
<span class="{prefix}-badge {prefix}-badge--success">Active</span>
<span class="{prefix}-badge {prefix}-badge--error">Failed</span>
<span class="{prefix}-badge {prefix}-badge--warning">Pending</span>
<span class="{prefix}-badge {prefix}-badge--info">Draft</span>
```

```css
.{prefix}-badge {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  padding: 3px 8px;
  border-radius: 999px;
  font-size: 11.5px;
  font-weight: 600;
  letter-spacing: 0.03em;
  border: 1px solid transparent;
}

.{prefix}-badge--success {
  background: var(--{prefix}-success-bg);
  color: var(--{prefix}-success);
  border-color: var(--{prefix}-success-border);
}

.{prefix}-badge--error {
  background: var(--{prefix}-error-bg);
  color: var(--{prefix}-error);
  border-color: var(--{prefix}-error-border);
}

.{prefix}-badge--warning {
  background: var(--{prefix}-warning-bg);
  color: var(--{prefix}-warning);
  border-color: var(--{prefix}-warning-border);
}

.{prefix}-badge--info {
  background: var(--{prefix}-info-bg);
  color: var(--{prefix}-info);
  border-color: var(--{prefix}-info-border);
}
```

---

## 12. Toast / Notification

```css
.{prefix}-toast {
  position: fixed;
  bottom: 28px;
  left: 50%;
  transform: translateX(-50%) translateY(20px);
  background: var(--{prefix}-error-bg);
  color: var(--{prefix}-error);
  border: 1px solid var(--{prefix}-error-border);
  padding: 10px 18px;
  border-radius: var(--{prefix}-radius-sm);
  font-size: 13.5px;
  font-weight: 500;
  opacity: 0;
  pointer-events: none;
  z-index: 999;
  box-shadow: var(--{prefix}-shadow-md);
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.{prefix}-toast.{prefix}-show {
  opacity: 1;
  transform: translateX(-50%) translateY(0);
}

/* Success variant */
.{prefix}-toast.{prefix}-toast--success {
  background: var(--{prefix}-success-bg);
  color: var(--{prefix}-success);
  border-color: var(--{prefix}-success-border);
}
```

---

## 13. Theme Toggle

```html
<button class="{prefix}-theme-toggle" aria-label="Toggle theme">
  <svg class="{prefix}-icon-sun"> … </svg>
  <svg class="{prefix}-icon-moon"> … </svg>
  <span>Theme</span>
</button>
```

```css
.{prefix}-theme-toggle {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 7px 14px;
  background: var(--{prefix}-surface);
  border: none;
  border-radius: var(--{prefix}-radius-sm);
  cursor: pointer;
  font-family: var(--{prefix}-font);
  font-size: 13px;
  font-weight: 500;
  color: var(--{prefix}-text-2);
  box-shadow: var(--{prefix}-shadow-sm);
  outline: 3px solid transparent;
  user-select: none;
  transition: background 0.3s ease, color 0.3s ease, outline 0.3s ease;
}

.{prefix}-theme-toggle svg { width: 15px; height: 15px; flex-shrink: 0; }
.{prefix}-theme-toggle:hover { background: var(--{prefix}-surface-hover); color: var(--{prefix}-text); }

[data-theme="light"] .{prefix}-icon-moon  { display: none; }
[data-theme="light"] .{prefix}-icon-sun   { display: block; }
[data-theme="dark"]  .{prefix}-icon-sun   { display: none; }
[data-theme="dark"]  .{prefix}-icon-moon  { display: block; }
```

```js
const toggle = document.querySelector('.{prefix}-theme-toggle');
toggle?.addEventListener('click', () => {
  const html = document.documentElement;
  html.dataset.theme = html.dataset.theme === 'dark' ? 'light' : 'dark';
});
```

---

## 14. Divider & Stats Bar

```css
.{prefix}-divider {
  height: 1px;
  background: var(--{prefix}-border);
  margin: 32px 0;
}

.{prefix}-stats-bar {
  display: flex;
  gap: 16px;
  margin-top: 12px;
  padding: 10px 14px;
  background: var(--{prefix}-surface);
  border-radius: var(--{prefix}-radius-sm);
  box-shadow: var(--{prefix}-shadow-sm);
}

.{prefix}-stat-item { font-size: 12px; color: var(--{prefix}-text-3); }
.{prefix}-stat-item strong {
  color: var(--{prefix}-text-2);
  font-weight: 600;
  font-family: var(--{prefix}-mono);
}
```

---

## 15. Responsive Rules

```css
@media (max-width: 600px) {
  .{prefix}-shell    { padding: 0 16px 60px; }
  .{prefix}-top-header { flex-direction: column; align-items: flex-start; gap: 12px; }
  .{prefix}-design-tab { width: 100%; }
  .{prefix}-design-tab-btn { flex: 1; justify-content: center; }
  .{prefix}-stat-value { font-size: 22px; }
  .{prefix}-table-wrap { font-size: 12.5px; }
}
```

---

## 16. Agent Checklist (run before output)

Before writing final code, verify every item:

- [ ] **Prefix confirmed** — either user-provided or asked for explicitly
- [ ] All CSS tokens declared in `:root` / `[data-theme="light"]` and overridden in `[data-theme="dark"]`
- [ ] **Zero hardcoded color or shadow values** outside the token block
- [ ] All buttons use `{prefix}-design-btn` + modifier classes — no one-off button styles
- [ ] Tabs use sliding pill indicator with JS `movePill()` function
- [ ] Tables are wrapped in `{prefix}-design-card {prefix}-table-wrap`
- [ ] Charts have transparent background; axis and grid use token variables
- [ ] All `outline` states set to `3px solid transparent` by default, with focus/active overrides
- [ ] Dark theme toggle bound and initialised
- [ ] Responsive breakpoint at `600px` applied
- [ ] Semantic HTML used throughout (`<button>`, `<nav>`, `<table>`, `role="tablist"`, etc.)
