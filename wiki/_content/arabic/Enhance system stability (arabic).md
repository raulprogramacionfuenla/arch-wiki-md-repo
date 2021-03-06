الهدف من هذا المقال هو تقديم تلميحات حول كيفية جعل نظام آرتش لينوكس مستقراً قدر الإمكان، وعلى الرغم من أن مطوري آرتش والأعضاء الموثوقين يعملون بِجِّد لتقديم حزم عالية الجودة والمحافظة على نظام الإصدار المتدحرج لآرتش والتحديثات السريعة للحزم إلا إن نظام آرتش قد يكون غير مناسب للمهمات الحرجة أو للاستخدام في بيئة الإنتاج التجاري.

لكن تبقى أرتش توزيعة مستقرة نظراً لالتزامها ببساطة التكوين إضافة إلى الدورة السريعة لعملية التبليغ عن العلل/إصلاح العلل، وأيضاً استخدام أكواد مصدرية من دون باتشات للبرامج الخارجية upstream، وباتباع النصائح المقدمة أدناه في إعداد آرتش والإشراف عليه سيحصل المستخدم على نظام مستقر جداً، كما أن النصائح المقدمة ستُسَهِّل من عملية صيانة النظام في حال مواجهة أعطال كبيرة.

ما هو مدى الاستقرار الذي سيحققه نظام آرتش؟ هناك الكثير من التقارير في منتديات آرتش عن مديري أنظمة خبراء يستخدمون آرتش في مُخَدِّمات خاصة بالإنتاج، موقع Archlinux.org هو مثال عن هذا الأمر أما على صعيد الحواسيب الشخصية فإن التثبيت الصحيح لآرتش يقدم استقراراً ممتازاً.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 إعداد آرتش](#إعداد_آرتش)
    *   [1.1 تلميحات محددة خاصة بآرتش](#تلميحات_محددة_خاصة_بآرتش)
        *   [1.1.1 أنشئ قسم كبير لـمجلد /var وحافظ على الحزم القديمة](#أنشئ_قسم_كبير_لـمجلد_/var_وحافظ_على_الحزم_القديمة)
        *   [1.1.2 اختر التكوينات التي يُنصح بها](#اختر_التكوينات_التي_يُنصح_بها)
        *   [1.1.3 كن حذراً عند استخدام الحزم غير الرسمية أو التي لم تُختبر جيداً](#كن_حذراً_عند_استخدام_الحزم_غير_الرسمية_أو_التي_لم_تُختبر_جيداً)
        *   [1.1.4 قم باستخدام مرايا حديثة up-to-date](#قم_باستخدام_مرايا_حديثة_up-to-date)
        *   [1.1.5 تجنب الحزم قيد التطوير](#تجنب_الحزم_قيد_التطوير)
        *   [1.1.6 ثَبِّت حزمة linux-lts](#ثَبِّت_حزمة_linux-lts)
    *   [1.2 أفضل الممارسات العامة](#أفضل_الممارسات_العامة)
        *   [1.2.1 استخدم مدير الحزم لتثبيت البرمجيات](#استخدم_مدير_الحزم_لتثبيت_البرمجيات)
        *   [1.2.2 استخدم الحزم التي أثبتت إمكانياتها](#استخدم_الحزم_التي_أثبتت_إمكانياتها)
        *   [1.2.3 اختر التعريفات مفتوحة المصدر](#اختر_التعريفات_مفتوحة_المصدر)
*   [2 متابعة آرتش](#متابعة_آرتش)
    *   [2.1 تلميحات محددة في آرتش](#تلميحات_محددة_في_آرتش)
        *   [2.1.1 قم بترقية النظام على فترات معتدلة](#قم_بترقية_النظام_على_فترات_معتدلة)
        *   [2.1.2 إقرأ قبل القيام بترقية النظام](#إقرأ_قبل_القيام_بترقية_النظام)
        *   [2.1.3 استجب إلى التنبيهات التي تظهر أثناء الترقية](#استجب_إلى_التنبيهات_التي_تظهر_أثناء_الترقية)
        *   [2.1.4 تعامل بسرعة مع ملفات .pacnew و .pacsave و .pacorig](#تعامل_بسرعة_مع_ملفات_.pacnew_و_.pacsave_و_.pacorig)
        *   [2.1.5 خذ بعين الاعتبار استخدام Pacmatic](#خذ_بعين_الاعتبار_استخدام_Pacmatic)
        *   [2.1.6 تجنب بعض الأوامر المعينة في pacman](#تجنب_بعض_الأوامر_المعينة_في_pacman)
        *   [2.1.7 تراجع عن ترقية الحزمة التي تسبب عدم الاستقرار](#تراجع_عن_ترقية_الحزمة_التي_تسبب_عدم_الاستقرار)
        *   [2.1.8 قم بأخذ قائمة احتياطية بالحزم المثبتة بانتظام](#قم_بأخذ_قائمة_احتياطية_بالحزم_المثبتة_بانتظام)
        *   [2.1.9 خذ نسخة احتياطية من قاعدة بيانات pacman بانتظام](#خذ_نسخة_احتياطية_من_قاعدة_بيانات_pacman_بانتظام)
            *   [2.1.9.1 أتمتة Systemd](#أتمتة_Systemd)
    *   [2.2 أفضل الممارسات العامة](#أفضل_الممارسات_العامة_2)
        *   [2.2.1 اشترك بتنبيهات NVD/CVE وقم بالترقية فقط عند ظهور تنبيه أمني](#اشترك_بتنبيهات_NVD/CVE_وقم_بالترقية_فقط_عند_ظهور_تنبيه_أمني)
        *   [2.2.2 اختبر التحديثات على نظام آخر](#اختبر_التحديثات_على_نظام_آخر)
        *   [2.2.3 دائماً خذ نسخة احتياطية من ملفات التكوين قبل التعديل عليها](#دائماً_خذ_نسخة_احتياطية_من_ملفات_التكوين_قبل_التعديل_عليها)
        *   [2.2.4 خذ نسخة احتياطية من مجلدات /etc و /home و /srv و /var في فترات منتظمة](#خذ_نسخة_احتياطية_من_مجلدات_/etc_و_/home_و_/srv_و_/var_في_فترات_منتظمة)

## إعداد آرتش

عند تثبيت وتكوين installing and configuring آرتش لينوكس لأول مرة فإن أمام المستخدم العديد من الخيارات الخاصة بالتكوين والبرامج والتعريفات، هذه الخيارات ستؤثر في درجة استقرار النظام.

### تلميحات محددة خاصة بآرتش

#### أنشئ قسم كبير لـمجلد /var وحافظ على الحزم القديمة

أثناء عملية التثبيت وعند مرحلة إعداد الأقسام partitions دائماً قم بحجز قسم كبير ومنفصل لمجلد /var، يجب أن تكون مساحة هذا القسم من 6 إلى 8 غيغابايت (يجب حجز مساحة أكبر للمُخدِّمات)، يقوم مدير الحزم Pacman بأرشفة جميع الحزم التي ثُبِّتَت على النظام في المسار /var/cache/pacman/pkg والذي يتطلب كمية كبيرة من مساحة التخزين، الحفاظ على هذه الحزم أمر مفيد في حال تسببت عملية ترقية الحزمة الحالية في عدم استقرار النظام، حيث تتم عملية خفض downgrade إلى حزمة مؤرشفة أقدم، قم بالاطلاع على [#Revert package upgrades that cause instability](#Revert_package_upgrades_that_cause_instability).

#### اختر التكوينات التي يُنصح بها

في الوثائق المفصلة الخاصة بتثبيت وتكوين آرتش لينوكس غالباً ما تجد أكثر من طريقة لإعداد جانب معين من النظام، دائماً قم باختيار الطريقة الافتراضية التي ينصح بها عند إعداد النظام، فهذه الطريقة تعكس أفضل الممارسات وتُحقق الاستقرار الأمثل للنظام وتُسَهِّل من عملية صيانته.

#### كن حذراً عند استخدام الحزم غير الرسمية أو التي لم تُختبر جيداً

تجنب استخدام أي حزمة من مستودع الاختبار testing أو أي حزمة خارجية قيد الاختبار، فهذه الحزم التجريبية خاصة بالتطوير والاختبار وهي غير مناسبة للأنظمة المستقرة.

كن حذراً عند تثبيت حزم من مستودع AUR، غالبية الحزم المتواجدة في AUR قٌدِّمَت من قِبَل مستخدمين وبالتالي فقد تكون مُحَزَّمة بغير طريقة التحزيم المعيارية الخاصة بالمستودعات الرسمية، دائماً تحقق من خلو ملفات البناء PKGBUILD الخاصة بالحزمة من أي إشارات أو أخطاء أو أكواد خبيثة قبل الشروع في بناء الحزمة وتثبيتها.

كن حذراً عند استخدام أدوات [AUR helpers](/index.php/AUR_helpers "AUR helpers") التي تعمل على تبسيط عملية تثبيت الحزم من AUR بشكل كبير، والتي قد تبني وتُثَبِّت حزماً تحتوي على ملفات بناء PKGBUILD خبيثة ومشوهة، يتوجب عليك **دائماً** أن تتفحص سلامة ملفات PKGBUILD قبل الشروع في بنائها و/أو تثبيتها.

أخيراً، فإنه من غير الحكمة أبداً أن تُشغِّل أية أدوات [AUR helpers](/index.php/AUR_helpers "AUR helpers") أو أن تُنفذ الأمر [makepkg](/index.php/Makepkg "Makepkg") بصلاحيات المستخدم الجذر.

قم باستخدام مستودعات طرف ثالث فقط عند الضرورة أو عندما تعرف ما الذي تقوم به، دائماً استخدم مستودع طرف ثالث من مصدر موثوق.

#### قم باستخدام مرايا حديثة up-to-date

استخدم المرايا التي تُحدَّث دوماً بالنسخ الأخيرة من الحزم من مُخَدِّم FTP الرئيسي لآرتش، راجع [Mirror Status webpage](https://www.archlinux.org/mirrors/status/) للتأكد من أن المرايا التي قمت باختيارها حديثة up to date، باستخدامك للمرايا المحدَّثة مؤخراً أنت تضمن بأن نظامك سيحوي دائماً على أحدث النسخ المتوفرة من الحزم.

أيضاً قم بتعديل قائمة المرايا في الملف `/etc/pacman.d` وذلك بوضع المرايا المحلية (المرايا المتواجدة ضمن بلدك أو منطقك الجغرافية) في أعلى القائمة، اطلع على [Enabling your favorite mirror](/index.php/Mirrors#Enabling_your_favorite_mirror "Mirrors") لمزيد من التفاصيل، وأيضاً اطلع على عملية تثبيت سكربت [rankmirrors](/index.php/Mirrors#List_by_speed "Mirrors") لتفعيل المرايا الأسرع، هذه الخطوات ستضمن لك أسرع المرايا وأكثرها موثوقيةً.

بعد تغيير المرايا المستخدمة للتحديث قم بالتأكد من أن نظامك يعمل على آخر تحديث عن طريق تنفيذ الأمر -Syu.

#### تجنب الحزم قيد التطوير

لمنع الأعطال الخطيرة في نظامك لا تقم بتثبيت أي حزمة لاتزال قيد التطوير والتي عادة ستجدها في مستودع AUR وفي بعض الأحيان في مستودع community، هذه الحزم تُؤخذ مباشرة من أفرع تطوير البرامج الخارجية وعادة ما يضاف أحد الكلمات التالية على اسم الحزمة: dev، devel، svn، cvs، git، hg، bzr أو darcs.

وعلى وجه الخصوص تجنب تثبيت أي نسخة قيد التطوير عند تثبيت حزم أساسية في النظام مثل النواة أوglibc.

إذا كنت تقوم ببناء حزمة معدلة باستخدام makepkg تحقق من أن ملفات البناء PKGBUILD تتبع معيار [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards") ومتضمنة لـ provides array، استخدم namcap للتحقق من ملف .tar.gz أو PKGBUILD النهائي.

#### ثَبِّت حزمة linux-lts

حزمة [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) عبارة عن حزمة بديلة لنواة آرتش مرتكزة على نواة لينوكس 3.0 ومتوفرة في مستودع [core]، هذه النسخة الخاصة من النواة تتمتع بدعم طويل المدى **l**ong-**t**erm **s**upport (LTS) من مصدرها، بما فيه إصلاحات أمنية وبعض المنافذ الخلفية الخاصة بالخصوصية، كما أنها مفيدة خصوصاً لمستخدمي آرتش الذين يطمحون لاستخدام مثل هذه النواة على مُخدِّم أو للذين يريدون العودة إلى النواة الأقدم في حال أن النواة الجديدة سببت مشاكل.

لجعل هذه النواة متاحة للاختيار أثناء الإقلاع يتوجب عليك تحديث ملف إعدادت مُحَمِّل الإقلاع، على سبيل المثال إذا كنت تستخدم [Syslinux](/index.php/Syslinux "Syslinux") فيجب عليك تعديل ملف `/boot/syslinux/syslinux.cfg` بإعادة تكرار نفس المدخلات باستثناء استخدام `vmlinuz-linux-lts` و `initramfs-linux-lts.img`، أما في حالة [GRUB](/index.php/GRUB "GRUB") فإن الطريقة التي ينصح بها هي أن إعادة توليد ملف .cfg تلقائياً [re-generate the .cfg](/index.php/GRUB#Generate_GRUB2_BIOS_Config_file "GRUB").

البعض يُفضل تثبيت حزمة [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) بالإضافة إلى الحزمة الاعتيادية [linux](https://www.archlinux.org/packages/?name=linux) وتعديل مدخلات Fallback لاستعمال نواة الدعم الطويل LTS.

### أفضل الممارسات العامة

#### استخدم مدير الحزم لتثبيت البرمجيات

مدير الحزم (في آرتش: [pacman](/index.php/Pacman "Pacman")) يعمل أفضل منك بكثير في تتبع الملفات، عند تثبيتك أشياءً بنفسك فإنك **سوف** تنسى ما فعلته عاجلاً أم آجلاً مثل في أي مسار قمت بالتثبيت أو هل قمت بتثبيت أشياء متعارضة أو قد تكون قمت بالتثبيت في أماكن خاطئة .. إلخ.

إذا أخذنا الاستقرار بعين الاعتبار فيجب عليك تجنب الحزم والبرمجيات غير المدعومة، لكن في حال أنك تحتاج إلى هذه الحزم فإن بناء الحزمة أفضل من القيام بالتجميع والتثبيت يدوياً.

يجب عليك أيضاً أن تُعطَِل الأمر make install في المسار /root/.bashrc (والذي يكون نموذجي في التسبب بكل المشاكل):

```
 make() {
   [ "$1" == 'install' ] &&
     echo -e "WARNING:
DON'T INSTALL SOFTWARE MANUALLY
DON'T USE unset make TO OVERRIDE" &&
     echo "Tip: It's easy to make own custom package see: man PKGBUILD makepkg" &&
     return 1;
   /usr/bin/make $@;
 }

```

#### استخدم الحزم التي أثبتت إمكانياتها

ثَبِّت البرمجيات الناضجة التي أثبتت قدراتها وإمكانياتها وتجنب البرمجيات "cutting edge" التي ما تزال غير مستقرة buggy، حاول تجنب تثبيت النسخ "point-oh" والتي تعرف أيضاً باسم x.y.0، على سبيل المثال بدلاً من تثبيت Foobar 2.5.0 انتظر حتى تتوفر النسخة Foobar 2.5.1، لا تنشر البرمجيات المطورة حديثاً حتى تَثبُت موثوقيتها، على سبيل المثال النسخ المبكرة من PulseAudio كانت غير جديرة بالثقة، المستخدمون المهتمون بالاستقرار العالي قاموا باستخدام نظام الصوت ALSA بدلاً منه، وأخيراً قم باستخدام البرمجيات التي لديها مجتمع تطوير قوي ونشط.

#### اختر التعريفات مفتوحة المصدر

كلما أمكن لك ذلك استخدم تعريفات مفتوحة المصدر، حاول تجنب التعريفات المملوكة، في معظم الأحيان فإن التعريفات مفتوحة المصدر أكثر استقراراً وموثوقية من التعريفات المملوكة، العلل التي تصيب التعريفات مفتوحة المصدر يتم إصلاحها بشكل أسهل وأسرع، في حين أن التعريفات المملوكة من الممكن أن تقدم قدرات وميزات أكثر لكن هذا الأمر سيكون على حساب الاستقرار، لتجنب هذا المأزق اختر قطع العتاد hardware التي يتوفر لها تعريفات مفتوحة المصدر مدعومة بكامل المزايا، يمكنك الحصول على معلومات عن قطع العتاد التي لها تعريفات مفتوحة المصدر من الرابط [linux-drivers.org](http://www.linux-drivers.org/).

## متابعة آرتش

بالإضافة إلى ضبط آرتش من أجل الاستقرار هناك خطوات يمكن للمستخدم أن يتبعها خلال المتابعة والإشراف والتي تزيد من الاستقرار، الانتباه إلى بعض تفاصيل SysAdmin سوف يساعد في التأكد من استمرار صلابة النظام.

### تلميحات محددة في آرتش

#### قم بترقية النظام على فترات معتدلة

العديد من مستخدمي آرتش يقومون بالترقية باستمرار حتى أنهم يقومون بالترقية يومياً بواسطة الأمر `pacman -Syu`، ومع أن الترقية بشكل متكرر غير ضرورية إلا أنه يجب على المستخدم أن يقوم بالترقية كل فترة لكي يحصل على آخر إصلاحات العلل والتحديثات الأمنية، الترقية الأسبوعية أو النصف أسبوعية هي فكرة جيدة.

إذا كان هناك حزم من مستودع AUR مثبتة على النظام فقم بترقيتها بانتباه.

#### إقرأ قبل القيام بترقية النظام

قبل ترقية آرتش قم بقراءة آخر [أخبار آرتش](https://www.archlinux.org/news/) لمعرفة ما إذا كان هناك أي برمجيات أساسية أو تغييرات تكوينية في الحزم الأخيرة، قبل ترقية البرمجيات الرئيسية مثل النواة أو خادم xorg أو glibc إلى إصدار أحدث ألقي نظرة على المنتدى المناسب [webforum](https://bbs.archlinux.org/) لكي تعرف ما إذا كان هناك أي مشاكل تم الإبلاغ عنها.

#### استجب إلى التنبيهات التي تظهر أثناء الترقية

أثناء ترقية النظام انتبه إلى التنبيهات الصادرة عن مدير الحزم Pacman، إذا طُلب منك أي إجراءات إضافية فاستجب فوراً، إذا كان التنبيه مُربك فابحث في المنتديات والمواضيع الإخبارية الأخيرة لكي تحصل على المزيد من الإرشادات المُفَصَّلة.

#### تعامل بسرعة مع ملفات .pacnew و .pacsave و .pacorig

عندما يقوم pacman بحذف حزمة تملك ملف تكوين فإنه يقوم بإنشاء نسخة احتياطية من ملف التكوين ويضيف عليه اللاحقة .pacsave، كذلك عندما يقوم pacman بترقية حزمة تتضمن ملف تكوين جديد أُنشئ من قبل المطور ويختلف عن ملف التكوين الحالي المُثَبَّت فإن pacman يقوم بإنشاء ملف تكوين باللاحقة .pacnew وأحياناً وتحت ظروف خاصة يتم إنشاء ملف .pacorig، يقوم pacman بإظهار ملاحظات عند إنشاء هذه الملفات.

يجب على المستخدمين أن يتعاملوا فوراً مع هذه الملفات عندما يقوم pacman بإنشائهم من أجل ضمان الاستقرار الأمثل للنظام، لمزيد من الإرشادات التفصيلية يرجى الاطلاع على صفحة [Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files").

#### خذ بعين الاعتبار استخدام Pacmatic

[Pacmatic](http://kmkeen.com/pacmatic/index.html) عبارة عن غلاف لمدير الحزم pacman يقوم بأتمتة عملية تفحص أخبار آرتش قبل الترقية، كما يعمل Pacmatic على التأكد من أن قاعدة بيانات pacman المحلية تم مزامنتها بشكل صحيح مع المرايا على الإنترنت، وبالتالي تجنب المشاكل المحتملة من تحديثات قواعد بيانات pacman -Sy غير المتقنة، وأخيراً فهي تقدم تحذيرات أكثر صرامة عن ملفات التكوين المُحدَّثة أو القديمة، يمكن أن يكون pacmatic بديلاً عن pacman ،كما أن الكثير من أدوات [AUR helpers](/index.php/AUR_helpers "AUR helpers") يمكن ضبطها لاستعمال pacmatic بدلاً من pacman.

#### تجنب بعض الأوامر المعينة في pacman

آرتش توزيعة تعتمد مفهوم الإصدار المتدحرج، وقد يكون من الخطر القيام بتحديث refresh لقواعد بيانات pacman من دون القيام بترقية كاملة للنظام بعدها مباشرة، تجنب تنفيذ الأمر `pacman -Sy package` لتثبيت حزمة ما، لكن بدلاً من ذلك قم بتنفيذ `pacman -S package` دائماً، وقم بترقية النظام بانتظام بواسطة الأمر `pacman -Syu`.

تجنب استخدام الخيار `-f` مع pacman **خصوصاً** مع الأوامر مثل `pacman -Syuf` بإشراك أكثر من حزمة، الخيار `--force` يتجاهل التعارض بين الملفات وحتى أنه قد يتسبب بفقد للملفات عند نقلها بين الحزم المختلفة! في نظام يتم الإشراف عليه بصورة صحيحة يجب عدم استعمال الأمر السابق أبداً.

لا تستخدم الأمر `pacman -Rdd package`، فاستخدام الخيار -d يتخطى مرحلة التحقق من الاعتماديات أثناء حذف الحزمة، حيث قد يتم حذف حزمة تقدم اعتمادية مهمة مما يتسبب في الحصول على نظام معطوب.

لا تنفذ الأمر `pacman -Scc` أبداً إلا إذا كنت في حاجة ملحة للمساحة على القرص أو إذا كنت لا ترغب بالاحتفاظ بالحزم المؤرشفة، من الأفضل الاحتفاظ بالحزم القديمة في أرشيف الملفات المخبأة حيث أنه في حال أن ترقية حزمة ما تسبب بمشاكل يمكن الرجوع إلى النسخة الأقدم منها، بدلاً من ذلك قم بتنفيذ الأمر `pacman -Sc` لإزالة الحزم المؤرشفة التي تمت إزالتها مسبقاً من قواعد بيانات pacman.

لا تستخدم هذا الأمر إلا إذا لم تعد هناك أية نية لإعادة تثبيت الحزم المحذوفة مؤخراً، إذا تم إعادة تثبيت نفس الحزم بعد تنفيذ هذا الأمر فلن يكون هناك نسخ أقدم أو نسخ مؤرشفة من الحزم في مجلد cache الخاص بمدير الحزم pacman.

في حال أن المساحة الخالية للمجلد /var أصبحت قليلة قم بنقل **كل** الحزم المؤرشفة إلى مجلد المنزل بواسطة السكربت [fduparch.sh](http://www.3111skyline.com/download/Archlinux/scripts/)، استخدم السكربت [fduppkg](http://www.3111skyline.com/download/Archlinux/scripts/fduppkg) لنقل الكل ما عدا آخر النسخ التي ثُبِّتت سابقاً المتواجدة في مجلد cache الخاص بـ pacman إلى مجلد المنزل.

#### تراجع عن ترقية الحزمة التي تسبب عدم الاستقرار

في حال أن حزمة ما أدت إلى عدم استقرار النظام بعد ترقيتها قم بتثبيت آخر نسخة مستقرة منها من مجلد الملفات المخبأة لمدير الملفات pacman بواسطة الأمر التالي:

```
pacman -U /var/cache/pacman/pkg/Package-Name.pkg.tar.gz

```

لمزيد من المعلومات المُفَصَّلة عن العودة إلى حزمة أقدم راجع صفحة [Downgrading packages](/index.php/Downgrading_packages "Downgrading packages").

حالما تعود إلى الحزمة الأقدم قم بإضافتها مؤقتاً إلى قسم الحزم المتجاهَلة [IgnorePkg section of pacman.conf](/index.php/Pacman#Skip_package_from_being_upgraded "Pacman") إلى أن تُحَل المشكلة، راجع ويكي آرتش و/أو المنتديات من أجل الحصول على النصيحة أو من أجل التبليغ عن العلل عند الضرورة.

#### قم بأخذ قائمة احتياطية بالحزم المثبتة بانتظام

أنشئ قائمة بالحزم المثبتة على فترات منتظمة، وقم بتخزين نسخة منها أو أكثر على وسائط تخزين محلية مثل قرص USB أو قرص صلب خارجي أو قرص مدمج CD-R، قم بتنفيذ الأمر التالي لكي تنشئ قائمة بالحزم المثبتة:

```
pacman -Qqe | grep -vx "$(pacman -Qqm)" > /path/to/chosen/directory/pkg.list

```

في حال حدوث فشل كارثي يتطلب إعادة تثبيت كامل للنظام يمكن إعادة تثبيت هذه الحزم بسرعة عن طريق الأمر:

```
xargs -a /path/to/chosen/directory/pkg.list pacman -S --needed

```

#### خذ نسخة احتياطية من قاعدة بيانات pacman بانتظام

يمكن تنفيذ الأمر التالي لأخذ نسخة احتياطية من قاعدة بيانات pacman المحلية ومن الممكن تنفيذه كـ cronjob:

```
tar -cjf /path/to/chosen/directory/pacman-database.tar.bz2 /var/lib/pacman/local

```

قم بتخزين نسخة منها أو أكثر على وسائط تخزين محلية مثل قرص USB أو قرص صلب خارجي أو قرص مدمج CD-R.

استرجع النسخة الاحتياطية من قاعدة البيانات عن طريق نقل ملف pacman-database.tar.bz2 إلى مجلد "/" وتنفيذ الأمر:

```
tar -xjvf pacman-database.tar.bz2

```

إذا كانت ملفات قاعدة بيانات pacman تالفة ولم يكن هناك نسخة احتياطية منها فمازال هناك بعض الأمل في إعادة بناء قاعدة بيانات pacman، راجع صفحة [How To Restore Pacman's Local Database](/index.php/Pacman_tips#Restore_pacman.27s_local_database "Pacman tips").

##### أتمتة Systemd

يمكنك إعداد [systemd](/index.php/Systemd "Systemd") لكي يقوم بأخذ نسخة احتياطية من قاعدة بيانات pacman في كل مرة يتم تثبيت أو تحديث حزمة جديدة، قم بحفظ وتشغيل السكربت التالي، انظر [هنا](/index.php/Pacman_tips#Backing_up_Local_database_with_Systemd "Pacman tips").

### أفضل الممارسات العامة

#### اشترك بتنبيهات NVD/CVE وقم بالترقية فقط عند ظهور تنبيه أمني

اشترك بتحديثات التنبيهات الأمنية لنقاط الضعف والتعرض الشائعة Common Vulnerabilities and Exposure التي تتيحها National Vulnerability Database والمتوفرة على الرابط [NVD Download webpage](http://nvd.nist.gov/download.cfm)، فقط قم بتحديث النظام عند ورود تنبيه أمني لحزمة مثبتة على النظام.

هذا هو البديل عن ترقية النظام كاملاً بشكل متكرر في فترات قصيرة، كما أنه يضمن أن المشاكل الأمنية في الحزم المتعددة يتم حلها سريعاً مع الإبقاء على كل الحزم الباقية مجمَّدة في تكوين معروف ومستقر، كما أن مراجعة تنبيهات CVE المتكررة لمعرفة ما إذا كان هناك شيء مخصص لحزم آرتش المثبتة يُعَّد أمراً مملاً ومضيعة للوقت.

#### اختبر التحديثات على نظام آخر

إذا كان بالإمكان فقم باختبار التغييرات في ملفات التكوين وتحديثات الحزم أولاً على نظام آخر متطابق وغير حرج، فإذا لم تظهر مشاكل فقم بتطبيق التغييرات على النظام المطلوب.

#### دائماً خذ نسخة احتياطية من ملفات التكوين قبل التعديل عليها

قبل أن تجري أي تعديلات على أي ملف تكوين config files قم دائماً بأخذ نسخة احتياطية من النسخة التي تعمل بشكل صحيح منه، ففي حال أن التعديلات على الملف سببت مشاكل يمكن للمستخدم أن يعود إلى النسخة المستقرة منه، قم بهذا الأمر عن طريق محرر نصوص لكن أولاً خذ نسخة احتياطية منه، أو نَفِّذ الأمر التالي:

```
cp config config.bak

```

استخدام اللاحقة **.bak** سيضمن وجود نسخة احتياطية (أُنشئت من قِبَل المستخدم) يسهل تمييزها في حال أن pacman قام بإنشاء ملفات .pacnew أو .pacsave أو .pacorig.

أداة [etckeeper](https://www.archlinux.org/packages/?name=etckeeper) تساعد في التعامل مع ملفات التكوين، فهي تحافظ على مجلد /var كاملاً ضمن version control.

#### خذ نسخة احتياطية من مجلدات /etc و /home و /srv و /var في فترات منتظمة

بما أن مجلدات /etc و /home و /srv و /var تحتوي على ملفات نظام وإعدادات مهمة ينصح بأخذ نسخة احتياطية من هذه المجلدات في فترات منتظمة، الأسطر القادمة عبارة عن دليل مبسط حول كيفية القيام بهذا الأمر.

*   **/etc:** خذ نسخة احتياطية من مجلد /etc عن طريق تنفيذ الأمر التالي بصلاحيات الجذر أو كـ cronjob:

```
tar -cjf /path/to/chosen/directory/etc-backup.tar.bz2 /etc

```

قم بتخزين النسخة الاحتياطية على وسيط تخزين محلي أو أكثر مثل قرص USB أو قرص صلب خارجي أو قرص مدمج CD-R، بين الحين والآخر تحقق من سلامة عملية النسخ الاحتياطي عن طريق مقارنة الملفات والمجلدات الأصلية مع النسخة الاحتياطية منها.

استرجع ملفات /etc التالفة عن طريق استخراج ملف etc-backup.tar.bz2 في مجلد عمل مؤقت، والنسخ على الملفات والمجلدات الشخصية إذا لزم الأمر، لاسترجاع جميع محتويات مجلد /etc انقل ملف etc-backup.tar.bz2 إلى مجلد "/"، ومن ثم نَفِّذ الأمر التالي كمستخدم جذر:

```
tar -xvjf etc-backup.tar.bz2

```

*   **/home:** على فترات منتظمة قم بأخذ نسخة احتياطية من مجلد /home وضعها على قرص صلب خارجي أو على مُخدِّم متصل بالشبكة أو على خدمة نسخ احتياطي على الإنترنت، بين الحين والآخر تحقق من سلامة عملية النسخ الاحتياطي عن طريق مقارنة الملفات والمجلدات الأصلية مع النسخة الاحتياطية منها.

*   **/srv:** يجب الحفاظ على نسخة احتياطية من مجلد /srv بانتظام في حال Server installations.

*   **/var:** هناك مجلدات إضافية في المجلد /var مثل المجلد /var/spool/mail أو المجلد /var/lib يجب أخذ نسخة احتياطية منها والتأكد من سلامتها بين الحين والآخر.

إذا كنت ترغب بإجراء عملية النسخ الاحتياطي بشكل أسرع (باستخدام الضغط المتوازي أو SMP) يجب عليك استخدام pbzip2 (Parallel bzip2)، الخطوات مختلفة قليلاً عن الطريقة السابقة.

أولاً سنأخذ نسخة احتياطية من الملفات ونضعها في ملف tarball بسيط ومن دون ضغط:

```
tar -cvf /path/to/chosen/directory/etc-backup.tar /etc

```

ثم سنستخدم pbzip2 لضغط الملف السابق على التوازي (تأكد من أنك قم بتثبيته عن طريق الأمر **pacman -S pbzip2**):

```
pbzip2 /path/to/chosen/directory/etc-backup.tar.bz2

```

هذا كل مافي الأمر، يجب على ملفاتك الآن أن تُنسخ احتياطياً باستخدام جميع الأنوية المتوفرة في معالجك.