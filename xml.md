# XML parsing

To read xml document with terminal we can use **xmllint** tool.

Lets say we have a file named **1.xml** with the below content:
```
<?xml version="1.0" encoding="utf-8"?>  
<item>  
  <definition test="abc">v. to provide a place to sleep or live</definition>  
  <definition>def2</definition>  
  <word>accommodates</word>  
</item>
```

**Get elements:**

`xmllint --xpath "/item/definition" 1.xml`

`Output: <definition test="abc">v. to provide a place to sleep or live</definition><definition>def2</definition>`

**Get text of elements:**

`xmllint --xpath "//item/word/text()" 1.xml`

`Output: accommodates`

**Get attributes:**

`xmllint --xpath "/item/definition/@test" 1.xml`

`Output:  test="abc"`

**Select elements by its attribute:**

`xmllint --xpath "/item/definition[@test='abc']" 1.xml`

`Output: <definition test="abc">v. to provide a place to sleep or live</definition>`

---

**Search element by part of text:**

`xmllint --xpath "//*[contains(*,'sleep')]" 1.xml`

**Search element by part of attribute:**

`xmllint --xpath "//*[contains(@test,'bc')]" 1.xml`

**Parse HTML URL:**

`xmllint --html --xpath //div/a  "http://blog.mbirgin.com"`

**Parse HTML and ignore error messages:** 

`curl -s http://www.mbirgin.com | xmllint --html  --xpath '(//td[contains(@class,"lastpost") and contains(@class,"windowbg2")])[1]/text()'  2>/dev/null -`
