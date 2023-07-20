<!DOCTYPE html>
<svelte:head>
	<title>Formulário</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
<h1>Formulário Svelte - 1º projeto</h1>
<p>Preencha os dados abaixo:</p>
</section>

<body>
	<form METHOD='post' id="myForm">
		<label for="nome">Nome: </label>
		<input type="text" id="nome" name="nome"><br><br>
	<p>Gênero:</p>
		<input type="radio" id="masculino" name="gênero" value="Masculino">
		<label for="masculino">Masculino</label>
		<input type="radio" id="feminino" name="gênero" value="Feminino">
		<label for="feminino">Feminino</label><br><br>
		<label for="nascimento">Data de nascimento: </label>
		<input type="date" id="nascimento" name="nascimento" min="1930-01-01" max="2016-12-30"><br><br>
		<button type="button" id="saveButton">Salvar</button>
		<button type="button" id="loadButton">Carregar json</button>
		<div id="dataContainer"></div>
	</form>

<script>
	 document.getElementById('saveButton').addEventListener('click', function() {
      var form = document.getElementById('myForm');
      var formData = new FormData(form);
      var jsonObject = {};

      for (const [key, value] of formData.entries()) {
        jsonObject[key] = value;
      }

      var jsonString = JSON.stringify(jsonObject);
      
      // Aqui você pode enviar o JSON para o servidor, armazená-lo localmente ou fazer qualquer outra ação necessária.
      
      // Exemplo: download do JSON
      var element = document.createElement('a');
      element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(jsonString));
      element.setAttribute('download', 'data.json');
      element.style.display = 'none';
      document.body.appendChild(element);
      element.click();
      document.body.removeChild(element);
    });

	document.getElementById('loadButton').addEventListener('click', function() {
      var xhr = new XMLHttpRequest();
      xhr.open('GET', 'C:\Users\Downloads\data.json', true);  // substitua 'caminho/do/arquivo.json' pelo caminho correto para o seu arquivo JSON - corrigir e apagar comentarios do chatgpt
      
      xhr.onload = function() {
        if (xhr.status === 200) {
          var data = JSON.parse(xhr.responseText);
          showData(data);
        }
      };
      
      xhr.send();
    });

    //a partir daqui nao funciona, é o cod do botao visualizar

    function showData(data) {
      var container = document.getElementById('dataContainer');
      container.innerHTML = '';
      
      for (var key in data) {
        if (data.hasOwnProperty(key)) {
          var value = data[key];
          var paragraph = document.createElement('p');
          paragraph.textContent = key + ': ' + value;
          container.appendChild(paragraph);
        }
      }
    }
</script>
	<p>Agradecemos sua participação!</p>
</body>

<style>
	h1 {
		padding-block: 1em;
		font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
		font-style:oblique;
		font-size: 1.5em;
		background-color: rgb(123, 184, 234);
	}
	* {
		text-align: center;
		justify-content:center;
		color:black;
		font-family:'Times New Roman', Times, serif;
		font-size: 1.1em;
	}
</style>