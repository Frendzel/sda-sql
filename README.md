# DOCKER
By default after deployment MySQL has following connection restrictions:

### docker pull mysql/mysql-server:5.7
### Start your mysql image with all port mappings required:
  
```
docker run -p 3306:3306 --name=mysql57 -d mysql/mysql-server:5.7
```
or, if the complete port mapping is required:

```
docker run -p 3306:3306 -p 33060:33060 --name=mysql57 -d mysql/mysql-server:5.7
```

### If this is the fresh installation - grab the default password:
docker logs mysql57 2>&1 | grep GENERATED

### Connect using mysql client directly to the mysqld in docker
```
docker exec -it mysql57 mysql -uroot -p
```

###If this is the fresh installation you will be asked to change the password using ALTER USER command. Do it.
```
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'root';
```   

### Run SQL
```
update mysql.user set host = '%' where user='root';
```

### Quit the mysql client and restart container
```
docker restart mysql57
```

### Now you will be able to connect from MySQL Workbench to
    
host: 0.0.0.0 
port: 3306
user: root
pass: root

# SQL

# ZADANIA WŁASNY SCHEMAT

##Zadanie 0
Zaprojektuj własny schemat

##Zadanie 1 (łatwe).
Zaimplementuj własny schemat w mysqlu (może być przez diagram ERD i forward engineering)

##Zadanie 2 (średnie).
Zamodeluj relacje przy użyciu instrukcji SQL

##Zadanie 3 (trudne).
Zastanów się w jaki sposób uzupełnić tabele przykładowymi danymi, jeżeli napotkasz trudności związane ze zbyt dużą liczbą constraintów na tabelach spróbuj uzupełnić je ręcznie niewielką ilością danych

##Zadanie 4 (trudne).
Twój schemat powinien zawierać co najmniej 
* 3 różne relacje, 
* 2 procedury składowane, 
* 2 funkcje, 
* 2 triggery
* 3 różne widoki.

# ZADANIA SCHEMAT EMPLOYEES

##ZADANIE 1

* Wyświetl dzisiejszą datę 
* Wyświetl aktualny rok:
* Wyświetl aktualny miesiąc:
* Wyświetl aktualny dzień:

##ZADANIE 2

* Policz wszystkich pracujących mężczyzn i kobiety.
* Policz wszystkich pracujących mężczyzn i kobiety urodzonych po 1960.

##ZADANIE 3
* Wyświetl imię i nazwisko pracownika w kolumnie zapisanej jako ‘rekin biznesu’ mężczyzn urodzonych po 1964 roku

##ZADANIE 4
* Policz rekinów biznesu i zapisz ich w danej kolumnie

##ZADANIE 5
* Policz ile osób pracuje na danym stanowisku

##ZADANIE 6
* Policz ile kobiet i ile mężczyzn pracuje na danym stanowisku

##ZADANIE 7 
* Wyświetl zarobki, imie i nazwisko pracownika wraz płcią, którzy zarabiają powyżej 150000 w konstrukcjach z JOIN i podzapytaniem z ANY (uwaga na ALL)

##ZADANIE 8 
* Wyświetl zarobki, imię i nazwisko pracownika wraz płcią, którzy zarabiają pomiędzy 145000 a 150000

##ZADANIE 9
* Wyświetlić mężczyznę i kobietę, którzy zarabiają najwięcej

##ZADANIE 10 
* Wyświetlić płeć, liczbę pracowników, średnie wynagrodzenie, sumę wynagrodzenia i maksymalne wynagrodzenie dla danej płci.

##Zadanie 11. 
* Dodać 250 pracowników do tabeli pracowników

##Zadanie 12.
* Policz ile jest oddziałów

##Zadanie 13.
* Wyświetl wszystkie zarobki audytowe pracowników, czyli takie, które już się zakończyły
* Utworz tabele audytowa i przenies tam dane z tabeli zarobkow.

* 3 instrukcje:
** select z tabeli zarobkow
** insert do tabeli audytowej
** delete z tabeli zarobkow

##Zadanie 14.
* Dokonać operacji zmiany płci

##Zadanie 15.
* Dokonać odwrotnej operacji zmiany płci w celu przywrócenia danych pierwotnych

##Zadanie 16. 
* Wykorzystaj instrukcję DATEDIFF i TIMEDIFF

##Zadanie 17. 
* Wyświetl pogrupowane po zawodzie średnie zarobki pracowników na danych stanowiskach większe niż 5000.
<podpowiedź -> having>

#PROCEDURY/FUNKCJE

##Zadanie 1.

Napisz procedurę dodawania pracowników

##Zadanie 2.
Napisz procedurę dającą awans

##Zadanie 3.
Napisz procedurę usuwającą pracownika z firmy

##Zadanie 4.
Napisz funkcję obliczającą średnią pensję dla danego stanowiska

#TRIGERY

##Zadanie 1.
Dodaj tabelę audytową pracowników

##Zadanie 2. 
Napisz trigger, który po usunięciu pracownika wstawi jego dane do tabeli audytowej.

#WIDOKI

##Zadanie 1. 
Zapisz w formie widoków i wyświetl dowolne zapytanie wykonane podczas zajęć.

#Zadania dodatkowe
https://sqlzoo.net/

#Dodatkowe linki:

##do testowania mysqla bez instalacji:
http://sqlfiddle.com/#!9/a6c585/1

##SQL INJECTION
https://www.w3schools.com/sql/sql_injection.asp

##EBOOKI
https://ebookpoint.pl/ksiazki/jezyk-sql-przyjazny-podrecznik-wydanie-ii-larry-rockoff,jsqlp2.htm

##IDE
https://blog.jetbrains.com/datagrip/2019/03/11/top-9-sql-features-of-datagrip-you-have-to-know/?utm_source=facebook&utm_medium=cpc&utm_campaign=ww_en_ww_datagrip_fb_na_cont&fbclid=IwAR0xIZu-zmkeZC7_qZV4sPiFvjxgUT61hM7vi_yZrTmHvRG83F2fwd2YK9A

#PODSUMOWANIE:
 
1. ACID
2. FUNKCJE AGREGUJĄCE
3. INDEKSY - po co
4. SEKWENCJE, kiedy mogą być używane?
5. RODZAJE RELACJI 
6. DOBRE PRAKTYKI PRZY MODELOWANIU BAZ DANYCH
7. SQL vs NOSQL
8. SPOSÓB ŁĄCZENIA TABEL
9. OGRANICZENIA DANYCH W TABELACH
10. JAKIE ZNASZ BAZY SQL