# Chapter 1 Web Application (In)security

# **Web Applications**

- **E-commerce, Social networks, Online banking, etc.**
- **Fundamental security problem:**
  - ***Users can supply arbitrary input***
- **Malicious input can compromise the site**
# **Static Website: Web 1.0**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8b9196bf-6d68-413e-99df-9ee47137c06d/image2.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XZPMWEJ3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210138Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDVdc6ZtulGC43sHBSsrkAoYfSOJ%2B%2BVHldNPPy%2F04B%2BZAIhANV2VJEe%2FUPk2gEf7xwGBDtW6wwEk0jrWZ88o795oRU%2FKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgyNh2voEGZ%2B03qjkEgq3AOBSXn6ev%2FVK8jGaOe6cufgnA6v8InAlraYqk1eP90Zy8pynJcieFjTuR2W1SWs4xSV7P54DufFqOg6%2FPB8tyRbQGhZQj6zXbJcrpSVHSTVpAb1fLLAMolCPz%2BBqgCE%2F%2BKi8WRFNHCdN%2BCITDe2gL6SUT9eZYneEVCzDfweatFEQ31qWBFdoMrNrMQcmHGvATTIQWBugaYC53W%2FsJ%2B0snDH3ADC1vbgTa5RaNV%2F9IsDXxlrIoLc2k%2FWYZuysJ8jD8pZ465leLcQq82icFjSQbCv6Z%2BBabrQc%2FRKRaElukvi%2FIv6LE%2B775VW42QeuXVkh3S%2FIP0Kl9qzEV5RPzAAcFnJqBnO7l0SmfFbQDcOfACWy2tQNuqE%2FPRbmjzeM%2FwiwyBDCfgKRCO3FSUgs7Pvl%2BAypjkWUFtPH21zVuD%2BWFDaSI58nsuMAhybgwZ4hx0PqBPmv7PAecXdmq2%2BpbUCDQwe%2F%2FR%2Biuj%2BP%2FrXATFFm7jeaCqfjZy0aGwK3H0bB9aB0e%2FPsl4Moe9qRuqf9Z6ei4WlOTqLeSPqdDKwwcJzRldTh3zkJZdzQqB29QFtbUCMqd1%2F2w1yHV0yo9Vt2J3907VWpauORyaOa2wnGZW1DW68OhimLksLrbnwBurWSjCoyKLUBjqkAfuDmTVE%2FeZV25G8AGXIIuLVXHaCl%2FZllxzw0%2F9Jei3kCUHC%2BcKmXF4BmVXLnKqSgJeL0i3J%2FBg%2FUauPhMcha1JbeG9YOK4MiTN9%2B1rFGPGXMtuuWYNj%2BWNbkRzI%2BQiY%2FqsXPcIQ%2Bb257i3N2PwewgA6g%2FADBs5LlSnOhZmt8uKWB2mADCmY39dGTIxa0XPyIivJYIW1bGfZk1jPA%2B9dpP%2FN%2BWMm&X-Amz-Signature=eaf5af5391aaa5bd91bd7108c00f7347199aaf27a2d9e23f060b1233200721b2&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- Information flows one-way
- Users don't log in,
> shop, or submit comments

- An attacker who exploits flaws in the Web server software can
  - Steal data on the Web server (usually only public data anyway)
  - Deface the site
# **Modern Web App**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cf3f68c5-5215-45eb-8a6e-bd6750a2c528/image3.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XZPMWEJ3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210138Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDVdc6ZtulGC43sHBSsrkAoYfSOJ%2B%2BVHldNPPy%2F04B%2BZAIhANV2VJEe%2FUPk2gEf7xwGBDtW6wwEk0jrWZ88o795oRU%2FKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgyNh2voEGZ%2B03qjkEgq3AOBSXn6ev%2FVK8jGaOe6cufgnA6v8InAlraYqk1eP90Zy8pynJcieFjTuR2W1SWs4xSV7P54DufFqOg6%2FPB8tyRbQGhZQj6zXbJcrpSVHSTVpAb1fLLAMolCPz%2BBqgCE%2F%2BKi8WRFNHCdN%2BCITDe2gL6SUT9eZYneEVCzDfweatFEQ31qWBFdoMrNrMQcmHGvATTIQWBugaYC53W%2FsJ%2B0snDH3ADC1vbgTa5RaNV%2F9IsDXxlrIoLc2k%2FWYZuysJ8jD8pZ465leLcQq82icFjSQbCv6Z%2BBabrQc%2FRKRaElukvi%2FIv6LE%2B775VW42QeuXVkh3S%2FIP0Kl9qzEV5RPzAAcFnJqBnO7l0SmfFbQDcOfACWy2tQNuqE%2FPRbmjzeM%2FwiwyBDCfgKRCO3FSUgs7Pvl%2BAypjkWUFtPH21zVuD%2BWFDaSI58nsuMAhybgwZ4hx0PqBPmv7PAecXdmq2%2BpbUCDQwe%2F%2FR%2Biuj%2BP%2FrXATFFm7jeaCqfjZy0aGwK3H0bB9aB0e%2FPsl4Moe9qRuqf9Z6ei4WlOTqLeSPqdDKwwcJzRldTh3zkJZdzQqB29QFtbUCMqd1%2F2w1yHV0yo9Vt2J3907VWpauORyaOa2wnGZW1DW68OhimLksLrbnwBurWSjCoyKLUBjqkAfuDmTVE%2FeZV25G8AGXIIuLVXHaCl%2FZllxzw0%2F9Jei3kCUHC%2BcKmXF4BmVXLnKqSgJeL0i3J%2FBg%2FUauPhMcha1JbeG9YOK4MiTN9%2B1rFGPGXMtuuWYNj%2BWNbkRzI%2BQiY%2FqsXPcIQ%2Bb257i3N2PwewgA6g%2FADBs5LlSnOhZmt8uKWB2mADCmY39dGTIxa0XPyIivJYIW1bGfZk1jPA%2B9dpP%2FN%2BWMm&X-Amz-Signature=c75b57be80f141fe0e770e9a77ed5e1aa99e2ac0bf3b060f4b56e3e89d91375d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Two-way information flow**
- **Users log in, submit content**
- **Content dynamically generated and tailored for each user**
- **Much data is sensitive and private (e.g. passwords)**
- **Most apps developed in-house**
- **Developers often naive about security**
### Common Web App **Functions**

- **Shopping (Amazon)**
- **Social networking (Facebook)**
- **Banking (Citibank)**
- **Web search (Google)**
- **Auctions (eBay)**
- **Gambling (Betfair)**
- **Web logs (Blogger)**
- **Web mail (Gmail)**
- **Interactive information (Wikipedia)**
### Internal Web Apps ("Cloud" Services)

- **HR -- payroll information, performance reviews**
- **Admin interfaces to servers, VMs, workstations**
- **Collaboration software (SharePoint)**
- **Enterprise Resource Planning (ERP)**
- **Email web interfaces (Outlook Web Access)**
- **Office apps (Google Apps, MS Office Live)**
# **Benefits of Web Apps**

- **HTTP is lightweight and connectionless**
  - **Resilient in event of communications errors**
  - **Can be proxied and tunneled over other protocols**
- **Web browsers run on many devices, highly functional, easy to use**
- **Many platforms and development tools available**
# **Web App Security**

- **Breaches are common**
  - **Attackers gets sensitive data, possibly complete control of back-end systems**
