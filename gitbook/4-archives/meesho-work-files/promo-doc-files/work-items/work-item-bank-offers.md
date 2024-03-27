##### Situation
Meesho is introducing a new feature related to bank offers for Android users. This feature involves the use of JusPay Offers List API, where users can avail discounts or cashbacks based on their payment methods.

##### Task
The primary task involves implementing changes in the payment screen to display and apply offers effectively for Android users. This includes handling various scenarios like payment instrument selection, card additions, and dynamic updates based on offers.

##### Action

###### Payment Screen Changes:

Display offers available text based on payment modes (UPI, Wallet, Card, NetBanking).
Implement logic for showing or hiding offers based on eligibility.
If a user clicks on a payment option, show offer descriptions and terms except for cards.

###### Cards:

Change "Add new Card" text to "Add new Card and check offers" if Card Payment mode has offers.
Show Card Offer Description & TNC if a card with an applicable offer is selected.
Dynamically update offer text and call cart/paymentInfo with offer details.
Bank Offers:

###### Display bank offers on the Add Card screen.
Update the cart/paymentInfo with bank offer details when selected.

###### Terms & Condition Bottom Sheet:

Launch a bottom sheet with terms and conditions when users click on TnC.

###### Edge Case Handling:

Handle scenarios where cart value changes (e.g., Meesho Credits deselection, product unavailability).
Detect changes in the cart and request updated amounts from the backend.
Update the offers data and call cart/paymentInfo with no selected payment options.

###### VPA Flow:

Implement a debounced behavior for UPI ID entry, triggering JusPay Offer List API.
Update UI based on offer applicability for UPI.

###### New Card Flow:

Fetch offers associated with added cards using JusPay Offer List API.
Update UI text and details based on offer applicability.

###### Offer Redemption Comms:

Ensure BE-driven flow for offer redemption communications.

###### Result
The payment screen for Android users will now effectively display and apply relevant offers based on user actions, enhancing the user experience and increasing engagement with bank offers.