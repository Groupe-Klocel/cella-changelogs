# Release Notes — Cella Back

<!-- CHANGELOG:START -->

## [2.30.0] - 2026-06-14

### New features

- **AI assistant for warehouse operators.** A new AI chat capability is available in CELLA. Warehouse users can now send natural-language messages to a configured AI assistant that can answer questions about CELLA features, query warehouse data, trigger business functions, and generate documents — all enforcing the user's existing rights and permissions. The assistant supports conversation history and can receive context about the current screen (e.g. the delivery being viewed) to resolve references like "this delivery" automatically.

- **AI availability check.** A lightweight query lets the front-end know whether the AI assistant is enabled for the current warehouse and which functions and documents are exposed to it, so the chat interface can be shown or hidden accordingly.

- **Per-warehouse AI configuration (admin).** Warehouse administrators can now configure an AI provider (OpenAI, Anthropic, Google, Azure AI Foundry), model, API key (stored encrypted), language, and the list of exposed V2 functions and documents. Two independent policies (`queries_mode` and `mutations_mode`) control how broadly the assistant can operate: `rights` (everything the user can do), `allowlist` (an explicit list of operations), or `none` (fully read-only or no mutations).

- **AI-assisted documentation of exposed functions and documents (admin).** Administrators can ask the warehouse's own LLM to analyse the source code of a V2 function or document and automatically generate its description and expected context. A bulk refresh of all exposed items is also available.

- **Client-specific knowledge base (admin).** Administrators can add, update and remove custom documentation articles for a warehouse. These articles are merged with CELLA's built-in documentation and made available to the AI assistant when users ask "how-to" questions.

- **MCP server.** External AI clients that support the Model Context Protocol (e.g. Claude Desktop) can now connect to CELLA's MCP endpoint via OAuth 2.1 and use the same AI tool set with the connected user's rights.

- **Appointment lines now visible from related records.** Appointment lines are now accessible directly from Loads, Stock Owners, Third Parties, Locations, and Carriers, making it easier to see scheduling information in context without navigating away.

- **New translation creation with initial values.** It is now possible to create a translation entry and provide its translated values in a single operation, instead of creating the translation first and then adding values separately.

### Improvements

- **Faster search across all fields.** The "search across all fields" feature has been optimised and now responds significantly faster, particularly on large data sets.

- **`DIFFERENT` operator now available in advanced filters and autocount filters.** Users can now filter lists using a "is different from" condition, in addition to the existing equality and comparison operators.

- **Advanced filter fix.** A bug affecting the `DIFFERENT` operator in advanced filters has been corrected so results are now accurate.

- **Missing autocounts and navigation links added.** Several record counters and cross-entity navigation links that were absent from certain screens are now present.

## [2.29.0] - 2026-05-01

### New features

- **Appointments** – A new Appointment and Appointment Line module is now available. Users can create, read, update, and delete appointment records (including type, dates, status, allowed zones, driver/vehicle details, linked carrier, third party, load, and location) as well as their associated lines. Document attachments and status histories are supported on appointments.

- **Custom permissions** – Administrators can now define fine-grained, SQL-based data access rules (Custom Permissions and Custom Permission Lines) and assign them to warehouse workers. These rules are automatically applied to all read, update, and delete operations, limiting which records a given user can see or modify without requiring any change to the application screens.

- **Field-level custom permission targeting** – Custom permission lines now support an optional `field_name` attribute, allowing access rules to be scoped to a specific field on a data object.

- **Document attachments on additional objects** – The "document attachments" relationship is now available on a wide range of objects that previously lacked it: Articles, Loads, Load Lines, Purchase Orders, Purchase Order Lines, Deliveries, Delivery Lines, Delivery Addresses, Orders, Order Lines, Order Addresses, Rounds, Payments, Payment Lines, Movements, Handling Units, Handling Unit Contents, Handling Unit Inbounds/Outbounds and their content variants, Third Parties, Third Party Addresses, Third Party Address Contacts, Stock Owners, and Custom Objects/Lines.

- **Excel support in custom functions** – Custom code executed via the function engine can now read and write Excel files using both `openpyxl` and `XlsxWriter` libraries.

### Improvements

- **More reliable external function calls** – When a hook triggers an external function, the system now retries the call up to three times (with a short pause between attempts) before reporting a failure, reducing spurious errors caused by transient network issues.

- **Improved connection stability** – TCP keep-alive is now active on both the API containers and the AWS SDK client used for external calls, preventing idle connections from being silently dropped by the network infrastructure.

- **More robust database error messages** – Database errors during create, update, delete, and list operations now always return a meaningful message, even when the underlying error does not include the expected detail section that was previously required.

### Fixes

- **Report expressions using `datetime`** – Expressions in report templates that reference `datetime` (e.g. `datetime.date.today()`) now evaluate correctly again after a regression introduced by a dependency update.

- **Accurate error details on database constraint violations** – Error messages returned to the client when a database constraint is violated no longer crash with an unhandled exception when the error detail is missing or has an unexpected format.

## [2.28.0] - 2026-03-14

### New features

- **Generate multiple documents in a single call.** A new `generateDocuments` mutation lets you render several documents at once (each with its own name, context and optional filename) and receive all results in one response. The reply now also includes the document filename and a Base64-encoded copy of the file alongside the existing download URL.

- **Document attachments.** A new *Document Attachment* object is available in the API. You can create, update, delete and query document attachments individually or in bulk. Attachments can also be included when calling `generateDocuments`, where they are bundled with the other generated files (uploaded to storage, tracked in document history and sent by e-mail if recipients are configured).

- **New fields on Deliveries.**
  - Estimated number of boxes, estimated number of palettes and estimated load meters.
  - Pre-assigned load: a delivery can now reference a load that has already been assigned to it.
  - Value-added services (free JSON field) and MRN number (customs reference).

- **New fields on Loads.**
  - Truck and trailer information: licence plates (truck + 2 trailers), driver name, driver licence number and driver ID number.
  - MRN number for customs.
  - Three free-text reference fields (`reference1`, `reference2`, `reference3`).
  - The load now exposes its associated location directly as a sub-object.

- **In-process quantity on outbound handling-unit content.** A new `inProcessQuantity` field tracks the quantity currently being picked but not yet packed.

- **Custom permissions model.** Administrators can now define named custom permissions and assign them to warehouse workers, giving finer control over what each operator is allowed to do.

