# Deploy Appwrite using GitHub Actions
Installs the CLI and uses `appwrite deploy collection` to synchronise the state in `appwrite.json` with the one deployed to your server. This action is an extension of the official [`setup-for-actions`](https://github.com/appwrite/setup-for-actions/tree/main) project.

### Configuration
The following input variables are required:
- endpoint: Where your server is hosted (e.g. `https://[HOSTNAME_OR_IP]/v1`)
- project: Project ID (found in dashboard, 20 characters by default)
- id: API key with at least Database permissions (can be generated in console, e.g. `${{ secrets.APPWRITE_API_KEY }}`)

The following input variable is optional:
- root_dir: Directory where the `appwrite.json` file is located (default: `./appwrite`)

### Prerequisites
You need to have a valid `appwrite.json` file under version control, located in the specified directory. This file cannot have the `projectId` field set, as this is overwritten depending on the configured value. The `projectName` field is ignored. Below is an example `appwrite.json` file:

```json
{
    "projectId": "",
    "projectName": "",
    "databases": [
        {
            "$id": "sampleDB",
            "name": "SampleDatabase",
            "$createdAt": "2023-01-01T12:00:00.000+00:00",
            "$updatedAt": "2023-01-01T12:00:00.000+00:00",
            "enabled": true
        }
    ],
    "collections": [
        {
            "$id": "sampleCollection",
            "$permissions": [],
            "databaseId": "sampleDB",
            "name": "SampleCollection",
            "enabled": true,
            "documentSecurity": false,
            "attributes": [],
            "indexes": []
        }
    ]
}
```

### Extensions
The CLI also exports deployment of buckets, collections and teams. If you want these supported, feel free to submit a PR.
