# Release Notes — Cella Front

<!-- CHANGELOG:START -->

## [1.44.0] - 2026-06-12

### New features

- **Gate Entry kiosk (mobile):** A new self-service kiosk flow is available on the mobile app, accessible from the home screen. Truck drivers can complete their check-in entirely autonomously, step by step:
  1. Choose the interface language (French, English, German).
  2. Search for an existing appointment by reference number, truck plate, or QR-code scan — or request an ad-hoc (unscheduled) entry.
  3. Fill in driver and vehicle details (driver name, company, phone, truck/trailer plates, seal number, estimated weight). For ad-hoc entries, a carrier and a slot duration are also selected.
  4. Read and accept the mandatory safety documents (images served from a warehouse business rule). Each document group must be explicitly checked before proceeding.
  5. Sign on screen with a touch-friendly digital signature pad.
  6. Wait on a live status screen while the security agent reviews the request (the screen polls every few seconds and displays how long the wait has been).
  7. See the final result: **approved** (with dock assignment) or **refused** (with the stated reason and a contact-security button).

- **Gate Validation dashboard (web):** Security agents now have a dedicated section under "Truck Management → Gate Validation". It lists all truck arrivals pending review, colour-coded by punctuality (on-time, early, late, very late). Agents can open any entry to see the full driver/vehicle details, the accepted safety documents and the digital signature, then either **approve** (mark as on-site and assign a dock) or **refuse** with a reason from a predefined list. Refusing offers the choice of cancelling the appointment outright or resetting it so the driver can restart the kiosk process.

- **Mail Templates (web):** A new "Mail Templates" section is available in the Administration menu (subject to permissions). Users can list, create, edit and delete email templates. Each template can be written directly in the editor or imported from an HTML/text file. A live side-by-side preview shows how the template will render in an email client.

- **CellaBot AI assistant (web):** When enabled for your warehouse and your user account, a floating chat button appears in the bottom-right corner of every web page. Clicking it opens a chat panel where you can ask questions about what you are currently viewing (lists, records, filters, selections). CellaBot is context-aware: it automatically knows which screen and which record are on screen. Conversations are cleared on logout. The feature is off unless explicitly activated by your system administrator.

### Improvements

- **Appointment schedule (web):** In the daily (dock) view, each dock column now has a guaranteed minimum width. When there are many docks, the schedule table scrolls horizontally instead of compressing the columns to an unusable size.

- **Delivery detail page (web):** Delivery line rows are now sorted by creation date by default, making the order of lines more predictable. Status-based button visibility (edit, cancel, delete) now reads live configuration values from the system settings, so it stays correct even when tenants customise their status codes.

- **List views (web) – filter persistence fix:** Switching between the standard search filters and the advanced filters no longer silently discards the other group's saved filter options. Both filter systems are now preserved together when saving user settings.

- **Login page (web):** The username field text is now always displayed in black, ensuring it remains readable on all themes and browsers.

## [1.43.4] - 2026-06-02

### Improvements

- **Smarter search filters across all record types.** Advanced-filter fields in list views (articles, orders, deliveries, handling units, rounds, movements, locations, and many more) now use the most appropriate filter widget for each field: text-search boxes appear where typing a name or code is natural, dropdown selectors appear for status/category fields, yes/no toggles appear for boolean fields, and number inputs appear for numeric fields. Previously these fields either had no filter widget or showed the wrong type, making it harder to narrow down records.

- **Auto-complete look-up fields now show results in alphabetical order.** Whenever you type in a linked-record field (e.g. choosing an article, a stock owner, a carrier, a location, etc.), the suggestions are now sorted A → Z, making it easier to find the right record.

- **Date-range filters now offer "Today" and "Tomorrow" quick-select shortcuts.** On any screen that has a date-range filter, you can click a preset button to instantly fill in today's or tomorrow's full-day range instead of picking dates manually.

- **Linked-record selectors switched from fixed dropdown lists to searchable auto-complete fields.** Across all modules (appointments, orders, deliveries, equipment, rounds, purchase orders, etc.), fields that link to another record now let you type and search rather than scrolling through a static list. This is particularly useful for tables with many records.

- **Round priority field now filters by category.** When selecting a round on shipping-unit screens, the list is pre-filtered to show only rounds of the relevant priority category, reducing irrelevant choices.

- **Round list: priority, blocking, and number fields use correctly typed filters.** The priority field now provides a numeric input, the blocking/weight-optimisation toggles now show yes/no filters, and the number of lines/articles fields accept numeric input, matching the nature of each value.

- **Config and Parameter screens: "scope" and "system" fields now use the correct filter widgets** (dropdown and yes/no toggle respectively) instead of plain text boxes.

## [1.43.3] - 2026-05-28

### New features

- **Pre-assigned load page – carrier & shipping date info:** When you select a load on the Pre-assigned Load page, the carrier name and expected shipping date for that load are now displayed directly next to the load selector, so you no longer have to navigate away to check those details.
- **Pre-assigned load page – estimated load summary:** When confirming deliveries in the pre-assigned load workflow, a new summary section now shows the total estimated number of boxes, pallets, and load metres across all selected deliveries, giving you an at-a-glance capacity overview before you confirm.

### Improvements

- **Navigation – "Business Management" menu moved earlier:** The Business Management section (Credits, Customer Orders, Payments) now appears higher up in the side menu, before Stock Management, reflecting a more logical grouping.
- **Navigation – "Truck Management" menu reorganised:** The Truck Management section now includes Pre-assigned Loads (previously listed under Preparation) alongside Loads, Appointments, and the Schedule. The order of items within the section has also been updated (Pre-assigned Loads → Loads → Appointments → Schedule).
- **Appointments breadcrumb corrected:** The breadcrumb trail for the Appointments section now correctly reads "Truck Management" instead of "Business Management".
- **Stock Movements search simplified:** Several fields in the Stock Movements list (including location, article, and origin/destination references) no longer show individual search/filter boxes, reducing clutter and making the search bar easier to use.

### Fixes

- **Pre-assigned load selection panel:** The action bar above the delivery list no longer has a fixed maximum height, preventing buttons or controls from being cut off on certain screen sizes.

## [1.43.2] - 2026-05-26

### Improvements

- **Search filters now available across all screens:** Text fields, date fields, numeric fields, boolean toggles and dropdown selectors are now properly activated as search/filter controls throughout the application. This affects virtually every list view — articles, barcodes, orders, deliveries, cycle counts, equipment, carriers, appointments, locations, and many more — where filtering fields that previously had no search control are now searchable with the appropriate input type (text box, date range picker, number field, yes/no toggle, or dropdown).

- **Corrected filter types on several fields:** A number of fields that were assigned the wrong filter type (e.g. a free-text box on a numeric or date field, or vice versa) have been corrected. Affected areas include delivery lines, customer orders, credit lines, delivery models and others. Filters on these fields will now behave as expected.

- **Appointment detail view simplified:** The Appointment detail page no longer shows a large block of entity address and contact fields that are not relevant in this context. The view is cleaner and easier to navigate.

- **Dark theme and global style enhancements:** Visual improvements have been applied to the interface, including an expanded dark theme and updated global styles, resulting in a more consistent look across the application.

- **Location extras edit form improved:** Minor layout and behaviour improvements to the form used to edit location extra fields.

- **Appointment scheduling page updated:** The appointment scheduling screen has been adjusted to improve usability and layout.

## [1.43.1] - 2026-05-25

### New features

- **Appointments module**: A new Appointments section is available in the web interface, allowing users to create, edit, view and manage appointments and their lines, including a scheduling view.
- **Goods-In lines**: A dedicated Goods-In Lines detail screen is now available, providing better visibility of inbound line data.
- **Delivery extras**: Users can now add, edit and remove extra information records directly on a delivery detail page.
- **Load extras**: Users can now add, edit and remove extra information records directly on a load detail page.
- **Location extras**: Users can now add and edit extra information records on a location detail page.
- **Attached documents panel**: A reusable document attachment list (download and delete) is now available on deliveries, loads, purchase orders and appointments.
- **Advised inventory on pick**: When a picker enters a quantity that empties a location, the system now prompts them to confirm whether the location is empty. If it is not empty, a cycle-count is automatically created for that location to trigger a stock verification.
- **Carrier box scan**: Handling units can now be found by scanning either their own barcode or a carrier box label in the Pick, Pack, Pick-and-Pack, Box Checking, Palletization, and Round Picking workflows.

### Improvements

- **Round selection order**: Rounds are now sorted by name as a tie-breaker after priority and delivery date, making the list more predictable.
- **Equipment handling unit validation**: The system now verifies that a scanned handling unit is of the correct type (equipment) before accepting it during picking, preventing erroneous associations.
- **HU model selection (Pack)**: Equipment-type handling unit models are now excluded from the model selection list during packing, reducing the risk of choosing the wrong container type.
- **Quantity entry – back navigation**: Going back from the quantity entry step now reliably returns to the correct previous step across all picking and packing workflows.
- **Change-content button**: The "Change content" button in the HU content selection screen is now controlled by a permission (`mobile_button_change-content`), so it can be hidden for users who should not perform that action.
- **Cycle count – features review**: The features review screen now automatically opens in edit mode when any feature value is missing, avoiding user confusion when required data has not yet been entered.
- **Cycle count – date feature handling**: Date-type features are now correctly identified and formatted, preventing numeric strings from being misinterpreted as dates.
- **Language/locale**: The mobile app layout no longer crashes when a user has no language preference saved; it falls back to the browser locale instead.
- **User settings reset**: Resetting column settings for a screen now correctly identifies all relevant settings, including those stored under sub-paths.
- **Date picker**: The date picker now supports German locale, and additional options (disabled dates, disabled times, custom time picker) are available throughout the application.
- **Table column reordering**: Dragging columns to reorder them in filter panels no longer loses sort configuration on those columns.
- **Scan form fields**: Forms across the mobile picking, packing, and stock management workflows now support sharing a single form instance, improving consistency when multiple inputs are managed together.

### Fixes

- **Pack workflow – box closure**: Removed a redundant confirmation step when closing a partially-filled box; the flow now proceeds directly to the review/weight step without a double prompt.
- **Pick workflow – location scan error**: Scanning an incorrect location now correctly resets the scanned value in addition to displaying an error message, preventing the workflow from getting stuck.
- **Mobile layout – missing settings crash**: Fixed a crash that occurred when a warehouse worker's settings record existed but contained no language configuration.
- **Cycle count page – "N/A" default for features**: The default feature code "N/A" is no longer incorrectly pre-filled when the article has a feature type and a new handling unit content is being created; the field is left blank so the user can enter the correct value.

## [1.43.0] - 2026-03-18

### New features

