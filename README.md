# SeedSigner Crosscheck (v1.1.4)

Een offline HTML-tool om de resultaten van je SeedSigner onafhankelijk te controleren (crosschecken): seed phrase (12/24 woorden), master fingerprint, xpubs en ontvangstadressen — voor zowel single-sig (BIP-84) als multisig (BIP-48), met keuze van het accountnummer.

## Waarom deze tool?

Ik heb de code van @M21 geforkt en aangepast zodat je de SeedSigner-software **gemakkelijker kunt crosschecken**.

> **Cruciaal:** download de SeedSigner-software op een **ander apparaat** dan het apparaat dat je voor deze crosscheck gebruikt.

**"Waarom is dit nog nodig als de GPG-keys al geverifieerd zijn?"**
Een geldige GPG-handtekening bewijst alleen dat het bestand dat je downloadde echt van de ontwikkelaars komt. Ze beschermt je niet tegen het apparaat waarop je dat doet. Staat er malware op je computer, dan kan die nog steeds heel wat manipuleren, zoals:

- de **12 (of 24) woorden** van je seed phrase;
- de **private keys**;
- de **xpubs**;
- de **ontvangstadressen**.

Door de SeedSigner-software op het ene apparaat te downloaden en de resultaten op een **tweede, onafhankelijk apparaat** met deze tool te controleren, moet een aanvaller beide apparaten tegelijk gecompromitteerd hebben om je te misleiden. Komen de resultaten van beide apparaten exact overeen, dan heb je veel meer zekerheid.

## Wat zit er in deze repository?

| Bestand | Uitleg |
|---|---|
| `test-2single-sig-en-multisig-met-fingerprint-accountnummers-v1.1.4.html` | De tool zelf: één zelfstandig HTML-bestand, zonder externe verzoeken (strikte Content-Security-Policy). |
| `test-2single-sig-en-multisig-met-fingerprint-accountnummers-v1.1.4.html.sig` | De GPG-handtekening van het HTML-bestand. Beide bestanden horen samen. |

## Functies

- Hex-/dobbelsteen-entropie zoals SeedSigner (50 tekens → 12 woorden, 99 tekens → 24 woorden, via SHA-256), of 32/64 tekens als directe BIP39-entropie
- BIP-84 single-sig en BIP-48 multisig preview, met master fingerprint
- Keuze van het accountnummer (standaard account 0)
- Nederlands/Engels, volledig offline
- Zelftest die bij een fout alles blokkeert (fail closed)

## Downloaden en verifiëren

1. Download **beide** bestanden (`.html` en `.html.sig`) via de knop **Code → Download ZIP** of via [Releases](../../releases).
2. Controleer de GPG-handtekening:

   ```bash
   gpg --verify test-2single-sig-en-multisig-met-fingerprint-accountnummers-v1.1.4.html.sig \
                test-2single-sig-en-multisig-met-fingerprint-accountnummers-v1.1.4.html
   ```

   De handtekening is gemaakt met de sleutel met fingerprint:

   ```
   CE1F B111 C2B5 FECC 91C3  6F11 C464 F440 9ED9 FEF2
   ```

   Je moet deze publieke sleutel eerst importeren (`gpg --import`) en de fingerprint via een onafhankelijk kanaal controleren.

3. Optioneel: controleer de SHA-256-hash:

   ```bash
   sha256sum test-2single-sig-en-multisig-met-fingerprint-accountnummers-v1.1.4.html
   # d5427add0af0c7e580de7a2d7330ce191d51ce8ac4a95aea18a0d006b35eb45b
   ```

## Veilig gebruiken

1. Download de SeedSigner-software op **apparaat A**.
2. Download en verifieer deze tool op **apparaat B** (een ander apparaat).
3. Koppel apparaat B **los van het internet** voordat je het HTML-bestand opent.
4. Open het bestand in een browser en vergelijk woorden, fingerprint, xpubs en adressen met wat je SeedSigner toont.
5. Sluit het tabblad na gebruik en gebruik voor echte fondsen bij voorkeur een apparaat dat nooit meer online komt (of een live-USB).

## Disclaimer

Gebruik op eigen risico. Deze tool is bedoeld als extra controle, niet als vervanging van goede operationele beveiliging. Test altijd eerst met een kleine hoeveelheid of met een testseed voordat je er echte fondsen aan toevertrouwt.
