# Sovendus Generic native App Integration for Voucher Network and Checkout Benefits


1. Create a webview component with the following HTML:
   ```html
   <!DOCTYPE html>
   <html>
     <head>
       <meta name="viewport" content="initial-scale=1" />
     </head>
     <body id="body">
       <div id="sovendus-voucher-banner"></div>
       <div id="sovendus-checkout-benefits-banner"></div>
       <script type="text/javascript">
         window.sovIframes = window.sovIframes || [];
         if ("$trafficMediumNumberVoucherNetwork") {
           window.sovIframes.push({
             trafficSourceNumber: "$trafficSourceNumber",
             trafficMediumNumber: "$trafficMediumNumberVoucherNetwork",
             iframeContainerId: "sovendus-voucher-banner",
             timestamp: "$orderUnixTime",
             sessionId: "$sessionId",
             orderId: "$orderId",
             orderValue: "$netOrderValue",
             orderCurrency: "$currencyCode",
             usedCouponCode: "$usedCouponCode",
             integrationType: "genericnative-1.0.1"
           });
         }
         if ("$trafficMediumNumberCheckoutBenefits") {
           window.sovIframes.push({
             trafficSourceNumber: "$trafficSourceNumber",
             trafficMediumNumber: "$trafficMediumNumberCheckoutBenefits",
             iframeContainerId: "sovendus-checkout-benefits-banner",
           });
         }
         window.sovConsumer = {
           consumerSalutation: "$salutation",
           consumerFirstName: "$firstName",
           consumerLastName: "$lastName",
           consumerEmail: "$email",
           consumerPhone: "$phone",
           consumerYearOfBirth: "$yearOfBirth",
           consumerStreet: "$street",
           consumerStreetNumber: "$streetNumber",
           consumerZipcode: "$zipcode",
           consumerCity: "$city",
           consumerCountry: "$country",
         };
       </script>
       <script
         type="text/javascript"
         src="https://api.sovendus.com/sovabo/common/js/flexibleIframe.js"
         async="true"
       ></script>
     </body>
   </html>
   ```
2. Make sure all variables in the HTML starting with a $ are defined
3. Clicks on external links need to be forwarded to the native browser, this can be done with one of the following ways:\
   a. Prevent all navigation requests and forward the URL it tried to navigate to, to the native browser

   b. Prevent all navigation requests, catch the javascript event "openInNativeBrowser" and open the url in the event in the native browser. This is how you can catch the event in javascript and get the URL it should navigate to:

   ```javascript
   window.addEventListener("openInNativeBrowser", (event) => {
     console.log("test", event.detail.url);
   });
   ```

4. The height of your native component should be based on the height of the body inside the webview. You can achieve this by adding a resize observer on the body inside the webview. For example like that:
   ```javascript
   const _body = document.getElementById("body");
   new ResizeObserver(() => {
     console.log(_body.clientHeight);
   }).observe(_body);
   ```
5. Use the component you've just created where you want the Sovendus Banner to appear