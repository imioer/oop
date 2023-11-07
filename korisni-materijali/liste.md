# Liste u Javi

- [Liste u Javi](#liste-u-javi)
  - [Nizovi](#nizovi)
    - [Kreiranje nizova](#kreiranje-nizova)
    - [Prednosti nizova](#prednosti-nizova)
    - [Mane nizova](#mane-nizova)
    - [Ugrađene metode i svojstva za nizove](#ugrađene-metode-i-svojstva-za-nizove)
    - [Nizovi kao referentni tip](#nizovi-kao-referentni-tip)
    - [Nizovi objekata](#nizovi-objekata)
  - [Liste](#liste)
    - [Generički tipovi](#generički-tipovi)
    - [Implementacije List interfejsa](#implementacije-list-interfejsa)
    - [Rad sa Listama](#rad-sa-listama)
      - [Kreiranje liste](#kreiranje-liste)
      - [Dodavanje elemenata](#dodavanje-elemenata)
      - [Pristupanje elementima](#pristupanje-elementima)
      - [Postavljanje vrednosti elementa na određenom indeksu](#postavljanje-vrednosti-elementa-na-određenom-indeksu)
      - [Iteriranje kroz listu](#iteriranje-kroz-listu)
      - [Brisanje elementa](#brisanje-elementa)
      - [Ostale metode](#ostale-metode)
    - [Prednosti korišćenja listi](#prednosti-korišćenja-listi)
    - [Mane korišćenja listi](#mane-korišćenja-listi)

## Nizovi

Nizovi (arrays) u Javi predstavljaju strukture podataka koje omogućavaju skladištenje više elemenata istog tipa podataka u sekvenci.

### Kreiranje nizova

Kreiranje nizova zahteva definisanje tipa elemenata niza i određivanje veličine niza. Ovi nizovi mogu biti referentnog tipa (kada se čuvaju u memoriji kao referenca) i imaju ugrađene metode za upravljanje podacima.

```java
// Niz celih brojeva
int[] brojevi = new int[5]; // Kreiranje niza celih brojeva sa 5 elemenata

int[][] matrica = new int[5][5]; // kreiranje matrice 5x5

// Niz stringova
String[] reci = new String[10]; // Kreiranje niza stringova sa 10 elemenata
```

### Prednosti nizova

- **Jednostavnost korišćenja:** Nizovi omogućavaju lako skladištenje više elemenata istog tipa u jednoj strukturi.

- **Brzi pristup elementima:** Pristupanje elementima niza je brzo i efikasno. Pristup određenom elementu se vrši preko indeksa, što omogućava direktni pristup elementima.

- **Sekvencijalno skladištenje:** Elementi niza su sekvencijalno smešteni u memoriji, olakšavajući pristup i upravljanje podacima.

### Mane nizova

- **Fiksna veličina:** Nizovi imaju fiksnu veličinu koja se određuje pri kreiranju, što znači da ne možete lako promeniti veličinu niza nakon što je kreiran.

- **Neefikasnost pri dodavanju/brisanju:** Dodavanje ili brisanje elemenata iz sredine niza može biti neefikasno jer zahteva pomeranje ostalih elemenata.

- **Ne podržavaju različite tipove podataka:** Nizovi u Javi mogu sadržavati samo elemente istog tipa.

- **Nedostatak ugrađenih metoda:** Nizovi nemaju mnogo ugrađenih metoda za manipulaciju podacima, što može otežati rad s njima.

### Ugrađene metode i svojstva za nizove

Ugrađene metode omogućavaju manipulaciju podacima u nizu:

- **length:** Svojstvo koje vraća dužinu niza.
  
```java
  int duzinaNiza = brojevi.length; // Vraća dužinu niza brojevi
```

Metode koje nam olakšavaju rad sa nizovima su uglavnom statičke metode klase [Arrays](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html).

Neke od tih metoda su:

- **copyOf:** Metoda koja kreira kopiju niza sa zadatom dužinom.

```java
  int[] novaKopija = Arrays.copyOf(brojevi, 10); // Kopira niz brojevi u novuKopija sa dužinom 10
```

- **fill:** Metoda koja popunjava ceo niz sa određenom vrednošću.
  
```java
  Arrays.fill(brojevi, 0); // Popunjava niz brojevi sa nulama
```

Ostale metode možete pronaći na [sledećem linku](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html).

### Nizovi kao referentni tip

U Javi, nizovi se smatraju referentnim tipom podataka. To znači da se referenca na niz skladišti u memoriji, a ne sami podaci. Kada se niz dodeljuje drugoj promenljivoj, zapravo se dodeljuje referenca na isti niz.

```java
int[] niz1 = {1, 2, 3};
int[] niz2 = niz1; // niz2 sada pokazuje na isti niz kao i niz1
```

Korišćenjem ugrađenih metoda i svojstava, Java nudi praktične alate za rad sa nizovima. Važno je imati na umu da nizovi kao referentni tipovi mogu deliti iste podatke, što zahteva pažnju pri manipulaciji sa njima kako bi se izbegli neželjeni efekti.

### Nizovi objekata

Ako postoji neki niz objekata koji je inicijalizovan, svih njegovi članovi će nakon inicijalizacije biti **null**. Zato je bitno da ako prolazimo po svim članovima niza koristeći petlju prvo pitamo da li je taj član različit od **null** i ukoliko jeste moguće je pristupiti svojstvima i metodama objekta. Drugi način bi bio da ne prolazimo po svim članovima niza nego čuvamo broj elemenata niza koji nisu null u nekoj promenljivoj.

## Liste

Za razliku od nizova, liste su deo [Java Collections Framework-a](https://docs.oracle.com/javase/8/docs/technotes/guides/collections/overview.html) i pružaju dinamički pristup podacima, omogućavajući dodavanje, brisanje i izmenu elemenata bez potrebe za fiksiranjem veličine.

### Generički tipovi

Generički tipovi (generic types) su deo Java programskog jezika koji omogućava kreiranje klasa, interfejsa i metoda koji su parametrizovani tipom podataka. Ovo omogućava programerima da napišu fleksibilniji i ponovno upotrebljiv kod koji može raditi sa različitim tipovima podataka.

Kroz korišćenje generičkih tipova, tip podataka se ne definiše unapred, već se određuje prilikom instanciranja objekta ili poziva metode. To omogućava veću apstrakciju i omogućava klasama i metodama da budu generičke u smislu tipova s kojima rade.

Na primer, generička klasa može izgledati ovako:

```java
public class Kutija<T> {
    private T sadrzaj;

    public void postaviSadrzaj(T sadrzaj) {
        this.sadrzaj = sadrzaj;
    }

    public T dohvatiSadrzaj() {
        return sadrzaj;
    }
}
```

U ovom primeru, `Kutija` je generička klasa koja može sadržavati bilo koji tip podataka `T`. Prilikom instanciranja objekta, tip `T` se određuje. Na primer:

```java
Kutija<String> stringKutija = new Kutija<String>();
Kutija<int> intKutija = new Kutija<int>();
stringKutija.postaviSadrzaj("Ovo je string");
intKutija.postaviSadrzaj(10);
```

Kroz generičke tipove, omogućeno je pisanje koda koji je manje specifičan za određeni tip podataka i omogućava veću ponovnu upotrebu koda za različite tipove. Generički tipovi se često koriste u kolekcijama, kao što su ArrayList, LinkedList itd., kako bi mogle raditi sa različitim tipovima podataka, omogućavajući sigurno tipiziranje i smanjujući potrebu za konverzijama tipova.

### Implementacije List interfejsa

U okviru [Java Collections Framework-a](https://docs.oracle.com/javase/8/docs/technotes/guides/collections/overview.html), List je interfejs koji definiše ponašanje za sekvencijalne strukture podataka. Neke od popularnih implementacija List interfejsa su:

- **ArrayList:** Dinamički niz koji omogućava brzi pristup elementima i efikasno proširenje. Omogućava elementima da se skladište u sekvenci i omogućava pristup preko indeksa.

- **LinkedList:** Struktura podataka koja se sastoji od čvorova povezanih pokazivačima. Omogućava brze operacije dodavanja i brisanja na početku, kraju i u sredini liste.

### Rad sa Listama

#### Kreiranje liste

```java
List<String> lista = new ArrayList<String>(); // Kreiranje ArrayList instance
List<int> drugaLista = new LinkedList<int>(); // Kreiranje LinkedList instance
```

#### Dodavanje elemenata

```java
lista.add("Prvi element");
lista.add("Drugi element");
lista.add("Treći element");
```

#### Pristupanje elementima

```java
String prvi = lista.get(0); // Pristup prvom elementu liste
```

#### Postavljanje vrednosti elementa na određenom indeksu

```java
int index = 1;
String value = "Test";
lista.set(index, value);
```

#### Iteriranje kroz listu

```java
for (String element : lista) {
    System.out.println(element);
}
```

#### Brisanje elementa

```java
lista.remove(1); // Brisanje elementa na indeksu 1
```

#### Ostale metode

Možete pronaći kompletnu listu metoda koje su deo `List` interfejsa u Javi na [zvaničnoj Java dokumentaciji](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/List.html).

### Prednosti korišćenja listi

- **Dinamička veličina:** Liste omogućavaju dodavanje i brisanje elemenata, prilagođavajući se potrebama.
- **Ugrađene metode:** Pružaju širok spektar ugrađenih metoda za manipulaciju podacima.

### Mane korišćenja listi

- **Sporiji pristup elementima:** Kod LinkedList-a, pristupanje elementima može biti sporije u odnosu na ArrayList.
- **Veća potrošnja memorije:** LinkedList koristi više memorije zbog potrebe za čuvanjem referenci na susedne čvorove.

Korišćenje List struktura omogućava fleksibilnost i olakšava rad sa podacima, pružajući efikasne mehanizme za upravljanje i manipulaciju listom elemenata. Odabir između ArrayList i LinkedList zavisi od konkretnih zahteva i očekivanja performansi aplikacije.
