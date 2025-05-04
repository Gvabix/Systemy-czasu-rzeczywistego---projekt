# Systemy czasu rzeczywistego - Model Smart Akwarium w języku AADL

# Autorzy:
- Gabriela Bułat, gbulat@student.agh.edu.pl
- Emilia Myrta, emiliamyrta@student.agh.edu.pl

# Opis projektu

Smart Akwarium to zintegrowany system sterowania akwarium, realizowany w języku AADL, którego celem jest monitorowanie i zarządzanie parametrami środowiska wodnego. System składa się z wielu komponentów podzielonych na różne typy AADL.

# Planowane komponenty projektu:
 
 ### Pakiet
- SmartAkwarium – główny pakiet zawierający wszystkie komponenty systemu inteligentnego akwarium.

 ### Data 
- TemperatureData – dane z czujnika temperatury wody.

- PHData – dane z czujnika pH wody.

- LightLevelData – dane dotyczące poziomu oświetlenia akwarium.

- CommandData – komendy przychodzące z zewnątrz (np. z aplikacji mobilnej).

- SchedulerConfig – konfiguracja harmonogramu sterowania.

- NetworkPacket – dane do przesyłania przez sieć (np. status, alerty).

- SensorReading – uogólniona struktura pojedynczego odczytu z czujnika.

### Threads
- TempMonitor – wątek monitorujący temperaturę wody.

- PHMonitor – wątek monitorujący pH wody.

- LightMonitor – wątek monitorujący poziom oświetlenia.

- NetworkReceiver – wątek odbierający komendy z sieci.

- ControlLoop – wątek przetwarzający dane i podejmujący decyzje sterujące.

### Process
- SensorProcess – proces zawierający wątki czujników (zbierających dane).

- ControlProcess – proces zawierający logikę sterowania na podstawie danych z czujników.

### Devices
- TemperatureSensor – fizyczny czujnik temperatury.

- PHSensor – czujnik poziomu pH wody.

- LightSensor – czujnik natężenia światła.

- HeaterActuator – urządzenie wykonawcze: grzałka.

- LightActuator – urządzenie wykonawcze: oświetlenie.

- WiFiModule – moduł komunikacji bezprzewodowej Wi-Fi.

### Bus
- I2CBus – magistrala komunikacyjna dla czujników (np. I2C).

- WiFiBus – logiczna magistrala do przesyłania danych przez Wi-Fi.

### Processor
- RPiController – główny procesor sterujący.

### Memory
- MainMemory – pamięć operacyjna dla systemu.

### System
- SmartAkwariumSystem – top-level system integrujący wszystkie komponenty.
