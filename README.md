# SFUD
SFUD (Serial Flash Universal Driver) Serial Flash Universal Driver Library

# 0. What is SFUD

SFUD is an open source serial SPI Flash universal driver library. Since there are most types of serial Flash in the market, and the specifications and commands of each Flash are different, SFUD is designed to solve these differences in Flash, so that our products can support Flash of different brands and specifications, and improve the Flash involved. The reusability and extensibility of the functional software can also avoid the risk of Flash out of stock or discontinuation of the product.

- Main features: support SPI/QSPI interface, object-oriented (support multiple Flash objects at the same time), flexible tailoring, strong scalability, support for 4-byte addresses

- Resource useage
  - Standard occupation: RAM: 0.2KB ROM: 5.5KB
  - Minimum occupation: RAM: 0.1KB ROM: 3.6KB

- Design ideas:
  - With SFDP support: It is the parameter table standard of serial Flash function formulated by JEDEC (Solid State Technology Association), the latest version V1.6B (https://www.jedec.org/standards-documents/docs/jesd216b). The standard stipulates that there will be a parameter table in each Flash, which stores Flash specification parameters such as Flash capacity, write granularity, erase command, and address mode. At present, except for some manufacturers’ older Flash models that do not support this standard, most of the other new factory’s Flash already support the SFDP standard. Therefore, the library will first read the SFDP table parameters during initialization.

  - Without SFDP support: If the Flash does not support the SFDP standard, SFUD will query the Flash parameter information table provided in the configuration file (/sfud/inc/sfud_flash_def.h) to see if the Flash is supported. If it is not supported, you can add the parameter information of the Flash in the configuration file (for details on the adding method, see 2.5 Adding Flash that the library does not currently support). After obtaining the specifications and parameters of the Flash, all operations on the Flash can be realized.

# 1. Why choose SFUD

- Avoid project risks caused by Flash out of stock, Flash discontinuation or product expansion
- More and more projects store firmware in serial Flash, such as: ESP8266 firmware, motherboard BIOS and firmware in other common electronic products, etc. However, various Flash specifications and commands are not uniform. Using SFUD can avoid the problem of not being able to adapt to different types of Flash hardware platforms based on the same functional software platform, and improve the reusability of the software
- Simplify the software process and reduce the difficulty of development. Now only need to configure SPI communication, you can start playing serial Flash freely
- Can be used to make Flash programmer/writer

# 2. How to use SFUD

## 2.1 Flash supported

The following table shows all the Flashes that have been tested on the Demo platform on the real machine. The Flash that does not support the SFDP standard has been defined in the Flash parameter information table.

|  Model  | Manufacturer | Capacity | Maximum Speed | SFDP Standard | QSPI Mode | Comment |
| :-----: | :----------: | :------: | :-----------: | ------------- | --------- | :------ |
| [W25Q64FV](https://www.winbond.com/resource-files/w25q64fv%20revs%2007182017.pdf)  | Winbond | 64Mb  | 104MHz | Content Cell  | Content Cell  | Content Cell  |
| [W25Q128FV](https://www.winbond.com/resource-files/w25q128fv%20rev.m%2005132016%20kms.pdf) | Winbond | 128Mb | 104MHz | Content Cell  | Content Cell  | Content Cell  |
