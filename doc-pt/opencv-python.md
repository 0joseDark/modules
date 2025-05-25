O módulo `opencv-python` é uma interface Python para a biblioteca **OpenCV** (Open Source Computer Vision Library), usada para **visão computacional**, **processamento de imagem** e **vídeo**. Vou explicar passo a passo como usar este módulo tanto no **Windows 10** como no **Ubuntu Linux**, seguido de um **exemplo completo com comentários**.

---

## ✅ 1. Instalação do OpenCV-Python

### 🪟 No Windows 10:

Abra o **Prompt de Comando** (cmd) ou **PowerShell**:

```bash
pip install opencv-python
```

### 🐧 No Ubuntu:

Abra o terminal e execute:

```bash
sudo apt update
sudo apt install python3-pip
pip3 install opencv-python
```

🔧 **Opcional (para funcionalidades extras como vídeo)**:

```bash
pip install opencv-contrib-python
```

---

## ✅ 2. Importação no Python

No início do script Python, basta importar assim:

```python
import cv2
```

---

## ✅ 3. Funcionalidades principais do OpenCV

| Função                    | Descrição                               |
| ------------------------- | --------------------------------------- |
| `cv2.imread()`            | Lê uma imagem                           |
| `cv2.imshow()`            | Mostra uma imagem numa janela           |
| `cv2.VideoCapture()`      | Acede à câmara ou ficheiro de vídeo     |
| `cv2.cvtColor()`          | Converte cores (por ex., BGR para GRAY) |
| `cv2.imwrite()`           | Grava uma imagem no disco               |
| `cv2.waitKey()`           | Espera por uma tecla                    |
| `cv2.destroyAllWindows()` | Fecha todas as janelas                  |

---

## ✅ 4. Exemplo completo passo a passo

### 🎯 Objetivo:

* Capturar vídeo da câmara
* Mostrar imagem em tempo real
* Aplicar efeito cinzento (grayscale)
* Gravar a imagem com uma tecla

---

### 🐍 Código Python comentado

```python
import cv2

# Abre a primeira câmara conectada (0 = câmara padrão)
camera = cv2.VideoCapture(0)

# Verifica se a câmara abriu corretamente
if not camera.isOpened():
    print("Erro: Não foi possível aceder à câmara.")
    exit()

# Loop principal
while True:
    # Lê um frame da câmara
    ret, frame = camera.read()
    
    # Verifica se a leitura foi bem-sucedida
    if not ret:
        print("Erro ao capturar imagem.")
        break

    # Converte para escala de cinzento
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    # Mostra a imagem original e a em cinzento
    cv2.imshow("Imagem Original", frame)
    cv2.imshow("Imagem em Cinzento", gray)

    # Espera por uma tecla por 1ms
    key = cv2.waitKey(1) & 0xFF

    # Tecla 's' para salvar imagem
    if key == ord('s'):
        cv2.imwrite("imagem_guardada.png", gray)
        print("Imagem gravada como imagem_guardada.png")

    # Tecla 'q' para sair
    if key == ord('q'):
        break

# Liberta a câmara e fecha as janelas
camera.release()
cv2.destroyAllWindows()
```

---

## ✅ 5. Explicação passo a passo

1. `cv2.VideoCapture(0)` — Abre a webcam padrão.
2. `camera.read()` — Lê um frame da câmara.
3. `cv2.cvtColor(..., cv2.COLOR_BGR2GRAY)` — Converte para cinzento.
4. `cv2.imshow()` — Mostra o frame na janela.
5. `cv2.waitKey(1)` — Espera 1 milissegundo por tecla.
6. `ord('s')` — Se carregar na tecla **s**, guarda imagem.
7. `ord('q')` — Se carregar na tecla **q**, sai do ciclo.
8. `camera.release()` — Liberta a câmara.
9. `cv2.destroyAllWindows()` — Fecha todas as janelas abertas.

---

## ✅ 6. Notas úteis

* Para usar uma **segunda câmara**, use `cv2.VideoCapture(1)`, etc.
* Para **ler um vídeo** de ficheiro:

  ```python
  camera = cv2.VideoCapture('video.mp4')
  ```
* Para **desenhar**:

  ```python
  cv2.rectangle(frame, (10,10), (100,100), (255,0,0), 2)
  ```

---
