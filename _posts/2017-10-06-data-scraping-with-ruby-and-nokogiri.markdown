---
layout: 'post'
title: 'Data Scraping with Ruby and Nokogiri'
date: 2017-10-06
author: 'Kristyn Bryan'
excerpt: 'Data scraping (also called web scraping) is the process of extracting information from websites. Data scraping focuses on transforming website content (usually HTML) into structured data which can be stored in a database or a spreadsheet. One way to do this it to use Ruby and a gem called **Nokogiri**.'
twitter: 'LEAVE BLANK IF NO TWITTER'
github: 'https://github.com/kristynrb'
website: 'http://kristynbryan.com/'
---

## Setup
1. Create a folder for this tutorial.

2. Create and open a ruby file with your text editor.

3. From inside the tutorial folder, install the gem Nokogiri:
  - `gem install nokogiri` OR some of you might need to `sudo install gem nokogiri`.
  - This will take a few minutes. To confirm that it was installed, you can run `gem list` to show all of your Ruby gems.

3. At the top of your Ruby file, require `Nokogiri` and `open-uri`:
  - `require "open-uri"`
  - `require "Nokogiri"`

## Let's scrape!

We're going to be following [the Nokogiri documentation](http://www.nokogiri.org/tutorials/parsing_an_html_xml_document.html#from_a_string) to help us with our data scraping.

1. Let's get all of the data from a website! Add a webiste to `doc = Nokogiri::HTML(open("THEWEBADDRESS")` and let the scraping begin!
  - Enter the code in your Ruby file:
    - `doc = Nokogiri::HTML(open("http://www.rickastley.co.uk"))`
  - We're going to want to see what is being saved to the `doc` variable (which should be all of the html from that web page).
    - `puts doc`
  - To run the file, put the keyword `ruby` followed by the name of your file in your terminal.
    - Ex: `ruby scraper.rb`
  - Look to your terminal to see the output of all of the scraped data for this site.

<hr>

2. Let's look at data from another site.

  - I want to get all of the information about Netflix Original Series. Let's open this site in our browser and update our code:
    - `https://en.wikipedia.org/wiki/List_of_original_programs_distributed_by_Netflix`

  - Your code should look like:

  ```ruby
doc = Nokogiri::HTML(open("https://en.wikipedia.org/wiki/List_of_original_programs_distributed_by_Netflix"))
```
  - To see these **all** of the data on the page, we can output the `doc` variable.

  ```ruby
# in your Ruby file
puts doc
```

  ```ruby
# in your terminal
ruby scraper.rb
```

3. We will use HTML and CSS **selectors** to specify the data that we want. You can inspect the elements on the page to see the selectors that were used. Use your [Chrome Developer Tools ](https://developer.chrome.com/devtools)to do this.

4. Let's grab all of the data from the `table` element on the page (including the HTML elements):
```ruby
puts tableData = doc.css("table")
```

5. If we wanted to see the text that is between the HTML elements, we could just ask for the text:
```ruby
puts tableDataText = doc.css("table").text
```

6. If I wanted all of the titles (and none of the categories), I would write a request like the following:
```ruby
allTitles = doc.css('a').text
```
We got a lot of titles, but they're all crammed together! Let's reformat:

7. Put it in a loop to print out the individual titles:
  ```ruby
allTitles = doc.css('a').each do |item|
  title = item.text
  puts "Title is: #{title}"
end
  ```

## Save the Data

If we want to store the data in its current state, then we could save it in a file and parse from there.

1. Use the `curl` command in your **terminal**, the address of the site, `>>`, and name the file where you'd like to save the data. Note: You don't have to create this file ahead of time. When you run the command in your terminal, you will be pushing and creating the file.

  ```
  curl https://en.wikipedia.org/wiki/List_of_original_programs_distributed_by_Netflix >> netflix_data.html
  ```

- You can use the Nokogiri parser on this file by switching out the web address to the location of the file. The only difference is the word `File` prefixed to `open`.

    ```ruby
    doc = Nokogiri::HTML(File.open("netflix_data.html"))
    ```

3. We can parse through the data the same way as when we were parsing from the web.

  ```ruby
  puts tableData = doc.css("table").text
  ```

## Help with Selectors:
Use [this link](http://ruby.bastardsbook.com/chapters/html-parsing/) for help with HTML and CSS selectors.

## More info about the legality of data scraping
[Terms of use for scraping](http://info.sagenceconsulting.com/blog/is-your-spidey-sense-tingling-the-three-cs-of-web-scraping)
