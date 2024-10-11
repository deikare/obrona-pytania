# Część podstawowa

## Porównać "siłę wyrazu" automatu skończonego, automatu ze stosem oraz maszyny Turinga. Jakie klasy języków rozpoznaje każdy z nich?
 izi
 

## Omówić i porównać algorytmy najkrótszej ścieżki wskazując ich kluczowe właściwości i logikę budowy: Dijkstry, Belmana-Forda, A*
izi


## Omówić zagadnienia redundancji i normalizacji w relacyjnej bazie danych oraz wynikające z tego wymagania

izi

## Dlaczego baza danych stanowi dobry fundament do budowy wielu systemów informatycznych?
izi

## Jaki jest cel uzgadniania trójetapowego (three way handshake) w protokole TCP? Jaka jest interpretacja numerów sekwencyjnych i potwierdzenia? Jaka jest wartość początkowa numeru sekwencyjnego?

Three way handshake:
1) A-B: SYN z numerem sekwencyjnym segmentu x
2) B-A: SYN ACK z numerem sekwencyjnym segmentu x+1
3) A-B: ACK z numerem sekwencyjnym segmentu x+2

Każdy segment wysyłany jest opisany numerem sekwencyjnym, żeby zachować kolejność wysyłanych segmentów - ten numer jest inkrementowany o liczbę przesyłanych bajtów.

Numer potwierdzenia - informacja, segmentu o jakim kolejnym numerze spodziewa się otrzymać odbiorca - jest to tak naprawdę numer ostatnio otrzymanego bajtu + 1

Początkowa wartość to liczba losowa, żeby zabezpieczyć wysyłanie danych i zabezpieczyć się przed sytuacją, gdzie opóźnione segmenty będą błędnie zinterpretowane jako dane wysyłane w ramach aktualnej komunikacji


## Procesy i wątki w systemie operacyjnym. Omówić budowę, szybkość działania i zakres zastosowania. Przedstawić problemy i możliwości komunikacji i synchronizacji.

Proces - uruchomiona instancja programu wraz ze środowiskiem wykonywania:
* informacje o procesie - id procesu, id rodzica, priorytet, otrzymane sygnały
* kod programu - adres kodu, stos, segment danych
* segment danych - otwarte wskaźniki, tablica stron procesu
* stan procesu - wartości rejestrów procesora, licznik programu

Wątek - podstawowa część procesu - odpowiada za wykonywanie jednej sekwencji sterowania w procesie. Wątek jest niskopoziomą jednostką:
* oddzielny stos, rejestry dla każdego wątku
* wątki tego samego procesu współdzielą jego zasoby
* mamy wątki procesu użytkownika oraz wątki w ramach jądra systemu

Problemy:
* wyścigi - ... izi
* deadlock - wątki/procesy oczekują wzajemnie na siebie - rozwiązaniem jest np. nadzorca monitorujący deadlocki, odpowiednie pisanie wątków z timeoutami
* zagłodzenie - wątek nie może dostać się do wykonania
* inwersja priorytetów - wątek o niższym priorytecie zajmuje zasób i o wyższym nie może się dostać do zasobu
* problemy izolacji/synchronizacji dostępu do danych

Rozwiązania komunikacji:
* IPC - wywołania systemowe (np. sleep() wakeup()), kolejki wiadomości, współdzielona pamięć
* wątki - semafory (w tym mutex), monitory, aktywne oczekiwanie (nie rozwiązuje to problemów synchronizacji)


## Scharakteryzować problemy i mechanizmy zarządzania pamięcią. Porównać cechy i przeznaczenie mechanizmów stronicowania i segmentacji.

Typy zarządzania pamięcią:
* brak zarządzania - jeden proces okupuje w danej chwili pamięć adresową
* współdzielona pula adresów - problemy z izolacją danych i dynamicznym przydzielaniem pamięci
* pamięć wirtualna - użycie pamięci operacyjnej (mniejszej i szybszej) oraz większej i wolniejszej pamięci pomocniczej do zwiększenia puli adresów - niekoniecznie istnieje bezpośrednia translacja adresów wirtualnych pamięci na adresy fizyczne

