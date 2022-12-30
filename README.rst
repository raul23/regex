====================
List of useful regex
====================
.. contents:: **Contents**
   :depth: 4
   :local:
   :backlinks: top

Dates to be matched
===================
Format: Month Day, Year (e.g. January 19, 1999)
-----------------------------------------------
`:information_source:` To test the regular expressions in this section: `regex101.com <https://regex101.com/r/nPuWny/2>`_

|

Without named groups: e.g. ``(January|February) (\d{1,2}), (\d{4})``
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
.. code-block:: bash

   (January|February|March|April|May|June|July|August|September|October|November|December) (\d{1,2}), (\d{4})

Dates that should be matched:

.. code-block:: bash

   January 19, 1999
   January 09, 1999

Dates that should not be matched:

.. code-block:: bash

   January 123, 1999
   January 19 1999
   January 19, 123

|

With named groups: e.g. ``(?P<day>\d{1,2})``
""""""""""""""""""""""""""""""""""""""""""""
.. code-block:: bash

   (?P<month>January|February|March|April|May|June|July|August|September|October|November|December) (?P<day>\d{1,2}), (?P<year>\d{4})

|

With and without capitalized month: e.g. ``[J|j]anuary``
""""""""""""""""""""""""""""""""""""""""""""""""""""""""
.. code-block:: bash

   ([J|j]anuary|[F|f]ebruary|[M|m]arch|[A|a]pril|[M|m]ay|[J|j]une|[J|j]uly|[A|a]ugust]|[S|s]eptember|[O|o]ctober|[N|n]ovember|[D|d]ecember) (\d{1,2}), (\d{4})
   
Dates that should be matched:

.. code-block:: bash

   january 19, 1999
   January 19, 1999

Dates that should not be matched:

.. code-block:: bash

   JANUARY 19, 1999
   MarcH 19, 1999

|

With at least one space: ``\s+``
""""""""""""""""""""""""""""""""
.. code-block:: bash

   (January|February|March|April|May|June|July|August|September|October|November|December)\s+(\d{1,2}),\s+(\d{4})

Dates that should be matched:

.. code-block:: bash

   January 19, 1999
   January 19,    1999
   January     19, 1999
   January     19,    1999

Dates that should not be matched: 

.. code-block:: bash

   January 19,1999
   January19,1999
   January19, 1999 

|

