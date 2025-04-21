## 🏛️ Arquitetura Adotada
Estilo Arquitetural: Clean Architecture
O projeto Test.AI adota o padrão Clean Architecture, proposto por Robert C. Martin (Uncle Bob), com o objetivo de tornar o sistema independente de frameworks, facilmente testável, facilmente adaptável a mudanças e com uma forte separação de responsabilidades.

🧠 Princípios Fundamentais da Clean Architecture:
- Independência de tecnologia: O núcleo do sistema (regras de negócio) não conhece detalhes de frameworks, bibliotecas ou I/O.

- Ordem de dependência: O fluxo de dependência sempre aponta para o centro — interfaces externas dependem do domínio, e nunca o contrário.

- Regras de negócio isoladas: Permite reaproveitamento em outros contextos (ex: CLI, APIs, interfaces gráficas).

## 🧱 Camadas da Arquitetura no Test.AI

```
 +---------------------------+
    |        Interface          |  <- Extensão VS Code (TypeScript)
    +---------------------------+
              ↓
    +---------------------------+
    |     Casos de Uso          |  <- Comandos de geração / orquestração
    +---------------------------+
              ↓
    +---------------------------+
    |     Domínio da Lógica     |  <- Regras de negócio em Python (interpretação .andes, geração de código)
    +---------------------------+
              ↓
    +---------------------------+
    |     Infraestrutura        |  <- APIs (LLMs), sistema de arquivos, variáveis de ambiente
    +---------------------------+
```

## 🧩 Aplicação no contexto do Test.AI:

| Camada | Descrição | Exemplos |
|----------|----------|----------|
| Interface  | Camada de interação com o usuário. Usa a API do VS Code para capturar ações como clique direito.  | Comandos como "Generate BDD", "Generate Steps"  |
| Aplicação  | Camada que define os fluxos principais e regras de orquestração dos dados.  | Script que decide como gerar arquivos a partir dos dados fornecidos.  |
| Domínio  | Contém as regras de negócio puras, como interpretação do .andes e geração dos testes.  | Classes e funções Python que fazem parsing e estruturam os dados.  |
| Infraestrutura  | Responsável por interagir com o sistema operacional, arquivos, APIs externas, .env.  | Integração com Gemini, leitura de .env, gravação de arquivos.  |
