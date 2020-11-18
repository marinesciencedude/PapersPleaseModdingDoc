**Speeches.txt**

Location: root\data

Defines the inspector and the entrants' dialogue.

### Examples
```
inspector
	ask-purpose
		What is the purpose of your trip?
```

```
traveler
	missing-passport
		They took away my passport.
		What is passport?
```

Standard dialogue, with an ID for referencing elsewhere and multiple lines that can be said.

***

```
inspector
	ask-forgery-missing
		This document is missing its seal.
		There is no seal here.
		I do not see the required seal here.
	ask-forgery-wrong
		This document is forged.
		This is a forgery.
	ask-forgery-entrypermit	EntryPermit/Emblem/MinistryOfAdmission
		=NONE *ask-forgery-missing
		*ask-forgery-wrong	
	ask-forgery-workpermit	WorkPermit/Emblem/MinistryOfLabor
		=NONE *ask-forgery-missing
		*ask-forgery-wrong
```

Contextual dialogue, as well as referencing other speeches. In this case if there is no seal on the Entry or Work Permits, the inspector can remark on its absence rather than merely stating that it is a forgery.

***

```
inspector
	ask-wrong-gender Passport/Gender
		=M You are a man?
		=M It says here that you are male.
		=F You are a woman?
		=F Your passport says you are female.
		Are you a woman or a man?
		You are male or female?
```

Contextual dialogue based on Entrant's traits, in this case for gender. Note the 'Passport/Gender' used to specify what to check for.

***

```
inspector
	ask-approved
		?Traveler/Nationality==Arstotzka 	Glory to Arstotzka.
		?Traveler/Nationality!=Arstotzka 	Cause no trouble.
	ask-nativesonly
		?Traveler/Nationality==Arstotzka 	Try again.
		?Traveler/Nationality!=Arstotzka 	Arstotzkans only.
	ask-wrong-nation
		?Traveler/Nationality==Obristan 	No entry from Obristan.
		?Traveler/Nationality==Kolechia 	No entry from Kolechia.
		?Traveler/Nationality==UnitedFed 	No entry from United Federation.
		?Traveler/Nationality==Antegria	 	No entry from Antegria.
		?Traveler/Nationality==Republia	 	No entry from Republia.
		?Traveler/Nationality==Arstotzka	No entry from Arstotzka.
		?Traveler/Nationality==Impor		No entry from Impor.
```

Contextual dialogue by a different means of checking (without specifying upfront), this time for nationality.

***

```
traveler
	state-purpose	Speech/Purpose
		=immigrate	?Passport/Gender==F I am coming to live with my husband.
		=immigrate	?Passport/Gender==M My wife is Arstotzkan.
```

Contextual dialogue by combining the above methods.
