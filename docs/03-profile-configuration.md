# Profile Configuration Guide

## Overview

This comprehensive guide details the creation, configuration, and management of device profiles (blueprints) in Jamf Now. Profiles define security policies, restrictions, network settings, and application management rules that govern iOS device behavior in enterprise environments. Proper profile configuration is essential for maintaining security standards while ensuring user productivity.

## Understanding Blueprints

### Blueprint Concepts

Jamf Now uses "Blueprints" as configuration profiles that contain:

- **Security Policies**: Passcode requirements, encryption settings, jailbreak detection
- **Restrictions**: App limitations, feature controls, content filtering
- **Network Configuration**: WiFi settings, VPN profiles, certificate distribution
- **App Management**: Automatic installation, blacklists, enterprise app deployment
- **Device Settings**: Email configuration, update policies, backup restrictions

### Blueprint Hierarchy

Blueprint application follows this priority order:
1. Device-specific assignments (highest priority)
2. User group assignments
3. Default organizational blueprint
4. iOS default settings (lowest priority)

## Creating Security Profiles

### Executive Profile (High Security)

For C-level executives and sensitive role users:

#### Passcode Configuration
```
Settings Path: Blueprints > Create New > Security
Passcode Required: Yes
Minimum Length: 8 characters
Character Requirements: Alphanumeric + special characters
Auto-lock Timeout: 2 minutes
Max Failed Attempts: 6 attempts
Passcode Expiration: 90 days
Passcode History: 12 previous passcodes
Grace Period: 0 minutes
```

#### Restriction Settings
```
App Store: Blocked
Installing Apps: Administrator only
Removing Apps: Administrator only
Safari Browser: Blocked
Camera: Disabled
Screenshots: Disabled
AirDrop: Disabled
Siri: Disabled when locked
Control Center: Disabled on lock screen
Today View: Disabled on lock screen
Notifications View: Disabled on lock screen
```

#### Network and Security
```
iCloud Backup: Disabled
iTunes Backup: Encrypted backups only
Automatic Downloads: Disabled
Auto-lock: Enabled (2 minutes maximum)
Touch ID/Face ID: Allowed with passcode backup
Activation Lock: Enabled
Find My iPhone: Forced on
```

### Sales Profile (Moderate Security)

For sales representatives and customer-facing roles:

#### Passcode Configuration
```
Passcode Required: Yes
Minimum Length: 6 characters
Character Requirements: Numeric allowed
Auto-lock Timeout: 5 minutes
Max Failed Attempts: 10 attempts
Passcode Expiration: 180 days
Passcode History: 6 previous passcodes
Grace Period: 1 hour
```

#### Application Management
```
App Store: Allowed with restrictions
Installing Apps: User allowed (business apps only)
Removing Apps: User allowed
Required Apps: 
  - Microsoft Teams
  - Zoom
  - Microsoft Outlook
  - OneDrive
Restricted App Categories:
  - Games
  - Social Media (except LinkedIn)
  - Entertainment
```

#### Communication Settings
```
Email Configuration: Exchange ActiveSync
VPN: Auto-connect for external access
WiFi: Corporate networks auto-configured
Personal Hotspot: Allowed
AirDrop: Contacts only
iMessage/FaceTime: Allowed
```

### Field Tech Profile (Basic Security)

For technicians and operational staff requiring flexibility:

#### Passcode Configuration
```
Passcode Required: Yes
Minimum Length: 4 characters
Character Requirements: Numeric only
Auto-lock Timeout: 10 minutes
Max Failed Attempts: Unlimited
Passcode Expiration: Never
Grace Period: 4 hours
```

#### Operational Settings
```
App Store: Full access
Camera: Enabled (for documentation)
Screenshots: Enabled
Safari: Enabled with safe browsing
Cellular Data: Enabled for field operations
Personal Hotspot: Enabled
AirDrop: Everyone (for file sharing)
```

#### Field-Specific Apps
```
Required Applications:
  - TeamViewer
  - Microsoft Remote Desktop
  - Field service management app
  - Inventory tracking app
Cellular Data Usage: Unlimited for business apps
Location Services: Always enabled for business apps
Background App Refresh: Enabled for critical apps
```

## Advanced Configuration Settings

### Network Configuration

#### Corporate WiFi Setup
```
Blueprint Section: Network > WiFi
Network Name (SSID): CorpWiFi-Secure
Security Type: WPA2-Enterprise
Authentication: EAP-TLS certificate
Certificate: [Upload corporate certificate]
Auto-connect: Enabled
Hidden Network: No
Proxy Configuration: Automatic
```

#### VPN Configuration
```
VPN Type: IKEv2
Server Address: vpn.company.com
Remote ID: Company VPN
Local ID: [User certificate]
Authentication: Certificate + User credentials
Split Tunneling: Disabled for security
On-demand Connection: 
  - Connect for corporate domains
  - Connect on cellular networks
```

### Email Configuration

#### Exchange ActiveSync Setup
```
Account Type: Microsoft Exchange
Exchange Server: mail.company.com
Domain: company.com
Username: [User's email]
Use SSL: Yes
Mail Days to Sync: 1 month
Sync Calendars: Yes
Sync Contacts: Yes
Sync Notes: No
Allow Messages to be moved: No
```

### Certificate Management

#### Installing Certificates
```
Certificate Types:
  - Root CA certificates
  - Intermediate CA certificates
  - User authentication certificates
  - WiFi authentication certificates
  - VPN authentication certificates

Installation Method:
1. Upload certificate to Jamf Now
2. Add to blueprint under Certificates section
3. Set trust level (Full Trust for root CAs)
4. Assign to appropriate device groups
```

## Application Management

### Required App Deployment

