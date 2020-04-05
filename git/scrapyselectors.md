# XPath and CSS Selectors in Scrapy

Web scraping is the process of data extraction from websites using a web scraping/crawling framework such as Scrapy. When you are scraping web pages, you need toy extract a certain part of the HTML source by using a mechanism called selectors, which are accessible by using either [XPath][XPath-doc] or [CSS][CSS-doc] expressions. These expressions are called selectors because they “select” certain parts of the HTML document specified either by XPath or CSS expressions.

XPath is a language for selecting nodes in XML documents, which can also be used with HTML. CSS is a language for applying styles to HTML documents. Either type of selector can be used in Scrapy for extracting data, but only XPATH can be used for certain complex queries because it is able to access more elements of the document. 

### Installing Scrapy

  - To install Scrapy, run the command: 
  
    ```sh
    $ pip install scrapy
    ```
    **Note:** To do this, you must have pip installed. Please see “Pre-Work: Python Installation” for more information.
    
### Creating a Project

- To create a new project in Scrapy, use the command below with your desired project_name: 
  
    ```sh
    $ scrapy startproject <project_name>
    ```
### Tutorials & Documentation
- [Scrapy Intro Tutorial][intro-tutorial]
- [Selectors in Scrapy documentation][selectors-doc]

### Scrapy Selectors Reference

* **XPath Selectors** - written in format: response.xpath('XPath selector here')
	E.g. response.xpath('//div')

* **CSS Selectors** - written in format: response.css('CSS selector here')
	E.g response.css('div')

    **Note:** All XPath and CSS use 1-based indexing (for referencing table cells, ect.)

| Shortcut | XPath Selector | CSS Selector |
| ------ | ------ | ------ |
| Queries response | response.xpath() | response.css()
| Select root element | /html | html
| Select all div elements | //div | div
| Select all attribute values of name (e.g. of "href")  | //a/@href | a::attr(href)
| Return value of first matched element (e.g. of attribute name "href")  | ("//a/@href").get() | ('a::attr(href)').get()
| Return all values of an element (e.g. of attribute name "href")  | ("//a/@href").getall() | ('a::attr(href)').getall() 
| Extract text data of only first matched element **same behavior as get() | Selector.extract_first() **e.g.** ('//title/text()').extract_first() | Selector.extract_first() **e.g.** ('title::text').extract_first()
| Extract text data of a selected element (returns None if no elements found) **same behavior as getall() | Selector.extract() | Selector.extract()
| Selects <div> on the page with an attribute called “class” | //div[@class] | div.class
| Select <div> with class attribute “someAttr” | //div[@class='someAttr'] | div.someAttr *Note: don’t have to specify class
| Select elements with id “someID” | //div[@id='someID'] | div#someID **Or use attribute notation: div[id="someID"]
| Select image element | //img | img
| Select <a> containing text ‘someText’ | //a[contains(text(),'someText')] | a:contains('someText')
| [Remove namespaces][remove-namespaces] | Selector.remove_namespaces() | Selector.remove_namespaces()
| Apply the given regex and return a list of matching unicode strings |  Selector.re(regex) | Selector.re(regex)
| Select table with id “tableName” | //table[@id='tableName'] | #tableName
| Select cell (e.g. 3rd row, 2nd column) of table with id “tableName” | //*[@id='tableName']//tr[3]//td[2] | #tableName tr:nth-child(3) td:nth-child(2)
| Select all elements | //* | *
| Select all attributes | //@* | *[attr]

[XPath-doc]: <https://docs.scrapy.org/en/xpath-tutorial/topics/xpath-tutorial.html>
[CSS-doc]: <https://www.w3.org/TR/selectors>
[intro-tutorial]: <https://docs.scrapy.org/en/latest/intro/tutorial.html>
[selectors-doc]: <https://docs.scrapy.org/en/latest/topics/selectors.html>
[remove-namespaces]: <https://docs.scrapy.org/en/latest/topics/selectors.html#removing-namespaces>

   
