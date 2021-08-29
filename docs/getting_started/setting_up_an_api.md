# Setting up an OPTIMADE API

These notes describe how to set up and customize an OPTIMADE API based on the reference server in this package for some existing crystal structure data.
To follow this guide, you will need to have a working development installation, as described in the [installation instructions](../INSTALL.md#full-development-installation).

Complete examples of APIs that use this package are described in the [Use Cases](./use_cases.md) section.

## Setting up the database

The `optimade` reference server requires a data source (instances of [`EntryCollection`][optimade.server.entry_collections.entry_collections.EntryCollection] subclasses) per OPTIMADE entry type (`structures`, `references`, `links`), though these can be configured to use any database, or even a static file, under the hood.

In the reference server, these data sources, or collections, are created in the submodule for the corresponding routers/endpoints.
To use MongoDB-based collections for each entry type, simply specify the appropriate options in your [configuration](../configuration.md), namely `"database_backend": "mongodb"`, `"mongo_uri": "mongodb://localhost:27017"`, `"mongo_database": "optimade"` and the collection names for each entry type (`"structures_collection": "structures"` etc.).

These notes will now assume that you have a MongoDB instance running and you have created a database that matches your `"mongo_database"` config option.

If you disable inserting test data (with the `"insert_test_data": false` configuration option), you can test your API/database connection by running the web server with `uvicorn optimade.main:app` and visiting the (hopefully empty) structures endpoint at `localhost:5000/v1/structures` (or your chosen host).

## Mapping non-OPTIMADE data

Two options:
- Run your data through a Mapper first, then create a new database
- Define aliases for custom fields and potentially map filters by field

### Creating a secondary database

### Aliases and transforming filters

## Serving non-OPTIMADE fields

Again, two options:
- List provider fields in config, which will get your provider prefix appended to them
- Extend e.g. `StructureResourceAttributes` model and manually prefix it. Allows you to add custom info

### Config-only

### Extending the OPTIMADE models

## Validating your implementation

## Registering as a provider
