# tao-lanci

Avviso ntfy quando **aprono gli scambi del token di una nuova subnet Bittensor**. Solo lettura: nessuna chiave, nessuna transazione.

Legge direttamente la blockchain (nodi RPC pubblici), la fonte da cui leggono anche Taostats e Taosis.
Gli scambi di un nuovo token si aprono quando il proprietario fa lo *start call* e il flag `SubtokenEnabled` diventa vero;
prima la catena respinge ogni acquisto o vendita.

Avvisi:
- **Nuova subnet SNx**: registrata, scambi chiusi, data in cui potranno aprire.
- **SNx pronta al lancio**: da ora il proprietario può aprire in qualsiasi momento. Parte il controllo rapido (ogni 20 secondi).
- **LANCIO SNx: scambi aperti** (urgente): prezzo, pool, link a Taostats e Taosis.
- Un avviso giornaliero silenzioso di funzionamento.

Frequenza a scalare, da quando una subnet può aprire gli scambi:
- prime 24 ore: controllo ogni 20 s, giri concatenati senza buchi (il calendario GitHub da solo salta molti giri);
- da 1 a 7 giorni: ogni 60 s, sempre senza buchi;
- oltre 7 giorni, e quando nessuna subnet è pronta: un controllo a ogni giro del calendario (in pratica ~ogni ora).

Affidabilità: 3 nodi RPC in alternanza; un avviso non consegnato da ntfy viene ritentato al controllo successivo;
avviso se i nodi non rispondono o se la struttura della catena cambia; avviso giornaliero silenzioso di funzionamento
(se una mattina non arriva, il sistema è fermo); riattivazione settimanale del calendario contro lo spegnimento dopo 60 giorni.

Canale ntfy: segreto o variabile `NTFY_TOPIC`. Stato in cache di Actions. Avvio a mano con "prova" = notifica di test.
