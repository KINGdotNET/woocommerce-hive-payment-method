=== WooCommerce Hive Payment Method ===
Contributors: roomservice, sagescrub, recrypto
Donate link: https://peakd.com/@roomservice
Tags: woocommerce, woo commerce, payment method, hive, hbd, crypto
Requires at least: 4.1
Tested up to: 5.4.1
Stable tag: 1.1.6
Requires PHP: 5.2.4
License: GPLv3
License URI: https://www.gnu.org/licenses/gpl-3.0.html

Accept HIVE, HBD and HIVE-ENGINE payments in your WooCommerce store via HiveSigner. Automatically converts from fiat (USD, EUR, etc) to HIVE. No transaction fees.

== Description ==

WooCommerce Hive Payment Method lets you accept Hive payments directly to your WooCommerce shop (Currencies: HIVE, HBD).

= Details =

* There is no extra transaction fee. Payments are made directly between customer and store owner via HiveSigner. 
* This plugin will automatically detect if payment was made once it is posted to Hive Blockchain. 
* If payment is not completed within several minutes of submitting an order an automatic payment reminder email will be sent to the customer with instructions for submitting payment. This is a fallback for 1) the customer doesn't complete the transaction, and 2) the payment detection functionality in this plugin stops working for any reason.
* Currency exchange rate between FIAT and HIVE/HBD is automatically calculated at time of checkout.
* Currency exchange rate between FIAT and HIVE/HBD can be optionally displayed below the product price on the product page.
* Support for YITH WooCommerce Subscription plugin subscription renewals

= Supported Steem Currencies =
- Hive (HIVE)
- Hive Backed Dollars (HBD)
- Hive-Engine Tokens

= FIAT Currencies Supported =
- Currently supports fiat currencies such as: AUD, BGN, BRL, CAD, CHF, CNY, CZK, DKK, GBP, HKD, HRK, HUF, IDR, ILS, INR, JPY, KRW, MXN, MYR, NOK, NZD, PHP, PLN, RON, RUB, SEK, SGD, THB, TRY, ZAR, EUR
- If none of the fiat currency listed above, it will default 1:1 conversion rate between your store's currency and HIVE or HBD.

= How it Works Behind The Scenes =
* Exchange rates are updated once an hour
* FIAT foreign exchange rates are gathered from the European Central Bank's free API
* HIVE/HBD exchange rates are determined by querying three exchanges and taking the average: Binance, and Bittrex.
* Binance rates are determined by converting USDT (Tether) -> BTC -> HIVE (HBD is not supported by Binance)
* Bittrex rates are determined by converting USD -> BTC -> HIVE / HBD
* HIVE-ENGINE token rates are determinded by converting USD -> BTC -> HIVE -> HIVE-ENGINE token
* Your store's wallet is scanned every 5 minutes for pending transactions (if there are any orders with pending payment)
* If an order is Pending Payment for too long it will be automatically canceled by WooCommerce default settings. You can change the timing or disable this feature in WooCommerce -> Settings -> Products -> Inventory -> Hold Stock (Minutes)

= Technical Requirements =
WooCommerce plugin must be installed before you install this plugin.

This plugin requires WordPress CRON jobs to be enabled. If CRON jobs are not enabled, currency exchange rates will not be updated and this plugin will not be able to search for HIVE payment records. If your exchange rates are not updating or if orders were paid for but still say "Payment Pending" or are automatically canceled, it is likely that CRON jobs are not enabled on your server or are not functioning properly.

Order payments should normally be reflected in the order automatically within 5-10 minutes max. If the order is is still status Payment Pending or becomes cancelled more than 10-15 minutes, it is likely that your CRON jobs are not enabled.

An alternative to using WordPress CRON jobs is setting up a real Crontab. A real Crontab is more efficient than using WordPress CRON jobs, and so you may prefer this approach. You can find instructions for setting up a real Crontab here: https://helloacm.com/setting-up-a-real-crontab-for-wordpress/

= Security Note =
You will <strong>NOT</strong> be required to enter any steem private keys into this plugin. You only have to provide your steem username so that the plugin knows where payments should be sent.

