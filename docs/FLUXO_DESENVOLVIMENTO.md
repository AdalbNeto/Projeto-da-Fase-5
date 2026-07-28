# Fluxo de Desenvolvimento da Solução – IA para Modelagem Automática de Ameaças

## Hackathon FIAP – Fase 4

### Visão Geral
Este documento descreve uma arquitetura completa para uma solução de IA capaz de interpretar diagramas de arquitetura de software, identificar componentes, reconstruir a topologia, aplicar a metodologia STRIDE e enriquecer a análise consultando bases de vulnerabilidades e contramedidas.

# Objetivos
- Interpretar diagramas automaticamente.
- Criar e anotar datasets.
- Treinar modelos supervisionados.
- Gerar ameaças STRIDE.
- Consultar CVE, CWE, CAPEC, OWASP ASVS e MITRE ATT&CK.
- Produzir relatório executivo de Threat Modeling.

# Arquitetura Geral

```text
Dataset -> Anotação -> YOLOv8/YOLO11 -> OCR -> Grafo -> STRIDE
                         |
                         v
                 Base Vetorial (RAG)
                         |
                         v
          CVE/CWE/CAPEC/OWASP/MITRE
                         |
                         v
             Contramedidas e Relatório
```

# Pipeline

## Fase 1 – Engenharia de Dados
Coleta de diagramas (AWS, Azure, GCP, Kubernetes, UML, C4, Mermaid, PlantUML), curadoria, limpeza, balanceamento e versionamento.

## Fase 2 – Anotação
Classes: Usuário, API Gateway, Load Balancer, Serviço, Banco de Dados, Cache, Fila, Storage, IAM, Firewall, WAF, Sistema Externo, Trust Boundary.

## Fase 3 – Treinamento
YOLOv8/YOLO11 para detecção de objetos, métricas Precision, Recall, mAP e F1.

## Fase 4 – Interpretação
OCR (Tesseract), OpenCV e reconstrução do grafo com NetworkX.

## Fase 5 – Threat Modeling
Aplicação da metodologia STRIDE por componente e fluxo.

## Fase 6 – Inteligência de Vulnerabilidades
Consulta a CVE, CWE, CAPEC, OWASP Top 10, OWASP ASVS e MITRE ATT&CK utilizando RAG (FAISS/ChromaDB + LLM).

## Fase 7 – Relatório
Para cada componente:
- ameaças STRIDE
- vulnerabilidades relacionadas
- impacto
- probabilidade
- nível de risco
- contramedidas
- referências

# Arquitetura de IA
- Visão Computacional: YOLOv8/YOLO11
- OCR: Tesseract
- Processamento: OpenCV
- Grafo: NetworkX
- LLM: Llama 3.x ou GPT
- Orquestração: LangChain/LangGraph
- Banco Vetorial: FAISS ou ChromaDB

# Métricas
- mAP
- Precision
- Recall
- F1-score
- Tempo de inferência
- Taxa de detecção de componentes

# DevSecOps
Integração futura com GitHub Actions, Azure DevOps e Jenkins para execução automática do Threat Modeling.

# Roadmap
1. Dataset próprio.
2. Fine-tuning multimodal.
3. GroundingDINO e SAM2.
4. Florence-2.
5. Interface Streamlit.
6. Exportação para PDF/HTML e Microsoft Threat Modeling Tool.

# Conclusão
A solução cobre todo o ciclo do desafio: criação do dataset, treinamento dos modelos, interpretação de diagramas, geração automática de ameaças STRIDE, enriquecimento com vulnerabilidades e recomendações de mitigação, apoiando práticas de Secure by Design e Shift-Left Security.
