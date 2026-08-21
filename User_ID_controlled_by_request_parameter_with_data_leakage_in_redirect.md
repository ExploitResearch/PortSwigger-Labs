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
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/4e833dd2-8913-48f3-932d-aefe23920fe4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SROOXSM7%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204646Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQD8RERobGZ7o6U6JJf44RW2KdsDaUNUeWiEFZ7PGgepDAIgb4a3NOX4UKsracVFfVEwYDoxxIczYzm0ei09gtYzZQAqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIO%2BXls7PbNv02%2FfSSrcA7HByacjalKdj%2BpumVSgiXe35O1BV4eIErg1QCqMZH3aIHISpQyrrIsAuXGGoKu7FwVNigRhN6MRoSwvtuEFY6iqQSlpEkfiViTBdc2ejpkGYhq3s6XypgcmvkPDG2WHNOWzRKaqfBRtcdoCGiyXjijni0H8WSqFWPvBTHf1u6GM6H0aBakqDOSCIOmg1S7MBZHE%2F1dQud1pOFPHTaxtuVcCJF5y2qiTgMrYFiM2Qowp9C4egx5pFiIo2z3xBGPi7ruh6rc%2FlqWQg4WFXbyeD0smRsO9LBodYxAqQg7QcTkfdGBZ5dUi0MlwYVwkzR4Ux4C0ay3pCf81RoGwkzTFMMybmDQ%2FWuWcSNZDvmCWR%2B88hAb7Hl30EGM3bvnJi56DsSOtVLc0LoCG8sYa7V13W4%2Fa7%2FtfVoiWPKjj0ENK8kxEzhMmXoRw%2FrX7kSXD6Zxm0jgtPWz%2Bef06rgO9PC%2BumxjFvay%2Fz2OQ2PgS3upEmmtPDTz0S%2BCK3X6gZfvYVrJedPKWAEKKU4hlRf%2BmnUk8GVOIQl3IEtuvqP5gaokxP3w2%2BZvZ%2BrbX8ATuxF2gwPt14GYEY%2BKVhJuSAZePoWfQlnc720kebrsWEvUrBSGvOUDeuqpIUVvLSKTTf5HeMMTGotQGOqUBUC9lnuUTwQfBf3x9sD4Jw2qrE853nbrYznTCTg%2FySHs7JkCn2I5MKiGsNF%2Fsg1y3V3D5WX%2F6br0ZrXoJGZmdT5cGkAvk9ZrERTyjJdV6wMYciYSuXlcpUnD0%2F%2BOvDvPIPrDexeo2%2FJS0Yq148lMmgVa%2FYjBdk7vUCb4YxcWxbqdvVbyKAedRt2KhxCndg2gZl%2FP4ecuy0uBf%2FyBfVNiAS6mzSbDk&X-Amz-Signature=566f4042750cb80e7f0bfa455215057c5a991e2ea95a2a833032626d33e25833&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Submit the API key.
