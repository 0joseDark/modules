## ✅ O que é o módulo `json`?

O módulo `json` em Python permite:

* **Ler dados JSON** (JavaScript Object Notation).
* **Escrever dados JSON** para ficheiros ou strings.
* Converter entre **objetos Python** (como dicionários) e **JSON**.

JSON é muito usado em **APIs**, **configurações**, **web services** e **comunicação entre sistemas**.

---

## ✅ Compatibilidade

* O módulo `json` faz parte da **biblioteca padrão do Python**, não precisas de instalar nada extra.
* Funciona **igual** em **Windows 10** e **Ubuntu Linux**.

---

## ✅ Equivalências Python ↔ JSON

| Python          | JSON           |
| --------------- | -------------- |
| `dict`          | objeto         |
| `list`, `tuple` | array          |
| `str`           | string         |
| `int`, `float`  | número         |
| `True`/`False`  | `true`/`false` |
| `None`          | `null`         |

---

## ✅ Exemplo completo: guardar e ler dados JSON

Vamos criar um programa Python que:

1. Cria um dicionário com dados.
2. Guarda os dados num ficheiro `.json`.
3. Lê os dados do ficheiro.
4. Acede aos dados e imprime-os.

---

### 📁 Estrutura de ficheiros

```
projeto_json/
│
├── dados.json        ← ficheiro gerado com os dados
└── exemplo_json.py   ← script Python
```

---

### 🧠 Código explicado: `exemplo_json.py`

```python
import json  # importa o módulo json

# 1. Criar um dicionário com dados
utilizador = {
    "nome": "Ana",
    "idade": 30,
    "email": "ana@example.com",
    "interesses": ["programação", "música", "viagens"],
    "ativo": True
}

# 2. Guardar os dados no ficheiro JSON
with open("dados.json", "w", encoding="utf-8") as ficheiro:
    json.dump(utilizador, ficheiro, ensure_ascii=False, indent=4)
    print("✅ Dados guardados em 'dados.json'")

# 3. Ler os dados de volta
with open("dados.json", "r", encoding="utf-8") as ficheiro:
    dados_lidos = json.load(ficheiro)

# 4. Aceder e imprimir os dados
print("\n🔍 Dados lidos:")
print("Nome:", dados_lidos["nome"])
print("Idade:", dados_lidos["idade"])
print("Email:", dados_lidos["email"])
print("Interesses:", ", ".join(dados_lidos["interesses"]))
print("Está ativo?", "Sim" if dados_lidos["ativo"] else "Não")
```

---

### 🖥️ Como executar no Windows 10 ou Ubuntu

#### No Windows:

1. Abre o **Prompt de Comando**.
2. Navega até à pasta: `cd caminho\para\projeto_json`
3. Executa: `python exemplo_json.py`

#### No Ubuntu:

1. Abre o **Terminal**.
2. Navega até à pasta: `cd /caminho/para/projeto_json`
3. Executa: `python3 exemplo_json.py`

---

### 📝 Conteúdo gerado no ficheiro `dados.json`

```json
{
    "nome": "Ana",
    "idade": 30,
    "email": "ana@example.com",
    "interesses": [
        "programação",
        "música",
        "viagens"
    ],
    "ativo": true
}
```

---

## ✅ Resumo de funções principais

| Função         | Descrição                                   |
| -------------- | ------------------------------------------- |
| `json.dump()`  | Escreve objeto Python num ficheiro JSON     |
| `json.load()`  | Lê JSON de um ficheiro e converte em Python |
| `json.dumps()` | Converte Python em string JSON              |
| `json.loads()` | Converte string JSON em objeto Python       |
