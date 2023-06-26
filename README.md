# Websiten basierend auf daten
Angenommen die Anforderung ist es 100 Serien mit ihrer beschreibung und cast online darzustellen.
Also man hat eine Seite und kann die Serien auswählen und dann werden die Daten dargestellt

# Lösung 1 jede serie eine .html serie
Ein Lösungsansatz wäre es für jede Serie eine eigene html datei zu machen und diese mit einer hauptseite zu verinekn.

## Mögliche Schwachstellen
Angenommen man soll zusätzich auf den einzelnen Serien seiten einen neune blöck mit einer Übersicht über ähnliche serien rein. DAnn msste man JEDE html seite anpassen. DAs will man natürlich nicht

# Lösung 2 
Ansatz hier ist es das man nur eine html seite hat. Und diese Seite wird dann vom javascript angepasst falls man eine andere Serie anzeigen will

## tutorial
Erstmal muss man sich gedanken machen wie man die ganzen informationen zu den serien in javascript nutzen kann. Eine Möglichkeit ist es soganntes json format zu nutzen.
Json ist abgekürzt für JavascriptObjectNotation. Letzendlich stellt man komplexe Daten in einer Variable dar

### json tutorial
variablen in javascript
```js
let stringVariable = "String"
let numberVariable = 1
let numberVariable2 = 3.3
let booleanVariable = true
let arrayVariable = ["element1", "element2"]
let ojectVariabel = {
    name: "Max",
    alter: 12
}
```
hier sind einige variablen gelistet.

#### Array
Besondere sind in dem Falle ein Array. Arrays sind einfach eine liste an anderen variablen. diese variablen können sowohl andere arrays, strings, nummern,boolen oder objekte sein. 
```js
let arrayVariable = ["element1", 2]
let arrayVariable2 = [true, false, 2]
```
Die variablen in den Arrays können gemischt von den typen sein. 

Werte von Arrays werden immer durch ein komma voneinander getrennt.

um auf elemente eines Arrays zuzugreifen nutzt man einen index. Der index ist immer eine nummer welcher die position der variable in der Liste definiert
```js
//  index        0       ,   1       ,     2
let array = ["element1", "element2", "element3"]
```
besonderheit hier ist das der index bei 0 anfängt. das Erste element ist index 0

Hier ein beispiel wie man das erste element in der console ausgeben würde
```js 
let array = ["element1", "element2", "element3"]
console.log(array[0]) // prints element1 to console 
```

#### Object
ein Object / Objekt ist eine variable mit mehreren Attributen/Eigenschaften
```js
let mensch = {
    name: "Max",
    alter: 12
}
```
hier zum beispiel hat die variable objectVariabel nicht einen Wert sondern 2. (name und alter)

um auf die werte zuzugreifen nutzt man den `.` operator
beispiel
```js
let mensch = {
    name: "Max",
    alter: 12
}
console.log(mensch.name) // prints Max to console
```

### Datenstrukturen
mit den arrays und den Objecten als variablen ist es nun recht simpel komplexe daten als eine variable im javascript darzustellen.
So könnten wir zum beispiel eine Liste an menschen erstellen welche alle eigene namen und unterscheidliche alter haben
```js
let menschen = [
    {
        name: "Mensch1",
        alter: 12
    },
    {
        name: "Mensch2",
        alter: 21
    },
    {
        name: "Mensch3",
        alter: 1222
    }
]
```

hier zum beispiel haben wir eine Liste/array erstellt welcher 3 Objekte beinhaltet. Jedes dieser Objekte hat jeweils einen name und ein alter als eigenschaft

Beispiel zum ausgeben des namen der Zweiten person in der Liste

```js
let menschen = [
    {
        name: "Mensch1",
        alter: 12
    },
    {
        name: "Mensch2",
        alter: 21
    },
    {
        name: "Mensch3",
        alter: 1222
    }
]
let mensch = menschen[1] // speichert element 2 bzw variable mit index 1 in neue variable mensch
console.log(mensch.name) // prints Mensch2
```
diesen schritt der erstellung der variable mensch kann man jedoch überspringen. Jedoch wird der Code dann schwerer nachvollziehbar für den Menschen der den Code lesen würde

