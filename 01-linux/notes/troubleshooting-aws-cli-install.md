# troubleshooting aws cli install

## Key Concepts

- Point 1
- Point 2

## Commands

`command` - what it does

## Examples

(code examples)

## What I Learned

In order to install WSL I entered a block command of four lines -
`curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"`
`unzip awscliv2.zip` 
`sudo ./aws/install`
`rm -rf aws awscliv2.zip` 
in Ubuntus terminal. However, I would get "AWS not found, but can be installed" with `sudo apt install awscli`.I also entered it all as one block, which was my main issue. This meant when one line failed, I couldnt identify which line at first.

I intially typed Y, to proceed with Ubuntus suggestion of install, but did not submit, because I realised Ubuntu could suggest and older version and it would be better if I obtained the link myself and installed the latested version. I also realised the intial link entered was x86_64, which is intel/AMD CPUs and my laptop is ARM CPU, hence why the install failed. 

To double check the CPU difference, I entered `uname -m` which repsonded with aarch64, confirming the ARM cpu issue. 

Also to double check the install failed, I entered `which unzip`, that came back with nothing showing unzip isn't installed. 

Had the four line command as a block been succesful, line one would have downloaded WSL, line two would have unziped the folder, line 3 would have installed it and line 4 would have deleted the no longer needed zip folder. 

To make sure I succesfuly aborted the previous install, I pressed Ctrl+C. 

Then I used `which aws` to check if anything is installed and it returned with nothing. 

I then wanted to make sure I refrshed Ubuntu's software list, and updated anything that was out of date. I used `sudo apt update` first which showed one thing had a new version available. Then I used `sudo apt upgrade` to install the newer version. 

Once all my install programs were updated, I then decided to proceed with the wsl install. 

I wnet to the official wsl install page, and aquired the correct link for linux arm. 

I then entered `curl "https://awscli.amazonaws.com/awscli-exe-linux-aarch64.zip" -o "awscliv2.zip"` to download the file.

I then entered `unzip awscliv2.zip` to unzip the file. 
Therafter, I entered `sudo ./aws/install` to install the file. 
Finally, I entered `rm -rf aws awscliv2.zip` to rmeove the unzipped file that is no longer neccesary. 

I orginally understood what the first 3 lines in the block command meant and does. I did not understand the 4th line. I used `rm --help`to read what the commands in the 4th line does indivdually, to understand the line as a whole. 

I then used `sudo apt install unzip` to finally install the downloaded and unzipped wsl files to Ubtuntu.

Finally, I used `aws --version` to check if the correct version was installed. 
