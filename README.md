<p align="center">

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/2bf565ef-6528-49fa-bc3b-e103c2a7ac2f)


</p>

<h1>Building Intuition for DNS</h1>
In this tutorial, We'll simplify DNS (Domain Name System) and easily understand it. We'll explore DNS A-Records, Creating and Deleting Records, CNAME Records, and Root Hints.<br />

>**Note***
>_The following uses material created in the previous demonstration, ["On-premises Active Directory Deployed in the Cloud (Azure)"](https://github.com/marklibador/AD-Configuration)._

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Connection (RDP)
- Command Line
- Microsoft Azure Directory
- Domain Name System (DNS)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)

<h2>List of Prerequisites</h2>

- Client VM joined to your Domain
- MicroSoft Azure w/ two pre-configured VM's
- Client-01 and DC-1 Virtual Machines
- MircoSoft Active Directory installed in DC-1
- DC-1 promoted to a Domain Controller

<h2>Actions and Observations</h2>

<h3>A-Record Exercise</h3>

>A-Records are mappings from hostnames to IP Addresses

- We'll take a look at DNS A-Records 
- Log into DC-1 as **mydomain.com\jane_admin**
- Log into Client-01 as **mydomain.com\jane_admin**
- Open `Command Prompt` as administrator on Client-01
- Type **ping mainframe**
- Notice that it fails.

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/65164576-efd0-4be1-a458-b9ba3321061d)


- There is no DNS Record
- Open `Tools` on DC-1 
- Click `DNS`

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/4f7ba249-77b6-49d0-90fb-e32f8bb8be3f)

- This will open `DNS Manager`
- Expand `DC-1`
- Expand `Forward Lookup Zones`
- Expand `mydomain.com`
- Right Click
- Select `New Host (A or AAAA)...`

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/702f70db-edaf-4847-b97a-8fca34dbd13c)

- Create A-Record named **mainframe**
- Set `IP Address` to **10.0.0.4**
- Click `Add Host`

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/752e56ee-8268-42fc-86f8-93266766fbfd)

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/1e3ef3dd-fd4c-4089-ba37-8ac5e0472b3d)

- Open Client-01 Virtual Machine
- Type **ping mainframe**
- Now you see that it works

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/2cca91be-5694-42df-8a60-d046dc5ad15c)

<h3>Local DNS Cache Exercise</h3>

- Open DC-1
- Right Click `mainframe`
- Select `Properties`

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/7abd0b4e-4e22-4792-91cf-52e1c29ed6bc)

- Change `IP Address` to **8.8.8.8**
- Click `Apply`
- Click `OK`

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/d3c65d72-403b-4b38-8a62-59d5f1c3c811)

- Return to Client-01
- In `Command Prompt` **ping mainframe**
- Notice it continues to ping the old address

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/08fb07a4-13a4-4a43-be14-021f830af9e8)

- Check the local DNS Cache using **ipconfig /displaydns**

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/3e855107-317b-4599-9fac-76c0bab5d039)

- Flush the DNS Cache using **ipconfig /flushdns**
- Observe the Cache is now empty

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/71e90d84-321b-4d62-9e34-6635746fa2a9)

- Type **ping mainframe**
- Observe the new IP Address shown

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/7c810328-ecab-4fb5-89f0-3c631e5b0aa6)

<h3>CNAME Record Exercise</h3>

>_A DNS CNAME record provides an alias for another domain._


- Return to DC-1
- Right click and Select `New Alias (CNAME)...`

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/083b6c9b-6543-421c-ab5a-5d699c19556f)

- Set `Alias name` to **search**
- Set `Fully qualified domain name` to **www.google.com**
- Select `OK`

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/647d0220-f27d-4c1a-8139-e3c88d944bdb)

- Return to Client-01
- Type **ping search**
- Observe the results of CNAME Records

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/79fa1b1e-6ff2-4d5c-980d-07852d0ec310)

- Type **nslookup mainframe** to query mainframe

![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/36c10303-75a9-4670-a25b-2693a9d67bfa)

- Type **nslookup search** to query search
  
![image](https://github.com/CarlosAlvarado0718/DNS-Intuition/assets/140138198/9673db75-615e-4a2e-9230-8c4805c50857)

<h1>ALL DONE!!! CONGRATS!!!</h1>
<h3>Now you have a better understanding of DNS, A-Records, DNS caching and CNAME Records. </h3>
