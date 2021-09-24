<h1 align="center">
<br>
<img src=image.png >
<br>
Cobalt Strike ⇌ ScareCrow
<br>
CNA Script
</h1>

### 💣 ScareCrow Options
```bash
-I string
    Path to the raw 64-bit shellcode.
-Loader string
    Sets the type of process that will sideload the malicious payload:
    [*] binary - Generates a binary based payload. (This type does not benefit from any sideloading)
    [*] control - Loads a hidden control applet - the process name would be rundll32 if -O is specified. A JScript loader will be generated.
    [*] dll - Generates just a DLL file. Can be executed with commands such as rundll32 or regsvr32 with DllRegisterServer, DllGetClassObject as export functions.
    [*] excel - Loads into a hidden Excel process using a JScript loader.
    [*] msiexec - Loads into MSIexec process using a JScript loader.
    [*] wscript - Loads into WScript process using a JScript loader.
-etw
    Enables ETW patching to prevent ETW events from being generated by the process. ETW utilizes built-in Syscalls to generate this telemetry. Since ETW is a native feature built into Windows, security products do not need to "hook" the ETW syscalls to gain the information. As a result, to prevent ETW, ScareCrow patches numerous ETW syscalls, flushing out the registers and returning the execution flow to the next instruction. 
-sandbox
    Enables sandbox evasion using IsDomainedJoined calls.
-injection string
    Enables Process Injection Mode and specifies the path to the process to create/inject into (use \ for the path).
```
## 📥 Clone the Project
```bash
git clone https://github.com/GeorgePatsias/ScareCrow-CobaltStrike.git
```

## 🏭 Install ScareCrow

Setup ScareCrow [https://github.com/optiv/ScareCrow](https://github.com/optiv/ScareCrow) just by running the `install.sh` script.
```bash
chmod +x install.sh
./install.sh
```

## 🔧 Setup CNA Script Configurations

Edit the ScareCrow.cna and replace the variables below accordingly. **NOTE!** Do not add the final **/** at the end of the paths!
```
#Path to the ScareCrow-CobaltStrike repository you just cloned.
$script_path = "/home/user/ScareCrow-CobaltStrike";

#Path to the compiled ScareCrow Go executable of the installation.
$scarecrow_executable = "/home/user/ScareCrow-CobaltStrike/ScareCrow/ScareCrow";

#Path to the CobaltStrike directory.
$cs_directory = "/home/user/cobaltstrike";

#Path to the python3 binary.
$python3 = "/usr/bin/python3";
```

## 💀 Add the CNA script to Cobalt Strike
`Cobalt Strike > Script Manager > Load > Select ScareCrow.cna`

You will see the new menu item called **ScareCrow** on the top menu of Cobalt Strike.

## References
[https://github.com/optiv/ScareCrow](https://github.com/optiv/ScareCrow)

### Side note
* Run DLLs as following and slightly change the name of the exported DLL <br> `rundll32 example.dll,DllRegisterServer` <br> `rundll32 example.dll,DllGetClassObject`
* Process Injection field must be defined with a single `\` e.g `C:\Windows\System32\notepad.exe`
