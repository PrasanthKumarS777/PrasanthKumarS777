<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Prasanth Kumar Sahu — Data Analyst Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet"/>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<style>
:root {
  --ink: #05060a;
  --surface: #080b14;
  --card: #0d1220;
  --border: rgba(14,165,233,0.15);
  --cyan: #0ea5e9;
  --violet: #7c3aed;
  --pink: #ec4899;
  --emerald: #10b981;
  --amber: #f59e0b;
  --text: #e2e8f0;
  --muted: #64748b;
  --glow-cyan: 0 0 40px rgba(14,165,233,0.4);
  --glow-violet: 0 0 40px rgba(124,58,237,0.4);
}

*{margin:0;padding:0;box-sizing:border-box;}

html{scroll-behavior:smooth;}

body{
  background:var(--ink);
  color:var(--text);
  font-family:'DM Mono', monospace;
  overflow-x:hidden;
  cursor:none;
}

/* CUSTOM CURSOR */
#cursor{
  position:fixed;width:12px;height:12px;
  background:var(--cyan);border-radius:50%;
  pointer-events:none;z-index:9999;
  transform:translate(-50%,-50%);
  transition:width .2s,height .2s,background .2s;
  mix-blend-mode:screen;
}
#cursor-trail{
  position:fixed;width:36px;height:36px;
  border:1px solid rgba(14,165,233,0.4);border-radius:50%;
  pointer-events:none;z-index:9998;
  transform:translate(-50%,-50%);
  transition:all .12s ease;
}

/* PARTICLES BG */
#particles-canvas{
  position:fixed;top:0;left:0;width:100%;height:100%;
  pointer-events:none;z-index:0;opacity:.6;
}

/* GRID OVERLAY */
body::before{
  content:'';position:fixed;top:0;left:0;width:100%;height:100%;
  background-image:
    linear-gradient(rgba(14,165,233,.04) 1px,transparent 1px),
    linear-gradient(90deg,rgba(14,165,233,.04) 1px,transparent 1px);
  background-size:60px 60px;
  pointer-events:none;z-index:0;
}

/* SCANLINE */
body::after{
  content:'';position:fixed;top:0;left:0;width:100%;height:100%;
  background:repeating-linear-gradient(
    0deg,transparent,transparent 2px,
    rgba(0,0,0,.03) 2px,rgba(0,0,0,.03) 4px
  );
  pointer-events:none;z-index:1;
}

section,.wrap{position:relative;z-index:2;}

/* ─── HERO ─────────────────────────────────────── */
#hero{
  min-height:100vh;display:flex;align-items:center;
  justify-content:center;position:relative;overflow:hidden;
}

#threejs-canvas{
  position:absolute;top:0;right:0;
  width:55%;height:100%;
  opacity:.85;
}

.hero-content{
  position:relative;z-index:5;
  padding:0 6vw;max-width:680px;
}

.hero-eyebrow{
  font-family:'Space Mono',monospace;
  font-size:.72rem;letter-spacing:.25em;
  color:var(--cyan);text-transform:uppercase;
  margin-bottom:1.4rem;
  display:flex;align-items:center;gap:.8rem;
}
.hero-eyebrow::before{
  content:'';display:block;width:32px;height:1px;background:var(--cyan);
}

.hero-name{
  font-family:'Syne',sans-serif;
  font-size:clamp(2.8rem,6vw,5.2rem);
  font-weight:800;line-height:1.05;
  letter-spacing:-.02em;
  background:linear-gradient(135deg,#fff 30%,var(--cyan) 60%,var(--violet) 100%);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
  background-clip:text;
}

.hero-role{
  font-family:'Space Mono',monospace;
  font-size:1.05rem;color:var(--muted);
  margin:.8rem 0 1.8rem;
  border-left:2px solid var(--cyan);
  padding-left:1rem;
}

/* TYPEWRITER */
#typewriter{
  font-family:'DM Mono',monospace;
  font-size:.88rem;color:var(--cyan);
  min-height:1.4rem;
}
#typewriter::after{
  content:'|';animation:blink .7s infinite;
}
@keyframes blink{0%,100%{opacity:1;}50%{opacity:0;}}

.hero-stats{
  display:flex;gap:2.5rem;margin:2.2rem 0;
}
.stat{
  display:flex;flex-direction:column;gap:.3rem;
}
.stat-num{
  font-family:'Syne',sans-serif;font-size:2.2rem;font-weight:800;
  color:var(--cyan);line-height:1;
}
.stat-label{font-size:.65rem;letter-spacing:.12em;color:var(--muted);text-transform:uppercase;}

.hero-cta{
  display:flex;gap:1rem;margin-top:2rem;flex-wrap:wrap;
}
.btn{
  font-family:'Space Mono',monospace;font-size:.75rem;
  padding:.75rem 1.8rem;border-radius:3px;
  letter-spacing:.08em;text-decoration:none;
  transition:all .25s;cursor:none;
  text-transform:uppercase;
}
.btn-primary{
  background:var(--cyan);color:var(--ink);
  box-shadow:0 0 24px rgba(14,165,233,.4);
}
.btn-primary:hover{
  background:#fff;box-shadow:0 0 40px rgba(14,165,233,.7);
  transform:translateY(-2px);
}
.btn-ghost{
  background:transparent;color:var(--cyan);
  border:1px solid rgba(14,165,233,.5);
}
.btn-ghost:hover{
  border-color:var(--cyan);background:rgba(14,165,233,.08);
  transform:translateY(-2px);
}

/* STATUS BADGE */
.status-badge{
  display:inline-flex;align-items:center;gap:.5rem;
  background:rgba(16,185,129,.1);border:1px solid rgba(16,185,129,.3);
  border-radius:2px;padding:.35rem .9rem;
  font-family:'Space Mono',monospace;font-size:.68rem;
  color:var(--emerald);letter-spacing:.1em;
  text-transform:uppercase;margin-bottom:1.2rem;
}
.status-dot{
  width:6px;height:6px;border-radius:50%;
  background:var(--emerald);
  animation:pulse-dot 2s infinite;
}
@keyframes pulse-dot{
  0%,100%{box-shadow:0 0 0 0 rgba(16,185,129,.5);}
  50%{box-shadow:0 0 0 6px rgba(16,185,129,0);}
}

/* SCROLL INDICATOR */
.scroll-hint{
  position:absolute;bottom:2.5rem;left:50%;transform:translateX(-50%);
  display:flex;flex-direction:column;align-items:center;gap:.5rem;
  font-family:'Space Mono',monospace;font-size:.62rem;
  color:var(--muted);letter-spacing:.15em;text-transform:uppercase;
  animation:float 3s ease-in-out infinite;
}
.scroll-line{
  width:1px;height:48px;
  background:linear-gradient(var(--cyan),transparent);
  animation:scroll-drop 2s ease-in-out infinite;
}
@keyframes float{0%,100%{transform:translateX(-50%) translateY(0);}50%{transform:translateX(-50%) translateY(-6px);}}
@keyframes scroll-drop{0%{transform:scaleY(0);transform-origin:top;}50%{transform:scaleY(1);transform-origin:top;}50.01%{transform-origin:bottom;}100%{transform:scaleY(0);transform-origin:bottom;}}

/* ─── QUOTE TICKER ───────────────────────────── */
.quote-ticker{
  background:rgba(14,165,233,.06);
  border-top:1px solid var(--border);
  border-bottom:1px solid var(--border);
  padding:.75rem 0;overflow:hidden;
  position:relative;z-index:2;
}
.ticker-track{
  display:flex;gap:4rem;
  animation:ticker 35s linear infinite;
  white-space:nowrap;
}
.ticker-track:hover{animation-play-state:paused;}
@keyframes ticker{from{transform:translateX(0);}to{transform:translateX(-50%)}}
.ticker-item{
  font-family:'Space Mono',monospace;font-size:.72rem;
  color:var(--muted);letter-spacing:.05em;
  display:flex;align-items:center;gap:.8rem;
  flex-shrink:0;
}
.ticker-item span{color:var(--cyan);}

/* ─── SECTION COMMONS ───────────────────────── */
.section{padding:7rem 6vw;}
.section-label{
  font-family:'Space Mono',monospace;font-size:.68rem;
  color:var(--cyan);letter-spacing:.25em;text-transform:uppercase;
  margin-bottom:.8rem;display:flex;align-items:center;gap:.8rem;
}
.section-label::before{content:'';width:24px;height:1px;background:var(--cyan);}
.section-title{
  font-family:'Syne',sans-serif;font-size:clamp(2rem,4vw,3.2rem);
  font-weight:800;line-height:1.1;
  margin-bottom:3.5rem;letter-spacing:-.02em;
}

/* ─── DATA QUOTES ────────────────────────────── */
#quotes{background:var(--surface);}
.quotes-grid{
  display:grid;grid-template-columns:repeat(auto-fit,minmax(320px,1fr));
  gap:1.5px;
  border:1px solid var(--border);
}
.quote-card{
  background:var(--card);padding:2.5rem 2rem;
  border:1px solid transparent;
  transition:all .3s;position:relative;overflow:hidden;
}
.quote-card::before{
  content:'';position:absolute;top:0;left:0;
  width:100%;height:2px;
  background:linear-gradient(90deg,var(--cyan),var(--violet));
  transform:scaleX(0);transform-origin:left;
  transition:transform .4s;
}
.quote-card:hover::before{transform:scaleX(1);}
.quote-card:hover{
  background:rgba(14,165,233,.05);
  border-color:var(--border);
}
.quote-mark{
  font-family:'Syne',sans-serif;font-size:5rem;font-weight:800;
  color:rgba(14,165,233,.12);line-height:.8;margin-bottom:.5rem;
}
.quote-text{
  font-family:'Syne',sans-serif;font-size:1.05rem;
  font-weight:600;line-height:1.55;color:var(--text);
  margin-bottom:1rem;
}
.quote-author{
  font-family:'Space Mono',monospace;font-size:.68rem;
  color:var(--cyan);letter-spacing:.12em;
  text-transform:uppercase;
}

