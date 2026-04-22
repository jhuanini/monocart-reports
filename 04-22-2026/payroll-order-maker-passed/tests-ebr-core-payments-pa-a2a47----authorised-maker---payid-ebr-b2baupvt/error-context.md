# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: tests/ebr/core/payments/payroll-order.spec.js >> Payroll payment - authorised maker - payid
- Location: utils/ebr/runtime-skip.js:344:14

# Error details

```
Error: page.waitForResponse: Target page, context or browser has been closed
```

# Test source

```ts
  606 | /**
  607 |  * Count total payments in ACH file
  608 |  */
  609 | function countAchPayments(filePath) {
  610 |   const fileContent = fs.readFileSync(filePath, 'utf-8');
  611 |   const lines = fileContent.split('\n');
  612 |   let count = 0;
  613 | 
  614 |   for (const line of lines) {
  615 |     if (line.startsWith('6')) {
  616 |       count++;
  617 |     }
  618 |   }
  619 | 
  620 |   return count;
  621 | }
  622 | 
  623 | /**
  624 |  * Calculate total amount based on file type
  625 |  */
  626 | function calculateBatchTotal(filePath) {
  627 |   if (filePath.endsWith('.ach')) {
  628 |     return calculateAchTotal(filePath);
  629 |   } else {
  630 |     return calculateAbaTotal(filePath);
  631 |   }
  632 | }
  633 | 
  634 | /**
  635 |  * Count payments based on file type
  636 |  */
  637 | function countBatchPayments(filePath) {
  638 |   if (filePath.endsWith('.ach')) {
  639 |     return countAchPayments(filePath);
  640 |   } else {
  641 |     return countAbaPayments(filePath);
  642 |   }
  643 | }
  644 | 
  645 | // ===== SHARED STATE FOR TEST COORDINATION =====
  646 | let batchFileUploaded = false;
  647 | let uploadedFileName = '';
  648 | let batchDescription = '';
  649 | 
  650 | // ===== TESTS =====
  651 | 
  652 | for (const data of rows) {
  653 |   test(data.title, async ({ page }, testInfo) => {
  654 |     test.slow();
  655 |     test.setTimeout(500000);
  656 |     const runtimeTestInfo = forcedProject.buildTestInfo(testInfo);
  657 | 
  658 |     const paymentsMakePage = new PaymentsMakePage(page);
  659 |     let paymentsSummaryPage;
  660 |     const paymentsConfirmationPage = new PaymentsConfirmationPage(page);
  661 |     const paymentsPayIdPage = new PaymentsPayIdPage(page);
  662 |     const paymentsPbaPage = new PaymentsPbaPage(page);
  663 | 
  664 |     // Detect country from project name
  665 |     const projectName = (runtimeTestInfo.project?.name || '').toLowerCase();
  666 |     const country = projectName.includes('us') ? 'US' : 'AU';
  667 |     const countryCode = country === 'US' ? 'us' : 'au';
  668 |     console.log(`🌍 Country detected for payroll upload: ${country}`);
  669 | 
  670 |     // Build payment data with country-specific card details
  671 |     const paymentData = /** @type {any} */ ({ ...commonData, ...data });
  672 | 
  673 |     if (paymentData.cardBrand && cardDetails[paymentData.cardBrand]) {
  674 |       const cardInfo = cardDetails[paymentData.cardBrand][countryCode];
  675 |       if (cardInfo) {
  676 |         paymentData.cardLast4 = cardInfo.cardLast4;
  677 |       }
  678 |     }
  679 | 
  680 |     let batchPaymentFilePath;
  681 |     if (country === 'US') {
  682 |       batchPaymentFilePath = '../../../../fixtures/test-data/ebr/us-22Payees.ach';
  683 |     } else {
  684 |       batchPaymentFilePath = '../../../../fixtures/test-data/ebr/au-1Payee.aba';
  685 |     }
  686 | 
  687 |     // Set correct upload button text based on country
  688 |     const uploadButtonText = country === 'US' ? 'Upload ACH file' : 'Upload ABA file';
  689 | 
  690 |     // Get file path and name
  691 |     const filePath = path.join(__dirname, batchPaymentFilePath);
  692 |     const fileName = path.basename(filePath);
  693 | 
  694 |     // Calculate batch totals BEFORE test execution (will be used for verification)
  695 |     const batchTotalAmount = calculateBatchTotal(filePath);
  696 |     const batchTotalPayments = countBatchPayments(filePath);
  697 | 
  698 |     console.log(`📊 Payroll file info: ${fileName}, Payments: ${batchTotalPayments}, Total: ${batchTotalAmount}`);
  699 | 
  700 |     await page.goto('/');
  701 | 
  702 |     // Create PaymentsSummaryPage early to capture membership tier from API
  703 |     paymentsSummaryPage = new PaymentsSummaryPage(page);
  704 | 
  705 |     // Wait for user-details API response to capture membership tier
> 706 |     await page.waitForResponse((r) => r.url().includes('/v3/user-details') && r.request().method() === 'GET' && r.status() === 200, { timeout: 60000 });
      |                ^ Error: page.waitForResponse: Target page, context or browser has been closed
  707 | 
  708 |     // Add a small wait to ensure UI is stable after API response
  709 |     await page.waitForTimeout(1000);
  710 | 
  711 |     // Check if this is an authorised user session
  712 |     const membershipTier = paymentsSummaryPage.cachedMembershipTierName || '';
  713 |     console.log(`🔍 Membership tier detected: ${membershipTier}`);
  714 | 
  715 |     if (membershipTier === 'AUTHORISED-USER') {
  716 |       console.log('🎯 Authorised user detected, checking for Status: Active element');
  717 | 
  718 |       const userCardExists = await page
  719 |         .getByText('Status: Active')
  720 |         .first()
  721 |         .waitFor({ state: 'visible', timeout: 30000 })
  722 |         .then(() => true)
  723 |         .catch(() => false);
  724 | 
  725 |       if (userCardExists) {
  726 |         console.log('✅ Found authorised user card, clicking Status: Active');
  727 |         const balanceResponsePromise = page.waitForResponse((response) => response.request().method() === 'GET' && response.url().includes('/v3/points/balance') && response.status() === 200, { timeout: 60000 });
  728 | 
  729 |         await page.getByText('Status: Active').first().click();
  730 | 
  731 |         const balanceResponse = await balanceResponsePromise;
  732 |         const balanceRequestHeaders = await balanceResponse.request().allHeaders();
  733 |         logJwtScopeFromAuthorizationHeader(balanceRequestHeaders.authorization);
  734 |       } else {
  735 |         console.log('ℹ️ No Status: Active element found');
  736 |       }
  737 |     } else {
  738 |       console.log('ℹ️ Not an authorised user session, skipping authorised user logic');
  739 |     }
  740 | 
  741 |     // Re-read tier after authorised user flow — clicking Status: Active triggers a second
  742 |     // /v3/user-details response that updates the cached tier (e.g. AUTHORISED-USER → EXECUTIVE)
  743 |     const effectiveMembershipTier = paymentsSummaryPage.cachedMembershipTierName || membershipTier;
  744 |     console.log(`🔍 Effective membership tier for PayID routing: ${effectiveMembershipTier}`);
  745 | 
  746 |     // EXECUTIVE tier: PayID has no additional funding source selection — skip split-payid cases
  747 |     if (effectiveMembershipTier === 'EXECUTIVE' && paymentData.method === 'payid' && paymentData.additionalMethod !== null) {
  748 |       test.skip(true, `EXECUTIVE tier: PayID does not support additional funding source selection (additionalMethod: ${paymentData.additionalMethod})`);
  749 |       return;
  750 |     }
  751 | 
  752 |     // Non-EXECUTIVE tier: PayID always requires a funding source — skip the no-additionalMethod case
  753 |     if (effectiveMembershipTier !== 'EXECUTIVE' && paymentData.method === 'payid' && paymentData.additionalMethod === null) {
  754 |       test.skip(true, `Non-EXECUTIVE tier (${effectiveMembershipTier}): PayID requires an additional funding source selection`);
  755 |       return;
  756 |     }
  757 | 
  758 |     // Match payment-order timing: only install make-payment mocks after the
  759 |     // landing-page authorised-user selection has had a chance to render.
  760 |     await mocksForMakePayment(page);
  761 |     const payrollPaymentLink = page.getByRole('link', { name: 'Pay your payroll' });
  762 |     await expect(payrollPaymentLink).toBeVisible({ timeout: 30000 });
  763 |     await payrollPaymentLink.click({ timeout: 15000 });
  764 | 
  765 |     // Wait for batch orders API to load
  766 |     await page.waitForResponse((r) => r.url().includes('/batch-orders') && r.request().method() === 'GET' && r.status() === 200, { timeout: 30000 });
  767 | 
  768 |     console.log('\n🔍 Resolving payroll entry state...');
  769 | 
  770 |     const batchEntryState = await resolveBatchEntryState(page, uploadButtonText, { timeout: 30000 });
  771 |     const isFileAlreadyUploaded = batchEntryState === 'existing-upload';
  772 | 
  773 |     console.log(`🔍 Payroll entry state: ${batchEntryState}`);
  774 | 
  775 |     // The page state is more reliable than the shared cache flag. If the UI is
  776 |     // asking for a new upload, clear any stale "already uploaded" state left by
  777 |     // a previous test in the same worker.
  778 |     if (!isFileAlreadyUploaded && batchFileUploaded) {
  779 |       console.log('⚠️ Shared payroll upload cache is stale; UI still requires a file upload. Resetting cached upload state.');
  780 |       batchFileUploaded = false;
  781 |       uploadedFileName = '';
  782 |       batchDescription = '';
  783 |     }
  784 | 
  785 |     if (isFileAlreadyUploaded) {
  786 |       console.log('✅ "Uploaded file details" found, reusing existing payroll upload...');
  787 | 
  788 |       if (!batchFileUploaded) {
  789 |         const description = extractBatchDescription(filePath);
  790 |         batchDescription = description;
  791 |         uploadedFileName = fileName;
  792 |         console.log(`📋 Using existing uploaded file: ${fileName}`);
  793 |       } else {
  794 |         console.log(`📋 Reusing previously uploaded file: ${uploadedFileName}`);
  795 |       }
  796 | 
  797 |       await continueBatchFlowIfNeeded(page, { timeout: 30000, label: 'Existing Upload Route' });
  798 | 
  799 |       await expect(page.locator('form')).toContainText(`Payroll file: ${uploadedFileName}`, { timeout: 20000 });
  800 |       console.log('✅ Payment form loaded from existing upload');
  801 | 
  802 |       // Select business (paying for) if dropdown is present
  803 |       await paymentsMakePage.selectPayingFor();
  804 | 
  805 |       // ✅ CRITICAL: Set flag to prevent Route 2 from executing
  806 |       batchFileUploaded = true;
```