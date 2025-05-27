O módulo `markdown` em Python permite converter texto escrito na linguagem **Markdown** (como `.md` ou strings) para **HTML**. Isso é muito útil para gerar páginas web, documentação, ou visualização em navegadores.

Vamos ver **passo a passo** como instalar e usar o módulo `markdown` no **Windows 10** e **Ubuntu Linux**, com um **exemplo completo**.

---

## ✅ 1. INSTALAÇÃO DO MÓDULO `markdown`

### 📌 Windows 10 e Ubuntu (ambos iguais):

1. Abre o terminal:

   * **Windows**: PowerShell ou `cmd`
   * **Ubuntu**: Terminal (Ctrl+Alt+T)

2. Instala com `pip`:

```bash
pip install markdown
```

> ⚠️ Se estiveres a usar Python 3 e `pip` não estiver a funcionar, tenta `pip3`.

---

## ✅ 2. VERIFICAR A INSTALAÇÃO

No terminal, digita:

```bash
python -m markdown --version
```

Se o módulo estiver instalado corretamente, mostra a versão.

---

## ✅ 3. EXEMPLO COMPLETO: Markdown para HTML

### 🎯 Objetivo:

* Lê um ficheiro `.md`
* Converte para HTML
* Guarda o resultado num ficheiro `.html`

### 📁 Estrutura:

```plaintext
meu_projeto/
├── exemplo.md
└── conversor.py
```

### 📝 3.1. Conteúdo do `exemplo.md`:

```markdown
# Título Principal

Este é um parágrafo com **negrito** e *itálico*.

## Lista:
- Item 1
- Item 2
- Item 3

[Link para o Google](https://www.google.com)
```

### 🐍 3.2. Código Python: `conversor.py`

```python
# conversor.py
import markdown

# Caminho do ficheiro .md
ficheiro_md = "exemplo.md"

# Caminho do ficheiro HTML de saída
ficheiro_html = "saida.html"

# Lê o conteúdo do Markdown
with open(ficheiro_md, "r", encoding="utf-8") as f:
    texto_md = f.read()

# Converte para HTML
html = markdown.markdown(texto_md)

# Adiciona estrutura HTML básica
html_final = f"""
<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <title>Documento Convertido</title>
</head>
<body>
{html}
</body>
</html>
"""

# Grava o HTML num ficheiro
with open(ficheiro_html, "w", encoding="utf-8") as f:
    f.write(html_final)

print("Conversão completa: ficheiro 'saida.html' criado com sucesso.")
```

---

## ✅ 4. EXECUTAR O SCRIPT

No terminal, dentro da pasta do projeto, corre:

```bash
python conversor.py
```

> Resultado: será criado o ficheiro `saida.html`.

---

## ✅ 5. ABRIR NO NAVEGADOR

Abre o ficheiro `saida.html` com o navegador (Chrome, Firefox, Edge…).

---

## ✅ 6. OPCIONAL: USAR EXTENSÕES

O módulo `markdown` também suporta **extensões**, como tabelas, código highlight, etc.

```python
html = markdown.markdown(texto_md, extensions=["extra", "codehilite", "tables"])
```

---

## ✅ 7. DICA: Converter Markdown da Web ou de String

```python
texto = "# Exemplo rápido\n\nTexto com *itálico* e **negrito**."
html = markdown.markdown(texto)
print(html)
```
