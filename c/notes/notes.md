#Moreno c notes

##Sprachtypen
+ c low-level Sprache oder auch Scriptsprache
	+ systemnahe
+ Java high-level Sprache (object oriented)
	+ systemfern

##Sourcecode
Sourcecode wird in eine ausführbare (binäre) Datei übersetzt.
```
#include <stdio.h>

main(){
   int number;
 
   printf("Enter an integer\n");
   scanf("%d",&number);
 
   printf("Integer entered by you is %d\n", number);
 
   return 0;
}
```
Der Sourcecode wird in einer Datei mit der Endung **.c** gespeichert.

##Compiler
Der Sourcecode wird mittels eines compilers übersetzt (gcc).
```
gcc -std=c99 -pedantic -Wall -D_XOPEN_SOURCE=500 -D_BSD_SOURCE -g -DENDEBUG sourcecode.c -o ausführbareDatei
```
+ **gcc:** Copmiler (Prgramm)
+ **-std=99:** c99 Standard
+ **-pedentic:** strenges prüfen des Codes
+ **-Wall:** zeige alle Warnings an
+ **-D\_XOPEN_SOURCE=500:** extra posix linux functions
+ **-D\_BSD_SOURCE:** extra posix linux functions
+ **-g:** gibt debugging informationen aus
+ **-DENDEBUG:** marko definition zum debuggen
+ **sourcedode.c:** datei in dem der Sourcecode ist.
+ **-o ausführbareDate:** Datei in das Programm gespeichert werden soll.

##Makefile
Ein Makefile erleichtert das compilen. Man definiert einmal was zu tun ist und man muss nur einmal in der Konsole **make** eingeben.

```
CC = gcc
CFLAGS = -std=c99 -pedantic -Wall -D_XOPEN_SOURCE=500 -D_BSD_SOURCE -g -DENDEBUG
LFLAGS =
SERVEROBJECTS = calserver.c
CLIENTOBJECTS = calclient.c
HEADEROBJECTS = cal.h

all: clean calclient calserver
 
calclient :
	$(CC) $(LFLAGS) $(CFLAGS) $(CLIENTOBJECTS) $(HEADEROBJECTS) -o calclient -lsem182

calserver :
	$(CC) $(LFLAGS) $(CFLAGS) $(SERVEROBJECTS) $(HEADEROBJECTS) -o calserver -lsem182

clean:
	rm -f calserver calclient

.PHONY: clean
```
##Variablen
in Variablen kann man Dinge speichern z.B. Zahlen, Buchstaben,...<br>
```
int meineColleZahl = 42;
```
Mit Variablen kann man rechnen.
```
int summand1 = 42;
int summand2 = 23;
int summe = summand1 + summand2;
```
Mit Buchstaben kann man, aber nicht rechnen^^.
###Variablentypen
In c muss man wenn man eine Variable definiert einen Typ angeben (Glanzzahl,Dezimalzahl,Buchstabe,...) damit das Programm den Speicher im RAM reservieren kann.

|Type|Explanation|
|--------|--------|
|char|ein einzelner Buchstabe|
|short|16Bit lange Zahl|
|int|16Bit lange Zahl|
|long|32Bit lange Zahl|
|float|Fließkommazahl|
|doulbe| längere Fließkommazahl|