- **Denial of Service at Application Level**
# **This Site is Secure**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ab4feb1b-b3a2-491d-aad4-20d6314adafb/image4.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XZPMWEJ3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210139Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDVdc6ZtulGC43sHBSsrkAoYfSOJ%2B%2BVHldNPPy%2F04B%2BZAIhANV2VJEe%2FUPk2gEf7xwGBDtW6wwEk0jrWZ88o795oRU%2FKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgyNh2voEGZ%2B03qjkEgq3AOBSXn6ev%2FVK8jGaOe6cufgnA6v8InAlraYqk1eP90Zy8pynJcieFjTuR2W1SWs4xSV7P54DufFqOg6%2FPB8tyRbQGhZQj6zXbJcrpSVHSTVpAb1fLLAMolCPz%2BBqgCE%2F%2BKi8WRFNHCdN%2BCITDe2gL6SUT9eZYneEVCzDfweatFEQ31qWBFdoMrNrMQcmHGvATTIQWBugaYC53W%2FsJ%2B0snDH3ADC1vbgTa5RaNV%2F9IsDXxlrIoLc2k%2FWYZuysJ8jD8pZ465leLcQq82icFjSQbCv6Z%2BBabrQc%2FRKRaElukvi%2FIv6LE%2B775VW42QeuXVkh3S%2FIP0Kl9qzEV5RPzAAcFnJqBnO7l0SmfFbQDcOfACWy2tQNuqE%2FPRbmjzeM%2FwiwyBDCfgKRCO3FSUgs7Pvl%2BAypjkWUFtPH21zVuD%2BWFDaSI58nsuMAhybgwZ4hx0PqBPmv7PAecXdmq2%2BpbUCDQwe%2F%2FR%2Biuj%2BP%2FrXATFFm7jeaCqfjZy0aGwK3H0bB9aB0e%2FPsl4Moe9qRuqf9Z6ei4WlOTqLeSPqdDKwwcJzRldTh3zkJZdzQqB29QFtbUCMqd1%2F2w1yHV0yo9Vt2J3907VWpauORyaOa2wnGZW1DW68OhimLksLrbnwBurWSjCoyKLUBjqkAfuDmTVE%2FeZV25G8AGXIIuLVXHaCl%2FZllxzw0%2F9Jei3kCUHC%2BcKmXF4BmVXLnKqSgJeL0i3J%2FBg%2FUauPhMcha1JbeG9YOK4MiTN9%2B1rFGPGXMtuuWYNj%2BWNbkRzI%2BQiY%2FqsXPcIQ%2Bb257i3N2PwewgA6g%2FADBs5LlSnOhZmt8uKWB2mADCmY39dGTIxa0XPyIivJYIW1bGfZk1jPA%2B9dpP%2FN%2BWMm&X-Amz-Signature=8d9608ace1a20b07e688afcf8e91c361ac065675a888db6aba222b28e4905b5d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- A frequent claim, very far from the truth
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c9c2110f-2577-49de-b49f-1745aa19ead8/image6.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XZPMWEJ3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210139Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDVdc6ZtulGC43sHBSsrkAoYfSOJ%2B%2BVHldNPPy%2F04B%2BZAIhANV2VJEe%2FUPk2gEf7xwGBDtW6wwEk0jrWZ88o795oRU%2FKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgyNh2voEGZ%2B03qjkEgq3AOBSXn6ev%2FVK8jGaOe6cufgnA6v8InAlraYqk1eP90Zy8pynJcieFjTuR2W1SWs4xSV7P54DufFqOg6%2FPB8tyRbQGhZQj6zXbJcrpSVHSTVpAb1fLLAMolCPz%2BBqgCE%2F%2BKi8WRFNHCdN%2BCITDe2gL6SUT9eZYneEVCzDfweatFEQ31qWBFdoMrNrMQcmHGvATTIQWBugaYC53W%2FsJ%2B0snDH3ADC1vbgTa5RaNV%2F9IsDXxlrIoLc2k%2FWYZuysJ8jD8pZ465leLcQq82icFjSQbCv6Z%2BBabrQc%2FRKRaElukvi%2FIv6LE%2B775VW42QeuXVkh3S%2FIP0Kl9qzEV5RPzAAcFnJqBnO7l0SmfFbQDcOfACWy2tQNuqE%2FPRbmjzeM%2FwiwyBDCfgKRCO3FSUgs7Pvl%2BAypjkWUFtPH21zVuD%2BWFDaSI58nsuMAhybgwZ4hx0PqBPmv7PAecXdmq2%2BpbUCDQwe%2F%2FR%2Biuj%2BP%2FrXATFFm7jeaCqfjZy0aGwK3H0bB9aB0e%2FPsl4Moe9qRuqf9Z6ei4WlOTqLeSPqdDKwwcJzRldTh3zkJZdzQqB29QFtbUCMqd1%2F2w1yHV0yo9Vt2J3907VWpauORyaOa2wnGZW1DW68OhimLksLrbnwBurWSjCoyKLUBjqkAfuDmTVE%2FeZV25G8AGXIIuLVXHaCl%2FZllxzw0%2F9Jei3kCUHC%2BcKmXF4BmVXLnKqSgJeL0i3J%2FBg%2FUauPhMcha1JbeG9YOK4MiTN9%2B1rFGPGXMtuuWYNj%2BWNbkRzI%2BQiY%2FqsXPcIQ%2Bb257i3N2PwewgA6g%2FADBs5LlSnOhZmt8uKWB2mADCmY39dGTIxa0XPyIivJYIW1bGfZk1jPA%2B9dpP%2FN%2BWMm&X-Amz-Signature=e283fa0aa098ce6385a42b6bebe11cf32cd41e8026dc65a443265174a0a11e7d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

## SinVR Hack

- Unauthenticated request allows anyone to download PII from users
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ba36e809-cc44-4568-a6dd-d84e1997f56a/image7.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XZPMWEJ3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210139Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDVdc6ZtulGC43sHBSsrkAoYfSOJ%2B%2BVHldNPPy%2F04B%2BZAIhANV2VJEe%2FUPk2gEf7xwGBDtW6wwEk0jrWZ88o795oRU%2FKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgyNh2voEGZ%2B03qjkEgq3AOBSXn6ev%2FVK8jGaOe6cufgnA6v8InAlraYqk1eP90Zy8pynJcieFjTuR2W1SWs4xSV7P54DufFqOg6%2FPB8tyRbQGhZQj6zXbJcrpSVHSTVpAb1fLLAMolCPz%2BBqgCE%2F%2BKi8WRFNHCdN%2BCITDe2gL6SUT9eZYneEVCzDfweatFEQ31qWBFdoMrNrMQcmHGvATTIQWBugaYC53W%2FsJ%2B0snDH3ADC1vbgTa5RaNV%2F9IsDXxlrIoLc2k%2FWYZuysJ8jD8pZ465leLcQq82icFjSQbCv6Z%2BBabrQc%2FRKRaElukvi%2FIv6LE%2B775VW42QeuXVkh3S%2FIP0Kl9qzEV5RPzAAcFnJqBnO7l0SmfFbQDcOfACWy2tQNuqE%2FPRbmjzeM%2FwiwyBDCfgKRCO3FSUgs7Pvl%2BAypjkWUFtPH21zVuD%2BWFDaSI58nsuMAhybgwZ4hx0PqBPmv7PAecXdmq2%2BpbUCDQwe%2F%2FR%2Biuj%2BP%2FrXATFFm7jeaCqfjZy0aGwK3H0bB9aB0e%2FPsl4Moe9qRuqf9Z6ei4WlOTqLeSPqdDKwwcJzRldTh3zkJZdzQqB29QFtbUCMqd1%2F2w1yHV0yo9Vt2J3907VWpauORyaOa2wnGZW1DW68OhimLksLrbnwBurWSjCoyKLUBjqkAfuDmTVE%2FeZV25G8AGXIIuLVXHaCl%2FZllxzw0%2F9Jei3kCUHC%2BcKmXF4BmVXLnKqSgJeL0i3J%2FBg%2FUauPhMcha1JbeG9YOK4MiTN9%2B1rFGPGXMtuuWYNj%2BWNbkRzI%2BQiY%2FqsXPcIQ%2Bb257i3N2PwewgA6g%2FADBs5LlSnOhZmt8uKWB2mADCmY39dGTIxa0XPyIivJYIW1bGfZk1jPA%2B9dpP%2FN%2BWMm&X-Amz-Signature=c03f667d97b1afd9c9f3b65edfbe32457f5cfd8b3dfc866580af287cb6df5ea4&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

