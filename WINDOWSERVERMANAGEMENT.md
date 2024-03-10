# Change windows admin server password
    - Signout 
    - press <Ctrl>+<Alt>+Del 
    - Switch User
    - Go to Admintrator
    - SignIn
    - Go to settings > Accounts > Sign-in options > password

# Enabling Active Directory - like root path '/'
    - Open Server Manager
    - On navigation > manage > add roles and feautres wizard
    - Click 'Next'
    - In Server Roles >  choose 2 options followed by AD
    - Install All

## Domain Controller
    - Go to notification
    - click promote this server to domain controller
    - On Deployment configuration
    - Add a new forest > specifiy domain name
    - Click 'Next'

## Users Group Policy 
    - Tools > Group Policy Mangement
    - Our Forest > domains > <forest>
    -  Right click on <forest>
    - New organization unit: test
    - <test> Right click > create a user GPO
    - Double click > settings > computer configuration 
    - right click > edit 
    - Computer configuration > windows installer > prohibit user install > enable 

## Create users in AD
    - Go to Tools
    - Active Directory users and computers
    - Right click on custom <forest> name
    - Right Click > Add > New > User/Computer

## File Server
    - Go to manage
    - Add roles nadn features wizard
    - At server Roles > choose file services tools
    - Enable files server resource manager tools
    - Install

## SMB confi
    - Sidebar: File and Storage Sevices > Shares
    - Dropdown 'Task' > new shares > share location > create custom
    - right click on new share > config quota (limits)

## DHCP config
    - Go to mangae > add roles and features wizard
    - Server selection > choose DHCP server > next > install
    - Notification: post-deployment configuration
