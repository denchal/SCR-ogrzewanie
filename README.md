# Systemy czasu rzeczywistego - projekt

## Tytuł modelu:

System centralnego ogrzewania budynku

## Dane studenta:

Michał Gomułczak

mgomulczak@student.agh.edu.pl

## Opis modelowanego systemu:

### Opis ogólny
```
Zamodelowany system jest systemem centralnego ogrzewania
w budynku mieszkalnym lub użytkowym, którego celem jest
utrzymywanie zadanej temperatury w poszczególnych pomieszczeniach.
System składa się z pieca grzewczego, czujników temperatury,
termostatów pokojowych, zaworów regulujących przepływ ciepła,
oraz elementów sterujących.
```
### Opis szczegółowy
```
System ogrzewania obsługuje kilka niezależnych stref grzewczych
(np. pokoje, korytarze, łazienki). Każda strefa posiada
termostat oraz czujnik temperatury, które mierzą aktualne warunki
i zgłaszają zapotrzebowanie na ciepło.

Piec (kocioł gazowy lub elektryczny) dostarcza ciepło do
instalacji, a przepływ czynnika grzewczego jest regulowany
zaworami w zależności od potrzeb zgłaszanych przez strefy.

System posiada logikę nadrzędną, która decyduje, kiedy należy
uruchomić piec, w oparciu o zbiorcze zapotrzebowanie. Jeżeli
żadna ze stref nie potrzebuje ciepła, piec pozostaje w trybie
czuwania. W przypadku wystąpienia zapotrzebowania – piec
zostaje włączony i utrzymuje zadaną temperaturę w obiegu.

System uwzględnia tryb nocny oraz harmonogramy czasowe,
które zmieniają temperatury zadane w zależności od pory dnia
lub obecności mieszkańców.

Jeżeli wykryta zostanie awaria (np. przegrzanie kotła, brak
wody w instalacji), system automatycznie zatrzymuje piec
i informuje użytkownika.

Możliwe jest także ręczne włączenie trybu awaryjnego (np. na czas mrozów),
który wymusza minimalne ogrzewanie wszystkich stref
niezależnie od ustawień użytkownika.
```
### Komponenty:
```
system HeatingControlSystem – główny system sterujący pracą ogrzewania

device RoomThermostat – termostat pokojowy z możliwością ustawienia temperatury

device TemperatureSensor – czujnik mierzący rzeczywistą temperaturę w pomieszczeniu

device Boiler – urządzenie grzewcze (piec, kocioł)

device ZoneValve – zawór kontrolujący przepływ czynnika grzewczego do strefy

device EmergencySwitch – przycisk lub przekaźnik włączający tryb awaryjny

thread Scheduler – wątek realizujący harmonogram czasowy ogrzewania

thread SafetyMonitor – wątek nadzorujący stan bezpieczeństwa systemu (np. awarie)

bus CommunicationBus – magistrala komunikacyjna między komponentami systemu
```
