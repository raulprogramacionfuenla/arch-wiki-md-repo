[Haskell](http://www.haskell.org) — чистый функциональный язык программирования общего назначения.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Компилятор](#.D0.9A.D0.BE.D0.BC.D0.BF.D0.B8.D0.BB.D1.8F.D1.82.D0.BE.D1.80)
*   [2 Проблемы со связыванием](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81.D0.BE_.D1.81.D0.B2.D1.8F.D0.B7.D1.8B.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC)
    *   [2.1 Статическое связывание](#.D0.A1.D1.82.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D1.81.D0.B2.D1.8F.D0.B7.D1.8B.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [2.2 Сборка статически связанных пакетов с помощью Cabal (без использования разделяемых библиотек)](#.D0.A1.D0.B1.D0.BE.D1.80.D0.BA.D0.B0_.D1.81.D1.82.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8_.D1.81.D0.B2.D1.8F.D0.B7.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_Cabal_.28.D0.B1.D0.B5.D0.B7_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D1.8F.D0.B5.D0.BC.D1.8B.D1.85_.D0.B1.D0.B8.D0.B1.D0.BB.D0.B8.D0.BE.D1.82.D0.B5.D0.BA.29)
    *   [2.3 Средства разработки Haskell](#.D0.A1.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B2.D0.B0_.D1.80.D0.B0.D0.B7.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.BA.D0.B8_Haskell)
*   [3 Управление пакетами Haskell](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B0.D0.BC.D0.B8_Haskell)
    *   [3.1 Плюсы / минусы различных методов](#.D0.9F.D0.BB.D1.8E.D1.81.D1.8B_.2F_.D0.BC.D0.B8.D0.BD.D1.83.D1.81.D1.8B_.D1.80.D0.B0.D0.B7.D0.BB.D0.B8.D1.87.D0.BD.D1.8B.D1.85_.D0.BC.D0.B5.D1.82.D0.BE.D0.B4.D0.BE.D0.B2)
    *   [3.2 Репозиторий ArchHaskell](#.D0.A0.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D0.B9_ArchHaskell)
    *   [3.3 cabal-install](#cabal-install)
        *   [3.3.1 Подготовка и $PATH](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8_.24PATH)
        *   [3.3.2 Установка пакетов user-wide](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2_user-wide)
        *   [3.3.3 Песочницы](#.D0.9F.D0.B5.D1.81.D0.BE.D1.87.D0.BD.D0.B8.D1.86.D1.8B)
        *   [3.3.4 Удаление пакетов](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
    *   [3.4 stack](#stack)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

### Компилятор

## Проблемы со связыванием

### Статическое связывание

### Сборка статически связанных пакетов с помощью Cabal (без использования разделяемых библиотек)

### Средства разработки Haskell

## Управление пакетами Haskell

### Плюсы / минусы различных методов

### Репозиторий ArchHaskell

### cabal-install

#### Подготовка и $PATH

#### Установка пакетов user-wide

#### Песочницы

#### Удаление пакетов

### stack

## Смотрите также