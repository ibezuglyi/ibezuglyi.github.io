---
layout: post
title: Nazewnictwo metod i zmiennych
---
### Z nazewnictwem zawsze jest problem
Powiedzmy sobie szczerze: z nazewnictwem zawsze jest problem. Czasami jest problem z samym uświadominiem tego faktu. Młodzi studenci swobodnie mogą pozwolić sobie nazwać metodę `Data()` i !UWAGA! nie zawsze to będzie zła nazwa. Ponieważ celem projektu studenckiego jest *zaliczenie* i metoda Data(), pobierająca zawartość pliku z systemu plików, tak samo dobrze pozwala osiąnąć ten cel, jak i metoda `GetFileContent()`. Najgorzej kiedy młody programista przyzwyczaja się do takiego podejścia i w kodzie produkcyjnym widzimy już dwie metody Data(): jedna do pobierania danych, druga do zapisywania. 

Prawdę mowiąc, jest jeszcze jeden przypadek, kiedy nazewnictwo nie jest aż tak ważne. W srodowisku startup-owym uważa się, że działający kod jest lepszym od tego, który ma przemyślaną architekturę, skalowalność, dobre nazewnictwo, ale .... nie działa. Ostatnio to doświadczyłem, uczestnicząc przy tworzeniu małej aplikacji w ramach Lean Pokera. Zdecydowanie zgadzam sie, że MVP ma nieco inne cele, niż produkt, tworzony, powiedzmy, dla banku inwestycyjnego. Ale nie sprzedajemy prototypów?      

Mówiąc, że z nazewnictwem jest zawsze jest problem, mam na myśli: zawsze i każdy to ma. Jeśli macie takie same problemy czasami jak ja, związane z odnajdywaniem metody, która powstała wczoraj albo dziś po porannej kawie, to tym bardziej musićie to przeczytać.     

### Szum w nazwach
Mały disclaimer: klasa musi być rzeczownikiem, metoda - czasownikiem. Jestem zwolennikiem powiedzenia, że kod ma się czytać jak dobrze napisany poemat. Jeśli coś mi nie brzmi fajnie, to napewno będą to klasy typu: `public class GetCustomer{}`, `public class MapCompanyToDto{}`. Jeśli nie podzielacie tego zdania, to proszę zamknijcie zakładkę i nie marnujcie sobie czasu.   

Nie zdajemy sobie sprawę czasami o ile nazewnictwo zmiennych i metod jest ważne. Jeśli by w projekcie komercyjnym zapytano mnie: co jest ważnejsze wydajność algorytmów czy dobre nazewnictwo, to bez wątpienia to byłoby dobre nazewnictwo. Ostatnimi czasami uważam, że sukces aplikacji od strony technicznej zapewnią w dużej mierze tylko dwie rzeczy - dobre nazewnictwo i zachowanie SRP w całym projekcie. Ale nigdy nie ma czasu tak banalne rzeczy jak nadawanie dobrych nazw, i to nie dlatego że goni nas biznes albo manager, a dlatego, że no przecież nie będziemy pisać długiej nazwy, bo algorytm również fajnie dzała z metodą `foo1(id)` i `GetCustomerById(id)`. 

Na pewno nie raz spotkaliście się z nazwami klas, które miały słowa `Manager`, `Service`, `Dispatcher`, `Data`, `Item`. Nic nie mam przeciw temu, żeby używać tych nazw w klasach, które naprawdę czymś zarządzają, czy udostepniają nam jakąś usługę, czy reprezentują jakieś dane, czt tez pojedynczy obiekt z kolekcji czegoś tam naprawdę ważnego. Problem tutaj często powstaje, kiedy `Manager` robi za dużo, kiedy `Service` robi za dużo, i kiedy `Data` ze swoim kolegą `Item`em reprezentują wszystko co tylko się da. Tutaj często ma się do czynienia z nadużyciem ogólnych nazw. Nazwa klasy/metody/zmiennej zawierająca słowo `Data` dla mnie jest potencjalnym problemem. Nie mówię o tym że słowo `Data` w j. angielskim jest liczbą mnogą i po metodzie `GetData` raczej bym się spodziewał kolekcji jakiś elementów, ale przede wszystkim widziałem takie cuda:

