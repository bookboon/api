#Methods in the bookboon.com API
 
##Support for different languages

All areas of the API accepts an optional header string parameter `Accept-Language`. If present the parameter will be taken as a hint for the preferred language of the user and we will try to deliver content in this language.

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

If you design your application to support any other language(s), do pass the relevant [ISO 639-1](http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) language code along in the `Accept-Language` header. If we do not have translations for your language, we will fallback to English. If we later add translations for the language, no change is required on your end to start receiving localized data.

##Categories

As reflected on bookboon.com, our books are organized into a hierarchy. Traversing the category tree begins here: http://bookboon.com/api/categories

Categories are returned as an array of objects with properties as follows:

  * `_id` : unique identifier for the category
  * `_link` : url to the category in the api
  * `name` : a short name for the category to be displayed in menus or the like
  * `description` : description of the category content and purpose
  * `homepage`: url to the category on bookboon.com


In order to query for contents of a category, make a new request with the `id` appended to the URL. Example: http://bookboon.com/api/categories/ab0f00ac-7749-4500-a808-a16200fca2f6

This will give you an expanded view of the selected category

  * `name` : a short name for the category (as before)
  * `description` : a few sentences of text introducing the category (as before)
  * `categories` : an array of subcategories, in same format as root category listing
  * `books` : an array of books in the category each with
    - `_id`
    - `_link`
    - `title`
    - `thumbnail`
    - `language`
    - `published`
    - `abstact`
    - `rating`
    - `homepage`

A category may contain either sub categories, books or both. The `lang` parameter will determine language of the category name and also whether to include books in that language. English will always be shown no matter the locale.

##Books

http://bookboon.com/api/books/add5ee13-0f5e-e011-bd88-22a08ed629e5

##Search

http://bookboon.com/api/search?q=austral

http://bookboon.com/api/search?q=austral&lang=da


##User profiles

Only registered users can download books via the API. However, the process of registering a user profile is very simple, and you only need to do it once for each user.

Each call to the authenticated API with handle and valid API key will either match a user profile or trigger the creation of a new profile if none exists. Calls to the authenticated API are done with HTTP Basic Authentication [RFC 2617](http://www.ietf.org/rfc/rfc2617.txt).

    https://[api_id]:[api_secret]@bookboon.com/api/<resource-name>

The handle can be any string (max length = 64), and may contain any ASCII character, excluding a colon. Your application might already have a unique user id (eg. Facebook Profile ID), alternatively you can generate a random string during installation of the app. Whatever you pick, the important thing is to stick with it. Every authenticated request made by a specific user must include her unique handle. Two users of the same app must not use the same handle.

##Questions and answers

Before a newly created user is allowed to download books, you will need to help us ask her a few questions. We need the answers for segmentation and statistic purposes. You decide if you will ask the questions upon installation of your application or immediately before the first download.

To get the list of questions we need answered by a specific user, simply make a GET request to:

    https://[api_id]:[api_secret]@bookboon.com/api/questions

Notice the use of HTTPS, which is required throughout the authenticated API, and remember to replace `[api_id]` and `[api_secret]` with the relevant values.

The request to the `/questions` resource will return an array of questions similar to this:

    [
        {
            question: "Studying or working?"
            answers: [
                {
                    id: "1400a987-7b18-4b5c-a63f-742cff3132cd"
                    text: "Student"
                },
                {
                    id: "6230e12c-68d8-45d5-8f02-1d3997713150"
                    text: "Working"
                }
            ]
        },
        {
            question: "Favorite food"
            answers: [
                {
                    id: "5aca0fe1-0d93-41b1-8691-aa242a526f17"
                    text: "Bacon"
                },
                {
                    id: "c31da2af-5b86-4096-945b-b43b1108ca49"
                    text: "Ham"
                },
                {
                    id: "1400a987-7b18-4b5c-a63f-742cff3132cd"
                    text: "Olives"
                }
            ]
        }
    ]

All questions are provided with a fixed set of possible answers. When the user has selected an answer for each question, make another request to the `/questions` method including the `id` of each selected answer as a separate `answer` parameter. Example (bacon-loving student) would post the following string to `/questions`:

    answer=6230e12c-68d8-45d5-8f02-1d3997713150&answer=5aca0fe1-0d93-41b1-8691-aa242a526f17

> **Note:** The example above – and more to come – uses POST style parameters. All methods in the authenticated API will enforce using the appropriate method, meaning resources retrieving information (safe) will only accept GET requests, whereas resources saving data will only accept POST requests.

Depending on the selected answers, a number of followup questions may be returned. Repeat the process of asking questions and submitting them until you receive an empty array when invoking the `/questions` resource.

Currently, no combination of answers will generate more than five questions in total, including those asked initially. We intend to enforce this limit in the future, and you are encouraged to communicate a maximum of five questions visually to your users. See the download form on [bookboon.com](http://bookboon.com/) for an example.

> **Note:** While most questions will make a fit for a drop down list, with 2-10 possible answers, a few questions will have as many as 100+ possible answers. Depending on your platform, you might want to consider some sort of auto-completing text box or similar for such questions.


##Downloading books

After discovering an interesting book via the [public API](public) (browsing categories or searching), you should present the user with a hard-to-miss download button/link. When activated, make an authenticated API request to the `/books/<bookid>/download` resource using the POST method:

    https://[api_id]:[api_secret]@bookboon.com/api/books/39a1bd3e-e876-47b5-896c-9efb00dd309e/download

If everything works out, you should get a 302 redirect response to the book file 

Do not store the link, as it is intended for a one-time download only and will expire. You can expect the link to be good for at least 30 minutes, which should give you sufficient time to complete the download.

If it happens that you have not yet provided us with answers for all of our questions, or if the set of questions have been changed, you will receive an answer like this (HTTP status code 403):

    {
        message: "The authenticated profile is incomplete.",
        error: "ProfileIncomplete"
    }

In that case, you must make a new call to `/questions` and continue with the question asking process from here. As soon as you get to an empty array of questions, the profile will be unblocked and you can proceed with the download.

> **Note:** HTTP status code 403 may have other causes than profile incompleteness. While you can, and should, use `status_code != 200` to detect if the request has succeeded, in the case of an error, you should proceed to test if `error == 'ProfileIncomplete'`. This token is a certain indicator of the problem at hand.

To enable developers to customize the books the download method takes two parameters `branding` and `rotation`. They should be posted with every download. They are both GUID types and are provided by Bookboon if relevant.

##Retrieving recommendations

By looking at the download history of a specific user, we are able to make recommendations for others books that might be of interest for this user. You can retrieve a list of recommended books by doing an authenticated API request to the `/recommendations` method:

    https://[api_id]:[api_secret]@bookboon.com/api/recommendations

By default we will return an array with at most five books. Use the `limit` parameter if you want a different number of books returned. Example of returned data:

##Submitting reviews

We are currently working on a new feature for the BookBoon.com platform and API, allowing users to post reviews of our books. Basically, the user can provide a rating (1 through 5) and a comment, both to be stored and published for other users.

More details on this feature will be added when the relevant API methods are available.
