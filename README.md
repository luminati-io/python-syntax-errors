# Avoiding and Fixing Python Syntax Errors

[![Promo](https://github.com/luminati-io/LinkedIn-Scraper/raw/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner.png)](https://brightdata.com/) 

This guide explains common Python syntax errors, what proactive strategies to use to prevent then, and what reactive methods to use to resolve them efficiently:

- [Types of Syntax Errors](#types-of-syntax-errors)
- [Avoiding Syntax Errors](#avoiding-syntax-errors)
  - [Proactive Strategies](#proactive-strategies)
  - [Reactive Strategies](#reactive-strategies)

## Syntax Errors in Python

The [Python Interpreter](https://docs.python.org/3/tutorial/interpreter.html) executes Python code, translating it to machine language. If syntax rules are violated, execution stops, and an error message with a traceback is displayed.

Syntax errors arise from structural mistakes, similar to grammatical errors in language. For example, Python requires correct indentation for blocks like `if` statements and loops.

Unlike [runtime errors](https://docs.python.org/3/library/exceptions.html#RuntimeError), which occur while a program runs, syntax errors prevent execution entirely.

## Types of Syntax Errors

Python follows many [syntax rules](https://peps.python.org/pep-0008/), making syntax errors common. This section explores several frequent errors and their solutions.

### Misplaced, Missing, or Mismatched Punctuation

Python relies on punctuation marks to structure code. Ensure they are correctly placed and properly matched to avoid syntax errors.

For example, parentheses `()`, brackets `[]`, and braces `{}` must always be used in pairs. If you open one, you must close it.

In the example below, a curly brace is left unclosed:

```python
# Incorrect
proxies = {
    'http': proxy_url,
    'https': proxy_url

```

If you try to run this, the interpreter throws a `SyntaxError`:

```python
File "python-syntax-errors.py", line 2
    proxies = {
            ^
SyntaxError: '{' was never closed
```

The Python interpreter provides a detailed error message, including the file name, line number, and an arrow indicating where the error occurred. Here, it specifies that `'{' was never closed`.

With this information, you can easily identify and fix the issue by closing the curly brace.

```python
# Correct
proxies = {
    'http': proxy_url,
    'https': proxy_url
} # Closed a curly bracket
```

Quotes (`'` or `"`) often cause issues in Python. Like many programming languages, Python uses quotes to define strings. Always ensure the same type of quote is used to open and close a string.

```python
# Incorrect
host = "brd.superproxy.io'
```

Mixing up single and double quotes results in a syntax error:

```python
File "python-syntax-errors.py", line 2
    host = "brd.superproxy.io'
        ^
SyntaxError: unterminated string literal (detected at line 2)
```

Here, the interpreter tells you that you haven’t terminated the string literal in the second line:

```python
# Correct
host = "brd.superproxy.io"
```

When a string contains both single and double quotes, use triple quotes (`'''` or `"""`) to enclose the string, like this:

```python
quote = """He said, "It's the best proxy service you can find!", and showed me this provider."""
```

Commas separate items in lists, tuples, and function arguments. Missing a comma can cause unexpected errors.

```python
# Incorrect
proxies= [
    {"http": "http://123.456.789.1:8080", "https": "https://123.456.789.1:8080"}
    {"http": "http://98.765.432.1:3128", "https": "https://98.765.432.1:3128"}
    {"http": "http://192.168.1.1:8080", "https": "https://192.168.1.1:8080"}
]
```

Running this code results in the following error message:

```python
File "python-syntax-errors.py", line 3
{"http": "http://123.456.789.1:8080", "https": "https://123.456.789.1:8080"}
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
SyntaxError: invalid syntax. Perhaps you forgot a comma?
```

Error messages are helpful but may not catch all issues. If a missing comma is detected, check the surrounding code for other missing commas to ensure proper syntax.

```python
# Correct
proxies = [
    {"http": "http://123.456.789.1:8080", "https": "https://123.456.789.1:8080"},
    {"http": "http://98.765.432.1:3128", "https": "https://98.765.432.1:3128"},
    {"http": "http://192.168.1.1:8080", "https": "https://192.168.1.1:8080"}
]
```

In contrast to commas, colons are used to start a new block of code (like in an `if` statement or `for` loop):

```python
import requests
from bs4 import BeautifulSoup

# Incorrect
response = requests.get('https://example.com')
if response.status_code == 200
    soup = BeautifulSoup(response.content, 'html.parser')
    title = soup.title.text
    print(title)
)
```

Forgetting a colon results in the following syntax error:

```python
if response.status_code == 200
    ^
SyntaxError: expected ':'   
```

From this error message, it’s easy to determine that there’s a colon missing, and you can add it in the suggested place to fix the issue:

```python
import requests
from bs4 import BeautifulSoup

# Correct
response = requests.get('https://example.com')
if response.status_code == 200:
    soup = BeautifulSoup(response.content, 'html.parser')
    title = soup.title.text
    print(title)

```

### Misspelled, Misplaced, or Missing Python Keywords

[Python keywords](https://docs.python.org/3/reference/lexical_analysis.html#keywords) are reserved words with specific meanings and cannot be used as variable names. Misspelling, misplacing, or omitting a keyword causes an error.

For example, misspelling the `import` keyword when importing the `requests` and `pprint` modules can lead to issues.

```python
# Incorrect
improt requests
import pprint
```

This misspelling causes the interpreter to raise the following `invalid syntax` error:

```python
File "python-syntax-errors.py", line 2
    improt requests
        ^^^^^^^^
SyntaxError: invalid syntax
```

Some error messages can be vague, requiring extra attention. In this case, the arrow points to `requests`, indicating where the syntax error was detected. Since a misspelled module name doesn’t cause a syntax error, the issue is likely a misspelled `import` keyword.

Correcting `import` resolves the error.

```python
# Correct
import requests
import pprint
```

It’s also possible to mess up the `from ... import …` statement like this:

```python
import BeautifulSoup from bs4
```

Although it seems okay, running the preceding code results in an error because the `from` keyword should go before `import`:

```python
File "python-syntax-errors.py", line 2
import BeautifulSoup from bs4
    ^^^^
SyntaxError: invalid syntax
```

Switching `from` and `import` fixes the issue:

```python
from bs4 import BeautifulSoup
```

Forgetting a keyword can cause various errors in Python. This issue is subtle, as different errors may appear depending on the missing keyword.

For example, omitting the `return` keyword in a function meant to return a value can lead to unexpected behavior.

```python
def fetch_data():
    response = requests.get('https://example.com')
    soup = BeautifulSoup(response.content, 'html.parser')
    data = soup.find_all('div', class_='data')
    # Missing a return statement here
    
data = fetch_data()
```

This does not throw a syntax error, but the function returns `None` instead of the expected result. Adding the `return` keyword fixes the preceding code:

```python
def fetch_data():
    response = requests.get('https://example.com')
    soup = BeautifulSoup(response.content, 'html.parser')
    data = soup.find_all('div', class_='data')
    return data

data = fetch_data()
```

If you forget the `def` keyword when defining a function, you encounter a syntax error:

```python
# Missing the `def` keyword
fetch_data():
    response = requests.get('https://example.com')
    soup = BeautifulSoup(response.content, 'html.parser')
    data = soup.find_all('div', class_='data')
    return data

data = fetch_data()
```

The preceding code raises a syntax error because the interpreter expects a keyword before the function name:

```python
File "python-syntax-errors.py", line 1
   fetch_data():
               ^
SyntaxError: invalid syntax
```

Adding the `def` keyword resolves the error:

```python
def fetch_data():
    response = requests.get('https://example.com')
    soup = BeautifulSoup(response.content, 'html.parser')
    data = soup.find_all('div', class_='data')
    return data

data = fetch_data()
```

Forgetting the `if` keyword in a conditional statement causes an error, as the interpreter expects a keyword before the condition.

```python
import requests
from bs4 import BeautifulSoup

response = requests.get('https://example.com')
# Missing the if keyword
response.status_code == 200:
    soup = BeautifulSoup(response.content, 'html.parser')
    title = soup.title.text
    print(title)
```

```python
File "python-syntax-errors.py", line 6
   response.status_code == 200:
                              ^
SyntaxError: invalid syntax
```

You just need to include the `if` keyword to fix this issue:

```python
import requests
from bs4 import BeautifulSoup

response = requests.get('https://example.com')
if response.status_code == 200:
    soup = BeautifulSoup(response.content, 'html.parser')
    title = soup.title.text
    print(title)
```

> **Note**:
> Missing keywords can throw other kinds of errors, too, so be extra careful.

### Incorrect Use of the Assignment Operator

In Python, `=` is for [assignment](https://docs.python.org/3/reference/expressions.html), while `==` is for [comparison](https://docs.python.org/3/library/stdtypes.html#comparisons). Confusing them can result in a syntax error.

```python
import requests
from bs4 import BeautifulSoup

# Incorrect
response = requests.get('https://example.com', proxies=proxies)
if response = requests.get('https://example.com/data', proxies=proxies):
    soup = BeautifulSoup(response.content, 'html.parser')
    data = soup.find_all('div', class_='data')
    for item in data:
    print(item.text)
else:
    print("Failed to retrieve data")
```

In the previous code, the interpreter correctly detects what caused the problem:

```python
File "python-syntax-errors.py", line 5
if response = requests.get('https://example.com/data', proxies=proxies)
     ^^^^^^
```

Here, you're checking if the response matches the result of `request.get()`. To fix the error, replace the assignment operator (`=`) with the comparison operator (`==`) in the `if` statement.

```python
import requests
from bs4 import BeautifulSoup

# Correct
response = requests.get('https://example.com', proxies=proxies)
# Change in the following line
if response == requests.get('https://example.com/data', proxies=proxies):
    soup = BeautifulSoup(response.content, 'html.parser')
    data = soup.find_all('div', class_='data')
    for item in data:
    print(item.text)
else:
    print("Failed to retrieve data")
```

### Indentation Errors

Python relies on indentation to define code blocks. Incorrect indentation prevents the interpreter from recognizing the block structure, leading to an `IndentationError`.

```python
# Incorrect
async with async_playwright() as playwright:
await run(playwright)
```

In the previous example, the block definition (after a colon) lacks indentation. Running the code results in an error.

```python
File "python-syntax-errors.py", line 2
    await run(playwright)
    ^
IndentationError: expected an indented block after the with statement on line 1
```

To fix this problem, follow Python’s syntax rules and indent the code block correctly:

```python
# Correct
async with async_playwright() as playwright:
    await run(playwright)
```

### Issues with Variable Declarations

Variable names must start with a letter or an underscore and can contain only letters, numbers, and underscores. Python is case-sensitive, so `myvariable`, `myVariable`, and `MYVARIABLE` are distinct.

A variable name cannot start with a number. The example below violates this rule by beginning with `1`.

```python
# Incorrect
1st_port = 22225
```

When you run the preceding code, the interpreter raises a `SyntaxError`:

```python
File "python-syntax-errors.py", line 2
    1st_port = 1
    ^
SyntaxError: invalid decimal literal
```

To fix this, you must start the variable name with a letter or an underscore. Any of the following options can work:

```python
# Correct
first_port = 22225
port_no_1 = 22225
```

### Function Definition and Call Errors

To define a function, use the `def` keyword, followed by the function name, parentheses, and a colon. When calling a function, use its name followed by parentheses. Omitting any of these elements results in a syntax error.

```python
import requests
from bs4 import BeautifulSoup

# Incorrect
def fetch_data
response = requests.get('https://example.com')
soup = BeautifulSoup(response.content, 'html.parser')
data = soup.find_all('div', class_='data')
return data

# Incorrect
data = fetch_data
```

In this example, missing elements cause multiple syntax errors. To fix them, add parentheses and a colon after `fetch_data` in the function definition and parentheses after the function call in the last line.

```python
import requests
from bs4 import BeautifulSoup

# Corrected
def fetch_data():
    response = requests.get('https://example.com')
    soup = BeautifulSoup(response.content, 'html.parser')
    data = soup.find_all('div', class_='data')
    return data

# Corrected
data = fetch_data()

```

Missing parentheses or colons in a function definition always causes a syntax error. However, forgetting parentheses when calling a function (`fetch_data()`) may not trigger an exception, leading to unexpected behavior.

## Avoiding Syntax Errors

Writing error-free code is a skill that comes with practice. Understanding and implementing the following best practices can help you avoid common syntax errors.

### Proactive Strategies

The best way to handle syntax errors is to prevent them. Before starting a project, familiarize yourself with the most common syntax rules of the language.  

#### Use a Code Editor with Syntax Highlighting and Indentation Checking

A good code editor helps avoid syntax errors with features like syntax highlighting and indentation checking. These tools can spot issues before you run your code.

For example, a red mark in the editor may indicate a missing colon in `if response.status_code == 200`.

![A red mark suggesting there is an error ](https://brightdata.com/wp-content/uploads/2024/08/A-red-mark-suggesting-there-is-an-error-1024x525.png)

#### Follow Consistent Coding Style Guidelines

Consistency is key to writing clean, error-free code. Following a consistent style improves readability and makes errors easier to spot.

In Python, the [PEP 8 Style Guide](https://peps.python.org/pep-0008/) is the standard, offering guidelines on variable naming, indentation, and whitespace usage.

#### Write Code in Small, Well-Defined Functions

Breaking code into small, well-defined functions improves manageability and debugging. Each function should serve a single, clear purpose. Functions that do too much become harder to understand and debug.

For example, consider the `scrape_and_analyze()` function:

```python
import requests
from bs4 import BeautifulSoup
from textblob import TextBlob

def scrape_and_analyze():
    url = "https://example.com/articles"
    response = requests.get(url)
    soup = BeautifulSoup(response.content, "html.parser")
    titles = soup.find_all("h2", class_="article-title")
    sentiments = []
    for title in titles:
    title_text = title.get_text()
    blob = TextBlob(title_text)
    sentiment = blob.sentiment.polarity
    sentiments.append(sentiment)
    return sentiments

print(scrape_and_analyze())

```

In this example, it would be more readable to break down this function into multiple smaller ones, each executing a smaller, more manageable portion of code:

```python
import requests
from bs4 import BeautifulSoup
from textblob import TextBlob

def scrape_titles(url):
    """Scrape article titles from a given URL."""
    response = requests.get(url)
    soup = BeautifulSoup(response.content, "html.parser")
    titles = soup.find_all("h2", class_="article-title")
    return [title.get_text() for title in titles]

def analyze_sentiment(text):
    """Analyze sentiment of a given text."""
    blob = TextBlob(text)
    return blob.sentiment.polarity

def analyze_titles_sentiment(titles):
    """Analyze sentiment of a list of titles."""
    return [analyze_sentiment(title) for title in titles]

def scrape_and_analyze(url):
    """Scrape titles from a website and analyze their sentiment."""
    titles = scrape_titles(url)
    sentiments = analyze_titles_sentiment(titles)
    return sentiments

url = "https://example.com/articles"
print(scrape_and_analyze(url))
```

### Reactive Strategies

Despite best efforts, errors can still occur. Python provides error messages that describe the issue and its location.

#### Read Error Messages Carefully

Python error messages provide details about the issue and its location. Carefully analyzing them can help identify the problem and find a solution.

#### Use Print Statements Strategically

Using `print()` statements is a quick way to trace execution flow and inspect variable values in small projects. It’s useful for rapid debugging but should not be used in production due to security and performance risks.

For complex issues or larger codebases, a debugger is more effective. Debuggers allow setting breakpoints, stepping through code, and inspecting variables across multiple function calls, providing a more controlled debugging process.

#### Leverage Online Resources and Communities

If you're stuck on a tricky error, don’t hesitate to seek help. Online resources like the [Python Docs](https://docs.python.org/3/) and [Real Python](https://realpython.com/) offer valuable guidance. Communities such as [r/Python](https://www.reddit.com/r/Python/), [r/LearnPython](https://www.reddit.com/r/learnpython/), [Stack Overflow](https://stackoverflow.com/questions/tagged/python), and the [Python Forum](https://python-forum.io/) are great places to find answers and solutions.

## Conclusion

Whether you need reliable proxies, automated data collection, [ready-to-use datasets](https://brightdata.com/products/datasets), or [automation of web scraping tasks](https://brightdata.com/products/web-scraper), Bright Data offers solutions that can make your web scraping projects more efficient and productive.

Sign up now to find the right product for your needs and start a free trial today!