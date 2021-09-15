+++
menuTitle = "Apply MFA for Root Account"
title = "Apply MFA for Root Account"
date = 2020-07-30T14:27:19-05:00
weight = 12
+++

### Apply MFA for Root Account
1. Use your AWS account email address and password to sign in as the AWS account root user to the IAM console at https://console.aws.amazon.com/iam/ 
2. On the right side of the navigation bar, click your account name, and click My Security Credentials. If necessary, click Continue to Security Credentials. 
3. Then expand the Multi-Factor Authentication (MFA) section on the page.
    
![Click on your account](/images/Module-2-Image-1.png)

![Multi-Factor Authentication](/images/Module-2-Image-2.png)

4. Click *Activate MFA*.
5. In the wizard, click *virtual MFA* device and then click *Continue*.

![Click virtual MFA](/images/Module-2-Image-3.png)

6. On the 'set up virtual MFA device window' click Show QR code.

7. With the Manage MFA Device wizard still open, open the virtual MFA app on the device.
    * If the virtual MFA software supports multiple accounts (multiple virtual MFA devices), then click the option to create a new account (a new virtual device).
    * The easiest way to configure the app is to use the app to scan the QR code. If you cannot scan the code, you can type the configuration information manually.
    
8. To use the QR code to configure the virtual MFA device, follow the app instructions for scanning the code. For example, you might need to tap the camera icon or tap a command like Scan account barcode, and then use the device's camera to scan the QR code.

9. If you cannot scan the code, type the configuration information manually by typing the Secret Configuration Key value into the app. For example, to do this in the Virtual MFA app, click Manually add account, and then type the secret configuration key and click Create.

10. The device starts generating six-digit numbers.

11. In the Manage MFA Device wizard, in the MFA Code 1 box, type the six-digit number that’s currently displayed by the MFA device. Wait up to 30 seconds for the device to generate a new number, and then type the new six-digit number into the Authentication Code 2 box.

12. Important: Submit your request immediately after generating the codes. If you generate the codes and then wait too long to submit the request, the MFA device successfully associates with the user but the MFA device is out of sync. This happens because time-based one-time passwords (TOTP) expire after a short period of time. If this happens, you can resync the device.

13. Click Assign MFA, and then click Finish. Note the 'success' confirmation and click Close.

For more information please read the [AWS User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html)