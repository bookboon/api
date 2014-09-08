# Introduction to the bookboon.com API

The bookboon.com API (the "API") is designed to make bookboon.com books available to 3rd parties that wants have our books deeply integrated into their own application. Because we use stamping of adverts and customized front pages we always need to generate an unique download URL for any permutation of a book. We selected the correct adverts on the basis of questions that must be individually answered by each user prior to downloading.

## Using the API
Before you can access the API you need an ID and secret. You can requset those by writing an email to [tbm@bookboon.com](mailto:tbm@bookboon.com) explaining your project and idea behind integration. Please note that we reserve the right to reject candidate projects on a case-by-case basis.

The user should always be directed to download the books from bookboon.com servers directly, it is not permitted to store or cache the books on your or any other servers. This has the added bonus of saving you tons of bandwidth - if you don't believe us look at [this graph](http://bookboon.com/blog/wp-content/uploads/2012/04/traffic-graph.png).

[API](https://github.com/bookboon/api/blob/master/API.md)

[Reference](https://github.com/bookboon/api/blob/master/Reference.md)

## Wrappers
[PHP Wrapper Class](https://github.com/bookboon/api-php)

[Microsoft .NET DK Class](https://github.com/bookboon/api-net)
