**Papers.xml**

Location: root/data

Defines items that can be 

### Usage Examples

```
<?xml version="1.0" encoding="UTF-8" ?>
<papers>
	<!-- Passports -->
	<paper id="" nation="" outer="" font="" fontshifty="" textcolor="" fromtraveler="true" stampable="true" canconfiscate="true">
		<page image="">
			<mark text="$Name" format="Last, First"/>
			<mark image="$Face" scale="0.5"/>
			<mark text="$BirthDate"/>
			<mark text="$Gender"/>
			<mark text="$IssuingCity"/>
			<mark text="$ExpirationDate" format="120 720"/>
			<mark text="$IdNumber"/>
		</page>
	</paper>
</papers>
```

* id: An id that can be referenced in Travelers.txt
* outer: Filename (and extension) of the item seen in the console area of the desk.
* font: Font used for text in the item.
* fontshifty: 
* textcolor: A hexadecimal code (prefaced by 0x) used for text colour.
* stampable="true": Determines if a stamp can be put on the item (Used for passports only)

Page

* image: Filename (and extension) of a page of the item seen in the main desk.
* tag: Text or image that replaces black dots on the image file, going top to bottom in the case of multiple tags.
	* text: A text string (or contextual information prefaced with $) to be displayed on the item at a black dot on the image file.
	* image: Filename (and extension) of image to be displayed on the item at a black dot on the image file.
	* format: Info-specific modifier:
		* $Name: Determines the name order if not First, Last.
	* scale: A float value to determine how much the image should be scaled.
