# Primeira-tentativa-
Votação para a escola 
DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Votação</title>
    <style>
        body {
            background-color: #d3d3d3;
            font-family: Arial, sans-serif;
            text-align: center;
        }
        .header {
            background-color: red;
            color: white;
            padding: 15px;
            font-size: 24px;
            font-weight: bold;
        }
        .opcao {
            background-color: black;
            color: white;
            padding: 10px;
            margin: 10px auto;
            width: 300px;
            border-radius: 5px;
            cursor: pointer;
        }
        .selecionado {
            background-color: lightblue !important;
        }
        .votos {
            font-size: 20px;
            font-weight: bold;
        }
        .resultado {
            margin-top: 20px;
            padding: 15px;
            background-color: white;
            border-radius: 5px;
            display: block; /* Alterado para block */
        }
        .botao-votar {
            background-color: red;
            color: white;
            font-size: 20px;
            padding: 15px 30px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 20px;
        }
        .botao-votar:disabled {
            background-color: gray;
            cursor: not-allowed;
        }
    </style>
</head>
<body>
    <div class="header">VOTAÇÃO</div>
    <h3>Escolha sua opção:</h3>
    <form id="formVotacao">
        <div class="opcao" data-value="juventude">Juventude com Visão</div>
        <div class="opcao" data-value="jovens">Jovens em Ação</div>
        <div class="opcao" data-value="chapa">Chapa do Futuro</div>
        <div class="opcao" data-value="nova">Nova Era</div>
        <div class="opcao" data-value="lions">Lions</div><br>
        <button type="submit" class="botao-votar">Votar</button>
    </form>
    <div class="resultado" id="resultado">
        <h3>Resultados da Votação</h3>
        <h3>Total de votantes: <span id="totalVotos">0</span></h3>
        <div id="votos">
            <p>Juventude com Visão: <span class="votos" id="juventudeVotos">0</span></p>
            <p>Jovens em Ação: <span class="votos" id="jovensVotos">0</span></p>
            <p>Chapa do Futuro: <span class="votos" id="chapaVotos">0</span></p>
            <p>Nova Era: <span class="votos" id="novaVotos">0</span></p>
            <p>Lions: <span class="votos" id="lionsVotos">0</span></p>
        </div>
    </div>
    <script>
        let votos = { juventude: 0, jovens: 0, chapa: 0, nova: 0, lions: 0 };
        let totalVotos = 0;
        let votou = false;
        let opcaoSelecionada = null;

        document.querySelectorAll('.opcao').forEach(opcao => {
            opcao.addEventListener('click', function() {
                if (opcaoSelecionada) {
                    opcaoSelecionada.classList.remove('selecionado');
                }
                this.classList.add('selecionado');
                opcaoSelecionada = this;
            });
        });

        document.getElementById('formVotacao').addEventListener('submit', function(event) {
            event.preventDefault();
            if (votou) {
                alert("Você já votou!");
                return;
            }

            if (!opcaoSelecionada) {
                alert("Por favor, selecione uma opção para votar.");
                return;
            }

            let opcao = opcaoSelecionada.getAttribute('data-value');
            votos[opcao]++;
            totalVotos++;
            votou = true;
            
            document.getElementById('totalVotos').innerText = totalVotos;
            document.getElementById(opcao + 'Votos').innerText = votos[opcao];
            document.querySelector('.botao-votar').disabled = true; // Desabilita o botão após votar
            window.scrollTo({ top: document.getElementById('resultado').offsetTop, behavior: 'smooth' });
        });
    </script>
</body>
</html>
