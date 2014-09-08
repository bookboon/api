# HTTP Headers

All API calls will accept the following HTTP request headers:

`Accept-Language` : Set to ISO-631-1 country codes, see the [API page](https://github.com/bookboon/api/blob/master/API.md) 

`X-Bookboon-Branding` : Override cover on book. GUID given by from bookboon if relevant

`X-Bookboon-Rotation` : Override adverts in book. GUID given by from bookboon if relevant

# /categories 
__Method__: GET  
__Variables__: *none*  
__Output__: array [ `_id` -- guid for category, `_link` -- link to api object, `name` -- name of category, `description` -- description of category content, `homepage` -- link the category on bookboon.com ]  

__Example__:  
`	[
		{ _id:"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      _link:"http://...",   
      name:"xxxxxx",   
      description:"...",  
      homepage:"http://..." }  
	]
`
## /categories/`<guid>` 
__Method__: GET  
__Variables__:  *none*  
__Output__: `name` -- name of the category,  
`title` -- subtitle
`description` -- long description of contents
categories [ `_id` -- guid for category, `name` -- name of category ],
books [ `_id` -- guid for book,
`name` --

__Example__:
`
	{
		"name":"Textbooks","title":"Download free textbooks online","description":"long description text",  
		"categories":  
		[  
				{"_id":"3e2e64e2-0965-e011-bd88-22a08ed629e5","name":"Accounting"}, ....  
		],  
		"books":[]  
	}
`
# /search
__Method__: GET  
__Variables__: `q`  -- Search string  
__Output__:  array[ `_id` -- guid for book, `title` -- name of book, `thumbnail` -- url to thumbnail picture , language [ `code` -- short name,  `name` -- proper country name ] ]  

__Example__:  
`
	[   
		{"_id":"d2d5ee13-0f5e-e011-bd88-22a08ed629e5","title":"Essentials of Macroeconomics:Exercises",  
		"thumbnail":"http://bookboon.com/uk/textbooks/macroeconimics-exercisebook.180.jpg",  
		"language":{"code":"en","name":"English"}},  
		....  
	]  
`
# /books/`<guid>`
__Method__: GET  
__Variables__: *none*  
__Output__:  array[ `title` -- name of book, `authors` -- authors of the book, `thumbnail` -- url to thumbnail picture , language [ `code` -- short name,  `name` -- proper country name ], `pages` -- page count ]  

__Example__:   
`
	[   
		{"title": "Excel 2010 Introduction: Part I",  
		"subtitle": null,  
		"authors": "Stephen Moffat, The Mouse Training Company",  
		"isbn": "978-87-7681-804-3",  
		"edition": 1,  
		"thumbnail": "http://bookboon.com/en/textbooks/excel-2010-introduction-part-i.180.jpg",  
		"language": {  
			"code": "en",  
			"name": "English"  
		},  
		"published": "2011-07-07T00:00:00",  
		"abstract": "This free Excel 2010 eBook should be used as a point of reference after following attendance of the advanced level Excel 2010 training course.",  
		"rating": {  
			"average": 4.1641998291015625,  
			"count": 134  
		},  
		detail: [{  
			"title": "Description"  
			"body": "..."  
			}, {  
			"title": "Content"  
			"body": "..."  
			}, {  
			"title": "Author"  
			"body": "..."  
			}, {  
			"title": "Preface"  
			"body": "..."  
			}, {  
			"title": "Appendix"  
			"body": "..."  
			}  
		],  
		"pages": 128}  
	]
`

## /books/`<guid>`/download 
__Method__: POST  
__Variables__: *none*   
__Output__: 302 Redirect

# /questions  
__Method__: POST  
__Variables__: `answer` -- post back variable for answers received.  
__Output__: array [ `question` -- question text to display, answers [ `_id` -- answer guid to post back, `text` -- answer text to display ] ]   

__Example__:  
`
	[ 
		{"question":"You are in",  
		"answers":[  
			{"_id":"ee82be8a-c04b-e011-bd88-22a08ed629e5","text":"United Kingdom"},  
			.....  
		]  
	]
`


# /recommendations
__Method__: GET  
__Variables__: `books` -- give recommendation based on these books  
__Output__:  array[ `_id` -- guid for book, `title` -- name of book, `thumbnail` -- url to thumbnail picture , language [ `code` -- short name,  `name` -- proper country name ] ]  

__Example__:   
`
	[ 
		{"_id":"c7d5ee13-0f5e-e011-bd88-22a08ed629e5",  
		"title":"Long-Term Assets",  
		"thumbnail":"http://bookboon.com/uk/textbooks/long-term-assets.180.jpg",  
		"language":{"code":"en","name":"English"}}, ...  
	]
`
