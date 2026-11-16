# proprietary_vendor_lge

Fork of `TheMuppets/proprietary_vendor_lge` for the **LG G Pad X 8.0 (V521)**
LineageOS 15.1 port.  The port builds from `lineage-15.1`; the other
branches are upstream.

Changes:

* The CAF protobuf runtime is installed as `libqc-protobuf-lite.so` so it
  does not clash with the AOSP one.  The blobs here stay pristine; the
  device tree rewrites their `DT_NEEDED` entries at build time.
* LG's stock CAF `libril.so` is not installed (it shadowed the LineageOS
  one).
* Prebuilt libraries are vendor modules.
* Added: the Qualcomm DPM daemon and libraries, and `liboemcrypto.so` for
  Widevine L1.

Port and device tree: <https://github.com/MicahOttah/android_device_lge_v521>
