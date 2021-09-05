# User

```
Zkontrolovat custom user model.
Je potřeboa ho zeštíhlit a zbytek přidat přes &quot;user_profile&quot; s OneToOne?
Omezené přístupy na adminu, také pomocí lokace (nebo jiných polí). Vytvořit na to custom
&quot;group&quot;, dekorátor ke groupě?
Použít - queryset=Model.objects.all() - jinou metudu?
User login - LDAP, custom auth middleware ok?
 
Vytvoření &quot;default&quot; usera při prvním loginu. Pomocí middlewaru? Nebylo by to pomalé? Použít
ModelManager?
 
Field &quot;Role&quot; - potřeba nebo přežitek z cherrypy? Neřeší to za nás groups a permissions?
```

---

- User profile vs. 1:1 model
- [https://docs.djangoproject.com/en/3.2/topics/auth/customizing/#custom-permissions]()
- metody querysetu ,...
- LDAP [https://django-auth-ldap.readthedocs.io/en/latest/]()
- `Role` - nepružné
  - [https://django-improved-permissions.readthedocs.io/en/latest/]()
  - [https://django-guardian.readthedocs.io/en/stable/]()
  - ...