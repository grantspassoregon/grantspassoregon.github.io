+++
title = "Announcements for 7/03/2024"
date = 2024-07-03

[taxonomies]
categories = ["News"]
tags = ["News", "Announcements"]

[extra]
author = "Erik Rose"
+++

## Address Verification

One of the primary uses of addresses issued by the city is for emergency response. Although we contract out our emergency dispatch services through Emergency Communications of Southern Oregon (ECSO), as the addressing authority we are responsible for ensuring the addresses that they use are accurate and up-to-date. Discrepancies between our address databases in the past have resulted in avoidable delays during response, emphasizing the fact that inaccuracies are a safety issue.

As a small but growing city, we have many of the address problems that occur at a large federal agency like the USPS, but lack deep pockets to purchase the expensive third-party software they use to manage addresses. Instead, we have been developing our own internal tooling to automate the cross-agency reconciliation process. These tools are not as fancy or feature-rich, but they are getting the job done. Over the past year, we have corrected hundreds of records, including one dating back to 2008.

Earlier this year, ECSO completed an update of their address database to comply with the latest National Emergency Number Association (NENA) standard. This update changes the way they store and report addresses, introducing new fields and altering the way they classify existing street names. Fortunately, Grants Pass moved to a NENA-compliant standard in 2022, so we had a head start tackling the new format from ECSO, but the process still took several weeks. During the update, our code base grew by only 3% to just under 7K LOC, while delivering new features and improving on existing methods. At the same time, our code documentation has increased from 350 to over 1000 lines, making the code easier to learn, maintain and share.

As we grow to better understand the problem space, we continue to improve our methods and increase the efficiency of the process. In additional to reconciling addresses with ECSO, the address code now also validates addresses for business licenses, and calculates the LexisNexis service boundary from the set of valid addresses for emergency response. Over time, we hope that reconciling the address database with our partner agencies can become painless and automated, and that avoidable emergency response delays related to bad address information can become a thing of past.
