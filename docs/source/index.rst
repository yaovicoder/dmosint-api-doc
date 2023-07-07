API Documentation
=================

Welcome to our API!

Our API is designed to provide comprehensive functionality for various processes, cases, and operations. It caters to two distinct areas: handling database records and managing operations on S3 file systems.

The API is divided into two major sections, each focusing on a specific domain:

1. **Database Record Operations Section**: This section enables seamless interaction with the database and offers a set of endpoints dedicated to managing database records. 

2. **S3 File System Operations Section**: In this section, you'll find endpoints that facilitate working with MinIO (S3) file systems, including S3, HDFS, and the local file system. 

By dividing our API into these two sections, we aim to provide clear separation and focus on the specific requirements of database records and file system operations. This approach ensures a more organized and intuitive experience when consuming the API, making it easier for developers to navigate and leverage the functionalities according to their needs.

Please refer to the API documentation for detailed information on the available endpoints and how to utilize them effectively. We hope our API enhances your productivity and simplifies the integration of database and file system operations into your applications.


Table of Contents
-----------------
.. contents::
   :depth: 2

--------------

.. _records-section:

1. Database Records Operations
======================================

.. _records-column:

1.1. Column
==========

.. _records-column-add:

1.1.1. Add column
---------------

This API endpoint adds a column to the database if it does not already exist.

.. _records-column-add-endpoint:

Endpoint
~~~~~~~~

``POST /api/v1/add-column``

Request Body
~~~~~~~~~~~~

The request body should be a JSON object with the following parameters:


=============== ====== ===============================
Name            Type   Description
=============== ====== ===============================
``column_name`` string The name of the column to add.
=============== ====== ===============================

.. _records-column-add-example-usage:

Example Usage
^^^^^^^^^^^^^

To add a column, send a POST request to the endpoint with the column name in the request body.

.. code:: bash

   curl -X POST \
     -H "Content-Type: application/json" \
     -d '{
       "column_name": "column_name"
     }' \
     http://ip_address:9000/api/v1/add-column

.. _records-column-add-response:

Response
~~~~~~~~

The response will depend on the result of adding the column.

Example Response
^^^^^^^^^^^^^^^^

- Success - Column Added successfully.
  
Example Response Body

  .. code:: json
     {
       "status": "success",
       "code": 200,
       "message": "Column added successfully",
       "column": {
         "column_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
         "column_name": "column_name",
         "partition": null,
         "ordering": null,
         "aggregate_on": null,
         "display": true
       }
     }

- Success - Column Already Exists
  If the column already exists in the database, the response will be No Content.

- Error
  Example Response Body.

  .. code:: json

     {
       "status": "error",
       "code": 500,
       "message": "Failed to add the column"
     }

.. _records-column-get-all:

1.1.2. Get all columns
----------------------

Retrieve all columns sorted by name.

.. _get-all-columns-endpoint:

Endpoint
~~~~~~~~

``GET /api/v1/get-columns-all``

.. _records-column-get-all-parameters:

Parameters
~~~~~~~~~~

None

.. _records-column-get-all-usage:

Usage
~~~~~

To get the list of all columns sorted by name, you can use the following example cURL command:

.. code:: bash

   curl -X GET http://ip_address:9000/api/v1/get-columns-all

.. _records-column-get-all-response:

Response
~~~~~~~~

-  HTTP Status Code: 200 OK
-  Content-Type: application/json

.. _records-column-get-all-response:

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

.. _records-file:

1.2. File
=======

.. _records-file-get:

1.2.1. Get a file record
----------------------

Retrieve a file by its ID.

.. _records-file-get-endpoint:

Endpoint
~~~~~~~~

``GET /api/v1/get-file/:file_id``

.. _records-file-get-parameters:

Parameters
~~~~~~~~~~

=========== ====== ===============================
Name        Type   Description
=========== ====== ===============================
``file_id`` string The ID of the file to retrieve.
=========== ====== ===============================

.. _records-file-get-response:

