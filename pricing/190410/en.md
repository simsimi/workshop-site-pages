<style
  type="text/css">
style {color:#ffffff;display:hidden}
h1, h2, h3, h4, h5, h6 {color:#333333;}
p, li {color:#333333}
code {color:#000080;}
</style>

# Free Credits
SimSimi Workshop provides new individual users with $300 free credit to use with any APIs. We ask you for your credit card to make sure you are not a robot. For service to continue uninterrupted, you must always have a valid payment method associated with your account. The usage cost will be paid from your free credits unless it run out or expire (whichever comes first). For service to continue uninterrupted, you must always have a valid payment method associated with your account.

You might notice a $0-1 transaction from SimSimi Workshop(or payment agency) after you sign up. This transaction:

* Is an authorization request to validate your account, not a permanent charge.
* Might be converted to local currency by your bank.
* Might appear on your statement for up to a month
* Contact your bank if you have questions about the authorization.

# Pricing Policy
The usage cost will be paid from your free credits unless it run out or expire (whichever comes first). If your free credits run out or expire, you only pay for what you use.
We charge you whenever your account reaches your payment threshold, or the end of each month -- whichever comes first. Any amount less than $1 will automatically be carried forward to the next billing cycle. You can understand your current API usage and estimate your monthly bill in the [console](https://workshop.simsimi.com/dashboard). See below for pricing details on each item.


## Smalltalk API
### Personal
* Basic charge : Each successful request will be charged a basic rate of $0.001(USD).
* Additional charges: Following additional charges will apply for each request including Response Control and Additional Information options.

| Type | Parameter | Additional charges (per request) |
| --- | --- | --- |
| Response Control | `country` | $0.0001 (USD) |
| Response Control | `atext_bad_prob_min` | $0.0001 (USD) |
| Response Control | `atext_bad_prob_max` | $0.0001 (USD) |
| Response Control | `atext_length_min` | $0.0001 (USD) |
| Response Control | `atext_length_max` | $0.0001 (USD) |
| Response Control | `regist_date_min` | $0.0001 (USD) |
| Response Control | `regist_date_max` | $0.0001 (USD) |
| Additional Information	 | `country` | $0.0001 (USD) |
| Additional Information	 | `atext_bad_prob` | $0.0001 (USD) |
| Additional Information	 | `atext_bad_type` | $0.0001 (USD) |
| Additional Information	 | `regist_date` | $0.0002 (USD) |
| Additional Information	 | `qtext` | $0.0005 (USD) |


* Pricing examples : 
If there are 10,000 successful requests, of which 3,000 requests have the `atext_bad_prob_max` and 1,000 requests have the `country` and the `regist_date`, the rate is calculated as follows:
```
Basic Charge                                 : 10,000  * $0.001  = $10
Response Control(atext_bad_prob_max)         :  3,000  * $0.0001 = $ 0.3
Additional Information(country)              :  1,000  * $0.0001 = $ 0.1
Additional Information(regist_date)          :  1,000  * $0.0002 = $ 0.2
-------------------------------------------------------------------------
Total                                        :                     $10.6
```
If the above example is the usage of the month you received the free credits, then all the charges will be paid from your free credits and the remaining free credits will be used to pay for the API fee next month.
```
$300.0 - $10.6 = $289.4 (USD)
```
### Business
* Please contact our sales team for plans for organization or business customers. (api@simsimi.com)

# Payment Threshold
After your free credit run out or expire, your usage cost will be charged based on payment information, such as a credit card number you set. You can think of your billing threshold as a way to build up a good payment history with SimSimi Workshop: It's an amount you can spend on the service before we charge you for them. Whenever your ad costs reach your billing threshold, we'll charge you for that amount. When you first start using on SimSimi Workshop, your billing threshold will be automatically set to a small amount. But as you make successful billing threshold payments, it may be raised until your account reaches a final threshold amount.

As an example, let's say you just created your first project, and your account has a billing threshold of $10. As you use the service, it'll accrue costs. If your outstanding costs reach $10, we'll charge you $10. Once your payment goes through, your balance will be cleared, this paid amount is shown as a prepaid amount. Your billing threshold may be raised to a new, higher amount

So in a given month, you could reach your billing threshold once, multiple times or not at all, depending on what your billing threshold is and how much money you're spending on services. This is also why you may be charged multiple times before the automatic payment date.
