# CISC & RISC

> Vedi libro pag. 130-138.

Fin dai primi processori, si sono distinte due diverse filosofie per i processori:
- **CISC**: ha tante istruzioni (op.code) diverse, ognuna molto complessa; servono meno istruzioni per realizzare un programma dato, ma ogni istruzione è più lenta.
- **RISC**: ha poche istruzioni (op.code) diverse, ognuna semplice; servono più istruzioni per realizzare un programma dato, ma ogni istruzione è più veloce, inoltre è particolarmene adatta alla tecnica del pipelining.

La formula per calcolare il tempo complessivo di un dato programma è:

\\[ tempo = \frac{tempo}{cicli} \frac{cicli}{istruzioni} istruzioni \\]

Il rapporto \\(\frac{tempo}{cicli}\\) è la velocità di clock del processore. CISC cerca di ridurre il numero di \\(istruzioni\\) sacrificando il rapporto \\(\frac{cicli}{istruzioni}\\); l'architettura RISC all'opposto cerca di ridurre il rapporto \\(\frac{cicli}{istruzioni}\\) sacrificando il numero di \\(istruzioni\\).

>> Vedi per approfondimenti [questa](https://cs.stanford.edu/people/eroberts/courses/soco/projects/risc/risccisc/) pagina.

Un altro fattore da tenere in considerazione è la potenza consumata, che viene calcolata come:

\\[ Energia = Potenza * Tempo \\]

Le architetture RISC hanno una potenza dissipata molto minore rispetto alle architetture CISC, anche se il tempo può essere un po' maggiore, quindi le rendono una scelta quasi obbligata per i dispositivi mobile. Anche per i data center, un minore consumo di energia vuol dire risparmiare sui costi di gestione, sia sull'alimentazione diretta dei server che per il sistema di raffreddamento.

> I data center consumano moltissima energia e sono a rischio incendio. Un incidente abbastanza recente è stato quello del gestore OVH a Strasburgo, in Francia.
![OVH fire](https://media.datacenterdynamics.com/media/images/sdis_67_ovhcloud_fire.width-358.jpg)

In generale, negli ultimi anni stiamo vedendo un vantaggio competitivo netto del RISC rispetto a CISC, che ne stanno determinando una sempre maggiore diffusione.
