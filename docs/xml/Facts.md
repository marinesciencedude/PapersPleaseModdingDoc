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
		< district val=""/>
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
<facts 
	<paper id="Rules" stay="true">
		<fact id="" val=""/>
		
		<fact id="[NATIONS]-Passport0" val="PassportOuter[NATIONS].png"/>
		<fact id="[NATIONS]-IssuingCities" val="[ISSUINGCITIES]"/>

		<fact id="Arstotzka-Districts" val="[DISTRICTS]"/>
	</paper>
</facts>
```
