<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Luxury Salon Experience</title>
  <meta name="description" content="Premium luxury salon website with modern animations, parallax, gallery lightbox, and interactive services." />

  <style>
    :root{
      --bg0:#05070f;
      --bg1:#060b18;
      --panel: rgba(255,255,255,.04);
      --panel2: rgba(255,255,255,.06);
      --stroke: rgba(255,255,255,.10);
      --stroke2: rgba(255,255,255,.18);
      --gold:#d6b25e;
      --gold2:#f0d68a;
      --cyan:#18e6ff;
      --cyan2:#74f7ff;
      --text:#e9f0ff;
      --muted: rgba(233,240,255,.72);
      --shadow: 0 18px 60px rgba(0,0,0,.55);
      --shadow2: 0 10px 30px rgba(0,0,0,.35);
      --radius: 18px;
      --radius2: 26px;
      --max: 1180px;
      --ease: cubic-bezier(.2,.8,.2,1);
      --ease2: cubic-bezier(.1,.9,.2,1);
    }

    *{ box-sizing: border-box; }
    html{ scroll-behavior: smooth; }
    body{
      margin:0;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji","Segoe UI Emoji";
      color: var(--text);
      background:
        radial-gradient(1200px 800px at 70% -10%, rgba(24,230,255,.14), transparent 55%),
        radial-gradient(900px 650px at 12% 10%, rgba(214,178,94,.12), transparent 52%),
        linear-gradient(180deg, var(--bg0), var(--bg1));
      overflow-x: hidden;
    }

    /* Ambient film grain */
    body::before{
      content:"";
      position: fixed;
      inset: 0;
      pointer-events: none;
      background-image:
        url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="260" height="260"><filter id="n"><feTurbulence type="fractalNoise" baseFrequency="0.8" numOctaves="4" stitchTiles="stitch"/></filter><rect width="260" height="260" filter="url(%23n)" opacity="0.35"/></svg>');
      mix-blend-mode: overlay;
      opacity: .07;
      transform: translateZ(0);
      z-index: 0;
    }

    /* Three.js particle canvas */
    #particles{
      position: fixed;
      inset: 0;
      width: 100%;
      height: 100%;
      z-index: 0;
      pointer-events: none;
      opacity: .95;
    }

    /* Layout */
    .app{ position: relative; z-index: 1; }

    .topbar{
      position: fixed;
      top: 0;
      left:0;
      right:0;
      z-index: 50;
      backdrop-filter: blur(10px);
      background: linear-gradient(180deg, rgba(4,7,15,.75), rgba(4,7,15,.40));
      border-bottom: 1px solid rgba(255,255,255,.08);
    }
    .topbar-inner{
      max-width: var(--max);
      margin: 0 auto;
      padding: 14px 18px;
      display:flex;
      align-items:center;
      justify-content: space-between;
      gap: 14px;
    }

    .brand{
      display:flex;
      align-items:center;
      gap: 12px;
      user-select:none;
    }
    .brand-mark{
      width: 38px; height: 38px;
      border-radius: 12px;
      background:
        radial-gradient(circle at 30% 30%, rgba(240,214,138,.45), transparent 55%),
        linear-gradient(135deg, rgba(24,230,255,.18), rgba(214,178,94,.22));
      border: 1px solid rgba(255,255,255,.12);
      box-shadow: 0 0 0 1px rgba(24,230,255,.12), 0 16px 50px rgba(0,0,0,.45);
      position: relative;
      overflow: hidden;
    }
    .brand-mark::after{
      content:"";
      position:absolute;
      inset:-40% -40%;
      background: conic-gradient(from 200deg, rgba(24,230,255,.0), rgba(24,230,255,.35), rgba(214,178,94,.35), rgba(24,230,255,.0));
      animation: spin 8s linear infinite;
      opacity:.85;
    }
    @keyframes spin{ to { transform: rotate(360deg); } }

    .brand h1{
      margin:0;
      font-size: 14px;
      letter-spacing: .18em;
      text-transform: uppercase;
      color: rgba(233,240,255,.86);
    }
    .brand small{
      display:block;
      margin-top: 2px;
      font-size: 12px;
      letter-spacing: .06em;
      color: rgba(214,178,94,.92);
    }

    .nav{
      display:flex;
      align-items:center;
      gap: 12px;
      flex-wrap: wrap;
      justify-content: flex-end;
    }
    .nav a{
      color: rgba(233,240,255,.78);
      text-decoration: none;
      font-size: 13px;
      padding: 8px 10px;
      border-radius: 12px;
      border: 1px solid rgba(255,255,255,.0);
      transition: transform .25s var(--ease), border-color .25s var(--ease), background .25s var(--ease), color .25s var(--ease);
    }
    .nav a:hover{
      transform: translateY(-1px);
      background: rgba(255,255,255,.04);
      border-color: rgba(24,230,255,.20);
      color: rgba(255,255,255,.92);
    }

    .cta-mini{
      display:inline-flex;
      align-items:center;
      gap: 10px;
      padding: 10px 14px;
      border-radius: 14px;
      text-decoration: none;
      color: rgba(6,10,20,.95);
      background: linear-gradient(135deg, rgba(24,230,255,.95), rgba(214,178,94,.95));
      font-weight: 700;
      border: 1px solid rgba(255,255,255,.22);
      box-shadow: 0 18px 60px rgba(24,230,255,.12), 0 18px 60px rgba(214,178,94,.10);
      transition: transform .25s var(--ease), filter .25s var(--ease);
      white-space: nowrap;
    }
    .cta-mini:hover{ transform: translateY(-1px) scale(1.01); filter: saturate(1.1); }

    section{
      padding: 92px 18px;
      position: relative;
    }

    .container{ max-width: var(--max); margin: 0 auto; }

    /* Scroll reveal */
    .reveal{
      opacity: 0;
      transform: translateY(18px);
      transition: opacity .7s var(--ease), transform .7s var(--ease);
    }
    .reveal.visible{
      opacity: 1;
      transform: translateY(0);
    }

    /* Hero */
    #hero{
      min-height: 100vh;
      padding-top: 92px;
      display:flex;
      align-items: center;
      overflow: hidden;
      border-bottom: 1px solid rgba(255,255,255,.08);
    }

    .hero-bg{
      position:absolute;
      inset: 0;
      z-index: 0;
      background:
        radial-gradient(900px 450px at 50% 20%, rgba(24,230,255,.13), transparent 60%),
        radial-gradient(800px 600px at 10% 30%, rgba(214,178,94,.12), transparent 55%),
        radial-gradient(1200px 700px at 90% 70%, rgba(24,230,255,.08), transparent 60%);
    }

    .hero-parallax{
      position:absolute;
      inset:-40px;
      z-index: 0;
      background:
        linear-gradient(180deg, rgba(0,0,0,.0), rgba(0,0,0,.35)),
        repeating-linear-gradient(90deg, rgba(255,255,255,.03), rgba(255,255,255,.03) 1px, transparent 1px, transparent 16px),
        repeating-linear-gradient(0deg, rgba(255,255,255,.02), rgba(255,255,255,.02) 1px, transparent 1px, transparent 16px);
      opacity: .45;
      transform: translateY(var(--pY, 0px));
      filter: blur(.2px);
    }

    .hero-grid-glow{
      position:absolute;
      inset: -20% -10%;
      z-index: 0;
      background:
        radial-gradient(circle at 70% 30%, rgba(214,178,94,.20), transparent 45%),
        radial-gradient(circle at 22% 62%, rgba(24,230,255,.17), transparent 40%);
      opacity: .8;
      transform: translateY(calc(var(--pY, 0px) * .35));
    }

    .hero-inner{
      z-index: 1;
      position: relative;
      display:grid;
      grid-template-columns: 1.2fr .8fr;
      gap: 26px;
      align-items: center;
    }

    .hero-copy{
      padding: 22px;
    }

    .kicker{
      display:inline-flex;
      align-items:center;
      gap: 10px;
      padding: 10px 14px;
      border-radius: 999px;
      background: rgba(255,255,255,.03);
      border: 1px solid rgba(255,255,255,.10);
      box-shadow: 0 0 0 1px rgba(24,230,255,.10) inset;
      color: rgba(233,240,255,.82);
      font-size: 13px;
      letter-spacing: .08em;
      text-transform: uppercase;
    }
    .kicker b{
      color: var(--gold2);
      text-shadow: 0 0 24px rgba(214,178,94,.28);
    }
    .dot{
      width: 9px; height: 9px;
      border-radius: 50%;
      background: radial-gradient(circle at 30% 30%, #fff, rgba(255,255,255,.0) 45%),
                  linear-gradient(135deg, rgba(24,230,255,.95), rgba(214,178,94,.95));
      box-shadow: 0 0 0 1px rgba(255,255,255,.12), 0 0 18px rgba(24,230,255,.35);
    }

    .hero-title{
      margin: 18px 0 12px;
      font-size: clamp(38px, 4.6vw, 62px);
      line-height: 1.02;
      letter-spacing: -0.02em;
    }

    .gradient-text{
      background: linear-gradient(90deg, rgba(214,178,94,1), rgba(240,214,138,1), rgba(24,230,255,1));
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      text-shadow:
        0 0 18px rgba(214,178,94,.22),
        0 0 36px rgba(24,230,255,.12);
    }

    .hero-sub{
      margin: 0 0 22px;
      max-width: 56ch;
      color: var(--muted);
      font-size: 16px;
      line-height: 1.7;
    }

    .hero-actions{
      display:flex;
      align-items:center;
      gap: 14px;
      flex-wrap: wrap;
    }

    .cta{
      position: relative;
      display:inline-flex;
      align-items:center;
      gap: 10px;
      padding: 14px 18px;
      border-radius: 16px;
      text-decoration:none;
      font-weight: 900;
      letter-spacing: .02em;
      color: rgba(6,10,20,.98);
      background: linear-gradient(135deg, rgba(24,230,255,1), rgba(214,178,94,1));
      border: 1px solid rgba(255,255,255,.24);
      box-shadow: 0 22px 70px rgba(24,230,255,.14), 0 22px 70px rgba(214,178,94,.12);
      overflow:hidden;
      transform: translateZ(0);
      transition: transform .25s var(--ease), filter .25s var(--ease);
    }
    .cta:hover{ transform: translateY(-2px); filter: saturate(1.1); }

    .cta::before{
      content:"";
      position:absolute;
      inset:-2px;
      background:
        conic-gradient(from 180deg,
          rgba(24,230,255,.0), rgba(24,230,255,.35), rgba(214,178,94,.40), rgba(24,230,255,.0));
      opacity: .85;
      filter: blur(10px);
      animation: glowSpin 5.5s linear infinite;
    }
    @keyframes glowSpin{ to{ transform: rotate(360deg);} }

    .cta > span{ position:relative; z-index: 2; }
    .cta svg{ position: relative; z-index: 2; }

    .secondary-pill{
      display:inline-flex;
      align-items:center;
      gap: 10px;
      padding: 12px 16px;
      border-radius: 999px;
      text-decoration:none;
      border: 1px solid rgba(255,255,255,.14);
      background: rgba(255,255,255,.03);
      color: rgba(233,240,255,.88);
      box-shadow: 0 0 0 1px rgba(214,178,94,.10) inset;
      transition: transform .25s var(--ease), border-color .25s var(--ease), background .25s var(--ease);
      user-select: none;
    }
    .secondary-pill:hover{
      transform: translateY(-2px);
      border-color: rgba(24,230,255,.26);
      background: rgba(255,255,255,.05);
    }

    .hero-side{
      position: relative;
      border-radius: var(--radius2);
      background: linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.02));
      border: 1px solid rgba(255,255,255,.12);
      box-shadow: var(--shadow2);
      padding: 18px;
      overflow:hidden;
    }

    .hero-side::before{
      content:"";
      position:absolute;
      inset:-1px;
      background:
        radial-gradient(600px 240px at 30% 10%, rgba(24,230,255,.20), transparent 60%),
        radial-gradient(500px 220px at 90% 65%, rgba(214,178,94,.18), transparent 62%);
      opacity: .9;
      pointer-events:none;
    }

    .hero-side-inner{ position:relative; z-index:1; }

    .stat-row{
      display:grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
      margin-top: 12px;
    }
    .stat{
      padding: 14px;
      border-radius: 16px;
      border: 1px solid rgba(255,255,255,.10);
      background: rgba(255,255,255,.03);
      transition: transform .3s var(--ease), border-color .3s var(--ease);
    }
    .stat:hover{ transform: translateY(-3px); border-color: rgba(24,230,255,.22); }

    .stat b{ display:block; font-size: 18px; letter-spacing: .02em; }
    .stat small{ color: rgba(233,240,255,.72); display:block; margin-top: 6px; line-height: 1.35; }

    .glow-border{
      position:absolute;
      inset: 10px;
      border-radius: calc(var(--radius2) - 8px);
      border: 1px solid rgba(24,230,255,.12);
      box-shadow:
        0 0 0 1px rgba(214,178,94,.08) inset,
        0 0 40px rgba(24,230,255,.12);
      pointer-events:none;
      opacity: .9;
    }

    /* Shared heading */
    .section-head{
      display:flex;
      align-items:flex-end;
      justify-content: space-between;
      gap: 18px;
      margin-bottom: 22px;
    }
    .section-head h2{
      margin:0;
      font-size: clamp(26px, 3vw, 38px);
      letter-spacing: -.02em;
    }
    .section-head p{
      margin:0;
      color: var(--muted);
      max-width: 62ch;
      line-height: 1.7;
    }

    /* About cards */
    .about-grid{
      display:grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
    }

    .tilt-card{
      position: relative;
      border-radius: var(--radius2);
      background: linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.02));
      border: 1px solid rgba(255,255,255,.12);
      box-shadow: var(--shadow2);
      padding: 18px;
      overflow:hidden;
      transform: translateZ(0);
    }

    .tilt-card::after{
      content:"";
      position:absolute;
      inset:-2px;
      background:
        radial-gradient(600px 260px at var(--mx, 50%) var(--my, 10%), rgba(24,230,255,.18), transparent 55%),
        radial-gradient(500px 240px at calc(var(--mx, 50%) + 20%) calc(var(--my, 10%) + 40%), rgba(214,178,94,.14), transparent 60%);
      opacity:.9;
      pointer-events:none;
      transition: opacity .4s var(--ease);
    }

    .tilt-card:hover::after{ opacity: 1; }

    .card-content{ position: relative; z-index: 1; }

    .about-pill{
      display:inline-flex;
      align-items:center;
      gap: 10px;
      padding: 10px 14px;
      border-radius: 999px;
      border: 1px solid rgba(255,255,255,.14);
      background: rgba(255,255,255,.03);
      color: rgba(233,240,255,.85);
      font-size: 13px;
      letter-spacing: .06em;
      text-transform: uppercase;
    }

    .about-pill svg{ filter: drop-shadow(0 0 10px rgba(24,230,255,.2)); }

    .about-title{
      margin: 14px 0 10px;
      font-size: 22px;
      letter-spacing: -.01em;
    }

    .about-text{
      margin:0;
      color: rgba(233,240,255,.74);
      line-height: 1.75;
      font-size: 15px;
    }

    .about-list{
      margin: 14px 0 0;
      padding:0;
      list-style:none;
      display:grid;
      gap: 10px;
    }
    .about-list li{
      display:flex;
      align-items:flex-start;
      gap: 10px;
      color: rgba(233,240,255,.80);
    }
    .check{
      width: 18px; height: 18px;
      border-radius: 6px;
      border: 1px solid rgba(255,255,255,.18);
      background: rgba(255,255,255,.03);
      display:grid;
      place-items:center;
      flex: 0 0 auto;
      box-shadow: 0 0 20px rgba(24,230,255,.10);
    }

    /* Services */
    .services-wrap{
      position: relative;
    }

    .service-grid{
      display:grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 12px;
    }

    @media (max-width: 980px){
      .hero-inner{ grid-template-columns: 1fr; }
      .hero-side{ max-width: 520px; }
      .about-grid{ grid-template-columns: 1fr; }
      .service-grid{ grid-template-columns: repeat(2, 1fr); }
    }

    @media (max-width: 520px){
      section{ padding: 78px 14px; }
      .service-grid{ grid-template-columns: 1fr; }
      .topbar-inner{ padding: 12px 14px; }
      .nav{ display:none; }
    }

    .service-card{
      border-radius: 18px;
      background: rgba(255,255,255,.03);
      border: 1px solid rgba(255,255,255,.10);
      padding: 14px;
      position: relative;
      overflow:hidden;
      cursor: pointer;
      transform: translateZ(0);
      transition: transform .35s var(--ease2), border-color .35s var(--ease2), background .35s var(--ease2);
      min-height: 140px;
    }

    .service-card::before{
      content:"";
      position:absolute;
      inset:-2px;
      background:
        radial-gradient(520px 160px at var(--sx, 50%) var(--sy, 20%), rgba(24,230,255,.18), transparent 55%),
        radial-gradient(520px 160px at calc(var(--sx, 50%) + 10%) calc(var(--sy, 20%) + 60%), rgba(214,178,94,.14), transparent 60%);
      opacity: 0;
      transition: opacity .35s var(--ease2);
      pointer-events:none;
    }
    .service-card:hover{
      transform: translateY(-6px);
      border-color: rgba(24,230,255,.25);
      background: rgba(255,255,255,.05);
    }
    .service-card:hover::before{ opacity: 1; }

    .service-top{ display:flex; align-items:flex-start; justify-content: space-between; gap: 12px; position: relative; z-index: 1; }
    .service-icon{
      width: 44px; height: 44px;
      border-radius: 16px;
      background: linear-gradient(135deg, rgba(24,230,255,.16), rgba(214,178,94,.16));
      border: 1px solid rgba(255,255,255,.12);
      box-shadow: 0 0 0 1px rgba(24,230,255,.10) inset, 0 20px 60px rgba(0,0,0,.25);
      display:grid;
      place-items:center;
      flex: 0 0 auto;
    }
    .service-icon svg{ width: 22px; height: 22px; }

    .service-card h3{ margin: 0; font-size: 15px; letter-spacing: .02em; position:relative; z-index:1; }
    .service-card .tag{
      margin-top: 10px;
      display:inline-flex;
      gap: 8px;
      align-items:center;
      font-size: 12px;
      color: rgba(233,240,255,.70);
      position:relative; z-index:1;
    }
    .service-card .tag i{
      width: 10px; height: 10px; border-radius: 50%;
      background: radial-gradient(circle at 30% 30%, #fff, rgba(255,255,255,0) 45%),
                  linear-gradient(135deg, rgba(24,230,255,.95), rgba(214,178,94,.95));
      box-shadow: 0 0 18px rgba(24,230,255,.35);
      display:inline-block;
    }

    .service-expand{
      height: 0;
      overflow:hidden;
      transition: height .45s var(--ease2);
      position: relative;
      z-index: 1;
    }
    .service-expand-inner{ padding-top: 12px; }
    .service-expand p{ margin: 0; color: rgba(233,240,255,.74); line-height: 1.65; font-size: 13px; }
    .service-expand .bullets{ margin: 10px 0 0; padding: 0; list-style:none; display:grid; gap: 8px; }
    .service-expand .bullets li{ display:flex; gap: 10px; align-items:flex-start; color: rgba(233,240,255,.78); font-size: 13px; }

    .service-expanded{
      border-color: rgba(214,178,94,.30);
      background: rgba(255,255,255,.06);
    }

    /* Gallery */
    .gallery-hero{
      border-radius: var(--radius2);
      border: 1px solid rgba(255,255,255,.12);
      background: rgba(255,255,255,.03);
      box-shadow: var(--shadow2);
      overflow:hidden;
      padding: 18px;
    }

    .gallery-strip{
      position: relative;
      display:flex;
      gap: 14px;
      overflow-x: auto;
      scroll-snap-type: x mandatory;
      padding-bottom: 10px;
    }
    .gallery-strip::-webkit-scrollbar{ height: 8px; }
    .gallery-strip::-webkit-scrollbar-thumb{ background: rgba(255,255,255,.14); border-radius: 999px; }
    
    .shot{
      flex: 0 0 auto;
      width: min(280px, 78vw);
      aspect-ratio: 4 / 3;
      border-radius: 18px;
      border: 1px solid rgba(255,255,255,.12);
      background: rgba(255,255,255,.03);
      position: relative;
      overflow:hidden;
      cursor: pointer;
      scroll-snap-align: start;
      transform: perspective(800px) rotateX(var(--rx,0deg)) rotateY(var(--ry,0deg)) translateY(0);
      transition: transform .25s var(--ease2), border-color .25s var(--ease2);
      box-shadow: 0 14px 40px rgba(0,0,0,.35);
    }

    .shot:hover{
      border-color: rgba(24,230,255,.28);
      transform: perspective(900px) rotateX(var(--rx,0deg)) rotateY(var(--ry,0deg)) translateY(-6px);
    }

    .shot img{
      width:100%; height:100%; object-fit: cover;
      filter: saturate(1.05) contrast(1.05);
      transform: scale(1.02);
      transition: transform .5s var(--ease2), filter .5s var(--ease2);
      user-select:none;
      -webkit-user-drag: none;
    }
    .shot:hover img{ transform: scale(1.08); filter: saturate(1.15) contrast(1.08); }

    .shot::after{
      content:"";
      position:absolute;
      inset:0;
      background:
        radial-gradient(420px 220px at var(--mx, 50%) var(--my, 10%), rgba(24,230,255,.22), transparent 55%),
        linear-gradient(180deg, rgba(0,0,0,.00), rgba(0,0,0,.35));
      opacity: .0;
      transition: opacity .25s var(--ease2);
    }
    .shot:hover::after{ opacity: 1; }

    .gallery-note{
      margin-top: 14px;
      color: rgba(233,240,255,.72);
      font-size: 13px;
      display:flex;
      gap: 10px;
      align-items:flex-start;
    }

    /* Lightbox */
    .lightbox{
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,.65);
      display:none;
      place-items:center;
      z-index: 100;
      padding: 18px;
    }
    .lightbox.open{ display:grid; }
    .lightbox-card{
      width: min(980px, 96vw);
      border-radius: 18px;
      overflow:hidden;
      border: 1px solid rgba(255,255,255,.14);
      background: rgba(255,255,255,.04);
      box-shadow: 0 22px 90px rgba(0,0,0,.65);
      position: relative;
    }
    .lightbox-card img{ width:100%; height: auto; display:block; max-height: 75vh; object-fit: cover; }
    .lightbox-close{
      position:absolute;
      top: 10px; right: 10px;
      width: 42px; height: 42px;
      border-radius: 14px;
      border: 1px solid rgba(255,255,255,.18);
      background: rgba(0,0,0,.35);
      color: rgba(255,255,255,.92);
      cursor:pointer;
      display:grid;
      place-items:center;
      backdrop-filter: blur(8px);
      transition: transform .2s var(--ease), background .2s var(--ease);
      font-size: 18px;
    }
    .lightbox-close:hover{ transform: translateY(-1px); background: rgba(0,0,0,.45); }

    /* Pricing */
    .pricing-grid{
      display:grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 14px;
      align-items: stretch;
    }

    .price-card{
      border-radius: var(--radius2);
      background: rgba(255,255,255,.03);
      border: 1px solid rgba(255,255,255,.12);
      box-shadow: var(--shadow2);
      padding: 18px;
      position: relative;
      overflow:hidden;
      transition: transform .35s var(--ease2), border-color .35s var(--ease2), background .35s var(--ease2);
    }
    .price-card::before{
      content:"";
      position:absolute;
      inset:-2px;
      background:
        radial-gradient(640px 240px at 30% 0%, rgba(24,230,255,.18), transparent 60%),
        radial-gradient(560px 260px at 85% 70%, rgba(214,178,94,.14), transparent 60%);
      opacity: 0;
      transition: opacity .35s var(--ease2);
      pointer-events:none;
    }
    .price-card:hover{
      transform: translateY(-6px);
      border-color: rgba(24,230,255,.25);
      background: rgba(255,255,255,.05);
    }
    .price-card:hover::before{ opacity: 1; }

    .price-top{ position:relative; z-index: 1; }
    .price-tier{
      display:flex;
      justify-content: space-between;
      align-items:center;
      gap: 10px;
      margin-bottom: 12px;
    }
    .tier-name{
      font-weight: 900;
      letter-spacing: .06em;
      text-transform: uppercase;
      font-size: 13px;
      color: rgba(233,240,255,.90);
    }
    .badge{
      padding: 8px 10px;
      border-radius: 999px;
      border: 1px solid rgba(255,255,255,.16);
      background: rgba(255,255,255,.03);
      color: rgba(214,178,94,.96);
      font-weight: 800;
      font-size: 12px;
      box-shadow: 0 0 30px rgba(214,178,94,.10);
    }

    .price{
      display:flex;
      align-items:baseline;
      gap: 10px;
      margin: 8px 0 12px;
      position:relative;
      z-index:1;
    }
    .price b{
      font-size: 42px;
      letter-spacing: -.03em;
      line-height: 1;
      background: linear-gradient(90deg, rgba(240,214,138,1), rgba(24,230,255,1));
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      text-shadow: 0 0 24px rgba(24,230,255,.10);
    }
    .price small{ color: rgba(233,240,255,.70); }

    .price-desc{ margin: 0 0 14px; color: rgba(233,240,255,.72); line-height: 1.7; }

    .price-list{ margin: 0; padding: 0; list-style:none; display:grid; gap: 10px; position:relative; z-index:1; }
    .price-list li{ display:flex; gap: 10px; align-items:flex-start; color: rgba(233,240,255,.80); font-size: 14px; }

    .price-action{ margin-top: 16px; position:relative; z-index:1; }
    .btn-outline{
      width:100%;
      display:inline-flex;
      justify-content:center;
      align-items:center;
      gap: 10px;
      padding: 12px 14px;
      border-radius: 16px;
      border: 1px solid rgba(255,255,255,.16);
      background: rgba(255,255,255,.03);
      color: rgba(233,240,255,.92);
      text-decoration: none;
      font-weight: 850;
      letter-spacing: .02em;
      transition: transform .25s var(--ease), border-color .25s var(--ease), background .25s var(--ease);
    }
    .btn-outline:hover{
      transform: translateY(-2px);
      border-color: rgba(24,230,255,.25);
      background: rgba(255,255,255,.05);
    }

    /* Contact */
    .contact-grid{
      display:grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
      align-items: start;
    }
    @media (max-width: 980px){
      .pricing-grid{ grid-template-columns: 1fr; }
      .contact-grid{ grid-template-columns: 1fr; }
    }

    .form-card{
      border-radius: var(--radius2);
      background: rgba(255,255,255,.03);
      border: 1px solid rgba(255,255,255,.12);
      box-shadow: var(--shadow2);
      padding: 18px;
      overflow:hidden;
      position: relative;
    }

    .form-card::before{
      content:"";
      position:absolute;
      inset:-2px;
      background:
        radial-gradient(700px 260px at 15% 10%, rgba(24,230,255,.18), transparent 60%),
        radial-gradient(600px 280px at 90% 70%, rgba(214,178,94,.14), transparent 60%);
      opacity: .7;
      pointer-events:none;
    }

    .form-inner{ position: relative; z-index: 1; }

    .form-title{ margin:0 0 10px; font-size: 20px; }

    .form-hint{ margin: 0 0 16px; color: rgba(233,240,255,.72); line-height: 1.7; font-size: 14px; }

    form{ display:grid; gap: 12px; }

    .field{
      display:grid;
      gap: 8px;
    }
    label{ font-size: 13px; color: rgba(233,240,255,.80); letter-spacing: .02em; }

    input, textarea{
      width: 100%;
      border-radius: 16px;
      border: 1px solid rgba(255,255,255,.14);
      background: rgba(0,0,0,.18);
      color: rgba(233,240,255,.92);
      padding: 12px 14px;
      outline: none;
      transition: border-color .25s var(--ease), box-shadow .25s var(--ease), transform .25s var(--ease);
      box-shadow: 0 0 0 rgba(24,230,255,.0);
    }
    textarea{ min-height: 120px; resize: vertical; }

    input:focus, textarea:focus{
      border-color: rgba(24,230,255,.40);
      box-shadow: 0 0 0 4px rgba(24,230,255,.10), 0 0 30px rgba(24,230,255,.16);
      transform: translateY(-1px);
    }

    .submit{
      display:flex;
      align-items:center;
      justify-content: space-between;
      gap: 12px;
      margin-top: 4px;
      flex-wrap: wrap;
    }

    .btn-gradient{
      flex: 1 1 auto;
      display:inline-flex;
      align-items:center;
      justify-content:center;
      gap: 10px;
      padding: 13px 16px;
      border-radius: 16px;
      border: 1px solid rgba(255,255,255,.22);
      color: rgba(6,10,20,.98);
      background: linear-gradient(135deg, rgba(24,230,255,1), rgba(214,178,94,1));
      font-weight: 950;
      cursor: pointer;
      transition: transform .25s var(--ease), filter .25s var(--ease);
      min-width: 220px;
    }
    .btn-gradient:hover{ transform: translateY(-2px); filter: saturate(1.1); }

    .status{
      flex: 1 1 auto;
      color: rgba(233,240,255,.76);
      font-size: 13px;
      line-height: 1.5;
    }

    .map-card{
      border-radius: var(--radius2);
      border: 1px solid rgba(255,255,255,.12);
      background: rgba(255,255,255,.03);
      box-shadow: var(--shadow2);
      overflow:hidden;
      position: relative;
      min-height: 420px;
    }
    .map-card::before{
      content:"";
      position:absolute;
      inset:-2px;
      background:
        radial-gradient(700px 260px at 75% 0%, rgba(214,178,94,.14), transparent 60%),
        radial-gradient(700px 260px at 15% 70%, rgba(24,230,255,.14), transparent 60%);
      opacity: .6;
      pointer-events:none;
    }
    .map-inner{ position:relative; z-index:1; height:100%; }
    .map-inner iframe{ width:100%; height:100%; border:0; filter: grayscale(35%) saturate(1.1) contrast(1.05); }

    footer{
      padding: 36px 18px;
      color: rgba(233,240,255,.70);
      border-top: 1px solid rgba(255,255,255,.08);
      position: relative;
      z-index: 1;
    }
    .footer-inner{ max-width: var(--max); margin: 0 auto; display:flex; justify-content: space-between; gap: 14px; flex-wrap: wrap; }

    /* Reduce motion */
    @media (prefers-reduced-motion: reduce){
      html{ scroll-behavior: auto; }
      .reveal{ transition: none; }
      .service-card, .price-card, .cta, .btn-outline, .secondary-pill{ transition: none; }
      .cta::before{ animation: none; }
    }
  </style>
