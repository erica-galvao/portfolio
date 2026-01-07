🔷 Vigia-Lite 🚓
Sistema Offline de Reconhecimento de Placas e Faces para Viaturas Inteligentes

Autora: Érica Galvão
Área: Visão Computacional · Inteligência Artificial · Edge Computing
Contexto: Segurança Pública · Piauí Gov Tech
Status: MVP técnico-conceitual funcional

📌 Visão Geral

O Vigia-Lite é um sistema de apoio à atividade policial, baseado em Visão Computacional e Inteligência Artificial, projetado para operar totalmente offline em viaturas policiais.

A solução foi concebida segundo a filosofia de inovação frugal, permitindo execução em dispositivos de baixo custo (Raspberry Pi, Jetson Nano ou notebooks embarcados), com foco em:

Autonomia operacional

Baixa latência

Portabilidade

Integração futura com sistemas institucionais

🏛 Contexto e Alinhamento Institucional

O projeto está alinhado ao Projeto Vigia, conforme previsto no item 1.3, alínea “a”, do Edital Piauí Gov Tech, integrando-se às ações do programa Pacto pela Ordem.

O Vigia-Lite atua como um módulo edge complementar, estendendo capacidades de inteligência diretamente para o campo, especialmente em cenários recorrentes no Estado do Piauí:

Áreas periféricas

Zonas rurais

Operações móveis

Regiões com conectividade limitada ou inexistente

O sistema não substitui o SPIA, mas amplia sua atuação ao permitir coleta e análise local, com sincronização posterior quando houver conectividade.

🎯 Objetivo Geral

Desenvolver e validar um MVP funcional de sistema embarcado para viaturas policiais, capaz de realizar reconhecimento automático de placas veiculares e faces humanas em tempo real, operando totalmente offline, com possibilidade de sincronização segura posterior com sistemas centrais da SSP-PI.

🎯 Objetivos Específicos

Implementar Reconhecimento Automático de Placas (ANPR) offline, compatível com padrões brasileiros (Mercosul e anterior).

Realizar reconhecimento facial local, baseado em embeddings biométricos.

Manter listas de interesse armazenadas em banco de dados local criptografado.

Gerar alertas operacionais imediatos, apoiando a tomada de decisão do policial em campo.

Garantir conformidade com a LGPD e normas de sigilo da segurança pública.

🧩 Escopo Funcional (MVP)

Detecção automática de veículos, placas e faces por visão computacional.

OCR otimizado para placas brasileiras, com validação por padrões formais.

Reconhecimento facial offline, sem uso de serviços em nuvem.

Registro local de alertas e ocorrências.

Operação contínua em ambiente offline.

Sincronização opcional quando houver conectividade.

Limites do Escopo

Não realiza decisões automatizadas sem validação humana.

Não contempla identificação civil ampla ou cadastro biométrico massivo.

Atua como sistema de apoio operacional, não decisório final.

🏛 Arquitetura do Sistema

Arquitetura modular e orientada a edge computing, priorizando baixa latência e independência de conectividade.

Câmera (USB / RTSP)
        ↓
Pré-processamento de Imagem
        ↓
Detecção (Veículos / Placas / Faces)
        ↓
┌─────────────────────────────┐
│ OCR de Placas               │
│ Reconhecimento Facial       │
└──────────────┬──────────────┘
               ↓
Validação com Listas de Interesse
(Banco local criptografado)
               ↓
Geração de Alertas
               ↓
Registro Local
               ↓
Sincronização Opcional

Princípios Arquiteturais

Offline-first

Edge computing

Baixa latência

Modularidade

Preparado para integração via API

🧠 Técnicas e Modelos Utilizados
Detecção

YOLOv8n / YOLOv7-tiny (quantizados – INT8)

Exportação ONNX para inferência otimizada

OCR

Tesseract OCR

Pipeline de limpeza + regex para padrão brasileiro

Alternativa prevista: CRNN quantizado

Reconhecimento Facial

MTCNN (detecção)

MobileFaceNet / FaceNet (embeddings)

FAISS para busca vetorial local

Otimizações

Quantização INT8

Podas estruturais

Pipeline de inferência assíncrona

🛠 Stack Tecnológico

Python 3.10+

OpenCV

ONNX Runtime / TensorRT

PyTorch (treinamento)

Flask (API)

React (Dashboard)

SQLite / SQLAlchemy

Docker (desenvolvimento)

GitHub Actions (CI básico)

📁 Estrutura do Repositório
vigia-lite/
├─ backend/
│  ├─ app.py
│  ├─ detection/
│  ├─ face/
│  ├─ ocr/
│  └─ models/
├─ frontend/
│  └─ react-app/
├─ data/
├─ notebooks/
├─ scripts/
└─ tests/

▶️ Como Executar
Backend
python -m venv .venv
source .venv/bin/activate
pip install -r backend/requirements.txt
python backend/app.py

Frontend
cd frontend
npm install
npm start

📊 Métricas de Avaliação

AP50 (detecção)

CER / WER (OCR)

FAR / FRR (reconhecimento facial)

FPS no hardware alvo

Latência média por frame

🔐 Segurança da Informação & LGPD

Processamento prioritariamente local.

Banco de dados criptografado.

Possibilidade de armazenamento apenas de embeddings.

Logs rotacionados e anonimizados.

Nenhum dado enviado para a nuvem.

🚀 Roadmap

Versão otimizada para Jetson Nano com TensorRT.

Melhorias para cenários noturnos.

OCR baseado em Deep Learning.

Integração com câmeras fixas (“Patrulha Virtual”).

Pilotos operacionais em ambiente real.

⚖️ Observação Final

Este repositório representa um MVP técnico-institucional, desenvolvido para demonstrar viabilidade, maturidade técnica e aderência ao edital, servindo como base para validação, evolução e eventual implantação institucional.
