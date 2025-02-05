---
title: "Jegyzetfüzetek"
icon: material/notebook-edit-outline
---

Kövesd nyomon jegyzeteid és naplóid anélkül, hogy harmadik félnek adnád át azokat.

Ha jelenleg olyan alkalmazást használsz, mint az Evernote, a Google Keep vagy a Microsoft OneNote, javasoljuk, hogy válassz egy olyan alternatívát, amely támogatja az End-to-End titksoítást.

## Felhő-alapú

### Joplin

!!! recommendation

    ![Joplin logo](assets/img/notebooks/joplin.svg){ align=right }
    
    A **Joplin** egy ingyenes, nyílt forráskódú, teljesen felszerelt jegyzetkezelő és teendő vezető alkalmazás, amely nagyszámú, jegyzetfüzetekbe és címkékbe rendezett markdown jegyzeteket képes kezelni. End-to-End titkosítást kínál, és képes szinkronizálni a Nextcloudon, a Dropboxon és sok máson keresztül is. Evernote és nyílt szöveges jegyzetek egyszerű importálását is lehetővé teszi.
    
    [:octicons-home-16: Honlap](https://joplinapp.org/){ .md-button .md-button--primary }
    [:octicons-eye-16:](https://joplinapp.org/privacy/){ .card-link title="Adatvédelmi Nyilatkozat" }
    [:octicons-info-16:](https://joplinapp.org/help/){ .card-link title=Dokumentáció}
    [:octicons-code-16:](https://github.com/laurent22/joplin){ .card-link title="Forráskód" }
    [:octicons-heart-16:](https://joplinapp.org/donate/){ .card-link title=Közreműködés }
    
    ??? downloads
    
        - [:simple-googleplay: Google Play](https://play.google.com/store/apps/details?id=net.cozic.joplin)
        - [:simple-appstore: App Store](https://apps.apple.com/us/app/joplin/id1315599797)
        - [:simple-github: GitHub](https://github.com/laurent22/joplin-android/releases)
        - [:simple-windows11: Windows](https://joplinapp.org/#desktop-applications)
        - [:simple-apple: macOS](https://joplinapp.org/#desktop-applications)
        - [:simple-linux: Linux](https://joplinapp.org/#desktop-applications)
        - [:simple-firefoxbrowser: Firefox](https://addons.mozilla.org/firefox/addon/joplin-web-clipper/)
        - [:simple-googlechrome: Chrome](https://chrome.google.com/webstore/detail/joplin-web-clipper/alofnhikmmkdbbbgpnglcpdollgjjfek)

A Joplin nem támogatja a jelszavas/PIN-kódos védelmet magához az [alkalmazáshoz vagy egyes jegyzetekhez és jegyzetfüzetekhez](https://github.com/laurent22/joplin/issues/289). Ettől függetlenül az adatok szállítás közben és a szinkronizáció helyén is titkosítva lesznek a főkulcs segítségével. Since January 2023, Joplin supports biometrics app lock for [Android](https://joplinapp.org/changelog_android/#android-v2-10-3-https-github-com-laurent22-joplin-releases-tag-android-v2-10-3-pre-release-2023-01-05t11-29-06z) and [iOS](https://joplinapp.org/changelog_ios/#ios-v12-10-2-https-github-com-laurent22-joplin-releases-tag-ios-v12-10-2-2023-01-20t17-41-13z).

### Standard Notes

!!! recommendation

    ![Standard Notes logo](assets/img/notebooks/standard-notes.svg){ align=right }
    
    **Standard Notes** is a simple and private notes app that makes your notes easy and available everywhere you are. It features E2EE on every platform, and a powerful desktop experience with themes and custom editors. It has also been [independently audited (PDF)](https://s3.amazonaws.com/standard-notes/security/Report-SN-Audit.pdf).
    
    [:octicons-home-16: Homepage](https://standardnotes.com){ .md-button .md-button--primary }
    [:octicons-eye-16:](https://standardnotes.com/privacy){ .card-link title="Privacy Policy" }
    [:octicons-info-16:](https://standardnotes.com/help){ .card-link title=Documentation}
    [:octicons-code-16:](https://github.com/standardnotes){ .card-link title="Source Code" }
    [:octicons-heart-16:](https://standardnotes.com/donate){ .card-link title=Contribute }
    
    ??? downloads
    
        - [:simple-googleplay: Google Play](https://play.google.com/store/apps/details?id=com.standardnotes)
        - [:simple-appstore: App Store](https://apps.apple.com/app/id1285392450)
        - [:simple-github: GitHub](https://github.com/standardnotes/app/releases)
        - [:simple-windows11: Windows](https://standardnotes.com)
        - [:simple-apple: macOS](https://standardnotes.com)
        - [:simple-linux: Linux](https://standardnotes.com)
        - [:octicons-globe-16: Web](https://app.standardnotes.com/)

### Cryptee

!!! recommendation

    ![Cryptee logo](./assets/img/notebooks/cryptee.svg#only-light){ align=right }
    ![Cryptee logo](./assets/img/notebooks/cryptee-dark.svg#only-dark){ align=right }
    
    **Cryptee** is an open-source, web-based E2EE document editor and photo storage application. Cryptee is a PWA, which means that it works seamlessly across all modern devices without requiring native apps for each respective platform.
    
    [:octicons-home-16: Homepage](https://crypt.ee){ .md-button .md-button--primary }
    [:octicons-eye-16:](https://crypt.ee/privacy){ .card-link title="Privacy Policy" }
    [:octicons-info-16:](https://crypt.ee/help){ .card-link title=Documentation}
    [:octicons-code-16:](https://github.com/cryptee){ .card-link title="Source Code" }
    
    ??? downloads
    
        - [:octicons-globe-16: PWA](https://crypt.ee/download)

Cryptee offers 100MB of storage for free, with paid options if you need more. Sign-up doesn't require an e-mail or other personally identifiable information.

## Local notebooks

### Org-mode

!!! recommendation

    ![Org-mode logo](assets/img/notebooks/org-mode.svg){ align=right }
    
    **Org-mode** is a [major mode](https://www.gnu.org/software/emacs/manual/html_node/elisp/Major-Modes.html) for GNU Emacs. Org-mode is for keeping notes, maintaining TODO lists, planning projects, and authoring documents with a fast and effective plain-text system. Synchronization is possible with [file synchronization](file-sharing.md#file-sync) tools.
    
    [:octicons-home-16: Homepage](https://orgmode.org){ .md-button .md-button--primary }
    [:octicons-info-16:](https://orgmode.org/manuals.html){ .card-link title=Documentation}
    [:octicons-code-16:](https://git.savannah.gnu.org/cgit/emacs/org-mode.git){ .card-link title="Source Code" }
    [:octicons-heart-16:](https://liberapay.com/bzg){ .card-link title=Contribute }

## Követelmények

**Tartsd figyelemben, hogy nem állunk kapcsolatban az általunk ajánlott projektek egyikével sem.** A [szabványos kritériumaink mellett](about/criteria.md), egyértelmű követelményrendszert dolgoztunk ki, hogy objektív ajánlásokat tudjunk tenni. Javasoljuk, hogy ismerkedj meg ezzel a listával, mielőtt kiválasztanál egy projektet, és végezz saját kutatásokat, hogy megbizonyosodj arról, hogy ez a megfelelő választás számodra.

!!! example "Ez a szakasz új"

    Azon dolgozunk, hogy meghatározott követelményeket állapítsunk meg az oldalunk minden egyes szakaszára vonatkozóan, és ez még változhat. Ha bármilyen kérdésed van a követelményinkkel kapcsolatban, kérjük, [kérdezz a fórumon](https://discuss.privacyguides.net/latest), és ne feltételezd, hogy valamit nem vettünk figyelembe az ajánlásaink elkészítésekor, ha az nem szerepel itt. There are many factors considered and discussed when we recommend a project, and documenting every single one is a work-in-progress.

- Clients must be open-source.
- Any cloud sync functionality must be E2EE.
- Must support exporting documents into a standard format.

### Best Case

- Local backup/sync functionality should support encryption.
- Cloud-based platforms should support document sharing.

--8<-- "includes/abbreviations.hu.txt"
