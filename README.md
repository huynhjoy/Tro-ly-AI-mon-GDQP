<!doctype html>
<html lang="vi"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self' 'unsafe-inline' https://cdn.jsdelivr.net https://cdnjs.cloudflare.com; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src https://fonts.gstatic.com; connect-src 'self' https://*.supabase.co https://cdnjs.cloudflare.com https://api.github.com https://raw.githubusercontent.com; worker-src blob:; img-src 'self' data: blob:; base-uri 'none'; object-src 'none'">
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2.45.4/dist/umd/supabase.min.js"></script>
<title>GDQP&AN – Trợ lý AI</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<style>
:root {
  --bg: #f3f4f6;          
  --sf: #ffffff;          
  --tx: #111827;          
  --mu: #6b7280;          
  --ln: #e5e7eb;          
  --pr: #10b981;          
  --pr-hover: #059669;    
  --ok: #10b981;          
  --no: #ef4444;          
  --am: #f59e0b;          
  --sh: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  box-sizing: border-box;
}

@media(prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#111827;--sf:#1f2937;--tx:#f9fafb;--mu:#9ca3af;--ln:#374151;--pr:#34d399;--ok:#34d399;--no:#f87171;--am:#fbbf24;color-scheme:dark}}
:root[data-theme="dark"]{--bg:#111827;--sf:#1f2937;--tx:#f9fafb;--mu:#9ca3af;--ln:#374151;--pr:#34d399;--ok:#34d399;--no:#f87171;--am:#fbbf24;color-scheme:dark}

html { scroll-padding-top: env(safe-area-inset-top,0px); }
* { box-sizing: border-box; }
body { margin: 0; background: var(--bg); color: var(--tx); font: 15px/1.6 'Inter', system-ui, sans-serif; }
main { max-width: 900px; margin: 0 auto; padding: 24px 16px; }

h1 { font-size: 1.5rem; font-weight: 800; margin: 0.2em 0; letter-spacing: -0.02em;}
h2 { font-size: 1.15rem; font-weight: 700; margin: 1.2em 0 0.5em; display: flex; align-items: center; gap: 8px;}

.card {
    background: var(--sf); border: 1px solid var(--ln); border-radius: 16px;
    padding: 24px; margin: 16px 0; box-shadow: var(--sh); transition: transform 0.2s;
}

label { display: block; font-weight: 600; margin: 12px 0 6px; font-size: 0.9rem; color: var(--tx); }
input, select, textarea {
    width: 100%; padding: 12px; border: 1px solid var(--ln);
    border-radius: 10px; background: var(--bg); color: var(--tx); font: inherit;
    transition: border-color 0.2s, box-shadow 0.2s;
}
input[type=checkbox], input[type=radio] { width: auto; accent-color: var(--pr); transform: scale(1.1); margin-right: 6px;}
.row { display: flex; gap: 12px; flex-wrap: wrap; }
.row > * { flex: 1; min-width: 140px; }

button {
    font: inherit; font-weight: 600; border: 0; border-radius: 10px;
    padding: 12px 20px; background: var(--pr); color: #fff;
    cursor: pointer; transition: all 0.2s; box-shadow: 0 2px 4px rgba(16, 185, 129, 0.2);
}
button:hover { background: var(--pr-hover); transform: translateY(-1px); box-shadow: 0 4px 6px rgba(16, 185, 129, 0.3); }
button.alt { background: transparent; color: var(--pr); border: 1.5px solid var(--pr); box-shadow: none; }
button.alt:hover { background: rgba(16, 185, 129, 0.05); }
button.danger { background: #fee2e2; color: var(--no); box-shadow: none; padding: 8px 12px; font-size: 0.85rem; }
button.danger:hover { background: #fca5a5; color: #fff; }
button:focus-visible, input:focus-visible, select:focus-visible, textarea:focus-visible { outline: 2px solid var(--pr); outline-offset: 2px; }

.tabs { display: flex; gap: 8px; margin: 16px 0; background: var(--sf); padding: 6px; border-radius: 12px; box-shadow: 0 1px 2px rgba(0,0,0,0.05); overflow-x: auto;}
.tabs button { background: transparent; color: var(--mu); border: none; border-radius: 8px; box-shadow: none; white-space: nowrap; padding: 10px 16px;}
.tabs button:hover { background: var(--bg); color: var(--tx); transform: none;}
.tabs button.on { background: var(--pr); color: #fff; }

.mu { color: var(--mu); font-size: 0.9rem; }
.code { font-size: 2rem; font-weight: 800; letter-spacing: 0.1em; color: var(--pr); text-align: center; display: block; margin: 10px 0;}

.hero {
    display: flex; align-items: center; gap: 16px; padding: 24px;
    border-radius: 20px; color: #fff;
    background: linear-gradient(135deg, #064e3b 0%, #10b981 100%);
    box-shadow: 0 10px 15px -3px rgba(16, 185, 129, 0.3); margin-bottom: 20px;
}
.hero .ic { font-size: 2.5rem; line-height: 1; }
.hero h1 { margin: 0; color: #fff; font-size: 1.6rem; }
.hero p { margin: 4px 0 0; opacity: 0.9; font-size: 0.95rem; }

.clock { position: sticky; top: env(safe-area-inset-top, 10px); z-index: 5; display: flex; justify-content: space-between; background: var(--sf); border: 2px solid var(--ln); border-radius: 12px; padding: 12px 20px; font-weight: 800; font-size: 1.2rem; box-shadow: var(--sh); margin-bottom: 20px;}
.clock.low { color: var(--no); border-color: var(--no); animation: pulse 1s infinite;}
@keyframes pulse { 0% { transform: scale(1); } 50% { transform: scale(1.02); } 100% { transform: scale(1); } }

.opt { display: block; width: 100%; text-align: left; margin: 10px 0; background: var(--bg); color: var(--tx); border: 2px solid transparent; padding: 16px; border-radius: 12px; font-weight: 500; font-size: 1rem; transition: all 0.2s;}
.opt:hover { background: var(--sf); border-color: var(--ln); transform: translateX(4px); box-shadow: none;}
.opt.ok { border-color: var(--ok); background: #d1fae5; color: #065f46; }
.opt.no { border-color: var(--no); background: #fee2e2; color: #991b1b; }

.q { font-size: 1.25rem; font-weight: 700; margin: 16px 0 24px; line-height: 1.5; color: var(--tx); }
.bar { display: flex; align-items: center; gap: 8px; margin: 6px 0; }
.bar i { display: block; height: 20px; background: var(--pr); border-radius: 10px; min-width: 4px; transition: width 0.5s; }

table { width: 100%; border-collapse: separate; border-spacing: 0; font-size: 0.95rem; margin-top: 10px; }
th, td { border-bottom: 1px solid var(--ln); padding: 12px; text-align: left; }
th { background: #f9fafb; color: var(--mu); font-weight: 600; text-transform: uppercase; font-size: 0.8rem; letter-spacing: 0.05em; }
tr:last-child td { border-bottom: none; }
.wrap { overflow-x: auto; border: 1px solid var(--ln); border-radius: 12px; background: var(--sf); }
td input { width: 70px; padding: 6px; }
.err { color: var(--no); font-weight: 600; }
.ok { color: var(--ok); font-weight: 600; }
.lst { max-height: 250px; overflow: auto; border: 1px solid var(--ln); border-radius: 10px; padding: 10px; background: var(--bg);}
.lst label { font-weight: 500; margin: 6px 0; display: flex; align-items: center;}

a.lk-btn { display: inline-block; padding: 10px 16px; border-radius: 10px; border: 1.5px solid var(--pr); font-weight: 600; text-decoration: none; color: var(--pr); transition: 0.2s;}
a.lk-btn:hover { background: var(--pr); color: #fff;}
.qrbox { display: flex; justify-content: center; background: #fff; padding: 20px; border-radius: 16px; border: 2px dashed var(--ln); margin: 16px 0; }
</style></head><body><main id="app"><p class="mu" style="text-align:center; margin-top:50px;">Đang tải hệ thống...</p></main>
<script>
//
