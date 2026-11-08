# Dentro o Fuori

Strumento web che dai fotogrammi TV ricostruisce la traiettoria del pallone: capisce se era un tiro o un cross e se, con o senza deviazione, sarebbe finito nello specchio, con il margine di errore.

Tutto gira nel browser: nessun server, nessun dato inviato altrove. I progetti si salvano nel browser e si possono esportare/importare come file `.json`.

## Pubblicazione su GitHub Pages

1. Crea un repository (es. `dentro-o-fuori`) oppure usa una cartella di un repo esistente.
2. Carica `index.html` (e questo `README.md`).
3. Settings → Pages → Source: branch `main`, cartella `/ (root)`.
4. Dopo un minuto il sito è su `https://<tuo-utente>.github.io/dentro-o-fuori/`.

## Come funziona

- **Calibrazione:** dai punti noti del campo (pali, angoli delle aree, dischetto, bandierine) e dai punti toccati lungo le linee (linea di fondo, lati e linea frontale delle aree, linee laterali, lunetta) calcola la corrispondenza immagine ↔ campo e stima la telecamera. Le linee servono quando un angolo è fuori dall'inquadratura o coperto. Il riferimento di altezza (giocatore o palo-traversa) rende più precisa la stima.
- **Traiettoria:** modello balistico senza attrito né effetto. Con i tempi dei fotogrammi stima anche la velocità; senza tempi usa la velocità ipotizzata.
- **Deviazione:** il fotogramma "Momento della deviazione" separa il tiro originale dalla traiettoria dopo il tocco. Lo strumento confronta dove sarebbe arrivato il tiro senza deviazione e dove arriva dopo.
- **Incertezza:** ripete il calcolo molte volte spostando a caso tutti i tocchi di qualche pixel. La percentuale "nello specchio" dice quanto il verdetto regge ai piccoli errori.

## Limiti da conoscere

- Con un solo fotogramma in volo la direzione non è determinabile: lo strumento lo dice e mostra tutte le mire compatibili.
- Ogni fotogramma calibrato a mano introduce piccoli errori indipendenti: se l'inquadratura non cambia, usa "Copia calibrazione dal precedente".
- Servono preferibilmente 5 o più fotogrammi in volo per tratto, con i tempi (a 25 fps ogni fotogramma vale 0,04 s), oppure il punto a terra sotto il pallone.
