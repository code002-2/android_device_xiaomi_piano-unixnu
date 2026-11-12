# A830 driver sources

The driver work for this port lives in
[UniXNU-Piano-Drivers](https://github.com/xiaomi-pad-8-pro-development/UniXNU-Piano-Drivers),
which `modules/Pagani` points at.

The branch used for the bring-up is `piano-gpu`; it carries the piano board glue
(`drivers/Adreno830/board/`), the SMEM socinfo fallback, the S7 skip when the board has no
Gen8 ZAP image, the annibale guard-table fix and the table-pool overlap length.

Measured board values: `chip_id 0x44050001`, `soc_id` **639** (PKX110 reports 618), no Gen8 ZAP,
GMU/SQE/AQE firmware byte-identical to the 13T pins.