- **German language support**: The interface is now available in German (Deutsch) on both the desktop and mobile applications. Users can select German from the language settings.
- **French locale code updated**: The French language option now uses the `fr-FR` locale code. Existing French preferences are migrated automatically; no action is required from users.
- **Environment label in the header**: When using a development, staging, or pre-production environment, a coloured badge (DEV / STAGING / PRE-PROD) is now displayed in the top navigation bar so users can immediately see which environment they are working in.
- **Document attachments**: Users can now upload and attach documents (any file type, up to 20 MB) to Loads and Deliveries directly from the relevant record pages. Uploaded files can be assigned a category and a description, and can later be included when printing.
- **Pre-assigned loads**: A new "Pre-assigned load" section is available under Preparation Management in the side menu, allowing users to manage loads that have been pre-assigned to deliveries.
- **Assign deliveries to a load**: From the Load detail page, users can now assign deliveries to a load via a dedicated modal.
- **Improved print modal**: A new print dialog allows users to select both standard documents and attached files at the same time, send them to a printer or open them in the browser, and optionally e-mail them to one or more recipients.
- **Version number on the About page**: The current application version is now displayed at the bottom of the About page.
- **Responsive navigation menu**: On smaller screens (tablets and compact desktops), the side navigation menu is now accessible via a hamburger button in the header and opens as a slide-in drawer, making the application easier to use on smaller displays.
- **Additional load fields**: Load records now expose new fields including truck licence plate, trailer licence plates, driver name, driver licence and ID numbers, MRN number, external name, references 1–3, expected/actual arrival, departure and shipping dates, and a dock location.
- **Additional delivery fields**: Delivery records now display the pre-assigned load, external name, and estimated quantities (boxes, pallets, load metres).

### Improvements

- **Sticky table headers**: Column headers in all data tables now remain visible when scrolling through long lists, making it easier to identify which column you are reading.
- **Language consistency**: Drop-down values, date pickers, and translated labels throughout the application now correctly reflect the selected language (including French and the new German option) in all screens and mobile workflows.
- **Responsive layout**: Page content areas adapt better to narrower screens, with improved margins and scrolling behaviour on tablets and smaller desktops.
- **Sticky action buttons on narrow screens**: Action buttons that float on the right side of the page now reposition to the top of the content area on smaller screens instead of overlapping content.
- **Advanced filters propagated to auto-complete fields**: Search fields that use auto-complete now respect advanced filter criteria, returning more relevant suggestions.
- **Search field for single-value selection**: Auto-complete inputs can now be configured to allow only a single selection where appropriate, rather than always showing a multi-select field.

### Fixes

- **SSO login errors on non-SSO instances**: Attempting to reach the SSO configuration when no SSO secret is configured no longer causes an error; the standard login flow is used instead.
- **Language settings migration**: Users whose language was stored as the old `fr` code are automatically upgraded to `fr-FR` on next login, preventing missing translations.
- **Advanced filters not refreshing**: Changing advanced filter criteria in list views now correctly triggers a data refresh without requiring a page reload.
- **Scroll position reset on navigation**: Navigating between pages now reliably returns the content area to the top of the page.

## [1.42.0] - 2026-03-04

### New features

- **Equipment Position Release (mobile):** A new workflow is available in the Preparation menu for mobile users. Operators can scan a round or equipment, select a position, scan a destination handling unit, and validate the release of items from an equipment position to a box or pallet.

- **"Declare Missing Quantity" button (mobile – Pick & Pick-and-Pack):** During picking and pick-and-pack operations, authorised users now see a "Missing Quantity" button at the scanning step. Pressing it opens a form to enter and confirm a missing quantity without interrupting the rest of the round.

- **"Declare Missing Quantity" action (web – Box line detail):** On the box detail page, a "missing quantity" action button now appears on each box line that is in progress and still has quantities to pick, allowing office users to declare shortages directly from the back-office.

- **Wave Picking entry point (mobile):** A "Wave Picking" option is now available in the Preparation menu for users who have the corresponding permission.

- **Recommended Cycle Counts – dedicated detail page (web):** Recommended cycle counts now have their own detail page, accessible from the Recommended Cycle Counts list.

- **Cycle Count creation – "Number of Days" and "Stock Mini" types now fully available (web):** The creation form for cycle counts now supports the "Nb days" and "Stock Mini" types, including the associated fields (number of days, threshold quantity). The "Empty location" type is also properly handled.

- **Bulk location creation – additional fields (web):** When creating locations in bulk (from a block or the Locations section), operators can now set Handling Unit Management, Stock Status, Location Group, and physical dimensions (length, width, height, max weight) for the locations being created.

### Improvements

- **Pick & Pick-and-Pack – total quantity counter corrected (mobile):** The picked-quantity counter in the header now shows the actual total quantity to be processed for the round, instead of the formerly used article count.

- **Similar locations – empty-location suggestions now use their own result-count parameters (mobile):** When the system proposes empty locations, it now reads a dedicated configuration for the maximum number of results, separate from the configuration used for similar-stocked locations.

- **Similar locations – handling unit category filter added (mobile):** Content movement and HU movement flows now pass the handling unit category to the location-suggestion engine, improving the relevance of proposed locations.

- **Customer Order detail – deliveries list always shown (web):** The linked deliveries list on a customer order is now always displayed (filtered by the order), removing the previous dependency on a pre-loaded list of IDs.

- **Cycle Count detail – "Errors" tab hidden for Recommended type (web):** The Cycle Count Errors section no longer appears on recommended cycle counts, where it is not applicable.

- **Cycle Count detail – movement section hidden for Recommended type before completion (web):** The movements sub-list is now correctly hidden for recommended cycle counts at "Created" status.

- **Cycle Count form – model field removed from view (web):** The "Model" field is no longer shown when creating a cycle count; the "Normal" model is set automatically.

- **Cycle Counts breadcrumb corrected (web):** The breadcrumb for cycle counts now reads "Stock Management" instead of "Configuration".

- **Handling Unit Content list – location column visible by default (web):** The location column in the Handling Unit Content list is now displayed by default instead of being hidden.

- **Movement-to-process page – header display improvements (mobile):** The reservation check mark is only shown when a reservation value is actually present; the final location name correctly falls back to the scanned location when no pre-defined final location exists; the final handling unit label adapts correctly depending on whether the location requires HU management.

- **Translations now also load global ("*" type) entries (web & mobile):** Both the web and mobile interfaces now fetch translations tagged as global in addition to their own type, ensuring shared labels are always available.

- **Reception – stock status lookup corrected (mobile):** The stock status passed to the location-suggestion component during reception now uses the correct value, fixing cases where an incorrect status could be sent.

### Fixes

- **Pick – location force-scan flag set correctly on unexpected scan (mobile):** When an unexpected barcode is scanned on the location-by-level selection step, the system now correctly sets the force-location flag, preventing inconsistent navigation.

- **Pick – round position transmitted on auto-validation (mobile):** The current round position is now included in the validation request, ensuring the back-end correctly processes picks that require position tracking.

- **Bulk location creation now goes through the back-end function (web):** Location bulk creation (from both the block page and the standalone location creation form) now calls the `bulk_create_locations` back-end function, enabling proper validation and error reporting instead of a direct database write.

## [1.41.1] - 2026-02-19

### New features

- **Pack (packing) workflow – new mobile screen.** A dedicated packing process is now available in the mobile app (accessible from the Preparation Management menu). Operators can scan a round, handling unit or position, scan article barcodes, enter quantities, select a packaging model and weight, and validate the box closure step by step. The workflow handles position-based packing, forced box closure with confirmation, and automatic round completion detection.

- **Reception – stock status and quantity on a single screen.** The stock-status selection and the quantity entry have been merged into one combined step during reception. Operators no longer need to navigate through two separate screens to capture both pieces of information.

- **Handling-unit movement – configurable location scan.** A new warehouse parameter (`FORCE_LOCATION_SCAN`) controls whether operators must scan the origin location before scanning the handling unit. When the parameter is off, the operator scans the handling unit directly and the system automatically resolves the originating location.

- **Pick workflow – equipment position displayed in header.** When position checking is active, the expected position number is now shown in the information header during picking, giving the operator immediate visibility of where to go.

- **Manual allocation – new management screen.** A Manual Allocation screen is now available in the web interface, allowing warehouse supervisors to manually assign stock to orders.

- **Customer order lines – dedicated edit form.** Customer order lines can now be edited through a dedicated form with the appropriate fields, replacing the previous limited editing experience.

- **Handling unit contents – inline edit modal.** Stock contents of a handling unit can now be edited directly from the handling unit contents list via a pop-up form, without leaving the page.

### Improvements

- **Round list sorted by priority and delivery date.** When an operator selects a round in the pick or pick-and-pack workflows, rounds are now returned pre-sorted by assigned user, then by priority (highest first), then by expected delivery date. The previous client-side alphabetical sort has been removed.

- **Supplier article code shown in more workflows.** The supplier article code displayed in the mobile header is now also populated during the **pick** and **pack** processes, in addition to the existing workflows.

- **Reception stock status now correctly displayed.** The stock status label shown in the reception header and stored for validation now uses the correct text value, fixing cases where the status appeared blank or incorrect.

- **Pick and pick-and-pack – round count no longer stored inside step data.** The number of available rounds is now tracked separately from the step data, avoiding situations where the round count could become stale after successive loops.

- **Pick – equipment handling unit correctly propagated.** After a pick cycle, the equipment handling unit returned by the back-end is now correctly passed to the next step, preventing mismatches when an operator picks across multiple rounds.

- **Pick-and-pack – palletization logic consolidated.** The conditions for enabling or disabling palletization for the carrier and the packaging model are now evaluated in a single, cleaner block, correcting edge cases where the palletization flag was not set when `forcePickingCheck` was active.

- **Mobile header – supplier article code visible earlier.** The supplier article code now appears as soon as article data is available, including in pick scenarios where no article has been scanned yet (the expected article from the round line is used).

- **Round and customer order models – enriched data.** Additional fields (including article details and carrier shipping mode) are fetched when loading rounds and customer orders, making more information available throughout the preparation workflows without extra requests.

- **Warehouse worker model – extended display.** The warehouse worker list in the web interface now exposes additional fields.

### Fixes

- **Pick – location forced correctly after choosing an alternative location.** When an operator used the "change location" shortcut from the article scan screen, the system was not consistently flagging that the next location scan must be manual. This is now handled reliably in both the pick and pick-and-pack workflows.

- **Pick – handling unit type check for equipment.** The scan handling-unit step now correctly distinguishes whether the scanned unit belongs to the current round's equipment, preventing an existing equipment unit from being treated as a new one to create.

- **HU movement – handling unit without a location no longer causes a crash.** If the scanned handling unit has no recorded location, a clear error message is shown instead of an unhandled error.

- **HU movement – back button hidden when location scan is not required.** When `FORCE_LOCATION_SCAN` is off, the back button on the handling unit scan step is correctly hidden since there is no previous location step to return to.

- **Reception – quantity and stock status saved to the correct step.** References to the quantity and stock-status data were pointing to the wrong workflow step (step 80 instead of step 70), causing the values to be missing during reception validation. This is now corrected.

- **Auto-validate pick – trigger corrected for non-position-checked rounds.** The auto-validation form was not triggered in some configurations where no position check step existed. The condition now correctly fires the validation when step 70 data is present without a position-check step.

## [1.41.0] - 2026-01-07

### New features

- **Pick process (mobile):** A dedicated "Pick" workflow is now available on handheld devices, covering the full picking sequence: select a round, select equipment, scan location, scan handling unit, scan article barcode, scan serial/batch features, enter quantity, and validate. The round is automatically assigned to the operator on first selection, and the system guides pickers step by step according to the round's advised addresses.

- **Movement-to-process (mobile):** A new "Movement to process" screen is available on handheld devices, letting warehouse operators process stock movements directly from a guided mobile workflow (select movement, scan/choose article and content, choose destination location, enter quantity, and validate).

- **Article translations (web):** Articles now have a dedicated translations tab in the back-office. Users can add, view, and edit translations for an article's descriptive fields directly from the article detail page.

- **Manual movement creation (web):** The stock movement creation form in the back-office has been significantly expanded, giving supervisors access to a more complete set of fields and validation options when creating movements manually.

