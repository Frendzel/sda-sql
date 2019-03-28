# DOCKER
Wykonaj poniższą instrukcję, aby zainstalować poprawnie obraz mysql servera w wersji 5.7
```
docker pull mysql/mysql-server:5.7
```

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

### If this is the fresh installation you will be asked to change the password using ALTER USER command. Do it.
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

# Schemat employees

Wywołać poniższe skrypty w następującej kolejności na bazie:

* employees.sql
* load_departments.dump ;
* load_employees.dump ;
* load_dept_emp.dump ;
* load_dept_manager.dump ;
* load_titles.dump ;
* load_salaries1.dump ;
* load_salaries2.dump ;
* load_salaries3.dump ;

Jeżeli użyłeśdockera wykorzystaj poniższe polecenia:
```
docker exec -i mysql57 mysql -uroot -ppassword < employees.sql
docker exec -i mysql57 mysql -uroot -ppassword < load_departments.dump
docker exec -i mysql57 mysql -uroot -ppassword < load_employees.dump
docker exec -i mysql57 mysql -uroot -ppassword < load_dept_emp.dump
docker exec -i mysql57 mysql -uroot -ppassword < load_dept_manager.dump
docker exec -i mysql57 mysql -uroot -ppassword < load_titles.dump
docker exec -i mysql57 mysql -uroot -ppassword < load_salaries1.dump
docker exec -i mysql57 mysql -uroot -ppassword < load_salaries2.dump
docker exec -i mysql57 mysql -uroot -ppassword < load_salaries3.dump
```

Jeżeli zdecydowałeś się na instalację mysqla za pomocą standardowego instalatora wystarczy uruchomić plik:
```
mysql -uroot -ppassword < employees-standard.sql
```

# SQL

# ZADANIA SCHEMAT EMPLOYEES

## ZESTAW 1
* Wyświetl dzisiejszą datę
```
select sysdate();
```
* Wyświetl aktualny rok:
```
select year(sysdate());
```
* Wyświetl aktualny miesiąc:
```
select month(sysdate());
```
* Wyświetl aktualny   dzień:
```
select day(sysdate());
```

Alternatywnie:

``` SELECT curdate(), year(current_date()), month(current_date()), dayofmonth(current_date()); ```
## ZESTAW 2
* Wyszukaj wszystkich pracowników?
```
select * from employees;
```
* Wyszukaj wśród pracowników wszystkich mężczyczn.
```
select * from employees where gender = 'M';
```
* I ogranicz wyniki do 10
```
select * from employees where gender = 'M' limit 10;
```
* Znajdź 30 najstarszych pracowników
```
select * from employees order by birth_date limit 30;
```
* Ile było i jest w firmie zatrudnionych pracowników?
```
select * FROM employees.dept_emp;
```
* Ilu inżynierów ('engineer') pracuje obecnie w firmie (tabela titles)?
```
select count(*) from employees e join titles t on e.emp_no = t.emp_no where title = 'Engineer'
```
* Policz wszystkich pracujących mężczyzn i kobiety.
```
select gender ,count(*) as ‘liczba pracownikow’ from employees 
group by gender;
```
* Policz wszystkich pracujących mężczyzn i kobiety urodzonych po 1960.
```
select count(*)'Pracowncicy urodzeni po 1960', gender 
from employees
where year(birth_date) > 1960
group by gender;
```
## ZESTAW 3
* Znajdź największe wynagrodzenie.
```
```
* Znajdź najmniejsze wynagrodzenie.
```
```
* Wyświetl imię i nazwisko pracownika w kolumnie zapisanej jako ‘rekin biznesu’ mężczyzn urodzonych po 1954 roku
```
```
## ZESTAW 4
* Policz rekinów biznesu i zapisz ich w danej kolumnie
```
```
## ZESTAW 5
* Policz ile osób pracuje na danym stanowisku
```
```
## ZESTAW 6
* Policz ile osób pracuje na jakim stanowisku.
```
```
* Policz ile kobiet i ile mężczyzn pracuje na danym stanowisku.
```
```
* Na których stanowiskach pracuje więcej niż 100 000 osób? (HAVING)
```
```
## ZESTAW 7 
* Wyświetl zarobki, imie i nazwisko pracownika wraz płcią, którzy zarabiają powyżej 150000 w konstrukcjach z JOIN i podzapytaniem z ANY (uwaga na ALL)
```
```
## ZESTAW 8 
* Wyświetl zarobki, imię i nazwisko pracownika wraz płcią, którzy zarabiają pomiędzy 145000 a 150000
```
```
## ZESTAW 9
* Wyświetlić mężczyznę i kobietę, którzy zarabiają najwięcej
```
```
## ZESTAW 10 
* Wyświetlić płeć, liczbę pracowników, średnie wynagrodzenie, sumę wynagrodzenia i maksymalne wynagrodzenie dla danej płci.
```
```
## ZESTAW 11. 
* Dodać 250 pracowników do tabeli pracowników
```
```
## ZESTAW 12.
* Policz ile jest oddziałów
```
```
## ZESTAW 13.
* Wyświetl wszystkie zarobki audytowe pracowników, czyli takie, które już się zakończyły
```
```
* Utworz tabele audytowa i przenies tam dane z tabeli zarobkow.
```
```
* 3 instrukcje:
** select z tabeli zarobkow
** insert do tabeli audytowej
** delete z tabeli zarobkow

