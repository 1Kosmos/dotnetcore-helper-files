# dotnetcore-helper-files

## Prerequisites

- ** Visual Studio **: 2017 or higher
- **.NET Core **:  3.1 or higher


## Clone the **latest version** of the [.NET CORE SDK](https://github.com/1Kosmos/dotnetcore-helper-files) repo from our [github](https://github.com/1Kosmos) and performs the below steps. 

	a) Clone the main repository git clone https://github.com/1Kosmos/dotnetcore-helper-files.git. Clone of main repository will not pull the submodules. You need to execute step 'b' and 'c' as well.

	```shell 
	git clone https://github.com/1Kosmos/dotnetcore-helper-files.git
	```

	b) To initialize a Git submodule, use the “git submodule update” command with the “–init” and the “–recursive” options. This command will register the git submodule directory path for 'shared' folder.

    	```shell 
	git submodule update --init --recursive
	```

	c) In order to update an existing Git submodule, you need to execute the “git submodule update” with the “–remote” and the “–merge” option.

    	```shell 
	git submodule update --remote --merge
	```
	
- Navigate to the `dotnetcore-helper-files` folder and open the project solution in Visual Studio (double-click `BIDHelpers.sln`)
- Build the solution:- **Select the project -> right-click -> Build**  

After a successful build, `BIDHelpers.1.0.0.nupkg` will be generated in `BIDHelpers/bin/Debug`  


#### Install BIDHelpers nuget package into your Project

In your project directory, copy and paste `BIDHelpers.1.0.0.nupkg` file into your desired location. 

- Add path for above nuget package into your project, Go to solution explorer and perform the following steps:  
  - Right click on **Project -> Manage Nuget Packages -> Click on the Settings icon (beside os the Package Source dropdown)**
  - Options window will open up, click on **Add Package (Plus Icon in green)** -> Add appropriate **Name and Source (Path to the BIDHelpers.1.0.0.nupkg above into your project)** -> After adding Name and Source, Click on **OK** button.
  - After adding this, select the newly added **package name under the Package Source dropdown**, you will see the **BIDHelper** package.
 
Now you should be able to see **BIDHelper nuget package** ready to install into your project.


## How to use dotnetcore BIDHelpers package into your project

Add namespace on the top of the your page:
```
using BIDHelpers.BIDECDSA;

```

## To generate public and private key pair

Copy and past below line:

```
 var keyPair = BIDECDSA.GenerateKeyPair();

```

## To create shared key from public and private key pair

Copy and past below line:

```
 var sharedKey = BIDECDSA.CreateSharedKey(keyPair.prKey, keyPair.pKey);

```

## To encrypt the string using the shared key

Copy and past below line:

```
 var encryptedBase64String = BIDECDSA.Encrypt("any string", sharedKey);

```

## To decrypt the string using the shared key

Copy and past below line:

```
var decryptedPlainString = BIDECDSA.Decrypt(encryptedBase64String, sharedKey);

```

## To get community info and sd (Service Directory)

Add namespace on the top of the your page:

```
using BIDHelpers.BIDTenant;
using BIDHelpers.BIDTenant.Model;

```

- To get Community Information
Copy and past below line:

```
BIDTenantInfo bidTenantInfo = new BIDTenantInfo("<dns>", "<communityName>", "<licenseKey>");
BIDCommunityInfo communityInfo = BIDTenant.GetCommunityInfo(bidTenantInfo);

```

- To get SD (Service Directory) Information
Copy and past below line:

```
BIDTenantInfo bidTenantInfo = new BIDTenantInfo("<dns>", "<communityName>", "<licenseKey>");
BIDSD sd = BIDTenant.GetSD(bidTenantInfo);

```

## To Create OR Poll UWL2.0 session

Add namespace on the top of the your page:

```
using BIDHelpers.BIDSessions;
using BIDHelpers.BIDSessions.Model;

```
- To create new UWL2.0 session 
Copy and past below line:

