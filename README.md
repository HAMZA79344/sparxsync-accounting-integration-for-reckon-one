=== SparxSync Accounting Integration for Reckon One ===
Contributors: haamzaa
Tags: reckon, reckon one, woocommerce, invoice, accounting
Requires at least: 6.2
Tested up to: 7.1
Requires PHP: 7.4
Stable tag: 2.1.0
License: GPLv2 or later
License URI: https://www.gnu.org/licenses/old-licenses/gpl-2.0.html

Send WooCommerce orders to Reckon One as customer invoices automatically, with matching lines, tax and totals. Safe background sync with retries.

== Description ==

**SparxSync Accounting Integration for Reckon One** connects your WooCommerce store to your Reckon One book. When an order reaches a status you choose (for example *Processing* or *Completed*), the plugin creates a matching customer invoice in Reckon One for you, in the background, so you no longer have to type orders into your accounts by hand.

It is built for Australian and New Zealand store owners, bookkeepers and accountants who use Reckon One and want a reliable WooCommerce to Reckon One sync: sales invoices with the right customer, ledger accounts and GST codes, matching WooCommerce to the cent.

This is an independent integration. It is **not** an official Reckon or WooCommerce product.

= What it does =

* **Dashboard and analytics:** see invoices sent, sales value sent to Reckon and a daily chart for the last 30 days, plus queue health and your most recent invoices, at a glance. All figures come from your own store data; nothing is tracked or sent anywhere.
* **Guided setup:** a step-by-step checklist shows exactly what is left to configure and takes you straight to it.
* **Secure connection:** connects to Reckon One with OAuth 2.0. Credentials can also be defined in `wp-config.php`.
* **Book and mappings:** choose your Reckon book, then map your sales, shipping and fee ledger accounts and your WooCommerce tax rates to Reckon tax codes.
* **Automatic invoices:** finds or creates the Reckon customer, then creates one invoice whose lines, tax and totals match the saved order.
* **Never slows checkout:** orders are queued with WooCommerce Action Scheduler. No Reckon API call happens while a customer is paying.
* **Duplicate protection:** every invoice carries a stable reference. If the result of a request is unknown, the plugin checks Reckon before trying again instead of sending a second invoice.
* **Invoice preview:** open any order that has not been sent yet and see exactly what its Reckon invoice will contain: each line, where it goes (Reckon item or ledger account), its tax code, and the totals. Problems such as a missing tax mapping or a missing SKU show up before anything is sent. The preview never contacts Reckon.
* **Send past orders:** choose a date range, see how many orders will be sent and how many already have an invoice, then send them in small background batches with a progress bar and a Cancel button. Orders that already have an invoice are skipped, so it is safe to run more than once.
* **Paid in Reckon:** once an hour the plugin reads the status of recently sent invoices and marks orders "Paid in Reckon" when the invoice is paid there, with a note on the order. It is read-only: nothing is written to Reckon and the WooCommerce order status is never changed. You can switch it off.
* **Clear status for every order:** a Reckon One panel on each order shows its invoice status, and an overview page lists queued, failed and needs-review orders with retry and recovery buttons.
* **Product options:** match products to Reckon items by SKU, post lines to a ledger account, or do both.
* **Refund and cancellation alerts:** orders refunded or cancelled after export are listed for your accountant to review. Reckon invoices are never changed or deleted automatically.
* **Privacy-minded logs:** credentials, tokens and customer details are never written to the log.
* **Compatible with HPOS** (High-Performance Order Storage) and legacy order storage.

= What it does not do =

To keep your accounts safe and predictable, this plugin creates invoices only. It does **not** post payments, create credit notes, or sync products, prices or stock. The only thing read back from Reckon is each invoice's status (Draft, Approved or Paid), which is shown on the order; WooCommerce orders are never changed because of it.

= Need help or a custom feature? =

