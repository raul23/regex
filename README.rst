=================
Regex with Python
=================
Dates to be matched
===================
Format: January 19, 1999
------------------------
`:information_source:` To test the regular expressions in this section: `regex101.com <https://regex101.com/r/4Lm6oE/1>`_

|

Without named groups:

.. code-block:: python

   regex = r"(January|February|March|April|May|June|July|August|September|October|November|December) (\d+), (\d+)"

With named groups: ``(?P<day>\d+)``

.. code-block:: python

   regex = r"(?P<month>January|February|March|April|May|June|July|August|September|October|November|December) (?P<day>\d+), (?P<year>\d+)"
   
With at least one space: ``\s+``

.. code-block:: python

   regex = r"(January|February|March|April|May|June|July|August|September|October|November|December)\s+(\d+),\s+(\d+)"
   
With zero and more space: ``\s*``

.. code-block:: python

   regex = r"(January|February|March|April|May|June|July|August|September|October|November|December)\s*(\d+),\s*(\d+)"
   
