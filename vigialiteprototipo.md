# Portfolio
Data Science Portfolio – Érica Galvão

🔷 VIGIA-LITE 🚓
Sistema Offline de Reconhecimento de Placas e Faces para Viaturas Inteligentes

Sistema de apoio à atividade policial, baseado em Visão Computacional e Inteligência Artificial, projetado para operar totalmente offline em viaturas, com foco em portabilidade, autonomia operacional e integração futura com sistemas institucionais.

# Vigia-Lite 🚓  
Sistema leve e offline para reconhecimento de placas (ANPR) e rostos para uso em viaturas inteligentes.  
O objetivo é criar um MVP funcional capaz de rodar em dispositivos de baixo custo (Raspberry Pi, Jetson Nano, notebooks modestos) — seguindo a filosofia de inovação frugal.

---

## 📌 Funcionalidades
- Detecção em tempo real de veículos e placas.
- OCR para placas brasileiras (Mercosul e padrão antigo).
- Detecção e reconhecimento facial offline.
- Banco local SQLite com lista de interesse (placas e rostos).
- Dashboard leve para visualizar alertas e ocorrências.
- Execução totalmente offline (com sincronização quando online).

---

## 🧠 Técnicas e Modelos Utilizados
### Detecção
- **YOLOv8n/YOLOv7-tiny** quantizados (INT8).
- Exportação ONNX → ONNX Runtime / TensorRT.

### OCR
- **Tesseract OCR** com pipeline de limpeza + regex BR.
- Alternativa: **CRNN quantizado**.

### Reconhecimento facial
- **MTCNN** (detecção facial).
- **MobileFaceNet** / **FaceNet** para embeddings.
- Busca: **FAISS** local.

### Otimizações
- Quantização INT8.
- Podas estruturais.
- Pipeline de inferência assíncrona.

---

## 🏛 Arquitetura
Camera → Pré-processamento → YOLO Detector →
|--> OCR da placa → Match → Alerta
|--> Face Embedding → FAISS → Alerta
↓
Logger (SQLite)
↓
Dashboard Flask/React
---

## 🛠 Stack Tecnológico
- Python 3.10+
- OpenCV
- ONNX Runtime / TensorRT
- PyTorch (para treino)
- Flask (API)
- React (Dashboard)
- SQLite / SQLAlchemy

---

## 📁 Estrutura do Repositório
vigia-lite/
├─ backend/
│ ├─ app.py
│ ├─ detection/
│ ├─ face/
│ ├─ ocr/
│ └─ models/
├─ frontend/
│ └─ react-app/
├─ data/
├─ notebooks/
├─ scripts/
└─ tests/


---

