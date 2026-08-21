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
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/4e833dd2-8913-48f3-932d-aefe23920fe4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SDDBW4OK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210351Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIFZZzYhlv2y7O8TlSXAtklUXUHulkS1Mj41fTsZAvt%2FSAiEA%2B5wZHXRqPb2T%2FotMamms7beiPcfPLSSi6ShYYh9%2F2bUqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIbX1nrx8G7jhwE0hCrcA75pp4j9FSxwXzTI5HpPBzjy2N5kWdh5KbXi0UWsgTHDrhwv0kuxGsHLKGNsxy01d83oaQ97D1rKqMgdA%2F%2FsEg%2B0DcyOyuO3%2BMOhrHX4dS3LxhpPxHwG5zbSvdi99B6Rh0%2BhHyVTSgvBWF73NVzTqF0zkd1fW6lTTogHE9AZw9I2MH84IDTDFVHoW81grz0yTyK7fKiht0EnN1l8o3qQzKH3QKTISeyCsZ7HVHFzQgKNy7ODLZ1fhXiJwiE8HpDVlUY1HaCNBf0UpEVB4wpYNZB%2BHdJvPO9JMDfED63Wcd5dOLAdLpDPa8TAcxf77fCSNLn7x7MAYoyWse1jiV0PTel%2FYKGEcNMq0EVMyb9Z%2Fp4o6Re6gIB8vC7Rcmr3tDCRxpJI6OIH4GGSMqb59P%2BAT8HDyEMCqKnJ2GSowleGvLZX7QxlPm98r6%2FxsdJxxInW7tQw2k1EyUBj34FZsebW9kTapNoxIKMfpO1uX%2F0hVz%2FWTHZ0nNZkfcJxrX0q%2B1hZvKtRiUI11kJucvdPoPVwXCMQCEoYdJaa4ddUoXhkO1%2BAW2sWQHWJwd74%2BY7aNbx43VwFt03l%2B7Vq7hIt0SRCcuUQLvYJkybBglyRDdvHxWg0uUQGwgBJuCwNIgPtMPTFotQGOqUBslWhJT8hS8%2BQgoe9G9tDBBLANtgkAP8zmrllLt7FdppVpl%2FsJTXxtp6w5QqGcu7W7dXjFImgvYpiElojvkYga4hjYCgR7BdJf22ve0mB%2BRRfJ10g%2BTNB4ONM2UdWXcq%2BTduahFIY7n7H8hah4997ARiUiuD027bWpJSEh0ApXGcyPDWxFZjxXbsY0ITuKiS5yJcRGgU1klC8MFCXQiU4Vpes3KR6&X-Amz-Signature=13b8fbb0e7168abbbddbc27ba33e2a58af130986cb4dcff1a40da25d6220e045&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Submit the API key.
