# Chapter 1 Web Application (In)security

# **Web Applications**

- **E-commerce, Social networks, Online banking, etc.**
- **Fundamental security problem:**
  - ***Users can supply arbitrary input***
- **Malicious input can compromise the site**
# **Static Website: Web 1.0**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8b9196bf-6d68-413e-99df-9ee47137c06d/image2.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666MMDZONH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204458Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDamAEU%2BKKgo9Zc20jEvyayR%2FuHx1DKzMSt3T%2Bp2RSZNwIhAJwSvCj0IBB9mpuOttu5F8zrBpUpb%2BW6d19jHOtmwXTEKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwE4APlUlUGz5HqQOYq3ANMaRUvYhYVo2zkj1xWX9IDsNYnVS%2BP5ycJpRFi5tYzRmVv1UUcmWUdioqh87lxz0g%2B1QHU170oGYXy6sJ715vcBsoQwcQK9QDXUqCz%2BnnKvAi13Tqtp8eTM6zLq356l%2FKXUuNxeM%2Fnhr8CNL0OK%2FW1PnRSFUhKYPRYXC8tkwWvex%2B3NY4QS%2Fb3FmGnQgrk%2BsBK7uko6ZNMaJGIzLG9MF7Xhq%2Be%2FpjFmlBfg8f55jC1RVXmLy%2BPof3nPB3cXIi%2F%2BiS8WB5I0PRzy6HRduQCgTF6fOgi63XMi64yARqo9QSdWmuiG0G0AhI43jhZTzNNCkDwqzCqy3tTV4hm3857%2BNme%2FxMUNXpecPC9XbUf8PXlW4RRDnmD8dbfCZokObzNG8aN3gKkaSdJXq2jjU9ihH2ewaEQrAgI%2BrpKSsCuQnLUKoCTyQrBUi%2ByT2eaZJKqTx%2FX83bdwlBAXite85yfb%2BcFWXE00A26BQntSgyASeT%2BGDUXuxDNuqZDoWmA7foHcyYhD6E%2FzuvTlJcaci4LkwUuJ%2FBvN1HtSQk10AmLUyP9gV5cVpAxgtdEtaFTdPlnG%2FB1sEY8sS2xp5PUnQpWzG7kPma77hE7ufzVYtOcnXAPDSYESTxg6vTsW1z1DzCnxqLUBjqkAZVJ%2F91o8fskEYkUgFbPnwoBc2nYkt9CwnP%2F2k1lx7EODv4sPYHG87AWaUYLlPz1VKM11KTrCn8zHbvdnKAwRAxda7kqIwn2lcqVuYULLOSlLc312DCRcQttBUxvJ7TeoMc7z0LXQfxKP9GrQWcOf9GsFIqb5Yrtk37LFR5aqLuM2hda0dxe6knUZcytxgBS2MuexZ6dT4A481SNqxMHsQHReny0&X-Amz-Signature=1d45740223ad36a2130e36abe30685c74be3f4ec7be1922c7e15444f576f8e04&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- Information flows one-way
- Users don't log in,
> shop, or submit comments

- An attacker who exploits flaws in the Web server software can
  - Steal data on the Web server (usually only public data anyway)
  - Deface the site