- **`managed_by_external_system` flag.** All major objects (articles, deliveries, loads, movements, orders, locations, handling units, etc.) now carry a flag indicating whether the record is owned and managed by an external system.

- **Printer filtering on the document-printing subscription.** When subscribing to `documentPrintings`, you can now supply a list of printers to watch and/or a list of printers to exclude, so each client only receives print jobs relevant to its station. Already-printed documents are also filtered out automatically.

### Improvements

- **Cubing now tries the largest containers first.** When several containers share the same priority, the packing algorithm now attempts the biggest ones first (by volume), improving compaction and reducing the number of boxes used.

- **Document generation now marks records as already printed when no printer is specified.** If a document is generated without a target printer, the history record is immediately flagged as printed, keeping the print queue clean.

- **Generated documents return more information.** Both `generateDocument` and `generateMergedDocument` now return the filename and a Base64 copy of the file in addition to the presigned URL.

- **Faster API responses under load.** Internal data-loading and resolver-lookup mechanisms have been optimised, reducing redundant work on requests that fetch many related objects simultaneously.

### Fixes

- **Restricted warehouse-worker stock owners** were not applied correctly in some queries; this has been fixed.
- **Null/None comparisons in automation rules** (hook filters) now behave as expected: `field is None`, `field == None` and similar expressions are correctly translated and evaluated.
- **Database session errors during cleanup** no longer cause unhandled exceptions; rollback and close failures are now caught and logged gracefully.

## [2.27.0] - 2026-02-21

### New features

- **Permission management via API:** It is now possible to create and delete permissions individually or in bulk through the API. Appropriate access controls are enforced — users can only manage permissions for warehouses they are authorised to administer, and standard (non-warehouse-specific) roles cannot be modified.

- **Movement sub-types exposed:** Stock movements now expose additional related details — including the stock owner, article, original and final handling units, handling unit contents, and original and final locations — making it easier to query complete movement information in a single request.

- **ZPL-to-PDF rendering engine choice:** When generating documents from ZPL templates, users can now choose between two PDF rendering engines: **Labelary** (existing) or the new **KloShip** renderer. The KloShip option accepts label dimensions in inches and handles the conversion automatically.

- **New "as-is until quantity" cubing mode:** A new cubing option allows the system to fill containers up to a given quantity threshold in "as-is" mode, distributing quantities evenly across the required number of containers rather than always creating fixed full-pack containers.

### Improvements

- **GraphiQL query sharing:** The built-in API explorer interface now supports sharing queries via URL. The current query, variables, and headers are reflected in the browser's address bar, so they can be copied and shared directly.

- **Movement stock-owner filtering:** Warehouse users with restricted stock-owner access will now have that restriction correctly applied when querying movements, in the same way it is applied to other stock records.

- **Cubing logging:** Cubing operations now produce detailed log entries at key stages (start, container loading, line estimation, completion), making it easier to diagnose issues when cubing produces unexpected results.

- **Volume and weight precision in cubing output:** Cubing results now report volume and weight as whole numbers, avoiding floating-point display artefacts in results.

### Fixes

- **Permissions query filter:** Filtering permissions by role, table, or mode in the API now works correctly.

- **Document generation with invalid warehouse:** Generating or merging documents when the warehouse associated with the session cannot be found now returns a clear error message instead of crashing.

- **ZPL-to-PDF connection security:** The Labelary rendering service is now called over HTTPS, preventing potential connection issues in secure network environments.

## [2.26.0] - 2026-01-01

### New features

- **Discount by fixed amount on orders and deliveries.** Orders, order lines, deliveries, delivery lines, purchase orders, and purchase order lines now support a discount expressed as a flat amount (in addition to the existing percentage discount). The discount type can be set per line or per document header.

- **"Fixed price" flag on orders.** An order can now be marked as *fixed price*, which tells Cella to skip its automatic price recalculation entirely. This is useful when prices are imported from an external system and must not be overwritten.

- **Document attachments.** A new *Document Attachment* record type is available, allowing files (identified by type, category and stock owner) to be linked to any Cella object.

- **Record validation configuration.** A new *Record Validation Config* object lets administrators define validation rules (filters, expected results, queries) that are evaluated when records of a given type are created or updated.

- **Maximum fill rate per handling unit model.** A *Max Fill Rate* percentage can now be configured on each handling unit model (default 100 %). The cubing engine will respect this limit when packing items.

- **Location linked to a load.** A location can now be assigned directly to a load record, indicating where the load is physically stored.

- **Separate stock-picking round option.** The round calculation profile now includes a *Separate Stock Picking Round* toggle.

- **External name and locking fields on all major objects.** An *External Name* field (searchable) and *Locked / Locked By / Locked At* fields are now available across all main Cella objects (articles, orders, deliveries, locations, handling units, loads, carriers, equipment, etc.), enabling richer integration and concurrency management.

### Improvements

- **Cubing dimension check corrected.** The engine now properly verifies that a product can physically fit inside a container by testing all possible orientations together (not each dimension independently). This prevents cases where a product was incorrectly rejected or incorrectly accepted.

- **Warehouse-worker creation error handling.** When creating a warehouse worker fails due to a database constraint (e.g. a duplicate entry), the system now returns a clear, user-readable error message instead of a generic failure. The `restrict_stock_owner` and `allow_login_without_sso` settings are also correctly saved during creation.

- **Improved price calculation for amount-based discounts.** When a line discount is expressed as a fixed amount, the unit price including taxes is now computed correctly, consistent with the line total.

- **Report rendering — rounded corners.** Text elements, frames, and other report blocks that have a border radius configured will now render with properly rounded corners in PDF output.

- **Report export to spreadsheet — text cells.** Cells explicitly typed as *text* in a report template are now exported to spreadsheets as text, preventing the spreadsheet application from auto-detecting and converting their content (e.g. numbers or dates stored as text).

- **ReportBro updated to version 3.12.0.** The reporting engine has been upgraded; this brings stability and rendering improvements to PDF and spreadsheet output.

### Fixes

- **Cubing rejected valid products.** A logic error in the dimension check caused certain products to be wrongly excluded from otherwise suitable containers. This is now resolved.

- **Warehouse-worker creation missing fields.** Two settings (`restrict_stock_owner` and `allow_login_without_sso`) were not saved when a warehouse worker was created via the API. This is now fixed.

- **Order price recalculation now respects the "fixed price" flag.** Orders flagged as fixed price are no longer recalculated, preserving externally provided prices.

