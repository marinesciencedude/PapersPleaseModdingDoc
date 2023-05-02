**Faces.xml**

Location: root/data

Defines the faces of the entrants.

### Usage

```
<faces>
  <sheet id="">
    <face age="" bmi="" hairheight="" head=""
                                      eyes=""
                                      mouth=""/>
  </sheet>
</faces>
```

Only one from head, eyes and mouth are used per face in the default Faces.xml, and only for Males.

* id: The ID of the Sheet, correpsonding to the image file i.e. id="M0" for SheetM0.png
* age: The age of the entrant.
* bmi: The Body-Mass Index of the entrant.
* head: _`Bald`_,_`Beard`_,_`Balding`_,_`Blonde`_ A modifier for the entrant.
* eyes: _`Glasses`_ A modifier for the entrant's eyes.
* mouth: _`Mustache`_ A modifier for the entrant's mouth.