Mechanizmy:
* alokacja statyczna - znany jest przed uruchomieniem procesu całkowity rozmiar potrzebnych danych w procesie. Łatwe, ale ograniczone, bo nie wszystkie procesy takie są + może marnotrawić zasoby
* dynamiczna - program dynamicznie prosi o dostęp w czasie działania do adresów - trudniejsze rozwiązanie, może prowadzić do fragmentacji, ale efektywniejsze jeżeli chodzi o przydział zasobów 
* stronicowanie
* segmentacja

Problemy:
* fragmentacja wewnętrzna - proces nie wykorzystuje pełnej puli adresów
* fragmentacja zewnętrzna - istnieją wolne pule adresów w pamięci, które są zbyt małe, żeby jakiś proces mógł zająć daną pulę adresów

Stronicowanie:
* zmapowanie obszarów wirtualnej pamięci (stron o stałych rozmiarach) do obszarów w pamięci fizycznej (ramek)
* każdemu procesowi przyporządkowana jest dana strona
* mechanizm niskiego poziomu służący do poszerzenia puli adresów adresów dostępnych w pamięci wirtualnej ponad pulę dostępną w pamięci fizycznej
* zadaniem mechanizmu jest odpowiednie wymiatanie zawartości ramki pomiędzy procesy o stronach współdzielących daną ramkę
* zapobiega fragmentacji zewnętrznej, ale umożliwia wewnętrzną

Segmentacja:
* podział pamięci na logiczne segmenty o numerze i adresie bazowym
* identyfikacja adresu przez nazwę segmentu + adres w segmencie
* mechanizm wyższego poziomu - programista ma możliwość zarządzania przestrzenią segmentów
* służy do efektywniejszego przydzielenia dostępu do pamięci
* może zapobiec fragmentacji wewnętrznej, ale umożliwia zewnętrzną

## Scharakteryzować standardy i narzędzia do modelowania procesów biznesowych
Standardy:
* BPMN - izi
* BPEL - język programowania odwzorowujący notację biznesową, skupia się na automatyzacji
* CMMN - szczególna odmiana BPMN - BPMN modeluje raczej standardowe procesy, a CMMN skupia się na procesach mocno dynamicznych, które nie są aż tak ustandaryzowane - np. szczególne decyzje, obsługa problematycznych klientów itp
* DMN - model struktury decyzyjnej, powiązań w ramach tej struktury oraz reguł decyzyjnych

Narzędzia:
* UML - istnieją sekwencje w UMLu, np opis przypadków użycia, sekwencja wywołań
Narzędzia:
* Microsoft Visio - lokalne narzędzie do modelowania procesów, ma m.in. standardowe procesy BPMN
* Lucidchart/draw.io - narzędzie w chmurze, ma AI do generowania modeli na podstawie opisu
* Camunda Modeler - narzędzie w chmurze, jest zintegrowane z Camunda BPM do automatyzacji procesów
* Bizagi Modeler - lokalny modeler na licencji freeware

## Przedstawić sieciowe modele optymalizacji stosowane w systemach zarządzania. Omówić ich właściwości.

Typowe modele:
* problem maksymalnego przepływu - ciągły - krawędzie to przepustowości - da się rozwiązać jako ZPL, Ford-Fullkersona
* najkrótsza ścieżka
* problem minimalnego kosztu przepływu - mieszany - krawędzie to przepustowości i koszty - ZPL
* problem przydziału - całkowitoliczbowy -  krawędzie to 1 lub 0 w zależności od tego, czy dany zasób jest przydzielony do konkretnej jednostki, w modelu są też całościowe dozwolone sumy przydziałów
* problem harmonogramowania - harmongramowanie zadań u różnych jednostek, gdzie różne etapy wymagają różnych czasów i jednostek - np. rozwiązać algorytmem Johnsona

