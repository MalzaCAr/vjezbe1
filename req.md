# Projekt: Termini Konzultacija / prijava na labaratorij
## Članovi tima: 
- Fran Crnac
- Luka Hat
- Petar Lukavec
- Ivano Anđelić
- Antun Abičić

## Github repozitorij
- Link: https://github.com/MalzaCAr/vjezbe1
- Svi članovi tima dodani: Da

## User storyji

### User story 1
US-01 Kao student, želim vidjeti sve detalje za pojedini labaratorij kao što su koji ih profesor drži, koliko ECTS bodova donosi, koliko se studenata prijavilo na labaratorij i koji je raspored/kada se održava.

### User story 2
US-02 Kao administrator, želim imati mogućnost kreiranja, uređivanja i brisanja termina konzultacija i laboratorijskih vježbi, postavljanja maksimalnog broja studenata po terminu te pregleda i upravljanja prijavama studenata, kako bih mogao učinkovito organizirati raspored, pratiti popunjenost termina i osigurati ravnomjernu raspodjelu studenata bez preopterećenja pojedinih termina.

## Funkcijski zahtjevi
**FZ-01** Sustav mora omogućiti administratoru kreiranje novog termina konzultacija ili laboratorija.  
**Prioritet:** Visok  
**Kriterij prihvaćanja:** administrator može unijeti naziv termina (obavezno), datum (obavezno), vrijeme (obavezno), vrstu termina (opcionalno) i opis (opcionalno) te se novi termin sprema u sustav. Administrator ne smije moći dodati termin koji nije u radnome vremenu fakulteta.

**FZ-02** Sustav mora omogućiti administratoru postavljanje kapaciteta za svaki termin.  
**Prioritet:** Visok  
**Kriterij prihvaćanja:** administrator pri izradi ili uređivanju termina može postaviti maksimalan broj prijava, a kapacitet se **ispravno** prikazuje uz termin.

**FZ-03** Sustav mora prikazati korisniku popis svih dostupnih termina za konzultacije.  
**Prioritet:** Visok  
**Kriterij prihvaćanja:** korisnik nakon otvaranja pregleda vidi sve aktivne termine s datumom, vremenom i kapacitetom.

**FZ-04** Sustav mora prikazati popunjenost svakog termina.  
**Prioritet:** Visok  
**Kriterij prihvaćanja:** uz svaki termin prikazuje se broj prijavljenih korisnika i broj preostalih mjesta. Kada nema više prostora to treba biti naznačeno.

**FZ-05** Sustav mora omogućiti korisniku prijavu i odjavu na odabrani termin na razuman način.  
**Prioritet:** Visok  
**Kriterij prihvaćanja:** korisnik može odabrati termin i uspješno se prijaviti ako termin ima slobodna mjesta i ako već nije prijavljen. Slično i za odjavu, korisnik se može odjaviti s termina ako je prijavljen. Prijava je moguća 12 sati(?) prije termina isto kao i odjava.

**FZ-06** Sustav mora omogućiti administratoru pregled popisa prijavljenih korisnika za odabrani termin.  
**Prioritet:** Srednji  
**Kriterij prihvaćanja:** administrator odabirom termina vidi popis svih trenutno prijavljenih korisnika.

**FZ-07** Sustav mora omogućiti administratoru uređivanje i brisanje postojećih termina.  
**Prioritet:** Srednji  
**Kriterij prihvaćanja:** administrator može promijeniti podatke termina ili obrisati termin, a promjene se odmah odražavaju u prikazu korisnicima. Editing je moguć 24 sati prije termina. Brisanje do roka kada je termin.

**FZ-08** Sustav automatski onemogućava prijavu kada se dostigne maksimalan kapacitet termina.

**Prioritet:** Srednji

**Kriterij prihvaćanja:** Kada broj prijavljenih studenata dosegne maksimalni kapacitet, sustav više ne dopušta nove prijave te javlja grešku, a terminu pridodaje status "popunjen".

**FZ-09** Sustav omogućuje studentu da filtrira slobodne termine ovisno o datumu i predmetu.

**Prioritet:** Nizak

**Kriterij prihvaćanja:** Student može odabrati datum i/ili predmet kao kriterij filtriranja te sustav prikazuje termine koji odgovaraju kriterijima, ako postoje.

**FZ-10** Sustav omogućava korisniku da vidi svoje trenutno prijavljene termine.

**Prioritet:** Nizak

**Kriterij prihvaćanja:** Korisnik može pristupiti pregledu svojih prijavljenih termina i osnovnih informacija termina.

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
   
