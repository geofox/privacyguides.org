---
title: סקירה כללית של אנדרואיד
icon: simple/android
---

אנדרואיד היא מערכת הפעלה מאובטחת הכוללת [ארגז חול חזק של אפליקציות](https://source.android.com/security/app-sandbox), [אתחול מאומת](https://source.android.com/security/verifiedboot) (AVB) ומערכת בקרת [הרשאות](https://developer.android.com/guide/topics/permissions/overview) חזקה.

## בחירת הפצת אנדרואיד

כאשר אתה קונה טלפון אנדרואיד, מערכת ההפעלה המוגדרת כברירת מחדל של המכשיר מגיעה לרוב עם אינטגרציה פולשנית עם אפליקציות ושירותים שאינם חלק מ[פרויקט הקוד הפתוח של אנדרואיד](https://source.android.com/). דוגמה כזו היא שירותי Google Play, שיש לו הרשאות בלתי חוזרות לגשת לקבצים שלך, אחסון אנשי הקשר, יומני שיחות, הודעות SMS, מיקום, מצלמה, מיקרופון, מזהי חומרה וכו'. אפליקציות ושירותים אלו מגדילים את משטח ההתקפה של המכשיר שלך ומהווים מקור לחששות פרטיות שונים עם אנדרואיד.

ניתן לפתור בעיה זו באמצעות הפצת אנדרואיד מותאמת אישית שאינה מגיעה עם אינטגרציה פולשנית כזו. לרוע המזל, הפצות רבות של אנדרואיד מותאמות אישית מפרות לעתים קרובות את מודל האבטחה של אנדרואיד בכך שאינן תומכות בתכונות אבטחה קריטיות כגון AVB, הגנה לאחור, עדכוני קושחה וכן הלאה. חלק מההפצות מספקות גם רכיבי [`userdebug`](https://source.android.com/setup/build/building#choose-a-target) אשר חושפים שורש באמצעות [ADB](https://developer.android.com/studio/command-line/adb) ודורשים [מדיניות](https://github.com/LineageOS/android_system_sepolicy/search?q=userdebug&type=code) SELinux מתירנית יותר כדי להתאים לתכונות ניפוי באגים, וכתוצאה מכך משטח התקפה מוגדל נוסף ומודל אבטחה מוחלש.

באופן אידיאלי, בעת בחירת הפצת אנדרואיד מותאמת אישית, עליך לוודא שהיא מקיימת את מודל האבטחה של אנדרואיד. לכל הפחות, להפצה צריכה להיות בניית ייצור, תמיכה ב-AVB, הגנה על חזרה, עדכוני קושחה ומערכת הפעלה בזמן, ו-SELinux ב[מצב אכיפה](https://source.android.com/security/selinux/concepts#enforcement_levels). כל הפצות האנדרואיד המומלצות שלנו עומדות בקריטריונים האלה.

[המלצות מערכת אנדרואיד שלנו :material-arrow-right-drop-circle:](../android.md ""){.md-button}

## הימנע מהשתרשות

[השרשת](https://en.wikipedia.org/wiki/Rooting_(Android)) טלפונים אנדרואיד יכולים להפחית את האבטחה באופן משמעותי מכיוון שהוא מחליש את [מודל האבטחה של אנדרואיד](https://en.wikipedia.org/wiki/Android_(operating_system)#Security_and_privacy). זה יכול להפחית את הפרטיות אם יש ניצול הנעזר בירידה באבטחה. שיטות השתרשות נפוצות כוללות התעסקות ישירה במחיצת האתחול, מה שהופך את זה לבלתי אפשרי לבצע אתחול מאומת בהצלחה. אפליקציות הדורשות שורש ישנו גם את מחיצת המערכת, כלומר אתחול מאומת יצטרך להישאר מושבת. חשיפת השורש ישירות בממשק המשתמש גם מגדילה את [משטח ההתקפה](https://en.wikipedia.org/wiki/Attack_surface) של המכשיר שלך ועשויה לסייע ב[הסלמה של הרשאות](https://en.wikipedia.org/wiki/Privilege_escalation) פגיעויות ועקיפות מדיניות SELinux.

חוסמי פרסומות, המשנים את [קובץ המארחים](https://en.wikipedia.org/wiki/Hosts_(file)) (AdAway) וחומות אש (AFWall+) הדורשות גישת בסיס מתמשכת הם מסוכנים ו אסור להשתמש. הם גם לא הדרך הנכונה לפתור את מטרותיהם המיועדות. לחסימת מודעות אנו מציעים במקום זאת פתרונות חסימת שרת [DNS](../dns.md) או [VPN](../vpn.md) מוצפנים. RethinkDNS, TrackerControl ו-AdAway במצב ללא-שורש יתפסו את חריץ ה-VPN (על ידי שימוש ב-VPN עם לולאה מקומית) וימנעו ממך להשתמש בשירותים לשיפור הפרטיות כגון Orbot או שרת VPN אמיתי.

AFWall+ פועל על בסיס גישת [סינון חבילות](https://en.wikipedia.org/wiki/Firewall_(computing)#Packet_filter) וייתכן שניתן לעקוף אותו במצבים מסוימים.

אנחנו לא מאמינים שקורבנות האבטחה שנעשו על ידי השתרשות טלפון שווים את יתרונות הפרטיות המפוקפקים של אפליקציות אלה.

## אתחול מאומת

[אתחול מאומת](https://source.android.com/security/verifiedboot) הוא חלק חשוב ממודל האבטחה של אנדרואיד. הוא מספק הגנה מפני התקפות [משרתת רעה](https://en.wikipedia.org/wiki/Evil_maid_attack), התמדה של תוכנות זדוניות, ומבטיח שלא ניתן לשדרג לאחור עדכוני אבטחה עם [הגנה לאחור](https://source.android.com/security/verifiedboot/verified-boot#rollback-protection).

אנדרואיד 10 ומעלה עברה מהצפנה בדיסק מלא ל[הצפנה מבוססת קבצים](https://source.android.com/security/encryption/file-based) גמישה יותר. הנתונים שלך מוצפנים באמצעות מפתחות הצפנה ייחודיים, וקבצי מערכת ההפעלה נותרים לא מוצפנים.

אתחול מאומת מבטיח את שלמות קבצי מערכת ההפעלה, ובכך מונע מיריב בעל גישה פיזית לחבל או להתקין תוכנה זדונית במכשיר. במקרה הבלתי סביר שתוכנות זדוניות מסוגלות לנצל חלקים אחרים של המערכת ולהשיג גישה מוסמכת יותר, אתחול מאומת ימנע ותחזיר שינויים במחיצת המערכת עם אתחול המכשיר מחדש.

למרבה הצער, יצרני ציוד מקורי מחויבים לתמוך באתחול מאומת רק בהפצת אנדרואיד בברירת מחדל שלהם. רק כמה יצרני OEM כגון גוגל תומכים ברישום מפתח AVB מותאם אישית במכשירים שלהם. בנוסף, חלק מנגזרות AOSP כגון LineageOS או /e/ OS אינן תומכות ב-Verified Boot אפילו בחומרה עם תמיכה ב-Verified Boot עבור מערכות הפעלה של צד שלישי. אנו ממליצים לבדוק אם יש תמיכה **לפני** רכישת מכשיר חדש. נגזרות AOSP שאינן תומכות באתחול מאומת **לא** מומלצות.

יצרני OEM רבים גם עשו יישום שבור של אתחול מאומת שעליך להיות מודע אליו מעבר לשיווק שלהם. לדוגמה, ה-Fairphone 3 ו-4 אינם מאובטחים כברירת מחדל, מכיוון ש[מטען האתחול של הברירת מחדל סומך על מפתח החתימה הציבורי של ](https://forum.fairphone.com/t/bootloader-avb-keys-used-in-roms-for-fairphone-3-4/83448/11)AVB. זה שובר אתחול מאומת במכשיר Fairphone ברירת מחדל, מכיוון שהמערכת תאתחל מערכות הפעלה חלופיות של אנדרואיד כגון (כגון /e/) [ללא כל אזהרה](https://source.android.com/security/verifiedboot/boot-flow#locked-devices-with-custom-root-of-trust) לגבי שימוש מותאם אישית במערכת ההפעלה.

## עדכוני קושחה

עדכוני קושחה הם קריטיים לשמירה על האבטחה ובלעדיהם המכשיר שלך לא יכול להיות מאובטח. ליצרני ציוד מקורי יש הסכמי תמיכה עם השותפים שלהם כדי לספק את רכיבי הקוד הסגור לתקופת תמיכה מוגבלת. אלה מפורטים ב[עלוני האבטחה של אנדרואיד](https://source.android.com/security/bulletin) החודשיים.

מכיוון שרכיבי הטלפון, כגון טכנולוגיות המעבד והרדיו, מסתמכים על רכיבי קוד סגור, העדכונים חייבים להיות מסופקים על ידי היצרנים המתאימים. לכן, חשוב שתרכוש מכשיר בתוך מחזור תמיכה פעיל. [קוואלקום](https://www.qualcomm.com/news/releases/2020/12/16/qualcomm-and-google-announce-collaboration-extend-android-os-support-and) ו[סמסונג](https://news.samsung.com/us/samsung-galaxy-security-extending-updates-knox/) תומכות במכשירים שלהן במשך 4 שנים, בעוד שלמוצרים זולים יותר יש לרוב מחזורי תמיכה קצרים יותר. עם ההשקה של [פיקסל 6](https://support.google.com/pixelphone/answer/4457705), גוגל מייצרת כעת את ה-SoC שלהם והם יספקו לפחות 5 שנים של תמיכה.

מכשירי EOL שאינם נתמכים עוד על ידי יצרן ה-SoC אינם יכולים לקבל עדכוני קושחה מספקי OEM או מפיצי אנדרואיד לאחר השוק. משמעות הדבר היא שבעיות אבטחה במכשירים אלה יישארו ללא תיקון.

Fairphone, למשל, משווקת את המכשירים שלהם כמקבלים 6 שנות תמיכה. עם זאת, ל-SoC (Qualcomm Snapdragon 750G ב-Fairphone 4) יש תאריך EOL קצר בהרבה. המשמעות היא שעדכוני אבטחת קושחה מ-Qualcomm עבור Fairphone 4 יסתיימו בספטמבר 2023, ללא קשר לשאלה אם Fairphone תמשיך לשחרר עדכוני אבטחה תוכנה.

## גרסאות אנדרואיד

חשוב לא להשתמש בגרסת [סוף החיים](https://endoflife.date/android) של אנדרואיד. גרסאות חדשות יותר של אנדרואיד לא רק מקבלות עדכוני אבטחה עבור מערכת ההפעלה אלא גם עדכונים חשובים לשיפור הפרטיות. לדוגמה, [לפני אנדרואיד 10](https://developer.android.com/about/versions/10/privacy/changes), כל אפליקציה עם הרשאת [`READ_PHONE_STATE`](https://developer.android.com/reference/android/Manifest.permission#READ_PHONE_STATE) יכלו לגשת למספרים סידוריים רגישים וייחודיים של הטלפון שלך כגון [IMEI](https://en.wikipedia.org/wiki/International_Mobile_Equipment_Identity), [MEID](https://en.wikipedia.org/wiki/Mobile_equipment_identifier), כרטיס ה-SIM שלך[IMSI](https://en.wikipedia.org/wiki/International_mobile_subscriber_identity), בעוד שכעת הם חייבים להיות אפליקציות מערכת כדי לעשות זאת. אפליקציות מערכת מסופקות רק על ידי הפצת OEM או אנדרואיד.

## הרשאות אנדרואיד

[הרשאות ב-אנדרואיד](https://developer.android.com/guide/topics/permissions/overview) מעניקות לך שליטה על האפליקציות המורשות לגשת. גוגל מבצעת בקביעות [שיפורים](https://developer.android.com/about/versions/11/privacy/permissions) במערכת ההרשאות בכל גרסה עוקבת. כל האפליקציות שאתה מתקין הן אך ורק [ארגז חול](https://source.android.com/security/app-sandbox), לכן, אין צורך להתקין אפליקציות אנטי וירוס. סמארטפון עם הגרסה העדכנית ביותר של אנדרואיד תמיד יהיה מאובטח יותר מסמארטפון ישן עם אנטי וירוס ששילמת עליו. עדיף לא לשלם על תוכנת אנטי וירוס ולחסוך כסף בקניית סמארטפון חדש כמו גוגל פיקסל.

אם תרצה להפעיל אפליקציה שאינך בטוח לגביה, שקול להשתמש בפרופיל משתמש או עבודה.

## גישה למדיה

לא מעט אפליקציות מאפשרות "לחלוק" איתם קובץ להעלאת מדיה. אם אתה רוצה, למשל, לצייץ תמונה לטוויטר, אל תעניק לטוויטר גישה ל"מדיה ותמונות" שלך, כי אז תהיה לה גישה לכל התמונות שלך. במקום זאת, עבור אל מנהל הקבצים שלך (documentsUI), שמור את התמונה ולאחר מכן שתף אותה עם טוויטר.

## פרופילי משתמשים

ניתן למצוא פרופילי משתמש מרובים ב**הגדרות** ← **מערכת** ← **משתמש מרובים** והם הדרך הפשוטה ביותר לבודד באנדרואיד.

עם פרופילי משתמש, אתה יכול להטיל הגבלות על פרופיל ספציפי, כגון: ביצוע שיחות, שימוש ב-SMS או התקנת אפליקציות במכשיר. כל פרופיל מוצפן באמצעות מפתח הצפנה משלו ואינו יכול לגשת לנתונים של אף פרופיל אחר. אפילו בעל המכשיר לא יכול לראות את הנתונים של פרופילים אחרים מבלי לדעת את הסיסמה שלהם. פרופילי משתמשים מרובים הם שיטה בטוחה יותר לבידוד.

## פרופיל עבודה

[פרופילי עבודה](https://support.google.com/work/android/answer/6191949) הם דרך נוספת לבודד אפליקציות בודדות ועשויה להיות נוחה יותר מפרופילי משתמשים נפרדים.

נדרשת אפליקציית **בקר מכשיר** כגון [Shelter](#recommended-apps) כדי ליצור פרופיל עבודה ללא MDM ארגוני, אלא אם אתה משתמש במערכת הפעלה אנדרואיד מותאמת אישית הכוללת אחת.

פרופיל העבודה תלוי בבקר התקן כדי לתפקד. תכונות כגון *מעבורת קבצים* ו*חסימת חיפוש אנשי קשר* או כל סוג של תכונות בידוד חייבות להיות מיושמות על ידי הבקר. עליך גם לסמוך באופן מלא על אפליקציית בקר המכשיר, מכיוון שיש לה גישה מלאה לנתונים שלך בתוך פרופיל העבודה.

שיטה זו בדרך כלל פחות מאובטחת מפרופיל משתמש משני; עם זאת, זה כן מאפשר לך את הנוחות של הפעלת אפליקציות בפרופיל העבודה וגם בפרופיל האישי בו-זמנית.

## מתג הרג VPN

אנדרואיד 7 ומעלה תומך ב-VPN Killswitch והוא זמין ללא צורך בהתקנת אפליקציות של צד שלישי. תכונה זו יכולה למנוע דליפות אם ה-VPN מנותק. ניתן למצוא אותו ב:gear: **הגדרות** ← **רשת & אינטרנט** ← **VPN** ← :gear: ← **חסום חיבורים ללא VPN**.

## חילופי מצבים גלובליים

למכשירי אנדרואיד מודרניים יש בוררים גלובליים לביטול Bluetooth ושירותי מיקום. אנדרואיד 12 הציגה את המתגים למצלמה ולמיקרופון. כאשר לא בשימוש, אנו ממליצים להשבית תכונות אלה. אפליקציות לא יכולות להשתמש בתכונות מושבתות (גם אם ניתנה להן הרשאה פרטנית) עד להפעלה מחדש.

## גוגל

אם אתה משתמש במכשיר עם שירותי Google, בין אם מערכת ההפעלה ברירת מחדל שלך או מערכת הפעלה המארחת בבטחה את שירותי Google Play כמו GrapheneOS, ישנם מספר שינויים נוספים שתוכל לבצע כדי לשפר את הפרטיות שלך. אנו עדיין ממליצים להימנע לחלוטין משירותי Google, או להגביל את שירותי Google Play לפרופיל משתמש/עבודה ספציפי על ידי שילוב של בקר מכשיר כמו *Shelter* עם Google Play Sandboxed של GrapheneOS.

### תוכנית הגנה מתקדמת

אם יש לך חשבון Google, אנו מציעים להירשם ל[תוכנית ההגנה המתקדמת](https://landing.google.com/advancedprotection/). הוא זמין ללא עלות לכל מי שיש לו שני מפתחות אבטחה חומרה או יותר עם תמיכה ב[FIDO](../basics/multi-factor-authentication.md#fido-fast-identity-online).

תוכנית ההגנה המתקדמת מספקת ניטור איומים משופר ומאפשרת:

- אימות דו-גורמי מחמיר יותר; למשל שחייבים להשתמש ב-[FIDO](../basics/multi-factor-authentication.md#fido-fast-identity-online) **must** ואוסר את השימוש ב- [SMS OTPs](../basics/multi-factor-authentication.md#sms-or-email-mfa), [TOTP](../basics/multi-factor-authentication.md#time-based-one-time-password-totp) ו [OAuth](https://en.wikipedia.org/wiki/OAuth)
- רק גוגל ואפליקציות צד שלישי מאומתות יכולות לגשת לנתוני החשבון
- סריקה של הודעות דוא"ל נכנסות בחשבונות Gmail עבור ניסיונות [דיוג](https://en.wikipedia.org/wiki/Phishing#Email_phishing)
- [סריקת דפדפן בטוחה](https://www.google.com/chrome/privacy/whitepaper.html#malware) מחמירה יותר עם Google Chrome
- תהליך שחזור מחמיר יותר עבור חשבונות עם אישורים שאבדו

 עבור משתמשים שמשתמשים בשירותי Google Play המועדפים (הנפוצים במערכות הפעלה שמגיעות בברירת מחדל), תוכנית ההגנה המתקדמת מגיעה גם עם [הטבות נוספות](https://support.google.com/accounts/answer/9764949?hl=en) כגון:

- לא לאפשר התקנת אפליקציות מחוץ לחנות Google Play, חנות האפליקציות של ספק מערכת ההפעלה או דרך [`adb`](https://en.wikipedia.org/wiki/Android_Debug_Bridge)
- סריקת התקן אוטומטית חובה עם [Play Protect](https://support.google.com/googleplay/answer/2812853?hl=en#zippy=%2Chow-malware-protection-works%2Chow-privacy-alerts-work)
- אזהרה לגבי יישומים לא מאומתים

### עדכוני מערכת Google Play

בעבר, עדכוני אבטחה אנדרואיד היו צריכים להישלח על ידי ספק מערכת ההפעלה. אנדרואיד הפכה מודולרית יותר החל מאנדרואיד 10, וגוגל יכולה לדחוף עדכוני אבטחה עבור **חלק** רכיבי מערכת באמצעות שירותי Play המועדפים.

אם יש לך מכשיר EOL שנשלח עם אנדרואיד 10 ומעלה ואינך יכול להריץ אף אחת ממערכות ההפעלה המומלצות שלנו במכשיר שלך, סביר להניח שעדיף לך להישאר עם התקנת האנדרואיד של היצרן ציוד המקורי (בניגוד למערכת הפעלה שאינה מופיעה ברשימה כאן כגון LineageOS או /e/ OS). זה יאפשר לך לקבל **כמה**תיקוני אבטחה מגוגל, מבלי להפר את מודל האבטחה של אנדרואיד על ידי שימוש בנגזרת אנדרואיד לא מאובטחת והגדלת משטח ההתקפה שלך. אנו עדיין ממליצים לשדרג למכשיר נתמך בהקדם האפשרי.

### מזהה פרסום

כל המכשירים עם שירותי Google Play מותקנים באופן אוטומטי מייצרים [>מזהה פרסום](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) המשמש לפרסום ממוקד. השבת תכונה זו כדי להגביל את הנתונים שנאספו עליך.

בהפצות אנדרואיד עם [Google Play בארגז חול](https://grapheneos.org/usage#sandboxed-google-play), עבור אל :gear: **הגדרות** ← **אפליקציות** → **Google Play בארגז חול** ← **הגדרות גוגל** ← **מודעות**, ותבחר *מחק מזהה פרסום*.

בהפצות אנדרואיד עם שירותי Google Play מורשים (כגון מערכת הפעלה ברירת מחדל), ההגדרה עשויה להיות באחד מכמה מיקומים. בדיקה

- :gear: **הגדרות** ← **גוגל** ← **מודעות**
- :gear: **הגדרות** ← **גוגל** ← **מודעות**

תינתן לך האפשרות למחוק את מזהה הפרסום שלך או *לבטל את הסכמתך למודעות מבוססות עניין*, זה משתנה בין הפצות OEM של אנדרואיד. אם מוצגת האפשרות למחוק את מזהה הפרסום המועדף. אם לא, הקפד לבטל את הסכמתך ולאפס את מזהה הפרסום שלך.

### SafetyNet ו-Play Integrity API

[SafetyNet](https://developer.android.com/training/safetynet/attestation) וה[ממשק API של Play Integrity](https://developer.android.com/google/play/integrity) משמשים בדרך כלל עבור [אפליקציות בנקאיות](https://grapheneos.org/usage#banking-apps). אפליקציות בנקאות רבות יעבדו מצוין ב-GrapheneOS עם שירותי Play בארגז חול, אולם לחלק מהאפליקציות הלא פיננסיות יש מנגנוני אנטי-שיבוש גולמיים משלהם שעלולים להיכשל. GrapheneOS עובר את בדיקת `basicIntegrity`, אך לא את בדיקת האישור `ctsProfileMatch`. למכשירים עם אנדרואיד 8 ואילך יש תמיכה באישורי חומרה שלא ניתן לעקוף ללא מפתחות דלופים או פגיעויות חמורות.

לגבי ארנק Google, אנו לא ממליצים על כך בשל [ מדיניות הפרטיות שלהם](https://payments.google.com/payments/apis-secure/get_legal_document?ldo=0&ldt=privacynotice&ldl=en), הקובעת שעליך לבטל את הסכמתך אם אינך רוצה שדירוג האשראי והמידע האישי שלך ישותפו עם שירותי שיווק שותפים.

--8<-- "includes/abbreviations.he.txt"
