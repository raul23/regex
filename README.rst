=================
Regex with Python
=================
Dates to be matched
===================
Format: Month Day, Year (e.g. January 19, 1999)
-----------------------------------------------
`:information_source:` To test the regular expressions in this section: `regex101.com <https://regex101.com/r/nPuWny/1>`_

|

Without named groups:

.. code-block:: python

   regex = r"(January|February|March|April|May|June|July|August|September|October|November|December) (\d{1,2}), (\d{4})"

Dates that should be matched: ``January 19, 1999`` and ``January 09, 1999`

Date that should not be matched: ``January 123, 1999``, ``January 19 1999`` and ``January 19 123``

|

With and without capitalized month:

.. code-block:: python

   regex = r"(([J|j]anuary|[F|f]ebruary|[M|m]arch|[A|a]pril|[M|m]ay|[J|j]une|[J|j]uly|[A|a]ugust]|[S|s]eptember|[O|o]ctober|[N|n]ovember|[D|d]ecember) (\d{1,2}), (\d{4})"
   
Date that should be matched: ``january 19, 1999``

Date that should not be matched: ``JANUARY 19, 1999``

|

With named groups: ``(?P<day>\d+)``

.. code-block:: python

   regex = r"(?P<month>January|February|March|April|May|June|July|August|September|October|November|December) (?P<day>\d{1,2}), (?P<year>\d{4})"

|

With at least one space: ``\s+``

.. code-block:: python

   regex = r"(January|February|March|April|May|June|July|August|September|October|November|December)\s+(\d{1,2}),\s+(\d{4})"

Date that should be matched: ``January 19, 1999``

Date that should not be matched: ``January 19,1999``

|

With zero and more space: ``\s*``

.. code-block:: python

   regex = r"(January|February|March|April|May|June|July|August|September|October|November|December)\s*(\d{1,2}),\s*(\d{4})"
   
Date that should be matched: ``January    19, 1999``

Date that should not be matched: ``january 19,  1999``

|

With at least Year 1:

.. code-block:: python

   regex = r"(January|February|March|April|May|June|July|August|September|October|November|December) (\d{1,2}), (\d+)"
   
Dates that should be matched: ``January 19, 123`` and ``January 19, 123456789``

Format: Day Month Year (e.g. 19 January 1999)
---------------------------------------------
`:information_source:` To test the regular expressions in this section: `regex101.com <https://regex101.com/r/eqpIOP/1>`_

|

Without named groups:

.. code-block:: python

   regex = r"(\d{1,2}) (January|February|March|April|May|June|July|August|September|October|November|December) (\d{4})"

Date that should be matched: ``January    19, 1999``

Date that should not be matched: ``january 19,  1999``

|
   
