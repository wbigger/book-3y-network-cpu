# Gestione della memoria

La memoria è uno dei due componenti principali di un elaboratore elettronico, insieme alla CPU.

Quando parliamo di memoria in questo capitolo, intendiamo sempre la _memoria primaria_, quella a cui il processore ha accesso diretto; generalmente è costituita dalla RAM, ovvero _Random Access Memory_, che si può traddure in _memoria ad accesso casuale_ o meglio in _memoria ad accesso non sequenziale_.

<div>
<p align="center">
<img title="RAM" src='https://github.com/wbigger/book-arch-cpu/blob/master/src/chap1/assets/ram.png?raw=true' width='50%'>
</p>
<p align="center">
<em>Diversi tipi di RAM. Fonte: wikipedia</em>
</p>
</div>

La caratteristica principale della memoria RAM è che, come dice il nome, si può accedere a qualsiasi parte di questo tipo di memoria
semplicemente conoscendone _l'indirizzo_, rappresentato da un numero intero.

> Al contrario, altri tipi di memoria come l'hard-disk, devono essere acceduti a cluster: per poter accedere ad una certa porzione di memoria, bisogna sapere in che cluster appartiene. In base alla posizione del cluster, potrebbe volerci più o meno tempo per accedere ad un certo dato.

Possiamo immaginare la RAM come un lunghissimo nastro, diviso in caselle, proprio come il nastro della macchina di Turing che abbiamo studiato ad inizio anno.

<div>
<p align="center">
<img title="Turing machine" src='https://github.com/wbigger/book-arch-cpu/blob/master/src/chap1/assets/turing-machine.jpg?raw=true' width='70%'>
</p>
<p align="center">
<em>Un esempio di macchina di Turing. Fonte: wikipedia</em>
</p>
</div>

Per convenzione e comodità, si usano i numeri esadecimali per indicare l'indirizzo di memoria a cui vogliamo accedere. Useremo inoltre la convenzione di scrivere gli indirizzi di memoria in verticale, con i numeri più bassi in alto.

Facciamo un esempio: immaginiamo una memoria RAM di 4GB, ovvero 2^32 bit. L'indirizzo più alto è quindi 2^32 che rappresentato in esadecimale è 0xFFFFFFFF (ricordiamoci che ogni lettera corrisponde a 4 bit). La rappresentazione sarà quindi come segue:


| Indirizzo  |
|------------|
| 0x00       |
| 0x01       |
| 0x02       |
| ...        |
| 0xFFFFFFFF |


> **<p>Esercizio</p>** Un dispositivo ha una memoria fisica di 8GB. Qual è l'ultimo indirizzo della memoria fisica?
Soluzione: 8GB è pari a 2^33, quindi l'ultimo indirizzo in binario si scrive con 33 cifre 1. Per la conversione in esadecimale, partendo da destra, a gruppetti di 4 bit, traduco nella corrispondente lettera. Il risultato finale è quindi *0x1FFFFFFFF*.
