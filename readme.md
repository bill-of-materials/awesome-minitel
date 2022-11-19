# Awesome Minitel [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of Minitel and Telematic resources

![Minitel Glitchs](/minitel.png)

## Contents

- [Hardware](#hardware)
  - [Documentation](#documentation)
  - [DIY serial interface](#diy-serial-interface)
- [Software](#software)
  - [Client side](#client-side)
    - [ESP32](#esp32)
  - [Server side](#server-side)
  - [Editors](#editors)
  - [Emulators](#emulators)
  - [Tools](#tools)
- [Resources](#resources)
- [Open Minitel Services](#open-minitel-services)


## Hardware

### Documentation

- [Official Tech. specs. (Minitel1B)](http://pila.fr/content/interface_usb_minitel/specifications%20techniques%20d%27utilisation%20du%20minitel.pdf) [(pila)](https://pila.fr/)
- [Official Magis Club](https://www.goto10.fr/minitel/notices/MinitelMagisClub.pdf) [(Goto10)](https://www.goto10.fr/)
- [Official Minitel 2 Philips](https://www.goto10.fr/minitel/notices/minitel_2_philips.pdf) [(Goto10)](https://www.goto10.fr/)
- [Official Minitel 5](https://www.goto10.fr/minitel/notices/minitel_5.pdf) [(Goto10)](https://www.goto10.fr/)
- [hxc2001](https://github.com/jfdelnero/minitel): Hardware study of the Minitel
  in french. Also available [here](http://hxc2001.free.fr/minitel/)

### DIY Serial interface

Different ways of using the Péri-informatique Serial socket of the Minitel.

- [ESP32](https://hackaday.io/project/180473-minitel-esp32)
- [Custom cable](https://www.jelora.fr/post/2020/02/25/Adaptateur-prise-DIN-peri-informatique-Minitel-vers-Serie-RS232-et-Serie-USB.html)


## Software

### Client side

#### ESP32

Projects for Minitels with a serial port and ESP32 microcontroller.

- [Minitel-ESP32](https://github.com/iodeo/Minitel-ESP32): Sample codes for
  Minitel apps development using ESP32 (arduino or micropython).
- [Socketel](https://github.com/iodeo/Socketel): A portal to minitel webservices
  written in micropython for ESP32.
- [Minitel1B_Hard](https://github.com/eserandour/Minitel1B_Hard): Minitel
  Library for Arduino (with HardwareSerial).
- [3615 SSH](https://github.com/jbellue/3615_SSH): An SSH client for ESP32.


### Server side

- [PyMinitel](https://github.com/Zigazou/PyMinitel): A python library to control
  a minitel from a computer running Linux.
- [pyNitel](https://github.com/cquest/pynitel): A python library to write Minitel
  servers/software. Contains two example services, a minitel directory and 3615
  ULLA simulation.
- [cristel](https://github.com/cquest/cristel): Apple II minitel server (1986)
  using [Merlin / BIGMAC assembler](https://en.wikipedia.org/wiki/Merlin_(assembler)).
- [dragster](https://github.com/cquest/dragster): Obsolete minitel server (1985)
  using MPW (Macintosh Programmer's Workshop).
- [minitel-server](https://github.com/BwanaFr/minitel-server): A small TCP based
  minitel server written in Python.
- [3615 IUT Auxerre
  Autoserver](https://serveur-minitel-2019-3615-iut-auxerre.webnode.fr/telechargements/)
  A small python minitel server made by students in 2019 during an academic
  project. In the eventuality the site goes down in the next years, the sources
  are available
  [here](https://drive.google.com/drive/folders/1wLk6xO69QS76uVHQZJHJCjxRyCORX_Op).


### Editors

- [miedit](https://github.com/Zigazou/miedit): A browser based minitel page
  editor using Canvas and ES6. [Online editor demo](https://minitel.cquest.org).


### Emulators

- [miedit (emulator
  section)](https://github.com/Zigazou/miedit/blob/master/EMULATOR.md): A
  Minitel emulator running in the browser
- [i-TimTel
  Flash](https://www.clubic.com/telecharger-fiche10827-i-timtel-flash.html): An
  obsolete proprietary Minitel emulator made by [GOTO
  Software](https://fr.wikipedia.org/wiki/GOTO_Software) running on Windows.

### Tools

- [vdt2bpm](https://github.com/jfdelnero/minitel/tree/master/VDT2BMP): A small
  VDT to BPM file converter.
- [vdt2wav](https://github.com/jfdelnero/minitel/tree/master/Minitel_VDT2WAV): A
  small VDT to WAV file converter.
- [arbomaker](http://pamal.org/minitel/arboMaker6.zip) [(PAMAL
  Group)](http://wiki.pamal.org/wiki/LOGICIELS): A Processing project to create
  minitel browsing tree structures.
- [AviToVdt](https://pamal.org/minitel/aviToVdt.zip) [(PAMAL
  Group)](http://wiki.pamal.org/wiki/LOGICIELS): A Processing project to
  convert movie files to `.vdt` for minitel display, running at 1 image per
  24s.
- [JpgToVdt](https://pamal.org/minitel/JpgToVdt.zip) [(PAMAL
  Group)](http://wiki.pamal.org/wiki/LOGICIELS): A Processing project to
  convert image files to `.vdt` for minitel display.
- [VdtAnalyser](http://pamal.org/minitel/VdtAnalyser.zip) [(PAMAL
  Group)](http://wiki.pamal.org/wiki/LOGICIELS): A Processing project to
  analyse the content of a `.vdt` file and identify how a page has been
  written.
- [ImgToVdt](https://anto80.com/fr-fr/traitement-image/convertir-image-au-format-minitel-vdt-imgtovdt):
  A Windows proprietary CLI conversion tool made by Anto80. (Non free)


## Resources

- [Musée du Minitel](https://www.museeminitel.fr/): The Minitel Museum. A lot of
  resources about Minitel and data preservation.
- [Reviving Minitel Presentation](https://github.com/Zigazou/reviving-minitel):
  Sources of the “Reviving Minitel” presentation given at FOSDEM 2020 (Belgium).
- [goto10](https://www.goto10.fr/): BBS and Minitel archives.
- [hxc2001/the_minitel_demo](https://github.com/jfdelnero/minitel/tree/master/minitel2/the_minitel_demo):
  An impressive demo using minitel. Videos are available on Youtube
  [here](https://www.youtube.com/watch?v=a2HD6OzNoEo) and
  [there](https://www.youtube.com/watch?v=ba_51zGY1cQ).
- [Minitel.us](https://minitel.us/): Minitel research lab. (US)
- [PAMAL Group](https://pamal.org/): Media archeology and preservation lab
  working a lot with Minitel hardware. (FR)
- [Pinky Story](http://troude.com/Pinky/): The story of a Telematic server
  running between 1986 and 1992. (FR)
- [3615 IUT
  Auxerre](https://serveur-minitel-2019-3615-iut-auxerre.webnode.fr/): An
  academic Minitel revival project by young students from Auxerre, France in
  2019-2020. Well documented, they follow the same path everyone has to walk to
  revive a Minitel today. A mirror for their study is available
  [here](https://docplayer.fr/184023214-3615-iut-auxerre-projet-rt-1-ere-annee-rapport-bonnet-maxime-branlard-alexandre-grimard-quentin-salamolard-baptiste.html)
  and [there](https://1fb8adcd25.cbaul-cdnwnd.com/eab614bfc800f69002de12023a32276a/200000014-592c45a26b/BONNET_BRANLARD_GRIMARD_SALAMOLARD_Rapport_ProjetTut_3615_IUT-Auxerre%20%282%29.pdf).
- [Telematic
  History](https://telecommunications.monsite-orange.fr/page-5a854449a7560.html):
  The complete history of Telematic with a lot of details and beautiful archive
  photographies. (FR)


## Open Minitel services

- [3611.re](http://3611.re/): 09.7227.3671
- [3615co.de](http://3615co.de): 09.7227.3675
- [3614 HACKER](http://www.3614hacker.fr): 09.7252.7252
- [3614 TEASER](http://www.3614teaser.fr:8080/)
- [3615 SM](https://sm.3615.live/)
- [JELORA](https://www.jelora.fr/post/2017/08/27/Serveur-Minitel.html): 09.7262.9267
- [COMPUTEL](https://www.computel.fr/): 01.8421.8116
- [JCA](https://forum.museeminitel.fr/t/computel-et-jca-de-retour/350): 01.8421.8115
- [HYTREL](#): 03.5925.1034
- [IUT Auxerre](https://serveur-minitel-2019-3615-iut-auxerre.webnode.fr/tester-le-serveur/): 03.5843.5150
- [Cosmos 6502](#): 01.8421.8124 (intermittent)

## Contribute

Contributions welcome! Read the [contribution guidelines](contributing.md) first.
