# Compiler Explorer

Vediamo nel dettaglio cosa succede quando compiliamo un programma.

> Useremo come liguaggio C, ma qualsiasi linguaggio viene convertito in codice Assembly (ASM).

Usiamo il sito [Compiler Explorer](https://godbolt.org/), che permette di vedere in modo interattivo cosa succede ad un codice compilato.

> Da linea di comando, usando `gcc`, è possibile vedere il codice ASM usando l'opzione `-S`.

Come caso di studio, riprendiamo l'esempio della somma.

<iframe width="800px" height="200px" src="https://godbolt.org/e#g:!((g:!((g:!((h:codeEditor,i:(filename:'1',fontScale:14,fontUsePx:'0',j:1,lang:___c,selection:(endColumn:2,endLineNumber:3,positionColumn:1,positionLineNumber:3,selectionStartColumn:2,selectionStartLineNumber:3,startColumn:1,startLineNumber:3),source:'int+somma(int+a,int+b)+%7B%0A++++return+a%2Bb%3B%0A%7D'),l:'5',n:'0',o:'C+source+%231',t:'0')),k:45.71428571428573,l:'4',n:'0',o:'',s:0,t:'0'),(g:!((h:compiler,i:(compiler:cg132,filters:(b:'0',binary:'1',binaryObject:'1',commentOnly:'0',debugCalls:'1',demangle:'0',directives:'0',execute:'0',intel:'0',libraryCode:'0',trim:'1'),flagsViewOpen:'1',fontScale:14,fontUsePx:'0',j:1,lang:___c,libs:!(),options:'',overrides:!(),selection:(endColumn:12,endLineNumber:10,positionColumn:9,positionLineNumber:2,selectionStartColumn:12,selectionStartLineNumber:10,startColumn:9,startLineNumber:2),source:1),l:'5',n:'0',o:'+x86-64+gcc+13.2+(Editor+%231)',t:'0')),k:54.28571428571431,l:'4',n:'0',o:'',s:0,t:'0')),l:'2',n:'0',o:'',t:'0')),version:4"></iframe>

Vediamo passo passo come le 3 linee di codice C diventano le linee di codice ASM.

## Linea 1: definizione di una funzione
Per la prima linea abbiamo la seguente traduzione:

```c
// Codice C
int somma(int a,int b) {
```

```nasm
; Codice ASM
push    rbp
mov     rbp, rsp
mov     DWORD PTR [rbp-4], edi
mov     DWORD PTR [rbp-8], esi
```

Quando viene chiamata una funzione, per prima cosa con il comando `push` viene salvato il vecchio valore del Base Pointer (`rbp`), il registro che punta sempre all'indirizzo di memoria all'inizio della funzione corrente. Questo valore verrà ripristinato alla fine della funzione.

Quindi, con `mov     rbp, rsp`, il valore del Base Pointer viene assegnato all'indirizzo dell'attuale cima della stack.

> Nota: essendo un'architettura a 64bit (Intel `x86_64`), i registri degli indirizzi sono a 64bit, e questo è visibile perché i nomi cominciano con la lettera `r` (come `rbp`). I registri a 32bit cominciano con la `e` (come `eax`) ed i registri a 16 bit sono formati da solo due lettere (ex. `ax`). Altre architetture (es. `arm`) usano altre convenzioni.

Infine, con le ultime due istruzioni vengono copiati nella stack i valori dei registri `edi` ed `esi`, che contengono i parametri di ingresso `a` e `b`. La posizione in cui vengono copiati dipende dalla dimensione dei valori da copiare: in questo caso essendo `int`, hanno una dimensione di 4 byte, quindi il primo viene copiato in `rbp - 4` ed il secondo in `rbp - 8`. Questi valori detti di _offset_ sono negativi perché, come detto in precedenza, la stack parte dai valori alti di memoria e _cresce_ verso i valori bassi, quindi gli offset devono essere sottratti all'indirizzo di partenza della funzione.

## Linea 2: corpo della funzione

Abbiamo la seguente traduzione della seconda linea.
```c
return a+b;
```

```asm
mov     edx, DWORD PTR [rbp-4]
mov     eax, DWORD PTR [rbp-8]
add     eax, edx
```

Nelle prime due linee, il processore copia i valori dalla stack nei registri `edx` e `eax`; questi sono i registri che vengono usati dall'ALU per le operazioni.

Nell'ultima riga, l'ALU fa la somma dei valori nei registri indicati e salva il risultato dell'operazione nel primo registro indicato, in questo caso `eax`.

## Linea 3: uscita da una funzione

Abbiamo infine la traduzione dell'ultima linea.

```c
}
```

```asm
pop     rbp
ret
```

Il comando `pop` riassegna nuovamente al registro `rbp` il valore salvato nel comando `push`, infine il comando `ret` fa saltare l'esecuzione alla funzione che ha chiamato.

Ricordiamo che il valore ritornato dalla funzione è sempre all'interno del registro `eax`.
