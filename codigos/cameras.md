# Como usar uma câmera no OpenCV ? #

--- 

Para utilizar uma câmera (como a Webcam de seu computador, por exemplo), utiliza-se o comando **VideoCapture** da Biblioteca OpenCV. 

No caso, uma simples implementação seria: 

```python
import cv2 as cv

cap = cv.VideoCapture(0)
```

Note que o argumento de VideoCapture, nesse caso, é zero (0). Esse argumento é utilizado para saber qual câmera do dispositivo você quer utilizar. Então, caso você tenha duas webcams e queria utilizar a segunda webcam, o argumento será 1, e por assim vai... 

Para controlarmos quanto tempo esse vídeo será "mostrado" na tela do usuário, deve-se implementar um loop do tipo While, para que assim que uma tecla do teclado seja pressionada, o vídeo seja fechado. 

Implementamos isso da seguinte forma: 