Właściwości:
* powszechność problemu - w różnych branżach
* skomplikanie sieci
* efektywne rozwiązania - szczególny przypadek ZPL, więc istnieją efektywne algorytmy rozwiązania
* modelowanie wielowymiarowych problemów
* algorytmy i metody numeryczne - typowy metody rozwiązania ZPL, heurystyki, Ford-Fullerkson, algorytm Johnsona, metoda przeszukiwań przestrzeni


## Omówić szczegółowo teorie, definicje, standardy i narzędzia wykorzystywane przy projektowaniu i implementacji systemów opartych na koncepcji agenta i aktora.

Agent
* autonomiczna jednostka w systemie
* proaktywność - agent dąży do realizacji swojego własnego celu
* może komunikować się z pozostałymi elementami systemu oraz wchodzić z nimi w interakcję
* reaktywność - może podejmować akcje na podstawie stanu wewnętrznego i otoczenia agenta

Aktor:
* asynchroniczny model obliczeniowy
* ma swój własny stan wewnętrzny
* aktor dopóki nie zostanie wywołany przez jakiś inny element systemu jest pasywny

Teorie:
* Teoria aktów mowy - zdefiniowanie komunikatów, jakie wysyłają między sobą elementy systemu
* BDI - believes-desire-intentions - model opisujący zachowanie agentów na podstawie ich przekonań, pragnień i intencji
* Teoria gier - agenty konkurują ze sobą w jednym środowisku dążąc do maksymalizacji swoich zysków
* Teoria kontraktów - agenty mogą negocjować między sobą ustalone zachowania

Standardy:
* FIPA - otwarty standard definiujący komunikaty, możliwe zasady współpracy oraz protokoły negocjacyjne między agentami
Narzędzia:
* JADE - framework do tworzenia systemów wieloagentowych w Javie
* SPADE - w Pythonie, korzysta z XMPP do wymieniania wiadomości
* Akka Agent - w Scali, bez wsparcia FIPA

## Wymienić i szczegółowo opisać wybrane algorytmy i metody wykorzystywane w systemach wieloagentowych i aktorowych

* Algorytmy przeszukiwania najkrótszej ścieżki w grafie - agenty mogą ich używać, aby dostać się jak w najszybszym czasie do...
* Inkrementalne drzewa decyzyjne - na podstawie doświadczeń negatywnych i pozytywnych agenta w ramach jego działania agent może uczyć w sobie model dynamicznego drzewa decyzyjnego
* Algorytmy minmax - agent może minimalizować koszty swojego fukcjonowania, zakładając jednocześnie, że środowisko agenta dąży do zmaksymalizowania swojego zysku
* Algorytmy aukcyjne - używane do alokacji i przydzielania zadań - np. aukcja holenderska, gdzie zaczyna się wysoką ceną, a aukcja kończy się w momencie, aż któryś z agentów zdecyduje się zaakceptować ofertę
* Algorytmy przydziału zadań
* Rozproszone uczenie się - agenci mogą korzystać z uczenia ze wzmocnieniem, korzystając ze swoich wzajemnych doświadczeń - przyspiesza to znacząco proces skutecznego uczenia się
* Q-learning - algorytm uczenia ze wzmocnieniem, gdzie:
  * agent działa w środowisku
  * ma przypisaną tablicę Q wartości, która jest zbiorem wartości przypisanych parze stan, akcja - każda wartość to oczekiwana długotrwała korzyść w stanie i przy danej akcji
  * w każdym kroku po podjęciu akcji agent otrzymuje informację w postaci nagrody/kary na podstawie efektywności
  * i w ostatnim kroku aktualizuje Q(s,a) jako = Q(s,a) + wsp.uczenia *(nagroda + wsp.dyskontu * max Q(s',a') w dowolnych przyszłych stanach i akcjach - obecne Q(s,a))

