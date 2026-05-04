# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: tests/ebr/core/payments/payment-order.spec.js >> business owner - bank account - bank - now
- Location: utils/ebr/runtime-skip.js:352:14

# Error details

```
Error: expect(locator).toBeVisible() failed

Locator: getByText('Transaction ID #PS8LXL')
Expected: visible
Timeout: 30000ms
Error: element(s) not found

Call log:
  - Expect "toBeVisible" with timeout 30000ms
  - waiting for getByText('Transaction ID #PS8LXL')

```

# Page snapshot

```yaml
- generic [ref=e3]:
  - banner [ref=e4]
  - main [ref=e6]:
    - generic [ref=e8]:
      - navigation "Benefits" [ref=e11]:
        - link "Home" [ref=e12] [cursor=pointer]:
          - /url: /
          - generic [ref=e13]:
            - img
          - generic [ref=e14]: Home
        - link "Make a payment" [ref=e15] [cursor=pointer]:
          - /url: /payments/make
          - generic [ref=e16]:
            - img
          - generic [ref=e17]: Make a payment
        - button "Payment methods" [ref=e18] [cursor=pointer]:
          - img [ref=e20]
          - generic [ref=e22]: Payment methods
        - link "Statement accounts" [ref=e23] [cursor=pointer]:
          - /url: /statements
          - generic [ref=e24]:
            - img
          - generic [ref=e25]: Statement accounts
        - link "Payees" [ref=e26] [cursor=pointer]:
          - /url: /payments/payees
          - generic [ref=e27]:
            - img
          - generic [ref=e28]: Payees
        - link "Scheduled payments" [ref=e29] [cursor=pointer]:
          - /url: ""
          - generic [ref=e30]:
            - img
          - generic [ref=e31]: Scheduled payments
        - link "Batch payment" [ref=e32] [cursor=pointer]:
          - /url: ""
          - generic [ref=e33]:
            - img
          - generic [ref=e34]: Batch payment
        - link "Approve payments" [ref=e35] [cursor=pointer]:
          - /url: /pending-approval-orders
          - generic [ref=e36]:
            - img
          - generic [ref=e37]: Approve payments
        - link "Rewards" [ref=e39] [cursor=pointer]:
          - /url: ""
          - generic [ref=e40]:
            - img
          - generic [ref=e41]: Rewards
        - link "Experiences" [ref=e42] [cursor=pointer]:
          - /url: ""
          - generic [ref=e43]:
            - img
          - generic [ref=e44]: Experiences
        - link "BizHub" [ref=e45] [cursor=pointer]:
          - /url: ""
          - generic [ref=e46]:
            - img
          - generic [ref=e47]: BizHub
        - link "Transfer my points" [ref=e49] [cursor=pointer]:
          - /url: ""
          - generic [ref=e50]:
            - img
          - generic [ref=e51]: Transfer my points
        - link "Activity" [ref=e53] [cursor=pointer]:
          - /url: /activity
          - generic [ref=e54]:
            - img
          - generic [ref=e55]: Activity
      - list [ref=e60]:
        - listitem [ref=e61]:
          - link "How it works" [ref=e62] [cursor=pointer]:
            - /url: https://support.symbionelite.com.au/hc/en-us
            - generic [ref=e63]: How it works
        - listitem [ref=e64]:
          - link "Terms & Conditions" [ref=e65] [cursor=pointer]:
            - /url: /terms-conditions
            - generic [ref=e66]: Terms & Conditions
        - listitem [ref=e67]:
          - link "Privacy Policy" [ref=e68] [cursor=pointer]:
            - /url: /privacy-policy
            - generic [ref=e69]: Privacy Policy
        - listitem [ref=e70]:
          - link "Contact" [ref=e71] [cursor=pointer]:
            - /url: /help
            - generic [ref=e72]: Contact
        - listitem [ref=e73]:
          - button "Action" [ref=e74] [cursor=pointer]: Logout
```

# Test source

