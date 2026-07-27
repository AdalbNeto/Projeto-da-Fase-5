# 🛡️ Entrega Hackathon — Modelagem de Ameaças com IA

Este projeto apresenta uma solução de **análise automatizada de diagramas de arquitetura de software** com foco em identificação de componentes, inferência de fluxos e geração de ameaças com base na metodologia **STRIDE**. A aplicação recebe uma imagem de arquitetura, processa seus elementos visuais e textuais e produz um relatório estruturado com ameaças e contramedidas de segurança. [1][2]

## 🚀 Visão Geral da Solução

A solução foi construída como um pipeline de visão computacional e análise de segurança aplicado a diagramas arquiteturais. No fluxo executado, o sistema detecta componentes visuais, associa rótulos textuais extraídos por OCR, organiza a estrutura em forma de topologia e aplica regras STRIDE por componente e por fluxo de dados. [1][2]

No resultado observado da base conceitual da v12, o pipeline foi capaz de detectar múltiplos componentes, inferir relações entre eles e produzir ameaças em categorias como Information Disclosure, Repudiation, Spoofing e Tampering. Na execução ampliada da mesma linha funcional, o processo chegou a 8 componentes detectados, 8 relações inferidas e 32 ameaças identificadas, evidenciando a capacidade do código em transformar imagem em análise estruturada de segurança. [1][2]

## 🔍 Etapas do Modelo

### Detecção de Componentes
A etapa de detecção de componentes utiliza um modelo **YOLOv8** treinado para localizar elementos arquiteturais presentes nos diagramas, como cliente web, ator de usuário e gateway de API. O objetivo dessa fase é transformar o conteúdo visual da imagem em caixas delimitadoras com classe e confiança, criando a base estrutural para as próximas etapas do pipeline. [1][2]

Na prática, essa detecção fornece os elementos mínimos para que o diagrama deixe de ser apenas uma imagem e passe a ser interpretado como um conjunto de entidades técnicas. Os resultados observados mostram que a solução conseguiu identificar componentes com confiança variável e manter uma estrutura suficiente para alimentar a construção de relações e a geração de ameaças. [1][2]

### Reconhecimento de Texto (OCR)
Após a localização dos componentes, o sistema aplica OCR para extrair os rótulos textuais visíveis nos diagramas. Essa etapa utiliza pré-processamento de imagem para aumentar o contraste e reduzir ruído antes da leitura textual, permitindo associar nomes ou indícios semânticos aos componentes detectados. [3][1]

O OCR é importante porque complementa a detecção visual com contexto semântico. Mesmo quando os rótulos não são perfeitamente legíveis, eles ajudam a distinguir elementos e enriquecer a interpretação do diagrama, especialmente em arquiteturas com nomenclaturas técnicas. [1][2]

### Construção de Topologia
Com os componentes detectados e seus rótulos associados, o sistema constrói uma representação topológica da arquitetura. Essa etapa infere relações entre componentes com base em critérios espaciais e organiza os elementos em uma estrutura de grafo, permitindo representar fluxos de dados entre origem e destino. [3][1][2]

A topologia é o elo entre visão computacional e análise de segurança. Em vez de apenas listar caixas detectadas, o pipeline passa a representar a arquitetura como um conjunto conectado de interações, o que é essencial para modelar ameaças associadas à comunicação entre componentes. [1][2]

### Modelagem STRIDE
Com a topologia consolidada, o motor STRIDE aplica ameaças por componente e por fluxo. Para componentes, o sistema associa categorias como **Tampering**, **Information Disclosure** e **Spoofing** com base no tipo identificado; para fluxos de dados, gera ameaças como **Tampering** e **Repudiation**, acompanhadas de contramedidas recomendadas. [1][2]

Essa etapa transforma a interpretação estrutural em valor de segurança. O resultado final deixa de ser apenas uma leitura da arquitetura e passa a oferecer uma análise prática, com vulnerabilidades prováveis e sugestões objetivas como TLS 1.2+, OAuth2/OIDC, rate limiting, WAF, audit logs e correlação de traces. [2]

## 🛠️ Tecnologias Utilizadas

- **Python 3** como linguagem principal de implementação e orquestração do pipeline. [3]
- **Jupyter Notebook / Google Colab** como ambiente de execução e experimentação do fluxo. [3]
- **Ultralytics YOLOv8** para detecção supervisionada de componentes em diagramas. [3]
- **OpenCV** para pré-processamento de imagens e preparação dos recortes para OCR. [3]
- **PyTesseract** para reconhecimento óptico de caracteres nos rótulos dos componentes. [3]
- **NetworkX** para estruturação da topologia em forma de grafo. [3]
- **Pandas** para organização tabular dos resultados intermediários e finais. [3]
- **Matplotlib** para apoio à visualização e inspeção dos resultados do pipeline. [3]

## 📂 Estrutura do Repositório

A estrutura abaixo representa uma organização coerente com o fluxo implementado no código e com os artefatos utilizados ao longo da solução:

```text
├── data/
│   ├── raw/                  # Imagens originais de diagramas de arquitetura
│   ├── annotated/            # Dataset anotado para detecção supervisionada
│   └── splits/               # Divisões de treino, validação e teste
├── models/                   # Pesos treinados do modelo de detecção
├── notebooks/                # Notebook principal da solução e experimentos relacionados
├── outputs/                  # Relatórios gerados, grafos, tabelas e imagens de saída
├── docs/                     # Documentação complementar do projeto
└── README.md                 # Este documento
```

Essa organização separa claramente os insumos do modelo, os artefatos de treinamento, o código executável e os resultados gerados. Ela facilita tanto a manutenção técnica quanto a evolução futura da solução. [3]

## ⚙️ Como Executar

O fluxo completo pode ser executado a partir do notebook principal da solução.

1. Instale as dependências necessárias do ambiente Python.
2. Abra o notebook no Jupyter ou Google Colab.
3. Execute as células na ordem definida pelo pipeline.
4. Forneça uma imagem de diagrama arquitetural para processamento.
5. Analise o relatório final com componentes detectados, relações inferidas e ameaças STRIDE. [3][1][2]

Um conjunto típico de dependências inclui bibliotecas de detecção, OCR, grafos e análise de dados, como `ultralytics`, `opencv-python`, `pytesseract`, `networkx`, `pandas` e `matplotlib`. [3]

## 📄 Saída Gerada

A saída principal da solução é um relatório estruturado contendo resumo executivo, componentes detectados, relações inferidas, ameaças por componente e ameaças por fluxo de dados. No fluxo observado, essa saída inclui vulnerabilidades associadas aos elementos identificados e contramedidas práticas de mitigação. [1][2]

Esse formato torna o resultado compreensível tanto para times técnicos quanto para avaliadores de produto, porque conecta visão computacional, estrutura arquitetural e análise de segurança em um único artefato legível. [2]