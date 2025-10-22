# 🃏 Prova d'esame del 17/07/2024

## Descrizione
Si vuole creare un piccolo programma per il **gioco delle carte tipo Scala 40** con carte da ramino  
(4 semi: **Cuori (C), Fiori (F), Picche (P), Quadri (Q)**, 13 carte per seme numerate da 1 a 13).  

Ogni carta è rappresentata dal **seme** (iniziale del seme) e dal **numero**.  
Le carte di ogni giocatore sono memorizzate in una **lista doppia**.

Sono forniti i file:
- `tipo.h` → definizione del tipo carta  
- `liste.h`, `liste.cc` → implementazione delle liste  
- `g1.txt`, `g2.txt` → carte iniziali per i due giocatori (una carta per riga, formato: numero e iniziale del seme)

---

## 📘 Punto 0 – Documentazione & Git

- Documentare il codice in modo che `doxygen` generi la documentazione del progetto nella cartella `doc/`.
- Creare un branch con il proprio **numero di matricola**.
- Eseguire **un commit per ogni punto svolto**.
- Effettuare il push finale al termine della prova (sarà abilitato dal docente).

---

## 🧩 Punto 1 – Preparazione del Gioco
**Valutazione massima: 20 punti**

Creare un progetto con **Makefile** che includa i moduli per le liste e implementi `tipo.cc`.

### Funzioni richieste:
- `int compare(carta a, carta b)`
- Restituisce:
  - `< 0` se la prima carta precede la seconda (per numero o, a parità, per seme)
  - `> 0` se è successiva
  - `0` se sono uguali

- `void pesca(lista& L, int v, char s)`
- Aggiunge alla lista `L` una carta con valore `v` e seme `s`.

- `void stampa(lista L1, lista L2)`
- Stampa le carte delle due liste **a coppie** nella stessa posizione.
- Per ogni coppia:  
  ```
    <carta L1> è maggiore/minore/uguale a <carta L2>
  ```

### `main`
- Chiede il numero di carte da assegnare.
- Legge le carte da `g1.txt` e `g2.txt`.
- Chiama `pesca` più volte per costruire le due liste.
- Richiama `stampa()`.

---

## ♣️ Punto 2.a – Ricerca dei Tris

Aggiungere in `compito.cc`:

```cpp
    int* tris(lista carte);
```
- Conta il numero di tris distinti per valore (3 carte dello stesso numero, anche con lo stesso seme).
- Restituisce un vettore dinamico di dimensione 13.
- Estendere il main() per richiamare la funzione tris() per entrambi i giocatori e stampare i risultati.

Esempio di output:
```
    giocatore 1: 0 1 1 1 0 0 0 0 0 0 0 0 0
    giocatore 2: 1 1 0 0 0 1 0 0 0 0 0 0 0
```
---

## ♦️ Punto 2.b – Gestione della Mano di Gioco

Aggiungere in compito.cc:
```
    int cala(lista& carte);
```

Cerca un tris da calare, lo stampa, lo rimuove dalla lista e restituisce il punteggio del tris.

Il main() deve implementare un turno di gioco:

- Ogni giocatore pesca una carta (input da tastiera).
- Cala tris finché disponibili.
- Aggiorna il punteggio totale.
- Se un giocatore finisce le carte → stampa "Fine gioco" e dichiara il vincitore.

Esempio di output:
```
giocatore 1: pesca 2 Q, cala 2Q 2P 2Q, 3Q 3P 3F, 4Q 4P 4P, punteggio: 27
giocatore 2: pesca 7C, cala 6P 6Q 6P, 7Q 7P 7C, 2Q 2P 2C, 1F 1C 1Q, punteggio: 48
```