# **PII**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fa5014a6-c5ef-4d89-9ef0-2760a5dbed5b/image8.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XZPMWEJ3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210139Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDVdc6ZtulGC43sHBSsrkAoYfSOJ%2B%2BVHldNPPy%2F04B%2BZAIhANV2VJEe%2FUPk2gEf7xwGBDtW6wwEk0jrWZ88o795oRU%2FKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgyNh2voEGZ%2B03qjkEgq3AOBSXn6ev%2FVK8jGaOe6cufgnA6v8InAlraYqk1eP90Zy8pynJcieFjTuR2W1SWs4xSV7P54DufFqOg6%2FPB8tyRbQGhZQj6zXbJcrpSVHSTVpAb1fLLAMolCPz%2BBqgCE%2F%2BKi8WRFNHCdN%2BCITDe2gL6SUT9eZYneEVCzDfweatFEQ31qWBFdoMrNrMQcmHGvATTIQWBugaYC53W%2FsJ%2B0snDH3ADC1vbgTa5RaNV%2F9IsDXxlrIoLc2k%2FWYZuysJ8jD8pZ465leLcQq82icFjSQbCv6Z%2BBabrQc%2FRKRaElukvi%2FIv6LE%2B775VW42QeuXVkh3S%2FIP0Kl9qzEV5RPzAAcFnJqBnO7l0SmfFbQDcOfACWy2tQNuqE%2FPRbmjzeM%2FwiwyBDCfgKRCO3FSUgs7Pvl%2BAypjkWUFtPH21zVuD%2BWFDaSI58nsuMAhybgwZ4hx0PqBPmv7PAecXdmq2%2BpbUCDQwe%2F%2FR%2Biuj%2BP%2FrXATFFm7jeaCqfjZy0aGwK3H0bB9aB0e%2FPsl4Moe9qRuqf9Z6ei4WlOTqLeSPqdDKwwcJzRldTh3zkJZdzQqB29QFtbUCMqd1%2F2w1yHV0yo9Vt2J3907VWpauORyaOa2wnGZW1DW68OhimLksLrbnwBurWSjCoyKLUBjqkAfuDmTVE%2FeZV25G8AGXIIuLVXHaCl%2FZllxzw0%2F9Jei3kCUHC%2BcKmXF4BmVXLnKqSgJeL0i3J%2FBg%2FUauPhMcha1JbeG9YOK4MiTN9%2B1rFGPGXMtuuWYNj%2BWNbkRzI%2BQiY%2FqsXPcIQ%2Bb257i3N2PwewgA6g%2FADBs5LlSnOhZmt8uKWB2mADCmY39dGTIxa0XPyIivJYIW1bGfZk1jPA%2B9dpP%2FN%2BWMm&X-Amz-Signature=0145d6cbc6e70d88c2495bb42aa8cec7775b8ec6d02daa0dc825b22b5c84534f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e99c7c2a-4e30-4de5-8008-f853d82c3f1d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XZPMWEJ3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210139Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDVdc6ZtulGC43sHBSsrkAoYfSOJ%2B%2BVHldNPPy%2F04B%2BZAIhANV2VJEe%2FUPk2gEf7xwGBDtW6wwEk0jrWZ88o795oRU%2FKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgyNh2voEGZ%2B03qjkEgq3AOBSXn6ev%2FVK8jGaOe6cufgnA6v8InAlraYqk1eP90Zy8pynJcieFjTuR2W1SWs4xSV7P54DufFqOg6%2FPB8tyRbQGhZQj6zXbJcrpSVHSTVpAb1fLLAMolCPz%2BBqgCE%2F%2BKi8WRFNHCdN%2BCITDe2gL6SUT9eZYneEVCzDfweatFEQ31qWBFdoMrNrMQcmHGvATTIQWBugaYC53W%2FsJ%2B0snDH3ADC1vbgTa5RaNV%2F9IsDXxlrIoLc2k%2FWYZuysJ8jD8pZ465leLcQq82icFjSQbCv6Z%2BBabrQc%2FRKRaElukvi%2FIv6LE%2B775VW42QeuXVkh3S%2FIP0Kl9qzEV5RPzAAcFnJqBnO7l0SmfFbQDcOfACWy2tQNuqE%2FPRbmjzeM%2FwiwyBDCfgKRCO3FSUgs7Pvl%2BAypjkWUFtPH21zVuD%2BWFDaSI58nsuMAhybgwZ4hx0PqBPmv7PAecXdmq2%2BpbUCDQwe%2F%2FR%2Biuj%2BP%2FrXATFFm7jeaCqfjZy0aGwK3H0bB9aB0e%2FPsl4Moe9qRuqf9Z6ei4WlOTqLeSPqdDKwwcJzRldTh3zkJZdzQqB29QFtbUCMqd1%2F2w1yHV0yo9Vt2J3907VWpauORyaOa2wnGZW1DW68OhimLksLrbnwBurWSjCoyKLUBjqkAfuDmTVE%2FeZV25G8AGXIIuLVXHaCl%2FZllxzw0%2F9Jei3kCUHC%2BcKmXF4BmVXLnKqSgJeL0i3J%2FBg%2FUauPhMcha1JbeG9YOK4MiTN9%2B1rFGPGXMtuuWYNj%2BWNbkRzI%2BQiY%2FqsXPcIQ%2Bb257i3N2PwewgA6g%2FADBs5LlSnOhZmt8uKWB2mADCmY39dGTIxa0XPyIivJYIW1bGfZk1jPA%2B9dpP%2FN%2BWMm&X-Amz-Signature=0c58eb6fe659460f3d8efeb92a3916d5022a5e1e0846df39fa3dc428962cd92f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Binary Protections

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8ce765cb-e1f3-4664-bde6-36709fc96046/image15.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XZPMWEJ3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210139Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDVdc6ZtulGC43sHBSsrkAoYfSOJ%2B%2BVHldNPPy%2F04B%2BZAIhANV2VJEe%2FUPk2gEf7xwGBDtW6wwEk0jrWZ88o795oRU%2FKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgyNh2voEGZ%2B03qjkEgq3AOBSXn6ev%2FVK8jGaOe6cufgnA6v8InAlraYqk1eP90Zy8pynJcieFjTuR2W1SWs4xSV7P54DufFqOg6%2FPB8tyRbQGhZQj6zXbJcrpSVHSTVpAb1fLLAMolCPz%2BBqgCE%2F%2BKi8WRFNHCdN%2BCITDe2gL6SUT9eZYneEVCzDfweatFEQ31qWBFdoMrNrMQcmHGvATTIQWBugaYC53W%2FsJ%2B0snDH3ADC1vbgTa5RaNV%2F9IsDXxlrIoLc2k%2FWYZuysJ8jD8pZ465leLcQq82icFjSQbCv6Z%2BBabrQc%2FRKRaElukvi%2FIv6LE%2B775VW42QeuXVkh3S%2FIP0Kl9qzEV5RPzAAcFnJqBnO7l0SmfFbQDcOfACWy2tQNuqE%2FPRbmjzeM%2FwiwyBDCfgKRCO3FSUgs7Pvl%2BAypjkWUFtPH21zVuD%2BWFDaSI58nsuMAhybgwZ4hx0PqBPmv7PAecXdmq2%2BpbUCDQwe%2F%2FR%2Biuj%2BP%2FrXATFFm7jeaCqfjZy0aGwK3H0bB9aB0e%2FPsl4Moe9qRuqf9Z6ei4WlOTqLeSPqdDKwwcJzRldTh3zkJZdzQqB29QFtbUCMqd1%2F2w1yHV0yo9Vt2J3907VWpauORyaOa2wnGZW1DW68OhimLksLrbnwBurWSjCoyKLUBjqkAfuDmTVE%2FeZV25G8AGXIIuLVXHaCl%2FZllxzw0%2F9Jei3kCUHC%2BcKmXF4BmVXLnKqSgJeL0i3J%2FBg%2FUauPhMcha1JbeG9YOK4MiTN9%2B1rFGPGXMtuuWYNj%2BWNbkRzI%2BQiY%2FqsXPcIQ%2Bb257i3N2PwewgA6g%2FADBs5LlSnOhZmt8uKWB2mADCmY39dGTIxa0XPyIivJYIW1bGfZk1jPA%2B9dpP%2FN%2BWMm&X-Amz-Signature=fa4b4054a617eda8c734af522f7b048f6bd994211048850353422fc1a85f85bd&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### The Core Security Problem

