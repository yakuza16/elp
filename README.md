# [Elektroniczny list przewozowy (ELP)](https://marcin-koduje.com/ "Elektroniczny list przewozowy (ELP)")

![](https://cdn2.iconfinder.com/data/icons/harry-potter-colour-collection/60/28_-_Harry_Potter_-_Colour_-_Hogwarts_Express-256.png)

## Aplikacja napisana we:

**VUE.js**   ![](https://cdn4.iconfinder.com/data/icons/logos-and-brands/512/367_Vuejs_logo-256.png)

------------
Aplikacja napisana w czystym VUE.js. Na codzień pracuję w firmie będącej operatorem intermodalnym, i do napisania tej aplikacji zmotywowała mnie wykonywana przeze mnie praca. Aplikację można wykorzystać w firmie spedycyjnej/logistycznej w której nadaje się pociągi do wygenerowania kodu XML który później zaczytujemy do systemu PKP Cargo Elektroniczny List Przewozowy i nadajemy w ten sposób pociąg.
Kod generujemy w ten sposób że:
1. Na początek uzupełniamy dane odbiorcy i nadawcy przesyłki. Po wpisaniu danych blokujemy je kłódką. W każdym momencie możemy zmienić dane.
2. Dodajemy wagony oraz kontenery. 
2.1 Wybieramy typ wagonu **(warto zaznaczyć, że każdy typ wagonu ma w sobie inne właściwości danego wagonu, tj. np ładowność lub tarę wagonu - dane te przypisane do każdego typu będą poprawnie zaczytane do wygenerowanego później kodu)**
2.2 Później wpisujemy numer wagonu - musi być 12 cyfr. Jest walidacja tego pola pod kątem długości wpisanych znaków. W każdym momencie możemy edytować numer wagonu lub go usunąć.
2.3 Następnie do wagonu przypisujemy kontener. Wybieramy jego rozmiar, wpisujemy nr kontenera. Wybieramy czy pusty czy ładowny. Jeśli kontener będzie ładowny to po dodaniu go, mamy obowiązek wpisać wagę towaru, oraz numery założonych plomb na kontenerze. Podobnie jak przy wagonach, tak też i przy kontenerach w zależności od tego jaki rozmiar kontenera wybierzemy, taka jego masa zostanie automatycznie zaczytana do wygenerowanego kodu XML. Jest również zaimplementowana walidacja wagi towaru, ponieważ jeśli wpiszemy masę powyżej 28ton, wtedy zostanie wyświetony wykrzynik informujący że coś jest nie tak. Nie implementowałem możliwości edycji nr kontenera, jest zaimplementowana natomiast możliwość usunięcia kontenera z wagonu.
3. Po uzupełnieniu wszystkich wagonów i znajdujących się na nich kontenerów, klikamy na niebieską ikonkę XML </> Code, po czym w polu textarea pojawi się kod XML.
4. Naciskamy zielony przycisk kopiowania lub klikamy lewym przyciskiem w pole textarea - cały kod XML zostanie automatycznie skopiowany do schowka.
5. Otwieramy notatnik i wklejamy wcześniej skopiowany kod XML. Plik zapisujemy z rozszerzeniem .xml
6. Zaczytujemy plik w systemie ELP https://e-serwis.pkp-cargo.eu/web/e-serwis/start i nadajemy pociag.
