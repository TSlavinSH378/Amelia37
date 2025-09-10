-   [Simple Datum Types](#AppendixC:DatumTypes-SimpleDatumTypes)
    -   [Person Datum](#AppendixC:DatumTypes-PersonDatum)
    -   [Ordinal Datum](#AppendixC:DatumTypes-OrdinalDatum)
    -   [Date Datum](#AppendixC:DatumTypes-DateDatum)
    -   [Time Datum](#AppendixC:DatumTypes-TimeDatum)
    -   [DateTime Datum](#AppendixC:DatumTypes-DateTimeDatum)
-   [Unit Datum Types](#AppendixC:DatumTypes-UnitDatumTypes)
    -   [Weight Datum](#AppendixC:DatumTypes-WeightDatum)
    -   [Temperature Datum](#AppendixC:DatumTypes-TemperatureDatum)
    -   [Area Datum](#AppendixC:DatumTypes-AreaDatum)
    -   [Length Datum](#AppendixC:DatumTypes-LengthDatum)
    -   [REPLACE Datum](#AppendixC:DatumTypes-REPLACEDatum)
    -   [Speed Datum](#AppendixC:DatumTypes-SpeedDatum)
    -   [Volume Datum](#AppendixC:DatumTypes-VolumeDatum)
    -   [Age Datum](#AppendixC:DatumTypes-AgeDatum)
    -   [Duration Datum](#AppendixC:DatumTypes-DurationDatum)
    -   [Currency Datum](#AppendixC:DatumTypes-CurrencyDatum)
    -   [Percentage Datum](#AppendixC:DatumTypes-PercentageDatum)
-   [Location Datum Types](#AppendixC:DatumTypes-LocationDatumTypes)
    -   [Airport](#AppendixC:DatumTypes-Airport)
    -   [Capital](#AppendixC:DatumTypes-Capital)
    -   [Country](#AppendixC:DatumTypes-Country)
    -   [US City](#AppendixC:DatumTypes-USCity)
    -   [US County](#AppendixC:DatumTypes-USCounty)
    -   [US State](#AppendixC:DatumTypes-USState)
    -   [US Street Address](#AppendixC:DatumTypes-USStreetAddress)
    -   [US Zipcode](#AppendixC:DatumTypes-USZipcode)
    -   [Province](#AppendixC:DatumTypes-Province)
    -   [Prefecture](#AppendixC:DatumTypes-Prefecture)
-   [Range Datum Types](#AppendixC:DatumTypes-RangeDatumTypes)
    -   [Simple Range Datum Types](#AppendixC:DatumTypes-SimpleRangeDatumTypes)
        -   [Date Range](#AppendixC:DatumTypes-DateRange)
        -   [Date Time Range](#AppendixC:DatumTypes-DateTimeRange)
        -   [Decimal Range](#AppendixC:DatumTypes-DecimalRange)
        -   [Integer Range](#AppendixC:DatumTypes-IntegerRange)
        -   [Ordinal Range](#AppendixC:DatumTypes-OrdinalRange)
        -   [Time Range](#AppendixC:DatumTypes-TimeRange)
    -   [Unit Range Datum Types](#AppendixC:DatumTypes-UnitRangeDatumTypes)
        -   [Age Range](#AppendixC:DatumTypes-AgeRange)
        -   [Area Range](#AppendixC:DatumTypes-AreaRange)
        -   [Currency Range](#AppendixC:DatumTypes-CurrencyRange)
        -   [Duration Range](#AppendixC:DatumTypes-DurationRange)
        -   [Length Range](#AppendixC:DatumTypes-LengthRange)
        -   [Percentage Range](#AppendixC:DatumTypes-PercentageRange)
        -   [Speed Range](#AppendixC:DatumTypes-SpeedRange)
        -   [Temperature Range](#AppendixC:DatumTypes-TemperatureRange)
        -   [Volume Range](#AppendixC:DatumTypes-VolumeRange)
        -   [Weight Range](#AppendixC:DatumTypes-WeightRange)
-   [Custom Datum](#AppendixC:DatumTypes-CustomDatum)
-   [Extracting Datum Types](#AppendixC:DatumTypes-ExtractingDatumTypes)
-   [Datum Decorators](#AppendixC:DatumTypes-DatumDecorators)
    -   [SingleDatumDecorator](#AppendixC:DatumTypes-SingleDatumDecorator)
    -   [RangeDatumDecorator](#AppendixC:DatumTypes-RangeDatumDecorator)
    -   [CustomDatumDecorator](#AppendixC:DatumTypes-CustomDatumDecorator)
-   [Range Decorator](#AppendixC:DatumTypes-RangeDecorator)
-   [Extractable Datums](#AppendixC:DatumTypes-ExtractableDatums)
Datums are tools for extracting valuable input values from natural language inputs. Each defined Slot has an assigned datum type unless the slot being defined is a custom type for which a Custom Datum type would be used composed of datums of type Custom Datum Field. Datums are pre built entities for facilitating the handling of most popular common concepts.
When working with the code,
-   A** Datum Registry** has been defined for getting an instance of the Datum of required type.
-   **Normalizers** are defined for each datum type. The purpose of a Normalizer is to interpret the input string identified from a conversation, create a Datum type of the said Slot type, extract meaningful information and assign to the Datum object.  
    Example: Two hundred and thirty two kgs is saved as 232 kilograms in the Weight Datum type.
-   **Formatters** are defined per datum type to export the value of the Datum as required by the scenario. See [Appendix D: Formatters](Appendix%20D_%20Formatters) for more details.  
    Example: Dates can be formatted as full date, short date, zoned date.
Following is a short overview of all the available datum types classified by type.
-   **Simple**: Simple Datum types can be best understood by comparing with the basic types available in most programming languages. In addition to the types like Boolean, Integer and Decimal, datum types representing other simple indivisible datum types are also included in this category.
-   **Location**: Location datum types are as the name suggests Datum types that represent location related information. All the datums of location type include Geolocation information and support geolocation related operations.
-   **Unit**: Datums of types that contain a unit for identifying the type of information are included in this category. The types of units per category including the symbols and conversion values are stored in the respective types by name.
-   **Ranges**: Datums representing ranges belong to two main categories, ranges of simple types and ranges of unit types. A range datum is a datum with two values at maximum and one at minimum. A range with two values is closed and ranges with only one value (either start or end) is open ended. All ranges are closed.
-   **Custom**: In scenarios where a Datum is required which does not fit by the given Datum types or cases where a Datum is being created dynamically, a Custom Datum is created. A custom datum is composed of custom datum field types. A custom Datum field is an identifiable individual dynamically created Datum.
All the datum types are explained further in this appendix. The table below displays a categorized list of available datum types.
Table. Available Datum Types
<table class="relative-table wrapped confluenceTable" style="width: 64.1554%;">
<colgroup>
<col style="width: 17%" />
<col style="width: 14%" />
<col style="width: 15%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 18%" />
</colgroup>
<tbody>
<tr class="odd">
<td colspan="6" class="confluenceTd" style="text-align: center;"><p>DATUM</p></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: center;"><p><strong>CUSTOM</strong></p></td>
<td class="confluenceTd" style="text-align: center;"><p><strong>LOCATION</strong></p></td>
<td colspan="2" class="confluenceTd" style="text-align: center;"><p><strong>RANGE</strong></p></td>
<td class="confluenceTd" style="text-align: center;"><p><strong>SIMPLE</strong></p></td>
<td class="confluenceTd" style="text-align: center;"><p><strong>UNIT</strong></p></td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: center;"><p><strong> </strong></p></td>
<td class="confluenceTd" style="text-align: center;"><p><strong> </strong></p></td>
<td class="confluenceTd" style="text-align: center;"><p><strong>SIMPLE</strong></p></td>
<td class="confluenceTd" style="text-align: center;"><p><strong>UNIT</strong></p></td>
<td class="confluenceTd" style="text-align: center;"><p><strong> </strong></p></td>
<td class="confluenceTd" style="text-align: center;"><p><strong> </strong></p></td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: center;">Custom Datum Field</td>
<td class="confluenceTd" style="text-align: center;">Airport</td>
<td class="confluenceTd" style="text-align: center;">Date Range</td>
<td class="confluenceTd" style="text-align: center;">Age Range</td>
<td class="confluenceTd" style="text-align: center;">Boolean</td>
<td class="confluenceTd" style="text-align: center;">Age</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: center;">Custom Datum</td>
<td class="confluenceTd" style="text-align: center;">Capital</td>
<td class="confluenceTd" style="text-align: center;">Decimal Range</td>
<td class="confluenceTd" style="text-align: center;">Area Range</td>
<td class="confluenceTd" style="text-align: center;">Date</td>
<td class="confluenceTd" style="text-align: center;">Area</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Country</td>
<td class="confluenceTd" style="text-align: center;">Integer Range</td>
<td class="confluenceTd" style="text-align: center;">Currency Range</td>
<td class="confluenceTd" style="text-align: center;">Date-Time</td>
<td class="confluenceTd" style="text-align: center;">Currency</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">US City</td>
<td class="confluenceTd" style="text-align: center;">Ordinal Range</td>
<td class="confluenceTd" style="text-align: center;">DurationRange</td>
<td class="confluenceTd" style="text-align: center;">Decimal</td>
<td class="confluenceTd" style="text-align: center;">Duration</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">US County</td>
<td class="confluenceTd" style="text-align: center;">Time Range</td>
<td class="confluenceTd" style="text-align: center;">Length Range</td>
<td class="confluenceTd" style="text-align: center;">Email</td>
<td class="confluenceTd" style="text-align: center;">Length</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">US State</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Percentage Range</td>
<td class="confluenceTd" style="text-align: center;">Integer</td>
<td class="confluenceTd" style="text-align: center;">Percentage</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">US Street Address</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Speed Range</td>
<td class="confluenceTd" style="text-align: center;">Ordinal</td>
<td class="confluenceTd" style="text-align: center;">Speed</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">US Zipcode</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Temperature Range</td>
<td class="confluenceTd" style="text-align: center;">Organization</td>
<td class="confluenceTd" style="text-align: center;">Temperature</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Province</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Volume Range</td>
<td class="confluenceTd" style="text-align: center;">Person</td>
<td class="confluenceTd" style="text-align: center;">Volume</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Prefecture (Japan)</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Weight Range</td>
<td class="confluenceTd" style="text-align: center;">Text</td>
<td class="confluenceTd" style="text-align: center;">Weight</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Time</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">US Phone Number</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">IBAN (for non-US locales)</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Nationality</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Occupation</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
</tr>
<tr class="odd">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Month/Year</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
</tr>
<tr class="even">
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
<td class="confluenceTd" style="text-align: center;">Response</td>
<td class="confluenceTd" style="text-align: center;"><br />
</td>
</tr>
</tbody>
</table>
# Simple Datum Types
Simple datum types can be best understood by comparing them to the primitive data types available in most programming languages. Examples would be the types Boolean, Decimal, Integer and Text. 
The other datums categorized in this section are Person, Ordinal, US Phone Number, Date, Time and Date-time. Each of these are explained below.
## Person Datum
The Person datum as the name would suggest is meant for storing the name related information of a person. It supports the presence of prefix, suffix as well as composite middle and last names.
Person is a special case since value in the Person datum object is another object that contains the details of the person name; prefix, first name, middle name, last name.
One can get the datum, call the value method on the datum and then get the desired parameter by its name.
One can check and retrieve specific values from the PersonDatum using the following methods:
-   hasFirstName(): Returns true if first name exists for the datum
-   firstName(): Returns the first name of the datum
-   hasMiddleName(): Returns true if middle name exists for the datum
-   middleName(): Returns the middle name of the datum
-   hasLastName(): Returns true if last name exists for the datum
-   lastName(): Returns the last name of the datum
Example:
``` java
def personDatum = contextService.latestSlot('person_name');
if (personDatum.hasMiddleName()) {
    String middleName = personDatum.middleName();
}
```
## Ordinal Datum
Ordinal datum is a special case from the Integer Datum for storing rank related information. Common examples of ordinals would be 5th and seventeenth.
## Date Datum
Date Datum stores dates and accepts various inputs to normalize into a date datum. A few examples would be:
-   12/01/2012 10:10:53
-   1232/12/201322
-   12/12/2012
-   2017/02/20 10:30 AM
-   today at 3 pm
-   tomorrow
-   next Friday
-   Three days from now
-   five days from today
-   now
-   march 5 2017
-   the beginning of the year
## Time Datum
The Time Datum in a similar manner as Date datum can accept a variety of inputs to normalize and create a time datum. A few examples of Time datum would be:
-   10:10:10 AM
-   9:10:10 PM
-   10 pm
-   around 3 pm
-   up to 9 am
-   up to nine am
-   at one pm
-   4 hours after 6 pm
-   03/02/2017 10:30 pm
-   9:10:10 hrs
-   18:10:10 hrs**  
    **
-   at 10 pm
## DateTime Datum
The purpose of the type DateTime Datum is for the times a data type is required to store both date and time related information. A few examples would be:
-   03/02/2017 10:30 pm
-   Today at 6 pm
**US Phone Number Datum** checks for the valid phone number and then saves the provided phone number input.
The following table provides an overview of all types in this category along with examples and formatted outputs. See [Appendix D: Formatters](Appendix%20D_%20Formatters) for details about formatters.
Table. Date/Time Datum Types

| Datum name | Internal Name | Description | Examples | Internal type of stored value |
| ----|----|----|----|----|
| Boolean | BOOLEAN | Matches a boolean value. | true/false | value stored as Boolean type |
| Date | DATE | Matches a date value | Wednesday, December 12 2012 | value stored as LocalDate |
|  |  |  | Friday, March 2, 1990 |  |
|  |  |  | March 2, 1990 |  |
|  |  |  | Mar 2, 1990 |  |
|  |  |  | 11/21/11 |  |
|  |  |  | 02/16/2016 |  |
| Date Time | DATE_TIME | Matches a value with date and time | 2012/12/01 2:10:53 AM | value stored as ZonedDateTime |
|  |  |  | ;Sat, 1 Dec 2012 16:10:53 -0500 |  |
|  |  |  | ;2012/12/01 11:10:53 PM EST |  |
| Decimal | DECIMAL | Matches a decimal number | 3.14 | value stored as BigDecimal |
| Email | EMAIL | Matches a email value | test.email@ipsoft.com | value stored as String |
| Integer | INTEGER | Matcher a integer value | 150 | value stored as Long |
|  |  |  | Two hundred and thirty |  |
| Ordinal | ORDINAL | Matches a ordinal value | 5th | value stored as Long |
|  |  |  | First |  |
| Organization | ORGANIZATION | Matches a string value representing an organization | Ipsoft Inc | value stored as String |
| Person | PERSON | Matches a Person name | Mr. James Arthur Gosling | value stored as PersonName type |
|  |  |  | James Gosling |  |
|  |  |  | James |  |
| Text | TEXT | Matches a text value | Hello World | value stoed as String |
| Time | TIME | Matches a time value | 10:20:50 PM | value stored as LocalTime |
|  |  |  | 22:20:50 |  |
| US Phone Number | PHONE_NUMBER | Matches a US phone number | 6177491234 | value stored as String |
| IBAN (for non-US locales) | IBAN | Matches a valid IBAN number | GB82 WEST 1234 5698 7654 32 | value stored as String |
| Nationality | NATIONALITY | Matches nationalities | Français, Anglais | value stored as String |
| Occupation | OCCUPATION | Matches occupations | Pharmacien, comptable | value stored as String |
| Month/Year | YEAR_MONTH | Matches dates in a month/year format, such as for credit card numbers (e.g. mm/yy). Assumes mm/yy instead of mm/dd. | 6/23, 6 2023 | value stored as;YearMonth |
| Response | RESPONSE | Extract the user's complete response to an ask in a BPN. Returns a TEXT datum | Amelia: Any comments you would like to add?User:;Thank you for being such a great listener! | value stored as String |

# Unit Datum Types
Datums which are associated with a unit are classified under the Unit Datum types category. 
It has to be noted during the creation of these types of Datums that the selection of the unit type is mandatory.
Both, imperial as well as metric types of units are supported and can be used interchangeably. This is not recommended but if the need arises, the module is capable of handling the said scenario as well.
All the formatters for this type would return the value in two forms; one with numeric value followed by the unit and the other with the numeric value in words followed by the unit. See [Appendix D: Formatters](Appendix%20D_%20Formatters) for details about formatters.
The following table lists the datum types, the supported units and a couple of examples to illustrate the use.
Table. Unit Datum Types

| Datum name | Supported Units | Examples |
| ----|----|----|
| Weight Datum | GrainOuncePoundShort TonLong TonMilligramGramsKilogramTonne | 100 KG20 pounds2 tonne |
| Temperature Datum | CelsiusFahrenheit | 100 degree celsius70.0 °C |
| Area Datum | Square_millimetersSquare_centimetersSquare_metersSquare_kilometersHectareSquare_inchesSquare_feetSquare_milesSquare_yardsAcre | 100 sq km2.5 square centimeters5 hectare |
| Length Datum | MillimetersCentimetersMetersKilometersMilesYardsInchesFeetNautical MilesLight YearsParsec | 100 cm20.5 meteRS200 miles6 nautical miles |
| REPLACE Datum | N/A | Accepts any response from a user in response to a corresponding Ask task for an entity with this datum type. This can be a useful way to pass along user input without normalization or other service or API interaction.An entity set to datum type RESPONSE would capture the user statement “I would like to add 300gb” in response to an Ask task, “How much storage do you want to add?” |
| Speed Datum | Meters per secondKilometers per secondMeter per minuteKilometers per hourMeters per hourKilometer per minuteSpeed of LightFeet per hourFeet per minuteFeet per secondMiles per hourMiles per secondMile per minuteKnots | 100 km/hr20 m/s2.5 miles/hr200 miles per hour |
| Volume Datum | Cubic CentimetersCubic MetersCubic KilometersMilliliterLiterCubic InchesCubic FeetCubic MilesCubic YardsOunceGallonAcre Foot | 100 cubic centimeter2 cu km200 liters40.5 oz20 cu yards |
| Age Datum | DecadeYearFiscalMonthQuarterDayHoursMinutesSecondsMilliseconds | 100 days20 months2.5 years1 year 6 months |
| Duration Datum | DecadeYearFiscalMonthQuarterDayHoursMinutesSecondsMilliseconds | 1 yr5 QUARTER20 hrs2 ms1 fiscal |
| Currency Datum | Currency symbolsCurrency names | $500¥1000€200£700?5500dollar 200 |
| Percentage Datum | PercentagePercentile | 100 percentage20%1 percentile50 percent3.1415926535897932384626433832795028841971693993751058209749% |

In addition to information above, the following table provides a description of more internal details of the working of the Unit Datums.
Table. Details about Unit Datum Types

| Datum name | Internal Name | Description | Internal type of stored value
 |
| ----|----|----|----|
| Age | AGE | Matches an age unit type | value stored as BigDecimal |
| Area | AREA | Matches an area unit type | value stored as BigDecimal |
| Currency | CURRENCY | Matches a currency unit type | value stored as BigDecimal |
| Duration | DURATION | Matches a duration | value stored as Long |
| Length | LENGTH | Matches a length unit type | value stored as BigDecimal |
| Percentage | PERCENTAGE | Matches a percentage unit type | value stored as BigDecimal |
| Speed | SPEED | Matches a speed unit type | value stored as BigDecimal |
| Temperature | TEMPERATURE | Matches a temperature unit type | value stored as BigDecimal |
| Volume | VOLUME | Matches a volume unit type | value stored as BigDecimal |
| Weight | WEIGHT | Matches a weight unit type | value stored as BigDecimal |

# Location Datum Types
Location datum types as the name would suggest are datums which contain location related information. Each datum in this category is associated with a geolocation parameter that contains the latitude and longitude related information.
These datums also support geolocation related operations like validating if the location passed is valid or finding the distance between two geolocations.
All the formatters for this type return the value of the location as was passed originally as input. See [Appendix D: Formatters](Appendix%20D_%20Formatters) for details about formatters.
The following table lists the datums available in this category. 
Table. Location Datum Types

| Datum name | Internal Name | Description | Examples | Internal type of stored value
 |
| ----|----|----|----|----|
| Airport | AIRPORT | Matches a value representing an airport | Newark International Airport | value stored as a String |
|  |  |  | EWR |  |
| Capital | CAPITAL | Matches a value representing a capital | New Delhi | value stored as a String |
| Country | COUNTRY | Matches a value representing a country | Mexico | value stored as a String |
|  |  |  | IND |  |
| US City | US_CITY | Matches a value representing a city name | Boston | value stored as a String |
| US County | US_COUNTRY | Matches a value representing a county name | Suffolk | value stored as a String |
| US State | US_STATE | Matches a value representing the name of a state | New Jersey | value stored as a String |
|  |  |  | MA |  |
| US Street Address | US_STREET_ADDRESS | Matches a value representing street address details | 17 State Street | value stored as a String |
| US Zipcode | US_ZIPCODE | Matches a value representing a zipcode | 10004 | value stored as a String |
| Province | PROVINCE | Matches Provinces/Territories | Cáceres, Zamora, Ontario, Champagne | value stored as a String |
| Prefecture | PREFECTURE (Japan) | Matches a value representing the name of a prefecture in Japan. Only for Japanese language pack as of Amelia 3.7.26+. | 東京都 | value stored as a String |

> [!warning]  
>
> Please make sure that the input provided to the Datums defined are valid. The inputs are validated and confirmed to be true before creating the Location Datum and storing it.

# Range Datum Types
Ranges can be open ended or closed. If both values are provided to the range, it would act as a closed range else it would act as an open range; either a closed open or an open closed range.
Table. Range Datum Types

| Range type | Meaning | Example |
| ----|----|----|
| Closed | Both values of the range are provided | From 30° C to 40° C |
| Open closed | Only the end value of the range is provided | Until 30th of October 2019 |
| Closed open | Only the starting value of the range is provided | Starting 10 AM CST |

All ranges include the start and the end value as part of the range.
It is important that you provide a valid range to create and store a Range Datum.
## Simple Range Datum Types
The simple range datum types use the Simple Datum types explained in [Simple Datum Types](#AppendixC:DatumTypes-SimpleDatumTypes) above.
The following table provides a high level overview of all the available Simple Range Datum with related information.
Table. Simple Range Datum Types

| Datum name | Internal Name | Description | Examples | Internal type of stored value
 |
| ----|----|----|----|----|
| Date Range | DATE_RANGE | Matches a range of two Date Datum values | Examples listed after the table | value stored as Guava Range |
| Date Time Range | DATE_TIME_RANGE | Matches a range of two DateTime Datum values | I want wifi from tomorrow at 10 AM until next Friday at midnight. | value stored as Guava Range |
| Decimal Range | DECIMAL_RANGE | Matches a range of two Decimal Datum values | from 2010.5between 15.20 and 117.65from 100.70 to 107.23568 | value stored as Guava Range |
| Integer Range | INTEGER_RANGE | Matches a range of two Integer Datum values | from 2010BETWEEN 15 and 117to 2500to two hundredfrom one hundred two to two hundred thirty three | value stored as Guava Range |
| Ordinal Range | ORDINAL_RANGE | Matches a range of two Ordinal Datum values | from 5thfrom three hundred and firstto seventeenthbetween two thousand two hundred thirty second and ten thousand first | value stored as Guava Range |
| Time Range | TIME_RANGE | Matches a range of two Time Datum values | Examples listed after the table | value stored as Guava Range |

More examples:
**Time Range:**
-   from 10 pm
-   starting 10:25 pm
-   after 10:25:10 pm
-   to 10 pm
-   before 10 pm
-   up until 10:25 pm
-   ending 10:25:10 pm
-   from ten pm
-   from eleven thirty five pm
-   to ten pm
-   ending eleven thirty five pm
-   between 10:30 pm and 11 pm
-   ending eleven thirty five pm
-   between ten thirty pm and eleven pm
-   4 hours after 6 pm
-   from 2 pm to 5 pm
-   from two pm to five pm
-   from two thirty five pm to five fifty six pm
-   from two am to five pm
**Date Range**
-   I want wifi today and tomorrow
-   I want wifi tomorrow
-   By the end of day
-   I need wifi in a day
-   for the day
-   for next 131 days
-   for the next eleven days
-   I want wifi next Sunday
-   I need wifi in a week
-   for the next 14 weeks
-   for second week of April
-   until the end of month
-   nine years from now
## Unit Range Datum Types
Similar to Simple Range Datums, the Unit Range Datum types consist of two UnitDatum objects, one for start and one for end.
The following table provides a high level overview of all the available Simple Range Datum with related information.
Table. Unit Range Datum Types

| Datum name | Internal Name | Description | Examples | Internal type of stored value
 |
| ----|----|----|----|----|
| Age Range | AGE_RANGE | Matches a range of two Age Datum values | from ages 10 to 20 | value stored as Guava Range |
| Area Range | AREA_RANGE | Matches a range of two Area Datum values | from 200.98 sq metersto 100.70 acrebetween 80.40 sq meters and 100 sq metersuntil 100.70 hectarefrom one hundred sq m to two hundred sq mbetween three hundred sq m and five hundred sq m | value stored as Guava Range |
| Currency Range | CURRENCY_RANGE | Matches a range of two Currency Datum values | from $100 to $200 | value stored as Guava Range |
| Duration Range | DURATION_RANGE | Matches a range of two Duration Datum values | between 100 days and 200 days | value stored as Guava Range |
| Length Range | LENGTH_RANGE | Matches a range of two Length Datum values | from 76 cmsstarting 32.88 milesto 877 cmsat most 12.77 milesBETWEEN 90.88 km and 350 miles | value stored as Guava Range |
| Percentage Range | PERCENTAGE_RANGE | Matches a range of two Percentage Datum values | from 50.65%to 70.50 %between 80 percent and 90 percentageuntil 56.70 percentile | value stored as Guava Range |
| Speed Range | SPEED_RANGE | Matches a range of two Speed Datum values | from 100 meter per secondstarting 30.60 m/sto 100 km/hrat most 30.60 miles per hourBETWEEN 30.60 km/s and 50 m/s | value stored as Guava Range |
| Temperature Range | TEMPERATURE_RANGE | Matches a range of two Temperature Datum values | from 70°Cto 100.70 degree celsiusbetween 5 degree celsius and 100 degree fahrenheituntil 100.70 f | value stored as Guava Range |
| Volume Range | VOLUME_RANGE | Matches a range of two Volume Datum values | from 320.18 cu metersto 90.30 ouncebetween 20.10 cu cm and 500 cu cmuntil 983.76 gallon | value stored as Guava Range |
| Weight Range | WEIGHT_RANGE | Matches a range of two Weight Datum values | from 200.98 mgto 100.70 ozbetween 80.40 kilogram and 100 kguntil 100.70 tonne | value stored as Guava Range |

# Custom Datum
These are datums types that are created on the fly in order to facilitate creation of a datum type that does not fit in any of the pre defined datum types. A custom datum is composed of multiple Custom Datum Field type datums.
For all the cases where the pre defined Datums are not the best choice, one would create a Custom datum 
A custom datum cannot exist on its own. It requires a container which is defined as a Composite Datum.
The composite datum should contain at least one Custom Datum of a type belonging to one of the pre defined datum types.
There is no upper limit for the custom datum that the composite can hold.
# Extracting Datum Types
The datums returned to the script/navigational tasks would contain two fields; namely datum type and value.
The datum type as the name suggests, would describe the type of the datum and the value would contain the normalized value for the Datum.
There are multiple ways of extracting the value for the Datum, one acquired.
One can call the value() function on the Datum object which would return the stored object.
In the cases of units, there would be three values in the datum object returned; datum type, value object and the unit.
A range datum object does not contain a value() method, instead there are two methods, start() and end() which return the respective datum objects on which one can call the value() method.
# Datum Decorators
As the names suggest, the decorator classes encapsulate the datum objects and expose the methods to retrieve and return only the required Datum information.
All the Datum Decorator objects expose the following methods:

| label |
| ----|
| String label()

**Return:**
Human readable label, e.g., for an SSN, the label will be "Social security number".
\|

| datumType |
| ----|
| String datumType()

**Return:**
Defines the type of the Datum. E.g. for an SSN, the DatumType is SSN_DATUM.
\|

| text |
| ----|
| String text()

**Return:**
Returns the raw String input received by Amelia.
\|
Three decorators exist for the three types of Datum; SingleDatumDecorator, RangeDatumDecorator and CustomDatumDecorator
The additional methods exposed by each of these Decorators in addition to the above mentioned methods are:
## **SingleDatumDecorator**
Encapsulates an AbstractSingleDatum object
Additional methods exposed:

| unit |
| ----|
| String unit()

**Return:**
In cases of Unit based Datum objects, this would return the unit in String.The method will return null if the Datum is not a UnitDatum and this method is called.
\|

| value |
| ----|
| Object value()

**Return:**
Returns the normalized value of the Datum.
\|
## RangeDatumDecorator
Encapsulats an AbstractRangeDatum object
Additional methods exposed:

| unit |
| ----|
| String unit()

**Return:**
In cases of Unit based Datum objects, this would return the unit in String.The method will return null if the Datum is not a RangeUnitDatum and this method is called.
\|

| start |
| ----|
| String start()

**Return:**
Returns the SingleDatumDecorator object that represents the start of the range
\|

| end |
| ----|
| String end()

**Return:**
Returns the SingleDatumDecorator object that represents the end of the range
\|

| value |
| ----|
| RangeDecorator value()

**Return:**
Returns a RangeDecorator object that holds the range parameters.
\|
## CustomDatumDecorator
Encapsulates a CustomDatum object

| value |
| ----|
| List<AbstractSingleDatum> value()

**Return:**
Returns the list of AbstractSingleDatum which represent the individual CustomDatumField objects.
\|
# Range Decorator
Range Decorator is a utility class that wraps around the Guava Range. It is the data type of the object held by a AbstractRangeDatum now.
It exposes the methods start() and end() to return the AbstractSingleDatum objects that represent the range limits.
Also exposed are the following methods:
-   boolean hasLowerBound(): Checks if the range has a start value
-   boolean hasUpperBound(): Checks if the range has an end value
-   boolean contains(T value): Checks if the range contains the value passed
-   boolean containsAll(Iterable\<T\> values): Checks if the range contains all the values passed as a list
# Extractable Datums
Following is the entire list of extactable datums:
-   BOOLEAN
-   INTEGER
-   DECIMAL
-   ORDINAL
-   CURRENCY
-   AREA
-   LENGTH
-   VOLUME
-   WEIGHT
-   SPEED
-   PERCENTAGE
-   TEMPERATURE
-   DURATION
-   AGE
-   EMAIL
-   PERSON
-   ORGANIZATION
-   DATE
-   TIME
-   DATE_TIME
-   DATE_RANGE
-   DATE_TIME_RANGE
-   DECIMAL_RANGE
-   INTEGER_RANGE
-   ORDINAL_RANGE
-   TIME_RANGE
-   AGE_RANGE
-   AREA_RANGE
-   CURRENCY_RANGE
-   DURATION_RANGE
-   LENGTH_RANGE
-   PERCENTAGE_RANGE
-   SPEED_RANGE
-   TEMPERATURE_RANGE
-   VOLUME_RANGE
-   WEIGHT_RANGE
-   AIRPORT
-   PHONE_NUMBER
-   US_ZIPCODE
-   CAPITAL
-   COUNTRY
-   US_CITY
-   US_STATE
-   US_COUNTY
-   US_STREET_ADDRESS
