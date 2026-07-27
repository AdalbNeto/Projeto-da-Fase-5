## 📖 Resumo Executivo

A modelagem de ameaças (*Threat Modeling*) é uma prática essencial para o desenvolvimento de software seguro, permitindo identificar vulnerabilidades ainda na fase de arquitetura. Tradicionalmente, esse processo é realizado de forma manual, exigindo tempo, experiência e conhecimento especializado.

Este MVP demonstra a viabilidade da automatização desse processo utilizando Inteligência Artificial. A solução recebe a imagem de um diagrama arquitetural e executa um pipeline capaz de identificar componentes, extrair informações textuais, reconstruir uma representação lógica da arquitetura e aplicar regras da metodologia STRIDE para gerar ameaças e recomendações de mitigação.

Ao transformar diagramas em análises estruturadas de segurança, o projeto contribui para práticas de **Secure by Design** e estabelece uma base para futuras integrações com processos de **DevSecOps**.

---

## 🎯 Objetivo

Desenvolver um MVP capaz de automatizar a identificação de riscos de segurança em diagramas de arquitetura de software através da integração entre:

- Inteligência Artificial e Visão Computacional
- OCR (Reconhecimento Óptico de Caracteres)
- Teoria dos Grafos
- Threat Modeling baseado na metodologia STRIDE

---

## ❗ O Problema

A análise manual de diagramas arquiteturais apresenta diversos desafios operacionais e de segurança:

- **Elevado esforço operacional:** Análise linha a linha de cada fluxo do diagrama.
- **Dependência de especialistas:** Gargalo no tempo de times dedicados de AppSec.
- **Baixa escalabilidade:** Dificuldade de acompanhar o ritmo de entregas em pipelines ágeis.
- **Subjetividade:** Risco de inconsistências e falhas humanas na identificação de vetores de ataque.
- **Gargalo no Shift-Left:** Dificuldade para incorporar a segurança desde a concepção do projeto.

---

## 💡 A Solução

O projeto implementa um pipeline automatizado modular capaz de interpretar diagramas arquiteturais e transformá-los em uma análise estruturada de segurança.

```text
┌─────────────────────────┐
│ Diagrama de Arquitetura │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ Detecção de Componentes │
│        (YOLOv8)         │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│    Extração de Texto    │
│ (PyTesseract + OpenCV)  │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ Reconstrução Topológica │
│       (NetworkX)        │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│      Motor de Regras    │
│ (Categorização STRIDE)  │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ Relatório de Ameaças    │
│ (Ameaças + Recomendações)│
└─────────────────────────┘
```

---

## 🔄 Pipeline da Solução

### 1. Detecção de Componentes

A primeira etapa utiliza o modelo **YOLOv8** para localizar automaticamente componentes presentes em diagramas arquiteturais. Entre os elementos mapeados estão:

* Usuários / Atores
* Clientes Web
* API Gateway
* Serviços / Aplicações
* Bancos de Dados
* Filas de Mensageria
* Armazenamento (Storage)
* Sistemas Externos

Cada componente detectado possui sua **classe**, **bounding box** (localização espacial) e **grau de confiança**.

### 2. Reconhecimento de Texto (OCR)

Após a detecção dos componentes, é realizado o pré-processamento das regiões de interesse (*ROIs*) utilizando **OpenCV** (conversão para escala de cinza, binarização e redução de ruído), seguido da extração de texto com **PyTesseract**. Essa etapa permite associar rótulos textuais às regiões detectadas, enriquecendo a interpretação semântica dos componentes arquiteturais identificados.

### 3. Reconstrução da Topologia

Os componentes identificados são organizados em uma estrutura de grafo direcionado utilizando **NetworkX**:

* **Vértices (Nós):** Representam os componentes arquiteturais e seus tipos.
* **Arestas (Conexões):** Representam as relações e fluxos de comunicação inferidos entre os componentes.

A reconstrução das conexões é baseada nas informações extraídas do diagrama e em critérios de relacionamento identificados durante o processamento, podendo evoluir futuramente com modelos específicos para detecção de conectores arquiteturais.

### 4. Modelagem de Ameaças (STRIDE)

Com a topologia construída, o sistema aplica regras baseadas na metodologia **STRIDE**, gerando ameaças para componentes e fluxos:

| Categoria | Definição | Foco da Análise |
| --- | --- | --- |
| **S**poofing | Falsificação de Identidade | Autenticação e validação de atores |
| **T**ampering | Alteração Indevida de Dados | Integridade de dados em trânsito e repouso |
| **R**epudiation | Repúdio de Ações | Rastreabilidade, logs e auditoria |
| **I**nformation Disclosure | Vazamento de Informações | Criptografia e proteção contra exposição de dados |
| **D**enial of Service | Negação de Serviço | Disponibilidade, limites de taxa e resiliência |
| **E**levation of Privilege | Elevação de Privilégios | Autorização e controle de acesso (RBAC) |

Para cada ameaça identificada, são geradas recomendações práticas de mitigação.

