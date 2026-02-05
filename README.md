# 👁️ OmniSight: RAG Architecture & Multi-Agent Orchestration

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)
![AI Framework](https://img.shields.io/badge/Framework-CrewAI%20%7C%20LangGraph-orange)
![Architecture](https://img.shields.io/badge/Architecture-RAG-green)
![Status](https://img.shields.io/badge/Status-R%26D%20%2F%20Portfolio-lightgrey)

> **Uma abordagem de Engenharia de Qualidade para Sistemas Generativos.**

## 📖 Sobre o Projeto
O **OmniSight** é um projeto de Pesquisa & Desenvolvimento (P&D) focado na criação de uma arquitetura robusta para sistemas de **RAG (Retrieval-Augmented Generation)** orquestrados por agentes autônomos.

Diferente de implementações padrão de chatbots, o foco deste projeto é a **Engenharia de Confiabilidade**: como garantir que agentes de IA tomem decisões determinísticas e que o contexto recuperado seja preciso, aplicando princípios de **QA e Testes Automatizados** em pipelines de Machine Learning.

---

## 🏗️ Arquitetura do Sistema

O sistema utiliza um padrão de orquestração multi-agente para decompor perguntas complexas e validar a precisão das respostas antes da entrega ao usuário.

```mermaid
graph TD
    User[Usuário] -->|Query Complexa| Router[Agent Router]
    
    subgraph "Agentes Especialistas (CrewAI)"
        Router -->|Busca Técnica| TechAgent[Agente Técnico]
        Router -->|Busca de Negócio| BizAgent[Agente de Negócio]
        Router -->|Análise de Dados| DataAgent[Agente de Análise]
    end
    
    subgraph "Pipeline RAG"
        TechAgent & BizAgent -->|Retrieval| VectorDB[(Vector DB)]
        VectorDB -->|Contexto Relevante| Reranker[Re-Ranker Model]
    end
    
    Reranker -->|Contexto Refinado| Generator[LLM Generator]
    Generator -->|Draft de Resposta| Validator[Agente QA / Guardrails]
    
    Validator -->|Aprovado| User
    Validator -->|Alucinação Detectada| Router

🛠️ Tech Stack
 * Linguagem: Python 3.10+
 * Orquestração de Agentes: CrewAI / LangGraph
 * Framework de LLM: LangChain
 * Vector Database: ChromaDB / FAISS
 * Observabilidade: LangSmith
 * Quality & Testing: Pytest, RAGAS (RAG Assessment), Great Expectations.
🧪 Estratégia de QA para IA (Quality Engineering)
Como SDET, o foco principal deste projeto é mitigar a natureza não-determinística das LLMs. A estratégia de testes abrange:
1. Validação de RAG (Retrieval)
 * Hit Rate: Testes automatizados para verificar se o documento correto aparece no top-k resultados.
 * Context Precision: Métricas para garantir que o ruído (informação inútil) seja filtrado pelo Reranker.
2. Validação de Geração (Hallucination Check)
Implementação de "Guardrails" onde um Agente Avaliador verifica a resposta gerada contra o contexto fornecido (Ground Truth).
 * Faithfulness: A resposta deriva puramente do contexto?
 * Answer Relevance: A resposta atende à pergunta do usuário?
3. Testes de Regressão em Prompts
Pipeline de CI/CD que executa um dataset de "Golden Questions" toda vez que um Prompt de Sistema é alterado, garantindo que melhorias em uma área não degradem outra.
🚀 Como Executar (Ambiente de Desenvolvimento)
Este repositório contém a documentação da arquitetura e snippets dos agentes.
# Clone o repositório
git clone [https://github.com/fabioribeiroquispe/OmniSight.git](https://github.com/fabioribeiroquispe/OmniSight.git)

# Instale as dependências
pip install -r requirements.txt

# Configure as chaves de API (.env)
cp .env.example .env
# Edite com sua OPENAI_API_KEY ou GEMINI_API_KEY

📂 Estrutura do Projeto
OmniSight/
├── agents/             # Definição dos Agentes (CrewAI)
│   ├── researcher.py   # Agente de busca e recuperação
│   ├── writer.py       # Agente de síntese e resposta
│   └── qa_guard.py     # Agente de validação de qualidade
├── rag_pipeline/       # Lógica de Ingestão e Retrieval
│   ├── ingestion.py    # Chunking e Vectorização
│   └── retriever.py    # Busca Híbrida (Keyword + Vector)
├── tests/              # Suíte de Testes Automatizados
│   ├── test_retrieval.py
│   └── evaluation_ragas.py
└── README.md

👨‍💻 Autor
Fábio Ribeiro
QA Engineer (SDET) | Especialista em Automação & IA