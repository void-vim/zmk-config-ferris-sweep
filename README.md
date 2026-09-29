# Ferris Sweep ZMK config

4 layers, mirrored to what you built in ZMK Studio, plus a mouse layer.

## Layers

| # | Name | How to enter |
| --- | --- | --- |
| 0 | qwerty | default |
| 1 | numbers | hold right inner thumb (`fn`) |
| 2 | symbols | hold left inner thumb (`fn`) |
| 3 | mouse | hold left thumb (symbols) + tap `T` -> vim keys `H J K L`; right thumb on mouse layer exits |

## Layout

```
layer 0 (qwerty)
row1  Q W E R T          Y U I O P
row2  A/S S/A D/C F/G    H J/G K/C L/A '/S
row3  Z X C V B          N M , . /
thmb  fn(SYM) space      enter fn(NUM)

layer 1 (numbers)   [each row starts with &mo 2 so the symbol layer stays active while you use both hands]
row1  - 1 2 3 tab    Home PgDn PgUp End ~
row2  - 4 5 6 bksp   left down up right ;
row3  - 7 8 9 0 -    - - - - -
thmb  - esc          - -

layer 2 (symbols)
row1  - [ { } mouse  ^ ( ) ] ~
row2  ! @ # $ %       * - = \ `
row3  - - studio - -       &  _  +  |  -
thmb  - -             - fn(NUM)

layer 3 (mouse)   vim movement
row1  - - - - LCLK             scrlUp scrlDn MCLK MB4 MB5
row2  - - - - -                 H=left  J=down  K=up  L=right
row3  - - - - -                 - - - - -
rest &trans  (passes through)
thmb  &trans &trans             &trans toggle off
```

## Notes

- `A/S` style keys are hold-tap: tap = letter, hold = modifier (200 ms, tap-preferred).
- Mouse enters with a plain key: hold **left thumb** (symbol layer) and tap `T` (`&tog 3`). The mouse layer stays on after you release the thumb. Tap **T** again, or the **right thumb** on the mouse layer, to turn it off. No combo/timing involved.
- Mouse move accelerates (2500 max, `mmv` node), scroll step 20 (`msc` node). Tune in `config/cradio.keymap`.
- `studio_unlock` is on symbol layer row 3, second key (hold right thumb, tap `X`). ZMK Studio edits live on the keyboard, so after editing in Studio your file changes need "Restore Stock Settings" to show up again.
- `&mo N` = hold to switch to layer N. (`&lt` is layer-tap and needs two args, e.g. `&lt 1 &kp TAB`.) Validate a keymap locally before pushing: preprocess it with `cpp` + `dtc` the way Zephyr does.
- Build: push to GitHub, action builds `cradio_left`, `cradio_right`, `settings_reset` (nice_nano_v2). Left half is the Studio-enabled one.
