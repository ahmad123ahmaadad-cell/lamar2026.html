<!doctype html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="theme-color" content="#0b0b0c">
<title>Lamar Cars</title>
<style>
*{box-sizing:border-box}body{margin:0;font-family:Arial,sans-serif;background:#f5f5f7;color:#111}
button,input,textarea,select{font:inherit}button{cursor:pointer}
.splash{position:fixed;inset:0;background:#090909;color:#fff;z-index:50;display:grid;place-items:center;transition:.45s}
.splash.hide{opacity:0;pointer-events:none}.sbox{text-align:center}.sbox .car{font-size:64px;animation:drive 1.7s ease-in-out}.sbox h1{letter-spacing:2px;margin:8px 0;font-size:32px}.sbox small{color:#aaa}
@keyframes drive{0%{transform:translateX(-140px);opacity:0}25%,75%{opacity:1}100%{transform:translateX(140px);opacity:0}}
header{position:sticky;top:0;z-index:10;background:#0b0b0c;color:#fff;padding:15px 14px 12px}.logo{text-align:center;font-size:24px;font-weight:800;letter-spacing:1px}.search{margin-top:12px;display:flex;gap:8px}.search input{flex:1;padding:13px;border:0;border-radius:12px;outline:0}.lang{background:#222;color:#fff;border:0;border-radius:10px;padding:0 11px}
.tabs{display:flex;gap:8px;overflow:auto;background:#fff;padding:12px}.tabs button{border:0;border-radius:20px;padding:10px 14px;background:#eee;white-space:nowrap}.tabs .on{background:#111;color:#fff}
.wrap{max-width:900px;margin:auto}.title{padding:17px 14px 9px;font-size:21px;font-weight:800}.grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:12px;padding:0 12px 95px}.card{background:#fff;border-radius:15px;overflow:hidden;box-shadow:0 2px 9px #ddd}.card img{width:100%;height:145px;object-fit:cover;background:#ddd}.ci{padding:10px}.ci h3{margin:0 0 6px;font-size:16px}.meta{font-size:12px;color:#777}.price{font-weight:800;color:#087b3b;margin:8px 0}.row{display:flex;gap:7px}.row button{flex:1;border:0;border-radius:9px;padding:9px;background:#111;color:#fff}.row .light{background:#eee;color:#111}
.empty{padding:35px;text-align:center;color:#777;grid-column:1/-1}
.bottom{position:fixed;bottom:0;left:0;right:0;background:#fff;display:flex;justify-content:space-around;padding:9px 5px calc(9px + env(safe-area-inset-bottom));box-shadow:0 -2px 12px #ddd;z-index:20}.bottom button{border:0;background:none;font-size:11px}.bottom b{display:block;font-size:21px}
.modal{position:fixed;inset:0;background:#0008;z-index:30;display:none;align-items:flex-end}.modal.show{display:flex}.sheet{background:#fff;width:100%;max-height:92vh;overflow:auto;border-radius:20px 20px 0 0;padding:18px}.sheet h2{margin-top:0}.close{float:left;border:0;background:#eee;border-radius:10px;padding:7px 11px}.form input,.form textarea,.form select{width:100%;padding:12px;margin:6px 0 10px;border:1px solid #ddd;border-radius:10px}.form textarea{min-height:90px;resize:vertical}.submit{width:100%;padding:13px;border:0;border-radius:11px;background:#111;color:#fff}.preview{width:100%;max-height:220px;object-fit:cover;border-radius:12px;display:none;margin:5px 0 10px}
.chatbox{height:280px;overflow:auto;background:#f5f5f5;border-radius:12px;padding:10px}.msg{padding:9px 11px;background:#fff;border-radius:12px;margin:7px 0;max-width:80%}.mine{margin-right:auto;background:#111;color:#fff}.chatrow{display:flex;gap:7px;margin-top:8px}.chatrow input{flex:1;padding:12px;border:1px solid #ddd;border-radius:10px}.chatrow button{border:0;background:#111;color:#fff;border-radius:10px;padding:0 15px}
@media(min-width:700px){.grid{grid-template-columns:repeat(3,minmax(0,1fr))}}
</style>
</head>
<body>
<div class="splash" id="splash"><div class="sbox"><div class="car">🚗</div><h1>LAMAR CARS</h1><small>Cars • Parts • Rental • Shipping</small></div></div>

<header><div class="logo">LAMAR CARS</div><div class="search"><input id="q" placeholder="🔍 ابحث عن سيارة أو قطعة" oninput="render()"><button class="lang" onclick="language()">🌐</button></div></header>

<div class="tabs">
<button class="on" data-cat="all" onclick="setCat('all',this)">الكل</button>
<button data-cat="sale" onclick="setCat('sale',this)">🚗 للبيع</button>
<button data-cat="parts" onclick="setCat('parts',this)">🔧 قطع</button>
<button data-cat="rent" onclick="setCat('rent',this)">🚘 للإيجار</button>
<button data-cat="ship" onclick="setCat('ship',this)">🚚 شحن</button>
</div>

<main class="wrap"><div class="title" id="title">سيارات مقترحة لك</div><div class="grid" id="grid"></div></main>

<div class="bottom">
<button onclick="home()"><b>🏠</b>الرئيسية</button>
<button onclick="openPost()"><b>➕</b>نشر إعلان</button>
<button onclick="openChat('Lamar Cars')"><b>💬</b>الرسائل</button>
<button onclick="showMyAds()"><b>📋</b>إعلاناتي</button>
</div>

<div class="modal" id="postModal"><div class="sheet"><button class="close" onclick="closeModal('postModal')">✕</button><h2>نشر إعلان</h2>
<div class="form">
<select id="ptype"><option value="sale">🚗 سيارة للبيع</option><option value="parts">🔧 قطعة سيارات</option><option value="rent">🚘 سيارة للإيجار</option><option value="ship">🚚 شحن سيارة</option></select>
<input id="pname" placeholder="اسم السيارة أو القطعة">
<input id="pprice" placeholder="السعر">
<select id="pcountry"><option>🇸🇾 سوريا</option><option>🇱🇧 لبنان</option><option>🇩🇪 ألمانيا</option><option>🇦🇪 الإمارات</option><option>🇸🇦 السعودية</option><option>🇴🇲 عُمان</option><option>🇯🇴 الأردن</option><option>🇺🇸 أمريكا</option><option>🇰🇷 كوريا</option></select>
<textarea id="pdesc" placeholder="اكتب الوصف والتفاصيل"></textarea>
<input id="photo" type="file" accept="image/*" onchange="previewPhoto(event)">
<img id="preview" class="preview">
<button class="submit" onclick="saveAd()">نشر الإعلان</button>
</div></div></div>

<div class="modal" id="chatModal"><div class="sheet"><button class="close" onclick="closeModal('chatModal')">✕</button><h2 id="chatTitle">المحادثة</h2><div class="chatbox" id="chatbox"></div><div class="chatrow"><input id="chatInput" placeholder="اكتب رسالتك"><button onclick="sendMsg()">إرسال</button></div></div></div>

<div class="modal" id="detailModal"><div class="sheet"><button class="close" onclick="closeModal('detailModal')">✕</button><div id="detail"></div></div></div>

<script>
const sample=[
{id:1,cat:'sale',name:'Mercedes-Benz C-Class',price:'$35,000',country:'🇩🇪 ألمانيا',desc:'سيارة بحالة ممتازة',img:'https://images.unsplash.com/photo-1553440569-bcc63803a83d?auto=format&fit=crop&w=800&q=80'},
{id:2,cat:'sale',name:'BMW 5 Series',price:'$28,000',country:'🇩🇪 ألمانيا',desc:'أوتوماتيك، مواصفات كاملة',img:'https://images.unsplash.com/photo-1555215695-3004980ad54e?auto=format&fit=crop&w=800&q=80'},
{id:3,cat:'rent',name:'Porsche 911',price:'$150 / يوم',country:'🇺🇸 أمريكا',desc:'متاحة للإيجار',img:'https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=800&q=80'},
{id:4,cat:'sale',name:'Audi Q8',price:'$48,000',country:'🇦🇪 الإمارات',desc:'حالة ممتازة',img:'https://images.unsplash.com/photo-1606664515524-ed2f786a0bd6?auto=format&fit=crop&w=800&q=80'}
];
let ads=JSON.parse(localStorage.getItem('lamarAds')||'[]'),cat='all',activeChat='Lamar Cars';
const allAds=()=>[...ads,...sample];
function render(){
 let q=document.getElementById('q').value.trim().toLowerCase();
 let list=allAds().filter(x=>(cat==='all'||x.cat===cat)&&(!q||(x.name+' '+x.country+' '+x.desc).toLowerCase().includes(q)));
 document.getElementById('grid').innerHTML=list.length?list.map(x=>`<article class="card"><img src="${x.img||placeholder()}" onerror="this.src=placeholder()"><div class="ci"><h3>${esc(x.name)}</h3><div class="meta">${esc(x.country)}</div><div class="price">${esc(x.price)}</div><div class="row"><button onclick="details(${x.id})">التفاصيل</button><button class="light" onclick="openChat('${esc(x.name)}')">💬</button></div></div></article>`).join(''):'<div class="empty">لا توجد نتائج حاليًا.</div>';
}
function placeholder(){return 'data:image/svg+xml;charset=UTF-8,'+encodeURIComponent('<svg xmlns="http://www.w3.org/2000/svg" width="800" height="500"><rect width="100%" height="100%" fill="#ddd"/><text x="50%" y="50%" text-anchor="middle" font-size="42" fill="#555">Lamar Cars</text></svg>')}
function esc(s){return String(s).replace(/[&<>"']/g,m=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[m]))}
function setCat(c,b){cat=c;document.querySelectorAll('.tabs button').forEach(x=>x.classList.remove('on'));b.classList.add('on');render()}
function home(){cat='all';document.querySelectorAll('.tabs button').forEach(x=>x.classList.toggle('on',x.dataset.cat==='all'));document.getElementById('q').value='';render();scrollTo(0,0)}
function openPost(){document.getElementById('postModal').classList.add('show')}
function closeModal(id){document.getElementById(id).classList.remove('show')}
function previewPhoto(e){let f=e.target.files[0],p=document.getElementById('preview');if(f){p.src=URL.createObjectURL(f);p.style.display='block'}}
function saveAd(){
 let f=document.getElementById('photo').files[0];
 const finish=(img)=>{let a={id:Date.now(),cat:ptype.value,name:pname.value.trim()||'إعلان جديد',price:pprice.value.trim()||'السعر عند التواصل',country:pcountry.value,desc:pdesc.value.trim(),img:img||placeholder(),mine:true};ads.unshift(a);localStorage.setItem('lamarAds',JSON.stringify(ads));closeModal('postModal');['pname','pprice','pdesc'].forEach(id=>document.getElementById(id).value='');document.getElementById('photo').value='';document.getElementById('preview').style.display='none';cat='all';render();alert('تم حفظ إعلانك على هذا الجهاز.')}
 if(f){let r=new FileReader();r.onload=()=>finish(r.result);r.readAsDataURL(f)}else finish(null)
}
function details(id){let x=allAds().find(a=>a.id===id);if(!x)return;document.getElementById('detail').innerHTML=`<img src="${x.img||placeholder()}" style="width:100%;max-height:280px;object-fit:cover;border-radius:14px"><h2>${esc(x.name)}</h2><p>${esc(x.country)}</p><h3 style="color:#087b3b">${esc(x.price)}</h3><p>${esc(x.desc||'لا يوجد وصف')}</p><button class="submit" onclick="closeModal('detailModal');openChat('${esc(x.name)}')">💬 تواصل مع العارض</button>`;document.getElementById('detailModal').classList.add('show')}
function openChat(name){activeChat=name;document.getElementById('chatTitle').textContent='المحادثة مع '+name;drawChat();document.getElementById('chatModal').classList.add('show')}
function drawChat(){let msgs=JSON.parse(localStorage.getItem('chat_'+activeChat)||'[]');document.getElementById('chatbox').innerHTML=msgs.length?msgs.map(m=>`<div class="msg ${m.mine?'mine':''}">${esc(m.t)}</div>`).join(''):'<div style="color:#888;text-align:center;padding:30px">ابدأ المحادثة</div>';let b=document.getElementById('chatbox');b.scrollTop=b.scrollHeight}
function sendMsg(){let v=document.getElementById('chatInput').value.trim();if(!v)return;let k='chat_'+activeChat,m=JSON.parse(localStorage.getItem(k)||'[]');m.push({t:v,mine:true});localStorage.setItem(k,JSON.stringify(m));document.getElementById('chatInput').value='';drawChat()}
function showMyAds(){let n=ads.length;alert(n?'لديك '+n+' إعلان محفوظ على هذا الجهاز.':'لم تنشر أي إعلان بعد.')}
function language(){alert('النسخة الحالية عربية. يمكن إضافة العربية والإنكليزية والألمانية والكورية وغيرها في النسخة متعددة اللغات.')}
setTimeout(()=>document.getElementById('splash').classList.add('hide'),2000);
render();
</script>
</body>
</html>
