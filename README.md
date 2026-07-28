## 📖 Resumo Executivo

A modelagem de ameaças (Threat Modeling) é uma prática essencial para o desenvolvimento de software seguro, permitindo identificar vulnerabilidades ainda na fase de arquitetura. Tradicionalmente, esse processo é realizado de forma manual, exigindo tempo, experiência e conhecimento especializado.

Este projeto demonstra a viabilidade da automatização desse processo utilizando Inteligência Artificial. A solução recebe a imagem de um diagrama arquitetural e executa um pipeline capaz de identificar componentes, extrair informações textuais, reconstruir uma representação lógica da arquitetura e aplicar regras da metodologia STRIDE para gerar ameaças e recomendações de mitigação.

Ao transformar diagramas em análises estruturadas de segurança, o projeto contribui para práticas de *Secure by Design* e estabelece uma base para futuras integrações com processos de *DevSecOps*.

---

## 🎯 Objetivo

Desenvolver um projeto capaz de automatizar a identificação de riscos de segurança em diagramas de arquitetura de software através da integração entre:

- Inteligência Artificial e Visão Computacional
- OCR (Reconhecimento Óptico de Caracteres)
- Teoria dos Grafos
- Threat Modeling baseado na metodologia STRIDE

---

## ❗ O Problema

A análise manual de diagramas arquiteturais apresenta diversos desafios operacionais e de segurança:

- **Elevado esforço operacional:** análise linha a linha de cada fluxo do diagrama.
- **Dependência de especialistas:** gargalo no tempo de times dedicados de AppSec.
- **Baixa escalabilidade:** dificuldade de acompanhar o ritmo de entregas em pipelines ágeis.
- **Subjetividade:** risco de inconsistências e falhas humanas na identificação de vetores de ataque.
- **Gargalo no Shift-Left:** dificuldade para incorporar a segurança desde a concepção do projeto.

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
┌──────────────────────────┐
│ Relatório de Ameaças     │
│ (Ameaças + Mitigações)   │
└──────────────────────────┘
```

---

## 🔄 Pipeline da Solução

### 1. Detecção de Componentes

A primeira etapa utiliza o modelo **YOLOv8** para localizar automaticamente componentes presentes em diagramas arquiteturais. Entre os elementos mapeados estão:

- Usuários / Atores
- Clientes Web
- API Gateway
- Serviços / Aplicações
- Bancos de Dados
- Filas de Mensageria
- Armazenamento (Storage)
- Sistemas Externos

Cada componente detectado possui sua **classe**, **bounding box** (localização espacial) e **grau de confiança**.

### 2. Reconhecimento de Texto (OCR)

Após a detecção dos componentes, é realizado o pré-processamento das regiões de interesse (ROIs) utilizando **OpenCV** (conversão para escala de cinza, binarização e redução de ruído), seguido da extração de texto com **PyTesseract**. Essa etapa permite associar rótulos textuais às regiões detectadas, enriquecendo a interpretação semântica dos componentes arquiteturais identificados.

### 3. Reconstrução da Topologia

Os componentes identificados são organizados em uma estrutura de grafo direcionado utilizando **NetworkX**:

- **Vértices (Nós):** representam os componentes arquiteturais e seus tipos.
- **Arestas (Conexões):** representam os fluxos de comunicação inferidos entre os componentes.

A reconstrução das conexões é baseada nas informações extraídas do diagrama e em critérios de relacionamento identificados durante o processamento, podendo evoluir futuramente com modelos específicos para detecção de conectores arquiteturais.

### 4. Modelagem de Ameaças (STRIDE)

Com a topologia construída, o sistema aplica regras baseadas na metodologia **STRIDE**, gerando ameaças para componentes e fluxos.

| Categoria | Definição | Foco da Análise |
|-----------|-----------|-----------------|
| **Spoofing** | Falsificação de Identidade | Autenticação e validação de atores |
| **Tampering** | Alteração Indevida de Dados | Integridade dos dados |
| **Repudiation** | Repúdio de Ações | Logs, auditoria e rastreabilidade |
| **Information Disclosure** | Vazamento de Informações | Confidencialidade e criptografia |
| **Denial of Service** | Negação de Serviço | Disponibilidade e resiliência |
| **Elevation of Privilege** | Elevação de Privilégios | Autorização e controle de acesso |

Para cada ameaça identificada são geradas recomendações práticas de mitigação.

A Inteligência Artificial é utilizada nas etapas de interpretação visual dos diagramas, identificação dos componentes arquiteturais, extração de informações textuais e reconstrução da estrutura lógica da arquitetura.

A identificação das categorias STRIDE é realizada por meio de um motor baseado em regras de segurança, seguindo a metodologia estabelecida para associar possíveis ameaças aos componentes e fluxos arquiteturais identificados.

Dessa forma, a solução combina técnicas de Inteligência Artificial para compreensão da arquitetura com regras estruturadas de Threat Modeling para geração das análises de segurança.

---

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Finalidade |
|------------|------------|
| **Python 3** | Linguagem principal |
| **Jupyter Notebook / Google Colab** | Ambiente de desenvolvimento |
| **Ultralytics YOLOv8** | Detecção de componentes |
| **OpenCV** | Processamento de imagens |
| **PyTesseract** | OCR |
| **NetworkX** | Modelagem em grafos |
| **Pandas** | Manipulação de dados |
| **Matplotlib** | Visualização gráfica |

---

## 📁 Estrutura do Projeto

```text
.
├── docs/
│   ├── ESPECIFICACAO_TECNICA.md          # Especificação técnica e arquitetural
│   └── FLUXO_DESENVOLVIMENTO_SOLUCAO.md  # Fluxo de desenvolvimento da solução
├── .gitignore                            # Arquivos ignorados pelo Git
├── Hackathon_7IADT.ipynb                 # Notebook principal do projeto
├── LICENSE                               # Licença MIT
├── README.md                             # Documentação principal
└── requirements.txt                      # Dependências do projeto

