# Known Notes and Source/Report Differences

This portfolio repository is a cleaned version of the original team project.

## 1. Routing terminology

The current source implements **controlled flooding**, not a route-discovery protocol such as AODV.
`get_next_hop()` currently returns `BROADCAST_ID`, while TTL and `(src, seq)` deduplication are used
to limit forwarding loops and repeated packets.

## 2. CRC

The cleaned source enables the SX1278/LoRa hardware CRC using:

```cpp
LoRa.enableCrc();
```

The team report also discusses a software CRC16-CCITT layer. That software CRC16 implementation
is not present in the source version included here, so this repository does not claim it.

## 3. DIO0 pin discrepancy

The current source defines:

```cpp
#define DIO0_PIN 2
```

The team report's wiring table lists DIO0 on GPIO26. Verify the actual hardware wiring before
flashing. This repository intentionally does not change the pin without hardware confirmation.

## 4. Portfolio fixes applied

- Fixed the Huffman compression-selection ratio bug (`int` truncation -> `float` comparison).
- Removed an incorrect fragment-counter increment from `send_raw_packet()`.
- Removed machine-specific COM ports from `platformio.ini`.
- Removed duplicated library/submodule and IDE-generated files from the portfolio copy.
- Renamed documentation and clarified that the network uses controlled flooding.
