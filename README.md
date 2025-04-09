# formulario-inscricao-2-
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulário de Inscrição</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Inscrição</h1>
        <form id="formInscricao">
            <input type="text" id="nome" placeholder="Nome" required>
            <input type="email" id="email" placeholder="E-mail" required>
            <input type="text" id="idade" placeholder="Idade" required>
            <input type="text" id="idUsuario" placeholder="ID do Usuário" required>
            <input type="password" id="senha" placeholder="Senha" required>
            <button type="submit">Salvar</button>
        </form>
        <div id="mensagemErro" class="hidden"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.container {
    background: white;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

input {
    width: 100%;
    padding: 10px;
    margin: 10px 0;
    border: 1px solid #ccc;
    border-radius: 3px;
}

button {
    width: 100%;
    padding: 10px;
    background-color: #28a745;
    color: white;
    border: none;
    border-radius: 3px;
    cursor: pointer;
}

button:hover {
    background-color: #218838;
}

.hidden {
    display: none;
}
document.getElementById('formInscricao').addEventListener('submit', function(event) {
    event.preventDefault();

    const nome = document.getElementById('nome').value;
    const email = document.getElementById('email').value;
    const idade = document.getElementById('idade').value;
    const idUsuario = document.getElementById('idUsuario').value;
    const senha = document.getElementById('senha').value;
    const mensagemErro = document.getElementById('mensagemErro');

    // Validação de e-mail
    if (!validarEmail(email)) {
        mensagemErro.textContent = 'E-mail inválido!';
        mensagemErro.classList.remove('hidden');
        return;
    }

    // Validação da idade
    if (isNaN(idade) || idade <= 0) {
        mensagemErro.textContent = 'Idade deve ser um número positivo!';
        mensagemErro.classList.remove('hidden');
        return;
    }

    // Armazenamento no LocalStorage
    const usuario = {
        nome,
        email,
        idade,
        idUsuario,
        senha
    };
    localStorage.setItem('usuario', JSON.stringify(usuario));

    alert('Inscrição realizada com sucesso!');
    mensagemErro.classList.add('hidden');
});

function validarEmail(email) {
    const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return regex.test(email);
}
