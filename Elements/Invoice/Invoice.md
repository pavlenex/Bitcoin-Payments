# Invoice

An **invoice** is a time-stamped comercial document that maintains a records of a transaction between a buyer and a seller. Issued by the seller, ab invoice establishes obligation on buyer's part to pay for products and services listed on the invoice. On seller's end obligation is to fulfil the order after the recorded settlment.

An invoices outline payment terms, unit costs, shipping and handling, and any other terms agreed during the transaction. For easier internal and external auditing, an invoice typically has a unique identifier (ID).

The **purpose** of the invoice is:

- To request timely payment from a buyer
- To serve during order fulfilment to a seller
- To help during accounting, troubleshooting and audits

## Categorization

* [Buyer's invoice (payer)](InvoicePayer.md)
* [Seller's invoice (receiver)](InvoiceReceiver.md)

### Invoice for a buyer

The invoice displayed to the buyer should be focused on smooth payment experience. This means clear instructions on how to pay a generated Bitcoin invoice.

#### Buyer's invoice components

The basic components of an invoice visible to the buyer are:

* A) QR Code with encoded amount and receiving address
* B) Timer which sets invoice to expired (to avoid volatility in rates)
* C) Invoice details (Total Price in fiat, Exchange rate, etc)
* D) Total amount and an address that can be copied separately (for wallet desktop users)
* E) Open in a wallet (Pay in a wallet) a button that opens and auto-populates sender's wallet fields

![Components of an invoice visible to buyer](/Assets/img/InvoicesViewBuyerSide.png)

##### Invoice QR Code

https://github.com/peakshift/bitcoin-ux/blob/master/payments/qr-codes.md#qr-code

##### Invoice Timer

Due to violatility in price, invoice generating softwares aim to lock a particular exchange rate into a certain time-interval (usually 15 minutes). By providing a time-window for invoice payment, you're protecting receiver from price manipulation attack that sender may attempt. 

The invoice timer should clearly indicate a sense of urgency to pay an invoice before the timer expires.

##### Invoice details

When buyer makes a purchase and goes to the checkout, it's resonable to assume that they'd want to review their invoice details prior to commiting to a purchase. In the invoice detail, it is good practice to show invoice amount, network fee, etc.

##### Pay from a wallet button

### Invoice for a seller

## Challenges

- [Address format compatibility](InvoiceProblems.md#paying-from-an-exchange-underpaid-invoice)
- [Underpaid invoices](InvoiceProblems.md#paying-from-an-exchange-underpaid-invoice)