### Preprocessing With Volatility

In this task, we will use the Volatility 3 tool version. However, we won’t go deep into the investigation and analysis part of the result—we could write a whole book about it! Instead, we want you to be familiar with and get a feel for how the tool works. Run the command as instructed and wait for the result to show. Each plugin takes 2-3 minutes to show the output.

Here are some of the parameters or plugins we will use. We will focus on Windows plugins.

- windows.pstree.PsTree
- windows.pslist.PsList
- windows.cmdline.CmdLine
- windows.filescan.FileScan
- windows.dlllist.DllList
- windows.malfind.Malfind
- windows.psscan.PsScan

Let’s get started then!

In your RemnuxVM, run `sudo su`, then navigate to **/home/ubuntu/Desktop/tasks/Wcry_memory_image/** directory, and our file would be **wcry.mem**. We will run each plugin after the command `vol3 -f wcry.mem`.

  

### PsTree

This plugin lists processes in a tree based on their parent process ID.

Terminal

```powershell
root@MACHINE_IP:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ vol3 -f wcry.mem windows.pstree.PsTree
Volatility 3 Framework 2.0.0
Progress:  100.00		PDB scanning finished
```

**View Results**

Terminal

```powershell
PID	PPID	ImageFileName	Offset(V)	Threads	Handles	SessionId	Wow64	CreateTime	ExitTime

4	0	System	0x823c8830	51	244	N/A	False	N/A	N/A
* 348	4	smss.exe	0x82169020	3	19	N/A	False	2017-05-12 21:21:55.000000 	N/A
** 620	348	winlogon.exe	0x8216e020	23	536	0	False	2017-05-12 21:22:01.000000 	N/A
*** 664	620	services.exe	0x821937f0	15	265	0	False	2017-05-12 21:22:01.000000 	N/A
**** 1024	664	svchost.exe	0x821af7e8	79	1366	0	False	2017-05-12 21:22:03.000000 	N/A
***** 1768	1024	wuauclt.exe	0x81f747c0	7	132	0	False	2017-05-12 21:22:52.000000 	N/A
***** 1168	1024	wscntfy.exe	0x81fea8a0	1	37	0	False	2017-05-12 21:22:56.000000 	N/A
**** 1152	664	svchost.exe	0x821bea78	10	173	0	False	2017-05-12 21:22:06.000000 	N/A
**** 544	664	alg.exe	0x82010020	6	101	0	False	2017-05-12 21:22:55.000000 	N/A
**** 836	664	svchost.exe	0x8221a2c0	19	211	0	False	2017-05-12 21:22:02.000000 	N/A
**** 260	664	svchost.exe	0x81fb95d8	5	105	0	False	2017-05-12 21:22:18.000000 	N/A
**** 904	664	svchost.exe	0x821b5230	9	227	0	False	2017-05-12 21:22:03.000000 	N/A
**** 1484	664	spoolsv.exe	0x821e2da0	14	124	0	False	2017-05-12 21:22:09.000000 	N/A
**** 1084	664	svchost.exe	0x8203b7a8	6	72	0	False	2017-05-12 21:22:03.000000 	N/A
*** 676	620	lsass.exe	0x82191658	23	353	0	False	2017-05-12 21:22:01.000000 	N/A
** 596	348	csrss.exe	0x82161da0	12	352	0	False	2017-05-12 21:22:00.000000 	N/A
1636	1608	explorer.exe	0x821d9da0	11	331	0	False	2017-05-12 21:22:10.000000 	N/A
* 1956	1636	ctfmon.exe	0x82231da0	1	86	0	False	2017-05-12 21:22:14.000000 	N/A
* 1940	1636	tasksche.exe	0x82218da0	7	51	0	False	2017-05-12 21:22:14.000000 	N/A
** 740	1940	@WanaDecryptor@	0x81fde308	2	70	0	False	2017-05-12 21:22:22.000000 	N/A
```

  

### PsList

This plugin is used to list all currently active processes in the machine.

Terminal

```powershell
root@MACHINE_IP:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ vol3 -f wcry.mem windows.pslist.PsList
Volatility 3 Framework 2.0.0
Progress:  100.00		PDB scanning finished
```

**View Results**

Terminal

```powershell
PID	PPID	ImageFileName	Offset(V)	Threads	Handles	SessionId	Wow64	CreateTime	ExitTime	File output

4	0	System	0x823c8830	51	244	N/A	False	N/A	N/A	Disabled
348	4	smss.exe	0x82169020	3	19	N/A	False	2017-05-12 21:21:55.000000 	N/A	Disabled
596	348	csrss.exe	0x82161da0	12	352	0	False	2017-05-12 21:22:00.000000 	N/A	Disabled
620	348	winlogon.exe	0x8216e020	23	536	0	False	2017-05-12 21:22:01.000000 	N/A	Disabled
664	620	services.exe	0x821937f0	15	265	0	False	2017-05-12 21:22:01.000000 	N/A	Disabled
676	620	lsass.exe	0x82191658	23	353	0	False	2017-05-12 21:22:01.000000 	N/A	Disabled
836	664	svchost.exe	0x8221a2c0	19	211	0	False	2017-05-12 21:22:02.000000 	N/A	Disabled
904	664	svchost.exe	0x821b5230	9	227	0	False	2017-05-12 21:22:03.000000 	N/A	Disabled
1024	664	svchost.exe	0x821af7e8	79	1366	0	False	2017-05-12 21:22:03.000000 	N/A	Disabled
1084	664	svchost.exe	0x8203b7a8	6	72	0	False	2017-05-12 21:22:03.000000 	N/A	Disabled
1152	664	svchost.exe	0x821bea78	10	173	0	False	2017-05-12 21:22:06.000000 	N/A	Disabled
1484	664	spoolsv.exe	0x821e2da0	14	124	0	False	2017-05-12 21:22:09.000000 	N/A	Disabled
1636	1608	explorer.exe	0x821d9da0	11	331	0	False	2017-05-12 21:22:10.000000 	N/A	Disabled
1940	1636	tasksche.exe	0x82218da0	7	51	0	False	2017-05-12 21:22:14.000000 	N/A	Disabled
1956	1636	ctfmon.exe	0x82231da0	1	86	0	False	2017-05-12 21:22:14.000000 	N/A	Disabled
260	664	svchost.exe	0x81fb95d8	5	105	0	False	2017-05-12 21:22:18.000000 	N/A	Disabled
740	1940	@WanaDecryptor@	0x81fde308	2	70	0	False	2017-05-12 21:22:22.000000 	N/A	Disabled
1768	1024	wuauclt.exe	0x81f747c0	7	132	0	False	2017-05-12 21:22:52.000000 	N/A	Disabled
544	664	alg.exe	0x82010020	6	101	0	False	2017-05-12 21:22:55.000000 	N/A	Disabled
1168	1024	wscntfy.exe	0x81fea8a0	1	37	0	False	2017-05-12 21:22:56.000000 	N/A	Disabled
```

  

  

### CmdLine

This plugin is used to list process command line arguments.

Terminal

```powershell
root@MACHINE_IP:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ vol3 -f wcry.mem windows.cmdline.CmdLine
Volatility 3 Framework 2.0.0
Progress:  100.00		PDB scanning finished
```

**View Results**

Terminal

```powershell
PID	Process	Args

4	System	Required memory at 0x10 is not valid (process exited?)
348	smss.exe	\SystemRoot\System32\smss.exe
596	csrss.exe	C:\WINDOWS\system32\csrss.exe ObjectDirectory=\Windows SharedSection=1024,3072,512 Windows=On SubSystemType=Windows ServerDll=basesrv,1 ServerDll=winsrv:UserServerDllInitialization,3 ServerDll=winsrv:ConServerDllInitialization,2 ProfileControl=Off MaxRequestThreads=16
620	winlogon.exe	winlogon.exe
664	services.exe	C:\WINDOWS\system32\services.exe
676	lsass.exe	C:\WINDOWS\system32\lsass.exe
836	svchost.exe	C:\WINDOWS\system32\svchost -k DcomLaunch
904	svchost.exe	C:\WINDOWS\system32\svchost -k rpcss
1024	svchost.exe	C:\WINDOWS\System32\svchost.exe -k netsvcs
1084	svchost.exe	C:\WINDOWS\system32\svchost.exe -k NetworkService
1152	svchost.exe	C:\WINDOWS\system32\svchost.exe -k LocalService
1484	spoolsv.exe	C:\WINDOWS\system32\spoolsv.exe
1636	explorer.exe	C:\WINDOWS\Explorer.EXE
1940	tasksche.exe	"C:\Intel\ivecuqmanpnirkt615\tasksche.exe" 
1956	ctfmon.exe	"C:\WINDOWS\system32\ctfmon.exe" 
260	svchost.exe	C:\WINDOWS\system32\svchost.exe -k LocalService
740	@WanaDecryptor@	@WanaDecryptor@.exe
1768	wuauclt.exe	"C:\WINDOWS\system32\wuauclt.exe" /RunStoreAsComServer Local\[400]SUSDS81a6658cb72fa845814e75cca9a42bf2
544	alg.exe	C:\WINDOWS\System32\alg.exe
1168	wscntfy.exe	C:\WINDOWS\system32\wscntfy.exe
```

  

  

### FileScan

This plugin scans for file objects in a particular Windows memory image. The results have more than 1,400 lines.

Terminal

```powershell
root@MACHINE_IP:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ vol3 -f wcry.mem windows.filescan.FileScan
Volatility 3 Framework 2.0.0
Progress:  100.00		PDB scanning finished
```

**View Results**

Terminal

```powershell
Offset	Name	Size
0x1f40310	\Endpoint	112
0x1f65718	\Endpoint	112
0x1f66cd8	\WINDOWS\system32\wbem\wmipcima.dll	112
0x1f67198	\WINDOWS\Prefetch\TASKDL.EXE-01687054.pf	112
0x1f67a70	\WINDOWS\system32\security.dll	112
0x1f67c68	\boot.ini	112
0x1f67ef8	\WINDOWS\system32\cfgmgr32.dll	112
0x1f684d0	\WINDOWS\system32\wbem\framedyn.dll	112
0x1f686d8	\WINDOWS\system32\wbem\cimwin32.dll	112
0x1f6a7f0	\WINDOWS\system32\kmddsp.tsp	112
0x1f6ae20	\$Directory	112
0x1f6b9b0	\$Directory	112
0x1f6bbf8	\$Directory	112
0x1f6bdc8	\PIPE_EVENTROOT\CIMV2SCM EVENT PROVIDER	112
0x1f6be60	\WINDOWS\win.ini	112
0x1f6bf90	\$Directory	112
0x1f6c2a8	\$Directory	112
0x1f6c3b8	\$Directory	112
0x1f6cea0	\$Directory	112
0x1f6d158	\lsass	112
0x1f6d4a8	\$Directory	112
0x1f6dba8	\$Directory	112
0x1f6e188	\$Directory	112
0x1f6e6a0	\$Directory	112
0x1f70708	\WINDOWS\system32\rastapi.dll	112
0x1f71190	\$Directory	112
0x1f71b88	\WINDOWS\system32\wbem\Logs\wbemess.log	112
0x1f72f90	\$Directory	112
0x1f732b0	\WINDOWS\system32\uniplat.dll	112
0x1f735d8	\$Directory	112
0x1f753d8	\WINDOWS\system32	112
0x1f75888	\$Directory	112
0x1f75ba8	\$Directory	112
0x1f75df0	\$Directory	112
0x1f761a8	\$Directory	112
0x1f76368	\$Directory	112
0x1f769e0	\$Directory	112
0x1f76b10	\$Directory	112
0x1f76e58	\Documents and Settings\All Users\Start Menu\desktop.ini	112
0x1f76f48	\$Directory	112
0x1f77028	\Documents and Settings\donny\Start Menu\Programs\Accessories\Accessibility\desktop.ini	112
0x1f77298	\$Directory	112
0x1f77728	\$Directory	112
0x1f7a190	\$Directory	112
0x1f7a590	\$Directory	112
0x1f7a990	\$Directory	112
0x1f7aea0	\$Directory	112
0x1f7b308	\$Directory	112
0x1f7b748	\$Directory	112
0x1f7bbd0	\$Directory	112
0x1f7d518	\$Directory	112
0x1f7da18	\Documents and Settings\All Users\Application Data\Microsoft\User Account Pictures\Default Pictures\butterfly.bmp.WNCRY	112
0x1f7dae0	\$Directory	112
0x1f7f180	\Documents and Settings\donny\My Documents\My Pictures\Desktop.ini	112
0x1f7f218	\WINDOWS\system32\rasqec.dll	112
0x1f7f538	\WINDOWS\WindowsUpdate.log	112
0x1f80bd8	\$Directory	112
0x1f81548	\WINDOWS\system32\wbem\framedyn.dll	112
0x1f83390	\$Directory	112
0x1f83758	\WINDOWS\Fonts\times.ttf	112
0x1f840a0	\$Directory	112
0x1f866b8	\$Directory	112
0x1f87028	\WINDOWS\system32\c_1258.nls	112
0x1f871a0	\Intel\ivecuqmanpnirkt615\@WanaDecryptor@.exe	112
0x1f87c10	\WINDOWS\Fonts\timesbd.ttf	112
0x1f87f08	\WINDOWS\system32\msls31.dll	112
0x1f88140	\WINDOWS\system32\c_1257.nls	112
0x1f885e8	\WINDOWS\system32\c_1256.nls	112
0x1f88d00	\WINDOWS\system32\c_1254.nls	112
0x1f8d548	\$Directory	112
0x1f8f798	\$Directory	112
0x1f8f9c0	\$Directory	112
0x1f8fbf8	\$Directory	112
0x1f90438	\$Directory	112
0x1f90a38	\$Directory	112
0x1f90ea0	\$Directory	112
0x1f92cf0	\$Directory	112
0x1f92d88	\ROUTER	112
0x1f95c28	\$Directory	112
0x1f990d8	\srvsvc	112
0x1f997c8	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x1f99a18	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x1f99ab0	\trkwks	112
0x1f99d20	\$Directory	112
0x1f9a848	\WINDOWS\system32\c_1255.nls	112
0x1f9aea8	\WINDOWS\system32\c_1253.nls	112
0x1f9fe18	\lsass	112
0x1fa1e60	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x1fa1ef8	\winreg	112
0x1fa1f90	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x1fa2c88	\WINDOWS\WindowsUpdate.log	112
0x1fa30c0	\$Directory	112
0x1fa55b0	\$Directory	112
0x1fa6960	\$Directory	112
0x1fa6ba8	\$Directory	112
0x1fa6df0	\$Directory	112
0x1fa8cc0	\WINDOWS\WinSxS\Manifests\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202.Manifest	112
0x1fac638	\$Directory	112
0x1facf28	\$Directory	112
0x1fb12c0	\{9B365890-165F-11D0-A195-0020AFD156E4}	112
0x1fb17a8	\Intel\ivecuqmanpnirkt615\@WanaDecryptor@.exe	112
0x1fb1880	\WINDOWS\Debug\UserMode\userenv.log	112
0x1fb1a40	\WINDOWS\pchealth\helpctr\BATCH	112
0x1fb2278	\Intel\ivecuqmanpnirkt615\taskse.exe	112
0x1fb3d10	\keysvc	112
0x1fb5620	\WINDOWS\system32\wbem\wmipcima.dll	112
0x1fb6310	\Documents and Settings\donny\Start Menu\Programs\Startup\desktop.ini	112
0x1fb7650	\WINDOWS\system32\mfc42.dll	112
0x1fb78a0	\$Directory	112
0x1fb7eb8	\keysvc	112
0x1fb7f50	\DAV RPC SERVICE	112
0x1fb8350	\srvsvc	112
0x1fb88c8	\lsass	112
0x1fba540	\WINDOWS\system32\wbem\Logs\wbemcore.log	112
0x1fbad10	\47	112
0x1fbc250	\$Directory	112
0x1fbce00	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x1fbcef8	\Intel\ivecuqmanpnirkt615\u.wnry	112
0x1fde628	\WINDOWS\system32\ntlanman.dll	112
0x1fde6c0	\WINDOWS\system32\netui0.dll	112
0x1fe4f90	\$Directory	112
0x1fe5858	\Endpoint	112
0x1fe5a40	\$Directory	112
0x1fe5b50	\$Directory	112
0x1fe65c8	\PIPE_EVENTROOT\CIMV2SCM EVENT PROVIDER	112
0x1fe6718	\$Directory	112
0x1fe6b40	\$Directory	112
0x1fe6d20	\$Directory	112
0x1fe7c48	\{9B365890-165F-11D0-A195-0020AFD156E4}	112
0x1fe7d00	\winreg	112
0x1fe7f90	\{9B365890-165F-11D0-A195-0020AFD156E4}	112
0x1fe8390	\PCHFaultRepExecPipe	112
0x1fe8940	\$Directory	112
0x1fec388	\WINDOWS\system32\c_1251.nls	112
0x1fec580	\WINDOWS\system32\c_949.nls	112
0x1fec6b8	\$Directory	112
0x1fee638	\WINDOWS\system32\wbem\cimwin32.dll	112
0x1ff7c78	\WINDOWS\system32\h323.tsp	112
0x1ff7d10	\WINDOWS\system32\ipconf.tsp	112
0x1ff8bd8	\WINDOWS\system32\security.dll	112
0x2004650	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x20046e8	\net\NtControlPipe7	112
0x2005848	\SfcApi	112
0x2005930	\SfcApi	112
0x200cd20	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x200d6b0	\WINDOWS\SchedLgU.Txt	112
0x200df90	\Endpoint	112
0x20147a8	\WINDOWS\0.log	112
0x2014a38	\PCHHangRepExecPipe	112
0x2014b30	\srvsvc	112
0x201f820	\WINDOWS\system32\mui\041D	112
0x201f948	\WINDOWS\system32\mui\041b	112
0x2021820	\WINDOWS\system32\mui\0419	112
0x2021948	\WINDOWS\system32\mui\0416	112
0x2022678	\$Directory	112
0x2022720	\$Directory	112
0x2022998	\WINDOWS\system32\narrator.exe	112
0x2025870	\WINDOWS\system32\mui\0415	112
0x2025998	\WINDOWS\system32\mui\0414	112
0x2026818	\WINDOWS\system32\mui\0413	112
0x2026900	\WINDOWS\system32\mui\0412	112
0x2026998	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x20288d8	\WINDOWS\Help\Tours\mmTour	112
0x2028998	\WINDOWS\system32\IME\TINTLGNT	112
0x2029848	\WINDOWS\system32\spool\drivers\color	112
0x2029970	\WINDOWS\PeerNet	112
0x202a6b0	\Program Files\Common Files\Microsoft Shared\Speech\1033	112
0x202a748	\Program Files\Common Files\SpeechEngines\Microsoft	112
0x202a870	\WINDOWS\system32\wbem\snmp	112
0x202a998	\WINDOWS\Resources\Themes\Luna\Shell\Metallic	112
0x202b638	\Program Files\Internet Explorer	112
0x202b8b0	\Program Files\Common Files\Microsoft Shared\VGX	112
0x202c938	\Documents and Settings\LocalService\NTUSER.DAT	112
0x202d848	\Program Files\Common Files\MSSoap\Binaries\Resources\1033	112
0x202d998	\Program Files\Common Files\MSSoap\Binaries	112
0x202e820	\WINDOWS\system32\oobe	112
0x202e948	\Program Files\Outlook Express	112
0x2030998	\spoolss	112
0x2031710	\WINDOWS\ime\chsime\applets	112
0x2031970	\Program Files\Windows NT\Pinball	112
0x2033748	\WINDOWS\ime\shared\res	112
0x2033870	\WINDOWS\system32\npp	112
0x2033998	\WINDOWS\mui	112
0x20348e8	\net\NtControlPipe5	112
0x2037718	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x203c918	\WINDOWS\system32	112
0x203f7b8	\Program Files\Common Files\SpeechEngines\Microsoft\TTS\1033	112
0x203f8e0	\WINDOWS\system32\Restore	112
0x2042718	\Documents and Settings\LocalService\Local Settings\Application Data\Microsoft\Windows\UsrClass.dat	112
0x20456b8	\WINDOWS\Resources\Themes\Luna\Shell\Homestead	112
0x2045870	\WINDOWS\Resources\Themes\Luna\Shell\NormalColor	112
0x2045998	\Program Files\Common Files\Microsoft Shared\Speech	112
0x2084c78	\WINDOWS\system32\hidphone.tsp	112
0x2084d10	\WINDOWS\system32\h323log.txt	112
0x20865f0	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x2088ab8	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x2088bf0	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Communications\Wireless Network Setup Wizard.lnk	112
0x2089978	\$Directory	112
0x2089bd0	\WINDOWS\system32\magnify.exe	112
0x208b198	\$Directory	112
0x208b5d8	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x208c5f8	\WINDOWS\system32\mui\0424	112
0x208c720	\WINDOWS\system32\mui\041f	112
0x208d238	\EVENTLOG	112
0x209db50	\WINDOWS\WinSxS\Policies\x86_policy.6.0.Microsoft.Windows.Common-Controls_6595b64144ccf1df_x-ww_5ddad775\6.0.2600.6028.Policy	112
0x209dbe8	\Intel\ivecuqmanpnirkt615\00000000.res	112
0x209ddb0	\WINDOWS\system32\wbem\wmiprvse.exe	112
0x209de48	\Intel\ivecuqmanpnirkt615\b.wnry	112
0x209e1c0	\$Directory	112
0x209e3a0	\$Directory	112
0x209e580	\$Directory	112
0x20a0e38	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x215b838	\browser	112
0x215c230	\WINDOWS\ime\imjp8_1\applets	112
0x215c418	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x215cad0	\Documents and Settings\donny\Start Menu\Programs\Accessories\desktop.ini	112
0x215e330	\$Directory	112
0x215e648	\$Directory	112
0x2162028	\net\NtControlPipe1	112
0x2162d50	\$Directory	112
0x2162df8	\$Directory	112
0x2162f90	\WINDOWS\system32\wucltui.dll	112
0x2164698	\$Directory	112
0x2164740	\$Directory	112
0x2164ed0	\$Directory	112
0x2165a80	\$Directory	112
0x2167f90	\$Directory	112
0x216a028	\atsvc	112
0x216a0d0	\epmapper	112
0x216b038	\$Directory	112
0x216b310	\WINDOWS\system32\config\system	112
0x216b3a8	\WINDOWS\system32\config\SECURITY	112
0x216be98	\$Directory	112
0x216c270	\WINDOWS\system32\olesvr32.dll	112
0x216cc68	\WINDOWS\WinSxS\x86_Microsoft.Windows.GdiPlus_6595b64144ccf1df_1.0.6002.23084_x-ww_f3f35550\GdiPlus.dll	112
0x216cef8	\WINDOWS\system32\url.dll	112
0x216cf90	\WINDOWS\system32\olethk32.dll	112
0x2170b38	\Endpoint	112
0x2172038	\$Directory	112
0x2172198	\Endpoint	112
0x2175038	\$Directory	112
0x2179038	\$Directory	112
0x2179f90	\$Directory	112
0x217a028	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x217cef8	\WINDOWS\system32\$winnt$.inf	112
0x217e028	\scerpc	112
0x217e138	\scerpc	112
0x217e378	\$Directory	112
0x217ef90	\$Directory	112
0x2180320	\$Directory	112
0x2183038	\$Directory	112
0x2184128	\WINDOWS\system32	112
0x2184318	\$Directory	112
0x2185320	\$Directory	112
0x2187f90	\WINDOWS\system32\olecnv32.dll	112
0x21885d8	\WINDOWS\system32\ndptsp.tsp	112
0x2189238	\WINDOWS\Tasks	112
0x218b028	\WINDOWS\system32\dllcache	112
0x218b690	\net\NtControlPipe6	112
0x218b848	\WINDOWS\system32\drivers\etc	112
0x218b8e0	\Documents and Settings\donny\Start Menu\Programs\Accessories\Address Book.lnk	112
0x218c320	\epmapper	112
0x218ce08	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x218cf90	\$Directory	112
0x218de68	\net\NtControlPipe3	112
0x218e0c8	\Endpoint	112
0x218ff10	\$Directory	112
0x2190038	\$Directory	112
0x2191038	\$Directory	112
0x2192d78	\$Directory	112
0x2194840	\$Directory	112
0x21948d8	\WINDOWS\system32\olecli32.dll	112
0x2194d00	\$Directory	112
0x2195038	\$Directory	112
0x2199418	\WINDOWS\system32\unimdm.tsp	112
0x219a130	\ntsvcs	112
0x219be98	\TerminalServer\AutoReconnect	112
0x219c198	\wkssvc	112
0x219cee8	\$Directory	112
0x219d028	\Documents and Settings\All Users\Start Menu\Programs\Games\Minesweeper.lnk	112
0x219d1c0	\Documents and Settings\LocalService\Cookies\index.dat	112
0x219d908	\Documents and Settings\All Users\Application Data\Microsoft\User Account Pictures\Default Pictures\chess.bmp.WNCRY	112
0x219e120	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x219e320	\$Directory	112
0x219f320	\WINDOWS\system32\hnetwiz.dll	112
0x219f750	\WINDOWS\system32\ipnathlp.dll	112
0x219fb70	\Endpoint	112
0x219fdf0	\$Directory	112
0x21a0028	\ROUTER	112
0x21a0848	\net\NtControlPipe11	112
0x21a2320	\$Directory	112
0x21a45a8	\$Directory	112
0x21a5668	\$Directory	112
0x21a6c68	\pagefile.sys	112
0x21a6d00	\WINDOWS\system32\wow32.dll	112
0x21a7500	\$Directory	112
0x21a75a8	\$Directory	112
0x21a7f10	\Documents and Settings\NetworkService\NTUSER.DAT	112
0x21a88d8	\Documents and Settings\NetworkService\ntuser.dat.LOG	112
0x21a8f90	\winlogonrpc	112
0x21a98f0	\atsvc	112
0x21aaef8	\WINDOWS\system32\config\Internet.evt	112
0x21aaf90	\Program Files\Common Files\Microsoft Shared\web server extensions\40\isapi\_vti_adm	112
0x21ac5e0	\WINDOWS\system32\mui\0411	112
0x21adf90	\WINDOWS\repair\setup.log	112
0x21ae220	\net\NtControlPipe2	112
0x21aff90	\Documents and Settings\donny\Start Menu\Programs\desktop.ini	112
0x21b0320	\net\NtControlPipe4	112
0x21b0f90	\WINDOWS\Prefetch\@WANADECRYPTOR@.EXE-06F053F5.pf	112
0x21b1e68	\WINDOWS\system32\mui\041a	112
0x21b1f90	\WINDOWS\system32\mui\0418	112
0x21b2028	\WINDOWS\system32\mui\0406	112
0x21b2108	\WINDOWS\system32\mui\0407	112
0x21b2c48	\WINDOWS\system32\rasppp.dll	112
0x21b3e90	\WINDOWS\system32\mui\0425	112
0x21b3f90	\WINDOWS\system32\mui\041e	112
0x21b6028	\Program Files\xerox\nwwia	112
0x21b6438	\WINDOWS\system32\mui\0816	112
0x21b6560	\WINDOWS\system32\mui\0804	112
0x21b72c0	\net\NtControlPipe2	112
0x21b7e40	\WINDOWS\system32\mui\0402	112
0x21b7f68	\WINDOWS\system32\mui\0C0A	112
0x21b8028	\Endpoint	112
0x21b8ec0	\net\NtControlPipe0	112
0x21b9028	\Documents and Settings\LocalService\ntuser.dat.LOG	112
0x21b9318	\WINDOWS\system32\IME\CINTLGNT	112
0x21b9748	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x21ba868	\WINDOWS\system32\davclnt.dll	112
0x21bb028	\Documents and Settings\LocalService\Local Settings\Application Data\Microsoft\Windows\UsrClass.dat.LOG	112
0x21bc068	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x21be198	\255	112
0x21bf230	\WINDOWS\system32\Setup	112
0x21bf318	\WINDOWS\system32\Com	112
0x21bf758	\Ctx_WinStation_API_service	112
0x21bfc08	\WINDOWS\ime\imkr6_1\applets	112
0x21c0dd0	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x21c1198	\WINDOWS\system32	112
0x21c1318	\Program Files\Internet Explorer\Connection Wizard	112
0x21c13f0	\WINDOWS\system32\xircom	112
0x21c1688	\WINDOWS\ime\imkr6_1	112
0x21c1720	\Program Files\Common Files\Microsoft Shared\MSInfo	112
0x21c1a98	\Program Files\Common Files\SpeechEngines\Microsoft\Lexicon\1033	112
0x21c1bc0	\WINDOWS\system32\IME\PINTLGNT	112
0x21c1c80	\WINDOWS\ime\shared	112
0x21c21f0	\Program Files\Common Files\System	112
0x21c2288	\Program Files\Windows NT	112
0x21c2830	\WINDOWS\srchasst	112
0x21c28c8	\WINDOWS\ime	112
0x21c2960	\Program Files\Movie Maker	112
0x21c29f8	\WINDOWS\Resources\Themes\Luna	112
0x21c2ad0	\Documents and Settings\NetworkService\Local Settings\Application Data\Microsoft\Windows\UsrClass.dat.LOG	112
0x21c2ef8	\Program Files\Windows Media Player	112
0x21c2f90	\Program Files\Common Files\Microsoft Shared\DAO	112
0x21c3238	\WINDOWS\system32\wbem\wmiprvse.exe	112
0x21c3610	\WINDOWS\pchealth\UploadLB\Binaries	112
0x21c3c58	\$Directory	112
0x21c3d00	\$Directory	112
0x21c3ea8	\WINDOWS\system32\mui\0427	112
0x21c3f90	\WINDOWS\system32\mui\0426	112
0x21c4c58	\$Directory	112
0x21c4d00	\$Directory	112
0x21c59a0	\WINDOWS	112
0x21c5f90	\WINDOWS\system32\wbem\xml	112
0x21c6028	\WINDOWS\system32\mui\0405	112
0x21c61c8	\Program Files\Common Files\Microsoft Shared\Triedit	112
0x21c62f0	\WINDOWS\ime\imjp8_1	112
0x21c6f90	\WINDOWS\system32\upnp.dll	112
0x21c7108	\WINDOWS\system32\mui\0404	112
0x21c72f0	\winlogonrpc	112
0x21c8320	\winlogonrpc	112
0x21c8c68	\Documents and Settings\donny	112
0x21c9c68	\WINDOWS\system32\filemgmt.dll	112
0x21ca028	\Endpoint	112
0x21cb198	\WINDOWS\system32	112
0x21cc870	\Documents and Settings\donny\Start Menu\Programs\Accessories\Tour Windows XP.lnk	112
0x21cd108	\WINDOWS\system32\mui\0408	112
0x21cd438	\Documents and Settings\donny\Start Menu\Programs\Accessories\Command Prompt.lnk	112
0x21cd508	\Program Files\Outlook Express\msimn.exe	112
0x21cdbc8	\Program Files\Common Files\Microsoft Shared\web server extensions\40\isapi	112
0x21cdc60	\Program Files\Common Files\Microsoft Shared\web server extensions\40\bin\1033	112
0x21cde18	\WINDOWS\system32\mui\040b	112
0x21ce1d0	\WINDOWS\system32\mui\0410	112
0x21ce2f8	\WINDOWS\system32\mui\040e	112
0x21ce898	\Program Files\Common Files\Microsoft Shared\web server extensions\40\_vti_bin	112
0x21ceba0	\Program Files\MSN Gaming Zone\Windows\bckgzm.exe	112
0x21cf260	\WINDOWS\system32\usmt	112
0x21cf3f0	\WINDOWS\system32\mui\0401	112
0x21cf4b0	\Program Files\Windows NT\Accessories	112
0x21cfb68	\WINDOWS\Debug\PASSWD.LOG	112
0x21d08d8	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x21d0d00	\Program Files\microsoft frontpage\version3.0\bin	112
0x21d0dd0	\WINDOWS\system32\wbem\mof	112
0x21d1028	\Endpoint	112
0x21d15a8	\Program Files\Common Files\Microsoft Shared\web server extensions\40\bots\vinavbar	112
0x21d1d60	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x21d2138	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x21d2238	\Program Files\Common Files\Microsoft Shared\web server extensions\40\admisapi\scripts	112
0x21d26a8	\Program Files\Common Files\Microsoft Shared\web server extensions\40\servsupp	112
0x21d2740	\WINDOWS\system32\drivers	112
0x21d2f50	\WINDOWS\Fonts	112
0x21d3378	\Program Files\Common Files\Microsoft Shared\web server extensions\40\bin	112
0x21d3410	\WINDOWS\system32\inetsrv	112
0x21d3850	\Ctx_WinStation_API_service	112
0x21d3c60	\Program Files\Common Files\Microsoft Shared\web server extensions\40\_vti_bin\_vti_aut	112
0x21d4028	\Endpoint	112
0x21d4550	\WINDOWS\SoftwareDistribution\DataStore\Logs\edb.log	112
0x21d5028	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x21d5198	\WINDOWS\system32\netui1.dll	112
0x21d6218	\Program Files\Common Files\Microsoft Shared\web server extensions\40\admcgi\scripts	112
0x21d6318	\WINDOWS\system32\1033	112
0x21d69d8	\WINDOWS\WinSxS\Manifests\x86_Microsoft.Windows.SystemCompatible_6595b64144ccf1df_5.1.2600.2000_x-ww_bcc9a281.Manifest	112
0x21d7908	\WINDOWS\WinSxS\Manifests\x86_Microsoft.Windows.Networking.RtcRes_6595b64144ccf1df_5.2.2.3_en_16a24bc0.Manifest	112
0x21d79a0	\WINDOWS\WinSxS\Manifests\x86_Microsoft.Windows.Networking.RtcDll_6595b64144ccf1df_5.2.2.3_x-ww_d6bd8b95.Manifest	112
0x21d7e08	\Documents and Settings\All Users\Start Menu\Microsoft Update Catalog.lnk	112
0x21d7f90	\WINDOWS\system32\es.dll	112
0x21d8690	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x21d8ac0	\Intel\ivecuqmanpnirkt615\s.wnry	112
0x21da708	\WINDOWS\system32\OEMINFO.INI	112
0x21dac68	\WINDOWS\Installer\{20C31435-2A0A-4580-BE8B-AC06FC243CA4}\python_icon.exe	112
0x21dad60	\WINDOWS\Help	112
0x21dadf8	\Program Files\Common Files\Microsoft Shared\web server extensions\40\_vti_bin\_vti_adm	112
0x21db7b0	\WINDOWS\system32	112
0x21dc028	\Intel\ivecuqmanpnirkt615\taskdl.exe	112
0x21dc3a8	\Documents and Settings\All Users\Start Menu\Programs\Accessories\System Tools\Character Map.lnk	112
0x21dc440	\Documents and Settings\donny\Start Menu\Programs\Accessories\Notepad.lnk	112
0x21dc578	\Documents and Settings\All Users\Start Menu\Programs\Administrative Tools\Local Security Policy.lnk	112
0x21dc940	\WINDOWS\system32\rcimlby.exe	112
0x21dc9d8	\WINDOWS\explorer.exe	112
0x21dcb68	\Endpoint	112
0x21dce00	\Documents and Settings\donny\Start Menu\Programs\Accessories\Program Compatibility Wizard.lnk	112
0x21dcf90	\Documents and Settings\NetworkService\Local Settings\Application Data\Microsoft\Windows\UsrClass.dat	112
0x21dd238	\WINDOWS\system32\davclnt.dll	112
0x21dd440	\WINDOWS\system32\mfc42.dll	112
0x21dd4d8	\Documents and Settings\All Users\Start Menu\Programs\desktop.ini	112
0x21dd6a8	\protected_storage	112
0x21ddb80	\WINDOWS\system32\wucltui.dll.mui	112
0x21ddf90	\WINDOWS\system32\taskkill.exe	112
0x21de828	\WINDOWS\Fonts\arialbd.ttf	112
0x21df420	\Documents and Settings\donny\Start Menu\Programs\Remote Assistance.lnk	112
0x21e0988	\WINDOWS\system32\attrib.exe	112
0x21e0c20	\$Directory	112
0x21e0d98	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Accessibility\Accessibility Wizard.lnk	112
0x21e16b0	\Endpoint	112
0x21e1748	\Documents and Settings\All Users\Start Menu\Programs\Python 2.7\Python Manuals.lnk	112
0x21e2760	\Documents and Settings\All Users\Start Menu\Programs\Games\Internet Checkers.lnk	112
0x21e28f8	\WINDOWS\system32\fldrclnr.dll	112
0x21e2ad8	\WINDOWS\system32\wbem\Repository\FS\INDEX.BTR	112
0x21e2b70	\WINDOWS\system32\wbem\Repository\FS\OBJECTS.MAP	112
0x21e5098	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x21e5418	\WINDOWS\system32\rundll32.exe	112
0x21e55c0	\Winsock2\CatalogChangeListener-400-0	112
0x21e5be8	\WINDOWS\system32\oembios.bin	112
0x21e5d20	\$Extend\$ObjId	112
0x21e7038	\$Directory	112
0x21e72e0	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x21e7418	\Endpoint	112
0x21e75a8	\Documents and Settings\LocalService\Local Settings\desktop.ini	112
0x21e7c68	\spoolss	112
0x21e7df8	\WINDOWS\system32\config\SysEvent.Evt	112
0x21e8740	\WINDOWS\system32\config\SecEvent.Evt	112
0x21e88b0	\Documents and Settings\All Users\Start Menu\Programs\Accessories\System Tools\System Information.lnk	112
0x21e8980	\Program Files\MSN Gaming Zone\Windows\hrtzzm.exe	112
0x21e8b38	\WINDOWS\WinSxS	112
0x21e8f28	\Program Files\Common Files\System\msadc	112
0x21e9c28	\Endpoint	112
0x21eaf90	\WINDOWS\system32\els.dll	112
0x21eb250	\WINDOWS\WinSxS\Policies\x86_policy.5.2.Microsoft.Windows.Networking.Rtcdll_6595b64144ccf1df_x-ww_c7b7206f\5.2.2.3.Policy	112
0x21eb2e8	\WINDOWS\WinSxS\Policies\x86_policy.5.2.Microsoft.Windows.Networking.Dxmrtp_6595b64144ccf1df_x-ww_362e60dd\5.2.2.3.Policy	112
0x21eb420	\Program Files\Common Files\Microsoft Shared\MSInfo\msinfo32.exe	112
0x21ec748	\wkssvc	112
0x21ec970	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x21ed748	\wkssvc	112
0x21ed810	\WINDOWS\WinSxS\Manifests\x86_Microsoft.Windows.Networking.Dxmrtp_6595b64144ccf1df_5.2.2.3_x-ww_468466a7.Manifest	112
0x21ed9e0	\WINDOWS\WinSxS\Manifests\x86_Microsoft.Windows.GdiPlus_6595b64144ccf1df_1.0.6002.23084_x-ww_f3f35550.Manifest	112
0x21ee698	\WINDOWS\system32\freecell.exe	112
0x21eeaf0	\WINDOWS\system32\drprov.dll	112
0x21eef90	\ntsvcs	112
0x21ef980	\WINDOWS\system32\netshell.dll	112
0x21efc80	\protected_storage	112
0x21f02b8	\$Directory	112
0x21f0b70	\$Directory	112
0x21f1418	\Documents and Settings\All Users\Start Menu\Programs\Accessories\System Tools\Files and Settings Transfer Wizard.lnk	112
0x21f1700	\Program Files\Common Files\Microsoft Shared\web server extensions\40\isapi\_vti_aut	112
0x21f18d8	\WINDOWS\system32\msiexec.exe	112
0x21f1c88	\Documents and Settings\donny\Start Menu\Programs\Outlook Express.lnk	112
0x21f1f90	\WINDOWS\SoftwareDistribution\DataStore\DataStore.edb	112
0x21f2368	\Documents and Settings\LocalService\Local Settings\Temporary Internet Files\Content.IE5\index.dat	112
0x21f2400	\Documents and Settings\donny\My Documents\desktop.ini	112
0x21f2910	\$Directory	112
0x21f2b70	\$Directory	112
0x21f3870	\Intel\ivecuqmanpnirkt615\tasksche.exe	112
0x21f3d00	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x21f3d98	\Documents and Settings\donny\Start Menu\Programs\Accessories\Entertainment\Windows Media Player.lnk	112
0x21f4f90	\Documents and Settings\donny\Start Menu	112
0x220ea70	\System Volume Information\tracking.log	112
0x220ec40	\Intel\ivecuqmanpnirkt615\msg\m_turkish.wnry	112
0x220feb8	\WINDOWS\system32\MSCTF.dll	112
0x2210278	\WINDOWS\system32\config\software.LOG	112
0x22109d0	\WINDOWS\AppPatch	112
0x2210df0	\$Directory	112
0x2211028	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Communications\Network Connections.lnk	112
0x22118f8	\WINDOWS\system32\msnsspc.dll	112
0x2211d20	\WINDOWS\system32\winipsec.dll	112
0x2211f90	\Documents and Settings\All Users\Start Menu\Programs\Accessories\System Tools\System Restore.lnk	112
0x2212028	\Intel\ivecuqmanpnirkt615\msg\m_russian.wnry	112
0x2212668	\WINDOWS\system32\oakley.dll	112
0x2212a90	\WINDOWS\system32\ipsecsvc.dll	112
0x2212eb8	\WINDOWS\system32\srvsvc.dll	112
0x22133b8	\WINDOWS\system32\dhcpcsvc.dll	112
0x2213c28	\WINDOWS\system32\digest.dll	112
0x22148f8	\WINDOWS\system32\credssp.dll	112
0x22159a0	\WINDOWS\WinSxS\Policies\x86_policy.1.0.Microsoft.Windows.GdiPlus_6595b64144ccf1df_x-ww_4e8510ac\1.0.6002.23084.Policy	112
0x2215c28	\WINDOWS\system32\netlogon.dll	112
0x2216028	\Documents and Settings\All Users\Start Menu\Programs\Accessories\System Tools\desktop.ini	112
0x2216510	\WINDOWS\system32\pstorsvc.dll	112
0x22168f8	\WINDOWS\system32\wdigest.dll	112
0x2216f28	\WINDOWS\system32\msxml3r.dll	112
0x2217200	\WINDOWS\system32\wbem	112
0x2217528	\Intel\ivecuqmanpnirkt615\msg\m_spanish.wnry	112
0x2217668	\WINDOWS\system32\netmsg.dll	112
0x2217a90	\WINDOWS\system32\iphlpapi.dll	112
0x2217cd0	\WINDOWS\system32\rasmans.dll	112
0x2217f90	\WINDOWS\pchealth\helpctr\binaries\pchsvc.dll	112
0x2218320	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Entertainment\Volume Control.lnk	112
0x22184b0	\WINDOWS\system32\netman.dll	112
0x2218800	\WINDOWS\system32\winspool.drv	112
0x2218c28	\WINDOWS\system32\schannel.dll	112
0x22193f0	\$Directory	112
0x22195a8	\WINDOWS\system32\dmserver.dll	112
0x22199d0	\WINDOWS\system32\certcli.dll	112
0x2219b30	\Intel\ivecuqmanpnirkt615\msg\m_slovak.wnry	112
0x2219df8	\WINDOWS\system32\themeui.dll	112
0x221aa90	\WINDOWS\system32\msapsspc.dll	112
0x221aeb8	\WINDOWS\system32\lmhsvc.dll	112
0x221b3d8	\WINDOWS\system32\uxtheme.dll	112
0x221b800	\WINDOWS\system32\msacm32.dll	112
0x221bc28	\WINDOWS\system32\winmm.dll	112
0x221ceb8	\WINDOWS\system32\msvcrt40.dll	112
0x221d3d8	\WINDOWS\system32\w32time.dll	112
0x221dad8	\Documents and Settings\All Users\Start Menu\Programs\Games\Freecell.lnk	112
0x221dd00	\WINDOWS\system32\es.dll	112
0x221e4b0	\WINDOWS\system32\scesrv.dll	112
0x221ed20	\WINDOWS\system32\kerberos.dll	112
0x221f668	\WINDOWS\AppPatch\AcGenral.dll	112
0x221fb90	\Documents and Settings\All Users\Start Menu\Programs\Games\Internet Hearts.lnk	112
0x221fd20	\WINDOWS\system32\dnsrslvr.dll	112
0x2220668	\WINDOWS\system32\shgina.dll	112
0x2220a90	\WINDOWS\system32\comres.dll	112
0x2220e98	\WINDOWS\system32\umpnpmgr.dll	112
0x22213d8	\WINDOWS\system32\cryptdll.dll	112
0x2221800	\WINDOWS\system32\samsrv.dll	112
0x2221c28	\WINDOWS\system32\samlib.dll	112
0x2222028	\WINDOWS\ime\imkr6_1\dicts	112
0x22239d0	\WINDOWS\system32\rasapi32.dll	112
0x2223df8	\WINDOWS\system32\adsldpc.dll	112
0x22243b8	\WINDOWS\system32\activeds.dll	112
0x2225128	\WINDOWS\system32\crypt32.dll	112
0x22259d0	\WINDOWS\system32\mprapi.dll	112
0x2225df8	\WINDOWS\system32\cryptui.dll	112
0x2226740	\WINDOWS\system32\rastls.dll	112
0x2226ab0	\WINDOWS\system32\drivers\fips.sys	112
0x2226eb8	\WINDOWS\system32\userinit.exe	112
0x2227128	\WINDOWS\system32\msasn1.dll	112
0x2227d20	\WINDOWS\system32\powrprof.dll	112
0x2228668	\WINDOWS\system32\cscui.dll	112
0x2228eb8	\WINDOWS\system32\atl.dll	112
0x2229158	\WINDOWS\system	112
0x2229320	\WINDOWS\system32\ctfmon.exe	112
0x22293d8	\WINDOWS\system32\logonui.exe	112
0x2229748	\Intel\ivecuqmanpnirkt615\msg\m_vietnamese.wnry	112
0x22298d8	\WINDOWS\system32\eappcfg.dll	112
0x2229c28	\WINDOWS\system32\tspkg.dll	112
0x222a028	\Endpoint	112
0x222a4d0	\WINDOWS\system32\mswsock.dll	112
0x222a8f8	\WINDOWS\system32\rtutils.dll	112
0x222ad20	\WINDOWS\system32\wlnotify.dll	112
0x222b220	\WINDOWS\system32\dimsntfy.dll	112
0x222b648	\WINDOWS\system32\cscdll.dll	112
0x222ba90	\WINDOWS\system32\oleacc.dll	112
0x222bc68	\WINDOWS\system32\ega.cpi	112
0x222beb8	\WINDOWS\system32\msimg32.dll	112
0x222c320	\Documents and Settings\All Users\Start Menu\Programs\Accessories\System Tools\Backup.lnk	112
0x222c3d8	\WINDOWS\system32\rasadhlp.dll	112
0x222c800	\WINDOWS\system32\winrnr.dll	112
0x222d028	\WINDOWS\system32\muweb.dll	112
0x222d4b0	\WINDOWS\system32\clbcatq.dll	112
0x222d8f8	\WINDOWS\system32\wzcsvc.dll	112
0x222dd20	\WINDOWS\system32\eventlog.dll	112
0x222e340	\WINDOWS\system32\dbghelp.dll	112
0x222e800	\WINDOWS\system32\dnsapi.dll	112
0x222ec08	\WINDOWS\system32\wshtcpip.dll	112
0x222f028	\Documents and Settings\All Users\Start Menu\Programs\Games\desktop.ini	112
0x222f4b0	\WINDOWS\system32\dot3api.dll	112
0x222f8d8	\WINDOWS\system32\hnetcfg.dll	112
0x222fc10	\Documents and Settings\LocalService\Local Settings\History\History.IE5\index.dat	112
0x2230668	\WINDOWS\system32\wmi.dll	112
0x2230ab0	\WINDOWS\system32\eapolqec.dll	112
0x2230eb8	\WINDOWS\system32\qutil.dll	112
0x2231158	\WINDOWS\msagent	112
0x22313d8	\WINDOWS\system32\esent.dll	112
0x22316b0	\System Volume Information\_restore{915C6505-6DED-4903-B727-F8B5C05262FF}\drivetable.txt	112
0x2231800	\WINDOWS\system32\xpsp2res.dll	112
0x2231c28	\WINDOWS\system32\rpcss.dll	112
0x2232418	\Intel\ivecuqmanpnirkt615\msg\m_swedish.wnry	112
0x22324d0	\WINDOWS\system32\ntmarta.dll	112
0x22328f8	\WINDOWS\system32\svchost.exe	112
0x2232d20	\WINDOWS\system32\scecli.dll	112
0x2232f28	\Documents and Settings\All Users\Start Menu\Programs\Administrative Tools\Computer Management.lnk	112
0x2233240	\WINDOWS\system32\wtsapi32.dll	112
0x2233518	\WINDOWS\system32\wbem\Repository\$WinMgmt.CFG	112
0x2233668	\WINDOWS\system32\winscard.dll	112
0x2233d20	\WINDOWS\system32\ntdsapi.dll	112
0x2233f18	\Intel\ivecuqmanpnirkt615	112
0x2234028	\WINDOWS\system32\drprov.dll	112
0x22345c0	\WINDOWS\system32\attrib.exe	112
0x2234688	\Documents and Settings\All Users\Start Menu\Programs\Games\Spider Solitaire.lnk	112
0x2234808	\WINDOWS\system32\rundll32.exe	112
0x2234b68	\WINDOWS\system32\cryptsvc.dll	112
0x2234f90	\WINDOWS\system32\webclnt.dll	112
0x22354b0	\WINDOWS\system32\midimap.dll	112
0x22358d8	\WINDOWS\system32\msacm32.drv	112
0x2235e00	\Documents and Settings\donny\Local Settings\Temp\24d004a104d4d54034dbcffc2a4b19a11f39008a575aa614ea04703480b1022c.bin	112
0x2235f90	\WINDOWS\system32\wdmaud.drv	112
0x2236320	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Internet Browser Choice.lnk	112
0x22364b0	\WINDOWS\system32\wkssvc.dll	112
0x22368d8	\WINDOWS\system32\audiosrv.dll	112
0x2236d78	\WINDOWS\Prefetch\TASKSE.EXE-02A1B304.pf	112
0x2236f90	\WINDOWS\system32\spoolsv.exe	112
0x2237158	\WINDOWS\msagent\intl	112
0x2237320	\WINDOWS\system32\shell32.dll	112
0x22374b0	\WINDOWS\system32\msidle.dll	112
0x22378d8	\WINDOWS\system32\schedsvc.dll	112
0x2238028	\Documents and Settings\donny\NetHood	112
0x2238758	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x22389d0	\WINDOWS\system32\wbem\wmisvc.dll	112
0x2238df8	\$Directory	112
0x2238ef8	\Documents and Settings\All Users\Start Menu\Programs\Accessories\WordPad.lnk	112
0x2238f90	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Remote Desktop Connection.lnk	112
0x2239028	\WINDOWS\system32\ulib.dll	112
0x2239668	\WINDOWS\system32\msv1_0.dll	112
0x2239f90	\WINDOWS\system32\desk.cpl	112
0x223a320	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x223a4b0	\WINDOWS\system32\shdocvw.dll	112
0x223a8d8	\WINDOWS\system32\wzcsapi.dll	112
0x223ab70	\WINDOWS\system32\rasmans.dll	112
0x223ad00	\WINDOWS\system32\eappprxy.dll	112
0x223b028	\System Volume Information\_restore{915C6505-6DED-4903-B727-F8B5C05262FF}\RP3\rp.log	112
0x223b320	\Documents and Settings\donny\Start Menu\Programs\Accessories\System Tools\Internet Explorer (No Add-ons).lnk	112
0x223b4d0	\WINDOWS\system32\dpcdll.dll	112
0x223b9d0	\WINDOWS\system32\vssapi.dll	112
0x223bad0	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x223bdf8	\WINDOWS\system32\netshell.dll	112
0x223c478	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Communications\Network Setup Wizard.lnk	112
0x223c518	\WINDOWS\system32\comres.dll	112
0x223c5b0	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x223c740	\WINDOWS\system32\tapi32.dll	112
0x223c8a0	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Communications\HyperTerminal.lnk	112
0x223cb68	\WINDOWS\system32\rasman.dll	112
0x223cf90	\WINDOWS\system32\termsrv.dll	112
0x223d8d8	\WINDOWS\system32\wbem\ncprov.dll	112
0x223dd00	\WINDOWS\system32\wuapi.dll	112
0x223e028	\Documents and Settings\donny\Start Menu\Programs\Accessories\Accessibility\On-Screen Keyboard.lnk	112
0x223e3e8	\$Directory	112
0x223e5a8	\WINDOWS\system32\onex.dll	112
0x223e9d0	\WINDOWS\system32\dot3dlg.dll	112
0x223edf8	\WINDOWS\system32\credui.dll	112
0x223fb68	\WINDOWS\explorer.exe	112
0x223ff90	\WINDOWS\system32\raschap.dll	112
0x22404b0	\WINDOWS\system32\riched20.dll	112
0x2240800	\WINDOWS\system32\dssenh.dll	112
0x2240c08	\WINDOWS\system32\wuauclt.exe	112
0x2240f90	\$Directory	112
0x22415a8	\WINDOWS\system32\browseui.dll	112
0x2241708	\DAV RPC SERVICE	112
0x2241d00	\WINDOWS\system32\wbem\wbemprox.dll	112
0x2242240	\WINDOWS\system32\msi.dll	112
0x2242478	\Documents and Settings\donny\Start Menu\Programs\Accessories\Windows Explorer.lnk	112
0x2242648	\WINDOWS\system32\colbact.dll	112
0x22428a0	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Paint.lnk	112
0x2242a90	\WINDOWS\system32\comsvcs.dll	112
0x2242c10	\Documents and Settings\All Users\Start Menu\Programs\7-Zip\7-Zip Help.lnk	112
0x2242d40	\Documents and Settings\All Users\Start Menu\Programs\Accessories\System Tools\Disk Defragmenter.lnk	112
0x2242dd8	\Documents and Settings\donny\Start Menu\desktop.ini	112
0x2242eb8	\WINDOWS\system32\wbem\wbemcons.dll	112
0x2243320	\WINDOWS\system32\sysmon.ocx	112
0x22434b0	\WINDOWS\system32\msutb.dll	112
0x2243d00	\WINDOWS\system32\actxprxy.dll	112
0x2244648	\WINDOWS\system32\icaapi.dll	112
0x2244a70	\WINDOWS\system32\mstlsapi.dll	112
0x2244bd8	\Endpoint	112
0x22453d8	\WINDOWS\system32\tcpmon.dll	112
0x22456e0	\Intel\ivecuqmanpnirkt615	112
0x2245800	\WINDOWS\system32\wbem\repdrvfs.dll	112
0x2245d00	\$Directory	112
0x2246028	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Entertainment\Sound Recorder.lnk	112
0x22464b0	\WINDOWS\system32\wbem\wmiutils.dll	112
0x22468f8	\WINDOWS\system32\wbem\wbemsvc.dll	112
0x2246a88	\Documents and Settings\All Users\Start Menu\Set Program Access and Defaults.lnk	112
0x2246c68	\$Directory	112
0x2246d20	\WINDOWS\system32\winhttp.dll	112
0x2246f90	\trkwks	112
0x22473f0	\Documents and Settings\donny\Start Menu\Programs\Windows Media Player.lnk	112
0x2247488	\WINDOWS\system32	112
0x22475c0	\Program Files\Internet Explorer\IEXPLORE.EXE	112
0x2247840	\WINDOWS\system32\sndvol32.exe	112
0x2247a90	\WINDOWS\system32\wuaueng.dll	112
0x2247ca0	\Documents and Settings\All Users\Start Menu\Programs\Games\Internet Backgammon.lnk	112
0x2247e70	\WINDOWS\system32\wbem\Repository\FS\INDEX.MAP	112
0x2247f08	\WINDOWS\system32\wbem\Repository\FS\MAPPING.VER	112
0x2248028	\WINDOWS\Media\Windows XP Startup.wav	112
0x2248b08	\WINDOWS\system32\wbem\Repository\FS\MAPPING2.MAP	112
0x2248ef8	\W32TIME	112
0x2248f90	\W32TIME	112
0x22490c0	\WINDOWS\system32\mshearts.exe	112
0x2249a90	\WINDOWS\system32\wuauserv.dll	112
0x2249eb8	\WINDOWS\system32\wbem\fastprox.dll	112
0x224a938	\WINDOWS\system32\c_1250.nls	112
0x224b4d0	\WINDOWS\system32\cnbjmon.dll	112
0x224b8f8	\WINDOWS\system32\spoolss.dll	112
0x224bd00	\WINDOWS\system32\ssdpapi.dll	112
0x224c028	\Documents and Settings\All Users\Start Menu\Programs\Python 2.7\Python (command line).lnk	112
0x224c740	\WINDOWS\system32\browser.dll	112
0x224ce98	\WINDOWS\system32\wups2.dll	112
0x224d320	\WINDOWS\system32\wsecedit.dll	112
0x224d3d8	\WINDOWS\system32\wups.dll	112
0x224d800	\WINDOWS\system32\wbem\wbemess.dll	112
0x224db70	\PIPE_EVENTROOT\CIMV2SCM EVENT PROVIDER	112
0x224dc28	\WINDOWS\system32\wbem\wmiprvsd.dll	112
0x224e4d0	\WINDOWS\system32\mspatcha.dll	112
0x224e708	\$Directory	112
0x224e8f8	\WINDOWS\system32\cabinet.dll	112
0x224ea80	\Documents and Settings\All Users\Start Menu\Programs\Games\Hearts.lnk	112
0x224eb18	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x224ed40	\WINDOWS\ime\SPTIP.dll	112
0x224f240	\WINDOWS\system32\sens.dll	112
0x224f418	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Calculator.lnk	112
0x224f668	\WINDOWS\system32\trkwks.dll	112
0x224fa90	\WINDOWS\system32\srsvc.dll	112
0x224fca8	\WINDOWS\system32\tapisrv.dll	112
0x224fd68	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x224fe00	\WINDOWS\system32\ntlanman.dll	112
0x224feb8	\WINDOWS\system32\seclogon.dll	112
0x22503d8	\WINDOWS\system32\psbase.dll	112
0x22505b0	\WINDOWS\system32\cleanmgr.exe	112
0x2250820	\WINDOWS\system32\wscntfy.exe	112
0x2250c28	\WINDOWS\system32\ctfmon.exe	112
0x22512c0	\Documents and Settings\All Users\Start Menu\Programs\Accessories\System Tools\Scheduled Tasks.lnk	112
0x2251840	\Documents and Settings\donny	112
0x22518d8	\WINDOWS\system32\upnp.dll	112
0x2251d40	\WINDOWS\system32\alg.exe	112
0x2251f28	\WINDOWS\system32\winmine.exe	112
0x22524d0	\WINDOWS\system32\verclsid.exe	112
0x22528f8	\WINDOWS\system32\resutils.dll	112
0x2252d20	\WINDOWS\system32\clusapi.dll	112
0x2253240	\WINDOWS\system32\wbem\wbemcomn.dll	112
0x22535b0	\WINDOWS\system32\msxml3.dll	112
0x2253668	\WINDOWS\system32\wbem\esscli.dll	112
0x2254028	\WINDOWS\WindowsUpdate.log	112
0x22552f0	\WINDOWS\system32\wbem\Repository\FS\MAPPING1.MAP	112
0x2255a60	\Documents and Settings\All Users\Start Menu	112
0x22562d8	\Program Files\MSN Gaming Zone\Windows\Rvsezm.exe	112
0x2256700	\Documents and Settings\All Users\Start Menu\Programs\Python 2.7\IDLE (Python GUI).lnk	112
0x2256c88	\Intel\ivecuqmanpnirkt615\t.wnry	112
0x2257b30	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x2257f90	\net\NtControlPipe8	112
0x22586a0	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x2258930	\WINDOWS\system32\ersvc.dll	112
0x2258a68	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Entertainment\desktop.ini	112
0x2258b88	\WINDOWS\system32\wscsvc.dll	112
0x2258eb8	\WINDOWS\system32\regsvc.dll	112
0x2259408	\Program Files\MSN Gaming Zone\Windows\chkrzm.exe	112
0x2259600	\WINDOWS\system32\ipnathlp.dll	112
0x2259858	\WINDOWS\system32\localspl.dll	112
0x2259b88	\WINDOWS\system32\ssdpsrv.dll	112
0x2259d60	\Program Files\Windows Media Player\wmplayer.exe	112
0x225a858	\WINDOWS\system32\rsaenh.dll	112
0x225aba8	\WINDOWS\system32\netcfgx.dll	112
0x225b390	\WINDOWS\system32\wsock32.dll	112
0x225b6c0	\WINDOWS\system32\mtxclu.dll	112
0x225b9f0	\WINDOWS\system32\wbem\wbemcore.dll	112
0x225bba0	\Python27\DLLs\py.ico	112
0x225ee10	\Documents and Settings\donny\NTUSER.DAT	112
0x225ef90	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x225f548	\WINDOWS\system32\wpa.dbl	112
0x225fb50	\WINDOWS\system32\cfgmgr32.dll	112
0x2262900	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x2264808	\Program Files\NetMeeting	112
0x22648a0	\WINDOWS\pchealth\helpctr\binaries	112
0x2265a40	\WINDOWS\system32\batmeter.dll	112
0x2277d10	\WINDOWS\system32\hid.dll	112
0x22783f0	\WINDOWS\system.ini	112
0x227b780	\WINDOWS\system32\wucltui.dll	112
0x227e338	\WINDOWS\system32\pjlmon.dll	112
0x227f950	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Accessibility\desktop.ini	112
0x227fb28	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x2280478	\Documents and Settings\All Users\Start Menu\Programs\Administrative Tools\Services.lnk	112
0x2280810	\WINDOWS\system32\moricons.dll	112
0x2280b60	\Documents and Settings\donny\Start Menu\Programs\Accessories\Accessibility\Utility Manager.lnk	112
0x2282728	\Documents and Settings\NetworkService\Local Settings\desktop.ini	112
0x2282ae8	\WINDOWS\system32\rasdlg.dll	112
0x2282f90	\net\NtControlPipe11	112
0x2284448	\net\NtControlPipe0	112
0x2285518	\net\NtControlPipe1	112
0x2285eb8	\WINDOWS\system32\msprivs.dll	112
0x22862a0	\WINDOWS\system32\webcheck.dll	112
0x2286460	\WINDOWS\system32\usbmon.dll	112
0x2286cc0	\WINDOWS\system32\inetpp.dll	112
0x2288980	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x228af90	\WINDOWS\system32\vga.dll	112
0x228f988	\WINDOWS\system32\authz.dll	112
0x228faf0	\WINDOWS\system32\winlogon.exe	112
0x228fbe0	\WINDOWS\system32\vga64k.dll	112
0x228fcd8	\WINDOWS\system32\vga256.dll	112
0x228fde8	\$Directory	112
0x2291f38	\WINDOWS\system32\framebuf.dll	112
0x2292c40	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x229a308	\WINDOWS\system32	112
0x229ba88	\WINDOWS\system32\nddeapi.dll	112
0x229e338	\$Directory	112
0x229ec48	\WINDOWS\system32\winsta.dll	112
0x229ed70	\WINDOWS\system32\setupapi.dll	112
0x229f028	\WINDOWS\system32\sfc.dll	112
0x229f198	\WINDOWS\system32\regapi.dll	112
0x229f270	\WINDOWS\system32\psapi.dll	112
0x229fa60	\WINDOWS\system32\netapi32.dll	112
0x229ff90	\WINDOWS\system32\profmap.dll	112
0x22a0f90	\WINDOWS\system32\msgina.dll	112
0x22a1028	\WINDOWS\system32\lsass.exe	112
0x22a1110	\WINDOWS\system32\MSCTFIME.IME	112
0x22a1238	\Winsock2\CatalogChangeListener-388-0	112
0x22a1620	\WINDOWS\system32\kbdus.dll	112
0x22a1740	\WINDOWS\system32\imm32.dll	112
0x22a1850	\WINDOWS\system32\ws2help.dll	112
0x22a32e8	\WINDOWS\system32\ws2_32.dll	112
0x22a3830	\WINDOWS\system32\wintrust.dll	112
0x22a4110	\WINDOWS\system32\services.exe	112
0x22a50e0	\$Directory	112
0x22a6d20	\Documents and Settings\All Users\Start Menu\Programs\Python 2.7\Module Docs.lnk	112
0x22a6f28	\Documents and Settings\donny\Start Menu\Programs\Accessories\Synchronize.lnk	112
0x22a7148	\WINDOWS\system32\notepad.exe	112
0x22a7340	\WINDOWS\system32\linkinfo.dll	112
0x22a7568	\WINDOWS\Fonts\framd.ttf	112
0x22a7b98	\WINDOWS\system32\rasdlg.dll	112
0x22a7e60	\WINDOWS\system32\inetpp.dll	112
0x22a8088	\WINDOWS\system32\netrap.dll	112
0x22a82a8	\WINDOWS\system32\win32spl.dll	112
0x22a84d8	\WINDOWS\system32\batmeter.dll	112
0x22a86f8	\WINDOWS\system32\stobject.dll	112
0x22a8960	\WINDOWS\system32\mlang.dll	112
0x22a8bb8	\WINDOWS\system32\webcheck.dll	112
0x22a8f28	\WINDOWS\Media\Windows XP Balloon.wav	112
0x22a9150	\WINDOWS\system32\usbmon.dll	112
0x22a9368	\WINDOWS\system32\tcpmon.dll	112
0x22a9590	\WINDOWS\system32\pjlmon.dll	112
0x22a9760	\WINDOWS\system32\cnbjmon.dll	112
0x22a9930	\WINDOWS\system32\localspl.dll	112
0x22a9be8	\WINDOWS\system32\spoolss.dll	112
0x22a9e48	\WINDOWS\system32\ssdpsrv.dll	112
0x22aa350	\WINDOWS\system32\drivers\disdn	112
0x22aa4e0	\WINDOWS\system32\ssdpapi.dll	112
0x22aa728	\WINDOWS\system32\tapisrv.dll	112
0x22aab28	\$Directory	112
0x22aabc0	\WINDOWS\ime\SPTIP.dll	112
0x22aaeb0	\WINDOWS\system32\wscntfy.exe	112
0x22ab1e8	\Documents and Settings\All Users\Start Menu\Programs\Startup\desktop.ini	112
0x22ab418	\Documents and Settings\All Users\Start Menu\Programs\Accessories\System Tools\Security Center.lnk	112
0x22ab610	\Documents and Settings\All Users\Start Menu\Programs\Accessories\System Tools\Disk Cleanup.lnk	112
0x22abb70	\$Directory	112
0x22abe00	\WINDOWS\SoftwareDistribution\ReportingEvents.log	112
0x22ac060	\$Directory	112
0x22ac0f8	\WINDOWS\system32\en-US\ieframe.dll.mui	112
0x22ac450	\$Directory	112
0x22ac4e8	\Documents and Settings\All Users\Start Menu\Programs\Python 2.7\Uninstall Python.lnk	112
0x22ac6e0	\Documents and Settings\All Users\Documents\desktop.ini	112
0x22ac8d8	\WINDOWS\system32\netcfgx.dll	112
0x22acb00	\$Directory	112
0x22acc68	\WINDOWS\system32\alg.exe	112
0x22aceb8	\WINDOWS\system32\verclsid.exe	112
0x22ad258	\$Directory	112
0x22ad2f0	\WINDOWS\system32\calc.exe	112
0x22ad620	\$Directory	112
0x22ad6b8	\WINDOWS\system32\ntbackup.exe	112
0x22ad9e8	\$Directory	112
0x22ada80	\WINDOWS\system32\sndrec32.exe	112
0x22adc78	\Documents and Settings\donny\Recent\Desktop.ini	112
0x22ae028	\Documents and Settings\All Users\Start Menu\Programs\Administrative Tools\Performance.lnk	112
0x22ae218	\$Directory	112
0x22ae2b0	\WINDOWS\system32\shimgvw.dll	112
0x22ae5e0	\$Directory	112
0x22aea68	\Program Files\Outlook Express\wab.exe	112
0x22aed98	\$Directory	112
0x22aee30	\WINDOWS\WinSxS\x86_Microsoft.Windows.GdiPlus_6595b64144ccf1df_1.0.6002.23084_x-ww_f3f35550	112
0x22af208	\Documents and Settings\donny\My Documents\My Music\Desktop.ini	112
0x22af400	\WINDOWS\system32\compatUI.dll	112
0x22af5f8	\WINDOWS\system32\ntshrui.dll	112
0x22af978	\$Directory	112
0x22afa10	\WINDOWS\system32\utilman.exe	112
0x22afbe0	\WINDOWS\system32\taskkill.exe	112
0x22afdd8	\Documents and Settings\All Users\Start Menu\Programs\Windows Movie Maker.lnk	112
0x22aff90	\Documents and Settings\donny\Start Menu\Programs\Internet Explorer.lnk	112
0x22b02b0	\WINDOWS\system32\resutils.dll	112
0x22b04d8	\WINDOWS\system32\clusapi.dll	112
0x22b0700	\WINDOWS\system32\wsock32.dll	112
0x22b0920	\WINDOWS\system32\mtxclu.dll	112
0x22b0b50	\WINDOWS\system32\colbact.dll	112
0x22b0d78	\WINDOWS\system32\comsvcs.dll	112
0x22b1148	\$Directory	112
0x22b11e0	\WINDOWS\system32\ntlsapi.dll	112
0x22b1520	\WINDOWS\system32\lz32.dll	112
0x22b15b8	\WINDOWS\system32\wbem\wbemcons.dll	112
0x22b17b8	\WINDOWS\system32\msutb.dll	112
0x22b1af8	\WINDOWS\system32\actxprxy.dll	112
0x22b1cc8	\WINDOWS\system32\mstlsapi.dll	112
0x22b1e98	\WINDOWS\system32\icaapi.dll	112
0x22b2028	\WINDOWS\system32\wuauclt.exe	112
0x22b20e8	\WINDOWS\system32\termsrv.dll	112
0x22b2448	\WINDOWS\system32\wbem\ncprov.dll	112
0x22b2698	\WINDOWS\system32\wuapi.dll	112
0x22b2a18	\WINDOWS\system32\browser.dll	112
0x22b2c80	\WINDOWS\system32\dssenh.dll	112
0x22b3508	\WINDOWS\system32\wups2.dll	112
0x22b3750	\WINDOWS\system32\wups.dll	112
0x22b3b78	\WINDOWS\system32\wbem\wbemess.dll	112
0x22b3d00	\WINDOWS\system32\mui\040D	112
0x22b3dc0	\WINDOWS\system32\mui\040C	112
0x22b3f28	\WINDOWS\system32\wbem\wmiprvsd.dll	112
0x22b4810	\WINDOWS\system32\fldrclnr.dll	112
0x22b5028	\WINDOWS\system32\cabinet.dll	112
0x22b52a0	\$Directory	112
0x22b5338	\WINDOWS\system32\wbem\Repository\FS\OBJECTS.DATA	112
0x22b5530	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x22b5728	\WINDOWS\system32\wbem\repdrvfs.dll	112
0x22b5a50	\WINDOWS\system32\wbem\wmiutils.dll	112
0x22b5c20	\WINDOWS\system32\wbem\wbemsvc.dll	112
0x22b5e70	\WINDOWS\system32\mspatcha.dll	112
0x22b6028	\Endpoint	112
0x22b62d8	\WINDOWS\system32\winhttp.dll	112
0x22b65f0	\WINDOWS\system32\wuaueng.dll	112
0x22b6e70	\WINDOWS\system32\wuauserv.dll	112
0x22b7330	\WINDOWS\system32\wbem\fastprox.dll	112
0x22b77f8	\WINDOWS\system32\wbem\esscli.dll	112
0x22b7b38	\WINDOWS\system32\wbem\wbemcore.dll	112
0x22b7f90	\WINDOWS\system32\wbem\wbemcomn.dll	112
0x22b8028	\WINDOWS\system32\seclogon.dll	112
0x22b8280	\WINDOWS\system32\wbem\wbemprox.dll	112
0x22b84a8	\WINDOWS\system32\msi.dll	112
0x22b8740	\WINDOWS\system32\wscsvc.dll	112
0x22b8938	\WINDOWS\system32\trkwks.dll	112
0x22b8b88	\WINDOWS\system32\srsvc.dll	112
0x22b8e40	\WINDOWS\system32\sens.dll	112
0x22b9288	\WINDOWS\system32\regsvc.dll	112
0x22b94b0	\	112
0x22b9960	\WINDOWS\system32\psbase.dll	112
0x22b9b88	\WINDOWS\system32\pstorsvc.dll	112
0x22b9db0	\WINDOWS\system32\netmsg.dll	112
0x22b9f90	\WINDOWS\system32\winipsec.dll	112
0x22ba1f8	\WINDOWS\system32\oakley.dll	112
0x22ba450	\WINDOWS\system32\ipsecsvc.dll	112
0x22ba6a8	\WINDOWS\system32\srvsvc.dll	112
0x22baa88	\$Directory	112
0x22bab20	\WINDOWS\pchealth\helpctr\binaries\pchsvc.dll	112
0x22bad60	\WINDOWS\system32\ersvc.dll	112
0x22baf90	\WINDOWS\system32\dmserver.dll	112
0x22bb1d0	\WINDOWS\system32\certcli.dll	112
0x22bb400	\WINDOWS\system32\cryptsvc.dll	112
0x22bb7f8	\Intel\ivecuqmanpnirkt615\00000000.pky	112
0x22bb9c8	\Documents and Settings\LocalService\Local Settings\History\History.IE5\index.dat	112
0x22bbbd8	\Documents and Settings\LocalService\Cookies\index.dat	112
0x22bbde8	\Documents and Settings\LocalService\Local Settings\Temporary Internet Files\Content.IE5\index.dat	112
0x22bbf90	\WINDOWS\system32\webclnt.dll	112
0x22bc200	\net\NtControlPipe8	112
0x22bc310	\WINDOWS\system32\sfc_os.dll	112
0x22bc688	\$Directory	112
0x22bcc50	\WINDOWS\system32\midimap.dll	112
0x22bce70	\WINDOWS\system32\msacm32.drv	112
0x22bd0d0	\WINDOWS\system32\mstsc.exe	112
0x22bd2c8	\WINDOWS\system32\BrowserChoice.exe	112
0x22bd3d0	\WINDOWS\system32\odbc32.dll	112
0x22bd610	\WINDOWS\system32\mspaint.exe	112
0x22bd868	\Topology	112
0x22bdac8	\WINDOWS\system32\mydocs.dll	112
0x22bddd0	\{9B365890-165F-11D0-A195-0020AFD156E4}	112
0x22bdf90	\WINDOWS\system32\accwiz.exe	112
0x22be268	\{9B365890-165F-11D0-A195-0020AFD156E4}	112
0x22be500	\WINDOWS\system32\wdmaud.drv	112
0x22be730	\Documents and Settings\donny\Application Data\Microsoft\Protect\CREDHIST	112
0x22bea60	\$Directory	112
0x22beaf8	\Documents and Settings\donny\Application Data\Microsoft\Protect\S-1-5-21-602162358-764733703-1957994488-1003\f6ef8b17-2d2e-43f2-ad8d-55572ca41909	112
0x22becf0	\WINDOWS\system32\wkssvc.dll	112
0x22bee00	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202\comctl32.dll	112
0x22bef28	\WINDOWS\system32\audiosrv.dll	112
0x22bf038	\$Directory	112
0x22bf350	\WINDOWS\system32\spoolsv.exe	112
0x22bf598	\WINDOWS\system32\msidle.dll	112
0x22bf9a0	\WINDOWS\system32\schedsvc.dll	112
0x22c0110	\WINDOWS\system32\stdole2.tlb	112
0x22c02e0	\WINDOWS\system32\vssapi.dll	112
0x22c05e8	\WINDOWS\system32\wbem\wmisvc.dll	112
0x22c08d0	\WINDOWS\Fonts\framdit.ttf	112
0x22c0b00	\WINDOWS\system32\MSIMTF.dll	112
0x22c0cf8	\WINDOWS\system32\themeui.dll	112
0x22c1028	\WINDOWS\system32\eappcfg.dll	112
0x22c10d8	\WINDOWS\system32\desk.cpl	112
0x22c12a8	\WINDOWS\system32\shdocvw.dll	112
0x22c16f0	\WINDOWS\system32\browseui.dll	112
0x22c1808	\$Directory	112
0x22c1950	\WINDOWS\Resources\Themes\Luna\luna.msstyles	112
0x22c1bf0	\WINDOWS\system32\wzcsapi.dll	112
0x22c1e20	\WINDOWS\system32\eappprxy.dll	112
0x22c2028	\Documents and Settings\donny\Start Menu\Programs\Accessories\Accessibility\Narrator.lnk	112
0x22c22d8	\WINDOWS\system32\onex.dll	112
0x22c2508	\WINDOWS\system32\dot3dlg.dll	112
0x22c26d8	\WINDOWS\system32\credui.dll	112
0x22c2930	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Communications\New Connection Wizard.lnk	112
0x22c2d60	\WINDOWS\system32\netman.dll	112
0x22c3028	\WINDOWS\system32\rasapi32.dll	112
0x22c34e0	\WINDOWS\system32\raschap.dll	112
0x22c3740	\WINDOWS\system32\riched20.dll	112
0x22c3968	\WINDOWS\Fonts\arialbi.ttf	112
0x22c3bc8	\WINDOWS\system32\tapi32.dll	112
0x22c3df8	\WINDOWS\system32\rasman.dll	112
0x22c4240	\WINDOWS\system32\adsldpc.dll	112
0x22c4480	\WINDOWS\system32\activeds.dll	112
0x22c46b8	\WINDOWS\system32\mprapi.dll	112
0x22c48e8	\WINDOWS\system32\cryptui.dll	112
0x22c4b30	\WINDOWS\system32\rastls.dll	112
0x22c4d98	\WINDOWS\system32\Microsoft\Protect\S-1-5-18\User\68fa1b6e-57a3-4316-98e3-8fa780aa107b	112
0x22c4f90	\WINDOWS\Fonts\arial.ttf	112
0x22c5290	\WINDOWS\system32\userinit.exe	112
0x22c54d0	\WINDOWS\system32\secupd.dat	112
0x22c56d0	\WINDOWS\system32\secupd.sig	112
0x22c58d0	\WINDOWS\system32\oembios.dat	112
0x22c5ad0	\WINDOWS\system32\oembios.sig	112
0x22c5cd0	\WINDOWS\system32\dpcdll.dll	112
0x22c5f90	\WINDOWS\system32\powrprof.dll	112
0x22c6c80	\WINDOWS\system32\cscui.dll	112
0x22c6f90	\$Directory	112
0x22c70e0	\WINDOWS\Web\Wallpaper\Bliss.bmp	112
0x22c72b0	\Intel\ivecuqmanpnirkt615\msg\m_english.wnry	112
0x22c74a8	\Documents and Settings\donny\Local Settings\desktop.ini	112
0x22c75b8	\WINDOWS\system32\shsvcs.dll	112
0x22c7720	\Documents and Settings\All Users\Start Menu\Windows Catalog.lnk	112
0x22c7e18	\WINDOWS\system32\shgina.dll	112
0x22c8190	\$Directory	112
0x22c8228	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x22c8448	\Documents and Settings\All Users\Start Menu\Programs\Administrative Tools\Data Sources (ODBC).lnk	112
0x22c8668	\WINDOWS\system32\clbcatq.dll	112
0x22c8960	\WINDOWS\system32\esent.dll	112
0x22c8ab8	\Documents and Settings\donny\NTUSER.DAT.LOG	112
0x22c8e58	\WINDOWS\system32\dot3api.dll	112
0x22c90b8	\WINDOWS\system32\qutil.dll	112
0x22c9318	\WINDOWS\system32\atl.dll	112
0x22c9558	\WINDOWS\system32\eapolqec.dll	112
0x22c9728	\WINDOWS\system32\wmi.dll	112
0x22c9930	\WINDOWS\system32\rtutils.dll	112
0x22c9b60	\WINDOWS\system32\wzcsvc.dll	112
0x22c9f28	\WINDOWS\system32\lmhsvc.dll	112
0x22ca028	\WINDOWS\system32\msimg32.dll	112
0x22ca188	\WINDOWS\system32\oleaccrc.dll	112
0x22ca578	\WINDOWS\system32\winspool.drv	112
0x22ca7c0	\WINDOWS\system32\wlnotify.dll	112
0x22ca990	\WINDOWS\system32\dimsntfy.dll	112
0x22cabb8	\WINDOWS\system32\cscdll.dll	112
0x22cadf0	\WINDOWS\system32\oleacc.dll	112
0x22cb5d8	\WINDOWS\system32\duser.dll	112
0x22cb968	\WINDOWS\system32\ntkrnlpa.exe	112
0x22cbb68	\WINDOWS\Fonts\micross.ttf	112
0x22cbe00	\WINDOWS\system32\logonui.exe.manifest	112
0x22cbf90	\WINDOWS\system32\logonui.exe	112
0x22ccad8	\WINDOWS\system32\shimgvw.dll	112
0x22cd120	\Documents and Settings\donny\Local Settings\Application Data\Microsoft\Windows\UsrClass.dat	112
0x22cf208	\WINDOWS\system32\dnsrslvr.dll	112
0x22cf3d8	\net\NtControlPipe6	112
0x22cf5d0	\WINDOWS\system32\mui\0009	112
0x22cf6e0	\WINDOWS\system32\odbcint.dll	112
0x22cf848	\Documents and Settings\donny\Local Settings\Application Data\Microsoft\Windows\UsrClass.dat.LOG	112
0x22cfbf8	\WINDOWS\system32\dhcpcsvc.dll	112
0x22cfec0	\WINDOWS\system32	112
0x22d0740	\$Directory	112
0x22d07d8	\Program Files\Common Files\System\ado	112
0x22d09d0	\WINDOWS\system32\rasadhlp.dll	112
0x22d0be0	\WINDOWS\system32\winrnr.dll	112
0x22d0e00	\WINDOWS\system32\wshtcpip.dll	112
0x22d1028	\WINDOWS\system32\config\SysEvent.Evt	112
0x22d10d8	\WINDOWS\system32\hnetcfg.dll	112
0x22d12a8	\WINDOWS\system32\mswsock.dll	112
0x22d1478	\WINDOWS\system32\ntoskrnl.exe	112
0x22d1678	\Program Files\MSN Gaming Zone\Windows	112
0x22d1870	\WINDOWS\inf	112
0x22d1a68	\Program Files\Common Files\System\Ole DB	112
0x22d1ce0	\net\NtControlPipe5	112
0x22d2120	\WINDOWS\system32\ncobjapi.dll	112
0x22d23a8	\WINDOWS\system32\config\SecEvent.Evt	112
0x22d25a0	\WINDOWS\system32\config\Internet.evt	112
0x22d28d0	\$Directory	112
0x22d2968	\WINDOWS\system32\config\AppEvent.Evt	112
0x22d2b78	\WINDOWS\system32\netevent.dll	112
0x22d2d80	\WINDOWS\system32\eventlog.dll	112
0x22d2f28	\Intel\ivecuqmanpnirkt615\tasksche.exe	112
0x22d3198	\WINDOWS\system32\rpcss.dll	112
0x22d3548	\WINDOWS\system32\ntmarta.dll	112
0x22d3780	\WINDOWS\system32\svchost.exe	112
0x22d39a0	\WINDOWS\system32\scecli.dll	112
0x22d3bd0	\WINDOWS\system32\wtsapi32.dll	112
0x22d3da0	\WINDOWS\system32\winscard.dll	112
0x22d3f90	\WINDOWS\system32\tspkg.dll	112
0x22d4240	\WINDOWS\system32\rsaenh.dll	112
0x22d4710	\WINDOWS\system32\wdigest.dll	112
0x22d48e0	\WINDOWS\system32\w32time.dll	112
0x22d4bd0	\WINDOWS\system32\netlogon.dll	112
0x22d4e00	\WINDOWS\system32\iphlpapi.dll	112
0x22d4f90	\WINDOWS\system32\msv1_0.dll	112
0x22d5598	\WINDOWS\system32\kerberos.dll	112
0x22d5850	\WINDOWS\system32\msprivs.dll	112
0x22d5a50	\WINDOWS\system32\WindowsLogon.manifest	112
0x22d5c48	\WINDOWS\system32\MSCTF.dll	112
0x22d61b0	\$Directory	112
0x22d6440	\WINDOWS\system32\msnsspc.dll	112
0x22d6610	\WINDOWS\system32\digest.dll	112
0x22d6878	\WINDOWS\system32\credssp.dll	112
0x22d6a48	\WINDOWS\system32\schannel.dll	112
0x22d6c18	\WINDOWS\system32\msvcrt40.dll	112
0x22d6de8	\WINDOWS\system32\msapsspc.dll	112
0x22d6f90	\WINDOWS\system32\uxtheme.dll	112
0x22d71c8	\WINDOWS\system32\msacm32.dll	112
0x22d7398	\WINDOWS\system32\winmm.dll	112
0x22d7568	\WINDOWS\AppPatch\AcGenral.dll	112
0x22d7840	\WINDOWS\system32\cryptdll.dll	112
0x22d7a78	\WINDOWS\system32\samsrv.dll	112
0x22d7d58	\WINDOWS\system32\samlib.dll	112
0x22d7f28	\WINDOWS\system32\dnsapi.dll	112
0x22d8388	\WINDOWS\system32\ntdsapi.dll	112
0x22d8558	\WINDOWS\AppPatch\AcAdProc.dll	112
0x22d8728	\WINDOWS\system32\shimeng.dll	112
0x22d88f8	\WINDOWS\system32\umpnpmgr.dll	112
0x22d8ac8	\WINDOWS\system32\scesrv.dll	112
0x22d8d18	\WINDOWS\system32\msvcp60.dll	112
0x22d8ec0	\WINDOWS\system32\ncobjapi.dll	112
0x22d9160	\WINDOWS\system32\lsasrv.dll	112
0x22d9330	\WINDOWS\system32\lsass.exe	112
0x22d9748	\WINDOWS\WinSxS\Policies\x86_policy.5.1.Microsoft.Windows.SystemCompatible_6595b64144ccf1df_x-ww_a0111510\5.1.2600.2000.Policy	112
0x22d9940	\WINDOWS\bootstat.dat	112
0x22d9b38	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x22d9e68	\$Directory	112
0x22da2c0	\$Directory	112
0x22da688	\$Directory	112
0x22da720	\WINDOWS\system32	112
0x22da918	\WINDOWS\system32	112
0x22dab10	\WINDOWS\system32\services.exe	112
0x22dace0	\WINDOWS\AppPatch\sysmain.sdb	112
0x22db618	\WINDOWS\system32\sfc_os.dll	112
0x22db7e8	\WINDOWS\system32\sfc.dll	112
0x22db9f8	\WINDOWS\system32\shsvcs.dll	112
0x22dbcf0	\WINDOWS\system32\odbcint.dll	112
0x22dbf00	\WINDOWS\WindowsShell.Manifest	112
0x22dc180	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202\comctl32.dll	112
0x22dc488	\$Directory	112
0x22dc520	\InitShutdown	112
0x22dc850	\$Directory	112
0x22dc8e8	\InitShutdown	112
0x22dcae0	\WINDOWS\system32\sxs.dll	112
0x22dcd50	\$Directory	112
0x22dceb8	\WINDOWS\system32\odbc32.dll	112
0x22dd168	\WINDOWS\system32\msgina.dll	112
0x22dd3b8	\WINDOWS\system32	112
0x22dd520	\WINDOWS\system32\MSCTFIME.IME	112
0x22dd6f0	\WINDOWS\Fonts\marlett.ttf	112
0x22dd8c0	\WINDOWS\Fonts\tahoma.ttf	112
0x22ddb88	\WINDOWS\Fonts\tahomabd.ttf	112
0x22ddd58	\WINDOWS\Fonts\trebucbd.ttf	112
0x22ddf28	\WINDOWS\Fonts\serife.fon	112
0x22de160	\WINDOWS\Fonts\sserife.fon	112
0x22de380	\WINDOWS\Fonts\coure.fon	112
0x22de588	\WINDOWS\Fonts\wst_swed.fon	112
0x22de788	\WINDOWS\Fonts\wst_span.fon	112
0x22de988	\WINDOWS\Fonts\wst_ital.fon	112
0x22deb88	\WINDOWS\Fonts\wst_germ.fon	112
0x22ded58	\WINDOWS\Fonts\wst_fren.fon	112
0x22def28	\WINDOWS\Fonts\wst_engl.fon	112
0x22df0e8	\WINDOWS\Fonts\wst_czec.fon	112
0x22df2b8	\WINDOWS\Fonts\symbole.fon	112
0x22df4d8	\WINDOWS\Fonts\smalle.fon	112
0x22df6a8	\WINDOWS\Fonts\modern.fon	112
0x22df878	\WINDOWS\Fonts\script.fon	112
0x22dfa80	\WINDOWS\Fonts\roman.fon	112
0x22dfc90	\WINDOWS\system32\kbdus.dll	112
0x22e0038	\$Directory	112
0x22e0278	\WINDOWS\system32\sortkey.nls	112
0x22e0488	\WINDOWS\system32\imm32.dll	112
0x22e0658	\WINDOWS\system32\ctype.nls	112
0x22e0828	\WINDOWS\system32\ws2help.dll	112
0x22e09f8	\WINDOWS\system32\ws2_32.dll	112
0x22e0c60	\WINDOWS\system32\wintrust.dll	112
0x22e0e30	\WINDOWS\system32\winsta.dll	112
0x22e1278	\WINDOWS\system32\setupapi.dll	112
0x22e1448	\WINDOWS\system32\regapi.dll	112
0x22e1680	\WINDOWS\system32\psapi.dll	112
0x22e1850	\WINDOWS\system32\netapi32.dll	112
0x22e1b60	\WINDOWS\system32\profmap.dll	112
0x22e1d30	\WINDOWS\system32\nddeapi.dll	112
0x22e1f00	\WINDOWS\system32\msasn1.dll	112
0x22e2118	\WINDOWS\system32\crypt32.dll	112
0x22e22e8	\WINDOWS\system32\authz.dll	112
0x22e2520	\WINDOWS\system32\winlogon.exe	112
0x22e2a80	\WINDOWS\Fonts\cga40woa.fon	112
0x22e2c78	\WINDOWS\Fonts\cga80woa.fon	112
0x22e2e70	\WINDOWS\Fonts\ega40woa.fon	112
0x22e39c8	\net\NtControlPipe7	112
0x22e3f90	\WINDOWS\system32\win32k.sys	112
0x22e4298	\WINDOWS\Fonts\ega80woa.fon	112
0x22e4490	\WINDOWS\Fonts\dosapp.fon	112
0x22e4858	\WINDOWS\system32\vga64k.dll	112
0x22e4a28	\WINDOWS\system32\vga256.dll	112
0x22e4bf8	\WINDOWS\system32\framebuf.dll	112
0x22e4e00	\WINDOWS\system32\vga.dll	112
0x22e4f90	\WINDOWS\Fonts\vgafix.fon	112
0x22e6560	\Documents and Settings\All Users\Start Menu\Programs\Games\Solitaire.lnk	112
0x22e67e8	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x22e7598	\WINDOWS\Fonts\vgaoem.fon	112
0x22e8208	\WINDOWS\system32\lz32.dll	112
0x22e89e8	\WINDOWS\system32\mycomput.dll	112
0x22e8e00	\Documents and Settings\All Users\Start Menu\Programs\Administrative Tools\desktop.ini	112
0x22e8f90	\WINDOWS\system32\netrap.dll	112
0x22e9228	\Documents and Settings\donny\Start Menu\Programs\Accessories\Entertainment\desktop.ini	112
0x22e92e0	\WINDOWS\system32\ntshrui.dll	112
0x22e94b8	\Documents and Settings\donny\Local Settings\Application Data\Microsoft\CD Burning	112
0x22ea158	\WINDOWS\system32\duser.dll	112
0x22ea310	\Documents and Settings\All Users\Start Menu\Programs\Games\Internet Spades.lnk	112
0x22eaa90	\WINDOWS\system32\linkinfo.dll	112
0x22eac68	\Documents and Settings\All Users\Desktop	112
0x22eaf90	\WINDOWS\system32\mstask.dll	112
0x22eb408	\browser	112
0x22eb4a8	\WINDOWS\Registration\R000000000007.clb	112
0x22eb660	\Documents and Settings\All Users\Start Menu\Programs\Games\Internet Reversi.lnk	112
0x22eba78	\WINDOWS\system32\charmap.exe	112
0x22ec358	\Documents and Settings\All Users\Start Menu\Programs\Games\Pinball.lnk	112
0x22ec718	\Intel\ivecuqmanpnirkt615\c.wnry	112
0x22ecb80	\Documents and Settings\All Users\Start Menu\Programs\Accessories\Communications\desktop.ini	112
0x22ecf90	\WINDOWS\system32\drivers\dxg.sys	112
0x22ed0a8	\WINDOWS\Fonts\vgasys.fon	112
0x22ed530	\WINDOWS\system32\usp10.dll	112
0x22ed9c0	\WINDOWS\system32\Restore\rstrui.exe	112
0x22ee398	\WINDOWS\system32\osk.exe	112
0x22ee620	\WINDOWS\system32\sxs.dll	112
0x22ee9a8	\WINDOWS\system32\odbcad32.exe	112
0x22eeec0	\WINDOWS\system32\lpk.dll	112
0x22ef0c8	\WINDOWS\system32\FNTCACHE.DAT	112
0x22ef3e0	\WINDOWS\system32\sorttbls.nls	112
0x22ef8d8	\WINDOWS\system32\locale.nls	112
0x22f04b0	\WINDOWS\system32\unicode.nls	112
0x22f06f8	\Intel\ivecuqmanpnirkt615\msg\m_romanian.wnry	112
0x22f0840	\WINDOWS\system32\riched32.dll	112
0x22f08f8	\WINDOWS\AppPatch\AcAdProc.dll	112
0x22f0b10	\Documents and Settings\All Users\Start Menu\Programs\Accessories\desktop.ini	112
0x22f0d50	\WINDOWS\system32\winsrv.dll	112
0x22f0f28	\WINDOWS\system32\spider.exe	112
0x22f1390	\WINDOWS\system32\basesrv.dll	112
0x22f1578	\WINDOWS\system32\csrsrv.dll	112
0x22f18c8	\WINDOWS\system32\csrss.exe	112
0x22f2028	\$Directory	112
0x22f2258	\WINDOWS\system32\config\software	112
0x22f2490	\WINDOWS\system32\config\SECURITY.LOG	112
0x22f2a38	\WINDOWS\system32	112
0x22f2b70	\WINDOWS\system32\kernel32.dll	112
0x22f3028	\WINDOWS\system32\shimeng.dll	112
0x22f3510	\$Directory	112
0x22f3cb8	\WINDOWS\system32\msvcp60.dll	112
0x22f3e58	\WINDOWS\system32\drivers\dxg.sys	112
0x22f60f8	\WINDOWS\system32\lsasrv.dll	112
0x22f66a0	\Documents and Settings\donny\Start Menu\Programs\Accessories\Accessibility\Magnifier.lnk	112
0x22f6738	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x22f6978	\WINDOWS\system32\imagehlp.dll	112
0x22f6c98	\WINDOWS\system32\gdi32.dll	112
0x2328270	\WINDOWS\system32\autochk.exe	112
0x2328308	\$Directory	112
0x23286e8	\$Mft	112
0x23287f0	\$Directory	112
0x2328888	\$Directory	112
0x2328920	\WINDOWS\system32\ntdll.dll	112
0x2328b20	\net\NtControlPipe3	112
0x2328bb8	\WINDOWS\ime\CHTIME\Applets	112
0x2329450	\WINDOWS\system32\cmd.exe	112
0x2329638	\WINDOWS\system32\cmd.exe	112
0x2329aa8	\$Directory	112
0x2329f28	\WINDOWS\system32\ntvdm.exe	112
0x232a1a0	\WINDOWS\system32\msvcrt.dll	112
0x232a370	\$Directory	112
0x232a530	\Documents and Settings\All Users\Start Menu\Programs\7-Zip\7-Zip File Manager.lnk	112
0x232a5c8	\Documents and Settings\All Users\Start Menu\Programs\Administrative Tools\Event Viewer.lnk	112
0x232a820	\WINDOWS\system32\xpsp2res.dll	112
0x232aa10	\Program Files\Windows NT\hypertrm.exe	112
0x232acd0	\WINDOWS\system32\olecnv32.dll	112
0x232b1d0	\$Directory	112
0x232b5e8	\WINDOWS\system32\wininet.dll	112
0x232b680	\WINDOWS\system32	112
0x232bb30	\WINDOWS\system32\config\default.LOG	112
0x235c3c0	\WINDOWS\AppPatch\drvmain.sdb	112
0x235cc80	\WINDOWS\system32\win32spl.dll	112
0x235e950	\$BitMap	112
0x235ede0	\WINDOWS\system32\secur32.dll	112
0x235ee78	\WINDOWS\system32\shlwapi.dll	112
0x235ef90	\$Directory	112
0x23637d8	\WINDOWS\system32\mpr.dll	112
0x23644e8	\$Directory	112
0x2364a50	\WINDOWS\system32\wldap32.dll	112
0x2364b60	\WINDOWS\system32\mpr.dll	112
0x2364e98	\WINDOWS\system32\olesvr32.dll	112
0x2365848	\WINDOWS\system32\win32k.sys	112
0x2367640	\WINDOWS\system32\shell32.dll	112
0x2368b98	\$Directory	112
0x2368cc0	\WINDOWS\system32\oleaut32.dll	112
0x2368f90	\net\NtControlPipe4	112
0x236d328	\WINDOWS\system32\userenv.dll	112
0x236d660	\WINDOWS\system32\ole32.dll	112
0x236d860	\$MftMirr	112
0x236de80	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x236df90	\WINDOWS\system32\drivers\etc\hosts	112
0x236e1b8	\WINDOWS\system32\csrss.exe	112
0x236e388	\$Directory	112
0x236ef90	\WINDOWS\system32\wow32.dll	112
0x23704f8	\$Directory	112
0x2370888	\WINDOWS\system32\config\default	112
0x2370c00	\$Directory	112
0x2370cd0	\WINDOWS\system32\urlmon.dll	112
0x2370e78	\$Directory	112
0x2370f90	\WINDOWS\system32\config\system.LOG	112
0x23711d8	\WINDOWS\system32\wininet.dll	112
0x23716e8	\$Directory	112
0x2371820	\WINDOWS\system32\url.dll	112
0x2371bb8	\WINDOWS\system32\csrsrv.dll	112
0x2371cd0	\WINDOWS\system32	112
0x2371e10	\WINDOWS\system32\comdlg32.dll	112
0x23728b0	\Program Files\Movie Maker\moviemk.exe	112
0x2372f90	\$Directory	112
0x2373438	\WINDOWS\system32\comdlg32.dll	112
0x2373550	\WINDOWS\system32\advapi32.dll	112
0x2373618	\WINDOWS\system32\sfcfiles.dll	112
0x2373708	\WINDOWS\system32\lpk.dll	112
0x2373e90	\WINDOWS\system32\ole32.dll	112
0x2373f28	\WINDOWS\system32\ntdll.dll	112
0x23753b0	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x23756b0	\WINDOWS	112
0x2375d30	\WINDOWS\system32\stobject.dll	112
0x2377078	\WINDOWS\system32\version.dll	112
0x2377298	\$Directory	112
0x23774e0	\WINDOWS\system32\iertutil.dll	112
0x2377608	\WINDOWS\system32\gdi32.dll	112
0x2377770	\WINDOWS\system32\msvcrt.dll	112
0x2377870	\WINDOWS\system32\user32.dll	112
0x2388178	\WINDOWS\system32\wuaucpl.cpl	112
0x2388488	\$Directory	112
0x2388578	\WINDOWS\system32\userenv.dll	112
0x2388748	\$Directory	112
0x2388918	\$Mft	112
0x2389168	\$Directory	112
0x2389288	\WINDOWS\system32\urlmon.dll	112
0x23895b0	\$Directory	112
0x2389f90	\$Directory	112
0x238a0b8	\WINDOWS\system32\comctl32.dll	112
0x238a150	\$Directory	112
0x238ac88	\WINDOWS\system32\ieframe.dll	112
0x238ae58	\$Directory	112
0x238b440	\WINDOWS\system32\shlwapi.dll	112
0x238b4d8	\WINDOWS\system32\wldap32.dll	112
0x2390178	\WINDOWS\system32\rpcrt4.dll	112
0x23903b0	\WINDOWS\system32\apphelp.dll	112
0x23904b0	\WINDOWS\system32\kernel32.dll	112
0x23906a8	\$Directory	112
0x2391d30	\WINDOWS\system32\smss.exe	112
0x2392238	\$Directory	112
0x2392618	\Program Files\Windows NT\Pinball\PINBALL.EXE	112
0x23927a0	\WINDOWS\system32\mobsync.exe	112
0x2392870	\Program Files\7-Zip\7zFM.exe	112
0x2393370	\WINDOWS\system32\rpcrt4.dll	112
0x2393518	\$Directory	112
0x2393d38	\WINDOWS\SoftwareDistribution\DataStore\Logs\tmp.edb	112
0x23941a8	\WINDOWS\system32\usp10.dll	112
0x2394c48	\$Directory	112
0x23952a8	\WINDOWS\system32\iertutil.dll	112
0x23954b8	\WINDOWS\system32\olecli32.dll	112
0x23956a8	\WINDOWS\system32\version.dll	112
0x2395830	\WINDOWS\system32\config\AppEvent.Evt	112
0x2395bc0	\WINDOWS\system32\user32.dll	112
0x2395f90	\WINDOWS\system32\olethk32.dll	112
0x239a3d0	\$Directory	112
0x239b410	\WINDOWS\system32\comctl32.dll	112
0x239b5c0	\$Directory	112
0x239b6d0	\$Directory	112
0x239b928	\WINDOWS\system32\config\SAM.LOG	112
0x239bb80	\WINDOWS\system32\config\SAM	112
0x239c690	\WINDOWS\system32\sfcfiles.dll	112
0x239c790	\$Directory	112
0x239f478	\WINDOWS\system32\dfrgres.dll	112
0x239f6d0	\Documents and Settings\donny\Desktop	112
0x239f928	\Documents and Settings\donny\PrintHood	112
0x239fb80	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x239fc78	\$Directory	112
0x239ff28	\WINDOWS\system32	112
0x23a0238	\WINDOWS\system32\tourstart.exe	112
0x23a0370	\WINDOWS\hh.exe	112
0x23a0788	\Documents and Settings\All Users\Start Menu\Microsoft Update.lnk	112
0x23a0820	\WINDOWS\system32\msxml3.dll	112
0x23a0cd0	\WINDOWS\WinSxS\x86_Microsoft.Windows.Common-Controls_6595b64144ccf1df_6.0.2600.6028_x-ww_61e65202	112
0x23a1aa0	\Program Files\MSN Gaming Zone\Windows\shvlzm.exe	112
0x23a1c28	\Documents and Settings\donny\Desktop\PIL-1.1.7.win32-py2.7.exe	112
0x23a2330	\WINDOWS\system32\sol.exe	112
0x23a2aa0	\WINDOWS\system32\usmt\migwiz.exe	112
0x23a2bc0	\Documents and Settings\All Users\Start Menu\Programs\Administrative Tools\Component Services.lnk	112
0x23a2c90	\Program Files\Windows NT\Accessories\wordpad.exe	112
0x23a72f8	\$Directory	112
0x23a7458	\WINDOWS\system32\ieframe.dll	112
0x23a7558	\WINDOWS\system32\advapi32.dll	112
0x23aa0c0	\WINDOWS\system32\autochk.exe	112
0x23aa360	\WINDOWS\system32\basesrv.dll	112
0x23aa668	\WINDOWS\system32\winsrv.dll	112
0x23aac88	\WINDOWS\system32\apphelp.dll	112
0x23aadc0	\$Directory	112
0x23aae58	\WINDOWS\system32\normaliz.dll	112
0x23cd490	\WINDOWS\system32\mlang.dll	112
0x23ce268	\WINDOWS\system32\normaliz.dll	112
0x23ce300	\$Directory	112
0x23ce698	\WINDOWS\system32\imagehlp.dll	112
0x23ceb60	\$LogFile	112
0x23cec88	\$Directory	112
0x23ced58	\WINDOWS\system32\oleaut32.dll	112
0x23cee58	\WINDOWS\system32\secur32.dll	112
0x23cef90	\$Directory	112
0x23eb8e8	\{9B365890-165F-11D0-A195-0020AFD156E4}	112
```

  

### DllList

This plugin lists the loaded modules in a particular Windows memory image. Due to a text limitation, this one won't have a View Results icon.

Terminal

```powershell
root@MACHINE_IP:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ vol3 -f wcry.mem windows.dlllist.DllList
Volatility 3 Framework 2.0.0
Progress:  100.00		PDB scanning finished
```

  

### PsScan

This plugin is used to scan for processes present in a particular Windows memory image.

Terminal

```powershell
root@MACHINE_IP:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ vol3 -f wcry.mem windows.psscan.PsScan
Volatility 3 Framework 2.0.0
Progress:  100.00		PDB scanning finished
```

**View Results**

Terminal

```powershell
PID	PPID	ImageFileName	Offset(V)	Threads	Handles	SessionId	Wow64	CreateTime	ExitTime	File output
860	1940	taskdl.exe	0x1f4daf0	0	-	0	False	2017-05-12 21:26:23.000000 	2017-05-12 21:26:23.000000 	Disabled
536	1940	taskse.exe	0x1f53d18	0	-	0	False	2017-05-12 21:26:22.000000 	2017-05-12 21:26:23.000000 	Disabled
424	1940	@WanaDecryptor@	0x1f69b50	0	-	0	False	2017-05-12 21:25:52.000000 	2017-05-12 21:25:53.000000 	Disabled
1768	1024	wuauclt.exe	0x1f747c0	7	132	0	False	2017-05-12 21:22:52.000000 	N/A	Disabled
576	1940	@WanaDecryptor@	0x1f8ba58	0	-	0	False	2017-05-12 21:26:22.000000 	2017-05-12 21:26:23.000000 	Disabled
260	664	svchost.exe	0x1fb95d8	5	105	0	False	2017-05-12 21:22:18.000000 	N/A	Disabled
740	1940	@WanaDecryptor@	0x1fde308	2	70	0	False	2017-05-12 21:22:22.000000 	N/A	Disabled
1168	1024	wscntfy.exe	0x1fea8a0	1	37	0	False	2017-05-12 21:22:56.000000 	N/A	Disabled
544	664	alg.exe	0x2010020	6	101	0	False	2017-05-12 21:22:55.000000 	N/A	Disabled
1084	664	svchost.exe	0x203b7a8	6	72	0	False	2017-05-12 21:22:03.000000 	N/A	Disabled
596	348	csrss.exe	0x2161da0	12	352	0	False	2017-05-12 21:22:00.000000 	N/A	Disabled
348	4	smss.exe	0x2169020	3	19	N/A	False	2017-05-12 21:21:55.000000 	N/A	Disabled
620	348	winlogon.exe	0x216e020	23	536	0	False	2017-05-12 21:22:01.000000 	N/A	Disabled
676	620	lsass.exe	0x2191658	23	353	0	False	2017-05-12 21:22:01.000000 	N/A	Disabled
664	620	services.exe	0x21937f0	15	265	0	False	2017-05-12 21:22:01.000000 	N/A	Disabled
1024	664	svchost.exe	0x21af7e8	79	1366	0	False	2017-05-12 21:22:03.000000 	N/A	Disabled
904	664	svchost.exe	0x21b5230	9	227	0	False	2017-05-12 21:22:03.000000 	N/A	Disabled
1152	664	svchost.exe	0x21bea78	10	173	0	False	2017-05-12 21:22:06.000000 	N/A	Disabled
1636	1608	explorer.exe	0x21d9da0	11	331	0	False	2017-05-12 21:22:10.000000 	N/A	Disabled
1484	664	spoolsv.exe	0x21e2da0	14	124	0	False	2017-05-12 21:22:09.000000 	N/A	Disabled
1940	1636	tasksche.exe	0x2218da0	7	51	0	False	2017-05-12 21:22:14.000000 	N/A	Disabled
836	664	svchost.exe	0x221a2c0	19	211	0	False	2017-05-12 21:22:02.000000 	N/A	Disabled
1956	1636	ctfmon.exe	0x2231da0	1	86	0	False	2017-05-12 21:22:14.000000 	N/A	Disabled
4	0	System	0x23c8830	51	244	N/A	False	N/A	N/A	Disabled
```

  

### Malfind

This plugin is used to lists process memory ranges that potentially contain injected code. There won't be any View Results icon for this one due to text limitation.

Terminal

```powershell
root@MACHINE_IP:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ vol3 -f wcry.mem windows.malfind.Malfind
Volatility 3 Framework 2.0.0
Progress:  100.00		PDB scanning finished
```

  

For more information regarding other plugins, you may check this [link(opens in new tab)](https://volatility3.readthedocs.io/en/stable/volatility3.plugins.html).

Now, you have the plugins running individually and seeing the result. What you will do now is process this in bulk. Remember, one of the investigative practices involves preprocessing evidence and saving the results to text files, right? The question is how?

The answer? Do a loop statement! See the command below.

Terminal

```powershell
root@MACHINE_IP:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pstree.PsTree windows.pslist.PsList windows.cmdline.CmdLine windows.filescan.FileScan windows.dlllist.DllList; do vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt; done
```

Let’s break this command down, shall we?

- We created a variable named `$plugin` with values of each volatility plugin
- Then ran vol3 parameters `-q`, which means quiet mode or does not show the progress in the terminal
- And `-f,` which means read from the memory capture.
- The `plugin > wcry.plugin.done;` means run volatility with the plugins and output it to a file with wcry at the beginning of the text, followed by the name of the plugins and with an extension of `.txt`. Repeat until the value of variable $plugin is used.

After running the command, you won't see any output from the terminal; you'll see files within the same directory where you ran the command.

![This image shows the desired output of running the command from the instructions. You should be able to see seven text files generated from running the loop statement](https://cdn-images.tryhackme.com/user-uploads/5e6bbe59a46ee9407fd65bbe/room-content/5e6bbe59a46ee9407fd65bbe-1727001460357.png)

  

### Preprocessing With Strings

Next, we will preprocess the memory image with the Linux strings utility. We will extract the **ASCII**, 16-bit **little-endian**, and 16-bit **big-endian** strings. See the command below.

Terminal

```powershell
root@MACHINE_IP:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ strings wcry.mem > wcry.strings.ascii.txt
root@MACHINE_IP:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ strings -e l  wcry.mem > wcry.strings.unicode_little_endian.txt
root@MACHINE_IP:/home/ubuntu/Desktop/tasks/Wcry_memory_image$ strings -e b  wcry.mem > wcry.strings.unicode_big_endian.txt
```

The strings command extracts printable ASCII text. The `-e l` option tells strings to extract 16-bit little endian strings. The `-e b` option tells strings to extract 16-bit big endian strings. All three string formats can provide useful information about the system under investigation.

You should have the same output below.

![This image shows the desired output when you run the command as per instructions. You should have at least three text files generated from running the command.](https://cdn-images.tryhackme.com/user-uploads/5e6bbe59a46ee9407fd65bbe/room-content/5e6bbe59a46ee9407fd65bbe-1727002235999.png)