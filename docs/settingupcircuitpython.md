# Setting up build Enviroment to work with Raspberry pi pico

## Download firmware

First thing to do before we start prototyping on our pico board is to upload a suitable firmware onto the board. At the time of writing this tutorial, there are two variations of python available to download with arduino support coming soon. We will be focusing on Ciruitpython firmware and link to it is as follows.

* **Circuitpython** - [Download](https://circuitpython.org/board/raspberry_pi_pico/){target=_blank}

!!! info
    Link points to the page to download the latest firmware.

## Download software

* **Code with Mu**: preffered IDE to be used with Micropython/Circuitpython firmware.

    download from the latest version from [here](https://codewith.mu/en/download).


!!! note
    Even though using an IDE is highly recommended, It is not strictly required. We can use any basic text editor to write our code. More information below on limitations of using a basic text editor.

## Installing firmware

* **hardware required**

| Item                              | Quantity                          |
| --------------------------------- | --------------------------------: |
| **`Raspberry pi pico`**           |  1                                |
| **`Micro USB cable`**             |  1                                |
<hr>

* **Step 1:**
    
    * Press and hold BOOTSEL button on the raspberry pi pico and Connect it to your pc/laptop using the supplied microUSB cable.

        ![Connect microusb to pico](installingfirmware/connectpico.png)
        <hr/>
        ![Connect usb to pc](installingfirmware/connectpc.png)
        <hr/>

    * Release the BOOTSEL button. After that, it'll show-up as a removable disk drive with the name `RPI-RP2`.

        ![disk drive](installingfirmware/firstboot.png){: style="width:300px"}

        !!! bug
            Even thought the drive shows 127 MB of total usable storage, Raspberry pi pico only sports 2 MB of internal storage. and while using Circuitpython firmware, only about 0.98 MB is available to users.

        <hr/>

* **Step 2:**
    
    * Copy the `*.uf2` firmware file downloaded [above](./#firmware) to the `RPI-RP2` drive by either dragging and dropping the file or by right-clicking the file and copying it to the drive. 
    
        ![copy from](installingfirmware/copyfrom.png){: style="height:350px"}
        ![copy to](installingfirmware/copyto.png){: style="height:350px"}
        <hr/>

    * After the firmware is copied, pico will restart by itself and it's now ready for programming.

        ![circuitpython drive](installingfirmware/circuitpy.png){: style="width:300px"}
        <hr/>
        
    * Following is the file structure of the circuitpython firmware.

        ![circuitpython contents](installingfirmware/contents.png)
        <hr/>
    



## Installing mu editor

* **Step 1:**

    * Double click `Mu-Editor-Win64-*.exe` downloaded from [above](./#download-software). You'll be presented with the following window.

        ![Installing Mu](installingmu/installingmu1.PNG)
        <hr/>

* **Step 2:**

    * Click on `I accept` check box and then click on `Install`.
    <hr/>

* **Step 3:**

    * After the installer is done installing the software, You'll be presented with the following window. Click on `Finish`.

        ![finish installing mu](installingmu/installingmu2.PNG)
        <hr/>

## Code with Mu First run.

* **Step 1:**

    * Open `Mu editor` from the the start menu.

        ![open from start menu](installingmu/openmu.PNG)
    <hr/>

* **Step 2:**

    * During the first run, We are presented with the following choice.
        
        ![select cpy](installingmu/setupcpy.PNG)
        <hr/>

    * Go ahead and select `circuitpython` option then click on `OK`.
    <hr/>


* **Step 3:**

    * If pico is already connected to the computer, then Mu will automatically recognize and connect to the board.

        ![select mpy](installingmu/mainwindow.PNG)
        <hr/>

    * Now go ahead and click on load and open `code.py` from pico's drive `CIRCUITPY(x:)`. where `x` stands for the letter assigned to the drive.

<!-- ## limitations of using a basic text editor

    work in progress -->