- **Round management modals (web):** Three new action dialogs are available on the Rounds pages: assign rounds to a preparation team, edit round priority, and trigger/confirm a round calculation directly from the interface without leaving the page.

- **Assignment management modal (web):** A new generic assignment modal is available across relevant modules, making it easier to assign records to users or groups from any list or detail view.

- **Supplier article code displayed during mobile operations:** The supplier's internal article reference (generic article comment) now appears in the information header on mobile screens during picking, reception, cycle counts, stock movements, box preparation, and other warehouse operations, so operators can cross-check against supplier labels.

- **Smart location suggestions on mobile (v2):** Improved "similar locations" and "empty locations" panels on mobile now support an optional block filter, letting operators narrow suggested putaway or pick locations to a specific warehouse block.

### Improvements

- **Highlighted fields on mobile detail screens:** Individual data fields in mobile information panels can now be displayed in **bold red** to draw the operator's attention to critical values (e.g., quantities or statuses that require special care).

- **Quantity entry – auto-validate when only 1 unit is available:** When the available quantity for a movement is exactly 1 and the "auto-validate" option is active, the quantity step is skipped automatically, reducing unnecessary taps for operators.

- **Pick-and-Pack – article and location check improvements:** Article and location validation steps in the Pick-and-Pack workflow now better handle multi-location rounds and provide clearer error messages when the scanned item does not match the expected one.

- **Pick-and-Pack – equipment selection now shows pending round count:** The equipment dropdown during round selection shows the number of rounds pending for each piece of equipment, helping operators choose the most appropriate cart or pallet.

- **Session state persistence for new workflows:** The Pick, Pack, and Movement-to-process mobile workflows now survive page refreshes and browser restarts — operators can resume where they left off without losing progress.

- **Cumulated stock page (web):** The cumulated stock view has been updated with additional filtering and display options.

- **Deliveries – manual allocation modals:** The manual allocation dialogs for deliveries and boxes have been extended with additional fields and logic to support more allocation scenarios.

### Fixes

- **Pick-and-Pack – location scan with no matching content:** Scanning a location that contains no stock for the expected article now correctly shows an error message instead of silently advancing to the next step.

- **Reception – feature checks:** The feature-scanning step during reception now correctly validates scanned values and shows a clearer error when the combination of features does not match any existing stock.

- **Quantity entry – initial value calculation:** The initial quantity shown in the entry field is now calculated correctly when both "initialValueType" and "autoValidate" options are combined, preventing the wrong default value from being pre-filled.

## [1.40.1] - 2025-12-05

### New features

- **Mobile – On-screen notification positioning:** Alert messages on mobile devices now appear at the bottom of the screen and automatically move up when the virtual keyboard is open, so they are never hidden behind it.
- **Mobile reception – Configurable default quantity:** A new warehouse parameter (`RECEPTION_DEFAULT_QUANTITY`) lets administrators pre-fill the quantity field during goods reception (e.g. default to 1 or to the maximum expected quantity), reducing manual entry for operators.
- **Rounds – Start a round from its detail page:** A "Start round" button is now available on a round's detail page when the round is in *Estimated* status. Clicking it transitions the round to *Started* directly from the interface.

### Improvements

- **Session timeout warning:** The countdown warning before automatic logout is now more reliable. Timers are properly cleared when you log out or log back in, preventing phantom notifications or duplicate countdowns in both the web and mobile interfaces.
- **Loading screen behaviour:** The application loading screen (spinner) is now shown only when actually needed — it no longer appears on the login or password-reset pages, and correctly waits until all settings are loaded before letting you in.
- **Detail pages – Reload button:** A refresh button (↺) has been added to record detail pages, allowing you to reload the latest data without navigating away.
- **Deleting hook configs and scheduler configs:** After deleting a hook configuration or a scheduler configuration, the list now refreshes in place instead of redirecting you to the list page.
- **Scheduler config arguments:** Argument keys are now displayed and saved correctly when they contain underscores (e.g. `my_arg` was previously shown as `arg` only).
- **Manual delivery allocation – Cancelled boxes excluded:** Boxes with a cancelled status are now automatically excluded from the manual allocation modal, so operators only see boxes that can actually be allocated.
- **Box cancellation – delivery check:** The "Cancel" action on a box (both in the list and on the detail page) is now only shown when the box is attached to a delivery, avoiding misleading options for unlinked boxes. Additional statuses (60 and 515) are also now eligible for cancellation.
- **SSO login:** Single sign-on authentication now triggers correctly whenever the session status changes, improving reliability for SSO-enabled warehouses.

### Fixes

- **Detail page spacing:** The top margin on detail sections without a group title has been slightly reduced for a cleaner layout.

## [1.40.0] - 2025-11-14

### New features

- **SSO (Single Sign-On) login support.** A new "SSO" button appears on the login page (web and mobile) when the warehouse is configured with an identity provider. Users can authenticate through their organisation's SSO instead of entering a username and password directly. Proper error messages are displayed in English and French if the SSO token is invalid, expired, or misconfigured.

