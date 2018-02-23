# Stappenplan werken met GitHub

* Inhoud
  * Basismethode om een pull request in te dienen
  * Een Git Push ongedaan maken
    * D.m.v. een ID en een branch-naam
    * D.m.v. HEAD~[commit_waar_je_naar_wilt_teruggaan]
  * De laatste Git Push ongedaan maken
  * Samenvatting
  

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

## Een Git Push ongedaan maken

Note: Het is belangrijk dat nog geen enkele andere user jouw veranderingen reeds gepulld heeft !

```
git push -f origin last_known_good_commit:branch_name
```

* **last_known_good_commit**: Het ID van de commit waarnaar je terug wilt gaan (Dit ID kan je vinden onder 'commits' in de betreffende repository) 
* **branch_name**: in de meeste gevallen zal dit gewoon 'master' zijn.

Onderstaand commando kan je gebruiken indien je terug wenst te gaan naar de **vierde** laatste commit en een nieuwe commit wilt maken met de aanpassingen:

```
git revert HEAD~3
```


## De laatste Git Push ongedaan maken

Note: Het **HEAD** keyword is zeer belangrijk! Indien je dit niet gebruikt zal de gehele publieke commit geschiedenis gewist worden binnen de betreffende repository !

```
git reset --hard HEAD
```
of:
```
git revert HEAD
git commit -m 'restoring the file I removed by accident'
```

## Samenvatting

- Wees steeds **duidelijk** en **specifiek** genoeg in de naam bij het aanmaken van een branch!
- Een branch wordt aangemaakt **per feature** die je wenst te pushen naar de master-branch (implementatie en incrementeel werken). Dus niet gewoon een branch maken per persoon of per subgroep! Dit maakt het ingewikkeld om alles correct te mergen.
- Alvorens je een branch wenst aan te maken en/of te pushen door een pull request te doen, **eerst steeds een pull** van de upstream doen !
- **Elke branch wordt verwijderd nadat de request werd goedgekeurd en de betreffende branch werd gemerged!**