## [2.25.1] - 2025-12-07

_Internal technical maintenance, no visible functional impact._

## [2.25.0] - 2025-12-07

### New features

- **Excel import now supports "update" and "delete" operations.** In addition to creating records, Excel import files can now update existing records (by matching on criteria columns, prefixed with `_`) or delete them using advanced filters. This makes mass data maintenance significantly more flexible.

- **Advanced ID inputs on create mutations.** When creating records via the API, it is now possible to identify a related record by one of its human-readable fields (e.g. a name or code) rather than having to supply an internal UUID. The system resolves the reference automatically and returns a clear error if no match or multiple matches are found.

- **SSO login now returns specific, actionable error codes.** When a Single Sign-On token is expired or otherwise invalid, the system now returns a dedicated error code (`SSO-000005` / `SSO-000006`) instead of silently returning nothing, making it easier to diagnose login failures.

- **SSO configuration validation extended.** The API now also checks that SSO metadata is present and returns a dedicated error (`SSO-000003`) when it is missing, rather than a generic "not found" error.

- **Hooks can now trigger in-app notifications and call warehouse functions directly.** The hook management service has been extended to support new hook types: push an in-app notification to a warehouse worker (`NOTIF`, `NOTIF_WM`, `NOTIF_MOBILE`) or execute a warehouse function (`FUNCTION` / `HTTP`) when a record change is detected.

- **Cubing: inner dimensions and volume percentage limit.** Containers used in the cubing calculation can now be given separate inner dimensions (`insideLength`, `insideWidth`, `insideHeight`). A new `maxVolumePercent` limit allows capping usable container volume to a percentage of total capacity.

- **Cubing: expansion coefficient on content configurations.** Content configurations now accept an `expansionCoefficient` field so that items requiring extra space (e.g. due to packaging) are accounted for correctly in volume calculations.

- **Cubing: maximum number of content lines per container.** A new `maxContents` limit on containers prevents more than a given number of distinct content lines from being packed into a single container.

- **GraphQL schema introspection is now disabled on production.** This reduces the attack surface on live environments; introspection remains available on non-production instances for development purposes.

---

### Improvements

- **Paramiko (SSH library) is now available in warehouse functions.** Custom functions can now use Paramiko for SSH/SFTP operations without any extra setup.

- **Parameter and configuration substitution in functions is faster.** The `[____…____]` placeholder replacement now reads values from the in-memory cache when available, avoiding extra database queries on each function execution.

- **Internal pre/post hook functions are compiled once at start-up.** Warehouse-specific pre- and post-processing logic is now compiled when the server loads, not on every single API call, reducing per-request overhead.

- **Function execution history is written asynchronously.** Saving the log of a function execution is now done in the background so it no longer adds latency to the function's response.

- **Scheduled tasks now run through the standard GraphQL API.** The scheduler invokes functions via GraphQL (like any other client) rather than duplicating internal logic, making behaviour consistent and easier to maintain.

- **Hook management service runs two parallel instances in production** for higher availability and throughput.

- **Error details are stored on failed hook requests.** When a hook cannot be processed, the error message is now saved on the hook request record, making troubleshooting much easier.

- **Better error propagation on bulk update.** When a bulk update fails, the error response now includes the specific variables that caused each failure, not just a generic message.

- **Warehouse functions and configurations reload together.** Changing a warehouse configuration or parameter now also triggers a reload of the in-memory function cache, ensuring custom logic always sees the latest settings.

---

### Fixes

- **Deleting a warehouse worker no longer fails intermittently.** An incorrect synchronous database call in the delete operation has been replaced with the correct async call, preventing random errors when removing users.

- **Cubing no longer crashes when an item or container has zero volume, weight, or quantity.** These edge cases now produce clear error messages in the cubing result instead of an unhandled exception.

- **Cubing compaction now correctly skips "as-is" containers** (containers that represent a single item sold in its own packaging) so their dimensions are never incorrectly swapped for a smaller container.

- **Cubing dimension checks now use inner dimensions** rather than outer dimensions, giving accurate fit results when inner and outer sizes differ.

- **Logging no longer fails when called from a background or server-side task** (i.e. when there is no HTTP request in context). The logger now gracefully falls back to a `SERVER_TASK` identifier.

- **WebSocket connections no longer fail with a binary encoding error.** A JSON serialisation issue affecting WebSocket responses has been resolved.

## [2.24.0] - 2025-10-18

### Fixes

- **Data export now correctly reflects the column order and column headings** defined in the list view: exported files (e.g. spreadsheets) will have their columns arranged and labelled exactly as configured on screen, rather than in an arbitrary order with raw technical names.
- **Nested data fields are now properly flattened during export**, preventing blank or missing values in exported files when the data contains multi-level information (e.g. linked records).
- **Export is compatible with both current and older interface versions**, ensuring that warehouses still running a previous front-end release do not experience broken exports after this server update.

## [2.23.0] - 2025-09-13

### New features

- **Environment-specific favicon**: The application icon displayed in the browser tab now reflects the current environment (development, staging, pre-production, or production), making it easier to identify at a glance which instance of Cella you are working in.

### Improvements

- **Report generation – table headers**: Table headers in generated PDF reports are now rendered correctly each time they appear (e.g. on each page), including any dynamic parameters they contain. Previously, headers could display stale or missing content on subsequent pages.
- **Report generation – linked text**: Hyperlinks embedded within text blocks in PDF reports no longer cause preceding text to be lost or misplaced.
- **Improved list query performance and correctness**: Data list screens that do not require cross-table filtering now use a more direct query path, which is faster and avoids edge cases where results could be missing or incorrectly ordered. Results are also now returned in a consistent, stable order.
- Updated internal libraries to their latest stable versions, improving overall stability and security.

### Fixes

- **Delivery launch – boxes without a round**: When launching a delivery, boxes (handling units) that are not yet assigned to a picking round are now only included in the launch process when the warehouse parameter `launch_boxes_without_round` is explicitly enabled. Previously, these unassigned boxes were always processed during launch, which could cause unintended behaviour.

## [2.22.0] - 2025-08-02

### New features

