# VM Deployment Plan

## Project Scope
Deploy a secure Linux virtual machine in Azure for cybersecurity monitoring and hardening demonstration.

## VM Specifications

### Basic Configuration
- **Operating System:** Ubuntu 22.04 LTS (Latest stable release)
- **VM Size:** Standard_B1s (1 vCPU, 1 GB RAM)
- **Storage:** 30 GB Premium SSD (encrypted)
- **Region:** East US (or closest to your location)

### Network Configuration
- **Resource Group:** `rg-cybersec-lab`
- **Virtual Network:** `vnet-cybersec-lab` (10.0.0.0/16)
- **Subnet:** `subnet-secure-vms` (10.0.1.0/24)
- **Public IP:** Dynamic (for SSH access)
- **Private IP:** Dynamic within subnet range

### Security Configuration

**Network Security Group (NSG) Rules:**
| Priority | Name | Port | Protocol | Source | Action |
|----------|------|------|----------|---------|--------|
| 1000 | Allow-SSH | 22 | TCP | Your IP only | Allow |
| 1100 | Allow-HTTP | 80 | TCP | Internet | Allow |
| 1200 | Allow-HTTPS | 443 | TCP | Internet | Allow |
| 4096 | Deny-All | Any | Any | Any | Deny |

**Authentication:**
- SSH key-based authentication only
- No password authentication
- Custom SSH port (will change from 22 during hardening)

**Management Features:**
- Auto-shutdown: 8 PM daily (cost optimization)
- Boot diagnostics: Enabled
- Azure monitoring: Enabled

## Security Objectives

### Initial Security Posture
1. **Network Isolation:** VM deployed in dedicated subnet with restrictive NSG
2. **Access Control:** SSH key authentication only, limited source IPs
3. **Encryption:** Disk encryption enabled at deployment
4. **Monitoring:** Basic Azure monitoring and logging enabled

### Post-Deployment Hardening Goals
1. **System Updates:** All packages updated to latest versions
2. **SSH Hardening:** Custom port, key-only auth, connection limits
3. **Firewall:** UFW configured with minimal required ports
4. **Services:** Disable unnecessary services, harden remaining ones
5. **User Security:** Disable root login, configure sudo properly
6. **File System:** Secure permissions, mount options
7. **Logging:** Enhanced logging for security events

## Pre-Deployment Checklist
- [ ] Azure Student account activated and verified
- [ ] SSH key pair generated and ready
- [ ] Source IP address identified for NSG rules
- [ ] Resource naming convention defined
- [ ] Auto-shutdown schedule configured
- [ ] Documentation structure prepared

## Risk Assessment

### Identified Risks
1. **Public IP Exposure:** VM will have public IP for SSH access
   - **Mitigation:** Restrictive NSG rules, SSH key auth only
2. **Cost Overrun:** Potential charges if resources left running
   - **Mitigation:** Auto-shutdown configured, regular monitoring
3. **Accidental Lockout:** SSH configuration errors could prevent access
   - **Mitigation:** Test configurations incrementally, keep Azure console access

### Security Considerations
- VM will be internet-accessible for learning purposes
- All hardening will be documented and reversible
- No sensitive data will be stored on the VM
- Regular security assessments will be performed

## Success Criteria
1. **Functionality:** VM deployed and accessible via SSH
2. **Security:** All planned security controls implemented and tested
3. **Monitoring:** SIEM solution collecting and analyzing logs
4. **Documentation:** Complete step-by-step documentation with screenshots
5. **Compliance:** Basic CIS benchmark controls implemented

## Next Steps
1. Execute VM deployment following documented procedures
2. Capture screenshots of each configuration step
3. Perform initial baseline security assessment
4. Begin systematic hardening process

---
**Deployment Date:** [To be filled]  
**Deployed By:** [Your name]  
**Status:** Ready for deployment