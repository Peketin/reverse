Reverse Utility
Kuvaus

Tämä projekti sisältää C-kielellä toteutetun komentoriviohjelman nimeltä reverse.

Ohjelman tarkoituksena on lukea tekstiä joko standardisyötteestä tai tiedostosta ja tulostaa rivit käänteisessä järjestyksessä. Ohjelma tukee myös tulosteen kirjoittamista erilliseen tiedostoon.

Ohjelma voidaan suorittaa kolmella tavalla:

./reverse
./reverse input.txt
./reverse input.txt output.txt
Toiminnallisuus

Ohjelma lukee syötteen rivi kerrallaan ja tallentaa rivit dynaamiseen taulukkoon. Koska rivien määrää tai yksittäisen rivin pituutta ei tiedetä etukäteen, ohjelma käyttää dynaamista muistinhallintaa.

Kun kaikki rivit on luettu, ohjelma tulostaa ne lopusta alkuun, jolloin syötteen rivijärjestys kääntyy.

Esimerkiksi syöte:

hello
this
is
a file

tuottaa tulosteen:

a file
is
this
hello
Kääntäminen

Ohjelman voi kääntää GCC-kääntäjällä seuraavasti:

gcc -std=c99 -Wall -Wextra -o reverse reverse.c

Tämän jälkeen syntyy suoritettava ohjelma nimeltä reverse.

Suorittaminen
1. Lukeminen standardisyötteestä
./reverse

Tämän jälkeen käyttäjä voi kirjoittaa rivejä käsin. Syötteen lopettamiseen käytetään Linuxissa näppäinyhdistelmää:

Ctrl + D
2. Lukeminen tiedostosta ja tulostus ruudulle
./reverse input.txt

Ohjelma lukee tiedoston input.txt sisällön ja tulostaa rivit ruudulle käänteisessä järjestyksessä.

3. Lukeminen tiedostosta ja tulostus toiseen tiedostoon
./reverse input.txt output.txt

Ohjelma lukee tiedoston input.txt ja kirjoittaa käännetyn tulosteen tiedostoon output.txt.

Virheenkäsittely

Ohjelma käsittelee seuraavat virhetilanteet:

Liian monta komentoriviargumenttia

Jos ohjelmalle annetaan liian monta argumenttia, ohjelma tulostaa:

usage: reverse <input> <output>

ja päättyy virhekoodilla 1.

Syöte- ja tulostiedosto ovat samat

Jos käyttäjä antaa saman tiedoston sekä syötteeksi että tulosteeksi, ohjelma tulostaa:

Input and output file must differ

ja päättyy virhekoodilla 1.

Tämä estää tilanteen, jossa tulostiedoston avaaminen tyhjentäisi alkuperäisen syötetiedoston ennen sen lukemista.

Tiedoston avaaminen epäonnistuu

Jos syöte- tai tulostiedostoa ei voida avata, ohjelma tulostaa esimerkiksi:

error: cannot open file 'input.txt'

ja päättyy virhekoodilla 1.

Muistin varaaminen epäonnistuu

Jos muistin varaaminen epäonnistuu, ohjelma tulostaa:

malloc failed

ja päättyy virhekoodilla 1.

Toteutuksen rakenne

Ohjelma koostuu seuraavista pääosista:

komentoriviargumenttien tarkistus
syöte- ja tulostiedostojen avaaminen
syöte- ja tulostiedoston vertailu
rivien lukeminen getline()-funktiolla
rivien tallentaminen dynaamiseen taulukkoon
rivien tulostaminen käänteisessä järjestyksessä
muistin vapauttaminen
tiedostojen sulkeminen
Käytetyt tärkeimmät C-funktiot

Ohjelmassa käytetään muun muassa seuraavia funktioita:

fopen()
getline()
fprintf()
realloc()
free()
fclose()
exit()
stat()
strcmp()
Muistinhallinta

Jokainen getline()-funktion lukema rivi tallennetaan dynaamiseen taulukkoon. Jos taulukon kapasiteetti loppuu, sitä kasvatetaan realloc()-funktiolla.

Lopuksi kaikki varattu muisti vapautetaan free()-funktiolla.

Testaus

Ohjelmaa voi testata esimerkiksi seuraavasti:

echo -e "hello\nthis\nis\na file" > input.txt
./reverse input.txt

Odotettu tuloste:

a file
is
this
hello

Tulostiedoston testaus:

./reverse input.txt output.txt
cat output.txt

Virhetilanteen testaus:

./reverse input.txt input.txt

Odotettu virheilmoitus:

Input and output file must differ
