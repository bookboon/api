#﻿Public methods in the bookboon.com API

The public API contains a number of read-only methods, allowing you to build an application fetching categories, books and search results.

##Support for different languages

All areas of the public API accepts an optional query string parameter `lang`. If present, the parameter will be taken as a hint for the preferred language of the user, and we will try to deliver content in this language.

Currently, most of our content is available in the following eleven languages:

  * Chinese = cn
  * Danish = da
  * Dutch = nl
  * English = en
  * Finnish = fi
  * French = fr
  * German = de
  * Norwegian = nb
  * Spanish = es
  * Swedish = sv
  * Czech = cs

If you design your application to support any other language(s), do pass the relevant [ISO 639-1](http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) language code along in the `lang` parameter. If we do not have translations for your language, we will fallback to English. If we later add translations for the language, no change is required on your end to start receiving localized data.

##Categories

As reflected on bookboon.com, our books are organized into a hierarchy. Traversing the category tree begins here: http://api.bookboon.com/categories

Categories are returned as an array of objects with properties as follows:

  * `id` : unique identifier for the category
  * `name` : a short name for the category to be displayed in menus or the like

In order to query for contents of a category, make a new request with the `id` appended to the URL. Example: http://api.bookboon.com/categories/ab0f00ac-7749-4500-a808-a16200fca2f6

This will give you an expanded view of the selected category

  * `name` : a short name for the category (as before)
  * `description` : a few sentences of text introducing the category
  * `categories` : an array of subcategories, in same format as root category listing
  * `books` : an array of books in the category each with
    - `id`
    - `title`
    - `thumbnail`
    - `language`
    - `published`
    - `abstact`
    - `rating`

A category may contain either sub categories, books or both. The `lang` parameter will determine language of the category name and also whether to include books in that language. English will always be shown no matter the locale.

##Books

http://api.bookboon.com/books/add5ee13-0f5e-e011-bd88-22a08ed629e5

##Search

http://api.bookboon.com/search?q=austral

http://api.bookboon.com/search?q=austral&lang=da
