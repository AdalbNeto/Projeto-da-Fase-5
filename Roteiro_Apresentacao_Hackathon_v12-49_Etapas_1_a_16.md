# Roteiro de Apresentação Hackathon — v12-49 por Etapas

## Abertura

Este roteiro apresenta a solução **v12-49** como um pipeline de ponta a ponta para modelagem de ameaças com IA, organizado em 16 etapas objetivas do notebook-base do MVP. [1]

A proposta do projeto é transformar um diagrama de arquitetura em uma análise automatizada que detecta componentes, lê rótulos, monta a topologia e sugere ameaças e correções com base em STRIDE. [1][2]

## Problema

Na prática, a modelagem de ameaças costuma ser manual, lenta e dependente de especialistas, o que dificulta sua adoção contínua em times de produto e arquitetura. [2]

A v12-49 resolve isso com um fluxo automatizado que começa no dataset, passa por visão computacional e OCR, e termina em um relatório estruturado de ameaças. [1][2]

## Etapas 1 a 16

### Etapa 1 — Instalação de dependências

Nesta etapa, o notebook instala as bibliotecas necessárias para todo o pipeline, incluindo YOLOv8, OCR, OpenCV, NetworkX, Streamlit e utilitários de apoio. [1]

Ela prepara o ambiente para que detecção, leitura de texto, análise topológica e geração de relatório funcionem de forma integrada. [1]

### Etapa 2 — Importações e configurações globais

Aqui são definidos os diretórios de trabalho, os caminhos de entrada e saída e a taxonomia principal de classes arquiteturais. [1]

Também é nessa fase que o projeto organiza classes como `useractor`, `webclient`, `apigateway`, `applicationservice`, `authservice`, `database`, `messagequeue`, `storage`, `externalsystem` e `networkboundary`. [1]

### Etapa 3 — Coleta do dataset Kaggle

Nesta etapa, o notebook baixa e extrai imagens de diagramas de arquitetura a partir de um dataset hospedado no Kaggle. [1]

Esse passo forma a base visual do treinamento, permitindo que o modelo aprenda padrões gráficos reais de componentes de software. [1]

### Etapa 4 — Visualização e carregamento de amostras

Depois da coleta, o notebook exibe uma amostra inicial das imagens para validar se os dados foram carregados corretamente e se fazem sentido para o problema. [1]

Essa inspeção reduz o risco de treinar o modelo em arquivos corrompidos, irrelevantes ou com baixa qualidade. [1]

### Etapa 5 — Anotação automática assistida

Nesta fase, o projeto gera anotações no formato YOLO com apoio de heurísticas, marcando nas imagens os componentes de arquitetura que serão aprendidos pelo modelo. [1]

É o passo que conecta o critério visual do dataset ao objetivo do hackathon: identificar usuário, API, banco, autenticação, armazenamento e outros blocos arquiteturais. [1]

### Etapa 6 — Preparação dos splits

Aqui o conjunto anotado é separado em treino, validação e teste. [1]

Essa divisão é essencial para medir generalização e evitar que o modelo pareça bom apenas porque memorizou exemplos vistos no treinamento. [1]

### Etapa 7 — Configuração do YOLOv8

Nesta etapa, o notebook monta o `dataset.yaml` e define os parâmetros que serão usados no treinamento do detector. [1]

Com isso, o pipeline informa ao YOLO onde estão as imagens, onde estão os rótulos e quais classes devem ser aprendidas. [1]

### Etapa 8 — Treinamento do modelo

Aqui ocorre o fine-tuning do YOLOv8n para aprender as classes arquiteturais definidas no projeto. [1]

É a etapa central de visão computacional, porque transforma o dataset anotado em um modelo capaz de reconhecer componentes sozinho em novos diagramas. [1]

### Etapa 9 — Avaliação e métricas

Depois do treinamento, o notebook calcula métricas como mAP, precisão, recall e matriz de confusão para entender a qualidade do detector. [1]

Essa etapa é importante para justificar tecnicamente a solução e mostrar à banca que houve medição objetiva de desempenho. [1]

### Etapa 10 — Inferência em nova imagem

Nesta fase, o modelo treinado é aplicado a um novo diagrama para detectar automaticamente os componentes presentes. [1]

Na prática, é aqui que o MVP deixa de ser apenas um experimento de treino e passa a resolver o caso de uso real do hackathon. [1]

### Etapa 11 — Extração OCR

Após detectar os blocos, o notebook executa OCR por região para ler os rótulos textuais de cada componente identificado. [1]

Esse passo complementa a detecção visual, porque o nome do bloco ajuda a enriquecer a interpretação semântica do diagrama. [1][2]

### Etapa 12 — Construção de topologia

Nesta etapa, o pipeline monta um grafo JSON da arquitetura a partir dos componentes detectados. [1]

Esse grafo representa a topologia do sistema e é a base para identificar relações entre elementos, fluxos de dados e superfícies de ataque. [1][2]

### Etapa 13 — Motor STRIDE

Aqui o sistema aplica regras de ameaça por componente e por fluxo, usando a taxonomia STRIDE como mecanismo de raciocínio. [1]

É essa etapa que converte a interpretação do diagrama em ameaças como spoofing, tampering, repudiation, information disclosure, denial of service e elevation of privilege. [1][2]

### Etapa 14 — Base de conhecimento

Nesta fase, o notebook utiliza uma base de conhecimento em YAML com vulnerabilidades, padrões de risco e contramedidas associadas. [1]

Isso permite que o sistema não apenas identifique ameaças, mas também proponha recomendações de correção de maneira estruturada. [1][2]

### Etapa 15 — Geração do relatório

Depois da análise, o pipeline produz um relatório em Markdown com resumo executivo, componentes detectados, ameaças associadas e limitações do MVP. [1][2]

Esse relatório é o principal artefato de negócio da solução, porque transforma a inferência técnica em evidência legível para arquitetos, segurança e banca avaliadora. [1][2]

### Etapa 16 — Visualização dos resultados

Por fim, o notebook exibe as detecções e o relatório dentro do próprio ambiente de execução. [1]

Essa etapa fecha a experiência do usuário, permitindo validar visualmente o que a IA reconheceu e como isso se converteu em análise de ameaças. [1][2]

## Como apresentar

A narrativa recomendada é: primeiro mostrar o problema, depois passar rapidamente pelas 16 etapas e, por fim, destacar que a v12-49 entrega um fluxo completo do diagrama até o relatório final. [1][2]

Na demo, vale enfatizar que o diferencial não está apenas em detectar caixas no diagrama, mas em ligar visão computacional, OCR, topologia e STRIDE em um único pipeline automatizado. [1][2]

## Diferencial da v12-49

A v12-49 deve ser posicionada como a evolução do MVP para apresentação, mantendo a espinha dorsal do notebook validado e refinando sua leitura do diagrama para chegar mais perto de uma análise arquitetural útil. [2]

O ponto forte para a banca é mostrar que o projeto cobre as quatro frentes exigidas: dataset, anotação, treinamento do modelo e sistema de mapeamento de ameaças com sugestões de correção. [calendar_event:0425f190f1cf4ebf82e7b7045beaafde][1][2]