/* FEATURED QUOTE */
.quote-featured{
  background:linear-gradient(135deg,rgba(124,58,237,.12),rgba(14,165,233,.08));
  border:1px solid rgba(124,58,237,.3);
  padding:3.5rem;text-align:center;margin-top:2rem;
  border-radius:2px;position:relative;overflow:hidden;
}
.quote-featured::after{
  content:'';position:absolute;
  width:200px;height:200px;border-radius:50%;
  background:radial-gradient(rgba(124,58,237,.2),transparent);
  top:-60px;right:-60px;
}
.quote-featured .quote-text{font-size:1.4rem;color:#fff;}
.quote-featured .quote-author{color:var(--violet);}

/* ─── SKILLS ─────────────────────────────────── */
#skills{background:var(--ink);}
.skills-layout{display:grid;grid-template-columns:1fr 1fr;gap:4rem;align-items:start;}

/* RADAR CHART */
#radar-wrap{
  position:relative;
}
#radar-canvas{
  width:100%;max-width:420px;
  filter:drop-shadow(0 0 30px rgba(14,165,233,.3));
}
.radar-legend{
  display:flex;flex-wrap:wrap;gap:.6rem;margin-top:1.5rem;
}
.legend-item{
  font-family:'Space Mono',monospace;font-size:.62rem;
  color:var(--muted);letter-spacing:.08em;
  display:flex;align-items:center;gap:.4rem;
}
.legend-dot{width:6px;height:6px;border-radius:50%;}

/* SKILL BARS */
.skill-bars{display:flex;flex-direction:column;gap:1.2rem;}
.skill-row{display:flex;flex-direction:column;gap:.4rem;}
.skill-meta{
  display:flex;justify-content:space-between;
  font-family:'Space Mono',monospace;font-size:.68rem;
  color:var(--muted);
}
.skill-name{color:var(--text);}
.skill-pct{color:var(--cyan);}
.skill-track{
  height:4px;background:rgba(255,255,255,.06);
  border-radius:2px;overflow:hidden;
}
.skill-fill{
  height:100%;border-radius:2px;width:0;
  transition:width 1.4s cubic-bezier(.23,1,.32,1);
}

/* BADGE GRID */
.badge-section{margin-top:3rem;}
.badge-category{margin-bottom:1.8rem;}
.badge-cat-label{
  font-family:'Space Mono',monospace;font-size:.65rem;
  color:var(--muted);letter-spacing:.18em;text-transform:uppercase;
  margin-bottom:.8rem;
  padding-bottom:.4rem;border-bottom:1px solid var(--border);
}
.badge-row{display:flex;flex-wrap:wrap;gap:.5rem;}
.badge{
  font-family:'DM Mono',monospace;font-size:.65rem;
  padding:.3rem .75rem;border-radius:2px;
  border:1px solid;letter-spacing:.04em;
  transition:all .2s;cursor:none;
}
.badge:hover{transform:translateY(-2px);}
.badge-cyan{color:var(--cyan);border-color:rgba(14,165,233,.3);background:rgba(14,165,233,.06);}
.badge-cyan:hover{background:rgba(14,165,233,.15);box-shadow:var(--glow-cyan);}
.badge-violet{color:#a78bfa;border-color:rgba(124,58,237,.3);background:rgba(124,58,237,.06);}
.badge-violet:hover{background:rgba(124,58,237,.15);}
.badge-pink{color:var(--pink);border-color:rgba(236,72,153,.3);background:rgba(236,72,153,.06);}
.badge-emerald{color:var(--emerald);border-color:rgba(16,185,129,.3);background:rgba(16,185,129,.06);}
.badge-amber{color:var(--amber);border-color:rgba(245,158,11,.3);background:rgba(245,158,11,.06);}

/* ─── PROJECTS ───────────────────────────────── */
#projects{background:var(--surface);}
.projects-grid{
  display:grid;grid-template-columns:repeat(auto-fit,minmax(340px,1fr));
  gap:1.5px;border:1px solid var(--border);
}
.project-card{
  background:var(--card);padding:2.2rem;
  transition:all .3s;position:relative;
  overflow:hidden;
}
.project-card::after{
  content:'';position:absolute;
  bottom:-60px;right:-60px;
  width:140px;height:140px;border-radius:50%;
  opacity:0;transition:opacity .4s;
}
.project-card:nth-child(1)::after{background:radial-gradient(rgba(14,165,233,.15),transparent);}
.project-card:nth-child(2)::after{background:radial-gradient(rgba(124,58,237,.15),transparent);}
.project-card:nth-child(3)::after{background:radial-gradient(rgba(236,72,153,.15),transparent);}
.project-card:nth-child(4)::after{background:radial-gradient(rgba(16,185,129,.15),transparent);}
.project-card:nth-child(5)::after{background:radial-gradient(rgba(245,158,11,.15),transparent);}
.project-card:nth-child(6)::after{background:radial-gradient(rgba(14,165,233,.15),transparent);}
.project-card:hover::after{opacity:1;bottom:-20px;right:-20px;}
.project-card:hover{background:rgba(14,165,233,.04);}

.project-num{
  font-family:'Space Mono',monospace;font-size:.65rem;
  color:var(--muted);letter-spacing:.12em;
  margin-bottom:1rem;
}
.project-title{
  font-family:'Syne',sans-serif;font-size:1.15rem;font-weight:700;
  color:#fff;margin-bottom:.6rem;line-height:1.3;
}
.project-desc{
  font-family:'DM Mono',monospace;font-size:.72rem;
  color:var(--muted);line-height:1.7;margin-bottom:1.2rem;
}
.project-metrics{
  display:flex;gap:1rem;flex-wrap:wrap;margin-bottom:1.2rem;
}
.metric-pill{
  font-family:'Space Mono',monospace;font-size:.6rem;
  padding:.25rem .7rem;border-radius:1px;
  background:rgba(14,165,233,.1);color:var(--cyan);
  border:1px solid rgba(14,165,233,.25);letter-spacing:.06em;
}
.project-link{
  font-family:'Space Mono',monospace;font-size:.65rem;
  color:var(--cyan);text-decoration:none;
  letter-spacing:.1em;text-transform:uppercase;
  display:inline-flex;align-items:center;gap:.5rem;
  transition:gap .2s;
}
.project-link:hover{gap:.9rem;}

/* ─── CERTS ──────────────────────────────────── */
#certs{background:var(--ink);}
.cert-grid{
  display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));
  gap:1px;border:1px solid var(--border);
}
.cert-card{
  background:var(--card);padding:1.5rem 1.8rem;
  display:flex;align-items:flex-start;gap:1rem;
  transition:background .3s;
  position:relative;overflow:hidden;
}
.cert-card::before{
  content:'';position:absolute;left:0;top:0;
  width:2px;height:100%;
  background:linear-gradient(var(--cyan),var(--violet));
  transform:scaleY(0);transition:transform .3s;transform-origin:top;
}
.cert-card:hover::before{transform:scaleY(1);}
.cert-card:hover{background:rgba(14,165,233,.04);}
.cert-num{
  font-family:'Space Mono',monospace;font-size:.65rem;
  color:var(--muted);min-width:28px;padding-top:.05rem;
}
.cert-info{flex:1;}
.cert-name{
  font-family:'Syne',sans-serif;font-size:.88rem;font-weight:600;
  color:var(--text);line-height:1.35;margin-bottom:.35rem;
}
.cert-meta{
  display:flex;gap:.75rem;flex-wrap:wrap;
  font-family:'DM Mono',monospace;font-size:.62rem;
  color:var(--muted);
}
.cert-platform{color:var(--cyan);}
.cert-link{
  font-family:'Space Mono',monospace;font-size:.6rem;
  color:var(--violet);text-decoration:none;
  padding:.2rem .5rem;border:1px solid rgba(124,58,237,.3);
  border-radius:2px;white-space:nowrap;
  transition:all .2s;
}
.cert-link:hover{background:rgba(124,58,237,.15);color:#a78bfa;}

.certs-section-title{
  font-family:'Space Mono',monospace;font-size:.68rem;
  color:var(--muted);letter-spacing:.18em;text-transform:uppercase;
  padding:1.2rem 1.8rem;
  background:rgba(14,165,233,.04);
  border-bottom:1px solid var(--border);
  grid-column:1/-1;
}

/* FORAGE CARDS */
.forage-grid{
  display:grid;grid-template-columns:1fr 1fr;
  gap:1.5rem;margin-top:2rem;
}
.forage-card{
  background:var(--card);border:1px solid var(--border);
  padding:2rem;border-radius:2px;
  transition:all .3s;position:relative;overflow:hidden;
}
.forage-card:hover{border-color:rgba(245,158,11,.4);box-shadow:0 0 30px rgba(245,158,11,.1);}
.forage-logo{
  font-family:'Syne',sans-serif;font-size:.75rem;font-weight:700;
  letter-spacing:.1em;text-transform:uppercase;
  color:var(--amber);margin-bottom:.6rem;
}
.forage-title{
  font-family:'Syne',sans-serif;font-size:1.05rem;font-weight:700;
  color:#fff;margin-bottom:.8rem;
}
.forage-tasks{
  list-style:none;
  font-family:'DM Mono',monospace;font-size:.7rem;
  color:var(--muted);line-height:1.9;
}
.forage-tasks li::before{content:'→ ';color:var(--amber);}

/* ─── STATS BAR ──────────────────────────────── */
#stats-bar{
  background:var(--surface);
  border-top:1px solid var(--border);
  border-bottom:1px solid var(--border);
  padding:3.5rem 6vw;
}
.stats-row{
  display:grid;grid-template-columns:repeat(4,1fr);
  gap:2rem;
}
.stat-block{
  text-align:center;
  padding:2rem 1rem;
  border:1px solid var(--border);
  background:var(--card);
  transition:all .3s;
  position:relative;overflow:hidden;
}
.stat-block::after{
  content:'';position:absolute;
  bottom:0;left:0;width:100%;height:2px;
  background:linear-gradient(90deg,var(--cyan),var(--violet));
  transform:scaleX(0);transition:transform .4s;
}
.stat-block:hover::after{transform:scaleX(1);}
.stat-block:hover{background:rgba(14,165,233,.04);}
.stat-block-num{
  font-family:'Syne',sans-serif;font-size:3rem;font-weight:800;
  background:linear-gradient(135deg,var(--cyan),var(--violet));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
  background-clip:text;line-height:1;margin-bottom:.4rem;
  display:block;
}
.stat-block-label{
  font-family:'Space Mono',monospace;font-size:.65rem;
  color:var(--muted);letter-spacing:.15em;text-transform:uppercase;
}

