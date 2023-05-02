**Travelers.txt**

Location: root\data

Defines the entrants referenced in Days.csv

### Usage

```
ENTRANT
	= nation 
	= name 
	= gender
	= face 
	= purpose
	> 

ANOTHER_ENTRANT
	INCLUDE ENTRANT
	MANUALPAPERS
	+ 
	= want

RANOM_ENTRANT
	= nation Arstotzka:1 Kolechia:1 Obristan:1 Republia:1 Antegria:1 Impor:1 UnitedFed:1
	= error
		x 1 --
		x 2 <generic> <speech> <missing>
```

* = nation _`Arstotzka_`/_`Kolechia`_/`_Obristan`_/_`Republia`_/_`Antegria`_/_`Impor`_/_`UnitedFed`_: Defines what nation (found in [Facts.xml](../xml/Facts.md)) the entrant is from. 
* = nation _`Arstotzka:A Kolechia:B Obristan:C Republia:D Antegria:E Impor:F UnitedFed:G`_: Used to randomise the entrant's nationality, notably for 'filler' entrants, where A,B,C,D,E,F are numbers used for weighting.
* = name _`FirstName-LastName`_: Defines the name of the entrant. As seen with HUSBAND_WIFE_TEAM, the First Name (and possibly Last Name) can be omitted to allow randomisation.
* = gender _`M`_/_`F`_: Defines the gender of the entrant.
* = face _`X-A-B-C-D-E`_: Defines the look of an entrant, where X is M/F and A,B,C,D,E are numbers corresponding to the sprites in root\faces.
* = purpose: Defines what should be on the 'Purpose' field for the Entry Permit. Correct values can be found in [Facts.xml](../xml/Facts.md)
* = duration: Defines what should be on the 'Duration of Stay' field for the Entry Permit. Correct values can be found in [Facts.xml](../xml/Facts.md)
* = job: Defines what should be on the 'Occupation' field for the Work Permit. Unused in Travelers.txt, though confirmed to be working.
* = error _`ErrorName`_: Defines what errors (found in Errors.txt) will be present in an entrant's documentation.
	* x 1 --
	* x 2 <generic> <speech> <missing>
		* Used for randomising whether the entrant will have an error or not.
* INCLUDE _`ENTRANT`_: Includes all features of another entrant, for use when an entrant appears on multiple days (see MR_PERSISTENT)
* MANUALPAPERS: Used for when an entrant is meant to have documents other than the typical for the day, e.g. none at all, Entry Ticket instead of Entry Permit etc.
* \+ _`Item ID`_: Sets one item an entrant has.
* = want _`Item ID`_: Indicates that an item can be given to an entrant.

### Custom Dialogue

```
> 
	" 
	" @
	+ 
	@
```

