# Weak isolation on dual-use endpoint

### Goal - 

Exploit logic flaw to access the admin panel and delete Carlos

### Analysis/Exploitation 

**Login as user **`wiener`**:**

One thing that catches my eye is the password change functionality:

Why does it contain the username as an input field? I'd expect either the password to be changed for the logged-in user, `wiener`. In this case, the input field for the username would be unnecessary.

What happens if I use it and simply change the username to `administrator`?

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/bb5a0148-e37a-4709-9b8f-4255565d4c2e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UR5VBDMY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210447Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIGeSAZSIaqY7k9KYWcEUJyDEIXTPCXnJ8cNLLRwHdALBAiEAygRJaqcYgOneBhna14wPNK5fygchd2XdtRLh7Zc8pKQqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDOoiMEGfXAS6J2%2BK%2BCrcA%2Bq8dFE6hOIs%2B4aLXeVJKlPOo%2Fhwj8IM8DbQXzB3HYoTYGoscCvUL2Rny%2BVmMh0ZfyJtuG5zNPqpMHBZX6NT%2BGCMAmGrQVl3Oz52Sdkz5RR5SZWj6zqedqz2%2Br5xaSZLNE4DRvbBMWSuP4YnTje%2BEvDx2A3w0ssLALAZm%2BWcsYV7M937xcPWntTVfYmiiXDMP8nw%2BbCFz%2FEF96grPrU3m4Ro7kXy7uYh8GaFlQRXaGMr8lWwB7DIMq5JRnNN7PV4NYxdKLCNQc%2Bq2nX7NSvQTtDzQzB3XOKvDh%2BU2i6vJq8vcI%2FXqFA7a6aCWBl0gDlYNdOj1nt0B2Sd6vY%2FsTg5tJ12WybrdaM2fbp4to98bNh7hGBjUidBPi509JCodHv1SGQ4VXO7eH%2FaDzN6ha%2BwWDHEpfgEfSfJWxtzhKyJw9rh3IxG6qp6%2FJKE%2BxzvmUEwvSGvEOrV7qxpQLzcLFBSdPGvjcsfhsWtSv6EZ6heBFtU4y2cIbsqmb16eV70W4ACd3iwuF7KtDvHTUMdx3bnT0UDY0WPIb2ZwJS1J8JmSFs0rFn%2F3JRaRxHs3kzsJTDmj3ojdWykWzzOVzHLYpGMTaTxQy0x3oeBID6b3KjSKUi34iOq2Lgj1XjorMvVMITJotQGOqUBj0jfhc4tTBujGJ8cHq5sB%2Fa3sevKrWe21IsUIX3JlHCTtwIJ%2Br7sPQ84qOu3NS9vVEIsel0AmTMqo5xNQd16bYCDalxDWVb7oPCNc0EbTymCXcEqnoNkStLdlEL5eCnuPWPSBiDIpdLkgWJZNvSuxrGzEoZd16C7o3vmOawF7NxA6hjmQqrh%2BUM2lfThffDUbS8cRwhi%2BXq2fbo24d0reyqDn4nz&X-Amz-Signature=5659a99b19bc311cefa24d6da5f62f96999e70d1411a921a817f4fee3e0065c8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

