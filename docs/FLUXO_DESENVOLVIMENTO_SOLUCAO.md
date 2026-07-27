# 🔐 Documentação do Fluxo de Desenvolvimento da Solução

## MVP — Apoio Automatizado à Modelagem de Ameaças Arquiteturais com IA

**Contexto:** Hackathon FIAP — Fase 5 (2026)  
**Projeto:** Pipeline automatizado de apoio à modelagem de ameaças utilizando Visão Computacional, OCR, Teoria dos Grafos e STRIDE.  
**Autor:** Adalberto Ferreira de Albuquerque Neto  

---

# 1. Visão Geral do Fluxo

A solução foi desenvolvida através de um pipeline modular destinado a auxiliar etapas iniciais do processo de Threat Modeling em arquiteturas de software.

O objetivo do MVP é transformar diagramas arquiteturais em uma representação estruturada, permitindo identificar componentes, extrair informações textuais, reconstruir uma visão lógica da arquitetura e aplicar regras baseadas na metodologia STRIDE para geração de possíveis ameaças e recomendações de mitigação.

O fluxo completo de desenvolvimento segue as seguintes etapas:

```text
Dataset de Diagramas
        ↓
Preparação e Anotação dos Dados
        ↓
Treinamento e Validação YOLOv8
        ↓
Detecção dos Componentes Arquiteturais
        ↓
Extração de Texto via OCR
        ↓
Reconstrução da Topologia Arquitetural
        ↓
Aplicação das Regras STRIDE
        ↓
Geração do Relatório de Ameaças
```

A solução utiliza Inteligência Artificial principalmente nas etapas de visão computacional e extração de informações, enquanto a análise STRIDE é realizada através de um motor baseado em regras estruturadas de segurança.

---

# 2. Fase 1 — Preparação do Ambiente e Aquisição de Dados

Esta fase teve como objetivo preparar o ambiente de desenvolvimento e organizar os dados utilizados no treinamento e validação do modelo.

## Instalação de Dependências

O ambiente foi configurado utilizando bibliotecas necessárias para cada etapa do pipeline:

- `ultralytics` para treinamento e inferência do modelo YOLOv8;
- `opencv-python` para processamento digital de imagens;
- `pytesseract` para reconhecimento óptico de caracteres (OCR);
- `networkx` para modelagem da arquitetura em grafos;
- bibliotecas auxiliares para manipulação e visualização dos resultados.

---

## Configuração da Estrutura do Projeto

Foi definida a organização dos diretórios e a taxonomia dos componentes arquiteturais utilizados na solução.

As classes consideradas incluem:

- Usuários / Atores;
- Clientes Web;
- API Gateway;
- Serviços / Aplicações;
- Banco de Dados;
- Filas de Mensageria;
- Armazenamento;
- Sistemas Externos.

Essa padronização permite que o modelo de visão computacional reconheça elementos recorrentes em diagramas arquiteturais.

---

## Coleta e Preparação do Dataset

Foi realizada a aquisição e preparação dos diagramas arquiteturais utilizados no desenvolvimento do modelo.

Os dados foram organizados para permitir:

- Anotação dos componentes;
- Treinamento supervisionado;
- Validação do desempenho do modelo.

---

## Inspeção Visual dos Dados

Foi realizada uma avaliação inicial das imagens para verificar:

- Qualidade dos diagramas;
- Clareza visual dos componentes;
- Compatibilidade dos dados com a etapa de detecção.

---

# 3. Fase 2 — Preparação e Treinamento do Modelo de Visão Computacional

Nesta fase o objetivo foi adaptar um modelo YOLOv8 para identificação de componentes presentes em diagramas arquiteturais.

---

## Anotação dos Dados

Os diagramas foram preparados com anotações no formato YOLO contendo:

- Classe do componente;
- Coordenadas da região identificada;
- Bounding Box correspondente.

Essas informações permitem o treinamento supervisionado do modelo.

---

## Organização dos Dados

O dataset foi dividido em conjuntos de:

- Treinamento;
- Validação;
- Teste.

Essa separação permite avaliar o desempenho do modelo em dados não utilizados durante o treinamento.

---

## Configuração do Modelo YOLOv8

Foi criado o arquivo de configuração contendo:

- Classes utilizadas;
- Localização dos dados;
- Parâmetros necessários para execução do treinamento.

---

## Ajuste e Validação do Modelo

O modelo YOLOv8 foi ajustado utilizando diagramas arquiteturais anotados, permitindo identificar componentes específicos de arquitetura de software.

A avaliação do modelo considera métricas utilizadas em detecção de objetos, como:

- Precisão;
- Recall;
- mAP (*mean Average Precision*).

---

# 4. Fase 3 — Interpretação dos Diagramas e Construção do Modelo de Ameaças

Nesta fase ocorre a transformação do diagrama visual em uma representação estruturada para análise de segurança.

---

## Detecção dos Componentes Arquiteturais

O modelo YOLOv8 recebe um diagrama arquitetural como entrada e identifica:

