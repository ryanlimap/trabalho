## Arquitetura Adotada
🏛️ Estilo Arquitetural: Clean Architecture
A extensão e biblioteca Test.AI adotam princípios da Clean Architecture, promovendo uma forte separação de responsabilidades e alta testabilidade.

🎯 Objetivo:
Garantir que regras de negócio estejam desacopladas de frameworks, interfaces de usuário, banco de dados ou qualquer tecnologia externa.

## 🧱 Componentes e Camadas
1. Camada de Interface (Interface Adapters)
Responsabilidade: Conectar os inputs dos usuários (VS Code) ao domínio da aplicação.

Tecnologias usadas:

Visual Studio Code API: Utilizada para registrar comandos no menu de contexto.

Extensão escrita em TypeScript.

Comunicação com arquivos .env, .andes, .feature e .cs.

2. Camada de Aplicação (Use Cases)
Responsabilidade: Orquestrar os fluxos de geração de código conforme a ação do usuário.

Tecnologias usadas:

Biblioteca Python test-ai-leds, que é chamada pela extensão para gerar os códigos.

Scripts que interpretam os arquivos de entrada e decidem o comportamento da geração.

3. Camada de Domínio
Responsabilidade: Contém a lógica central e regras de negócio do sistema.

Tecnologias usadas:

Lógica de interpretação dos arquivos .andes para BDD.

Geração de arquivos .feature, .cs, testes Cypress e unitários baseada em estrutura semântica.

Integração com LLMs via API (ex: Gemini) para enriquecer a geração automática com inteligência artificial.

4. Camada de Infraestrutura
Responsabilidade: Faz a ponte com o mundo externo (APIs, sistemas de arquivos).

Tecnologias usadas:

Chamadas HTTP para LLMs (Gemini ou outro).

Manipulação de arquivos e diretórios locais.

Configuração por meio do .env.

## 🌐 Tecnologias no Front-end vs Back-end

Camada	Tecnologia	Descrição
Front-end	VS Code Extension (TypeScript)	Responsável pela interação com o usuário e acionamento dos comandos.
Back-end	Python (test-ai-leds)	Responsável por processar os dados, interpretar arquivos e gerar os códigos.

## 📚 Referências Bibliográficas
Martin, R. C. (2017). Clean Architecture: A Craftsman's Guide to Software Structure and Design. Prentice Hall.

Fowler, M. (2003). Patterns of Enterprise Application Architecture. Addison-Wesley.

Google Developers. Documentação Gemini API

VS Code API Docs: https://code.visualstudio.com/api

PEP8 - Python Enhancement Proposal: https://peps.python.org/pep-0008/

## 🔍 Pontos de Melhoria com Base na Arquitetura
✅ O que já é bom:
Baixo acoplamento entre VS Code e a lógica de geração (via Python).

Alta coesão nas funcionalidades automatizadas.

Modularidade facilita manutenção e evolução.

Adoção de IA para enriquecer geração de código com contexto inteligente.

## ⚠️ Pontos de Melhoria:
Documentação de Interfaces

Melhorar a especificação do contrato entre extensão VS Code e test-ai-leds (ex: entrada esperada, formatos de resposta).

Sugestão: Usar Pydantic ou JSON Schema para estruturar e validar dados trocados.

Gerenciamento de Logs

Atualmente os erros são difíceis de rastrear.

Sugestão: Implementar sistema de log com níveis (INFO, ERROR) usando logging no Python e console no TypeScript.

Testabilidade

Criar testes automatizados unitários para os scripts de geração.

Utilizar mocks para testes de integração com API externa.

Plugabilidade de LLMs

Hoje o sistema é acoplado à Gemini.

Sugestão: Abstrair o serviço de LLM para suportar outras APIs (OpenAI, Anthropic, etc.).

UX da Extensão

Inserir feedback visual após a geração de código (ex: "Arquivo gerado com sucesso").

Melhorar mensagens de erro quando .env ou outros arquivos estão ausentes ou mal configurados.