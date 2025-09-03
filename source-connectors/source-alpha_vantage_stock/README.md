# Alpha Vantage Source Connector

This directory contains the manifest-only connector for **source-alpha_vantage_stock**.  
This connector allows you to pull stock market and financial data from [Alpha Vantage](https://www.alphavantage.co/) into Airbyte for analytics and integration with your data pipelines.  

This is a **manifest-only connector**, which means it is not a Python package on its own—it runs inside the base `source-declarative-manifest` image provided by Airbyte.

For more information on how to configure and use this connector within Airbyte, please refer to the connector's full documentation.

---

## Local Development

We recommend using the **Connector Builder** to edit this connector.  

- Using either **Airbyte Cloud** or your local **Airbyte OSS** instance, navigate to the **Builder** tab.  
- Select **Import a YAML** and choose the connector’s `manifest.yaml` file.  
- The connector will be loaded into the Builder and you’ll be ready to make changes!

If you prefer to develop locally, follow the instructions below.

---

## Building the Docker Image

You can build any manifest-only connector with **airbyte-ci**:

1. Install [airbyte-ci](https://docs.airbyte.com/).
2. Run the following command to build the Docker image:

```bash
airbyte-ci connectors --name=source-alpha_vantage_stock build
```

After the build, an image will be available on your host with the tag:

```
airbyte/source-alpha_vantage_stock:dev
```

---

## Creating Credentials

To use the Alpha Vantage connector, you’ll need an **API key** from [Alpha Vantage](https://www.alphavantage.co/support/#api-key).  

1. Generate an API key by signing up at Alpha Vantage.  
2. Create a file `secrets/config.json` that conforms to the connector’s `spec` defined in `manifest.yaml`.  

Example:

```json
{
  "api_key": "YOUR_ALPHA_VANTAGE_API_KEY",
  "symbol": "AAPL",
  "function": "TIME_SERIES_DAILY"
}
```

⚠️ Note: Any directory named `secrets` is **gitignored** across the entire Airbyte repo, so you don’t risk committing sensitive data.

---

## Running as a Docker Container

Once you’ve built the image and configured credentials, you can run the standard source connector commands:

```bash
# View connector specification
docker run --rm airbyte/source-alpha_vantage_stock:dev spec

# Validate config file
docker run --rm -v $(pwd)/secrets:/secrets airbyte/source-alpha_vantage_stock:dev check --config /secrets/config.json

# Discover available streams
docker run --rm -v $(pwd)/secrets:/secrets airbyte/source-alpha_vantage_stock:dev discover --config /secrets/config.json

# Read data using a configured catalog
docker run --rm -v $(pwd)/secrets:/secrets -v $(pwd)/integration_tests:/integration_tests   airbyte/source-alpha_vantage_stock:dev read --config /secrets/config.json --catalog /integration_tests/configured_catalog.json
```

---

## Running the CI Test Suite

You can run the full test suite locally using:

```bash
airbyte-ci connectors --name=source-alpha_vantage_stock test
```

---

## Publishing a New Version of the Connector

If you would like to contribute changes to **source-alpha_vantage_stock**, follow these steps:

1. Make your changes locally or load the connector’s `manifest.yaml` into Connector Builder and edit there.  
2. Run the tests:

```bash
airbyte-ci connectors --name=source-alpha_vantage_stock test
```

3. Bump the connector version (follow [semantic versioning](https://semver.org/)):  
   - Update the `dockerImageTag` value in `metadata.yaml`.
4. Update connector documentation and changelog:  
   - `docs/integrations/sources/alpha_vantage_stock.md`
5. Create a Pull Request (follow Airbyte PR naming conventions).  
6. Once merged, the connector will be automatically published to **Docker Hub** and the Airbyte connector registry.  

👏 Congratulations—you’ve contributed to the Airbyte ecosystem!

---

## Example Usage in Airbyte UI

When setting up the connector in Airbyte:

- **API Key**: Your Alpha Vantage API key  
- **Symbol**: e.g., `AAPL`  
- **Function**: e.g., `TIME_SERIES_DAILY`  

Airbyte will then fetch stock price data and make it available for sync into your chosen destination.

---
