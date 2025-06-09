# Systemy czasu rzeczywistego – projekt

## Tytuł modelu:

System centralnego ogrzewania budynku

## Dane studenta
`Michał Gomułczak`
`mgomulczak@student.agh.edu.pl`

## Opis modelowanego systemu

### Opis ogólny

System centralnego ogrzewania budynku ma na celu utrzymanie zadanych temperatur w poszczególnych strefach budynku (np. pokoje, łazienki). System składa się z pieca grzewczego, czujników temperatury, termostatów pokojowych, zaworów sterujących przepływem czynnika grzewczego, logiki sterującej oraz mechanizmów bezpieczeństwa.

System obsługuje tryb harmonogramu czasowego oraz tryb awaryjny, który wymusza minimalne ogrzewanie niezależnie od warunków zadanych przez użytkownika.

### Opis funkcjonalny

System został zamodelowany w języku AADL w pakiecie HeatingSystem. Składa się z komponentów reprezentujących urządzenia (devices), procesy sterujące (processes), magistrale (bus) i główny system nadrzędny (HeatingControlSystem).

W modelu uwzględniono dwie niezależne strefy grzewcze. Każda strefa posiada swój czujnik temperatury, termostat i zawór strefowy.

`RoomThermostat` – odbiera aktualną temperaturę z czujnika oraz generuje zapotrzebowanie na ciepło.

`TemperatureSensor` – dostarcza aktualną temperaturę z pomieszczenia.

`ZoneValve` – steruje przepływem czynnika grzewczego na podstawie poleceń sterujących.

`Boiler` – źródło ciepła. Otrzymuje sygnał zapotrzebowania oraz komendy harmonogramu. Odpowiada za rozprowadzanie czynnika grzewczego.

`Distributor` – agreguje zapotrzebowania ze stref i steruje zaworami oraz sygnalizuje zbiorcze zapotrzebowanie do pieca.

`Scheduler` – proces generujący harmonogramowe polecenia sterujące (np. ustawienia temperatur dziennych/nocnych).

`SafetyMonitor` – proces nadzorujący bezpieczeństwo systemu (np. wykrycie przegrzania, braku wody).

`EmergencySwitch` – urządzenie aktywujące tryb awaryjny.

`SchedulerToBoilerBus` – magistrala przesyłająca komendy harmonogramu do pieca.

## Funkcje specjalne

Tryb nocny / harmonogramowy – realizowany przez proces Scheduler, który steruje temperaturami zadanymi w czasie.

Tryb awaryjny – aktywowany przez EmergencySwitch, wymusza minimalne grzanie niezależnie od zapotrzebowania.

Zabezpieczenia – w przypadku wykrycia awarii przez SafetyMonitor, piec przechodzi w tryb bezpieczny i zostaje wyłączony.

## Struktura modelu

Model zawiera pełną instancję implementacyjną systemu HeatingControlSystem.impl, w której znajdują się wszystkie podsystemy oraz połączenia między komponentami. Uwzględniono następujące powiązania:

Komunikacja pomiędzy czujnikami a termostatami.

Przekazywanie zapotrzebowania cieplnego do dystrybutora.

Sterowanie zaworami na podstawie decyzji dystrybutora.

Sterowanie piecem w zależności od zapotrzebowania oraz harmonogramu.

Sygnalizacja błędów i aktywacja trybu awaryjnego.

## Dane i porty

W systemie zdefiniowano typy danych:

`Temperature` – temperatura zadana lub aktualna.

`HeatDemand` – zapotrzebowanie cieplne strefy.

`ValveCommand` – komenda sterująca zaworem.

`BoilerCommand` – komenda z harmonogramu do pieca.

Water – medium grzewcze w obiegu.

Porty są typu data port (dla danych ciągłych) i event port (dla zdarzeń systemowych, np. awarii).

