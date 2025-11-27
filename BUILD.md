# Como compilar o firmware (ESP32 - hardware)

Este projeto usa PlatformIO (ambientes definidos no `platformio.ini`). Para gerar o `firmware.bin` compilado para hardware (ESP32 físico), siga estes passos em uma máquina com PlatformIO / ESP-IDF configurado.

Pré-requisitos:
- Instalar Python (3.8+)
- Instalar PlatformIO CLI ou usar a extensão PlatformIO no VS Code
- Ter as ferramentas toolchain do ESP-IDF/PlatformIO

No PowerShell (Windows) ou terminal com PlatformIO disponível:

```powershell
# Entrar na pasta do projeto
cd C:\Users\Aula\Desktop\demo_iot-develop\demo_iot-develop

# Compilar para hardware real (ESP32 físico)
pio run -e esp32-hardware

# O binário final normalmente ficará em:
.pio\build\esp32-hardware\firmware.bin

# Para gravar no ESP32 (exemplo COM4):
pio run -e esp32-hardware -t upload

# Para conexão serial monitor:
pio device monitor -e esp32-hardware
```

Observações importantes:
- O projeto tem um ambiente `esp32-qemu` para emulação, mas o usuário pediu compilação para hardware — use `esp32-hardware`.
- As configurações WiFi e MQTT padrão estão em `src/services/mqtt_system.h` (CONFIG_WIFI_SSID, CONFIG_WIFI_PASSWORD, CONFIG_MQTT_BROKER_URI). As opções padrão já foram ajustadas para:
  - SSID: "iot"
  - PASSWORD: "123mudar"
  - BROKER: mqtt://192.168.0.1:1883

Se precisar, posso gerar um passo a passo (screenshots/comandos) para configurar a toolchain no seu computador.

CI / Build automático no GitHub
---------------------------------

Se preferir não configurar o toolchain localmente, você pode usar o workflow GitHub Actions incluído neste repositório. Após criar o repositório no GitHub e enviar (push) o código para a branch principal, o Actions irá executar a build e gerar um artefato chamado `firmware-esp32` contendo `firmware.bin` (procure na página do run do workflow -> Artifacts).

1. Confirme que o repositório contém este código.
2. Faça push para a branch `main` ou `master`.
3. Vá em Actions -> selecione a execução -> baixe o artefato `firmware-esp32`.

