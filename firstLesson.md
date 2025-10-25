

1.Retele Locale 
- **SOHO** (Small Office/Home Office) Networks
- Exemplu de retele SOHO In Cisco Packet Tracer:


Cablul ce conecteaza cele doua calculatoare se numeste: **Copper Crossover** (Cablu Incrucisat).

Se foloseste acest tip de cablu cand conectam doua dispozitive de acelasi tip.

Cablul (fie el Crossover sau Straight-Through) se conectează fizic la portul **RJ45** al Placi de Retea (Network Interface Card - NIC) a calculatorului.

OK, sa revenim la ce facem in Cisco Packet Tracer: 

1.Setam IP-urile pentru fiecare PC:
assets/SchemaSOHO.png

| **Clasa** | **Daca incepe cu...** | **Autocompletare Masca** | Reteaua(Network ID)            | Host(gazda)       |
| --------- | --------------------- | ------------------------ | ------------------------------ | ----------------- |
| **A**     | $1$ - $126$           | **$255$**.0.0.0          | Primul număr din adresa IP     | Ultimele 3 numere |
| **B**     | $128$ - $191$         | **$255.255$**.0.0        | Primele 2 numere din adresa IP | Ultimele 2 numere |
| **C**     | $192$ - $223$         | **$255.255.255$**.0      | Primele 3 numere din adresa IP | Ultimul număr     |
|           |                       |                          |                                |                   |

Exemple IPv4:
->**Clasa A** : 10.50.15.2
->Clasa B:  172.16.1.5
->Clasa C:  192.168.1.10


**Masca de retea** este un numar de 32 de biti care separa o adresa IP in doua parti: 
- Network ID
- Host ID

Doua calculatoare pot comunica daca sunt in aceeasi retea in functie de **tipul de conexiune ce se afla intre ele**: 

- doua PC-uri conectate intre ele (exemplu de mai sus) nu pot comunica prin cablu intre ele daca nu au aceeasi retea.
*(Calculatorul va vedea ca destinatia e in alta retea și va incerca sa trimita pachetul la un router (Default Gateway), nu direct prin cablu către celalalt PC. Cum nu există un router, pachetul se pierde.)*
- doua PC-uri conectate la un switch tot **nu pot** comunica intre ele daca nu se afla amandoua in aceeasi retea.
 *(PC1 **nu** va trimite pachetul catre switch. De ce? Pentru ca switch-ul este folosit doar pentru a vorbi cu vecinii din aceeași retea. Din moment ce PC1 a decis ca destinatia e in alta retea, el nici macar nu va incerca sa o gasească pe switch. El va cauta un **Router** (Gateway) pe care sa-l trimita.)*


La randul lor fiecare clasa (retea) poate fi subdivizata in subretele. Pentru o intelegere mai amanuntita luam exemplele de mai sus: 

->**Clasa A** : 
IPv4: 10.50.15.2
**Network ID**: 10
**Host ID**: 50.15.2
Masca: 255.0.0.0

***Creem o subretea:*** 
          Masca noua:255.255.0.0
          Noua regula: Network ID-ul este definit de primele doua numere. (Ai "împrumutat" numărul  50 din partea de host și l-ai transformat într-o parte a noului Network ID (subrețeaua).)
          **Network ID (Subreteaua):** 10.50
          **Host ID (în cadrul subretelei):** 15.2
        
->Clasa B:  172.16.1.5
->Clasa C:  192.168.1.10

--------------------------------------------------------------------------

CONTEXT ACTUAL :
In proiectul nostru, ele au  același Network ID: * 
PC1: `192.168.1.10` (Retea: **`192.168.1`**) * 
PC2: `192.168.1.11` (Retea: **`192.168.1`**)


REVENIND LA CISCO PACKET TRACER: 

2.Facem Ping
Ping este un instrument de diagnosticare a rețelei care testeaza daca poti ajunge la un alt calculator.
PC1 trimite un mic pachet de date (numit **ICMP Echo Request**) catre adresa de destinație PC2.
Daca PC2 primeste pachetul si este functional, el raspunde imediat cu propriul pachet (un **ICMP Echo Reply**).

Click pe PC1 ->Desktop -> Command Prompt  -> tastam ping urmata de IP-ul celuilalt calculator

![Ping reușit către PC2](/assets/ping1.png)

FELICITARIII   ATI REUSIT SA FACEM IMPREUNA PRIMUL PROGRAM IN PACKET TRACER !!!!!!!!!!!!!!!!!!!! XD

OK, poate te inca esti confuz cu acest ping, dar el doar verifica daca functioneaza conexiunea intre dispozitive. 

Acum hai sa adaugam, o imprimata: 

![Eroare la conectarea imprimantei](/assets/printer_cannot_connect.png)

De ce credeti ca da eroarea aceasta ?  Hmmmm

Pai sa ne gandim, un calculator are o placa de retea, care arata care arata cam asa: 
![Portul RJ45 al unei plăci de rețea](/assets/placa de retea.png)

Cum se si vede are doar un singur port.  In cazul actual noi daca am conectat cu un **Copper Crossover** cele doua calculatoare, nu mai ramane nici un port pentru a conecta imprimanta. AICI INTERVINE SWITCH-UL.

Ce este oare un SWITCH ?

Un device fizic care conecteaza mai multe dispozitive pentru a crea o retea locala LAN(Local Area Network). In contextul actual ne trebuie un asemenea device deoarece, cum am precizat mai sus vrem sa conectam calculatoarele la imprimanta si nu avem cum. Cu ajutorul switch-ului conectam calculatoarele la acesta si dupa switch-ul la imprimanta. 

Deci tot in acelasi proiect in packet tracer adaugam o imprimanta dar si un switch.
![Schema SOHO cu Switch și Imprimantă](/assets/Soho_cu_imprimanta.png)
Calculatoarele le-am configurat mai sus acum ramane doar imprimanta. Intai sa ne gandim la o adresa IPv4 pentru aceasta, 192.168.1.12. 
Pentru a configura adresa IP la imprimanta dam click pe aceasta -> Config ->FastEthernet0 


![Configurare IP Imprimantă](/assets/config_printer.png)


Inchidem fereastra, apasam pe PC1 si vedem daca imprimanta este detectabila. 

Cum credeti ca facem asta ?  

Tot cu ajutorul lui ping, instructiunile sunt aceleasi ca cele de sus, doar ca dupa ping trebuie sa adaugati adresa IPv4 a imprimantei. 

Siii..... TADAM !!!!! Totul a functionaatt, imprimanta a fost recunoscuta

![Ping reușit către imprimantă](/assets/ping_imprimanta.png)

Ok, acesta a fost primul programel in Packet Tracer, sper ca a fost distractiv.













