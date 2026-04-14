# Movie Theatre Management System

---

## 1. Įvadas

### a. Kas yra ši programa?
Ši programa yra kino teatro valdymo sistema, sukurta naudojant Python programavimo kalbą. Sistema leidžia vartotojams valdyti filmų įrašus, seansų tvarkaraščius, sėdimų vietų prieinamumą ir bilietų rezervacijas. Ji taip pat saugo duomenis teksto failuose, kad įrašai galėtų būti vėl įkelti, kai programa yra atnaujinta/perkrauta.

---

### b. Kaip paleisti programą?
1. Įsitikinkite, kad įdiegta Python 3.x versija;
2. Išsaugokite programą faile movie_theatre.py;
3. Patikrinkite, kad failo pradžioje yra:
from datetime import datetime
4. Įsitikinkite, kad programos paleidimo dalis yra:
if __name__ == "__main__":
    main()
5. Paleiskite programą terminale python movie_theatre.py.

---

### c. Kaip naudotis čia programa?
Paleidus programą, vartotojui pateikiamas pagrindinis meniu:

- Movie Records– leidžia pridėti, redaguoti, ištrinti bei peržiūrėti filmus.  
- Show Management– skirtas kurti ir valdyti seansus filmams.  
- Seat Management – leidžia peržiūrėti vietas (jos užimtos ar laisvos).  
- Booking Management – leidžia rezervuoti bilietus.  
- Exit – uždaro programą.  

---

## 2. Kodo analizė
Šis projektas vadovaujasi keliais pagrindiniais objektinio programavimo (OOP) principais:

### Encapsulation

Naudojama klasėje Seat:

class Seat:
    def __init__(self, seat_number):
        self.seat_number = seat_number
        self.__is_booked = False

__is_booked yra privatus ir pasiekiamas tik per metodus:
book_seat(), release_seat(), is_booked()

---

### Inheritance

class Customer(Person):

Customer paveldi Person.

Taip pat:
RegularTicket ir VIPTicket paveldi Ticket.

---

### Polymorphism

def calculate_total(self):

VIPTicket perrašo metodą:

return self.base_price + 5

---

### Method Overriding

def get_ticket_type(self):

Skirtingos klasės grąžina skirtingas reikšmes.

---

### Abstraction

Ticket klasė slepia sudėtingumą ir suteikia bendrus metodus:
calculate_total(), generate_ticket_info()

---

### Aggregation

Show turi Movie  
Booking turi Customer ir Show  

---

### Design Pattern (Factory)

if ticket_choice == "1":
    ticket = RegularTicket(...)
elif ticket_choice == "2":
    ticket = VIPTicket(...)

Šioje vietoje objektas sukuriamas priklausomai nuo vartotojo pasirinkimo. Nors nėra atskiros Factory klasės, ši logika atitinka Factory Pattern idėją – objektų kūrimas yra valdomas centralizuotai ir priklauso nuo sąlygų.

---

## 4. 

