<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#007aff">
<title>Civil Engineer — Abed Osama</title>

<style>
*{box-sizing:border-box}
body{
  margin:0;
  font-family:Arial,sans-serif;
  background:#f3f6fa;
  color:#172033;
}
header{
  background:linear-gradient(135deg,#007aff,#0056b3);
  color:white;
  padding:25px 18px;
  text-align:center;
}
header h1{margin:0 0 8px}
header p{margin:0;opacity:.9}
ou
.container{
  max-width:1000px;
  margin:auto;
  padding:18px;
}

.card{
  background:white;
  border-radius:16px;
  padding:18px;
  margin-bottom:18px;
  box-shadow:0 4px 18px rgba(0,0,0,.08);
}

input,select,button{
  width:100%;
  padding:13px;
  margin-top:8px;
  border-radius:10px;
  border:1px solid #ccd3dc;
  font-size:16px;
}

button{
  background:#007aff;
  color:white;
  border:0;
  cursor:pointer;
  font-weight:bold;
}

button:hover{opacity:.9}

.tabs{
  display:grid;
  grid-template-columns:repeat(5,1fr);
  gap:8px;
}

.tabs button{
  background:#e9eef5;
  color:#172033;
}

.tabs button.active{
  background:#007aff;
  color:white;
}

.grid{
  display:grid;
  grid-template-columns:repeat(2,1fr);
  gap:12px;
}

.result{
  background:#eef7ff;
  border-right:5px solid #007aff;
  padding:15px;
  border-radius:10px;
  margin-top:15px;
  font-size:18px;
}

.project{
  border:1px solid #ddd;
  padding:12px;
  border-radius:10px;
  margin-top:10px;
}

.danger{background:#e53935}
.secondary{background:#555}
.success{background:#159447}

.hidden{display:none}

footer{
  text-align:center;
  padding:25px;
  color:#666;
}

@media(max-width:700px){
  .grid{grid-template-columns:1fr}
  .tabs{grid-template-columns:repeat(2,1fr)}
}
</style>
</head>

<body>

<header>
  <h1>🏗️ Civil Engineer — Abed Osama</h1>
  <p>Engineering calculations and project management</p>
</header>

<div class="container">

<div class="card">
  <h2>🌐 Language / اللغة</h2>
  <select id="language" onchange="changeLanguage()">
    <option value="ar">العربية</option>
    <option value="en">English</option>
    <option value="fr">Français</option>
  </select>
</div>

<div class="card">
  <h2>📁 Project / المشروع</h2>

  <input id="projectName" placeholder="اسم المشروع">

  <button onclick="createProject()">➕ إنشاء مشروع</button>

  <div id="projects"></div>
</div>

<div class="card">
  <h2>🧮 Engineering Calculator</h2>

  <div class="tabs">
    <button class="active" onclick="showTab('concrete',this)">خرسانة</button>
    <button onclick="showTab('steel',this)">حديد</button>
    <button onclick="showTab('sand',this)">رمل</button>
    <button onclick="showTab('aggregate',this)">حصى</button>
    <button onclick="showTab('cement',this)">إسمنت</button>
  </div>

  <!-- CONCRETE -->
  <div id="concrete" class="calc">

    <h3>📐 حساب حجم الخرسانة</h3>

    <div class="grid">
      <div>
        <label>الطول (m)</label>
        <input type="number" id="cLength" step="0.01">
      </div>

      <div>
        <label>العرض (m)</label>
        <input type="number" id="cWidth" step="0.01">
      </div>

      <div>
        <label>الارتفاع / السماكة (m)</label>
        <input type="number" id="cHeight" step="0.01">
      </div>
    </div>

    <button onclick="calculateConcrete()">احسب الخرسانة</button>

    <div id="concreteResult" class="result hidden"></div>
  </div>

  <!-- STEEL -->
  <div id="steel" class="calc hidden">

    <h3>🔩 حساب كمية الحديد</h3>

    <div class="grid">

      <div>
        <label>قطر الحديد (mm)</label>
        <input type="number" id="steelDiameter" value="12">
      </div>

      <div>
        <label>عدد القضبان</label>
        <input type="number" id="steelBars" value="10">
      </div>

      <div>
        <label>طول القضيب (m)</label>
        <input type="number" id="steelLength" value="12">
      </div>

      <div>
        <label>نسبة الهدر (%)</label>
        <input type="number" id="steelWaste" value="5">
      </div>

    </div>

    <button onclick="calculateSteel()">احسب الحديد</button>

    <div id="steelResult" class="result hidden"></div>
  </div>

  <!-- SAND -->
  <div id="sand" class="calc hidden">

    <h3>🏖️ حساب الرمل</h3>

    <div class="grid">

      <div>
        <label>حجم الخرسانة (m³)</label>
        <input type="number" id="sandConcrete">
      </div>

      <div>
        <label>معامل الرمل</label>
        <input type="number" id="sandFactor" value="0.50" step="0.01">
      </div>

    </div>

    <button onclick="calculateSand()">احسب الرمل</button>

    <div id="sandResult" class="result hidden"></div>
  </div>

  <!-- AGGREGATE -->
  <div id="aggregate" class="calc hidden">

    <h3>🪨 حساب الحصى / Aggregate</h3>

    <div class="grid">

      <div>
        <label>حجم الخرسانة (m³)</label>
        <input type="number" id="aggregateConcrete">
      </div>

      <div>
        <label>معامل الحصى</label>
        <input type="number" id="aggregateFactor" value="0.80" step="0.01">
      </div>

    </div>

    <button onclick="calculateAggregate()">احسب الحصى</button>

    <div id="aggregateResult" class="result hidden"></div>
  </div>

  <!-- CEMENT -->
  <div id="cement" class="calc hidden">

    <h3>🧱 حساب الإسمنت</h3>

    <div class="grid">

      <div>
        <label>حجم الخرسانة (m³)</label>
        <input type="number" id="cementConcrete">
      </div>

      <div>
        <label>كمية الإسمنت kg/m³</label>
        <input type="number" id="cementRate" value="350">
      </div>

      <div>
        <label>وزن الكيس (kg)</label>
        <input type="number" id="bagWeight" value="50">
      </div>

    </div>

    <button onclick="calculateCement()">احسب الإسمنت</button>

    <div id="cementResult" class="result hidden"></div>
  </div>

</div>

<div class="card">
  <h2>💾 العمليات المحفوظة</h2>
  <div id="savedCalculations">
    لا توجد عمليات محفوظة.
  </div>
</div>

<div class="card">
  <h2>🖨️ التقرير</h2>

  <button class="success" onclick="printReport()">
    🖨️ طباعة / حفظ PDF
  </button>

  <button class="secondary" onclick="clearAll()">
    🗑️ حذف جميع البيانات
  </button>
</div>

</div>

<footer>
  Civil Engineer — Abed Osama
</footer>

<script>

let projects =
JSON.parse(localStorage.getItem("abedProjectsV2")) || [];

let currentProject = null;

let calculations =
JSON.parse(localStorage.getItem("abedCalculations")) || [];


/* =========================
   PROJECTS
========================= */

function saveProjects(){
  localStorage.setItem(
    "abedProjectsV2",
    JSON.stringify(projects)
  );
}

function createProject(){

  const name =
    document.getElementById("projectName").value.trim();

  if(!name){
    alert("أدخل اسم المشروع");
    return;
  }

  const project={
    id:Date.now(),
    name:name,
    date:new Date().toLocaleString()
  };

  projects.push(project);
  currentProject=project.id;

  saveProjects();
  renderProjects();

  document.getElementById("projectName").value="";
}

function renderProjects(){

  const box=document.getElementById("projects");

  box.innerHTML="";

  if(projects.length===0){
    box.innerHTML="<p>لا توجد مشاريع.</p>";
    return;
  }

  projects.forEach(project=>{

    const div=document.createElement("div");

    div.className="project";

    div.innerHTML=`
      <strong>📁 ${escapeHtml(project.name)}</strong>
      <br>
      <small>${project.date}</small>
      <br><br>

      <button onclick="selectProject(${project.id})">
        فتح المشروع
      </button>

      <button class="danger"
        onclick="deleteProject(${project.id})">
        حذف
      </button>
    `;

    box.appendChild(div);
  });
}

function selectProject(id){

  currentProject=id;

  const project=
    projects.find(p=>p.id===id);

  if(project){

    alert(
      "تم فتح المشروع: " +
      project.name
    );

  }
}

function deleteProject(id){

  if(!confirm("هل تريد حذف المشروع؟")) return;

  projects=
    projects.filter(p=>p.id!==id);

  calculations=
    calculations.filter(c=>c.projectId!==id);

  saveProjects();

  saveCalculations();

  renderProjects();

  renderCalculations();
}


/* =========================
   CALCULATORS
========================= */

function calculateConcrete(){

  const L=num("cLength");
  const W=num("cWidth");
  const H=num("cHeight");

  if(L<=0 || W<=0 || H<=0){
    alert("أدخل قيم صحيحة");
    return;
  }

  const result=L*W*H;

  showResult(
    "concreteResult",
    `حجم الخرسانة = <b>${result.toFixed(3)} m³</b>`
  );

  saveCalculation(
    "الخرسانة",
    `الحجم = ${result.toFixed(3)} m³`
  );
}


function calculateSteel(){

  const diameter=num("steelDiameter");
  const bars=num("steelBars");
  const length=num("steelLength");
  const waste=num("steelWaste");

  if(
    diameter<=0 ||
    bars<=0 ||
    length<=0
  ){
    alert("أدخل قيم صحيحة");
    return;
  }

  /*
    وزن المتر kg/m
    = القطر² / 162
  */

  const kgPerMeter=
    (diameter*diameter)/162;

  const base=
    kgPerMeter*bars*length;

  const total=
    base*(1+waste/100);

  showResult(
    "steelResult",
    `
    وزن المتر = <b>${kgPerMeter.toFixed(3)} kg/m</b><br>
    الكمية الإجمالية = <b>${total.toFixed(2)} kg</b>
    `
  );

  saveCalculation(
    "الحديد",
    `الكمية = ${total.toFixed(2)} kg`
  );
}


function calculateSand(){

  const concrete=num("sandConcrete");
  const factor=num("sandFactor");

  if(concrete<=0 || factor<=0){
    alert("أدخل قيم صحيحة");
    return;
  }

  const result=
    concrete*factor;

  showResult(
    "sandResult",
    `
    كمية الرمل التقديرية =
    <b>${result.toFixed(3)} m³</b>
    `
  );

  saveCalculation(
    "الرمل",
    `الكمية = ${result.toFixed(3)} m³`
  );
}


function calculateAggregate(){

  const concrete=
    num("aggregateConcrete");

  const factor=
    num("aggregateFactor");

  if(concrete<=0 || factor<=0){
    alert("أدخل قيم صحيحة");
    return;
  }

  const result=
    concrete*factor;

  showResult(
    "aggregateResult",
    `
    كمية الحصى التقديرية =
    <b>${result.toFixed(3)} m³</b>
    `
  );

  saveCalculation(
    "الحصى",
    `الكمية = ${result.toFixed(3)} m³`
  );
}


function calculateCement(){

  const concrete=
    num("cementConcrete");

  const rate=
    num("cementRate");

  const bagWeight=
    num("bagWeight");

  if(
    concrete<=0 ||
    rate<=0 ||
    bagWeight<=0
  ){
    alert("أدخل قيم صحيحة");
    return;
  }

  const kg=
    concrete*rate;

  const bags=
    kg/bagWeight;

  showResult(
    "cementResult",
    `
    الإسمنت = <b>${kg.toFixed(2)} kg</b><br>
    عدد الأكياس = <b>${Math.ceil(bags)}</b> كيس
    `
  );

  saveCalculation(
    "الإسمنت",
    `${kg.toFixed(2)} kg — ${Math.ceil(bags)} كيس`
  );
}


/* =========================
   RESULTS
========================= */

function showResult(id,html){

  const box=
    document.getElementById(id);

  box.innerHTML=html;

  box.classList.remove("hidden");
}


/* =========================
   SAVE CALCULATIONS
========================= */

function saveCalculation(type,result){

  const project=
    projects.find(
      p=>p.id===currentProject
    );

  const projectName=
    project
    ? project.name
    : "بدون مشروع";

  calculations.push({

    id:Date.now(),

    projectId:currentProject,

    projectName:projectName,

    type:type,

    result:result,

    date:new Date().toLocaleString()

  });

  saveCalculations();

  renderCalculations();
}

function saveCalculations(){

  localStorage.setItem(
    "abedCalculations",
    JSON.stringify(calculations)
  );
}

function renderCalculations(){

  const box=
    document.getElementById(
      "savedCalculations"
    );

  if(calculations.length===0){

    box.innerHTML=
      "لا توجد عمليات محفوظة.";

    return;
  }

  box.innerHTML="";

  calculations
    .slice()
    .reverse()
    .forEach(c=>{

      const div=
        document.createElement("div");

      div.className="project";

      div.innerHTML=`

        <strong>
          ${escapeHtml(c.type)}
        </strong>

        <br>

        المشروع:
        ${escapeHtml(c.projectName)}

        <br>

        النتيجة:
        ${escapeHtml(c.result)}

        <br>

        <small>${c.date}</small>

        <br><br>

        <button class="danger"
          onclick="deleteCalculation(${c.id})">
          حذف
        </button>

      `;

      box.appendChild(div);

    });
}

function deleteCalculation(id){

  calculations=
    calculations.filter(c=>c.id!==id);

  saveCalculations();

  renderCalculations();
}


/* =========================
   TABS
========================= */

function showTab(tab,button){

  document
    .querySelectorAll(".calc")
    .forEach(x=>
      x.classList.add("hidden")
    );

  document
    .getElementById(tab)
    .classList.remove("hidden");

  document
    .querySelectorAll(".tabs button")
    .forEach(x=>
      x.classList.remove("active")
    );

  button.classList.add("active");
}


/* =========================
   LANGUAGE
========================= */

function changeLanguage(){

  const lang=
    document.getElementById("language").value;

  if(lang==="en"){

    document.documentElement.lang="en";
    document.documentElement.dir="ltr";

    alert(
      "English mode selected. The calculator remains fully functional."
    );

  }
  else if(lang==="fr"){

    document.documentElement.lang="fr";
    document.documentElement.dir="ltr";

    alert(
      "Mode français sélectionné. La calculatrice reste fonctionnelle."
    );

  }
  else{

    document.documentElement.lang="ar";
    document.documentElement.dir="rtl";

  }
}


/* =========================
   PRINT / PDF
========================= */

function printReport(){

  let html=`

  <html dir="rtl">

  <head>

  <meta charset="UTF-8">

  <title>Engineering Report</title>

  <style>

  body{
    font-family:Arial;
    padding:30px;
  }

  h1{
    color:#007aff;
  }

  table{
    width:100%;
    border-collapse:collapse;
    margin-top:20px;
  }

  th,td{
    border:1px solid #ccc;
    padding:10px;
  }

  th{
    background:#eee;
  }

  </style>

  </head>

  <body>

  <h1>
  Civil Engineer — Abed Osama
  </h1>

  <h2>Engineering Report</h2>

  <table>

  <tr>
    <th>Project</th>
    <th>Type</th>
    <th>Result</th>
    <th>Date</th>
  </tr>
  `;

  calculations.forEach(c=>{

    html+=`

    <tr>

      <td>${escapeHtml(c.projectName)}</td>

      <td>${escapeHtml(c.type)}</td>

      <td>${escapeHtml(c.result)}</td>

      <td>${escapeHtml(c.date)}</td>

    </tr>

    `;

  });

  html+=`

  </table>

  </body>

  </html>
  `;

  const win=
    window.open("","_blank");

  if(!win){

    alert(
      "المتصفح منع نافذة الطباعة. اسمح بالنوافذ المنبثقة."
    );

    return;
  }

  win.document.write(html);

  win.document.close();

  win.focus();

  setTimeout(
    ()=>win.print(),
    500
  );
}


/* =========================
   UTILITIES
========================= */

function num(id){

  return Number(
    document.getElementById(id).value
  );
}

function escapeHtml(value){

  return String(value)
    .replace(/&/g,"&amp;")
    .replace(/</g,"&lt;")
    .replace(/>/g,"&gt;")
    .replace(/"/g,"&quot;")
    .replace(/'/g,"&#039;");
}

function clearAll(){

  if(!confirm(
    "هل أنت متأكد من حذف جميع المشاريع والحسابات؟"
  )) return;

  projects=[];
  calculations=[];
  currentProject=null;

  localStorage.removeItem(
    "abedProjectsV2"
  );

  localStorage.removeItem(
    "abedCalculations"
  );

  renderProjects();
  renderCalculations();

  alert("تم حذف جميع البيانات.");
}


/* =========================
   START
========================= */

renderProjects();
renderCalculations();

</script>

</body>
</html>
