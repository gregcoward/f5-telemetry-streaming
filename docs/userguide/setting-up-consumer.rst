.. _settingupconsumer-ref:

Consumers
=========

Use this section to find example declarations and notes for supported consumers. Note: each example below shows only the Consumer class of the declaration and needs to be included with the rest of the base declaration.


Splunk
~~~~~~
|splunk_img|

Required information:
 - Host: The address of the Splunk instance that runs the HTTP event collector (HEC).
 - Protocol: Check if TLS is enabled within the HEC settings :guilabel:`Settings > Data Inputs > HTTP Event Collector`.
 - Port: Default is 8088, this can be configured within the Global Settings section of the Splunk HEC.
 - API Key: An API key must be created and provided in the passphrase object of the declaration, refer to Splunk documentation for the correct way to create an HEC token.

.. NOTE:: There is an additional property that applies to all consumers but is only useful for Splunk. The ``format`` property can be set to ``legacy`` for users who wish to convert the stats output similar to the |splunk app|. To see more information, see |Analytics|. To see more information about using the HEC, see |HEC|.

Example Declaration:

.. code-block:: json
   :linenos:

    {
        "My_Consumer": {
            "class": "Telemetry_Consumer",
            "type": "Splunk",
            "host": "192.0.2.1",
            "protocol": "https",
            "port": "8088",
            "passphrase": {
                "cipherText": "apikey"
            }
        }
    }


Microsoft Azure Log Analytics
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
|azure_img|

Required Information:
 - Workspace ID: Navigate to :guilabel:`Log Analytics workspace > Advanced Settings > Connected Sources`.
 - Shared Key: Navigate to :guilabel:`Log Analytics workspace > Advanced Settings > Connected Sources` and use the primary key.

.. NOTE:: To see more information about sending data to Log Analytics, see |HTTP Data Collector API|.

Example Declaration:

.. code-block:: json
   :linenos:

    {
        "My_Consumer": {
            "class": "Telemetry_Consumer",
            "type": "Azure_Log_Analytics",
            "workspaceId": "workspaceid",
            "passphrase": {
                "cipherText": "sharedkey"
            }
        }
    }


Example Dashboard:

|azure_log_analytics_dashboard|

AWS Cloud Watch
~~~~~~~~~~~~~~~
|aws_img|   

Required information:
 - Region: AWS region of the cloud watch resource.
 - Log Group: Navigate to :guilabel:`Cloud Watch > Logs`
 - Log Stream: Navigate to :guilabel:`Cloud Watch > Logs > Your_Log_Group_Name`
 - Access Key: Navigate to :guilabel:`IAM > Users`
 - Secret Key: Navigate to :guilabel:`IAM > Users`

.. NOTE:: To see more information about creating and using IAM roles, see |IAM roles|.

Example Declaration:

.. code-block:: json
   :linenos:

    {
        "My_Consumer": {
            "class": "Telemetry_Consumer",
            "type": "AWS_CloudWatch",
            "region": "us-west-1",
            "logGroup": "f5telemetry",
            "logStream": "default",
            "username": "accesskey",
            "passphrase": {
                "cipherText": "secretkey"
            }
        }
    }

AWS S3
~~~~~~
|aws_s3|

Required Information:
 - Region: AWS region of the S3 bucket.
 - Bucket: Navigate to S3 to find the name of the bucket.
 - Access Key: Navigate to :guilabel:`IAM > Users`
 - Secret Key: Navigate to :guilabel:`IAM > Users`

.. NOTE:: To see more information about creating and using IAM roles, see |IAM roles|.

Example Declaration:

.. code-block:: json
   :linenos:

    {
        "My_Consumer": {
            "class": "Telemetry_Consumer",
            "type": "AWS_S3",
            "region": "us-west-1",
            "bucket": "bucketname",
            "username": "accesskey",
            "passphrase": {
                "cipherText": "secretkey"
            }
        }
    }


Graphite
~~~~~~~~
|graphite|

Required Information:
 - Host: The address of the Graphite system.
 - Protocol: Check Graphite documentation for configuration.
 - Port: Check Graphite documentation for configuration.

.. NOTE:: To see more information about installing Graphite, see |Installing Graphite|. To see more information about Graphite events, see |Graphite Events|.

.. code-block:: json
   :linenos:

    {
        "My_Consumer": {
            "class": "Telemetry_Consumer",
            "type": "Graphite",
            "host": "192.0.2.1",
            "protocol": "https",
            "port": "443"
        }
    }


Kafka
~~~~~
|Kafka|

Required Information:
 - Host: The address of the Kafka system.
 - Port: The port of the Kafka system.
 - Topic: The topic where data should go within the Kafka system

.. NOTE:: To see more information about installing Kafka, see |Installing Kafka|.

.. code-block:: json
   :linenos:

    {
        "My_Consumer": {
            "class": "Telemetry_Consumer",
            "type": "Kafka",
            "host": "192.0.2.1",
            "port": "9092"
            "topic": "f5-telemetry",
            
        }
    }


ElasticSearch
~~~~~~~~~~~~~
|ElasticSearch|

Required Information:
 - Host: The address of the Kafka system.
 - Index: The index where data should go within the ElasticSearch system.

