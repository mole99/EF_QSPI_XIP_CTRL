# MS_QSPI_XIP_CACHE
Quad I/O SPI Flash memory controller with support for:
- AHB lite interface.
- Execute in Place (XiP).
- NxM Read-only Direct-Mapped Cache; N: number of lines (NUM_LINES), M: line size (LINE_SIZE).

Intended to be used with SoCs that have no on-chip flash memory. 

## Todo:
 - [ ] support for WB bus
 
## Performance
### Miss Time
```28 + 4 x LINE_SIZE```

### ASIC PPA
The following data is obtained using the Sky130 HD library

| Configuration | # of Cells (K) | Delay (ns) | I<sub>dyn</sub> (mA/MHz) | I<sub>s</sub> (nA) | 
|---------------|----------------|------------|--------------------------|--------------------|
| 16x16 | 7.2 | 12 | 0.0625 | 20 |
| 32x16 | 14.3 | 17  | 0.126 | 39.5 |
