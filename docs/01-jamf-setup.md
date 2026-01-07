# Jamf Now Setup Guide

## Overview

This guide walks through the complete setup and configuration of Jamf Now, a cloud-based Mobile Device Management (MDM) platform for managing iOS devices in enterprise environments. Jamf Now provides essential features for device enrollment, policy enforcement, and fleet management without requiring on-premises infrastructure.

## Prerequisites

- Valid Apple ID for Apple Business Manager (recommended)
- Administrative access to configure MDM settings
- Understanding of iOS device management concepts
- Network access for device communication with Jamf cloud services

## Initial Account Setup

### Creating Jamf Now Account

1. Navigate to [Jamf Now](https://www.jamf.com/products/jamf-now/) and click "Try Jamf Now Free"
2. Complete account registration with business information:
   - Organization name
   - Business email address
   - Administrator contact details
   - Organization size and industry
3. Verify email address through confirmation link
4. Log into Jamf Now dashboard for initial configuration

### Dashboard Overview

The Jamf Now dashboard provides several key sections:

**Dashboard Home**
- Device overview and status summary
- Recent activity feed
- Quick access to common tasks
- Compliance status indicators

**Devices**
- Complete device inventory
- Device details and specifications
- Enrollment status tracking
- Remote action capabilities

**Blueprints (Profiles)**
- Security and configuration profiles
- Policy templates and customization
- Profile assignment management
- Compliance rule definitions

**Apps**
- Application catalog and deployment
- Custom app upload capabilities
- Installation and removal tracking
- License management

## Platform Configuration

### Organization Settings

Configure basic organization information:

1. Navigate to **Settings > Organization**
2. Complete organization profile:
   ```
   Organization Name: [Your Company Name]
   Support Email: helpdesk@company.com
   Support Phone: +1-555-123-4567
   Time Zone: [Your Time Zone]
   ```
3. Set up administrator accounts and permissions
4. Configure notification preferences for alerts and reports

### Security Settings

Essential security configurations:

1. **Two-Factor Authentication**
   - Enable 2FA for all administrator accounts
   - Configure backup authentication methods
   - Set session timeout policies

2. **API Access**
   - Generate API tokens for integration (if needed)
   - Configure webhook endpoints for automated responses
   - Set access logging and monitoring

3. **Device Security**
   - Define minimum iOS version requirements
   - Configure jailbreak detection policies
   - Set device encryption requirements

## Apple Push Notification Setup

### APNs Certificate Configuration

Critical for device communication:

1. **Generate Certificate Signing Request (CSR)**
   - Access **Settings > APNs Certificate**
   - Download CSR file from Jamf Now
   - Save CSR securely for Apple Developer portal

2. **Create APNs Certificate**
   - Log into [Apple Developer Portal](https://developer.apple.com)
   - Navigate to Certificates, Identifiers & Profiles
   - Create new APNs certificate using downloaded CSR
   - Download completed certificate (.pem file)

3. **Upload Certificate to Jamf Now**
   - Return to Jamf Now APNs settings
   - Upload the .pem certificate file
   - Verify certificate validity and expiration date
   - Test push notification connectivity

### Troubleshooting APNs Issues

Common APNs problems and solutions:

| Issue | Cause | Solution |
|-------|--------|----------|
| Certificate upload fails | Incorrect file format | Ensure .pem format, not .p12 |
| Push notifications not working | Expired certificate | Renew certificate in Apple Developer portal |
| Device communication fails | Network blocking | Configure firewall for Apple domains |

## Initial Blueprint Creation

### Default Security Profile

Create a basic security blueprint:

1. Navigate to **Blueprints > Create New Blueprint**
2. Configure basic settings:
   ```
   Blueprint Name: Standard Security
   Description: Default security profile for corporate devices
   Target Platform: iOS
   ```

3. **Passcode Requirements**
   - Require passcode: Enabled
   - Minimum length: 6 characters
   - Alphanumeric requirement: Optional
   - Auto-lock timeout: 5 minutes

4. **Basic Restrictions**
   - Allow app installation: Yes
   - Allow camera: Yes
   - Allow Safari: Yes
   - Allow Siri: Yes
   - Allow screenshots: Yes

5. **WiFi Configuration**
   - Add corporate WiFi networks
   - Configure authentication (WPA2-Enterprise if applicable)
   - Set auto-connect preferences

## Testing Platform Setup

### Verification Checklist

Before enrolling devices, verify:

- [ ] APNs certificate uploaded and valid
- [ ] Organization settings completed
- [ ] Administrator accounts configured
- [ ] Default blueprint created
- [ ] Network connectivity tested
- [ ] Enrollment invitation codes generated

### Test Device Enrollment

1. **Generate Enrollment Code**
   - Navigate to **Devices > Invite Device**
   - Generate invitation code
   - Note 15-minute expiration window

2. **Test Enrollment Process**
   - Use test iOS device
   - Follow enrollment steps from [Device Enrollment Guide](02-device-enrollment.md)
   - Verify device appears in inventory
   - Confirm blueprint application

## Dashboard Navigation

### Key Management Areas

**Device Management**
- View all enrolled devices
- Check device compliance status
- Execute remote actions (lock, wipe, etc.)
- Monitor last check-in times

**Profile Management**
- Create and edit blueprints
- Assign profiles to devices
- Monitor profile installation status
- Track compliance violations

**Reporting**
- Generate device inventory reports
- Compliance status summaries
- User activity logs
- Security incident tracking

### Daily Administrative Tasks

Regular management activities:

1. **Morning Review**
   - Check device compliance dashboard
   - Review overnight alerts and notifications
   - Verify all devices checked in within 24 hours

2. **Profile Updates**
   - Apply security patches and updates
   - Modify blueprints as policy changes
   - Deploy new application packages

3. **User Support**
   - Assist with enrollment issues
   - Troubleshoot device connectivity problems
   - Process device replacement requests

## Security Best Practices

### Administrator Account Management

- Use unique, strong passwords for all admin accounts
- Enable two-factor authentication on all accounts
- Regularly review and rotate admin credentials
- Limit admin privileges to necessary personnel only

### Certificate Management

- Monitor APNs certificate expiration dates
- Maintain backup certificates for continuity
- Document certificate renewal procedures
- Test certificate functionality regularly

### Network Security

- Ensure Jamf Now communication over HTTPS only
- Configure firewall rules for Apple MDM domains
- Monitor network traffic for suspicious activity
- Implement network segmentation for managed devices

## Common Setup Issues

### Account Access Problems

**Symptom**: Cannot log into Jamf Now dashboard
**Solution**:
1. Verify email address and password
2. Check for account lockout notifications
3. Reset password if necessary
4. Clear browser cache and cookies

### Certificate Issues

**Symptom**: APNs certificate upload fails
**Solution**:
1. Verify certificate file format (.pem)
2. Check certificate hasn't expired
3. Ensure certificate matches organization
4. Regenerate if corrupted

### Device Communication

**Symptom**: Devices not checking in
**Solution**:
1. Verify APNs certificate validity
2. Check device internet connectivity
3. Confirm Jamf Now service status
4. Review firewall configurations

## Next Steps

Once Jamf Now platform is properly configured:

1. Proceed to [Device Enrollment Process](02-device-enrollment.md)
2. Configure detailed security profiles using [Profile Configuration Guide](03-profile-configuration.md)
3. Develop troubleshooting procedures with [Troubleshooting Guide](04-troubleshooting.md)

## Additional Resources

- [Jamf Now Official Documentation](https://docs.jamf.com/jamf-now/)
- [Apple MDM Protocol Reference](https://developer.apple.com/documentation/devicemanagement)
- [iOS Security Guide](https://support.apple.com/guide/security/welcome/web)
- [Apple Business Manager Setup](https://business.apple.com)