# Smernice za bolje pisanje koda

- [Smernice za bolje pisanje koda](#smernice-za-bolje-pisanje-koda)
  - [Refaktorisanje](#refaktorisanje)
  - [Čist kod (Clean code)](#čist-kod-clean-code)
  - [Konvencije imenovanja](#konvencije-imenovanja)
    - [Izvori](#izvori)
    - [Vrste konvencija imenovanja](#vrste-konvencija-imenovanja)
    - [Upotreba konvencija u Javi](#upotreba-konvencija-u-javi)
    - [Imenovanje promenljivih, klasa i metoda](#imenovanje-promenljivih-klasa-i-metoda)
  - [Razmaci u Javi](#razmaci-u-javi)
    - [if](#if)
    - [for i while](#for-i-while)
    - [do while](#do-while)
    - [switch](#switch)
    - [Klasa i interfejs](#klasa-i-interfejs)
    - [Metoda](#metoda)
    - [Kastovanje](#kastovanje)
    - [Unarni operatori](#unarni-operatori)
    - [Binarni operatori](#binarni-operatori)
    - [Ternarni operator](#ternarni-operator)
    - [Komentari](#komentari)
    - [Nepotrebne linije](#nepotrebne-linije)
  - [Pisanje komentara](#pisanje-komentara)
  - [Funkcije i metode](#funkcije-i-metode)
  - [Struktuiranje kod](#struktuiranje-kod)
  - [DRY (Don't repeat yourself) princip](#dry-dont-repeat-yourself-princip)
  - [KISS (Keep it simple, stupid) princip](#kiss-keep-it-simple-stupid-princip)
  - [SOLID principi](#solid-principi)

> "Any fool can write code that a computer can understand. Good programmers write code that humans can understand." Martin Fowler

## Refaktorisanje

[Refactoring guru](https://refactoring.guru/)  

**Refaktorisanje** je proces preuređivanja i poboljšavanja postojećeg koda bez promene njegovog spoljašnjeg ponašanja. Ova praksa je osmišljena da unapredi čitljivost, održavanje i skalabilnost koda.

## Čist kod (Clean code)

Čist kod je jasan, razumljiv i održiv.

Zašto treba pisati čist kod?

- Čist kod je lak za čitanje i razumevanje. Jasno strukturiran, sa smislenim nazivima promenljivih i funkcija, olakšava razumevanje onima koji čitaju kod, uključujući i vas same u budućnosti.
- Kako projekti rastu, potrebno je održavanje koda. Čist kod smanjuje napor potreban za pronalaženje i ispravku grešaka (bug-ova), dodavanje novih funkcionalnosti ili izmenu postojećih.
- Čist kod smanjuje složenost projekta, olakšavajući dodavanje novih funkcionalnosti ili razumevanje poslovanja.
- Čist kod pomaže u ubrzanju razvojnog ciklusa. Jasno strukturiran, dokumentovan i dobro organizovan kod omogućava brže razumevanje postojećih delova i brže dodavanje novih.
- Čist kod olakšava timski rad. Različiti članovi tima mogu efikasnije raditi zajedno na projektu ako je kod čitljiv i strukturiran.
- Projekti čiji je kod čist, imaju tendenciju da budu dugoročno održivi. Dugotrajno održavanje koda je olakšano čistim pristupom.

## Konvencije imenovanja

### Izvori

- [Oracle](https://www.oracle.com/java/technologies/javase/codeconventions-namingconventions.html#:~:text=Naming%20conventions%20make%20programs%20more,helpful%20in%20understanding%20the%20code.)  
- [Server side](https://www.theserverside.com/feature/Java-naming-conventions-explained#:~:text=For%20variables%2C%20the%20Java%20naming,a%20lower%20camel%20case%20syntax.)
- [Baeldung](https://www.baeldung.com/java-clean-code)
- [Academind](https://github.com/academind/clean-code-course-code)

Prilikom imenovanja promenljivih, metoda, klasa, ... se treba truditi da ih imenujete smisleno i da im ime ne bude predugačko.

### Vrste konvencija imenovanja

|Konvencija|Primer|
|--------|-------------|
|Pascal Case|PascalCase|
|Camel Case|camelCase|
|Snake Case|snake_case|
|Screaming Snake Case|SCREAMING_SNAKE_CASE|
|Kebab Case|kebab-case|
|Lower Dot Case|lower.dot.case|

### Upotreba konvencija u Javi

|Upotreba|Konvencija|
|-----|---|
|promenljive i metodi|Camel Case|
|klase i interfejsi|Pascal Case|
|konstante|Screaming Snake Case|
|paketi|Lower Dot Case|

### Imenovanje promenljivih, klasa i metoda

Više o tome možete videti na [sledećoj prezetaciji](https://github.com/academind/clean-code-course-code/blob/naming-extra-attachments/slides-naming.pdf).

[Sumirano](https://github.com/academind/clean-code-course-code/blob/naming-extra-attachments/Naming-Summary.pdf)

## Razmaci u Javi

Smernice navedene u nastavku nisu obavezne, ali je preporučljivo ispratiti ih kako bi vaš kod bio čist. Iako postoje alati koji mogu sami da formatiraju kod u skladu sa standardima, nije na odmet proći neke osnovne standarde pisanja koda.

### if

```java
if (condition) {

} else {

}
```

Razmak nakon `if` i između `)` i `{`.
Razmak pre i posle `else`.

### for i while

```java
for (initialization; condition; steps) {

}

while (condition) {

}
```

Slično kao i za `if`.

### do while

```java
do {

}
while (condition);
```

### switch

```java
switch(expression) {
  case x:
    // code block
    break;
  case y:
    // code block
    break;
  default:
    // code block
}
```

### Klasa i interfejs

```java
class Klasa {

}

interface Interfejs {

}
```

Između naziva i `{` bi trebalo da postoji razmak.

### Metoda

```java
void metoda(argument1, argument2) {

}
```

Između `,` i narednog argumenta i `)` i `{` bi trebalo da postoji razmak.

### Kastovanje

```java
(int) 4.2
```

### Unarni operatori

```java
!true
-4
++a
c--
```

Ne postoji razmak između operatora i vrednosti ili promenljive.

### Binarni operatori

```java
a = 10;
a += 13;
true && false;
1 + 2
3 / 6
...
```

Razmak pre i posle operatora.

### Ternarni operator

```java
(condition) ? expressionTrue :  expressionFalse;
```

### Komentari

```java
int a; // razmak pre i nakon //
int c; /* razmak pre i nakon
*/

// ukoliko je samo komentar u liniji razmak nakon //
/* isto vazi i ovde
*/
```

### Nepotrebne linije

Treba brisati nepotrebne linije kao na primer poslednju praznu liniju u fajlu. Linije koje nije preporučljivo brisati su linija pre i linija nakon blokova
metode, if, switch i petlji (for, while, do while). Ukoliko je nakon ovih navedenih blokova `}` a ne neki koristan kod, onda je preporučljivo obrisati praznu liniju između njih.

Primer

```java
class Test {
  void metoda1() {

  }
  // postoji prazna linija
  void metoda2() {

  }
  // postoji prazna linija
  void metoda3() {

  } // ne postoji prazna linija nakon ovoga
}

void test() {
  int a,b;
  String c;
  // postoji prazna linija
  for () {

  }
  // postoji prazna linija
  while () {

  } // postoji prazna linija
}
```

## Pisanje komentara

[Slajdovi](https://github.com/academind/clean-code-course-code/blob/comments-formatting-extra-attachments/slides-comments-formatting.pdf)  
[Sumirano](https://github.com/academind/clean-code-course-code/blob/comments-formatting-extra-attachments/Comments-Formatting-Summary.pdf)

## Funkcije i metode

[Slajdovi](https://github.com/academind/clean-code-course-code/blob/functions-extra-attachments/slides-functions.pdf)  
[Sumirano](https://github.com/academind/clean-code-course-code/blob/functions-extra-attachments/Functions-Summary.pdf)

## Struktuiranje kod

[Slajdovi](https://github.com/academind/clean-code-course-code/blob/control-extra-attachments/slides-control-structures.pdf)  
[Sumirano](https://github.com/academind/clean-code-course-code/blob/control-extra-attachments/Control-Structures-Summary.pdf)

## DRY (Don't repeat yourself) princip

DRY je akronim za "Don't Repeat Yourself" (Ne Ponavljaj Se). Ovo je princip softverskog inžinjeringa koji promoviše smanjenje ponavljanja koda u softverskim projektima.

Glavne prednosti DRY principa uključuju:

- **Smanjenje redundanse**: Izostavljanje ponavljanja smanjuje količinu koda i podataka, čineći sistem efikasnijim.

- **Poboljšana održivost**: Kada se funkcionalnost ili podaci ponavljaju na više mesta, svaka promena mora biti ažurirana na svakom od tih mjesta. To može dovesti do grešaka i otežati održavanje koda.

- **Povećana čitljivost**: Kada se informacije ponavljaju, kod postaje duži i teži za čitanje. DRY princip olakšava razumevanje koda jer se ista funkcionalnost ili podaci nalaze na jednom mestu.

DRY princip se obično primenjuje na više nivoa razvoja softvera:

- **Kod**: Izbegavanje ponavljanja koda, funkcija ili blokova koda.
- **Podaci**: Izbegavanje ponavljanja istih podataka na više mesta.

## KISS (Keep it simple, stupid) princip

KISS princip je akronim za "Keep It Simple, Stupid". Ovaj princip se odnosi na filozofiju dizajniranja, razvoja softvera ili sistemskih arhitektura, gde se promoviše jednostavnost i minimalizam.

## SOLID principi

[Baeldung](https://www.baeldung.com/solid-principles)  
[Academind slajdovi](https://github.com/academind/clean-code-course-code/blob/obj-extra-attachments/slides-objects.pdf)  
[Academind sumirano](https://github.com/academind/clean-code-course-code/blob/obj-extra-attachments/Objects-Summary.pdf)

Evo šta svaki od SOLID principa znači:

1. **S - Single Responsibility Principle (Princip jedne odgovornosti)**: Svaka klasa treba da bude odgovorna samo za jedan aspekt funkcionalnosti. Ovo znači da klasa treba da ima samo jedan razlog za promenu.

2. **O - Open/Closed Principle (Princip otvorenosti/zatvorenosti)**: Klase treba dizajnirati tako da budu otvorene za proširenje, ali zatvorene za modifikacije. To znači da treba biti moguće proširiti funkcionalnost bez menjanja postojećeg koda.

3. **L - Liskov Substitution Principle (Liskov princip zamene)**: Ovaj princip kaže da objekti podklase mogu da budu zamena (substitutable) za objekte svoje nadklase bez narušavanja ispravnosti programa. Drugim rečima, potklasa treba da bude kompatibilna sa svojom nadklasom.

4. **I - Interface Segregation Principle (Princip segregacije interfejsa)**: Interfejsi treba da budu specifični za korisnike, tako da oni ne moraju zavisiti od funkcionalnosti koje ne koriste. Veliki interfejsi treba razbiti na manje specifične segmente kako bi se omogućila veća fleksibilnost.

5. **D - Dependency Inversion Principle (Princip inverzije zavisnosti)**: Moduli visokog nivoa ne bi trebalo da zavise od modula niskog nivoa. Trebalo bi da zavise od apstrakcija. Apstrakcije ne bi trebale zavisiti od detalja. Detalji bi trebali zavisiti od apstrakcija. Ovaj princip se fokusira na smanjenje zavisnosti između klasa. To se postiže korišćenjem apstrakcija i interfejsa, umesto da se klase direktno vezuju za implementacije drugih klasa.