#### Business Application Installation
```
Deployment Method: Automatic installation
App Source: 
  - Apple App Store (business apps)
  - Custom enterprise apps (.ipa files)
  - Volume Purchase Program (VPP)

Configuration:
- Install automatically on enrollment
- Prevent user removal
- Update automatically
- License management for paid apps
```

#### App Blacklisting
```
Restricted Categories:
  - Games (except educational)
  - Social media (company policy dependent)
  - Streaming media services
  - File sharing applications
  - Cryptocurrency applications

Enforcement: Block installation and remove existing
```

### Custom Application Deployment

#### Enterprise App Installation
```
Upload Process:
1. Obtain signed .ipa file
2. Upload to Jamf Now under Apps section
3. Configure app details and permissions
4. Assign to specific blueprints
5. Test installation on sample devices

Management Options:
- Required installation (cannot be removed)
- Optional installation (user choice)
- Automatic updates
- License tracking
```

## Compliance and Monitoring

### Compliance Rules

#### Defining Compliance Standards
```
Security Compliance:
  - Passcode enabled and meets complexity
  - Device not jailbroken
  - iOS version within 2 major releases
  - Required apps installed
  - Encryption enabled

Operational Compliance:
  - Device checks in within 7 days
  - No unauthorized apps installed
  - Corporate certificates valid
  - VPN profile configured
```

#### Compliance Monitoring
```
Monitoring Frequency: Real-time with daily reports
Compliance Actions:
  - Warning notifications for minor violations
  - Restricted access for major violations
  - Automatic remediation where possible
  - Escalation procedures for persistent violations

Reporting:
  - Daily compliance dashboard
  - Weekly compliance reports
  - Monthly trend analysis
  - Incident tracking and resolution
```

## Profile Testing and Validation

### Pre-Deployment Testing

#### Test Environment Setup
```
Test Devices: 
  - One device per profile type
  - Various iOS versions
  - Different device models

Testing Checklist:
□ Profile installs without errors
□ All restrictions function correctly
□ Required apps install automatically
□ Network connectivity works
□ Security policies enforce properly
□ User experience remains acceptable
□ Compliance rules trigger appropriately
```

#### Validation Procedures
```
Security Validation:
1. Test passcode requirements enforcement
2. Verify app installation restrictions
3. Confirm network security settings
4. Test remote management capabilities
5. Validate compliance monitoring

Functionality Validation:
1. Test all required applications
2. Verify network connectivity (WiFi/VPN)
3. Confirm email configuration
4. Test camera and other device features
5. Validate update mechanisms
```

### Gradual Deployment Strategy

#### Phased Rollout Process
```
Phase 1: IT Team Testing (Week 1)
  - Deploy to IT staff devices
  - Identify and resolve issues
  - Document configuration changes

Phase 2: Pilot Group (Week 2-3)
  - Deploy to volunteer users from each role
  - Collect feedback and usage data
  - Adjust profiles based on findings

Phase 3: Department Rollout (Week 4-6)
  - Deploy department by department
  - Monitor compliance and issues
  - Provide user training and support

Phase 4: Full Deployment (Week 7+)
  - Complete organization rollout
  - Ongoing monitoring and maintenance
  - Continuous improvement process
```

## Troubleshooting Profile Issues

### Common Configuration Problems

| Issue | Symptoms | Root Cause | Solution |
|-------|----------|------------|----------|
| Profile won't install | Installation error | Certificate issues | Verify certificate validity |
| Apps won't auto-install | Missing required apps | VPP license shortage | Acquire additional licenses |
| WiFi profile fails | Connection failures | Wrong certificate/credentials | Update network credentials |
| VPN won't connect | Authentication errors | Certificate mismatch | Re-issue VPN certificates |
| Restrictions not working | Policy not enforced | Sync delay | Force device check-in |

### Profile Conflict Resolution

#### Identifying Conflicts
```
Common Conflict Sources:
  - Multiple profiles with same settings
  - User-installed profiles vs. MDM profiles
  - iOS default settings vs. managed settings
  - App-specific configurations vs. system restrictions

Diagnostic Steps:
1. Review all installed profiles on device
2. Check profile installation order
3. Identify conflicting settings
4. Determine precedence rules
5. Resolve conflicts through profile updates
```

## Profile Maintenance

### Regular Maintenance Tasks

#### Weekly Tasks
```
□ Review compliance dashboards
□ Check for failed profile installations
□ Monitor certificate expiration dates
□ Update app deployment status
□ Address user support tickets
```

#### Monthly Tasks
```
□ Review and update security policies
□ Analyze compliance trends
□ Update required application lists
□ Refresh network configurations
□ Conduct security assessment
```

#### Quarterly Tasks
```
□ Comprehensive profile review
□ User feedback collection and analysis
□ Security policy updates
□ Certificate renewal planning
□ Technology stack evaluation
```

### Version Management

#### Profile Versioning Strategy
```
Version Numbering: [Major].[Minor].[Patch]
  - Major: Significant policy changes
  - Minor: Feature additions or modifications
  - Patch: Bug fixes and minor updates

Change Management:
1. Document all changes with rationale
2. Test changes in staging environment
3. Schedule deployment during maintenance windows
4. Communicate changes to affected users
5. Monitor deployment success and issues
```

## Next Steps

After configuring profiles:

1. Deploy profiles to test devices for validation
2. Monitor compliance and user feedback
3. Establish ongoing maintenance procedures
4. Refer to [Troubleshooting Guide](04-troubleshooting.md) for issue resolution

## Additional Resources

- [Apple Configuration Profile Reference](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf)
- [iOS Security Guide](https://support.apple.com/guide/security/welcome/web)
- [Jamf Now Profile Management](https://docs.jamf.com/jamf-now/)
- [Apple Business Manager Setup](https://business.apple.com)