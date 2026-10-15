# Processamento Morfológico de Imagens # 
---

Para consultar a documentação do OpenCV, clique [Aqui](https://docs.opencv.org/3.4.8/d9/d61/tutorial_py_morphological_ops.html)

---

Primeiramente, o que é um processamento morfológico ? Eles se resumem em técnicas de extração de componentes de uma imagem que sejam úteis para representação e descrição de uma forma ou região. 

Uma imagem binária pode ser completamente descrita por um conjuto de todos os seus pixels de "frente" e todas as operações relacionadas à morfologia são definidas em termo de conjuntos. 

Um outro termo importante são os **elementos estruturantes (SE)**. No caso, os mesmos serão as estruturas responsáveis por realizar as operações morfológicas.  

## 1. Elementos Estruturantes (SE) ## 

Os elementos estruturantes são pequenas matrizes utilizadas para analisar a vizinhança de cada pixel durante uma operação morfológica. Sua forma e dimensão determinam como a imagem será modificada.

Os formatos mais comuns são retangular, elíptico e em cruz.

Para a sua utilização, no OpenCV, pode-se escrever: 

```python
import cv2 as cv

SE_quadrado = cv.getgetStructuringElement(cv.MORPH_RECT, (3, 3)) ## SE Quadrado ou Retangular (dependendo das dimensões)

SE_cross = cv.getStructuringElement(cv.MORPH_CROSS, (3,3)) ## SE com o formato de cruz

SE_elipse = cv.getStructuringElement(cv.MORPH_ELLIPSE, (3,3)) ## SE com o formato circular (se os parâmetros forem iguais, a elipse vira um circulo)
```

Uma outra maneira (mais arcaica) de criar um SE é utilizando uma função: 

```python
def structure_element_quadrado(dim):
  SE = np.ones((dim,dim), dtype=np.uint8)
  return SE
```
---

## 2. Erosão ##

A erosão é uma operação morfológica que tende a reduzir as regiões brancas (objetos) de uma imagem binária.

Considerando um elemento estruturante, um pixel permanecerá branco somente se todos os pixels da vizinhança exigidos pelo elemento estruturante também pertencerem ao objeto.

Suas principais aplicações são a remoção de pequenos ruídos brancos, a separação de objetos conectados por regiões estreitas e a redução de bordas.

Para sua aplicação no OpenCV, temos: 

```python
img_erode = cv.erode(img, SE, iterations=1)
```

--- 

## 3. Dilatação ## 

A dilatação realiza a operação oposta à erosão, tendendo a expandir as regiões brancas de uma imagem binária.

Ela permite preencher pequenas lacunas, conectar regiões próximas e aumentar a espessura dos objetos.

Em Python, temos: 

```python
img_dilatada = cv.dilate(img, SE, iterations=1)
```

--- 

## 4. Abertura e Fechamento ## 

Além das operações primitivas, existem operações compostas, obtidas pela combinação de erosão e dilatação.

Abertura: consiste em aplicar uma erosão seguida de uma dilatação, utilizando o mesmo elemento estruturante. É especialmente útil para eliminar pequenos objetos brancos e conexões estreitas.

```pyhton
img_abertura = cv.morphologyEx(img, cv.MORPH_OPEN, SE)
```

Fechamento: consiste em aplicar uma dilatação seguida de uma erosão. É utilizado para preencher pequenos buracos pretos e conectar regiões próximas.


```pyhton
img_close = cv.morphologyEx(img, cv.MORPH_CLOSE, SE)
```
