# K-Clique to SAT

## Implementare

Pentru analizarea careului de sudoku am verificat corectitudinea acestuia pe linii, regiuni si
coloane (in aceasta ordine), adaugand inca un simbol in alfabet ("-") pentru a "goli" banda de
citire in implementarea pentru verificarea coloanelor.

Pentru linii am folosit starile:
- StartL -> aceasta stare sare peste peste prima * din input si ia primul numar de pe linie
- GasitXYX (XYZ sunt toate combinatiile partitiei {1, 2, 3, 4}) -> in aceste stari iau fiecare cifra si o retin pentru a verifica daca exista numere duplicate (de exemplu, pentru starea Gasit12, daca capul de citire citeste valoarea 1, masina tranzitioneaza in starea N)

Pentru regiuni am folosit starile:
- BackBeginR -> stare folosita pentru a ma intoarce la inceputul inputului dupa verificarealiniilor
- StartR -> similar ca la subpunctul anterior, retin prima cifra
- GasitRXYZ -> stari care retin cifrele gasite in regiune
- SkipXY -> aceste stari sunt folosite pentru a retine cifrele de pe prima linie din regiune si pentru a sarii la urmatoarea linie (intr-un input valid, urmatoarea linie se afla dupa *)
- NextZone1 si NextZone2 -> aceste stari sunt utilizate pentru a prelua liniile din input dupa analizarea unei regiuni/submatrici (Daca ultima linie dintr-o regiune este urmata de *, inseamna ca nu trebuie sa ma intorc cu capul de banda in stanga pentru a gasi prima linie din urmatoarea regiune. Altfel, trebuie sa caut prima linie a regiunii in stanga)

Pentru coloane:
- BackBeginC -> stare folosita pentru intoarcerea la inceputul inputului dupa verificarea unei coloane
- Ignore1* si CheckEmpty -> aceste stari sunt utilizate pentru a retine prima cifra din input numai daca acesta nu este gol (toate cifrele sunt inlocuite cu "-" dupa ce sunt retinute de o stare, practic incerc sa sterg fiecare coloana citita pentru a o retine si verifica pe urmatoarea)
- GasitCXYZ -> analog starilor GasitRXYZ si GasitXYZ	
- Jump\*XYZ -> aceste stari sunt folosite pentru a sari la urmatoarea cifra de pe coloana (cifrele de pe prima coloana se afla dupa simbolul "*" in input, cele de pe a doua dupa "*" si un "-" etc.)
	
Am ales sa introduc inca un simbol in alfabet deoarece altfel nu as fi stiut unde sa ma intorc la stanga pentru fiecare inceput de coloana.
