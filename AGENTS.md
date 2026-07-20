# Documentation project instructions

## About this project

- This is a documentation site built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json`
- Use the Mintlify MCP server, `https://mcp.mintlify.com`, to edit content and settings via MCP
- Use the Mintlify docs MCP server, `https://www.mintlify.com/docs/mcp`, to query information about using Mintlify via MCP
- The primary product implementation is in the sibling `../plangrep-by-hand` repository. Its Open API routes, DTOs, tests, and `docs/open-api/openapi.v1.yaml` are the evidence for API documentation updates.

## Code-to-docs sync workflow

Most requests in this repository are documentation syncs for code changes in `../plangrep-by-hand`.

1. Identify the documentation baseline and inspect the implementation commits since that point. Use detailed git history and diffs, especially changes to `worker/control-plane/src/open-api.ts`, public DTOs, runtime API routes, API tests, and `docs/open-api/openapi.v1.yaml`.
2. Document only externally visible behavior: endpoints, authentication and scopes, request validation, response fields, limits, statuses, events, errors, and user-facing workflows.
3. Treat the running public API implementation and its tests as the primary source of truth. Use the OpenAPI file as the contract reference. If they disagree, do not silently choose one; report the discrepancy and update only behavior supported by the implementation.
4. Update every affected reference page, guide, concept page, navigation entry, and example. Keep field descriptions, JSON examples, error tables, and cross-links consistent with the code.
5. Do not document internal URLs, capability tokens, container job IDs, private object keys, implementation-only diagnostics, or internal orchestration details.
6. Preserve existing user-facing concepts unless the code explicitly changes or removes them. Do not invent migration paths or compatibility behavior.
7. When the user requests commits, group changes into small, cohesive commits by public contract area, such as jobs, source reads, reviews, or search. Do not commit unrelated work.
8. Before handing off, run `git diff --check`, search affected pages for obsolete field names or values, and run an available Mintlify validation command when the repository provides one.

## Terminology

- Use **project** for the persistent, organization-scoped container that holds processed files and extracted entities.
- Use **job** for asynchronous ingestion and processing work.
- Use **review** for a durable source-grounded question-and-answer workflow.
- Use **source** for extracted drawing regions, sheets, specification sections, and document entities.
- Use **Open API** for bearer-token HTTP endpoints and **MCP** for connected tool clients.

## Style preferences

- Use active voice and second person ("you")
- Keep sentences concise — one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references

## Content boundaries

- Document public Open API and MCP behavior that users can call or observe.
- Keep implementation details out of public pages unless they change how users integrate with the product.
- Do not document private administrative, runtime, billing-operation, container, security, or deployment-only interfaces.
