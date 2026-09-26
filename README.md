<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>DS5 | PS5 DNS HUB</title>

<style>
*{box-sizing:border-box;margin:0;padding:0}

body{
font-family:Tahoma,Arial,sans-serif;
background:#05070b;
color:#fff;
min-height:100vh;
}

header{
padding:18px 7%;
display:flex;
justify-content:space-between;
align-items:center;
border-bottom:1px solid #ffffff15;
background:#070a0fcc;
backdrop-filter:blur(15px);
position:sticky;
top:0;
z-index:5;
}

.logo{
font-size:32px;
font-weight:900;
letter-spacing:4px;
color:#62ff9b;
text-shadow:0 0 25px #00ff88;
}

.status{
color:#62ff9b;
font-size:13px;
}

.hero{
text-align:center;
padding:70px 20px 40px;
}

.hero h1{
font-size:clamp(60px,15vw,110px);
letter-spacing:10px;
background:linear-gradient(90deg,#fff,#62ff9b,#fff);
-webkit-background-clip:text;
color:transparent;
}

.hero p{
color:#8995a6;
margin-top:15px;
}

.container{
max-width:900px;
margin:auto;
padding:20px;
}

.card{
background:#0b1119;
border:1px solid #ffffff12;
border-radius:22px;
padding:22px;
margin-bottom:20px;
box-shadow:0 15px 50px #0008;
}

input{
width:100%;
padding:14px;
margin:7px 0;
border-radius:12px;
border:1px solid #ffffff15;
background:#05080d;
color:#fff;
outline:none;
}

button{
border:0;
border-radius:11px;
padding:11px 16px;
font-weight:bold;
cursor:pointer;
}

.green{
background:#62ff9b;
color:#031008;
}

.red{
background:#ff4d5a;
color:white;
}

.blue{
background:#4da6ff;
color:white;
}

.dns{
display:flex;
align-items:center;
justify-content:space-between;
gap:10px;
background:#05080d;
padding:15px;
border-radius:14px;
margin-top:10px;
direction:ltr;
font-family:monospace;
}

.actions{
display:flex;
gap:8px;
direction:rtl;
}

.hidden{
display:none;
}

.search{
margin-bottom:15px;
}

.admin-title{
display:flex;
justify-content:space-between;
align-items:center;
margin-bottom:15px;
}

footer{
text-align:center;
padding:40px;
color:#596575;
}

@media(max-width:600px){
.dns{
flex-direction:column;
align-items:stretch;
}
.actions{
justify-content:center;
}
}
</style>
</head>

<body>

<header>
<div class="logo">DS5</div>
<div class="status">● ONLINE</div>
</header>

<section class="hero">
<h1>DS5</h1>
<p>PS5 DNS HUB 🎮</p>
</section>

<div class="container">

<!-- ورود -->
<div class="card" id="loginBox">
<h2>🔐 ورود به DS5</h2>

<input id="phone" placeholder="شماره تلفن">

<button class="green" style="width:100%;margin-top:8px"
onclick="login()">
ورود
</button>

<p id="loginMsg" style="color:#ff6670;margin-top:10px"></p>
</div>


<!-- سایت -->
<div id="site" class="hidden">

<div class="card">
<h2 style="margin-bottom:15px">📡 DNS های DS5</h2>

<input
class="search"
id="search"
placeholder="🔎 جستجوی DNS..."
oninput="render()">

<div id="dnsList"></div>
</div>


<!-- پنل مدیریت -->
<div class="card">

<div class="admin-title">
<h2>⚙️ پنل مدیریت</h2>
<span>ADMIN</span>
</div>

<input id="adminPass"
placeholder="رمز مدیریت"
type="password">

<button class="blue" onclick="adminLogin()">
ورود مدیر
</button>

<p id="adminMsg" style="margin-top:10px"></p>

<div id="adminPanel" class="hidden">

<hr style="border-color:#ffffff15;margin:20px 0">

<h3>➕ افزودن DNS</h3>

<input id="dnsName" placeholder="نام DNS">
<input id="dnsPrimary" placeholder="DNS اصلی">
<input id="dnsSecondary" placeholder="DNS دوم">

<button class="green"
onclick="addDNS()"
style="width:100%;margin-top:5px">
افزودن DNS
</button>

</div>

</div>

</div>

</div>

<footer>
© 2026 DS5 — PS5 DNS HUB 🎮
</footer>


<script>

let dns = [
{
name:"Cloudflare",
primary:"1.1.1.1",
secondary:"1.0.0.1"
},
{
name:"Google",
primary:"8.8.8.8",
secondary:"8.8.4.4"
},
{
name:"Quad9",
primary:"9.9.9.9",
secondary:"149.112.112.112"
}
];

function login(){

let phone=document.getElementById("phone").value.trim();

if(!phone){
document.getElementById("loginMsg").innerText=
"شماره تلفن را وارد کن.";
return;
}

document.getElementById("loginBox").classList.add("hidden");
document.getElementById("site").classList.remove("hidden");

render();
}

function render(){

let search=
document.getElementById("search").value.toLowerCase();

let list=dns.filter(x=>
x.name.toLowerCase().includes(search) ||
x.primary.includes(search) ||
x.secondary.includes(search)
);

let box=document.getElementById("dnsList");

box.innerHTML="";

list.forEach((x,index)=>{

box.innerHTML+=`

<div class="card">

<h3>🎮 ${x.name}</h3>

<div class="dns">
<span>${x.primary}</span>

<div class="actions">

<button class="green"
onclick="copyDNS('${x.primary}')">
کپی
</button>

<button class="red"
onclick="deleteDNS(${index})">
حذف
</button>

</div>
</div>

<div class="dns">
<span>${x.secondary}</span>

<div class="actions">

<button class="green"
onclick="copyDNS('${x.secondary}')">
کپی
</button>

</div>
</div>

</div>

`;

});

}

function adminLogin(){

let pass=document.getElementById("adminPass").value;

if(pass==="DS5ADMIN"){

document.getElementById("adminPanel")
.classList.remove("hidden");

document.getElementById("adminMsg").innerText=
"✅ ورود مدیر موفق بود";

}else{

document.getElementById("adminMsg").innerText=
"❌ رمز اشتباه است";

}

}

function addDNS(){

let name=document.getElementById("dnsName").value.trim();
let primary=document.getElementById("dnsPrimary").value.trim();
let secondary=document.getElementById("dnsSecondary").value.trim();

if(!name || !primary || !secondary){
alert("همه قسمت‌ها را پر کن.");
return;
}

dns.push({
name:name,
primary:primary,
secondary:secondary
});

document.getElementById("dnsName").value="";
document.getElementById("dnsPrimary").value="";
document.getElementById("dnsSecondary").value="";

render();

alert("✅ DNS اضافه شد!");
}

function deleteDNS(index){

if(confirm("این DNS حذف شود؟")){

dns.splice(index,1);

render();

}

}

function copyDNS(value){

navigator.clipboard.writeText(value);

alert("✅ کپی شد: "+value);

}

</script>

</body>
</html>
