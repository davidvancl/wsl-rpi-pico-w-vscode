# Developing applications for Raspberry Pi Pico W, MicroPython
- Operating system Windows 11
- VS Code development program needs to be installed
- Correct firmware needs to be loaded onto the Raspberry Pi Pico W

## Installing and setting up WSL
1. Enable WSL2 on Windows <br />
    - [Enable Windows Subsystem for Linux](https://www.makeuseof.com/enable-windows-subsystem-for-linux/) <br />
    - [Link to Settings](https://learn.microsoft.com/en-us/windows/wsl/install)
   
2. Set WSL 2 as the default version - 
   <span style="color:yellow">Windows console</span> <br />
   ```wsl --set-default-version 2```

3. Install Ubuntu distribution - 
   <span style="color:yellow">Windows console</span> <br />
   ```wsl --install -d Ubuntu```

4. Update dependencies and upgrade the system - 
   <span style="color:yellow">WSL console</span><br />
   ```sudo apt update -y && sudo apt upgrade -y```

5. Open the directory I want to mount -
   <span style="color:yellow">WSL console</span><br />
   ```cd /mnt/c/Users/David/Desktop/RPIPico```

6. Attach VSCode to this folder -
   <span style="color:yellow">WSL console</span><br />
   ```code .```

## Installing tools for connecting USB devices

7. Download the latest version of usbipd (currently 2.4.1)
   - [Link to releases](https://github.com/dorssel/usbipd-win/releases)
   - Download the .msi file and install it on Windows
   
8. Install necessary tools for connecting to Windows -
   <span style="color:yellow">WSL console</span><br />
   ```
   sudo apt install linux-tools-generic hwdata
   sudo update-alternatives --install /usr/local/bin/usbip usbip /usr/lib/linux-tools/*-generic/usbip 20
   ```

9.  Connect the board to USB
    
10. Display connected devices -
    <span style="color:yellow">Windows console</span><br />
    ```usbipd wsl list```

11. Attach USB device to WSL -
    <span style="color:red">Admin</span>
    <span style="color:yellow">windows console</span><br />
    ```usbipd wsl attach --busid 6-1```

12. Display connected devices inside WSL -
    <span style="color:yellow">WSL console</span><br />
    ```lsusb```

## Preparing and uploading the project to the board

13. Find the directory I want to open in VS code, which is connected to WLS -
    <span style="color:yellow">WSL console</span><br />
    ```code .```

14. Python is already installed, but pip needs to be installed -
    <span style="color:yellow">WSL console</span><br />
    ```sudo apt install python3-pip```

15. Install the necessary pyserial package for Python -
    <span style="color:yellow">WSL console</span><br />
    ```pip install pyserial```

16. Install VS code extensions for Raspberry Pi Pico W -
    <span style="color:orange">VS code</span><br />
    - Pico-W-Go
    - Python
    - Pylance
    - IntelliCode

17. Configure the project -
    <span style="color:orange">VS code</span><br />
    - CTRL + L SHIFT + P -> Pico-W-Go > Configure project

18. Open a console in the REPL for the board -
    <span style="color:orange">VS code</span><br />
    - By clicking on the + New Console and selecting the vREPL, open the console for the board.

19. Display the virtual file system of the board to see the files uploaded to it
    - Pico-W-Go > Toggle Virtual File System (closes existing vREPLs)

20. Create program ```script.py``` in my local directory -
    <span style="color:orange">VS code</span><br />
    ```
    from machine import Pin
    from time import sleep

    led = Pin("LED", Pin.OUT)

    led.on()
    sleep(1)
    led.off()
    ```

21. Drag and drop the program to the remote directory of the board and run it -
    <span style="color:orange">VS code</span><br />
    - Pico-W-Go > Remote > Run current file

22. Happy Coding