## ZESTAW 14.
* Dokonać operacji zmiany płci
```
```
## ZESTAW 15.
* Dokonać odwrotnej operacji zmiany płci w celu przywrócenia danych pierwotnych
```
```
## ZESTAW 16. 
* Wykorzystaj instrukcję DATEDIFF i TIMEDIFF
```
```
## ZESTAW 17. 
* Wyświetl pogrupowane po zawodzie średnie zarobki pracowników na danych stanowiskach większe niż 5000.
<podpowiedź -> having>
```
```
* Na których stanowiskach pracuje więcej niż 100 000 osób? (having)
```
```
## Zadnaie 18.
* Znajdź wszystkich managerów działu Development.
```
```
## ZESTAW 19. 
* Który dział zatrudnia obecnie najwięcej osób?
```
```
## ZESTAW 20. 
* Stwórz raport zarobków obecnych managerów od najmniej
zarabiających do najlepiej zarabiających podając działy w
których pracują.
(Nazwa działu, Imię, Nazwisko, Wynagrodzenie)
```
```
## ZESTAW 21.
Który dział miał najwięcej managerów?
```
```
## ZESTAW 22.
Znajdź najlepiej zarabiającą, obecnie zatrudnioną kobietę.
```
```
# PROCEDURY/FUNKCJE

## ZESTAW 1.

Napisz procedurę dodawania pracowników
```
```
## ZESTAW 2.
Napisz procedurę dającą awans
```
```
## ZESTAW 3.
Napisz procedurę usuwającą pracownika z firmy
```
```
## ZESTAW 4.
Napisz funkcję obliczającą średnią pensję dla danego stanowiska
```
```
# TRIGERY

## ZESTAW 1.
Dodaj tabelę audytową pracowników
```
```
## ZESTAW 2. 
Napisz trigger, który po usunięciu pracownika wstawi jego dane do tabeli audytowej.
```
```
# WIDOKI

## ZESTAW 1. 
Zapisz w formie widoków i wyświetl dowolne zapytanie wykonane podczas zajęć.
```
```
# ZADANIA WŁASNY SCHEMAT

## ZESTAW 0
Zaprojektuj własny schemat

## ZESTAW 1 (łatwe).
Zaimplementuj własny schemat w mysqlu (może być przez diagram ERD i forward engineering)

## ZESTAW 2 (średnie).
Zamodeluj relacje przy użyciu instrukcji SQL

## ZESTAW 3 (trudne).
Zastanów się w jaki sposób uzupełnić tabele przykładowymi danymi, jeżeli napotkasz trudności związane 
ze zbyt dużą liczbą constraintów na tabelach spróbuj uzupełnić je ręcznie niewielką ilością danych

## ZESTAW 4 (trudne).
Twój schemat powinien zawierać co najmniej 
* 3 różne relacje, 
* 2 procedury składowane, 
* 2 funkcje, 
* 2 triggery
* 3 różne widoki.

# Zadania dodatkowe
https://sqlzoo.net/

# Dodatkowe linki:

## do testowania mysqla bez instalacji:
http://sqlfiddle.com/#!9/a6c585/1

## SQL INJECTION
https://www.w3schools.com/sql/sql_injection.asp

## EBOOKI
https://ebookpoint.pl/ksiazki/jezyk-sql-przyjazny-podrecznik-wydanie-ii-larry-rockoff,jsqlp2.htm

## IDE
https://blog.jetbrains.com/datagrip/2019/03/11/top-9-sql-features-of-datagrip-you-have-to-know/?utm_source=facebook&utm_medium=cpc&utm_campaign=ww_en_ww_datagrip_fb_na_cont&fbclid=IwAR0xIZu-zmkeZC7_qZV4sPiFvjxgUT61hM7vi_yZrTmHvRG83F2fwd2YK9A

# PODSUMOWANIE:
 
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