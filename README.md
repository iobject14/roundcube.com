# Secure Roundcube Webmail

This repository runs the Roundcube webmail interface with Docker. Roundcube is an email client, so it requires an existing IMAP mailbox server and an authenticated SMTP submission server.

## Requirements

- Linux VPS with Docker and Docker Compose
- A domain you own
- Existing IMAP and SMTP service
- TLS on IMAP and SMTP
- DNS records: A/AAAA, MX, SPF, DKIM, and DMARC

## Setup

1. Copy `.env.example` to `.env`.
2. Replace the example values with your mail-server details and a strong database password.
3. Keep `.env` private and never commit it.
4. Start Roundcube:

```bash
docker compose up -d
```

5. Open `http://YOUR_SERVER_IP:8080` for initial testing.

Before production use, place Roundcube behind HTTPS and restrict direct access to port 8080.

## SMTP policy

This setup uses authenticated SMTP submission. Configure sending limits with your SMTP provider or server. An unrestricted relay will be abused and blocklisted.

Suggested starting limits for normal personal or small-business use:

- 50 messages per hour per mailbox
- 200 messages per day per mailbox
- 25 recipients per message
- No unauthenticated relaying

For legitimate newsletters or transactional bulk mail, use an opt-in delivery provider with unsubscribe, bounce, and complaint handling.

## Security

- Use IMAP port 993 with TLS.
- Use SMTP port 587 with STARTTLS or port 465 with TLS.
- Enable automatic security updates and backups.
- Use unique, strong passwords.
- Never commit `.env`, passwords, API keys, certificates, or private keys.
