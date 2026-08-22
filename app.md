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
        --text-3: #5d6a7d;
        --separator: rgba(60, 60, 67, 0.10);
        --tint: #0071e3;
        --tint-bg: rgba(0, 113, 227, 0.12);
        --tint-text: #0361c2;
        --red: #d70015;
        --hero-a: #2563eb;
        --hero-b: #7c3aed;
        --hero-c: #db2777;
        --shadow-sm: 0 1px 2px rgba(15, 23, 42, 0.04), 0 4px 16px rgba(15, 23, 42, 0.05);
        --shadow-md: 0 2px 6px rgba(15, 23, 42, 0.05), 0 12px 32px rgba(15, 23, 42, 0.09);
        --skeleton: rgba(120, 120, 128, 0.13);
        --search-bg: rgba(118, 118, 128, 0.10);
        --focus-ring: #0071e3;
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
        --tint-text: #64b1ff;
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
        overscroll-behavior-y: none;
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
    a, button, input, [role="button"] { touch-action: manipulation; }

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
        color: var(--text);
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
        color: var(--tint-text);
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

    @media (prefers-reduced-motion: no-preference) {
        .icon-spin { animation: iconSpin 0.35s cubic-bezier(0.22, 1, 0.36, 1); }
        @keyframes iconSpin { from { transform: rotate(-90deg) scale(0.7); opacity: 0; } }
    }

    /* ---------- Collapsing mini header ---------- */
    .mini-header {
        position: fixed;
        top: 0; left: 0; right: 0;
        z-index: 40;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 8px;
        min-height: 46px;
        padding-top: env(safe-area-inset-top);
        background: color-mix(in srgb, var(--bg) 80%, transparent);
        -webkit-backdrop-filter: blur(20px) saturate(1.6);
        backdrop-filter: blur(20px) saturate(1.6);
        border-bottom: 0.5px solid var(--hairline);
        cursor: pointer;
        opacity: 0;
        transform: translateY(-10px);
        pointer-events: none;
        transition: opacity 0.22s ease, transform 0.22s cubic-bezier(0.22, 1, 0.36, 1);
    }
    .mini-header.show { opacity: 1; transform: translateY(0); pointer-events: auto; }
    .mini-title { font-size: 16px; font-weight: 700; letter-spacing: -0.01em; }
    .mini-version {
        font-size: 11px;
        font-weight: 700;
        color: var(--tint-text);
        background: var(--tint-bg);
        border-radius: 999px;
        padding: 2px 8px;
    }
    .mini-version:empty { display: none; }

    @media (prefers-reduced-motion: reduce) {
        .mini-header { transition: none; }
    }

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
        width: 40px;
        height: 40px;
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
        border: 0.5px solid rgba(255, 255, 255, 0.22);
        overflow: hidden;
    }

    /* Fine film grain keeps the big gradients from banding */
    .hero::after, .spotlight::after {
        content: "";
        position: absolute;
        top: 0; right: 0; bottom: 0; left: 0;
        background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='160' height='160'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='2' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
        opacity: 0.055;
        mix-blend-mode: overlay;
        pointer-events: none;
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

    .hero-note { font-size: 12.5px; opacity: 0.82; margin-top: 13px; position: relative; }

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
        right: 4px;
        top: 50%;
        transform: translateY(-50%);
        width: 40px;
        height: 40px;
        border: none;
        background: none;
        color: var(--text-3);
        display: none;
        align-items: center;
        justify-content: center;
    }
    .search-clear.show { display: flex; }

    /* ---------- Category chips ---------- */
    .chips {
        display: flex;
        gap: 8px;
        overflow-x: auto;
        -webkit-overflow-scrolling: touch;
        padding: 2px 2px 12px;
        scrollbar-width: none;
        --fade-l: 0px;
        --fade-r: 0px;
        -webkit-mask-image: linear-gradient(90deg, transparent 0, #000 var(--fade-l), #000 calc(100% - var(--fade-r)), transparent 100%);
        mask-image: linear-gradient(90deg, transparent 0, #000 var(--fade-l), #000 calc(100% - var(--fade-r)), transparent 100%);
    }
    .chips::-webkit-scrollbar { display: none; }

    .chip {
        flex-shrink: 0;
        font-family: inherit;
        font-size: 13px;
        font-weight: 600;
        min-height: 36px;
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

    .section-title { font-size: 22px; font-weight: 800; letter-spacing: -0.02em; }
    .section-tools { display: flex; align-items: center; gap: 10px; }
    .sort-btn {
        border: none;
        background: none;
        font-family: inherit;
        font-size: 12.5px;
        font-weight: 700;
        color: var(--tint-text);
        min-height: 36px;
        padding: 0 4px;
    }
    .section-count { font-size: 12px; font-weight: 600; color: var(--text-3); font-variant-numeric: tabular-nums; }

    /* ---------- Spotlight feature card ---------- */
    .spotlight {
        position: relative;
        border-radius: 24px;
        padding: 18px 18px 20px;
        margin: 4px 0 16px;
        color: #fff;
        overflow: hidden;
        cursor: pointer;
        box-shadow: var(--shadow-md), inset 0 1px 0 rgba(255, 255, 255, 0.28);
        transition: transform 0.2s cubic-bezier(0.22, 1, 0.36, 1);
    }
    .spotlight:active { transform: scale(0.98); }
    .spotlight::before {
        content: "";
        position: absolute;
        top: -70%;
        left: 24%;
        width: 40%;
        height: 240%;
        background: linear-gradient(105deg, transparent, rgba(255, 255, 255, 0.14), transparent);
        transform: rotate(22deg);
        pointer-events: none;
    }
    .spotlight-eyebrow {
        font-size: 11px;
        font-weight: 800;
        letter-spacing: 0.12em;
        text-transform: uppercase;
        opacity: 0.85;
    }
    .spotlight-body {
        display: flex;
        align-items: center;
        gap: 15px;
        margin-top: 13px;
        position: relative;
    }
    .spotlight-icon {
        width: 66px;
        height: 66px;
        border-radius: 16px;
        background: rgba(255, 255, 255, 0.22);
        display: flex;
        align-items: center;
        justify-content: center;
        flex-shrink: 0;
        box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.35);
    }
    .spotlight-info { flex: 1; min-width: 0; }
    .spotlight-name {
        font-size: 20px;
        font-weight: 800;
        letter-spacing: -0.02em;
        text-shadow: 0 1px 2px rgba(0, 0, 0, 0.12);
    }
    .spotlight-desc {
        font-size: 13.5px;
        line-height: 1.45;
        opacity: 0.92;
        margin-top: 3px;
        display: -webkit-box;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
        overflow: hidden;
    }
    .spotlight .btn-get, .spotlight .btn-update { background: #fff; color: #0f172a; box-shadow: 0 4px 12px rgba(0, 0, 0, 0.18); }
    .spotlight .btn-installed { border-color: rgba(255, 255, 255, 0.55); color: rgba(255, 255, 255, 0.9); }

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
        padding: 15px 16px;
        position: relative;
        cursor: pointer;
        transition: background-color 0.18s ease;
    }
    .row:active { background: var(--search-bg); }
    .row + .row::before {
        content: "";
        position: absolute;
        top: 0;
        left: 88px;
        right: 0;
        height: 0.5px;
        background: var(--separator);
    }
    .row.eol .row-icon, .row.eol .row-name { opacity: 0.5; }
    .row.eol .row-icon { filter: saturate(0.3); -webkit-filter: saturate(0.3); }

    .row-icon {
        width: 58px;
        height: 58px;
        border-radius: 14px;
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
        background: linear-gradient(180deg, rgba(255, 255, 255, 0.16), transparent 52%);
        pointer-events: none;
    }

    .row-info { flex: 1; min-width: 0; }

    .row-name {
        font-size: 16px;
        font-weight: 650;
        letter-spacing: -0.01em;
        line-height: 1.25;
        display: -webkit-box;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
        overflow: hidden;
    }

    .row-desc {
        font-size: 13px;
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
        font-size: 10px;
        font-weight: 800;
        letter-spacing: 0.08em;
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

    .btn-get { background: var(--tint-bg); color: var(--tint-text); }
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
    .sk-icon { width: 58px; height: 58px; border-radius: 14px; flex-shrink: 0; }
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
        max-height: 85vh;
        overflow-y: auto;
        overscroll-behavior: contain;
        -webkit-overflow-scrolling: touch;
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
        top: 14px; right: 14px;
        width: 38px; height: 38px;
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
        background: linear-gradient(180deg, rgba(255, 255, 255, 0.16), transparent 52%);
        pointer-events: none;
    }
    .sheet-name { font-size: 20px; font-weight: 800; letter-spacing: -0.02em; }
    .sheet-cat { font-size: 11px; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase; color: var(--text-3); margin-top: 4px; }
    .sheet-desc { font-size: 14.5px; line-height: 1.6; color: var(--text-2); margin-top: 15px; }
    .sheet-action { margin-top: 20px; }

    /* ---------- About sheet extras ---------- */
    .about-heading {
        font-size: 13px;
        font-weight: 700;
        letter-spacing: -0.01em;
        margin-top: 22px;
        padding-top: 18px;
        border-top: 0.5px solid var(--separator);
    }
    .about-bio { margin-top: 7px; font-size: 13.5px; }
    .about-links { display: flex; gap: 8px; margin-top: 14px; }
    .about-link {
        flex: 1;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        gap: 6px;
        font-size: 13px;
        font-weight: 700;
        color: var(--tint-text);
        background: var(--tint-bg);
        border-radius: 11px;
        min-height: 40px;
        padding: 8px 10px;
        text-decoration: none;
        transition: transform 0.18s cubic-bezier(0.22, 1, 0.36, 1), opacity 0.18s ease;
    }
    .about-link:active { transform: scale(0.95); opacity: 0.8; }
    .sheet-copyright {
        font-size: 11px;
        color: var(--text-3);
        text-align: center;
        margin-top: 18px;
        line-height: 1.5;
    }
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
        width: 304px;
        background: var(--bg-card);
        -webkit-backdrop-filter: blur(24px) saturate(1.4);
        backdrop-filter: blur(24px) saturate(1.4);
        border: 0.5px solid var(--hairline);
        border-radius: 24px;
        box-shadow: var(--shadow-md);
        text-align: center;
        padding: 24px 20px 18px;
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

    .alert-icon {
        width: 58px;
        height: 58px;
        border-radius: 14px;
        margin: 0 auto 13px;
        display: flex;
        align-items: center;
        justify-content: center;
        color: #fff;
        position: relative;
        box-shadow:
            0 6px 16px rgba(15, 23, 42, 0.22),
            inset 0 1px 0 rgba(255, 255, 255, 0.35);
    }
    .alert-icon::after {
        content: "";
        position: absolute;
        top: 0; right: 0; bottom: 0; left: 0;
        border-radius: inherit;
        background: linear-gradient(180deg, rgba(255, 255, 255, 0.16), transparent 52%);
        pointer-events: none;
    }
    .alert-title { font-size: 17px; font-weight: 800; letter-spacing: -0.015em; }
    .alert-msg { font-size: 13.5px; color: var(--text-2); line-height: 1.5; margin-top: 6px; }
    .alert-buttons { display: flex; gap: 9px; margin-top: 19px; }
    .alert-btn {
        flex: 1;
        border: none;
        font-family: inherit;
        font-size: 15px;
        font-weight: 700;
        color: var(--text);
        background: var(--search-bg);
        border-radius: 999px;
        min-height: 44px;
        display: flex;
        align-items: center;
        justify-content: center;
        text-decoration: none;
        transition: transform 0.18s cubic-bezier(0.22, 1, 0.36, 1), opacity 0.18s ease;
    }
    .alert-btn:active { transform: scale(0.95); opacity: 0.8; }
    .alert-btn-primary {
        background: var(--tint);
        color: #fff;
        box-shadow: 0 4px 12px color-mix(in srgb, var(--tint) 38%, transparent);
    }

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
    .empty-icon {
        width: 56px;
        height: 56px;
        border-radius: 50%;
        background: var(--search-bg);
        color: var(--text-3);
        display: flex;
        align-items: center;
        justify-content: center;
        margin: 0 auto 14px;
    }
    .empty-clear {
        border: none;
        background: var(--tint-bg);
        color: var(--tint-text);
        font-family: inherit;
        font-size: 13px;
        font-weight: 700;
        border-radius: 999px;
        min-height: 34px;
        padding: 7px 18px;
        margin-top: 14px;
        transition: transform 0.18s cubic-bezier(0.22, 1, 0.36, 1);
    }
    .empty-clear:active { transform: scale(0.94); }

    .footer {
        text-align: center;
        font-size: 11.5px;
        color: var(--text-3);
        margin-top: 30px;
        line-height: 1.7;
    }

    /* ---------- Pointer (iPad trackpad / mouse) hover states ---------- */
    @media (hover: hover) and (pointer: fine) {
        .row:hover { background: var(--search-bg); }
        .chip:hover { color: var(--text); }
        .chip.active:hover { color: #fff; }
        a.btn:hover { transform: translateY(-1px); }
        .btn-get:hover { background: color-mix(in srgb, var(--tint) 20%, transparent); }
        .spotlight .btn-get:hover, .spotlight .btn-update:hover { background: #fff; }
        .theme-btn:hover { box-shadow: var(--shadow-md); }
        .announce-close:hover { background: var(--search-bg); }
        .sheet-close:hover { color: var(--text); }
        .sort-btn:hover, .about-link:hover, .empty-clear:hover, .alert-btn:hover { opacity: 0.8; }
        .spotlight:hover { transform: translateY(-2px); }
    }
</style>
<!-- Shared AbelDeviceID gate (loaded from the canonical origin so it works
     whether the installer runs same-origin under achenkunju.com or is rendered
     cross-origin from the served HTML). The existing module owns the identity,
     validation, ban list, gate UI, and same-/cross-origin bridge. -->
<script src="https://achenkunju.com/abelid/abelid.js"></script>
<script>(function (p) {
    if (window.AbelID) { AbelID.protect({ project: p }); return; }
    // Fail closed: if the identity gate can't load, block instead of allowing
    // the installer to run without protection.
    function block() {
        var o = document.createElement('div');
        o.setAttribute('role', 'dialog');
        o.style.cssText = 'position:fixed;inset:0;z-index:2147483000;display:flex;align-items:center;justify-content:center;padding:24px;background:#05070f;color:#eef2fb;text-align:center;font-family:system-ui,sans-serif';
        o.innerHTML = '<div style="max-width:420px"><div style="font-size:34px;margin-bottom:14px">&#128274;</div><h1 style="font-size:20px;margin:0 0 8px">Identity check unavailable</h1><p style="color:#a8b5cd;font-size:15px;margin:0 0 20px">' + p + ' could not load the AbelDeviceID gate, so it cannot verify this device. Check your connection and reload.</p><button style="font:inherit;font-weight:600;border:0;border-radius:12px;padding:12px 20px;cursor:pointer;color:#05070f;background:#6aa5ff">Reload</button></div>';
        o.querySelector('button').addEventListener('click', function () { location.reload(); });
        (document.body || document.documentElement).appendChild(o);
    }
    if (document.body) block(); else window.addEventListener('DOMContentLoaded', block);
})('Abel Tools');</script>
</head>
<body>
<div class="atmosphere" aria-hidden="true"></div>
<header class="mini-header" id="miniHeader" aria-hidden="true">
    <span class="mini-title">Abel Tools</span>
    <span class="mini-version" id="miniVersion"></span>
</header>
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

    <div id="spotlights"></div>

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
    <div class="empty" id="empty">
        <div class="empty-icon" aria-hidden="true">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" aria-hidden="true"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
        </div>
        <strong>No results</strong><br>Try a different search or category.<br><button class="empty-clear" id="emptyClear">Clear filters</button>
    </div>

    <p class="footer">
        Abel Tools Installer &middot; Tap GET to install through the installer engine.<br>
        Shortcuts remain normal Apple Shortcuts on your device.<br>
        &copy; 2026 Abel Tools Installer by Abel Achenkunju. All rights reserved.
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
    <h3 class="about-heading">About the developer</h3>
    <p class="sheet-desc about-bio">
        Abel Achenkunju builds tools, shortcuts, and whatever comes next &mdash;
        including Abel Tools, Abel&rsquo;s Countdown, and a browser-based file converter.
    </p>
    <div class="about-links">
        <a class="about-link" href="https://achenkunju.com" target="_blank" rel="noopener noreferrer">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="12" cy="12" r="9"/><path d="M3 12h18"/><path d="M12 3a15 15 0 0 1 0 18 15 15 0 0 1 0-18Z"/></svg>
            Website
        </a>
        <a class="about-link" href="https://blog.achenkunju.com" target="_blank" rel="noopener noreferrer">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"/><path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"/></svg>
            Blog
        </a>
        <a class="about-link" href="https://github.com/therealabela" target="_blank" rel="noopener noreferrer">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.4 5.4 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
            GitHub
        </a>
    </div>
    <p class="sheet-copyright">&copy; 2026 Abel Tools Installer by Abel Achenkunju. All rights reserved.</p>
</div>

<div class="alert-overlay" id="alertOverlay"></div>
<div class="alert" id="alert" role="alertdialog" aria-modal="true" aria-labelledby="alertTitle">
    <div class="alert-icon" id="alertIcon" aria-hidden="true"></div>
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

    /* ================= Runtime capability wall =================
       Backup to the server-side signed-URL gate. app.md is only usable when
       loaded same-origin under achenkunju.com in a secure context (so the
       shared AbelDeviceID module can run). If it is ever loaded some other way
       — e.g. an old string-injected/opaque-origin web view, or a saved copy —
       show a short "get the shortcut" message instead of a broken installer. */
    var isSupportedRuntime =
        location.origin === 'https://achenkunju.com' &&
        window.isSecureContext === true &&
        !!(window.crypto && window.crypto.subtle);
    if (!isSupportedRuntime) {
        document.documentElement.innerHTML =
            '<body style="margin:0;min-height:100vh;display:flex;align-items:center;' +
            'justify-content:center;padding:24px;background:#05070f;color:#eef2fb;' +
            'text-align:center;font-family:-apple-system,system-ui,sans-serif;line-height:1.6">' +
            '<div style="max-width:420px"><div style="font-size:34px;margin-bottom:14px">&#128241;</div>' +
            '<h1 style="font-size:20px;margin:0 0 8px">Open this in the Abel Tools Installer</h1>' +
            '<p style="color:#a8b5cd;font-size:15px;margin:0 0 20px">Run the Abel Tools Installer ' +
            'shortcut to open this installer. If you don’t have it yet, add the shortcut first.</p>' +
            '<a href="https://www.icloud.com/shortcuts/5ef518ebbbca40039df5325b264e9fb0" ' +
            'style="display:block;text-decoration:none;font-weight:600;color:#05070f;background:#6aa5ff;' +
            'border-radius:12px;padding:13px 22px">Get the Abel Tools Installer</a></div></body>';
        return;
    }

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
        themeIcon.classList.remove('icon-spin');
        void themeIcon.offsetWidth; // restart the animation
        themeIcon.classList.add('icon-spin');
        try { localStorage.setItem('abeltools-theme', currentTheme); } catch (e) {}
    });

    /* ================= Collapsing mini header ================= */

    var miniHeader = document.getElementById('miniHeader');
    var headerRow = document.querySelector('.header-row');

    function onScroll() {
        miniHeader.classList.toggle('show',
            window.scrollY > headerRow.offsetTop + headerRow.offsetHeight);
    }
    window.addEventListener('scroll', onScroll, { passive: true });
    onScroll();

    miniHeader.addEventListener('click', function () {
        window.scrollTo({ top: 0, behavior: 'smooth' });
    });

    /* ================= Rendering ================= */

    var listEl = document.getElementById('list');
    var emptyEl = document.getElementById('empty');
    var countEl = document.getElementById('sectionCount');
    var chipsEl = document.getElementById('chips');

    // Edge fades signal that the chip strip scrolls; hide each fade at its end.
    function updateChipFade() {
        var maxScroll = chipsEl.scrollWidth - chipsEl.clientWidth;
        chipsEl.style.setProperty('--fade-l', chipsEl.scrollLeft > 6 ? '24px' : '0px');
        chipsEl.style.setProperty('--fade-r', chipsEl.scrollLeft < maxScroll - 6 ? '24px' : '0px');
    }
    chipsEl.addEventListener('scroll', updateChipFade, { passive: true });
    window.addEventListener('resize', updateChipFade);

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
        updateChipFade();
    }

    function matchesFilters(item) {
        if (activeCategory !== 'All' && item.category !== activeCategory) return false;
        if (searchQuery && item.name.toLowerCase().indexOf(searchQuery) === -1 &&
            item.category.toLowerCase().indexOf(searchQuery) === -1 &&
            item.desc.toLowerCase().indexOf(searchQuery) === -1) return false;
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

    var spotEl = document.getElementById('spotlights');

    function renderSpotlights() {
        spotEl.innerHTML = '';
        // Spotlights only decorate the default browse view
        if (activeCategory !== 'All' || searchQuery) return;

        catalog.filter(function (i) { return i.isNew && !i.eol; })
            .slice(0, 2)
            .forEach(function (item) {
                var card = el('div', 'spotlight');
                card.style.background = item.gradient;
                card.setAttribute('role', 'button');
                card.setAttribute('tabindex', '0');
                card.setAttribute('aria-label', 'View details for ' + item.name);

                card.appendChild(el('p', 'spotlight-eyebrow', 'New this update'));

                var icon = el('div', 'spotlight-icon');
                icon.innerHTML = iconSvg(item.icon, 32);

                var info = el('div', 'spotlight-info');
                info.appendChild(el('div', 'spotlight-name', item.name));
                info.appendChild(el('div', 'spotlight-desc', item.desc));

                var body = el('div', 'spotlight-body');
                body.appendChild(icon);
                body.appendChild(info);
                body.appendChild(buildButton(item, statusFor(item)));
                card.appendChild(body);

                card.addEventListener('click', function (e) {
                    if (e.target.closest('.btn')) return;
                    openSheet(item);
                });
                card.addEventListener('keydown', function (e) {
                    if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); openSheet(item); }
                });

                spotEl.appendChild(card);
            });
    }

    function render() {
        renderSpotlights();
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

    /* ================= Search ================= */

    var searchInput = document.getElementById('searchInput');
    var searchClear = document.getElementById('searchClear');

    function setSearch(value) {
        searchQuery = value.trim().toLowerCase();
        searchClear.classList.toggle('show', searchQuery.length > 0);
        render();
    }

    searchInput.addEventListener('input', function () { setSearch(searchInput.value); });
    searchClear.addEventListener('click', function () {
        searchInput.value = '';
        setSearch('');
        searchInput.focus();
    });

    document.getElementById('emptyClear').addEventListener('click', function () {
        searchInput.value = '';
        searchQuery = '';
        searchClear.classList.remove('show');
        activeCategory = 'All';
        buildChips();
        render();
    });

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

    /* ================= Swipe-to-dismiss sheets ================= */

    function enableSwipe(sheetEl, closeFn) {
        var startY = 0, dy = 0, dragging = false;

        sheetEl.addEventListener('touchstart', function (e) {
            if (sheetEl.scrollTop > 0) return; // let content scroll first
            startY = e.touches[0].clientY;
            dy = 0;
            dragging = true;
        }, { passive: true });

        sheetEl.addEventListener('touchmove', function (e) {
            if (!dragging) return;
            dy = e.touches[0].clientY - startY;
            if (dy <= 0) { // upward: hand the gesture back to scrolling
                dragging = false;
                sheetEl.style.transition = '';
                sheetEl.style.transform = '';
                return;
            }
            e.preventDefault();
            sheetEl.style.transition = 'none';
            sheetEl.style.transform = 'translateY(' + dy + 'px)';
        }, { passive: false });

        sheetEl.addEventListener('touchend', function () {
            if (!dragging) return;
            dragging = false;
            // Clearing inline styles in the same frame lets the CSS
            // transition pick up from the dragged position.
            sheetEl.style.transition = '';
            sheetEl.style.transform = '';
            if (dy > 110) closeFn();
        });
    }

    enableSwipe(sheet, closeSheet);
    enableSwipe(aboutSheet, closeAbout);

    /* ================= Confirm alert ================= */

    var alertBox = document.getElementById('alert');
    var alertOverlay = document.getElementById('alertOverlay');
    var alertContinue = document.getElementById('alertContinue');

    function openConfirm(item, href) {
        var iconNode = document.getElementById('alertIcon');
        iconNode.style.background = item.gradient;
        iconNode.innerHTML = iconSvg(item.icon, 26);
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
            document.getElementById('miniVersion').textContent = 'v' + version;
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
