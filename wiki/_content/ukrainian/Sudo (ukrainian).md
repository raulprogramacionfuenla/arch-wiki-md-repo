## Contents

*   [1 Встановлення](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F)
*   [2 Ввімкнення sudo для користувачів](#.D0.92.D0.B2.D1.96.D0.BC.D0.BA.D0.BD.D0.B5.D0.BD.D0.BD.D1.8F_sudo_.D0.B4.D0.BB.D1.8F_.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D1.82.D1.83.D0.B2.D0.B0.D1.87.D1.96.D0.B2)
*   [3 Автодоповнення після sudo](#.D0.90.D0.B2.D1.82.D0.BE.D0.B4.D0.BE.D0.BF.D0.BE.D0.B2.D0.BD.D0.B5.D0.BD.D0.BD.D1.8F_.D0.BF.D1.96.D1.81.D0.BB.D1.8F_sudo)
*   [4 Час дії введеного пароля](#.D0.A7.D0.B0.D1.81_.D0.B4.D1.96.D1.97_.D0.B2.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BF.D0.B0.D1.80.D0.BE.D0.BB.D1.8F)
*   [5 Коротке узагальнення](#.D0.9A.D0.BE.D1.80.D0.BE.D1.82.D0.BA.D0.B5_.D1.83.D0.B7.D0.B0.D0.B3.D0.B0.D0.BB.D1.8C.D0.BD.D0.B5.D0.BD.D0.BD.D1.8F)
*   [6 Трохи розваг](#.D0.A2.D1.80.D0.BE.D1.85.D0.B8_.D1.80.D0.BE.D0.B7.D0.B2.D0.B0.D0.B3)
*   [7 Пароль root'а](#.D0.9F.D0.B0.D1.80.D0.BE.D0.BB.D1.8C_root.27.D0.B0)

## Встановлення

Для встановлення sudo введіть:

```
pacman -S sudo

```

## Ввімкнення sudo для користувачів

Для того, щоб додати користувача як користувача sudo ("sudoer"), відредагуйте /etc/sudoers у спеціальній сесії vi. Якщо ви не знаєте як користуватися vi, наберіть наступне:

```
EDITOR=nano visudo

```

(Ні в якому разі не редагуйте безпосередньо /etc/sudoers). Щоб дати користувачеві привілеї root'а, коли він вводить "sudo" перед командою, додайте такий рядок:

```
USER_NAME   ALL=(ALL) ALL

```

де USER_NAME - це ім'я користувача.

## Автодоповнення після sudo

За замовчуванням автодоповнення після команди sudo не працює. Наприклад, якщо в консолі написати:

```
fir

```

і натиснути клавішу Tab, то командна оболонка автоматично завершить команду:

```
firefox

```

А якщо додати в початок sudo:

```
sudo fir

```

і натиснути Tab, то нічого не відбудеться.

Щоб автодоповнення запрацювало, додайте в файл ~/.bashrc рядок:

```
complete -cf sudo

```

За аналогією можна включити автодоповнення після команд gksu (в середовищі GNOME) і kdesu (у середовищі KDE):

```
complete -cf sudo gksu kdesu

```

Або можна просто встановити пакет bash-completion (програмована автодополнялка) з репозиторію extra.

## Час дії введеного пароля

Можливо, ви хочете змінити проміжок часу, протягом якого sudo діє без введення пароля. Цього легко домогтися додавши в /etc/sudoers (visudo) наступне:

```
Defaults:arch timestamp_timeout=час(хв)

```

Це може виглядати так:

```
Defaults:arch timestamp_timeout=20

```

Де sudo для користувача arch діє без необхідності введення пароля протягом 20 хвилин.

**Note:** **Якщо ви хочете щоб sudo завжди вимагав введення пароля, зробіть timestamp_timeout рівним 0.**

## Коротке узагальнення

Підводячи підсумок, наступні пункти будуть корисні всім (USER_NAME - ім'я користувача):

```
1\. pacman -S sudo
2\. додати "USER_NAME   ALL=(ALL) ALL" e /etc/sudoers
3\. додати "complete -cf sudo" у /home/ІМ'Я_КОРИСТУВАЧА/.bashrc

```

## Трохи розваг

sudo може лаятися на вас кожен раз, коли ви вводите неправильний пароль, замість того щоб просто виводити повідомлення "Sorry, try again". Для включення цього "​​пасхального яйця":

```
# sudo visudo

```

Знайдіть розділ Defaults line (прибл. рядок 18) і додайте "insults" через кому, якщо там вже щось є. У підсумку це може виглядати так:

```
#Defaults specification
Defaults insults

```

**Note:** **Для перевірки наберіть sudo-K, щоб закінчити поточну сесію і дозволити sudo запитати пароль знову**

## Пароль root'а

Якщо вам потрібно sudo, наприклад для makepkg, але ви не хочете ризикувати безпекою, ви можете налаштувати sudo питати пароль root замість пароля користувача. Додайте "rootpw" до рядка Defaults:

```
 Defaults timestamp_timeout=0,rootpw

```