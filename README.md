<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>MEGARABATY – Kody dnia i miesiąca</title>
<meta name="description" content="MEGARABATY – najlepsze kody rabatowe dnia i miesiąca. Sprawdzone promocje do sklepów online.">

<style>
:root{
    --blue:#0d6efd;
    --blue-dark:#084298;
    --light:#f4f8ff;
}

body{
    margin:0;
    font-family: Arial, sans-serif;
    background:var(--light);
}

/* HEADER */
header{
    background:linear-gradient(90deg,var(--blue),var(--blue-dark));
    color:#fff;
    padding:30px 15px;
    text-align:center;
}

/* TABS */
.tabs{
    display:flex;
    justify-content:center;
    background:#fff;
    border-bottom:2px solid var(--blue);
}
.tabs button{
    padding:15px 25px;
    border:none;
    background:none;
    font-weight:bold;
    cursor:pointer;
}
.tabs button.active{
    color:var(--blue);
    border-bottom:4px solid var(--blue);
}

/* CONTAINER */
.container{
    max-width:1100px;
    margin:25px auto;
    padding:0 15px;
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(280px,1fr));
    gap:20px;
}

/* CARD */
.card{
    background:#fff;
    border-radius:10px;
    box-shadow:0 6px 20px rgba(0,0,0,0.08);
    padding:15px;
    display:flex;
    flex-direction:column;
}

.card img{
    width:100%;
    height:150px;
    object-fit:contain;
    background:#fff;
    margin-bottom:10px;
}

.card h3{
    margin:5px 0;
}

.code{
    background:#eef4ff;
    padding:10px;
    text-align:center;
    font-weight:bold;
    border-radius:6px;
    margin:10px 0;
    letter-spacing:2px;
}

.actions{
    margin-top:auto;
    display:flex;
    gap:8px;
    flex-wrap:wrap;
}

.actions button,
.actions a{
    flex:1;
    text-align:center;
    padding:10px;
    border:none;
    border-radius:6px;
    cursor:pointer;
    font-weight:bold;
    text-decoration:none;
}

.copy{
    background:var(--blue);
    color:#fff;
}

.cart{
    background:#198754;
    color:#fff;
}

.shop{
    background:#6c757d;
    color:#fff;
}

/* KOSZYK */
#cartBox{
    max-width:1100px;
    margin:30px auto;
    background:#fff;
    padding:20px;
    border-radius:10px;
    box-shadow:0 5px 15px rgba(0,0,0,0.1);
}

.cart-item{
    display:flex;
    justify-content:space-between;
    margin-bottom:8px;
}

/* FOOTER */
footer{
    background:#0b2d5c;
    color:#fff;
    text-align:center;
    padding:20px;
    margin-top:40px;
}
</style>
</head>

<body>

<header>
    <h1>MEGARABATY 🔥</h1>
    <p>Profesjonalne kody rabatowe – kody dnia i miesiąca</p>
</header>

<!-- TABS -->
<div class="tabs">
    <button class="active" onclick="setTab('all',this)">Wszystkie</button>
    <button onclick="setTab('day',this)">Kody dnia</button>
    <button onclick="setTab('month',this)">Kody miesiąca</button>
</div>

<!-- CODES -->
<div class="container" id="codes"></div>

<!-- CART -->
<div id="cartBox">
    <h2>🛒 Koszyk kodów</h2>
    <div id="cart"></div>
    <button class="copy" onclick="copyCart()">Kopiuj wszystkie kody</button>
</div>

<footer>
    © 2026 MEGARABATY – najlepsze promocje online
</footer>

<script>
const codes = [
{
    shop:"Allegro",
    code:"ALLEGRO10",
    link:"https://allegro.pl",
    img:"https://upload.wikimedia.org/wikipedia/commons/5/5a/Allegro.pl_sklep_logo.png",
    type:"day"
},
{
    shop:"Media Expert",
    code:"MEDIA20",
    link:"https://mediaexpert.pl",
    img:"https://upload.wikimedia.org/wikipedia/commons/7/77/Media_Expert_logo.png",
    type:"month"
},
{
    shop:"Zalando",
    code:"ZALANDO15",
    link:"https://zalando.pl",
    img:"https://upload.wikimedia.org/wikipedia/commons/2/20/Zalando_Logo.png",
    type:"day"
}
];

let tab="all";
let cart=[];

const codesDiv=document.getElementById("codes");
const cartDiv=document.getElementById("cart");

function render(){
    codesDiv.innerHTML="";
    codes.filter(c=>tab==="all"||c.type===tab)
    .forEach(c=>{
        codesDiv.innerHTML+=`
        <div class="card">
            <img src="${c.img}">
            <h3>${c.shop}</h3>
            <div class="code">${c.code}</div>
            <div class="actions">
                <button class="copy" onclick="copyCode('${c.code}')">Kopiuj</button>
                <button class="cart" onclick="addCart('${c.shop}','${c.code}')">Koszyk</button>
                <a class="shop" href="${c.link}" target="_blank">Do sklepu</a>
            </div>
        </div>`;
    });
}

