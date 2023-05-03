**Facts.xml**

Location: root\data

Defines information types for documents.

### Nations
```
<facts>
	<nations>
		<nation name="" cities="" citizen=""/>
	</nations>
</facts>
```
* name: Name of the Nation.
* cities: Name of the cities, separated by semicolons ;
* citizen: Name of the citizen of the Nation (likely unused)

### Purposes
```
<facts>
	<purposes>
		<purpose val="">
	</purposes>
</facts>
```
* val: Word describing the purpose of an entrant coming to Arstotzka.

### Durations
```
<facts>
	<durations>
		<duration val="" text="" purposes=""/>
	</durations>
</facts>
```
* val: The length in months (can be a decimal) of the duration.
* text: Defines the 'Duration' entry on the Entry Permit.
* purposes: Valid purposes this duration can be randomly chosen with, separated by a single space. 'native' is also a valid entry.

### Districts
```
<facts>
	<districts>
		<district val=""/>
	</districts>
</facts>
```
* val: Name of the Arstotzkan District.

### Jobs
```
<facts>
	<jobs>
		<job val=""/>
	</jobs>
</facts>
```
* val: The name of the job.

### Rules
```
<facts>
	<paper id="Rules" stay="true">
		<fact id="[NATIONS]-Passport0" val="PassportOuter[NATIONS].png"/>
		<fact id="[NATIONS]-IssuingCities" val="[ISSUINGCITIES]"/>

		<fact id="Arstotzka-Districts" val="[DISTRICTS]"/>
	</paper>
</facts>
```
* stay=true: Determines if it should be persistent across entrants exiting (and being detained).
* id: Identifier for referencing selectable information elsewhere.
	* _`[NATIONS]-Passport0`_: Bases it on a category of fact rather than repeating code for all within that category.
* val: reference to fact or filename (which can also reference a type of fact).

### Booth
```
<facts>
	<paper id="Booth">
		<fact id="Counter" val="VALID" desc="Missing documents"/>
		<fact id="Clock" val="VALID"/>
		<fact id="Face" val="VALID"/>
		<fact id="Weight"/>
		<fact id="Height"/>
	</paper>
</facts>
```
Allows parts of the boot to be selected.

### Traveler
```
<facts>
	<paper id="Traveler">
		<fact id="Nationality">
			<invalidate when="" path=""/>
			<desc when="" val="" />
		</fact>
	</paper>
	<fact id="Job"/>
	<fact id="Purpose"/>
	<fact id="Duration"/>
	<fact id="Gender"/>
	<fact id="Contraband" desc="Possible Smuggler Admitted">
		<!-- Only facts with generated contraband will appear, so it's ok to invalidate all of them -->
		<invalidate path="Photo/ContrabandBack"/>
		<invalidate path="Photo/ContrabandBackLegL"/>
		<invalidate path="Photo/ContrabandBackLegR"/>
		<desc when="*bomb" val="Possible Terrorist Admitted"/>
	</fact>
</facts>
```
Defines facts about the entrant, where the 'No Entry from Nation' discrepancies are handled. Also shows how to dynamically change the citation description.

### Photo
```
<facts>
	<paper id="Photo">
		<fact id="Name"/>
		<fact id="BodyFront"/>
		<fact id="BodyBack"/>
		<fact id="HeadFront"/>
		<fact id="HeadBack"/>
		<fact id="ContrabandBack"/>
		<fact id="ContrabandBackLegL"/>
		<fact id="ContrabandBackLegR"/>
		<clearconfusion path="Passport/Gender"/>
		<clearconfusion path="Rules/RuleSearchKolechia"/>
		<clearconfusion path="IdCard/Weight"/>
	</paper>
</facts>
```
Defines selectable information on Contraband Scanner photos. Note the `clearconfusion` for clearing discrepancies.


### Speech
```
<facts>
	<paper id="Speech">
		<fact id="Purpose">
			<invalidate when="work" path="Rules/RuleNeedWorkPermit"/>
		</fact>
		<fact id="Duration"/>
	</paper>
</facts>
```
Defines selectable information for the transcript.

### Passport
```
<facts>
	<paper id="Passport">
		<fact id=""/><!-- desc="Forbidden Nationality"/> -->
		<fact id="Exists"><invalidate path="Rules/RuleNeedPassport"/></fact>		
		<fact id="Visible" editable="true"><invalidate path="Rules/RuleNeedPassport"/></fact>
	</paper>
</facts>
```
* id="": Apparently is supposed to deal with Forbidden Nationalities.
* id="Exists": Whether an entrant has the document or not
* id="Visible": Whether an entrant has forgotten to show the document.
* editable: Determines whether this fact is changed by events mid-processing (in this case the entrant remembering their passport).
* invalidate path="": Reference to a fact this discrepancy is connected to.
* 

### Entry Permit
```
<facts>
	<paper id="EntryPermit" desc="Entry Permit">
		<fact id=""/>
		<fact id="Exists">
			<invalidate path="Rules/RuleNeedEntryPermit"/>
			<!-- This allows correlation with rule when carrying ticket instead of required permit -->
			<invalidate path="Rules/RuleNeedEntryTicket"/>
		</fact>
		<fact id="Visible" editable="true"><invalidate path="Rules/RuleNeedEntryPermit"/></fact>
		<fact id="Name" format="FIRST LAST">
			<!--<invalidate path="IdentityRecord/Alias"/>-->
		</fact>
		<fact id="IdNumber"/>
		<fact id="Purpose" format="FORDOC"/>
		<fact id="Duration" format="FORDOC"/>
		<fact id="ExpirationDate" range="10 30"/>
		<fact id="Emblem/MinistryOfAdmission" desc="Forged Entry Permit">
			<invalidate when="NONE" path="Rules/SealRequired"/>
			<invalidate path="Rules/EntryPermitSeals"/>
		</fact>
	</paper>
</facts>
```
* format:
* range:
* invalidate when="NONE": Creates an error if a fact is missing from the document