Zalety:
* środowiska rozproszonego, więc można zrównoleglać obliczenia
* dążą do optymalności rozwiązania mimo asynchroniczności środowiska

Wady:
* nie muszą osiągać rozwiązania optymalnego, bo agenty niekoniecznie muszą ze sobą współpracować
* zależne od parametrów


## Omówić metody modelowania architektury systemów informatycznych. Przedstawić cele i metody modelowania architektury.

Modelowanie architektury - stworzenie wielopoziomowej architektury systemu opierającej o zebranie wymagań funkcjonalnych i niefunkcjonalnych, model komponentów systemu, model interakcji i flow w systemie, model przesyłanych danych, model implementacji oraz wdrożenia
Cele:
* wysokopoziomowy opis systemu
* komunikacja pomiędzy IT oraz biznesem
* podejmowanie stabilnych, wczesnych decyzji, nie pozostawianie decyzji projektowych przypadkowi
* możliwość stosowania wzorców 
* wykrycie potencjalnych problemów

Metody:
* UML - język tworzenia diagramów - np. diagram klas, przypadków użycia, sekwencji, wdrożenia
* Architektura warstwowa - podział systemu na warstwy - ułatwienie zarządzania, modelowanie od ogółu do szczegółu
* Metoda 4+1 - scenariusze (przypadki użycia), widok logiczny (model warstwowy), procesowy (sekwencje), implementacja (diagram klas), fizyczna (model wdrożenia)
* Attribute-Driven Design (ADD) - najpierw identyfikujemy atrybuty jakości (np. bezpieczeństwo/wydajność), potem wybieramy taktyki dla każdego atrybutu i iteracyjnie przygotowujemy projekt architektury

## Czemu służą wzorce architektoniczne? Jak powstają? Jak są katalogowane? Omówić przykładowe wzorce architektoniczne.

Wzorce architektoniczne - ustalony wzorzec struktury systemu IT na różnych poziomach abstrakcji

Powstawanie:
* identyfikacja typowego problemu
* projektowanie wzorca
* implementacja i weryfikacja
* dokumentacja

Katalogowanie:
* według celu - skalowalność, bezpieczeństwo, elastyczność itp.
* według skali - monolit, mikroserwisy
* według struktury - wzorce warstwowe, klient-serwer, mikroserwisy...
* Według zastosowań

Przykłady:
* MVC
* Architektura warstwowa
* Komunikacja publish-subscribe
* Mikrousługi
* Repozytorium


## Przedstawić warunki konieczne i dostateczne optymalności różniczkowalnych zadań optymalizacji bez ograniczeń i z ograniczeniami oraz warunki regularności i omówić metody poszukiwania rozwiązań zadań optymalizacji nieliniowej.

1) Bez ograniczeń - jeśli f wypukła, to min. lokalne = globalne
    * war.konieczny - gradient f celu = 0
    * war. wystarczający - hesjan (macierz drugich pochodnych) ściśle dodatnia  / ujemna (jeżeli problem był maksymalizacją)
2) Z ograniczeniami:
    * war.konieczny - KKT:
      * gradient funkcji lagrange'a = 0
      * wszystkie ograniczenia spełnione
      * dla ogr. nierównościowych mnożniki >= 0
      * dla ogr. nierównościowych mnożnik * ogr. = 0
    * war.wystarczający:
      * f celu wypukła i ogr. nierównościowe też
      * ogr. równościowe są liniowe
      * zadanie jest regularne, czyli niezerowe i lnz gradienty ogr. aktywnych, domknięcie zbioru dopuszczalnych kierunków = zbiór możliwych kierunków poprawy