`customerService.GetCustomer()` i
`customerService.GetCustomerData()` 

I od razu wszystko jasne: jedna metoda zwraca customera, a druga jego dane. Autor nie wpadł na pomysł, że `customer` jest tez jakąś formą danych. Odkryję wam tajemnicę komercyjną po raz pierwszy w życiu: tak naprawdę pierwsza metoda zwracała encję, a druga metoda obiekt DTO, w którym była .... ta sama encja.

Jeśli widzę gdzieś słowo `Data` to pierwsze co robię - spodziewam się, że gdzieś tutaj zaraz będzie załamana zasada SRP. A ja do tego będę świadkiem tego przestępstwa, o nie... Z reguły tak jest, to kusi, przyznam się szczerze. `Data` jest słowem bardzo abstrakcyjnym, i do niego pasuje wszystko, kolekcję? - tak. encje? - tak, DTO? - tak! dane do generowania raportów i wykresów - tak, tak!

**Peirwsza reguła na dziś**: nazwij metodę/klasę/zmienną na tyle dokładnie na ile to się tylko da w tym zasięgu. Popatrz na swój kodzik przed komitem i zapytaj siebie, czy można doszczegółowić nazwę? Jeśli odpowiedź będzie tak - to zrób to natychmiast. Powtarzaj to w pętli dla każdej linijki kodu do pory, aż stwierdzisz, że wymyślić jeszcze bardziej dokładnej nawzy nie da się w tym zasięgu.   

### Widocznosc metod i generyczność
Już słyszę, jak ktoś mówi: "No a czemu w `clientRepository` nie mogę mieć metody `Remove()` albo `Get()`. No otóż dlatego, że złamiesz moją pierwszą regułę tego postu. Na jednej sesji z refaktoringu padł następujący pomysł, cytat: 

*Umówmy się, że w repozytorium będziemy mieć metody typu `Get()` i `Remove()`, które będą odpowiedzialne za pobieranie/usuwanie encji tego konkrentego repozytorium.*

Uważam, że konstrukcja *Umówmy się* jest zła. A jak umówimy się z developerem, który jest na urlopie? Autor *umówienia się* za tydzień idzie na urlop.. Dlaczego w kodzie mam pamiętać o rzeczach, o których umówilismy się 3/6/9 miesięcy temu? dlaczego kod nie mówi wprost co robi i jak, po co mam cokolwiek pamiętać, jeśli to nazwa metody może mi powiedzieć wprost. Uważam, że metoda `clientRepository.GetClientById(clientId)` jest cudowna, fajnie się czyta, ale co ważnejsze - rewelacyjnie ją zrozumie nawet kolega z innego projektu, który nie programuje w C#. Czy przypadkiem nie o to nam chodzi??? Co redundacja słowa `client`? W takim kodzie wolę redundancję niż zagadki. 

No to co z generycznymi klasami? Odpowiedź: zastosuj pierwszą regułę tego postu: *nazwij metodę/klasę/zmienną na tyle dokładnie na ile to się tylko da w tym zasięgu*. Definicja klasy generycznej musi być dość abstrakcyjna, taki przecież ma cel klasa generyczna. Definicja klasy abstrakcyjnej jest też dość abstrakcyjną, musi taką być po prostu. Jeśli generyczny repozytorium będzie miał metodę `Remove()` albo `Get()` - to nie mam absolutnie nic przeciw, ponieważ zakres działania klasy abstrakcyjnej/generycznej jest duży i ma dużą odpowiedziałność - to nie jestem w stanie doszczegółowić co robi metoda `Remove` pochodząca z klasy generycznej/abstrakcyjnej, bo `public class ClientRepository : BaseRepository<Client>` który dzieziczy po `BaseRepository` zamierza usuwać obiekt typu `client` w metodzie `Remove()`, a klasa `public class ProductRepository : BaseRepository<Product>` raczej będzie usuwała produkty. Skoro nie jestem w stanie bardziej doszczegółowić co robi metoda, to uważam, że nazwa jest wystarczająca dobra. Z reguły w generycznym repozytorium oczekuję krótkich nazw...      