```
BIDTenantInfo bidTenantInfo = new BIDTenantInfo("<dns>", "<communityName>", "<licenseKey>");
BIDSession sessionResponse = BIDSessions.CreateNewSession(bidTenantInfo, null, null);

```

- To poll new UWL2.0 session 
Copy and past below line:

```
BIDTenantInfo bidTenantInfo = new BIDTenantInfo("<dns>", "<communityName>", "<licenseKey>");
BIDSessionResponse pollResponse = BIDSessions.PollSession(bidTenantInfo, "sessionResponse.sessionId", true, true);

```

## To Request Email Verification link and Verify / Redeem Email verification link

Add namespace on the top of the your page:

```
using BIDHelpers.BIDAccessCodes;
using BIDHelpers.BIDTenant.Model;

```
- To Request Email Verification link
Copy and past below line:

```
BIDTenantInfo bidTenantInfo = new BIDTenantInfo("<dns>", "<communityName>", "<licenseKey>");
var requestEmailVerificationResponse  = BIDAccessCodes.RequestEmailVerificationLink(bidTenantInfo, "<emailTo>", "<emailTemplateB64OrNull>", "<emailSubjectOrNull>", "<createdBy>", "<ttl_seconds_or_null>");

```

- To poll new UWL2.0 session 
Copy and past below line:

```
BIDTenantInfo bidTenantInfo = new BIDTenantInfo("<dns>", "<communityName>", "<licenseKey>");
var fetchAccessCode = BIDAccessCodes.VerifyAndRedeemEmailVerificationCode(bidTenantInfo, requestEmailVerificationResponse.code);

```

## To Request/Verify OTP through email and/or sms

Add namespace on the top of the your page:

```
using BIDHelpers.BIDOTP;
using BIDHelpers.BIDOTP.Model;
using BIDHelpers.BIDTenant.Model;

```
- To Request OTP through email and/or sms
Copy and past below line:

```
BIDTenantInfo bidTenantInfo = new BIDTenantInfo("<dns>", "<communityName>", "<licenseKey>");
BIDOtpResponse requestOtp = BIDOTP.RequestOTP(bidTenantInfo, "<userName>", "<emailToOrNull>", "<smsToOrNull>", "<smsISDCodeOrNull>");

```

- To Verify OTP sent through email and/or sms 
Copy and past below line:

```
BIDTenantInfo bidTenantInfo = new BIDTenantInfo("<dns>", "<communityName>", "<licenseKey>");
BIDOtpVerifyResult verifyOTP = BIDOTP.VerifyOTP(bidTenantInfo, "<username>", "<otpCode>");

```


## To create/poll new Driver's License verification session

Add namespace on the top of the your page:

```
using BIDHelpers.BIDVerifyDocument;
using BIDHelpers.BIDVerifyDocument.Model;
using BIDHelpers.BIDMessaging;
using BIDHelpers.BIDMessaging.Model;
using BIDHelpers.BIDTenant.Model;

```
- To create new Driver's License verification session
Copy and past below line:

```
BIDTenantInfo bidTenantInfo = new BIDTenantInfo("<dns>", "<communityName>", "<licenseKey>");			
BIDCreateDocumentSessionResponse createdSessionResponse = BIDVerifyDocument.CreateDocumentSession(bidTenantInfo, "<dvcId>", "dl_object");

```

- Trigger SMS
```
BIDSendSMSResponse smsResponse = BIDMessaging.SendSMS(bidTenantInfo, "<smsTo>", "<smsISDCode>", "<smsTemplateB64>");

```

- To poll new Driver's License response and verify the document
Copy and past below line:

```
BIDTenantInfo bidTenantInfo = new BIDTenantInfo("<dns>", "<communityName>", "<licenseKey>");			
BIDPollSessionResponse pollSessionResponse = BIDVerifyDocument.PollSessionResult(bidTenantInfo, "<dvcId>", "<sessionId>");

```

- To verify the document
```
BIDVerifyDocumentResponse documentResponse = BIDVerifyDocument.VerifyDocument(bidTenantInfo, "<dvcId>", "<verifications>", "<faceCompareDocument>");

```