Metody poszukiwań rozwiązań:
* gradientowe - wykorzystują gradient funkcji celu w znalezieniu kolejnego kroku optymalizacji - gradient prosty, gradient sprzężony
* quasi-newtonowskie - gradientowe, gdzie długość kroku to przybliżony odwrotny Hesjan
* metody newtonowskie - czyli długość kroku to odwrotny Hesjan
* algorytmy ewolucyjne


## Omówić metody rozwiązywania zadań liniowych i kwadratowych optymalizacji

Zadania liniowe:
* simpleks - czyli zaczynamy z rozwiązania dopuszczalnego i próbujemy zamieniać zmienne bazowe z niebazowymi tak, aby poprawić funkcję celu - jeżeli cena zredukowana >= 0, to znaleziono rozwiązanie
* simpleks dwufazowy służy do znalezienia pierwszego dopuszczalnego rozwiązania
* simpleks dualny - tworzymy zadanie dualne do pierwotnego - funkcje ograniczeń stają się zmiennymi, a ograniczenia zmiennymi

Zadania programowania kwadratowego - ograniczenia liniowe, f celu kwadratowa
* metody gradientowe
* quasi-newtonowskie
* newtonowskie
* metoda ograniczeń aktywnych - badamy tylko ograniczenia aktywne w danym kroku, nieaktywne są ignorowane
* metoda punktu wewnętrznego - czyli zaczynamy wewnątrz ograniczeń i staramy się dochodzić bardzo blisko ograniczeń, badając kierunki rozwiązania


## Przedstawić koncepcję i przeznaczenie zegarów logicznych i wektorów stempli czasowych.
Zegary logiczne - koncepcja zwracania wartości timestampu dla momentu t. Zakłada, że jeżeli zdarzenie a > b, to L(a) > L(b) (zależność odwrotna nie musi być prawdziwa). Dzięki temu częściowo można ustalać chronologię zdarzeń w systemie

Wektory stempli czasowych - uogólnienie zegarów logicznych - w systemie rozproszonym złożonym z n każdy z procesów ma wektor o długości n reprezentujący jego timestamp + wyobrażenie o timestampie pozostałych. W ten sposób można aktualizować całkowity wektor, jeżeli otrzymany timestamp w wektorze od innego serwera w środowisku rozproszonym będzie >= od obecnego. W ten sposób da się ustalać ścisłą zależność między zdarzeniami, o ile zdarzenia są porównywalne, tzn. działa <= między zdarzeniami + istnieje przynajmniej jedna pozycja, że jest ściśle <. Wtedy mamy relację dwustronną, tzn. a < b <=> L(a) < L(b). Wektory stempli czasowych pozwalają zatem na rozpoznawanie współbieżności zdarzeń

Zatem zegary logiczne pozwalają na częściowe ustalanie chronologii zdarzeń, ale to wektory stempli czasowych pozwalają na wykrywanie współbieżności zdarzeń


## Omówić silne i słabe modele spójności danych w środowisku rozproszonym.

Silny model:
* spójność sekwencyjna - każdy proces widzi operacje w tej samej kolejności
* spójność liniowa (atomowa) - jak sekwencyjna i zachowana jest rzeczywista chronologia operacji

Słaby model:
* eventual consistency - w końcu dane będą spójne, jeżeli nie będzie modyfikacji
* spójność przy czytaniu własnych zapisów
* spójność przyczynowa, jeżeli B wynika przyczynowo z A, to wszyscy użytkownicy zobaczą A przed B
* spójność w ramach jednej sesji użytkownika

Silny model:
* każda modyfikacja danych w środowisku rozproszonym jest natychmiast propagowana na wszystkie pozostałe węzły,
* gwarantuje to synchronizację stanu danych
* oraz bardzo duży nakład obliczeniowy

Słaby model:
* dopuszczalne jest niejednolitość spójności danych w systemie
* stałość przyczynowo skutkowa, stałość w ramach jednej sesji
* daje to dużo większą elastyczność w tworzeniu systemu, pozwala na buforowanie i wysyłanie większych zapytań synchronizujących dane pomiędzy wierzchołkami systemu


