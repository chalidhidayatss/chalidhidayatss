<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GREEN META</title>
<link rel="manifest" href="manifest.json">
<meta name="theme-color" content="#0f5132">

<style>
body{
  margin:0;
  font-family:Arial;
  background:#0b1f17;
  color:white;
}
header{
  background:#0f5132;
  padding:15px;
  text-align:center;
  font-weight:bold;
}
.container{
  padding:15px;
  padding-bottom:80px;
}
input, select{
  width:100%;
  padding:10px;
  margin-top:8px;
  border-radius:8px;
  border:none;
}
.card{
  background:#132e25;
  padding:15px;
  margin-bottom:15px;
  border-radius:12px;
}
button{
  background:#0f5132;
  border:none;
  color:white;
  padding:10px;
  width:100%;
  border-radius:8px;
  margin-top:10px;
}
footer{
  position:fixed;
  bottom:0;
  width:100%;
  display:flex;
  background:#0f5132;
}
footer button{
  flex:1;
  border-radius:0;
}
</style>
</head>
<body>

<header>GREEN META</header>

<div class="container">

<div class="card">
<h3>Cari Hero</h3>
<input type="text" id="searchHero" placeholder="Ketik nama hero..." onkeyup="searchHero()">
<p id="heroList"></p>
</div>

<div class="card">
<h3>Counter Hero</h3>
<select id="heroSelect"></select>
<button onclick="showCounter()">Lihat Counter</button>
<p id="counterResult"></p>
</div>

<div class="card">
<h3>Counter Item</h3>
<select id="enemyType">
<option value="lifesteal">Lifesteal Tinggi</option>
<option value="magic">Burst Magic</option>
<option value="crit">Critical Tinggi</option>
<option value="tank">Tank Tebal</option>
</select>
<button onclick="showItem()">Rekomendasi Item</button>
<p id="itemResult"></p>
</div>

<div class="card">
<h3>Rekomendasi Emblem</h3>
<select id="roleType">
<option value="Mage">Mage</option>
<option value="Fighter">Fighter</option>
<option value="Tank">Tank</option>
<option value="Assassin">Assassin</option>
<option value="Marksman">Marksman</option>
<option value="Support">Support</option>
</select>
<button onclick="showEmblem()">Lihat Emblem</button>
<p id="emblemResult"></p>
</div>

</div>

<footer>
<button onclick="location.reload()">Home</button>
</footer>

<script>
const heroes = [
"Alucard","Miya","Layla","Tigreal","Eudora","Gusion","Lancelot",
"Franco","Esmeralda","Chou","Saber","Karina","Angela","Valir",
"Harith","Granger","Balmond","Zilong","Aldous","Claude"
];

const counterData = {
"Alucard":"Gunakan hero CC berat seperti Franco atau Chou.",
"Gusion":"Gunakan Tank tebal dan Athena Shield.",
"Lancelot":"Gunakan hero stun cepat & burst.",
"Claude":"Gunakan hero burst dan item anti-attack speed.",
"default":"Gunakan hero dengan crowd control tinggi."
};

function loadHeroes(){
let select = document.getElementById("heroSelect");
heroes.forEach(hero=>{
let option=document.createElement("option");
option.value=hero;
option.textContent=hero;
select.appendChild(option);
});
}
loadHeroes();

function searchHero(){
let input=document.getElementById("searchHero").value.toLowerCase();
let filtered=heroes.filter(hero=>hero.toLowerCase().includes(input));
document.getElementById("heroList").innerText=filtered.join(", ");
}

function showCounter(){
let hero=document.getElementById("heroSelect").value;
let result=counterData[hero] || counterData["default"];
document.getElementById("counterResult").innerText=result;
}

function showItem(){
let type=document.getElementById("enemyType").value;
let result="";
if(type==="lifesteal") result="Dominance Ice / Necklace of Durance.";
if(type==="magic") result="Athena Shield / Radiant Armor.";
if(type==="crit") result="Blade Armor.";
if(type==="tank") result="Demon Hunter Sword / Malefic Roar.";
document.getElementById("itemResult").innerText=result;
}

function showEmblem(){
let role=document.getElementById("roleType").value;
let result=role+" Emblem dengan talent sesuai meta terbaru.";
document.getElementById("emblemResult").innerText=result;
}

if ('serviceWorker' in navigator) {
navigator.serviceWorker.register('service-worker.js');
}
</script>

</body>
</html>