# Markdown
<center>[Home](../index.html)</center>

[TOC]

## Insert blockquotes

* **Format:**  

<div class="prism-show-language"><div class="prism-show-language-label">Markdown</div></div>
```
> Blockquotes are very handy in email to emulate reply text.
> This line is part of the same quote.

Quote break.

> This is a very long line that will still be quoted properly when it wraps. Oh boy let's keep writing to make sure this is long enough to actually wrap for everyone. Oh, you can *put* **Markdown** into a blockquote. 
```

* **Result:**  

> Blockquotes are very handy in email to emulate reply text.
> This line is part of the same quote.

Quote break.

> This is a very long line that will still be quoted properly when it wraps. Oh boy let's keep writing to make sure this is long enough to actually wrap for everyone. Oh, you can *put* **Markdown** into a blockquote. 

## Insert code

### Normal code
> To insert code you just have to type this:

<div class="prism-show-language"><div class="prism-show-language-label">Markdown</div></div>
```
	```language
		your code here
	```
```

### Highlighted code
> To insert highlighted code, you have to add the language name after the first **```**.  
> [List of the supported languages](https://support.codebasehq.com/articles/tips-tricks/syntax-highlighting-in-markdown)

* **Format:**

<div class="prism-show-language"><div class="prism-show-language-label">Markdown</div></div>
```
	```python
		def facto(x):
			if (x == 0 or x == 1):
				return 1
			return x * facto(x - 1)
	```
```
* **Result:**  

```python
	def facto(x):
		if (x == 0 or x == 1):
			return 1
		return x * facto(x - 1)
```

## Make a table of content

> It's pretty simple, all you have to do is to type ```[TOC]``` wherever you want to have it.

## Make an array

> Colons can be used to align columns.

* **Format:**  

<div class="prism-show-language"><div class="prism-show-language-label">Markdown</div></div>
```
| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |
```

* **Result:**  

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

> There must be at least 3 dashes separating each header cell.  
> The outer pipes (|) are optional, and you don't need to make the  raw Markdown line up prettily. You can also use inline Markdown.

* **Format:**  

<div class="prism-show-language"><div class="prism-show-language-label">Markdown</div></div>
```
Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3
```

* **Result:**  

Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3

## Help

[Help](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)


***

<center>ToolKit © 2017</center><center><a href="http://alexandre-ducobu.esy.es/En">About</a> </center>