## Omówić metody oraz typowe problemy w modelowaniu matematycznym dla problemów decyzyjnych i optymalizacyjnych

Modele i metody:
* liniowe - zmienne są ciągłe, ogr. liniowe, f celu liniowa
* całkowitoliczbowe i mieszane - zmienne są całkowite/liniowe, reszta j.w
* nieliniowe - metody gradientowe, quasi-newtonowskie, newtonowskie, genetyczne
* programowanie dynamiczne - podział problemu na podproblemy i rekurencyjne rozwiązanie - np. problem plecakowy
* grafowe/sieciowe - wykorzystanie grafu lub sieci do modelowania problemu

Typowe problemy:
* Złożoność problemu
* zbyt mała liczba danych/niedokładne dane
* wielowymiarowość
* nieliniowość/niewypukłość funkcji celu
* niedopuszczalność - nie istnieje x spełniający
* nieograniczoność problemu - f celu może maleć w nieskończoność


## Wyjaśnić główne zagadnienia modelowania matematycznego w systemach decyzyjnych z wykorzystaniem pojęć (nie)wypukłości i (nie)liniowości

Wypukłość:
* jak tak, to znalezione min lokalne jest jednocześnie min. globalnym
* np KKT wymaga, aby ograniczenia nierównościowe jak i funkcja celu były wypukłe
* jeżeli f celu nie jest wypukła, to problem robi się skomplikowany, ponieważ możemy utknąć w min. lokalnym - można wtedy np. użyć algorytmów ewolucyjnych

Liniowość:
* funkcja celu oraz ograniczenia są liniowe - wszystkie w pierwszych potęgach (A nie jakieś bzdury z dysku)
* jeżeli problem jest liniowy, to jest też wypukły
* problemy liniowe są najłatwiejszym typem modelowania, ale za to nie odzwierciedlają wszystkich możliwych zjawisk
* problemy nieliniowe wymagają dużo większego nakładu obliczeniowego, a ich rozwiązania mogą być obarczone większym błędem


## Na czym polega specyfika modelowania matematycznego układów cyber-fizycznych? Podać przykłady współpracy agentów w sieci i problemów w osiąganiu pożądanego zachowania układu.

Modelowanie matematyczne układów cyber-fizycznych:
* wiele zjawisk ma dyskretną liczbę modeli ciągłych
* mieszają się również zjawiska ciągłe fizyczne z dyskretnymi (np. sygnały sterujące)
* w modelach występuje duża niepewność oraz nieliniowość
* dynamiki ciągłe można modelować za pomocą równań różniczkowych
* spore wymagania czasu rzeczywistego

Rodzaje modeli:
* deskryptywne - odkrywają zależności między danymi pomiarowymi
* predykcyjne - przewidują stan systemu na podstawie pomiarów
* decyzyjne - wypluwają sterowania pchające system w pożądaną stronę

Np. autonomiczne poszukiwanie ludzi dronami - z jednej strony chcemy mieć minimalizację ryzyka i jak najsprawniejszy ruch, a z drugiej strony zjawiska losowe np. wiatr znacząco wpływa na trajektorię lotu


## Porównać podstawowe modele sieci złożonych. Jak odpowiadają one własnościom rzeczywistych sieci?

ER - połączenie między dwoma wierzchołkami = prawdopodobieństwo p:
* rozkład stopni wierzchołków to rozkład Poissona - nie pasuje do rzeczywistych
* średnia odległość wierzchołków to log(N) - zazwyczaj też nie
* brak hubów
* niska klasteryzacja - nie oddaje to rzeczywistych sieci

WS - tworzymy graf, gdzie każdy z wierzchołków ma taki sam stopień i losowo przekładamy krawędź do innego losowego wierzchołka - powstają w ten sposób skróty:
* rozkład stopni wykładniczy - nie oddaje to rzeczywistych sieci
* wysoka klasteryzacja
* brak hubów
* średnia odległość = ln N

