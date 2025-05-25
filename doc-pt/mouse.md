O módulo `mouse` em Python permite capturar eventos do rato (mouse) como movimentos, cliques e rolagem, e também simular ações com o rato. Ele é compatível com **Windows 10** e **Ubuntu Linux**, embora algumas funcionalidades (como simular cliques) possam exigir **privilégios de administrador** (Windows) ou **sudo/root** (Linux).

---

## ✅ Instalação

Antes de usar o módulo `mouse`, instala-se com:

```bash
pip install mouse
```

> No Ubuntu, se surgir erro de permissões, execute com `sudo`:

```bash
sudo pip install mouse
```

---

## 📦 Funcionalidades principais do módulo `mouse`

| Função                       | Descrição                                               |
| ---------------------------- | ------------------------------------------------------- |
| `mouse.move(x, y)`           | Move o cursor do rato para (x, y).                      |
| `mouse.click(button='left')` | Clica com o botão indicado (`left`, `right`, `middle`). |
| `mouse.press(button)`        | Pressiona o botão (sem soltar).                         |
| `mouse.release(button)`      | Solta o botão.                                          |
| `mouse.wheel(delta)`         | Simula rolagem do rato (positivo = para cima).          |
| `mouse.position()`           | Retorna posição atual do cursor.                        |
| `mouse.on_click(callback)`   | Executa `callback` sempre que clicar.                   |
| `mouse.on_move(callback)`    | Executa `callback` ao mover o rato.                     |
| `mouse.record()`             | Grava todos os eventos do rato.                         |
| `mouse.play(events)`         | Reproduz uma lista de eventos gravados.                 |

---

## ⚠️ Permissões

* **Windows 10**: Executa normalmente com Python.
* **Ubuntu**: Para usar eventos globais (como gravar ou clicar), o script precisa ser executado com `sudo`:

  ```bash
  sudo python3 script.py
  ```

---

## 💡 Exemplo completo: gravar e reproduzir movimentos do rato

### Script `rato_gravador.py`:

```python
# rato_gravador.py
import mouse
import time

def main():
    print("=== Gravador de rato ===")
    input("Pressiona ENTER para começar a gravar...")

    print("A gravar... move e clica com o rato. Pressiona botão do meio (scroll) para parar.")
    events = mouse.record(button='middle')  # para gravação quando clicar botão do meio

    print(f"\n{len(events)} eventos gravados.")
    time.sleep(1)

    input("Pressiona ENTER para reproduzir os movimentos...")
    mouse.play(events, speed_factor=1.0)  # speed_factor < 1.0 = mais lento

    print("Reprodução terminada.")

if __name__ == "__main__":
    main()
```

---

## 🧪 Testar

### No **Windows 10**:

* Salva o ficheiro `rato_gravador.py`.
* Corre com:

  ```bash
  python rato_gravador.py
  ```

### No **Ubuntu**:

* Corre com permissões elevadas:

  ```bash
  sudo python3 rato_gravador.py
  ```

---

## 📌 Observações

* A gravação para quando se clica **botão do meio** do rato (scroll).
* A reprodução imita os movimentos e cliques como foram feitos.
* Pode-se gravar esses eventos num ficheiro para uso posterior.

---

## 📁 Extensão: gravar em ficheiro `.log` e ler depois
