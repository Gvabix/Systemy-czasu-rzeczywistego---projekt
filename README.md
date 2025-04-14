# Systemy czasu rzeczywistego - Model Smart Akwarium w języku AADL

Planowane komponenty projektu:
 
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

### Subprogram 
- ReadTemperature – logika odczytu temperatury z czujnika.

- ReadPH – logika odczytu pH z czujnika.

- ReadLight – logika odczytu poziomu światła.

- ControlHeater – sterowanie grzałką.

- ControlLight – sterowanie oświetleniem.

- SendNetworkPacket – wysyłanie pakietu danych przez sieć Wi-Fi.

- ReceiveCommand – odbieranie komend z aplikacji mobilnej.

- ControlSubsystem – grupa podprogramów odpowiedzialnych za sterowanie urządzeniami wykonawczymi (grzałka, światło).

### Threads
- TempMonitor – wątek monitorujący temperaturę wody.

- PHMonitor – wątek monitorujący pH wody.

- LightMonitor – wątek monitorujący poziom oświetlenia.

- NetworkReceiver – wątek odbierający komendy z sieci.

- ControlLoop – wątek przetwarzający dane i podejmujący decyzje sterujące.

- MonitoringThreads – grupa wątków zajmujących się monitoringiem warunków w akwarium.

### Process
- SensorProcess – proces zawierający wątki czujników (zbierających dane).

- ControlProcess – proces zawierający logikę sterowania na podstawie danych z czujników.

### Subprogram
- PeriodicCheck – okresowe sprawdzanie stanu akwarium (np. co kilka sekund).

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
