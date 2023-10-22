# Vežbe 1  

Java programski jezik je jezik visokog nivoa koji se može opisati sledecim epitetma:
* Jednostavan
* Objektno-orijentisan
* Distribuiran
* Multithread - Nit (eng. thread) je osnovna izvršna jedinica u procesu koji omogućava programima izvršavanje niza instrukcija na procesoru. Svaka nit ima svoj stek i registre, što joj omogućava izvršavanje nezavisnih sekvenci instrukcija. Niti u procesu dele isti adresni prostor i resurse, što omogućava jednostavnu razmenu podataka i komunikaciju između njih. Niti omogućavaju paralelno ili istovremeno izvršavanje različitih delova programa, što povećava efikasnost programa, posebno na višejezgarnim računarima. Korišćenje niti može poboljšati odziv aplikacija i iskorišćenje resursa.
* Dinamičan
* Nezavisan od arhitekture računara
* Programski jezik visokih performani
* Siguran

## Kompajliranje i pokretanje Java programa

*Primer Java programa - HelloWorld.java*
```java
public class HelloWorldApp
{
  public static void main(String[] args)
  {
    System.out.println("Hello World!"); // Prikazi string.
  }
}
```

1. Svaka Java aplikacija mora sadržati barem jednu klasu s metodom main(String[] args). main metoda je prva metoda koja će se izvršiti nakon što se pokrene Java program (slično kao i u C).
2. Ovako napisan program se prevodi izvrsavajući komandu `javac HelloWorld.java` .
3. Ako nema grešaka prevodilac javac kreira datoteku HelloWorld.class koja sadrži bytecode instrukcije za JVM (Java virtual machine). Java virtuelna mašina je program koji je dostupan na mnogim operativnim sistemima i služi za izvršavanje bytecode-a (mašinski jezik za JVM). Isti .class fajl moguće je pokrenuti na
Windows-u, Linux-u, Solaris OS-u ili Mac OS-u. Zbog toga je Java programski jezik koji je nezavisan od platforme. Potrebno ga je kompajlirati samo jednom i moguće da ga je nakon toga izvršiti svuda.
4. JVM se pokreće sa `javac HelloWorld` .