- **Round Calculation Profiles** — It is now possible to create, view, update and delete round calculation profiles and their associated equipment assignments. These profiles allow configuring how picking rounds are calculated (e.g. whether to group by building, stock owner or delivery date, whether to create replenishment, etc.).
- **Outbound handling unit barcodes** — Barcodes can now be recorded against outbound handling units. Full create, read, update and delete operations are available.
- **Send notification mutation** — A new action (`sendNotification`) lets integrations and automated processes push in-app notifications directly to a named warehouse worker, with an optional preview text and structured arguments.
- **Long-running function execution** — When triggering a custom function, it is now possible to mark it as a long-running task. The API returns immediately with a confirmation, and the function continues to execute in the background without blocking the caller.
- **Notification on function completion** — When executing a function, you can now request that a notification be sent to the caller once the function finishes, including the final status and result.
- **Round name on movements** — Movements now carry the name of the round they belong to, making it easier to trace and filter movements by round.
- **Building priority order** — Buildings now have an `order` field, allowing them to be ranked by priority.
- **Extended hook notification types** — Hooks of type `NOTIF_WM` and `NOTIF_MOBILE` are now handled alongside the existing `NOTIF` type, with richer structured payloads sent to the recipient.
- **Notification security** — Users can now only update or delete their own notifications; attempts to modify another user's notifications are rejected.

### Improvements

- **Faster data loading on complex screens** — Screens and queries that load many related records at once (e.g. lists with numerous child objects) are noticeably faster thanks to optimised batch processing of database lookups.
- **Better query performance with large datasets** — When fetching related data for more than 100 records at a time, the system now uses a more efficient database join strategy instead of a plain list, reducing response times for high-volume queries.
- **Improved API stability and scalability** — The infrastructure serving the API has been reconfigured to start more instances by default and scale more aggressively under load, improving responsiveness during peak activity.
- **GraphQL batch queries enabled** — The API now supports batching of up to 100 GraphQL operations in a single request, reducing network round-trips for clients that issue multiple queries together.

### Fixes

- **Search filter with exclusion operator** — Filters using the exclusion (`^`) operator now correctly ignore the marker characters and apply the intended pattern match, preventing unexpected empty results.
- **Wildcard search now performs exact-pattern matching** — Searches containing `%` wildcards now use exact-case pattern matching rather than case-insensitive matching, giving more predictable results.

## [2.21.0] - 2025-07-06

### Fixes

- Hook (automation trigger) filters that reference field names are now evaluated exactly as written, preventing cases where camelCase field names were incorrectly converted and caused the filter condition to fail or be ignored.

### New features

- New customised permission types are available, giving administrators finer-grained control over what individual users or roles can access and do within the system.

## [2.20.2] - 2025-06-28

_Internal technical maintenance, no visible functional impact._

## [2.20.1] - 2025-06-28

_Internal technical maintenance, no visible functional impact._

## [2.20.0] - 2025-06-21

### New features

- **Single Sign-On (SSO) login for warehouse workers.** Users can now log in via their organisation's identity provider (e.g. Microsoft Entra, Okta). A new "SSO login" option is available on the login screen. Administrators can also enforce SSO for a warehouse so that standard username/password login is blocked for workers who do not have an explicit exemption.
- **New data fields available on several records.**
  - *Block* records now have a **location mask** field, making it possible to define naming patterns for locations within a block.
  - *Delivery* records now have a **carrier** field, allowing a carrier to be linked directly to a delivery (in addition to the carrier shipping mode).
  - *Equipment detail* records now have a **location category** field for finer classification of equipment positions.
- **Forced ID on record creation.** When creating a new record via the API, it is now possible to specify the exact identifier the record should receive, instead of having one generated automatically. This is useful for data-migration and integration scenarios.
- **New filter operators: LIKE, ILIKE, and exclusion (^).** List screens and integrations can now filter data using explicit case-sensitive (`LIKE`) or case-insensitive (`ILIKE`) pattern matching, as well as an exclusion prefix (`^`) to omit certain values from results.
- **Stock-owner relationship visible on rules.** A rule record now exposes its linked stock owner directly, so users can see which stock owner a rule belongs to without additional lookups.
- **Warehouse worker–stock owner link now shows related details.** The warehouse-worker/stock-owner association record now displays the full stock-owner and warehouse-worker information in a single view.

### Improvements

- **Barcode rendering in printed documents improved.** Barcodes in PDF labels and reports now respect horizontal and vertical alignment settings. Rotated barcodes also render more accurately within their designated space, and an explicit error is raised if a barcode is too large to fit rather than silently producing a broken layout.
- **Minimum page height for PDF reports reduced.** The minimum allowed page height has been lowered from 30 mm to 10 mm, enabling the creation of very narrow label formats that were previously rejected.
- **Sorting on grouped lists is more reliable.** When viewing lists that use aggregation (grouped results), sorting by any column now works consistently — previously, only columns that were part of the grouping could be used for sorting.
- **Exact-match filtering is faster for ID fields.** Filters on fields whose name contains "id" now use exact database matching instead of a pattern search, which is significantly faster on large datasets.
- **Volume values on content records now support decimal quantities.** The volume field in cubing/content calculations can now hold fractional values, preventing rounding errors when volumes are not whole numbers.
- **Report engine updated to version 3.11.0.** The underlying PDF report generator has been updated, bringing in the latest rendering fixes and improvements from the upstream project.

### Fixes

- **Sorting no longer causes errors in the integrator centre.** A specific case in the integrator centre where applying a sort order could produce an unexpected error has been resolved.
- **Rules management simplified and stabilised.** The logic for creating and reordering rule versions and rule version configurations has been moved into the core engine, removing a layer of custom code that could produce inconsistent results (e.g. incorrect version numbering or order values after concurrent edits).

## [2.19.0] - 2025-05-10

### New features

- **New equipment options:** Five new configuration flags are available on equipment records:
  - **Force repalletization** – automatically triggers a repalletization step when relevant.
  - **Dynamic cubing** – enables dynamic volume calculation during picking rounds.
  - **Launchable if no stock** – allows a round to be launched even when no stock is currently available.
  - **Mono block** – splits picking rounds by warehouse block.
  - **Mono building** – splits picking rounds by warehouse building.
- **SSO front secret:** A new field is available on warehouse settings to store a front-end secret used for SSO authentication flows.

### Fixes

