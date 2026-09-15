<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Моя коллекция энергетиков</title>
<style>
  :root{
    --bg:#0f1115; --card:#1a1d24; --card2:#22262f; --line:#2e333d;
    --text:#e8eaed; --muted:#9aa0aa; --accent:#00e5a0; --accent2:#00b37e;
    --danger:#ff5c5c; --gold:#ffd23f;
  }
  *{box-sizing:border-box}
  body{
    margin:0; font-family:system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;
    background:var(--bg); color:var(--text); padding:16px;
  }
  h1{font-size:22px;margin:0 0 4px}
  .sub{color:var(--muted);font-size:13px;margin-bottom:16px}
  .wrap{max-width:1100px;margin:0 auto}

  .panel{
    background:var(--card);border:1px solid var(--line);border-radius:14px;
    padding:16px;margin-bottom:16px;
  }
  .grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:12px}
  label{display:block;font-size:12px;color:var(--muted);margin-bottom:4px}
  input,select,textarea{
    width:100%;padding:10px;border-radius:9px;border:1px solid var(--line);
    background:var(--card2);color:var(--text);font-size:14px;outline:none;
  }
  input:focus,select:focus,textarea:focus{border-color:var(--accent)}
  textarea{resize:vertical;min-height:60px}

  .btn{
    padding:10px 16px;border-radius:9px;border:none;cursor:pointer;
    font-size:14px;font-weight:600;background:var(--accent);color:#04231a;
    transition:.15s;
  }
  .btn:hover{background:var(--accent2)}
  .btn.ghost{background:transparent;color:var(--text);border:1px solid var(--line)}
  .btn.ghost:hover{border-color:var(--accent);color:var(--accent)}
  .btn.danger{background:transparent;color:var(--danger);border:1px solid var(--danger)}
  .btn.danger:hover{background:var(--danger);color:#fff}
  .row{display:flex;gap:8px;flex-wrap:wrap;align-items:center}

  /* Звёзды оценки */
  .stars{display:flex;gap:4px;font-size:24px;cursor:pointer;user-select:none}
  .stars span{color:#3a3f4a;transition:.1s}
  .stars span.on{color:var(--gold)}

  /* Карточки */
  .cards{display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:14px}
  .card{
    background:var(--card);border:1px solid var(--line);border-radius:14px;
    padding:14px;display:flex;flex-direction:column;gap:8px;position:relative;
  }
  .card h3{margin:0;font-size:17px}
  .flavor{color:var(--muted);font-size:13px}
  .badge{
    display:inline-block;font-size:11px;padding:3px 8px;border-radius:20px;
    background:#2a2f3a;color:var(--muted);margin-right:4px;
  }
  .badge.limited{background:#3a2a00;color:var(--gold)}
  .card .score{font-size:15px;color:var(--gold);letter-spacing:1px}
  .card .note{font-size:13px;color:var(--muted);white-space:pre-wrap}
  .card .actions{display:flex;gap:8px;margin-top:auto;padding-top:6px}
  .empty{color:var(--muted);text-align:center;padding:40px 10px}
  .count{color:var(--muted);font-size:13px}
</style>
</head>
<body>
<div class="wrap">
  <h1>⚡ Коллекция энергетиков</h1>
  <div class="sub">Учёт банок, оценка вкуса и поиск по бренду, вкусу и лимитированности</div>

  <!-- ФОРМА -->
  <div class="panel">
    <div class="grid">
      <div>
        <label>Бренд *</label>
        <input id="brand" list="brandsList" placeholder="Red Bull, Monster...">
        <datalist id="brandsList"></datalist>
      </div>
      <div>
        <label>Вкус *</label>
        <input id="flavor" placeholder="Tropical, Original...">
      </div>
      <div>
        <label>Объём</label>
        <input id="volume" placeholder="500 мл">
      </div>
      <div>
        <label>Дата добавления</label>
        <input id="date" type="date">
      </div>
      <div>
        <label>Лимитированность</label>
        <select id="limited">
          <option value="no">Обычный</option>
          <option value="yes">Лимитированный</option>
        </select>
      </div>
      <div>
        <label>Оценка вкуса</label>
        <div class="stars" id="stars" data-value="0">
          <span data-v="1">★</span><span data-v="2">★</span><span data-v="3">★</span>
          <span data-v="4">★</span><span data-v="5">★</span>
        </div>
      </div>
    </div>
    <div style="margin-top:12px">
      <label>Заметка (впечатления, где купил и т.д.)</label>
      <textarea id="note" placeholder="Приятный кисло-сладкий вкус, куплен в Пятёрочке..."></textarea>
    </div>
    <div class="row" style="margin-top:12px">
      <button class="btn" id="saveBtn">Добавить в коллекцию</button>
      <button class="btn ghost" id="cancelEdit" style="display:none">Отмена</button>
    </div>
  </div>

  <!-- ПОИСК -->
  <div class="panel">
    <div class="grid">
      <div>
        <label>Поиск (бренд / вкус / заметка)</label>
        <input id="search" placeholder="Начните вводить...">
      </div>
      <div>
        <label>Фильтр лимитированности</label>
        <select id="filterLimited">
          <option value="all">Все</option>
          <option value="yes">Только лимитированные</option>
          <option value="no">Только обычные</option>
        </select>
      </div>
      <div>
        <label>Сортировка</label>
        <select id="sort">
          <option value="date_desc">Сначала новые</option>
          <option value="date_asc">Сначала старые</option>
          <option value="score_desc">По оценке (высокая)</option>
          <option value="score_asc">По оценке (низкая)</option>
          <option value="brand">По бренду (А-Я)</option>
        </select>
      </div>
      <div>
        <label>Минимальная оценка</label>
        <select id="minScore">
          <option value="0">Любая</option>
          <option value="1">1+</option><option value="2">2+</option>
          <option value="3">3+</option><option value="4">4+</option><option value="5">5</option>
        </select>
      </div>
    </div>
    <div class="row" style="margin-top:12px">
      <span class="count" id="count"></span>
      <button class="btn ghost" id="exportBtn">Экспорт JSON</button>
      <button class="btn ghost" id="importBtn">Импорт JSON</button>
      <input type="file" id="importFile" accept=".json" style="display:none">
    </div>
  </div>

  <!-- СПИСОК -->
  <div class="cards" id="cards"></div>
  <div class="empty" id="empty" style="display:none">Пока пусто. Добавьте первую банку ⚡</div>
</div>

<script>
const STORAGE_KEY = 'energy_collection_v1';
let items = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]');
let editId = null;
let currentScore = 0;

const $ = id => document.getElementById(id);

/* ---------- Сохранение ---------- */
function persist(){ localStorage.setItem(STORAGE_KEY, JSON.stringify(items)); }

/* ---------- Звёзды ---------- */
const starsEl = $('stars');
starsEl.addEventListener('click', e => {
  if(!e.target.dataset.v) return;
  currentScore = +e.target.dataset.v;
  paintStars();
});
function paintStars(){
  [...starsEl.children].forEach(s =>
    s.classList.toggle('on', +s.dataset.v <= currentScore));
}
paintStars();

/* ---------- Дата по умолчанию ---------- */
$('date').value = new Date().toISOString().slice(0,10);

/* ---------- Добавление / редактирование ---------- */
$('saveBtn').addEventListener('click', () => {
  const brand = $('brand').value.trim();
  const flavor = $('flavor').value.trim();
  if(!brand || !flavor){ alert('Заполните бренд и вкус'); return; }

  const data = {
    brand, flavor,
    volume: $('volume').value.trim(),
    date: $('date').value || new Date().toISOString().slice(0,10),
    limited: $('limited').value,
    score: currentScore,
    note: $('note').value.trim()
  };

  if(editId){
    const i = items.findIndex(x => x.id === editId);
    items[i] = { ...items[i], ...data };
    editId = null;
    $('saveBtn').textContent = 'Добавить в коллекцию';
    $('cancelEdit').style.display = 'none';
  } else {
    items.push({ id: crypto.randomUUID(), ...data });
  }

  persist();
  resetForm();
  render();
});

$('cancelEdit').addEventListener('click', () => {
  editId = null;
  $('saveBtn').textContent = 'Добавить в коллекцию';
  $('cancelEdit').style.display = 'none';
  resetForm();
});

function resetForm(){
  ['brand','flavor','volume','note'].forEach(id => $(id).value = '');
  $('limited').value = 'no';
  $('date').value = new Date().toISOString().slice(0,10);
  currentScore = 0; paintStars();
}

/* ---------- Редактирование ---------- */
function startEdit(id){
  const it = items.find(x => x.id === id);
  if(!it) return;
  editId = id;
  $('brand').value = it.brand;
  $('flavor').value = it.flavor;
  $('volume').value = it.volume || '';
  $('date').value = it.date;
  $('limited').value = it.limited;
  $('note').value = it.note || '';
  currentScore = it.score || 0; paintStars();
  $('saveBtn').textContent = 'Сохранить изменения';
  $('cancelEdit').style.display = 'inline-block';
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

/* ---------- Удаление ---------- */
function removeItem(id){
  if(!confirm('Удалить эту запись?')) return;
  items = items.filter(x => x.id !== id);
  persist(); render();
}

/* ---------- Отрисовка ---------- */
function render(){
  const q = $('search').value.trim().toLowerCase();
  const fl = $('filterLimited').value;
  const sort = $('sort').value;
  const minScore = +$('minScore').value;

  let list = items.filter(it => {
    const hay = (it.brand + ' ' + it.flavor + ' ' + (it.note||'') + ' ' + (it.volume||'')).toLowerCase();
    if(q && !hay.includes(q)) return false;
    if(fl !== 'all' && it.limited !== fl) return false;
    if((it.score||0) < minScore) return false;
    return true;
  });

  const cmp = {
    date_desc: (a,b) => (b.date||'').localeCompare(a.date||''),
    date_asc:  (a,b) => (a.date||'').localeCompare(b.date||''),
    score_desc:(a,b) => (b.score||0)-(a.score||0),
    score_asc: (a,b) => (a.score||0)-(b.score||0),
    brand:     (a,b) => a.brand.localeCompare(b.brand,'ru')
  }[sort];
  list.sort(cmp);

  const cards = $('cards');
  cards.innerHTML = '';
  $('empty').style.display = list.length ? 'none' : 'block';

  list.forEach(it => {
    const el = document.createElement('div');
    el.className = 'card';
    el.innerHTML = `
      <h3>${esc(it.brand)}</h3>
      <div class="flavor">🍹 ${esc(it.flavor)}${it.volume ? ' · '+esc(it.volume) : ''}</div>
      <div>
        <span class="badge ${it.limited==='yes'?'limited':''}">
          ${it.limited==='yes' ? '★ Лимитированный' : 'Обычный'}
        </span>
        <span class="badge">${esc(it.date||'')}</span>
      </div>
      <div class="score">${it.score ? '★'.repeat(it.score)+'☆'.repeat(5-it.score) : 'Без оценки'}</div>
      ${it.note ? `<div class="note">${esc(it.note)}</div>` : ''}
      <div class="actions">
        <button class="btn ghost" data-edit="${it.id}">Изменить</button>
        <button class="btn danger" data-del="${it.id}">Удалить</button>
      </div>`;
    cards.appendChild(el);
  });

  $('count').textContent = `Найдено: ${list.length} из ${items.length}`;

  // datalist брендов
  const brands = [...new Set(items.map(x => x.brand))].sort();
  $('brandsList').innerHTML = brands.map(b => `<option value="${esc(b)}">`).join('');
}

cards.addEventListener('click', e => {
  const ed = e.target.dataset.edit, dl = e.target.dataset.del;
  if(ed) startEdit(ed);
  if(dl) removeItem(dl);
});

function esc(s){ return String(s).replace(/[&<>"]/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c])); }

/* ---------- Фильтры ---------- */
['search','filterLimited','sort','minScore'].forEach(id =>
  $(id).addEventListener('input', render));

/* ---------- Экспорт / импорт ---------- */
$('exportBtn').addEventListener('click', () => {
  const blob = new Blob([JSON.stringify(items, null, 2)], {type:'application/json'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'energy-collection.json';
  a.click();
});
$('importBtn').addEventListener('click', () => $('importFile').click());
$('importFile').addEventListener('change', e => {
  const f = e.target.files[0]; if(!f) return;
  const r = new FileReader();
  r.onload = () => {
    try{
      const data = JSON.parse(r.result);
      if(!Array.isArray(data)) throw 0;
      data.forEach(d => { if(!d.id) d.id = crypto.randomUUID(); });
      items = items.concat(data);
      persist(); render();
    }catch{ alert('Неверный файл'); }
  };
  r.readAsText(f);
});

/* ---------- Старт ---------- */
render();
</script>
</body>
</html>
