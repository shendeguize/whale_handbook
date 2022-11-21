# Win11 with wsl2 best practice for developing(C++/Python/Remote-development)
@Auther: https://github.com/shendeguize  
@Date: 2022.11.19  

## preamble
The author is mainly developing c++ and python on remote linux server using local win11 platform. Thus this note would be directly helpful for those developer who work same way as me.
1. Why win11 rather than linux?
    - Gaming or other enjoyment shoule also be part of daily(or maybe weekly or whatever longer but necessary) requirement.
    - There are actually lots of helpful applications such as xshell/xterm or MobaXTerm.
    - Windows Terminal and Powershell could be really powerful.
    - WSL(windows subsystem for linux) could actually satisfy maybe most of your local needs. (As it would be one the remote linux server where you actually develop your project.)
2. Remote developing IDE?
    - VSCode. Somehow a traditional way for remote developing? You could still use it.
    - JetBrains Gateway. If you are familier with PyCharm or CLion or other JetBrains' IDE, I would strongly recommand this to you.

## Step By Step
1. Window terminal
    If you are using Windows professional, Windows Terminal should be already installed with system.  
    Otherwise, just open windows store and search Windows Terminal and install.  
    ![image](https://user-images.githubusercontent.com/30931540/202843289-6940826e-fa7a-4ac2-b90d-eb5334c45dd5.png)  
    Or you could install by yourself according to [https://github.com/microsoft/terminal](https://github.com/microsoft/terminal).  
2. Powershell
    I strongly recommend you to use latest version of Powershell.  
    Just like win-terminal, you could also install latest Powershell from windows store.  
    ![image](https://user-images.githubusercontent.com/30931540/202860397-3453bf45-8169-4848-8a08-ec05a9ba2ea5.png)  
    Or you could install by yoursel according to [https://github.com/powershell/powershell](https://github.com/powershell/powershell)  
3. Setting up Powershell & Windows Terminal
    ![image](https://user-images.githubusercontent.com/30931540/202860467-fd8cdb60-dc57-4d10-ad01-b8c785629196.png)  
    ![image](https://user-images.githubusercontent.com/30931540/202860513-2eaa5a5c-c437-486a-abc3-2a61682551a6.png)  
    ![image](https://user-images.githubusercontent.com/30931540/202860531-7dcb9504-c26d-4dc6-a291-27107a3b35f6.png)  
    ![image](https://user-images.githubusercontent.com/30931540/202860583-7e618960-5d55-4bef-9c38-67d88ba4e74e.png)  
4. WSL2
    1. First edit your bios to enable intel virual technology.  
    2. Then pick up these features  
        ![image](https://user-images.githubusercontent.com/30931540/202886651-b9efa1ab-50ec-4d4f-b798-019d1d9efea0.png)  
    3. Then just follow this official guide: [https://learn.microsoft.com/en-us/windows/wsl/install](https://learn.microsoft.com/en-us/windows/wsl/install)  
        1. Set wsl default version to wsl2.
            ```wsl --set-default-version 2```
        2. Install wsl2kernel.
            Pleas look at 4.4.2.
        3. Install your linux distribution. I would recommend you directly search in windows store and install.
            ![image](https://user-images.githubusercontent.com/30931540/203039492-00c0d5b3-26cb-4c9b-9875-2553165250b8.png)
        4. Initialize your wsl.
            Just click the run bottom on windows store and setup.  
            ![image](https://user-images.githubusercontent.com/30931540/203043849-3dbefc76-6cf3-4b0e-9661-17b3548159d1.png)
            Notice: The username for wsl does not need to match with your windows username.
        5. Move your wsl to other drive.
            Actually what you need to do is just following the official guide for "exporting and importing": [https://learn.microsoft.com/en-us/windows/wsl/use-custom-distro](https://learn.microsoft.com/en-us/windows/wsl/use-custom-distro)  
            Outside wsl:  
            ```
            cd $YOUR_TARGET_DRIVE
            mkdir wsl
            wsl --export $YOUR_DISTO $YOUR_DISTO.tar
            wsl --unregister $YOUR_DISTO
            mkdir $YOUR_DISTO
            wsl --import $YOUR_DISTO $YOUR_DISTO $YOUR_DISTO.tar
            ```
        6. Some advised mount:  
            Outside wsl:  
            ```
            cd $YOUR_WSL_WORKSPACE
            mkdir Dev
            ```  
            Inside wsl:  
            ```
            cd ~
            ln -s $YOUR_WSL_WORKSPACE/Dev ~/Dev
            ```
            ![image](https://user-images.githubusercontent.com/30931540/203050093-00f233fd-df7f-4455-b08a-fef46e408bdb.png)

    4. Troubleshooting:
        1. "无法解析服务器的名称或地址"  
            [https://github.com/microsoft/WSL/issues/8025#issuecomment-1256886006](https://github.com/microsoft/WSL/issues/8025#issuecomment-1256886006)  
        2. "WslRegisterDistribution failed with error: 0x800701bc Error: 0x800701bc WSL 2 ?????????????????? https://aka.ms/wsl2kernel"  
            This fault means you're missing wsl2kernel. Download and install from here: 
            
    

...TBD...
