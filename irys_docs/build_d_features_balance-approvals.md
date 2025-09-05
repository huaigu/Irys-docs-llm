{
  "title": "Irys | Balance Approvals",
  "description": "Use balance approvals to share balances between multiple addresses. This helps to onboard users without requiring them to own tokens.",
  "features": [
    "You pay for transactions.",
    "Users sign transactions."
  ],
  "details": {
    "tokenRequirement": "Both approver and approvee must use the same token.",
    "registration": "Are registered instantly upon upload completion.",
    "transferability": "Are non-transferable.",
    "expiration": "Can be configured to expire automatically."
  },
  "createApproval": {
    "description": "To update an existing approval, create a new approval with the same address (it will overwrite the existing approval).",
    "code": "const receipt = await irys.approval.createApproval({\n  amount: irys.utils.toAtomic(1), // Amount in atomic units\n  approvedAddress: \"<address>\",\n  expiresInSeconds: 100, // Expires in 100 seconds. Delete to remove expiration.\n});"
  },
  "uploadUsingApproval": {
    "code": "const receipt = await irys.upload(\"Hirys World\", { upload: { paidBy: \"<address>\" } });"
  },
  "combineApprovalsAndTags": {
    "code": "const uploadOptions = {\n  upload: {\n    paidBy: \"<address>\",\n  },\n  tags: [{ name: \"Content-Type\", value: \"text/plain\" }],\n};\nconst receipt = await irys.upload(dataToUpload, uploadOptions);"
  },
  "revokeApproval": {
    "code": "const receipt = await irys.approval.revokeApproval({ approvedAddress: \"<address>\" });"
  },
  "getBalancesApprovedToUse": {
    "code": "const approvals = await irys.approval.getApprovals({\n  payingAddresses: [\"<address>\"],\n});"
  },
  "getFirst100Approvals": {
    "code": "const approvals = await irys.approval.getApprovals({});"
  },
  "returnType": "{\n  amount: string; // Amount approved in atomic units\n  payingAddress: string; // Address of the payer's wallet\n  approvedAddress: string; // Address of the wallet that received the approval\n  expiresBy: number; // Timestamp (in milliseconds) when approval expires\n  timestamp: number; // Timestamp (in milliseconds) when the approval was created\n  token: string; // Approved token\n}[];",
  "getApprovalsCreated": {
    "code": "const createdApprovals = irys.approval.getCreatedApprovals({\n  approvedAddresses: [\"<address>\"],
});"
  },
  "getFirst100CreatedApprovals": {
    "code": "const createdApprovals = irys.approval.getCreatedApprovals({});"
  },
  "getBalanceApprovalsViaHTTP": {
    "description": "You can also request balance approvals via HTTP:",
    "mainnetURL": "https://uploader.irys.xyz/account/approval?payingAddress=<...>&token=<...>&approvedAddress=<...>"
  }
}