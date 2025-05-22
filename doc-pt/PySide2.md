O módulo **PySide2** é o **binding oficial da Qt 5 para Python**, desenvolvido pela **Qt for Python**. Ele permite criar **interfaces gráficas (GUI)** ricas e modernas em Python, usando os recursos poderosos do **Qt Framework**, que é amplamente usado para desenvolver aplicações multiplataforma.

---

## ✅ O que é o PySide2?

* É o **Qt para Python**, compatível com **Qt 5.15**.
* Permite usar componentes como **janelas, botões, menus, caixas de diálogo, gráficos, etc.**
* Funciona em **Windows 10**, **Ubuntu Linux**, **macOS**.
* É uma alternativa ao **PyQt5**, mas com **licença LGPL** (mais permissiva para projetos comerciais).

---

## ✅ Como instalar o PySide2?

### 💻 No **Windows 10** ou **Ubuntu Linux** (Python já instalado):

```bash
pip install PySide2
```

---

## ✅ Estrutura típica de uma aplicação PySide2

```python
import sys
from PySide2.QtWidgets import QApplication, QLabel, QPushButton, QVBoxLayout, QWidget
```

---

## ✅ Exemplo completo comentado passo a passo

```python
# importar módulos essenciais
import sys
from PySide2.QtWidgets import QApplication, QLabel, QPushButton, QVBoxLayout, QWidget

# criar uma função principal
def main():
    # 1️⃣ Criar o objeto da aplicação (obrigatório)
    app = QApplication(sys.argv)

    # 2️⃣ Criar o widget principal (janela)
    janela = QWidget()
    janela.setWindowTitle("Exemplo PySide2")

    # 3️⃣ Criar widgets de interface
    texto = QLabel("Olá, PySide2!")
    botao = QPushButton("Fechar")

    # 4️⃣ Conectar o botão à função para fechar a app
    botao.clicked.connect(app.quit)

    # 5️⃣ Criar um layout vertical e adicionar widgets
    layout = QVBoxLayout()
    layout.addWidget(texto)
    layout.addWidget(botao)

    # 6️⃣ Aplicar o layout à janela
    janela.setLayout(layout)

    # 7️⃣ Mostrar a janela
    janela.show()

    # 8️⃣ Executar o loop de eventos
    sys.exit(app.exec_())

# chamar a função principal
if __name__ == "__main__":
    main()
```

---

## ✅ Explicação passo a passo

| Passo | Função                  | Descrição                                        |
| ----- | ----------------------- | ------------------------------------------------ |
| 1️⃣   | `QApplication`          | Inicializa a aplicação Qt                        |
| 2️⃣   | `QWidget`               | Cria uma janela base                             |
| 3️⃣   | `QLabel`, `QPushButton` | Widgets visuais                                  |
| 4️⃣   | `.clicked.connect(...)` | Liga o clique do botão a uma ação                |
| 5️⃣   | `QVBoxLayout`           | Layout vertical para organizar os widgets        |
| 6️⃣   | `setLayout(...)`        | Define o layout da janela                        |
| 7️⃣   | `show()`                | Mostra a janela na tela                          |
| 8️⃣   | `exec_()`               | Inicia o loop principal da app (interface ativa) |

---

## ✅ Compatibilidade

| Sistema           | Estado                                          |
| ----------------- | ----------------------------------------------- |
| ✅ Windows 10      | Totalmente compatível                           |
| ✅ Ubuntu Linux    | Totalmente compatível                           |
| ✅ Multiplataforma | Pode compilar e rodar no Linux, Windows e macOS |

---

## ✅ Módulos importantes do PySide2

| Módulo         | Função                         |
| -------------- | ------------------------------ |
| `QtWidgets`    | Botões, janelas, layouts       |
| `QtCore`       | Sinais, slots, datas, arquivos |
| `QtGui`        | Desenho, fontes, eventos       |
| `QtMultimedia` | Som e vídeo                    |
| `QtNetwork`    | Comunicação de rede            |

---

## ✅ Como correr no Ubuntu

1. Certifique-se de que tem Python 3:

   ```bash
   sudo apt update
   sudo apt install python3 python3-pip
   ```

2. Instale PySide2:

   ```bash
   pip3 install PySide2
   ```

3. Grave o script num ficheiro `exemplo.py`, depois execute:

   ```bash
   python3 exemplo.py
   ```

---

## ❗ Dica: Atualizar PySide2

```bash
pip install --upgrade PySide2
```

---
