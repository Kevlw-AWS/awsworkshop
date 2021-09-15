+++
title = "2. Use MFA"
date = 2019-11-18T08:23:04+11:00
weight = 28
+++

MFA is the best way to protect accounts from inappropriate access. Always set up MFA on your Root user and AWS Identity and Access Management (IAM) users. If you use [AWS Single Sign-On (SSO)](https://aws.amazon.com/single-sign-on/) to control access to AWS or to federate your corporate identity store, you can enforce MFA there. Implementing MFA at the federated identity provider (IdP) means that you can take advantage of existing MFA processes in your organization. 

In this exercise we will use AWS Identity & Access Management (IAM) in the AWS Management Console to configure and enable a virtual multi factor authentication (MFA) device for both the *root account* as well as *IAM users*. 

Please note: To manage MFA devices for the AWS account, you must be signed in to AWS using your root user credentials. You cannot manage MFA devices for the root user using other credentials.

### Steps - Apply MFA for Root Account
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