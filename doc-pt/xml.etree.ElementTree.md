O módulo `xml.etree.ElementTree` em Python é usado para **criar, ler, modificar e gravar ficheiros XML**. Ele está incluído na biblioteca padrão do Python, o que significa que não é necessário instalar nada adicional, tanto no **Windows 10** quanto no **Ubuntu**.

---

## 🔧 Compatibilidade

* **Windows 10**: Funciona com Python instalado do site oficial ([https://www.python.org](https://www.python.org)).
* **Ubuntu Linux**: Funciona com Python instalado por padrão ou com `sudo apt install python3`.

---

## 📚 Passo a passo: Usar `xml.etree.ElementTree`

### 🧩 1. Importar o módulo

```python
import xml.etree.ElementTree as ET
```

---

### 🧩 2. Criar um XML na memória

```python
root = ET.Element("livraria")

livro1 = ET.SubElement(root, "livro", id="1")
ET.SubElement(livro1, "titulo").text = "Python Básico"
ET.SubElement(livro1, "autor").text = "João Silva"
ET.SubElement(livro1, "ano").text = "2023"

livro2 = ET.SubElement(root, "livro", id="2")
ET.SubElement(livro2, "titulo").text = "Aprender XML"
ET.SubElement(livro2, "autor").text = "Maria Sousa"
ET.SubElement(livro2, "ano").text = "2024"
```

---

### 🧩 3. Gravar o XML num ficheiro

```python
tree = ET.ElementTree(root)
with open("livraria.xml", "wb") as ficheiro:
    tree.write(ficheiro, encoding='utf-8', xml_declaration=True)
```

---

### 🧩 4. Ler e mostrar o XML do ficheiro

```python
tree = ET.parse("livraria.xml")
root = tree.getroot()

for livro in root.findall("livro"):
    titulo = livro.find("titulo").text
    autor = livro.find("autor").text
    ano = livro.find("ano").text
    print(f"Título: {titulo}, Autor: {autor}, Ano: {ano}")
```

---

### 🧩 5. Modificar um elemento

```python
for livro in root.findall("livro"):
    if livro.get("id") == "2":
        livro.find("titulo").text = "XML Avançado"

tree.write("livraria_modificada.xml", encoding='utf-8', xml_declaration=True)
```

---

### 🧩 6. Apagar um elemento

```python
for livro in root.findall("livro"):
    if livro.find("autor").text == "João Silva":
        root.remove(livro)

tree.write("livraria_filtrada.xml", encoding='utf-8', xml_declaration=True)
```

---

## 🧪 Ficheiro gerado: `livraria.xml`

```xml
<?xml version='1.0' encoding='utf-8'?>
<livraria>
  <livro id="1">
    <titulo>Python Básico</titulo>
    <autor>João Silva</autor>
    <ano>2023</ano>
  </livro>
  <livro id="2">
    <titulo>Aprender XML</titulo>
    <autor>Maria Sousa</autor>
    <ano>2024</ano>
  </livro>
</livraria>
```

---

## 🖥️ Como executar no Windows 10 ou Ubuntu:

1. Salva o código num ficheiro: `exemplo_xml.py`
2. Abre um terminal (cmd ou PowerShell no Windows, Terminal no Ubuntu)
3. Executa com:

```bash
python exemplo_xml.py
```

> ⚠️ Usa `python3` no Ubuntu se necessário.
