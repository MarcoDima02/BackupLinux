# Schedulazione backup

## 🧾 Descrizione
Questo script Bash è stato creato per automatizzare il backup quotidiano della directory home dell'utente selezionato, garantendo così la sicurezza dei dati personali in caso di malfunzionamenti, cancellazioni accidentali o problemi hardware.
Il backup viene copiato in una directory di destinazione predefinita: /opt/backup.

## ⚙️ Funzionalità dello script
- Comprende la home directory (/home/nome utente)

- Salva i backup in /opt/backup

- I file vengono compressi in un archivio .tar.gz nominato con data e ora

- Pensato per essere eseguito quotidianamente tramite cron

## 📋 Requisiti
- Sistema operativo Linux

- Permessi di scrittura su /opt/backup (scrivere sudo prima di ogni comando, per evitare di avere problemi di permessi).

- Permessi di lettura sulla home directory dell’utente

- Privilegi per modificare il crontab dell’utente o di root

## 🚀 Istruzioni per l'utilizzo
1. Copia dello script
Salva lo script in un file, ad esempio backup_home.sh, e assicurati che sia eseguibile:

```bash
chmod +x backup_home.sh
```
2. Contenuto dello script (esempio)
```bash
#!/bin/bash

# Data di inizio e fine (modifica le date come necessario)
START_DATE="2025-05-15"
END_DATE="2025-05-21"

# Data di oggi
TODAY=$(date +%F)

# Confronta le date
if [[ "$TODAY" < "$START_DATE" || "$TODAY" > "$END_DATE" ]]; then
    exit 0  # Esci senza fare nulla
fi

# Directory di origine e destinazione
SOURCE="/home/scripts"
DESTINATION="/opt/backup"

# Nome backup con data
DATE=$(date +'%Y-%m-%d')
BACKUP_NAME="backup_home_$DATE.tar.gz"

# Backup
tar -czf "$DESTINATION/$BACKUP_NAME" "$SOURCE"
```

3. Test dello script
Puoi testarlo manualmente eseguendo:

```bash
./backup_home.sh
```
Verifica che il file compresso sia stato creato correttamente in /opt/backup.

## 📆 Configurazione della schedulazione (cron)
Per eseguire automaticamente lo script ogni giorno, utilizza cron.

4. Modifica del crontab
Esegui:

```bash
crontab -e
```
Aggiungi la seguente riga per eseguire il backup ogni giorno alle 4:00 di notte:

```bash
0 4 * * * script/backup.sh
```



✅ Conclusione
Automatizzare i backup è un passo essenziale per la protezione dei dati. Questo script, abbinato a una semplice schedulazione cron, ti consente di mantenere una copia aggiornata della tua home directory senza sforzo manuale.