/* ─── EXPERIENCE ─────────────────────────────── */
#experience{background:var(--ink);}
.exp-grid{display:grid;grid-template-columns:1fr 1fr;gap:1.5px;border:1px solid var(--border);}
.exp-card{
  background:var(--card);padding:2.8rem;
  transition:background .3s;
}
.exp-card:hover{background:rgba(14,165,233,.04);}
.exp-header{
  display:flex;justify-content:space-between;align-items:flex-start;
  margin-bottom:1.5rem;
}
.exp-company{
  font-family:'Syne',sans-serif;font-size:1.3rem;font-weight:800;
  color:#fff;margin-bottom:.3rem;
}
.exp-role{
  font-family:'DM Mono',monospace;font-size:.78rem;color:var(--cyan);
}
.exp-badge{
  font-family:'Space Mono',monospace;font-size:.6rem;
  padding:.3rem .8rem;border:1px solid rgba(16,185,129,.3);
  color:var(--emerald);background:rgba(16,185,129,.08);
  border-radius:1px;letter-spacing:.1em;text-transform:uppercase;
  display:flex;align-items:center;gap:.4rem;
}
.exp-list{
  list-style:none;
  font-family:'DM Mono',monospace;font-size:.72rem;
  color:var(--muted);line-height:2;
}
.exp-list li::before{content:'▸ ';color:var(--cyan);}
.exp-tags{display:flex;flex-wrap:wrap;gap:.4rem;margin-top:1.4rem;}

/* ─── CONTACT ────────────────────────────────── */
#contact{
  background:var(--surface);
  text-align:center;padding:8rem 6vw;
  position:relative;overflow:hidden;
}
#contact::before{
  content:'';position:absolute;
  width:600px;height:600px;border-radius:50%;
  background:radial-gradient(rgba(124,58,237,.08),transparent 70%);
  top:50%;left:50%;transform:translate(-50%,-50%);
  pointer-events:none;
}
.contact-tagline{
  font-family:'Syne',sans-serif;
  font-size:clamp(1.8rem,4vw,3rem);
  font-weight:800;line-height:1.2;
  margin-bottom:1rem;
  background:linear-gradient(135deg,#fff,var(--cyan));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
  background-clip:text;
}
.contact-sub{
  font-family:'DM Mono',monospace;font-size:.85rem;
  color:var(--muted);margin-bottom:3rem;max-width:500px;margin-inline:auto;
}
.contact-links{
  display:flex;justify-content:center;gap:1rem;flex-wrap:wrap;
}
.contact-link{
  font-family:'Space Mono',monospace;font-size:.72rem;
  padding:.85rem 2rem;text-decoration:none;
  border:1px solid var(--border);color:var(--text);
  background:var(--card);transition:all .3s;
  letter-spacing:.1em;text-transform:uppercase;
  display:flex;align-items:center;gap:.6rem;
}
.contact-link:hover{border-color:var(--cyan);color:var(--cyan);
  box-shadow:var(--glow-cyan);transform:translateY(-3px);}
.contact-link.primary{
  background:var(--cyan);color:var(--ink);border-color:var(--cyan);
}
.contact-link.primary:hover{background:#fff;color:var(--ink);}

/* FOOTER */
footer{
  background:var(--ink);
  border-top:1px solid var(--border);
  padding:1.8rem 6vw;
  display:flex;justify-content:space-between;align-items:center;
  flex-wrap:wrap;gap:1rem;
  font-family:'Space Mono',monospace;font-size:.62rem;
  color:var(--muted);letter-spacing:.08em;
}
footer span{color:var(--cyan);}

/* ANIMATIONS */
.fade-up{
  opacity:0;transform:translateY(28px);
  transition:opacity .8s,transform .8s;
}
.fade-up.visible{opacity:1;transform:translateY(0);}

/* 3D CHART CONTAINER */
#chart3d-section{
  background:var(--surface);
  padding:7rem 6vw;
}
.chart3d-grid{
  display:grid;grid-template-columns:1fr 1fr;
  gap:3rem;align-items:center;
}
#bar3d-canvas{
  width:100%;height:400px;
  border:1px solid var(--border);
  background:var(--card);
  border-radius:2px;
}
.chart-info{padding:1rem 0;}
.chart-title{
  font-family:'Syne',sans-serif;font-size:1.6rem;font-weight:800;
  color:#fff;margin-bottom:1rem;
}
.chart-desc{
  font-family:'DM Mono',monospace;font-size:.78rem;
  color:var(--muted);line-height:1.9;margin-bottom:2rem;
}

/* RESPONSIVE */
@media(max-width:900px){
  #threejs-canvas{width:100%;height:50vh;top:auto;bottom:0;opacity:.3;}
  .skills-layout,.chart3d-grid,.exp-grid,.forage-grid{grid-template-columns:1fr;}
  .stats-row{grid-template-columns:1fr 1fr;}
  .hero-stats{gap:1.5rem;}
}
@media(max-width:600px){
  .stats-row{grid-template-columns:1fr 1fr;}
  .projects-grid{grid-template-columns:1fr;}
  .cert-grid{grid-template-columns:1fr;}
}
</style>
</head>
<body>

<div id="cursor"></div>
<div id="cursor-trail"></div>
<canvas id="particles-canvas"></canvas>

<!-- ══════════════════ HERO ══════════════════ -->
<section id="hero">
  <canvas id="threejs-canvas"></canvas>

  <div class="hero-content fade-up">
    <div class="status-badge">
      <span class="status-dot"></span>
      Available for full-time roles
    </div>

    <div class="hero-eyebrow">Data Analyst · MBA Finance & IT · LPU</div>

    <h1 class="hero-name">Prasanth<br/>Kumar Sahu</h1>

    <p class="hero-role">
      Turning noise into signal.<br/>
      Business brain × Data science toolkit.
    </p>

    <div id="typewriter"></div>

    <div class="hero-stats">
      <div class="stat">
        <span class="stat-num" data-count="21">0</span>
        <span class="stat-label">Certificates</span>
      </div>
      <div class="stat">
        <span class="stat-num" data-count="6">0</span>
        <span class="stat-label">Projects</span>
      </div>
      <div class="stat">
        <span class="stat-num" data-count="2">0</span>
        <span class="stat-label">Internships</span>
      </div>
      <div class="stat">
        <span class="stat-num" data-count="80">0</span>
        <span class="stat-label">Cert Hours+</span>
      </div>
    </div>

    <div class="hero-cta">
      <a href="#projects" class="btn btn-primary">View Projects</a>
      <a href="#contact" class="btn btn-ghost">Hire Me</a>
    </div>
  </div>

  <div class="scroll-hint">
    <div class="scroll-line"></div>
    Scroll
  </div>
</section>

<!-- ══════════════════ TICKER ══════════════════ -->
<div class="quote-ticker">
  <div class="ticker-track" id="ticker">
    <span class="ticker-item"><span>◆</span> "Data is the new oil — but insights are the refinery."</span>
    <span class="ticker-item"><span>◆</span> "In God we trust. All others must bring data." — W. Edwards Deming</span>
    <span class="ticker-item"><span>◆</span> "Without data, you're just another person with an opinion." — W. Edwards Deming</span>
    <span class="ticker-item"><span>◆</span> "The goal is to turn data into information, and information into insight." — Carly Fiorina</span>
    <span class="ticker-item"><span>◆</span> "Torture the data long enough and it will confess to anything." — Ronald Coase</span>
    <span class="ticker-item"><span>◆</span> "Data science is the sexiest job of the 21st century." — Harvard Business Review</span>
    <span class="ticker-item"><span>◆</span> "Every spreadsheet is a story waiting to be told."</span>
    <!-- duplicate for seamless loop -->
    <span class="ticker-item"><span>◆</span> "Data is the new oil — but insights are the refinery."</span>
    <span class="ticker-item"><span>◆</span> "In God we trust. All others must bring data." — W. Edwards Deming</span>
    <span class="ticker-item"><span>◆</span> "Without data, you're just another person with an opinion." — W. Edwards Deming</span>
    <span class="ticker-item"><span>◆</span> "The goal is to turn data into information, and information into insight." — Carly Fiorina</span>
    <span class="ticker-item"><span>◆</span> "Torture the data long enough and it will confess to anything." — Ronald Coase</span>
    <span class="ticker-item"><span>◆</span> "Data science is the sexiest job of the 21st century." — Harvard Business Review</span>
    <span class="ticker-item"><span>◆</span> "Every spreadsheet is a story waiting to be told."</span>
  </div>
