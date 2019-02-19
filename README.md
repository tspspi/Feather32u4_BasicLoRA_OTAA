# Feather32u4 BasicLoRA OTAA Example

A simple example how to use Feather 32u4 with RFM95W modem
and TTN.

Uses the LMIC library from https://github.com/matthijskooijman/arduino-lmic

## Software modification

This sample deviates from the original sample by adding

```
while (!Serial) {
 delay(1);
 }

```

after the initial serial port configuration as well as

```
LMIC_setClockError(MAX_CLOCK_ERROR * 1 / 100)
```

which is called after ```LMIC_reset```. This option increases the size of
the receive window by 1%.

## Hardware modifications

To use the LoRa32u4 II from BSFrance/DIYMail with LoRAWan you have to bridge
the DIO1 port with any digital input (pin6 with the configuration in this
example). If you use the FSK mode you've to connect DIO2 with any digital input
(for example 5) and provide the dio pin configuration too.

* DIO0 (connected internally to pin 7) is the TxDone/RxDone pin
* DIO1 is the RxTimeout for LoRa mode
* DIO2 is the TimeOut for FSK mode

If the DIO1 connection or configuration is missing one can see the join / join
accept messages as well as the first data message but not any more transmits.