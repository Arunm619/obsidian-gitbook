| Name            | Arun Sudharsan M                |
| --------------- | ------------------------------- |
| Designation     | Software Development Engineer 2 |
| Team            | Transact - Android              |
| Pod             | Prepaid Adoption                |
| Manager         | Naveen Kumar AV                 |
| Date of Joining | Nov 03, 2021                    |
### Work Items
- [[#Animated Sticky CTAs in PDP|Animated Sticky CTAs in PDP]]
- [[#App Shortcuts|App Shortcuts]]
- [[#Widgets to Cart Page using SDUI|Widgets to Cart Page using SDUI]]
- [[#Unit Testing|Unit Testing]]
- [[#Outage Warning|Outage Warning]]
- [[#Bank Offers|Bank Offers]]
- [[#Instant Checkout|Instant Checkout]]
- [[#PPR Enhancements|PPR Enhancements]]
- [[#Checkout Modularisation|Checkout Modularisation]]
- [[#Remove NON-MSC code|Remove NON-MSC code]]
- [[#Safe Commerce Fraud Awareness|Safe Commerce Fraud Awareness]]
- [[#Migrate Order Place to Kotlin|Migrate Order Place to Kotlin]]
- [[#Gender Input From User|Gender Input From User]]
### Animated Sticky CTAs in PDP
##### Situation
To enhance the user experience, we implemented dynamic smooth animations for the crucial "Add to Cart" and "Buy Now" buttons in the Meesho supply-android app's in Product Display Page (PDP). These buttons, utilised in the order of millions of times daily, reside in this complex PDP source code.
##### Task
To simplify the logic and improve code readability, we decided to create a library component within the mesh-android package, incorporating a finite state machine model. This would facilitate managing various states and transitions, focusing on animation and view rendering in the Animated Sticky Button Views.
##### Action
We meticulously studied states and events, introducing a finite state machine to handle the complexity. Defined states include Initial View, Potential Add to Cart Product View, Added To Cart View, Potential Immediate Buy Views, each with corresponding events to ensure smooth transitions.
##### Result
The Animated Sticky Button Views now seamlessly guide users through different states—enhancing user interaction, reducing complexity in code maintenance, and providing a structured foundation for future changes and improvements with 100% test coverage.
#### Competencies Achieved
- Coding & Problem Solving
- User first
- Problem first mindset
- Hire and grow exceptional talent
#### Reasoning
The implementation of animated sticky CTAs required advanced coding skills and problem-solving to ensure smooth transitions and user interactions. Prioritising the user experience and addressing challenges with a problem-first mindset were crucial aspects of this task. The state machine based animation approach was presented in android weekly tech sessions to share the knowledge and grow exceptional talent of the team.
#### Links
* Solutioning Doc Link: [Animated Sticky CTAs Solutioning Doc](https://docs.google.com/document/d/1HoV0VBZrKawCWqvDQyk707fY67h3F-NNd6JSId-XbMg/edit)
* PR Link: 
	1. [Animated Sticky CTAs mesh-android PR](https://github.com/Meesho/mesh-android/pull/208)  
	2. [Animated Sticky CTAs integration in supply-android PR](https://github.com/Meesho/supply_android/pull/3337)
* Presentation:
	1. [Deck](https://docs.google.com/presentation/d/1M8bUI2KfDoWkJ3HWBrU5AS2TBBrsGNundo1xhaFhGdk/edit?usp=sharing)
	2. [Recording](https://drive.google.com/file/d/1FL1-E3KlXfiaK8XxeWPTvc2MI38IrZrD/view?usp=sharing)

### App Shortcuts
##### Situation
Recognising a potential enhancement in our app's functionality—specifically, the absence of shortcuts—highlighted an opportunity to improve user engagement. The current lack of quick feature accessibility posed a challenge, sparking interest in exploring a strategic solution.
##### Task
To address this challenge, I initiated the development of the Android Shortcuts feature. With a focus on enhancing user engagement, I ideated, developed, and successfully implemented static and dynamic shortcuts. The goal was to recover and boost user engagement that had been impacted by the previous absence of this critical feature.
##### Action
The execution involved meticulous integration of dynamic shortcuts, tailored to individual user preferences based on the login state. Inspiration from competitors led us to add personalised content like "For You" and "Open Cart" shortcuts. This creative touch played a key role in enhancing the user experience.
##### Result
The Android Shortcuts feature, now accessible to 100% of our users, has effectively addressed the initial challenge. Users can swiftly access key features directly from the launcher, significantly enhancing user engagement and overall satisfaction. This strategic enhancement underscores our commitment to continuous improvement and user-centric innovation, positioning our app for sustained success in a competitive landscape.
#### Competencies Achieved
- Planning, Delivery & Stakeholder Management
- User first
- Bold Experimentation
#### Reasoning
Strategically planning and delivering the Android Shortcuts feature demonstrated effective stakeholder management. Prioritising user needs and experimenting with new features showcased a bold approach to innovation.
#### Links
* PR Link: [App Shortcuts PR](https://github.com/Meesho/supply_android/pull/5919)  
* Solutioning Doc Link: [App Shortcuts Solutioning Doc](https://meesho.atlassian.net/wiki/spaces/EW/pages/2517860689/Android+Shortcuts+-+WIP)
* Success Metrics: [Mixpanel Dashboard](https://mixpanel.com/project/1155510/view/98871/app/boards#id=4969979)

### Widgets to Cart Page using SDUI
##### Situation
Within the checkout module, a strategic assessment identified an under-utilized opportunity in the cart page for both "Buy Now" and "Add to Cart" flows. Specifically, there was unexplored real estate at the bottom of the screen that could enhance user engagement. Consequently, a decision was made to integrate dynamic widget functionality into these pages, leveraging this untapped potential.
##### Task
The task at hand was the seamless integration of dynamic widgets through the adoption of the newly introduced Velocity Widget based on Server Driven UI development principles. This approach was chosen for its real-time flexibility, allowing content and layout modifications without necessitating frequent app updates. The primary objective was to showcase various types of supported widgets, with configurability managed from the backend, effectively optimising the available space on the cart page.
##### Action
Our solution involved the incorporation of banners as dynamic widgets on the designated pages. While the initial focus was on banners, the design adhered to SDUI principles, ensuring adaptability for future expansions encompassing various widget types, all dynamically configured from the backend.
##### Result
The implementation successfully introduced banners as dynamic widgets on the cart page and the instant checkout review cart page. The application of SDUI principles ensures not only immediate success but also provides a robust foundation for ongoing optimisation and experimentation, ensuring continued enhancement of user engagement on these critical pages. The achievement was notable for its efficiency, aligning with project timelines with 100% test coverage.
#### Competencies Achieved
- Planning, Delivery & Stakeholder Management
- User first
- Bold Experimentation
- Architecture & Design
#### Reasoning
Strategic planning and delivery were crucial in integrating SDUI-based widgets, prioritising user-centric design, bold experimentation with new technology, and ensuring a robust architectural foundation for future expansions.
#### Links
* PR Link: [Widgets to Cart Page PR](https://github.com/Meesho/supply_android/pull/7044)
* Solutioning Doc Link: [Widgets to Cart Page Solutioning Doc](https://meesho.atlassian.net/wiki/spaces/EW/pages/2993225979/Dynamic+Widgets+in+Checkout+flow)
### Unit Testing
##### Situation
The Transact module has a 2% unit test coverage, posing risks to code reliability. During the code freeze period, a crucial initiative is to augment unit tests significantly, aiming for a 20% coverage.
##### Task
The task involves crafting comprehensive unit tests for Transact module source code, with a ten-fold increase in coverage during the code freeze. The goal is not just numerical, but to enhance code quality, identify potential issues, and fortify the module's robustness.
##### Action
The action plan includes identifying critical functionalities, creating meaningful test cases, and ensuring effective test coverage. The focus is on meaningful tests that contribute to code reliability and act as living documentation.
##### Result
The result is a Transact module with 20% unit test coverage, providing code reliability. Unit tests serve as documentation, aiding understanding and early bug detection. The impact encompasses improved code quality, confident refactoring, regression prevention, and increased developer productivity.
#### Competencies Achieved
- Testing, Scaling & Security
- Operational Excellence & Documentation
#### Reasoning
Crafting comprehensive unit tests showcases a commitment to testing, scaling, and securing the codebase. It also demonstrates operational excellence through thorough documentation, ensuring robust and reliable code.
#### Links
* PR Link: [Unit Testing PRs](https://github.com/Meesho/supply_android/pulls?q=is%3Apr+author%3Aarunsudharsan+label%3Aandroid-ut-marathon+label%3Aunit-tests+)
* Coverage Report: [Tracker](https://docs.google.com/spreadsheets/d/1Fm74DEwI7x2Fm4yFDSHdD9o60fKOgzy43LFRgsCEB2w/edit?usp=sharing)
### Outage Warning
##### Situation
As an e-commerce app with a significant user base and high daily transaction volume, we identified a critical challenge related to payment outages. The absence of a detailed incident response plan and proactive customer communication during payment outages posed a potential risk to user satisfaction and transaction success. This prompted the need for a strategic solution to address these deficiencies and enhance the app's resilience to payment outages.
##### Task
To tackle this challenge, our focus was on two key aspects: the development of a comprehensive incident response plan and the establishment of proactive customer communication strategies during payment outages. The task involved understanding the current state of payment option display on Android, optimising the frequency of API hits to Juspay for outage information, and determining how to convey payment failures effectively to users.
##### Action
The execution involved in-depth collaboration between the transact team and Juspay. We analysed the current Android payment option display process, delved into Juspay's APIs, and formulated a set of open questions to gather essential information. We proposed a refined testing schedule for payment processes, developed a plan for conveying outage messages to users based on Juspay's outage data, and sought answers to critical questions from both Juspay and the Transact backend.
##### Result
The result is a comprehensive solution that addresses the identified deficiencies. By implementing a refined incident response plan, optimising the frequency of API hits to Juspay, and formulating a strategy for conveying outage messages to users, we aim to enhance our app's resilience to payment outages. This strategic approach aligns with our commitment to providing a seamless user experience, minimising disruptions, and maintaining user trust in our e-commerce platform.
#### Competencies Achieved
- Planning, Delivery & Stakeholder Management
- Operational Excellence & Documentation
#### Reasoning
Developing a comprehensive incident response plan and optimising API hits demonstrate planning, delivery, stakeholder management, and operational excellence. Documentation ensures transparency and efficient collaboration in addressing challenges.
#### Links
* PR Link: [Outage Warning PR](https://github.com/Meesho/supply_android/pull/6797)
* Solutioning Doc Link: [Outage Warning Solutioning Doc](https://docs.google.com/document/d/1lK_s-vThqNFCS5q6cYeDiRPVhWzkYQDInyzbTCX23fI/edit?usp=sharing)
### Bank Offers
##### Situation
Meesho is introducing a new feature related to bank offers for Android users. This feature involves the use of JusPay Offers List API, where users can avail discounts or cashbacks based on their payment methods.
##### Task
The primary task involves implementing changes in the payment screen to display and apply offers effectively for Android users. This includes handling various scenarios like payment instrument selection, card additions, and dynamic updates based on offers.
##### Action
- Payment Screen: Show text for available offers based on payment modes; dynamically hide/show offers based on eligibility; display offer details/terms on payment option click.
- Cards: Modify "Add new Card" text based on card payment offers; show offer details if a card with an applicable offer is selected; update offer text and call cart/paymentInfo with details.
- Bank Offers: Display bank offers on Add Card screen; update cart/paymentInfo with bank offer details on selection.
- Terms & Condition Bottom Sheet: Launch bottom sheet with TnC on click.
- Edge Case Handling: Manage cart value changes, detect changes, and update offers data; call cart/paymentInfo with no selected payment options.
- VPA Flow: Implement debounced behavior for UPI ID entry, trigger JusPay Offer List API, and update UI based on offer applicability for UPI.
- New Card Flow: Fetch offers for added cards using JusPay Offer List API; update UI based on offer applicability.
- Offer Redemption Comms: Ensure BE-driven flow for offer redemption communications.
##### Result
The payment screen for Android users will now effectively display and apply relevant offers based on user actions, enhancing the user experience and increasing engagement with bank offers.
#### Competencies Achieved
- Coding & Problem Solving
- Testing, Scaling & Security
#### Reasoning
Implementing complex logic for displaying and applying offers involves strong coding and problem-solving skills. Additionally, ensuring the system handles various scenarios contributes to testing, scaling, and security aspects. Implemented this in pre-headless, headless and PPR flows.
#### Links
* PR Links: 
	1. [Pre-headless](https://github.com/Meesho/supply_android/pull/4340)
	2. [Headless](https://github.com/Meesho/supply_android/pull/5323)
	3. [PPR Enhancements](https://github.com/Meesho/supply_android/pull/5750)
* Solutioning Doc Link: [Bank Offers Solutioning Doc](https://meesho.atlassian.net/wiki/spaces/EW/pages/2775451888/Bank+offers+-+Headless+SDK+version+Solutioning)
### Instant Checkout
##### Situation
The Buy Now flow in the Multi-Supplier Cart system faces challenges in optimisation and scalability, affecting its efficiency for instant purchases and future improvements.
##### Task
Revamp the Instant Checkout Flow to enhance user experience and minimise perceived effort by reducing the 3-step process to a 2-step process.
##### Action
- Redirect the user to the existing Cart Page instead of the Address page.
- Modify the Checkout Progress Bar to showcase two steps: Review and Payment.
- Retain the existing Product Detail section with the option to modify product details.
- Introduce a new icon and handle the edge case where the default address is unserviceable.
- Implement a snackbar for error messages related to unserviceable addresses.
- Clicking "Continue" should direct the user to the Payment Screen.
- Payment page in the legacy buy now flow should become the payment summary page in the instant checkout flow thereby making it the last step in the checkout.
- Address page should now be gone and should become a bottom sheet in the review cart page.
##### Result
The foremost advantage of the revamped Instant Checkout Flow is the substantial acknowledgment that 90% of orders are placed via the Buy Now flow. This underscores the significance of optimising this particular pathway. The redesign aims to streamline the process, reducing the number of pages from 3 (Address, Payment, Summary) to 2 (Review Cart, Payment Summary). This optimisation is poised to significantly expedite the order placement for the majority of users who prefer the Buy Now flow.
#### Competencies Achieved
- Planning, Delivery & Stakeholder Management
- Coding & Problem Solving
- Operational Excellence & Documentation
#### Reasoning
Successfully revamping the Instant Checkout Flow involves meticulous planning, efficient coding, and ensuring operational excellence. Documenting the changes contributes to operational excellence and documentation competency.
#### Links
* PR Link: [Instant Checkout PRs](https://github.com/Meesho/supply_android/pulls?q=is%3Apr+author%3Aarunsudharsan+instant+checkout+is%3Aclosed+label%3Ainstant-checkout-transact)
* Solutioning Doc Link: [Instant Checkout Solutioning Doc](https://meesho.atlassian.net/wiki/spaces/EW/pages/2672328717/Instant+Checkout+-+Android+Solutioning)
### PPR Enhancements
##### Situation
The Payment Page in the Meesho App required a revamp to improve user experience. To achieve this, we tried to enhance the visibility of Bank Offers, introduce badges for available offers, integrate Buy Now, Pay Later (BNPL) offers, automate offer application by simple tap, and improve the overall Payment Page structure and others.
##### Tasks
1. **Bank Offers V2 - Showing Ineligible Offer Items:**
   - Display Bank Offers for users with Cart Value < MOV with a notification to add items worth ₹X to avail the offer.
2. **Add Offer Available Badges:**
   - Added badges to highlight the availability of offers, improving user awareness.
3. **Add BNPL Offers:**
   - Integrated Buy Now, Pay Later (BNPL) offers, expanding the range of payment options.
4. **Offer Auto-Application:**
   - Implemented auto-application of offers to streamline the user experience.
5. **Sticky Scrolling of Payment Header Tab:**
   - Introduced sticky scrolling for the payment header tab to address concerns related to the new flow's impact on Payment Page to Order Conversion.
6. **Add Lottie Animations in Header Tab:**
   - Enhanced visual appeal with Lottie animations in the header tab.
7. **Add Offers For You Section:**
   - Integrated a personalised "Offers For You" section for tailored recommendations.
8. **Breakdown PPR Viewmodel into Small Sub Viewmodels:**
   - Improved code readability and understanding by breaking down the PPR Viewmodel.
9. **Add Onboarding Flow to PPR:**
   - Introduced an onboarding flow to help users, especially Cash on Delivery (COD) users, understand the new tab structure.
10. **PPR Tab Restructuring:**
    - Addressed challenges faced by COD-only users through an onboarding flow.
    - Users are guided to choose a payment method with a translucent cover and tooltip.
    - Flash animation added to the tooltip for emphasis.
    - Sunset logic implemented to show the flow until the user places an order or sees the complete flow.
11. **PPR Tab Animations:**
    - Introduced the option to add animated gifs to Pay Online and Cash on Delivery tabs via backend control.
    - Users with the animation flag enabled see gifs; otherwise, default static icons are displayed.
##### Actions
Collaboration with cross-functional teams, including design, development, and data analysis.
Implementation of features and optimisations based on user behavior analysis.
#### Result
Enhanced visibility of Bank Offers for eligible users.
Improved user awareness through offer badges.
Expanded payment options with BNPL integration.
Streamlined user experience with auto-application of offers.
Improved visual appeal and navigation with sticky scrolling and animations.
Addressed challenges faced by COD-only users through onboarding and restructuring.
#### Competencies Achieved
- Planning, Delivery & Stakeholder Management
- Coding & Problem Solving
- Architecture & Design
- Testing, Scaling & Security
#### Reasoning
Executing PPR enhancements required meticulous planning, efficient coding, thoughtful architecture and design, and thorough testing, scaling, and security considerations to ensure a seamless and secure user experience.
#### Links
* PR Links:
	1. [PPR Tab Restructuring](https://github.com/Meesho/supply_android/pull/6917)
	2. [PPR FTUX onboarding experience](https://github.com/Meesho/supply_android/pull/6373)
	3. [Split VMs](https://github.com/Meesho/supply_android/pull/6326)
	4. [Sticky Scrolling of Payments Mode Switcher Tab](https://github.com/Meesho/supply_android/pull/6250)
	5. [PPR Offers Auto Application](https://github.com/Meesho/supply_android/pull/5877)
	6. [Added offers available badge for PPR payment option items](https://github.com/Meesho/supply_android/pull/5786)
### Checkout Modularisation
##### Situation
The majority (80%) of the checkout code has been successfully modularised and moved out of the app module. However, the remaining 20%, consisting of core and base classes for the entire checkout flow, needs modularisation. This step is crucial for achieving a fully modularised checkout system.
##### Task
Identify the usage and dependency of the core classes across the packages, move them to the core checkout module, and ensure functionality remains intact. Resolve dependencies to ensure other dependent packages can seamlessly utilise the modularised core classes.
##### Action 
The action involves a meticulous process of identifying dependencies, relocating core classes to the checkout module, and validating the functionality. Extensive testing and collaboration with development teams ensure a successful transition, resulting in improved developer productivity and reduced build times.
##### Result
Achieved 100% modularisation by moving the remaining core classes out of the app module. This accomplishment not only decreases build times but also significantly improves developer productivity by providing a streamlined and modular codebase.
#### Competencies Achieved
- Coding & Problem Solving
- Architecture & Design
#### Reasoning
The task requires a deep understanding of the existing codebase, its dependencies, and the architectural considerations for successful modularisation.
#### Links
* PR: [Modularise Checkout Package](https://github.com/Meesho/supply_android/pull/7114)
* Solutioning Doc Link: [Checkout Modularisation Solutioning Doc](https://meesho.atlassian.net/wiki/spaces/EW/pages/3001057383/app+checkout+modularisation)
### Remove NON-MSC code
##### Situation
As the Multi-Supplier Cart (MSC) feature reached its full deployment, an opportunity emerged to refine our Android codebase by eliminating dead code segments.
##### Task
Recognising the chance for code cleanup and optimisation, the task involved identifying and removing non-MSC code sections from our Android application. The objective was to leverage the complete integration of MSC, enhancing code clarity and realising technical advantages.
##### Action
Systematically, the identified dead code was removed, resulting in a more streamlined codebase and a substantial **150KB** reduction in the APK size. This cleanup initiative, closely tied to the widespread adoption of MSC, not only enhanced code readability for our engineering team but also delivered significant technical benefits.
#### Result
The successful removal of approximately **11,000** lines of non-MSC code not only accomplished our goal of code cleanup but also brought about a noteworthy reduction in the APK size, a critical optimisation for our application. Driven by the seamless integration of MSC, this process showcased its efficacy in improving overall code quality, readability, and maintainability. The positive impacts extended beyond code cleanliness, encompassing improved compilation times, enhanced runtime performance, and a reduced security risk footprint. This initiative reflects our commitment to delivering a streamlined, efficient, and secure application experience.
#### Competencies Achieved
- Coding & Problem Solving
- Operational Excellence & Documentation
#### Reasoning
Removing non-MSC code demanded a strategic approach to problem-solving, ensuring operational excellence through documentation, and contributing to a more efficient and secure application environment.
#### Links
* PR Link: [Remove NON-MSC Code PR](https://github.com/Meesho/supply_android/pull/4105)
### Safe Commerce Fraud Awareness
##### Situation
Meesho faces a critical challenge with users falling victim to scams due to a lack of awareness, leading to significant financial losses and a threat to the platform's reputation.
##### Task
Implement a fraud awareness solution seamlessly integrated into the order confirmation process to proactively educate users and create a more secure e-commerce environment.
###### Order Confirmation Screen Solution:
Display a user-friendly banner on the order confirmation screen with the text "Stay alert & stay safe from scams!" and a call-to-action (CTA) guiding users to insights on anti-phishing measures.
###### Technical Requirements
Implement backend toggles for banner control, dynamic content modification, and tracking mechanisms for user interactions to ensure a responsive and adaptable fraud awareness system.
##### Action
Execute the development of backend controls, seamlessly design and integrate the banner, apply conditions for display based on order success and margin, and establish tracking mechanisms to gauge user engagement.
##### Result
Anticipate a positive shift: heightened user awareness, decreased instances of fraud, gained customer trust, and quantifiable changes in user behavior, ensuring a more secure and resilient e-commerce ecosystem.
Despite the task's PRD being shared on the day of shipment, successful delivery was achieved, highlighting remarkable development speed from both frontend and backend
#### Competencies Achieved
- Think 10X, think long-term
- User first
#### Reasoning
The implementation of a fraud awareness solution requires a forward-thinking, long-term approach (Think 10X) and a focus on user-centric design and communication (User first).
#### Links
* PR Link: [Safe Commerce Fraud Awareness PR](https://github.com/Meesho/supply_android/pull/4069)
* PRD Link: [Safe Commerce Fraud Awareness PRD](https://coda.io/d/PRD-Fraud-awareness-comms-on-order-confirmation-page_diQ10jz8fOD/Problem-Discovery_suJmC#_luD90)
### Migrate Order Place to Kotlin
##### Situation
The Order Place Page within the Transact flow is currently implemented in Java and is responsible for executing the order placement logic, including preorders API calls and place order API calls. As part of the modularisation process for Transact checkout flows, there is a need to migrate the relevant files to Kotlin.
##### Task
Migrate the following Java files to Kotlin:
- com.meesho.supply.order.OrderPlaceVm
- com.meesho.supply.order.OrderPlaceActivity
This migration is a crucial initial step in the modularisation of Transact checkout flows.
##### Action 
- Commence the migration of com.meesho.supply.order.OrderPlaceVm and com.meesho.supply.order.OrderPlaceActivity from Java to Kotlin, preserving the current logic.
- After meticulous testing to ensure functionality remains unchanged, update documentation and communicate the successful completion of the migration.
- This initiative aims to enhance code consistency and maintainability within the Transact checkout flows.
##### Result
The migration of Order Place Page files from Java to Kotlin lays the foundation for the modularisation of Transact checkout flows, contributing to code consistency and enhancing maintainability.
#### Competencies Achieved
- Coding & Problem Solving
- Architecture & Design
#### Reasoning
The migration involves a deep understanding of code structure and logic (Coding & Problem Solving) and an architectural perspective in transitioning from Java to Kotlin (Architecture & Design).
#### Links
* PR Link: [Migrate Order Place to Kotlin PR](https://github.com/Meesho/supply_android/pull/4569)
* Solutioning Doc Link: [Migrate Order Place to Kotlin Solutioning Doc](https://meesho.atlassian.net/wiki/spaces/EW/pages/2668298261/Migration+of+Order+Place+Page+to+Kt.)

### Gender Input From User
##### Situation
The onboarding flow in the Meesho app lacked the integration of gender input from users, impacting the overall user experience. The North Star Metric for success is a significant improvement in the Gender Fill Rate, measured against the goal of achieving a 1OA (9 D) metric.
##### Task
Introduce a gender input feature in the onboarding flow, aiming to enhance user engagement and capture essential demographic information. The approach involves two variants: Variant 1, where gender is collected during the initial app installation, and Variant 2, where gender is gathered in subsequent sessions.
##### Action
In Variant 1, users are prompted for gender immediately after selecting their preferred language during app installation. In Variant 2, gender input occurs in a modal during the user's next session. Detailed scenarios for each variant outline user interactions based on language selection and gender input.
##### Result
Anticipate a significant increase in the Gender Fill Rate, leading to a more comprehensive understanding of user demographics. The A/B experimentation plan, tracked through Mixpanel, ensures systematic testing and evaluation of both variants, informing future decisions based on user behavior and preferences.
#### Competencies Achieved
- User first
- Problem first mindset
#### Reasoning
The introduction of gender input enhances the user experience, reflecting a user-centric approach (User first) and addressing a specific deficiency in the onboarding process (Problem first mindset).
#### Links
* PR Link: [Gender Input From User PR](https://github.com/Meesho/supply_android/pull/3388)
