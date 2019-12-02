
> Written with [StackEdit](https://stackedit.io/).

### Add to the end of every line
Let's say we want to add at the end of every line this `);`.

Use `Ctrl` + `H` to open the Replace page. Then use `Regular expressions` and put:

- Find what: `$`
- Replace with: `\);`

### Add to the beginning of every line
Let's say we want to add at the end of every line this `Data_`.

Use `Ctrl` + `H` to open the Replace page. Then use `Regular expressions` and put:

- Find what: `^`
- Replace with: `Data_`

### How to convert from a row to column and from column to row

#### From Column to Row:

- From column to row: `CTRL` + `A` selects all. Then `CTRL` + `J` aligns them in a row.

#### From Row to Column:

Example: 
Let's say we have something like this:
```
['marketer_id', 'calendar_year', 'calendar_date', 'registered_edt']
```

- Go to Search, Find, Replace. Find `,`, Replace `$1\n`, SearchMode: `Regular Expression`. The Find: `,` represent the comma on 

### How to remove blank lines in a file

We can use the Find and Replace option with  regular  express to remove empty lines  
  
1. Press Ctrl + F to open Find  dialog, move to Replace tab  
2. Change the  **Search Mode**  as  **Extended (\n,\r,\t,\0,\x ...)**  
3. Now,  
  
Find : `\r\n`

Replace with blank

#### [How to add single quote “ ' ”at beginning and end of field?](https://stackoverflow.com/questions/34900052/how-to-add-single-quote-at-beginning-and-end-of-field)

If all fields are ALWAYS containing alphanum and dash, you can do:

Ctrl+H

Find what:  `([\w-]+)`  
Replace with:  `'$1'`

Then click on  Replace all

`([\w-]+)`  is a character class that matches alphanumeric character (including underscore) and dash.  
This will replace each field by the same with single quotes arround it.

### [How to delete all lines in a document which has a specific text](https://notepad-plus-plus.org/community/topic/12814/how-to-delete-all-lines-in-a-document-which-has-a-specific-text)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU0MjI4ODIxLDE0NjU1NDY5NjcsLTU3Nz
kwNzQxNywxMzQ1NzMwOTkzLC00MzcxNjQ2NjMsLTEzMjY3OTY0
NzUsNTE1NzE0NzRdfQ==
-->