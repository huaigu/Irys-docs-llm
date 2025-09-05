```json
{
  "title": "Irys | Onchain Folders",
  "url": "https://docs.irys.xyz/build/d/features/onchain-folders",
  "content": {
    "onchainFolders": {
      "description": "Onchain folders are powerful way to organize transactions on Irys. Use them to reference onchain data by logical names instead of transaction IDs.",
      "whyUse": {
        "title": "Why Use Onchain Folders?",
        "points": [
          "Logical Grouping: Create organized and readable structures for onchain data.",
          "Human-Readable Referencing: Replace transaction IDs with logical names, improving accessibility.",
          "Cross-Ownership Grouping: Include any transactions on Irys, even if they weren’t created by you.",
          "Flexibility: Add new files to existing folders at any time."
        ]
      },
      "howItWorks": {
        "title": "How The Irys Gateway Resolves Onchain Folders",
        "steps": [
          "Looks up the manifest by ID.",
          "Looks in the manifest to see if the path exists.",
          "Returns the transaction associated with the path if found.",
          "Returns 404 if not found."
        ],
        "example": "https://gateway.irys.xyz/8eNpkShMwdbiNBtGuVGBKp8feDZCa21VppX2eDi3eLME/foo1.png"
      },
      "creatingFolders": {
        "title": "Creating Onchain Folders",
        "methods": [
          {
            "method": "Automatically",
            "description": "When you upload groups of files using the Irys SDK's uploadFolder() function or the CLI's upload-dir command, an onchain folder for you is automatically created for you."
          },
          {
            "method": "Manually",
            "description": "To manually create an onchain folder, create a JavaScript Map object where each entry maps a unique transaction ID to a unique path."
          }
        ]
      },
      "mutableFolders": {
        "title": "Mutable Onchain Folders",
        "description": "Mutable onchain folders let you add new files to an existing folder after it’s created.",
        "howToCreate": {
          "steps": [
            "Upload the Initial Folder.",
            "Reference Files Using a Mutable URL.",
            "Upload New Files.",
            "Create a Onchain Folder.",
            "Tag the New Manifest.",
            "Access the Updated Folder."
          ]
        }
      }
    }
  }
}
```