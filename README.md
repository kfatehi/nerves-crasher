# Crasher

This is an example Nerves application that crashes immediately in order to demonstrate the erlinit hanging configuration.

Here's what happens if you watch the bootup sequence with your serial monitor.

**Goal: control if we are to hang or auto-restart, as an application developer. Either implicitly via dev/prod distinction or explicitly in a config somewhere -- thoughts?**

```
synapse:Workspace keyvan$ miniterm.py /dev/cu.usbserial-AFYS0X3Z 115200
--- Miniterm on /dev/cu.usbserial-AFYS0X3Z: 115200,8,N,1 ---
--- Quit: Ctrl+]  |  Menu: Ctrl+T | Help: Ctrl+T followed by Ctrl+H ---

U-Boot SPL 2015.07 (Jan 07 2016 - 17:35:06)
reading args
spl_load_image_fat_os: error reading image args, err - -1
reading u-boot.img
reading u-boot.img


U-Boot 2015.07 (Jan 07 2016 - 17:35:06 -0500)

       Watchdog enabled
I2C:   ready
DRAM:  512 MiB
NAND:  0 MiB
MMC:   OMAP SD/MMC: 0, OMAP SD/MMC: 1
*** Error - No Valid Environment Area found
*** Warning - bad CRC, using default environment

Net:   <ethaddr> not set. Validating first E-fuse MAC
cpsw, usb_ether

switch to partitions #0, OK
mmc0 is current device
SD/MMC found on device 0
reading boot.scr
1857 bytes read in 6 ms (301.8 KiB/s)
Running bootscript from mmc0 ...
## Executing script at 82000000
Running Nerves U-Boot script
reading uEnv.txt
** Unable to read file uEnv.txt **
reading zImage
1984840 bytes read in 117 ms (16.2 MiB/s)
reading am335x-boneblack.dtb
26098 bytes read in 10 ms (2.5 MiB/s)
Kernel image @ 0x82000000 [ 0x000000 - 0x1e4948 ]
## Flattened Device Tree blob at 88000000
   Booting using the fdt blob at 0x88000000
   Loading Device Tree to 8fff6000, end 8ffff5f1 ... OK

Starting kernel ...

Uncompressing Linux... done, booting the kernel.
omap2_mbox_probe: platform not supported
bone-capemgr bone_capemgr.9: slot #0: No cape found
bone-capemgr bone_capemgr.9: slot #1: No cape found
bone-capemgr bone_capemgr.9: slot #2: No cape found
bone-capemgr bone_capemgr.9: slot #3: No cape found
omap_hsmmc mmc.5: of_parse_phandle_with_args of 'reset' failed
pinctrl-single 44e10800.pinmux: pin 44e10854 already requested by 44e10800.pinmux; cannot claim for gpio-leds.8
pinctrl-single 44e10800.pinmux: pin-21 (gpio-leds.8) status -22
pinctrl-single 44e10800.pinmux: could not request pin 21 on device pinctrl-single
Erlang/OTP 18 [erts-7.1] [source] [async-threads:10] [kernel-poll:false]

{"Kernel pid terminated",application_controller,"{application_start_failure,crasher,{{shutdown,{failed_to_start_child,'Elixir.Crasher.Worker',{'EXIT',{undef,[{'Elixir.Crasher.Worker',start_link,[<<\"i\">>,<<\"will\">>,<<\"crash\">>],[]},{supervisor,do_start_child,2,[{fi
le,\"supervisor.erl\"},{line,343}]},{supervisor,start_children,3,[{file,\"supervisor.erl\"},{line,326}]},{supervisor,init_children,2,[{file,\"supervisor.erl\"},{line,292}]},{gen_server,init_it,6,[{file,\"gen_server.erl\"},{line,328}]},{proc_lib,init_p_do_apply,3,[{file,
\"proc_lib.erl\"},{line,240}]}]}}}},{'Elixir.Crasher',start,[normal,[]]}}}"}

Crash dump is being written to: erl_crash.dump...Kernel pid terminated (application_controller) ({application_start_failure,crasher,{{shutdown,{failed_to_start_child,'Elixir.Crasher.Worker',{'EXIT',{undef,[{'Elixir.Crasher.Worker',start_link,[<<"i
erlinit: Sending SIGTERM to all processes
erlinit: Sending SIGKILL to all processes


FATAL ERROR:
erlinit: Hanging as requested by the erlinit configuration...

CANNOT CONTINUE.
```
