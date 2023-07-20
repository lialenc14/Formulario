<!DOCTYPE html>
<svelte:head>
    <title>Visualizar Respostas</title>
</svelte:head>
<body>
    <input type="file" id="fileInput" accept=".json">
    <button id="handleFile()">Carregar Arquivo JSON</button>
    <div id="dataDisplay"></div>
    <button id="showDataAsText()">Exibir Dados como Texto</button>

<script>
let jsonData; // Variável global para armazenar os dados do arquivo JSON

function handleFile() {
    const fileInput = document.getElementById('fileInput');

    const file = fileInput.files[0];
    const reader = new FileReader();

    reader.onload = function(event) {
        jsonData = JSON.parse(event.target.result);
        alert('Arquivo JSON carregado com sucesso!');
    }

    reader.readAsText(file);
}

function showDataAsText() {
    if (!jsonData) {
        alert('Por favor, carregue o arquivo JSON primeiro.');
        return;
    }

    const dataDisplay = document.getElementById('dataDisplay');
    dataDisplay.innerHTML = `<pre>${JSON.stringify(jsonData, null, 2)}</pre>`;
}
</script>
</body>