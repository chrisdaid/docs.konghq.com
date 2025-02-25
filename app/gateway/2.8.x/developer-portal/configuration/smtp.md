---
title: Dev Portal SMTP Configuration
badge: enterprise
---

The following property reference outlines each email and email variable used by the Dev Portal to send emails to Kong admins and developers.

These settings can be modified in the `Kong Manager` under the Dev Portal `Settings / Email` tab, or by running the following command:

```
curl http://localhost:8001/workspaces/<WORKSPACE_NAME> \
  --data "config.<PROPERTY_NAME>=off"
```

If they are not modified manually, the Dev Portal will use the default value defined in the Kong Configuration file.

Dev Portal email content and styling can be customized via [template files](/gateway/{{page.kong_version}}/developer-portal/theme-customization/emails/).

## portal_invite_email

**Default:** `on`

**Description:**
When enabled, Kong admins will be able to invite developers to a Dev Portal by using the Invite button in the Kong Manager.

**Email:**
```
Subject: Invite to access Dev Portal <WORKSPACE_NAME>

Hello Developer!

You have been invited to create a Dev Portal account at %s.
Please visit `<DEV_PORTAL_URL/register>` to create your account.
```


## portal_email_verification

**Default:** `off`

**Description:**
When enabled, developers will receive an email upon registration to verify their account. Developers will not be able to use the Dev Portal until their account is verified, even if auto-approve is enabled.


## portal_access_request_email

**Default:** `on`

**Description:**
When enabled, Kong Admins specified by `smtp_admin_emails` will receive an email when a Developer requests access to a Dev Portal.

```
Subject: Request to access Dev Portal <WORKSPACE NAME>

Hello Admin!

<DEVELOPER NAME> has requested Dev Portal access for <WORKSPACE_NAME>.
Please visit <KONG_MANAGER_URL/developers/requested> to review this request.
```


## portal_approved_email

**Default:** `on`

**Description:**
When enabled, developers will receive an email when access to a Dev Portal has been approved.

```
Subject: Dev Portal access approved

Hello Developer!
You have been approved to access <WORKSPACE_NAME>.
Please visit <DEV PORTAL URL/login> to login.

```

## portal_reset_email

**Default:** `on`

**Description:**
When enabled, developers will be able to use the Reset Password flow on a Dev Portal and will receive an email with password reset instructions.

When disabled, developers will *not* be able to reset their account passwords.

```
Subject: Password Reset Instructions for Dev Portal <WORKSPACE_NAME>.

Hello Developer,

Please click the link below to reset your Dev Portal password.

<DEV_PORTAL_URL/reset?token=12345>

This link will expire in <portal_reset_token_exp>

If you didn't make this request, keep your account secure by clicking
the link above to change your password.
```

## portal_reset_success_email

**Default:** `on`

**Description:**
When enabled, developers will receive an email after successfully resetting their Dev Portal account password.

When disabled, developers will still be able to reset their account passwords, but will not receive a confirmation email.

```
Subject: Dev Portal password change success

Hello Developer,
We are emailing you to let you know that your Dev Portal password at <DEV_PORTAL_URL> has been changed.

Click the link below to sign in with your new credentials.

<DEV_PORTAL_URL>
```


## portal_emails_from

**Default:** `nil`

**Description:**
The name and email address for the 'From' header included in all Dev Portal emails.

**Example :**

```
portal_emails_from = Your Name <example@example.com>
```


## portal_emails_reply_to

**Default:** `nil`

**Description:**
The email address for the 'Reply-To' header included in all Dev Portal emails.


**Example :**

```
portal_emails_reply_to: noreply@example.com
```
