# /categories
__Status__: Public  
__Method__: GET  
__Variables__:  `lang`  -- ISO 639-1 Language code  
__Output__: array [ `id` -- guid for category, `name` -- name of category ]  

__Raw__:  
	[ 
		{"id":"6ec2991a-d6b2-e011-b817-22a08ed629e5","name":"Travel guides"},  
		{"id":"6dc2991a-d6b2-e011-b817-22a08ed629e5","name":"Textbooks"},  
		{"id":"6cc2991a-d6b2-e011-b817-22a08ed629e5","name":"Business"}  
	]

## /categories/`<guid>`
__Status__: Public  
__Method__: GET  
__Variables__:  `lang`  -- ISO 639-1 Language code  
__Output__: `name` -- name of the section,  
`title` -- subtitle
`description` -- long description of contents
categories [ `id` -- guid for category, `name` -- name of category ],
books [ `id` -- guid for book,
`name` --

__Raw__:
	{
		"name":"Textbooks","title":"Download free textbooks online","description":"long description text",  
		"categories":  
		[  
				{"id":"3e2e64e2-0965-e011-bd88-22a08ed629e5","name":"Accounting"}, ....  
		],  
		"books":[]  
	}

# /search
__Status__: Public  
__Method__: GET  
__Variables__: `lang`  -- ISO 639-1 Language code  
`q`  -- Search string 
__Output__:  array[ `id` -- guid for book, `title` -- name of book, `thumbnail` -- url to thumbnail picture , language [ `code` -- short name,  `name` -- proper country name ] ]  

__Raw__:  
	[   
		{"id":"d2d5ee13-0f5e-e011-bd88-22a08ed629e5","title":"Essentials of Macroeconomics:Exercises",  
		"thumbnail":"http://bookboon.com/uk/textbooks/macroeconimics-exercisebook.180.jpg",  
		"language":{"code":"en","name":"English"}},  
		....  
	]  

# /books/`<guid>`
__Status__: Public  
__Method__: GET  
__Variables__: *none*  
__Output__:  array[ `title` -- name of book, `authors` -- authors of the book, `thumbnail` -- url to thumbnail picture , language [ `code` -- short name,  `name` -- proper country name ], `pages` -- page count ]  

__Raw__:
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

## /books/`<guid>`/thumbnail
__Status__: Public  
__Method__: GET  
__Variables__: `width` -- width in pixel of returned thumbnail. Accepted value 90, 120, 210 and 380,  
`branding` -- guid for branding (cover page) to be printed in the PDF  
__Output__: binary jpeg image

## /books/`<guid>`/download
__Status__: Authenticated  
__Method__: POST  
__Variables__: `rotation` -- guid for specific rotation to be printed in the PDF,  
`branding` -- guid for branding (cover page) to be printed in the PDF  
__Output__: `url` -- url where the PDF can be retrieved  

__Raw__:
	[ 
		{"url":"http://url.to.pdf.file"}
	]

# /questions
__Status__: Authenticated  
__Method__: POST  
__Variables__: `lang`  -- ISO 639-1 Language code,  
`all` -- output will contain all previously answered questions with `"selected": true`  
`answer` -- post back variable for answers received.  
__Output__: array [ `question` -- question text to display, answers [ `id` -- answer guid to post back, `text` -- answer text to display ] ]   

__Raw__:
	[ 
		{"question":"You are in",  
		"answers":[  
			{"id":"ee82be8a-c04b-e011-bd88-22a08ed629e5","text":"United Kingdom"},  
			.....  
		]  
	]



# /recommendations
__Status__: Authenticated  
__Method__: GET  
__Variables__: `lang`  -- ISO 639-1 Language code  
__Output__:  array[ `id` -- guid for book, `title` -- name of book, `thumbnail` -- url to thumbnail picture , language [ `code` -- short name,  `name` -- proper country name ] ]  

__Raw__:
	[ 
		{"id":"c7d5ee13-0f5e-e011-bd88-22a08ed629e5",  
		"title":"Long-Term Assets",  
		"thumbnail":"http://bookboon.com/uk/textbooks/long-term-assets.180.jpg",  
		"language":{"code":"en","name":"English"}}, ...  
	]

