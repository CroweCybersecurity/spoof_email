# spoof_email
spoof_email is a Python 3.X tool used to test Server Message Transfer Protocol (SMTP) server security. This tool was designed to simplify the testing of SMTP sending for normal and spoofed emails. The following features are supported:
- Basic SMTP variables
- CC and BCC recipients
- Custom headers
- Dynamic content variables (`{{.Server}}`)
- Secured Email Delivery Preference (in order):
    1. Required: SSL / TLS encryption
    2. Opportunistic: STARTTLS encryption
    3. None: No encryption
- All three major MIME SMTP types:
    - Text
    - HTML
    - Watch
- Dry run support
- Verbose delivery
- Logging with timestamps

## Design Insights
spoof_email was designed to increase the likeliness that a delivered email was to be accepted by the email server and client. The methods this tool uses to increase the likeliness are:
1. Offering all three major MIME SMTP types
2. Attempting the most secure encryption delivery first (i.e., 1. SSL/TLS, 2. STARTTLS, 3. Raw)
3. Stop attempting to send an email if an error arises
4. Allowing custom headers to be provided
5. Allowing easy customization of basic SMTP variables

## Examples
The following example will send a standard email to a recipient:
```
python spoof_email.py -sn "Test Email" -f john.doe@domain.tld -t jane.doe@domain.tld -s smtp1.domain.tld
```
The following example will perform a standard SMTP spoof of `jane.doe@domain.tld`:
```
python spoof_email.py -sn "Spoof Test Email" -f jane.doe@domain.tld -t jane.doe@domain.tld -s smtp1.domain.tld
```
The following example will perform a SPF-spoof of `jane.doe@domain.tld`:
```
python spoof_email.py -sn "SPF Spoof Test Email" -f john.doe@domain.tld -fh jane.doe@domain.tld -t jane.doe@domain.tld -s smtp1.domain.tld
```

## Contributions
We welcome contributions from the community. The following features are planned in future releases:
- More content variables (`{{.FirstName}}`, `{{.LastName}}`)
- Attachments
- Custom content
    - Idea is to provide `message.html` and have `spoof_email.py` convert the file to text and watch MIME types
- Recipient lists
- Extended README for:
    - `On Behalf of` emails
    - Content checks
    - SPF/DKIM/DMARC continued research and bypasses