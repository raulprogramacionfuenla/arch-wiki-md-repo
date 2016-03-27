**Состояние перевода:** На этой странице представлен перевод статьи [PulseAudio/Troubleshooting](/index.php/PulseAudio/Troubleshooting "PulseAudio/Troubleshooting"). Дата последней синхронизации: 16 марта 2016‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=PulseAudio/Troubleshooting&diff=0&oldid=425976).

Смотрите основную статью [PulseAudio (Русский)](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PulseAudio (Русский)").

## Contents

*   [1 Звук](#.D0.97.D0.B2.D1.83.D0.BA)
    *   [1.1 Автоматический бесшумный режим](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B1.D0.B5.D1.81.D1.88.D1.83.D0.BC.D0.BD.D1.8B.D0.B9_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC)
    *   [1.2 Аудиоустройство с отключенным звуком](#.D0.90.D1.83.D0.B4.D0.B8.D0.BE.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE_.D1.81_.D0.BE.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.BC)
    *   [1.3 Output stuck muted while Master is toggled](#Output_stuck_muted_while_Master_is_toggled)
    *   [1.4 Приложение с отключенным звуком](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81_.D0.BE.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.BC)
    *   [1.5 Настройка громкости не работает должным образом](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B3.D1.80.D0.BE.D0.BC.D0.BA.D0.BE.D1.81.D1.82.D0.B8_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.B4.D0.BE.D0.BB.D0.B6.D0.BD.D1.8B.D0.BC_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.BE.D0.BC)
    *   [1.6 Громкость приложений меняется, когда регулируется Общая громкость](#.D0.93.D1.80.D0.BE.D0.BC.D0.BA.D0.BE.D1.81.D1.82.D1.8C_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BC.D0.B5.D0.BD.D1.8F.D0.B5.D1.82.D1.81.D1.8F.2C_.D0.BA.D0.BE.D0.B3.D0.B4.D0.B0_.D1.80.D0.B5.D0.B3.D1.83.D0.BB.D0.B8.D1.80.D1.83.D0.B5.D1.82.D1.81.D1.8F_.D0.9E.D0.B1.D1.89.D0.B0.D1.8F_.D0.B3.D1.80.D0.BE.D0.BC.D0.BA.D0.BE.D1.81.D1.82.D1.8C)
    *   [1.7 Звук становится каждый раз громче, как только запускается новое приложение](#.D0.97.D0.B2.D1.83.D0.BA_.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D1.81.D1.8F_.D0.BA.D0.B0.D0.B6.D0.B4.D1.8B.D0.B9_.D1.80.D0.B0.D0.B7_.D0.B3.D1.80.D0.BE.D0.BC.D1.87.D0.B5.2C_.D0.BA.D0.B0.D0.BA_.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BD.D0.BE.D0.B2.D0.BE.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [1.8 На звуковой карте M-Audio Audiophile 2 496 звук только Mono](#.D0.9D.D0.B0_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.B2.D0.BE.D0.B9_.D0.BA.D0.B0.D1.80.D1.82.D0.B5_M-Audio_Audiophile_2_496_.D0.B7.D0.B2.D1.83.D0.BA_.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_Mono)
    *   [1.9 Нет звука ниже определённого уровня](#.D0.9D.D0.B5.D1.82_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0_.D0.BD.D0.B8.D0.B6.D0.B5_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D1.91.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D1.83.D1.80.D0.BE.D0.B2.D0.BD.D1.8F)
    *   [1.10 Тихая громкость внутреннего микрофона](#.D0.A2.D0.B8.D1.85.D0.B0.D1.8F_.D0.B3.D1.80.D0.BE.D0.BC.D0.BA.D0.BE.D1.81.D1.82.D1.8C_.D0.B2.D0.BD.D1.83.D1.82.D1.80.D0.B5.D0.BD.D0.BD.D0.B5.D0.B3.D0.BE_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD.D0.B0)
    *   [1.11 Клиенты изменяют основной выход звука (т. е. переход громкости к 100% после запущенного приложения)](#.D0.9A.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D1.8B_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D1.8F.D1.8E.D1.82_.D0.BE.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D0.BE.D0.B9_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0_.28.D1.82._.D0.B5._.D0.BF.D0.B5.D1.80.D0.B5.D1.85.D0.BE.D0.B4_.D0.B3.D1.80.D0.BE.D0.BC.D0.BA.D0.BE.D1.81.D1.82.D0.B8_.D0.BA_100.25_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.89.D0.B5.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F.29)
    *   [1.12 Нет звука после возобновления из спящего режима](#.D0.9D.D0.B5.D1.82_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B2.D0.BE.D0.B7.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B8.D0.B7_.D1.81.D0.BF.D1.8F.D1.89.D0.B5.D0.B3.D0.BE_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B0)
    *   [1.13 Каналы ALSA отключены, когда наушники подсоединены/отсоединены неправильно](#.D0.9A.D0.B0.D0.BD.D0.B0.D0.BB.D1.8B_ALSA_.D0.BE.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D1.8B.2C_.D0.BA.D0.BE.D0.B3.D0.B4.D0.B0_.D0.BD.D0.B0.D1.83.D1.88.D0.BD.D0.B8.D0.BA.D0.B8_.D0.BF.D0.BE.D0.B4.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D1.8B.2F.D0.BE.D1.82.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D1.8B_.D0.BD.D0.B5.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE)
*   [2 Микрофон](#.D0.9C.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD)
    *   [2.1 PulseAudio не обнаруживает микрофон](#PulseAudio_.D0.BD.D0.B5_.D0.BE.D0.B1.D0.BD.D0.B0.D1.80.D1.83.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D1.82_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD)
    *   [2.2 PulseAudio использует неправильный микрофон](#PulseAudio_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D1.82_.D0.BD.D0.B5.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD)
    *   [2.3 Нет микрофона на ThinkPad T400/T500/T420](#.D0.9D.D0.B5.D1.82_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD.D0.B0_.D0.BD.D0.B0_ThinkPad_T400.2FT500.2FT420)
    *   [2.4 Нет микрофона на Acer Aspire One](#.D0.9D.D0.B5.D1.82_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD.D0.B0_.D0.BD.D0.B0_Acer_Aspire_One)
    *   [2.5 Статический шум в записи микрофона](#.D0.A1.D1.82.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D1.88.D1.83.D0.BC_.D0.B2_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D0.B8_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD.D0.B0)
        *   [2.5.1 Определение звуковых карт в системе (1/5)](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.B2.D1.8B.D1.85_.D0.BA.D0.B0.D1.80.D1.82_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B5_.281.2F5.29)
        *   [2.5.2 Определить частоту дискретизации звуковой карты (2/5)](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B8.D1.82.D1.8C_.D1.87.D0.B0.D1.81.D1.82.D0.BE.D1.82.D1.83_.D0.B4.D0.B8.D1.81.D0.BA.D1.80.D0.B5.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.B2.D0.BE.D0.B9_.D0.BA.D0.B0.D1.80.D1.82.D1.8B_.282.2F5.29)
        *   [2.5.3 Установка частоты дескритизации в настройках PulseAudio (3/5)](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.87.D0.B0.D1.81.D1.82.D0.BE.D1.82.D1.8B_.D0.B4.D0.B5.D1.81.D0.BA.D1.80.D0.B8.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D0.B8_.D0.B2_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0.D1.85_PulseAudio_.283.2F5.29)
        *   [2.5.4 Перезапустите PulseAudio для применения новых настроек (4/5)](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D1.82.D0.B8.D1.82.D0.B5_PulseAudio_.D0.B4.D0.BB.D1.8F_.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BD.D0.BE.D0.B2.D1.8B.D1.85_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA_.284.2F5.29)
        *   [2.5.5 Наконец, проверьте запись и её воспроизведение (5/5)](#.D0.9D.D0.B0.D0.BA.D0.BE.D0.BD.D0.B5.D1.86.2C_.D0.BF.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D1.8C.D1.82.D0.B5_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D1.8C_.D0.B8_.D0.B5.D1.91_.D0.B2.D0.BE.D1.81.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.285.2F5.29)
    *   [2.6 Нет микрофона в Steam или Skype с enable-remixing = no](#.D0.9D.D0.B5.D1.82_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD.D0.B0_.D0.B2_Steam_.D0.B8.D0.BB.D0.B8_Skype_.D1.81_enable-remixing_.3D_no)
    *   [2.7 Искажение микрофона из-за автоматической регулировки](#.D0.98.D1.81.D0.BA.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B8.D0.BA.D1.80.D0.BE.D1.84.D0.BE.D0.BD.D0.B0_.D0.B8.D0.B7-.D0.B7.D0.B0_.D0.B0.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B9_.D1.80.D0.B5.D0.B3.D1.83.D0.BB.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B8)
*   [3 Качество звука](#.D0.9A.D0.B0.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.BE_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0)
    *   [3.1 Включить отмену Эха/Шума](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D1.8C_.D0.BE.D1.82.D0.BC.D0.B5.D0.BD.D1.83_.D0.AD.D1.85.D0.B0.2F.D0.A8.D1.83.D0.BC.D0.B0)
    *   [3.2 Глюки, пропуски или потрескивания](#.D0.93.D0.BB.D1.8E.D0.BA.D0.B8.2C_.D0.BF.D1.80.D0.BE.D0.BF.D1.83.D1.81.D0.BA.D0.B8_.D0.B8.D0.BB.D0.B8_.D0.BF.D0.BE.D1.82.D1.80.D0.B5.D1.81.D0.BA.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [3.3 Определение номера фрагмента по умолчанию и размера буфера в PulseAudio](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.BE.D0.BC.D0.B5.D1.80.D0.B0_.D1.84.D1.80.D0.B0.D0.B3.D0.BC.D0.B5.D0.BD.D1.82.D0.B0_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E_.D0.B8_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.B0_.D0.B1.D1.83.D1.84.D0.B5.D1.80.D0.B0_.D0.B2_PulseAudio)
        *   [3.3.1 Поиск параметров вашего аудиоустройства (1/4)](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2_.D0.B2.D0.B0.D1.88.D0.B5.D0.B3.D0.BE_.D0.B0.D1.83.D0.B4.D0.B8.D0.BE.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0_.281.2F4.29)
        *   [3.3.2 Вычисление размера вашего фрагмента в миллисекундах и количества фрагментов (2/4)](#.D0.92.D1.8B.D1.87.D0.B8.D1.81.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.B0_.D0.B2.D0.B0.D1.88.D0.B5.D0.B3.D0.BE_.D1.84.D1.80.D0.B0.D0.B3.D0.BC.D0.B5.D0.BD.D1.82.D0.B0_.D0.B2_.D0.BC.D0.B8.D0.BB.D0.BB.D0.B8.D1.81.D0.B5.D0.BA.D1.83.D0.BD.D0.B4.D0.B0.D1.85_.D0.B8_.D0.BA.D0.BE.D0.BB.D0.B8.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.B0_.D1.84.D1.80.D0.B0.D0.B3.D0.BC.D0.B5.D0.BD.D1.82.D0.BE.D0.B2_.282.2F4.29)
        *   [3.3.3 Редактирование конфигурационного файла PulseAudio (3/4)](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.BE.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_PulseAudio_.283.2F4.29)
        *   [3.3.4 Перезапуск демона PulseAudio (4/4)](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B4.D0.B5.D0.BC.D0.BE.D0.BD.D0.B0_PulseAudio_.284.2F4.29)
    *   [3.4 Прерывистый звук с аналогового объемного звучания](#.D0.9F.D1.80.D0.B5.D1.80.D1.8B.D0.B2.D0.B8.D1.81.D1.82.D1.8B.D0.B9_.D0.B7.D0.B2.D1.83.D0.BA_.D1.81_.D0.B0.D0.BD.D0.B0.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D0.BE.D0.B1.D1.8A.D0.B5.D0.BC.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B7.D0.B2.D1.83.D1.87.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [3.5 Тормозит звук](#.D0.A2.D0.BE.D1.80.D0.BC.D0.BE.D0.B7.D0.B8.D1.82_.D0.B7.D0.B2.D1.83.D0.BA)
    *   [3.6 Искажённый звук](#.D0.98.D1.81.D0.BA.D0.B0.D0.B6.D1.91.D0.BD.D0.BD.D1.8B.D0.B9_.D0.B7.D0.B2.D1.83.D0.BA)
*   [4 Аппаратные средства и карты](#.D0.90.D0.BF.D0.BF.D0.B0.D1.80.D0.B0.D1.82.D0.BD.D1.8B.D0.B5_.D1.81.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B2.D0.B0_.D0.B8_.D0.BA.D0.B0.D1.80.D1.82.D1.8B)
    *   [4.1 Спустя некоторое время, при выключенном мониторе отсутствует звук на выходе HDMI](#.D0.A1.D0.BF.D1.83.D1.81.D1.82.D1.8F_.D0.BD.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D0.BE.D0.B5_.D0.B2.D1.80.D0.B5.D0.BC.D1.8F.2C_.D0.BF.D1.80.D0.B8_.D0.B2.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.BD.D0.BE.D0.BC_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.B5_.D0.BE.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D0.B5.D1.82_.D0.B7.D0.B2.D1.83.D0.BA_.D0.BD.D0.B0_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4.D0.B5_HDMI)
    *   [4.2 Нет карты](#.D0.9D.D0.B5.D1.82_.D0.BA.D0.B0.D1.80.D1.82.D1.8B)
    *   [4.3 Запуск приложения прерывает звук другого приложения](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D1.80.D0.B5.D1.80.D1.8B.D0.B2.D0.B0.D0.B5.D1.82_.D0.B7.D0.B2.D1.83.D0.BA_.D0.B4.D1.80.D1.83.D0.B3.D0.BE.D0.B3.D0.BE_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [4.4 Единственное указанное устройство является "фиктивным выходом" или вновь подключенные карты не определяются](#.D0.95.D0.B4.D0.B8.D0.BD.D1.81.D1.82.D0.B2.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D1.83.D0.BA.D0.B0.D0.B7.D0.B0.D0.BD.D0.BD.D0.BE.D0.B5_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE_.D1.8F.D0.B2.D0.BB.D1.8F.D0.B5.D1.82.D1.81.D1.8F_.22.D1.84.D0.B8.D0.BA.D1.82.D0.B8.D0.B2.D0.BD.D1.8B.D0.BC_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4.D0.BE.D0.BC.22_.D0.B8.D0.BB.D0.B8_.D0.B2.D0.BD.D0.BE.D0.B2.D1.8C_.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BA.D0.B0.D1.80.D1.82.D1.8B_.D0.BD.D0.B5_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D1.8F.D1.8E.D1.82.D1.81.D1.8F)
    *   [4.5 Не возможно выбрать устройства HDMI 5/7.1](#.D0.9D.D0.B5_.D0.B2.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE_.D0.B2.D1.8B.D0.B1.D1.80.D0.B0.D1.82.D1.8C_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0_HDMI_5.2F7.1)
    *   [4.6 Не удалось создать устройство входа: устройство приостановлено](#.D0.9D.D0.B5_.D1.83.D0.B4.D0.B0.D0.BB.D0.BE.D1.81.D1.8C_.D1.81.D0.BE.D0.B7.D0.B4.D0.B0.D1.82.D1.8C_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0:_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE_.D0.BF.D1.80.D0.B8.D0.BE.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BE)
    *   [4.7 Одновременный вывод на несколько звуковых карт / устройств](#.D0.9E.D0.B4.D0.BD.D0.BE.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B9_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4_.D0.BD.D0.B0_.D0.BD.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.B2.D1.8B.D1.85_.D0.BA.D0.B0.D1.80.D1.82_.2F_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2)
    *   [4.8 Одновременный вывод на несколько устройств вывода на одной звуковой карте не работает](#.D0.9E.D0.B4.D0.BD.D0.BE.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B9_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4_.D0.BD.D0.B0_.D0.BD.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B0_.D0.BD.D0.B0_.D0.BE.D0.B4.D0.BD.D0.BE.D0.B9_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.B2.D0.BE.D0.B9_.D0.BA.D0.B0.D1.80.D1.82.D0.B5_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82)
    *   [4.9 Некоторые профили, такие как SPDIF не задействованы по умолчанию на карте](#.D0.9D.D0.B5.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D1.84.D0.B8.D0.BB.D0.B8.2C_.D1.82.D0.B0.D0.BA.D0.B8.D0.B5_.D0.BA.D0.B0.D0.BA_SPDIF_.D0.BD.D0.B5_.D0.B7.D0.B0.D0.B4.D0.B5.D0.B9.D1.81.D1.82.D0.B2.D0.BE.D0.B2.D0.B0.D0.BD.D1.8B_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E_.D0.BD.D0.B0_.D0.BA.D0.B0.D1.80.D1.82.D0.B5)
*   [5 Bluetooth](#Bluetooth)
    *   [5.1 Отключение поддержки Bluetooth](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B8_Bluetooth)
    *   [5.2 Проблемы воспроизведения гарнитуры Bluetooth](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D0.B2.D0.BE.D1.81.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B3.D0.B0.D1.80.D0.BD.D0.B8.D1.82.D1.83.D1.80.D1.8B_Bluetooth)
    *   [5.3 Автоматическое переключение на Bluetooth или USB-гарнитуру](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B0_Bluetooth_.D0.B8.D0.BB.D0.B8_USB-.D0.B3.D0.B0.D1.80.D0.BD.D0.B8.D1.82.D1.83.D1.80.D1.83)
    *   [5.4 Устройство сопряжено, но не проигрывает звук](#.D0.A3.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE_.D1.81.D0.BE.D0.BF.D1.80.D1.8F.D0.B6.D0.B5.D0.BD.D0.BE.2C_.D0.BD.D0.BE_.D0.BD.D0.B5_.D0.BF.D1.80.D0.BE.D0.B8.D0.B3.D1.80.D1.8B.D0.B2.D0.B0.D0.B5.D1.82_.D0.B7.D0.B2.D1.83.D0.BA)
*   [6 Приложения](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [6.1 Содержащие Flash](#.D0.A1.D0.BE.D0.B4.D0.B5.D1.80.D0.B6.D0.B0.D1.89.D0.B8.D0.B5_Flash)
    *   [6.2 Ошибка с правами доступа](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.D1.81_.D0.BF.D1.80.D0.B0.D0.B2.D0.B0.D0.BC.D0.B8_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.B0)
    *   [6.3 Audacity](#Audacity)
*   [7 Другие проблемы](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B)
    *   [7.1 Плохой файл настроек](#.D0.9F.D0.BB.D0.BE.D1.85.D0.BE.D0.B9_.D1.84.D0.B0.D0.B9.D0.BB_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA)
    *   [7.2 Невозможно обновить настройки звукового устройства в pavucontrol](#.D0.9D.D0.B5.D0.B2.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D1.8C_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0_.D0.B2_pavucontrol)
    *   [7.3 Не удалось создать устройство вывода: устройство вывода приостановлено](#.D0.9D.D0.B5_.D1.83.D0.B4.D0.B0.D0.BB.D0.BE.D1.81.D1.8C_.D1.81.D0.BE.D0.B7.D0.B4.D0.B0.D1.82.D1.8C_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B0:_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B0_.D0.BF.D1.80.D0.B8.D0.BE.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BE)
    *   [7.4 Pulse переписывает настройки ALSA](#Pulse_.D0.BF.D0.B5.D1.80.D0.B5.D0.BF.D0.B8.D1.81.D1.8B.D0.B2.D0.B0.D0.B5.D1.82_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_ALSA)
    *   [7.5 Предотвращение перезагрузки Pulse, после того как процесс был убит (kill)](#.D0.9F.D1.80.D0.B5.D0.B4.D0.BE.D1.82.D0.B2.D1.80.D0.B0.D1.89.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8_Pulse.2C_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D1.82.D0.BE.D0.B3.D0.BE_.D0.BA.D0.B0.D0.BA_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81_.D0.B1.D1.8B.D0.BB_.D1.83.D0.B1.D0.B8.D1.82_.28kill.29)
    *   [7.6 Не удаётся запустить Демон](#.D0.9D.D0.B5_.D1.83.D0.B4.D0.B0.D1.91.D1.82.D1.81.D1.8F_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D1.82.D0.B8.D1.82.D1.8C_.D0.94.D0.B5.D0.BC.D0.BE.D0.BD)
        *   [7.6.1 Вывод статуса ошибок PulseAudio утилитами проверки](#.D0.92.D1.8B.D0.B2.D0.BE.D0.B4_.D1.81.D1.82.D0.B0.D1.82.D1.83.D1.81.D0.B0_.D0.BE.D1.88.D0.B8.D0.B1.D0.BE.D0.BA_PulseAudio_.D1.83.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D0.B0.D0.BC.D0.B8_.D0.BF.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B8)
    *   [7.7 Демон уже запущен](#.D0.94.D0.B5.D0.BC.D0.BE.D0.BD_.D1.83.D0.B6.D0.B5_.D0.B7.D0.B0.D0.BF.D1.83.D1.89.D0.B5.D0.BD)
    *   [7.8 Сабвуфер перестает работать после окончания каждой песни](#.D0.A1.D0.B0.D0.B1.D0.B2.D1.83.D1.84.D0.B5.D1.80_.D0.BF.D0.B5.D1.80.D0.B5.D1.81.D1.82.D0.B0.D0.B5.D1.82_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.82.D1.8C_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.BE.D0.BA.D0.BE.D0.BD.D1.87.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BA.D0.B0.D0.B6.D0.B4.D0.BE.D0.B9_.D0.BF.D0.B5.D1.81.D0.BD.D0.B8)
    *   [7.9 Невозможно выбрать настройку объемного звучания, кроме "Surround 4.0"](#.D0.9D.D0.B5.D0.B2.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE_.D0.B2.D1.8B.D0.B1.D1.80.D0.B0.D1.82.D1.8C_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D1.83_.D0.BE.D0.B1.D1.8A.D0.B5.D0.BC.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B7.D0.B2.D1.83.D1.87.D0.B0.D0.BD.D0.B8.D1.8F.2C_.D0.BA.D1.80.D0.BE.D0.BC.D0.B5_.22Surround_4.0.22)
    *   [7.10 Планировщик в реальном времени](#.D0.9F.D0.BB.D0.B0.D0.BD.D0.B8.D1.80.D0.BE.D0.B2.D1.89.D0.B8.D0.BA_.D0.B2_.D1.80.D0.B5.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.BC_.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.B8)
    *   [7.11 Ошибка pactl "неверный параметр" с отрицательным процентным аргументом](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_pactl_.22.D0.BD.D0.B5.D0.B2.D0.B5.D1.80.D0.BD.D1.8B.D0.B9_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.22_.D1.81_.D0.BE.D1.82.D1.80.D0.B8.D1.86.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.BC_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D0.BD.D1.82.D0.BD.D1.8B.D0.BC_.D0.B0.D1.80.D0.B3.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D0.BE.D0.BC)
    *   [7.12 Резервное устройство не определяется](#.D0.A0.D0.B5.D0.B7.D0.B5.D1.80.D0.B2.D0.BD.D0.BE.D0.B5_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE_.D0.BD.D0.B5_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D1.8F.D0.B5.D1.82.D1.81.D1.8F)

## Звук

Здесь Вы найдете некоторые подсказки по проблемам звука и почему Вы ничего не можете услышать.

### Автоматический бесшумный режим

Автоматический бесшумный режим может быть включен изначально. Его можно легко отключить с помощью `alsamixer`.

Для подробностей смотрите [http://superuser.com/questions/431079/how-to-disable-auto-mute-mode](http://superuser.com/questions/431079/how-to-disable-auto-mute-mode)

Для сохранения текущих настроек, как опций по умолчанию, выполните от имени суперпользователя (root) `alsactl store`

### Аудиоустройство с отключенным звуком

Если нет звука при использовании [ALSA](/index.php/ALSA "ALSA"), попытайтесь включить звуковую карту. Чтобы сделать это, запустите `alsamixer`, и убедитесь, что каждый столбец имеет под ним зелёное значение `00` (можно переключать путём нажатия `m`):

$ alsamixer-c 0

**Примечание:** alsamixer не скажет Вам, какое устройство вывода установлено как значение по умолчанию. Одна из возможных причин отсутствия звука после установки состоит в том, что PulseAudio обнаруживает неправильное устройство вывода как значение по умолчанию. Установите [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) и проверьте, существует ли какой-нибудь вывод на панели pavucontrol, например, при проигрывании файла *.wav*.

### Output stuck muted while Master is toggled

In setups with multiple outputs (e.g. 'Headphone' and 'Speaker') using plain amixer to toggle Master can trigger PulseAudio to mute the active output too, but it does not necessarily unmute it when Master is toggled back to be unmuted. To resolve this, amixer must have the device flag set to 'pulse':

```
$ amixer -D pulse sset Master toggle

```

This will cause amixer to ask PulseAudio to do the toggling rather than toggling it directly. Because of this, PulseAudio will correctly unmute Master as well as any applicable output.

### Приложение с отключенным звуком

Если у определенного приложения отключен звук, или он тихий, в то время как все остальные приложения в порядке. Это может произойти из-за индивидуальной настройки `sink-input`. Выполните с приложением, у которого нарушен звук:

```
$ pacmd list-sink-inputs

```

Найдите и запишите `index` соответствия `sink input`.`properties:` `application.name` и `application.process.binary`, среди прочего, должны помочь здесь. Убедитесь, что присутствуют нормальные настройки, в частности те `muted` и `volume`. Если у устройства вывода отключен звук, его можно включить:

```
$ pacmd set-sink-input-mute <index> false

```

Если нужна корректировка громкости, она может быть установлена на 100%:

```
$ pacmd set-sink-input-volume <index> 0x10000

```

**Примечание:** Если `pacmd` выдаёт `0 sink input(s)`, перепроверьте, что приложение воспроизводит звук. Если звук всё ещё отсутствует, проверьте, что другие приложения показывают как устройство вывода.

### Настройка громкости не работает должным образом

Проверьте: `/usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common`

Если громкость, кажется, не постепенно увеличивается/постепенно уменьшается должным образом используя `alsamixer` или `amixer`, это может быть связано с PulseAudio, имеющего большее число инкрементов (65537, чтобы быть точным). Попытайтесь использовать большие значения при изменении громкости (например, `amixer set Master 655+`).

### Громкость приложений меняется, когда регулируется Общая громкость

Это вызвано тем, что PulseAudio использует "плоскую регулировку громкости" (flat-volumes) по умолчанию, вместо относительной регулировки громкости, по сравнению с абсолютной общей регулировкой громкостью. Если это поведение вызывает неудобства, относительная громкость может быть включена путем отключения плоской громкости в файле настроек демона PulseAudio:

 `/etc/pulse/daemon.conf or ~/.config/pulse/daemon.conf` 
```
flat-volumes = no

```

и затем перезапустите PulseAudio выполнив:

```
$ pulseaudio -k
$ pulseaudio --start

```

### Звук становится каждый раз громче, как только запускается новое приложение

По-умолчанию, кажется, как будто изменение громкости в приложении меняет общую громкость системы, а не только соответствующего приложения. Следовательно, настройки приложения громкости на старте заставляют системную громкость "прыгать".

Исправьте это путем отключения "плоской громкости", как продемонстрировано в предыдущем разделе. Когда Pulse после нескольких секунд вернёт приложению "не изменять больше глобальную громкость", и установит собственный уровень громкости приложения.

**Примечание:** Ранее установленный и удаленный pulseaudio-equalizer может оставить настройки в `~/.config/pulse/default.pa` или `~/.pulse/default.pa`, которые также могут доставить неприятности увеличения звука. Закомментируйте эти настройки, при необходимости.

### На звуковой карте M-Audio Audiophile 2 496 звук только Mono

Добавьте следующее:

 `/etc/pulseaudio/default.pa` 
```
load-module module-alsa-sink sink_name=delta_out device=hw:M2496 format=s24le channels=10 channel_map=left,right,aux0,aux1,aux2,aux3,aux4,aux5,aux6,aux7
load-module module-alsa-source source_name=delta_in device=hw:M2496 format=s24le channels=12 channel_map=left,right,aux0,aux1,aux2,aux3,aux4,aux5,aux6,aux7,aux8,aux9
set-default-sink delta_out
set-default-source delta_in

```

### Нет звука ниже определённого уровня

Известная проблема (не исправление): [https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/223133](https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/223133)

Если звук не играет, когда громкость PulseAudio регулируется ниже определенного уровня, попробуйте установить `ignore_dB=1` в `/etc/pulse/default.pa`:

 `/etc/pulse/default.pa` 
```
load-module module-udev-detect ignore_dB=1

```

Однако следует помнить, что это может привести к ошибке предотвращения PulseAudio чтобы включить колонки, когда наушники или другие аудио устройства выключены.

### Тихая громкость внутреннего микрофона

Если у вас низкая громкость звука, на внутреннем микрофоне ноутбука, попытайтесь установить:

 `/etc/pulse/default.pa` 
```
set-source-volume 1 300000

```

### Клиенты изменяют основной выход звука (т. е. переход громкости к 100% после запущенного приложения)

Если изменение громкости в конкретных приложениях или просто запуск приложения изменяет громкость воспроизведения, это происходит скорее всего из-за режима "плоская громкость" в PulseAudio. Перед отключением, пользователи KDE должны попытаться снизить громкость их системы уведомлений в *System Settings -> Application and System Notifications -> Manage Notifications* ( *Системные настройки -> приложения и уведомлений системы -> Управление Уведомлениями* на вкладке *Настройки воспроизведения*), на что-то разумное. Тут не поможет изменение *звуков событий*, громкости в KMix или другом приложении громкости микшера. Это должно заставить режим "плоской громкости" работать как задумано, если он не работает, некоторые другие приложения, скорее всего, запрашивают громкость 100%, когда что-то воспроизводят. Если все остальное не помогает, вы можете попробовать отключить "плоскую громкость":

 `/etc/pulse/daemon.conf` 
```
flat-volumes = no

```

Затем перезапустите демон PulseAudio:

```
# pulseaudio -k
# pulseaudio --start

```

### Нет звука после возобновления из спящего режима

Если звук обычно работает, но не работает после спящего режима, попытайтесь "перезагрузить" PulseAudio путем выполнения:

```
$ /usr/bin/pasuspender /bin/true

```

Это лучше, чем убить, и перезапустить его (`pulseaudio -k` сопровождаемый `pulseaudio --start`), потому что это уже не повредит запущенные приложения.

Если вышеупомянутое действие решает Вашу проблему, Вы можете автоматизировать это путем создания файла службы systemd.

1\. Создайте шаблонный файл службы в `/etc/systemd/system/resume-fix-pulseaudio@.service`:

```
[Unit]
Description=Fix PulseAudio after resume from suspend
After=suspend.target

[Service]
User=%I
Type=oneshot
Environment="XDG_RUNTIME_DIR=/run/user/%U"
ExecStart=/usr/bin/pasuspender /bin/true

[Install]
WantedBy=suspend.target

```

2\. Включите его для своей учетной записи пользователя

```
# systemctl enable resume-fix-pulseaudio@Здесь_ваше_имя_пользователя.service

```

3\. Перезагрузите systemd

```
# systemctl --system daemon-reload

```

### Каналы ALSA отключены, когда наушники подсоединены/отсоединены неправильно

Когда вы отключаете наушники или подключаете их, звук остается отключенным в alsamixer на неправильном канале, из-за его установки на 0%, вы сможете исправить это, открыв `/etc/pulse/default.pa` и закомментировав строку:

```
load-module module-switch-on-port-available

```

## Микрофон

### PulseAudio не обнаруживает микрофон

Определите номер карты и номер устройства Вашего микрофона:

```
 $ arecord -l
 **** List of CAPTURE Hardware Devices ****
 card 0: PCH [HDA Intel PCH], device 0: ALC269VC Analog [ALC269VC Analog]
 Subdevices: 1/1
 Subdevice #0: subdevice #0

```

В нотации hw:CARD,DEVICE, Вы определили вышеупомянутое устройство как `hw:0,0`.

Затем отредактируйте {`/etc/pulse/default.pa` и вставьте строку `load-module`, определяющую Ваше устройство следующим образом:

```
  load-module module-alsa-source device=hw:0,0
  # the line above should be somewhere before the line below
 .ifexists module-udev-detect.so

```

Наконец, перезапустите pulseaudio для применения новых настроек:

```
  $ pulseaudio -k ; pulseaudio -D

```

Если все работает правильно, то Вы должны увидеть, что микрофон обнаруживается при выполнении `pavucontrol` (на вкладке `Input Devices` ).

### PulseAudio использует неправильный микрофон

Если PulseAudio использует неправильный микрофон, и изменение Устройства ввода данных с Pavucontrol не помогало, смотрите alsamixer. Кажется, что Pavucontrol не всегда устанавливает входной источник правильно.

```
$ alsamixer

```

Нажмите `F6` и выберите свою звуковую карту, например, HDA Intel. Теперь нажмите `F5` для отображения всех элементов. Попытайтесь найти элемент: `Input Source`. С помощью клавиш Вверх / Вниз вы можете изменить источник входного сигнала.

Теперь попробуйте, правильный ли микрофон используется для записи.

### Нет микрофона на ThinkPad T400/T500/T420

Выплните:

```
alsamixer -c 0

```

Включите звук и максимизируйте громкость "Internal Mic" (внутреннего микрофона).

После того, как вы увидите устройство с помощью:

```
arecord -l

```

Вам возможно нужно скорректировать настройки. Микрофон и аудиоразъем являются дуплексными. Установите настройки внутреннего аудио pavucontrol в *Analog Stereo Duplex* (*Аналоговому Дуплексу Стерео*).

### Нет микрофона на Acer Aspire One

Установите pavucontrol, отсоедините каналы микрофона и выключите левый на 0. Ссылка: [http://getsatisfaction.com/jolicloud/topics/deaf_internal_mic_on_acer_aspire_one#reply_2108048](http://getsatisfaction.com/jolicloud/topics/deaf_internal_mic_on_acer_aspire_one#reply_2108048)

### Статический шум в записи микрофона

Если мы получаем статический шум в записях Skype, gnome-sound-recorder, arecord, и т.д., то в этом случае частота дискретизации звуковой карты является неправильной. Именно поэтому в записях микрофона Linux существует статический шум. Для того чтобы это исправить, мы должны установить уровень выборки (sampling rate) в `/etc/pulse/daemon.conf` для звукового оборудования.

#### Определение звуковых карт в системе (1/5)

Для этого потребуются установленые и необходимые пакеты [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils):

 `$ arecord --list-devices` 
```

**** List of CAPTURE Hardware Devices ****
card 0: Intel [HDA Intel], device 0: ALC888 Analog [ALC888 Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 2: ALC888 Analog [ALC888 Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0

```

`hw:0,0` является звуковой картой.

#### Определить частоту дискретизации звуковой карты (2/5)

 `arecord -f dat -r 60000 -D hw:0,0 -d 5 test.wav` 
```
"Recording WAVE 'test.wav' : Signed 16 bit Little Endian, Rate 60000 Hz, Stereo
Warning: rate is not accurate (requested = 60000Hz, **got = 96000Hz**)
please, try the plug plugin
```

заметьте, `got = 96000 Гц`. Это максимальная частота дискретизации нашей карты.

#### Установка частоты дескритизации в настройках PulseAudio (3/5)

Уровень дескритизации, по умолчанию, в PulseAudio:

 `$ grep "default-sample-rate" /etc/pulse/daemon.conf`  `; default-sample-rate = 44100` 

`44100` отключен, и должен быть изменен на `96000`:

```
# sed 's/; default-sample-rate = 44100/default-sample-rate = 96000/g' -i /etc/pulse/daemon.conf

```

#### Перезапустите PulseAudio для применения новых настроек (4/5)

```
$ pulseaudio -k
$ pulseaudio --start

```

#### Наконец, проверьте запись и её воспроизведение (5/5)

Давайте запишем речь с помощью микрофона в течение, 10 секунд. Удостоверьтесь, что микрофон не отключен.

```
$ arecord -f cd -d 10 test-mic.wav

```

После 10 секунд, давайте проиграем запись:

```
$ aplay test-mic.wav

```

Теперь, надеюсь, больше нет никакого статического шума на записи с микрофона

### Нет микрофона в Steam или Skype с enable-remixing = no

Когда Вы устанавите `enable-remixing = no` в `/etc/pulse/daemon.conf`, Вы можете обнаружить, что Ваш микрофон перестал работать в определенных приложениях, как Skype или Steam. Это происходит потому, что эти приложения получают микрофон как моно, только потому что отключен remixing, Pulseaudio больше не будет делать «remixing» Вашего стереомикрофона в моно.

Чтобы исправить это, вы должны сказать PulseAudio, что сделать за вас:

1\. Найти имя источника

```
# pacmd list-sources

```

Пример вывода отредактирован для краткости, имя которое вам нужно, выделено жирным:

```
   index: 2
       name: <**alsa_input.pci-0000_00_14.2.analog-stereo**>
       driver: <module-alsa-card.c>
       flags: HARDWARE HW_MUTE_CTRL HW_VOLUME_CTRL DECIBEL_VOLUME LATENCY DYNAMIC_LATENCY

```

2\. Добавить правило переназначения в `/etc/pulse/default.pa`, используйте имя, которое Вы нашли предыдущей командой, здесь мы будем использовать **alsa_input.pci-0000_00_14.2.analog-stereo** в качестве примера:

 `/etc/pulse/default.pa` 
```
### Remap microphone to mono
load-module module-remap-source master=alsa_input.pci-0000_00_14.2.analog-stereo master_channel_map=front-left,front-right channels=2 channel_map=mono,mono

```

3\. Перезапустите Pulseaudio

```
# pulseaudio -k

```

**Примечание:** Pulseaudio может не запуститься, если Вы не вышли из программы, использовавшей микрофон (например, если Вы протестировали в Steam, прежде, чем изменить файл), тогда Вы должны выйти из приложения, и вручную запустить Pulseaudio

```
# pulseaudio --start

```

### Искажение микрофона из-за автоматической регулировки

Если громкость микрофона повышается автоматически и вызывает искажение звука, вы можете это исправить путем отключения импульса микрофона:

В `/usr/share/pulseaudio/alsa-mixer/paths/analog-input-internal-mic.conf` и `/usr/share/pulseaudio/alsa-mixer/paths/analog-input-mic.conf`,

*   Под `[Element Internal Mic Boost]` установите `volume` в `zero (ноль)`.
*   Под `[Element Int Mic Boost]` установите `volume` в `zero`.
*   Под `[Element Mic Boost]` установите `volume` в `zero`.

Затем перезапустите PulseAudio:

```
# pulseaudio -k

```

## Качество звука

### Включить отмену Эха/Шума

Arch не загружает по умолчанию модуль аннулирования эха Pulseaudio, поэтому, мы должны включить его `/etc/pulse/default.pa`. Сначала Вы можете проверить, пресутствует ли модуль с помощью `pacmd` и вводом `list-modules`. Если Вы не можете найти строку {`list-modules` Вы должны добавить

 `/etc/pulse/default.pa ` 
```
###  Включить отмену Эха/Шума
load-module module-echo-cancel

```

затем перезапустите Pulseaudio

```
pulseaudio -k
pulseaudio --start

```

и проверьте, активируется ли модуль, путем запуска `pavucontrol`. Под `Recoding` устройством ввода, должно показать `Echo-Cancel Source Stream from"`

### Глюки, пропуски или потрескивания

Более новая реализация звукового сервера PulseAudio использует звуковой планировщик на основе таймера, вместо традиционного подхода управления прерываниями.

Основанное на таймере планирование может представлять проблемы в некоторых драйверах ALSA. С другой стороны, другие драйверы могли бы глючить без него, проверьте и посмотрите что работает на вашей системе.

Для выключения основанного на таймере планирования добавьте `tsched=0` в `/etc/pulse/default.pa`:

 `/etc/pulse/default.pa`  `load-module module-udev-detect tsched=0` 

Затем перезапустите сервер PulseAudio:

```
pulseaudio -k
pulseaudio --start

```

Наоборот, для включения основанного на таймере планирования, если он уже не включен по умолчанию.

Если Вы используете Intel [IOMMU](https://en.wikipedia.org/wiki/IOMMU "wikipedia:IOMMU") и испытываете глюки и/или пропуски, добавьте `intel_iommu=igfx_off` к Вашей командной строке ядра.

Некоторым звуковым картам Intel использующим модуль `snd-hda-intel` нужны опции `vid=8086 pid=8ca0 snoop=0`. Для постоянной их установки создайте/измените следующий файл, включая строку ниже.

 `/etc/modprobe.d/sound.conf`  `options snd-hda-intel vid=8086 pid=8ca0 snoop=0` 

Сообщите о любых таких картах [PulseAudio Broken Sound Driver page](http://www.freedesktop.org/wiki/Software/PulseAudio/Backends/ALSA/BrokenDrivers/)

### Определение номера фрагмента по умолчанию и размера буфера в PulseAudio

#### Поиск параметров вашего аудиоустройства (1/4)

Чтобы выяснить настройки буфера звуковой карты, используйте следующую команду, пока не найдете правильную запись выходного канала:

 `$ pactl list sinks` 
```
Sink #1
	State: RUNNING
	Name: alsa_output.pci-0000_00_1b.0.analog-stereo
	Description: Built-in Audio Analog Stereo
	Driver: module-alsa-card.c
	Sample Specification: s16le 2ch 44100Hz
	Channel Map: front-left,front-right
	Owner Module: 7
	Mute: no
	Volume: front-left: 42600 /  65% / -11.22 dB,   front-right: 42600 /  65% / -11.22 dB
	        balance 0.00
	Base Volume: 65536 / 100% / 0.00 dB
	Monitor Source: alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
	Latency: 70662 usec, configured 85000 usec
	Flags: HARDWARE HW_MUTE_CTRL HW_VOLUME_CTRL DECIBEL_VOLUME LATENCY 
	Properties:
		alsa.resolution_bits = "16"
		device.api = "alsa"
		device.class = "sound"
		alsa.class = "generic"
		alsa.subclass = "generic-mix"
		alsa.name = "ALC283 Analog"
		alsa.id = "ALC283 Analog"
		alsa.subdevice = "0"
		alsa.subdevice_name = "subdevice #0"
		alsa.device = "0"
		alsa.card = "1"
		alsa.card_name = "HDA Intel PCH"
		alsa.long_card_name = "HDA Intel PCH at 0xe111c000 irq 43"
		alsa.driver_name = "snd_hda_intel"
		device.bus_path = "pci-0000:00:1b.0"
		sysfs.path = "/devices/pci0000:00/0000:00:1b.0/sound/card1"
		device.bus = "pci"
		device.vendor.id = "8086"
		device.vendor.name = "Intel Corporation"
		device.product.id = "9ca0"
		device.product.name = "Wildcat Point-LP High Definition Audio Controller"
		device.form_factor = "internal"
		device.string = "front:1"
		device.buffering.buffer_size = "352800"
		device.buffering.fragment_size = "176400"
		device.access_mode = "mmap+timer"
		device.profile.name = "analog-stereo"
		device.profile.description = "Analog Stereo"
		device.description = "Built-in Audio Analog Stereo"
		alsa.mixer_name = "Realtek ALC283"
		alsa.components = "HDA:10ec0283,10ec0283,00100003"
		module-udev-detect.discovered = "1"
		device.icon_name = "audio-card-pci"
	Ports:
		analog-output-speaker: Speakers (priority: 10000, not available)
		analog-output-headphones: Headphones (priority: 9000, available)
	Active Port: analog-output-headphones
	Formats:
		pcm
...

```

Обратите внимание на то, что значения `buffer_size` и `fragment_size` релевантны соответствующей звуковой карте.

#### Вычисление размера вашего фрагмента в миллисекундах и количества фрагментов (2/4)

Частота дискретизации и битовая глубина PulseAudio по умолчанию установлены на `44100Hz` @ `16 bits`.

При такой конфигурации нам нужен битрейт `44100`*`16` = `705600` битов в секунду. Для стерео - `1411200 bps`.

Давайте взглянем на параметры, которые мы нашли в предыдущем шаге:

```
device.buffering.buffer_size = "352800" => 352800/1411200 = 0.25 s = 250 ms
device.buffering.fragment_size = "176400" => 176400/1411200 = 0.125 s = 125 ms

```

#### Редактирование конфигурационного файла PulseAudio (3/4)

 `/etc/pulse/daemon.conf` 
```
; default-fragments = X
; default-fragment-size-msec = Y

```

В предыдущем шаге мы рассчитали размер фрагмента. Узнать количество фрагментов также просто: buffer_size/fragment_size. Ответ в нашем случае будет равен (`250/125`) `2`:

 `/etc/pulse/daemon.conf` 
```
; default-fragments = **2**
; default-fragment-size-msec = **125**
```

#### Перезапуск демона PulseAudio (4/4)

```
$ pulseaudio -k
$ pulseaudio --start

```

Для получения дополнительной информации смотрите: [тему на форуме Linux Mint](http://forums.linuxmint.com/viewtopic.php?f=42&t=44862)

### Прерывистый звук с аналогового объемного звучания

Канал низкочастотных эфектов (НЭ) не ремикширован по-умолчанию. Чтобы включить его, нужно изменить следующее в `/etc/pulse/daemon.conf`:

 `/etc/pulse/daemon.conf` 
```
enable-lfe-remixing = yes

```

### Тормозит звук

Эта проблема возникает из-за неправильного размера буфера. Сначала убедитесь, что переменные {ic|default-fragments}} и `default-fragment-size-msec` не установлены на нестандартные значения в файле `/etc/pulse/daemon.conf`. Если это не помогло, попробуйте установить эти переменные на следующие значения:

 `/etc/pulse/daemon.conf` 
```
default-fragments = 5
default-fragment-size-msec = 2
```

### Искажённый звук

Искажённый звук может быть вызван неправильно настроенной частотой дискретизации. Попробуйте следующие настройки:

 `/etc/pulse/daemon.conf`  `default-sample-rate = 48000` 

и перезапустите сервер PulseAudio.

Если искажённый звук возникает в приложениях, использующих [OpenAL](https://en.wikipedia.org/wiki/ru:OpenAL "wikipedia:ru:OpenAL"), поменяйте частоту дискретизации в `/etc/openal/alsoft.conf`:

 `/etc/openal/alsoft.conf`  `frequency = 48000` 

Установка PCM volume выше 0 dB может вызвать [клиппинг](https://en.wikipedia.org/wiki/ru:%D0%9A%D0%BB%D0%B8%D0%BF%D0%BF%D0%B8%D0%BD%D0%B3_(%D0%B0%D1%83%D0%B4%D0%B8%D0%BE) "wikipedia:ru:Клиппинг (аудио)"). Запуск `alsamixer` позволит вам обнаружить и исправить проблему. Обратите внимание, что ALSA не может [корректно экспортировать](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/PulseAudioStoleMyVolumes) информацию о dB в PulseAudio. Попробуйте следующее:

 `/etc/pulse/default.pa`  `load-module module-udev-detect ignore_dB=1` 

и перезапустите сервер PulseAudio. Смотрите также [#No sound below a volume cutoff](#No_sound_below_a_volume_cutoff).

## Аппаратные средства и карты

### Спустя некоторое время, при выключенном мониторе отсутствует звук на выходе HDMI

Монитор подключается через HDMI / DisplayPort, а аудио разъем подключен к разъему для наушников монитора, но PulseAudio настаивает на том, что он отключен:

 `pactl list sinks` 
```
...
hdmi-output-0: HDMI / DisplayPort (priority: 5900, not available)
...

```

Это приводит к отсутствию звука, из выхода HDMI. Чтобы это обойти, переключитесь на другой VT и обратно. Если это не сработает, попробуйте: выключить монитор, переключиться на другой VT, включить монитор, а затем обратно. Эта проблема была обнаружена пользователями ATI / Nvidia / Intel.

### Нет карты

Если PulseAudio запускается, а выполнение `pacmd list` говорит что нет карт, убедитесь что они не используются устройствами ALSA:

```
$ fuser -v /dev/snd/*
$ fuser -v /dev/dsp

```

Убедитесь, что все приложения, использующие файлы pcm или dspзакрыты перед перезапуском PulseAudio.

### Запуск приложения прерывает звук другого приложения

Если у вас есть проблемы с некоторыми приложениями (например Teamspeak, Mumble) прерывающих звук уже запущенных приложений (например Deadbeaf), вы можете решить эту проблему закомментировав строку `load-module module-role-cork` в `/etc/pulse/default.pa` как показано ниже:

 `/etc/pulse/default.pa` 
```
### Cork music/video streams when a phone stream is active
# load-module module-role-cork

```

Затем перезагрузите PulseAudio, используя обычную учетную запись пользователя

```
pulseaudio -k
pulseaudio --start

```

### Единственное указанное устройство является "фиктивным выходом" или вновь подключенные карты не определяются

Another reason is [FluidSynth](/index.php/FluidSynth "FluidSynth") conflicting with PulseAudio as discussed in [this thread](https://bbs.archlinux.org/viewtopic.php?id=154002). One solution is to remove the package [fluidsynth](https://www.archlinux.org/packages/?name=fluidsynth).

Alternatively you could modify the *fluidsynth* configuration file `/etc/conf.d/fluidsynth` and change the driver to PulseAudio, then restart *fluidsynth* and PulseAudio:

 `/etc/conf.d/fluidsynth` 
```
AUDIO_DRIVER=pulseaudio
OTHER_OPTS='-m alsa_seq-r 48000'
```

It is also possible there is an issue with logind giving permissions, see [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") for more information.

### Не возможно выбрать устройства HDMI 5/7.1

Если вы не можете выбрать каналы выхода 5/7.1 для работающего устройства HDMI, вам может помоч выключение "stream device reading" в `/etc/pulse/default.pa`.

Смотрите [#Резервное устройство не определяется](#.D0.A0.D0.B5.D0.B7.D0.B5.D1.80.D0.B2.D0.BD.D0.BE.D0.B5_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE_.D0.BD.D0.B5_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D1.8F.D0.B5.D1.82.D1.81.D1.8F).

### Не удалось создать устройство входа: устройство приостановлено

Если у вас нет вывода звука и получаете десятки ошибок связанных с зависанием устройства в вашем журнале `journalctl -b`, сделайте резервную копию, а затем удалите в своём домашнем каталоге папки Pulse:

```
$ rm -r ~/.pulse ~/.pulse-cookie ~/.config/pulse

```

### Одновременный вывод на несколько звуковых карт / устройств

Одновременный вывод двух различных устройств может быть очень полезным. Например, отправить звук на ваш A / V ресивер через HDMI выход видеокарты, и также отправить один и тот же звук через аналоговый выход вашей материнской платы встроенного аудио. Теперь это менее хлопотно, чем раньше (в этом примере, мы используем рабочий стол GNOME).

Используя [paprefs](https://www.archlinux.org/packages/?name=paprefs), просто выберите "Добавить устройство виртуального выхода для одновременного вывода на всех локальных звуковых картах (Add virtual output device for simultaneous output on all local sound cards)" из вкладки "Одновременный вывод (Simultaneous Output)" . Затем в "Настройках Звука" GNOME, выберите одновременный вывод, который вы только что создали.

Если это не сработает, попробуйте добавить следующее `~/.asoundrc`:

```
pcm.dsp {
   type plug
   slave.pcm "dmix"
}

```

**Совет:** Одновременный вывод также может быть достигнуто вручную с помощью alsamixer. Отключите пункт "автоматическое отключение звука (auto mute)", затем включите другие источники вывода которые хотите услышать, и увеличте их громкость.

### Одновременный вывод на несколько устройств вывода на одной звуковой карте не работает

Это будет полезно для пользователей, у которых несколько источников звука, и они хотят воспроизводить их на разных устройствах вывода/выходах. Пример того как это использовать: допустим вы слушаете музыку и общаетесь в голосовом чате, и хотите выводить музыку на колонки (в данном случае цифровой S/PDIF) а голос в наушники (Аналог).

Иногда, но не всегда, PulseAudio автоматически это обнаруживает. Если вы знаете что ваша звуковая карта может выводить звук на Аналоговый выход и S/PDIF, в то время как у PulseAudio нет этой опции в своих профилях на pavucontrol или veromix, то вам нужно будет создать файл настроек для вашей звуковой карты.

Вам нужно создать более подробный профиль для конкретной звуковой карты. Это, в основном, делается в два этапа.

*   Создать правило Udev для выбора PulseAudio, вашего специфичного файла настроек PulseAudio для звуковой карты
*   Создать актуальные настройки

Создать правило pulseadio udev.

**Примечание:** Этот пример только для Asus Xonar Essence STX. Читайте [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") чтобы узнать праивльные значения.

**Примечание:** Ваш файл настроек должен иметь меньшее число, чем исходное правило PulseAudio вступающее в силу.
 `/usr/lib/udev/rules.d/90-pulseaudio-Xonar-STX.rules` 
```
ACTION=="change", SUBSYSTEM=="sound", KERNEL=="card*", \
ATTRS{subsystem_vendor}=="0x1043", ATTRS{subsystem_device}=="0x835c", ENV{PULSE_PROFILE_SET}="asus-xonar-essence-stx.conf" 

```

Теперь создайте файл настроек. Если потрудиться, вы можете написать его с нуля и сделать его красивым. Однако можете воспользоватся файлом настроек по умолчанию, переименовать его, а затем добавить в свой профиль то что будет там работать. Это менее красиво, зато быстро.

Чтобы включить несколько устройств вывода для Asus Xonar Essence STX, нужно только добавить это.

**Примечание:** `asus-xonar-essence-stx.conf` также содержит все коды/инструкции из `default.conf`.
 `/usr/share/pulseaudio/alsa-mixer/profile-sets/asus-xonar-essence-stx.conf` 
```
[Profile analog-stereo+iec958-stereo]
description = Analog Stereo Duplex + Digital Stereo Output
input-mappings = analog-stereo
output-mappings = analog-stereo iec958-stereo
skip-probe = yes

```

Это будет авто-профилем Asus Xonar Essence STX с профилями по умолчанию и добавит свой собственный профиль, так что вы можете иметь несколько устройств вывода.

Вам нужно создать еще один профиль в файле настроек, если вы хотите получить такую же функциональность с выходом AC3 Digital 5.1.

[смотрите статью о профилях PulseAudio](http://www.freedesktop.org/wiki/Software/PulseAudio/Backends/ALSA/Profiles/)

### Некоторые профили, такие как SPDIF не задействованы по умолчанию на карте

Некоторые профили, такие как IEC-958 (т.е. S/PDIF) не могут быть задействованы на выбранном устройстве. Каждый раз когда система запускается, профиль карт будет заблокирован, и демон PulseAudio не может его выбрать. Вы должны добавить выбор профиля в ваш файл default.pa. Проверьте имя карты и профиль:

```
$ pacmd list-cards

```

Затем отредактируйте файл настроек, чтобы добавить профиль

 `~/.config/pulse/default.pa` 
```
## Замените на ваши имена карты и профиля, которые вы хотите активировать
set-card-profile alsa_card.pci-0000_00_1b.0 output:iec958-stereo+input:analog-stereo

```

Pulseaudio добавит этот профиль, в пул доступных профилей

## Bluetooth

### Отключение поддержки Bluetooth

Если вы не используете Bluetooth, вы можете обнаружить следующую ошибку в журнале:

```
bluez5-util.c: GetManagedObjects() failed: org.freedesktop.DBus.Error.ServiceUnknown: The name org.bluez was not provided by any .service files

```

Чтобы отключить поддержку Bluetooth в PulseAudio, убедитесь, что следующие строчки закомментированы в используемом файле конфигурации (`~/.config/pulse/default.pa` или `/etc/pulse/default.pa`):

 `~/.config/pulse/default.pa` 
```
### Automatically load driver modules for Bluetooth hardware
#.ifexists module-bluetooth-policy.so
#load-module module-bluetooth-policy
#.endif

#.ifexists module-bluetooth-discover.so
#load-module module-bluetooth-discover
#.endif

```

### Проблемы воспроизведения гарнитуры Bluetooth

Некоторые пользователи [сообщают](https://bbs.archlinux.org/viewtopic.php?id=117420) о больших задержках или даже отсутствии звука, когда по Bluetooth-соединению не передаются никакие данные. Это вызвано модулем `module-suspend-on-idle`, который автоматически приостанавливает устройства ввода/вывода при простое. Так как это может вызвать проблемы с гарнитурой, можно отключить соответствующий модуль.

Для отключения загрузки модуля `module-suspend-on-idle` закомментируйте следующую строчку в используемом файле конфигурации (`~/.config/pulse/default.pa` или `/etc/pulse/default.pa`):

 `~/.config/pulse/default.pa` 
```
### Automatically suspend sinks/sources that become idle for too long
#load-module module-suspend-on-idle

```

И перезагрузите PulseAudio для применения изменений.

### Автоматическое переключение на Bluetooth или USB-гарнитуру

Добавьте следующие строчки в файл конфигурации:

 `/etc/pulse/default.pa` 
```
# automatically switch to newly-connected devices
load-module module-switch-on-connect

```

### Устройство сопряжено, но не проигрывает звук

[Смотрите раздел в статье Bluetooth](/index.php/Bluetooth#My_device_is_paired_but_no_sound_is_played_from_it "Bluetooth")

Начиная с PulseAudio 2.99 и bluez 4.101, вы должны **избегать** использования интерфейса Socket. НЕ используйте:

 `/etc/bluetooth/audio.conf` 
```
[General]
Enable=Socket

```

Если вы имеете проблемы с A2DP и PA 2.99, убедитесь, что у вас установлена библиотека [sbc](https://www.archlinux.org/packages/?name=sbc).

## Приложения

### Содержащие Flash

Поскольку Adobe Flash напрямую не поддерживает PulseAudio, рекомендуется [настроить ALSA использовать виртуальную звуковую карту PulseAudio](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#ALSA "PulseAudio (Русский)").

Если звук Flash заикается, можете попробовать использовать Flash через ALSA напрямую. Подробно смотрите [ALSA/dmix без захвата аппаратного устройства](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#ALSA.2Fdmix_.D0.B1.D0.B5.D0.B7_.D0.B7.D0.B0.D1.85.D0.B2.D0.B0.D1.82.D0.B0_.D0.B0.D0.BF.D0.BF.D0.B0.D1.80.D0.B0.D1.82.D0.BD.D0.BE.D0.B3.D0.BE_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0 "PulseAudio (Русский)").

### Ошибка с правами доступа

 `pulseaudio --start` 
```
E: [autospawn] core-util.c: Failed to create secure directory (/run/user/1000/pulse): Operation not permitted
W: [autospawn] lock-autospawn.c: Cannot access autospawn lock.
E: [pulseaudio] main.c: Failed to acquire autospawn lock
```

Известные програмы меняют права доступа для `/run/user*user id*/pulse` когда используется [Polkit](/index.php/Polkit "Polkit"):

*   [sakis3g](https://aur.archlinux.org/packages/sakis3g/)

В качестве обходного пути можно использовать [gksu](https://www.archlinux.org/packages/?name=gksu) или [kdesu](https://www.archlinux.org/packages/?name=kdesu) в [desktop entry](/index.php/Desktop_entry "Desktop entry") или добавить `*username* ALL=NOPASSWD: /usr/bin/*program_name*` в [sudoers](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0 "Sudo (Русский)") для запуска [sudo](https://www.archlinux.org/packages/?name=sudo) или `gksudo` без запроса пароля. Другой способ лежит через раскомментирование и установки `daemonize = yes` в `/etc/pulse/daemon.conf`.
Также стоит посмотреть [эту ветку форума (англ)](https://bbs.archlinux.org/viewtopic.php?id=135955).

### Audacity

При запуске Audacity вы можете обнаружить, что ваши наушники не работаую. Это может быть потому, что Audacity пытается использовать их в качестве записывающего устройства. Чтобы исправить это, откройте Audacity, затем установите его записывающее устройство `pulse:Internal Mic:0`.

В некоторых случаях, воспроизведение может быть искажено, ускорятся , или зависть, как описано в [Audacity Wiki's Linux Issues page](http://wiki.audacityteam.org/wiki/Linux_Issues#ALSA_and_other_sound_systems).

Решение, предложенное на этой странице может работать: запустите Audacity с опцией:

```
$ env PULSE_LATENCY_MSEC=30 audacity

```

Если указанное выше решение, не решает эту проблему, то можно временно отключить pulseaudio, во время работы Audacity при помощи команды `pasuspender`:

```
$ pasuspender -- audacity

```

Затем, не забудьте выбрать соответствующие устройства ввода и вывода ALSA в Audacity.

Смотрите также [#Определение номера фрагмента по умолчанию и размера буфера в PulseAudio](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.BE.D0.BC.D0.B5.D1.80.D0.B0_.D1.84.D1.80.D0.B0.D0.B3.D0.BC.D0.B5.D0.BD.D1.82.D0.B0_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E_.D0.B8_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.B0_.D0.B1.D1.83.D1.84.D0.B5.D1.80.D0.B0_.D0.B2_PulseAudio).

## Другие проблемы

### Плохой файл настроек

Если после запуска PulseAudio в системе нету звука, возможно необходимо удалить содержимое папки `~/.config/pulse` и/или `~/.pulse`. PulseAudio автоматически создаст новые файлы настроек при своём следующем запуске.

### Невозможно обновить настройки звукового устройства в pavucontrol

[pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) представляет собой удобную утилиту с графическим интерфейсом для настройки PulseAudio. На вкладке 'Настройки', вы можете выбрать различные профили для каждого из ваших звуковых устройств, например: аналоговое стерео, цифровой выход (IEC958), HDMI 5.1 Surround и т.д.

Тем не менее, вы можете столкнуться с случаем, когда выбрать другой профиль для карты приведёт к сбою демона Pulse и "зависнет" автоматическое повторное включение без нового выбора. Если это происходит, используйте другой полезный инструмент с графическим интерфейсом, [paprefs](https://www.archlinux.org/packages/?name=paprefs), чтобы проверить на вкладке "Одновременный вывод" для виртуального "одновременного устройства". Если этот параметр активен (флажок установлен), то это будет препятствовать вам изменению профиля любой карты в pavucontrol. Снимите флажок этого параметра, а затем настройте свой профиль в pavucontrol до повторного включения одновременного вывода в paprefs.

### Не удалось создать устройство вывода: устройство вывода приостановлено

Если у вас нету звука, и вы получаете десятки ошибок связанных с приостановкой устройства вывода в вашем журнале `journalctl -b`, сначала создайте резервную копию, а потом удалите папки pulse в вашем домашнем каталоге:

```
$ rm -r ~/.pulse ~/.pulse-cookie ~/.config/pulse

```

### Pulse переписывает настройки ALSA

PulseAudio обычно переписывает настройки ALSA — например устанавливает alsamixer при загрузке, даже когда демон ALSA загружен. Так как нет иного способа избежать такого поведения, чтобы восстановить настройки ALSA после запуска PulseAudio. Добавьте следующую команду в `.xinitrc` или `.bash_profile` или другой файл [Автоматической загрузки](/index.php/Autostarting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Autostarting (Русский)"):

```
restore_alsa() {
 while [ -z "$(pidof pulseaudio)" ]; do
  sleep 0.5
 done
 alsactl -f /var/lib/alsa/asound.state restore 
}
restore_alsa &

```

### Предотвращение перезагрузки Pulse, после того как процесс был убит (kill)

Иногда вы можете временно отключить Pulse. Для того чтобы сделать это, вы должны предотвратить Pulse от повторного запуска, после того как процесс был убит.

 `~/.config/pulse/client.conf` 
```
# Disable autospawning the PulseAudio daemon
autospawn = no
```

### Не удаётся запустить Демон

Попробуйте сбросить PulseAudio:

```
$ rm -rf /tmp/pulse* ~/.pulse* ~/.config/pulse
$ pulseaudio -k
$ pulseaudio --start

```

*   Убедитесь, что параметры для устройств вывода настроены правильно.

*   Если вы настроили default.pa для загрузки и использования модулей OSS проверьте [lsof](https://www.archlinux.org/packages/?name=lsof) что устройство `/dev/dsp` не используется другим приложением.

*   Установите предпочтительный метод работы передискретизации. Используйте `pulseaudio --dump-resample-methods` чтобы увидеть список всех доступных методов ресэмплинга (resample) которые вы можете использовать.

*   Чтобы получить подробную информацию о недавно появившихся незаписанных ошибок или просто получить статус демона, используйте команду `pax11publish -d` и `pulseaudio -v` где `v` опция может быть использована для многократно установления подробности вывода журнала, равное `--log-level[=LEVEL]` опции где LEVEL от 0 до 4\. Смотрите раздел [#Вывод статуса ошибок PulseAudio утилитами проверки](#.D0.92.D1.8B.D0.B2.D0.BE.D0.B4_.D1.81.D1.82.D0.B0.D1.82.D1.83.D1.81.D0.B0_.D0.BE.D1.88.D0.B8.D0.B1.D0.BE.D0.BA_PulseAudio_.D1.83.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D0.B0.D0.BC.D0.B8_.D0.BF.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B8).

Для больших подробностей смотрите страницу справки [pax11publish](http://linux.die.net/man/1/pax11publish) и [pulseaudio](http://linux.die.net/man/1/pulseaudio).

#### Вывод статуса ошибок PulseAudio утилитами проверки

Если `pax11publish -d` показывает ошибку как:

```
N: [pulseaudio] main.c: User-configured server at "user", refusing to start/autospawn.

```

затем запустите команду `pax11publish -r` и будет хорошо если вы выйдите из системы и войдёте снова. Это всегда требуется при использовании LXDM, поскольку он не перезапускает сервер X при завершении сеанса; смотрите [LXDM#PulseAudio](/index.php/LXDM#PulseAudio "LXDM").

Если команда `pulseaudio -vvvv` показывает ошибку:

```
E: [pulseaudio] module-udev-detect.c: You apparently ran out of inotify watches, probably because Tracker/Beagle took them all away. I wished people would do their homework first and fix inotify before using it for watching whole directory trees which is something the current inotify is certainly not useful for. Please make sure to drop the Tracker/Beagle guys a line complaining about their broken use of inotify.

```

Эту проблему можно временно решить с помощью:

```
$ echo 100000 > /proc/sys/fs/inotify/max_user_watches

```

Для постоянного использования сохраните настройки в файл *99-sysctl.conf*:

 `/etc/sysctl.d/99-sysctl.conf` 
```
# Increase inotify max watchs per user
fs.inotify.max_user_watches = 100000
```

**Важно:** Это может привести к гораздо большему потреблению памяти ядром.

**Смотрите также**

*   [proc_sys_fs_inotify](http://www.linuxinsight.com/proc_sys_fs_inotify.html) and [dnotify, inotify](http://lwn.net/Articles/604686/)- more details about *inotify/max_user_watches*
*   [reasonable amount of inotify watches with Linux](http://stackoverflow.com/questions/535768/what-is-a-reasonable-amount-of-inotify-watches-with-linux?answertab=votes#tab-top)
*   [inotify](http://linux.die.net/man/7/inotify) - man page

### Демон уже запущен

В некоторых системах, PulseAudio может быть запущен несколько раз. В таком случае journalctl сообщит:

```
[pulseaudio] pid.c: Daemon already running.

```

Убедитесь в том, что используете только один метод автоматического запуска приложений. [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) содержит следующие файлы:

*   `/etc/X11/xinit/xinitrc.d/pulseaudio`
*   `/etc/xdg/autostart/pulseaudio.desktop`
*   `/etc/xdg/autostart/pulseaudio-kde.desktop`

Также проверьте пользовательские файлы и каталоги автозапуска, такие как [xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)"), `~/.config/autostart/` и т.п..

### Сабвуфер перестает работать после окончания каждой песни

Известные проблемы: [https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/494099](https://bugs.launchpad.net/ubuntu/+source/pulseaudio/+bug/494099)

Чтобы это исправить, необходимо изменить: `/etc/pulse/daemon.conf` и включить `enable-lfe-remixing` :

 `/etc/pulse/daemon.conf` 
```
enable-lfe-remixing = yes

```

### Невозможно выбрать настройку объемного звучания, кроме "Surround 4.0"

Если вам не удается установить 5.1-канальный вывод объемного звучания в pavucontrol, поскольку он показывает только "Analog Surround 4.0 Output", откройте микшер ALSA и измените настройку вывода на 6 каналов. Затем перезагрузите PulseAudio и pavucontrol покажет много вариантов.

### Планировщик в реальном времени

Если rtkit не работает, вы можете вручную настроить систему для запуска PulseAudio с планировщиком в реальном времени, который может помочь в производительности. Чтобы сделать это, добавьте следующие строки в `/etc/security/limits.conf`:

```
@pulse-rt - rtprio 9
@pulse-rt - nice -11

```

После этого вам нужно добавить пользователя в группу `pulse-rt`:

```
# gpasswd -a <user> pulse-rt

```

### Ошибка pactl "неверный параметр" с отрицательным процентным аргументом

Команды `pactl`, которые принимают отрицательные процентные аргументов, терпят крах с ошибкой 'недопустимый параметр/опция'. Используйте стандартную оболочку '--' псевдо аргумента отключите парсинг аргумента перед отрицательным элиментом. *Например* `pactl set-sink-volume 1 -- -5%`.

### Резервное устройство не определяется

По умолчанию PulseAudio не использует настоящее устройство. Вместо этого он использует ["резервный вариант"](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/DefaultDevice/), который применяется только к новым звуковым потокам. Это означает, что ранее запущенные приложения не зависят от вновь установленного резервного устройства.

[gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center), [mate-media](https://www.archlinux.org/packages/?name=mate-media) и [paswitch](https://aur.archlinux.org/packages/paswitch/) справятся с этим. Альтернативно:

1\. Переместите старые потоки вручную в [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) на новую звуковую карту.

2\. Остановить Pulse, стереть "stream-volumes" в `~/.config/pulse` и/или `~/.pulse` и перезапустить Pulse. Это также сбросит громкость у приложений.

3\. Отключите устройства чтения потока. Это может понадобиться если не хотите чтобы искались различные звуковые карты с различными приложениями.

 `/etc/pulse/default.pa` 
```
load-module module-stream-restore restore_device=false

```