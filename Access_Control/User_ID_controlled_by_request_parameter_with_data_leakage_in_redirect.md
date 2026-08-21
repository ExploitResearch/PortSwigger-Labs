# User ID controlled by request parameter with data leakage in redirect

### Target Goal - 

Obtain the API key for the user `carlos` and submit it as the solution

### Analysis/Exploitation -

**Login as user **`wiener`**:**

- Send the request to Burp Repeater.
- Change the "id" parameter to `carlos`.
- Observe that although the response is now
redirecting you to the home page, it has a body containing the API key
belonging to `carlos`.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/4e833dd2-8913-48f3-932d-aefe23920fe4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UFL6MBU3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215515Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBaupAOOGnEtMESZh9VvtFqjCduYL4PJDe2G75fQrR3HAiEA896vGdsCovgAejaTEfg5BwD68uQbZ8zGoyjryLnus28qiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDDoiHCHF%2FOdBHVgSSyrcA0aCZ7io0pGFIRJKmviMY0mLBVaZ3Kl4LUVp%2BWwd7vrD4TXjzM7WdnOQhi%2FYEItlEw5RFABMpii6mk8VYEzC%2BZ9dtY5PSGPGoqRAojDIMdLGmdBUnq84wMYAW%2BmDbHHfsKaKQ1m%2FD7KxdvtZ09JelZ1BqUmjGhMOkISMMbMIIa5%2FR3WCL1vou5iPdaOeu4MlDRy3yGQEJigXXYI%2F2ZUuR5%2F%2B7Uwg%2FXNcbV9C3soATOzBxPHDxnrnTeVZ3PIB1W46f3p5Ip1xpPfRdC5wT%2Brl5yjb51kH0UEsi1CsaVQz%2B47zU4ndwYVEuAFU%2BrJwZmJZfqFJhF9qyHcrhcfnBc5UNaOWA%2BSkCKN1ZPgiE09zb4Iw7Hf1ppUE83L1c%2BW5L4sXWo2zLs99ZkfY%2FQMO%2BCJe1OxxsHN%2FmVaS8uTEy%2FG%2FgNemITt5pQW%2BQJFyNCU76VERNl53BSsIhApR%2B51Jz3PsgBKV371bougX0OV3O%2B9DhCagej3c2CF9SRXSjC3BsL2qTteHXZlzTX3jyKwqnLHSjYolPqLobA37c6WpW%2Bvb%2BpqTbWu90Ha%2FCBqf%2BHRc6FGv2xew7xujiJrFhWN%2FFdTRGge4bvz%2Bqn4cAPOR7v9fiAnarKXLdgyi02C%2BEP0LMNOGo9QGOqUB7Jkhl8T0oRr9fWxsBCJY9cypVdN8dXtwxXNiwOlicOYNhbPTkQToWJgWI2HT5JdmooMDYRcofZb40nrgCwxe0SL4O2YNAk3lxiOXRMhT1T7WjNW7t8m%2Bapq2e99uIaHT65Hp4J2TYiyzd1XiD5CibBjW9ukfelZMU0bOT%2F%2BoweDVifd5s%2FMu%2Bo9o21keVRtI21tSWrsPUHj5psGaIdcHOka5fpfb&X-Amz-Signature=83307c5567a46d838357397f39d3c8d6cda9ffa8deadeee471e0094d37f9691b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Submit the API key.
