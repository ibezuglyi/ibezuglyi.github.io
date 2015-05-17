---
layout: post
title: OneDayApp - czyli aplikacja w jeden dzień
---

#Pomysł#
Ostatnim czasem mam tak, że chce mi się spróbować rożnych technologii/bibliotek. Albo pojawia się pomysł na małą aplikację. Co gorzej, taki pomysł kręci mi się w głowie i nie odpuszcza, i wtedy stawiam sobie cel: Napisać appkę/prototyp lub udowodnić że się nie da. Nie mam na celu napisać w pełni działającą appkę, nie dbam specjalnie o jakość kodu. W tym #OneDayApp chodzi tylko o  działający prototyp.

###Ten weekend###
Bardzo mnie się spodobała nowa funkcja Resharpera 9.0 z wyszukiwaniem dostępnych akcji [https://www.jetbrains.com/resharper/whatsnew/#navigation](https://www.jetbrains.com/resharper/whatsnew/#navigation). Owy ficzer mamy w SublimeText po naciśnięciu Ctrl+Shift+P. A co z Visual Studio? Dlaczego jeszcze tam nie ma, pytam się grzecznie? No właśnie! Teraz jest. [https://github.com/ibezuglyi/TurboCommand](https://github.com/ibezuglyi/TurboCommand "TurboCommand"). Ale czekaj-czekaj, zanim pobierzesz powiedz sobie głosem wewnętrznym - "Proo-too-tyyp". Więc proszę nie oczekuj zachowanie Resharpera od appki napisanej w 4 godziny.

###Co ciekawe###
1. O kurcze, pamiętam WPF,
2. To jest moja pierwsza próba napisania pluginu do VS,
3. COM jest bardzo magiczny.

Jak można usprawnić plugin:

 1. zrozumieć czemu nie da się **czasem** uruchomić komendę COM?
 2. Napisać wątek, który asynchronicznie ładuje listę dostępnych komend.
 3. Zrefaktoryzować filtrowanie komend.


###Poprzedni weekend###
Weekend temu też miałem pomysł na appkę. Zadaniem appki było wyświetlenie statystyk NDepend'a. Jakoś nie jestem przekonany do danych statystycznych w postaci tekstu. Więc tak, dostajemy tekst z [NDepend](http://www.ndepend.com/)'a, parsujemy, zapisujemy  do [https://www.firebase.com/](https://www.firebase.com/), odświeżamy wykres w [D3](http://d3js.org/). Mam prototyp: [https://github.com/ibezuglyi/Ndependent.Stats](https://github.com/ibezuglyi/Ndependent.Stats)

###Co ciekawe###
1. D3 - jest fajna biblioteka,
2. Przechowywać dane w chmurze Firebase też się da,
3. ReactJS - jest też fajny, zaczynam go lubić.


###Kolejne pomysły:
Trochę jeszcze mam pomysłów, oby z czasem było dobrze.  
