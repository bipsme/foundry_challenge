# DataFut – Agente Inteligente para Partidas do Brasileirão Série A

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
```

**Exemplos de perguntas:**
- "Quais jogos acontecem no dia 28/11?"
- "Qual o horário do jogo São Paulo x Internacional?"
- "Onde assistir Flamengo x Ceará?"

---

### 4. Prints das Etapas no Azure Foundry


---

## 🚀 Como Executar

### Pré-requisitos
- Conta no Azure.
- Azure CLI instalado.
- Git instalado.

### Passos
1. Clone o repositório:
```bash
git clone https://github.com/<usuario>/DataFut.git
cd DataFut
```
2. Abra `web/partidas_brasileirao.html` no navegador.
3. Configure o agente no Azure Foundry usando o prompt e a URL do JSON com SAS.



## 🤖 Desenvolvido com Ajuda do Microsoft Copilot
Este projeto foi construído com suporte do **Microsoft Copilot**, que auxiliou na geração de código, criação de arquivos e automação das etapas de desenvolvimento, garantindo agilidade e qualidade na entrega.

## 📌 Próximos Passos
- Adicionar filtros no HTML.
- Criar busca dinâmica.


