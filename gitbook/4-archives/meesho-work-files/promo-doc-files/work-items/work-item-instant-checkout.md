#### Situation
The Buy Now Flow, a vital element in the Multi-Supplier Cart system, encounters optimization and scalability challenges, impeding its efficacy for instant buying and future enhancements.

#### Task
Revamp the Instant Checkout Flow to enhance user experience and minimize perceived effort by reducing the 3 step to a 2 two step process.

#### Action
Redirect the user to the existing Cart Page instead of the Address page.
Modify the Checkout Progress Bar to showcase two steps: Review and Payment.
Update animation files and URLs for the progress bar.
Retain the existing Product Detail section with the option to modify product details.
Introduce a new icon and handle the edge case where the default address is unserviceable.
Implement a snackbar for error messages related to unserviceable addresses.
Clicking "Continue" should direct the user to the Payment Screen.
Change the primary CTA to "Place Order" if no Payment Option is selected.
If the user selects an Online Payment Option, change the primary CTA to "Pay Now."


#### Result
The foremost advantage of the revamped Instant Checkout Flow, especially in Variant 1, is the substantial acknowledgment that 90% of orders are placed via the Buy Now flow. This underscores the significance of optimizing this particular pathway. The redesign aims to streamline the process, reducing the number of pages from 3 (Address, Payment, Summary) to 2 (Review Cart, Payment Summary). This optimization is poised to significantly expedite the order placement for the majority of users who prefer the Buy Now flow.