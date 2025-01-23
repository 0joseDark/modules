 - [English](https://github.com/0joseDark/modules/blob/main/doc-en/English-README.md)

 - [doc pt modules](https://github.com/0joseDark/modules/tree/main/doc-pt)

 - [linux ubuntu](https://github.com/0joseDark/modules/blob/main/doc-pt/linux-README.md)

Aqui está uma lista de **módulos Python organizados por classes de funcionalidade** com foco em uso no **Windows 10**.
---

## **1. Interface Gráfica**
- **tkinter**: Biblioteca padrão para criar interfaces gráficas.
- **PyQt5 / PySide2**: Frameworks poderosos para GUIs baseados em Qt.
- **Kivy**: Para criar aplicativos móveis e de desktop multiplataforma.
- **wxPython**: Biblioteca para GUIs nativas.
- **DearPyGui**: Interface gráfica moderna com suporte a DirectX.

---

## **2. Interação com Hardware**
### **Câmaras e Dispositivos USB** [libusb.org.](https://libusb.info/). [fazer módulo usb](https://github.com/0joseDark/modules/blob/main/make-module-USB.md). [Extensões em C/C++](https://github.com/0joseDark/my-python-book/blob/main/doc-pt/Extensoes-C.md)
- **usbinfo**: Fornece informações detalhadas sobre dispositivos USB conectados.
- **hid**: Focado em dispositivos HID (Human Interface Devices), como teclados, ratos e controladores de jogo.
- **pyserial**: Usado para comunicação com dispositivos USB que emulam portas seriais (ex.: Arduino).
- **libusb**: Biblioteca de baixo nível para comunicação direta com dispositivos USB. O Python pode usar esta biblioteca via pyusb.
- **win32com**: Utilizado no Windows para interagir com dispositivos e componentes do sistema (ex.: dispositivos conectados via COM).
- **subprocess**: Permite executar comandos do sistema para listar dispositivos USB (ex.: no Linux ou Windows).
- **ctypes**: Permite a interação com bibliotecas C para acessar funcionalidades de baixo nível, como USB.
- **platform**: Identifica o sistema operacional e arquitetura, útil para adaptar scripts USB conforme o ambiente.
- **pyusb**: Comunicação com dispositivos USB.
- **opencv-python (cv2)**: Trabalho com câmeras e processamento de imagens.
  
### **Teclado e Rato**
- **pynput**: Controle e monitoramento de teclado e mouse.
- **keyboard**: Manipulação de eventos de teclado.
- **mouse**: Controle e monitoramento de mouse.

### **Som**
- **pyaudio**: Gravação e reprodução de som.
- **sounddevice**: Alternativa moderna ao `pyaudio`.
- **wave**: Biblioteca padrão para manipular arquivos `.wav`.
- **pygame.mixer**: Módulo de som para jogos.
- **pyalsaaudio**: Áudio no ALSA (Linux, mas adaptável).

---

## **3. Rede e Comunicação**
- **socket**: Biblioteca padrão para comunicação de rede.
- **requests**: Para realizar requisições HTTP.
- **flask**: Framework para criar servidores web.
- **fastapi**: Framework moderno para APIs.
- **paramiko**: Para SSH e SFTP.
- **scapy**: Análise e manipulação de pacotes de rede.

---

## **4. Manipulação de Ficheiros**
- **os / pathlib**: Manipulação de caminhos e diretórios.
- **shutil**: Operações de alto nível com arquivos e diretórios.
- **xml.etree.ElementTree**: Manipulação de arquivos XML.
- **json**: Manipulação de arquivos JSON.
- **PyPDF2**: Manipulação de PDFs.
- **markdown**: Conversão de arquivos para Markdown.

---

## **5. Processamento de Imagem e Vídeo**
- **Pillow (PIL)**: Manipulação de imagens.
- **opencv-python (cv2)**: Processamento de imagem e vídeo.
- **ffmpeg-python**: Conversão e manipulação de vídeos.
- **imageio**: Leitura e escrita de imagens e vídeos.

---

## **6. Automação e Utilitários**
- **pyautogui**: Automação de teclado, mouse e GUI.
- **win32api / pywin32**: Para interagir com recursos específicos do Windows.
- **schedule**: Automação de tarefas agendadas.
- **subprocess**: Execução de comandos no sistema operacional.
- **pyinstaller**: Empacotamento de scripts Python em executáveis.

---

## **7. Jogos e Simulações**
- **pygame**: Desenvolvimento de jogos 2D.
- **pyglet**: Simulações e jogos 2D/3D leves.
- **arcade**: Biblioteca moderna para jogos 2D.

---

## **8. Ciência de Dados e IA**
- **numpy**: Cálculos numéricos.
- **pandas**: Manipulação e análise de dados.
- **matplotlib**: Criação de gráficos.
- **scikit-learn**: Algoritmos de aprendizado de máquina.
- **tensorflow / pytorch**: Redes neurais e aprendizado profundo.
- **opencv**: Visão computacional.

---

## **9. Segurança e Criptografia**
- **cryptography**: Para criptografia e segurança.
- **pycryptodome**: Manipulação de algoritmos criptográficos.
- **hashlib**: Geração de hashes (MD5, SHA).

---
