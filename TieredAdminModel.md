# Tiered Admin Model Documentation

This document outlines the Organizational Units (OUs), groups, and permissions created by the `invoke-TieredAdminModel.ps1` script.

## Root OU

The script creates a root OU named `Admin` to contain the entire tiered admin model.

## Tier 0

### OUs

- **Tier 0**: Main container for Tier 0 resources.
  - **Computers**: Contains Tier 0 servers.
    - **Identity**: For identity-related servers.
    - **PKI**: For Public Key Infrastructure servers.
    - **PAW**: For Privileged Access Workstations for Tier 0 admins.
  - **Groups**: Contains Tier 0 groups.
    - **Permission Groups**: Groups that grant specific permissions.
      - **Time Based Access**: For temporary permissions.
    - **Role Groups**: Groups that represent job roles.
  - **Entra Managed**: For cloud objects managed in Entra ID.
  - **Admins**: For Tier 0 administrator accounts.
  - **Accounts**: For user and service accounts for Tier 0 resources.
    - **Test Accounts**
    - **Service Accounts**
    - **Shared Accounts**
    - **Terminated**

### Groups

#### Permission Groups

- **PermADT0ComputersOU**: Manage objects in T0 computer OUs.
- **PermADT0ComputersGPOs**: Manage GPOs linked to T0 computers OU.
- **PermADT0ComputerLocalAdmin**: Local admins on T0 machines.
- **PermADT0ComputerServerOperator**: Server operators on T0 machines.
- **PermADT0GroupsOU**: Manage T0 security groups.
- **PermADT0AccountsOU**: Manage T0 accounts.
- **PermADT0AdminsOU**: Manage T0 admin accounts.
- **TempPermDomainAdmins**: Temporary Domain Admin access.

#### Role Groups

- **RoleT0InfraAdmins**: Infrastructure team admin accounts.
- **RoleT0IAMProductConnectors**: IAM product service accounts for T0 access.

### Permissions

- **PermADT0ComputersOU**: Granted `CreateDeleteManageComputerObjects` on `Tier 0\Computers` OU.
- **PermADT0GroupsOU**: Granted `CreateDeleteManageGroupObjects` on `Tier 0\Groups` OU.
- **PermADT0AdminsOU**: Granted `CreateDeleteManageUserObjects` on `Tier 0\Admins` OU.
- **PermADT0AccountsOU**: Granted `CreateDeleteManageUserObjects` on `Tier 0\Accounts` OU.

### Role Assignments

- **RoleT0InfraAdmins**:
  - `PermADT0ComputersOU`
  - `PermADT0AccountsOU`
  - `PermADT0groupsOU`
  - `PermADT1ComputersOU`
  - `PermADT1AccountsOU`
  - `PermADT1AdminsOU`
  - `RoleT0IAMProductConnectors`
  - `PermADT2ComputersOU`
  - `PermADT2AccountsOU`
  - `PermADT2AdminsOU`
  - `PermADT2groupsOU`
- **RoleT0IAMProductConnectors**:
  - `Pre-Windows 2000 Compatible Access`
  - `PermADT0AccountsOU`
  - `PermADT0groupsOU`
  - `PermADT1AccountsOU`
  - `PermADT1AdminsOU`
  - `PermADT1groupsOU`
  - `PermADT2AccountsOU`
  - `PermADT2AdminsOU`
  - `PermADT2groupsOU`

## Tier 1

### OUs

- **Tier 1**: Main container for Tier 1 resources.
  - **Computers**: Contains application servers.
    - **PAW**: For Privileged Access Workstations used by T1 admins.
  - **Groups**: Contains Tier 1 groups.
    - **Permission Groups**: For T0 and T1 accounts/roles/computers.
      - **Time Based Access**: For temporary permissions.
    - **Role Groups**: For job roles and tasks.
  - **Admins**: For T1 admin accounts.
  - **Accounts**: For user and service accounts for Tier 1 resources.
    - **Test Accounts**
    - **Shared Accounts**
    - **Service accounts**
      - **SyncedToEntra**

### Groups

#### Permission Groups

- **PermADT1ComputersOU**: Manage T1 computer OUs.
- **PermADT1ComputersGPOs**: Manage GPOs linked to T1 OUs.
- **PermADT1ComputersLocalAdmin**: Local admin on T1 computers.
- **PermADT1GroupsOU**: Manage T1 security groups.
- **PermADT1AccountsOU**: Manage T1 accounts.
- **PermADT1AdminsOU**: Manage T1 admins.
- **PermApp1Admins**: Admins on app 1.
- **PermApp2Admins**: Admins on app 2.
- **PermApp1DB_SYSAdmin**: DBAs on App1.
- **PermSaaS1Admins**: SaaS app 1 admins.
- **PermSaaS2Admins**: SaaS app 2 admins.
- **PermFilesChocoRepoT1_RO**: Read-only access to Choco repo.
- **PermFilesChocoRepoT1_RW**: Read-write access to Choco repo.
- **PermFilesDeptC**: Access to department C files.

