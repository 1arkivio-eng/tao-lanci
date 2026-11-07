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

Giro ogni 5 minuti; quando una subnet è pronta, ogni giro controlla ogni 20 s per ~9 minuti.
Canale ntfy: segreto `NTFY_TOPIC`. Stato in cache di Actions. Avvio a mano con "prova" = notifica di test.
