<style scoped>
 ol ol {
     margin-left: 20px;
 }
 p {
     margin: 20px 0;
     font-weight: bold;
     font-size: 16px;
 }
</style>

<template>
<div class="main">
    VUE - przykładowa aplikacja

    1. stworzenie projektu firebase, konfiguracja z vue cli, pobranie danych i wyświetlenie (~1h)<br>
    1. założenie projektu w firebase<br>
    2. import danych z json do firebase<br>
    3. zaciągnięcie czystego projektu (przygotowanego wcześniej w git)<br>
    4. import configu do projektu<br>
    5. nawiązanie połączenia z bazą<br>
    6. wyświetlanie pobieranych danych<br>
    2. Stworzenie komponentu głównego i ewentualnych komponentów dodatkowych, które wyświetlą dane (produkty + atrybuty + przyciski funkcyjne) oraz
    umożliwią funkcjonalności:<br>
    - dodawanie do koszyka<br>
    - dodawanie do wishlisty<br>
    - ukrywanie produktu (x)<br>
    Celem zadania nie jest sprawdzenie poprawnego "cięcia", ale należy przygotować strukture html oraz style, które w miare nadadzą wygląd całej<br>
    aplikacji (np dodaj do koszyka to czerwony button, dodaj do wishlisty do niebieski przycisk itd)
    <br><br><br>
    Informacje dodatkowe:<br>
    - celem zadania nie jest vuetify dlatego w zadaniu głównym nr 2 nie używamy komponentów vuetify (np do przycisków itd),<br>
    - dane do firebase znajduja się w folderze static (plik json)<br>
    - obrazki produktów znajdują się w folderze static/products<br>
    - struktura atrybutów jest nieco skomplikowana w data.json dlatego poniżej objaśnienie:<br>
    - attributes to główna "tabela" z dostepnymi atrybutami produktów (id,nazwa,typ)<br>
    - typ oznacza czy atrybut moze posiadac wartość pojedyńczą czy wielokrotną (tzn np produkt moze mieć jeden kraj pochodzenia, ale jeżeli
    chodzi o użyty chmiel to może mieć więcej niż jedną wartość)<br>
    - attributesIdValue to "tabela" która zawiera możliwe opcje dla danych atrybutów (gdzie pozycja w tablicy odpowiada id atrybutu z attributes, a
    wartosc czyli string to możliwe wartości dla tego atrybutu oddzielone znakiem |)<br>
    - każdy produkt posiada "attributes" które jest obiektem i sklada sie z par klucz - wartość gdzie klucz to id atrybutu a wartość to
    string idików wartości danego atrybutu oddzielone znakiem |


</div>
</template>
