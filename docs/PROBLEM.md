# PROBLEM

## Business context
Bomberna is a family-run garden centre / florist business in Maldegem, Oost-Vlaanderen,
Belgium. Part of the operation is a stall at a weekly farmers market: Wednesdays and
Saturdays, one fixed location. Revenue is strongly seasonal (summer high, winter low,
Easter is a notable peak). The business sells flowers and plants both to walk-up private
customers and to companies that need a proper invoice for their accounting.

## Who uses the tool
- The person at the stall (currently Victor, helping out over summer) on a phone.
- The administration office back at the business, who receive invoice requests and raise
  the formal invoices.

## The two problems

### 1. Tracking market performance
There is no quick, structured way to record how each market day went. The owner wants to
see revenue per market over time, compare days (Wednesday vs Saturday), and see seasonal
patterns (summer, Easter). Currently this is not captured systematically.

### 2. Capturing B2B invoice requests at the stall
When a company buys flowers and needs an invoice for their books, the stall person must
collect the company details and pass them to the admin office, who then create the formal
invoice. Doing this on paper or by memory is slow and error-prone, and the admin office
often lacks the full set of details needed to actually raise the invoice (notably the
amount and a description of what was sold, not just who the customer is).

## Constraints that shape the design
- **Phone, at a stall, possibly one-handed.** Fast entry matters.
- **Signal can be poor at the market.** The capture step must work offline. Sending
  (email) can wait until signal returns.
- **Belgian B2B invoicing.** A company customer is identified by an ondernemingsnummer
  (format `BE 0XXX.XXX.XXX`); the VAT (btw) number is normally `BE` + that number. The
  formal invoice is the admin office's responsibility, not the stall's.
- **Low maintenance.** This is an internal tool for a small family business, not a product.
  Avoid infrastructure that needs ongoing babysitting unless it clearly pays for itself.
