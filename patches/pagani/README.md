# A830 bring-up patches against `modules/Pagani`

`piano-gpu-driver.patch` carries the driver-side work this port needs; apply it with

```sh
git -C modules/Pagani apply ../../patches/pagani/piano-gpu-driver.patch
```

What it contains (all verified on the device):

- `Adreno830Start.cpp`: the SMEM socinfo fallback, the ZAP stage skipped when the board has no
  Gen8 image (piano's vendor set only ships the gen70e0x ones), and the probes used during bring-up.
- `Adreno830Status.h`: the S0 firmware-checked bit used by the same path.
- `A830Smmu.cpp`: the guard-table ASID check must not run in the annibale profile (TTBR1 is 0 there),
  and the bootloader's pre-existing GPU SMMU routes are taken down instead of refused.
- `NativeAdrenoVm.cpp`: a mapping's table overlap is compared against the table pool
  (`capacity_pages * 4096`), not against the 4 GiB aperture.
- `NativeAdrenoHandleIndex.h`, `NativeAdrenoPublish.cpp`: clang-24 and header fixes.
- `BootProgress`, `UfsLog`, `DarwinBoot`, `NativeVirtioBlock`, `Stage7Probe`: the boot-side changes
  this port relies on.

Board values used here: `soc_id` **639** (measured in SMEM on piano; PKX110 reports 618),
no Gen8 ZAP, GMU/SQE/AQE firmware byte-identical to the 13T pins.