## ▶️ Como Rodar
### Backend
```bash
python -m venv .venv
source .venv/bin/activate
pip install -r backend/requirements.txt
python backend/app.py


### Frontend

cd frontend
npm install
npm start


📊 Métricas

AP50 (detecção)

CER/WER (OCR)

FAR/FRR (face recognition)

FPS no hardware alvo

Latência média por frame

🧪 Snippet de Inferência
detections = model.infer(frame)
for d in detections:
    if d['class'] == 'plate':
        plate_img = crop(frame, d['bbox'])
        text = ocr(plate_img)
        if check_blacklist(text):
            log_alert("plate", text)
🚀 Roadmap
 Versão para Jetson Nano com TensorRT.

 Modo noturno com filtros adicionais.

 Suporte a OCR baseado em Deep Learning.

 Modo “Patrulha Virtual” com câmeras fixas.


🔐 Segurança & LGPD

Banco local criptografado.

Logs rotacionados e anonimizados.

Nenhum dado enviado para a nuvem.


EXPLICAÇÃO DETALHADA

1. Contexto e Alinhamento Institucional

O Vigia-Lite está alinhado ao Projeto Vigia, conforme previsto no item 1.3, alínea “a”, do Edital Piauí Gov Tech, integrando-se às ações do programa Pacto pela Ordem.

A solução foi concebida para atuar como um módulo complementar em edge computing, permitindo que viaturas policiais realizem reconhecimento de placas e faces sem dependência de conectividade, cenário recorrente em:

Áreas periféricas

Zonas rurais

Operações móveis

Regiões com instabilidade de rede

O projeto não substitui o SPIA, mas amplia sua capacidade operacional ao estender funcionalidades de inteligência para o campo.

2. Objetivo Geral

Desenvolver e validar um MVP funcional de sistema embarcado para viaturas policiais, capaz de executar reconhecimento automático de placas veiculares e faces humanas em tempo real, operando totalmente offline, com possibilidade de sincronização segura posterior com sistemas centrais da SSP-PI.

3. Objetivos Específicos

Implementar Reconhecimento Automático de Placas (ANPR) offline, compatível com padrões brasileiros (Mercosul e anterior).

Realizar reconhecimento facial local, baseado em embeddings biométricos.

Manter listas de interesse armazenadas em banco de dados local criptografado.

Gerar alertas operacionais imediatos para apoio à decisão do policial em campo.

Assegurar conformidade com a LGPD e normas de sigilo da segurança pública.

4. Escopo Funcional

O MVP contempla as seguintes funcionalidades:

Detecção automática de veículos, placas e faces por meio de visão computacional.

OCR otimizado para placas brasileiras, com validação por padrões formais.

Reconhecimento facial offline, sem uso de serviços em nuvem.

Registro local de alertas e ocorrências.

Operação contínua em ambiente offline, com sincronização opcional quando disponível.

5. Limites do Escopo (MVP)

Não contempla, nesta fase, decisões automatizadas sem validação humana.

Não realiza identificação civil ou cadastro biométrico amplo.

Atua como apoio operacional, não como sistema decisório final.
6. Arquitetura do Sistema (Visão Geral)

O Vigia-Lite adota uma arquitetura modular e orientada a edge computing, permitindo execução local, baixa latência e operação independente de conectividade externa.

A solução foi desenhada para facilitar:

Execução em hardware de baixo custo

Evolução incremental

Integração futura com sistemas institucionais

Fluxo Arquitetural
Câmera (USB / RTSP)
        ↓
Pré-processamento de Imagem
(resize, normalização, filtros)
        ↓
Detecção por Visão Computacional
(veículos, placas, faces)
        ↓
┌─────────────────────────────┐
│                             │
│  OCR de Placas              │
│  - Leitura do texto         │
│  - Validação de formato     │
│                             │
│  Reconhecimento Facial      │
│  - Extração de embeddings   │
│  - Comparação local         │
│                             │
└──────────────┬──────────────┘
               ↓
Validação com Listas de Interesse
(Banco local criptografado)
               ↓
Geração de Alerta Operacional
               ↓
Registro Local de Eventos
               ↓
Sincronização Opcional
(com sistemas centrais, quando online)

Princípios Arquiteturais

Offline-first: todo o pipeline funciona sem internet.

Edge computing: inferência executada localmente.

Baixa latência: resposta imediata ao operador.

Modularidade: cada componente pode ser evoluído isoladamente.

Interoperabilidade: preparado para integração via API.

7. Stack Tecnológico

A stack foi selecionada priorizando estabilidade, portabilidade e compatibilidade com ambientes governamentais.

Linguagem e Runtime

Python 3.10+

Visão Computacional e IA

OpenCV — captura e pré-processamento de vídeo

YOLO (versões leves) — detecção de veículos, placas e faces

ONNX Runtime — inferência otimizada em edge devices

FAISS — busca vetorial local (embeddings faciais)

OCR

Tesseract OCR

Pipeline de pós-processamento e validação por padrões brasileiros

Backend / API

Flask (ou FastAPI) — API local e serviços internos

Banco de Dados

SQLite

Possibilidade de uso com criptografia (ex.: SQLCipher)

Infraestrutura e DevOps

Docker (ambiente de desenvolvimento)

GitHub Actions (CI básico)

Execução nativa em Linux

8. Considerações de Implantação

Compatível com:

Notebooks embarcados em viaturas

Raspberry Pi

Jetson Nano (opcional, para maior desempenho)

Não requer conexão com nuvem.

Pode operar com câmera dedicada ou stream RTSP.

Escalável por replicação da solução em múltiplas viaturas.