</div>

<!-- ══════════════════ STATS BAR ══════════════════ -->
<div id="stats-bar">
  <div class="stats-row">
    <div class="stat-block fade-up">
      <span class="stat-block-num" data-count="21">0</span>
      <span class="stat-block-label">Verified Certs</span>
    </div>
    <div class="stat-block fade-up" style="transition-delay:.1s">
      <span class="stat-block-num" data-count="80">0</span>
      <span class="stat-block-label">Learning Hours+</span>
    </div>
    <div class="stat-block fade-up" style="transition-delay:.2s">
      <span class="stat-block-num" data-count="50000">0</span>
      <span class="stat-block-label">Records Analyzed+</span>
    </div>
    <div class="stat-block fade-up" style="transition-delay:.3s">
      <span class="stat-block-num" data-count="85">0</span>
      <span class="stat-block-label">Best R² Score %</span>
    </div>
  </div>
</div>

<!-- ══════════════════ QUOTES ══════════════════ -->
<section id="quotes" class="section">
  <div class="section-label">Philosophy</div>
  <h2 class="section-title">A Data Scientist's<br/>Mantras</h2>

  <div class="quotes-grid">
    <div class="quote-card fade-up">
      <div class="quote-mark">"</div>
      <p class="quote-text">The best ability a data scientist can have is the ability to ask the right question before writing a single line of code.</p>
      <div class="quote-author">— Data Analyst's First Law</div>
    </div>
    <div class="quote-card fade-up" style="transition-delay:.1s">
      <div class="quote-mark">"</div>
      <p class="quote-text">Correlation is not causation. But it's a really good starting point for a conversation with your stakeholders.</p>
      <div class="quote-author">— Every Data Scientist Ever</div>
    </div>
    <div class="quote-card fade-up" style="transition-delay:.15s">
      <div class="quote-mark">"</div>
      <p class="quote-text">A data scientist who can't explain their model to a business executive is just an expensive calculator.</p>
      <div class="quote-author">— On Communication & XAI</div>
    </div>
    <div class="quote-card fade-up" style="transition-delay:.2s">
      <div class="quote-mark">"</div>
      <p class="quote-text">Clean data is more valuable than a complex model. Garbage in, garbage out — no matter how fancy the algorithm.</p>
      <div class="quote-author">— The Preprocessing Gospel</div>
    </div>
    <div class="quote-card fade-up" style="transition-delay:.25s">
      <div class="quote-mark">"</div>
      <p class="quote-text">If your dashboard needs a legend to explain itself, your dashboard is the problem — not the data.</p>
      <div class="quote-author">— Power BI Philosophy</div>
    </div>
    <div class="quote-card fade-up" style="transition-delay:.3s">
      <div class="quote-mark">"</div>
      <p class="quote-text">Ninety percent of data science is data engineering. The other ten percent is arguing about whether it's really data engineering.</p>
      <div class="quote-author">— Industry Truth</div>
    </div>
  </div>

  <div class="quote-featured fade-up">
    <div class="quote-mark" style="color:rgba(124,58,237,.2);font-size:6rem;">"</div>
    <p class="quote-text">I don't just read data — I make it drive decisions.<br/>Because numbers without narrative are just noise.</p>
    <div class="quote-author" style="margin-top:1rem;">— Prasanth Kumar Sahu</div>
  </div>
</section>

<!-- ══════════════════ 3D CHART SECTION ══════════════════ -->
<section id="chart3d-section">
  <div class="section-label">Data Visualization · 3D</div>
  <h2 class="section-title">Skills in<br/>3D Space</h2>
  <div class="chart3d-grid">
    <canvas id="bar3d-canvas"></canvas>
    <div class="chart-info fade-up">
      <p class="chart-title">Interactive 3D<br/>Skill Landscape</p>
      <p class="chart-desc">
        This real-time 3D bar chart renders my technical proficiency across core data science domains. Built with Three.js — because if I'm showcasing data skills, the visualization itself should be a statement.<br/><br/>
        Drag to rotate · Scroll to zoom.
      </p>
      <div class="badge-row">
        <span class="badge badge-cyan">Three.js</span>
        <span class="badge badge-violet">WebGL</span>
        <span class="badge badge-pink">3D Rendering</span>
        <span class="badge badge-emerald">Real-time Data Viz</span>
      </div>
    </div>
  </div>
</section>

<!-- ══════════════════ SKILLS ══════════════════ -->
<section id="skills" class="section">
  <div class="section-label">Arsenal</div>
  <h2 class="section-title">Technical<br/>Proficiency</h2>

  <div class="skills-layout">
    <div id="radar-wrap" class="fade-up">
      <canvas id="radar-canvas" width="420" height="420"></canvas>
      <div class="radar-legend">
        <span class="legend-item"><span class="legend-dot" style="background:var(--cyan)"></span>Proficiency</span>
        <span class="legend-item"><span class="legend-dot" style="background:rgba(14,165,233,.2)"></span>Target</span>
      </div>
    </div>

    <div class="fade-up" style="transition-delay:.15s">
      <div class="skill-bars">
        <div class="skill-row">
          <div class="skill-meta"><span class="skill-name">Excel / Data Cleaning</span><span class="skill-pct">95%</span></div>
          <div class="skill-track"><div class="skill-fill" style="background:linear-gradient(90deg,var(--cyan),var(--violet));width:0" data-width="95%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span class="skill-name">Power BI / DAX</span><span class="skill-pct">90%</span></div>
          <div class="skill-track"><div class="skill-fill" style="background:linear-gradient(90deg,var(--cyan),var(--violet));" data-width="90%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span class="skill-name">EDA / Statistics</span><span class="skill-pct">90%</span></div>
          <div class="skill-track"><div class="skill-fill" style="background:linear-gradient(90deg,var(--violet),var(--pink));" data-width="90%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span class="skill-name">Pandas / NumPy</span><span class="skill-pct">88%</span></div>
          <div class="skill-track"><div class="skill-fill" style="background:linear-gradient(90deg,var(--cyan),var(--emerald));" data-width="88%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span class="skill-name">SQL / MySQL</span><span class="skill-pct">85%</span></div>
          <div class="skill-track"><div class="skill-fill" style="background:linear-gradient(90deg,var(--emerald),var(--cyan));" data-width="85%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span class="skill-name">Tableau</span><span class="skill-pct">80%</span></div>
          <div class="skill-track"><div class="skill-fill" style="background:linear-gradient(90deg,var(--amber),var(--pink));" data-width="80%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span class="skill-name">Machine Learning</span><span class="skill-pct">78%</span></div>
          <div class="skill-track"><div class="skill-fill" style="background:linear-gradient(90deg,var(--violet),var(--pink));" data-width="78%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span class="skill-name">FastAPI / Docker</span><span class="skill-pct">65%</span></div>
          <div class="skill-track"><div class="skill-fill" style="background:linear-gradient(90deg,var(--emerald),var(--cyan));" data-width="65%"></div></div>
        </div>
        <div class="skill-row">
          <div class="skill-meta"><span class="skill-name">Microsoft Azure</span><span class="skill-pct">60%</span></div>
          <div class="skill-track"><div class="skill-fill" style="background:linear-gradient(90deg,#0078d4,var(--cyan));" data-width="60%"></div></div>
        </div>
      </div>

      <div class="badge-section" style="margin-top:2.5rem;">
        <div class="badge-category">
          <div class="badge-cat-label">BI & Visualization</div>
          <div class="badge-row">
            <span class="badge badge-amber">Power BI</span>
            <span class="badge badge-amber">Tableau</span>
            <span class="badge badge-emerald">Excel</span>
            <span class="badge badge-pink">Streamlit</span>
          </div>
        </div>
        <div class="badge-category">
          <div class="badge-cat-label">Python Ecosystem</div>
          <div class="badge-row">
            <span class="badge badge-cyan">Python</span>
            <span class="badge badge-cyan">Pandas</span>
            <span class="badge badge-cyan">NumPy</span>
            <span class="badge badge-cyan">Scikit-learn</span>
            <span class="badge badge-cyan">Dask</span>
            <span class="badge badge-violet">XGBoost</span>
            <span class="badge badge-violet">SHAP</span>
          </div>
        </div>
        <div class="badge-category">
          <div class="badge-cat-label">Cloud & DevOps</div>
          <div class="badge-row">
            <span class="badge badge-violet">Azure</span>
            <span class="badge badge-amber">AWS</span>
            <span class="badge badge-cyan">Docker</span>
            <span class="badge badge-emerald">FastAPI</span>
            <span class="badge badge-pink">Firebase</span>
            <span class="badge badge-emerald">Linux</span>
          </div>
        </div>
        <div class="badge-category">
          <div class="badge-cat-label">Web & Security</div>
          <div class="badge-row">
            <span class="badge badge-pink">React</span>
            <span class="badge badge-pink">Next.js</span>
            <span class="badge badge-pink">Angular</span>
            <span class="badge badge-violet">Django</span>
            <span class="badge badge-emerald">NIST CSF 2.0</span>
            <span class="badge badge-amber">AutoCAD 3D</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ══════════════════ EXPERIENCE ══════════════════ -->
