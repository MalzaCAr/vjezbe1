
## Sequence dijagram
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


## Kratki opis sequence dijagrama
Ovaj sequence dijagram prikazuje jedan konkretan scenarij: student se prijavljuje na odabrani termin konzultacija ili laboratorija.
Sudionici u scenariju su Student, Korisničko sučelje, Sustav i Baza podataka.
Student preko sučelja šalje zahtjev za prijavu. Sustav provjerava podatke o terminu i broj slobodnih mjesta. Ako termin ima slobodnih mjesta, prijava se sprema u bazu i student dobiva potvrdu. Ako nema slobodnih mjesta, sustav vraća poruku o grešci.


## Slika sequence dijagrama
<img width="788" height="622" alt="sequnce" src="https://github.com/user-attachments/assets/331b380a-98e1-4bd9-95de-136d83cd0518" />


<!-- napravili Luka Hat i Antun Abičić --> 
