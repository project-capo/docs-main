Sterowniki
==========

Poniżej znajdziemy opis korzystania z sterowników oraz możliwości ich dalszego rozszerzania.

Sterownik jest:

* aplikacją uruchamianą na robocie
* komunikującą się z urządzeniem podłączonym do robota, na przykład
 * silnikami
 * laserowym dalmierzem
 * czujnikiem ruchu
* komunikującą się z mediatorem

Sterownik odpowiada za:

* ustawienie parametrów urządzenia
* współbieżny dostęp do urządzenia przez wiele klientów
* obserwowanie obecności klientów
* wysyłanie wiadomości dla klientów, którzy zarejestrowali się jako nasłuchujący
* odbieranie komunikatów, ich obsługę i odsyłanie wiadomości, jeśli to konieczne

Komunikacja
-----------

Sterownik komunikuje się z mediatorem przy pomocy potoków. Są to potoki standardowego wyjścia i wejścia. Wymagane jest, by sterownik na standardowym wejściu oczekiwał na dane, a na standardowe wyjście umieszczał dane.

Format komunikacji z mediatorem jest następująca:

* 2 bajty długości nagłówka wiadomości
* nagłówek wiadomości o zadanej długości
* 2 bajty długości wiadomości
* wiadomość o zadanej długości

Wartość długości powinna być przesyłana w porządku ``big-endian``, zgodna z sieciowymi warunkami przesyłania danych. Należy zwrócić uwagę na to, czyli wartości są ``singed`` czy ``unsigned``. Ze względu na wykorzystywanie Java, przyjmuje się, że wartości bajtów są ``signed``.

Nagłówek oraz wiadomość są binarnymi ciągami znaków. Należy zwrócić uwagę na sposób komunikacji z mediatorem poprzez potoki. W przypadku używania języka python, należy ustawić działanie interpretera na binarne obsługiwanie wejścia i wyjścia. Możliwe jest to dzięki opcji ``-u``.

Do serializacji i deserializacji wykorzystywane jest Google Protobuf. Wymagane jest, by co najmniej nagłówek był zgodny z przyjętym w mediatorze. Wiadomości przesyłane przez mediator nie są sprawdzane i może to być dowolny ciąg znaków. Zaleca się, by to było zgodne z protobuf i postacią wiadomości przyjętą w mediatorze.

 Aktualna postać nagłówka i podstawowej wiadomości dostępna jest `dev-amber/amber-common/drivermsg.proto`_.

 .. _dev-amber/amber-common/drivermsg.proto: https://github.com/dev-amber/amber-common/blob/master/proto/drivermsg.proto