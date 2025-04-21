## 🧠 Camada **Domínio da Lógica** no Test.AI

### 📌 Descrição

A **camada de Domínio da Lógica** no **Test.AI** é responsável por conter as **regras de negócio** para o funcionamento de um sistema. Fundamental para garantir que todas as ações de interpretação de dados e geração de arquivos de testes sejam feitas de forma correta e eficiente.

Essa camada é legal por ser **independente de frameworks e tecnologias externas**, isolando a lógica de negócio central do resto do sistema, o que facilita testes, manutenção e modificações sem impactar outras partes do projeto.

---


### ✅ Objetivo da Camada de Domínio da Lógica

O principal objetivo dessa camada é **isolamento das regras de negócio** das camadas superiores (como interface de usuário ou infraestrutura de APIs), garantindo que as regras de negócio possam ser facilmente reutilizadas e adaptadas sem afetar outras partes do sistema. Essa separação facilita o **teste independente** da lógica e permite que ela seja **refatorada sem impacto** nas dependências externas.

---


### 🔍 Principais Responsabilidades e Funcionalidades

| **Responsabilidade**                  | **Descrição**                                                                                                                                                          |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Interpretação de Gherkin e Arquivos .andes** | Responsável por processar os arquivos brutos, transformando-os em um formato que o sistema consiga manipular e utilizar para gerar testes.    |
| **Regras de Negócio**                | Contém as lógicas específicas para validar, transformar e estruturar os dados, garantindo que os códigos gerados, como os arquivos de teste em Gherkin, sejam corretos. |
| **Geradores de Códigos**             | Gera automaticamente os **cenários de teste BDD** em **Gherkin**, utilizando os dados de entrada para criar arquivos que possam ser executados de forma eficiente.      |

<br>
<br>

### 🔧 Exemplos de Funcionalidade

| **Função**                            | **Descrição**                                                                                             |
|---------------------------------------|-----------------------------------------------------------------------------------------------------------|
| **Parsing de Dados**                  | Realiza o *parsing* dos dados de entrada, garantindo que estejam no formato correto para gerar cenários.   |
| **Transformação de Dados**            | Organiza e valida os dados, assegurando que as informações necessárias para gerar os testes estejam completas. |
| **Geração de Testes**                 | Gera automaticamente os arquivos de teste em *Gherkin* a partir dos dados estruturados.                   |

---

### 📁 **Camada de Domínio:** *`crew_gherkin.py`*

#### ✅ **Responsabilidade**

Esse módulo é responsável por **gerar e revisar arquivos `.feature` no estilo BDD (Behavior Driven Development)** com auxílio de agentes que se comunicam por meio de tarefas e interagem com uma LLM.

---

#### ⚙️ **Como funciona**

1. **Inicialização de Modelos LLM**:
   - Usa duas configurações de LLM (temperaturas diferentes): uma mais criativa (`temp=0.6`) e outra mais precisa (default, `temp=0.0`).
   - As funções `init_llm`, `init_agent` e `init_task` são importadas de `module.py`.

2. **Ciclo de Geração em Rodadas**:
   - Roda três iterações para gerar e revisar arquivos `.feature`.
   - Em cada rodada:
     dddddddddddddddddd- Um agente “**gherkin_writer**” escreve o código Gherkin.
     - Um agente “**gherkin_reviewer**” revisa o código gerado.
     - Ambos são configurados dinamicamente com base no turno (ex: `rodada_1`, `rodada_2`, etc.).

3. **Definição de Tarefas**:
   - Tarefas são criadas a partir de descrições dinâmicas (`tasks_dict`), onde o `user_case` é inserido no texto da tarefa para contextualização.

4. **Uso de uma Estrutura de "Crew"**:
   - Ao que tudo indica (com base no nome das classes `Agent`, `Task`, `Crew`), está utilizando a biblioteca `crewai`, que estrutura o uso de múltiplos agentes colaborativos.

---

### 🧠 Inteligência Artificial

A integração com LLM permite que esses agentes gerem conteúdo mais natural, completo e alinhado com os padrões do Gherkin, mesmo com uma entrada simples como um caso de uso (`user_case`).

---

### ✨ Conclusão

Esse script representa um componente da **Camada de Domínio** que automatiza a **criação colaborativa de testes BDD** com uso de inteligência artificial e múltiplos agentes especializados. É aqui que reside a lógica principal para **converter requisitos textuais em testes executáveis** com validação automatizada.

---

### 🚀 Conclusão Geral

A **Clean Architecture** aplicada ao **Test.AI** traz uma estrutura sólida e flexível, isolando as regras de negócio no **Domínio da Lógica**. A camada de **Domínio** permite que a lógica central seja desenvolvida e testada independentemente, o que facilita manutenções e adaptações do sistema sem impactar outras camadas. O uso de múltiplos agentes e integração com modelos LLM torna o sistema robusto e escalável, permitindo a automação na criação de testes de alta qualidade.

---

Se precisar de mais detalhes sobre outros arquivos, como o `crew_xUnit.py` ou o `debate_agentes.py`, posso continuar a análise e a explicação dessa camada de domínio. Me avise!