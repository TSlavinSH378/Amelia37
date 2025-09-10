The BpnQuantityService normalizes and formats date references and quantity data included in user utterances during conversations with Amelia. For example, a user might say ‘day after tomorrow’ or ‘next week’ and this service will convert those phrases to specific dates with the user’s local timezone.
The quantity service enables one to do the following:
-   Get an already extracted datum using the slot code
-   Normalize a string and get a Datum object populated with the value
-   Normalize a string and get a formatted value from the normalized datum 
-   Format the value stored in a Datum object using the default formatter
-   Format the value stored in a Datum object with the formatter one passes as an argument.
For BPNs with tasks that use the Quantity Service, performance and results might be improved by turning off context switching in the Properties Panel of an Ask task. Specifically, setting the "If imperative allow others to respond," "If interrogative allow others to respond," and "If declarative allow others to respond" settings to No.
# Methods
## getExtractedDatum
    getExtractedDatum(String slotCode)
Pass the name of the slot to extract the Datum of the slot. The method will get the latest slot instance of the slot and retrieve the stored Datum from the slot instance.
Table. BpnQuantityService getExtractedDatum Parameters/Definitions

| Parameter | Definition |
| ----|----|
| slotCode | Slot name |

## normalize
normalize(String text, DatumType.\<datum type\>)
Table. BpnQuantityService normal Parameters/Definitions

| Parameter | Definition |
| ----|----|
| text | Sentence, word, or token |
| DatumType | Datum type |

## normalizeAndFormat
    normalizeAndFormat(String text, DatumType.<datum type>, Formatters.<formatter>)
Table. BpnQuantityService normalizeAndFormat Parameters/Definitions

| Parameter | Definition |
| ----|----|
| text | Sentence, word, or token |
| DatumType | Datum type |
| Formatters | Formatter |

## format
    format(AbstractDatum datum)
Table. BpnQuantityService format Parameters/Definitions

| Parameter | Definition |
| ----|----|
| datum | Datum |

## format
    format(AbstractDatum datum, Formatter formatter)
Table. BpnQuantityService format Parameters/Definitions

| Parameter | Definition |
| ----|----|
| DatumType | Datum type |
| Formatters | Formatter |

