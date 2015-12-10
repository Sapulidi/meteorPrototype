# meteorPrototype
## Learning meteor.js and keeping JS skills up to date for final project prototype and SRP at the HvA

Alexander Eerenberg, 2015

Tutorial - Making a plan

> Om mijn ervaring zo effectief als mogelijk te kunnen delen heb ik het voornemen elke stap en alles waar ik tegenaan loop zo zorgvuldig als mogelijk te documenteren. Allereerst is het van belang om mijn huidig kennisniveau te bepalen om een beter perspectief te bieden m.b.t. het niveau van instap voor de lezer. Herken je jezelf in dit niveau en durf je -net als ik- de sprong niet te wagen naar een wat geavanceerder framework/platform? Dan stel ik voor dat we dit samen gaan doen =).

Na het volgen en ontleden van de tutorial en meteor.js volgt mogelijk het moeilijkste gedeelte: iets voor jezelf maken. Je hebt een idee en weet niet echt hoe je dit moet gaan uitwerken. Op dit moment denk ik dat het voornamelijk belangrijk is om je processen goed in kaart te brengen. Weet wat je wilt en hoe het eruit moet gaan zien. Gebruik desnoods flowcharts e.d. om erachter te komen wat wanneer moet gebeuren.



### Inhoud
Inhoud volgt later.

- Tutorial
- Eigen module creëren

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

#### Meteor.js to-do app tutorial 

Dit is de officele [meteor.js tutorial](https://www.meteor.com/tutorials/blaze/creating-an-app) die gbruikt wordt tijdens dit project.

Allereerst dien je natuurlijk meteor.js te installeren. Gebruik de installatie op https://www.meteor.com/install. Ik raad Windows-gebruikers aan om Powershell te gebruiken in plaats van command-prompt. Dit omdat je wat makkelijker kan copy/pasten e.d.

Het eerste stukje javascript uit de tutorial:

####2 - Templates starter replacement code 

Onderstaande code wordt zoals vernoemd alleen door de client uitgevoerd. De content die getoond wordt als je dit in je browser bekijkt lijkt op dit moment nogal statisch te zijn. Meteor zorgt ervoor dat de taken die in dit voorbeeld zijn opgenomen in het stukje javascript getoond worden in de html. Het stukje: "Template.body.helpers" duidt aan dat er een helper is aangemaakt. Deze helper geeft een array aan informatie terug als je de inhoud hiervan zou opvragen.

####### js2.1
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
####### html2.2
```html
<head>
  <title>Todo List</title>
</head>
 
<body>
  <div class="container">
    <header>
    </header>
      <h1>Todo List</h1>
 
    <ul>
      {{#each tasks}}
        {{> task}}
      {{/each}}
    </ul>
  </div>
</body>
 
<template name="task">
  <li>{{text}}</li>
</template>
```

Binnen de unordered list staat een loop:
####### html2.2.0
```html
{{#each tasks}}
	{{> task}}
{{/each}}
```

Wat een platform als meteor.js en andere frameworks als angular.js zo aantrekkelijk maakt, is dat je door dit soort stukjes code toe te voegen aan je html-bestand al direct informatie uit bijvoorbeeld een database kunt tonen. Geen ingewikkeld gedoe met php en databases/queries, gewoon direct opvragen.

Wat hier staat is het volgende: Geef elke task uit de template helper tasks (in het stukje javascript hierboven) weer. Of dit nu task 1 t/m 100 is of de drie tasks die er nu staan zijn, ze worden allen weergegeven in je html door dit hele kleine stukje code.

Hoe deze taken in de unordered list;
####### html2.2.1
```html 
<ul> 
{{#each tasks}}
	{{> task}}
{{/each}}
</ul>
``` 
 worden weergegeven wordt bepaald door:
####### html2.2.2
```html
<template name="task">
	<li>{{text}}</li>
</template>
```

De naam van deze template is "task" en binnen de curly braces {{text}} wordt de tekst opgevraagd uit de array van de tasks helper in het eerste stukje javascript [js2.1](#js21).

#####Samenvatting 2.2

Middels dit kleine stukje code wordt er dus content getoond die eigenlijk niet in de html staat. Deze content zou uit bijvoorbeeld een database of JSON bestand kunnen komen. Het is een goed voorbeeld van hoe een template engine zou kunnen werken.

Zelf was ik al redelijk op de hoogte van wat hierboven beschreven staat. Het is echter zo dat het in stukken breken van stukjes code zeer nuttig kan zijn om het nog beter te begrijpen.

####3 - Collections

Dit is waar het al een stuk leuker gaat worden, we gaan gebruik maken van [MongoDB](http://searchdatamanagement.techtarget.com/definition/MongoDB) (MDB). Dit hoef je niet te installeren want MDB is onderdeel van het meteor.js pakket. Door MDB te gebruiken kun je heel veel meer dan bij traditionele(re) databases. De tutorial geeft al voldoende uitleg over wat MDB voor je kan betekenen.

Belangrijk om te onthouden is dat je aan MDB zogeheten 'collections' toe kan voegen. De informatie in deze collections worden documents genoemd.

Een nieuwe collectie toevoegen om daar later de informatie uit te gebruiken en weer te geven zoals in voorgaande oefening gaat heel gemakkelijk:

####### js3.1
```javascript
Tasks = new Mongo.Collection("tasks");
```

Dit lijkt heel erg op het aanmaken van een nieuwe variabele in bijvoorbeeld jQuery. De variabele 'Tasks' bevat een Mongo.Collection waar "tasks" in opgeslagen (en uitgehaald) kunnen worden.

####### js3.2
```javascript
if (Meteor.isClient) {
  // This code only runs on the client
  Template.body.helpers({
    tasks: function () {
      return Tasks.find({});
    }
  });
}
```

Dit is de code die [js2.1](#js21) vervangt. De array waar de informatie werd opgeslagen is nu een MongoDB collectie geworden. Wat hier in feite staat is het volgende: 

- de helper tasks functie roept alle informatie op die in de collectie(variabele) Tasks gevonden kan worden. 

De collectie is op dit moment nog leeg want we hebben er nog niets ingestopt. Omdat je meteor hebt draaien middels je console (powershell, cmd, terminal of iets anders) is er ook een actieve MongoDB server gestart.

type: 

```
meteor mongo
```

en druk op enter. Dit zorgt ervoor dat je instructies aan de database kan geven. Copy/paste of typ de instructie uit de tutorial om iets toe te voegen aan de MDB.

```
db.tasks.insert({ text: "Hello world!", createdAt: new Date() });
```

Je hebt nu een document toegevoegd aan de Tasks collectie! Als alles goed is gegaan is dit ook direct terug te zien in je html pagina, zonder deze te verversen. Geen extra code om verbinding te maken met de server en het verversen van de pagina. Het werkt gewoon zonder al die extra moeite. En dat is natuurlijk awesome =)!

####4 - Forms and events
