# Aula 03 — Inteligência Artificial para Visão Computacional

> **Disciplina:** SEL-0339 — Visão Computacional (EESC/USP)  
> **Material-base:** Aula 3 — Inteligência Artificial para Visão Computacional, Prof. Marcelo Andrade da Costa Vieira e João Manoel Herrera Pinheiro.

## 1. Aprendizado de Máquina (Machine Learning)

**Machine Learning (ML)** é a área que estuda algoritmos capazes de melhorar seu desempenho em uma tarefa a partir da experiência (dados), sem que todas as regras sejam explicitamente programadas.

Segundo a formulação apresentada na aula, podemos identificar:
- **Experiência (E):** dados utilizados pelo algoritmo;
- **Tarefa (T):** aquilo que o algoritmo deve executar;
- **Desempenho (P):** métrica utilizada para avaliar os resultados.

Em um problema de predição, um erro simples pode ser expresso por:

$$e_i = y_i - \hat{y}_i$$

em que $y_i$ é o valor real e $\hat{y}_i$ é o valor previsto.

## 2. Breve histórico das redes neurais

| Período | Marco apresentado na aula |
|---|---|
| 1943 | McCulloch e Pitts propõem um modelo de neurônio artificial. |
| 1950 | Alan Turing apresenta o Teste de Turing. |
| 1958 | Rosenblatt desenvolve o Perceptron. |
| 1959 | Widrow e Hoff introduzem o ADALINE. |
| 1969 | Discussão das limitações dos perceptrons de camada única, como o problema XOR. |
| 1980 | Neocognitron, precursor das redes convolucionais. |
| 1986 | Popularização da retropropagação (*backpropagation*). |
| Décadas de 1980–1990 | Desenvolvimento das CNNs por Yann LeCun e colaboradores. |
| 2012 | AlexNet impulsiona o uso de redes profundas para reconhecimento de imagens. |
| 2017 | Arquitetura Transformer. |

A trajetória mostra a evolução de modelos simples para arquiteturas capazes de aprender características complexas diretamente das imagens.

## 3. Neurônio artificial e Perceptron

Um neurônio artificial combina entradas ($x_i$) com pesos ($w_i$), soma um **viés (bias)** e aplica uma **função de ativação**:

$$u = \sum_{i=1}^{n} w_i x_i + b$$

$$\hat{y} = g(u)$$

- **Pesos:** representam a influência de cada entrada.
- **Bias:** desloca o limiar de ativação.
- **Função de ativação:** transforma o sinal combinado em uma saída.

O **Perceptron** é um classificador supervisionado que atualiza seus pesos com base nos erros. Sua limitação principal é que **um único perceptron só produz fronteiras de decisão lineares** e, portanto, não resolve sozinho o problema XOR.

O **ADALINE** utiliza uma abordagem de aprendizado associada à minimização do erro quadrático.

### Perceptron de múltiplas camadas (MLP)

Uma **MLP** adiciona camadas ocultas e funções de ativação não lineares, permitindo aprender fronteiras de decisão mais complexas, como as necessárias para o XOR.

## 4. Conceitos importantes no treinamento

| Conceito | Significado |
|---|---|
| **Epoch (época)** | Uma passagem completa pelo conjunto de treinamento. |
| **Batch (lote)** | Grupo de amostras utilizado em uma atualização do modelo. |
| **Learning rate ($\alpha$)** | Define o tamanho dos passos de atualização dos parâmetros. |
| **Loss function** | Quantifica a diferença entre previsões e resultados esperados. |
| **Overfitting** | O modelo se ajusta demais aos exemplos de treino e generaliza mal. |
| **Validação** | Conjunto utilizado para acompanhar o desempenho fora do treinamento e apoiar escolhas do modelo. |

**Atualização em lote (*batch*):** os parâmetros são atualizados a partir dos erros de um conjunto de amostras.  
**Aprendizado online:** os parâmetros são atualizados após cada amostra.

### Funções de ativação

- **Sigmoid:** produz valores entre 0 e 1; comum em saídas de classificação binária.
- **Tanh:** produz valores entre -1 e 1.
- **ReLU:** $g(x)=\max(0,x)$; amplamente utilizada em camadas internas.
- **Leaky ReLU:** mantém uma pequena inclinação para entradas negativas.
- **ELU:** variante que utiliza comportamento exponencial para valores negativos.
- **Softmax:** transforma um vetor de valores em probabilidades cuja soma é 1, muito utilizada na classificação multiclasse.

