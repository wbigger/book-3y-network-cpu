# Segmenti di memoria

La memoria assegnata ad un certo processo è divisa in _segmenti_, ovvero porzioni di memoria ognuna con un compito specifico. Di seguito i più importanti.

| Indirizzo  | Settore|
|------------|--------|
| 0x00       | Codice (text) |
| ...       | Variabili Statiche|
| ...        |Heap|
| ...        |  |
| 0x7FFFFFFFFFFF |Stack|

## Segmento del codice (text)

La prima porzione di memoria contiene le istruzioni che dovranno essere eseguite durante il processo; questo settore viene chiamato _code_ o anche _text_. Le istruzioni vengono memorizzate in memoria in accordo con l'architettura specifica del processore, e possono essere visualizzate in maniera comprensibile all'essere umano attraverso la rappresentazione Assembly.

Prendiamo ad esempio una funzione in C che esegue la somma di due numeri. Di seguito vediamo come questo viene tradotto in Assembly, e come ad ogni riga di Assembly corrispondano dei valori esadecimali. Questi valori sono quelli che si trovano nel segmento di memoria del codice.

<iframe width="800px" height="200px" src="https://godbolt.org/e?readOnly=true&hideEditorToolbars=true#g:!((g:!((g:!((h:codeEditor,i:(filename:'1',fontScale:14,fontUsePx:'0',j:1,lang:___c,selection:(endColumn:16,endLineNumber:2,positionColumn:16,positionLineNumber:2,selectionStartColumn:16,selectionStartLineNumber:2,startColumn:16,startLineNumber:2),source:'int+somma(int+a,int+b)+%7B%0A++++return+a%2Bb%3B%0A%7D'),l:'5',n:'0',o:'C+source+%231',t:'0')),k:45.71428571428573,l:'4',n:'0',o:'',s:0,t:'0'),(g:!((h:compiler,i:(compiler:cg132,filters:(b:'0',binary:'1',binaryObject:'0',commentOnly:'0',debugCalls:'1',demangle:'0',directives:'0',execute:'0',intel:'0',libraryCode:'0',trim:'1'),flagsViewOpen:'1',fontScale:14,fontUsePx:'0',j:1,lang:___c,libs:!(),options:'',overrides:!(),selection:(endColumn:1,endLineNumber:1,positionColumn:1,positionLineNumber:1,selectionStartColumn:1,selectionStartLineNumber:1,startColumn:1,startLineNumber:1),source:1),l:'5',n:'0',o:'+x86-64+gcc+13.2+(Editor+%231)',t:'0')),k:54.28571428571431,l:'4',n:'0',o:'',s:0,t:'0')),l:'2',n:'0',o:'',t:'0')),version:4"></iframe>

## Segmento delle variabili statiche

Subito dopo vengono memorizzate tutte quelle variabili che nascono con l'avvio del programma e vengono distrutte solo alla conclusione dello stesso. Rientrano in questa categoria ad esempio tutte le variabili globali e le variabili locali che vengono dichiarate con il modificatore _static_.

## Segmenti Stack & Heap

I settori precedenti hanno una dimensione fissa, nota all'avvio del programma. Tuttavia, durante l'esecuzione del programma stesso, le variabili che creiamo all'interno delle funzioni non sono note a priori, perché una funzione potrebbe essere chiamata più volte, oppure mai.

Esistono quindi due ulteriori settori che evolvono con l'esecuzione del programma stesso, chiamate _stack_ (catasta, a sinistra nella foto) e _heap_ (mucchio, a destra nella foto).

<p class="centered">
<img class="w80p" src="https://github.com/wbigger/book-cs-3y/raw/master/src/02-sorting/assets/stack-heap.jpg?raw=true" alt="Stack and heap" title="Stack and heap">
</p>

### Stack

La stack è una memoria a cui si può aggiungere una nuova variabile solo aggiungendola in cima, ed analogamente si possono togliere variabili solo dalla cima. Questa memoria viene gestita automaticamente dal compilatore e dal processore: ogni volta che creiamo una variabile, viene aggiunta alla stack; ogni volta che usciamo dall'ambito della variabile (in inglese, _scope_), questa variabile viene distrutta. Si esce dallo scope della variabile appena si raggiunge la parentesi graffa in cui è contenuta.

```c
int somma(int a, int b) {
    if (a > 0) {
        int c = a+b;
        return c;
    } // <-- qui viene distrutta la variabile c
} // qui vengono distrutte le variabili a e b
```

Per convenzione, la stack parte nello spazio di indirizzamento più alto disponibile della memoria virtuale e cresce verso gli indirizzi più bassi.

### Heap

La gestione automatica della stack a volte può essere limitante, perché non sempre lo scope reale della variabile corrisponde con quello del blocco in cui si trova. Per questo motivo esiste la heap, dove si ha maggiore controllo su quando distruggere la variabile, che può quindi passare da un blocco ad un altro (ad esempio può essere passato facilmente ad una o più funzioni).

> Se non si cancellano correttamente le variabili nella heap, può succedere che aree di memoria vengano sprecate. Questo fenomeno si chiama _memory leak_ ed è un problema a cui bisogna prestare la massima attenzione. Alcuni linguaggi come Java, Python o Rust hanno dei meccanismi per evitare che si verifichino i memory leaks.