```

## 📥 Repositorio de Trabalho do Projeto

Devido ao tamanho elevado do repositório de trabalho do projeto para carregar no github,
verifique no link do Google Drive:

🔗 **https://drive.google.com/drive/folders/1Wckn7iKo8ZL2Us0gRMRC5QT4WEj1UxTs?usp=drive_link** 

---

## ⚙️ Como Executar

### Execução via Google Colab ou Jupyter Notebook

1. Clone o repositório:

```bash
git clone https://github.com/AdalbNeto/Projeto-da-Fase-5.git
cd Projeto-da-Fase-5
```

2. Instale as dependências:

```bash
pip install ultralytics opencv-python pytesseract networkx pandas matplotlib
```

3. Abra o notebook principal:

📌 `Hackathon_7IADT.ipynb`

4. Execute as células sequencialmente.
---

## 📊 Resultados Gerados

Durante a execução, o pipeline gera automaticamente:

- **Bounding Boxes e Rótulos:** componentes detectados na imagem.
- **Texto Extraído:** identificação via OCR.
- **Grafo da Arquitetura:** representação lógica dos componentes e conexões.
- **Relatório STRIDE:** ameaças identificadas e respectivas recomendações de mitigação.

---

## ⭐ Diferenciais da Solução

- Aplicação prática de IA em AppSec.
- Pipeline multimodal (Visão Computacional + OCR + Grafos).
- Automação de práticas de Shift-Left Security.
- Arquitetura modular e extensível.
- Redução do esforço manual na modelagem de ameaças.

---

## 🚀 Próximos Passos

- [ ] Desenvolvimento de interface Web com Streamlit.
- [ ] Integração com múltiplos motores de OCR.
- [ ] Evolução da base de conhecimento STRIDE.
- [ ] Exportação de relatórios em PDF e HTML.
- [ ] API REST para integração com pipelines DevSecOps.
- [ ] Suporte a PlantUML e Mermaid.

---

## 🏆 Conclusão

Este projeto demonstra a viabilidade técnica da automatização da modelagem de ameaças em diagramas arquiteturais utilizando Inteligência Artificial.

A combinação entre Visão Computacional, OCR, Grafos e STRIDE permite transformar diagramas de arquitetura em análises estruturadas de segurança, reduzindo o esforço manual e estabelecendo uma base sólida para futuras evoluções voltadas à automação de processos DevSecOps e à adoção dos princípios de *Secure by Design*.

---

## 👨‍💻 Autor

**Adalberto Ferreira de Albuquerque Neto**

Hackathon FIAP — Fase 5 (2026)
