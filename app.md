<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>Abel Tools</title>
<style>
    :root {
        --bg: #f4f4f9;
        --bg-glow-1: rgba(0, 122, 255, 0.10);
        --bg-glow-2: rgba(124, 58, 237, 0.08);
        --bg-card: rgba(255, 255, 255, 0.86);
        --bg-solid: #ffffff;
        --hairline: rgba(15, 23, 42, 0.08);
        --text: #0f172a;
        --text-2: #475569;
        --text-3: #64748b;
        --separator: rgba(60, 60, 67, 0.10);
        --tint: #007aff;
        --tint-bg: rgba(0, 122, 255, 0.12);
        --red: #ff3b30;
        --hero-a: #2563eb;
        --hero-b: #7c3aed;
        --hero-c: #db2777;
        --shadow-sm: 0 1px 2px rgba(15, 23, 42, 0.04), 0 4px 16px rgba(15, 23, 42, 0.05);
        --shadow-md: 0 2px 6px rgba(15, 23, 42, 0.05), 0 12px 32px rgba(15, 23, 42, 0.09);
        --skeleton: rgba(120, 120, 128, 0.13);
        --search-bg: rgba(118, 118, 128, 0.10);
        --focus-ring: #007aff;
        --overlay: rgba(15, 23, 42, 0.35);
    }

    [data-theme="dark"] {
        --bg: #060608;
        --bg-glow-1: rgba(10, 132, 255, 0.13);
        --bg-glow-2: rgba(139, 92, 246, 0.10);
        --bg-card: rgba(26, 26, 32, 0.82);
        --bg-solid: #1a1a20;
        --hairline: rgba(255, 255, 255, 0.09);
        --text: #f5f5f7;
        --text-2: #a6a6b0;
        --text-3: #8e8e93;
        --separator: rgba(255, 255, 255, 0.07);
        --tint: #0a84ff;
        --tint-bg: rgba(10, 132, 255, 0.20);
        --red: #ff453a;
        --hero-a: #1d4ed8;
        --hero-b: #6d28d9;
        --hero-c: #be185d;
        --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.35), 0 6px 20px rgba(0, 0, 0, 0.35);
        --shadow-md: 0 2px 8px rgba(0, 0, 0, 0.45), 0 16px 44px rgba(0, 0, 0, 0.5);
        --skeleton: rgba(255, 255, 255, 0.08);
        --search-bg: rgba(118, 118, 128, 0.22);
        --focus-ring: #0a84ff;
        --overlay: rgba(0, 0, 0, 0.55);
    }

    * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }

    html, body {
        background: var(--bg);
        color: var(--text);
        font-family: -apple-system, BlinkMacSystemFont, "SF Pro Text", "Helvetica Neue", Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -webkit-text-size-adjust: 100%;
    }

    body {
        padding: env(safe-area-inset-top) env(safe-area-inset-right) env(safe-area-inset-bottom) env(safe-area-inset-left);
        min-height: 100vh;
        position: relative;
    }

    /* Ambient atmosphere behind everything */
    .atmosphere {
        position: fixed;
        top: 0; right: 0; bottom: 0; left: 0;
        pointer-events: none;
        z-index: 0;
        background:
            radial-gradient(560px 420px at 12% -6%, var(--bg-glow-1), transparent 68%),
            radial-gradient(640px 480px at 95% 12%, var(--bg-glow-2), transparent 70%);
    }

    a, button { cursor: pointer; }

    :focus { outline: none; }
    :focus-visible {
        outline: 2px solid var(--focus-ring);
        outline-offset: 2px;
        border-radius: 10px;
    }

    .container {
        position: relative;
        z-index: 1;
        max-width: 680px;
        margin: 0 auto;
        padding: 12px 18px 56px;
    }

    svg { display: block; }

    /* Shared surface recipe */
    .surface {
        background: var(--bg-card);
        -webkit-backdrop-filter: blur(20px) saturate(1.4);
        backdrop-filter: blur(20px) saturate(1.4);
        border: 0.5px solid var(--hairline);
    }

    /* ---------- Entrance choreography ---------- */
    @media (prefers-reduced-motion: no-preference) {
        .rise {
            opacity: 0;
            transform: translateY(14px);
            animation: rise 0.55s cubic-bezier(0.22, 1, 0.36, 1) forwards;
        }
        @keyframes rise {
            to { opacity: 1; transform: translateY(0); }
        }
        .d1 { animation-delay: 0.05s; }
        .d2 { animation-delay: 0.12s; }
        .d3 { animation-delay: 0.19s; }
        .d4 { animation-delay: 0.26s; }
        .d5 { animation-delay: 0.33s; }
    }

    /* ---------- Today-style header ---------- */
    .eyebrow {
        display: flex;
        align-items: center;
        gap: 7px;
        font-size: 11.5px;
        font-weight: 700;
        letter-spacing: 0.09em;
        text-transform: uppercase;
        color: var(--text-3);
        margin-top: 16px;
    }
    .eyebrow::before {
        content: "";
        width: 6px;
        height: 6px;
        border-radius: 50%;
        background: linear-gradient(135deg, var(--hero-a), var(--hero-b));
    }

    .header-row {
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 12px;
        margin-top: 3px;
    }

    .large-title {
        font-size: 40px;
        font-weight: 800;
        letter-spacing: -0.025em;
        line-height: 1.08;
        background: linear-gradient(180deg, var(--text) 55%, color-mix(in srgb, var(--text) 62%, transparent));
        -webkit-background-clip: text;
        background-clip: text;
        -webkit-text-fill-color: transparent;
    }

    .header-meta {
        display: flex;
        align-items: center;
        gap: 9px;
        margin-top: 8px;
    }

    .version-pill {
        font-size: 12px;
        font-weight: 700;
        color: var(--tint);
        background: var(--tint-bg);
        border: 0.5px solid color-mix(in srgb, var(--tint) 25%, transparent);
        border-radius: 999px;
        padding: 4px 11px;
    }

    .subtitle { font-size: 13px; color: var(--text-2); }

    .theme-btn {
        width: 44px;
        height: 44px;
        border-radius: 50%;
        color: var(--text);
        box-shadow: var(--shadow-sm);
        display: flex;
        align-items: center;
        justify-content: center;
        flex-shrink: 0;
        transition: transform 0.2s cubic-bezier(0.22, 1, 0.36, 1), background-color 0.2s ease;
    }
    .theme-btn:active { transform: scale(0.88); }

    /* ---------- Announcement banner ---------- */
    .announce {
        display: none;
        align-items: flex-start;
        gap: 10px;
        border-radius: 15px;
        box-shadow: var(--shadow-sm);
        padding: 12px 8px 12px 14px;
        margin-top: 16px;
    }
    .announce.show { display: flex; }
    .announce > svg { flex-shrink: 0; color: var(--tint); margin-top: 1px; }
    .announce-text { flex: 1; font-size: 13.5px; line-height: 1.5; color: var(--text-2); }
    .announce-close {
        border: none;
        background: none;
        color: var(--text-3);
        width: 32px;
        height: 32px;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-shrink: 0;
        border-radius: 50%;
        transition: background-color 0.2s ease;
    }
    .announce-close:active { background: var(--search-bg); }

    /* ---------- Featured hero card (signature) ---------- */
    .hero {
        position: relative;
        margin: 18px 0 24px;
        border-radius: 24px;
        padding: 22px 22px 20px;
        color: #fff;
        background:
            radial-gradient(120% 160% at 8% 0%, var(--hero-a), transparent 60%),
            radial-gradient(130% 170% at 100% 20%, var(--hero-c), transparent 55%),
            linear-gradient(140deg, var(--hero-a), var(--hero-b) 55%, var(--hero-c));
        box-shadow:
            0 2px 8px rgba(37, 99, 235, 0.22),
            0 18px 44px rgba(109, 40, 217, 0.28),
            inset 0 1px 0 rgba(255, 255, 255, 0.28);
        overflow: hidden;
    }

    /* Ghost version numeral — the card's signature */
    .hero-ghost {
        position: absolute;
        right: -6px;
        bottom: -34px;
        font-size: 148px;
        font-weight: 800;
        letter-spacing: -0.05em;
        line-height: 1;
        color: rgba(255, 255, 255, 0.13);
        pointer-events: none;
        -webkit-user-select: none;
        user-select: none;
    }

    .hero::before {
        content: "";
        position: absolute;
        top: -70%;
        left: 18%;
        width: 46%;
        height: 240%;
        background: linear-gradient(105deg, transparent, rgba(255, 255, 255, 0.16), transparent);
        transform: rotate(22deg);
        pointer-events: none;
    }

    .hero-eyebrow {
        font-size: 11px;
        font-weight: 700;
        letter-spacing: 0.12em;
        text-transform: uppercase;
        opacity: 0.78;
    }

    .hero-title {
        font-size: 25px;
        font-weight: 800;
        letter-spacing: -0.02em;
        margin-top: 5px;
        text-shadow: 0 1px 2px rgba(0, 0, 0, 0.12);
    }

    .hero-list {
        list-style: none;
        margin-top: 13px;
        display: flex;
        flex-direction: column;
        gap: 8px;
        position: relative;
    }

    .hero-list li {
        display: flex;
        gap: 9px;
        align-items: flex-start;
        font-size: 14px;
        line-height: 1.45;
        opacity: 0.96;
    }

    .hero-list li svg { flex-shrink: 0; margin-top: 2px; opacity: 0.9; }

    .hero-note { font-size: 12.5px; opacity: 0.75; margin-top: 13px; position: relative; }

    /* ---------- Search ---------- */
    .search-wrap { position: relative; margin: 0 0 13px; }

    .search-icon {
        position: absolute;
        left: 12px;
        top: 50%;
        transform: translateY(-50%);
        color: var(--text-3);
        pointer-events: none;
    }

    .search-input {
        width: 100%;
        border: 0.5px solid transparent;
        background: var(--search-bg);
        color: var(--text);
        border-radius: 13px;
        padding: 12px 42px 12px 38px;
        font-size: 16px;
        font-family: inherit;
        -webkit-appearance: none;
        transition: border-color 0.2s ease, box-shadow 0.2s ease, background-color 0.2s ease;
    }
    .search-input::placeholder { color: var(--text-3); }
    .search-input::-webkit-search-cancel-button { display: none; }
    .search-input:focus {
        border-color: color-mix(in srgb, var(--tint) 55%, transparent);
        box-shadow: 0 0 0 3.5px color-mix(in srgb, var(--tint) 16%, transparent);
        background: var(--bg-solid);
    }

    .search-clear {
        position: absolute;
        right: 5px;
        top: 50%;
        transform: translateY(-50%);
        width: 36px;
        height: 36px;
        border: none;
        background: none;
        color: var(--text-3);
        display: none;
        align-items: center;
        justify-content: center;
    }

    /* ---------- Category chips ---------- */
    .chips {
        display: flex;
        gap: 8px;
        overflow-x: auto;
        -webkit-overflow-scrolling: touch;
        padding: 2px 2px 12px;
        scrollbar-width: none;
    }
    .chips::-webkit-scrollbar { display: none; }

    .chip {
        flex-shrink: 0;
        font-family: inherit;
        font-size: 13px;
        font-weight: 600;
        min-height: 34px;
        padding: 0 15px;
        border-radius: 999px;
        color: var(--text-2);
        box-shadow: var(--shadow-sm);
        transition: background-color 0.2s ease, color 0.2s ease, transform 0.15s ease;
    }
    .chip:active { transform: scale(0.94); }
    .chip.active {
        background: var(--tint);
        border-color: transparent;
        color: #fff;
        box-shadow: 0 4px 14px color-mix(in srgb, var(--tint) 40%, transparent);
    }

    /* ---------- Section header ---------- */
    .section-head {
        display: flex;
        align-items: baseline;
        justify-content: space-between;
        margin: 14px 2px 11px;
    }

    .section-title { font-size: 21px; font-weight: 800; letter-spacing: -0.02em; }
    .section-tools { display: flex; align-items: center; gap: 10px; }
    .sort-btn {
        border: none;
        background: none;
        font-family: inherit;
        font-size: 12.5px;
        font-weight: 700;
        color: var(--tint);
        min-height: 32px;
        padding: 0 4px;
    }
    .section-count { font-size: 12px; font-weight: 600; color: var(--text-3); font-variant-numeric: tabular-nums; }

    /* ---------- Inset grouped list ---------- */
    .list {
        border-radius: 20px;
        box-shadow: var(--shadow-md);
        overflow: hidden;
    }

    .row {
        display: flex;
        align-items: center;
        gap: 14px;
        padding: 14px 16px;
        position: relative;
        cursor: pointer;
        transition: background-color 0.18s ease;
    }
    .row:active { background: var(--search-bg); }
    .row + .row::before {
        content: "";
        position: absolute;
        top: 0;
        left: 82px;
        right: 0;
        height: 0.5px;
        background: var(--separator);
    }
    .row.eol .row-icon, .row.eol .row-name { opacity: 0.5; }
    .row.eol .row-icon { filter: saturate(0.3); -webkit-filter: saturate(0.3); }

    .row-icon {
        width: 52px;
        height: 52px;
        border-radius: 13px;
        display: flex;
        align-items: center;
        justify-content: center;
        color: #fff;
        flex-shrink: 0;
        position: relative;
        box-shadow:
            0 4px 10px rgba(15, 23, 42, 0.18),
            inset 0 1px 0 rgba(255, 255, 255, 0.35);
    }
    .row-icon::after {
        content: "";
        position: absolute;
        top: 0; right: 0; bottom: 0; left: 0;
        border-radius: inherit;
        background: linear-gradient(180deg, rgba(255, 255, 255, 0.22), transparent 52%);
        pointer-events: none;
    }

    .row-info { flex: 1; min-width: 0; }

    .row-name {
        font-size: 15px;
        font-weight: 650;
        letter-spacing: -0.01em;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }

    .row-desc {
        font-size: 12.5px;
        color: var(--text-2);
        line-height: 1.4;
        margin-top: 2.5px;
        display: -webkit-box;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
        overflow: hidden;
    }

    .row-cat {
        font-size: 10.5px;
        font-weight: 700;
        letter-spacing: 0.08em;
        text-transform: uppercase;
        color: var(--text-3);
        margin-top: 4.5px;
    }

    .badge-new {
        display: inline-block;
        vertical-align: 2px;
        margin-left: 7px;
        font-size: 9px;
        font-weight: 800;
        letter-spacing: 0.09em;
        color: #fff;
        background: linear-gradient(135deg, #ff375f, #ff9f0a);
        border-radius: 5px;
        padding: 2.5px 5.5px;
        box-shadow: 0 2px 6px rgba(255, 55, 95, 0.35);
    }

    /* ---------- Action buttons ---------- */
    .btn {
        flex-shrink: 0;
        border: none;
        font-family: inherit;
        font-size: 13px;
        font-weight: 700;
        letter-spacing: 0.02em;
        border-radius: 999px;
        min-width: 78px;
        min-height: 32px;
        padding: 7px 16px;
        text-align: center;
        text-decoration: none;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        transition: transform 0.18s cubic-bezier(0.22, 1, 0.36, 1), opacity 0.18s ease;
    }
    a.btn:active { transform: scale(0.92); opacity: 0.75; }

    .btn-get { background: var(--tint-bg); color: var(--tint); }
    .btn-update {
        background: var(--tint);
        color: #fff;
        box-shadow: 0 4px 12px color-mix(in srgb, var(--tint) 38%, transparent);
    }
    .btn-installed { background: none; color: var(--text-3); border: 1.5px solid var(--separator); cursor: default; }
    .btn-eol { background: none; color: var(--red); border: 1.5px solid currentColor; opacity: 0.75; cursor: default; }

    /* ---------- Skeleton loading ---------- */
    .skeleton-row { display: flex; align-items: center; gap: 14px; padding: 14px 16px; }
    .sk { background: var(--skeleton); border-radius: 8px; }
    .sk-icon { width: 52px; height: 52px; border-radius: 13px; flex-shrink: 0; }
    .sk-lines { flex: 1; display: flex; flex-direction: column; gap: 7px; }
    .sk-line-1 { height: 13px; width: 55%; }
    .sk-line-2 { height: 10px; width: 85%; }
    .sk-btn { width: 78px; height: 32px; border-radius: 999px; flex-shrink: 0; }

    @media (prefers-reduced-motion: no-preference) {
        .sk { animation: pulse 1.4s ease-in-out infinite; }
        @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.4; } }
    }

    /* ---------- Detail sheet ---------- */
    .sheet-overlay {
        position: fixed;
        top: 0; right: 0; bottom: 0; left: 0;
        background: var(--overlay);
        -webkit-backdrop-filter: blur(8px);
        backdrop-filter: blur(8px);
        z-index: 50;
        opacity: 0;
        pointer-events: none;
        transition: opacity 0.28s ease;
    }
    .sheet-overlay.open { opacity: 1; pointer-events: auto; }

    .sheet {
        position: fixed;
        left: 0; right: 0; bottom: 0;
        z-index: 51;
        max-width: 680px;
        margin: 0 auto;
        background: var(--bg-solid);
        border: 0.5px solid var(--hairline);
        border-bottom: none;
        border-radius: 26px 26px 0 0;
        padding: 14px 22px calc(26px + env(safe-area-inset-bottom));
        transform: translateY(105%);
        transition: transform 0.38s cubic-bezier(0.32, 0.72, 0.24, 1);
        box-shadow: 0 -12px 60px rgba(0, 0, 0, 0.3);
    }
    .sheet.open { transform: translateY(0); }

    @media (prefers-reduced-motion: reduce) {
        .sheet, .sheet-overlay { transition: none; }
    }

    .sheet-grabber { width: 38px; height: 5px; border-radius: 3px; background: var(--separator); margin: 0 auto 18px; }
    .sheet-close {
        position: absolute;
        top: 16px; right: 16px;
        width: 32px; height: 32px;
        border: none;
        border-radius: 50%;
        background: var(--search-bg);
        color: var(--text-3);
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .sheet-head { display: flex; gap: 16px; align-items: center; }
    .sheet-icon {
        width: 76px; height: 76px;
        border-radius: 18px;
        display: flex;
        align-items: center;
        justify-content: center;
        color: #fff;
        flex-shrink: 0;
        position: relative;
        box-shadow:
            0 8px 22px rgba(15, 23, 42, 0.25),
            inset 0 1px 0 rgba(255, 255, 255, 0.35);
    }
    .sheet-icon::after {
        content: "";
        position: absolute;
        top: 0; right: 0; bottom: 0; left: 0;
        border-radius: inherit;
        background: linear-gradient(180deg, rgba(255, 255, 255, 0.22), transparent 52%);
        pointer-events: none;
    }
    .sheet-name { font-size: 20px; font-weight: 800; letter-spacing: -0.02em; }
    .sheet-cat { font-size: 11px; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase; color: var(--text-3); margin-top: 4px; }
    .sheet-desc { font-size: 14.5px; line-height: 1.6; color: var(--text-2); margin-top: 15px; }
    .sheet-action { margin-top: 20px; }
    .sheet-action .btn { width: 100%; min-height: 48px; font-size: 15px; border-radius: 15px; }

    /* ---------- Confirm alert ---------- */
    .alert-overlay {
        position: fixed;
        top: 0; right: 0; bottom: 0; left: 0;
        background: var(--overlay);
        -webkit-backdrop-filter: blur(6px);
        backdrop-filter: blur(6px);
        z-index: 60;
        opacity: 0;
        pointer-events: none;
        transition: opacity 0.22s ease;
    }
    .alert-overlay.open { opacity: 1; pointer-events: auto; }

    .alert {
        position: fixed;
        top: 50%; left: 50%;
        z-index: 61;
        width: 280px;
        background: var(--bg-solid);
        border: 0.5px solid var(--hairline);
        border-radius: 16px;
        box-shadow: var(--shadow-md);
        text-align: center;
        overflow: hidden;
        opacity: 0;
        pointer-events: none;
        transform: translate(-50%, -50%) scale(1.08);
        transition: opacity 0.22s ease, transform 0.22s cubic-bezier(0.22, 1, 0.36, 1);
    }
    .alert.open { opacity: 1; pointer-events: auto; transform: translate(-50%, -50%) scale(1); }

    @media (prefers-reduced-motion: reduce) {
        .alert, .alert-overlay { transition: none; }
    }

    .alert-title { font-size: 16px; font-weight: 700; padding: 19px 18px 5px; letter-spacing: -0.01em; }
    .alert-msg { font-size: 13px; color: var(--text-2); line-height: 1.45; padding: 0 18px 17px; }
    .alert-buttons { display: flex; border-top: 0.5px solid var(--separator); }
    .alert-btn {
        flex: 1;
        border: none;
        background: none;
        font-family: inherit;
        font-size: 16px;
        font-weight: 500;
        color: var(--tint);
        min-height: 46px;
        display: flex;
        align-items: center;
        justify-content: center;
        text-decoration: none;
        transition: background-color 0.15s ease;
    }
    .alert-btn:active { background: var(--search-bg); }
    .alert-btn + .alert-btn { border-left: 0.5px solid var(--separator); }
    .alert-btn-primary { font-weight: 700; }

    /* ---------- Header actions ---------- */
    .header-actions { display: flex; gap: 8px; flex-shrink: 0; }

    /* ---------- Empty / footer ---------- */
    .empty {
        display: none;
        text-align: center;
        color: var(--text-2);
        padding: 44px 20px;
        font-size: 14px;
        line-height: 1.6;
    }
    .empty strong { color: var(--text); }

    .footer {
        text-align: center;
        font-size: 11.5px;
        color: var(--text-3);
        margin-top: 30px;
        line-height: 1.7;
    }
</style>
</head>
<body>
<div class="atmosphere" aria-hidden="true"></div>
<div class="container">

    <p class="eyebrow rise" id="dateEyebrow"></p>
    <div class="header-row rise">
        <h1 class="large-title">Abel Tools</h1>
        <div class="header-actions">
            <button class="theme-btn surface" id="aboutBtn" aria-label="About Abel Tools">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" aria-hidden="true"><circle cx="12" cy="12" r="9"/><line x1="12" y1="11" x2="12" y2="16"/><line x1="12" y1="8" x2="12.01" y2="8"/></svg>
            </button>
            <button class="theme-btn surface" id="themeBtn" aria-label="Toggle dark mode">
                <svg id="themeIcon" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"></svg>
            </button>
        </div>
    </div>
    <div class="header-meta rise d1">
        <span class="version-pill" id="versionPill">v&hellip;</span>
        <span class="subtitle">Shortcut installer for iPad</span>
    </div>

    <div class="announce surface" id="announce" role="status">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" aria-hidden="true"><circle cx="12" cy="12" r="9"/><line x1="12" y1="11" x2="12" y2="16"/><line x1="12" y1="8" x2="12.01" y2="8"/></svg>
        <p class="announce-text" id="announceText"></p>
        <button class="announce-close" id="announceClose" aria-label="Dismiss announcement">
            <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" aria-hidden="true"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
        </button>
    </div>

    <section class="hero rise d2" aria-labelledby="heroTitle">
        <span class="hero-ghost" id="heroGhost" aria-hidden="true"></span>
        <p class="hero-eyebrow">What&rsquo;s new</p>
        <h2 class="hero-title" id="heroTitle">Latest update</h2>
        <ul class="hero-list" id="heroList">
            <li><span>Loading changelog&hellip;</span></li>
        </ul>
        <p class="hero-note">Everything installs as a normal Apple Shortcut.</p>
    </section>

    <div class="search-wrap rise d3">
        <span class="search-icon">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
        </span>
        <input class="search-input" id="searchInput" type="search" placeholder="Search shortcuts" aria-label="Search shortcuts" autocomplete="off" autocorrect="off" autocapitalize="off">
        <button class="search-clear" id="searchClear" aria-label="Clear search">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" aria-hidden="true"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
        </button>
    </div>

    <div class="chips rise d4" id="chips" role="tablist" aria-label="Categories"></div>

    <div class="section-head rise d4">
        <h2 class="section-title">Shortcuts</h2>
        <span class="section-tools">
            <button class="sort-btn" id="sortBtn" aria-label="Change sort order">Sort: Featured</button>
            <span class="section-count" id="sectionCount"></span>
        </span>
    </div>

    <div class="list surface rise d5" id="list">
        <div class="skeleton-row"><div class="sk sk-icon"></div><div class="sk-lines"><div class="sk sk-line-1"></div><div class="sk sk-line-2"></div></div><div class="sk sk-btn"></div></div>
        <div class="skeleton-row"><div class="sk sk-icon"></div><div class="sk-lines"><div class="sk sk-line-1"></div><div class="sk sk-line-2"></div></div><div class="sk sk-btn"></div></div>
        <div class="skeleton-row"><div class="sk sk-icon"></div><div class="sk-lines"><div class="sk sk-line-1"></div><div class="sk sk-line-2"></div></div><div class="sk sk-btn"></div></div>
        <div class="skeleton-row"><div class="sk sk-icon"></div><div class="sk-lines"><div class="sk sk-line-1"></div><div class="sk sk-line-2"></div></div><div class="sk sk-btn"></div></div>
    </div>
    <div class="empty" id="empty"><strong>No results</strong><br>Try a different search or category.</div>

    <p class="footer">
        Abel Tools Installer &middot; Tap GET to install through the installer engine.<br>
        Shortcuts remain normal Apple Shortcuts on your device.
    </p>
</div>

<div class="sheet-overlay" id="sheetOverlay"></div>
<div class="sheet" id="sheet" role="dialog" aria-modal="true" aria-labelledby="sheetName">
    <div class="sheet-grabber"></div>
    <button class="sheet-close" id="sheetClose" aria-label="Close">
        <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" aria-hidden="true"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
    </button>
    <div class="sheet-head">
        <div class="sheet-icon" id="sheetIcon"></div>
        <div>
            <div class="sheet-name" id="sheetName"></div>
            <div class="sheet-cat" id="sheetCat"></div>
        </div>
    </div>
    <p class="sheet-desc" id="sheetDesc"></p>
    <div class="sheet-action" id="sheetAction"></div>
</div>

<div class="sheet" id="aboutSheet" role="dialog" aria-modal="true" aria-labelledby="aboutName">
    <div class="sheet-grabber"></div>
    <button class="sheet-close" id="aboutClose" aria-label="Close">
        <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" aria-hidden="true"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
    </button>
    <div class="sheet-head">
        <div class="sheet-icon" style="background: linear-gradient(140deg, #2563eb, #7c3aed 55%, #db2777);">
            <svg width="36" height="36" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.8-3.8a6 6 0 0 1-8 8l-6.9 6.9a2.1 2.1 0 0 1-3-3L10.7 10a6 6 0 0 1 8-8l-4 4Z"/></svg>
        </div>
        <div>
            <div class="sheet-name" id="aboutName">Abel Tools</div>
            <div class="sheet-cat" id="aboutVersion">Installer</div>
        </div>
    </div>
    <p class="sheet-desc">
        Abel Tools is a collection of Apple Shortcuts for iPad, made by Abel.
        This installer keeps everything in one place: browse the catalog, install
        shortcuts with one tap, and get updates as soon as they ship. Every tool
        installs as a normal Apple Shortcut on your device.
    </p>
</div>

<div class="alert-overlay" id="alertOverlay"></div>
<div class="alert" id="alert" role="alertdialog" aria-modal="true" aria-labelledby="alertTitle">
    <p class="alert-title" id="alertTitle">Do you want to continue?</p>
    <p class="alert-msg" id="alertMsg"></p>
    <div class="alert-buttons">
        <button class="alert-btn" id="alertCancel">Cancel</button>
        <a class="alert-btn alert-btn-primary" id="alertContinue" href="#">Continue</a>
    </div>
</div>

<script>
(function () {
    'use strict';

    /* ================= Configuration ================= */

    var RAW_BASE = 'https://raw.githubusercontent.com/therealabela/abel_tools_datarepo/refs/heads/main/';
    var API_BASE = 'https://achenkunju.com/api/';
    var params = new URLSearchParams(location.search);
    var SELF_NAME = params.get('self') || 'Abel Tools Installer';

    /* ================= Icon set (stroke SVG, 24x24) ================= */

    var ICONS = {
        split: '<rect x="3" y="4" width="7" height="16" rx="1.5"/><rect x="14" y="4" width="7" height="16" rx="1.5"/>',
        layers: '<path d="M12 2 2 7l10 5 10-5-10-5z"/><path d="m2 12 10 5 10-5"/><path d="m2 17 10 5 10-5"/>',
        batteryBolt: '<rect x="2" y="7" width="16" height="10" rx="2"/><line x1="21" y1="10.5" x2="21" y2="13.5"/><path d="m11 9-2.5 3h4L10 15"/>',
        battery: '<rect x="2" y="7" width="16" height="10" rx="2"/><line x1="21" y1="10.5" x2="21" y2="13.5"/><line x1="6" y1="10.5" x2="6" y2="13.5"/>',
        scissors: '<circle cx="6" cy="6" r="2.6"/><circle cx="6" cy="18" r="2.6"/><line x1="20" y1="4" x2="8.1" y2="15.9"/><line x1="14.5" y1="14.5" x2="20" y2="20"/><line x1="8.1" y1="8.1" x2="12" y2="12"/>',
        image: '<rect x="3" y="3" width="18" height="18" rx="2.5"/><circle cx="8.5" cy="8.5" r="1.5"/><path d="m21 15-5-5L5 21"/>',
        leaf: '<path d="M11 20A7 7 0 0 1 9.8 6.1C15.5 5 17 4.5 19 2c1 2 2 4.2 2 8 0 5.5-4.8 10-10 10Z"/><path d="M2 21c0-3 1.9-5.4 5.1-6C9.5 14.5 12 13 13 12"/>',
        sparkle: '<path d="M12 2.5 14 9l6.5 2L14 13.5 12 20l-2-6.5L3.5 11 10 9Z"/>',
        cube: '<path d="M21 8a2 2 0 0 0-1-1.7l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.7l7 4a2 2 0 0 0 2 0l7-4a2 2 0 0 0 1-1.7Z"/><path d="m3.3 7 8.7 5 8.7-5"/><line x1="12" y1="22" x2="12" y2="12"/>',
        tablet: '<rect x="4" y="2" width="16" height="20" rx="2.5"/><line x1="10.5" y1="18.5" x2="13.5" y2="18.5"/>',
        broom: '<path d="m13 11 8-8"/><path d="M13 11 5.5 13.6a2 2 0 0 0-1.3 1.5L3 21l5.9-1.2a2 2 0 0 0 1.5-1.3L13 11Z"/><path d="m6.5 14.5 3 3"/>',
        terminal: '<polyline points="4 17 10 11 4 5"/><line x1="12" y1="19" x2="20" y2="19"/>',
        archive: '<rect x="2" y="3" width="20" height="5" rx="1"/><path d="M4 8v11a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8"/><line x1="10" y1="12" x2="14" y2="12"/>',
        wrench: '<path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.8-3.8a6 6 0 0 1-8 8l-6.9 6.9a2.1 2.1 0 0 1-3-3L10.7 10a6 6 0 0 1 8-8l-4 4Z"/>',
        sun: '<circle cx="12" cy="12" r="4"/><line x1="12" y1="2" x2="12" y2="4"/><line x1="12" y1="20" x2="12" y2="22"/><line x1="4.9" y1="4.9" x2="6.3" y2="6.3"/><line x1="17.7" y1="17.7" x2="19.1" y2="19.1"/><line x1="2" y1="12" x2="4" y2="12"/><line x1="20" y1="12" x2="22" y2="12"/><line x1="4.9" y1="19.1" x2="6.3" y2="17.7"/><line x1="17.7" y1="6.3" x2="19.1" y2="4.9"/>',
        moon: '<path d="M21 12.8A9 9 0 1 1 11.2 3a7 7 0 0 0 9.8 9.8Z"/>',
        check: '<polyline points="20 6 9 17 4 12"/>'
    };

    function iconSvg(name, size) {
        return '<svg width="' + size + '" height="' + size + '" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">' + ICONS[name] + '</svg>';
    }

    /* ================= Catalog metadata =================
       shortcutslist.md decides WHICH shortcuts exist; this map decorates
       known names. Unknown names get sensible defaults. */

    var META = {
        'quickscreen': { icon: 'split', gradient: 'linear-gradient(135deg,#0a84ff,#5e5ce6)', category: 'Productivity', desc: 'Split screen your apps and resize windows with ease. Perfect for iPad multitasking.', link: 'https://www.icloud.com/shortcuts/419b76c98a474c35b11c8497529b3d36' },
        'anythingbutglass': { icon: 'layers', gradient: 'linear-gradient(135deg,#5e5ce6,#bf5af2)', category: 'Customization', desc: 'Removes the Liquid Glass look from iOS 26 for a cleaner, classic appearance.', link: 'https://www.icloud.com/shortcuts/66d53e172121493e9d834df6a5062f25' },
        'savemybattery v2.1': { icon: 'batteryBolt', gradient: 'linear-gradient(135deg,#30d158,#0a84ff)', category: 'Battery', desc: 'Optimize battery life in one tap: low power mode, reduced transparency and motion.', link: 'https://www.icloud.com/shortcuts/32e766396219425e8d29eaf0e4c4a161' },
        'savemybattery v1': { icon: 'battery', gradient: 'linear-gradient(135deg,#8e8e93,#48484a)', category: 'Battery', desc: 'The original SaveMyBattery. Kept for older setups.', link: 'https://www.icloud.com/shortcuts/594fff3adae8400faf5a903167f0854d' },
        'coolbgremover': { icon: 'scissors', gradient: 'linear-gradient(135deg,#ff9f0a,#ff375f)', category: 'Images', desc: 'Remove backgrounds from images instantly.', link: 'https://www.icloud.com/shortcuts/c9d90103e0eb4a56bcde227b8006c9b7' },
        'coolimageeditor': { icon: 'image', gradient: 'linear-gradient(135deg,#bf5af2,#ff375f)', category: 'Images', desc: 'Quick image editing: crop, convert, resize and more.', link: 'https://www.icloud.com/shortcuts/b9d34799af7248e084e08671549c297d' },
        'leaf blower w/ google search': { icon: 'leaf', gradient: 'linear-gradient(135deg,#30d158,#64d2ff)', category: 'Voice', desc: 'A very dumb Siri alternative. Search the web using just your voice via Google Search.', link: 'https://www.icloud.com/shortcuts/a52c67fa1d68460abee42b63831bbae5' },
        'leaf blower w/ google gemini': { icon: 'sparkle', gradient: 'linear-gradient(135deg,#64d2ff,#5e5ce6)', category: 'Voice', desc: 'Leaf Blower powered by Google Gemini for smarter voice answers.', link: 'https://www.icloud.com/shortcuts/9a3c7bc343cb474e94b8ac83828f494b' },
        'editable materials': { icon: 'cube', gradient: 'linear-gradient(135deg,#ff9f0a,#ffd60a)', category: 'Productivity', desc: 'Edit files in the Materials section of Google Classroom.', link: 'https://www.icloud.com/shortcuts/d5e5fe1db65745a891e6e81038ed238f' },
        'editable matrials': { icon: 'cube', gradient: 'linear-gradient(135deg,#ff9f0a,#ffd60a)', category: 'Productivity', desc: 'Edit files in the Materials section of Google Classroom.', link: 'https://www.icloud.com/shortcuts/d5e5fe1db65745a891e6e81038ed238f' },
        'deviceinfo': { icon: 'tablet', gradient: 'linear-gradient(135deg,#48484a,#8e8e93)', category: 'Utilities', desc: 'See detailed information about your device at a glance.', link: 'https://www.icloud.com/shortcuts/ca35bc3d75814583af3461518c8badf8' },
        'moo cleanup tool': { icon: 'broom', gradient: 'linear-gradient(135deg,#ff375f,#ff9f0a)', category: 'Utilities', desc: 'Clean up leftovers and junk. New in version 44!', link: 'https://www.icloud.com/shortcuts/fa85f39337b049d4b175ca978d9a9966' },
        '[api] notarobot api v1.1': { icon: 'terminal', gradient: 'linear-gradient(135deg,#0a84ff,#64d2ff)', category: 'Developer', desc: 'NotARobot verification API for shortcut developers.', link: 'https://www.icloud.com/shortcuts/642810ae87534d64873d19a5498948f4' },
        'kool menu': { icon: 'archive', gradient: 'linear-gradient(135deg,#636366,#3a3a3c)', category: 'Legacy', desc: 'The original Kool Menu. No longer maintained.', link: 'https://www.icloud.com/shortcuts/9c0322bfe63647fb9782128d388325f7' }
    };

    var DEFAULT_META = { icon: 'wrench', gradient: 'linear-gradient(135deg,#8e8e93,#3a3a3c)', category: 'Other', desc: 'An Abel Tools shortcut.' };

    /* ================= State ================= */

    function normalize(name) { return name.replace(/\[EOL\]/gi, '').trim().toLowerCase(); }
    function parseNameList(value) {
        if (!value) return [];
        return value.split(',').map(normalize).filter(Boolean);
    }

    var installed = parseNameList(params.get('installed'));
    var updates = parseNameList(params.get('updates'));
    var catalog = [];
    var newNames = [];
    var activeCategory = 'All';
    var searchQuery = '';
    var sortMode = 0; // 0 = Featured, 1 = A-Z, 2 = Category
    var SORT_LABELS = ['Featured', 'A\u2013Z', 'Category'];

    function statusFor(item) {
        if (item.eol) return 'EOL';
        if (updates.indexOf(item.key) !== -1) return 'UPDATE';
        if (installed.indexOf(item.key) !== -1) return 'INSTALLED';
        return 'GET';
    }

    function deepLink(item) {
        return 'shortcuts://run-shortcut?name=' + encodeURIComponent(SELF_NAME) +
               '&input=text&text=' + encodeURIComponent('install:' + item.name);
    }

    function el(tag, className, text) {
        var node = document.createElement(tag);
        if (className) node.className = className;
        if (text) node.textContent = text;
        return node;
    }

    /* ================= Header date ================= */

    document.getElementById('dateEyebrow').textContent =
        new Date().toLocaleDateString('en-US', { weekday: 'long', month: 'long', day: 'numeric' }).toUpperCase();

    /* ================= Theme ================= */

    var themeBtn = document.getElementById('themeBtn');
    var themeIcon = document.getElementById('themeIcon');

    function applyTheme(theme) {
        if (theme === 'dark') {
            document.documentElement.setAttribute('data-theme', 'dark');
            themeIcon.innerHTML = ICONS.sun;
        } else {
            document.documentElement.removeAttribute('data-theme');
            themeIcon.innerHTML = ICONS.moon;
        }
    }

    function initialTheme() {
        var forced = params.get('theme');
        if (forced === 'dark' || forced === 'light') return forced;
        try {
            var saved = localStorage.getItem('abeltools-theme');
            if (saved === 'dark' || saved === 'light') return saved;
        } catch (e) { /* localStorage may be unavailable in web view */ }
        return window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';
    }

    var currentTheme = initialTheme();
    applyTheme(currentTheme);

    themeBtn.addEventListener('click', function () {
        currentTheme = currentTheme === 'dark' ? 'light' : 'dark';
        applyTheme(currentTheme);
        try { localStorage.setItem('abeltools-theme', currentTheme); } catch (e) {}
    });

    /* ================= Rendering ================= */

    var listEl = document.getElementById('list');
    var emptyEl = document.getElementById('empty');
    var countEl = document.getElementById('sectionCount');
    var chipsEl = document.getElementById('chips');

    function buildChips() {
        var cats = ['All'];
        catalog.forEach(function (item) {
            if (cats.indexOf(item.category) === -1) cats.push(item.category);
        });
        chipsEl.innerHTML = '';
        cats.forEach(function (cat) {
            var chip = el('button', 'chip surface' + (cat === activeCategory ? ' active' : ''), cat);
            chip.setAttribute('role', 'tab');
            chip.setAttribute('aria-selected', cat === activeCategory ? 'true' : 'false');
            chip.addEventListener('click', function () {
                activeCategory = cat;
                buildChips();
                render();
            });
            chipsEl.appendChild(chip);
        });
    }

    function matchesFilters(item) {
        if (activeCategory !== 'All' && item.category !== activeCategory) return false;
        if (searchQuery && item.name.toLowerCase().indexOf(searchQuery) === -1 &&
            item.category.toLowerCase().indexOf(searchQuery) === -1) return false;
        return true;
    }

    function buildButton(item, status) {
        if (status === 'EOL') return el('span', 'btn btn-eol', 'EOL');
        if (status === 'INSTALLED') return el('span', 'btn btn-installed', 'INSTALLED');
        var a = el('a', status === 'UPDATE' ? 'btn btn-update' : 'btn btn-get', status);
        // iCloud links open natively in any web view; deep link is the fallback
        a.href = item.link || deepLink(item);
        a.setAttribute('aria-label', (status === 'UPDATE' ? 'Update ' : 'Get ') + item.name);
        a.addEventListener('click', function (e) {
            e.preventDefault();
            openConfirm(item, a.href);
        });
        return a;
    }

    function sortedCatalog() {
        var items = catalog.filter(matchesFilters);
        if (sortMode === 1) {
            items.sort(function (a, b) { return a.name.localeCompare(b.name); });
        } else if (sortMode === 2) {
            items.sort(function (a, b) {
                return a.category.localeCompare(b.category) || a.name.localeCompare(b.name);
            });
        } else {
            // Featured: NEW shortcuts first, EOL last, otherwise list order
            items.sort(function (a, b) {
                return (b.isNew - a.isNew) || (a.eol - b.eol);
            });
        }
        return items;
    }

    function render() {
        listEl.innerHTML = '';
        var items = sortedCatalog();

        items.forEach(function (item) {
            var status = statusFor(item);
            var row = el('div', 'row' + (item.eol ? ' eol' : ''));
            row.setAttribute('role', 'button');
            row.setAttribute('tabindex', '0');
            row.setAttribute('aria-label', 'View details for ' + item.name);

            var icon = el('div', 'row-icon');
            icon.style.background = item.gradient;
            icon.innerHTML = iconSvg(item.icon, 25);

            var name = el('div', 'row-name', item.name);
            if (item.isNew && !item.eol) name.appendChild(el('span', 'badge-new', 'NEW'));

            var info = el('div', 'row-info');
            info.appendChild(name);
            info.appendChild(el('div', 'row-desc', item.desc));
            info.appendChild(el('div', 'row-cat', item.category));

            row.appendChild(icon);
            row.appendChild(info);
            row.appendChild(buildButton(item, status));

            row.addEventListener('click', function (e) {
                if (e.target.closest('.btn')) return; // GET/UPDATE taps keep their own action
                openSheet(item);
            });
            row.addEventListener('keydown', function (e) {
                if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); openSheet(item); }
            });

            listEl.appendChild(row);
        });

        countEl.textContent = items.length + ' of ' + catalog.length;
        listEl.style.display = items.length === 0 ? 'none' : 'block';
        emptyEl.style.display = items.length === 0 ? 'block' : 'none';
    }

    /* ================= Sort toggle ================= */

    var sortBtn = document.getElementById('sortBtn');
    sortBtn.addEventListener('click', function () {
        sortMode = (sortMode + 1) % SORT_LABELS.length;
        sortBtn.textContent = 'Sort: ' + SORT_LABELS[sortMode];
        render();
    });

    /* ================= Detail sheet ================= */

    var sheet = document.getElementById('sheet');
    var sheetOverlay = document.getElementById('sheetOverlay');

    function openSheet(item) {
        var status = statusFor(item);
        var iconNode = document.getElementById('sheetIcon');
        iconNode.style.background = item.gradient;
        iconNode.innerHTML = iconSvg(item.icon, 36);
        document.getElementById('sheetName').textContent = item.name;
        document.getElementById('sheetCat').textContent =
            item.category + (item.eol ? ' \u00b7 No longer maintained' : '');
        document.getElementById('sheetDesc').textContent = item.desc;

        var action = document.getElementById('sheetAction');
        action.innerHTML = '';
        action.appendChild(buildButton(item, status));

        sheet.classList.add('open');
        sheetOverlay.classList.add('open');
        document.body.style.overflow = 'hidden';
    }

    function closeSheet() {
        sheet.classList.remove('open');
        sheetOverlay.classList.remove('open');
        document.body.style.overflow = '';
    }

    document.getElementById('sheetClose').addEventListener('click', closeSheet);

    /* ================= About sheet ================= */

    var aboutSheet = document.getElementById('aboutSheet');

    function openAbout() {
        aboutSheet.classList.add('open');
        sheetOverlay.classList.add('open');
        document.body.style.overflow = 'hidden';
    }

    function closeAbout() {
        aboutSheet.classList.remove('open');
        sheetOverlay.classList.remove('open');
        document.body.style.overflow = '';
    }

    document.getElementById('aboutBtn').addEventListener('click', openAbout);
    document.getElementById('aboutClose').addEventListener('click', closeAbout);

    sheetOverlay.addEventListener('click', function () { closeSheet(); closeAbout(); });

    /* ================= Confirm alert ================= */

    var alertBox = document.getElementById('alert');
    var alertOverlay = document.getElementById('alertOverlay');
    var alertContinue = document.getElementById('alertContinue');

    function openConfirm(item, href) {
        document.getElementById('alertMsg').textContent =
            '\u201C' + item.name + '\u201D will open in Shortcuts.';
        alertContinue.href = href;
        alertBox.classList.add('open');
        alertOverlay.classList.add('open');
    }

    function closeConfirm() {
        alertBox.classList.remove('open');
        alertOverlay.classList.remove('open');
    }

    document.getElementById('alertCancel').addEventListener('click', closeConfirm);
    alertOverlay.addEventListener('click', closeConfirm);
    alertContinue.addEventListener('click', function () {
        // Let navigation proceed, then tidy up the dialog
        closeConfirm();
        closeSheet();
    });

    document.addEventListener('keydown', function (e) {
        if (e.key !== 'Escape') return;
        if (alertBox.classList.contains('open')) { closeConfirm(); return; }
        if (sheet.classList.contains('open')) closeSheet();
        if (aboutSheet.classList.contains('open')) closeAbout();
    });

    /* ================= Announcement banner ================= */

    function renderAnnouncement(text) {
        text = (text || '').trim();
        if (!text) return;
        try {
            if (localStorage.getItem('abeltools-announce-dismissed') === text) return;
        } catch (e) {}

        document.getElementById('announceText').textContent = text;
        var banner = document.getElementById('announce');
        banner.classList.add('show');
        document.getElementById('announceClose').addEventListener('click', function () {
            banner.classList.remove('show');
            try { localStorage.setItem('abeltools-announce-dismissed', text); } catch (e) {}
        });
    }

    /* ================= Hero (What's New) ================= */

    function renderChangelog(md, version) {
        if (version) {
            document.getElementById('heroTitle').textContent = 'New in version ' + version;
            document.getElementById('heroGhost').textContent = version;
        }
        var listNode = document.getElementById('heroList');
        var items = md.split('\n')
            .map(function (l) { return l.trim(); })
            .filter(function (l) { return /^[-*+]\s+/.test(l); })
            .map(function (l) { return l.replace(/^[-*+]\s+/, ''); });

        listNode.innerHTML = '';
        if (items.length === 0) items = [md.trim() || 'No changelog available.'];
        items.forEach(function (text) {
            var li = document.createElement('li');
            li.innerHTML = iconSvg('check', 15);
            li.appendChild(el('span', null, text));
            listNode.appendChild(li);
        });
    }

    /* ================= Data loading ================= */

    // Fallback snapshot used if GitHub is unreachable (mirrors shortcutslist.md).
    var FALLBACK_LIST = [
        'kool Menu [EOL]', 'Quickscreen', 'AnythingButGlass', 'SaveMyBattery V2.1',
        'SaveMyBattery V1', 'CoolBGRemover', 'CoolImageEditor',
        'leaf blower w/ Google Search', 'leaf blower w/ Google Gemini',
        'Editable Materials', 'DeviceInfo', 'Moo Cleanup Tool', '[API] NotARobot API V1.1'
    ];

    function buildCatalog(lines) {
        catalog = lines
            .map(function (l) { return l.trim(); })
            .filter(Boolean)
            .map(function (rawName) {
                var eol = /\[EOL\]/i.test(rawName);
                var meta = META[normalize(rawName)] || DEFAULT_META;
                var key = normalize(rawName);
                return {
                    name: rawName.replace(/\s*\[EOL\]\s*/i, ' ').trim(),
                    key: key,
                    eol: eol,
                    isNew: newNames.indexOf(key) !== -1,
                    icon: meta.icon,
                    link: meta.link || null,
                    gradient: meta.gradient,
                    category: eol ? 'Legacy' : meta.category,
                    desc: meta.desc
                };
            });
    }

    function fetchText(file) {
        return fetch(RAW_BASE + file, { cache: 'no-store' }).then(function (r) {
            if (!r.ok) throw new Error('HTTP ' + r.status + ' for ' + file);
            return r.text();
        });
    }

    function fetchApi(endpoint) {
        return fetch(API_BASE + endpoint, { cache: 'no-store' }).then(function (r) {
            if (!r.ok) throw new Error('HTTP ' + r.status + ' for ' + endpoint);
            return r.text();
        });
    }

    function init() {
        var versionPromise = fetchApi('newversion').then(function (v) {
            var version = v.trim();
            document.getElementById('versionPill').textContent = 'v' + version;
            document.getElementById('aboutVersion').textContent = 'Installer \u00b7 Version ' + version;
            return version;
        }).catch(function () {
            document.getElementById('versionPill').textContent = 'v?';
            return null;
        });

        Promise.all([
            fetchApi('newchangelog').catch(function () { return ''; }),
            versionPromise
        ]).then(function (results) {
            if (results[0]) renderChangelog(results[0], results[1]);
            else document.getElementById('heroList').innerHTML = '<li><span>Could not load changelog.</span></li>';
        });

        fetchText('announcement.md').then(renderAnnouncement).catch(function () {});

        Promise.all([
            fetchText('shortcutslist.md').then(function (t) { return t.split('\n'); })
                .catch(function () { return FALLBACK_LIST; }),
            fetchApi('newshortcuts').then(function (t) {
                return t.split('\n').map(normalize).filter(Boolean);
            }).catch(function () { return []; })
        ]).then(function (results) {
            newNames = results[1];
            buildCatalog(results[0]);
            buildChips();
            render();
        });
    }

    init();
})();
</script>
</body>
</html>