<section id="experience" class="section" style="background:var(--surface)">
  <div class="section-label">Experience</div>
  <h2 class="section-title">Work<br/>Experience</h2>
  <div class="exp-grid">
    <div class="exp-card fade-up">
      <div class="exp-header">
        <div>
          <div class="exp-company">Labmentix</div>
          <div class="exp-role">Data Analyst Intern</div>
        </div>
        <div class="exp-badge">
          <span class="status-dot"></span>
          Active
        </div>
      </div>
      <ul class="exp-list">
        <li>Building production Power BI dashboards for C-level stakeholders</li>
        <li>Conducting deep EDA on operational datasets to surface KPIs</li>
        <li>Automating reporting pipelines using Python + SQL</li>
        <li>Translating ambiguous business questions into precise data queries</li>
        <li>Creating DAX measures that reduced manual reporting by 70%+</li>
      </ul>
      <div class="exp-tags">
        <span class="badge badge-amber">Power BI</span>
        <span class="badge badge-cyan">Python</span>
        <span class="badge badge-cyan">SQL</span>
        <span class="badge badge-violet">DAX</span>
        <span class="badge badge-emerald">EDA</span>
      </div>
    </div>
    <div class="exp-card fade-up" style="transition-delay:.12s">
      <div class="exp-header">
        <div>
          <div class="exp-company">Codec Technologies</div>
          <div class="exp-role">Data Science Intern</div>
        </div>
        <div class="exp-badge">
          <span class="status-dot"></span>
          Active
        </div>
      </div>
      <ul class="exp-list">
        <li>Designing end-to-end ML pipelines from raw data to deployment</li>
        <li>Feature engineering, model selection, hyperparameter tuning</li>
        <li>Building predictive models solving real business problems</li>
        <li>Model interpretability using SHAP for stakeholder explainability</li>
        <li>Containerized API deployment via FastAPI + Docker</li>
      </ul>
      <div class="exp-tags">
        <span class="badge badge-cyan">Scikit-learn</span>
        <span class="badge badge-violet">XGBoost</span>
        <span class="badge badge-pink">SHAP</span>
        <span class="badge badge-emerald">FastAPI</span>
        <span class="badge badge-emerald">Docker</span>
      </div>
    </div>
  </div>
</section>

<!-- ══════════════════ PROJECTS ══════════════════ -->
<section id="projects" class="section">
  <div class="section-label">Work</div>
  <h2 class="section-title">Featured<br/>Projects</h2>
  <div class="projects-grid">

    <div class="project-card fade-up">
      <div class="project-num">01 / Power BI</div>
      <h3 class="project-title">Spotify Artist Intelligence Dashboard</h3>
      <p class="project-desc">End-to-end BI solution tracking artist streams, royalties, and audience demographics. Automated DAX measures cut analysis time drastically.</p>
      <div class="project-metrics">
        <span class="metric-pill">70% faster analysis</span>
        <span class="metric-pill">DAX automation</span>
        <span class="metric-pill">Live API data</span>
      </div>
      <div class="badge-row" style="margin-bottom:1.2rem">
        <span class="badge badge-amber">Power BI</span>
        <span class="badge badge-violet">DAX</span>
        <span class="badge badge-emerald">Spotify API</span>
      </div>
      <a href="https://github.com/PrasanthKumarS777/Spotify-Artist-Dashboard" class="project-link">View Project →</a>
    </div>

    <div class="project-card fade-up" style="transition-delay:.08s">
      <div class="project-num">02 / ML Platform</div>
      <h3 class="project-title">Tourism Analytics Platform</h3>
      <p class="project-desc">End-to-end ML platform on 50,000+ records — rating prediction, visit mode classification, and a hybrid recommendation engine.</p>
      <div class="project-metrics">
        <span class="metric-pill">R² = 0.85</span>
        <span class="metric-pill">70%+ accuracy</span>
        <span class="metric-pill">50k+ records</span>
      </div>
      <div class="badge-row" style="margin-bottom:1.2rem">
        <span class="badge badge-cyan">Python</span>
        <span class="badge badge-cyan">Scikit-learn</span>
        <span class="badge badge-pink">Streamlit</span>
      </div>
      <a href="https://github.com/PrasanthKumarS777/Tourism-Analytics-Platform" class="project-link">View Project →</a>
    </div>

    <div class="project-card fade-up" style="transition-delay:.12s">
      <div class="project-num">03 / NLP + Clustering</div>
      <h3 class="project-title">Zomato NLP & Clustering Analysis</h3>
      <p class="project-desc">Sentiment analysis + KMeans clustering on 10,000+ restaurant records uncovering hidden cuisine and location-based market segments.</p>
      <div class="project-metrics">
        <span class="metric-pill">10k+ records</span>
        <span class="metric-pill">NLP sentiment</span>
        <span class="metric-pill">KMeans clusters</span>
      </div>
      <div class="badge-row" style="margin-bottom:1.2rem">
        <span class="badge badge-cyan">Python</span>
        <span class="badge badge-violet">NLP</span>
        <span class="badge badge-amber">Jupyter</span>
      </div>
      <a href="https://github.com/PrasanthKumarS777/Zomato-Restaurant-Clustering-And-Sentimental-Analysis" class="project-link">View Project →</a>
    </div>

    <div class="project-card fade-up" style="transition-delay:.16s">
      <div class="project-num">04 / MLOps + XAI</div>
      <h3 class="project-title">Credit Risk Model with XAI</h3>
      <p class="project-desc">Production-ready credit risk classifier with SHAP explainability, deployed as a containerized REST API. Full MLOps lifecycle from training to serving.</p>
      <div class="project-metrics">
        <span class="metric-pill">SHAP explainability</span>
        <span class="metric-pill">REST API</span>
        <span class="metric-pill">Containerized</span>
      </div>
      <div class="badge-row" style="margin-bottom:1.2rem">
        <span class="badge badge-violet">XGBoost</span>
        <span class="badge badge-pink">SHAP</span>
        <span class="badge badge-emerald">FastAPI</span>
        <span class="badge badge-cyan">Docker</span>
      </div>
      <a href="https://github.com/PrasanthKumarS777/loan-default-prediction-xai" class="project-link">View Project →</a>
    </div>

    <div class="project-card fade-up" style="transition-delay:.2s">
      <div class="project-num">05 / Real-Time</div>
      <h3 class="project-title">Real-Time Weather Analytics Dashboard</h3>
      <p class="project-desc">Live weather analytics consuming real-time API feeds with dynamic interactive visualizations and location-based intelligence.</p>
      <div class="project-metrics">
        <span class="metric-pill">Live API</span>
        <span class="metric-pill">Interactive charts</span>
        <span class="metric-pill">Location-aware</span>
      </div>
      <div class="badge-row" style="margin-bottom:1.2rem">
        <span class="badge badge-amber">JavaScript</span>
        <span class="badge badge-cyan">REST API</span>
        <span class="badge badge-violet">Chart.js</span>
      </div>
      <a href="https://github.com/PrasanthKumarS777/Realtime-Weather-API-Dashboard" class="project-link">View Project →</a>
    </div>

    <div class="project-card fade-up" style="transition-delay:.24s">
      <div class="project-num">06 / Full-Stack</div>
      <h3 class="project-title">Financial Intelligence Dashboard</h3>
      <p class="project-desc">Full-stack personal finance manager with real-time Firebase backend, smart budget tracking, and spending behavior analytics.</p>
      <div class="project-metrics">
        <span class="metric-pill">Real-time DB</span>
        <span class="metric-pill">Smart analytics</span>
        <span class="metric-pill">Full-stack</span>
      </div>
      <div class="badge-row" style="margin-bottom:1.2rem">
        <span class="badge badge-amber">JavaScript</span>
        <span class="badge badge-amber">Firebase</span>
        <span class="badge badge-pink">Analytics</span>
      </div>
      <a href="https://github.com/PrasanthKumarS777/financial-intelligence-dashboard" class="project-link">View Project →</a>
    </div>

  </div>
</section>