Response
~~~~~~~~

-  HTTP Status Code: 200 OK
-  Content-Type: application/json

.. _records-file-get-response:

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


.. _records-file-get-all:

1.2.2. Get all files 
------------------

Retrieve all files sorted by name.

.. _records-file-get-all-endpoint:

Endpoint
~~~~~~~~

``GET /api/v1/get-files-all``

.. _records-file-get-all-parameters:

Parameters
~~~~~~~~~~

None

.. _records-file-get-all-usage:

Usage
~~~~~

To get the list of all imported files sorted by name, you can use the following example cURL command:

.. code:: bash

   curl -X GET http://ip_address:9000/api/v1/get-files-all

.. _records-file-get-all-response:

Response
~~~~~~~~

-  HTTP Status Code: 200 OK
-  Content-Type: application/json

.. _get-all-files-example-response:

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


.. _job:

1.3. Job
=======

[Will be updated soon...]


--------------

.. _storage-section:

2. S3 File System Operations
============================

.. _storage-files:

2.1. File In Storage
====================

.. _storage-file-get-file-sample:

2.1.1. Get file sample
---------------------

Retrieve a sample of a file.

.. _storage-file-get-file-sample-endpoint:

Endpoint
~~~~~~~~

``GET /api/v1/file-sample/filename/lines_count``

.. _storage-file-get-file-sample-parameters:

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

.. _storage-file-get-file-sample-usage:

Usage
~~~~~

To get a sample of a file, you can use the following example cURL command:

.. code:: bash

   curl -X GET http://ip_address:9000/api/v1/get-sample/file1.txt/1000

.. _storage-file-get-file-sample-response:

Response
~~~~~~~~

-  HTTP Status Code: 200 OK
-  Content-Type: application/json

.. _storage-file-get-file-sample-example-response:

Example Response
^^^^^^^^^^^^^^^^

.. code:: json

   "This is a sample of the file content."


.. _storage-file-get-raw-files-list:

2.1.2. Get raw files list
---------------------

Return list of files to be imported.

.. _storage-file-get-raw-files-list-endpoint:

Endpoint
~~~~~~~~

``GET /api/v1/get-raw-files``

.. _parameters-1:

Parameters
~~~~~~~~~~

None

.. _storage-file-get-raw-files-list-usage:

Usage
~~~~~

To get the list of files tobe imported, you can use the following example cURL command:

.. code:: bash

   curl -X GET http://ip_address:9000/api/v1/get-raw-files

.. _storage-file-get-raw-files-list-response:

Response
~~~~~~~~

-  HTTP Status Code: 200 OK
-  Content-Type: application/json

.. _storage-file-get-raw-files-list-example-response:

Example Response
^^^^^^^^^^^^^^^^

.. code:: json

   [
     "file1.txt",
     "file2.csv",
     "file3.json"
   ]

.. _storage-process-and-preview-file-data:

2.1.3. Process and preview file data
--------------------------------

This API endpoint processes the data from a file, performs necessary
transformations, and returns a preview of the processed data.

.. _storage-process-and-preview-file-data-endpoint:

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

.. _storage-process-and-preview-file-data-example-usage:

Example Usage
^^^^^^^^^^^^^

To process and preview file data, you can use the following example cURL command:

.. code:: bash

   curl -X POST \
     -H "Content-Type: application/json" \
     -d '{
       "filename": "file1.txt",
       "column_separator": "",
       "selected_columns": {},
       "has_header": false,
       "file_quotes": "double"
     }' \
     http://ip_address:9000/api/v1/preview-file

.. _storage-process-and-preview-file-data-response:

Response
~~~~~~~~

The response will be a JSON array containing the following elements:

-  ``checkboxes_html``: HTML representation of checkboxes for selected
   columns.
-  ``preview_data_html``: HTML representation of the preview data.
-  ``columns_map_table_html``: HTML representation of the table mapping
   original column names to desired column names.

.. _storage-process-and-preview-file-data-example-response:

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


