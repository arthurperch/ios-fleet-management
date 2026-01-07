# Device Enrollment Process

## Overview

This guide provides detailed procedures for enrolling iOS devices into Jamf Now MDM management. The enrollment process establishes the management relationship between devices and the MDM platform, enabling policy enforcement, security controls, and remote administration capabilities essential for enterprise device management.

## Prerequisites

- Jamf Now platform configured per [Jamf Setup Guide](01-jamf-setup.md)
- Valid APNs certificate installed and verified
- iOS devices running iOS 13.0 or later
- Stable internet connection on target devices
- Administrative access to Jamf Now dashboard

## Enrollment Methods

### Method 1: Invitation Code Enrollment (Primary)

Best for individual device enrollment and lab testing:

1. **Generate Enrollment Invitation**
   - Log into Jamf Now dashboard
   - Navigate to **Devices > Invite Device**
   - Click **Generate Invitation**
   - Copy invitation code (expires in 15 minutes)

2. **Device-Side Enrollment**
   - On iOS device: Open **Settings > General > VPN & Device Management**
   - Tap **Enroll in Mobile Device Management**
   - Enter invitation code when prompted
   - Tap **Next** to begin enrollment process

3. **Complete Enrollment**
   - Review permissions and profile information
   - Tap **Install** to accept MDM profile
   - Enter device passcode when prompted
   - Confirm enrollment completion

### Method 2: Email Invitation

Suitable for remote user enrollment:

1. **Send Email Invitation**
   - In Jamf Now: **Devices > Invite Device**
   - Enter user email address
   - Customize invitation message
   - Send invitation

2. **User Enrollment Process**
   - User receives email with enrollment link
   - Opens link on iOS device
   - Follows on-screen enrollment instructions
   - Completes profile installation

### Method 3: QR Code Enrollment

Efficient for bulk enrollment scenarios:

1. **Generate QR Code**
   - In Jamf Now: **Devices > Invite Device**
   - Select **QR Code** option
   - Generate and display QR code

2. **Scan and Enroll**
   - On iOS device: Open Camera app
   - Scan QR code
   - Tap notification to begin enrollment
   - Complete profile installation process

## Step-by-Step Enrollment Procedure

### Administrative Preparation

1. **Pre-Enrollment Setup**
   ```
   • Verify Jamf Now platform status
   • Check APNs certificate validity
   • Prepare device inventory spreadsheet
   • Generate enrollment codes for target devices
   ```

2. **Device Preparation**
   ```
   • Ensure devices are updated to latest iOS
   • Connect devices to stable WiFi network
   • Backup important data (if not new devices)
   • Remove any existing MDM profiles
   ```

### Detailed Enrollment Steps

**Step 1: Access Device Settings**
- Open **Settings** app on iOS device
- Navigate to **General > VPN & Device Management**
- Look for **Mobile Device Management** section

**Step 2: Initiate Enrollment**
- Tap **Enroll in Mobile Device Management**
- Choose enrollment method (code, email, or QR)
- Enter invitation code if using manual method

**Step 3: Profile Installation**
- Review MDM profile details and permissions
- Verify organization name matches expected value
- Tap **Install** to begin profile installation
- Enter device passcode when prompted

**Step 4: Complete Configuration**
- Wait for profile installation to complete
- Allow automatic configuration of settings
- Confirm enrollment success message
- Test basic MDM functionality

**Step 5: Verify Enrollment**
- Device should appear in Jamf Now inventory within 2-3 minutes
- Check device details and last check-in time
- Verify assigned blueprint is applied correctly
- Test remote management capabilities

## Enrollment Verification

### Dashboard Verification

In Jamf Now dashboard:

1. **Check Device Inventory**
   - Navigate to **Devices** section
   - Verify new device appears in list
   - Confirm device details are accurate:
     ```
     Device Name: [User-defined or auto-generated]
     Model: iPhone [model number]
     iOS Version: [current version]
     Last Check-in: [within last few minutes]
     Blueprint: [assigned profile]
     ```

2. **Verify Profile Application**
   - Click on device details
   - Check **Profiles** tab
   - Confirm assigned blueprint is installed
   - Review compliance status

### Device-Side Verification

On enrolled iOS device:

1. **Check MDM Profile**
   - Go to **Settings > General > VPN & Device Management**
   - Look for organization profile under **Device Management**
   - Profile should show "Verified" status