- **Users can submit arbitrary input**
  - **Alter parameters, cookies, HTTP headers**
  - **Client-side controls can't be trusted**
  - **Developers must assume all input is malicious**
  - **Attackers have attack tools like Burp; they are not restricted to using browsers**
# **Possible Attacks**

- **Change the price of an item**
- **Modify a session token to enter another user's account**
- **Remove parameters to exploit logic flaws**
- **SQL injection**
- ***SSL doesn't stop any of these***
# **Key Problem Factors**

- **Underdeveloped security awareness**
- **Custom development**
- **Deceptive simplicity**
  - **Easy to make a website, but hard to secure it**
- **Rapidly evolving threat profile**
- **Resource and time constraints**
- **Overextended technologies**
- **Increasing demands on functionality**
### The New Security Perimeter

- **Edge firewalls and "bastion hosts" are no longer enough**
  - **Keeping the attacker out of critical systems**
- **Customers can now send transactions to servers holding private data**
  - **Via the Web app**
- **Web app must act as a security barrier**
- **Often it includes components from others, like widgets**
- **Errors by other companies can compromise your servers**
- **Attackers can attack users instead of servers**
  - **XSS, drive-by downloads, etc.**
- **E-mail used for password recovery**
  - **A compromised email account exposes many other services also**
# **The Future**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0d109f1d-b571-4c0f-a8d2-c463d3065af6/image17.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XZPMWEJ3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210139Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDVdc6ZtulGC43sHBSsrkAoYfSOJ%2B%2BVHldNPPy%2F04B%2BZAIhANV2VJEe%2FUPk2gEf7xwGBDtW6wwEk0jrWZ88o795oRU%2FKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgyNh2voEGZ%2B03qjkEgq3AOBSXn6ev%2FVK8jGaOe6cufgnA6v8InAlraYqk1eP90Zy8pynJcieFjTuR2W1SWs4xSV7P54DufFqOg6%2FPB8tyRbQGhZQj6zXbJcrpSVHSTVpAb1fLLAMolCPz%2BBqgCE%2F%2BKi8WRFNHCdN%2BCITDe2gL6SUT9eZYneEVCzDfweatFEQ31qWBFdoMrNrMQcmHGvATTIQWBugaYC53W%2FsJ%2B0snDH3ADC1vbgTa5RaNV%2F9IsDXxlrIoLc2k%2FWYZuysJ8jD8pZ465leLcQq82icFjSQbCv6Z%2BBabrQc%2FRKRaElukvi%2FIv6LE%2B775VW42QeuXVkh3S%2FIP0Kl9qzEV5RPzAAcFnJqBnO7l0SmfFbQDcOfACWy2tQNuqE%2FPRbmjzeM%2FwiwyBDCfgKRCO3FSUgs7Pvl%2BAypjkWUFtPH21zVuD%2BWFDaSI58nsuMAhybgwZ4hx0PqBPmv7PAecXdmq2%2BpbUCDQwe%2F%2FR%2Biuj%2BP%2FrXATFFm7jeaCqfjZy0aGwK3H0bB9aB0e%2FPsl4Moe9qRuqf9Z6ei4WlOTqLeSPqdDKwwcJzRldTh3zkJZdzQqB29QFtbUCMqd1%2F2w1yHV0yo9Vt2J3907VWpauORyaOa2wnGZW1DW68OhimLksLrbnwBurWSjCoyKLUBjqkAfuDmTVE%2FeZV25G8AGXIIuLVXHaCl%2FZllxzw0%2F9Jei3kCUHC%2BcKmXF4BmVXLnKqSgJeL0i3J%2FBg%2FUauPhMcha1JbeG9YOK4MiTN9%2B1rFGPGXMtuuWYNj%2BWNbkRzI%2BQiY%2FqsXPcIQ%2Bb257i3N2PwewgA6g%2FADBs5LlSnOhZmt8uKWB2mADCmY39dGTIxa0XPyIivJYIW1bGfZk1jPA%2B9dpP%2FN%2BWMm&X-Amz-Signature=7717b61a6b6a7fc8f61425fc04780fe9accb9e93d18be14c564f7a5c1eec7264&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Some vulnerabilities are decreasing**
  - **#1 security measure: UPDATES**
- **Logic flaws and failure to use controls properly are not decreasing**
# **Core Defense Elements**

- **Limiting *****user access***** to app's data and functionality**
- **Limiting *****user input***** to prevent exploits that use malformed input**
- ***Frustrating attackers***** with appropriate behavior when targeted**
- ***Administrative monitoring and configuring***** the application**
# **Handling User Access**

- **Authentication**
- **Session management**
- **Access Control**
# **Authentication**

- **Username and password is most common method**
- **Better: additional credentials and multistage login**
- **Best: client certificates, smart cards, challenge- response tokens**
- **Also: self-registration, account recovery, password change**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/27352fc8-c398-41ec-8c1e-2e22915a1f30/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XZPMWEJ3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210139Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDVdc6ZtulGC43sHBSsrkAoYfSOJ%2B%2BVHldNPPy%2F04B%2BZAIhANV2VJEe%2FUPk2gEf7xwGBDtW6wwEk0jrWZ88o795oRU%2FKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgyNh2voEGZ%2B03qjkEgq3AOBSXn6ev%2FVK8jGaOe6cufgnA6v8InAlraYqk1eP90Zy8pynJcieFjTuR2W1SWs4xSV7P54DufFqOg6%2FPB8tyRbQGhZQj6zXbJcrpSVHSTVpAb1fLLAMolCPz%2BBqgCE%2F%2BKi8WRFNHCdN%2BCITDe2gL6SUT9eZYneEVCzDfweatFEQ31qWBFdoMrNrMQcmHGvATTIQWBugaYC53W%2FsJ%2B0snDH3ADC1vbgTa5RaNV%2F9IsDXxlrIoLc2k%2FWYZuysJ8jD8pZ465leLcQq82icFjSQbCv6Z%2BBabrQc%2FRKRaElukvi%2FIv6LE%2B775VW42QeuXVkh3S%2FIP0Kl9qzEV5RPzAAcFnJqBnO7l0SmfFbQDcOfACWy2tQNuqE%2FPRbmjzeM%2FwiwyBDCfgKRCO3FSUgs7Pvl%2BAypjkWUFtPH21zVuD%2BWFDaSI58nsuMAhybgwZ4hx0PqBPmv7PAecXdmq2%2BpbUCDQwe%2F%2FR%2Biuj%2BP%2FrXATFFm7jeaCqfjZy0aGwK3H0bB9aB0e%2FPsl4Moe9qRuqf9Z6ei4WlOTqLeSPqdDKwwcJzRldTh3zkJZdzQqB29QFtbUCMqd1%2F2w1yHV0yo9Vt2J3907VWpauORyaOa2wnGZW1DW68OhimLksLrbnwBurWSjCoyKLUBjqkAfuDmTVE%2FeZV25G8AGXIIuLVXHaCl%2FZllxzw0%2F9Jei3kCUHC%2BcKmXF4BmVXLnKqSgJeL0i3J%2FBg%2FUauPhMcha1JbeG9YOK4MiTN9%2B1rFGPGXMtuuWYNj%2BWNbkRzI%2BQiY%2FqsXPcIQ%2Bb257i3N2PwewgA6g%2FADBs5LlSnOhZmt8uKWB2mADCmY39dGTIxa0XPyIivJYIW1bGfZk1jPA%2B9dpP%2FN%2BWMm&X-Amz-Signature=ac717fbcf1374c9edd16eaf6b3066a236250ac068df5712bb12bc59ee9a5b810&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

