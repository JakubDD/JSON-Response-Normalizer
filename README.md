#JSON_Response_Normalizer
JSON Response Normalizer
 https://roadmap.sh/projects/js-json-response-normalizer
A small utility that normalizes a bloated API response into a compact list of published article summaries.

Problem

An API response often contains more data than a program actually needs (extra metadata, nested objects, unpublished items, etc.). This exercise extracts only the relevant, published articles and reshapes them into a flat, minimal summary object.

Functions
getPublishedArticles(response)

Filters the data array of the API response and returns only the articles whose status is "published".

Parameter: response — the full API response object (must have a data array).
Returns: an array of raw article objects with status === "published".
Does not mutate the original response object (.filter() returns a new array).
toArticleSummary(article)

Converts a single raw article object into a smaller "summary" object by picking and flattening only the needed fields.

Parameter: article — a single raw article object (expects id, title, author.name, and stats.views).
Returns: an object shaped as:
js
  { id, title, authorName, views }
normalizeArticles(response)

Combines the two functions above: filters the published articles, then maps each one to its summary form.

Parameter: response — the full API response object.
Returns: an array of article summaries ({ id, title, authorName, views }) for published articles only.
Usage
js
const summaries = normalizeArticles(apiResponse);
console.log(summaries);
Example Output

Given the sample apiResponse (3 articles, 2 published):

https://roadmap.sh/projects/js-json-response-normalizer

js
console.log(normalizeArticles(apiResponse));
// [
//   { id: 'a1', title: 'Learning JavaScript', authorName: 'Ava Stone', views: 1200 },
//   { id: 'a3', title: 'Async Basics', authorName: 'Mina Patel', views: 900 }
// ]

console.log(getPublishedArticles(apiResponse).length);
// 2

console.log(toArticleSummary(apiResponse.data[0]));
// { id: 'a1', title: 'Learning JavaScript', authorName: 'Ava Stone', views: 1200 }
Concepts Covered
Array filtering with .filter()
Array transformation with .map()
Function composition (normalizeArticles builds on getPublishedArticles and toArticleSummary)
Accessing and flattening nested object properties (author.name, stats.views)
Immutability — the original response/apiResponse object is never mutated
Running
bash
node index.js
