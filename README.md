# DataFut – Agente Inteligente para Partidas do Brasileirão Série A
Desafio fruto do curso da Microsoft em parceria com WoMakersCode de estudo sobre Microsoft Azure Foundry.

## 📌 Objetivo do Projeto
O **DataFut** foi criado para resolver uma dor comum: a dificuldade de acompanhar as transmissões dos jogos do Campeonato Brasileiro Série A, devido à fragmentação dos meios de transmissão (TV aberta, canais pagos, streaming).

Este projeto reúne:
- Um **agente inteligente** desenvolvido no **Azure Foundry**.
- Um **arquivo JSON** com todas as partidas, horários e canais de transmissão.
- Uma **interface HTML** simples para visualização dos dados.

---

## 🛠 Tecnologias Utilizadas
- **Azure Foundry** (para criação do agente conversacional).
- **Azure Blob Storage** (para hospedar o arquivo JSON com SAS Token).
- **Azure CLI** (para gerar SAS Token e gerenciar recursos).
- **GitHub** (para versionamento e documentação).
- **HTML + JavaScript** (para exibir os dados do JSON).
- **Microsoft Paint** (para formatação de imagens de printscreen)
- **Visual Studio Code** (para criação e visualização dos códigos HTML e JSON)

---

## 📂 Estrutura do Projeto
```
/DataFut
│
├── data/                     # Arquivo JSON com partidas
├── web/                      # Interface HTML para visualização
├── src/                      # Código do agente e lógica de integração
├── prints/                   # Prints das etapas no Azure Foundry
└── README.md                 # Documentação completa
```

---

## 📑 Etapas do Projeto

### 1. Criação do JSON
- As informações foram obtidas a partir da API do [football-data.org](https://www.football-data.org/).
- O JSON contém:
  - **Data** (ex.: `28/11`)
  - **Horário** (ex.: `19h00`)
  - **Partida** (ex.: `Juventude x Bahia`)
  - **Transmissão** (ex.: `Premiere`)

Exemplo:
```json
{
  "28/11": [
    {
      "horário": "19h00",
      "partida": "Juventude x Bahia",
      "transmissão": "Premiere"
    }
  ]
}
```

---

### 2. Criação do HTML
Arquivo: `web/partidas_brasileirao.html`
- Lê o JSON dinamicamente via JavaScript.
- Exibe os dados em uma tabela organizada por **Data | Horário | Partida | Transmissão**.

Exemplo:
```html
<script>
async function carregarPartidas() {
    const response = await fetch('partidas_brasileirao_corrigido.json');
    const dados = await response.json();
    const tbody = document.querySelector('#tabela-partidas tbody');

    for (const data in dados) {
        dados[data].forEach(partida => {
            const tr = document.createElement('tr');
            tr.innerHTML = `
                <td>${data}</td>
                <td>${partida['horário']}</td>
                <td>${partida['partida']}</td>
                <td>${partida['transmissão']}</td>
            `;
            tbody.appendChild(tr);
        });
    }
}
carregarPartidas();
</script>
```

---

### 3. Criação do Agente no Azure Foundry
- Nome do agente: **DataFut**.
- Função: Responder perguntas sobre partidas do Brasileirão Série A.
- Fonte de dados: JSON hospedado no Azure Blob Storage com SAS Token.

**Prompt do agente:**
```
Você é um assistente especializado em partidas do Campeonato Brasileiro Série A 2025.
Use exclusivamente os dados fornecidos no Knowledge (arquivo JSON).
Responda perguntas sobre:
- Data e horário das partidas.
- Times que jogam em determinada data.
- Onde assistir (transmissão).
Se a pergunta não estiver relacionada ao Brasileirão Série A, responda:
"Desculpe, só posso responder sobre partidas do Campeonato Brasileiro Série A."
Alguns exemplos de como responder são:
Exemplo 1:
Usuário: "Quais jogos acontecem no dia 28/11?"
Agente: "No dia 28/11 teremos: Juventude x Bahia às 19h00 (Premiere), Vasco da Gama x Internacional às 19h30 (Amazon), Santos x Sport às 21h30 (SporTV, Amazon)."
Exemplo 2:
Usuário: "Qual o horário do jogo São Paulo x Internacional?"
Agente: "São Paulo x Internacional será no dia 03/12 às 20h00, transmissão: sem informações."
Exemplo 3:
Usuário: "Onde assistir Flamengo x Ceará?"
Agente: "Flamengo x Ceará será no dia 03/12 às 21h30, transmissão: Globo."
Exemplo 4 (fora do escopo):
Usuário: "Qual a previsão do tempo para amanhã?"
Agente: "Desculpe, só posso responder sobre partidas do Campeonato Brasileiro Série A 2025."
Você deve responder de maneira gentil, mas objetiva. 
```

**Exemplos de perguntas:**
- "Quais jogos acontecem no dia 28/11?"
- "Qual o horário do jogo São Paulo x Internacional?"
- "Onde assistir Flamengo x Ceará?"

---

### 4. Prints das Etapas no Azure Foundry
**Criação de agente:**
<img width="1331" height="644" alt="criaçãoagente" src="https://github.com/user-attachments/assets/64eda2da-322a-4d4d-95a6-a6a1aa1848dd" />


**Criação de Storage Account:**
<img width="1366" height="639" alt="criaçãostorageaccount" src="https://github.com/user-attachments/assets/22702f81-0354-4b46-88a4-b4b567f70181" />


**Upload no Container Blob:**
<img width="1366" height="626" alt="uploadcontainerblob" src="https://github.com/user-attachments/assets/ccac3ad2-61bd-47bd-836d-e07eae32deb0" />


**Upload arquivo JSON na Storage Account:**
<img width="1366" height="768" alt="uploadjsonblob" src="https://github.com/user-attachments/assets/bbd56c26-2251-4f11-bc16-e29a8bf9d8d4" />


**Criação de Storage SAS Token:**
<img width="1366" height="570" alt="criaçãoblobsastoken" src="https://github.com/user-attachments/assets/ec3cc281-bc3d-4ca0-9d55-977fe767ecca" />


**Teste do agente DataFut:**
<img width="1349" height="654" alt="testeagenteplayground" src="https://github.com/user-attachments/assets/6feaedcb-3197-41a9-9854-c8f48b2b296f" />


---

## 🤖 Desenvolvido com Ajuda do Microsoft Copilot
Este projeto foi construído com suporte do **Microsoft Copilot**, que auxiliou na geração de código, criação de arquivos e automação das etapas de desenvolvimento, garantindo agilidade e qualidade na entrega.

## 📌 Próximos Passos
- Adicionar filtros no HTML.
- Criar busca dinâmica.