## Common Login Problems

- **Predictable usernames**
- **Password that can be guessed**
- **Defects in logic**
# **Session Management**

- **Session: a set of data structures that track the state of the user**
- **A token identifies the session, usually a cookie**
  - **Can also use hidden form fields or the URL query string**
- **Sessions expire**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ce49d6b6-4c9e-4ba9-a46c-8611b124ddc7/image30.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z5LVJU35%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210142Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFBPol9pbtkVbZLkjNQMLz7Q3ZS8o6NG9e9okBw7DapHAiA3A0kGOMUxkt3EXyISGeORYggByWf9440l7DOjunS%2BqiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlOjWgzIFI97pH%2FOOKtwDeAX%2F6nsJHCLj9nCsJFA5oSWoFzoobjFQNbXbSq%2FT0XqItIFU%2BDcBdziP2lC00oMSlvwFgUKloJt23UZdOZs2LsFWtxK5XV9LO1uz8t9NTVlbdWhqiuEp8meJ57cL00iRS2wE6T3wK1F5NuhXuPmuV2m9EpgUxchj9KVJIDhzU4R9KME20L6ZFDGhIs1%2BdhiSpjHjqcZgTrri8mZQFy%2BNZQKKuQddjcvyPg4wFhPoL%2FFvUm1cVaUvuVYuk7aA6oBCo8XZcODTnDSKGUW4ESebQGHG7g3VLpB2tK6d3SVd2habTOtYmmeJU8MbhrmdHVcE%2BMTvoOUsqAnL7iLhyvorIjGrgFxTimhHEHn25PMuZ2TNL0fU9wS4%2FYNKQTc7OFeO0Bc9XyY0EviXeoaGTak2%2B%2FfXbZYHekSghK7qoRFLyjFShs32snxLsYprM7PHaaI0wt5pgVykpLnGfark3%2F0PnBHF3A7RZ31%2BUb5kw9pY0jYtymyuBXXSD98wUdasV2eJYGdFzfvPWOqGPVdyitqIxIUsWjKwdgHqb65jvF5Sy7SY%2BTX%2BiRq2%2B%2FZLVLGerYLRdXnExncAxEOgvKsvexKrtChIvMfbLy8nLzImOrAiKiwRjoEWY7g9yJHDolIw48Wi1AY6pgF3P%2BAOPbkW%2F18eaJV8sB3hn0m8JreGd7NQGL%2FzunayWBn6ZsbqiLPvcDuJ8FKg8SVsmDjX9GaT3sgNqcAV7ELddTFco1ROrlNOeX7yjXBl8eIoKfI3W3Jq6ekYcH4baU%2F2rZ%2B%2Fnv7pbtj%2BDNeX6ImUtx2CWa6pUnKwEFupPw%2F1LypuXkNgt9Mek8vkMT6CsLPV1hoXeV1iI53pRdjNkPo8JXk0NpOg&X-Amz-Signature=cf46268b30f024d0089c72dbf9a90593cc4ccbfcc9f417576365f6eb41fa0af9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Common Session Problems

- **Tokens are predictable (not random)**
- **Tokens poorly handled, so an attacker can capture another user's token**
### Access Control

- **Each request must be permitted or denied**
- **Multiple roles within application**
- **Frequent logic errors and flawed assumptions**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e68c2bc6-4d70-4060-ac8e-b56958dffdd8/image31.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z5LVJU35%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210142Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFBPol9pbtkVbZLkjNQMLz7Q3ZS8o6NG9e9okBw7DapHAiA3A0kGOMUxkt3EXyISGeORYggByWf9440l7DOjunS%2BqiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlOjWgzIFI97pH%2FOOKtwDeAX%2F6nsJHCLj9nCsJFA5oSWoFzoobjFQNbXbSq%2FT0XqItIFU%2BDcBdziP2lC00oMSlvwFgUKloJt23UZdOZs2LsFWtxK5XV9LO1uz8t9NTVlbdWhqiuEp8meJ57cL00iRS2wE6T3wK1F5NuhXuPmuV2m9EpgUxchj9KVJIDhzU4R9KME20L6ZFDGhIs1%2BdhiSpjHjqcZgTrri8mZQFy%2BNZQKKuQddjcvyPg4wFhPoL%2FFvUm1cVaUvuVYuk7aA6oBCo8XZcODTnDSKGUW4ESebQGHG7g3VLpB2tK6d3SVd2habTOtYmmeJU8MbhrmdHVcE%2BMTvoOUsqAnL7iLhyvorIjGrgFxTimhHEHn25PMuZ2TNL0fU9wS4%2FYNKQTc7OFeO0Bc9XyY0EviXeoaGTak2%2B%2FfXbZYHekSghK7qoRFLyjFShs32snxLsYprM7PHaaI0wt5pgVykpLnGfark3%2F0PnBHF3A7RZ31%2BUb5kw9pY0jYtymyuBXXSD98wUdasV2eJYGdFzfvPWOqGPVdyitqIxIUsWjKwdgHqb65jvF5Sy7SY%2BTX%2BiRq2%2B%2FZLVLGerYLRdXnExncAxEOgvKsvexKrtChIvMfbLy8nLzImOrAiKiwRjoEWY7g9yJHDolIw48Wi1AY6pgF3P%2BAOPbkW%2F18eaJV8sB3hn0m8JreGd7NQGL%2FzunayWBn6ZsbqiLPvcDuJ8FKg8SVsmDjX9GaT3sgNqcAV7ELddTFco1ROrlNOeX7yjXBl8eIoKfI3W3Jq6ekYcH4baU%2F2rZ%2B%2Fnv7pbtj%2BDNeX6ImUtx2CWa6pUnKwEFupPw%2F1LypuXkNgt9Mek8vkMT6CsLPV1hoXeV1iI53pRdjNkPo8JXk0NpOg&X-Amz-Signature=df122dc248181efe6bbced2f1d0f7864b8c5045d6e67a64c57e9cea003b74ac7&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

# **Handling User Input**

- **"Input Validation" is the most common solution**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e8292331-5fd1-422f-bfda-b805ada91fc3/image32.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z5LVJU35%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210142Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFBPol9pbtkVbZLkjNQMLz7Q3ZS8o6NG9e9okBw7DapHAiA3A0kGOMUxkt3EXyISGeORYggByWf9440l7DOjunS%2BqiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlOjWgzIFI97pH%2FOOKtwDeAX%2F6nsJHCLj9nCsJFA5oSWoFzoobjFQNbXbSq%2FT0XqItIFU%2BDcBdziP2lC00oMSlvwFgUKloJt23UZdOZs2LsFWtxK5XV9LO1uz8t9NTVlbdWhqiuEp8meJ57cL00iRS2wE6T3wK1F5NuhXuPmuV2m9EpgUxchj9KVJIDhzU4R9KME20L6ZFDGhIs1%2BdhiSpjHjqcZgTrri8mZQFy%2BNZQKKuQddjcvyPg4wFhPoL%2FFvUm1cVaUvuVYuk7aA6oBCo8XZcODTnDSKGUW4ESebQGHG7g3VLpB2tK6d3SVd2habTOtYmmeJU8MbhrmdHVcE%2BMTvoOUsqAnL7iLhyvorIjGrgFxTimhHEHn25PMuZ2TNL0fU9wS4%2FYNKQTc7OFeO0Bc9XyY0EviXeoaGTak2%2B%2FfXbZYHekSghK7qoRFLyjFShs32snxLsYprM7PHaaI0wt5pgVykpLnGfark3%2F0PnBHF3A7RZ31%2BUb5kw9pY0jYtymyuBXXSD98wUdasV2eJYGdFzfvPWOqGPVdyitqIxIUsWjKwdgHqb65jvF5Sy7SY%2BTX%2BiRq2%2B%2FZLVLGerYLRdXnExncAxEOgvKsvexKrtChIvMfbLy8nLzImOrAiKiwRjoEWY7g9yJHDolIw48Wi1AY6pgF3P%2BAOPbkW%2F18eaJV8sB3hn0m8JreGd7NQGL%2FzunayWBn6ZsbqiLPvcDuJ8FKg8SVsmDjX9GaT3sgNqcAV7ELddTFco1ROrlNOeX7yjXBl8eIoKfI3W3Jq6ekYcH4baU%2F2rZ%2B%2Fnv7pbtj%2BDNeX6ImUtx2CWa6pUnKwEFupPw%2F1LypuXkNgt9Mek8vkMT6CsLPV1hoXeV1iI53pRdjNkPo8JXk0NpOg&X-Amz-Signature=af3a754dee35648142a3ec885152f4781d27ee96066b4beb551ef15a05c1201e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

