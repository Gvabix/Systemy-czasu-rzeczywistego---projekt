# Systemy czasu rzeczywistego - Model Smart Akwarium w języku AADL

## Autorzy:
- Gabriela Bułat, gbulat@student.agh.edu.pl
- Emilia Myrta, emiliamyrta@student.agh.edu.pl

## Opis projektu

**Smart Akwarium** to zintegrowany system monitorowania i sterowania parametrami wodnego akwarium, realizowany w języku AADL. System składa się z wielu komponentów podzielonych na różne typy AADL. Model systemu wykorzystuje właściwości SEI oraz analiz MIPS.

## Funkcjonalności systemu:

Monitorowanie oraz automatyczne sterowanie:

- temperaturą wody,

- poziomem pH,

- oświetleniem,

- poziomem wody.

Podgląd w czasie rzeczywistym z kamery.

Sterowaniem karmieniem ryb.

Przesyłania statusu oraz alertów przez WiFi.

Komunikacja z użytkownikiem poprzez aplikację (WiFi).

## Struktura systemu:
 
 ### Główne podsystemy:

 #### SensorSubsystem
- Odpowiada za zbieranie danych z czujników.
- Wykorzystuje proces SensorProcess.
- Udostępnia dane do dalszego przetwarzania.

#### ApplicationSubsystem
- Zawiera logikę sterującą oraz urządzenia i interfejsy z aplikacją użytkownika.
- Realizuje funkcje decyzyjne w oparciu o dane z SensorSubsystem.

## Główne komponenty modelu AADL:

 ### Data:
- `Timestamp` – znacznik czasu dla każdej próbki danych.
- `TemperatureData`, `PHData`, `LightLevelData`, `WaterLevelData` – dane pomiarowe.
- `PHDoseData`, `FeedingCommand`, `CameraCommand`, `CommandData` – dane sterujące.
- `NetworkPacket`, `SensorReading`, `SchedulerConfig` – dane komunikacyjne i pomocnicze.

### Threads
- Wątki monitorujące: `TempMonitor`, `PHMonitor`, `LightMonitor`, `WaterLevelMonitor`
- Wątki sterujące: `ControlLoop`, `FeedingControl`, `CameraControl`
- Komunikacja i diagnostyka: `NetworkReceiver`, `AllertManager`, `Logger`, `cmd_mux`
  
### Process
- `SensorProcess` – obsługa i przetwarzanie danych z czujników.
- `ControlProcess` – logika decyzyjna i sterowanie urządzeniami.

### Devices
- Czujniki: `TemperatureSensor`, `PHSensor`, `LightSensor`, `WaterLevelSensor`
- Urządzenia wykonawcze: `HeaterActuator`, `LightActuator`, `PHActuator`, `WaterPumpActuator`, `FishFeeder`
- Komunikacja: `WiFiModule`, `FishCamera`, `UserAppDevice`

### Bus
- `I2CBus` – magistrala sprzętowa czujników.
- `WiFiBus` – logiczna magistrala komunikacyjna z aplikacją.

### Processor
- `RPiController` – procesor główny systemu.
- `CameraProcessor` – dedykowany procesor dla kamery.

### Memory
- `MainMemory` – pamięć główna systemu.
- `CameraMemory` – pamięć dedykowana obsłudze kamery.

### System
- `SmartAkwariumSystem` – top-level system integrujący podsystemy: SensorSubsystem i ApplicationSubsystem, wraz z procesorami, pamięciami i magistralami.


## Dane (Data)

| Komponent          | Opis |
|--------------------|------|
| `Timestamp`        | Znacznik czasu każdej próbki – używany do synchronizacji i analizy czasowej danych. |
| `TemperatureData`  | Dane z czujnika temperatury – aktualna temperatura wody. |
| `PHData`           | Dane z czujnika pH – poziom kwasowości wody. |
| `LightLevelData`   | Poziom oświetlenia w akwarium. |
| `WaterLevelData`   | Poziom wody w akwarium. |
| `PHDoseData`       | Komenda dawkowania oraz wyboru środka regulującego pH. |
| `FeedingCommand`   | Polecenie aktywacji karmienia ryb. |
| `CameraCommand`    | Polecenie uruchomienia/wyłączenia kamery. |
| `CommandData`      | Dane ogólne dla urządzeń wykonawczych. |
| `NetworkPacket`    | Pakiet danych do/od aplikacji użytkownika. |
| `SensorReading`    | Surowe dane z czujników. |
| `SchedulerConfig`  | Konfiguracja harmonogramu sterowania. |

## Wątki (Threads)

| Komponent          | Opis |
|--------------------|------|
| `TempMonitor`      | Odczytuje dane z czujnika temperatury i przesyła je do procesora. |
| `PHMonitor`        | Monitoruje wartość pH. |
| `LightMonitor`     | Monitoruje poziom oświetlenia w akwarium. |
| `WaterLevelMonitor`| Monitoruje poziom wody. |
| `ControlLoop`      | Główna pętla sterująca – przetwarza dane i generuje komendy sterujące dla grzałki, pompy, dozownika pH oraz lampy. |
| `FeedingControl`   | Harmonogramuje i wykonuje karmienie ryb. |
| `CameraControl`    | Zarządza uruchomieniem kamery. |
| `NetworkReceiver`  | Odbiera dane z aplikacji użytkownika przez WiFi. |
| `AllertManager`    | Generuje alerty na podstawie stanów awaryjnych. |
| `Logger`           | Zapisuje dane i zdarzenia systemowe do pamięci. |
| `cmd_mux`          | Przesyła komendy do NetworkReceiver. |

