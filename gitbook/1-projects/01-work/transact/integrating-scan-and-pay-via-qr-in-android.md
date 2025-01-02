  
Figma: [Payments Page [DEV]](https://www.figma.com/file/GqJoBCCmJg98lZnkrGdb54/QR-on-Android?type=design&node-id=6009%3A11120&mode=design&t=jdIqJbCKI3hPuMuM-1)

### Problem Statement

Our app currently lacks a mechanism to scan and pay to place an order. The web client has recently implemented this feature, and the Android also wants to incorporate similar functionality.

### Possible Approaches

There are two potential approaches to solve this problem:

1. Android client handling
    
2. Web client handling with Android reusing the logic via WebView
    

### Approach #1: Android Client Handling

The Android client would independently handle all required logic. It would use the Juspay transaction (txn) API to generate a QR code by sending the order ID and retrieving the necessary details to formulate a deeplink URL, which would then be converted into a QR code.

**Current Situation:**

- The integrated Juspay Headless Payment Page SDK manages all other payment instruments.
    
- The Headless SDK does not support QR code functionality as it is not an industry standard.
    

**Implementation Requirements:**

- Android needs to implement this logic and callbacks to handle the order status (success or failure).
    

**Pros:**

1. Complete control over the logic.
    
2. Finer granularity of control on android side.
    

**Cons:**

1. Android must reimplement SDK behavior and maintain it long-term solely for QR functionality.
    
2. Duplicates the work already done by the web client.
    
3. Uncertain benefits from QR code implementation.
    
4. Increases complexity of the Android payment page.
    

### Approach #2: Web Client Handling via WebView

Leverage the existing web implementation by using WebView in the Android client. The web client would expose a dedicated path for Android.

**Implementation:**

- The Android client opens the web page inside a WebView.
    
- Create two JavaScript bridges for communication between the Android client and the web client:
    
    - onViewQRClicked(data: Data) (Android to Web)
        
    - onPaymentStatus(status: Status) (Web to Android)
        

**Pros:**

1. Reuses existing web logic.
    
2. Faster implementation.
    
3. Preferred method as it is experimental.
    
4. Reduces complexity on the already extensive Android payment page.
    

**Cons:**

1. Requires bandwidth from the web team (estimate needed).
    
2. Potentially sub-optimal non-native user experience (subjective).
    

### Conclusion

Considering the pros and cons, the WebView approach is recommended. It allows for quicker implementation, reduces complexity on the Android side, and leverages the existing web functionality.

This document outlines the rationale and recommendation for implementing the scan and pay feature on the Android platform using a WebView approach.