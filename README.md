Python wrapper to Google Search service.

rovide a wrapper for the following service:
* Google Search
* Google Translate

Forked from [xgoogle](https://github.com/pkrumins/xgoogle) 
by Peteris Krumins <peter@catonmat.net>

Contributors:
* Holger Berndt
* Juanjo Conti
* Steve Steiner
* azappella

Disclaimer
==========

It may voilate the Google [Terms of Service](https://www.google.com/intl/en/policies/terms/)

> Don’t misuse our Services. 
> For example, don’t interfere with our Services or 
> try to access them using a method 
> other than the interface and the instructions that we provide. 

I just provide it for personal study and research.

Usage
=====

Google Search
-------------

Here is an example usage of Google Search module:

    >>> from xgoogle.search import GoogleSearch
    >>> gs = GoogleSearch("catonmat")
    >>> gs.results_per_page = 25
    >>> results = gs.get_results()
    >>> for res in results:
    ...   print res.title.encode('utf8')
    ... 

    output:

    good coders code, great reuse
    MIT's Introduction to Algorithms, Lectures 1 and 2: Analysis of ...
    catonmat - Google Code
    ...

The GoogleSearch object has several public methods and properties:

    method get_results() - gets a page of results, returning a list of SearchResult objects.
    property num_results - returns number of search results found.
    property results_per_page - sets/gets the number of results to get per page.
    property page - sets/gets the search page.

A SearchResult object has three attributes -- "title", "desc", and "url".
They are Unicode strings, so do a proper encoding before outputting them.


Google Translate
----------------

Here is an example usage of Google Translate module:

    >>> from xgoogle.translate import Translator
    >>>
    >>> translate = Translator().translate
    >>> print translate("Mani sauc Pēteris", lang_to="ru").encode('utf-8')
    Меня зовут Петр
    >>> print translate("Mani sauc Pēteris", lang_to="en")
    My name is Peter
    >>> print translate("Меня зовут Петр")
    My name is Peter

The "translate" function takes three arguments - "message", "lang_from" and "lang_to".
If "lang_from" is not given, Google's translation service auto-detects it.
If "lang_to" is not given, it defaults to "en" (English).

In case of an error the "translate" function throws "TranslationError" exception.
Make sure to wrap your code in try/except block to catch it:

    >>> from xgoogle.translate import Translator, TranslationError
    >>>
    >>> try: 
    >>>   translate = Translator().translate
    >>>   print translate("")
    >>> except TranslationError, e:
    >>>   print e

    Failed translating: invalid text 


The Google Translate module also provides "LanguageDetector" class that can be used
to detect the language of the text.

Here is an example usage of LanguageDetector:

    >>> from xgoogle.translate import LanguageDetector, DetectionError
    >>>
    >>> detect = LanguageDetector().detect
    >>> english = detect("This is a wonderful library.")
    >>> english.lang_code
    'en'
    >>> english.lang
    'English'
    >>> english.confidence
    0.28078437000000001
    >>> english.is_reliable
    True

The "DetectionError" may get raised if the detection failed.


License
=======
Licensed under MIT license.
