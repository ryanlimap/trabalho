## 🖥️ Dominío no Test.AI

### 📌 Descrição

A **camada de Domínio da Lógica** no **Test.AI** é responsável por conter as **regras de negócio** para o funcionamento de um sistema. Fundamental para garantir que todas as ações de interpretação de dados e geração de arquivos de testes sejam feitas de forma correta e eficiente.

Essa camada é **independente de frameworks e tecnologias externas**, isolando a lógica de negócio central do resto do sistema, o que facilita testes, manutenção e modificações sem impactar outras partes do projeto.

---

### 🔍 **Como funciona**

1. **Inicialização de Modelos LLM**:
   - Usa duas configurações de LLM (temperaturas diferentes): uma mais criativa (`temp=0.6`) e outra mais precisa (default, `temp=0.0`).
   - As funções `init_llm`, `init_agent` e `init_task` são importadas de `module.py`.

2. **Ciclo de Geração em Rodadas**:
   - Roda três iterações para gerar e revisar arquivos `.feature`.
   - Em cada rodada:
     - Um agente “**gherkin_writer**” escreve o código Gherkin.
     - Um agente “**gherkin_reviewer**” revisa o código gerado.
     - Ambos são configurados dinamicamente com base no turno (ex: `rodada_1`, `rodada_2`, etc.).

3. **Definição de Tarefas**:
   - Tarefas são criadas a partir de descrições dinâmicas (`tasks_dict`), onde o `user_case` é inserido no texto da tarefa para contextualização.

4. **Uso de uma Estrutura de "Crew"**:
   - Ao que tudo indica (com base no nome das classes `Agent`, `Task`, `Crew`), está utilizando a biblioteca `crewai`, que estrutura o uso de múltiplos agentes colaborativos.

#### 🧠 Inteligência Artificial

A integração com LLM permite que esses agentes gerem conteúdo mais natural, completo e alinhado com os padrões do Gherkin, mesmo com uma entrada simples como um caso de uso (`user_case`).

---

### ✅ Resumo

Esse script representa um componente da **Camada de Domínio** que automatiza a **criação colaborativa de testes BDD** com uso de inteligência artificial e múltiplos agentes especializados. É aqui que reside a lógica principal para **converter requisitos textuais em testes executáveis** com validação automatizada.
