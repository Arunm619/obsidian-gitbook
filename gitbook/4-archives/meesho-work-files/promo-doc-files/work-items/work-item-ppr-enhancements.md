#### Situation:
The Payment Page in the Meesho App required a revamp to improve user experience. To achieve this, we tried to enhance the visibility of Bank Offers, introduce badges for available offers, integrate Buy Now, Pay Later (BNPL) offers, automate offer application by simple tap, and improve the overall Payment Page structure and others.

#### Tasks:

##### Bank Offers V2 - Showing Ineligible Offer Items:
Display Bank Offers for users with Cart Value < MOV with a notification to add items worth ₹X to avail the offer.


##### Add Offer Available Badges:
Added badges to highlight the availability of offers, improving user awareness.

##### Add BNPL Offers:

Integrated Buy Now, Pay Later (BNPL) offers, expanding the range of payment options.

##### Offer Auto-Application:
Implemented auto-application of offers to streamline the user experience.

##### Sticky Scrolling of Payment Header Tab:
Introduced sticky scrolling for the payment header tab to address concerns related to the new flow's impact on Payment Page to Order Conversion.

##### Add Lottie Animations in Header Tab:
Enhanced visual appeal with Lottie animations in the header tab.


##### Add Offers For You Section:
Integrated a personalized "Offers For You" section for tailored recommendations.

##### Breakdown PPR Viewmodel into Small Sub Viewmodels:
Improved code readability and understanding by breaking down the PPR Viewmodel.

##### Add Onboarding Flow to PPR:
Introduced an onboarding flow to help users, especially Cash on Delivery (COD) users, understand the new tab structure.

##### PPR Tab Restructuring:
Addressed challenges faced by COD-only users through an onboarding flow.
Users are guided to choose a payment method with a translucent cover and tooltip.
Flash animation added to the tooltip for emphasis.
Sunset logic implemented to show the flow until the user places an order or sees the complete flow.

##### PPR Tab Animations:
Introduced the option to add animated gifs to Pay Online and Cash on Delivery tabs via backend control.
Users with the animation flag enabled see gifs; otherwise, default static icons are displayed.

#### Actions

Collaboration with cross-functional teams, including design, development, and data analysis.
Implementation of features and optimizations based on user behavior analysis.


#### Results
Enhanced visibility of Bank Offers for eligible users.
Improved user awareness through offer badges.
Expanded payment options with BNPL integration.
Streamlined user experience with auto-application of offers.
Improved visual appeal and navigation with sticky scrolling and animations.
Addressed challenges faced by COD-only users through onboarding and restructuring.