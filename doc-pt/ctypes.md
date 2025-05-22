- [voltar](https://github.com/0joseDark/modules/blob/main/README.md)
- O módulo `ctypes` em Python permite chamar funções de bibliotecas partilhadas (DLLs no Windows ou `.so` em Linux), além de manipular estruturas C, ponteiros e tipos de dados nativos de C.

---

## 🔍 O que é o `ctypes`?

O `ctypes` é um **módulo embutido** do Python, ou seja, não é necessário instalar. Ele permite:

* Chamar funções de bibliotecas em C (como `.dll` ou `.so`)
* Trabalhar com tipos de dados C (`int`, `float`, `char`, `struct`, etc.)
* Manipular ponteiros e arrays
* Usar estruturas (`structs`) e unions como em C

---

## 💻 Compatibilidade

| Sistema Operativo | Biblioteca                 | Extensão |
| ----------------- | -------------------------- | -------- |
| Windows 10        | DLL (Dynamic Link Library) | `.dll`   |
| Ubuntu Linux      | Shared Object              | `.so`    |

---

## ✅ Passos Básicos para Usar o `ctypes`

1. **Importar o módulo**: `import ctypes`
2. **Carregar a biblioteca**:

   * `ctypes.CDLL("lib.so")` em Linux
   * `ctypes.WinDLL("lib.dll")` em Windows
3. **Definir os tipos de dados das funções**: Usar `.argtypes` e `.restype`
4. **Chamar a função da biblioteca**
5. **(Opcional)**: Definir estruturas e arrays como em C

---

## 📘 Exemplo Completo: Criar e Usar Biblioteca em C com Python (`ctypes`)

### 🧱 1. Criar uma biblioteca C simples

### ✅ Código em C (`mylib.c`)

```c
// mylib.c
#include <stdio.h>

int soma(int a, int b) {
    return a + b;
}

void ola() {
    printf("Olá de C!\n");
}
```

---

### ⚙️ 2. Compilar a biblioteca

#### 🪟 No **Windows 10** (usando MinGW):

```bash
gcc -shared -o mylib.dll -fPIC mylib.c
```

#### 🐧 No **Ubuntu**:

```bash
gcc -shared -o mylib.so -fPIC mylib.c
```

> ⚠️ Certifique-se de que tem o `gcc` instalado (`sudo apt install build-essential` em Ubuntu)

---

### 🐍 3. Código Python com `ctypes`

```python
import ctypes
import os
import platform

# Detectar sistema operativo
so = platform.system()

# Carregar biblioteca
if so == "Windows":
    lib = ctypes.CDLL(os.path.abspath("mylib.dll"))
else:
    lib = ctypes.CDLL(os.path.abspath("./mylib.so"))

# Definir tipos de argumento e retorno da função soma
lib.soma.argtypes = [ctypes.c_int, ctypes.c_int]
lib.soma.restype = ctypes.c_int

# Chamar função soma
resultado = lib.soma(10, 20)
print(f"Resultado da soma: {resultado}")

# Chamar função ola (não tem retorno nem parâmetros)
lib.ola()
```

---

### 🧪 Saída Esperada

```text
Resultado da soma: 30
Olá de C!
```

---

## 🧠 Notas Importantes

* `ctypes.c_int`, `c_float`, `c_char_p` representam tipos C (`int`, `float`, `char*`)
* `.argtypes` define os tipos dos parâmetros da função
* `.restype` define o tipo de retorno
* Pode-se também definir **estruturas C** com `ctypes.Structure`

---

## 🧱 Exemplo com `struct` em C

### Código C (`mylib_struct.c`)

```c
#include <stdio.h>

typedef struct {
    int x;
    int y;
} Ponto;

int soma_ponto(Ponto p) {
    return p.x + p.y;
}
```

Compile:

```bash
gcc -shared -o mylib_struct.so -fPIC mylib_struct.c   # Linux
gcc -shared -o mylib_struct.dll -fPIC mylib_struct.c  # Windows
```

### Código Python:

```python
import ctypes
import platform
import os

class Ponto(ctypes.Structure):
    _fields_ = [("x", ctypes.c_int), ("y", ctypes.c_int)]

so = platform.system()
if so == "Windows":
    lib = ctypes.CDLL(os.path.abspath("mylib_struct.dll"))
else:
    lib = ctypes.CDLL(os.path.abspath("./mylib_struct.so"))

lib.soma_ponto.argtypes = [Ponto]
lib.soma_ponto.restype = ctypes.c_int

p = Ponto(3, 7)
resultado = lib.soma_ponto(p)
print("Resultado:", resultado)
```

---

## ✅ Resumo dos Tipos `ctypes`

| Python         | C                |
| -------------- | ---------------- |
| `c_int`        | `int`            |
| `c_float`      | `float`          |
| `c_double`     | `double`         |
| `c_char`       | `char`           |
| `c_char_p`     | `char*` (string) |
| `Structure`    | `struct`         |
| `POINTER(...)` | ponteiro para... |

---

