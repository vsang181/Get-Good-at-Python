# Scapy Commands

Scapy provides a rich set of commands that allow us to analyse, manipulate, capture, and transmit packets. There are two primary ways to use Scapy:

1. **Interactively**, through the Scapy command-line shell
2. **Programmatically**, by importing Scapy into a Python script

For this learning unit, we will focus on the interactive approach by launching Scapy directly from the terminal using the `scapy` command (or in this case, `./run_scapy`).

When Scapy starts, you may see informational messages indicating missing optional dependencies. These warnings simply mean that certain advanced features will be unavailable, but Scapy’s core functionality will still work.

```
~/scapy % sudo ./run_scapy
INFO: Can't import PyX. Won't be able to use psdump() or pdfdump().
INFO: Can't import python-cryptography v1.7+. Disabled PKI & TLS crypto-related features.
INFO: Can't import python-cryptography v1.7+. Disabled WEP decryption/encryption. (Dot11)
INFO: Can't import python-cryptography v1.7+. Disabled IPsec encryption/authentication.
WARNING: No alternative Python interpreters found ! Using standard Python shell instead.
INFO: Using the default Python shell: History is disabled.
                                      
                     aSPY//YASa       
             apyyyyCY//////////YCa       |
            sY//////YSpcs  scpCY//Pp     | Welcome to Scapy
 ayp ayyyyyyySCP//Pp           syY//C    | Version 2.7.0rc1.dev7
 AYAsAYYYYYYYY///Ps              cY//S   |
         pCCCCY//p          cSSps y//Y   | https://github.com/secdev/scapy
         SPPPP///a          pP///AC//Y   |
              A//A            cyP////C   | Have fun!
              p///Ac            sC///a   |
              P////YCpc           A//A   | Craft packets like I craft my beer.
       scccccp///pSP///p          p//Y   |               -- Jean De Clerck
      sY/////////y  caa           S//P   |
       cayCyayP//Ya              pY/Ya
        sY/PsY////YCc          aC//Yp 
         sc  sccaCY//PCypaapyCP//YSs  
                  spCPY//////YPSps    
                       ccaacs         
                                      
>>> 
```

Once Scapy loads, you are placed into an interactive Python-like shell where Scapy-specific commands are available.

## Common Scapy Commands

Below are several essential commands that help you explore Scapy’s capabilities:

1. `ls()`

Displays all supported protocol layers and fields known to Scapy.

This is useful for discovering which packet types you can craft and inspect.

2. `explore()`

Opens a GUI-style interactive explorer (if supported), displaying all protocol layers and features.

3. `lsc()`

Displays a list of Scapy commands and functions, each with a short description.

This is very helpful for beginners exploring what Scapy can do.

4. `conf`

Shows Scapy’s current configuration settings, such as interface selection, verbosity level, and more.

5. help()``

Provides documentation for a specific Scapy function. For example, to view help for the `sniff()` function:

Example output (truncated):

```
>>> help(sniff)

Help on function sniff in module scapy.sendrecv:

sniff(*args, **kwargs)
    Sniff packets and return a list of packets.
    
    Args:
        count: number of packets to capture. 0 means infinity.
        store: whether to store sniffed packets or discard them
        prn: function to apply to each packet. If something is returned, it
             is displayed.
...
```

This command is extremely useful when learning packet capturing, crafting, or sending with Scapy.
