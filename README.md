# Klipper
Klipper Configs

DS18B20

Für den Einbau des Temperatursensors habe ich diesen hier bei AliExpress bestellt. 
Bei dem gibt es nichts zu löten und er braucht nur über 3 Kabel an den Raspi angeschlossen zu werden.

https://de.aliexpress.com/item/1005001665962941.html?spm=a2g0o.order_list.order_list_main.20.35e65c5fhwykA2&gatewayAdapt=glo2deu

Hier das passende Gehäuse das ich für den Sensor erstellt habe. 
Er lässt sich etwas stramm rein schieben aber so hält er ohne Schrauben oder kleben.
Das Gehäuse hab ich mit Spiegelklebeband von Tesa in den Druckraum geklebt.

https://www.printables.com/model/1161203-ds18b20-gehause

Wenn der Sensor am Pi angeschlossen ist den Pi starten und die fogenden Dinge durchführen:

per ssh auf raspi zugreifen und mit sudo raspi-config ins Menü Interfaces gehen.
Dort dann das 1-wire interface aktivieren und den Raspi neustarten.
Wieder per ssh zugreifen und mit lsmod | grep -i w1_ schauen, ob die passenden Kernel geladen sind.
Danach mit ls /sys/bus/w1/devices/  die Serial des Sensors auslesen und in der config in der printer.cfg eintragen.
Dann sollte der Sensor schon unter Klipper mit der aktuellen Temperatur sichtbar sein.
Wenn nicht und er bringt eine Fehlermeldung mit MCU dann musst du in deiner printer.cfg den genauen MCU Namen vom Raspi suchen und 
in der config vom Sensor abändern.
Dann nur noch das M191 macro in der printer.cfg einfügen und die Anweisungen in MaschinenStartGcode.jpg und OrcaSettingsDruckraum.jpg befolgen.
Jetzt sollte euer Drucker erst bis zur ausgewählten Temperatur aufheizen und dann mit dem Druck beginnen. Im Macro ist eingestellt das er bereits 2 Grad unter der Zieltemperatur beginnt,
den Druck vorzubereiten.

Tasmota

Die Tasmota Einrichtung ist eigentlich ganz einfach!
Ich verwende diese hier:

https://amzn.eu/d/0zycFKx

Ihr schließt sie in der Nähe des Routers an eine Steckdose an.
Danach mit dem Handy nach neuen Netzwerken suchen und mit dem Tasmota Wlan verbinden.
Danach solltet ihr auf das Web Ui der Tasmota geleitet werden und könnt sie dort mit dem Router verbinden.
Den Rest findet ihr unter Tasmota Config Moonraker und Tasmota Macro Power on-off
Wenn das alles eingerichtet ist dann sollte nach Neustart vom Raspi im Fluidd bzw Mainsail ein Schieberegler mit dem Namen Printer erscheinen worüber der Drucker aus und an geschaltet werden kann.
Dann sollten zwei Macros erscheinen mit aktivate und deaktivate Power off. Mit aktivate Schaltet ihr die automatische Abschaltung ein und mit deaktivate cancelt ihr es wieder falls er doch an bleiben soll.
Er kühlt den Drucker dann nach dem Druck ab und schaltet die Tasmota dann automatisch aus. Dafür natürlich den Drucker an die Tasmota hängen. Den Pi lasse ich 24/7 durch laufen da er nicht viel Strom verbraucht.


