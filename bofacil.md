🔷 BO-Fácil Smart NLP 📝
Sistema Inteligente de Apoio à Elaboração e Análise de Boletins de Ocorrência

Autora: Érica Galvão
Área: Ciência de Dados · Processamento de Linguagem Natural · IA Aplicada
Contexto: Segurança Pública · GovTech · Transformação Digital
Status: MVP técnico-conceitual funcional

📌 Visão Geral

O BO-Fácil Smart NLP é um sistema de apoio à atividade policial e administrativa, baseado em Processamento de Linguagem Natural (NLP) e Inteligência Artificial, projetado para automatizar, padronizar e qualificar o registro e a análise de Boletins de Ocorrência (BOs).

A solução atua como um assistente inteligente, reduzindo retrabalho, inconsistências textuais e tempo de preenchimento, além de gerar insumos estruturados para análise estatística e tomada de decisão institucional.

🏛 Contexto e Alinhamento Institucional

O projeto está alinhado às diretrizes de modernização da gestão pública, governo digital e uso estratégico de dados, conforme princípios do Piauí Gov Tech.

O BO-Fácil Smart NLP contribui diretamente para:

Padronização de registros policiais

Melhoria da qualidade dos dados textuais

Redução de erros manuais e ambiguidades

Apoio à inteligência policial e gestão pública

A solução não substitui o agente público, mas atua como ferramenta de apoio, mantendo a decisão e validação final sob responsabilidade humana.

🎯 Objetivo Geral

Desenvolver e validar um MVP funcional de sistema inteligente baseado em NLP, capaz de auxiliar na redação, classificação, análise e estruturação automática de boletins de ocorrência, promovendo eficiência operacional, padronização textual e geração de dados analíticos.

🎯 Objetivos Específicos

Auxiliar o agente na redação orientada de boletins de ocorrência.

Identificar automaticamente tipo de ocorrência, palavras-chave e entidades relevantes.

Padronizar linguagem e estrutura textual dos registros.

Classificar ocorrências para fins estatísticos e gerenciais.

Gerar base de dados estruturada a partir de texto livre.

Assegurar conformidade com a LGPD e diretrizes de segurança da informação.

🧩 Escopo Funcional (MVP)

Análise de texto livre de BOs.

Classificação automática do tipo de ocorrência.

Extração de entidades nomeadas (datas, locais, objetos, pessoas).

Sugestão de padronização textual.

Geração de campos estruturados a partir de texto narrativo.

Dashboard analítico para visualização de dados consolidados.

Limites do Escopo

Não realiza decisões jurídicas ou investigativas.

Não substitui análise humana.

Atua exclusivamente como sistema de apoio à redação e análise.

🏛 Arquitetura do Sistema

Arquitetura modular e orientada a serviços, permitindo evolução incremental e integração futura com sistemas institucionais.

Texto do BO
      ↓
Pré-processamento NLP
(tokenização, limpeza, normalização)
      ↓
Modelos de NLP
(classificação, NER, embeddings)
      ↓
┌─────────────────────────────┐
│ Classificação da Ocorrência │
│ Extração de Entidades       │
│ Padronização Textual        │
└──────────────┬──────────────┘
               ↓
Banco de Dados Estruturado
               ↓
Dashboard Analítico
               ↓
Integração Opcional (API)

Princípios Arquiteturais

Human-in-the-loop

Modularidade

Explicabilidade

Interoperabilidade

Privacidade por design

🧠 Técnicas e Modelos Utilizados
Processamento de Linguagem Natural

Tokenização e normalização textual

TF-IDF e embeddings semânticos

Classificação supervisionada de textos

Modelos

Logistic Regression / SVM (baseline)

BERTimbau / DistilBERT (opcional)

SpaCy para NER (português)

Análise

Extração de palavras-chave

Agrupamento semântico

Estatísticas textuais

🛠 Stack Tecnológico

Python 3.10+

Pandas / NumPy

Scikit-learn

SpaCy

Transformers (HuggingFace)

Flask ou FastAPI

SQLite / PostgreSQL

Dash / Streamlit / React (dashboard)

Docker (desenvolvimento)

📁 Estrutura do Repositório
bo-facil-smart-nlp/
├─ backend/
│  ├─ app.py
│  ├─ nlp/
│  ├─ models/
│  └─ services/
├─ frontend/
│  └─ dashboard/
├─ data/
│  ├─ raw/
│  └─ processed/
├─ notebooks/
├─ scripts/
└─ tests/

▶️ Como Executar
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python backend/app.py

📊 Métricas de Avaliação

Accuracy / F1-score (classificação)

Precisão e recall (NER)

Redução de tempo médio de preenchimento

Taxa de padronização textual

Qualidade dos dados estruturados gerados

🔐 Segurança da Informação & LGPD

Processamento local ou em ambiente controlado.

Possibilidade de anonimização de dados sensíveis.

Controle de acesso por perfil.

Logs auditáveis.

Princípio da minimização de dados.

🚀 Roadmap

Treinamento com dados reais anonimizados.

Ajuste fino com modelos em português jurídico-policial.

Integração com sistemas de registro oficiais.

Dashboards gerenciais avançados.

Piloto institucional em ambiente real.

⚖️ Observação Final

Este projeto representa uma prova de conceito técnico e institucional, demonstrando como NLP pode ser aplicado de forma responsável e eficaz na segurança pública, respeitando limites legais, éticos e operacionais.
