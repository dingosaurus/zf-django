# Models

```
Vyplatí se ke každému modelu hned vytvářet model forms? Jaké? Jejich použití v adminu -
omezení.
 
Computed fields - @property? Lazy?
Select v modelech?
Constraints:
- timespan_from &lt; timespan_to, a jiné - v Meta, nebo ve forms?
- One of two fields set (TCCServer - todo v pycharmu)
 
Diamond dependency - Hil patří do lokace a místnosti, lokace mají místnosti. Jak zajistit, aby
nebylo možné vybrat místnost z jiné lokace.
Nebo místnost má lokaci? .. Promyslet best practice.
Nebo nechat u HiLu jen místnost a řešit lokaci HiLu jako Hil.room.location?
 
HiL patří do projektu - k projektu přiřazuji HiLy. Jaká je best practice? Form inline? Jde to pomocí
custom forms?
 
 
Automaticky generované HiL ID podle BU. V New()? Created=True? Callable v default?
ModelManager?
 
 
Defaultní model - default settings, nebo &quot;not set&quot; možnost - řeší se to nějak konkrétně, nebo
přes &quot;default&quot; u fields? Mít připravenou default fixture?
 
Q a F ??
 
Timezones - zobrazení časů podle toho, jak si uživatel vybere. Defaultně automaticky podle
uživatelovy timezony. Je potřeba mít model TimeZone?
```

---

- `@property`, `@cached_property`
- Select v modelech - SQL operace patří do model QuerySetu
- Kontrolovat vygenerovaný SQL kód

Diamond dependency

  - ukládat postupně a následně readonly? 
  - Validace v modelu (`clean()`)?
  - Model.Meta Constraints

Timezone - ukládat v UTC
Q() a F() - klidně používat, kontrolovat SQL. [https://docs.djangoproject.com/en/3.2/ref/models/conditional-expressions/]()


Overview - ??


```python

class MyModelQuerySet(BaseQuerySet):
    def recommended(self):
        return self.filter(is_recommended=True)

    def random(self):
        return self.order_by('?')
    
    def published(self, user: User=None):
    
        qs = self.filter(
            # allow any
            Q(is_private=False, is_published=True) 
            |
            # allow admins
            Q(Q(owner=user) | Q(pk__in=objects_admined), is_published=False)
        )
        
        return qs

class MyModel(BaseModel):
    ...
    
    objects = MyModelQuerySet.as_manager()


MyModel.objects.random()
MyModel.objects.filter(...).published().recommended()

```