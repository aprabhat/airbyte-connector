# Alpha Vantage Stock source connector

This directory contains the manifest-only connector for `source-alpha-vantage-stock`.  
This _manifest-only_ connector runs inside the base `source-declarative-manifest` image.

For information about Alpha Vantage API, see the [official docs](https://www.alphavantage.co/documentation/).

---

## Local development

We recommend using the Connector Builder to edit this connector.  
Using either Airbyte Cloud or your local OSS instance, navigate to the **Builder** tab and select **Import a YAML**.  
Then load the connector’s `manifest.yaml` file.

If you prefer to develop locally, you can follow the instructions below.

---

### Building the docker image

You can build this connector using `airbyte-ci`:

1. Install [`airbyte-ci`](https://github.com/airbytehq/airbyte/blob/master/airbyte-ci/connectors/pipelines/README.md)  
2. Run the following command:

```bash
airbyte-ci connectors --name=source-alpha-vantage-stock build
