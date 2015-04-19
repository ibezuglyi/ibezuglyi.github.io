---
layout: post
title: Automatyzuj to i nie bądź pracowitym programistą
---

Często w pracy używam terminu "pracowity programista". To jest taki programista, ktory pisze długie metody, unika pętel, pisze komentarzy, a co więcej - utrzymuje te komentarze w kodzie czyli zmienia ich wraz ze zmianą kodu. Trafiają się róźni programiści - bardziej lub mniej pracowici. Ale to nie jest kompliment. Wbrew odwrotnie.

**Problem**
Jednego dnia w moim projekcie postanowiono, że wszelkie zmiany dokonane w plikach zasobów *.resx* wysyłać dodatkowo do TeamLead'a mailem. Nie będę teraz krytykował takiego podejscia, nie o to chodzi. Po kilku skończonych przeze mnie taskach okazało się, że zapominam to robić. Pracowity i sumienny programista nigdy by nie zapominał.

**Idea**
Chcę aby ktoś(lub coś) sam sledził moich zmian lokalnie w moim repo w plikach *.resx* i powiadamiał mnie o tym w stylu: "Hej, masz zmiany w plikach *.resx* nie zapomnij wysłać maiala do TL, treść maila masz tu."

**Rozwiązanie**
Pierwsze co przyszło mi do głowy to mechanizm hook'ow w git.
Skrypt jest uruchamiany przed każdym commit'em. Dla wszystkich plikow typu *.resx* robię *git diff* i rezultat porowania zapisuję do pliku diff.diff.

<script src="https://gist.github.com/ibezuglyi/baeff2bb71a2b631cdc1.js"></script>

Teraz w moim repo podczas zmian plików będę widzial plik diff.diff, ktory bedzie zawieral wszystkie zmiany plików zasobów. Moim zadaniem jest wysłac ten plik do TL'a.

**Rozwiązanie ++**
Lepszym rozwiazaniem byłoby wysyłanie tego pliku po każdym commicie do TL. Nad tym już pracuję.

**Wnioski**
1. Wrescie pobawilem sie w hooki git'a.
2. Bash jest fajny, ale chętnie uderzy Ci po rękach za brakujące/zbędne spacje.
3. Mam o jeden sposob więcej na to, żeby nie być pracowitym programistą. 
