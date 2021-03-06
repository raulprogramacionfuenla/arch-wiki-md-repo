**Состояние перевода:** На этой странице представлен перевод статьи [Sound system](/index.php/Sound_system "Sound system"). Дата последней синхронизации: 16 февраля 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Sound_system&diff=0&oldid=510425).

Эта статья рассказывает о базовых элементах управления звуком. Для более подробного описания смотрите [professional audio](/index.php/Pro_Audio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pro Audio (Русский)").

## Contents

*   [1 Общие сведения](#Общие_сведения)
*   [2 Драйверы и интерфейс](#Драйверы_и_интерфейс)
*   [3 Звуковые серверы](#Звуковые_серверы)
*   [4 Смотрите также](#Смотрите_также)

## Общие сведения

Звуковая система Arch Linux состоит из нескольких уровней

*   Драйверы и интерфейс – поддержка и взаимодействие с аппаратным обеспечением

*   Usermode API (библиотеки) – требуются и используются приложениями

*   **(дополнительно)** Звуковые серверы usermode – находят лучшее применение в сложных систмах, требующих одновременной поддержки множества аудиоприложений и незаменимы для более продвинутых возможностей, см. [pro audio](/index.php/Pro_Audio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pro Audio (Русский)").

*   **(дополнительно)** Звуковые фреймворки – высокоуровневые программные окружения, не связанные с серверными процессами.

Базовая установка Arch Linux уже включает ядро звуковой системы ([ALSA](/index.php/ALSA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ALSA (Русский)")), и множество утилит для него может быть установлено из [официального репозитория](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Если вам требуются дополнительные возможности, вы можете сменить его на [OSS](/index.php/OSS "OSS") или выбрать другой [звуковой сервер](https://en.wikipedia.org/wiki/sound_server "wikipedia:sound server").

## Драйверы и интерфейс

*   **[The Advanced Linux Sound Architecture (ALSA)](/index.php/ALSA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ALSA (Русский)")** — Компонент ядра Linux, содержащий драйверы устройств и обеспечивающий низкоуровневую поддержку для звукового аппаратного обеспечения.

	[http://www.alsa-project.org/](http://www.alsa-project.org/) || входит в состав ядра по умолчанию

*   **[The Open Sound System (OSS)](/index.php/OSS "OSS")** — Альтернативная звуковая архитектура для Unix- и POSIX-совместимых систем. OSS 3-ей версии являлась основной звуковой системой для Linux и включалась в ядро, но была вытеснена ALSA в 2002 году, когда 4-ая версия OSS стала проприетарным программным обеспечением. OSSv4 вновь стала свободным ПО в 2007, когда 4Front Technologies опубликовали ее исходные коды и разместила их под лицензией GPL. OSS не поддерживает такое же множество устройств как ALSA, но в некоторых случаях работает лучше.

	[http://www.opensound.com/](http://www.opensound.com/) || [oss](https://aur.archlinux.org/packages/oss/)

## Звуковые серверы

*   **[PulseAudio](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PulseAudio (Русский)")** — Очень популярный звуковой сервер, используемый большинством основных приложений Linux сегодня. Очень хорошо поддерживает несколько одновременных входов и может использоваться как клиент-серверная система передачи звука. Легко настраивается для работы. Зачастую для этого достаточно только установить приложение.

	[https://www.freedesktop.org/wiki/Software/PulseAudio/](https://www.freedesktop.org/wiki/Software/PulseAudio/) || [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio)

*   **[JACK Audio Connection Kit](/index.php/JACK_Audio_Connection_Kit "JACK Audio Connection Kit")** — Старая редакция звукового сервера используемая в профессиональной работе со звуком, особенно в приложениях, требующих быстрого отклика, таких как приложения для записи, эффектов, сведения в реальном времени и многих других. Хотя эта редакция является старой, она сохраняет группу активных и преданных разработчиков, и многие проблемы удается решить путем проб и ошибок.

	[http://jackaudio.org/](http://jackaudio.org/) || [jack](https://www.archlinux.org/packages/?name=jack)

*   **JACK2** — Это новая версия JACK, разработанная непосредственно для работы в мультипроцессорных системах и также включающую передачу через сеть.

	[https://github.com/jackaudio/jackaudio.github.com/wiki/Q_difference_jack1_jack2](https://github.com/jackaudio/jackaudio.github.com/wiki/Q_difference_jack1_jack2) || [jack2](https://www.archlinux.org/packages/?name=jack2)

*   **JACK2 with D-Bus** — Это JACK2 с иной архитектурой запуска, позволяющей работать совместно с PulseAudio и иными не-JACK приложениями, что являлось проблемой для двух предыдущих категорий JACK серверов.

	[https://github.com/jackaudio/jackaudio.github.com/wiki/WalkThrough_User_jack_control](https://github.com/jackaudio/jackaudio.github.com/wiki/WalkThrough_User_jack_control) || [jack2-dbus](https://www.archlinux.org/packages/?name=jack2-dbus)

*   **[NAS](https://en.wikipedia.org/wiki/Network_Audio_System "wikipedia:Network Audio System")** — Это звуковой сервер, поддерживаемый некоторыми крупными приложениями.

	[https://www.radscan.com/nas/nas-links.html](https://www.radscan.com/nas/nas-links.html) || [nas](https://aur.archlinux.org/packages/nas/)

## Смотрите также

*   [MIDI](/index.php/MIDI_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MIDI (Русский)")
*   [Codecs](/index.php/Codecs_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Codecs (Русский)")
*   [Professional audio](/index.php/Pro_Audio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pro Audio (Русский)")
*   [PC speaker](/index.php/PC_speaker_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PC speaker (Русский)")