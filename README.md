

MultiMiner
==========




### Author: Adam.trinity1 --> Skype:
### Email: Aminrahman24@gmail.com
### Your coins. Your pools. Your way.
__MultiMiner__ is a graphical application for crypto-coin mining on Windows, OS X and Linux. MultiMiner simplifies switching individual devices (GPUs, ASICs, FPGAs) between crypto-currencies such as Bitcoin and Litecoin.

MultiMiner uses the underlying mining engine ([bfgminer][2]) to detect available mining devices and then presents a user interface for selecting the coins you'd like to mine.

![Main Screen](https://github.com/nwoolls/MultiMiner/raw/master/Screenshots/Main%20Screen.png "Main Screen")

MultiMiner also offers several views, allowing you to display as much or as little information as you like.

![Brief View](https://github.com/nwoolls/MultiMiner/raw/master/Screenshots/Brief%20View.png "Brief View")

For new users, MultiMiner includes a Getting Started wizard that walks you through selecting an engine, a coin, a pool, and configuring [MobileMiner][14].

![Getting Started](https://github.com/nwoolls/MultiMiner/raw/master/Screenshots/Getting%20Started.png "Getting Started")

MultiMiner will automatically download and install the latest version of [bfgminer][2], making it simple for the new user to get started.

![Downloading and Installing Cgminer](https://github.com/nwoolls/MultiMiner/raw/master/Screenshots/Downloading%20and%20Installing%20Bfgminer.png "Downloading and Installing Cgminer")

You can then use the Configure Coins dialog to setup each coin that you would like to mine along with their pools, including support for load balancing.

![Configure Coins](https://github.com/nwoolls/MultiMiner/raw/master/Screenshots/Configure%20Coins.png "Configure Coins")

MultiMiner supports automatically mining the most profitable coins based on a set of configurable strategies. Profitability information is updated regularly from [CoinChoose.com][9].

![Configure Strategies](https://github.com/nwoolls/MultiMiner/raw/master/Screenshots/Configure%20Strategies.png "Configure Strategies")

MultiMiner also supports features such as relaunching crashed miners, starting with Windows, minimizing to the notification area, and mining on startup.

![Settings](https://github.com/nwoolls/MultiMiner/raw/master/Screenshots/Settings.png "Settings")

You can also use the interface provided by MultiMiner to adjust advanced settings such as API white-listing, disabling GPU mining, and automatically adjusting mining intensity based on the computer's idle time.

![Advanced Miner Settings](https://github.com/nwoolls/MultiMiner/raw/master/Screenshots/Advanced%20Miner%20Settings.png "Advanced Miner Settings")

Finally, MultiMiner supports [MobileMiner][14], an open API with mobile apps for remotely monitoring and controlling your rigs.

![MobileMiner](https://github.com/nwoolls/MultiMiner/raw/master/Screenshots/MobileMiner.png "MobileMiner")

![MobileMiner - Android](https://github.com/nwoolls/MultiMiner/raw/master/Screenshots/MobileMiner%20-%20Android.png "MobileMiner - Android")

![MobileMiner - Windows Phone](https://github.com/nwoolls/MultiMiner/raw/master/Screenshots/MobileMiner%20-%20Windows%20Phone.png "MobileMiner - Windows Phone")

By entering your MobileMiner email address and application key in the Configure Settings dialog, you will be able to remotely monitor and control your rigs _without having to open any firewalls or forward any ports_.

Downloads
----------------
You can download installers and zip files for Windows, OS X, Linux and Mono on the [GitHub Releases page][12].

Drivers
-------
Depending on your OS and the mining devices you plan on using you will need one or more of the following drivers / kernel extensions installed:

* [Block Erupter][20]
* [Blue / Red Fury][21]
* [BFL / Bitforce][22]
* [HashBuster Micro][23]
* [Bi•Fury][25]
* [AMD GPU][24]

Windows Installation
--------------------
1. Download and run the installer (.exe) file at the above link and follow instructions

The installer runs without needing admin rights and does not install to Program Files so as not to be intrusive. However, if you prefer you can use the zip file:

1. Download and extract the .zip file at the [GitHub Releases page][12]
2. Launch MultiMiner.Win.exe to get started

OS X Installation
-----------------
1. Install Xquartz available [here][7]
2. Install the latest version of [Mono][8]
3. Download and extract the __.app__.zip file at the [GitHub Releases page][12]
4. Launch MultiMiner.app to get started

MultiMiner will automatically download redistributable binaries of bfgminer from the [xgminer-osx][13] project.

![Main Screen - OS X](https://github.com/nwoolls/MultiMiner/raw/master/Screenshots/Main%20Screen%20-%20OS%20X.png "Main Screen - OS X")

Linux Installation (Debian-Based)
---------------------------------
1. Install the latest version of [Mono][8]

        sudo apt-get install mono-complete
        
2. Install your chosen mining engine

        sudo add-apt-repository ppa:unit3/bfgminer
        sudo apt-get update
        sudo apt-get install bfgminer
        
3. Download and extract the .zip file at the [GitHub Releases page][12]
4. Run MultiMiner.Win.exe using mono:

        mono MultiMiner.Win.exe
        
![Main Screen - Linux](https://github.com/nwoolls/MultiMiner/raw/master/Screenshots/Main%20Screen%20-%20Linux.png "Main Screen - Linux")
        
Generic Mono Installation
-------------------------------
1. Download and extract the zip file at the [GitHub Releases page][12]
2. Install bfgminer. For OS X, you can find packages and for doing so [here][5] and instructions for using them [here][6].
3. Install X11. Under OS X you should install Xquartz available [here][7].
4. Install the latest version of [Mono][8].
5. Run MultiMiner.Win.exe using mono:

        mono MultiMiner.Win.exe
        



        


```csharp
//examples of using MultiMiner.Xgminer.dll and MultiMiner.Xgminer.Api.dll

//download and install the latest version of bfgminer
const string executablePath = @"D:\bfgminer\";
const string executableName = "bfgminer.exe";

Console.WriteLine("Downloading and installing {0} from {1} to the directory {2}",
    executableName, Xgminer.Installer.GetMinerDownloadRoot(), executablePath);

//download and install bfgminer from the official website
Xgminer.Installer.InstallMiner(executablePath);
try
{
    //create an instance of Miner with the downloaded executable
    MinerConfiguration minerConfiguration = new MinerConfiguration()
    {
        ExecutablePath = Path.Combine(executablePath, executableName)
    };
    Miner miner = new Miner(minerConfiguration);

    //use it to iterate through devices
    List<Device> deviceList = miner.ListDevices();

    Console.WriteLine("Using {0} to list available mining devices", executableName);

    //output devices
    foreach (Device device in deviceList)
        Console.WriteLine("Device detected: {0}\t{1}\t{2}", device.Kind, device.Driver, device.Name);

    //start mining if there are devices
    if (deviceList.Count > 0)
    {
        Console.WriteLine("{0} device(s) detected, mining Bitcoin on Bitminter using all devices", deviceList.Count);

        //setup a pool
        MiningPool pool = new MiningPool()
        {
            Host = "mint.bitminter.com",
            Port = 3333,
            Username = "nwoolls_deepcore",
            Password = "deepcore"
        };
        minerConfiguration.Pools.Add(pool);

        //specify algorithm
        minerConfiguration.Algorithm = CoinAlgorithm.SHA256;

        //disable GPU mining
        minerConfiguration.DisableGpu = true;

        //specify device indexes to use
        for (int i = 0; i < deviceList.Count; i++)
            minerConfiguration.DeviceDescriptors.Add(deviceList[i]);

        //enable RPC API
        minerConfiguration.ApiListen = true;
        minerConfiguration.ApiPort = 4028;

        Console.WriteLine("Launching {0}", executableName);

        //start mining
        miner = new Miner(minerConfiguration);
        System.Diagnostics.Process minerProcess = miner.Launch();
        try
        {
            //get an API context
            Xgminer.Api.ApiContext apiContext = new Xgminer.Api.ApiContext(minerConfiguration.ApiPort);
            try
            {
                //mine for one minute, monitoring hashrate via the API
                for (int i = 0; i < 6; i++)
                {
                    Thread.Sleep(1000 * 10); //sleep 10s

                    //query the miner process via its RPC API for device information
                    List<Xgminer.Api.Responses.DeviceInformationResponse> deviceInformation = apiContext.GetDeviceInformation();

                    //output device information
                    foreach (Xgminer.Api.Responses.DeviceInformationResponse item in deviceInformation)
                        Console.WriteLine("Hasrate for device {0}: {1} current, {2} average", item.Index,
                                item.CurrentHashrate, item.AverageHashrate);
                }
            }
            finally
            {
                Console.WriteLine("Quitting mining via the RPC API");

                //stop mining, try the API first
                apiContext.QuitMining();
            }
        }
        finally
        {
            Console.WriteLine("Killing any remaining process");

            //then kill the process
            try
            {
                minerProcess.Kill();
                minerProcess.WaitForExit();
                minerProcess.Close();
            }
            catch (InvalidOperationException ex)
            {
                //already closed
            }
        }
    }
    else
    {
        Console.WriteLine("No devices capable of mining detected");
    }
}
finally
{
    Console.WriteLine("Cleaning up, deleting directory {0}", executablePath);
    Directory.Delete(executablePath, true);
}

Console.WriteLine("Press any key to exit");
Console.ReadKey();
```

License
-------
not for use, unless given permission by: aminrahman24@gmail.com 
all code is copyrighted with NDA.




Credits to All the GITHUB REPO's I FOKED LMFAO.

[1]: https://github.com/ckolivas/cgminer
[2]: https://github.com/luke-jr/bfgminer
[3]: https://www.dropbox.com/s/ne5eywfx8v7hneb/MultiMiner-1.0.7.zip
[4]: http://ck.kolivas.org/apps/cgminer/
[5]: http://homebrew.xgminer.com
[6]: http://howto.xgminer.com
[7]: http://xquartz.macosforge.org/
[8]: http://www.mono-project.com/Main_Page
[9]: http://coinchoose.com/
[10]: http://luke.dashjr.org/programs/bitcoin/files/bfgminer/
[11]: https://www.dropbox.com/s/o08inghtw7ut1an/MultiMiner-1.0.7.exe
[12]: https://github.com/nwoolls/MultiMiner/releases
[13]: http://xgminer.com
[14]: http://www.mobileminerapp.com
[15]: http://talk.multiminerapp.com
[16]: https://github.com/nwoolls/MultiMiner/tree/master/MultiMiner.Xgminer
[17]: https://github.com/nwoolls/MultiMiner/tree/master/MultiMiner.Xgminer.Api
[18]: https://github.com/luke-jr/bfgminer/blob/bfgminer/README.RPC
[19]: https://github.com/nwoolls/MultiMiner/tree/master/MultiMiner.Example
[20]: http://www.silabs.com/products/mcu/pages/usbtouartbridgevcpdrivers.aspx
[21]: http://minecoin.net/bluefuryredfury-driver-for-windows/
[22]: http://www.ftdichip.com/Drivers/VCP.htm
[23]: http://zadig.akeo.ie/
[24]: http://support.amd.com/en-us/download
[25]: http://store.bitcoin.org.pl/support
