Os módulos `os` e `pathlib` em **Windows 10** e **Ubuntu Linux**. Esses dois módulos são usados para **interagir com o sistema de ficheiros** (pastas, ficheiros, caminhos, permissões, etc.) em Python.

---

## 📁 1. Módulo `os`

### 📌 O que é?

O módulo `os` fornece funções para **interagir com o sistema operativo**, como:

* Navegar entre diretórios
* Criar/remover pastas
* Verificar existência de ficheiros/pastas
* Executar comandos no sistema

### 🧱 Funções principais do `os`

```python
import os

# Caminho atual
print(os.getcwd())

# Mudar de diretório
os.chdir("C:/Users/Nome" if os.name == "nt" else "/home/usuario")

# Listar conteúdos
print(os.listdir())

# Criar pasta
os.mkdir("nova_pasta")

# Criar árvore de pastas
os.makedirs("pasta1/pasta2/pasta3")

# Apagar pasta (vazia)
os.rmdir("nova_pasta")

# Apagar árvore de pastas
os.removedirs("pasta1/pasta2/pasta3")

# Verifica se existe
print(os.path.exists("ficheiro.txt"))

# Junta caminhos (portável entre SOs)
caminho = os.path.join("pasta", "ficheiro.txt")
print(caminho)
```

> ⚠️ No Windows usa `\` (barra invertida) e no Linux `/' (barra normal), mas `os.path.join()\` trata disso automaticamente.

---

## 📁 2. Módulo `pathlib`

### 📌 O que é?

`pathlib` é um módulo mais moderno (Python 3.4+) que representa caminhos como **objetos**, tornando o código mais limpo e intuitivo.

### 🧱 Funções principais do `pathlib`

```python
from pathlib import Path

# Caminho atual
caminho = Path.cwd()
print(caminho)

# Criar novo caminho
novo = Path("nova_pasta")

# Criar pasta
novo.mkdir(exist_ok=True)

# Criar árvore de pastas
Path("pasta1/pasta2/pasta3").mkdir(parents=True, exist_ok=True)

# Verificar existência
print(novo.exists())

# Listar conteúdos
print(list(caminho.iterdir()))

# Juntar caminhos
ficheiro = novo / "exemplo.txt"
print(ficheiro)

# Criar ficheiro
ficheiro.write_text("Olá mundo!")

# Ler ficheiro
texto = ficheiro.read_text()
print(texto)

# Apagar ficheiro e pasta
ficheiro.unlink()
novo.rmdir()
```

---

## ✅ Exemplo completo usando `os` e `pathlib`

### 🔄 Compatível com Windows 10 e Ubuntu

```python
import os
from pathlib import Path

# 1. Mostrar diretório atual
print("Diretório atual com os:", os.getcwd())
print("Diretório atual com pathlib:", Path.cwd())

# 2. Criar uma nova pasta
pasta = "exemplo_dir"
if not os.path.exists(pasta):
    os.mkdir(pasta)
    print(f"[os] Criada pasta: {pasta}")

pasta_path = Path(pasta)
if not pasta_path.exists():
    pasta_path.mkdir()
    print(f"[pathlib] Criada pasta: {pasta_path}")

# 3. Criar ficheiro dentro da pasta
ficheiro_os = os.path.join(pasta, "teste_os.txt")
with open(ficheiro_os, "w") as f:
    f.write("Texto usando os.\n")
print(f"[os] Criado ficheiro: {ficheiro_os}")

ficheiro_path = pasta_path / "teste_pathlib.txt"
ficheiro_path.write_text("Texto usando pathlib.\n")
print(f"[pathlib] Criado ficheiro: {ficheiro_path}")

# 4. Listar ficheiros na pasta
print("\nConteúdo da pasta (os):", os.listdir(pasta))
print("Conteúdo da pasta (pathlib):", list(pasta_path.iterdir()))

# 5. Limpar (apagar ficheiros e pasta)
os.remove(ficheiro_os)
print(f"[os] Ficheiro apagado: {ficheiro_os}")

ficheiro_path.unlink()
print(f"[pathlib] Ficheiro apagado: {ficheiro_path}")

os.rmdir(pasta)
print(f"[os] Pasta apagada: {pasta}")
```

---

## 💡 Dicas úteis

| Tarefa               | `os`                         | `pathlib`                      |
| -------------------- | ---------------------------- | ------------------------------ |
| Caminho atual        | `os.getcwd()`                | `Path.cwd()`                   |
| Criar pasta          | `os.mkdir("pasta")`          | `Path("pasta").mkdir()`        |
| Verificar existência | `os.path.exists("ficheiro")` | `Path("ficheiro").exists()`    |
| Juntar caminhos      | `os.path.join(a, b)`         | `Path(a) / b`                  |
| Ler ficheiro         | `open("ficheiro").read()`    | `Path("ficheiro").read_text()` |

---

## 🧪 Testar nos dois sistemas

* Em **Windows 10**, execute o script com:

  ```bash
  python nome_do_script.py
  ```

* Em **Ubuntu**, abra o terminal e execute:

  ```bash
  python3 nome_do_script.py
  ```

Ambos os módulos funcionam exatamente da mesma forma em **Windows e Linux**, com `pathlib` sendo preferido por ser mais moderno e seguro.
