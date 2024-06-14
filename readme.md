# Pre-requisites:
__1. Install rdp client on mac__
[here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect-rdp.html)

__2. Create your EC2 Instance__
- Choose windows server Base AMI
- Create an EC2 i3.metal instance
- Ensure security group allow rdp to port 3389

__5. Go to connect to created ec2 instance__

__6. Choose administrator as username__

__7. Go to get password and paste in the private key used to create ec2__
![ec2-connect](/img/ec2-connect.png)

__8. Click decrypt password__

__9. Copy the password__

__10. Go to the rdp tool on your mac__

__11. Paste in the public dns and username and password to the keychain and click connect__
  - Username: Administrator
  - Password: the decrypted password

__12. Follow this [guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10) to install HyperV on windows server__

__13. Make sure to check the box to allow server to restart after installation__

__14. Install wsl2 on the server:__
```
wsl.exe --install --no-distribution

OR

wsl --install
```
THEN
```
wsl --set-default-version 2
```

__15. Restart the server and wait for server to restart -> reconnect to VM__

__16. Download docker desktop__

__17. Right click docker desktop and run as admin__

__18. Wait for docker engine to start__

__19. Go to command prompt and run as admin__

__20. Type "Windows Powershell" in the Run dialog.__

__21. Press Ctrl + Shift + Enter to open Windows Powershell as an administrator.__
- If prompted by User Account Control (UAC), click "Yes" to allow the application to make changes to your device.
- Run `docker ps -a` to verify if the gateway container is running

# Execution:
__1. Go to kong konnect and go to gateway manager -> Data Plane nodes__

__2. Click create a data plane node and choose windows__
![DP](/img/dp.png)

__3. Copy the docker run command__

__4. Open windows powershell as admin__

__5. Paste it into the windows powershell on windows server (make sure to run as admin)__
  - Run `docker ps -a` to verify if the gateway container is running

__6. Head back to Konnect to verify the installation is complete__

__7. Create a service and route and test the connectivity to data plane via Edge browser__
  - Service: "https://httpbin.org/anything"
  - Route: "/mock" - leave rest as default to allow GET requests


# Additional Configuration
__1. Go to "Windows Defender Firewall" and click "advanced settings"__

__2. Click "Inbound Rules" -> "New Rule"__
![windows](/img/windows_defender.png)

__3. Follow the wizard when creating new rule__
- Click port
- allow specific local ports: 8000
- Allow the connection
- Allow the rule on domain, private and public
![config](/img/windows_defender_config.png)
- Name: "kong"

__4. Go to insomnia or try from local laptop browser to access the ec2 public domain and see if it's a success 200 response__
![insomnia](/img/insomnia.png)
