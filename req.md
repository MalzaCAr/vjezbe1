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
