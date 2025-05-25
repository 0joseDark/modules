O módulo `platform` do Python fornece uma maneira **portátil de obter informações sobre o sistema operativo, o hardware e o interpretador de Python em uso**, sem depender de comandos externos como `uname` (Linux) ou `systeminfo` (Windows).

---

## ✅ Onde funciona?

* **Windows 10:** funciona perfeitamente e retorna detalhes do sistema operativo da Microsoft.
* **Ubuntu Linux:** também funciona e pode retornar informações detalhadas do kernel e da distribuição.

---

## 🧠 Para que serve o `platform`?

Este módulo é útil, por exemplo, para:

* Fazer scripts compatíveis com diferentes sistemas operativos.
* Exibir informações de diagnóstico.
* Adicionar detalhes técnicos a um log ou relatório.
* Executar comportamentos diferentes dependendo da plataforma.

---

## 📦 Instalação

O módulo `platform` já vem com o Python (é da biblioteca padrão). Não precisa instalar nada.

---

## 📘 Funções principais de `platform`

| Função                      | Descrição                                              |
| --------------------------- | ------------------------------------------------------ |
| `platform.system()`         | Nome do sistema operativo (ex: 'Windows', 'Linux')     |
| `platform.release()`        | Versão do sistema operativo (ex: '10' ou '22.04')      |
| `platform.version()`        | Detalhes da versão do sistema                          |
| `platform.platform()`       | Informações combinadas sobre o sistema                 |
| `platform.machine()`        | Tipo de máquina (ex: 'x86\_64')                        |
| `platform.processor()`      | Tipo de processador (ex: 'Intel64 Family 6 Model 142') |
| `platform.architecture()`   | Arquitetura (ex: ('64bit', 'WindowsPE'))               |
| `platform.node()`           | Nome da máquina (hostname)                             |
| `platform.python_version()` | Versão do Python em uso                                |
| `platform.uname()`          | Retorna tudo acima junto, como uma namedtuple          |

---

## 🧪 Exemplo Completo em Python

Este exemplo funciona igual no **Windows 10** e no **Ubuntu Linux**:

```python
import platform

print("=== INFORMAÇÕES DO SISTEMA ===")
print(f"Nome do sistema: {platform.system()}")
print(f"Versão do sistema: {platform.version()}")
print(f"Lançamento do sistema: {platform.release()}")
print(f"Nome da máquina (node): {platform.node()}")
print(f"Arquitetura: {platform.architecture()}")
print(f"Tipo de máquina: {platform.machine()}")
print(f"Processador: {platform.processor()}")
print(f"Plataforma completa: {platform.platform()}")
print(f"Versão do Python: {platform.python_version()}")

print("\n=== INFORMAÇÕES COMBINADAS (uname) ===")
uname = platform.uname()
print(f"Sistema: {uname.system}")
print(f"Node: {uname.node}")
print(f"Release: {uname.release}")
print(f"Version: {uname.version}")
print(f"Machine: {uname.machine}")
print(f"Processor: {uname.processor}")
```

---

## 🖥️ Saída típica no **Windows 10**

```
=== INFORMAÇÕES DO SISTEMA ===
Nome do sistema: Windows
Versão do sistema: 10.0.19044
Lançamento do sistema: 10
Nome da máquina (node): DESKTOP-ABCD123
Arquitetura: ('64bit', 'WindowsPE')
Tipo de máquina: AMD64
Processador: Intel64 Family 6 Model 142 Stepping 10, GenuineIntel
Plataforma completa: Windows-10-10.0.19044-SP0
Versão do Python: 3.10.11

=== INFORMAÇÕES COMBINADAS (uname) ===
Sistema: Windows
Node: DESKTOP-ABCD123
Release: 10
Version: 10.0.19044
Machine: AMD64
Processor: Intel64 Family 6 Model 142 Stepping 10, GenuineIntel
```

---

## 🐧 Saída típica no **Ubuntu Linux**

```
=== INFORMAÇÕES DO SISTEMA ===
Nome do sistema: Linux
Versão do sistema: #42~22.04.1-Ubuntu SMP Fri Jun 2 15:20:56 UTC 2023
Lançamento do sistema: 5.19.0-46-generic
Nome da máquina (node): ubuntu-pc
Arquitetura: ('64bit', '')
Tipo de máquina: x86_64
Processador: x86_64
Plataforma completa: Linux-5.19.0-46-generic-x86_64-with-glibc2.35
Versão do Python: 3.10.12

=== INFORMAÇÕES COMBINADAS (uname) ===
Sistema: Linux
Node: ubuntu-pc
Release: 5.19.0-46-generic
Version: #42~22.04.1-Ubuntu SMP Fri Jun 2 15:20:56 UTC 2023
Machine: x86_64
Processor: x86_64
```

---

## 💡 Dica adicional

Se quiser verificar **em que sistema está a correr** o script e adaptar o comportamento:

```python
import platform

if platform.system() == "Windows":
    print("Executando em Windows")
elif platform.system() == "Linux":
    print("Executando em Linux")
else:
    print("Outro sistema operativo")
```
