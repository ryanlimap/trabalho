## 🏛️ Arquitetura Adotada
Estilo Arquitetural: Clean Architecture

Clean Architecture é uma estrutura de design de software com várias camadas, promovendo uma estrutura organizada e de fácil compreensão, o que é benéfico para o desenvolvimento.

Sua principal característica é a separação e independência das camadas, como o desacoplamento da lógica de negócios do sistema de influências externas como o sistema de interface do usuário (UI), frameworks, bancos de dados e assim por diante. Isso é alcançado definindo uma camada de domínio independente e isolada.

🧠 Princípios Fundamentais da Clean Architecture:
- Independência de tecnologia: O núcleo do sistema (regras de negócio) não conhece detalhes de frameworks, bibliotecas ou I/O.

- Ordem de dependência: O fluxo de dependência sempre aponta para o centro — interfaces externas dependem do domínio, e nunca o contrário.

- Regras de negócio isoladas: Permite reaproveitamento em outros contextos (ex: CLI, APIs, interfaces gráficas).

A principal ideia da Clean Architecture é separar o código em camadas concêntricas, onde:

🔄 As dependências sempre apontam para dentro:

```
+------------------------+
|      External Layer    | <- Interface com o usuário, web, banco, etc.
+------------------------+
|    Interface Adapters  | <- Controllers, Gateways, Presenters
+------------------------+
|     Use Cases Layer    | <- Regras de negócio da aplicação
+------------------------+
|   Entities (Core)      | <- Regras de negócio mais genéricas
+------------------------+
```

🧱 As camadas:
- Frameworks & Drivers (camada externa):
Onde ficam os frameworks, banco de dados, UI, serviços externos, etc.

- Interface Adapters:
Camada que adapta os dados para entrada/saída (ex: controllers, presenters, repositórios).

- Use Cases:
Casos de uso da aplicação, orquestram as regras para resolver problemas específicos do domínio.

- Entities:
Contém as regras de negócio mais genéricas e independentes de tecnologia.

## 🧩 Aplicação no contexto do Test.AI:

| Camada | Descrição | Exemplos |
|----------|----------|----------|
| Interface  | Camada de interação com o usuário. Usa a API do VS Code para capturar ações como clique direito.  | Comandos como "Generate BDD", "Generate Steps"  |
| Aplicação  | Camada que define os fluxos principais e regras de orquestração dos dados.  | Script que decide como gerar arquivos a partir dos dados fornecidos.  |
| Domínio  | Contém as regras de negócio puras, como interpretação do .andes e geração dos testes.  | Classes e funções Python que fazem parsing e estruturam os dados.  |
| Infraestrutura  | Responsável por interagir com o sistema operacional, arquivos, APIs externas, .env.  | Integração com Gemini, leitura de .env, gravação de arquivos.  |

## 🌐 Tecnologias no Front-end vs Back-end

Camada	Tecnologia	Descrição
Front-end	VS Code Extension (TypeScript)	Responsável pela interação com o usuário e acionamento dos comandos.
Back-end	Python (test-ai-leds)	Responsável por processar os dados, interpretar arquivos e gerar os códigos.

## 📚 Referências Bibliográficas

adicionar os links da galera depois ***(refs.md)***

## 🔍 Pontos de Melhoria com Base na Arquitetura
✅ O que já é bom:
- Baixo acoplamento entre VS Code e a lógica de geração (via Python).

- Alta coesão nas funcionalidades automatizadas.

- Modularidade facilita manutenção e evolução.

- Adoção de IA para enriquecer geração de código com contexto inteligente.

## ⚠️ Pontos de Melhoria:
Documentação de Interfaces

- Melhorar a especificação do contrato entre extensão VS Code e test-ai-leds (ex: entrada esperada, formatos de resposta).

- Sugestão: Usar Pydantic ou JSON Schema para estruturar e validar dados trocados.

- Gerenciamento de Logs

- Atualmente os erros são difíceis de rastrear.

- Sugestão: Implementar sistema de log com níveis (INFO, ERROR) usando logging no Python e console no TypeScript.

- Testabilidade

- Criar testes automatizados unitários para os scripts de geração.

- Utilizar mocks para testes de integração com API externa.

- Plugabilidade de LLMs

- Hoje o sistema é acoplado à Gemini.

- Sugestão: Abstrair o serviço de LLM para suportar outras APIs (OpenAI, Anthropic, etc.).

- UX da Extensão

- Inserir feedback visual após a geração de código (ex: "Arquivo gerado com sucesso").

- Melhorar mensagens de erro quando .env ou outros arquivos estão ausentes ou mal configurados.