# **Modern Web App**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cf3f68c5-5215-45eb-8a6e-bd6750a2c528/image3.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666MMDZONH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204458Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDamAEU%2BKKgo9Zc20jEvyayR%2FuHx1DKzMSt3T%2Bp2RSZNwIhAJwSvCj0IBB9mpuOttu5F8zrBpUpb%2BW6d19jHOtmwXTEKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwE4APlUlUGz5HqQOYq3ANMaRUvYhYVo2zkj1xWX9IDsNYnVS%2BP5ycJpRFi5tYzRmVv1UUcmWUdioqh87lxz0g%2B1QHU170oGYXy6sJ715vcBsoQwcQK9QDXUqCz%2BnnKvAi13Tqtp8eTM6zLq356l%2FKXUuNxeM%2Fnhr8CNL0OK%2FW1PnRSFUhKYPRYXC8tkwWvex%2B3NY4QS%2Fb3FmGnQgrk%2BsBK7uko6ZNMaJGIzLG9MF7Xhq%2Be%2FpjFmlBfg8f55jC1RVXmLy%2BPof3nPB3cXIi%2F%2BiS8WB5I0PRzy6HRduQCgTF6fOgi63XMi64yARqo9QSdWmuiG0G0AhI43jhZTzNNCkDwqzCqy3tTV4hm3857%2BNme%2FxMUNXpecPC9XbUf8PXlW4RRDnmD8dbfCZokObzNG8aN3gKkaSdJXq2jjU9ihH2ewaEQrAgI%2BrpKSsCuQnLUKoCTyQrBUi%2ByT2eaZJKqTx%2FX83bdwlBAXite85yfb%2BcFWXE00A26BQntSgyASeT%2BGDUXuxDNuqZDoWmA7foHcyYhD6E%2FzuvTlJcaci4LkwUuJ%2FBvN1HtSQk10AmLUyP9gV5cVpAxgtdEtaFTdPlnG%2FB1sEY8sS2xp5PUnQpWzG7kPma77hE7ufzVYtOcnXAPDSYESTxg6vTsW1z1DzCnxqLUBjqkAZVJ%2F91o8fskEYkUgFbPnwoBc2nYkt9CwnP%2F2k1lx7EODv4sPYHG87AWaUYLlPz1VKM11KTrCn8zHbvdnKAwRAxda7kqIwn2lcqVuYULLOSlLc312DCRcQttBUxvJ7TeoMc7z0LXQfxKP9GrQWcOf9GsFIqb5Yrtk37LFR5aqLuM2hda0dxe6knUZcytxgBS2MuexZ6dT4A481SNqxMHsQHReny0&X-Amz-Signature=b6cbd215c02492c0d29aac9dad3893e345564b7a73a429e07384e5e6b1c8462b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ab4feb1b-b3a2-491d-aad4-20d6314adafb/image4.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666MMDZONH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204458Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDamAEU%2BKKgo9Zc20jEvyayR%2FuHx1DKzMSt3T%2Bp2RSZNwIhAJwSvCj0IBB9mpuOttu5F8zrBpUpb%2BW6d19jHOtmwXTEKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwE4APlUlUGz5HqQOYq3ANMaRUvYhYVo2zkj1xWX9IDsNYnVS%2BP5ycJpRFi5tYzRmVv1UUcmWUdioqh87lxz0g%2B1QHU170oGYXy6sJ715vcBsoQwcQK9QDXUqCz%2BnnKvAi13Tqtp8eTM6zLq356l%2FKXUuNxeM%2Fnhr8CNL0OK%2FW1PnRSFUhKYPRYXC8tkwWvex%2B3NY4QS%2Fb3FmGnQgrk%2BsBK7uko6ZNMaJGIzLG9MF7Xhq%2Be%2FpjFmlBfg8f55jC1RVXmLy%2BPof3nPB3cXIi%2F%2BiS8WB5I0PRzy6HRduQCgTF6fOgi63XMi64yARqo9QSdWmuiG0G0AhI43jhZTzNNCkDwqzCqy3tTV4hm3857%2BNme%2FxMUNXpecPC9XbUf8PXlW4RRDnmD8dbfCZokObzNG8aN3gKkaSdJXq2jjU9ihH2ewaEQrAgI%2BrpKSsCuQnLUKoCTyQrBUi%2ByT2eaZJKqTx%2FX83bdwlBAXite85yfb%2BcFWXE00A26BQntSgyASeT%2BGDUXuxDNuqZDoWmA7foHcyYhD6E%2FzuvTlJcaci4LkwUuJ%2FBvN1HtSQk10AmLUyP9gV5cVpAxgtdEtaFTdPlnG%2FB1sEY8sS2xp5PUnQpWzG7kPma77hE7ufzVYtOcnXAPDSYESTxg6vTsW1z1DzCnxqLUBjqkAZVJ%2F91o8fskEYkUgFbPnwoBc2nYkt9CwnP%2F2k1lx7EODv4sPYHG87AWaUYLlPz1VKM11KTrCn8zHbvdnKAwRAxda7kqIwn2lcqVuYULLOSlLc312DCRcQttBUxvJ7TeoMc7z0LXQfxKP9GrQWcOf9GsFIqb5Yrtk37LFR5aqLuM2hda0dxe6knUZcytxgBS2MuexZ6dT4A481SNqxMHsQHReny0&X-Amz-Signature=ec1d86146a63c8c57d04e5a015c384740a7ebd2c730e162f6858ebc30c46d064&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- A frequent claim, very far from the truth
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c9c2110f-2577-49de-b49f-1745aa19ead8/image6.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666MMDZONH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204458Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDamAEU%2BKKgo9Zc20jEvyayR%2FuHx1DKzMSt3T%2Bp2RSZNwIhAJwSvCj0IBB9mpuOttu5F8zrBpUpb%2BW6d19jHOtmwXTEKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwE4APlUlUGz5HqQOYq3ANMaRUvYhYVo2zkj1xWX9IDsNYnVS%2BP5ycJpRFi5tYzRmVv1UUcmWUdioqh87lxz0g%2B1QHU170oGYXy6sJ715vcBsoQwcQK9QDXUqCz%2BnnKvAi13Tqtp8eTM6zLq356l%2FKXUuNxeM%2Fnhr8CNL0OK%2FW1PnRSFUhKYPRYXC8tkwWvex%2B3NY4QS%2Fb3FmGnQgrk%2BsBK7uko6ZNMaJGIzLG9MF7Xhq%2Be%2FpjFmlBfg8f55jC1RVXmLy%2BPof3nPB3cXIi%2F%2BiS8WB5I0PRzy6HRduQCgTF6fOgi63XMi64yARqo9QSdWmuiG0G0AhI43jhZTzNNCkDwqzCqy3tTV4hm3857%2BNme%2FxMUNXpecPC9XbUf8PXlW4RRDnmD8dbfCZokObzNG8aN3gKkaSdJXq2jjU9ihH2ewaEQrAgI%2BrpKSsCuQnLUKoCTyQrBUi%2ByT2eaZJKqTx%2FX83bdwlBAXite85yfb%2BcFWXE00A26BQntSgyASeT%2BGDUXuxDNuqZDoWmA7foHcyYhD6E%2FzuvTlJcaci4LkwUuJ%2FBvN1HtSQk10AmLUyP9gV5cVpAxgtdEtaFTdPlnG%2FB1sEY8sS2xp5PUnQpWzG7kPma77hE7ufzVYtOcnXAPDSYESTxg6vTsW1z1DzCnxqLUBjqkAZVJ%2F91o8fskEYkUgFbPnwoBc2nYkt9CwnP%2F2k1lx7EODv4sPYHG87AWaUYLlPz1VKM11KTrCn8zHbvdnKAwRAxda7kqIwn2lcqVuYULLOSlLc312DCRcQttBUxvJ7TeoMc7z0LXQfxKP9GrQWcOf9GsFIqb5Yrtk37LFR5aqLuM2hda0dxe6knUZcytxgBS2MuexZ6dT4A481SNqxMHsQHReny0&X-Amz-Signature=5ad3da6f3f1ac9d5f11fcd59fe5bd942e9f5a6ef03d22381424e0822efb78a7b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

## SinVR Hack

- Unauthenticated request allows anyone to download PII from users
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ba36e809-cc44-4568-a6dd-d84e1997f56a/image7.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666MMDZONH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204458Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDamAEU%2BKKgo9Zc20jEvyayR%2FuHx1DKzMSt3T%2Bp2RSZNwIhAJwSvCj0IBB9mpuOttu5F8zrBpUpb%2BW6d19jHOtmwXTEKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwE4APlUlUGz5HqQOYq3ANMaRUvYhYVo2zkj1xWX9IDsNYnVS%2BP5ycJpRFi5tYzRmVv1UUcmWUdioqh87lxz0g%2B1QHU170oGYXy6sJ715vcBsoQwcQK9QDXUqCz%2BnnKvAi13Tqtp8eTM6zLq356l%2FKXUuNxeM%2Fnhr8CNL0OK%2FW1PnRSFUhKYPRYXC8tkwWvex%2B3NY4QS%2Fb3FmGnQgrk%2BsBK7uko6ZNMaJGIzLG9MF7Xhq%2Be%2FpjFmlBfg8f55jC1RVXmLy%2BPof3nPB3cXIi%2F%2BiS8WB5I0PRzy6HRduQCgTF6fOgi63XMi64yARqo9QSdWmuiG0G0AhI43jhZTzNNCkDwqzCqy3tTV4hm3857%2BNme%2FxMUNXpecPC9XbUf8PXlW4RRDnmD8dbfCZokObzNG8aN3gKkaSdJXq2jjU9ihH2ewaEQrAgI%2BrpKSsCuQnLUKoCTyQrBUi%2ByT2eaZJKqTx%2FX83bdwlBAXite85yfb%2BcFWXE00A26BQntSgyASeT%2BGDUXuxDNuqZDoWmA7foHcyYhD6E%2FzuvTlJcaci4LkwUuJ%2FBvN1HtSQk10AmLUyP9gV5cVpAxgtdEtaFTdPlnG%2FB1sEY8sS2xp5PUnQpWzG7kPma77hE7ufzVYtOcnXAPDSYESTxg6vTsW1z1DzCnxqLUBjqkAZVJ%2F91o8fskEYkUgFbPnwoBc2nYkt9CwnP%2F2k1lx7EODv4sPYHG87AWaUYLlPz1VKM11KTrCn8zHbvdnKAwRAxda7kqIwn2lcqVuYULLOSlLc312DCRcQttBUxvJ7TeoMc7z0LXQfxKP9GrQWcOf9GsFIqb5Yrtk37LFR5aqLuM2hda0dxe6knUZcytxgBS2MuexZ6dT4A481SNqxMHsQHReny0&X-Amz-Signature=6a7af530bfa07598b6480218ac4d7a58bc1d52d801c49e48063b8d03cb7679e9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

