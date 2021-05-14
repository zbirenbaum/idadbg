# idadbg
Compilation instructions for idadbg (ida pintool)
# Disclaimer(s):
From: https://www.hex-rays.com/wp-content/uploads/2019/12/pin_tutorial.pdf 
-"Before using the PIN tracer the PIN tool module (distributed only in source code form) must be
built as the Intel PIN license disallows redistributing PIN tools in binary form"

(Very hard pdf to find for some reason, missing from ida site and some sites listing this paywalled? The instructions are awful and useless so don't bother with it)

In accordance with "Intel Bullshit" make sure you DO NOT download my ALREADY COMPILED versions of the dll because that would make the boys at intel and IDA real sad

# Instructions:
So if you decided not to download my sketchy dll here's what ya wanna do kiddos
1. Download Pin Tool: https://software.intel.com/content/www/us/en/develop/articles/pin-a-binary-instrumentation-tool-downloads.html
2. Download ida PIN tool(idadbg source): https://www.hex-rays.com/download-center/
3. Place extracted idapin directory in $(PIN_ROOT)/source/tools
4. Disregard all ida documentation because it's dogshit and doesn't work
5. Duplicate 'MyPinTool' directory after building it successfully as a test, keep a backup
6. Copy idadbg.cpp, idadbg.h, idadbg_local.h from idapin to "MyPinTool"
7. Delete all code in MyPinTool.cpp, replace with the code from idadbg.cpp (headers are fine to keep as is, they'll import properly)
8. goto Project > Properties > C/C++ > Command line:
9. Select: Configuration: (All Configurations) and Platform: (All Platforms) to avoid doing the next step 2+ times
10. Add flag /D_WINDOWS_H_PATH_="/D_WINDOWS_H_PATH_="C:/Program Files (x86)/Windows Kits/$(winversion)/Include/$(sdkversion)/um" to additional options
example: $(winversion)=10, $(sdkversion)=10.0.17763.0 (I did this on that sdk version with v142 toolkit in VStudio 2019 Community)
11. Build that fucker, preferably after selecting release. Do it for x64, Win32/x86, or both, but keep track of which is which
12. You will have dlls in the new x64/Release and Release directories. Make a directory called idadbg with two subdirectories, x86 and x64
13. Place the dll from x64/Release into idadbg/x64 and the dll from Release into x86
14. Rename both dlls to "idadbg.dll" instead of "MyPinTool.dll"
15. Select the Pin Tracer debugger, set the exe to pin.exe in PIN_ROOT and idadbg directory to one of the two subdirectories you just make
16. Note, the organization steps are optional, but I HIGHLY recommend doing them and placing the "idadbg" directory into your ida install dir, cuz you don't wanna do this twice
17. Celebrate because your tool works and you can tell ida documentation to go fuck itself
