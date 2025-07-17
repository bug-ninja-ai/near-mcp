<div align="center">
  <img src="assets/near-mcp.svg" alt="NEAR MCP Logo" width="200" />
</div>

[![npm version](https://badge.fury.io/js/@nearai%2Fnear-mcp.svg)](https://badge.fury.io/js/@nearai%2Fnear-mcp)
[![Telegram](https://img.shields.io/badge/Dev_Support-2CA5E0?style=flat&logo=telegram&logoColor=white)](https://t.me/nearaialpha)

# NEAR MCP

This project is a Model Context Protocol ([MCP](https://github.com/modelcontextprotocol)) compatible server for interacting with the [NEAR blockchain](https://near.org/). This tool provides a way for LLMs and AI agents to securely access and interact with NEAR accounts and blockchain functionality.

## Quickstart

Here is how to get started with the near-mcp server quickly with the `claude` code cli

```
npm install -g @anthropic-ai/claude-code
claude mcp add near-mcp npx @nearai/near-mcp@latest run
claude
```

Or deploy the MCP server remotely on Phala Cloud, check the instructions [here](./tee.md)

## Installing

`near-mcp` is meant to be used is with an MCP compatible client. Learn more in the [MCP docs](https://modelcontextprotocol.io/introduction)

Adding to the [`claude` code](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview) cli:

```bash
claude mcp add near-mcp npx @nearai/near-mcp@latest run
```

Adding to claude desktop via JSON config:

```json
{
  "mcpServers": {
    "near-mcp": {
      "command": "npx",
      "args": ["-y", "@nearai/near-mcp@latest", "run"],
      "env": {}
    }
  }
}
```

Adding to [`goose`](https://block.github.io/goose/)

```
┌   goose-configure
│
◇  What would you like to configure?
│  Add Extension
│
◇  What type of extension would you like to add?
│  Command-line Extension
│
◇  What would you like to call this extension?
│  near-mcp
│
◇  What command should be run?
│  npx @nearai/near-mcp@latest run
│
◇  Please set the timeout for this tool (in secs):
│  60
│
◇  Would you like to add environment variables?
│  No
│
└  Added near-mcp extension
```

Or you can install it globally and use it directly.

```bash
# Install globally
npm install -g @nearai/near-mcp@latest

# Or use directly with npx
npx @nearai/near-mcp@latest run
```

## Available Tools

This MCP server provides 22 tools organized into the following categories:

### System Management

- `system_list_local_keypairs` - List all NEAR accounts and keypairs in local keystore by network
- `system_import_account` - Import an account into local keystore from private key or file
- `system_remove_local_account` - Remove a local account from keystore

### Account Operations

- `account_view_account_summary` - Get summary information about any NEAR account
- `account_export_account` - Export a NEAR account from local keystore to file
- `account_sign_data` - Cryptographically sign data with account's private key
- `account_verify_signature` - Verify signed data against account's public key
- `account_create_implicit_account` - Create an implicit account derived from public key
- `account_create_account` - Create a new NEAR account with account ID
- `account_delete_account` - Delete an account from NEAR blockchain
- `account_list_access_keys` - List all access keys for an account
- `account_add_access_key` - Add access key to account (full access or function call)
- `account_delete_access_keys` - Delete access key from account by public key

### Token Operations

- `tokens_send_near` - Send NEAR tokens to an account
- `tokens_send_ft` - Send fungible tokens (FT) like USDC, USDT, WNEAR based on NEP-141/NEP-148

### Contract Interaction

- `contract_view_functions` - View available functions on a NEAR smart contract
- `contract_get_function_args` - Get arguments of a function call (experimental)
- `contract_call_raw_function_as_read_only` - Call contract function as read-only view method
- `contract_call_raw_function` - Call contract function as transaction (costs gas)

### Search & Discovery

- `search_near_fungible_tokens` - Search for fungible token contract information by account ID, symbol, or name

### DeFi Integration

- `ref_finance_get_pools` - Search for liquidity pools on Ref Finance exchange
- `ref_finance_get_swap_estimate` - Get swap estimate from Ref Finance exchange
- `ref_finance_execute_swap` - Execute token swap on Ref Finance

For detailed parameter specifications and usage examples, see [TOOLS.md](./TOOLS.md).

## Integration with AI Models

This tool is designed to be used with AI models that support the [Model Context Protocol](https://github.com/modelcontextprotocol). It enables AI assistants to:

1. Manage NEAR accounts on behalf of users
2. Check account balances and status
3. Sign and send transactions
4. Create new accounts and manage access keys
5. Inspect and execution smart contracts

## Security Considerations

- This MCP is meant to be run locally. Account private keys are stored in a local unencrypted keystore where the MCP server is running.
- The underlying models should not have access to see the private keys of the accounts they are interacting with with _one exception_. The `import_account` tool allows the model to import an account from a private key. This requires the user to provide the private key to the model.

## Contributing

We welcome contributions to the NEAR MCP server! Please see the [CONTRIBUTING.md](CONTRIBUTING.md) file for more information.

### Reporting Issues

If you find a bug or have a feature request, please open an issue on the GitHub repository.