* " _`Entrant Speech`_: Normal dialogue from the entrant. Can also be used for with certain dialogue IDs (defined in Speeches.txt) for the player character's dialogue. Custom purpose/duration dialogue must be appended with [Speech/Purpose] or [Speech/Duration] so they are selectable in the audio transcript for interrogation.
* " @_`Player Speech`_: Special case example for the player character's dialogue.
* \+ _`Item ID`_: Allows entrants to give items during dialogue.
* @ _`Leave`_: Forces the entrant to leave the booth (always to the left, back to Kolechia's side of the border).
* @ _`Detain`_: Enables detainment of an entrant (with the corresponding 'Detain' cue).
* @ News _`Headline \ Subtitle`_: Sets a headline for the following day's newspaper.
* \> Intro-Before: Actions and/or dialogue to take place before any intro dialogue (used only for the 'EZIC' entrant and an unused 'Pevert-1').
* \> Intro-After: Actions and/or dialogue to take place after any intro dialogue (used for the 'BROTHEL2' entrant (the one who sets the Ludum Dari plotline into motion) and an unused 'Pevert-1').
* \> Intro-Replace: Dialogue used when the entrant steps into the booth.
* \> ShutterClose: Actions to take palce if the shutters are closed (only used for the the 'MRPERSISTENT0' entrant, the first Jorji Costava appearance).
* \> Give-BrothelHelp/Give-EzicIntro: Actions and/or dialogue to take place as a result of giving the the 'BrothelHelp' or 'EzicIntro' items to this entrant
* \> Interrogate-Replace: Dialogue used when the entrant is interrogated.
* \> Detain-Replace: Dialogue used when the entrant is detained.
* \> Detain-After: Dialogue used just before a detained entrant exits the booth (only used for the 'KILLERATHELETE' entrant, i.e. Vince Lestrade).
* \> Approved: Dialogue used for an approved entrant.
* \> Denied: Dialogue used for a denied entrant.
* \> Leave: Actions and/or dialogue used for an exiting entrant, regardless of approval/denial status.

### Game Logic

There are multiple logic states, prefixed by 'Game/', for use in determining previous actions undertaken during a playthrough. These are:

* Game/Ezic
* Game/Ezic-MetCorman
* Game/MrPersistent
* Game/Brothel
* Game/HusbandWifeTeam
* Game/FirstSuicideBomber

These logic states are tested using `? Game/`_`LogicState`_` == "`_`value`_`"` and changed using `= Game/`_`LogicState value`_

This can be used for complex behaviours such as all EZIC-related entrants being condensed into a single entrant, for example:

```
EZIC
	? Game/Ezic == ""
		MANUALPAPERS			
		= nation Arstotzka
		> Intro-Replace
			" The Order awaits.
			+ EzicIntro
			= Game/Ezic waiting-for-corman
			@ Leave
	? Game/Ezic == waiting-for-corman
		= nation Arstotzka
		= name Corman-Drex
		= want EzicIntro
		( EzicIntroCorman
			.*/Name
			EzicIntro/Corman
		? Game/Ezic-MetCorman == YES
			> Intro-Replace
				" You have something of mine.
		> Intro-Before
			= Game/Ezic-MetCorman YES
		> Give-EzicIntro
			" Very good.
			" If you help us, we will help you.
			= Game/Ezic just-joined
	? Game/Ezic == just-joined
		= nation Arstotzka
```

All logic states are set to a blank `""` by default. The first EZIC entrant provides the `EzicIntro` item and sets `Game/Ezic` to `waiting-for-corman`. As a result, the next EZIC entrant will be Corman Drex, who sets `Game/Ezic-MetCorman` to `YES`. If the player neglects to give Corman Drex the `EzicIntro` item, the next time he comes will result in him having different Intro dialogue. Giving Corman Drex the `EzicIntro` item sets `Game/Ezic` to `just-joined`. This results in the next EZIC entrant (if any) being a generic Arstotzkan.

Another example is Jorji Costava, who ceases to keep coming (or rather becomes a generic entrant) if you approve him for entry at any point before his final appearance:

```
MR_PERSISTENT_BASE
	? Game/MrPersistent == done
		= fallback GENERIC
		BREAK
	= nation Obristan
	= name Jorji-Costava
	= gender M
	= face M-1-1-4-4-0
	> Approved
		" All right! You the best!
		" Arstotzka the best!
		" Here, take this!
		+ TokenObristan
		= Game/MrPersistent done
```

The final example for logic states is the Husband and Wife travelling together. For brevity most of the dialogue has been removed:

```
HUSBAND_WIFE_TEAM
	= nation Antegria
	? Game/HusbandWifeTeam == ""
		= gender M
		= name -Martin
		= purpose immigrate
		> Approved
			= Game/HusbandWifeTeam husband-approved
		> Denied
			= Game/HusbandWifeTeam husband-denied
	? Game/HusbandWifeTeam == husband-approved
		= gender F		
		= name -Martin
		= error EntryPermit-Missing
		> Intro-Replace
			" Did you see my husband?
			" He made it through, yes?
		> Approved
			= Game/HusbandWifeTeam husband-wife
		> Denied
			= Game/HusbandWifeTeam husband-only
	?  Game/HusbandWifeTeam == husband-denied
		= gender F		
		= name -Martin
		> Intro-Replace
			" Why did you turn my husband away?
			" I will not leave him to die.
			" You have doomed us both.
			= Game/HusbandWifeTeam husband-only
			@ Leave
```

As usual, by default `Game/HusbandWifeTeam` is set to the blank `""`. Regardless of the player's choice, the entrant is set to be female the next time it enters the booth. If the Husband is approved, the Wife will enter and allow the usual approval/denial. If the Husband is denied, the Wife will e with a different Intro dialogue and promptly leave the booth.

 Finally, the `BROTHEL3` (Dari Ludum) and `KILLER ATHLETE` (Vince Lestrade) entrants show how to make information on an item selectable for interrogation:
 
 ```
 BROTHEL3
	= nation Arstotzka
	= name Dari-Ludum
	= gender M
	= want BrothelHelp
	= error BrothelHelp
	= face M-11-12-8-5
	( PimpName
		.*/Name
		BrothelHelp
 ```
 
 * ( PimpName
 	* .*/Name: The field this information belongs to.
	* BrothelHelp: The ID of the item this information is found on.
 
 ```
 KILLERATHLETE
	= nation Republia
	= gender M
	= name Vince-Lestrade
	= face M-3-3-10-10
	+ Passport
	+ EntryPermit
	= purpose transit
	= error Bulletin-News0News1
	( KillerName0
		.*/Name
		.*/Face
		Bulletin/News0
	( KillerName1
		.*/Name
		.*/Face
		Bulletin/News1
 ```

* (KillerName0
	* Bulletin/News0: The [Facts.xml](../xml/Facts.md) reference to the information