Mam czasami bardzo różne spostrzeżenia z życia, które czasami idealnie się przekładają na programowanie. Przypomnijcie sobie, jak nazywają się stanowiska w waszych firmach. Dyrektor pionu ds sprzątania 2 piętra, Junior Software Developer, Senior Architekt, Program Manager, Director, Head, CTO, CEO. Im wyższe stanowisko - tym krótsza nazwa. Im większa odpowiedziałność - tym krótsza nazwa. Im większy zasięg działań - tym krótsza nazwa. Moim zdaniem to jest idealne odzwierciedlenie ważności nazw.

### Jeśli miałbyś szukać tej metody/klasy, to co wpisałbyś do pola wyszukiwania w smoim IDE
Znowu przykład z życia. Zdarzyło mi się jakoś wymienić bezpieczniki w rozdzielni. Byłem wtedy w trakcie przeprowadzki i dużo rzeczy miałem spakowane w kartonikach. Nie sposób było cokolwiek znaleźć, jeśli to nie leżało gdzieś na wierzchu. Spędziłem około 20 minut szukając bezpieczników. Kto widział, ten wie, że są to małe urządzenia elektryczne krótsze niz mój palec. Znalazłem je, ale postanowiłem, że tym razem **pomogę sobie przyszłemu** i nowe bezpieczniki zostawię w tym miejscu gdzie będę je szukać najpierw. Otóż krótkie pytanie do siebie, gdzie je szukałem, jak były bardzo potrzebne? Od czego zacząłem szukanie? W jakiej szafie? w jakiej szufladzie? I tam zostawiłem, sprawdziło mi się. Kolega z bloku obók potrzebował bezpieczniki, a ja miałem zapasowe dokładnie w tym miejscu gdzie zostawiłem ostatnio. Nie zapamiętywałem tego miejsca specjalnie. Jak miałem szukać drugi raz to zacząłem je szukać ... !UWAGA! w tym samym miejscu, i znalazłem po 5 sekundach! Nakładu pracy CPU - zero, RAM - zero, CZAS - 5 sekund, zlożonośc obliczeniowa - O(1), należy tylko zastanowić co robisz i po co?

Z nazewnictwem jest dokładnie tak samo. Jeśli zastanawicie się na wyborem dobrej nazwy dla zeminnej/klasy/metody, to zapytajcie siebie, cobyście wpisali do pola wyszukiwarki gdybyście chcieli znaleźć istniejącą metodę o takiej funkcjonalności. 

**Druga reguła na dziś**: Przed komitem zamknij wszystkie pliki, idź na kawę/sok/wodę, i po powrocie w polu wyszukiwarki wpisz nazwę metody, którą chcesz wkomitować i jeśli znajdziesz ją w pierwszej linijce wyników wyszukiwania, to nazwa raczej jest ok. Komituj. Właśnie pomogłeś sobie przyszłemu.  

### Refleksja i znowu z życia
Bardzo dużo z żoną zastanawialismy jakie imię dać synku. Imię miało spełnić całą masę kryteriów moich i żony, a co najważniejsze musiało podobać się mnie i żonie. Po kilku miesiącach ciężkich zastanowień w końcu doszliśmy do porozumienia i wybralismy jedno imię. Po tym czasie chyba przemyślałem swoje podejście do nazewnictwa czegokolwiek, trzeba nazywać rzeczy po imieniu, mowi się tak, ja z kolei mówię: jak nazwiesz łódź, tak będzie płynąć. 

Powtórzę złote reguły nazewnictwa:

1. Nazwij metodę/klasę/zmienną na tyle dokładnie na ile to się tylko da w tym zasięgu.

2. Przed komitem zamknij wszystkie pliki, idź na kawę/sok/wodę, i po powrocie w polu wyszukiwarki swego IDE wpisz nazwę metody, którą chcesz wkomitować i jeśli znajdziesz ją w pierwszej linijce wyników wyszukiwania, to nazwa raczej jest ok. Komituj. Właśnie pomogłeś sobie przyszłemu.