## Procesy (Processes)

| Komponent        | Opis |
|------------------|------|
| `SensorProcess`  | Agreguje i filtruje dane z czujników, przekazuje do analizy. |
| `ControlProcess` | Analizuje dane, podejmuje decyzje, wysyła komendy sterujące do urządzeń. |

## Urządzenia (Devices)

| Komponent             | Opis |
|-----------------------|------|
| `TemperatureSensor`   | Czujnik temperatury – pomiar temperatury wody. |
| `PHSensor`            | Czujnik pH – pomiar kwasowości. |
| `LightSensor`         | Czujnik światła – mierzy natężenie oświetlenia. |
| `WaterLevelSensor`    | Mierzy aktualny poziom wody w akwarium. |
| `HeaterActuator`      | Grzałka – podnosi temperaturę wody. |
| `LightActuator`       | Steruje oświetleniem akwarium. |
| `PHActuator`          | Dawkuje środek regulujący pH. |
| `WaterPumpActuator`   | Pompa wody – napełnianie/odprowadzanie. |
| `FishFeeder`          | Urządzenie do automatycznego karmienia ryb. |
| `WiFiModule`          | Umożliwia komunikację z aplikacją użytkownika. |
| `FishCamera`          | Kamera monitorująca stan akwarium. |
| `UserAppDevice`       | Aplikacja mobilna do sterowania i podglądu danych. |

## Magistrale (Bus)

| Komponent   | Opis |
|-------------|------|
| `I2CBus`    | Magistrala do komunikacji z czujnikami – fizyczne połączenie. |
| `WiFiBus`   | Logiczna magistrala komunikacyjna z aplikacją – oparte na WiFi. |

## Procesory (Processor)

| Komponent        | Opis |
|------------------|------|
| `RPiController`  | Główny procesor systemu – wykonuje logikę sterującą, odbiera dane z czujników. |
| `CameraProcessor`| Obsługuje przetwarzanie obrazu z kamery i jego transmisję. |

## Pamięć (Memory)

| Komponent       | Opis |
|-----------------|------|
| `MainMemory`    | Główna pamięć operacyjna systemu. |
| `CameraMemory`  | Dedykowana pamięć do przechowywania obrazu wideo. |

## Podsystemy (Subsystems)

| Komponent             | Opis |
|-----------------------|------|
| `SensorSubsystem`     | Odpowiedzialny za zbieranie danych z czujników, ich przetwarzanie i przekazywanie do części sterującej. Zawiera czujniki, wątki monitorujące i proces `SensorProcess`. |
| `ApplicationSubsystem`| Odpowiada za działania zewnętrzne: sterowanie urządzeniami, komunikację z użytkownikiem oraz rejestrowanie danych. Zawiera wątki sterujące, kamerę, moduł WiFi i proces `ControlProcess`. |

## System (System)

| Komponent               | Opis |
|-------------------------|------|
| `SmartAkwariumSystem`   | Główna jednostka systemowa integrująca wszystkie komponenty: czujniki, procesy, pamięci, komunikację i interfejs z użytkownikiem. Zawiera podsystemy `SensorSubsystem` (zbieranie danych) i `ApplicationSubsystem` (interakcja z użytkownikiem i sterowanie). |


# Architektura systemu.

### Diagram podsystemu sensorów

![Diagram smart akwarium](podsys1.png)

### Diagram podsystemu aplikacji
![Diagram smart akwarium](2podsys.png)


### Diagram systemu głównego
![Diagram smart akwarium](3system.png)

# Analizy

### Analiza Weight Totals
![analizy](weighttotals.png)

### Analiza MIPS Budget
![analizy](notbound.png)

# Bibliografia:

- [Empowering Aquarists a Comprehensive Study On IOT-Enabled Smart Aquarium Systems For Remote Monitoring And Control](https://www.researchgate.net/publication/382053839_Empowering_Aquarists_a_Comprehensive_Study_On_IOT-Enabled_Smart_Aquarium_Systems_For_Remote_Monitoring_And_Control)

- [Implementation of GSM Module based Smart Aquarium Monitoring and Controlling System](https://www.researchgate.net/publication/375553645_Implementation_of_GSM_Module_based_Smart_Aquarium_Monitoring_and_Controlling_System)

- [Assess your aquarium’s health with an AI-enabled ultrasonic sensor](https://blog.arduino.cc/2024/05/07/assess-your-aquariums-health-with-an-ai-enabled-ultrasonic-sensor/)

- [The Architecture Analysis and
Design Language: an overview](http://www.openaadl.org/downloads/tutorial_models15/part1_introducing_aadl.pdf)