We get error Current password is incorrect:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e6e26397-57bd-4650-a628-543c7609a0a8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666PFPHWWZ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210449Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIC8YyQgTRecsPE1k%2FEkBdxBMnsd%2BWymmEAYwSdyRoxcZAiBPSwA1MJQG2r2xIPGcM%2F31NmAHciaZZhaoHC9c6pwwtCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMoiEO5vjHPup957QdKtwDpINIobFlX98oeeD7PK9Wj2IY2TByV%2FcFjTXpxBGU2X94ut13UD%2Bz6clYUz%2FzeM6yUpc%2F8DKsld2UF6SEBsBwBxjUCgElbd%2F7vRI3Y0lYVdS3mMsUCZegInDtJI4ryF1exPqt1OobNHgy0pb7OUWPYaN0taZm5q0l0KWybCNJxsDO57ZC8MdJ3uKLKtJCe1um5sldEleB95aBEVhK2wQEDHmiF3zrf1HoQyZtSfFQApwky6N6b4hIq1aF8Y6Uytb6q707%2F2oYBhc06Zj4QavlOB%2BoJu58%2BInyhb0BspFSdEKuhI5E9i%2FxmgIPi5Gx%2FG9sRuFd5uw%2BWigapLoE9ZCp8aFlXfQDUjFbidiAidcQif%2BRgM7ZLITCfXiNUhSf9Qyd8MOv2zqqmXyLodLoigjPEcpD9V%2BuWIyTYLpWG0kzl1RUK6NS5l3%2B34lePu99tIM5joBhOA3y3PSVQQzZmOwCOyyspSBVaQyYvTfT5k8ELGWt1T2mTZi%2BTwjxsktexw%2FTw31%2BAMZlZcUh357%2BWA21u5vwqNH5y7Lb%2B8HOBvN4s9NGDyV1T7hgHmley7Dv3GS%2F7A8Izii6%2Bi%2FyePltOD9ZsYT4J2argpQdqVBRKFk6aSxmk338ZiY1RG12CMIw98Wi1AY6pgHFt0w1dQ8%2FjSsjSqSrbIZCQtGkV0cIcE%2BbfM%2BHKMbZmC%2BUnX7JrlnFoDk93GDSaTvSgUxj5gGOulEYT6%2BTX7HXO03YossqgSwJbON0C8%2FMtma4sKGBbLb1%2FqOSA8v2SfZrkGXaC5Fk6CMqwDRdBjcSUKc2ZpxlsBLQLRoIlBUGmTXH7yxl4SHNplJocF0nvaJanH5QsGhXQFGZo4qnlAHI2sFgZL%2FV&X-Amz-Signature=669423050c6990a4f34132556a0f1eda333d997e4066827522a84095080db1e1&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

From this result I can derive a few pieces of information:

1. The password change failed due to a wrong current password.
1. The password comparison was not performed with the password account that is logged in but with the password of the account set in `Username`
1. At the point the 'Update password' form was generated, the application did use the logged-in user again.
But at some point during the generation of the response, the application assumed that my username is `administrator`. This points to some weird logic behind the scenes that warrant further investigation.

To verify that no password was changed despite the error message, I attempt to log in with both `wiener` and `administrator` using the newly set password. It fails as expected.

### Analyzing the traffic

When we clicked the `Change password` button, **it send a POST request to **`/my-account/change-password`**, with parameter **`csrf`**, **`username`**, **`current-password`**, **`new-password-1`**, and **`new-password-2`**.**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/81e66630-f649-477b-94d3-afd5f40c0120/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UR5VBDMY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210447Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIGeSAZSIaqY7k9KYWcEUJyDEIXTPCXnJ8cNLLRwHdALBAiEAygRJaqcYgOneBhna14wPNK5fygchd2XdtRLh7Zc8pKQqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDOoiMEGfXAS6J2%2BK%2BCrcA%2Bq8dFE6hOIs%2B4aLXeVJKlPOo%2Fhwj8IM8DbQXzB3HYoTYGoscCvUL2Rny%2BVmMh0ZfyJtuG5zNPqpMHBZX6NT%2BGCMAmGrQVl3Oz52Sdkz5RR5SZWj6zqedqz2%2Br5xaSZLNE4DRvbBMWSuP4YnTje%2BEvDx2A3w0ssLALAZm%2BWcsYV7M937xcPWntTVfYmiiXDMP8nw%2BbCFz%2FEF96grPrU3m4Ro7kXy7uYh8GaFlQRXaGMr8lWwB7DIMq5JRnNN7PV4NYxdKLCNQc%2Bq2nX7NSvQTtDzQzB3XOKvDh%2BU2i6vJq8vcI%2FXqFA7a6aCWBl0gDlYNdOj1nt0B2Sd6vY%2FsTg5tJ12WybrdaM2fbp4to98bNh7hGBjUidBPi509JCodHv1SGQ4VXO7eH%2FaDzN6ha%2BwWDHEpfgEfSfJWxtzhKyJw9rh3IxG6qp6%2FJKE%2BxzvmUEwvSGvEOrV7qxpQLzcLFBSdPGvjcsfhsWtSv6EZ6heBFtU4y2cIbsqmb16eV70W4ACd3iwuF7KtDvHTUMdx3bnT0UDY0WPIb2ZwJS1J8JmSFs0rFn%2F3JRaRxHs3kzsJTDmj3ojdWykWzzOVzHLYpGMTaTxQy0x3oeBID6b3KjSKUi34iOq2Lgj1XjorMvVMITJotQGOqUBj0jfhc4tTBujGJ8cHq5sB%2Fa3sevKrWe21IsUIX3JlHCTtwIJ%2Br7sPQ84qOu3NS9vVEIsel0AmTMqo5xNQd16bYCDalxDWVb7oPCNc0EbTymCXcEqnoNkStLdlEL5eCnuPWPSBiDIpdLkgWJZNvSuxrGzEoZd16C7o3vmOawF7NxA6hjmQqrh%2BUM2lfThffDUbS8cRwhi%2BXq2fbo24d0reyqDn4nz&X-Amz-Signature=664f7ea9a3bc9e57becdd0e65294c2ae5643709885c3ea13c4adbc14cc48d424&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

