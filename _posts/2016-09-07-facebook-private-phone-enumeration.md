---
layout: post
title: Facebook Private Phone Number Enumeration
---

I started playing around with the Facebook bug bounty a few weeks ago and submitted a few issues that I considered bugs but wasn't sure if Facebook would. I wanted to get an idea about what they considered a security/privacy issue and what they did not. Based on Facebook's [bug bounty details](https://www.facebook.com/whitehat), vulnerabilities that reveal public information are not eligible for the bug bounty program. Public information includes your profile picture, username, ID, name, current cover photo, gender, and anything you've shared publicly.

While playing around with the account recovery feature of Facebook I noted that you could enter either an email address or a phone number and it would return a list of users that are related to the information provided. This allows you to choose your account and continue the account recovery process. I decided to try a little experiment with my account created specifically for bug hunting. This account had no data associated with me except my email address. I entered my email address in the account recovery form and immediately found my account. This email address is my primary contact information so I can't make it non-public.

Next, I decided to add my mobile phone number and I set it to Only Me, which implies the phone number is not public. Based on my email interchange with Facebook, they disagree. Anyway, I returned back to the account recovery page and entered what I thought was my private phone number. Facebook immediately brought up my account using the phone number. I then deleted the phone number from my account and tried again. Facebook still associated my private phone number with my account.

At this point I realized that anyone who added a phone number to Facebook expecting it to be private (Only Me) would have that private number associated with their account. If you could enumerate a large number of accounts using the phone number then you could associate users with phone numbers they haven't made public. I submitted a report to Facebook to inform them that I could enumerate private information and they said,

> I'm sorry, but we will not reward this submission. Information about recovering an account (ex: discovering another user's recovery question or viewing some of their friends to recover an account) isn't a security vulnerability on its own, as Facebook doesn't guarantee the privacy of this information and it's not considered sensitive.

> Also, there are protections for account recovery information. For example, before showing security questions or friends to unlock an account, we check if the request seems legitimate. Legitimacy is determined by a number of factors like IP and information about the computer being used to log in. There are also protections which would stop any larger-scale abuse of this feature.

I think they missed the point. I don't care that I can view friends, recovery questions, etc. I care that a "private" phone number I gave to Facebook is publicly associated with my account. I then asked,

> If I can show that your protections against large scale abuse of
enumeration are not effective would that make a difference?

Their response was,

> Thank you for the proof-of-concept code! One of the reasons we don't consider this as qualifying under our bug bounty program is that we have rate limiting in place which would kick in once you submitted enough requests. The code may work for a small amount of phone numbers, but you wouldn't be able to enumerate a large batch.

> As mentioned by Samuel, we also only show certain recovery options based on numerous factors including whether you've logged in on a specific machine before, or on the same network.

Facebook has the final say in all bug bounty submissions and even though I was frustrated, I dropped it and asked for permission to disclose. Since Facebook does not consider this a security or privacy issue they granted permission.

If you'd like to test this out yourself, add a phone number to your account and set the permissions to Only Me. You should then be able to logout and attempt an account recovery using the phone number you provided. If you'd like to try this at a larger scale you can use the proof of concept code on [GitHub](https://github.com/averagesecurityguy/pocs/blob/master/fb_phone_enum.py).

Here's some sample output from the script:

    $ python fb_phone_enum.py
    4233103102
    ==========
    Heather AndLuis Rojas - https://www.facebook.com/profile/pic.php?cuid=AYiKBhR95ZslM8LR_MDEz0dA0z-yb5-aO_OrZ7A7scnGqJM3ORm7elou0oNC4XReyxanVoqWq-LcluyZyWl-yXlmNOhOCWMMLdy_oK37lgEobbMG7vdNITFgsG9dCDDVG1VyaTFsOq_pJkgnW_02vU9B_VTyBwMyUh27H0YL2Jxirw

    4233103103
    ==========
    4233103103 - None

    4233103105
    ==========
    Kenneth Walker - https://www.facebook.com/profile/pic.php?cuid=AYi1Wew0LNbw2QuBdUZeDlmMpG7_vDEoffe9TMdJK8MPuTW_HVNMSLyfaBSw7K0brjBrWu9N_trDMpZL7q4ZAbe4MopDGLObTeJyV7ECtcBvPsDx_2MuqEEk9nfFEkPAeo5fAnzVz18FC08szzQB2fK-K52p4KCT4-OVcXnYntyWvA

    4233103106
    ==========
    Suzanne Churlik - https://www.facebook.com/profile/pic.php?cuid=AYjIDFk4u58z-4PCVaaiWR4mt4t8kDLyObehJn_1F2Sy6Gp-fyZc9YLIboh2Pj3_96UYYO849564mrmWflIVblFX7F5J_v3YqJYRKcYRgMQF88OCdIFZTo6wO7iMDNphy4mi48k9isb5Dtt9FEsF2sIifXCz2pkbKJtkL8xIBJyGWQ

Happy Hunting.
