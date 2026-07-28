# 📑 Especificação Técnica e Arquitetural do Projeto

**Curso:** Pós-Graduação FIAP  
**Evento:** Hackathon — Fase 5 (2026)  
**Projeto:** IA para Modelagem Automática de Ameaças em Arquiteturas de Software utilizando STRIDE  
**Autor:** Adalberto Ferreira de Albuquerque Neto  

---

## 1. Introdução e Contextualização

A modelagem de ameaças (*Threat Modeling*) é uma disciplina fundamental de Segurança da Informação (*Application Security*) focada na identificação proativa de falhas de design e vulnerabilidades arquiteturais. Tradicionalmente, este processo ocorre através de revisões manuais conduzidas por especialistas, o que gera gargalos operacionais em pipelines de entrega contínua (CI/CD).

Este documento especifica a arquitetura técnica da solução proposta para o Hackathon da FIAP Software Security. O projeto visa desenvolver uma IA para interpretar diagramas de arquitetura, identificar componentes, gerar modelagem de ameaças STRIDE, criar/anotar datasets, treinar modelos supervisionados e consultar vulnerabilidades e contramedidas.

---

## 2. Fundamentação Teórica e Tecnológica

### 2.1 Visão Computacional e Detecção de Objetos

A etapa de localização visual utiliza o framework **YOLOv8** (*You Only Look Once*), selecionado por sua alta eficiência computacional e precisão no mapeamento de Bounding Boxes em tempo real. O modelo foi ajustado utilizando diagramas arquiteturais anotados para identificar entidades da arquitetura, como Atores, Gateways, Bancos de Dados, Filas e Serviços.

### 2.2 Reconhecimento Óptico de Caracteres (OCR)

Para associar contexto semântico às regiões delimitadas pelo YOLOv8, utiliza-se a biblioteca **PyTesseract** combinada com técnicas de processamento digital de imagem via **OpenCV** (conversão para escala de cinza, binarização por Otsu e atenuação de ruídos).

### 2.3 Teoria dos Grafos para Topologia Arquitetural

A representação lógica da arquitetura é modelada como um Grafo Direcionado $G = (V, E)$ através do ecossistema **NetworkX**:

- **Vértices ($V$):** Nós representando os componentes detectados ($v_i \in V$).
- **Arestas ($E$):** Conexões direcionadas representando fluxos de comunicação ou dependências entre componentes ($(v_i, v_j) \in E$).

### 2.4 Metodologia STRIDE

A avaliação de riscos utiliza o modelo **STRIDE** (Microsoft), categorizando ameaças em:

- **S**poofing (Autenticação)
- **T**ampering (Integridade)
- **R**epudiation (Rastreabilidade)
- **I**nformation Disclosure (Confidencialidade)
- **D**enial of Service (Disponibilidade)
- **E**levation of Privilege (Autorização)

---

## 3. Arquitetura do Pipeline de Processamento

```text
[ Diagrama em Imagem ]
       │
       ├──> (1) Detecção YOLOv8 ──────> [ Bounding Boxes & Classes ]
       │                                         │
       ├──> (2) Crop ROI + OpenCV + OCR ────────> [ Rótulos Textuais ]
                                                 │
                                                 ▼
                                     (3) Grafo NetworkX G=(V,E)
                                                 │
                                                 ▼
                                     (4) Engine de Regras STRIDE
                                                 │
                                                 ▼
                                     [ Relatório Estruturado ]
```

---

## 4. Considerações de Segurança e DevSecOps (Shift-Left)

A automação proposta visa viabilizar a abordagem **Shift-Left Security**, permitindo que riscos arquiteturais sejam identificados e mitigados antes do início da fase de codificação.

As recomendações geradas pelo motor de regras priorizam contramedidas padrões da indústria, tais como:

- Criptografia forte em trânsito (TLS 1.3) e em repouso (AES-256).
- Autenticação e autorização centralizadas via OAuth 2.0 / OIDC / mTLS.
- Aplicação do Princípio do Menor Privilégio e RBAC.
- Implementação de Rate Limiting e WAF em pontos de entrada.

---

## 5. Limitações Conhecidas e Trabalhos Futuros

Como proposta de Hackathon, a solução apresenta as seguintes delimitações:

1. **Dependência da Qualidade da Imagem:** Diagramas com baixa resolução ou fontes não padrão podem impactar a precisão do OCR.

2. **Evolução do Grafo:** A inferência de arestas baseia-se em critérios espaciais de proximidade, podendo ser aprimorada com modelos focados em detecção de linhas/conectores.
