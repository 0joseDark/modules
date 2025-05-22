[voltar](https://github.com/0joseDark/modules/blob/main/README.md)
- O módulo `win32com` é um componente da biblioteca `pywin32`, usada exclusivamente em sistemas **Windows**. Ele permite interagir com objetos **COM (Component Object Model)**, como o **Excel**, **Word**, **Outlook**, e outros componentes do Windows que suportam automação.

---

## ⚠️ Importante:

* `win32com` **só funciona no Windows**.
* **Não é compatível com Ubuntu/Linux**, pois depende da tecnologia COM, que é exclusiva do Windows.

---

## ✅ Instalação no Windows 10

1. Abre o terminal (cmd ou PowerShell).
2. Instala a biblioteca `pywin32`, que inclui `win32com`:

```bash
pip install pywin32
```

---

## 🧠 O que é COM (Component Object Model)?

É uma tecnologia da Microsoft que permite automação entre aplicações. Com `win32com`, por exemplo, podemos:

* Abrir o Excel
* Criar uma folha de cálculo
* Escrever dados
* Guardar e fechar

---

## 📦 Estrutura do módulo `win32com.client`

O módulo mais usado é:

```python
import win32com.client
```

Ele permite **ligar a aplicações COM**, como `Excel.Application`, `Word.Application`, etc.

---

## 🧪 Exemplo completo: Criar um ficheiro Excel com Python (Windows 10)

### Objetivo:

Criar um ficheiro Excel chamado `exemplo.xlsx` com dados na célula A1.

### Código comentado passo a passo:

```python
import win32com.client
import os

# 1. Iniciar o Excel (invisível)
excel = win32com.client.Dispatch("Excel.Application")
excel.Visible = False  # True para mostrar o Excel durante a execução

# 2. Criar um novo livro (workbook)
workbook = excel.Workbooks.Add()

# 3. Selecionar a primeira folha (worksheet)
sheet = workbook.Worksheets(1)

# 4. Escrever um valor na célula A1
sheet.Cells(1, 1).Value = "Olá, mundo!"

# 5. Guardar o ficheiro
caminho = os.path.abspath("exemplo.xlsx")
workbook.SaveAs(caminho)

# 6. Fechar o Excel
workbook.Close(SaveChanges=True)
excel.Quit()

print("Ficheiro criado em:", caminho)
```

---

## 📝 Explicações das linhas principais

| Linha                           | Explicação                        |
| ------------------------------- | --------------------------------- |
| `Dispatch("Excel.Application")` | Inicia a aplicação Excel via COM  |
| `excel.Visible = False`         | Corre em fundo (sem abrir janela) |
| `Workbooks.Add()`               | Cria novo ficheiro Excel          |
| `Worksheets(1)`                 | Acede à primeira folha            |
| `Cells(1, 1).Value = ...`       | Escreve na célula A1              |
| `SaveAs(...)`                   | Guarda o ficheiro com caminho     |
| `Close()` e `Quit()`            | Fecha o Excel e liberta recursos  |

---

## 📛 No Ubuntu/Linux:

`win32com` **não funciona**. Em sistemas Linux, para gerar um Excel usa-se:

```bash
pip install openpyxl
```

E código alternativo:

```python
from openpyxl import Workbook

wb = Workbook()
ws = wb.active
ws['A1'] = "Olá, mundo!"
wb.save("exemplo.xlsx")
```

---

## ✅ Resumo:

| Sistema      | Módulo usado      | Suporte COM | Alternativa sugerida |
| ------------ | ----------------- | ----------- | -------------------- |
| Windows 10   | `win32com.client` | ✅ Sim       | `openpyxl`, `pandas` |
| Ubuntu/Linux | ❌ Não suportado   | ❌ Não       | `openpyxl`, `pandas` |
