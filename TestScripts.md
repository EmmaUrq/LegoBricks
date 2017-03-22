UAT: https://uat-dpu138.sicloud.atos.net/auth/login
GITHUB ISSUES: https://github.com/atosorigin/DEUX-138-Vivace
Timesheet shortcode for this week confirmed as Ace Sprint 1
Timecode is GB.708555.010.54 CCD Accelerated Cap Enviro (ACE)
DEV SPRINT TRELLO: https://trello.com/b/VinYJdwi/138-sprintboard
TESTER TRELLO: https://trello.com/b/4xJ0n0It/138-testing
GENERAL TRELLO: https://trello.com/b/oUTLzQhW/138-vivace

# Password Reset Test Scripts

Happy Flow Tests
====
All these tests should succeed without an error.
----
User follows the password reset steps, receives the password reset e-mail, and successfully resets their password using that link. They can then log in using the new password.

User exits the password reset page without performing any action.

User successfully logs in with previous password after requesting a password reset.

Remove stylesheets and ensure the page is still readable.


Validation Tests
====
An error message should be displayed after these actions.
----

Reset an account that does not exist.
Reset an account with an e-mail that is not on the system.
Reset an account that has not been successfully activated yet. 
	Expected result: resend activation e-mail
Reset an account with an expired e-mail link. 
	Expected result: resend, or redirect to password reset.
Boundary test the e-mail input field. 
Boundary test the password input field.
	Leave password field blank.
	Enter mis-matching passwords.
	Enter a password that does not meet minimum security requirements.
	Enter one field blank, the other valid, blank invalid etc.
Boundary test validation code.
	Enter invalid code, non-matching code, nonsense letters etc.
User password resets an account that is expired/disabled/deleted. [IF APPLICABLE]

# Timeout Tests

Forgotten password token expires after 15 mins.
Logged in user will auto logout after 30 mins.


#Password Reset Tests -- ACTUAL
	User Requests a Password Reset: PASS
	[Expected result: If your email has an account, your password reset has been sent. Please check you email for instructions.]
	User Receives the Password Reset E-mail: PASS
		From: do_not_reply@sicloud.atos.net [mailto:do_not_reply@sicloud.atos.net] 
		Sent: 20 March 2017 15:26
		To: Urquhart, Emma <emma.urquhart@atos.net>
		Subject: Reset Your Password

		Hello!
		Please click the following link to reset your password: 
		https://uat-dpu138.sicloud.atos.net/auth/resetPassword/6baeb5d8-4030-4efa-ab5f-c6b842d40e56 
	User Successfully Resets the Password: PASS
	Unable to Reset a Password for a Non-Existent Account: PASS
	[Expected result: If your email has an account, your password reset has been sent. Please check you email for instructions.]
	
	User Tries to Re-Use a Password Reset Token
	[Expected	'Your reset request has expired. Request another password reset.']


-----------------------------------------------------
//UAT SITE TESTS BEGIN HERE

#Login Tests
	User logs in with a non-existent account: PASS
	[Expected results: "Unable to log you in. Your credentials were not recognised."]
	User logs in with an unactivated account: PASS
	[Expected results: "Unable to log you in. Your account is not currently active.
Click here to resend the activation email."]

#Resend Activation Page
	https://uat-dpu138.sicloud.atos.net/auth/resendActivation
	
	User Resends Activation E-mail: PASS
	[Expected results: Second activation e-mail.]
	


# Register

	Try to register the same user twice.
	[Expected result: "A user already exists with the given details."]

# Issues
Error messages should in a red font.
Delay in showing errors for password/e-mail fields.
'You can successfully registered' wording.
'Please check you email' password reset wording.
Reset password gives no indication of the account name being reset.
Password reset doesn't match the 1st and second confirm password fields. You can reset with the second field non-matching.