This plugin is built and maintained by [SkillsSparx](https://skillssparx.com/). If you need help connecting Reckon One, setting up your mappings, fixing orders that will not sync, or you want a custom WooCommerce or accounting feature built for your store, [get in touch with our team](https://skillssparx.com/contact/).

Questions about the free plugin are also welcome in the WordPress.org support forum.

== External Services ==

This plugin connects to Reckon One, a third-party accounting service operated by Reckon Limited. It is required: the plugin's only purpose is to create invoices in your Reckon One book. A Reckon One subscription and Reckon developer-partner credentials (Client ID, Client Secret and Subscription Key) are needed.

Nothing is sent to Reckon during checkout. Requests are made only when an administrator uses the connection screens, when the background worker runs with synchronization switched on, or by the optional hourly invoice status check described below.

**Reckon Identity service** — `https://identity.reckon.com`

* Used for: signing in to Reckon (OAuth 2.0 authorization), exchanging and refreshing access tokens, and, if you choose, revoking access when you disconnect.
* Data sent: the authorization code, refresh token, and your Client ID and Client Secret.
* When: when you click Connect, Reconnect or Disconnect, and when an access token needs refreshing.

**Reckon One API** — `https://api-v2.reckonone.com`

* Used for: reading your books, ledger accounts, tax codes, address types and items; finding and creating customers; finding, creating and reading invoices; reading the status of invoices the plugin created.
* Data sent: the customer's name, company and billing email (and the billing address only if you turn that on); the invoice date, line descriptions, quantities, amounts, tax codes and tax amounts, an invoice reference, and a note with the WooCommerce order number.
* When: when you test the connection or refresh Reckon data, and when an order is processed by the background worker. If "Check Reckon for paid invoices" is switched on (Synchronization tab), up to 20 recently sent invoices are read once an hour; this request sends only the book ID and invoice ID.

Reckon's terms and privacy policy: [https://www.reckon.com/au/legal/](https://www.reckon.com/au/legal/)
Reckon developer portal: [https://developers.reckon.com/](https://developers.reckon.com/)

Credentials and tokens are stored in your WordPress database and are never shown again after saving. Please list Reckon as a data processor in your store's privacy policy.

The "Need help?" buttons in the plugin's admin pages are ordinary links to [skillssparx.com](https://skillssparx.com/). No data is sent to SkillsSparx unless you click one, and then only what your browser normally sends when opening a web page.

== Installation ==

1. In your WordPress admin go to **Plugins → Add New**, search for "SparxSync Accounting Integration for Reckon One", then click **Install Now** and **Activate**. WooCommerce 8.2 or later must be installed and active.
2. Go to **WooCommerce → Reckon One**.
3. **Connection tab:** enter your Client ID, Client Secret and Subscription Key, register the Redirect URI shown on the page with Reckon, then click **Connect to Reckon**.
4. **Book & mappings tab:** click **Refresh Reckon data**, choose your book, then map your ledger accounts and tax codes and save.
5. **Synchronization tab:** choose which order statuses create invoices, check that the configuration check is all green, then switch on **Automatic synchronization**.
6. Place a test order, then open it in WooCommerce: the **Reckon One** panel shows its invoice status. Anything that needs attention is listed on the **Orders** tab.

Automatic synchronization stays off after installing or upgrading until you have reviewed these settings.

== Frequently Asked Questions ==

= Do I need a Reckon developer account? =

Yes. Reckon issues the Client ID, Client Secret and Subscription Key to approved developer partners through the [Reckon developer portal](https://developers.reckon.com/). If you need help getting set up, [SkillsSparx can help](https://skillssparx.com/contact/).

= Which orders are sent to Reckon? =

Only orders that change to one of the statuses you select on the Synchronization tab. Pending, failed, cancelled and refunded orders are never invoiced.

= Can it create duplicate invoices? =

The plugin is designed to prevent them. Each invoice uses a stable reference, an order is marked before an invoice is created, and an unknown result is checked against Reckon before any retry. Reckon does not offer an idempotency key for invoices, so no integration can promise exactly-once delivery, but the plugin stops and asks you to review instead of guessing.

= Does it post payments or create credit notes? =

No. It creates invoices only. Orders that are refunded or cancelled after export are listed on the Orders tab so you can adjust them in Reckon.

= Does it sync products, prices or stock? =

No. SKU matching only looks up items that already exist in Reckon. It never creates or changes products, prices or stock.

= Does it work with HPOS? =

Yes. All order data is read and written through WooCommerce's own functions, and compatibility with High-Performance Order Storage is declared.

= What happens to my data if I delete the plugin? =

Pending background jobs are always cancelled. Settings, credentials and cached Reckon data are deleted only if you tick "Delete settings… when the plugin is deleted" on the Synchronization tab. Order sync records (Reckon invoice IDs and references) are always kept so the same orders are not exported twice after a reinstall. WooCommerce orders and Reckon records are never deleted.

= Can I send orders that were placed before I installed the plugin? =

Yes. On the **Orders** tab, under **Send past orders to Reckon**, choose a date range and click **Check orders**. You will see how many orders are in the range and how many already have an invoice, before anything is sent. Up to 5,000 orders can be sent in one go; use shorter ranges for more. Failed and needs-review orders are left for you to handle.

= How does "Paid in Reckon" work? =

Once an hour, the plugin reads the status of up to 20 invoices it created in the last 120 days that are not yet marked as paid. When Reckon reports an invoice as Paid, the order shows "Paid in Reckon" and gets an order note. The WooCommerce order status is not changed, and nothing is written to Reckon. Payments are still recorded in Reckon as usual. You can turn the check off on the Synchronization tab.

= Can I see the invoice before it is sent? =

Yes. Open an order that has not been sent yet and expand **Preview the Reckon invoice** in the Reckon One panel. It uses your saved mappings and cached Reckon data and never contacts Reckon. Reckon items are matched by SKU, and the customer is matched by email, only when the order is actually sent.

= Where can I see what went wrong with an order? =

Open the order in WooCommerce and look at the Reckon One panel, or go to **WooCommerce → Reckon One → Orders**. Detailed logs are under **WooCommerce → Status → Logs** with the source `reckon-wc`.

= I need a feature this plugin does not have. =

[Tell us about it](https://skillssparx.com/contact/). SkillsSparx builds custom WooCommerce and accounting integrations.

== Screenshots ==

1. Dashboard: invoices sent, sales value, a 30-day chart, queue health and recent invoices.
2. Guided setup checklist for new installs.
3. Connection tab: enter your Reckon credentials and connect.
4. Book & mappings tab: choose your book and map ledger accounts and tax codes.
5. Synchronization tab: configuration check and order status settings.
6. Orders tab: queued, failed and needs-review orders with retry buttons, and the progress of sending past orders.
7. Reckon One panel on the order screen: the invoice preview before an order is sent, and the invoice and "Paid in Reckon" status afterwards.
8. Send past orders: check a date range, then send it in the background.

== Changelog ==

= 2.1.0 =
* New: Invoice preview on the order screen shows each line, where it is posted, tax codes and totals before an order is sent, and flags problems early. It never contacts Reckon.
* New: Send past orders. Check a date range, then send its orders to Reckon in background batches of 25 with progress and Cancel. Already-invoiced, failed and needs-review orders are skipped.
* New: Paid in Reckon. An hourly, read-only check marks orders whose Reckon invoice is paid, adds an order note, and shows the Reckon status on the order and the dashboard. Can be switched off on the Synchronization tab.
* Fix: if two copies of the plugin are active (for example an older upload in a different folder), the second copy now stays inactive and shows a notice instead of causing a fatal error.

= 2.0.0 =
* First public release on WordPress.org.
* New: Dashboard with 30-day invoice analytics, queue health, recent invoices and a guided setup checklist.
* New: Modern, branded admin design. The stylesheet loads only on the plugin's own page, with no scripts and no external files.
* New: "Need help?" button and help box on the settings page, and help links on the Plugins screen.
* Changed: plugin renamed to "SparxSync Accounting Integration for Reckon One"; text domain is now `sparxsync-accounting-integration-for-reckon-one`.
* Background order queue with Action Scheduler, OAuth 2.0 connection, book and tax mappings, duplicate protection, verification and recovery tools, and an orders overview.

== Upgrade Notice ==

= 2.1.0 =
Adds an invoice preview, sending past orders in bulk, and a read-only "Paid in Reckon" status check. No settings need changing.

= 2.0.0 =
First public release. Automatic synchronization stays off until you review the connection, book, mappings and synchronization settings.
