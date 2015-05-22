---LAB 5---

---Oppgave 1---
a)
Vi skrev en svært enkel metode som skriver ut "Hello World", metoden ser du under.

#include <stdio.h>
int main() {
	printf("Hello World\n");
	return 0;
}

b)
Vi måtte først installere GCC med kommandoen sudo yum install gcc, yum fordi en av oss bruker Fedora.
Ved å kjøre kommandoen GCC test1 test1.c ble det opprettet en kjørbar fil som het test1 som skal brukes senere i oppgaven.

c)
Når man kompilerer et program kjøres en rekke kommandoer.

Her kommer komandoene i rekkefølge:
1. Først kjøres "cpp test.c > test.i" I denne fasen behandler GNU kompileren headers og macros, dette produserer test.i
2. Så kjøres gcc -S hello.i som kompilerer den behandlet koden ned til assembly kode. Dette produserer test.s.
3. Så kjøres as -o test.o test.s som konverterer assembly koden til machine code. Dette produserer test.o
4. Tilsutt kjøres id -o test.exe test.o ...libraries... som linker objekt kode til library kode som produserer test.exe

---Oppgave 2---
d)
rb betyr at filen kan leses og åpnes i binær modus.
r står for reading og b står for binary, sammen står det for reading binary.

---Oppgave 3---
a)
struct.unpack(fmt, string) pakker ut python strengen henhold til formate gitt. 
I dette tilfellet er formatet B, som betyr konvertering mellom C typen unsigned char og python typen integer.

b)
f.read(1) leser den første byten i filen test1 som er satt i variabelen f.
Det er viktig å merke at den leser første byte, og ikke første bit. Ved dette kallet leser vi verdien «x7f».

c)
Ved at unpack funksjonen kjøres via bin, returneres første byte som i dette tilfelle er «x7f».

d)
Siden den produserte filen er en ELF fil, den har en binær verdi på 127.

---Oppgave 4---
a)
bin >> 7 returnerer verdien 1

b)
bin >> 7 & 1 returnerer verdien 1

d)
bin >> 8 gir verdien 0, grunnen til dette er at vi har da oversteget til neste Byte.

e)
[str(bin >> x & 1) for x in (7,6,5,4,3,2,1,0)] gir verdien
[‘1’, ‘1’, ‘0’, ‘0’, ‘1’, ‘1’, ‘1’, ‘1’]

f)
For å få denne oppgaven til å funke mått jeg skrive ‘“”.join’ istedet for ‘“.join’, men vi fikk streng resultatet ‘11001111’.

g)
Resultat av hex(bin) er "0x7f", som er hexaverdien til 127 var resultatet på oppgave 3d.

h)
hex(bin) returnerer verdien "0x7f" relateres til ELF fordi en ELF fil vil alltid starte med de samme fire førstye bytene, disse er: "x7f", "E", "L" og "F". Dette kalles for Magic Number.

j)
Etter å ha kjørt bin = struct.unpack('B',f.read(1))[0] igjen returnerte den verdien 69.
Dette tilsvarer neste byte i filen som representerer bokstaven e.

---Oppgave 5---
ELF har ulike spessifikasjoner. Det finnes tredjeparts moduler, 
samt den tidligere brukt modulen struct som er en del av pythons standardbibliotek

---Oppgave 6---
Etter å ha kjørt bin = struct.unpack('B',f.read(1))[0] to ganger till fikk vi to nye verdier. Med første kall fikk vi verdien 70 som representerer «L». 
Med andre kall fikk vi verdien 76 som representrer «F».
Nå har vi gått gjennom de fire første bytse, viss ve setter verdiene sammen får vi «x7f», «E», «L» og «F».  
ELF filer vil alltid ha «x7f», «E», «L» og «F» som de fire første bytes i filen.

a)
Med denne artikkelen ser vi at, som vi beskrev tidligere, at ELF filer vil alltid starte med de samme 4 byrsene: «x7f», «E», «L» og «F».
Dette kalles for ELFs "Magic Number".

b)
Etter å ha kjørt f.read(1) fire ganger får vi verdiene «x7f», «E», «L» og «F», begrepet som kjennetgner detter er "Magic Number".

---Oppgave 7---
a)
Etter å ha kjørt f.read(1) for en femte og sjette gang fikk vi de første to bytsene etter "magic number" bytsene. Verdiene på disse to var '\x01'.

b)
For å få samme verdi på bin som vi fikk på skjette kall av f.read(1) vil vi beskrvie to mulige måter.
1. Man forrandre på bin funksjonen slik at den kaller på f.read(6) istedet for f.read(1).
2. Man kan først kalle funskjonen f.seek(5), så kjøre et kall til f.read(1) via bin funksjonen.
På disse to måtene skal man kunne komme til samme verdi på bin som med skjette kall av f.read(1).

---Oppgave 8---
Ved å først finn PID til python, kjørte vi kommandoen ls -l /proc/7476/fd for å finne finne om python prosessen hadde noen åpne filer.
Her fant vi at test1 file var åpnet av python prosessen.

---Oppgave 9---
ls -l /proc/<pid>/fd å finne alle åpnedede filer av en gitt prosess. fd står for "file descriptior som er en indikator brukt til å aksessere filer eller andre IO ressurser.
pid er prosess id'en til selve prosessen, i oppgave 8 var denne 7476 for python prossesen.

---Oppgave 10---
For å lukke filer i python shell kaller man metoden close() på den åpnede filen. I dette tilfele ville vi klat f.close() for å lukke test1 filen.

---Oppgave 11---
Med å kjøre gjennom punkt 2 til 6 hvor vi valgte å bruke en JPEG fil istedet for en ELF fil, kom vi frem til at JPEG filer har sitt eget sett med "magic number" Med å kjøre f.read(1) fire ganger kom vi frem til at 
JPEG magic number er "ff", "d8", "ff" og "d9".

