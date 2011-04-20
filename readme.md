# About OPCDataGrid
Check the website for more detail http://xangelo.ca/pages/OPCDataGrid

# Using OPCDataGrid
Due to some work that found its way into my lap, I have been working on updating my old OPCDataGrid code. OPCDataGrid is essentially a way to build a table from a multi-dimensional datasource. With the new update we push OPCDataGrid from version 2.1 to version 2.5. The reason for the jump in versions is simply because the feature set now provided is a bit more robust, and the code has received a small update to make things easier to work with. 

Before I go into it any further I'd suggest grabbing the latest version which I've transitioned away from PHPClasses to GitHub. To be honest, PHPClasses was becoming slower and filled with more crap. I couldn't even use it to properly manage my code, and I don't like users needing to be members of the website to download free code. 

Let's start with the newest feature, Modify.


## Using Modify
Here's our sample data-source: 
IE:
https://gist.github.com/929614

Modifying a row is extremely easy and there is only one condition. The row that you are trying to modify needs to be one of the displayed rows. As in, if you only choose username and email as displayed rows, then you can not modify 'user_id'. However, you _can_ refer to user_id even if it is not displayed.

To modify a row, you need to refer to it by the actual name of the row, not the name you give it. If I renamed `username` to `Users Name` then when I want to modify it, I need to refer to it as `username`. 

The code below will take the "username" column and modify each occurance when we try and build it.
https://gist.github.com/931926

The modify function will modify the field (first argument) by whatever you pass as the 2nd. It accepts anything that will pass `is_callable`.

Note that our anonymous function accepts a single argument that is a zero-index array. The first element of the array is the value of the field. The second is an array of the row that the field appears in. Basically, every time that's called a user has access to all of the fields for that row, even if they are not being displayed.

This update should take care of a lot of the usecases of OPCDataGrid where you want to display a row, but just modify the output slightly (truncate strings, change text into a link, etc). 


## General Use
Here is a very simple snippet of code that pulls some data from the database, instantiates OPCDataGrid with our datasource, modifies the names of the displayed columns and then modifies the contents of the two displayed rows. Then it spits out the html table.

https://gist.github.com/931922