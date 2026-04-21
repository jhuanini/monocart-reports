# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: tests/ebr/core/payments/payroll-order.spec.js >> Payroll payment - business owner - payid - credit - Mastercard
- Location: utils/ebr/runtime-skip.js:324:14

# Error details

```
TimeoutError: locator.waitFor: Timeout 10000ms exceeded.
Call log:
  - waiting for locator('.base-select-popup > ul > li').filter({ hasText: '*1005' }).filter({ hasNotText: 'VERIFY ACCOUNT' }).first() to be visible

```

# Page snapshot

```yaml
- generic [ref=e1]:
  - generic [ref=e3]:
    - banner [ref=e4]:
      - generic [ref=e5]:
        - link "Go to Home" [ref=e7] [cursor=pointer]:
          - /url: /
          - img "B2B AU PVT Logo" [ref=e9]
        - generic [ref=e10]:
          - generic:
            - button "PLATINUM":
              - button "PLATINUM":
                - generic:
                  - generic:
                    - generic:
                      - img
                    - paragraph: PLATINUM
            - button "Action":
              - paragraph: 1,000,043 PTS
          - list [ref=e11]:
            - listitem [ref=e12]:
              - button [ref=e13] [cursor=pointer]:
                - img [ref=e15]
            - listitem [ref=e17]:
              - button [ref=e18] [cursor=pointer]:
                - img [ref=e20]
            - listitem [ref=e22]:
              - button [ref=e23] [cursor=pointer]:
                - img [ref=e25]
    - main [ref=e27]:
      - generic [ref=e29]:
        - generic [ref=e30]:
          - navigation "Benefits" [ref=e32]:
            - link "Home" [ref=e33] [cursor=pointer]:
              - /url: /
              - generic [ref=e34]:
                - img
              - generic [ref=e35]: Home
            - link "Bank Link" [ref=e37] [cursor=pointer]:
              - /url: /make/bank-link
              - generic [ref=e38]:
                - img
              - generic [ref=e39]: Bank Link
            - link "Statement accounts" [ref=e40] [cursor=pointer]:
              - /url: /statements
              - generic [ref=e41]:
                - img
              - generic [ref=e42]: Statement accounts
            - link "Make a payment" [ref=e43] [cursor=pointer]:
              - /url: /payments/make
              - generic [ref=e44]:
                - img
              - generic [ref=e45]: Make a payment
            - link "Pay your payroll" [ref=e46] [cursor=pointer]:
              - /url: /payments/payroll
              - generic [ref=e47]:
                - img
              - generic [ref=e48]: Pay your payroll
            - link "Upload batch payment" [ref=e49] [cursor=pointer]:
              - /url: /bank-file-upload
              - generic [ref=e50]:
                - img
              - generic [ref=e51]: Upload batch payment
            - link "Scheduled payments" [ref=e52] [cursor=pointer]:
              - /url: /scheduled-payments
              - generic [ref=e53]:
                - img
              - generic [ref=e54]: Scheduled payments
            - link "Payees" [ref=e55] [cursor=pointer]:
              - /url: /payments/payees
              - generic [ref=e56]:
                - img
              - generic [ref=e57]: Payees
            - link "Approve payments" [ref=e58] [cursor=pointer]:
              - /url: /pending-approval-orders
              - generic [ref=e59]:
                - img
              - generic [ref=e60]: Approve payments
            - link "Shop rewards" [ref=e62] [cursor=pointer]:
              - /url: /gift-cards
              - generic [ref=e63]:
                - img
              - generic [ref=e64]: Shop rewards
            - link "Transfer points" [ref=e65] [cursor=pointer]:
              - /url: /points-programs
              - generic [ref=e66]:
                - img
              - generic [ref=e67]: Transfer points
            - link "TravelHub" [ref=e68] [cursor=pointer]:
              - /url: /travel-hub
              - generic [ref=e69]:
                - img
              - generic [ref=e70]: TravelHub
            - link "BizHub" [ref=e71] [cursor=pointer]:
              - /url: /community-hub
              - generic [ref=e72]:
                - img
              - generic [ref=e73]: BizHub
            - link "Experiences" [ref=e74] [cursor=pointer]:
              - /url: /competitions
              - generic [ref=e75]:
                - img
              - generic [ref=e76]: Experiences
            - link "Reporting" [ref=e78] [cursor=pointer]:
              - /url: /activity
              - generic [ref=e79]:
                - img
              - generic [ref=e80]: Reporting
          - generic "Make a payment" [ref=e86]:
            - generic [ref=e88]:
              - heading "Pay your payroll" [level=1] [ref=e91]
              - generic [ref=e93]:
                - generic [ref=e94]:
                  - heading "Paying on behalf of" [level=2] [ref=e96]
                  - generic [ref=e98]:
                    - generic [ref=e99]:
                      - img [ref=e102]
                      - textbox [ref=e104] [cursor=pointer]:
                        - /placeholder: Select business
                        - text: M.A MARTIN & M.B MARTIN - ABN 36 621 991 399
                      - button [ref=e106] [cursor=pointer]:
                        - img [ref=e108]
                    - generic [ref=e112]: Select the business you are paying on behalf of
                - generic [ref=e113]:
                  - heading "Paying to" [level=2] [ref=e115]
                  - generic [ref=e116]:
                    - generic [ref=e117]:
                      - generic [ref=e118]: "Payroll file: au-1Payee.aba"
                      - generic [ref=e119]: (6 payments)
                    - generic [ref=e120]:
                      - button "View" [ref=e122] [cursor=pointer]:
                        - generic [ref=e124]: View
                      - button "Remove" [ref=e126] [cursor=pointer]:
                        - generic [ref=e128]: Remove
                  - generic [ref=e130]:
                    - textbox "Amount *" [ref=e132]:
                      - /placeholder: "0.00"
                      - text: $43.43
                    - generic [ref=e133] [cursor=pointer]: Amount *
                    - generic [ref=e135]: Amount imported from ABA file
                - generic [ref=e137]:
                  - generic [ref=e138]:
                    - heading "Select how to pay" [level=2] [ref=e139]
                    - button "Processing times" [ref=e140] [cursor=pointer]:
                      - generic [ref=e141]:
                        - img [ref=e143]
                        - generic [ref=e145]: Processing times
                  - generic [ref=e146]:
                    - generic [ref=e149] [cursor=pointer]:
                      - radio "PayID" [checked] [ref=e150]
                      - generic [ref=e152]:
                        - strong [ref=e155]: PayID
                        - img [ref=e158]
                    - generic [ref=e163] [cursor=pointer]:
                      - radio "Credit/Debit Card" [ref=e164]
                      - generic [ref=e166]:
                        - strong [ref=e169]: Credit/Debit Card
                        - img [ref=e172]
                  - generic [ref=e175]:
                    - img [ref=e179]
                    - generic [ref=e181]: Payroll payments can only be made via PayID
                - generic [ref=e182]:
                  - generic [ref=e183]:
                    - heading "Select payment method to pay fees" [level=2] [ref=e184]
                    - button "+ Add new" [ref=e185] [cursor=pointer]:
                      - generic [ref=e186]: + Add new
                  - generic [ref=e187]: Fees will be charged separately to your chosen payment method once you make your PayID transaction on your internet banking.
                  - generic [ref=e190]:
                    - textbox [active] [ref=e191] [cursor=pointer]:
                      - /placeholder: Select payment method
                    - generic [ref=e192] [cursor=pointer]:
                      - generic:
                        - img
                - generic [ref=e193]:
                  - generic [ref=e196] [cursor=pointer]:
                    - img [ref=e199]
                    - generic [ref=e201]:
                      - text: I agree to the
                      - button "Action" [ref=e202]:
                        - strong [ref=e203]: Terms & Conditions
                  - generic [ref=e206] [cursor=pointer]:
                    - img [ref=e209]
                    - generic [ref=e211]: I confirm that all payments within the uploaded file are valid payroll payments
                - generic [ref=e213]:
                  - button "Cancel" [ref=e214] [cursor=pointer]:
                    - generic [ref=e215]: Cancel
                  - button "Continue" [disabled]:
                    - generic: Continue
        - list [ref=e217]:
          - listitem [ref=e218]:
            - link "How it works" [ref=e219] [cursor=pointer]:
              - /url: https://support.symbionelite.com.au/hc/en-us
              - generic [ref=e220]: How it works
          - listitem [ref=e221]:
            - link "Terms & Conditions" [ref=e222] [cursor=pointer]:
              - /url: /terms-conditions
              - generic [ref=e223]: Terms & Conditions
          - listitem [ref=e224]:
            - link "Privacy Policy" [ref=e225] [cursor=pointer]:
              - /url: /privacy-policy
              - generic [ref=e226]: Privacy Policy
          - listitem [ref=e227]:
            - link "Contact" [ref=e228] [cursor=pointer]:
              - /url: /help
              - generic [ref=e229]: Contact
          - listitem [ref=e230]:
            - button "Action" [ref=e231] [cursor=pointer]: Logout
  - listbox [ref=e233]:
    - generic [ref=e234]: No payment methods available
```