<!-- ══════════════════ CERTS ══════════════════ -->
<section id="certs" class="section" style="background:var(--surface)">
  <div class="section-label">Credentials</div>
  <h2 class="section-title">21 Certificates ·<br/>All Verified</h2>

  <div class="cert-grid">
    <div class="certs-section-title">📊 Data Science & Analytics Core</div>
    <div class="cert-card fade-up"><span class="cert-num">01</span><div class="cert-info"><div class="cert-name">Python for Data Analysis</div><div class="cert-meta"><span class="cert-platform">MTF Institute / Udemy</span><span>4.5h</span><span>Jan 2026</span></div></div><a href="https://ude.my/UC-3226dfa9-d872-45c4-9a75-36d8c6ce698c" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">02</span><div class="cert-info"><div class="cert-name">Data Manipulation: NumPy & Pandas</div><div class="cert-meta"><span class="cert-platform">Meta Brains / Udemy</span><span>4.0h</span><span>Jan 2026</span></div></div><a href="https://ude.my/UC-116f50ec-bc87-4c6a-98af-6f4998908898" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">03</span><div class="cert-info"><div class="cert-name">Power BI & Tableau 2-in-1 Bundle</div><div class="cert-meta"><span class="cert-platform">Start-Tech / Udemy</span><span>17.5h</span><span>Jan 2026</span></div></div><a href="https://ude.my/UC-046ab4fa-aa50-4b4f-8dad-a3a896ded970" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">04</span><div class="cert-info"><div class="cert-name">MySQL for Beginners</div><div class="cert-meta"><span class="cert-platform">Meta Brains / Udemy</span><span>2.5h</span><span>Jan 2026</span></div></div><a href="https://ude.my/UC-46236305-51da-4855-b97f-acdf0d8ebba0" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">05</span><div class="cert-info"><div class="cert-name">Data Science: Probability & Statistics</div><div class="cert-meta"><span class="cert-platform">MTF Institute / Udemy</span><span>7.5h</span><span>Jan 2026</span></div></div><a href="https://ude.my/UC-50bac0a4-ea41-4bfd-ad58-e4b9709696ba" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">06</span><div class="cert-info"><div class="cert-name">Deploy ML with FastAPI & Docker</div><div class="cert-meta"><span class="cert-platform">Meta Brains / Udemy</span><span>4.0h</span><span>Jan 2026</span></div></div><a href="https://ude.my/UC-0dff35f0-d48a-467e-b9b1-84e72ba2d24f" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">07</span><div class="cert-info"><div class="cert-name">Master Business Analysis</div><div class="cert-meta"><span class="cert-platform">Arun Singhal / Udemy</span><span>7.0h</span><span>Jan 2026</span></div></div><a href="https://ude.my/UC-10718909-e4d1-480a-a656-66fb911bbbf4" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">08</span><div class="cert-info"><div class="cert-name">Master Dask: Python Parallel Computing</div><div class="cert-meta"><span class="cert-platform">Meta Brains / Udemy</span><span>3.0h</span><span>Dec 2025</span></div></div><a href="https://ude.my/UC-33fe5381-0bd0-46b1-93ff-ea66309f4407" class="cert-link" target="_blank">Verify ↗</a></div>

    <div class="certs-section-title">☁️ Cloud & Infrastructure</div>
    <div class="cert-card fade-up"><span class="cert-num">09</span><div class="cert-info"><div class="cert-name">Microsoft Azure</div><div class="cert-meta"><span class="cert-platform">Learntoupgrade / Udemy</span><span>3.0h</span><span>Dec 2025</span></div></div><a href="https://ude.my/UC-b64febe2-f37a-4bfd-a580-f7a74e0ca5fe" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">10</span><div class="cert-info"><div class="cert-name">Python 4000: Linux Commands & DevOps Automation</div><div class="cert-meta"><span class="cert-platform">Mr. Randall Nagy / Udemy</span><span>4.5h</span><span>Dec 2025</span></div></div><a href="https://ude.my/UC-c0be4a9c-095f-4f02-8846-e71453255937" class="cert-link" target="_blank">Verify ↗</a></div>

    <div class="certs-section-title">🔐 Security & Cybersecurity</div>
    <div class="cert-card fade-up"><span class="cert-num">11</span><div class="cert-info"><div class="cert-name">NIST Cybersecurity Framework (CSF) 2.0</div><div class="cert-meta"><span class="cert-platform">Dr. Amar Massoud / Udemy</span><span>2.0h</span><span>Dec 2025</span></div></div><a href="https://ude.my/UC-d3ff6da3-04a7-4cb2-83f7-3a2c72607982" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">12</span><div class="cert-info"><div class="cert-name">Ethically Hack the Planet Part 3</div><div class="cert-meta"><span class="cert-platform">Cyber Twinkle / Udemy</span><span>33m</span><span>Dec 2025</span></div></div><a href="https://ude.my/UC-f6aea034-b593-41a3-81ba-9b2cd61ffae1" class="cert-link" target="_blank">Verify ↗</a></div>

    <div class="certs-section-title">🌐 Web Development & Engineering</div>
    <div class="cert-card fade-up"><span class="cert-num">13</span><div class="cert-info"><div class="cert-name">Mastering Web Design: HTML, CSS & Generative AI</div><div class="cert-meta"><span class="cert-platform">Skool of AI / Udemy</span><span>4.5h</span><span>Dec 2025</span></div></div><a href="https://ude.my/UC-cfaaabff-0ace-4056-939f-be21426c8562" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">14</span><div class="cert-info"><div class="cert-name">React.JS for Ecommerce</div><div class="cert-meta"><span class="cert-platform">Meta Brains / Udemy</span><span>3.5h</span><span>Dec 2025</span></div></div><a href="https://ude.my/UC-f0334987-9e14-41c2-aca6-357dd89dc35a" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">15</span><div class="cert-info"><div class="cert-name">Angular for Beginners to Advanced Projects</div><div class="cert-meta"><span class="cert-platform">Meta Brains / Udemy</span><span>3.5h</span><span>Dec 2025</span></div></div><a href="https://ude.my/UC-7acd2f3b-be84-4288-9125-ac87c9abae81" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">16</span><div class="cert-info"><div class="cert-name">Next.js: Build Scalable React Apps</div><div class="cert-meta"><span class="cert-platform">Anton Voroniuk / Udemy</span><span>5.0h</span><span>Dec 2025</span></div></div><a href="https://ude.my/UC-69af5fda-c053-4446-9caf-a161c437461c" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">17</span><div class="cert-info"><div class="cert-name">Secure Python & Django: Hack-Proof Web Apps</div><div class="cert-meta"><span class="cert-platform">Meta Brains / Udemy</span><span>5.5h</span><span>Dec 2025</span></div></div><a href="https://ude.my/UC-9363e402-7822-42e2-bc62-84db129f1905" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">18</span><div class="cert-info"><div class="cert-name">AutoCAD 3D: Basics to Advanced Modelling</div><div class="cert-meta"><span class="cert-platform">Meta Brains / Udemy</span><span>3.5h</span><span>Dec 2025</span></div></div><a href="https://ude.my/UC-0e0ad0dc-5dc0-44da-bc8f-9690c785b7f3" class="cert-link" target="_blank">Verify ↗</a></div>
    <div class="cert-card fade-up"><span class="cert-num">19</span><div class="cert-info"><div class="cert-name">No-Code SaaS Development: Idea to App</div><div class="cert-meta"><span class="cert-platform">Meta Brains / Udemy</span><span>7.5h</span><span>Dec 2025</span></div></div><a href="https://ude.my/UC-91e73cfb-8117-4b65-a40e-7eff1401e96d" class="cert-link" target="_blank">Verify ↗</a></div>

    <div class="certs-section-title">🏆 Industry Job Simulations — Forage</div>
    <div class="cert-card fade-up" style="grid-column:1/-1;background:rgba(245,158,11,.04);border:1px solid rgba(245,158,11,.15);">
      <span class="cert-num">20</span>
      <div class="cert-info">
        <div class="cert-name" style="color:var(--amber)">Walmart Global Tech — Advanced Software Engineering Job Simulation</div>
        <div class="cert-meta"><span style="color:var(--amber)">Forage Platform</span><span>Dec 12, 2025</span></div>
        <div style="margin-top:.6rem;font-family:'DM Mono',monospace;font-size:.65rem;color:var(--muted)">Advanced Data Structures · Software Architecture · Relational Database Design · Data Munging</div>
      </div>
    </div>
    <div class="cert-card fade-up" style="grid-column:1/-1;background:rgba(255,153,0,.04);border:1px solid rgba(255,153,0,.15);">
      <span class="cert-num">21</span>
      <div class="cert-info">
        <div class="cert-name" style="color:#ff9900">Amazon Web Services — Solutions Architecture Job Simulation</div>
        <div class="cert-meta"><span style="color:#ff9900">Forage Platform</span><span>Dec 18, 2025</span></div>
        <div style="margin-top:.6rem;font-family:'DM Mono',monospace;font-size:.65rem;color:var(--muted)">Designing simple, scalable, cloud-native hosting architectures on AWS</div>
      </div>
    </div>
  </div>
</section>

<!-- ══════════════════ CONTACT ══════════════════ -->
<section id="contact">
  <div class="fade-up">
    <div class="section-label" style="justify-content:center;margin-bottom:1.5rem">Let's build something</div>
    <h2 class="contact-tagline">Open to Data Analyst,<br/>BI Analyst & DS Roles</h2>
    <p class="contact-sub">Bring your messiest dataset. I'll turn it into your clearest decision. Let's talk.</p>
    <div class="contact-links">
      <a href="https://linkedin.com/in/prasanthsahu7" class="contact-link primary" target="_blank">↗ LinkedIn</a>
      <a href="mailto:pk777sahu@gmail.com" class="contact-link" target="_blank">✉ pk777sahu@gmail.com</a>
      <a href="https://github.com/PrasanthKumarS777" class="contact-link" target="_blank">⌥ GitHub</a>
    </div>
  </div>
</section>

<footer>
  <span>© 2026 Prasanth Kumar Sahu</span>
  <span>Built with <span>Three.js</span> · <span>Canvas API</span> · <span>WebGL</span></span>
  <span>Data drives decisions. <span>I drive data.</span></span>
</footer>

<script>
// ─── CURSOR ───────────────────────────────────────────────
const cursor = document.getElementById('cursor');
const trail  = document.getElementById('cursor-trail');
let mx=0,my=0,tx=0,ty=0;
document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  cursor.style.left = mx+'px'; cursor.style.top = my+'px';
});
(function animTrail(){
  tx += (mx-tx)*.12; ty += (my-ty)*.12;
  trail.style.left = tx+'px'; trail.style.top = ty+'px';
  requestAnimationFrame(animTrail);
})();
document.querySelectorAll('a,.btn,.badge,.project-card,.cert-card,.quote-card,.stat-block').forEach(el=>{
  el.addEventListener('mouseenter',()=>{cursor.style.width='20px';cursor.style.height='20px';cursor.style.background='var(--violet)';});
  el.addEventListener('mouseleave',()=>{cursor.style.width='12px';cursor.style.height='12px';cursor.style.background='var(--cyan)';});
});

