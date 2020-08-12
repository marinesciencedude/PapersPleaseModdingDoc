**Error.txt**

Location: root\data

Defines errors that can be present for an entrant.

### Usage

```
*ActionID
	" SpeechID

*ErrorID<tag>
	\ Requirement
	! RequirementCheck
		> Interrogate
			" SpeechID
			@ Action
	
*ConfusingErrorID<tag>
	\ Requirement
	! ~RequirementCheck
		> Interrogate
			" SpeechID
			@ Action
```

* *Action/ErrorID*: An ID for the Action or Error to be referenced elsewhere.
* <*generic/contraband/missing*>: An optional tag for the Error.
* \ Requirement: The ID of an item (found in Papers.xml) required for the error to be recognised. Can also be in the form of a logical expression, by checking information from a path (defined in Facts.xml).
* ! RequirementCheck: The ID of the information required for the error to be recognised. Prefaced with '~' if the error can be cleared.
* > *Interrogate/$Interrogate:Error*: Used for defining interrogation dialogue and actions. 
* " SpeechID: The ID for the speech (found in Speeches.txt).
* @ *Fingerprint/Detain/Search*: An action that occurs.

### Examples

```
*Interrogate:WrongName
	" ask-wrong-name
	" wrong-name
	@ Fingerprint

*Interrogate:WrongAlias
	" ask-wrong-alias
	" default
	@ Detain
```



```
Passport-WrongFaceClear<generic>
	\ Passport
	\ Day/Features has FINGERPRINT
	! ~Passport/Face
		> Interrogate 
			" ask-wrong-face
			" wrong-face
			@ Fingerprint
Passport-WrongFaceError<generic>
	\ Passport
	! Passport/Face
		> Interrogate 
			" ask-wrong-face
			" wrong-face
			@ Fingerprint
	! IdentityRecord/Fingerprints
		> $Interrogate:WrongFingerprints
```

Highlights the distinction in-code a 'clearable' error has.

```
Passport-Missing<missing>
	\ Passport
	\ Day/Features has INSPECT
	! Passport/Exists
		> $Interrogate:Missing passport
			+ VisaSlip
Passport-Hidden<missing>
	\ Passport
	\ Day/Features has INSPECT
	! Passport/Visible
		> $Interrogate:Hidden passport
			^ Passport/Visible
```

Hidden documents use a different system to other 'clearable errors'.

```
Rules-DetainKolechia
	\ Rules
	\ Traveler/Nationality == Kolechia
	\ Day/Rules has RuleDetainKolechia
	! Rules/RuleDetainKolechia
		> Interrogate
			" ask-detain-enabled
			" detain-enabled
			@ Detain
```

Some errors require certain rules to be in place.

```
Bulletin-News0
	\ Bulletin
	! Bulletin/News0
		> Interrogate
Bulletin-News1
	\ Bulletin
	! Bulletin/News1
		> Interrogate		
Bulletin-News0News1
	\ Bulletin
	! Bulletin/News0
		> Interrogate	
	! Bulletin/News1
		> Interrogate
```

Some errors are based around the bulletin. These appear to be for the entrant 'KILLERATHLETE' (Vince Lestrade)

```
Misc-BrothelHelp
	\ BrothelHelp
	! BrothelHelp
		> Interrogate
			# response is handled manually by traveler
Misc-BoothCounter
	! Booth/Counter
		> Interrogate
			# response is handled manually by traveler
Misc-Pezpert
	\ Pezpert
	! Pezpert
		> Interrogate
			# response is handled manually by traveler
```

And other errors are based around items other than a official documents, or lack thereof in the case of 'Misc-BoothCounter', used for 'MRPERSISTENT0' (Jorji Costava's first appearance).
