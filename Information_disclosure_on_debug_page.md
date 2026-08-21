# Information disclosure on debug page

### Goal - 

Obtain and submit the `SECRET_KEY` environment variable.

### Analysis/Exploitation -

### Using free tools

When I try to avoid using features from Burp Professional, several good free tools allow for content discovery. The one I use here is [ffuf](https://github.com/ffuf/ffuf) together with the great wordlists provided by [SecLists](https://github.com/danielmiessler/SecLists).

First, I search for common directories within the web root of the application with

```bash
ffuf -w /usr/share/wordlists/SecLists-master/Discovery/Web-Content/directory-list-2.3-small.txt -u https://0aeb000b03ce98ffc09d247e001c00a4.web-security-academy.net/FUZZ
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/30e0f4ad-9807-4e14-bd8f-f1a79b0171c5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466X6WIVMRV%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204731Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCdF87DTIvBl5KjPeHIJ3oy3Nuxz9ehYJyfo1Y%2B9L1cdAIgNsfrP%2BVNmyNfoBlNy1CxOF2uk%2BHP56yTW6oh1TwnbMgqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDEMQqCCblvtkH8pIlCrcA7HJ%2BQsGZtHU2RYJ0hunGbGDm2AUJmNAe01%2Ff%2ByEBupYGinifwOpiwr47nGfux95K5Rx2M25B4GjpFdbJhtKTd%2Fjxf5uz3McL8%2Ff1zX2fD5ZAXAWtzTiHb7V31UTxiQyjTowHRsvt%2F%2FmvVNj7SmvblhyBKSMK4GcSePZkzCT1jesUHLx1lJ6h4KCHeOWgAHs1wai5aZFhVGmu0T54Fqpq561rjBrP%2FzoK%2Fss2LognCuq9fL8YwyFAiVaxvPwLAVkUXhOlrIGk2G%2FwggebJnE1pf6NcLlq2XJi9Mg4gqhNcYg%2BHC%2FdpTKM3Y8229zaLljvyC4%2FjIIsxwqyFwtmnZB%2FG%2BfJ6pt%2FVbmcStD1zQhdA2kg%2BXda6RFghnoDktpK9tIfjzPwzhdHMMhh%2B19%2F1TEarWA2gCq7rW%2FWLaNwCaQhUER7ivi%2Bis0NlNvPKZryV2MFKDuiXacS01urspC40y%2FK5Kz6Eq9E2HL%2B7tE1xC0756Cl%2BiG7ZqVGcKXJxvU7b1VGaWtpdkBzDS9jWHiAjkD%2Bluuo65H4cexih3eLrnEpp4vFJPOZEQxd4lo2n1QPdewehkV7dmmeZMoAy0HSAxxaUvTGDDBibDTa00VZBmz5%2B3q2PxbR6fg0WVCE0OXMPzFotQGOqUB8yoVrmWX%2FC6vG5C4RNP6OGnJH6G9uEqjMwive82trSia%2FUwh%2F2BDJVEecPcWi%2FGCFimYQpBY16BlQQ2Zv4HHATtcIXaEH5T7%2F0KZ4SInulz%2BNT7d7vATz5UnP%2Fyv6qkDJqG1zLRrT0fCJ4J29r71yq%2FKubMW%2FOxZIE2cfRmQvbbmbPBw%2B7H5uKlo%2FZTWAAotxiRn4XNooo7mvD%2BDilKw15QKkjZQ&X-Amz-Signature=77f66e84b8bb7f24e06e295f62b01908892f978d6fcd41e60ed3fca757447d05&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

I can now search within this directory for common files with

```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery-content/Web-Content/common.txt  -u https://0aeb000b03ce98ffc09d247e001c00a4.web-security-academy.net/cgi-bin/FUZZ
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/37effcbf-768e-40cd-9bc5-8544f17e3ef0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466X6WIVMRV%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204731Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCdF87DTIvBl5KjPeHIJ3oy3Nuxz9ehYJyfo1Y%2B9L1cdAIgNsfrP%2BVNmyNfoBlNy1CxOF2uk%2BHP56yTW6oh1TwnbMgqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDEMQqCCblvtkH8pIlCrcA7HJ%2BQsGZtHU2RYJ0hunGbGDm2AUJmNAe01%2Ff%2ByEBupYGinifwOpiwr47nGfux95K5Rx2M25B4GjpFdbJhtKTd%2Fjxf5uz3McL8%2Ff1zX2fD5ZAXAWtzTiHb7V31UTxiQyjTowHRsvt%2F%2FmvVNj7SmvblhyBKSMK4GcSePZkzCT1jesUHLx1lJ6h4KCHeOWgAHs1wai5aZFhVGmu0T54Fqpq561rjBrP%2FzoK%2Fss2LognCuq9fL8YwyFAiVaxvPwLAVkUXhOlrIGk2G%2FwggebJnE1pf6NcLlq2XJi9Mg4gqhNcYg%2BHC%2FdpTKM3Y8229zaLljvyC4%2FjIIsxwqyFwtmnZB%2FG%2BfJ6pt%2FVbmcStD1zQhdA2kg%2BXda6RFghnoDktpK9tIfjzPwzhdHMMhh%2B19%2F1TEarWA2gCq7rW%2FWLaNwCaQhUER7ivi%2Bis0NlNvPKZryV2MFKDuiXacS01urspC40y%2FK5Kz6Eq9E2HL%2B7tE1xC0756Cl%2BiG7ZqVGcKXJxvU7b1VGaWtpdkBzDS9jWHiAjkD%2Bluuo65H4cexih3eLrnEpp4vFJPOZEQxd4lo2n1QPdewehkV7dmmeZMoAy0HSAxxaUvTGDDBibDTa00VZBmz5%2B3q2PxbR6fg0WVCE0OXMPzFotQGOqUB8yoVrmWX%2FC6vG5C4RNP6OGnJH6G9uEqjMwive82trSia%2FUwh%2F2BDJVEecPcWi%2FGCFimYQpBY16BlQQ2Zv4HHATtcIXaEH5T7%2F0KZ4SInulz%2BNT7d7vATz5UnP%2Fyv6qkDJqG1zLRrT0fCJ4J29r71yq%2FKubMW%2FOxZIE2cfRmQvbbmbPBw%2B7H5uKlo%2FZTWAAotxiRn4XNooo7mvD%2BDilKw15QKkjZQ&X-Amz-Signature=1a0b2f4006eb87ca2f28a5e4427d4911c939f2302a662ca82eeebc5ef0ee4db2&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Using Burp Professional

Go to the "Target" > "Site Map" tab. Right-click on the top-level entry for the lab and select "Engagement tools" > "Find comments". Notice that the home page contains an HTML comment that contains a link called "Debug". This points to `/cgi-bin/phpinfo.php`.

or Use the default options and start the content discovery. Burp quickly shows the `phpinfo.php` file in the site map:

Opening this file in the browser and scrolling through the content shows the answer:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ebc3c145-2e85-4bdd-86c9-badcaff70ec6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466X6WIVMRV%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204731Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCdF87DTIvBl5KjPeHIJ3oy3Nuxz9ehYJyfo1Y%2B9L1cdAIgNsfrP%2BVNmyNfoBlNy1CxOF2uk%2BHP56yTW6oh1TwnbMgqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDEMQqCCblvtkH8pIlCrcA7HJ%2BQsGZtHU2RYJ0hunGbGDm2AUJmNAe01%2Ff%2ByEBupYGinifwOpiwr47nGfux95K5Rx2M25B4GjpFdbJhtKTd%2Fjxf5uz3McL8%2Ff1zX2fD5ZAXAWtzTiHb7V31UTxiQyjTowHRsvt%2F%2FmvVNj7SmvblhyBKSMK4GcSePZkzCT1jesUHLx1lJ6h4KCHeOWgAHs1wai5aZFhVGmu0T54Fqpq561rjBrP%2FzoK%2Fss2LognCuq9fL8YwyFAiVaxvPwLAVkUXhOlrIGk2G%2FwggebJnE1pf6NcLlq2XJi9Mg4gqhNcYg%2BHC%2FdpTKM3Y8229zaLljvyC4%2FjIIsxwqyFwtmnZB%2FG%2BfJ6pt%2FVbmcStD1zQhdA2kg%2BXda6RFghnoDktpK9tIfjzPwzhdHMMhh%2B19%2F1TEarWA2gCq7rW%2FWLaNwCaQhUER7ivi%2Bis0NlNvPKZryV2MFKDuiXacS01urspC40y%2FK5Kz6Eq9E2HL%2B7tE1xC0756Cl%2BiG7ZqVGcKXJxvU7b1VGaWtpdkBzDS9jWHiAjkD%2Bluuo65H4cexih3eLrnEpp4vFJPOZEQxd4lo2n1QPdewehkV7dmmeZMoAy0HSAxxaUvTGDDBibDTa00VZBmz5%2B3q2PxbR6fg0WVCE0OXMPzFotQGOqUB8yoVrmWX%2FC6vG5C4RNP6OGnJH6G9uEqjMwive82trSia%2FUwh%2F2BDJVEecPcWi%2FGCFimYQpBY16BlQQ2Zv4HHATtcIXaEH5T7%2F0KZ4SInulz%2BNT7d7vATz5UnP%2Fyv6qkDJqG1zLRrT0fCJ4J29r71yq%2FKubMW%2FOxZIE2cfRmQvbbmbPBw%2B7H5uKlo%2FZTWAAotxiRn4XNooo7mvD%2BDilKw15QKkjZQ&X-Amz-Signature=ea4ca324f76b1184d8349218c8b6dff42dd1409226b80df212c5267e09cf53ef&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

