### Proof Of Concept: CI Travis (20/02/2018)
+
+- [OpenShift Deployment with GitHub](https://docs.travis-ci.com/user/deployment/openshift/)
+- [Travis CI Quickstart](https://hub.openshift.com/quickstarts/26-travis-ci)
+
+* Jenkins -> te veel werk om te implementeren & overkill (de schaalbaarheid is te groot voor de Lab9K-projecten = weinig profijt).
+* Travis lijkt wel een goede tool te zijn om op het niveau van de projecten binnen Lab9K op een continu integrerende manier te werken.
+    * **Travis = een tool die tussen GitHub en OpenShift functioneert: bijvoorbeeld aanpassingen aan de Master branch op de betreffende GitHub repository triggeren een automatische built op OpenShift.** 
+    * Travis dient gelinkt te worden aan de betreffende GitHub repository.
+    * de `.travis.yml` file dient zodanig geconfigureerd te worden dat iedereen toegang / de juiste authorization heeft tot het gemeenschappelijke project -> application.
+    * Voor elk projectlid kan dit d.m.v. het `travis setup openshift` commando.
+    * Zo weinig mogelijk terug van scratch beginnen (zie bottleneck Skosmos).
+
+* Handig om deze tool toe te passen binnen het Score project dat binnenkort gelaunchd zal worden (?)
+    * Gebruiksvriendelijk
+    * Snelle integratie
+    * Beperkingen opleggen is mogelijk
+    * Ideaal voor de omvang van het Score project
+
+* **Bottleneck Skosmos:**
+    * Momenteel werken degene, die met het [Skosmos](https://github.com/lab9k/Skos) project bezig zijn, niet echt opbouwend (niet continu met dezelfde application) en wordt er vaak terug van scratch begonnen (new app) . Hierdoor dient Travis steeds opnieuw geconfigureerd & gelinkt te worden aan deze nieuwe application. (zie bovenstaande documentatie)
