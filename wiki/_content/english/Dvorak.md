This is a quick blurb for setting or converting your keymaps to [dvorak](https://en.wikipedia.org/wiki/Dvorak_Simplified_Keyboard "wikipedia:Dvorak Simplified Keyboard") instead of qwerty.

## Contents

*   [1 Setting Dvorak Layout](#Setting_Dvorak_Layout)
*   [2 For international users](#For_international_users)
    *   [2.1 Swedish](#Swedish)
    *   [2.2 Spanish](#Spanish)
    *   [2.3 United Kingdom](#United_Kingdom)
*   [3 Typing tutors](#Typing_tutors)

## Setting Dvorak Layout

See [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") or [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") for configuration details.

For the virtual terminal, dvorak and the regional keyboard are combined into one keymap. But Xorg lists dvorak as varian of your regional keymap.

The `us` Dvorak keymaps for the virtual terminal are:

*   `dvorak`, Standard
*   `dvorak-l`, Left handed Dvorak
*   `dvorak-r`, Right handed Dvorak
*   `dvorak-programmer`, Programmer Dvorak

The `us` Dvorak keymaps for Xorg are:

*   `dvorak`, Standard
*   `dvorak-l`, Left Handed Dvorak
*   `dvorak-r`, Right Handed Dvorak
*   `dvp`, Programmer Dvorak
*   `dvorak-intl`, International Dvorak
*   `dvorak-classic`
*   `dvorak-alt-intl`

**Note:** For console, these are standalone keymaps, but for Xorg these are variants of the `us` layout, you need to pass them to `XkbVariant` variable. See [Keyboard configuration in Xorg#Setting keyboard layout](/index.php/Keyboard_configuration_in_Xorg#Setting_keyboard_layout "Keyboard configuration in Xorg") for an explanation.

## For international users

### Swedish

Swedish people interested in trying dvorak can find the swedish "version", called svorak, at [aoeu.info](http://www.aoeu.info)! To convert to svorak in X you do not need to download any additional files from www.aoeu.info.

### Spanish

In console, specify `dvorak-es` instead of `dvorak` to use the Spanish dvorak variant.

In Xorg, specify `es` as `XkbLayout` and `dvorak` as `XkbVariant`.

### United Kingdom

In console, specify `dvorak-ukp` (available from [dvorak-ukp](https://aur.archlinux.org/packages/dvorak-ukp/)) instead of `dvorak` to use the United Kingdom dvorak variant with ISO/IEC 9995-1 punctuation.

In Xorg, specify `gb` as `XkbLayout` and `dvorakukp` as `XkbVariant`.

## Typing tutors

	Console

*   [dvorakng](https://aur.archlinux.org/packages/dvorakng/)

	GUI

*   [ktouch](https://www.archlinux.org/packages/?name=ktouch) (includes Dvorak lessons in English, French, German & Spanish)
*   [klavaro](https://www.archlinux.org/packages/?name=klavaro) Dvorak lessons: (BG; BR; DE_neo2; EO; FR; FR_bépo; TR; UK; US; US_BR; US_ES; US_SE)