# MiniKube
Minikube is essentially a single-node Kubernetes cluster where both the master and worker processes run on the same machine. It is ideal for quickly trying out or testing Kubernetes features in a local environment.

### Pre-requisites

- 2 CPUs or more
- 2 GB of free memory
- 20 GB of free disk space.
- Internet Connection.
- Container or virtual machine manager such as: Docker, QEMU, Hyperkit, Hyper-V, KVM, Parallels, podman, virtualBox, or VMware Fusion/Workstation.


### Stesp to Install

In this example, I will be using Docker since it is already set up on my system. </br>
Below is the version of Docker that I am currently using.

```bash
docker version
```

![Docker Version](https://github.com/user-attachments/assets/01ef33ef-8d6d-4b12-8718-2b78644f4150)

With Docker already set up, I can now proceed to the next step: installing Minikube.

For this, Minikube can be installed in two ways:  
- Installer
- Using PowerShell  

I will proceed with the PowerShell installation.  
Run the belwo command to create a folder named "minikube" in your C drive using PowerShell

```bash
New-Item -Path 'c:\' -Name 'minikube' -ItemType Directory -Force
```

Below command will downloads the latest version of the Minikube executable for Windows and the file will be saved as minikube.exe in the C:\minikube directory.

```bash
Invoke-WebRequest -OutFile 'c:\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing
```

![image](https://github.com/user-attachments/assets/894a7c27-ff0d-4600-9c98-9226ca0ae5c3)

After executong the command, it will download required packages from GitHub.  You can also see the directory created under C drive.  

![image](https://github.com/user-attachments/assets/e54c94a3-cd6e-459f-999a-ede61e9136e3)

Once it is downloaded, we can set up the pah for MiniKube.  
Execute the below command.   This script checks if the C:\minikube directory is already part of your system's Path. If it isn't, the script adds it to the Path so that Minikube commands can be run globally from any terminal session.  

```bash
$oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine)
if ($oldPath.Split(';') -inotcontains 'C:\minikube'){
  [Environment]::SetEnvironmentVariable('Path', $('{0};C:\minikube' -f $oldPath), [EnvironmentVariableTarget]::Machine)
}
```

![image](https://github.com/user-attachments/assets/e9790c60-d186-4f1d-9f9e-9a2b7d0f9ce8)

Run the command `minikube`.  Close the current PowerShell window and reopen another one to run the command.

```bash
minikube
```

![image](https://github.com/user-attachments/assets/03b216a2-31b1-40c1-9106-7210f07da990)

As shown in the screenshot above, I encountered an error after executing the `minikube` command.  
Below is the Error message that I got.  

`
10296 main.go:291] Unable to resolve the current Docker CLI context "default": context "default": context not found: open C:\Users\Roshni\.docker\contexts\meta\37a8eec1ce19687d132fe29051dca629d164e2c4958ba141d5f4133a33f0688f\meta.json: The system cannot find the path specified.
minikube provisions and manages local Kubernetes clusters optimized for development workflows.
`

The error message suggests that MiniKube is having trouble resolving the Docker CLI context, specifically the "Default" context.
This issue can occure if the Docker context configuration is missing or corrupted.  

Verify the Docker installation to see if the Docker is properly installed.  

```bash
docker version
docker ps
```
![image](https://github.com/user-attachments/assets/3146db83-1532-4062-bc16-2d4354463191)  

I reset the Docker context to default to see if it resolves the issue.

```bash
docker context use default
```
![image](https://github.com/user-attachments/assets/91e80b34-a9c7-41eb-a6f2-080dde7faf3a)  

Lets' execute the `minikube` command to see if it worked.  

![image](https://github.com/user-attachments/assets/9d9c2138-aab7-427b-9133-00492b6ba9a5)  

From the above screenshot you can see the error is now gone. So resetting Docker context to default worked on me.  












