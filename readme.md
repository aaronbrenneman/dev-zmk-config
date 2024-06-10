# brenneman's zmk-config

Welcome to my personal [ZMK firmware](https://github.com/zmkfirmware/zmk/)
configuration. It consists of a 34-keys base layout that is re-used for various
boards, including my Corne-5col, my Planck, and my Preonic.[^1]

## features

- helper macros from urob's [zmk-helpers](https://github.com/urob/zmk-helpers)
- "timeless" homerow mods
- combos replacing the symbol layer

## to do 

- smart numbers and smart mouse layers that automatically toggle off when done
- sticky shift on right thumb, double-tap (or shift + tap) activates
  caps-word
- arrow-cluster doubles as <kbd>home</kbd>, <kbd>end</kbd>, <kbd>begin/end of
  document</kbd> on long-press
- more intuitive shift-actions: <kbd>, ;</kbd>, <kbd>. :</kbd> and <kbd>?
  !</kbd>
- <kbd>shift</kbd> + <kbd>space</kbd> morphs into <kbd>dot</kbd> →
  <kbd>space</kbd> → <kbd>sticky-shift</kbd>
- modified Github Actions workflow that recognizes git-submodules
- automated [build-scripts](https://github.com/urob/zmk-config/tree/main/scripts#readme)
  for local and Docker-based building (independently of VS Code)
- (img/keymap.png)

## config (using helpers)

```C++
/* use helper macros to define left and right hand keys */
#include "zmk-helpers/key-labels/36.h"                                      // key-position labels
#define KEYS_L LT0 LT1 LT2 LT3 LT4 LM0 LM1 LM2 LM3 LM4 LB0 LB1 LB2 LB3 LB4  // left-hand keys
#define KEYS_R RT0 RT1 RT2 RT3 RT4 RM0 RM1 RM2 RM3 RM4 RB0 RB1 RB2 RB3 RB4  // right-hand keys
#define THUMBS LH2 LH1 LH0 RH0 RH1 RH2                                      // thumb keys

/* left-hand HRMs */
ZMK_HOLD_TAP(hml,
    flavor = "balanced";
    tapping-term-ms = <280>;
    quick-tap-ms = <175>;                // repeat on tap-into-hold
    require-prior-idle-ms = <150>;
    bindings = <&kp>, <&kp>;
    hold-trigger-key-positions = <KEYS_R THUMBS>;
    hold-trigger-on-release;             // delay positional check until key-release
)

/* right-hand HRMs */
ZMK_HOLD_TAP(hmr,
    flavor = "balanced";
    tapping-term-ms = <280>;
    quick-tap-ms = <175>;                // repeat on tap-into-hold
    require-prior-idle-ms = <150>;
    bindings = <&kp>, <&kp>;
    hold-trigger-key-positions = <KEYS_L THUMBS>;
    hold-trigger-on-release;             // delay positional check until key-release
)
```

[^1]:With an additional numrow for gaming.
