```json
{
  "upload": {
    "description": "Uploads data to Irys.",
    "parameters": {
      "data": {
        "type": "string | Buffer | Readable",
        "description": "The data to upload."
      },
      "tags": {
        "type": "Tag[]",
        "description": "(Optional) metatags."
      },
      "anchor": {
        "type": "string",
        "description": "(Optional) Random value used to prevent data item ID collisions, used with deterministic data item IDs only."
      }
    },
    "returns": {
      "type": "object",
      "description": "A receipt as a JSON object with the following values.",
      "fields": {
        "id": "Transaction ID (used to download the data)",
        "timestamp": "Timestamp (UNIX milliseconds) of when the transaction was created and verified",
        "version": "The version of this JSON file, currently 1.0.0",
        "public": "Public key of the bundler node used",
        "signature": "A signed deep hash of the JSON receipt",
        "deadlineHeight": "The block number by which the transaction must be finalized",
        "block": "Deprecated",
        "validatorSignatures": "Deprecated",
        "verify": "An async function used to verify the receipt at any time"
      }
    },
    "funding": {
      "description": "Uploads of less than 100 KiB are free. For larger uploads, you'll need to fund your account first."
    },
    "example": {
      "description": "Use a token-specific version of getIrysUploader() to connect to an Irys Bundler before uploading.",
      "code": "const irys = await getIrysUploader();\nconst dataToUpload = 'Hirys world.';\ntry {\n\tconst receipt = await irys.upload(dataToUpload);\n\tconsole.log(`Data uploaded ==> https://gateway.irys.xyz/${'{\'}receipt.id{'\}'}`);\n} catch (e) {\n\tconsole.log('Error uploading data ', e);\n}"
    }
  }
}
```