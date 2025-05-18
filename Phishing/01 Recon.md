# 1.2 Recon

## Lab Prep
### Downloads
- Virtual Box: https://www.virtualbox.org/wiki/Downloads/
- Kali Linux VM: https://www.kali.org/downloads/
- [Buscador Linux VM](https://inteltechniques.com/buscador/):

  It has many built-in modules for online investigators and it was developed by David Westcott and Michael Bazzell of
Intel Techniques. That's where it can be found. It's got a ton of built-in tools like a custom Firefox browser with built-in add-ons, Tor browser, Google Earth Pro, which is good if you wanted to actually look at the company you
were trying to do OSINT on, Maltego, recon-NG and the harvester of course, and many more.

# 1.3 The Harvester

## What is The Harvester?
Built in Kali Linux package that can be used to gather email addresses, subdomains, host names, employee names, etc.
- It uses public sources including:
  - Search engines
  - Shodan database

## Using The Harvester
- Basic commands
  - `root@kali:~# theHarvester
    - Lists all of the harvester options
  - Common tags or switches
    - `-d`: domain to search
    - `-l`: limit the number of results
    - `-b`: data source
  - Example command
    - `root@kali:~# theHarvester -d google.com -l 500 -b google`

# 1.4 Recon-NG

## What is Recon-NG?

Full featured web recon framework, used in similar fashion to Metasploit
- Recon-ng was written in python, making it very easy to use and even contribute to
- Has many modules built in including
  - Recon modules
  - Reporting modules
  - Exploitation modules
  - Discovery modules
 
## What are modules?

Modules in Recon-NG are scripts that will perform a certain action, just like in Metasploit.

## Using Recon-NG

Recon-NG is used in a very similar fashion to the Metasploit framework.
- Launched by issuing the recon-ng command
  - `root@kali:~#recon-ng`
- `root@kali:~# recon-ng --help`
  - This will display usage options along with arguments
- Basic command structure
  - Use module
    - `[recon-ng][default] > use`
  - Set source
    - `[recon-ng][default][module] > set SOURCE`
    - `SOURCE =>`
  - Run
    - `[recon-ng][default][module] > run`

# 1.5 Using Recon-NG

## Wordplaces - What are they?
- `[recon-ng][default] >` What are workspaces? When you log into Recon-NG, you will see the prompt Recon-NG and then in brackets default, that is the default workspaces. Workspaces are used to organize any information that you gather and make it easy to keep things separate.

## Lab
1. `[recon-ng][default] > workspaces create lab`
2. `[recon-ng][lab] > db insert domains` then add `google.com`
3. `[recon-ng][lab] > db insert companies` then add `Google`
4. `[recon-ng][lab] > show domains`
5. `[recon-ng][lab] > show companies`

Note:
To change from one workspace to another: `[recon-ng][default] > workspaces load workspace_name`

  
# 1.6 Scanning With Recon-NG
1. `[recon-ng][lab] > marketplace search whois` to find the whois module
2. `[recon-ng][lab] > marketplace install whois_pocs`
3. `[recon-ng][lab] > modules load whois`
4. `[recon-ng][lab][whois_pocs] > info`
5. `[recon-ng][lab][whois_pocs] > options set SOURCE google.com`
6. `[recon-ng][lab][whois_pocs] > run`
7. `[recon-ng][lab][whois_pocs] > show contacts`
8. `[recon-ng][lab][whois_pocs] > back`
9. `[recon-ng][lab] > marketplace search reporting` to find reporting tool to export results 
10. `[recon-ng][lab] > marketplace install html`
11. `[recon-ng][lab] > modules load html`
12. `[recon-ng][lab][html] > info`
13. `[recon-ng][lab][html] > options set CREATOR <creator_name>`
14. `[recon-ng][lab][html] > options set CUSTOMER <customer_name>`
15. `[recon-ng][lab][html] > run`
 
