---
layout: post
title:      " Where to check your input/data?"
date:       2019-11-20 20:16:42 -0500
permalink:  cli_project_where_to_check_your_input_data
---


When getting information for your program from an external source, it is important to validate the information to make sure it is in the expected format and has correct values.  This is especially true when getting information from the internet, where trust is less assured.  Input and data validation can be use to prevent security issue, such as SQL injection and buffer overruns or catch and correct/fail safely when an error occurs. For example, if a function has an unexpected edge case that causes garbage output, validation would raise an exception instead of executing on the garbage. 

The CLI project gets a bulk or it’s input from the internet via an API call or website scrapping, thus it is important to validate this data.  Ideal we should validate on all data transformation and inputs (internal and external), however this can greatly slow down the program. Instead we need to strategically use validation where proper data is most important or where the program is most vulnerable. While exact placement will vary based on program needs, run-time/language, and style, below are some of the more common one’s I have seen recommended or in use by other programmers.

1.  When receiving new data
2.  Crossing or changing privilege/trust boundary in program.
3. Critical/Messy code portions

There is an old joke in programming:

"A QA tester is testing a bar, he orders a drink, then he orders 0 drinks , -1 drinks, 100 drinks and infinite drinks. Then a user walks in the bar and asks “where the bathroom is?” and the bar burns down."

Never trust data providers to provide the data in the intended format or the correctly. Data providers can be users at the CLI, API/web scrape results or data in a files.  Always check that data provided to the program from external source is in the correct format, type and range. Even data your program has written itself, such as data files or SQL entries, should be validated as a third-party could have changed them or it is no-longer valid due to random unforeseen reason.

Often a program will need a set of privileges or operate in different trust boundaries, to accomplish it’s task, for example see `ping` on Linux.  Coders following best practice of least privilege will segment the privileges and trust boundaries via a mechanism. Whenever data is passed internally between boundaries or permission segments, the receiving program should check it like new data.

Often an algorithm in a program do not work  flawlessly.  In rare occasions (not always known), it will produce incorrect data. In these cases, it is best to do some validation to ensure the data produced it within the expected acceptable range produced given the inputs provided and if not throw out the results and try again or take another corrective action. 

Finally, the amount of validation will vary, sometimes it is not possible to completely make sure data is correct due to a large valid range or validation would be too time intensive. In this case it is best to use a less rigorous approach. The industry also has a set of tools to help make validation easier.  
