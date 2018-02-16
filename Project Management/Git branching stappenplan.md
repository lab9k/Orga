# Stappenplan werken met GitHub

**Belangrijk: Gelieve NIET rechtstreeks op de Master branch te committen! Volg onderstaand stappenplan!**

Gezien we werken met branches is het belangrijk dat iedereen hetzelfde stramien volgt. 

## Basismethode

De basismethode gaat als volgt:

Het is altijd een goed idee om te beginnen met de laatste versie van de master:
  ```bash
  git pull
  ```

Maak daarna een nieuwe branch aan voor de feature waar je aan werkt. Probeer een duidelijke naamgeving te hanteren: `taak/feature` is een goed begin. (voorbeeld: `ldap/toevoegen-gebruikers`)
  ```bash
  git checkout -b taak/feature
  ```

Nu kan je gewoon normaal comitten op deze branch:
  ```bash
  git add .
  git commit -m "Commit message"
  ```

Probeer ook altijd een duidelijke commit message te gebruiken. Dingen als "*toevoegingen*" of "*stuff*" zijn nutteloos. 
Probeer te omschrijven wat de wijzigingen in de commit juist doet.

Andere mensen uit je team kunnen ook meewerken op deze branch. Om een bestaande branch van GitHub op te halen gebruik je volgende commando's:
  ```bash
  git checkout -b taak/feature
  git pull origin taak/feature
  ```

Vergeet niet om je commits regelmatig naar GitHub te pushen:
  ```bash
  git push origin taak/feature
  ```

Eens je feature klaar is kan je een pull request aanmaken om de code in de `master` branch te krijgen. 

**Opgelet: maak enkel voor werkende code een pull request!** 

Zolang je code niet werkt, werk je verder op je eigen branch, zodat de andere teams er geen invloed van ondervinden. Wanneer je onlangs gecommit hebt zal GitHub je vragen of je een pull request wil maken. Dit dien je dus pas te doen als je feature klaar is. 

Stel dat je per ongeluk een branch lokaal aanmaakt maar eigenlijk wou verbinden met een reeds bestaande branch, kan je deze als volgt aan koppelen:
  ```bash
  git branch --set-upstream-to-origin/<remote branch> <lokale branch>
  ```

## Samenvatting

- Wees steeds **duidelijk** en **specifiek** genoeg in de naam bij het aanmaken van een branch!
- Een branch wordt aangemaakt **per feature** die je wenst te pushen naar de master-branch (implementatie en incrementeel werken). Dus niet gewoon een branch maken per persoon of per subgroep! Dit maakt het ingewikkeld om alles correct te mergen.
- Alvorens je een branch wenst aan te maken en/of te pushen door een pull request te doen, **eerst steeds een pull** van de upstream doen !
- **Elke branch wordt verwijderd nadat de request werd goedgekeurd en de betreffende branch werd gemerged!**