# **Types of Input**

- **Arbitrary text, like blog posts**
- **Cookies**
- **Hidden form fields**
- **Parameters**
- **HTTP header fields, like User-Agent**
### **"Reject Known Bad"**

- **Also called "blacklisting"**
  - **Least effective method**
  - **Difficult to identify all bad inputs**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0be217f7-f659-4558-9619-18c04191a44e/image33.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z5LVJU35%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210143Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFBPol9pbtkVbZLkjNQMLz7Q3ZS8o6NG9e9okBw7DapHAiA3A0kGOMUxkt3EXyISGeORYggByWf9440l7DOjunS%2BqiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlOjWgzIFI97pH%2FOOKtwDeAX%2F6nsJHCLj9nCsJFA5oSWoFzoobjFQNbXbSq%2FT0XqItIFU%2BDcBdziP2lC00oMSlvwFgUKloJt23UZdOZs2LsFWtxK5XV9LO1uz8t9NTVlbdWhqiuEp8meJ57cL00iRS2wE6T3wK1F5NuhXuPmuV2m9EpgUxchj9KVJIDhzU4R9KME20L6ZFDGhIs1%2BdhiSpjHjqcZgTrri8mZQFy%2BNZQKKuQddjcvyPg4wFhPoL%2FFvUm1cVaUvuVYuk7aA6oBCo8XZcODTnDSKGUW4ESebQGHG7g3VLpB2tK6d3SVd2habTOtYmmeJU8MbhrmdHVcE%2BMTvoOUsqAnL7iLhyvorIjGrgFxTimhHEHn25PMuZ2TNL0fU9wS4%2FYNKQTc7OFeO0Bc9XyY0EviXeoaGTak2%2B%2FfXbZYHekSghK7qoRFLyjFShs32snxLsYprM7PHaaI0wt5pgVykpLnGfark3%2F0PnBHF3A7RZ31%2BUb5kw9pY0jYtymyuBXXSD98wUdasV2eJYGdFzfvPWOqGPVdyitqIxIUsWjKwdgHqb65jvF5Sy7SY%2BTX%2BiRq2%2B%2FZLVLGerYLRdXnExncAxEOgvKsvexKrtChIvMfbLy8nLzImOrAiKiwRjoEWY7g9yJHDolIw48Wi1AY6pgF3P%2BAOPbkW%2F18eaJV8sB3hn0m8JreGd7NQGL%2FzunayWBn6ZsbqiLPvcDuJ8FKg8SVsmDjX9GaT3sgNqcAV7ELddTFco1ROrlNOeX7yjXBl8eIoKfI3W3Jq6ekYcH4baU%2F2rZ%2B%2Fnv7pbtj%2BDNeX6ImUtx2CWa6pUnKwEFupPw%2F1LypuXkNgt9Mek8vkMT6CsLPV1hoXeV1iI53pRdjNkPo8JXk0NpOg&X-Amz-Signature=103c9873a19a856201e310cfce9b38d6f311d4654ca656ac3ec69f5515c65e0d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3455a3ee-c990-4c53-95f9-9bcb815cf625/image34.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z5LVJU35%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210143Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFBPol9pbtkVbZLkjNQMLz7Q3ZS8o6NG9e9okBw7DapHAiA3A0kGOMUxkt3EXyISGeORYggByWf9440l7DOjunS%2BqiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlOjWgzIFI97pH%2FOOKtwDeAX%2F6nsJHCLj9nCsJFA5oSWoFzoobjFQNbXbSq%2FT0XqItIFU%2BDcBdziP2lC00oMSlvwFgUKloJt23UZdOZs2LsFWtxK5XV9LO1uz8t9NTVlbdWhqiuEp8meJ57cL00iRS2wE6T3wK1F5NuhXuPmuV2m9EpgUxchj9KVJIDhzU4R9KME20L6ZFDGhIs1%2BdhiSpjHjqcZgTrri8mZQFy%2BNZQKKuQddjcvyPg4wFhPoL%2FFvUm1cVaUvuVYuk7aA6oBCo8XZcODTnDSKGUW4ESebQGHG7g3VLpB2tK6d3SVd2habTOtYmmeJU8MbhrmdHVcE%2BMTvoOUsqAnL7iLhyvorIjGrgFxTimhHEHn25PMuZ2TNL0fU9wS4%2FYNKQTc7OFeO0Bc9XyY0EviXeoaGTak2%2B%2FfXbZYHekSghK7qoRFLyjFShs32snxLsYprM7PHaaI0wt5pgVykpLnGfark3%2F0PnBHF3A7RZ31%2BUb5kw9pY0jYtymyuBXXSD98wUdasV2eJYGdFzfvPWOqGPVdyitqIxIUsWjKwdgHqb65jvF5Sy7SY%2BTX%2BiRq2%2B%2FZLVLGerYLRdXnExncAxEOgvKsvexKrtChIvMfbLy8nLzImOrAiKiwRjoEWY7g9yJHDolIw48Wi1AY6pgF3P%2BAOPbkW%2F18eaJV8sB3hn0m8JreGd7NQGL%2FzunayWBn6ZsbqiLPvcDuJ8FKg8SVsmDjX9GaT3sgNqcAV7ELddTFco1ROrlNOeX7yjXBl8eIoKfI3W3Jq6ekYcH4baU%2F2rZ%2B%2Fnv7pbtj%2BDNeX6ImUtx2CWa6pUnKwEFupPw%2F1LypuXkNgt9Mek8vkMT6CsLPV1hoXeV1iI53pRdjNkPo8JXk0NpOg&X-Amz-Signature=2b7a074cb3b0aa47d8c8ba8705aeeded2d753f2f1098c5c0b5e562717e761959&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/20ab29ba-ef80-4a1c-aaf5-e7ffc8ff33b9/image35.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z5LVJU35%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210143Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFBPol9pbtkVbZLkjNQMLz7Q3ZS8o6NG9e9okBw7DapHAiA3A0kGOMUxkt3EXyISGeORYggByWf9440l7DOjunS%2BqiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlOjWgzIFI97pH%2FOOKtwDeAX%2F6nsJHCLj9nCsJFA5oSWoFzoobjFQNbXbSq%2FT0XqItIFU%2BDcBdziP2lC00oMSlvwFgUKloJt23UZdOZs2LsFWtxK5XV9LO1uz8t9NTVlbdWhqiuEp8meJ57cL00iRS2wE6T3wK1F5NuhXuPmuV2m9EpgUxchj9KVJIDhzU4R9KME20L6ZFDGhIs1%2BdhiSpjHjqcZgTrri8mZQFy%2BNZQKKuQddjcvyPg4wFhPoL%2FFvUm1cVaUvuVYuk7aA6oBCo8XZcODTnDSKGUW4ESebQGHG7g3VLpB2tK6d3SVd2habTOtYmmeJU8MbhrmdHVcE%2BMTvoOUsqAnL7iLhyvorIjGrgFxTimhHEHn25PMuZ2TNL0fU9wS4%2FYNKQTc7OFeO0Bc9XyY0EviXeoaGTak2%2B%2FfXbZYHekSghK7qoRFLyjFShs32snxLsYprM7PHaaI0wt5pgVykpLnGfark3%2F0PnBHF3A7RZ31%2BUb5kw9pY0jYtymyuBXXSD98wUdasV2eJYGdFzfvPWOqGPVdyitqIxIUsWjKwdgHqb65jvF5Sy7SY%2BTX%2BiRq2%2B%2FZLVLGerYLRdXnExncAxEOgvKsvexKrtChIvMfbLy8nLzImOrAiKiwRjoEWY7g9yJHDolIw48Wi1AY6pgF3P%2BAOPbkW%2F18eaJV8sB3hn0m8JreGd7NQGL%2FzunayWBn6ZsbqiLPvcDuJ8FKg8SVsmDjX9GaT3sgNqcAV7ELddTFco1ROrlNOeX7yjXBl8eIoKfI3W3Jq6ekYcH4baU%2F2rZ%2B%2Fnv7pbtj%2BDNeX6ImUtx2CWa6pUnKwEFupPw%2F1LypuXkNgt9Mek8vkMT6CsLPV1hoXeV1iI53pRdjNkPo8JXk0NpOg&X-Amz-Signature=9b8e5657778af8bcbdf40ee582e2ffd0545d94f80ccaac08ffd9b9796d18918b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

