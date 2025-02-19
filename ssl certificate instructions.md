"I created a digital ocean droplet, installed nginx web server and am hosting a website. I also created gave it a custom domain name (www.qdtruong.com) but now when I go to www.qdtruong.com, my browser says the site is not safe. How do I make it secure?"

To secure your website, you need to install an SSL certificate. The best way to do this is by using **Let’s Encrypt**, which provides free SSL certificates and works well with Nginx.

Here’s a step-by-step guide:

1. **Install Certbot**:
   Certbot is a tool that automates the process of obtaining and installing SSL certificates.
   ```bash
   sudo apt update
   sudo apt install certbot python3-certbot-nginx
   ```

2. **Obtain an SSL Certificate**:
   Run Certbot for Nginx to obtain and install the certificate. Replace `www.qdtruong.com` with your domain.
   ```bash
   sudo certbot --nginx -d qdtruong.com -d www.qdtruong.com
   ```

3. **Configure Nginx to Use the SSL Certificate**:
   Certbot will automatically update your Nginx configuration. When prompted, choose to redirect HTTP traffic to HTTPS, which ensures all traffic is encrypted.

4. **Test the SSL Certificate**:
   Visit your site at https://www.qdtruong.com to verify it’s secure.

5. **Set Up Auto-Renewal**:
   Let’s Encrypt certificates expire every 90 days, so it’s essential to set up automatic renewal.
   Certbot’s installation typically includes a cron job that runs `certbot renew` twice daily, ensuring your certificates are renewed automatically. You can manually check the renewal process with:
   ```bash
   sudo certbot renew --dry-run
   ```

After completing these steps, your website should load securely.

"^[[DSaving debug log to /var/log/letsencrypt/letsencrypt.log
Enter email address (used for urgent renewal and security notices)
 (Enter 'c' to cancel): qdtruong@gmail.com
Invalid email address:qdtruong@gmail.com.
There seem to be problems with that address."

The error you're seeing could be due to the command's syntax or formatting. Here’s a step-by-step approach to help resolve it:

1. **Double-check the email address format**:
   Ensure there’s no extra whitespace or special characters. If it asks for the email address in the command line directly, try adding a space between the email flag and address.

2. **Re-run the Certbot command**:
   If you entered the email address inline, try this command instead, adjusting the spacing:

   ```bash
   sudo certbot --nginx -d qdtruong.com -d www.qdtruong.com --email qdtruong@gmail.com --agree-tos --no-eff-email
   ```

   The flags here:
   - `--email qdtruong@gmail.com` provides your email for notifications.
   - `--agree-tos` automatically agrees to the Terms of Service.
   - `--no-eff-email` opts out of receiving EFF-related (Electronic Frontier Foundation) emails.

3. **Proceed through prompts**:
   If Certbot still prompts for your email, enter it directly (without any extra characters) and see if the command proceeds.

This should help you get past the email issue and continue with the SSL certificate setup.
