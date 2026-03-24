<!-- napravili Luka Hat i Antun Abičić --> 
# SEQUENCE

### PlantUML kod
```plantuml
@startuml
actor Student
participant "Korisničko sučelje" as UI
participant "Sustav" as SYS
database "Baza podataka" as DB

Student -> UI : Klik na "Prijava na termin"
UI -> SYS : Zahtjev za prijavu

alt Korisnik nije autentificiran
    SYS --> UI : Poruka "Potrebna je prijava u sustav"
    UI --> Student : Prikaz poruke
else Korisnik je autentificiran
    SYS -> DB : Dohvati termin
    DB --> SYS : Podaci o terminu

    alt Ima slobodnih mjesta
        SYS -> DB : Spremi prijavu
        DB --> SYS : Prijava uspješno spremljena
        SYS --> UI : Potvrda prijave
        UI --> Student : Prikaz uspješne prijave
    else Termin je popunjen
        SYS --> UI : Poruka "Nema slobodnih mjesta"
        UI --> Student : Prikaz greške
    end
end

@enduml

```

## Kratki opis sequence dijagrama
Ovaj sequence dijagram prikazuje jedan konkretan scenarij: student se prijavljuje na odabrani termin konzultacija ili laboratorija.
Sudionici u scenariju su Student, Korisničko sučelje, Sustav i Baza podataka.
Student preko sučelja šalje zahtjev za prijavu. Sustav provjerava podatke o terminu i broj slobodnih mjesta. Ako termin ima slobodnih mjesta, prijava se sprema u bazu i student dobiva potvrdu. Ako nema slobodnih mjesta, sustav vraća poruku o grešci.

## Slika sequence dijagrama
<img width="788" height="622" alt="sequnce" src="https://github.com/user-attachments/assets/331b380a-98e1-4bd9-95de-136d83cd0518" />

<!-- napravio Petar Lukavec --> 
# Class diagram

PlantUML kod za class diagram:

```plantuml
@startuml
skinparam classAttributeIconSize 0
skinparam linetype ortho

title Class Diagram - Sustav za termine konzultacija i laboratorija

enum VrstaTermina {
  KONZULTACIJE
  LABORATORIJ
}

enum StatusTermina {
  OTVOREN
  POPUNJEN
  ZATVOREN
  OTKAZAN
}

enum StatusPrijave {
  AKTIVNA
  ODJAVLJENA
  ODBIJENA
}

abstract class Korisnik {
  - korisnikId: Long
  - ime: String
  - prezime: String
  - email: String
  - lozinkaHash: String
  + prijava(): void
  + odjava(): void
}

class Student {
  - jmbag: String
  - godinaStudija: int
  + pregledPrijavljenihTermina(): void
  + filtrirajTermine(): void
}

class Administrator {
  - zaposlenikId: String
  - odjel: String
  + kreirajTermin(): void
  + urediTermin(): void
  + obrisiTermin(): void
  + pregledPrijava(): void
}

Korisnik <|-- Student
Korisnik <|-- Administrator

class Predmet {
  - predmetId: Long
  - naziv: String
  - sifraPredmeta: String
  - semestar: int
}

class Lokacija {
  - lokacijaId: Long
  - nazivProstorije: String
  - kapacitetProstorije: int
}

class Termin {
  - terminId: Long
  - naziv: String
  - datum: Date
  - vrijemePocetka: Time
  - vrijemeZavrsetka: Time
  - vrsta: VrstaTermina
  - opis: String
  - kapacitet: int
  - status: StatusTermina
  + imaSlobodnihMjesta(): boolean
  + zatvoriPrijave(): void
  + azurirajStatus(): void
}

class Prijava {
  - prijavaId: Long
  - vrijemePrijave: DateTime
  - statusPrijave: StatusPrijave
  + potvrdi(): void
  + otkazi(): void
}

class Obavijest {
  - obavijestId: Long
  - naslov: String
  - sadrzaj: String
  - vrijemeSlanja: DateTime
}

class AuditLog {
  - logId: Long
  - opis: String
  - vrijeme: DateTime
  - uspjesno: boolean
}

class AuthService {
  + login(email: String, lozinka: String): String
  + validirajToken(token: String): boolean
  + dohvatiUlogu(token: String): String
}

class TerminService {
  + kreirajTermin(termin: Termin): Termin
  + urediTermin(termin: Termin): Termin
  + obrisiTermin(terminId: Long): void
  + dohvatiDostupneTermine(): List<Termin>
  + filtrirajPoDatumuIPredmetu(datum: Date, predmet: String): List<Termin>
}

class PrijavaService {
  + prijaviStudenta(studentId: Long, terminId: Long): Prijava
  + odjaviStudenta(studentId: Long, terminId: Long): void
  + provjeriKapacitet(terminId: Long): boolean
  + provjeriDupluPrijavu(studentId: Long, terminId: Long): boolean
  + dohvatiPrijavljeneStudente(terminId: Long): List<Student>
}

class BackupService {
  + izradiSigurnosnuKopiju(): void
  + vratiPodatkeIzKopije(): void
}

class NotificationService {
  + posaljiEmail(korisnik: Korisnik, obavijest: Obavijest): void
}

Student -- Prijava : ima
Termin -- Prijava : sadrzi
Prijava --> Student : pripada
Prijava --> Termin : odnosiSeNa

Predmet -- Termin : sadrzi
Lokacija -- Termin : odrzavaSeU
Administrator -- Termin : upravlja

Korisnik -- Obavijest : prima
Korisnik -- AuditLog : ima

AuthService ..> Korisnik
TerminService ..> Termin
TerminService ..> Predmet
TerminService ..> Lokacija
PrijavaService ..> Prijava
PrijavaService ..> Student
PrijavaService ..> Termin
NotificationService ..> Obavijest
NotificationService ..> Korisnik
BackupService ..> Termin
BackupService ..> Prijava
BackupService ..> Korisnik

@enduml
```

