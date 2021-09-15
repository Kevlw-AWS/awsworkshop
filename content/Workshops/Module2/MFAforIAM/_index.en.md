+++
menuTitle = "Apply MFA for IAM Users"
title = "Apply MFA for IAM Users"
date = 2020-07-30T14:27:19-05:00
weight = 13
+++

### Steps - Apply MFA for IAM Users
Use your AWS account email address and password to sign in as an IAM Admin user to the IAM console at https://console.aws.amazon.com/iam/ 

#### For existing users on AWS: 
1. Select *Users* on the left hand side of the Window. You should be able to see whether MFA has been applied on the users within your AWS accounts. 

![Select Users](/images/Module-2-Image-4.png)

2. Select a *user* that does not have MFA applied

![Select a user](/images/Module-2-Image-5.png)

3. Select *Security Credentials*

![Select Security Credentials](/images/Module-2-Image-6.png)

4. Click on *Manage* for Assigned MFA Device. 

![Select Security Credentials](/images/Module-2-Image-7.png)

5. In the wizard, click *virtual MFA* device and then click *Continue*.
6. On the 'set up virtual MFA device window' click Show QR code.

![Select Security Credentials](/images/Module-2-Image-8.png)

7.  With the Manage MFA Device wizard still open, open the virtual MFA app on the device. If the virtual MFA software supports multiple accounts (multiple virtual MFA devices), then click the option to create a new account (a new virtual device).

8. The easiest way to configure the app is to use the app to scan the QR code. If you cannot scan the code, you can type the configuration information manually.

9. To use the QR code to configure the virtual MFA device, follow the app instructions for scanning the code. For example, you might need to tap the camera icon or tap a command like Scan account barcode, and then use the device's camera to scan the QR code.

10. If you cannot scan the code, type the configuration information manually by typing the Secret Configuration Key value into the app. For example, to do this in the Virtual MFA app, click Manually add account, and then type the secret configuration key and click Create.

11. The device starts generating six-digit numbers.

12. In the Manage MFA Device wizard, in the MFA Code 1 box, type the six-digit number that’s currently displayed by the MFA device. Wait up to 30 seconds for the device to generate a new number, and then type the new six-digit number into the Authentication Code 2 box.

13. Important: Submit your request immediately after generating the codes. If you generate the codes and then wait too long to submit the request, the MFA device successfully associates with the user but the MFA device is out of sync. This happens because time-based one-time passwords (TOTP) expire after a short period of time. If this happens, you can resync the device.

14. Click Assign MFA, and then click Finish. Note the 'success' confirmation and click Close.

For more information please read the [AWS User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html)