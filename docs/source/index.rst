API Documentation
=================

This documentation provides information about the available endpoints
and their usage in the API.

Table of Contents
-----------------

-  `Get raw files list <#get-raw-files-list>`__
-  `Get file sample <#get-file-sample>`__
-  `Get all files <#get-all-files>`__
-  `Get a single file <#get-a-single-file>`__
-  `Get all columns <#get-all-columns>`__
-  `Process and preview file data <#process-and-preview-file-data>`__


--------------

1. Get raw files list
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

2. Get file sample
------------------

Retrieve a sample of a file.

.. _endpoint-1:

Endpoint
~~~~~~~~

``GET /api/v1/file-sample/:filename?lines_count=:lines_count``

.. _parameters-1:

Parameters
~~~~~~~~~~

+-----------------+----------+---------------------------------------------------+
| Name            | Type     | Description                                       |
+=================+==========+===================================================+
| ``filename``    | string   | The name of the file to retrieve the sample from  |
+-----------------+----------+---------------------------------------------------+
| ``lines_count`` | number   | The number of lines to include in the sample.     |
|                 |          | (Default: 1000)                                   |
+-----------------+----------+---------------------------------------------------+

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

3. Get all files 
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

4. Get a file
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

5. Get all columns
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

6. Process and preview file data
-----------------------------

This API endpoint processes the data from a file, performs necessary
transformations, and returns a preview of the processed data.

.. _endpoint-5:

Endpoint
~~~~~~~~

``POST /api/v1/preview-file``

Request Body
~~~~~~~~~~~~

The request body should be a JSON object with the following parameters:

+-----------------------+-----------+-----------------------------------------------------+
| Parameter             | Type      | Description                                         |
+=======================+===========+=====================================================+
| ``filename``          | string    | The name of the file to process.                    |
+-----------------------+-----------+-----------------------------------------------------+
| ``column_separator``  | string    | The separator used to separate columns in the file. |
+-----------------------+-----------+-----------------------------------------------------+
| ``selected_columns``  | object    | A map of selected columns to process, where the     |
|                       |           | keys represent the original column names and the    |
|                       |           | values represent the desired column names.          |
+-----------------------+-----------+-----------------------------------------------------+
| ``has_header``        | boolean   | Indicates whether the file has a header row. Set to |
|                       |           | ``true`` if the file includes a header row, or      |
|                       |           | ``false`` if not.                                   |
+-----------------------+-----------+-----------------------------------------------------+
| ``file_quotes``       | string    | Optional. The type of quotes used in the file. Set  |
|                       |           | to “simple” for single quotes (’) or “double” for   |
|                       |           | double quotes (“). If not provided, quotes will be  |
|                       |           | empty.                                              |
+-----------------------+-----------+-----------------------------------------------------+

.. _example-usage-5:

Example Usage
^^^^^^^^^^^^^

To process and preview file data, you can use the following example cURL command:

.. code:: bash

   curl -X POST \
     -H "Content-Type: application/json" \
     -d '{
       "filename": "disqus_clean.txt",
       "column_separator": ",",
       "selected_columns": {},
       "has_header": true,
       "file_quotes": "double"
     }' \
     http://ip_address:9000/api/v1/preview-file

.. _response-5:

Response
~~~~~~~~

The response will be a JSON array containing the following elements:

-  ``checkboxes_html``: HTML representation of checkboxes for selected
   columns.
-  ``preview_data_html``: HTML representation of the preview data.
-  ``columns_map_table_html``: HTML representation of the table mapping
   original column names to desired column names.

.. _example-response-5:

Example Response
^^^^^^^^^^^^^^^^

.. code:: json

   HTTP/1.1 200 OK
   Content-Type: application/json

   [
     "checkboxes_html",
     "preview_data_html",
     "columns_map_table_html"
   ]