function setTab(t,btn){
    tab=t;
    document.querySelectorAll(".tabs button").forEach(b=>b.classList.remove("active"));
    btn.classList.add("active");
    render();
}

function copyCode(c){
    navigator.clipboard.writeText(c);
    alert("Skopiowano: "+c);
}

function addCart(shop,code){
    if(!cart.find(i=>i.code===code)){
        cart.push({shop,code});
        renderCart();
    }
}

function renderCart(){
    cartDiv.innerHTML="";
    cart.forEach(i=>{
        cartDiv.innerHTML+=`
        <div class="cart-item">
            ${i.shop} – ${i.code}
            <button onclick="removeCart('${i.code}')">❌</button>
        </div>`;
    });
}

function removeCart(code){
    cart=cart.filter(i=>i.code!==code);
    renderCart();
}

function copyCart(){
    if(cart.length===0){ alert("Koszyk pusty"); return;}
    navigator.clipboard.writeText(cart.map(i=>i.code).join(", "));
    alert("Skopiowano wszystkie kody");
}

render();
</script>

</body>
</html>
<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>MEGARABATY – Kody rabatowe dnia i miesiąca</title>
<meta name="description" content="MEGARABATY – najlepsze kody rabatowe online. Kody dnia, miesiąca i sprawdzone promocje do sklepów internetowych.">

<meta name="theme-color" content="#0d6efd">