Optional Parameters:
 - Port: The port of the ElasticSearch system. Default is 9200.
 - Protocol: The protocol of the ElasticSearch system. Options: http or https. Default is http.
 - Allow Self Signed Cert: allow TS to skip Cert validation. Options: true or false. Default is false.
 - Path: The path to use when sending data to the ElasticSearch system.
 - Data Type: The type of data posted to the ElasticSearch system. Default is f5.telemetry
 - API Version: The API version of the ElasticSearch system.
 - Username: The username to use when sending data to the ElasticSearch system.
 - Passphrase: The secret/password to use when sending data to the ElasticSearch system.

.. NOTE:: To see more information about installing ElasticSearch, see |Installing ElasticSearch|.

.. code-block:: json
   :linenos:

    {
        "My_Consumer": {
            "class": "Telemetry_Consumer",
            "type": "ElasticSearch",
            "host": "192.0.2.1",
            "port": "9200",
            "protocol": "https",
            "allowSelfSignedCert": false,
            "path": "/path/to/post/data",
            "index": "f5telemetry",
            "dataType": "f5telemetry",
            "apiVersion": "6.5",
            "username": "username",
            "passphrase": {
                "cipherText": "secretkey"
            }
        }

    }


Sumo Logic
~~~~~~~~~~
|Sumo Logic|

Required Information:
 - Host: The address of the Sumo Logic collector.
 - Protocol: The protocol of the Sumo Logic collector.
 - Port: The port of the Sumo Logic collector.
 - Path: The HTTP path of the Sumo Logic collector (without the secret).
 - Secret: The protected portion of the HTTP path (the final portion of the path, sometimes called a system tenant).

.. NOTE:: To see more information about installing Sumo Logic, see |Installing Sumo Logic|.

.. code-block:: json
   :linenos:

    {
        "My_Consumer": {
            "class": "Telemetry_Consumer",
            "type": "Sumo_Logic",
            "host": "192.0.2.1",
            "protocol": "https",
            "port": "443",
            "path": "/receiver/v1/http/",
            "passphrase": {
                "cipherText": "secret"
            }
        }
    }


.. |splunk_img| image:: /images/splunk_logo.png
   :target: https://www.splunk.com
   :alt: Splunk

.. |azure_img| image:: /images/azure_logo.png
   :target: https://docs.microsoft.com/en-us/azure/azure-monitor/log-query/log-query-overview
   :alt: Microsoft Azure

.. |azure_log_analytics_dashboard| image:: /images/azure_log_analytics_dashboard.png

.. |aws_img| image:: /images/aws_logo.png
   :target: https://aws.amazon.com/cloudwatch/
   :alt: Amazon Web Services

.. |aws_s3| image:: /images/aws_s3.png
   :target: https://aws.amazon.com/s3/
   :alt: Amazon Web Services

.. |graphite| image:: /images/graphite.png
   :target: https://graphiteapp.org/
   :alt: Graphite

.. |grafana_img| image:: /images/grafana-logo.png
   :target: grafana_index.html
   :alt: Grafana

.. |Kafka| image:: /images/kafka-logo-wide.png
   :target: https://kafka.apache.org/
   :alt: Kafka

.. |ElasticSearch| image:: /images/ElasticSearch_img.png
   :target: https://www.elastic.co/
   :alt: Kafka

.. |Sumo Logic| image:: /images/Sumo_img.png
   :target: https://www.sumologic.com/
   :alt: Splunk



.. toctree::
   :caption: Choose a provider
   :hidden:
   :glob:
   :maxdepth: 1

   
.. |Azure documentation| raw:: html

   <a href="https://docs.microsoft.com/en-us/azure/azure-monitor/platform/data-collector-api" target="_blank">Azure documentation</a>

.. |IAM roles| raw:: html

   <a href="https://aws.amazon.com/iam/" target="_blank">AWS Identity and Access Management (IAM) documentation</a>

.. |HEC| raw:: html

   <a href="http://docs.splunk.com/Documentation/Splunk/latest/Data/UsetheHTTPEventCollector" target="_blank">Splunk HTTP Event Collector documentation</a>

.. |Analytics| raw:: html

   <a href="https://www.f5.com/pdf/deployment-guides/f5-analytics-dg.pdf" target="blank">F5 Analytics iApp Template documentation</a>

.. |splunk app| raw:: html

   <a href="https://splunkbase.splunk.com/app/3161/" target="blank">F5 Analytics App for Splunk</a>

.. |HTTP Data Collector API| raw:: html

   <a href="https://docs.microsoft.com/en-us/azure/azure-monitor/platform/data-collector-api" target="_blank">HTTP Data Collector API documentation</a>

.. |Installing Graphite| raw:: html

   <a href="https://graphite.readthedocs.io/en/latest/install.html" target="_blank">Installing Graphite documentation</a>

.. |Graphite Events| raw:: html

   <a href="https://graphite.readthedocs.io/en/latest/events.html" target="_blank">Graphite Events documentation</a>

.. |Installing Kafka| raw:: html

   <a href="https://kafka.apache.org/quickstart" target="_blank">Installing Kafka documentation</a>

.. |Installing ElasticSearch| raw:: html

   <a href="https://www.elastic.co/guide/index.html" target="_blank">Installing ElasticSearch documentation</a>

.. |Installing Sumo Logic| raw:: html

   <a href="https://help.sumologic.com/01Start-Here/Quick-Start-Tutorials" target="_blank">Installing Sumo Logic documentation</a>
