# README - OpenBook E-Reader

**Proiect TSC - Caramida-Stoian Petrisor-Cristian**

## Prezentare Generală

OpenBook este un e-reader open-source bazat pe ESP32-C6, dotat cu ecran e-paper de 7.5", senzori de mediu, sistem de alimentare cu baterie și conectivitate Wi-Fi și USB-C. Documentul prezintă structura hardware și componentele integrate.

## Diagramă Bloc

## Lista BOM

| **Componentă**       | **Part Number**               | **Descriere**                          | **Furnizor (Mouser)**                                                               | **Datasheet**                                                                                 |
|----------------------|------------------------------|----------------------------------------|------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| S                    | BME680                        | Senzor temperatură, umiditate, presiune | [Mouser](https://eu.mouser.com/ProductDetail/Bosch-Sensortec/BME680)               | [Datasheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme680-ds001.pdf) |
| U2                   | ESP32-C6-WROOM-1-N8           | MCU Wi-Fi 6, Bluetooth 5               | [Mouser](https://eu.mouser.com/ProductDetail/Espressif-Systems/ESP32-C6-WROOM-1-N8) | [Datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-c6-wroom-1_datasheet_en.pdf) |
| U1                   | W25Q512JVEIQ                  | Memorie Flash SPI 512Mb               | [Mouser](https://eu.mouser.com/ProductDetail/Winbond/W25Q512JVEIQ)                 | [Datasheet](https://www.winbond.com/resource-files/W25Q512JV%20RevD%2004082020.pdf)              |


---

## Detalii Functionalitate Hardware

## ESP32-C6-WROOM-1-N8

- **Rol**: Controler principal, conectivitate wireless și suport periferice.
- **Specificații**: 160MHz, 512KB SRAM, 8MB Flash.
- **Interfețe**:
  - **SPI**: Display e-paper, memorie Flash, card Micro SD.
  - **I2C**: Senzor BME680, monitorizare baterie (MAX17048), RTC (DS3231).
  - **GPIO**: Interacțiune cu butoane și LED-uri.
  - **UART**: Debugging și comunicare serială.

## Senzor BME680

- **Funcționalitate**: Măsoară temperatură, umiditate, presiune atmosferică și calitate aer.
- **Interfață**: I2C la 400kHz.
- **Consum**: Sub 1mA activ, sub 1µA în repaus.

## Sistem de Alimentare

- **Baterie**: Li-Po 2500mAh, 3.7V.
- **Încărcare**: Controlată de MCP73831 prin USB-C, cu capacitate de 1A.
- **Monitorizare**: MAX17048 prin I2C.
- **Consum energetic**:
  - Activ (Wi-Fi + ecran actualizat): ~150mA.
  - Standby (doar ecran afișat): ~10mA.
  - Deep Sleep: Sub 50µA.
  - **Autonomie estimată**: Aproximativ o săptămână (~250 ore cu un consum mediu de 10mA).

## Butoane de Navigare

- Butoane tactile Panasonic EVQPUJ02K cu rezistență pull-up de 10KΩ.

## USB-C

- **Rol**: Încărcare (5V/1A) și transfer de date (USB 2.0).
- **Protecție**: Diode ESD (USBLC6-2SC6Y) pentru siguranță la supratensiune.


## Configurare Pini ESP32-C6

| **Pin ESP32-C6** | **Funcție**         | **Componentă**         | **Rol**                                    |
|------------------|--------------------|------------------------|--------------------------------------------|
| GPIO0           | BOOT_BUTTON        | Buton                  | Mod boot la inițializare                   |
| GPIO1           | RESET_BUTTON       | Buton                  | Reset manual                               |
| GPIO2           | CHANGE_BUTTON      | Buton                  | Schimbare meniuri                          |
| GPIO3           | EPD_CS             | Display E-Paper        | Chip Select pentru SPI                     |
| GPIO4           | EPD_DC             | Display E-Paper        | Control Date/Comenzi                       |
| GPIO5           | EPD_RST            | Display E-Paper        | Reset display                              |
| GPIO6           | EPD_BUSY           | Display E-Paper        | Detectare stare refresh                    |
| GPIO7           | SPI_MOSI           | Display, Flash, SD     | Linii de date SPI                          |
| GPIO8           | SPI_MISO           | Display, Flash, SD     | Linie de date SPI (citire)                 |
| GPIO9           | SPI_SCK            | Display, Flash, SD     | Semnal de ceas SPI                         |
| GPIO10          | FLASH_CS           | Memorie Flash          | Chip Select pentru memorie                 |
| GPIO11          | SD_CS              | Card Micro SD          | Chip Select pentru card SD                 |
| GPIO12          | I2C_SDA            | BME680, MAX17048, DS3231 | Linie de date pentru I2C                   |
| GPIO13          | I2C_SCL            | BME680, MAX17048, DS3231 | Linie de ceas pentru I2C                   |
| GPIO14          | CHG_LED            | LED                    | Indică procesul de încărcare               |
| GPIO15          | UART_TX            | Debugging              | Transmitere date seriale                    |
| GPIO16          | UART_RX            | Debugging              | Recepție date seriale                       |
| GPIO17          | USB_D+             | USB-C                  | Linie de date USB pozitivă                  |
| GPIO18          | USB_D-             | USB-C                  | Linie de date USB negativă                  |

Notă: Pinii sunt alocați conform specificațiilor ESP32-C6 și cerințelor dispozitivului OpenBook. Anumiți pini sunt multifuncționali și pot fi utilizați în diferite configurații.