- **Bulk stock-feature update no longer causes deadlocks:** When updating multiple handling-unit content features at once, a locking issue that could block other operations has been resolved.
- **Handling-unit quantity recalculation corrected:** When a content feature is moved from one handling-unit content to another, the quantity of the previous content is now only recalculated if it actually changed, avoiding unnecessary and potentially incorrect updates.
- **Handling-unit modification timestamp no longer updated redundantly:** The last-modified date on a handling unit is now refreshed at most once per minute, preventing excessive write operations during bulk updates.
- **Warehouse custom functions now execute reliably:** Custom business logic attached to create, update, and delete operations (pre/post hooks) is now resolved correctly under all conditions, fixing cases where the function could silently fail to be found and called.

### Improvements

- Various third-party libraries used by the platform have been updated to their latest stable versions, bringing security patches and minor reliability improvements with no change to day-to-day workflows.

## [2.18.0] - 2025-04-30

### Improvements

- PDF document generation no longer relies on the commercial ReportLab PLUS licence. The system now uses an open-source RML processing library, so document generation continues to work without requiring a paid licence renewal.
- Temporary files are no longer created on disk during PDF generation, reducing I/O overhead and avoiding potential file-system clutter.

## [2.17.8] - 2025-04-26

### Fixes

- **Corrected status codes for "To Be Checked" and "Checked" steps** – The numeric values used internally for the *To Be Checked* and *Checked* statuses on deliveries, outbound handling units, and outbound handling unit contents have been corrected. Workflows that rely on these statuses (e.g. quality-check steps before dispatch) will now progress correctly.

- **Custom warehouse functions no longer silently ignored** – An indentation error caused custom internal functions configured for a warehouse to be loaded only for the first function found, and ignored for all others. All configured functions are now loaded and applied as intended.

