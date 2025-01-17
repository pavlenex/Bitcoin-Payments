# Invoice

An **invoice** is a time-stamped commercial document that maintains a records of a transaction between a buyer and a seller. Issued by the seller, an invoice establishes obligation on buyer's part to pay for products or services listed on the invoice. Seller's obligation is to fulfil the order after the recorded settlement.

An invoices outline payment terms, unit costs, shipping and handling, and any other terms agreed during the transaction. For easier internal and external auditing, an invoice typically has a unique identifier (ID).

The **purpose** of the invoice is:

- To request timely payment from a buyer
- To serve during order fulfillment to a seller
- To help during accounting, troubleshooting and audits

**Invoicing in Bitcoin** isn't different from a traditional invoicing process. When generated, Bitcoin invoice should provide a way for customer to review order information and pay. For seller an invoice is used for recording a payment, fulfilling the order and troubleshooting an issue. 

![Invoice flow](/Assets/img/Elements/Invoice/SimpleInvoiceFlow.png)

## Categorization

* Buyer's invoice (payer)
* Seller's invoice (receiver)

### Invoice for a buyer

The invoice displayed to the buyer should be focused on a smooth payment experience.

#### Buyer's invoice components

The basic components of an invoice visible to the buyer are:

* QR Code with encoded amount and receiving address
* Timer which sets invoice to expired (to avoid volatility in rates)
* Invoice details (Total Price in fiat, Exchange rate, etc)
* Total amount and an address that can be copied separately (for wallet desktop users)
* Open in a wallet (Pay in a wallet) a button that opens and auto-populates sender's wallet fields

![Components of an invoice visible to buyer](/Assets/img/Elements/Invoice/InvoiceScanTab.png)

![Components of an invoice visible to buyer](/Assets/img/Elements/Invoice/InvoiceCopyTab.png)

##### Invoice QR Code

https://github.com/peakshift/bitcoin-ux/blob/master/payments/qr-codes.md#qr-code

##### Invoice Timer

Due to volatility in price, invoice generating softwares aim to lock a particular exchange rate into a certain time-interval (usually 15 minutes). By providing a time-window for invoice payment, you're protecting receiver from price manipulation attack that sender may attempt. 

The invoice timer should clearly indicate a sense of urgency to pay an invoice before the timer expires.

##### Invoice details

When buyer makes a purchase and goes to the checkout, it's reasonable to assume that they'd want to review their invoice details prior to commiting to a purchase. In the invoice detail, it is good practice to show invoice amount, network fee, etc.

![Components of an invoice visible to buyer](/Assets/img/Elements/Invoice/InvoiceScanTabInvoideDetails.png)

![Components of an invoice visible to buyer](/Assets/img/Elements/Invoice/InvoiceCopyTabInvoideDetails.png.png)

##### Pay from a wallet button

### Invoice for a seller

#### Seller's invoice components

The invoice that’s appearing on merchant end needs to provide data relevant for:

* Verifying the payment
* Fulfilling the order
* Troubleshooting an issue

**Payment verification** is mostly handled by the payment processing software. In case of a problem with the payment, the payment processor notifies the merchant to take certain action,depending on the invoice status.

**Order fulfillment** data is relevant data a merchant needs to have in order to deliver the order. This kind of data is optional, and depends on the e-commerce CMS or the API settings merchant configured.

**Troubleshooting an issue** happens when usually there’s a problem with the payment or retroactively if there’s a need for a refund. Centralized payment processors have their support departments that handle this type of queries for merchants, especially processors that are custodial and convert funds instantly to fiat. The essential data needed here needs to provide information about the payment which would allow merchants an easy way to detect an issue and take action. This usually contains a transaction ID, the amount, the invoice (transaction/transactions) status.

## Invoice statuses

Invoice statuses follow the life-cycle of an invoice from newly generated (unpaid) invoice to a paid. Statuses allow you to easier keep a track of 
where every invoice is in their payment life-cycle. Different invoice statuses require different action.

- Unpaid
- Processing
- Paid
- Refunded

##### Data Structure of an invoice

![](/Assets/img/MerchantInvoiceData.png)

Here's an overview of typical data structure on an invoice on the receiver's (merchant's) side.

* A) General Invoice information – contains timestamps, invoice ID, invoice status, etc.
* B) Buyer’s information – optional used for fulfilling the order, the data can be parsed into CMS invoices like WordPress, so merchants don't need to look for this data in BTCPay in case they’re using a CMS.
* C) Product information – optional, used to provide information on what product was purchased.
* D) Invoice summary – provides quick information to quickly troubleshoot an issue or verify the payment manually if that’s needed
* E) Event logs – provide in-depth information about the status of the invoice and it’s transaction on the blockchain.

###### Data Structure - Code examples

```json
{
  "amount": "string",
  "currency": "string",
  "metadata": "string",
  "checkout": {
    "speedPolicy": "HighSpeed",
    "paymentMethods": [
      "string"
    ],
    "expirationMinutes": 0,
    "monitoringMinutes": 0,
    "paymentTolerance": 0
  },
  "id": "string",
  "createdTime": 0,
  "expirationTime": 0,
  "monitoringTime": 0,
  "status": "New",
  "additionalStatus": "None"
}
```
## Invoice Generation Flow

![Invoice Generation Flow](/Assets/img/InvoiceGenerationFlow.png)

## Challenges

- [Address format compatibility](InvoiceProblems.md#paying-from-an-exchange-underpaid-invoice)
- [Underpaid invoices](InvoiceProblems.md#paying-from-an-exchange-underpaid-invoice)