# **"Accept Known Good"**

- **Also called "whitelisting"**
- **Most effective technique, where feasible**
- **However, sometimes you can't do it**
  - **Human names really contain apostrophes, so you can't filter them out**
# **Sanitization**

- **Render dangerous input harmless**
- **HTML-Encoding: Space becomes %20, etc.**
- **Difficult if several kinds of data may be present within an item of input**
  - **Boundary validation is better (four slides ahead)**
# **Safe Data Handling**

- **Write code that can't be fooled by malicious data**
  - **SQL parameterized queries**
  - **Don't pass user input to an OS command line**
- **Effective when it can be applied**
# **Semantic Checks**

- **Some malicious input is identical to valid input**
  - **Such as changing an account number to another customer's number**
- **Data must be validated in context**
  - **Does this account number being to the currently logged-in user?**
### Difficulties with Simple Input **Validation**

- **Data coming from user is "bad" or "untrusted"**
- **The server-side app is "good" and trusted**
  - **Many different types of input with different filtering requirements**
  - **Apps may chain several processing steps together**
    - **Data may be harmless at one stage, but be transformed into harmful data at another stage**
# **Boundary Validation**

- **Trust boundary**
  - **Divides a trusted zone from an untrusted zone**
- **Clean data that passes a boundary**
  - **Such as from the user into an application**
# **Boundary Validation**

- **Each component treats its input as potentially malicious**
- **Data validation performed at each trust boundary**
  - **Not just between client and server**
# **Example**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d0a08c80-f41b-45af-b103-2e24622ecdb3/image36.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z5LVJU35%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210143Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFBPol9pbtkVbZLkjNQMLz7Q3ZS8o6NG9e9okBw7DapHAiA3A0kGOMUxkt3EXyISGeORYggByWf9440l7DOjunS%2BqiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlOjWgzIFI97pH%2FOOKtwDeAX%2F6nsJHCLj9nCsJFA5oSWoFzoobjFQNbXbSq%2FT0XqItIFU%2BDcBdziP2lC00oMSlvwFgUKloJt23UZdOZs2LsFWtxK5XV9LO1uz8t9NTVlbdWhqiuEp8meJ57cL00iRS2wE6T3wK1F5NuhXuPmuV2m9EpgUxchj9KVJIDhzU4R9KME20L6ZFDGhIs1%2BdhiSpjHjqcZgTrri8mZQFy%2BNZQKKuQddjcvyPg4wFhPoL%2FFvUm1cVaUvuVYuk7aA6oBCo8XZcODTnDSKGUW4ESebQGHG7g3VLpB2tK6d3SVd2habTOtYmmeJU8MbhrmdHVcE%2BMTvoOUsqAnL7iLhyvorIjGrgFxTimhHEHn25PMuZ2TNL0fU9wS4%2FYNKQTc7OFeO0Bc9XyY0EviXeoaGTak2%2B%2FfXbZYHekSghK7qoRFLyjFShs32snxLsYprM7PHaaI0wt5pgVykpLnGfark3%2F0PnBHF3A7RZ31%2BUb5kw9pY0jYtymyuBXXSD98wUdasV2eJYGdFzfvPWOqGPVdyitqIxIUsWjKwdgHqb65jvF5Sy7SY%2BTX%2BiRq2%2B%2FZLVLGerYLRdXnExncAxEOgvKsvexKrtChIvMfbLy8nLzImOrAiKiwRjoEWY7g9yJHDolIw48Wi1AY6pgF3P%2BAOPbkW%2F18eaJV8sB3hn0m8JreGd7NQGL%2FzunayWBn6ZsbqiLPvcDuJ8FKg8SVsmDjX9GaT3sgNqcAV7ELddTFco1ROrlNOeX7yjXBl8eIoKfI3W3Jq6ekYcH4baU%2F2rZ%2B%2Fnv7pbtj%2BDNeX6ImUtx2CWa6pUnKwEFupPw%2F1LypuXkNgt9Mek8vkMT6CsLPV1hoXeV1iI53pRdjNkPo8JXk0NpOg&X-Amz-Signature=77aa53c70def4ccdc4caf6b0c2efbd70a8e37d5361d4e3164d31d6018aa7242b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> Example SOAP Request

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d54353c7-1ad1-49d6-b966-0e7fc105182e/image37.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z5LVJU35%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210143Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFBPol9pbtkVbZLkjNQMLz7Q3ZS8o6NG9e9okBw7DapHAiA3A0kGOMUxkt3EXyISGeORYggByWf9440l7DOjunS%2BqiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlOjWgzIFI97pH%2FOOKtwDeAX%2F6nsJHCLj9nCsJFA5oSWoFzoobjFQNbXbSq%2FT0XqItIFU%2BDcBdziP2lC00oMSlvwFgUKloJt23UZdOZs2LsFWtxK5XV9LO1uz8t9NTVlbdWhqiuEp8meJ57cL00iRS2wE6T3wK1F5NuhXuPmuV2m9EpgUxchj9KVJIDhzU4R9KME20L6ZFDGhIs1%2BdhiSpjHjqcZgTrri8mZQFy%2BNZQKKuQddjcvyPg4wFhPoL%2FFvUm1cVaUvuVYuk7aA6oBCo8XZcODTnDSKGUW4ESebQGHG7g3VLpB2tK6d3SVd2habTOtYmmeJU8MbhrmdHVcE%2BMTvoOUsqAnL7iLhyvorIjGrgFxTimhHEHn25PMuZ2TNL0fU9wS4%2FYNKQTc7OFeO0Bc9XyY0EviXeoaGTak2%2B%2FfXbZYHekSghK7qoRFLyjFShs32snxLsYprM7PHaaI0wt5pgVykpLnGfark3%2F0PnBHF3A7RZ31%2BUb5kw9pY0jYtymyuBXXSD98wUdasV2eJYGdFzfvPWOqGPVdyitqIxIUsWjKwdgHqb65jvF5Sy7SY%2BTX%2BiRq2%2B%2FZLVLGerYLRdXnExncAxEOgvKsvexKrtChIvMfbLy8nLzImOrAiKiwRjoEWY7g9yJHDolIw48Wi1AY6pgF3P%2BAOPbkW%2F18eaJV8sB3hn0m8JreGd7NQGL%2FzunayWBn6ZsbqiLPvcDuJ8FKg8SVsmDjX9GaT3sgNqcAV7ELddTFco1ROrlNOeX7yjXBl8eIoKfI3W3Jq6ekYcH4baU%2F2rZ%2B%2Fnv7pbtj%2BDNeX6ImUtx2CWa6pUnKwEFupPw%2F1LypuXkNgt9Mek8vkMT6CsLPV1hoXeV1iI53pRdjNkPo8JXk0NpOg&X-Amz-Signature=c06e194a41b6ce2bebbc11f7a258022263625a46a5166794671b352a7e53dc0d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Link Ch 2a**
### Boundary Validation Example

- **1. App gets login: username and password**
  - **Allows only good characters, limits length, removes known attack signatures**
