# Use Airbyte's base image for low-code connectors
FROM airbyte/source-declarative-manifest

# Add your manifest and metadata files into the image
COPY manifest.yaml /airbyte/integration_code/manifest.yaml
COPY metadata.yaml /airbyte/integration_code/metadata.yaml