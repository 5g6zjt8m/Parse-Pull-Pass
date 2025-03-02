# Detailed breakdown

[Previous Page (Top level logic)](/AutoReportFwd/readme.md) | [Back home](/README.md)

# Flow

These are the steps expanded, with json included. The json itself helps give some insight into what is being referenced.

![1](/AutoReportFwd/Flow/Screenshots/1.png)

Triggers the flow. Specifies ``user``'s inbox, with emails coming from ``external.report@noreply.com`` with the string ``Report generated!`` in the subject.

[Peek Code](/AutoReportFwd/Flow/PeekCode/1.json)

_

![2](/AutoReportFwd/Flow/Screenshots/2.png)

This needs to be here because it is much easier and more reliable to substring normal text instead of HTML. This also means that this flow will survive any changes the organization makes to email formatting, like modifying banners.

It simply grabs the body of the email (as it is formatted in HTML) and gets rid of the HTML formatting.

[Peek Code](/AutoReportFwd/Flow/PeekCode/2.json)

_

![3](/AutoReportFwd/Flow/Screenshots/3.png)

Most technical step. Grabs the ``Acct#`` with the following expression:

``substring(string(outputs('Html_to_text')?['body']), add(indexOf(string(outputs('Html_to_text')?['body']), 'SL/HT'), 12), 8)``

[Peek Code](/AutoReportFwd/Flow/PeekCode/3.json)

_

![4](/AutoReportFwd/Flow/Screenshots/4.png)

Uses the ``Message Id`` of the original email to specify which email to reply to. I added in a message identifier into the body for fun. Specifies to direct this reply to ``internal.processing@example.com``, and formats the subject as "Report regarding Acct# ``Acct#``", using the variable.

[Peek Code](/AutoReportFwd/Flow/PeekCode/4.json)

_

![5](/AutoReportFwd/Flow/Screenshots/5.png)

Specifies the email that arrived, and moves it into a specified folder in ``user``'s inbox.

[Peek Code](/AutoReportFwd/Flow/PeekCode/5.json)

[Previous Page (Top level logic)](/AutoReportFwd/readme.md) | [Back home](/README.md)