```js
let menschen = [
    {
        name: "Mensch1",
        alter: 12
    },
    {
        name: "Mensch2",
        alter: 21
    },
    {
        name: "Mensch3",
        alter: 1222
    }
]
console.log(menschen[1].name) // prints Mensch2
```
## Was bringt uns das alles

Über listen kann man mit schleifen recht simpel "laufen". Also man nimmt sich jedes element und führt code damit aus.

Eine Idee wäre nun für jeden Menschen in der liste einen html Button zu erstellen. Wenn dieser button dann geklickt wird werden die Daten des Menschen weiter unten auf einer Seite dargestellt.

### For Schleife (Array)
```js
let menschen = [
    {
        name: "Mensch1",
        alter: 12
    },
    {
        name: "Mensch2",
        alter: 21
    },
    {
        name: "Mensch3",
        alter: 1222
    }
]
// nehme jedes element in den array und schreibe es in variable mensch.
// dann führe den code in den GEschweiften klammer aus
for(let mensch of menschen){ 
    console.log(mensch.name) // prints name of menschen in console
}
```
Hier in dem beispiel wird eine for schleife genutzt.

nun könnte man html elemente erstellen statt einfach nur einen console.log() zu machen
```js
let menschen = [
    {
        name: "Mensch1",
        alter: 12
    },
    {
        name: "Mensch2",
        alter: 21
    },
    {
        name: "Mensch3",
        alter: 1222
    }
]
for(let mensch of menschen){ 
    let buttonElement = document.createElement("button")
    buttonElement.innerText = mensch.name
    buttonElement.addEventListener("click", function(e){
        console.log(e)
        render(mensch)
    }) 
    document.body.appendChild(buttonElement)
}

function render(mensch){
    console.log(mensch)
}
```

* hier ist schon sehr viel passiert. Wir erstellen ein neues html button element und speichern uns das in der variable buttonElement.
* daraufhin setzen wir den innerText der variable buttonElement gleich dem namen des Menschen
* dann fugen wir dem button eine onclick function hinzu
    * diese onclick function ruft dann die `render()` function auf
    * diese render function wird die mensch variable als Parameter mitgegeben
        * das bedeutet die render function kennt die variable mensch
* in der render funktion geben wir erstmal nur den menschen als variable aus

Hier könnte man sich dann überlegen ob man auf bereits exestierende html elemente verweist oder neue html elemente erstellen will
### auf html elemente verweisen
hier muss du sicherstellen das die html elemente mit den ids bereits auf der seite existieren

```js
let menschen = [
    {
        name: "Mensch1",
        alter: 12
    },
    {
        name: "Mensch2",
        alter: 21
    },
    {
        name: "Mensch3",
        alter: 1222
    }
]
for(let mensch of menschen){ 
    let buttonElement = document.createElement("button")
    buttonElement.innerText = mensch.name
    buttonElement.addEventListener("click", function(e){
        console.log(e)
        render(mensch)
    }) 
    document.body.appendChild(buttonElement)
}

function render(mensch){
    document.getElementById("menschenName").innerText = mensch.name
    document.getElementById("menschenAlter").innerText = mensch.alter
}
```

### neue html elemente erstellen
hier muss es nur ein html element mit der id "menschenInfos" geben. dieses element wird dann immer gelöscht und neu beschreiben wenn ein button geklickt wird

```js
let menschen = [
    {
        name: "Mensch1",
        alter: 12
    },
    {
        name: "Mensch2",
        alter: 21
    },
    {
        name: "Mensch3",
        alter: 1222
    }
]
for(let mensch of menschen){ 
    let buttonElement = document.createElement("button")
    buttonElement.innerText = mensch.name
    buttonElement.addEventListener("click", function(e){
        render(mensch)
    }) 
    document.body.appendChild(buttonElement)
}

function render(mensch){#

    let menschenInfos = document.getElementById("menschenInfos")
    menschenInfos.innerHTML = "" // lösche alle elmente in den element
    
    //erstelle div elemente
    let namenElement = document.createElement("div")
    namenElement.innerText = mensch.name
    let alterElement = document.createElement("div")
    alterElement.innerText = mensch.alter
    
    //füge erstelle div elemenbte dem menschenInfo element hinzu
    menschenInfos.appendChild(namenElement)
    menschenInfos.appendChild(alterElement)
}
```