# **PII**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fa5014a6-c5ef-4d89-9ef0-2760a5dbed5b/image8.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666MMDZONH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204458Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDamAEU%2BKKgo9Zc20jEvyayR%2FuHx1DKzMSt3T%2Bp2RSZNwIhAJwSvCj0IBB9mpuOttu5F8zrBpUpb%2BW6d19jHOtmwXTEKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwE4APlUlUGz5HqQOYq3ANMaRUvYhYVo2zkj1xWX9IDsNYnVS%2BP5ycJpRFi5tYzRmVv1UUcmWUdioqh87lxz0g%2B1QHU170oGYXy6sJ715vcBsoQwcQK9QDXUqCz%2BnnKvAi13Tqtp8eTM6zLq356l%2FKXUuNxeM%2Fnhr8CNL0OK%2FW1PnRSFUhKYPRYXC8tkwWvex%2B3NY4QS%2Fb3FmGnQgrk%2BsBK7uko6ZNMaJGIzLG9MF7Xhq%2Be%2FpjFmlBfg8f55jC1RVXmLy%2BPof3nPB3cXIi%2F%2BiS8WB5I0PRzy6HRduQCgTF6fOgi63XMi64yARqo9QSdWmuiG0G0AhI43jhZTzNNCkDwqzCqy3tTV4hm3857%2BNme%2FxMUNXpecPC9XbUf8PXlW4RRDnmD8dbfCZokObzNG8aN3gKkaSdJXq2jjU9ihH2ewaEQrAgI%2BrpKSsCuQnLUKoCTyQrBUi%2ByT2eaZJKqTx%2FX83bdwlBAXite85yfb%2BcFWXE00A26BQntSgyASeT%2BGDUXuxDNuqZDoWmA7foHcyYhD6E%2FzuvTlJcaci4LkwUuJ%2FBvN1HtSQk10AmLUyP9gV5cVpAxgtdEtaFTdPlnG%2FB1sEY8sS2xp5PUnQpWzG7kPma77hE7ufzVYtOcnXAPDSYESTxg6vTsW1z1DzCnxqLUBjqkAZVJ%2F91o8fskEYkUgFbPnwoBc2nYkt9CwnP%2F2k1lx7EODv4sPYHG87AWaUYLlPz1VKM11KTrCn8zHbvdnKAwRAxda7kqIwn2lcqVuYULLOSlLc312DCRcQttBUxvJ7TeoMc7z0LXQfxKP9GrQWcOf9GsFIqb5Yrtk37LFR5aqLuM2hda0dxe6knUZcytxgBS2MuexZ6dT4A481SNqxMHsQHReny0&X-Amz-Signature=a4a3ecaf2172a3dfbd7d607f14f121c22a05c9467317c9d9298254a6d3f900dc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e99c7c2a-4e30-4de5-8008-f853d82c3f1d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666MMDZONH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204458Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDamAEU%2BKKgo9Zc20jEvyayR%2FuHx1DKzMSt3T%2Bp2RSZNwIhAJwSvCj0IBB9mpuOttu5F8zrBpUpb%2BW6d19jHOtmwXTEKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwE4APlUlUGz5HqQOYq3ANMaRUvYhYVo2zkj1xWX9IDsNYnVS%2BP5ycJpRFi5tYzRmVv1UUcmWUdioqh87lxz0g%2B1QHU170oGYXy6sJ715vcBsoQwcQK9QDXUqCz%2BnnKvAi13Tqtp8eTM6zLq356l%2FKXUuNxeM%2Fnhr8CNL0OK%2FW1PnRSFUhKYPRYXC8tkwWvex%2B3NY4QS%2Fb3FmGnQgrk%2BsBK7uko6ZNMaJGIzLG9MF7Xhq%2Be%2FpjFmlBfg8f55jC1RVXmLy%2BPof3nPB3cXIi%2F%2BiS8WB5I0PRzy6HRduQCgTF6fOgi63XMi64yARqo9QSdWmuiG0G0AhI43jhZTzNNCkDwqzCqy3tTV4hm3857%2BNme%2FxMUNXpecPC9XbUf8PXlW4RRDnmD8dbfCZokObzNG8aN3gKkaSdJXq2jjU9ihH2ewaEQrAgI%2BrpKSsCuQnLUKoCTyQrBUi%2ByT2eaZJKqTx%2FX83bdwlBAXite85yfb%2BcFWXE00A26BQntSgyASeT%2BGDUXuxDNuqZDoWmA7foHcyYhD6E%2FzuvTlJcaci4LkwUuJ%2FBvN1HtSQk10AmLUyP9gV5cVpAxgtdEtaFTdPlnG%2FB1sEY8sS2xp5PUnQpWzG7kPma77hE7ufzVYtOcnXAPDSYESTxg6vTsW1z1DzCnxqLUBjqkAZVJ%2F91o8fskEYkUgFbPnwoBc2nYkt9CwnP%2F2k1lx7EODv4sPYHG87AWaUYLlPz1VKM11KTrCn8zHbvdnKAwRAxda7kqIwn2lcqVuYULLOSlLc312DCRcQttBUxvJ7TeoMc7z0LXQfxKP9GrQWcOf9GsFIqb5Yrtk37LFR5aqLuM2hda0dxe6knUZcytxgBS2MuexZ6dT4A481SNqxMHsQHReny0&X-Amz-Signature=46752ab8e854ca5dffeed2ba4da92d1ba7b5b8f36df7e0722e80e4d419eed395&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Binary Protections

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8ce765cb-e1f3-4664-bde6-36709fc96046/image15.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666MMDZONH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204458Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDamAEU%2BKKgo9Zc20jEvyayR%2FuHx1DKzMSt3T%2Bp2RSZNwIhAJwSvCj0IBB9mpuOttu5F8zrBpUpb%2BW6d19jHOtmwXTEKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwE4APlUlUGz5HqQOYq3ANMaRUvYhYVo2zkj1xWX9IDsNYnVS%2BP5ycJpRFi5tYzRmVv1UUcmWUdioqh87lxz0g%2B1QHU170oGYXy6sJ715vcBsoQwcQK9QDXUqCz%2BnnKvAi13Tqtp8eTM6zLq356l%2FKXUuNxeM%2Fnhr8CNL0OK%2FW1PnRSFUhKYPRYXC8tkwWvex%2B3NY4QS%2Fb3FmGnQgrk%2BsBK7uko6ZNMaJGIzLG9MF7Xhq%2Be%2FpjFmlBfg8f55jC1RVXmLy%2BPof3nPB3cXIi%2F%2BiS8WB5I0PRzy6HRduQCgTF6fOgi63XMi64yARqo9QSdWmuiG0G0AhI43jhZTzNNCkDwqzCqy3tTV4hm3857%2BNme%2FxMUNXpecPC9XbUf8PXlW4RRDnmD8dbfCZokObzNG8aN3gKkaSdJXq2jjU9ihH2ewaEQrAgI%2BrpKSsCuQnLUKoCTyQrBUi%2ByT2eaZJKqTx%2FX83bdwlBAXite85yfb%2BcFWXE00A26BQntSgyASeT%2BGDUXuxDNuqZDoWmA7foHcyYhD6E%2FzuvTlJcaci4LkwUuJ%2FBvN1HtSQk10AmLUyP9gV5cVpAxgtdEtaFTdPlnG%2FB1sEY8sS2xp5PUnQpWzG7kPma77hE7ufzVYtOcnXAPDSYESTxg6vTsW1z1DzCnxqLUBjqkAZVJ%2F91o8fskEYkUgFbPnwoBc2nYkt9CwnP%2F2k1lx7EODv4sPYHG87AWaUYLlPz1VKM11KTrCn8zHbvdnKAwRAxda7kqIwn2lcqVuYULLOSlLc312DCRcQttBUxvJ7TeoMc7z0LXQfxKP9GrQWcOf9GsFIqb5Yrtk37LFR5aqLuM2hda0dxe6knUZcytxgBS2MuexZ6dT4A481SNqxMHsQHReny0&X-Amz-Signature=e82c505f262edfd59426ebf82427fd2c7d0a3a768da3fe0b87f20f39f6e988c4&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0d109f1d-b571-4c0f-a8d2-c463d3065af6/image17.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666MMDZONH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204458Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDamAEU%2BKKgo9Zc20jEvyayR%2FuHx1DKzMSt3T%2Bp2RSZNwIhAJwSvCj0IBB9mpuOttu5F8zrBpUpb%2BW6d19jHOtmwXTEKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwE4APlUlUGz5HqQOYq3ANMaRUvYhYVo2zkj1xWX9IDsNYnVS%2BP5ycJpRFi5tYzRmVv1UUcmWUdioqh87lxz0g%2B1QHU170oGYXy6sJ715vcBsoQwcQK9QDXUqCz%2BnnKvAi13Tqtp8eTM6zLq356l%2FKXUuNxeM%2Fnhr8CNL0OK%2FW1PnRSFUhKYPRYXC8tkwWvex%2B3NY4QS%2Fb3FmGnQgrk%2BsBK7uko6ZNMaJGIzLG9MF7Xhq%2Be%2FpjFmlBfg8f55jC1RVXmLy%2BPof3nPB3cXIi%2F%2BiS8WB5I0PRzy6HRduQCgTF6fOgi63XMi64yARqo9QSdWmuiG0G0AhI43jhZTzNNCkDwqzCqy3tTV4hm3857%2BNme%2FxMUNXpecPC9XbUf8PXlW4RRDnmD8dbfCZokObzNG8aN3gKkaSdJXq2jjU9ihH2ewaEQrAgI%2BrpKSsCuQnLUKoCTyQrBUi%2ByT2eaZJKqTx%2FX83bdwlBAXite85yfb%2BcFWXE00A26BQntSgyASeT%2BGDUXuxDNuqZDoWmA7foHcyYhD6E%2FzuvTlJcaci4LkwUuJ%2FBvN1HtSQk10AmLUyP9gV5cVpAxgtdEtaFTdPlnG%2FB1sEY8sS2xp5PUnQpWzG7kPma77hE7ufzVYtOcnXAPDSYESTxg6vTsW1z1DzCnxqLUBjqkAZVJ%2F91o8fskEYkUgFbPnwoBc2nYkt9CwnP%2F2k1lx7EODv4sPYHG87AWaUYLlPz1VKM11KTrCn8zHbvdnKAwRAxda7kqIwn2lcqVuYULLOSlLc312DCRcQttBUxvJ7TeoMc7z0LXQfxKP9GrQWcOf9GsFIqb5Yrtk37LFR5aqLuM2hda0dxe6knUZcytxgBS2MuexZ6dT4A481SNqxMHsQHReny0&X-Amz-Signature=e8cadb733f1dc175471da32dff3e61497bec01e69d936e36031b0b0ae2d9d30a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/27352fc8-c398-41ec-8c1e-2e22915a1f30/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666MMDZONH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204458Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDamAEU%2BKKgo9Zc20jEvyayR%2FuHx1DKzMSt3T%2Bp2RSZNwIhAJwSvCj0IBB9mpuOttu5F8zrBpUpb%2BW6d19jHOtmwXTEKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwE4APlUlUGz5HqQOYq3ANMaRUvYhYVo2zkj1xWX9IDsNYnVS%2BP5ycJpRFi5tYzRmVv1UUcmWUdioqh87lxz0g%2B1QHU170oGYXy6sJ715vcBsoQwcQK9QDXUqCz%2BnnKvAi13Tqtp8eTM6zLq356l%2FKXUuNxeM%2Fnhr8CNL0OK%2FW1PnRSFUhKYPRYXC8tkwWvex%2B3NY4QS%2Fb3FmGnQgrk%2BsBK7uko6ZNMaJGIzLG9MF7Xhq%2Be%2FpjFmlBfg8f55jC1RVXmLy%2BPof3nPB3cXIi%2F%2BiS8WB5I0PRzy6HRduQCgTF6fOgi63XMi64yARqo9QSdWmuiG0G0AhI43jhZTzNNCkDwqzCqy3tTV4hm3857%2BNme%2FxMUNXpecPC9XbUf8PXlW4RRDnmD8dbfCZokObzNG8aN3gKkaSdJXq2jjU9ihH2ewaEQrAgI%2BrpKSsCuQnLUKoCTyQrBUi%2ByT2eaZJKqTx%2FX83bdwlBAXite85yfb%2BcFWXE00A26BQntSgyASeT%2BGDUXuxDNuqZDoWmA7foHcyYhD6E%2FzuvTlJcaci4LkwUuJ%2FBvN1HtSQk10AmLUyP9gV5cVpAxgtdEtaFTdPlnG%2FB1sEY8sS2xp5PUnQpWzG7kPma77hE7ufzVYtOcnXAPDSYESTxg6vTsW1z1DzCnxqLUBjqkAZVJ%2F91o8fskEYkUgFbPnwoBc2nYkt9CwnP%2F2k1lx7EODv4sPYHG87AWaUYLlPz1VKM11KTrCn8zHbvdnKAwRAxda7kqIwn2lcqVuYULLOSlLc312DCRcQttBUxvJ7TeoMc7z0LXQfxKP9GrQWcOf9GsFIqb5Yrtk37LFR5aqLuM2hda0dxe6knUZcytxgBS2MuexZ6dT4A481SNqxMHsQHReny0&X-Amz-Signature=187173b675ad784adf1cadee14286d4d2fd42e57f8bec0a12dd2c1d14a36875b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

