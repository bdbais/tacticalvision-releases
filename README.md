# TacticalVision — rilasci

Canale ufficiale di distribuzione di **TacticalVision**, l'app di analisi video per il
tennistavolo. Qui trovi gli APK firmati e il manifest che l'app legge per accorgersi da sola
quando esce una versione nuova.

**Sito:** https://tacticalvision.pages.dev

## Scaricare l'app

Prendi l'APK dall'[ultima release](https://github.com/bdbais/tacticalvision-releases/releases/latest)
e aprilo sul telefono. Android chiederà di autorizzare l'installazione da questa origine: è la
procedura normale fuori dal Play Store.

Requisiti: Android 8.0 o successivo, processore ARM (`arm64-v8a` o `armeabi-v7a`).

Dopo la prima installazione non serve più tornare qui: l'app controlla gli aggiornamenti da sola,
scarica l'APK, ne verifica l'impronta SHA-256 e propone l'installazione.

## `update.json`

È la sola sorgente di verità sulla versione corrente: la leggono sia l'app sia il sito.

```json
{
  "versionCode": 5,
  "versionName": "0.3.0",
  "apkUrl": "https://github.com/.../tacticalvision-0.3.0.apk",
  "sha256": "...",
  "sizeBytes": 23752650,
  "minSdk": 26,
  "publishedAt": "2026-09-21",
  "releaseNotes": "..."
}
```

L'app aggiorna solo se `versionCode` è maggiore di quello installato, e installa solo se
l'impronta SHA-256 dell'APK scaricato corrisponde. Se non corrisponde, il file viene scartato.

## Verificare la firma

Tutti gli APK sono firmati con la stessa chiave. Impronta del certificato:

```
SHA-256  99:8C:0F:46:B3:96:80:94:88:FC:22:B1:18:92:C5:78:08:D0:FA:B5:BE:61:FA:C2:07:DF:F4:E5:88:94:33:AF
SHA-1    37:6D:2F:A6:72:E0:30:66:A8:E8:B2:1E:73:F5:D5:11:54:92:88:0A
```

```bash
apksigner verify --print-certs tacticalvision-0.3.0.apk
```

Se l'impronta è diversa, l'APK non viene da qui: non installarlo.

## Privacy

L'app non ha un backend. Le uniche connessioni che apre sono verso questo repository, per
leggere `update.json` e scaricare l'APK, e verso Google per il modello di riconoscimento della
posa (opzionale, 5 MB, una sola volta). Video e statistiche restano sul telefono.

## Codice sorgente

Il sorgente è in un repository privato. Questo repository contiene solo gli artefatti di rilascio.

## Licenza

MIT — vedi [LICENSE](LICENSE).
