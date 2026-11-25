# Interactive prototypes with Artifacts: default prototype banner

Use these instructions every time you build an interactive prototype as a Claude Artifact (a single HTML page). Every prototype starts with the same top banner. It has three default switchers: **Device**, **Width** (breakpoints) and **Grid**, plus a live breakpoint readout. Project-specific switchers (pages, variants, states) come after them.

The reference build is the HOT Stores and Consultants prototype. A tested starter file is at the end of this document.

---

## 1. When to use this

- Any clickable prototype, microsite or responsive page built as an Artifact.
- Any time the prototype needs reviewing at more than one breakpoint, or checking against the layout grid.
- Skip it only for a one-off inline visual in chat.

## 2. The banner at a glance

```
PROTOTYPE  Device [Fit|Desktop|Tablet|Mobile]  Width [Fit|390|768|1024|1280|1440|1920]  Grid [Off|On]  |  <project switchers>      1280px · xl 1280
```

| Order | Group | Options | What it does |
|---|---|---|---|
| 1 | Device | Fit, Desktop, Tablet, Mobile | Picks the frame. Fit fills the window. Desktop is a 1440 browser frame. Tablet is 768 x 1024 and Mobile is 390 x 812, both in a dark device bezel. |
| 2 | Width | Fit, 390, 768, 1024, 1280, 1440, 1920 | Sets the exact frame width. Picking a width also updates Device (under 768 is Mobile, 768 to 1023 is Tablet, 1024 and up is Desktop). |
| 3 | Grid | Off, On | Shows the 12-column layout grid (4 columns on mobile) over the page, with the live site margins and gutters. |
| 4 | Readout | (right side) | Live text like `1280px · xl 1280 · shown at 74%`, so you always know the real width and breakpoint, even when the frame is scaled down to fit. |
| 5+ | Project switchers | Page, variants, states | After a thin divider. One segmented control per decision you want to show the client. |

Defaults on load: Device Fit, Width Fit, Grid Off. The viewer's last Width and Grid choice is remembered in their browser.

Keyboard shortcuts (ignored while typing in a field): **G** toggles the grid. **1, 2, 3, 4** pick Fit, Desktop, Tablet, Mobile.

## 3. How the frame works (the rule everything depends on)

1. **`#app` is the viewport.** The whole prototype lives inside `#app`, never directly in `body`. The page scrolls inside `#scroller`, not the window.
2. **Use container queries, never media queries, for layout.** `#app` has `container-type: inline-size; container-name: app`. Write breakpoints as `@container app (max-width: 767px)`. Media queries read the browser window, which is wrong when the frame is 375 wide inside a 1440 window.
3. **Measure the frame, not the window, in JavaScript.** Use `appWidth()` or `isMobile()` from the starter (they read `#app.clientWidth`). Never use `innerWidth` or `matchMedia` for layout decisions.
4. **Fixed and overlay elements go inside `#app`.** `#app` has a transform, so `position: fixed` inside it pins to the frame, not the window. Sheets, modals, toasts belonging to the product, sticky bars: all inside `#app`.
5. **Wide frames scale to fit.** If the chosen width is wider than the window, the frame is scaled down (`--fs`) and the readout says "shown at 74%". Layout still renders at the true width.
6. **After any banner change, fire a `resize` event** so carousels, maps and measured layouts recalculate. The starter does this for you.

## 4. Layout grid overlay

The overlay sits on top of the page (`pointer-events: none`), inside `#app`, so it always matches the frame width.

Super Liquor values (mobile 390 / 20px and desktop 1440 / 85px from DESIGN.md; md, lg, gutter and columns kept from the HOT build):

| Breakpoint | Frame width | Columns | Margin | Gutter |
|---|---|---|---|---|
| mobile | 0 to 767 | 4 | 20 | 24 |
| md | 768 to 1023 | 12 | 24 | 24 |
| lg | 1024 to 1279 | 12 | 44 | 24 |
| xl | 1280 to 1535 | 12 | 85 | 24 |
| 2xl | 1536 to 1899 | 12 | 85 | 24 |
| 3xl | 1900 and up | 12 | 85 | 24, content max 1270 (frame max 1440) |

