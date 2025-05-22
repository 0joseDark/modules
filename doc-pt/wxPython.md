O módulo `wxPython` é uma biblioteca para criar interfaces gráficas (GUIs) em Python, baseada na biblioteca C++ `wxWidgets`. Funciona em Windows, macOS e Linux (como Ubuntu). Vamos ver passo a passo como instalar e usar o `wxPython`, com um exemplo completo de uma aplicação GUI com botões, texto e eventos.

---

## ✅ PASSO A PASSO – INSTALAÇÃO

### 🔹 No **Windows 10**:

1. Abra o **Prompt de Comando** (cmd).
2. Instale com o `pip`:

   ```bash
   pip install wxPython
   ```

### 🔹 No **Ubuntu Linux**:

1. Abra o **Terminal**.
2. Instale dependências:

   ```bash
   sudo apt-get update
   sudo apt-get install libgtk-3-dev libgl1-mesa-dev libglu1-mesa-dev
   ```
3. Instale com `pip`:

   ```bash
   pip install wxPython
   ```

---

## ✅ ESTRUTURA BÁSICA DE UM PROGRAMA COM wxPython

```python
import wx

app = wx.App(False)           # Cria a aplicação
frame = wx.Frame(None, title="Minha Janela")  # Cria a janela
frame.Show()                  # Mostra a janela
app.MainLoop()                # Inicia o loop principal
```

---

## ✅ EXEMPLO COMPLETO – Aplicação com:

* Janela com título
* Caixa de texto
* Botões: "Mostrar Texto", "Limpar", "Sair"
* Mensagens de alerta (caixa de diálogo)

### 🔽 CÓDIGO COMENTADO:

```python
import wx

class MinhaJanela(wx.Frame):
    def __init__(self, parent, title):
        super(MinhaJanela, self).__init__(parent, title=title, size=(400, 300))

        # Painel principal onde os componentes vão estar
        painel = wx.Panel(self)

        # Caixa de texto
        self.caixa_texto = wx.TextCtrl(painel, pos=(20, 20), size=(340, 30))

        # Botão "Mostrar Texto"
        botao_mostrar = wx.Button(painel, label="Mostrar Texto", pos=(20, 70))
        botao_mostrar.Bind(wx.EVT_BUTTON, self.mostrar_texto)

        # Botão "Limpar"
        botao_limpar = wx.Button(painel, label="Limpar", pos=(160, 70))
        botao_limpar.Bind(wx.EVT_BUTTON, self.limpar_texto)

        # Botão "Sair"
        botao_sair = wx.Button(painel, label="Sair", pos=(280, 70))
        botao_sair.Bind(wx.EVT_BUTTON, self.sair_aplicacao)

        self.Centre()  # Centraliza a janela no ecrã

    def mostrar_texto(self, event):
        texto = self.caixa_texto.GetValue()
        wx.MessageBox(f"O texto escrito foi:\n{texto}", "Texto Inserido", wx.OK | wx.ICON_INFORMATION)

    def limpar_texto(self, event):
        self.caixa_texto.SetValue("")

    def sair_aplicacao(self, event):
        self.Close()  # Fecha a janela

# Execução da aplicação
if __name__ == "__main__":
    app = wx.App(False)
    frame = MinhaJanela(None, "Aplicação com wxPython")
    frame.Show()
    app.MainLoop()
```

---

## ✅ EXPLICAÇÃO DOS COMPONENTES

| Componente      | Descrição                                      |
| --------------- | ---------------------------------------------- |
| `wx.Frame`      | Janela principal da aplicação                  |
| `wx.Panel`      | Área interna da janela onde ficam os elementos |
| `wx.TextCtrl`   | Caixa de texto editável                        |
| `wx.Button`     | Botão com texto clicável                       |
| `wx.MessageBox` | Caixa de mensagem pop-up                       |
| `Bind()`        | Liga um botão a uma função (evento)            |

---

## ✅ COMO EXECUTAR

1. Guarde o código num ficheiro chamado por exemplo `app_wxpython.py`.
2. Execute com:

   ```bash
   python app_wxpython.py
   ```

---

## ✅ FUNCIONA EM:

| Sistema       | Funciona?                      |
| ------------- | ------------------------------ |
| Windows 10    | ✅                              |
| Ubuntu 20.04+ | ✅ (após instalar dependências) |

---
