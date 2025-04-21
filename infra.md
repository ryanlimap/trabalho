## 🖥️ Infraestrutura no Test.AI

### 📌 Descrição

Este módulo define a infraestrutura backend do Test.AI utilizando o FastAPI como framework principal, com suporte a CORS, tratamento de requisições REST e integração com modelos de linguagem (LLMs) através da biblioteca crewai. O foco principal é o recebimento de eventos via POST, que são processados por agentes inteligentes para gerar arquivos de especificação de testes em formato Gherkin (BDD). Os resultados são orquestrados, revisados e consolidados por múltiplos agentes para produzir um artefato final de teste.

***CORS é um mecanismo usado para adicionar cabeçalhos HTTP que informam aos navegadores para permitir que uma aplicação Web seja executada em uma origem e acesse recursos de outra origem diferente.***

---

### 🔍 Trechos do Código Relacionados à Interface

**Arquivo:** `src/app/main.py`

```
crew = Crew(
    agents=agents + [manager],
    tasks=tasks + [final_task],
    max_rpm=10,
    output_log_file="crew_log.txt",
    manager_llm=llm_low_temp,
    process=Process.sequential,
    verbose=True
)
```
- Este trecho define a Crew com múltiplos agentes (writers, reviewers e manager) e suas respectivas tarefas. O processo é executado de forma sequencial, e os logs são salvos em crew_log.txt. A CrewAI orquestra toda a execução das tarefas com uso de LLMs configurados dinamicamente.

```
load_dotenv()
```

- Carrega as variáveis de ambiente a partir de um arquivo .env. Isso é essencial para o funcionamento correto da aplicação, especialmente para o uso de chaves de API como a GOOGLE_API_KEY necessária para configurar os LLMs utilizados pelos agentes da CrewAI.

```
@app.get("/")
async def home():
    return "Rodando"
```

- Este endpoint básico verifica se a aplicação está no ar.

```
@app.post("/gherkin")
async def generate_gherkin_file(evento: Evento):
    feature = generate_gherkin_feature(evento.evento)
    body = {
        "feature": feature
    }
    return JSONResponse(body)
```

- O endpoint /gherkin é o principal ponto de entrada para a geração de arquivos de teste. Ele recebe um JSON com um campo evento, que será transformado em uma feature Gherkin através da função generate_gherkin_feature.

- A função generate_gherkin_feature cria múltiplos agentes (writers e revisores), cada um com funções específicas na construção e verificação de cenários de teste. Um agente gerente sintetiza os melhores resultados em um único arquivo .feature.

---

### ✅ Resumo

- Backend criado com FastAPI, com suporte a CORS.

- Utilização da biblioteca CrewAI para orquestrar agentes inteligentes baseados em LLMs (modelo Gemini via GOOGLE_API_KEY).

- Entrada via POST em /gherkin recebe eventos e os transforma em cenários BDD (Gherkin).

- O processo de geração envolve múltiplos agentes:

- Escritores e revisores de cenários Gherkin.

- Um gerente que unifica as versões geradas.

- Resultado final é salvo em arquivo .feature e registrado em log (crew_log.txt).
