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
// =========================================================================
// 1. THẦY ĐIỀN THÔNG TIN SUPABASE CỦA THẦY VÀO ĐÂY (Project URL và API Key)
// =========================================================================
const CFG = {
    url: 'https://ctketefxmqmbghyknnvg.supabase.co',
    key: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImN0a2V0ZWZ4bXFtYmdoeWtubnZnIiwicm9sZSI6ImFub24iLCJpYXQiOjE3OTMzNDYyOTQsImV4cCI6MjEwODkyMjI5NH0.j1pwyRvDNIQAzvszg6bkwxU-wroyYVppRcdvgo8mHeA'
};
// =========================================================================


// --- CẤU TRÚC BÀI HỌC GDQP&AN ---
const LES_10=["Bài 1. Lịch sử, truyền thống của lực lượng vũ trang nhân dân Việt Nam","Bài 2. Nội dung cơ bản một số luật về quốc phòng và an ninh Việt Nam","Bài 3. Ma túy, tác hại của ma túy","Bài 4. Phòng, chống vi phạm pháp luật về trật tự an toàn giao thông","Bài 5. Bảo vệ an ninh quốc gia và bảo đảm trật tự, an toàn xã hội","Bài 6. Một số hiểu biết về an ninh mạng","Bài 7. Thường thức phòng tránh một số loại bom, mìn, đạn, vũ khí hỏa công","Bài 8. Đội ngũ từng người không có súng","Bài 9. Đội ngũ tiểu đội","Bài 10. Đội ngũ trung đội","Bài 11. Các tư thế, động tác cơ bản vận động trong chiến đấu","Bài 12. Kỹ thuật cấp cứu và chuyển thương"];
const LES_11=["Bài 1. Bảo vệ chủ quyền lãnh thổ, biên giới quốc gia","Bài 2. Luật nghĩa vụ quân sự và trách nhiệm của học sinh","Bài 3. Phòng chống tệ nạn xã hội ở Việt Nam","Bài 4. Một số vấn đề về vi phạm pháp luật bảo vệ môi trường","Bài 5. Kiến thức cơ bản về phòng không nhân dân","Bài 6. Giới thiệu súng tiểu liên AK và súng trường CKC","Bài 7. Kỹ thuật bắn súng tiểu liên AK và súng trường CKC","Bài 8. Kỹ thuật sử dụng lựu đạn","Bài 9. Chiến thuật bộ binh","Bài 10. Kỹ thuật băng bó cứu thương"];
const LES_12=["Bài 1. Bảo vệ an ninh quốc gia","Bài 2. Một số hiểu biết về nền quốc phòng toàn dân","Bài 3. Tổ chức quân đội và công an nhân dân","Bài 4. Nhà trường quân đội, công an","Bài 5. Luật sĩ quan quân đội","Bài 6. Các tư thế vận động trên chiến trường","Bài 7. Lợi dụng địa hình địa vật","Bài 8. Công tác phòng không nhân dân"];
const LES_MAP={"10":LES_10, "11":LES_11, "12":LES_12};

const LV={nb:"Nhận biết",th:"Thông hiểu",vd:"Vận dụng"},GT={mc:"Trắc nghiệm nhanh",tf:"Đúng – Sai nhanh",voice:"Trả lời bằng giọng nói",fill:"Điền khuyết",scr:"Xếp chữ giải mã thuật ngữ",match:"Ghép đôi khái niệm – mô tả",order:"Sắp xếp thứ tự các bước"};
const S={},P={};let T=null;
const $=s=>document.querySelector(s),esc=s=>String(s??'').replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c])),A=$=>document.getElementById('app');
const norm=s=>String(s||'').toLowerCase().normalize('NFC').replace(/[^\p{L}\p{N} ]/gu,'').trim();
const fmt=s=>Math.floor(Math.max(s,0)/60)+':'+String(Math.max(s,0)%60).padStart(2,'0');
const rcode=p=>p+Math.random().toString(36).slice(2,7).toUpperCase();
const shuf=a=>{a=[...a];for(let i=a.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[a[i],a[j]]=[a[j],a[i]]}return a};
const keys=k=>(k||[]).map(norm).filter(Boolean);
const say=t=>{try{const u=new SpeechSynthesisUtterance(t);u.lang='vi-VN';speechSynthesis.cancel();speechSynthesis.speak(u)}catch(e){}};

let SB;
const col=n=>({
 doc:id=>({
  async get(){const q=n=='config'?SB.from('roster').select('names').eq('id',1):SB.from(n).select('data').eq(n=='results'?'id':'code',id);
   const{data,error}=await q.maybeSingle();if(error)throw error;return{exists:!!data,data:()=>n=='config'?data:data.data}},
  async set(o){const row=n=='config'?{id:1,names:o.names}:n=='results'?{id,code:o.code,data:o}:{code:id,data:o};
   const{error}=await(n=='results'?SB.from(n).insert(row):SB.from(n=='config'?'roster':n).upsert(row));if(error&&error.code!='23505')throw error}}),
 where:(f,op,v)=>({async get(){const{data,error}=await SB.from(n).select('data').eq(f,v);if(error)throw error;return{docs:(data||[]).map(r=>({data:()=>r.data}))}}}),
 async get(){const{data,error}=await SB.from(n).select('data');if(error)throw error;return{docs:(data||[]).map(r=>({data:()=>r.data}))}}});