## Common Login Problems

- **Predictable usernames**
- **Password that can be guessed**
- **Defects in logic**
# **Session Management**

- **Session: a set of data structures that track the state of the user**
- **A token identifies the session, usually a cookie**
  - **Can also use hidden form fields or the URL query string**
- **Sessions expire**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ce49d6b6-4c9e-4ba9-a46c-8611b124ddc7/image30.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SS5I4UJH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBbEs1rejctGcmGzJ7ct%2BXbas8oBQ6%2FQMtzL%2F5ddz2gOAiEAgdurQ1uHdXVbENd3RSxh6EIvRe0JshwjMFF24CyoGiAqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKoxphm4qUYWxbOl5SrcA5%2FsxK0p3IOn73gy46K0xrs%2F9g18PVHc3ffmXyeyLu6ocONlg1LHCAd%2B0rQw6eRxdjMbzbJQEFkTKOihnAwO30sNiJLQROQwrgGIJxbHmfOajyDwnlU59q2oVPrAuBdeYfdQIejhe5RI9z9rbjxeefkkZ%2FhYHaC68Dwxf3VwSyT%2BXJsmw44CkaCnh6pGx6oYNfbG6OjPS%2FvNeHyQswgi6mS1JgU5fUtQHDSxUbXlBONh%2FCeu3g1CPJ2kMPgjfx15jiHNWNwjgyEruh%2FuTwA4K%2F1wu9t3GyFkDjpYiLiSdbayW0aJfGbn7NEwsVPDJz9WHRAWBtB2qki8Pppwqrry%2FcPfMdCgwR01xTAgcHbqrzEkYhMlLvID7nKyiNxBwfVQ7PpVr7IvTEVDChLHH9Jjs72Y8R970sJnk1Tfv%2BH9xumm3sTEt6%2FUVyXRXkC8V36vdqfn%2FZSVpvb1nMntwOFo%2BxhhwgpY%2F0%2FvU0sevCHsTiW5O3YEAnbdne8ntQHZxeqSZiEBt%2FCQJIAahzc9x6KGUikw5kSW%2B1a2866Ao7UqObMAlMfC2o0ZV9zjgAE%2BZjAG2ujBmLaZCLkGCD2Sjhgt2dR8UuNc%2F8QvfPSCan592x1rAvLm36HXOdcAvrU%2BMLrJotQGOqUBjaPFEQBNvvTb%2FYeRj%2FsN52xTZgknQec%2F5gY3W9xZA0HAfY24wgSdPUpIUp%2Bbu%2BvW7qibLZofNrI9KgajxUYxjQ%2BRzXoS4Jj4mCoIoROGFLNdpzl3Apt8qVBNnjkFsaFKAUYyCDIFk9HJPt9Caq5sq1B6gNHb3%2BJhrQFyAvm77M6oFSsGjXpI%2FPgBYtOL1QqmD4e7mElu7rOJVkaF%2F0YdG1zQ%2BrKs&X-Amz-Signature=a984a0a05f3898fcf0fa41494066e4fa834a8227a60adf5f39d08ee607e398e4&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Common Session Problems

