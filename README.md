# Movie Theatre Management System

---

## 1. Įvadas

### Kokia tai programa?
Ši programa yra kino teatro valdymo sistema, sukurta naudojant Python programavimo kalbą. Sistema leidžia vartotojams valdyti filmų įrašus, kurti ir redaguoti seansus, stebėti sėdimų vietų užimtumą ir atlikti bilietų rezervacijas. Ji taip pat saugo duomenis tekstiniuose failuose (movies.txt, shows.txt, bookings.txt), todėl programa gali išlaikyti informaciją tarp paleidimų.

### Kaip paleisti programą?
1. Įsitikinkite, kad įdiegta Python 3.x versija;
2. Išsaugokite programą faile movie_theatre.py;
3. Paleiskite programą:
```bash
python movie_theatre.py
```
Programa automatiškai paleis main() funkciją.

### Kaip naudotis šia programa?
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
Encapsulation leidžia apsaugoti objekto duomenis nuo neteisingo ar neleistino keitimo, apribojant tiesioginę prieigą prie jų.
Vienas aiškiausių encapsulation pavyzdžių yra Seat klasėje:

```python
self.__is_booked = False
```

Atributas __is_booked yra privatus, todėl negali būti tiesiogiai pasiekiamas ar keičiamas iš išorės.
Būsena keičiama per metodus:
```python
def book_seat(self):
```
```python
def release_seat(self):
```
Tai užtikrina, kad vietos būsena gali būti keičiama tik kontroliuojamu būdu, taip išvengiant loginių klaidų, pavyzdžiui, bandymo rezervuoti jau užimtą vietą.

### Inheritance
Inheritance leidžia kurti naujas klases, remiantis jau egzistuojančiomis klasėmis, taip pakartotinai naudojant jų savybes ir metodus.
Pavyzdžiui, bazinė klasė Person apibrėžia bendrą atributą name:
```python
class Person:
    def __init__(self, name):
        self.name = name
```
Klasė Customer paveldi šią savybę iš Person:
```python
class Customer(Person):
    def __init__(self, customer_id, name):
        super().__init__(name)
        self.customer_id = customer_id
```
Customer klasė paveldi name atributą iš Person klasės ir papildomai įveda naują atributą customer_id, taip išplečiant bazinės klasės funkcionalumą.

### Polymorphism
Polymorphism leidžia naudoti tą patį metodą skirtinguose objektuose, bet jo realizacija gali skirtis priklausomai nuo klasės.
Bazinė klasė Ticket apibrėžia metodą calculate_total():
```python
class Ticket:
    def calculate_total(self):
        return self.base_price
```
Šis metodas yra perrašomas paveldėtose klasėse:
```python        
class RegularTicket(Ticket):
    def calculate_total(self):
        return self.base_price
```
```python
class VIPTicket(Ticket):
    def calculate_total(self):
        return self.base_price + 5
```
Metodas calculate_total() egzistuoja visose klasėse, tačiau jo veikimas skiriasi: RegularTicket grąžina bazinę kainą, o VIPTicket prideda papildomą mokestį.

### Aggregation
Aggregation apibrėžia ryšį tarp klasių, kai viena klasė savo struktūroje naudoja kitų klasių objektus kaip sudedamąsias dalis, tačiau šie objektai gali egzistuoti nepriklausomai.
Booking klasė apjungia kelis skirtingus objektus:
```python
class Booking:
    def __init__(self, booking_id, customer, show, ticket):
        self.booking_id = booking_id
        self.customer = customer
        self.show = show
        self.ticket = ticket
```
Booking klasė naudoja Customer, Show ir Ticket objektus, kurie egzistuoja atskirai ir gali būti naudojami nepriklausomai nuo rezervacijos.

### Design Pattern – Factory Method
Factory Method yra kūrimo dizaino šablonas, leidžiantis kurti objektus neatskleidžiant konkrečios jų klasės, o naudojant bendrą kūrimo metodą.
Šis šablonas realizuotas TicketFactory klasėje:
```python
class TicketFactory:
    @staticmethod
    def create_ticket(ticket_choice, seat_number, base_price):
        if ticket_choice == "1":
            return RegularTicket(seat_number, base_price)
        if ticket_choice == "2":
            return VIPTicket(seat_number, base_price)
        return None
```
TicketFactory klasė atsakinga už tinkamo bilieto objekto sukūrimą pagal vartotojo pasirinkimą. Vietoj tiesioginio objektų kūrimo (RegularTicket ar VIPTicket), naudojamas bendras metodas create_ticket(), kuris grąžina atitinkamą objektą.

---

## 3. Rezultatai
- Sistema sėkmingai realizuoja pagrindines kino teatro valdymo funkcijas: filmų, seansų, vietų ir rezervacijų administravimą.
- Tinkamai sujungtos skirtingos klasės (Movie, Show, Seat, Booking) veikia kaip viena sistema.
- Naudojant validacijos funkcijas užtikrinama, kad vartotojas negalėtų įvesti neteisingų duomenų.

---

## 4. Išvada
Ši programa realizuoja pilną kino teatro valdymo sistemą, naudojant objektinio programavimo principus. Enkapsuliacija užtikrina duomenų saugumą, paveldėjimas leidžia išvengti kodo dubliavimo, polimorfizmas suteikia lankstumą dirbant su skirtingais bilietų tipais, agregacija modeliuoja realius objektų ryšius, o Factory Method šablonas leidžia efektyviai kurti objektus. Visa sistema suskaidyta į aiškias valdymo klases, kurios koordinuoja skirtingas funkcijas ir užtikrina tvarkingą bei išplečiamą architektūrą.

---

## 5. Kaip galima patobulinti?
- Pridėti daugiau bilietų tipų (pvz., studentų, vaikų, senjorų).
- Naudoti duomenų bazę vietoje tekstinių failų.
- Įtraukti vietų pasirinkimą pagal salės schemą.
