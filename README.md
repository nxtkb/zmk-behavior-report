# zmk-behavior-report

## introduction

report keyboard information (battery, connection type)

## usage

this modules depends on module: [nxtkb/zmk-behavior-send-string](https://github.com/nxtkb/zmk-behavior-send-string), so some setups are needed for that module

### configs

increase BEHAVIORS_QUEUE_SIZE (default is 64)

```conf
CONFIG_ZMK_BEHAVIORS_QUEUE_SIZE=512
```

### charmap

define a charmap file like `character_map.dtsi`

### behavior

define `report.dtsi`

```dtst
/*
 * Copyright (c) 2020 The ZMK Contributors
 *
 * SPDX-License-Identifier: MIT
 */

#include <dt-bindings/zmk/behaviors.h>

/ {
    behaviors {
        // Behavior can be invoked on peripherals, so name must be <= 8 characters.
#if ZMK_BEHAVIOR_OMIT(default_report)
    /omit-if-no-ref/
#endif
        default_report: default_report {
            compatible = "zmk,behavior-report";
            #binding-cells = <0>;
        };
    };
};
```

### keymap

```dtsi
#include "behaviors/report.dtsi"

/ {
    keymap {
        compatible = "zmk,keymap";

        default_layer {
            bindings = <
                &default_report    &none
                &none           &none
            >;
        };
    };
}
```