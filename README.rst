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
`:information_source:` To test the regular expressions in this section: `regex101.com <https://regex101.com/r/nPuWny/1>`_

|

Without named groups: e.g. ``(January|February) (\d{1,2}), (\d{4})``
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
.. code-block:: bash

   (January|February|March|April|May|June|July|August|September|October|November|December) (\d{1,2}), (\d{4})

Dates that should be matched:

.. code-block:: bash

   January 19, 1999
   January 09, 1999

Date that should not be matched:

.. code-block:: bash

   January 123, 1999
   January 19 1999
   January 19, 123

|

With named groups: e.g. ``(?P<day>\d+)``
""""""""""""""""""""""""""""""""""""""""
.. code-block:: bash

   (?P<month>January|February|March|April|May|June|July|August|September|October|November|December) (?P<day>\d{1,2}), (?P<year>\d{4})

|

With and without capitalized month: e.g. ``[J|j]anuary``
""""""""""""""""""""""""""""""""""""""""""""""""""""""""
.. code-block:: bash

   ([J|j]anuary|[F|f]ebruary|[M|m]arch|[A|a]pril|[M|m]ay|[J|j]une|[J|j]uly|[A|a]ugust]|[S|s]eptember|[O|o]ctober|[N|n]ovember|[D|d]ecember) (\d{1,2}), (\d{4})
   
Date that should be matched:

.. code-block:: bash

   january 19, 1999
   January 19, 1999

Date that should not be matched:

.. code-block:: bash

   JANUARY 19, 1999

|

With at least one space: ``\s+``
""""""""""""""""""""""""""""""""
.. code-block:: bash

   (January|February|March|April|May|June|July|August|September|October|November|December)\s+(\d{1,2}),\s+(\d{4})

Date that should be matched:

.. code-block:: bash

   January 19, 1999
   January 19,    1999
   January     19, 1999
   January     19,    1999

Date that should not be matched: 

.. code-block:: bash

   January 19,1999
   January19,1999
   January19, 1999 

|

With zero and more space: ``\s*``
"""""""""""""""""""""""""""""""""
.. code-block:: bash

   (January|February|March|April|May|June|July|August|September|October|November|December)\s*(\d{1,2}),\s*(\d{4})
   
Date that should be matched:

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
   
`:information_source:` 

 - For the last date, it is ``January 1, 1234`` that will be matched, the last digit (5) won't be matched.
 - In order to completely exclude ``January 1, 12345``, you must add ``(?!.+)`` (negative lookahead) 
   at the end of the regex, like this::
 
   (January|February|March|April|May|June|July|August|September|October|November|December) ((?!0)[0-3]{0,1}\d), (\d{4})(?!.+)

|

Dates that should not be matched:

.. code-block:: bash
   
   January 00, 1234
   January 01, 1234
   January 012, 1234
   January 123, 1234

Format: Day Month Year (e.g. 19 January 1999)
---------------------------------------------
`:information_source:` To test the regular expressions in this section: `regex101.com <https://regex101.com/r/eqpIOP/1>`_

|

Without named groups: ``(\d{1,2}) (January|February) (\d{4})``
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
.. code-block:: bash

   (\d{1,2}) (January|February|March|April|May|June|July|August|September|October|November|December) (\d{4})

Date that should be matched:

.. code-block:: bash

   19 January 1999

Date that should not be matched:

.. code-block:: bash

   January 19 1999
   
