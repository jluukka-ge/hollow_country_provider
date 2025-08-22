# hollow_country_provider Flutter Plugin
Hollow country Provider is a flutter library wrapper around the API provided by REST Countries https://restcountries.eu (Get information about countries via a RESTful API).

It contains minimal dependencies (`flutter` only) in order to not produce unnecessary dependency version conflicts. Yay!

Forked from TheAlphamerc/country_provider


## Getting Started
### 1. Add library to your pubspec.yaml

```yaml

dependencies:
  hollow_country_provider:
    git:
      url: https://github.com/jluukka-ge/hollow_country_provider.git

```

### 2. Import library in dart file

```dart
import 'package:hollow_country_provider/hollow_country_provider.dart';
```

### 3. Provide an HTTP GET function with which data can be fetched

```dart
// In `http` version `^0.13.3`, this used to be equivalent to:
Future<Response> httpGet() {
  return Client().get(Uri.parse(uri)); // Client from `http` package
}

final CountryProvider countryProvider = CountryProvider(httpGet);
```

## Note

Each method return a `List` of [`Country`](https://github.com/TheAlphamerc/country_provider/blob/master/lib/src/models/country.dart).

## Usage

- Get all countries.

```dart
// Get all countries
List<Country>? countries = await countryProvider.getAllCountries();
```

- Search by country name. It can be the native name or partial name.

```dart
// Search by country name
List<Country>? result = await countryProvider.getCountriesByName("Ameri");
```

If partial name, this method could return a list of countries. Else a List of one element.

- Search by country full name.

```dart
// Search by country full name
Country result = await countryProvider.getCountryByFullname("India")?.first;
```

-  Search by ISO 3166-1 2-letter or 3-letter country code.

```dart
// Search by list of ISO 3166-1 2-letter or 3-letter country codes
Country result = await countryProvider.getCountryByCode("Ind")?.first;
```

-  Search by list of ISO 3166-1 2-letter or 3-letter country codes.

```dart
// Search by list of ISO 3166-1 2-letter or 3-letter country codes
List<Country>? result =await countryProvider.getCountriesByListOfCodes(["Ind", "col", "ru"]);
```

- Search by ISO 4217 currency code.

```dart
// Search by ISO 4217 currency code
List<Country>? result = await countryProvider.getCountryByCurrencyCode("Inr")
```

- Search by ISO 639-1 language code.

```dart
// Search by ISO 639-1 language code
List<Country>? result = await countryProvider.getCountriesByLanguageCode(["Hin","en",]);
```

-  Search by capital city.

```dart
// Search by capital city
var result = await countryProvider.getCountryByCapitalCity("Delhi");
```

You can use `var` instead of explicit types. I use explicit types to show you the return type of each method.

- Search by calling code.

```dart
// Search by calling code
List<Country>? result = await countryProvider.getCountryByCallingCode(91);
```

-  Search by continent: Africa, Americas, Asia, Europe, Oceania.

```dart
//  Search by continent: Africa, Americas, Asia, Europe, Oceania
List<Country>? result = await countryProvider.getcountryByRegionalBloc("Asia");
```

- Search by regional bloc: EU, EFTA, CARICOM, AU, USAN, EEU, AL, ASEAN , CAIS, CEFTA , NAFTA , SAARC.

```dart
//  Search by regional bloc
List<Country>? result = await countryProvider.getCountriesByContinent("ASEAN");
```

**EU** (European Union), **EFTA** (European Free Trade Association), **CARICOM** (Caribbean Community), **PA** (Pacific Alliance), **AU** (African Union), **USAN** (Union of South American Nations), **EEU** (Eurasian Economic Union), **AL** (Arab League), **ASEAN** (Association of Southeast Asian Nations), **CAIS** (Central American Integration System), **CEFTA** (Central European Free Trade Agreement), **NAFTA** (North American Free Trade Agreement), **SAARC** (South Asian Association for Regional Cooperation).

## Apply filters

To get filtered country data pass [CountryFilter](https://github.com/TheAlphamerc/country_provider/blob/master/lib/src/models/countryFilter.dart) model as argument in search countries method.

```dart
// Get all countries name only
var countries = await countryProvider.getAllCountries(filter: CountryFilter(isName: true));
List<String> countriesInSpanish = countries.map((e) => e.name).toList();

// Get all countries name only in Spanish
var countries = await countryProvider.getAllCountries(filter: CountryFilter(isName: true));
List<String> countriesInSpanish = countries.map((e) => e.translations.es).toList();

// Get Europe countries in French language
var europeCountries = await countryProvider.getcountryByRegionalBloc("Europe",filter: CountryFilter(isName: true));
List<String> europeCountriesInFrench = europeCountries.map((e) => e.translations.?fr).toList();

// Get all countries name with their capital city only
var countries = await countryProvider.getAllCountries(filter: CountryFilter(isName: true,isCapital:true));

// Get all countries name with country code and their capital city only
var countries = await countryProvider.getAllCountries(filter: CountryFilter(isName: true,isCapital:true,isAlpha2Code:true,isAlpha3Code: true));


// Feel free to apply filters 🤓
```

Default language for country name is English, but you can also get the name in other languages such as: `de`(German language),  `es`(Spanish language), `fr`(French language),  `ja`(Japanese language), `it`(Italian language), `br`(Breton language), `pt`(Portuguese language), `nl`(Dutch language), `hr`(Croatian language) and `fa`(Persian language).


## Country class

```dart
class Country
{	  
    // Get Country name
    String? name;

    // Gets  Top Level Domain
    List<String>? topLevelDomain;

    // Gets Alpha2 Code
    String? alpha2Code;

    // Gets Alpha3 Code
    String? alpha3Code;

    // Gets Calling Code
    List<String>? callingCodes;

    // Gets Capital City
    String? capital;

    // Get Alt Spelling
    List<String>? altSpellings;

    // Get Region
    String? region;

    // Get Sub region
    String? subregion;

    // Get Population
    int? population;

    // Get Latlng(Latitude and Longitude)
    List<double>? latlng;

    // Get Demonym
    String? demonym;

    // Get Area
    double? area;

    // Get Gini
    double? gini;

    // Get Timezone
    List<String>? timezones;

    // Get Borders
    List<String>? borders;

    // Get Native Name
    String? nativeName;

    // Get Numeric Code
    String? numericCode;

    // Get Currencies
    List<Currency>? currencies;

     // Get Languages
    List<Language>? languages;

    // Gets Translations
    Translations? translations;

    // Get Flag
    String? flag;

    // Get Regional Blocs
    List<RegionalBloc>? regionalBlocs;

    // Get  Cioc(International Olympic Committee Code)
    String ?cioc;
}
```
## CountryFilter Class
``` dart
class CountryFilter{
  bool isName;
  bool isCapital;
  bool isRegion;
  bool isAlpha2Code;
  bool isAlpha3Code;
  bool isDemonym;
  bool isTimeZone;
  bool isCallingCode;
  bool isBorders;
  bool isAltSpellings;
  bool isCurrency;
  bool isLanguage;
  bool isLatLong;
  bool isTranslation;
  bool isFlag;

  CountryFilter({
    this.isName = false,
    this.isCapital = false,
    this.isRegion = false,
    this.isAlpha2Code = false,
    this.isAlpha3Code = false,
    this.isDemonym = false,
    this.isTimeZone = false,
    this.isCallingCode = false,
    this.isBorders = false,
    this.isAltSpellings = false,
    this.isCurrency = false,
    this.isLanguage = false,
    this.isLatLong = false,
    this.isTranslation = false,
    this.isFlag = false,
  });
}
```

## Credits

Thanks to:

- Fayder Florez for developing [REST Countries API](https://github.com/fayder/restcountries).
- Sonu Sharma for TheAlphamerc/country_provider

## Aid my quest to make hollow packages by carving out unnecessary dependencies

If you found this project helpful or you learned something from the source code and want to thank me, consider buying me a cup of :coffee:

- <a href="https://www.buymeacoffee.com/iekedemus"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" height="30"></a>
