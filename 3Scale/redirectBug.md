## Aanpassingen Dinsdag 7 Augustus

> De redirects in de Documentation pagina werkten niet omdat Swagger UI deze onderschepte en een fout opwerpt.
> Daarom heb ik de redirects in javascript gezet.

-   De ID tag toevoegen aan elke knop
-   De javascript functie onclick aanmaken voor elke link

### File: partial/submenu

```html
<div id="navbar-1" class="collapse navbar-collapse">
  {% if current_user %}
    {% unless current_account.requires_credit_card_now? %}
      <ul class="navbar-nav ml-auto">
        {% if provider.multiple_applications_allowed? %}
          <li class="nav-item {% if urls.applications.active? %}active{% endif %}">
            <a class="nav-link" href="{{ urls.applications }}" id="applicationsbutton">{{ urls.applications.title }}</a>
          </li>
          {% elsif current_account.applications.first == present%}
          {% assign app = current_account.applications.first %}
          <li class="nav-item {% if app.url.active? %}active{% endif %}">
            <a class="nav-link" href="{{ app.url }}">API Credentials</a>
          </li>
          {% elsif current_user.can.create_application? %}
          <li class="nav-item {% if url.new_application.active? %}active{% endif %}">
            <a class="nav-link" href="{{ urls.new_application }}">Get API Credentials</a>
          </li>
        {% else %}
          <!-- You don't have any application neither can create one. Bad luck. -->
        {% endif %}
        {% assign live_apps_present = current_account.applications | map: 'state' | any: 'live' %}
        {% if live_apps_present %}
          <li class="nav-item {% if urls.stats.active? %}active{% endif %}">
            <a class="nav-link" id="statisticsbutton" href="{{ urls.stats }}">Statistics</a>
          </li>
        {% endif %}
        {% if provider.multiple_services_allowed? %}
          <li class=" nav-item{% if urls.services.active? %}active{% endif %}">
            <a class="nav-link" href="{{ urls.services }}">{{ urls.services.title }}</a>
          </li>
        {% endif %}
        <li>
          <a class="nav-link" class="nav-item" id="docsbutton" {% if urls.docs.active? %}active{% endif %}" href="https://developerdv.gent.be/docs/">Documentation</a>
        </li>
      </ul>
    {% endunless %}
    <ul id="user_widget" class="nav navbar-nav">
      {% unless current_account.requires_credit_card_now? %}
        <li class="nav-item {% if urls.messages_inbox.active? %}active{% endif %}">
          <a class="nav-link" href="{{ urls.messages_inbox }}" id="messagesbutton">
            Messages
            {% if current_account.unread_messages.size > 0 %}
              <span class="badge">{{ current_account.unread_messages.size }}</span>
            {% endif %}
          </a>
        </li>
        <li class=" nav-item {% if urls.account_overview.active? %}active{% endif %}">
          <a class="nav-link" href="{{ urls.account_overview }}" id="settingsbutton">
            <i class="fa fa-cogs"></i>
            Settings
          </a>
        </li>
      {% endunless %}
    </ul>
     <ul class="navbar-nav">
        <li class="nav-item">
           <a id="sign-out-button" class="btn btn-sm btn-outline-secondary " title="Logout {{ current_user.username }}"    href="{{ urls.logout }}">Sign out
        </a>
        </li>
      </ul>
  {% else %}
    <ul class="navbar-nav ml-auto">
      <li class="nav-item active">
        <a class="nav-link" href="https://developerdv.gent.be/docs/" id="docsbutton">Documentation</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="https://developerdv.gent.be/#plans">Plans</a>
      </li>
    </ul>
    <ul class="navbar-nav">
      <li class="nav-item">
        <a class="btn btn-sm btn-outline-secondary" href="{{ urls.login }}" title="Login">Sign in</a>
      </li>
    </ul>
  {% endif %}
</div>
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