<style>
:root{
--blue:#0d6efd;
--dark:#084298;
--bg:#f4f8ff;
}
body{margin:0;font-family:Arial;background:var(--bg);}
header{background:linear-gradient(90deg,var(--blue),var(--dark));color:#fff;padding:30px;text-align:center}
.tabs{display:flex;justify-content:center;background:#fff}
.tabs button{border:none;background:none;padding:15px 25px;font-weight:bold;cursor:pointer}
.tabs .active{color:var(--blue);border-bottom:4px solid var(--blue)}
.container{max-width:1200px;margin:30px auto;display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:20px;padding:0 15px}
.card{background:#fff;border-radius:12px;box-shadow:0 8px 25px rgba(0,0,0,.1);padding:15px;display:flex;flex-direction:column}
.card img{height:140px;object-fit:contain}
.code{background:#eaf1ff;padding:10px;text-align:center;font-weight:bold;margin:10px 0;border-radius:6px}
.actions{margin-top:auto;display:flex;gap:8px;flex-wrap:wrap}
.actions button,.actions a{flex:1;padding:10px;border:none;border-radius:6px;font-weight:bold;cursor:pointer;text-decoration:none;text-align:center}
.copy{background:var(--blue);color:#fff}
.cart{background:#198754;color:#fff}
.shop{background:#6c757d;color:#fff}
#cartBox{max-width:1200px;margin:20px auto;background:#fff;padding:20px;border-radius:10px}
.cart-item{display:flex;justify-content:space-between;margin-bottom:6px}
footer{background:#0b2d5c;color:#fff;text-align:center;padding:20px}
.admin{display:none;max-width:600px;margin:30px auto;background:#fff;padding:20px;border-radius:10px}
input,select{width:100%;padding:8px;margin-bottom:10px}
</style>
</head>

<body>

<header>
<h1>MEGARABATY 🔥</h1>
<p>Kody rabatowe dnia i miesiąca – oszczędzaj mądrze</p>
</header>

<div class="tabs">
<button class="active" onclick="setTab('all',this)">Wszystkie</button>
<button onclick="setTab('day',this)">Kody dnia</button>
<button onclick="setTab('month',this)">Kody miesiąca</button>
<button onclick="toggleAdmin()">Admin</button>
</div>

<div class="container" id="codes"></div>

<div id="cartBox">
<h2>🛒 Koszyk</h2>
<div id="cart"></div>
<button class="copy" onclick="copyCart()">Kopiuj wszystkie kody</button>
</div>

<!-- ADMIN -->
<div class="admin" id="admin">
<h2>Panel admina</h2>
<input id="ashop" placeholder="Sklep">
<input id="acode" placeholder="Kod">
<input id="alink" placeholder="Link afiliacyjny">
<input id="aimg" placeholder="Link do logo">
<select id="atype">
<option value="day">Kody dnia</option>
<option value="month">Kody miesiąca</option>
</select>
<button class="copy" onclick="addAdminCode()">Dodaj kod</button>
</div>

<footer>
© 2026 MEGARABATY – Profesjonalne kody rabatowe
</footer>

<script>
let codes = JSON.parse(localStorage.getItem("codes")) || [
{shop:"Allegro",code:"ALLEGRO10",link:"https://allegro.pl",img:"https://upload.wikimedia.org/wikipedia/commons/5/5a/Allegro.pl_sklep_logo.png",type:"day"},
{shop:"Zalando",code:"ZALANDO15",link:"https://zalando.pl",img:"https://upload.wikimedia.org/wikipedia/commons/2/20/Zalando_Logo.png",type:"month"}
];

let cart=[], tab="all";
const codesDiv=document.getElementById("codes");
const cartDiv=document.getElementById("cart");

function render(){
codesDiv.innerHTML="";
codes.filter(c=>tab==="all"||c.type===tab).forEach(c=>{
codesDiv.innerHTML+=`
<div class="card">
<img src="${c.img}">
<h3>${c.shop}</h3>
<div class="code">${c.code}</div>
<div class="actions">
<button class="copy" onclick="copyCode('${c.code}')">Kopiuj</button>
<button class="cart" onclick="addCart('${c.shop}','${c.code}')">Koszyk</button>
<a class="shop" href="${c.link}" target="_blank">Do sklepu</a>
</div>
</div>`;
});
}

function setTab(t,b){tab=t;document.querySelectorAll(".tabs button").forEach(x=>x.classList.remove("active"));b.classList.add("active");render();}
function copyCode(c){navigator.clipboard.writeText(c);alert("Skopiowano "+c);}
function addCart(s,c){if(!cart.find(x=>x.code===c)){cart.push({s,c});renderCart();}}
function renderCart(){cartDiv.innerHTML="";cart.forEach(i=>cartDiv.innerHTML+=`<div class="cart-item">${i.s} – ${i.c}<button onclick="removeCart('${i.c}')">❌</button></div>`);}
function removeCart(c){cart=cart.filter(x=>x.c!==c);renderCart();}
function copyCart(){navigator.clipboard.writeText(cart.map(x=>x.c).join(", "));alert("Skopiowano kody");}

function toggleAdmin(){document.getElementById("admin").style.display="block";}
function addAdminCode(){
codes.push({
shop:ashop.value,code:acode.value,link:alink.value,img:aimg.value,type:atype.value
});
localStorage.setItem("codes",JSON.stringify(codes));
render();
}

render();
</script>

</body>
</html>
<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<title>Polityka Prywatności – MEGARABATY</title>
</head>
<body>

<h1>Polityka Prywatności</h1>

<p>Serwis MEGARABATY szanuje prywatność użytkowników.</p>

<h2>1. Administrator danych</h2>
<p>Administratorem danych jest właściciel serwisu MEGARABATY.</p>

<h2>2. Dane osobowe</h2>
<p>Serwis nie zbiera danych osobowych użytkowników.</p>

<h2>3. Pliki cookies</h2>
<p>Strona korzysta z plików cookies w celach statystycznych i reklamowych.</p>

<h2>4. Google AdSense</h2>
<p>Na stronie mogą być wyświetlane reklamy Google AdSense, które wykorzystują pliki cookies do personalizacji reklam.</p>

<h2>5. Linki afiliacyjne</h2>
<p>Strona zawiera linki afiliacyjne prowadzące do sklepów zewnętrznych.</p>

<h2>6. Kontakt</h2>
<p>W sprawach związanych z polityką prywatności prosimy o kontakt mailowy.</p>

</body>
</html>
<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<title>Regulamin – MEGARABATY</title>
</head>
<body>

<h1>Regulamin serwisu MEGARABATY</h1>

<h2>1. Informacje ogólne</h2>
<p>Serwis MEGARABATY udostępnia informacje o kodach rabatowych.</p>

<h2>2. Odpowiedzialność</h2>
<p>Serwis nie gwarantuje poprawności ani aktualności kodów rabatowych.</p>

<h2>3. Zewnętrzne serwisy</h2>
<p>Serwis zawiera linki do stron trzecich, za które nie ponosi odpowiedzialności.</p>

<h2>4. Postanowienia końcowe</h2>
<p>Korzystanie z serwisu oznacza akceptację regulaminu.</p>

</body>
</html>
<p>
<a href="polityka-prywatnosci.html" style="color:white;">Polityka Prywatności</a> |
<a href="regulamin.html" style="color:white;">Regulamin</a>
</p>
<h2>O MEGARABATY</h2>
<p>Tutaj tekst… min. 500–800 słów.</p>
<h2>Jak działają kody rabatowe</h2>
<p>Treść instruktażowa 400–800 słów</p>
<h2>Dlaczego warto korzystać z kodów</h2>
<p>Tekst… dodatkowe akapity</p>
<section>
  <h2>O MEGARABATY</h2>
  <p>MEGARABATY to strona poświęcona kody rabatowym i promocjom online. Naszym celem jest...
  (tu min. kolejnych ~300–400 słów opisujących historię, cel strony, jak działają kody, jak korzystać itp.)
  </p>
</section>
<section>
  <h2>Jak działają kody rabatowe</h2>
  <p>Kody rabatowe pozwalają na obniżenie ceny zakupów w sklepach internetowych...
  (tu wpisz min. ~300–500 słów o mechanizmie, przykładach, wskazówkach itp.)
  </p>
</section>


