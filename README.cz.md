# Vývoj aplikací pro Raspberry Pi Pico W, MicroPython
- Operační systém Windows 11
- Je potřeba mít nainstalovaný vývojový program VS Code
- Na Raspberry Pi Pico W nahraný správný firmware

## Instalace a nastavení WSL
1. Povolení WSL2 ve windows <br />
    - [Povolení susystému pro linux](https://www.makeuseof.com/enable-windows-subsystem-for-linux/) <br />
    - [Odkaz na nastavení](https://learn.microsoft.com/en-us/windows/wsl/install)
   
2. Nastavení verze WSL 2 - 
   <span style="color:yellow">Windows konzole</span> <br />
   ```wsl --set-default-version 2```

3. Instalace distribuce Ubuntu - 
   <span style="color:yellow">Windows konzole</span> <br />
   ```wsl --install -d Ubuntu```

4. Aktualizace závislostí a upgrade systému - 
   <span style="color:yellow">WSL konzole</span><br />
   ```sudo apt update -y && sudo apt upgrade -y```

5. Otevřít adresář, který chci namountovat -
   <span style="color:yellow">WSL konzole</span><br />
   ```cd /mnt/c/Users/David/Desktop/RPIPico```

6. Napojím VSCode do této složky -
   <span style="color:yellow">WSL konzole</span><br />
   ```code .```

## Instalace nástrojů pro připojení USB zařízení

7. Stáhnu poslední verzi usbipd (aktuálně 2.4.1)
   - [Odkaz na releases](https://github.com/dorssel/usbipd-win/releases)
   - Soubor .msi a nainstaluji do windows
   
8. Doinstaluji potřebné tools k propojení s windows -
   <span style="color:yellow">WSL konzole</span><br />
   ```
   sudo apt install linux-tools-generic hwdata
   sudo update-alternatives --install /usr/local/bin/usbip usbip /usr/lib/linux-tools/*-generic/usbip 20
   ```

9.  Připojím desku do USB
    
10. Zobrazení připojených zařízení -
    <span style="color:yellow">Windows konzole</span><br />
    ```usbipd wsl list```

11. Připojím USB zařízení do WSL -
    <span style="color:red">Admin</span>
    <span style="color:yellow">windows konzole</span><br />
    ```usbipd wsl attach --busid 6-1```

12. Uvnitř WSL vypíšu připojená zařízení -
    <span style="color:yellow">WSL konzole</span><br />
    ```lsusb```

## Příprava a nahrání projektu do desky

13. Najdu složku, kterou chci otevřít ve VS code připojenou do WLS -
    <span style="color:yellow">WSL konzole</span><br />
    ```code .```

14. Python je již předinstalován, ale je potřeba doinstalovat pip -
    <span style="color:yellow">WSL konzole</span><br />
    ```sudo apt install python3-pip```

15. Doinstaluji potřebný balíček pyserial pro python -
    <span style="color:yellow">WSL konzole</span><br />
    ```pip install pyserial```

16. Nainstaluji doplňky do VS code pro Raspberry Pi Pico W -
    <span style="color:orange">VS code</span><br />
    - Pico-W-Go
    - Python
    - Pylance
    - IntelliCode

17.  Předkonfiguruji projekt -
    <span style="color:orange">VS code</span><br />
    - CTRL + L SHIFT + P -> Pico-W-Go > Configure project

18. Otevřu konzoli vREPL pro desku -
    <span style="color:orange">VS code</span><br />
    - kliknutím na + nová konzole a zvolím vREPL, tím jsem otevřek konzoli desky

19. Zobrazím virtuální file system desky, abych viděl soubory nahrané v desce
    - Pico-W-Go > Toggle Virtual File System (closes existing vREPLs)

20. Naprodgramuji script ```script.py``` u sebe v adresáři -
    <span style="color:orange">VS code</span><br />
    ```
    from machine import Pin
    from time import sleep

    led = Pin("LED", Pin.OUT)

    led.on()
    sleep(1)
    led.off()
    ```

21. Program přetáhnu do remote adresáře desky a spustím -
    <span style="color:orange">VS code</span><br />
    Pico-W-Go > Remote > Run current file

22. Happy Coding