Rules:
- The product's own wrapper (`.wrap`) must use the **same** margins, gutter and max width as the overlay, so cards and blocks can be checked against it by eye.
- Keep the overlay colour light pink fills with a 1px edge (`rgba(255,72,110,.09)` fill, `.30` edge). It must read as tooling, never as design.
- Breakpoint names in the readout come from the `BP` list in the script. Keep them the same as the dev breakpoints.

## 5. Banner design rules

- Height 34px, fixed to the top, frosted light grey background, 1px bottom border.
- **System font** (`system-ui`), 11px, semibold. The banner must never use the product typeface or colours, so nobody mistakes it for part of the design. One brand touch only: the readout chip.
- Segmented controls with a white sliding thumb. The selected button has `aria-pressed="true"`.
- The banner scrolls sideways if it runs out of room (no wrapping, no second row).
- Use the `pb-` prefix for every banner class and id. Product CSS must never style `#protobar`, and banner CSS must never style the product.
- A short toast confirms each change ("Mobile, 375 wide", "Layout grid shown").
- Accessible: `role="toolbar"`, real `<button>`s, visible focus ring, `aria-live` on the readout, honours reduced motion.

## 6. Adding project switchers

Add each one after the divider, using the same markup:

```html
<div class="pb-group"><span>Cards</span><div class="pb-seg" data-group="cards"><span class="pb-thumb"></span>
  <button data-v="portrait" aria-pressed="true">Portrait</button><button data-v="landscape" aria-pressed="false">Landscape</button>
</div></div>
```

Then handle it in one place:

```js
window.onProtoChange = (group, value, state) => {
  if (group === 'cards') setCardVariant(value);
  if (group === 'page') location.hash = value;
};
```

Conventions:
- **Page** is always the first project switcher when the prototype has more than one page. Each page has a URL hash (`#home`, `#consultants`) and the switcher stays in sync when people navigate by clicking inside the prototype.
- **Variants** (A/B layouts, card styles): label with the plain name, not "Variant A". When switched, scroll the changed part of the page into view so the reviewer sees the difference.
- **States** (logged in, location allowed or blocked, empty results, over 10 reviews): one switcher per state, default to the most common real-world state.
- Keep labels to one or two words. Use the group name for context ("Location: Real | Allowed | Blocked").

## 7. Build checklist

- [ ] Banner first in `<body>`, then `#app` containing `#pbGrid` and `#scroller`.
- [ ] All layout breakpoints written as `@container app (...)`.
- [ ] JavaScript reads `appWidth()` / `isMobile()`, never `innerWidth`.
- [ ] Product wrapper margins, gutter and max width match the grid overlay.
- [ ] Modals, sheets and sticky elements live inside `#app`.
- [ ] Project switchers added after the divider and handled in `onProtoChange`.
- [ ] Browser storage only used for banner choices, wrapped in try/catch.

## 8. QA before publishing

1. Click every Width: 390, 768, 1024, 1280, 1440, 1920. Check nothing overflows sideways and the readout shows the right breakpoint.
2. Turn the Grid on at each width and check cards, headings and blocks start and end on column edges.
3. Device Mobile and Tablet: check the bezel frame, scrolling inside the frame, and that sheets and modals stay inside it.
4. Click every project switcher and confirm the change is visible without hunting for it.
5. Reload: the last Width and Grid choice comes back.
6. Check the browser console for errors.
7. Publish the same file path each time so the Artifact keeps its link.

## 9. Prompt to start a new prototype

Paste this when asking Claude for a new prototype:

> Build this as an interactive prototype Artifact using my default prototype banner (Device, Width, Grid and the breakpoint readout) from "Interactive prototypes with Artifacts: default prototype banner". Use `#app` as the viewport with container queries, match the grid overlay to [project] breakpoints and margins, and add these project switchers after the divider: [list].

## 10. Starter file (tested)

Copy this as the first version of any prototype, then build the product inside `#scroller`. Change the `BP` list, `DEVICE` sizes and the grid margins to the project's values.

