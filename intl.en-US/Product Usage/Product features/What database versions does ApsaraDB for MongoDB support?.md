# What database versions does ApsaraDB for MongoDB support?

ApsaraDB for MongoDB supports the following database versions:MongoDB 4.2, 4.0, and 3.4. We recommend that you use drivers running the same database version as the ApsaraDB for MongoDB instance to access it. You can download drivers in different languages from the [MongoDB official website](https://docs.mongodb.org/ecosystem/drivers/).

**Note:** For more information about differences between the database versions, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md).

## How do I view the database version of an ApsaraDB for MongoDB instance?

1.  Connect to a replica set instance by using the mongo shell. For more information, see [Connect to a replica set instance by using the mongo shell](/intl.en-US/Quick Start/Connect to an instance/Connect to a replica set instance by using the mongo shell.md).
2.  Run the following command to view the database version:

    ```
    db.version()
    ```


## References

[Upgrade MongoDB versions](/intl.en-US/User Guide/Instance management/Upgrading Database Version/Upgrade MongoDB versions.md)

