## Nefunkcijski zahtjevi

### NZ-01 (Performanse)
Sustav mora prikazati dostupne termine konzultacija i laboratorija u roku od najviše 2 sekunde za najmanje 95% zahtjeva.

**Prioritet:** Visok  

**Kriterij prihvaćanja:**  
Mjerenjem vremena odziva utvrđuje se da najmanje 95% zahtjeva ima vrijeme odziva ≤ 2 sekunde.


### NZ-02 (Logiranje i praćenje)
Sustav mora zabilježiti 100% neuspješnih rezervacija s opisom greške i vremenom događaja te mora bilježiti 100% prijava i odjava termina, uključujući identitet korisnika i vrijeme akcije.

**Prioritet:** Srednji  

**Kriterij prihvaćanja:**  
Pregledom logova mora biti vidljivo da su sve neuspješne rezervacije i sve prijave/odjave evidentirane s pripadajućim podacima.


### NZ-03 (Integritet podataka)
Sustav mora spriječiti dupliciranje prijava tako da za isti termin i korisnika postoji najviše jedna aktivna prijava (0% duplikata).

**Prioritet:** Visok  

**Kriterij prihvaćanja:**  
Pokušaj višestruke prijave na isti termin za istog korisnika mora biti odbijen.


### NZ-04 (Sigurnost)
Sustav mora zahtijevati autentifikaciju korisnika prije pristupa funkcijama prijave na termine.

**Prioritet:** Visok  

**Kriterij prihvaćanja:**  
Neautentificirani korisnik ne može pristupiti funkcijama prijave na termine niti izvršiti rezervaciju.


### NZ-05 (Sigurnosne kopije i oporavak)
Sustav mora izrađivati sigurnosne kopije podataka najmanje jednom dnevno te omogućiti povrat podataka unutar 1 sata od kvara.

**Prioritet:** Srednji  

**Kriterij prihvaćanja:**  
Simulacijom kvara sustava podaci se moraju uspješno vratiti iz sigurnosne kopije unutar 1 sata.


### NZ-06 (Arhitektura i autentifikacija)
Sustav mora biti implementiran kao mikroservisna aplikacija, a pristup zaštićenim dijelovima sustava mora biti omogućen isključivo korištenjem autentifikacijskih tokena (npr. JWT).

**Prioritet:** Visok  

**Kriterij prihvaćanja:**  
Svaki zahtjev prema zaštićenim dijelovima sustava mora sadržavati valjan autentifikacijski token; zahtjevi bez tokena ili s nevažećim tokenom moraju biti odbijeni.
