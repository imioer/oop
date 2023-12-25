# Niti

- [Niti](#niti)
  - [Uvod](#uvod)
  - [Niti u Javi](#niti-u-javi)
    - [Pokretanje niti](#pokretanje-niti)
    - [Čekanje kraja izvršavanja niti](#čekanje-kraja-izvršavanja-niti)
  - [Monitor](#monitor)
  - [Zadatak 1: Sabiranje](#zadatak-1-sabiranje)
  - [Synchronized](#synchronized)
  - [Redovi čekanja monitora](#redovi-čekanja-monitora)
    - [Monitor Queue](#monitor-queue)
    - [Wait Queue](#wait-queue)
      - [Problemi sa wait i notify](#problemi-sa-wait-i-notify)
  - [Zadatak 2: Producer i Consumer](#zadatak-2-producer-i-consumer)
    - [Rešenje](#rešenje)

## Uvod

Nit (eng. thread) je osnovna izvršna jedinica u procesu koji omogućava programima izvršavanje niza instrukcija na procesoru. Svaka nit ima svoj stek i registre, što joj omogućava izvršavanje nezavisnih sekvenci instrukcija. Niti u procesu dele isti adresni prostor i resurse, što omogućava jednostavnu razmenu podataka i komunikaciju između njih. Niti omogućavaju paralelno ili istovremeno izvršavanje različitih delova programa, što povećava efikasnost programa, posebno na višejezgarnim računarima. Korišćenje niti može poboljšati odziv aplikacija i iskorišćenje resursa.

| Kriterijum          | Proces                                 | Nit                                       |
|---------------------|----------------------------------------|-------------------------------------------|
| **Osnovna Jedinka** | Nezavisna izvršna jedinica             | Laka izvršna jedinica deljenog prostora    |
| **Komunikacija**    | Komunikacija između procesa je skuplja  | Komunikacija između niti je jeftinija      |
| **Način komunikacije**         | Zahteva IPC (Interprocesna komunikacija)  | Direktna komunikacija jer dele zajednički prostor adresa |
| **Resursi**         | Svaki proces ima sopstvene resurse     | Niti dele resurse sa ostalim nitima       |
| **Memorija**        | Svaki proces ima sopstvenu memoriju    | Niti dele memoriju sa ostalim nitima       |
| **Vreme kreiranja** | Kreiranje procesa je sporije            | Kreiranje niti je brže                    |
| **Efikasnost**      | Troši više resursa                      | Troši manje resursa                        |
| **Paralelizam**     | Procesi se izvršavaju nezavisno jedan od drugog | Niti mogu deliti resurse i izvršavati se paralelno |
| **Kontekst prekida**     | Svaki proces ima sopstveni kontekst       | Niti dele isti kontekst prekida             |
| **Težina kreiranja**     | Kreiranje procesa je resursno zahtevno    | Kreiranje niti je brže i manje resursno     |
| **Zaštita**              | Procesi imaju zaštitu od međusobnog pristupa | Niti moraju pažljivo upravljati deljenim resursima |
| **Otpornost na greške**  | Pad jednog procesa obično ne utiče na druge | Pad jedne niti može uticati na celu aplikaciju |

## Niti u Javi

Niti su definisane klasom `Thread` u standardnoj biblioteci. Ukoliko želimo da kreiramo novu nit, koja treba da radi određeni posao to možemo da uradimo na dva načina:

1. Kreiranjem klase koja nasleđuje klasu Thread (direktno ili indirektno)

```java
class MojaNit extends Thread {
    @Override
    public void run() {
        // radi neki posao
    }
}

Thread t = new MojaNit();
```

2. Kreiranjem klase koja implementira interfejs `Runnable` i prosleđivanjem instance te klase konstruktoru klase `Thread`

```java
class MojRunnable implements Runnable {
    public void run() {
        // radi neki posao
    }
}

Thread t = new Thread(new MojRunnble());
```

U metodi `run()` treba da bude smešten kod koji će se izvršiti kada se pokrene nit.

### Pokretanje niti

```java
Thread t = new MojaNit();
t.run(); // OVO JE POGRESNO I NEMOJTE OVO RADITI
t.start(); // stvarno pokretanje niti
```

Ukoliko pozovete t.run() izvršiće se run metoda u glavnoj niti, kao da ste pozvali bilo koju metodu objekta kao i do sada i neće biti kreirana nova nit. Pozivom metode t.start() kreira se nova nit koja će izvršavati kod koji je smešten u run() metodi.

### Čekanje kraja izvršavanja niti

**Primer 4.1**

```java
public class MojaNit extends Thread{
    public void run() {
        System.out.println("Ispis iz niti");
    }

    public static void main(String[] args) {
        Threat t = new MojaNit();

        t.start();

        System.out.println("Kraj programa");
    }
}
```

Ukoliko pokrenemo kompajiramo kod napisan u primeru **Primeru 4.1** i pokrenemo ga, ispis programa može biti

```text
Kraj programa
Ispis iz niti
```

ako je glavna nit imala procesorsko vreme, a nova nit koja je kreirana je čekala na procesorsko vreme. Ukoliko želite da glavna nit sačeka da nit `t` prvo završi svoje izvršavanje, kako bi glavna nit nakon toga mogla da nastavi potrebno je pozvati metodu `t.join()`. Ako pozovete ovu metodu, neophodno je obraditi izuzetak `InterruptedException` ili ga dodati u `throws` deklaraciju.  

**Primer 4.2**

```java
public class MojaNit extends Thread{
    public void run() {
        System.out.println("Ispis iz niti");
    }

    public static void main(String[] args) {
        Threat t = new MojaNit();

        t.start();

        try {
            t.join();
        }
        catch(InterruptedException e) {
            System.out.println("Greska");
        }

        System.out.println("Kraj programa");
    }
}
```

Program napisan u **Primeru 4.2** će uvek dati rezultat

```text
Kraj programa
Ispis iz niti
```

osim ukoliko ne doće do neke greške i `InterruptedException` bude bačen.

## Monitor

**Monitor** je koncept koji se koristi za sinhronizaciju pristupa deljenim resursima kako bi se izbegli problemi poput stanja trke (race conditions). Monitor pruža ekskluzivan pristup deljenim resursima, čime se obezbeđuje da samo jedna nit može izvršavati kritične sekcije koda unutar monitora u određenom trenutku. Za razliku od `Operativnih sistema 1` ne morate da koristite semafore i samo vodite računa o tome da li treba da skinete nešto sa semofora ili vratite nešto na semafor.

## Zadatak 1: Sabiranje

Napisati jednostavan program koji će imati tri niti koje povećavaju neku promenljivu za 1 određeni broj puta. Promenljiva na početku ima vrednost 0. Očekivani rezultat je da na kraju izvršavanje dobijemo 3 * `broj_povecavanja`.

Ako napišemo program na sledeći način da li ćemo dobiti očekivani rezultat?

```java
class Kalkulator {
    private int broj = 0;

    public void dodajJedan() {
        broj = broj + 1;
    }

    public int getBroj() {
        return broj;
    }
}

class Racunaljka extends Thread {
    private static final int brojPovecavanja = 10000;

    private Kalkulator kalkulator;

    public Racunaljka(Kalkulator kalkulator) {
        this.kalkulator = kalkulator;
    }

    public void run() {
        for(int i = 0; i < brojPovecavanja; i++) {
            kalkulator.dodajJedan();
        }
    }
}

public class Test {

    // sve niti primaju istu referencu, kako bi povecavale samo jedan broj
    // ukoliko bi svaka nit imala svoju referencu, ne bi bilo konkurentnosti

    public static void main(String[] args) throws InterruptedException {
        Kalkulator kalkulator = new Kalkulator();
        Thread t1 = new Racunaljka(kalkulator);
        Thread t2 = new Racunaljka(kalkulator);
        Thread t3 = new Racunaljka(kalkulator);

        t1.start();
        t2.start();
        t3.start();

        // glavna nit ceka da sve ostale niti zavrse sa izvrsavanjem kako bi ispisala rezultat

        t1.join();
        t2.join();
        t3.join();

        System.out.println(kalkulator.getBroj());
    }
}
```

Očekivani rezultat je 30000, ali je velika verovatnoća da nećemo dobiti taj broj.  

**Zašto?** Zato što nismo zaštitili kritičnu sekciju. Kada napišemo komandu `broj = broj + 1`, procesor će izvršiti tri instrukcije (čitanje iz memorije, sabiranje, pisanje u memoriju). Kada nit želi da pročita nešto iz memorije, dešava se prekid. Kada se desi prekid, nit se prebacuje u stanje čekanja. Za to vreme druga nit može da se izvršava. Dok se druga nit izvršava i ona želi da pročita nešto iz memorije, pa postoji mogućnost da će pročitati istu vrednost, uvećati je za jedan i **dva puta upisati istu vrednost** u procesor.  

## Synchronized

Kako bi rešili taj problem, moramo zaštititi kritičnu sekciju, koristeći ključnu reč `synchronized`. Svaki objekat ima svoj monitor. Svaka klasa ima svoj monitor. Ako se pozove statička `synchronized` metoda, nit će pokušati da uđe u monitor klase. Ako se pozove nestatička `synchronized` metoda, nit će pokušati da uđe u monitor objekta. Ne moramo samo metode definisati kao `synchronized`. Možemo unutar metode koja nije `synchronized`, da definišemo `synchronized` blok. U tom slučaju, moramo proslediti objekat ili klasu, kako bi blok znao u čiji monitor treba da pokuša da uđe.

```java
class Kalkulator {
    private int broj = 0;

    public synchronized void dodajJedan() {
        // kriticna sekcija
        broj = broj + 1;
    }

    public synchronized int getBroj() {
        // kriticna sekcija
        return broj;
    }

    public void dodajJedanDrugiNacin() {
        // nije kriticna sekcija

        synchronized(this) {
            // kriticna sekcija
            broj = broj + 1;
        }

        // nije kriticna sekcija
    }
}
```

## Redovi čekanja monitora

![Redovi cekanja monitora](https://ionutbalosin.com/wp-content/uploads/2018/06/MonitorLocks-1.png)

Monitor ima dva reda čekanja.

### Monitor Queue

Nit čeka da uđe u monitor.

### Wait Queue

Nit je ušla u monitor, ali je potrebno da pređe u stanje čekanja, jer čeka na neki resurs ili događaj, a dok ona čeka, druga nit može da uđe u monitor. Kada nit dobije neki resurs ili se desi neki događaj, **obavezno neko mora da je obavesti**, jer će inače večno čekati.

Nit, **koja je ušla u monitor**, prelazi u Wait Queue pozivom metode `wait()`. Postoji i oveload metode `wait()`. To je metoda `wait(long timeout)`, čijim pozivom nit prelazi u Wait Queue i u njemu se **neće zadržati više od** `timeout` ms (mili sekundi tj. 1000-ti deo sekunde). Ukoliko prođe više od `timeout` ms, nit napušta Wait Queue i čeka da uđe u monitor. Ako pozovete metodu `wait()` ili `wait(long timeout)`, neophodno je obraditi izuzetak `InterruptedException` ili ga dodati u `throws` deklaraciju.

Sa `notify()` nit koja je u monitoru obaveštava neku nit koja je u Wait Queue da izađe iz njega i čeka da uđe u monitor. Sa `notifyAll()` se obaveštavaju sve niti iz Wait Queue da izađu iz njega i čekaju da uđu u monitor.

Metode `wait()`, `wait(long timeout)`, `notify()` i `notifyAll()` se pišu **isključivo** u `synchronized` metoda ili `synchronized` bloku i **nigde** osim na tim mestima. Metode `wait()`, `wait(long timeout)`, `notify()` i `notifyAll()` su nasleđeni iz `Object` klase, pa ih zbog toga poseduju svi objekti.

#### Problemi sa wait i notify

Ukoliko se pozove `notify()`, može doći do situacije da je nit uklonjena iz Wait Queue a nije dobila resurs ili se nije desio događaj koji je trebalo da je ukloni iz Wait Queue. Da se to ne bi desilo, neophodno je pisati kod na sledeći način:

```java
synchronized(nekiObjekat) { // ili <modifikator> synchronized <tip_metoda> <ime_metoda>
    while(uslovBlokade) {
        try {
            wait();
        }
        catch(InterruptedException e) {

        }
    }

    // nit ne mora vise da ceka i moze da izvrsi sta treba

    notifyAll();
}

```

## Zadatak 2: Producer i Consumer

Napisati klasu `Skladiste` koja ima `privatnu` promenljivu `broj` koja je inicijalizovana na -1 i `javne` metode `uzmi`, koja vraća broj i setuje njegovu vrednost na -1 i `proizvedi`, koja setuje vrednost broja, tako što mu dodeli random broj iz opsega od [0,100].

Napisati klase `Producer` i `Consumer` koje nasleđuju klasu `Thread`. `Producer` će u svojoj run metodi imati beskonačnu petlju u kojoj će proivoditi brojeve ako i samo ako nisu već proizvedeni (ukoliko je `broj` različit od -1 ne treba opet pozvati metodu proizvedi, sve dok broj opet ne postane -1). `Consumer` će u svojoj run metodi imati beskonačnu petlju u kojoj će uzimati brojeve ako i samo ako su već proizvedeni (ukoliko je `broj` -1 ne treba opet pozvati metodu uzmi, sve dok broj opet ne postane veći od -1).

U main metodi kreirati jednog `Producer`-a i 3 `Consumera`-a. Sve ove niti će koristiti jedno zajedničko `Skladiste`.

### Rešenje

**BITNA NAPOMENA** - `Thread.sleep(long timeout)` **nije isto** kao i `wait(long timeout)`. Nakon `wait` nit **pokušava opet** da uđe u monitor. Nakon `Thread.sleep` nit **NE pokušava** da uđe u monitor. `Thread.sleep` služi da privremeno zaustavimo izvršavanje niti. To može biti korisno ako u beskonačnoj petlji želimo da uočimo neki ispis. Ukoliko ne bi koristili `Thread.sleep`, ne bi znali da li je ispis dobar ili ne jer bi se nešto stalno ispisivalo velikom brzinom. `Thread.sleep` **može** da baci izuzetak `InterruptedException`, koji je neophodno obraditi ili ga dodati u `throws` deklaraciju.  

[Razlika između wait i sleep Baeldung](https://www.baeldung.com/java-wait-and-sleep)

```java
import java.util.*;

class Skladiste {
    private int broj = -1;
    private Random random = new Random();

    public synchronized void proizvedi() {
        while(broj != -1) {
            try {
                wait();
            }
            catch(InterruptedException e) {
                e.printStackTrace();
            }
        }

        broj = random.nextInt(100);

        notifyAll();
    }

    public synchronized int uzmi() {
        while(broj == -1) {
            try {
                wait();
            }
            catch(InterruptedException e) {
                e.printStackTrace();
            }
        }

        int br = broj;
        broj = -1;

        notifyAll();

        return br;
    }
}

class Producer extends Thread {
    private Skladiste skladiste;

    public Producer(Skladiste skladiste) {
        this.skladiste = skladiste;
    }

    public void run() {
        while(true) {
            skladiste.proizvedi();
            System.out.println("Producer je proizveo");

            try {
                Thread.sleep(2000); // 2ms
            }
            catch(InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

class Consumer extends Thread {
    private Skladiste skladiste;
    private int id;

    public Consumer(Skladiste skladiste, int id) {
        this.skladiste = skladiste;
        this.id = id;
    }

    public void run() {
        while(true) {
            System.out.println("Consumer " + id + " je uzeo broj " + skladiste.uzmi());

            try {
                Thread.sleep(2000); // 2ms
            }
            catch(InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class Test {
    public static void main(String[] args) {
        Skladiste skladiste = new Skladiste();

        Thread p = new Producer(skladiste);
        Thread c1 = new Consumer(skladiste, 1);
        Thread c2 = new Consumer(skladiste, 2);
        Thread c3 = new Consumer(skladiste, 3);

        p.start();
        c1.start();
        c2.start();
        c3.start();
    }
}
```