2. **Test Policy Enforcement**
   - Verify passcode requirements are active
   - Check if restrictions are properly applied
   - Confirm WiFi profiles are installed
   - Test app installation permissions

## Troubleshooting Enrollment Issues

### Common Enrollment Problems

| Issue | Symptoms | Solution | Prevention |
|-------|----------|----------|------------|
| Invitation code expired | "Invalid code" error | Generate new code | Complete enrollment within 15 minutes |
| Network connection failed | Enrollment hangs | Check WiFi connectivity | Use stable network connection |
| Profile installation failed | Installation error message | Remove existing profiles first | Clean device before enrollment |
| Certificate trust error | SSL/TLS warning | Update device iOS version | Keep devices updated |
| Device already managed | "Device supervised" error | Contact previous MDM admin | Verify device ownership |

### Detailed Troubleshooting Steps

**Problem: Device Won't Accept Invitation Code**

1. Verify code hasn't expired (15-minute window)
2. Check for typos in code entry
3. Ensure device has internet connectivity
4. Generate new invitation code
5. Try different enrollment method (email or QR)

**Problem: Profile Installation Fails**

1. Remove any existing MDM profiles:
   - Settings > General > VPN & Device Management
   - Tap existing profile > Remove Profile
2. Restart iOS device
3. Retry enrollment process
4. Check Jamf Now system status

**Problem: Device Not Appearing in Dashboard**

1. Wait 5-10 minutes for sync
2. Refresh Jamf Now dashboard
3. Check device internet connection
4. Verify APNs certificate validity
5. Review Jamf Now service status

**Problem: Enrollment Completes but Policies Don't Apply**

1. Force device check-in:
   - Settings > General > VPN & Device Management
   - Tap organization profile
   - Tap "More Details"
2. Wait for policy sync (up to 15 minutes)
3. Check blueprint assignment in dashboard
4. Verify profile conflicts

## Fleet Enrollment Best Practices

### Bulk Enrollment Strategy

For multiple device enrollment:

1. **Preparation Phase**
   - Create device inventory spreadsheet
   - Pre-configure all required blueprints
   - Test enrollment process on single device
   - Prepare enrollment workspace with good connectivity

2. **Execution Phase**
   - Generate multiple invitation codes in advance
   - Enroll devices in small batches (5-10 at a time)
   - Document successful enrollments immediately
   - Address failures before proceeding

3. **Verification Phase**
   - Check all devices appear in dashboard
   - Verify blueprint assignments are correct
   - Test key policies on sample devices
   - Generate enrollment report for documentation

### Enrollment Documentation

Maintain detailed records:

```
Enrollment Log Template:
Date: ___________
Device Serial: ___________
Device Name: ___________
iOS Version: ___________
Enrollment Method: ___________
Blueprint Assigned: ___________
Enrollment Time: ___________
Issues Encountered: ___________
Resolution: ___________
Enrolled By: ___________
```

## Security Considerations

### Enrollment Security

- Only use trusted networks for device enrollment
- Verify invitation codes are shared securely
- Confirm device ownership before enrollment
- Monitor enrollment activity for unauthorized attempts

### Post-Enrollment Verification

- Verify device identity matches expected user
- Check for jailbreak detection alerts
- Confirm security policies are enforced
- Test remote management capabilities

## Advanced Enrollment Options

### Apple Business Manager Integration

For enterprise environments with ABM:

1. **Automated Device Enrollment (ADE)**
   - Devices automatically enroll during setup
   - No invitation codes required
   - Supervised mode enabled by default
   - Enhanced security and restrictions

2. **Volume Purchase Program (VPP)**
   - Automatic app deployment during enrollment
   - License management integration
   - Custom app deployment capabilities

### Supervised Mode Enrollment

Benefits of supervised enrollment:

- Additional restriction capabilities
- Forced app installation
- Enhanced security policies
- Improved remote management features

## Next Steps

After successful device enrollment:

1. Configure detailed security profiles - [Profile Configuration Guide](03-profile-configuration.md)
2. Test and verify all management capabilities
3. Establish ongoing device maintenance procedures
4. Document troubleshooting procedures - [Troubleshooting Guide](04-troubleshooting.md)

## Additional Resources

- [Apple Device Enrollment Program](https://business.apple.com)
- [iOS MDM Protocol Documentation](https://developer.apple.com/documentation/devicemanagement)
- [Jamf Now Enrollment Best Practices](https://docs.jamf.com/jamf-now/)
- [Apple Configurator 2 User Guide](https://support.apple.com/apple-configurator/)