</head>
<body>
  <canvas id="particles" aria-hidden="true"></canvas>

  <div class="app">
    <header class="topbar" role="banner">
      <div class="topbar-inner">
        <div class="brand" aria-label="Luxury Salon">
          <div class="brand-mark" aria-hidden="true"></div>
          <div>
            <h1>NYTRIXX SALON</h1>
            <small>Luxury Salon Experience</small>
          </div>
        </div>

        <nav class="nav" aria-label="Primary">
          <a href="#about">About</a>
          <a href="#services">Services</a>
          <a href="#gallery">Gallery</a>
          <a href="#pricing">Pricing</a>
          <a href="#contact">Contact</a>
        </nav>

        <a class="cta-mini" href="#contact" data-scroll>
          <span>Book Appointment</span>
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
            <path d="M5 12h14" stroke="rgba(6,10,20,.95)" stroke-width="2.2" stroke-linecap="round"/>
            <path d="M13 5l7 7-7 7" stroke="rgba(6,10,20,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </a>
      </div>
    </header>

    <!-- Hero -->
    <section id="hero" aria-label="Hero">
      <div class="hero-bg" aria-hidden="true"></div>
      <div class="hero-parallax" aria-hidden="true"></div>
      <div class="hero-grid-glow" aria-hidden="true"></div>

      <div class="container hero-inner">
        <div class="hero-copy">
          <div class="kicker reveal"> <span class="dot" aria-hidden="true"></span> <span>Handcrafted beauty • <b>Gold-grade glow</b></span></div>
          <h2 class="hero-title reveal">
            <span class="gradient-text">Luxury Salon Experience</span>
          </h2>
          <p class="hero-sub reveal">
            A premium destination for hair, skin, and self-care—designed with elegant artistry and powered by modern comfort.
            Discover signature treatments, glowing ambiance, and a concierge-level booking experience.
          </p>

          <div class="hero-actions reveal">
            <a class="cta" href="#contact" data-scroll>
              <span>Book Appointment</span>
              <svg width="22" height="22" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                <path d="M7 17L17 7" stroke="rgba(6,10,20,.95)" stroke-width="2.2" stroke-linecap="round"/>
                <path d="M10 7h7v7" stroke="rgba(6,10,20,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/>
              </svg>
            </a>
            <a class="secondary-pill" href="#services" data-scroll>
              <svg width="18" height="18" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                <path d="M12 2l3 7h7l-5.6 4 2.1 8L12 18l-6.5 3 2.1-8L2 9h7l3-7z" stroke="rgba(233,240,255,.92)" stroke-width="1.8" stroke-linejoin="round"/>
              </svg>
              <span>Explore Signature Services</span>
            </a>
          </div>
        </div>

        <aside class="hero-side reveal" aria-label="Highlights">
          <div class="glow-border" aria-hidden="true"></div>
          <div class="hero-side-inner">
            <div class="about-pill">
              <svg width="18" height="18" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                <path d="M12 2l3.5 7L23 9.5l-5.5 5.2L19 22l-7-3.8L5 22l1.5-7.3L1 9.5l7.5-.5L12 2z" stroke="rgba(240,214,138,.95)" stroke-width="1.9" stroke-linejoin="round"/>
              </svg>
              <span>Premium Treatments • Modern Care</span>
            </div>

            <div class="stat-row">
              <div class="stat">
                <b>Gold-Level Finish</b>
                <small>Luxury styling with refined technique and luminous results.</small>
              </div>
              <div class="stat">
                <b>Relaxed Concierge</b>
                <small>Fast booking. Thoughtful scheduling. Smooth experience.</small>
              </div>
            </div>

            <div class="stat-row">
              <div class="stat">
                <b>Glow Skin</b>
                <small>Facials designed for hydration, clarity, and softness.</small>
              </div>
              <div class="stat">
                <b>Curated Spa</b>
                <small>Rejuvenate with spa rituals for body and mind.</small>
              </div>
            </div>
          </div>
        </aside>
      </div>
    </section>

    <!-- About -->
    <section id="about" aria-label="About Us">
      <div class="container">
        <div class="section-head">
          <div>
            <h2 class="gradient-text reveal">About Us</h2>
          </div>
          <p class="reveal">We craft each appointment like a private ceremony—elevating texture, radiance, and confidence with artistry and precision.</p>
        </div>

        <div class="about-grid">
          <article class="tilt-card reveal" data-tilt>
            <div class="card-content">
              <div class="about-pill">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                  <path d="M12 21s-7-4.4-7-11A4 4 0 0 1 12 7a4 4 0 0 1 7 3c0 6.6-7 11-7 11z" stroke="rgba(24,230,255,.95)" stroke-width="1.8" stroke-linejoin="round"/>
                </svg>
                <span>Signature Craft</span>
              </div>
              <h3 class="about-title">Elegance in every detail</h3>
              <p class="about-text">From the first consultation to the final glow, we refine every step with premium products and a calm, luxurious atmosphere.</p>
              <ul class="about-list">
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span><span>Personalized recommendations and styling plans.</span></li>
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M20 6L9 17l-5-5" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span><span>Premium finish with a luminous, natural look.</span></li>
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span><span>Comfort-forward experience designed for ease.</span></li>
              </ul>
            </div>
          </article>

          <article class="tilt-card reveal" data-tilt>
            <div class="card-content">
              <div class="about-pill">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                  <path d="M12 2C8 2 5 5 5 9c0 6 7 13 7 13s7-7 7-13c0-4-3-7-7-7z" stroke="rgba(214,178,94,.95)" stroke-width="1.8" stroke-linejoin="round"/>
                  <path d="M12 12a3 3 0 1 0 0-6 3 3 0 0 0 0 6z" stroke="rgba(24,230,255,.95)" stroke-width="1.8"/>
                </svg>
                <span>Luxury Standard</span>
              </div>
              <h3 class="about-title">Modern care, timeless results</h3>
              <p class="about-text">Our team blends classic techniques with contemporary standards—so your look feels refined, fresh, and confidently you.</p>

              <ul class="about-list">
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M20 6L9 17l-5-5" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span><span>Skin-friendly practices and carefully selected formulas.</span></li>
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span><span>Hair services tailored to your texture and lifestyle.</span></li>
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M20 6L9 17l-5-5" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span><span>Polished finishes for photos, events, and everyday glow.</span></li>
              </ul>
            </div>
          </article>
        </div>
      </div>
    </section>

    <!-- Services -->
    <section id="services" aria-label="Services">
      <div class="container services-wrap">
        <div class="section-head">
          <div>
            <h2 class="gradient-text reveal">Services</h2>
          </div>
          <p class="reveal">Tap a service card to reveal details—designed with glowing hover effects and smooth premium transitions.</p>
        </div>

        <div class="service-grid">
          <!-- Haircut -->
          <article class="service-card reveal" tabindex="0" role="button" aria-expanded="false" data-service>
            <div class="service-top">
              <div class="service-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M4 4l16 16" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round"/>
                  <path d="M7 6l-3 3c2 2 6 1 8-1" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/>
                  <path d="M17 18l3-3c-2-2-6-1-8 1" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/>
                  <path d="M8 20c2 0 3-1 4-2" stroke="rgba(233,240,255,.85)" stroke-width="2.2" stroke-linecap="round"/>
                </svg>
              </div>
              <div style="flex:1;">
                <h3>Haircut</h3>
                <div class="tag"><i aria-hidden="true"></i><span>Precision shaping</span></div>
              </div>
            </div>
            <div class="service-expand" data-expand>
              <div class="service-expand-inner">
                <p>Signature cuts crafted for your face, texture, and daily style—finished with a luminous, salon-grade polish.</p>
                <ul class="bullets">
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Consultation + style plan</li>
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Finish with glow serum</li>
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Styling tips for home</li>
                </ul>
              </div>
            </div>
          </article>

          <!-- Styling -->
          <article class="service-card reveal" tabindex="0" role="button" aria-expanded="false" data-service>
            <div class="service-top">
              <div class="service-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M6 14c0-4 4-8 8-8s4 4 4 8-4 8-8 8-4-4-4-8z" stroke="rgba(24,230,255,.95)" stroke-width="2.2"/>
                  <path d="M13 6l-2 12" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round"/>
                </svg>
              </div>
              <div style="flex:1;">
                <h3>Styling</h3>
                <div class="tag"><i aria-hidden="true"></i><span>Event-ready finish</span></div>
              </div>
            </div>
            <div class="service-expand" data-expand>
              <div class="service-expand-inner">
                <p>From sleek blowouts to soft waves—crafted for movement, shine, and all-day comfort.</p>
                <ul class="bullets">
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Heat protection + shine</li>
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Durable hold, natural feel</li>
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Photo-ready detailing</li>
                </ul>
              </div>
            </div>
          </article>

          <!-- Spa -->
          <article class="service-card reveal" tabindex="0" role="button" aria-expanded="false" data-service>
            <div class="service-top">
              <div class="service-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M12 21s-7-4-7-10c0-3 2-5 5-5 1 0 2 1 2 2 0-1 1-2 2-2 3 0 5 2 5 5 0 6-7 10-7 10z" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linejoin="round"/>
                  <path d="M9.5 11.2c.7 1 1.6 1.6 2.5 1.8 1 .2 1.9-.1 2.6-.9" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round"/>
                </svg>
              </div>
              <div style="flex:1;">
                <h3>Spa</h3>
                <div class="tag"><i aria-hidden="true"></i><span>Restore + reset</span></div>
              </div>
            </div>
            <div class="service-expand" data-expand>
              <div class="service-expand-inner">
                <p>Relaxing rituals designed to revive your senses—so you leave lighter, calmer, and glowing.</p>
                <ul class="bullets">
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Soothing aromatherapy</li>
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Gentle hydration and massage</li>
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Calm, lounge-level finish</li>
                </ul>
              </div>
            </div>
          </article>

          <!-- Facial -->
          <article class="service-card reveal" tabindex="0" role="button" aria-expanded="false" data-service>
            <div class="service-top">
              <div class="service-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M12 22c4 0 8-3 8-8V7l-8-3-8 3v7c0 5 4 8 8 8z" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linejoin="round"/>
                  <path d="M9 12h6" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round"/>
                </svg>
              </div>
              <div style="flex:1;">
                <h3>Facial</h3>
                <div class="tag"><i aria-hidden="true"></i><span>Hydrate + clarify</span></div>
              </div>
            </div>
            <div class="service-expand" data-expand>
              <div class="service-expand-inner">
                <p>Premium facial treatments for a refined glow—targeting hydration, texture, and luminosity.</p>
                <ul class="bullets">
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Gentle cleanse + tone</li>
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Glow infusion mask</li>
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Barrier-friendly finish</li>
                </ul>
              </div>
            </div>
          </article>

          <!-- Makeup -->
          <article class="service-card reveal" tabindex="0" role="button" aria-expanded="false" data-service>
            <div class="service-top">
              <div class="service-icon" aria-hidden="true">
                <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M3 21l3-1 12-12-2-2L4 18l-1 3z" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linejoin="round"/>
                  <path d="M14 4l2-2 6 6-2 2-6-6z" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linejoin="round"/>
                  <path d="M11 7l6 6" stroke="rgba(233,240,255,.85)" stroke-width="2.2" stroke-linecap="round"/>
                </svg>
              </div>
              <div style="flex:1;">
                <h3>Makeup</h3>
                <div class="tag"><i aria-hidden="true"></i><span>Silk finish</span></div>
              </div>
            </div>
            <div class="service-expand" data-expand>
              <div class="service-expand-inner">
                <p>Elegant, long-wear makeup crafted to flatter your features—soft glam with a premium glow.</p>
                <ul class="bullets">
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Complexion matching</li>
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Eyes + lips definition</li>
                  <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Set for comfort + longevity</li>
                </ul>
              </div>
            </div>
          </article>
        </div>
      </div>
    </section>

    <!-- Gallery -->
    <section id="gallery" aria-label="Gallery">
      <div class="container">
        <div class="section-head">
          <div>
            <h2 class="gradient-text reveal">Gallery</h2>
          </div>
          <p class="reveal">Parallax scrolling showcase with a 3D tilt hover and a premium lightbox popup.</p>
        </div>

        <div class="gallery-hero reveal">
          <div class="gallery-strip" id="galleryStrip" aria-label="Gallery images">
            <!-- Inline images as gradients to keep it single-file -->
            <figure class="shot" data-shot data-src="https://images.unsplash.com/photo-1522335789203-aabd1fc54bc9?auto=format&fit=crop&w=1600&q=80" tabindex="0" aria-label="Salon styling gallery image 1" data-caption="Signature styling glow">
              <img alt="Luxury salon styling" loading="lazy" src="https://images.unsplash.com/photo-1522335789203-aabd1fc54bc9?auto=format&fit=crop&w=1200&q=80" />
            </figure>
            <figure class="shot" data-shot data-src="https://images.unsplash.com/photo-1522337660859-02fbefca4702?auto=format&fit=crop&w=1600&q=80" tabindex="0" aria-label="Salon styling gallery image 2" data-caption="Gold-hour hair texture">
              <img alt="Luxury salon hair" loading="lazy" src="https://images.unsplash.com/photo-1522337660859-02fbefca4702?auto=format&fit=crop&w=1200&q=80" />
            </figure>
            <figure class="shot" data-shot data-src="https://images.unsplash.com/photo-1545186552-6b3d3a6fd3b4?auto=format&fit=crop&w=1600&q=80" tabindex="0" aria-label="Salon spa gallery image 3" data-caption="Restorative spa ritual">
              <img alt="Luxury salon spa" loading="lazy" src="https://images.unsplash.com/photo-1545186552-6b3d3a6fd3b4?auto=format&fit=crop&w=1200&q=80" />
            </figure>
            <figure class="shot" data-shot data-src="https://images.unsplash.com/photo-1556228578-0d85b1a7d6f5?auto=format&fit=crop&w=1600&q=80" tabindex="0" aria-label="Salon facial gallery image 4" data-caption="Hydrate + glow facial">
              <img alt="Luxury salon facial" loading="lazy" src="https://images.unsplash.com/photo-1556228578-0d85b1a7d6f5?auto=format&fit=crop&w=1200&q=80" />
            </figure>
            <figure class="shot" data-shot data-src="https://images.unsplash.com/photo-1540206395-68808572332f?auto=format&fit=crop&w=1600&q=80" tabindex="0" aria-label="Makeup gallery image 5" data-caption="Silk glam finish">
              <img alt="Luxury salon makeup" loading="lazy" src="https://images.unsplash.com/photo-1540206395-68808572332f?auto=format&fit=crop&w=1200&q=80" />
            </figure>
            <figure class="shot" data-shot data-src="https://images.unsplash.com/photo-1520975958225-7f61bb3f9b5c?auto=format&fit=crop&w=1600&q=80" tabindex="0" aria-label="Hairstyle gallery image 6" data-caption="Event-ready elegance">
              <img alt="Luxury salon hairstyle" loading="lazy" src="https://images.unsplash.com/photo-1520975958225-7f61bb3f9b5c?auto=format&fit=crop&w=1200&q=80" />
            </figure>
          </div>

          <div class="gallery-note">
            <span class="dot" aria-hidden="true"></span>
            <span><b style="color:var(--gold2)">Tip:</b> Hover (desktop) for 3D tilt. Click to view in lightbox.</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Pricing -->
    <section id="pricing" aria-label="Pricing">
      <div class="container">
        <div class="section-head">
          <div>
            <h2 class="gradient-text reveal">Pricing</h2>
          </div>
          <p class="reveal">Stylish packages with glowing premium borders and a refined, concierge-style experience.</p>
        </div>

        <div class="pricing-grid">
          <article class="price-card reveal" data-reveal-price>
            <div class="price-top">
              <div class="price-tier">
                <div class="tier-name">Essential Glow</div>
              </div>
              <div class="price"><b>$79</b><small>/ session</small></div>
              <p class="price-desc">A signature refresh to elevate your look with premium care.</p>
              <ul class="price-list">
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Consultation + tailored finish</li>
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Glow-focused products</li>
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Style guidance for home</li>
              </ul>
              <div class="price-action">
                <a class="btn-outline" href="#contact" data-scroll>
                  <span>Choose Essential</span>
                  <svg width="18" height="18" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                    <path d="M5 12h14" stroke="rgba(233,240,255,.92)" stroke-width="2.2" stroke-linecap="round"/>
                    <path d="M13 5l7 7-7 7" stroke="rgba(233,240,255,.92)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
                </a>
              </div>
            </div>
          </article>

          <article class="price-card reveal" style="border-color: rgba(214,178,94,.26)" data-featured>
            <div class="price-top">
              <div class="price-tier">
                <div class="tier-name">Signature Luxe</div>
                <div class="badge">Most Popular</div>
              </div>
              <div class="price"><b>$129</b><small>/ session</small></div>
              <p class="price-desc">The complete premium ritual—made for shine, softness, and standout presence.</p>
              <ul class="price-list">
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Enhanced consultation + mood board</li>
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Hair + skin glow pairing</li>
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Concierge-level finish + set</li>
              </ul>
              <div class="price-action">
                <a class="btn-outline" href="#contact" data-scroll>
                  <span>Choose Luxe</span>
                  <svg width="18" height="18" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                    <path d="M5 12h14" stroke="rgba(233,240,255,.92)" stroke-width="2.2" stroke-linecap="round"/>
                    <path d="M13 5l7 7-7 7" stroke="rgba(233,240,255,.92)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
                </a>
              </div>
            </div>
          </article>

          <article class="price-card reveal">
            <div class="price-top">
              <div class="price-tier">
                <div class="tier-name">Afterglow Platinum</div>
              </div>
              <div class="price"><b>$189</b><small>/ session</small></div>
              <p class="price-desc">Premium multi-step experience for unforgettable radiance.</p>
              <ul class="price-list">
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Full luxury consultation + plan</li>
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(214,178,94,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Premium glow ritual (hair/skin)</li>
                <li><span class="check" aria-hidden="true"><svg width="12" height="12" viewBox="0 0 24 24" fill="none"><path d="M20 6L9 17l-5-5" stroke="rgba(24,230,255,.95)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></span>Event-ready styling + touch-up</li>
              </ul>
              <div class="price-action">
                <a class="btn-outline" href="#contact" data-scroll>
                  <span>Choose Platinum</span>
                  <svg width="18" height="18" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                    <path d="M5 12h14" stroke="rgba(233,240,255,.92)" stroke-width="2.2" stroke-linecap="round"/>
                    <path d="M13 5l7 7-7 7" stroke="rgba(233,240,255,.92)" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
                </a>
              </div>
            </div>
          </article>
        </div>
      </div>
    </section>

    <!-- Contact -->
    <section id="contact" aria-label="Contact">
      <div class="container">
        <div class="section-head">
          <div>
            <h2 class="gradient-text reveal">Contact</h2>
          </div>
          <p class="reveal">Send your request—inputs glow with premium focus, and the form provides instant feedback.</p>
        </div>

        <div class="contact-grid">
          <div class="form-card reveal">
            <div class="form-inner">
              <h3 class="form-title">Book an appointment</h3>
              <p class="form-hint">Tell us what you’d love. We’ll confirm your appointment details shortly.</p>

              <form id="contactForm" autocomplete="on">
                <div class="field">
                  <label for="name">Full Name</label>
                  <input id="name" name="name" type="text" placeholder="Your name" required />
                </div>
                <div class="field">
                  <label for="email">Email</label>
                  <input id="email" name="email" type="email" placeholder="you@example.com" required />
                </div>
                <div class="field">
                  <label for="service">Service</label>
                  <input id="service" name="service" type="text" placeholder="Haircut, Spa, Facial, Makeup..." required />
                </div>
                <div class="field">
                  <label for="message">Message</label>
                  <textarea id="message" name="message" placeholder="Preferred date/time and any notes" required></textarea>
                </div>

                <div class="submit">
                  <button class="btn-gradient" type="submit">
                    <span>Submit Request</span>
                    <svg width="18" height="18" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                      <path d="M22 2L11 13" stroke="rgba(6,10,20,.95)" stroke-width="2.2" stroke-linecap="round"/>
                      <path d="M22 2l-7 20-4-9-9-4 20-7z" stroke="rgba(6,10,20,.95)" stroke-width="2.2" stroke-linejoin="round" stroke-linecap="round"/>
                    </svg>
                  </button>
                  <div class="status" id="formStatus" role="status" aria-live="polite">&nbsp;</div>
                </div>
              </form>
            </div>
          </div>

          <div class="map-card reveal" data-map>
            <div class="map-inner">
              <iframe
                title="Google Map"
                loading="lazy"
                referrerpolicy="no-referrer-when-downgrade"
                src="https://www.google.com/maps?q=New%20York%20City&output=embed"
              ></iframe>
            </div>
          </div>
        </div>
      </div>
    </section>

    <footer>
      <div class="footer-inner">
        <div>© <span id="year"></span> NYTRIXX Salon. Luxury Salon Experience.</div>
        <div>Gold + Cyan glow • Responsive • Single-file</div>
      </div>
    </footer>

    <!-- Lightbox -->
    <div class="lightbox" id="lightbox" aria-hidden="true" aria-label="Image preview">
      <div class="lightbox-card">
        <button class="lightbox-close" id="lightboxClose" aria-label="Close preview">✕</button>
        <img id="lightboxImg" alt="Gallery preview" />
      </div>
    </div>
  </div>

  <script>
    /* Smooth scroll with offset for fixed header */
    (function(){
      const header = document.querySelector('.topbar');
      const offset = () => (header ? header.getBoundingClientRect().height + 10 : 80);

      function scrollToId(id){
        const el = document.querySelector(id);
        if(!el) return;
        const top = el.getBoundingClientRect().top + window.scrollY - offset();
        window.scrollTo({ top, behavior: 'smooth' });
      }

      document.addEventListener('click', (e)=>{
        const a = e.target.closest('a[data-scroll]');
        if(!a) return;
        const href = a.getAttribute('href');
        if(href && href.startsWith('#')){
          e.preventDefault();
          scrollToId(href);
        }
      });
    })();

    /* IntersectionObserver reveal */
    (function(){
      const els = Array.from(document.querySelectorAll('.reveal'));
      if(!('IntersectionObserver' in window)){
        els.forEach(el=>el.classList.add('visible'));
        return;
      }
      const io = new IntersectionObserver((entries)=>{
        for(const ent of entries){
          if(ent.isIntersecting){
            ent.target.classList.add('visible');
            io.unobserve(ent.target);
          }
        }
      }, { threshold: 0.12 });

      els.forEach(el=>io.observe(el));
    })();

    /* Hero parallax */
    (function(){
      const heroParallax = document.querySelector('.hero-parallax');
      const heroGlow = document.querySelector('.hero-grid-glow');
      const clamp = (v, a, b) => Math.max(a, Math.min(b, v));

      function onScroll(){
        const y = window.scrollY || 0;
        const p = clamp(y * 0.08, -30, 70);
        document.documentElement.style.setProperty('--pY', p + 'px');
        if(heroParallax) heroParallax.style.transform = `translateY(${p}px)`;
        if(heroGlow) heroGlow.style.transform = `translateY(${p * 0.35}px)`;
      }
      window.addEventListener('scroll', onScroll, { passive: true });
      onScroll();
    })();

    /* Generic tilt for about cards */
    (function(){
      const cards = document.querySelectorAll('[data-tilt]');
      if(!cards.length) return;

      const reduce = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
      if(reduce) return;

      cards.forEach(card => {
        card.addEventListener('mousemove', (e)=>{
          const r = card.getBoundingClientRect();
          const px = (e.clientX - r.left) / r.width;
          const py = (e.clientY - r.top) / r.height;
          const ry = (px - 0.5) * 10; // left/right
          const rx = (0.5 - py) * 10; // up/down
          card.style.transform = `perspective(900px) rotateX(${rx}deg) rotateY(${ry}deg) translateY(-2px)`;
          card.style.setProperty('--mx', (px*100) + '%');
          card.style.setProperty('--my', (py*100) + '%');
        });
        card.addEventListener('mouseleave', ()=>{
          card.style.transform = '';
          card.style.setProperty('--mx', '50%');
          card.style.setProperty('--my', '10%');
        });
      });
    })();

    /* Services: glowing hover + smooth expand */
    (function(){
      const cards = Array.from(document.querySelectorAll('[data-service]'));
      if(!cards.length) return;

      const reduce = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;

      cards.forEach(card => {
        const expand = card.querySelector('[data-expand]');
        if(!expand) return;

        const setVarsFromEvent = (e) => {
          const r = card.getBoundingClientRect();
          const sx = ((e.clientX - r.left) / r.width) * 100;
          const sy = ((e.clientY - r.top) / r.height) * 100;
          card.style.setProperty('--sx', sx + '%');
          card.style.setProperty('--sy', sy + '%');
        };

        card.addEventListener('mousemove', (e)=>{ if(!reduce) setVarsFromEvent(e); });

        const collapsed = () => expand.getAttribute('data-open') !== '1';

        const open = () => {
          card.classList.add('service-expanded');
          card.setAttribute('aria-expanded', 'true');
          const inner = expand.querySelector('.service-expand-inner');
          const h = inner ? inner.scrollHeight : 160;
          expand.style.height = h + 'px';
          expand.setAttribute('data-open','1');
        };

        const close = () => {
          card.classList.remove('service-expanded');
          card.setAttribute('aria-expanded', 'false');
          expand.style.height = '0px';
          expand.setAttribute('data-open','0');
        };

        // init
        close();

        const toggle = ()=>{
          if(collapsed()) open(); else close();
        };

        card.addEventListener('click', ()=> toggle());
        card.addEventListener('keydown', (e)=>{
          if(e.key === 'Enter' || e.key === ' '){
            e.preventDefault();
            toggle();
          }
        });
      });
    })();

    /* Gallery tilt + lightbox + parallax scrolling */
    (function(){
      const shots = Array.from(document.querySelectorAll('[data-shot]'));
      const strip = document.getElementById('galleryStrip');
      const lightbox = document.getElementById('lightbox');
      const lightboxImg = document.getElementById('lightboxImg');
      const closeBtn = document.getElementById('lightboxClose');

      if(!shots.length) return;

      const reduce = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;

      function openShot(src){
        lightboxImg.src = src;
        lightbox.classList.add('open');
        lightbox.setAttribute('aria-hidden','false');
        document.body.style.overflow = 'hidden';
      }
      function closeShot(){
        lightbox.classList.remove('open');
        lightbox.setAttribute('aria-hidden','true');
        document.body.style.overflow = '';
      }

      shots.forEach(shot => {
        shot.addEventListener('click', ()=>{
          const src = shot.getAttribute('data-src') || shot.querySelector('img')?.src;
          if(src) openShot(src);
        });
        shot.addEventListener('keydown', (e)=>{
          if(e.key === 'Enter' || e.key === ' '){
            e.preventDefault();
            const src = shot.getAttribute('data-src') || shot.querySelector('img')?.src;
            if(src) openShot(src);
          }
        });

        if(reduce) return;

        shot.addEventListener('mousemove', (e)=>{
          const r = shot.getBoundingClientRect();
          const px = (e.clientX - r.left) / r.width;
          const py = (e.clientY - r.top) / r.height;
          const rx = (0.5 - py) * 10;
          const ry = (px - 0.5) * 12;
          shot.style.setProperty('--rx', rx + 'deg');
          shot.style.setProperty('--ry', ry + 'deg');
          shot.style.setProperty('--mx', (px*100) + '%');
          shot.style.setProperty('--my', (py*100) + '%');
        });
        shot.addEventListener('mouseleave', ()=>{
          shot.style.setProperty('--rx', '0deg');
          shot.style.setProperty('--ry', '0deg');
          shot.style.setProperty('--mx', '50%');
          shot.style.setProperty('--my', '10%');
        });
      });

      closeBtn.addEventListener('click', closeShot);
      lightbox.addEventListener('click', (e)=>{ if(e.target === lightbox) closeShot(); });
      document.addEventListener('keydown', (e)=>{ if(e.key === 'Escape') closeShot(); });

      // Parallax effect on strip items
      function onScroll(){
        if(!strip) return;
        const rect = strip.getBoundingClientRect();
        const vh = window.innerHeight || 1;
        const progress = (vh - rect.top) / (vh + rect.height);
        const p = Math.max(-0.5, Math.min(0.5, progress));
        // subtle transform to give parallax feel
        strip.style.transform = `translateY(${p * 12}px)`;
      }
      window.addEventListener('scroll', onScroll, { passive: true });
      onScroll();
    })();

    /* Contact form (demo submit) */
    (function(){
      const form = document.getElementById('contactForm');
      const status = document.getElementById('formStatus');
      if(!form || !status) return;

      form.addEventListener('submit', (e)=>{
        e.preventDefault();

        const fd = new FormData(form);
        const name = String(fd.get('name') || '').trim();
        const email = String(fd.get('email') || '').trim();
        const service = String(fd.get('service') || '').trim();

        status.textContent = `Submitting...`; 

        // Simulate premium async submission
        setTimeout(()=>{
          status.innerHTML = `Thank you, <b>${escapeHtml(name || 'Guest')}</b>. We\'ll contact <b>${escapeHtml(email || 'your email')}</b> about <b>${escapeHtml(service || 'your service')}</b> soon.`;
          form.reset();
          setTimeout(()=>{ status.textContent = '\u00A0'; }, 5500);
        }, 650);
      });

      function escapeHtml(s){
        return s.replace(/[&<>"']/g, (c)=>({ '&':'&amp;','<':'<','>':'>','"':'"',"'":'&#39;' }[c]));
      }
    })();

    /* Footer year */
    document.getElementById('year').textContent = new Date().getFullYear();

    /* Three.js particle background (single-file loader) */
    (function(){
      const canvas = document.getElementById('particles');
      if(!canvas) return;
      const prefersReduced = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
      if(prefersReduced) return;

      const script = document.createElement('script');
      script.src = 'https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.min.js';
      script.async = true;
      document.head.appendChild(script);

      script.onload = () => {
        const THREE = window.THREE;
        if(!THREE) return;

        const renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true });
        renderer.setPixelRatio(Math.min(window.devicePixelRatio || 1, 2));

        const scene = new THREE.Scene();

        const camera = new THREE.PerspectiveCamera(60, 1, 0.1, 1000);
        camera.position.set(0, 0, 120);

        const gold = new THREE.Color('#d6b25e');
        const cyan = new THREE.Color('#18e6ff');

        const starCount = Math.floor(Math.min(240, Math.max(120, (window.innerWidth * window.innerHeight) / 9000)));
        const geometry = new THREE.BufferGeometry();
        const positions = new Float32Array(starCount * 3);
        const colors = new Float32Array(starCount * 3);
        const sizes = new Float32Array(starCount);

        const colorMix = () => (Math.random() > 0.55 ? cyan : gold);

        for(let i=0;i<starCount;i++){
          const i3 = i*3;
          // Spread in a sphere-ish volume
          const radius = 65 * Math.cbrt(Math.random());
          const theta = Math.random() * Math.PI * 2;
          const phi = Math.acos(2*Math.random()-1);

          const x = radius * Math.sin(phi) * Math.cos(theta);
          const y = radius * Math.sin(phi) * Math.sin(theta);
          const z = radius * Math.cos(phi);

          positions[i3] = x;
          positions[i3+1] = y;
          positions[i3+2] = z;

          const c = colorMix();
          colors[i3] = c.r;
          colors[i3+1] = c.g;
          colors[i3+2] = c.b;

          sizes[i] = 0.8 + Math.random() * 1.9;
        }

        geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
        geometry.setAttribute('color', new THREE.BufferAttribute(colors, 3));
        geometry.setAttribute('size', new THREE.BufferAttribute(sizes, 1));

        const material = new THREE.PointsMaterial({
          size: 2.2,
          vertexColors: true,
          transparent: true,
          opacity: 0.9,
          depthWrite: false
        });

        const points = new THREE.Points(geometry, material);
        scene.add(points);

        function resize(){
          const w = window.innerWidth;
          const h = window.innerHeight;
          renderer.setSize(w, h, false);
          camera.aspect = w / h;
          camera.updateProjectionMatrix();
        }
        window.addEventListener('resize', resize);
        resize();

        let t = 0;
        function animate(){
          t += 0.004;
          points.rotation.y = t * 0.8;
          points.rotation.x = t * 0.35;

          // gentle wave on vertices
          const pos = geometry.attributes.position;
          for(let i=0;i<starCount;i++){
            const idx = i*3;
            const x = pos.array[idx];
            const y = pos.array[idx+1];
            const z = pos.array[idx+2];
            pos.array[idx] = x + Math.sin(t*2 + z*0.02) * 0.02;
            pos.array[idx+1] = y + Math.cos(t*2 + x*0.02) * 0.02;
            // z unchanged for performance
          }
          pos.needsUpdate = true;

          renderer.render(scene, camera);
          requestAnimationFrame(animate);
        }
        animate();
      };
    })();
  </script>
</body>
</html>

