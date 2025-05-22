[**voltar**](https://github.com/0joseDark/modules/blob/main/README.md)
---
### 📦 **O que são módulos em Python?**

- Módulos são **ficheiros** (.py) que contêm **funções**, **classes** e **variáveis** que podes reutilizar em vários programas.
- Existem:
   - **Módulos internos (built-in)** → já vêm instalados com o Python.
   - **Módulos externos** → precisas instalar com `pip`.
   - **Módulos criados por ti** → podes escrever os teus próprios.

---

### ✅ **Módulos Internos mais usados**

| Módulo | Função Principal | Exemplo |
|--------|------------------|---------|
| `math` | Operações matemáticas | `math.sqrt(25)` |
| `random` | Geração de números aleatórios | `random.randint(1,10)` |
| `datetime` | Manipulação de datas e horas | `datetime.datetime.now()` |
| `os` | Acesso ao sistema operativo | `os.listdir()` |
| `sys` | Informações e controlo do Python | `sys.exit()` |
| `time` | Tempo e pausas | `time.sleep(2)` |
| `json` | Ler e escrever ficheiros JSON | `json.load()` |
| `re` | Expressões regulares | `re.search()` |
| `sqlite3` | Banco de dados SQLite | `sqlite3.connect()` |

---

### ✅ **Módulos Externos famosos**

| Módulo | Função Principal | Instalação |
|--------|-----------------|------------|
| `numpy` | Cálculo numérico e arrays | `pip install numpy` |
| `pandas` | Análise e tratamento de dados | `pip install pandas` |
| `matplotlib` | Gráficos e visualização | `pip install matplotlib` |
| `flask` | Criar aplicações web | `pip install flask` |
| `requests` | Fazer requisições HTTP | `pip install requests` |
| `opencv-python` | Processamento de imagens e vídeo | `pip install opencv-python` |
| `pyserial` | Comunicação com portas seriais (Arduino) | `pip install pyserial` |
| `tkinter` | Criar interfaces gráficas | (Já vem com o Python) |

---

### ✅ **Explicação básica de como usar**

#### Exemplo com módulo interno:
```python
import math

print("Raiz quadrada de 9 é:", math.sqrt(9))
```

#### Exemplo com módulo externo:
```python
import requests

resposta = requests.get("https://www.google.com")
print("Código de resposta:", resposta.status_code)
```

---

### ✅ **Vantagens de usar módulos**

- Reutilizas código pronto e testado.
- Poupas tempo.
- Organizas melhor o teu programa.
- Permites colaboração entre vários projetos.

---

Se quiseres, posso ainda:
1. Explicar mais categorias (ex: módulos para som, vídeo, robótica, redes, segurança).
2. Fazer um mapa mental dos módulos.
3. Mostrar como criar o **teu próprio módulo**.