## Kratki opis class diagrama

Ovaj model opisuje strukturu sustava za upravljanje terminima konzultacija i laboratorija te prikazuje glavne klase, korisničke uloge i servisne komponente. Apstraktna klasa `Korisnik` predstavlja zajedničke podatke svih korisnika, dok su `Student` i `Administrator` njezine specijalizacije s različitim odgovornostima. Klasa `Termin` opisuje pojedini termin, a `Prijava` povezuje studenta i termin te omogućuje evidenciju prijava i odjava. Dodatne klase `Predmet` i `Lokacija` služe za organizaciju termina po kolegiju i prostoru održavanja. Klase `Obavijest` i `AuditLog` podržavaju slanje email obavijesti te zapisivanje važnih događaja u sustavu. Veze među klasama prikazuju logične odnose između korisnika, termina i prijava, kao i ovisnosti između domenskih i servisnih komponenti. Po potrebi se model može dodatno proširiti zasebnom klasom za upravljanje sigurnošću lozinki, čime bi se osjetljivi podaci odvojili od osnovnih korisničkih podataka. 

# USE-CASE Dijagram

```plantuml
@startuml

left to right direction

actor Student
actor Administrator

rectangle "Sustav za termine konzultacija i laboratorija" {

  (Pregled termina) as UC1
  (Pregled detalja laboratorija) as UC2
  (Filtriranje termina) as UC3
  (Prijava na termin) as UC4
  (Odjava s termina) as UC5
  (Pregled vlastitih prijava) as UC6

  (Kreiranje termina) as UC7
  (Uređivanje termina) as UC8
  (Brisanje termina) as UC9
  (Pregled prijava) as UC10

  (Termin popunjen) as EX1
  (Već prijavljen) as EX2

  Student -- UC1
  Student -- UC2
  Student -- UC3
  Student -- UC4
  Student -- UC5
  Student -- UC6

  Administrator -- UC7
  Administrator -- UC8
  Administrator -- UC9
  Administrator -- UC10

  UC3 .> UC1 : <<include>>
  UC4 .> UC1 : <<include>>
  UC8 .> UC1 : <<include>>
  UC9 .> UC1 : <<include>>
  UC10 .> UC1 : <<include>> 

  EX1 .> UC4 : <<extend>>
  EX2 .> UC4 : <<extend>>

}

@enduml
```

## Opis modela

Ovaj Use Case dijagram prikazuje funkcionalnosti sustava za upravljanje terminima konzultacija i laboratorija te interakciju dvaju aktera: studenta i administratora. Student može pregledavati termine, vidjeti detalje, filtrirati ih te se prijavljivati i odjavljivati, dok administrator može kreirati, uređivati i brisati termine te pregledavati prijave.

Odnosi <<include>> označavaju obavezne podkorake, pa tako više funkcionalnosti uključuje pregled termina jer je za njih potrebno prvo odabrati termin. Odnosi <<extend>> prikazuju iznimne situacije koje se mogu dogoditi prilikom prijave, kao što su pokušaj prijave na popunjen termin ili dupla prijava.

Dijagram time jasno prikazuje glavne funkcionalnosti sustava, uloge korisnika i osnovne scenarije korištenja zajedno s mogućim iznimkama.