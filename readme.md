# Awesome Minitel [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of Minitel and Telematic resources

![Minitel Glitches](/minitel.png)

This repository stands here for Minitel enthusiasts who may want to give a
second life to their terminal. See
[Wikipedia](https://en.wikipedia.org/wiki/Minitel) for general information about
Minitel terminal and network.

The Minitel devices were made to work with a French dedicated public network
from the 80s implementing [X.25](https://en.wikipedia.org/wiki/X.25) protocol:
the [Transpac Network](https://fr.wikipedia.org/wiki/Transpac). This network was
also used in professional industry, including for inter-bank transfers,
payments... With the emergence of Internet, the network became unneeded and
obsolete. Its backbone was shut down in 2012, implying the death of the public
Minitel network. Since then, Minitel terminals became pretty much useless: they
were just display terminal with pretty much no compute and very limited RAM.
Hopefully new usages are now possible, thanks to some modifications made to the
original hardware, or with external hardware used to provide content to the
Minitel. Some terminals like Minitel 1B have a serial port at their back that
can be used to display characters on the screen and send keystrokes from the
user to an external device. This is mainly what this repository is about. You
will also find interesting archives and technical documentation.

## Contents

- [Hardware](#hardware)
  - [DIY serial interface](#diy-serial-interface)
  - [Telephonic socket](#telephonic-socket)
  - [Physical Hardware modification](#physical-hardware-modification)
  - [Physical Hardware hacking](#physical-hardware-hacking)
- [Software](#software)
  - [Client side](#client-side)
    - [Firmware for ESP32 using Minitel serial
      port](#firmware-for-esp32-using-minitel-serial-port)
    - [Clients for serial communication from
      computer](#clients-for-serial-communication-from-computer)
    - [Reprogramming](#reprogramming)
  - [Server side](#server-side)
  - [Editors](#editors)
  - [Emulators](#emulators)
  - [Tools](#tools)
- [Resources](#resources)
  - [Official documentation](#official-documentation)
  - [Extra studies and documentation](#extra-studies-and-documentation)
  - [Other resources](#other-resources)
- [Open Minitel Services](#open-minitel-services)

## Hardware

This section is dedicated on the hardware you can connect to a Minitel (serial
port or telephonic port / non-destructive) or the physical hardware
modifications (potentially destructive) you can perform on the terminal.

You have multiple possible approaches:

- Using the Minitel as a display terminal for a computer or small embedded
  computers like Raspberry Pi

- Using the Minitel as a standalone device able to serve local content / VDT
  pages locally hosted thanks to an ESP32 / Arduino board with local storage.

- Using the Minitel as a standalone device able to connect remote content
  providing servers through a classic network, using for example an ESP32 /
  Arduino with a WiFi or Ethernet interface.

- Using the Minitel in its original form, with external devices emulating the
  X.25 Transpac network and providing content with its native protocol.

- Hacking the Minitel as a standalone computer (despite huge hardware
  limitations), rewriting the content of it's embedded microcontroller.

- Using the Minitel as a display, just reusing the screen and replacing/throwing
  away most internal components.

In all those possible hardware modifications, the easiest way to provide content
to the Minitel is to use its serial port at the back (Minitel 1B), called the
*Péri-informatique* port.

### DIY Serial interface

This section provides different ways of using the Péri-informatique Serial
socket of the Minitel, which is able to receive characters / octets to display,
and send keyboard inputs. This is the easiest way to use the Minitel today
since it doesn't require any physical modifications of the terminals. Extra
hardware is required to adapt the signal due to unusual voltage levels (>5V).

- [**Iodeo's ESP32 devboard**](https://hackaday.io/project/180473-minitel-esp32)
  💙 and [specific instructions](https://hackaday.io/project/180473/instructions) -
  The easiest way to use the serial port of a Minitel today. You don't require
  any soldering skill or custom cable, everything is included. This a dedicated
  ESP32 devboard, including a WiFi adapter and a serial port with the voltage
  modification required to support Minitel levels. The ESP32 is powered by the
  Minitel, which is *very* useful. See [software
  section](#firmware-for-esp32-using-minitel-serial-port) for a list of software
  you can run client side on the ESP32.

- [pi0tel](https://github.com/faxm0dem/pi0tel) - 3615 pi0, a Raspberry Pi pi0 or
  pi0-w uHat designed to be plugged on serial interface and self powered by the
  Minitel.

- [Jelora's custom cables (Serial <> RS232 and Serial <>
  USB)](https://www.jelora.fr/post/2020/02/25/Adaptateur-prise-DIN-peri-informatique-Minitel-vers-Serie-RS232-et-Serie-USB.html) -
  You can plug Minitels 1B directly to a computer or a Raspberry Pi, thanks to a
  custom cable you can make with a few electronic components. This one is a bit
  more difficult to build than Pila's build below.

- [**Pila's custom adapter**](https://pila.fr/wordpress/?p=361) 💙 - An
  alternative tutorial to create a custom Serial <> USB cable using a 2N2222A
  transistor, some resistors and a PL2303HX UART <> USB converter (very easy to
  build). (FR)

- [Picotel's modification for Raspberry Pi
  Pico](https://arduino103.blogspot.com/2022/04/minitel-branche-sur-mon-raspberry-pi.html) -
  An alternative setup, but lacking some information about the level shifter.

### Telephonic socket

- [**vdt2bmp**](https://github.com/jfdelnero/minitel/tree/master/VDT2BMP) 💙 -
  Emulate FSK payloads (that the native V.23 modem will be able to decode)
  with a just a soundcard and a home made jack adapter with a resistor.
  Can work with a smartphone. More information on
  [hxc2001's website](http://hxc2001.free.fr/minitel/#modulation) and on
  [museeminitel](https://forum.museeminitel.fr/t/nouvelle-interface-de-connexion-du-minitel-une-simple-carte-son/1393)
  (FR)

### Physical Hardware modification

Another approach could be to modify the terminals directly.

- [High Tech Minitel](https://chapelierfou.org/blog/a-high-tech-minitel.html) -
  A replacement of the Minitel 1B screen and creation of an Arduino based
  generic USB keyboard controller. (EN)
- [64rulez's Minitel2.0](https://github.com/64rulez/minitel2.0) - A replacement
  of Minitel hardware with a Zynq board. (EN)
- [cfp-radio](https://www.cfp-radio.com/realisations/rea48/minitel-01.html) -
  Converting a Minitel to a TV monitor / composite video monitor. (FR)

### Physical Hardware hacking

See the [dedicated software section](#reprogramming) below.


## Software

Once you chose your hardware path, you can chose a way to provide content to
the terminal. This section contains various client and server implementations
that can help using your Minitel.

### Client side

By *client side*, we mean the software running on the Minitel side / next to the
terminal, able to serve content, receive inputs and eventually fetch content
from a remote server (see [server side](#server-side)). Depending on the
additional [hardware](#hardware) you own or hardware modifications you
performed, some clients may or may not be suitable for you.

#### Firmware for ESP32 using Minitel serial port

Those projects are dedicated to people using the serial port of their Minitel
with an ESP32 microcontroller. See the [hardware section
(DIY)](#diy-serial-interface) above for more information about the required
hardware (ESP32 devboard or a custom cable with a bare ESP32).

- [**iodeo/Minitel-ESP32**](https://github.com/iodeo/Minitel-ESP32) 💙 - Iodeo's
  compilation of code samples for Minitel apps development using ESP32 (Arduino
  or micropython). This is a good start point if you want to use a modified
  ESP32. See also the associated [hackaday project
  page](https://hackaday.io/project/180473/instructions) for instructions.
  [**Telnet
  Pro**](https://github.com/iodeo/Minitel-ESP32/tree/main/arduino/Minitel1B_Telnet_Pro)
  💙 is highly recommended, and takes profit from SPIFFS which is a small
  filesystem for Arduino (useful to persist your server list, SSID/WiFi
  credentials...).

- [iodeo/Socketel](https://github.com/iodeo/Socketel) - A portal to Minitel
  webservices written in micropython for ESP32. Services are externally hosted,
  see [server section](#server-side).

- [eserandour/Minitel1B_Hard](https://github.com/eserandour/Minitel1B_Hard) -
  Minitel Library for Arduino (with HardwareSerial).

- [jbellue/3615_SSH](https://github.com/jbellue/3615_SSH) - An SSH client for
  ESP32.

#### Clients for serial communication from computer.

Projects dedicated to people using the serial port of their Minitel directly
from a computer with a custom adapter, without needing a standalone
microcontroller. Useful if you can to control your Minitel from a Raspberry Pi,
a computer, etc.

- [Arduiblog, Bring Minitel back to life](https://arduiblog.com/2019/04/29/ressuscitez-le-minitel/) -
  A small but efficient documentation on how to configure a Linux server to be
  used with a Minitel terminal using the serial port. (FR)

- [Mars Hack Lab article](https://mars-hack-lab.fr/?p=282) - Configure a Debian
  stretch running on a Raspberry Pi Zero W to be used with a Minitel in terminal
  mode. (FR)

- [mntl.ti](http://canal.chez.com/mntl.ti) - Alexandre Montaron's terminfo file.
  You will need this configuration file to provide the right inputs/character
  codes to the Minitel if you plan to use a Minitel as a Linux terminal.

- [cquest/websocket2minitel](https://github.com/cquest/websocket2minitel) - A
  middleware between a websocket-based Minitel server and the Minitel serial
  port. Written by Christian Quest. (EN)

- [Picotel](https://github.com/mchobby/picotel) - A project by Dominique
  Meurisse using a Raspberry Pi pico and custom adapters. See also [his
  blog](https://arduino103.blogspot.com/2022/04/minitel-branche-sur-mon-raspberry-pi.html)
  for more information. (FR/BE)

#### Reprogramming

- [**Microprocessor
  Reprogrammation**](https://github.com/jfdelnero/minitel#bon-et-apr%C3%A8s--que-peut-on-faire-avec-cela-)
  💙 - Someone with a decent level of determination found the way to upload
  a custom firmware to the very limited Minitel microprocessor, in order to
  display an impressive [demo](https://www.youtube.com/watch?v=a2HD6OzNoEo). You
  can find the code of the demo here:
  [the_minitel_demo](https://github.com/jfdelnero/minitel/tree/master/minitel2/the_minitel_demo).
  You can also find a dump of the original EPROM with the stock firmware
  [here](http://hxc2001.free.fr/minitel/Minitel_ROMs.zip). A presentation has
  been made on the subject, slides can be found
  [here](http://hxc2001.free.fr/minitel/Presentation_Etude_Minitel_2_FR_DE.pdf)
  (FR/DE)


### Server side

Minitel server implementations. The idea of these projects is to serve content
(VDT pages, text, other...) to clients (software running on a companion
board/computer next to the Minitel or on the Minitel directly).
Most of the time, these projects are meant to work with Websockets, Telnet, SSH,
a directly serial connected terminal, or natively on a X.25 network.

Depending on your architecture, client and the way the client is able to fetch
content, some of these projects may or may not be suitable for you.

- [Zigazou/PyMinitel](https://github.com/Zigazou/PyMinitel) - A python library
  to control a Minitel from a computer running Linux using a serial interface.

- [jiktim/minitel.js](https://github.com/jiktim/minitel.js) - A
  NodeJS server to send content to a Minitel through a websocket.

- [Zigazou/miplayer](https://github.com/Zigazou/miplayer) - A python program to
  continuously send VDT files to Minitel using serial interface(s).

- [cquest/pyNitel](https://github.com/cquest/pynitel) - A python library to
  write Minitel servers/software communicating to Minitel through a serial
  interface. Contains two example services, a minitel directory and 3615 ULLA
  simulation.

- [BwanaFr/minitel-server](https://github.com/BwanaFr/minitel-server) - A small
  TCP based Minitel server written in Python.

- [64rulez/PyMoIP](https://github.com/64rulez/PyMoIP) - A Minitel server using
  websockets in python. The project also contains other useful elements.

- [Zigazou/HaMinitel](https://github.com/Zigazou/HaMinitel) - An Haskell Minitel
  server for Linux pushing content through `/dev/ttyUSB*` or a real RS-232 port
  connected to a modem.

- [3615 IUT Auxerre
  Autoserver](https://serveur-minitel-2019-3615-iut-auxerre.webnode.fr/telechargements/) -
  A python Minitel server based on pyNitel and made by students in 2019 during
  an academic project. In the eventuality the site goes down in a future time,
  the sources are available
  [here](https://drive.google.com/drive/folders/1wLk6xO69QS76uVHQZJHJCjxRyCORX_Op).

- [Mushussu/Serveur-Minitel](https://github.com/Mushussu/Serveur-Minitel) - A
  Minitel test server written in C pushing content to `/dev/ttyUSB0`.

- [cquest/cristel](https://github.com/cquest/cristel) - Apple II Minitel server
  (1986) using [Merlin / BIGMAC
  assembler](https://en.wikipedia.org/wiki/Merlin_(assembler)).

- [cquest/dragster](https://github.com/cquest/dragster) - Obsolete Minitel
  server (1985) using MPW (Macintosh Programmer's Workshop).

- [ludosevilla/minipaviCli](https://github.com/ludosevilla/minipaviCli) - A Minitel
  server SDK allowing to build services around simple HTTP requests and PHP.


### Editors

Minitel pages used to be provided in the form of a tree structure of .VDT pages.
VDT format was use to describe characters displayed on the screen and basic
animations / the order in which the characters are displayed. You can see VDT
files as some sort of ASCII/GIF file, but beware: the charset is quite different
from classic ASCII. To produce VDT pages, editors exist, allowing you to find
the available characters, hexadecimal correspondence for each symbol on screen,
and write your animations.

- [Zigazou/miedit](https://github.com/Zigazou/miedit) - A browser-based Minitel
  page editor using Canvas and ES6. [Online editor
  demo](https://minitel.cquest.org)


### Emulators

- [Zigazou/miedit (emulator
  section)](https://github.com/Zigazou/miedit/blob/master/EMULATOR.md) - A
  Minitel emulator running in the browser.

- [bill-of-materials/docker-miedit-emulator (container)](https://github.com/bill-of-materials/docker-miedit-emulator) -
  If you're lazy and just want to quickly run a miedit emulator to connect to a
  websocket server, you can use this almost pointless Docker container I'm
  maintaining.

- [AS-connect](http://wiz0u.free.fr/pulsar/asconnect/) - A Windows Minitel
  emulator.

- [xtel](http://pficheux.free.fr/xtel/) - A Linux/Unix based Minitel emulator
  developed from 1985 to 2001 for X11. Ubuntu manpage is available
  [here](https://manpages.ubuntu.com/manpages/trusty/man1/xtel.1.html).

- [i-TimTel
  Flash](https://www.clubic.com/telecharger-fiche10827-i-timtel-flash.html) - An
  obsolete proprietary Minitel emulator made by [GOTO
  Software](https://fr.wikipedia.org/wiki/GOTO_Software) running on Windows.


### Tools

- [jfdelnero/vdt2bpm](https://github.com/jfdelnero/minitel/tree/master/VDT2BMP) - A small VDT to BPM file converter.
- [jfdelnero/vdt2wav](https://github.com/jfdelnero/minitel/tree/master/Minitel_VDT2WAV) - A small VDT to WAV file converter.
- [pamal/arbomaker](http://pamal.org/minitel/arboMaker6.zip) [(PAMAL Group)](http://wiki.pamal.org/wiki/LOGICIELS) - A Processing project to create Minitel browsing tree structures.
- [pamal/AviToVdt](https://pamal.org/minitel/aviToVdt.zip) [(PAMAL Group)](http://wiki.pamal.org/wiki/LOGICIELS) - A Processing project to convert movie files to `.vdt` for minitel display, running at 1 image per 24s.
- [pamal/JpgToVdt](https://pamal.org/minitel/JpgToVdt.zip) [(PAMAL Group)](http://wiki.pamal.org/wiki/LOGICIELS) - A Processing project to convert image files to `.vdt` for minitel display.
- [pamal/VdtAnalyser](http://pamal.org/minitel/VdtAnalyser.zip) [(PAMAL Group)](http://wiki.pamal.org/wiki/LOGICIELS) - A Processing project to analyse the content of a `.vdt` file and identify how a page has been written.
- [anto80/ImgToVdt](https://anto80.com/fr-fr/traitement-image/convertir-image-au-format-minitel-vdt-imgtovdt) - A Windows proprietary CLI conversion tool made by Anto80 (Non free)
- [chris-y/PPMToVtx](https://github.com/chris-y/ppmtovtx) - A C program to convert PPM files ([Portable pixmap](https://fr.wikipedia.org/wiki/Portable_pixmap)) to Vtx.
- [Zigazou/unitel2vdt](https://github.com/Zigazou/Unitel) - A standalone Python3 script that allows you to extract Videotex pages from an 8 inches floppy disk created on a Unitel application
- [Zigazou/ebcdic2vdt/unitel2vdt](https://github.com/Zigazou/ebcdic2vdt) - A C and bash program to convert EBCDIC disk images to vdt files.
- [Zigazou/teletext2minitel](https://github.com/Zigazou/teletext2minitel) - A simple standalone CLI PHP script which tries to convert Teletext/CEEFAX pages to Minitel pages.
- [immjs/minitel-react](https://github.com/immjs/minitel-react) - A react renderer designed for the Minitel


## Resources

### Official documentation

- [Official Tech. specs. (Minitel1B)](http://pila.fr/content/interface_usb_minitel/specifications%20techniques%20d%27utilisation%20du%20minitel.pdf) [(pila)](https://pila.fr/)
- [**Browsable Official Tech. specs. (Minitel1B)**](https://jbellue.github.io/stum1b/) 💙 - A readable transcript of the official documentation, thanks jbellue!
- [Official Magis Club](https://www.goto10.fr/minitel/notices/MinitelMagisClub.pdf) [(Goto10)](https://www.goto10.fr/)
- [Official Minitel 2 Philips](https://www.goto10.fr/minitel/notices/minitel_2_philips.pdf) [(Goto10)](https://www.goto10.fr/)
- [Official Minitel 5](https://www.goto10.fr/minitel/notices/minitel_5.pdf) [(Goto10)](https://www.goto10.fr/)


### Extra studies and documentation

- [**hxc2001**](https://github.com/jfdelnero/minitel) 💙 - Hardware study of the
  Minitel in french. Also available [here](http://hxc2001.free.fr/minitel/).
  This content is referred multiple time in this repository and feels like a
  rabbit hole. (FR)
- [Minitel
  Datasheets](https://github.com/mchobby/picotel/raw/master/docs/minitel2_hack/minitel-datasheets.zip) -
  All datasheets of Minitel parts, compiled by MCHobby.
- [Matthieu Benoit's archives](http://matthieu.benoit.free.fr/minitel.htm) - A good
  amount of technical documents and archives about Minitel and telephony. The
  page also contains EPROM dumps from multiple Minitel models. (EN/FR)
- [Minitel Printer
  Interface](http://matthieu.benoit.free.fr/pdf/minitel_printer_interface.pdf) -
  A scan from Hobbytronic N.36 (full mirror in better quality [here](https://archives.doctsf.com/documents/feuilleter_document.php?num_doc=74077&num_serie=219)), see page 13. (FR)
- [Building around
  Minitels](https://ia601600.us.archive.org/8/items/etsf-montages-autour-dun-minitel/ETSF%20-%20Montages%20autour%20d%27un%20Minitel.pdf) -
  A book by Christian Tavernier. Seems to be impossible to buy anywhere, so here
  is the scanned version of the book from archive.org. (FR)


### Other resources

- [**Musée du Minitel**](https://www.museeminitel.fr/) 💙 - The Minitel Museum.
  A lot of resources about Minitel and data preservation. Also contains an
  amazing [**forum**](https://forum.museeminitel.fr/) 💙 with an enthusiast
  community and almost all resources you will need. (FR)
- [Reviving Minitel Presentation](https://github.com/Zigazou/reviving-minitel) - Sources of the “Reviving Minitel” presentation given at FOSDEM 2020 (Belgium).
- [goto10](https://www.goto10.fr/) - BBS and Minitel archives.
- [Minitel.us](https://minitel.us/) - Minitel research lab. (US)
- [PAMAL Group](https://pamal.org/) - Media archaeology and preservation lab working a lot with Minitel hardware. (FR)
- [Pinky Story](http://troude.com/Pinky/) - The story of a Telematic server running between 1986 and 1992. (FR)
- [3615 IUT Auxerre](https://serveur-minitel-2019-3615-iut-auxerre.webnode.fr/) - An academic Minitel revival project by young students from Auxerre, France in 2019-2020. Well documented, they follow the same path everyone has to walk to revive a Minitel today. A mirror for their study is available [here](https://docplayer.fr/184023214-3615-iut-auxerre-projet-rt-1-ere-annee-rapport-bonnet-maxime-branlard-alexandre-grimard-quentin-salamolard-baptiste.html) and [there](https://1fb8adcd25.cbaul-cdnwnd.com/eab614bfc800f69002de12023a32276a/200000014-592c45a26b/BONNET_BRANLARD_GRIMARD_SALAMOLARD_Rapport_ProjetTut_3615_IUT-Auxerre%20%282%29.pdf). (FR)
- [**Telematic History**](https://telecommunications.monsite-orange.fr/page-5a854449a7560.html) 💙 - The complete history of Telematic with a lot of details and beautiful archive photographies. (FR)
- [From Minitel to Internet](https://larevuedesmedias.ina.fr/du-minitel-linternet) - INA (FR)
- [Transpac Network Shutdown](https://www.zdnet.fr/blogs/infra-net/x25-c-est-fini-39852412.htm) - In 2012, the French Minitel network has been shut down (FR)
- [XReyRobert/VideotexPagesRepository](https://github.com/XReyRobert/VideotexPagesRepository) -
  An archive of VDT pages with GIF conversion for modern browsing.


## Open Minitel services

- [3611.re](http://3611.re/) - 09.7227.3671
- [3615co.de](http://3615co.de) - 09.7227.3675
- [3614 HACKER](http://www.3614hacker.fr) - 09.7252.7252
- [3614 TEASER](http://www.3614teaser.fr:8080/)
- [3615 SM](https://sm.3615.live/)
- [JELORA](https://www.jelora.fr/post/2017/08/27/Serveur-Minitel.html) - 09.7262.9267
- [COMPUTEL](https://www.computel.fr/) - 01.8421.8116
- [JCA](https://forum.museeminitel.fr/t/computel-et-jca-de-retour/350) - 01.8421.8115
- [HYTREL](#) - 03.5925.1034
- [IUT Auxerre](https://serveur-minitel-2019-3615-iut-auxerre.webnode.fr/tester-le-serveur/) - 03.5843.5150
- [Cosmos 6502](#) - 01.8421.8124 (intermittent)
- [RetroCampus](http://bbs.retrocampus.com/) - bbs.retrocampus.com:1651 (Telstar/Videotex) - Tel. 0039.0522.750051
- [GlassTTY](https://glasstty.com/) - glasstty.com:6502 (Telstar/Videotex)
- [MiniPavi](https://www.minipavi.fr/) - 09.7210.1721

## Contribute

Contributions welcome! Read the [contribution guidelines](contributing.md) first.

## License

The [awesome-minitel](https://github.com/bill-of-materials/awesome-minitel)
project is released under the CeCILL-B ([en](./Licence_CeCILL-B_V1-en.txt),
[fr](./Licence_CeCILL-B_V1-fr.txt)) license.

https://cecill.info/
