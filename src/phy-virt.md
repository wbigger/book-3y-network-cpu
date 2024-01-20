# Memoria fisica e memoria virtuale

Quando noi eseguiamo un programma cliccando sull'icona del suo eseguibile, accadono le seguenti cose:

1. il sistema operativo cerca un'area di memoria libera nella RAM
1. il sistema operativo copia il programma dall'hard-disk nella memoria RAM, creando un _processo_
1. il processo viene eseguito a partire dalle istruzioni contenute nel main (nel caso di C/C++)

La zona di memoria in cui viene esattamente copiato il programma dipende da quale zona è libera nel preciso momento in cui viene eseguito, cambiando quindi ad ogni esecuzione. Questa cosa è molto scomoda in generale per il programmatore, che si troverà ogni volta ad avere dei puntatori a posizione diverse della memoria. Inoltre espone il sistema operativo a diversi tipi di attacchi informatici, perché svela delle informazioni sullo stato attuale della macchina.

Per questi motivi, il sistema operativo crea uno spazio di indirizzamento virtuale, sempre uguale per tutte le applicazioni, e poi si occupa di mappare gli indirizzi virtuali in indirizzi fisici durante l'esecuzione. Più esattamente questa operazione è svolta dal **kernel**, la componente del sistema operativo che gestisce le componenti hardware.

> Il kernel di riferimento da noi utilizzato è **Linux**, essendo open-source, gratuito ed è il più utilizzato in ambito server.

La virtualizzazione offre anche un altro vantaggio: la possibilità di mappare parte della memoria virtuale sull'hard-disk, in caso la memoria fisica fosse esaurita. Questa operazione si chiama _swap_.

<div>
<p align="center">
<img alt="Memoria fisica e virtuale" title="Memoria fisica e virtuale" src='https://upload.wikimedia.org/wikipedia/commons/thumb/6/6e/Virtual_memory.svg/langit-303px-Virtual_memory.svg.png' width='50%'>
</p>
<p align="center">
<em>Memoria fisica e virtuale. Fonte: wikipedia</em>
</p>
</div>

Per convenzione, la memoria virtuale di ogni processo inizia sempre da 0x00; il valore finale dipende dal kernel e dall'architettura della macchina, per il kernel linux e processori x86 a 64 bit, l'ultimo valore è 0x7FFFFFFFFFFF.

| Indirizzo virtuale |
|------------|
| 0x00       |
| 0x01       |
| 0x02       |
| ...        |
| 0x7FFFFFFFFFFF |

Da notare che questo intervallo è lo stesso indipendentemente dalla quantità di memoria fisica installata sulla macchina.
