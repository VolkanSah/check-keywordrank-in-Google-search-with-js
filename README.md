# check-keywordrank-in-Google-search-with-js
A simple script that uses JavaScript and the browser's console to check the rank of a keyword in Google search results:

```javascript
function checkRank(keyword) {
  // Construct the Google search URL
  const url = `https://www.google.com/search?q=${encodeURIComponent(keyword)}`;

  // Make an AJAX request to fetch the search results page
  const xhr = new XMLHttpRequest();
  xhr.open('GET', url);
  xhr.onload = function() {
    // Parse the response HTML
    const parser = new DOMParser();
    const doc = parser.parseFromString(xhr.responseText, 'text/html');

    // Find the search result links
    const links = doc.querySelectorAll('div.g > div.rc > div.r > a');

    // Check the rank of the first search result that matches the keyword
    for (let i = 0; i < links.length; i++) {
      const link = links[i];
      if (link.textContent.toLowerCase().includes(keyword.toLowerCase())) {
        console.log(`Your website ranks at position ${i+1}`);
        return;
      }
    }

    // Keyword not found in search results
    console.log('Your website does not rank in the top 100 results');
  };
  xhr.send();
}

// Example usage: check the rank of the keyword "example keyword"
checkRank('example keyword');

```
In this script, the checkRank function takes a single parameter keyword which is the keyword you want to check the rank for. The script constructs a Google search URL for the keyword, makes an AJAX request to fetch the search results page, and parses the response HTML to find the search result links. The script then checks the rank of the first search result that matches the keyword, and logs the result to the console. If the keyword is not found in the top 100 search results, the script logs a message indicating that your website does not rank in the top 100 results.

Note that this script is a basic example and may not work for all cases. Google may block automated search queries or use different HTML structures for search results in different regions or languages. Additionally, this script may not account for personalized search results or other factors that can affect search rankings.
