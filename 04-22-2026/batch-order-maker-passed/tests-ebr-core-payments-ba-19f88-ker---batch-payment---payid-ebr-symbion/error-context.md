# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: tests/ebr/core/payments/batch-order.spec.js >> authorised maker - batch payment - payid
- Location: utils/ebr/runtime-skip.js:344:14

# Error details

```
Error: page.waitForResponse: Target page, context or browser has been closed
```

# Test source

```ts
  664 |     return calculateAbaTotal(filePath);
  665 |   }
  666 | }
  667 | 
  668 | /**
  669 |  * Count payments based on file type
  670 |  */
  671 | function countBatchPayments(filePath) {
  672 |   if (filePath.endsWith('.ach')) {
  673 |     return countAchPayments(filePath);
  674 |   } else {
  675 |     return countAbaPayments(filePath);
  676 |   }
  677 | }
  678 | 
  679 | /**
  680 |  * Fetch entity name from API for a given ABN
  681 |  */
  682 | async function fetchEntityName(page, abn, timeout) {
  683 |   const apiTimeout = timeout || 60000;
  684 | 
  685 |   try {
  686 |     const response = await page.request.get(`/v3/business-number/${abn}`, { timeout: apiTimeout });
  687 |     const businessData = await response.json();
  688 |     const entityName = businessData.data.entityName;
  689 |     return entityName;
  690 |   } catch (error) {
  691 |     console.log(`⚠️ Could not fetch entity name for ABN ${abn}`);
  692 |     return null;
  693 |   }
  694 | }
  695 | 
  696 | // ===== SHARED STATE FOR TEST COORDINATION =====
  697 | let batchFileUploaded = false; // Track if batch file is already uploaded
  698 | let uploadedFileName = ''; // Store the uploaded file name
  699 | let batchDescription = ''; // Store the batch description from ABA/ACH file
  700 | 
  701 | // ===== TESTS =====
  702 | 
  703 | for (const data of rows) {
  704 |   test(data.title, async ({ page }, testInfo) => {
  705 |     test.slow();
  706 |     test.setTimeout(500000);
  707 | 
  708 |     const paymentsMakePage = new PaymentsMakePage(page);
  709 |     let paymentsSummaryPage;
  710 |     const paymentsConfirmationPage = new PaymentsConfirmationPage(page);
  711 |     const paymentsPayIdPage = new PaymentsPayIdPage(page);
  712 |     const paymentsPbaPage = new PaymentsPbaPage(page);
  713 | 
  714 |     // Resolve country from provider config first (e.g. config/ebr/ach.json), fallback to project name.
  715 |     let country = 'AU';
  716 |     try {
  717 |       const { country: configuredCountry } = await getProjectConfig(testInfo, 'country');
  718 |       country = String(configuredCountry || 'AU').toUpperCase() === 'US' ? 'US' : 'AU';
  719 |     } catch (error) {
  720 |       const projectName = (testInfo.project?.name || '').toLowerCase();
  721 |       country = projectName.includes('us') ? 'US' : 'AU';
  722 |       console.warn(`⚠️ Failed to read country from config; fallback to project name detection: ${error.message}`);
  723 |     }
  724 |     const countryCode = country === 'US' ? 'us' : 'au';
  725 |     console.log(`🌍 Country detected for batch upload: ${country}`);
  726 | 
  727 |     // Build payment data with country-specific card details
  728 |     const paymentData = /** @type {any} */ ({ ...commonData, ...data });
  729 | 
  730 |     // Add cardLast4 for card payments based on country
  731 |     if (paymentData.cardBrand && cardDetails[paymentData.cardBrand]) {
  732 |       const cardInfo = cardDetails[paymentData.cardBrand][countryCode];
  733 |       if (cardInfo) {
  734 |         paymentData.cardLast4 = cardInfo.cardLast4;
  735 |       }
  736 |     }
  737 | 
  738 |     let batchPaymentFilePath;
  739 |     if (country === 'US') {
  740 |       batchPaymentFilePath = '../../../../fixtures/test-data/ebr/us-1Payee.ach';
  741 |     } else {
  742 |       batchPaymentFilePath = '../../../../fixtures/test-data/ebr/au-1Payee.aba';
  743 |     }
  744 | 
  745 |     // Set correct upload button text based on country
  746 |     const uploadButtonText = country === 'US' ? 'Upload ACH file' : 'Upload ABA file';
  747 | 
  748 |     // Get file path and name
  749 |     const filePath = path.join(__dirname, batchPaymentFilePath);
  750 |     const fileName = path.basename(filePath);
  751 | 
  752 |     // Calculate batch totals BEFORE test execution (will be used for verification)
  753 |     const batchTotalAmount = calculateBatchTotal(filePath);
  754 |     const batchTotalPayments = countBatchPayments(filePath);
  755 | 
  756 |     console.log(`📊 Batch file info: ${fileName}, Payments: ${batchTotalPayments}, Total: ${batchTotalAmount}`);
  757 | 
  758 |     await page.goto('/');
  759 | 
  760 |     // Create PaymentsSummaryPage early to capture membership tier from API
  761 |     paymentsSummaryPage = new PaymentsSummaryPage(page);
  762 | 
  763 |     // Wait for user-details API response to capture membership tier
> 764 |     await page.waitForResponse((r) => r.url().includes('/v3/user-details') && r.request().method() === 'GET' && r.status() === 200, { timeout: 60000 });
      |                ^ Error: page.waitForResponse: Target page, context or browser has been closed
  765 | 
  766 |     // Add a small wait to ensure UI is stable after API response
  767 |     await page.waitForTimeout(1000);
  768 | 
  769 |     // Check if this is an authorised user session
  770 |     const membershipTier = paymentsSummaryPage.cachedMembershipTierName || '';
  771 |     console.log(`🔍 Membership tier detected: ${membershipTier}`);
  772 | 
  773 |     if (membershipTier === 'AUTHORISED-USER') {
  774 |       console.log('🎯 Authorised user detected, checking for Status: Active element');
  775 | 
  776 |       const userCardExists = await page
  777 |         .getByText('Status: Active')
  778 |         .first()
  779 |         .waitFor({ state: 'visible', timeout: 30000 })
  780 |         .then(() => true)
  781 |         .catch(() => false);
  782 | 
  783 |       if (userCardExists) {
  784 |         console.log('✅ Found authorised user card, clicking Status: Active');
  785 |         const balanceResponsePromise = page.waitForResponse((response) => response.request().method() === 'GET' && response.url().includes('/v3/points/balance') && response.status() === 200, { timeout: 60000 });
  786 | 
  787 |         await page.getByText('Status: Active').first().click();
  788 | 
  789 |         const balanceResponse = await balanceResponsePromise;
  790 |         const balanceRequestHeaders = await balanceResponse.request().allHeaders();
  791 |         logJwtScopeFromAuthorizationHeader(balanceRequestHeaders.authorization);
  792 |       } else {
  793 |         console.log('ℹ️ No Status: Active element found');
  794 |       }
  795 |     } else {
  796 |       console.log('ℹ️ Not an authorised user session, skipping authorised user logic');
  797 |     }
  798 | 
  799 |     // Re-read tier after authorised user flow — clicking Status: Active triggers a second
  800 |     // /v3/user-details response that updates the cached tier (e.g. AUTHORISED-USER → EXECUTIVE)
  801 |     const effectiveMembershipTier = paymentsSummaryPage.cachedMembershipTierName || membershipTier;
  802 |     console.log(`🔍 Effective membership tier for PayID routing: ${effectiveMembershipTier}`);
  803 | 
  804 |     // EXECUTIVE tier: PayID has no additional funding source selection — skip split-payid cases
  805 |     if (effectiveMembershipTier === 'EXECUTIVE' && paymentData.method === 'payid' && paymentData.additionalMethod !== null) {
  806 |       test.skip(true, `EXECUTIVE tier: PayID does not support additional funding source selection (additionalMethod: ${paymentData.additionalMethod})`);
  807 |       return;
  808 |     }
  809 | 
  810 |     // Non-EXECUTIVE tier: PayID always requires a funding source — skip the no-additionalMethod case
  811 |     if (effectiveMembershipTier !== 'EXECUTIVE' && paymentData.method === 'payid' && paymentData.additionalMethod === null) {
  812 |       test.skip(true, `Non-EXECUTIVE tier (${effectiveMembershipTier}): PayID requires an additional funding source selection`);
  813 |       return;
  814 |     }
  815 | 
  816 |     // Match payment-order timing: only install make-payment mocks after the
  817 |     // landing-page authorised-user selection has had a chance to render.
  818 |     await mocksForMakePayment(page);
  819 |     const batchPaymentLink = page.getByRole('link', { name: 'Batch payment' });
  820 |     await expect(batchPaymentLink).toBeVisible({ timeout: 30000 });
  821 |     await batchPaymentLink.click({ timeout: 15000 });
  822 | 
  823 |     // Wait for batch orders API to load
  824 |     await page.waitForResponse((r) => r.url().includes('/batch-orders') && r.request().method() === 'GET' && r.status() === 200, { timeout: 30000 });
  825 | 
  826 |     console.log('\n🔍 Resolving batch entry state...');
  827 | 
  828 |     const uploadedFileDetailsLocator = page.locator('#sidebar-content').getByText('Uploaded file details');
  829 |     const batchEntryState = await resolveBatchEntryState(page, uploadButtonText, { timeout: 30000 });
  830 |     const isFileAlreadyUploaded = batchEntryState === 'existing-upload';
  831 | 
  832 |     console.log(`🔍 Batch entry state: ${batchEntryState}`);
  833 | 
  834 |     // The page state is more reliable than the shared cache flag. If the UI is
  835 |     // asking for a new upload, clear any stale "already uploaded" state left by
  836 |     // a previous test in the same worker.
  837 |     if (!isFileAlreadyUploaded && batchFileUploaded) {
  838 |       console.log('⚠️ Shared batch upload cache is stale; UI still requires a file upload. Resetting cached upload state.');
  839 |       batchFileUploaded = false;
  840 |       uploadedFileName = '';
  841 |       batchDescription = '';
  842 |     }
  843 | 
  844 |     if (isFileAlreadyUploaded) {
  845 |       console.log('✅ "Uploaded file details" found, reusing existing upload...');
  846 | 
  847 |       if (!batchFileUploaded) {
  848 |         const description = extractBatchDescription(filePath);
  849 |         batchDescription = description;
  850 |         uploadedFileName = fileName;
  851 |         console.log(`📋 Using existing uploaded file: ${fileName}`);
  852 |       } else {
  853 |         console.log(`📋 Reusing previously uploaded file: ${uploadedFileName}`);
  854 |       }
  855 | 
  856 |       await continueBatchFlowIfNeeded(page, { timeout: 30000, label: 'Existing Upload Route' });
  857 | 
  858 |       await expect(page.locator('form')).toContainText(`Batch file: ${uploadedFileName}`, { timeout: 20000 });
  859 |       console.log('✅ Payment form loaded from existing upload');
  860 | 
  861 |       // Select business (paying for) if dropdown is present
  862 |       await paymentsMakePage.selectPayingFor();
  863 | 
  864 |       // ✅ CRITICAL: Set flag to prevent Route 2 from executing
```