= Thanks =
* Special thanks to [@ReCrypto](https://peakd.com/@recrypto) and [@sagescrub](https://peakd.com/@recrypto) for being the authors of the original "WooCommerce Steem Payment Method" plugin before it was forked and updated into this plugin "WooCommerce Hive Payment Method".

= Disclaimer =
Authors claim no responsibility for missed transactions, loss of your funds, loss of customer funds, incorrect or delayed exchange rates or any other issue you may encounter as a result of using this plugin. Use this plugin at your own risk.

== Installation ==

1. Upload the plugin files to the `/wp-content/plugins/woocommerce-hive-payment-method` directory, or install the plugin through the WordPress plugins screen directly.
2. Activate the plugin through the 'Plugins' screen in WordPress
3. Turn on Hive as a payment method in WooCommerce->Settings->Payments. Turn on the "Enabled" switch.
4. Update settings for this plugin in WooCommerce->Settings->Payments and clicking "Manage" next to "Hive"
5. Make sure to put your Hive username in the "Payee" box so that you will receive payments.

== Frequently Asked Questions ==

= How is customer payment made? =
When the customer initiates payment the HiveSigner window will be opened. HiveSigner will be populated with the payment amount, currency and memo. The automatically generated memo is a random key that is matched to the order.

= How does it confirm Hive Transfers? =
It uses queries the store's HIVE wallet history every 2 minutes to and checks for a transaction that matches the payment MEMO, amount and currency (HIVE or HBD). When the matching payment is found, the order is marked from "payment pending" to "processing".

= What is the payment reminder email? =
If the customer does not complete the payment via HiveSigner within several minutes of initiating the payment, a confirmation email will be sent reminding the customer to make payment manually via Hive. The payment reminder email will include instructions including the memo.

= How can I support this plugin? =
Please support me by following me on Hive [@roomservice](https://peakd.com/@roomservice) and consider voting me for your witness, that would really help a lot on my future efforts with this plugin.

Hive: @roomservice
Discord: @roomservice#8215

== Screenshots ==

1. Product page showing optional exchange rate below product price.
2. Hive payment method option on checkout page. Customer can choose between HIVE or HBD currencies. Exchange rate from FIAT is calculated automatically.
3. HiveSigner for processing payment. Note memo that is provided will be used to match the order.
4. Payment not received reminder email.
5. Payment method in WooCommerce
6. Settings for this plugin within WooCommerce Payments Settings

== Changelog ==

= 1.3.0 - 2020-6-10 =
* Added HIVE-ENGINE token support

= 1.2.0 - 2020-6-3 =
* Forked and migrated to Hive Blockchain

= 1.1.5 - 2019-7-27 =
* The rate of time for checking matching transaction history is changed to be frequent when the order is first placed, and then gradually less frequent.

= 1.1.4 - 2019-7-24 =
* Fixed bug with Steem price displayed in cart for YITH WooCommerce Subscription renewals

= 1.1.3 - 2019-7-15 =
* Added support for YITH WooCommerce Subscription plugin subscription renewals

= 1.1.1 - 2019-4-26 =
* Tweaked variable price range to display STEEM/SBD currency symbol only once instead of twice.

= 1.1.0 - 2019-3-16 =
* Added two new crypto exchanges to query for STEEM/SBD exchange rates. Now a total of three exchanges are queried: Binance and Bittrex. The rates are averaged.

= 1.0.19 - 2019-3-8 =
* Reduced the time of checking for matching transaction history from 5 minutes to 2 minutes.
* Added filter for setting the transaction memo
* Added admin option to show discounted price in STEEM/SBD. If enabled products that are on sale will display the original price in STEEM/SBD with strikethrough.

= 1.0.18 - 2019-1-23 =
* Added error handling for querying steem transfer history
* Tweaked querying steem transfer history to prevent unneeded usage of API

= 1.0.17 - 2019-1-3 =
* Updated Readme files

= 1.0.16 - 2018-12-22 =
* Added order note for payment requested including exchange rate, from and to amounts and currencies.

= 1.0.15 - 2018-12-20 =
* Revived international currency rates conversion using Exchange Rates API (exchangeratesapi.io)

= 1.0.14 - 2018-12-19 =
* Fixed bug detecting payment

= 1.0.13 - 2018-12-19 =
* Removed direct access to properties on WC_Order and WC_Cart objects

= 1.0.12 - 2018-12-17 =
* Added currency symbol (STEEM/SBD) on the checkout page next to the amount that is displayed.
* Added apply_filters on payee steem username
* Added payee steem username on order memo for steem transaction
* Tweaked formatting/markup for STEEM/SBD prices that appear with products

= 1.0.11 - 2018-12-14 =
* Fixed cron event not being created for updating the exchange rates between fiat and STEEM/SBD

= 1.0.10 - 2018-10-23 =
* Updated deprecated WooCommerce functions

= 1.0.9 - 2018-10-23 =
* Updated pending payment emails to use WC_Email class for sending

= 1.0.8 - 2018-10-22 =
* Fixed order receipt not displaying steem transaction details correctly.

= 1.0.7 - 2018-10-10 =
* STEEM, SBD currencies now allowed as WooCommerce store currency.
* Sending payment to same STEEM wallet will now register as payment received. Helpful for testing order flow.

= 1.0.6 - 2018-09-05 =
* New version in WordPress Plugin Repository named "WooCommerce Steem Payment Method" (forked from WooCommerce Steem)
* Added auto payment reminder email
* Added SteemConnect into payment flow
* Updated the auto payment matching feature to use a different API since previous API (SteemSQL) is no longer freely available
* Fixed Null reference error that would not show exchange rate for order total when the checkout page first loads.

