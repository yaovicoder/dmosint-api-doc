API Documentation
=================

This documentation provides information about the available endpoints
and their usage in the API.

Table of Contents
-----------------

-  `Raw Files Action <#raw-files-action>`__
-  `File Sample Action <#file-sample-action>`__
-  `Get All Files Action <#get-all-files-action>`__
-  `Get File Action <#get-file-action>`__
-  `Get All Columns Action <#get-all-columns-action>`__

--------------

Raw Files Action
----------------

Return list of files to be imported.

Endpoint
~~~~~~~~

``GET /api/v1/raw-files``

Parameters
~~~~~~~~~~

None

Response
~~~~~~~~

-  HTTP Status Code: 200 OK
-  Content-Type: application/json

Example Response
^^^^^^^^^^^^^^^^

.. code:: json

   [
     "file1.txt",
     "file2.csv",
     "file3.json"
   ]

File Sample Action
------------------

Retrieve a sample of a file.

.. _endpoint-1:

Endpoint
~~~~~~~~

``GET /api/v1/file-sample/:filename?lines_count=:lines_count``

.. _parameters-1:

Parameters
~~~~~~~~~~

+-------------+------+-------------------------------------------------+
| Name        | Type | Description                                     |
+=============+======+=================================================+
| `           | st   | The name of the file to retrieve the sample     |
| `filename`` | ring | from.                                           |
+-------------+------+-------------------------------------------------+
| ``li        | nu   | The number of lines to include in the sample.   |
| nes_count`` | mber | (Default: 1000)                                 |
+-------------+------+-------------------------------------------------+

.. _response-1:

Response
~~~~~~~~

-  HTTP Status Code: 200 OK
-  Content-Type: application/json

.. _example-response-1:

Example Response
^^^^^^^^^^^^^^^^

.. code:: json

   "This is a sample of the file content."

Get All Files Action
--------------------

Retrieve all files sorted by name.

.. _endpoint-2:

Endpoint
~~~~~~~~

``GET /api/v1/get-files-all``

.. _parameters-2:

Parameters
~~~~~~~~~~

None

.. _response-2:

Response
~~~~~~~~

-  HTTP Status Code: 200 OK
-  Content-Type: application/json

.. _example-response-2:

Example Response
^^^^^^^^^^^^^^^^

.. code:: json

   [
     {
       "file_id": "1",
       "file_name": "file1.txt",
       "extension": "txt",
       "numberOfRows": 100,
       "file_size": 1024,
       "clean": true,
       "joined": false,
       "created_on": "2023-07-05T10:00:00Z",
       "parent_id": null,
       "file_index": 0
     },
     {
       "file_id": "2",
       "file_name": "file2.csv",
       "extension": "csv",
       "numberOfRows": 500,
       "file_size": 2048,
       "clean": false,
       "joined": true,
       "created_on": "2023-07-05T11:00:00Z",
       "parent_id": "1",
       "file_index": 1
     }
   ]

Get File Action
---------------

Retrieve a file by its ID.

.. _endpoint-3:

Endpoint
~~~~~~~~

``GET /api/v1/get-file/:file_id``

.. _parameters-3:

Parameters
~~~~~~~~~~

=========== ====== ===============================
Name        Type   Description
=========== ====== ===============================
``file_id`` string The ID of the file to retrieve.
=========== ====== ===============================

.. _response-3:

Response
~~~~~~~~

-  HTTP Status Code: 200 OK
-  Content-Type: application/json

.. _example-response-3:

Example Response
^^^^^^^^^^^^^^^^

.. code:: json

   {
     "file_id": "1",
     "file_name": "file1.txt",
     "extension": "txt",
     "numberOfRows": 100,
     "file_size": 1024,
     "clean": true,
     "joined": false,
     "created_on": "2023-07-05T10:00:00Z",
     "parent_id": null,
     "file_index": 0
   }

Get All Columns Action
----------------------

Retrieve all columns sorted by name.

.. _endpoint-4:

Endpoint
~~~~~~~~

``GET /api/v1/get-columns-all``

.. _parameters-4:

Parameters
~~~~~~~~~~

None

.. _response-4:

Response
~~~~~~~~

-  HTTP Status Code: 200 OK
-  Content-Type: application/json

.. _example-response-4:

Example Response
^^^^^^^^^^^^^^^^

.. code:: json

   [
     {
       "column_id": "1",
       "column_name": "column1",
       "partition": "partition_key",
       "ordering": 1,
       "aggregate_on": true,
       "display": true
     },
     {
       "column_id": "2",
       "column_name": "column2",
       "partition": null,
       "ordering": null,
       "aggregate_on": false,
       "display": true
     }
   ]