es gibt noch viel mehr [Datentypen](http://en.wikipedia.org/wiki/C_data_types)

##Arrays
Arrays sind mehrere Variablen zusammengefasst in eine Variable. Das bedeutet man kann in einer Variable mehre Werte speichern. Das wird sehr oft für Zeichenketten verwendet in dem man ein char array macht. Einem Array muss man immer bei der deklaration die Größe angeben damit das System den Speicher reservieren kann. Man kann Arrays auf mehrere Arten definieren.
```
char string[12];
string[0] = 'H';
string[1] = 'a';
string[2] = 'l';
string[3] = 'l';
string[4] = 'o';
string[5] = ' ';
string[6] = 'W';
string[7] = 'e';
string[8] = 'l';
string[9] = 't';
string[10] = '!';
string[10] = '\0';
```
Wenn man ein char Array erstellt und es befüllt sollte man am Ende des strings ein 0Byte hinzufügen damit man weiß wo der string aufhört.
```
char arr[] = {'c','o','d','e','\0'};
```
Strings kann man auch einfach hinschreiben und der Rest geschieht automatisch.
```
char arr[] = "code";
```

weitere Beispiele zu Arrays in c: http://www.thegeekstuff.com/2011/12/c-arrays/
##Funktionen
Wenn man Dinge immer wieder braucht kann man Teile des Sourcecode in Funktionen(Abschnitte) unterteilen und diesen einen Block immer wieder verwenden. Das bedeutet man muss den Code nur einmal schreiben. <br><br>

1. Eine Funktion besteht aus einem Funktionskopf der beschreibt: 
	1. welchen Datentyp die Funktion zurück gibt
	1. den Namen der Funktion
	1. die Parameter die der Funktion übergeben werden
1. einem Funktionskörper der von geschwungenen Klammern abgegrenzt wird und innerhalb des Funktionskörpers der Befehl **return** der angibt was von der Funktion zurückgeben wird.

Eine Funktion kann man aufrufen in dem man ihre Namen schriebt und die Parameter angibt.
```
int main(void){
	int Ergebnis = addieren(23,42);
}

int addieren(int summand1, int summand2){
	return summand1 + summand2;
}
```
Alle Variablen die innerhalb der Funktion deklariert werden sind nur innerhalb der Funktion sichtbar das gilt auch für die Parameter der Funktion. Weiters werden die übergeben Parameter in die Funktion kopiert. Das bedeutet wenn diese innerhalb der Funktion geändert werden ändern sie sich nicht außerhalb der Funktion.

##Pointers
Ein Pointer ist direkte Adresse die auf eine Variable im RAM zeigt. Das bedeutet mit dieser Adresse kann man Variablen direkt von überall bearbeiten und auslesen.<p>

Deklaration:
```
int *myPointer;
```

Deklaration und Definition:
```
int zahl = 42;
int *myPointer = &zahl;
```
Auflösen eines Pointers:
```
int zahl2 = *myPointer;
```

Mit Hilfe von Pointern können wir Variablen auch außerhalb einer Funktion bearbeiten.

##Ausgaben
Zu beginn wird sich alles im Terminal abspielen und da wir sehen wollen was unsere Programme so machen müssen wir das auch wieder ausgeben. Eine wichtige Funktion hierzu ist **printf**.
t
```
printf("Hallo Welt");
```
Zahlen kann man nicht einfach so ausgeben. Man muss sie in einem formatierten String ausgeben. Das bedeutet man gibt **printf** einen String zur Ausgabe der an bestimmten Stellen Platzhalter für die Zahlen bzw. Variablen hat. Weiters muss man die Variablen printf übergeben.
```
printf("%i",42);

float zahl = 23.333;
printf("Meine coole Zahl:%f",zahl);
```
| Symbol | Datentyp |
|--------|--------|
|%i or %d|int|
|%c|char|
|%f|float or double|
|%s|string|

##Eingabe
Um dem Programm Daten zu geben z.B. Usereingaben kann man die Funktion **scanf** verwenden.
```
int zahl;
scanf("%d",&zahl);
```

##Schleifen
Wenn man etwas iterativ lösen möchte kann man das mit Schleifen lösen. Wenn man z.B. alle Werte eines Arrays ausgeben möchte.

###for
eine for-Schleife besteht aus einer Laufvariable (wird oft i genannt), einer Bedingung wie lange die Schleife laufen soll. und was nach nach jedem Durchlauf passieren soll.<p>

```
int array = {0,1,2,3,4};
int i;
for(i = 0; i < 5; i++){
	printf("%i\n",array[i]);
}
```

###while
Eine while-schleife läuft solange die Bedingung erfüllt ist.

```
int i = 1;
while(i != 10){
	printf("Durchgang:%s":\n,i);
}
```

###do-while
Eine do-while-Schleife führt den ersten Schleifendurchlauf auf jeden fall aus und prüft erst nach dem ersten Durchlauf die Bedingung.

```
int zahl = -1;
do{
	zahl = zahl + 1;
	}while(zahl < 10);
```

##Kontrollstruckturen
Variablen abhängib den Verlauf des Progrmmes steuern.
###if
Wenn ein bestimmter Fall zurifft soll etwas gemacht werden, wenn nicht soll etwas anders gemacht werden.
```
double dividieren(int divident, int divisor){
	if(divisor != 0){
    	return divident/divisor;
    }else{
    	printf("error");
    	return 0;
    }
}
```

###switch
```
int myFancyFunction(char c){
	switch(c){
    	case 'a'  :
       		return 42;
       		break; /* optional */
    	case 'b' :
       		retrun 23;
       		break; /* optional */
  
    	/* you can have any number of case statements */
    	default : /* Optional */
       		return -1;
	}
}
```

##Kommentare
```
//egal was ich hier schreibe es wird vom Compiler ignoriert.
/*
so wird alles
zwischen
den Begrenzungen ignoriert. */
```

##includes
```
#include <stdio.h>
#include <math.h>
```

Damit nicht jeder Programmierer das Rad neu erfinden muss gibt es viele bereits vordefinierte Funktionen und Konstanten in sogenannten *Libaries*. Diese werden über *includes* zum Programm hinzugefügt. Diese includes schreibt man ganz zu beginn eines Files hin und diese gelten auch nur innerhalb dieses Files.

##makros
```
#define MAXENTRIES (365)
```

##Links
###Programmierenlernen
* http://openbook.galileocomputing.de/c_von_a_bis_z/
* http://codingbat.com/
* http://programmingbydoing.com/
* http://www.geekybrains.com/2013/02/best-websites-to-learn-coding-easily.html
* https://www.udacity.com/course/cs046
* http://www.thegeekstuff.com/2011/12/c-arrays/
* http://www.learnconline.com/2010/04/c-programming-examples.html

### OS X 
* [Compiler verwenden/installieren](http://stackoverflow.com/questions/9353444/how-to-use-install-gcc-on-mac-os-x-10-8-xcode-4-4)
* Texteditor: [Textmate](http://macromates.com/)
