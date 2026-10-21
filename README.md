# NEXVORA FF IDs VAULT — Neon Elite

## Files
- `index.html`: entry page
- `login.html`: sign in / register
- `vault.html`: active listings and details
- `payment.html`: listing checkout, dynamic amount QR, UPI app link, UTR submission (no screenshot upload)
- `dashboard.html`: button-first customer dashboard; username/password, orders, eligible order deletion, refund requests/history, policy and support
- `vault-admin.html`: listings, orders/delivery, UTR review, refunds, customer policy controls, editable website policy
- `nexvora-elite.css`: shared styling

## Customer dashboard behavior
- The dashboard menu is the first view. Orders/refunds load only after the customer taps the relevant button.
- Every section has a Back to Dashboard action.
- Order deletion is restricted to eligible unpaid orders with no payment/refund history; payment/refund history is protected.
- Refund requests require a paid/completed order and an approved payment record, reject duplicate active refund requests, and appear in My Refunds with the current status.
- The customer can view the current policy and their policy warning/ban history.
- A banned account is blocked from protected profile/order/payment/refund/delivery actions by Supabase row-level security. The customer can still access the policy/support UI.

## Admin policy controls
- `vault-admin.html` includes a POLICY tab to edit the customer-facing website policy.
- CUSTOMER management supports a warning, manual ban, and unban/reset. The first warning marks the account warned; a second warning automatically bans it from protected website actions.
- Policy actions are stored in `customer_policy_events`; account state is stored in `customer_account_controls`.
- Existing listings, orders, payment submissions, refund requests, profiles, and delivery records are retained.

## Refund and payment safety
- Payment submission asks for the UTR only; no screenshot upload is collected by this flow.
- Admin must verify the UTR against the actual bank/UPI transaction ledger before approving payment.
- Refund requests are reviewed against the original order and approved payment record. This package does **not** charge a separate ₹350 fee merely to allow a customer to submit a refund request; do not ask customers to pay an undisclosed fee to unlock a refund.

## Supabase
The existing Supabase project was updated additively with migrations:
- `add_vault_policy_and_customer_controls`
- `allow_safe_customer_order_deletion`
- `harden_customer_account_gate_function`

These migrations add policy/account-control tables and safe order-delete permissions; they do not delete or reset existing customer, listing, order, payment, refund, or delivery data.

## Deploy note
Upload/replace the site files in the existing GitHub repository and let the existing Vercel deployment build. Supabase changes have already been applied to the existing `nexvora-ff-ids-vault` project. Test customer dashboard, admin policy controls, a test order, and a refund request before taking live payments.