A inteligência artificial é utilizada nas etapas de interpretação visual dos diagramas, identificação dos componentes arquiteturais, extração de informações textuais e reconstrução da estrutura lógica da arquitetura.

A identificação das categorias STRIDE é realizada por meio de um motor baseado em regras de segurança, seguindo a metodologia estabelecida para associar possíveis ameaças aos componentes e fluxos arquiteturais identificados.

Dessa forma, a solução combina técnicas de Inteligência Artificial para compreensão da arquitetura com regras estruturadas de Threat Modeling para geração das análises de segurança.

---

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Finalidade |
| --- | --- |
| **Python 3** | Linguagem principal do projeto |
| **Jupyter / Colab** | Ambiente de desenvolvimento e execução do experimento |
| **Ultralytics YOLOv8** | Detecção de objetos e componentes visuais |
| **OpenCV** | Processamento digital de imagens e preparação para OCR |
| **PyTesseract** | Reconhecimento Óptico de Caracteres (OCR) |
| **NetworkX** | Modelagem da topologia da arquitetura em grafos |
| **Pandas** | Estruturação e manipulação de dados |
| **Matplotlib** | Visualização dos grafos e resultados |

---

## 📁 Estrutura do Projeto

```text
.
├── docs/                                          # Documentação auxiliar do projeto
│   ├── ESPECIFICACAO_TECNICA.md                   # Especificação técnica e arquitetural
│   └── FLUXO_DESENVOLVIMENTO_SOLUCAO.md           # Fluxo de desenvolvimento da solução
│
├── .gitignore                                     # Proteção contra arquivos temporários
├── LICENSE                                        # Licença MIT
├── [MVP_Threat_Modeling_AI_v12-executada-v1.ipynb](MVP_Threat_Modeling_AI_v12-executada-v1.ipynb)  # Notebook principal do projeto
├── README.md                                      # Documentação principal do repositório
└── requirements.txt                               # Dependências do ambiente Python
```

---

## ⚙️ Como Executar

### Execução via Google Colab ou Jupyter Notebook

1. Clone o repositório oficial do projeto:

```bash
git clone https://github.com/AdalbNeto/Projeto-da-Fase-5.git

cd Projeto-da-Fase-5
```

2. Instale as dependências requeridas no ambiente Python:

```bash
pip install ultralytics opencv-python pytesseract networkx pandas matplotlib
```

3. Abra e execute o notebook principal do projeto:
   
   📌 [MVP_Threat_Modeling_AI_v12-executada-v1.ipynb](./MVP_Threat_Modeling_AI_v12-executada-v1.ipynb)
```

4. Execute as células sequencialmente, forneça uma imagem de arquitetura como entrada e analise os artefatos de saída produzidos.

---

## 📊 Resultados Gerados

Durante e ao final da execução, o pipeline gera automaticamente na pasta `outputs/`:

* **Bounding Boxes e Rótulos:** Imagens anotadas com a classificação dos componentes.
* **Texto Extraído:** Mapeamento de nomes de serviços via OCR.
* **Grafo da Arquitetura:** Visualização estruturada de nós e conexões inferidas.
* **Relatório STRIDE:** Matriz contendo os riscos identificados por componente/fluxo e suas respectivas recomendações de mitigação.

---

## ⭐ Diferenciais da Solução

* **Aplicação Prática de IA em AppSec:** Automação de tarefas complexas de segurança.
* **Pipeline Multimodal:** Combinação de Visão Computacional, OCR e Teoria dos Grafos.
* **Shift-Left Security:** Análise automatizada ainda na fase de design arquitetural.
* **Arquitetura Modular:** Facilidade para expandir regras de segurança e novos modelos.
* **Redução de Esforço Manual:** Agilidade para times de desenvolvimento e segurança.

---

## 🚀 Próximos Passos

* [ ] Desenvolvimento de Interface Web interativa utilizando **Streamlit**.
* [ ] Suporte e integração a múltiplos motores de OCR.
* [ ] Evolução da Base de Conhecimento e regras do motor STRIDE.
* [ ] Módulo para exportação de relatórios executivos em formatos **PDF** e **HTML**.
* [ ] Construção de **API REST** para integração com esteiras de CI/CD (DevSecOps).
* [ ] Suporte à interpretação de diagramas sintáticos (**PlantUML** e **Mermaid**).

---

## 🏆 Conclusão

Este MVP demonstra a viabilidade técnica da automatização da modelagem de ameaças em diagramas arquiteturais utilizando Inteligência Artificial.

A combinação entre Visão Computacional, OCR, Grafos e STRIDE permite transformar diagramas de arquitetura em análises estruturadas de segurança, reduzindo o esforço manual e estabelecendo uma base sólida para futuras evoluções voltadas à automação de processos **DevSecOps** e **Secure by Design**.

---

## 👨‍💻 Autor

**Adalberto Ferreira de Albuquerque Neto**

*Hackathon FIAP — Fase 5 (2026)*
