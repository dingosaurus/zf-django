# Admin

```
Více django admin stránek s omezenými přístupy. Dělá se to tak? Jak moc náročné a
komplikované?
(Maintenance team má svůj admin, přidává upravuje maintenance…
project admin vidí a upravuje projekty, assign HiLů…)
 
Model forms na Django adminu. Je lepší používat model forms nebo definovat fields v adminu?
Proč se nedají ve forms používat fieldsets?
 
Add HiL - prefill. Dvě forms na django adminu (jedna pro výběr prefill hilu)?
Upravit template, nebo je tohle případ, na opuštění adminu.
Nejradši bych upravil admin template.
```

---


## Admin

- Zaregistrování modelu do více adminů
- BaseAmin
- ModelAdmin - lepší je definice fields

Permissions

  - Problém s jemnými právy (jen CRUD)
  - Object level permission

šablony 

  - upravoval lze 
  - dědičnost
  - pozor na nové verze djanga 

