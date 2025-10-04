# Appwrite Coolify Deployment Guide

This guide will help you deploy your forked Appwrite instance on Coolify.

## Prerequisites

- Coolify instance running
- Access to your forked Appwrite repository
- Basic understanding of Docker and environment variables

## Deployment Steps

### 1. Repository Setup

Your forked repository is already set up with the necessary files:
- `docker-compose.coolify.yml` - Production-ready Docker Compose configuration
- `coolify.env` - Environment variables template
- This deployment guide

### 2. Coolify Configuration

1. **Create a New Project in Coolify:**
   - Go to your Coolify dashboard
   - Click "New Project"
   - Choose "Docker Compose" as the source type

2. **Repository Configuration:**
   - Repository URL: `https://github.com/confersolutions/appwrite.git`
   - Branch: `main`
   - Docker Compose File: `docker-compose.coolify.yml`

3. **Environment Variables:**
   - Copy the contents of `coolify.env` to your Coolify environment variables
   - **IMPORTANT:** Change the following values for production:
     - `_APP_OPENSSL_KEY_V1`: Generate a secure random key
     - `_APP_EXECUTOR_SECRET`: Generate a secure random key
     - `_APP_DB_PASS`: Set a strong database password
     - `_APP_DB_ROOT_PASS`: Set a strong root database password
     - `_APP_DB_USER`: Set a custom database username
     - `_APP_REDIS_PASS`: Set a Redis password (optional but recommended)

### 3. Domain Configuration

Update the following environment variables with your domain:
- `_APP_CONSOLE_HOSTNAMES`: Your domain (e.g., `yourdomain.com`)
- `_APP_CONSOLE_DOMAIN`: Your domain
- `_APP_DOMAIN_FUNCTIONS`: `functions.yourdomain.com`
- `_APP_DOMAIN_SITES`: `sites.yourdomain.com`

### 4. Storage Configuration (Optional)

For production, consider using cloud storage:
- **AWS S3**: Set `_APP_STORAGE_DEVICE=s3` and configure S3 credentials
- **DigitalOcean Spaces**: Set `_APP_STORAGE_DEVICE=do` and configure DO credentials
- **Backblaze B2**: Set `_APP_STORAGE_DEVICE=backblaze` and configure B2 credentials

### 5. Email Configuration

For production email functionality:
- Set `_APP_SMTP_HOST` to your SMTP server
- Set `_APP_SMTP_PORT` (usually 587 for TLS or 465 for SSL)
- Set `_APP_SMTP_SECURE` to `tls` or `ssl`
- Configure `_APP_SMTP_USERNAME` and `_APP_SMTP_PASSWORD`

### 6. Security Considerations

1. **Change Default Secrets:**
   - Generate strong, unique values for all secret keys
   - Use a password manager to generate secure passwords

2. **Database Security:**
   - Use strong database passwords
   - Consider using external database services for production

3. **Network Security:**
   - Configure firewall rules appropriately
   - Use HTTPS in production (set `_APP_OPTIONS_FORCE_HTTPS=enabled`)

### 7. Deployment

1. **Deploy the Application:**
   - Click "Deploy" in Coolify
   - Monitor the deployment logs
   - Wait for all services to be healthy

2. **Initial Setup:**
   - Access your Appwrite console at `https://yourdomain.com/console`
   - Create your first project
   - Configure your API keys

### 8. Post-Deployment

1. **Verify Services:**
   - Check that all containers are running
   - Test the API endpoints
   - Verify the console is accessible

2. **Backup Configuration:**
   - Set up regular backups for your database
   - Consider backing up your environment variables

3. **Monitoring:**
   - Set up monitoring for your Appwrite instance
   - Monitor resource usage and performance

## Troubleshooting

### Common Issues

1. **Services Not Starting:**
   - Check environment variables are correctly set
   - Verify all required secrets are configured
   - Check Docker logs for specific errors

2. **Database Connection Issues:**
   - Verify database credentials
   - Check if MariaDB container is running
   - Ensure database is accessible from Appwrite container

3. **Storage Issues:**
   - Verify storage configuration
   - Check storage permissions
   - Ensure storage volumes are properly mounted

### Logs

To view logs in Coolify:
1. Go to your project
2. Click on the service you want to check
3. View the logs tab

## Maintenance

### Updates

To update your Appwrite instance:
1. Pull the latest changes from the repository
2. Update the Docker images in your Coolify configuration
3. Redeploy the application

### Backups

Regular backups are essential:
- Database backups
- Volume backups (uploads, functions, etc.)
- Configuration backups

## Support

For issues specific to this deployment:
- Check the [Appwrite Documentation](https://appwrite.io/docs)
- Review the [Coolify Documentation](https://coolify.io/docs)
- Check the GitHub repository for updates

## Security Notes

- Never commit secrets to your repository
- Use environment variables for all sensitive configuration
- Regularly update your Appwrite instance
- Monitor for security updates
- Use strong passwords and keys
- Enable HTTPS in production
- Consider using a reverse proxy for additional security
