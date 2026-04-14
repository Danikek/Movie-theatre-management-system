# Movie Theatre Management System

---

## 1. Įvadas

### Kokia tai programa?
Ši programa yra kino teatro valdymo sistema, sukurta naudojant Python programavimo kalbą. Sistema leidžia vartotojams valdyti filmų įrašus, seansų tvarkaraščius, sėdimų vietų prieinamumą ir bilietų rezervacijas. Ji taip pat saugo duomenis teksto failuose, kad įrašai galėtų būti vėl įkelti, kai programa yra atnaujinta/perkrauta.

---

### Kaip paleisti programą?
1. Įsitikinkite, kad įdiegta Python 3.x versija;
2. Išsaugokite programą faile movie_theatre.py;
3. Programa paleidžiama vykdant pagrindinį failą, kuriame yra main() funkcija:

if __name__ == "__main__":
    main()

4. Paleidus programą, vartotojui pateikiamas pagrindinis meniu, leidžiantis pasirinkti norimą funkcionalumą.

---

### Kaip naudotis čia programa?
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
Encapsulation reiškia duomenų ir su jais susijusios logikos apjungimą klasėje bei duomenų apsaugojimą nuo tiesioginio išorinio keitimo.

Vienas aiškiausių enkapsulation pavyzdžių yra Seat klasėje:

class Seat:
    def __init__(self, seat_number):
        self.seat_number = seat_number
        self.__is_booked = False

Čia atributas __is_booked yra privatus, todėl jis negali būti tiesiogiai keičiamas iš kitų klasių.
Vietoj to naudojami metodai:

def book_seat(self):
    if self.__is_booked:
        return False
    self.__is_booked = True
    return True

def release_seat(self):
    if not self.__is_booked:
        return False
    self.__is_booked = False
    return True

Vietos būsena keičiama tik per metodus, o ne tiesiogiai. Tai apsaugo nuo neteisingo duomenų keitimo (pvz., neleidžia rezervuoti jau užimtos vietos).

### Paveldėjimas (Inheritance)
Inheritance leidžia kurti naujas klases remiantis jau egzistuojančiomis.

class Person:
    def __init__(self, name):
        self.name = name

class Customer(Person):
    def __init__(self, customer_id, name):
        super().__init__(name)
        self.customer_id = customer_id

Customer paveldi name atributą iš Person. Papildomai prideda customer_id.

### Polymorphism
Polymorphism leidžia naudoti tą patį metodą skirtingiems objektams, tik jis elgiasi skirtingai. 

class Ticket:
    def calculate_total(self):
        return self.base_price
        
class RegularTicket(Ticket):
    def calculate_total(self):
        return self.base_price
        
class VIPTicket(Ticket):
    def calculate_total(self):
        return self.base_price + 5

Metodas calculate_total() egzistuoja visose klasėse, bet VIP bilietas prideda papildomą mokestį.

### Aggregation
Aggregation reiškia, kad viena klasė naudoja kitą kaip savo dalį.

class Booking:
    def __init__(self, booking_id, customer, show, ticket):
        self.booking_id = booking_id
        self.customer = customer
        self.show = show
        self.ticket = ticket

Booking turi Customer, Show ir Ticket. Tai reiškia, kad rezervacija yra sudaryta iš kelių objektų.

### Design Pattern – Factory Method
Šiame kode naudojamas Factory Method šablonas, realizuotas TicketFactory klasėje:

class TicketFactory:
    @staticmethod
    def create_ticket(ticket_choice, seat_number, base_price):
        if ticket_choice == "1":
            return RegularTicket(seat_number, base_price)
        if ticket_choice == "2":
            return VIPTicket(seat_number, base_price)
        return None

Ši klasė atsakinga už bilietų kūrimą, pagal vartotojo pasirinkimą sukuriamas tinkamas objektas.

## 3. Rezultatai
- Sistema sėkmingai realizuoja pagrindines kino teatro valdymo funkcijas: filmų, seansų, vietų ir rezervacijų administravimą.
- Tinkamai sujungtos skirtingos klasės (Movie, Show, Seat, Booking) veikia kaip viena sistema.
- Naudojant validacijos funkcijas užtikrinama, kad vartotojas negalėtų įvesti neteisingų duomenų.

## 4. Išvada
Ši programa realizuoja pilną kino teatro valdymo sistemą, naudojant objektinio programavimo principus. Enkapsuliacija užtikrina duomenų saugumą, paveldėjimas leidžia išvengti kodo dubliavimo, polimorfizmas suteikia lankstumą dirbant su skirtingais bilietų tipais, agregacija modeliuoja realius objektų ryšius, o Factory Method šablonas leidžia efektyviai kurti objektus. Visa sistema suskaidyta į aiškias valdymo klases, kurios koordinuoja skirtingas funkcijas ir užtikrina tvarkingą bei išplečiamą architektūrą.

## 5. Kaip galima patobulinti?
- Pridėti daugiau bilietų tipų (pvz., studentų, vaikų).
- Naudoti duomenų bazę vietoje tekstinių failų.
- Įtraukti vietų pasirinkimą pagal salės schemą.