const cv=x=>'"'+String(x||'').replace(/^[=+\-@]/,"'$&").replace(/"/g,'""')+'"';
const dl=(f,d)=>{const u=URL.createObjectURL(new Blob([d],{type:/\.csv$/.test(f)?'text/csv;charset=utf-8':/\.doc$/.test(f)?'application/msword':'text/plain;charset=utf-8'})),a=document.createElement('a');a.href=u;a.download=f;a.click();setTimeout(()=>URL.revokeObjectURL(u),4000)};
const isAdmin=async()=>{try{const{data}=await SB.from('admins').select('uid').limit(1).maybeSingle();return !!data}catch(e){return false}};
async function boot(){
 if(CFG.url.includes('THAY_URL_CUA_THAY_VAO_DAY')){A().innerHTML='<div class="card"><h1>Chưa cấu hình Supabase</h1><p>Mở file index.html, tìm phần CẤU HÌNH SUPABASE (ở dòng 120) và điền Link + Key của thầy vào.</p></div>';return}
 if(!window.supabase){A().innerHTML='<div class="card"><p class="err">Không tải được thư viện Supabase. Kiểm tra mạng rồi tải lại trang.</p></div>';return}SB=supabase.createClient(CFG.url,CFG.key);S.db=true;
 const h=location.hash.slice(1).toUpperCase(),{data:{session}}=await SB.auth.getSession();
 if(session&&!session.user.is_anonymous&&!h&&await isAdmin()){S.owner=true;return teacher()}
 if(h)return enter(h);landing()}

function landing(){A().innerHTML=`<div class="hero"><span class="ic">🪖</span><div><h1>Trợ lý AI - GDQP&AN</h1><p>Trò chơi & kiểm tra trực tuyến</p></div></div><div class="card"><h2>Học sinh</h2><label>Mã tham gia</label><input id="lc" autocomplete="off" placeholder="Nhập mã giáo viên cung cấp"><p><button onclick="enter($('#lc').value.trim().toUpperCase())" style="width:100%">Vào Học Ngay 🚀</button></p></div><div class="card"><h2>Quản trị (Giáo viên)</h2><label>Email</label><input id="ae" type="email" autocomplete="username"><label>Mật khẩu</label><input id="ap" type="password" autocomplete="current-password"><p><button onclick="adminLogin()">Đăng nhập Hệ thống</button> <span id="am" class="err"></span></p></div>`}
async function adminLogin(){const{error}=await SB.auth.signInWithPassword({email:$('#ae').value.trim(),password:$('#ap').value});if(error)return $('#am').textContent='Sai email hoặc mật khẩu';if(!await isAdmin()){await SB.auth.signOut();return $('#am').textContent='Tài khoản không có quyền quản trị'}S.owner=true;teacher()}
async function enter(code){if(!code)return;const{data:{session}}=await SB.auth.getSession();if(!session){const{error}=await SB.auth.signInAnonymously();if(error){A().innerHTML='<div class="card"><p class="err">Không đăng nhập được: '+esc(error.message)+'</p></div>';return}}student(code)}

/* ---------- GIÁO VIÊN ---------- */
function teacher(){
 A().innerHTML=`<div class="hero"><span class="ic">🪖</span><div><h1>Bảng điều khiển Giáo viên</h1><p>Môn GDQP&AN · AI tạo đề thi bám sát tài liệu & SGK</p></div></div><button class="danger" style="float:right; margin-top:-70px; position:relative; z-index:10;" onclick="SB.auth.signOut().then(()=>location.reload())">Đăng xuất</button>
 <div class="tabs"><button id="t-g" onclick="tab('g')">🎮 Trò chơi</button><button id="t-t" onclick="tab('t')">📝 Đề kiểm tra</button><button id="t-r" onclick="tab('r')">📊 Kết quả</button><button id="t-d" onclick="tab('d')">📚 Thư viện SGK</button></div>
 <div id="pane"></div>`;
 loadDocs().catch(()=>{}).then(()=>tab('g'));
}
function tab(t){['g','t','r','d'].forEach(x=>$('#t-'+x).className=x==t?'on':'');
 const base=`<label>Link trang này (dùng tạo mã QR)</label><input id="base" value="${esc((()=>{try{return localStorage.base}catch(e){}})()||location.href.split('#')[0])}">`;
 const gr=`<div class="row"><div><label>Khối</label><select id="gr" onchange="gch()"><option selected>10</option><option>11</option><option>12</option></select></div></div>`;
 if(t=='g')$('#pane').innerHTML=`<div class="card"><h2>Tạo trò chơi tương tác (Khởi động)</h2>${gr}
 <label>Bài dạy</label><select id="gl"></select><input id="gl2" style="display:none" placeholder="Nhập tên bài (chưa có SGK khối này trong tài liệu)">
 <label>Hình thức</label><select id="gm" onchange="gmch()"><option value="ca">Cá nhân (1 trò chơi)</option><option value="nhom">Nhóm thi đấu (nhiều trò chơi)</option></select>
 <label>Loại Trò chơi</label><div id="gt">${Object.entries(GT).map(([k,v],i)=>`<label><input type="radio" name="gt" value="${k}" ${i?'':'checked'}> ${v}</label>`).join('')}</div>
 <div class="row"><div><label>Số nhóm (nếu chơi nhóm)</label><input id="gn" type="number" value="4" min="2" max="12"></div><div><label>Thời gian (phút)</label><input id="gx" type="number" value="5" min="1"></div><div><label>Số câu hỏi</label><input id="gq" type="number" value="5" min="3" max="10"></div></div><label>Tài liệu đính kèm (tùy chọn)</label><select id="src"><option value="">— Không dùng —</option></select><p id="lh" class="mu"></p><label>Liên kết (Video/Tài liệu tham khảo)</label><textarea id="lk" rows="2" placeholder="Tên Link | https://..."></textarea>${base}
 <p><button onclick="mkGame()" id="gb">✨ Sinh Trò Chơi bằng AI</button></p><div id="share"></div></div>`;
 
 if(t=='t')$('#pane').innerHTML=`<div class="card"><h2>Tạo đề kiểm tra / trắc nghiệm</h2>${gr}
 <label>Ma trận đề mẫu</label><select id="pm" onchange="pre()"><option value="">Tùy chọn tự do</option><option value="a">Kiểm tra Thường xuyên – 20 phút</option><option value="b">Kiểm tra Giữa kỳ – 45 phút</option><option value="c">Kiểm tra Cuối kỳ – 45 phút</option></select>
 <label>Phạm vi kiến thức (Chọn 1 hoặc nhiều bài)</label><div class="lst" id="tl" onchange="mtx()"></div><input id="tl2" oninput="mtx()" style="display:none" placeholder="Nhập tên các bài...">
 <h2>Ma trận cấu trúc (Theo mức độ)</h2><div id="mx"></div><p id="mt" class="mu"></p><div class="row"><div><label>Thời gian (phút)</label><input id="tm" type="number" value="45" min="5"></div></div><label>Tài liệu đính kèm (tùy chọn)</label><select id="src"><option value="">— Không dùng —</option></select><p id="lh" class="mu"></p><label>Liên kết</label><textarea id="lk" rows="2"></textarea>${base}
 <p><button onclick="mkTest()" id="tb">✨ AI Xây Dựng Đề Thi</button></p><div id="share"></div></div>`;
 
 if(t=='t')mtx();if(t=='g'||t=='t'){renderLes();fillSrc()}if(t=='d')docsTab();if(t=='r'){$('#pane').innerHTML='<div class="card"><h2>Bảng điểm & Thống kê</h2><label>Chọn lớp / Mã đề</label><select id="rc" onchange="loadRes()"><option value="">Đang tải dữ liệu…</option></select><div id="rs"></div></div>';codes()}
}
const gch=()=>{renderLes();window.mtx&&mtx()};
function gmch(){const g=$('#gm').value=='nhom';$('#gt').innerHTML=Object.entries(GT).map(([k,v],i)=>`<label><input type="${g?'checkbox':'radio'}" name="gt" value="${k}" ${g||!i?'checked':''}> ${v}</label>`).join('')}
const TY={mc:'Trắc nghiệm (4 đáp án)',tf:'Đúng – sai',sa:'Trả lời ngắn',es:'Tự luận'};
function selLes(){const c=[...document.querySelectorAll('#tl input:checked')];if(LI.length)return c.map(x=>({id:LI[+x.value].id,n:LI[+x.value].n,doc:LI[+x.value].doc}));const v=$('#tl2').value.trim();return v?[{id:'x',n:v}]:[]}
function mtx(){if(!$('#mx'))return;const old={};document.querySelectorAll('#mx input').forEach(i=>old[i.id]=i.value);const L=selLes();
 $('#mx').innerHTML=L.length?L.map(l=>`<div class="card" style="margin:8px 0; border-left:4px solid var(--pr);"><b>${esc(l.n)}</b><div class="wrap"><table><tr><th>Dạng câu hỏi</th>${Object.values(LV).map(v=>`<th>${v}</th>`).join('')}<th>Tổng</th></tr>${Object.entries(TY).map(([t,tn])=>`<tr><td>${tn}</td>${Object.keys(LV).map(k=>{const id=`m_${l.id}_${t}_${k}`;return `<td><input id="${id}" type="number" min="0" value="${old[id]||0}" oninput="msum()"></td>`}).join('')}<td class="rs" style="font-weight:bold; color:var(--pr);">0</td></tr>`).join('')}</table></div></div>`).join(''):'<p class="mu">Vui lòng tick chọn ít nhất 1 bài để cấu hình ma trận.</p>';msum()}
function msum(){let tot=0;document.querySelectorAll('#mx tr').forEach(tr=>{const i=tr.querySelectorAll('input');if(!i.length)return;const s=[...i].reduce((a,b)=>a+(+b.value||0),0);tr.querySelector('.rs').textContent=s;tot+=s});$('#mt').innerHTML=`<b>Tổng số câu trong đề: <span style="font-size:1.2rem; color:var(--pr);">${tot}</span> câu</b>`}
function pre(){const m={a:{t:[8,1,2,0],l:[40,30,30],m:20},b:{t:[12,2,3,1],l:[40,30,30],m:45},c:{t:[12,2,3,1],l:[30,40,30],m:45}}[$('#pm').value];if(!m)return;const L=selLes();if(!L.length){$('#mt').textContent='Hãy chọn bài trước, rồi chọn lại ma trận mẫu.';return}
 $('#tm').value=m.m;document.querySelectorAll('#mx input').forEach(i=>i.value=0);let r=0;
 Object.keys(TY).forEach((t,ti)=>{const n=m.t[ti],lv=m.l.map(p=>Math.round(n*p/100));lv[0]+=n-lv.reduce((a,b)=>a+b,0);['nb','th','vd'].forEach((k,ki)=>{for(let c=0;c<lv[ki];c++){const l=L[r++%L.length],e=$(`#m_${l.id}_${t}_${k}`);e.value=+e.value+1}})});msum()}
function share(code,extra=''){const b=$('#base').value.replace(/#.*/,'');try{localStorage.base=b}catch(e){}const u=b+'#'+code;
 $('#share').innerHTML=`<div class="card" style="border: 2px solid var(--pr); background:#f0fdf4;"><h2>✅ Khởi tạo thành công!</h2><p>Mã Code: <span class="code">${code}</span></p><input readonly value="${esc(u)}" onclick="this.select()"><div id="qr" class="qrbox"></div>${extra}<p class="mu">Học sinh quét mã QR hoặc truy cập link trên để làm bài.</p></div>`;
 try{new QRCode($('#qr'),{text:u,width:180,height:180})}catch(e){}}

async function ai(p){const body={prompt:p+await srcText()};let last='';
 for(let k=0;k<4;k++){const{data,error}=await SB.functions.invoke('generate',{body});const msg=error?await fe(error):(data&&data.error)||'';
  if(!msg){let d=data;if(typeof d=='string'){try{d=JSON.parse(d.replace(/```json|```/g,'').trim())}catch(e){throw new Error('AI trả về sai định dạng, hãy thử lại')}}return d}
  last=String(msg);if(!/high demand|overload|unavailable|503|429|quota|rate/i.test(last))break;
  const b=$('#gb')||$('#tb');if(b)b.textContent='AI đang xử lý, vui lòng chờ '+(k+2)+'…';await new Promise(r=>setTimeout(r,3000*(k+1)))}
 throw new Error(/high demand|overload|unavailable|503/i.test(last)?'Máy chủ AI đang quá tải. Đã tự thử lại nhiều lần, hãy đợi 1–2 phút rồi bấm lại.':last)}
async function mkGame(){
 const b=$('#gb');b.disabled=true;b.textContent='✨ AI đang soạn nội dung...';
 try{const grade=$('#gr').value,les=LI.length?LI[+$('#gl').value].n:$('#gl2').value,mode=$('#gm').value,types=[...document.querySelectorAll('[name=gt]:checked')].map(x=>x.value),n=+$('#gq').value;
 if(!les||!types.length)throw{message:'Hãy chọn bài và loại trò chơi'};
 const q=await ai(`Bạn là giáo viên chuyên môn Giáo dục Quốc phòng và An ninh THPT. Soạn câu hỏi trò chơi Khởi động môn GDQP&AN lớp ${grade}, bài: ${les}. Bám sát thuật ngữ quân sự, pháp luật và SGK hiện hành. Chỉ trả JSON dạng {"mc":[{"q":"","o":["A","B","C","D"],"a":0}],"tf":[{"q":"","a":true}],"voice":[{"q":"câu hỏi ngắn có đáp án là một thuật ngữ","k":["thuật ngữ chấp nhận được"]}],"fill":[{"q":"câu có chỗ trống ____","k":["đáp án"]}],"scr":[{"q":"gợi ý nghĩa của từ","k":["TỪ KHOÁ không quá 12 chữ cái"]}],"match":[{"q":"Ghép khái niệm với mô tả","p":[["khái niệm","mô tả ngắn"]]}],"order":[{"q":"Sắp xếp các bước thực hành/động tác","s":["bước 1","bước 2","bước 3","bước 4"]}]}. Mỗi loại ${n} câu cho các loại: ${types.join(', ')} (riêng match và order mỗi câu có đúng 4 mục); loại khác để mảng rỗng. a của mc là chỉ số 0-3.`);
 if(!q||typeof q!='object'||Array.isArray(q))throw{message:'AI trả về sai định dạng, hãy thử lại'};const ng=mode=='nhom'?+$('#gn').value:0;
 const code=rcode('G');await col('games').doc(code).set({code,grade,les,mode,types,qs:q,ng,time:+$('#gx').value,links:getLinks(),at:Date.now()});share(code)}
 catch(e){$('#share').innerHTML='<p class="err">Không tạo được: '+esc(e.message||e.code)+'</p>'}
 b.disabled=false;b.textContent='✨ Sinh Trò Chơi bằng AI'}
 
async function mkTest(){
 const b=$('#tb');b.disabled=true;b.textContent='✨ AI đang thiết kế đề...';
 try{const grade=$('#gr').value,LL=selLes(),les=LL.map(l=>l.n).join('; ');if(!les)throw{message:'Hãy chọn bài học'};
 let spec='',total=0;LL.forEach(l=>{const parts=[];Object.keys(TY).forEach(t=>Object.keys(LV).forEach(k=>{const n=+$(`#m_${l.id}_${t}_${k}`).value||0;if(n){parts.push(`${n} câu t=${t} l=${k}`);total+=n}}));if(parts.length)spec+=`[${l.n}: ${parts.join(', ')}] `});if(!total)throw{message:'Hãy nhập số lượng câu hỏi vào ma trận'};
 const qs=await ai(`Bạn là giáo viên chuyên môn Giáo dục Quốc phòng và An ninh THPT. Ra đề kiểm tra môn GDQP&AN lớp ${grade} cho các bài: ${les}. Sử dụng đúng thuật ngữ quân sự, kỹ thuật chiến đấu bộ binh, và điều lệnh quản lý bộ đội. Phải sinh ĐÚNG số câu sau cho từng bài (t: mc = nhiều lựa chọn, tf = đúng-sai mỗi câu 4 mệnh đề, sa = trả lời ngắn, es = tự luận; l: nb/th/vd = nhận biết/thông hiểu/vận dụng): ${spec}. Mỗi câu có thêm trường "b" là tên bài. Chỉ trả JSON là mảng, mỗi phần tử: mc {"t":"mc","l":"nb|th|vd","q":"","o":["","","",""],"a":0}; tf {"t":"tf","l":"","q":"ngữ cảnh","s":[{"x":"mệnh đề","a":true}]}; sa {"t":"sa","l":"","q":"","k":["đáp án chấp nhận được"]}; es {"t":"es","l":"","q":"","k":["ý/từ khoá chấm điểm"]}. Xếp theo thứ tự mc, tf, sa, es.`);
 if(!Array.isArray(qs))throw{message:'AI trả về sai định dạng, hãy thử lại'};
 const code=rcode('T'),time=+$('#tm').value;await col('tests').doc(code).set({code,grade,les,time,qs,links:getLinks(),at:Date.now()});
 window.LAST={code,grade,les,time,qs};share(code,'<p><button onclick="dlDoc()">📄 Xuất đề + Đáp án (Word)</button> <button class="alt" onclick="dlTest()">Tải dạng .txt</button></p>')}
 catch(e){$('#share').innerHTML='<p class="err">Lỗi tạo đề: '+esc(e.message||e.code)+'</p>'}
 b.disabled=false;b.textContent='✨ AI Xây Dựng Đề Thi'}

function txtTest(d){let i=0;return `ĐỀ KIỂM TRA GDQP&AN ${d.grade||''}\nNội dung: ${d.les}\nThời gian: ${d.time} phút\n\n`+d.qs.map(q=>{i++;let s=`Câu ${i} (${LV[q.l]||''}): ${q.q}\n`;if(q.t=='mc')s+=q.o.map((o,j)=>' '+'ABCD'[j]+'. '+o).join('\n')+'\n';if(q.t=='tf')s+=q.s.map((m,j)=>' '+'abcd'[j]+') '+m.x).join('\n')+'\n';return s}).join('\n')+'\n--- ĐÁP ÁN ---\n'+d.qs.map((q,i)=>`Câu ${i+1}: `+(q.t=='mc'?'ABCD'[q.a]:q.t=='tf'?q.s.map(m=>m.a?'Đ':'S').join(' '):(q.k||[]).join(' / '))).join('\n')}
async function dlTest(){dl('de-kiem-tra-gdqp-'+LAST.code+'.txt',txtTest(LAST))}
const aTxt=q=>q.t=='mc'?'ABCD'[q.a]:q.t=='tf'?q.s.map((m,j)=>'abcd'[j]+'-'+(m.a?'Đ':'S')).join(', '):(q.k||[]).join(' / ');
function wordTest(d){let i=0;const body=d.qs.map(q=>{i++;let s=`<p><b>Câu ${i}.</b> <i>(${LV[q.l]||''})</i> ${esc(q.q)}</p>`;
 if(q.t=='mc')s+=q.o.map((o,j)=>`<p class="o">${'ABCD'[j]}. ${esc(o)}</p>`).join('');
 if(q.t=='tf')s+=q.s.map((m,j)=>`<p class="o">${'abcd'[j]}) ${esc(m.x)}</p>`).join('');
 if(q.t=='sa')s+='<p class="o">Trả lời: ……………………………………</p>';
 if(q.t=='es')s+='<p class="o">……………………………………………………………………………</p><p class="o">……………………………………………………………………………</p>';
 return s}).join('');
 const ans=d.qs.map((q,k)=>`<tr><td>${k+1}</td><td>${esc(aTxt(q))}</td></tr>`).join('');
 return `<html xmlns:o="urn:schemas-microsoft-com:office:office"><head><meta charset="utf-8"><style>body{font-family:'Times New Roman';font-size:13pt}h1{text-align:center;font-size:16pt}.o{margin:0 0 0 28pt}td,th{border:1px solid #000;padding:4pt}table{border-collapse:collapse}</style></head><body><h1>ĐỀ KIỂM TRA MÔN GDQP&AN ${esc(d.grade||'')}</h1><p style="text-align:center">Nội dung: ${esc(d.les)}<br>Thời gian: ${esc(d.time)} phút · Họ và tên: ………………………… Lớp: ………</p>${body}<br style="page-break-before:always" clear="all"><h1>ĐÁP ÁN</h1><table><tr><th>Câu</th><th>Đáp án</th></tr>${ans}</table></body></html>`}
const dlDoc=()=>dl('de-kiem-tra-gdqp-'+LAST.code+'.doc','\ufeff'+wordTest(LAST));
async function delRows(q,msg){if(!confirm(msg))return false;const{data,error}=await q.select('id');if(error){alert('Không xóa được: '+error.message);return false}if(!data||!data.length){alert('Lỗi quyền Xóa trên Supabase.');return false}return true}
async function delCode(c){const t=c[0]=='T'?'tests':'games';if(!confirm('Xóa HẲN mã '+c+'? Không thể hoàn tác.'))return;
 const a=await SB.from('results').delete().eq('code',c).select('id');
 const b=await SB.from(t).delete().eq('code',c).select('code');
 $('#rs').innerHTML='<p class="ok">Đã xóa thành công mã '+esc(c)+'.</p>';codes()}
async function delAll(c){if(await delRows(SB.from('results').delete().eq('code',c),'Xóa TOÀN BỘ kết quả của mã '+c+'?'))loadRes()}
async function delOne(i){const r=RS[i];if(r&&await delRows(SB.from('results').delete().eq('id',r._id),'Xóa kết quả của '+r.name+'?'))loadRes()}
async function codes(){const a=[...(await col('tests').get()).docs,...(await col('games').get()).docs].map(d=>d.data()).sort((x,y)=>y.at-x.at);
 $('#rc').innerHTML='<option value="">— Chọn mã bài tập —</option>'+a.map(d=>`<option value="${esc(d.code)}">${esc(d.code)} · ${esc(String(d.les||'').slice(0,40))}</option>`).join('')}
const getLinks=()=>($('#lk').value||'').split('\n').map(s=>{const p=s.split('|'),u=(p.length>1?p.slice(1).join('|'):p[0]).trim();return{n:p.length>1?p[0].trim()||u:u,u}}).filter(x=>/^https:\/\//i.test(x.u));
const linkBox=()=>(P.d.links||[]).length?'<h2>Liên kết học tập</h2>'+P.d.links.filter(l=>/^https:\/\//i.test(l.u)).map(l=>`<p><a href="${esc(l.u)}" target="_blank" class="lk-btn">${esc(l.n)} ↗</a></p>`).join(''):'';
const cm=s=>s>=8?'Giỏi: Đạt yêu cầu thực hành và lý thuyết tốt.':s>=6.5?'Khá: Nắm vững kiến thức, cần chú ý thuật ngữ quân sự.':s>=5?'Trung bình: Ôn tập thêm động tác và luật.':'Yếu: Cần bồi dưỡng thêm kiến thức cơ bản.';
async function loadRes(){const c=$('#rc').value;if(!c)return;const{data:rows,error:qe}=await SB.from('results').select('id,data').eq('code',c);if(qe){$('#rs').innerHTML='<p class="err">'+esc(qe.message)+'</p>';return}const rs=(rows||[]).map(r=>({...r.data,_id:r.id}));
 if(!rs.length){$('#rs').innerHTML='<p class="mu">Chưa có học sinh nộp bài.</p><p><button class="danger" onclick="delCode(\''+esc(c)+'\')">🗑 Xóa mã này</button></p>';return}
 rs.forEach(r=>r.score=Math.max(0,Math.min(10,+r.score||0)));const sc=rs.map(r=>r.score),avg=sc.reduce((a,b)=>a+b,0)/sc.length;
 $('#rs').innerHTML=`<div class="card" style="background:#f8fafc;"><p>Sĩ số: <b>${rs.length}</b> · Điểm TB: <b>${avg.toFixed(2)}</b> · Cao nhất: <b>${Math.max(...sc)}</b> · Thấp nhất: <b>${Math.min(...sc)}</b></p></div>
 <div class="wrap"><table><tr><th>Học sinh</th><th>Lớp</th><th>Nhóm</th><th>Điểm</th><th>Nhận xét</th><th></th></tr>${rs.sort((a,b)=>b.score-a.score).map((r,i)=>`<tr><td><b>${esc(r.name)}</b></td><td>${esc(r.cls||'')}</td><td>${esc(r.group||'')}</td><td style="font-weight:bold; color:var(--pr);">${r.score}</td><td>${r.kind=='test'?cm(r.score):''}</td><td><button class="danger" onclick="delOne(${i})">Xóa</button></td></tr>`).join('')}</table></div>
 <p style="margin-top:20px;"><button class="alt" onclick='dlCsv(${JSON.stringify(c)})'>Tải bảng điểm (.csv)</button> <button class="danger" onclick='delAll(${JSON.stringify(c)})'>🗑 Xóa hết kết quả</button></p>`;window.RS=rs}
async function dlCsv(c){dl('diem-gdqp-'+c+'.csv','\ufeffHọ tên,Lớp,Nhóm,Điểm\n'+RS.map(r=>[cv(r.name),cv(r.cls),cv(r.group),r.score].join(',')).join('\n'))}

let LDOCS=[],LI=[],DC={},PF=null;
const fe=async e=>{try{return (await e.context.json()).error||e.message}catch(_){return e.message}};
const GH={o:'',r:''}; 
const sgkRepo=()=>{if(GH.o)return GH;const h=location.hostname;return h.endsWith('.github.io')?{o:h.split('.')[0],r:(p=>p&&!/\.html?$/i.test(p)?p:h)(location.pathname.split('/')[1]||'')}:null};
const ghUrl=(k,p)=>{const g=sgkRepo();return g?`https://github.com/${g.o}/${g.r}/${k}/main/${encodeURI(p)}`:'#'};
const slug=x=>x.normalize('NFD').replace(/[\u0300-\u036f]/g,'').replace(/đ/g,'d').replace(/Đ/g,'D').toLowerCase().replace(/[^a-z0-9]+/g,'-').replace(/^-|-$/g,'');
let DSRC='',DERR='';
const ext=n=>(n.match(/\.[^.]+$/)||[''])[0].toLowerCase(),nice=n=>n.replace(/\.[^.]+$/,'').replace(/[-_]+/g,' ');

function splitMdIntoLessons(text, filePath, grade, defaultTitle, url) {
 if(!text) return [{title: defaultTitle, grade, kind:'md', path: filePath, url}];
 const lines = text.split('\n');
 const regex = /^#{1,4}\s*(?:\*\*)?\s*(BÀI\s+\d+|Bài\s+\d+)\s*[\.:\-–—]?\s*(.*?)(?:\*\*)?\s*$/i;
 const sections = [];
 let curTitle = '', curLines = [];
 for(let line of lines) {
  const m = line.trim().match(regex);
  if(m) {
   if(curTitle && curLines.length) sections.push({title: curTitle, content: curLines.join('\n')});
   curTitle = `${m[1].replace(/BÀI/i,'Bài')}: ${m[2].trim()}`; curLines = [line];
  } else { if(curTitle) curLines.push(line); }
 }
 if(curTitle && curLines.length) sections.push({title: curTitle, content: curLines.join('\n')});
 if(!sections.length) { DC[filePath] = text; return [{title: defaultTitle, grade, kind:'md', path: filePath, rawPath: filePath, url}]; }
 return sections.map((s, idx) => { const subPath = `${filePath}#sec_${idx + 1}`; DC[subPath] = s.content; return {title: s.title, grade, kind: 'md', path: subPath, rawPath: filePath, url }; });
}

async function loadDocs(force){LDOCS=[];DC={};DSRC='';DERR='';const g=sgkRepo();
 try{
  if(!g)throw new Error('Không nhận ra kho GitHub');
  const res=await Promise.all(['10','11','12'].map(async k=>{const r=await fetch(`https://api.github.com/repos/${g.o}/${g.r}/contents/sgk/khoi-${k}`);if(r.status==404)return[];if(!r.ok)throw new Error('GitHub API Lỗi');return(await r.json()).map(f=>({...f,k}))}));
  const files=res.flat().filter(f=>f.type=='file'&&!/^readme/i.test(f.name)&&!f.name.startsWith('.')),U=Object.fromEntries(files.map(f=>[f.path,f.download_url]));
  const es=await Promise.all(files.map(async f=>{const x=ext(f.name),stem=f.path.slice(0,f.path.length-x.length);
   if(x=='.md'||x=='.txt'){
    let t='';try{t=await(await fetch(f.download_url)).text()}catch(e){}
    DC[f.path]=t; const m=t.match(/^#\s+(.+)$/m); const defTitle = m?m[1].trim():nice(f.name);
    return splitMdIntoLessons(t, f.path, f.k, defTitle, f.download_url);
   }
   if(x=='.pdf'&&!U[stem+'.md']&&!U[stem+'.txt'])return [{title:nice(f.name),grade:f.k,kind:'pdf',path:f.path,url:f.download_url}];
   return [];
  }));
  LDOCS=es.flat().filter(Boolean); DSRC='GitHub';
 }catch(e){DERR=e.message||String(e);}}
function dstat(){const e=$('#dstat');if(e)e.innerHTML=`Trạng thái thư viện: <b>${LDOCS.length}</b> tài liệu hiện có${DERR?' · <span class="err">'+esc(DERR)+'</span>':''}`}
function lhint(g){const h=$('#lh');if(!h)return;const n=LDOCS.filter(d=>d.grade==g).length;h.innerHTML=n?`<span style="color:var(--pr)">Khối ${g}: Đã tải ${n} bài học từ Thư Viện SGK.</span>`:`Khối ${g}: Dùng danh mục dự phòng.`}

function lessonItems(g){
 const it=LDOCS.filter(d=>d.grade==g).sort((a,b)=>String(a.title).localeCompare(String(b.title),'vi',{numeric:true})).map((d,i)=>({id:'d_'+g+'_'+i,n:d.title,doc:d.path}));
 const defs=LES_MAP[g]||[];
 if(!it.length) defs.forEach((n,i)=>it.push({id:`def_${g}_${i}`,n,doc:''}));
 return it;
}
function renderLes(){if(!$('#gr'))return;const g=$('#gr').value;LI=lessonItems(g);lhint(g);
 const gl=$('#gl');if(gl)gl.innerHTML=LI.map((x,i)=>`<option value="${i}">${esc(x.n)}</option>`).join('');
 const tl=$('#tl');if(tl)tl.innerHTML=LI.map((x,i)=>`<label><input type="checkbox" value="${i}"> ${esc(x.n)}</label>`).join('');
 const none=!LI.length;[['gl','gl2'],['tl','tl2']].forEach(([a,b])=>{$('#'+a)&&($('#'+a).style.display=none?'none':'');$('#'+b)&&($('#'+b).style.display=none?'':'none')})}
function fillSrc(){const s=$('#src');if(!s)return;s.innerHTML='<option value="">— Không dùng —</option>';LDOCS.forEach(d=>{const o=document.createElement('option');o.value=d.path;o.textContent=`${d.title} (Khối ${d.grade})`;s.appendChild(o)})}
const pickDocs=()=>{
 const s=$('#src');if(s&&s.value)return[s.value];
 if($('#gl')&&LI[+$('#gl').value]&&LI[+$('#gl').value].doc)return[LI[+$('#gl').value].doc];
 if($('#tl'))return selLes().map(l=>l.doc).filter(Boolean);
 return[];
};
async function loadPdfJs(){if(window.pdfjsLib)return;await new Promise((ok,no)=>{const x=document.createElement('script');x.src='https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js';x.onload=ok;x.onerror=()=>no(new Error('Lỗi mạng tải trình đọc PDF'));document.head.appendChild(x)});const w=await(await fetch('https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js')).text();pdfjsLib.GlobalWorkerOptions.workerSrc=URL.createObjectURL(new Blob([w],{type:'text/javascript'}))}
async function openPdf(f){await loadPdfJs();return pdfjsLib.getDocument({data:await f.arrayBuffer()}).promise}
async function pdfTextOf(f,a,b){const pdf=await openPdf(f);a=a||1;b=Math.min(b||pdf.numPages,pdf.numPages);let t='';for(let i=a;i<=b;i++){const c=await(await pdf.getPage(i)).getTextContent();t+=`\n\n## Trang ${i}\n`+c.items.map(y=>y.str).join(' ').trim()}return t.trim()}
async function docText(p){
 if(DC[p]!=null)return DC[p];
 const root=p.split('#')[0],d=LDOCS.find(x=>x.path==p)||{},u=d.url||root;let t='';
 try{
  if(/\.pdf$/i.test(root)){t=await pdfTextOf(await(await fetch(u)).blob(),1,200);if(t.replace(/## Trang \d+/g,'').trim().length<100)t=''}
  else{const r=await fetch(u);if(!r.ok)throw 0;const full=await r.text();
   if(p.includes('#sec_')){splitMdIntoLessons(full,root,d.grade,'',d.url);t=DC[p]||''}else t=full}
 }catch(e){t=''}
 if(t)DC[p]=t;return t}
async function srcText(){const ids=[...new Set(pickDocs().filter(Boolean))];if(!ids.length)return '';const parts=[];
 for(const p of ids){const t=await docText(p),d=LDOCS.find(x=>x.path==p)||{};if(t)parts.push(`### ${d.title||'Bài học'}\n${t.slice(0,Math.floor(24000/ids.length))}`);else throw new Error(`Tài liệu "${d.title||p}" rỗng.`)}
 const t=parts.join('\n\n').slice(0,24000);return '\n\nTÀI LIỆU SGK QUỐC PHÒNG:\n'+t}
function docsTab(){const g=sgkRepo();$('#pane').innerHTML=`<div class="card"><h2>Thư viện Số & Học liệu</h2><p class="mu">Kho tài liệu SGK GDQP&AN khối 10, 11, 12.</p><p>${[10,11,12].map(k=>`<a href="${ghUrl('upload','sgk/khoi-'+k)}" target="_blank" class="lk-btn">➕ Thêm tệp khối ${k}</a>`).join(' ')} <button class="alt" onclick="refreshDocs()" style="margin-left:10px;">↻ Cập nhật thư viện</button></p><p id="dstat" class="mu"></p><div id="dlist" class="wrap"></div></div><div class="card" id="dview" style="display:none"></div><div class="card">${toolForm()}</div>`;dlist()}
function dlist(){dstat();$('#dlist').innerHTML=LDOCS.length?`<table><tr><th>Tên Bài Giảng</th><th>Khối</th><th>Định Dạng</th><th>Thao Tác</th></tr>${LDOCS.map((d,i)=>`<tr><td><b>${esc(d.title)}</b></td><td>${esc(d.grade)}</td><td><span style="background:var(--pr); color:#fff; padding:2px 8px; border-radius:4px; font-size:12px;">${esc(d.kind).toUpperCase()}</span></td><td><button class="alt" onclick="viewDoc(${i})" style="padding:6px 12px; font-size:13px;">📖 Đọc</button></td></tr>`).join('')}</table>`:'<p class="mu" style="padding:16px;">Thư viện trống.</p>'}
async function refreshDocs(){$('#dlist').innerHTML='<p class="mu" style="padding:16px;">Đang đồng bộ dữ liệu…</p>';await loadDocs(true);dlist();renderLes();fillSrc()}
async function viewDoc(i){const d=LDOCS[i],v=$('#dview');v.style.display='';v.innerHTML='<p class="mu">Đang load nội dung sách…</p>';const t=await docText(d.path);v.innerHTML=`<h2>${esc(d.title)}</h2><textarea readonly rows="12" style="background:#f9fafb;">${esc(t)}</textarea>`;v.scrollIntoView()}
function toolForm(){return `<h2>Công cụ OCR: Đọc PDF & Số hóa SGK</h2><label>Upload tệp PDF/MD</label><input id="df" type="file" accept=".md,.txt,.pdf" onchange="pickFile(this.files[0])"><div class="row"><div><label>Từ trang</label><input id="p1" type="number" min="1" placeholder="1"></div><div><label>Đến trang</label><input id="p2" type="number" min="1" placeholder="Hết"></div></div><p style="margin-top:16px;"><button onclick="readFile()">📖 Phân tích Văn bản</button> <button class="alt" onclick="ocrFile()">🤖 Dùng AI Đọc (Dành cho PDF Scan)</button></p><label>Nội dung số hóa (Trích xuất thành công)</label><textarea id="dc" rows="8"></textarea><div class="row"><div><label>Tên File xuất ra</label><input id="ft"></div><div><label>Khối áp dụng</label><select id="fg"><option selected>10</option><option>11</option><option>12</option></select></div></div><p style="margin-top:16px;"><button onclick="dlMd()" style="background:#2563eb;">⬇ Lưu thành Markdown (.md)</button> <span id="dm" class="mu"></span></p>`}
function dlMd(){const t=$('#ft').value.trim(),c=$('#dc').value.trim();if(!t||!c)return $('#dm').textContent='Chưa có nội dung.';dl(slug(t)+'.md',(/^#\s/.test(c)?'':'# '+t+'\n\n')+c);$('#dm').textContent='Đã lưu. Vui lòng upload lên GitHub.'}
function rng(n){let a=+$('#p1').value||1,b=+$('#p2').value||n;a=Math.max(1,Math.min(a,n));b=Math.max(a,Math.min(b,n));return[a,b]}
function pickFile(f){PF=f||null;if(!f)return;if(!$('#ft').value)$('#ft').value=f.name.replace(/\.[^.]+$/,'');$('#dm').textContent='Đã chọn '+f.name}
async function readFile(){const m=$('#dm');if(!PF)return;m.textContent='Đang trích xuất…';try{if(!/\.pdf$/i.test(PF.name)){const t=await PF.text();$('#dc').value=t;return m.textContent='Hoàn tất!'}const pdf=await openPdf(PF),[a,b]=rng(pdf.numPages),t=await pdfTextOf(PF,a,b),n=t.replace(/## Trang \d+/g,'').trim().length;if(n<100)m.innerHTML=`<span class="err">PDF không có Text, hãy dùng công cụ Dùng AI Đọc.</span>`;else{$('#dc').value=t;m.textContent=`Thành công!`}}catch(e){m.textContent='Lỗi: '+(e.message||e)}}
async function ocrFile(){const m=$('#dm');if(!PF||!/\.pdf$/i.test(PF.name))return;try{m.textContent='AI đang xử lý hình ảnh…';const pdf=await openPdf(PF),[a,b]=rng(pdf.numPages);if(b-a+1>30)return m.textContent='Giới hạn 30 trang/lần.';let out='';for(let i=a;i<=b;i+=2){const e=Math.min(i+1,b),imgs=[];m.textContent=`AI OCR trang ${i}–${e}…`;for(let p=i;p<=e;p++){const pg=await pdf.getPage(p),vp=pg.getViewport({scale:1.5}),cv=document.createElement('canvas');cv.width=vp.width;cv.height=vp.height;await pg.render({canvasContext:cv.getContext('2d'),viewport:vp}).promise;imgs.push(cv.toDataURL('image/jpeg',.75).split(',')[1])}const{data,error}=await SB.functions.invoke('generate',{body:{text:true,images:imgs,prompt:'Chép chính xác nội dung sách giáo khoa GDQP&AN sang Markdown, chú ý giữ nguyên thuật ngữ quân sự.'}});if(error)throw new Error(await fe(error));if(data.error)throw new Error(data.error);out+=`\n\n## Trang ${i}–${e}\n`+data.text;$('#dc').value=out.trim()}m.textContent=`Xong OCR!`}catch(e){m.textContent='Lỗi OCR: '+(e.message||e)}}

/* ---------- HỌC SINH LÀM BÀI ---------- */
function student(code){
 A().innerHTML=`<div class="hero"><span class="ic">🎯</span><div><h1>Khu vực Làm bài thi</h1><p>Nhập thông tin cá nhân để bắt đầu</p></div></div><div class="card" style="border-top: 4px solid var(--pr);"><label>Mã bài (Code)</label><input id="jc" value="${esc(code)}" autocomplete="off"><label>Họ và tên học sinh</label><input id="jn" maxlength="60" placeholder="Nguyễn Văn A"><label>Lớp học</label><input id="jl" maxlength="20" placeholder="VD: 12A1"><label>Chia nhóm (Chỉ dùng nếu có yêu cầu)</label><select id="jg"><option value="">— Đấu cá nhân —</option>${[1,2,3,4,5,6,7,8].map(i=>`<option>Tiểu đội ${i}</option>`).join('')}</select><p style="margin-top:20px;"><button onclick="join()" style="width:100%; font-size:16px;">Vào Làm Bài Tập Kích 🔫</button></p><p id="jm" class="err" style="text-align:center;"></p></div>`}
async function join(){
 const code=$('#jc').value.trim().toUpperCase(),name=$('#jn').value.trim().replace(/\s+/g,' '),cls=$('#jl').value.trim(),g=$('#jg').value,m=$('#jm');
 if(!code||name.length<2)return m.textContent='Thiếu mã tham gia hoặc Tên.';
 const d=await col(code[0]=='T'?'tests':'games').doc(code).get();if(!d.exists)return m.textContent='Mã bài không hợp lệ hoặc đã bị khóa.';
 const dd=d.data();if(dd.mode=='nhom'){if(!g)return m.textContent='Yêu cầu chọn Tiểu đội.';if(dd.ng&&+g.replace(/\D/g,'')>dd.ng)return m.textContent='Chỉ có '+dd.ng+' tiểu đội.'}
 const{data:{user}}=await SB.auth.getUser(),rid=code+'_'+user.id+'_'+norm(name).replace(/ /g,'');
 if((await col('results').doc(rid).get()).exists)return m.textContent='Bạn đã hoàn thành bài này rồi, không thể thi lại.';
 Object.assign(P,{d:dd,code,rid,name,cls,grp:dd.mode=='nhom'?g:'',score:0,n:0,done:false,lock:false});code[0]=='T'?runTest():runGame()}

function clock(end){clearInterval(T);P.left=P.d.time*60;const t=()=>{const c=$('#clk');if(c){c.textContent=fmt(P.left);c.parentNode.classList.toggle('low',P.left<=30)}};t();T=setInterval(()=>{P.left--;t();if(P.left<=0){clearInterval(T);end()}},1000)}

function runGame(){const d=P.d,ty=d.mode=='nhom'?d.types:[d.types[0]];P.q=[];ty.forEach(t=>(d.qs[t]||[]).forEach(q=>P.q.push({...q,g:t})));P.i=0;
 A().innerHTML=`<div class="clock"><span>Binh nhì: ${esc(P.name)} ${P.grp?'· '+P.grp:''}</span><span id="clk"></span></div><div id="gm" class="card"></div>`;clock(endGame);showQ()}

function showQ(){if(P.done)return;P.lock=false;const q=P.q[P.i];if(!q)return endGame();let h=`<p class="mu">${GT[q.g]} · Câu ${P.i+1}/${P.q.length} · Điểm số: <b style="color:var(--pr);">${P.score}</b></p><div class="q">${esc(q.q)}</div>`;
 if(q.g=='mc')h+=q.o.map((o,j)=>`<button class="opt" onclick="pick(${j},this)"><b>${'ABCD'[j]}</b>. ${esc(o)}</button>`).join('');
 if(q.g=='tf')h+=`<div class="row"><button class="opt" style="text-align:center;" onclick="pick(true,this)">ĐÚNG</button><button class="opt" style="text-align:center;" onclick="pick(false,this)">SAI</button></div>`;
 if(q.g=='voice'){h+=`<button onclick="mic()">🎤 Ghi âm</button> <label>Hoặc Nhập văn bản</label><input id="vt"><p><button onclick="vcheck($('#vt').value)">Xác nhận</button></p><p id="vs" class="mu"></p>`;}
 if(q.g=='fill')h+=`<input id="vt" placeholder="Điền từ còn thiếu..."><p><button onclick="vcheck($('#vt').value)">Chốt Đáp Án</button></p>`;
 if(q.g=='scr'){const w=((q.k||[])[0]||'').toUpperCase();let s=w;for(let t=0;t<9&&s==w&&w.length>2;t++)s=shuf([...w]).join('');h+=`<div class="code">${esc(s)}</div><input id="vt" placeholder="Giải mã từ trên"><p><button onclick="vcheck($('#vt').value)">Trả lời</button></p>`}
 if(q.g=='match'){P.defs=shuf(q.p.map((x,j)=>[x[1],j]));h+=q.p.map((x,j)=>`<p style="margin:16px 0;"><b>${esc(x[0])}</b><select id="mm${j}"><option value="">— Tìm định nghĩa —</option>${P.defs.map(d=>`<option value="${d[1]}">${esc(d[0])}</option>`).join('')}</select></p>`).join('')+`<button onclick="mcheck()" style="margin-top:10px;">Kiểm Tra Ghép Nối</button>`}
 if(q.g=='order'){P.sh=shuf(q.s.map((t,j)=>[t,j]));P.ch=[];h+=`<p id="oc" class="mu" style="margin-bottom:10px;">Thực hiện thứ tự thao tác:</p><div>${P.sh.map((x,j)=>`<button class="opt" onclick="opick(${j},this)">${esc(x[0])}</button>`).join('')}</div>`}
 $('#gm').innerHTML=h+'<p id="fb"></p>'}

function res(f,msg){if(P.lock||P.done)return;P.lock=true;f=+f;const p=Math.round(10*f),ok=f>=1;P.score+=p;$('#fb').innerHTML=`<div style="margin-top:20px; padding:12px; border-radius:8px; background:${ok?'#d1fae5':'#fee2e2'}; color:${ok?'#065f46':'#991b1b'}; border:1px solid ${ok?'#10b981':'#ef4444'}"><span class="${ok?'ok':'err'}"><b>${ok?'Chính xác! +10đ':(p?'Đúng 1 phần, +'+p+'đ. ':'Chưa chuẩn xác. ')}</b><br>${esc(msg||'')}</span></div>`;P.i++;setTimeout(showQ,1600)}
function mcheck(){const q=P.q[P.i];let c=0;q.p.forEach((x,j)=>{if($('#mm'+j).value===String(j))c++});res(c/q.p.length,'Đáp án chuẩn: '+q.p.map(x=>x[0]+' → '+x[1]).join('; '))}
function opick(j,el){el.disabled=true;el.style.opacity="0.5";P.ch.push(P.sh[j]);$('#oc').innerHTML='<b>Đã sắp xếp:</b><br><span style="color:var(--pr)">'+P.ch.map(x=>x[0]).join(' ➔ ')+'</span>';if(P.ch.length==P.sh.length){const q=P.q[P.i],c=P.ch.filter((x,i)=>x[1]==i).length;res(c/P.sh.length,'Thứ tự chuẩn SGK: '+q.s.join(' ➔ '))}}
function pick(v,el){const q=P.q[P.i];document.querySelectorAll('.opt').forEach(b=>b.disabled=true);const ca=q.g=='mc'?(typeof q.a=='string'?'ABCD'.indexOf(q.a.trim().toUpperCase()[0]):+q.a):(q.a===true||q.a==='true'),ok=v===ca;el.classList.add(ok?'ok':'no');res(ok,q.g=='mc'?'Đáp án đúng: '+'ABCD'[ca]:'Đáp án: '+(ca?'Đúng':'Sai'))}
function mic(){const R=window.SpeechRecognition||window.webkitSpeechRecognition;if(!R)return $('#vs').textContent='Thiết bị chưa hỗ trợ Mic.';$('#vs').textContent='Đang ghi âm, vui lòng nói...';const r=new R();r.lang='vi-VN';r.onresult=e=>{const t=e.results[0][0].transcript;$('#vs').textContent='Bạn nói: '+t;vcheck(t)};r.onerror=()=>$('#vs').textContent='Chưa nghe rõ.';try{r.start()}catch(e){}}
function vcheck(t){const q=P.q[P.i];if(!norm(t))return;res(keys(q.k).some(k=>norm(t).includes(k)),'Từ khóa đúng: '+(q.k||[])[0])}
async function endGame(){if(P.done)return;P.done=true;clearInterval(T);let rs=[];try{await col('results').doc(P.rid).set({code:P.code,name:P.name,cls:P.cls,group:P.grp||'',score:P.score,kind:'game',at:Date.now()});rs=(await col('results').where('code','==',P.code).get()).docs.map(d=>d.data())}catch(e){}
 const g={};if(!rs.length)rs=[{name:P.name,score:P.score,group:P.grp||''}];rs.forEach(r=>r.score=+r.score||0);rs.forEach(r=>{if(r.group)g[r.group]=(g[r.group]||0)+r.score});
 A().innerHTML=`<div class="card" style="text-align:center; border:2px solid var(--pr)"><h1>Huấn luyện Hoàn tất!</h1><p style="font-size:3rem; margin:10px 0; color:var(--pr); font-weight:800;">${P.score}</p><p class="mu">Điểm số cá nhân</p></div>
 <div class="card"><h2>🏆 Bảng vàng Thành tích</h2>${rs.sort((a,b)=>b.score-a.score).slice(0,10).map((r,i)=>`<div style="display:flex; justify-content:space-between; padding:8px 0; border-bottom:1px solid #eee;"><span><b>#${i+1}</b>. ${esc(r.name)}</span><strong style="color:var(--pr);">${r.score}</strong></div>`).join('')}
 ${Object.keys(g).length?'<h2 style="margin-top:30px;">🎖 Xếp hạng Tiểu đội</h2>'+Object.entries(g).sort((a,b)=>b[1]-a[1]).map(([n,s], i)=>`<div style="display:flex; justify-content:space-between; padding:8px 0; border-bottom:1px solid #eee;"><span><b>#${i+1}</b>. ${esc(n)}</span><strong style="color:#0284c7;">${s}đ</strong></div>`).join(''):''}</div>`;}

function runTest(){const d=P.d;let h=`<div class="clock"><span>${esc(P.name)}</span><span id="clk"></span></div>`;
 d.qs.forEach((q,i)=>{h+=`<div class="card"><b>Câu ${i+1}.</b> ${esc(q.q)} <span class="mu">(${LV[q.l]||''})</span>`;
  if(q.t=='mc')h+=q.o.map((o,j)=>`<label style="margin-left:10px;"><input type="radio" name="q${i}" value="${j}"> <b>${'ABCD'[j]}</b>. ${esc(o)}</label>`).join('');
  if(q.t=='tf')h+=q.s.map((m,j)=>`<p style="margin-top:16px;"><b>${'abcd'[j]})</b> ${esc(m.x)}<br><label style="display:inline-block; margin-right:20px; margin-top:8px;"><input type="radio" name="s${i}_${j}" value="1"> Đúng</label><label style="display:inline-block;"><input type="radio" name="s${i}_${j}" value="0"> Sai</label></p>`).join('');
  if(q.t=='sa')h+=`<input id="a${i}" placeholder="Điền đáp án ngắn gọn" style="margin-top:10px;">`;if(q.t=='es')h+=`<textarea id="a${i}" rows="4" placeholder="Trình bày tự luận..." style="margin-top:10px;"></textarea>`;h+='</div>'});
 A().innerHTML=h+'<p style="text-align:center; margin-top:30px;"><button onclick="submitTest()" style="font-size:18px; padding:15px 40px;">Nộp bài ngay</button></p>';clock(submitTest)}

async function submitTest(){if(P.done)return;P.done=true;clearInterval(T);const by={nb:[0,0],th:[0,0],vd:[0,0]};let e=0,tot=0;
 P.d.qs.forEach((q,i)=>{const w=q.t=='es'?2:1;let f=0;
  if(q.t=='mc'){const v=document.querySelector(`[name=q${i}]:checked`);f=v&&+v.value===q.a?1:0}
  if(q.t=='tf'){q.s.forEach((m,j)=>{const v=document.querySelector(`[name=s${i}_${j}]:checked`);if(v&&(v.value=='1')===m.a)f+=1/q.s.length})}
  if(q.t=='sa'){const v=norm($('#a'+i).value);f=v&&keys(q.k).some(k=>k==v||v.includes(k))?1:0}
  if(q.t=='es'){const v=norm($('#a'+i).value),k=keys(q.k);f=k.length?Math.min(1,k.filter(x=>v.includes(x)).length/Math.max(1,Math.ceil(k.length*.7))):0}
  e+=f*w;tot+=w;const l=by[q.l]?q.l:'nb';by[l][0]+=f*w;by[l][1]+=w});
 const s=Math.round(e/tot*100)/10;
 try{await col('results').doc(P.rid).set({code:P.code,name:P.name,cls:P.cls,score:s,by,kind:'test',at:Date.now()})}catch(er){P.done=false;alert('Lỗi nộp bài, hãy kiểm tra Wifi. ('+(er.message||er)+')');return}
 A().innerHTML=`<div class="card" style="text-align:center;"><h1>Hoàn thành Bài thi</h1><h2 style="font-size:3rem; margin:10px 0; color:var(--pr);">${s}/10</h2><p style="font-weight:600; color:#374151;">${cm(s)}</p><hr style="border-top:1px solid var(--ln); margin:20px 0;">${Object.keys(LV).map(k=>by[k][1]?`<p>Mức <b>${LV[k]}</b>: đạt <span style="color:var(--pr); font-weight:600;">${Math.round(by[k][0]/by[k][1]*100)}%</span></p>`:'').join('')}<p class="mu" style="margin-top:20px;">* Lưu ý: Phần tự luận sẽ được giáo viên bộ môn xem xét lại.</p></div>`}

addEventListener('hashchange',()=>location.reload());
boot();
</script></body></html>
