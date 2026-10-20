# Week 3 - EC2 PropertyLite Deployment

## 1. Launch the EC2 instance

In the AWS Console, open **EC2 → Instances → Launch instance**.

Settings:

- Name: `property-api-01`
- AMI: Amazon Linux 2023
- Instance type: `t2.micro` or `t3.micro`, if Free Tier eligible
- Key pair: create or select `training-key`, RSA, `.pem`
- Security group inbound rules:
  - SSH, TCP 22, source **My IP**
  - Custom TCP, port 8080, source **Anywhere** for this lab

Port 8080 is the port used by PropertyLite. SSH should remain restricted to my current IP address.

## 2. Add the bootstrap script

Under **Advanced details → User data**, paste the contents of `bootstrap.sh` from this folder. The script installs Python and Flask, creates the application files under `/opt/property-api`, and starts the application on port 8080.

Launch the instance and wait until its state is **Running**. Copy its public IPv4 address.

## 3. Connect to the instance

From PowerShell, use the downloaded key and public IP:

```powershell
ssh -i ".\training-key.pem" ec2-user@<PUBLIC_IP>
```

## 4. Verify PropertyLite from my computer

Run these commands in a local PowerShell window, not inside the SSH session:

```powershell
curl.exe http://<PUBLIC_IP>:8080/health
curl.exe http://<PUBLIC_IP>:8080/properties
curl.exe http://<PUBLIC_IP>:8080/properties/R100234
```

Expected results include:

- `/health` returns `{"status":"ok"}`.
- `/properties` returns the sample property records.
- `/properties/R100234` returns the Sacramento listing.

## 5. Create an EBS snapshot

1. Open **EC2 → Volumes**.
2. Select the root volume attached to `property-api-01`.
3. Choose **Actions → Create snapshot**.
4. Wait until the snapshot status is **Completed**.

An EBS snapshot is a point in time backup of the volume. A new EBS volume can be created from the snapshot later, usually in the same AWS Region.

## 6. Clean up resources

After capturing the evidence, terminate the instance:

1. Open **EC2 → Instances**.
2. Select `property-api-01`.
3. Choose **Instance state → Terminate instance**.
4. Confirm that the root volume was deleted if it is no longer needed.
5. Delete the training key pair and security group only if they are not needed for later labs.
6. Delete the EBS snapshot if it is not needed; snapshots can continue generating storage charges.

## What I learned

EC2 provides virtual servers that I configure and manage. The security group acts as a stateful firewall attached to the instance. I restricted SSH to my IP address and opened port 8080 so the PropertyLite API could be reached for this lab. User data allowed the instance to install dependencies and start the application automatically during boot. EBS provides persistent block storage, and snapshots provide point-in-time backups of EBS volumes.