# Aula 5
# Análise de Sinais e Sistemas de Comunicação (Signal Analysis and Communication Systems)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](COLOQUE_AQUI_O_LINK_DO_NOTEBOOK)

Este notebook apresenta uma série de análises e simulações focadas em processamento de sinais e sistemas de comunicação digital. Ele explora conceitos como códigos de Hadamard, espalhamento espectral, ruído AWGN, transformada wavelet e técnicas de remoção de ruído baseadas em domínio de tempo/frequência e domínio wavelet.

> Material desenvolvido para fins didáticos, no contexto de uma disciplina de Processamento Digital de Sinais.

## Sumário

- [Requisitos](#requisitos)
- [Estrutura do repositório](#estrutura-do-repositório)
- [Como rodar o notebook](#como-rodar-o-notebook)
- [Conteúdo do notebook](#conteúdo-do-notebook)
  - [1. Espalhamento Espectral com Códigos de Hadamard](#1-espalhamento-espectral-com-códigos-de-hadamard)
  - [2. Análise da Taxa de Erro de Bit (BER)](#2-análise-da-taxa-de-erro-de-bit-ber)
  - [3. Geração e Análise de Sinais Sintéticos](#3-geração-e-análise-de-sinais-sintéticos)
  - [4. Transformada Wavelet e Análise de Sinais](#4-transformada-wavelet-e-análise-de-sinais)
  - [5. Remoção de Ruído com Wavelet vs. DFT](#5-remoção-de-ruído-com-transformada-wavelet-e-comparação-com-dft)
- [Origem dos arquivos utilizados](#origem-dos-arquivos-utilizados)
- [Licença](#licença)

## Requisitos

- Python 3.x
- [numpy](https://numpy.org/)
- [scipy](https://scipy.org/)
- [matplotlib](https://matplotlib.org/)
- [PyWavelets](https://pywavelets.readthedocs.io/) (`pywt`, para as transformadas wavelet bior4.4 e db4)

Se for executar localmente (fora do Colab):

```bash
pip install numpy scipy matplotlib pywavelets
```

> No Colab, o upload do arquivo `leleccum.mat` é feito interativamente — veja [Como rodar o notebook](#como-rodar-o-notebook).

## Estrutura do repositório

```
.
├── notebook.ipynb        # Notebook principal
├── data/
│   └── leleccum.mat       # Sinal real utilizado nas seções de wavelet (gravação/geração própria)
└── README.md
```

> Ajuste os nomes/caminhos acima conforme a organização real do seu repositório.

## Como rodar o notebook

1. Abra o notebook no Google Colab.
2. Para as seções que utilizam o sinal real (**Seções 4 e 5**), será necessário fazer upload do arquivo `leleccum.mat`. Execute a célula de código que contém:
   ```python
   from google.colab import files
   uploaded = files.upload()
   ```
   Uma caixa de diálogo permitirá selecionar o arquivo do seu computador.
3. Execute as células em sequência para ver os resultados, gráficos e métricas (MSE, SNR, BER).

## Conteúdo do notebook

### 1. Espalhamento Espectral com Códigos de Hadamard

Simula um sistema de comunicação Direct Sequence Spread Spectrum (DSSS) utilizando códigos de Hadamard para espalhamento espectral.

- **Geração de matrizes de Hadamard:** implementação de uma função para gerar matrizes de Hadamard.
- **Codificação:** demonstração de como mensagens binárias são espalhadas usando códigos ortogonais de Hadamard.
- **Adição de ruído AWGN:** introdução de ruído branco gaussiano aditivo ao sinal combinado.
- **Decodificação:** processo de recuperação das mensagens originais através de correlação.
- **Visualizações:** gráficos dos sinais originais, códigos de Hadamard e sinais codificados.

### 2. Análise da Taxa de Erro de Bit (BER)

Aprofunda a análise do sistema DSSS, calculando a Taxa de Erro de Bit (BER) sob diferentes cenários de ruído e distorção.

- **BER com ruído no canal:** simulação Monte Carlo para calcular a BER quando o canal é afetado por ruído AWGN, mas o receptor possui conhecimento perfeito dos códigos.
- **BER com código distorcido:** simulação Monte Carlo para calcular a BER quando não há ruído no canal, mas os códigos de Hadamard no receptor são distorcidos por ruído.
- **Comparação:** plotagem e comparação das curvas de BER para ambos os cenários, ilustrando o impacto do ruído em diferentes partes do sistema.

### 3. Geração e Análise de Sinais Sintéticos

Foca na criação e exploração de um sinal sintético complexo.

- **Geração do sinal x(t):** construção de um sinal com múltiplas componentes sinusoidais e impulsos, variando em amplitude e frequência ao longo do tempo.
- **Visualização:** plotagem do sinal gerado para observação de suas características no domínio do tempo.

### 4. Transformada Wavelet e Análise de Sinais

Explora a transformada wavelet discreta (DWT) e sua aplicação em sinais, utilizando as wavelets **bior4.4** e **db4**.

- **Wavelet bior4.4:** análise dos coeficientes dos filtros de análise e síntese, junto com a decomposição do sinal sintético em 5 estágios, detalhando as subfaixas de frequência.
- **Sinal leleccum.mat:** carregamento de um sinal real, normalização e remoção da componente DC.
- **Análise no domínio da frequência:** cálculo e plotagem do espectro de amplitude (FFT) do sinal leleccum para entender suas características de frequência.
- **Wavelet db4:** análise dos filtros e funções mãe/escala.
- **Decomposição do leleccum com db4:** transformada wavelet em 5 estágios, com visualização dos coeficientes em diferentes subfaixas de frequência e cálculo da energia em cada nível.

### 5. Remoção de Ruído com Transformada Wavelet e Comparação com DFT

Demonstra a aplicação da transformada wavelet para remoção de ruído (denoising) e compara seu desempenho com uma abordagem de filtragem baseada na DFT.

- **Denoising wavelet (limiarização):** implementação de uma função de thresholding (modo soft) para os coeficientes wavelet, aplicada com diferentes limiares (baixo, universal, alto) no sinal leleccum. Desempenho avaliado por MSE e SNR.
- **Visualização da limiarização:** plotagem do sinal original e reconstruído para cada limiar, e comparação dos coeficientes de detalhe antes e depois da limiarização.
- **Filtragem baseada em DFT:** aplicação de filtragem no domínio da frequência, zerando componentes espectrais abaixo de um determinado limiar de magnitude.
- **Comparação detalhada:** comparação visual e quantitativa (MSE, SNR, coeficientes mantidos) entre as técnicas de filtragem DFT e wavelet, destacando vantagens e desvantagens de cada método.

## Origem dos arquivos utilizados

- `leleccum.mat`: sinal real, gravado/gerado para uso neste experimento.

## Licença

Este projeto é disponibilizado **apenas para fins educacionais**. Não possui uma licença de código aberto formal — sinta-se à vontade para consultar o conteúdo como referência de estudo, mas reentre em contato antes de qualquer uso fora desse contexto.
