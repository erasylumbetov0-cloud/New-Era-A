html=f'''<!doctype html>
<html lang="kk"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<title>Жаңа Мегаполис — тұрғындар картасы</title>
<style>
:root{{--bg:#071327;--panel:#10243a;--line:#245365;--gold:#ffc85a;--cyan:#61d6d8;--text:#f3f7ff}}
*{{box-sizing:border-box}}body{{margin:0;background:linear-gradient(145deg,#071327,#0b2936);color:var(--text);font-family:Arial,sans-serif}}
header{{padding:34px 18px 25px;text-align:center;background:#0c1c38;border-bottom:2px solid var(--gold)}}
h1{{font-size:clamp(28px,6vw,48px);margin:0 0 9px}}header p{{color:var(--cyan);margin:0}}
.wrap{{max-width:1100px;margin:auto;padding:20px}}
.stats{{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin:15px 0 22px}}
.stat,.facility,.resident{{background:var(--panel);border:1px solid var(--line);border-radius:14px;padding:15px}}
.stat b{{display:block;color:var(--gold);font-size:25px}}
input{{width:100%;padding:16px;border-radius:12px;border:2px solid var(--line);background:#071827;color:white;font-size:17px;outline:none}}
input:focus{{border-color:var(--cyan)}}h2{{margin:28px 0 13px;color:var(--gold)}}
.grid{{display:grid;grid-template-columns:repeat(auto-fill,minmax(210px,1fr));gap:10px}}
.resident{{display:flex;align-items:center;gap:12px;min-height:68px}}
.num{{color:var(--gold);font-weight:bold;font-size:18px;min-width:42px}}
.house{{font-size:24px}}.nick{{font-weight:600;overflow-wrap:anywhere}}.small{{font-size:12px;color:#9bb6c9;margin-top:4px}}
.facilities{{display:grid;grid-template-columns:repeat(auto-fit,minmax(170px,1fr));gap:10px}}
.facility{{text-align:center;padding:20px 12px}}.facility .ico{{font-size:32px}}.facility b{{display:block;color:var(--cyan);margin:8px}}
footer{{text-align:center;color:#91aabd;padding:28px;font-size:13px}}
@media(max-width:520px){{.stats{{grid-template-columns:1fr 1fr}}}}
</style></head>
<body><header><h1>🏙️ ЖАҢА МЕГАПОЛИС</h1><p>Таза • Қауіпсіз • Заманауи қала</p></header>
<main class="wrap">
<div class="stats"><div class="stat"><b>{len(names)}</b>Тұрғын</div><div class="stat"><b>{len(names)}</b>Үй нөмірі</div><div class="stat"><b>5</b>Қоғамдық нысан</div></div>
<h2>🔎 Тұрғынды никі немесе нөмірі арқылы іздеу</h2>
<input id="search" type="search" placeholder="Мысалы: miko немесе 001..." autocomplete="off">
<p id="count" class="small">Барлық тұрғын көрсетіліп тұр</p>
<div id="residents" class="grid"></div>
<h2>🏫 Қала нысандары</h2>
<div class="facilities">
<div class="facility"><div class="ico">🏫</div><b>Мектеп</b>Білім беру орталығы</div>
<div class="facility"><div class="ico">🏥</div><b>Аурухана</b>Медициналық көмек</div>
<div class="facility"><div class="ico">🏋️</div><b>Спорт зал</b>Спорт және жаттығу</div>
<div class="facility"><div class="ico">🕌</div><b>Мешіт</b>Рухани орталық</div>
<div class="facility"><div class="ico">🛍️</div><b>Дүкендер</b>Adiletm95 және danchiz</div>
</div></main><footer>Жаңа Мегаполис © Барлық тұрғынға жеке үй нөмірі берілген</footer>
<script>
const people={json.dumps(names,ensure_ascii=False)};
const root=document.getElementById('residents'),search=document.getElementById('search'),count=document.getElementById('count');
function render(){{
 const q=search.value.trim().toLocaleLowerCase();
 const matches=people.map((name,i)=>({{name,id:i+1}})).filter(p=>p.name.toLocaleLowerCase().includes(q)||String(p.id).padStart(3,'0').includes(q));
 root.innerHTML=matches.map(p=>`<article class="resident"><span class="num">#${{String(p.id).padStart(3,'0')}}</span><span class="house">🏠</span><div><div class="nick">${{escapeHtml(p.name)}}</div><div class="small">Үй № ${{p.id}}</div></div></article>`).join('');
 count.textContent=`${{matches.length}} тұрғын табылды`;
}}
function escapeHtml(s){{return s.replace(/[&<>"']/g,c=>({{'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}}[c]));}}
search.addEventListener('input',render);render();
</script></body></html>'''
with open('/mnt/data/megapolis.html','w',encoding='utf-8') as f:f.write(html)
print(os.path.getsize('/mnt/data/megapolis.html'))
