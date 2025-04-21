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