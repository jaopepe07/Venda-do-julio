# Venda-do-julio
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Vendas do Julio</title>

<style>
body {
    font-family: Arial, sans-serif;
    margin: 0;
    background: #f4f6f9;
}

header {
    background: #0d6efd;
    color: white;
    padding: 20px;
    text-align: center;
}

nav {
    display: flex;
    justify-content: center;
    gap: 10px;
    padding: 10px;
}

input, select {
    padding: 8px;
}

.produtos {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 20px;
    padding: 20px;
}

.produto {
    background: white;
    padding: 15px;
    width: 250px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

.produto img {
    width: 100%;
    border-radius: 8px;
}

button {
    background: #198754;
    color: white;
    border: none;
    padding: 10px;
    width: 100%;
    cursor: pointer;
    border-radius: 6px;
}

button:hover {
    opacity: 0.9;
}

.carrinho {
    position: fixed;
    top: 20px;
    right: 20px;
    background: white;
    padding: 15px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0,0,0,0.2);
}

footer {
    background: #222;
    color: white;
    text-align: center;
    padding: 15px;
}
</style>
</head>

<body>

<header>
<h1>Vendas do Julio</h1>
<p>Os melhores eletrodomésticos com entrega rápida!</p>
</header>

<nav>
<input type="text" id="busca" placeholder="Buscar produto...">
<select id="filtro">
<option value="todos">Todos</option>
<option value="geladeira">Geladeiras</option>
<option value="lavadora">Lavadoras</option>
<option value="microondas">Micro-ondas</option>
</select>
</nav>

<div class="carrinho">
🛒 Carrinho: <span id="contador">0</span> itens  
<br><br>
<button onclick="finalizarCompra()">Finalizar</button>
</div>

<section class="produtos" id="produtos"></section>

<footer>
© 2026 Vendas do Julio - Todos os direitos reservados
</footer>

<script>
const produtos = [
{nome:"Geladeira 400L Inox", preco:2499, categoria:"geladeira", img:"https://via.placeholder.com/250?text=Geladeira"},
{nome:"Lavadora 12kg Turbo", preco:1799, categoria:"lavadora", img:"https://via.placeholder.com/250?text=Lavadora"},
{nome:"Micro-ondas 30L", preco:549, categoria:"microondas", img:"https://via.placeholder.com/250?text=Microondas"},
{nome:"Geladeira Duplex 500L", preco:3299, categoria:"geladeira", img:"https://via.placeholder.com/250?text=Geladeira+500L"},
{nome:"Lavadora 15kg Digital", preco:2299, categoria:"lavadora", img:"https://via.placeholder.com/250?text=Lavadora+15kg"}
];

let carrinho = [];

function renderizar(lista) {
const container = document.getElementById("produtos");
container.innerHTML = "";

lista.forEach(prod => {
container.innerHTML += `
<div class="produto">
<img src="${prod.img}">
<h3>${prod.nome}</h3>
<p><strong>R$ ${prod.preco}</strong></p>
<button onclick="adicionarCarrinho('${prod.nome}', ${prod.preco})">Comprar</button>
<a href="https://wa.me/5511999999999?text=Olá%20quero%20comprar%20${prod.nome}" target="_blank">
<button style="background:#25D366;margin-top:5px;">WhatsApp</button>
</a>
</div>`;
});
}

function adicionarCarrinho(nome, preco){
carrinho.push({nome, preco});
document.getElementById("contador").innerText = carrinho.length;
}

function finalizarCompra(){
if(carrinho.length === 0){
alert("Carrinho vazio!");
return;
}
let total = carrinho.reduce((acc, item) => acc + item.preco, 0);
alert("Compra finalizada! Total: R$ " + total);
carrinho = [];
document.getElementById("contador").innerText = 0;
}

document.getElementById("busca").addEventListener("input", e=>{
const termo = e.target.value.toLowerCase();
const filtrado = produtos.filter(p=>p.nome.toLowerCase().includes(termo));
renderizar(filtrado);
});

document.getElementById("filtro").addEventListener("change", e=>{
if(e.target.value === "todos"){
renderizar(produtos);
} else {
renderizar(produtos.filter(p=>p.categoria === e.target.value));
}
});

renderizar(produtos);
</script>

</body>
</html>