```ts
  269 | 
  270 |       // Only continue with further assertions if payment succeeded
  271 |       if (result?.success) {
  272 |         // Add any additional verification here if needed
  273 |       }
  274 |     } else {
  275 |       await paymentsConfirmationPage.verifyPaymentConfirmation(paymentData, paymentsMakePage, paymentsSummaryPage, testInfo);
  276 |     }
  277 | 
  278 |     // DEBUG: For testing purposes only
  279 |     console.log('⏳ Waiting 3 seconds before clicking Done button...');
  280 |     await page.waitForTimeout(3000);
  281 | 
  282 |     // Skip activity page verification for scheduled payments
  283 |     if (paymentData.timing === 'schedule') {
  284 |       console.log('ℹ️ Skipping activity page verification for scheduled payment');
  285 |       return;
  286 |     }
  287 | 
  288 |     await page.getByRole('link', { name: /^(Activity|Reporting)$/ }).click();
  289 | 
  290 |     // Get the captured transaction ID from the appropriate source based on payment method
  291 |     let transactionId;
  292 |     if (paymentData.method === 'payid') {
  293 |       transactionId = paymentsPayIdPage.payIdReference;
  294 |       console.log('🔍 Looking for PayID transaction ID in activity list:', transactionId);
  295 |     } else if (paymentData.method === 'pba') {
  296 |       transactionId = paymentsPbaPage.transactionId;
  297 |       console.log('🔍 Looking for PBA transaction ID in activity list:', transactionId);
  298 |     } else {
  299 |       transactionId = paymentsConfirmationPage.getCapturedTransactionId();
  300 |       console.log('🔍 Looking for transaction ID in activity list:', transactionId);
  301 |     }
  302 | 
  303 |     // ✅ FIRST: Wait for the activity list to load before checking for transaction
  304 |     const maxRetries = 5;
  305 |     let retryCount = 0;
  306 |     let activityListLoaded = false;
  307 | 
  308 |     while (retryCount < maxRetries && !activityListLoaded) {
  309 |       try {
  310 |         await page.waitForSelector('a[href^="/activity/"]', { state: 'visible', timeout: 45000 });
  311 |         console.log(`✅ Activity list loaded (attempt ${retryCount + 1}/${maxRetries})`);
  312 |         activityListLoaded = true;
  313 |       } catch (error) {
  314 |         retryCount++;
  315 |         if (retryCount < maxRetries) {
  316 |           console.log(`⚠️ Activity list did not load within timeout (attempt ${retryCount}/${maxRetries}), reloading page...`);
  317 |           await page.reload();
  318 |         } else {
  319 |           throw new Error(`❌ Activity list failed to load after ${maxRetries} attempts`);
  320 |         }
  321 |       }
  322 |     }
  323 | 
  324 |     // Find all payment tiles that contain the transaction ID but NOT "Points Earned"
  325 |     // Use filter to exclude tiles with "Points Earned" text
  326 |     const paymentTiles = page
  327 |       .locator('a[href^="/activity/"]')
  328 |       .filter({ hasText: transactionId ?? undefined })
  329 |       .filter({ hasNotText: 'Points Earned' });
  330 | 
  331 |     // Check if the payment tile exists, reload if not found - retry up to 3 times
  332 |     let transactionFound = false;
  333 |     retryCount = 0;
  334 | 
  335 |     while (retryCount < maxRetries && !transactionFound) {
  336 |       const tileCount = await paymentTiles.count();
  337 | 
  338 |       if (tileCount === 0) {
  339 |         retryCount++;
  340 |         if (retryCount < maxRetries) {
  341 |           console.log(`⚠️ Transaction ID not found in activity list (attempt ${retryCount}/${maxRetries}), reloading page...`);
  342 |           await page.reload();
  343 |           await page.waitForSelector('a[href^="/activity/"]', { state: 'visible', timeout: 60000 });
  344 |           await page.waitForTimeout(2000); // Wait for page to reload
  345 |         } else {
  346 |           console.warn(`⚠️ Transaction ID ${transactionId} not found after ${maxRetries} attempts (infra flaky) - continuing test without activity verification`);
  347 |           return; // Skip activity verification but let test pass
  348 |         }
  349 |       } else {
  350 |         console.log(`✅ Found ${tileCount} matching activity tile(s) for transaction ID ${transactionId} (attempt ${retryCount + 1}/${maxRetries})`);
  351 |         transactionFound = true;
  352 |       }
  353 |     }
  354 | 
  355 |     const matchingHrefs = await paymentTiles.evaluateAll((elements) => elements.map((element) => element.getAttribute('href')).filter((href) => typeof href === 'string' && href.length > 0));
  356 | 
  357 |     if (!matchingHrefs.length) {
  358 |       console.warn(`⚠️ Matching activity tiles were found for ${transactionId}, but no hrefs could be extracted - skipping activity verification`);
  359 |       return;
  360 |     }
  361 | 
  362 |     const isPayIdFlow = paymentData.method === 'payid';
  363 | 
  364 |     if (!isPayIdFlow) {
  365 |       const href = matchingHrefs[0];
  366 |       const targetUrl = new URL(href, page.url()).toString();
  367 |       console.log(`🔍 Opening first matching activity: ${href}`);
  368 |       await page.goto(targetUrl, { waitUntil: 'domcontentloaded' });
> 369 |       await expect(page.getByText(`Transaction ID #${transactionId}`)).toBeVisible({ timeout: 30000 });
      |                                                                        ^ Error: expect(locator).toBeVisible() failed
  370 |       console.log('✅ Activity verification completed using first matching entry');
  371 |       console.log('⏳ Waiting 3 seconds to show screen');
  372 |       await page.waitForTimeout(3000);
  373 |       return;
  374 |     }
  375 | 
  376 |     for (let i = 0; i < matchingHrefs.length; i++) {
  377 |       const href = matchingHrefs[i];
  378 |       const targetUrl = new URL(href, page.url()).toString();
  379 |       console.log(`🔍 Opening matching activity ${i + 1}/${matchingHrefs.length}: ${href}`);
  380 |       await page.goto(targetUrl, { waitUntil: 'domcontentloaded' });
  381 | 
  382 |       // Verify the transaction ID is displayed on the payment details page
  383 |       await expect(page.getByText(`Transaction ID #${transactionId}`)).toBeVisible({ timeout: 30000 });
  384 | 
  385 |       if (i < matchingHrefs.length - 1) {
  386 |         console.log(`↩️ Returning to activity list to check next match (${i + 2}/${matchingHrefs.length})`);
  387 |         await page.goBack({ waitUntil: 'domcontentloaded' });
  388 |         await page.waitForSelector('a[href^="/activity/"]', { state: 'visible', timeout: 30000 });
  389 |       }
  390 |     }
  391 | 
  392 |     // DEBUG: For testing purposes only
  393 |     console.log('⏳ Waiting 3 seconds to show screen');
  394 |     await page.waitForTimeout(3000);
  395 |   });
  396 | }
  397 | 
```