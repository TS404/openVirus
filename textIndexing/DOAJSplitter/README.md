# Instructions for indexing DOAJ in Solr
## Download the archive
```bash
https://doaj.org/public-data-dump/article
mv article article.tar.gz
gzip -d article.tar.gz
tar -xvf article.tar
```
You will now have a folder containing the data files named  **doaj_article_data_yyyy-mm-dd**.  Delete the **article.ta**:  we don't need it now.
## Installing the prerequisites
- Install the .NET Core from Microsoft by following [these instructions](https://docs.microsoft.com/en-us/dotnet/core/install/linux-package-manager-ubuntu-1804).
- Install [PowerShell 7.0](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-7)

## Installing the utility
- Clone or pull the latest version of the openVirus repo to your home directory with **git**
- Start PowerShell with `pwsh`
- The DOAJSplitter resides in `~/openVirus/textIndexing/DOAJSplitter/DOAJSplitter/bin/Release/netcoreapp3.1/linux-x64`.  CD to this directory
- `chmod 777 ./DOAJSplitter` to make it executable
- `nano $PROFILE` then add the line:
```powershell
Set-Alias doajsplitter "~/openVirus/textIndexing/DOAJSplitter/DOAJSplitter/bin/Release/netcoreapp3.1/linux-x64/DOAJSplitter"
```
to allow invocation of the utility with the command `doajsplitter`
- Exit and restart Powershell

## Running the utility
Once set up you can split up the DOAJ files

- `cd doaj_article_data_yyyy-mm-dd` (substituting the correct date numbers)
- `mkdir ~/doaj` to hold the output files
- `dir *.json|ForEach-Object {doajsplitter $_ ../doaj}`