```html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Prototype starter</title>
<style>
/* ---------- 1. Prototype banner (tooling, never product styles) ---------- */
:root{--pb-h:34px;--pb-ink:#1d1d1f;--pb-mute:#8e8e93;--pb-bg:rgba(246,246,248,.92);--pb-seg:#e4e4e9;--pb-accent:#205AA7;--pb-accent-bg:#E9EFF8}
html,body{margin:0;height:100%}
body{overflow:hidden;background:#fff}
#protobar{position:fixed;inset:0 0 auto 0;height:var(--pb-h);z-index:1000;display:flex;align-items:center;gap:16px;padding:0 12px;
  background:var(--pb-bg);backdrop-filter:blur(14px) saturate(160%);-webkit-backdrop-filter:blur(14px) saturate(160%);border-bottom:1px solid #e1e1e6;
  font:600 11px/1 system-ui,-apple-system,"Segoe UI",sans-serif;color:var(--pb-mute);white-space:nowrap;overflow-x:auto;scrollbar-width:none}
#protobar::-webkit-scrollbar{display:none}
.pb-title{letter-spacing:.04em;text-transform:uppercase}
.pb-group{display:flex;align-items:center;gap:6px}
.pb-div{width:1px;height:18px;background:#d6d6dc;flex:none}
.pb-seg{position:relative;display:flex;padding:2px;border-radius:7px;background:var(--pb-seg)}
.pb-seg button{position:relative;z-index:1;height:22px;padding:0 9px;border:0;border-radius:5px;background:none;cursor:pointer;font:inherit;color:#6e6e73;transition:color .2s}
.pb-seg button[aria-pressed=true]{color:var(--pb-ink)}
.pb-seg button:focus-visible{outline:2px solid var(--pb-accent);outline-offset:1px}
.pb-thumb{position:absolute;top:2px;left:0;height:22px;border-radius:5px;background:#fff;box-shadow:0 1px 2px rgba(0,0,0,.12),0 0 0 .5px rgba(0,0,0,.06);transition:transform .28s cubic-bezier(.3,.7,.2,1),width .28s cubic-bezier(.3,.7,.2,1)}
.pb-bp{margin-left:auto;color:var(--pb-accent);background:var(--pb-accent-bg);border-radius:6px;padding:6px 9px}
.pb-toast{position:fixed;left:50%;bottom:20px;z-index:1001;transform:translate(-50%,8px);opacity:0;pointer-events:none;padding:8px 12px;border-radius:8px;background:#1d1d1f;color:#fff;font:500 12px/1.3 system-ui,sans-serif;transition:opacity .2s,transform .2s}
.pb-toast.on{opacity:1;transform:translate(-50%,0)}
@media (prefers-reduced-motion:reduce){.pb-thumb,.pb-toast{transition:none}}

/* ---------- 2. The frame: #app is the prototype's viewport ---------- */
#app{position:absolute;top:var(--pb-h);left:0;right:0;bottom:0;overflow:hidden;background:#fff;container-type:inline-size;container-name:app;transform:translateZ(0)}
#scroller{position:absolute;inset:0;overflow-y:auto;overflow-x:hidden;overscroll-behavior:contain}
html.pb-framed body{background:#dcd8e2}
/* Desktop and tablet: fixed width, scaled down to fit the window */
html.pb-framed #app{left:50%;right:auto;top:calc(var(--pb-h) + 12px);bottom:auto;width:var(--fw);height:var(--fh);margin-left:calc(var(--fw) / -2);
  transform:translateZ(0) scale(var(--fs,1));transform-origin:50% 0;border-radius:10px;box-shadow:0 0 0 1px rgba(28,6,45,.10),0 30px 70px -24px rgba(28,6,45,.40)}
html.pb-tablet #app{border-radius:24px;box-shadow:0 0 0 10px #16101c,0 0 0 11px #3a3340,0 40px 80px -20px rgba(28,6,45,.45)}
html.pb-mobile #app{border-radius:34px;box-shadow:0 0 0 10px #16101c,0 0 0 11px #3a3340,0 40px 80px -20px rgba(28,6,45,.45)}
html.pb-mobile #scroller,html.pb-tablet #scroller{scrollbar-width:none}

/* ---------- 3. Layout grid overlay (matches the live site grid) ---------- */
#pbGrid{display:none;position:absolute;inset:0;z-index:999;pointer-events:none}
html.pb-grid #pbGrid{display:block}
#pbGrid .gw{height:100%;max-width:1440px;margin:0 auto;padding:0 var(--m);display:grid;grid-template-columns:repeat(var(--cols),minmax(0,1fr));column-gap:var(--g)}
#pbGrid i{background:rgba(255,72,110,.09);border-inline:1px solid rgba(255,72,110,.30)}
#app{--m:85px;--g:24px;--cols:12}
@container app (max-width:1279px){#pbGrid{--m:44px}}
@container app (max-width:1023px){#pbGrid{--m:24px}}
@container app (max-width:767px){#pbGrid{--m:20px;--cols:4}#pbGrid i:nth-child(n+5){display:none}}

/* ---------- 4. Product styles start here. Use @container app, never @media, for layout ---------- */
.wrap{max-width:1440px;margin:0 auto;padding:0 85px;display:grid;grid-template-columns:repeat(12,minmax(0,1fr));column-gap:24px}
@container app (max-width:1279px){.wrap{padding:0 44px}}
@container app (max-width:1023px){.wrap{padding:0 24px}}
@container app (max-width:767px){.wrap{padding:0 20px;grid-template-columns:repeat(4,minmax(0,1fr))}}
.demo{grid-column:1/-1;padding:48px 0;font:400 16px/1.5 system-ui,sans-serif}
</style>
</head>
<body>
<div id="protobar" role="toolbar" aria-label="Prototype controls">
  <span class="pb-title">Prototype</span>
  <div class="pb-group"><span>Device</span><div class="pb-seg" data-group="device"><span class="pb-thumb"></span><button data-v="fit" aria-pressed="true">Fit</button><button data-v="desktop" aria-pressed="false">Desktop</button><button data-v="tablet" aria-pressed="false">Tablet</button><button data-v="mobile" aria-pressed="false">Mobile</button></div></div>
  <div class="pb-group"><span>Width</span><div class="pb-seg" data-group="width"><span class="pb-thumb"></span><button data-v="fit" aria-pressed="true">Fit</button><button data-v="390" aria-pressed="false">390</button><button data-v="768" aria-pressed="false">768</button><button data-v="1024" aria-pressed="false">1024</button><button data-v="1280" aria-pressed="false">1280</button><button data-v="1440" aria-pressed="false">1440</button><button data-v="1920" aria-pressed="false">1920</button></div></div>
  <div class="pb-group"><span>Grid</span><div class="pb-seg" data-group="grid"><span class="pb-thumb"></span><button data-v="off" aria-pressed="true">Off</button><button data-v="on" aria-pressed="false">On</button></div></div>
  <span class="pb-div" aria-hidden="true"></span>
  <!-- Project switchers go here, after the divider: pages, variants, states -->
  <span class="pb-bp" id="pbBp" aria-live="polite"></span>
</div>
<div class="pb-toast" id="pbToast" role="status"></div>

<div id="app">
  <div id="pbGrid" aria-hidden="true"><div class="gw"><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i></div></div>
  <div id="scroller">
    <main class="wrap"><div class="demo"><h1>Page content</h1><p>Build the prototype inside #scroller.</p></div></main>
  </div>
</div>

<script>
(function(){
  const $=(s,r=document)=>r.querySelector(s),$$=(s,r=document)=>[...r.querySelectorAll(s)];
  const H=document.documentElement,app=$('#app');
  /* Breakpoints and grid: change these to the project's own values */
  const BP=[[0,'mobile'],[768,'md 768'],[1024,'lg 1024'],[1280,'xl 1280'],[1536,'2xl 1536'],[1900,'3xl 1900']];
  const DEVICE={desktop:{w:1440},tablet:{w:768,h:1024},mobile:{w:390,h:812}};
  const S={device:'fit',width:'fit',grid:'off'};
  const store={get(k){try{return localStorage.getItem('pb:'+k)}catch(e){return null}},set(k,v){try{localStorage.setItem('pb:'+k,v)}catch(e){}}};

  let tt;function toast(m){const t=$('#pbToast');t.textContent=m;t.classList.add('on');clearTimeout(tt);tt=setTimeout(()=>t.classList.remove('on'),1400)}
  function press(group,v){const seg=$(`#protobar [data-group="${group}"]`);if(!seg)return;$$('button',seg).forEach(b=>b.setAttribute('aria-pressed',String(b.dataset.v===v)));place(seg)}
  function place(seg){const b=$('button[aria-pressed=true]',seg),th=$('.pb-thumb',seg);if(!b||!th)return;th.style.transform=`translateX(${b.offsetLeft}px)`;th.style.width=b.offsetWidth+'px'}

  function frame(){
    const w=S.width==='fit'?null:+S.width;
    const dev=S.device==='fit'?null:S.device;
    H.classList.toggle('pb-framed',!!w);
    H.classList.toggle('pb-mobile',dev==='mobile');H.classList.toggle('pb-tablet',dev==='tablet');
    if(!w){app.style.removeProperty('--fw');app.style.removeProperty('--fh');app.style.removeProperty('--fs');return}
    const availW=innerWidth-24,availH=innerHeight-34-24;
    const fixedH=dev&&DEVICE[dev].h;                       // tablet and mobile keep a real device height
    const fs=Math.min(1,availW/w,fixedH?availH/fixedH:1);
    const h=fixedH||availH/fs;                              // desktop fills the window height
    app.style.setProperty('--fw',w+'px');app.style.setProperty('--fh',h+'px');app.style.setProperty('--fs',fs.toFixed(4));
  }
  function readout(){const w=app.clientWidth;let bp=BP[0][1];BP.forEach(([min,n])=>{if(w>=min)bp=n});
    const s=parseFloat(getComputedStyle(app).getPropertyValue('--fs'))||1;
    $('#pbBp').textContent=`${w}px · ${bp}`+(s<1?` · shown at ${Math.round(s*100)}%`:'')}

  function set(group,v,quiet){
    S[group]=v;store.set(group,v);
    if(group==='device'){S.width=v==='fit'?'fit':String(DEVICE[v].w);press('width',S.width)}
    if(group==='width'){S.device=v==='fit'?'fit':+v<768?'mobile':+v<1024?'tablet':'desktop';press('device',S.device)}
    if(group==='grid')H.classList.toggle('pb-grid',v==='on');
    press(group,v);frame();
    requestAnimationFrame(()=>{dispatchEvent(new Event('resize'));readout()});
    if(!quiet)toast(group==='grid'?(v==='on'?'Layout grid shown':'Layout grid hidden'):S.width==='fit'?'Fit to window':`${S.device[0].toUpperCase()+S.device.slice(1)}, ${S.width} wide`);
    /* Project hook: react to banner changes here */
    window.onProtoChange&&window.onProtoChange(group,v,{...S});
  }

  $$('#protobar .pb-seg').forEach(seg=>{place(seg);$$('button',seg).forEach(b=>b.addEventListener('click',()=>set(seg.dataset.group,b.dataset.v)))});
  document.fonts&&document.fonts.ready.then(()=>$$('#protobar .pb-seg').forEach(place));
  addEventListener('resize',()=>{frame();readout()});
  new ResizeObserver(readout).observe(app);
  /* Keyboard: G toggles the grid, 1 to 4 pick Fit, Desktop, Tablet, Mobile (ignored while typing) */
  addEventListener('keydown',e=>{if(e.metaKey||e.ctrlKey||e.altKey||/INPUT|TEXTAREA|SELECT/.test(e.target.tagName)||e.target.isContentEditable)return;
    if(e.key==='g'||e.key==='G')set('grid',S.grid==='on'?'off':'on');
    const d={'1':'fit','2':'desktop','3':'tablet','4':'mobile'}[e.key];if(d)set('device',d)});
  /* Restore the last choices for this viewer */
  const w0=store.get('width'),g0=store.get('grid');if(w0)set('width',w0,true);if(g0)set('grid',g0,true);readout();
  /* Helper for product code: always measure the frame, not the window */
  window.appWidth=()=>app.clientWidth;window.isMobile=()=>app.clientWidth<768;
})();
</script>
</body>
</html>
```
