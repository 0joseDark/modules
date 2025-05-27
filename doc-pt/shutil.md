O módulo `shutil` (shell utilities) da biblioteca padrão do Python fornece várias funções para copiar, mover, remover ficheiros e diretórios, e até criar backups. Ele funciona da mesma forma no **Windows 10** e no **Ubuntu Linux**, já que é um módulo multiplataforma.

---

## ✅ O que o `shutil` pode fazer

| Função                    | O que faz                                               |
| ------------------------- | ------------------------------------------------------- |
| `shutil.copy()`           | Copia um ficheiro (sem as permissões)                   |
| `shutil.copy2()`          | Copia um ficheiro (com metadados, como hora de criação) |
| `shutil.copytree()`       | Copia diretório e todo o conteúdo recursivamente        |
| `shutil.move()`           | Move ficheiro ou diretório                              |
| `shutil.rmtree()`         | Remove diretório com todo o conteúdo                    |
| `shutil.make_archive()`   | Cria um ficheiro ZIP ou tar                             |
| `shutil.unpack_archive()` | Extrai arquivos ZIP, tar, etc.                          |
| `shutil.disk_usage()`     | Mostra uso do disco: total, usado, livre                |

---

## 🧪 Exemplo Completo — Copiar, Mover, Apagar e Criar Arquivo ZIP

### Estrutura antes do script:

```
projeto/
├── origem/
│   ├── ficheiro1.txt
│   └── subpasta/
│       └── ficheiro2.txt
└── destino/
```

### 📄 Código comentado passo a passo

```python
import shutil
import os

# 1. Verifica o sistema operativo
import platform
print("Sistema operativo:", platform.system())

# 2. Caminhos (use caminhos absolutos se preferir)
pasta_origem = "origem"
pasta_destino = "destino"
ficheiro = os.path.join(pasta_origem, "ficheiro1.txt")
novo_ficheiro = os.path.join(pasta_destino, "ficheiro1_copiado.txt")

# 3. Copiar ficheiro
print("\n[COPIAR] ficheiro1.txt para destino/")
shutil.copy(ficheiro, novo_ficheiro)

# 4. Copiar pasta inteira (recursivamente)
print("[COPIAR] pasta origem/ para destino/copia_origem/")
shutil.copytree(pasta_origem, os.path.join(pasta_destino, "copia_origem"), dirs_exist_ok=True)

# 5. Mover ficheiro
print("[MOVER] ficheiro1_copiado.txt para destino/movido.txt")
shutil.move(novo_ficheiro, os.path.join(pasta_destino, "movido.txt"))

# 6. Apagar diretório
print("[APAGAR] destino/copia_origem/")
shutil.rmtree(os.path.join(pasta_destino, "copia_origem"))

# 7. Criar um ZIP da pasta origem
print("[ZIPAR] pasta origem/ para origem_backup.zip")
shutil.make_archive("origem_backup", 'zip', pasta_origem)

# 8. Extrair ZIP para destino/
print("[DESZIPAR] origem_backup.zip para destino/")
shutil.unpack_archive("origem_backup.zip", extract_dir=pasta_destino)

# 9. Ver uso do disco
uso = shutil.disk_usage("/")
print(f"\n[DISCO] Total: {uso.total // (1024**3)} GB | Usado: {uso.used // (1024**3)} GB | Livre: {uso.free // (1024**3)} GB")
```

---

## 📌 Notas importantes

* No **Windows**, os caminhos podem conter barras invertidas (`\\`) ou normais (`/`). O `os.path.join()` cuida disso automaticamente.
* Em **Ubuntu/Linux**, os caminhos usam `/` e permissões de ficheiro podem ser mais restritas.
* `shutil.copytree(..., dirs_exist_ok=True)` só está disponível no Python 3.8+.
* `shutil.rmtree()` deve ser usado com cuidado — ele **apaga tudo recursivamente**.

---

## 📂 Como testar

1. Crie uma pasta chamada `projeto/`.
2. Dentro dela, crie:

   * `origem/`
   * `origem/ficheiro1.txt` com algum texto.
   * `origem/subpasta/ficheiro2.txt` com outro texto.
   * `destino/` vazia.
3. Coloque o script Python dentro de `projeto/` e execute-o.