# Datum Types
These datum types can be passed as a parameter to the methods described above. See [Appendix A: Datum Types and Formatters](#) for details.
## Simple Datum
-   DatumType.TEXT
-   DatumType.BOOLEAN
-   DatumType.INTEGER
-   DatumType.DECIMAL
-   DatumType.ORDINAL
-   DatumType.AGE
-   DatumType.EMAIL
-   DatumType.PERSON
-   DatumType.ORGANIZATION
-   DatumType.DATE
-   DatumType.TIME
## Unit Datum
-   DatumType.CURRENCY
-   DatumType.DURATION
-   DatumType.AGE
-   DatumType.AREA
-   DatumType.LENGTH
-   DatumType.VOLUME
-   DatumType.WEIGHT
-   DatumType.SPEED
-   DatumType.PERCENTAGE
-   DatumType.TEMPERATURE
## Location Datum
-   DatumType.AIRPORT
-   DatumType.US_PHONE_NUMBER
-   DatumType.US_ZIPCODE
-   DatumType.CAPITAL
-   DatumType.COUNTRY
-   DatumType.US_CITY
-   DatumType.US_STATE
-   DatumType.US_COUNTY
-   DatumType.US_STREET_ADDRESS
## Range Datum
-   DatumType.DATE_TIME
-   DatumType.DATE_RANGE
-   DatumType.DATE_TIME_RANGE
-   DatumType.DECIMAL_RANGE
-   DatumType.INTEGER_RANGE
-   DatumType.ORDINAL_RANGE
-   DatumType.TIME_RANGE
-   DatumType.AGE_RANGE
-   DatumType.AREA_RANGE
-   DatumType.CURRENCY_RANGE
-   DatumType.DURATION_RANGE
-   DatumType.LENGTH_RANGE
-   DatumType.PERCENTAGE_RANGE
-   DatumType.SPEED_RANGE
-   DatumType.TEMPERATURE_RANGE
-   DatumType.VOLUME_RANGE
-   DatumType.WEIGHT_RANGE
## Composite Datum
-   DatumType.COMPOSITE
-   DatumType.CUSTOM_DATUM
# Time Zones
-   TimeZones.ETC_GMT_PLUS_12
-   TimeZones.ETC_GMT_PLUS_11
-   TimeZones.MIT
-   TimeZones.PACIFIC_APIA
-   TimeZones.PACIFIC_MIDWAY
-   TimeZones.PACIFIC_NIUE
-   TimeZones.PACIFIC_PAGO_PAGO
-   TimeZones.PACIFIC_SAMOA
-   TimeZones.US_SAMOA
-   TimeZones.AMERICA_ADAK
-   TimeZones.AMERICA_ATKA
-   TimeZones.ETC_GMT_PLUS_10
-   TimeZones.HST
-   TimeZones.PACIFIC_FAKAOFO
-   TimeZones.PACIFIC_HONOLULU
-   TimeZones.PACIFIC_JOHNSTON
-   TimeZones.PACIFIC_RAROTONGA
-   TimeZones.PACIFIC_TAHITI
-   TimeZones.SYSTEMV_HST10
-   TimeZones.US_ALEUTIAN
-   TimeZones.US_HAWAII
-   TimeZones.PACIFIC_MARQUESAS
-   TimeZones.AST
-   TimeZones.AMERICA_ANCHORAGE
-   TimeZones.AMERICA_JUNEAU
-   TimeZones.AMERICA_NOME
-   TimeZones.AMERICA_YAKUTAT
-   TimeZones.ETC_GMT_PLUS_9
-   TimeZones.PACIFIC_GAMBIER
-   TimeZones.SYSTEMV_YST9
-   TimeZones.SYSTEMV_YST9YDT
-   TimeZones.US_ALASKA
-   TimeZones.AMERICA_DAWSON
-   TimeZones.AMERICA_ENSENADA
-   TimeZones.AMERICA_LOS_ANGELES
-   TimeZones.AMERICA_TIJUANA
-   TimeZones.AMERICA_VANCOUVER
-   TimeZones.AMERICA_WHITEHORSE
-   TimeZones.CANADA_PACIFIC
-   TimeZones.CANADA_YUKON
-   TimeZones.ETC_GMT_PLUS_8
-   TimeZones.MEXICO_BAJANORTE
-   TimeZones.PST
-   TimeZones.PST8PDT
-   TimeZones.PACIFIC_PITCAIRN
-   TimeZones.SYSTEMV_PST8
-   TimeZones.SYSTEMV_PST8PDT
-   TimeZones.US_PACIFIC
-   TimeZones.US_PACIFIC_NEW
-   TimeZones.AMERICA_BOISE
-   TimeZones.AMERICA_CAMBRIDGE_BAY
-   TimeZones.AMERICA_CHIHUAHUA
-   TimeZones.AMERICA_DAWSON_CREEK
-   TimeZones.AMERICA_DENVER
-   TimeZones.AMERICA_EDMONTON
-   TimeZones.AMERICA_HERMOSILLO
-   TimeZones.AMERICA_INUVIK
-   TimeZones.AMERICA_MAZATLAN
-   TimeZones.AMERICA_PHOENIX
-   TimeZones.AMERICA_SHIPROCK
-   TimeZones.AMERICA_YELLOWKNIFE
-   TimeZones.CANADA_MOUNTAIN
-   TimeZones.ETC_GMT_PLUS_7
-   TimeZones.MST
-   TimeZones.MST7MDT
-   TimeZones.MEXICO_BAJASUR
-   TimeZones.NAVAJO
-   TimeZones.PNT
-   TimeZones.SYSTEMV_MST7
-   TimeZones.SYSTEMV_MST7MDT
-   TimeZones.US_ARIZONA
-   TimeZones.US_MOUNTAIN
-   TimeZones.AMERICA_BELIZE
-   TimeZones.AMERICA_CANCUN
-   TimeZones.AMERICA_CHICAGO
-   TimeZones.AMERICA_COSTA_RICA
-   TimeZones.AMERICA_EL_SALVADOR
-   TimeZones.AMERICA_GUATEMALA
-   TimeZones.AMERICA_MANAGUA
-   TimeZones.AMERICA_MENOMINEE
-   TimeZones.AMERICA_MERIDA
-   TimeZones.AMERICA_MEXICO_CITY
-   TimeZones.AMERICA_MONTERREY
-   TimeZones.AMERICA_NORTH_DAKOTA_CENTER
-   TimeZones.AMERICA_RAINY_RIVER
-   TimeZones.AMERICA_RANKIN_INLET
-   TimeZones.AMERICA_REGINA
-   TimeZones.AMERICA_SWIFT_CURRENT
-   TimeZones.AMERICA_TEGUCIGALPA
-   TimeZones.AMERICA_WINNIPEG
-   TimeZones.CST
-   TimeZones.CST6CDT
-   TimeZones.CANADA_CENTRAL
-   TimeZones.CANADA_EAST_SASKATCHEWAN
-   TimeZones.CANADA_SASKATCHEWAN
-   TimeZones.CHILE_EASTERISLAND
-   TimeZones.ETC_GMT_PLUS_6
-   TimeZones.MEXICO_GENERAL
-   TimeZones.PACIFIC_EASTER
-   TimeZones.PACIFIC_GALAPAGOS
-   TimeZones.SYSTEMV_CST6
-   TimeZones.SYSTEMV_CST6CDT
-   TimeZones.US_CENTRAL
-   TimeZones.AMERICA_BOGOTA
-   TimeZones.AMERICA_CAYMAN
-   TimeZones.AMERICA_DETROIT
-   TimeZones.AMERICA_EIRUNEPE
-   TimeZones.AMERICA_FORT_WAYNE
-   TimeZones.AMERICA_GRAND_TURK
-   TimeZones.AMERICA_GUAYAQUIL
-   TimeZones.AMERICA_HAVANA
-   TimeZones.AMERICA_INDIANA_INDIANAPOLIS
-   TimeZones.AMERICA_INDIANA_KNOX
-   TimeZones.AMERICA_INDIANA_MARENGO
-   TimeZones.AMERICA_INDIANA_VEVAY
-   TimeZones.AMERICA_INDIANAPOLIS
-   TimeZones.AMERICA_IQALUIT
-   TimeZones.AMERICA_JAMAICA
-   TimeZones.AMERICA_KENTUCKY_LOUISVILLE
-   TimeZones.AMERICA_KENTUCKY_MONTICELLO
-   TimeZones.AMERICA_KNOX_IN
-   TimeZones.AMERICA_LIMA
-   TimeZones.AMERICA_LOUISVILLE
-   TimeZones.AMERICA_MONTREAL
-   TimeZones.AMERICA_NASSAU
-   TimeZones.AMERICA_NEW_YORK
-   TimeZones.AMERICA_NIPIGON
-   TimeZones.AMERICA_PANAMA
-   TimeZones.AMERICA_PANGNIRTUNG
-   TimeZones.AMERICA_PORT_AU_PRINCE
-   TimeZones.AMERICA_PORTO_ACRE
-   TimeZones.AMERICA_RIO_BRANCO
-   TimeZones.AMERICA_THUNDER_BAY
-   TimeZones.AMERICA_TORONTO
-   TimeZones.BRAZIL_ACRE
-   TimeZones.CANADA_EASTERN
-   TimeZones.CUBA
-   TimeZones.EST
-   TimeZones.EST5EDT
-   TimeZones.ETC_GMT_PLUS_5
-   TimeZones.IET
-   TimeZones.JAMAICA
-   TimeZones.SYSTEMV_EST5
-   TimeZones.SYSTEMV_EST5EDT
-   TimeZones.US_EAST_INDIANA
-   TimeZones.US_EASTERN
-   TimeZones.US_INDIANA_STARKE
-   TimeZones.US_MICHIGAN
-   TimeZones.AMERICA_ANGUILLA
-   TimeZones.AMERICA_ANTIGUA
-   TimeZones.AMERICA_ARUBA
-   TimeZones.AMERICA_ASUNCION
-   TimeZones.AMERICA_BARBADOS
-   TimeZones.AMERICA_BOA_VISTA
-   TimeZones.AMERICA_CAMPO_GRANDE
-   TimeZones.AMERICA_CARACAS
-   TimeZones.AMERICA_CUIABA
-   TimeZones.AMERICA_CURACAO
-   TimeZones.AMERICA_DOMINICA
-   TimeZones.AMERICA_GLACE_BAY
-   TimeZones.AMERICA_GOOSE_BAY
-   TimeZones.AMERICA_GRENADA
-   TimeZones.AMERICA_GUADELOUPE
-   TimeZones.AMERICA_GUYANA
-   TimeZones.AMERICA_HALIFAX
-   TimeZones.AMERICA_LA_PAZ
-   TimeZones.AMERICA_MANAUS
-   TimeZones.AMERICA_MARTINIQUE
-   TimeZones.AMERICA_MONTSERRAT
-   TimeZones.AMERICA_PORT_OF_SPAIN
-   TimeZones.AMERICA_PORTO_VELHO
-   TimeZones.AMERICA_PUERTO_RICO
-   TimeZones.AMERICA_SANTIAGO
-   TimeZones.AMERICA_SANTO_DOMINGO
-   TimeZones.AMERICA_ST_KITTS
-   TimeZones.AMERICA_ST_LUCIA
-   TimeZones.AMERICA_ST_THOMAS
-   TimeZones.AMERICA_ST_VINCENT
-   TimeZones.AMERICA_THULE
-   TimeZones.AMERICA_TORTOLA
-   TimeZones.AMERICA_VIRGIN
-   TimeZones.ANTARCTICA_PALMER
-   TimeZones.ATLANTIC_BERMUDA
-   TimeZones.ATLANTIC_STANLEY
-   TimeZones.BRAZIL_WEST
-   TimeZones.CANADA_ATLANTIC
-   TimeZones.CHILE_CONTINENTAL
-   TimeZones.ETC_GMT_PLUS_4
-   TimeZones.PRT
-   TimeZones.SYSTEMV_AST4
-   TimeZones.SYSTEMV_AST4ADT
-   TimeZones.AMERICA_ST_JOHNS
-   TimeZones.CNT
-   TimeZones.CANADA_NEWFOUNDLAND
-   TimeZones.AGT
-   TimeZones.AMERICA_ARAGUAINA
-   TimeZones.AMERICA_BAHIA
-   TimeZones.AMERICA_BELEM
-   TimeZones.AMERICA_BUENOS_AIRES
-   TimeZones.AMERICA_CATAMARCA
-   TimeZones.AMERICA_CAYENNE
-   TimeZones.AMERICA_CORDOBA
-   TimeZones.AMERICA_FORTALEZA
-   TimeZones.AMERICA_GODTHAB
-   TimeZones.AMERICA_JUJUY
-   TimeZones.AMERICA_MACEIO
-   TimeZones.AMERICA_MENDOZA
-   TimeZones.AMERICA_MIQUELON
-   TimeZones.AMERICA_MONTEVIDEO
-   TimeZones.AMERICA_PARAMARIBO
-   TimeZones.AMERICA_RECIFE
-   TimeZones.AMERICA_ROSARIO
-   TimeZones.AMERICA_SAO_PAULO
-   TimeZones.ANTARCTICA_ROTHERA
-   TimeZones.BET
-   TimeZones.BRAZIL_EAST
-   TimeZones.ETC_GMT_PLUS_3
-   TimeZones.AMERICA_NORONHA
-   TimeZones.ATLANTIC_SOUTH_GEORGIA
-   TimeZones.BRAZIL_DENORONHA
-   TimeZones.ETC_GMT_PLUS_2
-   TimeZones.AMERICA_SCORESBYSUND
-   TimeZones.ATLANTIC_AZORES
-   TimeZones.ATLANTIC_CAPE_VERDE
-   TimeZones.ETC_GMT_PLUS_1
-   TimeZones.AFRICA_ABIDJAN
-   TimeZones.AFRICA_ACCRA
-   TimeZones.AFRICA_BAMAKO
-   TimeZones.AFRICA_BANJUL
-   TimeZones.AFRICA_BISSAU
-   TimeZones.AFRICA_CASABLANCA
-   TimeZones.AFRICA_CONAKRY
-   TimeZones.AFRICA_DAKAR
-   TimeZones.AFRICA_EL_AAIUN
-   TimeZones.AFRICA_FREETOWN
-   TimeZones.AFRICA_LOME
-   TimeZones.AFRICA_MONROVIA
-   TimeZones.AFRICA_NOUAKCHOTT
-   TimeZones.AFRICA_OUAGADOUGOU
-   TimeZones.AFRICA_SAO_TOME
-   TimeZones.AFRICA_TIMBUKTU
-   TimeZones.AMERICA_DANMARKSHAVN
-   TimeZones.ATLANTIC_CANARY
-   TimeZones.ATLANTIC_FAEROE
-   TimeZones.ATLANTIC_MADEIRA
-   TimeZones.ATLANTIC_REYKJAVIK
-   TimeZones.ATLANTIC_ST_HELENA
-   TimeZones.EIRE
-   TimeZones.ETC_GMT
-   TimeZones.ETC_GMT_PLUS_0
-   TimeZones.ETC_GMT_MINUS_0
-   TimeZones.ETC_GMT0
-   TimeZones.ETC_GREENWICH
-   TimeZones.ETC_UCT
-   TimeZones.ETC_UTC
-   TimeZones.ETC_UNIVERSAL
-   TimeZones.ETC_ZULU
-   TimeZones.EUROPE_BELFAST
-   TimeZones.EUROPE_DUBLIN
-   TimeZones.EUROPE_LISBON
-   TimeZones.EUROPE_LONDON
-   TimeZones.GB
-   TimeZones.GB_EIRE = "GB-Eire";
-   TimeZones.GMT
-   TimeZones.GMT0
-   TimeZones.GREENWICH
-   TimeZones.ICELAND
-   TimeZones.PORTUGAL
-   TimeZones.UCT
-   TimeZones.UTC
-   TimeZones.UNIVERSAL
-   TimeZones.WET
-   TimeZones.ZULU
-   TimeZones.AFRICA_ALGIERS
-   TimeZones.AFRICA_BANGUI
-   TimeZones.AFRICA_BRAZZAVILLE
-   TimeZones.AFRICA_CEUTA
-   TimeZones.AFRICA_DOUALA
-   TimeZones.AFRICA_KINSHASA
-   TimeZones.AFRICA_LAGOS
-   TimeZones.AFRICA_LIBREVILLE
-   TimeZones.AFRICA_LUANDA
-   TimeZones.AFRICA_MALABO
-   TimeZones.AFRICA_NDJAMENA
-   TimeZones.AFRICA_NIAMEY
-   TimeZones.AFRICA_PORTO_NOVO
-   TimeZones.AFRICA_TUNIS
-   TimeZones.AFRICA_WINDHOEK
-   TimeZones.ARCTIC_LONGYEARBYEN
-   TimeZones.ATLANTIC_JAN_MAYEN
-   TimeZones.CET
-   TimeZones.ECT
-   TimeZones.ETC_GMT_MINUS_1
-   TimeZones.EUROPE_AMSTERDAM
-   TimeZones.EUROPE_ANDORRA
-   TimeZones.EUROPE_BELGRADE
-   TimeZones.EUROPE_BERLIN
-   TimeZones.EUROPE_BRATISLAVA
-   TimeZones.EUROPE_BRUSSELS
-   TimeZones.EUROPE_BUDAPEST
-   TimeZones.EUROPE_COPENHAGEN
-   TimeZones.EUROPE_GIBRALTAR
-   TimeZones.EUROPE_LJUBLJANA
-   TimeZones.EUROPE_LUXEMBOURG
-   TimeZones.EUROPE_MADRID
-   TimeZones.EUROPE_MALTA
-   TimeZones.EUROPE_MONACO
-   TimeZones.EUROPE_OSLO
-   TimeZones.EUROPE_PARIS
-   TimeZones.EUROPE_PRAGUE
-   TimeZones.EUROPE_ROME
-   TimeZones.EUROPE_SAN_MARINO
-   TimeZones.EUROPE_SARAJEVO
-   TimeZones.EUROPE_SKOPJE
-   TimeZones.EUROPE_STOCKHOLM
-   TimeZones.EUROPE_TIRANE
-   TimeZones.EUROPE_VADUZ
-   TimeZones.EUROPE_VATICAN
-   TimeZones.EUROPE_VIENNA
-   TimeZones.EUROPE_WARSAW
-   TimeZones.EUROPE_ZAGREB
-   TimeZones.EUROPE_ZURICH
-   TimeZones.MET
-   TimeZones.POLAND
-   TimeZones.ART
-   TimeZones.AFRICA_BLANTYRE
-   TimeZones.AFRICA_BUJUMBURA
-   TimeZones.AFRICA_CAIRO
-   TimeZones.AFRICA_GABORONE
-   TimeZones.AFRICA_HARARE
-   TimeZones.AFRICA_JOHANNESBURG
-   TimeZones.AFRICA_KIGALI
-   TimeZones.AFRICA_LUBUMBASHI
-   TimeZones.AFRICA_LUSAKA
-   TimeZones.AFRICA_MAPUTO
-   TimeZones.AFRICA_MASERU
-   TimeZones.AFRICA_MBABANE
-   TimeZones.AFRICA_TRIPOLI
-   TimeZones.ASIA_AMMAN
-   TimeZones.ASIA_BEIRUT
-   TimeZones.ASIA_DAMASCUS
-   TimeZones.ASIA_GAZA
-   TimeZones.ASIA_ISTANBUL
-   TimeZones.ASIA_JERUSALEM
-   TimeZones.ASIA_NICOSIA
-   TimeZones.ASIA_TEL_AVIV
-   TimeZones.CAT
-   TimeZones.EET
-   TimeZones.EGYPT
-   TimeZones.ETC_GMT_MINUS_2
-   TimeZones.EUROPE_ATHENS
-   TimeZones.EUROPE_BUCHAREST
-   TimeZones.EUROPE_CHISINAU
-   TimeZones.EUROPE_HELSINKI
-   TimeZones.EUROPE_ISTANBUL
-   TimeZones.EUROPE_KALININGRAD
-   TimeZones.EUROPE_KIEV
-   TimeZones.EUROPE_MINSK
-   TimeZones.EUROPE_NICOSIA
-   TimeZones.EUROPE_RIGA
-   TimeZones.EUROPE_SIMFEROPOL
-   TimeZones.EUROPE_SOFIA
-   TimeZones.EUROPE_TALLINN
-   TimeZones.EUROPE_TIRASPOL
-   TimeZones.EUROPE_UZHGOROD
-   TimeZones.EUROPE_VILNIUS
-   TimeZones.EUROPE_ZAPOROZHYE
-   TimeZones.ISRAEL
-   TimeZones.LIBYA
-   TimeZones.TURKEY
-   TimeZones.AFRICA_ADDIS_ABABA
-   TimeZones.AFRICA_ASMERA
-   TimeZones.AFRICA_DAR_ES_SALAAM
-   TimeZones.AFRICA_DJIBOUTI
-   TimeZones.AFRICA_KAMPALA
-   TimeZones.AFRICA_KHARTOUM
-   TimeZones.AFRICA_MOGADISHU
-   TimeZones.AFRICA_NAIROBI
-   TimeZones.ANTARCTICA_SYOWA
-   TimeZones.ASIA_ADEN
-   TimeZones.ASIA_BAGHDAD
-   TimeZones.ASIA_BAHRAIN
-   TimeZones.ASIA_KUWAIT
-   TimeZones.ASIA_QATAR
-   TimeZones.ASIA_RIYADH
-   TimeZones.EAT
-   TimeZones.ETC_GMT_MINUS_3
-   TimeZones.EUROPE_MOSCOW
-   TimeZones.INDIAN_ANTANANARIVO
-   TimeZones.INDIAN_COMORO
-   TimeZones.INDIAN_MAYOTTE
-   TimeZones.W_SU
-   TimeZones.ASIA_RIYADH87
-   TimeZones.ASIA_RIYADH88
-   TimeZones.ASIA_RIYADH89
-   TimeZones.MIDEAST_RIYADH87
-   TimeZones.MIDEAST_RIYADH88
-   TimeZones.MIDEAST_RIYADH89
-   TimeZones.ASIA_TEHRAN
-   TimeZones.IRAN
-   TimeZones.ASIA_AQTAU
-   TimeZones.ASIA_BAKU
-   TimeZones.ASIA_DUBAI
-   TimeZones.ASIA_MUSCAT
-   TimeZones.ASIA_ORAL
-   TimeZones.ASIA_TBILISI
-   TimeZones.ASIA_YEREVAN
-   TimeZones.ETC_GMT_MINUS_4
-   TimeZones.EUROPE_SAMARA
-   TimeZones.INDIAN_MAHE
-   TimeZones.INDIAN_MAURITIUS
-   TimeZones.INDIAN_REUNION
-   TimeZones.NET
-   TimeZones.ASIA_KABUL
-   TimeZones.ASIA_AQTOBE
-   TimeZones.ASIA_ASHGABAT
-   TimeZones.ASIA_ASHKHABAD
-   TimeZones.ASIA_BISHKEK
-   TimeZones.ASIA_DUSHANBE
-   TimeZones.ASIA_KARACHI
-   TimeZones.ASIA_SAMARKAND
-   TimeZones.ASIA_TASHKENT
-   TimeZones.ASIA_YEKATERINBURG
-   TimeZones.ETC_GMT_MINUS_5
-   TimeZones.INDIAN_KERGUELEN
-   TimeZones.INDIAN_MALDIVES
-   TimeZones.PLT
-   TimeZones.ASIA_CALCUTTA
-   TimeZones.IST
-   TimeZones.ASIA_KATMANDU
-   TimeZones.ANTARCTICA_MAWSON
-   TimeZones.ANTARCTICA_VOSTOK
-   TimeZones.ASIA_ALMATY
-   TimeZones.ASIA_COLOMBO
-   TimeZones.ASIA_DACCA
-   TimeZones.ASIA_DHAKA
-   TimeZones.ASIA_NOVOSIBIRSK
-   TimeZones.ASIA_OMSK
-   TimeZones.ASIA_QYZYLORDA
-   TimeZones.ASIA_THIMBU
-   TimeZones.ASIA_THIMPHU
-   TimeZones.BST
-   TimeZones.ETC_GMT_MINUS_6
-   TimeZones.INDIAN_CHAGOS
-   TimeZones.ASIA_RANGOON
-   TimeZones.INDIAN_COCOS
-   TimeZones.ANTARCTICA_DAVIS
-   TimeZones.ASIA_BANGKOK
-   TimeZones.ASIA_HOVD
-   TimeZones.ASIA_JAKARTA
-   TimeZones.ASIA_KRASNOYARSK
-   TimeZones.ASIA_PHNOM_PENH
-   TimeZones.ASIA_PONTIANAK
-   TimeZones.ASIA_SAIGON
-   TimeZones.ASIA_VIENTIANE
-   TimeZones.ETC_GMT_MINUS_7
-   TimeZones.INDIAN_CHRISTMAS
-   TimeZones.VST
-   TimeZones.ANTARCTICA_CASEY
-   TimeZones.ASIA_BRUNEI
-   TimeZones.ASIA_CHONGQING
-   TimeZones.ASIA_CHUNGKING
-   TimeZones.ASIA_HARBIN
-   TimeZones.ASIA_HONG_KONG
-   TimeZones.ASIA_IRKUTSK
-   TimeZones.ASIA_KASHGAR
-   TimeZones.ASIA_KUALA_LUMPUR
-   TimeZones.ASIA_KUCHING
-   TimeZones.ASIA_MACAO
-   TimeZones.ASIA_MACAU
-   TimeZones.ASIA_MAKASSAR
-   TimeZones.ASIA_MANILA
-   TimeZones.ASIA_SHANGHAI
-   TimeZones.ASIA_SINGAPORE
-   TimeZones.ASIA_TAIPEI
-   TimeZones.ASIA_UJUNG_PANDANG
-   TimeZones.ASIA_ULAANBAATAR
-   TimeZones.ASIA_ULAN_BATOR
-   TimeZones.ASIA_URUMQI
-   TimeZones.AUSTRALIA_PERTH
-   TimeZones.AUSTRALIA_WEST
-   TimeZones.CTT
-   TimeZones.ETC_GMT_MINUS_8
-   TimeZones.HONGKONG
-   TimeZones.PRC
-   TimeZones.SINGAPORE
-   TimeZones.ASIA_CHOIBALSAN
-   TimeZones.ASIA_DILI
-   TimeZones.ASIA_JAYAPURA
-   TimeZones.ASIA_PYONGYANG
-   TimeZones.ASIA_SEOUL
-   TimeZones.ASIA_TOKYO
-   TimeZones.ASIA_YAKUTSK
-   TimeZones.ETC_GMT_MINUS_9
-   TimeZones.JST
-   TimeZones.JAPAN
-   TimeZones.PACIFIC_PALAU
-   TimeZones.ROK
-   TimeZones.ACT
-   TimeZones.AUSTRALIA_ADELAIDE
-   TimeZones.AUSTRALIA_BROKEN_HILL
-   TimeZones.AUSTRALIA_DARWIN
-   TimeZones.AUSTRALIA_NORTH
-   TimeZones.AUSTRALIA_SOUTH
-   TimeZones.AUSTRALIA_YANCOWINNA
-   TimeZones.AET
-   TimeZones.ANTARCTICA_DUMONTDURVILLE
-   TimeZones.ASIA_SAKHALIN
-   TimeZones.ASIA_VLADIVOSTOK
-   TimeZones.AUSTRALIA_ACT
-   TimeZones.AUSTRALIA_BRISBANE
-   TimeZones.AUSTRALIA_CANBERRA
-   TimeZones.AUSTRALIA_HOBART
-   TimeZones.AUSTRALIA_LINDEMAN
-   TimeZones.AUSTRALIA_MELBOURNE
-   TimeZones.AUSTRALIA_NSW
-   TimeZones.AUSTRALIA_QUEENSLAND
-   TimeZones.AUSTRALIA_SYDNEY
-   TimeZones.AUSTRALIA_TASMANIA
-   TimeZones.AUSTRALIA_VICTORIA
-   TimeZones.ETC_GMT_MINUS_10
-   TimeZones.PACIFIC_GUAM
-   TimeZones.PACIFIC_PORT_MORESBY
-   TimeZones.PACIFIC_SAIPAN
-   TimeZones.PACIFIC_TRUK
-   TimeZones.PACIFIC_YAP
-   TimeZones.AUSTRALIA_LHI
-   TimeZones.AUSTRALIA_LORD_HOWE
-   TimeZones.ASIA_MAGADAN
-   TimeZones.ETC_GMT_MINUS_11
-   TimeZones.PACIFIC_EFATE
-   TimeZones.PACIFIC_GUADALCANAL
-   TimeZones.PACIFIC_KOSRAE
-   TimeZones.PACIFIC_NOUMEA
-   TimeZones.PACIFIC_PONAPE
-   TimeZones.SST
-   TimeZones.PACIFIC_NORFOLK
-   TimeZones.ANTARCTICA_MCMURDO
-   TimeZones.ANTARCTICA_SOUTH_POLE
-   TimeZones.ASIA_ANADYR
-   TimeZones.ASIA_KAMCHATKA
-   TimeZones.ETC_GMT_MINUS_12
-   TimeZones.KWAJALEIN
-   TimeZones.NST
-   TimeZones.NZ
-   TimeZones.PACIFIC_AUCKLAND
-   TimeZones.PACIFIC_FIJI
-   TimeZones.PACIFIC_FUNAFUTI
-   TimeZones.PACIFIC_KWAJALEIN
-   TimeZones.PACIFIC_MAJURO
-   TimeZones.PACIFIC_NAURU
-   TimeZones.PACIFIC_TARAWA
-   TimeZones.PACIFIC_WAKE
-   TimeZones.PACIFIC_WALLIS
-   TimeZones.NZ_CHAT = "NZ-CHAT";
-   TimeZones.PACIFIC_CHATHAM
-   TimeZones.ETC_GMT_MINUS_13
-   TimeZones.PACIFIC_ENDERBURY
-   TimeZones.PACIFIC_TONGATAPU
-   TimeZones.ETC_GMT_MINUS_14
-   TimeZones.PACIFIC_KIRITIMATI
# Formatters
These formatters can be passed as a parameter to the methods described above. See [Appendix A: Datum Types and Formatters](#) for details.
## Simple Formatters
-   Formatters.BOOLEAN
-   Formatters.DATE
-   Formatters.DATE_IN_WORDS
-   Formatters.DATE_LONG
-   Formatters.DATE_MEDIUM
-   Formatters.DATE_SHORT
-   Formatters.DATE_TIME_12_HR
-   Formatters.DATE_TIME_24_HR
-   Formatters.DATE_TIME_IN_WORDS_12_HR
-   Formatters.DATE_TIME_IN_WORDS_24_HR
-   Formatters.DATE_TIME_LONG_12_HR
-   Formatters.DATE_TIME_LONG_24_HR
-   Formatters.DATE_TIME_MEDIUM_12_HR
-   Formatters.DATE_TIME_MEDIUM_24_HR
-   Formatters.DATE_TIME_SHORT_12_HR
-   Formatters.DATE_TIME_SHORT_24_HR
-   Formatters.DATE_TIME_WITH_TIME_ZONE_12_HR
-   Formatters.DATE_TIME_WITH_TIME_ZONE_24_HR
-   Formatters.DECIMAL
-   Formatters.DECIMAL_IN_WORDS
-   Formatters.EMAIL
-   Formatters.INTEGER
-   Formatters.INTEGER_IN_WORDS
-   Formatters.ORDINAL
-   Formatters.ORDINAL_IN_WORDS
-   Formatters.ORGANIZATION
-   Formatters.PERSON_FULL_NAME
-   Formatters.PERSON_FIRST_NAME
-   Formatters.PERSON_LAST_NAME
-   Formatters.US_PHONE_NUMBER
-   Formatters.TEXT
-   Formatters.TIME_12H
-   Formatters.TIME_24H
## Location Formatters
-   Formatters.AIRPORT_NAME
-   Formatters.AIRPORT_CODE
-   Formatters.CAPITAL
-   Formatters.COUNTRY_NAME
-   Formatters.COUNTRY_CODE
-   Formatters.US_CITY
-   Formatters.US_COUNTY
-   Formatters.US_STATE_NAME
-   Formatters.US_STATE_CODE
-   Formatters.US_STREET_ADDRESS
-   Formatters.US_ZIP_CODE
## Unit formatters
-   Formatters.AGE
-   Formatters.AGE_IN_WORDS
-   Formatters.AREA
-   Formatters.AREA_IN_WORDS
-   Formatters.CURRENCY
-   Formatters.CURRENCY_IN_WORDS
-   Formatters.DURATION
-   Formatters.DURATION_IN_WORDS
-   Formatters.LENGTH
-   Formatters.LENGTH_IN_WORDS
-   Formatters.PERCENTAGE
-   Formatters.PERCENTAGE_IN_WORDS
-   Formatters.SPEED
-   Formatters.SPEED_IN_WORDS
-   Formatters.TEMPERATURE
-   Formatters.TEMPERATURE_IN_WORDS
-   Formatters.VOLUME
-   Formatters.VOLUME_IN_WORDS
-   Formatters.WEIGHT
-   Formatters.WEIGHT_IN_WORDS
## Simple Range Formatters
-   Formatters.TIME_RANGE_12_HR
-   Formatters.TIME_RANGE_24_HR
-   Formatters.DATE_RANGE
-   Formatters.DATE_RANGE_IN_WORDS
-   Formatters.DATE_RANGE_LONG
-   Formatters.DATE_RANGE_MEDIUM
-   Formatters.DATE_RANGE_SHORT
-   Formatters.DATE_TIME_RANGE_12_HR
-   Formatters.DATE_TIME_RANGE_24_HR
-   Formatters.DATE_TIME_RANGE_IN_WORDS_12_HR
-   Formatters.DATE_TIME_RANGE_IN_WORDS_24_HR
-   Formatters.DATE_TIME_RANGE_LONG_12_HR
-   Formatters.DATE_TIME_RANGE_LONG_24_HR
-   Formatters.DATE_TIME_RANGE_MEDIUM_12_HR
-   Formatters.DATE_TIME_RANGE_MEDIUM_24_HR
-   Formatters.DATE_TIME_RANGE_SHORT_12_HR
-   Formatters.DATE_TIME_RANGE_SHORT_24_HR
-   Formatters.INTEGER_RANGE
-   Formatters.INTEGER_RANGE_IN_WORDS
-   Formatters.DECIMAL_RANGE
-   Formatters.DECIMAL_RANGE_IN_WORDS
-   Formatters.ORDINAL_RANGE
-   Formatters.ORDINAL_RANGE_IN_WORDS
## Unit Range Formatters
-   Formatters.AGE_RANGE
-   Formatters.AGE_RANGE_IN_WORDS
-   Formatters.AREA_RANGE
-   Formatters.AREA_RANGE_IN_WORDS
-   Formatters.CURRENCY_RANGE
-   Formatters.CURRENCY_RANGE_IN_WORDS
-   Formatters.DURATION_RANGE
-   Formatters.DURATION_RANGE_IN_WORDS
-   Formatters.LENGTH_RANGE
-   Formatters.LENGTH_RANGE_IN_WORDS
-   Formatters.PERCENTAGE_RANGE
-   Formatters.PERCENTAGE_RANGE_IN_WORDS
-   Formatters.SPEED_RANGE
-   Formatters.SPEED_RANGE_IN_WORDS
-   Formatters.TEMPERATURE_RANGE
-   Formatters.TEMPERATURE_RANGE_IN_WORDS
-   Formatters.VOLUME_RANGE
-   Formatters.VOLUME_RANGE_IN_WORDS
-   Formatters.WEIGHT_RANGE
-   Formatters.WEIGHT_RANGE_IN_WORDS
# Syntax Examples
## Get extracted Datum
``` java
def datum = quantityService.getExtractedDatum(DatumTypes.age(),'user_age');
```
## Normalize
``` java
def datum = quantityService.normalize('Japan', DatumType.COUNTRY);
```
## Normalize and Format
``` java
quantityService.normalizeAndFormat('12/12/2000', DatumType.DATE, Formatters.DATE_IN_WORDS);
```
## Format
``` java
def datum = quantityService.normalize('China', DatumType.COUNTRY);
def datumFormatterByFormatterProvided = quantityService.format(datum, Formatters.COUNTRY);
def datumFormattedUsingDefaultFormatter = quantityService.format(datum);
```
# Extract Datum with quantityService
This demonstration extracts date-related terms -- this coming Friday or tomorrow -- from a user utterance and converts the term into a correct data adjusted for the user’s time zone.
![](attachments/11939536/11939537.png)
Figure. BPN to Extract Datum with quantityService
## Create a BPN
In the Amelia administration pages, use the Process Knowledge tab to create a new BPN model and name it testQuantity. Save the new model then build each of the BPN tasks as described below.
Create these Tasks in a BPN, as described and ordered in the table below.
Table. BPN Specifications to Extract Datum with quantityService

| Task Number | Task Object Text | Notes |
| ----|----|----|
| 1 | say let's get started | Initialize Amelia and let the person know the conversation has started |
| 2 | ask 'What is your question using a date word or phrase' | Prompt the user for a statement or request with an implied date, for example, “I need a rental car next Friday” or “day after tomorrow”For this demonstration, click the Properties Panel tab on the right side of the workspace and set Ask behavior (1st pass) and Ask behavior (subsequent) to Ignore if responded. |
| 3 | parse date | Click the task once and select the wrench Change Type icon and Script Task from the dropdown menu that appears.Click the task once and select the document Edit Script icon. The Script editor will appear.Type or copy/paste code from below into the Script editor. If needed, select Groovy as the language. |
| 4 | say "I parsed ${datum} out of '${sentence}' " | Display output of date extracted from utterance from Task 2 above, as well as the full utterance |

Once the BPN tasks are built and defined, finish with these steps:
-   Click the Save button
-   Click the Deploy button
These steps load the BPN model into Amelia’s memory.
## A Script to Extract Datum Information
This Groovy script is typed or copy/pasted into a Script Task, as described in Task 3 in the table above.
``` bash
def startSentence = execution.getVariable("response")
def dte = quantityService.normalizeAndFormat(startSentence, DatumType.DATE, Formatters.DATE_LONG)
execution.setVariable('datum', dte)
execution.setVariable('sentence', startSentence)
```
## Interact with Amelia
When the BPN models are built and approved, as described in the section above, open Amelia’s chat interface by selecting Mind from the navigation links at the top right of the administration pages. Then click the Process Memory tab on the right edge of the Mind panel.
1.  Click the web browser reload button to refresh the page and clear any earlier interactions.
2.  Ask Amelia to run the testQuantity workflow by typing this command in the chat interface:
    ``` bash
    run the workflow testQuantity
    ```
3.  Type in a sentence that includes an implied date-related reference, for example, “I need a hotel day after tomorrow” or “I need a hotel this coming Friday.”
4.  Amelia displays the date reference extracted from the utterance, as well as the full utterance.
## Attachments:
![](images/icons/bullet_blue.gif) [image2018-1-5_10-42-22.png](attachments/11939536/11939537.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-10-12_16-42-29.png](attachments/11939536/11939538.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-10-12_15-45-17.png](attachments/11939536/11939539.png) (image/png)  
![](images/icons/bullet_blue.gif) [image2017-10-12_15-40-30.png](attachments/11939536/11939540.png) (image/png)  