- Componentes presentes na imagem;
- Classe prevista;
- Localização espacial (*Bounding Box*);
- Grau de confiança da detecção.

O resultado desta etapa fornece a identificação visual dos elementos arquiteturais.

---

## Extração de Texto utilizando OCR

Após a detecção dos componentes, as regiões de interesse (*ROIs*) são processadas utilizando técnicas de tratamento de imagem através do OpenCV.

Posteriormente, o PyTesseract realiza a extração dos textos presentes nessas regiões.

Essa etapa permite associar rótulos textuais aos componentes identificados, enriquecendo a representação da arquitetura.

O OCR atua como mecanismo de extração de informações textuais, enquanto a interpretação arquitetural ocorre através da combinação dos dados obtidos pelo pipeline.

---

## Reconstrução da Topologia Arquitetural

Os componentes identificados visualmente e suas informações associadas são organizados em uma estrutura de grafo direcionado utilizando NetworkX.

A representação considera:

- **Vértices (Nós):** representam os componentes arquiteturais identificados;
- **Arestas (Conexões):** representam relações e possíveis fluxos de comunicação inferidos a partir das informações disponíveis no diagrama.

A reconstrução da topologia representa uma abstração lógica da arquitetura analisada.

A inferência das conexões pode ser aprimorada futuramente através de modelos especializados para identificação de conectores e relacionamentos arquiteturais.

---

## Aplicação da Metodologia STRIDE

Após a construção da representação arquitetural, um motor baseado em regras aplica a metodologia STRIDE para classificar possíveis categorias de ameaças.

As categorias analisadas são:

- **Spoofing:** falsificação de identidade;
- **Tampering:** alteração indevida de dados;
- **Repudiation:** ausência de rastreabilidade;
- **Information Disclosure:** exposição de informações;
- **Denial of Service:** indisponibilidade de serviços;
- **Elevation of Privilege:** elevação indevida de privilégios.

A Inteligência Artificial auxilia na identificação dos componentes e reconstrução da arquitetura.

A identificação das ameaças é realizada por regras estruturadas baseadas na metodologia STRIDE aplicadas sobre os componentes e fluxos identificados.

---

# 5. Fase 4 — Geração dos Resultados e Entregáveis

A etapa final transforma os dados processados em informações estruturadas para análise.

---

## Geração do Relatório de Ameaças

O resultado do motor STRIDE é organizado em um relatório contendo:

- Componentes analisados;
- Categoria da ameaça;
- Descrição do risco identificado;
- Recomendações de mitigação.

---

## Visualização dos Resultados

Durante a execução do pipeline são apresentados:

- Diagramas processados com componentes identificados;
- Informações extraídas via OCR;
- Representação da arquitetura em grafo;
- Relatório estruturado de ameaças.

---

## Interface Interativa

O desenvolvimento de uma interface utilizando Streamlit é considerado uma evolução futura da solução.

A proposta é disponibilizar uma camada visual que facilite a utilização do pipeline por usuários não técnicos, permitindo submissão de diagramas e visualização dos resultados gerados.

---

# 6. Limitações Conhecidas

Como MVP, a solução apresenta algumas limitações:

## Qualidade dos Diagramas

Diagramas com baixa resolução, fontes não padronizadas ou elementos visuais inconsistentes podem impactar a precisão da detecção e extração textual.

---

## Reconstrução das Conexões

As relações entre componentes são inferidas a partir das informações disponíveis no diagrama e dos critérios utilizados pelo pipeline.

Essa etapa pode evoluir futuramente com modelos específicos para reconhecimento de linhas, conectores e relacionamentos arquiteturais.

---

## Motor STRIDE Baseado em Regras

A análise de ameaças utiliza regras estruturadas baseadas na metodologia STRIDE.

Como evolução futura, o motor poderá incorporar abordagens híbridas utilizando modelos de linguagem e bases de conhecimento especializadas.

---

## Papel de Apoio ao Especialista

A solução tem como objetivo apoiar profissionais de segurança e desenvolvimento, reduzindo esforço manual nas etapas iniciais da análise.

O resultado gerado deve ser utilizado como apoio à decisão, mantendo a validação humana no processo de Threat Modeling.

---

# 7. Trabalhos Futuros

As evoluções planejadas incluem:

- Desenvolvimento de interface web utilizando Streamlit;
- Integração com pipelines DevSecOps;
- Exportação de relatórios executivos em PDF e HTML;
- Expansão da base de conhecimento STRIDE;
- Suporte a diagramas estruturados como PlantUML e Mermaid;
- Evolução dos modelos de interpretação arquitetural.

---

# 8. Conclusão

O desenvolvimento deste MVP demonstra a viabilidade de utilizar Inteligência Artificial, Visão Computacional, OCR e Teoria dos Grafos como suporte à automatização de etapas iniciais da modelagem de ameaças.

A solução permite transformar diagramas arquiteturais em uma representação estruturada capaz de auxiliar na identificação de possíveis riscos de segurança.

O projeto estabelece uma base para futuras evoluções envolvendo automação de processos de segurança, integração DevSecOps e práticas de Secure by Design e Shift-Left Security.
