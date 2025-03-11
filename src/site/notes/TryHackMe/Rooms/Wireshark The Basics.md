---
{"dg-publish":true,"permalink":"/try-hack-me/rooms/wireshark-the-basics/","created":"2024-10-25T15:46:36.380-04:00","updated":"2025-03-11T00:32:59.565-04:00"}
---

# Task 2 - Tool Overview

| Toolbar                       | Menus for packet sniffing and processing, including filtering, sorting, summarising, exporting and merging. |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Display Filter Bar            | Main query and filtering section.                                                                           |
| Recent Files                  | List of the recently investigated files.                                                                    |
| Capture Filter and Interfaces | Capture filters and available sniffing points (network interfaces).                                         |
| Status Bar                    | Tool status, profile and numeric packet information.                                                        |
| Packet List                   | Summary of each packet. You can click on the list to choose a packet for further investigation.             |
| Packet Details Pane           | Detailed protocol breakdown of the selected packet.                                                         |
| Packet Bytes Pane             | Hex and decoded ASCII representation of the selected packet.                                                |

> [!Question]
> **Read the "capture file comments". What is the flag?** 

![Exported image|1000](/img/user/TryHackMe/THM_Images/c06522ed3daab281eb09b0d426b468f8.png)  

![Exported image|1000](/img/user/TryHackMe/THM_Images/759145b04c2db1566017eafeb1180981.png)  

> [!Success] Answer
> TryHackMe_Wireshark_Demo

> [!Question]
> **What is the total number of packets?** 

![Exported image|1000](/img/user/TryHackMe/THM_Images/23ac11f9587fdb10bd92a4b1e19cecd5.png) 

> [!Success] Answer
> Answer: 58620

> [!Question]
> **What is the SHA256 hash value of the capture file?** 

![Exported image](/img/user/TryHackMe/THM_Images/4e212306dab8fe1179df91f346405872.png)  

> [!Success] Answer
> f446de335565fb0b0ee5e5a3266703c778b2f3dfad7efeaeccb2da5641a6d6eb
              
# Task 3 - Packet Dissection

> [!Question]
> **View packet number 38. Which markup language is used under the HTTP protocol?** 

![Exported image|1000](/img/user/TryHackMe/THM_Images/6a4665730b66be636cc54802cef36ca8.png)  

> [!Success] Answer
> extensible Markup Language

> [!Question]
> **What is the arrival date of the packet? (Answer format: Month/Day/Year)**  

![Exported image|1000](/img/user/TryHackMe/THM_Images/cc250e0a66b4f82909eb7562e23513f0.png)

> [!Success] Answer
> 05/13/2004

> [!Question]
> **What is the TTL value?** 

![Exported image|1000](/img/user/TryHackMe/THM_Images/27c1323fbcb27655fd326e5203d7bf93.png)  

> [!Success] Answer
> 47

> [!Question]
> **What is the TCP payload size?** 

![Exported image|1000](/img/user/TryHackMe/THM_Images/4c60e3d452ec863a7dc587baaeb9c31b.png)  

> [!Success] Answer
> 424

> [!Question]
> **What is the e-tag value?** 

![Exported image|1000](/img/user/TryHackMe/THM_Images/29faa04b9e1b20e83895e21a90a42c3d.png)  

> [!Success] Answer
> 9a01a-4696-7e354b00
                      
# Task 4 - Packet Navigation

Can do in-frame packet tracking through the "Go" menu

![|1000](/img/user/TryHackMe/THM_Images/e43dd7506f007d6825006deec27dbb08.png)

Can find packets by **packet content**
- "Edit --> Find Packet"
- Searches inside the packets
- Three panes, packet list, packet details, and packet bytes
- Have to search for the event in the correct information pane, or else it won't show up even if it exists

![|1000](/img/user/TryHackMe/THM_Images/eea453c69e723466d69e3e9edbb2960d.png)
    
Can mark packets
- Will be shown as black no matter what
- Temporary, will be lost after closing file

![|1000](/img/user/TryHackMe/THM_Images/d61d418470ae8a58ac4e2ad8c63ff2c7.png)

Can also put comments inside packets. Will stay within the capture file.

![|1000](/img/user/TryHackMe/THM_Images/416a6f2fc14e2ac2c52fd6558e017608.png)

Can export specified packets or objects (files). Available for HTTP, SMB, TFTP, IMF, and DICOM

![|1000](/img/user/TryHackMe/THM_Images/050053d9db9ccf35647540d5044388e8.png)

**Time Display Format**

Can go to "View --> Time Display Format" to change time display
    
![](/img/user/TryHackMe/THM_Images/2ead9de4d8a4c3d0f1f7d79cdb10cac3.png)
    
![|1000](/img/user/TryHackMe/THM_Images/9c8796a7631c327a7b6aa7d6dcbcc5aa.png)

**Color Severity**

| Severity | Colour | Info                                                     |
| -------- | ------ | -------------------------------------------------------- |
| Chat     | Blue   | Information on usual workflow.                           |
| Note     | Cyan   | Notable events like application error codes.             |
| Warn     | Yellow | Warnings like unusual error codes or problem statements. |
| Error    | Red    | Problems like malformed packets.                         |

> [!Question]
> **Search the "r4w" string in packet details. What is the name of artist 1?** 