- **Database lock errors during stock quantity updates resolved** – Concurrent operations (create, update, or delete of handling unit contents or their features) could cause database lock conflicts, leading to errors or incorrect quantity values (Redmine #30878). Proper record locking and transaction commit sequencing have been applied to prevent this.

- **Unnecessary quantity recalculations skipped** – When a handling unit content had no feature lines and its quantity was already zero, the system would still trigger a redundant update. This extra operation is now skipped, reducing unnecessary database writes.

## [2.17.7] - 2025-04-21

### Fixes

- **Bulk update with advanced filters now works reliably.** When using advanced filters to select which records to update in bulk, the operation could previously fail or behave incorrectly due to a database session conflict. This is now resolved, and bulk updates correctly apply to all matching records.

### Improvements

- **Faster API response times for repeated queries.** The server now caches a larger number of recently used queries (up to 10 000 instead of 1 000) and also caches query validation results. Users performing the same or similar operations repeatedly should notice quicker responses.

## [2.17.6] - 2025-04-20

_Internal technical maintenance, no visible functional impact._

## [2.17.5] - 2025-04-20

_Internal technical maintenance, no visible functional impact._

## [2.17.4] - 2025-04-20

### Improvements

- **Faster data loading on screens with linked records.** The server now avoids fetching the same record multiple times when several items on a screen share related data. Pages that display lists with many linked fields (e.g. locations, stock, movements) should load noticeably faster.

- **Advanced filters now work correctly on related-record panels.** When a sub-list is displayed inside a record (e.g. stock lines within a location), any active filters are now properly applied, so the results shown match the filters set by the user.

- **Sorting on related-record panels is more reliable.** Sorting options are now taken into account when grouping and caching related-record queries, preventing cases where a different sort order could return incorrectly cached results.

- **Large sub-lists are no longer capped at 1 000 items.** Related-record panels that display more than 1 000 lines now use the optimised loader, removing the previous hard limit.

### Fixes

- **Duplicate entries no longer appear in related-record panels.** A deduplication fix prevents the same record ID from being fetched twice, which could previously cause duplicate rows to appear in linked lists.

- **Record data returned after create or update operations is more reliable.** The server now uses an optimised and more accurate method to build the response sent back after saving a record, reducing the risk of missing or mismatched field values in confirmations.

## [2.17.3] - 2025-04-19

### Improvements

- Loading related lists of records (child lists) in the application is now significantly faster. When displaying standard data without custom filters or pagination, the system now batches and retrieves all related records in a single, optimised database query instead of one query per record. This reduces server load and speeds up page and list loading noticeably, especially when many records are displayed at once.

## [2.17.2] - 2025-04-19

### Improvements

- **Better performance under heavy load** – The server can now handle significantly more simultaneous data requests (capacity doubled), so pages and lists load faster during peak warehouse activity without requests queuing or timing out.
- **More stable database connections** – The connection pool has been enlarged, reducing the risk of "connection unavailable" errors when many users or automated processes hit the system at the same time.
- **Related-data lists now load in parallel** – Child record lists (e.g. stock lines linked to a location or order) are now fetched concurrently instead of one at a time, noticeably speeding up screens that display nested or linked data.
- **Improved resource cleanup** – Database sessions are now properly closed after every query, even when errors occur, reducing the chance of slow queries or resource exhaustion over time.

## [2.17.1] - 2025-04-19

### Fixes

- Fixed a connection issue that could prevent the hook management service from reaching the database when the database password or connection string contains a `%` character. Hook processing and status updates now work correctly in all configurations.

## [2.17.0] - 2025-04-19

### New features

- **Watermarks on PDF documents.** Reports can now include text or image watermarks, placed either behind or in front of the document content, with configurable rotation angle and opacity.
- **Rich-text content in reports.** Text elements that use rich-text formatting (bold, italic, underline, colour, font, alignment, links, etc.) are now fully rendered in generated PDF documents and exported correctly to spreadsheets.
- **`generateMergedDocument` mutation.** A new API operation lets users merge multiple documents into a single output in one request.
- **New fields on Handling Unit Content Inbound (HUCI).** Several additional fields are now available on inbound handling-unit content records: article, location, handling-unit names, stock owner, article LU name, and a structured features field.
- **New fields on Movements.** Movement records now expose an assigned user, a final block, and a next location.
- **Processing result tracking.** All entities that support extras now store the last processing result code and its detail, making it easier to trace what happened during automated processing steps.
- **Hook management service.** A new dedicated background service manages webhook/hook processing, improving reliability of event-driven integrations.
- **Hard-delete option on bulk-delete mutations.** Bulk-delete operations can now perform a permanent (hard) deletion when required.

### Improvements

- **Faster server start-up and lower latency.** Warehouse workers, permissions, configuration settings, and parameters are now loaded into memory at start-up and refreshed automatically when a change is detected in the database, reducing repeated database round-trips.
- **Live reload of in-memory data.** The server listens for database change notifications and reloads only the affected warehouse configuration or parameter set, keeping data fresh without a full restart.
- **Asynchronous document generation.** PDF and spreadsheet documents are now generated asynchronously, so large or complex reports no longer block other operations.
- **Text-shaping support for barcodes and rich text.** Barcode display values and rich-text blocks now support advanced font rendering (text shaping), which is required for right-to-left scripts and complex typefaces.
- **Better error messages.** Several error responses have been made clearer and more descriptive, particularly for delivery checks, role operations, and delete operations.
- **Improved WebSocket subscription stability.** GraphQL subscriptions (record changes, document printings, notifications) now clean up their database connections properly when a client disconnects, preventing resource leaks.
- **Smaller database connection pool.** The connection pool size has been reduced to better match actual concurrent usage and free up database resources.
- **History tracking for custom functions.** Changes to function definitions and function versions are now recorded in the audit history, giving full traceability of customisation changes.

### Fixes

- Fixed an issue where updating a role could fail or leave permissions in an inconsistent state.
- Fixed bulk-create for locations.
- Fixed bulk-update operations that could silently skip records.
- Fixed order price not being recalculated correctly on certain updates.
- Fixed the `round_line_check_status` and `delivery_line_check_status` functions returning incorrect results in some scenarios.
- Fixed the outbound handling-unit pre-update check so that cancellation is correctly blocked or allowed depending on the current status.
- Fixed creation of warehouse workers when a user role needs to be assigned at the same time.
- Fixed `create_handling_unit_with_content` mutation failing under certain conditions.
- Fixed delete mutations that could error when no transaction ID was provided.
- Fixed parameter reload for warehouses whose ID contains an underscore.
- Fixed transaction ID handling so that passing `None` no longer causes unexpected errors in update operations.
- Fixed document and notification history records being incorrectly wrapped in a database transaction.
- Fixed GraphQL subscriptions not properly closing their cursor and removing their database listener on disconnect.

## [2.16.0] - 2025-04-06

### New features

- **Pattern Path Links**: A new "Pattern Path Link" concept is available, allowing a single pattern path to be associated with multiple patterns (and vice versa). You can now create, update, delete, and search pattern path links individually or in bulk.
- **"Is strict" flag on Patterns**: Patterns now have an "Is strict" option that can be set to control how strictly the pattern rules are applied during operations.
- **Partial delivery flag**: A "Partial delivery" option has been added to Deliveries, Orders, Third Parties, and Carrier Shipping Modes, making it possible to explicitly mark these records as allowing partial fulfilment.
- **Location dimensions and weight**: Storage locations can now store physical measurements (length, width, height, weight), enabling more precise capacity and compatibility checks.
- **Assigned user on Rounds**: A round can now have a specific user assigned to it directly on the round record.
- **Bulk creation of Locations**: Locations can now be created in bulk in a single operation, in addition to the existing individual creation.
- **System configurations and parameters can now be created**: It is now possible to create system-level configuration entries and parameters through the standard interface.

### Improvements

- **Delivery cancellation cascades to lines**: When a delivery is cancelled, its associated delivery lines are now automatically cancelled as well, preventing orphaned open lines.
- **Outbound handling unit cancellation cascades**: When an outbound handling unit is cancelled, all its associated outbound handling unit contents are also automatically cancelled.
- **Pattern and pattern path deletion safeguards updated**: Deleting a pattern or pattern path now correctly checks for existing pattern path links before allowing a hard delete, preventing data integrity issues.
- **Parent handling unit name stored on inbound and outbound records**: Inbound and outbound handling unit records now retain the parent handling unit name as a text reference, preserving traceability even if the physical handling unit record is removed.
- **Faster server start-up in production**: The server now starts significantly faster in production and pre-production environments thanks to an optimised initialisation process.

### Fixes

- **Delivery line cancellation threshold corrected**: Delivery lines were being cancelled prematurely during certain delivery status transitions. The correct threshold is now applied, so lines are only cancelled at the appropriate stage.

## [2.15.0] - 2025-03-14

### New features

- **ReportBro document generation**: Reports can now be exported directly as PDF (`rbo_pdf`) or Excel (`rbo_xls`) using the ReportBro engine. A customised version of the ReportBro library is bundled to ensure consistent, accurate rendering of layouts, barcodes (Code 39, Code 128, EAN-8, EAN-13, UPC, QR code), tables, frames, sections and images.

### Fixes

- **Concurrent record updates**: When two users (or processes) attempt to update the same record at the same time, the system now locks the record before applying changes. This prevents data corruption or lost updates that could occur under high concurrency.
- **Reduced "Too Many Requests" errors**: The system now retries more aggressively when cloud rate limits are hit, reducing the frequency of failed requests seen by users during peak load.

## [2.14.0] - 2025-03-02

### New features

- **HTML-to-PDF conversion:** A new endpoint allows the system to convert HTML content (with optional CSS styling) directly into a PDF document, enabling richer and more flexible document templates.
- **PDF-to-ZPL conversion:** A new endpoint converts PDF documents into ZPL format, making it possible to print PDF-based labels directly on Zebra and compatible label printers.
- **HTML document templates:** Document templates written in HTML are now fully supported. When a document of type HTML is generated, it is automatically rendered as a PDF ready for download or sending.
- **Python document type support:** Python-based document templates are now recognised as a valid output type during document generation.
- **Barcode and image helpers available in DOCX templates:** When generating Word (DOCX) documents, barcode generation and base64 image embedding are now available directly within the template context, allowing labels and images to be included in Word-based documents.
- **Long-running task option:** Document generation and function execution now support a "long-running task" flag, allowing operations that take more time to complete without timing out.

### Improvements

- **PDF generation library updated:** The ReportLab library used for PDF generation has been updated to a newer version, bringing stability and compatibility improvements.
- Internal libraries and dependencies used across all background functions have been updated to their latest stable versions, improving reliability and security.

## [2.13.0] - 2025-02-09

### Improvements

- When listing translations, warehouse-specific translations now automatically take priority over the standard (generic) translations for the same entry. Users will see their warehouse's customised labels and messages instead of the default ones wherever a specific translation has been defined, without needing to do anything differently.
- The translation count displayed in paginated lists now correctly reflects this override logic, so the totals and page numbers shown are accurate and consistent with the results returned.

## [2.12.0] - 2025-01-19

### New features

- **Translations can now be managed per warehouse.** Authorised users can create, update, and delete custom translations specific to their warehouse directly through the API.
- **Warehouse-specific translation list.** A dedicated query returns the merged list of translations for a warehouse worker: standard (shared) translations are returned by default, but any warehouse-specific override automatically takes precedence.
- **Translation permissions.** Translations are now covered by the standard permission system (read, create, update, delete), giving administrators fine-grained control over who can manage them.

### Fixes

- **Translation read now correctly scoped.** Fetching a single translation is restricted to translations that belong to the requesting user's warehouse, preventing accidental access to other warehouses' data.
- **Protection against cross-warehouse translation changes.** Creating, updating, or deleting a translation for a warehouse other than your own is now blocked with a clear permission-denied error.
- **Standard (shared) translations cannot be modified by warehouse users.** Only super-administrators can create or modify translations that are not tied to a specific warehouse, preventing accidental changes to system-wide labels.
- **Warehouse ID cannot be changed on an existing translation.** Attempting to move a translation to a different warehouse is now explicitly rejected.

## [2.11.0] - 2025-01-12

### Fixes

- Fixed an issue where PDF, image (PNG, JPG, JPEG), and ZIP documents returned by KloShip could not be generated or printed correctly. These document types are now handled properly, so labels and shipping documents produced via KloShip are generated and available as expected.

## [2.10.0] - 2024-12-28

### New features

- **New custom function management (V2).** Administrators and integrators can now create, version, and manage custom functions with a richer model that supports three levels of scope: standard (platform-wide), client-specific, and warehouse-specific. When a function exists at multiple levels, the most specific version (warehouse > client > standard) is automatically selected at runtime.
- **Per-warehouse function deployment.** A new "deploy" mechanism lets you choose which active version of a function is used in each warehouse, independently of other warehouses. You can deploy, update, or undeploy a function version per warehouse without affecting others.
- **Translation table.** A new translation repository is available in the system, enabling warehouse-specific label and text overrides by language.
- **Function execution history enriched.** Each function execution record now also captures the function identifier (in addition to its name), making it easier to trace history when multiple versions or scopes of the same function exist.

### Improvements

- **Function execution priority logic.** When a scheduled task or an incoming webhook triggers a custom function, the system now automatically picks the most appropriate version: warehouse-specific first, then client-specific, then the standard version. The previous (V1) function lookup remains as a fallback so existing functions continue to work without any changes.
- **Stricter access controls on custom functions.** Creating, updating, or deleting a function or a function version is now blocked if the requesting user does not have rights over the target warehouse or client. Integrator users can only manage functions belonging to their own warehouses or clients.
- **Active version is protected.** It is no longer possible to edit or delete a function version that is currently marked as active in any warehouse deployment, preventing accidental disruption of running operations.
- **Real-time connection stability.** Dropped or cancelled WebSocket connections (used for live screen updates) are now handled gracefully, avoiding error noise in the logs and improving overall reliability of real-time features.

### Fixes

- **Subscription errors with latest platform update.** A compatibility issue that could cause live-update subscriptions to fail after a platform library upgrade has been resolved. Real-time notifications should now work consistently.
- **Stock owner logo field.** A validation error that could occur when saving a stock owner record with a logo URL in certain formats has been corrected.

## [2.9.0] - 2024-12-22

### Fixes

- **Handling unit content features on articles without a feature type:** Attempting to create a handling unit content feature (HUCF) for an article that has no feature type now correctly returns a clear error message instead of silently succeeding or failing in an unexpected way. This prevents inconsistent stock data caused by feature records attached to articles that are not configured to use them.

### Improvements

- **JSON fields now accept lists as well as objects:** Custom JSON fields across records (create, bulk create, update, and bulk update) can now store list values (e.g. `[1, 2, 3]`) in addition to key/value objects. Previously, submitting a list in a JSON field could cause it to be saved incorrectly.

## [2.8.0] - 2024-11-03

### New features

- **Warehouse worker profiles now fully editable:** All additional fields on a warehouse worker record — including extra text and numeric fields, SSO login permission, stock owner restriction, and token check — can now be updated through the system. Previously, changes to these fields were silently ignored.

- **Stock-owner filtering on rule execution:** When executing a business rule, the system now respects the stock owner restriction configured on the operator's profile. Operators whose access is limited to specific stock owners will only see rules applicable to those stock owners. A specific stock owner can also be passed explicitly when calling a rule.

- **Equipment reservation pattern:** Equipment records now expose their associated reservation location pattern, making it available wherever equipment details are displayed or used.

### Improvements

- **Rule execution is now more reliable:** The rule selection logic was corrected so that only the rule matching the requested name is evaluated, and conditions that reference missing context variables now correctly exclude the rule step from consideration. This prevents incorrect or unexpected rule outcomes.

### Fixes

- **Packages can no longer be added to a shipped delivery:** The system now blocks any attempt to add a package (handling unit outbound) to a load that has already been dispatched, preventing data inconsistencies on completed shipments.

- **Dispatched loads are now protected from modification:** Any update to a load that has already been dispatched — including adding new lines — is blocked with a clear error message, preserving the integrity of shipped records.

- **Parameter deletion checks now work correctly:** When checking whether a configuration parameter is still in use before deleting it, the system now compares values correctly, preventing false positives that could have blocked valid deletions.

## [2.7.1] - 2024-10-20

### New features

- **SSO (Single Sign-On) configuration per warehouse** – Each warehouse can now be fully configured to authenticate users via an external identity provider (SSO). Administrators can define the SSO type, authentication and token URLs, client credentials, redirect URI, scope, and metadata directly at the warehouse level.
- **Enforce SSO login per warehouse** – A new option lets administrators require that all users of a warehouse log in exclusively through SSO, preventing standard username/password access.
- **Allow selected users to bypass SSO** – Individual warehouse workers can be granted an exception to log in without SSO even when SSO is activated for their warehouse, giving administrators fine-grained control over access methods.

## [2.7.0] - 2024-10-20

### New features

- **SSO (Single Sign-On) support for warehouses:** Warehouses can now be configured to authenticate users via an external SSO provider. Administrators can set the SSO type, authentication URLs, client credentials, redirect URIs, token and disconnect URLs, scope, and metadata directly on the warehouse record.
- **Enforce SSO login at warehouse level:** A new "SSO login enforced" option on the warehouse prevents users from bypassing SSO and logging in with a local password.
- **Allow selected workers to bypass SSO:** Individual warehouse workers can be granted an exception to log in without SSO, even when SSO enforcement is active for their warehouse.
- **Reservation pattern on equipment:** Equipment records now support a dedicated reservation pattern, allowing separate picking path logic for reservation operations.

### Improvements

- **Faster and more reliable webhook processing:** Webhook triggers (notifications, record history, document printing) now use deferred database triggers, reducing the risk of processing records before they are fully committed. The retry window for locating a record has also been extended (up to 30 attempts), and retry intervals are shorter (0.5 s instead of 1.5 s) for quicker recovery.
- **Webhook read/write separation:** Webhooks now read data from a dedicated read replica and write only when necessary, improving overall system stability and reducing load on the primary database.
- **ZPL document generation options clarified:** The page orientation and page size options available when generating ZPL documents (Portrait/Landscape, Letter/Legal/A4/A5/A6) are now correctly labelled — the "A6" size was previously displayed incorrectly.
- **Report generation updated:** The reporting engine has been updated to a newer version, bringing stability and compatibility improvements to PDF and label document output.

### Fixes

- **Webhook record history payload corrected:** An issue that could produce malformed JSON in webhook payloads for record history events has been resolved, ensuring downstream integrations receive well-formed data.
- **Warehouse creation error resolved:** A problem that prevented new warehouses from being created correctly has been fixed.

## [2.6.0] - 2024-09-14

### Improvements

- **Faster data loading for related records:** When the system fetches linked records (e.g. a product's location, a handling unit's article), it now groups and batches those database lookups instead of running them one by one. This reduces the number of queries sent to the database and speeds up screen loading times noticeably when many related items are displayed.

- **More reliable sorting on list screens:** Sorting warehouses, warehouse workers, roles, user roles, and permissions without specifying a sort order no longer causes an error — the lists now load correctly in all cases.

- **Improved server stability and connection management:** The database connection pool has been tuned to better handle high concurrency, and connections are now cleanly released when the server shuts down. This reduces the risk of "too many connections" errors under heavy load.

- **Faster infrastructure health checks:** The load balancer now checks server health every 10 seconds (previously 60 seconds), so any unhealthy instance is detected and removed from rotation much more quickly, improving overall availability.

### Fixes

- **Sorting on auth-related lists no longer crashes when no sort order is provided:** Querying lists of roles, permissions, warehouses, and related entities without an explicit sort now works as expected instead of returning an error.

- **Linked record lookups now correctly return results:** A missing `await` in the resolution of linked (child) records was causing some related data to not appear. This is now corrected.

## [2.5.1] - 2024-09-07

_Internal technical maintenance, no visible functional impact._

## [2.5.0] - 2024-09-07

_Internal technical maintenance, no visible functional impact._

## [2.4.0] - 2024-09-07

### New features

- **Barcode image generation on the fly:** Cella can now generate barcode images (SVG format) directly from the server for any supported barcode type and value. Appearance options such as size, colours, and text position can be customised per request. This makes it easier to display or print barcodes without needing an external tool.

- **Clearer error messages when browsing lists:** When a database problem occurs while loading, counting, or sorting a list of records, Cella now returns a structured, descriptive error message instead of a generic failure. Users and support teams will see meaningful details about what went wrong and, where possible, a hint on how to resolve it.

### Improvements

- **Faster API responses:** Response encoding has been switched to a higher-performance library, reducing the time it takes to receive data when querying large lists or complex records.

- **More robust list filtering:** Filtering or sorting on custom or computed fields no longer causes unexpected errors; the system now handles these cases gracefully.

### Fixes

- **List queries no longer fail when sorting or filtering on relationship fields:** A crash that could occur when applying filters or sort criteria involving certain linked data fields has been resolved. Affected list screens will now load correctly.

- **Reliable data reading under load:** A database routing issue affecting read operations in list resolvers has been corrected, improving stability when multiple users query the system simultaneously.

## [2.3.2] - 2024-08-22

### Fixes

- **Real-time feeds now stay reliable when the database replica is lagging.** The live update streams for record history, document printings, and notifications were previously reading from a read replica, which could lag behind the primary database and cause missed or delayed events. They now read directly from the primary database, ensuring subscribers always receive up-to-date information immediately.

## [2.3.1] - 2024-08-20

### Fixes

- Notifications triggered by webhooks are now correctly delivered; a data-formatting error that caused notification processing to fail has been resolved.

## [2.3.0] - 2024-08-19

### Fixes

- **Cubing – containers without a weight limit no longer cause errors.** When a container had no maximum weight configured, the cubing engine would fail or behave unpredictably. It now treats such containers as having no weight restriction, so packing calculations complete correctly.
- **Cubing – compacting step now handles containers missing weight limits.** The same missing-weight-limit issue could also occur during the compacting phase; this has been resolved.

## [2.2.0] - 2024-08-12

### Fixes

- **Clearer error messages when a save operation fails:** When creating or updating a record triggers a database conflict or constraint violation, the error message shown to users is now better formatted and easier to read.
- **Article price duplicate detection improved:** The uniqueness check for article prices now also takes into account the quantity, status, and currency fields. This prevents cases where two distinct price records with different quantities, statuses, or currencies could be incorrectly blocked as duplicates — or, conversely, where true duplicates were not detected.
- **Duplicate-record rules now handle empty (null) values correctly:** Across all major record types (articles, barcodes, orders, deliveries, purchase orders, carriers, handling units, rules, and many more), the system now correctly treats records with missing optional fields as distinct when checking for duplicates. Previously, records containing blank optional fields could be incorrectly identified as duplicates of one another, preventing valid data entry.
- **User-role assignment no longer incorrectly blocks valid combinations:** The rule preventing the same role from being assigned twice to a user has been consolidated and corrected, avoiding false duplicate errors when assigning roles to warehouse workers or integrator users.

## [2.1.0] - 2024-08-11

### Improvements

- The global search ("search all fields") on records such as deliveries and orders now correctly excludes fields like `address_1`, VAT code, EORI code, and INSEE code from free-text matching, reducing irrelevant results and preventing unexpected query errors.
- Searching across related records (e.g. finding deliveries by order information, or orders by third-party details) is now more reliable: the system stops traversing relationships at the right depth, preventing overly broad or incorrect search results.
- Database migration scripts have been consolidated into a cleaner, unified structure, making future upgrades and new warehouse provisioning faster and more dependable.