#### Role Groups

- **RoleT1AdminInfoSecApps**: Infosec team admin accounts.
- **RoleT1AdminBusinessApps**: Business apps team admin accounts.
- **RoleT1ITServerSupportAdmins**: Server support team admin accounts.
- **RoleT1DomainJoiners**: Automation accounts for domain joining.

### Permissions

- **PermADT1ComputersOU**: Granted `CreateDeleteManageComputerObjects` on `Tier 1\Computers` OU.
- **PermADT1GroupsOU**: Granted `CreateDeleteManageGroupObjects` on `Tier 1\Groups` OU.
- **PermADT1AdminsOU**: Granted `CreateDeleteManageUserObjects` on `Tier 1\Admins` OU.
- **PermADT1AccountsOU**: Granted `CreateDeleteManageUserObjects` on `Tier 1\Accounts` OU.

### Role Assignments

- **RoleT1ITServerSupportAdmins**:
  - `PermADT1ComputersOU`
  - `PermADT1AccountsOU`
  - `PermADT1AdminsOU`
  - `PermADT1groupsOU`
  - `PermADT2ComputersOU`
  - `PermADT2AccountsOU`
  - `PermADT2AdminsOU`
  - `PermADT2groupsOU`
  - `PermFilesChocoRepoT1_RW`
- **Domain Users**: `PermFilesChocoRepoT1_RO`
- **Domain Computers**: `PermFilesChocoRepoT1_RO`
- **RoleT1DomainJoiners**:
  - `PermADT1ComputersOU`
  - `PermADT2ComputersOU`
- **RoleT1AdminBusinessApps**:
  - `PermSaaS1Admins`
  - `PermSaaS2Admins`
  - `PermApp1Admins`
  - `PermApp2Admins`

## Tier 2

### OUs

- **Tier 2**: Main container for Tier 2 resources.
  - **Computers**: Contains user desktops.
    - **MultisessionHosts**
    - **Win10**: Default location for new Windows 10 machines.
      - **US**: Machines with US policies.
        - **NewYork**
        - **Miami**
      - **UK**: Machines with UK policies.
        - **Northampton**
        - **Luton**
        - **Slough**
      - **FR**: Machines with French policies.
        - **LesGets**
        - **Meribel**
      - **CH**: Machines with Swiss policies.
        - **Verbier**
      - **AT**: Machines with Austrian policies.
        - **Mooserwirt**
  - **Groups**: Contains Tier 2 groups.
    - **Permission Groups**: For end-user resources.
      - **Synced to Entra**
      - **Time Based Access**
    - **Role Groups**: For job roles and tasks.
  - **Admins**: For T2 admin accounts.
  - **Accounts**: For T2 user accounts.
    - **Service Accounts**
    - **Test Accounts**
    - **Shared Accounts**
    - **Terminated**

### Groups

#### Permission Groups

- **PermADT2ComputersOU**: Manage objects in T2 computer OUs.
- **PermADT2ComputersGPOs**: Manage GPOs linked to T2 OUs.
- **PermADT2ComputersLocalAdmin**: Local admin on T2 computers.
- **PermADT2GroupsOU**: Manage T2 security groups.
- **PermADT2AdminsOU**: Manage T2 admin accounts.
- **PermADT2AccountsOU**: Manage T2 accounts.
- **TempPermADT2Accounts**: Temporary management of T2 accounts.
- **PermFiles_ProjectA_RW**: Read-write access to Project A files.
- **PermFiles_ProjectB_RW**: Read-write access to Project B files.
- **PermFilesDeptC_RW**: Read-write access to Department C files.
- **PermFilesChocoRepoT2_RO**: Read-only access to Choco repo.
- **PermFilesChocoRepoT2_RW**: Read-write access to Choco repo.
- **PermSaas1**: Access to SaaS 1.
- **PermSaaS2**: Access to SaaS 2.
- **PermDesktopAppE**: Access to Desktop App E.

#### Role Groups

- **RoleHR**: Role for the HR team.
- **RoleOperations**: Role for the Operations team.
- **RoleFinance**: Role for the Finance team.
- **RoleStaff**: Role for all full-time staff.
- **RoleContractors**: Role for contractors.
- **RoleInterns**: Role for interns.

### Permissions

- **PermADT2ComputersOU**: Granted `CreateDeleteManageComputerObjects` on `Tier 2\Computers` OU.
- **PermADT2GroupsOU**: Granted `CreateDeleteManageGroupObjects` on `Tier 2\Groups` OU.
- **PermADT2AdminsOU**: Granted `CreateDeleteManageUserObjects` on `Tier 2\Admins` OU.
- **PermADT2AccountsOU**: Granted `CreateDeleteManageUserObjects` on `Tier 2\Accounts` OU.

### Role Assignments

- **RoleHR**: `PermFilesDeptC_RW`

> Automatic Created by Gemini