// ─── PARTICLES ─────────────────────────────────────────────
const pc = document.getElementById('particles-canvas');
const pctx = pc.getContext('2d');
let pw, ph, particles=[];
function resizeP(){ pw=pc.width=window.innerWidth; ph=pc.height=window.innerHeight; }
resizeP(); window.addEventListener('resize',resizeP);
class Particle {
  constructor(){this.reset();}
  reset(){
    this.x=Math.random()*pw; this.y=Math.random()*ph;
    this.vx=(Math.random()-.5)*.3; this.vy=(Math.random()-.5)*.3;
    this.r=Math.random()*1.5+.5;
    this.life=Math.random()*180+60; this.age=0;
    this.color=Math.random()<.5?'14,165,233':'124,58,237';
  }
  update(){this.x+=this.vx;this.y+=this.vy;this.age++;if(this.age>this.life)this.reset();}
  draw(){
    const alpha=(this.age<30?this.age/30:this.age>this.life-30?(this.life-this.age)/30:1)*.6;
    pctx.beginPath();pctx.arc(this.x,this.y,this.r,0,Math.PI*2);
    pctx.fillStyle=`rgba(${this.color},${alpha})`;pctx.fill();
  }
}
for(let i=0;i<120;i++) particles.push(new Particle());

// Draw lines between nearby particles
function drawLines(){
  for(let i=0;i<particles.length;i++){
    for(let j=i+1;j<particles.length;j++){
      const dx=particles[i].x-particles[j].x;
      const dy=particles[i].y-particles[j].y;
      const dist=Math.sqrt(dx*dx+dy*dy);
      if(dist<120){
        const alpha=(1-dist/120)*.15;
        pctx.beginPath();
        pctx.moveTo(particles[i].x,particles[i].y);
        pctx.lineTo(particles[j].x,particles[j].y);
        pctx.strokeStyle=`rgba(14,165,233,${alpha})`;
        pctx.lineWidth=.5;pctx.stroke();
      }
    }
  }
}
function animP(){
  pctx.clearRect(0,0,pw,ph);
  drawLines();
  particles.forEach(p=>{p.update();p.draw();});
  requestAnimationFrame(animP);
}
animP();

// ─── THREE.JS HERO NEURAL NETWORK ──────────────────────────
(function initHeroThree(){
  const canvas = document.getElementById('threejs-canvas');
  const renderer = new THREE.WebGLRenderer({canvas, antialias:true, alpha:true});
  renderer.setPixelRatio(window.devicePixelRatio);
  renderer.setClearColor(0x000000, 0);

  const scene = new THREE.Scene();
  const camera = new THREE.PerspectiveCamera(60, canvas.clientWidth/canvas.clientHeight, 0.1, 1000);
  camera.position.set(0, 0, 28);

  function resize(){
    const w=canvas.clientWidth, h=canvas.clientHeight;
    renderer.setSize(w,h,false);
    camera.aspect=w/h; camera.updateProjectionMatrix();
  }
  resize(); window.addEventListener('resize',resize);

  // ─ Floating data nodes
  const nodeGeo = new THREE.SphereGeometry(.22,12,12);
  const nodeMat = new THREE.MeshPhongMaterial({color:0x0ea5e9, emissive:0x0369a1, shininess:120});
  const nodes=[], nodePositions=[];
  for(let i=0;i<60;i++){
    const mesh=new THREE.Mesh(nodeGeo,nodeMat.clone());
    const x=(Math.random()-.5)*30, y=(Math.random()-.5)*20, z=(Math.random()-.5)*16;
    mesh.position.set(x,y,z);
    nodePositions.push({x,y,z,vx:(Math.random()-.5)*.015,vy:(Math.random()-.5)*.015,vz:(Math.random()-.5)*.01});
    scene.add(mesh); nodes.push(mesh);
  }

  // ─ Lines between nodes
  const lineMat = new THREE.LineBasicMaterial({color:0x0ea5e9, transparent:true, opacity:.15});
  const lineGroup = new THREE.Group(); scene.add(lineGroup);

  function updateLines(){
    lineGroup.clear();
    for(let i=0;i<nodes.length;i++){
      for(let j=i+1;j<nodes.length;j++){
        const dx=nodes[i].position.x-nodes[j].position.x;
        const dy=nodes[i].position.y-nodes[j].position.y;
        const dz=nodes[i].position.z-nodes[j].position.z;
        const dist=Math.sqrt(dx*dx+dy*dy+dz*dz);
        if(dist<7){
          const pts=[nodes[i].position.clone(),nodes[j].position.clone()];
          const geo=new THREE.BufferGeometry().setFromPoints(pts);
          const mat=new THREE.LineBasicMaterial({color:0x0ea5e9,transparent:true,opacity:(1-dist/7)*.2});
          lineGroup.add(new THREE.Line(geo,mat));
        }
      }
    }
  }

  // ─ Central rotating sphere (data globe)
  const globeGeo = new THREE.SphereGeometry(4.5,32,32);
  const globeMat = new THREE.MeshPhongMaterial({
    color:0x0f172a, wireframe:true,
    emissive:0x0ea5e9, emissiveIntensity:.08,
    transparent:true, opacity:.5
  });
  const globe = new THREE.Mesh(globeGeo,globeMat);
  scene.add(globe);

  // ─ Orbit ring
  const ringGeo = new THREE.TorusGeometry(6,.04,8,80);
  const ringMat = new THREE.MeshBasicMaterial({color:0x7c3aed, transparent:true, opacity:.5});
  const ring = new THREE.Mesh(ringGeo,ringMat);
  ring.rotation.x = Math.PI/3;
  scene.add(ring);

  const ring2 = new THREE.Mesh(new THREE.TorusGeometry(7.5,.03,8,80),
    new THREE.MeshBasicMaterial({color:0x0ea5e9,transparent:true,opacity:.3}));
  ring2.rotation.x = Math.PI/5; ring2.rotation.z = Math.PI/4;
  scene.add(ring2);

  // ─ Floating data "bars"
  const barGroup = new THREE.Group(); scene.add(barGroup);
  const barData = [.95,.90,.90,.88,.85,.80,.78,.65,.60];
  const barColors=[0x0ea5e9,0x7c3aed,0xec4899,0x10b981,0x0ea5e9,0xf59e0b,0x7c3aed,0x10b981,0x0078d4];
  barData.forEach((v,i)=>{
    const h=v*6;
    const geo=new THREE.BoxGeometry(.5,h,.5);
    const mat=new THREE.MeshPhongMaterial({color:barColors[i],emissive:barColors[i],emissiveIntensity:.25,transparent:true,opacity:.8});
    const bar=new THREE.Mesh(geo,mat);
    bar.position.set(-10+i*2.5, h/2-5, -6);
    barGroup.add(bar);
  });

  // Lights
  scene.add(new THREE.AmbientLight(0x0f172a, 2));
  const dLight=new THREE.DirectionalLight(0x0ea5e9, 3);
  dLight.position.set(5,10,10); scene.add(dLight);
  const pLight=new THREE.PointLight(0x7c3aed,4,30);
  pLight.position.set(-8,0,5); scene.add(pLight);
  const pLight2=new THREE.PointLight(0xec4899,2,25);
  pLight2.position.set(8,-4,3); scene.add(pLight2);

  let frame=0;
  function animate(){
    requestAnimationFrame(animate); frame++;
    globe.rotation.y+=.004; globe.rotation.x+=.001;
    ring.rotation.z+=.006; ring2.rotation.y+=.004;

    nodes.forEach((n,i)=>{
      const p=nodePositions[i];
      p.x+=p.vx; p.y+=p.vy; p.z+=p.vz;
      if(Math.abs(p.x)>15)p.vx*=-1;
      if(Math.abs(p.y)>10)p.vy*=-1;
      if(Math.abs(p.z)>8)p.vz*=-1;
      n.position.set(p.x,p.y,p.z);
      n.material.emissiveIntensity=.1+Math.sin(frame*.02+i)*.1;
    });

    barGroup.children.forEach((b,i)=>{
      b.rotation.y+=.008;
      b.position.y=barData[i]*3+Math.sin(frame*.03+i*.7)*.3-2;
    });

    if(frame%3===0) updateLines();
    renderer.render(scene,camera);
  }
  animate();
})();

