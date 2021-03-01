# Working with JSON data in BigQuery
## TL;DR
* JavaScript Object Notation (JSON) is a popular, semistructured format for sending data around the internet.
* BigQuery supports storing unstructured data as json-formatted strings
* BigQuery also supports functions that make it easy to extract key and value pairs from these strings, including nested objects
* Json-formatted strings can take up lots of space, so when using these functions pay attention to query costs!

## Introduction
*What is JSON? And why do we care?*
JavaScript Object Notation (JSON) is a semistructured format for passing data between two locations. It is [the most popular way](https://twobithistory.org/2017/09/21/the-rise-and-rise-of-json.html) to send and receive information on the internet. When you opened up this article, Medium sent information to a host of services in order to populate this page’s contents, understand which browser is accessing the page, and track the interactions you make on it. The majority of that data hand-holding was in JSON.

One reason for its popularity is it is easy and fast to interpret for both humans and computers. It supports many [common data types](https://www.w3schools.com/js/js_json_datatypes.asp), and supports a flexible data structure. To highlight it’s flexibility, let’s consider a toy example. A JSON object containing some core details about myself could look like:

``` json
{
	"firstName": "Bryan", 
	"lastName": "Holman", 
	"birthCountry": "United States"
}
```

* A good guide to JSON: [An introduction to JSON. A complete beginner’s guide | by Raivat Shah | Towards Data Science](https://towardsdatascience.com/an-introduction-to-json-c9acb464f43e)
* A page about the rise in popularity of JSON: [The Rise and Rise of JSON](https://twobithistory.org/2017/09/21/the-rise-and-rise-of-json.html)

## The functions

`json_query()`

`json_value()`

## End-to-end example

## Summary

## Related reading

