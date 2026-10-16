<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, viewport-fit=cover, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>Abel Tools Installer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,600;12..96,700;12..96,800&amp;family=Figtree:wght@400;500;600;700&amp;family=JetBrains+Mono:wght@500;600&amp;display=swap" rel="stylesheet">
<script>
/* Paint the saved look before the first frame, so a dark-mode device never
   flashes the light theme. The main script re-derives the same choice and
   owns it from then on. */
(function () {
    var d = document.documentElement, mode = '', accent = '';
    try {
        mode = localStorage.getItem('abeltools-thememode') || localStorage.getItem('abeltools-theme') || '';
        accent = localStorage.getItem('abeltools-accent') || '';
    } catch (e) {}
    if (!mode || !accent) {
        var m = document.cookie.match(/(?:^|; )abeltools-look=([^;]*)/);
        var look = m ? decodeURIComponent(m[1]).split('|') : [];
        mode = mode || look[0] || '';
        accent = accent || look[1] || '';
    }
    if (mode !== 'light' && mode !== 'dark') {
        mode = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';
    }
    if (mode === 'dark') d.setAttribute('data-theme', 'dark');
    if (accent && accent !== 'blue') d.setAttribute('data-accent', accent);
})();
</script>
<style>
    /* ================= Tokens =================
       Light is paper and ink, dark is the near-black set from the Discover
       artboard. Every surface reads a token, so a screen the design only
       drew in light still gets a dark mode that belongs to it. */

    :root {
        --f-display: 'Bricolage Grotesque', -apple-system, system-ui, sans-serif;
        --f-body: 'Figtree', -apple-system, system-ui, sans-serif;
        --f-mono: 'JetBrains Mono', ui-monospace, Menlo, monospace;

        --bg: #F4F2ED;
        --side: #ECE9E2;
        --side-line: #DEDAD1;
        --card: #FFFFFF;
        --card-line: #E6E2D9;
        --row-line: #EFECE6;
        --ink: #17171B;
        --ink-2: #3D3D45;
        --ink-3: #4A4A53;
        --muted: #5E5E68;
        --muted-2: #6E6E78;
        --sub: #5E5E68;
        --star-off: #9A9AA3;
        --search-ic: #6E6E78;
        --field: #FFFFFF;
        --field-line: #E0DCD3;
        --nav-on: #FFFFFF;
        --nav-on-shadow: 0 1px 0 #D9D5CB;
        --sync-card: #F7F5F0;
        --sync-card-line: #DCD8CE;
        --sync-avatar: #E2DED4;
        --notice: #17171B;
        --notice-ink: #F4F2ED;
        --notice-x: #C9C7C0;
        --seg: #E6E2D9;
        --seg-2: #EFECE6;
        --seg-on: #FFFFFF;
        --seg-on-shadow: 0 1px 2px rgba(23, 23, 27, 0.08);
        --seg-off: #4A4A53;
        --pill-line: #E0DCD3;
        --pill-ink: #5E5E68;
        --retired: #A1401C;
        --retired-line: #DDB7A8;
        --ret-card-line: #D3CEC3;
        --ret-tile: #B5B5BB;
        --lime: #CDEB52;
        --brand-bg: #17171B;
        --brand-fg: #CDEB52;
        --panel: #17171B;
        --panel-line: transparent;
        --panel-ink: #F4F2ED;
        --panel-muted: #BDBBB4;
        --panel-tile: #2A2A31;
        --panel-btn: #24242A;
        --panel-btn-line: #3A3A42;
        --tile-2: #F1EFEA;
        --dl: #FAF9F6;
        --dl-line: #ECE9E2;
        --steps: #F6F4EF;
        --steps-line: #EBE8E1;
        --input: #FAF9F6;
        --input-line: #D6D2C8;
        --btn2: #FFFFFF;
        --btn2-line: #D6D2C8;
        --ink-btn: #17171B;
        --ink-btn-fg: #FFFFFF;
        --hint: #ECE9E2;
        --ghost: #E6E2D9;
        --radio-off: #CFCBC1;
        --ok-bg: #E4F3EA;
        --ok-ink: #17643C;
        --bad-bg: #FBE9E6;
        --bad-ink: #B42318;
        --bad-solid: #C42B1C;
        --scrim: rgba(23, 23, 27, 0.42);
        --scrim-alert: rgba(23, 23, 27, 0.48);
        --sheet-shadow: -20px 0 60px rgba(23, 23, 27, 0.22);
        --alert-shadow: 0 30px 80px rgba(23, 23, 27, 0.35);
        --sheet-edge: transparent;

        /* Accent: blue, exactly as drawn */
        --accent: #2742E8;
        --accent-ink: #1A2FB8;
        --accent-soft: #E6EAFD;
        --accent-soft-ink: #1A2FB8;
        --accent-dim: #B9C2F5;
        --on-accent: #FFFFFF;
        --link: #2742E8;
        --link-hover: #1A2FB8;

        color-scheme: light;
    }

    :root[data-theme="dark"] {
        --bg: #111114;
        --side: #16161A;
        --side-line: #26262C;
        --card: #1B1B20;
        --card-line: #2A2A31;
        --row-line: #27272D;
        --ink: #F2F1EE;
        --ink-2: #C8C8D0;
        --ink-3: #B6B6BF;
        --muted: #9C9CA6;
        --muted-2: #8E8E98;
        --sub: #A8A8B2;
        --star-off: #74747E;
        --search-ic: #9C9CA6;
        --field: #1B1B20;
        --field-line: #2E2E35;
        --nav-on: #26262D;
        --nav-on-shadow: none;
        --sync-card: #1B1B20;
        --sync-card-line: #2A2A31;
        --sync-avatar: #2A2A31;
        --notice: #24242A;
        --notice-ink: #F2F1EE;
        --notice-x: #B6B6BF;
        --seg: #22222A;
        --seg-2: #22222A;
        --seg-on: #34343C;
        --seg-on-shadow: none;
        --seg-off: #B6B6BF;
        --pill-line: #34343B;
        --pill-ink: #A8A8B2;
        --retired: #F08A65;
        --retired-line: #6B3A29;
        --ret-card-line: #3A3A42;
        --ret-tile: #4A4A52;
        --brand-bg: #CDEB52;
        --brand-fg: #17171B;
        --panel: #24242A;
        --panel-line: #2E2E36;
        --panel-ink: #F2F1EE;
        --panel-muted: #B6B6BF;
        --panel-tile: #34343C;
        --panel-btn: #2E2E36;
        --panel-btn-line: #3A3A42;
        --tile-2: #26262D;
        --dl: #16161A;
        --dl-line: #2A2A31;
        --steps: #16161A;
        --steps-line: #27272D;
        --input: #16161A;
        --input-line: #34343B;
        --btn2: #1B1B20;
        --btn2-line: #34343B;
        --ink-btn: #F2F1EE;
        --ink-btn-fg: #17171B;
        --hint: #1B1B20;
        --ghost: #26262D;
        --radio-off: #3A3A42;
        --ok-bg: #16301F;
        --ok-ink: #7FD9A3;
        --bad-bg: #3A1B17;
        --bad-ink: #FF9A8A;
        --bad-solid: #C42B1C;
        --scrim: rgba(0, 0, 0, 0.55);
        --scrim-alert: rgba(0, 0, 0, 0.6);
        --sheet-shadow: -20px 0 60px rgba(0, 0, 0, 0.5);
        --alert-shadow: 0 30px 80px rgba(0, 0, 0, 0.6);
        --sheet-edge: #2A2A31;

        --accent: #8090FF;
        --accent-ink: #B3BCFF;
        --accent-soft: #252A52;
        --accent-soft-ink: #C2C9FF;
        --on-accent: #0C0F2B;
        --link: #B3BCFF;
        --link-hover: #D3D8FF;

        color-scheme: dark;
    }

    /* The other seven accents keep blue's relationships: each token sits at
       the lightness blue's does, in the accent's own hue. */
    :root[data-accent="indigo"] { --accent-dim: #C4C0EC; --accent: #5B4FE0; --accent-ink: #3D2FA6; --accent-soft: #EAE9FA; --accent-soft-ink: #3D2FA6; --link: #5B4FE0; --link-hover: #3D2FA6; }
    :root[data-theme="dark"][data-accent="indigo"] { --accent: #988CED; --accent-ink: #C1B9F3; --accent-soft: #2D294B; --accent-soft-ink: #CDC7F5; --on-accent: #120E27; --link: #C1B9F3; --link-hover: #DBD6F8; }
    :root[data-accent="purple"] { --accent-dim: #D2BAEB; --accent: #8B3FF0; --accent-ink: #5A0CA8; --accent-soft: #EFE7F9; --accent-soft-ink: #5A0CA8; --link: #8B3FF0; --link-hover: #5A0CA8; }
    :root[data-theme="dark"][data-accent="purple"] { --accent: #B37EEB; --accent-ink: #D3B1F1; --accent-soft: #37244B; --accent-soft-ink: #DCC1F3; --on-accent: #180B26; --link: #D3B1F1; --link-hover: #E6D2F6; }
    :root[data-accent="pink"] { --accent-dim: #EAB6BF; --accent: #D6307F; --accent-ink: #86014A; --accent-soft: #F9E5E9; --accent-soft-ink: #86014A; --link: #D6307F; --link-hover: #86014A; }
    :root[data-theme="dark"][data-accent="pink"] { --accent: #E17490; --accent-ink: #F0ACB8; --accent-soft: #47202A; --accent-soft-ink: #F4BDC5; --on-accent: #230810; --link: #F0ACB8; --link-hover: #F7CFD4; }
    :root[data-accent="red"] { --accent-dim: #EAB7B1; --accent: #D42A4B; --accent-ink: #8A0429; --accent-soft: #F9E6E4; --accent-soft-ink: #8A0429; --link: #D42A4B; --link-hover: #8A0429; }
    :root[data-theme="dark"][data-accent="red"] { --accent: #E37872; --accent-ink: #F0AFA6; --accent-soft: #48211F; --accent-soft-ink: #F4BFB7; --on-accent: #240908; --link: #F0AFA6; --link-hover: #F7D1CB; }
    :root[data-accent="orange"] { --accent-dim: #E0BEA6; --accent: #E0640F; --accent-ink: #763103; --accent-soft: #F5E8E0; --accent-soft-ink: #763103; --link: #E0640F; --link-hover: #763103; }
    :root[data-theme="dark"][data-accent="orange"] { --accent: #D38752; --accent-ink: #E4B797; --accent-soft: #422714; --accent-soft-ink: #E9C6AB; --on-accent: #200D02; --link: #E4B797; --link-hover: #EFD6C3; }
    :root[data-accent="green"] { --accent-dim: #B0CEC0; --accent: #138A55; --accent-ink: #055733; --accent-soft: #E3EEE9; --accent-soft-ink: #055733; --link: #138A55; --link-hover: #055733; }
    :root[data-theme="dark"][data-accent="green"] { --accent: #67AD8F; --accent-ink: #A4CCBB; --accent-soft: #1B342A; --accent-soft-ink: #B6D6C9; --on-accent: #05170F; --link: #A4CCBB; --link-hover: #CAE1D8; }
    :root[data-accent="graphite"] { --accent-dim: #C4C5CA; --accent: #4F5663; --accent-ink: #434954; --accent-soft: #EAEBED; --accent-soft-ink: #434954; --link: #4F5663; --link-hover: #434954; }
    :root[data-theme="dark"][data-accent="graphite"] { --accent: #989BA5; --accent-ink: #C0C1C8; --accent-soft: #2D2E32; --accent-soft-ink: #CCCDD2; --on-accent: #121315; --link: #C0C1C8; --link-hover: #DADBDE; }

    /* ================= Base ================= */

    /* Box sizing follows the artboards: buttons and fields are border-box
       (as the browser draws them there), and so is every element the design
       marks that way below. Everything else is content-box, so a 270px panel
       with 20px padding really is 310px wide, as drawn. */
    * { -webkit-tap-highlight-color: transparent; }
    button, input { box-sizing: border-box; }
    html { -webkit-text-size-adjust: 100%; background: var(--bg); }
    body {
        margin: 0;
        background: var(--bg);
        color: var(--ink);
        font-family: var(--f-body);
    }
    button, input { font-family: inherit; }
    button { cursor: pointer; }
    button:disabled { cursor: default; }
    a { color: var(--link); }
    a:hover { color: var(--link-hover); }
    a, button, input, [role="button"] { touch-action: manipulation; }
    [hidden] { display: none !important; }
    :focus-visible { outline: 2px solid var(--accent); outline-offset: 2px; }
    h1, h2, h3, p { margin: 0; }

    .app { display: flex; min-height: 100vh; min-height: 100dvh; }

    /* ================= Sidebar ================= */

    .side {
        width: 248px;
        flex-shrink: 0;
        box-sizing: border-box;
        position: sticky;
        top: 0;
        height: 100vh;
        height: 100dvh;
        overflow-y: auto;
        display: flex;
        flex-direction: column;
        gap: 22px;
        padding: calc(22px + env(safe-area-inset-top)) 16px calc(18px + env(safe-area-inset-bottom)) calc(16px + env(safe-area-inset-left));
        background: var(--side);
        border-right: 1px solid var(--side-line);
        scrollbar-width: none;
    }
    .side::-webkit-scrollbar { display: none; }

    .brand { display: flex; align-items: center; gap: 11px; padding: 0 6px; min-width: 0; }
    .brand-tile {
        width: 38px; height: 38px; border-radius: 10px; flex-shrink: 0;
        background: var(--brand-bg); color: var(--brand-fg);
        display: flex; align-items: center; justify-content: center;
    }
    .brand-text { display: flex; flex-direction: column; gap: 2px; min-width: 0; }
    .brand-name { font-family: var(--f-display); font-weight: 800; font-size: 18px; letter-spacing: -0.02em; }
    .brand-ver { font-family: var(--f-mono); font-size: 11px; color: var(--muted); }

    .nav-group { display: flex; flex-direction: column; gap: 4px; }
    .nav-btn {
        display: flex; align-items: center; gap: 12px;
        height: 44px; padding: 0 12px;
        border: 0; border-radius: 11px;
        background: transparent; color: var(--ink-2);
        font-size: 15px; font-weight: 600; text-align: left;
    }
    .nav-btn .lbl { flex: 1; }
    .nav-btn[aria-current="page"] { background: var(--nav-on); box-shadow: var(--nav-on-shadow); color: var(--ink); }
    .nav-btn[aria-current="page"] svg { stroke: var(--accent); }
    .nav-count { font-family: var(--f-mono); font-size: 12px; color: var(--muted); }
    .nav-badge {
        min-width: 22px; height: 22px; padding: 0 7px; border-radius: 999px; box-sizing: border-box;
        background: var(--accent); color: var(--on-accent);
        font-size: 12px; font-weight: 700;
        display: inline-flex; align-items: center; justify-content: center;
    }

    .cats { display: flex; flex-direction: column; gap: 2px; }
    .side-label {
        padding: 0 12px 8px;
        font-family: var(--f-mono); font-size: 11px; font-weight: 600; letter-spacing: 0.08em;
        color: var(--muted);
    }
    .cat-btn {
        display: flex; align-items: center; gap: 12px;
        height: 38px; padding: 0 12px;
        border: 0; border-radius: 10px;
        background: transparent; color: var(--ink-2);
        font-size: 14px; font-weight: 500; text-align: left;
    }
    .cat-btn[aria-pressed="true"] { background: var(--nav-on); box-shadow: var(--nav-on-shadow); color: var(--ink); font-weight: 600; }
    .cat-dot { width: 8px; height: 8px; border-radius: 3px; flex-shrink: 0; background: var(--c); }
    [data-theme="dark"] .cat-dot { background: var(--cd); }
    .cat-name { flex: 1; }
    .cat-count { font-family: var(--f-mono); font-size: 12px; color: var(--muted-2); }

    .side-foot { margin-top: auto; display: flex; flex-direction: column; gap: 6px; }
    .sync-card {
        display: flex; align-items: center; gap: 11px;
        padding: 10px;
        border: 1px solid var(--sync-card-line); border-radius: 13px;
        background: var(--sync-card); color: var(--ink); text-align: left;
    }
    .sync-avatar {
        width: 36px; height: 36px; border-radius: 50%; flex-shrink: 0;
        background: var(--sync-avatar); color: var(--ink-2);
        display: flex; align-items: center; justify-content: center;
        font-family: var(--f-display); font-weight: 800; font-size: 16px;
    }
    .sync-avatar.is-initial { background: var(--brand-bg); color: var(--brand-fg); }
    .sync-text { display: flex; flex-direction: column; gap: 1px; flex: 1; min-width: 0; }
    .sync-title { font-size: 14px; font-weight: 700; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
    .sync-sub { font-size: 12px; color: var(--muted); }
    .sync-sub.is-alert, .set-sub.is-alert { color: var(--accent-ink); font-weight: 600; }

    /* Settings sidebar */
    .side-settings { gap: 18px; padding-bottom: calc(22px + env(safe-area-inset-bottom)); }
    .back-btn {
        align-self: flex-start;
        display: flex; align-items: center; gap: 6px;
        height: 40px; padding: 0 10px 0 6px;
        border: 0; border-radius: 10px;
        background: transparent; color: var(--link);
        font-size: 15px; font-weight: 700;
    }
    .set-title { margin: 0 6px; font-family: var(--f-display); font-weight: 800; font-size: 30px; letter-spacing: -0.03em; }
    .set-items { display: flex; flex-direction: column; gap: 4px; }
    .set-item {
        display: flex; align-items: center; gap: 12px;
        min-height: 52px; padding: 6px 12px;
        border: 0; border-radius: 11px;
        background: transparent; color: var(--ink-2); text-align: left;
    }
    .set-item[aria-current="page"] { background: var(--nav-on); box-shadow: var(--nav-on-shadow); color: var(--ink); }
    .set-tile {
        width: 30px; height: 30px; border-radius: 8px; flex-shrink: 0;
        display: flex; align-items: center; justify-content: center;
    }
    .t-brand { background: var(--brand-bg); color: var(--brand-fg); }
    .t-accent { background: var(--accent); color: var(--on-accent); }
    .t-gray { background: #6E6E78; color: #FFFFFF; }
    .set-text { display: flex; flex-direction: column; gap: 1px; }
    .set-name { font-size: 15px; font-weight: 600; }
    .set-sub { font-size: 12px; color: var(--muted); }

    /* Phone-width header and tabs (shown below 760px only) */
    .topbar, .tabs, .cat-strip { display: none; }

    /* ================= Shared pieces ================= */

    .view { flex: 1; min-width: 0; min-height: 100vh; min-height: 100dvh; box-sizing: border-box; display: flex; flex-direction: column; }
    .h1 { font-family: var(--f-display); font-weight: 800; font-size: 38px; letter-spacing: -0.03em; line-height: 1; }
    .eyebrow, .mono-label {
        font-family: var(--f-mono); font-size: 11px; font-weight: 600; letter-spacing: 0.08em;
        color: var(--muted);
    }
    .eyebrow { font-size: 11.5px; }
    .mono-count { font-family: var(--f-mono); font-size: 12px; color: var(--muted); }
    .card { background: var(--card); border: 1px solid var(--card-line); border-radius: 16px; }

    .icon-btn {
        width: 44px; height: 44px; flex-shrink: 0; padding: 0;
        border-radius: 12px; border: 1px solid var(--field-line);
        background: var(--field); color: var(--ink);
        display: flex; align-items: center; justify-content: center;
    }

    .tile {
        display: flex; align-items: center; justify-content: center; flex-shrink: 0;
        background: var(--t); color: #FFFFFF;
    }
    [data-theme="dark"] .tile { background: var(--td, var(--t)); }
    .tile.has-img { overflow: hidden; }
    .tile-img {
        width: 100%; height: 100%;
        object-fit: cover; border-radius: inherit; display: block;
        pointer-events: none; -webkit-user-select: none; user-select: none;
    }
    /* Retired tools keep their icon, faded the way the list always showed them */
    .row.is-eol .tile, .ret-card .tile.has-img { opacity: 0.5; filter: saturate(0.3); -webkit-filter: saturate(0.3); }
    .tile-40 { width: 40px; height: 40px; border-radius: 10px; }
    .tile-44 { width: 44px; height: 44px; border-radius: 11px; }
    .tile-52 { width: 52px; height: 52px; border-radius: 13px; }
    .tile-56 { width: 56px; height: 56px; border-radius: 14px; }
    .tile-60 { width: 60px; height: 60px; border-radius: 15px; }
    .tile-84 { width: 84px; height: 84px; border-radius: 21px; }

    .badge-new {
        font-family: var(--f-mono); font-size: 10.5px; font-weight: 600; letter-spacing: 0.06em;
        padding: 4px 7px; border-radius: 5px;
        background: var(--lime); color: #17171B;
    }
    .badge-new.sm { font-size: 10px; padding: 3px 5px; border-radius: 4px; flex-shrink: 0; }
    .badge-new.tight { letter-spacing: 0; } /* the detail panel's badge is drawn without tracking */

    /* Install buttons and status pills */
    .pill {
        box-sizing: border-box;
        display: inline-flex; align-items: center; justify-content: center; gap: 5px;
        border: 0; border-radius: 999px;
        font-weight: 700; text-decoration: none; white-space: nowrap;
        min-width: 76px; height: 36px; padding: 0 16px; font-size: 13.5px;
    }
    .pill-get, .pill-get:hover { background: var(--accent-soft); color: var(--accent-soft-ink); }
    .pill-upd, .pill-upd:hover { background: var(--accent); color: var(--on-accent); }
    .pill-inst, .pill-ret { min-width: 0; padding: 0 12px; font-size: 13px; font-weight: 600; }
    .pill-inst { border: 1px solid var(--pill-line); color: var(--pill-ink); background: transparent; }
    .pill-ret { border: 1px dashed var(--retired-line); color: var(--retired); background: transparent; }
    .pill.sz-spot { min-width: 80px; height: 38px; padding: 0 18px; font-size: 14px; }
    .pill.sz-spot.pill-inst, .pill.sz-spot.pill-ret { min-width: 0; padding: 0 12px; font-size: 13px; }
    .pill.sz-sm { min-width: 68px; padding: 0 14px; }
    .pill.sz-sm.pill-inst, .pill.sz-sm.pill-ret { min-width: 0; padding: 0 12px; }
    .pill.sz-xl { min-width: 96px; height: 42px; padding: 0 20px; font-size: 14px; }

    .seg { display: flex; gap: 2px; padding: 3px; border-radius: 11px; background: var(--seg); }
    .seg-btn {
        height: 34px; padding: 0 14px;
        border: 0; border-radius: 8px;
        background: transparent; color: var(--seg-off);
        font-size: 13px; font-weight: 600;
    }
    .seg-btn[aria-pressed="true"] { background: var(--seg-on); box-shadow: var(--seg-on-shadow); color: var(--ink); font-weight: 700; }

    .btn-ink, .btn-2 {
        height: 46px; padding: 0 22px; border-radius: 12px;
        font-size: 15px; font-weight: 700;
    }
    .btn-ink { border: 0; background: var(--ink-btn); color: var(--ink-btn-fg); }
    .btn-2 { border: 1px solid var(--btn2-line); background: var(--btn2); color: var(--ink); }
    .btn-lime { height: 42px; border-radius: 11px; border: 0; background: var(--lime); color: #17171B; font-size: 14px; font-weight: 700; }
    .btn-quiet {
        height: 44px; padding: 0 12px;
        border: 0; border-radius: 10px;
        background: transparent; color: var(--ink-3);
        font-size: 14px; font-weight: 700;
    }

    @keyframes star-pop { 0% { transform: scale(1); } 40% { transform: scale(1.28); } 100% { transform: scale(1); } }
    @media (prefers-reduced-motion: no-preference) {
        .star-pop svg { animation: star-pop 0.32s cubic-bezier(0.2, 0.8, 0.2, 1); }
    }

    /* ================= Discover ================= */

    .view-discover { gap: 18px; padding: calc(26px + env(safe-area-inset-top)) calc(34px + env(safe-area-inset-right)) calc(34px + env(safe-area-inset-bottom)) 34px; }
    .page-head { display: flex; align-items: flex-end; justify-content: space-between; gap: 20px; }
    .head-titles { display: flex; flex-direction: column; gap: 4px; }
    .head-tools { display: flex; align-items: center; gap: 10px; }
    .search { position: relative; display: flex; align-items: center; width: 300px; }
    .search svg { position: absolute; left: 14px; color: var(--search-ic); pointer-events: none; }
    .search input {
        width: 100%; height: 44px; padding: 0 14px 0 40px;
        border-radius: 12px; border: 1px solid var(--field-line);
        background: var(--field); color: var(--ink);
        font-size: 15px; font-weight: 500;
        -webkit-appearance: none; appearance: none;
    }

    /* The artboard draws this bar 36px tall (its column squeezes it), so
       that is the height here; longer notices grow around the text. */
    .notice {
        display: flex; align-items: center; gap: 12px;
        min-height: 36px; padding: 0 8px 0 16px;
        border-radius: 12px;
        background: var(--notice); color: var(--notice-ink);
    }
    .notice-tag {
        flex-shrink: 0;
        font-family: var(--f-mono); font-size: 11px; font-weight: 600; letter-spacing: 0.06em;
        padding: 4px 7px; border-radius: 5px;
        background: var(--lime); color: #17171B;
    }
    .notice-text { flex: 1; font-size: 14px; padding: 9px 0; }
    .notice-x {
        width: 36px; height: 36px; flex-shrink: 0; padding: 0;
        border: 0; border-radius: 9px;
        background: transparent; color: var(--notice-x);
        display: flex; align-items: center; justify-content: center;
    }

    .update-grid { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 16px; }
    .update-grid.n1 { grid-template-columns: repeat(2, minmax(0, 1fr)); }
    .update-grid.n0 { grid-template-columns: minmax(0, 1fr); }
    .whatsnew { display: flex; flex-direction: column; gap: 12px; padding: 18px 20px; }
    .wn-head { display: flex; align-items: baseline; justify-content: space-between; }
    .wn-ver { font-family: var(--f-mono); font-size: 11px; color: var(--muted); }
    .wn-list { margin: 0; padding: 0; list-style: none; display: flex; flex-direction: column; gap: 10px; }
    .wn-list li { display: flex; gap: 10px; font-size: 14px; line-height: 1.4; }
    .wn-list svg { flex-shrink: 0; margin-top: 2px; color: var(--accent); }
    .wn-foot { margin-top: auto; font-size: 12.5px; color: var(--muted); }

    .spot {
        display: flex; flex-direction: column; gap: 12px;
        padding: 18px 20px; border-radius: 16px;
        background: var(--s1); border: 1px solid var(--s2);
        cursor: pointer;
    }
    [data-theme="dark"] .spot { background: var(--s3); border-color: var(--s4); }
    .spot-top { display: flex; align-items: center; justify-content: space-between; }
    .spot-body { display: flex; flex-direction: column; gap: 4px; }
    .spot-name { font-family: var(--f-display); font-weight: 700; font-size: 19px; letter-spacing: -0.015em; }
    .spot-desc { font-size: 13.5px; line-height: 1.45; color: var(--ink-2); }
    .spot-foot { margin-top: auto; display: flex; align-items: center; justify-content: space-between; gap: 10px; }
    .spot-meta { font-size: 12.5px; font-weight: 600; color: var(--ink-2); }

    .all { display: flex; flex-direction: column; gap: 12px; padding-top: 6px; }
    .list-head { display: flex; align-items: center; justify-content: space-between; gap: 12px; flex-wrap: wrap; }
    .list-title { display: flex; align-items: baseline; gap: 10px; min-width: 0; }
    .list-title h2 { font-family: var(--f-display); font-weight: 700; font-size: 22px; letter-spacing: -0.02em; }

    .list {
        display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); column-gap: 28px;
        padding: 4px 18px; border-radius: 16px;
        background: var(--card); border: 1px solid var(--card-line);
    }
    .row {
        display: flex; align-items: center; gap: 13px;
        min-height: 70px; min-width: 0; box-sizing: border-box;
        border-bottom: 1px solid var(--row-line);
        cursor: pointer;
    }
    .row-info { flex: 1; min-width: 0; display: flex; flex-direction: column; gap: 3px; }
    .row-top { display: flex; align-items: center; gap: 7px; min-width: 0; }
    .row-name { font-size: 15px; font-weight: 700; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
    .row-sub { font-size: 13px; color: var(--sub); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
    .star-btn {
        width: 40px; height: 40px; flex-shrink: 0; padding: 0;
        border: 0; border-radius: 10px;
        background: transparent; color: var(--star-off);
        display: flex; align-items: center; justify-content: center;
    }
    .star-btn.on { color: var(--accent); }
    .row-act { width: 104px; flex-shrink: 0; display: flex; justify-content: flex-end; }

    .sk { background: var(--ghost); border-radius: 6px; }
    .sk-tile { width: 44px; height: 44px; border-radius: 11px; flex-shrink: 0; }
    .sk-lines { flex: 1; display: flex; flex-direction: column; gap: 8px; }
    .sk-l1 { height: 13px; width: 55%; }
    .sk-l2 { height: 11px; width: 80%; }
    .sk-btn { width: 76px; height: 36px; border-radius: 999px; flex-shrink: 0; }
    @media (prefers-reduced-motion: no-preference) {
        .sk { animation: sk-pulse 1.4s ease-in-out infinite; }
        @keyframes sk-pulse { 50% { opacity: 0.55; } }
    }

    .list-empty {
        display: flex; flex-direction: column; align-items: center; gap: 8px;
        padding: 36px 20px; text-align: center;
    }
    .list-empty strong { font-family: var(--f-display); font-weight: 700; font-size: 20px; letter-spacing: -0.015em; }
    .list-empty p { font-size: 14.5px; color: var(--ink-3); margin-bottom: 8px; }

    /* ================= Favorites ================= */

    .view-favorites { padding: calc(26px + env(safe-area-inset-top)) calc(34px + env(safe-area-inset-right)) calc(34px + env(safe-area-inset-bottom)) 34px; }
    .fav-headline { display: flex; align-items: baseline; gap: 12px; }
    .fav-empty {
        flex: 1;
        display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 22px;
        padding: 24px 0; text-align: center;
    }
    .fav-art { position: relative; width: 220px; height: 150px; }
    .fav-art .ghost-l, .fav-art .ghost-r {
        position: absolute; top: 34px; width: 72px; height: 72px; border-radius: 18px;
        background: var(--ghost);
    }
    .fav-art .ghost-l { left: 10px; transform: rotate(-10deg); }
    .fav-art .ghost-r { right: 10px; transform: rotate(10deg); }
    .fav-art .hero {
        position: absolute; left: 66px; top: 14px; width: 88px; height: 88px; border-radius: 22px;
        background: var(--brand-bg); color: var(--brand-fg);
        display: flex; align-items: center; justify-content: center;
        box-shadow: 0 14px 30px rgba(23, 23, 27, 0.18);
    }
    .fav-copy { display: flex; flex-direction: column; gap: 8px; max-width: 420px; }
    .fav-copy h2 { font-family: var(--f-display); font-weight: 700; font-size: 26px; letter-spacing: -0.02em; }
    .fav-copy p { font-size: 15.5px; line-height: 1.55; color: var(--ink-3); }
    .fav-btns { display: flex; gap: 10px; flex-wrap: wrap; justify-content: center; }
    .hint {
        align-self: center;
        display: flex; align-items: center; gap: 10px;
        padding: 12px 16px; border-radius: 12px;
        background: var(--hint); color: var(--ink-2);
        font-size: 13.5px;
    }
    .hint svg { color: var(--accent); flex-shrink: 0; }
    .fav-full { display: flex; flex-direction: column; gap: 12px; margin-top: 22px; }

    /* ================= Library ================= */

    .view-library { gap: 22px; padding: calc(26px + env(safe-area-inset-top)) calc(34px + env(safe-area-inset-right)) calc(34px + env(safe-area-inset-bottom)) 34px; }
    .lib-head { display: flex; flex-direction: column; gap: 6px; }
    .lib-head p { font-size: 15px; color: var(--ink-3); }
    .lib-cols { display: flex; gap: 22px; align-items: flex-start; }
    .lib-main { flex: 1; min-width: 0; display: flex; flex-direction: column; gap: 22px; }
    .lib-sec { display: flex; flex-direction: column; gap: 10px; }
    .lib-h2 {
        display: flex; align-items: baseline; gap: 8px;
        font-family: var(--f-display); font-weight: 700; font-size: 20px; letter-spacing: -0.02em;
    }
    .lib-h2 span { font-family: var(--f-mono); font-size: 12px; font-weight: 500; letter-spacing: 0; color: var(--muted); }
    .upd-card {
        display: flex; align-items: center; gap: 16px;
        padding: 16px 18px; border-radius: 16px;
        background: var(--card); border: 1.5px solid var(--accent);
        cursor: pointer;
    }
    .upd-info { flex: 1; min-width: 0; display: flex; flex-direction: column; gap: 3px; }
    .upd-name { font-size: 16px; font-weight: 700; }
    .upd-text { font-size: 13.5px; color: var(--ink-3); }
    .inst-list {
        display: flex; flex-direction: column;
        padding: 2px 18px; border-radius: 16px;
        background: var(--card); border: 1px solid var(--card-line);
    }
    .inst-row { display: flex; align-items: center; gap: 14px; min-height: 68px; border-bottom: 1px solid var(--row-line); cursor: pointer; }
    .inst-row:last-child { border-bottom: 0; }
    .inst-info { flex: 1; min-width: 0; display: flex; flex-direction: column; gap: 2px; }
    .inst-name { font-size: 15px; font-weight: 700; }
    .inst-cat { font-size: 13px; color: var(--muted); }
    .st-ready { font-size: 13px; font-weight: 700; color: var(--accent-ink); white-space: nowrap; }
    .st-ok { display: inline-flex; align-items: center; gap: 5px; font-size: 13px; font-weight: 600; color: var(--muted); white-space: nowrap; }
    .ret-card {
        display: flex; align-items: center; gap: 14px;
        padding: 12px 18px; min-height: 68px; border-radius: 16px; box-sizing: border-box;
        background: transparent; border: 1px dashed var(--ret-card-line);
        cursor: pointer;
    }
    .ret-card .tile { background: var(--ret-tile); }
    .ret-card .inst-name { color: var(--ink-3); }
    .st-ret { font-size: 13px; font-weight: 600; color: var(--retired); }
    .lib-empty { display: flex; flex-direction: column; align-items: flex-start; gap: 8px; padding: 26px 24px; }
    .lib-empty strong { font-family: var(--f-display); font-weight: 700; font-size: 20px; letter-spacing: -0.015em; }
    .lib-empty p { font-size: 14.5px; line-height: 1.5; color: var(--ink-3); margin-bottom: 8px; }

    .glance {
        width: 270px; flex-shrink: 0;
        display: flex; flex-direction: column; gap: 14px;
        padding: 20px; border-radius: 16px;
        background: var(--panel); color: var(--panel-ink);
    }
    .glance-label { font-family: var(--f-mono); font-size: 11px; font-weight: 600; letter-spacing: 0.08em; color: var(--lime); }
    .glance-grid { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 14px; }
    .glance-stat { display: flex; flex-direction: column; gap: 2px; }
    .glance-num { font-family: var(--f-display); font-weight: 800; font-size: 34px; letter-spacing: -0.03em; }
    .glance-cap { font-size: 13px; color: var(--panel-muted); }
    .glance p { font-size: 13px; line-height: 1.5; color: var(--panel-muted); }

    /* ================= Detail slide-over ================= */

    .scrim {
        position: fixed; inset: 0; z-index: 50;
        background: var(--scrim);
        opacity: 0; pointer-events: none;
        transition: opacity 0.25s ease;
    }
    .scrim.open { opacity: 1; pointer-events: auto; }
    .panel {
        position: fixed; z-index: 51;
        top: calc(12px + env(safe-area-inset-top));
        right: calc(12px + env(safe-area-inset-right));
        bottom: calc(12px + env(safe-area-inset-bottom));
        width: 470px; max-width: calc(100vw - 24px);
        display: flex; flex-direction: column;
        border-radius: 22px;
        background: var(--card); box-shadow: var(--sheet-shadow);
        overflow: hidden; outline: none;
        transform: translateX(calc(100% + 24px));
        visibility: hidden;
        transition: transform 0.34s cubic-bezier(0.2, 0.8, 0.2, 1), visibility 0s linear 0.34s;
    }
    [data-theme="dark"] .panel { box-shadow: var(--sheet-shadow), inset 0 0 0 1px var(--sheet-edge); }
    [data-theme="dark"] .alert { box-shadow: var(--alert-shadow), inset 0 0 0 1px var(--sheet-edge); }
    .panel.open { transform: none; visibility: visible; transition: transform 0.34s cubic-bezier(0.2, 0.8, 0.2, 1), visibility 0s; }
    .p-head { display: flex; align-items: center; justify-content: space-between; padding: 18px 18px 0 28px; }
    .chip {
        display: inline-flex; align-items: center; gap: 7px;
        height: 28px; padding: 0 11px; border-radius: 999px;
        background: var(--cb); color: var(--ci);
        font-size: 12.5px; font-weight: 700;
    }
    [data-theme="dark"] .chip { background: var(--cbd); color: var(--cd); }
    .chip .cat-dot { width: 7px; height: 7px; border-radius: 2px; }
    .close-btn {
        width: 44px; height: 44px; flex-shrink: 0; padding: 0;
        border: 0; border-radius: 50%;
        background: var(--tile-2); color: var(--ink-2);
        display: flex; align-items: center; justify-content: center;
    }
    .p-body {
        flex: 1;
        display: flex; flex-direction: column; gap: 22px;
        padding: 10px 28px 28px;
        overflow-y: auto; -webkit-overflow-scrolling: touch; overscroll-behavior: contain;
    }
    .p-top { display: flex; align-items: center; gap: 18px; }
    .p-top .tile { box-shadow: 0 10px 24px color-mix(in srgb, var(--t) 32%, transparent); }
    .p-titles { display: flex; flex-direction: column; gap: 6px; min-width: 0; }
    .p-name { font-family: var(--f-display); font-weight: 800; font-size: 28px; letter-spacing: -0.025em; line-height: 1.05; }
    .p-status { display: inline-flex; align-items: center; gap: 7px; font-size: 14px; font-weight: 600; color: var(--st); }
    .p-status i { width: 8px; height: 8px; border-radius: 50%; background: var(--sd); flex-shrink: 0; }
    .p-actions { display: flex; gap: 10px; }
    .p-primary {
        flex: 1; height: 52px; border-radius: 14px; border: 0;
        background: var(--accent); color: var(--on-accent);
        font-size: 16px; font-weight: 700; text-decoration: none;
        display: flex; align-items: center; justify-content: center; gap: 9px;
    }
    .p-primary:hover { color: var(--on-accent); }
    .p-primary.is-static, .p-primary.is-static:hover { background: var(--tile-2); color: var(--ink-3); cursor: default; }
    .p-fav {
        width: 52px; height: 52px; flex-shrink: 0; padding: 0;
        border: 0; border-radius: 14px;
        background: var(--tile-2); color: var(--ink-2);
        display: flex; align-items: center; justify-content: center;
    }
    .p-fav.on { background: var(--accent-soft); color: var(--accent); }
    .p-desc { font-size: 15.5px; line-height: 1.6; color: var(--ink-2); }
    .facts {
        margin: 0;
        display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 1px;
        border-radius: 14px; overflow: hidden;
        background: var(--dl-line); border: 1px solid var(--dl-line);
    }
    .fact { display: flex; flex-direction: column; gap: 3px; padding: 12px 14px; background: var(--dl); }
    .fact dt { font-family: var(--f-mono); font-size: 10.5px; font-weight: 600; letter-spacing: 0.07em; color: var(--muted); }
    .fact dd { margin: 0; font-size: 14.5px; font-weight: 600; }
    .p-sec { display: flex; flex-direction: column; gap: 10px; }
    .p-h3 { font-family: var(--f-display); font-weight: 700; font-size: 17px; letter-spacing: -0.01em; }
    .pair {
        display: flex; align-items: center; gap: 13px;
        padding: 12px 14px; border-radius: 14px;
        border: 1px solid var(--dl-line);
        cursor: pointer;
    }
    .pair-info { flex: 1; min-width: 0; display: flex; flex-direction: column; gap: 2px; }
    .pair-name { display: flex; align-items: center; gap: 7px; font-size: 14.5px; font-weight: 700; }
    .pair-note { font-size: 13px; color: var(--muted); }
    .olds { display: flex; gap: 8px; flex-wrap: wrap; }
    .old {
        display: inline-flex; align-items: center; gap: 7px;
        height: 36px; padding: 0 13px; border-radius: 10px;
        background: var(--tile-2);
        font-size: 13.5px; font-weight: 600;
    }
    .old span { color: var(--muted); font-weight: 500; }

    /* ================= Install confirm ================= */

    .alert-scrim { z-index: 60; background: var(--scrim-alert); }
    .alert-wrap {
        position: fixed; inset: 0; z-index: 61;
        display: flex; align-items: center; justify-content: center;
        padding: 16px; pointer-events: none;
    }
    .alert {
        width: 420px; max-width: 100%;
        display: flex; flex-direction: column; gap: 20px;
        padding: 28px; border-radius: 24px; box-sizing: border-box;
        background: var(--card);
        box-shadow: var(--alert-shadow);
        opacity: 0; transform: scale(0.96); visibility: hidden;
        transition: opacity 0.2s ease, transform 0.2s ease, visibility 0s linear 0.2s;
    }
    .alert.open { opacity: 1; transform: none; visibility: visible; pointer-events: auto; transition: opacity 0.2s ease, transform 0.2s ease, visibility 0s; }
    .al-head { display: flex; align-items: center; gap: 14px; }
    .al-titles { display: flex; flex-direction: column; gap: 3px; min-width: 0; }
    .al-title { font-family: var(--f-display); font-weight: 800; font-size: 22px; letter-spacing: -0.02em; }
    .al-msg { font-size: 14px; color: var(--ink-3); }
    .steps { margin: 0; padding: 0; list-style: none; display: flex; flex-direction: column; border-radius: 14px; background: var(--steps); }
    .steps li { display: flex; align-items: center; gap: 12px; padding: 12px 14px; font-size: 14px; border-bottom: 1px solid var(--steps-line); }
    .steps li:last-child { border-bottom: 0; }
    .steps strong { font-weight: 700; }
    .step-n {
        width: 24px; height: 24px; border-radius: 50%; flex-shrink: 0;
        background: var(--brand-bg); color: var(--brand-fg);
        font-family: var(--f-mono); font-size: 12px; font-weight: 600;
        display: flex; align-items: center; justify-content: center;
    }
    .al-btns { display: flex; gap: 10px; }
    .btn-cancel {
        flex: 1; height: 50px; border-radius: 13px; border: 0;
        background: var(--tile-2); color: var(--ink);
        font-size: 15.5px; font-weight: 700;
    }
    .btn-go, .btn-go:hover {
        flex: 1.4; height: 50px; border-radius: 13px;
        background: var(--accent); color: var(--on-accent);
        font-size: 15.5px; font-weight: 700; text-decoration: none;
        display: flex; align-items: center; justify-content: center; gap: 8px;
    }

    /* ================= Settings pages ================= */

    .view-settings { padding: calc(40px + env(safe-area-inset-top)) calc(56px + env(safe-area-inset-right)) calc(40px + env(safe-area-inset-bottom)) 56px; }
    .view-appearance { gap: 30px; }
    .set-head { display: flex; flex-direction: column; gap: 6px; }
    .set-head h2, .sd-head h2, .si-head h2 { font-family: var(--f-display); font-weight: 800; font-size: 34px; letter-spacing: -0.03em; }
    .set-head p { font-size: 15px; color: var(--ink-3); }
    .set-sec { display: flex; flex-direction: column; gap: 14px; }
    .sec-label { font-family: var(--f-mono); font-size: 11.5px; font-weight: 600; letter-spacing: 0.08em; color: var(--muted); }

    .theme-grid { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 16px; }
    .theme-card {
        display: flex; flex-direction: column; gap: 12px;
        padding: 12px; border-radius: 16px;
        border: 2px solid var(--card-line); background: var(--card);
        text-align: left; color: var(--ink);
    }
    .theme-card[aria-pressed="true"] { border-color: var(--accent); }
    .tc-preview { display: flex; height: 118px; border-radius: 10px; overflow: hidden; }
    .tc-preview span { display: flex; }
    .tc-row { display: flex; align-items: center; justify-content: space-between; gap: 8px; }
    .tc-text { display: flex; flex-direction: column; gap: 1px; }
    .tc-name { font-size: 15px; font-weight: 700; }
    .tc-sub { font-size: 12.5px; color: var(--muted); }
    .radio {
        width: 24px; height: 24px; border-radius: 50%; flex-shrink: 0; box-sizing: border-box;
        border: 2px solid var(--radio-off);
        display: flex; align-items: center; justify-content: center;
    }
    .radio.on { border: 0; background: var(--accent); color: var(--on-accent); }

    .accent-row { display: flex; gap: 22px; align-items: stretch; }
    .swatch-grid {
        flex: 1;
        display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 10px;
        padding: 16px; border-radius: 16px;
        background: var(--card); border: 1px solid var(--card-line);
    }
    .swatch {
        display: flex; flex-direction: column; align-items: center; gap: 7px;
        padding: 8px 4px; border: 0; border-radius: 12px;
        background: transparent;
    }
    .sw-dot {
        width: 40px; height: 40px; border-radius: 50%;
        background: var(--sw); color: #FFFFFF;
        display: flex; align-items: center; justify-content: center;
    }
    .swatch[aria-pressed="true"] .sw-dot { box-shadow: 0 0 0 3px var(--card), 0 0 0 5.5px var(--sw); }
    .sw-name { font-size: 12.5px; font-weight: 600; color: var(--ink-2); }
    .preview-card {
        width: 300px; flex-shrink: 0; box-sizing: border-box;
        display: flex; flex-direction: column; gap: 12px;
        padding: 16px; border-radius: 16px;
        background: var(--card); border: 1px solid var(--card-line);
    }
    .pv-label { font-family: var(--f-mono); font-size: 10.5px; font-weight: 600; letter-spacing: 0.08em; color: var(--muted); }
    .pv-row { display: flex; align-items: center; gap: 11px; }
    .pv-row .pv-name { flex: 1; font-size: 14.5px; font-weight: 700; }
    .pv-row > svg { color: var(--accent); }
    .pv-btns { display: flex; gap: 8px; }
    .pv-btns span {
        flex: 1; height: 36px; border-radius: 999px;
        font-size: 13.5px; font-weight: 700;
        display: flex; align-items: center; justify-content: center;
    }
    .pv-get { background: var(--accent-soft); color: var(--accent-soft-ink); }
    .pv-upd { background: var(--accent); color: var(--on-accent); }
    .pv-note { font-size: 12.5px; line-height: 1.45; color: var(--muted); }

    /* About */
    .view-about { flex-direction: row; gap: 28px; }
    .about-main { flex: 1; min-width: 0; display: flex; flex-direction: column; gap: 24px; }
    .about-top { display: flex; align-items: center; gap: 20px; }
    .about-logo {
        width: 92px; height: 92px; border-radius: 24px; flex-shrink: 0;
        background: var(--brand-bg); color: var(--brand-fg);
        display: flex; align-items: center; justify-content: center;
    }
    .about-titles { display: flex; flex-direction: column; gap: 6px; }
    .about-titles h2 { font-family: var(--f-display); font-weight: 800; font-size: 34px; letter-spacing: -0.03em; line-height: 1; }
    .about-ver { font-family: var(--f-mono); font-size: 13px; color: var(--muted); }
    .about-p { font-size: 16px; line-height: 1.6; color: var(--ink-2); max-width: 520px; }
    .dev-card { display: flex; flex-direction: column; gap: 12px; padding: 20px; }
    .dev-who { display: flex; flex-direction: column; gap: 4px; }
    .dev-name { font-family: var(--f-display); font-weight: 700; font-size: 20px; letter-spacing: -0.015em; }
    .dev-bio { font-size: 14.5px; line-height: 1.55; color: var(--ink-3); }
    .links { display: flex; flex-direction: column; margin-top: 4px; border-top: 1px solid var(--row-line); }
    .link-row, .link-row:hover {
        display: flex; align-items: center; gap: 12px;
        min-height: 50px; border-bottom: 1px solid var(--row-line);
        color: var(--ink); text-decoration: none;
    }
    .link-row:last-child { border-bottom: 0; }
    .link-row > svg:first-child { color: var(--accent); }
    .lr-name { flex: 1; font-size: 15px; font-weight: 600; }
    .lr-host { font-family: var(--f-mono); font-size: 12.5px; color: var(--muted); }
    .lr-arrow { color: var(--muted-2); }
    .about-side { width: 300px; flex-shrink: 0; display: flex; flex-direction: column; gap: 16px; }
    .id-card {
        display: flex; flex-direction: column; gap: 12px;
        padding: 20px; border-radius: 16px;
        background: var(--panel); color: var(--panel-ink);
    }
    .id-card h3 { font-family: var(--f-mono); font-size: 11.5px; font-weight: 600; letter-spacing: 0.08em; color: var(--lime); }
    .id-block { display: flex; flex-direction: column; gap: 4px; }
    .id-cap { font-size: 13px; color: var(--panel-muted); }
    .id-value { font-family: var(--f-mono); font-size: 14px; font-weight: 600; word-break: break-all; }
    .id-state { display: inline-flex; align-items: center; gap: 7px; font-size: 13px; color: var(--panel-muted); }
    .id-state i { width: 8px; height: 8px; border-radius: 50%; background: var(--dot, var(--lime)); }
    .id-copy {
        height: 42px; border-radius: 11px;
        border: 1px solid var(--panel-btn-line); background: var(--panel-btn); color: var(--panel-ink);
        font-size: 14px; font-weight: 700;
        display: flex; align-items: center; justify-content: center; gap: 8px;
    }
    .id-copy:disabled { opacity: 0.5; }
    .id-note { font-size: 12.5px; line-height: 1.45; color: var(--panel-muted); }
    .copyright { margin: auto 0 0; font-size: 12px; line-height: 1.5; color: var(--muted); }

    /* Account and Sync */
    .view-sync { padding: 0; }
    .si-wrap {
        flex: 1;
        display: flex; gap: 32px; align-items: flex-start;
        padding: calc(40px + env(safe-area-inset-top)) calc(56px + env(safe-area-inset-right)) calc(40px + env(safe-area-inset-bottom)) 56px;
    }
    .si-main { flex: 1; min-width: 0; display: flex; flex-direction: column; gap: 22px; }
    .si-head { display: flex; flex-direction: column; gap: 6px; }
    .si-head p { font-size: 15.5px; line-height: 1.5; color: var(--ink-3); max-width: 460px; }
    .si-form {
        display: flex; flex-direction: column; gap: 16px;
        padding: 24px; border-radius: 18px; max-width: 480px;
        background: var(--card); border: 1px solid var(--card-line);
    }
    .seg2 { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 2px; padding: 3px; border-radius: 11px; background: var(--seg-2); }
    .seg2 button {
        height: 38px; border: 0; border-radius: 8px;
        background: transparent; color: var(--seg-off);
        font-size: 14px; font-weight: 600;
    }
    .seg2 button[aria-pressed="true"] { background: var(--seg-on); box-shadow: var(--seg-on-shadow); color: var(--ink); font-weight: 700; }
    .field { display: flex; flex-direction: column; gap: 7px; }
    .field label { font-size: 13.5px; font-weight: 700; }
    .input {
        width: 100%; height: 50px; padding: 0 16px;
        border-radius: 12px; border: 1px solid var(--input-line);
        background: var(--input); color: var(--ink);
        font-size: 16px;
        -webkit-appearance: none; appearance: none; outline: none;
    }
    .input:focus { border: 1.5px solid var(--accent); box-shadow: 0 0 0 4px var(--accent-soft); background: var(--card); }
    .pw-wrap { position: relative; display: flex; align-items: center; }
    .pw-wrap .input { padding-right: 64px; }
    .pw-show {
        position: absolute; right: 6px;
        height: 38px; padding: 0 10px;
        border: 0; border-radius: 8px;
        background: transparent; color: var(--accent-ink);
        font-size: 13.5px; font-weight: 700;
    }
    .btn-primary {
        width: 100%; height: 52px; border-radius: 13px; border: 0;
        background: var(--accent); color: var(--on-accent);
        font-size: 16px; font-weight: 700;
    }
    .btn-primary:disabled { background: var(--accent-dim); }
    [data-theme="dark"] .btn-primary:disabled { background: var(--accent); opacity: 0.35; }
    .si-note { display: flex; gap: 9px; font-size: 13px; line-height: 1.5; color: var(--muted); }
    .si-note svg { flex-shrink: 0; margin-top: 1px; color: var(--muted-2); }
    .form-msg {
        padding: 10px 12px; border-radius: 10px;
        background: var(--hint); color: var(--ink-2);
        font-size: 13.5px; line-height: 1.45;
    }
    .form-msg.ok { background: var(--ok-bg); color: var(--ok-ink); }
    .form-msg.error { background: var(--bad-bg); color: var(--bad-ink); }
    .what-syncs {
        width: 300px; flex-shrink: 0; margin-top: 98px;
        display: flex; flex-direction: column; gap: 16px;
        padding: 22px; border-radius: 18px;
        background: var(--panel); color: var(--panel-ink);
    }
    .ws-label { font-family: var(--f-mono); font-size: 11px; font-weight: 600; letter-spacing: 0.08em; color: var(--lime); }
    .ws-row { display: flex; gap: 12px; }
    .ws-ic {
        width: 34px; height: 34px; border-radius: 9px; flex-shrink: 0;
        background: var(--panel-tile); color: var(--lime);
        display: flex; align-items: center; justify-content: center;
    }
    .ws-text { display: flex; flex-direction: column; gap: 2px; }
    .ws-title { font-size: 15px; font-weight: 700; }
    .ws-body { font-size: 13px; line-height: 1.45; color: var(--panel-muted); }

    .code-wrap {
        flex: 1;
        display: flex; align-items: center; justify-content: center;
        padding: calc(40px + env(safe-area-inset-top)) 40px calc(40px + env(safe-area-inset-bottom));
    }
    .code-card {
        width: 480px; max-width: 100%; box-sizing: border-box;
        display: flex; flex-direction: column; align-items: center; gap: 22px;
        padding: 36px 36px 28px; border-radius: 22px;
        background: var(--card); border: 1px solid var(--card-line);
        text-align: center;
    }
    .code-tile {
        width: 64px; height: 64px; border-radius: 17px;
        background: var(--brand-bg); color: var(--brand-fg);
        display: flex; align-items: center; justify-content: center;
    }
    .code-copy { display: flex; flex-direction: column; gap: 8px; }
    .code-copy h2 { font-family: var(--f-display); font-weight: 800; font-size: 28px; letter-spacing: -0.025em; }
    .code-copy p { font-size: 15px; line-height: 1.5; color: var(--ink-3); }
    .digits { margin: 0; padding: 0; border: 0; display: flex; gap: 10px; }
    .sr-only { position: absolute; width: 1px; height: 1px; overflow: hidden; clip: rect(0 0 0 0); white-space: nowrap; }
    .digit {
        width: 56px; height: 68px; padding: 0;
        border-radius: 13px; border: 1px solid var(--input-line);
        background: var(--input); color: var(--ink);
        text-align: center;
        font-family: var(--f-mono); font-size: 28px; font-weight: 600;
        caret-color: var(--accent);
        -webkit-appearance: none; appearance: none; outline: none;
    }
    .digit:focus { border: 2px solid var(--accent); box-shadow: 0 0 0 4px var(--accent-soft); background: var(--card); }
    .code-card .form-msg { align-self: stretch; }

    .sd-wrap {
        display: flex; flex-direction: column; gap: 20px;
        padding: calc(36px + env(safe-area-inset-top)) calc(48px + env(safe-area-inset-right)) calc(36px + env(safe-area-inset-bottom)) 48px;
    }
    .sd-head { display: flex; align-items: center; justify-content: space-between; gap: 16px; min-height: 41px; }
    .status-pill {
        display: inline-flex; align-items: center; gap: 8px;
        min-height: 38px; padding: 0 14px; border-radius: 999px; box-sizing: border-box;
        background: var(--hint); color: var(--ink-2);
        font-size: 14px; font-weight: 700;
        max-width: 60%;
    }
    .status-pill span { padding: 9px 0; } /* one line sits as drawn; a long error wraps inside */
    .status-pill.ok { background: var(--ok-bg); color: var(--ok-ink); }
    .status-pill.error { background: var(--bad-bg); color: var(--bad-ink); }
    .status-pill svg { flex-shrink: 0; }
    .sd-cols { display: flex; gap: 22px; align-items: flex-start; }
    .sd-main { flex: 1; min-width: 0; display: flex; flex-direction: column; gap: 20px; }
    .acct-card { display: flex; flex-direction: column; gap: 18px; padding: 22px; border-radius: 18px; }
    .acct-top { display: flex; align-items: center; gap: 14px; }
    .avatar {
        width: 52px; height: 52px; border-radius: 50%; flex-shrink: 0;
        background: var(--brand-bg); color: var(--brand-fg);
        font-family: var(--f-display); font-weight: 800; font-size: 22px;
        display: flex; align-items: center; justify-content: center;
    }
    .acct-who { flex: 1; min-width: 0; display: flex; flex-direction: column; gap: 2px; }
    .acct-email { font-size: 17px; font-weight: 700; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
    .acct-sub { font-size: 13.5px; color: var(--muted); }
    .btn-sync {
        height: 44px; padding: 0 20px; border-radius: 12px; border: 0;
        background: var(--accent); color: var(--on-accent);
        font-size: 14.5px; font-weight: 700;
        display: flex; align-items: center; justify-content: center; gap: 8px;
    }
    .stats {
        margin: 0;
        display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 1px;
        border-radius: 13px; overflow: hidden;
        background: var(--dl-line); border: 1px solid var(--dl-line);
    }
    .stat { display: flex; flex-direction: column; gap: 4px; padding: 14px 16px; background: var(--dl); }
    .stat dt { font-family: var(--f-mono); font-size: 10.5px; font-weight: 600; letter-spacing: 0.07em; color: var(--muted); }
    .stat dd { margin: 0; font-family: var(--f-display); font-size: 24px; font-weight: 800; }
    .bk-card { display: flex; flex-direction: column; gap: 14px; padding: 22px; border-radius: 18px; }
    .bk-head { display: flex; align-items: center; justify-content: space-between; gap: 12px; }
    .bk-head h3 { font-family: var(--f-display); font-weight: 700; font-size: 20px; letter-spacing: -0.015em; }
    .bk-meter { display: flex; align-items: center; gap: 10px; }
    .slots { display: flex; gap: 4px; }
    .slot { width: 18px; height: 8px; border-radius: 3px; background: var(--ghost); }
    .slot.on { background: var(--accent); }
    .bk-count { font-family: var(--f-mono); font-size: 12.5px; color: var(--muted); }
    .bk-list { margin: 0; padding: 0; list-style: none; display: flex; flex-direction: column; }
    .bk-row { display: flex; align-items: center; gap: 14px; min-height: 64px; border-bottom: 1px solid var(--row-line); }
    .bk-row:last-child { border-bottom: 0; }
    .bk-ic {
        width: 40px; height: 40px; border-radius: 10px; flex-shrink: 0;
        background: var(--tile-2); color: var(--ink-2);
        display: flex; align-items: center; justify-content: center;
    }
    .bk-info { flex: 1; min-width: 0; display: flex; flex-direction: column; gap: 2px; }
    .bk-title { font-size: 15px; font-weight: 700; }
    .bk-when { font-size: 13px; color: var(--muted); }
    .bk-when.warn { color: var(--bad-ink); font-weight: 600; }
    .bk-when.ask { color: var(--accent-ink); font-weight: 600; }
    .bk-btn { height: 38px; padding: 0 14px; border-radius: 10px; border: 0; font-size: 13.5px; font-weight: 700; flex-shrink: 0; }
    .bk-btn.restore { background: var(--accent-soft); color: var(--accent-soft-ink); }
    .bk-btn.remove { background: var(--bad-bg); color: var(--bad-ink); }
    .bk-btn.restore.armed { background: var(--accent); color: var(--on-accent); }
    .bk-btn.remove.armed { background: var(--bad-solid); color: #FFFFFF; }
    .bk-empty { font-size: 14px; line-height: 1.5; color: var(--muted); padding: 4px 0 2px; }
    .bk-foot { display: flex; align-items: center; justify-content: space-between; gap: 12px; flex-wrap: wrap; }
    .btn-add {
        height: 44px; padding: 0 18px; border-radius: 12px;
        border: 1px solid var(--btn2-line); background: var(--btn2); color: var(--ink);
        font-size: 14.5px; font-weight: 700;
        display: flex; align-items: center; gap: 8px;
    }
    .btn-add:disabled { opacity: 0.5; }
    .how {
        width: 250px; flex-shrink: 0;
        display: flex; flex-direction: column; gap: 12px;
        padding: 20px; border-radius: 18px;
        background: var(--hint);
    }
    [data-theme="dark"] .how { box-shadow: inset 0 0 0 1px var(--card-line); }
    /* The ink panels sit on a near-black page in dark mode, so they get an edge there */
    [data-theme="dark"] .glance, [data-theme="dark"] .id-card, [data-theme="dark"] .what-syncs { box-shadow: inset 0 0 0 1px var(--panel-line); }
    .how p { font-size: 14px; line-height: 1.55; color: var(--ink-2); }

    @media (prefers-reduced-motion: reduce) {
        .panel, .panel.open, .scrim, .alert, .alert.open { transition: none; }
    }

    /* ================= Narrower screens =================
       The artboards are landscape iPad. Portrait iPad keeps the sidebar and
       stacks the side panels; phone width folds the sidebar into a header. */

    @media (max-width: 1060px) {
        .list { grid-template-columns: minmax(0, 1fr); }
    }

    @media (max-width: 980px) {
        .view-discover, .view-favorites, .view-library { padding-left: 28px; padding-right: calc(28px + env(safe-area-inset-right)); }
        .update-grid, .update-grid.n1 { grid-template-columns: repeat(2, minmax(0, 1fr)); }
        .update-grid .whatsnew { grid-column: 1 / -1; }
        .update-grid.n0 { grid-template-columns: minmax(0, 1fr); }
        .search { width: 230px; }
        .lib-cols, .si-wrap, .sd-cols, .view-about, .accent-row { flex-direction: column; align-items: stretch; }
        .glance, .what-syncs, .how, .about-side, .preview-card { width: auto; }
        .what-syncs { margin-top: 0; }
        .glance-grid { grid-template-columns: repeat(4, minmax(0, 1fr)); }
        .view-settings, .si-wrap { padding-left: 32px; padding-right: calc(32px + env(safe-area-inset-right)); padding-top: calc(32px + env(safe-area-inset-top)); }
        .sd-wrap { padding-left: 32px; padding-right: calc(32px + env(safe-area-inset-right)); padding-top: calc(32px + env(safe-area-inset-top)); }
        .si-form { max-width: none; }
        .copyright { margin-top: 0; }
        .view-sync { padding: 0; }
    }

    @media (max-width: 760px) {
        .app { flex-direction: column; }
        .side { display: none; }

        .topbar {
            display: flex; align-items: center; justify-content: space-between; gap: 12px;
            position: sticky; top: 0; z-index: 20;
            padding: calc(12px + env(safe-area-inset-top)) calc(16px + env(safe-area-inset-right)) 12px calc(16px + env(safe-area-inset-left));
            background: var(--side); border-bottom: 1px solid var(--side-line);
        }
        .tabs {
            display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 2px;
            margin: 14px 16px 0; padding: 3px; border-radius: 11px;
            background: var(--seg);
        }
        .tab {
            height: 38px; border: 0; border-radius: 8px;
            background: transparent; color: var(--seg-off);
            font-size: 14px; font-weight: 600;
            display: flex; align-items: center; justify-content: center; gap: 6px;
        }
        .tab[aria-current="page"] { background: var(--seg-on); box-shadow: var(--seg-on-shadow); color: var(--ink); font-weight: 700; }
        .tab .nav-badge { min-width: 20px; height: 20px; padding: 0 6px; font-size: 11px; }

        .view { min-height: 0; }
        .view-discover, .view-favorites, .view-library {
            padding: 18px calc(16px + env(safe-area-inset-right)) calc(28px + env(safe-area-inset-bottom)) calc(16px + env(safe-area-inset-left));
        }
        .h1 { font-size: 32px; }
        .page-head { flex-direction: column; align-items: stretch; gap: 14px; }
        .head-tools .search { flex: 1; width: auto; }

        .cat-strip {
            display: flex; gap: 8px; overflow-x: auto;
            margin: 0 -16px; padding: 0 16px;
            scrollbar-width: none;
        }
        .cat-strip::-webkit-scrollbar { display: none; }
        .cat-chip {
            flex-shrink: 0;
            display: flex; align-items: center; gap: 8px;
            height: 38px; padding: 0 13px;
            border-radius: 10px; border: 1px solid var(--card-line);
            background: var(--card); color: var(--ink-2);
            font-size: 14px; font-weight: 500; white-space: nowrap;
        }
        .cat-chip[aria-pressed="true"] { background: var(--ink-btn); border-color: var(--ink-btn); color: var(--ink-btn-fg); font-weight: 600; }
        .cat-chip .cat-count { color: inherit; opacity: 0.7; }

        .update-grid, .update-grid.n1, .update-grid.n0 { grid-template-columns: minmax(0, 1fr); }
        .list { padding: 2px 14px; }
        .row { gap: 11px; }
        .row-act { width: auto; }
        .fav-empty { padding: 40px 0; }
        .glance-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
        .upd-card { flex-wrap: wrap; }

        .panel {
            top: calc(48px + env(safe-area-inset-top)); left: 0; right: 0; bottom: 0;
            width: auto; max-width: none;
            border-radius: 22px 22px 0 0;
            transform: translateY(100%);
        }
        .p-head { padding: 16px 16px 0 22px; }
        .p-body { padding: 10px 22px calc(28px + env(safe-area-inset-bottom)); }
        .p-name { font-size: 24px; }
        .alert { padding: 22px; }

        .side-settings {
            display: flex; position: static;
            width: auto; height: auto; overflow: visible;
            gap: 10px; border-right: 0; border-bottom: 1px solid var(--side-line);
            padding: calc(12px + env(safe-area-inset-top)) calc(16px + env(safe-area-inset-right)) 14px calc(16px + env(safe-area-inset-left));
        }
        .set-title { font-size: 26px; }
        .set-items { flex-direction: row; gap: 6px; overflow-x: auto; margin: 0 -16px; padding: 0 16px; scrollbar-width: none; }
        .set-items::-webkit-scrollbar { display: none; }
        .set-item { flex-shrink: 0; }
        .view-settings, .si-wrap, .sd-wrap {
            padding: 22px calc(16px + env(safe-area-inset-right)) calc(32px + env(safe-area-inset-bottom)) calc(16px + env(safe-area-inset-left));
        }
        .set-head h2, .sd-head h2, .si-head h2, .about-titles h2 { font-size: 28px; }
        .theme-grid { grid-template-columns: minmax(0, 1fr); }
        .about-top { gap: 16px; }
        .about-logo { width: 72px; height: 72px; border-radius: 19px; }
        .code-wrap { padding: 22px 16px; }
        .code-card { padding: 28px 18px 22px; }
        .digits { gap: 8px; width: 100%; }
        .digit { flex: 1; width: auto; min-width: 0; height: 60px; font-size: 24px; }
        .sd-head { flex-direction: column; align-items: flex-start; }
        .status-pill { max-width: 100%; }
        .acct-top { flex-wrap: wrap; }
        .btn-sync { width: 100%; }
        .stats { grid-template-columns: minmax(0, 1fr); }
        .bk-row { flex-wrap: wrap; padding: 10px 0; }
        .view-sync { padding: 0; }
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
        o.setAttribute('role', 'alertdialog');
        o.setAttribute('aria-labelledby', 'gateLockTitle');
        o.style.cssText = 'position:fixed;inset:0;z-index:2147483000;display:flex;align-items:center;justify-content:center;padding:24px;background:#111114;color:#F2F1EE;font-family:Figtree,-apple-system,system-ui,sans-serif';
        o.innerHTML =
            '<section style="width:440px;max-width:100%;display:flex;flex-direction:column;gap:22px;padding:34px;box-sizing:border-box;border-radius:24px;background:#1B1B20;border:1px solid #2A2A31">' +
            '<span style="font-family:\'JetBrains Mono\',ui-monospace,monospace;font-size:11px;font-weight:600;letter-spacing:0.08em;color:#9C9CA6">IDENTITY CHECK UNAVAILABLE</span>' +
            '<div style="width:64px;height:64px;border-radius:17px;background:#2A2A31;display:flex;align-items:center;justify-content:center"><svg width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="#F08A65" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="4" y="10.5" width="16" height="10.5" rx="2.5"/><path d="M8 10.5V7a4 4 0 0 1 8 0v3.5M12 14.5v3"/></svg></div>' +
            '<div style="display:flex;flex-direction:column;gap:8px"><h2 id="gateLockTitle" style="margin:0;font-family:\'Bricolage Grotesque\',-apple-system,system-ui,sans-serif;font-weight:800;font-size:28px;letter-spacing:-0.025em;line-height:1.1">Can\'t verify this iPad</h2>' +
            '<p style="margin:0;font-size:15px;line-height:1.55;color:#B6B6BF">' + p + ' couldn\'t load the AbelDeviceID check, so it\'s staying locked. Check your connection and try again.</p></div>' +
            '<button type="button" style="height:52px;border-radius:13px;border:1px solid #3A3A42;background:#24242A;color:#F2F1EE;font:inherit;font-size:16px;font-weight:700;display:flex;align-items:center;justify-content:center;gap:8px;cursor:pointer"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M21 12a9 9 0 1 1-2.6-6.4M21 3v6h-6"/></svg>Try again</button>' +
            '</section>';
        o.querySelector('button').addEventListener('click', function () { location.reload(); });
        (document.body || document.documentElement).appendChild(o);
    }
    if (document.body) block(); else window.addEventListener('DOMContentLoaded', block);
})('Abel Tools');</script>
</head>
<body>
<div class="app">

    <!-- Phone width: the sidebar folds into this header and tab strip -->
    <header class="topbar" id="topbar">
        <div class="brand">
            <div class="brand-tile"><svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.8-3.8a6 6 0 0 1-8 8l-6.9 6.9a2.1 2.1 0 0 1-3-3L10.7 10a6 6 0 0 1 8-8l-4 4Z"/></svg></div>
            <div class="brand-text">
                <span class="brand-name">Abel Tools</span>
                <span class="brand-ver" data-fill="installer">Installer &middot; v&hellip;</span>
            </div>
        </div>
        <button class="icon-btn" id="topSettings" type="button" aria-label="Settings">
            <svg width="19" height="19" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.7 1.7 0 0 0 .3 1.8l.1.1a2 2 0 1 1-2.8 2.8l-.1-.1a1.7 1.7 0 0 0-1.8-.3 1.7 1.7 0 0 0-1 1.5V21a2 2 0 1 1-4 0v-.1a1.7 1.7 0 0 0-1.1-1.5 1.7 1.7 0 0 0-1.8.3l-.1.1a2 2 0 1 1-2.8-2.8l.1-.1a1.7 1.7 0 0 0 .3-1.8 1.7 1.7 0 0 0-1.5-1H3a2 2 0 1 1 0-4h.1a1.7 1.7 0 0 0 1.5-1.1 1.7 1.7 0 0 0-.3-1.8l-.1-.1a2 2 0 1 1 2.8-2.8l.1.1a1.7 1.7 0 0 0 1.8.3H9a1.7 1.7 0 0 0 1-1.5V3a2 2 0 1 1 4 0v.1a1.7 1.7 0 0 0 1 1.5 1.7 1.7 0 0 0 1.8-.3l.1-.1a2 2 0 1 1 2.8 2.8l-.1.1a1.7 1.7 0 0 0-.3 1.8V9a1.7 1.7 0 0 0 1.5 1H21a2 2 0 1 1 0 4h-.1a1.7 1.7 0 0 0-1.5 1Z"/></svg>
        </button>
    </header>
    <nav class="tabs" id="tabs" aria-label="Main">
        <button class="tab" type="button" data-go="discover">Discover</button>
        <button class="tab" type="button" data-go="favorites">Favorites <span class="nav-count" data-fill="favcount"></span></button>
        <button class="tab" type="button" data-go="library">Library <span class="nav-badge" data-fill="updbadge" hidden></span></button>
    </nav>

    <!-- Sidebar -->
    <nav class="side" id="mainSide" aria-label="Main">
        <div class="brand">
            <div class="brand-tile"><svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.8-3.8a6 6 0 0 1-8 8l-6.9 6.9a2.1 2.1 0 0 1-3-3L10.7 10a6 6 0 0 1 8-8l-4 4Z"/></svg></div>
            <div class="brand-text">
                <span class="brand-name">Abel Tools</span>
                <span class="brand-ver" data-fill="installer">Installer &middot; v&hellip;</span>
            </div>
        </div>

        <div class="nav-group">
            <button class="nav-btn" type="button" data-go="discover">
                <svg width="19" height="19" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="12" cy="12" r="9"/><path d="m15.5 8.5-2 5-5 2 2-5z"/></svg>
                <span class="lbl">Discover</span>
            </button>
            <button class="nav-btn" type="button" data-go="favorites">
                <svg width="19" height="19" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linejoin="round" aria-hidden="true"><path d="M12 2.6 14.3 8.9 20.9 9.1 15.7 13.2 17.5 19.6 12 15.9 6.5 19.6 8.3 13.2 3.1 9.1 9.7 8.9Z"/></svg>
                <span class="lbl">Favorites</span>
                <span class="nav-count" data-fill="favcount"></span>
            </button>
            <button class="nav-btn" type="button" data-go="library">
                <svg width="19" height="19" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M4 4h4v16H4zM10 4h4v16h-4zM16.5 4.5l3.8 1 -3.9 15.4-3.8-1z"/></svg>
                <span class="lbl">Library</span>
                <span class="nav-badge" data-fill="updbadge" hidden></span>
            </button>
        </div>

        <div class="cats" id="catGroup" hidden>
            <span class="side-label">CATEGORIES</span>
            <div class="cats" id="catList"></div>
        </div>

        <div class="side-foot">
            <button class="sync-card" id="syncCard" type="button">
                <span class="sync-avatar" id="syncAvatar"></span>
                <span class="sync-text">
                    <span class="sync-title" id="syncTitle">Sign in to Sync</span>
                    <span class="sync-sub" id="syncSub">Favorites on every iPad</span>
                </span>
            </button>
            <button class="nav-btn" id="settingsBtn" type="button">
                <svg width="19" height="19" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.7 1.7 0 0 0 .3 1.8l.1.1a2 2 0 1 1-2.8 2.8l-.1-.1a1.7 1.7 0 0 0-1.8-.3 1.7 1.7 0 0 0-1 1.5V21a2 2 0 1 1-4 0v-.1a1.7 1.7 0 0 0-1.1-1.5 1.7 1.7 0 0 0-1.8.3l-.1.1a2 2 0 1 1-2.8-2.8l.1-.1a1.7 1.7 0 0 0 .3-1.8 1.7 1.7 0 0 0-1.5-1H3a2 2 0 1 1 0-4h.1a1.7 1.7 0 0 0 1.5-1.1 1.7 1.7 0 0 0-.3-1.8l-.1-.1a2 2 0 1 1 2.8-2.8l.1.1a1.7 1.7 0 0 0 1.8.3H9a1.7 1.7 0 0 0 1-1.5V3a2 2 0 1 1 4 0v.1a1.7 1.7 0 0 0 1 1.5 1.7 1.7 0 0 0 1.8-.3l.1-.1a2 2 0 1 1 2.8 2.8l-.1.1a1.7 1.7 0 0 0-.3 1.8V9a1.7 1.7 0 0 0 1.5 1H21a2 2 0 1 1 0 4h-.1a1.7 1.7 0 0 0-1.5 1Z"/></svg>
                <span class="lbl">Settings</span>
            </button>
        </div>
    </nav>

    <!-- Settings sidebar -->
    <nav class="side side-settings" id="setSide" aria-label="Settings" hidden>
        <button class="back-btn" id="setBack" type="button">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="m15 18-6-6 6-6"/></svg>
            <span id="setBackLabel">Discover</span>
        </button>
        <h1 class="set-title">Settings</h1>
        <div class="set-items">
            <button class="set-item" type="button" data-page="sync">
                <span class="set-tile t-brand"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M21 12a9 9 0 0 1-15.5 6.2M3 12a9 9 0 0 1 15.5-6.2M18.5 2v4h-4M5.5 22v-4h4"/></svg></span>
                <span class="set-text"><span class="set-name">Account &amp; Sync</span><span class="set-sub" id="setSyncSub">Not signed in</span></span>
            </button>
            <button class="set-item" type="button" data-page="appearance">
                <span class="set-tile t-accent"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 22a10 10 0 1 1 10-10c0 2.8-2.2 5-5 5h-1.8a2 2 0 0 0-1.5 3.3l.2.2a2 2 0 0 1-1.4 3.3z"/></svg></span>
                <span class="set-text"><span class="set-name">Appearance</span><span class="set-sub" data-fill="look">Auto &middot; Blue</span></span>
            </button>
            <button class="set-item" type="button" data-page="about">
                <span class="set-tile t-gray"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" aria-hidden="true"><circle cx="12" cy="12" r="9"/><path d="M12 11v5M12 8h.01"/></svg></span>
                <span class="set-text"><span class="set-name">About</span><span class="set-sub" data-fill="version">Version &hellip;</span></span>
            </button>
        </div>
    </nav>

    <!-- ================= Discover ================= -->
    <main class="view view-discover" id="viewDiscover">
        <header class="page-head">
            <div class="head-titles">
                <span class="eyebrow" id="dateEyebrow"></span>
                <h1 class="h1" id="discoverTitle">Discover</h1>
            </div>
            <div class="head-tools">
                <label class="search">
                    <svg width="17" height="17" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><circle cx="11" cy="11" r="7.5"/><path d="m20.5 20.5-4.2-4.2"/></svg>
                    <input id="searchInput" type="search" placeholder="Search shortcuts" aria-label="Search shortcuts" autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false">
                </label>
                <button class="icon-btn" id="themeBtn" type="button" aria-label="Switch to dark mode">
                    <svg id="themeIcon" width="19" height="19" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"></svg>
                </button>
            </div>
        </header>

        <div class="cat-strip" id="catStrip" role="group" aria-label="Categories"></div>

        <div class="notice" id="notice" role="status" hidden>
            <span class="notice-tag">NOTICE</span>
            <span class="notice-text" id="noticeText"></span>
            <button class="notice-x" id="noticeClose" type="button" aria-label="Dismiss announcement">
                <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" aria-hidden="true"><path d="M18 6 6 18M6 6l12 12"/></svg>
            </button>
        </div>

        <section class="update-grid n0" id="updateGrid" aria-label="This update">
            <div class="card whatsnew">
                <div class="wn-head">
                    <span class="mono-label">WHAT'S NEW</span>
                    <span class="wn-ver" data-fill="vtag"></span>
                </div>
                <ul class="wn-list" id="wnList"><li><span>Loading changelog&hellip;</span></li></ul>
                <span class="wn-foot">Everything installs as a normal Apple Shortcut.</span>
            </div>
        </section>

        <section class="all" aria-labelledby="listTitle">
            <div class="list-head">
                <div class="list-title">
                    <h2 id="listTitle">All shortcuts</h2>
                    <span class="mono-count" id="listCount"></span>
                </div>
                <div class="seg" id="sortSeg" role="group" aria-label="Sort">
                    <button class="seg-btn" type="button" data-sort="0" aria-pressed="true">Featured</button>
                    <button class="seg-btn" type="button" data-sort="1" aria-pressed="false">A&ndash;Z</button>
                    <button class="seg-btn" type="button" data-sort="2" aria-pressed="false">Category</button>
                </div>
            </div>
            <div class="list" id="list" aria-busy="true">
                <div class="row" aria-hidden="true"><div class="sk sk-tile"></div><div class="sk-lines"><div class="sk sk-l1"></div><div class="sk sk-l2"></div></div><div class="sk sk-btn"></div></div>
                <div class="row" aria-hidden="true"><div class="sk sk-tile"></div><div class="sk-lines"><div class="sk sk-l1"></div><div class="sk sk-l2"></div></div><div class="sk sk-btn"></div></div>
                <div class="row" aria-hidden="true"><div class="sk sk-tile"></div><div class="sk-lines"><div class="sk sk-l1"></div><div class="sk sk-l2"></div></div><div class="sk sk-btn"></div></div>
                <div class="row" aria-hidden="true"><div class="sk sk-tile"></div><div class="sk-lines"><div class="sk sk-l1"></div><div class="sk sk-l2"></div></div><div class="sk sk-btn"></div></div>
                <div class="row" aria-hidden="true"><div class="sk sk-tile"></div><div class="sk-lines"><div class="sk sk-l1"></div><div class="sk sk-l2"></div></div><div class="sk sk-btn"></div></div>
                <div class="row" aria-hidden="true"><div class="sk sk-tile"></div><div class="sk-lines"><div class="sk sk-l1"></div><div class="sk sk-l2"></div></div><div class="sk sk-btn"></div></div>
            </div>
            <div class="card list-empty" id="listEmpty" hidden>
                <strong>No results</strong>
                <p>Try a different search or category.</p>
                <button class="btn-2" id="emptyClear" type="button">Clear filters</button>
            </div>
        </section>
    </main>

    <!-- ================= Favorites ================= -->
    <main class="view view-favorites" id="viewFavorites" hidden>
        <div class="fav-headline">
            <h1 class="h1">Favorites</h1>
            <span class="mono-count" id="favHeadCount"></span>
        </div>

        <div class="fav-empty" id="favEmpty">
            <div class="fav-art" aria-hidden="true">
                <div class="ghost-l"></div>
                <div class="ghost-r"></div>
                <div class="hero">
                    <svg width="42" height="42" viewBox="0 0 24 24" fill="currentColor" stroke="currentColor" stroke-width="1.6" stroke-linejoin="round"><path d="M12 2.6 14.3 8.9 20.9 9.1 15.7 13.2 17.5 19.6 12 15.9 6.5 19.6 8.3 13.2 3.1 9.1 9.7 8.9Z"/></svg>
                </div>
            </div>
            <div class="fav-copy">
                <h2>No favorites yet</h2>
                <p>Tap the star on any shortcut and it lands here, so the tools you reach for are one tap away.</p>
            </div>
            <div class="fav-btns">
                <button class="btn-ink" type="button" data-go="discover">Browse shortcuts</button>
                <button class="btn-2" type="button" data-settings="sync">Restore from Sync</button>
            </div>
        </div>

        <section class="fav-full" id="favFull" aria-label="Your favorites" hidden>
            <div class="list" id="favList"></div>
        </section>

        <div class="hint" id="favHint">
            <svg width="17" height="17" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M21 12a9 9 0 0 1-15.5 6.2M3 12a9 9 0 0 1 15.5-6.2M18.5 2v4h-4M5.5 22v-4h4"/></svg>
            Signed in? Favorites, theme and accent follow you to every iPad.
        </div>
    </main>

    <!-- ================= Library ================= -->
    <main class="view view-library" id="viewLibrary" hidden>
        <header class="lib-head">
            <h1 class="h1">Library</h1>
            <p>Abel Tools shortcuts on this iPad, as reported when the installer opened.</p>
        </header>

        <div class="lib-cols">
            <div class="lib-main">
                <section class="lib-sec" id="libUpdates" aria-labelledby="updHead">
                    <h2 class="lib-h2" id="updHead">Updates <span id="libUpdCount"></span></h2>
                    <div class="lib-sec" id="libUpdList"></div>
                </section>
                <section class="lib-sec" id="libInstalled" aria-labelledby="instHead">
                    <h2 class="lib-h2" id="instHead">Installed <span id="libInstCount"></span></h2>
                    <div class="inst-list" id="libInstList"></div>
                </section>
                <section class="lib-sec" id="libRetired" aria-labelledby="retHead">
                    <h2 class="lib-h2" id="retHead">Retired <span id="libRetCount"></span></h2>
                    <div class="lib-sec" id="libRetList"></div>
                </section>
                <div class="card lib-empty" id="libEmpty" hidden>
                    <strong>Nothing installed yet</strong>
                    <p>Shortcuts you install with Abel Tools show up here, along with any updates waiting for them.</p>
                    <button class="btn-ink" type="button" data-go="discover">Browse shortcuts</button>
                </div>
            </div>

            <aside class="glance" aria-label="At a glance">
                <span class="glance-label">AT A GLANCE</span>
                <div class="glance-grid">
                    <div class="glance-stat"><span class="glance-num" id="glInstalled">0</span><span class="glance-cap">installed</span></div>
                    <div class="glance-stat"><span class="glance-num" id="glUpdates">0</span><span class="glance-cap" id="glUpdatesCap">updates ready</span></div>
                    <div class="glance-stat"><span class="glance-num" id="glMissing">0</span><span class="glance-cap">not installed</span></div>
                    <div class="glance-stat"><span class="glance-num" id="glFavs">0</span><span class="glance-cap" id="glFavsCap">favorites</span></div>
                </div>
                <p>Every tool installs as a normal Apple Shortcut, so removing one happens in the Shortcuts app.</p>
                <button class="btn-lime" id="glBrowse" type="button" data-go="discover">Browse all</button>
            </aside>
        </div>
    </main>

    <!-- ================= Settings: Account & Sync ================= -->
    <main class="view view-settings view-sync" id="pageSync" hidden>

        <div class="si-wrap" id="syncSignIn">
            <div class="si-main">
                <header class="si-head">
                    <h2>Abel Tools Sync</h2>
                    <p>Keep your favorites and look on every iPad you use Abel Tools on. Your shortcuts stay exactly where they are.</p>
                </header>
                <form class="si-form" id="acctForm" novalidate>
                    <div class="seg2" role="group" aria-label="Account mode">
                        <button type="button" id="modeSignIn" aria-pressed="true">Sign in</button>
                        <button type="button" id="modeSignUp" aria-pressed="false">Create account</button>
                    </div>
                    <div class="field">
                        <label for="acctEmail">Email</label>
                        <input class="input" id="acctEmail" type="email" autocomplete="username" inputmode="email" autocapitalize="none" autocorrect="off" spellcheck="false" required>
                    </div>
                    <div class="field">
                        <label for="acctPassword">Password</label>
                        <div class="pw-wrap">
                            <input class="input" id="acctPassword" type="password" autocomplete="current-password" required>
                            <button class="pw-show" id="pwShow" type="button" aria-pressed="false" aria-label="Show password">Show</button>
                        </div>
                    </div>
                    <button class="btn-primary" id="acctSubmit" type="submit">Sign in</button>
                    <p class="form-msg" id="signInMsg" role="status" hidden></p>
                    <p class="si-note">
                        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><circle cx="12" cy="12" r="9"/><path d="M12 11v5M12 8h.01"/></svg>
                        The Shortcuts app keeps its own sign in, so signing in on achenkunju.com in Safari doesn't carry over here.
                    </p>
                </form>
            </div>

            <aside class="what-syncs" aria-label="What syncs">
                <span class="ws-label">WHAT SYNCS</span>
                <div class="ws-row">
                    <span class="ws-ic"><svg width="17" height="17" viewBox="0 0 24 24" fill="currentColor" stroke="currentColor" stroke-width="1.6" stroke-linejoin="round" aria-hidden="true"><path d="M12 2.6 14.3 8.9 20.9 9.1 15.7 13.2 17.5 19.6 12 15.9 6.5 19.6 8.3 13.2 3.1 9.1 9.7 8.9Z"/></svg></span>
                    <span class="ws-text"><span class="ws-title">Favorites</span><span class="ws-body">The first sync merges both lists, so nothing is lost.</span></span>
                </div>
                <div class="ws-row">
                    <span class="ws-ic"><svg width="17" height="17" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 22a10 10 0 1 1 10-10c0 2.8-2.2 5-5 5h-1.8a2 2 0 0 0-1.5 3.3l.2.2a2 2 0 0 1-1.4 3.3z"/></svg></span>
                    <span class="ws-text"><span class="ws-title">Theme &amp; accent</span><span class="ws-body">Pick a look once, see it everywhere.</span></span>
                </div>
                <div class="ws-row">
                    <span class="ws-ic"><svg width="17" height="17" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M2 3h20v5H2zM4 8v12h16V8M10 12h4"/></svg></span>
                    <span class="ws-text"><span class="ws-title">Backups</span><span class="ws-body">Up to 5 saved copies you can restore any time.</span></span>
                </div>
            </aside>
        </div>

        <div class="code-wrap" id="syncCode" hidden>
            <form class="code-card" id="acctMfaForm" novalidate>
                <div class="code-tile">
                    <svg width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 22s8-3.5 8-10V5l-8-3-8 3v7c0 6.5 8 10 8 10z"/><path d="m9 12 2 2 4-4"/></svg>
                </div>
                <div class="code-copy">
                    <h2>Enter your code</h2>
                    <p>Your account has two-factor sign in. Open your authenticator app and type the 6-digit code for Abel Tools.</p>
                </div>
                <fieldset class="digits">
                    <legend class="sr-only">Authentication code</legend>
                    <input class="digit" aria-label="Digit 1" inputmode="numeric" autocomplete="one-time-code" pattern="[0-9]*">
                    <input class="digit" aria-label="Digit 2" inputmode="numeric" autocomplete="off" pattern="[0-9]*">
                    <input class="digit" aria-label="Digit 3" inputmode="numeric" autocomplete="off" pattern="[0-9]*">
                    <input class="digit" aria-label="Digit 4" inputmode="numeric" autocomplete="off" pattern="[0-9]*">
                    <input class="digit" aria-label="Digit 5" inputmode="numeric" autocomplete="off" pattern="[0-9]*">
                    <input class="digit" aria-label="Digit 6" inputmode="numeric" autocomplete="off" pattern="[0-9]*">
                </fieldset>
                <button class="btn-primary" id="acctMfaSubmit" type="submit" disabled>Verify</button>
                <p class="form-msg" id="codeMsg" role="status" hidden></p>
                <button class="btn-quiet" id="acctMfaCancel" type="button">Sign in as someone else</button>
            </form>
        </div>

        <div class="sd-wrap" id="syncSignedIn" hidden>
            <header class="sd-head">
                <h2>Account &amp; Sync</h2>
                <div class="status-pill" id="syncPill" role="status" hidden></div>
            </header>
            <div class="sd-cols">
                <div class="sd-main">
                    <section class="card acct-card" aria-label="Account">
                        <div class="acct-top">
                            <span class="avatar" id="acctAvatar" aria-hidden="true"></span>
                            <div class="acct-who">
                                <span class="acct-email" id="acctWho"></span>
                                <span class="acct-sub" id="acctWhoSub">Signed in on this iPad</span>
                            </div>
                            <button class="btn-sync" id="acctSync" type="button">
                                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M21 12a9 9 0 0 1-15.5 6.2M3 12a9 9 0 0 1 15.5-6.2M18.5 2v4h-4M5.5 22v-4h4"/></svg>
                                Sync now
                            </button>
                        </div>
                        <dl class="stats">
                            <div class="stat"><dt>FAVORITES</dt><dd id="statFav">0</dd></div>
                            <div class="stat"><dt>LAST SYNCED</dt><dd id="statLast">Never</dd></div>
                            <div class="stat"><dt>LOOK</dt><dd data-fill="look">Auto &middot; Blue</dd></div>
                        </dl>
                    </section>

                    <section class="card bk-card" aria-labelledby="bkHead">
                        <div class="bk-head">
                            <h3 id="bkHead">Backups</h3>
                            <div class="bk-meter">
                                <div class="slots" id="bkSlots" aria-hidden="true"></div>
                                <span class="bk-count" id="acctBackupCount">0 of 5 slots</span>
                            </div>
                        </div>
                        <ul class="bk-list" id="backupList"></ul>
                        <p class="bk-empty" id="backupEmpty">No backups yet. Back up now to keep a copy of your favorites and look that syncing can never take away.</p>
                        <div class="bk-foot">
                            <button class="btn-add" id="acctBackup" type="button">
                                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" aria-hidden="true"><path d="M12 5v14M5 12h14"/></svg>
                                <span id="acctBackupLabel">Back up now</span>
                            </button>
                            <button class="btn-quiet" id="acctSignOut" type="button">Sign out of this device</button>
                        </div>
                    </section>
                </div>

                <aside class="how" aria-label="How backups work">
                    <span class="mono-label">HOW BACKUPS WORK</span>
                    <p>A backup is a saved copy of your favorites and look. Syncing never touches it, only you can restore or remove one.</p>
                    <p>Restoring replaces this iPad's favorites and look, then saves them to your account so other iPads follow.</p>
                    <p>Signing out keeps your favorites on this iPad.</p>
                </aside>
            </div>
        </div>
    </main>

    <!-- ================= Settings: Appearance ================= -->
    <main class="view view-settings view-appearance" id="pageAppearance" hidden>
        <header class="set-head">
            <h2>Appearance</h2>
            <p>Your look syncs with your favorites when you're signed in.</p>
        </header>

        <section class="set-sec" aria-labelledby="themeHead">
            <h3 class="sec-label" id="themeHead">THEME</h3>
            <div class="theme-grid" id="modeCards" role="group" aria-label="Theme">
                <button class="theme-card" type="button" data-mode="auto" aria-pressed="false">
                    <span class="tc-preview" aria-hidden="true" style="border: 1px solid #E6E2D9">
                        <span style="flex: 1; background: #F4F2ED"><span style="width: 34%; background: #ECE9E2"></span><span style="flex: 1; flex-direction: column; gap: 6px; padding: 10px"><span style="height: 8px; width: 60%; border-radius: 3px; background: #17171B"></span><span style="height: 22px; border-radius: 5px; background: #FFFFFF"></span><span style="height: 22px; border-radius: 5px; background: #FFFFFF"></span></span></span>
                        <span style="flex: 1; background: #111114"><span style="width: 34%; background: #16161A"></span><span style="flex: 1; flex-direction: column; gap: 6px; padding: 10px"><span style="height: 8px; width: 60%; border-radius: 3px; background: #F2F1EE"></span><span style="height: 22px; border-radius: 5px; background: #1B1B20"></span><span style="height: 22px; border-radius: 5px; background: #1B1B20"></span></span></span>
                    </span>
                    <span class="tc-row">
                        <span class="tc-text"><span class="tc-name">Auto</span><span class="tc-sub">Follows your iPad</span></span>
                        <span class="radio"></span>
                    </span>
                </button>
                <button class="theme-card" type="button" data-mode="light" aria-pressed="false">
                    <span class="tc-preview" aria-hidden="true" style="border: 1px solid #E6E2D9; background: #F4F2ED"><span style="width: 34%; background: #ECE9E2"></span><span style="flex: 1; flex-direction: column; gap: 6px; padding: 10px"><span style="height: 8px; width: 50%; border-radius: 3px; background: #17171B"></span><span style="height: 22px; border-radius: 5px; background: #FFFFFF"></span><span style="height: 22px; border-radius: 5px; background: #FFFFFF"></span><span style="height: 22px; border-radius: 5px; background: #FFFFFF"></span></span></span>
                    <span class="tc-row">
                        <span class="tc-text"><span class="tc-name">Light</span><span class="tc-sub">Paper and ink</span></span>
                        <span class="radio"></span>
                    </span>
                </button>
                <button class="theme-card" type="button" data-mode="dark" aria-pressed="false">
                    <span class="tc-preview" aria-hidden="true" style="border: 1px solid #2A2A31; background: #111114"><span style="width: 34%; background: #16161A"></span><span style="flex: 1; flex-direction: column; gap: 6px; padding: 10px"><span style="height: 8px; width: 50%; border-radius: 3px; background: #F2F1EE"></span><span style="height: 22px; border-radius: 5px; background: #1B1B20"></span><span style="height: 22px; border-radius: 5px; background: #1B1B20"></span><span style="height: 22px; border-radius: 5px; background: #1B1B20"></span></span></span>
                    <span class="tc-row">
                        <span class="tc-text"><span class="tc-name">Dark</span><span class="tc-sub">Easy at night</span></span>
                        <span class="radio"></span>
                    </span>
                </button>
            </div>
        </section>

        <section class="set-sec" aria-labelledby="accHead">
            <h3 class="sec-label" id="accHead">ACCENT COLOR</h3>
            <div class="accent-row">
                <div class="swatch-grid" id="swatches" role="group" aria-label="Accent color"></div>
                <div class="preview-card">
                    <span class="pv-label">PREVIEW</span>
                    <div class="pv-row">
                        <div id="pvTile"></div>
                        <span class="pv-name">Quickscreen</span>
                        <svg width="19" height="19" viewBox="0 0 24 24" fill="currentColor" stroke="currentColor" stroke-width="1.8" stroke-linejoin="round" aria-hidden="true"><path d="M12 2.6 14.3 8.9 20.9 9.1 15.7 13.2 17.5 19.6 12 15.9 6.5 19.6 8.3 13.2 3.1 9.1 9.7 8.9Z"/></svg>
                    </div>
                    <div class="pv-btns" aria-hidden="true"><span class="pv-get">Get</span><span class="pv-upd">Update</span></div>
                    <span class="pv-note">Buttons, stars, the selected tab and badges take the accent. Everything else stays ink.</span>
                </div>
            </div>
        </section>
    </main>

    <!-- ================= Settings: About ================= -->
    <main class="view view-settings view-about" id="pageAbout" hidden>
        <div class="about-main">
            <div class="about-top">
                <div class="about-logo">
                    <svg width="46" height="46" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.8-3.8a6 6 0 0 1-8 8l-6.9 6.9a2.1 2.1 0 0 1-3-3L10.7 10a6 6 0 0 1 8-8l-4 4Z"/></svg>
                </div>
                <div class="about-titles">
                    <h2>Abel Tools Installer</h2>
                    <span class="about-ver"><span data-fill="version">Version &hellip;</span> &middot; Shortcut installer for iPad</span>
                </div>
            </div>

            <p class="about-p">Abel Tools is a collection of Apple Shortcuts for iPad. This installer keeps them in one place: browse the catalog, install with one tap, and get updates as soon as they ship. Every tool installs as a normal Apple Shortcut.</p>

            <section class="card dev-card" aria-labelledby="devHead">
                <h3 class="sec-label" id="devHead">THE DEVELOPER</h3>
                <div class="dev-who">
                    <span class="dev-name">Abel Achenkunju</span>
                    <span class="dev-bio">Builds tools, shortcuts, and whatever comes next, including Abel Tools, Abel's Countdown, and a browser-based file converter.</span>
                </div>
                <div class="links">
                    <a class="link-row" href="https://achenkunju.com" target="_blank" rel="noopener noreferrer">
                        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="12" cy="12" r="9"/><path d="M3 12h18M12 3a15 15 0 0 1 0 18 15 15 0 0 1 0-18Z"/></svg>
                        <span class="lr-name">Website</span>
                        <span class="lr-host">achenkunju.com</span>
                        <svg class="lr-arrow" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M7 17 17 7M8 7h9v9"/></svg>
                    </a>
                    <a class="link-row" href="https://blog.achenkunju.com" target="_blank" rel="noopener noreferrer">
                        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"/></svg>
                        <span class="lr-name">Blog</span>
                        <span class="lr-host">blog.achenkunju.com</span>
                        <svg class="lr-arrow" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M7 17 17 7M8 7h9v9"/></svg>
                    </a>
                    <a class="link-row" href="https://github.com/therealabela" target="_blank" rel="noopener noreferrer">
                        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M9 19c-4.5 2-5-2-7-2M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5a5.4 5.4 0 0 0-1-3.5 5 5 0 0 0 0-3.5s-1 0-3 1.5a10.4 10.4 0 0 0-8 0C5 2 4 2 4 2a5 5 0 0 0 0 3.5A5.4 5.4 0 0 0 3 9c0 3.5 3 5.5 6 5.5-.4.5-.7 1-.8 1.7-.2.6-.2 1.2-.2 1.8v4"/></svg>
                        <span class="lr-name">GitHub</span>
                        <span class="lr-host">therealabela</span>
                        <svg class="lr-arrow" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M7 17 17 7M8 7h9v9"/></svg>
                    </a>
                </div>
            </section>
        </div>

        <aside class="about-side">
            <section class="id-card" aria-labelledby="idHead">
                <h3 id="idHead">THIS IPAD</h3>
                <div class="id-block">
                    <span class="id-cap">AbelDeviceID</span>
                    <span class="id-value" id="abelIdValue">Checking&hellip;</span>
                </div>
                <span class="id-state" id="abelIdState"><i></i><span>Checking</span></span>
                <button class="id-copy" id="abelIdCopy" type="button" disabled>
                    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M9 9h11v11H9zM5 15H4V4h11v1"/></svg>
                    <span id="abelIdCopyLabel">Copy ID</span>
                </button>
                <span class="id-note">Share this when you ask for help with Abel Tools.</span>
            </section>
            <p class="copyright">&copy; 2026 Abel Tools Installer by Abel Achenkunju. All rights reserved.</p>
        </aside>
    </main>
</div>

<!-- ================= Shortcut detail ================= -->
<div class="scrim" id="sheetScrim"></div>
<section class="panel" id="sheet" role="dialog" aria-modal="true" aria-labelledby="sheetName" tabindex="-1">
    <div class="p-head">
        <span class="chip" id="sheetChip"><span class="cat-dot"></span><span id="sheetChipText"></span></span>
        <button class="close-btn" id="sheetClose" type="button" aria-label="Close">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" aria-hidden="true"><path d="M18 6 6 18M6 6l12 12"/></svg>
        </button>
    </div>
    <div class="p-body" id="sheetBody"></div>
</section>

<!-- ================= Install confirm ================= -->
<div class="scrim alert-scrim" id="alertScrim"></div>
<div class="alert-wrap">
    <section class="alert" id="alert" role="alertdialog" aria-modal="true" aria-labelledby="alertTitle" aria-describedby="alertMsg">
        <div class="al-head">
            <div id="alertIcon"></div>
            <div class="al-titles">
                <h2 class="al-title" id="alertTitle"></h2>
                <p class="al-msg" id="alertMsg">It opens in the Shortcuts app to finish.</p>
            </div>
        </div>
        <ol class="steps">
            <li><span class="step-n">1</span>Shortcuts opens with the shortcut</li>
            <li><span class="step-n">2</span>Tap <strong>Add Shortcut</strong></li>
            <li><span class="step-n">3</span>Come back here for the rest</li>
        </ol>
        <div class="al-btns">
            <button class="btn-cancel" id="alertCancel" type="button">Cancel</button>
            <a class="btn-go" id="alertContinue" href="#">Open Shortcuts
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M7 17 17 7M8 7h9v9"/></svg>
            </a>
        </div>
    </section>
</div>

<script>
(function () {
    'use strict';

    /* ================= Runtime capability wall =================
       Backup to the server-side signed-URL gate. app.md is only usable when
       loaded same-origin under achenkunju.com in a secure context (so the
       shared AbelDeviceID module can run). If it is ever loaded some other way
       - e.g. an old string-injected/opaque-origin web view, or a saved copy -
       show a short "get the shortcut" message instead of a broken installer. */
    var SHORTCUT_LINK = 'https://www.icloud.com/shortcuts/5ef518ebbbca40039df5325b264e9fb0';
    var isSupportedRuntime =
        location.origin === 'https://achenkunju.com' &&
        window.isSecureContext === true &&
        !!(window.crypto && window.crypto.subtle);
    if (!isSupportedRuntime) {
        document.documentElement.innerHTML =
            '<head><meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">' +
            '<link href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,800&family=Figtree:wght@400;700&family=JetBrains+Mono:wght@600&display=swap" rel="stylesheet"></head>' +
            '<body style="margin:0;min-height:100vh;display:flex;align-items:center;justify-content:center;padding:24px;box-sizing:border-box;' +
            'background:#111114;color:#F2F1EE;font-family:Figtree,-apple-system,system-ui,sans-serif">' +
            '<section style="width:440px;max-width:100%;display:flex;flex-direction:column;gap:22px;padding:34px;box-sizing:border-box;border-radius:24px;background:#1B1B20;border:1px solid #2A2A31">' +
            '<span style="font-family:\'JetBrains Mono\',ui-monospace,monospace;font-size:11px;font-weight:600;letter-spacing:0.08em;color:#9C9CA6">OPENED OUTSIDE THE SHORTCUT</span>' +
            '<div style="width:64px;height:64px;border-radius:17px;background:#CDEB52;display:flex;align-items:center;justify-content:center"><svg width="30" height="30" viewBox="0 0 24 24" fill="none" stroke="#17171B" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.8-3.8a6 6 0 0 1-8 8l-6.9 6.9a2.1 2.1 0 0 1-3-3L10.7 10a6 6 0 0 1 8-8l-4 4Z"/></svg></div>' +
            '<div style="display:flex;flex-direction:column;gap:8px"><h1 style="margin:0;font-family:\'Bricolage Grotesque\',-apple-system,system-ui,sans-serif;font-weight:800;font-size:28px;letter-spacing:-0.025em;line-height:1.1">Open this in the Abel Tools Installer</h1>' +
            '<p style="margin:0;font-size:15px;line-height:1.55;color:#B6B6BF">The installer runs from its shortcut. Run it from the Shortcuts app, or add it first if you don\'t have it yet.</p></div>' +
            '<a href="' + SHORTCUT_LINK + '" style="height:52px;border-radius:13px;background:#8090FF;color:#0C0F2B;font-size:16px;font-weight:700;text-decoration:none;display:flex;align-items:center;justify-content:center;gap:8px">Get the installer shortcut' +
            '<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M7 17 17 7M8 7h9v9"/></svg></a>' +
            '</section></body>';
        return;
    }

    /* ================= Configuration ================= */

    var RAW_BASE = 'https://raw.githubusercontent.com/therealabela/abel_tools_datarepo/refs/heads/main/';
    var API_BASE = 'https://achenkunju.com/api/';
    var params = new URLSearchParams(location.search);
    var SELF_NAME = params.get('self') || 'Abel Tools Installer';

    function $(id) { return document.getElementById(id); }

    function el(tag, className, text) {
        var node = document.createElement(tag);
        if (className) node.className = className;
        if (text) node.textContent = text;
        return node;
    }

    /* ================= Icons =================
       Interface icons and the shortcut glyphs, all stroke paths on a 24 grid
       as drawn in the redesign. Tiles are a flat color with a white glyph. */

    var ICONS = {
        check: '<path d="M20 6 9 17l-5-5"/>',
        x: '<path d="M18 6 6 18M6 6l12 12"/>',
        moon: '<path d="M21 12.8A9 9 0 1 1 11.2 3a7 7 0 0 0 9.8 9.8Z"/>',
        sun: '<circle cx="12" cy="12" r="4"/><path d="M12 2v2M12 20v2M4.9 4.9l1.4 1.4M17.7 17.7l1.4 1.4M2 12h2M20 12h2M4.9 19.1l1.4-1.4M17.7 6.3l1.4-1.4"/>',
        download: '<path d="M12 4v11M7 10l5 5 5-5M5 20h14"/>',
        user: '<path d="M19 21v-2a4 4 0 0 0-4-4H9a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/>',
        archive: '<path d="M2 3h20v5H2zM4 8v12h16V8M10 12h4"/>',
        alert: '<circle cx="12" cy="12" r="9"/><path d="M12 7.5v5.5M12 16.5h.01"/>'
    };

    var STAR_PATH = 'M12 2.6 14.3 8.9 20.9 9.1 15.7 13.2 17.5 19.6 12 15.9 6.5 19.6 8.3 13.2 3.1 9.1 9.7 8.9Z';

    function icon(name, size, sw) {
        return '<svg width="' + size + '" height="' + size + '" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="' +
            (sw || 2) + '" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">' + ICONS[name] + '</svg>';
    }

    function starSvg(size, filled, sw) {
        return '<svg width="' + size + '" height="' + size + '" viewBox="0 0 24 24" fill="' +
            (filled ? 'currentColor' : 'none') + '" stroke="currentColor" stroke-width="' + (sw || 1.8) + '" ' +
            'stroke-linejoin="round" aria-hidden="true"><path d="' + STAR_PATH + '"/></svg>';
    }

    var GLYPHS = {
        link: 'M9 15 15 9M11 6.5l1.8-1.8a4.6 4.6 0 0 1 6.5 6.5L17.5 13M13 17.5l-1.8 1.8a4.6 4.6 0 0 1-6.5-6.5L6.5 11',
        bolt: 'M3 8h14v8H3zM20 11v2M11 9.5 9 12h3l-2 2.5',
        battery: 'M3 8h14v8H3zM20 11v2M6.5 11v2',
        split: 'M4 5h6v14H4zM14 5h6v14h-6z',
        layers: 'M12 3 3 8l9 5 9-5-9-5zM3 13l9 5 9-5M3 17.5l9 4.5 9-4.5',
        scissors: 'M6 3.5a2.5 2.5 0 1 0 0 5a2.5 2.5 0 1 0 0-5zM6 15.5a2.5 2.5 0 1 0 0 5a2.5 2.5 0 1 0 0-5zM20 4 8 16M14.5 14.5 20 20M8 8l4 4',
        image: 'M4 4h16v16H4zM9 7.5a1.5 1.5 0 1 0 0 3a1.5 1.5 0 1 0 0-3zM20 15l-5-5L4 20',
        leaf: 'M11 20A7 7 0 0 1 9.8 6.1C15.5 5 17 4.5 19 2c1 2 2 4.2 2 8 0 5.5-4.8 10-10 10ZM2 21c0-3 1.9-5.4 5.1-6C9.5 14.5 12 13 13 12',
        sparkle: 'M12 2.5 14 9l6.5 2L14 13.5 12 20l-2-6.5L3.5 11 10 9Z',
        cube: 'M21 8 12 3 3 8v8l9 5 9-5zM3.3 7.5 12 12.5l8.7-5M12 22V12.5',
        tablet: 'M5 2.5h14v19H5zM10.5 18.5h3',
        broom: 'm13 11 8-8M13 11 5.5 13.6a2 2 0 0 0-1.3 1.5L3 21l5.9-1.2a2 2 0 0 0 1.5-1.3L13 11ZM6.5 14.5l3 3',
        terminal: 'M4 17l6-6-6-6M12 19h8',
        archive: 'M2 3h20v5H2zM4 8v12h16V8M10 12h4',
        wrench: 'M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.8-3.8a6 6 0 0 1-8 8l-6.9 6.9a2.1 2.1 0 0 1-3-3L10.7 10a6 6 0 0 1 8-8l-4 4Z'
    };

    /* ================= Real shortcut icons (embedded WebP) =================
       Downloaded from each shortcut's iCloud record and optimized. Used in
       place of the generated glyphs; ICON_TINT holds each icon's dominant
       color for accent surfaces. Unknown shortcuts fall back to a glyph. */
    var ICON_IMG = {
        "quickscreen": 'data:image/webp;base64,UklGRqADAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IAQDAAAwFQCdASp4AHgAPmEskUYkIqGhLRO5EIAMCUAZoU44Vf1Le75hj3Hk/+v+QB7Jttn5gP1k/YD3wP1A9gHoAf4DzjvYA9AD9M/Tj9lP90kiAM9xQXPNAqoV9Afjdz+6luWBWcBimXUYXkEIiwfVyfd9cwGQbpyr/FEBFHxVDQz3YWbUTljphF+3lSw7zfx7B3h7u3Umd8J5CKURrx0elQBCSjAXX61pTc3vFjPnI8UuD+oAAP7tMl//yVvXZ2vcn7k8Qf/zrkglfD/zf/IecwAAjwgZ8QjRGuU+c1uu9UOdD1ki6dFkK1rkHmRMQiaZqtX6R0KJ9OQblUHKLRLj+Pcf7+rVuDZr5ARsIya2QFpwEuOAUKAPUByeZDT/Baqrgg9vjFWgQpS6+Yjvr8s9+cQvMfEWQ55eBBk/gY518+/s+4cjAdHiQR4eTocCiqU/rhe2AlwbQSpWAKBnwoZHyGfMZULDOQGjcoCMiJGMeMii3a9QW2bNC+0Dqtfvc9dJOJUlpvseg5oNi/Kz5HdE2rXXZUeEFzyKLhr+HFJVsIVuAu241Uwvg5DBAI9K/tNq1Bi2drE3lIjBwncXDXxGkzAtbQT+HZwtC4akvfimrZnvpfPqf5gwA1Gu/7VBzKzep/h8wunB2q8m0W9GzkajFlEHzsJqzy4NSnVLCu4hXZnDb5S5UYhv6Dan6yVm7PBBDeGqoA9ELRUIJR6QqKDQnHZGT3Qje5wlFPkdPsVECK/DJuNJZ8O+MK0wP/MKM6OFrjA7AUPEET6AOKKNHgKFMbX2M6sCVnnBvJDSoAXZAUI1WU10HSnvFfr4k7fMQzMMbCE51u/xXFakPbSyFrs6x6ezIKFtTOznsbsFIrGReoznfLndev19fw30+IKqihw0CSUr9t8uzzk8Hi1S/ZEMug0Aq6S7fcfgNf1sptYvo4gxX83Wrw6SBLD/UrqWBKAu49VJUvB3Y6nH9cAZor2kJa60DisjDxkppT8bLiL1Dt5pw7tzzztKVF4Ki8monHrY7jvjkAAA',
        "anythingbutglass": 'data:image/webp;base64,UklGRggEAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IGwDAACwFACdASp4AHgAPmEwlEakIyIhKRVZCIAMCUAaGAKvsuVPJMmr6gNsP5oPOq89XfRN5mryGvFNPvf831Vn3jH8s79AVELdBQzWJcXK1w8zORo8tCWqzUTXOx+OeH5y1XbiCUBZigWNpkLKiO6aSTTWAbKufDtI29sXHZicibmJdtk0S0fmG5LfQaGs2cjVrgdipUflwSpb9tCbIXiyKM9mdqymRIvItcMU2ShV0AAA/vDiI58dCMecw5qP/+Jv0aN/TDtRmezbRngk7wOPcDq+uCdlscno7NJ4mZI2V9/dDlOxjiiLZDqh4nEdXkkiZ6H835OlH8KywNSfa79wgGpAv5EClhhzYDAY4i52Uw2YUO4r7DeLRJoJHlE5QA/HBjcvCKN88LwZ4AczjdQwnp3rOFrLs581yHiAKSEz3+cZQv97nZbEmagg90JxHKOZfWOoSpjbXNkwbJ0WbKCVIS7ZEFAEfyKpeWlIkyAX1g8SQzayvtD36dl8VbazIKNIjkmgnmEJhBO6nSvRj5Q9pTd+c8XpjLzPCqJBUOZSctxVmN5WmJffbeMtZUcUKW4oUZO3WSX9ozs1ZOmqVQY0+b1JdT58wzZzQzeNL89yR7nfgnEUO5eIQYMwTZVSmirmYHRKOAS6i4aBGBUuJme+Kczyv1SpA1HtaJOJYjo2shf81vk9fZfS0lFH4Enx7KpkPAj84iV7IopHfs6zBTuaUy+QblbKShDAgzv4vFa/yU2EHT+8irllS/H97IwUtNrYnlW3Knsu6APH64bHzDC1UF5ZkWG9B+tM6hHAGwzgXOVOair6d7WUTB3S5FJk3+QbYks3qeb9aMdrYXg9rsjff6trOz38aUrEDEg1o64WSbPACgS+Hw/k7nFILT1GvKBRet38JEWnalySyuoqOI5MCxSKzGxH/hYPu1ubSUvNv2ZxBlLwzlH7TYs5pMWfH1djfJ0QbrwNEeX0MGQsFzlMjkIBnxvlEUBCJ2t3MaBSqXwrql7ogzy89zloScSnNu9cHvt064XQDTCF2WeQZIdXL9AONDZKLaUvlV5hAuooP+t4N8ULREisMDCWuh3pdrRZ3qUfC00be6sMuLQwoK8t/LgJcwziaXz/yy/v/8gAAARBaIcFbmvoEHWbSzNh5YKnkn+UOKaJXsfn5kxwAAA=',
        "savemybattery v2.2": 'data:image/webp;base64,UklGRiAEAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IIQDAABwFgCdASp4AHgAPmEwlUekIqIhIhQJmIAMCUB2A6qQq/iBtZniOVQ6yMp+r/8/9pPsq+wDzAOdB5gP4n/cf2q94D+5f5n+V+4D0AP2Z6wD0L/2j9Nf9kvhQ/c70nHkGG63UROhRYnJIHI7mr8tbnkqK8hk4YO02CUi1Zua9+InkBETYjT9IZcex5/XbjJqgmB+QtqICUDLWJmtpf1uHN5N+46n6zMsqlaUC2AM89V1nz2yfnVVy8juaU1aoAD+zwG5JF2oNxkP+Va/8q17K/NTQRmY71/evZb7RAu/fcc1YCDKDziomR7fKjuPNslyc+ph2wHV5ZVdPJV3ErV4XU6/MEXvj/dcHtJRgPJSJVY2e0InawE9boEToB1DmgJlWcFpexGloMT5UvzIMWoyXfnSLEMk+4h9AKnlXVJ9d1mjMCxW4FkWxDwMCsCj1AjpYz+q8Okg6eIwwUF/+miv7CVe5uSvVg7yDJbjyTLDT0je1HQbmPQDlpL1qDToLbmrLEUxbYedvCc++9KM+syO7Pji7bfF3mOQGWyp+bCCebSJBcPl1nyLWt7fUviFYW7f5asq6p5RT4fgrnHCwdV67qPTIHN3ii3VEV1bWf5+9iqt9uZEZUR31wIvTUgD3SYINPB7HEYKax1dvkHa/j6g1mYd6ScRAz6wqnk+RO0wqaC+/sFRlN/pJjFlalrjPyOLZngCbYv/HAmfvjhvwoyNAs6ufprhVR+q6F2CejkxM2sENjAZf9DJjO506/OeECCsQ1BT9xxInzvOFiPgHd8zkuaNxJxHK2Aw80v4AQWomEaOQfucr6rDbxGCqY3txWXmFTzG/KzVb4LtWi80UBS5OzfkmHtAchAkDVvP9773IVyEGYzQnoE16NQNZ32Oz4HiHlFFnR3+eQi9gtHmWVuXj8c6yF9FqFSfTRxDbZg5oj4BQT8YQ86JDUHvmB5QtBFp/1/TGjUAPBUhkWwcu8kfttmonpyWp9Yhqy+jwyprNMV9KGZ3ej/qYf+SCQIWnTNGUpo5vkfw2oPrtpJ1x5VYo7ADhWAXnBUP5uBM2Ie7zvi3suEmAfqDix8AIrZ5Yt0bRasyLheCw3YzKclqHt7oyWPw0ZcyGerJOpwRVhUa/1kuq2VTzC8LHS6zIgVU4JnqqUOc/bNLnlUM3me19Og7Z0NqHOf7XMRH27SDbeQqO8bqmMvAAAA=',
        "savemybattery v2.2 automation": 'data:image/webp;base64,UklGRqQDAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IAgDAACwEwCdASp4AHgAPmEulUekIqIhJRGpCIAMCUDOAaeAyvmcK/qr5pPL/+u+0ntAbe/zMfrh6PH+O6wD9nesl9DDy3f2A+Fz9xPScT43wFP7uJp47C5vErDmcgiZxR791YWmGbbuIIwOJ896vOLapXSyMr0WiAH2ZSHJ4X31AUxQby6I/P2ittqM2L7ksLP6+RyGhuEhJ/Xo1tA2Fv6msHLHdXB3DCogAP7qqyT46EY/dlfVKp73/+hQl7iB5X/SH//EP/nHS5OmQtNEQY/+NFrHX7V+WybnFBgPUeBzw1/dfGBZxD0Khmtgnhfo5+xr7wn0YdK4VqiByS3jZt/7gMaUazvSvK3AbwBNRyL8S7P6/vxOxQh8Cuzhg6u2duhUk6PIHiYu854QP2liyOMXnIz2XgFrhQ68rs/K/f+CCDudtMekwdHxDUBXBgGvPb5Y15y3ZW+opMf5N79K30sZXJvU/NbZn1FOhel91zXSjaetiRRPO/vbIbVn6FEAVMsLg4v51roYAE6LoP7p6hYUhtxaU46UfU94CDAWGjO/XYVxh9jyuvUBaxn9ku/j7/8Kc3u5co625qKulg2Xzfv8kK9xNCDe2d9qp9lhBonIZCE1po7SYvMw5fyXysHhPwFepM8cZnvvz8pspnyvJ/irVSc6fQJ9bPwgV2MjfRRv7oDdsCoA2Fn1CZxqc4sLIUclgjxobpUYh5dKes6oeKlLEnOPAIYArpzzH2nT9+d/Ja51zpe5N1u5/J3GrFy1pGselG1FSbDq/pS7NlvU+aV9xYeBXVop36gh6V+P40P82kUsmY+C2hvoSKNdzS0lzhZWeV38W+DlrOOt6SIjWQYIsFZwBaO2l0bbFmkfJKcq25Od2DJhkk/0XX44U3Nhv3/W1UJaj9mklilNTMdocM6EBqz1wEJ21vsjauRcFD93dY8EVt75W4LbHgCgxw0qeJDRVBl4ANRTvRGGjgzze415a5sa7ctL9SdAAC9PQBgZy0k+QSFWskNX7JKqfgb43xgVlF9Cn/Bv+/IAAA==',
        "savemybattery v2.1": 'data:image/webp;base64,UklGRmIFAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IMYEAABQGQCdASp4AHgAPmEwlUekIyIhIpZpwIAMCUDOAanXYvkPN8uH+Q4j5mfoTcxfLN8H/UB4pfSV8wH6zfsB7vv96/1Xs+9AD9jeso/Yz2H/La/aD4W/3B9JumYbS86/gjpvJpHkiOsq9AdSbN3oBu6lJKRTFHMlDvRGkpOythom5AwBzofD1I5UIpAlVCZbwuv5aNqYFaU8MT+nAzRe8IlD/YL4DpkHznBdk4LXePgL4wuHDRNWfSQDJP4UbGMhAgzxEw7e2WrcOTCcmsFvJhNY9eoAAP7qqyT46EY/i6wsPjf//6FAA9o5W/8Qz/xDPZCCvVJoifSFj4DKUoRS65SKHLZNc5OJVY9/3XximkzQFU+Pmgmqlida8bdu34Aa5FoMmGY5Q3M4/W9uW1Kym8Lmk0Oga4dNnT26H2Tzz/iKmP4uAW3GPJA4kM+9pN7xEbC/RkVX0RuHK72WdGHt5K5VxCqmdUvwhohadRZT5mUs0q9doBeAPNGYYpHu1XCC4LVc2WBnq7Ls95hPJHdxK6pQkB1OQpJUIv+c3h+2lTviWGYPgNFZ+IpLuPGY8p8T7/gk1i1HHYcDPYwEFfUJovpet8LjbuFUx3mNT4RTg3nrXnyLHUraMHHPMBSNg2wXxnjKzSagJg6QXldlp8V55jgFVXsu8m0GrFNZeAI4vVCp7/ha6iMOKNzi+H00RNNg7l9bidHuueRPekwUqLo+uSs0Gf0xzYw4yEN1n+/4/Sd07+cPWGIiyEvQHM9shlzFrwKyCf5vSvPdxFVuIMYTx2XJpse5vrG6ZO1RRnQc8CDujIcnXUytSGcGRyOL3xYSjMnl31FhMBmJ/jjTH1d9kqoeTDSQfGxlQo5cKwh99atZLILT3E6fO3IFDJhE/N3OQqTt2xUaiL1H/G9lMZA9zWCsU/4sN/xCROMAPPXHAgXhDo6o/ZprNoq6ZljrB7cdLnXabc2L81yDOZDONYuiLiq3gEAfyDzV75comF7Xqxk3UaHzy9RdDB/+pqc0/RNXQMGPopaw1ZJ9p+5ki3deqUvkvxZU9mRlBiuVv/d8nBXuEHjvMIoKH9TTpIcYL97s+bsqPrIAC5zS5mu22esMSxbwz+wm2esePZ+AYv4ubdfXBE1W3n8EdqjZrIXi3K2o6lGT39iH2qwHVFM/a5oCSL+9/52o748ZXUA6jozLDodlp/esHjheR4o8iW7wF5JciJ9dY78nwUo/xWak4/xaWyHmtkjV0bv6zs3PRMJNclVGF2Fe+EJDI20j5NK6w/2CmCUmMkKGkVXbI7O/QN9WXUmdStI1lk1t4j/STK4Y+hvb0h4VZr8pEZ6z5t++aTgy1Z8znnXgNQE+HHr0FEIDV/uzVdb/v/v3jmZt2fUwD4NC2LgVyEQCFQzUz4hxH0najXfCWVvc6PPkAVC2gZC65lWPvHIcwdvVl+VLhZadojR9KcVhGIYfHKIkbcoltiddRODKnM8BK0K15X5NMaz8QJ3ktKVrh3lfCcjtMRZsNn73k4bSIMhUU3eOA6FdpEifEAAAC2CTYHhs5yYOesdMThIgj5CD9muCQJrHW4tp5OfUnQAAyS86UG4LXBV20v9PfORCF0PHZLFT7w5tjJy5r4F/ob/POAAA',
        "savemybattery v1": 'data:image/webp;base64,UklGRpoDAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IP4CAACQEgCdASp4AHgAPmEulUekIqIhJBIJkIAMCUDOAaf4wPlcNO4SqgdoDbgeMB6u/9w/x2qMfsr7Ev7M+m7+wHw0/uL6Tie+97aFkf7vWGUKFCb2Ey1jWGCw/Zpozq8pl0g3XlRE+3SocgbjOePb5kc/XvW+8DuQaI2WX/SSj/3czkSwXKkHYyDyeoIfQ40vU+xu8tFg/UdYuSIpnr2AAP7qqyT46EY/dCCAqqOH//Qzd7OW6b/pC3/iFv2QdiOGE8bGHI4DKUniR794osZuix85ZWGVkVP6p8Ynhb20xRgQYMU9vmfY8qV2yIvVRqiBySsV6eWkOELldTJqUoAgfnx8amIbAhde734ncUHex8/sl7LvmNKkFDMciEZLaH/tVEve8TFsqHSPj/SBdddZvTscvg2sgXnXV7rlY/y7AF8GVnHPRik/w2TQjC9dWlFybsonQKnrsuaS93uxB8tQ7pP8I6QaZVlp8APpVEMn6SW86q+SBLljdnR7r6PGwGAflNrmxoXFLB8MxhxTddvJbWsXNRvHAS4AKYokaBs1hwBb65f1C2NJnH4wc3gRyBYsOVF+MPI23iy2Zq5BwSfVopdArSNFgB2CiHh+X6+wyMEtm2KNS+rRU8KwmfxK0CMdbrlpkHFBbHi/x7mV3N8f5wCaCLyPefnv0THHpSIrRgin4/U/zGBBjVr/ObjFR2lDfsO7OkQ8rSElQ63KmW2z/yrO0/l508qPoUfx49nBLYqEPRc25lX8neNjMWvgOIProFB4jw/KmMZZ1Y/uj/v536oJmCvo/LcYhjISWVGXqNNacuNGGQ2isyaF5vnJyK+3UA3wCgm4Wmx5BdLz0RuEwcWDIqk7E3NyNtvxy/g8MFCzXh+/nRtf813sCQ1c2WIHYZmSfh5tpctqH+KFnbusYF1aFPTtLKa1RSh9OVKnIh9WBo1hCX38+HXGTADADfGlC/s6QRzT1BB2YxS14AAmEqw0xw/ig6Mxn09tVdMDMF9fH0jxiYC5ZWvq//4ZgAAA',
        "coolbgremover": 'data:image/webp;base64,UklGRkAFAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IKQEAAAwGQCdASp4AHgAPmEwlEckIyIhJRZpWIAMCUB2A5iAq7Hr1X8kOfB4HMxe2ScB90HuAfpL0iPMB+y37K++B/K/0A9wH+H9QD+y/8DrGPQA/W704/2w+Dr9wv269p95IgwR5DdiYJ6UFm0aAJxXesx0tNxf3Pk9MGqDU72342koH4ppi6FKbYEm3fSNPPUe757wuAEduO9QR0qZ41xq10DcOvwoa6fSzNZqfT27jtpOaRPzeFAxqg4ML3fd7nWCd8OZ8/fleZOqYs+TgWGR7xWK+gAA/s8Bv+oXPcU/in5WH8rD2Xf+LE3gGNiBrCYlEEaWSbrCcwX/stXy+2gpdDK49/i/Nv/amJNOkvwtXzyND47Zc5L/ZVk8/1FMyCbVX0wCoOyv0bXm3H7UhcswxujKPt7HXhSYNd8xUZrmxuMqnGdvwRYaVZnNQkqGeTt5g6DvIxS61n2IerCP5hbe5j3VGEewF1ZxqBuh7tX2A2kN3dK3QRWs1Hg00/gFVxWkBtElhtaMwX1CcAdmTcNIM9ob3Ik7OBt8vJ/wzZxKJyLFTptlab34iXlRNYjLCVndXjyq93QF49KeQ+EmWQTvVi4DsdGxGL2zYUiE69hbnHWIwT3OVXnS2+zWOjaHIRPZeK3Jig9gQQxGMM3KdfOv388ouZI4QUGjn7LHTAM6gSUVXqofqyvbWttNj1J5WeS4d1mxl/2rrRxnbRQA4o4tKOTMOyt8/Lla7qv7LbsgsQ49x89+AxW4eSosn2BVIGbKa9sOUuaC3HStGln2PXCJ+EZUeGfb/H45FdfLkX1Lgb7DKAeN8O1UfBqHOUqvVsEv/Ajs6Wm9Tk59XGvMpULLvdSPOr+UVjeNIskVxXOVfjI6M3vA6RDkB8bKs9aGJaoMkzVOAE6fosqE2jGfWtLDruKPuPDqDLV/eHqQOyjMfjrUWkG9ymVhzbpM99FCVTewGL41EpNZlXmExXN8Ke5i1uc/3EZ2gKA1FkRCCb/oxsAtQQLgP8ga7c47TZxq6ecP/h8kdmFaATZZJTy3kHH5dQW/igmu+ELO4/9nOsEyNl00FtD7RNtj7jsKg3BTkD6rkJqEwJb7iHrtLe7cYvPPmgPDFU5XsfhgosJEQG5U2njx+DwuPDXmpTZ0ssufrjI08WMlVM4izF4PEzrxzkKXUE0D+pkqXimFwwdFfL2mDZE+0/Lrbke1J7afRI9lPSVlaiUXXdn9hAjProYuJv9nMSYnOcqfszMQTDt3HWUdxiObbfqEs2u9+n1N5ph3uUZPeftuWOOOzBSuPYNbinfdIDsOccU7jp0AInp64egpLPt67CNS0hF45ylwU9GV45RzyS3rfIYNVdfqoVIQqFSKRYuA10VvxZhWgdZItaB5cBq/2TOFvnLucekXsXVa7tAYBkc5TBhrShxmreVyC9bAb1GtjI2x8Ag86Dujx81UjCSjGxn+O7SskurhWpwAzK+kgNp/H0u8j835PqF8KFKfcpYIkZSrbKRUY7/1/71VuY/KiM3hfLicUMLB7JJEuzwF1OA4zsUQzqTVfqHxkByXP+A48jZ3qipETNkCAc3mAp8SLmI8AAA=',
        "coolimageeditor": 'data:image/webp;base64,UklGRgYFAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IGoEAACwGQCdASp4AHgAPmEsk0ckIiGhJxW5IIAMCUB2A5uIOvAcctuv4q1bnmOcb/8bzQf272L+YB+qnSA8wH7Gekp+wHuQ9Aj+a/47rEfQA/bv00P3U+Ef9z/3D9o55Ew4qyBMsVLDS/KGs5SlKUo/f7R5MzeSdLkBf8rCDFZov+Zfey4eksa1K1IPyJMTBhad67qI1flziAK5b1AFx89q9BNS8Rr39WdQo8PiVqCG0KJq3tbTccXYigwH+KfotXcFoX8ST++WK4TX/3JbcgoMsillj2AAdLTAAP7JaBpz/9QSr64xAgc/5sP/zYd3z//kBUn2I+2b4W+Sm4VZzSSeKUsD6AgyvzGgalQ8MHc3zZtVqwXxWuzUe1dHI0B0Q+4AXE+CuuYmVKEPF8tS8Y2DAjquRFU/DhG+bjozchYJVT/22VT0lWeXWxgFrZm2c71RQWW0HOBpMSs0DmvkWCQg2BjW043Wi0OCAh0RZV/pKO748QqtLCJB1WvAj4Tz2Nwp8Mhr8hZsNUHPsYrpVJ1iGmpk0E0aNJAYh754gnYgHMGMIfOEWr35sWwhe5DVSK8NzQC2/PwPfAixJ+wfaGJmfn7P5fAdHVqmsLf3TEB3GGH0rJzpqVFChEy9Jde6Xahu5vCO4eAgZ1LXvRunIAWPJfUYi0Jpc9OZOEFTI1k4VwlvRJ5TuDP0nKSviimnvDrzuwpm7jcuCgY2Y88nUXSXSlQeVWTYZo2KgXblChgn79HB+Ckaayjx02vtggc80SVVluxiWSwS32BQuS34eYIxZA9mWxZwvBrOX+d/Z1lUtz6529kDv4Jr+i0JZ83rZ5jMG6Zsm9x3CO5lRkOHkrh+yv8Jy0s+Wca3IyIVw1nHjqFU+oGF9ll0B/PpXLUfvH8setl/nWML0yVgj/0zVVvxU9Owlex8dcOQKiAsKIny2S2dH2wRf2zNgxtjs/3JRr120fPoEGTCnLMMo1nKOMq5GV3gScJDX97ecpFy1/j/2GeUPFgORR4FGnrqa+astePGNcE21VSA6aZMPjbu2rnue2F7Q1dkIYKim9CDs9yyVZVM0ovKo4wnnTOXCti7gKQSUqC6gOTnyKP9ujF+UGdQ8VunulBYzb3oJ4gbfRuLwDyzerTNmt+8fbWL67EP2crGwc9IcG2HZ/wKivYrD8MkGUeIKtWePvaafPCBdkfEeS103bLiIPSkxLIJ9lM+YYIhOjZ+G17qDzMFb0HJxOD4QRz2JCfZU6fXWirnJ7GQJ199pHKg6UN/scDox7XK3Ko7xmCgkAvuJoXj9e2PP6U/2vh4zlarWYdNVWI+yMFWUb/42yq7LKJI2i5HAtdfns1XRIAPCJBd3P+69bYHE58l4Ym29j6BKSPD8ERkALU/LqRLf5AGPFRWpY0Ix/PQ6UVHBawBLdPh2FG6qQNHy5F8V9f+6sxHM/NQ3yVjNGPd6MxjPV4JEC6nAVTYPxUoD4/uMC1J1fgOOfY9ycvz+yAqPy/wckuovonA34AAAA==',
        "leaf blower w/ google search": 'data:image/webp;base64,UklGRqYDAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IAoDAABwFACdASp4AHgAPmEwlEYkI6IhKxdIwIAMCWMDsB1DvnX6u3U030eznPKb9P/oM8wH2ge6L/w/UB0KPq4eir+wHWyG0Bpj2fQrs2V+AGFQSZ9Cqb3xLrEpbcKSslLdAin8VsZ/EarPQRWuy50ukJeymzdsyAaL5nxchR0i7aAGjsSRRzDnsugqDXfw0Z1Dl6yMVt9RY6spc6WjH/13Xw1xv1+nK8iVgnp0N59AAP7uwqb887/besNLLbucWv/V3t4Dz93O7ukT+z0t46HDEmfj1rLCbmh7lz59DSpBJHrbcIveK+fVMgkh/y2PXqIYxhpnm05MstfA32k/8kXaQQ4TEmBBchHg84Uk3d4tWSURTD0+wHC8QohUM81KAroB6OAdkO+UKXeqFMzL5jEK0heAeDT7hJZUO/4eCFt/HO2NLy1ulPRebD0JUm3HF2dZdSOwTCLg/PHQ2KdXheQbjpg+yUZTlZ4a2xun8v+G2HiVOnehVUY6G9eQrbWQNJSwnhmBsMKsiQBrg4QxEoaH5929jPPmt53HiIAu9iTrcYsg7tsmBoN+2oZs1P7QNqBtIy7zwdfv4502PyIe2neK5MxIS3VXUTvRFKXLAj6z1n2uz+iKQpTEewv1AoetkWb0V7UeyWSQHmn/xJjjGOODFIsh54LfSVO3knZxSuPsZAo+DzSHzSrr365P+aRAvO/bLK/9GDvBqZHieeBh8eoH8wqmEweC488ecEywrGW2dGXN5B8drALlDR0sNKWigLpsbcTN5/P1mJVauyo8Sa7YVtUGIGTjJTZkTvAtBrM271gKqYUyoU6CJepEA4rutk72qztHIPRXforWj3hwzVg+AehgEHKQzEGgpbtz9oX9vHurx9palyBYhwQwdQEsY68fDuau0033Lgd9yJCYOgZnyfAJtu+rm4GIn8XtcxAGpA9wvSJ9LzEIn0uwerx7fhvbpg9vqLhLuapS9KVQlrWLfbejI+cV1p+tWAAAAu9k28Vo4EVjUxXA9AyJJHGxbpz7v+Zg0B4xt+8HAAAA',
        "leaf blower w/ google gemini": 'data:image/webp;base64,UklGRqYDAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IAoDAABwFACdASp4AHgAPmEwlEYkI6IhKxdIwIAMCWMDsB1DvnX6u3U030eznPKb9P/oM8wH2ge6L/w/UB0KPq4eir+wHWyG0Bpj2fQrs2V+AGFQSZ9Cqb3xLrEpbcKSslLdAin8VsZ/EarPQRWuy50ukJeymzdsyAaL5nxchR0i7aAGjsSRRzDnsugqDXfw0Z1Dl6yMVt9RY6spc6WjH/13Xw1xv1+nK8iVgnp0N59AAP7uwqb887/besNLLbucWv/V3t4Dz93O7ukT+z0t46HDEmfj1rLCbmh7lz59DSpBJHrbcIveK+fVMgkh/y2PXqIYxhpnm05MstfA32k/8kXaQQ4TEmBBchHg84Uk3d4tWSURTD0+wHC8QohUM81KAroB6OAdkO+UKXeqFMzL5jEK0heAeDT7hJZUO/4eCFt/HO2NLy1ulPRebD0JUm3HF2dZdSOwTCLg/PHQ2KdXheQbjpg+yUZTlZ4a2xun8v+G2HiVOnehVUY6G9eQrbWQNJSwnhmBsMKsiQBrg4QxEoaH5929jPPmt53HiIAu9iTrcYsg7tsmBoN+2oZs1P7QNqBtIy7zwdfv4502PyIe2neK5MxIS3VXUTvRFKXLAj6z1n2uz+iKQpTEewv1AoetkWb0V7UeyWSQHmn/xJjjGOODFIsh54LfSVO3knZxSuPsZAo+DzSHzSrr365P+aRAvO/bLK/9GDvBqZHieeBh8eoH8wqmEweC488ecEywrGW2dGXN5B8drALlDR0sNKWigLpsbcTN5/P1mJVauyo8Sa7YVtUGIGTjJTZkTvAtBrM271gKqYUyoU6CJepEA4rutk72qztHIPRXforWj3hwzVg+AehgEHKQzEGgpbtz9oX9vHurx9palyBYhwQwdQEsY68fDuau0033Lgd9yJCYOgZnyfAJtu+rm4GIn8XtcxAGpA9wvSJ9LzEIn0uwerx7fhvbpg9vqLhLuapS9KVQlrWLfbejI+cV1p+tWAAAAu9k28Vo4EVjUxXA9AyJJHGxbpz7v+Zg0B4xt+8HAAAA',
        "editable materials": 'data:image/webp;base64,UklGRvADAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IFQDAACwFQCdASp4AHgAPmEskUakIqGhLBNY0IAMCUB2A6y4TsFnUt8B75ZPfzf4t/6N7APuA9wD9Tek35gP209bT+weoD0Dv2Q6yX0APLA9j79zPS3u8muDNATM2Cui42b8D9HthJvrkCfCQwmUN9WK4gl1W60t+MbYD6NEc2xMIs9e5UHzXVsuVL7kjI+NkFSm+Kk9zEXY1QzBPB6YthNNRTB6uyA3qyF7uhV9CuD0U2hBzniYP2D0AAD+zwWPz410/9hhIw5bWi3/pJv/aLWkR/+X+PwAOny//Gr2ARsezwdtQygueI2jX1MvKA/HfGPHITGjatVmn9HwhbRUNKElQ0kW+n9TDPxqxOPnDeXdj3keIv+DEhxhTaYMcNqV8MGrbm0YtbbDcfXPGTqr1E7Zp9d9NqY+NHvvZEEKNAhNXduEoGKlRlYW+45ThmujPwpbcnUec/TkoFEaAjmRGRySfJ0GePwEpAUzcKBmN1+LZov6wUtN4i8ioBSdW9byIv/xgUyrHNT/jaCC6r8aww8ttOFbeXOR1grtR1Id4uyYINVdxOLIoL/jXxEesJjobuIxmX4QNNTTW/znvsOTJMLdb9uWStm9ZdBXANxxGCnN3ij6FNiprwA9kBGh2CD/g8VlERGqRKUTc6jljFCYj5I6XpurQ4m6pfpZcTCTpQ0m7KCcXH9UihS2KY95l3bWjSAR6PkCoriAuz9ayn7lgx+qTVmchW6arxGkZl430Pjp/U+1hn/yyxUjkE24I9hzcxwOXn/njgq92WeoeyOePObdhzE5HR8H99/Yt2cG4Yo9yVrNPN4GpAFM72dWXKPhDuv6hl/HInZe4WX2C0l6Fmupi3tptKfnhEhlFjOTh7BGCG/reY8JVOKl+LdaZO1G7QdvU19h8r1Ig5P9wJJ+yFiidr6T6nzd3DsdzS88sNb5p2vyNmVfUbDsSUHnI6PSMCqMTrH44pZYNRepe6MPjNlXHxSCs4IajRtgjczHktQtVjPHTSgSmdz4ObEcOanMEmM2yvaVuAbgKKVHCLsC8WIEONqyh/QaPP/qPI1JuRkaojdf8BmTQVA64zkPAuprrUetbkCO3ubUPNvXBlH/y/jz/6G/KNh7N0OXCAvSHTidKU1/ybpoAAA=',
        "editable matrials": 'data:image/webp;base64,UklGRvADAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IFQDAACwFQCdASp4AHgAPmEskUakIqGhLBNY0IAMCUB2A6y4TsFnUt8B75ZPfzf4t/6N7APuA9wD9Tek35gP209bT+weoD0Dv2Q6yX0APLA9j79zPS3u8muDNATM2Cui42b8D9HthJvrkCfCQwmUN9WK4gl1W60t+MbYD6NEc2xMIs9e5UHzXVsuVL7kjI+NkFSm+Kk9zEXY1QzBPB6YthNNRTB6uyA3qyF7uhV9CuD0U2hBzniYP2D0AAD+zwWPz410/9hhIw5bWi3/pJv/aLWkR/+X+PwAOny//Gr2ARsezwdtQygueI2jX1MvKA/HfGPHITGjatVmn9HwhbRUNKElQ0kW+n9TDPxqxOPnDeXdj3keIv+DEhxhTaYMcNqV8MGrbm0YtbbDcfXPGTqr1E7Zp9d9NqY+NHvvZEEKNAhNXduEoGKlRlYW+45ThmujPwpbcnUec/TkoFEaAjmRGRySfJ0GePwEpAUzcKBmN1+LZov6wUtN4i8ioBSdW9byIv/xgUyrHNT/jaCC6r8aww8ttOFbeXOR1grtR1Id4uyYINVdxOLIoL/jXxEesJjobuIxmX4QNNTTW/znvsOTJMLdb9uWStm9ZdBXANxxGCnN3ij6FNiprwA9kBGh2CD/g8VlERGqRKUTc6jljFCYj5I6XpurQ4m6pfpZcTCTpQ0m7KCcXH9UihS2KY95l3bWjSAR6PkCoriAuz9ayn7lgx+qTVmchW6arxGkZl430Pjp/U+1hn/yyxUjkE24I9hzcxwOXn/njgq92WeoeyOePObdhzE5HR8H99/Yt2cG4Yo9yVrNPN4GpAFM72dWXKPhDuv6hl/HInZe4WX2C0l6Fmupi3tptKfnhEhlFjOTh7BGCG/reY8JVOKl+LdaZO1G7QdvU19h8r1Ig5P9wJJ+yFiidr6T6nzd3DsdzS88sNb5p2vyNmVfUbDsSUHnI6PSMCqMTrH44pZYNRepe6MPjNlXHxSCs4IajRtgjczHktQtVjPHTSgSmdz4ObEcOanMEmM2yvaVuAbgKKVHCLsC8WIEONqyh/QaPP/qPI1JuRkaojdf8BmTQVA64zkPAuprrUetbkCO3ubUPNvXBlH/y/jz/6G/KNh7N0OXCAvSHTidKU1/ybpoAAA=',
        "deviceinfo": 'data:image/webp;base64,UklGRugDAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IEwDAAAQFQCdASp4AHgAPmEulEakIqIhKhJpoIAMCUAlP7uDI9OnsW9uzWXqfJH+b+136H+jDbZeYD9bv2Z96/9QPYB6AH9g6hf0AP2A9Nv2Uv3H9K47QBjjddxAlJ15hn17LvKr3pfgQzkWlMGivgM2qfo+nasjKOtc2S89cthObhcnGdA2gHuQASz+GjHSqNhCNsrNbbnHVtd1XTJeFzgOo8YQvdaAgR3eW//oBme8FlezOgAA/s8Bv/9QeFazBZP/lY/+Vj9l7//FhSjmC61+tedLW144ku6roPTu4pARak9wlX7mgdisny9P9d5t58htha36iFV/O7hf9l26Ej6bOJZCh868r9B9tzNe+QoatyzFNtD8y5flcrzaMJWvZuNRu1t2H6MmNhHmlmnrWSlDH1y9Z5KnUN8+ZqcPHmuAYbYxdinWgsJvBlYjtCDfCbcStPqRMqCx+nDihJ3Sb5C7zwbywQyrecSMOkx4WBtilAPvUyOlT8F/Ktr0rYOZRI0Xudy+DKx6RiqQhAMqCNyQE6MVtnGxiSe0Xun5T7VgQL288vlK25NIEvqNNgOCQBheDg3uBKVPARX7NJ9xQSheRFcJ2WZu+V08EjKJKVDoGPGyGsl8MhYnoScjKcM4WFY9kJbVkU88EwZu4t8JxUO1VOLRCtAWuYl3BnamCW8+Tx0p/m0r1QLFsxijQhtgvvSWTe/cR0qAkhDI2rf6fSBPp9/7sPm1rzJ+9Bd7KWfBDOKagHDZwk8zSHoWBmupNazH8orHAYNZozHZo1JNxSSV3buKRFEVuYVpw4lw8fHA8q+LfF4e/VWOAngLlsmu61NKuCSFNrRC619pP7H5PpuunxJMHnYUVrvuSqAmfGVjBE3YipnD2TtnnyENGTxCyleQXeject0WcCaum/lXGpZ0WTQn5m+dzX9tkluKl5qc5WjNNvctrpgEbYjaqKibvYary3XqSxlkzPYBkMxR71cjj0U2f/lKGUArBdwEd+feyZhRQPQZ5zyGuWMKR9O15tbPI/1SFMOe9+31zfOOGhyHdXcgZVbYHfIIoNoqWgX0D64yV8V/DZDNBYRLleHOAHh/JnGO3BtC0VbCL5c+zYJgXWfmxcPt6xgfMol4AAAA',
        "moo cleanup tool": 'data:image/webp;base64,UklGRhAGAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IHQFAACQGwCdASp4AHgAPmEsk0ckIiGhJpO5uIAMCWIDsBzLOvdo5KfjTxRk7/Pr/A/rv5Ve7P/K+wfzAP066QHmA/Yn9cvdg/s37M+5r/OeoB/Tf+l1ifoM/tJ6Z/7ifB/+637ne0TSA8fvfRlA8ANI1NJ8lv1SSqHSvwArjRZmEZ3KDp5ucdWW0xH+nLw0rIvwYzt7/9SykO66OqMXGDf01yYJ+awgSJIY/wFQUb4MbCwIQldmgQRH2rbPvnmFIXyA0zp+lCWN5Mxs5r6vGFcJltn0tPeWXS6ggYFWie6qJkvehhjwjIloAP7JaBpz/9Qc6eUyk/+bC/82Fm9f/5AcqCAXtl9VWxJ6ocNBHPlh/al/7LZQ6tlMG6j6d/zavsY8KoRB2GXa52d5h59T2kz6EHNimtIumXklKQopXMyqUun4E6aD2TxSHu2HTe5CNTnwE5j2F8aru7FlDU/jp+sTenDlI3etB/nCuOUu9U+0ZEYbfIaR7T2Fzl0prXGf7PiRmbkROWPFyO0dfd8Fus2Xdv0UnG2xc8hZG++wI09lkhbgadv2q9uy5S32AHbPUx88dsykNpKgiunpXIr0HJCz4kYqnfU3iL2s+g4ILJM1kd8Gc+RyTHirO4JqB9eEPDfhFPPPoGaLAspdDVhUOvsqEhZIPsUvhR3Tk0rqdaoeu/iuAcqHPSn/RD79K0fPMR9c/VwZC9JmmIMBl35fifmf6Lrn0zq60caPRJR3Ilcyj2E3/M5R0992kYi5sMXamSiMu8/4x3P75wz9j2Jf5JYEAfh166l9aht8M5zCq7CDsQEPstVT3ysvWq9xCjDxfe5y+v4ecqF7hODwoCJ0XimSbnWr8I8CytNTXS1eSxfIeql/rh65KdoFBohryhd1IRc1AOtNqwXWh22ABH+78DaYB+1CTxl7csFkdt3TQm30iv6XUxt/dTAvUHFdwWBOR0Did8RrSupVPkrFL1H8w3G9pDfUJevW1u4ZV1Ty8rQK2C1qjocW58HLSH+jx3O4er1CJs8RQvnnfWrpttz2EgPMfKln+8oaKKGvSzCLPu5BKoiqcS1i0kJPrb1WrSfmWzbW0yibRaSgfHLPqWmu+pcPi/32lCByu7z3J1zi5JI4NC/0x9rcMPZJoHyOv2nCqL4tjH/IftaQpIguJrmgplvYunApbQkLMMsDHe7QuLo1L+vFZC0laLGAbpNDQa51wmou3wLz7fWzibcqpWbunRYfbv5sXwojI4uDXZfMzTjjvW5nYQyEpYDbacJzYKx25VolAY8b7t3v4xGjFD5AAQF+lHRbhg6ys8zSbd946a1NnPJMnEjYNmeD7bAxcijO4HumVCOSKrt/A4xS6bUGtLEXJrt1390tjR+jOSiZ3YJKxD+ZC3glg/++CEjJ7B8l3Ye6Gyhz5MRJEKOt7p4Z2r34qdraFlSTLATLtxjkhzZollHksN3GWaMe9xz1MP3bR7kXkN4klvhQsFCZucK4OubffS2zomKrNyAn6/EO6y1Rtsrz1qlmpQjzJ0rADogin1cWLLlzv5DgaoOLpGRvdq5c4na3IN9xSAlYCW27X3l/CDoLa06QjAstvDnT7tgJv5KXdXp8+RbJ2al9nVNO8zodIyDgTRjiQLLCOJX2FndfkowLSsoS9lDTwcT6tZEsqAfY+Pq63kAggcwulOXdHtJrLaDwhlY/5JP+KmTBX9S4uItmE2kKSPt87lt/EkvD17lOBhlPBeP/PSNg5+YNFcEjQ0bNo2+Q7KNUeOipXBrhDYmUMPmfz0y4Gq7qXu43y3OL6sa5xdXCATAGpDNA/ykzxLuDBdTgOPTHJp57LuJxiBNw/emSk3r30/acd+0HrEikjdk4PNAA',
        "[api] notarobot api v1.1": 'data:image/webp;base64,UklGRhgEAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IHwDAADwFgCdASp4AHgAPmEwkkYkIyGhKptowIAMCUAZKU8oI/3zkjeHNf/Mu9T4V+UD5+fzn+3fwD+AfCXzAP0O6QHmA83f/ZdQP/R+o89AD9bvTF/Z74Vf2y/aT2gCZlJ0Gz2vmoD5PkaxaRIlyxouAyhkdBQuOdwfjdWgCCewpgOC99ME8g6dXe6t02Ei293m30hf95ti23TFUM/mmzmQTLMztk1DwWVGYMv80TTs6jZ1k5utnBDp+6Avd7nCxlgKA6AA/slpT7Tn/VlJIsZQdgv/oCf/QE+vr/+Ud+7txb3bfEWY5ndogyyNHaMGU6PVXa39l5rJXn+MTmPp0zOXhVx9DyLB0j2yBX2xaDNYyIK2/05U6Lyx6h37UQ4F1Rx+v7DMZcGdolZ7eTccu+Nwa6YY1XdTyofXs/f4P2JcbxlpydoV+Ud324xvGPWqO/e3IpR3U+9tr34fayUr4ojXInfv4n8qcAfxWIpSn8Hwj/vRUQR/mXMTQq3ALpbqb/UK503QJqfC569AnHrHfBPrMO+NIe0G5MIK8mziCsTSHQjoAdKWLprBaWXNAfdLAHfkjQb1z6YKatrdAclL+TT3x8EBfdwrgMcrCieM5gKYxTkRxKu0D2PP9PSrWHcNY0Gre0y+aQrPFwc6WJndF+h4HNyxyXfkhBVjcMvUN1ECPS4A/3W/hOFW042Qfi63GS3NRoj1tECjVLmqiAsjfKOSTOu66re93vYHQtFIoiS14OUcwF0xMBkSwzghqCt5lBXstX2FBwEJkZgdLXriqBVyuVD73ckIBi91m6sZ3Y0sdxhYwj0Zve7GeCwilNz6XhhzIJ6jZ72Zw02i+dvirYM9QsoFybpM0//Rng3+yYSs2DKvojFoA50WUIJQWXEXZXlK9HptWxCMvIKbZYwARs9R15eu3+KRLwnehJI3p7m9H0Tlm/TtyvjUzpe8Dvy7E/HHQ1/iJ4cpdbEVY/VoNRYkjEDvpclOYPuO4hXJT1Rwsucfb466KJoBGCiSl26E0pHOwckM6DJavG0r+qexMAwIOj1u9hjt7QJPXXMno3u2KMHJEecFW8yvMDmNa7Wum0oVZdRmZtjRcZuhx8YiT/TxfvPaPaYsIRCK4I3Fv0lZx6+dXlJT+yGZopnlovjFq2fw/Nr/5VImjnrj+19VjPHcJ8M/g/rWsafxhTpoAAAA',
        "kool menu": 'data:image/webp;base64,UklGRsIFAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4ICYFAAAQHgCdASp4AHgAPmEukEWkIqGXDExwQAYEsgHYDohb/9u7cTjnYvOfsP9Y/C+HVfzPux93f+A9gH5k/2/uAfqF0gPMB5yvod9CDyQPYc9AD9M/Tg9kX9z/2u9qrVNPPHYxXg+DXenKV4KaSCaN5SYhYHDjSZZEoihn0t8lLqAnUc4FMHCWKytYPNnCyYNKPQ2LvV56CUnL3wThC0C4+G30MMI59/9blc59if9qWiy0xbEeJ+oVg2g6RqufK9LE1iU4TyJLRN/KcciPNhMCfe7v36z/3oAgIKvJ4qFvPAdLygto6vKX1U45t46DnlhdDka/VNEzdZ8uKQAA/s8Fj8+NdPYVFEyWlNxv+ysf6lmVn8wviqTmdfvLWkgvSsABH/9lQqphCfUokmH/jGXyGk5rP+mWUX/B7NhMZSlAiPidXcr9/OCd1npLcBDp2Oe9rwudVCTpQdUiYksZqhCWAXU4+nn7S2d7iHG7UfUBR3H1XV+dMjfM8NL4d7DhhoWMHpvPGuAS5ArUw0yTLLq/BHiHZ1Pd+nLLTUAnEjtpk5HLIuBic3Th5jezjVmfEbkiiNBrM0xqfi1ElE/KLopfBJZlGvU0oBw03IvyzPB3BqKgIGnkuq8oepmiHcxWs8ySAWmElYkOB50E3MprKeh/rtvrjX2bU5lMUKGdxVHOJnCM5uyisFCU0zSZ5CyGZtTux2qZzokfXAVvxILp1x7Jhthi5UKFSuBKcOtfroPYDMRGG6/uKxiMYaak6GhCyrU9qHCC4ZO6KN7925aFUhUdOhM8iUkkc0olF4F3Dot5lopMrI5mX5Xq6oPdTLNz5o3uZIPftV6zpSVJ+z+N16No4HP5EuufPZXC4mIWYuV07UCKw+oMqRDL+HlVuumD7D5wLSJf+m+XP6Px84qSdLihDej7YyZUznW/kc4JLn2hHl3OllaEvzmPTXr3bnpYufFX7ZSu1uYuOM+vyGXM8VvF+eGA/fuSyBkgLoCkpQ0Ced/5GbTDU7BlqfuSHefpaIage2eKyrzQA7y9a2/sW7fPn1ofaG2DgpZgi2aSSH/38KXekXwhmpV9+32K1mX2cXwqRzYSbHHD7CmWVhJI0mH1TesDFh/VmU3ThuPV2xHHLTxHD/5zQywghI4hxesWxkvWv/+ntjhwmfqLFeffhfh4EypgkDGZ3YYUT0//7yuA24ElTq3KJmQ3apcSaGHiyjrYetWdQl+Go826AeBJVgWA56Qq0LB1KFqx7RWbz9AfRBbN9mtrrT8ppH6+4l4agoBSN1FRnAqhZJhAYSkHmmwA7GQnXqC9+Cl9PTLQcm2mBDd4a/cdHpIDkjGp2j/xFedj2lLHYxBYKLxp19QiGRC6ahb5gSZhKnPT7xKNPDlxq6yL+aRYahTqJ/5y1vOFr2NrTGyXDqAGT5omiP+PqDKWY1MLf5Z/i++L47gcphALJ+EY7MYfFIrGnFluYJJH2/UNGOU2duPIMfThYdo+SnBmnZK+W2kcKnSdrgzBSFOx9R+o13ldUlVFQEZWvmmH74aMHydHkYL81yJ2qdGRsHNA3Ur4IGGu9lp0eN6tfhok6P+BGbuaZ+wwyoBt5s3YpjQe3+OzCHpTpyP56v8BjZtyBxyfR/sMjmiGioQyjEispg2YN9qztmrHmGyRJ3AafEeYBg9MaaDrAXvCVuf/PLPcBOzQN8K3fibaBa8thqnABIUnvog1kG36yUwY/m254No7QJ/PHDxgUufiRkvW//CD+tKj9+KnvEAA',
        "abel's url compressor": 'data:image/webp;base64,UklGRg4HAABXRUJQVlA4WAoAAAAQAAAAdwAAdwAAQUxQSHYAAAABcFvbthLdEH5DSAtWpc9UgpWgMaQfoscbiW/8I2ICAJjstd+Pknzu/ZUZ/Me90u0jANGphM8IZlLKk8mVdP5m9d5Z7RerS1iJOv87/zvoCyuxrOzMai5ZlSmrxB84DT6Cg9ERAAg7Pl2Ify8pZissxM5F4gEAVlA4IHIGAADQHwCdASp4AHgAPmEuk0akIqGhKBcJ0IAMCWQAxgJ0wC/u3ncUx+t/iPKJ+b/+j/bvyV+fH9L/yvsA8wD9WPOu9QH7heoD9lv2A90//C/rp7pfQH/kf/I6xX0Ef2K9Nz90PhL/bT9ov//7mzyo6DOw2UcwV0nE1HyT6hPSUMLqbAO6kyGM5r6Y+0DkeTWAeYFOvwjBnGVSOb7pvRVAzxokz1uBM5kvY9epIV1IZClsJ2TOKtW8mop4QPl989FKj+NOm/wv5DUptYUaiMJAyTwZmuz+zBovCqupMVN8T0ketK3hpg9iortu3AyuzpfHuQT6CkEmKddhmaaI/pELw0VqqNcsOEK4AAD+yWgac/6g5VIOTCf/mzf/NmyX//kDOHaMPDr1cJrNCxgkjtSOJrCQZ/3CXM0ebroSpiWhfNqHW74EOi3Oq7DufM+GSDEG3DZ31eBaGX95n9xRCecl58fmz1Ja9NRjQ+Fn7FuCdgWJK1yx2WpyOk1X2Wmoz0ywln2n5wmm+Tz0Zn6jF29Z0VR0lOto0Losy4bn9GNE+8aP+WvlcAQUoe5FLZ7nKodB6azf7gG2dHB9LjcxTVN60aPU6aYXA++Pt/PvobwFixxhA0+ohhuNJhTYe04lVVYwRGQe900KCp4uc1ey+GKxIncS2IXFPAY/AjO32rnQ6FHQBlPhPBIv/1LpE+JEd2zDlWX8IhQuhiJMb+P4hAPrkGIAVun5eqnjEVTMZdWQxtuBUzzFLSk5JL0qmLK48fvVN4hYJfHxQHElKfU5bwEkaYZMS2vlMgm0uu1I1P/OsvIYBPX/eApViKW2WACTIy95m/Mh57HsOvntN0XUrsknNAieX2i0FIrUFvlE3DKvbiucET96mcIEFozOECNtyzvNHUhJ04PnZS+OKY7Ryc8TIXQdwv7mMIhPADmXm4su1ZFNxD4nsRHj/Wjn93OrFypv/urcaHyN8bLRHnVjpdSvOdwa1R2/57PD6uHu6+k6VzAc5Z1vKX8XtnQV7UQlgBx+k4Z39ZZmznHPBpdGk69mDEEMyBcOMFapsFoRcwBG61tpZJjcY2G4X+1dauJS7bVKkU1urXrpZ/IDf7hCwCjdrpH7UYUp0xF3zpnpSExC+RdGOIJv1mqCimUx5JcuTPRIxuQx3OE+KKCH9JobcMnB+xMMvBf4woiRNgevgV16wcub9iHJRt3E636eHA9RDWPjncRVwou1q8A7+UOPxsp7Q589x9spFj2VP0aUfObMa7i5XNw5xYcNdltknCAiPpcNkZH7VlxG8gnMZVucKMBCtNPo+biPaypoJtw0T7Xt1qNb3nAgR456HtbStuVv/804ua3YlvckDIm6dTlYKrxZwbVN7uk2ODhOoGOmByM3v84bmPAuJvwygT7n35+e0sYUvLaoiJfNrXlu1TijLC8WMhF23v3PA/a/YvEKrBXA06/P/Bys80dk381FGUYbN6ZYVjD00TIaRwISC51IF3be3zfy0qTMgqAHAgvJIZ5JbAoXXGkykb9/RDascVr9K2bjAKil1A+xO1+bTfG35k7G6mV1wNDAsFh8D5Mk+fDltGnKPNIW6sUK3QIFzmyoU0jpa9kqFWQcJS/H5rpSUG/3YdWhAZvBBWTWvkS/b0PRfec8q5eeDdqDHh3P+tQDdZka3nI6aqZSJk//T4+dAPWNKjMW9xupYO1AaLJf/uoSPNotqvGsHny6j5iqkqHO4qApg5EQYxz2U+pEPv628dOfypV2HpBh4A47A4uJ9eQuvpvrTNwtgZtUds99O22Xi2Q8ZZsm7hk9m7Ei5WyJhzQauCyik90LsaMb6rZAjZZVTuXLEsM2WDsDtnXpEivXb4tbFU4221MWFuRREgFg71+ggIfs7Aa84Jvl5Qtsn/igbT6PWeQUAgeCRCcUxPLBxoSqiFVOZcDZgKZmn6b8yIzoRS+JJn/OsA80msCuGWi8gD3QU4yv7Q4Xq79rRo7KykUKGLT8fwwlV2R28eR1QaidH5sH3JNDaiAWEMk8mXdD0ECWNBgAAbh8qUWWUr10n5/wOh0PYOwsewfNAoF4YJQLaJxATT8cqiSGkWWcFXCIwPnnbEOkkMqDu70Q1+xg0AqEK/zBXE+g3VTc7mRdV4Yj9VUibrgaSVXg2+da6gahnrIZkQmwkFyd7efwHGGqmjWkckamk9p4Ihe0EaweJxmRxsgAAAA=',
    };
    var ICON_TINT = {
        "quickscreen": '#45b3f6',
        "anythingbutglass": '#ec8ed4',
        "savemybattery v2.2": '#4888f7',
        "savemybattery v2.2 automation": '#e86c72',
        "savemybattery v2.1": '#ec6168',
        "savemybattery v1": '#ec6067',
        "coolbgremover": '#3c82fc',
        "coolimageeditor": '#3e84fc',
        "leaf blower w/ google search": '#67c663',
        "leaf blower w/ google gemini": '#67c663',
        "editable materials": '#4588fd',
        "editable matrials": '#4588fd',
        "deviceinfo": '#4286fc',
        "moo cleanup tool": '#377ffc',
        "[api] notarobot api v1.1": '#3c82fc',
        "kool menu": '#4185fc',
        "abel's url compressor": '#3c82fc',
    };

    // Tile size -> glyph size, as drawn on each artboard
    var GLYPH_SIZE = { 40: 20, 44: 22, 52: 26, 56: 28, 60: 30, 84: 40 };

    // A shortcut's tile is its real icon, filling the tile on the icon's own
    // dominant color, as the installer has drawn them since v47. A shortcut
    // without one yet gets a glyph on its catalog color instead.
    function tile(item, size) {
        var node = el('div', 'tile tile-' + size);
        var img = ICON_IMG[item.key];
        if (img) {
            node.classList.add('has-img');
            node.style.setProperty('--t', ICON_TINT[item.key] || item.tint);
            node.innerHTML = '<img class="tile-img" src="' + img + '" alt="" draggable="false">';
            return node;
        }
        node.style.setProperty('--t', item.tint);
        if (item.tintDark) node.style.setProperty('--td', item.tintDark);
        node.innerHTML = '<svg width="' + GLYPH_SIZE[size] + '" height="' + GLYPH_SIZE[size] +
            '" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="' + (size >= 84 ? 1.8 : 1.9) +
            '" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="' +
            (GLYPHS[item.glyph] || GLYPHS.wrench) + '"/></svg>';
        return node;
    }

    /* ================= Catalog metadata =================
       shortcutslist.md decides WHICH shortcuts exist; this map decorates
       known names. Unknown names get sensible defaults.

       short  the one-line pitch in a list row
       pitch  the longer line on a "new this update" card (falls back to short)
       desc   the full description in the detail panel
       soft   spotlight card [light bg, light border, dark bg, dark border]
       pairs  shortcuts that work with this one; older: earlier versions */

    var META = {
        'quickscreen': {
            glyph: 'split', tint: '#0A7AE8', soft: ['#E4EEF7', '#CFDFEE', '#132639', '#203B56'], category: 'Productivity',
            short: 'Split screen your apps and resize windows with ease.',
            desc: 'Split screen your apps and resize windows with ease. Perfect for iPad multitasking.',
            link: 'https://www.icloud.com/shortcuts/419b76c98a474c35b11c8497529b3d36'
        },
        'anythingbutglass': {
            glyph: 'layers', tint: '#5E5CE6', soft: ['#F5E8EF', '#ECD6E0', '#341B29', '#4F2C3F'], category: 'Customization',
            short: 'Removes the Liquid Glass look from iOS 26.',
            desc: 'Removes the Liquid Glass look from iOS 26 for a cleaner, classic appearance.',
            link: 'https://www.icloud.com/shortcuts/66d53e172121493e9d834df6a5062f25'
        },
        'savemybattery v2.2': {
            glyph: 'bolt', tint: '#3D7BF7', soft: ['#E6ECFB', '#D3DCF5', '#1A2340', '#2A3660'], category: 'Battery',
            short: 'Squeeze more out of every charge in one tap.',
            desc: 'The newest SaveMyBattery. Squeeze more out of every charge in one tap, with the latest tweaks for iOS 26.',
            pairs: [{ key: 'savemybattery v2.2 automation', label: 'V2.2 Automation', note: 'Runs this for you at a battery level you pick · iOS 27' }],
            older: [{ key: 'savemybattery v2.1', label: 'V2.1', note: 'previous version' }, { key: 'savemybattery v1', label: 'V1', note: 'for older setups' }],
            link: 'https://www.icloud.com/shortcuts/53346b499365410c8f4109ff3bc56e5b'
        },
        'savemybattery v2.2 automation': {
            glyph: 'bolt', tint: '#E8455F', soft: ['#FBE7EA', '#F3D0D6', '#361A21', '#52272F'], category: 'Battery', needs: 'iOS 27',
            short: 'Runs V2.2 when your battery drops to a level you pick.',
            pitch: 'Runs V2.2 for you when your battery drops to a level you pick.',
            desc: 'Runs SaveMyBattery V2.2 for you the moment your battery drops to a percentage you pick. Needs iOS 27 and SaveMyBattery V2.2 installed first.',
            pairs: [{ key: 'savemybattery v2.2', label: 'SaveMyBattery V2.2', note: 'Install this first · it does the saving' }],
            link: 'https://www.icloud.com/shortcuts/780ac51dcc514b9ba12e04f78e9ef53b'
        },
        'savemybattery v2.1': {
            glyph: 'bolt', tint: '#2E9E63', soft: ['#F9E8E5', '#F2D5D0', '#3B1915', '#592922'], category: 'Battery',
            short: 'Low power mode, less transparency and motion.',
            desc: 'Optimize battery life in one tap: low power mode, reduced transparency and motion.',
            link: 'https://www.icloud.com/shortcuts/32e766396219425e8d29eaf0e4c4a161'
        },
        'savemybattery v1': {
            glyph: 'battery', tint: '#7C7C85', soft: ['#FAE8E5', '#F3D5D0', '#3B1915', '#592922'], category: 'Battery',
            short: 'The original. Kept for older setups.',
            desc: 'The original SaveMyBattery. Kept for older setups.',
            link: 'https://www.icloud.com/shortcuts/594fff3adae8400faf5a903167f0854d'
        },
        'coolbgremover': {
            glyph: 'scissors', tint: '#E58300', soft: ['#E6ECFC', '#D3DCF7', '#192242', '#293563'], category: 'Images',
            short: 'Remove backgrounds from images instantly.',
            desc: 'Remove backgrounds from images instantly.',
            link: 'https://www.icloud.com/shortcuts/c9d90103e0eb4a56bcde227b8006c9b7'
        },
        'coolimageeditor': {
            glyph: 'image', tint: '#A64AE8', soft: ['#E6ECFC', '#D3DCF7', '#192242', '#293563'], category: 'Images',
            short: 'Crop, convert, resize and more.',
            desc: 'Quick image editing: crop, convert, resize and more.',
            link: 'https://www.icloud.com/shortcuts/b9d34799af7248e084e08671549c297d'
        },
        'leaf blower w/ google search': {
            title: 'Leaf Blower w/ Google Search',
            glyph: 'leaf', tint: '#2F9E55', soft: ['#E4F0E6', '#CEE3D3', '#0E2C18', '#184327'], category: 'Voice',
            short: 'A very dumb Siri alternative. Search by voice.',
            desc: 'A very dumb Siri alternative. Search the web using just your voice via Google Search.',
            link: 'https://www.icloud.com/shortcuts/a52c67fa1d68460abee42b63831bbae5'
        },
        'leaf blower w/ google gemini': {
            title: 'Leaf Blower w/ Google Gemini',
            glyph: 'sparkle', tint: '#2E95C7', soft: ['#E4F0E6', '#CEE3D3', '#0E2C18', '#184327'], category: 'Voice',
            short: 'Leaf Blower with Gemini for smarter answers.',
            desc: 'Leaf Blower powered by Google Gemini for smarter voice answers.',
            link: 'https://www.icloud.com/shortcuts/9a3c7bc343cb474e94b8ac83828f494b'
        },
        'editable materials': {
            glyph: 'cube', tint: '#D49500', soft: ['#E6ECFB', '#D3DCF6', '#1A2241', '#2A3661'], category: 'Productivity',
            short: 'Edit files in Google Classroom Materials.',
            desc: 'Edit files in the Materials section of Google Classroom.',
            link: 'https://www.icloud.com/shortcuts/d5e5fe1db65745a891e6e81038ed238f'
        },
        'deviceinfo': {
            glyph: 'tablet', tint: '#55555C', soft: ['#E6ECFC', '#D3DCF6', '#1A2241', '#2A3562'], category: 'Utilities',
            short: 'Detailed info about your device at a glance.',
            desc: 'See detailed information about your device at a glance.',
            link: 'https://www.icloud.com/shortcuts/ca35bc3d75814583af3461518c8badf8'
        },
        'moo cleanup tool': {
            glyph: 'broom', tint: '#D9384F', soft: ['#E6ECFC', '#D2DCF8', '#192243', '#293564'], category: 'Utilities',
            short: 'Clean up leftovers and junk.',
            desc: 'Clean up leftovers and junk. New in version 44!',
            link: 'https://www.icloud.com/shortcuts/fa85f39337b049d4b175ca978d9a9966'
        },
        '[api] notarobot api v1.1': {
            glyph: 'terminal', tint: '#1F7AE0', soft: ['#E6ECFC', '#D3DCF7', '#192242', '#293563'], category: 'Developer',
            short: 'Verification API for shortcut developers.',
            desc: 'NotARobot verification API for shortcut developers.',
            link: 'https://www.icloud.com/shortcuts/642810ae87534d64873d19a5498948f4'
        },
        'kool menu': {
            title: 'Kool Menu',
            glyph: 'archive', tint: '#8E8E93', tintDark: '#6E6E76', soft: ['#E6ECFC', '#D3DCF6', '#1A2241', '#2A3562'], category: 'Legacy',
            short: 'The original Kool Menu. No longer maintained.',
            desc: 'The original Kool Menu. No longer maintained.',
            link: 'https://www.icloud.com/shortcuts/9c0322bfe63647fb9782128d388325f7'
        },
        'abel\'s url compressor': {
            glyph: 'link', tint: '#2F6FE8', soft: ['#E6ECFC', '#D3DCF7', '#1A2242', '#2A3563'], category: 'Utilities',
            short: 'Shrink long links into short, shareable TinyURLs.',
            pitch: 'Shrink long links into short, shareable TinyURLs in one tap.',
            desc: 'Shrink long links into short, shareable TinyURLs in one tap. Paste or share a URL and get a compact link back.',
            link: 'https://www.icloud.com/shortcuts/9b3fadd93afa4c0c8e051223ce70f6ce'
        }
    };
    META['editable matrials'] = META['editable materials']; // older spelling in some lists

    var DEFAULT_META = {
        glyph: 'wrench', tint: '#55555C', soft: ['#ECECED', '#DDDCDE', '#252426', '#39383B'], category: 'Other',
        short: 'An Abel Tools shortcut.', desc: 'An Abel Tools shortcut.'
    };

    // Category colors: [dot, dark dot, chip background, chip text, dark chip background]
    var CATS = {
        'Productivity': ['#0A7AE8', '#3B93F0', '#EBF2FF', '#185AA7', '#1F2C41'],
        'Customization': ['#5E5CE6', '#8583F0', '#F0F0FF', '#4C4CAC', '#2B283F'],
        'Battery': ['#2E9E63', '#3FBF7A', '#EAF5EF', '#1D6B43', '#173226'],
        'Images': ['#E58300', '#F09A2A', '#FAF0E6', '#844B03', '#382913'],
        'Voice': ['#2E95C7', '#4AB3E0', '#EBF3FA', '#1D6285', '#1D2E39'],
        'Utilities': ['#55555C', '#9C9CA6', '#F2F2F2', '#5A5A5F', '#2C2B2D'],
        'Developer': ['#1F7AE0', '#4B95EA', '#EBF2FF', '#215AA2', '#212C3F'],
        'Legacy': ['#A1401C', '#F08A65', '#FBEFEA', '#8A442B', '#3B261C'],
        'Other': ['#55555C', '#9C9CA6', '#F2F2F2', '#5A5A5F', '#2C2B2D']
    };
    var CAT_ORDER = ['Productivity', 'Customization', 'Battery', 'Images', 'Voice', 'Utilities', 'Developer'];

    function catColors(name) { return CATS[name] || CATS.Other; }

    function paintCat(node, name) {
        var c = catColors(name);
        node.style.setProperty('--c', c[0]);
        node.style.setProperty('--cd', c[1]);
        node.style.setProperty('--cb', c[2]);
        node.style.setProperty('--ci', c[3]);
        node.style.setProperty('--cbd', c[4]);
    }

    /* ================= State ================= */

    function normalize(name) { return name.replace(/\[EOL\]/gi, '').trim().toLowerCase(); }
    function parseNameList(value) {
        if (!value) return [];
        return value.split(',').map(normalize).filter(Boolean);
    }

    var installed = parseNameList(params.get('installed'));
    var updates = parseNameList(params.get('updates'));
    var catalog = [];
    var catalogByKey = Object.create(null);
    var catalogReady = false;
    var newNames = [];
    var activeCategory = 'All';
    var searchQuery = '';
    var sortMode = 0; // 0 = Featured, 1 = A-Z, 2 = Category

    function statusFor(item) {
        if (item.eol) return 'EOL';
        if (updates.indexOf(item.key) !== -1) return 'UPDATE';
        if (installed.indexOf(item.key) !== -1) return 'INSTALLED';
        return 'GET';
    }

    // The shortcut reports what this device has; a retired one still counts
    // as being on it.
    function isOnDevice(item) {
        return installed.indexOf(item.key) !== -1 || updates.indexOf(item.key) !== -1;
    }

    function deepLink(item) {
        return 'shortcuts://run-shortcut?name=' + encodeURIComponent(SELF_NAME) +
               '&input=text&text=' + encodeURIComponent('install:' + item.name);
    }

    /* ================= Favorites =================
       Kept on the device under one versioned envelope. Abel Tools SYNC sends
       this exact shape to the account and merges whatever comes back (see the
       sync seam near the end). */

    var FAV_KEY = 'abeltools-favorites';

    function readFavorites() {
        try {
            var data = JSON.parse(localStorage.getItem(FAV_KEY) || 'null');
            if (data && Array.isArray(data.keys)) {
                return {
                    keys: data.keys.map(normalize).filter(Boolean),
                    updatedAt: typeof data.updatedAt === 'number' ? data.updatedAt : 0
                };
            }
        } catch (e) { /* unreadable or blocked storage: start with none */ }
        return { keys: [], updatedAt: 0 };
    }

    var favState = readFavorites();

    function saveFavorites() {
        try {
            localStorage.setItem(FAV_KEY, JSON.stringify({
                v: 1,
                keys: favState.keys,
                updatedAt: favState.updatedAt
            }));
        } catch (e) { /* storage full or blocked: favorites last for this session */ }
    }

    function isFavorite(key) { return favState.keys.indexOf(key) !== -1; }

    // Favorites for shortcuts that have left the catalog are kept on purpose:
    // a shortcut can come back, and the list fetch can fail.
    function favoriteCount() {
        return catalog.filter(function (item) { return isFavorite(item.key); }).length;
    }

    function toggleFavorite(key) {
        var i = favState.keys.indexOf(key);
        if (i === -1) favState.keys.push(key); else favState.keys.splice(i, 1);
        touchPrefs();
        return i === -1;
    }

    /* ================= Preference stamp and mirror =================
       Favorites, theme mode and accent are one preference set with one
       timestamp, so sync can settle conflicts with last write wins. A theme
       change has to move the same clock as a favorite, or a device that only
       changed its accent would never win a merge.

       localStorage is the store. The cookie is a mirror for web views that
       block or partition it, which is the case where a saved look appears to
       reset on every launch. Neither survives Safari clearing site data, that
       is what signing in will fix. */

    var applyingRemote = false; // set while a synced snapshot is being applied

    function touchPrefs() {
        if (applyingRemote) return; // remote data keeps the sender's timestamp
        favState.updatedAt = Date.now();
        saveFavorites();
        schedulePush(); // no-op until this device is signed in
    }

    var LOOK_COOKIE = 'abeltools-look';

    function readCookie(name) {
        try {
            var m = document.cookie.match(new RegExp('(?:^|; )' + name + '=([^;]*)'));
            return m ? decodeURIComponent(m[1]) : '';
        } catch (e) { return ''; }
    }

    function saveLook() {
        try {
            document.cookie = LOOK_COOKIE + '=' + encodeURIComponent(themeMode + '|' + currentAccent) +
                ';path=/;max-age=31536000;SameSite=Lax;Secure';
        } catch (e) { /* cookies blocked: localStorage is still the store */ }
    }

    function readLook() {
        var parts = readCookie(LOOK_COOKIE).split('|');
        return { mode: parts[0] || '', accent: parts[1] || '' };
    }

    function popStar(node) {
        node.classList.remove('star-pop');
        void node.offsetWidth; // restart the animation
        node.classList.add('star-pop');
    }

    /* ================= Header date ================= */

    $('dateEyebrow').textContent =
        new Date().toLocaleDateString('en-US', { weekday: 'long', month: 'long', day: 'numeric' }).toUpperCase();

    /* ================= Theme ================= */

    var themeBtn = $('themeBtn');
    var themeIcon = $('themeIcon');
    var root = document.documentElement;

    var ACCENTS = ['blue', 'indigo', 'purple', 'pink', 'red', 'orange', 'green', 'graphite'];
    // Swatch colors are the light accents, so a swatch looks the same in both themes
    var ACCENT_SWATCH = {
        blue: '#2742E8', indigo: '#5B4FE0', purple: '#8B3FF0', pink: '#D6307F',
        red: '#D42A4B', orange: '#E0640F', green: '#138A55', graphite: '#4F5663'
    };

    function systemDark() {
        return !!(window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches);
    }

    function isMode(m) { return m === 'auto' || m === 'light' || m === 'dark'; }
    function cap(s) { return s ? s.charAt(0).toUpperCase() + s.slice(1) : s; }

    // Order matters: what this device chose wins, then the cookie mirror, and
    // only then ?theme= / ?accent= from the shortcut. Those params used to be
    // read first, which quietly overrode a saved choice on every launch.
    function initialMode() {
        try {
            var m = localStorage.getItem('abeltools-thememode');
            if (isMode(m)) return m;
            var old = localStorage.getItem('abeltools-theme'); // migrate legacy key
            if (old === 'dark' || old === 'light') return old;
        } catch (e) { /* localStorage may be unavailable in web view */ }
        var mirrored = readLook().mode;
        if (isMode(mirrored)) return mirrored;
        var forced = params.get('theme'); // first run only
        if (forced === 'dark' || forced === 'light') return forced;
        return 'auto';
    }

    function initialAccent() {
        try {
            var a = localStorage.getItem('abeltools-accent');
            if (a && ACCENTS.indexOf(a) !== -1) return a;
        } catch (e) {}
        var mirrored = readLook().accent;
        if (ACCENTS.indexOf(mirrored) !== -1) return mirrored;
        var forced = params.get('accent'); // first run only
        if (forced && ACCENTS.indexOf(forced) !== -1) return forced;
        return 'blue';
    }

    var themeMode = initialMode();      // 'auto' | 'light' | 'dark'
    var currentTheme;                   // resolved 'light' | 'dark'
    var currentAccent = initialAccent();

    function resolvedTheme() {
        return themeMode === 'auto' ? (systemDark() ? 'dark' : 'light') : themeMode;
    }

    function applyTheme(theme) {
        if (theme === 'dark') root.setAttribute('data-theme', 'dark');
        else root.removeAttribute('data-theme');
        themeIcon.innerHTML = theme === 'dark' ? ICONS.sun : ICONS.moon;
        themeBtn.setAttribute('aria-label', theme === 'dark' ? 'Switch to light mode' : 'Switch to dark mode');
    }

    function applyAccent(name) {
        if (ACCENTS.indexOf(name) === -1) name = 'blue';
        currentAccent = name;
        if (name === 'blue') root.removeAttribute('data-accent');
        else root.setAttribute('data-accent', name);
    }

    function syncTheme() {
        currentTheme = resolvedTheme();
        applyTheme(currentTheme);
    }

    function lookLabel() { return cap(themeMode) + ' · ' + cap(currentAccent); }

    applyAccent(currentAccent);
    syncTheme();

    // Write back whatever we resolved, so a look recovered from the cookie or
    // from a URL param becomes this device's own saved choice from now on.
    try {
        localStorage.setItem('abeltools-thememode', themeMode);
        localStorage.setItem('abeltools-accent', currentAccent);
    } catch (e) {}
    saveLook();

    // Follow the system automatically while in Auto mode.
    if (window.matchMedia) {
        var mq = window.matchMedia('(prefers-color-scheme: dark)');
        var onMq = function () { if (themeMode === 'auto') syncTheme(); };
        if (mq.addEventListener) mq.addEventListener('change', onMq);
        else if (mq.addListener) mq.addListener(onMq);
    }

    function setMode(mode) {
        themeMode = mode;
        try { localStorage.setItem('abeltools-thememode', mode); } catch (e) {}
        saveLook();
        touchPrefs();
        syncTheme();
        updateAppearanceUI();
    }

    function setAccent(name) {
        applyAccent(name);
        try { localStorage.setItem('abeltools-accent', name); } catch (e) {}
        saveLook();
        touchPrefs();
        updateAppearanceUI();
    }

    // Header toggle: quick flip between light and dark (steps out of Auto).
    themeBtn.addEventListener('click', function () {
        setMode(currentTheme === 'dark' ? 'light' : 'dark');
    });

    /* ================= Appearance page ================= */

    var modeCards = $('modeCards');
    var swatchesEl = $('swatches');

    ACCENTS.forEach(function (name) {
        var b = el('button', 'swatch');
        b.type = 'button';
        b.setAttribute('data-accent', name);
        b.setAttribute('aria-label', cap(name) + ' accent');
        b.style.setProperty('--sw', ACCENT_SWATCH[name]);
        b.innerHTML = '<span class="sw-dot"></span>';
        b.appendChild(el('span', 'sw-name', cap(name)));
        b.addEventListener('click', function () { setAccent(name); });
        swatchesEl.appendChild(b);
    });

    Array.prototype.forEach.call(modeCards.querySelectorAll('.theme-card'), function (btn) {
        btn.addEventListener('click', function () { setMode(btn.getAttribute('data-mode')); });
    });

    $('pvTile').replaceWith(tile({ key: 'quickscreen', tint: META.quickscreen.tint, glyph: META.quickscreen.glyph }, 40));

    function fillAll(name, text) {
        Array.prototype.forEach.call(document.querySelectorAll('[data-fill="' + name + '"]'), function (node) {
            node.textContent = text;
        });
    }

    function updateAppearanceUI() {
        Array.prototype.forEach.call(modeCards.querySelectorAll('.theme-card'), function (btn) {
            var on = btn.getAttribute('data-mode') === themeMode;
            btn.setAttribute('aria-pressed', on ? 'true' : 'false');
            var radio = btn.querySelector('.radio');
            radio.classList.toggle('on', on);
            radio.innerHTML = on ? icon('check', 13, 3.2) : '';
        });
        Array.prototype.forEach.call(swatchesEl.querySelectorAll('.swatch'), function (btn) {
            var on = btn.getAttribute('data-accent') === currentAccent;
            btn.setAttribute('aria-pressed', on ? 'true' : 'false');
            btn.querySelector('.sw-dot').innerHTML = on ? icon('check', 16, 3.2) : '';
        });
        fillAll('look', lookLabel());
    }
    updateAppearanceUI();

    /* ================= Navigation =================
       Three main views share the sidebar; Settings swaps in its own sidebar
       and pages. The body scrolls, the sidebar stays put. */

    var mainSide = $('mainSide');
    var setSide = $('setSide');
    var topbar = $('topbar');
    var tabs = $('tabs');
    var VIEWS = { discover: $('viewDiscover'), favorites: $('viewFavorites'), library: $('viewLibrary') };
    var PAGES = { sync: $('pageSync'), appearance: $('pageAppearance'), about: $('pageAbout') };
    var VIEW_NAMES = { discover: 'Discover', favorites: 'Favorites', library: 'Library' };
    var currentView = 'discover';
    var lastMainView = 'discover';
    var settingsPage = 'appearance';

    function showView(name) {
        currentView = name;
        var inSettings = name === 'settings';
        if (!inSettings) lastMainView = name;

        mainSide.hidden = inSettings;
        topbar.hidden = inSettings;
        tabs.hidden = inSettings;
        setSide.hidden = !inSettings;
        Object.keys(VIEWS).forEach(function (k) { VIEWS[k].hidden = k !== name; });
        Object.keys(PAGES).forEach(function (k) { PAGES[k].hidden = !(inSettings && k === settingsPage); });

        Array.prototype.forEach.call(document.querySelectorAll('.nav-btn[data-go], .tab[data-go]'), function (b) {
            if (b.getAttribute('data-go') === name) b.setAttribute('aria-current', 'page');
            else b.removeAttribute('aria-current');
        });
        Array.prototype.forEach.call(setSide.querySelectorAll('.set-item'), function (b) {
            if (b.getAttribute('data-page') === settingsPage) b.setAttribute('aria-current', 'page');
            else b.removeAttribute('aria-current');
        });
        $('setBackLabel').textContent = VIEW_NAMES[lastMainView];
        $('catGroup').hidden = name === 'library' || !catalogReady;

        renderCurrent();
        window.scrollTo(0, 0);
    }

    // Repaint whatever is on screen without moving it, for data that arrives
    // in the background (the catalog, a sync).
    function renderCurrent() {
        if (currentView === 'discover') renderDiscover();
        else if (currentView === 'favorites') renderFavorites();
        else if (currentView === 'library') renderLibrary();
        else if (settingsPage === 'sync') renderAccount();
    }

    function openSettings(page) {
        settingsPage = page;
        showView('settings');
    }

    // Anything with data-go switches main view; Discover from the nav also
    // steps out of a category.
    document.addEventListener('click', function (e) {
        var go = e.target.closest('[data-go]');
        if (go) {
            if (go.getAttribute('data-go') === 'discover') { activeCategory = 'All'; }
            showView(go.getAttribute('data-go'));
            return;
        }
        var s = e.target.closest('[data-settings]');
        if (s) openSettings(s.getAttribute('data-settings'));
    });

    Array.prototype.forEach.call(setSide.querySelectorAll('.set-item'), function (b) {
        b.addEventListener('click', function () { openSettings(b.getAttribute('data-page')); });
    });
    $('setBack').addEventListener('click', function () { showView(lastMainView); });
    $('settingsBtn').addEventListener('click', function () { openSettings('appearance'); });
    $('topSettings').addEventListener('click', function () { openSettings('appearance'); });
    $('syncCard').addEventListener('click', function () { openSettings('sync'); });

    /* ================= Sidebar counts and categories ================= */

    var catList = $('catList');
    var catStrip = $('catStrip');

    function categoryCounts() {
        var counts = Object.create(null);
        catalog.forEach(function (item) { counts[item.category] = (counts[item.category] || 0) + 1; });
        var order = CAT_ORDER.filter(function (c) { return counts[c]; });
        Object.keys(counts).forEach(function (c) {
            if (order.indexOf(c) === -1 && c !== 'Legacy') order.push(c);
        });
        if (counts.Legacy) order.push('Legacy'); // retired tools always sit last
        return order.map(function (c) { return { name: c, count: counts[c] }; });
    }

    function pickCategory(name) {
        activeCategory = activeCategory === name ? 'All' : name;
        if (currentView !== 'discover') showView('discover');
        else renderDiscover();
    }

    function renderCategories() {
        var cats = categoryCounts();
        catList.innerHTML = '';
        catStrip.innerHTML = '';
        $('catGroup').hidden = cats.length === 0 || currentView === 'library';

        var all = el('button', 'cat-chip');
        all.type = 'button';
        all.setAttribute('data-cat', 'All');
        all.appendChild(el('span', null, 'All'));
        all.appendChild(el('span', 'cat-count', String(catalog.length)));
        all.addEventListener('click', function () { activeCategory = 'All'; renderDiscover(); });
        catStrip.appendChild(all);

        cats.forEach(function (c) {
            [['cat-btn', catList], ['cat-chip', catStrip]].forEach(function (pair) {
                var b = el('button', pair[0]);
                b.type = 'button';
                b.setAttribute('data-cat', c.name);
                paintCat(b, c.name);
                b.appendChild(el('span', 'cat-dot'));
                b.appendChild(el('span', 'cat-name', c.name));
                b.appendChild(el('span', 'cat-count', String(c.count)));
                b.addEventListener('click', function () { pickCategory(c.name); });
                pair[1].appendChild(b);
            });
        });
        paintCategoryUI();
    }

    function paintCategoryUI() {
        Array.prototype.forEach.call(document.querySelectorAll('[data-cat]'), function (b) {
            var on = currentView === 'discover' && b.getAttribute('data-cat') === activeCategory;
            b.setAttribute('aria-pressed', on ? 'true' : 'false');
        });
    }

    function renderNavCounts() {
        var favs = favoriteCount();
        var upd = catalog.filter(function (i) { return statusFor(i) === 'UPDATE'; }).length;
        fillAll('favcount', favs > 0 ? String(favs) : '');
        Array.prototype.forEach.call(document.querySelectorAll('[data-fill="updbadge"]'), function (b) {
            b.textContent = String(upd);
            b.hidden = upd === 0;
        });
    }

    /* ================= Rows and buttons ================= */

    // GET/UPDATE open the confirm, whose link does the installing; installed
    // and retired are labels only.
    function actionButton(item, size) {
        var status = statusFor(item);
        var sz = size ? ' sz-' + size : '';
        if (status === 'EOL') return el('span', 'pill pill-ret' + sz, 'Retired');
        if (status === 'INSTALLED') {
            var s = el('span', 'pill pill-inst' + sz);
            s.innerHTML = icon('check', 14, 2.6) + 'Installed';
            return s;
        }
        // The cards on Discover use the solid button for GET as well
        var solid = status === 'UPDATE' || size === 'spot';
        var b = el('button', 'pill ' + (solid ? 'pill-upd' : 'pill-get') + sz, status === 'UPDATE' ? 'Update' : 'Get');
        b.type = 'button';
        b.setAttribute('aria-label', (status === 'UPDATE' ? 'Update ' : 'Get ') + item.title);
        b.addEventListener('click', function (e) {
            e.stopPropagation();
            openConfirm(item);
        });
        return b;
    }

    var starsByList = { discover: Object.create(null), favorites: Object.create(null) };

    function favLabel(item, on) {
        return on ? 'Remove ' + item.title + ' from favorites' : 'Add ' + item.title + ' to favorites';
    }

    function paintStar(btn, item) {
        var on = isFavorite(item.key);
        btn.classList.toggle('on', on);
        btn.innerHTML = starSvg(20, on);
        btn.setAttribute('aria-pressed', on ? 'true' : 'false');
        btn.setAttribute('aria-label', favLabel(item, on));
    }

    function buildStar(item, listName) {
        var btn = el('button', 'star-btn');
        btn.type = 'button';
        paintStar(btn, item);
        btn.addEventListener('click', function (e) {
            e.stopPropagation(); // the rest of the row opens the detail panel
            toggleFavorite(item.key);
            popStar(btn);
            favoritesChanged(item);
        });
        starsByList[listName][item.key] = btn;
        return btn;
    }

    // Single place that repaints everything a favorite touches.
    function favoritesChanged(item) {
        renderNavCounts();
        if (currentView === 'favorites') renderFavorites();
        Object.keys(starsByList).forEach(function (n) {
            var b = starsByList[n][item.key];
            if (b && b.isConnected) paintStar(b, item);
        });
        if (sheetItem && sheetItem.key === item.key) paintSheetFav();
        if (currentView === 'library') renderLibrary();
        renderAccount();
    }

    function openOnActivate(node, item) {
        node.addEventListener('click', function (e) {
            if (e.target.closest('.pill') || e.target.closest('.star-btn')) return;
            openSheet(item);
        });
        node.addEventListener('keydown', function (e) {
            if (e.target !== node) return;
            if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); openSheet(item); }
        });
    }

    function buildRow(item, listName) {
        var row = el('div', 'row' + (item.eol ? ' is-eol' : ''));
        row.setAttribute('role', 'button');
        row.setAttribute('tabindex', '0');
        row.setAttribute('aria-label', 'View details for ' + item.title);

        var info = el('div', 'row-info');
        var top = el('div', 'row-top');
        top.appendChild(el('span', 'row-name', item.title));
        if (item.isNew && !item.eol) top.appendChild(el('span', 'badge-new sm', 'NEW'));
        info.appendChild(top);
        info.appendChild(el('span', 'row-sub', item.category + ' · ' + item.short));

        var act = el('div', 'row-act');
        act.appendChild(actionButton(item));

        row.appendChild(tile(item, 44));
        row.appendChild(info);
        row.appendChild(buildStar(item, listName));
        row.appendChild(act);
        openOnActivate(row, item);
        return row;
    }

    /* ================= Discover ================= */

    var listEl = $('list');
    var listEmpty = $('listEmpty');
    var updateGrid = $('updateGrid');

    function matchesFilters(item) {
        if (activeCategory !== 'All' && item.category !== activeCategory) return false;
        if (searchQuery && item.title.toLowerCase().indexOf(searchQuery) === -1 &&
            item.name.toLowerCase().indexOf(searchQuery) === -1 &&
            item.category.toLowerCase().indexOf(searchQuery) === -1 &&
            item.desc.toLowerCase().indexOf(searchQuery) === -1) return false;
        return true;
    }

    function featuredSort(items) {
        // Featured: NEW shortcuts first, EOL last, otherwise list order
        return items.sort(function (a, b) {
            return (b.isNew - a.isNew) || (a.eol - b.eol) || (a.order - b.order);
        });
    }

    function sortedCatalog(items) {
        if (sortMode === 1) {
            return items.sort(function (a, b) { return a.title.localeCompare(b.title); });
        }
        if (sortMode === 2) {
            var rank = function (c) { var i = CAT_ORDER.indexOf(c); return c === 'Legacy' ? 99 : (i === -1 ? 50 : i); };
            return items.sort(function (a, b) {
                return (rank(a.category) - rank(b.category)) || a.title.localeCompare(b.title);
            });
        }
        return featuredSort(items);
    }

    function renderSpotlights() {
        Array.prototype.slice.call(updateGrid.querySelectorAll('.spot')).forEach(function (n) {
            updateGrid.removeChild(n);
        });
        var fresh = catalog.filter(function (i) { return i.isNew && !i.eol; }).slice(0, 2);
        updateGrid.className = 'update-grid n' + fresh.length;

        fresh.forEach(function (item) {
            var card = el('div', 'spot');
            card.style.setProperty('--s1', item.soft[0]);
            card.style.setProperty('--s2', item.soft[1]);
            card.style.setProperty('--s3', item.soft[2]);
            card.style.setProperty('--s4', item.soft[3]);
            card.setAttribute('role', 'button');
            card.setAttribute('tabindex', '0');
            card.setAttribute('aria-label', 'View details for ' + item.title);

            var top = el('div', 'spot-top');
            top.appendChild(tile(item, 52));
            top.appendChild(el('span', 'badge-new', 'NEW'));

            var body = el('div', 'spot-body');
            body.appendChild(el('span', 'spot-name', item.title));
            body.appendChild(el('span', 'spot-desc', item.pitch));

            var foot = el('div', 'spot-foot');
            foot.appendChild(el('span', 'spot-meta', item.category + (item.needs ? ' · Needs ' + item.needs : '')));
            foot.appendChild(actionButton(item, 'spot'));

            card.appendChild(top);
            card.appendChild(body);
            card.appendChild(foot);
            openOnActivate(card, item);
            updateGrid.appendChild(card);
        });
    }

    function renderDiscover() {
        paintCategoryUI();
        if (!catalogReady) return;

        // The update cards decorate the default browse view only
        var browsing = activeCategory === 'All' && !searchQuery;
        updateGrid.hidden = !browsing;
        if (browsing) renderSpotlights();

        var items = sortedCatalog(catalog.filter(matchesFilters));
        $('listTitle').textContent = searchQuery ? 'Search results'
            : (activeCategory !== 'All' ? activeCategory : 'All shortcuts');
        $('listCount').textContent = String(items.length);

        listEl.innerHTML = '';
        listEl.removeAttribute('aria-busy');
        starsByList.discover = Object.create(null);
        items.forEach(function (item) { listEl.appendChild(buildRow(item, 'discover')); });
        listEl.hidden = items.length === 0;
        listEmpty.hidden = items.length !== 0;
    }

    /* ================= Search and sort ================= */

    var searchInput = $('searchInput');

    searchInput.addEventListener('input', function () {
        searchQuery = searchInput.value.trim().toLowerCase();
        renderDiscover();
    });

    $('emptyClear').addEventListener('click', function () {
        searchInput.value = '';
        searchQuery = '';
        activeCategory = 'All';
        renderDiscover();
    });

    var sortSeg = $('sortSeg');
    Array.prototype.forEach.call(sortSeg.querySelectorAll('.seg-btn'), function (btn) {
        btn.addEventListener('click', function () {
            sortMode = Number(btn.getAttribute('data-sort'));
            Array.prototype.forEach.call(sortSeg.querySelectorAll('.seg-btn'), function (b) {
                b.setAttribute('aria-pressed', b === btn ? 'true' : 'false');
            });
            renderDiscover();
        });
    });

    /* ================= Favorites view ================= */

    function renderFavorites() {
        if (!catalogReady) return;
        var items = featuredSort(catalog.filter(function (i) { return isFavorite(i.key); }));
        var none = items.length === 0;
        $('favEmpty').hidden = !none;
        $('favHint').hidden = !none;
        $('favFull').hidden = none;
        $('favHeadCount').textContent = none ? '' : String(items.length);

        var favList = $('favList');
        favList.innerHTML = '';
        starsByList.favorites = Object.create(null);
        items.forEach(function (item) { favList.appendChild(buildRow(item, 'favorites')); });
    }

    /* ================= Library view ================= */

    function libRow(item) {
        var status = statusFor(item);
        var row = el('div', 'inst-row');
        row.setAttribute('role', 'button');
        row.setAttribute('tabindex', '0');
        row.setAttribute('aria-label', 'View details for ' + item.title);
        var info = el('div', 'inst-info');
        info.appendChild(el('span', 'inst-name', item.title));
        info.appendChild(el('span', 'inst-cat', item.category));
        row.appendChild(tile(item, 44));
        row.appendChild(info);
        if (status === 'UPDATE') {
            row.appendChild(el('span', 'st-ready', 'Update ready'));
        } else {
            var ok = el('span', 'st-ok');
            ok.innerHTML = icon('check', 14, 2.6) + 'Up to date';
            row.appendChild(ok);
        }
        openOnActivate(row, item);
        return row;
    }

    function renderLibrary() {
        if (!catalogReady) return;
        var onDevice = catalog.filter(function (i) { return !i.eol && isOnDevice(i); });
        var waiting = onDevice.filter(function (i) { return statusFor(i) === 'UPDATE'; });
        // As drawn, Retired lists every retired tool, and counts never treat
        // one as installed.
        var retired = catalog.filter(function (i) { return i.eol; });
        var favs = favoriteCount();

        $('libUpdates').hidden = waiting.length === 0;
        $('libInstalled').hidden = onDevice.length === 0;
        $('libRetired').hidden = retired.length === 0;
        $('libEmpty').hidden = onDevice.length > 0;

        $('libUpdCount').textContent = String(waiting.length);
        var updList = $('libUpdList');
        updList.innerHTML = '';
        waiting.forEach(function (item) {
            var card = el('div', 'upd-card');
            card.setAttribute('role', 'button');
            card.setAttribute('tabindex', '0');
            card.setAttribute('aria-label', 'View details for ' + item.title);
            var info = el('div', 'upd-info');
            info.appendChild(el('span', 'upd-name', item.title));
            info.appendChild(el('span', 'upd-text', 'A newer version is ready. Your favorites and settings stay as they are.'));
            card.appendChild(tile(item, 56));
            card.appendChild(info);
            card.appendChild(actionButton(item, 'xl'));
            openOnActivate(card, item);
            updList.appendChild(card);
        });

        $('libInstCount').textContent = String(onDevice.length);
        var instList = $('libInstList');
        instList.innerHTML = '';
        // Updates lead, the rest keep catalog order
        onDevice.slice().sort(function (a, b) {
            return (statusFor(a) === 'UPDATE' ? 0 : 1) - (statusFor(b) === 'UPDATE' ? 0 : 1) || a.order - b.order;
        }).forEach(function (item) { instList.appendChild(libRow(item)); });

        $('libRetCount').textContent = String(retired.length);
        var retList = $('libRetList');
        retList.innerHTML = '';
        retired.forEach(function (item) {
            var card = el('div', 'ret-card');
            card.setAttribute('role', 'button');
            card.setAttribute('tabindex', '0');
            card.setAttribute('aria-label', 'View details for ' + item.title);
            var info = el('div', 'inst-info');
            info.appendChild(el('span', 'inst-name', item.title));
            info.appendChild(el('span', 'inst-cat', 'No longer maintained. It won\'t get updates.'));
            card.appendChild(tile(item, 44));
            card.appendChild(info);
            card.appendChild(el('span', 'st-ret', 'Retired'));
            openOnActivate(card, item);
            retList.appendChild(card);
        });

        $('glInstalled').textContent = String(onDevice.length);
        $('glUpdates').textContent = String(waiting.length);
        $('glUpdatesCap').textContent = waiting.length === 1 ? 'update ready' : 'updates ready';
        $('glMissing').textContent = String(catalog.length - onDevice.length);
        $('glFavs').textContent = String(favs);
        $('glFavsCap').textContent = favs === 1 ? 'favorite' : 'favorites';
        $('glBrowse').textContent = 'Browse all ' + catalog.length;
    }

    /* ================= Detail panel ================= */

    var sheet = $('sheet');
    var sheetScrim = $('sheetScrim');
    var sheetBody = $('sheetBody');
    var sheetItem = null;     // the item the panel is currently showing
    var sheetFav = null;
    var sheetReturn = null;   // where focus goes back to when it closes

    var STATUS_LINE = {
        GET: ['Not installed', 'var(--muted)', 'var(--muted-2)'],
        UPDATE: ['Installed · update ready', 'var(--accent-ink)', 'var(--accent)'],
        INSTALLED: ['Installed · up to date', 'var(--ink-2)', '#2E9E63'],
        EOL: ['Retired · no longer maintained', 'var(--retired)', 'var(--retired)']
    };
    var STATUS_FACT = { GET: 'Not installed', UPDATE: 'Update ready', INSTALLED: 'Installed', EOL: 'Retired' };

    function paintSheetFav() {
        if (!sheetItem || !sheetFav) return;
        var on = isFavorite(sheetItem.key);
        sheetFav.classList.toggle('on', on);
        sheetFav.setAttribute('aria-pressed', on ? 'true' : 'false');
        sheetFav.setAttribute('aria-label', favLabel(sheetItem, on));
        sheetFav.innerHTML = starSvg(22, on, 1.6);
    }

    function primaryAction(item) {
        var status = statusFor(item);
        if (status === 'INSTALLED' || status === 'EOL') {
            var s = el('span', 'p-primary is-static');
            s.innerHTML = status === 'INSTALLED' ? icon('check', 18, 2.4) + 'Installed' : 'Retired';
            return s;
        }
        var b = el('button', 'p-primary');
        b.type = 'button';
        b.innerHTML = icon('download', 18, 2.2);
        b.appendChild(document.createTextNode(status === 'UPDATE' ? 'Update' : 'Get'));
        b.addEventListener('click', function () { openConfirm(item); });
        return b;
    }

    function fact(term, value) {
        var d = el('div', 'fact');
        d.appendChild(el('dt', null, term));
        d.appendChild(el('dd', null, value));
        return d;
    }

    function fillSheet(item) {
        var status = statusFor(item);
        sheetItem = item;

        var chip = $('sheetChip');
        paintCat(chip, item.category);
        $('sheetChipText').textContent = item.category;

        sheetBody.innerHTML = '';
        sheetBody.scrollTop = 0;

        var top = el('div', 'p-top');
        top.appendChild(tile(item, 84));
        var titles = el('div', 'p-titles');
        var name = el('h2', 'p-name', item.title);
        name.id = 'sheetName';
        titles.appendChild(name);
        var line = STATUS_LINE[status];
        var st = el('span', 'p-status');
        st.style.setProperty('--st', line[1]);
        st.style.setProperty('--sd', line[2]);
        st.appendChild(el('i'));
        st.appendChild(document.createTextNode(line[0]));
        titles.appendChild(st);
        top.appendChild(titles);
        sheetBody.appendChild(top);

        var actions = el('div', 'p-actions');
        actions.appendChild(primaryAction(item));
        sheetFav = el('button', 'p-fav');
        sheetFav.type = 'button';
        sheetFav.addEventListener('click', function () {
            toggleFavorite(item.key);
            popStar(sheetFav);
            favoritesChanged(item);
        });
        actions.appendChild(sheetFav);
        paintSheetFav();
        sheetBody.appendChild(actions);

        sheetBody.appendChild(el('p', 'p-desc', item.desc));

        var facts = el('dl', 'facts');
        facts.appendChild(fact('CATEGORY', item.category));
        facts.appendChild(fact('STATUS', STATUS_FACT[status]));
        facts.appendChild(fact('INSTALLS AS', 'Apple Shortcut'));
        facts.appendChild(fact('OPENS IN', 'Shortcuts app'));
        sheetBody.appendChild(facts);

        var pairs = (item.pairs || []).filter(function (p) { return catalogByKey[p.key]; });
        if (pairs.length) {
            var sec = el('div', 'p-sec');
            sec.appendChild(el('h3', 'p-h3', 'Works with'));
            pairs.forEach(function (p) {
                var other = catalogByKey[p.key];
                var row = el('div', 'pair');
                row.setAttribute('role', 'button');
                row.setAttribute('tabindex', '0');
                row.setAttribute('aria-label', 'View details for ' + other.title);
                var info = el('div', 'pair-info');
                var nm = el('span', 'pair-name', p.label);
                if (other.isNew && !other.eol) nm.appendChild(el('span', 'badge-new sm tight', 'NEW'));
                info.appendChild(nm);
                info.appendChild(el('span', 'pair-note', p.note));
                row.appendChild(tile(other, 44));
                row.appendChild(info);
                row.appendChild(actionButton(other, 'sm'));
                openOnActivate(row, other);
                sec.appendChild(row);
            });
            sheetBody.appendChild(sec);
        }

        var older = (item.older || []).filter(function (o) { return catalogByKey[o.key]; });
        if (older.length) {
            var osec = el('div', 'p-sec');
            osec.appendChild(el('h3', 'p-h3', 'Older versions'));
            var chips = el('div', 'olds');
            older.forEach(function (o) {
                var c = el('span', 'old', o.label);
                c.appendChild(el('span', null, '· ' + (isOnDevice(catalogByKey[o.key]) ? 'installed' : o.note)));
                chips.appendChild(c);
            });
            osec.appendChild(chips);
            sheetBody.appendChild(osec);
        }
    }

    function openSheet(item) {
        if (!sheet.classList.contains('open')) sheetReturn = document.activeElement;
        fillSheet(item);
        sheet.classList.add('open');
        sheetScrim.classList.add('open');
        document.body.style.overflow = 'hidden';
        sheet.focus({ preventScroll: true });
    }

    function closeSheet() {
        if (!sheet.classList.contains('open')) return;
        sheet.classList.remove('open');
        sheetScrim.classList.remove('open');
        document.body.style.overflow = '';
        sheetItem = null;
        sheetFav = null;
        if (sheetReturn && sheetReturn.isConnected && sheetReturn.focus) sheetReturn.focus({ preventScroll: true });
        sheetReturn = null;
    }

    $('sheetClose').addEventListener('click', closeSheet);
    sheetScrim.addEventListener('click', closeSheet);

    // At phone width the panel is a bottom sheet: drag it down to dismiss.
    (function () {
        var startY = 0, dy = 0, dragging = false;
        var narrow = window.matchMedia ? window.matchMedia('(max-width: 760px)') : null;
        sheet.addEventListener('touchstart', function (e) {
            if (!narrow || !narrow.matches || sheetBody.scrollTop > 0) return;
            startY = e.touches[0].clientY;
            dy = 0;
            dragging = true;
        }, { passive: true });
        sheet.addEventListener('touchmove', function (e) {
            if (!dragging) return;
            dy = e.touches[0].clientY - startY;
            if (dy <= 0) { // upward: hand the gesture back to scrolling
                dragging = false;
                sheet.style.transition = '';
                sheet.style.transform = '';
                return;
            }
            e.preventDefault();
            sheet.style.transition = 'none';
            sheet.style.transform = 'translateY(' + dy + 'px)';
        }, { passive: false });
        sheet.addEventListener('touchend', function () {
            if (!dragging) return;
            dragging = false;
            // Clearing inline styles in the same frame lets the CSS
            // transition pick up from the dragged position.
            sheet.style.transition = '';
            sheet.style.transform = '';
            if (dy > 110) closeSheet();
        });
    })();

    /* ================= Install confirm ================= */

    var alertBox = $('alert');
    var alertScrim = $('alertScrim');
    var alertContinue = $('alertContinue');
    var alertReturn = null;

    function openConfirm(item) {
        alertReturn = document.activeElement;
        var iconNode = $('alertIcon');
        iconNode.innerHTML = '';
        iconNode.appendChild(tile(item, 60));
        $('alertTitle').textContent = (statusFor(item) === 'UPDATE' ? 'Update ' : 'Get ') + item.title + '?';
        // iCloud links open natively in any web view; deep link is the fallback
        alertContinue.href = item.link || deepLink(item);
        alertBox.classList.add('open');
        alertScrim.classList.add('open');
        $('alertCancel').focus({ preventScroll: true });
    }

    function closeConfirm() {
        if (!alertBox.classList.contains('open')) return;
        alertBox.classList.remove('open');
        alertScrim.classList.remove('open');
        if (alertReturn && alertReturn.isConnected && alertReturn.focus) alertReturn.focus({ preventScroll: true });
        alertReturn = null;
    }

    $('alertCancel').addEventListener('click', closeConfirm);
    alertScrim.addEventListener('click', closeConfirm);
    alertContinue.addEventListener('click', function () {
        // Let navigation proceed, then tidy up the dialog
        alertReturn = null;
        closeConfirm();
        closeSheet();
    });

    document.addEventListener('keydown', function (e) {
        if (e.key !== 'Escape') return;
        if (alertBox.classList.contains('open')) { closeConfirm(); return; }
        closeSheet();
    });

    /* ================= Announcement ================= */

    function renderAnnouncement(text) {
        text = (text || '').trim();
        if (!text) return;
        try {
            if (localStorage.getItem('abeltools-announce-dismissed') === text) return;
        } catch (e) {}

        $('noticeText').textContent = text;
        var notice = $('notice');
        notice.hidden = false;
        $('noticeClose').addEventListener('click', function () {
            notice.hidden = true;
            try { localStorage.setItem('abeltools-announce-dismissed', text); } catch (e) {}
        });
    }

    /* ================= What's new ================= */

    function renderChangelog(md) {
        var listNode = $('wnList');
        var items = md.split('\n')
            .map(function (l) { return l.trim(); })
            .filter(function (l) { return /^[-*+]\s+/.test(l); })
            .map(function (l) { return l.replace(/^[-*+]\s+/, ''); });

        listNode.innerHTML = '';
        if (items.length === 0) items = [md.trim() || 'No changelog available.'];
        items.forEach(function (text) {
            var li = document.createElement('li');
            li.innerHTML = icon('check', 16, 2.6);
            li.appendChild(el('span', null, text));
            listNode.appendChild(li);
        });
    }

    /* ================= Data loading ================= */

    // Fallback snapshot used if GitHub is unreachable (mirrors shortcutslist.md).
    var FALLBACK_LIST = [
        'kool Menu [EOL]', 'Abel\'s URL Compressor', 'Quickscreen', 'AnythingButGlass',
        'SaveMyBattery V2.2', 'SaveMyBattery V2.2 Automation',
        'SaveMyBattery V2.1', 'SaveMyBattery V1',
        'CoolBGRemover', 'CoolImageEditor',
        'leaf blower w/ Google Search', 'leaf blower w/ Google Gemini',
        'Editable Materials', 'DeviceInfo', 'Moo Cleanup Tool', '[API] NotARobot API V1.1'
    ];

    function buildCatalog(lines) {
        catalogByKey = Object.create(null);
        catalog = lines
            .map(function (l) { return l.trim(); })
            .filter(Boolean)
            .map(function (rawName, order) {
                var eol = /\[EOL\]/i.test(rawName);
                var key = normalize(rawName);
                var meta = META[key] || DEFAULT_META;
                var name = rawName.replace(/\s*\[EOL\]\s*/i, ' ').trim();
                var item = {
                    name: name,                   // as listed; installs and deep links use it
                    title: meta.title || name,    // as shown
                    key: key,
                    order: order,
                    eol: eol,
                    isNew: newNames.indexOf(key) !== -1,
                    glyph: meta.glyph,
                    tint: meta.tint,
                    tintDark: meta.tintDark || null,
                    soft: meta.soft || DEFAULT_META.soft,
                    link: meta.link || null,
                    category: eol ? 'Legacy' : meta.category,
                    short: meta.short,
                    pitch: meta.pitch || meta.short,
                    desc: meta.desc,
                    needs: meta.needs || null,
                    pairs: meta.pairs || null,
                    older: meta.older || null
                };
                catalogByKey[key] = item;
                return item;
            });
        catalogReady = true;
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
        fetchApi('newversion').then(function (v) {
            var version = v.trim();
            fillAll('installer', 'Installer · v' + version);
            fillAll('vtag', 'v' + version);
            fillAll('version', 'Version ' + version);
        }).catch(function () {
            fillAll('installer', 'Installer · v?');
            fillAll('version', 'Version ?');
        });

        fetchApi('newchangelog').then(renderChangelog).catch(function () {
            $('wnList').innerHTML = '<li><span>Could not load changelog.</span></li>';
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
            searchInput.placeholder = 'Search ' + catalog.length + ' shortcuts';
            renderCategories();
            renderNavCounts();
            renderCurrent();
        });
    }

    showView('discover');
    init();

    /* ================= Sync seam (for Abel Tools SYNC) =================
       snapshot() is what this device holds, and merge() takes what the
       account holds. Favorites, theme mode and accent share one timestamp,
       and last write wins on the whole snapshot, so a device that has been
       offline for a week cannot wipe changes made since. */

    window.AbelToolsPrefs = {
        snapshot: function () {
            return {
                v: 1,
                updatedAt: favState.updatedAt,
                favorites: favState.keys.slice(),
                theme: { mode: themeMode, accent: currentAccent }
            };
        },
        // Three ways in, because plain last write wins is wrong twice over. On a
        // first sign in it throws away whichever list happens to be older, and
        // on a restore it refuses the backup for being old, which is the one
        // time being old is the whole point.
        //
        //   default   the account copy is taken only when it is newer
        //   'union'   first sync on this device: keep both lists
        //   'restore' the backup wins outright and is stamped now
        merge: function (remote, mode) {
            if (!remote || !Array.isArray(remote.favorites)) return false;
            var remoteKeys = remote.favorites.map(normalize).filter(Boolean);
            var remoteAt = typeof remote.updatedAt === 'number' ? remote.updatedAt : 0;
            var localAt = favState.updatedAt;
            var keys, stamp, takeTheme;

            if (mode === 'restore') {
                keys = remoteKeys;
                stamp = Date.now(); // newest everywhere, so other devices take it too
                takeTheme = true;
            } else if (mode === 'union') {
                keys = favState.keys.slice();
                remoteKeys.forEach(function (key) {
                    if (keys.indexOf(key) === -1) keys.push(key);
                });
                takeTheme = remoteAt > localAt;
                if (keys.length === favState.keys.length && !takeTheme) return false;
                stamp = Math.max(remoteAt, localAt, Date.now());
            } else {
                if (remoteAt <= localAt) return false; // this device is newer
                keys = remoteKeys;
                stamp = remoteAt;
                takeTheme = true;
            }

            applyingRemote = true;
            try {
                favState.keys = keys;
                favState.updatedAt = stamp;
                saveFavorites();
                if (takeTheme) {
                    var theme = remote.theme || {};
                    if (isMode(theme.mode)) setMode(theme.mode);
                    if (ACCENTS.indexOf(theme.accent) !== -1) setAccent(theme.accent);
                }
            } finally {
                applyingRemote = false;
            }
            renderNavCounts();
            renderCurrent();
            return true;
        }
    };

    /* ================= Account and sync =================
       Sign in is Supabase Auth, spoken to over its own REST endpoints so the
       installer stays one self-contained file with no auth SDK. Tokens live
       on this device. Preferences travel through /api/sync, which verifies
       the token and is the only thing that ever sees the spreadsheet.

       This is the installer's own sign in on purpose: the Shortcuts web view
       keeps a separate cookie and storage jar, so signing in at achenkunju.com
       in Safari does not carry over here. */

    var AUTH_KEY = 'abeltools-auth';
    var LAST_SYNC_KEY = 'abeltools-lastsync';

    // Accounts are Supabase Auth, a fork of the same GoTrue that Netlify
    // Identity ran, so this talks to it over the same REST shapes as before.
    // The anon key belongs in the page: it is the key the browser is meant to
    // hold and it grants nothing on its own.
    var SUPABASE_URL = 'https://buqtnbhyuufyymfgvoyx.supabase.co';
    var SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImJ1cXRuYmh5dXVmeXltZmd2b3l4Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3ODg3NjM4NzUsImV4cCI6MjEwNDMzOTg3NX0.ptsLo9yCspgyxyZGb2EnBMIyYWCVirQfhfFCo2zB2cA';
    var IDENTITY_BASE = SUPABASE_URL + '/auth/v1';

    var syncSignIn = $('syncSignIn');
    var syncCode = $('syncCode');
    var syncSignedIn = $('syncSignedIn');
    var acctForm = $('acctForm');
    var acctSubmit = $('acctSubmit');
    var acctEmailInput = $('acctEmail');
    var acctPasswordInput = $('acctPassword');
    var modeSignIn = $('modeSignIn');
    var modeSignUp = $('modeSignUp');

    var acctMfaForm = $('acctMfaForm');
    var acctMfaSubmit = $('acctMfaSubmit');
    var digits = Array.prototype.slice.call(acctMfaForm.querySelectorAll('.digit'));

    var signupMode = false;
    var syncTimer = null;
    var syncInFlight = false;
    var mfaChecking = false;

    // A password gets an aal1 session. If the account has a verified factor
    // that session is real but unfinished, and /api/sync refuses it, which is
    // what makes the installer a closed door rather than a way around the
    // code prompt on the website.
    var mfaPending = false;
    var mfaFactor = null;
    var mfaChallenge = null;

    var MAX_BACKUPS = 5; // matches the sheet, which is what actually enforces it
    var backups = [];
    var SYNCED_KEY = 'abeltools-synced-with';

    var SYNC_MESSAGES = {
        pulled: 'Brought this iPad up to date',
        pushed: 'Saved to your account',
        merged: 'Merged this iPad with your account. Nothing was lost.',
        backed: 'Backed up',
        restored: 'Backup restored here and saved to your account',
        removed: 'Backup removed'
    };

    function readStored(key) {
        try { return JSON.parse(localStorage.getItem(key) || 'null'); } catch (e) { return null; }
    }

    var session = (function () {
        var saved = readStored(AUTH_KEY);
        return (saved && saved.access_token && saved.refresh_token) ? saved : null;
    })();

    var lastSyncedAt = Number(readStored(LAST_SYNC_KEY)) || 0;

    function saveSession(next) {
        session = next;
        try {
            if (next) localStorage.setItem(AUTH_KEY, JSON.stringify(next));
            else localStorage.removeItem(AUTH_KEY);
        } catch (e) { /* storage blocked: this sign in lasts for the session */ }
    }

    function markSynced() {
        lastSyncedAt = Date.now();
        try { localStorage.setItem(LAST_SYNC_KEY, String(lastSyncedAt)); } catch (e) {}
    }

    function identityCall(path, options) {
        options = options || {};
        // Every Supabase auth call carries the anon key, on top of whatever
        // headers the caller wanted.
        var headers = { apikey: SUPABASE_ANON_KEY };
        Object.keys(options.headers || {}).forEach(function (name) {
            headers[name] = options.headers[name];
        });
        options.headers = headers;
        return fetch(IDENTITY_BASE + path, options).then(function (r) {
            return r.text().then(function (text) {
                var body;
                try { body = JSON.parse(text); } catch (e) { body = {}; }
                if (!r.ok) {
                    throw new Error(body.error_description || body.msg || body.error ||
                        ('Could not reach the account service (' + r.status + ')'));
                }
                return body;
            });
        });
    }

    function storeToken(token) {
        saveSession({
            access_token: token.access_token,
            refresh_token: token.refresh_token,
            // Refresh a minute early so a slow request never lands on a dead token
            expires_at: Date.now() + ((token.expires_in || 3600) * 1000) - 60000
        });
        return token;
    }

    function passwordGrant(email, password) {
        return identityCall('/token?grant_type=password', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ email: email, password: password })
        }).then(storeToken);
    }

    function accessToken() {
        if (!session) return Promise.reject(new Error('Sign in to sync.'));
        if (Date.now() < session.expires_at) return Promise.resolve(session.access_token);
        return identityCall('/token?grant_type=refresh_token', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ refresh_token: session.refresh_token })
        }).then(function (token) {
            storeToken(token);
            return session.access_token;
        }).catch(function (err) {
            saveSession(null); // the refresh token is dead, ask for a fresh sign in
            renderAccount();
            throw err;
        });
    }

    // Display only. The server reads the account from the token itself, so
    // nothing here is ever trusted for identity.
    function sessionClaims() {
        if (!session) return {};
        try {
            var part = session.access_token.split('.')[1].replace(/-/g, '+').replace(/_/g, '/');
            while (part.length % 4) part += '=';
            return JSON.parse(atob(part)) || {};
        } catch (e) { return {}; }
    }

    function sessionEmail() { return sessionClaims().email || ''; }

    function deviceId() {
        try { return (window.AbelID && AbelID.getState().id) || ''; } catch (e) { return ''; }
    }

    function identityAuthed(path, options) {
        return accessToken().then(function (token) {
            options = options || {};
            options.headers = options.headers || {};
            options.headers.Authorization = 'Bearer ' + token;
            return identityCall(path, options);
        });
    }

    function newChallenge() {
        return identityAuthed('/factors/' + mfaFactor + '/challenge', { method: 'POST' })
            .then(function (challenge) { mfaChallenge = challenge.id; });
    }

    // Reached when the server says a second factor is owed. Finds the factor
    // and opens a challenge, so the code the user types has something to be
    // checked against.
    function enterMfa() {
        return identityAuthed('/user', {}).then(function (user) {
            var factors = (user.factors || []).filter(function (f) {
                return f.factor_type === 'totp' && f.status === 'verified';
            });
            if (!factors.length) return false;
            mfaFactor = factors[0].id;
            return newChallenge().then(function () {
                mfaPending = true;
                clearCode();
                renderAccount();
                setAcctMsg('', '');
                if (currentView === 'settings' && settingsPage === 'sync') digits[0].focus();
                return true;
            });
        });
    }

    function syncCall(payload) {
        payload.deviceId = deviceId();
        return accessToken().then(function (token) {
            return fetch(API_BASE + 'sync', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json', 'Authorization': 'Bearer ' + token },
                body: JSON.stringify(payload)
            });
        }).then(function (r) {
            return r.text().then(function (text) {
                var body;
                try { body = JSON.parse(text); } catch (e) { body = {}; }
                if (!r.ok || body.error) throw new Error(body.error || ('Sync failed (' + r.status + ')'));
                return body;
            });
        });
    }

    function pushPrefs() {
        return syncCall({ action: 'put', data: window.AbelToolsPrefs.snapshot() })
            .then(function () { markSynced(); return 'pushed'; });
    }

    // Signing in on a device is remembered per account, because the very first
    // sync is the dangerous one: both sides hold real data and neither is a
    // copy of the other, so that one time the lists are unioned instead.
    function deviceHasSynced() {
        return readStored(SYNCED_KEY) === (sessionEmail() || 'account');
    }

    function markDeviceSynced() {
        try { localStorage.setItem(SYNCED_KEY, JSON.stringify(sessionEmail() || 'account')); } catch (e) {}
    }

    // Pull first: if the account is ahead, this device takes its data. If not,
    // this device is the newer one and sends its own up.
    function pullPrefs() {
        return syncCall({ action: 'get' }).then(function (res) {
            backups = res.backups || [];
            renderBackups();
            var first = !deviceHasSynced();
            markDeviceSynced();
            if (res.data && window.AbelToolsPrefs.merge(res.data, first ? 'union' : null)) {
                if (!first) { markSynced(); return 'pulled'; }
                // A union leaves this device holding the superset, so it goes up.
                return pushPrefs().then(function () { return 'merged'; });
            }
            return pushPrefs();
        });
    }

    function backupNow() {
        return syncCall({ action: 'backup', data: window.AbelToolsPrefs.snapshot() })
            .then(function (res) {
                backups = res.backups || [];
                renderBackups();
                return 'backed';
            });
    }

    // Restoring writes the backup straight back up to the account as the newest
    // copy. Without that push the next device to sync would still be holding
    // newer data and would undo the restore.
    function restoreBackup(id) {
        var entry = null;
        backups.forEach(function (b) { if (b.id === id) entry = b; });
        if (!entry) return Promise.reject(new Error('That backup is not there any more.'));
        window.AbelToolsPrefs.merge(entry.data, 'restore');
        return pushPrefs().then(function () { return 'restored'; });
    }

    function removeBackup(id) {
        return syncCall({ action: 'deleteBackup', backupId: id })
            .then(function (res) {
                backups = res.backups || [];
                renderBackups();
                return 'removed';
            });
    }

    function backupSummary(data) {
        var count = (data && Array.isArray(data.favorites)) ? data.favorites.length : 0;
        var theme = (data && data.theme) || {};
        var bits = [count + (count === 1 ? ' favorite' : ' favorites')];
        if (theme.mode && theme.mode !== 'auto') bits.push(theme.mode);
        if (theme.accent) bits.push(theme.accent);
        return bits.join(', ');
    }

    function backupWhen(entry) {
        var ts = Date.parse(entry && entry.createdAt);
        return isNaN(ts) ? 'saved' : relativeTime(ts);
    }

    // Restore and remove each throw something away, so both ask twice. The
    // second tap has to land within a few seconds, which keeps a stray tap in a
    // scrolling list from taking a backup with it. Only one is ever armed.
    var disarmCurrent = null;

    function armedButton(label, kind, whenEl, ask, run) {
        var btn = el('button', 'bk-btn ' + kind, label);
        var timer = null;
        btn.type = 'button';

        function disarm() {
            clearTimeout(timer);
            timer = null;
            btn.classList.remove('armed');
            btn.textContent = label;
            whenEl.className = 'bk-when';
            whenEl.textContent = whenEl.getAttribute('data-when');
            if (disarmCurrent === disarm) disarmCurrent = null;
        }

        btn.addEventListener('click', function () {
            if (timer) {
                disarm();
                runSync(run, true);
                return;
            }
            if (disarmCurrent) disarmCurrent();
            disarmCurrent = disarm;
            btn.classList.add('armed');
            btn.textContent = 'Tap again';
            whenEl.className = 'bk-when ' + (kind === 'remove' ? 'warn' : 'ask');
            whenEl.textContent = ask;
            timer = setTimeout(disarm, 4000);
        });
        return btn;
    }

    function renderBackups() {
        var full = backups.length >= MAX_BACKUPS;
        if (disarmCurrent) disarmCurrent();
        $('acctBackupCount').textContent = backups.length + ' of ' + MAX_BACKUPS + ' slots';
        $('backupEmpty').hidden = backups.length > 0;

        var slots = $('bkSlots');
        slots.innerHTML = '';
        for (var i = 0; i < MAX_BACKUPS; i++) slots.appendChild(el('span', 'slot' + (i < backups.length ? ' on' : '')));

        $('acctBackup').disabled = full;
        $('acctBackupLabel').textContent = full ? 'All ' + MAX_BACKUPS + ' slots are full' : 'Back up now';

        var list = $('backupList');
        list.innerHTML = '';
        backups.forEach(function (entry) {
            var row = el('li', 'bk-row');
            var ic = el('span', 'bk-ic');
            ic.innerHTML = icon('archive', 18, 2);

            var info = el('span', 'bk-info');
            info.appendChild(el('span', 'bk-title', backupSummary(entry.data)));
            var when = el('span', 'bk-when', backupWhen(entry));
            when.setAttribute('data-when', when.textContent);
            info.appendChild(when);

            row.appendChild(ic);
            row.appendChild(info);
            row.appendChild(armedButton('Restore', 'restore', when,
                'Restore this backup? It replaces this iPad\'s favorites and look.', function () {
                    return restoreBackup(entry.id);
                }));
            row.appendChild(armedButton('Remove', 'remove', when, 'Remove this backup for good?', function () {
                return removeBackup(entry.id);
            }));
            list.appendChild(row);
        });
    }

    // Local changes come in bursts (starring three shortcuts in a row), so they
    // settle into one push instead of one request per tap.
    function schedulePush() {
        if (!session) return;
        clearTimeout(syncTimer);
        syncTimer = setTimeout(function () { runSync(pushPrefs, false); }, 1500);
    }

    function runSync(work, loud) {
        if (syncInFlight) return Promise.resolve();
        syncInFlight = true;
        if (loud) setAcctMsg('', 'Syncing…');
        return work().then(function (how) {
            syncInFlight = false;
            renderAccount();
            if (loud) setAcctMsg('ok', SYNC_MESSAGES[how] || 'Done');
        }, function (err) {
            syncInFlight = false;
            // The server is the one that knows a factor is owed, so this is
            // driven by its answer rather than by guessing up front. That keeps
            // the common case at zero extra requests.
            if (/two factor/i.test(err.message)) {
                return enterMfa().then(function (started) {
                    if (started) return;
                    renderAccount();
                    setAcctMsg('error', err.message);
                }, function () {
                    renderAccount();
                    setAcctMsg('error', err.message);
                });
            }
            renderAccount();
            setAcctMsg('error', err.message);
        });
    }

    // One message, shown wherever the account page currently is: under the
    // sign in form, under the code, or in the signed-in header.
    function setAcctMsg(kind, text) {
        [$('signInMsg'), $('codeMsg')].forEach(function (node) {
            node.className = 'form-msg' + (kind ? ' ' + kind : '');
            node.textContent = text || '';
            node.hidden = !text;
        });
        var pill = $('syncPill');
        pill.className = 'status-pill' + (kind ? ' ' + kind : '');
        pill.innerHTML = kind === 'ok' ? icon('check', 15, 2.8) : (kind === 'error' ? icon('alert', 15, 2.4) : '');
        pill.appendChild(el('span', null, text || ''));
        pill.hidden = !text;
    }

    function relativeTime(ts) {
        if (!ts) return 'never';
        var mins = Math.round((Date.now() - ts) / 60000);
        if (mins < 1) return 'just now';
        if (mins < 60) return mins + (mins === 1 ? ' min ago' : ' mins ago');
        var hours = Math.round(mins / 60);
        if (hours < 24) return hours + (hours === 1 ? ' hour ago' : ' hours ago');
        var days = Math.round(hours / 24);
        return days + (days === 1 ? ' day ago' : ' days ago');
    }

    // The sidebar card and the Settings row say where the account stands.
    function renderSyncEntry() {
        var pending = !!session && mfaPending;
        var signedIn = !!session && !mfaPending;
        var avatar = $('syncAvatar');
        var title = $('syncTitle');
        var sub = $('syncSub');
        var setSub = $('setSyncSub');
        var email = sessionEmail();

        avatar.classList.toggle('is-initial', signedIn);
        if (signedIn) avatar.textContent = (email.charAt(0) || 'A').toUpperCase();
        else avatar.innerHTML = icon('user', 18, 2);

        if (pending) {
            title.textContent = 'Finish signing in';
            sub.textContent = 'Code needed';
            setSub.textContent = 'Code needed';
        } else if (signedIn) {
            title.textContent = email || 'Abel Tools account';
            sub.textContent = lastSyncedAt ? 'Synced ' + relativeTime(lastSyncedAt) : 'Signed in';
            setSub.textContent = sub.textContent;
        } else {
            title.textContent = 'Sign in to Sync';
            sub.textContent = 'Favorites on every iPad';
            setSub.textContent = 'Not signed in';
        }
        sub.classList.toggle('is-alert', pending);
        setSub.classList.toggle('is-alert', pending);
    }

    function renderAccount() {
        var pending = !!session && mfaPending;
        var signedIn = !!session && !mfaPending;
        syncSignIn.hidden = !!session;
        syncCode.hidden = !pending;
        syncSignedIn.hidden = !signedIn;
        renderSyncEntry();
        if (!signedIn) return;

        var email = sessionEmail();
        $('acctAvatar').textContent = (email.charAt(0) || 'A').toUpperCase();
        $('acctWho').textContent = email || 'Abel Tools account';
        $('acctWhoSub').textContent = 'Signed in on this iPad' +
            (sessionClaims().aal === 'aal2' ? ' · two-factor on' : '');
        $('statFav').textContent = String(favState.keys.length);
        $('statLast').textContent = cap(relativeTime(lastSyncedAt));
    }

    // "Synced 3 mins ago" should not freeze while the installer stays open
    setInterval(function () { if (session) renderAccount(); }, 60000);

    function setSignupMode(on) {
        signupMode = on;
        modeSignIn.setAttribute('aria-pressed', on ? 'false' : 'true');
        modeSignUp.setAttribute('aria-pressed', on ? 'true' : 'false');
        acctSubmit.textContent = on ? 'Create account' : 'Sign in';
        acctPasswordInput.setAttribute('autocomplete', on ? 'new-password' : 'current-password');
    }

    modeSignIn.addEventListener('click', function () { setSignupMode(false); setAcctMsg('', ''); });
    modeSignUp.addEventListener('click', function () { setSignupMode(true); setAcctMsg('', ''); });

    $('pwShow').addEventListener('click', function () {
        var show = acctPasswordInput.type === 'password';
        acctPasswordInput.type = show ? 'text' : 'password';
        this.textContent = show ? 'Hide' : 'Show';
        this.setAttribute('aria-pressed', show ? 'true' : 'false');
        this.setAttribute('aria-label', show ? 'Hide password' : 'Show password');
    });

    acctForm.addEventListener('submit', function (e) {
        e.preventDefault();
        var email = acctEmailInput.value.trim();
        var password = acctPasswordInput.value;
        if (!email || !password) { setAcctMsg('error', 'Enter your email and password.'); return; }
        acctSubmit.disabled = true;
        setAcctMsg('', signupMode ? 'Creating your account…' : 'Signing in…');

        var work = signupMode
            ? identityCall('/signup', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ email: email, password: password })
            }).then(function () {
                setSignupMode(false);
                setAcctMsg('ok', 'Account created. Confirm it from the email sent to ' + email + ', then sign in.');
            })
            : passwordGrant(email, password).then(function () {
                acctPasswordInput.value = '';
                renderAccount();
                return runSync(pullPrefs, true);
            });

        work.catch(function (err) {
            setAcctMsg('error', err.message);
        }).then(function () {
            acctSubmit.disabled = false;
        });
    });

    /* Six boxes, one code. Typing moves along, backspace moves back, and a
       pasted or autofilled code spreads across the boxes from wherever it
       lands, since autofill only ever fills the first. */

    function codeValue() { return digits.map(function (d) { return d.value; }).join(''); }

    function paintVerify() { acctMfaSubmit.disabled = mfaChecking || codeValue().length !== 6; }

    function clearCode() {
        digits.forEach(function (d) { d.value = ''; });
        paintVerify();
    }

    function spreadCode(from, text) {
        var chars = text.replace(/\D/g, '').split('');
        for (var i = from; i < digits.length && chars.length; i++) digits[i].value = chars.shift();
        var next = digits.filter(function (d) { return !d.value; })[0] || digits[digits.length - 1];
        next.focus();
        paintVerify();
    }

    digits.forEach(function (d, i) {
        d.addEventListener('input', function () {
            var v = d.value.replace(/\D/g, '');
            if (v.length > 1) { d.value = ''; spreadCode(i, v); return; }
            d.value = v;
            if (v && i < digits.length - 1) digits[i + 1].focus();
            paintVerify();
        });
        d.addEventListener('keydown', function (e) {
            if (e.key === 'Backspace' && !d.value && i > 0) {
                e.preventDefault();
                digits[i - 1].value = '';
                digits[i - 1].focus();
                paintVerify();
            } else if (e.key === 'ArrowLeft' && i > 0) {
                digits[i - 1].focus();
            } else if (e.key === 'ArrowRight' && i < digits.length - 1) {
                digits[i + 1].focus();
            }
        });
        d.addEventListener('paste', function (e) {
            var t = (e.clipboardData || window.clipboardData).getData('text');
            if (!t) return;
            e.preventDefault();
            spreadCode(i, t);
        });
        d.addEventListener('focus', function () { if (d.select) d.select(); });
    });

    acctMfaForm.addEventListener('submit', function (e) {
        e.preventDefault();
        var code = codeValue();
        if (code.length !== 6) { setAcctMsg('error', 'Enter the 6 digit code.'); return; }
        mfaChecking = true;
        paintVerify();
        setAcctMsg('', 'Checking…');
        identityAuthed('/factors/' + mfaFactor + '/verify', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ challenge_id: mfaChallenge, code: code })
        }).then(function (token) {
            storeToken(token); // the verified session comes back at aal2
            mfaPending = false;
            clearCode();
            renderAccount();
            return runSync(pullPrefs, true);
        }, function (err) {
            setAcctMsg('error', err.message);
            clearCode();
            digits[0].focus();
            // A rejected code burns its challenge, so open a fresh one.
            return newChallenge().catch(function () {});
        }).then(function () {
            mfaChecking = false;
            paintVerify();
        });
    });

    $('acctMfaCancel').addEventListener('click', function () {
        saveSession(null);
        mfaPending = false;
        mfaFactor = null;
        mfaChallenge = null;
        clearCode();
        renderAccount();
        setAcctMsg('', '');
    });

    $('acctSync').addEventListener('click', function () {
        runSync(pullPrefs, true);
    });

    $('acctBackup').addEventListener('click', function () {
        runSync(backupNow, true);
    });

    $('acctSignOut').addEventListener('click', function () {
        // Local sign out only: favorites and the look stay on this device, and
        // the account's copy in the sheet is left untouched.
        saveSession(null);
        mfaPending = false;
        backups = []; // the account's backups are still in the account, just not shown here
        renderBackups();
        renderAccount();
        setAcctMsg('', 'Signed out. Your favorites stay on this iPad.');
    });

    setSignupMode(false);
    renderAccount();
    renderBackups();

    // A signed-in device catches up quietly as soon as the installer opens.
    if (session) runSync(pullPrefs, false);

    /* ================= AbelDeviceID card =================
       Shows the device's shared AbelDeviceID on the About page, with a copy
       button. Reads the existing AbelID module state; never generates or
       stores anything itself (generation stays in the AbelDeviceID gate). */
    (function () {
        var value = $('abelIdValue');
        var state = $('abelIdState');
        var copy = $('abelIdCopy');
        var copyLabel = $('abelIdCopyLabel');
        if (!window.AbelID) {
            value.textContent = 'Unavailable';
            state.lastChild.textContent = 'Not checked';
            state.style.setProperty('--dot', '#9C9CA6');
            return;
        }
        var STATES = {
            active: ['Verified', 'var(--lime)'],
            checking: ['Checking', '#9C9CA6'],
            missing: ['Not generated', '#9C9CA6'],
            banned: ['Banned', '#F08A65']
        };
        function upd() {
            var s = AbelID.getState();
            var look = STATES[s.status] || STATES.checking;
            value.textContent = s.id || (s.status === 'checking' ? 'Checking…' : 'Not generated');
            state.lastChild.textContent = look[0];
            state.style.setProperty('--dot', look[1]);
            copy.disabled = !s.id;
        }
        upd();
        AbelID.onChange(upd);
        copy.addEventListener('click', function () {
            var id = AbelID.getState().id;
            if (!id || !navigator.clipboard) return;
            navigator.clipboard.writeText(id).then(function () {
                copyLabel.textContent = 'Copied';
                setTimeout(function () { copyLabel.textContent = 'Copy ID'; }, 1200);
            }).catch(function () {});
        });
    })();
})();
</script>
</body>
</html>
