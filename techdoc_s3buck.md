
# Vulnerable S3 Bucket - Red Teaming

 ![App Screenshot](https://drive.google.com/uc?export=view&id=1uSG8jeENF6hlHk_NIquqs4UNQrFdx7_M)


Amazon S3 (Simple Storage Service) is a popular cloud-based storage service used by many individuals and organizations to store and retrieve data. However, if an S3 bucket is misconfigured, it can become vulnerable to exploitation, potentially leading to data breaches and other security incidents.

One common misconfiguration that makes S3 buckets vulnerable is leaving them publicly accessible with no security rules in place. In this case, anyone with the S3 bucket URL can access and download the data stored within it, which could include sensitive or confidential information such as personal identifiable information (PII), financial data, or trade secrets.

Hackers can exploit this vulnerability by simply running a web crawler or automated tool to search for S3 buckets with open access. They can then use this information to access the data, potentially causing significant harm to individuals or organizations.

It's important to note that S3 bucket misconfigurations are not always obvious, and sometimes occur due to human error or a lack of understanding of S3 bucket security features. Therefore, it's crucial for individuals and organizations to review their S3 bucket configurations regularly and ensure they have appropriate security rules in place to prevent unauthorized access.

In conclusion, the exploitation of an S3 bucket misconfiguration can be very easy if it was left publicly accessible with no security rules in place. Therefore, it's important for individuals and organizations to be aware of the potential risks and take appropriate steps to secure their S3 buckets.

To demonstrate Vulnerable S3 Bucket:

For domain and bucket discovery of a site: type nslookup <sitename>

nslookup flaws.cloud
  
![App Screenshot](https://drive.google.com/uc?export=view&id=1BVRVQ6qhRjdTM5wtDdQuYGtsuZkX5Yn7)


host flaws.cloud
  
![App Screenshot](https://drive.google.com/uc?export=view&id=1Hofov-ZiaDDwiSNh9srE1rpQNVhv2w2j)


To do a reverse lookup: type host <ipaddress>

This query shows that this website is in S3 and it’s in the us-west-2 region.
  
![App Screenshot](https://drive.google.com/uc?export=view&id=1BK7Y5ZQa0yWDApfODoRZB1TyMqQ3ubkD)


There is a common naming format to find out how S3 websites are. To check if this is a website in S3, type the domain + s3.amazonaws.com on a browser: 
http://flaws.cloud.s3.amazonaws.com

  
![App Screenshot](https://drive.google.com/uc?export=view&id=1_EUuiDCxxDw-PLgcsMnUgZ1Bnr8jn7nO)


First, install AWS CLI on Ubuntu or Linux, follow instruction here to install it: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

To do basic enumeration on S3 bucket:
aws s3 ls s3://flaws.cloud/ --region us-west-2

![App Screenshot](https://drive.google.com/uc?export=view&id=1L6eDRP1LPnIL-EbGSdBoVhd3IKJ9vjTh)


This error means, there’s no credentials and I’m not authenticated so I don’t have any access to this bucket. 

There is a work around to specify “no sign request” which basically means not to sign the request or look for credentials. That means I can anonymously access the S3 bucket.

To enumerate with no credentials:
aws s3 ls s3://flaws.cloud/ --region us-west-2 --no-sign-request

![App Screenshot](https://drive.google.com/uc?export=view&id=1Z9UK97oVHBl_KizkVHTXHbUIxJLMVF41)


Now, I’m able to list the content of the bucket without any credentials. I will view the “secret-dd02c7c.html” on a browser. 

Type the S3 bucket URL: http://flaws.cloud.s3.amazonaws.com/secret-dd02c7c.html

![App Screenshot](https://drive.google.com/uc?export=view&id=1moMD7WG-4mzn70KxRa-zQP2HWjmhnwwW)


I also created a “testing.txt” and saved it that means, I was able to hack into it.
  

![App Screenshot](https://drive.google.com/uc?export=view&id=1Dx4DtG_YIqJSBwcbkfQixDkTleT8QUh7)


References:

- Install AWS CLI: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
- Flaws.com https://www.youtube.com/watch?v=fEjAryrzLSQ
