# meteorPrototype
## Learning meteor.js and keeping JS skills up to date for final project prototype and SRP at the HvA

Tutorial - Making a plan

> Om mijn ervaring zo effectief als mogelijk te kunnen delen heb ik het voornemen gevat elke stap en alles waar ik tegenaan loop zo zorgvuldig als mogelijk te documenteren. Allereerst is het van belang om mijn huidig kennisniveau te bepalen om een beter perspectief te bieden m.b.t. het niveau van instap voor de lezer. Herken je jezelf in dit niveau en durf je -net als ik- de sprong niet te wagen naar een wat geavanceerder framework/platform? Dan stel ik voor dat we dit samen gaan doen =).

### Inhoud
Inhoud volgt later.

---

### What do I know?
In schooljaar 2013-2014 heb ik het vak Frontend development 2 gevolgd. Hier zet ik de begrippen en methoden die daar zijn gehanteerd uiteen. Sleutelwoorden tijdens dat vak waren:

- Syntax
- Variabele
- Array
- Meesturen van data
- OOP
- Object
- Self invoking function
- Scope
- Routing

Aan de hand van voorbeelden in de tutorial van meteor.js zal ik in gaan op deze materie gebaseerd op eigen ervaring.

#### Meteor.js to-do app

Het eerte stukje javascript uit de tutorial:

#####2.2 Templates starter replacement code

```javascript
if (Meteor.isClient) {
  // This code only runs on the client
  Template.body.helpers({
    tasks: [
      { text: "This is task 1" },
      { text: "This is task 2" },
      { text: "This is task 3" }
    ]
  });
}
```
