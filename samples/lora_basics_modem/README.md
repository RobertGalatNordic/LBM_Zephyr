# LoRa Basics Modem samples

Those examples provide reference code from Semtech adapted to Zephyr for LBM.

* porting_tests: Some low level tests from LBM to validate the Zephyr port
* hw_modem: For testing purposes, exposes an UART bus usually handled by Pytest scripts
* lctt_certif: The reference LCTT certification example
* periodical_uplink: A fully working example that joins the network + periodical uplink when the user presses the button.


## Board support

The samples are tested on the `nrf52840dk/nrf52840` board and the shields provided by this repository.
If any other board is used, a new DTS overlay should be created for it.

## Building and flashing

Go into the sample you want to flash, then run (with the relevant board and shield):

```bash
west build -b nrf52840dk/nrf52840 -- -DSHIELD=semtech_lr1110mb1xxs
west flash
```

## Boards without Arduino header

If the board does not have arduino header definied in DTS, it can still be used with this project.
The example is `nrf54l15dk/nrf54l15/cpuapp` board.
For this board aditional shield has been created (`LBM/boards/shields/nrf54l15dk_arduino_adapter`) to reroute the gpio connections to dummy Ardiono header.
This shield also enables all necessary hardware components required for that target, so there is no need for aditional baord overlay in the sample.
To use it simply add the adapter shield before the semtech sheld like in the example build command below:

```bash
west build -b nrf54l15dk/nrf54l15/cpuapp --pristine -- -DSHIELD="nrf54l15dk_arduino_adapter;semtech_lr1110mb1xxs"
west flash
```

