# TP DE ICV - Compressor QOI (Quite Okay Image)
### Alunos: Arthur Linhares Madureira - 2021031599, César Morais - 2021031521 e Tomas Lacerda - 2021088116

### Algoritmo QOI (Quite Okay Image)

O algoritmo QOI (Quite Okay Image) é um formato de compressão de imagens desenvolvido para ser simples, rápido e eficiente. Ele é projetado para oferecer uma compressão sem perda de qualidade e é especialmente útil para imagens que contêm muitas áreas de cores repetidas. Aqui está uma explicação da metodologia por trás do algoritmo QOI:

#### Estrutura do Arquivo

Um arquivo QOI é composto por três partes principais:
1. **Cabeçalho**: Contém informações essenciais sobre a imagem.
2. **Dados**: Contém os dados comprimidos da imagem.
3. **Marcador de Fim**: Indica o fim dos dados da imagem.

##### Cabeçalho (14 bytes)
- **Magic Bytes (4 bytes)**: "qoif", usado para identificar o arquivo como um arquivo QOI.
- **Largura (4 bytes)**: A largura da imagem em pixels (big-endian).
- **Altura (4 bytes)**: A altura da imagem em pixels (big-endian).
- **Canais (1 byte)**: Número de canais de cores (3 para RGB, 4 para RGBA).
- **Espaço de Cor (1 byte)**: Indica o espaço de cor (0 para sRGB com alfa linear, 1 para todos os canais lineares).

#### Compressão dos Dados

O QOI utiliza um conjunto de técnicas para comprimir os dados da imagem de maneira eficiente:

1. **Codificação por Índice**:
   - Mantém uma tabela de 64 entradas de cores recentemente vistas.
   - Quando uma cor é encontrada novamente, um índice para essa cor é armazenado em vez dos valores completos dos pixels.

2. **Codificação por Diferença**:
   - Para cores que mudam ligeiramente de um pixel para o próximo, o QOI armazena a diferença entre os valores de cor.
   - Utiliza um único byte para armazenar pequenas diferenças entre as cores.

3. **Codificação Luma**:
   - Extensão da codificação por diferença, otimizada para a diferença no canal de verde (luminância).
   - Armazena a diferença do verde e as diferenças relativas dos canais vermelho e azul em dois bytes.

4. **Codificação de Execução (Run-Length Encoding)**:
   - Agrupa sequências de pixels idênticos.
   - Armazena o número de pixels consecutivos que possuem a mesma cor, utilizando um único byte para representar até 62 pixels iguais.

5. **Codificação Literal (RGB/RGBA)**:
   - Para pixels que não podem ser eficientemente codificados pelos métodos anteriores, os valores RGB ou RGBA são armazenados diretamente.

#### Processamento dos Dados

O algoritmo processa cada pixel da imagem, utilizando as técnicas de compressão descritas para reduzir o tamanho dos dados armazenados. Durante a decompressão, o processo é invertido, reconstruindo a imagem original a partir dos dados comprimidos.

#### Marcador de Fim (8 bytes)
- **Marcador**: Uma sequência de 8 bytes zero, indicando o fim dos dados da imagem.

### Benefícios do QOI

- **Simplicidade**: O algoritmo é simples de implementar e entender, utilizando operações básicas e estruturas de dados.
- **Velocidade**: O processamento é rápido tanto na compressão quanto na descompressão, sendo adequado para aplicações em tempo real.
- **Eficiência**: Oferece uma boa relação de compressão para imagens com áreas de cores repetidas, como gráficos e ilustrações.

### Conclusão

O QOI é uma solução eficaz para compressão de imagens, equilibrando simplicidade, velocidade e eficiência. Ele é ideal para situações onde a compressão sem perda é necessária e o desempenho é uma prioridade. Com sua abordagem direta e técnicas de compressão bem escolhidas, o QOI se destaca como um formato prático e útil para uma variedade de aplicações.
