# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: tests/ebr/core/payments/payment-order.spec.js >> bpay - bank - schedule
- Location: utils/ebr/runtime-skip.js:320:12

# Error details

```
TimeoutError: page.waitForResponse: Timeout 60000ms exceeded while waiting for event "response"
```

# Page snapshot

```yaml
- generic [active] [ref=e1]:
  - generic [ref=e3]:
    - banner [ref=e4]:
      - generic [ref=e5]:
        - link "Go to Home" [ref=e6] [cursor=pointer]:
          - /url: /
          - img "Symbion Elite Rewards Logo" [ref=e8]
        - generic [ref=e9]:
          - button "PLATINUM" [ref=e10] [cursor=pointer]:
            - button "PLATINUM" [ref=e11]:
              - generic [ref=e13]:
                - img [ref=e15]
                - paragraph [ref=e34]: PLATINUM
          - button "Action" [ref=e36] [cursor=pointer]:
            - paragraph [ref=e37]: 1,526,903 PTS
        - generic [ref=e38]:
          - button "Notifications" [ref=e40] [cursor=pointer]:
            - img [ref=e42]
          - button "Show cart" [ref=e46] [cursor=pointer]:
            - img [ref=e48]
          - button "Show eWallet" [ref=e52] [cursor=pointer]:
            - img "avatar" [ref=e56]
    - main [ref=e58]:
      - generic [ref=e60]:
        - generic [ref=e61]:
          - navigation "Benefits" [ref=e63]:
            - link "Home" [ref=e64] [cursor=pointer]:
              - /url: /
              - generic [ref=e65]:
                - img
              - generic [ref=e66]: Home
            - link "Make a payment" [ref=e67] [cursor=pointer]:
              - /url: /payments/make
              - generic [ref=e68]:
                - img
              - generic [ref=e69]: Make a payment
            - button "Payment methods" [ref=e70] [cursor=pointer]:
              - img [ref=e72]
              - generic [ref=e74]: Payment methods
            - link "Statement accounts" [ref=e75] [cursor=pointer]:
              - /url: /statements
              - generic [ref=e76]:
                - img
              - generic [ref=e77]: Statement accounts
            - link "Payees" [ref=e78] [cursor=pointer]:
              - /url: /payments/payees
              - generic [ref=e79]:
                - img
              - generic [ref=e80]: Payees
            - link "Scheduled payments" [ref=e81] [cursor=pointer]:
              - /url: /scheduled-payments
              - generic [ref=e82]:
                - img
              - generic [ref=e83]: Scheduled payments
            - link "Batch payment" [ref=e84] [cursor=pointer]:
              - /url: /bank-file-upload
              - generic [ref=e85]:
                - img
              - generic [ref=e86]: Batch payment
            - link "Approve payments" [ref=e87] [cursor=pointer]:
              - /url: /pending-approval-orders
              - generic [ref=e88]:
                - img
              - generic [ref=e89]: Approve payments
            - link "Rewards" [ref=e91] [cursor=pointer]:
              - /url: /gift-cards
              - generic [ref=e92]:
                - img
              - generic [ref=e93]: Rewards
            - link "Experiences" [ref=e94] [cursor=pointer]:
              - /url: /competitions
              - generic [ref=e95]:
                - img
              - generic [ref=e96]: Experiences
            - link "BizHub" [ref=e97] [cursor=pointer]:
              - /url: /community-hub
              - generic [ref=e98]:
                - img
              - generic [ref=e99]: BizHub
            - link "Transfer my points" [ref=e101] [cursor=pointer]:
              - /url: /points-programs
              - generic [ref=e102]:
                - img
              - generic [ref=e103]: Transfer my points
            - link "TravelHub" [ref=e104] [cursor=pointer]:
              - /url: /travel-hub
              - generic [ref=e105]:
                - img
              - generic [ref=e106]: TravelHub
            - link "Activity" [ref=e108] [cursor=pointer]:
              - /url: /activity
              - generic [ref=e109]:
                - img
              - generic [ref=e110]: Activity
          - generic [ref=e114]:
            - generic [ref=e118]:
              - generic [ref=e119]:
                - paragraph [ref=e121]: Bill payments overview
                - generic [ref=e122]:
                  - combobox [ref=e123] [cursor=pointer]:
                    - option "Filter By:" [disabled]
                    - option "Last 7 days"
                    - option "Last 30 days" [selected]
                    - option "Last 60 days"
                    - option "Last 90 days"
                    - option "All"
                  - generic:
                    - generic:
                      - img
              - generic [ref=e124]:
                - generic [ref=e125]:
                  - generic [ref=e126]:
                    - img [ref=e128]
                    - generic [ref=e131]: Total bill payments
                  - generic [ref=e133]: $104,395.44
                - generic [ref=e134]:
                  - generic [ref=e135]:
                    - img [ref=e137]
                    - generic [ref=e140]: Transaction volume
                  - generic [ref=e142]: "94"
                - generic [ref=e143]:
                  - generic [ref=e144]:
                    - img [ref=e147]
                    - generic [ref=e166]: Points earned
                  - generic [ref=e167]:
                    - generic [ref=e168]: 102,664
                    - generic [ref=e169]: PTS
              - list [ref=e174]:
                - listitem [ref=e175] [cursor=pointer]:
                  - paragraph [ref=e178]: Total Amount
                - listitem [ref=e179] [cursor=pointer]:
                  - paragraph [ref=e182]: Points Balance
            - generic [ref=e184]:
              - link "Find out more" [ref=e186] [cursor=pointer]:
                - /url: https://www.qantas.com/au/en/business-rewards/exclusive-offers/campaign-b2b-2026.html?utm_source=qbr.qantas.com&utm_medium=referral&utm_campaign=B2B2026&utm_content=partnerofferbanner_findoutmore
                - paragraph [ref=e190]: Find out more
              - link "Learn More" [ref=e192] [cursor=pointer]:
                - /url: https://shop.symbion.com.au/promotions/may24_elite-rewards_nutra-life
                - paragraph [ref=e196]: Learn more
              - link "Transfer points" [ref=e198] [cursor=pointer]:
                - /url: /points-programs
                - paragraph [ref=e202]: Transfer points
              - link "See available experiences" [ref=e204] [cursor=pointer]:
                - /url: /competitions
                - paragraph [ref=e208]: See available experiences
        - list [ref=e210]:
          - listitem [ref=e211]:
            - link "How it works" [ref=e212] [cursor=pointer]:
              - /url: https://support.symbionelite.com.au/hc/en-us
              - generic [ref=e213]: How it works
          - listitem [ref=e214]:
            - link "Terms & Conditions" [ref=e215] [cursor=pointer]:
              - /url: /terms-conditions
              - generic [ref=e216]: Terms & Conditions
          - listitem [ref=e217]:
            - link "Privacy Policy" [ref=e218] [cursor=pointer]:
              - /url: /privacy-policy
              - generic [ref=e219]: Privacy Policy
          - listitem [ref=e220]:
            - link "Contact" [ref=e221] [cursor=pointer]:
              - /url: /help
              - generic [ref=e222]: Contact
          - listitem [ref=e223]:
            - button "Action" [ref=e224] [cursor=pointer]: Logout
  - iframe [ref=e225]:
    - button "Support" [ref=f2e4] [cursor=pointer]:
      - img [ref=f2e6]
      - generic [ref=f2e13]: Support
```

