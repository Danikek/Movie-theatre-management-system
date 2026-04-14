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
```python
from datetime import datetime
4. Įsitikinkite, kad programos paleidimo dalis yra:
```python
if __name__ == "__main__":
    main()
5. Paleiskite programą terminale python movie_theatre.py.

---

### c. Kaip naudotis čia programa?
Paleidus programą, vartotojui pateikiamas pagrindinis meniu:

- **Movie Records** – leidžia pridėti, redaguoti, ištrinti bei peržiūrėti filmus.  
- **Show Management** – skirtas kurti ir valdyti seansus filmams.  
- **Seat Management** – leidžia peržiūrėti vietas (jos užimtos ar laisvos).  
- **Booking Management** – leidžia rezervuoti bilietus.  
- **Exit** – uždaro programą.  

---

## 2. Kodo analizė
Šis projektas vadovaujasi keliais pagrindiniais objektinio programavimo (OOP) principais:

● Encapsulation
Encapsulation yra naudojama klasėje Seat:
```python
class Seat:
    def __init__(self, seat_number):
        self.seat_number = seat_number
        self.__is_booked = False

Kintamasis __is_booked yra privatus (private)
Jis negali būti pasiekiamas tiesiogiai iš išorės
Prieiga vykdoma tik per metodus:
book_seat()
release_seat()
is_booked()
Tai leidžia apsaugoti duomenis nuo neteisingo keitimo.

●Inheritance
Inheritance naudojamas tarp Person ir Customer:
```bash
class Person:
    def __init__(self, name):
        self.name = name

class Customer(Person):
    def __init__(self, customer_id, name):
        super().__init__(name)
        self.customer_id = customer_id
##Taip pat inheritance pasireiškia tarp:
Ticket (parent)
RegularTicket, VIPTicket (child)

Tai leidžia pakartotinai naudoti kodą bei išplėsti funkcionalumą.

●Polymorphism
Polymorphism naudojamas klasėse:
Ticket
RegularTicket
VIPTicket
```bash
def calculate_total(self):
    return self.base_price
```bash
class VIPTicket(Ticket):
    def calculate_total(self):
        return self.base_price + 5
##Tas pats metodas (calculate_total) elgiasi skirtingai priklausomai nuo objekto tipo.

●Method Overriding
Overriding vyksta, kai child klasė pakeičia parent metodą.
```bash
class RegularTicket(Ticket):
    def get_ticket_type(self):
        return "Regular Ticket"
```bash
class VIPTicket(Ticket):
    def get_ticket_type(self):
        return "VIP Ticket"

●Abstraction
●
## 1. Input validation
Yra naudojamos funkcijos, kurios užtikrina, kad vartotojas įveda teisingus duomenis.:
def calculate_total(self):
    return self.base_price
validate_non_empty()
validate_positive_int()
validate_date()
validate_time()

## 2. File management
Klasė FileManager saugo duomenis į failus:
```bash
movies.txt
shows.txt
bookings.txt

## Taip pat užkrauna duomenis programos paleidimo metu. Tai leidžia išsaugoti informaciją tarp programos paleidimų.

## 3. Movie management
Klasės:
```bash
Movie
MovieManager

## Leidžia:
-pridėti filmą;
-peržiūrėti visus filmus;
-atnaujinti informaciją;
-ištrinti filmą.

## 4. 
python movie_theatre.py
