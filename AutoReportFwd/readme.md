# Top level logic

[Previous Page (Home)](/README.md) | [Next Page (Detailed breakdown)](/AutoReportFwd/Flow/readme.md)

![TopLevel](/AutoReportFwd/Flow/Screenshots/TopLevel.png)

## How does it work? 

The flow is triggered when an email from ``external.reports@noreply.com`` arrives in ``user``'s inbox, with ``Report generated!`` being in the subject line. It will not run if that string is not part of the subject.

- The email received from ``external.reports@noreply.com`` triggers the flow and is parsed into a JSON format.
- The body of the email is extracted and presented as raw HTML content in string format.
- The raw HTML string is then converted into regular text.
- A variable is created, which holds an expression designed to extract the ``Acct#`` from the email body.
- A reply is generated to the received email, with the subject formatted as "Report regarding Acct# ``Acct#``".

## How can it isolate the account number?

This is done with a very modular expression that I created.

``substring(string(outputs('Html_to_text')?['body']), add(indexOf(string(outputs('Html_to_text')?['body']), 'SL/HT'), 12), 8)``

The details on how this expression functions:

``substring`` grabs a portion of text from a larger string using a start position and length, returning only those characters. It needs:
- The string to search through (the HTML-to-text converted output of the email).
- The start position, which is determined using the ``indexOf`` function.
- The length of the string, which is always eight characters for account numbers.

``string`` converts the target content into a string format.

``indexOf`` finds the start position of a specified substring within a string. It requires:
- The string to search through (the HTML-to-text converted email body).
- The substring itself to get the index value for ``Acct#``.

``add`` performs addition between two integers. It requires:
- The first integer, which is the result of ``indexOf`` (indicating where ``Acct#`` begins).
- The second integer, which is always 12 (since the account number is 12 characters after ``Acct#``).

Essentially, the expression retrieves the account number by substringing the HTML-converted email content. It locates the account's start position by finding the index of a fixed substring (``Acct#``) and then adding 12 (another fixed value) to pinpoint the account number’s beginning.

[Previous Page (Home)](/README.md) | [Next Page (Detailed breakdown)](/AutoReportFwd/Flow/readme.md)
