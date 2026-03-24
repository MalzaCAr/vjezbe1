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

#napravili Luka Hat i Antun Abičić 
