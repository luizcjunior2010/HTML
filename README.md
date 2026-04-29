<!DOCTYPE html><html lang="pt-br">
<head>
  <meta charset="UTF-8">
  <title>Organização de Armários</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      margin: 0;
      padding: 20px;
    }h1 {
  text-align: center;
}

.container {
  max-width: 900px;
  margin: auto;
}

.form-box {
  background: white;
  padding: 15px;
  border-radius: 10px;
  margin-bottom: 20px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.2);
}

input, textarea {
  width: 100%;
  margin: 5px 0;
  padding: 8px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

button {
  background: #28a745;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
}

.card {
  background: white;
  margin-bottom: 15px;
  padding: 15px;
  border-radius: 10px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.2);
}

img {
  max-width: 100%;
  border-radius: 10px;
  margin-top: 10px;
}

  </style>
</head>
<body><div class="container">
  <h1>Controle de Armários</h1>  <div class="form-box">
    <h3>Cadastrar Armário</h3>
    <input type="text" id="nome" placeholder="Nome do armário">
    <textarea id="itens" placeholder="Lista de itens"></textarea>
    <input type="file" id="foto" accept="image/*">
    <button onclick="adicionarArmario()">Adicionar</button>
  </div>  <div id="lista"></div>
</div><script>
function adicionarArmario() {
  const nome = document.getElementById('nome').value;
  const itens = document.getElementById('itens').value;
  const fotoInput = document.getElementById('foto');

  if (!nome) {
    alert('Digite o nome do armário');
    return;
  }

  const reader = new FileReader();

  reader.onload = function(e) {
    const lista = document.getElementById('lista');

    const card = document.createElement('div');
    card.className = 'card';

    card.innerHTML = `
      <h3>${nome}</h3>
      <p><strong>Itens:</strong><br>${itens.replace(/\n/g, '<br>')}</p>
      ${e.target.result ? `<img src="${e.target.result}">` : ''}
    `;

    lista.appendChild(card);

    document.getElementById('nome').value = '';
    document.getElementById('itens').value = '';
    document.getElementById('foto').value = '';
  }

  if (fotoInput.files[0]) {
    reader.readAsDataURL(fotoInput.files[0]);
  } else {
    reader.onload({ target: { result: null } });
  }
}
</script></body>
</html>
