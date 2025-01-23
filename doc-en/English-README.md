# Modules
[Linux Ubuntu](https://github.com/0joseDark/modules/blob/main/doc-en/linux.md)

Here is a list of **Python modules organized by functionality classes** with a focus on use in **Windows 10**.
---

## **1. Graphical User Interface**
- **tkinter**: Standard library for creating graphical interfaces.
- **PyQt5 / PySide2**: Powerful frameworks for Qt-based GUIs.
- **Kivy**: For creating cross-platform desktop and mobile applications.
- **wxPython**: Library for native GUIs.
- **DearPyGui**: Modern graphical interface with DirectX support.

---

## **2. Hardware Interaction**
### **Cameras and USB Devices** [libusb.org.](https://libusb.info/). [Create USB module](https://github.com/0joseDark/modules/blob/main/doc-en/USB%20Devices.md). [C/C++ Extensions](https://github.com/0joseDark/modules/blob/main/doc-en/Extensions-C.md)
- **usbinfo**: Provides detailed information about connected USB devices.
- **hid**: Focused on HID (Human Interface Devices), such as keyboards, mice, and game controllers.
- **pyserial**: Used for communication with USB devices that emulate serial ports (e.g., Arduino).
- **libusb**: Low-level library for direct communication with USB devices. Python can use this library via pyusb.
- **win32com**: Used on Windows to interact with system devices and components (e.g., devices connected via COM).
- **subprocess**: Allows executing system commands to list USB devices (e.g., on Linux or Windows).
- **ctypes**: Enables interaction with C libraries to access low-level functionalities like USB.
- **platform**: Identifies the operating system and architecture, useful for adapting USB scripts to the environment.
- **pyusb**: Communication with USB devices.
- **opencv-python (cv2)**: Working with cameras and image processing.

### **Keyboard and Mouse**
- **pynput**: Control and monitoring of keyboard and mouse.
- **keyboard**: Keyboard event handling.
- **mouse**: Control and monitoring of mouse.

### **Sound**
- **pyaudio**: Sound recording and playback.
- **sounddevice**: Modern alternative to `pyaudio`.
- **wave**: Standard library for handling `.wav` files.
- **pygame.mixer**: Sound module for games.
- **pyalsaaudio**: Sound on ALSA (Linux, but adaptable).

---

## **3. Networking and Communication**
- **socket**: Standard library for network communication.
- **requests**: To perform HTTP requests.
- **flask**: Framework for creating web servers.
- **fastapi**: Modern framework for APIs.
- **paramiko**: For SSH and SFTP.
- **scapy**: Network packet analysis and manipulation.

---

## **4. File Handling**
- **os / pathlib**: Path and directory handling.
- **shutil**: High-level operations with files and directories.
- **xml.etree.ElementTree**: XML file handling.
- **json**: JSON file handling.
- **PyPDF2**: PDF file handling.
- **markdown**: Conversion of files to Markdown.

---

## **5. Image and Video Processing**
- **Pillow (PIL)**: Image manipulation.
- **opencv-python (cv2)**: Image and video processing.
- **ffmpeg-python**: Video conversion and manipulation.
- **imageio**: Reading and writing of images and videos.

---

## **6. Automation and Utilities**
- **pyautogui**: Automation of keyboard, mouse, and GUI.
- **win32api / pywin32**: To interact with Windows-specific resources.
- **schedule**: Automation of scheduled tasks.
- **subprocess**: Execution of operating system commands.
- **pyinstaller**: Packaging Python scripts into executables.

---

## **7. Games and Simulations**
- **pygame**: Development of 2D games.
- **pyglet**: Lightweight 2D/3D simulations and games.
- **arcade**: Modern library for 2D games.

---

## **8. Data Science and AI**
- **numpy**: Numerical calculations.
- **pandas**: Data manipulation and analysis.
- **matplotlib**: Graph creation.
- **scikit-learn**: Machine learning algorithms.
- **tensorflow / pytorch**: Neural networks and deep learning.
- **opencv**: Computer vision.

---

## **9. Security and Cryptography**
- **cryptography**: For encryption and security.
- **pycryptodome**: Handling cryptographic algorithms.
- **hashlib**: Generating hashes (MD5, SHA).