With zero and more space: ``\s*``
"""""""""""""""""""""""""""""""""
.. code-block:: bash

   (January|February|March|April|May|June|July|August|September|October|November|December)\s*(\d{1,2}),\s*(\d{4})
   
Dates that should be matched:

.. code-block:: bash

   January    19, 1999
   January 19,       1999
   January 19,1999
   January19,1999
   January19, 1999
   
|

With at least Year 1: ``(?!0)`` and ``\d+`` (negative lookahead)
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
.. code-block:: bash

   (January|February|March|April|May|June|July|August|September|October|November|December) (\d{1,2}), (?!0)(\d+)

Dates that should be matched:

.. code-block:: bash

   January 19, 1
   January 19, 10
   January 19, 123
   January 19, 123456789

Dates that should not be matched:

.. code-block:: bash

   January 19, 0
   January 19, 01
   January 19, 00

|

Restrict day to not begin with zero: ``(?!0)`` (negative lookahead)
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
.. code-block:: bash

   (January|February|March|April|May|June|July|August|September|October|November|December) ((?!0)[0-3]{0,1}\d), (\d{4})

Dates that should be matched:

.. code-block:: bash

   January 1, 1234
   January 10, 1234
   January 1, 12345
   
`:information_source:` About the last date (``January 1, 12345``) in the previous example:

- For the last date, it is ``January 1, 1234`` that will be matched, i.e. the last digit (5) won't be matched.
- In order to completely exclude ``January 1, 12345``, you must add ``(?!.+)`` (negative lookahead) 
  at the end of the regex, like this:
 
  .. code-block:: bash

     (January|February|March|April|May|June|July|August|September|October|November|December) ((?!0)[0-3]{0,1}\d), (\d{4})(?!.+)

|

Dates that should not be matched:

.. code-block:: bash
   
   January 00, 1234
   January 01, 1234
   January 012, 1234
   January 123, 1234

|

Format: Day Month Year (e.g. 19 January 1999)
---------------------------------------------
`:information_source:` To test the regular expressions in this section: `regex101.com <https://regex101.com/r/eqpIOP/2>`_

|

Without named groups: ``(\d{1,2}) (January|February) (\d{4})``
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
.. code-block:: bash

   (\d{1,2}) (January|February|March|April|May|June|July|August|September|October|November|December) (\d{4})

Dates that should be matched:

.. code-block:: bash

   19 January 1999
   0 January 1999
   09 January 1999
   00 January 1999
   19 January 12345

`:information_source:` To completely exclude ``19 January 12345``, you must add ``(?!.+)`` (negative lookahead) 
at the end of the regex, like this:
 
.. code-block:: bash

   (\d{1,2}) (January|February|March|April|May|June|July|August|September|October|November|December) (\d{4})(?!.+)

|

Dates that should not be matched:

.. code-block:: bash

   123 January, 1999
   19 january 1234

|

`:star:` You can add some of the tokens from the `previous section <#format-month-day-year-e-g-january-19-1999>`_ to 
make the regex more restrictive or flexible, such as ``^(?!0)`` for the day part (it must not begin with 0):

.. code-block:: bash

   ^(?!0)(\d{1,2}) (January|February|March|April|May|June|July|August|September|October|November|December) (\d{4})

Dates that should be matched:

.. code-block:: bash

   19 January 1999
   19 January 12345

Dates that should not be matched:

.. code-block:: bash

   0 January 1999
   09 January 1999
   00 January 1999
   123 January, 1999
   19 january 1234
 
|

Format: YYYY-MM-DD with regex only (e.g. 1940-01-19)
----------------------------------------------------
`:information_source:` To test the regular expressions in this section: `regex101.com <https://regex101.com/r/eqpIOP/2>`_

|

Without named groups: ``^(?!0)\d{4}-(?!00)\d{1,2}-(?!00)\d{1,2}(?!.+)``
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
.. code-block:: bash

   ^(?!0)\d{4}-(?!00)\d{1,2}-(?!00)\d{1,2}(?!.+)
   
Dates that should be matched:

.. code-block:: bash

   1940-11-19
   1500-01-19
   1980-01-01
   1980-1-1
   1980-1-01

Dates that should not be matched:

.. code-block:: bash

   1980-00-00
   1980-01-00
   2019-123-20
   1940-12-123
   0-01-19
   0000-12-25
   12-12-12
   
|

`:information_source:` Explaining the different parts of ``^(?!0)\d{4}-(?!00)\d{1,2}-(?!00)\d{1,2}(?!.+)``

- ``^(?!0)``: year doesn't start with zero
- ``\d{4}``: year takes exactly 4 digits
- ``(?!00)``: exclude ``00`` as a month and day
- ``\d{1,2}``: month and day take 1 or 2 digits
- ``(?!.+)``: exclude dates with days longer than 2 digits

|

A more complex regex that restricts month and day to a smaller range of values:

.. code-block:: bash

   ^(?!0)\d{4}-((?!00)(?!13|14|15|16|17|18|19)((?![2-9])\d{0,1})(\d))-((?!00)(?!32|33|34|35|36|37|38|39)((?![4-9])\d{0,1})(\d))(?!.+)
   
Dates that should be matched:

.. code-block:: bash

   1940-11-19
   1500-01-19
   1980-01-01
   1980-1-1
   1980-1-01

Dates that should not be matched:

.. code-block:: bash

   1980-13-30
   1980-12-32
   1980-00-00
   1980-01-00
   2019-123-20
   1940-12-123
   0-01-19
   0000-12-25
   12-12-12

|

`:information_source:` 

- ``(?!13|14|15|16|17|18|19)``: since we accept the first digit of a two-digits month to be 0 or 1, we further restrict it to not be
  in the range [13-19] (inclusive)
- ``(?![2-9])\d{0,1}``: the first digit of a two-digits month must not start with a value greater than 1
- ``(?!32|33|34|35|36|37|38|39)``: since we accept the first digit of a two-digits day to be in the range [0-3] (inclusive), 
  we further restrict. it to not be in the range [32-39] (inclusive)
- ``(?![4-9])\d{0,1}``: the first digit of a two-digits month must not start with a value greater than 3
- ``(?!.+)``: exclude dates with days longer than 2 digits