BA - bierzemy mały graf, dodajemy wierzchołki i krawędzie im większy stopień wierzchołka:
* rozkład stopni wierzchołków to rozkład potęgowy
* krótka średnia ścieżka = ln ln N
* obecne huby
* niska klasteryzacja
* dobrze oddaje połączenia w internecie


## Porównać metody projekcji grafów dwudzielnych. Przedstawić ich użyteczność w grupowaniu dokumentów tekstowych.

Graf dwudzielny - da się wyodrębnić dwie grupy wierzchołków w grafie, że każdy wierzchołek z pierwszej ma dokładnie jedno połączenie z jakimś wierzchołkiem z drugiej

* Projekcja prosta - wierzchołki dolne łączone, jeśli mają wspólny wierzchołek górny
* ważona - znormalizowana względem liczby wierzchołków górnych
* Newmana - znormalizowana względem stopni wierzchołków górnych
* Jaccarda - w oparciu o współczynnik Jaccarda

W dokumentach tekstowych możemy grupować, jeżeli zrobimy graf dwudzielny teksty -> słowa kluczowe:
* projekcja na dokumenty na podstawie wspólnych słów kluczowych
* nieskierowana z wagami - wagi są liczone jako liczba wspólnych terminów
* skierowana - analiza kierunkowych relacji, np. cytowania

## Scharakteryzować problem segmentacji obrazu. Przedstawić podstawowe strategie i algorytmy segmentacji przy użyciu pomocą metod klasycznych oraz sieci neuronowych

Segmentacja obrazu - wyodrębnienie wspólnych obszarów na obrazie
* przez progowanie - wielowartościowa, w zależności czy piksel bądź grupa pikseli jest większa/ mniejsza od progu - problemy z zaszumionym obrazem
* obszarowa - rozrost obszarów - zaczynamy od punktów początkowych i dla każdego z punktu próbujemy znaleźć nierozpatrzonego sąsiada, który nie psuje nam jednorodności regionu
* dziel i łącz - odwrócona obszarowa - czyli rozpoczynamy od całego regionu - jeśli region nie jest jednorodny, to podziel go na 4 i połącz jednorodne części i rekurencja
* działy wody - rozpoznajemy minima lokalne jasności - źródła wody, woda rozlewa się wzdłuż możliwych obszarów, jeżeli woda styka się z różnych źródeł, to mamy granicę obszarów
* segmentacja przez klasyfikację - używamy np sieci splotowych, svmki, różnych cech typu jasność piksela, kolor, cechy tekstur


## Opisać problem detekcji obiektów w obrazach. Przedstawić podstawowe strategie i algorytmy detekcji przy użyciu metod klasycznych oraz sieci neuronowych. Jak skonstruować detektor obiektów dysponując istniejącym klasyfikatorem tych obiektów?

Detekcja obiektów - określenie pozycji danego obiektu

Podstawowe metody klasyczne:
* przesuwne okno klasyfikujące w każdej pozycji
* hog - wyciągamy gradienty w obrazie tworząc histogramy dla różnych komórek i próbujemy je sklasyfikować np przez SVM

Sieci neuronowe:
* Region CNN - generuje propozycje obszarów zainteresowania, a następnie w tych obszarach klasyfikuje
* Faster RCNN - szybsze RCNN, bo propozycje obszarów generuje sieć neuronowa
* Single Shot Detector - najpierw SSD generuje detekcje różnych rozmiarów obiektów w jednym przejściu na podstawie różnych głębokości sieci neuronowej
* YOLO - detekcja jednorazowo przechodzi przez sieć, dzieli obraz na siatkę i poszukuje obiektów w każdej komórce siatki

Można użyć okna przesuwnego i sprawdzać region po regionie albo np. użyć HOGa i deskryptory obiektów w postaci gradientów próbować sklasyfikować jako konkretne obiekty