// ─── THREE.JS 3D BAR CHART ─────────────────────────────────
(function initBar3D(){
  const canvas = document.getElementById('bar3d-canvas');
  const renderer = new THREE.WebGLRenderer({canvas, antialias:true, alpha:true});
  renderer.setPixelRatio(Math.min(window.devicePixelRatio,2));
  renderer.setClearColor(0x0d1220, 1);
  renderer.shadowMap.enabled=true;

  const scene = new THREE.Scene();
  const camera = new THREE.PerspectiveCamera(50, 1, .1, 200);
  camera.position.set(18,14,18);
  camera.lookAt(0,3,0);

  function resize(){
    const w=canvas.clientWidth, h=canvas.clientHeight;
    renderer.setSize(w,h,false);
    camera.aspect=w/h; camera.updateProjectionMatrix();
  }
  resize(); window.addEventListener('resize',resize);

  // Grid floor
  const gridHelper=new THREE.GridHelper(22,22,0x1e293b,0x1e293b);
  scene.add(gridHelper);

  // Bars
  const skills=[
    {label:'Excel',val:.95,color:0x10b981},
    {label:'Power BI',val:.90,color:0xf59e0b},
    {label:'EDA',val:.90,color:0x0ea5e9},
    {label:'Pandas',val:.88,color:0x0ea5e9},
    {label:'SQL',val:.85,color:0x7c3aed},
    {label:'Tableau',val:.80,color:0xf59e0b},
    {label:'ML',val:.78,color:0xec4899},
    {label:'FastAPI',val:.65,color:0x10b981},
    {label:'Azure',val:.60,color:0x0078d4},
  ];
  const maxH=10;
  const bars=[];
  skills.forEach((s,i)=>{
    const h=s.val*maxH;
    const geo=new THREE.BoxGeometry(1.2,h,1.2);
    const mat=new THREE.MeshPhongMaterial({
      color:s.color,emissive:s.color,emissiveIntensity:.2,
      transparent:true,opacity:.92,shininess:100
    });
    const bar=new THREE.Mesh(geo,mat);
    bar.position.set(i*2.2-9,h/2,0);
    bar.castShadow=true;
    bar.userData={targetY:h/2, origH:h, idx:i};
    scene.add(bar);
    bars.push(bar);

    // Top glow plane
    const topGeo=new THREE.PlaneGeometry(1.2,1.2);
    const topMat=new THREE.MeshBasicMaterial({color:s.color,transparent:true,opacity:.7});
    const top=new THREE.Mesh(topGeo,topMat);
    top.rotation.x=-Math.PI/2;
    top.position.set(i*2.2-9,h,0);
    scene.add(top);
  });

  // Lights
  scene.add(new THREE.AmbientLight(0x0f172a,3));
  const dL=new THREE.DirectionalLight(0xffffff,2); dL.position.set(10,20,10); scene.add(dL);
  const pL=new THREE.PointLight(0x0ea5e9,4,40); pL.position.set(-5,15,8); scene.add(pL);
  const pL2=new THREE.PointLight(0x7c3aed,3,35); pL2.position.set(10,10,-5); scene.add(pL2);

  // Orbit controls (manual)
  let isDragging=false, prevX=0, prevY=0;
  let theta=Math.PI/4, phi=Math.PI/4, radius=30;
  canvas.addEventListener('mousedown',e=>{isDragging=true;prevX=e.clientX;prevY=e.clientY;});
  window.addEventListener('mouseup',()=>isDragging=false);
  window.addEventListener('mousemove',e=>{
    if(!isDragging)return;
    theta-=(e.clientX-prevX)*.008;
    phi=Math.max(.2,Math.min(1.4,phi-(e.clientY-prevY)*.008));
    prevX=e.clientX;prevY=e.clientY;
  });
  canvas.addEventListener('wheel',e=>{radius=Math.max(15,Math.min(50,radius+e.deltaY*.05));});

  let frame=0;
  function animate(){
    requestAnimationFrame(animate);frame++;
    // Auto rotate when not dragging
    if(!isDragging) theta+=.005;
    camera.position.x=radius*Math.sin(theta)*Math.cos(phi);
    camera.position.y=radius*Math.sin(phi);
    camera.position.z=radius*Math.cos(theta)*Math.cos(phi);
    camera.lookAt(0,3,0);

    // Animate bars breathing
    bars.forEach((b,i)=>{
      const h=b.userData.origH;
      const wave=Math.sin(frame*.04+i*.5)*.3;
      b.scale.y=1+(wave/h);
      b.position.y=b.userData.targetY+wave/2;
      b.material.emissiveIntensity=.2+Math.abs(wave)*.15;
    });

    renderer.render(scene,camera);
  }
  animate();
})();

// ─── RADAR CHART ───────────────────────────────────────────
(function drawRadar(){
  const canvas=document.getElementById('radar-canvas');
  const ctx=canvas.getContext('2d');
  const cx=210,cy=210,r=160;
  const skills=[
    {label:'Power BI',val:.90},{label:'Python',val:.88},
    {label:'SQL',val:.85},{label:'ML',val:.78},
    {label:'Statistics',val:.90},{label:'Tableau',val:.80},
    {label:'EDA',val:.92},{label:'Excel',val:.95}
  ];
  const n=skills.length;
  let prog=0;
  function draw(p){
    ctx.clearRect(0,0,420,420);
    // Background webs
    for(let lvl=1;lvl<=5;lvl++){
      ctx.beginPath();
      for(let i=0;i<n;i++){
        const angle=i*(2*Math.PI/n)-Math.PI/2;
        const rv=r*(lvl/5);
        const x=cx+rv*Math.cos(angle), y=cy+rv*Math.sin(angle);
        i===0?ctx.moveTo(x,y):ctx.lineTo(x,y);
      }
      ctx.closePath();
      ctx.strokeStyle=`rgba(14,165,233,${.04+lvl*.02})`;
      ctx.lineWidth=1;ctx.stroke();
    }
    // Axes
    for(let i=0;i<n;i++){
      const angle=i*(2*Math.PI/n)-Math.PI/2;
      ctx.beginPath();ctx.moveTo(cx,cy);
      ctx.lineTo(cx+r*Math.cos(angle),cy+r*Math.sin(angle));
      ctx.strokeStyle='rgba(14,165,233,.12)';ctx.lineWidth=1;ctx.stroke();
    }
    // Data polygon (fill)
    ctx.beginPath();
    skills.forEach((s,i)=>{
      const angle=i*(2*Math.PI/n)-Math.PI/2;
      const rv=r*s.val*p;
      const x=cx+rv*Math.cos(angle), y=cy+rv*Math.sin(angle);
      i===0?ctx.moveTo(x,y):ctx.lineTo(x,y);
    });
    ctx.closePath();
    const grad=ctx.createRadialGradient(cx,cy,0,cx,cy,r);
    grad.addColorStop(0,'rgba(124,58,237,.35)');
    grad.addColorStop(1,'rgba(14,165,233,.15)');
    ctx.fillStyle=grad;ctx.fill();
    ctx.strokeStyle='rgba(14,165,233,.8)';ctx.lineWidth=2;ctx.stroke();
    // Data points
    skills.forEach((s,i)=>{
      const angle=i*(2*Math.PI/n)-Math.PI/2;
      const rv=r*s.val*p;
      const x=cx+rv*Math.cos(angle), y=cy+rv*Math.sin(angle);
      ctx.beginPath();ctx.arc(x,y,4,0,Math.PI*2);
      ctx.fillStyle='var(--cyan)';
      ctx.shadowColor='var(--cyan)';ctx.shadowBlur=10;ctx.fill();
      ctx.shadowBlur=0;
    });
    // Labels
    ctx.font='bold 11px Space Mono, monospace';
    ctx.textAlign='center';ctx.textBaseline='middle';
    skills.forEach((s,i)=>{
      const angle=i*(2*Math.PI/n)-Math.PI/2;
      const x=cx+(r+24)*Math.cos(angle), y=cy+(r+24)*Math.sin(angle);
      ctx.fillStyle='#94a3b8';ctx.fillText(s.label,x,y);
    });
  }
  function animRadar(){
    if(prog<1){prog=Math.min(1,prog+.025);draw(prog);requestAnimationFrame(animRadar);}
    else draw(1);
  }
  // Trigger on scroll
  const obs=new IntersectionObserver(entries=>{
    if(entries[0].isIntersecting){animRadar();obs.disconnect();}
  },{threshold:.3});
  obs.observe(canvas);
})();

// ─── TYPEWRITER ────────────────────────────────────────────
const lines=[
  'print("Turning chaos into clarity")',
  'SELECT insight FROM raw_data WHERE noise = 0',
  'model.fit(business_problem, data_solution)',
  'dashboard.deploy("C-Level Decision Support")',
  'SHAP.explain(why_this_prediction_matters)',
  'df.dropna().transform().tell_the_story()',
];
let li=0,ci=0,deleting=false;
const tw=document.getElementById('typewriter');
function typeAnim(){
  const current=lines[li];
  if(!deleting){
    tw.textContent=current.slice(0,ci+1);ci++;
    if(ci===current.length){deleting=true;setTimeout(typeAnim,1800);return;}
  } else {
    tw.textContent=current.slice(0,ci-1);ci--;
    if(ci===0){deleting=false;li=(li+1)%lines.length;setTimeout(typeAnim,400);return;}
  }
  setTimeout(typeAnim,deleting?40:60);
}
typeAnim();

// ─── COUNTER ANIMATION ─────────────────────────────────────
function animCount(el,target,suffix=''){
  let start=0;
  const dur=2000, step=16;
  const inc=target/(dur/step);
  const t=setInterval(()=>{
    start=Math.min(start+inc,target);
    el.textContent=Math.floor(start)+(suffix);
    if(start>=target)clearInterval(t);
  },step);
}
const obs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      e.target.querySelectorAll('[data-count]').forEach(el=>{
        const v=parseInt(el.dataset.count);
        const suffix=el.dataset.count==='85'?'%':el.dataset.count==='80'?'+':
                     el.dataset.count==='50000'?'+':'';
        animCount(el,v,suffix);
      });
      obs.unobserve(e.target);
    }
  });
},{threshold:.3});
document.querySelectorAll('#hero,#stats-bar').forEach(s=>obs.observe(s));

// ─── SKILL BARS ANIMATION ──────────────────────────────────
const barObs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      e.target.querySelectorAll('.skill-fill[data-width]').forEach((fill,i)=>{
        setTimeout(()=>{ fill.style.width=fill.dataset.width; },i*80);
      });
      barObs.unobserve(e.target);
    }
  });
},{threshold:.2});
document.querySelectorAll('#skills').forEach(s=>barObs.observe(s));

// ─── FADE-UP OBSERVER ──────────────────────────────────────
const fadeObs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{if(e.isIntersecting){e.target.classList.add('visible');fadeObs.unobserve(e.target);}});
},{threshold:.08});
document.querySelectorAll('.fade-up').forEach(el=>fadeObs.observe(el));
</script>
</body>
</html>
