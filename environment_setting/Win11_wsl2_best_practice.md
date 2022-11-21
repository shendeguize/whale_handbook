# Win11 with wsl2 best practice for developing(C++/Python/Remote-development)
@Auther: https://github.com/shendeguize  
@Date: 2022.11.21  

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
    Otherwise, just open microsoft store and search Windows Terminal and install.  
    ![image](https://user-images.githubusercontent.com/30931540/202843289-6940826e-fa7a-4ac2-b90d-eb5334c45dd5.png)  
    Or you could install by yourself according to [https://github.com/microsoft/terminal](https://github.com/microsoft/terminal).  
2. Powershell
    I strongly recommend you to use latest version of Powershell.  
    Just like win-terminal, you could also install latest Powershell from microsoft store.  
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
        ![image](https://user-images.githubusercontent.com/30931540/203073099-e76c3aae-e064-485f-83e4-0deddaafd626.png)
    3. Then just follow this official guide: [https://learn.microsoft.com/en-us/windows/wsl/install](https://learn.microsoft.com/en-us/windows/wsl/install)  
        1. Set wsl default version to wsl2.
            ```wsl --set-default-version 2```
        2. Install wsl2kernel.
            Pleas look at 4.4.2.
        3. Install your linux distribution. I would recommend you directly search in microsoft store and install.
            ![image](https://user-images.githubusercontent.com/30931540/203039492-00c0d5b3-26cb-4c9b-9875-2553165250b8.png)
        4. Initialize your wsl.
            Just click the run bottom on microsoft store and setup.  
            ![image](https://user-images.githubusercontent.com/30931540/203043849-3dbefc76-6cf3-4b0e-9661-17b3548159d1.png)
            Notice: The username for wsl does not need to match with your windows username. But I recommend you to use root directly.
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
        6. How to enter wsl from powershell and exit from wsl:  
            Just use `bash` in powershell, then you would enter wsl. Use `Ctrl + D` in wsl, then you would quit back to powershell.
        7. Some advised mount:  
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
        7. Some optional steps:  
            ```
            sudo apt update
            ```
            ```
            sudo apt install tree
            sudo apt install htop
            ```
            ```
            vim ~/.bash_aliases
            ```            
            Paste and edit these:  
            ```
            # ~/.bash_aliases
            alias ll="ls -alF"
            ```  
            ```
            vim ~/.bash_profile
            ```  
            Paste and edit these:  
            ```
            # ~/.bash_profile
            if [[ -f ~/.bashrc ]] ; then
                . ~/.bashrc
            fi
            ```   
            Setup wsl2 according to [https://learn.microsoft.com/en-us/windows/wsl/wsl-config#example-wslconfig-file](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#example-wslconfig-file).  
            ```
            [wsl2]
            memory=24GB
            processors=4
            swap=8GB
            localhostforwarding=true
            nestedVirtualization=false
            ```
    4. Troubleshooting:
        1. "无法解析服务器的名称或地址"  
            [https://github.com/microsoft/WSL/issues/8025#issuecomment-1256886006](https://github.com/microsoft/WSL/issues/8025#issuecomment-1256886006)  
        2. "WslRegisterDistribution failed with error: 0x800701bc Error: 0x800701bc WSL 2 ?????????????????? https://aka.ms/wsl2kernel"  
            This fault means you're missing wsl2kernel. Download and install from here: [https://learn.microsoft.com/zh-cn/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package](https://learn.microsoft.com/zh-cn/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package)  
5. Git for windows  
    1. Download installation package from [https://git-scm.com/download/win](https://git-scm.com/download/win).  
    2. **Before you install git, you should install vscode first!**  
    3. Notice some options I recommend you to change as listed:  
        1. Use vscode as default editor.  
            ![image](https://user-images.githubusercontent.com/30931540/203053531-dc58c9a1-0198-4477-9e7a-d415bb5ddadb.png)
        2. I strongly recommend you to use unix-style line finish!  
            ![image](https://user-images.githubusercontent.com/30931540/203053880-f68ee627-54f5-4d74-bcb0-f0ecdba48162.png)
        3. Enable symbolic links.  
            ![image](https://user-images.githubusercontent.com/30931540/203054072-3781afaf-7bb3-485c-b005-b9881cbb0fea.png)
    4. Update system PATH.  
        ![image](https://user-images.githubusercontent.com/30931540/203054604-a6effa45-d5f5-4f71-9479-c7816b78730d.png)  
        Add `$GIT_ROOT\bin` and `$GIT_ROOT\mingw64\bin`. The latter would be helpful when setting ssh config and using connect.exe.  
6. Fonts and Oh-my-posh
    [Oh-My-Posh](https://ohmyposh.dev) is a prompt theme engine for any shell which supports Powershell and wsl both.  
    1. Installation  
        1. powershell:  
            Just install from microsoft store. Click [here](ms-windows-store://pdp/?productid=XP8K0HKJFRXGCK)  
            ![image](https://user-images.githubusercontent.com/30931540/203061632-aebe2957-ba71-461b-a31d-ff971e1a9f75.png)
        2. wsl:  
            Follow the official guide is enough(I prefer using manual install method): [https://ohmyposh.dev/docs/installation/linux](https://ohmyposh.dev/docs/installation/linux).  
    2. Fonts  
        most themes on Oh-my-posh requires fonts like [Nerd Fonts](https://www.nerdfonts.com/) or [cascadia-code](https://learn.microsoft.com/en-us/windows/terminal/cascadia-code). Just go to [https://github.com/ryanoasis/nerd-fonts](https://github.com/ryanoasis/nerd-fonts) and find one you like and download. (I'm using [DejaVuSansMono NFM](https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/DejaVuSansMono/Regular/complete)).  
        ![image](https://user-images.githubusercontent.com/30931540/203068319-bb6a4f99-7ac8-4e1d-be1c-e1fdccaa8197.png)
    3. Run oh-my-posh when start terminal.  
        1. Powershell:  
            ```
            code $PROFILE
            ```
            Paste and edit these in vscode:  
            ```
            #$PROFILE
            oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\paradox.omp.json" | Invoke-Expression
            ```
        2. wsl:    
            ```
            code ~/.bash_profile
            ```            
            Paste and edit these in vscode:  
            ```            
            eval "$(oh-my-posh --init --shell bash --config ~/.poshthemes/paradox.omp.json)"
            ```
        If nothing wrong, your terminal would be like:  
        ![image](https://user-images.githubusercontent.com/30931540/203068531-09f89005-bf18-4881-8587-a5d5510e4240.png)

## Other Tools or Applications:
1. [Github Desktop](https://desktop.github.com/)
2. [JetBrains](https://www.jetbrains.com/)
3. [mobaxterm](https://mobaxterm.mobatek.net/)
4. [Motrix](https://motrix.app/)
5. [XShell](https://www.xshell.com/)
6. clang-format(wsl)

## Tricks or Appendices
1. Automatically sync remote folder to local drive in case fault occured.
    Use crontab. Here is a sample for command or script  
    ```
    rsync -vhra $remote_alias:$remote_dir/$project_name $local_dir --include='**.gitignore' --filter=':- .gitignore' --delete-after
    ```
    These are for file mode change diff:  
    ```
    git submodule foreach git config core.filemode false
    git config core.filemode false
    ```  
    Reset:  
    ```
    # git config --unset core.filemode
    ```  
2. Anaconda
    1. Enable powershell remote-signed (https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy?view=powershell-7.3)[https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy?view=powershell-7.3]  
        Open powershell under admin.  
        ```
        Set-ExecutionPolicy RemoteSigned
        ```  
    2. Edit PATH  
        ![image](https://user-images.githubusercontent.com/30931540/203090221-c45ebbd5-85a3-4780-839a-26b466758825.png)
    3. Init conda in powershell (needs to reopen a new admin terminal):  
        ```
        conda init powershell
        ```  
3. KeyBoard mappings  
    1. I prefer delete `Ctrl + C` and `Ctrl + V`, as these might cause misleading.  
        ![image](https://user-images.githubusercontent.com/30931540/203091456-6fe1d77b-7546-429a-b86e-56491ad2cc6c.png)  
        ![image](https://user-images.githubusercontent.com/30931540/203091546-60a68a1f-ad24-445e-9d4f-5f0b65b95d36.png)  

4. VSCode with WSL
    [https://code.visualstudio.com/docs/remote/wsl-tutorial](https://code.visualstudio.com/docs/remote/wsl-tutorial)
    
    
        
