NEXVORA FF IDs VAULT — Neon Elite

Files
- index.html: entry page
- login.html: sign in / register
- vault.html: active listings and details
- payment.html: listing checkout, dynamic amount QR, UPI app link, UTR submission (no screenshot upload)
- dashboard.html: button-first customer dashboard, username/password changes, orders with protected deletion checks, refund request and refund history
- vault-admin.html: listings, orders/delivery, UTR review, refunds, customer list
- nexvora-elite.css: shared styling

Recent fixes in this package
- Payment submission asks for UTR only; screenshot upload is removed.
- Admin payment review displays UTR and warns about repeated UTRs within the loaded records. Admin must still verify the transaction against the real UPI/bank ledger before approving.
- Refund requests can be submitted for paid/completed orders.
- Deleting a listing with linked order history safely marks it inactive instead of breaking historical orders.
- Existing Supabase URL and publishable key were preserved.

Deploy note
Upload/replace these files in the existing GitHub repository and let the existing Vercel deployment build. No Supabase schema change was made by this ZIP update. Test with a small test order before accepting real payments.

Customer order deletion is intentionally limited to unpaid orders with no payment/refund history; paid/completed financial records are protected. Supabase RLS must allow the signed-in user to delete eligible own orders for that action to succeed.