### Groups
XML section that connects different facts together to enable discrepancy matching.
```
<facts>
	<groups>
		<group id="Appearance">
			<path val="Passport/Gender"/>
			<path val=".*/Face"/>
		</group>
```
Demonstrates how to connect entrant appearance to document pictures and gender information, note the `.*/` wildcard to be applicable to all instances of `Face`.
```
		<group id="Name">
			<path val=".*/Name"/>
			<path val="IdentityRecord/Alias"/>
		</group>
```
Ditto, but for names.
```
		<group id="IdNumber">
			<path val="Passport/IdNumber"/>
			<path val="EntryPermit/IdNumber"/>
			<path val="WorkPermit/IdNumber"/>
		</group>
```
Standard connection of information errors, this example being passport numbers.
```
		<group id="IssuingCity[NATION]">
			<path val="Passport/IssuingCity"/>
			<path val="Rules/IssuingCity"/>
			<path val="Rules/[NATION]-IssuingCities"/>
		</group>
		<group id="PassportAppearance[NATION]">
			<path val="Passport"/>
			<path val="Rules/[NATION]-Passport0"/>
		</group>
```
Referencing by fact category, note how `[NATION]` is used here but the fact id in the original documents are defined with `[NATIONS]`
```
		<group id="PaperRequired-EntryPermit">
			<path val="Rules/RuleNeedEntryPermit"/>
			<path val="EntryPermit"/>
			<path val="Booth/Counter"/>
			<!-- This allows correlation with rule when carrying ticket instead of required permit -->
			<path val="EntryTicket"/>
		</group>
	</groups>
</facts>
```
Shows how to make one document outdated to another.

### ModdingExample

Process of implementing a new nation-based emblem:

`Emblems.xml`
```
<emblems>
	<emblem id="SealArstotzka" file="SealArstotzka.png" count="2" valid="1" size="60 60" canrotate="true" />
	<emblem id="SignatureArstotzka" file="SignatureArstotzka.png" count="2" valid="1" size="102 7" canrotate="false" />
</emblems>
```
Add new emblems.

`Facts.xml`
```
<facts>
	<paper id="Rules" stay="true">
		<fact id="[NATIONS]-PassportSeals" val="PassportSeals[NATIONS].png" />
		<fact id="SealRequired" val="RuleSealRequired.png"/>
	</paper>
</facts>
```
Add new rules and the corresponding rule image.

`Papers.xml`
```
<papers>
	<paper id="Passport" nation="Arstotzka" ...>
		<page image="PassportInnerArstotzka.png">
			<mark emblem="SignatureArstotzka" emblemrect="12 168 147 49" />
			<mark emblem="SealArstotzka" emblemrect="12 158 147 59" />
		</page>
	</paper>
</papers>
```
Add emblems to document.

`Facts.xml`
```
<facts>
	<paper id="Passport">
		<fact id="Emblem/Seal[NATIONS]" desc="Forged Passport">
			<invalidate path="Rules/[NATION]-PassportSeals"/>
		</fact>
		<fact id="Emblem/SealArstotzka" desc="Missing Arstotzkan Passport Seal">
			<invalidate when="NONE" path="Rules/Arstotzka-PassportSeals"/>
		</fact>
		<fact id="Emblem/Signature[NATIONS]" desc="Forged Passport">
			<invalidate path="Rules/[NATION]-PassportSeals"/>
		</fact>
		<fact id="Emblem/SignatureArstotzka" desc="Forged Passport">
			<invalidate when="NONE" path="Rules/Arstotzka-PassportSeals"/>
		</fact>
	</paper>

```
Add emblems as facts. Note that each nation needs a separate entry for `invalidate when="NONE"`
```
	<groups>
		<group id="PassportSeal[NATION]">
			<path val="Passport/Emblem/Seal[NATION]" />
			<path val="Rules/[NATION]-PassportSeals" />
			<path val="Passport" />
		</group>
		<group id="PassportSealRequired[NATION]">
			<path val="Passport" />
			<path val="Rules/[NATION]-PassportSeals" />
		</group>
		<group id="PassportSignature[NATION]">
			<path val="Passport/Emblem/Signature[NATION]" />
			<path val="Rules/[NATION]-PassportSeals" />
			<path val="Passport" />
		</group>
		<group id="PassportSignatureRequired[NATION]">
			<path val="Passport" />
			<path val="Rules/[NATION]-PassportSeals" />
		</group>
	</groups>
</facts>
```
Set up discrepancy handling. Note that this successfully connects more than one fact to the same rule.

`Speeches.txt`
```
ask-forgery-passport Passport/Emblem/SealArstotzka
	=NONE *ask-forgery-missing
	*ask-forgery-wrong
ask-signature-missing
	This passport is missing its signature.
	There is no signature here.
	I do not see the required signature here.
ask-signature Passport/Emblem/SignatureArstotzka
	=NONE *ask-signature-missing
	*ask-forgery-wrong
```
Add dialogue.

`Errors.txt`
```
Passport-WrongSeal<forgery>
	\ Passport
	! Passport/Emblem/SealArstotzka
		> $Interrogate:Forgery passport
Passport-WrongSignature<forgery>
	\ Passport
	! Passport/Emblem/SignatureArstotzka
		> Interrogate
			" ask-signature
			" forgery
			@ Detain
```
Add dialogue/action handling for error.