- **Session expiry countdown and warning.** When a session is approaching its timeout limit, the mobile header now displays a live countdown timer. A notification is also shown in advance (based on the warehouse's configured notification window) so users know they are about to be logged out. Clicking the timer shows the remaining time.

- **Automatic session expiry logout.** Users are now automatically redirected to the login page when their session token expires, preventing silent failures or error states.

- **Quantity displayed on the location scan label (mobile Pick & Pack).** The scan-location step now shows the available quantity for the article in the suggested location directly in the input label, giving pickers immediate stock visibility without extra navigation.

- **Warehouse worker stock-owner assignments.** A new management section is available for warehouse workers, allowing administrators to view, create, and edit the stock owners assigned to each worker.

- **Article extras management.** Articles now have an "Extras" sub-section where supplementary attributes can be listed, added, and edited directly from the article detail page.

- **Configurable round-check on content and HU movements.** A new parameter (`MOVEMENT_CHECK_ROUND`) controls whether the system warns operators about planned rounds when they select a picking location during a content or handling-unit movement. Previously this check was always active; it can now be turned on or off per warehouse configuration.

---

### Improvements

- **Pick & Pack workflow reliability.** The entire Pick & Pack process now keeps its state in the application's in-memory store rather than in browser local storage. This removes a class of issues where stale or inconsistent data in local storage caused unexpected behaviour during picking, back-navigation, or round progression.

- **Feature scanning accuracy.** When scanning a serial/batch feature code during picking, the system now cross-checks the scanned value against the exact handling-unit content proposed by the round, preventing false positives from other stock with the same article.

- **Location change during picking.** When an operator selects an alternative picking location, the update is now handled more robustly. An option (`dontAskBeforeLocationChange`) allows the confirmation dialog to be skipped in workflows where the change is always expected.

- **Similar locations filter now respects reservation.** The "similar locations" panel during picking only shows locations whose reservation matches the delivery line, avoiding misleading suggestions.

- **Quantity entry: flexible initial value.** The quantity entry screen can now be pre-filled with either 1 or the full available quantity depending on workflow context, reducing manual input in common cases.

- **Round selection: feature code details richer.** The round selection query now retrieves date-type and unique flags for feature codes, ensuring downstream feature-scanning steps have all the information they need without extra round-trips.

- **Reception goods-in selection simplified.** The goods-in selection step no longer triggers an unnecessary round-status update function call, making the step faster and less error-prone.

- **Notification and alert display duration is now configurable.** Success, error, info, and warning messages can be shown for a custom duration where needed (for example, the session timeout warning stays visible for 10 seconds).

- **Web list filters refactored for better usability.** Filter panels across list pages have been consolidated, making filter behaviour more consistent throughout the back-office interface.

- **Delivery line edit page enriched.** The delivery line edit form now exposes additional fields (carrier shipping mode, stock owner) that were previously unavailable.

- **Customer orders list and detail pages improved.** The customer orders index and detail pages have been updated with additional data and display improvements.

---

### Fixes

- **Back-navigation step counter corrected.** Going back through multi-step RF (radio-frequency) workflows now restores the correct previous step number in all cases, fixing an off-by-one error that could send the user to the wrong step.

- **Pick & Pack round finish after last item.** After successfully packing the last item of a round, the workflow now correctly resets to the round-selection step instead of getting stuck.

- **HU movement location selector now respects round-check setting.** The handling-unit movement workflow correctly reads the `MOVEMENT_CHECK_ROUND` parameter; previously it always performed the check regardless of configuration.

- **Article model field corrections.** Several article-related data fields were mapped incorrectly, causing display issues on article detail and edit pages; these have been corrected.

- **Side menu scroll behaviour fix.** Removed a spurious empty menu item that was previously added as a workaround for scroll behaviour, cleaning up the navigation menu display.

- **Login page no longer crashes when SSO configuration is absent.** If no SSO provider is configured for the warehouse the SSO button is simply not shown, and no error is thrown on page load.

## [1.39.2] - 2025-10-06

### Improvements

- **Reception workflow – state management overhaul.** The entire goods-receipt process (standard reception and return reception) now stores its in-progress data in a central, application-level state instead of individual browser-storage entries. This makes the workflow more robust and consistent: step data is no longer lost or misread between navigation actions, and going back to a previous step now correctly rolls back only the relevant information.

- **Reception session automatically saved and restored.** In-progress reception and pick-and-pack sessions are now automatically saved to secure local storage in real time and reloaded when you return to the application, so an accidental page refresh or brief navigation away no longer wipes out your progress.

- **Cleaner "back" navigation during reception.** Pressing the back button at any step in the reception flow now reliably returns you to the correct previous step and discards only the data entered after that point, instead of sometimes leaving stale data from later steps.

- **Goods-in / PO scan now calls the backend more directly.** The scan of a goods-in or purchase order number during reception is now processed through a more efficient backend call, reducing the number of intermediate hops and improving response reliability.

- **Article feature-code entry added to the new reception flow.** Scanning feature codes (serial numbers, dates, etc.) during reception now uses the updated state-driven components, ensuring that entered feature data is preserved correctly when navigating between steps.

- **Header information display simplified.** The summary banner shown at the top of the reception screen (purchase order, goods-in, handling unit, article, quantity, location, etc.) now updates reactively as you progress through steps, without depending on a separate render-trigger mechanism that could occasionally show stale values.

### Fixes

- **Duplicate purchase order entries no longer appear during reception.** A data-processing issue that could cause the same purchase order to be listed more than once when scanning a goods-in linked to multiple round lines has been corrected.

- **Resetting or leaving the reception page now fully clears session data.** Using the reset button or navigating away from the reception screen now correctly wipes the in-progress session for that workflow, preventing leftover data from appearing the next time you open the page.

## [1.39.1] - 2025-09-26

### New features

- **Stock initialisation on mobile (Init Stock):** A new "Init Stock" workflow is now available in the mobile Stock Management menu. Operators can scan a location, scan or create a handling unit, select a handling unit model, scan an article EAN barcode, choose the stock owner, enter product features (including date-type features), enter a quantity, select a stock status, optionally record a reservation reference, and finally validate the operation. A comment can be added at any point during the process via a dedicated button. The workflow guides the user step by step and retains all entries until final validation.

### Improvements

- **Column settings reset per screen:** In the web interface, users can now reset column display preferences for the current screen only, without affecting settings on other screens. A new button "Reset settings (this screen only)" is available in the user settings panel.
- **Column show/hide and ordering (web tables):** The column customisation panel has been simplified. Showing/hiding and reordering columns now works more reliably, and saved preferences are restored more accurately when returning to a list screen.
- **Quantity auto-filled from scanned features:** When serialised (unique) features have been scanned for an article, the quantity field is automatically pre-filled with the number of scanned serial numbers, reducing manual entry errors.
- **Location pre-selected when handling-unit management is disabled:** If a storage location does not require separate handling-unit management, the handling unit is automatically set to the location name, skipping a manual scan step.

### Fixes

- **Pick-and-pack workflow step navigation:** A typo in an internal step key (`cuurrentStep` → `currentStep`) caused the pick-and-pack process to navigate to the wrong step when closing a round. This is now corrected and round closure behaves as expected.
- **Optional scan fields no longer block progress:** Scan fields that are not mandatory (e.g. reservation entry) no longer prevent the user from continuing when left empty.
- **Sticky action buttons correctly positioned in web lists:** The action buttons (export, etc.) on list pages were misaligned. They are now correctly anchored to the top-right of the table area.

## [1.39.0] - 2025-09-15

### New features

- **Manual allocation of boxes into rounds (new modal):** On both the Boxes list page and the Delivery detail page, you can now select one or more boxes (that have not yet been started) and trigger a manual round allocation. A new dialog lets you optionally restrict the allocation to specific equipment; it also shows the number of selected boxes, their total volume and their total theoretical weight before you confirm.

- **Carrier and shipping mode visible on boxes:** The box info screen on the mobile terminal now displays the carrier name and the shipping mode alongside the other box details.

- **Delivery progress bar reworked:** The circular progress indicator on a delivery now reflects the actual delivery workflow stages (from "update in progress" through to "dispatched"), rather than relying on an extra data query. A completed/dispatched delivery is shown in green; a cancelled one in red.

- **New delivery statuses available:** Two additional statuses ("Pre-checked" and "To be palletized") are now recognised throughout the interface, enabling finer-grained progress tracking for deliveries.

### Improvements

- **Round list: more filtering and sorting options.** The warehouse code column is now visible in the list. The "expected date" column can now be filtered using a calendar date range. The "name" column is now sortable and searchable.

- **Box edit button now available up to "Loaded" status:** The edit action on a box (both on the list and on the detail page) remains available until the box reaches "Loaded" status, rather than being blocked at "Load in progress".

- **Delivery edit button conditionally shown:** The "Edit" button on a delivery detail page is now only displayed when the delivery has not yet been loaded, preventing accidental edits on advanced deliveries.

- **Delivery list edit action aligned with delivery edit page:** The edit link in the deliveries list is now hidden once a delivery reaches "Loaded" status, consistent with the detail page.

- **Carrier name visible on deliveries and boxes (back-office):** The carrier name is now shown as a column in the delivery and outbound box lists and in their detail pages, with a direct link to the carrier shipping mode record.

- **Pick-and-pack: article description always displayed.** The expected article description is now shown at all times in the pick-and-pack header, regardless of whether the article has already been confirmed.

- **Pick-and-pack: alternative locations now sorted by ascending quantity and show location category.** The "similar picking locations" table sorts locations from the lowest to the highest available quantity and replaces the generic "type" column with the location category.

- **Cycle count: location scan now validates that the scanned location matches the expected one.** If an unexpected location is scanned, an error is recorded automatically and the scan field is reset.

- **Reception workflow: HU scanning steps no longer rendered prematurely.** Handling-unit scan and validation steps now wait until the reception configuration is fully loaded before appearing, avoiding blank or erratic states.

- **Stock move operations now only clear their own workflow session.** After completing a handling-unit move, pallet move, or quantity move, only the data for that specific workflow is removed from local storage; other active workflows are left untouched.

- **Drop-down filter options are now sorted.** In list filter panels, numeric codes are sorted numerically and text codes alphabetically within each dropdown, making it easier to find a value.

- **List column headers rendered even when the list is empty.** Table columns are now defined regardless of whether any results have been returned, so the table structure is always visible.

- **Number entry field on mobile now ignores non-numeric scan input.** If a barcode scanner accidentally fires into a quantity field, non-numeric characters are silently discarded rather than causing an error.

- **Mobile pages now scroll vertically.** Long pages on the mobile interface can be scrolled up and down; only horizontal scrolling remains disabled.

- **Round creation success message now includes the calculation number.** After launching a round allocation (from the Rounds page, the Deliveries page, or the new Boxes modal), the confirmation message shows both the round calculation number and the count of rounds created.

### Fixes

- **Pick-and-pack: handling unit pre-selection now validates article/stock-owner/status/reservation.** When a handling unit is pre-selected automatically (single HU on location), the system now confirms it actually contains the expected article and matching stock attributes before accepting it, and shows a clear error if it does not.

- **Pick-and-pack: auto-validate step correctly resumes at the scan step.** After automatic pick validation, the workflow now reliably advances to the correct next scan step instead of occasionally stalling.

- **Cycle count: navigation back from article/feature check step now uses the correct step reference.** A typo that caused a crash when navigating back during a cycle count article check has been corrected.

- **Reception: goods-in "to-be-created" case handled correctly.** When a new goods-in record is pending creation during reception, the handling-unit check no longer incorrectly rejects the scanned unit.

- **Similar locations panel now closed when a location is confirmed in pick-and-pack.** The alternative-locations suggestion panel is properly hidden once the operator confirms a picking location.

- **Delivery address and third-party address edit pages now require Update permission** (instead of Create), so users with update-only rights can correctly access those pages.

- **Inbound boxes detail pages now use the correct goods-in permission** instead of the inbound-boxes permission, matching the actual access-control requirement.

- **Priority/order buttons in lists (equipment, rounds, rules, patterns, round calculation profiles) now work correctly.** A data-binding issue that could cause the "move down" button to be incorrectly disabled or show a perpetual loading spinner has been resolved across all affected pages.

## [1.38.2] - 2025-08-27

### New features

- **Mobile – password reset for warehouse workers:** Workers using the mobile interface who are required to change their password are now redirected to a dedicated password-reset screen. The form validates that the new password meets the minimum length and that both entries match before saving.

### Improvements

- **Permission checks before destructive actions:** Deleting, disabling, or re-opening a record (on both list and detail screens in the desktop interface) now verifies that the logged-in user holds the required permission before proceeding. If the permission is missing, a clear error message is displayed and the action is blocked.
- **"Search all fields" filter moved to the top of the filter panel:** The general free-text search box now appears at the very top of the filter list, making it easier to find and use quickly.

### Fixes

- **Pick-and-pack auto-validation – round number check corrected:** An error in the Pick & Pack automatic validation flow that could cause incorrect behaviour when determining whether a round should restart from the beginning has been fixed. Round numbering is now evaluated correctly.

## [1.38.1] - 2025-08-22

### Improvements

- **Handling unit content edits now record stock movements more reliably.** The movement tracking triggered when editing a handling unit content has been rewritten to use a more robust internal mechanism, reducing the risk of silent failures and improving error messages shown when something goes wrong.

- **Saved column layouts are now fully restored.** When a table has a previously saved column configuration (order, visibility, pinned columns), it is now correctly re-applied when the page loads, including pinned/fixed columns. Previously, some saved layout settings could be ignored on page load.

- **Pinning columns in table settings now works correctly.** Fixing a column via the column-filter drawer now reliably pins the selected columns, regardless of their position in the table.

- **Delivery progress bar column no longer interferes with column pinning.** The progress bar column on the Deliveries list is now properly marked as unpinned, preventing layout conflicts when saving or restoring column preferences.

### Fixes

- **Label preview (ZPL rendering) now works in all network environments.** The external label rendering service is now contacted over a secure HTTPS connection, fixing potential blocked-request errors in environments that enforce secure connections.

## [1.38.0] - 2025-08-21

### New features

- **Role-based screen permissions (web):** Administrators can now manage screen-level permissions for each role directly from the Roles section. A dedicated "Screen Permissions" page lets you grant or restrict access to every section of the web interface (wm_\* screens) and the mobile application (mobile_\* screens), separated into two clear tables. Changes require confirmation before being saved.

- **Permission-controlled navigation (web & mobile):** The side menu and all mobile home/sub-menus now show only the sections that the logged-in user's role is allowed to access. Menu items for sections the user cannot read are hidden automatically. Attempting to navigate directly to a restricted page redirects the user to the home page with an access-denied message.

- **Page titles in the browser tab (web):** Every page now displays a meaningful title in the browser tab (e.g. the record name or the section name) instead of the generic application title.

- **"Skip to next location" button during Pick & Pack (mobile):** A new "Next" action button is available on the location-scan step of Pick & Pack. Operators can skip the currently proposed location and move on to the next advised address without having to complete or cancel the current pick.

- **Session expiry detection (mobile):** The mobile app now checks the user's session on each protected page. If the session has expired, the operator sees a clear message and is automatically redirected to the login page.

- **Password-reset prompt at login (mobile):** When an account requires a password reset, the operator is redirected to the reset-password screen immediately after logging in, with an explanatory warning message.

### Improvements

- **Pick & Pack – round order reliability:** Advised addresses during Pick & Pack are now sorted by their round order directly from the server, removing occasional mis-ordering that could cause operators to be sent to the wrong location.

- **Equipment selection shows round count (mobile):** The equipment selection screen during Pick & Pack now displays, next to each equipment name, the number of rounds currently assigned to it, making it easier to choose the right equipment.

- **Round selection filtered by user (mobile):** The list of available rounds shown to an operator is now filtered to include only rounds that are unassigned or already assigned to that specific user, preventing confusion over rounds belonging to colleagues.

- **Cancel box status extended (web):** The cancellation of a handling-unit outbound now covers additional statuses (400 and 455), giving warehouse teams more flexibility when reversing outbound operations.

- **Global search field available in all list views (web):** An "All fields" search box is now present in the filter panel of every list screen, allowing users to search across all columns at once without having to select a specific field.

- **Items-per-page preference respected in lists (web):** List screens now honour the pagination preference stored in the user's settings, so the preferred number of rows per page is applied automatically on every visit.

- **"Location" field searchable as text (web):** The location field in stock content views can now be searched as free text, making it easier to filter contents by location name.

- **Mobile page header includes browser title:** Each mobile screen now correctly sets the browser/tab title to match the page being displayed.

### Fixes

- **Pick & Pack – already-visited locations no longer re-proposed:** When an operator finishes picking from a location, that handling-unit content is now excluded from subsequent proposals within the same round session. If all locations have been visited, the list resets correctly so the round can be completed.

- **Duplicate page-title tags removed (web):** Several detail sub-sections (configurations, handling-unit contents, hook configs, parameters, purchase order lines, record history, scheduler configs) were incorrectly rendering an extra browser-title tag. This has been removed, preventing duplicate or incorrect titles from appearing.

- **Login no longer stores unnecessary data in the session cookie:** The user roles and permissions are no longer written to the browser cookie on login; only the minimal user identity information is stored, improving both security and cookie size.

## [1.37.0] - 2025-08-13

### New features

- **Round Calculation Profiles** – A new "Round Calculation Profiles" section is available under Configuration. Users can list, create, view, edit, and delete profiles that control how picking rounds are calculated, including options such as mono-delivery-date rounds, replenishment creation, re-cubing, and equipment assignment.

- **Handling Unit Outbound Barcodes** – A new "Handling Unit Outbound Barcodes" section is available under Preparation Management. Users can list, create, view, edit, and delete outbound barcodes. Barcodes associated with a box are also visible and manageable directly from the box detail page.

- **Cumulated Stock view** – A new "Cumulated Stock" page is available under Stock Management, showing total quantities per article, stock owner, and stock status across all handling units.

- **Reception: smarter quantity allocation across multiple purchase-order lines** – When receiving goods against a purchase order that has several lines for the same article, the system now distributes the received quantity across lines intelligently: it fills lines with partially received quantities first, then lines that still have remaining ordered quantity, and finally lines with remaining authorised-over-quantity capacity. Stock status and stock owner are now displayed in the reception summary screen.

- **Cycle count: feature-code format validation** – When reviewing features during a cycle count, input fields that have a defined format mask now validate the entered value against that mask and display a clear error message if it does not match.

### Improvements

- **Table columns are resizable** – In all list tables on the web interface, users can drag the edge of any column header to resize it. The chosen widths are saved to user preferences and restored on the next visit.

- **Text search filters: case-sensitivity and wildcard controls** – String filter fields now show two toggle buttons ("Aa" for case-sensitive and "%" for wildcard/contains search), giving users finer control over how text searches are applied.

- **Column visibility preferences saved per page** – Column visibility, order, and fixed-column settings are now saved to user account preferences (instead of the browser's local storage), so the configuration follows the user across devices and browser sessions.

- **Scan input trims leading/trailing spaces** – Scanned or typed values in mobile scan fields now have surrounding whitespace removed automatically, reducing errors caused by accidental spaces.

- **Reception: available quantity shown correctly** – The remaining quantity available to receive is now calculated as the sum across all matching purchase-order lines, so the counter shown to the operator is always accurate even when the same article appears on multiple lines.

- **Reception: stock status displayed during reception** – The stock status (e.g. blocked, available) for the purchase-order line being received is now shown on the mobile reception screen.

- **Movements list: "Final quantity" column visible by default** – The final quantity column in the Movements list is now shown by default instead of being hidden.

- **Browser tab titles updated** – Page titles for Articles and Goods-ins now display the actual section name in the browser tab instead of the generic application title.

### Fixes

- **Reception: quantity update correctly applied to all relevant purchase-order lines** – Previously, validating a reception updated only a single purchase-order line. The system now correctly updates all affected lines when the received quantity spans more than one line.

- **Cycle count: closing a handling unit or location now uses the correct backend function** – The function called when a cycle-count operator closes a handling unit or location was updated to match the current backend API, preventing silent failures.

- **Cycle count: cancelling the quantity-overwrite confirmation modal now fully resets the scan** – After dismissing the overwrite confirmation without confirming, the scan form now resets completely, allowing the operator to scan a different item without stale data remaining.

- **Column filter drag-and-drop in table settings now works correctly** – Reordering columns in the table filter drawer by drag-and-drop no longer fails to find the correct row, making column reordering reliable again.

## [1.36.3] - 2025-07-08

### Improvements

- **Editing a handling unit content is now blocked when features are auto-counted.** If a handling unit content has one or more automatically counted features, the article field on its edit form is disabled to prevent inconsistent data.

- **Deleting a content feature now correctly records a stock movement.** When a feature is removed (either from the feature list or from the feature detail page), Cella now properly calculates the quantity change and registers the corresponding movement in the stock history, ensuring traceability is maintained.

- **Adding a content feature now correctly records a stock movement.** When a new feature is added to a handling unit content, Cella immediately registers the resulting stock movement, keeping inventory records accurate.

- **Editing a content feature no longer attempts to create an unnecessary stock movement.** Only operations that actually change quantities (add and delete) trigger a movement record; editing a feature value alone no longer does.

- **The "View" button on content features now navigates to the correct detail page**, passing along the necessary context so the page loads with full information.

### Fixes

- **Confirmation dialog wording corrected.** The delete confirmation prompt on content features now shows the generic action-confirmation message instead of a delete-specific message, which is more accurate when the action may also update stock quantities.

## [1.36.2] - 2025-06-24

### Fixes

- **Cycle counts – location selection:** When adding a cycle count, all eligible locations are now listed correctly. Previously, the list could be truncated, causing some locations to be missing from the selection.
- **Deliveries – cubing calculation:** The cubing function triggered from the Deliveries pages now executes correctly, resolving an issue where the calculation could fail to run.

## [1.36.1] - 2025-06-17

### Improvements

- **Equipment list page** now shows an edit button (pencil icon) directly in the equipment list, alongside the existing view button, making it faster to update equipment settings without opening the detail page first.

- **Equipment detail – location category**: Equipment details now include a "Location Category" field that can be set when adding or editing an equipment detail line.

- **Priority / ordering controls** (customer order lines, rounds, patterns, rule version configs, equipment): The up/down reorder buttons are now smarter — they are disabled when an item is already at the top or bottom of the list, show a loading indicator while a reorder is in progress, and prevent double-clicks from triggering conflicting moves. Reordering is also more reliable across page boundaries.

- **Pick & Pack – handling unit model selection**: When a shipment does not need to be palletised, the system now automatically pre-selects the default pallet model instead of skipping the step entirely, ensuring the workflow always completes correctly.

- **Mobile feature scanning – input mask validation**: When a feature code has a format mask defined, the scan input field now validates the scanned value against that mask in real time and shows a clear error message if the format does not match.

### Fixes

- **Table column visibility**: Columns that are shown or hidden dynamically (e.g. after a configuration change) now update correctly without requiring a page reload.

- **Priority reordering after deletion**: Deleting an item from an ordered list (rule version configs, pattern path links) now correctly re-sequences the remaining items.

## [1.36.0] - 2025-06-12

### New features

- **Pick & Pack – Equipment selection step**: When the "Equipment scan at preparation" setting is enabled, operators are now prompted to select their equipment at the start of the Pick & Pack process. The chosen equipment is displayed in the session header and is used to filter the list of available rounds.

- **Pick & Pack – Force article scan**: A new "Force article scan" parameter allows administrators to require operators to always scan the article barcode, even when only one article is present on the handling unit, preventing automatic bypassing of this step.

- **Empty locations – Block filter**: A new optional filter on the empty-locations widget lets operators narrow down the list of available empty locations by warehouse block. The filter appears only when the corresponding parameter (`EMPTY_LOCATIONS_SHOW_BLOCK_FILTER`) is activated.

- **Rules – Stock owner on rules**: It is now possible to associate a stock owner with a rule when creating or viewing it.

- **Rules – Unified configuration form**: Input and output rule configurations (In/Out) are now managed through a single, unified form and page, simplifying the setup and editing of rule version parameters.

- **Last processing result on key records**: The last processing result code and detail message are now visible on Deliveries, Purchase Orders, Rounds, Outbound Handling Units, and Handling Unit Contents detail and list pages, making it easier to diagnose processing issues.

- **Manual allocation – Total weight**: The manual allocation modal for deliveries now displays the total theoretical weight (in kg) of the selected deliveries alongside the existing box count and total volume.

### Improvements

- **Pick & Pack – Back-navigation after round completion**: After finishing a round, the operator is correctly returned to the appropriate step (equipment selection if applicable, or round selection), avoiding a loss of session context.

- **Pick & Pack – Palletising logic refined**: The model used to display the handling-unit model selection and the one sent to the back end are now managed independently, ensuring the right behaviour in all equipment configurations.

- **Empty locations widget – Visual border**: The empty-locations panel now has a visible border and rounded corners to better distinguish it from the surrounding page.

- **Reception – Available quantity cap**: The quantity entry screen during reception now enforces a maximum corresponding to the remaining quantity to receive on the purchase order line, preventing over-reception at input time.

- **Handling unit carousel – Type label**: In the handling-unit selection carousel, the handling unit type label is now displayed instead of the internal code, making the choice clearer for operators.

- **Rules – Deleting a rule version config reorders remaining configs**: Deleting a configuration line from a rule version now automatically re-orders the remaining lines so there are no gaps in the sequence.

- **Rules – Add/Edit config disabled when lines already exist**: The buttons to add or edit input/output configuration parameters on a rule version are disabled (with an explanatory tooltip) when configuration lines already exist, preventing inconsistent setups.

- **Rules – Rule version status no longer editable**: The status field has been removed from the rule version edit form; status is now managed exclusively by the system.

- **Rules – Rule version deletion restricted**: A rule version can only be deleted if it is not the active version or if the rule is not currently in progress.

- **Web tables – Record count display**: List tables now show the range of currently displayed records and the total number of items (e.g. "1–25 out of 142 items").

- **Content movement – Improved error handling**: When scanning a handling unit during a content movement with an enforced origin location, invalid scans now navigate back and clear the session cleanly instead of showing a generic error.

- **Content movement – Expected handling unit check**: When a specific handling unit is expected at a location, scanning the wrong handling unit now raises a clear "unexpected item" error.

### Fixes

- **Pick & Pack – Feature type details on article scan**: Feature type details at preparation are now correctly filtered before being stored, avoiding the inclusion of irrelevant feature types in downstream steps.

- **Pick & Pack – Step 5 preserved across location changes**: The equipment selection step (step 5) data is now properly preserved when navigating through location selection, preventing data loss during the round flow.

- **Quantity validation – Zero available quantity**: The maximum-quantity validation rule on quantity entry screens now applies correctly even when the available quantity is zero (previously, a value of `0` was treated as "no limit").

- **Reception page – Unused variable warning removed**: A minor clean-up removes an unused state variable that had no effect on operators.

## [1.35.2] - 2025-06-03

### Improvements

- **Cycle count creation – smarter location range selection:** When defining the location range for a cycle count (by block, aisle, column, level, and position), the form now behaves more intuitively:
  - Selecting **"\*" (wildcard)** for the start of a range automatically sets the end to "\*" as well, covering all values for that dimension.
  - The column, level, and position fields are now **greyed out and locked** until the preceding dimension is chosen, preventing incomplete or inconsistent range definitions.
  - Changing the **block** selection now correctly **clears all previously chosen location fields** (aisle, column, level, position) so stale values from a different block can no longer be submitted.
  - The "end" aisle/column/level/position fields are **disabled when the corresponding start field is set to "\*"**, since the wildcard already implies the full range.

### Fixes

- **Movement detail – inbound box link corrected:** In the movement detail view, the link associated with the inbound handling unit now navigates to the correct "Inbound Boxes" page instead of the previous, incorrect destination.

## [1.35.1] - 2025-05-23

### Fixes

- **Pick & Pack – correct article identified when scanning a barcode shared by multiple articles.** Previously, the wrong article could be selected during preparation if a barcode was linked to more than one article. The system now matches the scanned barcode to the exact article it belongs to, preventing mix-ups during picking.

- **Pick & Pack – feature scanning now targets the right handling unit content when several articles are present.** When a round contained multiple different articles, feature details (serial numbers, batch numbers, etc.) could be recorded against the wrong item. The scan step now correctly filters by article, ensuring features are attached to the intended product.

## [1.35.0] - 2025-05-20

### New features

- **Change stock status directly from the mobile HU Info and content screens.** When the "enable content change" option is active, operators can open a modal on any stock-handling-unit content to update its stock status, quantity, and add a comment. Stock movements are recorded automatically.

- **Article-Info: new content selector filtered by article.** A dedicated carousel screen lets operators browse all stock contents for a given article (optionally filtered by location or handling unit), with location and category details displayed. When only one content matches it is selected automatically.

- **Reception: separate "Normal" and "Return" workflows.** The Reception Management menu now routes normal receptions and return receptions to distinct processes. Scanning a purchase order already filters the list to show only order types that match the chosen mode.

- **Reception: optional comment field on stock-status and quantity screens.** Operators can enter a free-text comment when selecting a stock status or confirming a received quantity; the comment is passed through to the final validation call.

- **Pick & Pack: shipping mode drives palletisation step.** When the carrier shipping mode is marked "not to be palletised" and no force-picking-check is set on the equipment, the handling-unit model selection step is skipped automatically and the process moves straight to auto-validation.

- **Pick & Pack: feature scanning now validates against real stock.** Each scanned feature value is checked against the actual handling-unit content features in the system; an error is shown immediately if the combination does not exist or the quantity is zero.

- **Locations: dimensions and weight fields.** Length, width, height, and maximum weight can now be entered when creating or editing a location in the back-office.

- **Locations: status now visible in the location list and detail view.** The location status (e.g. Available, Occupied, Disabled) is displayed in the location list and on the detail page.

### Improvements

- **Empty-location and similar-location suggestions exclude disabled locations.** The mobile screens that propose alternative put-away or picking locations no longer display locations whose status is "Disabled".

- **Location validation on the mobile prevents moves to disabled locations.** When a destination location is disabled, an error message is shown and the operator is sent back to re-scan.

- **Content-movement and HU-movement: scanning an invalid origin now returns to the menu.** If the scanned handling unit is empty or invalid and the scan was forced (e.g. from a round), the app now navigates back to the previous menu and clears the session instead of staying on the same step.

- **HU movement: final location data structure unified.** The destination location is now consistently handled as a list, removing edge-case errors when a location was returned as a single object versus an array.

- **Article-feature scanning in content movement filters to unique feature codes only.** Scanning an article/feature now restricts the search to unique feature codes, reducing false matches.

- **Pick & Pack: available quantity in the header reflects the matched content.** After features are confirmed, the available-quantity figure shown in the header is taken from the specific handling-unit content whose features match those scanned, rather than a generic first content.

- **Pick & Pack: article feature-type details (including feature code and date type) are now retrieved at scan time,** ensuring the correct feature prompts are displayed for each article.

### Fixes

- **HU movement crash when accessing final location.** A mismatch between `finalLocation` and `finalLocations` caused a crash at the final confirmation step; this is now resolved.

- **Logistic-unit picking-location selector no longer offers disabled locations.** The "disabled" status constant was incorrectly named; the right value is now used, so disabled locations are properly excluded from the picking-location dropdown in article logistic-unit forms.

- **Similar-location suggestions no longer include disabled locations** in both the standard reception and the stock-management flows.

## [1.34.1] - 2025-04-29

### New features

- **Box Checking workflow (mobile):** A new "Box Checking" screen is now available on the mobile interface under the Preparation Management menu. Operators can work through a guided step-by-step process to verify prepared boxes:
  1. **Select a printer** – choose the label printer to use for the operation.
  2. **Scan a handling unit** – scan the barcode of the outbound box to check; the system validates that it is in the correct "To Be Checked" status before proceeding.
  3. **Scan an article EAN** – scan the barcode of the article inside the box; the system confirms it matches the expected content.
  4. **Auto-validation** – once the article is confirmed, the box is automatically validated and the appropriate label is printed. If further boxes remain to check, the workflow loops back to the scan step automatically; otherwise a success message is displayed.

### Improvements

- The **Preparation Management** menu on mobile now includes the "Box Checking" option, making it directly accessible from the preparation home screen.
- The outbound handling unit status thresholds used during box checking have been updated to align with the new workflow statuses (the "To Be Checked" and new "Checked" statuses are now correctly recognised by the system).

## [1.34.0] - 2025-04-29

### New features

- **Pick & Pack – round assignment**: When you select a round that has no assigned operator, it is now automatically assigned to you. If another operator has already taken the round, you will see a clear error message and cannot start it by mistake.

- **Pick & Pack – shipping unit name**: You can now type in a custom name for a new shipping handling unit during the pick-and-pack process, giving you direct control over box/pallet labelling without extra steps.

- **Pick & Pack – location selection by level**: A dedicated level-selector screen is now available during picking, letting you choose the exact shelf level when a location has multiple levels, with barcode-scanner support.

- **Cycle count – locations without HU management**: Cycle counts can now be conducted on locations that do not use handling-unit management. A dedicated "Location count finished" button replaces the "HU count finished" button in those cases, and the closure logic is handled automatically.

- **Reception – scan handling unit at the end**: A new reception workflow variant lets you scan the handling unit at the end of the reception process instead of at the beginning, offering more flexibility for goods-in operations.

- **Stock management menu – reception content movement shortcut**: A new "Reception content movement" entry appears in the Stock Management menu, letting you start a content movement pre-set to the reception area with a single tap.

- **Cancelled purchase orders**: The system now correctly recognises a "Cancelled" status for purchase orders, preventing cancelled orders from appearing in active reception workflows.

---

### Improvements

- **Similar locations & empty locations – configurable count**: The number of suggested similar or empty locations displayed on the mobile device is now driven by a configurable parameter (`SIMILAR_LOCATIONS_NUMBER` / `EMPTY_LOCATIONS_NUMBER`) instead of being fixed at 3.

- **Pick & Pack – alternative picking location**: When you scan a picking location different from the one originally proposed but that contains the correct stock, you are now prompted to confirm the change. The system automatically updates the pick address and continues the workflow without losing your progress.

- **Pick & Pack – feature-type handling at article scan**: When scanning an article that has traceable features (e.g. serial numbers, batch numbers) required at preparation time, those features are now correctly identified and queued for scanning in the subsequent steps.

- **Pick & Pack – assigned-user re-check at validation**: Before finalising a pick-and-pack operation, the system now re-verifies that the round is still assigned to you, preventing conflicts when two operators work concurrently.

- **Cycle count – location checks relaxed**: Scanning a location during a cycle count no longer rejects it immediately if it differs from the expected one; the system now presents the available levels and lets the cycle-count logic decide on correctness, reducing unnecessary interruptions.

- **HU movement – multi-article destination check**: Moving a handling unit to a destination box that already contains stock now correctly allows the move as long as every article in the origin unit is also present in the destination, rather than only comparing the first article.

- **HU movement – locations without HU management**: Handling units that belong to a location flagged as "no HU management" are now blocked from being moved, with a clear error message, preventing unintended stock inconsistencies.

- **Content movement / quantity move validation**: Stock movement validation now calls the back-end function directly, delivering more precise and translated error messages instead of a generic failure notice.

- **Reception – handling unit location check**: When scanning a handling unit during reception, the system now verifies that the scanned unit is actually in the selected location, and shows a clear message (including the actual location name) if it is not.

- **Reception – article check relaxed**: Scanning an article during reception no longer requires the article to already exist in the scanned handling unit, allowing you to receive new articles into an existing unit.

- **Rounds list – personal rounds first**: Your own rounds (already assigned to you) are now listed at the top of the round-selection dropdown, making it quicker to find and resume your work.

- **Content-feature selection query improved**: The feature-selection step now queries features directly, returning more accurate and complete information for traceable articles.

- **Stock-owner filter on content selection**: When selecting stock content for an article, results are now filtered by stock owner, avoiding ambiguous matches across different owners.

---

### Fixes

- **Pick & Pack – "Back" navigation**: Pressing "Back" from the final handling-unit scan step now correctly returns to the previous step instead of skipping two steps back.

- **Pick & Pack – round status update**: Starting a round that was in "Started" status now correctly updates only that round's status to "In preparation" instead of affecting unrelated rounds.

- **Pick & Pack – loading spinner**: The auto-validation screen no longer displays a stray `/` character while processing; a clean loading spinner is shown instead.

- **Cycle count – location data persistence**: Location information (including HU-management flag) is now correctly saved and carried through all cycle-count steps, preventing data loss when navigating between screens.

- **Content movement – enforced HU back navigation**: If a pre-filled handling unit fails validation checks (empty, wrong location, wrong category), the workflow now correctly navigates back to the appropriate step instead of leaving you on a blank screen.

- **Quantity move – article information mapping**: Article details (name, stock owner) are now correctly mapped when validating a quantity move, preventing failures caused by missing data.

- **Quantity move – final handling unit step reference**: The form now reads the final handling unit from the correct workflow step, fixing cases where the unit appeared empty at validation time.

- **HU movement – final location data**: The final location is now passed correctly to the validation logic whether it comes as a single object or an array, preventing movement failures in certain location configurations.

- **Reception goods-in scan – purchase order filter**: The purchase order lookup no longer applies an unnecessary type filter, allowing all expected order types to be found when scanning a goods-in reference.

- **Reception goods-in scan – round-line detail inbounds**: Inbound details per round-line are now included in the goods-in response, giving the reception workflow complete information to track already-received quantities.

## [1.33.1] - 2025-04-02

_Internal technical maintenance, no visible functional impact._

## [1.33.0] - 2025-03-26

### Improvements

- **Adjustable page size in tables:** A page-size selector is now visible on all data tables, letting you choose how many rows are displayed per page without having to rely on a fixed default.
- **Smarter pagination after row removal:** When items are removed from a drag-and-drop list and the current page becomes empty, the interface automatically moves you back to the previous page instead of showing a blank page.
- **More reliable drag-and-drop reloading:** If a drag-and-drop list returns an unexpected empty result while data still exists, the list now refreshes automatically so items are never incorrectly hidden.

### Fixes

- **"Drop here" placeholder stays at the bottom:** The placeholder row in drag-and-drop location lists is now always sorted to the end, preventing it from appearing in the middle of the list after items are rearranged.
- **Dragging to the end of a list works correctly:** Dropping a location onto the "drop here" zone now correctly appends it at the very end of the list rather than inserting it at an unintended position.
- **Reordering no longer moves the placeholder:** Dragging existing locations between positions no longer accidentally triggers a move for the "drop here" placeholder row, ensuring only real locations are reordered.

## [1.32.0] - 2025-03-21

### New features

- **Manual allocation page for deliveries**: A new "Manual allocation" entry is now available in the Deliveries section of the side menu. It lists deliveries that are ready to be allocated, lets you select one or more, and triggers round creation by choosing from available equipment. The page also shows the number of boxes and total volume for the selected deliveries.

- **Drag-and-drop location management for pattern paths**: The screen for managing locations assigned to a pattern path has been fully redesigned. Locations can now be dragged from the left-hand list (with filters by category, block, aisle, column, level, and position) and dropped into the right-hand ordered list—or dragged back to remove them. Rows in the destination list can also be reordered by dragging. "Send all" and "Remove all" buttons allow bulk moves in one click.

- **Pattern path links on the Pattern detail page**: The detail page of a pattern now shows the list of associated pattern paths with their priority order. Up/Down arrows let you adjust the order directly from the list, and a disconnect button lets you remove a link after confirmation.

- **Pattern paths now shown on the Pattern path detail page**: The detail page of a pattern path now displays both the associated patterns and the associated locations (listed in order).

- **"Strict" flag on Patterns**: Patterns now expose an "Is Strict" (checkbox) field that can be viewed and edited.

- **Description field on article logistic units**: A description text area has been added to the add and edit forms for article logistic units.

- **Dispatch load via business function**: Dispatching a load now goes through a dedicated business function that provides richer error messages (including listing the deliveries that blocked the dispatch) and is more reliable.

- **Notifications menu item now respects permissions**: The "Notifications" entry in the monitoring menu is only shown to users who have read access to notifications.

### Improvements

- **Pattern path detail page**: The associated locations list is now sorted by their order number by default.

- **Pattern paths list and edit**: Pattern path names are now sortable in the list. The edit page no longer requires stock owner or pattern to be filled in (they were previously locked read-only fields that were mandatory).

- **Rule version config priority buttons**: The up/down order buttons for rule version configs are no longer disabled after the first click; they work reliably for repeated reordering.

- **Purchase order date column**: The purchase order date column now displays with a clearer label in the list.

- **Pattern paths breadcrumb**: Pattern paths and patterns pages now include the full Cartography breadcrumb trail for easier navigation.

### Fixes

- **Round packing stock owner**: During round packing validation on mobile, the stock owner was incorrectly taken from the round content instead of the round handling unit. This is now corrected, preventing stock owner mismatches on created stock.

- **Load dispatch permissions check**: The Edit Rule Version page was incorrectly checking Location permissions instead of Rule Version permissions. This is now fixed.

## [1.31.0] - 2025-02-18

### New features

- **Translations management:** A new **Translations** section is available under Administration. Users can view, create, edit, and delete translation entries (label/value pairs per language and category) directly from the interface, without needing developer intervention.

- **"Extras" management for Configurations and Parameters:** The detail page of a Configuration or Parameter now displays a dedicated **Extras** table. Users can add, edit, and delete individual key/value extra data entries attached to each record.

- **Shipping unit editing:** A dedicated edit form is now available for Shipping Units, allowing users to update all relevant fields (carrier, weight, delivery, status, etc.) from the interface.

### Improvements

- **Priority reordering across pages:** When reordering items using up/down priority arrows, the system now correctly handles items that sit at the boundary between two pages — the swap will work even if the adjacent item is on a different page.

- **Round advised address list:** Sorting on several columns in the Round Advised Address list has been disabled to prevent incorrect ordering results.

- **Equipment – handling unit model:** The weight of the handling unit model is now included when selecting a model on Equipment pages, providing more complete information during configuration.

### Fixes

- **Dark-theme breadcrumb separator:** The breadcrumb separator colour in dark mode was not being applied correctly; it now renders as expected.

- **Pattern path bulk creation:** A mismatch in the bulk-create input type for pattern-path locations has been corrected, preventing errors when adding multiple locations at once.

## [1.30.0] - 2025-02-04

_Internal technical maintenance, no visible functional impact._

## [1.29.0] - 2025-01-28

### Improvements

- **Dark mode – date & time pickers:** Date pickers, time pickers and range selectors are now fully styled in dark mode: calendar panels, headers, navigation arrows, placeholder text, separators and suffix icons all appear correctly on a dark background instead of reverting to a light/white style.
- **Dark mode – number inputs:** Numeric input fields (including their increment/decrement arrows) now display correctly in dark mode with the proper background and text colours.
- **Dark mode – autofill:** Browser-autofilled fields no longer flash white in dark mode; the filled background and text colour now match the rest of the dark theme.
- **Dark mode – selected-option highlight:** The highlighted item in a dropdown search list is now clearly visible in dark mode.
- **Dark mode – modal & drawer tables:** Tables inside modals and side drawers now keep the correct dark background instead of reverting to the light theme.
- **Dark mode – miscellaneous fixes:** Alert banners, collapsible sections, card titles, modal titles/headers/close buttons, loading spinner background, message notifications, sortable table rows, frozen table columns, and selected-item count labels all render correctly in dark mode.
- **Loading screen:** The full-screen loading spinner now uses the correct background colour (dark or light) according to the user's current theme setting, avoiding a harsh white flash when loading in dark mode.
- **Carrier form – "Available" and "To be loaded" fields:** These two checkboxes can now be edited when adding a new carrier. When editing an existing carrier, they are also editable unless the carrier already has shipments in progress, in which case they are locked to prevent unintended changes.
- **Article editing – Status field removed:** The "Status" field has been removed from the article edit form to reflect the correct business rules.
- **Cycle count form – section labels corrected:** The "From" and "To" section headers in the Add Cycle Count form now display the correct translated labels.
- **Role details – remove user without page reload:** Removing a warehouse worker from a role now refreshes the list in place instead of reloading the entire page, making the action faster and smoother.
- **List pagination reset on filter change:** When a filter or column sort is changed on any list page, the page number automatically resets to page 1, preventing the situation where no results appear because the user was on a page that no longer exists after filtering.
- **Language selector – no duplicate settings:** Changing the interface language no longer creates duplicate language preference entries; the existing preference is updated in place.
- **Mobile – language displayed on load:** The language selector on mobile now reliably shows the correct currently active language when the app first loads.
- **Settings reset – logout protection:** Resetting user settings when no saved preferences exist no longer triggers an unnecessary page reload; the settings panel simply closes instead.

## [1.28.0] - 2025-01-21

_Internal technical maintenance, no visible functional impact._

## [1.27.0] - 2025-01-19

### New features

- **Translations from the database:** Labels and messages throughout the mobile interface can now be managed and customised directly in the Cella back-office, without waiting for a software update. The interface automatically falls back to the built-in translations when no database entry is found.
- **User language preference saved per account (mobile):** The language selected in the mobile interface is now saved to your user profile and restored automatically at each login, even across devices.
- **Round picking auto-validation:** The round picking workflow now validates and moves to the next picking task automatically once a quantity is confirmed, removing the need for an extra manual validation step.
- **Round packing auto-validation:** Similarly, the round packing workflow now auto-progresses to the next packing step after each confirmation, and automatically triggers box closing when all items have been packed.
- **Better duplicate-scan detection:** When scanning a serial number or feature that has already been recorded in the current picking or packing operation, the system now shows a specific "already scanned" warning instead of a generic error message.
- **Last cycle-count date and modification date visible on handling units:** The date of the last cycle count and the last modification date are now available when consulting handling unit information.

### Improvements

- **Round categories renamed for clarity:** Rounds are now labelled "Inbound" and "Outbound" (previously "Reception" and "Preparation") throughout the mobile interface, making their purpose clearer.
- **Language selector persists the choice:** Changing the display language in the mobile app now immediately saves the preference to your account so it is remembered for future sessions.
- **Stock quantity updates use atomic operations:** Quantity changes during picking, packing, and round-line processing are now applied as increments/decrements rather than absolute values, reducing the risk of discrepancies if two operations happen in quick succession.
- **Movement traceability improved for round picking:** Stock movement records now capture the exact article, stock owner, and feature information directly from the handling-unit contents at the time of picking, making movement history more reliable.
- **Crash prevention on optional data:** Several screens (HU movement, quantity movement) no longer crash when optional information such as stock-owner name is absent.

### Fixes

- **Reception goods-in scan now uses the correct round category filter:** Scanning a goods-in reference at reception now correctly searches inbound rounds only, preventing mis-matches with outbound rounds that share the same name.
- **Round picking and packing round-selection lists now show only outbound rounds:** The round selector in picking and packing workflows was previously using the wrong category filter; it now correctly lists only outbound rounds.
- **Mobile app port consistency:** The development and production start-up commands now consistently use port 3001, preventing conflicts when both the web and mobile applications are running simultaneously.

## [1.26.0] - 2024-12-28

### New features

- **Cycle count – Feature review step:** During a cycle count, operators are now shown a dedicated screen to review and, if needed, correct the traceability features (e.g. serial numbers, lot dates) attached to a handling unit before recording the counted quantity. Any modification is automatically logged as a cycle count error for traceability purposes.

- **Cycle count – Automatic validation:** Once the quantity is entered, the cycle count movement is now validated automatically, without requiring a separate confirmation button press. The workflow advances on its own to the next handling unit or line.

- **Cycle count – Cross-pass handling unit recognition:** A handling unit that was scanned during a previous counting pass is now correctly recognised in subsequent passes (even when it no longer physically exists in stock), avoiding false "unit not found" errors.

- **Cycle count – Cycle count errors list:** A new dedicated page is available in the web interface to list and consult all errors logged during a cycle count (anomalies, unexpected items, feature changes, etc.).

- **Palletization – Handling unit model selection:** When palletising boxes onto a pallet, operators are now prompted to select the pallet model (type/format) before scanning boxes. The chosen model's weight and closure weight are automatically applied to the newly created pallet.

- **Carriers – Edit form:** Carriers can now be fully edited from the web interface, including contact details and entity address fields that were previously read-only.

- **Purchase orders – Edit form:** Purchase orders can now be fully edited from the web interface, including address and contact information fields.

- **Deliveries – Edit address form:** The delivery address can now be edited directly from a dedicated form in the web interface.

- **Third-party address contacts – Edit form:** Third-party address contacts can now be edited from the web interface.

- **Credits – "Print credit" action:** A "Print credit" action button is now available on credit note pages.

- **Date pickers – Locale-aware display:** Date fields across the mobile app now display and accept dates in the format matching the active language (DD/MM/YYYY in French, MM/DD/YYYY in English). The calendar pop-up is also sized to remain fully visible on small screens.

---

### Improvements

- **Cycle count – Stock owner auto-selection:** When only one stock owner exists, it is selected automatically and the operator is not prompted to choose.

- **Cycle count – Line-by-line progression:** After closing a location, the workflow now moves directly to the next pending cycle count line instead of restarting from the beginning, making multi-line counts faster.

- **Cycle count – Larger cycle count list:** Up to 200 cycle counts (previously 100) are now shown in the selection list, and already-validated counts are also included.

- **Cycle count – Handling unit from previous pass:** A handling unit recorded in a previous pass is now correctly associated even if it is no longer present in stock, preventing unnecessary "unit does not exist" pop-ups.

- **Cycle count movements – Improved list display:** The movements list now shows the stock owner name, location name, article name, and handling unit name as plain text columns, making the list easier to read and filter. A "Created by cycle count" indicator and the features data are also now visible on the detail page.

- **Cycle count lines – Order column:** The line order number is now displayed in the cycle count lines list and detail pages.

- **Palletization – Simplified header:** The palletization screen header is streamlined; no longer switches to a secondary display mode during the process.

- **Loads – Conditional step display:** The load validation step is now shown only when applicable, preventing an empty or misleading screen when automatic validation is not triggered.

- **Article barcode creation – Preserved form context:** After adding a barcode, the form now retains the article and stock owner context so the operator can immediately add another barcode without re-entering that information.

- **Barcode error messages:** Error messages when a barcode already exists are now displayed correctly to the operator.

- **"Cartography" label (French):** Corrected French translation from "Cartography" to "Cartographie".

- **Cycle count line finished notification:** A clear success message is shown when a cycle count line is fully completed.

---

### Fixes

- **Cycle count – Duplicate confirmation dialogs:** Fixed an issue where the "overwrite quantity" or "create handling unit" confirmation pop-up could appear multiple times if the screen re-rendered before the operator answered.

- **Cycle count – Wrong article detected across passes:** Scanning an article on pass 2 or 3 that differs from what was scanned on pass 1 now correctly triggers an error instead of silently overwriting the previous pass data.

- **Handling unit scan – Stale state on failed scan:** When a handling unit barcode was scanned but not found, the previous result was incorrectly kept. This is now properly cleared.

- **Palletization – Error code display:** GraphQL error codes returned during palletization final-step validation are now correctly shown to the operator.

- **Cycle count – Location closure no longer requires an active scan:** Fixed a regression where attempting to close a location would incorrectly block if a scan had been started but not yet completed.

- **"Vat rates" label:** Corrected an English label collision between "Vat Rate" (singular) and "Vat Rates" (plural) so both appear correctly across the interface.

## [1.25.0] - 2024-12-01

_Internal technical maintenance, no visible functional impact._

## [1.24.0] - 2024-11-23

### New features

- **Pick & Pack – handling unit model selection:** During the Pick & Pack workflow, operators are now prompted to choose a handling unit (box/pallet) model when no packing unit is already in progress. A dedicated selection screen lists all eligible outbound models and supports barcode scanning to speed up the choice.

- **Equipment – picking pattern and reservation pattern:** Equipment records now include two new optional fields — **Pattern** (picking round profile) and **Reservation pattern** — which can be set when creating or editing a piece of equipment. Both fields are visible on the equipment detail page.

- **Pattern paths – delete from list and detail:** Pattern paths can now be deleted directly from both the list view (via a trash-can button on each row) and the detail page. Deletion goes through a confirmation dialog before taking effect.

- **Customer order address – address lookup (France):** When adding a delivery address on a customer order, a new **Address to search** field is available. Typing a partial address queries a real-time address validation service (France only) and lets operators pick the correct street, postcode and city from the suggestions, automatically filling in the address fields.

- **AutoComplete fields in forms:** Several fields that previously used a plain dropdown (e.g. delivery address fields) now use a searchable auto-complete control, making it faster to find the right value in long lists.

### Improvements

- **Pick & Pack – clearer error for already-shipped loads:** The mobile app now displays an explicit message when an operator tries to process a load that has already been shipped, instead of a generic error.
- **Pattern path breadcrumb:** The breadcrumb navigation on pattern path pages now correctly follows the full Cartography → Pattern Paths hierarchy.
- **Add pattern path – default order value:** When creating a new pattern path, the order number is now automatically pre-filled with the next available value based on existing paths, reducing manual data entry.

### Fixes

- **Duplicate barcode error message:** The system now shows a clear message ("This barcode already exists for this stock owner") when a duplicate barcode is detected during article creation, in both English and French.

## [1.23.0] - 2024-11-03

### New features

- **Round conflict warning on location selection (mobile):** When performing a content move or a handling-unit move, if the destination location is already planned for one or more active picking rounds, a confirmation pop-up now warns the operator before proceeding. The operator can confirm or cancel the selection.

- **"Close" action on Credit and Customer Order detail pages:** A **Close** button is now available on the Credit and Customer Order detail pages, allowing users to manually set the record status to "Closed" directly from the detail view.

- **"Add content feature" button hidden when not applicable:** On the Handling Unit Content detail page, the button to add a content feature is now only displayed when the article actually has a feature type defined, avoiding confusion for articles that do not use features.

### Improvements

- **Stock-zero items filtered out during content and handling-unit moves (mobile):** Articles with a quantity of zero are now automatically excluded when selecting contents to move. If no stock remains, the operator receives a clear message ("This article is no longer in stock") and is sent back to the previous step.

- **Action Codes and Return Codes lists upgraded:** Both lists now use the more capable list framework (V2), enabling standard delete and soft-delete (disable/lock) actions with confirmation dialogs, consistent with the rest of the application. A scope filter dropdown replaces the previous free-text filters.

- **Feature Types and Stock Statuses: system records can now be deleted:** The restriction that prevented deletion of records flagged as "system" has been removed from the Feature Types and Stock Statuses lists.

- **Location edit form now auto-populates the building name:** The building associated with a location's block is retrieved and displayed automatically when editing a location, removing the need to pass it manually through the page URL.

- **Equipment edit form – toggle fields and dropdowns reset correctly:** Boolean toggles (available, distributed, mono-company, etc.) and dropdown selectors on the Equipment edit page now reflect the saved values correctly when the form is opened. Dropdown fields (Stock Owner, Mechanized System, Label Printing, Printer) also have a clear button so the selection can be removed.

- **Equipment Detail form – fields resolved correctly:** The Equipment Detail edit form now reads the equipment and stock-owner identifiers directly from the record, preventing mismatches when the form is reloaded.

- **Edit forms refresh data reliably after save:** Several edit forms (Customer Order, Customer Order Address, Credit Address, Location, Article Barcode, Article Logistic Unit, Equipment, Return Code, Action Code) now correctly re-populate their fields whenever the underlying record changes, preventing stale data from appearing after a save.

- **Handling Unit Content detail page refreshes after a content feature is deleted:** Removing a content feature from a Handling Unit Content now immediately refreshes the detail view so the deleted feature disappears without a manual page reload.

- **Location detail page shows the associated building:** The block detail on a location now includes the building name, visible in the breadcrumb and detail panel.

- **Round-picking display is more resilient:** The picking round summary no longer crashes when the location or article name is temporarily unavailable.

- **Location blocking-status and location-group dropdowns have a clear option:** Both fields on the Location edit form can now be cleared (set to no value) using the standard clear button instead of requiring a blank placeholder entry.

- **Credit list now shows invoice number and creation date by default:** The invoice number column is visible by default in the Credits list, and the creation date column is also shown without needing to be manually unhidden.

- **"Documents" label added to the interface:** A new "Documents" label is available in both English and French, ready for use in upcoming document-related screens.

- **New translated field labels (French & English):** Labels for *Date Type*, *Location* (on handling unit and content views), and *Invoicing third party* are now correctly translated and displayed in lists and detail panels.

### Fixes

- **Block location edit breadcrumb now links correctly:** The breadcrumb on the block-location edit page now points to the correct block detail page.

- **Edit button on block location detail page now navigates to the correct URL:** The "Edit" button on a block location detail page was pointing to a wrong path; this is now corrected.

- **Action Code translation handled correctly when fields are empty:** Saving an Action Code with no translation values no longer sends an empty translation object to the server, preventing unexpected overwrite of existing translations.

- **Credit detail page internal link corrected:** The link from a credit record to its parent customer order now resolves to the correct page.

## [1.22.0] - 2024-10-19

### Improvements

- **Updated look of page headers** across the desktop interface and the mobile interface: the back-button, title, subtitle, breadcrumb, tags, and action buttons are now rendered with a custom header component that replaces the deprecated Ant Design PageHeader, keeping the same information in a cleaner layout.

- **Breadcrumb colours** in the desktop interface now correctly adapt to the dark theme (separator and active item text are rendered in lighter tones so they remain legible on dark backgrounds).

- **Side menu** text and arrow colours are now explicitly white so menu items are always readable on the dark sidebar background.

- **Logo in the desktop header** is now a clickable link that takes users back to the home page.

- **Language selector** (both desktop and mobile) no longer shows a dropdown arrow and has a cleaner borderless style that blends into the header bar.

- **Theme and menu toggle switches** no longer display unwanted internal padding, giving them a tidier appearance in the header.

- **Tables** (desktop): column-separator lines between header cells are hidden, resulting in a cleaner table header.

- **Drawers** (desktop and mobile): migrated from the deprecated `visible` prop to `open`, resolving potential rendering warnings and ensuring drawers open and close reliably.

- **Modals** (print copies, single print, crontab editor, bulk-edit articles): migrated from the deprecated `visible` prop to `open`, ensuring consistent display behaviour.

- **Mobile theme preference** is now stored under a dedicated cookie key (`mobile_theme`) so that the mobile and desktop theme settings no longer interfere with each other.

- **Dark and light CSS themes** have been refreshed with formatting improvements that keep multi-value `transition`, `box-shadow`, and `animation` properties on separate lines, improving predictability across browsers.

- **Underlying platform upgrades** (Next.js, React, Ant Design, and several supporting libraries) bring stability, performance, and compatibility improvements that users may notice as faster page loads and fewer visual glitches.

### Fixes

- **Delete actions** in several detail pages (Action Codes, Article Sets, Article LU Barcodes, etc.) no longer depend on a stale loading flag; the success callback now executes correctly immediately after the server confirms deletion.

- **Unsaved-changes guard** on the Article Logistic Unit add and edit forms now clears correctly after a successful save, preventing a false "unsaved changes" warning when navigating away after saving.

- **Profile menu** in the desktop header now uses the current Ant Design `Dropdown` API (`menu` prop), fixing a deprecation warning and ensuring the menu opens correctly.

## [1.21.0] - 2024-10-06

### New features

- **Round advised addresses: reorder picking sequence** – On a round's detail page, the list of advised addresses now includes up/down arrow buttons to adjust the picking order of each address, as long as the round has not yet started.

### Improvements

- **Consistent date display across all list screens** – Dates and date-times stored in records are now formatted according to your language/locale on every list screen (equipment, notifications, hook configurations, scheduler configurations, pattern paths, record history, rule versions, rule version configurations, and all generic list views). Previously, some screens displayed raw date strings.

- **Feature-code "date" values no longer misformatted** – When a handling-unit content feature stores a value that looks like a date but is not actually of date type (e.g. a serial number or code that resembles a date), the value is now displayed as-is instead of being incorrectly converted to a formatted date. This applies to detail pages, edit pages, and list views.

## [1.20.0] - 2024-09-24

### Improvements

- During Pick & Pack operations, the article description is now displayed on the mobile screen alongside the article name, giving operators more context when confirming the item to pick.

## [1.19.0] - 2024-08-25

### Fixes

- When scanning a value that happens to be a valid date (e.g. a serial number or batch code that looks like a date), the system no longer incorrectly converts it into a date format. Only fields explicitly defined as date-type features are now reformatted as dates, both during picking/pack preparation and goods reception.

## [1.18.0] - 2024-08-22

### New features

- **Scheduler Configs (web):** A new "Scheduler Configs" section is available in the Administration menu. Users with the appropriate permissions can create, view, edit and delete scheduler configurations, manage their arguments (add, edit, delete individual key/value pairs), and configure the execution schedule through a dedicated crontab editor with field-by-field guidance (minute, hour, day of month, month, day of week).

- **Excel Import (web):** A new "Excel Imports" page is available in the Administration menu. Users can select and upload an `.xlsx` file to import data directly into the WMS without leaving the interface.

- **Hook Config arguments (web):** Arguments for hook configurations can now be managed individually (add, edit, delete a single key/value pair) directly from a hook config's detail page, replacing the previous free-text field approach.

### Improvements

- **Unload of pallets (mobile):** When unloading a pallet from a load, all boxes attached to that pallet are now correctly reset to "to be loaded" status in one operation, rather than only the pallet itself. This prevents boxes being left in an incorrect state after an unload.

- **Empty locations and similar locations (mobile):** The panels showing empty locations and locations with similar stock now load more reliably and no longer depend on an intermediate hook that could cause display issues or stale data.

- **Configuration parameters (web):** All configuration parameters now show the edit button regardless of whether they are flagged as system entries, giving authorised users consistent access to edit any parameter.

## [1.17.0] - 2024-08-10

### New features

- **Documents attached to third parties:** You can now associate files (e.g. contracts, certificates, PDFs) directly with a third-party record. A new "Documents" section appears on the third-party detail page, where you can upload one or several files at once (up to 20 MB each) using a drag-and-drop area.
- **Download / print a third-party document:** Each document listed on a third party can be downloaded directly from the list or from its detail page using the dedicated button.
- **Third-party document detail page:** Clicking on a document opens a dedicated detail page showing who created or last modified it and when. The document can also be deleted from that page if you have the required permissions.

### Improvements

- **Delivery address drop-down more resilient:** When adding an address to a delivery, addresses that have no entity name are now shown using their entity code instead of appearing blank, and the list sorts correctly even when some names are missing.
- **Round box order follows picking route:** Boxes associated with a round are now listed in the same order as the advised picking addresses, making it easier to prepare shipments in the correct sequence.

### Fixes

- **Handling-unit movement on mobile:** The final destination check during a handling-unit move no longer fails when the system returns an empty result set; the validation now correctly handles the case where no matching unit is found.

