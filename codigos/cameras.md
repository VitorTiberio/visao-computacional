# Como usar uma câmera no OpenCV ? #

--- 

Para utilizar uma câmera (como a Webcam de seu computador, por exemplo), utiliza-se o comando **VideoCapture** da Biblioteca OpenCV. 

No caso, uma simples implementação seria: 

```python
import cv2 as cv

cap = cv.VideoCapture(0)
```

Note que o argumento de VideoCapture, nesse caso, é zero (0). Esse argumento é utilizado para saber qual câmera do dispositivo você quer utilizar. Então, caso você tenha duas webcams e queria utilizar a segunda webcam, o argumento será 1, e por assim vai... 

---

Para controlarmos quanto tempo esse vídeo será "mostrado" na tela do usuário, deve-se implementar um loop do tipo While, para que assim que uma tecla do teclado seja pressionada, o vídeo seja fechado. 

Implementamos o código da seguinte forma: 
```python

import numpy as np
import cv2 as cv

cap = cv.VideoCapture(0)

while True:
  ret, frame = cap.read() ## frame será uma imagem instantânea daquele momento do vídeo (é um array do numpy) e ret será um indicador se a captura da imagem está "funcionando" corretamente
  cv.imshow("frame", frame) ## aqui é do mesmo princípio de processamento digital de imagens. Você vai exibir a imagem em uma outra janela chamada "frame". Dará a impressão que é um vídeo, pois, devido ao loop, a variável frame será atualizada a cada segundo

  if cv.WaitKey(1) == ord('q'): ## adiciona uma condição de parada. Se a tecla "Q" do teclado for pressionanda, o programa interrompe
    break

cap.release() ## "libera" o uso da câmera para outro dispositivo do computador, uma vez que o VideoCapture toma "posse" do poder de uso da câmera do dispositivo.
cv.destroyAllWindows() ## fecha todas as janelas que foram abertas no código 
```
  
