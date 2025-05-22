O módulo **PyQt5** é um conjunto de *bindings* (ligações) em Python para a biblioteca **Qt5**, que é um framework C++ popular para desenvolver interfaces gráficas (GUI). Com PyQt5, pode criar janelas, botões, menus, caixas de texto, e muito mais — de forma multiplataforma, ou seja, o mesmo código pode correr em **Windows 10, Ubuntu Linux, macOS**, etc.

---

## ✅ Instalação do PyQt5

### No **Windows 10** e no **Ubuntu** (via `pip`):

```bash
pip install PyQt5
```

Para verificar se foi instalado corretamente:

```bash
python -c "from PyQt5.QtWidgets import QApplication, QLabel; print('PyQt5 instalado com sucesso')"
```

---

## 🧪 Exemplo passo a passo de um programa PyQt5 simples

Vamos criar uma **janela básica** com um **botão que fecha a aplicação**.

### 🟦 Código completo com comentários

```python
# importar sys para aceder aos argumentos do sistema
import sys

# importar as classes necessárias do módulo PyQt5.QtWidgets
from PyQt5.QtWidgets import QApplication, QWidget, QPushButton

# criar uma classe que herda de QWidget (janela base)
class MinhaJanela(QWidget):
    def __init__(self):
        super().__init__()  # chama o construtor da classe base QWidget
        self.initUI()       # método que configura a interface

    def initUI(self):
        self.setWindowTitle('Exemplo PyQt5')     # título da janela
        self.setGeometry(100, 100, 300, 200)      # posição x, y e dimensão largura, altura

        # criar um botão
        self.botao = QPushButton('Fechar', self)  # texto do botão e parent (self = janela)
        self.botao.move(100, 80)                  # posição do botão dentro da janela
        self.botao.clicked.connect(self.close)    # ligar o clique ao método close() da janela

# ponto de entrada da aplicação
if __name__ == '__main__':
    app = QApplication(sys.argv)  # cria a aplicação (deve ser única)
    janela = MinhaJanela()        # cria uma instância da janela
    janela.show()                 # mostra a janela
    sys.exit(app.exec_())         # inicia o loop da aplicação
```

---

## 🔧 Explicação passo a passo

| Linha                             | Explicação                                                      |
| --------------------------------- | --------------------------------------------------------------- |
| `import sys`                      | Necessário para aceder a `sys.argv`, usado pelo `QApplication`. |
| `from PyQt5.QtWidgets import ...` | Importa classes do módulo Qt para construir a GUI.              |
| `class MinhaJanela(QWidget)`      | Define uma nova janela personalizada.                           |
| `self.setWindowTitle(...)`        | Define o título da janela.                                      |
| `self.setGeometry(...)`           | Define posição e tamanho da janela.                             |
| `QPushButton(...)`                | Cria um botão com o texto "Fechar".                             |
| `self.botao.clicked.connect(...)` | Liga o clique do botão ao método `close()` da janela.           |
| `QApplication(sys.argv)`          | Cria a aplicação Qt (obrigatória).                              |
| `janela.show()`                   | Torna a janela visível.                                         |
| `app.exec_()`                     | Entra no *loop* de eventos da aplicação.                        |

---

## 🪟 Correr no **Windows 10**

1. Guardar o código num ficheiro, por exemplo: `exemplo_pyqt5.py`
2. Executar no terminal:

   ```bash
   python exemplo_pyqt5.py
   ```

---

## 🐧 Correr no **Ubuntu**

### Pré-requisitos no Ubuntu:

```bash
sudo apt update
sudo apt install python3-pyqt5
```

Ou usando `pip`:

```bash
pip install PyQt5
```

Depois:

```bash
python3 exemplo_pyqt5.py
```

---

## 🧱 Componentes comuns do PyQt5

* `QMainWindow` – Janela principal com menu, barra de ferramentas, etc.
* `QDialog` – Janela de diálogo (ex: abrir ficheiro, confirmação).
* `QPushButton` – Botão clicável.
* `QLabel` – Texto ou imagem.
* `QLineEdit` – Campo de entrada de texto.
* `QTextEdit` – Caixa de texto com várias linhas.
* `QVBoxLayout` / `QHBoxLayout` – Layouts verticais/horizontais.

---

## 🔚 Conclusão

O **PyQt5** é uma ferramenta poderosa e multiplataforma para criar aplicações gráficas com Python. Pode ser usada tanto no **Windows 10** como no **Ubuntu** sem alterações no código.

Se quiser posso mostrar como:

* criar menus,
* abrir ficheiros,
* mudar o estilo da aplicação,
* ou usar `QMainWindow` para janelas mais completas.