## To Register and Authenticate using FIDO2

Add namespace on the top of the your page:

```
using BIDHelpers.BIDWebAuthn;
using BIDHelpers.BIDWebAuthn.Model;
using BIDHelpers.BIDTenant.Model;

```
- To FetchAttestationOptions for register
Copy and past below line:

```
BIDTenantInfo bidTenantInfo = new BIDTenantInfo("<dns>", "<communityName>", "<licenseKey>");	
		
//If your device is a security key, such as a YubiKey
var bidAttestationValues = new BIDAttestationOptionsValue()
    {
		displayName = "<displayName>",
        username = "<username>",
        dns = "<dns>",
        attestation = "direct",
        authenticatorSelection = new BIDAuthenticatorSelectionValue()
        {
           requireResidentKey = true
        },
    };

//If your device is a platform authenticator, such as TouchID:
var bidAttestationValues = new BIDAttestationOptionsValue()
	{
		ddisplayName = "<displayName>",
		username = "<username>",
		dns = "<dns>",
		attestation = "direct",
		authenticatorSelection = new BIDAuthenticatorSelectionValue()
		{
			authenticatorAttachment = "platform"
		},
	};
	
//If your device is a MacBook:
var bidAttestationValues = new BIDAttestationOptionsValue()
	{
		displayName = "<displayName>",
		username = "<username>",
		dns = "<dns>",
		attestation = "none",
	};

BIDAttestationOptionsResponse attestationOptionsResponse = BIDWebAuthn.FetchAttestationOptions(bidTenantInfo, "<bidAttestationValues>");

```


- To SubmitAttestationResult for registeration
Copy and past below line:

```
BIDTenantInfo bidTenantInfo = new BIDTenantInfo("<dns>", "<communityName>", "<licenseKey>");
BIDAttestationResultValue attestationResultRequest = new BIDAttestationResultValue
            {
                rawId = "<rawId>",
                response = new BIDAttestationResultResponseValue() { 
                attestationObject = "<attestationObject>",
                clientDataJSON = "<clientDataJSON>",
                getAuthenticatorData = {},
                getPublicKey = {},
                getPublicKeyAlgorithm = {},
                getTransports = {},
                },
                authenticatorAttachment = "<authenticatorAttachment>",
                getClientExtensionResults = "<getClientExtensionResults>",
                id = "<id>",
                type = "<type>",
                dns = "<current domain>"
            };
BIDAttestationResultData attestationResultResponse = BIDWebAuthn.SubmitAttestationResult(bidTenantInfo, "<attestationResultRequest>");

```

- To FetchAssertionOptions for authenticate
Copy and past below line:

```
BIDTenantInfo bidTenantInfo = new BIDTenantInfo("<dns>", "<communityName>", "<licenseKey>");	
		
BIDAssertionOptionValue assertionOptionRequest = new BIDAssertionOptionValue
            {
                username = "<username>",
                displayName = "<displayName>",
                dns = "<current domain>"
            };
BIDAssertionOptionResponse assertionOptionResponse = BIDWebAuthn.FetchAssertionOptions(bidTenantInfo, assertionOptionRequest);

```


- To SubmitAssertionResult for authenticate
Copy and past below line:

```
BIDTenantInfo bidTenantInfo = new BIDTenantInfo("<dns>", "<communityName>", "<licenseKey>");
BIDAssertionResultValue assertionResultRequest = new BIDAssertionResultValue
            {
                rawId = "<rawId>",
                dns = "<dns>",
                response = new BIDAssertionResultResponseValue()
                {
                    authenticatorData = "<authenticatorData>",
                    signature = "<signature>",
                    userHandle = "<userHandle>",
                    clientDataJSON = "<clientDataJSON>",
                },
                getClientExtensionResults = "<getClientExtensionResults>",
                id = "<id>",
                type = "<type>"
            };

BIDAssertionResultResponse assertionResultResponse = BIDWebAuthn.SubmitAssertionResult(bidTenantInfo, assertionResultRequest);


```