# Test source

```ts
  44  |   }
  45  | }
  46  | 
  47  | // // ===== TEST AID: GENERATE VIDEO FOR PASSED TESTS ====
  48  | test.use({
  49  |   video: 'on',
  50  |   // trace: 'on',
  51  | });
  52  | // // =================================================
  53  | 
  54  | test.describe.configure({ retries: 1 });
  55  | 
  56  | const commonData = {
  57  |   description: generateTextFromConfig('bank account', 'description'),
  58  |   reference: generateTextFromConfig('bank account', 'reference'),
  59  |   timing: ['now', 'schedule'],
  60  |   amount: generateNumber(2000, 4, { additionalTwoDecimal: true }),
  61  | };
  62  | 
  63  | // Define payee configurationsa
  64  | const payees = {
  65  |   bankAccount: { payeeType: 'bank account', payeeName: "Don't delete payee" },
  66  |   bpay: { payeeType: 'bpay', payeeName: 'nabtrade' },
  67  | };
  68  | 
  69  | // Extract last 4 digits from bank account numbers (AU and US)
  70  | const bankAccountLast4 = bankAccountNumber.bankAccountNo.map((accountNo) => accountNo.slice(-4));
  71  | 
  72  | // Define payment method configurations
  73  | const paymentMethods = [
  74  |   { method: 'credit', additionalMethod: null, cardBrand: 'Visa', cardConfigs: cardDetails, pointsToRedeem: null },
  75  |   { method: 'credit', additionalMethod: null, cardBrand: 'Amex', cardConfigs: cardDetails, pointsToRedeem: null },
  76  |   { method: 'bank', additionalMethod: null, cardBrand: null, bankAccountNo: bankAccountLast4, pointsToRedeem: null },
  77  |   { method: 'points', additionalMethod: null, cardBrand: null, pointsToRedeem: 'max', amount: generateNumber(5, 1, { additionalTwoDecimal: true }) }, // Override the amount to a smaller one to save points.
  78  |   { method: 'points', additionalMethod: 'credit', cardBrand: 'Mastercard', cardConfigs: cardDetails, pointsToRedeem: generateNumber(20, 5) },
  79  |   { method: 'points', additionalMethod: 'bank', cardBrand: null, bankAccountNo: bankAccountLast4, pointsToRedeem: generateNumber(20, 5, { additionalTwoDecimal: false }) },
  80  |   { method: 'payid', additionalMethod: null, cardBrand: null, pointsToRedeem: null },
  81  |   { method: 'pba', additionalMethod: 'payTo', cardBrand: null, pointsToRedeem: null, amount: generateNumber(900, 4, { additionalTwoDecimal: true }) }, // Override the amount to enable payTo payment.
  82  |   { method: 'pba', additionalMethod: 'BECS', cardBrand: null, pointsToRedeem: null, amount: generateNumber(2000, 1000, { additionalTwoDecimal: true }) }, // Override the amount to enable BECS payment.
  83  | ];
  84  | 
  85  | // Generate payment scenarios by combining payees and payment methods
  86  | const paymentScenarios = Object.values(payees)
  87  |   .flatMap((payee) =>
  88  |     paymentMethods.map((paymentMethod) => ({
  89  |       ...payee,
  90  |       ...paymentMethod,
  91  |     }))
  92  |   )
  93  |   .flatMap((base) =>
  94  |     commonData.timing.map((timing) => {
  95  |       // derive readable label for title
  96  |       let redeemLabel;
  97  |       if (base.method === 'points') {
  98  |         redeemLabel = base.pointsToRedeem === 'max' ? 'max' : 'partial';
  99  |       } else {
  100 |         redeemLabel = null;
  101 |       }
  102 | 
  103 |       return { ...base, timing, redeemLabel };
  104 |     })
  105 |   );
  106 | 
  107 | const rows = buildTestTitles(paymentScenarios, {
  108 |   base: '',
  109 |   keys: ['payeeType', 'method', 'additionalMethod', 'cardBrand', 'redeemLabel', 'timing'],
  110 |   indexDuplicates: true,
  111 | });
  112 | 
  113 | for (const data of rows) {
  114 |   test(data.title, async ({ page }, testInfo) => {
  115 |     test.setTimeout(500000);
  116 | 
  117 |     const paymentsMakePage = new PaymentsMakePage(page);
  118 |     const paymentsConfirmationPage = new PaymentsConfirmationPage(page);
  119 |     const paymentsPayIdPage = new PaymentsPayIdPage(page);
  120 |     const paymentsPbaPage = new PaymentsPbaPage(page);
  121 | 
  122 |     const paymentData = { ...commonData, ...data };
  123 | 
  124 |     // 🔄 RETRY LOGIC: Switch card brand on retry
  125 |     // If this is a retry (retryCount > 0), switch between Visa and Mastercard
  126 |     if (testInfo.retry > 0 && paymentData.cardBrand) {
  127 |       const originalCardBrand = paymentData.cardBrand;
  128 |       if (paymentData.cardBrand === 'Visa') {
  129 |         paymentData.cardBrand = 'Mastercard';
  130 |         console.log(`🔄 RETRY ${testInfo.retry}: Switching card brand from ${originalCardBrand} to Mastercard`);
  131 |       } else if (paymentData.cardBrand === 'Mastercard') {
  132 |         paymentData.cardBrand = 'Visa';
  133 |         console.log(`🔄 RETRY ${testInfo.retry}: Switching card brand from ${originalCardBrand} to Visa`);
  134 |       }
  135 |     }
  136 | 
  137 |     await page.goto('/');
  138 |     // await page.pause(); // Pause at the start of the test for debugging purposes
  139 | 
  140 |     // Create PaymentsSummaryPage early to capture membership tier from API
  141 |     const paymentsSummaryPage = new PaymentsSummaryPage(page);
  142 | 
  143 |     // Wait for user-details API response to capture membership tier
> 144 |     await page.waitForResponse((r) => r.url().includes('/v3/user-details') && r.request().method() === 'GET' && r.status() === 200, { timeout: 60000 });
      |                ^ TimeoutError: page.waitForResponse: Timeout 60000ms exceeded while waiting for event "response"
  145 | 
  146 |     // Wait a brief moment for the API response to be processed
  147 |     await page.waitForTimeout(1000);
  148 | 
  149 |     // Check if this is an authorised user session
  150 |     const membershipTier = paymentsSummaryPage.cachedMembershipTierName || '';
  151 |     console.log(`🔍 Membership tier detected: ${membershipTier}`);
  152 | 
  153 |     if (membershipTier === 'AUTHORISED-USER') {
  154 |       console.log('🎯 Authorised user detected, checking for Status: Active element');
  155 | 
  156 |       // Authorised user selection logic - click Status: Active if it exists
  157 |       const userCardExists = await page
  158 |         .getByText('Status: Active')
  159 |         .first()
  160 |         .waitFor({ state: 'visible', timeout: 30000 })
  161 |         .then(() => true)
  162 |         .catch(() => false);
  163 | 
  164 |       if (userCardExists) {
  165 |         console.log('✅ Found authorised user card, clicking Status: Active');
  166 |         const balanceResponsePromise = page.waitForResponse((response) => response.request().method() === 'GET' && response.url().includes('/v3/points/balance') && response.status() === 200, { timeout: 60000 });
  167 | 
  168 |         await page.getByText('Status: Active').first().click();
  169 | 
  170 |         const balanceResponse = await balanceResponsePromise;
  171 |         const balanceRequestHeaders = await balanceResponse.request().allHeaders();
  172 |         logJwtScopeFromAuthorizationHeader(balanceRequestHeaders.authorization);
  173 |       } else {
  174 |         console.log('ℹ️ No Status: Active element found');
  175 |       }
  176 |     } else {
  177 |       console.log('ℹ️ Not an authorised user session, skipping authorised user logic');
  178 |     }
  179 | 
  180 |     await paymentsMakePage.makeAPayment(/** @type {any} */ (paymentData), testInfo);
  181 |     await paymentsSummaryPage.verifyPaymentSummary(paymentData, paymentsMakePage, testInfo);
  182 |     if (paymentsSummaryPage.shouldEndTestAfterSummary()) {
  183 |       console.log(`ℹ️ Ending test after summary flow: ${paymentsSummaryPage.getSummaryFlowCompletionReason()}`);
  184 |       return;
  185 |     }
  186 |     if (paymentData.method === 'payid') {
  187 |       await paymentsPayIdPage.processPayIdPayment(paymentsSummaryPage, paymentData, testInfo);
  188 |     } else if (paymentData.method === 'pba') {
  189 |       const result = await paymentsPbaPage.completePayToPayment('jhoana.crisostomo@eonx.com', paymentsSummaryPage, paymentData.additionalMethod, testInfo);
  190 | 
  191 |       if (result?.flaky) {
  192 |         test.fixme(true, `PayTo payment failed after multiple retries: ${result.error}`);
  193 |       }
  194 | 
  195 |       // Only continue with further assertions if payment succeeded
  196 |       if (result?.success) {
  197 |         // Add any additional verification here if needed
  198 |       }
  199 |     } else {
  200 |       await paymentsConfirmationPage.verifyPaymentConfirmation(paymentData, paymentsMakePage, paymentsSummaryPage, testInfo);
  201 |     }
  202 | 
  203 |     // DEBUG: For testing purposes only
  204 |     console.log('⏳ Waiting 3 seconds before clicking Done button...');
  205 |     await page.waitForTimeout(3000);
  206 | 
  207 |     // Skip activity page verification for scheduled payments
  208 |     if (paymentData.timing === 'schedule') {
  209 |       console.log('ℹ️ Skipping activity page verification for scheduled payment');
  210 |       return;
  211 |     }
  212 | 
  213 |     await page.getByRole('link', { name: /^(Activity|Reporting)$/ }).click();
  214 | 
  215 |     // Get the captured transaction ID from the appropriate source based on payment method
  216 |     let transactionId;
  217 |     if (paymentData.method === 'payid') {
  218 |       transactionId = paymentsPayIdPage.payIdReference;
  219 |       console.log('🔍 Looking for PayID transaction ID in activity list:', transactionId);
  220 |     } else if (paymentData.method === 'pba') {
  221 |       transactionId = paymentsPbaPage.transactionId;
  222 |       console.log('🔍 Looking for PBA transaction ID in activity list:', transactionId);
  223 |     } else {
  224 |       transactionId = paymentsConfirmationPage.getCapturedTransactionId();
  225 |       console.log('🔍 Looking for transaction ID in activity list:', transactionId);
  226 |     }
  227 | 
  228 |     // ✅ FIRST: Wait for the activity list to load before checking for transaction
  229 |     const maxRetries = 5;
  230 |     let retryCount = 0;
  231 |     let activityListLoaded = false;
  232 | 
  233 |     while (retryCount < maxRetries && !activityListLoaded) {
  234 |       try {
  235 |         await page.waitForSelector('a[href^="/activity/"]', { state: 'visible', timeout: 45000 });
  236 |         console.log(`✅ Activity list loaded (attempt ${retryCount + 1}/${maxRetries})`);
  237 |         activityListLoaded = true;
  238 |       } catch (error) {
  239 |         retryCount++;
  240 |         if (retryCount < maxRetries) {
  241 |           console.log(`⚠️ Activity list did not load within timeout (attempt ${retryCount}/${maxRetries}), reloading page...`);
  242 |           await page.reload();
  243 |         } else {
  244 |           throw new Error(`❌ Activity list failed to load after ${maxRetries} attempts`);
```