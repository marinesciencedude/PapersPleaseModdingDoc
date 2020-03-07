**Bodies.xml**

Location: root/data

Defines regions of the body and contraband.

### Usage

```
<bodies>
  <loc id="" rect=""/>
  
  <contra type="" loc="" file="">
    <offset body="" val=""/>
  </contra>
</bodies>
```

Body region:

* id: ID of the body region that can be referenced elsewhere.
* rect: The area of the body region represented by a rectangle.

Contraband:

* type: _gun,knife,bomb,drugs_ Type of contraband.
* loc: _back,legr,legl_ Region of body the contraband is on.
* file: Filename (and extension) of the image in root/faces
* body: The body ID, i.e. M0, F0 etc.
* val: The amount the sprite is offset by in the format "x y".
