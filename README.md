# proprietary_vendor_lge

Fork of `TheMuppets/proprietary_vendor_lge` with the changes of the **LG G
Pad X 8.0 (V521)** port to **LineageOS 15.1** (Android 8.1).

| Branch | What it is |
| --- | --- |
| `lineage-15.1` | the branch the V521 port builds from |
| `staging/lineage-15.1` | the upstream staging branch, unchanged |

## What is different on `lineage-15.1`

| Commit | Subject |
| --- | --- |
| `46e5e31` | v521: keep the CAF blobs out of the AOSP protobuf stack |
| `1a9bf59` | v521: drop the stock CAF libril.so that shadowed the LineageOS one |
| `f47a4e5` | v521: build the prebuilt libraries as vendor modules |
| `24a590f` | v521: add the Qualcomm DPM daemon and its libraries |
| `57c76d0` | v521: add the OEM crypto library for Widevine |

* **The CAF protobuf runtime** (`46e5e31`) is installed under a second name,
  `/system/vendor/lib/libqc-protobuf-lite.so`, so that the CAF blobs and
  the AOSP ones do not fight over the same symbols.  The `DT_NEEDED`
  entries of the blobs are rewritten at build time by
  `device/lge/v521/patch-qc-protobuf.py`; the blobs in this repository stay
  **pristine**.
* **The stock CAF `libril.so`** (`1a9bf59`) must not be installed into
  `/system/lib`: it shadows the LineageOS `hardware/ril-caf` one in
  `/system/vendor/lib` and the radio daemon then cannot link.
* **The prebuilt libraries** (`f47a4e5`) are built as vendor modules so
  that they land in `/system/vendor/lib` and not in `/system/lib`.
* **The DPM daemon** (`24a590f`) - `dpmd`, the NSRM configuration and the
  TCM client - comes from the stock ROM of the device and is byte-identical
  to it.
* **The OEM crypto library** (`57c76d0`) is Qualcomm's `liboemcrypto.so`.
  The Widevine CDM loads it at run time (it is not a `DT_NEEDED` entry)
  and it is the piece that reaches the TEE; without it the CDM cannot
  initialise its crypto backend at all.

## The port

The full description of the port is in the device tree:
<https://github.com/MicahOttah/android_device_lge_v521>
