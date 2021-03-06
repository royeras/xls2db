xls2db
======

xls2db is a python program that takes an excel spreadsheet following a certain
schema into an sqlite database that can be opened using python's sqlite3 module.
It can also be used as a module.

Why??
-----

Because fuck you, that's why.

But seriously: I was getting sick of doing data entry for this toy project of
mine using cursor.execute()'s, so I figured I'd try entering the data into an
excel spreadsheet, converting it into the db, and then manipulating it from
there. Crazy, I know.

Usage:
--------

As a script::

    xls2db infile.xls outfile.db

As a module::

    from xls2db import xls2db
    xls2db("infile.xls", "outfile.db")

Alternately, you can use an instance of ``xlrd.Book`` instead of an .xls
filename, and you can use an instance of ``sqlite3.Connection`` instead of an
sqlite database filename. For example::

    from xls2db import xls2db
    import xlrd
    import sqlite3 as sqlite

    db = sqlite.connect(":memory:")
    xls2db(xlrd.open_workbook("infile.xls"), db)


Schema:
-------

Each worksheet represents a table with that name. Each table is written with
headers corresponding to column names/types/etc. expected in an sqlite database,
and the rest of the rows are, well, rows. For example, I have data in a
worksheet called "links" that looks like this::

    src string  dst string  dir string
    kitchen     outside     West
    kitchen     w_hwy       East
    w_hwy       ctr_hwy     East
    ctr_hwy     e_hwy       East
    e_hwy       living      East
    w_hwy       w_bath      North
    ctr_hwy     e_bath      North
    w_hwy       josh_bdr    South
    ctr_hwy     guest_bdr   South
    e_hwy       james_bdr   South

If you're familiar with sql, this probably makes sense. Somewhat.

Installation:
-------------

::

    sudo pip install -U xls2db

Dependencies:
-------------

- xlrd
- xlwt
- plac (for command line args)


Tests:
------

I haven't written any yet, because I'm lazy.

Developers! Developers! Developers!
-----------------------------------

I suspect most of you are stabbing your eyes out with rusty nails. If you're
not, however, why not give it a try? Help me track down some bugs? Fix anything
that seems like it's begging for sql injection?

License:
--------

    The MIT License (MIT)

    Copyright (c) 2013 Joshua Holbrook

    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in
    all copies or substantial portions of the Software.

    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
    OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
    THE SOFTWARE.
