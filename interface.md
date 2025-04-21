## 🖥️ Interface no Test.AI

### 📌 Descrição
A **camada de Interface** é responsável por interagir diretamente com o **usuário final**. No projeto Test.AI, essa interação é realizada por meio de uma aplicação em **Streamlit**, que serve como a camada de apresentação visual, exibindo os dados gerados pelas APIs e capturando comandos do usuário.

Essa camada não processa lógica de negócio, mas atua como ponte entre o usuário e a aplicação.

---

### 🔍 Trechos do Código Relacionados à Interface

**Arquivo:** `src/scripts/comparacao.py`

| Trecho de Código | Descrição | Função na Interface |
|------------------|-----------|---------------------|
| `import streamlit as st` | Importa a biblioteca de interface gráfica. | Inicializa a camada de interface web. |
| `user_input = data_json['payload']` | Carrega a entrada do usuário a partir de um JSON. | Captura o dado a ser enviado para as APIs. |
| `if st.button("Enviar"):` | Cria o botão de envio. | Dispara o processamento ao clicar. |
| `col1, col2 = st.columns([1, 1])` | Cria duas colunas visuais na interface. | Divide as respostas do modelo "Debate" e "Sequencial". |
| `st.session_state['messages'].append(...)` | Armazena as mensagens da sessão. | Controla o histórico da interação. |
| `st.write(...)` | Exibe as respostas e entrada do usuário. | Mostra os dados na tela para o usuário. |
| `if st.button("Limpar Conversa"):` | Cria botão de limpeza da sessão. | Reseta a interface e o histórico da conversa. |

---

### ✅ Resumo

A camada de Interface no Test.AI atua como um **painel de controle visual** da aplicação. Ela é responsável por:

- **Receber dados de entrada do usuário**
- **Enviar esses dados para APIs externas (Debate e Sequencial)**
- **Exibir os resultados recebidos de forma clara e organizada**
- **Manter o histórico da sessão de forma interativa**
- **Resetar a interface sob demanda**
