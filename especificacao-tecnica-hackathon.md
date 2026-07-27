# 🎤 Roteiro de Apresentação — Hackathon FIAP

## 1. Abertura
Bom dia. Este projeto apresenta uma solução de **modelagem de ameaças com IA** aplicada a diagramas de arquitetura de software. A proposta é transformar uma imagem arquitetural em uma análise estruturada de segurança, identificando componentes, inferindo fluxos e gerando ameaças com base na metodologia STRIDE. [1][2]

## 2. Contexto do Problema
A análise de ameaças ainda é, em muitos cenários, um processo manual, dependente de leitura visual de diagramas, interpretação humana e conhecimento especializado em segurança. Isso torna a atividade mais lenta, menos escalável e sujeita a inconsistências, especialmente em ambientes com muitas arquiteturas e necessidade de resposta rápida. [1][2]

## 3. Proposta da Solução
A solução foi construída como um pipeline que une visão computacional, OCR, estruturação topológica e regras STRIDE. Em vez de apenas ler uma imagem, o sistema busca interpretar o diagrama como uma arquitetura composta por entidades e relações, convertendo esse entendimento em uma saída prática de segurança. [1][2]

## 4. Como o Sistema Funciona
### 4.1 Detecção de Componentes
O primeiro passo é a identificação visual dos elementos do diagrama. Para isso, a solução utiliza **YOLOv8**, que localiza componentes arquiteturais e atribui classes com base no modelo treinado. Essa etapa transforma o diagrama em um conjunto inicial de entidades técnicas detectáveis. [3][1][2]

### 4.2 Reconhecimento de Texto (OCR)
Depois da detecção visual, o sistema extrai os rótulos textuais presentes nos componentes. O OCR recebe apoio de pré-processamento com OpenCV para melhorar contraste e legibilidade antes da leitura dos textos. Essa etapa complementa a visão computacional com contexto semântico, ajudando a enriquecer a interpretação dos elementos detectados. [3][1]

### 4.3 Construção de Topologia
Com componentes e rótulos disponíveis, a solução organiza a arquitetura em forma de grafo. As relações entre elementos são inferidas a partir de critérios espaciais, permitindo representar fluxos de dados entre componentes de origem e destino. Esse passo é importante porque conecta a detecção visual à leitura estrutural da arquitetura. [3][1][2]

### 4.4 Modelagem STRIDE
Na etapa final, o sistema aplica a metodologia STRIDE sobre os componentes e fluxos identificados. Isso permite gerar ameaças como Spoofing, Tampering, Information Disclosure e Repudiation, além de sugerir contramedidas compatíveis com cada cenário detectado. [1][2]

## 5. Resultado Entregue
No fluxo observado da solução, o sistema foi capaz de detectar múltiplos componentes, inferir relações entre eles e gerar ameaças por elemento e por fluxo de dados. Na execução mais robusta desse pipeline, foram detectados **8 componentes**, inferidas **8 relações** e produzidas **32 ameaças**, cobrindo categorias como Denial of Service, Information Disclosure, Repudiation, Spoofing e Tampering. [2]

Esse resultado mostra que a solução não se limita a identificar caixas em uma imagem. Ela estrutura o diagrama como arquitetura e converte essa estrutura em uma análise objetiva de segurança. [2]

## 6. Valor da Solução
O valor central do projeto está em automatizar uma etapa que normalmente exige esforço manual e alta especialização. A ferramenta reduz a distância entre desenho arquitetural e análise de risco, criando uma saída útil para times de segurança, arquitetura e engenharia. [1][2]

Além disso, a abordagem demonstra que técnicas de visão computacional podem ser aplicadas não apenas à identificação de objetos genéricos, mas também à leitura semântica de artefatos técnicos, como diagramas de software. [1][2]

## 7. Tecnologias Utilizadas
A solução foi desenvolvida com uma base tecnológica orientada a processamento de imagem, detecção supervisionada, OCR e grafos:

- **Python 3** como base de implementação. [3]
- **Jupyter Notebook / Google Colab** como ambiente de execução. [3]
- **Ultralytics YOLOv8** para detecção de componentes. [3]
- **OpenCV** para pré-processamento de imagem. [3]
- **PyTesseract** para OCR. [3]
- **NetworkX** para modelagem topológica em grafo. [3]
- **Pandas** e **Matplotlib** para organização e visualização de resultados. [3]

## 8. Encerramento
Esta entrega demonstra uma arquitetura funcional de análise automatizada de ameaças a partir de diagramas de software. O principal resultado do projeto é mostrar que uma imagem de arquitetura pode ser convertida em componentes, relações e ameaças de forma estruturada, criando uma base concreta para apoio à segurança de sistemas. [1][2]

Obrigado.