# Test source

```ts
  1395 |       throw new Error('Unable to read maximum points from slider tooltip');
  1396 |     }
  1397 | 
  1398 |     // Return to min and read min points
  1399 |     await this.page.keyboard.press('Home');
  1400 |     await this.page.waitForTimeout(80);
  1401 |     const minTooltipValue = await readTooltipValue();
  1402 |     const resolvedMinPoints = Number.isFinite(minTooltipValue) ? minTooltipValue : min;
  1403 | 
  1404 |     // Clamp and align target to slider step in points domain
  1405 |     const clampedTarget = Math.max(resolvedMinPoints, Math.min(targetPoints, maxPoints));
  1406 |     const alignedTarget = (() => {
  1407 |       // step read earlier is assumed in points units; fall back to 1
  1408 |       const s = Number.isFinite(step) && step > 0 ? step : 1;
  1409 |       const q = Math.round((clampedTarget - resolvedMinPoints) / s) * s + resolvedMinPoints;
  1410 |       // guard floating precision
  1411 |       return Number(q.toFixed(6));
  1412 |     })();
  1413 | 
  1414 |     // Walk the slider one keyboard step at a time from its minimum state.
  1415 |     let current = resolvedMinPoints;
  1416 |     let attempts = 0;
  1417 |     while (Number.isFinite(current) && current !== alignedTarget && attempts++ < 200) {
  1418 |       await handle.focus();
  1419 |       await this.page.keyboard.press(current < alignedTarget ? 'ArrowRight' : 'ArrowLeft');
  1420 |       await this.page.waitForTimeout(20);
  1421 |       const next = await readTooltipValue();
  1422 |       if (!Number.isFinite(next)) break;
  1423 |       if (next === current) {
  1424 |         throw new Error(`Slider stopped responding to keyboard input at ${current} while targeting ${alignedTarget}.`);
  1425 |       }
  1426 |       current = next;
  1427 |     }
  1428 | 
  1429 |     const finalValue = await readTooltipValue();
  1430 |     console.log(`Points to redeem: ${finalValue}/${targetPoints}`);
  1431 |     if (!Number.isFinite(finalValue) || finalValue !== alignedTarget) {
  1432 |       throw new Error(`Failed to set points to exact target. Expected ${alignedTarget}, got ${finalValue}.`);
  1433 |     }
  1434 |     if (this.currentPaymentOptions) {
  1435 |       this.currentPaymentOptions.pointsToRedeem = finalValue;
  1436 |     }
  1437 |   }
  1438 | 
  1439 |   /**
  1440 |    * Select specific card or bank account after choosing payment method
  1441 |    * This method handles the secondary selection for credit/debit cards and bank accounts
  1442 |    * @param {string} method - Payment method ('creditdebit', 'credit', 'debit', 'card', 'bank', 'banktransfer', 'payid')
  1443 |    * @param {Object} paymentOptions - Payment options containing card/bank details
  1444 |    * @param {string|string[]} [paymentOptions.bankAccountNo] - Bank account number or list for bank transfers (optional)
  1445 |    * @param {string} [paymentOptions.cardBrand] - Card brand for credit/debit payments (required when using card methods)
  1446 |    * @param {string} [paymentOptions.cardLast4] - Last 4 digits of card number (required when using card methods)
  1447 |    */
  1448 |   async selectCardOrBank(method, paymentOptions = {}) {
  1449 |     const normalizedMethod = method.toLowerCase();
  1450 | 
  1451 |     console.log(`\n🔍 [selectCardOrBank] Starting card/bank selection`);
  1452 |     console.log(`🔍 [selectCardOrBank] Method: ${normalizedMethod}`);
  1453 |     console.log(`🔍 [selectCardOrBank] Payment options:`, JSON.stringify(paymentOptions, null, 2));
  1454 |     console.log(`🔍 [selectCardOrBank] Payee type: ${this.selectedPayeeDetails.type}`);
  1455 | 
  1456 |     // Accept 'points' as a valid method and proceed to selectInput.click() like card/bank
  1457 | 
  1458 |     if (['creditdebit', 'credit', 'debit', 'card'].includes(normalizedMethod) || ((normalizedMethod === 'points' || normalizedMethod === 'payid') && paymentOptions.cardBrand && paymentOptions.cardLast4)) {
  1459 |       console.log(`🔍 [selectCardOrBank] Entering credit/debit card path`);
  1460 | 
  1461 |       // POM-level guard: if project config hides credit/debit card for this payee type, skip points+card flow
  1462 |       if (normalizedMethod === 'points' && paymentOptions.cardBrand && paymentOptions.cardLast4) {
  1463 |         // credit/debit hidden state already enforced via payeeSpecs earlier
  1464 |       }
  1465 |       // For credit/debit cards or points+card: Type brand and last 4 digits, then select first option
  1466 |       if (!paymentOptions.cardBrand || !paymentOptions.cardLast4) {
  1467 |         throw new Error('Card details are required for credit/debit payments. Please provide both cardBrand and cardLast4 in paymentOptions.');
  1468 |       }
  1469 |       const cardBrand = paymentOptions.cardBrand;
  1470 |       const last4Digits = paymentOptions.cardLast4;
  1471 |       const normalizedCardBrand = this.normalizeCardBrand(cardBrand);
  1472 |       const cardDisplayText = `${normalizedCardBrand} *${last4Digits}`;
  1473 |       const payeeType = this.selectedPayeeDetails.type.toLowerCase();
  1474 | 
  1475 |       console.log(`🔍 [selectCardOrBank] Card brand: ${cardBrand} → ${normalizedCardBrand}`);
  1476 |       console.log(`🔍 [selectCardOrBank] Card last 4: ${last4Digits}`);
  1477 |       console.log(`🔍 [selectCardOrBank] Card display text: ${cardDisplayText}`);
  1478 |       console.log(`🔍 [selectCardOrBank] About to open card selector list...`);
  1479 | 
  1480 |       // await this._waitForSelectInputEnabled();
  1481 |       await this.selectInput.click({ timeout: 20000 });
  1482 |       // American Express restriction logic unchanged
  1483 |       const isAmex = cardBrand.toLowerCase().includes('amex') || cardBrand.toLowerCase().includes('american express');
  1484 |       // Determine brand-level restriction from config (creditDebitCard.amex === 'not accepted')
  1485 |       // Amex brand acceptance now handled purely by backend/UI responses; no config-based brand rule
  1486 | 
  1487 |       // BUG: https://eonx.atlassian.net/browse/SIR-4036
  1488 |       // OLD IMPLEMENTATION: Look for brand + card number (e.g., "Visa *1000")
  1489 |       // const cardOption = this.page.locator('li').filter({ hasText: cardDisplayText }).first();
  1490 | 
  1491 |       // NEW IMPLEMENTATION: Look for card number only with asterisk (e.g., "*1000")
  1492 |       const cardNumberOnly = `*${last4Digits}`;
  1493 |       console.log(`🔍 [selectCardOrBank] Searching for card number only: ${cardNumberOnly}`);
  1494 |       const cardOption = this.page.locator('.base-select-popup > ul > li').filter({ hasText: cardNumberOnly, hasNotText: 'VERIFY ACCOUNT' }).first();
> 1495 |       await cardOption.waitFor({ state: 'visible', timeout: 10000 });
       |                        ^ TimeoutError: locator.waitFor: Timeout 10000ms exceeded.
  1496 |       await cardOption.click();
  1497 |       // log removed: selected card
  1498 | 
  1499 |       // For PayID funding source selection, only wait for payment-methods/fees here.
  1500 |       // The PayID radio selection already waited for program-fees.
  1501 |       try {
  1502 |         let paymentMethodsFeesResponse;
  1503 |         if (normalizedMethod === 'payid') {
  1504 |           console.log('⏳ Waiting for POST /payment-methods/fees response after PayID card selection...');
  1505 |           paymentMethodsFeesResponse = await this.page.waitForResponse((response) => response.request().method() === 'POST' && response.url().includes('/v3/payment-methods/fees') && response.status() === 200, { timeout: 15000 });
  1506 |           console.log('✅ payment-methods/fees API confirmed after PayID card selection');
  1507 |         } else {
  1508 |           console.log('⏳ Waiting for POST /program-fees AND POST /payment-methods/fees responses after card selection...');
  1509 |           const responses = await Promise.all([
  1510 |             this.page.waitForResponse((response) => response.request().method() === 'POST' && response.url().includes('/program-fees') && response.status() === 200, { timeout: 15000 }),
  1511 |             this.page.waitForResponse((response) => response.request().method() === 'POST' && response.url().includes('/v3/payment-methods/fees') && response.status() === 200, { timeout: 15000 }),
  1512 |           ]);
  1513 |           paymentMethodsFeesResponse = responses[1];
  1514 |           console.log('✅ Both program-fees and payment-methods/fees APIs confirmed after card selection');
  1515 |         }
  1516 | 
  1517 |         // Process the payment-methods/fees response to determine percentage and assert UI text
  1518 |         const feeJson = await paymentMethodsFeesResponse.json().catch(() => null);
  1519 |         this.lastCardFeeResponse = feeJson;
  1520 |         this.lastFeesApiResponse = feeJson;
  1521 |         let rawPct = undefined;
  1522 |         // Common paths
  1523 |         if (feeJson) {
  1524 |           // Direct numeric
  1525 |           if (typeof feeJson.percentageFeeRate === 'number') rawPct = feeJson.percentageFeeRate;
  1526 |           // Direct string convertible
  1527 |           else if (typeof feeJson.percentageFeeRate === 'string' && !isNaN(parseFloat(feeJson.percentageFeeRate))) rawPct = parseFloat(feeJson.percentageFeeRate);
  1528 |           // data level
  1529 |           else if (feeJson.data && typeof feeJson.data.percentageFeeRate === 'number') rawPct = feeJson.data.percentageFeeRate;
  1530 |           else if (feeJson.data && typeof feeJson.data.percentageFeeRate === 'string' && !isNaN(parseFloat(feeJson.data.percentageFeeRate))) rawPct = parseFloat(feeJson.data.percentageFeeRate);
  1531 |           // fee container
  1532 |           else if (feeJson.fee && typeof feeJson.fee.percentageFeeRate === 'number') rawPct = feeJson.fee.percentageFeeRate;
  1533 |           else if (feeJson.fee && typeof feeJson.fee.percentageFeeRate === 'string' && !isNaN(parseFloat(feeJson.fee.percentageFeeRate))) rawPct = parseFloat(feeJson.fee.percentageFeeRate);
  1534 |           // Typical payment-methods/fees structure: data.paymentSources[0].percentageFeeRate
  1535 |           else if (feeJson.data && Array.isArray(feeJson.data.paymentSources)) {
  1536 |             for (const src of feeJson.data.paymentSources) {
  1537 |               if (src && src.percentageFeeRate !== undefined) {
  1538 |                 if (typeof src.percentageFeeRate === 'number') {
  1539 |                   rawPct = src.percentageFeeRate;
  1540 |                   break;
  1541 |                 }
  1542 |                 if (typeof src.percentageFeeRate === 'string' && !isNaN(parseFloat(src.percentageFeeRate))) {
  1543 |                   rawPct = parseFloat(src.percentageFeeRate);
  1544 |                   break;
  1545 |                 }
  1546 |               }
  1547 |               // Alternate key 'percentage' sometimes used
  1548 |               if (src && src.percentage !== undefined) {
  1549 |                 if (typeof src.percentage === 'number') {
  1550 |                   rawPct = src.percentage;
  1551 |                   break;
  1552 |                 }
  1553 |                 if (typeof src.percentage === 'string' && !isNaN(parseFloat(src.percentage))) {
  1554 |                   rawPct = parseFloat(src.percentage);
  1555 |                   break;
  1556 |                 }
  1557 |               }
  1558 |             }
  1559 |           } else {
  1560 |             // Fallback: scan for first numeric key matching /percentage.*fee/i
  1561 |             const stack = [feeJson];
  1562 |             while (stack.length && rawPct === undefined) {
  1563 |               const node = stack.pop();
  1564 |               if (node && typeof node === 'object') {
  1565 |                 for (const [k, v] of Object.entries(node)) {
  1566 |                   if (rawPct !== undefined) break;
  1567 |                   if (typeof v === 'number' && /percentage.*fee/i.test(k)) {
  1568 |                     rawPct = v;
  1569 |                     break;
  1570 |                   }
  1571 |                   if (v && typeof v === 'object') stack.push(v);
  1572 |                 }
  1573 |               }
  1574 |             }
  1575 |           }
  1576 |         }
  1577 |         if (rawPct !== undefined) {
  1578 |           // If rawPct appears to be a fraction (<1), convert to percentage
  1579 |           const pct = rawPct < 1 ? rawPct * 100 : rawPct;
  1580 |           // Format to 3 decimal places to match API precision (e.g., 2.145%)
  1581 |           // Then remove trailing zeros (e.g., 2.140% -> 2.14%, 2.000% -> 2%)
  1582 |           let pctFormatted = pct.toFixed(3);
  1583 |           // Remove trailing zeros after decimal point
  1584 |           pctFormatted = pctFormatted.replace(/\.?0+$/, '');
  1585 |           // If it ends with .00, remove it (e.g., "1.00" -> "1")
  1586 |           if (pctFormatted.endsWith('.00')) {
  1587 |             pctFormatted = pctFormatted.slice(0, -3);
  1588 |           }
  1589 |           // Wait for the fee text to appear and assert it contains expected percentage
  1590 |           // AU uses "GST", US uses "Sales Tax"
  1591 |           await this.processingFeeText.waitFor({ state: 'visible', timeout: 5000 });
  1592 |           // Check if text contains the percentage - don't enforce exact tax label (GST vs Sales Tax)
  1593 |           await expect(this.processingFeeText).toContainText(`${pctFormatted}%`);
  1594 |           // log removed: verified processing fee percentage
  1595 |         } else {
```