![Exported image|1000](/img/user/TryHackMe/THM_Images/7c46146e16033e6bcf5e656d10c8ea59.png)  

> [!Success] Answer
> r4w8173

> [!Question]
> **Go to packet 12 and read the comments. What is the answer?** 

![Exported image|1000](/img/user/TryHackMe/THM_Images/15c41aa3cad08b6e98b378125957c45b.png)  

![Exported image|1000](/img/user/TryHackMe/THM_Images/4b467320b663ef95674d008df069a2fa.png)  

![Exported image|1000](/img/user/TryHackMe/THM_Images/60cf035135578060a13ddc5d1eedbdcf.png)

![Exported image|1000](/img/user/TryHackMe/THM_Images/3e4be635c82a7a4b979920c81ec84b4e.png)     

![Exported image|1000](/img/user/TryHackMe/THM_Images/7f098476f797999e17d97d98a5154454.png)  

![Exported image|1000](/img/user/TryHackMe/THM_Images/705b0dab4e519281393039c8e243259b.png)  

> [!OR]

![Exported image](/img/user/TryHackMe/THM_Images/0c8bbd4ef87b4d3de3e4293ad889d9bc.png)

![Exported image](/img/user/TryHackMe/THM_Images/4a0239bdcdd359683d27c40f546bdfaf.png)  

![Exported image](/img/user/TryHackMe/THM_Images/b488530ef9c787f38701910039515b80.png)  

> [!Success] Answer
> 911cd574a42865a956ccde2d04495ebf

> [!Question]
> **There is a ".txt" file inside the capture file. Find the file and read it; what is the alien's name?** 

![Exported image|1000](/img/user/TryHackMe/THM_Images/e6bfcde03489d22c6c397c94f0b0c41c.png)  

![Exported image|1000](/img/user/TryHackMe/THM_Images/5309e2f40ea4d5ed80c7e32487ca96d0.png)  

> [!Success] Answer
> PACKETMASTER

> [!Question]
> **Look at the expert info section. What is the number of warnings?** 

![Exported image|1000](/img/user/TryHackMe/THM_Images/610129f881122dcee0c3133117d93b61.png)  

![Exported image](/img/user/TryHackMe/THM_Images/93fa5efa61df1e7514bd8abaac721e70.png)  

> [!Success] Answer
> 1636
                                  
# Task 5 - Packet Filtering

- **Capture** filtering, used to capture valid packets in the first place
- **Display** filtering, used to filter valid packets that were captured from the capture filtering

**Applying as Filter**
- "Analyze --> Apply as Filter"
    ![Wireshark - apply as filter|1000](/img/user/TryHackMe/THM_Images/cb10936f339c901d3f2abf715f089377.png)

**Conversation Filter**
- View only related packets to that one packet
- "Analyze --> Conversation Filter"
    ![Wireshark - conversation filter|1000](/img/user/TryHackMe/THM_Images/dfc6218e7545f9e501d4c06d7e967ba4.png)

**Colorize Conversation**
- Highlights linked packets without applying the filter
- "View --> Colorize Conversation"
    ![|1000](/img/user/TryHackMe/THM_Images/df2938c549f34223fbad462f897c2cac.png)

**Prepare as Filter**
- Create display filters without applying it
![Wireshark - prepare as filter|1000](/img/user/TryHackMe/THM_Images/5ae1d5e9650fc4684e7580f12b31883d.png)

**Apply as Column**
- Add columns to the packet list pane
- "Analyze --> Apply as Column" 
    ![Wireshark - apply as column|1000](/img/user/TryHackMe/THM_Images/50dd215a9a8c413058700e031ed2f341.png)

**Follow Stream**
- View raw traffic presented at application level
- "Analyze --> Follow TCP/UDP/HTTP Stream"
![Wireshark - follow stream|1000](/img/user/TryHackMe/THM_Images/dc8d9ca21de82afdaf26fc0f784c7b1b.png)

> [!Question]
> **Go to packet number 4. Right-click on the "Hypertext Transfer Protocol" and apply it as a filter. Now, look at the filter pane. What is the filter query**? 

![Exported image|1000](/img/user/TryHackMe/THM_Images/399ebb267b7573781773e3ffae9834d9.png)

![Exported image|1000](/img/user/TryHackMe/THM_Images/dc27e7c70368874782c0b58468d2b3c7.png)  

> [!Success] Answer
> http

> [!Question]
> **What is the number of displayed packets?** 

After applying the http filter

![Exported image](/img/user/TryHackMe/THM_Images/aa2444fdef2cd9d2b5bcc72ebc0eb016.png)  

> [!Success] Answer
> 1089

> [!Question]
> **Go to packet number 33790 and follow the stream. What is the total number of artists?** 

![Exported image|1000](/img/user/TryHackMe/THM_Images/0dc7758e615ac9e32e80eba86ff567f6.png)  

![Exported image](/img/user/TryHackMe/THM_Images/bf9969df078b8026dfc83b73b9d89f52.png)  

> [!Success] Answer
> 3

> [!Question]
> **What is the name of the second artist?** 

![Exported image](/img/user/TryHackMe/THM_Images/9ffeb5f4d27b211c6b559745b81310f2.png)  

> [!Success] Answer
> Blad3