- **Tokens are predictable (not random)**
- **Tokens poorly handled, so an attacker can capture another user's token**
### Access Control

- **Each request must be permitted or denied**
- **Multiple roles within application**
- **Frequent logic errors and flawed assumptions**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e68c2bc6-4d70-4060-ac8e-b56958dffdd8/image31.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SS5I4UJH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBbEs1rejctGcmGzJ7ct%2BXbas8oBQ6%2FQMtzL%2F5ddz2gOAiEAgdurQ1uHdXVbENd3RSxh6EIvRe0JshwjMFF24CyoGiAqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKoxphm4qUYWxbOl5SrcA5%2FsxK0p3IOn73gy46K0xrs%2F9g18PVHc3ffmXyeyLu6ocONlg1LHCAd%2B0rQw6eRxdjMbzbJQEFkTKOihnAwO30sNiJLQROQwrgGIJxbHmfOajyDwnlU59q2oVPrAuBdeYfdQIejhe5RI9z9rbjxeefkkZ%2FhYHaC68Dwxf3VwSyT%2BXJsmw44CkaCnh6pGx6oYNfbG6OjPS%2FvNeHyQswgi6mS1JgU5fUtQHDSxUbXlBONh%2FCeu3g1CPJ2kMPgjfx15jiHNWNwjgyEruh%2FuTwA4K%2F1wu9t3GyFkDjpYiLiSdbayW0aJfGbn7NEwsVPDJz9WHRAWBtB2qki8Pppwqrry%2FcPfMdCgwR01xTAgcHbqrzEkYhMlLvID7nKyiNxBwfVQ7PpVr7IvTEVDChLHH9Jjs72Y8R970sJnk1Tfv%2BH9xumm3sTEt6%2FUVyXRXkC8V36vdqfn%2FZSVpvb1nMntwOFo%2BxhhwgpY%2F0%2FvU0sevCHsTiW5O3YEAnbdne8ntQHZxeqSZiEBt%2FCQJIAahzc9x6KGUikw5kSW%2B1a2866Ao7UqObMAlMfC2o0ZV9zjgAE%2BZjAG2ujBmLaZCLkGCD2Sjhgt2dR8UuNc%2F8QvfPSCan592x1rAvLm36HXOdcAvrU%2BMLrJotQGOqUBjaPFEQBNvvTb%2FYeRj%2FsN52xTZgknQec%2F5gY3W9xZA0HAfY24wgSdPUpIUp%2Bbu%2BvW7qibLZofNrI9KgajxUYxjQ%2BRzXoS4Jj4mCoIoROGFLNdpzl3Apt8qVBNnjkFsaFKAUYyCDIFk9HJPt9Caq5sq1B6gNHb3%2BJhrQFyAvm77M6oFSsGjXpI%2FPgBYtOL1QqmD4e7mElu7rOJVkaF%2F0YdG1zQ%2BrKs&X-Amz-Signature=799c99d6dd0d8741908a17a90ec28f42e4bc18e9b8510a9548786d8468c955f9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

# **Handling User Input**

