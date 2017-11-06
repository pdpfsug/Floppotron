Raspberry Pi
============
Costruzione Software
--------------------
In principio c'era nulla... 

Installazione OS
^^^^^^^^^^^^^^^^
Ora procedi con la preparazione del raspberry.

Per prima cosa diventa root.

  .. highlight:: console
  su
Scarica il sistema operativo `Raspbian <https://downloads.raspberrypi.org/raspbian_lite_latest>`_:

  .. highlight:: console
  wget https://downloads.raspberrypi.org/raspbian_lite_latest

Scomprimi il file compresso:

  .. highlight:: console
  unzip $(ls -rt | tail -n1)

Nel mentre inserisci la micro SD nel computer.

Visualizza il percorso della SD:

  .. highlight:: console
  lsblk

Scrivi la ISO sulla SD, il processo formattera' la SD.

Sostituisci *<iso>* con il nome del file appena estratto.

Sostituisci *<dev>* con il percorso della SD, solitamente **/dev/sdb**.

EX. ``dd if=2017-09-07-raspbian-stretch-lite.img of=/dev/sdb status=progress``

  .. highlight:: console
  umount <dev>

  dd if=<iso> of=<dev> status=progress


Preparazione
^^^^^^^^^^^^
Dopo il completamento del *dd* inserisci la SD nel raspberry.

Collega il cavo Ethernet dal raspberry al computer oppure al router.

Alimenta il raspberry con il cavo microUSB.

Controlla la configurazine della rete dal tuo computer:

  .. highlight:: console
  ip a

Dopo 1 minuto il raspberry si accende.

Scopri l'ip del raspberry.

Sostituisci *<int>* con l'interfaccia della rete che precedentemente hai ottenuto con il comando ``ip a``.

EX. ``arp-scan --interface=enp2s0 --localnet``.

  .. highlight:: console
  arp-scan --interface=<int> --localnet

Una volta scoperto l'ip del'raspberry collegati da remoto.

Sostituisci *<ip>* con l'ip del raspberry che precedentemente hai opttenuto con il comando ``arp-scan``.

  .. highlight:: console
  ssh pi@<ip>

Ci sara' uno scambio di chiavi pubbliche, Premi "Yes".

La passward per accedere al raspberry e' **raspberry**.


Ora sei sul terminale del raspberry.
Diventa root:

  .. highlight:: console
  su

Clona il repository `Floppotron <https://github.com/pdpfsug/Floppotron.git>`_

  .. highlight:: console
  apt-get install git -y

  cd /home/pi

  git clone https://github.com/pdpfsug/Floppotron.git

Installa la libreria WiringPi: 

  .. highlight:: console
  cd /home/pi/Floppotron/wiringPi

  ./build

Compila il programma musicale:
  
  .. highlight:: console
  gcc floppy.cpp -o start -l wiringPi

Appena il collegamento del lettore floppy al raspberry averra' fai partire la musica:

  .. highlight:: console
  ./start
