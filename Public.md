#﻿Public methods in the BookBooN.com API

The public API contains a number of read-only methods, allowing you to build an application fetching categories, books and search results.

##Support for different languages

All areas of the public API accepts an optional query string parameter `lang`. If present, the parameter will be taken as a hint for the preferred language of the user, and we will try to deliever content in this language.

Currently, most of our content is available in the following eight languages:

  * Danish = da
  * Dutch = nl
  * English = en
  * Finnish = fi
  * French = fr
  * German = de
  * Norwegian = nb
  * Swedish = sv

If you design your application to support any other language(s), do pass the relevant [ISO 639-1](http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) language code along in the `lang` parameter. If we do not have translations for your language, we will fallback to English. If we later add translations for the language, no change is required on your end to start receiving localized data.

##Categories

As reflected on BookBooN.com, our books are organized into a hierarchy. Traversing the category tree begins here: http://api.bookboon.com/categories

Categories are returned as an array of objects with properties as follows:

  * `id` : unique identifier for the category
  * `name` : a short name for the category to be displayed in menus or the like

In order to query for contents of a category, make a new request with the `id` appended to the URL. Example: http://api.bookboon.com/categories/412e64e2-0965-e011-bd88-22a08ed629e5

This will give you an expanded view of the selected category

  * `name` : a short name for the category (as before)
  * `description` : a few sentences of text introducing the category
  * `categories` : an array of subcategories, in same format as root category listing
  * `books` : an array of books in the category each with
    - `id`
    - `title`
    - `thumbnail`
    - `language`

A category may contain either sub categories, books or both.

> **Note:** While the category tree currently has a fixed height of two, you should not rely on this in your application design. As the number of books available at BookBooN.com grows, we might have to introduce additional layers in some areas of the tree.


##Books

http://api.bookboon.com/books/add5ee13-0f5e-e011-bd88-22a08ed629e5

##Search

http://api.bookboon.com/search?q=austral

http://api.bookboon.com/search?q=austral&lang=da