- **2. App performs a SQL query to verify credentials**
  - **Escape dangerous characters**
### Boundary Validation Example

- **3. Login succeeds; app passes data from user profile to a SOAP service**
  - **XML metacharacters are encoded to block SOAP injection**
- **4. App displays user's account information back to the user's browser**
  - **User-supplied data is HTML-encoded to block XSS**
# **Filtering Problems**

- **App removes this string:**
  - **<script>**
- **So attacker sends this**
  - **<scr<script>ipt>**
# **Multistep Validation**

- **App first removes**
> ../

- **Then removes**
> ..\

- **Attacker sends**
> ....\/

# **Canonicalization**

- **App gets URL-encoded data from Web browser**
  - **Apostrophe is %27**
  - **Percent is %25**
- **To block apostrophes, app filters %27**
- **But URL is decoded twice by mistake**
  - **%2527 becomes %27 becomes apostrophe**
# **Handling Attackers**

- **Handling errors**
- **Maintaining audit logs**
- **Alerting administrators**
- **Reacting to attacks**
# **Handling Errors**

- **Show appropriate error messages**
- **Unhandled errors lead to overly-informative error messages like this**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/6427d727-990b-4736-a734-c33cdacf0bbd/image38.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z5LVJU35%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210143Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFBPol9pbtkVbZLkjNQMLz7Q3ZS8o6NG9e9okBw7DapHAiA3A0kGOMUxkt3EXyISGeORYggByWf9440l7DOjunS%2BqiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlOjWgzIFI97pH%2FOOKtwDeAX%2F6nsJHCLj9nCsJFA5oSWoFzoobjFQNbXbSq%2FT0XqItIFU%2BDcBdziP2lC00oMSlvwFgUKloJt23UZdOZs2LsFWtxK5XV9LO1uz8t9NTVlbdWhqiuEp8meJ57cL00iRS2wE6T3wK1F5NuhXuPmuV2m9EpgUxchj9KVJIDhzU4R9KME20L6ZFDGhIs1%2BdhiSpjHjqcZgTrri8mZQFy%2BNZQKKuQddjcvyPg4wFhPoL%2FFvUm1cVaUvuVYuk7aA6oBCo8XZcODTnDSKGUW4ESebQGHG7g3VLpB2tK6d3SVd2habTOtYmmeJU8MbhrmdHVcE%2BMTvoOUsqAnL7iLhyvorIjGrgFxTimhHEHn25PMuZ2TNL0fU9wS4%2FYNKQTc7OFeO0Bc9XyY0EviXeoaGTak2%2B%2FfXbZYHekSghK7qoRFLyjFShs32snxLsYprM7PHaaI0wt5pgVykpLnGfark3%2F0PnBHF3A7RZ31%2BUb5kw9pY0jYtymyuBXXSD98wUdasV2eJYGdFzfvPWOqGPVdyitqIxIUsWjKwdgHqb65jvF5Sy7SY%2BTX%2BiRq2%2B%2FZLVLGerYLRdXnExncAxEOgvKsvexKrtChIvMfbLy8nLzImOrAiKiwRjoEWY7g9yJHDolIw48Wi1AY6pgF3P%2BAOPbkW%2F18eaJV8sB3hn0m8JreGd7NQGL%2FzunayWBn6ZsbqiLPvcDuJ8FKg8SVsmDjX9GaT3sgNqcAV7ELddTFco1ROrlNOeX7yjXBl8eIoKfI3W3Jq6ekYcH4baU%2F2rZ%2B%2Fnv7pbtj%2BDNeX6ImUtx2CWa6pUnKwEFupPw%2F1LypuXkNgt9Mek8vkMT6CsLPV1hoXeV1iI53pRdjNkPo8JXk0NpOg&X-Amz-Signature=80eab90cb55c4e8649b2bee23086609a831e0ea98aa2c4683eaa573600efbed1&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

# **Audit Logs**

- **Authentication events: login success and failure, change of password**
- **Key transactions, such as credit card payments**
- **Access attempts that are blocked by access control mechanisms**
- **Requests containing known attack strings**
- **For high security, log every client request in full**
# **Protecting Logs**

- **Logs should contain time, IP addresses, and username**
  - **May contain cookies and other sensitive data**
- **Attackers will try to erase and/or read logs**
- **Log must be protected**
  - **Place on an autonomous system that only accepts update messages**
  - **Flush logs to write-once media**
# **Alerting Administrators**

- **Usage anomalies, like a large number of requests from the same IP address or user**
- **Business anomalies, such as a large number of funds transfers to/from the same account**
- **Requests containing known attack strings**
- **Requests where hidden data has been modified**
# **Firewalls**

- **Web App Firewalls can detect generic attacks**
  - **But not subtle ones that are specific to your app**
- **Most effective security control is integrated with app's input validation mechanisms**
  - **Check for valid values of your parameters**
# **Reacting to Attacks**

- **Attackers probe for vulnerabilities**
- **Sending many similar requests**
- **Automated defenses**
  - **Respond increasingly slowly to requests**
  - **Terminate the attacker's session**
### **Managing the Application**

- **Management interface allows administrator to control user accounts, roles, access monitoring, auditing, etc.**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ce5c8c3e-7e63-487a-8d3f-b7ce1eaa22fe/image39.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SL3OB376%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210153Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCr5L%2FSnVJZXpSAc3leO9sOpTzMFKT0c6IqpvQqwAf%2BgwIgPXcg6%2Fg4%2F7lVCyhX2qSJVopY7rResLVqmAPXyv8lXXgqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDEktrbwFrstBih791SrcAwEcH5YHLs7ofFmZ4revGcGMC2qYspOrOQ090FTkK%2B%2BPfLCmY2oKZj5TWw2P9BFJ3pwLNjhpo03wDvIYWay%2BXECFNpGxzOQSIVK4d1CQdC0ws6nApKdxJSrOx95bbVF%2BkWKSIq%2FjhT9RsUEaM9DVlyPE9Wl0N5EnaGFujVgEVg7t%2B%2BnbpdWg9fu9lFwDeKqkbBmuhOAGgDH8TtCdBQJmdbtUUz0ya4kR5z6Q%2F8orVSoGo%2FIbVHmcZZuIPbPkPIN79AfdPIMUPH04tCPGt5GqyToyMpL%2FXQnStQh7RjEnudwPzTe%2F7qkeUMow6X1SDaiw3JlLUOPG6ZuW5V3EFZ2n8Z9lbY%2FvuGvpvxsiRns12xF0VV%2FDIKIGcQF4FhyQbVcf3KQ5wys7skHdrjNFgWmXHcgyUCAkjYp%2B6MQIM7R52ArKd7fzegb66nwq2JOc99waakdto%2FQwj8LT9OUw0RBrruU1v3%2FICIOHKWoXDEamqugGfVV56GqrVsyILNkY0xwKADZG1GeYpRqkEquCijafcfJF40IIBBUFoVer%2FB73rM2UqpSpuPpGlbwIOxhfmrFsQAL9%2B7DR38MgJ%2BbMlWDWkSxBa1oZN2EJXCkPnMUYiFD3attjJLu3Acna7vppMPHIotQGOqUB9YnGv0DdFvQnvuo1O2VN83ChlTn%2Ff0arbB%2BQ9ORczzc41bLs8N6XoMX71PhZM0Jr3HKPxI4GKMs5TkpdrG5Xav0qWB1m4oac%2BcHQXFm2kGr13y%2BcRz8%2FzVa5KrAnK9nX4PNAkzr3mdLNJ%2FedNgumq92Pwjkq9vV0JXp%2BiLUkuUPo4jIokjmxERWOaZUHabLfNZYxZNEBcIpW4I%2Bu1cYCepkczCJS&X-Amz-Signature=d27341c1e6c5d0d8e88659a7c7b43acfc60e8eea26e1faccff408fcfe3c78d84&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### **Attacking the Administration Panel**

- **Defeat weak authentication**
- **Some administrative functions might not require high privileges**
- **XSS flaws can allow cookie theft and session hijacking**