- **"Input Validation" is the most common solution**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e8292331-5fd1-422f-bfda-b805ada91fc3/image32.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SS5I4UJH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBbEs1rejctGcmGzJ7ct%2BXbas8oBQ6%2FQMtzL%2F5ddz2gOAiEAgdurQ1uHdXVbENd3RSxh6EIvRe0JshwjMFF24CyoGiAqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKoxphm4qUYWxbOl5SrcA5%2FsxK0p3IOn73gy46K0xrs%2F9g18PVHc3ffmXyeyLu6ocONlg1LHCAd%2B0rQw6eRxdjMbzbJQEFkTKOihnAwO30sNiJLQROQwrgGIJxbHmfOajyDwnlU59q2oVPrAuBdeYfdQIejhe5RI9z9rbjxeefkkZ%2FhYHaC68Dwxf3VwSyT%2BXJsmw44CkaCnh6pGx6oYNfbG6OjPS%2FvNeHyQswgi6mS1JgU5fUtQHDSxUbXlBONh%2FCeu3g1CPJ2kMPgjfx15jiHNWNwjgyEruh%2FuTwA4K%2F1wu9t3GyFkDjpYiLiSdbayW0aJfGbn7NEwsVPDJz9WHRAWBtB2qki8Pppwqrry%2FcPfMdCgwR01xTAgcHbqrzEkYhMlLvID7nKyiNxBwfVQ7PpVr7IvTEVDChLHH9Jjs72Y8R970sJnk1Tfv%2BH9xumm3sTEt6%2FUVyXRXkC8V36vdqfn%2FZSVpvb1nMntwOFo%2BxhhwgpY%2F0%2FvU0sevCHsTiW5O3YEAnbdne8ntQHZxeqSZiEBt%2FCQJIAahzc9x6KGUikw5kSW%2B1a2866Ao7UqObMAlMfC2o0ZV9zjgAE%2BZjAG2ujBmLaZCLkGCD2Sjhgt2dR8UuNc%2F8QvfPSCan592x1rAvLm36HXOdcAvrU%2BMLrJotQGOqUBjaPFEQBNvvTb%2FYeRj%2FsN52xTZgknQec%2F5gY3W9xZA0HAfY24wgSdPUpIUp%2Bbu%2BvW7qibLZofNrI9KgajxUYxjQ%2BRzXoS4Jj4mCoIoROGFLNdpzl3Apt8qVBNnjkFsaFKAUYyCDIFk9HJPt9Caq5sq1B6gNHb3%2BJhrQFyAvm77M6oFSsGjXpI%2FPgBYtOL1QqmD4e7mElu7rOJVkaF%2F0YdG1zQ%2BrKs&X-Amz-Signature=589bb9971fc3c5c5dbf71ed84e38028152505608f9870b1f8535c6f5f2174ba4&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0be217f7-f659-4558-9619-18c04191a44e/image33.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SS5I4UJH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBbEs1rejctGcmGzJ7ct%2BXbas8oBQ6%2FQMtzL%2F5ddz2gOAiEAgdurQ1uHdXVbENd3RSxh6EIvRe0JshwjMFF24CyoGiAqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKoxphm4qUYWxbOl5SrcA5%2FsxK0p3IOn73gy46K0xrs%2F9g18PVHc3ffmXyeyLu6ocONlg1LHCAd%2B0rQw6eRxdjMbzbJQEFkTKOihnAwO30sNiJLQROQwrgGIJxbHmfOajyDwnlU59q2oVPrAuBdeYfdQIejhe5RI9z9rbjxeefkkZ%2FhYHaC68Dwxf3VwSyT%2BXJsmw44CkaCnh6pGx6oYNfbG6OjPS%2FvNeHyQswgi6mS1JgU5fUtQHDSxUbXlBONh%2FCeu3g1CPJ2kMPgjfx15jiHNWNwjgyEruh%2FuTwA4K%2F1wu9t3GyFkDjpYiLiSdbayW0aJfGbn7NEwsVPDJz9WHRAWBtB2qki8Pppwqrry%2FcPfMdCgwR01xTAgcHbqrzEkYhMlLvID7nKyiNxBwfVQ7PpVr7IvTEVDChLHH9Jjs72Y8R970sJnk1Tfv%2BH9xumm3sTEt6%2FUVyXRXkC8V36vdqfn%2FZSVpvb1nMntwOFo%2BxhhwgpY%2F0%2FvU0sevCHsTiW5O3YEAnbdne8ntQHZxeqSZiEBt%2FCQJIAahzc9x6KGUikw5kSW%2B1a2866Ao7UqObMAlMfC2o0ZV9zjgAE%2BZjAG2ujBmLaZCLkGCD2Sjhgt2dR8UuNc%2F8QvfPSCan592x1rAvLm36HXOdcAvrU%2BMLrJotQGOqUBjaPFEQBNvvTb%2FYeRj%2FsN52xTZgknQec%2F5gY3W9xZA0HAfY24wgSdPUpIUp%2Bbu%2BvW7qibLZofNrI9KgajxUYxjQ%2BRzXoS4Jj4mCoIoROGFLNdpzl3Apt8qVBNnjkFsaFKAUYyCDIFk9HJPt9Caq5sq1B6gNHb3%2BJhrQFyAvm77M6oFSsGjXpI%2FPgBYtOL1QqmD4e7mElu7rOJVkaF%2F0YdG1zQ%2BrKs&X-Amz-Signature=b2f22ece53057fe65e861a156e29745599e2a24f4c3e431e8c1e950ac8f95bb8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3455a3ee-c990-4c53-95f9-9bcb815cf625/image34.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SS5I4UJH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBbEs1rejctGcmGzJ7ct%2BXbas8oBQ6%2FQMtzL%2F5ddz2gOAiEAgdurQ1uHdXVbENd3RSxh6EIvRe0JshwjMFF24CyoGiAqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKoxphm4qUYWxbOl5SrcA5%2FsxK0p3IOn73gy46K0xrs%2F9g18PVHc3ffmXyeyLu6ocONlg1LHCAd%2B0rQw6eRxdjMbzbJQEFkTKOihnAwO30sNiJLQROQwrgGIJxbHmfOajyDwnlU59q2oVPrAuBdeYfdQIejhe5RI9z9rbjxeefkkZ%2FhYHaC68Dwxf3VwSyT%2BXJsmw44CkaCnh6pGx6oYNfbG6OjPS%2FvNeHyQswgi6mS1JgU5fUtQHDSxUbXlBONh%2FCeu3g1CPJ2kMPgjfx15jiHNWNwjgyEruh%2FuTwA4K%2F1wu9t3GyFkDjpYiLiSdbayW0aJfGbn7NEwsVPDJz9WHRAWBtB2qki8Pppwqrry%2FcPfMdCgwR01xTAgcHbqrzEkYhMlLvID7nKyiNxBwfVQ7PpVr7IvTEVDChLHH9Jjs72Y8R970sJnk1Tfv%2BH9xumm3sTEt6%2FUVyXRXkC8V36vdqfn%2FZSVpvb1nMntwOFo%2BxhhwgpY%2F0%2FvU0sevCHsTiW5O3YEAnbdne8ntQHZxeqSZiEBt%2FCQJIAahzc9x6KGUikw5kSW%2B1a2866Ao7UqObMAlMfC2o0ZV9zjgAE%2BZjAG2ujBmLaZCLkGCD2Sjhgt2dR8UuNc%2F8QvfPSCan592x1rAvLm36HXOdcAvrU%2BMLrJotQGOqUBjaPFEQBNvvTb%2FYeRj%2FsN52xTZgknQec%2F5gY3W9xZA0HAfY24wgSdPUpIUp%2Bbu%2BvW7qibLZofNrI9KgajxUYxjQ%2BRzXoS4Jj4mCoIoROGFLNdpzl3Apt8qVBNnjkFsaFKAUYyCDIFk9HJPt9Caq5sq1B6gNHb3%2BJhrQFyAvm77M6oFSsGjXpI%2FPgBYtOL1QqmD4e7mElu7rOJVkaF%2F0YdG1zQ%2BrKs&X-Amz-Signature=1c2299db1c0e576f5753201d066a64e7a590a5c40d44974fabd170baa7b03d46&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/20ab29ba-ef80-4a1c-aaf5-e7ffc8ff33b9/image35.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SS5I4UJH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBbEs1rejctGcmGzJ7ct%2BXbas8oBQ6%2FQMtzL%2F5ddz2gOAiEAgdurQ1uHdXVbENd3RSxh6EIvRe0JshwjMFF24CyoGiAqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKoxphm4qUYWxbOl5SrcA5%2FsxK0p3IOn73gy46K0xrs%2F9g18PVHc3ffmXyeyLu6ocONlg1LHCAd%2B0rQw6eRxdjMbzbJQEFkTKOihnAwO30sNiJLQROQwrgGIJxbHmfOajyDwnlU59q2oVPrAuBdeYfdQIejhe5RI9z9rbjxeefkkZ%2FhYHaC68Dwxf3VwSyT%2BXJsmw44CkaCnh6pGx6oYNfbG6OjPS%2FvNeHyQswgi6mS1JgU5fUtQHDSxUbXlBONh%2FCeu3g1CPJ2kMPgjfx15jiHNWNwjgyEruh%2FuTwA4K%2F1wu9t3GyFkDjpYiLiSdbayW0aJfGbn7NEwsVPDJz9WHRAWBtB2qki8Pppwqrry%2FcPfMdCgwR01xTAgcHbqrzEkYhMlLvID7nKyiNxBwfVQ7PpVr7IvTEVDChLHH9Jjs72Y8R970sJnk1Tfv%2BH9xumm3sTEt6%2FUVyXRXkC8V36vdqfn%2FZSVpvb1nMntwOFo%2BxhhwgpY%2F0%2FvU0sevCHsTiW5O3YEAnbdne8ntQHZxeqSZiEBt%2FCQJIAahzc9x6KGUikw5kSW%2B1a2866Ao7UqObMAlMfC2o0ZV9zjgAE%2BZjAG2ujBmLaZCLkGCD2Sjhgt2dR8UuNc%2F8QvfPSCan592x1rAvLm36HXOdcAvrU%2BMLrJotQGOqUBjaPFEQBNvvTb%2FYeRj%2FsN52xTZgknQec%2F5gY3W9xZA0HAfY24wgSdPUpIUp%2Bbu%2BvW7qibLZofNrI9KgajxUYxjQ%2BRzXoS4Jj4mCoIoROGFLNdpzl3Apt8qVBNnjkFsaFKAUYyCDIFk9HJPt9Caq5sq1B6gNHb3%2BJhrQFyAvm77M6oFSsGjXpI%2FPgBYtOL1QqmD4e7mElu7rOJVkaF%2F0YdG1zQ%2BrKs&X-Amz-Signature=ded45f43206a37eed61ff10141b78c47172f450e353d8887961c8746cb3ec999&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d0a08c80-f41b-45af-b103-2e24622ecdb3/image36.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SS5I4UJH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBbEs1rejctGcmGzJ7ct%2BXbas8oBQ6%2FQMtzL%2F5ddz2gOAiEAgdurQ1uHdXVbENd3RSxh6EIvRe0JshwjMFF24CyoGiAqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKoxphm4qUYWxbOl5SrcA5%2FsxK0p3IOn73gy46K0xrs%2F9g18PVHc3ffmXyeyLu6ocONlg1LHCAd%2B0rQw6eRxdjMbzbJQEFkTKOihnAwO30sNiJLQROQwrgGIJxbHmfOajyDwnlU59q2oVPrAuBdeYfdQIejhe5RI9z9rbjxeefkkZ%2FhYHaC68Dwxf3VwSyT%2BXJsmw44CkaCnh6pGx6oYNfbG6OjPS%2FvNeHyQswgi6mS1JgU5fUtQHDSxUbXlBONh%2FCeu3g1CPJ2kMPgjfx15jiHNWNwjgyEruh%2FuTwA4K%2F1wu9t3GyFkDjpYiLiSdbayW0aJfGbn7NEwsVPDJz9WHRAWBtB2qki8Pppwqrry%2FcPfMdCgwR01xTAgcHbqrzEkYhMlLvID7nKyiNxBwfVQ7PpVr7IvTEVDChLHH9Jjs72Y8R970sJnk1Tfv%2BH9xumm3sTEt6%2FUVyXRXkC8V36vdqfn%2FZSVpvb1nMntwOFo%2BxhhwgpY%2F0%2FvU0sevCHsTiW5O3YEAnbdne8ntQHZxeqSZiEBt%2FCQJIAahzc9x6KGUikw5kSW%2B1a2866Ao7UqObMAlMfC2o0ZV9zjgAE%2BZjAG2ujBmLaZCLkGCD2Sjhgt2dR8UuNc%2F8QvfPSCan592x1rAvLm36HXOdcAvrU%2BMLrJotQGOqUBjaPFEQBNvvTb%2FYeRj%2FsN52xTZgknQec%2F5gY3W9xZA0HAfY24wgSdPUpIUp%2Bbu%2BvW7qibLZofNrI9KgajxUYxjQ%2BRzXoS4Jj4mCoIoROGFLNdpzl3Apt8qVBNnjkFsaFKAUYyCDIFk9HJPt9Caq5sq1B6gNHb3%2BJhrQFyAvm77M6oFSsGjXpI%2FPgBYtOL1QqmD4e7mElu7rOJVkaF%2F0YdG1zQ%2BrKs&X-Amz-Signature=bf3f2a20fb7499999c213e77bc2f4333de1bdc7f10c04290c0dd760980bd0774&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> Example SOAP Request

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d54353c7-1ad1-49d6-b966-0e7fc105182e/image37.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SS5I4UJH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBbEs1rejctGcmGzJ7ct%2BXbas8oBQ6%2FQMtzL%2F5ddz2gOAiEAgdurQ1uHdXVbENd3RSxh6EIvRe0JshwjMFF24CyoGiAqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKoxphm4qUYWxbOl5SrcA5%2FsxK0p3IOn73gy46K0xrs%2F9g18PVHc3ffmXyeyLu6ocONlg1LHCAd%2B0rQw6eRxdjMbzbJQEFkTKOihnAwO30sNiJLQROQwrgGIJxbHmfOajyDwnlU59q2oVPrAuBdeYfdQIejhe5RI9z9rbjxeefkkZ%2FhYHaC68Dwxf3VwSyT%2BXJsmw44CkaCnh6pGx6oYNfbG6OjPS%2FvNeHyQswgi6mS1JgU5fUtQHDSxUbXlBONh%2FCeu3g1CPJ2kMPgjfx15jiHNWNwjgyEruh%2FuTwA4K%2F1wu9t3GyFkDjpYiLiSdbayW0aJfGbn7NEwsVPDJz9WHRAWBtB2qki8Pppwqrry%2FcPfMdCgwR01xTAgcHbqrzEkYhMlLvID7nKyiNxBwfVQ7PpVr7IvTEVDChLHH9Jjs72Y8R970sJnk1Tfv%2BH9xumm3sTEt6%2FUVyXRXkC8V36vdqfn%2FZSVpvb1nMntwOFo%2BxhhwgpY%2F0%2FvU0sevCHsTiW5O3YEAnbdne8ntQHZxeqSZiEBt%2FCQJIAahzc9x6KGUikw5kSW%2B1a2866Ao7UqObMAlMfC2o0ZV9zjgAE%2BZjAG2ujBmLaZCLkGCD2Sjhgt2dR8UuNc%2F8QvfPSCan592x1rAvLm36HXOdcAvrU%2BMLrJotQGOqUBjaPFEQBNvvTb%2FYeRj%2FsN52xTZgknQec%2F5gY3W9xZA0HAfY24wgSdPUpIUp%2Bbu%2BvW7qibLZofNrI9KgajxUYxjQ%2BRzXoS4Jj4mCoIoROGFLNdpzl3Apt8qVBNnjkFsaFKAUYyCDIFk9HJPt9Caq5sq1B6gNHb3%2BJhrQFyAvm77M6oFSsGjXpI%2FPgBYtOL1QqmD4e7mElu7rOJVkaF%2F0YdG1zQ%2BrKs&X-Amz-Signature=6159f9d3b86117c495f66c4cc31b7d278a4c471de4b7abc569e645a216465c48&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/6427d727-990b-4736-a734-c33cdacf0bbd/image38.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SS5I4UJH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBbEs1rejctGcmGzJ7ct%2BXbas8oBQ6%2FQMtzL%2F5ddz2gOAiEAgdurQ1uHdXVbENd3RSxh6EIvRe0JshwjMFF24CyoGiAqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKoxphm4qUYWxbOl5SrcA5%2FsxK0p3IOn73gy46K0xrs%2F9g18PVHc3ffmXyeyLu6ocONlg1LHCAd%2B0rQw6eRxdjMbzbJQEFkTKOihnAwO30sNiJLQROQwrgGIJxbHmfOajyDwnlU59q2oVPrAuBdeYfdQIejhe5RI9z9rbjxeefkkZ%2FhYHaC68Dwxf3VwSyT%2BXJsmw44CkaCnh6pGx6oYNfbG6OjPS%2FvNeHyQswgi6mS1JgU5fUtQHDSxUbXlBONh%2FCeu3g1CPJ2kMPgjfx15jiHNWNwjgyEruh%2FuTwA4K%2F1wu9t3GyFkDjpYiLiSdbayW0aJfGbn7NEwsVPDJz9WHRAWBtB2qki8Pppwqrry%2FcPfMdCgwR01xTAgcHbqrzEkYhMlLvID7nKyiNxBwfVQ7PpVr7IvTEVDChLHH9Jjs72Y8R970sJnk1Tfv%2BH9xumm3sTEt6%2FUVyXRXkC8V36vdqfn%2FZSVpvb1nMntwOFo%2BxhhwgpY%2F0%2FvU0sevCHsTiW5O3YEAnbdne8ntQHZxeqSZiEBt%2FCQJIAahzc9x6KGUikw5kSW%2B1a2866Ao7UqObMAlMfC2o0ZV9zjgAE%2BZjAG2ujBmLaZCLkGCD2Sjhgt2dR8UuNc%2F8QvfPSCan592x1rAvLm36HXOdcAvrU%2BMLrJotQGOqUBjaPFEQBNvvTb%2FYeRj%2FsN52xTZgknQec%2F5gY3W9xZA0HAfY24wgSdPUpIUp%2Bbu%2BvW7qibLZofNrI9KgajxUYxjQ%2BRzXoS4Jj4mCoIoROGFLNdpzl3Apt8qVBNnjkFsaFKAUYyCDIFk9HJPt9Caq5sq1B6gNHb3%2BJhrQFyAvm77M6oFSsGjXpI%2FPgBYtOL1QqmD4e7mElu7rOJVkaF%2F0YdG1zQ%2BrKs&X-Amz-Signature=916c11aa179e673a9eeb1db855c686d9babad31d0d8d7cbdeb13e9e961ead1be&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ce5c8c3e-7e63-487a-8d3f-b7ce1eaa22fe/image39.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WJ6DMHRN%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204510Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDbAhmc4Oz7oaS2HTjnbtfpJakcyAvOqSp8ClwPvlTlSAiBP%2Finu3Gn5%2FP2rkMPBboMb1rlIeBVDY593LVO4mo11OiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMmLdo2WGfG7e0aKXeKtwDhKQOb4h%2FgCH79so1FXy7N%2B0xRsip4r2HXL5wgiEgVh0uUW3Lvq%2F0eCIEeZHuwz9ZOBPxhadawh0xWVw8PRXMAxA2iF%2FdYYTfveb7F%2BXCAH2eWP4Hvp2hrc3FotwduVDXQq5kl2Zy5e7CgETaQkvy%2FzSIgXqMQKlKTcJokpjDxUmFCsJuNboGClxGBLf1dh4rQRi535u8DTCvhRhwd8Sadckp6cNMdjRPHoLkbaB9caz4AM6tBZaFxJOIiNzhDj5yxtImw5vhXCHvzgmNx%2FAyfjQaCZQX74LBGxRhc6kYPc%2FAuwiHCLPZo65%2BETEilNGMqg6BDfe4fADOETGudLDOkiys6Y9uJDBWOHVqUfQwWFcnxQGXl6ibtOa1yBiK4ZyHXNVyfnJNpjd0k3FvjJTmMoUNS2DEJtkqOErHlSAVg35W1bNfRrOTyVbmaM5F7ZAj%2BXeMS%2BVwS26Q%2Blb1440u1CPhplCU8eMCrk9uzhvQod1txiZUv5Z5dN8HPfT%2BHokzLIdloF5IFXVaxhpQP%2FlLTWIUlL4KYbjgGTOBevBt9TCcp1RNCA27fM65y0d9Zj42qc1yeUFDXGqTamcE%2Fb5xelCioeMcTZCn%2FCm33aageOTDYjMu1xCMGlFDy2ww6cii1AY6pgGwLwEqC4oVrEOOxcyg31WFbgegQ6GTDSPnnI1KTARwGrzR7tLVyNq%2FZHwBIFbH0C5KtUWUtdv%2B5VuHPcxNJqOwhS0Joxfdtm3n%2FKXTogf6%2BBtE7Dhl30VLyNJLfsGwqGSmCnSbzRlIoB2e9MlQI5FwM08uXEqWKje2ucLNf9NJdk0H6BkaPfynokH5jb5KgDSV0HYRW5lBXLKI64A4AN77U156tNTZ&X-Amz-Signature=1b406bde851244b4d41d5b244ac271b79d2da7549ac9bfca6bba14fdc32cdd25&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### **Attacking the Administration Panel**

- **Defeat weak authentication**
- **Some administrative functions might not require high privileges**
- **XSS flaws can allow cookie theft and session hijacking**