## Aanpassingen Dinsdag 7 Augustus

> De redirects in de Documentation pagina werkten niet omdat Swagger UI deze onderschepte en een fout opwerpt.
> Daarom heb ik de redirects in javascript gezet.

-   De ID tag toevoegen aan elke knop
-   De javascript functie onclick aanmaken voor elke link

### File: partial/submenu

```html
...
<a class="nav-link" href="{{ urls.applications }}" id="applicationsbutton">{{ urls.applications.title }}</a>
...
<a class="nav-link" id="statisticsbutton" href="{{ urls.stats }}">Statistics</a>
...
<a class="nav-link" class="nav-item" id="docsbutton" {% if urls.docs.active? %}active{% endif %} href="https://developerdv.gent.be/docs/">Documentation</a>
...
<a class="nav-link" href="{{ urls.messages_inbox }}" id="messagesbutton">
...
<a class="nav-link" href="{{ urls.account_overview }}" id="settingsbutton">
...
<a class="nav-link" href="https://developerdv.gent.be/docs/" id="docsbutton">Documentation</a>
...

<script type="text/javascript">
    (function () {

        document.getElementById("docsbutton").onclick = function () {
            location.href = "https://developerdv.gent.be/docs/";
        };

        document.getElementById("statisticsbutton").onclick = function () {
            location.href = "https://developerdv.gent.be/buyer/stats";
        };

        document.getElementById("messagesbutton").onclick = function () {
            location.href = "https://developerdv.gent.be/admin/messages/received";
        };

        document.getElementById("settingsbutton").onclick = function () {
            location.href = "https://developerdv.gent.be/admin/account";
        };

        document.getElementById("applicationsbutton").onclick = function () {
            location.href = "https://developerdv.gent.be/admin/applications";
        };

    }());
</script>
```