OK, so I have the csrf token, username and the three password parameters.

While the application generated the response, at the moment my username was embedded, I was the `administrator` user. I was also considered `administrator` while the current password was checked and the error message got inserted. As such, the password change failed as it was not the correct password for that user.

So what happens if I remove the current-password parameter from the form?

This depends on whether it always checks the current password on password change. If this is the case, then it will fail as well, as it should.

However, if the password check only occurs when the parameter is present, then it will be bad for the application but good for me.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2fc35871-6a2d-4cb6-92f8-1016672f0b1d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UR5VBDMY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210447Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIGeSAZSIaqY7k9KYWcEUJyDEIXTPCXnJ8cNLLRwHdALBAiEAygRJaqcYgOneBhna14wPNK5fygchd2XdtRLh7Zc8pKQqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDOoiMEGfXAS6J2%2BK%2BCrcA%2Bq8dFE6hOIs%2B4aLXeVJKlPOo%2Fhwj8IM8DbQXzB3HYoTYGoscCvUL2Rny%2BVmMh0ZfyJtuG5zNPqpMHBZX6NT%2BGCMAmGrQVl3Oz52Sdkz5RR5SZWj6zqedqz2%2Br5xaSZLNE4DRvbBMWSuP4YnTje%2BEvDx2A3w0ssLALAZm%2BWcsYV7M937xcPWntTVfYmiiXDMP8nw%2BbCFz%2FEF96grPrU3m4Ro7kXy7uYh8GaFlQRXaGMr8lWwB7DIMq5JRnNN7PV4NYxdKLCNQc%2Bq2nX7NSvQTtDzQzB3XOKvDh%2BU2i6vJq8vcI%2FXqFA7a6aCWBl0gDlYNdOj1nt0B2Sd6vY%2FsTg5tJ12WybrdaM2fbp4to98bNh7hGBjUidBPi509JCodHv1SGQ4VXO7eH%2FaDzN6ha%2BwWDHEpfgEfSfJWxtzhKyJw9rh3IxG6qp6%2FJKE%2BxzvmUEwvSGvEOrV7qxpQLzcLFBSdPGvjcsfhsWtSv6EZ6heBFtU4y2cIbsqmb16eV70W4ACd3iwuF7KtDvHTUMdx3bnT0UDY0WPIb2ZwJS1J8JmSFs0rFn%2F3JRaRxHs3kzsJTDmj3ojdWykWzzOVzHLYpGMTaTxQy0x3oeBID6b3KjSKUi34iOq2Lgj1XjorMvVMITJotQGOqUBj0jfhc4tTBujGJ8cHq5sB%2Fa3sevKrWe21IsUIX3JlHCTtwIJ%2Br7sPQ84qOu3NS9vVEIsel0AmTMqo5xNQd16bYCDalxDWVb7oPCNc0EbTymCXcEqnoNkStLdlEL5eCnuPWPSBiDIpdLkgWJZNvSuxrGzEoZd16C7o3vmOawF7NxA6hjmQqrh%2BUM2lfThffDUbS8cRwhi%2BXq2fbo24d0reyqDn4nz&X-Amz-Signature=716207ede826e927cb583c6af1d098d0b08a41925b0c5ad512dc805e57f6d67c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

We successfully changed `administrator`’s password!

Try to logout and login again, this time with the credentials `administrator:peter`:


And I appear to be inside the administrator account. The application states that my username is `administrator` and it provides me with a link to an `Admin panel`. I access it, delete `carlos` and receive a confirmation:

