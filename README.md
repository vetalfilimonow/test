<!DOCTYPE html>
<html lang="uk">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ЯВІР — Каркасні будинки під ключ</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --ink:    #0D1A0F;
    --forest: #2C5F2E;
    --gold:   #C8A84B;
    --cream:  #F5F0E8;
    --white:  #FFFFFF;
    --mist:   #E8E2D8;
    --serif:  'Playfair Display', Georgia, serif;
    --sans:   'Inter', system-ui, sans-serif;
  }

  html { scroll-behavior: smooth; font-size: 16px; }

  body {
    background: var(--ink);
    color: var(--cream);
    font-family: var(--sans);
    font-weight: 300;
    line-height: 1.6;
    overflow-x: hidden;
  }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 1.25rem 4rem;
    transition: background .4s, backdrop-filter .4s;
  }
  nav.scrolled {
    background: rgba(13,26,15,.88);
    backdrop-filter: blur(14px);
    border-bottom: 1px solid rgba(200,168,75,.15);
  }
  .nav-logo {
    font-family: var(--serif); font-size: 1.5rem; font-weight: 700;
    color: var(--white); letter-spacing: .04em; text-decoration: none;
  }
  .nav-logo span { color: var(--gold); }
  .nav-links { display: flex; gap: 2rem; list-style: none; }
  .nav-links a {
    font-size: .8rem; letter-spacing: .12em; text-transform: uppercase;
    color: rgba(245,240,232,.7); text-decoration: none;
    transition: color .25s;
  }
  .nav-links a:hover { color: var(--gold); }
  .nav-cta {
    padding: .6rem 1.5rem; border: 1px solid var(--gold);
    color: var(--gold); font-size: .8rem; letter-spacing: .1em;
    text-transform: uppercase; text-decoration: none;
    transition: background .25s, color .25s;
  }
  .nav-cta:hover { background: var(--gold); color: var(--ink); }

  /* burger */
  .burger { display: none; flex-direction: column; gap: 5px; cursor: pointer; background: none; border: none; padding: 4px; }
  .burger span { display: block; width: 24px; height: 1.5px; background: var(--cream); transition: .3s; }
  .burger.open span:nth-child(1) { transform: translateY(6.5px) rotate(45deg); }
  .burger.open span:nth-child(2) { opacity: 0; }
  .burger.open span:nth-child(3) { transform: translateY(-6.5px) rotate(-45deg); }

  .mobile-menu {
    display: none; position: fixed; inset: 0; z-index: 99;
    background: rgba(13,26,15,.97); flex-direction: column;
    align-items: center; justify-content: center; gap: 2rem;
  }
  .mobile-menu.open { display: flex; }
  .mobile-menu a {
    font-family: var(--serif); font-size: 2rem; color: var(--cream);
    text-decoration: none; transition: color .2s;
  }
  .mobile-menu a:hover { color: var(--gold); }
  .mobile-menu .nav-cta { font-family: var(--sans); font-size: 1rem; }

  /* ── HERO ── */
  .hero {
    position: relative; min-height: 100vh;
    display: flex; flex-direction: column; justify-content: flex-end;
    padding: 0 4rem 6rem;
    overflow: hidden;
  }
  .hero-bg {
    position: absolute; inset: 0;
    background: url('https://images.unsplash.com/photo-1601919051950-bb9f3ffb3fee?auto=format&fit=crop&w=1920&q=85') center/cover no-repeat;
  }
  .hero-bg::after {
    content: '';
    position: absolute; inset: 0;
    background: linear-gradient(160deg, rgba(13,26,15,.3) 0%, rgba(13,26,15,.85) 70%, rgba(13,26,15,1) 100%);
  }
  .hero-tag {
    position: relative;
    display: inline-flex; align-items: center; gap: .75rem;
    margin-bottom: 1.5rem;
    font-size: .7rem; letter-spacing: .2em; text-transform: uppercase;
    color: var(--gold);
  }
  .hero-tag::before {
    content: ''; display: block; width: 32px; height: 1px; background: var(--gold);
  }
  .hero-title {
    position: relative;
    font-family: var(--serif); font-weight: 900;
    font-size: clamp(3rem, 7vw, 6.5rem);
    line-height: 1.02; letter-spacing: -.02em;
    max-width: 800px; margin-bottom: 1.5rem;
  }
  .hero-title em { font-style: italic; color: var(--gold); }
  .hero-sub {
    position: relative; max-width: 500px;
    font-size: 1rem; line-height: 1.7;
    color: rgba(245,240,232,.75); margin-bottom: 2.5rem;
  }
  .hero-actions {
    position: relative; display: flex; align-items: center; gap: 2rem; flex-wrap: wrap;
  }
  .btn-primary {
    display: inline-block; padding: 1rem 2.5rem;
    background: var(--gold); color: var(--ink);
    font-size: .85rem; font-weight: 600; letter-spacing: .08em; text-transform: uppercase;
    text-decoration: none; transition: transform .2s, box-shadow .2s;
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 30px rgba(200,168,75,.35); }
  .btn-ghost {
    display: inline-flex; align-items: center; gap: .5rem;
    font-size: .85rem; color: rgba(245,240,232,.8); text-decoration: none;
    border-bottom: 1px solid rgba(245,240,232,.3); padding-bottom: 2px;
    transition: color .2s, border-color .2s;
  }
  .btn-ghost:hover { color: var(--gold); border-color: var(--gold); }

  /* stats strip */
  .hero-stats {
    position: relative;
    display: flex; gap: 4rem; margin-top: 5rem;
    padding-top: 2rem; border-top: 1px solid rgba(200,168,75,.25);
  }
  .stat-num {
    font-family: var(--serif); font-size: 2.8rem; font-weight: 700; color: var(--white);
    line-height: 1;
  }
  .stat-num sup { font-size: 1.2rem; color: var(--gold); vertical-align: super; }
  .stat-label { font-size: .75rem; letter-spacing: .1em; text-transform: uppercase; color: rgba(245,240,232,.5); margin-top: .25rem; }

  /* scroll indicator */
  .scroll-hint {
    position: absolute; bottom: 2rem; right: 4rem;
    display: flex; flex-direction: column; align-items: center; gap: .5rem;
    font-size: .65rem; letter-spacing: .15em; text-transform: uppercase; color: rgba(245,240,232,.4);
  }
  .scroll-line {
    width: 1px; height: 48px; background: linear-gradient(to bottom, var(--gold), transparent);
    animation: scrollDown 1.8s ease-in-out infinite;
  }
  @keyframes scrollDown { 0%,100%{transform:scaleY(1);opacity:.8} 50%{transform:scaleY(.4);opacity:.2} }

  /* ── SECTIONS common ── */
  section { padding: 7rem 4rem; }
  .eyebrow {
    display: inline-flex; align-items: center; gap: .75rem;
    font-size: .7rem; letter-spacing: .2em; text-transform: uppercase; color: var(--gold);
    margin-bottom: 1rem;
  }
  .eyebrow::after { content:''; display:block; width:24px; height:1px; background:var(--gold); }
  h2 {
    font-family: var(--serif); font-size: clamp(2rem, 4vw, 3.5rem);
    font-weight: 700; line-height: 1.1; letter-spacing: -.02em;
    color: var(--white); margin-bottom: 1rem;
  }
  .section-lead {
    font-size: 1rem; color: rgba(245,240,232,.6);
    max-width: 500px; line-height: 1.7;
  }

  /* ── PROCESS ── */
  #process { background: var(--ink); }
  .process-header { margin-bottom: 4rem; }
  .process-grid {
    display: grid; grid-template-columns: repeat(4,1fr); gap: 1.5px;
  }
  .process-item {
    position: relative; overflow: hidden; aspect-ratio: 3/4;
    cursor: default;
  }
  .process-item img {
    width: 100%; height: 100%; object-fit: cover;
    transition: transform .6s ease, filter .6s ease;
    filter: brightness(.55) saturate(.7);
  }
  .process-item:hover img { transform: scale(1.06); filter: brightness(.35) saturate(.5); }
  .process-overlay {
    position: absolute; inset: 0;
    display: flex; flex-direction: column; justify-content: flex-end;
    padding: 2rem 1.5rem;
    background: linear-gradient(to top, rgba(13,26,15,.9) 0%, transparent 60%);
    transition: background .4s;
  }
  .process-item:hover .process-overlay { background: linear-gradient(to top, rgba(13,26,15,.97) 0%, rgba(13,26,15,.4) 100%); }
  .process-num {
    font-family: var(--serif); font-size: 5rem; font-weight: 900;
    color: rgba(200,168,75,.15); line-height: 1;
    position: absolute; top: 1rem; right: 1rem;
    transition: color .4s;
  }
  .process-item:hover .process-num { color: rgba(200,168,75,.4); }
  .process-title {
    font-family: var(--serif); font-size: 1.3rem; font-weight: 700; color: var(--white);
    margin-bottom: .4rem;
  }
  .process-time {
    font-size: .72rem; letter-spacing: .1em; text-transform: uppercase; color: var(--gold);
  }
  .process-desc {
    font-size: .85rem; color: rgba(245,240,232,.7); line-height: 1.6;
    max-height: 0; overflow: hidden; transition: max-height .5s ease, margin .4s;
  }
  .process-item:hover .process-desc { max-height: 80px; margin-top: .75rem; }

  /* process CTA strip */
  .process-cta {
    margin-top: 4rem; padding: 3rem;
    border: 1px solid rgba(200,168,75,.2);
    display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; gap: 1.5rem;
    background: rgba(200,168,75,.04);
  }
  .process-cta p { font-family: var(--serif); font-size: 1.4rem; color: var(--white); max-width: 500px; }

  /* ── TECH ── */
  #tech { background: var(--cream); }
  #tech h2, #tech .eyebrow, #tech .section-lead { color: var(--ink); }
  #tech .eyebrow { color: var(--forest); }
  #tech .eyebrow::after { background: var(--forest); }
  .tech-grid {
    display: grid; grid-template-columns: repeat(2,1fr); gap: 0;
    margin-top: 4rem; border: 1px solid rgba(44,95,46,.15);
  }
  .tech-card {
    padding: 3rem 2.5rem;
    border-right: 1px solid rgba(44,95,46,.15);
    border-bottom: 1px solid rgba(44,95,46,.15);
    position: relative; overflow: hidden;
    transition: background .3s;
  }
  .tech-card:nth-child(2n) { border-right: none; }
  .tech-card:nth-last-child(-n+2) { border-bottom: none; }
  .tech-card:hover { background: rgba(44,95,46,.05); }
  .tech-icon {
    width: 44px; height: 44px; margin-bottom: 1.5rem;
    color: var(--forest);
  }
  .tech-card h3 {
    font-family: var(--serif); font-size: 1.4rem; font-weight: 700;
    color: var(--ink); margin-bottom: .75rem; line-height: 1.2;
  }
  .tech-card p { font-size: .9rem; color: rgba(13,26,15,.65); line-height: 1.7; }
  .tech-accent {
    position: absolute; bottom: -20px; right: -20px;
    font-family: var(--serif); font-size: 7rem; font-weight: 900;
    color: rgba(44,95,46,.06); line-height: 1; pointer-events: none;
    transition: color .3s;
  }
  .tech-card:hover .tech-accent { color: rgba(44,95,46,.1); }

  /* ── PORTFOLIO ── */
  #portfolio { background: var(--ink); }
  .portfolio-header { margin-bottom: 4rem; }
  .portfolio-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: auto auto;
    gap: 1.5px;
  }
  .port-item {
    position: relative; overflow: hidden;
  }
  .port-item:first-child {
    grid-row: span 2;
  }
  .port-item img {
    width: 100%; height: 100%; object-fit: cover; display: block;
    min-height: 280px;
    transition: transform .7s ease;
  }
  .port-item:first-child img { min-height: 560px; }
  .port-item:hover img { transform: scale(1.05); }
  .port-overlay {
    position: absolute; inset: 0;
    background: linear-gradient(to top, rgba(13,26,15,.85) 0%, transparent 50%);
    display: flex; flex-direction: column; justify-content: flex-end;
    padding: 2rem;
  }
  .port-tag {
    font-size: .68rem; letter-spacing: .15em; text-transform: uppercase;
    color: var(--gold); margin-bottom: .4rem;
  }
  .port-title { font-family: var(--serif); font-size: 1.4rem; font-weight: 700; color: var(--white); }
  .port-meta { font-size: .78rem; color: rgba(245,240,232,.6); margin-top: .25rem; }

  .portfolio-cta {
    margin-top: 4rem; text-align: center;
  }
  .portfolio-cta p {
    font-family: var(--serif); font-size: 1.1rem; color: rgba(245,240,232,.6);
    margin-bottom: 1.5rem;
  }

  /* ── WHY ── */
  #why {
    background: var(--forest);
    position: relative; overflow: hidden;
  }
  #why::before {
    content: 'ЯВІР';
    position: absolute; right: -2rem; top: 50%; transform: translateY(-50%);
    font-family: var(--serif); font-size: 22vw; font-weight: 900;
    color: rgba(255,255,255,.04); line-height: 1; pointer-events: none;
    white-space: nowrap;
  }
  .why-grid {
    display: grid; grid-template-columns: repeat(4,1fr); gap: 2rem;
    margin-top: 4rem; position: relative;
  }
  .why-card {
    padding: 2rem 0; border-top: 1px solid rgba(245,240,232,.2);
  }
  .why-num {
    font-family: var(--serif); font-size: .85rem; color: rgba(245,240,232,.4);
    margin-bottom: 1.5rem;
  }
  .why-card h3 {
    font-family: var(--serif); font-size: 1.25rem; font-weight: 700;
    color: var(--white); margin-bottom: .75rem;
  }
  .why-card p { font-size: .87rem; color: rgba(245,240,232,.7); line-height: 1.7; }

  /* ── STEPS ── */
  #steps { background: var(--cream); }
  #steps h2, #steps .eyebrow, #steps .section-lead { color: var(--ink); }
  #steps .eyebrow { color: var(--forest); }
  #steps .eyebrow::after { background: var(--forest); }
  .steps-list { margin-top: 4rem; }
  .step-row {
    display: grid; grid-template-columns: 80px 1fr;
    gap: 2rem; align-items: start;
    padding: 2rem 0; border-bottom: 1px solid rgba(13,26,15,.1);
    transition: background .2s;
  }
  .step-row:hover { background: rgba(44,95,46,.04); }
  .step-index {
    font-family: var(--serif); font-size: 3rem; font-weight: 900;
    color: rgba(13,26,15,.12); line-height: 1; padding-top: .15rem;
  }
  .step-body h3 {
    font-family: var(--serif); font-size: 1.25rem; font-weight: 700;
    color: var(--ink); margin-bottom: .5rem;
  }
  .step-body p { font-size: .9rem; color: rgba(13,26,15,.6); line-height: 1.7; }

  /* ── REVIEWS ── */
  #reviews { background: var(--ink); }
  .reviews-grid { display: grid; grid-template-columns: repeat(3,1fr); gap: 1px; margin-top: 4rem; }
  .review-card {
    padding: 2.5rem 2rem;
    border: 1px solid rgba(200,168,75,.1);
    transition: border-color .3s, background .3s;
  }
  .review-card:hover { border-color: rgba(200,168,75,.4); background: rgba(200,168,75,.03); }
  .stars { color: var(--gold); font-size: 1rem; letter-spacing: .1em; margin-bottom: 1.25rem; }
  .review-text { font-size: .92rem; line-height: 1.75; color: rgba(245,240,232,.8); margin-bottom: 1.5rem; font-style: italic; }
  .reviewer { display: flex; align-items: center; gap: .75rem; }
  .reviewer-avatar {
    width: 38px; height: 38px;
    background: var(--forest);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-family: var(--serif); font-weight: 700; font-size: .8rem; color: var(--cream);
  }
  .reviewer-name { font-size: .85rem; color: var(--white); font-weight: 500; }
  .reviewer-meta { font-size: .72rem; color: rgba(245,240,232,.45); margin-top: .1rem; }

  /* ── CONTACT ── */
  #contact-form {
    background: var(--cream);
    display: grid; grid-template-columns: 1fr 1fr; gap: 0;
    padding: 0;
  }
  .contact-left {
    padding: 6rem 4rem;
    background: var(--ink);
    display: flex; flex-direction: column; justify-content: space-between;
  }
  .contact-left h2 { font-size: clamp(2rem,3.5vw,3rem); margin-bottom: 1rem; }
  .contact-left .section-lead { margin-bottom: 3rem; }
  .contact-info { display: flex; flex-direction: column; gap: 1.5rem; }
  .contact-info-item {}
  .contact-info-label { font-size: .68rem; letter-spacing: .15em; text-transform: uppercase; color: var(--gold); margin-bottom: .3rem; }
  .contact-info-val { font-size: .95rem; color: rgba(245,240,232,.85); }

  .contact-right {
    padding: 6rem 4rem;
    background: var(--cream);
  }
  .contact-right h3 {
    font-family: var(--serif); font-size: 1.6rem; font-weight: 700;
    color: var(--ink); margin-bottom: 2rem;
  }

  /* calculator */
  .calc-block { margin-bottom: 2rem; }
  .calc-label {
    display: flex; justify-content: space-between; align-items: center;
    font-size: .8rem; letter-spacing: .08em; text-transform: uppercase;
    color: rgba(13,26,15,.6); margin-bottom: .75rem;
  }
  .calc-label span { font-family: var(--serif); font-size: 1.1rem; font-weight: 700; color: var(--ink); letter-spacing: 0; text-transform: none; }
  input[type=range] {
    -webkit-appearance: none; width: 100%; height: 2px;
    background: rgba(13,26,15,.2); outline: none;
  }
  input[type=range]::-webkit-slider-thumb {
    -webkit-appearance: none; width: 18px; height: 18px;
    background: var(--forest); border-radius: 50%; cursor: pointer;
    border: 2px solid var(--cream); box-shadow: 0 0 0 2px var(--forest);
  }
  .combo-select {
    display: grid; grid-template-columns: repeat(3,1fr); gap: .5rem;
    margin-bottom: 1.5rem;
  }
  .combo-btn {
    padding: .65rem .5rem; border: 1px solid rgba(13,26,15,.2);
    background: transparent; cursor: pointer; font-family: var(--sans);
    font-size: .78rem; letter-spacing: .05em; color: rgba(13,26,15,.7);
    transition: all .2s; text-align: center;
  }
  .combo-btn.active { background: var(--forest); color: var(--white); border-color: var(--forest); }

  .price-display {
    padding: 1.5rem 2rem; background: var(--ink); margin-bottom: 1.5rem;
    display: flex; align-items: baseline; gap: .75rem; flex-wrap: wrap;
  }
  .price-label { font-size: .72rem; letter-spacing: .12em; text-transform: uppercase; color: rgba(245,240,232,.4); }
  .price-val { font-family: var(--serif); font-size: 2rem; font-weight: 700; color: var(--gold); }

  .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; margin-bottom: 1rem; }
  .field { display: flex; flex-direction: column; gap: .4rem; }
  .field label { font-size: .72rem; letter-spacing: .1em; text-transform: uppercase; color: rgba(13,26,15,.5); }
  .field input {
    padding: .85rem 1rem; border: 1px solid rgba(13,26,15,.2); background: var(--white);
    font-family: var(--sans); font-size: .9rem; color: var(--ink); outline: none;
    transition: border-color .2s;
  }
  .field input:focus { border-color: var(--forest); }

  .submit-btn {
    width: 100%; padding: 1.1rem; background: var(--ink); color: var(--cream);
    border: none; cursor: pointer; font-family: var(--sans);
    font-size: .85rem; font-weight: 600; letter-spacing: .1em; text-transform: uppercase;
    transition: background .25s;
  }
  .submit-btn:hover { background: var(--forest); }

  .success-msg {
    display: none; padding: 2rem; border: 1px solid rgba(44,95,46,.4);
    background: rgba(44,95,46,.08); text-align: center;
  }
  .success-msg.show { display: block; }
  .success-msg h4 { font-family: var(--serif); font-size: 1.3rem; color: var(--ink); margin-bottom: .5rem; }
  .success-msg p { font-size: .9rem; color: rgba(13,26,15,.6); }

  /* ── FOOTER ── */
  footer {
    background: #080F09; padding: 4rem;
    display: grid; grid-template-columns: 2fr 1fr 1fr; gap: 3rem;
    border-top: 1px solid rgba(200,168,75,.12);
  }
  .footer-brand {}
  .footer-logo { font-family: var(--serif); font-size: 1.8rem; font-weight: 700; color: var(--white); margin-bottom: .75rem; }
  .footer-logo span { color: var(--gold); }
  .footer-desc { font-size: .85rem; color: rgba(245,240,232,.45); line-height: 1.7; max-width: 280px; }
  .footer-col h4 { font-size: .7rem; letter-spacing: .15em; text-transform: uppercase; color: var(--gold); margin-bottom: 1.25rem; }
  .footer-col ul { list-style: none; display: flex; flex-direction: column; gap: .6rem; }
  .footer-col ul a { font-size: .85rem; color: rgba(245,240,232,.5); text-decoration: none; transition: color .2s; }
  .footer-col ul a:hover { color: var(--cream); }
  .footer-bottom {
    background: #080F09; padding: 1.5rem 4rem;
    display: flex; justify-content: space-between; align-items: center;
    border-top: 1px solid rgba(245,240,232,.06);
    font-size: .72rem; color: rgba(245,240,232,.3);
  }

  /* ── ANIMATIONS ── */
  .reveal { opacity: 0; transform: translateY(28px); transition: opacity .7s ease, transform .7s ease; }
  .reveal.visible { opacity: 1; transform: none; }
  .reveal-delay-1 { transition-delay: .1s; }
  .reveal-delay-2 { transition-delay: .2s; }
  .reveal-delay-3 { transition-delay: .3s; }
  .reveal-delay-4 { transition-delay: .4s; }

  /* ── RESPONSIVE ── */
  @media (max-width: 1024px) {
    nav { padding: 1.25rem 2rem; }
    .nav-links, .nav-cta { display: none; }
    .burger { display: flex; }
    section { padding: 5rem 2rem; }
    .hero { padding: 0 2rem 5rem; }
    .process-grid { grid-template-columns: repeat(2,1fr); }
    .tech-grid { grid-template-columns: 1fr; }
    .tech-card:nth-child(2n) { border-right: 1px solid rgba(44,95,46,.15); }
    .tech-card:nth-last-child(-n+2) { border-bottom: 1px solid rgba(44,95,46,.15); }
    .tech-card:last-child { border-bottom: none; }
    .why-grid { grid-template-columns: repeat(2,1fr); }
    .reviews-grid { grid-template-columns: 1fr; }
    #contact-form { grid-template-columns: 1fr; }
    .contact-left, .contact-right { padding: 4rem 2rem; }
    footer { grid-template-columns: 1fr 1fr; }
    .footer-bottom { padding: 1.5rem 2rem; }
    .hero-stats { gap: 2rem; }
  }
  @media (max-width: 640px) {
    .hero-title { font-size: 2.6rem; }
    .process-grid { grid-template-columns: 1fr; }
    .portfolio-grid { grid-template-columns: 1fr; grid-template-rows: auto; }
    .port-item:first-child { grid-row: auto; }
    .why-grid { grid-template-columns: 1fr; }
    .form-row { grid-template-columns: 1fr; }
    footer { grid-template-columns: 1fr; }
    .hero-stats { flex-wrap: wrap; gap: 1.5rem; }
    .scroll-hint { display: none; }
    .process-cta { flex-direction: column; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav id="navbar">
  <a href="#" class="nav-logo">ЯВ<span>І</span>Р</a>
  <ul class="nav-links">
    <li><a href="#process">Етапи</a></li>
    <li><a href="#tech">Технологія</a></li>
    <li><a href="#portfolio">Портфоліо</a></li>
    <li><a href="#contact-form">Контакти</a></li>
  </ul>
  <a href="#contact-form" class="nav-cta">Розрахувати вартість</a>
  <button class="burger" id="burger" aria-label="Меню">
    <span></span><span></span><span></span>
  </button>
</nav>

<!-- MOBILE MENU -->
<div class="mobile-menu" id="mobileMenu">
  <a href="#process" onclick="closeMobile()">Етапи</a>
  <a href="#tech" onclick="closeMobile()">Технологія</a>
  <a href="#portfolio" onclick="closeMobile()">Портфоліо</a>
  <a href="#contact-form" onclick="closeMobile()">Контакти</a>
  <a href="#contact-form" class="nav-cta" onclick="closeMobile()">Розрахувати вартість</a>
</div>

<!-- HERO -->
<section class="hero" id="home">
  <div class="hero-bg"></div>
  <div class="hero-tag">Каркасне будівництво</div>
  <h1 class="hero-title">Будинок під&nbsp;ключ за <em>4&nbsp;місяці</em></h1>
  <p class="hero-sub">Каркасні будинки зі власною бригадою, фіксованою ціною в договорі та гарантією 10 років — без подорожчань і сюрпризів.</p>
  <div class="hero-actions">
    <a href="#contact-form" class="btn-primary">Розрахувати вартість</a>
    <a href="tel:+380672345678" class="btn-ghost">+380 67 234 56 78 &rarr; Безкоштовний замір</a>
  </div>
  <div class="hero-stats">
    <div>
      <div class="stat-num" data-target="120"><sup>+</sup>0</div>
      <div class="stat-label">Будинків здано</div>
    </div>
    <div>
      <div class="stat-num" data-target="4">0</div>
      <div class="stat-label">Місяці під ключ</div>
    </div>
    <div>
      <div class="stat-num" data-target="10">0</div>
      <div class="stat-label">Років гарантії</div>
    </div>
  </div>
  <div class="scroll-hint">
    <div class="scroll-line"></div>
    <span>Скрол</span>
  </div>
</section>

<!-- PROCESS -->
<section id="process">
  <div class="process-header reveal">
    <div class="eyebrow">Етапи будівництва</div>
    <h2>Від фундаменту<br>до новосілля</h2>
    <p class="section-lead">Чотири чіткі етапи без затримок — кожен закритий актом до переходу далі.</p>
  </div>
  <div class="process-grid">
    <div class="process-item reveal reveal-delay-1">
      <img src="https://images.unsplash.com/photo-1530863506128-dc9eb5c3e0fc?auto=format&fit=crop&w=600&h=800&q=80" alt="Фундамент" loading="lazy">
      <div class="process-overlay">
        <div class="process-num">01</div>
        <div class="process-title">Фундамент</div>
        <div class="process-time">~ 2 тижні</div>
        <div class="process-desc">Пальово-рандбалковий або плитний фундамент залежно від ґрунту ділянки.</div>
      </div>
    </div>
    <div class="process-item reveal reveal-delay-2">
      <img src="https://images.unsplash.com/photo-1587582423116-ec07293f0395?auto=format&fit=crop&w=600&h=800&q=80" alt="Каркас" loading="lazy">
      <div class="process-overlay">
        <div class="process-num">02</div>
        <div class="process-title">Каркас і коробка</div>
        <div class="process-time">~ 3 тижні</div>
        <div class="process-desc">Збірка деревʼяного каркасу, обшивка, вікна та зовнішні двері.</div>
      </div>
    </div>
    <div class="process-item reveal reveal-delay-3">
      <img src="https://images.unsplash.com/photo-1690719095815-549c60090c9f?auto=format&fit=crop&w=600&h=800&q=80" alt="Дах" loading="lazy">
      <div class="process-overlay">
        <div class="process-num">03</div>
        <div class="process-title">Дах</div>
        <div class="process-time">~ 1 тиждень</div>
        <div class="process-desc">Стропильна система, гідро- й теплоізоляція, покрівельне покриття.</div>
      </div>
    </div>
    <div class="process-item reveal reveal-delay-4">
      <img src="https://images.unsplash.com/photo-1656733911001-16912b79d2bf?auto=format&fit=crop&w=600&h=800&q=80" alt="Оздоблення" loading="lazy">
      <div class="process-overlay">
        <div class="process-num">04</div>
        <div class="process-title">Оздоблення</div>
        <div class="process-time">~ 6 тижнів</div>
        <div class="process-desc">Інженерні мережі, утеплення, чорнове і фінішне оздоблення.</div>
      </div>
    </div>
  </div>
  <div class="process-cta reveal">
    <p>Готові обговорити ваш проєкт? Залиште заявку — інженер передзвонить і допоможе підібрати оптимальний план.</p>
    <a href="#contact-form" class="btn-primary">Отримати консультацію</a>
  </div>
</section>

<!-- TECH -->
<section id="tech">
  <div class="reveal">
    <div class="eyebrow">Технологія</div>
    <h2>Чому каркасна технологія</h2>
    <p class="section-lead">Чотири причини, чому каркас обирають для швидкого та комфортного будівництва.</p>
  </div>
  <div class="tech-grid">
    <div class="tech-card reveal reveal-delay-1">
      <svg class="tech-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
        <circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/>
      </svg>
      <h3>Швидкість</h3>
      <p>Відсутній «мокрий» процес і час на висихання — каркас монтується за тижні, не місяці.</p>
      <div class="tech-accent">01</div>
    </div>
    <div class="tech-card reveal reveal-delay-2">
      <svg class="tech-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
        <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/>
      </svg>
      <h3>Енергоефективність</h3>
      <p>Багатошарова теплоізоляція знижує витрати на опалення вдвічі порівняно з цеглою.</p>
      <div class="tech-accent">02</div>
    </div>
    <div class="tech-card reveal reveal-delay-3">
      <svg class="tech-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
        <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/>
      </svg>
      <h3>Екологічність</h3>
      <p>Деревина — відновлюваний матеріал з природним мікрокліматом усередині будинку.</p>
      <div class="tech-accent">03</div>
    </div>
    <div class="tech-card reveal reveal-delay-4">
      <svg class="tech-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
        <polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/>
      </svg>
      <h3>Стійкість</h3>
      <p>Легка гнучка конструкція добре переносить вітрові та сейсмічні навантаження.</p>
      <div class="tech-accent">04</div>
    </div>
  </div>
</section>

<!-- PORTFOLIO -->
<section id="portfolio">
  <div class="portfolio-header reveal">
    <div class="eyebrow">Портфоліо</div>
    <h2>Реалізовані об'єкти</h2>
    <p class="section-lead">Кілька каркасних будинків, які ми збудували за останній рік.</p>
  </div>
  <div class="portfolio-grid">
    <div class="port-item reveal reveal-delay-1">
      <img src="https://images.unsplash.com/photo-1668015642046-22044ddc7247?auto=format&fit=crop&w=800&h=1000&q=80" alt="Будинок Сосновий" loading="lazy">
      <div class="port-overlay">
        <div class="port-tag">145 м² · 4 місяці · Київська обл.</div>
        <div class="port-title">Будинок «Сосновий»</div>
      </div>
    </div>
    <div class="port-item reveal reveal-delay-2">
      <img src="https://images.unsplash.com/photo-1542299861-7c9d068a5edf?auto=format&fit=crop&w=800&h=490&q=80" alt="Будинок Кленовий" loading="lazy">
      <div class="port-overlay">
        <div class="port-tag">180 м² · 5 місяців · Бучанський р-н</div>
        <div class="port-title">Будинок «Кленовий»</div>
      </div>
    </div>
    <div class="port-item reveal reveal-delay-3">
      <img src="https://images.unsplash.com/photo-1502304104451-b61947b321ca?auto=format&fit=crop&w=800&h=490&q=80" alt="Будинок Дубовий" loading="lazy">
      <div class="port-overlay">
        <div class="port-tag">120 м² · 3.5 місяці · Обухівський р-н</div>
        <div class="port-title">Будинок «Дубовий»</div>
      </div>
    </div>
  </div>
  <div class="portfolio-cta reveal">
    <p>Сподобався один із проєктів? Можемо адаптувати будь-який план під ваш бюджет і ділянку.</p>
    <a href="#contact-form" class="btn-primary">Обговорити проєкт</a>
  </div>
</section>

<!-- WHY -->
<section id="why">
  <div class="reveal">
    <div class="eyebrow" style="color:rgba(245,240,232,.5)">Чому ми</div>
    <h2>Чому обирають ЯВІР</h2>
    <p class="section-lead">Чотири причини, чому клієнти рекомендують нас знайомим.</p>
  </div>
  <div class="why-grid">
    <div class="why-card reveal reveal-delay-1">
      <div class="why-num">01</div>
      <h3>Фіксована ціна</h3>
      <p>Вартість прописана в договорі та не змінюється до завершення будівництва.</p>
    </div>
    <div class="why-card reveal reveal-delay-2">
      <div class="why-num">02</div>
      <h3>Власна бригада</h3>
      <p>Будуємо силами штатних майстрів — без субпідрядників і втрати якості.</p>
    </div>
    <div class="why-card reveal reveal-delay-3">
      <div class="why-num">03</div>
      <h3>Гарантія 10 років</h3>
      <p>Письмова гарантія на каркас і конструктивні елементи будинку.</p>
    </div>
    <div class="why-card reveal reveal-delay-4">
      <div class="why-num">04</div>
      <h3>Щотижневі звіти</h3>
      <p>Фото й відео з об'єкта щотижня — бачите прогрес, навіть якщо ви не в Україні.</p>
    </div>
  </div>
</section>

<!-- STEPS -->
<section id="steps">
  <div class="reveal">
    <div class="eyebrow">Співпраця</div>
    <h2>Як ми працюємо</h2>
    <p class="section-lead">Пʼять простих кроків від першого дзвінка до отримання ключів.</p>
  </div>
  <div class="steps-list">
    <div class="step-row reveal reveal-delay-1">
      <div class="step-index">01</div>
      <div class="step-body">
        <h3>Консультація</h3>
        <p>Обговорюємо бажання, бюджет і ділянку — безкоштовно та без зобовʼязань.</p>
      </div>
    </div>
    <div class="step-row reveal reveal-delay-2">
      <div class="step-index">02</div>
      <div class="step-body">
        <h3>Проєкт</h3>
        <p>Готуємо план будинку і детальний кошторис під ваш запит.</p>
      </div>
    </div>
    <div class="step-row reveal reveal-delay-3">
      <div class="step-index">03</div>
      <div class="step-body">
        <h3>Договір</h3>
        <p>Фіксуємо ціну та терміни на папері — зміни можливі лише за вашою ініціативою.</p>
      </div>
    </div>
    <div class="step-row reveal reveal-delay-4">
      <div class="step-index">04</div>
      <div class="step-body">
        <h3>Будівництво</h3>
        <p>Будуємо за погодженим графіком зі щотижневою фотозвітністю.</p>
      </div>
    </div>
    <div class="step-row reveal">
      <div class="step-index">05</div>
      <div class="step-body">
        <h3>Здача</h3>
        <p>Підписуємо акт виконаних робіт і урочисто передаємо ключі.</p>
      </div>
    </div>
  </div>
</section>

<!-- REVIEWS -->
<section id="reviews">
  <div class="reveal">
    <div class="eyebrow">Відгуки</div>
    <h2>Що кажуть наші клієнти</h2>
    <p class="section-lead">Понад 120 родин уже живуть у будинках ЯВІР.</p>
  </div>
  <div class="reviews-grid">
    <div class="review-card reveal reveal-delay-1">
      <div class="stars">★★★★★</div>
      <p class="review-text">Будинок здали на тиждень раніше обіцяного. Жодного подорожчання — все, як у договорі.</p>
      <div class="reviewer">
        <div class="reviewer-avatar">ІК</div>
        <div>
          <div class="reviewer-name">Ігор К.</div>
          <div class="reviewer-meta">Будинок 145 м² · 2025</div>
        </div>
      </div>
    </div>
    <div class="review-card reveal reveal-delay-2">
      <div class="stars">★★★★★</div>
      <p class="review-text">Дуже сподобались щотижневі фотозвіти — будували, поки я був за кордоном, і все було видно.</p>
      <div class="reviewer">
        <div class="reviewer-avatar">НП</div>
        <div>
          <div class="reviewer-name">Наталія П.</div>
          <div class="reviewer-meta">Будинок 120 м² · 2024</div>
        </div>
      </div>
    </div>
    <div class="review-card reveal reveal-delay-3">
      <div class="stars">★★★★★</div>
      <p class="review-text">Бригада дуже акуратна, ділянку прибрали ідеально. Рекомендуємо всім друзям, хто будується.</p>
      <div class="reviewer">
        <div class="reviewer-avatar">ОВ</div>
        <div>
          <div class="reviewer-name">Олексій В.</div>
          <div class="reviewer-meta">Будинок 180 м² · 2025</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<div id="contact-form">
  <div class="contact-left">
    <div>
      <div class="eyebrow" style="color:rgba(200,168,75,.7)">Контакти</div>
      <h2>Отримайте точний розрахунок</h2>
      <p class="section-lead">Заповніть форму — інженер зателефонує протягом робочого дня.</p>
    </div>
    <div class="contact-info">
      <div class="contact-info-item">
        <div class="contact-info-label">Офіс</div>
        <div class="contact-info-val">м. Київ, вул. Велика Васильківська, 100</div>
      </div>
      <div class="contact-info-item">
        <div class="contact-info-label">Телефон</div>
        <div class="contact-info-val">+380 67 234 56 78</div>
      </div>
      <div class="contact-info-item">
        <div class="contact-info-label">Графік роботи</div>
        <div class="contact-info-val">Пн–Сб: 9:00–19:00</div>
      </div>
    </div>
  </div>
  <div class="contact-right">
    <h3>Калькулятор вартості</h3>

    <div class="calc-block">
      <div class="calc-label">
        Площа будинку, м²
        <span id="areaLabel">100 м²</span>
      </div>
      <input type="range" id="areaSlider" min="60" max="300" value="100" step="5">
    </div>

    <div class="calc-block">
      <div class="calc-label">Комплектація</div>
      <div class="combo-select">
        <button class="combo-btn" data-mult="1" onclick="setCombo(this, 1)">Економ</button>
        <button class="combo-btn active" data-mult="1.4" onclick="setCombo(this, 1.4)">Стандарт</button>
        <button class="combo-btn" data-mult="1.9" onclick="setCombo(this, 1.9)">Преміум</button>
      </div>
    </div>

    <div class="price-display">
      <div class="price-label">Орієнтовна вартість</div>
      <div class="price-val" id="priceOut">₴ 2 800 000</div>
    </div>

    <div id="contactFormInner">
      <div class="form-row">
        <div class="field">
          <label>Ваше ім'я</label>
          <input type="text" id="nameInput" placeholder="Ігор">
        </div>
        <div class="field">
          <label>Телефон</label>
          <input type="tel" id="phoneInput" placeholder="+380 67 000 00 00">
        </div>
      </div>
      <button class="submit-btn" onclick="submitForm()">Отримати точний розрахунок →</button>
    </div>
    <div class="success-msg" id="successMsg">
      <h4>Дякуємо!</h4>
      <p>Інженер зателефонує вам протягом робочого дня для уточнення деталей.</p>
    </div>
  </div>
</div>

<!-- FOOTER -->
<footer>
  <div class="footer-brand">
    <div class="footer-logo">ЯВ<span>І</span>Р</div>
    <p class="footer-desc">Каркасні будинки під ключ у Києві та області. Будуємо швидко, чесно і за фіксованою ціною.</p>
  </div>
  <div class="footer-col">
    <h4>Компанія</h4>
    <ul>
      <li><a href="#tech">Технологія</a></li>
      <li><a href="#portfolio">Портфоліо</a></li>
      <li><a href="#why">Чому ми</a></li>
      <li><a href="#process">Етапи</a></li>
    </ul>
  </div>
  <div class="footer-col">
    <h4>Контакти</h4>
    <ul>
      <li><a href="tel:+380672345678">+380 67 234 56 78</a></li>
      <li><a href="#">вул. В. Васильківська, 100</a></li>
      <li><a href="#">Пн–Сб 9:00–19:00</a></li>
    </ul>
  </div>
</footer>
<div class="footer-bottom">
  <span>© 2026 ЯВІР. Усі права захищені.</span>
  <span>Каркасне будівництво · Київ та область</span>
</div>

<script>
  // NAV scroll
  const navbar = document.getElementById('navbar');
  window.addEventListener('scroll', () => {
    navbar.classList.toggle('scrolled', window.scrollY > 60);
  });

  // Burger
  const burger = document.getElementById('burger');
  const mobileMenu = document.getElementById('mobileMenu');
  burger.addEventListener('click', () => {
    burger.classList.toggle('open');
    mobileMenu.classList.toggle('open');
  });
  function closeMobile() {
    burger.classList.remove('open');
    mobileMenu.classList.remove('open');
  }

  // Counters
  function animateCounters() {
    document.querySelectorAll('[data-target]').forEach(el => {
      const target = parseInt(el.dataset.target);
      const hasSup = el.querySelector('sup');
      const supHTML = hasSup ? hasSup.outerHTML : '';
      let current = 0;
      const step = Math.ceil(target / 40);
      const timer = setInterval(() => {
        current = Math.min(current + step, target);
        el.innerHTML = supHTML + current;
        if (current >= target) clearInterval(timer);
      }, 30);
    });
  }

  // Scroll reveal + trigger counters once
  let countersRan = false;
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
      }
    });
    // Trigger counters when hero stats are visible
    if (!countersRan) {
      animateCounters();
      countersRan = true;
    }
  }, { threshold: 0.12 });
  reveals.forEach(r => observer.observe(r));
  // Always animate counters on load
  setTimeout(animateCounters, 400);

  // Calculator
  let comboMult = 1.4;
  const BASE_PRICE_PER_SQM = 20000;

  function calcPrice() {
    const area = parseInt(document.getElementById('areaSlider').value);
    document.getElementById('areaLabel').textContent = area + ' м²';
    const total = Math.round(area * BASE_PRICE_PER_SQM * comboMult / 100) * 100;
    document.getElementById('priceOut').textContent = '₴ ' + total.toLocaleString('uk-UA');
  }

  function setCombo(btn, mult) {
    document.querySelectorAll('.combo-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    comboMult = mult;
    calcPrice();
  }

  document.getElementById('areaSlider').addEventListener('input', calcPrice);
  calcPrice();

  // Form submit
  function submitForm() {
    const name = document.getElementById('nameInput').value.trim();
    const phone = document.getElementById('phoneInput').value.trim();
    if (!name || !phone) {
      alert('Будь ласка, заповніть ім\'я та телефон');
      return;
    }
    document.getElementById('contactFormInner').style.display = 'none';
    document.getElementById('successMsg').classList.add('show');
  }

  // Reduced motion
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    document.querySelectorAll('.reveal').forEach(el => el.classList.add('visible'));
  }
</script>
</body>
</html>