### Gradiente descendente e retropropagação

O **gradiente descendente** ajusta os parâmetros para reduzir a função de perda:

$$\mathbf{w}_{t+1} = \mathbf{w}_{t} - \alpha\nabla L(\mathbf{w}_{t})$$

A **retropropagação (*backpropagation*)** calcula como cada peso contribui para o erro, permitindo a atualização dos parâmetros da rede pelo otimizador.

Uma taxa de aprendizado muito alta pode dificultar a convergência; uma taxa muito baixa pode tornar o treinamento lento.

**Generalização:** é importante observar tanto a perda de treino quanto a de validação. Quando a perda de treino continua caindo, mas a de validação começa a aumentar, pode haver **overfitting**.

## 5. Redes Neurais Convolucionais (CNNs)

Uma imagem colorida pode ser representada como um **tensor** de dimensões *altura × largura × canais*. As **CNNs (Convolutional Neural Networks)** exploram relações espaciais entre pixels usando filtros aplicados sobre pequenas regiões da imagem.

### Operações fundamentais

1. **Convolução:** um filtro (*kernel*) percorre a imagem e produz um **mapa de características (feature map)**.
2. **Ativação:** funções como ReLU introduzem não linearidade.
3. **Pooling:** reduz a resolução espacial dos mapas (por exemplo, com máximo ou média em janelas locais).
4. **Camadas finais:** combinam as características extraídas para gerar previsões.

Os filtros de uma CNN são **aprendidos durante o treinamento**, diferentemente de filtros fixos escolhidos manualmente. As primeiras camadas podem detectar bordas e texturas; camadas posteriores combinam essas informações em padrões mais complexos.

### Formatos de convolução

Para uma dimensão, com passo (*stride*) igual a 1 e kernel de tamanho $K$:

- **Valid (sem preenchimento):** $N_{saída}=N_{entrada}-K+1$.
- **Full (preenchimento completo):** $N_{saída}=N_{entrada}+K-1$.

Essas fórmulas assumem dilatação unitária e as respectivas condições de preenchimento.

### Exemplos de arquiteturas

- **LeNet-5:** reconhecimento de dígitos manuscritos;
- **AlexNet:** marco do avanço do Deep Learning em visão computacional;
- **VGGNet:** empilhamento de convoluções pequenas, especialmente $3\times3$;
- **ResNet, Inception e MobileNet:** outras famílias importantes citadas na aula.

## 6. Aplicações de IA em imagens

| Tarefa | Objetivo |
|---|---|
| **Classificação** | Atribuir uma categoria a uma imagem. |
| **Detecção de objetos** | Localizar e identificar objetos, geralmente com caixas delimitadoras. |
| **Segmentação** | Atribuir classes ou regiões aos pixels da imagem. |
| **Detecção de bordas** | Identificar limites e contornos. |
| **Geração de imagens** | Produzir novas imagens com modelos generativos, como GANs. |
| **Super-resolução** | Obter uma imagem de maior resolução a partir de outra de menor resolução. |

### YOLO — You Only Look Once

O **YOLO** é uma família de modelos de **detecção de objetos**, capaz de prever classes e posições de objetos em uma imagem. A aula ilustra o fluxo de processamento da imagem, execução da rede e pós-processamento das detecções.

### Transfer learning

O **aprendizado por transferência** aproveita conhecimentos de um modelo já treinado em outra tarefa ou conjunto de dados, reduzindo a necessidade de começar o treinamento do zero.

### Mapas de ativação

Mapas de ativação e de saliência ajudam a visualizar as regiões da imagem que mais influenciam determinadas previsões do modelo.



## Referências e material de apoio

- **Slides da Aula 3:** *Inteligência Artificial para Visão Computacional* — SEL-0339, EESC/USP.
- [TensorFlow Playground](https://playground.tensorflow.org/) — experimento interativo de redes neurais (utilizado nos exemplos dos slides).
- LeCun, Y.; Bengio, Y.; Hinton, G. (2015). *Deep learning*. **Nature**, 521, 436–444 (referência citada nos slides).

---

> Resumo elaborado a partir dos conteúdos apresentados nos slides, com redação sintetizada para consulta no GitHub.
