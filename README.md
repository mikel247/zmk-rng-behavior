# ZMK-behavior-random

This module adds random number generators using the onboard random entropy generator


## Usage
#TODO
To load the module, add the following entries to `remotes` and `projects` in
`config/west.yml`.

```yaml
manifest:
  remotes:
    - name: zmkfirmware
      url-base: https://github.com/zmkfirmware
    - name: urob
      url-base: https://github.com/urob
  projects:
    - name: zmk
      remote: zmkfirmware
      revision: v0.3 # Set to desired ZMK release.
      import: app/west.yml
    - name: zmk-leader-key
      remote: urob
      revision: v0.3 # Should match ZMK release.
  self:
    path: config
```

Note: This module uses a version scheme that is synchronized with upstream ZMK.
To ensure compatibility, I highly recommend setting the revision of this module
to the same as ZMK's.

## Configuration

### Leader sequences

Leader sequences are defined as child nodes of a leader-key instance. Each
sequence takes two arguments `sequence` and `bindings`. Example:

```c
/ {
    behaviors {
        leader1: leader1 {
            compatible = "zmk,behavior-leader-key";
            #binding-cells = <0>;
            usb { sequence = <U S B>; bindings = <&out OUT_USB>; };
            ble { sequence = <B L E>; bindings = <&out OUT_BLE>; };
            bt0 { sequence = <B N0>; bindings = <&bt BT_SEL 0>; };
            bt1 { sequence = <B N1>; bindings = <&bt BT_SEL 1>; };
            bt2 { sequence = <B N2>; bindings = <&bt BT_SEL 2>; };
            btc { sequence = <C L E A R>; bindings = <&bt BT_CLR>; };
            boot { sequence = <B O O T>; bindings = <&bootloader>; };
            reset { sequence = <R E S E T>; bindings = <&sys_reset>; };
        };

        leader2: leader2 {
            compatible = "zmk,behavior-leader-key";
            #binding-cells = <0>;
            de_ae { sequence = <A E>; bindings = <&de_ae>; };
            de_oe { sequence = <O E>; bindings = <&de_oe>; };
            de_ue { sequence = <U E>; bindings = <&de_ue>; };
        };
    };
};
```
